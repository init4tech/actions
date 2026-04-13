# release-crates.yml

## Base Usage

```yml
release-crates:
  uses: init4tech/actions/.github/workflows/release-crates.yml@main
  secrets:
    CARGO_REGISTRY_TOKEN: ${{ secrets.CARGO_REGISTRY_TOKEN }}
```

## Optional Parameters

### `package`

**Description:** Specific package to publish (for workspaces). When empty, publishes the root crate.

**Type**: `string`

**Default Value:** `''`

### `dry-run`

**Description:** Runs `cargo publish --dry-run` instead of actually publishing to crates.io

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

### `requires-private-deps`

**Description:** Will require the use of private dependencies in the repository, meaning an ssh key needs to be added to ssh-agent

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

### `require-lockfile`

**Description:** Will require a `Cargo.lock` file to be present and pass `--locked` to cargo

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`, `true`

## Optional Secrets

### `CARGO_REGISTRY_TOKEN`

**Description:** The crates.io API token used to publish the crate. Required unless `dry-run` is set to `true`.

### `SSH_PRIVATE_KEY`

**Description:** The SSH private key to be used for private dependencies, required if `requires-private-deps` is set to `true`

### `SSH_PRIVATE_KEY_2`

**Description:** Additional SSH private key for private dependencies

### `SSH_PRIVATE_KEY_3`

**Description:** Additional SSH private key for private dependencies
