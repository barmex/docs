---
sourcePath: en/ydb/ydb-docs-core/en/core/maintenance/_includes/backup_and_recovery/06_s3_3_access_keys.md
---
### Creating access keys {#s3_create_access_keys}

Access keys are used for authentication and authorization in S3-compatible storage. The [YDB console client](../../../reference/ydb-cli/index.md) provides three ways to pass keys:

* Through the `--access-key` and `--secret-key` command line options.
* Using the `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` environment variables.
* Through the `~/.aws/credentials` file created and used by the [AWS CLI](https://aws.amazon.com/cli/).

The settings apply in the order described above. For example, if you use all three ways to pass the access_key or secret_key value at the same time, the values passed through the command-line options will be used.
