# igpt-procurement

Procurement intelligence for procurement teams, category managers, and
operators handling vendor relationships. Turn the email already in your
inbox into a live picture of contract renewals, supplier risk, vendor
performance, purchase orders in flight, pricing history, and active
escalations.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Procurement runs on email — between the vendor, the business owner, and
the procurement team. Renewal dates and notice periods sit on calendars
nobody centralizes until 30 days out. A vendor's CFO mentions "supply
chain pressure" in a thread and nobody connects it to the late
deliveries last month. POs get raised, confirmations come back across
weeks, and matching them to invoices is somebody's quarterly headache.
Pricing history with each vendor lives across 18 months of threads
that nobody reconstructs until the next negotiation. SLA breaches get
escalated, then the escalation drifts.

This plugin gives you six focused workflows that mine your supplier
email and return structured answers about what's actually open, at
risk, or about to come due.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What contracts are coming up to renew?"
>
> "Any supplier risk signals?"
>
> "Trace the pricing history with Atlas Logistics."
>
> "What POs are still open?"
>
> "Any vendor escalations active?"
>
> "What did each vendor commit to this quarter?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning vendor risk scan.** *"Any supplier risk signals?"*
The `supplier-risk-signals` skill returns early warning patterns
across vendors — financial pressure language, capacity constraints,
contact turnover, quality slippage, single-source dependencies. You
spot a combination at one vendor (capacity constraints + new contact
+ two late deliveries) that warrants a direct call.

**Mid-week PO check.** *"What POs are still open?"*
`purchase-order-tracker` returns POs not yet confirmed, awaiting
delivery, or missing invoices. Two POs past expected delivery without
explanation; vendor follow-up.

**Pre-negotiation prep.** *"Trace the pricing history for Atlas
Logistics."* `pricing-negotiation-history` reconstructs every quote,
concession, agreed rate, and pricing commitment with that one vendor —
material to walk into the renewal conversation knowing the trajectory.

**Renewal calendar.** *"What contracts are coming up to renew?"*
`contract-renewal-radar` returns vendor contracts with renewal dates,
notice periods, auto-renew flags, and renegotiation signals. Three in
the next 60 days; one with a clear renegotiation opportunity based on
usage data and the pricing history.

---

## The skills

| Skill | When to use it |
|---|---|
| [`contract-renewal-radar`](skills/contract-renewal-radar/) | Vendor contracts with renewal or expiry dates, notice periods, auto-renewals, renegotiation signals |
| [`pricing-negotiation-history`](skills/pricing-negotiation-history/) | Reconstructs the full pricing conversation with a specific vendor — quotes, concessions, agreed rates, future commitments. Requires a vendor name. |
| [`purchase-order-tracker`](skills/purchase-order-tracker/) | POs referenced in email — supplier, amount, confirmation status, expected delivery, invoice received |
| [`supplier-risk-signals`](skills/supplier-risk-signals/) | Early warning patterns — financial pressure, capacity constraints, contact turnover, quality, single-source dependencies |
| [`vendor-commitment-tracker`](skills/vendor-commitment-tracker/) | Promises vendors made (delivery dates, SLAs, price holds) — fulfilled vs. open |
| [`vendor-escalation-log`](skills/vendor-escalation-log/) | Escalations, complaints, unresolved issues, SLA breaches across the supplier base |

Each skill collects what it needs from you (time window, vendor
category, specific vendor, etc.) and returns structured findings with
evidence from the actual email threads. Commercial terms — notice
periods, discount levels, payment terms, SLA percentages — are
presented verbatim, not rounded or paraphrased.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"where am I exposed in the supply
chain"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — supplier risk and active escalations
first, then contracts expiring soon, then unfulfilled vendor
commitments and open POs.

