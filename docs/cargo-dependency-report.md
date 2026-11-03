# cargo-dependency-report.yml

## Base Usage

```yml
cargo-dependency-report:
  uses: init4tech/actions/.github/workflows/cargo-dependency-report.yml@<commit sha>
```

For each Cargo workspace named, reports the RustSec advisories that match its
lockfile, from `cargo deny check advisories`, and the semver-compatible updates
the lockfile could take, from `cargo update --dry-run`. Nothing is built and
the lockfile is not changed.

It uploads a dependency report and never fails on a finding. The report holds:

- `summary.txt`, sorted, with lines of two kinds:
  - `advisory<TAB>workspace<TAB>code<TAB>id<TAB>package`
  - `update<TAB>workspace<TAB>Updating name vX -> vY`
- `advisories-<workspace>.jsonl`: cargo-deny's JSON diagnostics.
- `updates-<workspace>.txt`: the update lines.

The workspace is the manifest's directory, with `/` as `_`, or `root`.

## Optional Parameters

### `manifests`

**Description:** Space-separated `Cargo.toml` paths, one per workspace.

**Type**: `string`

**Default Value:** `Cargo.toml`

### `deny-config`

**Description:** The cargo-deny config used for every workspace, so its
advisory ignores apply. Skipped when the file does not exist.

**Type**: `string`

**Default Value:** `deny.toml`

### `runs-on`

**Description:** The runner, as JSON: a label string, or an object for a runner group.

**Type**: `string`

**Default Value:** `'"ubuntu-latest"'`

### `artifact-name`

**Type**: `string`

**Default Value:** `dependency-report-cargo`

### `cargo-deny-version`

**Description:** The cargo-deny version to install, checked against
`taiki-e/install-action`'s manifest.

**Type**: `string`

**Default Value:** `0.20.2`

## Permissions Required

- `contents: read`
