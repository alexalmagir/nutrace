# Nutrace — PRD-Lite

**Document:** docs/04-prd-lite.md
**Version:** 1.0
**Date:** 2026-03-01
**Phase:** C — Definition
**Author:** CPO (AI agent)
**Signed off by:** Alexandre Maravilla
**Status:** Draft — pending CDO (UX flows) and CTO (architecture) review

**Dependencies:**

- Phase A: `docs/00-project-charter.md` — GO decision, scope, ICP
- Phase B: `docs/03-validation-plan-and-results.md` — H1 + H2 results, all build implications

---

## 1. Purpose of This Document

This PRD-Lite defines what Nutrace builds, for whom, why, and to what standard of done — in the minimum scope needed to unblock design (CDO) and architecture (CTO). It is not a full PRD. It does not specify implementation, technology choices, or UI details. Those belong in docs/05 (CDO) and docs/06 (CTO).

This document supersedes any scope statements in CLAUDE.md. It is the single source of truth for Phase D (Build).

---

## 2. Problem Statement

People with digestive disorders (IBS, IBD, GERD, food intolerances) are told to keep food diaries. Almost none sustain it.

**Why the current tools fail:**

- Manual logging is tedious. Recording a meal in MyFitnessPal or a paper diary takes 3–7 minutes. Most people stop within days.
- Forms are designed for nutrition, not symptoms. Fields like "portion size in grams" are irrelevant and alienating.
- Recall is unreliable. Even motivated patients cannot accurately reconstruct what they ate 6 hours ago.
- Data is not actionable. A log of meals with no pattern analysis does not change clinical decisions.
- The professional loop is broken. Even when patients bring notes, they are narrative and incomplete.

**The result:** Patients spend months or years in consultations without the data their doctors need to help them. Average time-to-diagnosis for IBS is 6.6 years. Patients miss 3.6 work days per month. 76% of IBS patients still find symptom management difficult (AGA 2024).

**The opportunity:** If capture friction is removed — photo replaces manual logging, voice replaces text recall — sustained logging becomes feasible. If patterns are surfaced within days (not weeks), the insight loop closes before users abandon. If the output is structured and clinical, professionals can act on it.

**Validated in Phase B:**

- H1 (photo + voice capture is sustainable): 14/15 users — PASS
- H2 (structured log is clinically useful): 15/15 professionals unanimous — PASS

---

## 3. Product Vision (One Sentence)

Nutrace is a frictionless food and symptom diary that warns patients before they eat a known trigger — and gives their doctor a clinical-grade PDF to act on.

---

## 4. Who We Are Building For

### 4.1 Primary ICP

**Age:** 20–50
**Condition:** Recurring digestive symptoms (bloating, abdominal pain, irregular bowel, nausea)
**Status:** Currently consulting — or about to consult — a gastroenterologist or registered dietitian
**Motivation:** Find out what is triggering their symptoms. Get data to their doctor.
**NOT the target:** Wellness users optimizing gut health. Nutrace is a diagnostic support tool, not a lifestyle app.

### 4.2 User Segments

Six segments defined in Phase B. All are in scope for MVP unless noted.

| Segment | Who | Primary need | MVP priority |
| --- | --- | --- | --- |
| A — Active Diagnosis Seeker | Consulting a specialist, no diagnosis yet | First insight ≤3 days; export prominent | Primary |
| B — Self-Investigator | Self-managing, no specialist | Privacy controls; compelling pattern view | Secondary |
| C — Chronic Follow-up | Confirmed diagnosis, long-term management | Month-over-month view; clean export | Secondary |
| D — High-Literacy Patient | Healthcare professional or expert user | Fast AI correction; accuracy disclosed | Secondary |
| E — Dismissed Patient | Told "nothing's wrong" | Data-as-evidence framing | Secondary |
| F — Prior Diagnosis + Relapse | Had diagnosis, improved, symptoms returned | Prior diagnosis context field; tripartite question | Secondary |

**Segment F design note:** Segment F users need an onboarding path that acknowledges prior diagnosis history. They come to the app with a reference point — their known condition — and need to determine whether the recurrence is a relapse, a new condition, or evidence of original misdiagnosis. The MVP delivers an optional "prior diagnosis context" free-text field in onboarding, which is surfaced in the PDF header. Comparison view (current episode vs. prior episode) is a V2 feature.

### 4.3 Professionals in the Loop

Healthcare professionals receive data via PDF. They do not have an account or dashboard in Nutrace. That is V2.

Primary professional segments validated in Phase B:

