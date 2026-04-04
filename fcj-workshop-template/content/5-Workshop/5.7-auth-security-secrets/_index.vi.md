---
title: "Xác thực, Bảo mật & Quản lý Secrets"
weight: 6
---

# 6.6 Xác thực, Bảo mật & Quản lý Secrets

Phần này mô tả cách hệ thống IMS xử lý xác thực, phân quyền, bảo mật mạng và
quản lý thông tin nhạy cảm.

## Sơ đồ kiến trúc bảo mật

![IAM roles and permissions for ECS, CI/CD and SES](/images/5-Workshop/5.7-auth-security-secrets/IAM.png)

_Hình IAM cho phần IAM Roles & Permissions trong module 6.6._

![Security group inbound rules for ALB](/images/5-Workshop/5.7-auth-security-secrets/sg-ALB-inbound.png)
![Security group outbound rules for ALB](/images/5-Workshop/5.7-auth-security-secrets/sg-ALB-outbound.png)

_Hai hình SG-ALB dùng cho phần Network Security (ALB security group) của module 6.6._

![Security group inbound rules for ECS tasks](/images/5-Workshop/5.7-auth-security-secrets/sg-ECS-inbound.png)
![Security group outbound rules for ECS tasks](/images/5-Workshop/5.7-auth-security-secrets/sg-ECS-outbound.png)

_Hai hình SG-ECS dùng cho phần Network Security (ECS security group) của module 6.6._

![Security group inbound rules for RDS](/images/5-Workshop/5.7-auth-security-secrets/sg-RDS-inbound.png)
![Security group outbound rules for RDS](/images/5-Workshop/5.7-auth-security-secrets/sg-RDS-outbound.png)

_Hai hình SG-RDS dùng cho phần Network Security (RDS security group) của module 6.6._

![Secrets Manager storing database and SMTP credentials](/images/5-Workshop/5.7-auth-security-secrets/secrete%20manager.png)
![KMS key protecting encrypted secrets](/images/5-Workshop/5.7-auth-security-secrets/KMS.png)

_Hai hình Secrets Manager và KMS cho phần Secrets Management & KMS trong module 6.6._

![CloudWatch alarm as part of security and monitoring](/images/5-Workshop/5.7-auth-security-secrets/cloudwatch-alarm.png)

_Hình CloudWatch Alarm dùng chung cho phần Network Security/Monitoring của module 6.6 và liên kết với module 6.7 Observability & CI/CD._

Các sơ đồ này cho thấy cách IAM, security groups, Secrets Manager và KMS được cấu hình
để triển khai truy cập theo nguyên tắc least-privilege và bảo vệ dữ liệu nhạy cảm.

## Authentication & Authorization

- Backend sử dụng **Spring Security** để bảo vệ APIs và thực thi phân quyền theo vai trò.
- Các vai trò chính:
  - `ADMIN` - các chức năng quản trị hệ thống.
  - `MANAGER` - lập kế hoạch và giám sát sản xuất.
  - `LINE_LEADER` - thực thi công việc tại chuyền/xưởng.
- Frontend tích hợp auth APIs qua `authService` và lưu token ở phía client.

Bạn có thể mở rộng thiết kế auth hiện tại bằng cách tích hợp **Amazon Cognito** làm identity provider:

- User Pool cho quản lý người dùng và hosted login.
- JWT tokens do Cognito phát hành được Spring Boot xác thực.
- Phân quyền chi tiết qua Cognito groups ánh xạ sang vai trò ứng dụng.

### OTP và xác minh email

Cho các luồng quên mật khẩu và xác minh tài khoản, backend có thể cung cấp endpoint như:

- `POST /auth/forgot-password` - tạo OTP ngắn hạn và gửi qua SES đến email người dùng.
- `POST /auth/verify-otp` - xác thực OTP và cho phép đổi mật khẩu.

