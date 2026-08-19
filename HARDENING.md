<!-- markdownlint-disable -->

# Hardening Report: sparksp--elm-review-action/v1.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sparksp--elm-review-action/v1.1.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two `uses:` references in `.github/workflows/test.yml` pin to the mutable tag `@v2` instead of a full 40-character commit SHA. This exposes the workflow to supply-chain attacks if the tag is moved. Affected lines: `uses: actions/checkout@v2` (build job, line 13) and `uses: actions/checkout@v2` (test job, line 21).

Locations:

- `.github/workflows/test.yml:13`
- `.github/workflows/test.yml:21`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/test.yml` has no top-level `permissions:` key, and the `build` job has no job-level `permissions:` key. Without explicit permissions, the job inherits the default (potentially broad) token permissions. Only the `test` job defines job-level permissions (`checks: write`). The `build` job must also declare explicit minimal permissions, or a top-level `permissions:` block should be added to restrict all jobs by default.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/test.yml: (1) Pinned both `actions/checkout@v2` references to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e # v2`. (2) Added top-level `permissions: {}` to restrict all jobs by default, and added explicit `permissions: {}` to the `build` job. The `test` job already had minimal `checks: write` permissions.

