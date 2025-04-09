---
title : "Kiểm tra kết nối tới ứng dụng"
date :  "`r Sys.Date()`" 
weight : 4 
chapter : false
pre : " <b> 4.4 </b> "
---

**1. Tìm public IPv4 DNS của máy ảo chạy ứng dụng phát hiện đối tượng**  
+ Truy cập [dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home)  
+ Chọn **máy ảo chạy ứng dụng phát hiện đối tượng**, sau đó sao chép **Public IPv4 DNS**.  
![Public IPv4 DNS](/images/4.sectionb/039-publicdns.png)

**2. Sao chép Public IPv4 DNS đó và mở trong trình duyệt web.**
Nếu thấy trên web hiển thị sơ đồ kiến trúc nghĩa là ứng dụng đã chạy thành công.
![Truy cập web](/images/4.sectionb/040-accessweb.png)

{{% notice info %}}  
Lưu ý rằng ở bước này, ta sẽ chỉ thấy sơ đồ kiến trúc ở phía bên trái của trang.  
{{% /notice %}}

