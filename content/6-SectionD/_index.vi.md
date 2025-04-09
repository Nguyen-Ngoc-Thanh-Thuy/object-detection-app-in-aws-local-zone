---
title : "Phần D - Kiểm tra hoạt động của ứng dụng"
date :  "`r Sys.Date()`" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

Trong phần này, chúng ta sẽ xác minh tính năng của hệ thống bằng cách phát trực tuyến video từ môi trường on-premises và chạy ứng dụng phát hiện đối tượng trong AWS Local Zone.

![Kiến trúc hệ thống](/images/architecture.png)

### Tổng quan quá trình kiểm tra
- Quá trình kiểm tra bao gồm bốn bước chính:
  + **Chạy ứng dụng streaming video** – Khởi động dịch vụ phát video từ hệ thống on-premises để thiết lập luồng dữ liệu thời gian thực.
  + **Chạy ứng dụng phát hiện đối tượng** – Kích hoạt mô hình AI phát hiện đối tượng trong AWS Local Zone để xử lý luồng video đầu vào.
  + **Truy cập web để kiểm tra** – Mở trình duyệt web và điều hướng đến giao diện ứng dụng để quan sát và xác minh kết quả phát hiện đối tượng theo thời gian thực.

### Nội dung
6.1. [Kiểm tra hoạt động của ứng dụng phát hiện đối tượng](6.1-testapp/)
