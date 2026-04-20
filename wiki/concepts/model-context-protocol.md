---
title: Model Context Protocol (MCP)
type: concept
sources: [claude-101-connecting-tools]
last_updated: 2026-04-12
---

# Model Context Protocol (MCP)

## What it is
An open standard that defines how AI models connect to external tools, data sources, and applications. MCP is to AI integrations what USB-C is to hardware peripherals — one universal interface that works across devices and vendors. Created by Anthropic, but designed to be adopted broadly.

## Why it matters (for this domain)
MCP is the connectivity layer that turns Claude from a chat interface into an informed collaborator that can reach into your actual tools and data. For analytics engineers: MCP connectors to dbt, Snowflake, Notion, or your BI stack would let Claude reason over your real data environment. For business builders: MCP is the protocol you'd implement to make your product "Claude-connectable."

## How it works
MCP defines a client-server architecture:
- **MCP Server**: the tool/data source exposes a standardized interface (a set of callable functions and data resources)
- **MCP Client**: Claude connects to the server and discovers what functions are available
- Claude then calls those functions mid-conversation as needed

Two deployment modes:
- **Web connectors**: cloud services (Google Drive, Notion, Slack, Linear, Stripe, etc.) — runs over HTTPS
- **Desktop extensions**: local tools accessed via Claude Desktop app — runs locally on your machine

## Practical notes
- Permissions are scoped per connector — you see exactly what access you're granting.
- Claude sees only what YOU have access to. Connecting your Gmail doesn't expose colleagues' inboxes.
- Connections are revocable at any time via Claude settings or the third-party service's security settings.
- You can build custom MCP servers. This is how you'd connect Claude to an internal data warehouse, a proprietary API, or a custom analytics tool.
- Security: treat custom/third-party MCP servers like npm packages — only install from trusted sources, review what they expose.

## See also
- [[tools/mcp-connectors]]
- [[tools/claude-desktop]]
- [[concepts/agentic-ai]]

## Sources
- [[sources/claude-101-connecting-tools]] — explains MCP as the standard powering all Claude connectors, with setup instructions
