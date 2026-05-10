# Wiki Log

## [2026-05-10] session | Session 2026-05-10 closed
- Session page written: wiki/sessions/2026-05-10.md
- Wiki total: 81 pages

## [2026-05-10] ingest | Model Context Protocol — complete documentation set (16 sources)
- Created sources (16): mcp-what-is, mcp-introducing, mcp-architecture-overview, mcp-beginners-course, mcp-server-concepts, mcp-client-concepts, mcp-build-server, mcp-build-client, mcp-security-best-practices, mcp-authorization, mcp-connect-local, mcp-agent-skills, mcp-clients-overview, mcp-inspector-doc, mcp-example-clients, mcp-sdks
- Created concepts (3): mcp-primitives, mcp-security + major expansion of model-context-protocol
- Created tools (1): mcp-inspector
- Created domains (1): domains/mcp (narrative + Mermaid diagrams)
- Created ventures (1): revolut-ai-toolkit (idea stage — 5 MCP server concepts for Revolut stack)
- Total pages: 49 → 80

## [2026-05-10] ingest | AI Fluency Framework Foundations — complete course (9 lessons)
- Created sources (9): ai-fluency-generative-ai, ai-fluency-4d-framework-lesson, ai-fluency-capabilities-limitations, ai-fluency-delegation, ai-fluency-description, ai-fluency-discernment, ai-fluency-diligence, ai-fluency-prompting, ai-fluency-conclusion
- Created concepts (6): generative-ai, delegation-competency, description-competency, discernment-competency, diligence-competency, prompting-techniques
- Updated concepts (2): 4d-framework (sources expanded), prompt-engineering (sources expanded)
- All concept pages grounded in Revolut/data engineering context (Trino SQL, EOS YAML, reg reporting)
- Total pages: 34 → 49

## [2026-04-20] schema-update | Human-readable architecture header added to CLAUDE.md
- Added "For humans" section at top of CLAUDE.md: stack table, directory structure, setup guide, session workflow, evolution roadmap
- Single source of truth: one file for both agent instructions and human replication guide
- Roadmap phases documented: Learn (active) → Test → Build → Ship

## [2026-04-20] schema-update | Sessions layer added
- New page type: wiki/sessions/YYYY-MM-DD.md — daily learning journal
- SESSION workflow added to CLAUDE.md (open/close protocol)
- Session page template added to CLAUDE.md page formats
- Commit convention: session(YYYY-MM-DD): <topic>
- index.md updated with Sessions section

## [2026-04-20] schema-update | Git-aware session startup + repo initialised
- Repo initialised with `git init`; initial commit includes all 33 wiki pages + raw sources.
- CLAUDE.md startup checklist updated: step 2 now runs `git status` / `git diff --name-only HEAD` first.
- Benefit: only reads changed files at session start instead of full wiki re-read.
- `.gitignore` excludes `.obsidian/` and `.claude/`.

## [2026-04-20] ingest | Anthropic Academy AI Fluency Framework Foundations — lessons 1 & 2
- Created sources (2): ai-fluency-intro, ai-fluency-why
- Created concepts (3): ai-fluency, 4d-framework, ai-collaboration-modes
- Created entities (2): rick-dakan, joseph-feller
- Updated concepts (2): agentic-ai (added Agency mode link), prompt-engineering (added 4D source + see-also)
- Updated entities (1): anthropic-academy (added AI Fluency course entry)
- Updated: index.md (9 new entries, total pages 24 → 33)

> Append-only. Format: `## [YYYY-MM-DD] {operation} | {title}`

## [2026-04-12] schema-update | Added ventures/ layer and four-layer knowledge model
- Added `ventures/` directory to wiki structure.
- Added four-layer knowledge model to CLAUDE.md (Knowledge → Sources → Synthesis → Action).
- Added VENTURE workflow to CLAUDE.md.
- Added venture page template to CLAUDE.md (stages: idea → plan → active → shipped).
- Updated index format with Ventures section.

## [2026-04-12] ingest | Anthropic Academy Claude 101 — all 9 lessons
- Created sources (9): claude-101-projects, claude-101-first-conversation, claude-101-desktop-modes, claude-101-better-results, claude-101-connecting-tools, claude-101-skills, claude-101-research-mode, claude-101-other-ways, claude-101-use-cases
- Created concepts (8): rag, model-context-protocol, agentic-ai, extended-thinking, prompt-engineering, evals, skills-vs-projects, context-window
- Created tools (7): claude-ai, claude-code, claude-projects, claude-skills, claude-research, claude-desktop, mcp-connectors
- Created entities (2): anthropic, anthropic-academy
- Updated: index.md (24 new entries, all sections populated)

## [2026-04-12] schema-update | raw/ directory convention documented
- Flat structure with descriptive slugs (author-site-topic-year.ext).
- assets/ remains the only subdirectory.
- Evolution path to source-type subdirs noted for when archive exceeds ~20 files.

## [2026-04-12] setup | Wiki initialised
- Folder structure created.
- index.md and log.md initialised.
- CLAUDE.md installed.
