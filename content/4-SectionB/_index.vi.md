---
title : "Phần B - Triển khai instance đầu tiên trong Local Zone và kết nối đến ứng dụng"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

Phần này cung cấp hướng dẫn chi tiết về cách triển khai một máy ảo EC2 trong AWS Local Zone và khởi chạy một ứng dụng phát hiện đối tượng.

![Kiến trúc hệ thống](/images/architecture.png)

### Tổng quan các bước triển khai
Quy trình triển khai bao gồm bốn bước chính:
  - **Cấu hình Security Groups** – Thiết lập các quy tắc bảo mật để cho phép lưu lượng HTTP chỉ từ địa chỉ IP của chúng ta đến máy ảo phát hiện đối tượng.
  - **Khởi chạy máy ảo EC2** – Triển khai một máy ảo EC2 trong AWS Local Zone.
  - **Triển khai ứng dụng phát hiện đối tượng** – Cài đặt các thư viện cần thiết và triển khai ứng dụng phát hiện đối tượng trên máy ảo EC2 vừa tạo.
  - **Kiểm tra kết nối** – Kiểm tra khả năng truy cập đến ứng dụng bằng cách truy cập địa chỉ IP public của ứng dụng thông qua trình duyệt web.

### Nội dung
4.1. [Cấu hình Security Groups và IAM Role](4.1-createsgandrole/) \
4.2. [Chạy máy ảo EC2 trong AWS Local Zone](4.2-launchec2/) \
4.3. [Triển khai ứng dụng phát hiện đối tượng](4.3-deployapplication/) \
4.4. [Kiểm tra kết nối tới ứng dụng](4.4-testapplication)