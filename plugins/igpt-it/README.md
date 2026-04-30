# igpt-it

IT operations intelligence for IT teams, sysadmins, and IT managers.
Turn the email already in your inbox into a live picture of what's
open across IT — active incidents, security alerts, access requests,
change control, vendor commitments, and licenses about to renew.

`6 Skills` · `1 Agent` · `Structured Output` · `MIT License`

---

## Why this exists

A lot of IT operations work flows through email — between the ticketing
system, the cloud console, and the vendor inboxes. Phishing reports
arrive forwarded from employees. Suspicious-login alerts get sent to
the IT distribution list. Access-request approvals bounce between
manager and IT. Change requests get socialized in threads before they
hit the CAB. Vendor SLA discussions, patch schedules, and incident
post-mortems live in long email chains. License renewals show up 60
days out and disappear into someone's inbox.

For a small IT team this is dozens of threads a week to keep visible.
For a larger team it's the difference between catching a breach signal
and missing it. Either way, the picture you need is rarely
consolidated until something forces it to be.

This plugin gives you six focused workflows that mine your IT email
and return structured answers about what is actually open, escalating,
or coming due.

---

## What you can ask

Just ask in plain language. The agent or the right skill picks itself up
based on what you say:

> "What's open in IT this week?"
>
> "Any active incidents?"
>
> "Where are we exposed security-wise?"
>
> "Any access requests stuck?"
>
> "What licenses are coming up for renewal?"
>
> "How are our vendors performing on their commitments?"
>
> "Walk me through what needs my attention this week."

The last one — broad, cross-skill — is when the agent earns its keep. It
runs the relevant skills in parallel and gives you a prioritized list of
where to spend your attention.

---

## A typical week

**Monday morning ops review.** *"Any active incidents?"* The
`incident-tracker` returns every incident, outage, and unresolved
issue with current status, system affected, and ownership. You see one
incident has been open for 8 days without a post-incident review
mentioned.

**Mid-week security check.** *"Any security signals worth knowing
about?"* `security-alert-monitor` returns phishing reports forwarded
by employees, suspicious-login alerts, vulnerability disclosures, and
policy-violation signals. Two phishing reports name the same domain;
worth blocking pre-emptively.

**Quarterly license review.** *"What's coming up for renewal?"*
`license-renewal-tracker` returns SaaS subscriptions, software
licenses, and IT contracts with renewal dates, auto-renew flags, and
usage signals. Three contracts auto-renew in 60 days; two are worth
renegotiating based on usage.

**End of month, vendor scorecard.** *"How are vendors performing?"*
`it-vendor-commitment-tracker` returns commitments each vendor made
(SLAs, response times, patch schedules) and what's been delivered or
missed. One MSP has missed two committed delivery dates this quarter.

---

## The skills

| Skill | When to use it |
|---|---|
| [`access-request-tracker`](skills/access-request-tracker/) | Access and permission requests — approved, fulfilled, or stuck |
| [`change-request-log`](skills/change-request-log/) | System changes, deployments, infrastructure modifications — approval status, implemented or not |
| [`incident-tracker`](skills/incident-tracker/) | Outages, system failures, unresolved technical issues — current status and ownership |
| [`it-vendor-commitment-tracker`](skills/it-vendor-commitment-tracker/) | Promises from IT vendors and MSPs (SLAs, response times, patch schedules) — fulfilled vs. open |
| [`license-renewal-tracker`](skills/license-renewal-tracker/) | Software licenses, SaaS subscriptions, IT contracts with renewal or expiry dates |
| [`security-alert-monitor`](skills/security-alert-monitor/) | Phishing reports, suspicious logins, vulnerability disclosures, policy violations — signals to investigate |

Each skill collects what it needs from you (time window, system,
vendor, etc.) and returns structured findings with evidence from the
actual email threads. System names, ticket IDs, hostnames, and CVE
numbers are presented verbatim — never paraphrased.

---

## The agent

Each plugin includes one **agent** that handles broad, cross-skill
questions where you don't know which specific skill to invoke — *"what
needs my attention this week"* or *"where are we exposed"*. The agent
picks the right skills, runs them in parallel, and synthesizes a
prioritized list — security alerts and active incidents first, then
upcoming license renewals or expiring contracts, then access and
change backlog.

