# Salesforce MCP integration — business use at TDS

**What it is.** A client module in the requestor's editor (Neovim) that connects to Salesforce's Hosted MCP servers, so org work — querying records, checking flows — can be done from the editor under hard guardrails: OAuth 2.0 with PKCE through an External Client App, every call executed as the signed-in user under Salesforce's own field-level security and sharing rules, a confirmation prompt before any call executes, and credentials held only in an encrypted store, never logged.

**Business case.** The integration replaces standing, broad API access with per-call, human-confirmed operations that inherit Salesforce's own permission model. It is submitted now so the pattern is reviewed before activation, not after.

**Status, stated plainly.** The module is built and validated, but the org-side activation (External Client App, server activation, Flex Credits) is not done.

*Draft, 2026-11-11. Not submitted.*
