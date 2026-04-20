---
title: Prompt Engineering
type: concept
sources: [claude-101-first-conversation, claude-101-better-results, ai-fluency-intro]
last_updated: 2026-04-20
---

# Prompt Engineering

## What it is
The practice of designing inputs to an LLM to get reliably useful outputs. Not a fixed skill set — it evolves as models evolve — but the core principle remains: the model can only work with what you give it. Better inputs produce better outputs, and the relationship is learnable.

## Why it matters (for this domain)
For analytics engineers, prompt engineering determines the gap between "Claude writes code that sort of works" and "Claude writes production-quality dbt models that pass your team's style guide." For course builders: teaching prompt engineering is teaching people how to think about communicating with AI — the highest-leverage skill for any Claude user.

## How it works

### The three-part prompt structure (Anthropic's framework)
1. **Set the stage** — context: who you are, what you're working on, who the output is for
2. **Define the task** — what you actually want: write, analyze, compare, debug, etc.
3. **Specify rules** — constraints: format, tone, length, what to include/exclude, examples

### The iteration mindset
First drafts are starting points. The mental model shift: prompting is a conversation, not a one-shot command. Effective workflow:
- Run the first prompt
- Identify specifically what's wrong (not "make it better" → "cut paragraphs 1-2 and make the conclusion actionable")
- Know when to start fresh vs. refine in-thread

### The 4D AI Fluency framework (Anthropic/Dakan & Feller)
- **Delegation** — deciding which tasks go to AI vs. human
- **Description** — communicating clearly with AI (the prompt itself)
- **Discernment** — critically evaluating AI output
- **Diligence** — using AI responsibly and maintaining accountability

## Practical notes
- **Specificity beats length.** "Write an email to our enterprise client explaining the two-week delay on the integration, second delay, keep it professional but apologetic" beats "write an email about the delay."
- **Show, don't just tell.** For format requirements, provide an example of the desired structure.
- **Tone in plain language.** "More conversational," "authoritative and formal," "terse, like a senior engineer wrote it."
- **For recurring tasks, build evals.** Prompts that work reliably need to be tested, not just intuited. See [[concepts/evals]].

## See also
- [[concepts/evals]]
- [[concepts/skills-vs-projects]]
- [[concepts/4d-framework]] — the 4D framework in full; Description is one dimension
- [[concepts/ai-fluency]]
- [[tools/claude-projects]]

## Sources
- [[sources/claude-101-better-results]] — common failure modes, the iteration mindset, the 4D framework, and eval approach
- [[sources/claude-101-first-conversation]] — foundational three-part prompt structure
- [[sources/ai-fluency-intro]] — primary academic source for the 4D framework origin
