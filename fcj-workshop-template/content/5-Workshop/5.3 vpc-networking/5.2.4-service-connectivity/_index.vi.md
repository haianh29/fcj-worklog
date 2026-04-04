---
title: "6.2.4 Kết nối dịch vụ - ECS, RDS, S3 & Messaging"
date: 2026-01-01
weight: 4
chapter: false
---

# 6.2.4 Kết nối dịch vụ - ECS, RDS, S3 & Messaging

Cuối cùng, bạn kết nối các dịch vụ AWS vào VPC để ứng dụng có thể chạy end-to-end.

#### Các thành phần được kết nối

- **ECS Fargate service** trong private subnets, nhận traffic từ ALB ở public subnets.
- **RDS PostgreSQL** trong private subnets, chỉ cho phép truy cập từ security group của ECS.
- Truy cập từ ECS tasks tới:
  - **Amazon ECR** để kéo container image.
  - **Amazon S3** để lưu trữ tệp.
  - **Amazon SQS/SNS** cho background jobs và notifications.
  - **Amazon SES** để gửi OTP và email hệ thống.
  - **AWS Secrets Manager** để lấy DB credentials và SMTP/SES secrets.

#### ALB và Target Group

![Application Load Balancer in public subnets routing traffic to ECS](/images/5-Workshop/5.3-vpc-networking/ALB.png)

![Target Group for ECS service behind ALB](/images/5-Workshop/5.3-vpc-networking/TG.png)

Các sơ đồ này thể hiện cách ALB lắng nghe ở public subnets và chỉ chuyển tiếp lưu lượng đến các ECS tasks khỏe mạnh trong private subnets thông qua target group.

#### Mẫu kết nối mạng

- Bắt đầu với mô hình truy cập qua **NAT gateway** tới các public AWS endpoints.
- Tùy chọn mở rộng: dùng **VPC endpoints** (S3, SQS, SNS, Secrets Manager, CloudWatch Logs) như một bước hardening cho môi trường production.

#### Nhiệm vụ workshop

- Gắn private subnets vào ECS cluster và RDS subnet group.
- Xác minh ECS tasks có thể truy cập ECR, S3, SQS/SNS/SES và Secrets Manager từ private subnets.
- Đối chiếu cách lớp mạng này hỗ trợ các module phía sau: backend trên ECS/RDS, messaging và notifications, security, và observability.
