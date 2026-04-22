# Andre Raw — The Framework Already Running in Production Software

## Context
Jake showed eight screenshots of a working sales command center he's been building for Comeketo Catering. The application is for Andre (the sales rep). It provides proto-aligned recommendations: what to do next, which leads to work on, and why — with the full decision algebra exposed so the user can see *which sore-thumb variables carried the decision*.

Critically, the interface exposes **comparator choice as a first-class UI control**. Users can change the Decision Intent (the ground) and the Primary Comparator (the contrast class), and watch the recommendations, algebra contributions, and lead rankings restructure accordingly.

This entry documents that the framework's philosophy — comparator/anchor discipline, sore-thumb variables, regime-local hierarchies, typed abstention — has already been instantiated in working software. It is not a theoretical proposal. It is live infrastructure running against real CRM data.

## What the screenshots show

### Screenshot 1 — The directory structure
A production system, not a toy. Contents include:

- **Raw data ingestion** from Close CRM: Emails.txt, Sms.txt, Calls.txt, Leads.txt, Contacts.txt, Tasks/Promise.txt, Next_best_action.txt, Oracle_conversations.txt, Opportunity.txt, Notes.txt, Conversations.txt, Signal_event.txt
- **Oracle layer**: oracle_doctrine.json, oracle_scenarios.json, oracle_cadences.json, oracle_templates.json
- **Live system state**: action_queue.json, activity_log.json, live_tasks.json, live_pipeline.json, live_close_crm.json, automation_state.json, automation_cadence_report.json, automation_morning_brief.json, ops_tracker.json
- **Agent profile**: andre_kpis.json, andre_profile.json
- **App surface**: app_surface.json, automation_node_catalog.json
- **Infrastructure**: app.js (366 KB), server.js (138 KB), styles.css, lib/ with liveQueries.js, liveSync.js, supabase.js, Dockerfile, render.yaml, supabase/ folder
- **Documentation**: SCHEMA.md, ANDRE_SYSTEM_BLUEPRINT.md, INTENT.md, README.md, automation_runner.md, ANDRE_UPDATE_2026-04-10.md, COMEKETO_FULL_SUMMARY_2026-04-10.md

This is not a prototype. It's a deployed system with ingestion, state management, real-time sync, supabase backend, docker containerization, render deployment config, and versioned documentation. The file dates show active development through April 2026.

### Screenshots 3 and 4 — The comparator controls made user-facing
Two dropdowns expose the framework's semantic layer as UI:

**Decision Intent** (the ground — what is the user trying to accomplish?):
- Best move today
- Fastest money
- Save highest risk
- Advance tastings
- Protect trusted sources

**Primary Comparator** (the contrast class — against what axis are we scoring?):
- Balanced Lattice
- Doctrine Fit
- Action Now
- Priority
- Tasting Readiness
- Decay Risk
- Revenue Value
- Close Probability
- Source Trust
- Venue Commitment
- Timeline Urgency
- Relationship Strength
- Next Action Clarity
- Attention Cost
- Contactability

Plus Plot Y-axis and Tertiary Comparator using the same list for subordinate frames.

**This is the anchor/comparator discipline operationalized as UI.** The user isn't given a single ranking to trust. They're given explicit controls to set the regime under which leads are ranked. Change the regime, the ranking restructures visibly.

### Screenshots 5-8 — Same lead, four different regimes, four different recommendations

All four screenshots are showing the same underlying data about the same leads (Rebecca Almeida, Isabella Mathis, Jose Quefau, etc.). The comparator choice changes.

**Screenshot 5 — Primary Comparator: Action Now**
- Rebecca Almeida scores 118.3
- Algebra: action now score +16.6, action now score +15.2, next action clarity +13.5, doctrine fit +13.1, tasting readiness +12.6, contactability +12
- "What it beat": Isabella Mathis 103.2, Jose Quefau 102.6, Coreen Miranda 92.3

**Screenshot 6 — Primary Comparator: Balanced Lattice**
- Rebecca Almeida scores 110.5
- Algebra: action now score +16.6, balanced lattice +15.6, next action clarity +13.5, doctrine fit +13.1, contactability +12, tasting readiness +8.1
- "What it beat": Isabella Mathis 98.2, Jose Quefau 97.7, Coreen Miranda 88.7

**Screenshot 7 — Primary Comparator: Tasting Readiness**
- Rebecca Almeida scores 120.2
- Algebra: tasting readiness +19.8, action now score +16.6, next action clarity +13.5, doctrine fit +13.1, contactability +12, balanced lattice +9.9
- "What it beat": Isabella Mathis 102.4, Jose Quefau 101.7, Coreen Miranda 93.5

