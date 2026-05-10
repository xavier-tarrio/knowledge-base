---
title: Model Context Protocol (MCP)
type: concept
sources: [claude-101-connecting-tools, mcp-what-is, mcp-introducing, mcp-architecture-overview, mcp-beginners-course, mcp-server-concepts]
last_updated: 2026-05-10
---

# Model Context Protocol (MCP)

## What it is
An open-source protocol standard that defines how AI applications connect to external tools, data sources, and services. Often described as "USB-C for AI" — one standardized interface that, once implemented, works with any MCP-compatible host or server. Created by Anthropic, open to the ecosystem; 113+ clients support it as of mid-2025.

## Why it matters (for this domain)
Without MCP, connecting Claude to a database, a Slack workspace, and a REST API requires three separate custom integrations — each with its own tool schemas, error handling, and maintenance burden. With MCP, those integrations are pre-built MCP servers you just connect to. For data engineering: querying Trino, reading dbt model schemas, or triggering Airflow runs all become possible as MCP tools, maintainable at scale.

## How it works

### Architecture: three roles

```
MCP Host (Claude Desktop / VS Code / your chat app)
  ├── MCP Client 1  ──── MCP Server A  (e.g. Filesystem)
  ├── MCP Client 2  ──── MCP Server B  (e.g. Database)
  └── MCP Client 3  ──── MCP Server C  (e.g. GitHub)
```

- **MCP Host**: The AI application that manages the interaction. Creates one dedicated client per server. Examples: Claude Desktop, Claude Code, VS Code Copilot, Cursor.
- **MCP Client**: One per server. Handles the JSON-RPC protocol, capability negotiation, and surfaces server capabilities to the host.
- **MCP Server**: Exposes capabilities (tools, resources, prompts) via the protocol. Can be local (STDIO) or remote (HTTP).

### What servers expose: three primitives

| Primitive | Controlled by | Purpose |
|-----------|--------------|---------|
| **Tools** | Model | Executable functions — write to DB, call API, run query |
| **Resources** | Application | Read-only data sources — schemas, file contents, docs |
| **Prompts** | User | Reusable workflow templates — slash commands |

See [[concepts/mcp-primitives]] for full detail.

### Two transports

- **STDIO** — local processes on the same machine, via stdin/stdout. Zero network overhead. One client per server. Used for locally installed servers (e.g. `npx @modelcontextprotocol/server-filesystem`).
- **Streamable HTTP** — remote servers, HTTP POST + Server-Sent Events. OAuth 2.0 support. Multiple clients per server. Used for cloud services and team-shared servers.

### Wire protocol
All messages use **JSON-RPC 2.0**. Client and server negotiate capabilities in an `initialize` handshake before any operations. Standard operations: `tools/list`, `tools/call`, `resources/list`, `resources/read`, `prompts/list`, `prompts/get`.

## Practical notes
- **MCP ≠ Tool Use**: Tool Use is how Claude *calls* a function. MCP is about *who writes the function definitions*. Without MCP: you write all schemas yourself. With MCP: the server ships them pre-built. MCP is the integration distribution layer.
- **STDIO for prototyping, HTTP for production**: Start local to validate your tools, then deploy over HTTP for team access.
- **Build once, use everywhere**: A Python `@mcp.tool()` function works in Claude Desktop, Claude Code, VS Code Copilot, Cursor, and any other MCP host — no changes needed.
- **Security surface is wider than standard web**: Prompt injection via external content, tool poisoning via metadata, token passthrough attacks. See [[concepts/mcp-security]].
- **Permissions are you-scoped**: Claude can only see data YOU have access to on connected services.

## See also
- [[concepts/mcp-primitives]] — Tools, Resources, Prompts in depth
- [[concepts/mcp-security]] — AI-specific attack vectors
- [[concepts/agentic-ai]] — MCP is the infrastructure layer enabling autonomous AI behavior
- [[tools/mcp-connectors]] — Claude's built-in MCP connectors (web + desktop)
- [[tools/mcp-inspector]] — tool for testing MCP servers during development

## Sources
- [[sources/claude-101-connecting-tools]] — explains MCP as the standard powering Claude connectors, setup instructions
- [[sources/mcp-what-is]] — introductory definition and USB-C analogy
- [[sources/mcp-introducing]] — Anthropic Academy: the problem MCP solves
- [[sources/mcp-architecture-overview]] — official architecture: participants, layers, primitives, JSON-RPC
- [[sources/mcp-beginners-course]] — Microsoft 11-lesson course: end-to-end implementation
- [[sources/mcp-server-concepts]] — server primitives in depth with full examples
