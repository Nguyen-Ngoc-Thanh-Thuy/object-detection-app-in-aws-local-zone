---
title : "Phần C - Triển khai kết nối VPN giữa On-Premise và Local Zone"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

Phần này cung cấp hướng dẫn chi tiết về cách thiết lập một kết nối VPN giữa môi trường on-premises và AWS Local Zone, đảm bảo môi trường on-premise có thể giao tiếp an toàn và hiệu quả với các dịch vụ AWS.

![Kiến trúc hệ thống](/images/architecture.png)

### Tổng quan các bước triển khai
Quá trình triển khai được chia thành bốn giai đoạn chính:
   - **Triển khai máy ảo VPN:**: Trong bước đầu tiên, chúng ta sẽ triển khai một máy ảo EC2 hoạt động như một VPN gateway trong AWS Local Zone. Máy ảo này sẽ cho phép giao tiếp an toàn giữa mạng on-premises và môi trường AWS.
   - **Cấu hình VPN trên môi trường on-premises mô phỏng:** Tiếp theo, chúng ta sẽ cấu hình một VPN trên môi trường on-premises. Cấu hình này sẽ đảm bảo rằng mạng on-premises và AWS Local Zone có thể giao tiếp liền mạch qua kết nối VPN.
   - **Cài đặt và cấu hình VPN trong AWS Local Zone sử dụng Openswan**: Bước thứ ba là cài đặt và cấu hình phần mềm VPN trên máy ảo EC2 trong AWS Local Zone, sử dụng Openswan, một giải pháp mã nguồn mở phổ biến cho VPN IPsec. Cấu hình này rất quan trọng để thiết lập một kết nối VPN an toàn giữa AWS Local Zone và mạng on-premises.
   - **Cập nhật bảng định tuyến VPC để định tuyến lưu lượng VPN**: Cuối cùng, chúng ta sẽ cập nhật bảng định tuyến VPC trong AWS Local Zone để định tuyến lưu lượng qua VPN, giúp các tài nguyên trên AWS có thể truy cập an toàn vào các hệ thống on-premises.

### Nội dung
5.1. [Tạo máy ảo VPN trong AWS Local Zone](5.1-vpninstance/) \
5.2. [Cấu hình VPN on-premises sử dụng kết nối Site-to-Site (S2S) VPN](5.2-s2svpn/) \
5.3. [Cài đặt và cấu hình VPN Openswan trong AWS Local Zone](5.3-openswanconfig/) \
5.4. [Cập nhật bảng định tuyến để định tuyến lưu lượng qua VPN](5.4-rtupdate)