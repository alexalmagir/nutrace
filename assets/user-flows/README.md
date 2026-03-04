# Nutrace — User Flow Diagrams (FigJam)

> Visual representation of all 6 Nutrace user flows as navigation diagrams.
>
> **Format:** FigJam flowcharts (Mermaid-based)
> **Phase:** C — Definition
> **Source:** Derived from `docs/05-ux-flows-and-wireframes.md`
> **Created:** 2026-03-02

---

## Overview

These diagrams show the screen-level navigation for each user flow defined by the CDO in Phase C. Each diagram maps all screens, decision points, and navigation paths for a given flow.

They complement the written spec in `docs/05-ux-flows-and-wireframes.md` — the spec defines the layout and content of each screen; these diagrams show how screens connect and what choices the user makes at each step.

---

## Flow Index

| Flow | Description | Screens | FigJam |
|------|-------------|---------|--------|
| Flow 1 — Onboarding | First-use setup: contraindication screen, prior diagnosis field, account creation, permissions | 7 screens + 1 branch | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/aaa9d987-8b28-4539-9897-79d6b0091755?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 2 — Meal Log Entry | Core loop: photo → AI detection → ingredient review → optional voice → save | 5 screens + 2 states | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/e45a5038-4477-4cad-92a3-06cf036e950f?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 3 — Delayed Symptom Check-in | Push notification at 2h and 4h post-meal → 5-emoji severity selector → entry appended | 1 screen + notification | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/53d4b549-eb1a-466e-ac60-50afd24f15bb?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 4 — Pattern View (My Log) | Log history with two states: default (<3 days) and pattern surfaced (≥3 days) + ingredient toggle + entry detail modal | 3 screens + ingredient view | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/33f647ac-4b3c-4003-b4c7-2b0ba11d5b0d?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 5 — PDF Export | Export setup (date range, photos, doctor note) → PDF preview → native share sheet | 2 screens | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/96abfbc4-8cf6-4d07-b6e8-1d8c736168f3?utm_source=claude&utm_content=edit_in_figjam) |
| Flow 6 — Proactive Trigger Alert Detail | Alert detail screen triggered from Flow 2: correlation stats, symptom timeline, inline disclaimer | 1 screen + 3 exit paths | [Open in FigJam](https://www.figma.com/online-whiteboard/create-diagram/b307ebcc-59b4-411b-8fed-7cc0e315dbdd?utm_source=claude&utm_content=edit_in_figjam) |

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
├── Push notifications                   → Flow 3
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

---

## Related Files

- `docs/04-prd-lite.md` — CPO PRD-Lite (Section 8: functional flows)
- `docs/05-ux-flows-and-wireframes.md` — CDO full spec with ASCII wireframes and screen descriptions
- `assets/wireframes/` — low-fidelity wireframes (to be added in Phase D)
