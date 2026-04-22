# Secretary Spec — Sub-Agent Fleet

**Status:** drafted — not yet built; specialist agent designs already exist (~21 from framework work)
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

Secretary is currently an orchestrator without a fleet. The missing piece is a set of typed sub-agents that the orchestrator delegates to — each with its own **jurisdiction**, **failure mode**, and **handoff grammar**.

From existing framework work, Jake already has ~21 specialist agents designed with jurisdiction contracts, handoff graphs, and failure mode taxonomies. Time to move those from spec into running code inside Secretary so there's something to use below the top-level orchestrator.

## Why it matters

The orchestrator alone handles framing and commitment. The sub-agents handle **execution quality**. Without them, every task has to be handled at orchestrator-level generality — fine for proposals, too coarse for the actual artisan work of drafting, researching, auditing. Sub-agents are where the framework's "jurisdiction contracts" become an operational feature rather than a design document.

## Minimal v1 scope

### Directory layout
- `agents/` — one subfolder per sub-agent.
- Each subfolder contains `agents.md` declaring:
  - Jurisdiction (what it can do)
  - Inputs (typed)
  - Outputs (typed)
  - Failure modes
  - Escalation rules (when to hand back to orchestrator, when to hand off sideways)

### Sub-agent registry
Single index the orchestrator reads to know who's available and what they do. Typed, versioned, source-of-truth for what the fleet can cover.

### Delegation mechanism
- Orchestrator hands a typed task to a sub-agent.
- Sub-agent returns a typed result **or** a typed abstention (the framework-lawful move when the task is outside jurisdiction).
- Typed abstention is first-class here — it's how jurisdiction contracts actually get enforced operationally.

### First 3-5 sub-agents (earn their keep immediately)
- **Research/enrichment agent** — pulls context, cites sources, returns typed findings.
- **Drafting agent** — message drafts, typed by channel (SMS / email / slack / iMessage).
- **Red-team agent** — ties directly into `framework_red_team_certification`. Challenges claims and candidate moves.
- **Voice-audit agent** — enforces the voice model (which isn't loaded yet — blocker).
- **Calendar/scheduling agent** — reads calendar, proposes slots, handles tentative vs. firm distinction.

## Dependencies

- **Orchestrator stage-selection logic** — still an open thread on the Secretary project. Sub-agents can't be delegated to until the orchestrator knows how to pick a stage.
- **Voice model not yet loaded** — blocks the voice-audit agent specifically.
- **21 specialist agents spec location** — Jake has these designed somewhere in the framework work. Need to locate and pull the jurisdiction contracts + handoff graphs into `agents/` as starting material. Open question.
- **Typed abstention already exists as a commitment** — the operational semantics are already declared, sub-agents inherit them.

## Comparator hint

`system_capability_depth`. Direction anchor, not fidelity anchor. Weight high (0.9) on the building dimension — doesn't need to score against daily moves.

## Open questions

- Which of the ~21 specialist agents ship in v1 vs. which stay as specs until their jurisdiction shows up in real work?
- Agent versioning: versioned per `agents.md` commit, or each sub-agent has its own version lifecycle?
- Handoff graph encoding: declared in each agent's `agents.md`, or centralized in the registry?
- Typed-result schema: per-agent, or a unified return type with per-agent payload?
- Sub-agent model selection: each agent declares the model tier it needs, or orchestrator picks at delegation time?

## Structural note

Sub-agents are where the "orchestrator-as-stage-selector is a general primitive" claim gets tested. If the same orchestrator cleanly delegates to a drafting agent, a red-team agent, and a calendar agent — and each of them returns typed results or typed abstentions — that's evidence the primitive generalizes. If the delegation mechanism fragments into per-agent special cases, that's evidence the primitive doesn't.

## Cross-links

- `framework_red_team_certification` — the red-team agent is the execution layer for that project.
- `typed_abstention_first_class` commitment — directly inherited.
- `secretary` project — stage_inventory_open_threads already names "typed registry" and "Orchestrator's stage-selection logic" as open; sub-agent fleet can't land before those do.
- `rod_chief_of_staff_framework_native_ai_product` — Rod is sibling product, validated the two-mouse UI discipline. Rod's proposal engine is effectively orchestrator-level; sub-agents are the next layer down.
