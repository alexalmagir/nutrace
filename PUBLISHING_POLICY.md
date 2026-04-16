# Nutrace — Publishing Policy

> This file governs what is published to GitHub from this repository and what must stay private. Paired with `PUBLIC_PRIVATE_MAP.md`.

---

## Purpose of this repository

This repository is a **showcase / portfolio repository**. Its goals are:

1. Demonstrate how a Senior Technical Product Manager works end-to-end with AI tools — from market research and discovery through architecture, delivery, and launch.
2. Show publicly that serious AI-native product work is organized, structured, and evidence-based.
3. Preserve the economic value and intellectual property of Nutrace itself.

It is **not open source**. See [LICENSE](LICENSE) for the restrictive license terms.

---

## The two-layer model

| Layer | Purpose | Typical contents |
|---|---|---|
| **PUBLIC** | Showcase of process, thinking, and capability | `README.md`, `docs/`, `docs/public/`, `assets/`, public governance files |
| **PRIVATE** | Internal operating mechanics | `.claude/agents/`, `.claude/rules/`, `.claude/skills/`, `.mcp.json`, `.env*` |

Everything under `.gitignore` is PRIVATE. Everything tracked by git is PUBLIC.

See [PUBLIC_PRIVATE_MAP.md](PUBLIC_PRIVATE_MAP.md) for a per-path classification.

---

## What this repository publishes

The public layer shows:

- **Product thinking** — project charter, PRD-Lite, user segments, jobs-to-be-done
- **Market research & discovery** — competitive analysis, validation plan, interview methodology
- **Architecture thinking** — technical architecture doc, implementation plan, data model rationale
- **AI-assisted workflow** — session-by-session build log, transparent methodology notes
- **Repository organization** — how the studio and product layers are separated and coordinated
- **Lessons learned** — what worked, what didn't, what changed

## What this repository does NOT publish

The private layer protects:

- **Raw AI agent definitions** — the markdown files that define how each agent behaves, under `.claude/agents/`
- **Raw operational rules** — internal rulebooks under `.claude/rules/`
- **Reusable operational skills** — under `.claude/skills/`
- **Secrets and tokens** — `.mcp.json`, `.env*`, credentials
- **Local Claude Code state** — caches, logs, local settings overrides
- **Internal planning drafts** — private notes, not-yet-curated material

The `.claude/` folder is explicitly governed: its `README.md` is public and explains *that* the agent system exists; the raw agent files themselves are gitignored.

---

## Agent system publishing rule

> **Raw `.claude/agents/*.md` files are NEVER published.**

The existence of the agent system, the role each agent plays at a high level, and how the studio+product layers coordinate IS publicly documented — through curated docs in `docs/public/`:

- [docs/public/agent-system-overview.md](docs/public/agent-system-overview.md)
- [docs/public/venture-studio-operating-model.md](docs/public/venture-studio-operating-model.md)
- [docs/public/nutrace-technical-delivery-model.md](docs/public/nutrace-technical-delivery-model.md)

This lets the repository demonstrate *that* a serious multi-agent system is in use, without exposing the raw prompts, internal heuristics, or reusable operational logic that make the system valuable.

---

## Repository structure publishing rule

The commented tree and explanation of how this repository is organized — including both the AI Product Builder venture studio layer AND the Nutrace product layer — is published at:

- [docs/public/repository-structure.md](docs/public/repository-structure.md)

This shows the two-level organization without exposing raw internals.

---

## Decision rules

**Publish if content:**
- demonstrates product, research, architecture, or delivery capability
- strengthens the portfolio / builder signal
- does not weaken ownership or replication barriers

**Keep private if content:**
- reveals raw agent definitions or prompts
- exposes proprietary implementation logic
- contains secrets or credentials
- reveals monetization-sensitive strategy in detail
- makes cloning the product materially easier

When in doubt: keep it private. Public-safe derivations can always be added later.

---

## How to update

1. Classify any new file in [PUBLIC_PRIVATE_MAP.md](PUBLIC_PRIVATE_MAP.md) before committing.
2. If a private file should have a public summary, create it in `docs/public/` and mark the private file as 📝 DERIVED in the map.
3. If `.gitignore` needs updating to protect something new, do it in the same commit that adds the new content.
4. Historical note: some early docs were already committed to this repository before this policy was formalized. They remain public as originally written; going forward, new sensitive content flows into `.claude/` or other gitignored paths.
