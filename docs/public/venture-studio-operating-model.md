# AI Product Builder — Venture Studio Operating Model

> The executive layer that sits above every product in the studio. Nutrace is the first product; this layer is designed to run many.

---

## What the studio is

**AI Product Builder** is a personal agentic studio run by Alexandre Maravilla to build AI-native products end-to-end, in public, with AI tools. The studio lives on the local machine as a meta-workspace; each product is its own GitHub repository.

Think of it as a small, opinionated venture studio whose "partners" are six AI agents, each with a clear role.

## The six executive agents

| Agent | Role | Main artifacts |
|---|---|---|
| **Chief of Staff** | Orchestrates every session. Opens with a plan, closes with a concrete next block. Detects contradictions between agents. | Session plans, decision logs |
| **Founder** | GO / GO-LIMITED / PARK / NO-GO on new ideas. Scores on a 10-criterion rubric. Owns the 0→1 thesis and the 1→100 scaling question. | Venture briefs, scorecards |
| **CPO** | Owns the problem. ICP, JTBD, PRD-Lite, validation plans, success metrics. | PRD-Lite, validation plans, ICP segmentation |
| **CTO** | Owns technical execution across the portfolio. Stack trade-offs, architecture, implementation plan, 1→10→100 evolution. | Tech architecture, implementation plan, stack-decision records |
| **CDO** | Owns UX and research. Happy path, edge cases, wireframes, microcopy, usability checks. | UX flow docs, wireframe packs, user-research notes |
| **CMO** | Converts product + execution into professional signal. Positioning, messaging, READMEs, demo scripts, launch posts. | README narrative, demo script, launch plan |

## How a session runs

1. The studio operator tells **Chief of Staff** the current state (project + phase + any update).
2. Chief of Staff returns a session plan and a list of artifacts.
3. The operator switches into the required agent(s) for the session — the plan tells them which one.
4. Each agent produces a committed artifact (doc, code, decision). No session ends without one.
5. The session closes back at Chief of Staff, which books the next block.

## Sequencing rules

- No CPO without problem framing from the Founder or a prior validated thesis
- No CTO build plan without a scoped MVP from the CPO
- No CMO positioning without something real (PRD + at least one shippable artifact)
- Every artifact must live in GitHub — "if it's not in the repo, it doesn't exist"

## Orchestration phases

| Phase | Name | Lead agents |
|---|---|---|
| A | Ideation / Selection | Founder + CPO + CMO |
| B | Validation | CPO + CDO + CMO |
| C | Definition | CPO + CDO + CTO |
| D | Build | CTO + CPO + CDO |
| E | Launch / Evidence | CMO + Founder + CPO |

## Why this matters for Nutrace

Nutrace is the first product built under this studio. The studio layer stays stable across products; the product-technical layer (eight technical agents inside Nutrace) is replicated per product. This separation is what makes the studio reusable and Nutrace's technical team focused.

See also:
- [`nutrace-technical-delivery-model.md`](nutrace-technical-delivery-model.md) — the product-technical layer
- [`agent-system-overview.md`](agent-system-overview.md) — how the two layers coordinate
- [`ai-product-builder-structure.md`](ai-product-builder-structure.md) — the studio directory layout
