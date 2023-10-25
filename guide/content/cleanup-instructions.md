
---

weight: 99

title: Cleanup Instructions

description: Instructions to cleanup the resources created by the ABI package

---

## Cleanup Instructions

  

You may have tried this ABI package and want to redeploy the package or remove it completely. In either cases, this ABI package leaves certain resources as-is when you delete the stacks deployed. This is by desgin to avoid deleting the history of data collections you may have in your accounts.

  

You may want to clean up the resources created by the ABI package to:

1. Avoid incurring any charges for the resources created

2. Avoid conflicts while redeploying the stack.

  

This section provides instructions to clean up the resources created by the ABI package.

  

#### Delete CloudFormation stack

1. Navigate to [AWS Console](https://console.aws.amazon.com/cloudformation#/stacks/)

2. Select the stack created by the ABI package and delete it

3. Wait for the stack deletion to complete. Wait for the stack status DELETE_COMPLETE.

  

#### Delete resources created by the ABI package

  

##### In the Management Account

1. [Delete all Amazon S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) listed below:

- cfn-abi-amazon-guardduty-`<account-id>`-`<region>`

- cfn-abi-aws-cloudtrail-`<account-id>`-`<region>`

- sra-gd-staging-`<account-id>`-`<region>`

- sra-cloudtrail-staging-`<account-id>`-`<region>`

2. [Delete all SSM Parameters](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) listed below:

- All parameter with prefix `/sra/gd/`

- All parameter with prefix `/sra/ctrail/`

3. [Delete all CloudWatch Log Groups](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) listed below:

- All log groups that start with prefixes:

- `/sra/sra-org-trail`

  

##### In the Log Archive Account

1. [Delete all Amazon S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/delete-bucket.html) listed below:

- sra-guardduty-org-delivery-<account-id>-<region>

- sra-org-trail-logs-<account-id>-<region>

3. [Delete all CloudWatch Log Groups](https://docs.aws.amazon.com/solutions/latest/research-service-workbench-on-aws/deleting-the-aws-cloudwatch-logs.html) listed below:

- All log groups that start with prefixes:

- `/aws/lambda/sra-ct-s3`

- `/aws/lambda/sra-gd-s3`