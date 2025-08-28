# solidity-base.yml

## Base Usage

```yml
solidity-base:
  uses: init4tech/actions/.github/workflows/solidity-base.yml@main
```

## Optional Parameters

### `disable-gas-snapshot`

**Description:** Disables the step to check if a diff is present in the current committed `.gas-snapshot` file and a freshly generated snapshot. Flag is primarily used for bootstrapped a repository, if used for extended periods of time security may remove.

**Type**: `boolean`

**Default Value:** `false`

### `gas-diff-tolerance`

**Description:** Sets the tolerance level for the gas snapshot diff step in terms of a percentage. For example passing 1 into this step means that the diff can have up to 1% numerical difference without failing the CI step.

**Type**: `number`

**Default Value:** `1`

### `foundry-profile`

**Description:** Sets the FOUNDRY_PROFILE env variable for all forge steps (build, format, test) except for generating the gas report, which always uses FOUNDRY_PROFILE=snapshot.

**Type**: `string`

**Default Value:** `ci`