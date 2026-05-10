---
title: Understanding Authorization in MCP
type: source
source_file: raw/Understanding Authorization in MCP.md
date_ingested: 2026-05-10
tags: [mcp, oauth, authorization, keycloak]
---

# Understanding Authorization in MCP

## Summary
Tutorial on implementing OAuth 2.1 authorization for MCP servers. Covers when authorization is needed, the full OAuth flow step-by-step, and a hands-on Keycloak implementation example for local testing.

## Key takeaways
- Authorization is **optional** for local STDIO servers (use env-based credentials instead) — but strongly recommended when accessing user-specific data, needing audit trails, or building for enterprise
- OAuth flows are designed for HTTP-based remote MCP servers; STDIO servers can use environment variables or embedded credentials
- Use cases requiring auth: user-specific data access, audit trails, rate limiting per user, enterprise access controls
- Keycloak setup: configure `mcp:tools` scope, set it as default with `Include in token scope`, add Audience mapper to embed the MCP server as token destination (critical to prevent token passthrough)
- Token audience validation: the audience embedded in the token ensures the MCP server can verify the token was issued specifically for it

## Concepts covered
- [[concepts/mcp-security]]
- [[concepts/model-context-protocol]]

## Connections
Practical companion to [[sources/mcp-security-best-practices]]. The Keycloak example is the fastest path to testing OAuth-protected MCP servers locally.
