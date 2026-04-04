---
title: "VPC & Networking cho hệ thống IMS"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 6.2 </b> "
---

## VPC & Networking cho hệ thống quản lý sản xuất AI

Trong module này, bạn sẽ thiết kế nền tảng mạng cho hệ thống AI Production Management System.

Bạn sẽ ánh xạ kiến trúc hệ thống vào một VPC duy nhất (ví dụ `vpc-ims`, CIDR `12.0.0.0/16`) với hai subnet public và ba subnet private phân bố trên hai Availability Zone `ap-southeast-1a` và `ap-southeast-1b`, đồng thời xác định vị trí triển khai của Application Load Balancer, ECS services và RDS.

### Mục tiêu học tập

- Hiểu cách kiến trúc IMS được triển khai trong AWS VPC với subnet public và private.
- Đặt ALB, ECS tasks và RDS vào các subnet và Availability Zone phù hợp.
- Chuẩn bị hạ tầng mạng để các module tiếp theo (ECS, RDS, S3/CloudFront, messaging) có thể triển khai an toàn.

### Các phần nội dung

- VPC Basics - CIDR & Subnets
- Routing, Internet Gateway & NAT
- Security Boundaries - Security Groups, NACLs & IAM
- Service Connectivity - ECS, RDS, S3 & Messaging
