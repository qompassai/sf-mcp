# sf-mcp — Salesforce Hosted MCP client for Neovim

A Neovim client module for Salesforce's Hosted MCP servers, written in Lua.

Salesforce hosts the MCP servers; this module is the **client**. It connects
Neovim to the hosted servers over Streamable HTTP (MCP protocol
`2025-06-18`), lists their tools, and calls them as the signed-in Salesforce
user — SObject reads and writes, Flows, Apex invocable actions, Data 360,
Prompt Builder, and API discovery — without leaving the editor.

This is not an MCP server, and it does not spawn one: a remote hosted server
cannot be started locally, so the module speaks JSON-RPC over HTTPS directly
instead of the stdio transport used for local MCP servers.

By [Qompass AI](https://github.com/qompassai).

## Status

Built and validated as a module. **Org-side activation is not yet done:**
connecting it to a live org still requires the one-time Salesforce setup in
[SETUP.md](SETUP.md) — activating a hosted MCP server, creating an External
Client App with the `mcp_api` scope, completing the browser OAuth flow once,
and having Flex Credits available for the hosted servers. Nothing in this
repository has been run against a production org.

## How it works

- **Auth:** OAuth 2.0 + PKCE through a Salesforce **External Client App**
  (Connected Apps are rejected by the MCP gateway). JWT-based access tokens,
  refreshed automatically. The `client_id` and refresh token live in
  [`pass`](https://www.passwordstore.org/) (`salesforce/mcp-client-id`,
  `salesforce/mcp-refresh-token`); the module never stores a client secret
  and never logs a token.
- **Confirmation:** `:SfMcpCall` always asks for confirmation before
  executing a tool.
- **Bounds:** responses are capped at 8 MiB, HTTP calls time out at 30 s,
  and tool results are truncated for display.

## Known servers

| Key | Description |
|---|---|
| `api-catalog` | API discovery |
| `data-360` | Data 360 SQL-based analytics |
| `flows` | Trigger Salesforce Flows |
| `invocable-actions` | Invoke Apex invocable actions |
| `prompt-builder` | Prompt Builder templates |
| `sobject-all` | Full sObject read + write access |
| `sobject-deletes` | Delete records |
| `sobject-mutations` | Create and update records |
| `sobject-reads` | Read-only sObject access |

Server URLs are built as
`https://api.salesforce.com/platform/mcp/v1/[sandbox/]platform/<key>`.

## Install

Copy `lua/salesforce/` into your Neovim configuration's `lua/` directory,
then load the module and register the commands:

```lua
require('salesforce.mcp').setup()
```

## Commands

| Command | What it does |
|---|---|
| `:SfMcpServers` | List the known hosted servers |
| `:SfMcpSetup` | Show the one-time setup steps |
| `:SfMcpAuthStatus` | Show whether the `pass` entries are present (never their values) |
| `:SfMcpTools [server] [sandbox]` | List a server's tools (default `sobject-reads`) |
| `:SfMcpCall <server> <tool> [json-args] [sandbox]` | Call a tool, with confirmation |
| `:SfMcpForgetToken` | Clear the cached access token |

## Repository layout

- `lua/salesforce/mcp.lua` — the module (single file, no dependencies
  beyond Neovim and `curl`).
- `SETUP.md` — the one-time Salesforce org setup guide.
- `tris/` — TDS TRIS (Technology Request Information Sheet) submission
  materials for this integration: worksheet, checklist, and business case.

The module's working copy lives in the Diver Neovim configuration; this
repository is its standalone publication and submission face, and the two
can diverge.

## License

Apache-2.0. See [LICENSE](LICENSE).
