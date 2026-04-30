# igpt-finance

Finance intelligence for finance teams, controllers, bookkeepers, and
anyone managing their own books. Turn the receipts, invoices, and
billing emails already in your inbox into structured reports — expenses
by project, invoices to reconcile, subscriptions you forgot you had,
vendor spend totals, tax documents in one place.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

A surprising amount of finance work is actually email forensics.
Receipts arrive as PDFs in your inbox. Invoices show up scattered
across vendors and currencies. Subscription renewals confirm silently.
Payments get acknowledged in threads nobody consolidates. Tax
documents drift in across the year and you go hunting for them in
April.

A controller closing the books at month end is mostly chasing emails.
A consultant building a project expense report is mostly searching for
receipts. A founder doing personal taxes is mostly trying to remember
which SaaS subscriptions counted as business expenses.

This plugin gives you six focused workflows that mine your billing
email and return structured answers — totals you can hand to your
accountant, lists you can paste into a spreadsheet, reports you can
drop into a board update.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Build me an expense report for May, in USD."
>
> "What invoices are overdue from the last 90 days?"
>
> "What subscriptions am I paying for that I don't use?"
>
> "Pull together all my tax documents for 2024, US."
>
> "Where did the money go last quarter? Total by vendor."
>
> "Help me close the books for last month."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a consolidated view
of the month's financial activity.

---

## A typical week

**Monday morning.** *"What's overdue?"* The `payment-status-tracker`
returns every invoice without a payment confirmation, flagging anything
past due. You see two receivables overdue 30+ days; quick AR follow-up
emails go out before lunch.

**Mid-week, vendor review.** *"What did we spend with each vendor last
quarter?"* `vendor-spend-analyzer` returns vendors ranked by total
spend, in your local currency. You spot two vendors you'd assumed were
small but actually account for 8% of opex — worth a closer look.

**End of month, close the books.** *"Help me close the books for
February."* The agent runs `expense-report-builder`,
`invoice-reconciliation`, `payment-status-tracker`, and
`subscription-tracker` in parallel. You hand the consolidated output to
your bookkeeper instead of re-deriving it from threads.

**Pre-tax filing.** *"All my tax documents for 2024, US."*
`tax-document-collector` returns every tax-relevant document found in
email — VAT invoices, 1099s, official receipts — in one structured
list to hand to your accountant.

---

## The skills

| Skill | When to use it |
|---|---|
| [`expense-report-builder`](skills/expense-report-builder/) | Receipts and purchase confirmations over a period; supports grouping by project or client; converts to your local currency |
| [`invoice-reconciliation`](skills/invoice-reconciliation/) | Incoming invoices in a period, normalized to your local currency |
| [`payment-status-tracker`](skills/payment-status-tracker/) | Match invoices against payment confirmations; flag overdue payables and receivables |
| [`subscription-tracker`](skills/subscription-tracker/) | Recurring subscriptions and SaaS billing across a 13-month window; flags cancelled or stalled ones |
| [`tax-document-collector`](skills/tax-document-collector/) | Tax-relevant documents (VAT invoices, 1099s, official receipts) for a tax year and jurisdiction |
| [`vendor-spend-analyzer`](skills/vendor-spend-analyzer/) | Total spend per vendor over a period, ranked, in your local currency |

Each skill collects what it needs from you (time window, currency,
project scope, etc.) and returns structured findings with evidence from
the actual email threads. A few skills require values with no sensible
default — currency, tax year, tax jurisdiction — and will ask before
running.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"close
the books for last month"* or *"where do I stand financially this
quarter"*. The agent picks the right skills, runs them in parallel, and
produces a consolidated view.

The agent is auto-discovered when the plugin is installed. You don't
invoke it explicitly — Claude routes broad finance questions to it
automatically.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** build me an expense report for may, grouped by project

**Claude:**
Quick question before I run — what currency would you like totals in?
(USD, EUR, ILS, GBP — common choices, but anything works.)

**You:** USD

**Claude:** *(running `expense-report-builder` — scanning May 2026 receipts and purchase confirmations, converting all amounts to USD)*

**May 2026 expense report — 12 expenses, $4,287.42 total in USD.**

**Project Apex** — $1,902.10
- AWS infrastructure (May 3) — $1,240.00
- Adobe Creative Cloud (May 7) — $54.99
- Notion team plan (May 12) — $96.00
- Conference travel — Acme Summit (May 19) — $511.11

