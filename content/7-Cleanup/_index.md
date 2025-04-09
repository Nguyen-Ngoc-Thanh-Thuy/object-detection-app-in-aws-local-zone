+++
title = "Clean up resources"
date = 2022
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

To terminate the resources created during the workshop, follow the steps below in the AWS console:

### Access CloudFormation
- In the AWS console search bar, type **"CloudFormation"** and select **"Stack"** → **"streamingServer"**.
- Click **"Delete**.
![Delete stack](/images/7.cleanup/000-stack.png)
![Delete stack](/images/7.cleanup/001-stack.png)


### Delete resources in AWS Local Zones
- Before opting out of the AWS Local Zone, it is essential to delete all the resources utilized there:
    + VPN instance: ```localZone-vpn-instance```
    + Object Detector instance: ```detectorServer```
    + Security Groups: ```my-detectorServer-sg```, ```my-detectorServer-sg```
    + Internet Gateway (IGW): ```igw-aws-local-zone```
    + Public subnet: ```my-subnet-in-aws-local-zone```
    + VPC extended to the AWS Local Zone: ```vpc-extended-tp-aws-local-zone```
    + Role: ```detectionServer-vpn-ssm-ec2-instance-profile```


- In the AWS console search bar, type **EC2** and select the **EC2 service**.
- Locate and select both the **localZone-vpn-instance** and **detectorServer instances**.
- Click **Terminate instance**.
![Delete instances](/images/7.cleanup/002-instance.png)
![Delete instances](/images/7.cleanup/003-instance.png)


- In the AWS console search bar, type **VPC** and select the **VPC service**.
- Select the VPC: ```vpc-extended-tp-aws-local-zone``` and **"Delete VPC"**.
![Delete vpc](/images/7.cleanup/004-vpc.png)
![Delete vpc](/images/7.cleanup/005-vpc.png)

- In the AWS console search bar, type **IAM** and select the **IAM service**.
- On the left panel, select **"Roles"**. Search for the role ```detectionServer-vpn-ssm-ec2-instance-profile``` and delete.
![Delete IAM role](/images/7.cleanup/006-iam.png)
![Delete IAM role](/images/7.cleanup/007-iam.png)


