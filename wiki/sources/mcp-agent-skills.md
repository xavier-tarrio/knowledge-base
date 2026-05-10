---
title: Build with Agent Skills
type: source
source_file: raw/Build with Agent Skills.md
date_ingested: 2026-05-10
tags: [mcp, agent-skills, claude-code, scaffolding, deployment]
---

# Build with Agent Skills

## Summary
Official guide to using agent skills (portable instruction sets for AI coding assistants) to scaffold MCP servers. The `mcp-server-dev` plugin for Claude Code provides three composing skills that guide you from use-case discovery to deployment.

## Key takeaways
- Agent skills encode design decisions (deployment model, tool patterns, auth) so Claude Code can scaffold a correctly architected server without you specifying every detail
- Three skills: `build-mcp-server` (entry point), `build-mcp-app` (adds interactive UI widgets), `build-mcpb` (packages server with runtime for zero-dependency distribution)
- Discovery phase before any code: the skill asks about what it connects to, who uses it, action surface size, user interaction needs, and upstream auth
- Four deployment paths: Remote Streamable HTTP (default for cloud APIs), MCP Apps (with interactive widgets), MCP Bundles (zero-install local servers), Local STDIO (prototyping)
- Install in Claude Code: `/plugin marketplace add anthropics/claude-plugins-official` → `/plugin install mcp-server-dev`

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Tools mentioned
- [[tools/claude-code]]
- [[tools/mcp-inspector]]

## Connections
The fastest path to building a production-ready MCP server when using Claude Code. The four deployment paths map to concrete use cases and are the key decision framework.
