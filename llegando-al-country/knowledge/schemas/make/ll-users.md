---
title: "LL_Users — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-012 — `LL_Users`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-012` |
| Exact name | `LL_Users` |
| Make Data Store ID | `193869` |
| Data structure | `LL_Users` (ID `568876`, strict=false) |
| Records / size at inspection | 2 records / 411 bytes (max 1048576 bytes) |
| Criticality | Medium |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Per-user profile memory (key = `wa_id`): last neighbourhood used when recommending (`barrio`, `barrio_id` from Strapi `barrios-agenda`) and origin (`recomendacion_simple` / `recomendacion_multiple`). Used by RecMulti 1 to pre-fill the neighbourhood of a new multiple recommendation.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `wa_id` | text | No | Número de WhatsApp del usuario |
| `nombre` | text | No | — |
| `barrio` | text | No | Último barrio usado al recomendar (nombre normalizado de Strapi) |
| `barrio_id` | number | No | ID del barrio en Strapi (barrios-agenda) |
| `origen` | text | No | recomendacion_simple / recomendacion_multiple |
| `updated_at` | date | No | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Chatbot Recomendacion de Servicios` | `2505419` | Update (upsert) after a single recommendation with exact zone |
| `LL - RecMulti 1 Recibir mensaje` | `6920256` | Search |
| `LL - RecMulti 5 Confirmar` | `6920183` | Update (upsert) |

## Relations, issues and notes

Created 2026-11-05 together with the RecMulti family. Not related to Strapi `LL - Usuarios` (different concept). 2 records at inspection.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
