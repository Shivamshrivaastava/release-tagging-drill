# Release Notes

## v1.1.1 — 2026-09-07

### Changed
- Normalized the Checkout service's runtime metadata to separate `SERVICE_NAME` from `SERVICE_VERSION`.
- Updated startup output to display the service name and version consistently.

**Rollback target:** `v1.1.0`, the previous known-good structured release.

## v1.1.0 — 2026-09-07

### Added
- Established the first approved Checkout service deployment baseline after the initial implementation.

### Changed
- Recorded a structured semantic release point for the existing Checkout service baseline.

**Rollback target:** `v1.0.0`, the initial known-good release.

## v1.0.0 — 2026-09-07

### Added
- Added the initial Checkout service placeholder implementation and repository documentation.

**Rollback target:** No earlier managed release exists; restore the pre-release backup or investigate the deployment artifact rather than selecting an unversioned legacy label.
