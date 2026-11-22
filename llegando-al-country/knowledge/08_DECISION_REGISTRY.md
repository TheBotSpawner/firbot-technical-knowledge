---
title: "Decision Registry"
status: Draft
last_modified: 2026-11-22
verification: "ADR-001..005 from onboarding; ADR-006..011 observed in live Make configuration 2026-11-22"
---

# 08 — Decision Registry

These are **observed architecture choices** evidenced by the current system. Dates, approvers and alternatives considered were not supplied; recording them is **not** a claim that a formal decision meeting took place. "Since" dates are Make creation/edit dates of the implementing scenarios.

| Decision ID | Since | Topic | Status | Current approach (evidence) | Consequences / follow-up |
|---|---|---|---|---|---|
| `ADR-LTC-001` | Unknown (main scenario created 2025-07-21) | WhatsApp-first service discovery | Observed, active | Nexo via WhatsApp Cloud API, custom webhook into Make | Meta config not inspected |
| `ADR-LTC-002` | Unknown | Make account ownership | **Verified** | Client-owned org 4655020 / team 1163364; Firbot edits scenarios | Same account hosts Firbot tooling (FIND-LTC-008) |
| `ADR-LTC-003` | Unknown | Data/platform boundary | **Verified** | Strapi is system of record; Make reads `servicios` only and writes recommendations/messages through REST and custom `wpp-bot` endpoints | Token permissions unverified |
| `ADR-LTC-004` | Unknown | No separate test environment | **Verified constraint** | Development and tests run in production (2026-11-05 provenance); RecMulti adds a `TestMode` flag as mitigation | High change risk (FIND-LTC-002) |
| `ADR-LTC-005` | 2026-02-24 | Technical notifications | **Verified, with conflict** | Central subscenario 4226818 sends e-mail via **Microsoft 365** (not Gmail) + optional WA apology | FIND-LTC-007 |
| `ADR-LTC-006` | 2025-08 → 2026-11 | Modular subscenario architecture | Observed | One webhook entry + on-demand subscenarios via `CallSubscenario` (sync for data-returning steps, async for logging/notices) | Shared logger/notifier are single points of failure |
| `ADR-LTC-007` | 2025-08 | Short-term conversation memory in Make Data Store | Observed | `LL_MessagesHistory` (≤10 records/user, 2-h purge) feeds AI prompts; Strapi keeps durable log | Non-atomic lock (FIND-LTC-004) |
| `ADR-LTC-008` | 2025-08 | AI as structured extractor, not free chat | Observed | `transformTextToStructuredData` modules output typed slots; routing done by Make filters; replies mostly templated text | Prompt changes require production edits |
| `ADR-LTC-009` | 2026-03 | Contact-time window for business-initiated templates with off-time queue | Observed but **bypassed** | `LL_OffTimeRecomendations` + `LL - Send Template On Time`; filters short-circuited by `test=test` | FIND-LTC-003 — decide whether window is still required |
| `ADR-LTC-010` | 2026-11-05 | Credentials via Make team variables for new scenarios | Observed (partial migration) | RecMulti + Firbot tools use `LL_WA_TOKEN` / `LL_STRAPI_TOKEN`; older scenarios still literal | Complete migration + rotation (FIND-LTC-001) |
| `ADR-LTC-011` | 2026-02-24 (edited 2026-11-06) | A/B testing of provider templates | Observed | Team variable `ABTesting` alternates `llegando_contacto_recomendados_a/_b`; `_c` when no category; variant id logged to Strapi | Results analysis owner Unknown |

## Not decisions (proposals or unknown)

- Formal maintenance retainer; separate test environment; automated documentation refresh — **not current state**.
- Removal of Firbot temporal tools — pending authorisation.
