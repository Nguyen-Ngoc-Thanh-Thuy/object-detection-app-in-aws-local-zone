---
title : "Section D - Validate the application deployment"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

In this section, we will verify the functionality of the system by streaming video from the on-premises environment and executing the object detection application within the AWS Local Zone.

![Project Architecture](/images/architecture.png)

### Overview of the testing process
- The testing phase comprises four critical steps:
   + **Initiate the video streaming application** – This step involves launching the video streaming service from the on-premises setup to establish a real-time feed.
   + **Run the object detection application** – The AI-based object detection model will be activated within the AWS Local Zone to process the incoming video stream.
   + **Access the web for testing** – Open a web browser and navigate to the web to observe and validate the real-time detection results.

### Content
6.1. [Test the object detection application](6.1-testapp/)
