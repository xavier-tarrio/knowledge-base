---
title: Understanding MCP Servers
type: source
source_file: raw/Understanding MCP servers.md
date_ingested: 2026-05-10
tags: [mcp, servers, primitives, tools, resources, prompts]
---

# Understanding MCP Servers

## Summary
Official deep-dive into MCP server capabilities from modelcontextprotocol.io. Covers all three primitives (tools, resources, prompts) with detailed protocol operations, example implementations, user interaction models, and a multi-server travel planning walkthrough that shows primitives composing together.

## Key takeaways
- Tools use JSON Schema for input validation; `tools/list` discovers, `tools/call` executes; user consent mechanisms are expected (approval dialogs, permission settings, activity logs)
- Resources support two URI patterns: direct (fixed URI) and templates (parameterized, e.g. `travel://activities/{city}/{category}`); templates support parameter completion for discovery UX
- Resources expose MIME types and support `resources/subscribe` for change notifications
- Prompts are user-controlled (slash commands, command palettes), support parameter completion, and can reference available tools and resources for complex workflows
- The real power of MCP: multiple servers composing together — Travel + Weather + Calendar servers combining seamlessly for a full travel booking workflow
- Who controls what: Tools = model, Resources = application, Prompts = user — each requires different UX patterns

## Concepts covered
- [[concepts/mcp-primitives]]
- [[concepts/model-context-protocol]]

## Connections
Best source for concrete tool definition examples (JSON Schema patterns). The multi-server travel planning scenario (section "Bringing Servers Together") is the most useful illustration of MCP's compositional power.
