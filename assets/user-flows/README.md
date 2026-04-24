# Nutrace — User Flow Diagrams (FigJam)

> Visual representation of all 6 Nutrace user flows as navigation diagrams.
>
> **Format:** FigJam flowcharts (Mermaid-based)
> **Phase:** D — Build (updated from Phase C)
> **Source:** Derived from `docs/05-ux-flows-and-wireframes.md` v2.0
> **Updated:** 2026-03-04
>
> **v2.0 changes vs. Phase C diagrams:** Flow 3 includes 3.N3 symptom nudge notification. Flow 5 includes "Generate doctor link" exit path. Flow 6 shows simplified alert detail (counts only, no timeline).

---

## Overview

These diagrams show the screen-level navigation for each user flow defined by the CDO. Each diagram maps all screens, decision points, and navigation paths for a given flow.

They complement the written spec in `docs/05-ux-flows-and-wireframes.md` — the spec defines the layout and content of each screen; these diagrams show how screens connect and what choices the user makes at each step.

---

## Flow Index

| Flow | Description | Screens | FigJam |
|------|-------------|---------|--------|
| Flow 1 — Onboarding | First-use setup: contraindication screen, prior diagnosis field, account creation, permissions | 7 screens + 1 advisory branch | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/3d9a8a89-c4f7-41e9-9218-4496b0e4c88c?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 2 — Meal Log Entry | Core loop: photo → AI detection → ingredient review → optional voice → save | 5 screens + 2 states | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/5d7b726f-a207-43ab-9fd7-cd0d4d82fd36?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 3 — Delayed Symptom Check-in | Push notifications at 2h and 4h post-meal + symptom nudge (2 days without symptoms) → 5-point severity selector → entry appended | 1 screen + 3 notification variants | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/bad954b4-f4bf-4ab3-bb63-72e386e93cdf?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 4 — Pattern View (My Log) | Log history with empty state + 2 data states (< 3 days / pattern surfaced) + ingredient toggle + entry detail modal | 3 screens + ingredient view + empty state | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/cd8c2f39-0e99-4b86-b1ac-35dd4514ba68?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 5 — PDF Export | Export setup (date range, photos, doctor note) → PDF preview → native share OR HCP doctor link | 2 screens + empty state | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/333b571c-d8aa-47f2-aa1b-49f9a094461d?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 6 — Proactive Trigger Alert Detail | Alert detail: counts only (MVP), inline disclaimer, 3 exit paths | 1 screen + 3 exit paths | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/88581b84-8f1a-4bc0-8809-acb34667312c?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 7 — Capture Loop *(showcase)* | Narrative arc: camera → AI detection wow → confident save. Derived from Flow 2 (happy path only). | 5 screens | — |
| Flow 8 — Insight Loop *(showcase)* | Narrative arc: 2h notification → 1-tap check-in → day-3 pattern reveal → user trusts the record. Combines Flow 3 + Flow 4. | 5 screens | — |
| Flow 9 — Clinical Handoff Loop *(showcase)* | Narrative arc: export setup → polished PDF preview wow → confident doctor share. Derived from Flow 5. | 5 screens | — |

> **Showcase note (Flows 7–9):** FigJam diagram links will be added once boards are created. Figma Make prototypes: [Flow 7](https://patio-metal-90671589.figma.site) · [Flow 8](https://snare-drift-10973156.figma.site/) · [Flow 9](https://butter-grass-83569298.figma.site/)

---

## App Structure (for reference)

```
Nutrace (mobile — iOS + Android)
├── Onboarding (first use only)          → Flow 1
│
├── Tab bar (3 tabs, persistent)
│   ├── [Camera] Log — center tab        → Flow 2 (+ Flow 6)
│   ├── [Calendar] My Log                → Flow 4
│   └── [Document] Export                → Flow 5
│
├── Push notifications                   → Flow 3 (2h, 4h, symptom nudge)
└── Entry detail modal                   → Flow 4 (Screen 4.3)
```

---

## Design Constraints Covered by These Flows

All 10 hard constraints from Phase B are addressed in the flows above. Key ones visible in the diagrams:

- **Voice optional:** Flow 2 shows Save always reachable without going through voice note
- **Contraindication mandatory:** Flow 1 has no skip path out of Screen 1.2
- **Trigger alert non-blocking:** Flow 2 State B — Save is always visible alongside the alert card
- **Pattern at 3 days:** Flow 4 — two distinct states based on data threshold
- **Delayed check-in:** Flow 3 — triggered by notification, not by user opening the app
- **Symptom nudge:** Flow 3 — 3.N3 fires when meals logged but no symptoms in 2+ days
- **HCP share link:** Flow 5 — "Generate doctor link" is a distinct exit from the native share sheet

---

## Related Files

- `docs/04-prd-lite.md` — CPO PRD-Lite (Section 8: functional flows)
- `docs/05-ux-flows-and-wireframes.md` — CDO full spec v2.0 with ASCII wireframes and screen descriptions
- `assets/wireframes/README.md` — Figma Make prompts for low-fidelity wireframes
