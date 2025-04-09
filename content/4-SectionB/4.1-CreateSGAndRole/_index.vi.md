---
title : "Cấu hình Security Groups và IAM Role"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

**1. Tạo một Security Group**  
+ Truy cập [dịch vụ VPC](https://console.aws.amazon.com/vpc/home)  
+ Trong bảng điều khiển bên trái, nhấp vào **"Security groups"**, sau đó chọn **"Create security group"**.  
![Nút Create Security Group](/images/4.sectionb/000-createsg.png)
+ Bây giờ, cấu hình **security group cho Detector Server**:  
  - Tên Security Group: Nhập ```my-detectorServer-sg```.  
  - Description: Thêm ghi chú như ```HTTP - web server, TCP 80 và 443 - linux repos, TCP 8554 - RSTP```.  
  - Chọn **vpc-extended-to-aws-local-zone VPC**.  
  ![Cấu hình Security Group](/images/4.sectionb/001-sgconfig.png)

**2. Thêm các quy tắc vào Security Group**  
+ Nhấp vào **"Add rule"**.  
+ Đối với **Inbound rules**: Chọn HTTP là loại. Đặt Source thành **"My IP"**.  
  ![Inbound ruless trong Security Group](/images/4.sectionb/002-inboundrule.png)  
+ Đối với **Outbound rulesrules**, thêm các quy tắc sau:  
  - **TCP trên cổng 80 và 443** (với destination: 0.0.0.0/0) → Cần cho các bản cập nhật gói Linux.  
  - **TCP trên cổng 8554** (với destination: 0.0.0.0/0) → Cần cho RTSP streaming.  
  ![Outbound rules trong Security Group](/images/4.sectionb/003-outboundrule.png)

{{% notice warning%}}  
Cổng 8554 bắt buộc dùng cho RTSP. Ở các bước sau, chúng ta sẽ cập nhật security group để giới hạn lưu lượng outbound chỉ cho máy ảo streaming thôi, chứ không mở rộng ra 0.0.0.0/0 .  
{{% /notice %}}

**3. Tạo một IAM Role**  
+ Mở **AWS Console**, nhập **"IAM"**, và chọn dịch vụ **IAM**.  
+ Trong bảng điều khiển bên trái, nhấp vào **"Roles"**, sau đó nhấp vào **"Create role"**.  
![Tạo IAM Role](/images/4.sectionb/004-createrole.png)  
+ Chọn **"AWS service"**, sau đó chọn **"EC2"**, và nhấp **"Next"**.  
![Dịch vụ AWS](/images/4.sectionb/005-awsservice.png)  
![Chọn dịch vụ EC2](/images/4.sectionb/006-ec2serviceselect.png)  
+ Tìm kiếm **"AmazonSSMManagedInstanceCore"**, chọn nó, và nhấp **"Next"**.  
![Role SSM](/images/4.sectionb/007-ssmrole.png)  
+ Đặt tên role là ```detectionServer-vpn-ssm-ec2-instance-profile```, sau đó nhấp **"Create role"**.  
![Tên của role](/images/4.sectionb/008-rolename.png)  
![Xác nhận tạo role](/images/4.sectionb/009-createrolesubmit.png)

  {{% notice note%}}  
  Chúng ta đã tạo security group và IAM role cho máy ảo EC2 thành công.  
  {{% /notice %}}