# Tag History Audit

## Scope and finding

The checked-out ref database contains no surviving legacy tag refs, so the historical tag names below are reconstructed from the repository's deployment history, incident log, and old release notes. That absence is itself an audit failure: the team cannot use Git alone to verify the release identifiers recorded for production.

| Evidence | Specific problem | Impact on the team | Rollback / traceability risk |
| --- | --- | --- | --- |
| `version-1.0` | Uses a word prefix and omits the required `vMAJOR.MINOR.PATCH` shape. | Tooling and people cannot reliably compare it with semantic versions. | A responder may mistake it for an earlier or later release and select the wrong rollback commit. |
| `release_2` | Is a non-semantic, lightweight tag with no release annotation. | It carries neither intent nor a verified release record. | The incident log records that it pointed to an unsupported commit; rolling back to it can reintroduce defects. |
| `1.5.0` | Looks semantic but omits the required `v` prefix. | A query or automation that filters `v*` releases will silently skip it. | The apparent patch/minor ordering is incomplete, so the previous known-good release is ambiguous. |
| `v2-final-FINAL` | Is not a valid semantic version and encodes an unorderable, subjective status. | The tag cannot be sorted or compared as a release version. | Teams cannot determine whether it precedes or supersedes a normal `v2.0.0` during an outage. |
| `stable-build` | Is a mutable-sounding label rather than an immutable versioned release identifier. | “Stable” does not identify the shipped changes or release sequence. | It cannot establish a reproducible rollback point, especially if the label is moved or reused. |
| `latest-good` | Is a subjective alias, not a version or documented release. | Different operators can apply different meanings to “good.” | The deployment history records a production deployment from it without matching release notes, so audit evidence is missing. |
| `patch-new` | Does not state which version it patches or what compatibility level it has. | Reviewers cannot identify its predecessor or scope. | There is no deterministic way to choose it versus another patch while recovering production. |
| `v1.4.2` | Uses the preferred shape but has no recorded production commit or deployment mapping. | A correctly shaped name alone does not prove what shipped. | The deployment record says staging was only *assumed* to match it; a rollback could target the wrong artifact. |

## Corrective action

Legacy names are retained only as historical evidence in the documents above; they are not adopted as release refs. New releases use immutable, annotated `vMAJOR.MINOR.PATCH` tags and are recorded in `RELEASE-MAP.md` and `RELEASES.md`.