**Project Northstar** — $1,615.20
- Figma team plan (May 1) — $144.00
- Linear plus seats (May 4) — $80.00
- Designer freelance — Atlas Studio (May 22) — $1,250.00 (€1,148 → USD)
- Stock photos (May 28) — $141.20

**Unassigned / general** — $770.12
- Slack billing (May 1) — $96.00
- Stripe processing fees (May 31) — $487.40
- Domain renewal — gandi.net (May 16) — $43.20
- 1Password family plan (May 19) — $143.52

**Currency note:** 1 expense (Atlas Studio, €1,148) converted at the
mid-month FX rate. Original amount preserved in the source row.

> *Want me to break this out as a CSV, draft a reimbursement request,
> or run the same report for April for comparison?*

---

**You:** what invoices are overdue?

**Claude:** *(running `payment-status-tracker` — matching invoices against payment confirmations across the last 90 days)*

**3 receivables overdue + 1 payable approaching due date.**

**Receivables (you're owed)**

**Acme Corp — $14,500** (due Feb 15, 23 days overdue)
Invoice #2026-014 sent Feb 1. No payment confirmation in email.
Most recent contact: AP team confirmed receipt on Feb 18, said
"working on it". No follow-up since.
*Recommended: friendly reminder email today.*

**Northstar Logistics — $6,250** (due Feb 28, 10 days overdue)
Invoice #2026-018 sent Feb 14. No payment confirmation, no AP
acknowledgement.
*Recommended: confirm receipt was processed; resend if no record.*

**Greenfield Partners — $3,400** (due Feb 22, 16 days overdue)
Invoice #2026-016 sent Feb 8. AP confirmed receipt; said payment was
"queued for next run".
*Recommended: gentle nudge; their next AP run was the 1st.*

**Payables (you owe)**

**Marina Hosting — $890** (due Mar 12, 2 days out)
Invoice #MH-3344 received Feb 27. Not yet paid based on email.
*Recommended: process this week.*

> *Want me to draft AR reminder emails for the 3 overdue receivables?*

---

**You:** what subscriptions am i paying for?

**Claude:** *(running `subscription-tracker` — scanning the last 13 months for recurring billing emails to catch monthly and annual subscriptions)*

**18 active subscriptions — total annualized $7,824.**

**Tools the team uses (12 subs — $5,940 / yr)**

| Subscription | Frequency | Last charge | Annualized |
|---|---|---|---|
| AWS | monthly | Mar 3 | $14,880 |
| Notion (team plan) | monthly | Mar 1 | $1,152 |
| Slack | monthly | Mar 1 | $1,152 |
| Linear | monthly | Mar 4 | $960 |
| Figma | monthly | Mar 1 | $1,728 |
| 1Password (family) | annual | Apr 1 (next) | $144 |
| GitHub team | monthly | Mar 1 | $432 |
| Adobe Creative Cloud | monthly | Mar 7 | $660 |
| Vercel Pro | monthly | Mar 9 | $240 |
| Sentry | monthly | Mar 4 | $312 |
| PagerDuty | monthly | Mar 1 | $588 |
| Loom team | monthly | Mar 5 | $156 |

**Unclear if still in use (3 subs — $384 / yr)**
- **Calendly Premium** — last meaningful usage signal in email was 8
  months ago. Still being charged $144/yr.
- **Pluralsight** — billed $144/yr. No "shared a course" or
  invitation emails in the last 9 months.
- **Stock photos service** — recurring $96/yr. Last download
  notification was 11 months ago.

**Stopped renewing (3 subs — saved $1,500 / yr)**
- Old SEO tool — last charge Aug 2025, no resumed billing
- A defunct task tracker — cancelled Oct 2025
- Marketing automation trial — never converted

> *Want me to draft cancellation emails for the 3 "unclear" subs, or
> dig into any specific renewal?*

---

**You:** help me close the books for february

**Claude:** *(the finance agent kicks in, running 4 skills in parallel
against your email through iGPT — expense report, invoice
reconciliation, payment status, subscription tracking...)*

**February 2026 close — consolidated view.**

**Inflows** (revenue invoiced)
- 9 invoices sent, $48,200 total
- 6 paid, 3 outstanding ($24,150)
- See payment-status-tracker for the overdue list

**Outflows** (vendors paid + payables)
- Confirmed paid: $19,840 across 14 vendors
- Open payables: 1 ($890 to Marina Hosting, due Mar 12)
- Subscription charges this month: $987 across 12 services

**Reimbursable expenses** (project-tagged)
- Project Apex: $1,902.10
- Project Northstar: $1,615.20
- Unassigned / general: $770.12

**Anomalies worth a look**
1. **AWS bill up 19% month-over-month** — usually steady; investigate
   for unexpected resource usage.
2. **Stripe fees up vs. revenue** — fees ratio crept from 2.1% to
   2.7%; check if a new payment method came online with worse rates.
3. **Adobe billed twice** in February (Mar 5 and Mar 7) — looks like a
   plan switch but worth confirming.

> *Want me to export the consolidated close as CSV, draft AR follow-ups
> for the 3 overdue invoices, or dig into the AWS spend bump?*

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
2. **Find `igpt-finance`.** In the iGPT marketplace, click into
   **igpt-finance** to see the skills and the agent it includes.
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
   language — *"build me an expense report for May in USD"*, *"what
   invoices are overdue?"* — and the right skill or the agent picks up
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
/plugin install igpt-finance@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-finance/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-finance.md
└── skills/
    ├── expense-report-builder/
    ├── invoice-reconciliation/
    ├── payment-status-tracker/
    ├── subscription-tracker/
    ├── tax-document-collector/
    └── vendor-spend-analyzer/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last month", "the month of May", "Q1 2026", "fiscal year 2024",
"since Jan 1" — all fine. You don't need to type ISO dates.

**Currency and tax jurisdiction are required for some skills.**
Expense reports, invoice reconciliation, vendor-spend analysis, and tax
document collection all need either your local currency or your tax
jurisdiction with no default — these are values where guessing would
be wrong half the time. The skills will ask before running.

**Add categories or expense types.** Each skill's output schema has
enums you can extend in the SKILL.md to fit your chart of accounts —
project codes, expense categories, tax-document types specific to your
jurisdiction, vendor classifications.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Add it to the agent's "Available skills"
list so the agent knows about it.

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

**`expense-report-builder`** — for "build me an expense report for May
in USD":

```json
{
  "period_from": "2026-05-01",
  "period_to": "2026-05-31",
  "local_currency": "USD",
  "grouping": "project",
  "expenses": [
    {
      "vendor": "AWS",
      "amount": 1240.00,
      "currency": "USD",
      "amount_local_currency": 1240.00,
      "date": "2026-05-03",
      "category": "infrastructure",
      "project": "Project Apex"
    },
    {
      "vendor": "Atlas Studio",
      "amount": 1148.00,
      "currency": "EUR",
      "amount_local_currency": 1250.00,
      "fx_rate_used": 1.0889,
      "date": "2026-05-22",
      "category": "freelance",
      "project": "Project Northstar"
    }
  ],
  "total_local_currency": 4287.42,
  "by_project": [
    { "project": "Project Apex", "total": 1902.10, "count": 4 },
    { "project": "Project Northstar", "total": 1615.20, "count": 4 },
    { "project": "Unassigned / general", "total": 770.12, "count": 4 }
  ],
  "currency_conversion_count": 1,
  "summary": "12 expenses totaling $4,287.42 USD across 3 project groupings; 1 expense converted from EUR at mid-month rate."
}
```

**`payment-status-tracker`** — for "what invoices are overdue":

```json
{
  "as_of": "2026-03-10",
  "direction_scope": "both",
  "receivables": [
    {
      "counterparty": "Acme Corp",
      "invoice_number": "2026-014",
      "amount": 14500.00,
      "currency": "USD",
      "invoice_date": "2026-02-01",
      "due_date": "2026-02-15",
      "days_overdue": 23,
      "status": "outstanding",
      "last_communication_date": "2026-02-18",
      "last_communication_summary": "AP team confirmed receipt and said 'working on it'; no follow-up since",
      "recommended_action": "Friendly reminder email"
    }
  ],
  "payables": [
    {
      "counterparty": "Marina Hosting",
      "invoice_number": "MH-3344",
      "amount": 890.00,
      "currency": "USD",
      "invoice_date": "2026-02-27",
      "due_date": "2026-03-12",
      "days_overdue": 0,
      "status": "outstanding_due_soon",
      "recommended_action": "Process this week"
    }
  ],
  "overdue_receivables_count": 3,
  "overdue_receivables_total": 24150.00,
  "outstanding_payables_count": 1,
  "summary": "3 receivables overdue ($24,150 total); 1 payable due Mar 12."
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
