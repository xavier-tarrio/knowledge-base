---
title: "Claude 101: Connecting Your Tools"
type: source
source_file: "raw/Connecting your tools.md"
date_ingested: 2026-04-12
tags: [claude, mcp, connectors, integrations, tools, security]
---

# Claude 101: Connecting Your Tools

## Summary
Lesson on Claude's connector system — how to give Claude access to your actual tools and data through the Model Context Protocol. Covers the connector directory, setup for web connectors and desktop extensions, practical use cases across major tool categories, and security considerations.

## Key takeaways
- Connectors transform Claude from an assistant into an informed collaborator — instead of pasting context, Claude reads your live data
- MCP (Model Context Protocol) is the open standard powering connectors — "USB-C for AI" — enables any tool to expose a standardized interface to Claude
- Two connector types: **web connectors** (cloud services: Google Drive, Notion, Slack, Asana, Linear, Stripe) and **desktop extensions** (local tools via Claude Desktop)
- Claude can read AND act — depending on permissions, it can search, retrieve, create, update, and execute tasks across connected apps
- Security model: scoped permissions, you-only access (Claude sees what you see), revocable at any time, custom connectors can be built for internal tools

## Concepts covered
- [[concepts/model-context-protocol]]
- [[concepts/agentic-ai]]

## Tools mentioned
- [[tools/mcp-connectors]]
- [[tools/claude-desktop]]

## Connections
Connectors are what make Research mode powerful (combine web + your integrations in one pass) and what enable Claude Code to interact with external services. The MCP standard is also the architecture pattern for building Claude-connectable products.
