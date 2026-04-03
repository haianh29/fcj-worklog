---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Bắt đầu vòng test tổng thể đầu tiên sau khi dự án đã deploy.
- Tìm và fix các lỗi ưu tiên cao trong những luồng nghiệp vụ chính theo vai trò.
- Đồng bộ hành vi API và UI dựa trên kết quả kiểm thử thực tế.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                         | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                                             |
| --- | --------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------ |
| 2   | - Lập test plan, test case và tiêu chí nghiệm thu cho các luồng quan trọng        | 23/02/2026   | 23/02/2026      | <https://www.atlassian.com/continuous-delivery/software-testing/types-of-software-testing> |
| 3   | - Chạy test functional và integration cho authentication và module theo role      | 24/02/2026   | 24/02/2026      | <https://www.postman.com/api-platform/api-testing/>                                        |
| 4   | - Phân loại lỗi, tái hiện issue và ưu tiên fix các lỗi mức nghiêm trọng cao       | 25/02/2026   | 25/02/2026      | <https://martinfowler.com/articles/nonDeterminism.html>                                    |
| 5   | - Re-test các lỗi đã fix và chạy regression có trọng tâm trên module bị ảnh hưởng | 26/02/2026   | 26/02/2026      | <https://playwright.dev/docs/intro>                                                        |
| 6   | - Review số liệu lỗi với mentor/team và lập backlog bug cho tuần 9                | 27/02/2026   | 27/02/2026      | <https://cloudjourney.awsstudygroup.com/>                                                  |

### Kết quả đạt được tuần 8:

- Hoàn thành vòng test end-to-end đầu tiên cho các module đã triển khai.
- Fix được các lỗi chặn luồng chính liên quan login, điều hướng theo role và mapping dữ liệu API.
- Cải thiện thông báo validate và trạng thái fallback UI dựa trên lỗi thực tế.
- Thiết lập file tracking bug có severity, trạng thái và ghi chú nguyên nhân gốc.
- Tạo backlog lỗi ưu tiên rõ ràng cho sprint kiểm thử kế tiếp.
