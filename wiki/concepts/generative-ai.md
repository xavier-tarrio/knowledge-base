---
title: Generative AI
type: concept
sources: [ai-fluency-generative-ai, ai-fluency-capabilities-limitations]
last_updated: 2026-05-10
---

# Generative AI

## What it is
AI systems that create new content — text, code, images, audio — rather than classifying or retrieving existing data. Modern generative AI is powered by Large Language Models (LLMs) built on the transformer architecture, trained on vast datasets, and fine-tuned to follow instructions and be helpful.

## Why it matters (for this domain)
Understanding how LLMs work changes how you use them. Knowing that Claude predicts the next most-likely token (not "thinking" the way humans do) explains why hallucinations happen, why context window size matters, and why the quality of your prompt determines the quality of the output. For a data engineer at Revolut, this knowledge underpins every decision about what to delegate.

## How it works
Three developments made modern LLMs possible:
1. **Transformer architecture** — the algorithmic breakthrough enabling parallel attention over long sequences
2. **Vast training data** — billions of text examples from the internet, books, and code
3. **Dramatic compute increases** — GPUs/TPUs enabling training at scale

**Training stages:**
- **Pre-training** — the model learns statistical patterns across billions of examples; learns to predict next tokens
- **Fine-tuning** — the model learns to follow instructions, be helpful, and align with human preferences

**Key properties:**
- Context window — the token limit bounding what the model can see in one call (see [[concepts/context-window]])
- Emergent capabilities — abilities that appear at scale not explicitly trained for
- Hallucinations — confident, fluent, factually wrong outputs (a consequence of the prediction mechanism)

## Practical notes
- Knowledge cutoff: the model knows nothing after its training cutoff date — always verify time-sensitive claims
- Hallucinations are not bugs; they are a fundamental property of next-token prediction. Mitigation: [[concepts/discernment-competency]] and [[concepts/evals]]
- Context window limits matter at Revolut scale — large SQL schemas, long migration specs, or full YAML configs may need chunking

## See also
- [[concepts/context-window]]
- [[concepts/delegation-competency]] — knowing AI's limits shapes what you delegate
- [[concepts/discernment-competency]] — knowing how AI works sharpens evaluation

## Sources
- [[sources/ai-fluency-generative-ai]] — transformer architecture, training stages, emergent capabilities
- [[sources/ai-fluency-capabilities-limitations]] — current capabilities and limitations in practice
