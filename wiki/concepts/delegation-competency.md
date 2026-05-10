---
title: Delegation Competency
type: concept
sources: [ai-fluency-delegation, ai-fluency-4d-framework-lesson]
last_updated: 2026-05-10
---

# Delegation Competency

## What it is
The first of the 4D competencies. Delegation is the skill of deciding what work to do yourself, what to do together with AI, and what to let AI handle independently. It requires both domain expertise and understanding of AI capabilities — you cannot delegate what you don't understand.

## Why it matters (for this domain)
At Revolut, regulatory reporting is high-stakes. Delegation decisions directly determine risk. SQL generation for well-defined transformations = safe to delegate. Business logic decisions in GAIA→EOS migration = stay with the human. Getting this boundary wrong in either direction is costly: over-delegation risks incorrect outputs in reg reports; under-delegation leaves productivity on the table.

## How it works
Three sub-components:

| Sub-component | Question it answers |
|--------------|-------------------|
| **Problem Awareness** | Do I clearly understand my goal and the work involved? |
| **Platform Awareness** | What can this specific AI system actually do well vs. poorly? |
| **Task Delegation** | Which specific tasks go to AI, which stay with me, which are collaborative? |

Delegation is not a one-time decision — it's re-evaluated as you learn more about both the problem and the platform.

## Practical notes
- **Delegation requires expertise first.** If you don't know what good output looks like, you can't delegate safely. This is why Discernment and Delegation are coupled.
- **For Trino SQL:** Delegate boilerplate joins, aggregations, and schema-following transformations. Retain business rule interpretation and output validation.
- **For EOS YAML migration:** Delegate structural reformatting and dependency mapping. Retain dataset naming decisions, test coverage choices, and sign-off.
- **Platform Awareness in practice:** Claude Code has full file context; claude.ai chat has a session context only. Same model, different delegation profiles.

## See also
- [[concepts/4d-framework]]
- [[concepts/ai-collaboration-modes]] — modes shape what delegation looks like
- [[concepts/discernment-competency]] — evaluation is delegation's necessary partner
- [[concepts/generative-ai]] — knowing capabilities informs Platform Awareness

## Sources
- [[sources/ai-fluency-delegation]] — three sub-components in detail
- [[sources/ai-fluency-4d-framework-lesson]] — Delegation in context of the full framework
