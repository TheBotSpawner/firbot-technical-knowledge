---
title: "Verification Checklist"
status: Draft
last_modified: 2026-11-22
verification: "Updated after live Make inventory 2026-11-22"
---

# Verification Checklist

## Security, before sharing exports

- [ ] Rotate/revoke the WhatsApp token (present in 19 scenarios) — *owner: Meta app owner*.
- [ ] Rotate the two Strapi API tokens and the `X-Bot-Token` — *owner: Country Magazine tech team*.
- [x] Review all HTTP modules and subscenarios for embedded credentials (done 2026-11-22, see `docs/SECURITY_NOTES.md`).
- [ ] Migrate all scenarios to one managed credential mechanism.
- [x] `.gitignore` covers raw exports (verified with `git check-ignore`); sanitized exports scanned before commit.
- [ ] Human review of sanitized exports before sharing outside Firbot.
- [x] No chat transcripts, phone numbers or contact lists committed (design samples removed from exports).

## Make — read-only inventory

- [x] Confirm org/team: `Llegando al Country` (4655020) / `My Team` (1163364), single team, no private spaces.
- [x] List all scenarios: 37 (29 active / 8 inactive), names, IDs, status, schedules, webhooks; no folders.
- [x] Main scenario ID 2505419; live blueprint exported (onboarding JSON superseded).
- [x] Trace all `CallSubscenario` edges and verify targets exist and are active.
- [x] Error paths, retries (`Break`), DLQ settings and alert coverage documented.
- [x] All 9 Data Stores: IDs, structures, usage; 38022/193869/193870 resolved.
- [x] Sanitized exports + manifest with SHA-256.
- [x] Webhooks (17) and connections (5) inventoried; unattached hooks identified.
- [ ] Read execution details of the 2 failed executions (2026-11-05) and the Onboarding Paso 3 DLQ item.
- [ ] Confirm team variable values exist/are current (`LL_WA_TOKEN`, `LL_STRAPI_TOKEN`, `ABTesting`) without recording them.
- [ ] Confirm with Firbot whether `Delete Messages` date parsing works (execution log).

## Strapi and other systems

- [ ] Validate full collection schemas, relations and token permissions (no Strapi access in this session).
- [x] **Read-only** operations for `LL - Anuncios` (`/api/servicios`) confirmed from Make side.
- [x] Map other Strapi collections used by Make (barrios-agenda, categorias-de-servicios, grupos-categorias, opiniones, wpp-bot endpoints).
- [ ] Identify Strapi emitters for the 8 Make webhooks.
- [ ] Confirm Meta WABA/app/webhook config and non-Coexistence setup; template approval status.
- [x] OpenAI modules: purposes, models, output schemas documented (no real samples).
- [ ] Resolve Gmail vs. Microsoft 365 error-channel conflict and mailbox ownership.
- [ ] Verify the client dashboard reads Strapi message/conversation data.

## Operations / handoff

- [ ] Approve role placeholders, change authority and production change process.
- [ ] Incident intake, DLQ/replay runbook, rollback approach (Make scenario version history).
- [ ] Address the no-test-environment risk (`TestMode` exists only in RecMulti).
- [ ] Personal data handling, consent, retention.
- [ ] Decide on removal of Firbot temporal tools and unused assets.
- [x] Canonical documents cross-linked; IDs unique (see `knowledge/06_NAMING_AND_ID_CONVENTIONS.md`).
