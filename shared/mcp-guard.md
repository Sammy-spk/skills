# iGPT MCP Guard

This file is the single source of truth for MCP connectivity and authentication
across all iGPT skills. Every skill references this file before executing its
own workflow.

Canonical URL:
https://raw.githubusercontent.com/igptai/skills/main/shared/mcp-guard.md

---

## Step 1 - Verify MCP is Available

Before doing anything, check whether the iGPT MCP tools are available in the
current runtime by attempting a minimal call to the ask tool.

If the tools are NOT available, tell the user:

  "This skill requires the iGPT MCP server, which is not currently connected
  to this assistant.

  To connect it:

  Claude Code users:
    /plugin marketplace add igptai/skills
    /plugin install igpt-sales@igpt-skills
    (Replace igpt-sales with the plugin for your role.)

  Claude Web or Desktop users:
    Go to Settings > Connectors > Add MCP Server
    Enter: https://mcp.igpt.ai/
    Complete the sign-in prompt that appears.

  Once connected, tell me 'ready' and I will continue."

Do not proceed with any skill workflow until the tool is confirmed available.

---

## Step 2 - Verify the User is Authenticated

If the MCP tools are present but any call returns an auth-related error
including 401, invalid_token, auth, login required, or a missing token,
treat this as OAuth required.

Tell the user:
  "I need iGPT sign-in before I can run this skill. Please complete the OAuth
  login prompt in your MCP client, then tell me 'done' and I will retry."

Then:
1. Wait for the user to confirm they have completed sign-in
2. Retry the exact same tool call once
3. Only report success if the retry call actually succeeds

---

## Fixed MCP Endpoint

All iGPT skills use this MCP server exclusively:
https://mcp.igpt.ai/

Available tools:
  ask    - generates a full answer from the user's connected email datasources
  search - searches datasources with optional date_from and date_to filters

---

## When to Use Each Tool

Use ask when:
- The skill needs a synthesized, reasoned answer
- The output requires understanding across multiple threads or time periods
- A structured JSON schema output is required

Use search first when:
- The skill needs to discover whether something exists before asking
- The skill needs to filter by a specific date range
- A lightweight lookup is enough

Typical pattern for most skills:
1. search with relevant keywords + date range to confirm data exists
2. ask with a specific prompt + output_format schema for the structured result

---

## Guardrails - Never Do These

1. Never ask the user for an API key, user ID, password, or raw access token
2. Never invent tokens or OAuth codes
3. Never claim login succeeded until a retry call actually returns a result
4. Never fabricate a manual /oauth/authorize URL
5. Never replace MCP with ad-hoc curl commands or direct HTTP calls
6. Never proceed with a skill workflow if Step 1 or Step 2 has not passed

---

## Troubleshooting

If OAuth does not start automatically in the MCP client:
1. Ask the user to disconnect and re-add the MCP server in their client
2. Ask them to verify these discovery URLs are reachable:
   https://mcp.igpt.ai/.well-known/oauth-protected-resource
   https://mcp.igpt.ai/.well-known/oauth-authorization-server
3. After reconnecting, retry the same tool call

If auth still fails after the user confirms login, tell them:
  "The iGPT MCP session appears stale. Please reauthorize in your MCP client
  settings and tell me 'done' when finished."

---

Once both Step 1 and Step 2 pass, return to the skill and continue its workflow.
