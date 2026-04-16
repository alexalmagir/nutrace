# Nutrace — Product Structure

> Detail of the Nutrace product repository (`alexalmagir/nutrace`).

---

## Layout

```text
nutrace/
├── README.md                              ← public front door + restrictive notice
├── LICENSE                                ← all rights reserved
├── CLAUDE.md                              ← project memory for Claude
├── PUBLISHING_POLICY.md                   ← nutrace governance
├── PUBLIC_PRIVATE_MAP.md                  ← per-path classification
├── .gitignore                             ← publishing control
├── .mcp.json                              🔒 private — GitHub MCP (env-var token)
├── .claude/
│   ├── README.md                          🌐 public — explains what is private and why
│   ├── settings.json                      🌐 trivial workspace settings
│   ├── agents/                            🔒 private — 8 technical agents
│   │   ├── tech-lead.md
│   │   ├── backend-engineer.md
│   │   ├── frontend-engineer.md
│   │   ├── product-engineer.md
│   │   ├── code-reviewer.md
│   │   ├── refactoring-engineer.md
│   │   ├── qa-engineer.md
│   │   └── security-engineer.md
│   ├── rules/                             🔒 private — 6 operational rules
│   │   ├── coding-standards.md
│   │   ├── architecture.md
│   │   ├── testing.md
│   │   ├── migrations.md
│   │   ├── security.md
│   │   └── delivery.md
│   └── skills/                            🔒 private — reusable skills
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

## Classification highlights

- Every root-level file is public: `README.md`, `LICENSE`, `CLAUDE.md`, both governance files, `.gitignore`.
- `.claude/README.md` and `.claude/settings.json` are public. Everything else under `.claude/` is gitignored.
- Internal `docs/00`–`docs/10` are already publicly pushed (historical decision, preserved).
- `docs/public/` is the curated portfolio-facing layer.

## Reading order for a visitor

1. [`README.md`](../../README.md) — the one-minute read
2. [`docs/public/project-overview.md`](project-overview.md) — what, why, status
3. [`docs/public/market-research-summary.md`](market-research-summary.md) — market evidence
4. [`docs/public/discovery-summary.md`](discovery-summary.md) — how we validated
5. [`docs/public/prd-lite.md`](prd-lite.md) — what we're actually building
6. [`docs/public/architecture-overview.md`](architecture-overview.md) — how it's built
7. [`docs/public/agent-system-overview.md`](agent-system-overview.md) — the team behind it
8. Optional deep dive: the full `docs/00`–`docs/10` files

See also:
- [`ai-product-builder-structure.md`](ai-product-builder-structure.md) — the studio above this product
- [`repository-structure.md`](repository-structure.md) — both layers side by side
