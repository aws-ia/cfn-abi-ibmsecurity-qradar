
---

weight: 4

title: Cost and licenses

description: Cost of the solution and licenses required.

---
<partner cost>

## IBM Security QRadar Log Insights SaaS

See Pricing @ [IBM Security QRadar Log Insights SaaS (US)](https://aws.amazon.com/marketplace/pp/prodview-p2llj6q6wlsq4)

  

<AWS Service cost>

## If AWS CloudTrail setup is chosen when deploying the QRadar ABI template:

- [AWS CloudTrail usage](https://aws.amazon.com/cloudtrail/pricing/) in all regions and accounts

- [S3 storage](https://aws.amazon.com/s3/pricing/) for CloudTrail data

- [S3 data transfer](https://aws.amazon.com/s3/pricing/) from the ABI S3 bucket region to configured QRadar destination AWS Region

- [SQS usage](https://aws.amazon.com/sqs/pricing/) for tracking and ingesting CloudTrail data into QRadar
 
 

## If Amazon GuardDuty setup is chosen when deploying the QRadar ABI template:

- [Amazon GuardDuty usage](https://docs.aws.amazon.com/guardduty/latest/ug/monitoring_costs.html) in all regions and accounts

- [S3 storage](https://aws.amazon.com/s3/pricing/) for GuardDuty data

- [S3 data transfer](https://aws.amazon.com/s3/pricing/) from the ABI S3 bucket region to configured QRadar destination AWS Region

- [SQS usage](https://aws.amazon.com/sqs/pricing/)  for tracking and ingesting GuardDuty data into QRadar
  

**Next:** Choose [Architecture](/architecture/index.html) to get started.