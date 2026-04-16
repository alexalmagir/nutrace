# Nutrace — Project Context

> Public-safe overview of the project, the role AI plays in building it, and how public and private materials are separated. This document replaces any direct exposure of internal operational memory.

---

## What Nutrace is

Nutrace is a frictionless food and symptom diary for people with IBS, IBD, food intolerances, and undiagnosed digestive symptoms. Users photograph meals, receive proactive trigger alerts via vision AI, record symptoms by voice, and export structured PDFs for their gastroenterologist or dietitian.

It is a data-capture and journaling tool. It does not diagnose, recommend treatment, or provide medical advice.

## How it is built

Nutrace is built end-to-end using an AI-native product organization: a team of Claude Code agents, structured in two layers, working under a Senior Technical PM.

- **Studio layer** — six executive agents (Chief of Staff, Founder, CPO, CTO, CDO, CMO) handle ideation, validation, product definition, architecture, UX, and positioning.
- **Product layer** — eight technical agents (tech-lead, backend-engineer, frontend-engineer, product-engineer, code-reviewer, refactoring-engineer, qa-engineer, security-engineer) handle day-to-day engineering execution.

Every session produces at least one committed artifact. The build log at [`docs/ai-build-log.md`](../ai-build-log.md) records what was produced, by which agents, in each session.

## What is publicly visible

This repository is a portfolio showcase. The following are tracked by git and visible on GitHub:

- **Product documentation** — project charter, market research, competitive analysis, validation results, PRD-Lite, UX flows, architecture, implementation plan, review notes, and validation experiments (`docs/00` through `docs/10`)
- **Curated summaries** — portfolio-facing navigation layer in `docs/public/`
- **Repository scaffolding** — `README.md`, `LICENSE`, `.gitignore`, `.claude/README.md`, `.claude/settings.json`
- **Assets** — FigJam flow descriptions, wireframe prompts, social media materials

## What is private

The following exist locally but are never pushed to GitHub:

- **Operational memory** (`CLAUDE.md`) — session state, agent instructions, internal context. This is working memory for the agent system, not a public artifact.
- **Governance and classification files** (`PUBLISHING_POLICY.md`, `PUBLIC_PRIVATE_MAP.md`) — internal controls that define what is published and how files are classified.
- **Agent definitions** (`.claude/agents/`) — raw prompts and behavior specifications for all agents.
- **Operating rules** (`.claude/rules/`) — coding standards, architecture principles, testing strategy, migration safety, security posture, delivery standards.
- **Reusable skills** (`.claude/skills/`) — operational patterns that may be shared across products.
- **MCP configuration** (`.mcp.json`) — server config with token references.
- **Secrets** (`.env*`, credentials) — never committed.

## Why this separation exists

This repository demonstrates how a Senior Technical PM works with AI tools — from market research through architecture, delivery, and launch. That demonstration requires real, visible work product.

At the same time, the operational logic that makes the agent system work — the prompts, heuristics, escalation criteria, governance mechanics — is intellectual property. Publishing it would make the system trivially clonable without reproducing the thinking behind it.

The separation is straightforward:

- **Show the work** — product thinking, research, architecture, code, decisions
- **Protect the operating system** — agent definitions, rules, governance, session memory

Public documentation describes *that* the system exists and *what each role does*. It does not expose *how* the agents are prompted or *how* internal decisions are classified.

## Project status

| Phase | Status |
|---|---|
| A — Ideation | Done (GO, 43/50) |
| B — Validation | Done (H1 14/15, H2 15/15) |
| C — Definition | Done (PRD + UX + architecture) |
| D — Build | In progress (validation experiments E1-E7) |
| E — Launch | Pending |

## Where to start

| You want to... | Read |
|---|---|
| Understand the product | [`project-overview.md`](project-overview.md) |
| See the market evidence | [`market-research-summary.md`](market-research-summary.md) |
| See how discovery was run | [`discovery-summary.md`](discovery-summary.md) |
| See the architecture | [`architecture-overview.md`](architecture-overview.md) |
| See the agent system | [`agent-system-overview.md`](agent-system-overview.md) |
| See the repo layout | [`repository-structure.md`](repository-structure.md) |
