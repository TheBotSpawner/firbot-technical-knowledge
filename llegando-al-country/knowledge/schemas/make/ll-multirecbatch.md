---
title: "LL_MultiRecBatch — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-007 — `LL_MultiRecBatch`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-007` |
| Exact name | `LL_MultiRecBatch` |
| Make Data Store ID | `193870` |
| Data structure | `LL_MultiRecBatch` (ID `568877`, strict=false) |
| Records / size at inspection | 0 records / 0 bytes (max 1048576 bytes) |
| Criticality | High |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Pending 'multiple recommendation' tray per WhatsApp user (key = `wa_id`). Holds the list of contacts sent (`contacts` JSON `{items:[{n,t,s}]}` = name, phone, service), the conversation status (`await_zone` / `await_confirm`), selected neighbourhood and timestamps. A tray is considered active for 2 h after `updated_at`.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `wa_id` | text | No | — |
| `user_name` | text | No | — |
| `status` | text | No | await_zone / await_confirm |
| `contacts` | text | No | JSON: {items:[{n,t,s}]} |
| `zone_name` | text | No | — |
| `zone_id` | number | No | — |
| `created_at` | date | No | — |
| `updated_at` | date | No | — |
| `last_msg` | text | No | Último mensaje armado por el bot (debug/test) |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Chatbot Recomendacion de Servicios` | `2505419` | Search (is there an active tray?) |
| `LL - RecMulti 1 Recibir mensaje` | `6920256` | Search |
| `LL - RecMulti 2 Mostrar Resumen` | `6920153` | AddRecord overwrite (upsert tray) |
| `LL - RecMulti 3 Cancelar` | `6920171` | Delete (real) / Update (test mode) |
| `LL - RecMulti 5 Confirmar` | `6920183` | Delete (real) / Update (test mode) |

## Relations, issues and notes

`zone_id` is defined but not written by RecMulti 2 (zone ID is resolved again in RecMulti 5). Contains third-party phone numbers (recommended providers) — Confidential. Empty at inspection (records are deleted on confirm/cancel).

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
