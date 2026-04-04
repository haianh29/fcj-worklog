---
title: "Kiến trúc giải pháp & IaC"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Kiến trúc giải pháp & Infrastructure-as-Code

Phần này trình bày kiến trúc tổng thể của hệ thống IMS trên AWS và cách bạn có thể triển khai bằng Infrastructure-as-Code (IaC).

### Kiến trúc logic

Ở mức cao, hệ thống đi theo luồng sau:

- **Trình duyệt / Frontend** - React SPA được build từ thư mục `frontend/`.
- **CDN & Lưu trữ tĩnh** - Artifact frontend được host trên Amazon S3 và phân phối qua Amazon CloudFront.
- **DNS & Định tuyến** - Tên miền tùy chỉnh quản lý bởi Amazon Route 53, trỏ tới CloudFront (frontend) và ALB (backend API).
- **Backend API** - Ứng dụng Spring Boot từ `backend/backend`, đóng gói Docker image và chạy trên Amazon ECS (Fargate) phía sau Application Load Balancer.
- **Cơ sở dữ liệu** - Amazon RDS (PostgreSQL) lưu đơn hàng, kế hoạch sản xuất, hiệu suất chuyền, và kết quả phân tích AI.
- **Lưu trữ tệp** - Nhiều S3 bucket cho:
  - Tài nguyên tĩnh của frontend.
  - Tài liệu sản xuất (POM/SOOP, biểu mẫu, tệp đính kèm).
  - Artifact triển khai và backup.
- **Nhắn tin & Thông báo** - Amazon SQS cho background job, Amazon SNS và SES cho cảnh báo và email.
- **Bảo mật & Cấu hình** - AWS Secrets Manager lưu credential và API key, IAM role cho ECS task và CI/CD.
- **Giám sát** - Amazon CloudWatch cho log, metric, alarm, và dashboard.

### Ánh xạ từ repo sang kiến trúc

- `backend/backend` -> Docker image -> ECS Task Definition -> ECS Service -> ALB Target Group.
- `frontend/` -> đầu ra build của Vite -> S3 website bucket -> CloudFront distribution.
- Database schema (Flyway migrations dưới `src/main/resources/db/migration/`) -> Amazon RDS.
- Template email `otp-email.html` -> luồng OTP và thông báo dựa trên SES.

### Các lựa chọn Infrastructure-as-Code

Bạn có thể hiện thực kiến trúc trên theo nhiều cách:

- Thiết lập thủ công trên console để học từng bước.
- CloudFormation / AWS CDK template để định nghĩa VPC, ECS, RDS, S3, CloudFront và các tài nguyên liên quan.
- Terraform nếu bạn muốn tiếp cận IaC theo phong cách multi-cloud.

Với workshop này, bạn có thể bắt đầu bằng console + CLI để nắm rõ từng thành phần, sau đó mở rộng bằng cách chuẩn hóa thành IaC template.

### Khác biệt so với workshop Serverless

So với ứng dụng Travel Guide serverless trong Workshop 5 (Lambda + API Gateway + DynamoDB):

- Ở đây bạn chạy container service dài hạn trên ECS Fargate thay vì Lambda chạy ngắn hạn.
- Bạn dùng cơ sở dữ liệu quan hệ (RDS PostgreSQL) thay vì DynamoDB.
- Bạn quản lý container image trong ECR và triển khai qua ECS/ALB.

Kiến trúc này gần với cách nhiều hệ thống doanh nghiệp Spring Boot + React hiện có được modernize lên AWS.
