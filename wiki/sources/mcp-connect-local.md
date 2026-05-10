---
title: Connect to Local MCP Servers
type: source
source_file: raw/Connect to local MCP servers.md
date_ingested: 2026-05-10
tags: [mcp, claude-desktop, local, filesystem, configuration]
---

# Connect to Local MCP Servers

## Summary
Tutorial for connecting Claude Desktop to local MCP servers, using the official filesystem server as the example. Covers configuration, the approval model, troubleshooting, and platform-specific gotchas for Windows.

## Key takeaways
- Configuration via JSON file: add `mcpServers` key to `claude_desktop_config.json`; each server gets a `command` + `args` entry
- Approval model: Claude requests explicit user approval before any file system operation — you review and approve each action individually
- Windows gotcha: `${APPDATA}` may not expand in paths; add `"APPDATA": "C:\\Users\\user\\AppData\\Roaming\\"` to the `env` key in config
- Log locations: macOS `~/Library/Logs/Claude/`, Windows `%APPDATA%\Claude\logs`; `mcp.log` for connection issues, `mcp-server-SERVERNAME.log` for server-specific errors
- "Server not showing up": check JSON syntax, use absolute paths (not relative), **fully quit** Claude Desktop (window close ≠ quit on Windows — use system tray)

## Concepts covered
- [[concepts/model-context-protocol]]

## Tools mentioned
- [[tools/claude-desktop]]
- [[tools/mcp-connectors]]

## Connections
Practical setup guide. The Windows path expansion gotcha is relevant given the current environment. The approval model walkthrough explains the human-in-the-loop design of local MCP.
