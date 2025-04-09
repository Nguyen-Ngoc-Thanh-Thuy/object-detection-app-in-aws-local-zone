---
title : "Configure the newly created AWS Local Zone subnet as Public"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---

**1. Create an Internet Gateway (IGW)**
+ Open **VPC Console** and select **"Internet gateways"** from the left panel. Click **"Create internet gateway"**. 
![Create IGW button](/images/3.sectiona/014-createigw.png)
+ Enter a name tag ```igw-aws-local-zone```. Click **"Create internet gateway"**.
![Create IGW](/images/3.sectiona/015-createigw.png)

**2. Attach VPC**
+ In the **Internet gateways** section, select the **igw-aws-local-zone** IGW we just created. 
+ Click **"Actions"** → **"Attach to VPC"**.
![IGW attach to VPC](/images/3.sectiona/016-igwattachvpc.png)
+ Select **vpc-extended-to-aws-local-zone** VPC. Click **"Attach internet gateway"**.
![VPC attached](/images/3.sectiona/017-vpcattached.png)

**3. Update the Route Table to use the Internet Gateway**
+ In the **VPC Console**, go to **"Route tables"** from the left panel.
+ Select the Route Table associated with **vpc-extended-to-aws-local-zone** VPC.
+ Click **"Routes"** → **"Edit routes"**.
![Edit routes in Route Table](/images/3.sectiona/018-editroutes.png)
+ Click **"Add Route"**.
![Add routes button](/images/3.sectiona/019-addroutebutton.png)
+ In **Destination**, enter ```0.0.0.0/0``` (this means all Internet traffic).
+ In **Target**, select **"Internet Gateway"**, then choose the **igw-aws-local-zone** IGW we created.
+ Click **"Save changes"**.
![Add route to igw](/images/3.sectiona/020-routetoigw.png)

{{% notice note %}}
The AWS Local Zone subnet is now public, meaning instances inside it can access the Internet.
{{% /notice %}}