| Clinical segment | Profile | PDF requirements |
| --- | --- | --- |
| P1 — GI Dietitian | FODMAP / GI nutrition, high tech adoption | Ingredient detail, severity scale, timing |
| P2 — GP / Primary Care | First-contact prescriber, recommends referrals | Simple, clean, no jargon |
| P3 — Specialist Gastroenterologist | Complex cases, time-poor | Full log, severity, timestamp, disclaimer |
| P4 — GI Mental Health | Gut-brain connection cases | Optional mood field; temporal correlation |
| P5 — Multidisciplinary Clinic | Multiple providers share the same data | Patient-identifiable, date-stamped |
| P6 — Researcher | Academic, data quality focus | V2 — CSV/JSON export out of MVP scope |

---

## 5. Jobs to Be Done

| Job | Statement | Priority |
| --- | --- | --- |
| JTBD-01 | When I eat something, I want to record it without interrupting my meal, so I can build a log without it becoming a burden | Core |
| JTBD-02 | When I have a symptom, I want to record how I feel right now, so the timing and severity are captured accurately | Core |
| JTBD-03 | When I have a doctor's appointment, I want to share a structured report, so my doctor can review what I ate and how I felt without relying on my memory | Core |
| JTBD-04 | When the app detects a pattern, I want to be warned before I eat a trigger food, so I can make an informed choice | Core |
| JTBD-05 | When I see my log over time, I want to understand which foods correlate with bad days, so I can test eliminations myself | Secondary |
| JTBD-06 | When I return to Nutrace after a relapse, I want to add context about my prior diagnosis, so my doctor can tell if this is the same condition or something new | Secondary (Segment F) |

---

## 6. MVP Feature Set

### 6.1 In Scope

**Capture**

- Meal photo capture (camera or gallery upload)
- Vision AI ingredient detection from photo (with AI model TBD by CTO)
- AI ingredient detection result shown to user before saving — editable, 2-tap correction, not mandatory to review every item
- Voice note after eating (10 seconds max; transcribed to text)
- Photo-only entries supported — voice is optional per entry
- Delayed symptom check-in: optional push notification at 2h and 4h post-meal ("How are you feeling?")

**Proactive Trigger Alert**

- At photo-capture step: if any detected ingredient has previously correlated with symptoms in the user's log, the app surfaces a warning before the entry is saved
- Warning shows: the flagged ingredient(s), the number of prior symptomatic entries containing it, and a prompt to proceed or adjust
- Does not block logging — alert is informational, not a gate
- Alert is only available once the user has ≥3 days of meal + symptom data

**Pattern View**

- Timeline of meals + symptoms (default 14-day window)
- Each entry shows: date, time, thumbnail photo, detected ingredients, symptom severity (if recorded)
- Pattern surface: "You had symptoms after X of Y meals containing [ingredient]"
- First pattern insight target: ≤3 days of data

**Export**

- PDF export of the full log (7-day minimum; 14-day default)
- PDF includes: date range, photo thumbnails (optional — user controls), ingredient list per meal, symptom log per entry with severity indicator (traffic light: green / amber / red), timestamp correlation
- PDF header includes: user name (optional), prior diagnosis context (if provided in onboarding, Segment F), regulatory disclaimer
- PDF footer disclaimer (non-negotiable): "Nutrace is a data-capture and journaling tool. It does not provide medical advice or diagnosis. All clinical interpretation should be performed by a qualified healthcare professional."

**Onboarding**

- Eating disorder contraindication screen: shown before first use; user confirms they are not using the app for calorie restriction or weight management; if they indicate an eating disorder history, an appropriate advisory is shown before proceeding
- Prior diagnosis context field (optional, Segment F): "Have you previously been diagnosed with a digestive condition? (Optional — helps provide context for your doctor)"
- Regulatory framing in onboarding: "Nutrace is a food and symptom diary. It helps you collect data. It does not give medical advice or diagnoses."

**Accounts and Data**

- User account (email + password, or sign-in with Apple/Google)
- All data stored on device + cloud sync (Supabase — CTO to confirm)
- Data privacy: photo storage disclosed in onboarding; user can delete all data at any time

### 6.2 Out of Scope for MVP

| Feature | Reason |
| --- | --- |
| Professional dashboard / login | V2 — PDF export sufficient per Phase B validation |
| Barcode scanning | Friction reduction in a different direction; camera capture is faster |
| FODMAP analysis | Regulatory risk; adds complexity without core value proof |
| Dietary recommendations | Regulatory risk; out of non-diagnostic framing |
| Nutrition tracking (calories, macros) | Eating disorder risk; out of ICP |
| Social / community features | Scope creep; no Phase B signal |
| Wearable integrations | V2 |
| Pattern comparison view (current vs. prior episode) | Segment F V2 feature — data structure must support it, but UI is V2 |
| CSV / JSON data export | Researcher segment (P6) — V2 |
| Mood / emotional state logging | GI Mental Health segment (P4) signal — future field |

