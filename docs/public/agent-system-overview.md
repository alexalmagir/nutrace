# Agent System Overview

> How Nutrace is built: a two-layer AI-native product organization. The raw agent definitions and operating rules are intentionally private — see [`PUBLISHING_POLICY.md`](../../PUBLISHING_POLICY.md).

---

## The two layers

Nutrace is built by a deliberately structured team of Claude Code subagents, organized in two layers.

```
┌────────────────────────────────────────────────────────┐
│  Layer 1 — AI Product Builder (venture studio)         │
│  ────────────────────────────────────────────────────  │
│  Chief of Staff   ←  session orchestration             │
│  Founder          ←  0→1 / 0→no-go decisions           │
│  CPO              ←  product strategy, PRD, ICP        │
│  CTO              ←  architecture governance           │
│  CDO              ←  UX, research, design              │
│  CMO              ←  positioning, messaging, GTM       │
└────────────────────────────────────────────────────────┘
                          │ delegates product build
                          ▼
┌────────────────────────────────────────────────────────┐
│  Layer 2 — Nutrace (product technical team)            │
│  ────────────────────────────────────────────────────  │
│  tech-lead            ←  implementation direction      │
│  backend-engineer     ←  FastAPI + Supabase            │
│  frontend-engineer    ←  React Native + Expo           │
│  product-engineer     ←  glue across UX and data       │
│  code-reviewer        ←  high-signal review            │
│  refactoring-engineer ←  targeted cleanups             │
│  qa-engineer          ←  validation and regression     │
│  security-engineer    ←  sensitive-area review         │
└────────────────────────────────────────────────────────┘
```

## How they coordinate

- **Chief of Staff** (studio) opens every session, sets a plan, and closes every session with a concrete next block.
- **Founder / CPO / CDO / CMO** make product- and market-level decisions and hand scope to the CTO.
- **CTO** (studio) governs technical strategy across all projects and delegates product-level implementation to the Nutrace technical agents.
- **tech-lead** (Nutrace) owns implementation direction within the product and escalates strategic decisions back to the studio CTO.
- The engineering specialists (backend, frontend, product-engineer) execute. The reviewer, refactoring, QA, and security agents provide quality and risk coverage.

## What each agent produces

| Agent | Typical output |
|---|---|
| Chief of Staff | Session plans, handoffs, contradictions-between-agents log |
| Founder | GO/NO-GO, scorecard, 0→1 roadmap |
| CPO | PRD-Lite, ICP, validation plan, success metrics |
| CTO | Architecture doc, stack trade-offs, implementation plan |
| CDO | UX flows, wireframes, microcopy, usability checks |
| CMO | README narrative, positioning, demo scripts, launch posts |
| tech-lead | Technical direction inside the product, milestone checkpoints |
| backend-engineer | API, schema, integrations |
| frontend-engineer | Mobile UI, capture flows, state |
| product-engineer | Vertical slices that span UI + data |
| code-reviewer | High-signal review with tradeoff framing |
| refactoring-engineer | Targeted cleanups before or after behavior changes |
| qa-engineer | Risk-weighted test plans and regression coverage |
| security-engineer | Authn/authz, data-boundary, dependency review |

## What is public vs. private

| Public | Private |
|---|---|
| *That* this agent system exists | *How* each agent is prompted |
| *What* each role does at a high level | Raw prompts, heuristics, escalation thresholds |
| *How* the two layers coordinate | Reusable operational skills |

The raw `.claude/agents/*.md` and `.claude/rules/*.md` files are gitignored on purpose. This layered transparency lets the repository show rigorous AI-native product organization without giving away the operating logic that makes it work.

See:
- [`venture-studio-operating-model.md`](venture-studio-operating-model.md) for the studio layer
- [`nutrace-technical-delivery-model.md`](nutrace-technical-delivery-model.md) for the Nutrace technical layer
- [`repository-structure.md`](repository-structure.md) for the full tree
