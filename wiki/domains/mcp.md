---
title: "Domain: Model Context Protocol"
type: domain
created: 2026-05-10
last_updated: 2026-05-10
dependencies: [generative-ai, agentic-ai]
---

# Domain: Model Context Protocol (MCP)

> **Prerequisites**: [[concepts/generative-ai]] → [[concepts/agentic-ai]] → this domain
>
> **What you'll understand after this**: How AI models connect to the outside world in a standardized, maintainable way — and how to build that connection yourself.

---

## The Problem: Every Integration Was Custom

Imagine you're building a chat assistant that needs to answer questions about your company's data. It needs to query a database, read documentation, check a calendar, and send a Slack message. Without a standard, you'd write four separate integrations — each with its own tool schemas, error handling, authentication, and maintenance burden.

Now multiply that by every company building AI, every database vendor, every SaaS tool. You get M × N custom integrations — every client needs to know about every server, in every combination.

**MCP solves this with a standard**: one protocol, one interface. Any AI application that speaks MCP can talk to any MCP server. The ecosystem becomes M + N instead of M × N.

> **Analogy**: MCP is to AI what USB-C is to devices. Before USB-C, every device had its own cable. After USB-C, one standard works everywhere. Before MCP, every AI integration was custom code. After MCP, one standard works everywhere.

---

## Architecture: Who Does What

MCP defines three roles that interact through a standardized protocol:

```mermaid
flowchart TD
    subgraph Host["MCP Host (Your AI App / Claude Desktop / VS Code)"]
        C1[MCP Client 1]
        C2[MCP Client 2]
        C3[MCP Client 3]
    end

    S1["MCP Server A\n(Filesystem)"]
    S2["MCP Server B\n(Database / Trino)"]
    S3["MCP Server C\n(GitHub / Slack)"]

    C1 -- "STDIO (local)" --> S1
    C2 -- "STDIO (local)" --> S2
    C3 -- "HTTP + OAuth (remote)" --> S3
```

| Role | What it is | Examples |
|------|-----------|---------|
| **MCP Host** | The AI application. Creates and manages clients. | Claude Desktop, Claude Code, VS Code, Cursor |
| **MCP Client** | One per server. Handles the protocol, capability negotiation, message routing. | Created by the host automatically |
| **MCP Server** | Exposes capabilities to clients. Can be local or remote. | Filesystem server, GitHub server, your custom Trino server |

**Key insight**: The host never talks to servers directly — always through a dedicated client. This is what enables one host to talk to many servers simultaneously without them interfering with each other.

---

## The Three Primitives: What Servers Expose

Every MCP server can expose up to three types of capabilities. Understanding which primitive to use for what is the core design decision when building a server.

```mermaid
flowchart LR
    Server["MCP Server"]

    Server --> T["🔧 Tools\nModel decides when to call\nExecutable functions\nEx: run_query, send_email"]
    Server --> R["📄 Resources\nApp decides when to include\nRead-only data / context\nEx: table schemas, docs"]
    Server --> P["💬 Prompts\nUser explicitly invokes\nWorkflow templates\nEx: /generate-report"]

    T --> M["🤖 AI Model"]
    R --> A["🖥️ Application"]
    P --> U["👤 User"]
```

### Tools — the model acts
Tools are executable functions. The model reads the tool's description and decides autonomously whether to call it and with what arguments. Think of them as functions your AI can invoke.

```python
@mcp.tool()
async def run_trino_query(query: str, catalog: str = "hive") -> str:
    """Execute a read-only SQL query against Trino.
    
    Args:
        query: The SQL query to execute
        catalog: Trino catalog name (default: hive)
    """
    # FastMCP generates the JSON Schema from type hints + docstring
    return await execute_query(query, catalog)
```

### Resources — context flows in
Resources are passive data sources. The application controls when to include them in the model's context — no action taken, just information provided. URI-addressed, like a file system.

```
trino://hive/payments/transactions       → schema definition for transactions table
file:///docs/eos-model-spec.md           → EOS YAML specification
calendar://my-calendar/this-week         → current week's meetings
```

### Prompts — user guides the workflow
Prompts are parameterized workflow templates the user explicitly invokes. They encode expertise about how to use the server's tools and resources together for a complex task.

```
/generate-eos-model table=transactions catalog=hive
  → guides Claude through: read schema → check existing models → generate YAML → validate
```

---

## How a Request Flows

Here's what happens from the moment a user types a question to when they see an answer:

```mermaid
sequenceDiagram
    participant U as User
    participant App as Your App / Claude Desktop
    participant C as MCP Client
    participant S as MCP Server
    participant LLM as Claude (LLM)

    U->>App: "What's the schema of the payments table?"
    App->>C: Forward query
    C->>S: tools/list (discover available tools)
    S-->>C: [{name: "get_schema", ...}, {name: "run_query", ...}]
    C->>LLM: Send query + tool schemas
    LLM-->>C: "Use get_schema(table='payments')"
    C->>S: tools/call {name: "get_schema", args: {table: "payments"}}
    S-->>C: {columns: [...], types: [...]}
    C->>LLM: Here is the schema result
    LLM-->>C: Natural language answer
    C-->>App: Final response
    App-->>U: "The payments table has columns: id (bigint), amount (decimal)..."
```