---

## 7. Key Design Constraints

These are requirements derived from Phase B validation, not preferences. CDO and CTO must treat these as hard constraints.

| Constraint | Source | Specification |
| --- | --- | --- |
| Voice is optional | U03, U06, U08 | Every log entry must work with photo-only. The log entry save flow must not require a voice note to proceed. |
| First pattern within 3 days | U07, U11, U12 | The pattern algorithm must surface a first correlation at 3 days of data — not 7. Early signal is the primary retention driver. |
| AI correction is fast | U09, U14, C14 | Ingredient list editable before saving. Maximum 2 taps to remove or replace an ingredient. Auto-suggest based on prior corrections. No confirmation modals. |
| PDF symptom severity is visual | All 15 clinical experts | The PDF must show a traffic light (green / amber / red) or 1–5 scale per entry. Text-only severity is not acceptable to professionals. |
| Delayed symptom onset supported | C05, C15 | Symptom logging must be available beyond the immediate post-meal window. Check-in prompts at 2h and 4h. Pattern algorithm must consider symptom entries logged up to 24h after a meal. |
| Eating disorder screen is mandatory | C10 | Not optional. Must be shown to every user before first use. |
| PDF disclaimer is non-negotiable | C02, C06, C14 | On every PDF. Exact text specified in 6.1. |
| AI ingredient detection disclosed | C03, C11 | Every ingredient list must show "AI-detected — tap to review and correct." Cannot be hidden or dismissed by default. |
| 14-day default log window | C01–C12 | Default PDF export covers 14 days. Users can adjust down to 7. |
| Prior diagnosis context in PDF | U05, U15 | If provided in onboarding, the Segment F context field appears in the PDF header — not buried. |

---

## 8. User Flows (High Level)

Detailed flows with wireframes are owned by CDO in `docs/05-ux-flows-and-wireframes.md`. This section defines the required flows at a functional level.

### Flow 1 — First Use (Onboarding)

1. Welcome screen — product explanation, regulatory framing
2. Eating disorder contraindication screen (mandatory)
3. Prior diagnosis context field (optional, Segment F)
4. Account creation or sign-in
5. Camera permission request with explanation
6. Notification permission request with explanation (for check-in prompts)
7. First meal prompt — "Take a photo of your next meal to get started"

### Flow 2 — Meal Log Entry (Standard)

1. User opens app → taps "Log meal"
2. Camera opens → user takes photo (or selects from gallery)
3. AI detects ingredients → shows ingredient list preview (3–5 seconds)
4. **Proactive trigger alert** fires if flagged ingredients detected
5. User reviews ingredients (optional: tap to edit, add, remove)
6. User saves entry (photo-only path ends here)
7. Optional: user taps microphone → records voice note (≤10 seconds) → transcribed
8. Entry saved → confirmation screen with habit-loop reward (e.g., "Day 3 — keep going, first insight coming soon")

### Flow 3 — Delayed Symptom Check-in

1. Push notification at 2h post-meal: "How are you feeling? Tap to add a quick note."
2. User taps notification → opens simplified symptom entry (severity selector + optional voice/text)
3. Entry appended to the original meal log entry with a 2h timestamp offset

### Flow 4 — Pattern View

1. User navigates to "My Log" tab
2. 14-day calendar-style timeline shown
3. Tapping any day shows meal entries and symptom entries for that day
4. Pattern insight card shown at top when ≥3 days of data: "Bloating appeared after 4 of 5 meals containing [wheat]"
5. User can tap ingredient to see all entries containing it

### Flow 5 — PDF Export

1. User navigates to "Export" tab
2. Date range selector (default: last 14 days; minimum: 7 days)
3. Optional: include/exclude photo thumbnails
4. Optional: add a note to the PDF (e.g., "prepared for Dr. Martínez")
5. Preview PDF before export
6. Export options: share link, email, download
7. PDF includes regulatory disclaimer footer (always, cannot be removed)

### Flow 6 — Proactive Trigger Alert Detail

1. User takes meal photo
2. AI detects ingredient previously correlated with symptoms in ≥2 prior entries
3. Alert shown: "[Ingredient] appeared in your log X times before symptomatic entries. Proceed?"
4. Options: "Continue logging" | "Tell me more" | "Remove ingredient from this entry"
5. Either way, logging is not blocked — the entry saves regardless

---

## 9. Success Metrics (MVP)

**North Star Metric:** 7-day retention rate (% of users who log ≥1 meal per day for 7 consecutive days)
**Target:** ≥40% at 7 days

