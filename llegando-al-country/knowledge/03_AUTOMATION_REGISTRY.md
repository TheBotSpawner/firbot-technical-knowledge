---
title: "Automation Registry"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
---

# 03 — Automation Registry

Complete inventory of the Make team `My Team` (1163364) in organization `Llegando al Country` (4655020), obtained read-only on **2026-11-22**: **37 scenarios (29 active, 8 inactive)**. All have a sanitized export (see [manifest](../exports/make/manifest.md)). IDs `AUTO-LTC-001..012` were provisionally allocated during onboarding and are **preserved**; `013..037` are new. Status = `isActive` in Make on 2026-11-22.

| Automation ID | Exact Make name | Make ID | Status | Criticality | Trigger | Purpose | Called by | Detail |
|---|---|---|---|---|---|---|---|---|
| `AUTO-LTC-001` | LL - Chatbot Recomendacion de Servicios | 2505419 | Active | Critical | Webhook `WPP-Messages-Nexo-Webhook` (2623296) | Nexo inbound orchestration | — (entry) | [doc](automations/make/ll-chatbot-recomendacion-de-servicios.md) |
| `AUTO-LTC-002` | LL - Buscar Zona | 2637689 | Active | High | Subscenario | Resolve neighbourhood (exact/AI-similar) | 001, 012 | [doc](automations/make/ll-search-subscenarios.md) |
| `AUTO-LTC-003` | LL - Buscar Categoría | 2637692 | Active | High | Subscenario | Resolve service category / similar ads | 001 | [doc](automations/make/ll-search-subscenarios.md) |
| `AUTO-LTC-004` | LL - Buscar Servicio por Zona | 2637743 | Active | High | Subscenario | Search ads and reply results | 001 | [doc](automations/make/ll-search-subscenarios.md) |
| `AUTO-LTC-005` | LL - Recomendar Servicio | 2637777 | Active | High | Subscenario | Create/update single recommendation in Strapi | 001 | [doc](automations/make/ll-recomendar-servicio.md) |
| `AUTO-LTC-006` | LL - Admin Mode | 4133823 | Active | Medium | Subscenario | Admin menu / welcome campaign | 001 | [doc](automations/make/ll-admin-mode-and-welcome.md) |
| `AUTO-LTC-007` | Envio de Notificaciones de Error Chatbots | 4226818 | Active | Critical (monitoring) | Subscenario | Error e-mail (Outlook) + optional WA apology | 23 scenarios | [doc](automations/make/shared-utility-subscenarios.md) |
| `AUTO-LTC-008` | LL - Log Message | 5421473 | Active | Critical | Subscenario | Log message to Strapi (+ DS) | 20 scenarios | [doc](automations/make/shared-utility-subscenarios.md) |
| `AUTO-LTC-009` | LL - Subscenario Send Sticker | 5694920 | Active | Low | Subscenario | Send sticker from Google Drive | 001 | [doc](automations/make/shared-utility-subscenarios.md) |
| `AUTO-LTC-010` | LL - Subscenario Special Interaction | 5695064 | Active | High | Subscenario | Button/keyword handlers incl. review answers | 001 | [doc](automations/make/ll-special-interaction-and-review.md) |
| `AUTO-LTC-011` | Sleep n Seconds | 5892850 | Active | Low | Subscenario | Delayed "processing" notice | 001 | [doc](automations/make/shared-utility-subscenarios.md) |
| `AUTO-LTC-012` | LL - RecMulti 1 Recibir mensaje | 6920256 | Active | High | Subscenario | Multi-recommendation controller (reconciled from "Recomendación múltiple") | 001 | [doc](automations/make/ll-recmulti-recomendacion-multiple.md) |
| `AUTO-LTC-013` | Delete Messages | 2629639 | Active | Medium | Schedule every 2 h | Purge stale `LL_MessagesHistory` | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-014` | LL - Enviar Bienvenida | 4137315 | Active | Medium | Subscenario | Send welcome template to queued contacts | 006 | [doc](automations/make/ll-admin-mode-and-welcome.md) |
| `AUTO-LTC-015` | LL - Agregar Contactos de Bienvenida | 4199053 | Active | Low | Subscenario | Queue welcome contacts | 006 | [doc](automations/make/ll-admin-mode-and-welcome.md) |
| `AUTO-LTC-016` | LL - Envio de Mensaje Recomendado | 4222809 | Active | High | Webhook `Creacion-Recomendado-Strapi` (1925734) | Template + coupon to recommended provider (A/B) | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-017` | LL - Envio de Mensaje Recomendados Previos | 4227025 | Active (inert) | Low | On-demand, no caller | Leftover: reads `LL_RecommendationsMade` only | — | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-018` | LL - Anuncio Publicado | 4378165 | Active | High | Webhook `Codigo-Verificacion-WPP-Strapi` (1999490) | Templates to advertiser and recommenders on publication | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-019` | LL - Nueva Opinion Anuncio | 4469351 | Active | Medium | Webhook `NewPostOpinionStrapi` (2039466) | Template on 1st / 5th review | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-020` | LL - Nueva Visita Anuncio | 4469369 | Active | Medium | Webhook `NewPostVisitStrapi` (2039478) | Template on 20 visits | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-021` | LL - Send Template On Time | 5146890 | Active | Medium | Schedule 10:00 & 18:00 | Replay off-time queue | — | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-022` | LL - Pedido Review | 5625466 | Active | Medium | Webhook `Boton-Contactar` (2560154) | Ask user whether they contacted provider | Website | [doc](automations/make/ll-special-interaction-and-review.md) |
| `AUTO-LTC-023` | LL - Onboarding Paso 2 | 5822771 | Active | Medium | Webhook `Onboarding-Paso-02` (2642230) | Advertiser follow-up template | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-024` | LL - Onboarding Paso 3 | 5822780 | Active (1 DLQ item) | Medium | Webhook `Onboarding-Paso-03` (2642233) | Advertiser follow-up (no views) | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-025` | LL - Onboarding Paso 4 | 5822785 | Active | Medium | Webhook `Onboarding-Paso-04` (2642237) | Advertiser follow-up (ask for reviews) | Strapi | [doc](automations/make/ll-outbound-notifications.md) |
| `AUTO-LTC-026` | LL - RecMulti 2 Mostrar Resumen | 6920153 | Active | High | Subscenario | Show/persist multi-rec tray | 012 | [doc](automations/make/ll-recmulti-recomendacion-multiple.md) |
| `AUTO-LTC-027` | LL - RecMulti 3 Cancelar | 6920171 | Active | Medium | Subscenario | Cancel tray / re-inject message | 012 | [doc](automations/make/ll-recmulti-recomendacion-multiple.md) |
| `AUTO-LTC-028` | LL - RecMulti 4 Registrar Contacto | 6919980 | Active | High | Subscenario | Create/append recommendation in Strapi | 029 | [doc](automations/make/ll-recmulti-recomendacion-multiple.md) |
| `AUTO-LTC-029` | LL - RecMulti 5 Confirmar | 6920183 | Active | High | Subscenario | Register all contacts, report | 012 | [doc](automations/make/ll-recmulti-recomendacion-multiple.md) |
| `AUTO-LTC-030` | LL - Limpieza Tabla Recomendados Interna | 6477190 | **Inactive** | — | Schedule 15 min (off) | Unfinished cleanup | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-031` | Automation Testing | 4141246 | **Inactive** | — | On-demand | Obsolete test | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-032` | Firbot - Blueprint Patcher | 6919674 | **Inactive** | Tooling (high risk) | On-demand | Patch scenario blueprints via Make API | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-033` | Firbot - Consulta Strapi (temporal) | 6920671 | **Inactive** | Tooling | On-demand | Ad-hoc Strapi GET | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-034` | Firbot - Simulador WhatsApp (temporal) | 6920717 | **Inactive** | Tooling | On-demand | Post simulated message to main webhook | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-035` | Firbot - Borrar registros de prueba (temporal) | 6932098 | **Inactive** | Tooling | On-demand | Delete test recommendation in Strapi | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-036` | Firbot - Test IA extractor (temporal) | 6933016 | **Inactive** | Tooling | On-demand | Prompt testing | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |
| `AUTO-LTC-037` | Firbot - Buscar registros de prueba (temporal) | 6933260 | **Inactive** | Tooling | On-demand | Dummy test | — | [doc](automations/make/housekeeping-and-firbot-tooling.md) |

## Reconciliation with the onboarding baseline

| Baseline item | Live result |
|---|---|
| 11 `SCN_*` references in the main blueprint | All 11 exist and are **active**; names match exactly. |
| `AUTO-LTC-012` "Recomendación múltiple (exact name TODO)" | = `LL - RecMulti 1 Recibir mensaje` (6920256), which calls 4 more RecMulti scenarios. |
| `AUTO-LTC-001` live ID TODO | = **2505419**. Live blueprint last edited 2026-11-06; supersedes the onboarding export (which was not compared byte-for-byte because it was not provided to this session). |
| "Additional scheduled flows — do not assume" | Confirmed: 2 scheduled (013, 021) + 1 inactive (030); 8 webhook-triggered flows independent of the chat (016, 018–020, 022–025). |
| Scenario folders | None used in the team. |

## Operating notes

- Development changes are applied directly to production (no test team/organization exists in Make; confirmed by execution provenance on 2026-11-05).
- Execution logs are retained 30 days (plan setting). Failed executions in the window: 2505419 (1, 2026-11-05) and 6920256 (1, 2026-11-05, manual MCP run). Scenario 5822780 has 1 item in the incomplete-executions queue.
