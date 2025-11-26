# s3-upload.yml

## Base Usage

```yml
upload-to-s3:
  uses: init4tech/actions/.github/workflows/s3-upload.yml@main
  with:
    s3_bucket_name: 'my-bucket'
    deployer_role_arn: 'arn:aws:iam::123456789012:role/deployer-role'
    aws_region: 'us-east-1'
    source_path: '.'
    delete: true
```

## Required Parameters

### `s3_bucket_name`

**Description:** The name of the S3 bucket to upload files to

**Type**: `string`

### `deployer_role_arn`

**Description:** The IAM role ARN to assume for S3 deployment. This role must have permissions to upload objects to the specified S3 bucket.

**Type**: `string`

## Optional Parameters

### `aws_region`

**Description:** The AWS region where the S3 bucket is located

**Type**: `string`

**Default Value**: `us-east-1`

### `source_path`

**Description:** The source path to upload. This can be a directory or file path relative to the repository root. Defaults to the repository root.

**Type**: `string`

**Default Value**: `.`

### `delete`

**Description:** If set to `true`, files in the S3 bucket that are not present in the source will be deleted. This enables synchronization behavior.

**Type**: `boolean`

**Default Value**: `true`

