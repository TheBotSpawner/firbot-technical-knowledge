---
title: "Verification Checklist"
status: Draft
last_modified: 2026-11-22
verification: "Initial baseline; partial validation"
---

# Verification Checklist

## Security, before sharing exports

- [ ] Rotate/revoke the WhatsApp Bearer credential(s) appearing in the submitted main blueprint.
- [ ] Review all HTTP modules and subscenarios for embedded credentials.
- [ ] Confirm approved secure Make connection/credentials mechanism; avoid literals in exports.
- [ ] Confirm `.gitignore` and repository access; perform secret scan before first push.
- [ ] Do not place customer chat transcripts, screenshots with phone numbers or private contact lists in Git.

## Make — read-only inventory

- [ ] Confirm correct client-owned Make organisation/team and authorised read access.
- [ ] List *all* scenarios and IDs: name, folder, status, trigger/schedule, owners.
- [ ] Confirm main scenario exact ID and compare current configuration with supplied blueprint.
- [ ] Trace all `CallSubscenario` calls and verify `SCN_*` references and exact resource names.
- [ ] Confirm children statuses, failure paths, retries, error alert coverage and dependencies.
- [ ] List all nine observed Data Stores and any others; capture IDs, schema, owners and scenario usage.
- [ ] Resolve Data Store ID `38022` conflicting labels; map `193869` and `193870`.
- [ ] Sanitize/inspect versioned blueprint exports; update `exports/make/manifest.md`.

## Strapi and other systems

- [ ] Validate exact API collection names, schemas, relations, field types, permissions and source-of-truth scope.
- [ ] Confirm **read-only** Make permissions/operations for `LL - Anuncios`.
- [ ] Map other relevant Strapi collections used by child scenarios.
- [ ] Confirm Meta WABA and phone config (without recording secrets) and non-Coexistence setup.
- [ ] Record OpenAI module models/prompt purposes securely, no real message samples.
- [ ] Verify Gmail technical-error notification ownership and escalation.
- [ ] Verify client's custom dashboard is Strapi-backed and clarify read paths.

## Operations / handoff

- [ ] Approve role placeholders, owner/maintainer boundaries and production change authority.
- [ ] Agree incident intake, monitoring, escalation, recovery and rollback playbooks.
- [ ] Address no-separate-test-environment risk with client-approved strategy.
- [ ] Confirm personal data handling, consent, retention and access constraints.
- [ ] Reconcile incidents and architecture decisions with owner(s).
- [ ] Check all canonical documents link properly and all IDs are stable/unique.
