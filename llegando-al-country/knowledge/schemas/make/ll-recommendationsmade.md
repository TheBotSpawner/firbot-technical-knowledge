---
title: "LL_RecommendationsMade — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-010 — `LL_RecommendationsMade`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-010` |
| Exact name | `LL_RecommendationsMade` |
| Make Data Store ID | `80766` |
| Data structure | `Recommendation Contact` (ID `295935`, strict=false) |
| Records / size at inspection | 285 records / 44223 bytes (max 1048576 bytes) |
| Criticality | High |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Idempotency/de-duplication register of providers already contacted after being recommended. `LL - Envio de Mensaje Recomendado` searches `Phone Number` (normalised, `contains`) before sending the recommendation template and adds a record afterwards (`Messages Sent`=1, `Last Contact Timestamp`).

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `Contact Name` | text | No | Nombre del contacto |
| `Phone Number` | text | Yes | Numero de telefono del contacto |
| `Last Contact Timestamp` | date | No | Horario en el que se envio el ultimo mensaje al usuario contactado  |
| `Messages Sent` | number | Yes | Cantidad de mensajes enviados al usuario recomendado |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Envio de Mensaje Recomendado` | `4222809` | Search, AddRecord |
| `LL - Envio de Mensaje Recomendados Previos` | `4227025` | Search (sorted by Last Contact Timestamp; result not used further) |
| `Automation Testing (inactive)` | `4141246` | Search |

## Relations, issues and notes

Largest store (285 records). Overlaps with Strapi `LL - Recomendaciones de servicios.mensajesEnviados` which is also set to 1 by the same scenario — two sources of truth for 'already contacted'. Contains provider names and phones — Confidential.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
