# hugo-build-deploy.yml

## Base Usage

```yml
rust-base:
  uses: init4tech/actions/.github/workflows/hugo-build-deploy.yml@main
  with:
    hugo-src-dir: 'src'
    hugo-theme: 'hugo-theme'
    environment: 'production'
    aws-iam-deployer-role: 'arn:aws:iam::123456789012:role/deployer-role'
    aws-s3-bucket: 'my-bucket'
    aws-region: 'us-east-1'
```

## Required Parameters

### `hugo-src-dir`

**Description:** Sets the path to the hugo source files

**Type**: `string`

### `hugo-theme`

**Description:** The name of the theme to use for the hugo build

**Type**: `string`

### `environment`

**Description:** The github environment to use for deployment

**Type**: `string`

### `aws-iam-deployer-role`

**Description:** The IAM role to use for deployment

**Type**: `string`

### `aws-s3-bucket`

**Description:** The S3 bucket to use for deployment

**Type**: `string`

### `aws-region`

**Description:** The AWS region to use for deployment

**Type**: `string`

**Default Value**: `us-east-1`
