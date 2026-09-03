<!-- markdownlint-disable -->

# Hardening Report: Azure--aci-deploy/v1.1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--aci-deploy/v1.1.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file uses `actions/stale@v3` (a mutable tag reference) in two steps. These should be pinned to a full 40-character commit SHA to prevent supply-chain attacks. Failing references: `uses: actions/stale@v3` (line 16) and `uses: actions/stale@v3` (line 27).

Locations:

- `.github/workflows/defaultLabels.yml:16`
- `.github/workflows/defaultLabels.yml:27`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the only job (`build`) also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. A minimal permissions block (e.g. `permissions: issues: write` for a stale-issue action) should be added.

Locations:

- `.github/workflows/defaultLabels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/defaultLabels.yml: (1) Pinned both `actions/stale@v3` references to the full SHA `98ed4cb500039dbcccf4bd9bedada4d0187f2757` with `# v3` comments. (2) Added a top-level `permissions:` block with `issues: write` and `pull-requests: write` — the minimal permissions required for the stale action to label and manage stale issues and PRs.

