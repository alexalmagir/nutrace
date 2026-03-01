# Nutrace — UX Flows and Wireframes

**Document:** docs/05-ux-flows-and-wireframes.md
**Version:** 1.0
**Date:** 2026-03-01
**Phase:** C — Definition
**Author:** CDO (AI agent)
**Signed off by:** Alexandre Maravilla
**Status:** Draft — pending CTO review before architecture

**Input:** `docs/04-prd-lite.md` — Sections 7 (design constraints), 8 (user flows), 4.2 (user segments)

---

## CDO Design Brief

This document translates the functional flows defined by the CPO in `docs/04-prd-lite.md` into detailed UX flows with screen-level descriptions and interaction specifications. It does not define visual styling, color palettes, or component libraries — those belong to the design system phase.

**Design north star:** Every interaction must earn its place. Nutrace users are experiencing symptoms, stressed about their health, and often logging while eating or mid-symptom. The app must be faster, lower-friction, and more trustworthy than a paper diary — or users will not return.

**Hard constraints from Phase B (non-negotiable):**

1. Voice is optional — photo-only entry must complete without any voice prompt
2. First pattern insight at 3 days — UI must surface it before 7-day mark
3. AI correction: 2 taps max — no modals, no confirmation screens
4. PDF severity indicator must be visual (traffic light) — not text
5. Delayed symptom check-in at 2h and 4h post-meal
6. Eating disorder screen mandatory — non-skippable
7. PDF disclaimer on every export — cannot be removed
8. AI detection label "AI-detected" always visible — cannot be dismissed
9. 14-day default export window
10. Prior diagnosis context (Segment F) in PDF header

---

## App Structure

```
Nutrace (mobile — iOS + Android)
├── Onboarding (first use only)
│   ├── Welcome
│   ├── Contraindication screen (mandatory)
│   ├── Prior diagnosis field (optional)
│   ├── Account creation / sign-in
│   ├── Permissions (camera, notifications)
│   └── First meal prompt
│
├── Tab bar (main navigation, 3 tabs)
│   ├── [Camera] Log — primary action, center tab
│   ├── [Calendar] My Log — timeline + pattern view
│   └── [Document] Export — PDF generation
│
└── Entry detail (modal, opened from My Log)
```

**Design rationale:** 3-tab structure keeps the primary action (Log) always one tap away. No hamburger menu. No nested navigation in the primary flow. The log entry is a modal — it does not replace the current context.

---

## Flow 1 — First Use (Onboarding)

**Trigger:** App opened for the first time after install.
**Goal:** Get user past safety screens, account creation, and permissions — and into their first meal log — without losing them.
**Segment consideration:** Segment A (Active Diagnosis Seeker) will move fast. Segment F (Prior Diagnosis + Relapse) needs the prior diagnosis field surfaced. Segment B (Self-Investigator) may be concerned about privacy on the permissions screen.

---

### Screen 1.1 — Welcome

**Layout:** Full-screen, single focal point. Logo + tagline + single CTA.

```
┌─────────────────────────────┐
│                             │
│         [Nutrace logo]      │
│                             │
│   "Photo your meals.        │
│    Record how you feel.     │
│    Find what's causing it." │
│                             │
│   ──────────────────────  │
│                             │
│   Nutrace is a food and     │
│   symptom diary. It helps   │
│   you collect data. It does │
│   not give medical advice   │
│   or diagnoses.             │
│                             │
│   [Get started →]           │
│                             │
└─────────────────────────────┘
```

**Copy notes:**
- Regulatory framing appears here, on screen 1 — not buried in settings
- "Get started" does not say "Sign up" — reduces friction before commitment
- No skip option on this screen

---

### Screen 1.2 — Contraindication Screen (mandatory)

**Layout:** Centered card. Two explicit tap targets. Cannot be dismissed without selecting one.

```
┌─────────────────────────────┐
│                             │
│   Before we start          │
│                             │
│   Nutrace is designed for   │
│   people tracking digestive │
│   symptoms. It is not a     │
│   calorie counter, weight   │
│   tracker, or food          │
│   restriction tool.         │
│                             │
│   Are you using Nutrace to  │
│   track digestive symptoms  │
│   (bloating, pain, nausea,  │
│   irregular bowel)?         │
│                             │
│   [Yes, that's me →]        │
│                             │
│   [No / I'm not sure]       │
│                             │
└─────────────────────────────┘
```

