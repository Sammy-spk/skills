# iGPT Skills

> **Email intelligence for every role in the company.** A Claude Code plugin marketplace that turns the email already in your inbox into structured, queryable insight — by role, by skill, in plain language.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Plugins](https://img.shields.io/badge/plugins-13-green.svg)
![Skills](https://img.shields.io/badge/skills-76-orange.svg)
![Agents](https://img.shields.io/badge/agents-13-purple.svg)
![MCP](https://img.shields.io/badge/MCP-Streamable_HTTP-7b61ff.svg)

13 role-specific plugins · 76 focused skills · 13 agents · all powered by the iGPT MCP at `https://mcp.igpt.ai/`.

---

## What this is

iGPT Skills is a marketplace of Claude Code plugins that lets people ask plain-language questions about their email and get back grounded, structured answers — by role.

Each plugin targets a specific role (sales, finance, HR, ...) and ships:

- A tightly-scoped set of **skills** that each answer one focused question.
- An **agent** that handles broad, cross-skill questions and synthesizes a prioritized response.
- An **MCP configuration** that points at the iGPT backend at `https://mcp.igpt.ai/`.

A salesperson asking *"who's waiting on a reply from me?"*, a finance lead asking *"build me an expense report for May in USD"*, a researcher asking *"what grant deadlines are coming up?"*, or a CSM asking *"which customers should I be worried about?"* — the right skill picks itself up and returns a clean, ready-to-act answer grounded in their actual email threads.

---

## Who it's for

**End users.** Salespeople, customer success managers, finance leads, HR business partners, recruiters, executives, marketers, real estate agents, consultants, procurement leads, IT teams, researchers — anyone whose work runs through email.

**Builders and integrators.** Developers extending the plugins, customizing prompts and schemas, or integrating the iGPT API directly. Every skill's prompt and structured output schema is documented at the file level (`plugins/<plugin>/skills/<skill>/SKILL.md`) and reusable.

---

## Quick start

Install one of the plugins and connect your email through iGPT. That's the whole setup.

### Cowork (Claude desktop app)

1. Open the plugins section in Cowork. **Search the marketplace** for *iGPT*, or **add from GitHub**: paste `igptai/skills` (or the full URL `https://github.com/igptai/skills`).
2. Pick the plugin matching your role (e.g. `igpt-sales`).
3. Install. The first time you ask the plugin a question, you'll be prompted to sign in to iGPT (free account; OAuth in a browser; read-only email permissions).
4. Ask in plain language: *"who's waiting on a reply?"*, *"what grant deadlines are coming up?"*, *"any compliance flags I should know about?"*

### Claude Desktop

Settings → **Connectors** → **Add MCP Server** → enter `https://mcp.igpt.ai/` and complete OAuth.

### Claude Code

```bash
/plugin marketplace add igptai/skills
/plugin install igpt-sales@igpt-skills   # or any plugin name
```

The plugin ships its own `.mcp.json` so the MCP server is registered for you. OAuth happens on first use.

### Other MCP clients

Any Streamable-HTTP MCP client works. Point it at `https://mcp.igpt.ai/` and use the prompts and JSON schemas from each `SKILL.md` directly.

---

## At a glance

| | |
|---|---|
| Plugins | 13 |
| Skills | 76 |
| Agents | 13 (one per plugin) |
| Backend MCP | `https://mcp.igpt.ai/` |
| MCP transport | Streamable HTTP |
| Auth | OAuth (per user, read-only email) |
| License | MIT |

| Plugin | Skills | Focus |
|---|---|---|
| [`igpt-sales`](plugins/igpt-sales/) | 7 | Pipeline, deal friction, follow-ups, meeting prep |
| [`igpt-cs`](plugins/igpt-cs/) | 5 | Churn signals, escalations, renewals, advocacy |
| [`igpt-finance`](plugins/igpt-finance/) | 6 | Invoices, expenses, subscriptions, vendor spend |
| [`igpt-hr`](plugins/igpt-hr/) | 5 | Hiring pipeline, offers, onboarding, team friction |
| [`igpt-recruiting`](plugins/igpt-recruiting/) | 6 | External agencies, sourcing, alignment, declines |
| [`igpt-executive`](plugins/igpt-executive/) | 6 | Board updates, fundraising, investors, crisis signals |
| [`igpt-projects`](plugins/igpt-projects/) | 5 | Blockers, decisions, risks, milestones, actions |
| [`igpt-marketing`](plugins/igpt-marketing/) | 6 | Agencies, brand mentions, campaigns, partnerships, press |
| [`igpt-procurement`](plugins/igpt-procurement/) | 6 | Vendor risk, contract renewals, pricing history, POs |
| [`igpt-it`](plugins/igpt-it/) | 6 | Incidents, security alerts, license renewals, vendors |
| [`igpt-realestate`](plugins/igpt-realestate/) | 6 | Deal pipeline, client preferences, listings, vendors |
| [`igpt-consulting`](plugins/igpt-consulting/) | 6 | Deliverables, scope creep, retainer usage, proposals |
| [`igpt-research`](plugins/igpt-research/) | 6 | Grants, publications, collaborations, lab actions |

---

## Plugins

Every plugin has a dedicated `README.md` (linked above) with chat-style examples, a "How it works" pipeline, and hand-held install steps tuned to the role. The skill tables below give a one-line summary of what each skill solves.

### `igpt-sales` — Sales intelligence

For account executives, sales leaders, and BDRs working active deals.

| Skill | What it solves |
|---|---|
| `deal-open-items` | Every unresolved commitment, decision, and "I'll get back to you" across active deal threads |
| `deal-friction-detector` | Objections, hesitations, pricing friction, and stall signals on a specific deal |
| `cross-sell-upsell-signals` | Adjacent problems, budget hints, or expansion interest buried in existing customer email |
| `competitor-mentions` | Every mention of a competitor or alternative across accounts, with sentiment context |
| `follow-up-radar` | Threads waiting past silence thresholds — them on us, us on them, unanswered questions |
| `meeting-prep-briefing` | Pre-call brief on a contact at a company — history, open items, concerns, what they care about |
| `past-solutions-matcher` | Past customers who faced a similar problem — fuel for case-study moments in conversation |

### `igpt-cs` — Customer success intelligence

For CSMs, account managers, and customer success leaders.

| Skill | What it solves |
|---|---|
| `churn-signal-detector` | Early warning signals across accounts — dissatisfaction, competitor mentions, declining engagement |
| `renewal-readiness-checker` | Renewal sentiment, engagement, open issues, likely-to-renew vs. at-risk |
| `escalation-tracker` | Active escalations, SLA breaches, executive complaints, unresolved issues with growing severity |
| `success-story-miner` | Customer satisfaction moments, testimonial-worthy quotes, proof-point opportunities |
| `onboarding-gaps-detector` | Stalls and gaps in new-customer onboarding journeys; systemic onboarding issues |

### `igpt-finance` — Financial intelligence

For finance teams, controllers, bookkeepers, and anyone managing their own books.

| Skill | What it solves |
|---|---|
| `invoice-reconciliation` | Incoming invoices in a period, normalized to your local currency |
| `expense-report-builder` | Receipts and purchases over a period; supports grouping by project or client |
| `payment-status-tracker` | Match invoices against payment confirmations; flag overdue payables and receivables |
| `subscription-tracker` | Recurring SaaS and service subscriptions across a 13-month window; flags cancelled or stalled |
| `vendor-spend-analyzer` | Total spend per vendor, ranked, in your local currency |
| `tax-document-collector` | Tax-relevant documents (1099s, VAT invoices, official receipts) for a tax year and jurisdiction |

### `igpt-hr` — HR intelligence

For HR business partners, people leaders, and recruiters managing internal talent operations.

| Skill | What it solves |
|---|---|
| `candidate-pipeline-tracker` | Active candidates across open roles — current stage, last action, next step, where stalled |
| `offer-status-tracker` | Offers made, current status, negotiation points, expected start, offers outstanding too long |
| `onboarding-action-items` | Open onboarding tasks per new hire — access, equipment, paperwork, intros, training |
| `team-friction-detector` | Signals of tension, communication breakdowns, disengagement in internal threads |
| `policy-question-miner` | HR policy questions and benefits inquiries; what was answered, repeat questions, gaps |

### `igpt-recruiting` — Recruiting intelligence

For in-house recruiters, talent acquisition leaders, and external agency recruiters.

| Skill | What it solves |
|---|---|
| `interview-pipeline-tracker` | Every active candidate's stage, feedback received, who hasn't submitted feedback, where stalled |
| `agency-recruiter-tracker` | External agencies — roles worked, candidates submitted, fee arrangements, delivery patterns |
| `hiring-manager-alignment-checker` | Signals of misalignment — shifting criteria, slow feedback, inconsistent rejections |
| `job-requisition-status` | Open reqs — approval status, JD finalized, sourcing started, pipeline depth, stall signals |
| `offer-decline-analyzer` | Patterns across declined offers — reasons given, competing offers, comp signals |
| `sourcing-conversation-tracker` | Outbound prospect conversations — who responded, level of interest, where conversations went quiet |

### `igpt-executive` — Founder / CEO intelligence

For founders, CEOs, and senior leaders. Email is where the most important decisions, risks, and relationships live for an exec.

| Skill | What it solves |
|---|---|
| `board-update-builder` | Wins, decisions, risks, hires, financial signals, open asks — raw material for a board update |
| `crisis-signal-detector` | Early warning signals — legal threats, financial pressure, key-person flight risk, regulatory inquiries |
| `fundraising-thread-tracker` | Investor pipeline — stage, last contact, next step, signals of interest or pulling back |
| `investor-relationship-tracker` | Health of relationships with existing investors — tone, open asks, warm vs. cool |
| `key-relationship-health` | Health of key external relationships — customers, advisors, partners, senior contacts |
| `strategic-commitment-log` | Commitments made to investors, board, partners — what was promised, evidence of delivery |

### `igpt-projects` — Project & operations intelligence

For project managers, program managers, and operators running cross-functional initiatives.

| Skill | What it solves |
|---|---|
| `project-blocker-detector` | Blockers, unresolved dependencies, impediments — what's stuck, who owns resolving it |
| `decision-log` | Significant decisions made — what was decided, who decided, alternatives considered, conditions |
| `risk-radar` | Risk signals — timeline slippage, resource pressure, scope additions, stakeholder dissatisfaction |
| `stakeholder-action-tracker` | Action items assigned to specific stakeholders by project — status of each |
| `milestone-status-extractor` | Milestones and phases — target dates, current status, on-track / at-risk / delayed |

### `igpt-marketing` — Marketing & partnerships intelligence

For marketing leaders, brand managers, and growth operators.

| Skill | What it solves |
|---|---|
| `agency-deliverables-tracker` | Deliverables expected from creative agencies and freelancers — revisions, feedback loops, what's late |
| `brand-mention-sentiment` | External mentions of the brand by audience type; sentiment patterns; quotable lines |
| `campaign-feedback-miner` | Feedback and reactions on specific campaigns — internal stakeholders, partners, customers, agencies |
| `event-action-items` | Outstanding tasks across event lifecycles — logistics, vendors, speakers, sponsors, follow-up |
| `partnership-pipeline-tracker` | Partnership and BD conversations — stage, last contact, next step, open commitments |
| `press-coverage-tracker` | Coverage landed, pitches outstanding, journalist relationships, media opportunities |

### `igpt-procurement` — Procurement & vendor intelligence

For procurement teams, category managers, and operators handling vendor relationships.

| Skill | What it solves |
|---|---|
| `contract-renewal-radar` | Vendor contracts with renewal dates, notice periods, auto-renewals, renegotiation signals |
| `pricing-negotiation-history` | Full pricing conversation with a specific vendor — quotes, concessions, agreed rates, future commitments |
| `purchase-order-tracker` | POs in flight — supplier, amount, confirmation status, expected delivery, invoice received |
| `supplier-risk-signals` | Early warning patterns — financial pressure, capacity constraints, contact turnover, single-source |
| `vendor-commitment-tracker` | Promises vendors made (delivery dates, SLAs, price holds) — fulfilled vs. open |
| `vendor-escalation-log` | Escalations, complaints, unresolved issues, SLA breaches across the supplier base |

### `igpt-it` — IT & security intelligence

For IT teams, sysadmins, and IT managers.

| Skill | What it solves |
|---|---|
| `access-request-tracker` | Access and permission requests — approved, fulfilled, or stuck |
| `change-request-log` | System changes, deployments, infrastructure modifications — approval status, implemented or not |
| `incident-tracker` | Outages, system failures, unresolved technical issues — current status and ownership |
| `it-vendor-commitment-tracker` | IT vendor and MSP promises — SLAs, response times, patch schedules; fulfilled vs. open |
| `license-renewal-tracker` | Software licenses, SaaS subscriptions, IT contracts with renewal or expiry dates |
| `security-alert-monitor` | Phishing reports, suspicious logins, vulnerability disclosures, policy violations — signals to investigate |

### `igpt-realestate` — Real estate agent intelligence

For residential and commercial agents, brokers, and team leaders.

| Skill | What it solves |
|---|---|
| `deal-pipeline-tracker` | Active transactions — stage, key parties, next step, expected closing, blockers |
| `client-offer-history` | Reconstructs a specific client's full offer history — prices, counters, outcomes, seller feedback |
| `client-preference-miner` | Preferences a client has expressed — must-haves, deal-breakers, budget shifts, what's changed |
| `listing-expiry-tracker` | Listing agreements with expiry dates, notice periods, renewal / extension signals |
| `vendor-coordination-tracker` | Inspectors, appraisers, contractors, title, lender, attorney — what's confirmed, what's outstanding |
| `commission-agreement-tracker` | Commission, referral, and co-brokerage arrangements — rates, conditions, payment status |

### `igpt-consulting` — Consultant / freelancer intelligence

For independent consultants, boutique agencies, and consulting firms.

| Skill | What it solves |
|---|---|
| `client-deliverable-tracker` | Every deliverable across every client — promised, delivered, overdue, awaiting feedback, blocked |
| `scope-creep-detector` | Out-of-scope requests accepted without a change order, grouped by client with severity |
| `retainer-usage-tracker` | Retainer utilization, burn-rate signals, clients trending toward over- or under-using their hours |
| `proposal-follow-up-tracker` | Outstanding proposals — status, days pending, interest signals, gone-quiet flags |
| `client-feedback-collector` | Satisfaction signals, criticism, unactioned concerns; per-client overall sentiment |
| `reference-request-miner` | Reference / testimonial / case-study openings — both prospects asking and clients offering |

### `igpt-research` — Research & academia intelligence

For academic researchers, principal investigators, and research lab leaders.

| Skill | What it solves |
|---|---|
| `grant-deadline-tracker` | Grant applications and funding opportunities — submission deadlines, internal milestones, owner assignments |
| `publication-pipeline-tracker` | Manuscripts under submission or revision — stage, decisions, reviewer feedback, deadlines, co-author actions |
| `collaboration-commitment-tracker` | Commitments by you and by collaborators (data, analyses, drafts, reviews); separates your obligations from theirs |
| `data-source-tracker` | Data sources, datasets, access requests — approval status, agreements, blocking issues |
| `literature-tracker` | Papers, preprints, datasets shared in email — relevance to ongoing projects, follow-up actions expected |
| `research-action-items` | Action items assigned to lab members — analyses, experiments, code, writing, reviews |

---

## Architecture

Each plugin in this marketplace bundles four kinds of artifact, all auto-discovered by Claude Code from convention-based folder names.

### Skills

A **skill** is a single focused workflow: collect a few inputs from the user, query iGPT against their email, return a structured answer.

Each skill lives at `plugins/<plugin>/skills/<skill-name>/SKILL.md` and follows a consistent template:

1. **Step 1 — collect user-supplied values.** Variables like `[time_range]` and `[scope]` are defined with defaults and descriptions. The agent or skill asks the user for any value without a default.
2. **Step 2 — query iGPT** with structured parameters (search-style filtering by date range, keywords, scope).
3. **Step 3 — call the iGPT `ask` tool** with the user's variables substituted into a prompt template, and a strict JSON output schema.

Skills always return schema-validated JSON to the LLM, which is what produces the clean rendered chat response the user sees.

### Agents

An **agent** is a higher-level coordinator for a plugin. Each plugin ships exactly one agent at `plugins/<plugin>/agents/<plugin>.md` that handles broad, cross-skill questions ("walk me through what needs my attention this week") by routing to the right skills, running them in parallel, and synthesizing a prioritized response.

Agents also enforce **domain-specific guardrails**:

- Verbatim commercial terms in finance and procurement
- Patterns-not-judgments in HR and recruiting
- Stage discipline + contrarian signals in sales
- Faithful decision reconstruction in projects
- And so on across all 13

### Plugins

A **plugin** is a folder containing one set of skills, one agent, an `.mcp.json` for MCP server registration, and a `plugin.json` with metadata. Plugins are auto-discovered by Claude Code from the marketplace manifest.

### Marketplace

The **marketplace manifest** at `.claude-plugin/marketplace.json` lists all 13 plugins with their categories, keywords, and source paths.

---

## How it works

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

A plain-language question becomes the right query against your email, returns evidence-grounded structured findings, and gets rendered into a readable answer. You see the rendered answer in chat; integrators can also work with the structured output directly.

---

## Privacy and data flow

**Your email stays with iGPT.** The plugin doesn't pipe raw email to Claude. You connect your email account to iGPT through OAuth (read-only); iGPT processes the email on its side; only the structured findings — never the raw inbox — reach Claude.

**OAuth, not credentials.** No API keys, passwords, or access tokens are ever shared with the plugin or pasted into chat. Authentication happens through a standard OAuth flow in the browser.

**Read-only.** The iGPT MCP only reads from your connected email. The skills are designed for analysis and synthesis — they never send email on your behalf.

**Per-user authorization.** Each user installs and authorizes their own iGPT connection. Multi-user deployments preserve user-level access controls — no cross-user email leakage.

**Sensitive content care.** Several plugins enforce additional rules at the skill and agent layer:

- `igpt-recruiting`: candidate names handled as sensitive data; hiring manager performance described as patterns, not character judgments.
- `igpt-executive`: measured language for board / fundraising / settlement / compensation contexts; minimized raw quotation.

See each plugin's `README.md` for the full set of role-specific guardrails.

---

## Repository structure

```
iGPT-SKILLS-Building-Blocks/
│
├── .claude-plugin/
│   └── marketplace.json
│
├── shared/
│   └── mcp-guard.md
│
├── plugins/
│   │
│   ├── igpt-sales/
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json
│   │   ├── .mcp.json
│   │   ├── README.md
│   │   ├── agents/
│   │   │   └── igpt-sales.md
│   │   └── skills/
│   │       ├── competitor-mentions/SKILL.md
│   │       ├── cross-sell-upsell-signals/SKILL.md
│   │       ├── deal-friction-detector/SKILL.md
│   │       ├── deal-open-items/SKILL.md
│   │       ├── follow-up-radar/SKILL.md
│   │       ├── meeting-prep-briefing/SKILL.md
│   │       └── past-solutions-matcher/SKILL.md
│   │
│   ├── igpt-cs/
│   ├── igpt-finance/
│   ├── igpt-hr/
│   ├── igpt-recruiting/
│   ├── igpt-executive/
│   ├── igpt-projects/
│   ├── igpt-marketing/
│   ├── igpt-procurement/
│   ├── igpt-it/
│   ├── igpt-realestate/
│   ├── igpt-consulting/
│   └── igpt-research/
│       (each plugin follows the same structure as igpt-sales above)
│
├── CLAUDE.md          # Internal repo conventions for contributors
└── README.md          # This file
```

Each plugin folder contains exactly:

- `.claude-plugin/plugin.json` — plugin metadata (name, description, version, author, license)
- `.mcp.json` — MCP server registration (`type: "http"`, URL points to iGPT)
- `README.md` — buyer-facing front door with chat examples, install instructions, output schemas
- `agents/<plugin>.md` — the per-plugin agent
- `skills/<skill>/SKILL.md` — one folder per skill, each with the `[var]`-driven workflow

---

## Customization and extending

### Adjust an existing skill

Each `SKILL.md` is human-readable and self-contained. Edit the workflow's variable defaults, search keywords, prompt template, or output schema in place. The skill is ready to use as soon as the file is saved — no build step.

### Add a new skill

Create a folder under `plugins/<plugin>/skills/` with a `SKILL.md` that follows the project pattern:

- YAML frontmatter with `name`, `description`, `metadata.version`
- A 3-step workflow: collect user inputs (Step 1), query iGPT (Step 2), call `ask` with `input` and `output_format` (Step 3)
- An inline `## Prerequisites` block (the standard one used across the marketplace)

Then add the skill to the corresponding agent's "Available skills" list so the agent knows about it.

### Add a new plugin

Copy the structure of an existing plugin (e.g. `plugins/igpt-consulting/`), update `plugin.json`, write skills and one agent, and add an entry to `.claude-plugin/marketplace.json`.

### Use the prompts and schemas outside MCP

Every `SKILL.md` documents its prompt template and output schema in plain text. They work directly against the iGPT API without going through MCP — useful for backend integrations, batch processing, or custom UIs. See [`docs.igpt.ai`](https://docs.igpt.ai) for direct API docs.

---

## Conventions

This repository follows a small set of strict conventions documented in [`CLAUDE.md`](CLAUDE.md):

- `SKILL.md` YAML frontmatter — single-line `description`, nested `metadata.version`
- `.mcp.json` shape — `{type: "http", url: "https://mcp.igpt.ai/"}`, no extra fields
- Inline Prerequisites blocks — self-contained per skill, with the canonical `shared/mcp-guard.md` as fallback
- Workflow template — `[var]` placeholders, step-1 user input collection, step-3 `ask` with `input` only
- Per-plugin README pattern — practitioner-first voice, "What you can ask", "What you see", "How it works", install paths, collapsible JSON for developers
- Per-plugin agent — one per plugin at `agents/<plugin>.md` with domain-specific guardrails

Contributors should read `CLAUDE.md` before making structural changes.

---

## Versioning

Each `SKILL.md` and agent file carries a `metadata.version` field (currently `1.0.0` across all 76 skills and 13 agents). Bump the version when behavior changes meaningfully — output schema changes, prompt rewrites, default value shifts.

The marketplace itself follows semantic versioning at the plugin level (see each `plugin.json`).

---

## Contributing

Contributions are welcome. Please read [`CLAUDE.md`](CLAUDE.md) first — it documents the project conventions for skills, agents, READMEs, and `.mcp.json` configs. PRs that follow those conventions land faster.

A few specific notes:

- Don't hardcode plugin counts in plugin-level READMEs — say "all our role-specific plugins" so they don't go stale.
- Use the `[var]` placeholder convention in `SKILL.md` workflows. Hardcoded values inside `ask` prompts are a no-go.
- Domain-specific guardrails live at the agent body level. Surface them in plugin READMEs' "How it works" sections too.

---

## Related

- [iGPT website](https://igpt.ai) — sign up for the iGPT account that backs these plugins
- [iGPT API docs](https://docs.igpt.ai) — direct API reference for backend integrations
- [iGPT Python SDK](https://github.com/igptai/igptai-python) — `pip install igptai`
- [iGPT Node.js SDK](https://github.com/igptai/igptai-node) — `npm install igptai`
- [Playground](https://igpt.ai/hub/playground) — try queries interactively before writing code

---

## License

MIT
