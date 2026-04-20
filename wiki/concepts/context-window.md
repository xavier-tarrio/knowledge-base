---
title: Context Window
type: concept
sources: [claude-101-projects]
last_updated: 2026-04-12
---

# Context Window

## What it is
The maximum amount of text (measured in tokens) that a language model can process in a single inference call. Everything the model "sees" — the system prompt, conversation history, uploaded files, tool outputs — must fit within this window. Content outside the window is invisible to the model.

## Why it matters (for this domain)
Context window size determines what Claude can reason about simultaneously. For analytics engineers: a single large dbt project might have more code than fits in one context. For business builders: designing AI products means understanding what can and can't fit, and building retrieval strategies (RAG) for when it doesn't.

## How it works
- Tokens ≈ 0.75 words in English. Claude's context windows range from ~100K to 200K+ tokens depending on model.
- All inputs consume context: system instructions, user messages, assistant responses, tool call results, uploaded files.
- When context fills up, older content is either truncated or summarized (depending on the interface).
- In Claude Projects, RAG activates automatically near the context limit — retrieval replaces bulk loading.

## Practical notes
- Context is not free — larger context = more expensive API calls and slower responses.
- "Within context" vs. "retrieved via RAG" is a quality trade-off: in-context content is always available to the model; retrieved content is only available if the retrieval step finds it.
- For critical reference material (e.g. a system prompt, a key schema definition), put it in context. For large corpora (e.g. all your documentation), use RAG.
- Long conversations accumulate context. If a conversation goes off track, starting fresh with a clean, focused prompt often outperforms trying to redirect a loaded context.

## See also
- [[concepts/rag]]
- [[tools/claude-projects]]

## Sources
- [[sources/claude-101-projects]] — context window limits as the trigger for RAG in Claude Projects
