---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Data Assets Registry

## Registry

| ID | Type | Exact / working name | Platform | Business role | Owner | Sensitivity | Linked automations | Verification |
|---|---|---|---|---|---|---|---|---|
| `DATA-ORD-001` | List | `Vivino Orders Tracking` | SharePoint (Weincenter Lörrach – Intern) | Order-level state and execution tracking | Client (assumed) | Confidential (provisional) | AUTO-ORD-001, AUTO-ORD-003, AUTO-ORD-004 | Historical guide pp. 6-8; TODO: verify current schema |
| `DATA-ORD-002` | List | `Hawesko Orders Tracking` (working name, exact spelling TODO) | SharePoint | Hawesko order tracking | Client (assumed) | Confidential (provisional) | AUTO-ORD-002 | Stakeholder-reported only; TODO: verify name and schema |
| `DATA-ORD-003` | Excel configuration | `Package weight and dimensions.xlsx` | SharePoint Documents | Parcel size/weight rules for DPD | Client (assumed) | Internal (provisional) | AUTO-ORD-001; Hawesko dependency TODO | Historical guide pp. 8-9; TODO: verify |
| `DATA-ORD-004` | Archive folder | `Documents / Vivino Order Tracking / Orders Archive` | SharePoint | Retain backups of old orders deleted from operational list | Client (assumed) | Confidential (provisional) | AUTO-ORD-004 | Historical guide p. 8; TODO: verify current operation |

## Vivino Orders Tracking — known fields from guide (pp. 6-7)

Visible labels (NOT verified internal SharePoint column names/IDs):

| Display field | Meaning |
|---|---|
| Platform | Originating marketplace |
| Processed Date | Timestamp of bot processing |
| Order Code | Marketplace order ID/code |
| DPD Shipping Code | Carrier tracking/shipment code |
| Invoice Number | WEGA invoice ID/number |
| Products | Product description summary |
| Customer Name | Customer name |
| Company Name | Business customer name if applicable |
| Total Value | Order amount |
| Status | Workflow state |
| Notes | Free text about errors/manual actions |

SharePoint list URL (historical): `https://haltingerwinzereg.sharepoint.com/sites/WeincenterLrrach52-Intern/Lists/Vivino%20Orders%20Tracking`

## Package configuration columns (historical guide p. 9)

`Bottles in Parcel`, `Weight in KG`, `Length`, `Width`, `Height`. Workbook path from guide: `Documents / Vivino Order Tracking / Package weight and dimensions.xlsx`.

## Risks / gaps

- No confirmed live SharePoint column IDs, field types, validation, versioning, list IDs, file IDs, retention policy or owner.
- Sensitive operational and customer information may be present. Keep screenshots/data exports access-controlled, redact production personal data before broad sharing.
- Backup retention and deletion behavior need checks against actual flow.
