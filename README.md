# intelli-agent

**Autonomous general-purpose multi-agent orchestrator for Claude Code.**

Give it any multi-domain task. It classifies the domain, routes to specialized agents via a registry, runs them in parallel on a global dependency-graph scheduler, validates outputs with a review agent, and produces final results — no API key, no separate service, no credentials.

## What it does

- **Domain detection** — classifies your task into research / code / data / content / analysis (or multi-domain combinations)
- **Specialized agent registry** — 7 v1 agents, each with defined expertise, token budgets, and output contracts
- **Global DAG scheduler** — every task whose dependencies are met runs simultaneously (up to concurrency cap), across all domains at once
- **Task-level review** — high-stakes tasks (code, analysis recommendations) auto-trigger a review agent before their output proceeds
- **Vector memory** — prior run results inform new tasks (requires chromadb; graceful fallback if unavailable)
- **Live dashboard** — real-time agent cards, DAG flowchart, progress bar, interactive approvals, milestone undo/redo

## Install

```
/plugin marketplace add FaisalNoman/agentic-builder
/plugin install intelli-agent@intelli-agent
```

(Note: hosted in the same repo as agentic-builder. Install them independently — they don't interfere.)

## Use

Describe what you want:

```
Research the top 5 AI coding assistants, analyze their pricing and feature gaps,
then produce a competitive intelligence report with a recommendation for our team of 12.
```

Or invoke explicitly:

```
/intelli-agent Research our competitors in the project management space and produce
a strategic positioning document.
```

intelli-agent will: detect domains → ask any needed clarifying questions → show a DAG plan for approval → run specialist agents in parallel → validate outputs → produce final files in `outputs/`.

## v1 agents

| Agent | Domain(s) | What it does |
|---|---|---|
| research-agent | research, analysis | Web search, source synthesis, citations |
| code-agent | code | Implementation, tests, self-review |
| data-agent | data_processing | ETL, schema validation, aggregation |
| content-agent | content | Documents, reports, summaries |
| analysis-agent | analysis, research | Comparisons, SCQA recommendations |
| review-agent | all | Quality scoring — never rewrites, only judges |
| coordinator-agent | all | Decomposition, gate management, merging |

## What it's not

- Not a replacement for agentic-builder (which handles SDLC/code builds with TDD and code review)
- Not a standalone service — runs in-session under Claude Code, uses your subscription
- Not multi-user — single session, single user

## Notes

- Dashboard binds to `localhost` on an auto-selected port starting at 4318
- No API key required
- chromadb optional (vector memory) — install with `pip install chromadb`

## License

MIT
