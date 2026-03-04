# Nutrace — Implementation Plan

**Document:** docs/07-implementation-plan.md
**Version:** 1.0
**Date:** 2026-03-03
**Phase:** D — Build
**Author:** CTO (AI agent)
**Signed off by:** Alexandre Maravilla — pending
**Status:** Draft

**Inputs:**
- `docs/06-tech-architecture.md` — stack decisions, data model, API design

---

## 1. Build Overview

**Target:** Private beta (internal dogfood) in 6 weeks.
**Team:** 1 developer (Alexandre) + AI pair programming.
**Methodology:** Weekly milestones, each ending with a deployed artifact. No sprint ceremonies.

**Definition of private beta:** A working iOS + Android build that completes all 6 UX flows end-to-end with real data. Minimum 3 real users logging for 3+ days before any wider distribution.

---

## 2. Repository Structure

```
nutrace/
├── CLAUDE.md
├── README.md
├── docs/
│   └── ... (all planning docs)
│
├── backend/                     ← FastAPI
│   ├── app/
│   │   ├── main.py              ← FastAPI app, middleware, router registration
│   │   ├── config.py            ← env vars, settings (Pydantic BaseSettings)
│   │   ├── database.py          ← Supabase client init
│   │   ├── auth/
│   │   │   └── middleware.py    ← JWT validation
│   │   ├── meals/
│   │   │   ├── router.py        ← /meals endpoints
│   │   │   ├── schemas.py       ← Pydantic request/response models
│   │   │   ├── service.py       ← business logic
│   │   │   └── detector.py      ← GPT-4o Vision call
│   │   ├── symptoms/
│   │   │   ├── router.py
│   │   │   └── service.py
│   │   ├── patterns/
│   │   │   ├── router.py
│   │   │   ├── engine.py        ← pattern algorithm
│   │   │   └── trigger.py       ← trigger alert check
│   │   ├── voice/
│   │   │   └── transcriber.py   ← Whisper API call
│   │   ├── pdf/
│   │   │   ├── router.py
│   │   │   ├── generator.py     ← WeasyPrint render
│   │   │   └── template.html    ← PDF HTML/CSS template
│   │   └── notifications/
│   │       ├── scheduler.py     ← APScheduler setup
│   │       └── sender.py        ← Expo Push API call
│   ├── tests/
│   │   ├── test_detector.py
│   │   ├── test_patterns.py
│   │   └── test_pdf.py
│   ├── Dockerfile
│   ├── requirements.txt
│   └── .env.example
│
├── mobile/                      ← React Native + Expo
│   ├── app/                     ← Expo Router (file-based routing)
│   │   ├── (onboarding)/
│   │   │   ├── welcome.tsx
│   │   │   ├── contraindication.tsx
│   │   │   ├── prior-diagnosis.tsx
│   │   │   ├── account.tsx
│   │   │   ├── permissions.tsx
│   │   │   └── first-meal.tsx
│   │   ├── (tabs)/
│   │   │   ├── log.tsx          ← camera tab (Flow 2)
│   │   │   ├── my-log.tsx       ← pattern view (Flow 4)
│   │   │   └── export.tsx       ← PDF export (Flow 5)
│   │   ├── modals/
│   │   │   ├── ingredient-review.tsx
│   │   │   ├── trigger-detail.tsx
│   │   │   ├── symptom-checkin.tsx
│   │   │   └── entry-detail.tsx
│   │   └── _layout.tsx
│   ├── components/
│   │   ├── IngredientList.tsx
│   │   ├── TriggerAlert.tsx
│   │   ├── PatternCard.tsx
│   │   ├── SeverityPicker.tsx
│   │   └── VoiceRecorder.tsx
│   ├── lib/
│   │   ├── api.ts               ← API client (fetch wrapper)
│   │   ├── supabase.ts          ← Supabase client
│   │   └── notifications.ts     ← Expo push token registration
│   ├── store/
│   │   └── auth.ts              ← Zustand auth store
│   ├── package.json
│   ├── app.json
│   └── .env.example
│
└── .github/
    └── workflows/
        ├── backend-ci.yml       ← pytest on PR
        └── mobile-ci.yml        ← expo build check on PR
```

---

## 3. Environment Setup (Week 0 — Before Day 1)

### Backend

```bash
# Prerequisites: Python 3.12, pip
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# .env (copy from .env.example)
SUPABASE_URL=https://xxx.supabase.co
SUPABASE_SERVICE_KEY=...        # service role key (backend only)
OPENAI_API_KEY=...
EXPO_ACCESS_TOKEN=...           # for push notifications
ENVIRONMENT=development
LOG_LEVEL=INFO
```

