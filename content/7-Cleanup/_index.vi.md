+++
title = "Dọn dẹp tài nguyên  "
date = 2021
weight = 7
chapter = false
pre = "<b>7. </b>"
+++

Để hủy các tài nguyên đã tạo trong quá trình làm workshop, có thể thực hiện theo các bước sau trong AWS Management Console:

### Truy cập CloudFormation
- Trong thanh tìm kiếm của AWS Management Console, nhập **"CloudFormation"** và chọn **"Stack"** → **"streamingServer"**.
- Nhấp chọn **Delete**.
![Xóa stack](/images/7.cleanup/000-stack.png)
![Xóa stack](/images/7.cleanup/001-stack.png)


### Xóa các tài nguyên trong AWS Local Zones
- Trước khi opt-out AWS Local Zone, chúng ta cần xóa tất cả các tài nguyên đã sử dụng tại đó:
+ Máy ảo VPN: ```localZone-vpn-instance```
+ Máy ảo Object Detector: ```detectorServer```
+ Security Groups: ```my-detectorServer-sg```, ```my-detectorServer-sg```
+ Internet Gateway (IGW): ```igw-aws-local-zone```
+ Public subnet: ```my-subnet-in-aws-local-zone```
+ VPC mở rộng đến AWS Local Zone: ```vpc-extended-tp-aws-local-zone```
+ Role: ```detectionServer-vpn-ssm-ec2-instance-profile```

- Trong thanh tìm kiếm của AWS Management Console, nhập **EC2** và chọn **dịch vụ EC2**.
- Tìm và chọn các instance: **localZone-vpn-instance** và **detectorServer**.​
- Click vào **Terminate instance**.
![Xóa instances](/images/7.cleanup/002-instance.png)
![Xóa instances](/images/7.cleanup/003-instance.png)


- Trong thanh tìm kiếm của AWS Management Console, nhập **VPC** và chọn **dịch vụ VPC**.
- Chọn VPC: **vpc-extended-tp-aws-local-zone** và nhấp vào **"Delete VPC"**.
![Xóa vpc](/images/7.cleanup/004-vpc.png)
![Xóa vpc](/images/7.cleanup/005-vpc.png)

- Trong thanh tìm kiếm của AWS Management Console, nhập **IAM** và chọn **dịch vụ IAM**.
- Trong thanh điều hướng bên trái, chọn **"Roles"**. Tìm kiếm và chọn role **detectionServer-vpn-ssm-ec2-instance-profile**.
![Xóa IAM role](/images/7.cleanup/006-iam.png)
![Xóa IAM role](/images/7.cleanup/007-iam.png)