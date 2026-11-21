---
status: Draft
last_modified: 2026-11-21
client_slug: weincenter-loerrach
---

# Onboarding gaps and verification checklist

## Priority checks

- [ ] Inspect Vivino Power Automate solution export ZIP (flows, triggers, connections, child desktop flows, error handling).
- [ ] Inspect Hawesko solution export ZIP (same areas).
- [ ] Confirm production flow IDs and Power Automate environment; no passwords or connector secrets in published repo.
- [ ] Confirm real Vivino step sequence (DPD then WEGA per historical guide, or WEGA then DPD per stakeholder narrative).
- [ ] Confirm current schedules: orchestration cadence; Vivino end-of-day shipping at 17:00; cleanup every 14 days.
- [ ] Verify tracking list exact names/IDs, SharePoint field IDs/data types and the shared Excel configuration workbook (stakeholder confirms both lists and workbook use one site).
- [ ] Verify both order-retrieval APIs from each solution export; identify Hawesko API endpoint, authentication owner and update mechanism.
- [ ] Check for other Excel/SharePoint dependencies not currently recalled by the stakeholder.
- [ ] Inspect retry safeguards and idempotency before deleting/resetting any tracking record.
- [ ] Identify physical Windows machine, session account, machine connectivity, support owner and unattended restrictions.
- [ ] Check exact licensing SKU and subscription; no unverified assumptions.
- [ ] Identify data sensitivity, source-of-truth fields, permissions and secure repository access.
- [ ] Identify current alert recipients and incident escalation ownership.
- [ ] Describe scope and automation coverage for Eurotax Declaration.
- [ ] Confirm main approval authority and track DPD API proposal in development backlog.

## Follow-up evidence to collect

1. Two solution export ZIPs, each with export date, solution version and target/source environment.
2. SharePoint list schema screenshots/exports for both tracking lists, including internal column IDs if possible.
3. Current package configuration workbook, with commercial/customer data redacted if required.
4. The physical machine specifications and PAD desktop-flow names/IDs.
5. Recent run-history evidence of success/failure and schedule triggers (sanitized).
6. Current DPD, WEGA, Vivino, Hawesko integrations docs and any documented manual recovery procedures.

## Recommended next detailed docs

- `knowledge/automations/vivino-orders-delivery.md`: trigger, stages, statuses, retries, error paths, I/O, owners, dependencies.
- `knowledge/automations/hawesko-orders-delivery.md`: same template after export inspection.
- `knowledge/schemas/vivino-orders-tracking.md`, `knowledge/schemas/hawesko-orders-tracking.md`: exact SharePoint schemas.
- `knowledge/systems/pad-windows-machine.md`: runbook and operational constraints.
- `knowledge/playbooks/failed-order-recovery.md`: *only* after safe/idempotent recovery validated.

## Suggested development workstream (separate from this knowledge repository)

Draft an evaluation brief for a DPD API migration: feasibility, credentials/authorization, endpoints, failure handling, migration approach, testing and rollback. Do not deploy or describe as production until the client explicitly approves and deployment is verified.