**"No / I'm not sure" path:**

```
┌─────────────────────────────┐
│                             │
│   Nutrace may not be        │
│   right for you             │
│                             │
│   This app is built for     │
│   people experiencing       │
│   digestive symptoms who    │
│   want to find food         │
│   triggers.                 │
│                             │
│   If you have a history of  │
│   eating disorders or food  │
│   anxiety, please speak     │
│   with a healthcare         │
│   professional before       │
│   using a food logging app. │
│                             │
│   [Continue anyway]         │
│   [Exit]                    │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- This screen is not skippable. Back button is hidden.
- "No / I'm not sure" does not block access — it shows an advisory and lets the user continue. The screen does NOT imply the user has an eating disorder; it surfaces the advisory for anyone in that situation.
- All text passes plain-language review — no medical terminology.

---

### Screen 1.3 — Prior Diagnosis Context (Segment F)

**Layout:** Optional field, framed as helpful context — not a clinical form.

```
┌─────────────────────────────┐
│                             │
│   One optional question     │
│                             │
│   Have you previously been  │
│   diagnosed with a          │
│   digestive condition?      │
│                             │
│   (This helps give your     │
│   doctor context when you   │
│   share your log.)          │
│                             │
│   ┌─────────────────────┐   │
│   │ e.g. IBS, IBD,      │   │
│   │ Crohn's, celiac...  │   │
│   └─────────────────────┘   │
│                             │
│   [Save and continue →]     │
│   [Skip]                    │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- Field is free text — no dropdown (avoids incorrect self-labelling)
- "Skip" is visible and equally prominent — this field is genuinely optional
- The field value is stored and shown in the PDF header on every export
- Shown to all users — not just users who self-identify as Segment F. The question itself surfaces the Segment F use case naturally.

---

### Screen 1.4 — Account Creation

**Layout:** Standard email + password form with SSO options above.

```
┌─────────────────────────────┐
│                             │
│   Create your account       │
│                             │
│   [Continue with Apple]     │
│   [Continue with Google]    │
│                             │
│   ─────── or ───────        │
│                             │
│   Email                     │
│   ┌─────────────────────┐   │
│   └─────────────────────┘   │
│                             │
│   Password                  │
│   ┌─────────────────────┐   │
│   └─────────────────────┘   │
│                             │
│   [Create account →]        │
│                             │
│   Already have an account?  │
│   Sign in                   │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- SSO options first — reduces friction for most users
- No name field at signup — optional later in profile
- Password requirements shown inline when field is active, not as an error

---

### Screen 1.5 — Camera Permission

**Layout:** Explanation screen before the native OS permission dialog. Pre-permission screens significantly increase permission grant rates.

```
┌─────────────────────────────┐
│                             │
│   [Camera icon]             │
│                             │
│   Nutrace needs your camera │
│                             │
│   To detect ingredients     │
│   from your meal photos.    │
│   Photos are stored         │
│   securely and never        │
│   shared without your       │
│   permission.               │
│                             │
│   [Enable camera →]         │
│   [Not now]                 │
│                             │
└─────────────────────────────┘
```

→ Tapping "Enable camera" triggers the native OS permission dialog.

**"Not now" path:** User can log meals by uploading from gallery. Camera can be enabled later in Settings. App does not block on camera permission.

---

### Screen 1.6 — Notification Permission

```
┌─────────────────────────────┐
│                             │
│   [Bell icon]               │
│                             │
│   Optional: symptom         │
│   check-ins                 │
│                             │
│   Nutrace can remind you    │
│   to record how you feel    │
│   2 and 4 hours after       │
│   eating — when symptoms    │
│   often appear.             │
│                             │
│   You can turn this off     │
│   any time.                 │
│                             │
│   [Enable reminders →]      │
│   [Not now]                 │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- Framed around the user benefit (catch delayed symptoms), not "allow notifications"
- "Not now" is visible — this is low-stakes compared to camera
- Both "Not now" paths proceed to the first meal prompt without penalty

---

### Screen 1.7 — First Meal Prompt

```
┌─────────────────────────────┐
│                             │
│   You're ready              │
│                             │
│   Next time you eat,        │
│   take a photo before       │
│   your first bite.          │
│                             │
│   That's all you need       │
│   to do.                    │
│                             │
│   [📷 Log my first meal]    │
│                             │
│   [I'll do it later]        │
│                             │
└─────────────────────────────┘
```

