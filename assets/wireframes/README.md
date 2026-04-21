# Nutrace — Wireframes (Figma Make Prompts)

> Prompts for generating low-fidelity wireframes in Figma Make.
>
> **Phase:** D — Build (updated from Phase C)
> **CDO Owner:** CDO agent (Phase D revision 2026-03-04)
> **Source spec:** `docs/05-ux-flows-and-wireframes.md` v2.0
> **Flow navigation diagrams:** `assets/user-flows/README.md`
>
> **v2.0 changes (Phase D all-hands):** Flow 3 added Frame 3.N3 (symptom nudge notification). Flow 5 Screen 5.2: removed bar chart → text table + HCP share link button. Flow 6 Screen 6.1: removed symptom timeline table → two data rows only.

---

## How to use

1. Open [figma.com/make](https://www.figma.com/make) with your personal account (`alex.almagir@gmail.com`)
2. Create a new project called **nutrace**
3. For each flow, copy the prompt below and paste it into Figma Make
4. Each prompt generates all screens in that flow as a single canvas
5. Once generated, paste the Figma file link in the **Figma wireframe** column below

---

## Flow Index

| Flow | Screens | FigJam (navigation) | FigJam (PNG) | Figma wireframe |
|------|---------|---------------------|--------------|-----------------|
| Flow 1 — Onboarding | 7 + advisory branch | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/3d9a8a89-c4f7-41e9-9218-4496b0e4c88c?utm_source=claude&utm_content=edit_in_figjam) | [PNG](../user-flows/flow-1-onboarding.png) | [Figma Make](https://claim-manage-96224058.figma.site/) |
| Flow 2 — Meal Log Entry | 5 + 2 states | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/5d7b726f-a207-43ab-9fd7-cd0d4d82fd36?utm_source=claude&utm_content=edit_in_figjam) | [PNG](../user-flows/flow-2-meal-log-entry.png) | [Figma Make](https://smog-sheen-50549098.figma.site) |
| Flow 3 — Delayed Symptom Check-in | 1 + 2 notification variants + 1 nudge notification | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/bad954b4-f4bf-4ab3-bb63-72e386e93cdf?utm_source=claude&utm_content=edit_in_figjam) | [PNG](../user-flows/flow-3-delayed-symptom-checkin.png) | [Figma Make](https://seven-acre-26715721.figma.site/) |
| Flow 4 — Pattern View (My Log) | 3 + ingredient view + empty state | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/cd8c2f39-0e99-4b86-b1ac-35dd4514ba68?utm_source=claude&utm_content=edit_in_figjam) | _to be added_ | _to be added_ |
| Flow 5 — PDF Export | 2 + empty state + HCP share link | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/333b571c-d8aa-47f2-aa1b-49f9a094461d?utm_source=claude&utm_content=edit_in_figjam) | _to be added_ | _to be added_ |
| Flow 6 — Trigger Alert Detail | 1 + 3 exit paths | [FigJam](https://www.figma.com/online-whiteboard/create-diagram/88581b84-8f1a-4bc0-8809-acb34667312c?utm_source=claude&utm_content=edit_in_figjam) | _to be added_ | _to be added_ |

---

## Prompts

> Style guide for all prompts: iPhone 16 Pro frame size. Low-fidelity wireframe style: white backgrounds, gray fills for image placeholders, black text, no decorative color. Label each frame above with the screen number and name.

---

### Flow 1 — Onboarding (7 screens + advisory branch)

```
Create low-fidelity wireframes for a mobile app called Nutrace — a food and symptom diary
for people with digestive conditions (IBS, IBD, Crohn's, celiac). Design 8 screens in
iPhone 16 Pro frame size, arranged horizontally in sequence. Wireframe style: white
backgrounds, gray fills for image/icon placeholders, black text, no color. Label each
frame above with the screen number and name.

SCREEN 1.1 — Welcome
Full-screen. Top center: Nutrace logo placeholder (rectangle, ~80px tall). Center: tagline
in 3 stacked lines: "Photo your meals. / Record how you feel. / Find what's causing it."
Below tagline: horizontal divider. Short disclaimer paragraph (2–3 lines): "Nutrace is a
food and symptom diary. It helps you collect data. It does not give medical advice or
diagnoses." Bottom: large primary CTA button "Get started →". No back navigation.

SCREEN 1.2 — Contraindication (mandatory)
Centered card layout taking ~80% of screen. Title: "Before we start". Body paragraph
(3–4 lines): app is designed for digestive symptom tracking, not calorie counting or
food restriction. Question below: "Are you using Nutrace to track digestive symptoms
(bloating, pain, nausea, irregular bowel)?" Two buttons stacked: primary "Yes, that's me
→" and secondary outlined "No / I'm not sure". No back navigation visible. No skip option.

SCREEN 1.2b — Advisory (shown after "No / I'm not sure")
Same card layout. Title: "Nutrace may not be right for you". Body paragraph: app is for
people with digestive symptoms who want to find food triggers. Advisory about eating
disorders and food anxiety — recommends speaking with a healthcare professional before
using a food logging app. Two buttons: "Continue anyway" (primary) and "Exit" (ghost/link).

SCREEN 1.3 — Prior Diagnosis (optional)
Title: "One optional question". Short paragraph: "Have you previously been diagnosed with
a digestive condition? (This helps give your doctor context when you share your log.)"
Free-text input field with placeholder "e.g. IBS, IBD, Crohn's, celiac...". Two buttons:
primary "Save and continue →" and equally prominent ghost "Skip". Both buttons must be
visually similar weight — this is a genuinely optional field.

SCREEN 1.4 — Account Creation
Title: "Create your account". Two full-width SSO buttons at top: "Continue with Apple"
(with Apple logo placeholder) and "Continue with Google" (with Google logo placeholder).
Horizontal divider "or". Email text field with label. Password text field with label and
eye icon. Primary button "Create account →". Small text link below: "Already have an
account? Sign in".

SCREEN 1.5 — Camera Permission
Centered layout. Large camera icon placeholder (circle, ~60px). Title: "Nutrace needs
your camera". Body (2–3 lines): "To detect ingredients from your meal photos. Photos are
stored securely and never shared without your permission." Primary button "Enable camera
→". Ghost button "Not now". Note at bottom: "You can always enable this later in Settings."

SCREEN 1.6 — Notification Permission
Same centered layout as 1.5. Bell icon placeholder (circle, ~60px). Title: "Optional:
symptom check-ins". Body: "Nutrace can remind you to record how you feel 2 and 4 hours
after eating — when symptoms often appear." Small line: "You can turn this off any time."
Primary button "Enable reminders →". Ghost button "Not now".

SCREEN 1.7 — First Meal Prompt
Centered. Large checkmark or success icon. Title: "You're ready". Body (2 lines): "Next
time you eat, take a photo before your first bite. That's all you need to do." Primary
button with camera icon "Log my first meal". Ghost button "I'll do it later".

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

### Flow 2 — Meal Log Entry (5 screens + 2 states on Screen 2.3)

```
Create low-fidelity wireframes for the core meal logging flow of Nutrace (a food and
symptom diary app). Design 6 screens in iPhone 16 Pro frame size, arranged horizontally.
Wireframe style: white backgrounds, gray fills, black text, no color. Label each frame.

SCREEN 2.1 — Camera
Full-screen camera viewfinder (large gray rectangle filling the entire screen). Top-left:
X close button (returns to previous screen without saving). Top-right: flash toggle icon.
Bottom area (fixed, floating over viewfinder): large primary button "Take photo" with
camera icon. Below it: smaller ghost button "Choose from gallery" with image icon. Gallery
option must always be visible — critical for users in social or restaurant contexts.

SCREEN 2.2 — AI Processing
Top half (~50%): meal photo placeholder (gray rectangle). Below photo: centered text
"Detecting ingredients..." with a dot progress indicator below it and an estimated time
"~3 sec". Remaining screen: empty, giving breathing room. Top-left: X close button.
This screen is the visual confirmation that the photo was received — important for the
habit loop.

SCREEN 2.3a — Ingredient Review (no alert — standard state)
Top bar: X on left, "Save →" button on right (primary, always visible). Below: meal photo
placeholder (~25% height). Section label: "AI-detected ingredients / Tap to edit". List of
4 ingredients, each as a row: bullet point, ingredient name, X remove button on far right.
Example ingredients: Pasta, Tomato sauce, Parmesan, Basil. Below list: "+ Add ingredient"
link/row. Horizontal divider. Bottom: secondary button with mic icon "Add voice note
(optional)". Note: Save → is always reachable — no voice note required to save.

SCREEN 2.3b — Ingredient Review (trigger alert — flagged ingredient detected)
Same layout as 2.3a. Between photo and ingredient list: inline alert card (rounded
rectangle with warning triangle icon). Card title: "Heads up". Card body (2 lines):
"Parmesan appeared in your log 3 times before symptomatic entries." Two small text links
inside the card: "Tell me more →" and "Remove from entry". In the ingredient list: the
flagged ingredient (Parmesan) has a small warning icon prefix. Save → always visible
at top-right — alert does not block saving.

SCREEN 2.4 — Voice Note Overlay (optional)
Screen 2.3a shown dimmed in background. Bottom sheet overlay (~40% screen height) sliding
up from bottom. Inside sheet: title "How are you feeling?" Recording state: animated
recording indicator dot, live timer "Recording... 0:04" (max 10 seconds). Stop button
below. "Cancel" link at bottom. After recording completes: transcribed text in a bordered
box (e.g. "A bit bloated, nothing major"). Playback button, "Edit text" link, and two
buttons: "Use this" (primary) and "Re-record" (ghost).

SCREEN 2.5 — Entry Saved (confirmation)
Centered layout. Large checkmark icon. Title: "Meal logged". Subtitle (dynamic by day —
show day 3 example): "Day 3 of your log. First pattern insight coming soon." Two buttons,
equal visual weight: "View my log" and "Log another meal". Note: this screen auto-dismisses
after 3 seconds if not tapped — the day counter is the primary streak mechanic.

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

### Flow 3 — Delayed Symptom Check-in (2 notification variants + 1 nudge notification + 1 screen)

```
Create low-fidelity wireframes for the delayed symptom check-in flow of Nutrace (a food
and symptom diary app). Design 4 frames in iPhone 16 Pro frame size, arranged horizontally.
Wireframe style: white backgrounds, gray fills, black text, no color. Label each frame.

FRAME 3.N1 — Lock Screen Notification (2h variant)
Simulate a phone lock screen: blurred gray background rectangle. Top status bar. Center:
notification banner (rounded rectangle): app icon placeholder on left, bold app name
"Nutrace", notification body: "How are you feeling 2 hours after your lunch?" Smaller
sub-text: "Tap to add a note." Time shown: 14:32 (2h after a 12:30 lunch example).

FRAME 3.N2 — Lock Screen Notification (4h variant)
Same layout as 3.N1. Notification body changes to: "How are you feeling 4 hours after
your lunch?" Time: 16:32. This is the same screen with dynamic copy — both 2h and 4h
notifications trigger identical UI with different text.

FRAME 3.N3 — Lock Screen Notification (Symptom Nudge — 2 days without symptoms)
Same lock screen layout as 3.N1 and 3.N2. Notification body: "How did you feel after
your last meal? Add a symptom note — your doctor needs this data." No time reference.
Add a small annotation note below the frame: "Triggered when user has logged meals for
2+ days but has zero symptom entries in that period. Sends once per 48h."

SCREEN 3.1 — Quick Symptom Entry
Minimal layout — single-purpose screen. Top bar: X close on left, "Save →" on right.
Title: "How are you feeling?" Subtitle referencing the actual linked meal name (not generic):
"(2h after your Lunch — Pasta, tomato sauce)". Center: horizontal row of 5 equally-spaced
circles representing severity faces, numbered 1–5 below each. Labels below the row: "Great",
"OK", "Meh", "Bad", "Awful". Instruction text below circles: "Tap one to save instantly."
Below a horizontal divider: "Optional: add a note". Short text input field (1 line,
placeholder text). Below: secondary button with mic icon "Add voice note". The emoji
tap is the primary action — all other inputs are optional.

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

### Flow 4 — Pattern View / My Log (empty state + 2 log states + ingredient view + entry modal)

```
Create low-fidelity wireframes for the My Log / Pattern View of Nutrace (a food and
symptom diary app). Design 5 screens in iPhone 16 Pro frame size, arranged horizontally.
Wireframe style: white backgrounds, gray fills, black text, no color. All main screens
include a bottom tab bar with 3 tabs: [camera icon] Log | [calendar icon] My Log (active)
| [document icon] Export. Label each frame.

SCREEN 4.0 — My Log (empty state, 0 entries)
Full-width empty state banner in center of screen. Icon (magnifying glass or blank calendar
placeholder). Title: "Take a photo of your next meal to start your log." Large primary
button: "Log first meal" with camera icon. No log entries below.

SCREEN 4.1 — My Log (default state, less than 3 days of data)
Top bar: title "My Log" on left, "Filter" icon on right. Below: progress banner card
(rounded rectangle, lighter border): "Keep going — patterns appear after 3 days of
logging. 2 more meals to go." + small progress bar. Section header "Today — Monday".
Two log entry cards (rounded rectangles): each shows a small photo thumbnail (gray
square) on left, time and meal label ("12:34 Lunch"), ingredient names on one line.
One card shows an emoji inline (delayed check-in result: "2h: meh face"). Section
header "Yesterday — Sunday" with one entry card. Bottom: 3-tab bar.

SCREEN 4.2 — My Log (pattern surfaced, 3 or more days)
Top bar: "My Log" + "Filter". Pattern card at top (rounded rectangle, distinct border):
magnifying glass icon + "Pattern found". Body: "Bloating appeared after 4 of 5 meals
containing dairy." Link: "See dairy entries →". Below card: two adjacent toggle tabs:
"Day view" (active) | "Ingredient →". Below toggles: list of days with symptom severity
dot rows (e.g. Tuesday: 3 filled dots + 2 empty dots out of 5, Monday: 1 filled, Sunday:
2 filled). Log entries below as in 4.1. Bottom: 3-tab bar.

SCREEN 4.2b — Ingredient View (toggled from 4.2)
Same top bar. Toggle shows "Ingredient" tab active. Below toggle: instruction text "Tap
an ingredient to see its symptom history:". Ingredient list rows — each row: filled
circle placeholder on left (representing correlation severity), ingredient name, two
lines of sub-text: "X meals containing it" and "Y meals with symptoms after". Example
rows: Dairy (high — 5 meals / 4 with symptoms), Wheat (medium — 3 meals / 2 with
symptoms), Chicken (low — 4 meals / 0 with symptoms), Rice (low — 2 meals / 0 symptoms).
Tapping a row filters the log to entries containing that ingredient. Bottom: 3-tab bar.

SCREEN 4.3 — Entry Detail (modal)
Modal sheet overlay on top of My Log screen. Top of modal: X close on left, date and time
as title "Tuesday 12:34". Full-width meal photo placeholder (~35% of modal height).
Section "Ingredients". Sub-label: "AI-detected · Tap to edit". Ingredient tags or
comma-separated list. Horizontal divider. Section "Symptoms". Three rows:
"Immediately: [face emoji] + text note", "+2h: [face emoji] + text note",
"+4h: not recorded". Bottom: two equal buttons "Edit entry" (secondary) and "Delete" (ghost).

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

### Flow 5 — PDF Export (empty state + 2 screens)

```
Create low-fidelity wireframes for the PDF export flow of Nutrace (a food and symptom
diary app). Design 3 screens in iPhone 16 Pro frame size, arranged horizontally. Wireframe
style: white backgrounds, gray fills, black text, no color. Include bottom tab bar on app
screens with 3 tabs: [camera icon] Log | [calendar icon] My Log | [document icon] Export
(active). Label each frame.

SCREEN 5.0 — Export (empty state)
Top bar: title "Export your log". Empty state centered on screen: document icon placeholder
(circle, ~60px). Title: "Log a few meals first". Body: "You'll need at least 7 days of
entries for a useful export." Ghost primary button: "Log your first meal →". Bottom: 3-tab
bar.

SCREEN 5.1 — Export Setup
Top bar: title "Export your log". Bottom: 3-tab bar. Content:
Section "Date range": dropdown selector showing "Last 14 days [v]". Small text below:
"Options: 7 days / 14 days / Custom range".
Section "Include photos in PDF?": two equal toggle buttons side by side: "Yes" (selected,
outlined) and "No" (ghost).
Section "Add a note for your doctor (optional)": multi-line text input, 3 lines tall,
placeholder "e.g. For Dr. García, appointment 15 March".
Full-width primary button at bottom of content: "Preview PDF →".

SCREEN 5.2 — PDF Preview
Top bar: X close on left, "PDF Preview" as title. A scrollable PDF preview frame
(rounded rectangle, subtle shadow) taking ~65% of screen height. Inside the preview,
document layout (not a mobile UI — this is a paper document representation):
Header: "NUTRACE FOOD & SYMPTOM DIARY" bold. Fields: "Patient:", "Prior condition:
[if provided at onboarding]", "Period:", "Generated:". Section "NOTE FOR DOCTOR" (if
added). Section "SYMPTOM OVERVIEW — 14 DAYS": one line of plain text, two values side
by side: "Symptomatic days: 8 / 14" and "Average severity: 3.2 / 5". No bar chart.
Section "TOP PATTERNS": two rows with filled circle placeholders (high/medium) and
pattern description text. Below preview: text "Scroll to see full log ↓".
Below preview frame: two full-width buttons stacked: primary "Share / Export ↑" with
share icon, and secondary outlined "Generate doctor link 🔗" with a note beside it
"(opens in any browser — no login needed)".

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

### Flow 6 — Proactive Trigger Alert Detail (1 screen, 3 exit paths)

```
Create a low-fidelity wireframe for the trigger alert detail screen of Nutrace (a food
and symptom diary app). Design 1 screen in iPhone 16 Pro frame size. Wireframe style:
white background, gray fills for placeholders, black text, no color.

SCREEN 6.1 — Trigger Alert Detail
This screen opens from the "Tell me more →" link on the trigger alert card in Screen 2.3.
No tab bar — this is a full-screen modal.

Top: X close button on left, no title text (the ingredient name serves as the heading).

SECTION 1 — Header
Warning triangle icon (small, ~20px) + ingredient name as large title: "About Parmesan"

SECTION 2 — Stats from user's own log
Sub-label: "In your last 14 days:". Two data rows only:
  "Meals containing parmesan:   5"
  "Meals with symptoms after:   3"
IMPORTANT: display as counts only — no percentages, no statistical language, no timeline
table. This is the MVP version: two numbers, nothing else. The symptom-by-meal timeline
is deferred to V1.1.

SECTION 3 — Inline disclaimer
Horizontal divider. Italic or lighter-weight text: "This is a pattern from your log —
not a diagnosis. Share this with your doctor before making any changes to your diet."

BOTTOM ACTIONS — two stacked buttons
Primary: "Continue logging →" (proceed to save entry as-is)
Ghost: "Remove from this entry" (removes the flagged ingredient before saving, does not
delete it from log history)

---

STYLE SYSTEM / VISUAL CONSISTENCY

This flow is part of a larger mobile product, so the visual style must remain consistent across all prototypes.

Create a polished, high-fidelity mobile app aesthetic for a modern AI-powered wellness / nutrition product. The product should feel premium, calm, warm, trustworthy, and visually refined — closer to a beautifully crafted consumer wellness app than to a clinical or enterprise tool.

VISUAL DIRECTION
- Avoid black-and-white only UI.
- Avoid harsh borders, boxed layouts, and wireframe-like screens.
- Prefer a soft, elegant, premium visual language.
- Use borderless or near-borderless surfaces with subtle elevation, tonal contrast, soft shadows, and layered backgrounds.
- Use generous rounded corners throughout the interface.
- Favor visual hierarchy through spacing, typography, color, and depth rather than visible outlines.
- Make every screen feel intentionally designed, polished, and demo-ready.

COLOR SYSTEM
- Use a cohesive, tasteful palette with warmth and personality.
- Prefer soft off-white, ivory, cream, or lightly tinted backgrounds instead of pure white.
- Use muted but rich accent colors such as sage green, muted teal, soft coral, peach, lavender, dusty plum, pale mint, or warm sand.
- Text should use charcoal or dark desaturated tones instead of pure black.
- Keep contrast accessible and readability high.
- Use color consistently across all screens and flows so the product feels like one unified design system.

COMPONENT STYLE
- Use elegant borderless cards or softly separated surfaces.
- Use large rounded buttons with modern, clean typography.
- Inputs, selectors, chips, pills, and segmented controls should feel soft and minimal, using fills and tonal contrast rather than strong borders.
- Icons should be simple, friendly, modern, and slightly rounded.
- Progress, states, summaries, and feedback elements should feel visually delightful, not dashboard-like.
- Use subtle gradients or tinted surfaces where appropriate to add depth and polish.

LAYOUT & TYPOGRAPHY
- Mobile-first iPhone-style composition.
- Use generous whitespace and clear vertical rhythm.
- Keep layouts breathable, calm, and uncluttered.
- Use a modern sans-serif style with strong hierarchy: elegant headings, readable body text, and concise supporting copy.
- Headings should feel premium and calming, not technical or clinical.

PRODUCT FEEL
- Warm, intelligent, supportive, and emotionally safe.
- Wellness-oriented, not hospital-like.
- Trustworthy and modern, with a subtle AI-native feel.
- Suitable for user testing, founder demos, and early-stage stakeholder presentations.

CONSISTENCY REQUIREMENT
Maintain the same design language across all flows:
- same palette family
- same button style
- same card treatment
- same corner radius logic
- same spacing rhythm
- same typography hierarchy
- same input style
- same icon style
- same visual tone

The result should feel like one coherent product, not separate concepts generated independently.
```

---

## CPO + CDO Review Notes (2026-03-02)

Corrections applied in this document vs. original prompts generated in the session:

| Flow | Correction |
|------|-----------|
| Flow 1 — Screen 1.6 | Added "You can turn this off any time" to notification permission copy |
| Flow 2 — Screen 2.5 | Both CTAs ("View my log" / "Log another meal") now specified as equal visual weight |
| Flow 3 | Added 2h and 4h notification variants as separate frames (3.N1 and 3.N2). Added dynamic meal name reference in Screen 3.1 subtitle |
| Flow 4 | Added Screen 4.0 (empty state with 0 entries) as a retention-critical screen. Added "tap to filter" interaction to ingredient view description. Added bottom tab bar to all main screens |
| Flow 5 | Added Screen 5.0 (empty state). Added Segment F prior condition field in PDF preview layout |
| Flow 6 | Added explicit constraint: counts only, no percentages, no statistical language — regulatory requirement |

**FigJam corrections to apply manually:**

- Flow 2: rename node from "Trigger Check" → "Ingredient Review + Trigger Alert"
- Flow 3: add note that both notification paths render the same screen with dynamic copy; add 3.N3 nudge node
- Flow 4: add empty state (0 entries) as a node before the <3 days state
- Flow 5: add empty state node as entry point when no data exists

---

## CDO Revision Notes — Phase D (2026-03-04)

Changes applied to prompts vs. Phase C version, following all-hands review (docs/08) and founder risk mitigations (docs/09):

| Flow | Change |
| ---- | ------ |
| Flow 3 | Added Frame 3.N3 — symptom nudge notification (triggered when user logs meals for 2+ days with zero symptom entries) |
| Flow 5 — Screen 5.2 | Removed bar chart placeholder. Replaced SYMPTOM OVERVIEW with plain text: "Symptomatic days: X / 14 — Average severity: X.X / 5". Added second button: "Generate doctor link 🔗" below the native share button |
| Flow 6 — Screen 6.1 | Removed symptom timeline table (3-row per-meal breakdown). MVP shows only two counts: meals containing ingredient + meals with symptoms. Timeline deferred to V1.1 |
