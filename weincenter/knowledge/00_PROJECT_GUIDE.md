---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Project Guide

## Purpose

Canonical technical documentation of Weincenter Lörrach's **currently verified** technical landscape. Proposed implementation and in-progress changes belong in a separate `automations-development/` repository, not here.

## Client overview

- Client: Weincenter Lörrach (legal entity/name to verify against an authoritative source).
- Industry: Wine sales and order fulfilment across marketplaces (user-reported current state).
- Primary marketplaces in automation scope: Vivino and Hawesko.
- Automation delivery/maintenance partner: Firbot (user-reported).
- Business contact: `<Business Owner / Main Client Contact>` (name/contact details kept in access-controlled directory).
- Primary communication: WhatsApp; email occasionally (user-reported).
- Main processing: order retrieval, invoicing in WEGA, carrier shipment creation in DPD, tracking/status updates.

## Scope

- Cloud flows and desktop flows in the client's Microsoft 365 tenant.
- Vivino and Hawesko order-delivery automations, WEGA, DPD, related SharePoint assets, physical Windows machine and operational guidance.
- Eurotax Declaration: partially automated; detailed scope unknown.
- The third French marketplace is outside the automation scope for now.

## Operating model

1. Start with [`02_SYSTEMS_REGISTRY.md`](02_SYSTEMS_REGISTRY.md), [`03_AUTOMATION_REGISTRY.md`](03_AUTOMATION_REGISTRY.md), [`04_DATA_ASSETS_REGISTRY.md`](04_DATA_ASSETS_REGISTRY.md).
2. Consult referenced evidence in [`../source-material/`](../source-material/) and future inspected [`../exports/`](../exports/).
3. Distinguish stakeholder-reported status from live or export verification.
4. Do not modify production systems via this repository; document deployed changes only after validation.

## Environments, access, and safety

- **Stakeholder-reported:** single Microsoft 365/Power Automate environment; no separate testing environment.
- **Stakeholder-reported:** PAD runs on a physical Windows machine kept powered on.
- **Historical source:** attended operation requires a logged-in, unlocked/available Windows session (Vivino user guide, pp. 4-5).
- **Unknown:** exact entitlements, licenses and connection owners. No evidence of unattended capacity.
- Never include passwords, tokens, or secrets in this repository or copied exports.
- Access permissions for repository: TODO: verify.

## Evidence and verification

- `source-material/User Guide - New Vivino Orders Delivery.pdf`: user-supplied operational guide; **historical source material**, NOT proof of live configuration.
- Current onboarding conversation, 2026-11-21: stakeholder-reported current operations; TODO: verify against production exports.
- Future Power Automate solution ZIPs: **not yet provided**. Inspect before treating resource names, exact schedules and actions as verified.

## Relation to development

`technical-knowledge` = observed and verified production state. `automations-development` = proposals and ongoing changes. DPD API migration is unapproved and MUST NOT appear as already deployed.
