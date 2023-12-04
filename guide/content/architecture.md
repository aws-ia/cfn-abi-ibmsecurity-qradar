---
weight: 5
title: Architecture
description: ABI Solution architecture
---

Deploying this AWS Built-in package builds the following architecture:

![Architecture diagram](/images/architecture.png)

* In all existing and future AWS accounts in your AWS organization:

    * If you choose CloudTrail when deploying the QRadar AWS Built-in template, all actions defined in the [AWS CloudTrail SRA module](https://github.com/aws-samples/aws-security-reference-architecture-examples/tree/main/aws_sra_examples/solutions/cloudtrail/cloudtrail_org) are performed.
    * If you choose GuardDuty when deploying the QRadar AWS Built-in template, all actions defined in the [Amazon GuardDuty SRA module](https://github.com/aws-samples/aws-security-reference-architecture-examples/tree/main/aws_sra_examples/solutions/guardduty/guardduty_org) are performed.

* In the log archive account, if using CloudTrail, the following resources are created:

    * An Amazon Simple Queue Service (Amazon SQS) queue to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's CloudTrail data.
    * `ObjectCreated` notifications on the S3 bucket monitoring the path to the CloudTrail data for all accounts and regions and targeting the Amazon SQS queue.

* If using GuardDuty, the following resources are created:

    * An Amazon SQS queue to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's GuardDuty data.
    * `ObjectCreated` notifications on the S3 bucket monitoring the path to the GuardDuty data for all accounts and regions and targeting the Amazon SQS queue.

**IAM role**

The following role is created in the logging account to provide access to the Amazon SQS queues created to track new data and access the required data from S3 and any required AWS Key Management Service (AWS KMS) keys. The trust policy on this role contains the `PrincipalARN` key provided during the CloudFormation template execution.

Policy

    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "sqs:DeleteMessage",
                "s3:GetObject",
                "kms:Decrypt",
                "sqs:ReceiveMessage",
                "sqs:GetQueueAttributes"
            ],
            "Resource": [
                "arn:aws:kms:us-east-1:<Logging Account>:key/*",
                "arn:aws:kms:us-east-1:<Audit Acount>:key/*",
                "arn:aws:sqs:us-east-1:<Logging Account>:qradar-cloudtrail-queue",
                "arn:aws:sqs:us-east-1:<Logging Account>:qradar-guardduty-queue",
                "arn:aws:s3:::sra-org-trail-logs-<Logging Account>-us-east-1/*",
                "arn:aws:s3:::sra-guardduty-org-delivery-<Logging Account>-us-east-1/*"
            ],
            "Effect": "Allow",
            "Sid": "VisualEditor0"
        }
    ]
    }

Trust relationship

    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "<Principal provided during stack setup>"
            },
            "Action": "sts:AssumeRole"
        }
    ]
    }


**Next**: [Deployment options](/deployment-options/index.html)