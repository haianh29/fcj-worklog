---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---



### Mục tiêu tuần 5:

- Bắt đầu gắn các module frontend với API backend.
- Chỉnh lại UI tạm để khớp với contract request/response từ backend.
- Ổn định các luồng chính với trạng thái loading, validate và xử lý lỗi phù hợp.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc                                                                                | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                                                         |
| --- | ---------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------------------------------------------- |
| 2   | - Rà soát tài liệu API backend, danh sách endpoint và schema dữ liệu cho các luồng chính | 02/02/2026   | 02/02/2026      | <https://swagger.io/resources/articles/documenting-apis-with-swagger/> |
| 3   | - Cấu hình tầng gọi API, xử lý token xác thực và biến môi trường                         | 03/02/2026   | 03/02/2026      | <https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication>     |
| 4   | - Thay mock data bằng API thật cho các màn hình list/detail và kiểm tra mapping dữ liệu  | 04/02/2026   | 04/02/2026      | <https://react.dev/learn/synchronizing-with-effects>                   |
| 5   | - Chỉnh component UI để khớp field backend, rule validate và format lỗi trả về           | 05/02/2026   | 05/02/2026      | <https://json-schema.org/learn/getting-started-step-by-step>           |
| 6   | - Chạy các kịch bản kiểm thử tích hợp, tổng hợp lỗi và lập kế hoạch fix cho tuần 6       | 06/02/2026   | 06/02/2026      | <https://cloudjourney.awsstudygroup.com/>                              |

### Kết quả đạt được tuần 5:

- Gắn được các luồng frontend chính với API backend và xác nhận dữ liệu đi/đến đúng.
- Thay thế phần lớn mock data bằng request API thật trên các màn hình trọng tâm.
- Cập nhật form, bảng và chi tiết hiển thị để khớp contract backend và logic validate.
- Bổ sung trạng thái loading, empty-state và error-state cho các màn hình quan trọng.
- Tổng hợp danh sách lỗi và backlog cải tiến cho vòng phát triển tiếp theo.
