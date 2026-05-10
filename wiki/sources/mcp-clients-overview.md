---
title: MCP Clients (Anthropic Academy)
type: source
source_file: raw/MCP clients.md
date_ingested: 2026-05-10
tags: [mcp, clients, transport, message-flow]
---

# MCP Clients (Anthropic Academy)

## Summary
Anthropic Academy lesson on the MCP client role. Covers transport agnosticism, the two primary message types, and the complete request flow from user query to Claude response using the GitHub repositories example.

## Key takeaways
- MCP client is transport-agnostic: STDIO (same machine, most common) or HTTP/WebSockets (remote)
- Two core message pairs: `ListToolsRequest/ListToolsResult` (discovery) and `CallToolRequest/CallToolResult` (execution)
- Complete query flow: user asks → server discovers tools via `tools/list` → sends to Claude → Claude picks tool → client calls tool → result returned to Claude → Claude formulates response
- The client abstracts all protocol complexity so application code stays clean

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Connections
Pairs with [[sources/mcp-client-concepts]] for a complete client picture. The query flow is the single most useful concept for understanding how a user message becomes a tool call.
