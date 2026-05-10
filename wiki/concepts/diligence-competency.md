---
title: Diligence Competency
type: concept
sources: [ai-fluency-diligence, ai-fluency-4d-framework-lesson]
last_updated: 2026-05-10
---

# Diligence Competency

## What it is
The fourth 4D competency. Diligence addresses the ethical and safety dimensions of AI collaboration — while the other three competencies focus on effectiveness and efficiency, Diligence ensures that effectiveness doesn't come at the cost of responsibility.

## Why it matters (for this domain)
Regulatory reporting at Revolut is a legally accountable activity. "The AI generated it" is not a defence when a reg report is wrong. Diligence makes explicit: you own the output. This shapes how AI is used — AI as a drafting and validation tool, human as the accountable signatory.

## How it works
Three sub-components:

| Sub-component | What it covers |
|--------------|---------------|
| **Creation Diligence** | Which AI system to use, what data to share, privacy/security considerations |
| **Transparency Diligence** | Being open about AI's role with everyone who needs to know |
| **Deployment Diligence** | Taking full responsibility for verifying and owning AI-assisted outputs |

**Context matters:** Disclosure expectations differ between personal, academic, and professional contexts. In a regulated financial institution, assume maximum scrutiny.

**Diligence Statement:** A formal declaration of AI's role in a piece of work and the author's responsibility for its accuracy. Worth creating for any AI-assisted work that goes to stakeholders.

## Practical notes
- **At Revolut:** Never send AI-generated SQL or YAML to production without human review and explicit sign-off. Creation Diligence = don't share confidential customer data with external AI APIs. Transparency Diligence = if your manager asks "did you write this?" — answer accurately.
- **Data sensitivity:** Revolut's internal data (transaction records, regulatory filings) should not be pasted into external AI tools. Use Claude Code on local files or approved internal tools only.
- **Creation Diligence includes tool choice.** Claude Code operating on local files is different from pasting data into claude.ai chat. Choose accordingly.

## See also
- [[concepts/4d-framework]]
- [[concepts/evals]] — Deployment Diligence operationalised at scale
- [[concepts/discernment-competency]] — Discernment is the technical mechanism; Diligence is the accountability wrapper

## Sources
- [[sources/ai-fluency-diligence]] — three sub-components and Diligence Statements
- [[sources/ai-fluency-4d-framework-lesson]] — Diligence in context of the full framework
