---
title: "LL - Anuncios — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "UI fields from screenshots (partial); Make-observed fields confirmed from live blueprints 2026-11-22"
---

# SCHEMA-LTC-004 — LL - Anuncios — Visible UI Fields

- **Canonical Data ID:** `DATA-LTC-004`
- **Strapi API identifier (visible):** `servicio`
- **Evidence:** screenshots of authenticated Strapi Content Manager, shared 2026-11-22.
- **Verification level:** **Confirmed from user-provided screenshot**, **not a complete schema**. Type labels are UI-derived/inferred where appropriate. Do not assume underlying DB/API field types, cardinality, nullability, permissions or field completeness.
- **Write policy:** Read-only from Firbot/Nexo — stakeholder confirmed.

## Fields seen in screenshots

| UI field/label | Apparent type | Note |
|---|---|---|
| `Nombre` | Text | Required visible |
| `Estado` | Enum/select | Displayed activo |
| `Descripción` | Long text | Visible in UI; actual schema TODO |
| `Es premium` | Boolean | Visible in UI; actual schema TODO |
| `Tipo de plan` | Enum/select | free and other options; complete list TODO |
| `Suscripción (fecha de alta)` | Datetime | Visible in UI; actual schema TODO |
| `Premium hasta` | Datetime | Visible in UI; actual schema TODO |
| `Legacy vigente hasta` | Datetime | Visible in UI; actual schema TODO |
| `Suscripción activa (Mercado Pago)` | Relation | Visible in UI; actual schema TODO |
| `Email de facturación` | Email | Visible in UI; actual schema TODO |
| `Situación frente al IVA` | Select | Visible in UI; actual schema TODO |
| `CUIT / CUIL / DNI` | Text | Sensitive |
| `Descripción corta` | Text | Visible in UI; actual schema TODO |
| `Tipo de servicio` | Select | Visible in UI; actual schema TODO |
| `Origen del alta` | Select | Displayed Recomendado |
| `Portada` | Media | Visible in UI; actual schema TODO |
| `FotoBanner` | Media | Visible in UI; actual schema TODO |
| `Galería` | Media | Visible in UI; actual schema TODO |
| `Whatsapp` | Text | Visible in UI; actual schema TODO |
| `Teléfono` | Text | Visible in UI; actual schema TODO |
| `Email` | Email | Visible in UI; actual schema TODO |
| `Instagram` | Text | Visible in UI; actual schema TODO |
| `Facebook` | Text | Visible in UI; actual schema TODO |
| `Sitio web` | Text/URL | Visible in UI; actual schema TODO |
| `Domicilio` | Text | Visible in UI; actual schema TODO |
| `Horarios de atención` | Long text | Visible in UI; actual schema TODO |
| `Barrios a los que llega el servicio` | Relation | Visible in UI; actual schema TODO |
| `Corredor del local` | Relation | Visible in UI; actual schema TODO |
| `Categoría principal del servicio` | Relation | Visible in UI; actual schema TODO |
| `Subcategorías` | Relation | Visible in UI; actual schema TODO |
| `Propietario del servicio` | Relation | Visible in UI; actual schema TODO |
| `Origen recomendación` | Relation | Visible in UI; actual schema TODO |
| `Paseos a los que llega` | Relation | Visible in UI; actual schema TODO |
| `Puntuación del servicio` | Number | Visible in UI; actual schema TODO |
| `Cantidad de calificaciones` | Number | Visible in UI; actual schema TODO |
| `Resumen de atributos (derivado)` | JSON | Visible in UI; actual schema TODO |
| `Aprobado en` | Datetime | Visible in UI; actual schema TODO |
| `mensaje_bienvenida_enviado` | Boolean | Visible in UI; actual schema TODO |
| `hit_20_visitas_enviado` | Boolean | Visible in UI; actual schema TODO |
| `seguimiento_dia3_enviado` | Boolean | Visible in UI; actual schema TODO |
| `seguimiento_dia10_enviado` | Boolean | Visible in UI; actual schema TODO |
| `seguimiento_dia30_enviado` | Boolean | Visible in UI; actual schema TODO |
| `Impresiones de tarjeta` | Number | Visible in UI; actual schema TODO |
| `Entradas al perfil` | Number | Visible in UI; actual schema TODO |
| `Contactos (total)` | Number | Visible in UI; actual schema TODO |
| `contadorContactosWhatsapp` | Number | Visible in UI; actual schema TODO |
| `contadorContactosEmail` | Number | Visible in UI; actual schema TODO |
| `contadorContactosTelefono` | Number | Visible in UI; actual schema TODO |
| `contadorContactosInstagram` | Number | Visible in UI; actual schema TODO |
| `contadorContactosFacebook` | Number | Visible in UI; actual schema TODO |
| `contadorContactosWeb` | Number | Visible in UI; actual schema TODO |
| `contadorContactosDomicilio` | Number | Visible in UI; actual schema TODO |
| `Texto de búsqueda (derivado)` | Text | Do not edit manually |
| `Texto de búsqueda normalizado (derivado)` | Text | Do not edit manually |
| `aviso_aprobado_pendiente` | Boolean | Visible in UI; actual schema TODO |

