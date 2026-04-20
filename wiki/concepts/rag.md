---
title: Retrieval-Augmented Generation (RAG)
type: concept
sources: [claude-101-projects]
last_updated: 2026-04-12
---

# Retrieval-Augmented Generation (RAG)

## What it is
A technique that expands an AI model's effective knowledge beyond its context window by dynamically fetching relevant information from an external store at inference time. Instead of loading all documents into the prompt, the system retrieves only the chunks most relevant to the current query.

## Why it matters (for this domain)
In Claude Projects, RAG activates automatically when a knowledge base approaches context window limits — expanding capacity up to 10x transparently. For analytics engineers building AI tools on top of large document corpora (e.g. internal data dictionaries, runbooks, client reports), RAG is the architecture that makes this feasible at scale.

## How it works
1. Documents are chunked and embedded into a vector store.
2. At query time, the user's input is embedded using the same model.
3. The most semantically similar chunks are retrieved.
4. Those chunks are injected into the model's context alongside the query.
5. The model generates a response grounded in the retrieved content.

The quality of retrieval depends heavily on: chunk size, overlap strategy, embedding model choice, and how well the query matches the stored content (dense vs. sparse retrieval trade-off).

## Practical notes
- Claude handles RAG invisibly within Projects — you don't configure it, it just kicks in.
- For custom pipelines (e.g. building your own RAG-backed tool via the API), you control every step: chunking, embedding, retrieval, re-ranking.
- RAG does NOT guarantee accuracy — it retrieves the most similar chunks, not necessarily the most correct or complete answer. Hallucination is still possible.
- For analytics use cases: RAG works well for structured reference material (schemas, metric definitions, process docs) but poorly for "compute this from raw data" queries — use SQL tools for that.

## See also
- [[tools/claude-projects]]
- [[concepts/context-window]]
- [[concepts/agentic-ai]]

## Sources
- [[sources/claude-101-projects]] — describes RAG as Claude's automatic scaling mechanism for project knowledge bases
