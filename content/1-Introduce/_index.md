---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
### ISSUE

Before **AWS Local Zones** were introduced, applications requiring low latency faced several challenges due to the geographical distance between end users and AWS Regions.

**1. High latency due to distance from the main AWS Region.**
- Previously, applications were typically deployed in a central AWS Region, but users could be located far from that region. 
- When data had to travel long distances from the AWS Region to the end user’s device, high latency could negatively impact user experience, especially for: 
    + Gaming and livestream applications
    + AR/VR applications
    + Real-time financial transaction systems
    + AI/ML applications that require fast data processing from sensors/IoT devices

**2. On-premise applications offer low latency but lack scalability.**
- Before **AWS Local Zones**, some businesses had to run applications in their own data centers (on-premises) close to users to ensure low latency. 
- However, on-premise solutions had some limitations: 
    + High costs of infrastructure investment
    + Lack of flexible resource scaling, unlike AWS

### SOLUTION

To address the latency issues caused by the physical distance between users and AWS Regions, **AWS introduced AWS Local Zones**. These are extensions of AWS Regions that bring compute, storage, and networking resources closer to end users in metropolitan areas.

#### What is "AWS Local Zones"?
- AWS Local Zones are extensions of AWS Regions that bring compute, storage, and networking services closer to end-users in specific geographic locations, providing them very low latency access to the applications running locally.
- AWS Local Zones are also connected to the parent region via Amazon’s redundant and very high bandwidth private network, giving applications running in AWS Local Zones fast, secure, and seamless access to the rest of AWS services.

#### Key Benefits of AWS Local Zones
- **Reduced Latency**
    + By placing workloads closer to end-users, AWS Local Zones minimize the round-trip time for data processing.
    + Suitable for real-time applications like gaming, media streaming, machine learning inference, and AR/VR.
- **Hybrid Cloud & On-Premise Integration**
    + AWS Local Zones support AWS Direct Connect and AWS VPN, allowing seamless integration with on-premise environments.

#### Who should use AWS Local Zones?
- We can use AWS Local Zones to deploy workloads closer to our end-users for low-latency requirements. AWS Local Zones have their own connection to the Internet and support AWS Direct Connect, so resources created in the Local Zone can serve local end-users with very low-latency communications.

### ARCHITECTURE

![Project Architecture](/images/architecture.png)

##### AWS cloud (us-west-2: Oregon)
- **VPC 10.0.0.0/24**: A VPC that hosts AWS resources in AWS Region us-west-2.
- **Public Subnet (10.0.0.0/25)**: Contains key components:
    + **Detection Server**: A server that performs object detection tasks
    + **VPN Instance (OpenSwan)**: A server acting as a Customer Gateway to establish a VPN connection with the simulated on-premise environment.
- **Internet Gateway**: Provides Internet access to resources in AWS Cloud.
- **AWS Systems Manager**: Manages systems and allows remote access to EC2 without direct SSH/RDP.

##### Virtual on-premise environment (us-east-1: Virginia)
- **VPC 172.16.0.0/24**: Simulates an on-premise network using a VPC in a different AWS Region (us-east-1).
- **Private Subnet (172.16.0.0/25)**:
    + Streaming Server: A server that handles streaming or data transmission from the on-premise environment to the cloud.
- **Public Subnet (172.16.0.128/25)**:
    + NAT Gateway: Allows private subnet instances to access the Internet without requiring a public IP.
- **Internet Gateway**: Provides Internet access.

##### VPN Site-to-Site
- **VPN Gateway** (in the virtual on-premise VPC) connects to the VPN instance (OpenSwan) in AWS Cloud.
- The VPN Instance acts as a **Customer Gateway** (using OpenSwan) to establish a secure connection with the on-premise VPC.
- VPN Site-to-Site connection enables servers in AWS Local Zone to communicate securely with the simulated on-premise environment in us-east-1 without requiring public Internet access.


### PROCESS
- In this workshop, we are going to deploy an object detector application closer to our on-premises location.
- From a simulated on-premises location wewe will use a pre deployed instance to stream a video feed to the closest AWS Local Zone.
- To avoid sending the video feed over the public Internet, we will deploy a VPN instance in our AWS Local Zone and connect it to our simulated on-premises VPN.
- Finally, we will deploy and install an object detection application in the selected AWS Local Zone, that will detect persons and objects from the video stream.
- The workshop will go through the process of:
    + Using AWS Console to perform the workshop.
    + Enabling an AWS Local Zone.
    + Creating and extending the VPC to the AWS Local Zone.
    + Deploying an latency sensitve application (running object detection application at the edge) in the AWS Local Zone.
    + Deploying a VPN instance in the AWS Local Zone.
    + Using a pre deployed video streaming application in simulated on-premises environment.
    + Enabling the object detection application and running our tests.

### SECTIONS
- This workshop consists of 4 sections as shown in the architecure above:
    + **Section A - Enable an AWS Local Zone and expand the VPC:** This section, will guide us to enable our AWS Local Zone, create an VPC and extend it to our AWS Local Zone by creating a public subnet in the AWS Local Zone.
    + **Section B - Provision an EC2 Instance in an AWS Local Zone and establish application connectivity:** In this section, we will deploy our first EC2 instance in our AWS Local Zone, and make sure we can access our web server over Internet.
    + **Section C - Configuring a VPN connection to bridge an on-premises environment with an AWS Local Zone:** Now that our application is deployed and running in our AWS Local Zone, let's connect our simulated on-premises environment to our AWS Local Zone using a VPN.
    + **Section D - Validate the application deployment:** In this final section, we will use the simulated on-premises environment to stream the video to the AWS Local Zone where we will be running our object detection application.

### TECHNOLOGIES

#### Openswan
Openswan is a tool that helps secure network connections using IPsec (a protocol for encrypting Internet traffic). It runs on Linux and supports advanced security features like IKEv2, X.509 certificates, and NAT traversal. It's open-source and continues the development of FreeS/WAN.

#### ffmpeg
FFmpeg is a powerful multimedia tool that can play, convert, stream, and edit audio/video files. It supports almost all formats, from old to modern ones. It runs on Linux, Windows, Mac, and more. FFmpeg is also open-source, but some parts follow stricter licensing rules.

#### rtsp-simple-server
rtsp-simple-server is a lightweight and easy-to-use server for handling live video and audio streaming. It acts as a server or proxy to send and receive RTSP streams. It doesn’t require extra dependencies and is open-source.