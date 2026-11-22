---
title: "Documentation Gaps"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# Documentation Gap Summary — Initial Baseline

| Priority | Gap / question | Why it matters | Recommended evidence |
|---|---|---|---|
| P0 | Raw main Make export contains embedded WhatsApp Bearer credentials | Credential exposure risk | Rotate/revoke affected token; inspect other scenario exports and current live HTTP headers securely |
| P0 | No separate test environment | Production-change regression risk | Agree test strategy, rollback procedure and controlled test data (in development workspace) |
| P1 | Main scenario live revision / actual ID not verified | Export may be stale | Inspect current Make scenario read-only, compare hashes/configuration safely |
| P1 | Child scenarios not inspected | Incomplete end-to-end dependencies | Inventory Make org/team and export/read each active scenario |
| P1 | Strapi API models not inspected | UI screenshots are not complete schemas | Read-only Strapi Content-Type Builder schema/export |
| P1 | Strapi access scopes and credential ownership unknown | Data integrity / security | Review permissions and service connections with client technical admin |
| P1 | Messaging retention, privacy and consent unknown | Personal data is handled | Client-approved policies and deletion/reporting responsibilities |
| P1 | Error alerts recipients, coverage and incident playbooks unknown | Reliability and business continuity | Inspect error-notification child and perform approved dry-run plan |
| P2 | Make Data Store 193870, 193869 mappings unknown | Incomplete architecture | Reconcile vendor IDs with connected Make stores |
| P2 | Data Store 38022 metadata aliases conflict | Unclear canonical mapping | Confirm exact current name / ID and past renames |
| P2 | Data Store schemas and active use not verified | Data model incomplete | Read-only Data Store structure inspection |
| P2 | AI models/prompts/output structures not documented | Hard to maintain and debug | Inspect module configs with sensitive content redacted |
| P2 | WABA/Meta app ownership and webhook configuration unknown | Recovery/change management | Meta account owner read-only verification |
| P2 | Commercial trial/paid subscription rules tentative | Avoid technical/billing misdocumentation | Client product owner confirmation; inspect authoritative billing logic |
| P2 | Roles, change approvals and support agreement undefined | Accountable operations | Business/technical owner confirmation |
| P2 | Exact Strapi hosting, dashboard implementation unknown | Operational handoff | Client technical team documentation |

**Current state vs proposals:** Paid maintenance, test environment and Claude-based automated refresh are **not** existing production capabilities. Proposals belong in the separate `automations-development` repository.
