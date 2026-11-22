# Exports

This folder is an **evidence staging area**, not executable deployment tooling. Do not use it to import/run changes into live environments.

- `make/private/`: ignored local raw exports and other sensitive source artifacts. **Never commit**.
- `make/sanitized/`: versioned, inspected and approved sanitized blueprint snapshots.
- `make/manifest.md`: export inventory, source evidence and inspection status.

The main JSON supplied during onboarding was **not added** because it contained plaintext WhatsApp credentials. See `../docs/SECURITY_NOTES.md`.
