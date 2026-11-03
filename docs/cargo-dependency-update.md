# cargo-dependency-update.yml

## Base Usage

```yml
cargo-dependency-update:
  needs: dependency-routine
  permissions:
    contents: write
    pull-requests: write
  uses: init4tech/actions/.github/workflows/cargo-dependency-update.yml@<commit sha>
  secrets:
    app-client-id: ${{ secrets.DEPENDENCY_APP_CLIENT_ID }}
    app-private-key: ${{ secrets.DEPENDENCY_APP_PRIVATE_KEY }}
```

Applies the Cargo updates that `dependency-routine.yml` decided to adopt now,
and keeps one pull request with them up to date. No model runs in this job.
It reads the routine's `decisions.json` and keeps only entries that:

- are `cargo` entries for a workspace listed in `manifests`;
- name a crate matching `^[A-Za-z0-9_-]{1,64}$`;
- give `from` and `to` as plain semver versions;
- have `from` still locked when the job runs.

For each it runs `cargo update -p <crate>@<from> --precise <to>`. Nothing is
built. The changed lockfiles are committed through the API with no author, so
GitHub signs the commit for the token's identity, and pushed to `branch`. One
pull request from that branch is opened, or updated if it is already open. Its
body lists each update with the routine's reason. The repository's CI and
merge rules decide whether it lands.

The routine writes decisions only on runs where it ran Claude and wrote the
summary issue, so a day with no new reports applies nothing.

## Optional Parameters

### `manifests`

**Description:** The `Cargo.toml` paths the routine may update, as passed to
`cargo-dependency-report.yml`. An entry for any other workspace is dropped.

**Type**: `string`

**Default Value:** `Cargo.toml`

### `decisions-artifact`

**Type**: `string`

**Default Value:** `dependency-decisions`

### `branch`

**Description:** The branch the updates are pushed to. Each run replaces its
contents, so the pull request always holds the latest decisions.

**Type**: `string`

**Default Value:** `dependency-routine/cargo`

### `max-updates`

**Description:** The most updates applied in one run.

**Type**: `number`

**Default Value:** `10`

### `runs-on`

**Type**: `string`

**Default Value:** `'"ubuntu-latest"'`

## Secrets

### `app-client-id` and `app-private-key`

A GitHub App with contents and pull-request write access on the repository.
GitHub starts no workflow for a pull request opened with a workflow's own
token, so without an App the pull request gets no CI until a person closes and
reopens it, and its body says so.

## Permissions Required

- `contents: write`
- `pull-requests: write`
