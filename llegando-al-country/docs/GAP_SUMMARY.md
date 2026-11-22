---
title: "Documentation Gaps"
status: Draft
last_modified: 2026-11-22
verification: "Updated after live Make inventory 2026-11-22"
---

# Documentation Gap Summary

## Closed by the 2026-11-22 Make inventory

| Former gap | Resolution |
|---|---|
| Main scenario live ID / revision | 2505419, last edited 2026-11-06; exported |
| Child scenarios not inspected | All 37 scenarios inspected and exported (sanitized) |
| `AUTO-LTC-012` exact name | `LL - RecMulti 1 Recibir mensaje` (6920256) |
| Data Stores 193869/193870 mapping, 38022 alias conflict | `LL_Users`, `LL_MultiRecBatch`; 38022 = `LL_MessagesHistory` (old label stale) |
| Data Store schemas and usage | 9 schema docs + usage matrix |
| AI models/prompts/outputs | Documented per scenario (prompts preserved in sanitized exports) |
| Scheduled/independent flows | 2 schedules + 8 platform-webhook flows found and documented |
| Scope of embedded credentials | Quantified: 1 WA token (19 scenarios), 2 Strapi tokens (16), 1 bot token (3) |
| LL - Anuncios read-only | Verified (GET only) |

## Open gaps

| Priority | Gap / question | Why it matters | Recommended evidence / owner |
|---|---|---|---|
| P0 | Rotation of WhatsApp, Strapi and bot tokens; inventory of where else they are used | Live credentials exposed in Make config and exports | Meta owner, Country Magazine tech team |
| P0 | No test environment; development executed in production | Regression and data-pollution risk | Agree strategy in `automations-development` |
| P1 | Main webhook authentication / Meta signature validation | Spoofed events possible | Firbot + Meta owner |
| P1 | Strapi content-type schemas and API-token permissions | Make-observed keys ≠ full model; write scope unknown | Read-only Strapi access or schema export |
| P1 | Strapi emitters of the 8 Make webhooks (lifecycle hooks, cron, website) | Needed to diagnose missing notifications | Client Strapi developers |
| P1 | Server logic of `/api/wpp-bot/mensajes` and `/api/wpp-bot/codigo` (conversation creation, coupon/variant) | Logging and coupon behaviour depend on it | Client Strapi developers |
| P1 | Error channel conflict (Gmail vs. Microsoft 365) and ownership of alert mailboxes | Alerts may be missed | Stakeholder + Firbot |
| P1 | Whether the contact-time window is still a business requirement (currently bypassed) | Templates sent at night | Business owner |
| P1 | Status of DLQ item in `LL - Onboarding Paso 3` and the 2026-11-05 failures | Possibly lost notifications | Firbot (read execution details) |
| P2 | Meta config: WABA, app ownership, template approval status/content, phone number quality | Recovery and template changes | Meta owner |
| P2 | OpenAI account ownership, model `gpt-6-luna` validity/cost, data-retention settings | Cost/compliance | Firbot / client |
| P2 | Who maintains `LL_PermissionsList` and approval process for admins | Admin can bulk-message | Client |
| P2 | Retention/consent policy for messages in Strapi, Make DS, OpenAI and e-mail alerts | Personal data | Client legal/business |
| P2 | Business owner and analysis of A/B test results | Decision follow-up | Client |
| P2 | Fate of unused/temporary assets (7 webhooks, 4227025, 030/031, Firbot tools, data structures) | Hygiene/security | Firbot + client approval |
| P2 | Dashboard implementation and its dependence on Make-written fields (e.g. hard-coded test data from Pedido Review) | Report accuracy | Client |
| P3 | Commercial trial/paid model rules | Avoid misdocumentation | Client |

**Current state vs proposals:** fixes for the findings in `knowledge/07_INCIDENT_REGISTRY.md` are proposals and belong in `automations-development`; none have been applied.
