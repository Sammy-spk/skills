# igpt-projects

Project intelligence for project managers, program managers, and
operators running cross-functional initiatives. Turn the email already
in your inbox into a live picture of what's blocked, what's slipping,
what's been decided, and which stakeholder owes what.

`5 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Project work runs on email — the parts that don't live in the project
tracker. Decisions get made in threads and then nobody can find them
when someone asks "wait, when did we agree to that?". Blockers get
raised, escalated, and sometimes silently dropped. Risk signals appear
in language ("slipping", "concerned about timing", "we may need
more resources") long before they show up on a status report. Action
items get assigned to specific people in side-of-thread asks and then
get lost. Milestone updates appear in scattered confirmations and
nobody assembles them into a real status picture until the steering
meeting.

This plugin gives you five focused workflows that mine your project
email and return structured answers about what's actually open,
slipping, blocked, or decided across your initiatives.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What's blocking the Phoenix migration?"
>
> "Any risk signals on the Q1 launch?"
>
> "Where do milestones stand for the customer portal redesign?"
>
> "What did we decide on the Phoenix architecture?"
>
> "What action items does Maria owe?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a triage list with
blockers and at-risk milestones first.

---

## A typical week

**Monday morning.** *"What's blocking the Phoenix migration?"* The
`project-blocker-detector` returns every blocker on that project —
what's stuck, who owns resolving it, how long it's been outstanding.
You see two blockers waiting on the same person; nudge today.

**Wednesday before the steering meeting.** *"Where do milestones
stand for Phoenix?"* `milestone-status-extractor` returns every
milestone, target date, and current status from email evidence. You
walk in knowing the picture without re-reading the project channel.

**Mid-week risk scan.** *"Any risk signals on the Q1 launch?"*
`risk-radar` returns language patterns suggesting timelines may slip,
resources are stretched, or scope is quietly expanding. Two signals
worth raising in the next steering meeting.

**End of week, action item review.** *"What action items are open
across all projects?"* `stakeholder-action-tracker` returns every
assigned action item with owner, deadline, and completion evidence.
Three are overdue without comment.

**When someone asks "what did we decide?".** *"What did we decide on
Phoenix architecture?"* `decision-log` reconstructs the decision with
date, who decided, alternatives considered, and conditions attached.

---

## The skills

| Skill | When to use it |
|---|---|
| [`decision-log`](skills/decision-log/) | Significant decisions on a project — what was decided, who decided, alternatives considered, conditions attached |
| [`milestone-status-extractor`](skills/milestone-status-extractor/) | Milestones and phases — target dates, current status from email evidence, on-track / at-risk / delayed |
| [`project-blocker-detector`](skills/project-blocker-detector/) | Blockers, dependencies, impediments — what's stuck, who owns resolving it, how long outstanding |
| [`risk-radar`](skills/risk-radar/) | Risk signals — timeline slippage, resource pressure, scope additions, stakeholder dissatisfaction |
| [`stakeholder-action-tracker`](skills/stakeholder-action-tracker/) | Action items assigned to specific stakeholders, by project — status of each |

Each skill collects what it needs from you (project name, time
window, stakeholder, etc.) and returns structured findings with
evidence from the actual email threads.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"what's the state of all my
projects"*. The agent picks the right skills, runs them in parallel,
and synthesizes a status update — milestones with current status
first, then blockers, then risks, then recent decisions worth noting.

The agent enforces three project-specific guardrails: a project is
"delayed" only if email evidence says so (and "at risk" if the
language is cautious — never escalate from one to the other without
evidence); decisions are reconstructed faithfully including
alternatives and conditions; and broad questions get a project-name
clarification asked first when the question is project-specific.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Decisions are
reconstructed faithfully. The structured output that powers the
rendering is documented under "Output schemas" below if you want to see
it.

---

**You:** what's blocking the phoenix migration?

**Claude:** *(running `project-blocker-detector` — scanning Phoenix migration threads from the last 60 days)*

**4 active blockers on the Phoenix migration. 2 share an owner.**

**Critical (stalling progress)**

**Database schema sign-off** (open 9 days, owner: Lin K.)
Schema review requested Mar 1; Lin asked for clarifications on Mar 2;
team responded Mar 3; no further action from Lin since.
*Recommended: direct nudge today; this is gating the migration
script work.*

**API contract approval** (open 7 days, owner: Lin K.)
Contract proposed Mar 3; awaiting Lin's review.
*Recommended: combined nudge with the schema item — same owner.*

**This week**

**Customer notification timing** (open 4 days, owner: Maya P.)
Communications team needs to lock the cutover-week notification
timing. Maya asked for product input Mar 6; product hasn't replied.
*Recommended: ping product lead today.*

**Vendor support window** (open 12 days, owner: external — vendor X)
Cutover requires vendor X to extend their on-call support window.
Initial request Feb 26; vendor confirmed receipt but no commitment
yet.
*Recommended: escalate to vendor X account manager; cutover plan
depends on the support window.*

> *Want me to draft a combined nudge to Lin K. on the schema and API
> items, the product lead ping, or the vendor X escalation?*

---

**You:** any risk signals on the q1 launch?

**Claude:** *(running `risk-radar` — analyzing Q1 launch threads from the last 60 days for risk patterns)*

**3 risk signals on the Q1 launch. None are red yet.**

**Yellow — timeline pressure language emerging**

In two threads (Mar 4, Mar 8), the engineering lead used phrasing
like *"we'll see if we can hold the date"* and *"keeping it tight"*.
Not a formal slip flag — but a shift from the confident tone of
4 weeks ago.

*Recommended: direct conversation with the engineering lead this
week. Better to surface a slip 30 days early than 5.*

**Yellow — scope addition without formal agreement**

Marketing asked Feb 28 if a localization for one additional language
could "land in the launch window". No formal agreement; engineering
hasn't pushed back but hasn't committed either.

*Recommended: explicit decision needed this week — yes (with scope
implications) or no.*

**Watch — resource concern**

Design lead mentioned in passing on Mar 5: *"capacity is tight if any
new asks come in"*. No specific issue yet, but the next ask should
trigger a re-prioritization conversation rather than a quiet add.

> *Want me to draft a 1:1 talking-points note for the engineering
> lead conversation, or a decision memo on the localization scope
> question?*

---

**You:** what did we decide on the phoenix architecture?

**Claude:** *(running `decision-log` — reconstructing significant decisions on the Phoenix migration from the last 90 days)*

**Phoenix architecture — 4 decisions reconstructed.**

**Database — Postgres** (decided Feb 18)
Decided by: tech lead Marco T., with sign-off from Lin K.
Alternatives considered: MySQL, CockroachDB.
Reason given: existing operational expertise + ecosystem maturity.
Conditions: revisit if multi-region requirements emerge in year 2.
Source thread: "Phoenix DB choice" (Feb 14–18).

**API style — REST with selective GraphQL** (decided Feb 26)
Decided by: tech lead Marco T.
Alternatives considered: full GraphQL, gRPC for internal.
Reason given: REST for external consumers; GraphQL only for the
admin console (read-heavy).
Conditions: gRPC remains an option for internal service-to-service if
performance becomes a constraint.
*Worth noting: there was disagreement in the thread. Two engineers
preferred full GraphQL. The decision was made; the thread did not
reach consensus.*
Source thread: "Phoenix API style" (Feb 22–26).

**Caching layer — Redis with planned eviction strategy** (decided
Mar 4)
Decided by: tech lead Marco T., with input from Lin K.
Alternatives considered: in-process LRU, Memcached.
Conditions: review if hit ratios fall below 80% in production.

**Deployment — single-region first, multi-region phase 2** (decided
Mar 6)
Decided by: tech lead + program lead.
Conditions: phase 2 is a Q3 2026 commit, not a hand-wave; specific
trigger is signed multi-region customers.

> *Want me to package these as a decision record for the project
> wiki?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the projects agent kicks in, running 4 skills in parallel
against your email through iGPT — blockers, milestones, risks,
stakeholder actions...)*

**This week, in priority order:**

**Stalling (today)**

1. **Phoenix migration — schema + API sign-off blocked on Lin K.**
   2 items, 9 and 7 days open, same owner. Combined nudge.

2. **Q1 launch — engineering lead's tone has shifted**
   Hold a direct conversation this week; better to surface a slip
   30 days early.

**Decisions needed (this week)**

3. **Q1 launch localization — explicit yes-or-no needed**
   No formal agreement; risk of quiet scope add.

4. **Customer portal redesign — design system version pinned to v3**
   Decision discussed but not formally made; outstanding.

**Active items**

5. **Vendor X support window — escalate to account manager**
   Cutover plan depends on it; 12 days outstanding.

6. **3 stakeholder actions overdue without comment**
   Quick reminder loop on each.

**Watch**

7. **Q1 launch — design lead capacity concern**
   No specific issue yet; next ask should trigger re-prioritization.

> *Where would you like to start? I can draft the Lin K. combined
> nudge, the engineering lead 1:1 talking points, the localization
> decision memo, or the vendor X escalation.*

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

**Facts vs. sentiment.** A milestone is "delayed" only if email
evidence says so. It's "at risk" if the language is cautious. The
skills and agent never escalate from one to the other without
evidence — small distinctions matter when the output is going to the
status report.

**Decisions reconstructed faithfully.** When the decision log
reconstructs a decision, it includes alternatives considered and
conditions attached — and notes when there was disagreement in the
thread that didn't reach consensus. Decision logs that smooth over
disagreement become misleading; the skill keeps the texture.

**Project name first.** Most skills make more sense scoped to a
specific project. If a question is project-specific and no project is
named, the agent asks before running.

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
2. **Find `igpt-projects`.** In the iGPT marketplace, click into
   **igpt-projects** to see the skills and the agent it includes.
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
   language — *"what's blocking the Phoenix migration?"*, *"any risk
   signals on the Q1 launch?"* — and the right skill or the agent
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
/plugin install igpt-projects@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-projects/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-projects.md
└── skills/
    ├── decision-log/
    ├── milestone-status-extractor/
    ├── project-blocker-detector/
    ├── risk-radar/
    └── stakeholder-action-tracker/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 60 days", "since the kickoff", "May 2024", "since the
last steering meeting" — all fine. You don't need to type ISO dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your project
classifications, milestone status levels, blocker types, risk
categories, decision categories.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the project guardrails — facts
vs. sentiment distinction, faithful decision reconstruction. Add the
new skill to the agent's "Available skills" list.

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

**`project-blocker-detector`** — for "what's blocking the Phoenix
migration":

```json
{
  "as_of": "2026-03-10",
  "project_scope": "Phoenix migration",
  "blockers": [
    {
      "title": "Database schema sign-off",
      "owner": "Lin K.",
      "owner_role": "internal",
      "raised_date": "2026-03-01",
      "days_open": 9,
      "severity": "critical",
      "context": "Schema review requested Mar 1; Lin asked for clarifications Mar 2; team responded Mar 3; no further action from Lin since",
      "downstream_impact": "Gating the migration script work",
      "recommended_action": "Direct nudge today"
    },
    {
      "title": "API contract approval",
      "owner": "Lin K.",
      "owner_role": "internal",
      "raised_date": "2026-03-03",
      "days_open": 7,
      "severity": "critical",
      "context": "Contract proposed Mar 3; awaiting review",
      "recommended_action": "Combined nudge with the schema item"
    },
    {
      "title": "Vendor X support window for cutover",
      "owner": "Vendor X account manager",
      "owner_role": "external",
      "raised_date": "2026-02-26",
      "days_open": 12,
      "severity": "high",
      "context": "Vendor confirmed receipt but no commitment yet",
      "downstream_impact": "Cutover plan depends on it",
      "recommended_action": "Escalate to vendor account manager"
    }
  ],
  "by_owner": [
    { "owner": "Lin K.", "blocker_count": 2 }
  ],
  "critical_count": 2,
  "high_count": 1,
  "this_week_count": 1,
  "summary": "4 active blockers; 2 share an owner (Lin K.); 1 external blocker requires vendor escalation."
}
```

**`decision-log`** — for "what did we decide on the Phoenix
architecture":

```json
{
  "as_of": "2026-03-10",
  "project_scope": "Phoenix migration",
  "decisions": [
    {
      "topic": "Database choice",
      "decided": "Postgres",
      "decided_by": ["Marco T. (tech lead)", "Lin K. (sign-off)"],
      "decided_on": "2026-02-18",
      "alternatives_considered": ["MySQL", "CockroachDB"],
      "reason_given": "Existing operational expertise + ecosystem maturity",
      "conditions": ["Revisit if multi-region requirements emerge in year 2"],
      "consensus": true,
      "source_thread": "Phoenix DB choice (Feb 14–18)"
    },
    {
      "topic": "API style",
      "decided": "REST with selective GraphQL for admin console",
      "decided_by": ["Marco T. (tech lead)"],
      "decided_on": "2026-02-26",
      "alternatives_considered": ["Full GraphQL", "gRPC for internal"],
      "reason_given": "REST for external consumers; GraphQL only for the admin console (read-heavy)",
      "conditions": ["gRPC remains an option for internal service-to-service if performance becomes a constraint"],
      "consensus": false,
      "disagreement_note": "Two engineers preferred full GraphQL; the decision was made but the thread did not reach consensus",
      "source_thread": "Phoenix API style (Feb 22–26)"
    },
    {
      "topic": "Caching layer",
      "decided": "Redis with planned eviction strategy",
      "decided_by": ["Marco T. (tech lead)", "Lin K. (input)"],
      "decided_on": "2026-03-04",
      "alternatives_considered": ["in-process LRU", "Memcached"],
      "conditions": ["Review if hit ratios fall below 80% in production"],
      "consensus": true
    }
  ],
  "decision_count": 4,
  "non_consensus_count": 1,
  "summary": "4 decisions reconstructed. One (API style) was made without consensus; the disagreement is preserved in the record."
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
