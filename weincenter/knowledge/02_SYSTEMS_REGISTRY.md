---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Systems Registry

This registry records **stakeholder-reported** current architecture, not a live inspection. Every item requires validation against exported flows and/or production evidence.

| System ID | Exact / working name | Type | Reported status | Criticality | Role | Owner | Technical owner | Verification |
|---|---|---|---|---|---|---|---|---|
| `SYS-ORD-001` | Vivino | Marketplace | Active - Core | High (provisional) | Orders and order statuses | Client | TODO | User-reported + historical user guide; TODO: verify |
| `SYS-ORD-002` | Hawesko | Marketplace | Active - Core | High (provisional) | Orders and order statuses | Client | TODO | User-reported; TODO: verify |
| `SYS-OPS-001` | Power Automate | Cloud automation | Active - Core | Critical (provisional) | Scheduling, APIs, orchestration | Client tenant | Firbot (maintenance reported) | User-reported + historical guide; TODO: verify |
| `SYS-OPS-002` | Power Automate Desktop | RPA | Active - Core | Critical (provisional) | UI-based WEGA/DPD processing on one physical PC | Client | Firbot (maintenance reported) | User-reported + historical guide; TODO: verify |
| `SYS-ERP-001` | WEGA | ERP | Active - Core | High (provisional) | Invoice creation and number | Client | TODO | User-reported; TODO: verify |
| `SYS-SHP-001` | DPD | Shipping | Active - Core | High (provisional) | Shipments, label/tracking creation | Client | TODO | User-reported; TODO: verify |
| `SYS-DATA-001` | SharePoint | Lists / documents | Active - Core | High (provisional) | Order tracking and configuration files | Client | TODO | Historical guide + user-reported; TODO: verify |
| `SYS-IT-001` | Microsoft 365 | Identity / tenant | Active - Core | High (provisional) | Hosts flows, machines/connections and SharePoint | Client | TODO | User-reported; TODO: verify |

## Infrastructure, licenses and connections

- Windows machine: physical, powered on continuously according to user. Exact host name/OS, support owner, backups, reboot plan and machine connection identity unknown.
- PAD execution: **attended** in historical Vivino guide (pp. 4, 10), consistent with stakeholder description. Exact license SKU/subscription unknown. Do not assume Premium ($15) is active.
- Production and test separation: stakeholder confirms **none**. Document as current risk, not an incident.
- Connections, IDs, auth owners and third-party credentials: TODO: verify from exports + secure access review (never place secrets in docs).
