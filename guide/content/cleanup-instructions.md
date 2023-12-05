---
weight: 99
title: Cleanup instructions
description: Instructions to clean up the resources created by the AWS Built-in package
---

After trying this AWS Built-in solution, you may want to redeploy or remove it completely. In either case, this solution leaves certain resources as-is when you delete the stacks that are deployed. This behavior is working as designed to avoid deleting the history of data collections in your accounts.

You can clean up resources created this AWS Built-in solution to avoid incurring charges for resources created and avoid conflicts while redeploying the stack.

This section provides instructions to clean up the resources created by the AWS Built-in package.

## Delete the CloudFormation stack

1. Navigate to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation#/stacks/).
2. Choose the stack created by the AWS Built-in solution and delete it.
3. Wait for the **DELETE_COMPLETE** status to confirm the stack deletion.

## Delete resources created by the AWS Built-in solution

#### In the management account:

1. [Delete the following Amazon S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html).

- sra-gd-staging-`<account-id>`-`<region>`
- sra-cloudtrail-staging-`<account-id>`-`<region>`
- sra-helper-`<account-id>`-`<region>`
- sra-staging-`<account-id>`-`<regions>` # Repeat for all regions where the solution is deployed.

2. [Delete Systems Manager parameters](https://docs.aws.amazon.com/systems-manager/latest/userguide/deleting-parameters.html) that start with prefix `/sra/`. Repeat for all active regions.

3. [Delete the AWS CloudWatch log groups](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) that start with the following prefixes:

- `/sra/sra-org-trail`
- `/aws/lambda/sra-codebuild-project-lambda`
- `/aws/lambda/sra-guardduty-codebuild-project-lambda`

4. [Delete a build project in AWS CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/delete-project.html) that start with the following prefixes.

- `sra-codebuild-project`

5. [Delete AWS IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_manage_delete.html) that are listed below.

- `sra-execution`

6. [Delete a stack set](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-delete.html) with name `sra-stackset-execution-role`.

7. [Delete a stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacks.html) with stack name `sra-common-prerequisites-staging-s3-bucket`.

#### In the log archive account:

1. [Delete the following Amazon S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html).

- sra-guardduty-org-delivery-`<account-id>`-`<region>`
- sra-org-trail-logs-`<account-id>`-`<region>`

2. [Delete Systems Manager parameters](https://docs.aws.amazon.com/systems-manager/latest/userguide/deleting-parameters.html) that start with prefix `/sra/`. Repeat for all active regions.

3. [Delete the AWS CloudWatch log groups](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) that start with the following prefixes:

- `/aws/lambda/sra-ct-s3`
- `/aws/lambda/sra-gd-s3`
- `/sra/gd/`

4. [Delete AWS IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_manage_delete.html) that are listed below.

- `sra-execution`

#### In the audit account:

1. [Delete AWS IAM roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_manage_delete.html) that are listed below.
- `sra-execution`