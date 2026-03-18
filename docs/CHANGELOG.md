# Changelog

All notable changes to Quorum are documented here.

## [v4.1.0](https://github.com/qinnovates/quorum/releases/tag/v4.1.0) — 2026-03-17

### Security
- Fixed injection defense gap in ARCHITECTURE.md templates (Cross-Review, Devil's Advocate, Phase 5 reviewer)
- Added profile sanitization for project profile poisoning prevention
- Added injection defense to Provocateur archetype
- Scoped adversarial agent file access to project directory

### Architecture
- **SKILL.md split:** 1490 lines → 250 lines. All architecture, templates, and deep-dive content moved to docs/. SKILL.md is now user-facing only with progressive loading references.
- **Divergence Engine:** Provocateur archetype, EXPLORE mode, preserve-if-unique triage, creative disruption check, research partition overlap
- **Structural Protections (enforced):** Adversarial immunity, Socratic follow-ups (2-3 per team), refutation resistance (replaces confidence scores), Socratic Remainder, inverted early termination
- **Anti-boxing:** Condition-based outsider injection (replaces counter-based), exploration signal in Socratic Gate, Contestability replaces Falsifiability
- Added EXPLORE mode to GUIDE.md with Provocateur documentation

### Changed
- Version bump 4.0.0 → 4.1.0
- Socratic Gate: 5 dimensions → 6 (added Exploration signal)
- Socratic Gate: Falsifiability → Contestability (supports normative questions)

---

## [v4.0.0](https://github.com/qinnovates/quorum/releases/tag/v4.0.0) — 2026-03-17

### Added — Adaptive Intelligence
- **Project Profiles** (`_swarm/project-profile.json`) — auto-generated on first run, persists project context (type, domains, tech stack, default teams, constraints) across runs. Eliminates re-discovery. Boosts Socratic Gate scoring. Sharpens ponder questions.
- **Task Classification Gate** — 4-dimension scoring matrix (Domain count, Certainty demand, Scope breadth, Artifact presence). Score 0-12 maps to mode, agent count, structure, and rigor. Override rules for binary decisions (auto-dialectic), feasibility probes (dialectic-first), and cross-domain questions (auto-org).
- **Config Transparency Block** — replaces `--dry-run` with "here's what I read, here's my config, here's why." Always shown unless `--quiet`. User approves, edits, or cancels before tokens are spent.
- **Adaptive Output Templates** — 5 templates matched to task type: AUDIT (verdict + finding table), RESEARCH (evidence table + citations), DIALECTIC (dialogue transcript + what emerged), DECISION (recommendation + tradeoff table), ORG (team positions + clash table + Socrates/Plato sections).
- New flags: `--yes` (auto-proceed), `--quiet` (suppress transparency block), `--profile show|update|reset`, `--format audit|research|dialectic|decision|org`

### Changed
- Quick Start updated: "auto-configures everything" replaces "default is fast mode (5 agents)"
- Version bump 3.2.0 → 4.0.0 (breaking: output format changes, default behavior changes)

### Design Process
Feature designed by a 6-agent Quorum swarm (3 teams: Architecture, UX, Efficiency). Swarm report: `_swarm/2026-03-17-quorum-adaptive-intelligence.md`

---

## [v3.2.0](https://github.com/qinnovates/quorum/releases/tag/v3.2.0) — 2026-03-17

### Security Hardening
- **[CRITICAL FIX] Removed `Bash`, `Write`, `Edit` from manifest `allowed-tools`.** These were available to all spawned agents despite documentation stating they were supervisor-only. Now only the supervisor session has access.
- **[CRITICAL FIX] Added XML tag injection defense.** Artifact content and inter-agent transfers now use unique session boundaries (`{{SESSION_BOUNDARY}}`) instead of fixed XML tags, preventing tag-injection prompt escapes.
- **Added agent-level prompt injection detection.** All agent templates (Research, Analysis) now include active defense instructions to detect and flag injection attempts in fetched content.
- **Added credential detection patterns.** Defined 8+ specific regex patterns for automatic redaction (AWS keys, Stripe, Slack, GitHub PATs, JWTs, private keys) instead of relying on undefined model heuristics.
- **Added path validation guidance.** `--output` and `--resume` must validate against allowed path prefixes.
- **Fixed privacy disclosure.** Cross-AI validation gate now clearly states that artifact excerpts may be included in synthesis passed to the validation agent.
- **Added independence disclaimer.** Phase 5 "independent" reviewer is now explicitly documented as same-session Claude instance, not a separate model.

### Architecture
- **Added `argument-hint` frontmatter.** Autocomplete now shows available flags when typing `/quorum`.
- **Added `disable-model-invocation: true`.** Prevents Claude from auto-triggering Quorum without explicit user invocation.
- **Added Usage Guide** (`docs/GUIDE.md`) — decision matrix for flat swarms vs subteams vs dialectic vs validation, cost guide, real-world examples.

---

## [v3.1.0](https://github.com/qinnovates/quorum/releases/tag/v3.1.0) — 2026-03-17

### Added
- **Research + Validation Workflow** — new section in SKILL.md with three copy-paste patterns:
  - Two-stage (research swarm, then validation swarm)
  - Validate any external research (not just Quorum output)
  - Resume and re-validate a prior session
- **Three-tier verdict output** for validation runs: VALIDATED / FLAGGED / BLOCKED
- **Panel Provenance** section in validation output (who validated, their stances, what models)
- **Coverage Notice** in validation output (what the panel could and could not evaluate)
- **Scope disclaimer** hard-coded into validation output template
- 5th Quick Start example showing validation pattern

### Changed
- Version bump 3.0.0 → 3.1.0

### Design Process
Feature designed by an 11-agent Quorum swarm (3 teams: Product Design, Engineering, Documentation + Socrates + Plato structural roles). Swarm report: `_swarm/2026-03-17-quorum-validate-feature.md`

---

## [v3.0.0](https://github.com/qinnovates/quorum/commit/8c4ce4f) — 2026-03-14

### Added
- **Subteam Mode** (`--teams`, `--org`) — hierarchical org-chart deliberation with team leads, internal debate, cross-team challenges
- **Socrates** (cross-team questioner) and **Plato** (evidence auditor) structural roles
- **Dialectic Mode** (`--rigor dialectic`) — Socratic deep-dive, two agents drilling through contradiction
- **5-layer validation pipeline** — source grading, contradiction check, hallucination red flags, independent validation, transparency
- **Research-backed defaults** — team sizes, org structure grounded in Hackman, Miller, Brooks, Janis
- **Session persistence** — resume prior swarms with `--resume`
- **Privacy controls** — `--no-web`, `--no-save`, `--redact`, `--no-cross-ai`
- **Output formats** — `--format full/brief/actions-only`
- Published to GitHub, submitted to Anthropic marketplace

### Changed
- Renamed from "Expert Swarm" to "Quorum"

---

## v2.1.0 — 2026-03-13

### Added
- Multi-agent intelligence with built-in BS detection
- Devil's Advocate, Naive User, Domain Outsider mandatory roles
- Cross-AI validation gate
- Competitive positioning vs Claude Swarm, Auto-Claude, CrewAI

### Changed
- Reframed as "swarm conductor" with outcome-focused documentation

---

## v1.0.0 — 2026-03-12

### Added
- Initial release as "Expert Swarm"
- Basic multi-agent panel with parallel independent work and supervisor synthesis
