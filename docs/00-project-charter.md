# Nutrace — Project Charter

**Date:** 2026-02-28
**Decision:** GO ✅
**Phase:** A — Ideation / Selection
**Repo:** `alexalmagir/nutrace` (to be initialized)

---

## What is Nutrace?

Nutrace is a frictionless food and symptom diary for people experiencing undiagnosed or recently diagnosed digestive problems.

Users photograph their meals — a vision AI model detects the ingredients. After eating, they record a 10-second voice note about how they feel. The app surfaces patterns over time in a structured log that the user can share with their gastroenterologist or dietitian.

**One sentence:** Nutrace helps people with digestive problems track what they eat and how they feel — using photos and voice, not forms — so they and their doctor can find the patterns that explain their symptoms.

---

## Naming Decision

**Selected name: Nutrace**

Chosen by CPO + CMO alignment on 2026-02-28.

| Candidate | Rejected reason |
|-----------|----------------|
| GutLog | Functional but generic; no brand potential |
| Gutsy | Too lifestyle-focused; wrong connotation for clinical context |
| PatternLog | Two words, clinical-cold, not memorable |
| Trazr | Generic startup naming, 2015 aesthetic |
| **Nutrace** | ✅ Nutrition + Trace/Rastrear; international; pronounceable; describes the action; clean repo name |

---

## GO Decision

**Decision:** GO with scope restriction.

**Scorecard result:** 43/50 (threshold: 40 = GO). See `docs/01-founder-venture-brief.md` for full scorecard.

**Scope restriction:** The MVP is not a platform. It is a proof of two hypotheses:

1. **Friction hypothesis:** Photo + voice capture reduces friction enough that users sustain daily logging for 7+ consecutive days (vs. industry average ~30% retention at D7 for manual food diary apps).

2. **Clinical value hypothesis:** The structured output (ingredients + symptom timeline) is useful enough that a professional (gastroenterologist or dietitian) would recommend it to a patient.

If either hypothesis fails in validation, the build scope changes before any code is written.

---

## ICP (Ideal Customer Profile)

**Primary user:**
- Age 20–50
- Experiencing recurring digestive symptoms: bloating, abdominal pain, irregular bowel habits, nausea, discomfort post-meal
- Has consulted or is in the process of consulting a gastroenterologist or dietitian
- Suspects a food-related trigger but has no confirmed diagnosis
- Motivated by the impact on daily life and work (IBS patients miss 3.6 work/school days/month [1])

**What they are NOT:** Wellness-motivated users optimizing gut health as a lifestyle habit. Nutrace is a diagnostic support tool, not a wellness app.

**Professionals in the loop:**
- Gastroenterologists
- Registered dietitians / nutritionists

Both use food diaries as a standard clinical instrument. The dietitian is likely the faster early adopter; the gastroenterologist is the higher-value clinical validator.

---

## MVP Scope (v1 — confirmed by CPO)

**In scope:**
- Meal logging via photo → AI ingredient detection (with user correction)
- Post-meal voice note → transcribed symptom record
- Basic pattern view: timeline of meals + symptoms
- Export function: PDF or shareable link for the professional

**Out of scope for MVP:**
- Professional account / dashboard (professionals receive PDF, not app access)
- Barcode scanning
- FODMAP analysis or dietary recommendations
- Nutrition tracking (calories, macros)
- Social features
- Wearable integrations
- Prescription or medical advice of any kind

**Why this scope:** The professional dashboard (B2B) would double the build time. Starting with patient-side only + PDF export validates the core hypotheses without the complexity of a B2B product. If the hypotheses validate, the professional dashboard becomes Week 5–8.

---

## Regulatory Framing

Nutrace is a **data-capture and journaling tool**. It is not a diagnostic tool, does not provide medical advice, and does not make clinical recommendations. All clinical interpretation is performed by the user's healthcare professional.

This framing keeps Nutrace outside Class II medical device territory in the EU (MDR) and US (FDA 21 CFR Part 820). This must be reflected in all UX copy, README, App Store description, and marketing materials.

