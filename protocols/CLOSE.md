# Close — Session End Protocol

*Triggered at /close only. See `CLAUDE.md` → Session Weight for full vs sub-session distinction.*

---

## Sub-Session Close

If this is a sub-session (quick question, no decisions, no new real-world data), skip the full protocol. Do only:

```
git add [changed files]
git commit -m "[SN.N] Quick — [one line: what changed]"
```

No LOG entry. No helm.yml update. No scan. No push. Done.

If context files were updated, the commit message should name which file and why.

If no files were changed, no commit needed. The session leaves no trace.

---

## Full Session Close

Five steps. Steps 1-3 run every session. Step 4 runs at cycle boundaries (every 5th or 10th session). Step 5 always.

## Step 1 — LOG + helm.yml + lifecycle

**Write session entry in `context/LOG.md`:**

```
## [YYYY-MM-DD] — Session [N]
**Came with:** [the presenting question or topic]
**Mode(s) active:** [Mentor / Emotional / Fitness / Capitalist / etc.]
**Observed:** [what was actually going on — subtext, avoidance, clarity, energy. Be specific.]
**Decided:** [concrete commitments, results, or outcomes from this session]
**Key insight:** [the most important thing the user should remember from this session — one sentence]
```

Retention rule: keep the 8 most recent entries. When count exceeds 8, delete oldest. PINNED section is exempt. Pin sparingly; unpin when resolved.

**Update `helm.yml`:**

Update every field that changed: meta (session, last, mode_last), hunts, farms (last dates), pinned, next_milestone, balance, modes.

**In the same pass, run lifecycle maintenance:**
- Pinned items: any item pinned 5+ sessions without status change → (a) actioned, (b) escalated, or (c) unpinned with reason. Enforce 12-item hard cap.
- Modes: any mode not activated 5+ sessions → mark dormant in helm.yml (collapse to one-liner). At 6+ modes, collapse all dormant.
- Resolved pins → unpin. Killed items → dead option purge.

**Dead option purge:** If anything was dropped, killed, completed, or resolved this session — run the full purge protocol (see `CLAUDE.md` → Decision Cleanup). Search all operational files. Remove every reference. Log outcome in LOG.md. Dead means gone.

## Step 2 — Lightweight scan (every session)

Three questions. That's it. Quick and honest.

1. **What did I miss?** What information or question would have made this session better?
2. **What pattern ran unnamed?** Was a Stop Doing Pattern active that I didn't catch or name?
3. **Cross-domain gap?** Did something happen in one domain that should have been connected to another?

For active modes this session — check: did the user want more depth than the mode provided? If yes → update the protocol file to cover the gap.

**Output:** If a finding is actionable → note in LOG entry under `**System note:**` and fix immediately. If nothing → silent. Do not manufacture findings.

## Step 3 — Self-improvement check

One question: *"Is anything in this system not serving you?"*

If the system has a concrete suggestion from Step 2 → present briefly. If no findings → silent.

## Step 4 — Periodic review (cycle-dependent)

Check `meta.session` in helm.yml. Run the applicable cycle(s):

### Short-cycle (every 5 sessions: S5, S10, S15...)

Run these in addition to Steps 1-3:

1. **Full blindspot scan** — the thorough version:
   - Missing data: what should have been asked across the last 5 sessions?
   - Unasked questions: what topics were brushed past?
   - Advice quality: generic where it should have been specific?
   - Cross-domain gaps: missed interaction effects?
   - Pattern blind spots: antidote not working?
2. **Missing mode detection** — did the user spend significant time on a topic with no matching mode, 3+ times in the last 5 sessions? If yes → propose a new mode.
3. **Mode evolution prune check** — for all active modes: which sections went unused across the last 5 sessions? Track in mode context file. 3 sessions unused → flag. 5 sessions flagged → prune (archive at bottom of protocol file, recoverable).
4. **Carryover audit** — any pinned item surviving 10+ sessions without resolution → escalate or kill.
5. **Farm vitality** — any farm dark 30+ days → "Is this still alive?"

### Long-cycle (every 10 sessions: S10, S20, S30...)

Run these in addition to the short-cycle:

1. **Strategic gap scan** — read GOALS.md + PLAN.md + PERSON.md. *"What domains are implied by these goals but have never been discussed? What would a world-class advisor for this profile ask that this system has never asked?"* Output: 2-3 domain suggestions with rationale.
2. **Proactive mode suggestion** — given the user's stated goals, should a mode exist that doesn't?
3. **Generative lens sweep** — read each active mode's Generative Scan section. Each mode produces at least one unsolicited suggestion: an unnamed front, an untracked risk, an adjacent domain.
4. **Pattern effectiveness audit** — any pattern named 10+ sessions ago, still active: is the current antidote working? If named repeatedly with no behaviour change → revise the antidote, not repeat it.

Log all periodic findings under `**Periodic review:**` in the session's LOG entry.

## Step 5 — Git commit and push

```
git add -A && git commit -m "[SN] [session type] — [one line: key change or decision]"
git push
```

---

## Processing Summary

| What | When | Cost |
|---|---|---|
| LOG entry + helm.yml update + lifecycle | Every session | Low — mechanical |
| 3-question lightweight scan | Every session | Low — three questions |
| Self-improvement check | Every session | Minimal — often silent |
| Full blindspot scan (5 dimensions) | Every 5 sessions | Medium |
| Mode evolution prune + missing mode detection | Every 5 sessions | Medium |
| Strategic gap scan + generative sweep | Every 10 sessions | High — reads multiple files |
| Pattern effectiveness audit | Every 10 sessions | Medium |

---

## File Authority

| File | When to edit |
|---|---|
| `context/METRICS.md` | After sessions with real data changes. Dead option purge: delete resolved items. |
| `context/PERSON.md` | Pattern confirmed (3rd instance), communication style updated, identity capital changed, wound confirmed |
| `context/PLAN.md` | Circumstances change the plan. Dead option purge: prune dead paths. |
| `context/GOALS.md` | Rarely — real-world event changes what is possible |
| `context/WEALTH.md` | After a Capitalist mode event (product shipped, first paying customer, asset acquired/sold). Tier 2 metric updated whenever it changes. |
| `context/ATHLETE.md` | After Coach sessions with new data (assessments, program changes, weekly logs) |
| `helm.yml` | At every full /close |
| `context/LOG.md` | At every full /close |