The agent enforces the plugin's care rules: surface combinations of
risk signals as higher-confidence indicators (not single hiccups), and
preserve commercial terms verbatim so a procurement team can act on
them without re-deriving the numbers.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Commercial
terms are quoted verbatim. The structured output that powers the
rendering is documented under "Output schemas" below if you want to see
it.

---

**You:** what contracts are coming up to renew?

**Claude:** *(running `contract-renewal-radar` — scanning vendor and contract email from the last 24 months)*

**11 contracts tracked. 5 in the next 90 days. 2 require decisions
this month.**

**Decision needed this month**

**Beacon Cloud — IaaS Master Agreement**
- Renews: Apr 1 (auto-renew, annual)
- Annual value: $180,000
- Notice period: **30 days written notice** (per §11.4)
- Days until notice window closes: 22
- Renegotiation signal: usage at 65% of committed capacity for the
  past 6 months
- *Recommended: renegotiate before auto-renew. Capacity reduction
  conversation is supported by the usage data.*

**Atlas Logistics — Logistics Services Agreement**
- Renews: Apr 14 (auto-renew, 2-year term)
- Annual value: $96,000
- Notice period: **60 days written notice** (per Schedule A §3)
- Days until notice window closes: -7 (window already inside notice)
- Open issue: 2 missed delivery dates this quarter (see
  vendor-escalation-log)
- *Recommended: do not auto-renew before the SLA conversation
  resolves. Notice window has already passed; pricing leverage is
  reduced.*

**Decision needed in 60 days**

**Constellation Software — Enterprise License** (renews May 8)
$240,000/yr. 30-day notice. No open issues. Standard renewal motion.

**Marina Industrial — Raw Materials Supply** (renews May 22)
$420,000/yr. 90-day notice. Pricing locked through term; renewal
should focus on volume commitment for next year.

**Northwind Components — Electronic Components** (renews Jun 3)
$160,000/yr. 45-day notice. Single-source dependency; risk-signal
review before renewal recommended.

> *Want me to draft the Beacon Cloud renegotiation note or build a
> position summary for the Atlas Logistics SLA conversation?*

---

**You:** any supplier risk signals?

**Claude:** *(running `supplier-risk-signals` — scanning the last 90 days of vendor email for early warning patterns)*

**3 vendors with risk patterns worth attention. None are crises — but
each is a combination, not a single signal.**

**Atlas Logistics — combination signal (high attention)**

Three patterns at the same vendor in the same quarter:
- **Capacity constraints** — vendor referenced "supply chain pressure"
  and "longer lead times" in two threads (Feb 4, Feb 22).
- **Contact turnover** — primary contact (account manager) departed
  Feb 11; new contact has missed two scheduled calls.
- **Quality / delivery** — 2 missed delivery dates this quarter,
  flagged in vendor-escalation-log.

The combination is the signal. Any one of these alone is normal; all
three at the same vendor in the same quarter is a pattern worth a
direct conversation, especially with the renewal on the calendar.

*Recommended: schedule a vendor business review with their senior
account leadership before renewal.*

**Northwind Components — single-source dependency (moderate)**

Single supplier for a critical electronic component. No vendor
problems currently — but reliance on one source is itself the signal.
Renewal in June.

*Recommended: surface for procurement strategy review; sourcing a
backup is a longer-term project but worth scoping.*

**Marina Industrial — pricing pressure language (watch)**

Vendor mentioned "input cost increases" twice in the last 6 weeks
without yet asking for a price adjustment. Often a precursor.

*Recommended: monitor; have a counter-position ready before the next
quarterly review.*

> *Want me to draft a vendor business review request for Atlas
> Logistics or a sourcing-strategy brief for Northwind?*

---

**You:** trace the pricing history for atlas logistics

**Claude:** *(running `pricing-negotiation-history` — reconstructing the full pricing conversation with Atlas Logistics from the last 24 months)*

**Pricing trajectory with Atlas Logistics — 24-month reconstruction.**

