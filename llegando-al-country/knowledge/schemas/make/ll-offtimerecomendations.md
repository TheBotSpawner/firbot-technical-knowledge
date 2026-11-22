---
title: "LL_OffTimeRecomendations — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-008 — `LL_OffTimeRecomendations`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-008` |
| Exact name | `LL_OffTimeRecomendations` |
| Make Data Store ID | `101658` |
| Data structure | `OffTimeRecomendations` (ID `377659`, strict=false) |
| Records / size at inspection | 0 records / 0 bytes (max 1048576 bytes) |
| Criticality | Medium |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Deferred-delivery queue for outbound template notifications that arrive outside the allowed contact window (Mon–Fri 18:00–22:00, Sat–Sun 10:00–22:00, Buenos Aires). Each record stores the original webhook `Payload` and the `WebhookToSend` (URL of the originating Make webhook). `LL - Send Template On Time` replays each payload to its webhook and deletes the record.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `Payload` | text | Yes | All data to send again the webhook |
| `WebhookToSend` | text | Yes | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Envio de Mensaje Recomendado` | `4222809` | AddRecord (off-time branch) |
| `LL - Anuncio Publicado` | `4378165` | AddRecord (off-time branch) |
| `LL - Nueva Opinion Anuncio` | `4469351` | AddRecord (off-time branch) |
| `LL - Nueva Visita Anuncio` | `4469369` | AddRecord (off-time branch) |
| `LL - Send Template On Time` | `5146890` | Stats, Search, Delete |
| `LL - Enviar Bienvenida` | `4137315` | Listed by Make as a usage, but the only reference is inside a disconnected (orphan) router — never executed |

## Relations, issues and notes

**Finding:** in 3 of the 4 producers (`4222809`, `4469351`, `4469369`) the time-window filter has an always-true OR group (`test = test`) and in `4378165` an always-true group (`Testing = Testing`), so the off-time branch is never reached; consistent with 0 records at inspection. `WebhookToSend` contains full webhook URLs (bearer-like secrets) — do not export records. Schema has only 2 fields; data structure `OffTimeRecomendation` (377666) is an unused duplicate.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
