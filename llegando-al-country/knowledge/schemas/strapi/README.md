---
title: "Strapi schemas — index and Make integration matrix"
status: Draft
last_modified: 2026-11-22
verification: "Make-side usage confirmed from live blueprints (2026-11-22); Strapi models not inspected directly"
---

# Strapi (client-owned) — collections used by Make

**Base URL:** `https://admin.countrymagazine.com.ar/api/` (Strapi v4 REST conventions: `data[].attributes`, `filters[...]`, `populate`, `pagination`). Response headers in design samples show `x-powered-by: Strapi` behind `nginx/1.18.0 (Ubuntu)`.

**Evidence levels.** Two kinds of field information exist and must not be mixed:

1. *UI-visible fields* — from Strapi Content Manager screenshots supplied during onboarding (partial).
2. *Make-observed fields* — field keys literally used in Make request URLs, filters, bodies and response mappings (confirmed from live blueprints, 2026-11-22). These are exact API keys but **not** the complete model.

Full content-type schemas (types, required flags, relations, permissions of the API tokens) were **not** inspected: no read access to Strapi was available in this session.

## Endpoint ↔ collection map

| Schema / Data ID | Collection (UI name) | REST endpoint used by Make | Operations from Make | Doc |
|---|---|---|---|---|
| `SCHEMA-LTC-001` / `DATA-LTC-001` | LL - Recomendaciones de servicios | `/api/recomendaciones-servicios` | GET (filter by phone / by cupón), POST (create), PUT (append `Recomendadores`, set `mensajesEnviados`), DELETE (inactive test tool only) | [doc](ll-recomendaciones-de-servicios.md) |
| `SCHEMA-LTC-002` / `DATA-LTC-002` | LL - WhatsApp Conversación | *none directly*; written by Strapi custom endpoint `/api/wpp-bot/mensajes` (**Inference**) | — | [doc](ll-whatsapp-conversacion.md) |
| `SCHEMA-LTC-003` / `DATA-LTC-003` | LL - WhatsApp Mensaje | `/api/wpp-bot/mensajes` (custom POST), `/api/wpp-mensajes` (GET by `claveExterna`, PUT `vistoEn`) | POST (via custom controller), GET, PUT | [doc](ll-whatsapp-mensaje.md) |
| `SCHEMA-LTC-004` / `DATA-LTC-004` | LL - Anuncios | `/api/servicios` | **GET only** (read-only confirmed) | [doc](ll-anuncios.md) |
| `SCHEMA-LTC-014` / `DATA-LTC-014` | Barrios (agenda) | `/api/barrios-agenda` | GET | [doc](other-collections-used-by-make.md#barrios-agenda) |
| `SCHEMA-LTC-015` / `DATA-LTC-015` | Categorías de servicios | `/api/categorias-de-servicios` | GET | [doc](other-collections-used-by-make.md#categorias-de-servicios) |
| `SCHEMA-LTC-016` / `DATA-LTC-016` | Grupos de categorías | `/api/grupos-categorias` | GET | [doc](other-collections-used-by-make.md#grupos-categorias) |
| `SCHEMA-LTC-017` / `DATA-LTC-017` | LL - Opiniones | `/api/opiniones` | GET (count per servicio) | [doc](other-collections-used-by-make.md#opiniones) |
| `SCHEMA-LTC-018` / `DATA-LTC-018` | Custom bot API | `/api/wpp-bot/mensajes`, `/api/wpp-bot/codigo` | POST | [doc](other-collections-used-by-make.md#wpp-bot-custom-endpoints) |

Collections visible in the Strapi UI but **not referenced by any Make scenario** (2026-11-22): `LL - Usuarios` (only read as populated relation `usuario` of `servicios`), `LL - Subcategorías`, `LL - Cupones` (only as populated relation `cuponUsado` / filter `cupon.cupon`), `LL - WhatsApp Variante` (only through `/wpp-bot/codigo` and `VarianteId` logging, **Inference**), `LL - Log de Búsquedas`, `LL - Pagos`, `LL - Suscripciones Servicios` (only as populated relation `suscripcion_activa` in design samples).

## Authentication patterns (no values recorded)

| Pattern | Where | Status |
|---|---|---|
| `Authorization: Bearer <literal Strapi API token>` hard-coded in HTTP modules | 13 scenarios (see security notes) | **Security finding** |
| `X-Bot-Token: <literal>` hard-coded | `LL - Log Message`, `LL - Envio de Mensaje Recomendado`, `LL - Buscar Servicio por Zona` (orphan modules) | **Security finding** |
| `Authorization: Bearer {{var.team.LL_STRAPI_TOKEN}}` (Make team custom variable) | RecMulti 4/5, Firbot temporal tools | Preferred pattern (still visible to anyone with Make team access) |

## LL - Anuncios read-only rule

Verified 2026-11-22: across all 37 scenarios, every request to `/api/servicios` is a `GET`. No POST/PUT/PATCH/DELETE to `servicios` exists. **No conflict found.** Note: the literal Strapi token used for these reads is the same token used for writes to `recomendaciones-servicios`; whether that token *could* write `servicios` depends on Strapi API-token permissions (**Unknown — verify in Strapi**).
