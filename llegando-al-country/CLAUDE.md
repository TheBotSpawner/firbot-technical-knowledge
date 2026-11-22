# Claude Code / AI Assistant Instructions — Llegando al Country

## Mission and boundaries

This is the **documentation repository** for Llegando al Country and Nexo. Document **current verified state**, not intended future behavior. **Never** create, edit, enable, disable or execute production scenarios, alter Strapi records, call the WhatsApp API, rotate credentials or edit other external resources merely to improve documentation. Ask for explicit approval in an appropriate development workflow before any mutation.

- `technical-knowledge`: current state, documentation-only.
- `automations-development`: improvements, fixes and proposed state (separate sibling workspace if established).

## Evidence priority

1. Current live-system evidence observed with authorised read access.
2. Inspected export with timestamp, path and scenario/vendor ID.
3. Current canonical documentation.
4. Confirmed stakeholder requirements or operational testimony.
5. Other source material, recent tickets, historical documentation.
6. Explicitly labelled inference; general platform knowledge last.

Use explicit labels: **Confirmed from live system**, **Confirmed from inspected export**, **Confirmed from canonical documentation**, **Confirmed requirement**, **Historical**, **Inference**, **Unknown**, **TODO: verify**, **Conflict — verification required**.

## First Make-connected session

1. Confirm that the connected organisation/team belongs to **Llegando al Country**; do not accidentally inventory Firbot's own Make account or any other customer.
2. Start with *read-only* discovery: list scenarios, scenario IDs, active status, folders, schedules/webhooks, dependencies, Data Stores, and scenario inputs/outputs. Do not run or mutate scenarios.
3. The starter registry already contains **provisionally allocated canonical IDs**. Reuse them when the resource matches; never silently renumber, duplicate or change platform IDs.
4. Map all `CallSubscenario` references and reconcile them against live scenario names and statuses.
5. Track ownership and access permissions **without obtaining or storing secrets**.
6. Inspect Strapi schemas via approved read-only access if available; otherwise clearly distinguish UI screenshot fields from full API schema.
7. Update canonical registries and detailed docs only as findings are corroborated. Keep a source/evidence section per document, including inspection date and path/URL or ID.
8. Update `exports/make/manifest.md`, `docs/GAP_SUMMARY.md` and `docs/VERIFICATION_CHECKLIST.md` after inventory.

## Security / confidentiality

- The onboarding blueprint **contains embedded bearer credentials**. Treat all exported JSON as sensitive until reviewed; rotate exposed credentials through the authorised security process.
- Raw exports belong in ignored `exports/make/private/` or a secure approved vault, **not Git**.
- Sanitised exports belong in `exports/make/sanitized/` only after review; preserve scenario structure while replacing secrets with placeholders.
- **Never** copy token values, API keys, service credentials, customer phone numbers, private message contents, or sample customer profiles into Markdown, commit messages or chat summaries.
- Avoid presenting personal names, email addresses or phone numbers in `knowledge/05_CONTACTS_AND_ROLES.md`; use role placeholders and link a separate controlled contact directory if needed.

## Editing rules

- Read registry first, then matching detailed docs and current evidence.
- Keep exact platform names (`LL_RecommendationsMade`, `LL - WhatsApp Mensaje`, etc.) alongside canonical IDs. Never rename live resources for tidiness.
- Use English for documentation, YAML frontmatter with `status` and `last_modified: YYYY-MM-DD`, and relative links.
- Record facts, unknowns, known conflicts, incident evidence and operating decisions in their respective registries.
- Never infer an automation is active just because the main blueprint calls its ID.
- Do not make proposed maintenance contracts or separate test environments appear to exist already.

## Documentation workflow

**Read → Search → Analyse → Explain → Recommend → Document verified evidence**.

If implementation is needed: document the proposed change in the separate `automations-development` workspace; after an authorised deployment is verified, update this repository.
