---
title: "LL - WhatsApp Conversación — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# LL - WhatsApp Conversación — Visible UI Fields

- **Canonical Data ID:** `DATA-LTC-002`
- **Strapi API identifier (visible):** `wpp-conversacion`
- **Evidence:** screenshots of authenticated Strapi Content Manager, shared 2026-11-22.
- **Verification level:** **Confirmed from user-provided screenshot**, **not a complete schema**. Type labels are UI-derived/inferred where appropriate. Do not assume underlying DB/API field types, cardinality, nullability, permissions or field completeness.
- **Write policy:** May be read and written by Nexo according to requirements; exact endpoints/operations TODO.

## Fields seen in screenshots

| UI field/label | Apparent type | Note |
|---|---|---|
| `conversacionId` | Text | Required visible |
| `telefono` | Text | Required visible |
| `usuario` | Relation | Visible in UI; actual schema TODO |
| `recomendacion` | Relation | Visible in UI; actual schema TODO |
| `iniciada` | Datetime | Required visible |
| `ultimoMensaje` | Datetime | Visible in UI; actual schema TODO |
| `cantidadMensajes` | Number | Visible in UI; actual schema TODO |
| `varianteInicial` | Relation | Visible in UI; actual schema TODO |

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
