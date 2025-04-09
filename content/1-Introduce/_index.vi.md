---
title : "Giới thiệu"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---
### VẤN ĐỀ

Trước khi **AWS Local Zones** ra đời, các ứng dụng cần độ trễ thấp gặp phải nhiều thách thức do khoảng cách địa lý giữa người dùng cuối và các Regions chính của AWS.

**1. Độ trễ cao do khoảng cách xa với Region chính**
- Trước đây, các ứng dụng thường được triển khai tại một Region trung tâm, trong khi người dùng có thể ở rất xa khu vực đó.
- Khi dữ liệu phải di chuyển một quãng đường dài từ AWS Region đến thiết bị của người dùng, độ trễ cao có thể ảnh hưởng tiêu cực đến trải nghiệm người dùng, đặc biệt là trong các ứng dụng:
    + Trò chơi trực tuyến và livestream
    + Ứng dụng thực tế ảo (AR/VR)
    + Hệ thống giao dịch tài chính theo thời gian thực
    + Ứng dụng AI/ML cần xử lý dữ liệu nhanh từ cảm biến/thết bị IoT

**2. Hệ thống on-premise có độ trễ thấp nhưng thiếu khả năng mở rộng**
- Trước khi có AWS Local Zones, nhiều doanh nghiệp phải chạy ứng dụng trên hệ thống on-premise với trung tâm dữ liệu riêng gần người dùng để đảm bảo độ trễ thấp. 
- Tuy nhiên, hệ thống on-premise có một số hạn chế:
    + Chi phí đầu tư hạ tầng cao.
    + Không linh hoạt và khó mở rộng như AWS.

### GIẢI PHÁP

Để giải quyết vấn đề độ trễ do khoảng cách địa lý, **AWS đã giới thiệu AWS Local Zones** – một phần mở rộng của AWS Region, cung cấp tài nguyên tính toán, lưu trữ và dịch vụ mạng gần hơn với người dùng cuối tại các khu vực đô thị.

#### AWS Local Zones là gì?
- AWS Local Zones là phần mở rộng của AWS Region, cung cấp dịch vụ tính toán, lưu trữ và dịch vụ mạng ngay tại các vị trí địa lý cụ thể, giúp người dùng có thể truy cập ứng dụng với độ trễ cực thấp.
- AWS Local Zones kết nối với Region gốc thông qua mạng riêng có băng thông của AWS, giúp ứng dụng chạy trong LAWS Local Zones có thể truy cập nhanh, an toàn vào các dịch vụ AWS khác.

#### Lợi ích chính của AWS Local Zones:
- **Giảm độ trễ**
    + Đặt workload gần người dùng giúp giảm thời gian truyền dữ liệu.
    + Phù hợp với các ứng dụng thời gian thực như game, phát trực tuyến, suy luận máy học và AR/VR.
- **Tích hợp hybrid giữa cloud & on-premise**
    + AWS Local Zones hỗ trợ AWS Direct Connect và AWS VPN, giúp tích hợp dễ dàng với hệ thống on-premise.

#### Khi nào nên sử dụng AWS Local Zones?
- Nếu ứng dụng yêu cầu độ trễ thấp, AWS Local Zones là giải pháp lý tưởng. AWS Local Zones có kết nối Internet riêng và hỗ trợ AWS Direct Connect, giúp tài nguyên trong Local Zone phục vụ người dùng local với tốc độ cao.

### KIẾN TRÚC

![Kiến trúc hệ thống](/images/architecture.png) 

##### Môi trường đám mây trên AWS (us-west-2: Oregon)
- **VPC 10.0.0.0/24**: Lưu trữ tài nguyên AWS trong Region us-west-2.
- **Public Subnet (10.0.0.0/25)**: Gồm các thành phần chính:
    + **Detection Server**: Máy chủ thực hiện nhiệm vụ phát hiện đối tượng.
    + **Máy ảo VPN (OpenSwan)**: Máy chủ đóng vai trò là Customer Gateway, thiết lập kết nối VPN với môi trường on-premise mô phỏng.
- **Internet Gateway**: Cung cấp truy cập Internet cho tài nguyên trong AWS Cloud.
- **AWS Systems Manager**: Quản lý hệ thống và cho phép truy cập từ xa vào máy ảo EC2 mà không cần SSH/RDP trực tiếp.

##### Môi trường on-premise mô phỏng (us-east-1: N. Virginia)
- **VPC 172.16.0.0/24:** Mô phỏng mạng on-premise bằng một VPC ở us-east-1.
- **Private Subnet (172.16.0.0/25):**
    + **Streaming Server:**: Xử lý việc truyền phát dữ liệu/video từ môi trường on-premise.
