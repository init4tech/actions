# rust-base.yml

## Base Usage

```yml
rust-base:
  uses: init4tech/actions/.github/workflows/rust-base.yml@main
```

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

### `requires-private-deps`
 
**Description:** Will require the use of private dependencies in the repository, meaning an ssh key needs to be added to ssh-agent

**Type**: `boolean`

**Default Value:** `false`

**Allowed values:** `false`,`true`

## Optional Secrets

### `SSH_PRIVATE_KEY`

**Description:** The SSH private key to be used for private dependencies, required if `requires-private-deps` is set to `true`