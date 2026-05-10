---
title: Build an MCP Client (Python Quickstart)
type: source
source_file: raw/Build an MCP client.md
date_ingested: 2026-05-10
tags: [mcp, python, tutorial, client, anthropic-sdk]
---

# Build an MCP Client (Python Quickstart)

## Summary
Official tutorial for building an LLM-powered MCP client in Python that connects to any MCP server. The client uses the Anthropic Python SDK alongside the MCP SDK to create a full chat loop where Claude decides which tools to call based on user queries.

## Key takeaways
- Client architecture: `MCPClient` class with `AsyncExitStack` for resource management → `connect_to_server()` → `process_query()` (the core loop) → `chat_loop()` for interactive use
- `process_query()` flow: list available tools → send query to Claude with tool schemas → if Claude uses a tool, execute it → send result back to Claude → get final response
- The client passes tool schemas to Claude at each API call, not just once — Claude decides per-query which tools to use
- Supports both Python (`.py`) and Node.js (`.js`) servers — detects by file extension
- First response may take up to 30 seconds (server init + Claude processing + tool execution); subsequent responses are faster
- Security: store API keys in `.env`, add `.env` to `.gitignore`

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Connections
Pairs with [[sources/mcp-build-server]]. Together they show the complete picture: server exposes tools, client connects and enables Claude to call them via the Anthropic API.
