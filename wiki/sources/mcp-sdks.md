---
title: MCP SDKs
type: source
source_file: raw/SDKs.md
date_ingested: 2026-05-10
tags: [mcp, sdk, python, typescript]
---

# MCP SDKs

## Summary
Official SDK directory for MCP. Lists all supported languages with tier classification (Tier 1 = full feature support + maintenance commitment, Tier 3 = community-maintained).

## Key takeaways
- Tier 1 SDKs (full support): TypeScript, Python, C#, Go
- Tier 2 SDKs: Java, Rust
- Tier 3 SDKs (community): Swift, Ruby, PHP; Kotlin is TBD
- All SDKs support: servers that expose tools/resources/prompts, clients that connect to any MCP server, local and remote transport, protocol compliance with type safety
- For data engineering work: Python SDK (Tier 1) is the natural choice — `pip install mcp` or `uv add "mcp[cli]"`

## Concepts covered
- [[concepts/model-context-protocol]]

## Connections
Choose Python (Tier 1) for data engineering use cases. TypeScript if building web-based MCP applications.
