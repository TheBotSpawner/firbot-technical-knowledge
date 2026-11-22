---
title: "Incident Registry"
status: Verified
last_modified: 2026-11-22
verification: "Make execution history (30-day retention) and live configuration reviewed 2026-11-22"
---

# 07 — Incident Registry

## Incidents (events that occurred)

No user-impacting production incident has been reported by stakeholders. Make keeps execution logs for 30 days; the failed executions found in that window are recorded below as **execution failures**, not confirmed incidents.

| Incident ID | Date | Summary | Affected | Severity | Status | Root cause | Evidence |
|---|---|---|---|---|---|---|---|
| `INC-LTC-001` | 2026-11-05 | Failed execution of main scenario (6 ops, 1.4 s) during the RecMulti rollout | AUTO-LTC-001 | Low (single execution) | Closed? — **TODO: verify** | Unknown (error detail not retrieved) | Make executions_list status=3 |
| `INC-LTC-002` | 2026-11-05 | `LL - RecMulti 1` failed with `DataError` ("'{object}' is not a valid array" in `map()`); run was started manually via Make MCP `scenarios_run` (development test in production) | AUTO-LTC-012 | Low | Presumably fixed (scenario edited until 2026-11-20) — **TODO: verify** | Mapping bug during development | Make executions_list, provenance `mcp / scenarios_run` |
| `INC-LTC-003` | Unknown (≤ 2026-11-22) | 1 execution of `LL - Onboarding Paso 3` waiting in incomplete executions (DLQ) | AUTO-LTC-024 | Low (one advertiser follow-up not sent) | Open | Unknown | scenarios_get `dlqCount=1` |

## Findings requiring follow-up (risks / defects observed in configuration — not incidents)

| Finding ID | Summary | Affected | Severity | Evidence label | Detail |
|---|---|---|---|---|---|
| `FIND-LTC-001` | Literal WhatsApp/Strapi/bot tokens in 19+16+3 scenario occurrences | many | **Critical (security)** | Confirmed from live system | [SECURITY_NOTES](../docs/SECURITY_NOTES.md) |
| `FIND-LTC-002` | No test environment; development, simulations and test deletes executed in production | all | High | Confirmed (execution provenance, Firbot tools) | [tooling](automations/make/housekeeping-and-firbot-tooling.md) |
| `FIND-LTC-003` | Contact-window filters bypassed by always-true OR groups (`test=test` / `Testing=Testing`) → templates sent at any hour; off-time queue unused | 016, 018, 019, 020, 021 | Medium | Confirmed config; effect = Inference | [outbound](automations/make/ll-outbound-notifications.md) |
| `FIND-LTC-004` | Processing lock in `LL_MessagesHistory` is not atomic (parallel executions) | 001 | Medium | Inference from config | [main](automations/make/ll-chatbot-recomendacion-de-servicios.md) |
| `FIND-LTC-005` | Main webhook without authentication | 001 | High (security) | Confirmed config | [SECURITY_NOTES](../docs/SECURITY_NOTES.md) |
| `FIND-LTC-006` | Webhook URLs stored in DS/hard-coded | 008-DS, 027, 034 | Medium | Confirmed | [SECURITY_NOTES](../docs/SECURITY_NOTES.md) |
| `FIND-LTC-007` | Alerting tied to a personal Microsoft account; stakeholder said "Gmail" | 007 | Medium | **Conflict — verification required** | [utilities](automations/make/shared-utility-subscenarios.md) |
| `FIND-LTC-008` | Privileged Firbot tooling (Blueprint Patcher, Strapi dump) left in prod team | 032–037 | Medium | Confirmed | [tooling](automations/make/housekeeping-and-firbot-tooling.md) |
| `FIND-LTC-009` | Revista call from AI route maps `WichSpecialEvent` (typo) — required input missing | 001 → 010 | Medium (functional) | Confirmed config; effect = Inference | [main](automations/make/ll-chatbot-recomendacion-de-servicios.md) |
| `FIND-LTC-010` | `LL - Pedido Review` logs outbound messages with hard-coded test name/phone/slug | 022 → Strapi `LL - WhatsApp Mensaje` | Medium (data quality, dashboard) | Confirmed config | [review](automations/make/ll-special-interaction-and-review.md) |
| `FIND-LTC-011` | `Nueva Opinion Anuncio` "Empty Data" alert condition is impossible (`total=1 AND total=5`) — missing data never alerted | 019 | Low | Confirmed config | [outbound](automations/make/ll-outbound-notifications.md) |
| `FIND-LTC-012` | Unused assets: 7 unattached webhooks (incl. `Onboarding-Paso-01`, no Paso 1 scenario), inert active scenario 4227025, inactive 030/031, unused data structures, `Reset` enum without route in 010 | various | Low (hygiene) | Confirmed | [Make index](automations/make/README.md) |
| `FIND-LTC-013` | Personal e-mails hard-coded as alert recipients | ~25 modules | Low/Medium (privacy) | Confirmed | [SECURITY_NOTES](../docs/SECURITY_NOTES.md) |
| `FIND-LTC-014` | Personal data sent to OpenAI; model value `gpt-6-luna` configured in most AI modules (validity/cost not verified) | 001–003, 006, 012, 016 | Medium (privacy/ops) | Confirmed config | [main](automations/make/ll-chatbot-recomendacion-de-servicios.md) |
| `FIND-LTC-015` | Duplicate "already contacted" state (`LL_RecommendationsMade` vs Strapi `mensajesEnviados`); single-recommendation path can append the same recommender twice | 005, 016 | Low | Confirmed / Inference | [data assets](04_DATA_ASSETS_REGISTRY.md) |
| `FIND-LTC-016` | `Delete Messages` parses dates with a pattern that no longer matches the field type | 013 | Low | Inference | [housekeeping](automations/make/housekeeping-and-firbot-tooling.md) |

## Support process gaps

- No formal maintenance contract/SLA; alert routing is per-module hard-coded e-mail.
- No runbook for DLQ handling; replaying executions re-sends WhatsApp messages to real users.
