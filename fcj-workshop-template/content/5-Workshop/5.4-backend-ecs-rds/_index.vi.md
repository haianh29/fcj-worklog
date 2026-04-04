---
title: "Backend trên ECS, ECR & RDS"
weight: 3
---

# 6.3 Dịch vụ Backend trên ECS, ECR & RDS

Trong phần này, bạn sẽ tập trung đóng gói và triển khai backend Spring Boot
từ thư mục `backend/backend` lên **Amazon ECR** và **Amazon ECS (Fargate)**,
sau đó kết nối backend với cơ sở dữ liệu **Amazon RDS**.

## Tổng quan Backend Service

Backend là một ứng dụng Spring Boot cung cấp các REST API cho:

- Quản lý production orders và work orders.
- Định nghĩa production lines và công suất.
- Theo dõi tiến độ sản xuất và độ trễ.
- Cung cấp metrics cho dashboards và AI analysis endpoints.
- Gửi OTP emails và notifications thông qua SES.

Dự án sử dụng:

- Java 17
- Spring Boot
- Spring Security (phân quyền theo vai trò)
- JPA/Hibernate với Flyway database migrations

## Sơ đồ kiến trúc ECS

![High-level ECS service architecture for the IMS backend](/images/5-Workshop/5.4-backend-ecs-rds/ecs1.png)

![ECS networking with private subnets, ALB and security groups](/images/5-Workshop/5.4-backend-ecs-rds/ecs7network.png)

Những sơ đồ này tóm tắt cách backend chạy trên Fargate tasks trong private subnets, kết nối tới RDS, và được front bởi ALB.

## Containerization & Amazon ECR

1. **Tạo ECR repository** (ví dụ `ims-production`) trong AWS account/region đích.
2. Xem lại `Dockerfile` trong `backend/backend/`.
3. Build JAR bằng Maven (`./mvnw -DskipTests clean package`).
4. Đăng nhập ECR bằng AWS CLI (hoặc để CodeBuild thực hiện với `aws ecr get-login-password`).
5. Build Docker image và tag với ECR repository URI, ví dụ:
   - `638389534958.dkr.ecr.ap-southeast-1.amazonaws.com/ims-production:<git-sha>`
   - và tùy chọn `:latest`.
6. Push image lên **Amazon ECR**.

Trong workshop, quy trình này được tự động hóa bằng **AWS CodeBuild** với
file `buildspec.yml` tại root của repository:

- CodeBuild đăng nhập vào ECR.
- Build Spring Boot JAR và Docker image.
- Tag image với Git commit SHA rút gọn và `latest`.
- Push cả hai tag lên ECR repository.

## Triển khai lên ECS (Fargate)

![Creating ECS cluster and Fargate service](/images/5-Workshop/5.4-backend-ecs-rds/ecs2.png)
![Task definition with container image and CPU/memory](/images/5-Workshop/5.4-backend-ecs-rds/ecs3.png)
![Service configuration, desired count and deployment](/images/5-Workshop/5.4-backend-ecs-rds/ecs4.png)
![Load balancer integration for ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs5.png)
![Auto scaling configuration for ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs6.png)
![ALB listener and target group wired to ECS](/images/5-Workshop/5.4-backend-ecs-rds/ecs8alb.png)
![ECS service scaling policy based on CPU utilization](/images/5-Workshop/5.4-backend-ecs-rds/ecs9autoscale.png)

1. Tạo **ECS Cluster** (loại Fargate).
2. Định nghĩa **Task Definition**:
   - Container image được **pull từ ECR repository** ở trên.
   - Giới hạn CPU/Memory (ví dụ 0.5 vCPU / 1-2 GB RAM).
   - Container port (ví dụ 8080).
   - Environment variables (database URL, username, password, ...) - nên lấy từ Secrets Manager.
3. Tạo **Application Load Balancer (ALB)** và target group cho ECS service.
4. Cấu hình health checks (ví dụ `/actuator/health` nếu đã bật).
5. Tạo **ECS Service** sử dụng task definition và gắn vào ALB target group.

## Kết nối với Amazon RDS

![Amazon RDS PostgreSQL instance in private subnets](/images/5-Workshop/5.4-backend-ecs-rds/RDS.png)

1. Provision cơ sở dữ liệu **PostgreSQL** trên Amazon RDS bên trong private subnets của VPC.
2. Cấu hình Security Groups để chỉ ECS tasks (và tùy chọn bastion/administration hosts) được kết nối tới RDS.
3. Lưu database credentials trong **AWS Secrets Manager**.
4. Map secrets/environment variables vào ECS task definition:
   - `SPRING_DATASOURCE_URL`
   - `SPRING_DATASOURCE_USERNAME`
   - `SPRING_DATASOURCE_PASSWORD`
5. Xác minh Flyway migrations trong `src/main/resources/db/migration/` chạy thành công khi ứng dụng khởi động.

## Traffic Flow & Logs

Khi chạy thực tế, requests đi theo luồng:

`Client -> Route 53 -> ALB -> ECS Service (Spring Boot) -> RDS`

Logs từ container được gửi tới **CloudWatch Logs** (ví dụ log group `/ecs/ims-backend`).
Bạn có thể dùng các log này để troubleshoot lỗi và xác minh service vẫn healthy sau mỗi lần deployment.
