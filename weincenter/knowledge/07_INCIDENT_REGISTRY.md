---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Incident Registry

## Initial registry

No specific dated production incidents were supplied during this onboarding. **Empty does not mean there have been no incidents.**

| ID | Date | Incident | Affected assets | Status | Evidence |
|---|---|---|---|---|---|
| — | — | No individual incidents documented yet | — | Initial/incomplete | TODO: interview, run histories, ticket exports |

## General failure modes in historical guide (NOT confirmed incidents)

- PAD session interrupted by a user, session locking or interactive interference.
- Vivino API errors, DPD website failures, WEGA connection failures or missing order data.
- Orders may stay `Error` or `In Processing`; alert email and tracking list can support investigation.
- Guide suggests, in some cases, removing a row to allow automatic retry. **Do not follow that recovery method without inspecting and validating current idempotency rules**: it can create duplicates or repeat invoices/shipments.

Source: historical Vivino guide pp. 4-5, 9-12.
