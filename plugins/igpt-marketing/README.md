# igpt-marketing

Marketing intelligence for marketing leaders, brand managers, and
growth operators. Turn the email already in your inbox into a live
picture of agency deliverables, brand mentions, campaign feedback,
event coordination, partnership pipeline, and press / PR activity.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

A lot of marketing's signal lives in email — between the team, the
agency, partners, journalists, customers, and the people who write
inbound notes about your brand. Agency deliverables get committed to in
threads that nobody centralizes. Customers say something quote-worthy
in a reply and it never makes it into a case study. Press pitches
outbound and the responses (or the silence) live in inboxes nobody
audits at the end of the quarter. Event logistics scatter across
dozens of vendors and confirmations. A grumpy customer email gets
forwarded around but nobody flags whether it's a one-off or a pattern.

This plugin gives you six focused workflows that mine your marketing
email and return structured answers about what's actually shipping,
who's saying what about the brand, where partnerships and press are
landing, and what's stalled.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "Any agency deliverables outstanding?"
>
> "What are people saying about us this quarter?"
>
> "What's the press picture this month?"
>
> "Where do partnerships stand?"
>
> "Any event action items still open?"
>
> "What feedback came back on the Spring launch?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning agency check.** *"Any agency deliverables
outstanding?"* The `agency-deliverables-tracker` returns every
deliverable from creative agencies and freelancers — what's in
revision, what's late, what's awaiting feedback. Two from Atlas
Studio are 4 days late; quick check-in.

**Mid-week brand pulse.** *"What are people saying about us this
quarter?"* `brand-mention-sentiment` returns external mentions of the
brand from customers, partners, and press, with sentiment patterns by
audience type. You spot three quote-worthy customer praise lines worth
sending to the case-study queue.

**Pre-event sweep.** *"Any open action items for the Acme Summit?"*
`event-action-items` returns outstanding logistics, vendor
deliverables, speaker confirmations, and post-event follow-ups for
the upcoming event. Two speakers haven't confirmed travel and one
sponsorship deliverable is overdue.

**End of quarter, press + partnerships.** *"What's the press picture
and where do partnerships stand?"* `press-coverage-tracker` and
`partnership-pipeline-tracker` give you the consolidated view for
quarterly review.

---

## The skills

| Skill | When to use it |
|---|---|
| [`agency-deliverables-tracker`](skills/agency-deliverables-tracker/) | Deliverables expected from agencies and freelancers — revisions, feedback loops, what's late |
| [`brand-mention-sentiment`](skills/brand-mention-sentiment/) | External mentions of the brand by audience type; sentiment patterns, quotable lines |
| [`campaign-feedback-miner`](skills/campaign-feedback-miner/) | Feedback and reactions on specific campaigns from internal and external sources; common themes |
| [`event-action-items`](skills/event-action-items/) | Outstanding tasks across event lifecycles — logistics, vendors, speakers, sponsors, post-event follow-up |
| [`partnership-pipeline-tracker`](skills/partnership-pipeline-tracker/) | Partnership and BD conversations — stage, last contact, next step, open commitments |
| [`press-coverage-tracker`](skills/press-coverage-tracker/) | Press / PR activity — coverage landed, pitches outstanding, journalist relationships, media opportunities |

Each skill collects what it needs from you (time window, agency,
campaign, event, audience segment, etc.) and returns structured
findings with evidence from the actual email threads. Quotes worth
preserving are surfaced verbatim — voice is content.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"how is the brand doing"*. The
agent picks the right skills, runs them in parallel, and synthesizes a
prioritized list — overdue agency deliverables and event blockers
first, then press / brand signals worth responding to, then
partnership pipeline items going stale.

The agent enforces two marketing-specific guardrails: quote brand
mentions and customer feedback verbatim where it preserves voice
(testimonial-worthy lines deserve to land in your hands as the
customer wrote them), and distinguish signal from noise (a single
grumpy email isn't a brand crisis; a pattern across multiple senders
is).

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. Quote-worthy
customer voices are preserved verbatim. The structured output that
powers the rendering is documented under "Output schemas" below if you
want to see it.

