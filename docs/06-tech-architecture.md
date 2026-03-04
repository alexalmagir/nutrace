# Nutrace — Tech Architecture

**Document:** docs/06-tech-architecture.md
**Version:** 1.0
**Date:** 2026-03-03
**Phase:** D — Build
**Author:** CTO (AI agent)
**Signed off by:** Alexandre Maravilla — pending
**Status:** Draft

**Inputs:**
- `docs/04-prd-lite.md` — PRD-Lite (CPO)
- `docs/05-ux-flows-and-wireframes.md` — UX flows and constraints (CDO)
- `docs/competitive-analysis.md` — Section 6.5 monetization implications for CTO
- `CLAUDE.md` — preliminary stack choices + multi-tenancy requirement

---

## 1. CTO Mandate

Produce a minimal, shippable architecture for Nutrace MVP that:

1. Delivers all 6 UX flows defined in docs/05 with the performance targets they require
2. Supports the pattern algorithm at ≤3 days of data — the primary retention driver
3. Is GDPR-compliant by default (photo storage, user deletion, consent)
4. Designs the data model for multi-tenancy (patient → clinician) from day 1, even though the HCP portal ships at V1.5
5. Does not over-engineer — no microservices, no Kubernetes, no MLOps pipeline; this is a two-person build

---

## 2. Open Questions — Resolved by CTO

The CDO surfaced the following open questions in the UX handoff. CTO resolves them here.

| # | Question (from docs/05) | Resolution |
|---|-------------------------|------------|
| AI processing time | Realistic latency for ingredient detection | **Target: ≤5s p95 for GPT-4o Vision call**. Screen 2.2 loading state shows 3–5s. Implement timeout at 8s with graceful fallback (empty ingredient list, user enters manually). |
| Confidence per ingredient | Does the model return confidence per ingredient? | **Yes — prompt-engineered.** GPT-4o structured output returns `"confidence": "high" \| "medium" \| "low"` per ingredient. Show for Segment D (high-literacy). Low-confidence ingredients styled differently on Screen 2.3. |
| Pattern algorithm | Minimum dataset for first correlation | **3 days of data with ≥3 meal entries that each have ≥1 symptom entry.** Correlation threshold: ingredient appears in ≥60% of symptomatic meals, with ≥2 symptomatic entries containing it. See Section 6. |
| Notification system | How 2h/4h post-meal notifications are triggered | **Scheduled notification queued at meal save time.** On `POST /meals/{id}/save`, server schedules two Expo Push notifications: one at `created_at + 2h`, one at `created_at + 4h`. Delivered via Expo Push → APNs/FCM. |
| Data model for Segment F | Does the data model support future comparison view? | **Yes — designed in from day 1.** `prior_diagnosis` field on users table. Meal entries are timestamped. A future "episode" concept (V2) can be layered without schema migration by adding an `episode_id` FK. |
| Photo storage | Cloud vs. on-device? | **Cloud — Supabase Storage (EU region).** Reasons: pattern algorithm runs server-side and needs metadata cross-device; user data must survive phone loss; photos enable future model improvement. GDPR: per-user bucket, user can delete all data including photos at any time. Disclosed in onboarding. |

---

## 3. Stack Decisions

### 3.1 Decision Table

| Layer | Selected | Alternative considered | Rationale |
|-------|----------|------------------------|-----------|
| Mobile | **React Native + Expo** | Flutter, Next.js PWA | Single codebase iOS+Android; Expo simplifies camera, notifications, and OTA updates; larger hiring market than Flutter; PWA has poor camera API support |
| Backend | **FastAPI (Python)** | Node.js + Express | Python native to AI/ML libraries; clean async; Pydantic for request validation; easy Supabase integration |
| Database | **Supabase (PostgreSQL)** | PlanetScale, Neon | Auth + DB + Storage + RLS in one service; Row Level Security handles multi-tenancy; avoids separate auth service |
| Auth | **Supabase Auth** | Clerk, Auth0 | Bundled with DB; handles email + Apple SSO + Google SSO; no additional service cost |
| Storage | **Supabase Storage** | AWS S3, Cloudflare R2 | Same GDPR region config as DB; per-user bucket isolation; RLS policies apply to storage |
| Vision AI | **GPT-4o (structured output)** | Gemini 1.5 Pro Vision | Better ingredient recognition in unstructured food photos; structured output mode returns typed JSON reliably; OpenAI API is more stable for production |
| STT | **OpenAI Whisper API** | Deepgram, AssemblyAI | Best accuracy for short, food/symptom vocabulary; already on OpenAI; no second vendor |
| PDF | **WeasyPrint (Python)** | ReportLab, Puppeteer | HTML+CSS → PDF; easy to maintain the clinical template; runs in FastAPI as a library (no headless browser) |
| Push Notifications | **Expo Push Notifications** | OneSignal, Firebase direct | Native to Expo; wraps APNs and FCM; no extra service |
| Hosting | **Railway (backend) + Expo EAS (mobile)** | Render, Fly.io, Heroku | Railway: simple Dockerfile deploy, built-in Postgres option (not used — using Supabase), env management; EAS: Expo's managed build and OTA |

