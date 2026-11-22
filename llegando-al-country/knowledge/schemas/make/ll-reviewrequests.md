---
title: "LL_ReviewRequests — Make Data Store schema"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
sources: "Make data-stores_list / data-structures_list (team 1163364) and scenario blueprints"
---

# SCHEMA-LTC-011 — `LL_ReviewRequests`

| Attribute | Value |
|---|---|
| Canonical data ID | `DATA-LTC-011` |
| Exact name | `LL_ReviewRequests` |
| Make Data Store ID | `123790` |
| Data structure | `Review Requests` (ID `441583`, strict=false) |
| Records / size at inspection | 12 records / 4782 bytes (max 1048576 bytes) |
| Criticality | Medium |
| Evidence | **Confirmed from live system**, 2026-11-22 |

## Purpose

State of 'did you contact the provider?' review requests. `LL - Pedido Review` (triggered by the website 'Contactar' button) creates a record with a unique `reviewRequestId` = `review_<serviceId>_<phone>_<unix ts>`, sent as quick-reply payload `review_yes|…` / `review_no|…`. When the user answers, `LL - Subscenario Special Interaction` (event `Contactar`) looks it up and updates `status`/`response`/`answeredAt`.

## Fields (data structure definition — no record data exported)

| Field | Type | Required | Help text in Make |
|---|---|---|---|
| `reviewRequestId` | text | Yes | — |
| `telefono` | text | Yes | — |
| `serviceId` | number | Yes | — |
| `serviceName` | text | No | — |
| `serviceSlug` | text | No | — |
| `postLink` | text | Yes | — |
| `category` | text | Yes | — |
| `createdAt` | date | No | — |
| `status` | text | No | — |
| `answeredAt` | date | No | — |
| `response` | text | No | — |

## Scenarios using this store

| Scenario | Make ID | Operations observed in blueprint |
|---|---|---|
| `LL - Pedido Review` | `5625466` | AddRecord (overwrite=true) |
| `LL - Subscenario Special Interaction` | `5695064` | Search, Update |

## Relations, issues and notes

`serviceId` references Strapi `servicios` (LL - Anuncios). No expiry/cleanup process observed. Contains phone numbers — Confidential.

## Related documents

- Registry: [`../../04_DATA_ASSETS_REGISTRY.md`](../../04_DATA_ASSETS_REGISTRY.md)
- Automations: [`../../automations/make/README.md`](../../automations/make/README.md)
