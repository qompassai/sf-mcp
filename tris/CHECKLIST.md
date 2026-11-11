# Salesforce MCP integration — TRIS submission checklist

One line per requirement on the TRIS form (Technology Request Information Sheet) for this product's submission.

**Where each answer is entered.** Every requestor answer is entered on the TRIS form itself, in the section named in each heading below; row numbers are the TRIS template's. Under the TRIS Approval Process: the Requestor completes the form (step 1) and sends it to DLT-IT TRIS Request (step 2); the TRIS Administrator verifies completeness and routes it for initial approvals — IT Solution Architecture, Data Management, and Security Engineering — and then to the IT & DM&S Leadership Team; after full approval the Administrator creates the AIR entry and sends the final communication, and the Requestor submits a Procurement Engagement Request (PER).

**Status key.** **Completed** — the answer is in [WORKSHEET.md](WORKSHEET.md) or the cited evidence in this folder. **Pending** — waiting on the exact input named on the line; nothing is guessed. **IT** — a reviewer field (template rows 66–91), completed by IT; no requestor input.

**What is being submitted.** A Neovim (diver) client module, `salesforce/mcp.lua`, connecting to Salesforce's Hosted MCP servers. The vendor of record is Salesforce; the client module is the requestor's own code. Status: the module is built and validated, but org-side activation has **not** been completed — this submission asks for the pattern to be reviewed before activation.

## General — TRIS form, General section

