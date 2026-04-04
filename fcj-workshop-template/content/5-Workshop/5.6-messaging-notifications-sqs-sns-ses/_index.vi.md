---
title: "Messaging & Notifications (SQS, SNS, SES)"
weight: 5
---

# 6.5 Nhắn tin & Thông báo với SQS, SNS, SES

Phần này tập trung vào xử lý bất đồng bộ và cơ chế thông báo trong hệ thống IMS,
sử dụng Amazon SQS, Amazon SNS và Amazon SES.

## Sơ đồ messaging & notifications

![SQS queue configuration for IMS background jobs](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20queue.png)
![SQS access policy for producers and consumers](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20policy.png)
![Queue details including DLQ configuration](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20config.png)

![SNS topic used to broadcast production alerts](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS.png)
![Email alert received from SNS notification](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS%20alert.png)

![SES configuration for sending OTP and notification emails](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SES.png)

![CloudWatch alarm integrated with SNS for infrastructure alerts](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/cloudwatch-alarm.png)

Các hình trên minh họa cách hàng đợi, topic, gửi email và cảnh báo được cấu hình để hỗ trợ xử lý bất đồng bộ và cơ chế alert.

## Use Cases

- Xếp hàng các tác vụ nền như:
  - Tính toán lại production KPIs.
  - Tạo báo cáo sản xuất theo ngày/tuần.
  - Xử lý các sự kiện chậm tiến độ hoặc exception.
- Fan-out notifications đến nhiều bên nhận (ví dụ: managers, monitoring tools).
- Gửi OTP email và thông báo hệ thống (ví dụ: thay đổi lịch, cảnh báo quan trọng).

## Amazon SQS - Xử lý nền

1. Tạo queues cho background jobs (ví dụ: `ims-delay-events`, `ims-report-jobs`).
2. Cấu hình dead-letter queues (DLQ) cho các message lỗi.
3. Trong backend, thiết kế services để:
   - Publish messages lên SQS khi có sự kiện xảy ra (ví dụ: phát hiện delay).
   - Consume messages từ SQS (qua scheduled tasks, workers hoặc ECS services).
4. Sử dụng message attributes để truyền thêm ngữ cảnh (order ID, line, severity, ...).

## Amazon SNS - Alerts & Fan-Out

1. Tạo SNS topics (ví dụ: `ims-critical-alerts`, `ims-status-updates`).
2. Subscribe SQS queues, email addresses hoặc các endpoints khác vào các topic này.
3. Từ backend services, publish high-level events lên SNS khi:
   - Xảy ra sự cố sản xuất nghiêm trọng.
   - Kích hoạt các ngưỡng cảnh báo quan trọng.
4. Tích hợp SNS với CloudWatch alarms để nhận cảnh báo hạ tầng.

## Amazon SES - OTP Email & Notifications

1. Verify domains và email addresses trong **Amazon SES**.
2. Cấu hình backend gửi email bằng SES (ví dụ dùng HTML template
   cho OTP hoặc thông báo lịch sản xuất).
3. Các luồng điển hình:
   - Quên mật khẩu -> backend tạo OTP (kèm thời hạn) -> gửi qua SES -> người dùng submit
     OTP về API -> backend xác thực OTP và cho phép đặt lại mật khẩu.
   - Manager tạo lịch mới -> hệ thống gửi email cho line leaders kèm tài liệu/đường dẫn
     hoặc link tới trang lịch.
4. Xử lý giới hạn SES sandbox (cần verify cả sender và recipient khi còn trong sandbox).
5. Theo dõi SES metrics và bounces trong CloudWatch / SNS.

Khi kết nối SQS, SNS và SES với nhau, hệ thống IMS có thể xử lý khối lượng công việc lớn
theo mô hình bất đồng bộ và luôn giữ người dùng được cập nhật về các sự kiện sản xuất quan trọng.
