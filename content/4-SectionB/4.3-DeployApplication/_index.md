---
title : "Deploy an object detection application"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

**1. Access EC2 Instance.**
+ Go to [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
+ Select the Instance: Choose the **DetectorServer** instance.
+ Click on **"Connect"** to access the instance.
![Connect instance](/images/4.sectionb/025-instanceconnect.png)

**2. Connect Using Session Manager.**
+ In the options to connect, choose **"Session Manager"**. It may take a minute for the Session Manager to be ready.
+ Once ready, click on the **"Connect"** button to start a session with the EC2 instance.
![Connect instance by SSM](/images/4.sectionb/026-ssmconnect.png)

**3. Deploy the Application.**: Now, we will run a series of commands to set up the environment, download necessary files, and install dependencies.

+ *Update the system and install required software.*
  ```
  sudo apt update && sudo apt upgrade -y
  sudo apt install -y git nginx unzip python3-pip
  ```
  ![update command](/images/4.sectionb/027-update.png)
  ![install nginx and unzip](/images/4.sectionb/028-installnginxunzip.png)

+ *Clone YOLOv7 repository. Then, navigates into the yolov7 directory, where the code has been cloned.*
  ```
  sudo git clone https://github.com/WongKinYiu/yolov7.git
  cd yolov7
  ```
  ![git clone command](/images/4.sectionb/029-gitclone.png)

+ *Download YOLOv7 pre-trained model.*
  ```
  sudo wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
  ```
  ![wget command](/images/4.sectionb/030-wget.png)

+ *Download object detection web files.*
  ```
  sudo curl 'https://static.us-east-1.prod.workshops.aws/public/bdfac965-db9c-4fa3-9d89-af97e8cdf015/assets/src/ObjectDetection/objectDetection.zip' --output objectDetection.zip
  ```
  ![curl command](/images/4.sectionb/031-curl.png)

+ *Then extracts the downloaded zip file into the current directory.*
  ```
  sudo unzip objectDetection.zip
  ```
  ![unzip command](/images/4.sectionb/032-unzip.png)

+ *Configure Nginx to serve the application.*
  - *Copy the provided Nginx configuration file to the correct directory.*
    ```
    sudo cp nginx.conf /etc/nginx/nginx.conf
    ```
    ![copy nginx field](/images/4.sectionb/033-copynginx.png)

  - *Open the ***nginx.conf*** file and change the user that Nginx runs as, from ***nginx*** to ```ubuntu``` to ensure the proper permissions on our system.*
    ![change user](/images/4.sectionb/034-changeuser.png)


  - *Restart Nginx to apply the new configuration.*
    ```
    sudo systemctl restart nginx
    ```
    ![restart nginx](/images/4.sectionb/035-restartnginx.png)

+ *Install required Python dependencies.*
  ```
  python3 -m pip install --no-cache-dir -r requirements.txt
  python3 -m pip install --no-cache-dir -r objectdetection_requirements.txt
  ```
  ![install python packages](/images/4.sectionb/036-pythonpackage.png)
  ![install python packages](/images/4.sectionb/037-pythonpackage.png)


+ *Run the object detection script.*
  ```
  python3 ObjectDetection.py
  ```
  ![run detector application](/images/4.sectionb/038-runapp.png)


{{% notice note %}}
By following these steps, we can set up and deploy the object detection application, which will allow us to detect objects using the YOLOv7 model.
{{% /notice %}}