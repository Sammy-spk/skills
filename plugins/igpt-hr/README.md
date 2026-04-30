# igpt-hr

HR intelligence for HR business partners, people leaders, and recruiters
managing internal talent operations. Turn the email already in your
inbox into a live picture of where hiring is stalling, which offers
need attention, where onboarding is breaking, and what the org is
quietly asking about or feeling.

`5 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

HR work runs on email — the parts of it that aren't already in the
ATS. Hiring manager feedback that comes back in a thread instead of
the system. Offer negotiations that happen over a few back-and-forths.
New hire onboarding tasks that get assigned, accepted, and then
forgotten. Policy questions that get asked the same way by twelve
different employees in twelve different threads. Subtle signals about
team friction that nobody notices until someone resigns.

A single recruiter or HRBP can be working forty active candidates
across a dozen reqs, three onboardings in flight, and two slow
problems brewing — all visible only by reading every thread, which
nobody has time for.

This plugin gives you five focused workflows that mine your HR email
and return structured answers about what is actually happening across
hiring, onboarding, policy, and people.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Where's the hiring process stuck?"
>
> "Any offers I should be worried about?"
>
> "How are new hires doing this week?"
>
> "What policy questions keep coming up?"
>
> "Any friction signals in the org I should know about?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention this week.

---

## A typical week

**Monday morning.** *"Where's the hiring process stuck?"* The
`candidate-pipeline-tracker` returns every active candidate's current
stage, the most recent action, and what's blocking forward motion. You
see two candidates have been waiting 6+ business days for hiring
manager feedback; nudge time.

**Tuesday after offer was sent Friday.** *"How does the Acme offer
look?"* `offer-status-tracker` returns offer status, negotiation
points, expected start date, and red flags. The candidate has been
silent for 4 days after asking about equity vesting — proactive
clarification is in order.

**Wednesday new-hire check.** *"Any new hires blocked?"*
`onboarding-action-items` returns outstanding onboarding tasks per new
hire — IT access, equipment, paperwork, training, intros. One new hire
hasn't received their laptop on day 4; escalate to IT.

**End of month, broader scan.** *"What policy questions keep coming
up?"* `policy-question-miner` returns the questions employees actually
asked — what was answered, what wasn't, which questions came up
multiple times. You spot three repeated questions about parental leave
that signal the policy doc isn't doing its job.

---

## The skills

| Skill | When to use it |
|---|---|
| [`candidate-pipeline-tracker`](skills/candidate-pipeline-tracker/) | Active candidates across open roles — current stage, last action, next step, who owns it, where it stalled |
| [`offer-status-tracker`](skills/offer-status-tracker/) | Offers made — current status, negotiation points, expected start, offers outstanding too long |
| [`onboarding-action-items`](skills/onboarding-action-items/) | Open onboarding tasks per new hire — access, equipment, paperwork, intros, training |
| [`policy-question-miner`](skills/policy-question-miner/) | HR policy questions and benefits inquiries asked across the org — what was answered, repeat questions, gaps |
| [`team-friction-detector`](skills/team-friction-detector/) | Signals of tension, communication breakdowns, disengagement, interpersonal conflict in internal threads |

Each skill collects what it needs from you (time window, role,
employee, etc.) and returns structured findings with evidence from the
actual email threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"how is hiring going across the
board"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — friction signals or stuck onboardings
first, then offers at risk of going stale, then candidate pipeline
gaps.

The agent also enforces the plugin's tone guardrails: neutral
observational language, framing patterns rather than judgments about
people, and treating friction signals as items worth a closer look —
not verdicts.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. People are
described in measured, observational language; patterns are surfaced,
not judgments rendered. The structured output that powers the rendering
is documented under "Output schemas" below if you want to see it.

---

**You:** where's the hiring process stuck?

**Claude:** *(running `candidate-pipeline-tracker` — scanning hiring threads from the last 90 days for stage status and stall signals)*

**4 candidates have stalled or near-stalled across 3 open roles.**

**Senior Backend Engineer (hiring manager: Maria Chen)**

**Sarah K.** — interview feedback overdue 7 business days
Onsite completed Mar 1. Two of four interviewers have submitted
feedback; two haven't. Candidate has not heard from us since.
*Recommended: nudge the two interviewers today; send a holding note
to the candidate.*

**Marcus T.** — phone screen scheduled, then deferred twice
Phone screen rescheduled twice in 2 weeks (each by us). Candidate
asked Mar 4 whether we're still interested.
*Recommended: lock the next slot or move to decline if the role
priorities have shifted.*

**Product Designer (hiring manager: Raj Patel)**

**Lena V.** — offer discussions stalled awaiting compensation band
Offer conversation paused Feb 28 pending updated salary band approval.
Candidate has been quiet since.
*Recommended: confirm the band and re-engage with a target date.*

**Senior CS Manager (hiring manager: Jordan Lee)**

**Daniel R.** — final round complete, no decision in 9 business days
Final round Feb 26. Hiring manager said "want to think about it",
no follow-up since.
*Recommended: close-the-loop conversation with hiring manager;
candidate likely fielding other offers.*

> *Want me to draft hiring-manager nudges, holding notes for the
> candidates, or both?*

---

**You:** any offers i should be worried about?

**Claude:** *(running `offer-status-tracker` — scanning offer-related threads from the last 90 days)*

**3 offers in flight. 1 needs proactive attention.**

**Acme — Engineering** (extended Mar 5, candidate Lena V.)
Status: questions raised. Candidate asked about equity vesting and
remote-first policy 4 days ago. We confirmed receipt; substantive
response not yet sent.
Expected start: Apr 14. Offer outstanding 5 days.
*Recommended: send the substantive response today. Silence at this
stage usually means a competing offer is being closed.*

**Acme — Marketing** (extended Mar 7, candidate Priya M.)
Status: under review with stated decision date.
Candidate said "I'll have a decision by end of next week." On track.
Expected start: Apr 21.
*Status: monitor.*

**Acme — Operations** (extended Mar 9, candidate Tomás G.)
Status: signed.
Background check pending; routine turnaround.
*Status: complete; route to onboarding kickoff.*

> *Want me to draft a substantive equity + remote-policy response for
> Lena, or set a calendar nudge for Priya's stated decision date?*

---

**You:** how are new hires doing?

**Claude:** *(running `onboarding-action-items` — scanning new-hire onboarding threads from the last 90 days)*

**4 new hires in onboarding. 2 have outstanding action items.**

**Camille L. — VP Marketing (started Mar 3, day 5)**

Outstanding:
- **Laptop not yet delivered** (IT order placed Feb 26; no shipping
  confirmation in email)
- Benefits enrollment paperwork sent Mar 3, not returned

*Action: escalate to IT today; HR ops to follow up on benefits
paperwork.*

**Tomás G. — Operations (started Mar 8, day 2)**

Outstanding:
- **Manager intro meeting not scheduled**
- Slack and ticketing system access not provisioned

*Action: nudge hiring manager Jordan Lee for intro; IT to provision
access.*

**On track**

- **Anjali B.** — Senior Engineer (started Feb 24, day 13). All
  onboarding tasks confirmed complete; first 1:1 with manager done.
- **Erik S.** — Customer Success (started Feb 17, day 18). Shadowed 4
  CS calls; ramp plan on schedule.

> *Want me to draft an IT escalation for Camille's laptop or a manager
> nudge to Jordan for Tomás's intro?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the HR agent kicks in, running 4 skills in parallel
against your email through iGPT — candidate pipeline, offer status,
onboarding, policy questions...)*

**This week, in priority order:**

**Risk of losing someone (act today)**

1. **Lena V. (Acme Engineering offer) — equity questions unanswered
   for 4 days**
   Substantive response needed today.

2. **Camille L. — laptop missing on day 5**
   IT escalation needed; new-hire experience is bad signal.

**Hiring momentum (this week)**

3. **Sarah K. backend engineer — interview feedback overdue 7 BD**
   Two interviewers haven't submitted; candidate hasn't heard from
   us. Nudge today.

4. **Daniel R. CS manager — no decision 9 BD after final round**
   Close-the-loop conversation with hiring manager.

5. **Marcus T. backend phone screen — twice deferred**
   Lock the next slot or move to decline.

**Pattern worth a closer look**

6. **Parental leave policy questions — 3 separate threads in 6 weeks**
   The policy doc isn't doing its job. Worth a brief update or an
   FAQ supplement.

> *Where would you like to start? I can draft Lena's response, the
> IT escalation, the interviewer nudges, or all three.*

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

**Tone and people-data care.** HR email contains compensation,
performance, interpersonal conflict, and termination context. The
skills and agent use neutral, observational language and frame people
patterns as "worth a closer look", not as judgments about
individuals. `team-friction-detector` is treated especially carefully
— its outputs are signals, not verdicts.

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
2. **Find `igpt-hr`.** In the iGPT marketplace, click into **igpt-hr**
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
   language — *"where's hiring stuck?"*, *"any offers I should be
   worried about?"* — and the right skill or the agent picks up
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
/plugin install igpt-hr@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-hr/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-hr.md
└── skills/
    ├── candidate-pipeline-tracker/
    ├── offer-status-tracker/
    ├── onboarding-action-items/
    ├── policy-question-miner/
    └── team-friction-detector/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 30 days", "since the role opened", "May 2024", "since the
reorg" — all fine. You don't need to type ISO dates.

**Add categories specific to your team.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your hiring playbook
or policy taxonomy — interview stage names, offer status types,
onboarding tracks, policy areas, friction-signal categories your team
already uses.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the tone guardrails — neutral
observational language, patterns over judgments. Add the new skill to
the agent's "Available skills" list.

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

**`candidate-pipeline-tracker`** — for "where's the hiring process
stuck":

```json
{
  "as_of": "2026-03-10",
  "stalled_candidates": [
    {
      "candidate_name": "Sarah K.",
      "role": "Senior Backend Engineer",
      "hiring_manager": "Maria Chen",
      "stage": "post_onsite_awaiting_feedback",
      "days_in_stage": 7,
      "blocker": "2 of 4 interviewers have not submitted feedback",
      "candidate_last_contacted": "2026-03-01",
      "recommended_action": "Nudge the two interviewers today; send holding note to candidate"
    },
    {
      "candidate_name": "Marcus T.",
      "role": "Senior Backend Engineer",
      "hiring_manager": "Maria Chen",
      "stage": "phone_screen_deferred",
      "days_in_stage": 14,
      "blocker": "Phone screen rescheduled twice by us; candidate asked if we are still interested",
      "candidate_last_contacted": "2026-03-04",
      "recommended_action": "Lock next slot or move to decline if priorities shifted"
    }
  ],
  "by_role": [
    { "role": "Senior Backend Engineer", "stalled_count": 2 },
    { "role": "Product Designer", "stalled_count": 1 },
    { "role": "Senior CS Manager", "stalled_count": 1 }
  ],
  "total_stalled": 4,
  "summary": "4 candidates stalled across 3 roles. Most concerning: Sarah K. (7 BD without feedback) and Daniel R. (9 BD without decision)."
}
```

**`offer-status-tracker`** — for "any offers I should be worried
about":

```json
{
  "as_of": "2026-03-10",
  "offers": [
    {
      "candidate_name": "Lena V.",
      "role": "Engineering",
      "extended_date": "2026-03-05",
      "days_outstanding": 5,
      "status": "questions_raised",
      "open_questions": ["equity vesting", "remote-first policy"],
      "days_since_question": 4,
      "expected_start": "2026-04-14",
      "risk_level": "high",
      "recommended_action": "Send substantive response today; silence at this stage often signals a competing offer being closed"
    },
    {
      "candidate_name": "Priya M.",
      "role": "Marketing",
      "extended_date": "2026-03-07",
      "days_outstanding": 3,
      "status": "under_review",
      "candidate_stated_decision_date": "2026-03-21",
      "expected_start": "2026-04-21",
      "risk_level": "low",
      "recommended_action": "Monitor; calendar nudge for stated decision date"
    },
    {
      "candidate_name": "Tomás G.",
      "role": "Operations",
      "extended_date": "2026-03-09",
      "status": "signed",
      "next_step": "background_check_pending",
      "risk_level": "none",
      "recommended_action": "Route to onboarding kickoff"
    }
  ],
  "high_risk_count": 1,
  "low_risk_count": 1,
  "complete_count": 1,
  "summary": "3 offers in flight. Lena V. needs proactive equity + remote response today (high risk). Priya M. is on track. Tomás G. is signed."
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
