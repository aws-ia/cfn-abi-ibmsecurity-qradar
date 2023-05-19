

# IBM QRadar Amazon Built-in Quickstart

## **Prerequisites:**

For the ABI Pilot program, primary Prerequisite is that you have deployed an AWS Control which ensures you have a multi-account Landing Zone already configured.

This is critical to ensure that services such as CloudTrail and Guard Duty are deployed organization-wide, and that all logs are centralized in the Logging Account for consumption.

## **AWS Core Services that will be enabled:**

· **CloudTrail** organization trail for all regions in all accounts configured for Management Events

![](https://github.com/aws-ia/cfn-abi-aws-cloudtrail/raw/main/images/sra-cloudtrail-org.png)

· **Amazon Guard Duty** threat detection services for all regions in all accounts

![](https://github.com/aws-ia/cfn-abi-amazon-guardduty/blob/main/images/SRA-GuardDuty.jpg?raw=true)

Please refer to the AWS Built-in Documentation at [ TODO: ABI DOCS ] for more details about enabling CloudTrail organization trail Management events and Guard Duty.


## **Additional AWS resources that will be created for QRadar to collect data all in the Control Tower Logging Account**

**Event Driven Notifications for new CloudTrail Findings in S3**
 - Object Created Notifications on CloudTrail org S3 bucket
 - SQS Queue to receive the Object Created notifications
 - KMS Key to encrypt Guard Duty notifications SQS queue

**Event Driven Notifications for new Guard Duty Findings in S3**

 - Object Created Notifications on Guard Duty S3 bucket
 - SQS Queue to receive the Object Created notifications
 - KMS Key to encrypt Guard Duty notifications SQS queue

## IAM Role to allow polling of SQS queue and reading of related S3 objects

A role with the ARN  **arn:aws:iam::{Logging Account #}:role/QRadarRole**  will be created to allow least privileged access to the required resources. It will have a trust policy containing the only  **PrincipalARN** you provide when deploying the QRadar Built-in CloudFormation Stack.

**Example Inline Policy in IAM Role**

In this example the Logging account is 111111111111 and the Audit account is 222222222222

    {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "kms:Decrypt",
                "s3:GetObject",
                "sqs:DeleteMessage",
                "sqs:ReceiveMessage",
                "sqs:GetQueueAttributes"
            ],
            "Resource": [
                "arn:aws:kms:us-east-1:111111111111:key/*",
                "arn:aws:kms:us-east-1:222222222222:key/*",
                "arn:aws:sqs:us-east-1:111111111111:qradar-cloudtrail-queue",
                "arn:aws:sqs:us-east-1:111111111111:qradar-guardduty-queue",
                "arn:aws:s3:::sra-org-trail-logs-111111111111-us-east-1/*",
                "arn:aws:s3:::sra-guardduty-org-delivery-111111111111-us-east-1/*"
            ]
        }
    ]
    }

You will notice all resources above belong to the logging account except for the KMS key used to encrypt the S3 buckets created during CloudTrail and Guard Duty setup is from the Audit account.

## **AWS Credentials**
No credentials will be created as part of the QRadar ABI deployment. It is recommended to use Instance Credentials when connecting from other AWS resources and provide the PrincipalARN required when deploying to secure the trust policy on the role to only that principal.

If you are not connecting from withing AWS or require credentials for some other reason, please create the credentials as needed and provide the ARN of the IAM user associated as the Principal when deploying the QRadar ABI stack.

## **Deploying the QRadar ABI Stack:**

{ ABI Stack Placeholder }

The ABI stack must be deployed from the Management Account of the Landing Zone.

[https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create?stackName=QRadarSIEMABI&templateURL=https://placeholderbucket.s3.us-east-1.amazonaws.com/qradar/templates/abi-qradar.template.yaml](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create?stackName=QRadarSIEMABI&templateURL=https://placeholderbucket.s3.us-east-1.amazonaws.com/qradar/templates/abi-qradar.template.yaml)

**Required Inputs:**

**PrincipalArn** - ARN of the principal that can assume the role

**Stack Outputs:**

**QRadarCloudTrailSQSQueueUrl**  - SQS URL for the CloudTrail events

**QRadarGuardDutyFindingsSQSQueueUrl**  - SQS URL for the GuardDuty findings

**QRadarIAMRoleArn**  – The ARN of the QRadar IAM role

**QRadarRegion**  - AWS Region where the SQS queues and bucket resides

These outputs will be used to setup 2 log source in QRadar, one to collect all CloudTrail data and another to collect all Guard Duty findings.

**Configuring QRadar to collect data:**

To Follow
