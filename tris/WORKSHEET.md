# Salesforce MCP integration (Neovim client module for Salesforce Hosted MCP) — TRIS form-input worksheet

The requestor's working worksheet for this product's TRIS form (Technology Request Information Sheet): every requestor-facing field, pre-filled from the submission evidence wherever the evidence supports a value. Anything only the requestor can supply is marked **[INPUT NEEDED: …]** — nothing here is invented. Numbers in parentheses are the TRIS template's row numbers, so each line can be checked against the form and against [CHECKLIST.md](CHECKLIST.md).

This is one product's slice of the combined six-product submission worksheet prepared 2026-11-11 (ONTrack, LightShow, Fathom, Versemend, the Salesforce MCP integration, and Niflheim were submitted together in one email). IT reviewer fields (template rows 66–91) need no requestor input and are not listed here.

## Shared submitter fields (rows 3–6, repeated on all six forms)

- Requestor (3): Matt A. Porter — Field Service Technician (FST), matthew.porter@tdstelecom.com
- Requestor's Manager (4): [INPUT NEEDED: your manager's name]
- PAT Manager (5): [INPUT NEEDED: PAT Manager name — note: the process document names an Internal Employee Tools PAT contact as the AIR-access contact; that is not evidence he is the PAT Manager for this request]
- CoE Director (6): [INPUT NEEDED: CoE Director for the accountable Agile team — if left blank, the TRIS Administrator determines the accountable team, AM, and AD per the process document]

## Product answers

