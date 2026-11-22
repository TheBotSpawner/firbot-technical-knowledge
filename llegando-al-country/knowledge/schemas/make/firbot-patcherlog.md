---
title: "Firbot_PatcherLog — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-005 — `Firbot_PatcherLog`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-005` |
| Exact name | `Firbot_PatcherLog` |
| Make Data Store ID | `193874` |
| Data structure | `Firbot_PatcherLog` (ID `568881`, strict=false) |
| Records / size at inspection | 20 records / 22729 bytes (max 1048576 bytes) |
| Criticality | Tooling / obsolete candidate |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Diagnostic log for Firbot development tooling. Written by `Firbot - Blueprint Patcher` (result of each blueprint patch attempt: counts, dryRun, applied, statusCode, truncated response/probe) and by the temporary helper scenarios (`Firbot - Consulta Strapi (temporal)` stores up to 8,000 chars of a Strapi GET response in `probe`; `Firbot - Borrar registros de prueba (temporal)`; `Firbot - Buscar registros de prueba (temporal)`). **Not used by any Nexo production flow.**

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `scenarioId` | number | No | — |
| `dryRun` | boolean | No | — |
| `counts` | text | No | — |
| `applied` | boolean | No | — |
| `statusCode` | number | No | — |
| `response` | text | No | — |
| `probe` | text | No | — |
| `length` | number | No | — |
| `newLength` | number | No | — |
| `at` | date | No | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `Firbot - Blueprint Patcher` | `6919674` | AddRecord (create) |
| `Firbot - Consulta Strapi (temporal)` | `6920671` | AddRecord |
| `Firbot - Borrar registros de prueba (temporal)` | `6932098` | AddRecord |
| `Firbot - Buscar registros de prueba (temporal)` | `6933260` | AddRecord |

## Relations, issues and notes

No relation to production data. `probe` may contain fragments of live blueprints (including literal tokens present in those blueprints) or Strapi responses (personal data) — **treat records as sensitive**; candidate for purge once development tooling is retired.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
