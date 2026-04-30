# igpt-realestate

Real estate intelligence for residential and commercial agents,
brokers, and team leaders. Turn the email already in your inbox into
a live picture of your active deals, what each client really wants,
which listings are expiring, and which vendor steps are gating
closings.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Real estate runs on email — between the client, the other agent, the
lender, the inspector, the title attorney, the contractor, the
photographer, the seller's family. A buyer's preferences shift over
six months of showings and the agent's mental model lags behind.
Listings expire and the agreements drift onto someone's calendar
without a renewal conversation. Closing-week coordination scatters
across a dozen vendor threads. Every offer history with a client
lives in 30+ messages spread across MLS, email, and phone notes.
Commission agreements get drafted in a thread and then nobody
reconstructs whether payment actually happened.

This plugin gives you six focused workflows that mine your real
estate email and return structured answers — what's stuck, what's
expiring, what each client actually said they wanted, what the
vendor critical path looks like for the deal closing in 18 days.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Where do my deals stand?"
>
> "What listings are about to expire?"
>
> "What does the Henderson family really want?"
>
> "Trace the offer history for the Chens."
>
> "What's gating the Maple Ave closing?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list
of where to spend your attention.

---

## A typical week

**Monday morning pipeline review.** *"Where do my deals stand?"* The
`deal-pipeline-tracker` returns every active transaction with stage,
key parties, next step, and expected closing. You see one deal has
slipped from "under contract" silently because of an inspection
finding nobody actioned.

**Wednesday before showings.** *"What does the Henderson family
really want?"* `client-preference-miner` returns everything the
Hendersons have expressed — explicit must-haves, deal-breakers,
budget shifts, location preferences — and flags what has *changed*
since they started looking. You walk into showings knowing their
budget went up $50K last month and the school district is now a
must.

**Mid-week vendor coordination.** *"What's gating the Maple Ave
closing?"* `vendor-coordination-tracker` returns inspector, appraiser,
title, lender, attorney status. Inspector confirmed; appraisal
delivered; title pending one document; lender awaiting income
verification.

**End of month, listing review.** *"What listings are about to
expire?"* `listing-expiry-tracker` returns listing agreements with
expiry dates, notice periods, and seller renewal signals. Two are
expiring in 30 days; one seller has hinted at switching agents.

---

## The skills

| Skill | When to use it |
|---|---|
| [`client-offer-history`](skills/client-offer-history/) | Reconstructs a specific client's full offer history — prices, counters, outcomes, seller feedback. Requires a client name. |
| [`client-preference-miner`](skills/client-preference-miner/) | Preferences and reactions a specific client has expressed; surfaces what has changed over the search. Requires a client name. |
| [`commission-agreement-tracker`](skills/commission-agreement-tracker/) | Commission, referral, and co-brokerage arrangements — rates, conditions, payment status |
| [`deal-pipeline-tracker`](skills/deal-pipeline-tracker/) | Active transactions — stage, key parties, next step, closing date, blockers |
| [`listing-expiry-tracker`](skills/listing-expiry-tracker/) | Listing agreements with expiry dates, notice periods, renewal / extension signals |
| [`vendor-coordination-tracker`](skills/vendor-coordination-tracker/) | Vendor coordination on active transactions — inspectors, appraisers, contractors, title, lender, attorney; what's confirmed, what's outstanding |

Each skill collects what it needs from you (time window, client,
property, etc.) and returns structured findings with evidence from
the actual email threads. Prices, dates, and contingency deadlines
are presented verbatim — never rounded or approximated.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"walk me through my book"*. The
agent picks the right skills, runs them in parallel, and synthesizes
a prioritized list — closing-critical vendor items first, then
listings expiring soon, then deals at risk, then commission items
outstanding.

The agent enforces the plugin's care rules: prices and dates verbatim,
preference changes flagged explicitly (often what the client said
two months ago no longer holds), and two skills (offer history and
preference miner) require a specific client name — the agent will ask
before running.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Numbers and
dates are quoted verbatim. The structured output that powers the
rendering is documented under "Output schemas" below if you want to
see it.

---

**You:** where do my deals stand?

**Claude:** *(running `deal-pipeline-tracker` — scanning active transaction threads from the last 6 months)*

**6 active transactions. 1 needs attention today.**

**Closing in 18 days — 447 Maple Ave** ($785,000)
Buyer: the Hendersons. Stage: under contract.
Critical-path items: appraisal **delivered Mar 5** at $792K; title
**pending** one document from seller's prior refinance; lender awaiting
buyer's income verification (requested Mar 7).
Risk: lender item is gating; if not in by Mar 14 the closing slides.
*Action: chase the buyer for income docs today.*

**Closing in 32 days — 12 Oak Lane** ($1,250,000)
Buyer: Mr. and Mrs. Chen. Stage: under contract; inspection
contingency expires Mar 17.
Critical-path items: inspection completed Mar 6; **3 inspection
findings** (roof, HVAC, electrical panel) require negotiation by
Mar 17. Seller initial response: willing to credit $8K; buyer
counter: requesting $18K.
*Action: schedule a call with both sides this week to land a number.*