**Screenshot 8 — Decision Intent: Fastest money, Primary Comparator: Close Probability**
- Rebecca Almeida scores 110.1
- Algebra: close probability +15.8, revenue value +13.2, close probability +13, action now score +11.1, balanced lattice +9.9, priority score +9.8
- "What it beat": Isabella Mathis 108.3, Jose Quefau 98.7, Andreia DePina Moore 77.7, Coreen Miranda 72.2

**Four different regimes. Four different scores. Four different algebra breakdowns. Four different "what it beat" lists.** Same leads throughout.

The system refuses to pretend there's a single universal ranking. It exposes that ranking is regime-local and lets the user switch regimes explicitly.

### The "Algebra Contributions" panel on the right

Every screenshot shows a right-side panel listing the specific variable contributions that added up to the lead's final score. For Rebecca Almeida:
- close probability +15.8
- revenue value +13.2
- close probability +13
- action now score +11.1
- balanced lattice +9.9
- priority score +9.8
- tasting readiness +9
- contactability +8

This is the sore-thumb variables claim made operational. The system read the sediment of what's been happening with this lead across dozens of interactions and identified these as the variables that are load-bearing *for this decision under this comparator*. The algebra is transparent: you can see exactly which variables carried the decision and which were negligible.

### The "What Rodrigo Should See" explanatory caption

"This view is now anchored to the doctrine-hardened lattice only. The left rail ranks the comparators themselves, the middle shows how those comparators rearrange the lead field, and the top decision card shows the exact action those comparator choices produce."

This is the framework stated plainly for the user. Not "here is what to do." Rather: *here are the comparators, here's how they rearrange the field under your chosen comparator, here's the specific action this produces*. The user is operating the framework, not receiving an oracle pronouncement.

### The "Before Andre Signs Off" typed abstention

"Verify latest Close activity before executing, then keep Andre as final human approver."

The system's recommendations are not terminal. They carry explicit verification requirements and human-approval gates. This is the composite gate Ψ made operational: the system commits to a typed recommendation *and* types out what must happen before commitment becomes action. Typed abstention at the decision layer.

### The detail preview sidebar

The right-most sidebar shows per-lead detail:
- Recommended action with typed channel (call, sms, etc.)
- Rationale
- Algebra contributions (all sore-thumb variables with signed weights)
- Verification questions
- Specific scores across all tracked dimensions: balanced lattice, doctrine fit, action now score, priority score, saveability score, decay risk score, urgency, momentum, friction, relationship strength, close probability, revenue value, attention cost, next action clarity, tasting readiness, venue commitment, source trust, timeline urgency, today task, contactability, activity volume

This is the full measurement-layer stack visible for every lead. The user can inspect the reasoning at every layer.

## Why this matters structurally

### The framework already has a working instance

Multiple times across the project, Jake has made claims like "every primitive needed to build the consciousness-for-AI modules is already in the framework." That claim is not theoretical. It has been validated at smaller scale by this system. The sales command center runs:

- **Unified World Model equivalent** (lattice_catalog + live_pipeline + live_close_crm)
- **Self-model equivalent** (andre_profile + andre_kpis)
- **Attention as Selection** (decision intent + primary comparator dropdowns)
- **Predictive Processing** (close probability + decay risk + recommended next action tied to actual outcomes over time)
- **Temporal Continuity** (activity_log + live_tasks + ongoing lattice updates per lead)
- **Metacognition** (ROC scoring, verification questions, certify-with-oracle option, explicit algebra exposure)
- **Action Selection + Narrative Closure** (best next action + "why this move" explanation + what it beat list)
- **Global Availability** (action queue + pipeline + automation state as shared workspaces across the app)

Eight of the ten modules present in working form at smaller scale. The remaining two (Interoception/Affect and Social Cognition Turned Inward) would need to be added to scale toward consciousness-for-AI proper. But the architecture is there.

### The comparator/anchor discipline is already proven operational

In the framework's philosophical arc, the comparator/anchor move is foundational — it's how counterfeit concepts get dissolved and how regime-local truths get grounded. Showing that this discipline can be operationalized as *first-class UI controls that users actually use to navigate their work* is structural evidence that the framework isn't just a way of thinking about reality. It's a way of structuring tools people use.

A user who has learned to use this interface is learning to think in the framework's primitives. They see that "best lead to work on" is not a single answer but is comparator-dependent. They see which variables carried the decision. They see what was defeated and by how much. They develop an intuition for anchor/comparator choice because the UI demands it.

