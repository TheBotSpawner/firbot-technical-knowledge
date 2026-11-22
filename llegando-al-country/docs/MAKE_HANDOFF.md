---
title: "Make and Claude Handoff"
status: Verified
last_modified: 2026-11-22
verification: "First Make-connected inventory completed 2026-11-22 (read-only)"
---

# Make Inventory and Claude Handoff

## Status

The first read-only, Make-connected inventory was completed on **2026-11-22** through the Make MCP connector (account user of the client organization). **No production resource was modified, activated, deactivated or executed**; only list/get operations were used (`organizations_list`, `scenarios_list`, `scenarios_get`, `hooks_list`, `connections_list`, `keys_list`, `data-stores_list`, `data-structures_list`, `executions_list`, `folders_list`, `users_me`).

> ⚠️ The Make MCP connector also exposes *tools that execute scenarios* (named `s<ID>_<scenario name>`, e.g. `LL - Subscenario Send Sticker`, `LL - Buscar Zona`, the RecMulti scenarios) and mutating tools (`scenarios_update`, `scenarios_run`, `data-store-records_*`, `hooks_*`…). **Calling an `s<ID>_…` tool runs the production scenario immediately** (sends WhatsApp messages, writes Strapi). Never call them for documentation.

## Results

| Area | Result | Where |
|---|---|---|
| Org/team | `Llegando al Country` 4655020 / `My Team` 1163364, zone us2, Pro plan | [02](../knowledge/02_SYSTEMS_REGISTRY.md) |
| Scenarios | 37 (29 active, 8 inactive), 0 folders | [03](../knowledge/03_AUTOMATION_REGISTRY.md), [Make index](../knowledge/automations/make/README.md) |
| Dependencies | Full `CallSubscenario` graph + HTTP re-injection edges | [Make index](../knowledge/automations/make/README.md) |
| Data Stores | 9, all schemas | [schemas/make](../knowledge/schemas/make/README.md) |
| Strapi | 9 endpoints/collections used; Anuncios read-only verified | [schemas/strapi](../knowledge/schemas/strapi/README.md) |
| Exports | 37 sanitized + manifest | [manifest](../exports/make/manifest.md) |
| Findings | 3 execution failures, 16 findings | [07](../knowledge/07_INCIDENT_REGISTRY.md), [security](SECURITY_NOTES.md) |

## Next session (read-only) — suggested sequence

1. Re-run `scenarios_list` for team 1163364; compare `lastEdit` with the manifest; re-export changed scenarios.
2. Read execution details of the failed executions and the DLQ item (read-only `executions_get-detail`), without replaying.
3. If read-only Strapi access is granted: export content-type schemas and API-token permissions; replace "Make-observed" field tables.
4. With the Meta owner: WABA/app/webhook/template inventory.
5. Update registries, gap summary and checklist.

## Practical separation

- Current state lives here. Fixes (token migration, webhook auth, time-window filters, `WichSpecialEvent` typo, Pedido Review log values, cleanup of tooling) go to `automations-development` once authorised.
- Never use the Firbot Blueprint Patcher or simulators as part of documentation work.
