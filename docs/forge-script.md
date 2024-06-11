# github-release-binaries.yml

## Base Usage

```yml
create-release:
  uses: init4tech/actions/.github/workflows/auto-release.yml@main
```

## Required Parameters

### `github-environment`

**Description:** The github environment to use for the release

**Type**: `string`

### `forge-script-contract`

**Description:** The forge script contract to use for the release

**Type**: `string`

### `forge-script-signature`

**Description:** The signature of the function you want to call in the forge script contract

**Type**: `string`

## Optional Parameters

### `forge-script-params`

**Description:** A space separated list of parameters to pass to the forge script

**Type**: `string`

## Required Secrets

### `aws-role`

**Description:** The AWS role to use for the kms signer key for forge

### `kms-key-id`

**Description:** The AWS kms key id to use for the kms signer key for forge

### `rpc-url`

**Description:** The url of the rpc endpoint for forge to use
