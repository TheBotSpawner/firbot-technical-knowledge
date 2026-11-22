---
title: "LL - WhatsApp Mensaje — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# LL - WhatsApp Mensaje — Visible UI Fields

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

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
