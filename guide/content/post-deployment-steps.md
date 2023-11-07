
---

weight: 9

title: PostDeployment Options

description: Post deployment options

---

  

# Configure QRadar Log Insights to ingest the CloudTrail and GuardDuty Data

  

## AWS CloudTrail

Setup a new Ingestion Data Source with the following parameters:

**On the Overview Tab:**
| Parameter |Value  |
|--|--|
|Name|*\<User selected>* |
|Data source type|AWS CloudTrail|
|Connector type|Amazon AWS S3 REST API|
|Data source identifier|*\<User selected>*|
|Data Collector|*\<Choose the desired attached Data Collector>*

**On the Connector Tab:**
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

Any options such as Proxy Server, EPS Throttle, or other Advanced options may be configured as required for your environment.


  

## Amazon GuardDuty

**On the Overview Tab:**
| Parameter |Value  |
|--|--|
|Name|*\<User selected>* |
|Data source type|Amazon GuardDuty
|Connector type|Amazon AWS S3 REST API|
|Data source identifier|*\<User selected>*|
|Data Collector|*\<Choose the desired attached Data Collector>*

**On the Connector Tab:**
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

Any options such as Proxy Server, EPS Throttle, or other Advanced options may be configured as required for your environment.


**Next:** Choose [Test the Deployment](/test-deployment/index.html) to get started.