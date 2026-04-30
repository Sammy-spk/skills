# igpt-executive

Executive intelligence for founders, CEOs, and senior leaders. Turn the
email already in your inbox into a live picture of what matters at the
executive level — board updates, fundraising pipeline, investor
relationships, strategic commitments, key relationships, and emerging
risks.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Running a company is partly about keeping a lot of important threads in
your head at once — a board meeting that's three weeks out, a fundraise
mid-flight, six investors at six different stages, the customer
concentration risk you've been quietly aware of, the head of engineering
who hasn't said anything but has stopped being on the all-hands
recordings, the commitment you made to Beacon Partners last quarter
that's quietly slipping.

Most of that lives in email. None of it gets consolidated until the
board meeting agenda goes out, the term sheet lands, or something
breaks. By then the picture you needed was three weeks ago.

This plugin gives you six focused workflows that mine your executive
email and return structured answers about what is actually happening
across the things you're paying attention to as a leader.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What should I bring to next week's board meeting?"
>
> "Where do I stand with each investor?"
>
> "Anything I should be worried about right now?"
>
> "What commitments have I made that are still open?"
>
> "How healthy are my key external relationships?"
>
> "Walk me through the top things on my plate this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning.** *"What should I be worried about?"* The
`crisis-signal-detector` returns early-warning signals across the last
60 days — financial pressure, key-person flight risk, regulatory
inquiries, customer concentration. You see one of your top customers
mentioned slowing growth in a recent thread; quiet signal worth a
direct check-in.

**Wednesday before a 1:1 with the board chair.** *"What's the state
of the fundraise?"* `fundraising-thread-tracker` returns where each
investor is in the conversation, last contact, what was last discussed,
who owns the next step. You walk into the call knowing the pipeline
without re-reading 40 threads.

**Friday before the board prep deadline.** *"Pull together the
board update raw material."* `board-update-builder` extracts wins,
decisions, risks, hires, financial signals, and open asks from the
last 30 days of email — the skeleton you'll edit into the deck.

**End of quarter, commitment audit.** *"What commitments are still
open?"* `strategic-commitment-log` returns every revenue target,
milestone, hire, and strategic promise you made to investors or board
members — with evidence of delivery or what remains open.

---

## The skills

| Skill | When to use it |
|---|---|
| [`board-update-builder`](skills/board-update-builder/) | Raw material for a board update — wins, decisions, risks, hires, financial signals, open asks |
| [`crisis-signal-detector`](skills/crisis-signal-detector/) | Early warning signals — legal threats, financial pressure, key-person flight risk, regulatory inquiries |
| [`fundraising-thread-tracker`](skills/fundraising-thread-tracker/) | Investor pipeline — stage, last contact, next step, signals of interest or pulling back |
| [`investor-relationship-tracker`](skills/investor-relationship-tracker/) | Health of relationships with existing investors — tone, open asks, warm vs. cool |
| [`key-relationship-health`](skills/key-relationship-health/) | Health of external relationships — key customers, advisors, partners, senior contacts |
| [`strategic-commitment-log`](skills/strategic-commitment-log/) | Commitments made to investors, board, partners — what was promised, evidence of delivery, what remains open |

Each skill collects what it needs from you (time window, scope, etc.)
and returns structured findings with evidence from the actual email
threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what's
most important this week"* or *"walk me through what's on my plate"*.
The agent picks the right skills, runs them in parallel, and synthesizes
a prioritized list — crisis signals and overdue commitments first, then
capital-stage items, then relationships needing attention.

The agent is auto-discovered when the plugin is installed. You don't
invoke it explicitly — Claude routes broad executive questions to it
automatically.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** what should i bring to next week's board meeting?

**Claude:** *(running `board-update-builder` — extracting milestones, decisions, risks, hires, and asks from the last 30 days of executive email)*

**Board update raw material — last 30 days.**

**Wins**
- ARR milestone hit ($14M ARR, 22 days ahead of plan)
- Acme Corp expansion landed (3-year, $2.1M ACV, replaces incumbent)
- Two senior hires accepted: VP Marketing (start Mar 24), Head of
  Customer Success (start Apr 7)

**Decisions made**
- Pricing tier consolidation approved (effective May 1)
- Decision to pause EMEA expansion until Q3 (capital allocation)
- Move from quarterly to monthly board updates (committed last meeting,
  this is the first one)

