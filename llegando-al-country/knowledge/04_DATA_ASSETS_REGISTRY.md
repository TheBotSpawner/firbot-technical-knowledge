---
title: "Data Assets Registry"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 04 — Data Assets Registry

**Important:** the Strapi fields listed in `schemas/strapi/` were seen in *UI screenshots*, **not** inspected full database/API schemas. The Data Stores were visible in the client's Make UI; purpose and schemas of most still need verification. The screenshot counts are intentionally not stored as long-term truth.

| Data ID | Type | Exact observed name | Platform | Role | Owner | Sensitivity (provisional) | Criticality | Linked automations | Schema/detail | Evidence |
|---|---|---|---|---|---|---|---|---|---|---|
| `DATA-LTC-001` | Strapi collection | LL - Recomendaciones de servicios | Strapi | Recommended providers, referral/coupon/follow-up records | Client / Country Magazine | Confidential | High | AUTO-LTC-005; TODO | [fields](schemas/strapi/ll-recomendaciones-de-servicios.md) | Screenshots + stakeholder |
| `DATA-LTC-002` | Strapi collection | LL - WhatsApp Conversación | Strapi | Conversations and activity counts | Client / Country Magazine | Confidential | High | AUTO-LTC-001, AUTO-LTC-008; TODO | [fields](schemas/strapi/ll-whatsapp-conversacion.md) | Screenshots |
| `DATA-LTC-003` | Strapi collection | LL - WhatsApp Mensaje | Strapi | Individual WhatsApp messages | Client / Country Magazine | Confidential | High | AUTO-LTC-008; TODO | [fields](schemas/strapi/ll-whatsapp-mensaje.md) | Screenshots |
| `DATA-LTC-004` | Strapi collection | LL - Anuncios | Strapi | Published service listings; **read-only for Firbot** | Client / Country Magazine | Internal / Confidential | Critical | AUTO-LTC-002–004; TODO | [fields](schemas/strapi/ll-anuncios.md) | Screenshots + stakeholder |
| `DATA-LTC-005` | Make Data Store | Firbot_PatcherLog | Make.com | Purpose not verified | Client-owned Make account | Unknown | Unknown | TODO | TODO | Screenshot only |
| `DATA-LTC-006` | Make Data Store | LL_MessagesHistory | Make.com | Message state/history (by name, main search mapping) | Client-owned Make account | Confidential | High | AUTO-LTC-001; TODO | TODO | Screenshot + main export |
| `DATA-LTC-007` | Make Data Store | LL_MultiRecBatch | Make.com | Multiple recommendation batches (inference) | Client-owned Make account | Confidential | Unknown | TODO | TODO | Screenshot |
| `DATA-LTC-008` | Make Data Store | LL_OffTimeRecomendations | Make.com | Off-time recommendations (inference) | Client-owned Make account | Confidential | Unknown | TODO | TODO | Screenshot |
| `DATA-LTC-009` | Make Data Store | LL_PermissionsList | Make.com | Permissions (by name and main lookup) | Client-owned Make account | Confidential | High | AUTO-LTC-001; TODO | TODO | Screenshot + main export |
| `DATA-LTC-010` | Make Data Store | LL_RecommendationsMade | Make.com | Recommendations already made (inference) | Client-owned Make account | Confidential | Unknown | TODO | TODO | Screenshot |
| `DATA-LTC-011` | Make Data Store | LL_ReviewRequests | Make.com | Review request state (inference) | Client-owned Make account | Confidential | Unknown | TODO | TODO | Screenshot |
| `DATA-LTC-012` | Make Data Store | LL_Users | Make.com | User tracking/state (inference) | Client-owned Make account | Confidential | High | TODO | TODO | Screenshot |
| `DATA-LTC-013` | Make Data Store | LL_WelcomeContactsMade | Make.com | Welcome-message contacts (inference) | Client-owned Make account | Confidential | Unknown | TODO | TODO | Screenshot |

## Confirmed write boundaries

- Firbot integration may create/update recommendation and WhatsApp-related records in Strapi as needed for the chatbot. **Specific field-level write permissions remain TODO.**
- Strapi `LL - Anuncios` is **read-only from Firbot's automation scope**, as explicitly confirmed by the stakeholder.
- The client manages Strapi's own system, domain model and website/dashboard.

## Other visible Strapi collections (not yet formally registered as in-scope)

`LL - Usuarios`, `LL - Categorías`, `LL - Subcategorías`, `LL - Cupones`, `LL - Opiniones`, `LL - WhatsApp Variante`, `LL - Log de Búsquedas`, `LL - Pagos`, `LL - Suscripciones Servicios`, and others were visible in the navigation. Register each as a canonical DATA ID **only once live Make/Strapi evidence confirms actual integration relevance**.

## Vendor IDs confirmed from inspected main export

- Main lookup `datastore: 38022` had inconsistent metadata labels **`LL_MessagesHistory`** and **`CountryMagazineDataStore`**: **Conflict — verification required** before assigning a final mapping.
- Main lookup `datastore: 76312` labelled `LL_PermissionsList`.
- Main lookup `datastore: 193870` and `193869`: **TODO: verify** corresponding Data Store names.

## Sensitivity and documentation policy

- Phone numbers and message text imply at least **Confidential** handling for message-related data; formal classification and retention: **TODO: verify**.
- Do not copy live customer records, phone numbers or chat message contents into this repository.
- Document schemas as field definitions, not record dumps.
