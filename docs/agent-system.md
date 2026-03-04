# Nutrace — AI Agent System

> How this product is being built: a multi-agent AI system collaborating with a Senior Technical PM across every phase of a 0-to-1 product lifecycle.

---

## Overview

Nutrace is not being built with a single AI assistant. It is being built with a **coordinated system of six specialized AI agents**, each assigned a distinct role, a defined set of responsibilities, and specific artifacts to produce. The system is operated and directed by a Senior Technical PM (Alexandre Maravilla), who sets strategy, makes all key decisions, and controls what gets committed.

The goal is not to replace the PM — it is to give a single person the **depth and throughput of a full product team** during the critical 0-to-1 phase.

---

## Why a Multi-Agent Architecture

Building a product from zero involves fundamentally different cognitive modes: market skepticism (Founder), user empathy (CPO), visual thinking (CDO), systems architecture (CTO), and narrative framing (CMO). A single generalist AI assistant optimizes for none of these — it averages them.

By assigning each mode to a dedicated agent with a defined role, internal "personality," and set of constraints, the system produces outputs that are sharper, more consistent, and easier to review than what a single assistant would generate.

Critically: **agents disagree with each other**. The CPO and Founder argue about scope. The CDO and CTO negotiate constraint tradeoffs. The CMO pushes for positioning that the CPO has to ground in evidence. This tension is designed in — it is how real product teams work.

---

## The Six Agents

| Agent | Role | Primary responsibility | Key artifacts |
| --- | --- | --- | --- |
| **Chief of Staff** | Session orchestrator | Sequences work, enforces scope, blocks drift, ensures every session produces an artifact | Session briefs, handoff checklists |
| **Founder** | Market thesis + GO/NO-GO | Validates market opportunity, stress-tests business viability, makes the GO decision | Venture brief, founder scorecard |
| **CPO** | Product | ICP definition, hypothesis design, validation synthesis, PRD, metrics | PRD-Lite, validation plan, OKRs |
| **CDO** | Design | User flows, interaction design, wireframes, UX constraints | UX flows and wireframes |
| **CTO** | Engineering | Architecture decisions, stack selection, implementation planning, code | Architecture doc, implementation plan, source code |
| **CMO** | Go-to-market | Positioning, messaging, app store copy, LinkedIn, launch narrative | GTM doc, README, launch materials |

Each agent has a defined activation point in the project timeline. Agents are not all running simultaneously — they are activated in sequence as the project reaches the phase where their domain is relevant.

---

## How the System Works

### The Human Role

Alexandre Maravilla operates as the **system director**:

- Sets the strategic brief at the start of each session
- Decides which agents to activate and in what order
- Reviews all agent outputs before they become decisions
- Makes all judgment calls where agents surface tradeoffs
- Controls what gets committed to GitHub — nothing ships without his sign-off

The AI drafts, synthesizes, analyzes, and argues. The human decides.

### The Chief of Staff Role

The Chief of Staff is the first agent activated in every session. Its job is:

1. Read the current project state (CLAUDE.md)
2. Determine which phase the project is in and what the next artifact should be
3. Activate the appropriate agent(s) for the session
4. Enforce scope — flag any output that exceeds MVP boundaries
5. Ensure the session ends with a committed artifact, not just a conversation

The Chief of Staff does not produce product artifacts. Its output is structure and sequencing.

### Agent Collaboration Patterns

Three collaboration patterns are used across the project:

**Sequential:** One agent produces an artifact that becomes the input for the next. The Founder's venture brief informs the CPO's ICP definition, which informs the CDO's UX flows, which informs the CTO's architecture.

**Adversarial:** Two agents argue opposite sides of a decision. Example: CMO proposes a product name; CPO challenges it against brand and product constraints; the human decides.

**Parallel review:** Multiple agents review the same artifact from their domain perspective. Example: the CDO and CTO both review the PRD-Lite — the CDO for UX feasibility, the CTO for technical feasibility.