## Fields observed in Make (exact API keys) — confirmed from live blueprints, 2026-11-22

**REST endpoint:** `/api/servicios` (the "LL - Anuncios" collection is exposed as `servicios`; singular API ID `servicio`).
**Operations from Make:** `GET` only — `GET /api/servicios` (list, filtered) and `GET /api/servicios/{id}`. **No writes found → read-only rule confirmed; no conflict.**

| API key | Used as | Scenarios (Make ID) |
|---|---|---|
| `id` | path param from webhook payload `servicio.id` / `opinion.servicio.id` | 4378165, 4469351, 4469369, 5625466, 5822780 |
| `nombre` | response (message text, AI input); `fields[]` | 2637692, 4378165, 5625466 |
| `descripcion` | response → OpenAI category detection | 5625466 |
| `descripcionCorta` | `fields[]`, AI similarity input | 2637692 |
| `slug` | `fields[]`, filter `slug $containsi`, public URL `/llegando/servicio/{slug}` | 2637692, 5695064, 5625466 |
| `estado` | filter `estado $eq activo` | 2637692, 2637743 |
| `whatsapp` | `fields[]`, recipient of advertiser templates | 4378165, 4469351, 4469369 |
| `hit_20_visitas_enviado` | `fields[]`, filter in Onboarding Paso 3 (send only if false) | 5822780 |
| `textoBusquedaNormalizado` | referenced in search mapping | 2637692 |
| `barrios` (relation → barrios) | `populate`, filter `barrios.nombre $containsi` | 2637743 |
| `categorias` (relation → categorías) | `populate`, filter `categorias.nombre $containsi` | 2637743 |
| `categoriaPrincipal` (relation) | filter `categoriaPrincipal.nombre $containsi` | 2637743 |
| `usuario` (relation → LL - Usuarios: `nombre`, `numero`) | populated; advertiser name/phone fallback | 4378165, 4469351, 4469369, 5625466 |
| `cuponUsado` (relation → LL - Cupones: `cupon`) | populated; used to find recommenders who share the coupon | 4378165 |

Relations seen populated in design-time responses (not used in mappings): `paseos`, `galeria`, `portada`, `corredor`, `opiniones`, `FotoBanner`, `ll_seccion_homes`, `suscripcion_activa`, `origenRecomendacion` (→ recomendaciones-servicios). Flags `mensaje_bienvenida_enviado` and `hit_20_visitas_enviado` are **set by Strapi/website logic, not by Make** (no Make writes).

**Make scenarios reading this collection:** `LL - Buscar Categoría`, `LL - Buscar Servicio por Zona`, `LL - Anuncio Publicado`, `LL - Nueva Opinion Anuncio`, `LL - Nueva Visita Anuncio`, `LL - Pedido Review`, `LL - Subscenario Special Interaction`, `LL - Onboarding Paso 3`.

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