The agent enforces the plugin's care rules: security findings are
**signals to investigate**, not conclusions ("a breach happened" only
appears if the evidence explicitly says so), and identifiers are
preserved verbatim.

---

## What you see

These are real chat exchanges — you ask in plain language, Claude renders
the answer as readable markdown with action items teed up. The structured
output that powers the rendering is documented under "Output schemas"
below if you want to see it.

---

**You:** any active incidents?

**Claude:** *(running `incident-tracker` — scanning IT email from the last 60 days for incidents, outages, and unresolved technical issues)*

**3 incidents currently open. 1 needs immediate attention.**

**INC-2841 — production database elevated latency** (open 8 days)
System: `prod-db-primary`. First reported Mar 2 by the on-call
engineer; intermittent latency spikes attributed to a query plan
regression after a Postgres minor-version upgrade.
Status: mitigation applied (query rewrite); root cause not formally
documented. **No post-incident review (PIR) scheduled.**
Owner: Database team (Lin).
*Action: schedule the PIR; 8 days without one is past your team's
3-day target.*

**INC-2867 — auth-service intermittent 500s** (open 3 days)
System: `auth-service`. Reported Mar 7. Root cause traced to a token
cache eviction edge case during a deployment.
Status: hotfix deployed Mar 9; monitoring for recurrence.
Owner: Platform team (Marcus).
*Action: confirm 48-hour clean window; if no recurrence by Mar 11,
close.*

**INC-2872 — customer portal slow page loads** (open 2 days)
System: `customer-portal`. Reported Mar 8. Investigation pointing to
a CDN config change deployed Mar 6.
Status: investigating; CDN rollback being prepared.
Owner: Frontend team (Priya).
*Action: monitor; rollback decision expected today.*

> *Want me to draft a PIR scheduling note for INC-2841 or a status
> update for the customer portal team?*

---

**You:** any security signals worth knowing about?

**Claude:** *(running `security-alert-monitor` — scanning the last 30 days of email for phishing, suspicious logins, vulnerabilities, and policy signals)*

**4 security signals worth attention. None confirmed as incidents — all
warrant investigation.**

**Phishing — same domain reported twice**
Two employees forwarded suspicious emails from `notify-payroll-update[.]com` in
the last 6 days. Both impersonated the payroll provider and asked
recipients to "verify your account". Reported by Sarah K. (Mar 5) and
Tomás G. (Mar 9).
*Action to consider: block the domain at the email gateway and send a
brief org-wide note about this campaign.*

**Suspicious login — geographically improbable**
Okta admin alert Mar 7 flagged a login for user `m.chen@`
originating from a new country within 2 hours of a successful login
from the usual city. User confirmed they did not travel.
*Status: under investigation by the security team. Token revocation
and password reset performed.*

**Vulnerability disclosure — Datadog agent CVE-2025-1844**
Vendor email Mar 4 disclosed a medium-severity issue in the Datadog
agent affecting versions before 7.49.0.
*Status: patched on most hosts per the IT distribution list update;
4 hosts still on the older version per the inventory check.*

**Policy violation — credentials in a thread**
Internal email Mar 3 between two engineers contained what appears to
be an API key for `staging-billing-service` quoted inline.
*Action: rotate the key today; brief reminder to the team about
secret handling.*

**These are signals**, not confirmed breaches. The geographically
improbable login was investigated and the user confirmed no travel —
that's how it should be triaged. The "credentials in a thread" item
is a real handling issue but doesn't indicate external compromise.

> *Want me to draft the org-wide phishing note, the team reminder
> about secret handling, or the patching status follow-up for the 4
> outstanding hosts?*

---

**You:** what licenses are coming up for renewal?

**Claude:** *(running `license-renewal-tracker` — scanning the last 24 months of vendor and software email for renewal dates and notice periods)*

**12 renewals tracked. 5 in the next 90 days.**

**Action this month**

