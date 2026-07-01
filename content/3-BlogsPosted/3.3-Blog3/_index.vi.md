---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# MINECRAFT CYBER SECURITY TRÊN AWS : KHÔNG CHỈ LÀ MỞ SECURITY GROUP, HÃY TỰ ĐỘNG HÓA PHẢN ỨNG SỰ CỐ (SOAR CHO GAME SERVER)

Khi triển khai các máy chủ dịch vụ như Minecraft Server trên AWS, nhiều đội ngũ thường bắt đầu bằng việc tạo một vài Security Group để mở cổng kết nối (như cổng TCP 25565) và giới hạn IP truy cập.

Tuy nhiên, thách thức thực tế không nằm ở việc bật server, mà nằm ở việc duy trì và bảo vệ hệ thống trước các cuộc tấn công DDoS Layer 3/4 hoặc các hành vi brute-force, dò quét cổng liên tục thay đổi từ hacker khi IP máy chủ bị lộ ra ngoài Internet.

Để giải quyết bài toán này, dự án của mình không chỉ dựa vào các lớp cấu hình tĩnh, mà ứng dụng giải pháp phản ứng sự cố tự động (SOAR) kết hợp bảo vệ đa tầng từ Edge Location đến tận Instance.

## NHỮNG ĐIỂM NỔI BẬT CỦA GIẢI PHÁP:

- Ẩn IP gốc và chống DDoS bằng AWS Global Accelerator & Shield: Game Minecraft chạy trên giao thức custom TCP Layer 4 nên không thể dùng AWS WAF bảo vệ. Giải pháp thay thế là cấp 2 IP Anycast tĩnh toàn cầu thông qua Global Accelerator được tích hợp AWS Shield Standard tại rìa mạng, giúp gánh và lọc bỏ hoàn toàn lưu lượng DDoS (SYN Flood, UDP Amplification) trước khi dẫn traffic sạch về qua Network Load Balancer (NLB). IP thật của EC2 được giấu kín hoàn toàn.

- Zero-Trust Management đóng hoàn toàn cổng SSH: Để loại bỏ triệt để nguy cơ chiếm quyền điều khiển, cổng SSH (Port 22) trên máy chủ EC2 được cấu hình đóng 100% ra Internet. Quản trị viên chỉ kết nối và thực thi lệnh thông qua kênh truyền mã hóa riêng biệt của AWS Systems Manager (SSM) Session Manager.

- Hệ thống phát hiện xâm nhập Amazon GuardDuty: Thay vì chỉ giám sát thủ công, GuardDuty chạy ngầm ở tầng AWS liên tục phân tích VPC Flow Logs từ máy chủ EC2 để nhận diện các hành vi bất thường, Port Scan hoặc các nỗ lực Brute-force từ hacker.

- Tự động hóa phản ứng bằng Lambda và EventBridge (SOAR Loop): Ngay khi GuardDuty phát hiện mối đe dọa, Amazon EventBridge lập tức bắt lấy sự kiện theo thời gian thực và kích hoạt AWS Lambda (Python). Hàm Lambda sẽ tự động trích xuất chính xác IP nguồn của kẻ tấn công.

- Khóa cửa ngõ mạng theo thời gian thực tại Network ACL: Thay vì cấu hình thủ công, Lambda thực thi lệnh ghi trực tiếp một rule DENY /32 đối với IP của hacker ngay tại tầng VPC Network ACL (Cửa ngõ Subnet). Kẻ tấn công bị cô lập hoàn toàn khỏi hệ thống chỉ sau vài giây.

- Cấu hình thông báo "Ting Ting" qua Amazon SNS: Đồng thời với lệnh chặn mạng, Lambda gọi dịch vụ Amazon SNS để gửi một Email cảnh báo đỏ khẩn cấp chứa đầy đủ thông tin (IP nguồn, loại tấn công, mức độ nghiêm trọng) trực tiếp về điện thoại của người quản trị để theo dõi trạng thái.

- Khôi phục thảm họa tự động với AWS Backup: Độc lập với luồng bảo mật mạng, AWS Backup Plan được thiết lập để tự động chụp ảnh snapshot ổ đĩa EBS mỗi giờ một lần (Hourly Backup) và lưu trữ mã hóa an toàn tại một Backup Vault biệt lập. Nếu xảy ra sự cố phá hoại dữ liệu (Griefing), hệ thống có khả năng phục hồi nguyên trạng với chỉ số mất mát dữ liệu (RPO) theo giờ tùy theo cấu hình.

## KẾT LUẬN:

Điều mình thấy thú vị là kiến trúc này cho thấy một hướng tiếp cận quan trọng trong bảo mật đám mây:

Bảo mật hệ thống không nên chỉ là một tập hợp các luật Security Group được cấu hình một lần rồi để đó.

Một kiến trúc an ninh hiệu quả cần có khả năng:

- Quan sát và giám sát liên tục (Continuous Monitoring)
- Phát hiện mối đe dọa theo thời gian thực (Real-time Detection)
- Tự động hóa phản ứng và cô lập nguồn tấn công (Automated Incident Response)
- Đảm bảo tính bền bỉ và khôi phục dữ liệu khi có thảm họa (Cyber Resilience)

## KIẾN NGHỊ:

Blog tiếp theo mình sẽ chia sẻ sâu hơn về phần tối ưu hóa chi phí (Cost Optimization) cho kiến trúc này, bởi vì việc duy trì AWS Global Accelerator và NLB chạy 24/7 có thể phát sinh chi phí cố định khá lớn đối với các dự án vừa và nhỏ. Việc tìm ra điểm cân bằng giữa bài toán kinh tế và mức độ an ninh bảo mật chính là trọng tâm tiếp theo.

Theo ý kiến cá nhân của mình, chủ đề này rất dễ tạo tương tác trong group vì nhiều bạn làm hệ thống/game server trên AWS vẫn có thói quen public IP trực tiếp của EC2 và mở Security Group khá thoáng, chưa khai thác mô hình tự động hóa hướng sự kiện (Event-driven Security) kết hợp Network ACL + Lambda để cô lập hacker tự động.

## KIẾN TRÚC:

![Architecture Diagram](/images/3-BlogsPosted/3.3-Blog3/ArchitectureBlog3.png)

## LINK TÀI LIỆU & BÀI BÁO LIÊN QUAN:

Report: https://docs.google.com/document/d/1gLwVqTCD2lwx72q6pu60ZA4vUM945DOM860uvY6uNTI/edit?usp=sharing

![Blog3](/images/3-BlogsPosted/3.3-Blog3/Blog3.png)