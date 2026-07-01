# Đề xuất dự án
## Hệ thống bảo mật máy chủ Minecraft trên AWS
### Phát hiện xâm nhập và tự động ứng phó bằng các dịch vụ AWS

---

# 1. Tóm tắt dự án (Executive Summary)

Dự án **Hệ thống bảo mật máy chủ Minecraft trên AWS** được xây dựng nhằm chứng minh khả năng ứng dụng các dịch vụ bảo mật của Amazon Web Services (AWS) để triển khai một máy chủ trò chơi an toàn, có khả năng phát hiện các hành vi tấn công và tự động thực hiện các biện pháp ứng phó.

Không chỉ dừng lại ở việc triển khai một Minecraft Server thông thường trên Amazon EC2, hệ thống còn tích hợp nhiều lớp bảo mật nhằm giảm thiểu rủi ro trước các hình thức tấn công phổ biến như dò quét cổng (Port Scanning), Brute Force SSH, DDoS, truy cập trái phép và mất dữ liệu.

Kiến trúc của hệ thống được xây dựng theo hướng **Cloud-native Security** và **Security Automation**, kết hợp các dịch vụ như Amazon GuardDuty, Amazon EventBridge, AWS Lambda, AWS Backup, Amazon SNS, AWS Systems Manager Session Manager và AWS Global Accelerator để hình thành một mô hình SOAR (Security Orchestration, Automation and Response) thu nhỏ.

Ngoài mục tiêu đảm bảo an toàn cho máy chủ Minecraft, dự án còn đóng vai trò như một mô hình thực hành giúp sinh viên và kỹ sư Cloud tiếp cận các dịch vụ bảo mật của AWS trong môi trường thực tế.

---

# 2. Bài toán đặt ra (Problem Statement)

## Thực trạng

Các máy chủ Minecraft công khai thường xuyên trở thành mục tiêu của nhiều hình thức tấn công như:

- Dò quét cổng (Port Scanning).
- Brute Force vào cổng SSH.
- Tấn công từ chối dịch vụ (DDoS).
- Khai thác lỗ hổng để làm sập máy chủ.
- Phá hoại dữ liệu thế giới (World Data).
- Truy cập trái phép vào hệ thống quản trị.

Bên cạnh đó, nhiều quản trị viên vẫn sử dụng phương pháp quản trị truyền thống thông qua SSH và Key Pair, làm gia tăng nguy cơ rò rỉ thông tin truy cập.

Nếu không có cơ chế phát hiện và phản ứng tự động, các cuộc tấn công có thể gây gián đoạn dịch vụ, mất dữ liệu và ảnh hưởng đến trải nghiệm của người chơi.

## Giải pháp đề xuất

Dự án đề xuất triển khai một kiến trúc bảo mật nhiều lớp trên nền tảng AWS với các đặc điểm:

- Máy chủ Minecraft được triển khai trên Amazon EC2.
- Không mở cổng SSH ra Internet, thay vào đó sử dụng AWS Systems Manager Session Manager để quản trị.
- Amazon GuardDuty giám sát liên tục các hoạt động bất thường.
- Amazon EventBridge tự động chuyển các sự kiện bảo mật.
- AWS Lambda thực hiện phản ứng tự động bằng cách cập nhật Security Group để chặn IP độc hại.
- Amazon SNS gửi thông báo ngay lập tức cho quản trị viên.
- AWS Backup sao lưu dữ liệu định kỳ nhằm hỗ trợ khôi phục sau sự cố.
- AWS Global Accelerator kết hợp Network Load Balancer giúp che giấu địa chỉ IP thực của máy chủ và tăng khả năng chống DDoS.

---

# 3. Mục tiêu dự án

## Mục tiêu chính

