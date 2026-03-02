# Nutrace — Competitive Analysis

> **Document type:** Market Intelligence
> **Phase:** C → D transition
> **Authors:** Chief of Staff (coordination) · CPO (market + positioning analysis) · CMO (messaging + UVP assessment)
> **Date:** 2026-03-02
> **Status:** Final — approved for CTO handoff

---

## 1. Competitor Profiles

### 1.1 mySymptoms

**Category:** Food + symptom diary (manual)
**Platform:** iOS + Android
**Users:** 800,000+
**Rating:** 4.6/5 (iOS)
**Price:** Free (limited) + premium (~$4.99)
**Active:** Yes

**Positioning:** The most clinically-credible manual diary on the market. Statistical correlation analysis that surfaces patterns over time.

**Value Proposition:** "Track your food and symptoms to discover what triggers your digestive problems."

**Core Features:**

- Manual food + symptom entry (free-text + structured)
- Barcode scanning (food database)
- Statistical correlation analysis (pattern detection)
- mySymptoms Clinic portal — HCPs can view patient logs online
- PDF + CSV export for clinicians

**Target segments:** IBS/IBD patients, GERD sufferers, food intolerance seekers. Both self-managed and clinician-referred.

**Clinical positioning:** Strongest clinical credibility of any consumer app. Clinician portal is unique in the market.

**Key weaknesses:**

- Manual entry creates friction — documented adherence drop-off beyond 14 days
- No AI for capture (no vision, no voice)
- No proactive trigger warnings before eating
- Pattern emerges slowly (statistical, not predictive)
- UI dated

---

### 1.2 Bowelle

**Category:** Food + symptom diary (manual)
**Platform:** iOS only
**Users:** ~100,000 estimated (2,100+ ratings)
**Rating:** 4.74/5
**Price:** Free (limited) + $3.99/month or $29.99/year
**Active:** Yes

**Positioning:** Clean, IBS-focused food diary for iOS users. Design-first among established competitors.

**Value Proposition:** "Track your IBS symptoms and identify food triggers."

**Core Features:**

- Manual food + symptom entry
- IBS-specific symptom tracking (Bristol Stool Chart)
- Trigger identification (manual correlation)
- Email export (basic PDF)
- Journaling (notes per entry)

**Target segments:** IBS patients, iOS-only users who value clean design. Self-managed, not clinician-connected.

**Key weaknesses:**

- iOS only — no Android
- No AI (no vision, no voice, no ML pattern detection)
- Export is basic — not clinician-grade
- No clinical sharing or HCP portal
- Pattern detection is manual, not automated

---

### 1.3 Cara Care → Mahana (absorbed into Nerva, May 2025)

**Category:** Food + symptom diary + dietitian program
**Status:** Cara Care acquired by Mahana (Mar 2024) → Mahana absorbed by Nerva (May 2025) — **market exit**
**Rating (at peak):** 4.78/5
**Price:** Free + dietitian program (subscription)

**Positioning:** Clinical-grade diary + human dietitian support. DiGA-reimbursed in Germany (prescription digital therapeutic equivalent). Most sophisticated clinical positioning pre-acquisition.

**Value Proposition:** "Get relief from IBS with evidence-based support from a specialist dietitian."

**Core Features:**

- Manual food + symptom diary
- Evidence-based protocols (FODMAP elimination)
- In-app dietitian program (human coach)
- DiGA certification (Germany) — insurance-reimbursable
- PDF export for GPs/gastros

**Target segments:** Medically-referred IBS patients, German market (DiGA), users who want human professional support.

**Current status:** Brand discontinued. Users migrating to Nerva. No active development.

**Competitive implication:** The strongest clinical competitor has exited the market. The clinical+consumer slot is now open.

---

### 1.4 Nerva

**Category:** Gut-brain hypnotherapy — NOT a food diary
**Platform:** iOS + Android
**Users:** 300,000+
**Clinicians recommending:** 11,000+
**Rating:** 4.7/5 (12,000+ reviews)
**Price:** $19.99/month or $199/year
**Active:** Yes

**Positioning:** Clinically-validated gut-brain therapy. Absorbed Mahana IBS (FDA-cleared CBT) and Cara Care. Positioned as the leading prescription digital therapeutic for IBS.

**Value Proposition:** "Gut-brain hypnotherapy that actually works. Clinically proven to reduce IBS symptoms."

**Core Features:**

