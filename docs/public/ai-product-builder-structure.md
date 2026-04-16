# AI Product Builder — Studio Structure

> Detail of the local studio meta-workspace. The studio itself is not a git repo; it orchestrates many products, each in its own repo. All studio-level files are private.

---

## Layout

```text
AI Product Builder/                       ← LOCAL meta-workspace (not a git repo)
├── CLAUDE.md                             🔒 operational memory (private)
├── PUBLISHING_POLICY.md                  🔒 internal governance (private)
├── PUBLIC_PRIVATE_MAP.md                 🔒 internal classification (private)
├── .mcp.json                             🔒 MCP config (env-var token)
├── .claude/
│   ├── settings.json                     🔒
│   ├── agents/                           🔒 executive agents
│   │   ├── chief-of-staff.md
│   │   ├── founder.md
│   │   ├── cpo.md
│   │   ├── cto.md
│   │   ├── cdo.md
│   │   └── cmo.md
│   ├── rules/                            🔒 system-level rules
│   │   └── ai-product-builder-rules.md
│   └── skills/                           🔒 reusable cross-project skills
│       └── README.md
└── projects/
    └── nutrace/                          ← independent git repo
```

## What lives where

| Path | Purpose | Visibility |
|---|---|---|
| `CLAUDE.md` | Operational memory. Session state, active projects, agent workflow. | 🔒 Private |
| `PUBLISHING_POLICY.md` | Internal governance — publishing criteria and decision rules. | 🔒 Private |
| `PUBLIC_PRIVATE_MAP.md` | Internal classification — per-path public/private assignments. | 🔒 Private |
| `.claude/agents/` | The six executive agents (Chief of Staff, Founder, CPO, CTO, CDO, CMO). | 🔒 Private |
| `.claude/rules/` | System rules, build rhythm, GitHub handoff format. | 🔒 Private |
| `.claude/skills/` | Reusable skills that can be called across projects. | 🔒 Private |
| `projects/` | Each subfolder is an independent git repo on GitHub. | Per-product |

## Git boundary

- `AI Product Builder/` has **no `.git/` directory** and must never be `git init`-ed.
- `projects/nutrace/` has its own `.git/` and pushes to `alexalmagir/nutrace`.
- This boundary keeps all studio-level files — operational memory, governance, agent definitions — strictly local.

## Why the studio is entirely local

The studio is the operating system behind many potential products. Publishing it would:

1. Expose orchestration patterns and executive agent prompts
2. Conflate workspace tooling with product work
3. Create a monorepo when each product benefits from its own clean history

Instead, the studio stays local. Each product repo publishes curated summaries (see [`venture-studio-operating-model.md`](venture-studio-operating-model.md)) so visitors understand the model without the raw internals.

## How a new product joins the studio

1. `mkdir projects/<new-product>`
2. `git init` inside the product folder and push to `alexalmagir/<new-product>`
3. Copy the `.claude/` skeleton (README, settings, agents/, rules/, skills/)
4. Register the product in the studio's internal project tracking

See:
- [`nutrace-structure.md`](nutrace-structure.md) for how this plays out inside a product
- [`repository-structure.md`](repository-structure.md) for the full tree
