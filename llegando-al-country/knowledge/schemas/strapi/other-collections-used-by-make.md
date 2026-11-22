---
title: "Other Strapi collections and endpoints used by Make"
status: Draft
last_modified: 2026-11-22
verification: "Make-side usage confirmed from live blueprints (2026-11-22); full Strapi models not inspected"
---

# Other Strapi collections and endpoints used by Make

All requests go to `https://admin.countrymagazine.com.ar/api/…`. Only the field keys literally used by Make are listed (exact API keys, incomplete model). All are **read-only** from Make except the custom `wpp-bot` endpoints.

## barrios-agenda

- **IDs:** `DATA-LTC-014` / `SCHEMA-LTC-014`. Collection of neighbourhoods/countries (UI label not verified).
- **Endpoint / ops:** `GET /api/barrios-agenda` — `filters[nombre][$containsi]=<normalised input>`; full paginated list (`pagination[pageSize]=40`, iterated page by page) for AI similarity matching; `fields[0]=nombre`.
- **Fields used:** `id`, `nombre`.
- **Used by:** `LL - Buscar Zona` (2637689), `LL - Recomendar Servicio` (2637777, ID lookup for `barrioServicio`), `LL - RecMulti 5 Confirmar` (6920183).
- **Relation:** target of `recomendaciones-servicios.barrioServicio`; `servicios.barrios` is filtered by `barrios.nombre` (**Inference:** same collection).

## categorias-de-servicios

- **IDs:** `DATA-LTC-015` / `SCHEMA-LTC-015`. UI: `LL - Categorías` (**Inference**).
- **Endpoint / ops:** `GET /api/categorias-de-servicios` — `filters[nombre][$containsi]`, `filters[$or][..][nombre][$startsWithi|$containsi]`, `filters[id]=`, full list `pagination[pageSize]=400`.
- **Fields used:** `id`, `nombre`. Design samples also show `tipo`, `palabras_claves`, `palabras_claves_texto` (not used in mappings).
- **Used by:** `LL - Buscar Categoría` (2637692), `LL - Recomendar Servicio` (2637777), `LL - Envio de Mensaje Recomendado` (4222809), `LL - RecMulti 4 Registrar Contacto` (6919980).
- **Relation:** target of `recomendaciones-servicios.categoriaServicio`; `servicios.categorias` / `servicios.categoriaPrincipal`.

## grupos-categorias

- **IDs:** `DATA-LTC-016` / `SCHEMA-LTC-016`.
- **Endpoint / ops:** `GET /api/grupos-categorias?filters[nombre][$containsi]=` — second-level match in `LL - Buscar Categoría` when no category matches exactly.
- **Fields used:** `nombre` (existence check only).

## opiniones

- **IDs:** `DATA-LTC-017` / `SCHEMA-LTC-017`. UI: `LL - Opiniones`.
- **Endpoint / ops:** `GET /api/opiniones?filters[servicio][id][$eq]=…&pagination[pageSize]=1&fields[0]=id&publicationState=preview` — reads only `meta.pagination.total` to detect the 1st and 5th review of an ad.
- **Used by:** `LL - Nueva Opinion Anuncio` (4469351). Webhook payload from Strapi contains `opinion.servicio.id`, `opinion.servicio.slug`.

## wpp-bot custom endpoints

- **IDs:** `DATA-LTC-018` / `SCHEMA-LTC-018`. Custom Strapi controllers (not standard collections). Auth: header `X-Bot-Token` (literal value hard-coded in blueprints — security finding).

| Endpoint | Caller | Request | Response keys used |
|---|---|---|---|
| `POST /api/wpp-bot/mensajes` | `LL - Log Message` (5421473) | see [`ll-whatsapp-mensaje.md`](ll-whatsapp-mensaje.md) | `guardados`, `errores`, `omitidos` |
| `POST /api/wpp-bot/codigo` | `LL - Envio de Mensaje Recomendado` (4222809) | `{ recomendacionId, elegirVariante: true, campaniaId: 1 }` | `codigo` (coupon code inserted in the provider template) |

**Inference:** `/wpp-bot/codigo` generates/assigns a coupon (`LL - Cupones`) to the recommendation and selects a template variant (`LL - WhatsApp Variante`). Server-side logic is client-owned and not visible from Make — **TODO: verify**.

## Strapi → Make webhooks (outbound from Strapi/website)

Payload shapes observed in webhook interfaces/design samples (no personal data reproduced):

| Make webhook (ID) | Scenario | Payload keys |
|---|---|---|
| `Creacion-Recomendado-Strapi` (1925734) | 4222809 | `modelo` (`ll-pre-servicio`), `evento` (`afterCreate`), `data.id`, `rawData.{nombrePrestador, telefonoServicio, barrioCliente, categoriaServicio.connect[].id, observacion}` |
| `Codigo-Verificacion-WPP-Strapi` (1999490) | 4378165 | `servicio.{id, slug}` (event *ad published* — **Inference** from module names) |
| `NewPostOpinionStrapi` (2039466) | 4469351 | `opinion.servicio.{id, slug}` |
| `NewPostVisitStrapi` (2039478) | 4469369 | `event` (`servicio_20_visitas`), `visitas`, `servicio.{id, slug, nombre}`, `timestamp` |
| `Boton-Contactar` (2560154) | 5625466 | `tipo` (`pedido_review`), `telefono`, `usuario.{id,nombre}`, `servicio.{id,nombre,slug,url}`, `contacto.{tipo,fecha}`, `debug` |
| `Onboarding-Paso-02/03/04` (2642230/2642233/2642237) | 5822771/5822780/5822785 | `event` (e.g. `servicio_seguimiento_dia_3`), `dia`, `timestamp`, `servicio.{id,nombre,slug,whatsapp,telefono,aprobado_en}`, `usuario.{id,nombre,telefono}` |

Which Strapi lifecycle/cron emits each webhook is not visible from Make — **TODO: verify with client**.
