---
title : "Tạo máy ảo VPN trong AWS Local Zone"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

1. Truy cập [dịch vụ VPC](https://console.aws.amazon.com/vpc/home). 

2. Khởi chạy máy ảo và đặt tên: ```localZone-vpn-instance```.  
![Khởi chạy VPN instance](/images/5.sectionc/000-vpninstance.png)  

3. Chọn AMI: **Amazon Linux 2 AMI (HVM) - Kernel 5.10, SSD Volume Type**.  
![Chọn AMI](/images/5.sectionc/001-ami.png)  

4. Chọn loại máy ảo: Sử dụng **c5.large**.  

{{% notice warning%}}  
Nếu bạn đang sử dụng một Local Zone khác với **us-west-2-lax-1**, hãy kiểm tra tính khả dụng của loại máy ảo **c5.large** trong AWS Local Zone đó.
{{% /notice %}}  

5. Chọn option **Proceed without a key pair**: Vì sẽ sử dụng AWS Systems Manager để quản lý thay vì SSH keys.  
![Loại máy ảo và Key Pair](/images/5.sectionc/002-typekp.png)  

6. Cấu hình **Network settings**.  
+ Chọn VPC **vpc-extended-to-aws-local-zone** và subnet **my-subnet-in-aws-local-zone**.  
+ **Bật "Auto-assign public IP"** để máy ảo có thể truy cập từ internet.  
![Cấu hình Network Settings](/images/5.sectionc/003-networksettings.png)  

7. Tạo **Security Group**: Cho phép **UDP ports 500 & 4500**, và **TCP port 8554** từ địa chỉ IP riêng của máy ảo chạy ứng dụng phát hiện đối tượng.  
![Tạo Security Group](/images/5.sectionc/004-sg.png)  
![Rule 1](/images/5.sectionc/005-rule1.png)  
![Rule 2, 3](/images/5.sectionc/006-rule23.png)  

8. Gán **IAM Profile**: Sử dụng **detectionServer-vpn-ssm-ec2-instance-profile** cho AWS SSM.  
![IAM Profile](/images/5.sectionc/007-iamprofile.png)  

9. **Khởi chạy máy ảo**.  
![Khởi chạy instance](/images/5.sectionc/008-launchinstance.png)  

10. **Vô hiệu hóa Source/Destination Check** bằng cách chọn **Actions** → **Networking** → **Change source/destination check**.  
![Thay đổi Source/Destination Check](/images/5.sectionc/009-changesrcdescheck.png)  
![Dừng Source/Destination Check](/images/5.sectionc/010-stopsrcdescheck.png)  

11. Ghi chú lại **public IP của VPN instance** để sử dụng ở các bước sau.  
![Sao chép Public IP](/images/5.sectionc/011-copypublicip.png)  
