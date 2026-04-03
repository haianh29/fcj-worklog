---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}}
 **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 8:

* Áp dụng endpoint policy và bucket policy theo nguyên tắc least privilege.
* Kiểm chứng cơ chế deny-by-default và chỉ mở đúng quyền cần thiết.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | - Lập kế hoạch triển khai theo mục tiêu trong tuần | 23/02/2026 | 23/02/2026 | <https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_evaluation-logic.html> |
| 3 | - Thực hiện hạng mục chính và kiểm tra kết quả | 24/02/2026 | 24/02/2026 | <https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html> |
| 4 | - Tiếp tục triển khai thực hành, kiểm thử và thu thập evidence | 25/02/2026 | 25/02/2026 | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies-vpc-endpoint.html> |
| 5 | - Cập nhật tài liệu, tối ưu kết quả và xử lý vấn đề phát sinh | 26/02/2026 | 26/02/2026 | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-policy-language-overview.html> |
| 6 | - Review cuối tuần với mentor và tổng kết bài học | 27/02/2026 | 27/02/2026 | <https://docs.aws.amazon.com/whitepapers/latest/security-overview-amazon-s3/iam-policies.html> |

### Kết quả đạt được tuần 8:

* Triển khai được bộ endpoint policy và bucket policy theo least privilege.
* Kiểm chứng được cơ chế deny-by-default và các ngoại lệ hợp lệ.
* Có bộ test scenario lặp lại được cho nhiều vai trò truy cập.
* Giảm sự trùng lặp policy nhờ gom nhóm statement tái sử dụng.
* Hoàn thành gói policy sẵn sàng cho bước review cuối.
