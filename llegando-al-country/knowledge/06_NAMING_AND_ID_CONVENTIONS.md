---
title: "Naming and ID Conventions"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 06 — Naming and ID Conventions

## Canonical IDs

| Type | Convention | Example |
|---|---|---|
| System | `SYS-LTC-NNN` | `SYS-LTC-001` |
| Automation | `AUTO-LTC-NNN` | `AUTO-LTC-001` |
| Reusable component | `COMP-LTC-NNN` | `COMP-LTC-001` |
| Data asset | `DATA-LTC-NNN` | `DATA-LTC-001` |
| Document | `DOC-LTC-NNN` | `DOC-LTC-001` |
| Schema | `SCHEMA-LTC-NNN` | `SCHEMA-LTC-001` |
| Incident | `INC-LTC-NNN` | `INC-LTC-001` |
| Decision | `ADR-LTC-NNN` | `ADR-LTC-001` |
| Playbook | `PLAYBOOK-LTC-NNN` | `PLAYBOOK-LTC-001` |
| Test record | `TEST-LTC-NNN` | `TEST-LTC-001` |

## Repository and file conventions

- Repository name: **`technical-knowledge`** when created in the client's workspace; ZIP package root is `technical-knowledge/` for straightforward repository initialisation.
- Client slug: **`llegando-al-country`**; internal ID domain `LTC` — initial recommendation, not an existing customer system identifier.
- File names: `lowercase-kebab-case.md`; base canonical indices remain `00_...md` to `09_...md` to follow the template.
- Canonical IDs are **stable, independent of Make `SCN_*` IDs and Strapi API IDs**, and never reused or renumbered for appearance.
- **Always preserve exact production spelling**, punctuation and accents in the corresponding record; this includes `LL_OffTimeRecomendations`, which is not silently corrected.
- Source evidence should capture inspected date, origin, vendor ID, export timestamp (if available), and verification status.
- Detail docs: `knowledge/automations/make/<slug>.md`, `knowledge/schemas/strapi/<slug>.md`, `knowledge/systems/<slug>.md`.
- New detailed docs should carry `status`, `last_modified`, `verification` and `sources` in YAML frontmatter when feasible.

## Production and versioning

- Do **not** rename production scenarios, stores, collections or fields for aesthetic reasons.
- Export names, sanitized versioning and timestamp guidelines: `exports/make/README.md`.
- Documentation updates only after verified system changes, not pending feature work.
- Initial IDs here are **reserved**; reconcile without creating duplicates after connecting Make.
