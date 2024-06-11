# github-release-binaries.yml

## Base Usage

```yml
create-release:
  uses: init4tech/actions/.github/workflows/auto-release.yml@main
  with:
    generate-tag: true
```

## Required Parameters

### `generate-tag`

**Description:** If set to `true` then the action will automatically find the next patch release and create a new tag + release for it

**Type**: `boolean`

## Optional Parameters

### `custom-tag`

**Description:** If `generate-tag` is set to `false` then the specified tag will be used to create the release

**Type**: `string`

## Outputs

### `GENERATED_TAG`

**Description:** The tag that was generated for the release
