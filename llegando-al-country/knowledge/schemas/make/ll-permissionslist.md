---
title: "LL_PermissionsList — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-009 — `LL_PermissionsList`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-009` |
| Exact name | `LL_PermissionsList` |
| Make Data Store ID | `76312` |
| Data structure | `Llegando Admin Phones` (ID `280435`, strict=false) |
| Records / size at inspection | 5 records / 594 bytes (max 1048576 bytes) |
| Criticality | High |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Allow-list of WhatsApp numbers authorised to enter **Admin Mode** by sending `#adminmode`. The main scenario searches `Phone Number` = sender `wa_id`; if found, `LL - Admin Mode` is called, otherwise a 'not authorised' message is sent.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `Name` | text | Yes | — |
| `Phone Number` | text | Yes | — |
| `Role` | text | No | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Chatbot Recomendacion de Servicios` | `2505419` | Search (read-only) |

## Relations, issues and notes

No Make scenario writes to it: records are maintained manually in the Make UI (**Inference**). 5 records at inspection (contents not exported). Security-relevant: anyone in this list can trigger mass welcome-template sends via Admin Mode.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
