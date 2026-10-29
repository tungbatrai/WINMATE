# Chính sách cổng kiểm tra đề xuất

Đây là chính sách mẫu; nhóm phải điều chỉnh theo khả năng và yêu cầu thực tế. Agent review không thay thế phê duyệt của người khi chính sách yêu cầu.

| Mức | Ví dụ | Review đề xuất |
|---|---|---|
| Thấp | Tài liệu, copy không ảnh hưởng logic | Có thể không yêu cầu người khác nếu chính sách cho phép và kiểm tra đạt. |
| Trung bình | Thay đổi chức năng thông thường | Ít nhất một người có chuyên môn phù hợp. |
| Cao | Xác thực, phân quyền, thanh toán, dữ liệu nhạy cảm, migration phá hủy | Ít nhất hai người phù hợp; thêm chuyên gia bảo mật khi cần. |

Phân loại theo tác động thực tế của thay đổi, không chỉ theo tác giả hoặc tên file. Chọn mức cao nhất khi nhiều loại rủi ro cùng xuất hiện. Quyền tự phê duyệt và danh sách tác giả được tin cậy phải do nhóm quy định; không mặc định áp dụng.

## Điều kiện qua cổng

1. **Hiểu và thiết kế:** có tiêu chí nghiệm thu, phạm vi, mức rủi ro, cách kiểm tra và hoàn tác; các giả định ảnh hưởng kết quả đã được xử lý.
2. **Xây dựng:** kiểm tra liên quan đạt trên thay đổi hiện tại. Nếu không thể chạy, ghi lý do và rủi ro; người có thẩm quyền quyết định có chấp nhận ngoại lệ theo chính sách dự án hay không.
3. **Review:** finding được xử lý và có đủ phê duyệt theo mức rủi ro; finding bảo mật chưa giải quyết chặn merge. Nếu không có reviewer độc lập, ghi rõ và áp dụng chính sách của nhóm.
4. **Tích hợp:** kiểm tra bắt buộc đạt trên phiên bản dự kiến merge; có hướng dẫn phát hành, theo dõi và hoàn tác phù hợp. Không coi việc viết tài liệu là đã phát hành.

## Thiết lập thực tế

- Cấu hình bảo vệ nhánh hoặc ruleset: yêu cầu các kiểm tra CI, số người phê duyệt và chủ sở hữu đường dẫn phù hợp với nền tảng Git.
- Tạo CI chạy lint, kiểm tra kiểu, test, build và quét bảo mật phù hợp với stack; chỉ đánh dấu bắt buộc các kiểm tra đã cấu hình và chạy được.
- Nếu nền tảng hỗ trợ, dùng merge queue hoặc cập nhật nhánh và chạy lại kiểm tra trên tổ hợp sẽ merge.
- Dùng feature flag, phát hành dần, giám sát và rollback khi hệ thống hỗ trợ; ghi người phụ trách và cách kiểm chứng sau phát hành.
- Ghi nhận sự cố và false positive làm dữ liệu cải thiện review; không khẳng định hiệu quả nếu chưa đo.
