# static-analysis-base.yml

## Base Usage

```yml
static-analysis-base:
  uses: init4tech/actions/.github/workflows/solidity-static-analysis.yml@main
```

## Optional Parameters

### `divide-before-multiply`

**Description:** Disables the detector to check if there exists instances of performing division before multiplication in a smart contract suite. Solidity's integer division truncates. Thus, performing division before multiplication can lead to precision loss.

**Type**: `boolean`

**Default Value:** `false`

### `encode-packed-collision`

**Description:** Disables the detector to check if there exists collisions due to dynamic type usages in abi.encodePacked.

**Type**: `boolean`

**Default Value:** `false`

### `arbitrary-send-erc20`

**Description:** Disables the detector to check when msg.sender is not used as from in transferFrom.

**Type**: `boolean`

**Default Value:** `false`

### `array-by-reference`

**Description:** Disables the detector to detect arrays passed to a function that expects reference to a storage array.

**Type**: `boolean`

**Default Value:** `false`

### `tautology`

**Description:** Disables the detector to detect statements that are always true or always false (or contradictions)

**Type**: `boolean`

**Default Value:** `false`

### `suicidal`

**Description:** Disables the detector to detect unprotected usages of selfdestruct.

**Type**: `boolean`

**Default Value:** `false`