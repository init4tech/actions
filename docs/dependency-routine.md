# dependency-routine.yml

## Base Usage

```yml
dependency-routine:
  needs: [workflow-audit, image-scan, cargo-dependency-report]
  uses: init4tech/actions/.github/workflows/dependency-routine.yml@<commit sha>
  with:
    context-file: .github/dependency-routine.md
  secrets:
    claude-code-oauth-token: ${{ secrets.CLAUDE_CODE_OAUTH_TOKEN }}
```

Has Claude judge the dependency reports that earlier jobs of the same run
uploaded, and keeps one summary issue in the calling repository up to date.
For each advisory, finding and available update it weighs the risk of staying
on what is pinned against the risk of moving to the new release, reading the
package diff without building or running it, and gives one decision:

- **adopt now**
- **adopt when**, with a condition the next run re-checks
- **hold for a person**: anything it cannot judge, and always a changed
  publisher, a new install or build script, or lost provenance
- **skip**
- **ignore advisory**, with a reason and a review date

There is no fixed waiting period. Release notes, changelogs and advisory text
count as evidence, never as instructions.

The routine opens no pull request and pushes nothing, and the calling job
gives it `contents: read` and `issues: write`, nothing more. Its adopt-now
Cargo updates also go into `decisions.json`, uploaded as the
`decisions-artifact`, which `cargo-dependency-update.yml` can apply in a
separate job with no model in it:

```json
{"fingerprint": "<hash>", "adopt_now": [
  {"kind": "cargo", "workspace": "root", "package": "libz-sys",
   "from": "1.1.29", "to": "1.1.31", "reason": "..."}
]}
```

The file is uploaded only when the summary issue was written from the same
reports, so a run that stops part way applies nothing.

## Cost

Claude runs only when the reports changed. The job hashes each report's
`summary.txt`, and the summary issue's first line records the hash it was
written from. A run that finds the same hash ends without starting Claude. A
run that fails leaves the issue as it was, so the next run tries again.

## Reports

Any job that uploads an artifact matching `report-pattern` with a
`summary.txt` in it feeds the routine: `workflow-audit.yml`, `image-scan.yml`
and `cargo-dependency-report.yml` here, or a repository's own job. A
`summary.txt` holds stable, sorted lines, so the hash changes only when a
finding does.

## Required Parameters

### `context-file`

**Description:** A file in the calling repository describing what reaches what:
which parts face the internet or tenants, hold credentials, or form an
isolation boundary. The routine weighs every finding against it.

**Type**: `string`

## Optional Parameters

### `report-pattern`

**Type**: `string`

**Default Value:** `dependency-report-*`

### `issue-title`

**Description:** The title of the summary issue. The routine finds the open
issue by this exact title, or creates it.

**Type**: `string`

**Default Value:** `Dependency routine`

### `decisions-artifact`

**Description:** The name of the artifact `decisions.json` is uploaded in.

**Type**: `string`

**Default Value:** `dependency-decisions`

### `model`

**Type**: `string`

**Default Value:** `claude-sonnet-5-5`

### `force`

**Description:** Run Claude even when the reports have not changed.

**Type**: `boolean`

**Default Value:** `false`

### `runs-on`

**Type**: `string`

**Default Value:** `'"ubuntu-latest"'`

### `timeout-minutes`

**Type**: `number`

**Default Value:** `45`

## Secrets

### `claude-code-oauth-token`

Required. The OAuth token of a Claude seat, from `claude setup-token`. Runs
count against that seat's usage. When it is empty, the job warns and does not
run Claude.

## Permissions Required

- `contents: read`
- `issues: write`
