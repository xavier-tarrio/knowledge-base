---
title: Discernment Competency
type: concept
sources: [ai-fluency-discernment, ai-fluency-4d-framework-lesson]
last_updated: 2026-05-10
---

# Discernment Competency

## What it is
The third 4D competency. Discernment is the skill of thoughtfully evaluating AI outputs, reasoning processes, and collaboration behavior. It is the mirror of Description — while Description shapes what you ask for, Discernment evaluates what you receive. Together they form a continuous feedback loop.

## Why it matters (for this domain)
In regulatory reporting, Claude's output going into production without Discernment is a compliance risk. A hallucinated join condition or a misunderstood business rule will produce wrong numbers in a reg report — and wrong numbers in reg reports have legal consequences. Discernment is not optional in this context; it's what makes AI use responsible.

## How it works
Three sub-components:

| Sub-component | What it evaluates |
|--------------|------------------|
| **Product Discernment** | Output quality — accuracy, appropriateness, coherence, relevance |
| **Process Discernment** | Reasoning quality — logical errors, attention gaps, inappropriate shortcuts |
| **Performance Discernment** | Collaboration quality — did the AI behave as instructed? Was the communication style appropriate? |

**Key insight:** Domain expertise amplifies Discernment. You can only catch errors in areas you know. This is why Delegation requires expertise first — so you can actually evaluate what AI produces.

## Practical notes
- **Process Discernment is the underused one.** Most people check outputs (Product) but not reasoning. For complex SQL or YAML migration, inspect *how* Claude got there — wrong reasoning that produces right output today will fail on edge cases.
- **For Trino SQL:** Check join conditions, NULL handling, aggregation scope, and filter order — common Claude errors in SQL generation.
- **For EOS YAML:** Check dependency declarations, test coverage completeness, naming convention adherence.
- **Systematic Discernment = [[concepts/evals]].** When you need Discernment at scale or repeatably, formalise it.

## See also
- [[concepts/4d-framework]]
- [[concepts/description-competency]] — the feedback loop partner
- [[concepts/evals]] — operationalising Discernment systematically
- [[concepts/generative-ai]] — understanding hallucinations grounds Product Discernment

## Sources
- [[sources/ai-fluency-discernment]] — three sub-components and the Description↔Discernment loop
- [[sources/ai-fluency-4d-framework-lesson]] — Discernment in context of the full framework
