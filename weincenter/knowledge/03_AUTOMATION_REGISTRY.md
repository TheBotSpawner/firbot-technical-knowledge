---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Automation Registry

## Registry

| ID | Canonical name | Platform | Reported status | Trigger | Outcome | Linked systems | Exact resource name | Evidence |
|---|---|---|---|---|---|---|---|---|
| `AUTO-ORD-001` | Vivino Orders Delivery | Cloud + PAD | Active (stakeholder) | Scheduled; hourly in historical guide | Retrieve orders, DPD shipments, WEGA invoices, track and update statuses | SYS-ORD-001, SYS-OPS-001, SYS-OPS-002, SYS-ERP-001, SYS-SHP-001, SYS-DATA-001 | `Vivino Orders Delivery - Orchestrator` shown in guide screenshot p.5; TODO: verify exact live name | Historical guide pp. 2-11 + user report |
| `AUTO-ORD-002` | Hawesko Orders Delivery | Cloud + PAD | Active (stakeholder) | Scheduled, multiple times daily; cadence unknown | Retrieve orders via Hawesko API, DPD shipments, WEGA invoices, tracking and status | SYS-ORD-002, SYS-OPS-001, SYS-OPS-002, SYS-ERP-001, SYS-SHP-001, SYS-DATA-001 | TODO: verify | Stakeholder-reported API retrieval (2026-11-21); export pending |
| `AUTO-TAX-001` | Eurotax Declaration | Partially automated, platform TODO | Active / partial scope (stakeholder) | TODO | Support tax declaration process | TODO | TODO: verify | User report |
| `AUTO-ORD-003` | Vivino end-of-day Shipped update | Cloud (historical) | Unknown - verification required | Guide: 17:00 daily | Confirmed -> Shipped in tracking/Vivino per SLA | SYS-OPS-001, SYS-ORD-001, SYS-DATA-001 | TODO: verify | Historical guide pp. 3-4 |
| `AUTO-ORD-004` | Vivino completed-order cleanup and backup | Cloud (historical) | Unknown - verification required | Guide: every 2 weeks | Archive eligible orders before removing them from tracking list | SYS-OPS-001, SYS-DATA-001 | Example only in guide: `Vivino Orders Delivery | Remove old orders`; TODO: verify | Historical guide pp. 7-8 |

## Vivino specifics from historical user guide

- Cloud retrieves eligible orders via API for all active merchants; the order is sequential by merchant, due to only one PAD machine. Examples listed: Germany, France, Netherlands, others (p. 3).
- State-machine examples: `New`, `In Processing`, `Confirmed`, `Shipped`, `Error` (pp. 2, 7, 11).
- Two distinct PAD flows: DPD/shipping and WEGA/invoicing (p. 2). Exact live names and flow IDs TODO: verify.
- Invoice number saved in SharePoint early to support recovery (p. 2).
- Emails sent for errors with context (guide pp. 9-10); current recipient and failure paths TODO: verify.
- **Conflict — verification required:** guide pp. 3-4 indicates DPD before WEGA; stakeholder described WEGA followed by DPD in a simplified summary. Do not interpret as a confirmed sequencing change.

## Hawesko details and shared dependencies

- **Stakeholder-reported current state (2026-11-21):** Hawesko order retrieval uses API, just as Vivino does. API endpoint, credentials owner, request logic, status-update method and marketplace-specific business rules are TODO: verify.
- Both automations use different order-tracking SharePoint lists **on the same site**, and both rely on the same `Package weight and dimensions.xlsx` configuration workbook.
- No other Excel dependency was recalled by the stakeholder; this is not evidence that no other dependency exists.

## Export intake

Expected: two solution ZIPs under `exports/`, one for each primary automation. Verify solution content, referenced connection names (not secrets), exact triggers, status transitions, shared flow dependencies, concurrency, retries and untracked external dependencies before detailed documentation.
