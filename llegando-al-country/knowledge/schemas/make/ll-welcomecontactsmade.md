---
title: "LL_WelcomeContactsMade — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-013 — `LL_WelcomeContactsMade`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-013` |
| Exact name | `LL_WelcomeContactsMade` |
| Make Data Store ID | `76313` |
| Data structure | `Llegando Welcome Contacts Made` (ID `280440`, strict=false) |
| Records / size at inspection | 9 records / 1200 bytes (max 1048576 bytes) |
| Criticality | Medium |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Queue + register for the Admin-Mode 'welcome message' campaign. Admins send contacts to Nexo; `LL - Agregar Contactos de Bienvenida` adds them (`Contact Done`=false) if not already present; `LL - Enviar Bienvenida` sends template `llegando_first_message_v2` to every pending record and sets `Contact Done`=true.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `Contact Name` | text | No | — |
| `Phone Number` | text | Yes | — |
| `Contact Timestamp` | date | No | — |
| `Contact Done` | boolean | No | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Agregar Contactos de Bienvenida` | `4199053` | Search, AddRecord |
| `LL - Enviar Bienvenida` | `4137315` | Search (Contact Done ≠ true), Update |

## Relations, issues and notes

De-duplication is by exact `Phone Number` text match (no normalisation). Contains third-party names/phones — Confidential.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
