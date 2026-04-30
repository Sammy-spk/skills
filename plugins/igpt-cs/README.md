# igpt-cs

Customer success intelligence for CSMs, account managers, and customer
success leaders. Turn the email already in your inbox into a live picture
of which accounts are at risk, what's escalating, who's ready to renew,
and where onboarding is stalling.

`5 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Customer success runs on email. Every churn signal, every escalation,
every renewal cue, every onboarding hiccup, every moment of customer joy
lives in threads scattered across dozens of accounts. Nobody consolidates
the picture until a customer churns and the team asks "did we see this
coming?"

A customer drops a competitor name in a thread and you don't notice. An
escalation simmers for two weeks before someone loops you in. A
renewal lands on your calendar but you haven't actually checked
sentiment. A new customer's onboarding stalls quietly because nobody
flagged that their integration questions never got answered. A happy
customer says something gold-quote-worthy and it never makes it into a
case study.

This plugin gives you five focused workflows that mine your customer
email and return structured answers about what's actually happening
across your book.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Which customers should I be worried about right now?"
>
> "Anything escalating I haven't seen?"
>
> "How's the renewal pipeline shaping up?"
>
> "Where is onboarding stuck for new customers?"
>
> "Any quotable wins this quarter for case studies?"
>
> "Walk me through the state of my book this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning.** *"Which customers are at risk?"* The
`churn-signal-detector` returns every account with churn signals across
the last 90 days — dissatisfaction language, competitor mentions,
reduced engagement, escalating frustration. You see Acme Corp dropped a
competitor name three times in the last two weeks; time for a save
call.

**Wednesday before a customer call.** *"What's the state of Acme
Corp?"* The agent runs `churn-signal-detector`, `escalation-tracker`,
and `renewal-readiness-checker` for that one account. You walk in
knowing the open escalation, the recent sentiment shift, and that
their renewal is 90 days out.

**Friday CS standup prep.** *"Any active escalations across my
accounts?"* `escalation-tracker` returns every active escalation — SLA
breaches, executive complaints, situations where a customer's language
shows they're past normal patience. Two of yours need exec attention
before Monday.

**End of quarter, advocacy review.** *"Any quotable success
moments?"* `success-story-miner` finds every customer who praised the
product or reported a result, ranked by case-study fit. Three solid
testimonial quotes you can run by Marketing.

---

## The skills

| Skill | When to use it |
|---|---|
| [`churn-signal-detector`](skills/churn-signal-detector/) | Early warning signals across accounts — dissatisfaction language, competitor mentions, declining engagement |
| [`escalation-tracker`](skills/escalation-tracker/) | Active escalations, SLA breaches, executive complaints, unresolved issues with growing severity |
| [`onboarding-gaps-detector`](skills/onboarding-gaps-detector/) | Stalls and gaps in new-customer onboarding journeys; systemic onboarding issues |
| [`renewal-readiness-checker`](skills/renewal-readiness-checker/) | Renewal sentiment, engagement, open issues that could affect renewal, likely-to-renew vs. at-risk |
| [`success-story-miner`](skills/success-story-miner/) | Customer satisfaction moments, testimonial-worthy quotes, proof-point opportunities |

Each skill collects what it needs from you (time window, account to
focus on, etc.) and returns structured findings with evidence from the
actual email threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"walk me through the state of my
book"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — escalations and churn risk first, then
upcoming renewals at risk, then opportunities for advocacy.

The agent is auto-discovered when the plugin is installed. You don't
invoke it explicitly — Claude routes broad CS questions to it
automatically.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** which customers are at risk right now?

**Claude:** *(running `churn-signal-detector` — scanning your customer email from the last 90 days for dissatisfaction, competitor mentions, and disengagement)*

**3 accounts have churn signals worth attention.**

**High risk — Acme Corp**
3 mentions of "Vendor X" (your top competitor) in the last 14 days.
Engagement down: response times have doubled, two pricing-comparison
questions raised. Last contact 9 days ago.
*Recommended: schedule a save call this week. Bring competitive
positioning and a roadmap angle.*

**Moderate risk — Northstar Logistics**
Two unresolved support escalations from last month surfaced again.
Language shift: phrases like "we're considering options" and "this
shouldn't be this hard" in the most recent thread.
*Recommended: reach out from a senior CSM or AE; address the
escalations explicitly.*

**Watch — Greenfield Partners**
Reduced engagement: gone from weekly check-ins to biweekly without
explanation. No explicit dissatisfaction signals, but the pattern is
worth noting.
*Recommended: a check-in email this week to re-establish cadence.*

> *Want me to draft a save-call agenda for Acme or a check-in for
> Greenfield?*

---

**You:** anything escalating i haven't seen?

**Claude:** *(running `escalation-tracker` — scanning for active escalations, SLA breaches, and executive involvement in the last 60 days)*

**2 active escalations need attention.**

**Acme Corp — production outage handling, escalated to CTO** (Feb 14)
Open 24 days. Originally a P2 ticket; escalated to P1 after a second
outage. CTO looped in last week. Most recent email from their VP
Engineering: *"We need a clear plan and timeline by EOW."*
*Status: active. Owner on our side: Sarah (Sr CSM). Next step is a
formal incident review committed to by Friday.*

**Northstar Logistics — billing dispute** (Feb 28)
Open 10 days. Customer disputes a $14K usage overage; claims the
metering was misconfigured during onboarding. Finance is looped in.
*Status: under review. Owner: Marcus (Account Manager). Next step is
metering audit, due Tuesday.*

> *Want me to draft a status update to the Acme CTO or build a brief
> for the Northstar billing call?*

---

**You:** how's the renewal pipeline looking?

**Claude:** *(running `renewal-readiness-checker` — scanning customer threads from the last 180 days for renewal sentiment, engagement, and open issues)*

**5 renewals in the next 90 days. 2 strong, 2 at risk, 1 unknown.**

**Strong — Apex Digital** (renews Apr 12)
Renewal language already in recent threads ("looking forward to year
two"). Engagement is high; no open issues; CSM relationship is warm.
*No action needed beyond standard renewal motion.*

**Strong — Meridian Health** (renews Apr 28)
Three case-study-worthy quotes in the last quarter; product-led
expansion happening organically. Renewal conversation has not started
formally but signals are unambiguous.
*Action: open the renewal conversation early; size up for expansion.*

**At risk — Acme Corp** (renews May 1)
Active escalation (see above), competitor mentions, declining
engagement. Save play needed before renewal motion.
*Action: tie save plan to renewal — don't open the renewal conversation
until churn signals are addressed.*

**At risk — Northstar Logistics** (renews May 22)
Open billing dispute, two unresolved escalations from last month.
*Action: clear the air on disputes before renewal; consider sizing
adjustment.*

**Unknown — Greenfield Partners** (renews Jun 4)
Sentiment is flat; not negative, not positive. No churn signals, no
expansion signals.
*Action: schedule a discovery call to understand current value
realization and roadmap fit.*

> *Want me to draft renewal-conversation starters for the strong
> renewals or save plans for the at-risk ones?*

---

**You:** walk me through the state of my book this week

**Claude:** *(the customer success agent kicks in, running 4 skills in
parallel against your email through iGPT — churn signals, escalations,
renewal readiness, onboarding gaps...)*

**This week, in priority order:**

**Critical (act today)**

1. **Acme Corp — save play needed** (churn + escalation + renewal)
   3 competitor mentions, active CTO-level escalation, May 1 renewal.
   This is the top priority of the week.

2. **Northstar Logistics — clear escalations before renewal**
   Two open issues (support + billing), May 22 renewal. Don't open the
   renewal conversation until these are resolved.

**This week**

3. **Bluefield Co — onboarding stalled at week 4**
   Integration questions unanswered for 8 days; new-customer momentum
   slipping. CSM should re-engage.

4. **Greenfield Partners — engagement cooling**
   Cadence dropped from weekly to biweekly with no explanation. Renewal
   in 90 days. Reach out for a discovery call.

**Opportunity**

5. **Meridian Health — strong renewal + expansion signal**
   Three case-study-worthy quotes, organic product-led expansion. Open
   the renewal conversation early and size up.

> *Where would you like to start? I can draft any of these emails or
> build a full Acme save plan.*

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
2. **Find `igpt-cs`.** In the iGPT marketplace, click into **igpt-cs**
   to see the skills and the agent it includes.
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
   language — *"which customers are at risk?"*, *"any escalations
   I haven't seen?"* — and the right skill or the agent picks up
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
/plugin install igpt-cs@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-cs/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-cs.md
└── skills/
    ├── churn-signal-detector/
    ├── escalation-tracker/
    ├── onboarding-gaps-detector/
    ├── renewal-readiness-checker/
    └── success-story-miner/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 90 days", "the last quarter", "May 2024", "since the QBR" —
all fine. You don't need to type ISO dates.

**Add categories or signal types.** Each skill's output schema has
enums (e.g. churn signal types, escalation types) you can extend in the
SKILL.md to fit your CS playbook — green/yellow/red taxonomies,
industry-specific risk patterns, save-play categories, whatever your
team already uses.

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

**`churn-signal-detector`** — for "which customers are at risk":

```json
{
  "as_of": "2026-03-10",
  "accounts_at_risk": [
    {
      "account": "Acme Corp",
      "risk_level": "high",
      "primary_signals": ["competitor_mentions", "engagement_decline"],
      "competitor_mentions": ["Vendor X", "Vendor X", "Vendor X"],
      "engagement_trend": "declining",
      "days_since_last_contact": 9,
      "evidence": "3 mentions of Vendor X in 14 days; pricing-comparison questions raised; response times doubled",
      "recommended_action": "Schedule a save call this week with competitive positioning and roadmap angle"
    },
    {
      "account": "Northstar Logistics",
      "risk_level": "moderate",
      "primary_signals": ["unresolved_escalation", "language_shift"],
      "language_shift_quotes": ["we're considering options", "this shouldn't be this hard"],
      "evidence": "Two unresolved support escalations resurfaced; sentiment language shifted negative",
      "recommended_action": "Reach out from a senior CSM or AE; address escalations explicitly"
    }
  ],
  "high_risk_count": 1,
  "moderate_risk_count": 1,
  "watch_count": 1,
  "summary": "3 accounts have churn signals — 1 high (Acme), 1 moderate (Northstar), 1 watch (Greenfield)."
}
```

**`escalation-tracker`** — for "anything escalating I haven't seen":

```json
{
  "as_of": "2026-03-10",
  "active_escalations": [
    {
      "account": "Acme Corp",
      "issue_summary": "Production outage handling, escalated to CTO",
      "escalation_type": "executive_involvement",
      "first_raised": "2026-02-14",
      "days_open": 24,
      "current_severity": "P1",
      "owner_internal": "Sarah (Sr CSM)",
      "customer_contacts": ["VP Engineering", "CTO"],
      "most_recent_quote": "We need a clear plan and timeline by EOW.",
      "next_step": "Formal incident review committed for Friday",
      "status": "active"
    },
    {
      "account": "Northstar Logistics",
      "issue_summary": "Billing dispute over $14K usage overage",
      "escalation_type": "billing_dispute",
      "first_raised": "2026-02-28",
      "days_open": 10,
      "current_severity": "moderate",
      "owner_internal": "Marcus (Account Manager)",
      "customer_contacts": ["Finance"],
      "next_step": "Metering audit due Tuesday",
      "status": "under_review"
    }
  ],
  "total_active": 2,
  "total_executive_involvement": 1,
  "summary": "2 active escalations. Acme is P1 with CTO involvement, 24 days open. Northstar is a billing dispute, 10 days open, under review."
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
