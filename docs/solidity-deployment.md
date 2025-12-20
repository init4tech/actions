# solidity-deployment.yml

## Base Usage

```yml
deploy:
  uses: init4tech/actions/.github/workflows/solidity-deployment.yml@main
  with:
    network: 'holesky'
    chain-id: '17000'
    deployer-address: ${{ secrets.DEPLOYER_ADDRESS }}
    etherscan-url: 'https://holesky.etherscan.io'
    environment: 'production'
    forge-deployment-contract: 'DeployContract'
    forge-deployment-signature: 'deploy()'
    forge-deployment-script-file: 'DeployContract.s.sol'
  secrets:
    aws-deployer-role: ${{ secrets.AWS_DEPLOYER_ROLE }}
    kms-key-id: ${{ secrets.KMS_KEY_ID }}
    rpc-url: ${{ secrets.RPC_URL }}
    etherscan-api-key: ${{ secrets.ETHERSCAN_API_KEY }}
```

## Required Parameters

### `network`

**Description:** The EVM network to deploy to

**Type**: `string`

**Default Value:** `holesky`

### `chain-id`

**Description:** Chain ID of the network

**Type**: `string`

**Default Value:** `17000`

### `deployer-address`

**Description:** Address of the deployer account

**Type**: `string`

### `etherscan-url`

**Description:** The base URL for etherscan for the network

**Type**: `string`

**Default Value:** `https://holesky.etherscan.io`

### `environment`

**Description:** GitHub Environment to deploy from; contains required secrets

**Type**: `string`

### `forge-deployment-contract`

**Description:** Name of the contract containing the deploy script

**Type**: `string`

### `forge-deployment-signature`

**Description:** Signature of the deploy script function to call

**Type**: `string`

**Default Value:** `deploy()`

### `forge-deployment-script-file`

**Description:** Name of the deployment script file

**Type**: `string`

## Optional Parameters

### `forge-deployment-params`

**Description:** Parameters for the deployment script

**Type**: `string`

## Required Secrets

### `aws-deployer-role`

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