### 3.2 What is NOT in the stack (deliberate)

- No Redis / message queue — scheduled notifications via Expo Push are sufficient at MVP scale; add if scale demands
- No separate ML model — GPT-4o Vision handles ingredient detection; custom model is a V2 investment if accuracy is insufficient
- No Kubernetes / container orchestration — Railway handles this; revisit at >10k DAU
- No analytics SDK at MVP — use Supabase query logs and basic event table; add PostHog or Mixpanel at V1.5

---

## 4. System Architecture

### 4.1 Component Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                         NUTRACE MVP                                  │
│                                                                       │
│  ┌────────────────────┐         ┌────────────────────────────────┐   │
│  │  React Native App  │         │       FastAPI Backend           │   │
│  │  (Expo)            │         │                                │   │
│  │                    │──REST──▶│  /meals  /symptoms  /patterns  │   │
│  │  Flow 1: Onboard   │◀────────│  /export  /trigger-alert       │   │
│  │  Flow 2: Log meal  │         │                                │   │
│  │  Flow 3: Check-in  │         │  ┌──────────────────────────┐  │   │
│  │  Flow 4: Pattern   │         │  │  Ingredient Detector     │  │   │
│  │  Flow 5: Export    │         │  │  (GPT-4o Vision)         │  │   │
│  │  Flow 6: Alert     │         │  └──────────────────────────┘  │   │
│  └────────────────────┘         │  ┌──────────────────────────┐  │   │
│           │                     │  │  Voice Transcriber       │  │   │
│           │                     │  │  (Whisper API)           │  │   │
│           │Supabase SDK         │  └──────────────────────────┘  │   │
│           ▼                     │  ┌──────────────────────────┐  │   │
│  ┌────────────────────┐         │  │  Pattern Engine          │  │   │
│  │  Supabase          │         │  │  (Python — pure SQL)     │  │   │
│  │                    │◀────────│  └──────────────────────────┘  │   │
│  │  Auth              │         │  ┌──────────────────────────┐  │   │
│  │  PostgreSQL        │         │  │  PDF Generator           │  │   │
│  │  Storage           │         │  │  (WeasyPrint)            │  │   │
│  └────────────────────┘         │  └──────────────────────────┘  │   │
│                                 │  ┌──────────────────────────┐  │   │
│                                 │  │  Notification Scheduler  │  │   │
│                                 │  │  (Expo Push API)         │  │   │
│                                 │  └──────────────────────────┘  │   │
│                                 └────────────────────────────────┘   │
│                                                                       │
│  External APIs: OpenAI (GPT-4o, Whisper)                             │
│  Mobile build: Expo EAS                                              │
│  Backend hosting: Railway                                            │
└─────────────────────────────────────────────────────────────────────┘
```

### 4.2 Data Flow — Meal Log Entry (Flow 2, the critical path)

```
1. User taps [Take photo]
   → App captures image → compresses to ≤2MB JPEG

2. App uploads photo to Supabase Storage
   → POST /storage/v1/object/photos/{user_id}/{entry_id}.jpg
   → Returns public URL (signed, user-scoped)

3. App calls POST /meals
   → Body: { photo_url, created_at }
   → Backend creates meal_entry row, returns entry_id

4. App calls POST /meals/{id}/detect
   → Backend sends photo_url to GPT-4o Vision
   → Prompt: structured output schema (see Section 5.2)
   → Response: [{ name, confidence }] list
   → Backend stores detected ingredients in meal_ingredients table
   → Returns ingredient list to app

5. App calls GET /trigger-alert?entry_id={id}
   → Backend runs pattern check against user's history (see Section 6)
   → Returns: [] or [{ ingredient_name, count_in_log, symptomatic_count }]
   → App renders Screen 2.3 (State A or State B)

