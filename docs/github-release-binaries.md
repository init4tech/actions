# github-release-binaries.yml

## Base Usage

```yml
release-binaries:
  uses: init4tech/actions/.github/workflows/github-release-binaries.yml@main
```

## Required Parameters

### `binary-name`

**Description:** The name of the binary from the `target/release` folder to be uploaded to the github release.

**Type**: `string`
