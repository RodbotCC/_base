# Secretary Spec — AI Billing & Subscription Index

**Status:** drafted — not yet built
**Scope:** Secretary app
**Source:** Jake writeup, 2026-04-22

---

## The core claim

A simple ledger of every AI subscription, API account, and token budget Jake has in flight. When each one renews, when each one runs out, how much of the monthly bucket has been consumed. Real-time where the provider exposes usage endpoints (Anthropic, OpenAI). Manual entry where they don't.

## Why it matters

The lynchpin architecture (local Claude Code subprocess + BYO OpenAI fallback) depends on knowing which credentials are live. When a subscription expires silently or a token bucket drains, the whole Delegate layer starts failing and **the cause is invisible**. The index makes that invisible state visible.

Invisible operational substrate failures cascade everywhere. Low daily cost to honor (just watch the ledger). High cost of not honoring (silent failure that breaks unrelated-seeming things).

## Minimal v1 scope

### Ledger file
```
_ledger/ai_billing.json
[
  {
    "provider": "anthropic",
    "plan_name": "Team/API/etc.",
    "monthly_cost": 200.00,
    "renewal_date": "2026-05-15",
    "token_budget": null,
    "token_used_this_period": null,
    "notes": ""
  }
]
```

### Poller
Small poller for providers that expose usage endpoints:
- Anthropic usage API
- OpenAI usage endpoint
- Fetch every few hours, write fresh values to the ledger.

### Billing view
Settings tab (or its own top-level tab) showing:
- Which accounts are healthy
- Which are close to limits
- Which are renewing soon

### Alert mechanism
When any account hits a threshold (near budget, near renewal), it surfaces as a commitment candidate on the morning grid:

> "Anthropic billing renews in 3 days — confirm you want to continue at this tier."

## Dependencies

- **Grid generator** — needs to accept typed alert inputs from the billing subsystem and promote them into candidate cells.
- **Anthropic / OpenAI API credentials** — both need to be configured before pollers can run. This is a chicken-and-egg note: the substrate the ledger monitors includes the substrate it depends on.
- **TCL integration (soft)** — billing events (renewals, threshold crossings) could log into the day ledger, but it's not required for v1.

## Comparator hint

`operational_substrate_health`. Low-weight maintenance anchor (0.3-0.5) but critical to honor. Low weight because the daily action is cheap — you're just glancing at a dashboard. Critical because a silent failure here cascades.

## Open questions

- Alert thresholds: absolute ("80% of token budget" / "3 days to renewal") or per-account configurable?
- Manual-entry cadence for providers without usage endpoints: Jake updates weekly, monthly, or prompted on threshold?
- Does the ledger also capture one-off top-ups / prepaid credits, or only recurring subscriptions?
- Does an alert that fires on the morning grid need to be dismissable once acknowledged, or does it persist until the underlying state changes?
- Polling frequency per provider — every hour? Every 6 hours? Back-off when near limits vs. poll-harder?

## Cross-links

- Anchor `ai_billing_visibility` — the scoring dimension for this subsystem.
- Regime `operational_substrate_health` — where this anchor sits; note the regime probably eventually accumulates more anchors (hosting, domains, backup integrity, local model weights — all substrate).
- `mission_control_over_fpga` commitment — architectural discipline says operational substrate gets visible representation; this spec is that commitment applied to the AI billing layer.
