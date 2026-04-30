# CLAUDE.md

Notes for any Claude session working in this repo. Keep this short. If
something here is wrong, fix it — don't accumulate stale context.

## What this is

A Claude Code plugin marketplace for iGPT. The marketplace manifest is at
`.claude-plugin/marketplace.json`. Each plugin under `plugins/` bundles a
role-specific set of skills (sales, CS, finance, HR, etc.) that all
talk to the same backend MCP server: `https://mcp.igpt.ai/`. The marketplace
ships 13 plugins, 76 skills, and 13 agents (one per plugin) total at the
time of writing.

## Working branch

`dev`. `main` is the published branch — don't commit there directly. PRs
from `dev` → `main` happen on demand, not yet wired up.

## Conventions to follow

**SKILL.md YAML frontmatter** — single line for `name` and `description`,
plus a nested `metadata` block. No quotes:

```yaml
---
name: skill-name-matches-directory
description: One-paragraph trigger description. Inline quotes for trigger phrases like "what's open" are fine — no escaping needed since the value isn't quoted.
metadata:
  version: 1.0.0
---
```

Don't use folded multi-line descriptions (continuation lines are fragile;
one file got silently broken that way before). `version` is a string and
parses fine without quotes. Bump it when the skill's behavior changes.

**`.mcp.json` in every plugin** — exactly this shape, nothing more:

```json
{
  "mcpServers": {
    "igpt": {
      "type": "http",
      "url": "https://mcp.igpt.ai/"
    }
  }
}
```

No `description` field. `type` is `http`, not `url`.

**Prerequisites section in SKILL.md** — inline, not a remote fetch. Every
SKILL.md has a `## Prerequisites` block right after the H1 that tells Claude
what to do if the iGPT MCP isn't connected or auth fails. The block is
self-contained so a user who installs a single skill outside the plugin still
gets useful guidance. The full guard at `shared/mcp-guard.md` (canonical URL
in each block) is kept as a fallback for deeper troubleshooting only — not
fetched on every invocation.

If you change the inline block, change it across all 76 SKILL.md files in
one pass with a script. Don't drift.

**MCP tools available from `https://mcp.igpt.ai/`** — `ask` and `search`.
Pattern in most skills: `search` first to confirm data exists and narrow the
date range, then `ask` with a structured `output_format` schema for the
final answer. The `ask` tool takes two named arguments: `input` (the prompt
text) and `output_format` (the JSON schema). Use `input:`, never `prompt:`.

**Workflow section in SKILL.md** — every skill follows the same template:

1. **Step 1 collects user-supplied values.** No hardcoded numbers, dates,
   or scopes anywhere in tool calls. Each variable the skill needs is
   defined in step 1 with a default and a description; values come from
   the user. Derived variables (e.g. a clause that's empty when scope is
   "all") are also defined here so step 3's input stays clean.
2. **Step 2 calls search** with structured params. Variables are
   substituted into the params (e.g. date_from: ISO start date derived
   from [time_range]).
3. **Step 3 calls ask** with two arguments only: input and output_format.
   The input value is **only** the prompt template with [var] placeholders
   inline — no surrounding quotes, no meta instructions about substitution,
   no "where:" clauses, nothing else. When the skill runs, each [var] is
   replaced by the user's value and the resulting plain text is what gets
   sent.

**Placeholder syntax** — use `[var_name]`, not `{var_name}` and not
backtick-wrapped. Square brackets are the project standard. The brackets
are markers for substitution, not literal characters; they never appear in
the value sent to a tool.

**Time / date handling** — when a skill needs a date window, the variable
holds the user's natural-language phrasing ("the last 3 months", "May 2024",
"between Jan 1 and Mar 15", "since the kickoff"). Convert to ISO dates only
for the search call's `date_from` / `date_to`. For the ask input, use the
user's phrasing as-is. Don't ask the user for ISO dates; let them speak
naturally.

