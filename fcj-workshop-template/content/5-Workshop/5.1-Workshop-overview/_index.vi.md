---
title: "Tổng quan hệ thống IMS và Workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Tổng quan hệ thống và workshop

Trong mục này, chúng ta tóm tắt bài toán nghiệp vụ, các vai trò người dùng, và kịch bản demo của hệ thống **AI-Assisted Electronics Production Management System (IMS)**, đồng thời giải thích cách workshop thực hành được tổ chức xoay quanh hệ thống này.

### Bài toán nghiệp vụ

Các nhà máy điện tử quy mô vừa và nhỏ thường gặp các vấn đề:

- Lập kế hoạch sản xuất thủ công bằng Excel.
- Không theo dõi được tiến độ theo thời gian thực ở từng công đoạn (SMT, DIP, testing).
- Dữ liệu đơn hàng và báo cáo nằm rải rác ở nhiều file/hệ thống.
- Khó nhìn được năng lực chuyền và điểm nghẽn sản xuất.
- Phụ thuộc hạ tầng on-prem khó mở rộng và khó giám sát.

### Người dùng mục tiêu và vai trò

Hệ thống được thiết kế cho 3 vai trò chính:

- **Admin** - quản lý tài khoản, phân quyền, và cấu hình hệ thống.
- **Manager** - tạo/quản lý đơn hàng sản xuất, lập kế hoạch, theo dõi KPI và OEE.
- **Line Leader** - xem tác vụ được giao, cập nhật trạng thái thực thi, nhận lịch và thông báo.

### Kịch bản demo

Trong workshop, chúng ta sử dụng mô hình nhà máy điện tử mẫu với nhiều chuyền (SMT, DIP, testing):

- Manager tạo đơn hàng mới và kế hoạch sản xuất trên web app.
- Line leader nhận tác vụ theo ngày và cập nhật tiến độ từ hiện trường sản xuất.
- Hệ thống tổng hợp dữ liệu lên dashboard cùng các chỉ số OEE/throughput.
- Các AI endpoint hỗ trợ truy vấn ngôn ngữ tự nhiên, ví dụ:
  - "Chuyền nào đang gây chậm tiến độ trong tuần này?"
  - "OEE hôm nay của chuyền SMT line 1 là bao nhiêu?"
  - "Đơn hàng nào có nguy cơ trễ hạn?"

### Hành trình workshop

Xuyên suốt workshop, bạn sẽ:

- Hiểu kiến trúc end-to-end của hệ thống IMS trên AWS.
- Containerize và deploy backend Spring Boot lên ECS cùng RDS.
- Host frontend React trên S3 + CloudFront.
- Tích hợp SQS, SNS, SES cho xử lý bất đồng bộ và thông báo.
- Bảo mật secrets bằng Secrets Manager và cấu hình IAM cơ bản.
- Thiết lập CloudWatch logs, metrics, alarms và pipeline CI/CD đơn giản.

### Cấu trúc workshop

Workshop được chia thành các module bám sát kiến trúc hệ thống thực tế:

- **Architecture & IaC** - ánh xạ hệ React + Spring Boot lên AWS (CloudFront, S3, ALB, ECS, RDS, SQS/SNS/SES, Secrets Manager, CloudWatch).
- **VPC & Networking** - thiết kế VPC, subnet, routing và security group cho hệ thống.
- **Backend on ECS & RDS** - build và deploy Spring Boot API trên ECS Fargate với PostgreSQL trên RDS.
- **Frontend on S3 & CloudFront** - build và publish React SPA.
- **Messaging & Notifications** - dùng SQS/SNS/SES cho cảnh báo trễ, sự cố và email OTP.
- **Auth & Secrets** - cấu hình IAM role, SES IAM user, Secrets Manager và KMS.
- **Observability & CI/CD** - cấu hình CloudWatch logs/metrics/alarms và luồng CodeBuild/CodePipeline -> ECR -> ECS.
- **AI & Analytics** - kết nối dữ liệu sản xuất với trợ lý AI và dashboard phân tích.

Để xem đầy đủ yêu cầu nghiệp vụ và user stories chi tiết, tham khảo mục **2-Proposal**. Workshop tập trung vào cách hiện thực các yêu cầu đó bằng dịch vụ AWS.
