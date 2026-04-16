# Repository Structure

> Commented tree across both layers. Shows the studio (local meta-workspace) and the Nutrace product repo side by side, with public/private classification.

---

## Two-layer model

| Layer | Purpose | Git state |
|---|---|---|
| **AI Product Builder** (studio) | Executive agents, session orchestration, reusable skills | Local-only (not a git repo) |
| **Nutrace** (product) | Actual product work, public showcase of capability | Own GitHub repo (`alexalmagir/nutrace`) |

---

## Full tree

```text
AI Product Builder/                          ← LOCAL meta-workspace (not a git repo)
├── CLAUDE.md                                🌐 studio entry point for Claude
├── PUBLISHING_POLICY.md                     🌐 studio-level governance
├── PUBLIC_PRIVATE_MAP.md                    🌐 studio-level classification
├── .mcp.json                                🔒 MCP config (token via env var)
├── .claude/
│   ├── settings.json                        🔒 local
│   ├── agents/                              🔒 studio executive agents (private)
│   │   ├── chief-of-staff.md
│   │   ├── founder.md
│   │   ├── cpo.md
│   │   ├── cto.md
│   │   ├── cdo.md
│   │   └── cmo.md
│   ├── rules/                               🔒 system-level rules (private)
│   │   └── ai-product-builder-rules.md
│   └── skills/                              🔒 reusable cross-project skills
│       └── README.md
└── projects/
    └── nutrace/                             ← INDEPENDENT git repo → alexalmagir/nutrace
        ├── README.md                        🌐 front-door intro + restrictive notice
        ├── LICENSE                          🌐 all rights reserved
        ├── CLAUDE.md                        🌐 project memory for Claude
        ├── PUBLISHING_POLICY.md             🌐 nutrace-level governance
        ├── PUBLIC_PRIVATE_MAP.md            🌐 nutrace-level classification
        ├── .gitignore                       🌐 publishing control
        ├── .mcp.json                        🔒 MCP config
        ├── .claude/
        │   ├── README.md                    🌐 explains the agent system + why private
        │   ├── settings.json                🌐 trivial workspace settings
        │   ├── agents/                      🔒 8 technical agents (private)
        │   │   ├── tech-lead.md
        │   │   ├── backend-engineer.md
        │   │   ├── frontend-engineer.md
        │   │   ├── product-engineer.md
        │   │   ├── code-reviewer.md
        │   │   ├── refactoring-engineer.md
        │   │   ├── qa-engineer.md
        │   │   └── security-engineer.md
        │   ├── rules/                       🔒 6 operational rules (private)
        │   │   ├── coding-standards.md
        │   │   ├── architecture.md
        │   │   ├── testing.md
        │   │   ├── migrations.md
        │   │   ├── security.md
        │   │   └── delivery.md
        │   └── skills/                      🔒 reusable operational skills
        ├── docs/                            🌐 full internal docs (already public)
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
        │   └── public/                      🌐 curated portfolio-facing layer
        │       ├── project-overview.md
        │       ├── market-research-summary.md
        │       ├── discovery-summary.md
        │       ├── prd-lite.md
        │       ├── architecture-overview.md
        │       ├── agent-system-overview.md
        │       ├── venture-studio-operating-model.md
        │       ├── nutrace-technical-delivery-model.md
        │       ├── repository-structure.md
        │       ├── ai-product-builder-structure.md
        │       ├── nutrace-structure.md
        │       ├── ai-build-log.md
        │       └── lessons-learned.md
        ├── assets/                          🌐 FigJam links, wireframe prompts, social
        └── src/                             🌐 source code (case-by-case as written)
```

## Legend

- 🌐 PUBLIC — tracked by git, visible on GitHub
- 🔒 PRIVATE — gitignored, local-only
- 📝 DERIVED — public-safe summary exists; see `PUBLIC_PRIVATE_MAP.md`

## Why it's shaped this way

- The **studio** is local-only because it orchestrates many potential products. Its internals are IP.
- The **product** is a public repo because the work itself is the portfolio.
- Both layers share the same governance pattern: `PUBLISHING_POLICY.md` + `PUBLIC_PRIVATE_MAP.md`.
- The `.claude/` folder follows a "public README, private internals" pattern at both levels.

See also:
- [`ai-product-builder-structure.md`](ai-product-builder-structure.md) — studio directory detail
- [`nutrace-structure.md`](nutrace-structure.md) — product directory detail
- [`PUBLISHING_POLICY.md`](../../PUBLISHING_POLICY.md) at the nutrace root
