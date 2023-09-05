---
weight: 8
title: Deployment steps
description: Deployment steps
---

## Launch the CloudFormation Template in the Management Account

1. Download the cloudformation template from source: https://abi-qradar-demo-rpjc5noqyz36.s3.amazonaws.com/abi-enable-qradar-integration.yaml (DRAFT)

2. Launch CloudFormation template in your AWS Control Tower home region.

* Stack name: `ibmsecurity-qradar-abi-integrations`

* List Parameters with [call out default values and update below example as needed]

* **PrincipalArn**: `arn:aws:iam::123456789012:root` (No default)
ARN of the principal that can assume the role

* **pEnableCloudTrial**: `true` (Default: false)
Enable CloudTrail at the Organization level

* **pEnableGuardDuty**: `true` (Default: false)
Enable GuardDuty at the Organization level

* **pSRAS3BucketRegion**: `us-east-1` (Default : should not require changing)

* **pSRASourceS3BucketName**: `aws-abi-pilot` (Default : should not require changing)

* **pSRAStagingS3KeyPrefix**: `cfn-abi-ibmsecurity-qradar` (Default : should not require changing)
  

3. Choose both the **Capabilities** and select **Submit** to launch the stack.

  

[] I acknowledge that AWS CloudFormation might create IAM resources with custom names.

  

[] I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND

  

Wait for the CloudFormation status to change to `CREATE_COMPLETE` state.

  

  

## Launch using Customizations for Control Tower (CfCT)

  

  

[Customizations for AWS Control Tower](https://aws.amazon.com/solutions/implementations/customizations-for-aws-control-tower/) combines AWS Control Tower and other highly-available, trusted AWS services to help customers more quickly set up a secure, multi-account AWS environment using AWS best practices. You can easily add customizations to your AWS Control Tower landing zone using an AWS CloudFormation template and service control policies (SCPs). You can deploy the custom template and policies to individual accounts and organizational units (OUs) within your organization. It also integrates with AWS Control Tower lifecycle events to ensure that resource deployments stay in sync with your landing zone. For example, when a new account is created using the AWS Control Tower account factory, Customizations for AWS Control Tower ensures that all resources attached to the account's OUs will be automatically deployed.

  

The templates provided as part of the ABI packages are deployable using Customizations for Control Tower. Please check below for additional details.

  

#### Pre-requisites

  

1. The CfCT solution, do not have ability to launch resources on the Management account. Hence, you need to create the role with required permissions in the Management account.

  

#### How it works

  

To deploy this sample partner integration page using CfCT solution, add the following blurb to the `manifest.yaml` file from your CfCT solution and update the account/ou names as needed.

  

```

resources:

- name: sra-enable-partner1-solution

resource_file: https://aws-abi-pilot.s3.us-east-1.amazonaws.com/cfn-abi-aws-reference-guide/templates/abi-enable-partner1-securityhub-integration.yaml

deploy_method: stack_set

parameters:

- parameter_key: pProductArn

parameter_value: arn:aws:securityhub:us-east-1::product/cloud-custodian/cloud-custodian

- parameter_key: pSRASourceS3BucketName

parameter_value: aws-abi-pilot

- parameter_key: pSRAStagingS3KeyPrefix

parameter_value: cfn-abi-aws-reference-guide

deployment_targets:

accounts:

- [[MANAGEMENT-AWS-ACCOUNT-ID]]

```

  

  

**Next:** Choose [Postdeployment Options](/post-deployment-steps/index.html) to get started.