| Vendor / product | Renewal | Annual cost | Auto-renew | Action |
|---|---|---|---|---|
| GitHub Enterprise | Apr 1 | $48,000 | Yes | Confirm seat count vs. usage; 8 unused seats |
| Datadog | Apr 14 | $96,000 | Yes | Renegotiation possible — usage at 60% of plan |

**Action next 60 days**

| Vendor / product | Renewal | Annual cost | Auto-renew | Action |
|---|---|---|---|---|
| Snowflake | May 8 | $180,000 | No | Notice period 30 days; confirm renewal intent |
| Okta | May 22 | $42,000 | Yes | Standard renewal; usage at expected level |
| Atlassian Cloud | May 28 | $28,000 | Yes | Confirm Jira seat count |

**Tracked further out**

7 contracts with renewal dates beyond 90 days, including Slack
(Aug 14, $36K), Adobe Creative Cloud (Sep 1, $14K), and AWS Reserved
Instances (Nov 30 — purchase decision, not renewal).

**Worth a closer look**

- **GitHub Enterprise — 8 unused seats** at $50/seat/yr could be
  removed at renewal ($4,800 savings).
- **Datadog — 60% utilization** suggests the next tier down would
  cover usage at meaningful savings; worth a renegotiation
  conversation.

> *Want me to draft the GitHub seat-reduction note or the Datadog
> renegotiation outreach?*

---

**You:** walk me through what needs my attention this week

**Claude:** *(the IT agent kicks in, running 4 skills in parallel
against your email through iGPT — incidents, security alerts, license
renewals, vendor commitments...)*

**This week, in priority order:**

**Active operational risk (today)**

1. **INC-2841 — production database, 8 days open, no PIR scheduled**
   Schedule the PIR; surface the latency root cause.

2. **Phishing campaign — same domain reported twice**
   Block `notify-payroll-update[.]com` at the email gateway and brief
   the org.

3. **API key in a thread**
   Rotate the staging-billing key today; team reminder about secrets.

**This week**

4. **GitHub Enterprise renewal — 8 unused seats** ($4,800 savings
   available)
   Decide before Apr 1 auto-renew.

5. **Datadog renewal — 60% utilization**
   Open a renegotiation conversation before Apr 14 auto-renew.

6. **MSP commitment slip — 2 missed delivery dates this quarter**
   Vendor performance check-in needed.

**Watch**

7. **Snowflake renewal — May 8, 30-day notice period**
   No action this week, but on the calendar for early April.

8. **CVE-2025-1844 — 4 hosts still on outdated Datadog agent**
   Patch the stragglers when next change window opens.

> *Where would you like to start? I can draft the PIR note, the
> phishing block + org brief, the secret-handling reminder, or the
> GitHub seat-reduction message.*

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

**Identifiers are preserved verbatim.** System names, ticket IDs,
hostnames, license keys (when redacted), and CVE numbers are presented
exactly as they appear in email — IT work depends on these being
right. The skills and agent never paraphrase technical identifiers.

**Security findings are signals.** A reported phishing attempt or a
suspicious login is something worth investigating — the output is
framed that way. Claude won't declare a breach has happened unless the
email evidence explicitly says so.

**Your data stays with iGPT.** The plugin doesn't pipe raw email to
Claude — only the structured answers iGPT extracts. Your inbox is
connected to iGPT through OAuth, not shared with the model. The
plugin will never ask you to paste passwords, API keys, or access
tokens into the conversation — even if a skill seems to require it.

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
2. **Find `igpt-it`.** In the iGPT marketplace, click into **igpt-it**
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
   language — *"any active incidents?"*, *"what licenses are coming
   up for renewal?"* — and the right skill or the agent picks up
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
/plugin install igpt-it@igpt-skills
```

The plugin ships its own `.mcp.json` so the MCP server is registered for
you. You'll be prompted for OAuth on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/`
and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## Folder structure

```
igpt-it/
├── .claude-plugin/plugin.json
├── .mcp.json
├── README.md
├── agents/
│   └── igpt-it.md
└── skills/
    ├── access-request-tracker/
    ├── change-request-log/
    ├── incident-tracker/
    ├── it-vendor-commitment-tracker/
    ├── license-renewal-tracker/
    └── security-alert-monitor/
```

