---
weight: 99
title: Cleanup instructions
description: Instructions to clean up the resources created by the AWS Built-in package
---

# Cleanup instructions

After trying this AWS Built-in solution, you may want to redeploy or remove it completely. In either case, this solution leaves certain resources as-is when you delete the stacks that are deployed. This behavior is working as designed to avoid deleting the history of data collections in your accounts.

You can clean up resources created this AWS Built-in solution to avoid incurring charges for resources created and avoid conflicts while redeploying the stack.

This section provides instructions to clean up the resources created by the AWS Built-in package.

## Delete the CloudFormation stack

1. Navigate to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation#/stacks/).
2. Choose the stack created by the AWS Built-in solution and delete it.
3. Wait for the **DELETE_COMPLETE** status to confirm the stack deletion.

## Delete resources created by the AWS Built-in solution

In the management account:

1. Delete the following Amazon S3 buckets. See [Deleting a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) for more information.

- cfn-abi-amazon-guardduty-`<account-id>`-`<region>`
- cfn-abi-aws-cloudtrail-`<account-id>`-`<region>`
- sra-gd-staging-`<account-id>`-`<region>`
- sra-cloudtrail-staging-`<account-id>`-`<region>`

2. Delete the following AWS Systems Manager (SSM) parameters. See [Deleting a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) for more information.

- All parameters with prefix `/sra/gd/`
- All parameters with prefix `/sra/ctrail/`

3. Delete all CloudWatch log groups that start with `/sra/sra-org-trail` prefixes. See [Deleting the AWS CloudWatch logs](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) for more information.

In the log archive account:

1. Delete the following Amazon S3 buckets. See [Deleting a bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) for more information.

- sra-guardduty-org-delivery-<account-id>-<region>
- sra-org-trail-logs-<account-id>-<region>

2. Delete the CloudWatch log groups that start with the following prefixes. See [Deleting the AWS CloudWatch logs](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) for more information.

- `/aws/lambda/sra-ct-s3`
- `/aws/lambda/sra-gd-s3`