6. User reviews ingredients (optional edits)
   → App calls PUT /meals/{id}/ingredients with final list

7. User taps [Save] (or optional: records voice note → POST /meals/{id}/voice → Whisper)
   → App calls POST /meals/{id}/save
   → Backend marks entry as complete
   → Backend schedules Expo Push notifications: +2h and +4h

8. Confirmation screen shown (Screen 2.5)
```

### 4.3 Data Flow — Pattern Computation

```
Pattern computation is NOT real-time on every request.
It runs:
  (a) On GET /patterns — on-demand, cached in memory for 5 min per user
  (b) On meal save — background task, invalidates cache

Pattern cache: in-process dict with TTL (no Redis needed at MVP scale).
At >1k DAU, move to Supabase materialized view or Redis.
```

---

## 5. API Design

### 5.1 Endpoint Inventory

| Method | Path | Description | Auth |
|--------|------|-------------|------|
| POST | `/auth/signup` | Email+password or SSO (delegated to Supabase Auth) | — |
| POST | `/auth/login` | Same | — |
| POST | `/meals` | Create meal entry with photo URL | Required |
| POST | `/meals/{id}/detect` | Trigger GPT-4o ingredient detection | Required |
| PUT | `/meals/{id}/ingredients` | Save final ingredient list after user review | Required |
| POST | `/meals/{id}/voice` | Upload voice note → Whisper transcription | Required |
| POST | `/meals/{id}/save` | Mark entry complete, schedule notifications | Required |
| POST | `/symptoms` | Log symptom entry (linked to meal_entry_id + offset_hours) | Required |
| GET | `/meals` | Get paginated meal entries for current user | Required |
| GET | `/patterns` | Get current pattern analysis | Required |
| GET | `/trigger-alert` | Check if detected ingredients trigger alert | Required |
| POST | `/export/pdf` | Generate PDF, return signed URL | Required |
| DELETE | `/account` | Delete all user data (GDPR right to erasure) | Required |

### 5.2 GPT-4o Prompt and Structured Output Schema

**System prompt:**
```
You are a food ingredient identifier. Given a photo of a meal, identify all visible ingredients.
Return a JSON array only. Do not explain. Do not add ingredients that are not clearly visible.
For each ingredient: use common English name (singular), lowercase.
Assign confidence based on how clearly the ingredient is visible:
  "high" = clearly identifiable, "medium" = likely present, "low" = uncertain.
```

**Structured output schema (OpenAI response_format):**
```json
{
  "type": "json_schema",
  "json_schema": {
    "name": "ingredient_list",
    "schema": {
      "type": "object",
      "properties": {
        "ingredients": {
          "type": "array",
          "items": {
            "type": "object",
            "properties": {
              "name": { "type": "string" },
              "confidence": { "type": "string", "enum": ["high", "medium", "low"] }
            },
            "required": ["name", "confidence"]
          }
        }
      },
      "required": ["ingredients"]
    }
  }
}
```

**Fallback:** If GPT-4o times out (>8s) or returns malformed JSON, return `{ "ingredients": [], "error": "detection_failed" }`. App shows empty ingredient list with "AI couldn't detect ingredients — add them manually." No entry is blocked.

---

## 6. Pattern Algorithm

### 6.1 Requirements

- First correlation surfaced at ≥3 days of logged data with ≥3 meal entries containing at least 1 symptom entry
- Correlation = ingredient appears in ≥60% of meals where symptoms (severity ≥3) were logged within 24h
- Minimum evidence bar: ≥2 symptomatic meal entries containing the ingredient
- Symptom window: any symptom_entry linked to a meal with offset_hours ≤24

### 6.2 Algorithm (Python / SQL)

```python
def compute_patterns(user_id: str, window_days: int = 30) -> list[dict]:
    """
    Returns a ranked list of ingredient-symptom correlations.

    Returns:
        [
          {
            "ingredient": "dairy",
            "total_meals": 5,
            "symptomatic_meals": 4,
            "correlation_rate": 0.80,
            "severity_avg": 3.5,
            "last_seen": "2026-02-28"
          },
          ...
        ]
    """
    # Implemented as a single SQL query with CTEs for performance.
    # See /backend/app/patterns/engine.py

    # Step 1: Get all meal entries + ingredients for user in window
    # Step 2: For each meal, check if any symptom_entry within 24h has severity >= 3
    # Step 3: For each ingredient, count total_meals and symptomatic_meals
    # Step 4: Filter: correlation_rate >= 0.60 AND symptomatic_meals >= 2
    # Step 5: Sort by correlation_rate DESC, symptomatic_meals DESC
