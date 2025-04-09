---
title : "Requesting CPU Quota Increase"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

Before starting the workshop, we need to ensure that the necessary resources are allocated adequately to avoid interruptions during the practice. Specifically, since the object detection server will run on an EC2 instance of type **g4dn.2xlarge**, we need to **request a quota for 8 vCPUs** of **type G** in the us-west-2 Region.

The g4dn.2xlarge instance is equipped with an NVIDIA T4 GPU, making it suitable for AI/ML tasks and real-time video processing. However, due to AWS's default limits, vCPUs for G-type instances may not be sufficiently allocated in our account. Therefore, before proceeding, visit AWS Service Quotas, check the current quota, and submit an upgrade request if necessary.

{{% notice warning %}}
This preparation ensures that when launching the instance, we will have enough resources and avoid errors due to quota limitations. If the quota increase request is not approved, we may encounter an **"InstanceLimitation" error** when creating the instance, which could disrupt the workshop deployment.
{{% /notice %}}

1. Go to the **Service Quotas** console page.
![Service Quotas Page.](/images/2.preparation/000-requestquota.png)

2. In the **Service Quotas dashboard**, select **AWS services**
  + Search for **Amazon Elastic Compute Cloud (Amazon EC2)**
  ![Select Amazon EC2 in AWS Services.](/images/2.preparation/001-requestquota.png)

3. Select **Running On-Demand G and VT instances**, then click **Request increase a account level** button.
![Select Running On-Demand G and VT instances.](/images/2.preparation/002-requestquota.png)

4. Enter **"8"** in the **Increase quota value** field and click **Request** to submit the request.
![Enter quota value and submit request.](/images/2.preparation/003-requestquota.png)

5. **Quota increase request approved**. We can now use G-series instances (g4dn.2xlarge) in us-west-2 (Oregon) with a maximum limit of 8 vCPUs.
![Quota successfully increased to 8vCPUs.](/images/2.preparation/004-requestquota.png)
![Quota successfully increased to 8vCPUs.](/images/2.preparation/005-requestquota.png)

