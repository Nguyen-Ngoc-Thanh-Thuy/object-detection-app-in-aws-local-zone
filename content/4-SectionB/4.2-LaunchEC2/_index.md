---
title : "Launch an EC2 Instance in the AWS Local Zone"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

**1. Open the EC2 Service.**
+ Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).

**2. Launch a new instance.**
+ Click **"Launch instance"**.
![Launch Instance button](/images/4.sectionb/010-launchinstancebutton.png)
+ Instance Name: Enter ```detectorServer```.
![Name an instance](/images/4.sectionb/011-detectorservername.png)

**3. Choose an Amazon Machine Image (AMI).**: 
+ Select ```Ubuntu 22.04 - NICE DCV with NVIDIA TESLA GPU Driver```.
![Browse AMIs](/images/4.sectionb/012-browseami.png)
![Select AMI](/images/4.sectionb/013-selectami.png)
![Suscribe AMI](/images/4.sectionb/014-subscribeami.png)
![Submit AMI](/images/4.sectionb/015-submitami.png)

**4. Select Instance type.**
+ Choose **g4dn.2xlarge** (suitable for GPU workloads).
![Select instance type](/images/4.sectionb/016-instancetype.png)

**5. Configure Key pair.**
+ Select **"Proceed without a key pair"** (we will use AWS Systems Manager to connect).
![Without key pair option](/images/4.sectionb/017-withoutkeypair.png)

**6. Configure Network settings.**
+ Click **"Edit"**.
![Edit Network Settings](/images/4.sectionb/018-editnetworksettings.png)
+ **VPC**: Choose **"vpc-extended-to-aws-local-zone"**.
+ **Subnet**: Choose **"my-subnet-in-aws-local-zone"**.
+ **Enable Public IP** (to access the server over the Internet).
+ **Security Group**: Select **"my-detectorServer-sg"** (created in Step 1).
![Configure Network Settings](/images/4.sectionb/019-networksettings.png)

**7. Configure Storage.**
+ Set the Root volume Size to **32 GiB**.
![Configure storage](/images/4.sectionb/020-storage.png)

**8. Assign IAM Role.**
+ In **Advanced details**, locate **IAM instance profile**.
+ Select **"detectionServer-ec2-instance-profile"**.
![Select IAM Profile](/images/4.sectionb/021-advanceddetails.png)

**9. Launch the Instance.**
+ Click **"Launch instance"**.
![Launch instance](/images/4.sectionb/022-launchinstance.png)

{{% notice warning%}}
The AMI registration process may take some time. Please keep the browser open to ensure the EC2 instance is launched. Once the subscription is completed, the instance will launch automatically.
{{% /notice %}}
![Subscription warning](/images/4.sectionb/023-subscriptionwarning.png)

{{% notice note%}}
The EC2 instance is now being deployed in the AWS Local Zone.
{{% /notice %}}
![Launch instance succesfully](/images/4.sectionb/024-launchsuccessfully.png)