- Gut-directed hypnotherapy sessions (audio)
- CBT-based modules (from Mahana IBS)
- Progress tracking (symptom severity)
- Clinician referral pathway

**Target segments:** IBS patients seeking non-pharmacological therapy. Clinician-referred. Post-diagnosis (confirmed IBS).

**Assessment for Nutrace:** NOT a direct competitor. Nerva is a therapy app, not a food or symptom diary. Different JTBD: relief vs. understanding. No food tracking, no ingredient detection, no clinical export. Potential future **partner** — patients could use Nutrace to track triggers alongside Nerva therapy.

---

### 1.5 Mahana IBS (FDA-cleared — wound down)

**Category:** Prescription digital therapeutic (PDT)
**Status:** Being wound down (absorbed into Nerva, May 2025)
**Regulatory:** FDA De Novo clearance (2020) — first FDA-cleared prescription IBS therapy

**Positioning:** Evidence-based, physician-prescribed CBT for IBS. Required doctor prescription to access.

**Assessment for Nutrace:** Prescription-gated, therapy-focused (CBT) — not a diary or trigger-finder. Effectively exited market. No competitive overlap with Nutrace MVP. Confirms regulatory risk of claiming therapeutic function.

---

### 1.6 LivingWith UC (Pfizer)

**Category:** Disease management app (pharma-sponsored)
**Platform:** iOS + Android
**Price:** Free (pharma-funded)
**Target:** Ulcerative Colitis (UC) patients — post-diagnosis

**Positioning:** Pfizer-sponsored disease management and symptom tracking for UC patients already on treatment.

**Value Proposition:** "Track, understand, and manage your UC."

**Core Features:**

- Manual symptom tracking
- Medication tracking
- Flare tracking (UC-specific)
- PDF export (recently added)
- Integration with Pfizer patient programs

**Target segments:** Diagnosed UC patients on biologic therapy. Does NOT target IBS or undiagnosed patients.

**Assessment for Nutrace:** Pharma-sponsored, UC-specific, post-diagnosis. No overlap with Nutrace's ICP (undiagnosed, pre/during diagnosis, broad GI). Not a competitive threat.

---

### 1.7 New AI Entrants (2024–2025)

#### EatSense

- **Category:** AI food diary (photo + voice)
- **Platform:** iOS + Android
- **Launched:** 2024
- **Positioning:** Gut health + food sensitivity discovery via AI photo capture
- **Key gap:** Consumer wellness focus; no proactive personal correlation alerts; no symptom tracking layer; no clinician-grade PDF; no clinical sharing

#### Gut AI

- **Category:** AI food photo analyzer
- **Platform:** iOS (iOS 18+)
- **Price:** $6.99/month
- **Positioning:** Photo → identifies 10 gut irritants per meal
- **Key gap:** Population-level FODMAP/irritant lookup only — not personal symptom correlation; no symptom tracking; no clinical export; no voice
- **Validation:** Confirms vision AI is technically feasible and user-accepted for food capture. Does NOT correlate with personal symptom history — no proactive alert capability.

#### Gutly

- **Category:** AI FODMAP analyzer
- **Platform:** iOS
- **Rating:** 4.53/5 (77 ratings)
- **Positioning:** "GutAI™ FODMAP analysis" from photo or text; lab-verified food database
- **Key gap:** FODMAP lookup only (no personal symptom correlation); no clinical export; wellness positioning only

#### Gut Lens

- **Category:** AI FODMAP photo analyzer
- **Platform:** iOS
- **Positioning:** Photo → FODMAP breakdown; "AI learns your patterns"
- **Key gap:** Pattern = FODMAP tolerance (population-level), not personal symptom correlation; no clinical PDF; no voice

