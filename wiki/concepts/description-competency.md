---
title: Description Competency
type: concept
sources: [ai-fluency-description, ai-fluency-prompting, ai-fluency-4d-framework-lesson]
last_updated: 2026-05-10
---

# Description Competency

## What it is
The second 4D competency. Description is the skill of communicating effectively with AI systems — not just writing prompts, but creating a collaborative environment where both parties can work effectively together. AI cannot read your mind; quality of results directly reflects quality of communication.

## Why it matters (for this domain)
A vague prompt asking Claude to "migrate this table to EOS" will produce a generic guess. A well-described prompt specifying the source GAIA structure, the target EOS YAML conventions, the dependency constraints, and the expected output format produces a usable first draft. The gap between these two outcomes is entirely determined by Description quality.

## How it works
Three sub-components:

| Sub-component | What it defines |
|--------------|----------------|
| **Product Description** | What you want — output format, audience, style, scope |
| **Process Description** | How to approach it — reasoning steps, constraints, what to avoid |
| **Performance Description** | How the AI should behave — verbosity, tone, when to ask vs. assume |

Description and [[concepts/discernment-competency]] form a **continuous feedback loop**: describe → receive → evaluate → re-describe.

## Practical notes
- **Most neglected sub-component:** Process Description. Telling Claude *what* you want is obvious; telling it *how to reason through it* is the upgrade most people skip.
- **For Trino SQL prompts:** Product = the query structure and output schema. Process = join order, filter-before-aggregate, handling NULLs. Performance = show the SQL only, no explanation unless asked.
- **For EOS migration:** Product = valid EOS YAML. Process = follow naming convention X, preserve test coverage, flag unclear dependencies. Performance = flag ambiguities rather than guessing.
- **Secret weapon:** Ask Claude to critique your own prompt before you run it.

## See also
- [[concepts/4d-framework]]
- [[concepts/prompt-engineering]]
- [[concepts/prompting-techniques]] — the six tactical techniques for Product/Process/Performance
- [[concepts/discernment-competency]] — the feedback loop partner

## Sources
- [[sources/ai-fluency-description]] — three sub-components framework
- [[sources/ai-fluency-prompting]] — six practical techniques
- [[sources/ai-fluency-4d-framework-lesson]] — Description in context of the full 4D framework
