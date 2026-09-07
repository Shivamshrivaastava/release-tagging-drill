# Versioning Convention

## Semantic versioning

Production releases use semantic versions in the form `MAJOR.MINOR.PATCH`.

- **MAJOR** increments for backward-incompatible API, configuration, or behavior changes. Example: `v1.4.2` → `v2.0.0` when a checkout API removes a supported request field.
- **MINOR** increments for backward-compatible functionality. Example: `v1.4.2` → `v1.5.0` when a compatible payment-status endpoint is added.
- **PATCH** increments for backward-compatible bug fixes only. Example: `v1.4.2` → `v1.4.3` when checkout timeout handling is corrected without changing the API.

## Tag format

Every final production release is named exactly `vMAJOR.MINOR.PATCH`, where each component is a non-negative integer. For example: `v1.1.0`.

## Release-tag type

Release tags **must be annotated**. An annotated tag records the tagger, timestamp, and a human-readable release message in Git, making the release auditable independently of external tooling.

```bash
git tag -a v1.1.0 -m "Release 1.1.0: describe the shipped, backward-compatible change"
```

Lightweight tags are not permitted for production releases, rollback targets, or deployment records.

## Pre-releases

Release candidates and betas append a semantic pre-release suffix, for example `v1.5.0-rc.1` or `v1.5.0-beta.1`. Pre-releases are also annotated tags and sort before the corresponding final release: `v1.5.0-rc.1` precedes `v1.5.0`. A pre-release is not a production rollback target unless it has been explicitly approved and recorded as such.