```

**Has sufficient data check:**
```python
def has_sufficient_data(user_id: str, min_days: int = 3) -> bool:
    # True if:
    # - User has meal entries spanning >= min_days distinct calendar days
    # - At least min_days entries have at least 1 linked symptom_entry
```

### 6.3 Trigger Alert (at photo capture)

```python
def check_trigger_alert(user_id: str, detected_ingredients: list[str]) -> list[dict]:
    if not has_sufficient_data(user_id):
        return []

    patterns = compute_patterns(user_id)
    pattern_ingredients = {p["ingredient"] for p in patterns}

    alerts = []
    for ingredient in detected_ingredients:
        if ingredient.lower() in pattern_ingredients:
            pattern = next(p for p in patterns if p["ingredient"] == ingredient.lower())
            alerts.append({
                "ingredient": ingredient,
                "total_meals": pattern["total_meals"],
                "symptomatic_meals": pattern["symptomatic_meals"],
                "correlation_rate": pattern["correlation_rate"]
            })

    return alerts
```

**Ingredient matching:** Normalize to lowercase, strip accents. Use fuzzy match for close variants (e.g., "parmesan cheese" → "parmesan"). Library: `rapidfuzz` for Python.

---

## 7. Data Model

### 7.1 Schema

```sql
-- Multi-tenancy note: `hcp_links` table is designed in now; HCP portal UI ships at V1.5.
-- Row Level Security (RLS) policies: all tables scoped to auth.uid().

CREATE TABLE users (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email          TEXT UNIQUE NOT NULL,
  name           TEXT,
  prior_diagnosis TEXT,           -- Segment F: optional free-text (onboarding)
  push_token     TEXT,            -- Expo push token for notifications
  created_at     TIMESTAMPTZ DEFAULT now(),
  deleted_at     TIMESTAMPTZ     -- soft delete for GDPR; hard delete job runs after 30d
);

CREATE TABLE meal_entries (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id        UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  photo_url      TEXT NOT NULL,
  voice_url      TEXT,            -- null if no voice note
  voice_text     TEXT,            -- Whisper transcription
  saved_at       TIMESTAMPTZ,    -- null until POST /meals/{id}/save
  created_at     TIMESTAMPTZ DEFAULT now(),
  -- V2: episode_id UUID REFERENCES episodes(id) -- for Segment F comparison view
  INDEX          (user_id, created_at DESC)
);

CREATE TABLE meal_ingredients (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  meal_entry_id  UUID REFERENCES meal_entries(id) ON DELETE CASCADE NOT NULL,
  name           TEXT NOT NULL,           -- normalized lowercase
  name_display   TEXT NOT NULL,           -- original case for UI
  ai_detected    BOOLEAN DEFAULT true,
  user_corrected BOOLEAN DEFAULT false,   -- true if user edited this ingredient
  confidence     TEXT CHECK (confidence IN ('high', 'medium', 'low')),  -- from GPT-4o
  created_at     TIMESTAMPTZ DEFAULT now(),
  INDEX          (meal_entry_id),
  INDEX          (name)                  -- for pattern query performance
);

CREATE TABLE symptom_entries (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id        UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  meal_entry_id  UUID REFERENCES meal_entries(id) ON DELETE CASCADE,  -- null = standalone
  severity       SMALLINT CHECK (severity BETWEEN 1 AND 5) NOT NULL,
  note_text      TEXT,
  voice_url      TEXT,
  offset_hours   SMALLINT DEFAULT 0,   -- 0 = immediate, 2 = 2h check-in, 4 = 4h
  created_at     TIMESTAMPTZ DEFAULT now(),
  INDEX          (user_id, created_at DESC),
  INDEX          (meal_entry_id)
);

CREATE TABLE trigger_alerts (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id        UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  meal_entry_id  UUID REFERENCES meal_entries(id) ON DELETE CASCADE NOT NULL,
  ingredient_name TEXT NOT NULL,
  action_taken   TEXT CHECK (action_taken IN ('ignored', 'removed', 'viewed_detail', 'continued')),
  shown_at       TIMESTAMPTZ DEFAULT now()
  -- Used for alert efficacy measurement and future model improvement
);

