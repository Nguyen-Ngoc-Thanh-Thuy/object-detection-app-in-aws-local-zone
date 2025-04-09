---
title : "Cấu hình public subnet trong AWS Local Zone"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3.3. </b> "
---
**1. Tạo một Internet Gateway (IGW)**  
+ Mở **VPC Console** và chọn **"Internet gateways"** từ bảng điều khiển bên trái. Nhấp vào **"Create internet gateway"**.  
![Nút Create IGW](/images/3.sectiona/014-createigw.png)  
+ Nhập tên ```igw-aws-local-zone```. Nhấp vào **"Create internet gateway"**.  
![Tạo IGW](/images/3.sectiona/015-createigw.png)

**2. Attach VPC**  
+ Trong phần **Internet gateways**, chọn IGW **igw-aws-local-zone** vừa tạo.  
+ Nhấp vào **"Actions"** → **"Attach to VPC"**.  
![IGW gắn vào VPC](/images/3.sectiona/016-igwattachvpc.png)  
+ Chọn VPC **vpc-extended-to-aws-local-zone**. Nhấp vào **"Attach internet gateway"**.  
![VPC đã gắn](/images/3.sectiona/017-vpcattached.png)

**3. Cập nhật Bảng định tuyến để sử dụng Internet Gateway**  
+ Trong **VPC Console**, truy cập **"Route tables"** từ bảng điều khiển bên trái.  
+ Chọn Bảng định tuyến liên kết với VPC **vpc-extended-to-aws-local-zone**.  
+ Nhấp vào **"Routes"** → **"Edit routes"**.  
![Chỉnh sửa route trong Route Table](/images/3.sectiona/018-editroutes.png)  
+ Nhấp vào **"Add Route"**.  
![Nút Add routes](/images/3.sectiona/019-addroutebutton.png)  
+ Trong mục **Destination**, nhập ```0.0.0.0/0``` (tất cả lưu lượng Internet).  
+ Trong mục **Target**, chọn **"Internet Gateway"**, sau đó chọn IGW **igw-aws-local-zone** vừa tạo.  
+ Nhấp vào **"Save changes"**.  
![Thêm route đến IGW](/images/3.sectiona/020-routetoigw.png)

{{% notice note %}}  
Subnet của AWS Local Zone giờ đã là một public subnet, có nghĩa là các máy ảo trong đó có thể truy cập Internet.  
{{% /notice %}}
