---
title : "Yêu cầu tăng Quota vCPU"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

Trước khi triển khai workshop, chúng ta cần đảm bảo rằng tài nguyên cần thiết đã được cấp phát đầy đủ để tránh gián đoạn trong quá trình thực hành. Cụ thể, do object detection server sẽ chạy trên một máy ảo EC2 có loại **g4dn.2xlarge**, chúng ta cần yêu cầu quota cho 8 vCPU loại G tại Region us-west-2.

Máy ảo g4dn.2xlarge được trang bị GPU NVIDIA T4, phù hợp cho các tác vụ AI/ML và xử lý video thời gian thực. Tuy nhiên, do giới hạn mặc định của AWS, vCPU cho các loại instance G có thể chưa được cấp đủ trong tài khoản. Vì vậy, trước khi bắt đầu, hãy truy cập AWS Service Quotas, kiểm tra quota hiện tại và gửi request nâng cấp nếu cần.

{{% notice warning %}}
Việc chuẩn bị trước này giúp đảm bảo rằng khi khởi chạy máy ảo, chúng ta sẽ có đủ tài nguyên mà không gặp lỗi do hạn mức tài nguyên bị giới hạn. Nếu request tăng hạn mức chưa được phê duyệt, bạn có thể gặp lỗi "InstanceLimitation" khi tạo máy ảo, làm gián đoạn quá trình triển khai workshop.
{{% /notice %}}

1. Truy cập vào giao diện của **Service Quotas**
![Trang chủ Service Quotas.](/images/2.preparation/000-requestquota.png)

2. Trong bảng điều khiển **Service Quotas**, chọn **AWS services**
  + Tìm dịch vụ **Amazon Elastic Compute Cloud (Amazon EC2)**
  ![Chọn Amazon EC2 trong AWS Services.](/images/2.preparation/001-requestquota.png)

3. Chọn **Running On-Demand G and VT instances**. Sau đó, click vào button **Request increase a account level**
![Chọn Running On-Demand G and VT instances.](/images/2.preparation/002-requestquota.png)

4. Điền **"8"** vào ô **Increase quota value** và chọn **Request** để gửi đi yêu cầu.
![Nhập giá trị quota và gửi yêu cầu.](/images/2.preparation/003-requestquota.png)

5. **Yêu cầu tăng quota đã được phê duyệt**. Chúng ta có thể sử dụng các loại instance thuộc loại G trong region Uus-west-2 (Oregon) với giới hạn tối đa 8 vCPU.
![Quota tăng lên 8 vCPU thành công.](/images/2.preparation/004-requestquota.png)
![Quota tăng lên 8 vCPU thành công.](/images/2.preparation/005-requestquota.png)
