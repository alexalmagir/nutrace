# Nutrace — Project Overview

> Elevator pitch + status. Curated public summary derived from the internal project charter.

---

## One sentence

Nutrace warns you before you eat a trigger food — and gives your doctor the structured log to act on it.

## What it is

A frictionless food and symptom diary for people with IBS, IBD, food intolerances, and undiagnosed digestive symptoms. Users photograph meals (vision AI detects ingredients, warns about previously correlated triggers), record a short voice note about how they feel, and export a structured PDF their gastroenterologist or dietitian can act on.

## Why it matters

- 40% of the global population has functional GI disorders
- 76% of IBS patients still find symptom management difficult (AGA 2024)
- IBS patients miss 3.6 work days per month
- Existing food diaries are manual and abandoned within days

## ICP

Adults 20–50 with recurring digestive symptoms, currently consulting or about to consult a gastroenterologist or dietitian, who suspect food-related triggers but do not yet have a confirmed diagnosis. Nutrace is NOT positioned for wellness/gut-health optimization.

## Regulatory framing

Nutrace is a data-capture and journaling tool. It does not diagnose, recommend treatment, or provide medical advice. Clinical interpretation is performed by the user's healthcare professional. This framing keeps Nutrace outside Class II medical device territory.

## Status

| Phase | Status |
|---|---|
| A — Ideation / Selection | ✅ GO (Founder scorecard 43/50) |
| B — Validation | ✅ H1 PASS (14/15), H2 PASS (15/15) |
| C — Definition | ✅ PRD-Lite + UX flows + architecture done |
| D — Build | 🔄 Validation experiments E1–E7 in progress |
| E — Launch | Pending |

## How this repository is organized

This is a public showcase repository. See:

- [`repository-structure.md`](repository-structure.md) for the full tree
- [`agent-system-overview.md`](agent-system-overview.md) for how the AI agent team works
- [`claude-project-context.md`](claude-project-context.md) for how public and private layers are separated
