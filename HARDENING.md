<!-- markdownlint-disable -->

# Hardening Report: Azure--aci-deploy/v1.1.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Azure--aci-deploy/v1.1.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow file uses action references pinned to mutable tags instead of full 40-character commit SHAs. In auto-triage-issues: `uses: larrylawl/Auto-Github-Issue-Labeller@v1.0` (tag). In defaultLabels.yml: `uses: actions/stale@v3` (tag, used twice). These can be silently updated to include malicious code.

Locations:

- `.github/workflows/auto-triage-issues:12`
- `.github/workflows/defaultLabels.yml:16`
- `.github/workflows/defaultLabels.yml:23`

### missing-permissions (severity: medium)

Workflow file has no top-level `permissions:` key and no job-level `permissions:` key on any job. Without explicit permissions, the workflow inherits the default broad permissions (typically `contents: write` for classic repos), violating the principle of least privilege.

Locations:

- `.github/workflows/auto-triage-issues:1`
- `.github/workflows/defaultLabels.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files in .github/workflows/: (1) Pinned larrylawl/Auto-Github-Issue-Labeller@v1.0 to SHA 3bf15b39ebddda551472f6de4c74083194ee8271 in auto-triage-issues; (2) Pinned both occurrences of actions/stale@v3 to SHA 98ed4cb500039dbcccf4bd9bedada4d0187f2757 in defaultLabels.yml; (3) Added top-level `permissions: { issues: write }` to auto-triage-issues; (4) Added top-level `permissions: { issues: write, pull-requests: write }` to defaultLabels.yml (the stale action needs both to mark issues and PRs). Original tags preserved as inline comments.

