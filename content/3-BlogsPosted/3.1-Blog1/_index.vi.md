# CYBER SECURITY TRÊN AWS: KHÔNG CHỈ DÙNG WAF, HÃY TỰ ĐỘNG HÓA WAF

Khi triển khai **AWS WAF**, nhiều đội ngũ thường bắt đầu bằng việc tạo một vài rule để chặn **SQL Injection**, **Cross-Site Scripting (XSS)** hoặc giới hạn **request rate**.

Tuy nhiên, thách thức thực tế không nằm ở việc **bật WAF**, mà nằm ở việc **duy trì và cập nhật cơ chế bảo vệ** khi môi trường, ứng dụng và các kỹ thuật tấn công liên tục thay đổi.

Để giải quyết bài toán này, AWS cung cấp **Security Automations for AWS WAF** – một giải pháp giúp **tự động triển khai và vận hành nhiều lớp bảo vệ phổ biến**, thay vì phải cấu hình và quản lý từng rule theo cách thủ công.

---

# Những điểm nổi bật của giải pháp

## 1. AWS Managed Rules – Lớp bảo vệ nền tảng

Các **AWS Managed Rule Groups** giúp giảm đáng kể công sức xây dựng và bảo trì rule bằng cách tự động cập nhật các cơ chế bảo vệ trước:

- OWASP Top 10
- Bot traffic
- Lưu lượng độc hại phổ biến
- Các kỹ thuật tấn công web mới được AWS cập nhật

---

## 2. Chặn SQL Injection và XSS ngay từ tầng WAF

Giải pháp triển khai sẵn các rule kiểm tra:

- URI
- Query String
- Request Body

để phát hiện và ngăn chặn các mẫu tấn công web phổ biến như:

- SQL Injection (SQLi)
- Cross-Site Scripting (XSS)

---

## 3. HTTP Flood Protection

Hệ thống tự động phát hiện các địa chỉ IP gửi số lượng request bất thường nhằm giảm thiểu:

- Brute-force Attack
- HTTP Flood
- Layer 7 DDoS

---

## 4. Scanner & Probe Protection

Log từ các dịch vụ như:

- CloudFront
- Application Load Balancer (ALB)
- AWS WAF

được phân tích để phát hiện các IP có hành vi:

- Quét hệ thống (Scanning)
- Dò tìm endpoint
- Khai thác lỗ hổng

Các IP đáng ngờ có thể được **tự động đưa vào Block List**.

---

## 5. Bad Bot Detection

Giải pháp sử dụng:

- Honeypot
- Phân tích hành vi (Behavior Analysis)

để phát hiện bot độc hại và tự động cập nhật danh sách chặn trên AWS WAF.

---

## 6. Kết hợp Threat Intelligence

Hệ thống có khả năng cập nhật danh sách IP độc hại từ các **Threat Intelligence / Reputation Lists**, giúp ngăn chặn sớm các nguồn tấn công đã được nhận diện.

---

## 7. Tự động hóa bằng Lambda và Athena

Thay vì chỉ dựa trên các rule tĩnh, giải pháp tận dụng:

- AWS Lambda
- AWS Athena
- Log Parsing

để:

- Phân tích lưu lượng
- Phát hiện hành vi bất thường
- Tự động cập nhật cơ chế phòng thủ theo thời gian

Đây chính là điểm khác biệt lớn giữa một WAF truyền thống và một hệ thống phòng thủ có khả năng thích ứng.

---

# Kết luận

Điều mình thấy thú vị ở **Security Automations for AWS WAF** là giải pháp này cho thấy một tư duy quan trọng:

> **WAF không nên chỉ là tập hợp các rule được cấu hình một lần rồi để đó.**

Một kiến trúc WAF hiệu quả cần có khả năng:

- Quan sát lưu lượng (Traffic Monitoring)
- Phân tích log (Log Analysis)
- Học từ các dấu hiệu tấn công (Threat Detection)
- Tự động cập nhật cơ chế phòng thủ (Automated Protection)

Nói cách khác, WAF cần trở thành một thành phần **chủ động**, thay vì chỉ là một lớp lọc request thụ động.

---

# Kiến nghị

Ở bài blog tiếp theo, mình sẽ chia sẻ một giải pháp giúp giải quyết những điểm mà **AWS WAF** vẫn còn thiếu.

Mục tiêu không chỉ dừng lại ở việc **block request**, mà là xây dựng một **vòng lặp phát hiện và phản ứng liên tục (Continuous Detection & Response)** đối với các mối đe dọa ở tầng ứng dụng.

Theo quan điểm cá nhân, chủ đề này có thể tạo nhiều tương tác hơn bài viết về **Cyber Resilience**, bởi hiện nay rất nhiều doanh nghiệp đang sử dụng **ALB** hoặc **CloudFront**, nhưng chỉ dừng ở việc bật **AWS Managed Rules**, trong khi chưa khai thác hết giá trị của **Automation** và **Log-driven Protection** – vốn là trọng tâm của giải pháp này.

---

# Kiến trúc

![Architecture Diagram](/images/3-BlogsPosted/3.1-Blog1/ArchitectureBlog1.png)

---

# Tài liệu tham khảo

- AWS Security Automations for AWS WAF – Architecture Overview  
  https://docs.aws.amazon.com/solutions/latest/security-automations-for-aws-waf/architecture-overview.html

![Blog1](/images/3-BlogsPosted/3.1-Blog1/Blog1.png)