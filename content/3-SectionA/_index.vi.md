---
title : "Phần A - Kích hoạt AWS Local Zone và mở rộng VPC"
date :  "`r Sys.Date()`" 
weight : 3 
chapter : false
pre : " <b> 3. </b> "
---

Phần này cung cấp hướng dẫn triển khai hạ tầng trong AWS Local Zone, tập trung vào việc mở rộng VPC vào AWS Local Zone.

![Kiến trúc hệ thống](/images/architecture.png)

### Tổng quan các bước triển khai
Phần này bao gồm bốn bước chính:
- Sử dụng vùng AWS us-west-2 làm Region chính.
- Đăng ký AWS Local Zone us-west-2-lax-1.
- Tạo và mở rộng VPC vào AWS Local Zone.
- Tạo public subnet trong AWS Local Zone.

### Nội dung
3.1. [Kích hoạt AWS Local Zone](3.1-enableawslocalzone/) \
3.2. [Mở rộng VPC vào AWS Local Zone](3.2-extendvpctolocalzone/) \
3.3. [Cấu hình public subnet trong AWS Local Zone](3.3-createlocalzonesubnet/)