# Close — Session End Protocol

*Triggered at /close only.*

---

## Step 1 — Write session entry in `context/LOG.md`

```
## [YYYY-MM-DD] — Session [N]
**Came with:** [the presenting question or topic]
**Mode:** [Execution / Planning / Processing]
**Observed:** [what was actually going on — subtext, avoidance, clarity, energy. Be specific.]
**Decided:** [concrete commitments, results, or outcomes from this session]
**Key insight:** [the most important thing the user should remember from this session — one sentence]
```

### Retention rule
Keep the 8 most recent entries. When a new entry is added and the count exceeds 8, delete the oldest. Git history preserves everything — LOG.md is a working window, not an archive.

PINNED section (top of LOG.md) is exempt from the count. Pin sparingly: only load-bearing insights or unresolved commitments. Unpin when resolved.

## Step 2 — Update `helm.yml`

Update every field that changed: meta (session, last, mode_last), hunts, farms (last dates), pinned, next_milestone, balance.

**Decision cleanup:** If a decision was made this session (job accepted, path chosen, option eliminated), delete the dead options from helm.yml, `context/METRICS.md`, and `context/PLAN.md`. Only the result stays.

## Step 3 — Self-improvement check

One question: *"Is anything in this system not serving the user?"*

If yes → propose one specific change in conversation. User decides immediately.
If no → silent.

## Step 4 — Git commit and push

```
git add -A && git commit -m "[SN] [session type] — [one line: key change or decision]"
git push
```
