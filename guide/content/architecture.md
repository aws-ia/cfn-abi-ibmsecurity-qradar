

## Deploying this ABI package builds the following architecture:

  

**In all current and AWS accounts in your AWS organization:**


* If CloudTrail setup is chosen when deploying the QRadar ABI template, all actions defined in https://github.com/aws-ia/cfn-abi-aws-cloudtrail/tree/main will be performed

* If Guard Duty setup is chosen when deploying the QRadar ABI template, all actions defined in https://github.com/aws-ia/cfn-abi-amazon-guardduty/tree/main will be performed

  
**In the log archive account:**

*If CloudTrail setup is chosen:*

* An SQS Queue will be created to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's CloudTrail data

* `ObjectCreated` notifications on the S3 bucket monitoring the path to the CloudTrail data for all accounts and regions and targeting the above SQS queue

*If Guard Duty setup is chosen:*

* An SQS Queue will be created to receive `ObjectCreated` notifications from the S3 bucket in the logging account containing the organization's Guard Duty data

* `ObjectCreated` notifications on the S3 bucket monitoring the path to the Guard Duty data for all accounts and regions and targeting the above SQS queue


**IAM Role**

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