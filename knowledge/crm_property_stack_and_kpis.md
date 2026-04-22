# CRM Property Stack + KPI Stack — Operational Translation

The method only ships if the CRM reflects it. Most CRMs store admin trivia (next-contact-date, stage name, deal size) and nothing about how deals are actually won. The point of this stack is to force the CRM to carry the data that the five-step method produces, so coaching, reporting, and automation can actually operate on it.

## CRM Property Stack

### Discovery fields — populated during Map

| Property | Values | What it captures |
|---|---|---|
| Scale Preference | intimate / balanced / expansive | where on the scale axis the buyer placed themselves |
| Decision Style | decisive / consensus / partner-led | how decisions get made internally |
| Control Preference | hands-off / collaborative / high-control | how much they want to drive the process |
| Budget Posture | value-maximizing / balanced / premium-certainty | what price is doing work for |
| Customization Appetite | bespoke / guided / packaged | how bespoke the solution needs to feel |
| Buyer Vector Summary | text | one-line composite of all five positions |

### Trust / rapport fields — populated during Mirror + Align

| Property | Values | What it captures |
|---|---|---|
| Burned-By Pattern | ghosting / hidden fees / generic package / handoff chaos / last-minute changes | the prior injury the buyer is protecting against |
| Shared Standard | text | the line in the sand they refuse to cross |
| Safe-Distance Insight Confirmed | yes / no | did an Adjacent Inference land and get confirmed |
| Primary Emotional Driver | relief / certainty / status / family harmony / control | what they actually want the outcome to feel like |

### Objection fields — populated during Share

| Property | Values | What it captures |
|---|---|---|
| Objection Type | price / fit / timing / trust / authority / other | the surface complaint |
| Comparison Set | text | what they're comparing against (or "undefined") |
| Frame Clarified? | yes / no | was the axis defined before the rep answered |
| Real Concern vs Reflex Concern | real / reflex | did frame clarification reveal a deeper issue |
| Stakeholder Gravity | low / medium / high | how much unseen influence sits outside the room |

### Close fields — populated during Define

| Property | Values | What it captures |
|---|---|---|
| Next Committed Action | text | what was explicitly agreed as the next move |
| Decision Deadline | date | the deadline named (not assumed) |
| Ask Made? | yes / no | did the rep explicitly advance the deal |
| Signal-to-Action Lag | duration | time from buyer signal to rep's next move |
| Stage Exit Evidence | text | what concretely justifies this stage transition |

## KPI Stack

These ten KPIs operationalize all five engines without flattening them into generic sales-coaching.

**Ask Execution Rate** — percent of qualified calls where the rep explicitly advanced the deal. Directly measures Define discipline. Answers: "are we asking, or are we waiting?"

**Signal-to-Action Lag** — median time from buyer signal to rep move. Directly measures Motion Control. Answers: "are we fast enough?"

**Frame Clarification Rate** — percent of objections clarified (axis named, comparison set defined) before any pitch or discount. Directly measures Frame Control discipline. Answers: "are we diagnosing, or defending?"

**Standard Alignment Capture Rate** — percent of opportunities where the buyer's line in the sand is explicitly documented. Directly measures Align discipline. Answers: "are we building tribe, or just pitching features?"

**Discovery Resolution Score** — number of key axes mapped before proposal is drafted. Directly measures Map discipline. Answers: "does the proposal have a target, or is it a generic shot?"

**Proposal Match Score** — how tightly proposal language mirrors the buyer vector. Measures the bridge from Map to Define. Answers: "does the proposal sound like the map talking back?"

**Stakeholder Activation Rate** — percent of deals where secondary decision-makers were engaged before the first stall. Measures Stakeholder Gravity literacy. Answers: "are we surfacing the shadow buyers before they kill the deal?"

**Undefined Deal Days** — days with no concrete next step. Measures heat loss. Answers: "how much is this deal cooling?"

**Discount-Before-Diagnosis Rate** — how often price concessions happen before frame clarity. Inverse KPI — lower is better. Answers: "how often are we burning margin inside someone else's fog?"

**Trust-Speed Score** — how quickly buyers begin offering voluntary context on the call. Measures Intel Calibration effectiveness. Answers: "does our prep sound like empathy, or evidence?"

## How this maps to Andre's Command Center

See `andre_raw_sales_command_center_framework_instantiated` — Andre's system already has 8 of 10 consciousness modules live. The CRM stack above is a candidate **next-module specification**: the data layer that would make the Command Center's typed recommendations richer. Specifically:

- The Command Center's current "verify latest Close activity" gate could be enriched with "verify Frame Clarified? = yes before committing a discount recommendation."
- Andre's Signal-to-Action Lag becomes a live metric rather than an implicit one.
- Stakeholder Activation Rate becomes a typed input to the Oracle's follow-up decisions.

This is open as a product decision — integration timing and scope belong to Jake.

## Why this stack, not the standard sales-CRM stack

Standard CRM stacks store *pipeline state*: stage, amount, close date, owner, next contact. That's enough for reporting. It's not enough for coaching or automation because none of those fields record *how* the deal is progressing, only *where* it is.

This stack stores *how*. Was the frame clarified? Is the shared standard captured? What's the buyer vector? Those are the fields that let a coach watch a stall and diagnose the actual cause rather than guess from call recordings.

## Cross-references
- Source: `buyer_vector_method_source` §3, §4
- Umbrella: `buyer_vector_method_umbrella`
- Integration target: `andre_raw_sales_command_center_framework_instantiated`
- Engines: all five
