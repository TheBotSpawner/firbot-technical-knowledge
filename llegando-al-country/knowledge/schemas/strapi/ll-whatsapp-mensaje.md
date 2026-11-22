---
title: "LL - WhatsApp Mensaje — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "UI fields from screenshots (partial); Make-observed fields confirmed from live blueprints 2026-11-22"
---

# SCHEMA-LTC-003 — LL - WhatsApp Mensaje — Visible UI Fields

- **Canonical Data ID:** `DATA-LTC-003`
- **Strapi API identifier (visible):** `wpp-mensaje`
- **Evidence:** screenshots of authenticated Strapi Content Manager, shared 2026-11-22.
- **Verification level:** **Confirmed from user-provided screenshot**, **not a complete schema**. Type labels are UI-derived/inferred where appropriate. Do not assume underlying DB/API field types, cardinality, nullability, permissions or field completeness.
- **Write policy:** May be read and written by Nexo according to requirements; exact endpoints/operations TODO.

## Fields seen in screenshots

| UI field/label | Apparent type | Note |
|---|---|---|
| `claveExterna` | Text | Required visible |
| `nombre` | Text | Visible in UI; actual schema TODO |
| `telefono` | Text | Required visible |
| `mensaje` | Long text | Visible in UI; actual schema TODO |
| `direccion` | Enum or select | Seen "saliente"; full choices TODO |
| `ocurridoEn` | Datetime | Required visible |
| `conversacionId` | Text | Visible in UI; actual schema TODO |
| `recomendacion` | Relation | Visible in UI; actual schema TODO |
| `usuario` | Relation | Visible in UI; actual schema TODO |
| `servicio` | Relation | Visible in UI; actual schema TODO |
| `variante` | Relation | Visible in UI; actual schema TODO |
| `metadata` | JSON | Visible in UI; actual schema TODO |
| `vistoEn` | Datetime | Visible in UI; actual schema TODO |

## Fields observed in Make (exact API keys) — confirmed from live blueprints, 2026-11-22

Make does **not** create messages through the standard collection endpoint. All logging goes through the custom endpoint **`POST /api/wpp-bot/mensajes`** (auth header `X-Bot-Token`, literal value hard-coded) from `LL - Log Message` (5421473). Response keys: `guardados`, `errores`, `omitidos` (an error e-mail is sent if `errores ≥ 1` or `omitidos ≥ 1`).

| Request key (custom endpoint) | Source | Maps to (Inference) |
|---|---|---|
| `claveExterna` | WhatsApp message id (`wamid…`) — idempotency key | `claveExterna` |
| `telefono` | user/recipient wa_id | `telefono` |
| `mensaje` | text, emojis replaced by spaces | `mensaje` |
| `direccion` | `saliente` / `entrante` | `direccion` |
| `ocurridoEn` | WA unix timestamp or ISO now (UTC) | `ocurridoEn` |
| `esRecontacto` | always `false` | unknown |
| `nombre` (optional) | profile name | `nombre` |
| `varianteId` (optional) | template A/B variant id | `variante` relation |
| `recomendacionId` (optional) | Strapi recommendation id | `recomendacion` relation |
| `metadata` (optional, JSON) | `{flow, tipoMensaje, incomingMessageId, …}` | `metadata` |

Standard endpoint use: the main scenario (2505419, route *Non-Message*) handles WhatsApp **status** callbacks with `status = read`: `GET /api/wpp-mensajes?filters[claveExterna][$eq]=<status id>` then `PUT /api/wpp-mensajes/{id}` with `{ "vistoEn": <ISO UTC> }`.

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
