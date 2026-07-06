---
title: "Worklog Tuần 8"
date: 2026-06-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:
* Thực hành môi trường lập trình đám mây AWS Cloud9 và công cụ dòng lệnh AWS CLI.
* Triển khai tự động hóa hạ tầng (Lambda, Tags), bảo mật động (ABAC) và hệ thống giám sát nâng cao (CloudWatch, Grafana).

### Công việc & Tiến độ:

| Thứ | Công việc | Ngày chạy | Công cụ | Kết quả đạt được |
| :---: | :--- | :---: | :--- | :--- |
| **2** | Nghiên cứu kiến trúc Cloud9 & viết kịch bản tự động hóa. | 08/06/2026 | AWS Cloud9, AWS Lambda | Khởi tạo Cloud9 IDE; dùng Lambda tự động hóa chuỗi khởi tạo VPC, Security Group, EC2 và đẩy Webhook thông báo về Slack. |
| **3** | Khám phá giao diện IDE & quản lý tài nguyên theo cụm logic. | 09/06/2026 | AWS Resource Groups, Tag Editor | Thực hành thao tác terminal trên Cloud9. Thiết lập quy tắc gắn thẻ (Tags) để đồng bộ và phân cụm quản lý tài nguyên. |
| **4** | Thao tác file trên IDE & nâng cấp bảo mật phân quyền động. | 10/06/2026 | AWS IAM, Cloud9 Terminal | Chỉnh sửa, điều hướng file trên Cloud; kết hợp IAM Policies và Resource Tags để phân quyền dựa trên thuộc tính (ABAC). |
| **5** | Cấu hình AWS CLI & tham gia Workshop CloudWatch nâng cao. | 11/06/2026 | AWS CLI, CloudWatch Agent | Kiểm tra credentials/region trên Cloud9; tự động hóa cài đặt CloudWatch Agent lên máy chủ để thu thập log và cảnh báo đa lớp. |
| **6** | Dọn dẹp hệ thống & tích hợp giải pháp giám sát trực quan. | 12/06/2026 | Amazon Managed Grafana, CloudWatch | Tổng hợp lợi ích của Cloud IDE và dọn dẹp môi trường. Kết nối metric từ CloudWatch vào Grafana, xây dựng Dashboard theo dõi thời gian thực. |

---

### Kết quả đạt được tuần 8:

* Tạo và sử dụng thành công môi trường Cloud9.
* Thực hành các thao tác file và terminal trong IDE.
* Cấu hình AWS CLI và chạy lệnh AWS từ Cloud9.
* Hiểu rõ trường hợp nên dùng IDE cloud để phát triển.
* Ghi nhớ quy trình dọn dẹp Cloud9 sau khi sử dụng.