**Critical insight on all AI entrants:** They use vision AI as a **lookup tool** (photo → FODMAP database query) rather than as a **personal correlation engine** (photo → this user's symptom history → proactive alert). This is a fundamentally different JTBD. All are wellness-positioned, not clinical.

---

## 2. Feature Comparison Matrix

| Feature | Nutrace (MVP) | mySymptoms | Bowelle | Cara Care | EatSense | Gut AI | Gutly |
| --------- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Vision AI capture** | ✅ | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Voice capture (STT)** | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Manual entry** | ❌ MVP | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| **Proactive trigger alert** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Personal symptom correlation** | ✅ (AI) | ✅ (statistical) | ⚠️ (manual) | ⚠️ (manual) | ❌ | ❌ | ❌ |
| **FODMAP lookup** | ❌ MVP | ❌ | ❌ | ✅ | ❌ | ✅ | ✅ |
| **Delayed check-in prompts (2h/4h)** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Pattern view (≥3 days)** | ✅ | ✅ | ⚠️ | ✅ | ❌ | ❌ | ❌ |
| **Clinical-grade PDF export** | ✅ (severity + disclaimer) | ✅ (basic) | ❌ (email only) | ✅ | ❌ | ❌ | ❌ |
| **HCP sharing portal** | ❌ (V2) | ✅ (Clinic) | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Eating disorder contraindication screen** | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| **Undiagnosed/in-diagnosis ICP** | ✅ | ✅ | ✅ | ❌ (DiGA = diagnosed) | ✅ | ✅ | ✅ |
| **Android support** | ✅ | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Active development** | ✅ | ✅ | ✅ | ❌ (wound down) | ✅ | ✅ | ✅ |

---

## 3. Positioning Map

### Axes

- **X-axis:** Capture friction — High (100% manual entry) → Low (AI-first, photo + voice)
- **Y-axis:** Clinical orientation — Wellness/self-care → Clinical/doctor-ready

```text
                         CLINICAL / DOCTOR-READY
                                   │
                                   │
          mySymptoms ●             │              ★ NUTRACE (target)
          (best clinical,          │       (AI capture + clinical PDF)
           manual entry)           │
                                   │
 ─────────────────────────────────────────────────────────────────────
 HIGH FRICTION                     │                    LOW FRICTION
 (manual entry)                    │             (AI / photo capture)
                                   │
    Bowelle ●                      │
    (clean design,                 │
     manual, no clinical)          │      EatSense ●
                                   │                         Gut AI ●
    LivingWith UC ●                │                         Gutly ●
    (pharma, narrow segment)       │                         Gut Lens ●
                                   │
                         WELLNESS / SELF-CARE
```

**Notes:**

- Cara Care (top-left, clinical+manual) **exited the market** May 2025 — slot is now open
- Nerva is off-map — therapy, not diary; different JTBD
- Mahana IBS (prescription PDT) is off-map — exited market

**White space confirmed:** The top-right quadrant (low friction + clinical orientation) is **empty**. mySymptoms holds top-left (best clinical, manual). AI entrants occupy bottom-right (low friction, wellness). No competitor combines both dimensions.

---

## 4. Conclusion — UVP Assessment and Recommendations

### 4.1 Does Nutrace Have a Unique Value Proposition?

**Yes. The UVP is confirmed and defensible.**

No current competitor combines:

1. **Vision AI + voice capture** — lowest friction in the market
2. **Proactive personal correlation alerts** — unique; zero competitors have this
3. **Clinical-grade PDF export** with severity indicator and regulatory disclaimer
4. **In-diagnosis ICP** — the hardest-to-reach, highest-value patient moment

The closest competitor on clinical credibility (mySymptoms) has zero AI and no proactive alerts. The closest competitors on AI capture (Gut AI, Gutly, Gut Lens) have no symptom tracking and no clinical output. These are not converging — they occupy different quadrants by design.

**Nutrace occupies a unique position that no current competitor holds or is actively moving toward.**

---

### 4.2 Positioning Statement Assessment

**Current (from CLAUDE.md):** "Frictionless food and symptom diary for digestive patients — photo + voice, not forms."

**Assessment:** Accurate but undersells the two strongest differentiators:

1. The proactive alert ("warns you before you eat") is the sharpest hook — no competitor has it
2. The clinical PDF ("your doctor can actually use") separates Nutrace from wellness AI apps

The current framing emphasizes friction reduction, which is a means, not the core value. The outcome — pattern discovery before your next meal, and a record your doctor trusts — is the value.

---

### 4.3 Recommended Positioning (refined)

**For the patient:**
> "Nutrace watches your patterns so you don't have to. Photograph your meal — we'll warn you if something in it has triggered your symptoms before. After, record how you feel with a voice note. In days, you and your doctor will see what your gut has been trying to tell you."

**For the HCP:**
> "Your patients won't maintain a paper diary. Nutrace captures meals by photo, symptoms by voice, and exports a structured 14-day log — severity indicators included — as a PDF you can act on."

**One-liner (App Store / LinkedIn):**
> "The food diary that warns you before you eat — and gives your doctor a log they can actually use."

---

### 4.4 What Should We Change?

| Area | Current | Recommendation | Rationale |
| ------ | --------- | ---------------- | ----------- |
| **Core positioning** | Keep | No change needed | White space confirmed. UVP is real and unoccupied. |
| **Proactive alert messaging** | Lead with it | Lead with it in ALL messaging | No competitor has this. It is Nutrace's sharpest differentiator and clearest hook. |
| **ICP (undiagnosed / in-diagnosis)** | Keep | No change | Most underserved moment. Best retention driver (high anxiety, high motivation to track). |
| **Clinical PDF** | Keep + emphasize | Make export more prominent in onboarding messaging | mySymptoms proves HCPs value structured data. Nutrace's PDF is better (severity + disclaimer). |
| **Voice input** | Keep optional | No change | Phase B validated: friction is the problem, mandatory voice is not the solution. |
| **FODMAP lookup** | Out of scope MVP | Keep out of scope | Gut AI / Gutly / Gut Lens own this positioning. Nutrace's angle is personal correlation, not population-level lookup. Adding FODMAP would dilute and not differentiate. |
| **HCP portal** | Planned for V2 | Accelerate to V1.5 | mySymptoms Clinic portal is a real moat. If mySymptoms adds vision AI before Nutrace adds the portal, they could reclaim the clinical+AI quadrant. |
| **Monetization model** | Not yet defined | Consider: free for patients / subscription for HCPs | Nerva $199/year. mySymptoms charges patients. Nutrace could be patient-free to maximize adoption, HCP portal subscription (V2) to monetize the clinical side. |

---

### 4.5 Competitive Risks

| Risk | Likelihood | Impact | Mitigation |
| ------ | ----------- | -------- | ------------ |
| mySymptoms adds vision AI capture | Medium (12–18 months) | High | Launch and establish user base before they respond. First-mover advantage in top-right quadrant. |
| Gut AI / Gutly adds symptom tracking + clinical PDF | Low — different JTBD, requires full pivot | Medium | Clinical credibility + ICP focus creates switching cost. These apps have no symptom layer today. |
| Nerva enters tracking space | Low | Medium | Nerva's moat is therapy (hypnotherapy + CBT). Entering food diary would dilute. |
| Pharma-sponsored clinical app enters (like LivingWith UC for IBS) | Low-Medium | Medium | Pharma apps are condition-specific and require diagnosed patients. Nutrace's ICP (undiagnosed) is not addressable by pharma. |

---

### 4.6 Market Timing Assessment

**Market timing is favorable. Act in the next 12 months.**

- **Cara Care / Mahana have exited** — the strongest clinical competitor is gone; the clinical slot is open
- **Mahana IBS wound down** — the FDA-cleared PDT competitor eliminated; no new clinical entrant yet
- **AI entrants are moving fast in wellness** — if Nutrace doesn't claim the clinical+AI quadrant within 12–18 months, it risks being repositioned (or perceived) as "another wellness AI food app"
- **IBS prevalence rising** — post-COVID surge documented (6.1% → 11%); total addressable population growing
- **HCP openness to digital tools** — accelerated post-COVID; telehealth normalization reduces resistance to app-supported care

**Window: 12–18 months before mySymptoms responds with AI or a new clinical AI entrant appears.**

---

## 5. Summary

| Question | Answer |
| ---------- | -------- |
| Do we have a UVP? | **Yes** — proactive personal correlation alert + clinical PDF + AI capture. Unique combination. No competitor has it. |
| Should we change positioning? | **No change to strategy.** Refine messaging to lead with the proactive alert, not just friction reduction. |
| Should we change core features? | **No.** MVP scope is correct. Proactive alert is the hook; clinical PDF is the closer. |
| What should we prioritize post-MVP? | **HCP portal (V1.5).** mySymptoms Clinic portal is a moat — we need feature parity before they respond with AI. |
| Biggest competitive risk? | mySymptoms adding AI capture. Timeline: 12–18 months. Action: launch, establish, and grow before they respond. |
| Market timing? | **Favorable.** Cara Care / Mahana exited, AI wave validates capture approach, IBS prevalence rising. |

---

*Prepared by: CPO + CMO, coordinated by Chief of Staff.*

*All competitive data sourced from public information: App Store listings, company websites, press releases, and industry sources as of March 2026.*

*This document is a living artifact — update as competitive landscape evolves.*
