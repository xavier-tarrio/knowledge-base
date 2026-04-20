---
title: Claude Research Mode
type: tool
sources: [claude-101-research-mode]
last_updated: 2026-04-12
---

# Claude Research Mode

## What it does
An agentic investigation feature that transforms Claude from a single-query responder into a systematic multi-source researcher. When enabled, Claude autonomously conducts multiple iterative web searches (and connected integrations), building on each search result to pursue leads and fill gaps — without you directing each step. Extended thinking is automatically enabled. Outputs include comprehensive reports with citations. Completion time: 5–45 minutes depending on complexity.

## When to use it
- **Market and competitive analysis** — synthesizing information about a market, competitor landscape, or vendor evaluation
- **Complex project planning** — team offsites, product launches, initiatives requiring multi-source input
- **Technical research** — documenting a technology area by pulling from multiple sources
- **Cross-source synthesis** — combining web research with your connected integrations (Gmail, Drive, Slack) in one pass
- When you need **citations** you can verify
- When you'd otherwise spend hours manually searching and reading

## When NOT to use it
| Instead use... | When... |
|---------------|---------|
| Web search | Quick specific fact (stock price, company address) |
| Extended thinking | Deep reasoning on a problem that doesn't need external data |
| Enterprise search | Question specific to your org's internal knowledge |
| Standard chat | Speed matters more than comprehensiveness |

## How it works
1. Extended thinking activates — Claude plans its investigation approach
2. Claude runs multiple iterative searches (not one query, but a sequence that builds on findings)
3. Claude synthesizes findings from web + any connected integrations
4. Output: comprehensive report with inline citations

## Practical notes
- Web search must be enabled for Research to work.
- You can turn OFF web search and use Research for internal-only synthesis across connected tools (e.g. "summarize everything discussed about Q3 launch across Slack and Docs").
- **Invest in your prompt** — a 45-minute research run on a bad prompt is 45 wasted minutes. Specify: goal, sections you want, constraints (budget, geography, timeframe).
- Connected integrations (Google Workspace) dramatically increase power for business questions.

## Key concepts to understand
- [[concepts/agentic-ai]] — Research is agentic search
- [[concepts/extended-thinking]] — always active in Research mode
- [[tools/mcp-connectors]] — integrations that Research can query

## Sources
- [[sources/claude-101-research-mode]] — complete feature description, decision framework, prompt tips