**Risks emerged**
- Customer concentration: top 3 customers = 41% of ARR (up from 36%)
- Regulatory: SOC 2 Type II audit findings pushed remediation 3 weeks
- Key-person: Head of Engineering signaled wanting to "talk through
  career path" — context for retention conversation

**Open asks for the board**
- Approval for $4M opex bump tied to expansion plan
- Intros requested: 2 enterprise prospects in financial services
- Confirmation on Q2 hiring plan (8 roles)

> *Want me to draft the actual board update deck section by section, or
> do a deeper dive on the customer concentration risk?*

---

**You:** where do i stand with investors?

**Claude:** *(running `fundraising-thread-tracker` — scanning fundraising and investor outreach threads from the last 6 months)*

**3 active investor conversations + 2 cooling.**

**Active — Beacon Partners** (potential lead)
Stage: term sheet drafted. Last contact 4 days ago. Most recent
discussion was around board composition and pro-rata rights.
Signals: high interest, moving fast.
*Next: their committee meeting is Tuesday. You committed to send the
updated cap table by Monday EOD.*

**Active — Constellation Capital** (potential follow-on lead)
Stage: deep diligence. Last contact 2 days ago. Working through
customer references and unit economics.
Signals: engaged but slower; second partner now involved.
*Next: customer reference call with Acme is scheduled Friday.*

**Active — Marina Ventures** (potential participant)
Stage: post-pitch, evaluating. Last contact 9 days ago. They asked for
the 3-year financial model.
Signals: moderate interest; haven't seen tone shift either way.
*Next: send model + follow up on their specific questions about ARR
quality.*

**Cooling — Lighthouse Ventures**
Last contact 26 days ago after initial enthusiasm. No explicit no, no
clear next step. Likely needs a direct close-the-loop conversation.

**Cooling — Pinnacle Partners**
Two intro emails sent, no substantive response in 6 weeks. Treat as a
soft no unless they reactivate.

> *Want me to draft the cap-table cover note for Beacon, or build a
> diligence brief for Constellation's customer reference call?*

---

**You:** anything i should be worried about right now?

**Claude:** *(running `crisis-signal-detector` — scanning the last 60 days for legal, financial, regulatory, key-person, and reputational signals)*

**3 signals worth your attention.** None are crises yet — but each is
the kind of thing you want to be aware of, not surprised by.

**Customer concentration / top-account risk** (moderate)
Top-3 concentration moved from 36% to 41% of ARR in the last quarter.
In a recent thread, the top customer's CFO mentioned reviewing all
software vendors as part of a cost-rationalization initiative. No
signal of intent to leave — but the language is worth a direct
check-in.

**Key-person — Head of Engineering** (moderate)
Two signals in the last 30 days: declined a panel invitation citing
"thinking through next steps", and a "career path conversation"
request. No external job-search signals visible in email, but
combined this is worth proactive engagement.

**Regulatory — SOC 2 Type II remediation** (low, but watch)
Auditor pushed remediation deadline 3 weeks; a customer email last
week asked about your SOC 2 status as part of vendor review. Not a
blocker yet but it could become one if remediation slips again.

> *Want me to brief you for the customer CFO conversation, prep a
> retention 1:1 outline for the Head of Engineering, or both?*

---

**You:** walk me through the top things on my plate this week

**Claude:** *(the executive agent kicks in, running 4 skills in
parallel against your email through iGPT — crisis signals, fundraising
pipeline, strategic commitments, key relationship health...)*

**This week, in priority order:**

**Critical (this week)**

1. **Beacon Partners — cap table due Monday EOD**
   You committed to it; their committee meets Tuesday. Top of the list.

2. **Top-customer CFO conversation**
   Vendor cost-rationalization signal. Direct check-in this week before
   it becomes a renewal problem.

3. **Head of Engineering retention 1:1**
   Career path conversation requested. Don't let this slip past this
   week.

**This week**

4. **Constellation Capital reference call Friday**
   Acme reference scheduled. Brief the customer on what to emphasize.

5. **Board update raw material assembled**
   Generated above. Edit into deck before Wednesday's draft review.

**Watch**

6. **Marina Ventures — financial model owed**
   No urgent deadline but the conversation goes cold without it.

7. **SOC 2 remediation status**
   Customer asked last week. If remediation slips again, this becomes
   front-and-center.

> *Where would you like to start? I can draft the Beacon cover note,
> the Acme reference brief, or the Head of Engineering retention
> outline.*

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
2. **Find `igpt-executive`.** In the iGPT marketplace, click into
   **igpt-executive** to see the skills and the agent it includes.
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
   language — *"what should I bring to next week's board meeting?"*,
   *"where do I stand with investors?"* — and the right skill or the
   agent picks up automatically.