- **Public Subnet (172.16.0.128/25):**
    + **NAT Gateway:** Giúp các máy ảo EC2 trong private subnet truy cập Internet mà không cần IP public.
- **Internet Gateway:** Cho phép truy cập Internet.

##### VPN Site-to-Site
- **VPN Gateway** (trong VPC on-premise) kết nối với máy ảo VPN (OpenSwan) trong AWS Cloud.
- VPN Instance hoạt động như **Customer Gateway** để thiết lập kết nối bảo mật với VPC on-premise.
- Kết nối VPN Site-to-Site giúp server trong AWS Local Zone giao tiếp an toàn với môi trường on-premise mô phỏng trong us-east-1 mà không cần qua Internet.


### QUÁ TRÌNH TRIỂN KHAI
- Trong workshop này, chúng ta sẽ triển khai một ứng dụng phát hiện đối tượng gần với vị trí on-premise hơn.
- Từ một vị trí on-premise mô phỏng, chúng ta sẽ sử dụng một máy ảo đã triển khai sẵn để truyền phát video đến AWS Local Zone gần nhất.
- Để tránh truyền video qua Internet một cách công khai, chúng ta sẽ triển khai máy ảo VPN trong AWS Local Zone để kết nối VPN với môi trường on-premise mô phỏng.
- Cuối cùng, chúng ta sẽ triển khai và cài đặt ứng dụng phát hiện đối tượng trong Local Zone đã được chọn để nhận diện người và vật thể trong streaming video.
- Workshop sẽ hướng dẫn từng bước quá trình:
    + Sử dụng AWS Console để thực hiện workshop.
    + Kích hoạt AWS Local Zone.
    + Tạo và mở rộng VPC sang AWS Local Zone.
    + Triển khai ứng dụng phát hiện đối tượng yêu cầu độ trễ thấp.
    + Triển khai máy ảo VPN trong Local Zone.
    + Sử dụng ứng dụng streaming video trong môi trường on-premise mô phỏng.
    + Bật tính năng phát hiện đối tượng và kiểm tra kết quả.

### CÁC PHẦN CHÍNH
- Workshop gồm 4 phần, tương ứng với kiến trúc đã đề cập:
    + **Phần A - Kích hoạt AWS Local Zone và mở rộng VPC:** Kích hoạt AWS Local Zone, tạo VPC và mở rộng nó bằng cách tạo public subnet trong Local Zone.
    + **Phần B - Triển khai máy ảo đầu tiên trong Local Zone và kết nối đến ứng dụng:** Triển khai máy ảo EC2 trong Local Zone và kiểm tra truy cập đến detection web server qua Internet.
    + **Phần C - Triển khai kết nối VPN giữa on-premise và Local Zone:** Sau khi ứng dụng phát hiện đối tượng được triển khai và chạy ở AWS Local Zone, chúng ta sẽ kết nối môi trường on-premise mô phỏng với AWS Local Zone qua VPN.
    + **Phần D - Kiểm tra hoạt động của ứng dụng:** Truyền video từ môi trường on-premise mô phỏng đến AWS Local Zone, nơi đang chạy ứng dụng phát hiện đối tượng.

### CÔNG NGHỆ SỬ DỤNG

#### Openswan
Openswan là một công cụ giúp bảo mật kết nối mạng bằng IPsec, một giao thức mã hóa lưu lượng Internet. Nó chạy trên Linux và hỗ trợ các tính năng bảo mật nâng cao như IKEv2, chứng chỉ X.509 và NAT traversal. Đây là một dự án mã nguồn mở, tiếp tục phát triển từ FreeS/WAN.

#### ffmpeg
FFmpeg là một công cụ đa phương tiện mạnh mẽ có thể phát, chuyển đổi, truyền phát và chỉnh sửa file âm thanh/video. Nó hỗ trợ hầu hết các định dạng, từ cũ đến mới nhất, và có thể chạy trên nhiều hệ điều hành như Linux, Windows, MacOS. FFmpeg là phần mềm mã nguồn mở, nhưng một số thành phần có giấy phép chặt chẽ hơn.

#### rtsp-simple-server
rtsp-simple-server là một máy chủ RTSP nhẹ, dễ sử dụng, giúp xử lý truyền phát video và âm thanh trực tuyến. Nó có thể hoạt động như một server hoặc proxy để gửi và nhận luồng RTSP. Công cụ này không yêu cầu phụ thuộc bổ sung và là phần mềm mã nguồn mở.