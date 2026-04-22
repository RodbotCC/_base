# Secretary Spec — Contact Layer (Rebuild the Human Contact Layer)

**Status:** drafted — not yet built
**Scope:** Secretary app + people/ bedrock folder
**Source:** Jake writeup, 2026-04-22

---

## The core claim

Fill out Secretary's contacts and reestablish a daily/weekly rotation with people worth staying in orbit with. The AI work pulled Jake into hermit mode. Time to reverse that.

Hermit mode is a specific cost of the AI work that needs a specific countermeasure. Declared as an anchor regime, it becomes a scoring dimension; undeclared, it stays drift.

## Operational shape

### People schema extension
Each `people/` entry gets:
- `name`
- `role`
- `last_contact` — ISO date or null
- `owed_response` — boolean + optional context
- `relationship_weight` — 0.0-1.0
- `cadence` — enum: `daily` | `weekly` | `monthly` | `dormant-but-keep-warm`

### Contacts view
A Secretary view that surfaces aging-out:

> "You haven't talked to X in 6 weeks. Relationship weight 0.7, cadence says monthly. This is drifting."

### Morning-grid integration
Morning grid occasionally proposes a reconnection move — same mechanism it uses to propose a Rodrigo text. Candidate selection: aging × weight × cadence.

## Why it matters

Hermit mode is a specific cost of the AI work that needs a specific countermeasure. Declared as an anchor → scoring dimension. Undeclared → drift.

## Streak candidates

- `reached_out_to_one_person_today` — daily
- `contacts_maintained_this_week` — weekly rollup of how many relationship anchors got touched

Comparator hint: `relationship_network_fidelity`. Weight 0.7-0.8 — important enough to score daily, not important enough to outrank the core-partnership daily fidelity (Rodrigo/Andre) when they compete for the same window.

## Dependencies

- **TCL** — last_contact timestamps update off TCL entries (when a conversation is logged, contact record updates).
- **Streak tracker** — reads the two new anchors.
- **Grid generator** — reads the Contacts view state to pick reconnection candidates.

## Open questions

- `owed_response`: boolean only, or should it also capture the content (what you owe, when they asked, the link to the message)?
- `cadence` default for new entries: null, `monthly`, or inferred from relationship_weight?
- Aging-out threshold: function of cadence (missed 3× cadence = "drifting") or absolute (>30 days = drifting regardless)?
- How does the Contacts view surface dormant-but-keep-warm contacts differently from cadence-driven ones? (Dormants don't drift on a clock — they drift on life events.)
- Does a reconnection move proposed by the grid require Jake's approval, or auto-queue into a "reach out" list?

## Cross-links

- Anchors from batch 2 (`rodrigo_morning_text`, `andre_afternoon_text`) are a tighter-cadence instance of this same mechanism — these two anchors are the specialized case, the contact-layer anchors are the general case.
- `daily_relationship_cadence` commitment covers Rodrigo/Andre; the new `reverse_hermit_mode` commitment covers the broader network.
- Anchor regime `relationship_network_fidelity` sits adjacent to `relationship_maintenance_fidelity` — both score on relationship health but at different weight tiers, different cadences, different failure modes.
