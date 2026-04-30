# igpt-recruiting

Recruiting intelligence for in-house recruiters, talent acquisition
leaders, and agency recruiters. Turn the email already in your inbox
into a live picture of where hiring is moving, where it's stuck, which
offers need attention, and which agencies are actually delivering.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Recruiting runs on email — even with an ATS in the loop. Hiring
manager feedback comes back in threads, not the system. Offer
negotiations happen in back-and-forths nobody reconstructs at the
quarter close. Sourcing conversations land or stall depending on what
gets followed up — and a lot of warm conversations go quiet because
nobody nudged the right way at the right time. Agency submissions
flood in, and which agency is actually delivering vs. just spamming
becomes hard to see without a pattern view. After every loss, the
"why didn't they accept?" question gets answered anecdotally — and
then the same factor causes the next loss six weeks later.

This plugin gives you six focused workflows that mine your hiring
email and return structured answers about pipeline health, offer
risk, agency performance, sourcing momentum, hiring manager
alignment, and decline patterns.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Where is hiring stuck?"
>
> "What offers are at risk?"
>
> "Where are reqs not getting traction?"
>
> "Why are we losing offers lately?"
>
> "How are our agencies performing?"
>
> "Are hiring managers and recruiters aligned on the open roles?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning pipeline check.** *"Where is hiring stuck?"* The
`interview-pipeline-tracker` returns every active candidate, current
stage, last action, and where the process has stalled. You see two
candidates have been waiting 6+ business days for hiring manager
feedback; nudge time.

**Mid-week alignment check.** *"Are recruiters and hiring managers
aligned on open roles?"* The `hiring-manager-alignment-checker`
returns signals of misalignment — shifting criteria, slow feedback,
inconsistent rejections. Frames patterns, not judgments. One role
shows feedback cycles averaging 7 business days; worth a recalibration
conversation.

**Pre-debrief.** *"Why have we been losing offers?"* The
`offer-decline-analyzer` returns patterns across declines —
compensation signals, competing offers, role-fit reasons. The picture
shows a pattern: 3 of the last 5 declines cited the comp band as a
factor.

**End of month, agency review.** *"How are our agencies doing?"*
`agency-recruiter-tracker` returns submission volume, hiring manager
reactions, fee arrangements, and whether each agency is meeting their
commitments. One agency has submitted 14 candidates in a month with
zero advancing past phone screen.

---

## The skills

| Skill | When to use it |
|---|---|
| [`interview-pipeline-tracker`](skills/interview-pipeline-tracker/) | Active candidates' stage, feedback received, who hasn't submitted feedback, where the process stalled |
| [`agency-recruiter-tracker`](skills/agency-recruiter-tracker/) | External agencies — roles worked, candidates submitted, fee arrangements, delivery patterns |
| [`hiring-manager-alignment-checker`](skills/hiring-manager-alignment-checker/) | Signals of misalignment — shifting criteria, slow feedback, inconsistent rejections |
| [`job-requisition-status`](skills/job-requisition-status/) | Open reqs — approval status, JD finalized, sourcing started, pipeline depth, stall signals |
| [`offer-decline-analyzer`](skills/offer-decline-analyzer/) | Patterns across declined offers — reasons, competing offers, comp signals |
| [`sourcing-conversation-tracker`](skills/sourcing-conversation-tracker/) | Outbound prospect conversations — who responded, level of interest, where conversations went quiet |

Each skill collects what it needs from you (time window, role,
candidate, etc.) and returns structured findings with evidence from
the actual email threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"how is hiring going across the
board"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — candidates where feedback is overdue
or stages are stalling first, then reqs without progress, then process
or alignment issues, then trend signals from offer declines.

The agent enforces the plugin's care rules: candidate names treated
as sensitive (first name + last initial only when summarizing), hiring
manager performance described as patterns rather than judgments
("feedback cycles averaged 6 days" is fine; "Manager X is slow" is
not), and a careful distinction between process issues and candidate
issues when conversations go quiet.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Candidates
are referenced by first name + last initial. Hiring manager performance
is described as patterns, not character judgments. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** where is hiring stuck?

**Claude:** *(running `interview-pipeline-tracker` — scanning hiring threads from the last 90 days)*

**4 candidates stalled across 3 open roles. 2 share a hiring manager.**

**Senior Backend Engineer (HM: Maria Chen)**

**Sarah K.** — interview feedback overdue 7 business days
Onsite completed Mar 1. 2 of 4 interviewers have submitted feedback;
2 haven't.
*Recommended: nudge the 2 outstanding interviewers today; send a
holding note to the candidate.*

