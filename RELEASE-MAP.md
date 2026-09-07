# Release Map

This ledger maps immutable annotated release tags to the commits selected for deployment. The date is the annotated-tag creation date (2026-09-07); commit hashes are abbreviated only for readability and can be expanded with `git rev-parse <tag>`.

| Version (tag) | Commit (short hash) | Date | What Shipped |
| --- | --- | --- | --- |
| `v1.0.0` | `ff1fb9a` | 2026-09-07 | Initial Checkout service baseline: repository documentation and placeholder Checkout service implementation. |
| `v1.1.0` | `c17d4c4` | 2026-09-07 | Checkout service release baseline approved for deployment; this commit records the first structured release point after the initial implementation. |
| `v1.1.1` | `82535d9` | 2026-09-07 | Checkout service metadata and startup output were normalized to use `SERVICE_NAME` and `SERVICE_VERSION`. |

## Traceable rollback procedure

Use the version sort to identify the deployed release and its immediate prior release, then check out the approved known-good tag before rebuilding and redeploying the artifact:

```bash
git fetch --tags origin
git tag --sort=-v:refname        # the sortable release history
git show --no-patch --format=fuller v1.1.1
git checkout v1.1.0              # roll back to the last known-good tag, then redeploy
```

Because each release is an immutable annotated semantic tag mapped to a commit and release notes, `v1.1.0` resolves to one precise source state and is reproducible by any responder. The former labels such as `release_2` and `latest-good` did not consistently identify a version, commit, or deployment record, so choosing a rollback target was guesswork.
