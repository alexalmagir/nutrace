# Nutrace — Project Context for Claude

> This file is the project-level memory for Claude. Read it at the start of every session before doing any work on Nutrace.

---

## What is Nutrace?

Nutrace is a **frictionless food and symptom diary** for people experiencing undiagnosed or recently diagnosed digestive problems (IBS, IBD, food intolerances, GERD).

Users photograph their meals → a vision AI detects ingredients. After eating, they record a 10-second voice note about how they feel. The app surfaces patterns over time in a structured log that the user can share with their gastroenterologist or dietitian.

**One sentence:** Nutrace helps people with digestive problems track what they eat and how they feel — using photos and voice, not forms — so they and their doctor can find the patterns that explain their symptoms.

---

## Current Status

| Field | Value |
|-------|-------|
| Phase | **A — Ideation / Selection** |
| Decision | **GO ✅** (Founder scorecard: 43/50) |
| Repo | `alexalmagir/nutrace` |
| Branch | `main` |
| Last session | 2026-02-28 |
| Next step | Validate H1 + H2 → CPO writes PRD-Lite |

---

## ICP (Who We're Building For)

**Primary user:**
- Age 20–50, recurring digestive symptoms (bloating, abdominal pain, irregular bowel, nausea)
- Currently consulting or about to consult a gastroenterologist or dietitian
- Suspects food-related triggers — **no confirmed diagnosis yet**
- Motivated: symptoms affect daily work and life (IBS patients miss 3.6 days/month)

**NOT the target user:** Wellness/lifestyle users optimizing gut health. Nutrace is a diagnostic support tool.

**Professionals in the loop:** gastroenterologists + registered dietitians. Both receive data via PDF export (not app login — that's V2).

---

## MVP Scope (What We Build)

**IN scope:**
- Meal photo → AI ingredient detection (with user correction flow)
- Post-meal voice note → transcribed symptom record
- Pattern view: timeline of meals + symptoms
- Export: PDF or shareable link for the professional

**OUT of scope for MVP:**
- Professional dashboard / login
- Barcode scanning
- FODMAP analysis or dietary recommendations
- Nutrition tracking (calories, macros)
- Social or community features
- Wearable integrations
- Medical advice or diagnosis

---

## Critical Hypotheses (must validate before building)

| # | Hypothesis | Test method | Pass criteria |
|---|-----------|------------|---------------|
| H1 | Photo + voice reduces friction enough for 7-day sustained logging | Manual experiment: 3 users, WhatsApp + shared folder, 5 days | ≥2/3 complete ≥4/5 days |
| H2 | Structured log is clinically useful to professionals | 15-min call with gastroenterologist or dietitian + mock dashboard | "Yes, I'd recommend this to patients" |

**Rule:** Both must pass before writing code. If H1 fails → revisit capture mechanic. If H2 fails → pivot away from clinical angle.

---

## Regulatory Framing (NON-NEGOTIABLE)

Nutrace is a **data-capture and journaling tool**. It is NOT a diagnostic tool and does NOT provide medical advice. All clinical interpretation is performed by the user's healthcare professional.

This framing keeps Nutrace outside Class II medical device territory (EU MDR, US FDA). This must appear in all UX copy, README, App Store listing, and marketing.

---

## Naming Decision

**Nutrace** = Nutrition + Trace/Rastrear. Chosen by CPO + CMO on 2026-02-28 over: GutLog, Gutsy, PatternLog, Trazr.

---

## Tech Stack (preliminary — CTO to finalize in docs/06)

| Layer | Approach |
|-------|----------|
| Frontend | React Native (iOS + Android) or Next.js PWA |
| Backend | FastAPI (Python) or Node.js |
| Vision AI | OpenAI GPT-4V or Google Gemini Vision |
| Voice/STT | OpenAI Whisper API |
| Storage | Supabase (auth + DB + storage) |
| Export | PDF generation (WeasyPrint or similar) |

---

## Repo Structure

```
nutrace/
├── CLAUDE.md                   ← this file
├── README.md                   ← public-facing intro
├── docs/
│   ├── 00-project-charter.md   ← GO decision, ICP, scope ✅
│   ├── 01-founder-venture-brief.md  ← scorecard, market data ✅
│   ├── 02-product-problem-icp-jtbd.md   ← CPO (pending)
│   ├── 03-validation-plan-and-results.md ← CPO (pending)
│   ├── 04-prd-lite.md          ← CPO (pending)
│   ├── 05-ux-flows-and-wireframes.md ← CDO (pending)
│   ├── 06-tech-architecture.md ← CTO (pending)
│   ├── 07-implementation-plan.md ← CTO (pending)
│   ├── 08-decisions-log.md     ← all agents (pending)
│   ├── 09-metrics-and-instrumentation.md ← CPO (pending)
│   ├── 10-gtm-and-messaging.md ← CMO (pending)
│   ├── 11-demo-script.md       ← CMO + CDO (pending)
│   ├── 12-retro-and-learnings.md ← end of project
│   ├── 13-scale-1-to-100-hypothesis.md ← all agents
│   └── ai-build-log.md         ← AI session log ✅
├── src/                        ← source code
├── tests/                      ← tests
├── assets/
│   ├── wireframes/
│   └── social/
└── .github/workflows/          ← CI (CTO, Week 3)
```

---

## Agent Team

| Agent | Role | Status |
|-------|------|--------|
| Chief of Staff | Session orchestration, sequencing | Active |
| Founder | GO decision, market thesis | ✅ Done — Phase A |
| CPO | PRD, ICP, hypotheses, metrics | Next up |
| CTO | Architecture, implementation plan, code | Week 2 |
| CDO | UX flows, wireframes | Week 2 |
| CMO | Positioning, README, LinkedIn | Week 4 |

---

## Key Decisions Log (summary)

| Date | Decision | Made by |
|------|----------|---------|
| 2026-02-28 | Project name: Nutrace | CMO + CPO |
| 2026-02-28 | Phase A: GO (43/50) | Founder |
| 2026-02-28 | MVP scope: patient-only, PDF export | Chief of Staff + CPO |
| 2026-02-28 | ICP: undiagnosed/in-diagnosis, not wellness | CPO |
| 2026-02-28 | Professionals: gastro + dietitian via PDF | CPO |

---

## Market Context (key data points)

- 40% of global population has functional GI disorders
- IBS prevalence nearly doubled post-COVID (6.1% → 11%)
- 76% of IBS patients still find symptom management difficult (AGA 2024)
- Patients miss 3.6 work days/month due to IBS (up from 2.1 in 2015)
- Competitors (Cara Care, mySymptoms, Bowelle) are manual food diaries — none use vision + voice AI for capture

---

## Session Rules for Claude

1. **Always read this file first** before any Nutrace work
2. **Never scope-creep** — respect MVP scope. If new ideas arise, log them in `docs/08-decisions-log.md` as "future consideration"
3. **Always cite sources** in any research document
4. **Every session produces an artifact** — no session ends with just discussion
5. **GitHub handoff mandatory** — every response ends with files to commit
6. **Regulatory framing** — never describe Nutrace as diagnostic or medical
