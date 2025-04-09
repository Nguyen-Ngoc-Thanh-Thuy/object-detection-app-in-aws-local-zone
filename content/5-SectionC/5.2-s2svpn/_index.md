---
title : "Configure the on-premises VPN using site-to-site (S2S) VPN"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---
In this section, we will simulate an on-premises environment by deploying an VPC in a **us-east-1** region and using the AWS Site-to-Site VPN service.

**1. Download the file [streamingServer_over_vgw.json](http://localhost:1313/data/streamingServer_over_vgw.json).**

{{% notice warning %}}
The instance type **c5.2xlarge** is not available in Availability Zone **us-east-1e** of the us-east-1 region and is only supported in AZs **us-east-1a to us-east-1d** and **us-east-1f**. Therefore, the JSON file explicitly specifies us-east-1a for deploying the private subnet to ensure compatibility when creating future c5.2xlarge EC2 instances.
{{% /notice %}}
![Availability Zone error](/images/5.sectionc/012-azerror.png) \
![Availability Zone change](/images/5.sectionc/013-azchange.png)

{{% notice note %}}
The JSON file is used to define infrastructure on AWS using CloudFormation. It includes resources which are essential for setting up the virtual environment: \
🔹**On-premise VPC.** \
🔹**Private subnet to deploy EC2 Streaming instance.** \
🔹**Private Route Table** \
🔹**Public Subnet for Internet.** \
🔹**Public Route Table.** \
🔹**Internet Gateway.** \
🔹**NAT Gateway.** \
🔹**Elastic IP.** \
🔹**On-premise VPN Gateway.** \
🔹**Local Zone Gateway.** \
🔹**VPN connection.** \
🔹**Video streamer EC2 instance.** \
...
{{% /notice %}}


**2. Create a stack in AWS CloudFormation**
+ Go to **AWS Console**, search for **CloudFormation**, and select the service. Click **"Create stack"** → **With new resources (standard)**
![CloudFormation](/images/5.sectionc/014-cloudformation.png)
+ Select **Choose an existing template** → **"Upload a template file"** → Click **"Choose file"** and upload **streamingServer_over_vgw.json**.
![Stack](/images/5.sectionc/015-stack.png)
+ Click **"Next"**.

**3. Provide required information for deployment**
+ Stack name: Enter a name ```streamingServer```.
+ Instance type: Select **c5.2xlarge**.
+ Give the **private IP of the object detector instance**. This address will be used in the streaming instance’s security group.
+ Give **public IP of the VPN instance** in AWS Local Zone (deployed in the previous step).
+ Click "Next".
![Stack](/images/5.sectionc/017-stack.png)
+ On the **Review page**, check the box to **Acknowledge that AWS CloudFormation may create IAM resources with custom names**.
![Stack](/images/5.sectionc/018-stack.png)
+ Review and click **"Submit"** to start deploying the simulated on-premises environment.

{{% notice info %}}
The VPN setup may take 3-5 minutes to complete.
{{% / notice %}}
![Stack complete](/images/5.sectionc/019-stackcomplete.png)


**4. Check VPN Status**
+ Go to [VPC service management console](https://console.aws.amazon.com/vpc/home)
+ In the left panel, select **Site-to-Site VPN connections**.
+ **Ensure that:** 
    - Tunnel status is **"Down"** (this is the default state before further configuration).
    ![VPN connection](/images/5.sectionc/020-vpnconnection.png)
    - **Customer Gateway Address** matches the **Public IP of the localZone-vpn-instance**.
    ![VPN connection](/images/5.sectionc/021-vpnconnection.png)


**5. Download  VPN Configuration File**
+ Select the **vpn-OnPremise-LocalZone** connection and click **"Download configuration"** button.
![VPN configuration file](/images/5.sectionc/022-configfile.png)

+ Select **Generic**. Then click **"Download"** to get the **VPN configuration file**.
![VPN configuration file](/images/5.sectionc/023-configfile.png)

+ The file will look like this.
![VPN configuration file](/images/5.sectionc/024-configfile.png)


{{% notice note %}}
📌 **Important notes about the configuration file** \
🔹 "Left IP" must be the **Public IP of localZone-vpn-instance (Customer Gateway)**. \
🔹 "Right IP" must be the **Public IP of the VPN gateway on the simulated on-premises environment (Virtual Private Gateway)**.
{{% /notice %}}

After having downloaded this configuration file, we will apply it to the localZone-vpn-instance in the next step. 


