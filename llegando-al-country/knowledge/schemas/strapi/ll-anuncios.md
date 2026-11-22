---
title: "LL - Anuncios — Visible Fields"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# LL - Anuncios — Visible UI Fields

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

## Schema verification required

- Retrieve Strapi model schema through authorised read-only method; preserve exact API field keys, relation targets, types and constraints.
- Identify unique keys, validation, retention rules, business ownership and actual Make read/write paths.
- Never store production values or sample contact data in this repository.
