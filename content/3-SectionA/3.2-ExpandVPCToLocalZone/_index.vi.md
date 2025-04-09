---
title : "Mở rộng VPC sang AWS Local Zone"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 3.2. </b> "
---

**1. Tạo một VPC mới**  
+ Truy cập [dịch vụ VPC](https://console.aws.amazon.com/vpc/home)  
+ Nhấp vào **"Create VPC"**.  
![Nút Create VPC](/images/3.sectiona/005-createvpc.png)  
+ Chọn **"VPC Only"**, sau đó nhập tên VPC  
```vpc-extended-to-aws-local-zone```  
+ Đặt khối IPv4 CIDR  
```10.0.0.0/24```  
![Cấu hình VPC](/images/3.sectiona/006-vpcconfig.png)  
+ Nhấp vào **"Create VPC"** để hoàn tất.  
![Xác nhận tạo VPC](/images/3.sectiona/007-createvpcsubmit.png)  

**2. Tạo một Subnet trong AWS Local Zone**  
+ Ở bảng điều khiển bên trái, chọn **"Subnets"**, sau đó nhấp vào **"Create subnet"**.  
![Nút Create Subnet](/images/3.sectiona/008-createsubnet.png)  
+ Chọn VPC **vpc-extended-to-aws-local-zone** mới tạo.  
![Chọn VPC cho Subnet](/images/3.sectiona/009-subnetinvpc.png)  
+ Nhập tên subnet  
```my-subnet-in-aws-local-zone```  
+ Chọn AWS Local Zone **us-west-2-lax-1a** trong trường **Availability Zone**.  
+ Xác định khối CIDR  
```10.0.0.0/25```  
![Cấu hình Subnet](/images/3.sectiona/010-subnetconfig.png)  
+ Nhấp vào **"Create subnet"**.  
![Xác nhận tạo Subnet](/images/3.sectiona/011-createsubnetsubmit.png)  

**3. Bật DNS Hostnames cho VPC**  
+ Truy cập mục **"Your VPCs"**.  
+ Chọn VPC **vpc-extended-to-aws-local-zone**.  
+ Nhấp vào nút **Action**, sau đó chọn **"Edit VPC settings"**.  
![Chỉnh sửa cài đặt VPC](/images/3.sectiona/012-editvpc.png)  
+ Bật **"DNS hostnames"** để tự động gán tên DNS cho các máy ảo EC2 và nhấp **"Save changes"**.  
![Bật DNS hostnames](/images/3.sectiona/013-enabledns.png)  

{{% notice note %}}  
Chúng ta vừa mở rộng VPC đến AWS Local Zone.  
{{% /notice %}}