**Pre-listing — 1450 Pine Street**
Owner: Jenkins family. Stage: pre-listing prep. Photographer
scheduled Mar 12; pre-listing inspection Mar 14; listing live Mar 18.
*Status: on track.*

**Active showings — Henderson family search**
Multiple properties shown over last 6 weeks; their preferences have
shifted (see preference miner). Continue showing.

**Closed — 88 Elm Court** (closed Feb 28)
Closed at $612,000. Commission posted to office.

**Closed — 233 Cedar Lane** (closed Feb 22)
Closed at $445,000. Commission still pending office processing —
flagged in commission-agreement-tracker.

> *Want me to draft the income-doc chase to the Hendersons or a
> negotiation approach for the Oak Lane inspection items?*

---

**You:** what does the henderson family really want?

**Claude:** *(running `client-preference-miner` — reconstructing the Hendersons' full preference picture from email since they started searching)*

**The Hendersons — 6-month preference picture.**

**Must-haves (consistent throughout)**

- 4+ bedrooms (firm — they have 3 kids)
- Yard for dogs ("we won't compromise on this")
- Walking distance to a park

**Must-haves (developed during search)**

- **School district — added Feb 14.** Their oldest is starting middle
  school next fall; this became a hard constraint after a tour they
  didn't enjoy.
- **No HOA fees over $200/mo — added Jan 22.** They saw a property
  with a $480/mo HOA and were taken aback.

**Nice-to-haves**

- Updated kitchen (they'll renovate, but prefer not to)
- Home office (one of them now works hybrid)
- South-facing yard

**Deal-breakers (confirmed during search)**

- Busy main road (toured 12 Sycamore, didn't like it)
- Pool requiring maintenance
- Significant deferred maintenance

**Budget shifts**

- Started at **$650,000** (Sep 2025)
- Stretched to **$725,000** in November (after one home they loved)
- Currently at **$785,000** (since Feb 22) — bank pre-approval increased
  after Mr. Henderson's promotion

**What has changed recently (worth noting before the next showing)**

- Budget up $60K from October baseline.
- School district added as a must-have.
- HOA cap added.
- Yard requirement softened slightly — they said *"we'd consider a
  smaller yard if there's a park very close"*.

> *Want me to package this as a pre-showing brief, or build a
> property-fit checklist from the latest preference picture?*

---

**You:** what's gating the maple ave closing?

**Claude:** *(running `vendor-coordination-tracker` — scanning the 447 Maple Ave transaction threads from the last 60 days)*

**447 Maple Ave — closing in 18 days. 2 vendor items on critical
path.**

**On critical path**

**Lender — buyer income verification** (requested Mar 7, not yet
received)
Lender (Constellation Mortgage) requires updated W-2 + last 2 pay
stubs. Buyers acknowledged the request Mar 8; nothing received.
*Action: chase the buyers today; if not received by Mar 14, closing
slides.*

**Title — seller's prior refinance discharge** (pending)
Title (Beacon Title) flagged Mar 4 that the seller's prior refinance
needs a discharge confirmation. Seller's attorney is sourcing it from
the prior lender; ETA "early next week".
*Action: confirm with seller's attorney mid-week; have a fallback
plan if the discharge takes longer.*

**Confirmed**

- **Inspector** — inspection report delivered Feb 28; no findings
  requiring negotiation. Closed.
- **Appraiser** — appraisal delivered Mar 5 at $792K (over contract
  price of $785K). Closed.
- **Buyer's attorney** — review complete; no items outstanding.

**Watch**

- Closing-day walkthrough scheduled Mar 27. No issues anticipated.

> *Want me to draft the income-docs chase for the Hendersons or a
> mid-week check-in with the seller's attorney?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the realestate agent kicks in, running 4 skills in
parallel against your email through iGPT — deal pipeline, vendor
coordination, listing expiry, commission tracking...)*

**This week, in priority order:**

**Closing-critical (today)**

1. **Maple Ave — chase buyer's income verification**
   Lender item; without it closing slides past Mar 27.

2. **Oak Lane — inspection-finding negotiation by Mar 17**
   Buyer countered $18K vs. seller's $8K offer; gap to close this
   week.

**Listings (this week)**

3. **2 listings expiring in 30 days — 1 has churn signal**
   One seller has hinted at switching agents in a recent thread.
   Direct conversation needed before agreement expires.

**Commission**

4. **233 Cedar Lane commission pending office processing**
   Closed Feb 22. Past office's typical turnaround.

**Active work**

5. **Henderson preference shift — budget up $60K, school district now
   must-have**
   Update the showing list.

6. **Pine Street pre-listing — photographer + inspection on track**
   No action needed; review at the Friday huddle.

> *Where would you like to start? I can draft the Hendersons' income
> chase, the Oak Lane negotiation note, the listing-expiry seller
> conversation, or the office commission follow-up.*

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

**Prices and dates verbatim.** Offer prices, listing prices, closing
dates, contingency expirations, commission percentages — all quoted
as they appear in email. Real estate work depends on these being
right; the skills and agent never round or approximate.

**Preference changes are flagged explicitly.** Buyers shift through
a search — budget moves, must-haves get added, deal-breakers get
discovered after a tour. The preference miner surfaces *what changed*
alongside the current picture, because what a client said two months
ago often no longer holds.

**Two skills require a client name.** `client-offer-history` and
`client-preference-miner` only make sense for a single named client —
there's no "all clients" mode. The agent asks before running.

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
2. **Find `igpt-realestate`.** In the iGPT marketplace, click into
   **igpt-realestate** to see the skills and the agent it includes.
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
   language — *"where do my deals stand?"*, *"what listings are about
   to expire?"* — and the right skill or the agent picks up
   automatically.

You do steps 1–4 once. After that, the plugin is always available and
your iGPT connection is remembered.

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter
`https://mcp.igpt.ai/` and complete the OAuth flow. The plugin's skills
trigger automatically based on what you ask.

### Claude Code

```
/plugin marketplace add igptai/skills
/plugin install igpt-realestate@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-realestate/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-realestate.md
└── skills/
    ├── client-offer-history/
    ├── client-preference-miner/
    ├── commission-agreement-tracker/
    ├── deal-pipeline-tracker/
    ├── listing-expiry-tracker/
    └── vendor-coordination-tracker/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 6 months", "since the spring market", "May 2024", "since
the listing went live" — all fine. You don't need to type ISO dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your transaction
classifications, vendor types specific to your market, commission
arrangement types, listing-status taxonomies.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the real estate guardrails —
prices and dates verbatim, preference changes surfaced. Add the new
skill to the agent's "Available skills" list.

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

**`deal-pipeline-tracker`** — for "where do my deals stand":

```json
{
  "as_of": "2026-03-10",
  "deals": [
    {
      "property_address": "447 Maple Ave",
      "transaction_type": "purchase",
      "client_role": "buyer",
      "client_name": "Hendersons",
      "stage": "under_contract",
      "contract_price": 785000,
      "currency": "USD",
      "expected_closing_date": "2026-03-27",
      "days_to_closing": 18,
      "critical_path_items": [
        {
          "type": "lender",
          "status": "awaiting_buyer_income_verification",
          "requested_date": "2026-03-07",
          "blocking": true
        },
        {
          "type": "title",
          "status": "pending_seller_prior_refinance_discharge",
          "blocking": true
        },
        {
          "type": "appraisal",
          "status": "complete",
          "appraised_value": 792000,
          "blocking": false
        }
      ],
      "risk_level": "moderate",
      "recommended_action": "Chase buyer for income docs today; closing slides if not received by Mar 14"
    },
    {
      "property_address": "12 Oak Lane",
      "transaction_type": "purchase",
      "client_role": "buyer",
      "client_name": "Chen",
      "stage": "under_contract_inspection_negotiation",
      "contract_price": 1250000,
      "currency": "USD",
      "inspection_contingency_expires": "2026-03-17",
      "expected_closing_date": "2026-04-11",
      "inspection_findings_count": 3,
      "current_negotiation": {
        "buyer_request": 18000,
        "seller_offer": 8000,
        "gap": 10000
      },
      "recommended_action": "Schedule call with both sides this week to land a number"
    }
  ],
  "active_count": 6,
  "closing_within_30_days_count": 2,
  "summary": "6 active transactions. Maple Ave needs lender follow-up today; Oak Lane needs inspection-finding negotiation by Mar 17."
}
```

**`client-preference-miner`** — for "what does the Henderson family
really want":

```json
{
  "client_name": "Hendersons",
  "search_started": "2025-09",
  "as_of": "2026-03-10",
  "must_haves": [
    {
      "preference": "4+ bedrooms",
      "established": "initial",
      "consistency": "firm",
      "context": "3 kids"
    },
    {
      "preference": "Yard for dogs",
      "established": "initial",
      "consistency": "firm",
      "client_quote": "we won't compromise on this"
    },
    {
      "preference": "School district X",
      "established": "2026-02-14",
      "consistency": "firm",
      "context": "Oldest starting middle school next fall; became hard constraint after a tour"
    },
    {
      "preference": "HOA fees ≤ $200/mo",
      "established": "2026-01-22",
      "consistency": "firm",
      "context": "Saw $480/mo HOA, was taken aback"
    }
  ],
  "nice_to_haves": [
    "updated kitchen",
    "home office",
    "south-facing yard"
  ],
  "deal_breakers": [
    "busy main road",
    "pool requiring maintenance",
    "significant deferred maintenance"
  ],
  "budget_history": [
    { "date": "2025-09", "amount": 650000 },
    { "date": "2025-11", "amount": 725000, "reason": "After a home they loved" },
    { "date": "2026-02-22", "amount": 785000, "reason": "Bank pre-approval increased after Mr. Henderson's promotion" }
  ],
  "recent_changes": [
    "Budget up $60K from October baseline",
    "School district added as must-have",
    "HOA cap added",
    "Yard requirement softened: 'we'd consider a smaller yard if there's a park very close'"
  ],
  "summary": "Strong, clear picture. 4 must-haves, 3 deal-breakers, current budget $785K. Recent changes worth knowing before next showing: budget up, school district must-have, yard preference softened."
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
