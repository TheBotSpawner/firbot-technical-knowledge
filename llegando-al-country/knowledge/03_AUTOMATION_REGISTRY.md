---
title: "Automation Registry"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# 03 — Automation Registry

This is an **initial** inventory: the main scenario is reported live and its supplied export was inspected. Every other row below is **only a dependency observed within that blueprint**, not independent proof of an active deployed scenario. Use the connected Make environment to reconcile complete inventory, status, scenario IDs and exact names. **Do not assume this is the full scenario list.**

| Automation ID | Exact / observed name | Platform | Status | Criticality | Trigger | Purpose | Involved systems | Vendor scenario ID/reference | Detailed file |
|---|---|---|---|---|---|---|---|---|---|
| `AUTO-LTC-001` | LL - Chatbot Recomendacion de Servicios | Make.com | Active - Under Improvement | Critical | Webhook: WPP-Messages-Nexo-Webhook | Inbound message orchestration and routing | SYS-LTC-001 and linked APIs | TODO: live scenario ID | [detail](automations/make/ll-chatbot-recomendacion-de-servicios.md) |
| `AUTO-LTC-002` | LL - Buscar Zona | Make.com | Unknown — verify | Unknown | Call from main | Search zone | SYS-LTC-001 and linked APIs | SCN_2637689 | TODO |
| `AUTO-LTC-003` | LL - Buscar Categoría | Make.com | Unknown — verify | Unknown | Call from main | Search category | SYS-LTC-001 and linked APIs | SCN_2637692 | TODO |
| `AUTO-LTC-004` | LL - Buscar Servicio por Zona | Make.com | Unknown — verify | Unknown | Call from main | Search service by zone | SYS-LTC-001 and linked APIs | SCN_2637743 | TODO |
| `AUTO-LTC-005` | LL - Recomendar Servicio | Make.com | Unknown — verify | Unknown | Call from main | Recommendation flow | SYS-LTC-001 and linked APIs | SCN_2637777 | TODO |
| `AUTO-LTC-006` | LL - Admin Mode | Make.com | Unknown — verify | Unknown | Call from main | Administrator interaction path | SYS-LTC-001 and linked APIs | SCN_4133823 | TODO |
| `AUTO-LTC-007` | Envio de Notificaciones de Error Chatbots | Make.com | Unknown — verify | Unknown | Error handling call | Technical error notifications | SYS-LTC-001 and linked APIs | SCN_4226818 | TODO |
| `AUTO-LTC-008` | LL - Log Message | Make.com | Unknown — verify | Unknown | Call from main | Entry/exit message logging | SYS-LTC-001 and linked APIs | SCN_5421473 | TODO |
| `AUTO-LTC-009` | LL - Subscenario Send Sticker | Make.com | Unknown — verify | Unknown | Call from main | Sticker interactions | SYS-LTC-001 and linked APIs | SCN_5694920 | TODO |
| `AUTO-LTC-010` | LL - Subscenario Special Interaction | Make.com | Unknown — verify | Unknown | Call from main | Special interactions | SYS-LTC-001 and linked APIs | SCN_5695064 | TODO |
| `AUTO-LTC-011` | Sleep n Seconds | Make.com | Unknown — verify | Unknown | Call from main | Asynchronous wait for message handling | SYS-LTC-001 and linked APIs | SCN_5892850 | TODO |
| `AUTO-LTC-012` | Recomendación múltiple (label from main call; exact subscenario name TODO) | Make.com | Unknown — verify | Unknown | Call from main | Multiple-contact recommendations | SYS-LTC-001 and linked APIs | SCN_6920256 | TODO |

## Findings from the inspected main blueprint

- Starts with a WhatsApp message webhook and branches into regular conversation, admin and non-message event paths.
- Contains filters for new/ongoing conversations, text, button and contacts payloads, repeated messages, multi-contact recommendations, and search/recommend/publication/magazine intents.
- References eleven distinct `SCN_*` subscenarios. Exact names are available in metadata for most, but `SCN_6920256` has only the call label in the supplied blueprint.
- References OpenAI text-to-structured-data modules, Make Data Stores, direct WhatsApp HTTP calls, message logging and notification subscenarios.
- The source export is **not included** due to plaintext credentials.

## Items for live inventory

- All current scenarios, active/disabled status, owners, schedules, inputs and outputs, exact vendor IDs.
- Differences between current live main and inspected blueprint (export revision/timestamps not sufficient to prove deployment).
- Connections, retry logic, idempotency, error handlers, message persistence and monitoring.
- Whether additional flows run on schedules (follow-up, coupons, conversion, billing, etc.) — **do not assume** they exist because Strapi has similarly named fields.

**Source:** stakeholder account and inspected main Make blueprint supplied 2026-11-22.