→ Tapping "Log my first meal" opens Flow 2 (Meal Log Entry).
→ "I'll do it later" goes to the main app (My Log tab, empty state).

---

## Flow 2 — Meal Log Entry (Standard)

**Trigger:** User taps the center tab (Log) or the CTA from the empty state.
**Goal:** Create a complete meal entry — photo + optional voice — in under 30 seconds.
**Critical constraint:** This flow must work completely with photo-only. Voice is optional and must not interrupt the save path.

---

### Screen 2.1 — Camera

**Layout:** Full-screen camera viewfinder. Minimal chrome.

```
┌─────────────────────────────┐
│  ✕                    [⚡]  │  ← flash toggle
│                             │
│                             │
│                             │
│      [live viewfinder]      │
│                             │
│                             │
│                             │
│   ┌─────────────────────┐   │
│   │ 📷 Take photo       │   │  ← large tap target
│   └─────────────────────┘   │
│                             │
│   [🖼 Choose from gallery]  │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- No timer, no countdown, no instruction overlay — just the camera
- Gallery option is always visible — important for social/restaurant contexts (Segment A, U08)
- ✕ closes the camera and returns to previous screen without saving anything

---

### Screen 2.2 — AI Ingredient Detection (Processing)

**Layout:** Photo shown at top, processing indicator below.

```
┌─────────────────────────────┐
│  ✕                          │
│ ┌─────────────────────────┐ │
│ │                         │ │
│ │      [meal photo]       │ │
│ │                         │ │
│ └─────────────────────────┘ │
│                             │
│   Detecting ingredients...  │
│   [●●●○○○] 3s               │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- Loading state is explicit — user sees the photo was received
- Duration: 3–5 seconds (CTO to optimize)
- This screen is the "post-photo reward" that closes the habit loop — the photo disappearing into a void is a retention killer

---

### Screen 2.3 — Ingredient Review + Trigger Alert

This screen has two states: **no alert** (standard) and **alert** (trigger detected).

**State A — No alert (standard):**

```
┌─────────────────────────────┐
│  ✕              [Save →]    │
│ ┌─────────────────────────┐ │
│ │      [meal photo]       │ │
│ └─────────────────────────┘ │
│                             │
│   AI-detected ingredients   │  ← always shown, cannot be hidden
│   Tap to edit               │
│                             │
│   ● Pasta        [✕]        │
│   ● Tomato sauce [✕]        │
│   ● Parmesan     [✕]        │
│   ● Basil        [✕]        │
│   [+ Add ingredient]        │
│                             │
│   ─────────────────────     │
│   [🎤 Add voice note]       │  ← optional, not required to save
│                             │
└─────────────────────────────┘
```

**State B — Trigger alert (flagged ingredient detected):**

