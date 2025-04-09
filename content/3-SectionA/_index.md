---
title : "Section A - Enable an AWS Local Zone and expand the VPC"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

This section provides guidance on deploying resources within an AWS Local Zone, with a particular emphasis on extending an VPC into the Local Zone.

![Project Architecture](/images/architecture.png)

### Overview of deployment steps
This section consists of four main steps:
- Use the AWS region us-west-2 as the primary region. 
- Opt-in the AWS Local Zone us-west-2-lax-1.
- Establish and extend an VPC into an AWS Local Zone.
- Configure a public subnet in an AWS Local Zone.

### Content
3.1. [Enable an AWS Local Zone](3.1-enableawslocalzone/) \
3.2. [Expand the VPC to the AWS Local Zone](3.2-expandvpctolocalzone/) \
3.3. [Configure the newly created AWS Local Zone subnet as Public](3.3-createlocalzonesubnet/)