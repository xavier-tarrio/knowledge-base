---
title: MCP Connectors
type: tool
sources: [claude-101-connecting-tools]
last_updated: 2026-04-12
---

# MCP Connectors

## What it does
Connectors give Claude access to external tools and data sources through the Model Context Protocol standard. Once connected, Claude can read from — and in some cases write to — your tools directly within a conversation. Two types: **web connectors** (cloud services) and **desktop extensions** (local tools via Claude Desktop).

## When to use it
- When you're repeatedly copying and pasting data from a tool into Claude — a connector eliminates that
- When Claude needs live data to answer a question (current Stripe revenue, today's Asana tasks, last week's Slack decisions)
- When you want Claude to take actions in your tools (create tasks, draft replies, update records)
- For Research mode: connected integrations let Claude combine web research with your actual org data

## When NOT to use it
- When data security is a concern and you're not certain of the connector's permission scope — review carefully before connecting
- For sensitive systems (financial, legal, HR data) — evaluate the minimum permissions needed
- Don't connect tools you don't use regularly — connector sprawl creates unnecessary access surface

## Available connector categories (examples)
| Category | Examples |
|----------|---------|
| Project management | Asana, Linear, Jira |
| Communication | Slack, Gmail |
| Documentation | Notion, Google Drive, Confluence |
| Business tools | Stripe, PayPal, Salesforce |
| Dev tools | GitHub (via desktop extensions) |

## Security model
- **Scoped permissions**: you see exactly what access each connector requests; individual permissions can be toggled
- **You-scoped only**: Claude can only see data YOU have access to. Connecting Gmail doesn't expose anyone else's inbox.
- **Revocable**: disconnect via Claude settings or the third-party service's security settings at any time
- **Custom connectors**: you can build your own MCP server to connect any internal tool

## Key concepts to understand
- [[concepts/model-context-protocol]] — the standard that powers all connectors
- [[concepts/agentic-ai]] — connectors enable Claude to act, not just respond

## Sources
- [[sources/claude-101-connecting-tools]] — connector directory walkthrough, setup steps, practical use cases, security considerations
