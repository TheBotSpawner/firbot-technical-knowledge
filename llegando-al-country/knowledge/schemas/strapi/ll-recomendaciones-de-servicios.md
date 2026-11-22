---
title: "LL - Recomendaciones de servicios — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# LL - Recomendaciones de servicios — Visible UI Fields

- **Canonical Data ID:** `DATA-LTC-001`
- **Strapi API identifier (visible):** `recomendacion-servicio`
- **Evidence:** screenshots of authenticated Strapi Content Manager, shared 2026-11-22.
- **Verification level:** **Confirmed from user-provided screenshot**, **not a complete schema**. Type labels are UI-derived/inferred where appropriate. Do not assume underlying DB/API field types, cardinality, nullability, permissions or field completeness.
- **Write policy:** May be read and written by Nexo according to requirements; exact endpoints/operations TODO.

## Fields seen in screenshots

| UI field/label | Apparent type | Note |
|---|---|---|
| `Nombre del prestador del servicio` | Text | Required visible |
| `Teléfono del servicio` | Text | Required visible |
| `Barrio donde se realizó el servicio` | Relation | Visible in UI; actual schema TODO |
| `Categoría del servicio` | Relation | Visible in UI; actual schema TODO |
| `Mensaje enviado` | Boolean | Visible in UI; actual schema TODO |
| `Enviar aviso de recomendación al prestador` | UI action | Not an ordinary field |
| `Cupón generado para el prestador del servicio` | Relation | Visible in UI; actual schema TODO |
| `Opinión generada` | Relation | Visible in UI; actual schema TODO |
| `Nombre del cliente` | Text | Visible in UI; actual schema TODO |
| `Email del cliente` | Text | Visible in UI; actual schema TODO |
| `Barrio del cliente` | Text | Required visible |
| `Observaciones` | Long text | Visible in UI; actual schema TODO |
| `Fecha de próximo contacto` | Date | Visible in UI; actual schema TODO |
| `Anuncio creado` | Relation | Visible in UI; actual schema TODO |
| `observacion` | Long text | Visible in UI; actual schema TODO |
| `Recomendadores` | JSON-like field | Contains identifying information; never include real samples |
| `mensajesEnviados` | Not verified | Visible below fold or in listing; inspect schema |

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
