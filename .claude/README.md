# `.claude/` — Intentionally Private Agent System

> This folder configures the Claude Code agent team that builds Nutrace. Most of its contents are intentionally excluded from this public repository.

---

## What lives here

| Path | In repo? | What it is |
|---|---|---|
| `.claude/README.md` | ✅ Yes (this file) | Explains what this folder is and why it's mostly private. |
| `.claude/settings.json` | ✅ Yes | Trivial Claude Code workspace settings. |
| `.claude/agents/*.md` | ❌ Gitignored | Raw definitions of the 8 technical agents (tech-lead, backend-engineer, frontend-engineer, product-engineer, code-reviewer, refactoring-engineer, qa-engineer, security-engineer). |
| `.claude/rules/*.md` | ❌ Gitignored | Internal operating rules (coding standards, architecture, testing, migrations, security, delivery). |
| `.claude/skills/*` | ❌ Gitignored | Reusable operational skills. |

## Why the raw files are not published

The agent definitions, operational rules, and reusable skills are the **operating system** of the Nutrace product team. They encode how this team actually works — prompts, heuristics, escalation criteria, quality gates.

Publishing them raw would:

1. Weaken the intellectual property of the studio by making the operational logic trivially clonable
2. Expose internal heuristics that are explicitly meant to be refined privately
3. Conflate showcase (process, thinking, craft) with reusable template (copy-and-run)

This repository is a showcase, not an open-source template.

## What IS documented publicly

The *existence* of the agent system, the role each agent plays at a high level, and how the agents coordinate — all of that is public, because demonstrating rigorous AI-native product organization is one of the explicit goals of this repository.

See the curated docs in [`docs/public/`](../docs/public/):

- [`agent-system-overview.md`](../docs/public/agent-system-overview.md) — the two-layer (studio + product) model
- [`nutrace-technical-delivery-model.md`](../docs/public/nutrace-technical-delivery-model.md) — the 8 Nutrace technical agents
- [`venture-studio-operating-model.md`](../docs/public/venture-studio-operating-model.md) — the studio-level executive layer
- [`repository-structure.md`](../docs/public/repository-structure.md) — commented tree showing both layers

## Governance

This repository follows a strict public/private separation. Governance and classification files are internal. Public-facing documentation lives in [`docs/public/`](../docs/public/).
