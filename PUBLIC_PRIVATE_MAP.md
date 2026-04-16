# Nutrace — Public/Private Map

> Per-path classification. Paired with [PUBLISHING_POLICY.md](PUBLISHING_POLICY.md). Update this file whenever you add or reclassify content.

## Legend

| Marker | Meaning |
|---|---|
| 🌐 PUBLIC | Tracked by git and pushed to GitHub. |
| 🔒 PRIVATE | Gitignored. Never leaves the local machine. |
| 📝 DERIVED | A curated public-safe summary exists in `docs/public/`; the source material may or may not be public. |

---

## Root files

| Path | Classification | Notes |
|---|---|---|
| `README.md` | 🌐 PUBLIC | Front-door intro with restrictive notice. |
| `LICENSE` | 🌐 PUBLIC | All rights reserved, no open-source grant. |
| `PUBLISHING_POLICY.md` | 🌐 PUBLIC | This governance is itself public so visitors understand the model. |
| `PUBLIC_PRIVATE_MAP.md` | 🌐 PUBLIC | This file. |
| `CLAUDE.md` | 🌐 PUBLIC | Project memory for Claude. Already public as of early history. |
| `.gitignore` | 🌐 PUBLIC | Publishing control itself. |
| `.mcp.json` | 🔒 PRIVATE | MCP server config, may include token references. |

## `docs/` (existing numbered docs — already public)

| Path | Classification | Notes |
|---|---|---|
| `docs/00-project-charter.md` | 🌐 PUBLIC + 📝 DERIVED | Full charter. Summary in `docs/public/project-overview.md`. |
| `docs/01-founder-venture-brief.md` | 🌐 PUBLIC + 📝 DERIVED | Market brief. Summary in `docs/public/market-research-summary.md`. |
| `docs/02-competitive-analysis.md` | 🌐 PUBLIC | Competitive landscape. |
| `docs/03-validation-plan-and-results.md` | 🌐 PUBLIC + 📝 DERIVED | Full validation record. Summary in `docs/public/discovery-summary.md`. |
| `docs/04-prd-lite.md` | 🌐 PUBLIC + 📝 DERIVED | Full PRD. Summary in `docs/public/prd-lite.md`. |
| `docs/05-ux-flows-and-wireframes.md` | 🌐 PUBLIC | CDO full UX spec. |
| `docs/06-tech-architecture.md` | 🌐 PUBLIC + 📝 DERIVED | Full architecture. Summary in `docs/public/architecture-overview.md`. |
| `docs/07-implementation-plan.md` | 🌐 PUBLIC | CTO implementation plan. |
| `docs/08-all-hands-review.md` | 🌐 PUBLIC | Multi-agent review session notes. |
| `docs/09-founder-mitigations.md` | 🌐 PUBLIC | Founder risk mitigations. |
| `docs/10-validation-experiments.md` | 🌐 PUBLIC | Phase D validation experiments E1–E7. |
| `docs/agent-system.md` | 🌐 PUBLIC | Transparency doc about the 6-agent system. |
| `docs/ai-build-log.md` | 🌐 PUBLIC | Session-by-session build log. |
| `docs/competitive-analysis.md` | 🌐 PUBLIC | Alternative competitive analysis. |

## `docs/public/` (curated public navigation layer — newly created)

All files in this folder are 🌐 PUBLIC and 📝 DERIVED. They are concise, portfolio-facing summaries that link to the full internal docs where useful.

| File | Purpose |
|---|---|
| `project-overview.md` | Elevator pitch + status, derived from charter |
| `market-research-summary.md` | Market data summary, derived from founder brief + competitive analysis |
| `discovery-summary.md` | Validation methodology and results, derived from `03-validation-plan-and-results.md` |
| `prd-lite.md` | Public-safe PRD summary, derived from `04-prd-lite.md` |
| `architecture-overview.md` | High-level architecture, derived from `06-tech-architecture.md` |
| `agent-system-overview.md` | Describes the agent system without exposing raw definitions |
| `venture-studio-operating-model.md` | Explains the AI Product Builder studio layer |
| `nutrace-technical-delivery-model.md` | Explains the Nutrace technical agent layer |
| `repository-structure.md` | Commented tree across both layers |
| `ai-product-builder-structure.md` | Studio-level structure detail |
| `nutrace-structure.md` | Product-level structure detail |
| `ai-build-log.md` | Pointer to the main build log |
| `lessons-learned.md` | Cross-session patterns and takeaways |

## `.claude/` (operating system for Claude Code)

| Path | Classification | Notes |
|---|---|---|
| `.claude/README.md` | 🌐 PUBLIC | Public-facing explanation of what this folder is and why the raw files are private. |
| `.claude/settings.json` | 🌐 PUBLIC | Trivial Claude Code settings ({}). Safe to show. |
| `.claude/agents/*.md` | 🔒 PRIVATE + 📝 DERIVED | Raw technical agent definitions. Summary in `docs/public/nutrace-technical-delivery-model.md`. |
| `.claude/rules/*.md` | 🔒 PRIVATE | Coding, architecture, testing, migrations, security, delivery rules. |
| `.claude/skills/*` | 🔒 PRIVATE | Reusable operational skills. |
| `.claude/settings.local.json` | 🔒 PRIVATE | Local Claude Code overrides. |
| `.claude/cache/`, `.claude/logs/` | 🔒 PRIVATE | Local state. |

## `assets/`

| Path | Classification | Notes |
|---|---|---|
| `assets/user-flows/` | 🌐 PUBLIC | FigJam flow links and descriptions. |
| `assets/wireframes/` | 🌐 PUBLIC | Wireframe prompts and descriptions. |
| `assets/social/` | 🌐 PUBLIC | Social media assets. |

## `src/`

| Path | Classification | Notes |
|---|---|---|
| `src/.gitkeep` | 🌐 PUBLIC | Placeholder. Build code landing here will be classified case-by-case as it's written. |

## `.github/`, `.vscode/`, root dotfiles

| Path | Classification | Notes |
|---|---|---|
| `.env*` | 🔒 PRIVATE | Secrets. |
| `.DS_Store` | 🔒 PRIVATE | macOS cruft. |
| `node_modules/`, `dist/`, `build/`, `.venv/` | 🔒 PRIVATE | Build artifacts. |

---

## Maintenance checklist (when adding new content)

1. Add the new path here with a classification.
2. If PRIVATE, verify it matches a rule in `.gitignore` (or add one).
3. If DERIVED, create the summary in `docs/public/` in the same commit.
4. If you reclassify PRIVATE → PUBLIC, treat it as a publishing decision: review for secrets, IP, and moat implications before committing.