You do steps 1–4 once. After that, the plugin is always available and
your iGPT connection is remembered.

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter
`https://mcp.igpt.ai/` and complete the OAuth flow. The plugin's skills
trigger automatically based on what you ask.

### Claude Code

```
/plugin marketplace add igptai/skills
/plugin install igpt-executive@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-executive/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-executive.md
└── skills/
    ├── board-update-builder/
    ├── crisis-signal-detector/
    ├── fundraising-thread-tracker/
    ├── investor-relationship-tracker/
    ├── key-relationship-health/
    └── strategic-commitment-log/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 30 days", "since the last board meeting", "May 2024",
"since the round opened" — all fine. You don't need to type ISO dates.

**Add commitment, signal, or relationship categories.** Each skill's
output schema has enums you can extend in the SKILL.md to fit how your
company tracks things — board update sections specific to your industry,
crisis signal types specific to your risk register, commitment
categories tied to your OKRs, whatever your team already uses.

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

**`board-update-builder`** — for "what should I bring to next week's
board meeting":

```json
{
  "period_from": "2026-02-08",
  "period_to": "2026-03-10",
  "wins": [
    {
      "category": "metrics",
      "summary": "ARR milestone hit ($14M ARR, 22 days ahead of plan)",
      "evidence_count": 3
    },
    {
      "category": "customers",
      "summary": "Acme Corp expansion landed: 3-year, $2.1M ACV, replaces incumbent",
      "evidence_count": 4
    },
    {
      "category": "hires",
      "summary": "Two senior hires accepted: VP Marketing (Mar 24 start), Head of CS (Apr 7 start)",
      "evidence_count": 2
    }
  ],
  "decisions": [
    {
      "summary": "Pricing tier consolidation approved (effective May 1)",
      "decided_on": "2026-02-19",
      "decision_type": "operational"
    },
    {
      "summary": "Pause EMEA expansion until Q3 (capital allocation)",
      "decided_on": "2026-02-26",
      "decision_type": "strategic"
    }
  ],
  "risks": [
    {
      "category": "customer_concentration",
      "summary": "Top-3 customers = 41% of ARR (up from 36%)",
      "severity": "moderate"
    },
    {
      "category": "key_person",
      "summary": "Head of Engineering signaled career path conversation needed",
      "severity": "moderate"
    },
    {
      "category": "regulatory",
      "summary": "SOC 2 Type II remediation pushed 3 weeks",
      "severity": "low"
    }
  ],
  "open_asks": [
    "Approval for $4M opex bump tied to expansion plan",
    "Intros: 2 enterprise prospects in financial services",
    "Confirmation on Q2 hiring plan (8 roles)"
  ],
  "summary": "Strong period: ARR milestone, marquee expansion, 2 senior hires. Watch: customer concentration up to 41%; key-person and regulatory signals worth tracking."
}
```

**`crisis-signal-detector`** — for "anything I should be worried about
right now":

```json
{
  "as_of": "2026-03-10",
  "signals": [
    {
      "category": "customer_concentration",
      "severity": "moderate",
      "summary": "Top customer mentioned vendor cost-rationalization initiative",
      "evidence": "CFO email referenced 'reviewing all software vendors' as part of cost initiative",
      "people_involved": ["Top customer CFO"],
      "urgency": "this_week",
      "recommended_action": "Direct check-in before this becomes a renewal conversation"
    },
    {
      "category": "key_person",
      "severity": "moderate",
      "summary": "Head of Engineering retention signal",
      "evidence": "Declined panel invitation citing 'next steps thinking'; requested career path conversation",
      "people_involved": ["Head of Engineering"],
      "urgency": "this_week",
      "recommended_action": "Proactive 1:1 with retention framing"
    },
    {
      "category": "regulatory",
      "severity": "low",
      "summary": "SOC 2 Type II remediation slipping; customer asked about status",
      "evidence": "Auditor pushed remediation 3 weeks; customer email last week asked about SOC 2",
      "urgency": "monitor",
      "recommended_action": "Ensure remediation owner has firm timeline"
    }
  ],
  "moderate_count": 2,
  "low_count": 1,
  "high_count": 0,
  "summary": "3 signals worth attention — none yet crises. Customer concentration and key-person retention are this-week priorities; SOC 2 is a monitor."
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
