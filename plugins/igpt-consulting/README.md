# igpt-consulting

Consulting intelligence for independent consultants, boutique agencies, and
consulting firms. Turn the email already in your inbox into a live picture
of where every engagement actually stands — what's overdue, what's slipping
out of scope, where retainers are burning, who needs a follow-up.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Consulting runs on email. Every deliverable promised, every scope
discussion, every retainer conversation, every proposal follow-up lives in
threads that nobody consolidates until a client asks "where's that thing
you promised?"

A client asks for "one more thing" in a thread and you say yes — without
realizing it's the fourth unscoped addition this month. A proposal you
sent three weeks ago got no response and you forgot to follow up. A
retainer client is burning through their hours twice as fast as expected
but nobody flagged it because the pattern is only visible across multiple
threads. A happy client offered to be a reference six months ago and
nobody took them up on it.

This plugin gives you six focused workflows that mine your client email
and return structured answers about what's actually happening across your
practice.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What am I behind on across all my clients?"
>
> "Has Apex Digital been creeping out of scope?"
>
> "How is the Northstar retainer tracking this month?"
>
> "Which proposals have gone quiet?"
>
> "Who offered to be a reference and I never followed up?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized punch
list.

---

## A typical week

**Monday morning.** *"What am I behind on?"* The
`client-deliverable-tracker` skill returns every deliverable across every
client, sorted with overdue items first, items waiting on client input
next, and in-progress work last. You see Northstar's Q1 report is overdue
but blocked on their data — quick email to nudge them, three minutes.

**Wednesday before a client call.** *"What's the state of Apex
Digital?"* The agent runs `client-deliverable-tracker`,
`client-feedback-collector`, and `scope-creep-detector` for that one
client. You walk in knowing the open feedback items, recent sentiment,
and the two unscoped requests you've quietly absorbed.

**Friday retainer review.** *"How is the Apex retainer looking?"*
`retainer-usage-tracker` shows hours consumed, the renewal date, and
flags that they're burning faster than usual — a signal it's time for a
scope conversation, not just a renewal.

**End of month, pipeline review.** *"Which proposals are still
outstanding?"* `proposal-follow-up-tracker` ranks them by conversion
likelihood and flags the gone-quiet ones at the bottom.

---

## The skills

| Skill | When to use it |
|---|---|
| [`client-deliverable-tracker`](skills/client-deliverable-tracker/) | Every deliverable across every client — what's promised, delivered, overdue, awaiting feedback, blocked on client input |
| [`scope-creep-detector`](skills/scope-creep-detector/) | Out-of-scope requests accepted without a change order, grouped by client with severity |
| [`retainer-usage-tracker`](skills/retainer-usage-tracker/) | Retainer utilization, burn-rate signals, clients trending toward over- or under-using their hours |
| [`proposal-follow-up-tracker`](skills/proposal-follow-up-tracker/) | Outstanding proposals — status, days pending, interest signals, gone-quiet flags |
| [`client-feedback-collector`](skills/client-feedback-collector/) | Satisfaction signals, criticism, unactioned concerns; per-client overall sentiment |
| [`reference-request-miner`](skills/reference-request-miner/) | Reference / testimonial / case-study openings — both prospects asking and clients offering |

Each skill collects what it needs from you (time window, client to focus
on, etc.) and returns structured findings with evidence from the actual
email threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"walk me through the state of my
practice"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list (overdue items first, then anything
threatening renewal or satisfaction, then opportunities).

The agent is auto-discovered when the plugin is installed. You don't
invoke it explicitly — Claude routes broad consulting questions to it
automatically.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** what am i behind on?

**Claude:** *(running `client-deliverable-tracker` — scanning your client email for deliverable threads in the last 90 days)*

**2 deliverables need attention right now.**

**Overdue — Northstar Logistics: Q1 operational efficiency report**
9 days late. Blocked waiting on their warehouse throughput data.
*Next: nudge them for the data, or note the blocker before your next
check-in.*

**In revision — Apex Digital: Revised go-to-market strategy deck**
3 days late. 2 open feedback items:
- Reframe competitive section around pricing not features
- Add a slide on partner channel economics

*You're on the hook. Next: send revised draft or ETA.*

> *Want me to draft a status update email for either client?*

---

**You:** any scope creep at apex this quarter?

**Claude:** *(running `scope-creep-detector` — scanning Apex Digital threads for unscoped requests)*

**2 unaddressed scope creep instances at Apex Digital** — both accepted
without a change order.

**Pricing comparison against top 3 competitors** (Feb 18)
Not in original GTM scope. Accepted in thread:
> *"While you're working on the GTM deck, could you also pull together a
> pricing comparison against the top 3 competitors?"*

Recommended: raise a change order or document for the next renewal.

**Weekly check-ins expanded from 30 to 60 minutes** (Feb 25)
Confirmed in calendar invite without renegotiation.
Recommended: address at the next retainer review.

Two unscoped additions in a month suggests a scope conversation is
overdue.

> *Want me to draft a brief change-order note?*

---

**You:** which proposals have gone quiet?

**Claude:** *(running `proposal-follow-up-tracker` — scanning your prospecting threads from the last 6 months)*

**2 outstanding proposals — 1 high-conversion, 1 gone quiet.**

