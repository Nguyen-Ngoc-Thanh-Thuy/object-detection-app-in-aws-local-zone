---
title : "Deploying a low-latency object detection in AWS Local Zone for streaming video via Site-to-Site VPN using OpenSwan"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Deploying a low-latency object detection application in AWS Local Zone for streaming video via Site-to-Site VPN using OpenSwan

### Overall
In this lab, we will deploy and configure a video streaming system from a virtual on-premises environment to a low-latency object detection application in AWS Local Zones via a Site-to-Site (S2S) VPN connection using OpenSwan. 

We will practice steps including setting up the network resources in AWS, extending a VPC to an AWS Local Zone, deploying a VPN, streaming real-time video, and running an object detection application at the edge.

This lab helps us understand how to leverage AWS Local Zones to reduce latency in real-time applications while optimizing connectivity between on-premises environments and AWS.

![Project Architecture](/static/images/architecture.png)

### Content
 1. [Introduction ](/1-introduce/)
 2. [Preparation](2-preparation/)
 3. [Section A - Enable an AWS Local Zone and expand the VPC](3-sectiona/)
 4. [Section B - Provision an EC2 Instance in an AWS Local Zone and establish application connectivity](4-sectionb/)
 5. [Section C - Configure VPN connection to bridge on-premises environment with AWS Local Zone](5-sectionc/)
 6. [Section D - Validate the application deployment](6-partd/)
 7. [Cleanup](7-cleanup/)

