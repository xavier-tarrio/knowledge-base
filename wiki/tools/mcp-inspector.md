---
title: MCP Inspector
type: tool
sources: [mcp-inspector-doc]
last_updated: 2026-05-10
---

# MCP Inspector

## What it does
An interactive browser-based developer tool for testing and debugging MCP servers. Runs directly via `npx` with no installation required. Lets you browse a server's tools, resources, and prompts, execute them with custom inputs, and inspect results — all without needing Claude Desktop or any other MCP host.

```bash
npx @modelcontextprotocol/inspector <command>
# Example: inspect the filesystem server
npx -y @modelcontextprotocol/inspector npx @modelcontextprotocol/server-filesystem ~/Desktop
```

## When to use it
- During MCP server development, to validate that your tools/resources/prompts are correctly defined and returning expected results
- To debug a server that isn't showing up or behaving correctly in Claude Desktop
- To explore an unfamiliar MCP server before connecting it to Claude
- For iterative development: make a change → test in Inspector → connect to host

## When NOT to use it
- For production monitoring (it's a dev/debug tool only)
- As a substitute for integration tests — test with the real host (Claude Desktop, etc.) before shipping

## Key features

| Feature | What it shows |
|---------|--------------|
| **Tools tab** | All tools with schemas, custom input form, execution results |
| **Resources tab** | Available resources with MIME types; content inspection; subscription testing |
| **Prompts tab** | Prompt templates with argument forms; generated message preview |
| **Notifications pane** | Server logs and notifications in real time |
| **Server connection pane** | Transport selection (STDIO or HTTP); custom CLI args and env vars |

## Key concepts to understand
- [[concepts/model-context-protocol]] — the protocol the Inspector operates over
- [[concepts/mcp-primitives]] — the three things being tested (tools, resources, prompts)

## Sources
- [[sources/mcp-inspector-doc]] — official MCP Inspector documentation: installation, features, best practices
