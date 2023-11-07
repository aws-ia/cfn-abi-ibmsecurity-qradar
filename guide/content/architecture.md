

## Deploying this ABI package builds the following architecture:

![Architecture diagram](/images/architecture.png)

**In all existing and future AWS accounts in your AWS organization:**


* If CloudTrail setup is chosen when deploying the QRadar ABI template, all actions defined in the  [AWS CloudTrail SRA module](https://github.com/aws-samples/aws-security-reference-architecture-examples/tree/main/aws_sra_examples/solutions/cloudtrail/cloudtrail_org) will be performed

* If GuardDuty setup is chosen when deploying the QRadar ABI template, all actions defined in the [Amazon GuardDuty SRA module](https://github.com/aws-samples/aws-security-reference-architecture-examples/tree/main/aws_sra_examples/solutions/guardduty/guardduty_org) will be performed

  
**In the log archive account:**

*If CloudTrail setup is chosen, the following resources are created:

* An SQS Queue will be created to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's CloudTrail data

* `ObjectCreated` notifications on the S3 bucket monitoring the path to the CloudTrail data for all accounts and regions and targeting the above SQS queue

*If GuardDuty setup is chosen, the following resources are created:

* An SQS Queue will be created to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's GuardDuty data

* `ObjectCreated` notifications on the S3 bucket monitoring the path to the GuardDuty data for all accounts and regions and targeting the above SQS queue


**IAM Role**

The following role will be created in the Logging Account to provide access to the SQS Queues created to track new data and to access the required data from S3 and any required KMS keys. The trust policy on this role will contain the "PrincipalARN" provided during the CloudFormation template execution.

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

Trust Relationship

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

  

  

**Next:** Choose [Deployment Options](/deployment-options/index.html) to get started.