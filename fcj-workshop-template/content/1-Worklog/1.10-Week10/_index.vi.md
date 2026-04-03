---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

- Triển khai kiểm thử hiệu năng và độ ổn định cho các luồng quan trọng của dự án.
- Phát hiện và xử lý các điểm nghẽn ảnh hưởng thời gian phản hồi và trải nghiệm người dùng.
- Nâng độ tin cậy hệ thống dưới tải thực tế và số lượng request lớn hơn.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                       | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                                  |
| --- | ------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------------------------------------------------------------- |
| 2   | - Thiết kế kịch bản test hiệu năng, ngưỡng mục tiêu và baseline ban đầu         | 09/03/2026   | 09/03/2026      | <https://k6.io/docs/testing-guides/test-types/>                                                 |
| 3   | - Chạy load/stress test cho API trọng yếu và thu thập metric latency/error rate | 10/03/2026   | 10/03/2026      | <https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/welcome.html> |
| 4   | - Fix điểm nghẽn backend (đường truy vấn, timeout handling, chiến lược retry)   | 11/03/2026   | 11/03/2026      | <https://martinfowler.com/bliki/CircuitBreaker.html>                                            |
| 5   | - Tối ưu rendering frontend và cập nhật state trên các màn hình dữ liệu lớn     | 12/03/2026   | 12/03/2026      | <https://web.dev/performance-scoring/>                                                          |
| 6   | - Benchmark lại, so sánh số liệu trước/sau và tổng hợp báo cáo cải thiện        | 13/03/2026   | 13/03/2026      | <https://cloudjourney.awsstudygroup.com/>                                                       |

### Kết quả đạt được tuần 10:

- Hoàn thành các vòng test hiệu năng và ổn định cho module trọng tâm.
- Giảm thời gian phản hồi API chính và cải thiện tỷ lệ lỗi khi tải tăng cao.
- Khắc phục lỗi timeout/retry, nâng khả năng chịu lỗi cho các tình huống không ổn định.
- Tối ưu hiển thị frontend ở màn hình list/detail khi dữ liệu lớn.
- Có bộ benchmark trước/sau thể hiện rõ hiệu quả cải tiến.