Each skill folder contains a `SKILL.md` with the workflow (variables
collected from the user, the iGPT query, output schema).

---

## Customization

**Time windows are natural language.** Each skill asks how far back to
scan. "Last 30 days", "since the outage", "Q1 2026", "since the last
audit" — all fine. You don't need to type ISO dates.

**Add taxonomies your team already uses.** Each skill's output schema
has enums you can extend in the SKILL.md to fit how your team
classifies things — incident severity tiers, change classes, security
signal categories specific to your stack, vendor tiers, license
categories.

**Add a new skill.** Create a folder under `skills/` with a `SKILL.md`
that follows the project pattern (YAML frontmatter with `name`,
`description`, `metadata.version`; a workflow that queries iGPT against
your email; an output schema). For security-related skills, mirror the
care rule — outputs are signals, not conclusions; never request
credentials. Add the new skill to the agent's "Available skills"
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

**`incident-tracker`** — for "any active incidents":

```json
{
  "as_of": "2026-03-10",
  "incidents": [
    {
      "ticket_id": "INC-2841",
      "title": "Production database elevated latency",
      "system": "prod-db-primary",
      "severity": "P2",
      "first_reported": "2026-03-02",
      "days_open": 8,
      "status": "mitigated",
      "owner_team": "Database",
      "owner_name": "Lin",
      "root_cause_summary": "Query plan regression after Postgres minor-version upgrade",
      "mitigation_summary": "Query rewrite applied",
      "post_incident_review_scheduled": false,
      "recommended_action": "Schedule PIR (8 days past 3-day target)"
    },
    {
      "ticket_id": "INC-2867",
      "title": "Auth-service intermittent 500s",
      "system": "auth-service",
      "severity": "P2",
      "first_reported": "2026-03-07",
      "days_open": 3,
      "status": "monitoring",
      "owner_team": "Platform",
      "owner_name": "Marcus",
      "root_cause_summary": "Token cache eviction edge case during deployment",
      "mitigation_summary": "Hotfix deployed Mar 9",
      "recommended_action": "Confirm 48-hour clean window; close if no recurrence"
    }
  ],
  "open_count": 3,
  "needs_pir_count": 1,
  "summary": "3 incidents open. INC-2841 is past PIR target by 5 days."
}
```

**`security-alert-monitor`** — for "any security signals worth knowing
about":

```json
{
  "as_of": "2026-03-10",
  "signals": [
    {
      "category": "phishing",
      "severity": "moderate",
      "summary": "Same domain reported twice impersonating payroll provider",
      "indicator": "notify-payroll-update[.]com",
      "reported_by": ["Sarah K. (Mar 5)", "Tomás G. (Mar 9)"],
      "status": "open",
      "confirmed_breach": false,
      "recommended_action": "Block domain at email gateway; brief the org"
    },
    {
      "category": "suspicious_login",
      "severity": "moderate",
      "summary": "Geographically improbable login flagged by Okta",
      "user": "m.chen@",
      "reported_by": ["Okta admin alert (Mar 7)"],
      "status": "investigating",
      "user_confirmed_no_travel": true,
      "remediation_taken": "Token revocation and password reset",
      "confirmed_breach": false,
      "recommended_action": "Continue monitoring; standard incident workflow"
    },
    {
      "category": "vulnerability",
      "severity": "moderate",
      "summary": "Datadog agent CVE-2025-1844 disclosed",
      "indicator": "CVE-2025-1844",
      "fixed_version": "7.49.0",
      "hosts_outstanding": 4,
      "status": "partially_remediated",
      "recommended_action": "Patch remaining hosts at next change window"
    },
    {
      "category": "policy_violation",
      "severity": "moderate",
      "summary": "Apparent API key for staging-billing-service quoted inline in internal thread",
      "status": "open",
      "confirmed_breach": false,
      "recommended_action": "Rotate key today; brief team about secret handling"
    }
  ],
  "open_count": 4,
  "confirmed_breach_count": 0,
  "summary": "4 security signals worth attention. None confirmed as breaches; all warrant investigation."
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