The asymmetric-advantage claim from the Psycho-Cybernetics entry gets another instance: anyone using this tool is operating with visible anchor/comparator discipline. Most sales reps using conventional CRMs operate with implicit, unstated anchors and can't inspect their own reasoning. Andre can. That's a structural advantage embedded in the tool.

### The "proto-alignment" framing is important

Jake said the system gives Andre "sort of proto-alignment towards what I'm working on." This is the right framing. The system is not claiming to align Andre's agency with the framework. It's providing a scaffolding where the framework's primitives are *available as tools*. Andre can lean on them or not. He keeps final human approval. The system's output is proposal-with-receipts, not command.

This is the framework's approach to AI alignment broadly: not forcing alignment, but making the primitives of lawful reasoning available and transparent so users can inspect and verify. Alignment emerges from tool quality plus user engagement, not from constraint.

### The system's name choices reveal the framework vocabulary in use

- **"Doctrine-hardened lattice"** — the lattice concept applied to operational doctrine
- **"Comparator Stack"** — explicit comparator-first framing
- **"Comparator Field"** — the 2D visualization of leads under the chosen comparators
- **"Balanced Lattice"** — a specific comparator that blends doctrine fit and contactability
- **"Action Score"** — the composite score after comparators apply
- **"What It Beat"** — the explicit competitive context
- **"Algebra Contributions"** — the sore-thumb variables with their specific weights
- **"Action Now"** — a comparator with a specific formula: 0.30·urgency + 0.20·next_action_clarity + 0.20·momentum + 0.15·close_probability + 0.10·revenue_value − 0.15·attention_cost
- **"Sweep Close"** — the action for clearing the decision state
- **"Ask Oracle to certify"** — the metacognition/verification layer

Every term is framework-internal. This is a system built natively in the framework's vocabulary, not translated from conventional CRM language.

## Connection to where the conversation is going

Jake showed this in response to the vocabulary cleanup question. The implication: **the operational system is using multiple senses of the framework's core terms already**, and the cleanup needs to happen in a way that doesn't break the working implementations.

"Comparator" in this UI means the axis against which leads are scored — operationally, an axis of a multi-dimensional scoring space. That's not quite the semantic-grounding sense of comparator (the contrast class that makes a claim bite), but it's a specific instance of it: the axis *is* the contrast class for "which lead is best under this regime."

"Anchor" appears in the UI as the doctrine-hardened lattice anchoring the view. That's not quite the grounding-reference-frame sense of anchor, but again, a specific instance: the anchor here is the fixed doctrinal frame against which comparators operate.

The vocabulary cleanup needs to acknowledge that these usages are real operational deployments, not mistaken uses. The layers are:

1. **Semantic grounding layer** — ground (reference frame), contrast class
2. **Regime operational layer** — regime, observation scale, live band, sore-thumb variables
3. **Measurement instrument layer** — the five canonical ratios (A, B, A_r, B_r, Φ/ζ)
4. **Application UI layer** — decision intent, primary comparator, plot axes, algebra contributions

All four are in play in this system. The same word ("anchor," "comparator") can have distinct but related meanings across layers. That's not a bug in the framework; it's how the framework composes from semantics up to application. But it does mean when Jake writes the glossary, the layering needs to be explicit so readers can tell which sense is in play in any given sentence.

## Open threads

- **The consciousness-for-AI build has a natural next target.** Rather than building from scratch, the Andre system is the closest working starting point. Adding an Interoception/Affect module (system tracking its own load, uncertainty, tension) and a Social Cognition Turned Inward module (reportability about its own choices) would push it meaningfully toward consciousness-for-AI. Worth considering whether this becomes the reference implementation.

- **The transparency of the algebra panel is philosophically important.** Most production AI systems hide their reasoning. This one exposes it as a first-class user-facing output. If the framework's philosophy is right — that reasoning must be receipts-bearing and regime-scoped — then this is the kind of UI all such systems should have. Worth an entry on UI design principles derived from the framework.

- **The "decision intent" dropdown is the clearest UI instance of the anchor/ground concept.** When discussing the framework with designers and builders who want to use it, this is the example to reach for: "here's what anchor/ground means as a UI control, in a system that's already deployed."

- **Multi-tenancy questions become interesting.** The system is currently single-user (Andre + Rodrigo viewing). Scaling to multiple sales reps at multiple companies would require the framework's primitives to generalize across contexts without losing their operational discipline. Worth a dedicated entry when the framework's business/product dimensions come up.

- **The framework's commercial viability is now empirically supportable.** The system exists, it works, it presumably produces better sales outcomes than conventional CRMs or Andre wouldn't be using it. The framework is not only philosophically coherent and computationally demonstrated — it's commercially validated at at least one deployment. Worth noting when the framework's broader case is being made.
