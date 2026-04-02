# HELM — A Mentor System for Seeing Clearly

HELM is a structured mentoring system built to run inside Claude Code. It gives you a wisdom mentor — someone who watches, names what you can't see, and helps you uncover the patterns running underneath your decisions, your relationships, and your self-doubt.

This is not therapy. It is not coaching. It is a system for emotional clarity and restored capacity to act.

---

## What This System Does

- **Tracks your life across fronts** — goals, income, relationships, internal state — in one place
- **Runs structured emotional processing** — when something is stuck internally, the mentor shifts mode and helps you name it precisely
- **Discovers wounds and patterns** — over sessions, a map of your psychology builds up in `context/PERSON.md`
- **Holds you accountable** — not by pushing, but by naming what you're avoiding and why

---

## Setup

### Requirements
- [Claude Code](https://claude.ai/code) (CLI, desktop app, or IDE extension)
- A directory for your HELM instance (this folder)

### Steps

1. **Open this folder in Claude Code** as your working directory.
2. **First session:** Type `/hud` to start. The mentor will read `helm.yml`, render your HUD, and ask what you want to work on.
3. **Customize `context/GOALS.md`** — define your priority hierarchy. What matters most? What's blocking you? The mentor uses this to make judgment calls.
4. **Customize `helm.yml`** — fill in your current hunts (things you're pursuing), farms (things you maintain), and financial snapshot.
5. **Let `context/PERSON.md` build naturally** — don't try to fill it in advance. The mentor updates it as patterns emerge across sessions.

### Session Flow

```
/hud          →  See where you are
[talk]        →  Work on what matters — the mentor shifts mode as needed
/close        →  End session — logs entry, updates helm.yml, commits to git
```

### Between Sessions

Your state is preserved in `helm.yml` (fast-read cache) and `context/` files (full detail). Each `/close` commits to git, so your history is preserved.

---

## Commands

| Command | When | What It Does |
|---|---|---|
| `/hud` | Session start | Renders the dashboard from helm.yml |
| `/close` | Session end | Logs session, updates files, commits |
| `/blind` | Something feels off | Mentor reports what you're not seeing |
| `/stuck` | Can't break a pattern | Names the pattern + gives the antidote |
| `/decide [A / B]` | Paralyzed or looping | Surfaces options, picks one, 48hr freeze |
| `/honest` | Want the unfiltered read | Front-by-front assessment + cross-front pattern |
| `/why` | Doubt or low energy | Reminds you via facts you've already paid for |

---

## How Wounds Get Discovered

You don't need to know your wounds in advance. The system discovers them through conversation:

1. **You talk about what's bothering you.** Relationship frustration, career doubt, loneliness, anger — whatever is actually there.
2. **The mentor names emotions precisely.** Not "that sounds hard" — the specific feeling underneath the words.
3. **Patterns surface across sessions.** The same mechanism showing up in different areas gets named and tracked.
4. **Wounds get confirmed, not assumed.** A wound enters `context/PERSON.md` only after it's been observed multiple times. New wounds are staged in `context/STAGING.md` for your approval before being added.

Over time, a map builds. The map isn't the goal — clarity is. But the map makes the next conversation deeper because the mentor remembers what was found.

---

## File Structure

```
HELM/
├── CLAUDE.md              ← Mentor operating instructions (the brain)
├── helm.yml               ← Session cache (fast-read snapshot)
├── protocols/
│   ├── COMMANDS.md        ← How each command works
│   ├── CLOSE.md           ← Session close procedure
│   └── EMOTIONAL.md       ← Emotional processing protocol
└── context/
    ├── PERSON.md           ← Your psychology — wounds, patterns, values
    ├── LOG.md              ← Session history (rolling 8 entries)
    ├── GOALS.md            ← Priority hierarchy and objectives
    ├── PLAN.md             ← Current strategy
    └── METRICS.md          ← Progress tracking
```

---

## Important Notes

- **This is not a substitute for professional support.** If you're experiencing clinical-level distress, the mentor will name that directly and suggest professional help.
- **The mentor doesn't push.** It observes, names, and explains. You decide what to do with what you see.
- **Wounds are private.** Your `context/PERSON.md` file contains sensitive self-knowledge. Keep it in a private repo or local-only.
- **Git history is your archive.** The rolling log keeps 8 sessions; everything else is preserved in git commits.
