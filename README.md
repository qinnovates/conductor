# Quorum

**Orchestrate a swarm of AI experts on any question. From 3 agents to 1,000. One command, multiple minds, stress-tested answers.**

Type one command. Quorum spins up a team of specialists — researchers, analysts, skeptics, domain experts — makes them work the problem from every angle, debate each other, validate their claims, and deliver a synthesized verdict you can actually act on.

Like having a room full of smart people argue about your question before anyone gives you the answer. Or, in swarm mode, an entire conference hall.

```
/quorum "your question here"
```

Built by [qinnovate](https://qinnovate.com) | [Full docs](docs/ARCHITECTURE.md)

---

## Why Quorum?

When you ask AI a question, you get one perspective. It sounds confident. It might be completely wrong. And you have no way to know.

Quorum gives you what a single AI agent never can: **a second opinion, a third opinion, a devil's advocate, and a fact-checker — all at once.**

Here's what happens when you run it:

1. **A team assembles.** Quorum picks the right experts for your question — a strategist, a skeptic, a researcher, a domain specialist, someone from a completely different field
2. **They work independently.** No groupthink. Each expert tackles the question from their unique angle without seeing anyone else's answer
3. **They challenge each other.** The skeptic pokes holes. The researcher checks sources. Debate pairs argue the real disagreements
4. **A supervisor synthesizes.** Not a vote count — an authored judgment that weighs reasoning quality, surfaces buried insights, and tells you what actually matters
5. **You get the verdict.** What survived scrutiny, what's still disputed, and what to do next

**The result: answers that have been stress-tested by multiple minds before you see them.**

## Quick Start

```bash
# Install (works with Claude Code and Cowork)
claude install qinnovates/quorum

# Ask any question
/quorum "Should we use PostgreSQL or DynamoDB for our new service?"

# Review a document
/quorum "Review this proposal" --artifact proposal.md

# Deep Socratic exploration
/quorum "Should we open-source our core product?" --rigor dialectic

# Fact-check a prior research swarm
/quorum "Validate this research" --artifact _swarm/report.md --rigor high

# Swarm mode — hundreds of agents, emergent intelligence
/quorum "Impact of EU AI Act on BCI startups" --swarm

# Prediction mode — Delphi-method forecasting
/quorum "Will neural data be classified as biometric by 2028?" --swarm --predict

# See the plan before running
/quorum "your question" --dry-run
```

## Features

### Built-in BS Detection (5 layers)

| Layer | What It Does |
|---|---|
| Source Grading | Every finding rated STRONG / MODERATE / WEAK / UNVERIFIED |
| Contradiction Check | Catches when agents disagree AND when they agree without evidence |
| Hallucination Red Flags | Supervisor checklist for fabricated stats, fake citations, too-clean numbers |
| Independent Validation | Separate reviewer challenges the synthesis |
| Transparent Output | Report shows what's verified, what's unresolved, what couldn't be checked |

**The rule: If it can't be sourced, it gets flagged. If it can't be verified, it says so. If agents disagree, both sides are shown. You decide — not the AI.**

### Challenge Levels (`--rigor`)

| Level | When to Use |
|---|---|
| `low` | Brainstorming — light pushback, creative flow |
| `medium` (default) | Decisions — real debate with evidence |
| `high` | High stakes — stress test, agents actively try to break the conclusion |
| `dialectic` | Deep questions — two agents drill through contradiction Socrates-style until they hit bedrock truth |

### Dialectic Mode (Socratic Deep-Dive)

Instead of 5 agents giving parallel opinions, two agents enter a philosophical dialogue:

- **Thesis** states a position with evidence
- **Antithesis** finds the contradiction, the unstated assumption, the edge case where it breaks
- Each round goes **deeper, not wider** — no new topics, no retreating to generalities
- The supervisor calls it when one of three things happens:
  - **Synthesis** — both sides arrive at a combined position better than either started with
  - **Bedrock** — the disagreement is irreducible, comes down to values. Now you know what you're actually deciding
  - **Spark** — the dialogue surfaces a question nobody started with. The best possible outcome

```
/quorum "Should we open-source our core product?" --rigor dialectic
```

### Privacy Controls

| Flag | What It Does |
|---|---|
| `--no-web` | No web searches — everything stays local |
| `--no-save` | Nothing saved to disk |
| `--redact` | Strip URLs, names, PII from saved sessions |
| `--no-cross-ai` | Skip independent validation |

**Maximum privacy:** `/quorum "query" --no-web --no-cross-ai --no-save`

### All Options

| Flag | Default | Description |
|---|---|---|
| `--size N` | auto | Number of expert agents (3-1000+) |
| `--rounds N` | 1 | Debate rounds (1-3 standard, 3-20 swarm) |
| `--full` | — | Full mode: 8 agents, 2 rounds, validation |
| `--lite` | — | Minimal: 3 agents, 1 round |
| `--rigor LEVEL` | medium | low / medium / high / dialectic |
| `--mode MODE` | auto | review / research / hybrid / explore |
| `--artifact PATH` | — | File to review |
| `--format FORMAT` | auto | audit / research / dialectic / decision / org / explore |
| `--dry-run` | — | Show plan without running |
| `--output PATH` | auto | Custom output path |
| `--resume ID` | — | Resume a previous session |
| **Swarm Mode** | | |
| `--swarm` | — | Enable swarm mode (20-1000+ agents) |
| `--predict` | — | Prediction mode with sentiment tracking and coalition detection |
| `--branches "a,b,c"` | auto | Manual top-level taxonomy branches |
| `--schedule STRATEGY` | round-robin | round-robin / reactive / priority / probabilistic |
| `--taxonomy show` | — | Show generated taxonomy without running |
| `--interviews N` | 5 | Agents the supervisor interviews directly |

## How It Works

Quorum runs a multi-phase pipeline. You don't need to understand this to use it — just type `/quorum "question"` and go. But if you want the details:

**[Full architecture documentation →](docs/ARCHITECTURE.md)**

**Standard mode (3-17 agents):**
1. **Setup** — Supervisor analyzes your question, picks the right experts and assigns each a unique angle
2. **Independent work** — All agents work in parallel, no one sees anyone else's output
3. **Triage** — Supervisor reads all reports, drops low-value agents, identifies key disagreements
4. **Cross-review** — Selected agents debate each other directly. Devil's Advocate challenges the majority
5. **Synthesis** — Supervisor authors the final report with editorial judgment
6. **Validation** — Independent reviewer challenges the synthesis
7. **Final report** — What survived, what's disputed, what to do next

**Swarm mode (20-1000+ agents):**
1. **Taxonomy** — Partition Engine decomposes the problem into non-overlapping territories
2. **Spawn** — One agent per territory, persona derived from its domain
3. **Simulation** — Agents POST findings, REACT to others, HANDOFF cross-territory discoveries, SHIFT positions across multiple rounds
4. **Pattern extraction** — Environment Server identifies opinion clusters, polarizations, cascades, coalitions
5. **Synthesis** — Supervisor reads patterns (not individual reports), interviews key agents
6. **Structural challenge** — Socrates questions clusters, Plato audits evidence
7. **Validation** — Independent reviewer challenges the synthesis
8. **Final report** — Emergent consensus, polarizations, sentiment trajectory, what to do next

## Scaling: Flat → Hierarchy → Swarm

Most multi-agent tools are flat: split a task, hand each piece to an agent, merge. That works for 5 agents on a focused question. It falls apart at 12+ agents on a cross-domain question — a security researcher and a clinician aren't arguing about the same thing, they're arguing about different things using the same words. A flat supervisor managing 15 individual perspectives loses signal fast.

Quorum scales in four tiers:

| Mode | Agents | Structure | When to Use |
|------|--------|-----------|-------------|
| **Flat** (`--lite`, default) | 3-8 | Single panel, everyone debates everyone | Focused questions in 1-2 domains |
| **Subteam** (`--teams`) | 9-17 | Named teams deliberate internally, leads cross-challenge | Questions crossing 3+ domains with different incentives |
| **Org** (`--org`) | 17+ | Full hierarchy: teams + Socrates + Plato | High-stakes decisions, regulatory review, research synthesis |
| **Swarm** (`--swarm`) | 20-1000+ | Taxonomy-partitioned agents, environment-based coordination | Predictions, landscape surveys, exhaustive red teaming, Delphi consensus |

**Why hierarchy beats flat at scale:**

- **15 flat agents** produce 15 reports. The supervisor reads all 15, loses nuance, defaults to vote-counting. Echo chambers form because everyone sees similar context.
- **3 teams of 5** produce 3 team positions. Each team has internal debate first (local consensus), then team leads present to the supervisor. Cross-team challenges happen at the leadership level where the real tensions are. The supervisor arbitrates between 3 institutional positions — not 15 individual hot takes.

**Why swarm beats org at massive scale:**

- **17 org agents** can be supervised individually. The supervisor reads every report. This breaks at 50+.
- **200 swarm agents** write to a shared environment. The supervisor doesn't read 200 reports — it reads the **patterns** that emerge: which opinions clustered independently across unrelated territories, where polarization formed, which findings cascaded through the swarm. The input is O(patterns), not O(agents).

**Two structural roles appear in subteam/org/swarm mode:**

- **Socrates** asks each team lead (or opinion cluster in swarm mode) ONE question — the one they'd least want to answer. Cannot state an opinion. Forces teams to defend their weakest point. Prevents echo chambers.
- **Plato** audits every claim across all teams (or top clusters): is it sourced or asserted? Produces an evidence audit table. Any unsupported claim is flagged in the final report. Prevents hallucination.

Together, Socrates prevents echo chambers (forces teams to defend their weakest points) and Plato prevents hallucination (forces teams to source their strongest claims). You can't agree quickly if you haven't survived questioning AND evidence audit.

```bash
# Focused question — flat is perfect
/quorum "Should we use Rust or Go for our CLI?"

# Cross-domain — subteams needed
/quorum "Review our BCI security posture" --teams "engineering,legal,clinical"

# High-stakes research synthesis — full org
/quorum "Validate the receptor expansion research" --org --rigor high

# Landscape survey — swarm covers exhaustively
/quorum "EEG authentication methods: full landscape" --swarm --size 100

# Prediction — emergent collective intelligence
/quorum "Will the EU classify neural data as biometric by 2028?" --swarm --predict
```

**[Full guide: when to use flat vs subteams vs dialectic vs swarm →](docs/GUIDE.md)**

## What Makes Quorum Different

Every multi-agent tool in the Claude Code ecosystem does the same thing: splits a task, hands each piece to an agent, collects answers, merges them. More hands, same brain. If all 8 agents hallucinate the same thing, you get a confident, well-formatted wrong answer.

Quorum is the only plugin that asks: *"How do we know this answer is actually right?"*

### Anti-Boxing

When you give an AI a project profile and a classification gate, it starts only pulling from familiar domains, only spawning agents it already knows, only asking questions it can answer. The profile IS the box. The classification gate IS the box. Every efficiency optimization that prunes "low-signal" agents is killing exactly the perspectives that would break the box.

What I call **anti-boxing** is Quorum's structural guarantee that the system keeps reaching outside its own comfort zone. It is not an established term in AI/ML literature. The concepts it draws from have other names — lateral thinking (de Bono), structured dissent (Janis groupthink prevention), adversarial robustness, cognitive diversity in teams — but anti-boxing as a named architectural pattern for multi-agent systems is original to Quorum.

Quorum walks a razor's edge. On one side: hallucination — agents confidently generating plausible nonsense. On the other: an echo chamber (no pun intended) — agents constrained so tightly that they never think outside the project's existing mental model. Both failure modes produce the same result: the user gets back what they already believe, packaged in confidence they didn't earn.

This is the direct practice of Socrates. He did not teach by giving answers. He taught by questioning assumptions — including his own. Quorum embodies this: every swarm includes agents whose job is to challenge, and the system deliberately reaches outside its own comfort zone to find perspectives the user didn't ask for.

**The 6 anti-boxing rules:**

1. **Domain Outsider never from the profile's default domains.** If the profile says "accessibility, engineering, design," the outsider comes from somewhere else. The outsider's value comes from NOT being in the profile.
2. **Classification gate scores the question, not the project.** A business question in a research repo gets business agents, not more researchers.
3. **Condition-based outsider injection.** When the last 3+ runs showed high consensus with low challenge, inject a lateral thinker. The trigger is unexamined confidence, not a counter.
4. **Exploratory queries invert the profile.** When the user asks "What am I missing?" the profile represents exactly the box they need to escape. The swarm spawns from domains the profile doesn't list.
5. **Adversarial agents are immune to pruning.** The Devil's Advocate and Provocateur can never be killed by efficiency rules.
6. **Inverted early termination.** When everyone agrees, scrutiny goes UP, not down. Unanimous consensus is the highest-risk scenario for blind spots.

Constraint kills creativity. Transparency kills hallucination. Quorum chooses transparency.

**What exists today and why it's not enough:**

- **Claude Swarm, Auto-Claude, Claude Squad** — task dispatchers. Agents never challenge each other. No source verification. No debate.
- **CrewAI, AutoGen, LangGraph** — require Python setup, YAML configs, infrastructure. Hours of work before your first question. And agents still don't argue.
- **Cursor, Copilot, Windsurf** — single agent, single perspective, coding only. No second opinion.

**What Quorum adds that none of them have:**

- Agents assigned **opposing positions**, forced to defend them with evidence
- A **Devil's Advocate** who argues against the majority — because the answer that survives pushback is the one worth trusting
- Challenge agents get **less context on purpose** so they can't just agree with everyone
- Research agents search **different sources with different terms** — not the same Google result five times
- The supervisor **judges reasoning quality**, not vote counts — a well-argued minority beats a hand-waving majority
- **Dialectic mode** — two agents drill through contradiction across multiple rounds until they hit bedrock. Doesn't exist anywhere else
- **Swarm mode** — scales to 1000+ agents with taxonomy-partitioned territories, environment-based coordination, and emergent pattern detection. No other AI plugin does collective intelligence at this scale with built-in epistemic guarantees

The difference: other tools give you more answers. Quorum gives you *better* answers — and now, at any scale.

## Examples

It's not a developer tool. It's a thinking tool. Any question where you'd want a smart friend to push back before you commit.

**Before a job interview:**
```
/quorum "I'm interviewing at Stripe for senior security engineer. What will they ask that I'm not preparing for?"
```

**Settling an argument:**
```
/quorum "Is a hot dog a sandwich?" --rigor dialectic
```

**Naming your startup:**
```
/quorum "We're building AI tutoring for kids with ADHD. Evaluate these names: FocusOwl, Sparktrain, Brainbuddy" --rigor high
```

**Buying a house:**
```
/quorum "We found a house for $450K, 1960s build, no inspection yet. What should first-time buyers worry about?"
```

**Career crossroads:**
```
/quorum "I'm 35, making $180K in fintech, got offered $140K at a climate startup. Is the pay cut worth it?" --rigor dialectic
```

**Evaluating a business idea:**
```
/quorum "An app that matches dog owners for group walks. Is this a business or a feature?" --full
```

**Planning a difficult conversation:**
```
/quorum "I need to tell my cofounder we should pivot. They've spent 8 months on the current product. How do I frame this?"
```

**Dog health:**
```
/quorum "My 11-year-old golden retriever started limping after a walk. No swelling. What should I know before calling the vet?"
```

**Research deep-dive:**
```
/quorum "What are the most promising approaches to Alzheimer's early detection?" --mode research --full
```

**Validate research (two-stage pattern):**
```bash
# Stage 1 — Research (expensive, runs once)
/quorum "EEG-based authentication methods" --mode research --full --output _swarm/eeg-auth.md

# Stage 2 — Validate (cheap, re-run as needed)
/quorum "Fact-check for hallucinations and unsupported claims" \
  --artifact _swarm/eeg-auth.md --mode review --rigor high --no-web
```

**Document review:**
```
/quorum "Review this contract for risks I might miss" --artifact contract.pdf --rigor high
```

**Quick opinion:**
```
/quorum "Best Python web framework for a small API?" --lite
```

**Swarm: predict a market shift:**
```
/quorum "Will BCI startups consolidate or fragment by 2028?" --swarm --predict --size 200
```

**Swarm: exhaustive red team:**
```
/quorum "Red team our authentication system — every vector" --swarm --branches "network,application,social,physical,supply-chain"
```

**Swarm: landscape survey:**
```
/quorum "Complete landscape: adversarial attacks on EEG systems" --swarm --schedule reactive --rounds 10
```

## Output Format

Every standard report includes:
- **Executive Summary** — 3-5 sentences, degree of consensus, key finding
- **Supervisor's Assessment** — The quorum's own judgment (most valuable section)
- **Confidence & Verification** — What's backed by evidence vs. supervisor judgment
- **Disagreement Register** — Unresolved disputes with both positions preserved
- **Priority Actions** — Ranked by impact, not by how many agents mentioned them
- **Blind Spots** — What the team collectively could not evaluate

Swarm reports add:
- **Emergent Consensus** — Findings that agents in unrelated territories reached independently (strongest signal)
- **Polarizations** — Genuine disagreements with evidence on both sides
- **Cascades** — Findings that changed the swarm's trajectory
- **Coalition Map** — Which territory groups aligned on which recommendations
- **Sentiment Trajectory** — How the swarm's collective position evolved across rounds

## What's New in v5.0.0

**Swarm Mode.** Quorum now scales from 3 agents to 1,000+.

Standard Quorum tops out at ~17 agents — the supervisor reads every report, designs every debate pair, writes every synthesis. That's the right approach for focused questions. But for predictions, landscape surveys, exhaustive red teaming, and Delphi-method consensus, you need collective intelligence at population scale.

Swarm mode replaces per-agent orchestration with **environment-based coordination**:

- **Partition Engine** — decomposes the problem into a MECE (mutually exclusive, collectively exhaustive) taxonomy. Each agent gets a unique territory. No overlap, guaranteed.
- **Environment Server** — shared state store where agents POST findings, REACT to others, HANDOFF cross-territory discoveries, and SHIFT positions. The supervisor reads emergent patterns, not individual reports.
- **Activation Scheduler** — not all agents run every round. Four scheduling strategies (round-robin, reactive, priority, probabilistic) keep compute linear as agent count grows.
- **Prediction mode** (`--predict`) — probabilistic activation, sentiment trajectory tracking, coalition detection. Designed for forecasting questions.

The supervisor still writes the final verdict. Socrates still questions. Plato still audits evidence. The 5-layer validation pipeline still runs. Anti-boxing rules still apply. Everything that makes Quorum an epistemic quality gate is preserved — it just scales.

Inspired by [MiroFish/OASIS](https://github.com/666ghj/MiroFish) swarm intelligence architecture. Adapted with Quorum's epistemic guarantees: hard territory boundaries, evidence tiers, structural challenge, independent validation.

```bash
/quorum "Impact of EU AI Act on BCI startups" --swarm
/quorum "Will neural data be biometric by 2028?" --swarm --predict --size 200
/quorum "Red team our auth" --swarm --branches "network,app,social,physical,supply-chain"
```

[Full swarm mode architecture →](docs/ARCHITECTURE.md#swarm-mode---swarm) | [Full changelog →](docs/CHANGELOG.md)

<details>
<summary><strong>Previous releases</strong></summary>

### v4.1.0 — Divergence Engine
Provocateur archetype, EXPLORE mode, structural protections (adversarial immunity, Socratic follow-ups), security hardening, SKILL.md split.

### v4.0.0 — Adaptive Intelligence
Project Profiles, Task Classification Gate, Config Transparency Block, Adaptive Output Templates.

### v3.2.0 — Security Hardening
Removed shell access from agent manifest, injection defense on all templates, credential detection patterns.

### v3.1.0 — Epistemic Quality Gate
Two-stage research + validation workflow. VALIDATED / FLAGGED / BLOCKED verdicts.

### v3.0.0 — Subteams & Dialectic
Subteam/Org modes, Socrates + Plato structural roles, Dialectic mode, 5-layer validation pipeline.

[Full changelog →](docs/CHANGELOG.md)
</details>

## On Hallucination

No LLM is hallucination-proof. Not GPT-4. Not Claude. Not any model running inside Quorum. Hallucination is not a bug — it is a structural property of how these systems work.

Every transformer output is a probability sample from a learned distribution, not a fact lookup (Vaswani et al. 2017). The model's weights are a lossy compression of training data — and lossy decompression produces artifacts (Deletang et al. 2024). In images, those artifacts are JPEG blocks. In language models, they are hallucinations. The math does not permit zero error.

This is not unique to machines. Artificial neural networks were modeled after biological neurons (McCulloch & Pitts 1943). Biological brains also confabulate — reconstructing memories from statistical patterns rather than retrieving stored records (Bartlett 1932, Schacter 1999, Loftus & Palmer 1974). Both systems fill gaps with plausible guesses. The difference is that we built the LLM, so we can study the mechanism.

Quorum's 5-layer validation pipeline, adversarial agents, and evidence audits reduce hallucination. They make it *visible*. They do not eliminate it. Every Quorum report is a starting point for human judgment, not a replacement for it.

Models will get more accurate. The rates will shrink. They will not reach zero, because probability in an indeterministic world means errors are structural, not temporary. That is what keeps us learning.

**[Full scientific explanation with citations →](docs/SAFETY.md#0-on-hallucination-why-no-llm-is-hallucination-proof)**

## Documentation

- **[Usage Guide](docs/GUIDE.md)** — When to use flat swarms vs subteams vs dialectic vs validation. Decision matrix, real-world examples, cost guide
- **[Architecture](docs/ARCHITECTURE.md)** — Full phase-by-phase technical specification
- **[Prompt Templates](docs/PROMPTS.md)** — All agent templates with variable reference
- **[Safety & Privacy](docs/SAFETY.md)** — Guardrails, privacy disclosure, tool permissions
- **[Privacy Policy](https://qinnovate.com/privacy)** — Full privacy policy for all qinnovate tools
- **[Changelog](docs/CHANGELOG.md)** — Version history and what changed
- **[Releases](https://github.com/qinnovates/quorum/releases)** — GitHub releases with download links

## License

MIT

## Author

Kevin Qi — [qinnovate.com](https://qinnovate.com)
