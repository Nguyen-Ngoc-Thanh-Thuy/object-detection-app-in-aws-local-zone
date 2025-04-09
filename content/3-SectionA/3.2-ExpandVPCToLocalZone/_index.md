---
title : "Expand the VPC to the AWS Local Zone"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 3.2. </b> "
---

**1. Create a new VPC**
+ Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
+ Click **"Create VPC"**.
![Create VPC button](/images/3.sectiona/005-createvpc.png)
+ Choose **"VPC Only"**, then enter a VPC name ```vpc-extended-to-aws-local-zone```.
+ Set an IPv4 CIDR block ```10.0.0.0/24```.
![VPC Configuration](/images/3.sectiona/006-vpcconfig.png)
+ Click **"Create VPC"*** to complete.
![Submit to create VPC](/images/3.sectiona/007-createvpcsubmit.png)

**2. Create a Subnet in AWS Local Zone**
+ In the left panel, select **"Subnets"**, then click **"Create subnet"**.
![Create Subnet button](/images/3.sectiona/008-createsubnet.png)
+ Choose a newly created VPC **vpc-extended-to-aws-local-zone**.
![Create Subnet in VPC](/images/3.sectiona/009-subnetinvpc.png)
+ Enter a subnet name ```my-subnet-in-aws-local-zone```.
+ Select the AWS Local Zone **us-west-2-lax-1a** for **Availability Zone** field.
+ Define the CIDR block ```10.0.0.0/25```.
![Subnet Configuration](/images/3.sectiona/010-subnetconfig.png)
+ Click **"Create subnet"**.
![Submit to create Subnet](/images/3.sectiona/011-createsubnetsubmit.png)

**3. Enable DNS Hostnames for VPC**
+ Go to **"Your VPCs"**.
+ Select **vpc-extended-to-aws-local-zone** VPC.
+ Select **Action** button, then click **"Edit VPC settings"**.
![Edit VPC Settings](/images/3.sectiona/012-editvpc.png)
+ Enable **"DNS hostnames"** to automatically assign a DNS name to EC2 instances and click **"Save changes"**.
![Enable DNS hostnames](/images/3.sectiona/013-enabledns.png)

{{% notice note %}}
We have just extended the VPC to the AWS Local Zone.
{{% /notice %}}