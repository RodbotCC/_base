# Secretary Spec — Simple Ratio Lattice (stub tonight, full tomorrow)

**Status:** drafted — stub tonight, ratios declared tomorrow
**Build order position:** 3 of 3 (TCL → Streak Tracker → Ratio Lattice stub)
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

Jake doesn't want to build the full lattice tonight, but wants a minimal shape locked in so Secretary's scoring has somewhere to look.

## Minimal v1 shape

```
_ledger/ratio_lattice.json
[
  { id, a: "anchor_id_1", b: "anchor_id_2", ratio: "3:1", context: "when in conflict", weight: 0.8 }
]
```

The ratio declares: **"when anchor A and anchor B both apply to a candidate move, anchor A dominates at this ratio."** That's enough for the grid generator to resolve tradeoffs without needing the full Pincer Engine yet.

## What ships tonight (stub-only)

- The file `_ledger/ratio_lattice.json` as an empty array with scaffold notes.
- The schema locked: `{ id, a, b, ratio, context, weight }` per entry.
- Loader plumbing so `ai_instructions.js` can already see the lattice block — empty today, populated tomorrow.

Full Pincer Engine is a tomorrow job. Tonight's move is: stub the file, lock the schema, wire the loader.

## Why stub now instead of waiting

The grid generator is already being designed around "read bedrock, read TCL, read north_star, read ratio_lattice, propose moves." If the lattice isn't wired in from the start, adding it later means touching the generator twice. Stub it now, populate tomorrow, generator code doesn't move.

## Dependencies

- `north_star.json` anchors must exist before ratios can reference them. Anchor ids are the foreign key.
- TCL is not a hard dependency for the stub, but the full version (tomorrow) will read TCL outcomes to tune or learn weights.

## Open questions to resolve at build time

- `ratio` format: string "3:1" (human-readable), numeric 3.0 (math-friendly), or both? A string is easy to declare; a number is easy to compute with. Probably: store string, parse to float at load time.
- `context` field granularity: free-text phrase, or tagged enum ("conflict", "scarcity", "interruption", etc.)?
- Symmetry: is `{a: X, b: Y, ratio: 3:1}` different from `{a: Y, b: X, ratio: 1:3}`? If yes, both directions get stored; if canonical, loader normalizes.
- Weight semantics: global confidence in the ratio itself (0.8 = "we're 80% sure this dominance holds") or regime-contingent (different weights under different sore-thumbs)?
- How many pairwise ratios before the full Pincer Engine takes over — is there a count threshold, or does Jake just flip the switch?
