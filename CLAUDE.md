# Nutrace — Project Context for Claude

> This file is the project-level memory for Claude. Read it at the start of every session before doing any work on Nutrace.

---

## What is Nutrace?

Nutrace is a **frictionless food and symptom diary** for people experiencing undiagnosed or recently diagnosed digestive problems (IBS, IBD, food intolerances, GERD).

Users photograph their meals → a vision AI detects ingredients → if any detected ingredient has previously correlated with symptoms, the app warns the user before they eat. After eating, they record a short voice note about how they feel (optional). The app surfaces patterns over time in a structured log that the user can share with their gastroenterologist or dietitian.

**One sentence:** Nutrace warns you before you eat a trigger food — and gives your doctor the structured log to act on it.

---

## Current Status

| Field | Value |
|-------|-------|
| Phase | **D — Build** |
| Decision | **GO ✅** (Founder scorecard: 43/50) |
| Repo | `alexalmagir/nutrace` |
| Branch | `main` |
| Last session | 2026-03-03 (Session 005) |
| Next step | Alex confirms CTO stack decisions → Week 1 build begins (backend skeleton + mobile onboarding) |

**Phase history:**

- Phase A ✅ — GO decision (43/50), ICP defined, name chosen
- Phase B ✅ — H1 PASS (14/15), H2 PASS (15/15), 6 user segments + 6 clinical segments defined
- Phase C ✅ — PRD-Lite done (docs/04), UX flows + wireframes spec done (docs/05), FigJam diagrams + Figma Make prompts done
- Phase D 🔄 — Tech architecture done (docs/06), implementation plan done (docs/07) — awaiting Alex sign-off + Week 1 build start

---

## ICP (Who We're Building For)

**Primary user:**

- Age 20–50, recurring digestive symptoms (bloating, abdominal pain, irregular bowel, nausea)
- Currently consulting or about to consult a gastroenterologist or dietitian
- Suspects food-related triggers — **no confirmed diagnosis yet**
- Motivated: symptoms affect daily work and life (IBS patients miss 3.6 days/month)

**NOT the target user:** Wellness/lifestyle users optimizing gut health. Nutrace is a diagnostic support tool.

