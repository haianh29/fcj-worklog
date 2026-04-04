---
title: "6.2.2 Định tuyến, Internet Gateway & NAT"
date: 2026-01-01
weight: 2
chapter: false
---

# 6.2.2 Định tuyến, Internet Gateway & NAT

Trong phần này, bạn cấu hình luồng lưu lượng đi vào và đi ra khỏi VPC.

Trong môi trường `vpc-ims`, kiến trúc định tuyến được tổ chức như sau:

- **Internet Gateway:** `igw-ims` được gắn vào `vpc-ims`.
- **Public route table:** `rt-public` gắn với hai public subnet và định tuyến `0.0.0.0/0 -> igw-ims`.
- **Private route table:** `rt-private` gắn với ba private subnet và định tuyến `0.0.0.0/0 -> nat-ims`.
- **NAT gateway:** `nat-ims` đặt trong public subnet để private subnets có thể truy cập Internet theo chiều outbound.

#### Vì sao phần này quan trọng

- Application Load Balancer và NAT gateway cần truy cập Internet thông qua IGW.
- ECS tasks trong private subnets phải truy cập được các dịch vụ bên ngoài (kéo image từ ECR, gọi external APIs, SES/SNS/SQS) **nhưng không bị public trực tiếp**.

#### Nhiệm vụ workshop

- Tạo mới hoặc xác minh **Internet Gateway** `igw-ims` và gắn vào VPC.
- Tạo/xác minh `rt-public` và `rt-private`, sau đó associate với đúng các subnet.
- Đảm bảo `rt-public` định tuyến `0.0.0.0/0` tới `igw-ims` và `rt-private` định tuyến `0.0.0.0/0` tới NAT gateway `nat-ims`.