CREATE TABLE notification_schedule (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id        UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  meal_entry_id  UUID REFERENCES meal_entries(id) ON DELETE CASCADE NOT NULL,
  scheduled_for  TIMESTAMPTZ NOT NULL,
  offset_hours   SMALLINT NOT NULL,
  sent           BOOLEAN DEFAULT false,
  sent_at        TIMESTAMPTZ
);

-- V1.5: HCP portal multi-tenancy (schema ready, UI ships later)
CREATE TABLE hcp_links (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  patient_user_id UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  hcp_user_id     UUID REFERENCES users(id) ON DELETE CASCADE NOT NULL,
  consent_given   BOOLEAN DEFAULT false,
  consent_given_at TIMESTAMPTZ,
  access_level    TEXT DEFAULT 'read',   -- 'read' only at V1.5
  created_at      TIMESTAMPTZ DEFAULT now(),
  UNIQUE (patient_user_id, hcp_user_id)
);
```

### 7.2 RLS Policies (Supabase)

```sql
-- Users can only read/write their own data.
-- Applied on all tables. Example for meal_entries:
ALTER TABLE meal_entries ENABLE ROW LEVEL SECURITY;

CREATE POLICY "user_owns_meals" ON meal_entries
  FOR ALL
  USING (auth.uid() = user_id);

-- V1.5: HCP read access via hcp_links join (policy to be added at V1.5 build)
```

---

## 8. PDF Architecture

### 8.1 Template Design

WeasyPrint renders an HTML/CSS template at `/backend/app/pdf/template.html`.

**PDF structure:**
- Page 1: Summary — patient header (name, prior diagnosis if set), date range, symptom overview bar chart (SVG), top patterns ranked
- Page 2+: Daily log — per meal entry: timestamp, photo thumbnail (optional), ingredient list with `AI-detected` label, symptom entries with traffic light emoji
- Last page: Regulatory disclaimer (hardcoded, not configurable)

**Traffic light mapping:**
```
Severity 1-2 → 🟢 green
Severity 3   → 🟡 amber
Severity 4-5 → 🔴 red
```

**Photo inclusion:** Thumbnails are 120×90px JPEG embedded as base64 in the HTML. User can opt out (Screen 5.1) — if opted out, meal entries show ingredient list only.

**Generation time target:** ≤3s for 14-day PDF with photos.

### 8.2 PDF Delivery

- Generated PDF stored temporarily in Supabase Storage (`/exports/{user_id}/{uuid}.pdf`)
- Signed URL returned to app (TTL: 24h)
- App opens native share sheet with the URL
- Cleanup job: delete export files older than 24h

---

## 9. Notification System

### 9.1 Flow

```
1. User saves meal entry → POST /meals/{id}/save
2. Backend inserts 2 rows in notification_schedule:
   { meal_entry_id, scheduled_for: now()+2h, offset_hours: 2 }
   { meal_entry_id, scheduled_for: now()+4h, offset_hours: 4 }
3. Background worker (APScheduler, runs in FastAPI) polls notification_schedule
   every 60 seconds for due notifications (scheduled_for <= now() AND sent = false)
4. For each due notification: call Expo Push API with user's push_token
   Notification body: "How are you feeling {N}h after your [meal time] meal?"
