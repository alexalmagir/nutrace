# Discovery Summary

> Validation methodology and outcomes. Curated public summary derived from the internal validation plan and results document.

---

## Two critical hypotheses

| # | Hypothesis | Result |
|---|---|---|
| H1 | Photo + voice capture reduces friction enough to sustain 7-day logging | ✅ PASS — 14/15 (Round 2) |
| H2 | The structured log is clinically useful to gastroenterologists and dietitians | ✅ PASS — 15/15 unanimous (Round 2) |

Both hypotheses were validated in two rounds of interviews. Phase B closed with a GO to build.

## Methodology

- **Rounds:** two (iterative — second round refined after Round 1 feedback)
- **Patient interviews:** targeted recruitment via digestive-health communities, screened for ICP fit
- **Clinical interviews:** gastroenterologists and registered dietitians, both independent and hospital-affiliated
- **Scoring:** each interview scored on a 5-point rubric per hypothesis; pass threshold preregistered

## User segments identified (6)

| Segment | Description | Core need |
|---|---|---|
| A — Active Diagnosis Seeker | In consultation, no diagnosis yet | First insight in ≤3 days; export prominent |
| B — Self-Investigator | Self-managing, no specialist | Privacy controls; pattern view compelling |
| C — Chronic Follow-up | Confirmed diagnosis, managing long-term | Month-over-month comparison; clean export |
| D — High-Literacy Patient | Clinical or expert user | Fast correction flow; AI accuracy disclosed |
| E — Dismissed Patient | Told "nothing's wrong" despite symptoms | Data as evidence framing |
| F — Prior Diagnosis + Relapse | Had diagnosis, improved, symptoms returned | Prior-diagnosis context field; relapse vs. new vs. misdiagnosis triage |

## Clinical segments identified (6)

Gastroenterologists and dietitians across: hospital-affiliated generalists, private-practice specialists, functional/integrative practitioners, digital-first clinics, academic researchers, and nutrition-focused allied professionals. All six expressed willingness to receive a PDF during consultation.

## Build implications locked in Phase B

- Voice input is optional; photo-only entries must be supported
- Proactive trigger alert fires at photo-capture step, not later
- First insight target: 3 days (not 7) — early signal is a retention driver
- AI correction flow: 2-tap maximum, editable ingredient list before saving
- PDF must include a symptom severity indicator (traffic light or 1–5 scale)
- Check-in prompts at 2h and 4h post-meal for delayed-onset symptoms
- Eating disorder contraindication screen in onboarding
- Optional prior-diagnosis field for Segment F (appears in PDF header)
- Data window: 7 days minimum useful; 14 days default

## Phase C and D continuation

After H1 + H2 passed, the PRD-Lite, UX flows, and technical architecture encoded these decisions. Phase D runs seven additional validation experiments in build.

Full methodology, transcripts, and scoring are in internal documentation.
