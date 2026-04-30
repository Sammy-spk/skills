# igpt-research

Research intelligence for academic researchers, principal
investigators, and research lab leaders. Turn the email already in
your inbox into a live picture of grant deadlines, papers in flight,
collaborator commitments, data-access status, lab action items, and
literature shared with you.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

Research runs on email — between collaborators, co-authors, funders,
data providers, journal editors, reviewers, and lab members. Grant
deadlines hide in long announcement threads. Papers under revision
slip past their deadlines because the back-and-forth with co-authors
lives across 30 messages nobody consolidates. Collaborators commit to
deliverables in friendly threads ("happy to share that data once we
finalize the protocol") and the commitment quietly drifts. Data-access
requests bounce between you and a custodian for weeks. Action items get
assigned to lab members in side asks and get lost. Papers and
preprints flow into the lab inbox and the truly relevant ones don't
get read because nobody flagged them.

This plugin gives you six focused workflows that mine your research
email and return structured answers about what's actually open,
slipping, blocking, or worth your attention this week.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What grant deadlines are coming up?"
>
> "Where do my papers stand?"
>
> "What commitments are open between me and my collaborators?"
>
> "What data-access requests are stuck?"
>
> "What action items does Anjali owe?"
>
> "Anything in the literature I should be reading?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list
of where to spend your attention.

---

## A typical week

**Monday morning grants check.** *"What grant deadlines are coming
up?"* The `grant-deadline-tracker` returns every grant with a
submission date, internal review milestones, owner assignments, and
progress signals. You see one R01 has a section assigned to Dr. Patel
that's flagged as not yet started; check-in needed.

**Mid-week paper review.** *"Where do my papers stand?"* The
`publication-pipeline-tracker` returns each manuscript's stage,
editorial status, reviewer feedback summaries, and any deadlines.
One paper has a 14-day revision deadline approaching with two
co-author actions outstanding.

**Friday lab meeting prep.** *"What action items are open across the
lab?"* `research-action-items` returns commitments by lab member —
analyses, experiments, code, reviews. Two analyses overdue; surface
in the lab meeting agenda.

**Pre-collaborator meeting.** *"What commitments are open between me
and the Bayesian lab collaboration?"* `collaboration-commitment-
tracker` separates *your* outstanding commitments from *theirs*. You
walk in knowing exactly what you owe before they ask.

**Quarterly literature pulse.** *"Anything in the literature I
should be reading?"* `literature-tracker` returns papers and
preprints shared with you across the quarter, ranked by relevance to
ongoing projects. Two were flagged by collaborators with explicit
"you might want to cite this".

---

## The skills

| Skill | When to use it |
|---|---|
| [`collaboration-commitment-tracker`](skills/collaboration-commitment-tracker/) | Commitments by you and by collaborators (data, analyses, drafts, reviews) — separates your outstanding obligations from theirs |
| [`data-source-tracker`](skills/data-source-tracker/) | Data sources, datasets, access requests — approval status, agreements, blocking issues |
| [`grant-deadline-tracker`](skills/grant-deadline-tracker/) | Grant applications and funding opportunities — submission deadlines, internal milestones, owner assignments, progress |
| [`literature-tracker`](skills/literature-tracker/) | Papers, preprints, datasets, and reports shared in email — relevance to ongoing projects, follow-up actions expected |
| [`publication-pipeline-tracker`](skills/publication-pipeline-tracker/) | Manuscripts under submission or revision — stage, decisions, reviewer feedback, deadlines, co-author actions |
| [`research-action-items`](skills/research-action-items/) | Action items assigned to lab members — analyses, experiments, code, writing, reviews |

Each skill collects what it needs from you (time window, project,
collaborator, etc.) and returns structured findings with evidence
from the actual email threads. Submission deadlines, revision
windows, and other hard-edged dates are presented verbatim — never
paraphrased ("end of the month" is not a substitute for an explicit
date).

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"walk me through where my projects
stand"*. The agent picks the right skills, runs them in parallel, and
synthesizes a prioritized list — grant and revision deadlines first,
then commitments past their informal deadline, then action items
overdue, then literature worth reviewing.

The agent enforces the plugin's care rules: hard-edged deadlines
preserved verbatim, *your* commitments separated from your
collaborators' (because what you owe matters most for triage), and
authorship / credit / reviewer identity treated carefully — what the
email says, no inference.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Deadlines
are quoted verbatim. The structured output that powers the rendering
is documented under "Output schemas" below if you want to see it.

---

**You:** what grant deadlines are coming up?

**Claude:** *(running `grant-deadline-tracker` — scanning grant and funding email from the last 12 months)*

**4 grants in flight. 2 with deadlines in the next 60 days.**

**Action this month**

**NIH R01 — Continuation submission, due Apr 5**
PI: you. Co-Is: Dr. Chen, Dr. Patel.
Internal milestones referenced in email:
- Specific Aims final by **Mar 18**
- Significance & Innovation by **Mar 22**
- Approach (Dr. Patel-owned) **not yet started** as of Mar 8
- Budget by **Mar 28**
*Recommended: check in with Dr. Patel about Approach this week. Not
yet started with 28 days to go is tight given internal review
overhead.*

**NSF CAREER — pre-proposal due Mar 22**
PI: you. No co-Is.
Internal milestone referenced: drafting one-pager by **Mar 15**.
*Status: tracked; on schedule per most recent thread.*

**Action next 60 days**

**EU Horizon Europe — collaborative proposal, due May 14**
Co-PIs: Prof. Martínez (Barcelona), Dr. Lin (Shanghai).
Coordinator: Prof. Martínez. Your role: WP3 lead.
Internal milestone for our WP3: contribution due **Apr 28**.
*Status: tracked; Prof. Martínez requested updated CVs from
collaborators by Mar 31.*

**NIH R21 — resubmission, due May 30**
Reviewer responses to draft.
*Status: in revision; co-author input expected.*

**Tracked further out**

2 grants with deadlines in Q3+ (private foundation grant; departmental
seed).

> *Want me to draft the Dr. Patel check-in or build a status note for
> Prof. Martínez?*

---

**You:** where do my papers stand?

**Claude:** *(running `publication-pipeline-tracker` — scanning manuscript and journal threads from the last 12 months)*

**5 papers in pipeline. 1 needs co-author action this week.**

**Revision deadline approaching — Hippocampal Encoding Paper**
- Journal: Nature Neuroscience
- Status: major revision invited Feb 14
- Revision deadline: **Mar 24** (14 days remaining)
- Co-author actions outstanding:
  - **Sarah K.** — re-run statistics with reviewer's suggested model
    (acknowledged Feb 22, no update since)
  - **Marcus T.** — supplementary figure update (acknowledged Feb 22,
    figures shared with you Mar 7 for review)
*Recommended: nudge Sarah this week; finish Marcus's figure review
this weekend.*

**Under review — BioProtein Methods Paper**
- Journal: eLife
- Status: under review since Feb 4
- Standard turnaround for this journal: 6–8 weeks
- *Status: monitor; no action needed.*

**Submitted, awaiting decision — Synaptic Plasticity Letter**
- Journal: Cell Reports
- Submitted Mar 1
- *Status: standard wait period.*

**In drafting — Imaging Pipeline Paper**
- Target journal: NeuroImage
- Last co-author update: Feb 22 (Anjali B.)
- *Status: writing in progress; no deadline pressure.*

**Editor response pending — Theory Paper**
- Journal: PLOS Computational Biology
- Submitted Jan 18, no editor response since
- *Status: outside standard turnaround. Polite editor inquiry
  appropriate.*

> *Want me to draft the nudge to Sarah, the editor inquiry for the
> Theory paper, or both?*

---

**You:** what commitments are open between me and the bayesian lab collaboration?

**Claude:** *(running `collaboration-commitment-tracker` — scanning the Bayesian lab collaboration threads from the last 6 months)*

**8 active commitments in this collaboration. Cleanly separated.**

**You owe (3 commitments)**

- **Updated dataset with the new participant subset** — committed
  Feb 11. No follow-up from your side since.
- **Section 3 draft of the joint paper** — committed Feb 22; "next
  two weeks" was the informal window, putting it past due.
- **Permission for Prof. Lee to use Figure 2 in their talk** —
  asked Mar 4; you have not yet replied.

**They owe you (4 commitments)**

- **Bayesian model implementation** — committed Feb 4 by their
  postdoc. No update since.
- **Participant counts from their replication study** — committed
  Feb 18 by Prof. Lee. Should arrive end of March per the email.
- **Section 5 draft of the joint paper** — committed Feb 22. No
  update; same status as your Section 3.
- **Confirmation on the conference submission joint authorship
  order** — informal commitment to clarify by Mar 1; not yet
  resolved.

**Mutual / scheduling**

- **Joint planning call** — last on Feb 14; no follow-up scheduled
  yet.

**For triage:** your three open items are the priority, especially
Section 3 and the Figure 2 permission ask (1 week stale).

> *Want me to draft a quick acknowledgment for Prof. Lee's Figure 2
> ask, an update to your collaborators on Section 3 timing, or a
> joint planning call invite?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the research agent kicks in, running 4 skills in parallel
against your email through iGPT — grant deadlines, publication
pipeline, collaboration commitments, lab action items...)*

**This week, in priority order:**

**Hard deadlines (this week)**

1. **Hippocampal Encoding Paper revision — Mar 24 deadline**
   Sarah K.'s statistics rerun + Marcus T.'s figure review.

2. **R01 Approach section — not yet started, 28 days to deadline**
   Check in with Dr. Patel; tight given internal review overhead.

**Your outstanding commitments**

3. **Updated dataset for Bayesian lab — past due**
   Send today or set an explicit new date.

4. **Section 3 draft for joint paper — past informal deadline**
   Update your collaborators on timing.

5. **Figure 2 permission for Prof. Lee — 6 days unanswered**
   Quick yes/no this week.

**Lab actions outstanding**

6. **2 lab analyses overdue from the last lab meeting**
   Surface in this Friday's meeting agenda.

**Watch**

7. **Theory Paper — editor response 51 days, outside standard window**
   Polite inquiry warranted, not urgent.

8. **2 collaborator commitments to you (Bayesian model + participant
   counts)** — track but no action needed yet.

> *Where would you like to start? I can draft Sarah's statistics
> nudge, the R01 check-in for Dr. Patel, the Section 3 timing
> update, or the Figure 2 permission reply.*

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

**Hard deadlines preserved verbatim.** Grant submission deadlines,
journal revision deadlines, and internal milestone dates are quoted as
they appear in email. "End of the month" is not a substitute for an
explicit date — research deadlines are rarely flexible.

**Your commitments separated from theirs.** When the
collaboration-commitment-tracker reconstructs an active collaboration,
it surfaces *what you owe* and *what they owe* as distinct lists.
Triage starts with what's on your plate.

**Careful with attribution.** Authorship, contribution credit, and
reviewer identity are sensitive in academia. The skills present what
the email says — they don't infer or assign credit beyond explicit
text.

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
2. **Find `igpt-research`.** In the iGPT marketplace, click into
   **igpt-research** to see the skills and the agent it includes.
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
   language — *"what grant deadlines are coming up?"*, *"where do
   my papers stand?"* — and the right skill or the agent picks up
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
/plugin install igpt-research@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-research/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-research.md
└── skills/
    ├── collaboration-commitment-tracker/
    ├── data-source-tracker/
    ├── grant-deadline-tracker/
    ├── literature-tracker/
    ├── publication-pipeline-tracker/
    └── research-action-items/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 12 months", "since the funding cycle opened", "May 2024",
"since the manuscript was first drafted" — all fine. You don't need
to type ISO dates.

**Add taxonomies your lab uses.** Each skill's output schema has
enums you can extend in the SKILL.md to fit your project codenames,
funding source categories, manuscript status taxonomy, lab role
designations.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the research guardrails — hard
deadlines verbatim, separate your commitments from theirs, careful
attribution. Add the new skill to the agent's "Available skills"
list.

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

**`grant-deadline-tracker`** — for "what grant deadlines are coming
up":

```json
{
  "as_of": "2026-03-10",
  "grants": [
    {
      "name": "NIH R01 continuation",
      "submission_deadline": "2026-04-05",
      "days_until": 26,
      "pi": "you",
      "co_investigators": ["Dr. Chen", "Dr. Patel"],
      "internal_milestones": [
        { "task": "Specific Aims final", "due": "2026-03-18", "status": "in_progress" },
        { "task": "Significance & Innovation", "due": "2026-03-22", "status": "in_progress" },
        { "task": "Approach", "due": "internal", "owner": "Dr. Patel", "status": "not_yet_started" },
        { "task": "Budget", "due": "2026-03-28", "status": "in_progress" }
      ],
      "risk_level": "moderate",
      "recommended_action": "Check in with Dr. Patel about Approach; not yet started with 28 days to go"
    },
    {
      "name": "NSF CAREER pre-proposal",
      "submission_deadline": "2026-03-22",
      "days_until": 12,
      "pi": "you",
      "internal_milestones": [
        { "task": "One-pager draft", "due": "2026-03-15", "status": "on_schedule" }
      ],
      "risk_level": "low"
    },
    {
      "name": "EU Horizon Europe collaborative proposal",
      "submission_deadline": "2026-05-14",
      "days_until": 65,
      "your_role": "WP3 lead",
      "coordinator": "Prof. Martínez (Barcelona)",
      "co_pis": ["Prof. Martínez (Barcelona)", "Dr. Lin (Shanghai)"],
      "internal_milestones": [
        { "task": "WP3 contribution", "due": "2026-04-28", "owner": "you", "status": "in_progress" },
        { "task": "Updated CVs from collaborators", "due": "2026-03-31", "status": "tracked" }
      ],
      "risk_level": "low"
    }
  ],
  "deadlines_within_30_days_count": 1,
  "deadlines_within_60_days_count": 2,
  "summary": "4 grants in flight. R01 has a section flagged as not yet started with 28 days to deadline. NSF CAREER on track."
}
```

**`collaboration-commitment-tracker`** — for "what commitments are
open between me and the Bayesian lab collaboration":

```json
{
  "as_of": "2026-03-10",
  "collaboration_scope": "Bayesian lab",
  "your_commitments": [
    {
      "summary": "Updated dataset with the new participant subset",
      "committed_on": "2026-02-11",
      "informal_deadline": null,
      "status": "open",
      "days_open": 27,
      "stale": true
    },
    {
      "summary": "Section 3 draft of the joint paper",
      "committed_on": "2026-02-22",
      "informal_deadline_text": "next two weeks",
      "status": "past_informal_deadline",
      "days_open": 16
    },
    {
      "summary": "Permission for Prof. Lee to use Figure 2 in their talk",
      "asked_on": "2026-03-04",
      "status": "awaiting_your_reply",
      "days_open": 6
    }
  ],
  "their_commitments": [
    {
      "summary": "Bayesian model implementation",
      "committed_by": "their postdoc",
      "committed_on": "2026-02-04",
      "status": "open",
      "days_open": 34
    },
    {
      "summary": "Participant counts from replication study",
      "committed_by": "Prof. Lee",
      "committed_on": "2026-02-18",
      "informal_deadline_text": "end of March",
      "status": "open"
    },
    {
      "summary": "Section 5 draft of the joint paper",
      "committed_on": "2026-02-22",
      "status": "open",
      "days_open": 16
    },
    {
      "summary": "Confirmation on conference joint authorship order",
      "informal_deadline": "2026-03-01",
      "status": "past_informal_deadline",
      "days_open": 9
    }
  ],
  "mutual": [
    {
      "summary": "Joint planning call",
      "last_held": "2026-02-14",
      "next_scheduled": null
    }
  ],
  "your_open_count": 3,
  "their_open_count": 4,
  "summary": "8 active commitments. Your three are the triage priority, especially Section 3 and the Figure 2 permission ask."
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
