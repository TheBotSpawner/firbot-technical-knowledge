---
title: "Naming and ID Conventions"
status: Draft
last_modified: 2026-11-22
verification: "Updated with live Make inventory 2026-11-22"
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
| Finding (risk/defect observed, not an incident) | `FIND-LTC-NNN` | `FIND-LTC-001` |

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

## Allocated ranges (2026-11-22)

| Type | Allocated | Notes |
|---|---|---|
| `SYS-LTC` | 001–009 | 007 Microsoft 365, 008 Google Drive, 009 Make API added |
| `AUTO-LTC` | 001–037 | 001–012 preserved from onboarding; 013–037 new |
| `DATA-LTC` | 001–022 | 014–018 Strapi collections/endpoints; 019 team variables; 020 webhooks; 021 Drive stickers; 022 WA templates |
| `SCHEMA-LTC` | 001–018 | Number = matching `DATA-LTC` number |
| `INC-LTC` | 001–003 | |
| `FIND-LTC` | 001–016 | |
| `ADR-LTC` | 001–011 | |
| `DOC-LTC` | 001–036 | see `09_DOCUMENT_REGISTRY.md` |

## Make naming conventions observed (descriptive, not normative)

- Production scenarios: prefix `LL - ` (Llegando). Exceptions: `Envio de Notificaciones de Error Chatbots`, `Sleep n Seconds`, `Delete Messages`, `Automation Testing`.
- Subscenario names: `LL - Subscenario …` (only 2), `LL - RecMulti N …` (numbered family).
- Firbot tooling: prefix `Firbot - `, suffix `(temporal)` for throw-away tools.
- Data Stores: `LL_<PascalCase>`; Firbot tooling store `Firbot_PatcherLog`. Spelling preserved: `LL_OffTimeRecomendations`.
- Webhooks: mixed styles (`WPP-Messages-Nexo-Webhook`, `NewPostOpinionStrapi`, `Onboarding-Paso-0N`). Webhook names do not always match purpose (`Codigo-Verificacion-WPP-Strapi` → ad published).
- In blueprints, subscenario references are written `SCN_<Make scenario ID>`; data stores by numeric ID; module labels may be stale (e.g. `CountryMagazineDataStore` = 38022).
- WhatsApp templates: `llegando_<purpose>[_variant]`, language `es_AR` (except `llegando_first_message_v2` → `en`).

## Canonical ↔ Make ID equivalences

| Canonical | Make | Canonical | Make | Canonical | Make |
|---|---|---|---|---|---|
| AUTO-LTC-001 | 2505419 | AUTO-LTC-014 | 4137315 | AUTO-LTC-027 | 6920171 |
| AUTO-LTC-002 | 2637689 | AUTO-LTC-015 | 4199053 | AUTO-LTC-028 | 6919980 |
| AUTO-LTC-003 | 2637692 | AUTO-LTC-016 | 4222809 | AUTO-LTC-029 | 6920183 |
| AUTO-LTC-004 | 2637743 | AUTO-LTC-017 | 4227025 | AUTO-LTC-030 | 6477190 |
| AUTO-LTC-005 | 2637777 | AUTO-LTC-018 | 4378165 | AUTO-LTC-031 | 4141246 |
| AUTO-LTC-006 | 4133823 | AUTO-LTC-019 | 4469351 | AUTO-LTC-032 | 6919674 |
| AUTO-LTC-007 | 4226818 | AUTO-LTC-020 | 4469369 | AUTO-LTC-033 | 6920671 |
| AUTO-LTC-008 | 5421473 | AUTO-LTC-021 | 5146890 | AUTO-LTC-034 | 6920717 |
| AUTO-LTC-009 | 5694920 | AUTO-LTC-022 | 5625466 | AUTO-LTC-035 | 6932098 |
| AUTO-LTC-010 | 5695064 | AUTO-LTC-023 | 5822771 | AUTO-LTC-036 | 6933016 |
| AUTO-LTC-011 | 5892850 | AUTO-LTC-024 | 5822780 | AUTO-LTC-037 | 6933260 |
| AUTO-LTC-012 | 6920256 | AUTO-LTC-025 | 5822785 | | |
| AUTO-LTC-013 | 2629639 | AUTO-LTC-026 | 6920153 | | |

| Canonical | Make Data Store ID | Canonical | Make Data Store ID |
|---|---|---|---|
| DATA-LTC-005 `Firbot_PatcherLog` | 193874 | DATA-LTC-010 `LL_RecommendationsMade` | 80766 |
| DATA-LTC-006 `LL_MessagesHistory` | 38022 | DATA-LTC-011 `LL_ReviewRequests` | 123790 |
| DATA-LTC-007 `LL_MultiRecBatch` | 193870 | DATA-LTC-012 `LL_Users` | 193869 |
| DATA-LTC-008 `LL_OffTimeRecomendations` | 101658 | DATA-LTC-013 `LL_WelcomeContactsMade` | 76313 |
| DATA-LTC-009 `LL_PermissionsList` | 76312 | | |

Export file naming: `<slug-of-exact-name>__<make-id>__<YYYY-MM-DD>.sanitized.json`.
