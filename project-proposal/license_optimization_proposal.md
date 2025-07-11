# Đề xuất Dự án: Nền tảng Tối Ưu Hóa License với Usage Tracking

---

## Executive Summary

Trong bối cảnh các tổ chức sử dụng nhiều phần mềm bản quyền với chi phí ngày càng gia tăng, việc quản lý license hiệu quả đóng vai trò quan trọng để tối ưu chi phí, đảm bảo tuân thủ pháp lý và hỗ trợ ra quyết định chiến lược. Tuy nhiên, nhiều tổ chức hiện vẫn quản lý license theo cách thủ công, dẫn đến việc cấp phát dư thừa, không có khả năng theo dõi theo thời gian thực, và không phát hiện được license không sử dụng.

Dự án này đề xuất một nền tảng nhỏ gọn nhằm theo dõi việc sử dụng license và cung cấp các khuyến nghị tối ưu hoá dựa trên dữ liệu hoạt động thực tế. Giải pháp sử dụng công cụ trên nền tảng AWS kết hợp với các công nghệ mã nguồn mở như Python, Streamlit, SQLite để triển khai một hệ thống thu thập dữ liệu, phân tích sử dụng và báo cáo trực quan.

**Lợi ích chính:**

- Cắt giảm lãng phí license không sử dụng (dự kiến 20–30%)
- Hỗ trợ kiểm tra tuân thủ dễ dàng
- Cải thiện khả năng ra quyết định phân bổ tài nguyên

**Đầu tư và thời gian:**

- Mức đầu tư: tối thiểu trong môi trường demo
- Thời gian: 8 tuần

**Thành công đo lường bằng:**

- Nhận diện đúng license nhàn rỗi (>90% độ chính xác)
- Tỷ lệ sử dụng license tăng ≥ 20%

---

## Problem Statement

### Phân tích hiện trạng

Nhiều đội phát triển nhỏ được cấp quyền truy cập vào các tài nguyên như GitHub, Adobe, Office 365,... nhưng không có công cụ theo dõi hoặc báo cáo mức độ sử dụng. Điều này dẫn đến:

- License cấp phát nhưng không được sử dụng
- Không thể xác định ai đang dùng, ai không
- Không có cảnh báo khi vượt quá giới hạn license

### Pain Points và tác động định lượng:

- Trung bình 25–40% license bị cấp phát mà không được sử dụng
- Mỗi user GitHub Enterprise có thể tiêu tốn \$20/tháng không cần thiết

### Stakeholders chịu ảnh hưởng:

- Team leader: khó kiểm soát tài nguyên
- Người tài trợ hoặc quản trị tài chính: chi phí tăng cao

### Hệ quả nếu không hành động:

- Gia tăng chi phí sử dụng phần mềm
- Gây khó khăn trong kiểm toán hoặc đánh giá hiệu quả sử dụng

### Cơ hội mở rộng:

Dự án này có thể được phát triển thành một công cụ nhẹ phục vụ các nhóm sinh viên, nhóm nghiên cứu hoặc startup nhỏ.

---

## Solution Architecture

### Kiến trúc tổng quan:

```
[GitHub API/Microsoft Graph API/CSV] → [AWS Lambda/Python Script] → [SQLite/S3] → [Streamlit Dashboard] → [Báo cáo]
```

### Dịch vụ và công nghệ sử dụng:

- AWS Lambda (xử lý script tự động)
- Amazon S3 (lưu dữ liệu và báo cáo)
- Amazon CloudWatch (log và cảnh báo)
- Python + Streamlit + SQLite

### Thành phần chính:

- **Data Collector:** thu thập dữ liệu người dùng và license qua API hoặc import file CSV
- **Logic Engine:** đánh giá tình trạng sử dụng (idle, active)
- **Dashboard:** giao diện trực quan với Streamlit
- **Alert Engine:** gửi cảnh báo qua email hoặc webhook

### Kiến trúc bảo mật:

- Xác thực API bằng OAuth token
- Không lưu trữ thông tin cá nhân định danh (PII)
- Mã hóa dữ liệu lưu trữ

### Tính mở rộng và tích hợp:

- Có thể thêm tích hợp với hệ thống nội bộ hoặc API khác (Adobe, Jira, v.v.)

---

## Technical Implementation

### Các giai đoạn triển khai:

1. Tuần 1–2: Kết nối API, xác thực và kiểm thử dữ liệu đầu vào
2. Tuần 3: Viết script Python thu thập dữ liệu
3. Tuần 4: Phát triển module phân tích logic (idle detection, overuse)
4. Tuần 5: Xây dựng giao diện người dùng (Streamlit)
5. Tuần 6: Thiết lập gửi báo cáo định kỳ qua email hoặc lưu trên hệ thống
6. Tuần 7: Kiểm thử hệ thống
7. Tuần 8: Tổng kết và báo cáo kết quả

