---
title : "Chạy máy ảo EC2 trong AWS Local Zone"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

**1. Mở dịch vụ EC2.**
+ Truy cập [dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home).

**2. Khởi chạy máy ảo mới.**  
+ Nhấp vào **"Launch instance"**.  
![Nút Launch Instance](/images/4.sectionb/010-launchinstancebutton.png)  
+ Tên máy ảo: Nhập ```detectorServer```.  
![Đặt tên cho máy ảo](/images/4.sectionb/011-detectorservername.png)

**3. Chọn Amazon Machine Image (AMI).**:  
+ Chọn ```Ubuntu 22.04 - NICE DCV with NVIDIA TESLA GPU Driver```.  
![Duyệt AMIs](/images/4.sectionb/012-browseami.png)  
![Chọn AMI](/images/4.sectionb/013-selectami.png)  
![Đăng ký AMI](/images/4.sectionb/014-subscribeami.png)  
![Gửi AMI](/images/4.sectionb/015-submitami.png)

**4. Chọn Instance type.**  
+ Chọn **g4dn.2xlarge** (phù hợp với khối lượng công việc sử dụng GPU).  
![Chọn loại instance](/images/4.sectionb/016-instancetype.png)

**5. Cấu hình Key pair.**  
+ Chọn **"Proceed without a key pair"** (chúng ta sẽ sử dụng AWS Systems Manager để kết nối).  
![Tùy chọn không sử dụng key pair](/images/4.sectionb/017-withoutkeypair.png)

**6. Cấu hình Network settings.**  
+ Nhấp vào **"Edit"**.  
![Chỉnh sửa cài đặt mạng](/images/4.sectionb/018-editnetworksettings.png)  
+ **VPC**: Chọn **"vpc-extended-to-aws-local-zone"**.  
+ **Subnet**: Chọn **"my-subnet-in-aws-local-zone"**.  
+ **Bật Public IP** (để truy cập server qua Internet).  
+ **Security Group**: Chọn **"my-detectorServer-sg"** (được tạo ở Bước 1).  
![Cấu hình cài đặt mạng](/images/4.sectionb/019-networksettings.png)

**7. Cấu hình Storage.**  
+ Đặt kích thước Root volume là **32 GiB**.  
![Cấu hình storage](/images/4.sectionb/020-storage.png)

**8. Gán IAM Role.**  
+ Trong **Advanced details**, tìm **IAM instance profile**.  
+ Chọn **"detectionServer-ec2-instance-profile"**.  
![Chọn IAM Profile](/images/4.sectionb/021-advanceddetails.png)

**9. Khởi chạy máy ảo.**  
+ Nhấp vào **"Launch instance"**.  
![Khởi chạy máy ảo](/images/4.sectionb/022-launchinstance.png)

{{% notice warning%}}  
Quá trình đăng ký AMI có thể mất chút ít thời gian. Giữ trình duyệt mở để đảm bảo máy ảo EC2 được khởi chạy. Khi đăng ký hoàn tất, máy ảo sẽ tự động được khởi chạy.  
{{% /notice %}}  
![Cảnh báo đăng ký](/images/4.sectionb/023-subscriptionwarning.png)

{{% notice note%}}  
Máy ảo EC2 đã được triển khai trong AWS Local Zone.  
{{% /notice %}}  
![Khởi chạy thành công instance](/images/4.sectionb/024-launchsuccessfully.png)