---

**You:** any agency deliverables outstanding?

**Claude:** *(running `agency-deliverables-tracker` — scanning agency and freelancer threads from the last 90 days)*

**5 deliverables in flight across 3 agencies. 2 are running late.**

**Late — Atlas Studio**

**Spring launch hero illustration** (committed Mar 1, due Mar 5,
4 days overdue)
Most recent thread: round 2 revisions sent Mar 3. Atlas confirmed
receipt; no further update.
*Recommended: status check today; production deadline depends on
this asset.*

**Customer-story video — Northstar Logistics edit** (committed Feb 22,
due Mar 8, 2 days overdue)
Rough cut delivered on time; revised cut promised Mar 8 with the new
B-roll; not yet received.
*Recommended: confirm new ETA; schedule the review session.*

**On track — Northwind Creative**

**Q2 campaign creative concepts** (due Mar 14)
Initial directions delivered Mar 6; feedback session scheduled for
Mar 11.
*Status: on track.*

**Newsletter template refresh** (due Mar 20)
Wireframes approved Mar 4; design in progress.
*Status: on track.*

**On track — Beacon Design**

**Pitch deck template** (due Mar 22)
Outline approved Mar 7; design in progress.
*Status: on track.*

> *Want me to draft the Atlas status check or the Northstar edit
> follow-up?*

---

**You:** what are people saying about us this quarter?

**Claude:** *(running `brand-mention-sentiment` — scanning inbound external email from the last 90 days for brand mentions and sentiment)*

**38 brand mentions surfaced across 4 audience types. Net positive
overall; 3 quote-worthy lines and 1 pattern worth attention.**

**Customer praise — quote-worthy**

> "Honestly, this has saved my team about 4 hours a week. We didn't
> realize how much time we were spending on this until we stopped."
> — *Operations Lead, Northstar Logistics, Feb 28*

> "The integration with our existing stack was the smoothest we've
> done in years. Worth flagging that to other prospects."
> — *Head of IT, Apex Digital, Mar 3*

> "Your support team replied in 12 minutes on a Saturday. Genuinely
> didn't expect that and it mattered."
> — *Customer success contact, Bluefield Co, Feb 14*

*Recommended: route these to the case-study and testimonial queue.*

**Press / analyst — neutral**

Two analyst notes from independent firms referencing us in coverage
of the category. Coverage is factual; no pull-quotes worth
amplifying yet.

**Customer concern — pattern worth attention**

Three customers in the last 6 weeks raised the same friction point:
the onboarding wizard's third step. Language varied
("confusing", "we got stuck", "took us a couple of attempts") but
the consistency suggests a real UX issue rather than three
unrelated complaints.

*Recommended: brief Product about the pattern; one fix could
prevent more friction.*

**Partner outreach — positive sentiment, no specific quotes**

Three new partner inbounds in the last 30 days mentioning a peer
recommendation. Suggests organic word-of-mouth in the partner
ecosystem.

> *Want me to package the customer praise lines for Marketing's
> case-study queue, or draft a brief for Product on the onboarding
> wizard pattern?*

---

**You:** what's the press picture this month?

**Claude:** *(running `press-coverage-tracker` — scanning press / PR threads from the last 90 days)*

**Coverage landed — 3 stories. Pitches outstanding — 6.**

**Coverage that landed**

**Forbes — "How [Category] is changing"** (published Mar 2)
Featured quote from our CEO in a category overview piece. 8
companies mentioned; we got a single sentence. Modest amplification
visible in the partner echo.

**TechCrunch — funding announcement** (published Feb 18)
Standard funding coverage; Andrew picked up the story off the
embargo list; quote from our CEO and from Beacon Partners as lead
investor.

