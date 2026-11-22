---
title: "LL - Recomendaciones de servicios — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "UI fields from screenshots (partial); Make-observed fields confirmed from live blueprints 2026-11-22"
---

# SCHEMA-LTC-001 — LL - Recomendaciones de servicios — Visible UI Fields

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

## Fields observed in Make (exact API keys) — confirmed from live blueprints, 2026-11-22

**REST endpoint:** `/api/recomendaciones-servicios`. Strapi model UID seen in webhook payloads: `ll-pre-servicio` (event `afterCreate`) — **Inference:** the collection's internal model name is `ll-pre-servicio`.

| Operation | Scenario (Make ID) | Detail |
|---|---|---|
| GET `?filters[telefonoServicio][$containsi]=` | `LL - Recomendar Servicio` (2637777), `LL - RecMulti 4 Registrar Contacto` (6919980) | Dedup by provider phone (normalised: spaces/`+` removed, `54911`→`11`; RecMulti uses last 10 digits) |
| POST create | 2637777 (3 variants), 6919980 | New recommended provider |
| PUT `/{id}` `Recomendadores` | 2637777, 6919980 | Appends `{ "<recommender name>": "<recommender wa_id>" }` to the JSON array |
| PUT `/{id}` `mensajesEnviados: 1` | `LL - Envio de Mensaje Recomendado` (4222809) | After provider template is sent |
| GET `?filters[cupon][cupon][$eq]=…&fields[0]=recomendadores` | `LL - Anuncio Publicado` (4378165) | Find recommenders of an advertiser by coupon |
| GET (paginated, `telefonoServicio $notNull`, `mensajesEnviados` null or 1) | `LL - Limpieza Tabla Recomendados Interna` (6477190, **inactive**, incomplete) | — |
| DELETE `/{id}` (only ID `1230` allowed by filter) | `Firbot - Borrar registros de prueba (temporal)` (6932098, **inactive**) | Test-data cleanup |

| API key | Type (observed) | Written by Make | Notes |
|---|---|---|---|
| `nombrePrestador` | text | Yes | Provider name (from AI extraction / contact) |
| `telefonoServicio` | text | Yes | Provider phone (digits) — key for dedup |
| `barrioCliente` | text | Yes | Neighbourhood as typed/normalised |
| `barrioServicio` | relation (`connect: [{id}]`) → barrios-agenda | Yes | Only when zone resolved |
| `categoriaServicio` | relation (`connect: [{id}]`) → categorias-de-servicios | Yes | Only when category resolved |
| `observacion` | text | Yes | `"Barrio ingresado: … Servicio ingresado: …"`; parsed back by 4222809 to choose template variant |
| `Recomendadores` | JSON array of `{name: phone}` objects | Yes | Personal data — never sample |
| `mensajesEnviados` | number | Yes (=1) | Overlaps with Make DS `LL_RecommendationsMade` |
| `cupon` (relation → Cupones; `cupon.cupon`) | relation | No (filter only) | |
| `rawData.*`, `data.id`, `modelo`, `evento` | webhook payload | — | Sent by Strapi to webhook `Creacion-Recomendado-Strapi` |

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