---

## Technical Approach (preliminary — CTO to develop in `docs/06-tech-architecture.md`)

**Core AI capabilities required:**
- Vision model (GPT-4V or equivalent) for ingredient detection from meal photos
- Speech-to-text (Whisper API or equivalent) for voice note transcription
- Basic NLP for symptom keyword extraction from transcription

**Likely stack:**
- Frontend: React Native (iOS + Android from one codebase) or Next.js PWA
- Backend: Node.js or Python (FastAPI)
- AI: OpenAI API (vision + Whisper)
- Storage: Supabase or Firebase (auth + data)
- Export: PDF generation library

CTO will validate and finalize in `docs/06-tech-architecture.md` after CPO completes `docs/04-prd-lite.md`.

---

## Critical Hypotheses to Validate Before Build

| # | Hypothesis | How to test | Pass criteria |
|---|-----------|------------|---------------|
| H1 | Photo + voice reduces friction enough for 7-day sustained use | Manual experiment: 3 users, WhatsApp + shared folder, 5 days | ≥2/3 complete ≥4/5 days |
| H2 | Professional finds structured log clinically useful | 1 x 15-min call with gastroenterologist or dietitian, show mock dashboard | "Yes, I'd recommend this to patients" |

**Decision rule:** Both hypotheses must pass before writing a line of code. If H1 fails, revisit the capture mechanic. If H2 fails, revisit the professional loop or pivot to direct B2C without the clinical angle.

---

## 4-Week Build Plan

| Week | Focus | Lead | Output |
|------|-------|------|--------|
| 1 | Validate + define | CPO | Validation experiment results, `docs/04-prd-lite.md` |
| 2 | Architecture + UX | CTO + CDO | `docs/06-tech-architecture.md`, `docs/05-ux-flows-and-wireframes.md` |
| 3 | Build MVP | CTO | Working prototype: photo → ingredients → voice → log |
| 4 | Polish + launch | CMO + CDO | Demo, `README.md`, LinkedIn post |

---

## Success Metrics (MVP)

**Product:**
- D7 retention ≥ 50% (vs. ~30% category average for manual food diary apps)
- Avg meals logged per active user per day ≥ 2
- ≥ 1 professional recommendation or validation (qualitative)

**Builder signal:**
- GitHub repo public with all docs by Week 1
- Working demo video by Week 4
- LinkedIn post published with ≥ 50 reactions

---

## Open Questions for Next Session (CPO)

1. What is the exact user journey from "first open" to "first useful pattern"? How many days of data does the professional need to make the consultation useful?
2. What is the minimum viable pattern view? (Simple timeline? Heatmap? Symptom correlation chart?)
3. What symptom dimensions should be tracked? (Pain scale 1–5, specific symptoms like bloating/nausea/urgency, stool type via Bristol Scale?)

---

## Agents Involved in This Decision

| Agent | Input |
|-------|-------|
| Chief of Staff | Session orchestration, GO decision framing |
| Founder | Market research, scorecard, risk analysis |
| CMO + CPO | Name selection (Nutrace chosen over GutLog, Gutsy, PatternLog) |

---

## Sources

[1] American Gastroenterological Association (AGA). "IBS in America: Despite advances, IBS remains a burden for many millions." 2024 survey, n=2,013 patients + 600 HCPs. https://gastro.org/press-releases/ibs-in-america-despite-advances-ibs-remains-a-burden-for-many-millions/

[2] Healio. "Striking change: Prevalence of IBS nearly doubled during COVID-19 pandemic." 2025. https://www.healio.com/news/gastroenterology/20250820/striking-change-prevalence-of-ibs-nearly-doubled-during-covid19-pandemic

[3] Gutivate. "Symptom and Food Tracking Apps for IBS — competitive landscape." https://gutivate.com/blog/apps

[4] Nature. "Global evolution of inflammatory bowel disease across epidemiologic stages." 522 population-based studies, 82 global regions (1920–2024). https://www.nature.com/articles/s41586-025-08940-0
