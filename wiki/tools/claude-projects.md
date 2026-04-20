---
title: Claude Projects
type: tool
sources: [claude-101-projects]
last_updated: 2026-04-12
---

# Claude Projects

## What it does
A persistent workspace feature in Claude.ai that combines three elements: a **knowledge base** (uploaded documents), **custom instructions** (a persistent system prompt), and **shared chat history**. Every conversation within a project inherits the knowledge base and instructions — you never re-upload the same context. When knowledge bases approach context limits, Claude automatically activates RAG to expand capacity up to 10x.

## When to use it
- **Recurring work streams** that need the same reference material every session (client accounts, ongoing projects, research areas)
- **Team collaboration** (Team/Enterprise plans) — shared knowledge base and instructions for a working group
- **Domain specialization** — configure Claude as a specific expert (e.g. "you are an analytics engineer familiar with our dbt project and BigQuery conventions")
- **Course building** — a project per course, with curriculum docs and style guide as the knowledge base

## When NOT to use it
- One-off tasks that don't repeat — standard chat is simpler
- Process-oriented tasks with defined steps — use a [[tools/claude-skills|Skill]] instead
- When you need Claude to search the live web — Projects don't automatically include web search (enable it separately)

## Key components

### Knowledge base
Upload PDFs, markdown, code files, CSVs. Claude references them in every conversation in the project. Files are indexed; RAG activates automatically near context limits.

### Project instructions
A persistent system prompt scoped to the project. Set: persona, expertise level, tone, response format, constraints. Applied to every chat in the project.

### Chat history
All conversations within a project are retained and visible together. Different from standard chats which are isolated.

## Practical notes
- Instructions > knowledge base > conversation history in Claude's attention hierarchy. Keep instructions tight and precise.
- For large knowledge bases (e.g. uploading an entire dbt project's docs), expect RAG to activate — retrieval quality depends on how well your query matches stored content.
- Projects are not Agents. They don't act autonomously — they're a persistent context environment.

## Key concepts to understand
- [[concepts/rag]] — the scaling mechanism that makes large knowledge bases viable
- [[concepts/context-window]] — what Projects extend
- [[concepts/skills-vs-projects]] — when to use each

## Sources
- [[sources/claude-101-projects]] — full feature walkthrough with learning objectives and key takeaways
