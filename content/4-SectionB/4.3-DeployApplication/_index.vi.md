---
title : "Triển khai ứng dụng phát hiện đối tượng"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

**1. Truy cập EC2 Instance.**  
+ Truy cập [dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home).
+ Chọn máy ảo **DetectorServer**.  
+ Nhấp vào **"Connect"** để truy cập máy ảo.  
![Kết nối instance](/images/4.sectionb/025-instanceconnect.png)

**2. Kết nối qua Session Manager**  
+ Trong các tùy chọn kết nối, chọn **"Session Manager"**. Có thể mất một vài phút để Session Manager sẵn sàng.  
+ Khi đã sẵn sàng, nhấp vào nút **"Connect"** để bắt đầu một phiên làm việc với máy ảo EC2.  
![Kết nối instance qua SSM](/images/4.sectionb/026-ssmconnect.png)

**3. Triển khai Ứng Dụng**: Chúng ta sẽ chạy một loạt các lệnh để thiết lập môi trường, tải các file cần thiết và cài đặt các phụ thuộc.

+ *Cập nhật hệ thống và cài đặt phần mềm cần thiết*.  
  ```
  sudo apt update && sudo apt upgrade -y
  sudo apt install -y git nginx unzip python3-pip
  ```  
  ![Cập nhật hệ thống](/images/4.sectionb/027-update.png)  
  ![Cài đặt nginx và unzip](/images/4.sectionb/028-installnginxunzip.png)

+ *Clone YOLOv7 repository. Sau đó, chuyển vào thư mục yolov7, nơi mã nguồn đã được clone.*  
  ```
  sudo git clone https://github.com/WongKinYiu/yolov7.git
  cd yolov7
  ```  
  ![Lệnh git clone](/images/4.sectionb/029-gitclone.png)

+ *Tải YOLOv7 pre-trained model.*
  ```
  sudo wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7-tiny.pt
  ```  
  ![Lệnh wget](/images/4.sectionb/030-wget.png)

+ *Tải file dùng trong triển khai web chạy ứng dụng phát hiện đối tượng.*  
  ```
  sudo curl 'https://static.us-east-1.prod.workshops.aws/public/bdfac965-db9c-4fa3-9d89-af97e8cdf015/assets/src/ObjectDetection/objectDetection.zip' --output objectDetection.zip
  ```  
  ![Lệnh curl](/images/4.sectionb/031-curl.png)

+ *Sau đó, giải nén tệp zip đã tải xuống vào thư mục hiện tại.*  
  ```
  sudo unzip objectDetection.zip
  ```  
  ![Lệnh unzip](/images/4.sectionb/032-unzip.png)

+ *Cấu hình Nginx dùng cho việc triển khai web.*
  - *Sao chép file cấu hình Nginx đã cung cấp vào thư mục ***/etc/nginx/nginx.conf.*** .*
    ```
    sudo cp nginx.conf /etc/nginx/nginx.conf
    ```  
    ![Sao chép file nginx](/images/4.sectionb/033-copynginx.png)

  - *Mở file ***nginx.conf*** và thay đổi người dùng mà Nginx chạy dưới quyền, từ ***nginx*** thành ```ubuntu``` để đảm bảo quyền truy cập đúng trên hệ thống.*  
    ![Thay đổi người dùng](/images/4.sectionb/034-changeuser.png)

  - *Khởi động lại Nginx để áp dụng cấu hình mới.* 
    ```
    sudo systemctl restart nginx
    ```  
    ![Khởi động lại nginx](/images/4.sectionb/035-restartnginx.png)

+ *Cài đặt các phụ thuộc Python cần thiết.*  
  ```
  python3 -m pip install --no-cache-dir -r requirements.txt
  python3 -m pip install --no-cache-dir -r objectdetection_requirements.txt
  ```  
  ![Cài đặt các gói python](/images/4.sectionb/036-pythonpackage.png)  
  ![Cài đặt các gói python](/images/4.sectionb/037-pythonpackage.png)

+ *Chạy script ứng dựng phát hiện đối tượng.* 
  ```
  python3 ObjectDetection.py
  ```  
  ![Chạy ứng dụng detector](/images/4.sectionb/038-runapp.png)

{{% notice note %}}  
Các bước trên giúp  thiết lập và triển khai ứng dụng phát hiện đối tượng, cho phép phát hiện các đối tượng bằng mô hình YOLOv7.  
{{% /notice %}}
