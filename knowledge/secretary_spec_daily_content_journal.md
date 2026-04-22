# Secretary Spec — Daily Content Journal (the Reservoir)

**Status:** drafted — not yet built
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

Write one entry a day documenting something new I've discovered, something novel within the framework (or that I think might be novel), or something I'm actively working on. Capture with screenshots, videos, and whatever media makes the entry tangible.

**The goal isn't immediate publication — it's building a reservoir of raw material that can later be funneled into Twitter threads, YouTube videos, LinkedIn posts, whatever surface is right for the content.**

## Why it matters

Right now everything Jake discovers gets mentioned in a chat, lives in a voice note, or disappears into a Codex session. The reservoir pattern means every discovery gets captured at the moment it happens, even if it takes weeks or months before it gets shaped into a public artifact.

**Separating capture from publication is what makes the content flywheel work** — you can't publish what you didn't capture, and capture pressure shouldn't demand publication-readiness.

This anchor also closes a loop with `public_surface_build` (item 5 / batch 2). The journal is what feeds Twitter, YouTube, LinkedIn when those channels go live. Without the journal, the social surface is always scrambling for something to post. With the journal, the social surface has a year of material to draw from by the time it matters.

## Minimal v1 scope

### Directory layout
```
_ledger/journal/
  YYYY-MM-DD.md       — the text entry
  YYYY-MM-DD/         — attachments folder for that day (screenshots, video clips, diagrams)
```

### Entry schema
- **Title**
- **Body** (markdown)
- **Attachments** (optional, stored in day-folder alongside)
- **Tags** — three dimensions:
  - **Framework area** — `delta-physics`, `ratio-lattice`, `secretary-architecture`, `buyer-vector-method`, `sub-agent-fleet`, etc.
  - **Platform intent** — `twitter-thread-candidate`, `youtube-explainer-candidate`, `linkedin-post-candidate`, `internal-only`
  - **Media type** — `text-only`, `has-screenshots`, `has-video`, `has-diagrams`

### Views
- **Chronological view** — entries in date order.
- **Pull-by-tag view** — filter by any tag dimension when assembling content later.

### Optional v1.5: reflection pass
Lightweight cheap-model pass that reads each new entry and auto-suggests:
- Tags (framework area + platform intent + media type)
- Related bedrock entries (by content match against knowledge/)
- Which surface the entry might eventually belong on

Jake accepts/rejects suggestions — same pattern as chat reflections.

## Dependencies

- **None upstream** — journal can start accumulating day 1, entries just need a writable folder.
- **Downstream** — `public_surface_build` surfaces pull FROM the journal when assembling content.
- **Soft TCL link** — journal entries might cross-reference TCL `notable[]` items for the day (same event, different lens: TCL captures "what happened", journal captures "what's worth compounding").

## Comparator hint

`reservoir_building`. Medium-high weight (0.75-0.85) because the compounding value is high and the daily cost is low.

## Streak candidate

- `journal_entry_today` — daily. Jake explicitly named this as **probably the single most valuable streak in the whole set** because it compounds directly into public-surface development.

## Open questions

- Minimum viable entry: what counts? One paragraph? A sentence + a screenshot? Hard floor prevents gaming; too-hard floor makes the streak break-prone on low-energy days.
- Tag vocabulary evolution: who manages the canonical tag list? Free-text with a cleanup pass? Controlled vocabulary from the start?
- Attachment storage quota / git-ignore behavior — video clips get big fast. Local-only vs. synced?
- Reflection pass cadence: on every write, or batched nightly?
- Does the reflection pass's "which surface" suggestion auto-queue content into `public_surface_build`'s surface-specific backlogs, or just tag and wait for Jake to pull manually?

## Structural note

This spec turns a known capture failure into an instrumented discipline. Jake's current pattern: brilliance → chat → lost. Target pattern: brilliance → journal entry → tagged → retrievable → shaped → shipped. The journal is the ingestion end of the content flywheel; `public_surface_build` is the emission end. Both have to exist for the flywheel to turn.

## Cross-links

- `public_surface_build` project — downstream consumer of the journal's output.
- `anchor journal_entry_today` — the scoring dimension.
- `reservoir_building` regime — this anchor is the first inhabitant; others may follow (e.g., voice-memo capture, link/paper bookmark capture as subordinate reservoirs).
- `three_layer_memory_system` — journal is the conscious-capture layer; TCL is the session-residue layer; bedrock is the crystallized layer. All three layers get represented.