**requirements.txt (core):**
```
fastapi==0.115.0
uvicorn[standard]==0.32.0
pydantic-settings==2.6.0
supabase==2.10.0
openai==1.57.0
weasyprint==62.3
apscheduler==3.10.4
structlog==24.4.0
rapidfuzz==3.10.0
pytest==8.3.0
httpx==0.28.0           # for testing FastAPI
pytest-asyncio==0.24.0
```

### Mobile

```bash
# Prerequisites: Node.js 22, bun (or npm)
cd mobile
bun install

# .env
EXPO_PUBLIC_API_URL=http://localhost:8000
EXPO_PUBLIC_SUPABASE_URL=https://xxx.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=...

# Run
npx expo start
```

**Key packages:**
```json
{
  "expo": "~52.0.0",
  "react-native": "0.76.x",
  "expo-camera": "~16.0.0",
  "expo-av": "~15.0.0",
  "expo-notifications": "~0.29.0",
  "expo-file-system": "~18.0.0",
  "expo-router": "~4.0.0",
  "@supabase/supabase-js": "^2.46.0",
  "zustand": "^5.0.0"
}
```

### Supabase Setup (one-time)

1. Create project in Supabase dashboard, EU region (Frankfurt)
2. Run schema SQL from Section 7.1 of docs/06
3. Enable RLS on all tables, create RLS policies
4. Enable Apple + Google OAuth in Supabase Auth
5. Create storage bucket `photos` (private, per-user path: `{user_id}/`)
6. Create storage bucket `exports` (private, per-user path: `{user_id}/`)

---

## 4. Weekly Milestones

### Week 1 — Foundation + Auth

**Goal:** Working API skeleton with auth; photo upload to Supabase; end-to-end onboarding flow (Screens 1.1–1.7) on mobile.

**Backend tasks:**
- [ ] FastAPI project structure, `main.py`, middleware (CORS, JWT validation)
- [ ] Supabase client setup (`database.py`), connection test
- [ ] Schema migration: run SQL from docs/06 Section 7.1
- [ ] `POST /meals` — create meal entry, return entry_id
- [ ] `POST /meals/{id}/save` — mark complete (empty implementation, no notifications yet)
- [ ] Health check endpoint `GET /health`
- [ ] Dockerfile, deploy to Railway (dev environment)

**Mobile tasks:**
- [ ] Expo project init, Expo Router, tab structure
- [ ] Supabase Auth integration: email signup/login (Screens 1.4)
- [ ] Apple SSO + Google SSO (Screen 1.4)
- [ ] Onboarding flow (Screens 1.1–1.7): navigation, screen layouts
- [ ] Prior diagnosis field: stored in Supabase `users.prior_diagnosis` on save
- [ ] Camera permission screen (Screen 1.5): Expo Camera setup
- [ ] Notification permission screen (Screen 1.6): Expo Notifications, register push token
- [ ] Photo upload: capture → compress → Supabase Storage → return photo_url

**Definition of done Week 1:**
- User can create an account, complete onboarding, and have a meal entry created in the database with a photo URL stored in Supabase Storage.
- API deployed to Railway and responding on dev URL.

---

### Week 2 — AI Core

**Goal:** GPT-4o ingredient detection working end-to-end; Whisper voice transcription; pattern algorithm first implementation.

**Backend tasks:**
- [ ] `POST /meals/{id}/detect` — GPT-4o Vision call, structured output, store results in `meal_ingredients`
- [ ] `PUT /meals/{id}/ingredients` — accept final ingredient list after user correction
- [ ] `POST /meals/{id}/voice` — upload voice → Whisper API → return transcription text
- [ ] Pattern engine (`patterns/engine.py`): SQL query, has_sufficient_data check
- [ ] `GET /patterns` — returns current pattern analysis for user
- [ ] `GET /trigger-alert?entry_id={id}` — trigger alert check against patterns
- [ ] Benchmark GPT-4o Vision on 20 real food photos; measure p95 latency and ingredient accuracy

**Mobile tasks:**
- [ ] Screen 2.2 — AI detection loading state (3–5s animation, timeout handling)
- [ ] Screen 2.3 State A — ingredient review (list, [✕] remove, [+ Add])
- [ ] Screen 2.3 State B — trigger alert inline card
- [ ] `IngredientList.tsx` component with confidence badge (Segment D)
- [ ] `TriggerAlert.tsx` component

**Definition of done Week 2:**
- Take a meal photo → AI detects ingredients → shown in app within 5s.
- Correct/remove ingredients → saved to DB.
- If trigger pattern exists (manual test data seeded), alert fires.
- Pattern endpoint returns correct data for a seeded user.

---

### Week 3 — Meal Log Flow + Notifications

**Goal:** Full meal log entry flow (Flow 2) shippable; delayed check-in notifications working (Flow 3).

