---
title: Claude Code
type: tool
sources: [claude-101-other-ways]
last_updated: 2026-04-12
---

# Claude Code

## What it does
An agentic coding tool that runs in your terminal, IDE, browser, or Slack. Claude Code reads and understands your entire codebase, not just the file you paste in. It can execute commands, run tests, write code, create commits, and manage full development workflows through natural language instructions. It operates in an agentic loop — write, run, observe output, fix, repeat — without you directing each step.

## When to use it
- **Building features**: describe what you need; Claude writes the code, runs tests, and creates commits
- **Debugging**: paste an error or describe the problem; Claude reads your codebase to trace root cause and fix
- **Codebase navigation**: "how does the auth middleware work?" across an unfamiliar or large codebase
- **Dev automation**: fixing lint errors, resolving merge conflicts, writing release notes, scaffolding boilerplate
- **Analytics engineering**: generating dbt models, writing complex SQL, documenting schemas, running dbt tests
- **Preferred**: when you want to stay in your terminal/IDE workflow rather than switching to a browser

## When NOT to use it
- Simple one-shot code questions — standard Claude.ai chat is faster and cheaper
- Non-code tasks — use Claude.ai instead
- When you need to review each change carefully before execution — Claude Code is autonomous; set up checkpoints for high-stakes operations (e.g. migrations, destructive changes)

## How it differs from Claude.ai
| Dimension | Claude.ai | Claude Code |
|-----------|-----------|-------------|
| Interface | Browser/app | Terminal / IDE |
| Codebase awareness | File-at-a-time (you paste) | Full repo context |
| Execution | No | Yes (runs commands, tests) |
| Git integration | No | Yes (commits, branches) |
| Autonomy | Responds per message | Agentic loop until goal met |

## Key concepts to understand
- [[concepts/agentic-ai]] — Claude Code is the most mature agentic surface Anthropic offers
- [[concepts/context-window]] — large repos may exceed context; Claude Code handles this with repo-level indexing
- [[concepts/prompt-engineering]] — how you describe a task to Claude Code determines solution quality

## Sources
- [[sources/claude-101-other-ways]] — positions Claude Code vs. other Claude surfaces, primary use cases
