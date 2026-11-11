# TRIS submission materials — Salesforce MCP integration

This folder holds the TDS TRIS (Technology Request Information Sheet) submission materials for the **Salesforce MCP integration** (the Neovim client module `salesforce/mcp.lua` for Salesforce's Hosted MCP servers), prepared 2026-11-11. The integration was submitted together with ONTrack, LightShow, Fathom, Versemend, and Niflheim in one combined email to DLT-IT TRIS Request; the combined package (the email text, the full six-product worksheet, and the source form/process documents) is kept in the requestor's submission records and is not published here.

**Placement note.** These materials live in the module's standalone public repository, [qompassai/sf-mcp](https://github.com/qompassai/sf-mcp), alongside the module source (`lua/salesforce/mcp.lua`). The module's working copy remains in the requestor's Neovim configuration repository (diver); this repository is its publication and submission face.

## Contents

- [WORKSHEET.md](WORKSHEET.md) — every requestor-facing TRIS form field for the integration, pre-filled from the submission evidence; open items are marked **[INPUT NEEDED]**.
- [CHECKLIST.md](CHECKLIST.md) — one line per TRIS requirement: where the answer is entered (form section and row, and the process step at which it is submitted) and its status, with links to the satisfying evidence in this folder.
- [BUSINESS-USE.md](BUSINESS-USE.md) — the business case at TDS: per-call, human-confirmed Salesforce org work from the editor, executed as the signed-in user under Salesforce's own permission model.

## Status

- Checklist: **41 completed · 8 pending** (requestor lines; the reviewer fields, form rows 66–91, are IT's and are listed separately in the checklist).
- The pending lines are the inputs only the requestor can supply — manager/PAT Manager/CoE Director names, the version to cite, the vendor product page, TDS-approved Salesforce tooling to name as related, Flex Credits entitlement/cost, and prior legal/procurement review of the Salesforce terms. See [CHECKLIST.md](CHECKLIST.md) for the exact list.
- The module is built and validated; org-side activation (External Client App, server activation, Flex Credits) is **not** done — the submission asks for the pattern to be reviewed before activation.
- Submission status: **DRAFT — prepared, not yet submitted.** After TRIS approval, a Procurement Engagement Request (PER) follows.

## Public-copy notes

- One employer-internal contact name that appears in the internal working worksheet (in the row 5 note) is redacted in these public copies; no answer is changed.
- Reviewer and approver fields (form rows 66–91) are listed in the checklist by role only, without personal names.
