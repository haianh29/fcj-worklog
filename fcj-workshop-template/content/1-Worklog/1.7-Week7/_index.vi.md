---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---



### Mục tiêu tuần 7:

- Bắt đầu deploy dự án bằng các service của AWS.
- Chuẩn bị các thành phần runtime trên cloud và cấu hình triển khai cho module chính.
- Kiểm chứng luồng deploy đầu tiên và độ ổn định của môi trường.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                                      |
| --- | -------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------- |
| 2   | - Chốt kiến trúc triển khai và mapping từng module sang các service AWS phù hợp              | 16/02/2026   | 16/02/2026      | <https://docs.aws.amazon.com/whitepapers/latest/aws-overview/introduction.html>                                     |
| 3   | - Cấu hình môi trường deploy, IAM role và biến runtime cho môi trường staging                | 17/02/2026   | 17/02/2026      | <https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html>                                              |
| 4   | - Deploy phiên bản đầu tiên của dự án lên AWS và kiểm tra health check dịch vụ               | 18/02/2026   | 18/02/2026      | <https://docs.aws.amazon.com/whitepapers/latest/practicing-continuous-integration-continuous-delivery/welcome.html> |
| 5   | - Xử lý lỗi khi deploy, đồng bộ API endpoint và kiểm tra kết nối frontend-backend trên cloud | 19/02/2026   | 19/02/2026      | <https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html>                                |
| 6   | - Demo môi trường đã deploy với team và lập danh sách hardening cho tuần 8            | 20/02/2026   | 20/02/2026      | <https://cloudjourney.awsstudygroup.com/>                                                                           |

### Kết quả đạt được tuần 7:

- Hoàn thành đợt deploy đầu tiên của các thành phần dự án bằng dịch vụ AWS.
- Thiết lập đầy đủ cấu hình runtime và biến môi trường cho môi trường staging.
- Xác nhận các luồng API và UI chính hoạt động sau khi triển khai lên cloud.
- Phát hiện và xử lý các lỗi khởi đầu liên quan tới deploy/runtime.
- Chuẩn bị checklist ổn định hệ thống để tiếp tục tối ưu bảo mật và độ tin cậy ở tuần 8.
