---
title : "Test the object detection application"
date : "`r Sys.Date()`"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

**1. Start the video streaming application.**
+ Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).

+ Connect to the video streamer instance using **AWS SSM**.
![SSM Connect](/images/6.sectiond/000-ssm.png)
![SSM Connect](/images/6.sectiond/001-ssm.png)

+ Run the **streaming application**.
    - Execute the following command in the terminal to start the RTSP streaming server:
    ```
    sudo su ubuntu
    cd /home/ubuntu
    docker run --rm -it -e RTSP_PROTOCOLS=tcp -p 8554:8554 -p 1935:1935 -p 8888:8888 -p 8889:8889 aler9/rtsp-simple-server &
    ```
    ![Streaming server](/images/6.sectiond/002-streaming.png)

    - Download the sample video:
    ```
    curl 'https://static.us-east-1.prod.workshops.aws/public/bdfac965-db9c-4fa3-9d89-af97e8cdf015/assets/src/videostreamer/street_day.mp4' --output street_day.mp4
    ```
    ![Streaming server](/images/6.sectiond/003-streaming.png)
    

    - Start streaming the video via RTSP:
    ```
    ffmpeg -re -stream_loop -1 -i street_day.mp4 -vcodec libx264 -preset ultrafast -tune zerolatency -pix_fmt yuv422p -f rtsp -rtsp_transport tcp rtsp://localhost:8554/mystream
    ```
    ![Streaming server](/images/6.sectiond/004-streaming.png)
    ![Streaming server](/images/6.sectiond/005-streaming.png)
    
**2. Start the object detection application.**
+ On the **EC2** Management Console, connect to the **detectorServer instance** using **AWS SSM**.
![SSM Connect](/images/6.sectiond/006-ssm.png)

+ Execute the following command (replace <private IP of videostreamer instance> with the private IP address of the video streamer instance):
    ```
    sudo su ec2-user
    cd /home/ec2-user/yolov7
    python3 ObjectDetection.py -s rtsp://<private IP videostreamer instance>:8554/mystream --weights yolov7-tiny.pt --enable-detection
    ```
    ![Streaming](/images/6.sectiond/007-streaming.png)

**3. Check results in the web browser.**
+ Open a web browser. Access the **Public IPv4 DNS of the detectorServer** to view the real-time object detection results.
![Test](/images/6.sectiond/008-test.png)
![Test](/images/6.sectiond/009-test.gif)
![Test](/images/6.sectiond/010-test.png)





