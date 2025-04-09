---
title : "Update VPC Route Tables for VPN traffic routing"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

Now that the VPN connection is set up, we need to update the VPC route tables in our AWS Local Zone to direct traffic to the on-premises network through the VPN instance.

**1. Access Local Zone route tables.**
+ Go to [VPC service management console](https://console.aws.amazon.com/vpc/home) and navigate to the **Route Tables** section. Find the **route table of "vpc-extended-to-aws-local-zone VPC".**
![Update Route Table](/images/5.sectionc/044-updatert.png)

**2. Edit routes.**
+ Click **"Edit routes"** → Select **"Add route"**
![Update Route Table](/images/5.sectionc/045-updatert.png)
![Update Route Table](/images/5.sectionc/046-updatert.png)

**3. Add a new route.**
+ **Destination:** **172.16.0.0/24 (on-premises network)**.
+ **Target:** Select the **localZone-vpn-instance** (Openswan VPN instance).
+ Click **"Save changes"** to apply the new route.
![Update Route Table](/images/5.sectionc/047-updatert.png)

{{% notice note %}}
We have successfully updated the Local Zone route table. This ensures that traffic destined for the on-premises network is routed through your VPN instance.
{{% /notice %}}