**Marcus T.** — phone screen scheduled, then deferred twice
Phone screen rescheduled twice in 14 days (each by us). Candidate
asked Mar 4 whether we're still interested.
*Recommended: lock the next slot or move to decline if priorities
shifted.*

**Product Designer (HM: Raj Patel)**

**Lena V.** — offer discussions stalled awaiting comp band
Offer conversation paused Feb 28 pending updated salary band approval.
Candidate has been quiet since.
*Recommended: confirm the band and re-engage with a target date.*

**Senior CS Manager (HM: Jordan Lee)**

**Daniel R.** — final round complete, no decision in 9 BD
Final round Feb 26. HM said "want to think about it"; no follow-up
since.
*Recommended: close-the-loop conversation with the hiring manager;
candidate likely fielding other offers.*

> *Want me to draft hiring manager nudges, holding notes for the
> candidates, or both?*

---

**You:** are recruiters and hiring managers aligned on open roles?

**Claude:** *(running `hiring-manager-alignment-checker` — scanning recruiting threads from the last 90 days)*

**3 alignment signals across 2 roles. None are conclusions — these
are patterns worth a conversation.**

**Senior Backend Engineer**

- Feedback cycles for this role have averaged **7 business days**
  over the last quarter (against the team's 3-BD target).
- 2 candidates rejected after final round; reasons cited were
  "team fit" and "felt junior", neither of which had been raised as
  criteria earlier in the process.

*Pattern worth a closer look:* the rejection reasons may signal that
final-round criteria are different from what's documented at intake.
Worth a calibration session before more candidates move to onsite.

**Product Designer**

- The job description has been edited 3 times in 8 weeks (most
  recently changing the seniority slug from "Senior" to "Mid-to-
  Senior"). Recruiter has flagged the changes in two threads.

*Pattern worth a closer look:* JD instability is making sourcing
inconsistent. Worth a 30-minute conversation to lock the role
definition.

**Senior CS Manager**

- Hiring manager has not yet replied to the recruiter's request for
  a sample debrief format (asked Mar 1).

*Pattern worth a closer look:* small request, but unanswered — and
the role has been open 47 days. Easier to ask now than later.

> *Want me to draft a calibration-session request for the Senior
> Backend Engineer role or the JD-lock conversation for Product
> Designer?*

---

**You:** why have we been losing offers?

**Claude:** *(running `offer-decline-analyzer` — scanning offer-decline threads from the last 12 months)*

**5 declines in the last 12 months. 1 clear pattern, 1 emerging
pattern.**

**Pattern — comp band cited in 3 of 5 declines** (clear)

| Candidate | Role | Reason mentioned |
|---|---|---|
| Andrew P. | Senior Engineer | "Comp came in below my current" |
| Yuki S. | Engineering Manager | "Total comp gap of ~$25K with my other offer" |
| Diego R. | Senior Designer | "Base was the gap; equity didn't bridge" |

*Worth raising:* the comp band conversation. 3 of 5 declines is
above what the broader market explains; worth a comp-team check on
where bands sit vs. comparable companies.

**Pattern — remote/hybrid policy cited in 2 of 5 declines**
(emerging)

Two candidates explicitly mentioned remote work as a factor. One had
moved to a fully-remote role; the other cited "concerns about the
hybrid expectation."

*Worth raising:* if remote-flex was previously a tiebreaker in our
favor, it may now be working against us. Worth a quiet check on how
the policy is being communicated late in the process.

**Other reasons (single instances)**

- 1 decline cited "scope of role" (Senior CS Manager — Daniel R., who
  ultimately took an EM role elsewhere)
- 1 decline cited "company stage" (early hire who chose a later-stage
  competitor)

*These are single data points — keep an eye on them but don't
generalize from one.*

> *Want me to package these as a memo for the leadership team or
> draft a comp-band review request?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the recruiting agent kicks in, running 4 skills in
parallel against your email through iGPT — interview pipeline,
hiring manager alignment, offer decline patterns, sourcing
conversations...)*

**This week, in priority order:**

**Risk of losing someone (today)**

1. **Sarah K. — interview feedback overdue 7 BD**
   Nudge the 2 outstanding interviewers today; holding note to
   candidate.

2. **Daniel R. — 9 BD without a decision after final round**
   Close-the-loop conversation with HM Jordan Lee.

**Pipeline momentum (this week)**

3. **Marcus T. — twice-deferred phone screen**
   Lock the slot or decline.

4. **Lena V. — offer discussions stalled on comp band**
   Confirm band; re-engage.

5. **Senior Backend Engineer feedback cycle averaging 7 BD**
   Calibration session with HM Maria Chen.

**Patterns worth raising**

6. **Comp band cited in 3 of 5 recent declines**
   Comp-team check on where bands sit vs. comparable companies.

7. **Remote/hybrid policy emerging as decline factor**
   Worth understanding how it's being communicated late in process.

**Watch**

8. **Constellation Talent — 14 submissions, zero advancing**
   Agency conversation needed; not this week, but on the list.

> *Where would you like to start? I can draft the interviewer nudges,
> the Daniel R. close-the-loop note, the Lena V. re-engagement, the
> calibration request, or the comp-band review memo.*

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

**Candidate names are sensitive.** When summarizing, candidates are
referenced by first name + last initial. Full names appear only where
explicitly required (e.g. official offer correspondence drafted on
your behalf). The skills and agent don't speculate about what a
candidate is "really" thinking — they stick to evidence in the email.

**Hiring manager performance is patterns, not judgments.** "Feedback
cycles for this role have averaged 7 business days" is the kind of
statement the skills produce. "Manager X is slow" is the kind they
don't. The same data point with different framing produces a usable
conversation vs. an HR-incident-style summary.

**Process issues vs. candidate issues.** A candidate going quiet may
be the candidate's choice or the process losing them. The skills
flag the pattern carefully and avoid auto-blaming either side without
evidence.

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
2. **Find `igpt-recruiting`.** In the iGPT marketplace, click into
   **igpt-recruiting** to see the skills and the agent it includes.
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
   language — *"where is hiring stuck?"*, *"why have we been losing
   offers?"* — and the right skill or the agent picks up
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
/plugin install igpt-recruiting@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-recruiting/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-recruiting.md
└── skills/
    ├── agency-recruiter-tracker/
    ├── hiring-manager-alignment-checker/
    ├── interview-pipeline-tracker/
    ├── job-requisition-status/
    ├── offer-decline-analyzer/
    └── sourcing-conversation-tracker/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 90 days", "since the role opened", "May 2024", "since
the last quarterly review" — all fine. You don't need to type ISO
dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your interview stage
names, offer status types, decline reason categories, agency tiers,
sourcing channel types.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the recruiting tone guardrails —
candidate names sensitive, hiring manager performance as patterns
rather than judgments. Add the new skill to the agent's "Available
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

**`interview-pipeline-tracker`** — for "where is hiring stuck":

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
      "candidate_last_contacted_by": "us",
      "recommended_action": "Nudge the 2 outstanding interviewers; holding note to candidate"
    },
    {
      "candidate_name": "Daniel R.",
      "role": "Senior CS Manager",
      "hiring_manager": "Jordan Lee",
      "stage": "post_final_awaiting_decision",
      "days_in_stage": 9,
      "blocker": "Hiring manager said 'want to think about it'; no follow-up since",
      "recommended_action": "Close-the-loop conversation with HM; candidate likely fielding other offers"
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

**`offer-decline-analyzer`** — for "why have we been losing offers":

```json
{
  "period_from": "2025-03-10",
  "period_to": "2026-03-10",
  "decline_count": 5,
  "patterns": [
    {
      "factor": "compensation_band",
      "occurrence_count": 3,
      "occurrence_share": 0.6,
      "strength": "clear_pattern",
      "examples": [
        { "candidate": "Andrew P.", "role": "Senior Engineer", "quoted_reason": "Comp came in below my current" },
        { "candidate": "Yuki S.", "role": "Engineering Manager", "quoted_reason": "Total comp gap of ~$25K with my other offer" },
        { "candidate": "Diego R.", "role": "Senior Designer", "quoted_reason": "Base was the gap; equity didn't bridge" }
      ],
      "recommended_action": "Comp-team check on where bands sit vs. comparable companies"
    },
    {
      "factor": "remote_hybrid_policy",
      "occurrence_count": 2,
      "occurrence_share": 0.4,
      "strength": "emerging_pattern",
      "examples": [
        { "candidate": "Olivia M.", "role": "Senior PM", "context": "moved to a fully-remote role" },
        { "candidate": "Theo K.", "role": "Senior Engineer", "quoted_reason": "concerns about the hybrid expectation" }
      ],
      "recommended_action": "Quiet check on how policy is being communicated late in the process"
    }
  ],
  "single_instance_factors": [
    { "factor": "scope_of_role", "candidate": "Daniel R.", "context": "took an EM role elsewhere" },
    { "factor": "company_stage", "candidate": "(early hire)", "context": "chose a later-stage competitor" }
  ],
  "summary": "5 declines in 12 months. Comp band cited in 3 (clear pattern). Remote/hybrid cited in 2 (emerging pattern). 2 single-instance factors worth monitoring."
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