- Triển khai máy chủ Minecraft an toàn trên AWS.
- Xây dựng hệ thống phát hiện và phản ứng trước các mối đe dọa.
- Tự động hóa quy trình xử lý sự cố bảo mật.
- Bảo vệ dữ liệu và giảm thiểu thời gian gián đoạn dịch vụ.

## Mục tiêu phụ

- Thực hành các dịch vụ bảo mật của AWS.
- Minh họa mô hình SOAR trên quy mô nhỏ.
- Nâng cao kỹ năng triển khai hạ tầng Cloud theo kiến trúc Zero Trust.
- Xây dựng mô hình có khả năng mở rộng và tái sử dụng cho các dự án tương lai.

---

# 4. Kiến trúc giải pháp (Solution Architecture)

Kiến trúc hệ thống được xây dựng theo mô hình nhiều lớp nhằm đảm bảo tính bảo mật, khả năng mở rộng và tự động hóa.

![Architecture](/images/2-Proposal/Architecture.png)

Luồng hoạt động của hệ thống:

```
Sơ đồ được chia thành 3 phân khu luồng chức năng rõ ràng:

1. LUỒNG TRUY CẬP & GIẢM THIỂU DDOS (TRAFFIC ROUTING & DDOS MITIGATION):
- [1] 'Người chơi / Người dùng' kết nối qua cổng TCP 25565 tới 'AWS Global Accelerator'.
- [2] Icon 'AWS Shield Standard' được đặt ở rìa mạng để lọc bỏ các gói tin độc hại Layer 3/4.
- [3] Traffic sạch sau khi lọc được chuyển tiếp đến 'Network Load Balancer (NLB)' nằm trong VPC.
- [4] NLB định tuyến traffic đến 'Amazon EC2 Instance' (nhãn: Minecraft Server chạy PaperMC). Bên cạnh EC2 hiển thị icon 'AWS Systems Manager (SSM)' đại diện cho quản trị an toàn, và hiển thị cổng SSH Port 22 bị gạch chéo bằng dấu 'X' màu đỏ (biểu thị đóng hoàn toàn).

2. LUỒNG PHẢN ỨNG TỰ ĐỘNG HÓA BẢO MẬT (SOAR AUTOMATION LOOP):
- [5] Một mũi tên mang nhãn 'VPC Flow Logs' nối từ EC2 sang 'Amazon GuardDuty' (Hệ thống phát hiện xâm nhập).
- [6] 'Amazon GuardDuty' gửi cảnh báo tấn công sang 'Amazon EventBridge' (Bộ lọc sự kiện thời gian thực).
- [7] 'Amazon EventBridge' kích hoạt một hàm 'AWS Lambda' (hiển thị kèm logo Python nhỏ).
- [8] 'AWS Lambda' thực thi script tự động chỉnh sửa 'VPC Network ACL', thêm một luật 'DENY IP Kẻ Tấn Công' ngay tại cửa ngõ Subnet.
- [9] Đồng thời, 'AWS Lambda' kích hoạt 'Amazon SNS' để bắn một Email cảnh báo khẩn cấp (icon Hộp thư/Chuông báo) tới điện thoại người quản trị.

3. LUỒNG SAO LƯU & KHÔI PHỤC THẢM HỌA (DISASTER RECOVERY & BACKUP):
- [10] Một 'AWS Backup Plan' tự động chụp ảnh snapshot ổ đĩa EBS của EC2 mỗi giờ một lần và lưu trữ an toàn mã hóa bên trong một 'Backup Vault' biệt lập.
```

---

# Các dịch vụ AWS sử dụng

