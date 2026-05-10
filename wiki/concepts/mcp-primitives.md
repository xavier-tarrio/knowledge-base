---
title: MCP Primitives (Tools, Resources, Prompts)
type: concept
sources: [mcp-server-concepts, mcp-architecture-overview, mcp-beginners-course]
last_updated: 2026-05-10
---

# MCP Primitives

## What it is
The three building blocks that MCP servers expose to AI applications. Each serves a different purpose and is controlled by a different actor in the interaction. Getting the primitive type right is the core design decision when building any MCP server.

## Why it matters (for this domain)
Choosing the wrong primitive breaks the UX. If you expose a Trino table as a Resource, Claude reads it passively as context. If you expose it as a Tool (`run_query`), Claude queries it dynamically based on user intent. A schema definition is a Resource; the ability to execute a query is a Tool.

## How it works

### Tools — model-controlled execution
The most powerful primitive. Executable functions with typed JSON Schema inputs/outputs. The model decides when to call them based on context and user request.

- Discovered via `tools/list`, executed via `tools/call`
- May require user consent before execution (clients implement approval dialogs)
- Should be single-responsibility — one tool, one job

```typescript
{
  name: "run_trino_query",
  description: "Execute a read-only SQL query against Trino",
  inputSchema: {
    type: "object",
    properties: {
      query: { type: "string", description: "SQL query to execute" },
      catalog: { type: "string", description: "Trino catalog name" }
    },
    required: ["query"]
  }
}
```

### Resources — application-controlled context
Passive data sources. The *application* (not the model) decides when to include them as context. Think of resources as the "documents" Claude can draw from, without taking action.

- Each resource has a unique URI: `file:///path`, `trino://catalog/schema/table`, `calendar://events/2024`
- Two patterns:
  - **Direct resources** — fixed URIs pointing to specific data
  - **Resource templates** — parameterized URIs: `trino://catalog/{schema}/{table}/schema`
- Support parameter completion (typing "Pay" might suggest "Payments" schema)
- Discovered via `resources/list` + `resources/templates/list`, read via `resources/read`
- Can subscribe to change notifications via `resources/subscribe`

### Prompts — user-controlled workflows
Reusable instruction templates that users explicitly invoke. They encode expertise about how to best use the server's tools and resources — like slash commands for complex workflows.

- Parameterized with typed arguments and optional completion hints
- Surface as slash commands (`/generate-eos-model`), command palettes, or dedicated buttons
- Discovered via `prompts/list`, retrieved with arguments via `prompts/get`

### Who controls what — the critical mental model

| Primitive | Controlled by | Triggered when | Analogy |
|-----------|--------------|----------------|---------|
| **Tools** | Model | Model decides it needs to act | A function the AI invokes |
| **Resources** | Application | App decides what context to inject | A document added to context |
| **Prompts** | User | User explicitly starts a workflow | A slash command |

### Client primitives (less common, but important)
Servers can also request capabilities FROM the client:
- **Sampling** — server asks the host LLM to generate a completion (useful when server needs AI but doesn't want to pick a model)
- **Elicitation** — server requests additional information from the user mid-operation
- **Logging** — server sends debug logs to the client

## Practical notes
- **Compose small tools**: `list_schemas()` + `get_table_columns()` + `run_query()` is far more flexible than a single `do_everything()` tool.
- **Schemas as resources**: Always expose your DB schema definitions as resources — Claude reads them as context before writing queries, producing far better SQL.
- **Prompts encode expertise**: If you run the same complex workflow repeatedly ("generate EOS YAML for table X"), encode it as a prompt with parameters. It becomes reproducible and shareable.
- **Resource templates enable discovery**: Dynamic URIs mean Claude can navigate your data structure without you hard-coding every possible path.

## See also
- [[concepts/model-context-protocol]] — full architecture and transport layer
- [[concepts/agentic-ai]] — how tool composition creates autonomous behavior
- [[tools/mcp-inspector]] — tool for testing all three primitive types interactively

## Sources
- [[sources/mcp-server-concepts]] — primary; full examples, user interaction models, travel planning walkthrough
- [[sources/mcp-architecture-overview]] — formal primitive definitions and JSON-RPC operations
- [[sources/mcp-beginners-course]] — practical tools/resources/prompts perspective (lessons 2 and 5)
