---
title : "Configure Security Groups and define an IAM Role"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---
**1. Create a Security Group**
+ Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
+ In the left panel, click **"Security groups"**, then select **"Create security group"**.
![Create Security Group button](/images/4.sectionb/000-createsg.png)
+ Now, configure the **security group for the Detector server**:
  - Security Group Name: Enter ```my-detectorServer-sg```.
  - Description: Add a note like ```HTTP - web server, TCP 80 and 443 - linux repos, TCP 8554 - RSTP```.
  - VPC Selection: Choose the **vpc-extended-to-aws-local-zone VPC**.
  ![Security Group Configuration](/images/4.sectionb/001-sgconfig.png)

**2. Add Rules to the Security Group**
+ Click **"Add rule"**.
+ For **Inbound traffic**: Select HTTP as the type. Set Source to **"My IP"**.
  ![Security Group inbound rule](/images/4.sectionb/002-inboundrule.png)
+ For **Outbound traffic**, add these rules:
  - **TCP on port 80 and 443** (destination: 0.0.0.0/0) → Needed for Linux package updates.
  - **TCP on port 8554** (destination: 0.0.0.0/0) → Needed for RTSP streaming.
  ![Security Group outbound rule](/images/4.sectionb/003-outboundrule.png)

{{% notice warning%}}
Port 8554 is required for RTSP, but later we will update the security group to restrict outbound traffic only to the streaming instance.
{{% /notice %}}

**3. Create an IAM Role**
+ Open the **AWS Console**, type **"IAM"**, and select the **IAM service**.
+ In the left panel, click **"Roles"**, then click **"Create role"**.
![Create IAM Role](/images/4.sectionb/004-createrole.png)
+ Choose **"AWS service"**, then select **"EC2"**, and click **"Next"**.
![AWS Services](/images/4.sectionb/005-awsservice.png)
![EC2 Service Select](/images/4.sectionb/006-ec2serviceselect.png)
+ Search for **"AmazonSSMManagedInstanceCore"**, select it, and click **"Next"**.
![SSM Role](/images/4.sectionb/007-ssmrole.png)
+ Name the role ```detectionServer-vpn-ssm-ec2-instance-profile```, then click **"Create role"**.
![Name of the role](/images/4.sectionb/008-rolename.png)
![Submit](/images/4.sectionb/009-createrolesubmit.png)

{{% notice note%}}
We have successfully created a security group and IAM role for an EC2 instance.
{{% /notice %}}