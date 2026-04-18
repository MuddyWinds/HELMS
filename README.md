# HELM

A personal operating system built on Claude Code. HELM gives you a long-running mentor that holds your full picture across sessions — psychology, career, finances, fitness, relationships — names what you can't see, and converts every insight into a concrete next action.

Most AI conversations start from zero. HELM doesn't. It remembers where you are, what you've decided, what patterns keep running, and what you're avoiding. It gets sharper over time.

---

## How It Works

HELM is a git repo that Claude Code reads as its operating instructions. The repo contains:

- **A mentor persona** with defined voice, stance, and coaching philosophy
- **Context files** that build up a picture of who you are over time
- **Protocol files** that define how the mentor coaches across different domains
- **A session cache** (`helm.yml`) that gives the mentor your full state in a single file read

Every session follows a loop: read state → render a dashboard → surface outstanding items → work on what matters → audit what was missed → commit the updated state. The repo is the mentor's memory. Git history is the audit trail.

---

## Core Principles

1. **Action is the primary mode of understanding.** Every observation ends in a concrete next step within 48 hours. Insight without action decays.
2. **Observe, name, resolve.** Naming a pattern is half the job. The other half is showing the exit.
3. **Explain the why — then stop.** Sharp over thorough. One clean cut, not three careful angles.
4. **The system actively sheds what no longer matters.** Dead options, stale references, resolved items — operational files contain only what is currently actionable.
5. **The system audits itself.** Every session close includes a blindspot scan that catches what was missed. Modes self-evolve toward actual needs.

---

## Session Flow

```
1. Read state          helm.yml — full picture in one file
2. Render HUD          Visual dashboard: map, hunts, farms, mode states
3. Carryover Gate      Surface overdue items before asking what to work on
4. Session Gate        "What do you want to work on?"
5. Session work        Mentor operates through relevant mode(s)
6. Close (/close)      LOG entry → state update → blindspot scan → git commit
```

The **carryover gate** (Step 3) is a structural enforcement mechanism. Before the user sets the agenda, the mentor surfaces outstanding commitments, overdue experiments, and stale farms. The user can choose not to act on them — but they can't avoid knowing they exist.

---

## Commands

| Command | When | What it does |
|---|---|---|
| `/hud` | Session start | Full dashboard from current state |
| `/close` | End of session | LOG, state update, blindspot scan, mode evolution, commit |
| `/blind` | Something feels off | Surfaces what's not being talked about + concrete actions |
| `/stuck` | Pattern running, can't break out | Names the pattern, explains the mechanism, gives resolution path |
| `/decide [A / B]` | Paralysed or circling | Evaluates options, picks one, 48-hour freeze |
| `/honest` | Want unvarnished reality | Front-by-front read + cross-front pattern + "what aren't you saying?" |
| `/why` | Doubt or low energy | Facts already paid — evidence, not motivation |

---

## Modes

Modes are expert personas that activate automatically when conversation enters a specific domain. The base mentor never disappears — modes are lenses on top of it.

Each mode has:
- A **persona** (voice, expertise, boundaries)
- **First principles** (irreducible truths governing the domain)
- **Methodology** (how the expert actually operates)
- **Milestone structure** (trackable progression)
- **Cross-mode awareness** (how it connects to the full picture)

**Auto-detection:** Talk about training and the fitness coach activates. Talk about interview prep and the career mode activates. No commands needed.

**Priority rule:** If two modes could apply, the deeper layer wins. Emotional content always takes precedence — process the emotion first, then return to the domain.

**Self-evolution:** At every `/close`, modes expand where more depth was needed and prune sections unused for 5+ sessions. The system converges toward what the user actually needs, not what the designer imagined.

**New modes:** When a domain need recurs 3+ times without a matching mode, the mentor proposes a new one — built from first principles via the generation protocol in `MODES.md`.

---

## Architecture

