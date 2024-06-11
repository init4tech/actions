# github-release-binaries.yml

## Base Usage

```yml
create-release:
  uses: init4tech/actions/.github/workflows/auto-release.yml@main
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

<<<<<<< HEAD
**Description:** The tag that was generated for the release
=======
**Description:** The tag that was generated for the release
>>>>>>> d40a6fd (feat(auto-release): updates to create output of the tag created by auto-release, plus docs)
