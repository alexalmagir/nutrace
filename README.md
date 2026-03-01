# Nutrace

**Frictionless food and symptom diary for people with digestive problems — built in public by a Senior Technical PM using AI tools.**

> Photograph your meals. Record a 10-second voice note about how you feel. Let the app find the patterns. Share them with your doctor.

---

## The Problem

People with IBS, IBD, food intolerances, and undiagnosed digestive symptoms are told to keep a food diary. Almost nobody does it — because logging every meal manually is tedious and they forget to do it mid-symptoms.

The result: months of wasted consultations, delayed diagnoses, and frustrated patients.

**40% of the global population** has functional GI disorders. **76% of IBS patients** still find symptom management difficult (AGA 2024).

---

## What Nutrace Does

| Step | What you do | What Nutrace does |
|------|-------------|-------------------|
| Before eating | Take a photo of your meal | Detects ingredients via vision AI |
| After eating | Record a 10-second voice note | Transcribes and structures your symptoms |
| Over time | Nothing | Surfaces patterns: which foods correlate with which symptoms |
| At appointment | Tap Export | Generates a structured PDF for your gastroenterologist or dietitian |

**No manual logging. No forms. No friction.**

---

## Who It's For

- People aged 20–50 with recurring digestive symptoms (bloating, abdominal pain, irregular bowel, nausea)
- Currently consulting — or about to consult — a gastroenterologist or registered dietitian
- Motivated: their symptoms affect work and daily life

**Nutrace is a data-capture and journaling tool. It does not provide medical advice or diagnosis.**

---

## Status

| Phase | Status |
|-------|--------|
| Phase A — Ideation / Selection | ✅ GO (Founder scorecard: 43/50) |
| Phase B — Validation (H1 + H2) | In progress |
| Phase C — Definition (PRD-Lite) | Pending |
| Phase D — Build | Pending |
| Phase E — Launch | Pending |

**Active docs:**
- [Project Charter](docs/00-project-charter.md) — GO decision, ICP, scope
- [Founder Venture Brief](docs/01-founder-venture-brief.md) — market data, scorecard, 0→1 roadmap
- [AI Build Log](docs/ai-build-log.md) — running log of AI-assisted build sessions

---

## Tech Stack (planned)

| Layer | Approach |
|-------|----------|
| Frontend | React Native (iOS + Android) or Next.js PWA |
| Backend | FastAPI (Python) |
| Vision AI | GPT-4V / Gemini Vision |
| Voice/STT | OpenAI Whisper API |
| Storage | Supabase |
| Export | PDF generation |

---

## Built in Public

This project is being built end-to-end in public — product decisions, architecture, code, and launch — by a Senior Technical PM as a demonstration of 0→1 execution with AI tools.

Every doc, decision, and commit is real work, not a tutorial.

**GitHub:** [alexalmagir/nutrace](https://github.com/alexalmagir/nutrace)
