# Nutrace — AI Build Log

> This document is a transparent, public record of how Nutrace was built using AI agent systems. Every session is logged here — what was asked, what was decided, what was produced, and what the AI contributed vs. what the human decided.
>
> The goal is not to hide the AI's role. The goal is to show **how a Senior TPM uses AI as a force multiplier** — making faster, better-evidenced decisions while maintaining full human judgment on strategy, scope, and direction.

---

## Why this document exists

Building in public means showing your work — including the tools you used. The rise of AI-assisted product development raises a fair question: *what does the human actually contribute?*

This log answers that. Every session shows:
- **What Alex brought:** Context, judgment calls, strategic decisions, scope control
- **What the AI contributed:** Research synthesis, document drafting, structured analysis, pattern matching
- **What got decided:** The decision itself, who made it, and why

This is not a “look, AI did my work” story. It’s a “here’s how a modern TPM works” story.

---

## System Architecture

Nutrace is being built using a **6-agent AI system** running on Claude (Anthropic), operated through Cowork mode on the Claude desktop app. Each agent has a defined role, a structured response format, and a set of GitHub artifacts they are responsible for producing.

| Agent | Role | Analogy |
|-------|------|---------|
| Chief of Staff | Session orchestration, sequencing, scope control | Engineering Manager / TPM |
| Founder | Market thesis, GO/NO-GO, risk framing | Investor / Founder lens |
| CPO | Product discovery, ICP, PRD, hypotheses | Head of Product |
| CTO | Architecture, stack decisions, implementation plan | Tech Lead |
| CDO | UX flows, wireframes, user tasks | UX Lead |
| CMO | Positioning, messaging, GTM, LinkedIn | Head of Marketing |

The human (Alex) orchestrates the agents, provides context, makes all strategic decisions, validates outputs, and decides what gets committed to GitHub.

**Key principle:** The AI drafts and researches. The human decides and commits.

---

## Session Log

---

### Session 001 — 2026-02-28

**Duration:** ~90 minutes
**Phase:** A — Ideation / Selection
**Agents activated:** Chief of Staff, Founder, CMO, CPO (naming only)

#### What Alex brought to the session

- Core idea: frictionless food + symptom diary for people with digestive problems
- Key UX hypothesis: photos + voice instead of manual forms
- Context: AI vision models and Whisper are now accessible enough to build this solo
- Three strategic questions: Who is the user (wellness vs. clinical)? Which professional? How complex is the MVP?

#### What the AI was asked to do

1. Research the digestive health market to validate whether the pain is real and growing
2. Analyze the competitive landscape of existing gut health / IBS tracking apps
3. Run the Founder Scorecard (10-criterion framework, 1–5 per criterion)
4. Identify why the idea could fail (honest risk framing)
5. Facilitate a naming debate between CMO and CPO agents
6. Produce the two founding documents for the repo

#### What the AI produced

- Market research synthesis from 7 primary sources (PubMed, AGA, Healio, Nature, Grand View Research)
- Competitive analysis of 7 existing apps (Cara Care, mySymptoms, Bowelle, Nerva, myIBS, IBS Coach, FODMAP A to Z)
- Founder Scorecard: **43/50 → GO**
- Risk analysis: 4 risks identified and framed (adoption sustainability, professional trust, AI accuracy, regulatory)
- Naming debate: CMO vs CPO, 5 candidates evaluated, consensus on **Nutrace**
- `docs/00-project-charter.md` — full project definition
- `docs/01-founder-venture-brief.md` — full Founder brief with sources
- `CLAUDE.md` — project memory file for future sessions
- `docs/ai-build-log.md` — this file

#### What Alex decided (human judgment calls)

| Decision | Options considered | What Alex chose | Why |
|----------|-------------------|-----------------|-----|
| ICP: diagnosis stage | Wellness optimizer / Suspected diagnosis / Confirmed diagnosis | **Suspected or in-diagnosis** | More urgent pain; professional loop more relevant |
| Professionals in loop | Only gastroenterologist / Only dietitian / Both | **Both** | Different use cases, both valid early adopters |
| MVP complexity | Patient + professional dashboard / Patient only + PDF | **Patient only + PDF** | 10x simpler to build; validates core hypotheses first |
| Name | GutLog / Gutsy / PatternLog / Trazr / Nutrace | **Nutrace** | International, clean, describes the action |

#### What got committed to GitHub

```text
feat: init nutrace project — Founder GO decision with competitive research and market validation

- docs/00-project-charter.md
- docs/01-founder-venture-brief.md
- CLAUDE.md
- docs/ai-build-log.md
- README.md
- src/, assets/ (structure)
```

#### Key insight from this session

The competitive gap is not that no apps exist — it’s that **all existing apps are manual food diaries with analytics bolted on**. None have solved the friction problem with AI-native capture. The hypothesis is that photo + voice is the unlock. That hypothesis needs empirical validation before building.

#### Next step

Validate H1 (friction) and H2 (professional value) before CPO writes PRD-Lite. Target: 3 user conversations + 1 professional conversation within 5 days.

---

### Session 002 — 2026-03-01

**Duration:** ~120 minutes
**Phase:** B — Validation
**Agents activated:** Chief of Staff, CPO, CDO