| Dịch vụ | Vai trò |
|----------|----------|
| Amazon EC2 | Chạy máy chủ Minecraft |
| Amazon VPC | Phân vùng mạng |
| Security Group | Kiểm soát lưu lượng truy cập |
| Network ACL | Lớp bảo vệ mạng |
| IAM | Quản lý quyền truy cập |
| Systems Manager Session Manager | Quản trị không cần SSH |
| Amazon GuardDuty | Phát hiện mối đe dọa |
| Amazon EventBridge | Điều phối sự kiện |
| AWS Lambda | Phản ứng tự động |
| Amazon SNS | Gửi thông báo |
| AWS Backup | Sao lưu dữ liệu |
| Backup Vault | Lưu trữ bản sao lưu |
| Global Accelerator | Che giấu IP và tăng khả năng chống DDoS |
| Network Load Balancer | Cân bằng tải TCP |
| Amazon CloudWatch | Thu thập log |
| AWS CloudTrail | Ghi nhận hoạt động hệ thống |

---

# 5. Thiết kế kỹ thuật (Technical Design)

## Quản trị theo mô hình Zero Trust

Hệ thống không mở cổng SSH (22) ra Internet.

Quản trị viên sử dụng AWS Systems Manager Session Manager để kết nối trực tiếp đến EC2 thông qua IAM Role.

Lợi ích:

- Không cần Key Pair.
- Không cần Bastion Host.
- Giảm nguy cơ Brute Force SSH.
- Tuân thủ nguyên tắc Least Privilege.

---

## Phát hiện mối đe dọa

Amazon GuardDuty liên tục phân tích:

- VPC Flow Logs.
- CloudTrail Logs.
- DNS Logs.

Khi phát hiện hành vi bất thường, GuardDuty sinh ra Security Finding.

---

## Tự động phản ứng

Sau khi GuardDuty phát hiện mối đe dọa:

```
- [5] Một mũi tên mang nhãn 'VPC Flow Logs' nối từ EC2 sang 'Amazon GuardDuty' (Hệ thống phát hiện xâm nhập).
- [6] 'Amazon GuardDuty' gửi cảnh báo tấn công sang 'Amazon EventBridge' (Bộ lọc sự kiện thời gian thực).
- [7] 'Amazon EventBridge' kích hoạt một hàm 'AWS Lambda' (hiển thị kèm logo Python nhỏ).
- [8] 'AWS Lambda' thực thi script tự động chỉnh sửa 'VPC Network ACL', thêm một luật 'DENY IP Kẻ Tấn Công' ngay tại cửa ngõ Subnet.
- [9] Đồng thời, 'AWS Lambda' kích hoạt 'Amazon SNS' để bắn một Email cảnh báo khẩn cấp (icon Hộp thư/Chuông báo) tới điện thoại người quản trị.
```

Quá trình này diễn ra hoàn toàn tự động mà không cần sự can thiệp của quản trị viên.

---

## Sao lưu và khôi phục

Dữ liệu thế giới Minecraft được sao lưu định kỳ bằng AWS Backup.

Các bản sao lưu được lưu trong Backup Vault và có thể nhanh chóng phục hồi khi xảy ra sự cố hoặc mất dữ liệu.

---

# 6. Các tính năng bảo mật

## Bảo mật hạ tầng

- Kiến trúc Zero Trust.
- Không mở SSH Public.
- IAM Least Privilege.
- Security Group.
- Network ACL.

## Phát hiện mối đe dọa

- Amazon GuardDuty.
- CloudWatch Logs.
- AWS CloudTrail.

## Tự động phản ứng

- EventBridge.
- AWS Lambda.
- Chặn IP tự động.
- Gửi Email cảnh báo.

## Khả năng sẵn sàng

- AWS Global Accelerator.
- Network Load Balancer.

## Khả năng phục hồi

- AWS Backup.
- Backup Vault.
- Sao lưu định kỳ.
- Disaster Recovery.

---

# 7. Kế hoạch triển khai

## Giai đoạn 1

Thiết kế kiến trúc

- Phân tích yêu cầu.
- Thiết kế hạ tầng AWS.
- Thiết kế kiến trúc bảo mật.

---

## Giai đoạn 2

Triển khai hạ tầng

- Amazon VPC.
- Security Group.
- IAM.
- EC2.

---

