---
title: "Phan tich san xuat voi AI"
weight: 8
---

# 6.8 Lớp AI Production Analytics

Phần này tập trung vào cách AI được tích hợp vào hệ thống IMS để cung cấp
insights và analytics dạng ngôn ngữ tự nhiên trên dữ liệu sản xuất.

## Mục tiêu của AI trong IMS

Lớp AI giúp managers và engineers:

- Nhanh chóng nắm được tình trạng hoạt động của các chuyền sản xuất.
- Xác định điểm chậm tiến độ và bottlenecks.
- Tóm tắt dashboard phức tạp thành nội dung ở mức điều hành.
- Trả lời các câu hỏi ad-hoc về đơn hàng, lịch sản xuất, OEE và độ trễ.

Ví dụ các câu hỏi hệ thống có thể trả lời:

- "Công đoạn nào đang gây chậm cho kế hoạch tuần này?"
- "OEE hôm nay của chuyền SMT 1 là bao nhiêu?"
- "Liệt kê các đơn hàng có nguy cơ trễ deadline."

## Nguồn dữ liệu

Các dịch vụ AI sử dụng dữ liệu lưu trong **Amazon RDS**, bao gồm:

- Orders và work orders.
- Lịch sản xuất và execution logs thực tế.
- Chỉ số hiệu năng chuyền (OEE, throughput, downtime).
- Lịch sử trễ tiến độ và incident records.

Các backend services tổng hợp dữ liệu này thành prompt có cấu trúc trước khi gửi tới
LLM/AI API.

## Backend AI Services

Trong backend (Spring Boot), phần AI thường được triển khai qua các service như:

- `AIProductionAnalysisService`
- `ProductionAnalysisService`

Các service này:

- Truy vấn dữ liệu sản xuất từ RDS.
- Xây dựng context gọn và có cấu trúc (ví dụ JSON hoặc các bullet points).
- Gọi external AI API (ví dụ OpenAI) bằng secret API key lưu trong **AWS Secrets Manager**.
- Hậu xử lý phản hồi AI thành văn bản dễ đọc hoặc JSON có cấu trúc cho frontend.

## Lưu ý về bảo mật và chi phí

- **Secrets**: Không hard-code AI API keys; luôn lấy từ Secrets Manager
  thông qua ECS task role.
- **Privacy**: Tránh gửi dữ liệu cá nhân hoặc dữ liệu nhạy cảm không cần thiết tới AI APIs.
- **Cost**: Đặt giới hạn tần suất request và kích thước context tối đa.
- **Timeouts & Retries**: Thiết lập timeout hợp lý và xử lý lỗi để ứng dụng
  vẫn phản hồi tốt khi nhà cung cấp AI chậm.

## Tích hợp Frontend

Frontend React gọi các AI-related endpoints qua `aiService` và hiển thị:

- Các bản tóm tắt ngôn ngữ tự nhiên (ví dụ: "Tóm tắt sức khỏe sản xuất hôm nay").
- Các rủi ro nổi bật (đơn trễ, chuyền quá tải).
- Gợi ý hoặc hành động tiếp theo cho managers.

Bằng cách kết hợp dữ liệu sản xuất mang tính xác định với lớp AI summarization,
hệ thống IMS mang lại cách tiếp cận trực quan hơn để người dùng không chuyên kỹ thuật
vẫn hiểu nhanh tình trạng nhà máy.
