# Make Blueprint Exports

Put future reviewed, **sanitised** scenario snapshots in `sanitized/` and update [`manifest.md`](manifest.md). Never commit raw Make exports without a secrets + personal-data scan.

Suggested naming for sanitized files: `<exact-name-slug>__<vendor-scenario-id>__<YYYY-MM-DD>.sanitized.json`.

Rules:
- Preserve module IDs, route topology, filters and input/output schema where possible.
- Replace bearer credentials, API keys, webhook secrets and private records with literal placeholders such as `[REDACTED]`.
- Confirm that redaction did not break JSON syntax; **do not re-import sanitised exports as deployable blueprints**.
- Record source date, actual current scenario ID, last compared-to-live date, inspection reviewer, redaction status and SHA-256 of **sanitized** file only.
- Raw exports may be temporarily inspected inside `private/` (ignored by Git) under client-approved policy. For strong confidentiality, use an approved secure storage system rather than local Git working copies.
- Do not infer statuses from file existence; inspect the live Make environment.