**Stratechery — analytical piece referencing the category** (published
Feb 25)
We're mentioned alongside three peers in a thesis-level piece; not a
feature, but a category-credentializing mention.

**Pitches outstanding**

| Outlet | Reporter | Pitch sent | Status |
|---|---|---|---|
| The Information | Saira Patel | Mar 1 | engaged — asked for customer references |
| Bloomberg | Mark Chen | Feb 22 | acknowledged, no follow-up since |
| Wall Street Journal | (no specific reporter) | Feb 14 | no response |
| Wired | Lia Chen | Mar 5 | engaged — wants product walkthrough |
| Ars Technica | Brian Diaz | Feb 28 | engaged — researching |
| Forbes | Sarah K. | Feb 8 | gone quiet |

**Pitches needing action**

- The Information: provide the requested customer references this
  week to keep momentum.
- Wired: schedule the product walkthrough.
- Forbes (Sarah K.): close the loop or move on; 31 days quiet.

> *Want me to draft a customer reference brief for The Information,
> a Wired walkthrough scheduling note, or a close-the-loop check-in
> for Forbes?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the marketing agent kicks in, running 4 skills in parallel
against your email through iGPT — agency deliverables, brand mentions,
press coverage, event action items...)*

**This week, in priority order:**

**Production blockers (today)**

1. **Atlas Studio — Spring launch hero illustration, 4 days late**
   Production deadline depends on it. Status check today.

2. **Acme Summit — 2 speakers haven't confirmed travel**
   Event is in 18 days. Travel locks in this week or next.

**Press momentum (this week)**

3. **The Information — customer references requested**
   Saira Patel asked Mar 1; high-leverage piece. Provide references
   this week to keep momentum.

4. **Wired — product walkthrough scheduling**
   Lia Chen engaged. Schedule before momentum cools.

**Brand health (act this week)**

5. **Onboarding wizard step 3 — pattern across 3 customers**
   Brief Product. Consistent friction point worth a fix.

6. **Customer praise queue — 3 quote-worthy lines**
   Route to case-study and testimonial queue.

**Watch**

7. **Forbes (Sarah K.) — 31 days quiet**
   Close the loop or accept it's not happening.

> *Where would you like to start? I can draft the Atlas status check,
> the customer reference brief for The Information, the Wired
> scheduling note, or the Product brief on the onboarding pattern.*

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

**Voice is content.** When customer praise, campaign feedback, or
brand mentions are quote-worthy, the renderer preserves them verbatim.
A direct quote from the customer lands in your hands as the customer
wrote it — useful for testimonials, case studies, pull-quotes, and
internal proof points.

**Patterns over outliers.** A single grumpy email isn't a brand
crisis. A pattern across multiple senders is. The skills and the
agent flag patterns explicitly and avoid amplifying isolated reactions
into something larger.

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
2. **Find `igpt-marketing`.** In the iGPT marketplace, click into
   **igpt-marketing** to see the skills and the agent it includes.
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
   language — *"any agency deliverables outstanding?"*, *"what are
   people saying about us this quarter?"* — and the right skill or
   the agent picks up automatically.

You do steps 1–4 once. After that, the plugin is always available and
your iGPT connection is remembered.

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter
`https://mcp.igpt.ai/` and complete the OAuth flow. The plugin's skills
trigger automatically based on what you ask.

### Claude Code