**Mar 2024** — Initial pricing
Per-shipment rate: $42.00. Volume commitment: 200 shipments/month.
Annual value: $100,800.

**Sep 2024** — First negotiation (renewal of original term)
Atlas proposed: $46.00 (+9.5%). Justification: fuel pass-through +
labor inflation.
We countered: $43.50.
Agreed: **$44.00 per shipment**, locked for 12 months.
Volume commitment maintained at 200/month.

**Mar 2025** — Mid-term volume adjustment
Volume increased to 280 shipments/month (peak season).
Atlas held the agreed rate ($44.00) — no surcharge.
*Worth noting: this was a goodwill gesture; not contractually
required.*

**Sep 2025** — Second negotiation (current term)
Atlas proposed: $48.50 (+10.2%).
We countered: $44.00 (hold).
Agreed: **$46.00 per shipment**, locked for 12 months.
Volume commitment: 240/month (raised from 200).

**Pricing commitment for next renewal** (per Atlas's email Sep 2025):
*"We expect modest input pressure into 2026 but will work with you on
a measured adjustment, not a step change."* — Atlas account director.

**Direction of movement**

Per-shipment rate: $42.00 → $44.00 → $46.00 over 24 months
(+9.5% total).

**Negotiation patterns to use in the upcoming renewal**

- Atlas opens at +9–10% and lands ~5%. Plan accordingly.
- Goodwill gesture in Mar 2025 (held rate during volume spike) is
  a useful credit to acknowledge.
- Their own commitment language ("measured adjustment, not a step
  change") sets a ceiling you can hold them to.
- Current SLA performance gives you leverage — combination of risk
  signals (see supplier-risk-signals) and 2 missed deliveries this
  quarter is a real position.

> *Want me to draft a renewal-preparation memo with the position and
> opening, or a short briefing for the procurement lead?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the procurement agent kicks in, running 4 skills in parallel
against your email through iGPT — contract renewals, supplier risk,
vendor commitments, vendor escalations...)*

**This week, in priority order:**

**Decisions this week**

1. **Beacon Cloud — renegotiate before Apr 1 auto-renew**
   Usage at 65% of committed capacity; renegotiation supported.
   Notice window closes in 22 days.

2. **Atlas Logistics — do not auto-renew before SLA resolves**
   Combination risk signal + 2 missed deliveries; pricing leverage
   exists. Renewal in 35 days.

**Vendor management (this week)**

3. **Atlas Logistics — vendor business review with senior leadership**
   Tied to the renewal posture; 3-pattern combination warrants a
   direct conversation.

4. **2 POs past expected delivery without explanation**
   Routine vendor follow-up.

**Open commitments**

5. **2 SLA commitments unfulfilled** (Atlas Logistics + Northwind
   Components)
   Track for renewal leverage and supplier-relationship clarity.

**Watch**

6. **Marina Industrial — input cost language pattern**
   No request yet, but be prepared for a price-increase ask in the
   next quarterly review.

7. **Northwind Components — single-source dependency**
   Strategic project; not this week, but on the procurement strategy
   list before June renewal.

> *Where would you like to start? I can draft the Beacon
> renegotiation note, the Atlas vendor business review request, the
> PO follow-ups, or a position summary for the Atlas SLA
> conversation.*

---

## How it works

When you ask, the right skill picks itself (or for broad questions, the
agent picks several). Each skill **mines your connected email through
iGPT** — it searches relevant threads and asks structured questions
about them. iGPT returns specific, evidence-backed findings; Claude then
renders them into the readable answer you see in chat.

```
You ask in chat
        ↓
Agent (or skill) routes the question
        ↓
Skill queries iGPT against your connected email
        ↓
iGPT returns structured findings (with evidence)
        ↓
Claude renders the findings into readable markdown
```

You ask in plain language and the right answer comes back, grounded in
your actual threads. The structured output that powers it is available
in the schemas section below for anyone integrating directly.

**Commercial terms preserved verbatim.** Notice periods, payment
terms, SLA percentages, discount levels, contractual quantities, and
prices are quoted as they appear in email. Procurement work depends
on these being right; the skills and agent never round or paraphrase
commercial terms.

**Risk signals are about combinations.** A single delivery hiccup or
a lost contact is a data point, not a vendor failure. Patterns and
combinations (e.g. capacity constraints + contact turnover + quality
issues at the same vendor in the same quarter) are flagged as
higher-confidence risk indicators.

**Negotiation context.** When summarizing pricing history for a
renewal or negotiation, the skill surfaces direction of movement,
concessions made, and any pricing commitments about future periods —
the things that actually matter walking into the next conversation.

**Your data stays with iGPT.** The plugin doesn't pipe raw email to
Claude — only the structured answers iGPT extracts. Your inbox is
connected to iGPT through OAuth, not shared with the model.

---

## Install

This plugin is part of the `igpt-skills` marketplace. Install it through
your MCP client and connect your email — that's the whole setup.

### Cowork

1. **Find the iGPT plugin marketplace.** In Cowork, open the plugins
   section from the menu. You can either:
   - **search the marketplace** for *iGPT*, or
   - **add it from GitHub**: find the option to add a custom marketplace
     from a URL or GitHub repo and paste
     `igptai/skills` (or the full URL `https://github.com/igptai/skills`).

   Either path pulls the iGPT marketplace into Cowork so you can browse
   our plugins.
2. **Find `igpt-procurement`.** In the iGPT marketplace, click into
   **igpt-procurement** to see the skills and the agent it includes.
3. **Install.** Click install. Cowork sets up the plugin for you —
   no command line, no config editing.
4. **Connect your email through iGPT (one-time setup).** The first
   time you ask the plugin a question, Cowork prompts you to sign in
   to iGPT and authorize email access. A browser window opens; you
   sign in to iGPT (or create a free account), pick which email
   account to connect (Gmail, Outlook, etc.), and approve the
   read-only permissions. iGPT does the email processing on its side
   so your inbox isn't shared with Claude — Claude only ever sees the
   structured findings iGPT returns.
5. **Ask anything.** Once connected, just type questions in plain
   language — *"what contracts are coming up to renew?"*, *"any
   supplier risk signals?"* — and the right skill or the agent
   picks up automatically.

You do steps 1–4 once. After that, the plugin is always available and
your iGPT connection is remembered.

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter
`https://mcp.igpt.ai/` and complete the OAuth flow. The plugin's skills
trigger automatically based on what you ask.

### Claude Code

```
/plugin marketplace add igptai/skills
/plugin install igpt-procurement@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-procurement/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-procurement.md
└── skills/
    ├── contract-renewal-radar/
    ├── pricing-negotiation-history/
    ├── purchase-order-tracker/
    ├── supplier-risk-signals/
    ├── vendor-commitment-tracker/
    └── vendor-escalation-log/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 90 days", "the last 24 months", "May 2024", "since the
last RFP" — all fine. You don't need to type ISO dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your category
classifications, supplier tiers, risk signal categories specific to
your supply chain, escalation severity levels.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the procurement guardrails —
preserve commercial terms verbatim, treat risk signals as combinations
not single hiccups. Add the new skill to the agent's "Available
skills" list.

**Use outside MCP.** The prompts and schemas in each `SKILL.md` work
directly through the iGPT API. The skills are documented at the file
level, so you can lift their inputs and output schemas into your own
code.

---

<details>
<summary><strong>Output schemas (for developers / integrators)</strong></summary>

The skills return strict, schema-validated output to the LLM, which is
what produces the clean rendering you see above. Each schema is defined
in its `SKILL.md`. If you're integrating directly with the iGPT API,
here are two representative examples.

**`contract-renewal-radar`** — for "what contracts are coming up to
renew":

```json
{
  "as_of": "2026-03-10",
  "contracts": [
    {
      "vendor": "Beacon Cloud",
      "agreement_type": "IaaS Master Agreement",
      "renewal_date": "2026-04-01",
      "auto_renewing": true,
      "annual_value": 180000,
      "currency": "USD",
      "notice_period_clause_reference": "§11.4",
      "notice_period_text": "30 days written notice",
      "days_until_notice_window_closes": 22,
      "renegotiation_signal": {
        "type": "usage_below_committed_capacity",
        "details": "Usage at 65% of committed capacity for the past 6 months",
        "leverage": "high"
      },
      "open_issues": false,
      "recommended_action": "Renegotiate before auto-renew; capacity reduction conversation supported by usage data"
    },
    {
      "vendor": "Atlas Logistics",
      "agreement_type": "Logistics Services Agreement",
      "renewal_date": "2026-04-14",
      "auto_renewing": true,
      "term_length_years": 2,
      "annual_value": 96000,
      "currency": "USD",
      "notice_period_clause_reference": "Schedule A §3",
      "notice_period_text": "60 days written notice",
      "days_until_notice_window_closes": -7,
      "open_issues": true,
      "open_issues_summary": "2 missed delivery dates this quarter (see vendor-escalation-log)",
      "recommended_action": "Do not auto-renew before SLA conversation resolves; notice window already inside"
    }
  ],
  "decisions_this_month_count": 2,
  "renewing_within_60_days_count": 4,
  "renewing_within_90_days_count": 5,
  "summary": "11 contracts tracked. 5 in the next 90 days. 2 require decisions this month."
}
```

**`pricing-negotiation-history`** — for "trace the pricing history with
Atlas Logistics":

```json
{
  "vendor": "Atlas Logistics",
  "period_from": "2024-03-01",
  "period_to": "2026-03-10",
  "pricing_events": [
    {
      "date": "2024-03",
      "type": "initial_pricing",
      "rate": "$42.00 per shipment",
      "volume_commitment": "200 shipments/month",
      "annual_value": 100800
    },
    {
      "date": "2024-09",
      "type": "negotiation",
      "vendor_proposal": "$46.00 (+9.5%)",
      "vendor_justification": "Fuel pass-through + labor inflation",
      "our_counter": "$43.50",
      "agreed_rate": "$44.00 per shipment",
      "term": "12 months locked"
    },
    {
      "date": "2025-09",
      "type": "negotiation",
      "vendor_proposal": "$48.50 (+10.2%)",
      "our_counter": "$44.00 (hold)",
      "agreed_rate": "$46.00 per shipment",
      "term": "12 months locked",
      "volume_commitment_change": "240/month (raised from 200)"
    }
  ],
  "future_pricing_commitments": [
    {
      "date_made": "2025-09",
      "source": "Atlas account director",
      "quote": "We expect modest input pressure into 2026 but will work with you on a measured adjustment, not a step change."
    }
  ],
  "rate_trajectory": {
    "starting_rate": "$42.00",
    "current_rate": "$46.00",
    "total_change_pct": "+9.5%",
    "duration_months": 24
  },
  "negotiation_patterns": [
    "Vendor opens at +9–10%, lands at ~5% increase",
    "Goodwill gesture: held rate during 2025 volume spike (not contractually required)"
  ],
  "summary": "Rate moved $42 → $44 → $46 over 24 months (+9.5%). Vendor's own commitment language sets a ceiling for the upcoming renewal."
}
```

</details>

---

## Related

- [iGPT Skills (full marketplace)](https://github.com/igptai/skills) — all our role-specific plugins
- [iGPT Python SDK](https://github.com/igptai/igptai-python)
- [iGPT Node.js SDK](https://github.com/igptai/igptai-node)
- [API Documentation](https://docs.igpt.ai)
- [Playground](https://igpt.ai/hub/playground) — try queries before writing code

## License

MIT
