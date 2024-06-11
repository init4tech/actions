# github-release-binaries.yml

## Base Usage

```yml
release-binaries:
  uses: init4tech/actions/.github/workflows/auto-release.yml@main
  with:
    network: 'holesky'
    chain-id: '17000'
    environment: 'production'
    forge-deployment-contract: 'ForgeDeployment'
    forge-deployment-signature: 'deploy'
    forge-deployment-script-file: 'deploy.js'
    etherscan-url: 'https://holesky.etherscan.io'
  secrets:
    aws-role: ${{ secrets.AWS_ROLE }}
    kms-key-id: ${{ secrets.KMS_KEY_ID }}
    rpc-url: ${{ secrets.RPC_URL }}
    etherscan-api-key: ${{ secrets.ETHERSCAN_API_KEY }}
```

## Required Parameters

### `network`

**Description:** The evm network to deploy to

**Type**: `choice`

**Choices**:
- `holesky`

### `chain-id`

**Description:** Chain ID for the network

**Type**: `choice`

**Choices**:
- `17000`

### `etherscan-url`

**Description:** The base URL for etherscan for the network

**Type**: `choice`

**Choices**:
- `https://holesky.etherscan.io`


### `environment`

**Description:** Github Environment to deploy from; contains required secrets

**Type**: `string`

### `forge-deployment-contract`

**Description:** Name of the contract containing the deploy script

**Type**: `string`

### `forge-deployment-signature`

**Description:** Signature of the deploy script function to call

**Type**: `string`

### `forge-deployment-script-file`

**Description:** Name of the file containing the deploy script

**Type**: `string`

## Required Secrets

### `aws-role`

**Description:** AWS Role to assume

**Type**: `string`

### `kms-key-id`

**Description:** KMS key ID for AWS

**Type**: `string`

### `rpc-url`

**Description:** RPC URL for the network

**Type**: `string`

### `etherscan-api-key`

**Description:** Etherscan API key; used for verifying the contract

**Type**: `string`