**Professionals in the loop:** gastroenterologists + registered dietitians. Both receive data via PDF export (not app login — that's V2).

**User segments (Phase B — 6 defined):**

| Segment | Who | Key need |
| --- | --- | --- |
| A — Active Diagnosis Seeker | In consultation, no diagnosis yet | First insight in ≤3 days; export prominent |
| B — Self-Investigator | Self-managing, no specialist | Privacy controls; pattern view compelling |
| C — Chronic Follow-up | Confirmed diagnosis, managing long-term | Month-over-month comparison; clean export |
| D — High-Literacy Patient | Healthcare professional or expert user | Fast correction flow; AI accuracy disclosed |
| E — Dismissed Patient | Told "nothing's wrong" despite symptoms | Data as evidence framing |
| F — Prior Diagnosis + Relapse | Had diagnosis, improved, symptoms returned | Prior diagnosis context field; tripartite question: relapse / new condition / misdiagnosis |

---

## MVP Scope (What We Build)

**IN scope:**

- Meal photo → AI ingredient detection (with user correction flow)
- **Proactive trigger alert:** when photo is taken, app warns if any detected ingredient has previously correlated with symptoms
- Post-meal voice note → transcribed symptom record (voice optional — photo-only entries supported)
- Pattern view: timeline of meals + symptoms (first insight target: ≤3 days)
- Export: PDF with symptom severity indicator (traffic light / 1–5 scale) + regulatory disclaimer
- Onboarding: eating disorder contraindication screen + optional prior diagnosis context field (Segment F)

**OUT of scope for MVP:**

- Professional dashboard / login
- Barcode scanning
- FODMAP analysis or dietary recommendations
- Nutrition tracking (calories, macros)
- Social or community features
- Wearable integrations
- Medical advice or diagnosis
- Pattern comparison view across episodes (Segment F — future feature)

---

## Critical Hypotheses (must validate before building)

| # | Hypothesis | Result |
| --- | --- | --- |
| H1 | Photo + voice reduces friction enough for 7-day sustained logging | ✅ PASS — 14/15 (Round 2) |
| H2 | Structured log is clinically useful to professionals | ✅ PASS — 15/15 unanimous (Round 2) |

**Phase B complete. Both hypotheses validated. Proceed to build.**

Full methodology, interview transcripts, and segmentation: `docs/03-validation-plan-and-results.md`

**Key build implications from Phase B (must inform PRD and architecture):**

- Voice input optional — photo-only entries must work
- First insight target: 3 days (not 7) — early signal = retention driver
- Proactive trigger alert fires at photo-capture step
- AI correction flow: 2-tap max, editable ingredient list before saving
- PDF must include symptom severity indicator (traffic light or 1–5 scale)
- Delayed symptom onset support: check-in prompts at 2h and 4h post-meal
- Eating disorder contraindication screen in onboarding
- PDF regulatory disclaimer on every export
- Segment F: optional prior diagnosis context field in onboarding (appears in PDF header)
- Data window: 7 days minimum useful; 14 days default

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
│   ├── 03-validation-plan-and-results.md ← CPO ✅
│   ├── 04-prd-lite.md          ← CPO ✅
│   ├── 05-ux-flows-and-wireframes.md ← CDO ✅
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
│   ├── user-flows/             ← FigJam navigation diagrams (6 flows) ✅
│   ├── wireframes/             ← Figma Make prompts (6 flows) ✅
│   └── social/
└── .github/workflows/          ← CI (CTO, Week 3)
```

---

## Agent Team

| Agent | Role | Status |
| --- | --- | --- |
| Chief of Staff | Session orchestration, sequencing | Active |
| Founder | GO decision, market thesis | ✅ Done — Phase A |
| CPO | PRD, ICP, hypotheses, metrics | ✅ Done — docs/03 + docs/04 committed |
| CDO | UX flows, wireframes | ✅ Done — docs/05, FigJam diagrams, Figma Make prompts committed |
| CTO | Architecture, implementation plan, code | 🔄 Active — docs/06 + docs/07 produced |
| CMO | Positioning, README, LinkedIn | Phase E |

---

## Key Decisions Log (summary)

| Date | Decision | Made by |
| --- | --- | --- |
| 2026-02-28 | Project name: Nutrace | CMO + CPO |
| 2026-02-28 | Phase A: GO (43/50) | Founder |
| 2026-02-28 | MVP scope: patient-only, PDF export | Chief of Staff + CPO |
| 2026-02-28 | ICP: undiagnosed/in-diagnosis, not wellness | CPO |
| 2026-02-28 | Professionals: gastro + dietitian via PDF | CPO |
| 2026-03-01 | Voice input optional (photo-only entries supported) | CPO + CDO — Phase B |
| 2026-03-01 | Proactive trigger alert added to capture flow | CPO + CDO — Phase B |
| 2026-03-01 | First insight target: 3 days (not 7) | CPO — Phase B |
| 2026-03-01 | PDF must include symptom severity indicator | CPO — Phase B |
| 2026-03-01 | Eating disorder contraindication screen in onboarding | CPO — Phase B |
| 2026-03-01 | Segment F added: prior diagnosis + relapse | Alex — validated with real users |
| 2026-03-02 | Monetization: Free for patients, HCP portal subscription ($39/mo) at V1.5 | CPO + CMO |
| 2026-03-02 | MVP ships with zero paywall — PDF export fully unlocked | CPO + CMO |
| 2026-03-02 | DiGA certification (Germany) flagged as Phase 3 option (2026–2027) | CPO |
| 2026-03-03 | Stack: React Native + Expo, FastAPI, Supabase (EU region), GPT-4o Vision, Whisper, WeasyPrint, Railway | CTO |
| 2026-03-03 | Photo storage: cloud (Supabase Storage, EU region) — not on-device | CTO |
| 2026-03-03 | Pattern algorithm: ≥3 days data, ≥60% correlation, ≥2 symptomatic entries | CTO |
| 2026-03-03 | Multi-tenancy (hcp_links table) designed in from day 1; HCP portal UI ships at V1.5 | CTO |
| 2026-03-03 | Build plan: 6 weeks to private beta (3 real users, 3+ days logging) | CTO |

---

## Monetization Decision

Strategy: Free for patients, subscription for HCPs (B2B2C)

| Phase | Model | Timing |
| ------ | ----- | ------ |
| MVP (V1) | Fully free — no paywall, no payment infrastructure | Phase D (now) |
| V1.5 | HCP portal subscription: $39/month per clinician, $349/year | Post D7 retention validation |
| V1.5 add-on | Patient extended history: $2.99/month beyond 90-day log | Low priority; signal-dependent |
| Phase 3 | DiGA certification (Germany) — insurance reimbursement ~€400–600/year | 2026–2027 evaluation |

**One-line decision:** "Free for patients, subscription for clinicians — Nutrace earns money when it delivers clinical value, not before."

**Non-negotiable for MVP:** PDF export must be fully unlocked. Gating it behind a paywall contradicts the clinical value proposition.

**CTO note:** Data model must support patient → clinician linking (multi-tenancy) to avoid a rebuild at V1.5, even though the HCP portal UI ships later.

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
