---
title: Skills vs. Projects (Claude's Knowledge/Process Duality)
type: concept
sources: [claude-101-skills, claude-101-projects]
last_updated: 2026-04-12
---

# Skills vs. Projects (Claude's Knowledge/Process Duality)

## What it is
A core mental model for organizing work with Claude. **Projects store knowledge. Skills execute processes.** They are complementary, not competing — a skill can pull from knowledge stored in a project.

| Dimension | Projects | Skills |
|-----------|----------|--------|
| Purpose | Store what Claude needs to KNOW | Define how Claude should DO a task |
| Contains | Uploaded documents, reference material, instructions | Step-by-step methodology, brand guidelines, process workflows |
| Best for | Long-term context, reference material, team collaboration | Repeatable workflows, multi-step tasks, consistent methodology |
| Activated | Available across all chats in the project | Invoked automatically when task is relevant |
| Example | Customer hub with CRM exports, contracts, meeting notes | Quarterly variance analysis process, brand voice review |

## Why it matters (for this domain)
This duality maps cleanly onto analytics engineering work:
- **Projects** = your data warehouse context (schema docs, metric definitions, dbt model docs, team conventions)
- **Skills** = your recurring processes (code review checklist, dashboard design methodology, stakeholder update format)

For business builders: this is also how you design Claude-powered products. The knowledge layer (what your product knows) and the process layer (what your product does) should be architected separately.

## How it works
- **Projects** are workspaces that hold uploaded files + written instructions. Claude references them passively across all conversations in the project.
- **Skills** are instruction packages (YAML/markdown files with metadata) that Claude loads dynamically when a task matches. They can include scripts and templates.
- Skills are created by describing a workflow to Claude in conversation — Claude structures it into a proper skill file for you.
- Combination: a "client call prep" skill can pull from a project that contains client profiles, deal history, and account notes.

## Practical notes
- Don't try to put processes into project instructions — they'll be inconsistently followed. Use a Skill for anything with a defined sequence of steps.
- Don't create Skills for one-off tasks — they're for *repeatable* workflows.
- When a workflow changes, update the Skill. This keeps process knowledge version-controlled and separate from reference knowledge.
- Custom Skills are private to your account. Enterprise Skills can be shared org-wide.

## See also
- [[tools/claude-projects]]
- [[tools/claude-skills]]

## Sources
- [[sources/claude-101-skills]] — the definitive comparison table and use-case framing
- [[sources/claude-101-projects]] — explains project knowledge bases and RAG scaling
