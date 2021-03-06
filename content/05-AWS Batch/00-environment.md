+++
title = "a. Lab Environment"
date = 2019-09-18T10:46:30-04:00
weight = 20
tags = ["tutorial", "install", "AWS", "Batch"]
+++

In this step, we will create an IAM role with Administrator access and configure Cloud9 to use the IAM role for the rest of this lab.

1. Follow [this deep link to create an IAM role with Administrator access](https://console.aws.amazon.com/iam/home#/roles$new?step=review&commonUseCase=EC2%2BEC2&selectedUseCase=EC2&policies=arn:aws:iam::aws:policy%2FAdministratorAccess).

2. Confirm that **AWS service** and **EC2** are selected, then click **Next: Permissions** to view permissions.

3. Confirm that **AdministratorAccess** is checked, then click **Next: Tags** to assign tags.

4. Take the defaults, and click **Next: Review** to review.

5. Enter **hpcworkshop-admin** for the Name, and click **Create role**. 
![AWS Batch](/images/aws-batch/iam-role-1.png)

6. Follow [this deep link to find your Cloud9 EC2 instance](https://console.aws.amazon.com/ec2/v2/home?#Instances:search=cloud9;sort=desc:launchTime).

7. Select the instance, then choose **Actions / Instance Settings / Attach/Replace IAM Role**. 
![AWS Batch](/images/aws-batch/iam-role-2.png)

8. Choose **hpcworkshop-admin** from the IAM Role drop down, and select **Apply**.
![AWS Batch](/images/aws-batch/iam-role-3.png)

9. In Cloud9, click the gear icon (in top right corner), or click to open a new tab and choose “Open Preferences”. Select **AWS SETTINGS** to turn off **AWS managed temporary credentials**, then close the Preferences tab.
![AWS Batch](/images/aws-batch/c9disableiam.png)

10. To ensure temporary credentials aren’t already in place we will also remove any existing credentials file:

```bash
rm -vf ${HOME}/.aws/credentials
```

11. Identify the AWS region with the following commands:

```bash
export AWS_REGION=$(curl -s 169.254.169.254/latest/dynamic/instance-identity/document | jq -r '.region')
echo $AWS_REGION
```

12. Configure the AWS CLI to use this AWS region:

```bash
aws configure set default.region ${AWS_REGION}
aws configure get default.region
```
