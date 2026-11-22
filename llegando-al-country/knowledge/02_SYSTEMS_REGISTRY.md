---
title: "Systems Registry"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 02 — Systems Registry

IDs are repository-specific and **not** vendor resource IDs.

| System ID | Exact platform / system | Role | Status | Criticality | Owner / technical maintainer | Data handled | Connected systems | Verification |
|---|---|---|---|---|---|---|---|---|
| `SYS-LTC-001` | Make.com — Llegando al Country account | Nexo orchestration / Data Stores | Active - Core | Critical | Client owns account; Firbot maintains scenarios | Messages, workflow state, API interactions | 002, 003, 004, 005 | Stakeholder + Make screenshot + inspected main export |
| `SYS-LTC-002` | Strapi — `admin.countrymagazine.com.ar` | Domain records / service listings / bot logs | Active - Core | Critical | Country Magazine technical team | Providers, recommendation details, users, messages, ads, payment-linked entities | 001, 006 | Stakeholder + UI screenshots |
| `SYS-LTC-003` | WhatsApp Business Cloud API | End-user messages / notifications | Active - Core | Critical | Client ownership/configuration TODO; Firbot integration | Messages, phone IDs, contact profiles | 001 | Stakeholder + inspected Make HTTP/webhook config |
| `SYS-LTC-004` | OpenAI API | Text processing / AI extraction | Active | High | API account owner TODO; Firbot integration | Conversation inputs/AI outputs | 001 | Stakeholder + inspected Make module types |
| `SYS-LTC-005` | Gmail | Technical error notifications | Active | Medium | Notification mailbox owner TODO; Firbot error-handling flow | Diagnostic alerts | 001 | Stakeholder + notification subscenario references |
| `SYS-LTC-006` | Country Magazine / Llegando al Country website and custom dashboard | Ads discovery, message/stats UI | Active - Core | High | Country Magazine technical team | Strapi-derived operational/business data | 002 | Stakeholder; dashboard implementation not inspected |

## Outstanding system details

- **TODO: verify:** exact Make organisation and team ID from authoritative account admin; screenshot URL alone is insufficient.
- **TODO: verify:** actual Strapi version, hosting, database engine, public/private API scopes, endpoint restrictions and connection ownership.
- **TODO: verify:** Meta WABA ID, phone-number ID, app ownership, webhook subscriptions and token rotation status. No credentials in docs.
- **TODO: verify:** OpenAI model(s), project ownership, request limits, retention policy and error handling.
- **TODO: verify:** error mailbox identity and notification routing. Do not infer from browser tab labels.
- **TODO: verify:** client dashboard implementation, availability/monitoring and identity/access controls.
