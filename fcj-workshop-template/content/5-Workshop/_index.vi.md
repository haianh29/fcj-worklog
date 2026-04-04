---
title: "Workshop - AI Production Management System"
date: 2026-01-01
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

# AI Production Management System on AWS - Workshop

#### Tổng quan

Workshop này hướng dẫn toàn bộ quá trình thiết kế và triển khai end-to-end một **hệ thống quản lý sản xuất điện tử có hỗ trợ AI** trên AWS.

Hệ thống là một dự án thực tế, kết hợp:

- **Backend:** Spring Boot (containerized) chạy trên Amazon ECS Fargate
- **Frontend:** React (Vite) host trên Amazon S3 và phân phối qua Amazon CloudFront
- **Database:** Amazon RDS (PostgreSQL)
- **Infrastructure & Security:** VPC, subnets, security groups, IAM, AWS Secrets Manager, AWS KMS
- **Messaging & Notifications:** Amazon SQS, Amazon SNS, Amazon SES (OTP và alerts)
- **Observability:** Amazon CloudWatch Logs, Metrics, Dashboards và Alarms

Bạn sẽ thấy cách kiến trúc trong proposal và các architecture diagrams được hiện thực trong thực tế, từ networking và containers cho đến monitoring và alerting.

#### Bạn sẽ học được gì

Kết thúc workshop, bạn có thể:

- Thiết kế **kiến trúc dựa trên VPC** với public/private subnets, ALB, ECS services và RDS.
- Build và đóng gói backend Spring Boot thành Docker image rồi push lên **Amazon ECR**.
- Triển khai backend lên **Amazon ECS Fargate** phía sau **Application Load Balancer**.
- Build frontend React và triển khai lên **Amazon S3 + CloudFront + Route 53** với HTTPS.
- Dùng **Amazon SQS** và **Amazon SNS** để tách rời background tasks và alerts.
- Tích hợp **Amazon SES** để gửi OTP emails và production alerts.
- Áp dụng best practices bảo mật với **IAM roles**, IAM user cho SES, **Secrets Manager** và mã hóa **KMS**.
- Cấu hình **CloudWatch Logs**, **metrics**, **dashboards** và **alarms** (ví dụ ECS CPU > 80%) để giám sát hệ thống.

#### Đối tượng phù hợp

- Sinh viên và kỹ sư muốn có một ví dụ cụ thể về hệ thống web kiểu production trên AWS.
- Developers đã có kiến thức cơ bản về AWS (EC2/ECS, S3, IAM) và phát triển web (Java/Spring, React).

#### Các module trong workshop

Workshop được tổ chức thành các phần sau (xem thư mục con trong `5-Workshop/`):

1. **[System & Workshop Overview](5.1-Workshop-overview/)** - bối cảnh nghiệp vụ của hệ thống IMS và cách tổ chức phần lab thực hành.
2. **[Solution Architecture & IaC](5.2-architecture-iac/)** - kiến trúc tổng thể IMS trên AWS và hướng tiếp cận infrastructure-as-code (tùy chọn).
3. **[VPC & Networking](5.3%20vpc-networking/)** - VPC, subnets, routing, Internet/NAT gateways, security groups và kết nối tới dịch vụ AWS.
4. **[Backend on ECS & RDS](5.4-backend-ecs-rds/)** - Spring Boot containers, ECR repository, ECS task definitions/services và PostgreSQL schema.
5. **[Frontend on S3 & CloudFront](5.5-frontend-s3-cloudfront/)** - React build pipeline, S3 static hosting, CloudFront distribution và domain configuration.
6. **[Messaging & Notifications (SQS/SNS/SES)](5.6-messaging-notifications-sqs-sns-ses/)** - SQS queues, SNS topics và SES email/OTP flows.
7. **[Auth & Secrets](5.7-auth-security-secrets/)** - IAM roles, SES IAM user, Secrets Manager, KMS và application security patterns.
8. **[AI & Production Analytics](5.8-ai-production-analytics/)** - cách dữ liệu sản xuất (orders, lines, delays, OEE) được đưa vào AI assistants và báo cáo.
9. **[Observability & CI/CD](5.9-observability-ci-cd/)** - CloudWatch logs/metrics/alarms, dashboards và pipeline triển khai buildspec/CodeBuild-ECR-ECS.

Mỗi phần liên kết trực tiếp với mã nguồn đang chạy trong repository này (`backend/` và `frontend/`) và với các tài nguyên AWS đã mô tả trong **Idea for AWS project** và **2-Proposal**.
