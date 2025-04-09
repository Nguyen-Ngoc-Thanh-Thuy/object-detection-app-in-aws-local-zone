---
title : "Section B - Provision an EC2 Instance in an AWS Local Zone and establish application connectivity"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---
This section provides a comprehensive guide on deploying an EC2 instance within an AWS Local Zone and launching an object detection application.

![Project Architecture](/images/architecture.png)

### Overview of deployment steps
The deployment process comprises four key steps:
   - **Configuring Security Groups** – Establishing security rules to permit HTTP traffic exclusively from our IP address to the object detection instance.
   - **Launching an EC2 Instance** – Deploying an EC2 instance within the AWS Local Zone.
   - **Installing the object detection application** – Setting up the necessary dependencies and deploying the application on the newly created instance.
   - **Validating connectivity** – Testing accessibility by navigating to the application's public address via a web browser.

### Content
4.1. [Configure Security Groups and ddefine an IAM Role](4.1-createsgandrole/) \
4.2. [Launch an EC2 Instance in the AWS Local Zone](4.2-launchec2/) \
4.3. [Deploy an object detection application](4.3-deployapplication/) \
4.4. [Verify connectivity to the application](4.4-testapplication)