**Backend tasks:**
- [ ] Notification scheduler: APScheduler in FastAPI, polling `notification_schedule` every 60s
- [ ] `notifications/sender.py`: Expo Push API call
- [ ] On `POST /meals/{id}/save`: insert 2 rows in `notification_schedule` (+2h, +4h)
- [ ] `POST /symptoms`: log symptom entry linked to meal, with offset_hours
- [ ] Test: save meal → wait 2 min (use 2-min test interval) → notification received

**Mobile tasks:**
- [ ] Screen 2.4 — Voice note recorder (Expo AV, max 10s, transcription display)
- [ ] Screen 2.5 — Entry saved confirmation, day counter, progress message
- [ ] Flow 3 — Notification tap → Screen 3.1 (Quick Symptom Entry)
- [ ] `SeverityPicker.tsx` — 5-emoji selector
- [ ] `VoiceRecorder.tsx` — record, stop, playback, re-record
- [ ] Deeplink from notification to symptom check-in screen, linked to correct meal entry

**Definition of done Week 3:**
- Full meal log flow works end-to-end: photo → detect → review → optional voice → save → confirmation.
- Notification arrives ~2h after meal save (tested with 2-min test interval).
- Symptom check-in saves correctly and links to the original meal entry.

---

### Week 4 — Pattern View + My Log Tab

**Goal:** My Log tab (Flow 4) fully functional; pattern card shown at ≥3 days of data.

**Backend tasks:**
- [ ] Refine pattern engine: test against seeded 3-day, 7-day, 14-day datasets
- [ ] Ensure pattern computation ≤500ms for 30-day window
- [ ] `GET /meals` — paginated meal entries with linked symptom entries

**Mobile tasks:**
- [ ] Screen 4.1 — My Log, <3 days state: list of entries + progress card
- [ ] Screen 4.2 — Pattern surfaced: pattern card at top, ingredient correlation list
- [ ] Screen 4.2 — Ingredient view toggle (day view / ingredient view)
- [ ] Screen 4.3 — Entry detail modal: full photo, ingredient list (AI-detected label), symptom timeline
- [ ] `PatternCard.tsx` component
- [ ] Screen 6.1 — Trigger Alert Detail (Flow 6): correlation breakdown, timeline
- [ ] Empty states for all My Log states (Section "Empty States" in docs/05)

**Definition of done Week 4:**
- Log entries appear in My Log with photos and symptom data.
- After seeding 3+ days of data with symptom entries, pattern card appears with correct correlation data.
- Entry detail modal shows full data correctly.
- Trigger alert detail screen shows historical correlation breakdown.

---

### Week 5 — PDF Export

**Goal:** PDF export (Flow 5) working end-to-end; clinical-grade output with traffic light severity.

**Backend tasks:**
- [ ] `pdf/template.html` — HTML/CSS template for WeasyPrint
  - Page 1: header (name, prior_diagnosis if set, date range), symptom overview bar, top patterns
  - Page 2+: daily log per entry (thumbnail if included, ingredient list, symptom entries with emoji)
  - Last page: regulatory disclaimer (hardcoded)
- [ ] `POST /export/pdf` — generate PDF, store in Supabase Storage, return signed URL
- [ ] Test: 14-day PDF with 42 entries + photos generates in ≤3s
- [ ] Cleanup job: delete export files older than 24h

**Mobile tasks:**
- [ ] Screen 5.1 — Export setup: date range picker, photo toggle, doctor note
- [ ] Screen 5.2 — PDF preview: open signed URL in native viewer
- [ ] Share sheet integration: share PDF via email, AirDrop, WhatsApp, Files
- [ ] Export tab empty state (Screen 5 empty state from docs/05)
- [ ] "Time to export?" prompt on day-7 confirmation screen (Screen 2.5)

**Definition of done Week 5:**
- User can generate a PDF for a real 14-day log, preview it in-app, and share via native share sheet.
- PDF includes: patient header, top patterns, daily log with traffic light severity, photo thumbnails, regulatory disclaimer.
- PDF footer disclaimer is always present and cannot be removed.

---

### Week 6 — Polish, Observability, Private Beta

**Goal:** App is stable enough for 3+ real users to dogfood for 7 days.

**Backend tasks:**
- [ ] Structured JSON logging (structlog) on all endpoints
- [ ] Log GPT-4o Vision latency, pattern computation time, PDF generation time
- [ ] `DELETE /account` — GDPR right to erasure (soft delete + Supabase Storage wipe)
- [ ] Error handling: graceful responses for GPT-4o timeout, Supabase errors
- [ ] Rate limiting: 10 requests/min per user on `/detect` (Supabase RLS or middleware)
- [ ] CI: GitHub Actions `backend-ci.yml` running pytest on PR