**Agents in `plugins/<plugin>/agents/`** — every plugin has exactly one
agent file at `plugins/<plugin>/agents/<plugin>.md` (the file name matches
the plugin directory). Auto-discovered by Claude Code; no path declaration
needed in `marketplace.json` or `plugin.json`. Each agent has YAML
frontmatter with `name`, `description`, `tools`, and `metadata.version`:

```yaml
---
name: igpt-<plugin>
description: When to invoke this agent — broad/cross-skill questions for this domain.
tools: mcp__igpt__ask, mcp__igpt__search
metadata:
  version: 1.0.0
---
```

`tools` is restricted to the iGPT MCP tools so the agent stays in its lane.
The body follows a consistent structure across all 13 agents: when-to-invoke
examples, a list of available skills with one-line summaries, decision
dimensions for choosing between skills, working-with-user guardrails
(defaults, natural-language dates, lead-with-the-punch-line, offer next
action), and the same inline Prerequisites block as SKILL.md. Each agent
also adds **domain-specific guardrails** that don't fit elsewhere — e.g.
"be precise about commercial terms" in finance / procurement, "candidate
names are sensitive" in recruiting, measured language for board /
fundraising contexts in executive. Keep those when editing.

When a skill is added to or removed from a plugin, update the agent's
"Available skills" list to match. The agent's body is a manual sync point;
nothing auto-generates it.

**Root `README.md`** — top-of-repo marketplace overview and the entry
point for first-time visitors. Different shape from per-plugin READMEs:
positioned to onboard both end users (the buyer) and builders /
integrators in one document.

Standard sections in order: title + tagline + badges, "What this is",
"Who it's for", "Quick start" (Cowork, Claude Desktop, Claude Code,
other MCP clients), "At a glance" (facts table + per-plugin overview
table), "Plugins" (one H3 per plugin with a skill table), "Architecture"
(skills / agents / plugins / marketplace as concepts), "How it works"
(the same pipeline diagram used in plugin READMEs), "Privacy and data
flow" (data stays with iGPT, OAuth, read-only, per-user, sensitive-
content rules summarized), "Repository structure" (tree), "Customization
and extending", "Conventions" (pointer to this file), "Versioning",
"Contributing", "Related", "License".

Rules for the root README:

- **Skill names in the per-plugin tables must match actual files.**
  When skills get renamed or added, update the root README's plugin
  tables to match. A previous version listed several skills that
  didn't exist — guard against that drift.
- **Plugin / skill / agent counts are surfaced at the top** (badges +
  at-a-glance table). That's where they need to be accurate. Per-
  plugin skill descriptions in the tables don't need to repeat
  counts.
- **Per-plugin READMEs are linked from the at-a-glance overview
  table** so anyone scanning the root can drill in.
- **Privacy and data flow gets its own section.** Enterprise buyers
  will read it. Cover: data stays with iGPT, OAuth not credentials,
  read-only, per-user authorization, plus a brief summary of plugin-
  level sensitive-content rules (candidate-name privacy in recruiting,
  measured language for executive contexts, etc.).

**Per-plugin README** — buyer-facing front door for the plugin. Speak to
the role (consultant, salesperson, recruiter), not to developers. The
shape is locked across all plugins; use `igpt-consulting/README.md` as
the reference template.

Standard sections in order: title + tagline + badges, "Why this exists",
"What you can ask", "A typical week", "The skills" (table), "The agent",
"What you see" (3–4 chat exchanges), "How it works" (pipeline diagram +
privacy note + domain-specific guardrails), "Install" (Cowork →
Desktop → Code → other), "Folder structure", "Customization",
collapsible "Output schemas", "Related", "License".

The **"How it works" section has two parts**: a universal block (pipeline
diagram + the standard "data stays with iGPT" privacy paragraph) followed
by 1–3 short paragraphs lifting the agent's domain-specific guardrails
into buyer-facing prose — e.g. "stage discipline + contrarian signals"
in sales, "facts vs. sentiment + faithful decision logs" in projects,
"voice is content + patterns over outliers" in marketing. Mirror what
the agent body already enforces; the README is just surfacing it for
the buyer.

