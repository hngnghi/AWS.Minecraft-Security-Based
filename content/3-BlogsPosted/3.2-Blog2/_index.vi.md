# [DỰ ÁN ĐANG ĐƯỢC CẬP NHẬT] CYBER SECURITY TRÊN AWS: TỪ WAF TỰ ĐỘNG HÓA ĐẾN HỆ THỐNG PHÁT HIỆN XÂM NHẬP BẰNG MACHINE LEARNING

Trong quá trình tìm hiểu về Cyber Security trên AWS, mình đã có cơ hội nghiên cứu và triển khai giải pháp Security Automations for AWS WAF. Đây là một giải pháp khá thú vị vì nó cho phép tự động phát hiện, phân tích và phản ứng với các hành vi tấn công nhắm vào ứng dụng web mà không cần quá nhiều thao tác thủ công từ đội ngũ vận hành.

Điều mình đánh giá cao ở giải pháp này là khả năng kết hợp nhiều dịch vụ AWS để tạo thành một quy trình bảo vệ hoàn chỉnh. Sau khi nghiên cứu và triển khai mô hình này, mình nhận thấy đây là một ví dụ điển hình cho cách AWS xây dựng các hệ thống bảo mật theo hướng tự động hóa và có khả năng mở rộng cao. Tuy nhiên, phần khiến mình hứng thú hơn lại nằm ở bước phát triển tiếp theo.

---

## VẤN ĐỀ - BÀI TOÁN CẦN GIẢI QUYẾT

Các hệ thống WAF truyền thống chủ yếu hoạt động dựa trên các tập luật (Rule-Based Detection). Cách tiếp cận này rất hiệu quả đối với những hình thức tấn công đã được biết trước, nhưng lại gặp nhiều hạn chế khi đối mặt với các kỹ thuật tấn công mới, tấn công lai, tấn công giả hoặc các hành vi bất thường chưa từng xuất hiện trong hệ thống.

Điều đó khiến mình đặt ra câu hỏi:

> "Liệu có thể xây dựng một hệ thống có khả năng học từ dữ liệu mạng để phát hiện các mối đe dọa mà không cần phải định nghĩa trước toàn bộ các rule hay không?"

---

## GIẢI PHÁP

Đó cũng là lý do mình đang nghiên cứu xây dựng một dự án có tên **"Network Intrusion Detection System (NIDS) trên AWS sử dụng Machine Learning"**.

Thay vì chỉ dựa trên các dấu hiệu tấn công đã được định nghĩa sẵn, hệ thống sẽ học từ dữ liệu lưu lượng mạng để nhận biết sự khác biệt giữa hành vi bình thường và hành vi bất thường.

Để thực hiện điều này, mình sử dụng bộ dữ liệu **CSE-CIC-IDS2018 on AWS**, một trong những bộ dữ liệu phổ biến trong lĩnh vực phát hiện xâm nhập mạng hiện nay.

Dataset này được xây dựng trên môi trường AWS và mô phỏng nhiều loại hình tấn công thực tế như:

- DDoS Attack
- DoS Attack
- Brute Force Attack
- Botnet Traffic
- Web Attacks
- Infiltration Attacks
- Reconnaissance Activities
- Các dạng lưu lượng mạng bình thường và bất thường khác

Từ bộ dữ liệu này, mình sẽ tiến hành:

- Tiền xử lý và làm sạch dữ liệu.
- Trích xuất các đặc trưng quan trọng của lưu lượng mạng.
- Huấn luyện mô hình Machine Learning để phân loại lưu lượng bình thường và lưu lượng độc hại.
- Đánh giá hiệu năng của mô hình thông qua các chỉ số như Accuracy, Precision, Recall và F1-Score.
- Triển khai mô hình trên AWS để thực hiện phát hiện tấn công theo thời gian thực.

Kiến trúc mà mình đang hướng tới có thể được mô tả như sau:

```text
Network Traffic
        ↓
Feature Extraction
        ↓
ML Model
        ↓
Threat Detection
        ↓
AWS Lambda
        ↓
AWS WAF / Security Group / SNS
```

Trong mô hình này:

- Lưu lượng mạng sẽ được thu thập và xử lý thành các đặc trưng đầu vào.
- Mô hình Machine Learning sẽ đánh giá mức độ nguy hiểm của từng phiên kết nối hoặc từng luồng dữ liệu.
- Khi phát hiện dấu hiệu tấn công, AWS Lambda có thể tự động kích hoạt các hành động phản ứng.
- Các hành động này có thể bao gồm cập nhật AWS WAF, chặn IP thông qua Security Group hoặc gửi cảnh báo qua Amazon SNS.

Điều mình thấy thú vị là sự kết hợp giữa hai hướng tiếp cận khác nhau:

### Rule-Based Detection

- Hiệu quả với các mối đe dọa đã biết.
- Dễ triển khai và dễ giải thích.
- Phù hợp với các chính sách bảo mật truyền thống.

### Machine Learning-Based Detection

- Có khả năng phát hiện các hành vi bất thường.
- Thích nghi tốt hơn với các mẫu tấn công mới.
- Giảm sự phụ thuộc vào việc cập nhật rule thủ công.

---

## KẾT LUẬN & KIẾN NGHỊ

Trong tương lai, mình tin rằng các hệ thống phòng thủ mạng hiện đại sẽ không chỉ dựa vào các rule cố định mà sẽ kết hợp thêm các mô hình Machine Learning để nâng cao khả năng phát hiện và phản ứng với các mối đe dọa ngày càng phức tạp.

Đối với mình, việc nghiên cứu Security Automations for AWS WAF là bước khởi đầu để hiểu cách xây dựng các cơ chế phòng thủ tự động trên AWS. Còn dự án NIDS sử dụng Machine Learning với bộ dữ liệu CSE-CIC-IDS2018 on AWS là bước tiếp theo nhằm tiến gần hơn đến mục tiêu xây dựng các hệ thống phát hiện xâm nhập thông minh, có khả năng học hỏi và thích nghi với môi trường thực tế.

Đây là hướng nghiên cứu mà mình đã và đang tiếp tục theo đuổi trong thời gian tới. Chi tiết hơn thì hẹn gặp các bạn tại buổi **[HCM] Mini Meetup – First Cloud AI Journey | 06/06/2026** sắp tới nhé!

## KIẾN TRÚC

![Architecture Diagram](/images/3-BlogsPosted/3.2-Blog2/ArchitectureBlog2.png)

---

## LINK TÀI LIỆU & BÀI BÁO LIÊN QUAN

Repository GitHub: https://github.com/PeterHovng/HUTECH_DACN.CyberSecurity.AWS

Slide & Report: https://drive.google.com/.../1IA7GSU3iP9iwe09...

Video Demo: https://drive.google.com/.../1meqhF7-d0B_zZeQrG4mJTcT...

Source Code: https://drive.google.com/.../1qeoT3BBTsU3Tm8rSQ6Y4AXH83C7...

Dataset gốc: https://www.unb.ca/cic/datasets/ids-2018.html

![Blog2](/images/3-BlogsPosted/3.2-Blog2/Blog2.png)