```
HELM/
  CLAUDE.md                 Mentor operating instructions (the OS)
  helm.yml                  Session cache — single-file state for fast startup
  README.md                 This file

  context/                  User-specific state (the mirror)
    PERSON.md               Psychology, patterns, identity, wounds, evidence trail
    GOALS.md                North stars, priority hierarchy
    PLAN.md                 Strategy, phases, contingency map
    METRICS.md              Live numbers across all fronts
    LOG.md                  Last 8 sessions + pinned working memory
    STAGING.md              Proposed wounds/patterns awaiting user approval
    ATHLETE.md              Fitness tracking (Coach mode)
    WEALTH.md               Tier 2 ledger (Capitalist mode)
    [MODE].md               Additional mode-specific context as modes are generated

  protocols/                Mentor behaviour rules (the coach)
    MODES.md                Mode abstraction layer + evolution + generation protocol
    COMMANDS.md             Execution guides for all commands
    CLOSE.md                Session close + blindspot scan + mode evolution
    THERAPIST.md            Emotional processing + relationship navigation
    COACH.md                Fitness coach — training, nutrition, body composition
    CAPITALIST.md           Wealth-track operator — product, pricing, customers
```

### Separation rule

- **Protocol files** define how the mentor coaches. They are domain knowledge — they could coach any user with similar goals.
- **Context files** hold the user's current state. They are a mirror — reflecting what is true about this specific person right now.
- **`PERSON.md`** holds psychology and identity. Not mode-specific — read by all modes.
- **Shared context** (GOALS, METRICS, PLAN) serves the base mentor and is read by all modes.

### Naming convention

Protocol files are named after the expert persona (COACH, CAPTAIN). Context files are named after the user's journey (ATHLETE, CADET). This prevents ambiguity when both files exist for the same mode.

---

## Key Mechanisms

### Session Weight

Not every interaction is a full session.

- **Full session** (S1, S2...): New real-world data or decisions entered the system. Gets full `/close` with LOG entry, blindspot scan, mode evolution, and push.
- **Sub-session** (S1.1, S1.2...): Quick questions or processing known material. Committed locally with a minimal message. No LOG entry, no push.

### Pinned Items (Working Memory)

The PINNED section in `LOG.md` is the mentor's working memory. Each pin carries a `pinned_at_session` counter. Items pinned 5+ sessions without status change must be actioned, escalated, or unpinned. This prevents the working memory from becoming a graveyard of good intentions.

### Dead Option Purge

When something is dropped or completed: log the outcome, then remove every reference from all operational files. No "Status: Dropped" entries. Dead means gone from the operational surface. Git history preserves the record.

### Background Operating Layer

The mentor runs a silent awareness layer:
- **Pattern-breaking by design** — when recommending actions, check if they also create contact with a known psychological pattern. Frame as the goal, not the therapy.
- **Timeline awareness** — after 3 sessions where a named pattern has no real-world contact, engineer a situation where the user's goals naturally require engaging with it.
- **Architecture-as-avoidance watch** — if 3+ consecutive sessions are spent refining the system instead of doing the work, name the possibility that system-building is functioning as avoidance.

### Farm Staleness

Farms track last-activity dates. 14+ days stale renders a warning. 30+ days triggers automatic surfacing at the carryover gate. Silent decay is one of the system's most dangerous failure modes.

### Blindspot Scan

At every `/close`, the mentor audits itself across six dimensions:
1. Missing data — what should have been asked?
2. Unasked questions — what was brushed past?
3. Advice quality — generic where it should have been specific?
4. Cross-domain gaps — missed interaction effects?
5. Pattern blind spots — antidote not working?
6. Dream cross-reference — motif arcs shifted or stalled?

---

## Getting Started

```bash
# Clone and open with Claude Code
cd ~/Desktop/HELM
claude
```

To set up HELM for yourself:

1. **Fork this repo.** The architecture is the product — your context is the content.
2. **Rewrite `context/` files** with your own situation. `PERSON.md` (who you are), `GOALS.md` (what you're building toward), `PLAN.md` (current strategy), `METRICS.md` (live numbers).
3. **Customise `CLAUDE.md`** — adjust the mentor voice, priority hierarchy, and coaching rules to fit your needs.
4. **Delete or regenerate modes** that don't apply to your domains. Use the generation protocol in `protocols/MODES.md` to create new ones.
5. **Start a session.** The system builds itself from contact — the first few sessions will be thin, but the mentor's picture of you compounds with every `/close`.

The system is designed to learn. Early sessions establish baseline. By session 10, the mentor knows your patterns better than you do.

---

## Design Philosophy

HELM is built on the premise that capable people fail not from lack of talent but from inability to see clearly under pressure. The system exists to hold the full picture when you cannot, name what is invisible from the inside, and convert every insight into contact with reality.

The system's own failure mode is the same as the user's: insight without action. The carryover gate, pinned item lifecycle, farm staleness thresholds, and blindspot scans exist to prevent the system from becoming another preparation room you never have to leave.
