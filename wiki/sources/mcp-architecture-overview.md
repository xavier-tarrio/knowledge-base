---
title: MCP Architecture Overview
type: source
source_file: raw/Architecture overview.md
date_ingested: 2026-05-10
tags: [mcp, architecture, protocol, json-rpc]
---

# MCP Architecture Overview

## Summary
Official architectural documentation from modelcontextprotocol.io. Covers the three participant roles (Host, Client, Server), the two protocol layers (data layer and transport layer), the three server primitives (tools, resources, prompts), the three client primitives (sampling, elicitation, logging), and the JSON-RPC 2.0 wire protocol.

## Key takeaways
- Three roles: **Host** (AI app) creates one **Client** per **Server**; local servers (STDIO) serve one client; remote servers (Streamable HTTP) serve many
- Two layers: **data layer** (JSON-RPC 2.0 messages, lifecycle, primitives) and **transport layer** (STDIO or Streamable HTTP)
- Three server primitives: Tools (AI calls), Resources (context data), Prompts (interaction templates)
- Three client primitives: Sampling (server requests LLM completion), Elicitation (server requests user input), Logging
- Lifecycle: every connection starts with an `initialize` handshake for capability negotiation
- Notifications enable real-time push updates from server to client (e.g. `notifications/tools/list_changed`)

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Tools mentioned
- [[tools/mcp-inspector]]

## Connections
The authoritative architectural reference. More technical than the introductory sources but essential for building servers or clients.
