---
title: Prompting Techniques
type: concept
sources: [ai-fluency-prompting, ai-fluency-description]
last_updated: 2026-05-10
---

# Prompting Techniques

## What it is
The six foundational techniques for crafting effective prompts — the tactical implementation of the [[concepts/description-competency]]. Prompt engineering combines familiar human communication principles with AI-specific considerations; it is iterative, not a one-shot skill.

## Why it matters (for this domain)
For a data engineer at Revolut, prompting is the interface to a highly capable coding and reasoning partner. The difference between a mediocre and an excellent Trino SQL generation is almost entirely in how the task was described. These six techniques are the repeatable levers.

## How it works

| Technique | What it does | Example for data work |
|-----------|-------------|----------------------|
| **Give context** | Explain what, why, and relevant background | "This is a Trino SQL query on a Revolut EOS dataset. The table has these columns: ..." |
| **Show examples** | Demonstrate the desired output format | Paste a working GAIA query and say "produce the EOS equivalent in this style" |
| **Specify constraints** | Define format, length, what to exclude | "Return only the SQL. No explanation. Use CTEs, not subqueries." |
| **Break into steps** | Guide multi-step reasoning explicitly | "First identify the joins, then the filters, then the aggregations" |
| **Ask AI to think first** | Give space for reasoning before output | "Think through the edge cases before writing the query" |
| **Define role/tone** | Set the collaboration mode | "Act as a senior analytics engineer reviewing this for correctness" |

**Secret weapon:** Ask Claude to critique and improve your own prompt before running it. This surfaces missing context you didn't know was missing.

## Practical notes
- **Most underused technique for data work:** Show examples. Pasting an existing working query and asking for the equivalent eliminates 80% of format and style mismatch.
- **Iteration is expected.** First prompt is a starting point, not a final answer. The loop is: prompt → evaluate (Discernment) → refine (Description) → repeat.
- **Constraints prevent scope creep.** Unconstrained prompts produce verbose, padded outputs. In data work, be explicit: "SQL only", "YAML only", "list the issues, don't fix them".

## See also
- [[concepts/description-competency]] — the framework these techniques implement
- [[concepts/prompt-engineering]] — broader context and the three-part structure
- [[concepts/discernment-competency]] — the evaluation side of the iteration loop

## Sources
- [[sources/ai-fluency-prompting]] — the six techniques and troubleshooting strategies
- [[sources/ai-fluency-description]] — the Product/Process/Performance framework these techniques serve
