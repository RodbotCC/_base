# Secretary Spec — Temporal Continuity Ledger (TCL)

**Status:** drafted — not yet built
**Build order position:** 1 of 3 (TCL → Streak Tracker → Ratio Lattice stub)
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

This is the big one. A calendar inside Secretary that's not a scheduling tool — it's a **day-ledger**. Each day gets:

- What we did (gestures committed, channels delegated to, tasks executed).
- Conversations we had (chat turns, reflections, notable exchanges).
- What was left open (pending commitments, unresolved threads, stale leads, broken streaks).

And critically: the TCL is read back into the morning grid generator. Every new 3x3 starts by ingesting yesterday's TCL entry plus the current day's state. The grid proposes moves with full knowledge of what happened, what didn't, and what's still hanging.

## Minimal v1 scope

- `_ledger/tcl/<YYYY-MM-DD>.json` — one file per day.
- Structure per day: `{ date, done[], conversations[], left_open[], streak_events[], notable[] }`.
- A Calendar view in Secretary — one cell per day, clickable, shows the day's ledger entry in read-only form.
- The grid generator pulls `yesterday.tcl.json` and `today.tcl.json (in-progress)` into the prompt context alongside Mission Control bedrock.

## Why it matters

This is what makes Secretary actually remember. Right now each morning grid is generated fresh from static state. TCL gives it a running river of what's already happened, so today's proposals are informed by yesterday's outcomes. It's the missing temporal dimension.

## Dependencies

None upstream — TCL is the foundation the other two features build on. Streak Tracker reads from TCL. Ratio Lattice scoring eventually reads from TCL to learn from observed outcomes. Build TCL first so data starts accumulating immediately.

## Open questions to resolve at build time

- Day-boundary semantics: midnight local, or "until Jake ends the day"? Affects when streak_events close out and when the grid generator stops treating a TCL as in-progress vs. final.
- `notable[]` criteria: auto-tagged from sore-thumb-variable signals, or Jake-flagged in the moment, or both?
- Calendar view density: single month or rolling 30-day strip? Mobile-first or desktop-grid?
- How far back does the grid generator read? Just yesterday, or a rolling N-day window?
