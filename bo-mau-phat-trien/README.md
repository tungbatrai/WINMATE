# Bộ mẫu phát triển code với AI

Bộ mẫu giúp người và agent triển khai, kiểm tra và review thay đổi theo rủi ro. Đây là quy trình đề xuất dựa trên nội dung bạn cung cấp, không phải bản sao hay xác nhận quy trình nội bộ của Anthropic.

## Bắt đầu

1. Sao chép thư mục này vào dự án. Điền thông tin thực tế vào `HUONG-DAN-AGENT.md`; nếu dự án đã có `AGENTS.md` hoặc `CLAUDE.md`, bổ sung nội dung phù hợp thay vì ghi đè.
2. Với mỗi yêu cầu, sao chép `MAU-THAY-DOI.md` thành một hồ sơ riêng và điền mục tiêu, phạm vi, rủi ro và bằng chứng.
3. Giao việc bằng prompt trong `PROMPT-AGENT.md`; sau khi triển khai, dùng prompt review độc lập trong cùng file.
4. Dùng `REVIEW.md` làm tiêu chí review và `MAU-PR.md` khi tạo pull request.
5. Cấu hình Git/CI theo `CONG-KIEM-TRA.md` nếu muốn các cổng thực sự ngăn merge.

## 16 bước, 4 cổng

| Cổng | Bước | Việc cần làm |
|---|---:|---|
| 1. Hiểu và thiết kế | 1 | Nêu vấn đề, người dùng và kết quả mong muốn. |
| | 2 | Khảo sát code, quy ước và các thay đổi liên quan. |
| | 3 | Xác định phạm vi, trường hợp biên và tiêu chí nghiệm thu. |
| | 4 | Phân loại rủi ro, chọn cách kiểm tra và phương án hoàn tác. |
| 2. Xây dựng và tự kiểm tra | 5 | Chia việc thành các thay đổi nhỏ, có thể review. |
| | 6 | Viết hoặc cập nhật test có ý nghĩa khi thay đổi hành vi. |
| | 7 | Triển khai theo quy ước, xử lý lỗi và giữ phạm vi. |
| | 8 | Chạy các kiểm tra phù hợp, ghi lệnh và kết quả thật. |
| 3. Review và bảo mật | 9 | Kiểm tra diff, hợp đồng và các đường đi thất bại. |
| | 10 | Review độc lập với ngữ cảnh mới nếu có công cụ/người phù hợp. |
| | 11 | Kiểm tra bảo mật theo dữ liệu và quyền bị ảnh hưởng. |
| | 12 | Xử lý từng finding, kiểm tra lại phần thay đổi và xác nhận số người review. |
| 4. Tích hợp và vận hành | 13 | Chạy lại kiểm tra trên phiên bản sẽ được merge. |
| | 14 | Hoàn thiện PR: bằng chứng, rủi ro và cách hoàn tác. |
| | 15 | Merge và phát hành theo chính sách của dự án; dùng flag/triển khai dần khi có. |
| | 16 | Theo dõi sau phát hành, xử lý hoặc hoàn tác khi cần; ghi lại bài học. |

Chi tiết điều kiện qua từng cổng và cách áp dụng theo rủi ro nằm trong `CONG-KIEM-TRA.md`. Không đánh dấu đạt khi kiểm tra chưa chạy hoặc không có bằng chứng.