```
┌─────────────────────────────┐
│  ✕              [Save →]    │
│ ┌─────────────────────────┐ │
│ │      [meal photo]       │ │
│ └─────────────────────────┘ │
│                             │
│  ⚠️  Heads up               │
│  ┌───────────────────────┐  │
│  │ Parmesan appeared in  │  │
│  │ your log 3 times      │  │
│  │ before symptomatic    │  │
│  │ entries.              │  │
│  │                       │  │
│  │ [Tell me more]        │  │
│  │ [Remove from entry]   │  │
│  └───────────────────────┘  │
│                             │
│   AI-detected ingredients   │
│   Tap to edit               │
│                             │
│   ● Pasta        [✕]        │
│   ●⚠️Parmesan   [✕]        │  ← flagged ingredient highlighted
│   ● Tomato sauce [✕]        │
│   ● Basil        [✕]        │
│   [+ Add ingredient]        │
│                             │
│   [🎤 Add voice note]       │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- Alert is shown inline — not as a blocking modal or full-screen overlay
- "Save →" is always visible and always tappable — alert does not gate saving
- [✕] on each ingredient = 1 tap to remove (constraint: 2-tap correction max)
- [+ Add ingredient] opens a text field with auto-suggest from prior entries
- Flagged ingredient gets a ⚠️ prefix in the list — subtle, not alarming
- "Tell me more" expands to show a mini correlation view (which meals, which symptoms)
- Alert only shown if user has ≥3 days of data with symptom entries
- The "AI-detected" label is always shown — cannot be hidden or dismissed

---

### Screen 2.4 — Voice Note (Optional)

**Trigger:** User taps [🎤 Add voice note] on Screen 2.3.
**Layout:** Overlay panel from bottom (does not replace Screen 2.3).

```
┌─────────────────────────────┐
│                             │
│   ┌─────────────────────────┤
│   │                         │
│   │   How are you feeling?  │
│   │                         │
│   │   [●  Recording... 0:04]│  ← live timer, max 10s
│   │                         │
│   │   [■ Stop]              │
│   │                         │
│   │   Cancel                │
│   └─────────────────────────┘
└─────────────────────────────┘
```

After recording:

```
│   ┌─────────────────────────┤
│   │                         │
│   │   "A bit bloated,       │
│   │    nothing major"       │  ← transcribed text
│   │                         │
│   │   [▶ Play back]         │
│   │   [✎ Edit text]         │
│   │                         │
│   │   [Use this] [Re-record]│
│   └─────────────────────────┘
```

**Design notes:**
- Max 10 seconds — enforced by the timer (auto-stops at 10s)
- Transcription shown immediately — user sees what the AI heard
- "Edit text" lets user correct transcription without re-recording
- "Cancel" on the recording panel returns to Screen 2.3 without saving a voice note — photo-only entry is preserved

---

### Screen 2.5 — Entry Saved (Confirmation)

```
┌─────────────────────────────┐
│                             │
│         ✓                   │
│                             │
│   Meal logged               │
│                             │
│   Day 3 of your log.        │
│   First pattern insight     │
│   coming soon.              │  ← progress message, varies by day
│                             │
│   [View my log]             │
│   [Log another meal]        │
│                             │
└─────────────────────────────┘
```

**Progress messages by day:**

| Day | Message |
| --- | --- |
| 1 | "Day 1. Keep going — patterns take a few days to appear." |
| 2 | "Day 2. You're building a picture." |
| 3 | "Day 3. Check your log — you may already have your first insight." |
| 4–6 | "Day N of your log. Your pattern view is getting clearer." |
| 7+ | "You have X days of data. Time to export for your next appointment?" |

**Design notes:**
- This confirmation screen is the habit-loop close — it must feel rewarding, not administrative
- Day counter is the primary motivator (streak mechanic, no gamification chrome)
- "View my log" deep-links to My Log tab
- Auto-dismisses after 3 seconds if no tap

---

## Flow 3 — Delayed Symptom Check-in

**Trigger:** Push notification at 2h post-meal (and optionally at 4h).
**Goal:** Capture delayed symptom onset without requiring the user to open the app proactively.
**Constraint:** Must complete in under 15 seconds from notification tap to saved entry.

---

### Notification (Lock Screen / Banner)

```
┌─────────────────────────────┐
│  Nutrace                    │
│  How are you feeling 2      │
│  hours after your lunch?    │
│  Tap to add a note.         │
└─────────────────────────────┘
```

→ Tapping the notification opens Screen 3.1.

---

### Screen 3.1 — Quick Symptom Entry

**Layout:** Minimal. No navigation. Single purpose.

```
┌─────────────────────────────┐
│  ✕                 [Save →] │
│                             │
│   How are you feeling?      │
│   (2h after your lunch)     │  ← references the linked meal
│                             │
│   ┌─────────────────────┐   │
│   │ 😊  😐  😟  😖  😫 │   │  ← 5-point severity selector
│   └─────────────────────┘   │
│                             │
│   Optional: add a note      │
│   ┌─────────────────────┐   │
│   │                     │   │
│   └─────────────────────┘   │
│   or  [🎤 voice note]       │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- 5-point emoji severity selector = primary input. Tapping one emoji is sufficient to save.
- The selected emoji maps to the traffic light in the PDF: 😊=green, 😐=green, 😟=amber, 😖=amber, 😫=red
- Text note and voice note are both optional — severity tap alone saves the entry
- The linked meal is shown at the top (not just "your meal" — "your lunch") for context
- This entry is appended to the original meal log entry with a timestamp offset (+2h or +4h)

---

## Flow 4 — Pattern View (My Log Tab)

**Trigger:** User navigates to "My Log" tab.
**Goal:** Surface meal-symptom correlations in a scannable format. Show the first pattern at day 3.

---

### Screen 4.1 — My Log (Default State, <3 Days)

