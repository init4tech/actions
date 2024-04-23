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
