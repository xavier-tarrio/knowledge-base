---
title: Agentic AI
type: concept
sources: [claude-101-research-mode, claude-101-other-ways, claude-101-connecting-tools, ai-fluency-why]
last_updated: 2026-04-20
---

# Agentic AI

## What it is
AI behavior where the model operates autonomously across multiple steps — planning, acting, observing results, and deciding what to do next — without a human directing each individual step. Contrasted with "chat" behavior where every model output is a direct response to a user turn.

## Why it matters (for this domain)
Agentic AI is the architectural shift that makes AI actually useful for complex professional work. Chat AI assists. Agentic AI executes. For analytics engineers: an agent that can write dbt models, run tests, inspect failures, fix them, and open a PR is categorically more powerful than a chatbot that suggests code. Understanding the agentic paradigm is essential for building serious AI products.

## How it works
An agentic loop typically has four phases:
1. **Plan** — the model breaks down the goal into sub-tasks
2. **Act** — the model calls a tool (runs code, searches the web, queries a database, writes a file)
3. **Observe** — the model reads the tool's output
4. **Decide** — continue, adjust, or complete based on what it found

This loop repeats until the goal is reached or an ambiguity requires human input. The agent is not responding to you — it's pursuing an objective.

## Practical notes
- Agentic behavior requires **tools** — without tool access, the model can only plan and reason, not act.
- The loop can fail in unexpected ways. Good agent design includes: clear goal definition, explicit stopping conditions, and human checkpoints for irreversible actions (file deletion, API writes, etc.).
- Claude Code is a fully agentic coding assistant — it can read your codebase, write code, run tests, see errors, fix them, and commit. This is the most mature agentic surface Anthropic offers as of 2026.
- Research mode is agentic search — multiple iterative web queries that build on each other, with extended thinking to plan the approach.
- The boundary between "chat with tools" and "agent" is fuzzy — think of it as a spectrum of autonomy.

## See also
- [[tools/claude-code]]
- [[tools/claude-research]]
- [[concepts/extended-thinking]]
- [[concepts/model-context-protocol]]
- [[concepts/ai-collaboration-modes]] — "Agency mode" in the AI Fluency framework is the human-facing framing of agentic AI

## Sources
- [[sources/claude-101-research-mode]] — shows agentic behavior in search: iterative queries, automatic lead-following
- [[sources/claude-101-other-ways]] — Claude Code as the primary agentic coding surface
- [[sources/ai-fluency-why]] — frames agentic AI as "Agency mode" in the three-tier collaboration model
