---
title: "6.2.1 Kiến thức VPC cơ bản - CIDR & Subnets"
date: 2026-01-01
weight: 1
chapter: false
---

# 6.2.1 Kiến thức VPC cơ bản - CIDR & Subnets

Trong bước này, bạn sẽ tạo **VPC và các subnet** để triển khai hệ thống AI Production Management System.

Trong workshop này, chúng ta dùng mô hình VPC tương tự môi trường thực tế:

- Tên VPC: `vpc-ims`
- CIDR block: `12.0.0.0/16`
- Availability Zones: `ap-southeast-1a` và `ap-southeast-1b`
- Các subnet:
  - **Public-Subnet1** tại `ap-southeast-1a` - `12.0.1.0/24`
  - **Public-Subnet2** tại `ap-southeast-1b` - `12.0.2.0/24`
  - **Private-Subnet1** tại `ap-southeast-1a` - `12.0.3.0/24`
  - **Private-Subnet2** tại `ap-southeast-1a` - `12.0.4.0/24`
  - **Private-Subnet-5** tại `ap-southeast-1b` - `12.0.5.0/24`

#### Vì sao phần này quan trọng

- Public subnet chỉ công khai **điểm vào (ALB / NAT Gateway)** ra Internet.
- Private subnet giúp cô lập **application containers và database** khỏi truy cập trực tiếp từ bên ngoài.
- Triển khai trên 2 AZ giúp tăng tính sẵn sàng cho điểm vào frontend và các backend services.

#### Sơ đồ: Bố cục VPC của IMS

![IMS VPC with public and private subnets across AZs](/images/5-Workshop/5.3-vpc-networking/VPC.png)

#### Nhiệm vụ workshop

- Tạo mới hoặc xác minh VPC với CIDR `12.0.0.0/16` và các subnet như trên.
- Gắn tag rõ ràng cho subnet (ví dụ: `ims-public-1a`, `ims-public-1b`, `ims-private-1a`, `ims-private-1a-extra`, `ims-private-1b`).
- Ở các bước sau, gắn các private subnet này vào ECS cluster và RDS subnet group.
