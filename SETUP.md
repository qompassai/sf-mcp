# Salesforce Hosted MCP — Setup Guide

**Status: org-side setup required.** The Neovim module
(`lua/salesforce/mcp.lua`) is ready; it needs credentials to talk to. None
of the steps below are done yet for any org using this repository.

Time estimate: ~10 minutes of clicking + up to 30 minutes of Salesforce
propagation delay (their global API gateways are slow to pick up new
External Client Apps — this is normal).

---

## What you're building

```
Neovim ──HTTPS──> Salesforce Hosted MCP Server ──> your org's data
  │                        │
  │  OAuth 2.0 + PKCE      │  respects your user's
  │  (per-user, JWT tokens)│  field-level security
  └────────────────────────┘  and sharing rules
```

Salesforce hosts the MCP server. Your Neovim is the MCP client. Every tool
call runs as *you*, with *your* permissions. Nothing bypasses Salesforce
security.

**Cost note:** Hosted MCP Servers require Flex Credits — Salesforce bills
for server usage. Talk to your Salesforce AE or check Salesforce
Foundations to get started. There is no free tier for the hosted servers
themselves.

---

## Step 1: Enable and activate an MCP server (5 min)

1. Log in to your Salesforce org (sandbox recommended for testing).
2. **Setup → search "MCP Servers" → Salesforce Servers.**
3. Find the server you want and click **Activate**. Start with one:
   | Server | What it does | Start here? |
   |--------|--------------|-------------|
   | `sobject-reads` | Read-only record access | ✅ safest first |
   | `sobject-all` | Full read + write | after reads works |
   | `flows` | Trigger Flows | when you need automation |
   | `invocable-actions` | Call Apex invocable actions | for custom logic |
   | `data-360` | SQL analytics | for reporting |
4. Copy the **Server URL**. It looks like:
   - Sandbox: `https://api.salesforce.com/platform/mcp/v1/sandbox/platform/sobject-reads`
   - Production: `https://api.salesforce.com/platform/mcp/v1/platform/sobject-reads`
   (Drop `sandbox/` for production orgs.)

## Step 2: Create the External Client App (5 min)

⚠️ **Must be an External Client App. Connected Apps are REJECTED by the MCP
gateway** with "Invalid token". This is the #1 setup failure.

1. **Setup → External Client App Manager → New External Client App.**
2. Enable OAuth. Add these scopes (both required):
   - **Access MCP servers** (`mcp_api`)
   - **Perform requests at any time** (`refresh_token` / `offline_access`)
3. Security settings:
   - ✅ **Require Proof Key for Code Exchange (PKCE)**
   - ✅ **Issue JSON Web Token (JWT)-based access tokens for named users**
   - For this public-client flow: do **not** require client secret on refresh.
4. Callback URLs — register the one matching your OAuth helper. If you use
   a localhost helper script (see Step 3, Option A), register:
   - `http://localhost:8080/callback`
5. Click **Create**.
6. Open the app's detail page and copy the **Consumer Key**. This is your
   OAuth `client_id`. (There is no client secret in the PKCE public flow —
   that's the point of PKCE.)

**Then wait.** Salesforce's global gateways take up to 30 minutes to
propagate a new External Client App. If your first connection attempt fails
with `OAUTH_APPROVAL_ERROR_GENERIC` or "Invalid token", wait 10–15 minutes
and retry before assuming something is wrong.

## Step 3: One-time browser authorization (2 min)

You need to complete the OAuth authorization code flow once to get a
refresh token. Options:

**Option A — helper script (recommended).** Use a minimal PKCE OAuth
helper that:

1. Generates `code_verifier` + `code_challenge` (S256)
2. Prints the authorize URL — open it in your browser, log in, approve
3. Runs a localhost listener on :8080 for the redirect
4. Exchanges the code for tokens and prints the `refresh_token`

**Option B — use any MCP client that already does this** (Claude Code,
Cursor, Postman). Connect it to the same server URL + consumer key,
complete the browser login, then extract the refresh token from that
client's token store.

**Option C — `sf` CLI.** If your org is already authenticated in `sf`, you
can mint tokens — but `sf`'s tokens carry the `sfap_api` scope family, and
the MCP gateway **requires** `mcp_api`-scoped JWTs from an External Client
App. So Option C does NOT work for MCP. Use A or B.

## Step 4: Store secrets in `pass` (1 min)

```bash
pass insert salesforce/mcp-client-id      # paste the Consumer Key
pass insert salesforce/mcp-refresh-token  # paste the refresh token
```

Verify in Neovim:

```vim
:SfMcpAuthStatus
" client_id:     present in pass
" refresh_token: present in pass
```

## Step 5: Test

```vim
:SfMcpServers          " list known hosted servers
:SfMcpTools sobject-reads sandbox
" Tools on sobject-reads (sandbox) (N):
"   ...
```

Then a real call (you'll get a confirmation prompt first):

```vim
:SfMcpCall sobject-reads <tool-name> {"limit": 5} sandbox
```

---

## Troubleshooting

| Symptom | Cause | Fix |
|---------|-------|-----|
| "Invalid token" | Connected App instead of ECA, or wrong scopes | Recreate as External Client App with `mcp_api` scope |
| `OAUTH_APPROVAL_ERROR_GENERIC` | ECA not yet propagated | Wait 10–30 min, retry |
| Empty tool list | Server not activated | Setup → MCP Servers → Activate |
| 401 on refresh | Refresh token revoked or expired | Redo Step 3 |
| `pass entry not found` | Secrets not stored | Redo Step 4 |

## Security notes

- The refresh token in `pass` is the crown jewel — it grants org access as
  you. `pass` encrypts it with your GPG key. Never paste it into chat,
  logs, or files.
- The Neovim module never logs tokens. `:SfMcpAuthStatus` shows presence,
  not values.
- `:SfMcpCall` always asks for confirmation before executing a tool.
- All traffic is HTTPS to `api.salesforce.com`. No tokens touch disk
  outside `pass` and the in-memory cache (cleared with
  `:SfMcpForgetToken`).
