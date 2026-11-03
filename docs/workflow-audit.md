# workflow-audit.yml

## Base Usage

```yml
workflow-audit:
  uses: init4tech/actions/.github/workflows/workflow-audit.yml@<commit sha>
```

Audits the calling repository's GitHub Actions workflows with
[zizmor](https://github.com/zizmorcore/zizmor): template injection, dangerous
triggers, credentials left on disk, and, with the run's token, whether each
action pinned to a commit really belongs to that action's repository.

It uploads a dependency report and never fails on a finding. The report holds:

- `summary.txt`: one line per finding, `rule<TAB>severity<TAB>file:line`, sorted.
- `zizmor.json`: zizmor's full output.

The run's step summary shows zizmor's plain output.

## Optional Parameters

### `runs-on`

**Description:** The runner, as JSON: a label string, or an object for a runner group.

**Type**: `string`

**Default Value:** `'"ubuntu-latest"'`

**Allowed values:** `'"blacksmith-2vcpu-ubuntu-2404-arm"'`, `'{"group": "init4-runners"}'`, and the like.

### `path`

**Description:** The directory of workflows to audit.

**Type**: `string`

**Default Value:** `.github/workflows`

### `artifact-name`

**Description:** The name of the uploaded report.

**Type**: `string`

**Default Value:** `dependency-report-workflows`

### `zizmor-version`

**Description:** The zizmor version to install. It is installed by
`taiki-e/install-action`, which checks the download against its manifest's
checksum.

**Type**: `string`

**Default Value:** `1.31.1`

## Permissions Required

- `contents: read`