Rules for README copy:

- **Don't hardcode plugin counts.** Say "all our role-specific plugins",
  not "all 13 plugins". Per-plugin skill counts in the badges line are
  fine since they're accurate to that plugin.
- **Tool-agnostic workflow phrasing.** No "search + ask", "search then
  ask", or other references to specific iGPT tool names — describe the
  workflow as "queries iGPT against your email". Skills may evolve.
- **No anti-JSON framing.** No "you never see JSON" / "you don't see
  it" — we also want developers using these. JSON examples live in a
  collapsible `<details>` block for integrators; just don't bash them.
- **Folder structure shows only plugin-defining files** —
  `.claude-plugin/plugin.json`, `.mcp.json`, `agents/`, `skills/`,
  `README.md`. Don't list `LICENSE.txt` or other generic boilerplate.
- **Flag skills that require a user-supplied input** in the skills
  table itself. Example: real estate's `client-offer-history` ends
  with "Requires a client name."; sales' `meeting-prep-briefing` ends
  with "Requires contact + company." This sets expectations before the
  user invokes the skill; the agent will also ask for the value before
  running.

**"What you see" pattern.** Each chat exchange starts with **You:**
*question* (lowercase, casual — how a user actually types), then
**Claude:** *(running `skill-name` — short description of what's
happening against email)*, then the rendered response with bold names,
dates, action notes, and a follow-up offer in italics block-quote.
Separate exchanges with `---`. No cute headers like "Monday morning
triage" above each — the question is the header. Include one
cross-skill example showing the agent in action (announced as *(the X
agent kicks in, running N skills in parallel...)*).

**Use realistic role-specific content.** Made-up but plausible
vendor names ("Atlas Studio", "Beacon Cloud"), candidate names with
sensitivity rules where relevant ("Sarah K." not "Sarah Kowalski"
in recruiting), real publication names where they fit ("Forbes",
"Nature Neuroscience"), real prospect dialogue. Generic placeholders
("Customer A", "$X") read as marketing fluff and undercut the engine
visibility the section is meant to convey.

**Cowork install — 5 steps.** Step 1 shows the marketplace search and
the GitHub URL (`igptai/skills` or `https://github.com/igptai/skills`)
as parallel options, not as a fallback. No preamble before step 1, no
apologetic "if you don't see it" framing on the GitHub option. Steps 2–5
walk through finding the plugin, installing, connecting email through
iGPT (one-time OAuth in a browser, mention read-only permissions and
that raw email stays with iGPT, only structured findings reach Claude),
and asking in plain language with 1–2 role-specific example questions.

## Repo quirks

The repo lives on a Windows filesystem mounted into the sandbox. Git
operations work but spew `Operation not permitted` warnings on
`.git/objects/tmp_obj_*` and occasionally fail to clear `.git/index.lock`
or `.git/HEAD.lock`. Workaround: `mv` the lock file out of the way (rename,
since `rm` fails on the mount), then retry. Commits go through correctly
despite the warnings — verify with `git log` after.

Note: the file tools (Read/Write/Edit) and bash sometimes see different
versions of a file mid-edit on this mount. If git can't see your changes
after editing through the file tools, rewrite the file via bash heredoc.

## Things to leave alone unless asked

- `name` field of any skill or agent (matches its directory / file;
  renaming breaks plugin discovery)
- The actual prose of skill descriptions — they're tuned for triggering
- The domain-specific guardrails in agent bodies — they reflect deliberate
  per-domain choices (candidate-name sensitivity in recruiting, measured
  language for executive board / fundraising contexts, etc.)
- The root `README.md` structure (Quick start, At a glance, Architecture,
  Privacy and data flow) — visitor-facing, change deliberately
- The per-plugin README section order and "What you see" / "How it
  works" patterns — buyer-facing, change deliberately
- `shared/mcp-guard.md` — single source of truth for connectivity UX
- `marketplace.json` and the per-plugin `plugin.json` files — versioned
  metadata, change deliberately
