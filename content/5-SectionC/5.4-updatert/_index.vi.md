---
title : "Cập nhật bảng định tuyến để định tuyến lưu lượng qua VPN"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 5.4 </b> "
---

**1. Truy cập bảng định tuyến**
   + Truy cập [dịch vụ VPC](https://console.aws.amazon.com/vpc/home) và chuyển đến phần **Route Tables**.
   + Tìm **bảng định tuyến của VPC "vpc-extended-to-aws-local-zone"**.
     ![Cập nhật bảng định tuyến](/images/5.sectionc/044-updatert.png)

**2. Chỉnh sửa các routes**
   + Nhấp vào **"Edit routes"** → Chọn **"Add route"**.
     ![Cập nhật bảng định tuyến](/images/5.sectionc/045-updatert.png)
     ![Cập nhật bảng định tuyến](/images/5.sectionc/046-updatert.png)

**3. Thêm route mới**
   + **Destination**: Nhập **172.16.0.0/24** (mạng on-premise).
   + **Target**: Chọn **localZone-vpn-instance** (máy ảo VPN cài đặt Openswan).
   + Nhấp vào **"Save changes"** để áp dụng route mới.
     ![Cập nhật bảng định tuyến](/images/5.sectionc/047-updatert.png)

  {{% notice note %}}
  Chúng ta đã cập nhật thành công bảng định tuyến, đảm bảo rằng lưu lượng truy cập hướng đến mạng on-premise sẽ được định tuyến qua máy ảo VPN.
  {{% /notice %}}
