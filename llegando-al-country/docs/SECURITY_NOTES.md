---
title: "Security Notes"
status: Verified
last_modified: 2026-11-22
verification: "Confirmed from live system (Make API, read-only) on 2026-11-22"
---

# Security Notes

No secret value, webhook URL, e-mail address or phone number is reproduced in this repository. Counts below come from scanning the 37 live blueprints on 2026-11-22.

## FIND-LTC-001 — Literal credentials embedded in production scenarios (confirmed, live)

The onboarding finding (tokens in the main blueprint) is **confirmed in the current live configuration and is wider than reported**:

| Credential (type only) | Distinct values | Scenarios containing it | Of which active |
|---|---|---|---|
| WhatsApp Cloud API access token (`Authorization: Bearer EAA…`) | 1 | 19: 2505419, 2637692, 2637743, 2637777, 4133823, 4137315, 4141246, 4222809, 4226818, 4378165, 4469351, 4469369, 5625466, 5694920, 5695064, 5822771, 5822780, 5822785, 5892850 | 18 |
| Strapi API token (`Authorization: Bearer <256 hex>`) | 2 | 14 (token A): 2505419, 2637689, 2637692, 2637743, 2637777, 4222809, 4227025, 4378165, 4469351, 4469369, 5625466, 5695064, 5822780, 6477190; 2 (token B): 2637777, 4227025 (in fallback/orphan modules) | 13 / 2 |
| Strapi custom bot token (`X-Bot-Token`) | 1 | 3: 2637743 (orphans), 4222809, 5421473 | 3 |

Exposure surface: anyone with access to the Make team (or to any exported blueprint, execution log or the onboarding JSON) can read these values. Exposure ≠ proven misuse (**Unknown**).

**Required action (authorised owners only — not performed here):** rotate the WhatsApp token (Meta app/WABA owner) and both Strapi tokens + bot token (Country Magazine technical team); then replace literals with a centrally managed reference (the RecMulti scenarios already use team variables `LL_WA_TOKEN` / `LL_STRAPI_TOKEN`). Rotation without first updating all 19/14/3 scenarios will break production.

## Other security findings

| ID | Finding | Evidence | Risk |
|---|---|---|---|
| FIND-LTC-005 | Main webhook `WPP-Messages-Nexo-Webhook` (2623296) has no API-key/signature check; Meta `X-Hub-Signature-256` is not validated | Hook config `apikey: []`; no validation module | Anyone with the URL can inject fake WhatsApp events (triggering AI calls, Strapi writes and outbound messages). The URL is also hard-coded in RecMulti 3 and the Firbot simulator. |
| FIND-LTC-006 | Webhook URLs stored in Data Store records (`LL_OffTimeRecomendations.WebhookToSend`) and hard-coded in scenarios | Blueprints | URLs act as bearer secrets. |
| FIND-LTC-007 | Error alerting depends on an individual's Microsoft 365 OAuth connection (`LMelman Firbot Connection`, 5431897) | Connection list | Alerting stops if the person leaves/revokes; e-mails carry error text that may include user messages. |
| FIND-LTC-008 | `Firbot - Blueprint Patcher` + Make API key connection (12169302) can rewrite any scenario; `Firbot - Consulta Strapi` copies Strapi data into `Firbot_PatcherLog` | Blueprints 6919674, 6920671 | Privileged tooling left in the production team (inactive). |
| FIND-LTC-013 | Personal e-mail addresses of Firbot/client staff hard-coded as alert recipients in ~25 modules | Blueprints | Personal data in configuration; recipient changes require editing every scenario. |
| FIND-LTC-014 | Personal data processed by OpenAI (last ≤10 messages, contact cards) | Main scenario prompts | Data-processing/consent position **Unknown**. |
| — | 4 unused WhatsApp-app webhooks with trivial verify tokens; one references a connection ID (4524873) absent from the team's connection list | hooks_list | Hygiene; unused attack surface. |
| — | Design-time sample bundles in blueprints contain real names, phones, e-mails, coupon codes and Mercado Pago references | Raw blueprints | Removed in sanitized exports; raw exports must stay out of Git. |

## Repository controls applied in this session

- Raw blueprints kept only in `exports/make/private/raw/` (ignored by `.gitignore`, verified with `git check-ignore`).
- Sanitized exports: tokens, webhook paths, e-mails, phone numbers, person names, user identities and all design-time samples replaced by `[REDACTED_*]`; scanned afterwards for `EAA…`, 64+ hex strings, `@`, webhook paths and known names (0 hits).

## Follow-up checklist

- [ ] Rotate WhatsApp token; confirm token type (system-user vs. user) and scopes with Meta owner.
- [ ] Rotate Strapi API tokens A and B and the `X-Bot-Token`; review Strapi token permissions (read-only for `servicios`?).
- [ ] Move all credentials to one managed mechanism; remove literals from the 19 + 16 + 3 scenario occurrences.
- [ ] Add authentication/verification to the main webhook (or a validation step) and rotate its URL afterwards (update RecMulti 3 + Meta app).
- [ ] Replace the personal Microsoft connection with a service mailbox; centralise recipients (e.g. team variable).
- [ ] Remove/archive Firbot dev tooling and purge `Firbot_PatcherLog` after approval.
- [ ] Confirm policy for sharing exports with AI assistants (this session read blueprints containing secrets via the Make MCP).
