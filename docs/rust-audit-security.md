# rust-audit-security.yml

## Base Usage

```yml
rust-security:
  uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
```

This workflow runs `cargo audit` to check for security vulnerabilities in your Rust dependencies. When vulnerabilities are found, it automatically creates GitHub issues with detailed information about each advisory.

## Features

- **Automatic Issue Creation**: Creates GitHub issues for each security advisory
- **Deduplication**: Checks for existing issues to avoid duplicates
- **Customizable Issue Metadata**: Configure labels, assignees, and milestones
- **Advisory Filtering**: Ignore specific advisories when needed
- **Flexible Scheduling**: Run on a schedule, on push, or manually

## Optional Parameters

### `issue-labels`

**Description:** Comma-separated labels to apply to created issues

**Type**: `string`

**Default Value:** `security,dependencies`

**Allowed values:** Any valid GitHub label names, comma-separated

### `issue-assignees`

**Description:** Comma-separated GitHub usernames to assign to created issues

**Type**: `string`

**Default Value:** `''` (empty string, no assignees)

**Allowed values:** Valid GitHub usernames, comma-separated (e.g., `user1,user2`)

### `issue-milestone`

**Description:** Milestone name or number to assign to created issues

**Type**: `string`

**Default Value:** `''` (empty string, no milestone)

**Allowed values:** Valid milestone name or number in your repository

### `deny-warnings`

**Description:** Fail workflow on audit warnings (not just errors). By default, the workflow only fails on security errors.

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

### `ignore-advisories`

**Description:** Comma-separated advisory IDs to ignore. Useful for accepting known risks or false positives.

**Type**: `string`

**Default Value:** `''` (empty string, no advisories ignored)

**Allowed values:** Advisory IDs from RustSec database (e.g., `RUSTSEC-2021-0001,RUSTSEC-2021-0002`)

### `requires-private-deps`

**Description:** Requires private dependencies to be fetched, sets up ssh-agent

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

### `require-lockfile`

**Description:** Require a `Cargo.lock` file to be present and use the `--locked` flag

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

### `working-directory`

**Description:** Directory containing `Cargo.toml`. Useful for monorepos or non-root projects.

**Type**: `string`

**Default Value:** `.` (repository root)

**Allowed values:** Any valid directory path relative to repository root

## Optional Secrets

### `SSH_PRIVATE_KEY`

**Description:** The SSH private key to be used for private dependencies, required if `requires-private-deps` is set to `true`

### `SSH_PRIVATE_KEY_2`

**Description:** Additional SSH private key for private dependencies (optional)

### `SSH_PRIVATE_KEY_3`

**Description:** Additional SSH private key for private dependencies (optional)

## Scheduling Recommendations

This workflow is designed to run on a schedule to continuously monitor your dependencies for security vulnerabilities.

### Daily Check (Recommended for Active Projects)

```yml
on:
  schedule:
    - cron: '0 9 * * *'  # 9 AM UTC daily
  workflow_dispatch:  # Allow manual runs
```

### Weekly Check (Recommended for Most Projects)

```yml
on:
  schedule:
    - cron: '0 9 * * 1'  # 9 AM UTC every Monday
  workflow_dispatch:  # Allow manual runs
```

### Monthly Check (Low-Risk Projects)

```yml
on:
  schedule:
    - cron: '0 9 1 * *'  # 9 AM UTC on the 1st of each month
  workflow_dispatch:  # Allow manual runs
```

## Issue Management

### Issue Format

Created issues follow this format:

**Title**: `Security: RUSTSEC-YYYY-NNNN - [Advisory Title]`

**Body**: Includes package name, version, severity, description, patched versions, and links to the advisory.

### Deduplication

The workflow checks for existing issues with the same advisory ID in the title before creating new issues. This prevents duplicate issues on subsequent runs.

### Managing False Positives

If an advisory does not apply to your usage or you accept the risk, you have two options:

1. **Close the issue**: Simply close the GitHub issue. The workflow will not recreate it as long as it exists (even when closed).

2. **Ignore the advisory**: Add the advisory ID to the `ignore-advisories` parameter. This prevents the workflow from reporting the advisory at all.

```yml
with:
  ignore-advisories: 'RUSTSEC-2021-0001,RUSTSEC-2023-0042'
```

## Example Configurations

### Basic Configuration with Scheduling

```yml
name: Security Audit
on:
  schedule:
    - cron: '0 9 * * 1'  # Weekly on Monday
  workflow_dispatch:

permissions:
  contents: read
  issues: write

jobs:
  security-audit:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
```

### With Custom Labels and Assignees

```yml
jobs:
  security-audit:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      issue-labels: 'security,high-priority,dependencies'
      issue-assignees: 'security-team,project-lead'
      issue-milestone: 'Security Sprint'
```

### Strict Mode (Fail on Warnings)

```yml
jobs:
  security-audit:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      deny-warnings: true
```

### With Private Dependencies

```yml
jobs:
  security-audit:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      requires-private-deps: true
    secrets:
      SSH_PRIVATE_KEY: ${{ secrets.SSH_PRIVATE_KEY }}
```

### Monorepo Configuration

```yml
jobs:
  security-audit-api:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      working-directory: './packages/api'
      issue-labels: 'security,api'

  security-audit-cli:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      working-directory: './packages/cli'
      issue-labels: 'security,cli'
```

### Ignoring Known Issues

```yml
jobs:
  security-audit:
    uses: init4tech/actions/.github/workflows/rust-audit-security.yml@main
    with:
      ignore-advisories: 'RUSTSEC-2020-0071,RUSTSEC-2021-0145'
```

## Permissions Required

The workflow requires the following GitHub token permissions:

- `contents: read` - To checkout the repository
- `issues: write` - To create and check issues

These permissions must be set in the calling workflow:

```yml
permissions:
  contents: read
  issues: write
```

## Notes

- The workflow uses `continue-on-error: true` for the audit step to ensure issues are created even when vulnerabilities are found
- The final step checks the audit exit code and fails the workflow appropriately
- Issues are only created for vulnerabilities, not for warnings or informational messages
- The workflow uses the GitHub CLI (`gh`) to manage issues, which respects your repository's issue templates and automation
