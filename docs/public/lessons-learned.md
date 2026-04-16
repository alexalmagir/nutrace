# Lessons Learned

> Cross-session patterns and takeaways from building Nutrace with an AI-native team. Kept honest on purpose — including what didn't work.

---

## What has worked

1. **Chief of Staff first, every session.** Starting cold with a specialist agent produces shallow work. Starting with Chief of Staff produces a session plan that keeps the specialists coherent.
2. **One artifact per session, always committed.** The rule "if it's not in the repo, it doesn't exist" forces the team to produce instead of discuss. It also makes drift visible when it happens.
3. **Two-round validation.** H1 and H2 both needed a second round to pass confidently. Stopping after Round 1 would have baked in false positives. The scorecard + pass threshold kept the bar honest.
4. **Proactive alert at photo-capture.** Users repeatedly told us the value was *before* the meal, not after. Moving the alert from retrospective pattern view to capture-time flow was a direct result of validation, not a design preference.
5. **Segment F emerged from real users.** The "prior diagnosis + relapse" segment wasn't in the original six. Adding it meant an onboarding field and a PDF-header context, both minor build costs for a non-trivial user population.
6. **Separating studio and product layers.** Keeping the executive agents in a local meta-workspace and the technical agents inside the product repo stops IP leakage at the executive level while letting the product work be fully public.

## What has not worked

1. **First PDF draft used a bar chart.** The CDO and CTO both landed on an SVG bar chart before realizing clinicians wanted a text table. Reverted in Session 006.
2. **Too many segments before consolidation.** Early research produced 9 user segments. They collapsed to 6 after clinical feedback. The extra 3 added noise to the PRD.
3. **Early temptation to gate PDF export behind a paywall.** CPO and CMO agreed, then reversed: gating clinical value kills the clinical value proposition. MVP ships with PDF fully unlocked.
4. **Token exposure in early MCP config.** First `.mcp.json` embedded the GitHub token literally. Moved to env-var interpolation + macOS Keychain before any commit, but the lesson stands: secrets management should be set up *before* integrating any MCP server, not after.

## Patterns that keep repeating

- **Constraints clarify scope faster than ideation.** Every time we added a non-negotiable (regulatory framing, PDF unlocked, data residency EU), the downstream decisions got easier, not harder.
- **Agents disagree, and that's useful.** CPO and CTO have disagreed multiple times on scope. Chief of Staff's "detect contradictions between agents" role is what turns those disagreements into decisions instead of churn.
- **Evidence first, build second.** Every committed build decision traces back to either an interview, a preregistered hypothesis, or a regulatory constraint. No "I think" without evidence.

## What to watch next

- **Phase D validation experiments (E1–E7).** If any of them fail, scope has to shrink fast. Details are in internal documentation.
- **Beta success gate:** one clinician's qualitative review of a real patient's PDF. That is the GO/NO-GO for V1.5 investment, not a metric threshold.
- **Retention at 7 days.** If photo-and-voice capture does not sustain logging, everything downstream collapses. This is the hypothesis the MVP is really testing.

## Portability

Most of these lessons are about **how the agent system stays coherent**, not about Nutrace specifically. They will carry over to the next product built under AI Product Builder. That is part of why the two-layer model exists.
