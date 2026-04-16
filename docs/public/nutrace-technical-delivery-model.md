# Nutrace — Technical Delivery Model

> The eight technical agents that build the Nutrace product. Each has a specific role and a clear escalation path to the AI Product Builder CTO.

---

## Design intent

The Nutrace technical team is deliberately structured like a small, high-signal engineering org:

- One **technical lead** sets implementation direction inside the product
- Three **delivery roles** write code (backend, frontend, product-engineer)
- Four **quality and risk roles** protect the delivery (code review, refactoring, QA, security)

This mirrors how real product engineering teams work, not how a single coding-assistant chat behaves.

## The eight agents

| Agent | What they do | Escalate to studio CTO when |
|---|---|---|
| **tech-lead** | Owns implementation direction. Translates architecture into milestones. Resolves in-product tradeoffs. | Strategy crosses product boundaries; platform shift is proposed |
| **backend-engineer** | FastAPI, Supabase schema + RLS, integrations (vision, speech, push), PDF generation | A change affects data residency, compliance, or the overall platform posture |
| **frontend-engineer** | React Native + Expo, capture flows, pattern view, PDF-request UI, state management | A UX-level decision conflicts with the PRD-Lite and needs product re-scoping |
| **product-engineer** | Vertical slices across UI + API + data when a feature needs glue | A slice requires changing the product's scope or surfacing a new ICP need |
| **code-reviewer** | High-signal review: correctness, risk, tradeoffs, not style nitpicks | Code review reveals a systemic pattern that should be addressed portfolio-wide |
| **refactoring-engineer** | Targeted cleanups, separated from behavior changes | A refactor would cross architectural boundaries |
| **qa-engineer** | Risk-weighted test plans, regression protection on fragile areas, explicit validation reports | Coverage gaps imply a systemic quality risk |
| **security-engineer** | Authn/authz, data-boundary review, dependency risk, sensitive-area review | A finding changes the product's security posture or implies portfolio-level risk |

## Operating rules (private, summarized here)

All eight agents share a set of internal operating rules covering:

- **Coding standards** — simplicity, reviewability, explicit failure handling
- **Architecture** — boundaries, evolution over rewrite, local-vs-strategic decisions
- **Testing** — risk-weighted, deterministic, explicit validation reporting
- **Migrations** — additive first, rollback-aware, downtime made visible
- **Security** — least privilege, validated input, secret hygiene, escalation criteria
- **Delivery** — small increments, narrow diffs, visible tradeoffs

The raw rules files are gitignored — see [`PUBLISHING_POLICY.md`](../../PUBLISHING_POLICY.md).

## Escalation chain

```
  Nutrace product team
  ────────────────────
  backend / frontend / product-eng
           │
           ▼
       tech-lead (Nutrace)
           │
           ▼   (for strategic or cross-product decisions)
       CTO (AI Product Builder studio)
```

The tech-lead handles everything local to Nutrace. Strategic calls — platform shifts, build-vs-buy, portfolio-wide architecture patterns, severe security posture changes — escalate to the studio CTO.

## Why this is public

Describing *that* this structure exists and *what each role does* is portfolio-grade signal: it shows AI-native product delivery organized like a real engineering team, not a single chat thread. The raw agent definitions are kept private — exposing them would make the operating logic trivially clonable.

See also:
- [`agent-system-overview.md`](agent-system-overview.md) — how both layers coordinate
- [`venture-studio-operating-model.md`](venture-studio-operating-model.md) — the executive layer above
- [`nutrace-structure.md`](nutrace-structure.md) — where these agents live in the repo
