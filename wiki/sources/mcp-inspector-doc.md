---
title: MCP Inspector Documentation
type: source
source_file: raw/MCP Inspector.md
date_ingested: 2026-05-10
tags: [mcp, debugging, inspector, dev-tools]
---

# MCP Inspector Documentation

## Summary
Official documentation for the MCP Inspector developer tool. Covers installation, all interactive tabs (Tools, Resources, Prompts, Notifications), and the recommended development workflow.

## Key takeaways
- Zero-install: runs via `npx @modelcontextprotocol/inspector <command>`; supports both npm packages and locally developed servers
- Four tabs mirror the three primitives: Tools (call with custom inputs, see results), Resources (browse, inspect content, test subscriptions), Prompts (test with custom arguments, preview messages), plus Notifications (server logs in real time)
- Recommended workflow: start server → connect Inspector → iterative test → test edge cases → connect to real host (Claude Desktop, etc.)
- Server connection pane allows selecting transport type and customizing CLI args + env vars for the test session

## Concepts covered
- [[concepts/mcp-primitives]]
- [[concepts/model-context-protocol]]

## Tools mentioned
- [[tools/mcp-inspector]]

## Connections
Pairs with [[sources/mcp-build-server]] — the Inspector is what you use immediately after running `uv run weather.py` to verify your server before connecting to Claude Desktop.
