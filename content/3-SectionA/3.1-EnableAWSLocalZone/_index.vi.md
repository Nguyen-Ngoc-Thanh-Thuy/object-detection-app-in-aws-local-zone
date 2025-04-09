---
title : "Kích hoạt AWS Local Zone"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 3.1. </b> "
---

**1. Truy cập dịch vụ VPC trên AWS Console**
  + Mở AWS Management Console..
  + Trong thanh tìm kiếm, nhập **"VPC"** và chọn dịch vụ **VPC** từ kết quả hiển thị.
![Đi đến dịch vụ VPC](/images/3.sectiona/000-gotovpc.png)

**2. Điều hướng đến cài đặt AWS Local Zone**
  + Cuộn xuống cuối trang dịch vụ VPC.
  + Nhấp vào **"Settings"** để truy cập phần cài đặt AWS Local Zones.
![VPC Settings](/images/3.sectiona/001-vpcsettings.png)

**3. Chọn AWS Local Zone muốn bật và tiến hành Opt-in**
  + Chuyển đến **Zone tab**
  ![Zone Tab](/images/3.sectiona/002-zonetab.png)
  + Xác định AWS Local Zone được chỉ định cho workshop này **(us-west-2-lax-1)**
  + Nhấp vào nút **"Action"** và chọn **Opt-in**.
  ![Opt in Local Zone](/images/3.sectiona/003-optinlocalzone.png)
  
  {{% notice note %}}
  Lưu ý rằng quá trình này có thể mất khoảng 1-2 phút để hoàn tất.
  {{% /notice %}}

**4. Kích hoạt AWS Local Zone thành công**.
![Kích hoạt thành công](/images/3.sectiona/004-enablesuccessfully.png)


