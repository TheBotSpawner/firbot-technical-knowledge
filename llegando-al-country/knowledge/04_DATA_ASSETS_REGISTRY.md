---
title: "Data Assets Registry"
status: Verified
last_modified: 2026-11-22
verification: "Make assets confirmed from live system 2026-11-22; Strapi fields: UI screenshots + Make-observed API keys (models not inspected)"
---

# 04 — Data Assets Registry

Evidence: Make Data Stores, data structures, webhooks and scenario blueprints read via the Make API on 2026-11-22 (read-only). Strapi was **not** accessed directly; Strapi information = onboarding screenshots + field keys used by Make. **No records were exported.**

## Strapi collections and endpoints

| Data ID | Type | Exact name (UI) / endpoint | Role | Make operations | Sensitivity | Criticality | Schema |
|---|---|---|---|---|---|---|---|
| `DATA-LTC-001` | Strapi collection | LL - Recomendaciones de servicios — `/api/recomendaciones-servicios` | Recommended providers | GET, POST, PUT (DELETE only in inactive test tool) | Confidential | High | [SCHEMA-LTC-001](schemas/strapi/ll-recomendaciones-de-servicios.md) |
| `DATA-LTC-002` | Strapi collection | LL - WhatsApp Conversación | Conversations | None direct (server-side via `/wpp-bot/mensajes`, Inference) | Confidential | High | [SCHEMA-LTC-002](schemas/strapi/ll-whatsapp-conversacion.md) |
| `DATA-LTC-003` | Strapi collection | LL - WhatsApp Mensaje — `/api/wpp-mensajes` | Durable message log | POST via custom endpoint; GET + PUT `vistoEn` | Confidential | High | [SCHEMA-LTC-003](schemas/strapi/ll-whatsapp-mensaje.md) |
| `DATA-LTC-004` | Strapi collection | LL - Anuncios — `/api/servicios` | Published ads | **GET only** (read-only confirmed) | Internal/Confidential | Critical | [SCHEMA-LTC-004](schemas/strapi/ll-anuncios.md) |
| `DATA-LTC-014` | Strapi collection | `/api/barrios-agenda` | Neighbourhood catalogue | GET | Internal | High | [SCHEMA-LTC-014](schemas/strapi/other-collections-used-by-make.md#barrios-agenda) |
| `DATA-LTC-015` | Strapi collection | `/api/categorias-de-servicios` | Category catalogue | GET | Internal | High | [SCHEMA-LTC-015](schemas/strapi/other-collections-used-by-make.md#categorias-de-servicios) |
| `DATA-LTC-016` | Strapi collection | `/api/grupos-categorias` | Category groups | GET | Internal | Low | [SCHEMA-LTC-016](schemas/strapi/other-collections-used-by-make.md#grupos-categorias) |
| `DATA-LTC-017` | Strapi collection | LL - Opiniones — `/api/opiniones` | Reviews (count only) | GET | Internal | Low | [SCHEMA-LTC-017](schemas/strapi/other-collections-used-by-make.md#opiniones) |
| `DATA-LTC-018` | Strapi custom API | `/api/wpp-bot/mensajes`, `/api/wpp-bot/codigo` | Bot logging; coupon/variant assignment | POST | Confidential | Critical | [SCHEMA-LTC-018](schemas/strapi/other-collections-used-by-make.md#wpp-bot-custom-endpoints) |

## Make Data Stores (all 9 in the team)

| Data ID | Exact name | Make DS ID | Role | Readers / writers (Make IDs) | Records | Sensitivity | Criticality | Schema |
|---|---|---|---|---|---|---|---|---|
| `DATA-LTC-005` | `Firbot_PatcherLog` | 193874 | Firbot dev-tool log (not production) | W: 6919674, 6920671, 6932098, 6933260 | 20 | Confidential (may hold data fragments) | Low | [SCHEMA-LTC-005](schemas/make/firbot-patcherlog.md) |
| `DATA-LTC-006` | `LL_MessagesHistory` | 38022 | Conversation memory + processing flag | R/W: 2505419, 5421473, 5892850, 2637743, 2637777, 4133823, 5695064, 6920183, 2629639 | 1 | Confidential | Critical | [SCHEMA-LTC-006](schemas/make/ll-messageshistory.md) |
| `DATA-LTC-007` | `LL_MultiRecBatch` | 193870 | Multi-recommendation tray | R: 2505419, 6920256; W: 6920153, 6920171, 6920183 | 0 | Confidential | High | [SCHEMA-LTC-007](schemas/make/ll-multirecbatch.md) |
| `DATA-LTC-008` | `LL_OffTimeRecomendations` | 101658 | Off-hours template queue (bypassed) | W: 4222809, 4378165, 4469351, 4469369; R/D: 5146890 | 0 | Confidential (stores webhook URLs) | Medium | [SCHEMA-LTC-008](schemas/make/ll-offtimerecomendations.md) |
| `DATA-LTC-009` | `LL_PermissionsList` | 76312 | Admin allow-list | R: 2505419; maintained manually (Inference) | 5 | Confidential | High | [SCHEMA-LTC-009](schemas/make/ll-permissionslist.md) |
| `DATA-LTC-010` | `LL_RecommendationsMade` | 80766 | Providers already contacted (dedup) | R/W: 4222809; R: 4227025, 4141246 | 285 | Confidential | High | [SCHEMA-LTC-010](schemas/make/ll-recommendationsmade.md) |
| `DATA-LTC-011` | `LL_ReviewRequests` | 123790 | Review-request state | W: 5625466; R/U: 5695064 | 12 | Confidential | Medium | [SCHEMA-LTC-011](schemas/make/ll-reviewrequests.md) |
| `DATA-LTC-012` | `LL_Users` | 193869 | Remembered neighbourhood per user | U: 2505419, 6920183; R: 6920256 | 2 | Confidential | Medium | [SCHEMA-LTC-012](schemas/make/ll-users.md) |
| `DATA-LTC-013` | `LL_WelcomeContactsMade` | 76313 | Welcome campaign queue | W: 4199053; R/U: 4137315 | 9 | Confidential | Medium | [SCHEMA-LTC-013](schemas/make/ll-welcomecontactsmade.md) |

## Other assets

| Data ID | Type | Exact name | Notes |
|---|---|---|---|
| `DATA-LTC-019` | Make team custom variables | `LL_WA_TOKEN`, `LL_STRAPI_TOKEN`, `ABTesting` | Names observed in blueprints; values **not read**. `ABTesting` is written by 4222809 via the Make API. |
| `DATA-LTC-020` | Make webhooks | 17 hooks (see [automations/make/README.md](automations/make/README.md#webhooks-17-in-team)) | URLs are secrets; 7 hooks unattached. |
| `DATA-LTC-021` | Google Drive folder | Nexo sticker files (`.webp`, 7 file IDs) | Client Google account; read by 5694920. |
| `DATA-LTC-022` | WhatsApp message templates (Meta) | `llegando_first_message_v2`, `llegando_contacto_recomendados_a/_b/_c`, `llegando_new_post_for_creators`, `llegando_new_post_for_recommenders`, `llegando_first_post_review`, `llegando_post_5_reviews`, `llegando_post_20_visits`, `llegando_click_boton_contactar`, `llegando_share_your_profile`, `llegando_no_views`, `llegando_ask_for_reviews` | Names from blueprints; approval status/content in Meta not inspected. |

## Resolved conflicts and mappings (from onboarding)

- `datastore: 38022` labelled both `LL_MessagesHistory` and `CountryMagazineDataStore` → **resolved:** ID 38022 is currently named `LL_MessagesHistory`; `CountryMagazineDataStore` is a stale label in old module metadata (`Delete Messages`, `Automation Testing`).
- `193870` = `LL_MultiRecBatch`; `193869` = `LL_Users` (**resolved**).

## Overlaps / consistency risks

- "Provider already contacted" is tracked twice: `LL_RecommendationsMade` (Make) and `mensajesEnviados` (Strapi).
- Messages are stored twice: short-term `LL_MessagesHistory` (Make) and durable `LL - WhatsApp Mensaje` (Strapi).
- `LL_Users` (Make) is unrelated to Strapi `LL - Usuarios`.

## Write boundaries (verified 2026-11-22)

- Make writes to Strapi only: `recomendaciones-servicios` (POST/PUT; DELETE in inactive tool), `wpp-mensajes` (`vistoEn`), custom `wpp-bot/*` endpoints.
- `LL - Anuncios` (`/api/servicios`): **read-only — no contradiction found.**
- Strapi API-token permissions themselves: **Unknown — verify in Strapi.**
