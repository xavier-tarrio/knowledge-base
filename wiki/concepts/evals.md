---
title: Evals (AI Evaluations)
type: concept
sources: [claude-101-better-results]
last_updated: 2026-04-12
---

# Evals (AI Evaluations)

## What it is
Systematic testing of an AI model's performance on specific, real tasks relevant to your workflow. Not abstract benchmarks — evals are about whether Claude performs well on *your* emails, *your* data analysis, *your* code patterns. A lightweight eval is 5–10 examples with defined success criteria.

## Why it matters (for this domain)
Generic Claude benchmarks tell you nothing about whether Claude will write good dbt models in your specific stack or produce clean SQL for your warehouse's dialect. Evals are how you convert vague impressions ("Claude seems pretty good at this") into structured confidence ("Claude gets the right answer 8/10 times on this task type, and fails specifically when X"). For course builders: teaching evals is teaching professional AI integration methodology.

## How it works

**Simple eval workflow:**
1. **Gather examples** — 5–10 instances of a task you do regularly (emails you've written, analyses you've run)
2. **Write test prompts** — prompts that would produce similar outputs, with the natural context you'd have
3. **Run and compare** — does Claude capture the key information? Is tone/style right? What's missing?
4. **Refine and categorize** — adjust prompts, identify where human review is always needed, build intuition for where Claude excels

**What to look for in output comparison:**
- Correct information vs. plausible-but-wrong information
- Appropriate tone and format
- Coverage of what matters (recall) vs. irrelevant additions (precision)
- Consistency across similar inputs

## Practical notes
- You don't need infrastructure for basic evals — a spreadsheet with inputs, outputs, and pass/fail notes is sufficient to start.
- Evals are how you discover the failure modes specific to your domain. Claude might be excellent at executive summaries but poor at technical runbooks for your specific tooling.
- **The output of an eval is a better prompt, not just a score.** The goal is to learn what context to add, what examples to provide, and which tasks need human review.
- As you build more automations (agents, pipelines), evals become a testing framework — you cannot ship an AI workflow without knowing its failure rate on your actual data.

## See also
- [[concepts/prompt-engineering]]
- [[concepts/agentic-ai]]

## Sources
- [[sources/claude-101-better-results]] — practical 4-step eval approach with a data analysis example