**Greenfield Partners — 6-month digital transformation advisory** ($72K)
Sent 23 days ago. Last contact 8 days ago. Two open questions still
unanswered:
- "Can we phase the engagement starting with a diagnostic?"
- "What does the offboarding look like if we pause after phase 1?"

These are *buying signals*, not objections. Conversion likelihood high if
you reply this week.

**Meridian Health — Compliance audit + remediation roadmap** ($35K)
Sent 41 days ago. Last contact 33 days ago. Initial interest, then
silence. Currently gone quiet.

> *Want me to draft a phasing-and-exit response for Greenfield, and a
> brief check-in for Meridian?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the consulting agent kicks in, running 4 skills in
parallel against your email through iGPT — deliverable tracker, scope
creep detector, retainer usage, proposal follow-up...)*

**This week, in priority order:**

**Critical (act today)**

1. **Northstar Logistics — Q1 report overdue 9 days**
   Blocked waiting on their warehouse data. Send a nudge today.

2. **Apex Digital — 2 unaddressed scope creep instances**
   Both accepted without a change order. Schedule a scope conversation.

**This week**

3. **Apex Digital retainer burning faster than usual**
   At 78% of monthly hours by week 3. Consider raising at the next 1:1.

4. **Greenfield Partners proposal — 23 days outstanding, high
   conversion**
   Two buying-signal questions still unanswered. Reply this week.

5. **Northstar offered to be a reference 4 months ago — never followed
   up**
   Strong fit for the Greenfield prospect. Consider asking now.

> *Where would you like to start? I can draft any of the emails or
> build a full Northstar client brief.*

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
2. **Find `igpt-consulting`.** In the iGPT marketplace, click into
   **igpt-consulting** to see the skills and the agent it includes.
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
   language — *"what am I behind on?"*, *"any scope creep at Apex?"* —
   and the right skill or the agent picks up automatically.

You do steps 1–4 once. After that, the plugin is always available and
your iGPT connection is remembered.

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter
`https://mcp.igpt.ai/` and complete the OAuth flow. The plugin's skills
trigger automatically based on what you ask.

### Claude Code

```
/plugin marketplace add igptai/skills
/plugin install igpt-consulting@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-consulting/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-consulting.md
└── skills/
    ├── client-deliverable-tracker/
    ├── client-feedback-collector/
    ├── proposal-follow-up-tracker/
    ├── reference-request-miner/
    ├── retainer-usage-tracker/
    └── scope-creep-detector/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, search query, ask prompt, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 90 days", "the last 3 months", "May 2024", "since the
kickoff" — all fine. You don't need to type ISO dates.

**Add deliverable or scope-creep categories.** Each skill's output schema
has enums (e.g. `deliverable_type`, `creep_type`) you can extend in the
SKILL.md to fit your practice — fractional leadership, code review,
workshop facilitation, out-of-hours support, whatever.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). The agent will auto-include it on the next session
once you add it to the agent's skill list.

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

**`client-deliverable-tracker`** — for "what am I behind on across all my
clients":

```json
{
  "deliverables": [
    {
      "client": "Northstar Logistics",
      "deliverable": "Q1 operational efficiency report",
      "deliverable_type": "report",
      "committed_on": "2026-02-10",
      "due_date": "2026-03-01",
      "status": "overdue",
      "days_overdue": 9,
      "open_feedback_items": [],
      "blocker": "Waiting on access to their warehouse throughput data",
      "we_are_waiting_on_client": true
    },
    {
      "client": "Apex Digital",
      "deliverable": "Revised go-to-market strategy deck",
      "deliverable_type": "presentation",
      "committed_on": "2026-02-25",
      "due_date": "2026-03-07",
      "status": "in_revision",
      "days_overdue": 3,
      "open_feedback_items": [
        "Reframe competitive section around pricing not features",
        "Add a slide on partner channel economics"
      ],
      "blocker": "",
      "we_are_waiting_on_client": false
    }
  ],
  "overdue_count": 1,
  "waiting_on_client_count": 1,
  "summary": "2 deliverables need attention. Northstar report is overdue but blocked on their data. Apex deck has 2 open revision requests."
}
```

**`scope-creep-detector`** — for "any scope creep at Apex this quarter":

```json
{
  "as_of": "2026-03-10",
  "scope_creep_instances": [
    {
      "client": "Apex Digital",
      "description": "Pricing comparison against top 3 competitors not in original GTM scope",
      "creep_type": "additional_deliverable",
      "date_requested": "2026-02-18",
      "accepted": true,
      "change_order_raised": false,
      "estimated_impact": "moderate",
      "evidence": "'While you're working on the GTM deck, could you also pull together a pricing comparison against the top 3 competitors?'",
      "recommended_action": "Raise a change order or document for the next renewal conversation"
    },
    {
      "client": "Apex Digital",
      "description": "Weekly check-ins expanded from 30 to 60 minutes without renegotiation",
      "creep_type": "extra_meeting",
      "date_requested": "2026-02-25",
      "accepted": true,
      "change_order_raised": false,
      "estimated_impact": "moderate",
      "recommended_action": "Address at the next retainer review — two unscoped additions suggest a scope conversation is overdue"
    }
  ],
  "by_client": [
    { "client": "Apex Digital", "instance_count": 2, "unaddressed_count": 2, "overall_severity": "moderate" }
  ],
  "total_unaddressed": 2,
  "summary": "2 unaddressed scope creep instances at Apex Digital. Both accepted without a change order — a scope conversation is recommended."
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
