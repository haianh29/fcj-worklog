---
title: "6.2.3 Ranh giới bảo mật - Security Groups, NACLs & IAM"
date: 2026-01-01
weight: 3
chapter: false
---

# 6.2.3 Ranh giới bảo mật - Security Groups, NACLs & IAM

Phần này định nghĩa cách cho phép lưu lượng giữa các thành phần và cách bảo mật mạng liên kết với IAM và secrets.

#### Bạn sẽ cấu hình gì

- **Security groups** cho:
  - Application Load Balancer: cho phép HTTP/HTTPS từ Internet.
  - ECS service: chỉ cho phép lưu lượng từ security group của ALB.
  - RDS PostgreSQL: chỉ cho phép lưu lượng từ security group của ECS service.
- **Network ACLs** (NACLs) tùy chọn - giữ đơn giản, dùng default allow rules trong workshop.
- Mối quan hệ giữa **ranh giới mạng** và **ranh giới danh tính**:
  - Security groups / NACLs: kiểm soát thành phần nào được giao tiếp ở **tầng mạng**.
  - IAM roles & policies: kiểm soát ECS tasks được gọi những **AWS APIs** nào (ECR, S3, SQS, SNS, SES, Secrets Manager, CloudWatch).
  - **Secrets Manager + KMS**: lưu trữ và mã hóa thông tin nhạy cảm như DB credentials, SMTP/SES secrets và các cấu hình bí mật khác.

#### Nhiệm vụ workshop

- Tạo security groups cho ALB, ECS service và RDS, sau đó kết nối đúng luồng truy cập giữa chúng.
- Xác minh database chỉ truy cập được từ ECS tasks, không truy cập trực tiếp từ Internet.
- Liên kết sang cấu hình IAM và secrets chi tiết ở module [6.6-auth-security-secrets](../../5.7-auth-security-secrets/).
