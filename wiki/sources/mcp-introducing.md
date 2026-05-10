---
title: Introducing MCP (Anthropic Academy)
type: source
source_file: raw/Introducing MCP.md
date_ingested: 2026-05-10
tags: [mcp, anthropic-academy, integration]
---

# Introducing MCP (Anthropic Academy)

## Summary
Anthropic Academy's lesson on the problem MCP solves. Uses the GitHub integration example to demonstrate the integration tax: without MCP, every service integration requires authoring, testing, and maintaining all tool schemas yourself. With MCP, the server provider ships those schemas pre-built.

## Key takeaways
- Without MCP: building a GitHub-connected chat interface requires implementing hundreds of tool schemas for repos, PRs, issues, projects, etc.
- MCP shifts the tool definition burden from your server to dedicated MCP servers — the server provider does the hard work, you just connect
- Key distinction: MCP servers provide tool schemas + execution; tool use is how Claude *calls* those tools — they are complementary, not the same
- Anyone can create an MCP server; service providers often publish official implementations (e.g. AWS releasing an official MCP server for their services)
- Result: instead of maintaining complex custom integrations, you leverage community/official MCP servers

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/mcp-primitives]]

## Connections
Explains the "why" behind MCP more clearly than the spec docs. The GitHub example is the most useful illustration of integration tax reduction.
