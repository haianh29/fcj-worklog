---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Tiếp tục kiểm thử với vòng regression sâu hơn cho các tính năng đã fix và mới tích hợp.
- Tập trung test edge case, biên quyền truy cập và tình huống dữ liệu không hợp lệ.
- Giảm tỷ lệ lỗi reopen bằng cách fix theo nguyên nhân gốc.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                        | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                             |
| --- | ------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------------------------------------------------------------------- |
| 2   | - Chạy full regression cho các luồng admin, manager và line leader                               | 02/03/2026   | 02/03/2026      | <https://www.browserstack.com/guide/regression-testing>                    |
| 3   | - Thực hiện negative test và boundary test quyền truy cập (token hết hạn, payload lỗi, sai role) | 03/03/2026   | 03/03/2026      | <https://owasp.org/www-project-web-security-testing-guide/>                |
| 4   | - Fix các lỗi mức trung bình/cao và refactor logic chưa ổn định gây lỗi lặp                      | 04/03/2026   | 04/03/2026      | <https://refactoring.guru/refactoring>                                     |
| 5   | - Kiểm tra lại trên staging và chạy smoke test sau mỗi lần cập nhật deploy                       | 05/03/2026   | 05/03/2026      | <https://learn.microsoft.com/en-us/azure/devops/pipelines/test/smoke-test> |
| 6   | - Tổng hợp chỉ số chất lượng và chốt danh sách hardening cho tuần 10                             | 06/03/2026   | 06/03/2026      | <https://cloudjourney.awsstudygroup.com/>                                  |

### Kết quả đạt được tuần 9:

- Mở rộng độ bao phủ regression và giảm đáng kể số lỗi bị reopen.
- Xử lý các lỗi phân quyền và session trong các luồng theo vai trò.
- Đồng bộ tốt hơn giữa format lỗi từ backend và cách hiển thị ở frontend.
- Ổn định các user journey chính trên staging sau nhiều vòng smoke/regression.
- Hoàn thiện danh sách known issues kèm hành động phòng ngừa cho sprint tiếp theo.