**Mobile tasks:**
- [ ] Error states: network error, AI timeout, auth expiry
- [ ] Loading states: skeleton screens on My Log and Pattern View
- [ ] Haptic feedback on key interactions (save meal, severity picker)
- [ ] CI: GitHub Actions `mobile-ci.yml` running `expo build --check`
- [ ] Expo EAS: configure development + preview build profiles
- [ ] TestFlight (iOS) + internal track (Android) distribution

**Definition of done Week 6 / Private Beta:**
- 3 real users complete onboarding and log ≥1 meal/day for 3+ days
- Pattern card fires for at least 1 user
- At least 1 PDF exported and shared
- No P0 crashes observed (no force-close on primary flows)
- GPT-4o Vision p95 latency < 5s measured in production

---

## 5. Testing Strategy

### 5.1 Backend Tests (pytest)

| Test | What it covers |
|------|----------------|
| `test_detector.py` | GPT-4o structured output parsing; fallback on timeout/malformed response |
| `test_patterns.py` | Pattern engine with seeded datasets (3-day, 7-day, edge cases: all-negative, all-positive) |
| `test_pdf.py` | WeasyPrint render completes without exception; output is valid PDF bytes |
| `test_trigger.py` | Trigger alert logic: no data → no alert; below threshold → no alert; above threshold → alert |
| `test_notifications.py` | Notification scheduling: 2 rows inserted on meal save; sent flag updated after send |

**CI:** pytest runs on every PR to main. No merge without green CI.

### 5.2 Mobile Testing

- Manual smoke test per flow before each week's milestone is marked done
- No automated mobile tests at MVP — too slow to set up; add Detox at V1.5

### 5.3 AI Accuracy Benchmarking (Week 2)

Before launch: benchmark GPT-4o Vision on 50 diverse food photos:
- 25 home-cooked meals
- 25 restaurant meals (varied cuisines)

Measure:
- Precision: % of detected ingredients that are actually present
- Recall: % of visible ingredients detected
- AI correction rate proxy: % of entries where any ingredient would need correction

**Target: precision ≥70%.** If below threshold, iterate on system prompt before continuing to Week 3.

---

## 6. Decisions Delegated to Alex

Before Week 1 begins, Alex needs to confirm or override:

| Decision | CTO default | Override? |
|----------|-------------|-----------|
| Mobile: React Native + Expo | Confirmed | — |
| Backend hosting: Railway | Confirmed | — |
| Supabase EU region (Frankfurt) | Confirmed | — |
| Photo storage: cloud (not on-device) | Confirmed | — |
| Pattern trigger: ≥3 days + ≥60% correlation | Confirmed | OQ-02 |
| AI accuracy threshold: ≤30% correction rate | Confirmed | OQ-01 |
| PDF language: English only at MVP | Confirmed | OQ-05 |

---

## 7. Post-MVP Backlog (V1.5 — do not build now)

Items intentionally deferred. Data model supports them; UI does not ship at MVP.

| Feature | Effort | When |
|---------|--------|------|
| HCP portal: multi-tenant dashboard | Large | After D7 retention ≥40% validated |
| HCP invite flow (patient → clinician linking) | Medium | V1.5 |
| Segment F comparison view (current vs. prior episode) | Medium | V1.5 |
| Custom export date range (Segment C) | Small | V1.5 |
| Mood/emotional state field (Segment P4) | Small | V1.5 |
| Confidence indicator UI for Segment D | Small | V1.5 — model supports it from day 1 |
| Analytics: PostHog or Mixpanel | Small | V1.5 |
| Manual food entry (no photo) | Medium | V1.5 |
| FODMAP lookup | Large | V2 — separate positioning decision needed |

---

## 8. Commit Convention

```
feat: <what was added>       ← new feature
fix: <what was corrected>    ← bug fix
chore: <maintenance>         ← deps, CI, config
docs: <documentation>        ← planning docs only
test: <test additions>       ← tests only
```

Examples:
```
feat(backend): add GPT-4o Vision ingredient detection endpoint
feat(mobile): implement meal log entry flow (screens 2.1–2.5)
fix(patterns): correct off-by-one in has_sufficient_data day count
chore: add GitHub Actions CI for backend pytest
```

---

## 9. GitHub Handoff Checklist

**Artifacts to commit from Phase D kickoff:**

- [ ] `docs/06-tech-architecture.md` ← this session
- [ ] `docs/07-implementation-plan.md` ← this session
- [ ] `backend/` skeleton (Week 1 kickoff)
- [ ] `mobile/` skeleton (Week 1 kickoff)

**Session rule:** Every session ends with a commit. No session closes with uncommitted work.

---

## Sources

- Architecture decisions: `docs/06-tech-architecture.md`
- UX flow constraints: `docs/05-ux-flows-and-wireframes.md`
- MVP scope: `docs/04-prd-lite.md` Section 6
- Expo documentation: https://docs.expo.dev
- FastAPI documentation: https://fastapi.tiangolo.com
- Supabase documentation: https://supabase.com/docs
