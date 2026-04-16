# Nutrace

**Frictionless food and symptom diary for people with digestive problems — built in public by a Senior Technical PM using AI tools.**

> Photograph your meal — we'll warn you if it contains something that's triggered your symptoms before. Record how you feel with a voice note. In days, share the pattern with your doctor.

---

## Important Notice

This repository is published as a **showcase and portfolio**, not as open-source software.

- Source code, docs, research, architecture, and design artifacts are **all rights reserved** — see [LICENSE](LICENSE).
- Visible material demonstrates how a Senior Technical PM works end-to-end with AI tools. It is **not** a template you can clone, modify, or use commercially.
- The AI agent system that builds Nutrace is partially private. Raw agent prompts and operational rules are intentionally gitignored — see [`PUBLISHING_POLICY.md`](PUBLISHING_POLICY.md) and [`PUBLIC_PRIVATE_MAP.md`](PUBLIC_PRIVATE_MAP.md).
- Nutrace is a data-capture and journaling tool. It is **not a medical device** and does **not** provide medical advice, diagnosis, or treatment.

---

## Start here

| You want to… | Read |
|---|---|
| Understand the product in one minute | [`docs/public/project-overview.md`](docs/public/project-overview.md) |
| See the market evidence | [`docs/public/market-research-summary.md`](docs/public/market-research-summary.md) |
| See how discovery was run | [`docs/public/discovery-summary.md`](docs/public/discovery-summary.md) |
| See what we're actually building | [`docs/public/prd-lite.md`](docs/public/prd-lite.md) |
| Understand the architecture | [`docs/public/architecture-overview.md`](docs/public/architecture-overview.md) |
| See the AI-native team behind it | [`docs/public/agent-system-overview.md`](docs/public/agent-system-overview.md) |
| See the repository layout | [`docs/public/repository-structure.md`](docs/public/repository-structure.md) |
| See cross-session lessons | [`docs/public/lessons-learned.md`](docs/public/lessons-learned.md) |

Full internal docs live in [`docs/`](docs/) (`00-project-charter.md` through `10-validation-experiments.md`).

---

## The problem

People with IBS, IBD, food intolerances, and undiagnosed digestive symptoms are told to keep a food diary. Almost nobody does it — because logging every meal manually is tedious and they forget to do it mid-symptoms.

The result: months of wasted consultations, delayed diagnoses, and frustrated patients.

**40% of the global population** has functional GI disorders. **76% of IBS patients** still find symptom management difficult (AGA 2024).

---

## What Nutrace does

| Step | What you do | What Nutrace does |
|------|-------------|-------------------|
| Before eating | Take a photo of your meal | Detects ingredients via vision AI — and warns you if the meal contains a known trigger |
| After eating | Record a 10-second voice note | Transcribes and structures your symptoms |
| Over time | Nothing | Learns which foods correlate with your symptoms, surfaces patterns, and powers real-time alerts before you eat |
| At appointment | Tap Export | Generates a structured PDF for your gastroenterologist or dietitian |

**No manual logging. No forms. No friction.**

---

## Who it's for

- Adults 20–50 with recurring digestive symptoms (bloating, abdominal pain, irregular bowel, nausea)
- Currently consulting — or about to consult — a gastroenterologist or registered dietitian
- Motivated: their symptoms affect work and daily life

**Nutrace is a data-capture and journaling tool. It does not provide medical advice or diagnosis.**

---

## Status

| Phase | Status |
|-------|--------|
| A — Ideation / Selection | ✅ GO (Founder scorecard: 43/50) |
| B — Validation (H1 + H2) | ✅ PASSED (H1: 14/15, H2: 15/15) |
| C — Definition (PRD + UX + architecture) | ✅ Done |
| D — Build | 🔄 Validation experiments E1–E7 in progress |
| E — Launch | Pending |

---

## Tech stack

| Layer | Choice |
|-------|--------|
| Mobile | React Native + Expo (iOS + Android) |
| Backend | FastAPI (Python) on Railway |
| Vision AI | GPT-4o Vision |
| Voice/STT | OpenAI Whisper API |
| DB + Auth + Storage | Supabase (EU region) |
| PDF export | WeasyPrint |

See [`docs/public/architecture-overview.md`](docs/public/architecture-overview.md) for the full rationale.

---

## Built in public

Built end-to-end in public — product decisions, architecture, code, and launch — by a Senior Technical PM as a demonstration of 0→1 execution with AI tools.

Every doc, decision, and commit is real work, not a tutorial. Session-by-session log: [`docs/ai-build-log.md`](docs/ai-build-log.md).

**GitHub:** [alexalmagir/nutrace](https://github.com/alexalmagir/nutrace) · **Contact:** alex.almagir@gmail.com
