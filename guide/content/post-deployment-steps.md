---
weight: 9
title: Postdeployment options
description: Postdeployment options
---

Configure IBM Security QRadar to ingest CloudTrail and GuardDuty data.

**Note**: Configure other options, including Proxy Server, EPS Throttle, or other advanced options, as required for your environment.

## AWS CloudTrail

Set up a new ingestion data source with the following parameters:

**On the Overview tab:**
| Parameter |Value  |
|--|--|
|Name|*\<User selected>* |
|Data source type|AWS CloudTrail|
|Connector type|Amazon AWS S3 REST API|
|Data source identifier|*\<User selected>*|
|Data Collector|*\<Choose the desired attached Data Collector>*

**On the Connector tab:**
|Parameter|Value|
|--|--|
|Authentication Method|EC2 Instance IAM Role
|Assume an IAM Role (Optional)|Enabled|
|Assume Role ARN|Cloudformation Output **{QRadarIAMRoleArn}**|
|Assume Role Session Name|QRadarAWSSession *\<Can be changed to another unique identifier for STS logging in CloudTrail>*
|SQS Queue URL|Cloudformation Output **{QRadarCloudTrailSQSQueueUrl}**
|Region Name|Cloudformation Output **{QRadarRegion}**|
|S3 Collection Method|SQS Event Notifications|
|Event Format|AWS CloudTrail JSON|

## Amazon GuardDuty

**On the Overview tab:**
| Parameter |Value  |
|--|--|
|Name|*\<User selected>* |
|Data source type|Amazon GuardDuty
|Connector type|Amazon AWS S3 REST API|
|Data source identifier|*\<User selected>*|
|Data Collector|*\<Choose the desired attached Data Collector>*

**On the Connector tab:**
|Parameter|Value|
|--|--|
|Authentication Method|EC2 Instance IAM Role
|Assume an IAM Role (Optional)|Enabled|
|Assume Role ARN|Cloudformation Output **{QRadarIAMRoleArn}**|
|Assume Role Session Name|QRadarAWSSession *\<Can be changed to another unique identifier for STS logging in CloudTrail>*
|SQS Queue URL|Cloudformation Output **{QRadarGuardDutyFindingsSQSQueueUrl}**
|Region Name|Cloudformation Output **{QRadarRegion}**|
|S3 Collection Method|SQS Event Notifications|
|Event Format|LINEBYLINE

**Next**: [Test the deployment](/test-deployment/index.html)