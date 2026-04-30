# igpt-sales

Sales intelligence for account executives, sales leaders, and BDRs
working active deals. Turn the email already in your inbox into a
live picture of pipeline hygiene, deal friction, follow-ups owed,
expansion signals, competitor mentions, and meeting prep ready when
you need it.

`7 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Selling runs on email — the parts that don't live in the CRM. Open
items get committed to in long threads and nobody reconstructs them
into a "what do we still owe Acme" view until the renewal call.
Friction on a deal shows up first as small language shifts in
emails — *"we'll need to align with finance"*, *"can we revisit
this next week"* — that don't make it onto a stage update. Follow-
ups slip past silence thresholds because no one is auditing every
thread for who owes what. A prospect drops a competitor name in a
side comment and nobody remembers it during the next call. A
discovery question matches a problem we solved 18 months ago for
another customer, and nobody finds the proof point in time.

This plugin gives you seven focused workflows that mine your sales
email and return structured answers about pipeline status, friction
signals, follow-ups, expansion, competitors, and pre-meeting
context.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Who's waiting on a reply from me?"
>
> "What's friction-y on the Acme deal?"
>
> "Brief me on Maria Chen at Northstar Logistics for tomorrow's call."
>
> "Have we solved a problem like this before?"
>
> "Any expansion signals from existing customers?"
>
> "Who's been mentioning competitors lately?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning pipeline hygiene.** *"Who's waiting on a reply?"*
The `follow-up-radar` returns every thread where someone's waiting
past a silence threshold — them on us, us on them, or a question
that was never answered. Three threads need a response today.

**Pre-call prep.** *"Brief me on Maria Chen at Northstar for
tomorrow's 10am."* `meeting-prep-briefing` pulls relationship
history, last discussed, open items, concerns raised, what they care
about, and what to prioritize. You walk in 10 minutes prepared
instead of skimming a 40-message thread on the way to the call.

**Mid-week deal diagnosis.** *"What's friction-y on the Acme
deal?"* `deal-friction-detector` returns objections, hesitation
language, discount asks, response delays — and surfaces the
contrarian positives too, so the briefing isn't single-sided.

**Discovery support.** *"Have we solved an inventory-visibility
problem like this before?"* `past-solutions-matcher` searches the
last two years for customers with a similar problem and what we
did. Three matches, with quotable customer outcomes.

**End-of-quarter scans.** *"Any expansion signals?"* and *"Who's
been mentioning competitors lately?"* — `cross-sell-upsell-signals`
and `competitor-mentions` for portfolio review.

---

## The skills

| Skill | When to use it |
|---|---|
| [`follow-up-radar`](skills/follow-up-radar/) | Threads where someone is waiting past silence thresholds — them on us, us on them, unanswered questions |
| [`deal-open-items`](skills/deal-open-items/) | Open commitments, unanswered questions, unresolved decisions on a specific deal or across deals |
| [`deal-friction-detector`](skills/deal-friction-detector/) | Friction signals on a specific deal — objections, hesitation, discount asks, response delays. Requires a deal/company name. |
| [`meeting-prep-briefing`](skills/meeting-prep-briefing/) | Pre-meeting brief on a specific contact at a specific company — history, open items, concerns, what they care about. Requires contact + company. |
| [`past-solutions-matcher`](skills/past-solutions-matcher/) | Past customers who faced a similar problem and how it was solved. Requires a problem description. |
| [`competitor-mentions`](skills/competitor-mentions/) | Mentions of competitors and alternatives by audience type, with sentiment context |
| [`cross-sell-upsell-signals`](skills/cross-sell-upsell-signals/) | Expansion signals from existing customers — budget hints, growth language, adjacent problems mentioned |

Each skill collects what it needs from you (time window, deal,
contact, company, problem description, etc.) and returns structured
findings with evidence from the actual email threads. Prospect
quotes are preserved verbatim where they matter — voice carries
into the next conversation.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"what's the state of the pipeline"*.
The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — friction on near-term deals first,
then follow-ups overdue, then expansion signals, then competitive
intelligence.

The agent enforces three sales-specific guardrails: deal-stage claims
don't get inflated ("we're close" doesn't become "closing"),
contrarian signals are surfaced even on positive-looking deals
(single-sided briefings lead to surprises), and prospect quotes get
preserved verbatim where they matter.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Prospect
voices are preserved verbatim where they're useful. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** who's waiting on a reply from me?

**Claude:** *(running `follow-up-radar` — scanning sales threads from the last 60 days for silence-threshold violations)*

**6 threads need attention today.**

**They're waiting on us (silence > 5 BD)**

**Northstar Logistics — Maria Chen** (last reply from her Mar 1, 9 BD)
She asked two specific questions: pricing for a 200-seat deployment
and a security review timeline.
*Recommended: substantive reply today; both questions are buying
signals.*

**Bluefield Co — Tomás G.** (last reply from him Mar 4, 6 BD)
He shared procurement documentation and asked about the redlines
turnaround.
*Recommended: confirmation today even if redlines aren't ready —
silence at procurement stage reads as withdrawal.*

**Acme Corp — Sarah K.** (last reply from her Mar 6, 4 BD — at
threshold)
She replied to your demo follow-up with a calendar request for two
of her engineers to see a deeper technical session.
*Recommended: schedule the technical session this week.*

**We're waiting on them (silence > 7 BD)**

**Greenfield Partners — Lia V.** (last reply from us Feb 28, 10 BD)
We sent the proposal and have heard nothing since.
*Recommended: a "checking in" note today; if no response by end of
week, consider closing the loop or moving to nurture.*

**Constellation Capital — Andrew P.** (last reply from us Mar 1, 9 BD)
We sent the technical questionnaire response.
*Recommended: gentle nudge; reference a specific item to give them
something to react to.*

**Unanswered question**

**Apex Digital — Diego R.** (asked Feb 25, never substantively
answered)
He asked about the customer-success motion specifically: how onboarding
is staffed for accounts our size. We replied with general "we'll set
you up" language, not the specific staffing question.
*Recommended: actually answer the staffing question this week — he
asked it for a reason.*

> *Want me to draft the Northstar reply, the Bluefield confirmation,
> the Apex staffing answer, or all three?*

---

**You:** brief me on maria chen at northstar logistics for tomorrow's call

**Claude:** *(running `meeting-prep-briefing` — assembling history, status, open items, concerns, and priorities for Maria Chen at Northstar Logistics)*

**Pre-meeting brief — Maria Chen, VP Operations, Northstar
Logistics.**

**Relationship history** — 4 months
First contact Nov 8 via warm intro from Jason at Beacon Logistics.
Discovery call Dec 4. Demo Jan 18. Three follow-up threads since,
last substantive Mar 1.

**Last discussed and current status**

She asked two specific questions in her last email:
1. **Pricing for a 200-seat deployment.** She mentioned the team
   size has been confirmed.
2. **Security review timeline.** Her IT team needs to know how long
   our SOC 2 review process takes for procurement.

She closed the email with: *"This is moving — internally we're
aligned that we want to do this in Q2."*

**Open commitments**

- We owe: substantive answers on both questions above. (Past due 9
  BD.)
- She owes: confirmed buying committee — she said in early February
  she'd loop in the CFO before final negotiation. Hasn't yet.

**Concerns / objections raised historically**

- **Implementation risk** (raised Dec 4, addressed Jan 18 demo). She
  liked the implementation approach.
- **Internal change management** (raised Feb 14). She mentioned her
  team is "change-averse"; you sent a customer story about a
  similar-stage rollout; she replied positively.

**What she cares about most** *(from her own words across threads)*

> "If this works it has to work for the operations leads, not just
> the analysts." (Dec 4)

> "I want to feel confident about how this lands with my team — that
> matters more than the feature list." (Jan 18)

> "Our top-down ROI math has to make sense, but the bottom-up
> adoption is what actually decides this." (Feb 14)

**Pattern:** her decision criteria sit on adoption / change
management more than feature parity. The CFO loop will be about
ROI, but Maria's call is about people.

**Watch (contrarian signal worth knowing)**

She's said *"this is moving"*, but the CFO loop hasn't happened
yet. Stage discipline: this is qualified discovery, not late-stage
negotiation. Don't let confidence on her side translate into
forecast lift on ours yet.

**For tomorrow's call — recommended priorities**

1. Answer the pricing question with the 200-seat number.
2. Lay out the security review timeline concretely.
3. Land the CFO conversation — confirm Maria will loop in this
   week.
4. Re-anchor on adoption / change management; reference the
   customer story she liked.

> *Want me to draft a 1-page leave-behind that confirms answers to
> her two questions, or a follow-up after the call?*

---

**You:** what's friction-y on the acme deal?

**Claude:** *(running `deal-friction-detector` — scanning Acme Corp threads from the last 60 days)*

**3 friction signals + 2 positive signals on the Acme deal.** This
is a balanced read, not a single-sided briefing.

**Friction**

**Discount conversation has shifted** (moderate)
In the proposal thread Feb 14 they accepted standard pricing. In a
follow-up Mar 1 the procurement contact asked about "any flexibility
on the year-2 ramp pricing". Not a hard request — but the
conversation now exists.
*Recommended: don't volunteer a discount yet; have a defensible
position ready if they ask formally.*

**Approval language emerging** (low-moderate)
Sarah K. mentioned in a thread Mar 6 that *"we'll need to coordinate
with finance"*. This wasn't on the buying committee map a month ago.
*Recommended: ask explicitly who needs to be in the room for the
final approval. Surfacing the committee shape now beats discovering
it later.*

**Technical session ask post-demo** (low)
Sarah asked for a deeper technical session for her engineers (see
follow-up-radar). On its own this is normal — but combined with the
discount conversation, it could indicate a competitive eval
underway.
*Recommended: do the session well; ask casually whether they're
evaluating others.*

**Positive (worth not losing sight of)**

**Champion engagement is high.** Sarah has replied to every email
within 1 BD. She's volunteered customer-side stakeholder names
(unprompted) and asked unprompted questions about implementation
specifics — both stage-progression signals.

**Internal momentum reference.** Her email Mar 1: *"Internally I've
got buy-in from product and ops; finance is the one I need to bring
along."* That's an honest stage assessment that maps cleanly to a
real procurement path.

**Net read**

Mid-funnel, real momentum, real but normal friction emerging. Stage
is "evaluation with procurement orientation", not "closing soon."
The technical session is the right next step; the discount and
finance conversations are early signals to handle deliberately.

> *Want me to draft a discount-position note for your records, a
> committee-mapping question for Sarah, or both?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the sales agent kicks in, running 4 skills in parallel
against your email through iGPT — follow-up radar, deal open items,
deal friction, expansion signals...)*

**This week, in priority order:**

**Reply today (high-leverage)**

1. **Northstar — Maria Chen waiting 9 BD on pricing + security
   answers**
   Both are buying-signal questions. Substantive reply today.

2. **Bluefield — Tomás G. waiting 6 BD on redlines status**
   Confirmation today even without final redlines.

3. **Apex — Diego R.'s staffing question never substantively
   answered**
   He asked it for a reason. Answer this week.

**Friction to handle deliberately**

4. **Acme — discount conversation emerging; finance loop signaled**
   Don't volunteer pricing flexibility. Surface the buying
   committee shape with Sarah.

**Pipeline hygiene (this week)**

5. **Greenfield Partners — proposal sent Feb 28, no response 10 BD**
   Checking-in note; if silence by Friday, decide on nurture.

6. **Constellation Capital — questionnaire response, 9 BD silence**
   Gentle nudge; reference a specific item.

**Tomorrow (already prepped)**

7. **Northstar — Maria Chen 10am call**
   Brief above. Priorities: pricing, security, CFO loop, adoption
   anchor.

**Watch**

8. **Acme technical session ask + discount question — possible
   competitive eval**
   Confirm casually during the technical session.

> *Where would you like to start? I can draft any of the replies, the
> Acme committee-mapping question, the Greenfield checking-in note,
> or the Northstar leave-behind for tomorrow.*

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

**Stage discipline.** A prospect saying *"this is moving"* doesn't
mean the deal is closing. The skills frame findings using the
evidence's language and avoid inflating signals. Forecast hygiene
starts with not letting one positive note override stage-appropriate
caution.

**Contrarian signals surfaced.** When summarizing a deal that looks
positive, the briefing also flags any friction. When summarizing a
deal that looks negative, it flags any positives. Single-sided
briefings lead to surprises later.

**Prospect quotes preserved verbatim.** Direct quotes from the
prospect — concerns, objections, must-haves, internal-momentum
references — are quoted as written. Voice carries into the next
conversation; paraphrasing strips usable signal.

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
2. **Find `igpt-sales`.** In the iGPT marketplace, click into
   **igpt-sales** to see the skills and the agent it includes.
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
   language — *"who's waiting on a reply?"*, *"what's friction-y on
   the Acme deal?"* — and the right skill or the agent picks up
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
/plugin install igpt-sales@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-sales/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-sales.md
└── skills/
    ├── competitor-mentions/
    ├── cross-sell-upsell-signals/
    ├── deal-friction-detector/
    ├── deal-open-items/
    ├── follow-up-radar/
    ├── meeting-prep-briefing/
    └── past-solutions-matcher/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 60 days", "since the proposal went out", "May 2024",
"the last 2 years" — all fine. You don't need to type ISO dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your stage taxonomy,
friction signal categories, expansion signal types, competitor list,
silence thresholds.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the sales guardrails — stage
discipline, contrarian signals surfaced, prospect quotes preserved.
Add the new skill to the agent's "Available skills" list.

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

**`follow-up-radar`** — for "who's waiting on a reply from me":

```json
{
  "as_of": "2026-03-10",
  "they_waiting_on_us": [
    {
      "company": "Northstar Logistics",
      "contact": "Maria Chen",
      "last_their_message_date": "2026-03-01",
      "business_days_silent": 9,
      "outstanding_questions": [
        "Pricing for 200-seat deployment",
        "Security review timeline"
      ],
      "signal_strength": "buying_signals",
      "recommended_action": "Substantive reply today"
    },
    {
      "company": "Bluefield Co",
      "contact": "Tomás G.",
      "last_their_message_date": "2026-03-04",
      "business_days_silent": 6,
      "context": "Procurement stage; awaiting redlines turnaround",
      "recommended_action": "Confirmation today even without final redlines"
    }
  ],
  "we_waiting_on_them": [
    {
      "company": "Greenfield Partners",
      "contact": "Lia V.",
      "last_our_message_date": "2026-02-28",
      "business_days_silent": 10,
      "context": "Proposal sent, no response",
      "recommended_action": "Checking-in note; if silence by Friday, consider nurture"
    }
  ],
  "unanswered_questions": [
    {
      "company": "Apex Digital",
      "contact": "Diego R.",
      "question": "How is onboarding staffed for accounts our size?",
      "asked_date": "2026-02-25",
      "our_response_summary": "General 'we'll set you up' — did not actually answer",
      "recommended_action": "Substantively answer this week"
    }
  ],
  "they_waiting_count": 3,
  "we_waiting_count": 2,
  "unanswered_count": 1,
  "summary": "6 threads need attention. 3 high-leverage replies are owed today; 2 outbound nudges this week; 1 unanswered question to actually address."
}
```

**`deal-friction-detector`** — for "what's friction-y on the Acme
deal":

```json
{
  "as_of": "2026-03-10",
  "deal": "Acme Corp",
  "friction_signals": [
    {
      "type": "discount_conversation_shifted",
      "severity": "moderate",
      "summary": "Procurement asked about flexibility on year-2 ramp pricing after initially accepting standard pricing",
      "evidence_thread_dates": ["2026-02-14", "2026-03-01"],
      "recommended_action": "Don't volunteer a discount; have a defensible position ready if asked formally"
    },
    {
      "type": "approval_language_emerging",
      "severity": "low_moderate",
      "summary": "Champion mentioned needing to coordinate with finance — finance was not previously on the buying committee map",
      "evidence_thread_date": "2026-03-06",
      "evidence_quote": "we'll need to coordinate with finance",
      "recommended_action": "Ask explicitly who needs to be in the room for final approval"
    },
    {
      "type": "competitive_eval_signal_low_confidence",
      "severity": "low",
      "summary": "Technical-session ask post-demo, combined with discount conversation, could indicate a competitive eval — but on its own normal",
      "evidence_thread_date": "2026-03-06",
      "recommended_action": "Do the session well; ask casually whether they're evaluating others"
    }
  ],
  "positive_signals": [
    {
      "type": "champion_engagement_high",
      "summary": "Champion replies within 1 BD; volunteered stakeholder names; asked unprompted implementation questions"
    },
    {
      "type": "internal_momentum_reference",
      "summary": "Champion's own framing of where buy-in stands maps cleanly to a real procurement path",
      "evidence_quote": "Internally I've got buy-in from product and ops; finance is the one I need to bring along."
    }
  ],
  "stage_assessment": "evaluation_with_procurement_orientation",
  "stage_discipline_note": "Champion's positive signals do not justify forecast lift to closing-soon yet",
  "summary": "3 friction signals (1 moderate, 2 low/low-moderate) + 2 positive signals. Mid-funnel, real momentum, real but normal friction emerging."
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
