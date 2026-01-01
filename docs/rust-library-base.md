# rust-library-base.yml

## Base Usage

```yml
rust-library-base:
  uses: init4tech/actions/.github/workflows/rust-library-base.yml@main
```

## Description

This workflow extends `rust-base.yml` with additional feature checks. It runs all the checks from `rust-base.yml` (tests, doctests, rustfmt, clippy, docs) plus additional clippy checks for all feature combinations.

## Optional Parameters

### `rust-channel`

**Description:** Sets the rust-toolchain channel if no toolchain file present

**Type**: `string`

**Default Value:** `stable`

**Allowed values:** `stable`, `beta`, `nightly`

### `install-foundry`

**Description:** Will install `foundry` as a pre-test step to all use of the binary during the test phase

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`,`true`

### `require-lockfile`

**Description:** Will require a `Cargo.lock` file to be present in the repository

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`,`true`

### `os`

**Description:** Sets the OS for the runner

**Type**: `string`

**Default Value:** `ubuntu-latest`

### `requires-private-deps`

**Description:** Will require the use of private dependencies in the repository, meaning an ssh key needs to be added to ssh-agent

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`,`true`

### `rust-profile`

**Description:** The profile to give to cargo for running

**Type**: `string`

**Default Value:** `dev`

## Optional Secrets

### `SSH_PRIVATE_KEY`

**Description:** The SSH private key to be used for private dependencies, required if `requires-private-deps` is set to `true`

**Type**: `string`

### `SSH_PRIVATE_KEY_2`

**Description:** Additional SSH private key for fetching private dependencies

**Type**: `string`

### `SSH_PRIVATE_KEY_3`

**Description:** Additional SSH private key for fetching private dependencies

**Type**: `string`

## Jobs

This workflow runs two jobs:

1. **rust-base-checks**: Runs all checks from `rust-base.yml` (tests, doctests, rustfmt, clippy, docs)
2. **feature-checks**: Runs clippy with `--all-features` and `--no-default-features` to ensure code compiles with different feature combinations

