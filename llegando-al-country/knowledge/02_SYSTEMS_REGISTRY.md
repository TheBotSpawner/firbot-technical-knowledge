---
title: "Systems Registry"
status: Verified
last_modified: 2026-11-22
verification: "Make configuration confirmed from live system 2026-11-22; other systems as indicated"
---

# 02 — Systems Registry

IDs are repository-specific and **not** vendor resource IDs.

| System ID | System | Role | Status | Criticality | Owner / maintainer | How Make connects | Verification |
|---|---|---|---|---|---|---|---|
| `SYS-LTC-001` | Make.com — org `Llegando al Country` (4655020), team `My Team` (1163364), zone `us2.make.com`, plan Pro | Orchestration, Data Stores, webhooks | Active - Core | Critical | Client owns account; Firbot maintains scenarios | — | Confirmed from live system |
| `SYS-LTC-002` | Strapi — `admin.countrymagazine.com.ar` (Strapi v4-style REST, nginx/Ubuntu) | System of record: ads, recommendations, messages, catalogues, custom bot API | Active - Core | Critical | Country Magazine technical team | Raw HTTP; 2 literal API tokens + 1 bot token; team var `LL_STRAPI_TOKEN` (RecMulti) | Endpoints confirmed from blueprints; models not inspected |
| `SYS-LTC-003` | WhatsApp Business Cloud API (Graph v22.0; phone-number ID `717278908136135`) | User channel, templates, media | Active - Core | Critical | Meta app / WABA owner **Unknown** | Inbound: custom webhook 2623296; outbound: raw HTTP with literal token (19 scenarios) or team var `LL_WA_TOKEN` | Confirmed from blueprints; Meta config not inspected |
| `SYS-LTC-004` | OpenAI API (Make app `openai-gpt-3`) | Intent/slot extraction, similarity, FAQ, name extraction | Active | High | Account owner **Unknown** | Connection `My OpenAI connection` (4527306) | Confirmed connection; models configured: `gpt-6-luna`, `gpt-4o-mini` |
| `SYS-LTC-005` | Gmail | Stated error-notification channel | **Conflict — verification required** | Medium | Unknown | **No Gmail module/connection exists in Make.** Gmail addresses appear only as e-mail *recipients*. | Stakeholder statement vs. live config |
| `SYS-LTC-006` | Country Magazine / Llegando website and dashboard | Ads UI, "Contactar" button, stats/messages dashboard | Active - Core | High | Country Magazine technical team | Calls Make webhooks (Inference for which component); reads Strapi | Stakeholder + webhook payloads |
| `SYS-LTC-007` | Microsoft 365 / Outlook (Make app `microsoft-email`) | **Actual** sender of error e-mails | Active | High (monitoring) | Individual Firbot account (connection 5431897) | OAuth connection | Confirmed from live system |
| `SYS-LTC-008` | Google Drive (client Google account) | Sticker image storage | Active | Low | Client | Connection 9967715 (expires 2027-05-19) | Confirmed |
| `SYS-LTC-009` | Make API | A/B variable update (9953737, OAuth, expires 2027-05-20); Blueprint Patcher (12169302, API key) | Active / tooling | Medium | Client Make user | Make app connections | Confirmed |

## Outstanding

- Meta: WABA ID, app ownership, webhook callback URL and verify token, token type/expiry, template approval status.
- Strapi: version, hosting, token permissions, lifecycle hooks/cron that call Make webhooks, custom `wpp-bot` controllers.
- OpenAI: account/project owner, billing, data-retention settings; whether `gpt-6-luna` is the intended model.
- E-mail: who owns the alert mailboxes; whether Gmail is still expected anywhere.
