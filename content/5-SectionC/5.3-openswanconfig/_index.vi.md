---
title : "Cài đặt và cấu hình Openswan VPN trong AWS Local Zone"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

**1. Truy cập máy ảo EC2**
   + Truy cập [EC2 service management console](https://console.aws.amazon.com/ec2/v2/home).
   + Chọn **'LocalZone-vpn-instance'** đã tạo ở bước 1 của phần C - Tạo máy ảo VPN trong AWS Local Zone.
     ![EC2 Security Group](/images/5.sectionc/025-ec2security.png)
   + Cập nhật security group:
     - Chọn security group **my-vpnlocalzone-sg**.
       ![Security Group](/images/5.sectionc/026-sg.png)
     - Chọn **"Edit inbound rules"**.
       ![Security Group](/images/5.sectionc/027-sg.png)
     - **Sửa đổi inbound rules:** Mở các cổng TCP 4500 và 500 cho địa chỉ IP public được tìm thấy trong file cấu hình Openswan. Xóa "0.0.0.0/0" trong inbound rules, thay vào đó bằng địa chỉ IP public từ file cấu hình Openswan.
       ![VPN configuration file](/images/5.sectionc/024-configfile.png)
       ![Edit inbound rules](/images/5.sectionc/028-inboundrule.png)
   + Kết nối đến VPN instance bằng **AWS SSM**.
     ![SSM Connect](/images/5.sectionc/029-ssmconnect.png)
     ![SSM Connect](/images/5.sectionc/030-ssmconnect.png)

**2. Cài đặt Openswan**
```
/bin/bash 
sudo su yum 
install openswan -y
```
![Openswan](/images/5.sectionc/031-openswan.png)

**3. Cấu hình Openswan**
+ Chỉnh sửa file **sysctl.conf**.
  ```
  vi /etc/sysctl.conf
  ```
  ![Openswan](/images/5.sectionc/032-openswan.png)
+ Thêm các dòng sau vào file.
  ```
  net.ipv4.ip_forward = 1
  net.ipv4.conf.default.rp_filter = 0
  net.ipv4.conf.default.accept_source_route = 0
  ```
  ![Openswan](/images/5.sectionc/033-openswan.png)

+ Chạy lệnh sau.
  ```
  sysctl -p
  ```
  ![Openswan](/images/5.sectionc/034-openswan.png)

**4. Cấu hình IPSec**
+ Chỉnh sửa file **/etc/ipsec.conf**:
  ```
  vi /etc/ipsec.conf
  ```
  ![Openswan](/images/5.sectionc/035-openswan.png)

+ Đảm bảo dòng **#include /etc/ipsec.d/*.conf** không bị chú thích (không có # ở đầu dòng).
  ![Openswan](/images/5.sectionc/036-openswan.png)

+ Mở file **/etc/ipsec.d/aws.conf**.
  ![Openswan](/images/5.sectionc/037-openswan.png)
+ Thay thế các giá trị mẫu bằng các giá trị thực tế từ file cấu hình Openswan:
  - Public IP of OpenSwan/CGW → Địa chỉ IP công khai của máy ảo VPN.
  - Public IP of VGW - Tunnel 1 → Địa chỉ IP public từ file cấu hình Openswan.
  - LOCAL NETWORK → CIDR của AWS Local Zone (`10.0.0.0/24`).
  - REMOTE NETWORK → CIDR của mạng on-premise (`172.16.0.0/24`).
    ```
    conn Tunnel1
      authby=secret
      auto=start
      left=%defaultroute
      leftid=<Địa chỉ IP công khai của OpenSwan/CGW>
      right=<Địa chỉ IP công khai của VGW - Tunnel 1>
      type=tunnel
      ikelifetime=8h
      keylife=1h
      phase2alg=aes128-sha1;modp1024
      ike=aes128-sha1;modp1024
      keyingtries=%forever
      keyexchange=ike
      leftsubnet=<MẠNG NỘI BỘ>
      rightsubnet=<MẠNG TỪ XA>
      dpddelay=10
      dpdtimeout=30
      dpdaction=restart_by_peer
    ```
    ![Openswan](/images/5.sectionc/038-openswan.png)

**5. Tạo file Secrets**
+ Sao chép **giá trị Pre-shared Key** từ file cấu hình Openswan.
  ![Openswan](/images/5.sectionc/039-openswan.png)

+ Tạo file **/etc/ipsec.d/aws.secrets**.
  ```
  vi /etc/ipsec.d/aws.secrets
  ```
  ![Openswan](/images/5.sectionc/040-openswan.png)

+ Dán giá trị **pre-shared-key** vào.
  ```
  Customer-GW-IP  Virtual Private Gateway-IP:  PSK  "<Giá trị Pre-Shared-key>"
  ```
  ![Openswan](/images/5.sectionc/041-openswan.png)

**6. Khởi động dịch vụ Openswan VPN**
+ Chạy các lệnh sau để khởi động dịch vụ Openswan và kiểm tra trạng thái.
  ```
  systemctl start ipsec
  systemctl status ipsec
  ```
  ![Openswan](/images/5.sectionc/042-openswan.png)

**7. Xác minh kết nối VPN**
+ Truy cập **dịch vụ VPC**. Trong thanh điều hướng bên trái, chọn **Site-to-Site VPN connections**.
+ Chọn kết nối **"vpn-OnPremise-LocalZone"** và đảm bảo trạng thái đang là **"Up"** (có thể mất đến 5 phút).
  ![Openswan](/images/5.sectionc/043-openswan.png)

{{%notice info%}}
Trong workshop này, chỉ có 1 tunnel ở trạng thái **"Up"**.
{{% /notice %}}

