# Make Blueprint Exports

- `sanitized/` — 37 sanitized snapshots of every scenario in the Llegando al Country Make team, taken 2026-11-22. See [`manifest.md`](manifest.md) for hashes, status and redaction counts.
- `private/` — Git-ignored local staging for raw exports (`private/raw/<make-id>.json`). Raw files contain live credentials and personal data: never commit, share or upload them; delete when no longer needed or move to an approved vault.

File naming: `<exact-name-slug>__<make-scenario-id>__<YYYY-MM-DD>.sanitized.json`.

Each sanitized file is the full `scenarios_get` object (scenario metadata + `blueprint`) plus a `__sanitization__` block describing source and redaction counts.

Rules:
- Preserve module IDs, route topology, filters, mappings and interfaces; replace secrets/PII with `[REDACTED_*]` placeholders.
- Validate JSON after redaction and re-scan for tokens, e-mails, phones, webhook paths and names before committing.
- **Do not re-import sanitized exports** into Make — they are evidence, not deployable blueprints.
- Do not infer status from file existence; re-check the live Make environment.

## Refresh procedure (read-only)

1. List scenarios for team `1163364`; fetch each with `scenarios_get`.
2. Store raw JSON in `private/raw/`.
3. Run the sanitizer (same rules as the 2026-11-22 run), validate, scan, write new dated files, update `manifest.md` and the registries for any changed scenario.
