# Secretary Spec — Streak Tracker

**Status:** drafted — not yet built
**Build order position:** 2 of 3 (TCL → Streak Tracker → Ratio Lattice stub)
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

A first-class subsystem inside Secretary that tracks which of our declared goals we've actually stuck to, day over day. **Not a gamification layer — a fidelity meter.** Every anchor in `north_star.json` can have a streak attached. Streaks are computed from gesture residue plus the Temporal Continuity Ledger, not self-reported. If the anchor was honored today, the streak extends. If it wasn't, it breaks — visibly, with the reason.

## Minimal v1 scope

- `_ledger/streaks.json` — one entry per anchor with `current_streak`, `longest_streak`, `last_honored`, `last_broken`, `break_reason`.
- A **Streaks strip** somewhere visible — probably on the topbar or as a card on the morning grid — showing live streaks for the anchors Jake has flagged as streak-worthy.
- A nightly job (or end-of-day commit) that walks the day's residue and decides which anchors were honored, which were broken, and updates the ledger.
- An **"honor this anchor" gesture** on any commit, so the chain between action and anchor is explicit when Jake wants it to be.

## Why it matters

This is the mechanism that makes the North Star Ledger operational instead of aspirational. Declared anchors without a fidelity tracker are just a list. Declared anchors with a streak are a system.

## Dependencies

- **TCL must exist first** — the nightly job walks TCL entries to decide honored/broken. Without the day ledger, streaks have nothing to compute from.
- `north_star.json` anchors must exist — streaks attach to anchors by id. Anchors need a `streak_worthy` boolean (or similar flag) so the tracker knows which ones to display.

## Open questions to resolve at build time

- Streak-worthy flag: where does it live — on the anchor itself in `north_star.json`, or in a separate config? Former keeps it close; latter keeps the anchor schema clean.
- Break semantics: partial honor counts as a break? (Probably yes — fidelity means fidelity.) Explicit `break_reason` strings: free-text, or constrained enum?
- "Honor this anchor" gesture UI: button on commit, multi-select dropdown, or inferred automatically from the commit's anchor cross-refs?
- Nightly job trigger: scheduled task at fixed time, or triggered when Jake signals end-of-day? Former is predictable; latter respects the "until Jake ends the day" boundary.
- Grace windows: does a missed day always break the streak, or is there a configurable "rest day" per anchor? Risk: grace windows turn fidelity meter back into gamification.