---

## Project Phases and Agent Activation

| Phase | Name | Agents active | Key output |
| --- | --- | --- | --- |
| A | Ideation / Selection | Chief of Staff, Founder, CPO (naming), CMO (naming) | GO decision, venture brief, ICP, project name |
| B | Validation | Chief of Staff, CPO, CDO | Hypothesis framework, synthetic interview research, H1/H2 validation, user segmentation |
| C | Definition | Chief of Staff, CPO, CDO | PRD-Lite, UX flows and wireframes |
| D | Build | Chief of Staff, CTO, CDO | Architecture, implementation plan, source code |
| E | Launch | Chief of Staff, CMO, CPO | App Store listing, GTM doc, LinkedIn posts, launch metrics |

The system is phase-gated. No agent begins Phase D work before Phase C artifacts are complete and committed. This is enforced by the Chief of Staff.

---

## Artifact Ownership Map

Each document in this repository has a single agent owner responsible for producing it. Other agents may review, but ownership is clear.

| File | Owner | Status |
| --- | --- | --- |
| `docs/00-project-charter.md` | Chief of Staff + Founder | Done |
| `docs/01-founder-venture-brief.md` | Founder | Done |
| `docs/03-validation-plan-and-results.md` | CPO + CDO | Done |
| `docs/04-prd-lite.md` | CPO | Done |
| `docs/05-ux-flows-and-wireframes.md` | CDO | Pending |
| `docs/06-tech-architecture.md` | CTO | Pending |
| `docs/07-implementation-plan.md` | CTO | Pending |
| `docs/08-decisions-log.md` | All agents | Pending |
| `docs/09-metrics-and-instrumentation.md` | CPO | Pending |
| `docs/10-gtm-and-messaging.md` | CMO | Pending |
| `docs/11-demo-script.md` | CMO + CDO | Pending |
| `src/` (application code) | CTO | Pending |

---

## Memory and Context Architecture

The agent system maintains persistent context across sessions through a structured memory file (`CLAUDE.md` in the project root). This file is read at the start of every session and contains:

- Current project phase and status
- ICP definition and user segments
- MVP scope (in and out)
- Key decisions log with dates and rationale
- Agent team status
- Critical hypotheses and their validation results

This allows the system to maintain continuity across sessions without requiring the human to re-brief agents from scratch each time. The Chief of Staff is responsible for keeping `CLAUDE.md` current after every session.

---

## What the System Does Not Do

To be clear about the boundaries:

- **Does not make strategic decisions.** All product strategy, scope calls, and go/no-go decisions are made by Alexandre. Agents surface options and tradeoffs; they do not choose.
- **Does not commit to GitHub autonomously.** Every commit is reviewed and approved by Alexandre before it goes to the repository.
- **Does not conduct real user research.** Phase B validation used synthetic (AI-generated) interview simulations to stress-test hypotheses. Real-user validation was done by Alexandre directly. This is documented transparently in `docs/03-validation-plan-and-results.md`.
- **Does not hallucinate market data.** All market claims in this repo link to primary sources. If a source cannot be found, the claim is not included.

---

## Why Build This Way

This project is a deliberate demonstration of what a Senior Technical PM can execute alone in 2026, using AI as a force multiplier.

The traditional 0-to-1 product process requires: a Founder for market conviction, a CPO for product clarity, a CDO for design, a CTO for architecture, a CMO for launch. In a startup, that's 5 people, months of coordination, and significant equity dilution before a single line of code is written.

This system compresses that to one person and a structured AI architecture — with the same rigor, the same phase gating, and the same artifact quality.

Every document in this repo is real work, not a demo. The decisions are real, the tradeoffs are real, and the limitations are documented honestly.

**The point is not "AI did this." The point is: this is what execution looks like now.**

---

## Full Build Transparency

Every session — what was asked, what was produced, what the human decided, and what got committed — is logged in [`docs/ai-build-log.md`](ai-build-log.md).
