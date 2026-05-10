---
title: Build an MCP Server (Python Quickstart)
type: source
source_file: raw/Build an MCP server.md
date_ingested: 2026-05-10
tags: [mcp, python, tutorial, fastmcp, weather]
---

# Build an MCP Server (Python Quickstart)

## Summary
Official hands-on tutorial from modelcontextprotocol.io for building a Python MCP weather server and connecting it to Claude Desktop. Uses the FastMCP framework with the `@mcp.tool()` decorator pattern. Covers environment setup, tool implementation, server configuration in Claude Desktop, and troubleshooting.

## Key takeaways
- FastMCP pattern: decorate a Python async function with `@mcp.tool()` — docstring becomes the tool description, type hints become the input schema. About 50 lines for a working two-tool server.
- STDIO logging gotcha: NEVER write to stdout in an STDIO server (`print()` corrupts JSON-RPC messages); use `sys.stderr` or the `logging` module instead
- Claude Desktop config is a JSON file at `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) / `%APPDATA%\Claude` (Windows); add `mcpServers` key with command + args
- What happens when you ask a question: user asks → Claude analyzes tools → client executes chosen tool via MCP server → result sent to Claude → natural language response
- Troubleshooting: "server not showing up" = check JSON syntax, use absolute paths, fully quit and restart Claude Desktop (closing the window doesn't quit it on Windows)

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Tools mentioned
- [[tools/mcp-inspector]]
- [[tools/claude-desktop]]

## Connections
The entry point for anyone wanting to build their first MCP server. FastMCP is the recommended Python path; the `@mcp.tool()` pattern is the pattern to internalize.
