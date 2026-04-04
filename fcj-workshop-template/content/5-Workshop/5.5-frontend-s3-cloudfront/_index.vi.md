---
title: "Frontend với S3 & CloudFront"
weight: 4
---

# 6.4 Lưu trữ Frontend với S3 & CloudFront

Phần này trình bày cách build và triển khai frontend React từ thư mục `frontend/`
bằng Amazon S3 và Amazon CloudFront.

## Sơ đồ kiến trúc frontend

![S3 bucket for hosting IMS frontend static website](/images/5-Workshop/5.5-frontend-s3-cloudfront/s3.png)

![CloudFront distribution in front of S3 origin](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront.png)
![CloudFront behavior and cache settings](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront1.png)
![CloudFront distribution details and domain name](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront2.png)

Các sơ đồ này minh họa cách người dùng truy cập ứng dụng React qua CloudFront, trong đó nội dung tĩnh được phục vụ từ S3 bucket.

## Năng lực Frontend

Ứng dụng React cung cấp các luồng UI cho:

- Đăng nhập người dùng và điều hướng theo vai trò (Admin / Manager / Line Leader).
- Quản lý đơn sản xuất và xem chi tiết đơn.
- Theo dõi kế hoạch sản xuất, lịch của chuyền và dashboard cơ bản.
- Truy cập các trang AI insights (qua `aiService`) để xem tóm tắt và phân tích sản xuất.

## Build Frontend

1. Cài dependencies ở máy local:
   - `npm install`
2. Cấu hình API base URL (ví dụ dùng biến môi trường `VITE_API_BASE_URL`).
3. Build production bundle:
   - `npm run build`
4. Xác minh thư mục `dist/` (hoặc tương đương) được tạo với các static files.

## Host trên Amazon S3

1. Tạo một S3 bucket chuyên dùng để host frontend (ví dụ `ims-frontend-prod`).
2. Bật static website hosting (hoặc dùng CloudFront origin access control cho private bucket).
3. Upload toàn bộ nội dung thư mục `dist/` lên S3 bucket.
4. Cấu hình index document (ví dụ `index.html`) và error document cho SPA routing.

## Phân phối qua CloudFront

1. Tạo **CloudFront distribution** với S3 bucket làm origin.
2. Đặt default root object là `index.html`.
3. Cấu hình caching và custom error responses cho SPA (trả về `index.html` khi 404).
4. Gắn **ACM certificate** và custom domain (qua Route 53) nếu dùng HTTPS.

## API Integration & CORS

- Đảm bảo frontend gọi backend API bằng base URL chính xác (ALB DNS hoặc custom domain).
- Cấu hình CORS ở backend (và/hoặc ALB) để cho phép CloudFront domain.
- Với production, tránh hard-code URLs; dùng biến môi trường trong lúc build.

Kết thúc phần này, React frontend sẽ truy cập được qua CloudFront URL hoặc custom domain,
đóng vai trò entrypoint chính của hệ thống IMS.