```
/plugin marketplace add igptai/skills
/plugin install igpt-marketing@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-marketing/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-marketing.md
└── skills/
    ├── agency-deliverables-tracker/
    ├── brand-mention-sentiment/
    ├── campaign-feedback-miner/
    ├── event-action-items/
    ├── partnership-pipeline-tracker/
    └── press-coverage-tracker/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 90 days", "since the rebrand", "May 2024", "since the
campaign launched" — all fine. You don't need to type ISO dates.

**Add categories your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit your workflow —
deliverable types specific to your agencies, audience segments
specific to your ICP, campaign-feedback themes you track, partnership
types, press tiers.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). Mirror the marketing guardrails —
preserve voice in quotes, distinguish patterns from outliers. Add the
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

**`brand-mention-sentiment`** — for "what are people saying about us
this quarter":

```json
{
  "period_from": "2025-12-10",
  "period_to": "2026-03-10",
  "audience_scope": "all",
  "mentions": [
    {
      "audience_type": "customer",
      "person_company": "Operations Lead, Northstar Logistics",
      "date": "2026-02-28",
      "context": "Praising time savings",
      "sentiment": "positive",
      "quote": "Honestly, this has saved my team about 4 hours a week. We didn't realize how much time we were spending on this until we stopped.",
      "quote_worthy": true,
      "case_study_candidate": true
    },
    {
      "audience_type": "customer",
      "person_company": "Head of IT, Apex Digital",
      "date": "2026-03-03",
      "context": "Praising integration experience",
      "sentiment": "positive",
      "quote": "The integration with our existing stack was the smoothest we've done in years. Worth flagging that to other prospects.",
      "quote_worthy": true,
      "case_study_candidate": true
    }
  ],
  "patterns": [
    {
      "type": "consistent_friction",
      "summary": "3 customers in 6 weeks raised the onboarding wizard's third step",
      "audience_type": "customer",
      "evidence_count": 3,
      "severity": "moderate",
      "recommended_action": "Brief Product about the pattern"
    },
    {
      "type": "organic_word_of_mouth",
      "summary": "3 partner inbounds mentioned peer recommendations",
      "audience_type": "partner",
      "evidence_count": 3,
      "severity": "positive",
      "recommended_action": "Track for partner program signal"
    }
  ],
  "by_audience": {
    "customer": { "count": 18, "net_sentiment": "positive" },
    "press": { "count": 6, "net_sentiment": "neutral" },
    "partner": { "count": 9, "net_sentiment": "positive" },
    "prospect": { "count": 5, "net_sentiment": "mixed" }
  },
  "summary": "38 mentions, net positive overall. 3 quote-worthy lines for case studies; 1 pattern (onboarding step 3) worth a Product brief."
}
```

**`press-coverage-tracker`** — for "what's the press picture this
month":

```json
{
  "as_of": "2026-03-10",
  "coverage_landed": [
    {
      "outlet": "Forbes",
      "reporter": "Sarah K.",
      "headline": "How [Category] is changing",
      "published": "2026-03-02",
      "type": "category_overview",
      "depth": "single_sentence_mention"
    },
    {
      "outlet": "TechCrunch",
      "reporter": "Andrew M.",
      "headline": "Funding announcement",
      "published": "2026-02-18",
      "type": "funding",
      "depth": "feature"
    },
    {
      "outlet": "Stratechery",
      "headline": "Category thesis piece",
      "published": "2026-02-25",
      "type": "analytical",
      "depth": "category_credentializing_mention"
    }
  ],
  "pitches_outstanding": [
    {
      "outlet": "The Information",
      "reporter": "Saira Patel",
      "pitch_date": "2026-03-01",
      "status": "engaged",
      "outstanding_request": "customer references",
      "recommended_action": "Provide references this week to keep momentum"
    },
    {
      "outlet": "Wired",
      "reporter": "Lia Chen",
      "pitch_date": "2026-03-05",
      "status": "engaged",
      "outstanding_request": "product walkthrough",
      "recommended_action": "Schedule walkthrough before momentum cools"
    },
    {
      "outlet": "Forbes",
      "reporter": "Sarah K.",
      "pitch_date": "2026-02-08",
      "status": "gone_quiet",
      "days_quiet": 31,
      "recommended_action": "Close the loop or accept"
    }
  ],
  "coverage_count": 3,
  "pitches_outstanding_count": 6,
  "pitches_engaged_count": 3,
  "pitches_gone_quiet_count": 1,
  "summary": "3 stories landed. 6 pitches outstanding — 3 actively engaged, 1 gone quiet, 2 acknowledged without follow-up."
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
