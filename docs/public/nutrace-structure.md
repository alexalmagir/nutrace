# Nutrace — Product Structure

> Detail of the Nutrace product repository (`alexalmagir/nutrace`).

---

## Layout

```text
nutrace/
├── README.md                              🌐 front door + restrictive notice
├── LICENSE                                🌐 all rights reserved
├── .gitignore                             🌐 publishing control
├── CLAUDE.md                              🔒 operational memory (gitignored)
├── PUBLISHING_POLICY.md                   🔒 internal governance (gitignored)
├── PUBLIC_PRIVATE_MAP.md                  🔒 internal classification (gitignored)
├── .mcp.json                              🔒 MCP config (gitignored)
├── .claude/
│   ├── README.md                          🌐 explains the agent system + why private
│   ├── settings.json                      🌐 trivial workspace settings
│   ├── agents/                            🔒 8 technical agents (gitignored)
│   │   ├── tech-lead.md
│   │   ├── backend-engineer.md
│   │   ├── frontend-engineer.md
│   │   ├── product-engineer.md
│   │   ├── code-reviewer.md
│   │   ├── refactoring-engineer.md
│   │   ├── qa-engineer.md
│   │   └── security-engineer.md
│   ├── rules/                             🔒 6 operational rules (gitignored)
│   │   ├── coding-standards.md
│   │   ├── architecture.md
│   │   ├── testing.md
│   │   ├── migrations.md
│   │   ├── security.md
│   │   └── delivery.md
│   └── skills/                            🔒 reusable skills (gitignored)
├── docs/                                  🌐 full internal docs (already public)
│   ├── 00-project-charter.md
│   ├── 01-founder-venture-brief.md
│   ├── 02-competitive-analysis.md
│   ├── 03-validation-plan-and-results.md
│   ├── 04-prd-lite.md
│   ├── 05-ux-flows-and-wireframes.md
│   ├── 06-tech-architecture.md
│   ├── 07-implementation-plan.md
│   ├── 08-all-hands-review.md
│   ├── 09-founder-mitigations.md
│   ├── 10-validation-experiments.md
│   ├── agent-system.md
│   ├── ai-build-log.md
│   ├── competitive-analysis.md
│   └── public/                            🌐 curated portfolio layer
├── assets/
│   ├── user-flows/                        🌐 FigJam navigation diagrams
│   ├── wireframes/                        🌐 Figma Make prompts + descriptions
│   └── social/                            🌐 social media assets
└── src/                                   🌐 source code (case-by-case)
```

## What is public

- `README.md`, `LICENSE`, `.gitignore` — visible on GitHub
- `.claude/README.md`, `.claude/settings.json` — explain the agent system without exposing internals
- `docs/00`–`docs/10` — full product docs, already publicly pushed (historical decision, preserved)
- `docs/public/` — curated portfolio-facing summaries

## What is private

- `CLAUDE.md` — operational memory for the agent system (session state, internal context)
- `PUBLISHING_POLICY.md`, `PUBLIC_PRIVATE_MAP.md` — internal governance and classification criteria
- `.mcp.json` — MCP server config with token references
- `.claude/agents/`, `.claude/rules/`, `.claude/skills/` — raw operating logic

All private files are gitignored. They exist locally but are never pushed to GitHub.

## Reading order for a visitor

1. [`README.md`](../../README.md) — the one-minute read
2. [`docs/public/project-overview.md`](project-overview.md) — what, why, status
3. [`docs/public/market-research-summary.md`](market-research-summary.md) — market evidence
4. [`docs/public/discovery-summary.md`](discovery-summary.md) — how we validated
5. [`docs/public/prd-lite.md`](prd-lite.md) — what we're actually building
6. [`docs/public/architecture-overview.md`](architecture-overview.md) — how it's built
7. [`docs/public/agent-system-overview.md`](agent-system-overview.md) — the team behind it
8. [`docs/public/claude-project-context.md`](claude-project-context.md) — project context and privacy model
9. Optional deep dive: the full `docs/00`–`docs/10` files

See also:
- [`ai-product-builder-structure.md`](ai-product-builder-structure.md) — the studio above this product
- [`repository-structure.md`](repository-structure.md) — both layers side by side
