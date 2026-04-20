---
title: AI Collaboration Modes
type: concept
sources: [ai-fluency-why]
last_updated: 2026-04-20
---

# AI Collaboration Modes

## What it is
A three-tier model describing the depth of human-AI collaboration on any given task. Introduced in the AI Fluency Framework by Dakan & Feller. The three modes are **Automation**, **Augmentation**, and **Agency**.

| Mode | Human role | AI role | Example |
|------|-----------|---------|---------|
| **Automation** | Gives instructions | Executes specific tasks | "Summarise this document" |
| **Augmentation** | Co-thinks with AI | Creative and execution partner | Drafting + iterating a strategy together |
| **Agency** | Configures AI upfront | Works independently on your behalf | Claude Code running a test suite; this wiki agent |

## Why it matters (for this domain)
The mode you choose determines how you architect the interaction — and what can go wrong. Automation is lowest risk, lowest leverage. Agency is highest leverage, highest risk. For AI product builders and course creators, understanding which mode a workflow uses determines what to teach and what guardrails to build.

## How it works
These modes are not a linear progression — you use all three constantly, often within the same session:
- You **automate** routine extraction tasks
- You **augment** your thinking on strategy or analysis
- You **configure for agency** when you want Claude to run a multi-step process unattended

The key decision variable is *how much context and judgment* you want to delegate. Automation delegates execution. Augmentation delegates a thinking partner role. Agency delegates the judgment loop itself.

## Practical notes
- **Agency requires upfront investment** — you must give the AI enough context, constraints, and stopping conditions that it can operate without asking you every step. CLAUDE.md in this repo is an example of this investment.
- **Augmentation is the most underused mode** — people jump between asking questions (Automation) and setting up automations (Agency), missing the high-leverage creative collaboration in the middle.
- **Mode mismatch is a common failure** — using Automation framing (transactional prompts) for a task that needs Augmentation (iterative co-thinking) produces frustrating results.

## See also
- [[concepts/ai-fluency]]
- [[concepts/4d-framework]]
- [[concepts/agentic-ai]] — the technical architecture that enables Agency mode
- [[concepts/prompt-engineering]] — essential for Automation and Augmentation

## Sources
- [[sources/ai-fluency-why]] — primary source introducing the three-mode model
