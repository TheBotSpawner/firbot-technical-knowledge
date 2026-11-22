---
title: "Nexo Main Make Scenario"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# AUTO-LTC-001 — LL - Chatbot Recomendacion de Servicios

## Summary

- **Purpose:** Nexo main inbound WhatsApp router and orchestration entry point.
- **Platform:** Make.com (client-owned account).
- **Business status:** **In production** (stakeholder-confirmed); ongoing improvements.
- **Export name:** `LL - Chatbot Recomendacion de Servicios` (exact inspected title).
- **Live vendor scenario ID:** **TODO: verify**. Do not confuse with referenced `SCN_*` child IDs.
- **Evidence:** user-provided, inspected JSON blueprint (2026-11-22). The original is excluded from Git because it contains plaintext credentials. Current live revision not independently verified.
- **Trigger (from inspected export):** Custom webhook labelled `WPP-Messages-Nexo-Webhook`, Make module `gateway:CustomWebHook` (`id=575`).
- **Ownership:** client Make account; Firbot scenario/integration maintainer.

## High-level behavior supported by export

1. Accept WhatsApp events from webhook; distinguish regular messages, admin mode and non-message events.
2. Inspect Make Data Store state to detect existing users/conversations and messages currently being processed.
3. Route multiple-contact recommendations through a dedicated child `SCN_6920256` where relevant.
4. Handle initial conversation and repeated-message response paths, including parallel delay child.
5. Classify or extract intents using OpenAI text-to-structured-data modules; route search/recommend/publication/magazine/special-event interactions.
6. Call specialised search/recommendation, logging, sticker, interaction and error-notification subscenarios.
7. Send WhatsApp replies via Meta Graph HTTP modules and call logging subscenario where configured.

**Not asserted yet:** exact end-to-end contracts of child flows, coverage/reliability of every route, active model names, deployment equivalence, or full persistence design.

## Observed main route families

- Regular Conversation, Admin Mode, Non-Message.
- Recomendación múltiple / No es recomendación múltiple.
- Conversation Starting, `isContacts`, Check If Doble Message, More Than 1 Message.
- Search by category/zone/service; `isBuscar`, `isRecomendar`, `isPublicar`, `isRevista`, `isOther`.
- Special events and emoji interactions.

## Dependencies

See [`../../03_AUTOMATION_REGISTRY.md`](../../03_AUTOMATION_REGISTRY.md) for referenced `AUTO-LTC-002..012` and their `SCN_*` IDs. Supporting assets include `LL_MessagesHistory`, `LL_PermissionsList` and two vendor datastore IDs not yet mapped to exact names.

## Error handling and operations

- Several `onerror` branches call `SCN_4226818`, an error-notification scenario; some responses include an apology over WhatsApp.
- The inspected export has **literal WhatsApp Bearer tokens in HTTP request headers**. This requires security remediation; no token strings retained here.
- Make runtime retry behaviour, dead-letter recovery, schedule, rate limiting, execution retention, actual error-email delivery: **TODO: verify**.

## Additional documentation required

- Exact incoming event payload shapes and message type handling.
- Inputs/outputs and synchronous vs async behaviour for every child subscenario.
- AI prompts, schema outputs, model settings and privacy treatment (redacted documentation only).
- State machine, double-message locking, reset, admin mode and race conditions.
- Strapi collection API endpoints and write scopes; read-only constraint for ads.
- Error classifications, alert recipients and recovery playbooks.
- Verification of current live revision and scenario IDs.

## Data classification

Confidential: contact details and message content are processed by the system. Store **no personal examples or secrets** in docs.