| Metric | Definition | Target |
| --- | --- | --- |
| Day 3 retention | % of users who log on Day 1, Day 2, and Day 3 | ≥70% |
| 7-day retention | % of users who log ≥1 meal/day for 7 days | ≥40% |
| First pattern surfaced | % of active users who reach the first pattern insight | ≥60% within 5 days |
| Export rate | % of users who export at least one PDF | ≥30% within 30 days |
| Trigger alert interaction | % of users who receive at least one proactive trigger alert and take an action (not ignore) | ≥50% |
| Voice note usage | % of meal entries with a voice note | ≥40% (photo-only tolerated; voice is signal of engagement) |
| AI correction rate | % of ingredient lists where user corrects ≥1 item | ≤30% (lower = higher AI accuracy) |

**Qualitative success signal:** A gastroenterologist or registered dietitian receives a Nutrace PDF from a patient and uses it to change a clinical recommendation.

---

## 10. Regulatory Framing (Non-Negotiable)

Nutrace is a data-capture and journaling tool. It is not a diagnostic tool and does not provide medical advice.

This framing must appear in:

- Onboarding (Flow 1, screen 1)
- Every PDF export footer (exact text in Section 6.1)
- App Store description
- README
- Any marketing copy or press materials

**Why this matters:** This framing keeps Nutrace outside Class II medical device territory under EU MDR Article 2(1) and US FDA 21 CFR Part 880. If Nutrace ever makes diagnostic claims, it would require clinical validation and regulatory approval before distribution. All agents must flag any copy, feature, or UX pattern that implies diagnostic capability.

---

## 11. Risks and Open Questions

### Risks

| Risk | Severity | Mitigation |
| --- | --- | --- |
| AI ingredient detection accuracy below user tolerance threshold | High | Build AI correction flow first; measure correction rate in private beta; iterate on model before full launch |
| Voice note perceived as too intrusive in social eating | Medium | Voice is optional; promote photo-only flow in onboarding |
| Eating disorder contraindication screen creates false negatives (users skip or dismiss it) | Medium | Screen is non-skippable; neutral framing ("this app is not for calorie tracking or weight management") |
| Pattern algorithm does not surface useful insights within 3 days | High | CTO must design minimum viable pattern algorithm that works on 3-day dataset; validate in internal beta before launch |
| PDF too dense for GP use (P2 clinical segment) | Medium | CDO to design a "summary view" PDF tier — 1-page overview + optional full log as appendix |

### Open Questions

| # | Question | Owner | Needed by |
| --- | --- | --- | --- |
| OQ-01 | What is the minimum AI ingredient detection accuracy required before launch? | CTO + CPO | Before build Phase D |
| OQ-02 | Should the proactive trigger alert fire after 3 days of data, or only after a statistically meaningful correlation? | CPO + CTO | Before ML design session |
| OQ-03 | Should the eating disorder contraindication screen block access or only show an advisory? | CPO + CDO | Before UX flows |
| OQ-04 | ~~What is the monetization model for MVP?~~ **RESOLVED (2026-03-02):** MVP ships free (no paywall). V1.5 = HCP portal subscription ($39/month). See `docs/competitive-analysis.md` Section 6. | CPO + CMO | ✅ Done |
| OQ-05 | Does the PDF need to be translated/localized at MVP? Which languages? | CPO + CMO | Before launch |
| OQ-06 | Will Nutrace store photos in the cloud or only on-device? (Privacy and GDPR implications) | CTO + CPO | Before architecture finalized |

---

## 12. Handoff Checklist

| Artifact | Owner | Status |
| --- | --- | --- |
| `docs/04-prd-lite.md` (this doc) | CPO | ✅ Done |
| `docs/05-ux-flows-and-wireframes.md` | CDO | Pending — blocked on this doc |
| `docs/06-tech-architecture.md` | CTO | Pending — blocked on docs/05 |
| `docs/07-implementation-plan.md` | CTO | Pending — blocked on docs/06 |
| `docs/08-decisions-log.md` | All agents | Pending |
| `docs/09-metrics-and-instrumentation.md` | CPO | Pending — blocked on docs/06 |

**Next:** CDO reads this doc and produces `docs/05-ux-flows-and-wireframes.md`, covering all 6 flows defined in Section 8, all 6 user segments, and all design constraints from Section 7.

---

## Sources

- Phase B validation: `docs/03-validation-plan-and-results.md`
- Project charter: `docs/00-project-charter.md`
- Founder venture brief: `docs/01-founder-venture-brief.md`
- Project context: `CLAUDE.md`
- AGA 2024 IBS data: cited in `docs/01-founder-venture-brief.md`
- Segment F validated by Alex Maravilla with real users, 2026-03-01
