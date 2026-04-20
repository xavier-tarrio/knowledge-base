---
title: Claude Desktop App
type: tool
sources: [claude-101-desktop-modes, claude-101-other-ways, claude-101-connecting-tools]
last_updated: 2026-04-12
---

# Claude Desktop App

## What it does
The native macOS/Windows application for Claude. Required for desktop extensions (local MCP). Offers three distinct interaction modes within a single app: **Chat** (conversational), **Cowork** (complex multi-step task execution), and **Code** (software development). Also enables mobile task dispatch via Dispatch.

## The three modes

### Chat
Standard conversational interface — same as claude.ai. Best for: questions, writing, analysis, back-and-forth dialogue. No special setup.

### Cowork
Claude's multi-step task execution mode. Handles: research briefs, document creation (Excel, Word, PowerPoint, PDF), file organization, multi-step data analysis. Works with Skills and connected tools. Best for: complex outputs that require multiple steps you'd otherwise orchestrate manually.

### Code
Software development mode — equivalent to Claude Code but through the desktop GUI. Best for: users who prefer a UI over terminal, or who want Claude Code integrated with their visual workflow.

## When to use Desktop over claude.ai web
- You need **desktop extensions** (local file access, browser control, native app integration) — these require the Desktop app
- You prefer a **native app experience** with offline capability
- You're using **Cowork** for complex multi-step document workflows
- You want Claude Code integrated in a visual environment rather than CLI

## Desktop extensions
Local MCP servers that run on your machine. Enable:
- Local file system access
- Browser automation and control
- Native application integration (Figma, etc.)
To install: Settings → Extensions → Browse and Install

## Key concepts to understand
- [[concepts/model-context-protocol]] — desktop extensions are local MCP servers
- [[concepts/agentic-ai]] — Cowork mode is agentic task execution

## Sources
- [[sources/claude-101-desktop-modes]] — three-mode overview and when to use each
- [[sources/claude-101-other-ways]] — summary table of all Claude surfaces including Desktop
- [[sources/claude-101-connecting-tools]] — desktop extensions as a connector type
