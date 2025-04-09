---
title : "Kiểm tra hoạt động của ứng dụng phát hiện đối tượng"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 5.1 </b> "
---

1. **Khởi động ứng dụng streaming video**
   + Truy cập [dịch vụ EC2](https://console.aws.amazon.com/ec2/v2/home).

   + Kết nối với **máy ảo videoStreamer** bằng **AWS SSM**.
     ![Kết nối SSM](/images/6.sectiond/000-ssm.png)
     ![Kết nối SSM](/images/6.sectiond/001-ssm.png)

   + Chạy **ứng dụng streaming**.
     - Thực hiện lệnh sau trong giao diện dòng lệnh để khởi động server RTSP:
       ```
       sudo su ubuntu
       cd /home/ubuntu
       docker run --rm -it -e RTSP_PROTOCOLS=tcp -p 8554:8554 -p 1935:1935 -p 8888:8888 -p 8889:8889 aler9/rtsp-simple-server &
       ```
       ![Máy chủ Streaming](/images/6.sectiond/002-streaming.png)

     - Tải video mẫu:
       ```
       curl 'https://static.us-east-1.prod.workshops.aws/public/bdfac965-db9c-4fa3-9d89-af97e8cdf015/assets/src/videostreamer/street_day.mp4' --output street_day.mp4
       ```
       ![Máy chủ Streaming](/images/6.sectiond/003-streaming.png)

     - Bắt đầu truyền phát video qua RTSP:
       ```
       ffmpeg -re -stream_loop -1 -i street_day.mp4 -vcodec libx264 -preset ultrafast -tune zerolatency -pix_fmt yuv422p -f rtsp -rtsp_transport tcp rtsp://localhost:8554/mystream
       ```
       ![Máy chủ Streaming](/images/6.sectiond/004-streaming.png)
       ![Máy chủ Streaming](/images/6.sectiond/005-streaming.png)

2. **Khởi động ứng dụng phát hiện đối tượng**
   + Trên **EC2 Management Console**, kết nối với **máy ảo detectorServer** bằng **AWS SSM**.
     ![Kết nối SSM](/images/6.sectiond/006-ssm.png)

   + Thực hiện lệnh sau (thay **private IP videostreamer instance** bằng địa chỉ IP private của máy ảo streaming):
     ```
     sudo su ec2-user
     cd /home/ec2-user/yolov7
     python3 ObjectDetection.py -s rtsp://<private IP videostreamer instance>:8554/mystream --weights yolov7-tiny.pt --enable-detection
     ```
     ![Đang truyền phát](/images/6.sectiond/007-streaming.png)

3. **Kiểm tra kết quả trên trình duyệt web**
   + Mở trình duyệt web và truy cập **Public IPv4 DNS** của **detectorServer** để xem kết quả phát hiện vật thể theo thời gian thực.
     ![Kiểm tra](/images/6.sectiond/008-test.png)
     ![Kiểm tra](/images/6.sectiond/009-test.gif)
     ![Kiểm tra](/images/6.sectiond/010-test.png)




