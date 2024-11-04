# auto-release-rust.yml

## Base Usage

```yml
create-release:
  uses: init4tech/actions/.github/workflows/auto-release-rust.yml@main
  with:
    binary-name: "my-binary"
```

## Required Parameters

### `binary-name`

**Description:** The name of the binary (from `Cargo.toml`) that should be used for picking the version of the release

**Type**: `string`