```
┌─────────────────────────────┐
│  My Log              [Filter│
│                             │
│  ┌─────────────────────────┐│
│  │ Keep going — patterns   ││
│  │ appear after 3 days     ││
│  │ of logging.             ││
│  │ 2 more meals to go.     ││
│  └─────────────────────────┘│
│                             │
│  Today — Monday             │
│  ┌─────────────────────────┐│
│  │ [thumb] 12:34 Lunch    ││
│  │  Pasta, tomato sauce,  ││
│  │  parmesan              ││
│  │  😐 (2h: mild bloating)││  ← delayed check-in shown inline
│  └─────────────────────────┘│
│  ┌─────────────────────────┐│
│  │ [thumb] 08:12 Breakfast ││
│  │  Oats, milk, banana    ││
│  │  No symptoms logged    ││
│  └─────────────────────────┘│
│                             │
│  Yesterday — Sunday         │
│  ┌─────────────────────────┐│
│  │ [thumb] 19:45 Dinner   ││
│  │  ...                   ││
│  └─────────────────────────┘│
└─────────────────────────────┘
```

---

### Screen 4.2 — My Log (Pattern Surfaced, ≥3 Days)

```
┌─────────────────────────────┐
│  My Log              [Filter│
│                             │
│  ┌─────────────────────────┐│
│  │ 🔍 Pattern found        ││
│  │                         ││
│  │ Bloating appeared after ││
│  │ 4 of 5 meals containing ││
│  │ dairy.                  ││
│  │                         ││
│  │ [See dairy entries →]   ││
│  └─────────────────────────┘│
│                             │
│  [Day view] [Ingredient →]  │  ← toggle between views
│                             │
│  Tuesday ●●●○○              │  ← symptom severity dots by day
│  Monday  ●○○○○              │
│  Sunday  ●●○○○              │
│  Saturday●●●●○              │
│  Friday  ●○○○○              │
│  ...                        │
│                             │
└─────────────────────────────┘
```

**Ingredient view (toggled):**

```
│  [Day view] [Ingredient ✓]  │
│                             │
│  Tap an ingredient to see   │
│  its symptom history:       │
│                             │
│  🔴 Dairy        5× meals   │
│     4× with symptoms        │
│  🟡 Wheat        3× meals   │
│     2× with symptoms        │
│  🟢 Chicken      4× meals   │
│     0× with symptoms        │
│  🟢 Rice         2× meals   │
│     0× with symptoms        │
```

**Design notes:**
- Pattern card is shown above the log when ≥3 days of data exist with at least one symptom entry
- Severity dots per day give a quick visual of "good days vs. bad days" without requiring users to read entries
- Ingredient view shows a ranked list by symptom correlation — highest correlation at top
- Traffic light color on each ingredient reflects symptom correlation rate
- Tapping an ingredient deep-links to all entries containing it

---

### Screen 4.3 — Entry Detail (Modal)

**Trigger:** Tapping any log entry card.

```
┌─────────────────────────────┐
│  ✕          Tuesday 12:34   │
│                             │
│  ┌─────────────────────────┐│
│  │                         ││
│  │      [full meal photo]  ││
│  │                         ││
│  └─────────────────────────┘│
│                             │
│  Ingredients                │
│  AI-detected · Tap to edit  │  ← always shown
│  Pasta · Parmesan · Basil   │
│  Tomato sauce               │
│                             │
│  ──────────────             │
│  Symptoms                   │
│  Immediately: 😐 (text note)│
│  +2h: 😟 "bloating, mild"   │
│  +4h: not recorded          │
│                             │
│  [Edit entry] [Delete]      │
│                             │
└─────────────────────────────┘
```

---

## Flow 5 — PDF Export

**Trigger:** User navigates to "Export" tab or taps "Time to export?" from day-7 confirmation screen.
**Goal:** Generate a clinical-grade PDF and share it with a healthcare professional.

---

### Screen 5.1 — Export Setup

```
┌─────────────────────────────┐
│  Export your log            │
│                             │
│  Date range                 │
│  ┌─────────────────────────┐│
│  │ Last 14 days     [▼]   ││  ← default 14 days
│  └─────────────────────────┘│
│  Options: 7 days / 14 days  │
│  / Custom range             │
│                             │
│  Include photos in PDF?     │
│  [Yes]  [No]                │
│                             │
│  Add a note for your doctor │
│  (optional)                 │
│  ┌─────────────────────────┐│
│  │ e.g. "For Dr. García,  ││
│  │ appointment 15 March"  ││
│  └─────────────────────────┘│
│                             │
│  [Preview PDF →]            │
│                             │
└─────────────────────────────┘
```

