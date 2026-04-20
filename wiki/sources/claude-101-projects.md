---
title: "Claude 101: Introduction to Projects"
type: source
source_file: "raw/Introduction to projects.md"
date_ingested: 2026-04-12
tags: [claude, projects, rag, context-window, knowledge-base]
---

# Claude 101: Introduction to Projects

## Summary
Lesson from Anthropic Academy's Claude 101 course introducing Claude Projects — self-contained workspaces combining a knowledge base, custom instructions, and persistent chat history. Covers setup, knowledge base management, and how Claude automatically scales with RAG when context limits approach.

## Key takeaways
- Projects are isolated environments with their own memory, chat histories, knowledge bases, and instructions — think dedicated workspaces for specific work streams
- Project knowledge lets you upload documents once; Claude references them across every chat in the project without re-uploading
- Project instructions are a persistent system prompt — specify tone, expertise level, response style, constraints
- When knowledge base approaches context limits, Claude automatically activates RAG to expand capacity up to 10x
- Team/Enterprise plans can share projects across teammates — enabling collaborative AI workspaces

## Concepts covered
- [[concepts/rag]]
- [[concepts/context-window]]
- [[concepts/skills-vs-projects]]

## Tools mentioned
- [[tools/claude-projects]]
- [[tools/claude-ai]]

## Connections
Foundational to understanding Claude's organizational model. Every advanced use case (custom AI assistants, team knowledge bases, course delivery systems) builds on this pattern.
