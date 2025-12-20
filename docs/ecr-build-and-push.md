# ecr-build-and-push.yml

## Base Usage

```yml
docker-ecr-push:
  uses: init4tech/actions/.github/workflows/ecr-build-and-push.yml@main
  with:
    rust-binary-name: 'my-binary'
    environment: 'dev'
  secrets:
    aws-ecr-repository: ${{ secrets.AWS_ECR_REPOSITORY }}
    aws-ecr-deployer-role-arn: ${{ secrets.AWS_ECR_DEPLOYER_ROLE_ARN }}
```

## Required Parameters

### `rust-binary-name`

**Description:** Name of the Rust binary to build

**Type**: `string`

### `environment`

**Description:** Environment to deploy to (used for GitHub environment secrets)

**Type**: `string`

## Optional Parameters

### `requires-private-deps`

**Description:** Requires private dependencies to be fetched, sets up ssh-agent

**Type**: `boolean`

**Default Value:** `false`

### `dockerfile-path`

**Description:** Path to the Dockerfile to use

**Type**: `string`

**Default Value:** `Dockerfile`

## Required Secrets

### `aws-ecr-repository`

**Description:** ECR repository to push to

**Type**: `string`

### `aws-ecr-deployer-role-arn`

**Description:** Role ARN to assume for ECR access

**Type**: `string`

## Optional Secrets

### `SSH_PRIVATE_KEY`

**Description:** SSH private key for fetching private dependencies (required if `requires-private-deps` is `true`)

**Type**: `string`

### `SSH_PRIVATE_KEY_2`

**Description:** Additional SSH private key for fetching private dependencies

**Type**: `string`

### `SSH_PRIVATE_KEY_3`

**Description:** Additional SSH private key for fetching private dependencies

**Type**: `string`