---

### Screen 5.2 — PDF Preview

**Layout:** Scrollable preview of the PDF. Actual PDF opens in native viewer.

The PDF layout (described for CDO spec, not user-facing):

```
PAGE 1 — SUMMARY
─────────────────────────────
NUTRACE FOOD & SYMPTOM DIARY
Patient: [name if provided]
Prior condition: [if provided in onboarding — Segment F]
Period: 14 Feb – 28 Feb 2026
Generated: 1 Mar 2026

NOTE FOR DOCTOR (if added): "For Dr. García, appointment 15 March"

SYMPTOM OVERVIEW
■■■□□ Day severity (14-day bar chart — traffic light colored)

TOP PATTERNS
• Dairy: symptoms in 4 of 5 meals containing dairy
• Wheat: symptoms in 2 of 3 meals containing wheat

─────────────────────────────
PAGE 2+ — DAILY LOG

[Date] [Time] [Meal photo thumbnail if included]
Ingredients (AI-detected): Pasta · Parmesan · Tomato sauce
Symptoms: 😟 Immediately — "mild bloating"
          😖 +2h — "strong bloating, discomfort"
          Not recorded +4h

[repeat per entry]

─────────────────────────────
LAST PAGE — DISCLAIMER
─────────────────────────────
Nutrace is a data-capture and journaling tool. It does not provide
medical advice or diagnosis. All clinical interpretation should be
performed by a qualified healthcare professional.

Generated by Nutrace · nutrace.app
```

**Screen 5.2 continued:**

```
┌─────────────────────────────┐
│  ✕          PDF Preview     │
│                             │
│  ┌─────────────────────────┐│
│  │  NUTRACE FOOD &         ││
│  │  SYMPTOM DIARY          ││
│  │  14 Feb – 28 Feb 2026   ││
│  │                         ││
│  │  PATTERNS               ││
│  │  🔴 Dairy: 4/5 meals    ││
│  │  🟡 Wheat: 2/3 meals    ││
│  │                         ││
│  │  [scroll to see log ↓]  ││
│  └─────────────────────────┘│
│                             │
│  [Share / Export ↑]         │
│                             │
└─────────────────────────────┘
```

→ "Share / Export" triggers native share sheet (AirDrop, email, WhatsApp, save to Files, etc.)

**Design notes:**
- PDF disclaimer is on the last page of every PDF — cannot be removed by the user (no toggle)
- Photo thumbnails: included by default, can be turned off in Screen 5.1 for privacy
- The "prior diagnosis" Segment F field appears in the PDF header — not a footnote

---

## Flow 6 — Proactive Trigger Alert Detail

**Trigger:** User taps "Tell me more" on the trigger alert card (Screen 2.3, State B).
**Goal:** Give the user enough context to make an informed decision about eating the flagged ingredient — without making a diagnostic claim.

---

### Screen 6.1 — Trigger Alert Detail

```
┌─────────────────────────────┐
│  ✕                          │
│                             │
│  ⚠️ About Parmesan          │
│                             │
│  In your last 14 days:      │
│                             │
│  Meals with parmesan:   5   │
│  Meals with symptoms:   3   │
│                             │
│  Symptom timeline:          │
│  ┌─────────────────────────┐│
│  │ Mon 24 · Lunch   😟 +2h ││
│  │ Wed 19 · Dinner  😖 +1h ││
│  │ Sat 15 · Lunch   😟 +2h ││
│  └─────────────────────────┘│
│                             │
│  ──────────────────         │
│  This is a pattern from     │
│  your log — not a           │
│  diagnosis. Share this      │
│  with your doctor.          │
│                             │
│  [Remove from this entry]   │
│  [Continue logging →]       │
│                             │
└─────────────────────────────┘
```

**Design notes:**
- Numbers shown are from the user's own log — not general population data
- Disclaimer shown inline: "This is a pattern from your log — not a diagnosis."
- "Remove from this entry" removes the ingredient before saving — does not delete it from the log history
- "Continue logging →" saves the entry as-is and returns to the confirmation screen
- This screen does not appear until the user has ≥3 days of data

---

## Empty States

