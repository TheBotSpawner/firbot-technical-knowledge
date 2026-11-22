# Llegando al Country — Technical Knowledge

This repository is the **read-only, evidence-based technical baseline** for **Llegando al Country**, linked to Country Magazine, including its production WhatsApp assistant **Nexo**.

- **`technical-knowledge`** = verified current technical state, with provenance and open questions.
- **`automations-development`** = proposed changes, work in progress, fixes and feature development. Keep as a *separate repository*; it has **not** been created here.

**Current scope:** Make.com scenarios and Data Stores, WhatsApp Business Cloud API, OpenAI API, Strapi integration, Gmail error notifications and dependencies on the client's website/dashboard.

**Start here:** [`knowledge/00_PROJECT_GUIDE.md`](knowledge/00_PROJECT_GUIDE.md), then [`knowledge/01_SYSTEM_MAP.md`](knowledge/01_SYSTEM_MAP.md), [`knowledge/03_AUTOMATION_REGISTRY.md`](knowledge/03_AUTOMATION_REGISTRY.md) and [`docs/MAKE_HANDOFF.md`](docs/MAKE_HANDOFF.md).

## Repository layout

```text
knowledge/                Ten canonical baseline files + detail directories
exports/make/             Sanitised blueprint snapshots, manifest and private staging area
source-material/          Source inventory (avoid storing PII screenshots by default)
templates/                Templates for future system/automation/schema records
docs/                     Source hierarchy, gap register, checklist, handoff and security notes
CLAUDE.md                 Rules for any connected AI assistant
.gitignore                Excludes raw exports, credentials and sensitive files
```

## Status on 2026-11-22

- Nexo is **in production** with real users — **Confirmed by project stakeholder**.
- The uploaded main Make blueprint has been **inspected** to establish initial module routing and subscenario references. This is **not** proof that the same revision is deployed at this moment.
- The companion Make scenarios, full Strapi schemas, live permissions, tests and monitoring are **not fully verified**.
- No separate test environment is reported.

## Security first

**Do not commit unredacted Make blueprints.** The main blueprint supplied for onboarding contains **literal WhatsApp Bearer tokens** in HTTP modules. The original file and the screenshots were **intentionally not bundled** with this starter repository. The affected credential should be rotated and stored through appropriate secure Make connection/credential mechanisms. See [`docs/SECURITY_NOTES.md`](docs/SECURITY_NOTES.md).

Use `exports/make/private/` for temporary raw exports (ignored by Git); use `exports/make/sanitized/` only after automated and manual secret/PII review. Do not upload private exports to a public or shared repository.

## Initial authoring protocol

1. Read [`CLAUDE.md`](CLAUDE.md) and [`docs/SOURCE_HIERARCHY.md`](docs/SOURCE_HIERARCHY.md).
2. Connect to the *correct client-owned Make account* with read-only scope first.
3. Inspect every relevant current scenario, datastore, connections metadata and historical exports; avoid exposing credentials.
4. Update the registries with exact platform names and vendor IDs, maintaining stable canonical IDs.
5. Write focused detailed documents under `knowledge/automations/make/`, `knowledge/systems/` and `knowledge/schemas/`.
6. Record gaps and conflicts instead of guessing.
7. Change no live production resource as part of documentation.

See [`docs/VERIFICATION_CHECKLIST.md`](docs/VERIFICATION_CHECKLIST.md).
