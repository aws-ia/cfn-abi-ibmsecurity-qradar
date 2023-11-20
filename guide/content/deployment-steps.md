---
weight: 8
title: Deployment steps
description: Deployment steps
---
# Deployment steps

## Launch the CloudFormation template in the AWS Organizations management account {#launch-cfn}

1. Download the [CloudFormation template](https://github.com/aws-ia/cfn-abi-ibmsecurity-qradar/blob/main/templates/abi-enable-qradar-integration.yaml).
2. Launch the CloudFormation template in your AWS Control Tower home Region, using the following parameters:

* **Stack name**: `ibmsecurity-qradar-abi-integrations`
* **PrincipalArn**: `arn:aws:iam::123456789012:root` (Amazon Resource Name of the principal that can assume the role.
* **pEnableCloudTrial**: `true` (Enables CloudTrail at the organization level. Default is false.)
* **pEnableGuardDuty**: `true` (Enables GuardDuty at the organization level. Default is false.)
* **pSRAS3BucketRegion**: `us-east-1` (Do not change unless the `pSRASourceS3BucketName` parameter is changed to your own Amazon S3 bucket. In that case, match the region with AWS Region where the S3 bucket is created.)
* **pSRASourceS3BucketName**: `aws-abi-pilot` (Leave the default value.)
* **pSRAStagingS3KeyPrefix**: `cfn-abi-ibmsecurity-qradar` (Leave the default value.)

3. Select the following **Capabilities** and choose **Submit** to launch the stack.

[] I acknowledge that AWS CloudFormation might create IAM resources with custom names.
[] I acknowledge that AWS CloudFormation might require the following capability: CAPABILITY_AUTO_EXPAND

Wait for the CloudFormation status to change to `CREATE_COMPLETE` state.

## Launch using Customizations for Control Tower {#launch-cfct}

You can use [Customizations for AWS Control Tower](https://aws.amazon.com/solutions/implementations/customizations-for-aws-control-tower/) to deploy the templates provided with the AWS Built-in solution. 

The CfCT solution can't launch resources on the management account. Therefore, you must create the role with required permissions in the management account.

To deploy this sample partner integration page using CfCT solution, add the following content to the `manifest.yaml` file from your CfCT solution and update the account and OU names as needed.

```
resources:
  - name: launch-qradar-main-abi
    resource_file: https://aws-abi-pilot.s3.us-east-1.amazonaws.com/cfn-abi-ibmsecurity-qradar/templates/abi-enable-qradar-integration.yaml
    deploy_method: stack_set
    parameters:
      - parameter_key: pEnableCloudTrial
        parameter_value: 'false'  # Set to 'true' to enable CloudTrail integration
      - parameter_key: pEnableGuardDuty
        parameter_value: 'false'  # Set to 'true' to enable GuardDuty integration
      - parameter_key: pSRASourceS3BucketName
        parameter_value: aws-abi
      - parameter_key: pSRAS3BucketRegion
        parameter_value: us-east-1
      - parameter_key: pSRAStagingS3KeyPrefix
        parameter_value: cfn-abi-ibmsecurity-qradar
    deployment_targets:
      accounts:
        - [[MANAGEMENT-AWS-ACCOUNT-ID]]

```

**Next**: [Postdeployment options](/post-deployment-steps/index.html) 