Good empty states are retention tools. They explain what the user should do next, not what the app can't show yet.

| Screen | Empty state message |
| --- | --- |
| My Log (0 entries) | "Take a photo of your next meal to start your log." + [📷 Log first meal] |
| My Log (1–2 days, no pattern yet) | "Keep going. Patterns usually appear after 3 days of logging." + progress indicator |
| Pattern card (3+ days, no correlation) | "No strong patterns yet. Keep logging — more data gives clearer signals." |
| Export (0 entries) | "Log a few meals first. You'll need at least 7 days for a useful export." |

---

## Segment-Specific UX Notes

### Segment A — Active Diagnosis Seeker

- Onboarding CTA should emphasize the export: "Log now. Share with your doctor."
- Day 7 confirmation screen should prominently surface the Export tab
- First pattern card framing: "Share this with your gastroenterologist"

### Segment B — Self-Investigator

- Camera permission screen must include privacy reassurance ("never shared without your permission")
- Pattern view should be the most polished part of the product — this segment's primary motivation
- No mandatory professional sharing in any flow

### Segment C — Chronic Follow-up

- Ingredient view in My Log (Screen 4.2) is their primary value — they already know their triggers; they want to monitor trends
- Export date range selector should support custom ranges (not just 7/14 days)

### Segment D — High-Literacy Patient

- AI detection label must be prominent (they will scrutinize it)
- Correction flow must be the fastest path — edit/remove ingredients with minimum friction
- Consider displaying confidence indicator per ingredient (CTO decision — if model supports it)

### Segment E — Dismissed Patient

- Framing: "your data as evidence" — reinforce in empty states and export screens
- Export screen copy: "Bring this to your next appointment as objective data"
- Pattern card framing: "You've documented a pattern. Your data speaks for itself."

### Segment F — Prior Diagnosis + Relapse

- Prior diagnosis context (Screen 1.3) shown in PDF header — this is the key feature
- Entry detail (Screen 4.3) should show full date range — they need chronological context
- Pattern comparison view (current vs. prior episode) — V2 feature; data model must support it from day 1 (CTO note)

---

## Design Constraints Compliance Checklist

For CTO review before architecture:

| Constraint | How it is addressed in this doc |
| --- | --- |
| Voice is optional | Screen 2.3: [Save →] visible without voice note; 2.4 is optional step |
| First pattern at 3 days | Screen 4.1 shows progress count; Screen 4.2 pattern card fires at day 3 |
| AI correction 2 taps max | Screen 2.3: [✕] on each ingredient = 1 tap; no confirmation modal |
| PDF severity visual | PDF layout: traffic light per entry; emoji severity selector maps to colors |
| Delayed check-in 2h/4h | Flow 3: notification + Screen 3.1; appended to original entry |
| Eating disorder screen mandatory | Screen 1.2: non-skippable; back button hidden |
| PDF disclaimer always present | PDF last page: non-removable |
| AI detection label always shown | Screen 2.3: "AI-detected ingredients" header; Screen 4.3: entry detail |
| 14-day default window | Screen 5.1: default selection |
| Segment F context in PDF header | Screen 1.3 → stored → PDF header |

---

## Handoff to CTO

The following decisions require CTO input before this UX can be finalized:

| Item | Question | UX dependency |
|------|----------|--------------|
| AI processing time | What is the realistic latency for ingredient detection from photo? | Screen 2.2 loading state duration and messaging |
| Confidence per ingredient | Does the vision model return a confidence score per ingredient? | Screen 2.3: optional confidence indicator for Segment D |
| Pattern algorithm | What is the minimum dataset required for a first correlation? | Screen 4.1/4.2: exact trigger condition for pattern card |
| Notification system | How are the 2h/4h post-meal notifications triggered? | Flow 3: notification delivery timing accuracy |
| Data model for Segment F | Does the data model support future comparison view (current vs. prior episode)? | Future-proofing for V2 |
| Photo storage | Cloud vs. on-device? | Screen 1.5 camera permission copy; Screen 5.1 photo toggle |

---

## Sources

- CPO PRD-Lite: `docs/04-prd-lite.md` — Sections 7, 8, 4.2
- Phase B validation: `docs/03-validation-plan-and-results.md` — user quotes and clinical requirements
- User segments: `docs/04-prd-lite.md` Section 4.2
- Design constraints: `docs/04-prd-lite.md` Section 7
