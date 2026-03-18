# Changelog

All notable changes to Quorum are documented here.

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
