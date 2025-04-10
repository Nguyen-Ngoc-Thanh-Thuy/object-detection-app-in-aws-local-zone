---
title : "Cấu hình VPN on-premises sử dụng kết nối site-to-site (S2S) VPN"
date :  "`r Sys.Date()`" 
weight : 2 
chapter : false
pre : " <b> 5.2 </b> "
---

Trong phần này, chúng ta sẽ mô phỏng môi trường on-premises bằng cách triển khai VPC trong khu vực **us-east-1** và sử dụng dịch vụ AWS Site-to-Site VPN.  

**1. Tải xuống file [streamingServer_over_vgw.json](https://nguyen-ngoc-thanh-thuy.github.io/object-detection-app-in-aws-local-zone/data/streamingServer_over_vgw.json).**  

{{% notice warning %}}  
Loại máy ảo **c5.2xlarge** không khả dụng trong Availability Zone **us-east-1e** của khu vực us-east-1, chỉ được hỗ trợ trong AZs **us-east-1a đến us-east-1d** và **us-east-1f**. Do đó, file JSON chỉ định rõ **us-east-1a** để triển khai private subnet nhằm đảm bảo tính tương thích khi tạo các máy ảo **c5.2xlarge** sau này.  
{{% /notice %}}  

![Lỗi Availability Zone](/images/5.sectionc/012-azerror.png)  
![Thay đổi Availability Zone](/images/5.sectionc/013-azchange.png)  

{{% notice note %}}  
File JSON được sử dụng để định nghĩa cơ sở hạ tầng trên AWS bằng CloudFormation. Nó bao gồm các tài nguyên cần thiết để thiết lập môi trường ảo:  
🔹 **On-premise VPC.**  
🔹 **Private subnet để triển khai máy ảo Streaming.**  
🔹 **Private Route Table**  
🔹 **Public Subnet cho Internet.**  
🔹 **Public Route Table.**  
🔹 **Internet Gateway.**  
🔹 **NAT Gateway.**  
🔹 **NAT Gateway EIP.**  
🔹 **On-premise VPN Gateway.**  
🔹 **Local Zone Gateway.**  
🔹 **VPN connection.**  
🔹 **Video streamer máy ảo.**  
...  
{{% /notice %}}  

**2. Tạo một stack trong AWS CloudFormation**  
+ Truy cập **AWS Console**, tìm kiếm **CloudFormation**, và chọn dịch vụ. Nhấp vào **"Create stack"** → **With new resources (standard)**.  
![CloudFormation](/images/5.sectionc/014-cloudformation.png)  
+ Chọn **Choose an existing template** → **"Upload a template file"** → Nhấp **"Choose file"** và tải lên **streamingServer_over_vgw.json**.  
![Stack](/images/5.sectionc/015-stack.png)  
+ Nhấp **"Next"**.  

**3. Cung cấp thông tin cần thiết cho triển khai**  
+ **Stack name**: Nhập tên ```streamingServer```.  
+ **Instance type**: Chọn **c5.2xlarge**.  
+ Cung cấp **địa chỉ IP riêng của máy ảo object detector**. Địa chỉ này sẽ được sử dụng trong security group của máy ảo streaming.  
+ Cung cấp **địa chỉ IP công khai của máy ảo VPN** trong AWS Local Zone (đã triển khai ở bước trước).  
+ Click **"Next"**.  
![Stack](/images/5.sectionc/017-stack.png)  
+ Trong trang **Review**, đánh dấu chọn **I acknowledge that AWS CloudFormation may create IAM resources with custom names**.  
![Stack](/images/5.sectionc/018-stack.png)  
+ Chọn **"Submit"** để bắt đầu triển khai môi trường on-premises mô phỏng.  

{{% notice info %}}  
VPN setup có thể mất **3-5 phút** để hoàn thành.  
{{% /notice %}}  
![Stack hoàn tất](/images/5.sectionc/019-stackcomplete.png)  

**4. Kiểm tra trạng thái VPN**  
+ Truy cập [dịch vụ VPC](https://console.aws.amazon.com/vpc/home).  
+ Trong bảng điều khiển bên trái, chọn **Site-to-Site VPN connections**.  
+ **Đảm bảo rằng:**  
    - Trạng thái **Tunnel** đang **"Down"** (đây là trạng thái mặc định trước khi thực hiện cấu hình thêm).  
    ![Kết nối VPN](/images/5.sectionc/020-vpnconnection.png)  
    - **Customer Gateway Address** khớp với **public IP của máy ảo localZone-vpn-instance**.  
    ![Kết nối VPN](/images/5.sectionc/021-vpnconnection.png)  

**5. Tải xuống file cấu hình VPN**  
+ Chọn kết nối **vpn-OnPremise-LocalZone"** và nhấp vào nút **"Download configuration"**.  
![File cấu hình VPN](/images/5.sectionc/022-configfile.png)  

+ Chọn **Generic**, sau đó nhấp **"Download"** để tải xuống **file cấu hình VPN**.  
![File cấu hình VPN](/images/5.sectionc/023-configfile.png)  

+ File sẽ có dạng như sau:  
![File cấu hình VPN](/images/5.sectionc/024-configfile.png)  

{{% notice note %}}  
📌 **Lưu ý quan trọng**  
🔹 "Left IP" phải là **Public IP của máy ảo localZone-vpn-instance** (Customer Gateway).  
🔹 "Right IP" phải là **Public IP của VPN gateway trên môi trường on-premise mô phỏng** (Virtual Private Gateway).  
{{% /notice %}}  

Sau khi tải xuống file cấu hình này, chúng ta sẽ áp dụng nó vào máy ảo ```localZone-vpn-instance``` trong bước tiếp theo.