- Technology Name (8): Salesforce Hosted MCP integration — Neovim (diver) client module `salesforce/mcp.lua`, connecting to Salesforce's Hosted MCP servers.
- Technology Version (9): [INPUT NEEDED: version to cite — the client module is unversioned in the tree, and the hosted service's version is Salesforce-managed]
- Vendor Name (10): Salesforce (hosted MCP servers). The client module is the requestor's own code (Qompass AI).
- Website (11): [INPUT NEEDED: vendor website/product page to cite — the service endpoints are api.salesforce.com; no product page is in the package evidence]
- Description (14): A streamable-HTTP MCP client module in the Neovim editor (Tiger Style Lua) for Salesforce's Hosted MCP servers (record reads/writes, flows, invocable actions, Data 360 analytics). OAuth 2.0 + PKCE through an External Client App with the `mcp_api` scope; every tool call runs as the signed-in user under Salesforce's field-level security and sharing rules; the module prompts for confirmation before executing any call and never logs tokens.
- How used at TDS (15): Editor-based Salesforce org work — the requestor's Trailhead and org work (querying records, inspecting flows) — with per-call human confirmation instead of standing API access.
- Who will use it (16): Developers — initially the requestor only.
- Technology replaced/removed (17): Nothing. No TDS technology is removed.
- Direct customer impact (18): No direct customer-facing impact — an internal org-work tool.
- Supported internally or by vendor (19): The hosted servers are Salesforce's service; the client module is supported internally by the requestor.
- Production or test/development (20): Test/development at this time. Status, honestly: the client module is built and validated, but org-side activation has NOT been completed — it requires an External Client App with the `mcp_api` scope (Connected Apps are rejected by the MCP gateway), activation of a hosted server in the org, a one-time browser OAuth authorization, credentials stored in `pass`, and Flex Credits. Production org use only after activation and this review.
- Impact if discontinued (21): None — no system depends on it; org work reverts to the Salesforce UI and the sf CLI.
- Backout plan/cost (22): Delete the client module from the editor configuration, delete the stored credentials from `pass`, and deactivate/delete the External Client App in the org. Cost: minutes.
- Similar technologies at TDS (23): [INPUT NEEDED: TDS-approved Salesforce tooling to name as related — in the requestor's own use, the sf CLI is the incumbent tool; note the sf CLI's tokens do not carry the mcp_api scope and cannot drive the hosted MCP gateway]
- Alternatives considered (24): The sf CLI alone (cannot provide MCP access — wrong token scope family); general MCP clients (Claude Code, Cursor, Postman) for the authorization step. The Neovim module is requested because the editor is the requestor's working environment and the module enforces confirmation-before-execution.
- AI component (26): Yes — an MCP client exists so AI assistants can call tools through it. It contains no model of its own; AI Policy 710 should be treated as applicable.
- Internet access (28): Yes — outbound HTTPS to api.salesforce.com (Salesforce Hosted MCP servers).
- Hosted internal/external (29): External — Salesforce hosts the MCP servers and processes org data under the org's existing Salesforce agreements. The client module runs on the requestor's workstation.
- Uploads data outside the Enterprise network (30): Yes — tool-call requests (queries and record operations) are sent to Salesforce's hosted servers, i.e., to the org's own Salesforce cloud. No other third party receives data.
- Inbound access to the Enterprise network (31): No — outbound connections only. (The one-time OAuth callback is a localhost listener on the client machine.)
- Data collected (32): Salesforce org records the user queries, bounded by that user's own permissions (Salesforce enforces field-level security and sharing). Credentials: the OAuth refresh token is stored only in an encrypted password store (pass/GPG); the module displays credential presence, never values, and never logs tokens.
- Java required (33): No.
- Microsoft 365 integration (34): No.
- Security risk assessment required (35): Yes — requested. The integration holds an org credential (refresh token); the review should cover the token handling, the confirmation gate, and which orgs/scopes are in bounds.
- Cardholder/banking data (36): No cardholder or banking data is processed by the module itself.
- How licensed (38): Commercial — Salesforce hosted service, billed through Flex Credits (Salesforce bills for hosted MCP server usage; there is no free tier for the hosted servers). The client module is the requestor's own code with no separate license fee.
- License model (39): Consumption-based (Flex Credits), controlled by Salesforce.
- License fees and quantity (40): [INPUT NEEDED: Flex Credits entitlement/cost for the intended usage — quantity is the requestor's org-work usage; procurement runs through Salesforce]
- Support/maintenance fees (41): No separate support fee in evidence; the hosted service is Salesforce's.
- How long around (43): Client module built October 2026; the Hosted MCP servers are a current Salesforce offering.
- Governing License (45): Not open source — Salesforce commercial service terms govern the hosted servers; the client module is the requestor's own code.
- License previously reviewed by legal (46): [INPUT NEEDED: whether the Salesforce service terms / Flex Credits arrangement has prior TDS legal or procurement review]
- Distributed / external use (47): No external distribution of the client module.
- Modified by TDS (48): No — the client module is requestor-authored; TDS modification is not applicable.
- Directly impacts a product or service provided to customers (49): No — an internal org-work tool.
- Mobile — developer (51): Client module: the requestor. Hosted service: Salesforce. (The Mobile section is not applicable — this is a workstation editor module, not a mobile app.)
- Mobile — store certification (52): Not applicable.
- Mobile — platforms (53): Workstation (Neovim editor). Not a mobile platform application.
- Mobile — TDS fee / required for a TDS service (54): No fee charged by TDS; not required to use any TDS service.
- Mobile — confidential information (55): Yes — Salesforce org data accessed through it, and the OAuth refresh token (held only in the encrypted store; see row 32).
- Mobile — third-party code (56): The hosted service is Salesforce's own platform. The client module is the requestor's own Lua; no third-party libraries are in the module evidence.
- Mobile — user data collection language (57): No telemetry. The module never logs tokens and its auth-status command shows credential presence only.
- Mobile — development tools/SDKs (58): Neovim/Lua toolchain. No Apple/Google SDK code.
- Mobile — in-app purchase (59) / Apple push (60) / Game Center (61) / iCloud (62) / Passes (63) / Apple Maps (64): No.

---
*Worksheet slice prepared 2026-11-11 from the TRIS template and process documents and the submission package evidence. DRAFT — not yet submitted. See [README.md](README.md) for the status summary and the public-copy notes.*
