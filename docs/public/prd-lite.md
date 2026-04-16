# PRD-Lite — Public Summary

> Public-safe summary derived from [`docs/04-prd-lite.md`](../04-prd-lite.md). Monetization-sensitive strategy detail is omitted here and remains in the full PRD.

---

## Product statement

Nutrace turns meal photos and 10-second voice notes into a structured symptom log that patients and their gastroenterologist or dietitian can actually use.

## MVP scope (IN)

1. **Meal photo → AI ingredient detection** with a 2-tap correction flow
2. **Proactive trigger alert** — when a photo is taken, warn if any detected ingredient has previously correlated with symptoms
3. **Post-meal voice note** → transcribed into a structured symptom record (voice is optional; photo-only entries supported)
4. **Pattern view** — timeline of meals and symptoms; first insight target: ≤3 days
5. **PDF export** — symptom severity indicator, regulatory disclaimer, prior-diagnosis context field in header when provided
6. **Onboarding** — eating-disorder contraindication screen and optional prior-diagnosis context
7. **Check-in prompts** at 2h and 4h post-meal for delayed-onset symptoms
8. **Symptom nudge** push notification after 2 days without a symptom entry

## MVP scope (OUT)

Professional dashboard/login, barcode scanning, FODMAP analysis, nutritional tracking (calories/macros), social features, wearable integrations, any form of medical advice, and pattern comparison across episodes (Segment F follow-up).

## Non-negotiables

- Nutrace is a data-capture and journaling tool. Not diagnostic. No medical advice.
- PDF export is fully unlocked in MVP (no paywall on clinical value).
- Regulatory disclaimer appears on every PDF.

## Success signals for MVP

| Signal | Threshold |
|---|---|
| Time to first actionable pattern | ≤ 3 days |
| 7-day sustained logging | ≥ 50% of activated users |
| Clinician qualitative feedback on real PDF | ≥ 1 positive review (GO/NO-GO gate for V1.5) |

## Monetization posture (high level)

Free for patients. HCP-facing subscription considered at V1.5, gated on retention evidence. The MVP ships with zero paywall so clinical value is provable before monetization is introduced. See the full PRD for detail.

## Out-of-scope but recorded

- Professional dashboard with login (planned for V1.5 on a clinician subscription)
- DiGA reimbursement path in Germany (Phase 3 option, 2026–2027)
- Patient extended history beyond 90 days (possible low-priority add-on)

Full PRD: [`docs/04-prd-lite.md`](../04-prd-lite.md).