**What the model sees**: At each step, Claude sees your query AND a list of available tool schemas (names + descriptions + input shapes). It decides which tool to call — or none at all — based on what's needed.

---

## Two Transports: Local vs Remote

How the client and server communicate depends on where the server runs:

```mermaid
flowchart LR
    subgraph Local["Local (same machine)"]
        H1[Host] -- "stdin/stdout\nJSON-RPC" --> S1["MCP Server\n(process)"]
    end

    subgraph Remote["Remote (cloud/team)"]
        H2[Host] -- "HTTP POST\n+ SSE streaming\n+ OAuth 2.0" --> S2["MCP Server\n(HTTP service)"]
    end
```

| | STDIO | Streamable HTTP |
|--|-------|----------------|
| **Where server runs** | Same machine as host | Anywhere (cloud, team server) |
| **Communication** | stdin/stdout streams | HTTP POST + Server-Sent Events |
| **Auth** | Environment variables | OAuth 2.0 (bearer tokens) |
| **Clients per server** | 1 | Many |
| **Use when** | Dev, personal tools, Claude Desktop | Team tools, production, public servers |
| **Example** | `npx @modelcontextprotocol/server-filesystem` | GitHub MCP server (hosted by GitHub) |

---

## Security: AI-Specific Threats

MCP introduces attack vectors that don't exist in traditional software. The ones you need to know:

```mermaid
flowchart TD
    subgraph Threats["Key MCP Threats"]
        PI["🔴 Prompt Injection\nMalicious instructions hidden in\nexternal content (PDFs, SQL results)"]
        TP["🔴 Tool Poisoning\nMalicious tool description field\ntricks model into bad behavior"]
        TK["🔴 Token Passthrough\nServer forwards token without\nvalidating it was issued for it"]
        SS["🟡 SSRF\nMalicious OAuth URLs point to\ninternal network resources"]
        SH["🟡 Session Hijack\nStolen session ID impersonates user"]
    end

    subgraph Mitigations["Mitigations"]
        PI --> M1["Spotlighting + delimiters\nSeparate trusted vs untrusted content"]
        TP --> M2["Pin tool schemas at approval\nAudit before connecting"]
        TK --> M3["Validate token audience claim\nMUST match your server"]
        SS --> M4["Block private IP ranges\nEnforce HTTPS"]
        SH --> M5["Bind session to user_id:session_id\nCryptographic random IDs"]
    end
```

**The rule of thumb**: Think of community MCP servers like npm packages. Trust official providers (GitHub's own server, AWS's own server). Audit community servers before connecting.

---

## Building Your First MCP Server: The Pattern

With the Python SDK, a working server is ~50 lines:

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("my-server")

@mcp.tool()
async def get_schema(table: str, catalog: str = "hive") -> dict:
    """Get column definitions for a Trino table.
    
    Args:
        table: Table name
        catalog: Trino catalog (default: hive)
    """
    return await trino_client.describe_table(catalog, table)

@mcp.tool()  
async def run_query(sql: str) -> list[dict]:
    """Execute a read-only SQL query against Trino."""
    return await trino_client.execute(sql)

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

Then add it to Claude Desktop's config:
```json
{
  "mcpServers": {
    "my-server": {
      "command": "python",
      "args": ["/absolute/path/to/server.py"]
    }
  }
}
```

---

## Learning Dependency Map

Where MCP sits in the broader knowledge graph:

```mermaid
flowchart LR
    GA[Generative AI\nconcepts/generative-ai] --> CW[Context Window\nconcepts/context-window]
    GA --> AIA[Agentic AI\nconcepts/agentic-ai]
    AIA --> MCP[MCP Protocol\nconcepts/model-context-protocol]
    MCP --> PRIM[MCP Primitives\nconcepts/mcp-primitives]
    MCP --> SEC[MCP Security\nconcepts/mcp-security]
    PRIM --> BUILD["Build MCP Server\n(sources/mcp-build-server)"]
    PRIM --> BUILD2["Build MCP Client\n(sources/mcp-build-client)"]
    BUILD --> INSP[MCP Inspector\ntools/mcp-inspector]

    style MCP fill:#2563eb,color:#fff
    style PRIM fill:#7c3aed,color:#fff
    style SEC fill:#dc2626,color:#fff
```

**Learning order**: Generative AI → Agentic AI → MCP Protocol → Primitives → build a server → test with Inspector → connect to Claude Desktop.

---

## Concepts in This Domain

- [[concepts/model-context-protocol]] — the full protocol reference
- [[concepts/mcp-primitives]] — tools, resources, and prompts in depth
- [[concepts/mcp-security]] — AI-specific threats and mitigations
- [[tools/mcp-inspector]] — the debugging tool
- [[tools/mcp-connectors]] — Claude's built-in connectors (pre-built MCP servers for popular services)
