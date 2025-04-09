---
title : "Provision an EC2 instance to host the VPN in the AWS Local Zone"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

1. Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)

2. Launch an instance and name it: ```localZone-vpn-instance```.
![Launch VPN instance](/images/5.sectionc/000-vpninstance.png)

3. Choose an AMI: **Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Type**.
![Select AMI](/images/5.sectionc/001-ami.png)

4. Select instance Type: Use **c5.large**. 

{{% notice warning%}}
Verify the type availability in your AWS Local Zone if you have used another AWS Local Zone than **us-west-2-lax-1**.
{{% /notice %}}

5. Select **"Proceed without a key pair"**: Use AWS Systems Manager for management instead of SSH keys.

![Instance type and key pair](/images/5.sectionc/002-typekp.png)

6. Configure **"Network settings"**.
+ Select the **vpc-extended-to-aws-local-zone** VPC and **my-subnet-in-aws-local-zone** subnet.
+ **Enable "Auto-assign public IP"** to make the instance accessible over the internet.
![Configure Network Settings](/images/5.sectionc/003-networksettings.png)


7. Create **Security Group**: Allow **UDP ports 500 & 4500**, and **TCP port 8554** from the private IP of the detector server.
![Create Security Group](/images/5.sectionc/004-sg.png)
![Rule 1](/images/5.sectionc/005-rule1.png)
![Rule 2, 3](/images/5.sectionc/006-rule23.png)

8. Assign **IAM Profile**: Use **detectionServer-vpn-ssm-ec2-instance-profile** for AWS SSM.
![IAM Profile](/images/5.sectionc/007-iamprofile.png)


9. **Launch instance**.
![Launch instance](/images/5.sectionc/008-launchinstance.png)


10. **Disable Source/Destination Check** via **Actions** → **Networking** → **Change source/destination check**.
![Change source/destination check](/images/5.sectionc/009-changesrcdescheck.png)
![Stop source/destination check](/images/5.sectionc/010-stopsrcdescheck.png)

11. Note the **public IP of VPC instance** for later use.
![Copy public IP](/images/5.sectionc/011-copypublicip.png)