5. Mark notification as sent in notification_schedule
```

**APScheduler** is used as an in-process scheduler (no separate worker). This is acceptable at MVP scale. If concurrency becomes an issue, move to a separate worker process.

**Push token management:** App registers Expo push token on login and on each app open (token can change). Stored in `users.push_token`.

---

## 10. Observability

### 10.1 Metrics to Instrument

| Metric | Why | How |
|--------|-----|-----|
| GPT-4o Vision p95 latency | Core UX constraint (≤5s target) | Log duration on every `/detect` call |
| GPT-4o ingredient accuracy proxy | AI correction rate (target ≤30%) | Count `user_corrected = true` in meal_ingredients |
| Pattern computation time | Should be ≤500ms | Log duration on every `/patterns` call |
| PDF generation time | Should be ≤3s | Log duration on every `/export/pdf` call |
| Notification delivery rate | Check-in capture rate | `sent` field in notification_schedule |
| API error rates | Reliability | FastAPI middleware: log 4xx and 5xx counts by endpoint |

### 10.2 Logging

- Structured JSON logs (Python `structlog`) — each log line includes `user_id`, `request_id`, `endpoint`, `duration_ms`, `status`
- No PII in logs — user_id (UUID) is sufficient for debugging; never log email, name, photo URL, or symptom text
- Railway provides log streaming — no separate log aggregation at MVP

### 10.3 Alerts

| Condition | Action |
|-----------|--------|
| GPT-4o Vision p95 > 8s (timeout threshold) | Railway alert → investigate API quota or fallback |
| Error rate > 5% on `/detect` | Railway alert |
| Notification send failure rate > 10% | Check Expo push token validity |

---

## 11. Security

| Concern | Mitigation |
|---------|------------|
| Auth | Supabase Auth handles JWT; all FastAPI endpoints validate `Authorization: Bearer {token}`; Supabase RLS as second layer |
| Photo access | Supabase Storage signed URLs (TTL 1h for app, 24h for PDF export); no public URLs |
| API secrets | OpenAI key, Supabase service key in Railway environment variables; never in code or git |
| Input validation | Pydantic models on all request bodies; max photo size: 10MB (rejected at API layer); voice max: 15s enforced server-side |
| GDPR right to erasure | `DELETE /account` sets `users.deleted_at`; hard delete job runs after 30 days; Supabase cascade deletes all child rows; Supabase Storage deletion via API |
| Data residency | Supabase EU region (eu-central-1 — Frankfurt) for GDPR compliance |

---

## 12. Risks and Failure Modes

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| GPT-4o Vision accuracy below 70% for food photos | Medium | High — correction rate metric fails | A/B test prompts before launch; benchmark on 50 representative food photos; fallback: allow manual entry as primary path if accuracy insufficient |
| Supabase Storage bandwidth cost at scale | Low (MVP) | Medium | Photos compressed to ≤2MB JPEG at app layer; thumbnails generated server-side; revisit at 10k+ DAU |
| Pattern algorithm produces false positives (spurious correlations) | Medium | Medium — undermines trust | Minimum evidence bar (≥2 symptomatic entries) reduces false positives; show correlation count explicitly ("4 of 5 meals") so user can assess; never frame as diagnostic |
| Expo Push notification delivery failure (iOS background restrictions) | Medium | Medium — check-in capture drops | Implement in-app fallback: "Add symptom check-in" banner shown when user opens app 2h after last meal entry |
| WeasyPrint PDF performance with many photos | Low | Low | Benchmark 14-day PDF with 42 photo thumbnails; optimize if >5s |
| APScheduler notification timing drift under load | Low | Low (UX degradation, not data loss) | Monitor actual delivery time vs scheduled_for; acceptable ±5 min at MVP |

---

## 13. Open Questions Remaining

These were not resolvable by the CTO alone — escalated to Alex:

| # | Question | Default if not resolved before Week 1 |
|---|----------|-----------------------------------------|
| OQ-01 | What is the minimum acceptable AI ingredient detection accuracy (precision) before launch? | **Default: ≤30% AI correction rate** (matches PRD metric). If user corrections exceed 30%, pause launch and investigate model/prompt. |
| OQ-05 | PDF localization? Spanish at MVP? | **Default: English only at MVP.** Template supports i18n via Jinja2 — Spanish is a ≤1-day add once needed. |

OQ-02, OQ-03, OQ-06 are resolved above.

---

## 14. Handoff to Implementation Plan

Architecture decisions are complete. CTO now produces `docs/07-implementation-plan.md` with:
- 6-week build plan to private beta
- File/folder structure
- Environment setup
- Testing strategy
- Definition of done per milestone

**What Alex needs to decide before Week 1 builds:**
1. Confirm React Native + Expo (vs Flutter) — if Alex has strong Flutter preference, this changes Week 1–3 timeline
2. Confirm Railway for backend hosting (vs Fly.io or Render)
3. Confirm OQ-01 accuracy threshold

---

## Sources

- CPO PRD-Lite: `docs/04-prd-lite.md`
- CDO UX flows: `docs/05-ux-flows-and-wireframes.md`
- Competitive analysis: `docs/competitive-analysis.md` Section 6.5
- Supabase RLS: https://supabase.com/docs/guides/auth/row-level-security
- OpenAI structured output: https://platform.openai.com/docs/guides/structured-outputs
- WeasyPrint: https://weasyprint.org/
- Expo push notifications: https://docs.expo.dev/push-notifications/overview/
- APScheduler: https://apscheduler.readthedocs.io/