- [x] **Row 3 — Requestor.** Completed — [WORKSHEET.md](WORKSHEET.md) (shared submitter fields).
- [ ] **Row 4 — Requestor's Manager.** Pending — input needed: your manager's name. Slot: [WORKSHEET.md](WORKSHEET.md) (shared submitter fields).
- [ ] **Row 5 — PAT Manager.** Pending — input needed: PAT Manager name. Slot: [WORKSHEET.md](WORKSHEET.md) (shared submitter fields).
- [ ] **Row 6 — CoE Director.** Pending — input needed: CoE Director for the accountable Agile team (if left blank, the TRIS Administrator determines the accountable team, AM, and AD per the process document). Slot: [WORKSHEET.md](WORKSHEET.md) (shared submitter fields).
- [x] **Row 8 — Technology Name.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [ ] **Row 9 — Technology Version.** Pending — input needed: the version to cite (the client module is unversioned in the tree; the hosted service's version is Salesforce-managed). Slot: [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 10 — Vendor Name.** Completed — Salesforce (hosted MCP servers); client module is the requestor's own code. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [ ] **Row 11 — Website.** Pending — input needed: the vendor website/product page to cite (the service endpoints are api.salesforce.com; no product page is in the package evidence). Slot: [WORKSHEET.md](WORKSHEET.md) (product answers).

## Technology Details — TRIS form, Technology Details section

- [x] **Row 14 — Description.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 15 — How used at TDS.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers); business case: [BUSINESS-USE.md](BUSINESS-USE.md).
- [x] **Row 16 — Who will use it.** Completed — developers; initially the requestor only. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 17 — Technology replaced/removed.** Completed — nothing is removed. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 18 — Direct customer impact.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 19 — Supported internally or by vendor.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 20 — Production or test/development.** Completed — test/development at this time; org-side activation not completed (External Client App with the `mcp_api` scope, server activation, one-time OAuth authorization, Flex Credits). Production org use only after activation and this review. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 21 — Impact if discontinued.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 22 — Backout plan/cost.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [ ] **Row 23 — Similar technologies at TDS.** Pending — input needed: TDS-approved Salesforce tooling to name as related (in the requestor's own use the sf CLI is the incumbent; its tokens do not carry the `mcp_api` scope and cannot drive the hosted MCP gateway). Slot: [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 24 — Alternatives considered.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).

## Technical Security — TRIS form, Technical Security section

- [x] **Row 26 — AI component.** Completed — yes; an MCP client exists so AI assistants can call tools through it. It contains no model of its own. [WORKSHEET.md](WORKSHEET.md) (product answers).
- **Row 27 — See AI Policy 710.** Template instruction row; applies — see the row 26 answer.
- [x] **Row 28 — Internet access.** Completed — yes; outbound HTTPS to api.salesforce.com. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 29 — Hosted internal/external.** Completed — external (Salesforce hosts the servers under the org's existing Salesforce agreements); the client module runs on the requestor's workstation. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 30 — Uploads data outside the Enterprise network.** Completed — yes; tool-call requests go to the org's own Salesforce cloud, no other third party. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 31 — Inbound access to the Enterprise network.** Completed — no; outbound only (the one-time OAuth callback is a localhost listener). [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 32 — Data collected.** Completed — Salesforce org records the user queries, bounded by that user's permissions (field-level security and sharing enforced by Salesforce); the OAuth refresh token is held only in an encrypted password store and never logged. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 33 — Java required.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 34 — Microsoft 365 integration.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 35 — Security risk assessment required.** Completed — yes; requested (token handling, the confirmation gate, and which orgs/scopes are in bounds). [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 36 — Cardholder/banking data.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).

## Licensing — TRIS form, Licensing section

- [x] **Row 38 — How licensed.** Completed — commercial: Salesforce hosted service billed through Flex Credits; the client module carries no separate license fee. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 39 — License model.** Completed — consumption-based (Flex Credits), controlled by Salesforce. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [ ] **Row 40 — License fees and quantity.** Pending — input needed: Flex Credits entitlement/cost for the intended usage (procurement runs through Salesforce). Slot: [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 41 — Support/maintenance fees.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 42 — Company's financial resources.** Completed — not applicable on this form: the vendor of record is Salesforce, not Qompass AI (see rows 10 and 38). [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 43 — How long around.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).

## Open Source — TRIS form, Open Source section

- [x] **Row 45 — Governing License.** Completed — not open source: Salesforce commercial service terms govern the hosted servers; the client module is the requestor's own code. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [ ] **Row 46 — License previously reviewed by legal.** Pending — input needed: whether the Salesforce service terms / Flex Credits arrangement has prior TDS legal or procurement review. Slot: [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 47 — Distributed / external use.** Completed — no external distribution of the client module. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 48 — Modified by TDS.** Completed — not applicable; the client module is requestor-authored. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 49 — Directly impacts a customer product/service.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).

## Mobile — TRIS form, Mobile section

- [x] **Row 51 — Developer.** Completed — client module: the requestor; hosted service: Salesforce. (The Mobile section is not applicable — this is a workstation editor module, not a mobile app.) [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 52 — Store certification.** Completed — not applicable. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 53 — Platforms.** Completed — workstation (Neovim editor). [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 54 — TDS fee / required for a TDS service.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 55 — Confidential information.** Completed — yes; Salesforce org data accessed through it, and the OAuth refresh token (held only in the encrypted store — row 32). [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 56 — Third-party code.** Completed — the hosted service is Salesforce's own platform; the client module is the requestor's own Lua with no third-party libraries in the module evidence. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 57 — User data collection language.** Completed — no telemetry; the module never logs tokens and its auth-status command shows credential presence only. [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Row 58 — Development tools/SDKs.** Completed — [WORKSHEET.md](WORKSHEET.md) (product answers).
- [x] **Rows 59–64 — Apple service rows** (in-app purchase, push notification, Game Center, iCloud, Passes, Maps). Completed — not a mobile app. [WORKSHEET.md](WORKSHEET.md) (product answers).

## Reviewer fields — TRIS form rows 66–91 (IT & DM&S use only; no requestor input)

- [ ] **Rows 68–70 — Security Engineering** (resource, review comments, recommendation). IT — completed by Security Engineering during initial approvals (process step: initial approvals, typically within 5 days).
- [ ] **Rows 72–74 — Data Management** (resource, review comments, recommendation). IT — completed by Data Management during initial approvals.
- [ ] **Rows 76–78 — Solution Architecture** (resource, review comments, recommendation). IT — completed by IT Solution Architecture during initial approvals.
- [ ] **Rows 81–89 — Leadership approvers.** IT — completed when the TRIS Administrator routes the request to the IT & DM&S Leadership Team (approval email carries Approve/Reject voting buttons, a link to the TRIS, and a 48-hour turnaround date).
- [ ] **Row 90 — Leadership review comments.** IT.
- [ ] **Row 91 — Leadership Team recommendation.** IT — on full approval the tracking entry moves to Completed, the Administrator creates the AIR entry and sends the final communication; the Requestor then submits the PER.

---
*Checklist prepared 2026-11-11 from the TRIS template and process documents, the combined submission worksheet, and the Salesforce MCP setup guide. DRAFT — not submitted.*
