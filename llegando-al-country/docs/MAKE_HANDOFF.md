---
title: "Make and Claude Handoff"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# Make Inventory and Claude Handoff

## Handoff objective

Connect the correct **Llegando al Country** Make account and turn this *partial initial baseline* into a verified, maintainable map of the productive Nexo ecosystem. Inventory only — **not a development or production mutation request**.

## Proposed read-only sequence

1. Read `../CLAUDE.md`, all ten `../knowledge/0*.md` registries and this handoff.
2. Confirm Make organisation/team and that no other client's assets are in scope.
3. Discover all scenarios with IDs, exact names, folders, active status and trigger type. Reconcile the 12 initial automation IDs; preserve them when matched.
4. Read active main and child scenario configurations; map `CallSubscenario` edges, inputs/outputs, webhook routes, data store dependencies, endpoint methods, error handlers, and concurrency/idempotency.
5. Inventory each Data Store; preserve exact names and vendor IDs, record schemas and verify any obsolete/unused assets without deleting them.
6. Trace Strapi integrations and separate *reads* from *writes*. **LL - Anuncios remains read-only** according to stakeholder and should not be modified to "test" assumptions.
7. Redact/review all export artifacts. Document source, timestamp, hashes, exact scope and sanitisation status in `../exports/make/manifest.md`.
8. Update `03_AUTOMATION_REGISTRY.md`, `04_DATA_ASSETS_REGISTRY.md`, focused files under `knowledge/automations/make/` and `knowledge/schemas/`, gaps and checklists. Do not mark an export as identical to live until compared.
9. Present a reconciliation report listing verified findings, unknowns, conflicts, security issues and next recommended documents.

## Requested outputs per scenario

- Stable canonical ID, exact Make name, Make scenario ID, active state, folder and owner.
- Trigger/webhook/schedule, inputs, outputs, dependencies, connected services and data.
- Business purpose, routing summary, logging, error handling, retry/rollback/manual recovery.
- Sensitive-data treatment, known limitations, source references and last verification date.
- Diagram or subscenario call graph where it improves troubleshooting.

## Practical separation

- Keep current state in this repo. Create proposed architecture fixes, new scenarios or major refactors in sibling **`automations-development/`** only when that workspace exists and a change request is authorised.
- If any access level allows edits, **do not use mutating operations** during inventory. Never run scenario execution or test production messages without explicit approval.
