---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
 **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 9:

* Xây dựng khả năng quan sát (observability) cho luồng truy cập S3 qua endpoint.
* Nâng cao kỹ năng xử lý sự cố DNS, route và permission.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Lập kế hoạch triển khai theo mục tiêu trong tuần | 02/03/2026 | 02/03/2026 | <https://docs.aws.amazon.com/vpc/latest/userguide/flow-logs.html> |
| 3 | - Thực hiện hạng mục chính và kiểm tra kết quả | 03/03/2026 | 03/03/2026 | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerLogs.html> |
| 4 | - Tiếp tục triển khai thực hành, kiểm thử và thu thập evidence | 04/03/2026 | 04/03/2026 | <https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html> |
| 5 | - Cập nhật tài liệu, tối ưu kết quả và xử lý vấn đề phát sinh | 05/03/2026 | 05/03/2026 | <https://repost.aws/knowledge-center/vpc-interface-endpoint-issues> |
| 6 | - Review cuối tuần với mentor và tổng kết bài học | 06/03/2026 | 06/03/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 9:

* Thiết lập đầy đủ lớp quan sát cho cả network path và storage access.
* Chuẩn hóa quy trình chẩn đoán lỗi endpoint theo từng nhóm nguyên nhân.
* Có dashboard và cảnh báo giúp phát hiện sớm bất thường.
* Hoàn thiện runbook xử lý sự cố với luồng thao tác lặp lại được.
* Tăng sự tự tin khi xử lý các ca gián đoạn kết nối hybrid.
