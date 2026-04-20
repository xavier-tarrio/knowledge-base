---
title: Claude Skills
type: tool
sources: [claude-101-skills]
last_updated: 2026-04-12
---

# Claude Skills

## What it does
Skills are instruction packages — folders of instructions, scripts, and resources — that Claude loads dynamically to execute specialized tasks in a defined, repeatable way. Think of them as procedural expertise: they teach Claude *how* to run a specific workflow, not just what to know. Claude invokes relevant skills automatically based on the task.

## When to use it
- **Repeatable document creation**: Excel models, PowerPoint decks, Word docs, PDFs — built-in Anthropic skills handle these
- **Recurring workflows**: any multi-step process you run regularly (quarterly variance analysis, brand voice reviews, client call prep, code review checklists)
- **Consistent methodology**: when you need Claude to follow the same steps every time, in the same order
- **Custom processes**: encoding your team's specific way of doing things — not just "make a chart" but "make a chart in our format with these specific elements"

## When NOT to use it
- One-time tasks — don't build a skill for something you'll do once
- Knowledge storage — use a Project for that
- If you're on the free plan — Skills require paid plans (Pro, Max, Team, Enterprise)

## Types of skills
| Type | Created by | Available to | Auto-invoked? |
|------|-----------|-------------|---------------|
| Anthropic built-in | Anthropic | All paid users | Yes |
| Custom personal | You, via conversation | Your account only | Yes |
| Custom org (Enterprise) | Org admin | All org members | Yes |

## Creating a custom skill
You don't write code — you describe it to Claude:
1. Tell Claude what workflow you want to encode
2. Claude interviews you about steps, criteria, examples
3. Upload reference materials (templates, style guides, examples)
4. Claude generates the skill file — save it, and it's ready

Skills can be iterated: ask Claude to edit a skill, it updates the files.

## Key concepts to understand
- [[concepts/skills-vs-projects]] — the foundational mental model for when to use each
- [[concepts/agentic-ai]] — skills are a form of procedural agentic behavior

## Sources
- [[sources/claude-101-skills]] — complete overview including creation workflow, types, and comparison with Projects
