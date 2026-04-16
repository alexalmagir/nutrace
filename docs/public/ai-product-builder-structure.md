# AI Product Builder — Studio Structure

> Detail of the local studio meta-workspace. The studio itself is not a git repo; it orchestrates many products, each in its own repo.

---

## Layout

```text
AI Product Builder/                       ← LOCAL meta-workspace (not a git repo)
├── CLAUDE.md                             ← studio entry point + active projects
├── PUBLISHING_POLICY.md                  ← studio governance
├── PUBLIC_PRIVATE_MAP.md                 ← studio classification
├── .mcp.json                             ← GitHub MCP config (env-var token)
├── .claude/
│   ├── settings.json
│   ├── agents/                           ← executive agents (private)
│   │   ├── chief-of-staff.md
│   │   ├── founder.md
│   │   ├── cpo.md
│   │   ├── cto.md
│   │   ├── cdo.md
│   │   └── cmo.md
│   ├── rules/
│   │   └── ai-product-builder-rules.md
│   └── skills/
│       └── README.md
└── projects/
    └── nutrace/                          ← independent git repo
```

## What lives where

| Path | Purpose |
|---|---|
| `CLAUDE.md` | Studio entry point. Describes the purpose, workflow, active projects. Read at the start of every session. |
| `PUBLISHING_POLICY.md` | Why the studio is local-only and how publishing decisions are made. |
| `PUBLIC_PRIVATE_MAP.md` | Per-path classification inside the studio. |
| `.claude/agents/` | The six executive agents (Chief of Staff, Founder, CPO, CTO, CDO, CMO). |
| `.claude/rules/` | System rules, build rhythm, GitHub handoff format. |
| `.claude/skills/` | Reusable skills that can be called across projects. |
| `projects/` | Each subfolder is an independent git repo on GitHub. |

## Git boundary

- `AI Product Builder/` has **no `.git/` directory** and must never be `git init`-ed.
- `projects/nutrace/` has its own `.git/` and pushes to `alexalmagir/nutrace`.
- This boundary is what keeps executive-layer IP local while the product layer is public.

## Why it's not a git repo

The studio is the operating system behind many potential products. Committing it would:

1. Publish the orchestration patterns and executive agent prompts
2. Conflate "workspace tooling" with "product work"
3. Create one giant monorepo when each product benefits from its own clean history

Instead, the studio stays local, and every product repo publishes a curated summary of the studio (see [`venture-studio-operating-model.md`](venture-studio-operating-model.md)) so visitors understand the model without the raw internals.

## How a new product joins the studio

1. `mkdir projects/<new-product>`
2. `git init` inside the product folder and push to `alexalmagir/<new-product>`
3. Copy the `.claude/` skeleton (README, settings, agents/, rules/, skills/)
4. Add the product to the "Active Projects" table in studio `CLAUDE.md`

See:
- [`nutrace-structure.md`](nutrace-structure.md) for how this plays out inside a product
- [`repository-structure.md`](repository-structure.md) for the full tree
