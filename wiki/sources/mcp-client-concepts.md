---
title: Understanding MCP Clients
type: source
source_file: raw/Understanding MCP clients.md
date_ingested: 2026-05-10
tags: [mcp, clients, transport, message-types]
---

# Understanding MCP Clients

## Summary
Anthropic Academy's lesson on MCP clients — the communication bridge between your application server and MCP servers. Covers transport mechanisms, the two primary message types, and the full request flow from user query through tool execution back to Claude.

## Key takeaways
- MCP client is transport-agnostic: most common is same-machine STDIO, but HTTP and WebSockets are also supported
- Two primary message exchanges: `ListToolsRequest/ListToolsResult` (what tools exist?) and `CallToolRequest/CallToolResult` (execute this tool)
- Full flow for "What repositories do I have?": user query → server discovers tools → sends to Claude → Claude decides tool → client calls MCP server → result returned → Claude responds
- The client handles all protocol details so your application code doesn't have to

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Connections
Complements the server concepts doc. The request flow diagram is the best illustration of how client, Claude, and MCP server interact within a single user query.
