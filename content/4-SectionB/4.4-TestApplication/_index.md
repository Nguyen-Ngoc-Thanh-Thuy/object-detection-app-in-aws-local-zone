---
title : "Verify connectivity to the application"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

**1. Find the public IPv4 DNS of object detector EC2 instance**
+ Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home)
+ Select the **object detector instance**, and copy the **Public IPv4 DNS**.
![Public IPv4 DNS](/images/4.sectionb/039-publicdns.png)

**2. Copy the Public IPv4 DNS and open in a web browser.** 
If we can see the architecture diagram, it means our application is up and running properly, and we have successfully tested our connectivity.
![Access web](/images/4.sectionb/040-accessweb.png)

{{% notice info %}}
Note that at this stage of the workshop, we will only see the architecture diagram on the left side of the page.
{{% /notice %}}