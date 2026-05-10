---
title: Revolut AI Toolkit
type: venture
stage: idea
created: 2026-05-10
last_updated: 2026-05-10
tags: [mcp, data-engineering, revolut, trino, eos, airflow]
---

# Revolut AI Toolkit

## The opportunity
Data engineers at Revolut work daily with Trino SQL, EOS (internal dbt), Airflow, and JOVE — but Claude has no direct access to any of these systems. Every interaction requires copy-pasting schemas, queries, YAML definitions, and error messages into the chat. This friction limits how much Claude can actually help and forces the engineer to be the integration layer. MCP can eliminate that entirely.

**Why now**: MCP has reached broad ecosystem support (113+ clients), Claude Code supports it natively, and the Python SDK makes building custom servers practical in an afternoon. The barrier is low; the productivity gain is significant.

## Core concept
A personal MCP server (or small suite of servers) that gives Claude direct read access to the Revolut data stack — schemas, existing models, query results, pipeline status. Claude becomes a genuine pairing partner instead of a text processor.

## Ideas by tool

### 1. Trino MCP Server
**What it enables**: Claude can explore your data catalog, understand table schemas, and validate SQL queries before you run them.

| Tool | What it does |
|------|-------------|
| `list_catalogs()` | Returns all available Trino catalogs |
| `list_schemas(catalog)` | Lists schemas within a catalog |
| `list_tables(catalog, schema)` | Lists tables in a schema |
| `get_table_schema(catalog, schema, table)` | Returns column names, types, comments |
| `run_read_query(sql)` | Executes a read-only query, returns results as JSON |
| `explain_query(sql)` | Returns Trino's EXPLAIN output for a query |

**Resources**: Expose table schemas as Resources so they're automatically included as context when Claude writes SQL — no need to paste the schema manually.

**New use case idea**: *Query validator* — before running a query in JOVE, ask Claude to review it. Claude reads the real schema (via Resource), checks column names, types, join conditions, and flag potential issues.

### 2. EOS Model Assistant
**What it enables**: Claude can read existing EOS model definitions and generate new ones following your team's conventions.

| Tool | What it does |
|------|-------------|
| `list_eos_models(domain)` | Lists EOS models in a domain |
| `get_eos_model(model_name)` | Returns the full YAML definition |
| `validate_eos_yaml(yaml_string)` | Validates YAML against EOS schema rules |

**Resources**: Expose the EOS YAML specification as a Resource — Claude always knows the current format without you pasting it.

**Prompt**: `/generate-eos-model table=<name> catalog=<catalog>` — triggers a guided workflow:
1. Read table schema from Trino (via Tool)
2. Check existing models in the same domain (via Tool)
3. Generate EOS YAML following established patterns
4. Validate the output (via Tool)

**New use case idea**: *Migration assistant for GAIA→EOS* — expose both the GAIA source definitions and EOS target templates as Resources, then use a `/migrate-model` prompt to guide Claude through generating the EOS equivalent for each GAIA model.

### 3. Airflow Pipeline Inspector
**What it enables**: Claude understands which pipelines feed which tables, and can check DAG status before debugging data issues.

| Tool | What it does |
|------|-------------|
| `list_dags(filter_tag)` | Lists Airflow DAGs with optional tag filter |
| `get_dag_status(dag_id)` | Returns last N run statuses for a DAG |
| `get_dag_definition(dag_id)` | Returns the DAG Python code |
| `get_task_log(dag_id, run_id, task_id)` | Returns task execution log |

**New use case idea**: *Data freshness check* — when Claude is helping debug a reporting discrepancy, it first checks Airflow to see if the upstream pipeline ran successfully and when, before digging into the SQL logic.

### 4. Reg Report Validator
**What it enables**: Before submitting Bank Account Register reports (the GAIA→EOS migration work), Claude can validate output against expected row counts, null rates, and business rules.

| Tool | What it does |
|------|-------------|
| `run_validation_suite(model_name, date)` | Runs pre-defined quality checks for a model |
| `compare_gaia_vs_eos(model_name, date)` | Row-level comparison between GAIA and EOS output |
| `get_reconciliation_summary(date)` | Returns summary stats for reconciliation report |

**New use case idea**: *Automated diff report* — after each EOS migration run, Claude generates a plain-English summary of the reconciliation results: "3 of 5 models pass. Table X has a 0.02% row count discrepancy, most likely due to…"

### 5. Context Injector (meta-tool)
A lightweight MCP server that exposes your personal workspace context as Resources:

- Current sprint tickets (from JIRA/your task system)
- Team conventions doc (coding standards, naming rules)
- Recent decisions log (what was decided in last week's meetings)

**Why this matters**: Every Claude conversation currently starts cold. With context injection, Claude always knows what you're working on, what the team conventions are, and what was recently decided — without you re-explaining every session.

## Knowledge dependencies
- [[concepts/model-context-protocol]] — the protocol all of this is built on
- [[concepts/mcp-primitives]] — tools for actions, resources for schemas/docs, prompts for workflows
- [[concepts/mcp-security]] — security considerations before exposing internal data
- [[concepts/agentic-ai]] — the multi-step behavior these tools enable
- [[sources/mcp-build-server]] — the Python FastMCP tutorial to follow

## Next actions
- [ ] Build Trino MCP server (local STDIO, Python, read-only queries only)
- [ ] Test with MCP Inspector before connecting to Claude Desktop
- [ ] Connect to Claude Desktop and validate the `list_tables` + `get_schema` tools
- [ ] Use Claude to write 5 real queries using the Trino server — measure how much better the SQL is
- [ ] Expand to EOS model reading once Trino server is stable

## Log
- **2026-05-10**: Venture created after ingesting MCP documentation. Ideas identified during MCP learning session. All at idea stage — none implemented yet.