Mã OTP và thời điểm hết hạn nên được lưu ở phía server (ví dụ trong bảng database
hoặc cache như Redis), và không nhúng trực tiếp vào JWT.

## Network Security

- Tất cả dịch vụ chạy trong một **VPC** riêng.
- **Security Groups** giới hạn lưu lượng:
  - ALB cho phép inbound HTTP/HTTPS từ internet.
  - ECS tasks chỉ nhận lưu lượng từ ALB.
  - RDS chỉ cho phép lưu lượng từ ECS tasks (và nguồn quản trị nếu cần).
- Private subnets dùng cho ECS và RDS, public subnets chỉ dùng cho ALB và NAT gateways.

## IAM Roles & Permissions

IAM được dùng để cấp cho mỗi thành phần đúng mức quyền tối thiểu cần thiết khi truy cập tài nguyên AWS.

### ECS roles

- **ECS task execution role** (ví dụ `ecsTaskExecutionRole-ims-prod`):
  - Được ECS agent sử dụng, không phải mã ứng dụng.
  - Kéo container images từ **ECR**.
  - Ghi logs vào **CloudWatch Logs**.
  - Thường gắn managed policy `AmazonECSTaskExecutionRolePolicy`.

- **ECS task role** (ví dụ `ecsTaskRole-ims-backend-prod`):
  - Được backend Spring Boot trong task sử dụng.
  - Có quyền least-privilege tới:
    - **S3** - đọc/ghi tài liệu sản xuất trong bucket chuyên dụng.
    - **SQS** - gửi và nhận messages cho background jobs và events.
    - **SNS** - publish alert và status messages.
    - **SES** - gửi email nếu dùng AWS SDK thay vì SMTP.
    - **AWS Secrets Manager** - đọc application secrets lúc runtime.
    - **KMS** - giải mã secrets được mã hóa bằng customer-managed key.

### CI/CD roles

- **CodeBuild / CodePipeline roles**:
  - Lấy source từ CodeCommit/GitHub qua CodeConnections.
  - Build backend JAR và Docker image.
  - Push images lên **ECR**.
  - Cập nhật ECS task definitions và services trong quá trình deployment.
  - Upload build artifacts (ví dụ `imagedefinitions.json`, frontend bundles) lên **S3**.

### IAM user cho SES SMTP

Với kiểu gửi email dựa trên SMTP, dùng một IAM user riêng chỉ dành cho SES:

- Ví dụ: `ims-ses-smtp-user`.
- Có quyền gọi `ses:SendEmail` / `ses:SendRawEmail`.
- SMTP credentials tạo trong SES console được lưu dưới dạng secrets
  (không hard-code) và được inject vào ứng dụng qua cấu hình.

Tuân theo nguyên tắc **least privilege** và tránh dùng policy quá rộng `*:*` trong môi trường production.

## Secrets Management & KMS

Dùng **AWS Secrets Manager** để lưu thông tin nhạy cảm như:

- Database credentials (RDS username, password).
- JWT signing keys hoặc OAuth client secrets.
- SES SMTP / access keys và sender addresses.
- External AI API keys (nếu sử dụng).

Secrets được mã hóa khi lưu trữ bằng **AWS KMS** keys (AWS managed hoặc
customer-managed key như `alias/ims-secrets-key`). ECS task role được
cấp quyền gọi `secretsmanager:GetSecretValue` và `kms:Decrypt` để backend
có thể tải secrets an toàn khi khởi động.

Trong ECS Task Definitions, tham chiếu secrets qua:

- Environment variables lấy từ Secrets Manager.
- Hoặc gọi AWS SDK trong ứng dụng bằng task role.

Tuyệt đối không hard-code secrets trong:

- Source code.
- Docker images.
- Frontend bundles.

Khi cấu trúc đúng các thành phần authentication, OTP/email verification, IAM roles,
network boundaries và KMS-encrypted secrets, hệ thống IMS có thể đáp ứng các kỳ vọng
bảo mật phổ biến cho enterprise workloads.
