---
title : "Session Management"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
---
# Triển khai ứng dụng phát hiện đối tượng trên AWS Local Zone với độ trễ thấp cho video streaming qua Site-to-Site VPN sử dụng OpenSwan.

### Tổng quan

Workshop sẽ triển khai và cấu hình hệ thống stream video từ môi trường on-premises mô phỏng đến ứng dụng nhận diện đối tượng có độ trễ thấp trong AWS Local Zones thông qua kết nối VPN Site-to-Site (S2S) sử dụng OpenSwan. 

Chúng ta sẽ thực hành các bước từ thiết lập tài nguyên mạng trên AWS, mở rộng VPC đến AWS Local Zone, triển khai kết nối VPN, stream video theo thời gian thực và chạy ứng dụng nhận diện đối tượng tại vùng mạng biên.

Workshop giúp chúng ta hiểu rõ cách tận dụng AWS Local Zones để giảm độ trễ trong các ứng dụng nhạy cảm với thời gian thực, đồng thời tối ưu hóa kết nối giữa môi trường on-premises và AWS.

![Kiến trúc hệ thống](/images/architecture.png) 

### Nội dung

 1. [Giới thiệu](1-introduce/)
 2. [Các bước chuẩn bị](2-preparation/)
 3. [Phần A - Kích hoạt AWS Local Zone và mở rộng VPC sang AWS Local Zone](3-sectiona/)
 4. [Phần B - Triển khai máy ảo đầu tiên trong AWS Local Zone và kết nối đến ứng dụng](4-sectionb/)
 5. [Phần C - Triển khai kết nối VPN giữa pn-premise và AWS Local Zone](5-sectionc/)
 6. [Phần D - Kiểm tra hoạt động của ứng dụng](6-partd/)
 7. [Dọn dẹp tài nguyên](7-cleanup/)