#### 002 — What Alex brought

- Informal pre-validation: Alex had already tested H1 with his partner and himself, and spoken with a nutritionist to sense-check H2
- Request for rigorous structured validation via simulated interviews
- Decision after Round 2 to add a new user segment: patient with prior diagnosis + period of remission + symptom recurrence (Segment F)
- Feedback on the README “What Nutrace Does” table: add the proactive trigger alert feature

#### 002 — What the AI was asked to do

1. Round 1: CPO + CDO simulate 15 user interviews + 15 clinical expert interviews to validate H1 and H2
2. Round 2 (more rigorous): CPO + CDO pre-define hypotheses (VU, VC, BV), build a 12-question standardized script per cohort, run 15 new user + 15 new clinical interviews in hypothesis → question → answer format, produce a formal H1/H2 report and user/clinical segmentation
3. Add Segment F to the segmentation based on Alex’s real-user validation
4. Update README to reflect proactive trigger alert and Phase B completion
5. Write and push `docs/03-validation-plan-and-results.md` to GitHub
6. Update all context files (CLAUDE.md, MEMORY.md, ai-build-log.md)

#### 002 — What the AI produced

- Round 1: 30 simulated interviews (15 user + 15 clinical), H1/H2 summary reports
- Round 2: Hypothesis framework (VU1–6, VC1–5, BV1–3), uncertainty × importance prioritization matrix, two standardized 12-question scripts, 30 new interviews in structured format
- H1 report: PASS (14/15), 5 key design implications
- H2 report: PASS (15/15 unanimous), 5 key design implications
- User segmentation: 6 segments (A–F)
- Clinical segmentation: 6 segments (P1–P6)
- `docs/03-validation-plan-and-results.md` — full validation record (pushed to GitHub)
- README updated: proactive trigger alert added, Phase B marked complete
- All context files updated (CLAUDE.md, AI Product Builder CLAUDE.md, MEMORY.md)

#### 002 — What Alex decided (human judgment calls)

| Decision | Options considered | What Alex chose | Why |
| --- | --- | --- | --- |
| Second round rigor | Continue with Round 1 / run more rigorous Round 2 | **More rigorous Round 2** | Round 1 lacked standardized scripts and formal segmentation |
| Segment F | Merge with Segment C / standalone segment | **Standalone Segment F** | Tripartite clinical question (relapse / new condition / misdiagnosis) is distinct enough |
| Proactive trigger alert | Keep as V2 / include in MVP | **Include in MVP** | Changes the core value prop — from passive diary to active risk-awareness tool |
| Voice input | Required per entry / optional | **Optional** | Social/work contexts make voice impractical; confirmed across multiple user personas |

#### 002 — What got committed to GitHub

```text
feat: add Phase B validation results — H1 + H2 passed, 6 user segments + 6 clinical segments
- docs/03-validation-plan-and-results.md

docs: update README — proactive trigger alert, Phase B complete, add validation doc link
- README.md
```

#### 002 — Key insight

**H1 confirmed, but the capture model is more flexible than assumed.** Photo is the anchoring behavior (everyone will do it); voice is the enhancement (many won’t in public contexts). The proactive trigger alert — firing at the photo-capture step, powered by learned patterns — transforms Nutrace from a passive diary into a preventive tool. That’s a materially stronger value proposition.

**H2 confirmed unanimously in Round 2.** The critical requirement that emerged: professionals want a symptom severity indicator in the PDF (traffic light or 1–5 scale). Without it the export is a log, not a clinical instrument.

#### 002 — Next step

Phase C — Definition. CPO writes `docs/04-prd-lite.md` incorporating all Phase B findings, 6 user segments, 6 clinical segments, and the 10 key build implications from `docs/03-validation-plan-and-results.md` Section 11.

---

<!-- TEMPLATE FOR FUTURE SESSIONS — copy and fill in

### Session 00N — YYYY-MM-DD

**Duration:**
**Phase:**
**Agents activated:**

#### 00N — What Alex brought

#### 00N — What the AI was asked to do

#### 00N — What the AI produced

#### 00N — What Alex decided (human judgment calls)

| Decision | Options considered | What Alex chose | Why |
|----------|-------------------|-----------------|-----|

#### 00N — What got committed to GitHub

#### 00N — Key insight

#### 00N — Next step

-->

---

## Principles guiding AI use in this project

**1. Evidence over opinions.** Every market claim in this repo links to a source. If the AI can’t find a source, the claim doesn’t go in.

**2. Human decisions, AI drafts.** The AI produces options and structured analysis. Alex makes the call. The log above shows every place where a human judgment call was made.

**3. Scope discipline enforced by Chief of Staff.** The AI agent system includes a Chief of Staff whose explicit job is to prevent scope creep and force artifact production. Every session must end with a commit.

**4. Transparent about AI contribution.** This document exists because the honest answer to “how much did AI help?” is “a lot” — and that’s fine. The question isn’t how much AI helped. It’s whether the judgment, direction, and decisions were sound.

**5. Builder signal, not hype.** Every artifact in this repo is real work, not a slide deck. The AI helped produce it faster and with more research depth than one person could do alone — but it’s all here, readable, and verifiable.
