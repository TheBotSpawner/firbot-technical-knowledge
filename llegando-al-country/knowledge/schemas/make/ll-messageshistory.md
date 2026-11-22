---
title: "LL_MessagesHistory — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-006 — `LL_MessagesHistory`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-006` |
| Exact name | `LL_MessagesHistory` |
| Make Data Store ID | `38022` |
| Data structure | `My data structure` (ID `150742`, strict=false) |
| Records / size at inspection | 1 records / 243 bytes (max 2097152 bytes) |
| Criticality | Critical |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

Short-term conversation memory and concurrency flag store for Nexo. One record per message (inbound `Entrada` / outbound `Salida`) per user (`Cellphone_Number` = WhatsApp `wa_id`). The main scenario reads the user's records to (a) decide if a conversation is starting, (b) build the transcript sent to OpenAI (`Aggregate User/Bot Messages`), (c) detect admin mode (`Admin_Mode`) and (d) detect a message already being processed (`Is Currently Processing`). History is capped at ~10 records per user (`LimitReached` deletes the oldest when ≥11) and trimmed to the last messages after a search/recommendation completes. `Delete Messages` purges records older than ~3 h every 2 h.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `Name` | text | No | Nombre del usuario |
| `Cellphone_Number` | text | No | Numero de celular de la persona |
| `Message` | text | No | El mensaje  |
| `Timestamp` | date | No | Cuando se genero ese mensaje |
| `Direction` | text | No | Si es de entrada o salida |
| `Admin_Mode` | boolean | No | — |
| `Is Currently Processing` | boolean | No | With this we check if another message is processing right now |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Chatbot Recomendacion de Servicios` | `2505419` | Search, AddRecord (overwrite by key → set not-processing), Delete |
| `LL - Log Message` | `5421473` | AddRecord (when `SaveInDataStore`=true); returns key |
| `Sleep n Seconds` | `5892850` | Search (outbound messages in last n+2 s) |
| `LL - Buscar Servicio por Zona` | `2637743` | Search, AddRecord(overwrite), Delete (trim history) |
| `LL - Recomendar Servicio` | `2637777` | Search, Delete (keep last) |
| `LL - Admin Mode` | `4133823` | Search, AddRecord, Delete |
| `LL - Subscenario Special Interaction` | `5695064` | AddRecord(overwrite), Delete |
| `LL - RecMulti 5 Confirmar` | `6920183` | Search (limit 50), Delete (keep last) |
| `Delete Messages` | `2629639` | Search, Delete (>3 h old) |
| `Automation Testing (inactive)` | `4141246` | Delete |

## Relations, issues and notes

Key = auto-generated record key; logical key = `Cellphone_Number`. Mirrors (partially) Strapi `LL - WhatsApp Mensaje`, which is the durable log. Older blueprint metadata labels this store `CountryMagazineDataStore` (e.g. `Delete Messages` module restore label) — **conflict resolved: same vendor ID 38022; the label is stale metadata from a previous name.** Data structure name is the generic `My data structure` (ID 150742). `Delete Messages` parses `Timestamp` with format `YYYY-MM-DD HH:mm` while the live field type is `date` and writers store ISO/`YYYY-MM-DD HH:mm:ss` values — **Inference:** age computation may be unreliable; verify with an execution log.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
