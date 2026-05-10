---
title: MCP Security Best Practices
type: source
source_file: raw/Security Best Practices.md
date_ingested: 2026-05-10
tags: [mcp, security, oauth, prompt-injection, ssrf]
---

# MCP Security Best Practices

## Summary
Official security guide from modelcontextprotocol.io covering all major attack vectors specific to MCP implementations. Companion to the MCP Authorization spec. Targets developers building MCP servers, server operators, and security professionals evaluating MCP systems.

## Key takeaways
- **Confused Deputy**: MCP proxy servers using static OAuth client IDs must implement per-client consent storage server-side before any third-party OAuth flow — stored consent cookies alone are not sufficient
- **Token Passthrough explicitly forbidden**: MCP servers MUST NOT accept tokens not issued specifically for them; validate the `aud` (audience) claim on every token
- **SSRF via OAuth discovery**: malicious servers can return URLs pointing to cloud metadata endpoints (`169.254.169.254`) or internal services; block private IP ranges and enforce HTTPS
- **Session Hijacking**: bind session IDs to `user_id:session_id` format; never use sessions for authentication; use cryptographically secure random IDs
- **Scope Minimization**: start with minimal scopes (`mcp:tools-basic`), elevate incrementally; never use wildcards or omnibus scopes
- All mitigations include specific technical implementations (code-level patterns, cookie attributes, redirect URI validation rules)

## Concepts covered
- [[concepts/mcp-security]]
- [[concepts/model-context-protocol]]

## Connections
The most detailed security source. Pairs with [[sources/mcp-authorization]] for the full OAuth 2.1 implementation picture. Reference before deploying any remote MCP server handling user data.