## Giai đoạn 3

Triển khai máy chủ Minecraft

- Ubuntu Server.
- Java Runtime.
- PaperMC Server.
- Session Manager.

---

## Giai đoạn 4

Triển khai hệ thống bảo mật

- GuardDuty.
- EventBridge.
- Lambda.
- SNS.

---

## Giai đoạn 5

Triển khai tính sẵn sàng

- Network Load Balancer.
- AWS Global Accelerator.

---

## Giai đoạn 6

Triển khai sao lưu

- AWS Backup.
- Backup Vault.
- Backup Plan.

---

## Giai đoạn 7

Kiểm thử

- Sinh sự kiện tấn công mẫu.
- Kiểm tra phản ứng tự động.
- Kiểm tra gửi Email.
- Kiểm tra khôi phục dữ liệu.

---

# 8. Dự toán chi phí

Hệ thống sử dụng chủ yếu các dịch vụ thuộc AWS Free Tier.

Chi phí phát sinh chủ yếu đến từ:

- Amazon EC2.
- AWS Global Accelerator.
- Network Load Balancer.
- GuardDuty.
- AWS Backup.

Chi phí vận hành phụ thuộc vào:

- Thời gian hoạt động của EC2.
- Lượng lưu lượng mạng.
- Số lượng Security Findings.
- Dung lượng dữ liệu sao lưu.

Có thể sử dụng AWS Pricing Calculator để ước lượng chi phí trước khi triển khai.

---

# 9. Đánh giá rủi ro

| Rủi ro | Mức độ | Biện pháp |
|---------|---------|-----------|
| Tấn công DDoS | Cao | Global Accelerator |
| Brute Force SSH | Cao | Không mở SSH |
| Mất dữ liệu | Cao | AWS Backup |
| Truy cập trái phép | Trung bình | IAM & Session Manager |
| Chi phí vượt dự kiến | Trung bình | AWS Budget và Cost Explorer |

---

# 10. Kết quả mong đợi

## Về kỹ thuật

- Triển khai thành công máy chủ Minecraft trên AWS.
- Xây dựng hệ thống phát hiện xâm nhập tự động.
- Tự động phản ứng khi phát hiện tấn công.
- Tự động gửi Email cảnh báo.
- Thực hiện sao lưu và khôi phục dữ liệu.

## Về học thuật

- Hiểu rõ kiến trúc bảo mật trên AWS.
- Thực hành mô hình SOAR.
- Tiếp cận các dịch vụ bảo mật của AWS.
- Áp dụng kiến thức Cloud Security vào dự án thực tế.

---

# 11. Hướng phát triển

Trong tương lai, hệ thống có thể được mở rộng với các dịch vụ như:

- AWS Security Hub.
- Amazon Inspector.
- AWS Config.
- AWS Firewall Manager.
- Route 53.
- Amazon CloudFront.
- AWS CDK hoặc Terraform để tự động triển khai hạ tầng.
- Dashboard giám sát bằng Grafana.
- Tích hợp Discord Bot hoặc Telegram Bot để gửi cảnh báo theo thời gian thực.

---

# 12. Kết luận

Dự án **Hệ thống bảo mật máy chủ Minecraft trên AWS** không chỉ giải quyết bài toán triển khai một máy chủ trò chơi an toàn mà còn minh họa cách kết hợp các dịch vụ bảo mật của AWS để xây dựng một hệ thống giám sát và phản ứng tự động trước các mối đe dọa.

Thông qua việc áp dụng các nguyên tắc Zero Trust, Security Automation và Disaster Recovery, hệ thống mang lại khả năng bảo vệ hạ tầng, giảm thiểu rủi ro và nâng cao khả năng sẵn sàng của dịch vụ. Đây đồng thời là mô hình thực hành phù hợp cho việc học tập, nghiên cứu và phát triển các giải pháp Cloud Security trong môi trường thực tế.