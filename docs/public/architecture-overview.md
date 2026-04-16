# Architecture Overview

> Curated public summary derived from internal technical architecture and implementation plan documents.

---

## Principles

1. **Simplest thing that demonstrably works.** Proven managed services over bespoke infra.
2. **EU-first data residency.** All patient data stored in EU regions from day one.
3. **Designed for multi-tenant HCP linking.** Schema supports patient → clinician relationships in the MVP even though the HCP portal UI ships at V1.5.
4. **Ship in small increments.** Narrow diffs, visible risk, shippable checkpoints every few days.
5. **Regulatory-safe by construction.** Copy and behavior never imply diagnosis; disclaimers on every export.

## Logical architecture

```
┌────────────────────────────────────────────────────────────┐
│  Mobile client (React Native + Expo — iOS & Android)       │
│   ├── Capture (camera, voice)                              │
│   ├── Pattern view + timeline                              │
│   └── PDF request                                          │
└────────────────────────────────────────────────────────────┘
                           │ HTTPS / auth
                           ▼
┌────────────────────────────────────────────────────────────┐
│  API layer (FastAPI on Railway)                            │
│   ├── /meals (photo upload → vision inference)             │
│   ├── /notes (voice upload → Whisper transcription)        │
│   ├── /patterns (correlation over user history)            │
│   ├── /export (PDF via WeasyPrint)                         │
│   └── /hcp-links (patient ↔ clinician — prep for V1.5)     │
└────────────────────────────────────────────────────────────┘
                           │
    ┌──────────────────────┼──────────────────────────┐
    ▼                      ▼                          ▼
┌──────────────┐   ┌───────────────────┐   ┌──────────────────┐
│ Supabase     │   │ OpenAI / Gemini   │   │ Push / nudges    │
│ (Postgres +  │   │ (GPT-4o Vision,   │   │ (Expo Push)      │
│  Auth +      │   │  Whisper)         │   │                  │
│  Storage,    │   └───────────────────┘   └──────────────────┘
│  EU region)  │
└──────────────┘
```

## Stack decisions

| Layer | Choice | Rationale |
|---|---|---|
| Mobile | React Native + Expo | Single codebase iOS+Android, OTA updates, fast feedback |
| Backend | FastAPI (Python) | Fastest path to ship; rich ecosystem for vision/audio adapters |
| Vision AI | GPT-4o Vision | Highest accuracy on mixed-dish ingredient detection at MVP stage |
| Speech-to-text | OpenAI Whisper API | Proven quality for short-form voice notes |
| DB + Auth + Storage | Supabase (EU region) | One managed provider covers three needs; RLS for tenant isolation |
| PDF generation | WeasyPrint | Deterministic HTML-to-PDF with designer-friendly templates |
| Hosting | Railway | Zero-ops Python hosting for the MVP |

## Data model highlights

- `users`, `meals`, `ingredients` (detected + user-corrected), `symptom_entries`, `patterns`, `exports`
- `hcp_links` table present from day 1 — patient ↔ clinician relationship prep for V1.5
- Photos stored in Supabase Storage (EU region), not on-device — enables reprocessing as vision models improve

## Pattern detection

MVP algorithm: fires a pattern for a given ingredient when the user has ≥3 days of data, ≥60% correlation with a symptom, and ≥2 symptomatic entries. Tunable. Future versions can layer ML on top once enough anonymized data exists.

## Regulatory / privacy posture

- Data residency: EU region on Supabase
- No PHI shared with model providers beyond what is required for inference
- Every PDF export carries the regulatory disclaimer (not diagnostic; for informational purposes)
- Photo storage is opt-out-able; roadmap item for patient data export and deletion

## Build plan (high level)

| Week | Focus | Shippable |
|---|---|---|
| 1 | Backend skeleton + mobile onboarding | Auth flow, schema, basic capture |
| 2 | Vision + voice loop | Photo → detected ingredients → voice-note flow |
| 3 | Pattern view + PDF export | First insight in ≤3 days; signed PDF link |
| 4 | Beta polish + HCP share | Push notifications; HCP share link (no login) |

Beta success gate = one clinician's qualitative review of a real patient's PDF. That review is the GO/NO-GO for V1.5 investment.

Full architecture and implementation plan are in internal documentation.

## UX designs

High-fidelity screens are generated with Figma Make from the prompts in [`assets/wireframes/`](../../assets/wireframes/README.md).

| Flow | Status | Link |
|---|---|---|
| Flow 1 — Onboarding | ✅ Done | [Figma Make](https://claim-manage-96224058.figma.site/) |
| Flow 2 — Meal Log Entry | Pending | — |
| Flow 3 — Delayed Symptom Check-in | Pending | — |
| Flow 4 — Pattern View / My Log | Pending | — |
| Flow 5 — PDF Export | Pending | — |
| Flow 6 — Trigger Alert Detail | Pending | — |
