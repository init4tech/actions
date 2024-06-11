# github-release-binaries.yml

## Base Usage

```yml
release-binaries:
  uses: init4tech/actions/.github/workflows/release-rust-bin.yml@main
```

## Required Parameters

### `binary-name`

**Description:** The name of the binary to be released

**Type**: `string`

## Optional Parameters

### `tag`

**Description:** The tag to be used for which release to upload the binary to

**Type**: `string`
