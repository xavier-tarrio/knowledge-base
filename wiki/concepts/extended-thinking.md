---
title: Extended Thinking
type: concept
sources: [claude-101-research-mode]
last_updated: 2026-04-12
---

# Extended Thinking

## What it is
A Claude capability that gives the model additional compute time to reason through a problem before producing a final response. The model generates an internal chain of thought — breaking the problem into sub-problems, working through them systematically — before writing its answer. This "scratchpad" is separate from the visible response.

## Why it matters (for this domain)
Complex analytics problems (e.g. debugging a multi-join dbt model, designing a metric tree, evaluating architectural trade-offs) benefit from extended thinking because the answer emerges from reasoning, not retrieval. It's also automatically combined with Research mode, meaning Claude both plans its investigation AND gathers information — a qualitatively different level of output than standard chat.

## How it works
Extended thinking is computationally more expensive — it consumes more tokens because the model generates a full reasoning trace before the answer. In practice:
- Claude decomposes the question into parts
- Works through each part, potentially revising earlier conclusions
- Produces a final answer informed by the full reasoning chain

The user does not see the raw scratchpad (unless Claude Code's chain-of-thought display is enabled), but the answer quality reflects it.

## Practical notes
- **Not always better.** For simple, factual, or creative tasks, extended thinking adds latency without meaningful quality improvement. Use it for genuinely hard reasoning problems.
- **Always on in Research mode** — you get both multi-source retrieval AND deep reasoning in a single pass.
- **Separate from Research.** Use extended thinking alone when you need deep reasoning on a problem that doesn't require external information (code debugging, mathematical analysis, logical planning).
- **Context window cost.** The reasoning trace consumes context. On very long inputs, this can be a constraint.

## See also
- [[concepts/agentic-ai]]
- [[tools/claude-research]]

## Sources
- [[sources/claude-101-research-mode]] — explains when to use extended thinking vs Research vs web search vs enterprise search