### Yêu cầu kỹ thuật:

- Python 3.x
- Streamlit framework
- SQLite hoặc Amazon S3
- GitHub API, Microsoft Graph API hoặc file CSV giả lập

### Testing:

- Unit test cho các module xử lý API
- Integration test giữa các thành phần
- Manual test với bộ dữ liệu mẫu

### Triển khai:

- Chạy cục bộ hoặc đẩy lên môi trường đám mây
- Dự phòng bằng cách lưu snapshot của dữ liệu và script

---

## Timeline & Milestones

| Tuần | Milestone           | Kết quả mong đợi      |
| ---- | ------------------- | --------------------- |
| 1–2  | Kết nối API         | API key hoạt động     |
| 3    | Script hoàn chỉnh   | Có dữ liệu license    |
| 4    | Logic đánh giá      | Phân loại active/idle |
| 5    | Streamlit dashboard | Giao diện trực quan   |
| 6    | Hệ thống cảnh báo   | Cảnh báo hoạt động    |
| 7    | Kiểm thử hệ thống   | ≥ 90% test pass       |
| 8    | Tổng kết demo       | Báo cáo hoàn chỉnh    |

### Phân bổ nhân lực:

- 1 lập trình viên
- 1 người cố vấn kỹ thuật (nếu có)

---

## Budget Estimation

| Hạng mục   | Chi phí | Ghi chú              |
| ---------- | ------- | -------------------- |
| AWS Lambda | \$0     | Xử lý backend        |
| Amazon S3  | \$0     | Lưu trữ dữ liệu      |
| Streamlit  | \$0     | Dùng bản mã nguồn mở |
| GitHub API | \$0     | Miễn phí sử dụng     |

**Tổng chi phí:** \$0 cho môi trường demo

### ROI:

- Tăng hiệu suất sử dụng license ≥ 20%
- Giảm chi phí license dư thừa trung bình từ \$200–500/tháng (khi áp dụng thực tế)

---

## Risk Assessment

| Rủi ro               | Xác suất   | Ảnh hưởng  | Biện pháp                         |
| -------------------- | ---------- | ---------- | --------------------------------- |
| API không ổn định    | Trung bình | Trung bình | Dùng dữ liệu backup (CSV)         |
| Dữ liệu không đầy đủ | Cao        | Cao        | Cho phép nhập tay khi cần         |
| Dashboard lỗi        | Thấp       | Trung bình | Kiểm thử đa nền tảng              |
| Hiểu sai khuyến nghị | Trung bình | Trung bình | Đưa giải thích và tooltip rõ ràng |

---

## Expected Outcomes

### Chỉ số thành công:

- Nhận diện license không sử dụng chính xác ≥ 90%
- Dashboard phản hồi dưới 2 giây
- Thu thập đầy đủ dữ liệu sử dụng

### Lợi ích theo thời gian:

- Ngắn hạn (0–6 tháng): có khả năng kiểm soát tình trạng license
- Trung hạn (6–18 tháng): triển khai trong nhóm thực tế
- Dài hạn (18+ tháng): mở rộng thành sản phẩm có thể thương mại hóa

### Cải thiện trải nghiệm người dùng:

- Giao diện đơn giản, dễ thao tác
- Báo cáo và cảnh báo rõ ràng

---

## Phụ lục

### A. Sơ đồ kiến trúc hệ thống

(Sơ đồ minh hoạ các thành phần đã trình bày trong phần Solution Architecture)

### B. Script mẫu thu thập dữ liệu GitHub

(Đoạn mã Python sử dụng GitHub API để lấy thông tin người dùng)

### C. Dashboard mẫu

(Giao diện Streamlit hiển thị trạng thái license, biểu đồ sử dụng, và khuyến nghị tối ưu hóa)

### D. Tài liệu tham khảo

- GitHub REST API Docs: [https://docs.github.com/en/rest](https://docs.github.com/en/rest)
- Microsoft Graph API Docs: [https://learn.microsoft.com/en-us/graph/overview](https://learn.microsoft.com/en-us/graph/overview)
- Streamlit Docs: [https://docs.streamlit.io](https://docs.streamlit.io)
- AWS Lambda Docs: [https://docs.aws.amazon.com/lambda/latest/dg/welcome.html](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)
- AWS S3 Docs: [https://docs.aws.amazon.com/s3/index.html](https://docs.aws.amazon.com/s3/index.html)

