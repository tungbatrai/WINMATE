# Prompt dùng lại

## Agent triển khai

```text
Hãy thực hiện yêu cầu: [mô tả].
Tiêu chí nghiệm thu: [liệt kê].
Phạm vi và giới hạn: [liệt kê].

Đọc hướng dẫn dự án và code liên quan trước khi sửa. Điền hồ sơ thay đổi theo MAU-THAY-DOI.md; xác định rủi ro và cách hoàn tác. Thực hiện thay đổi nhỏ, viết test có ý nghĩa khi cần, chạy các kiểm tra phù hợp và đọc lại diff. Không tự ý thực hiện thao tác Git ghi dữ liệu hoặc phát hành khi chưa được yêu cầu. Báo file đã sửa, hành vi, lệnh và kết quả thực tế, cùng phần chưa kiểm tra.
```

## Review độc lập

```text
Bạn là reviewer độc lập. Xem yêu cầu [mô tả], tiêu chí nghiệm thu [liệt kê] và diff của thay đổi [phạm vi/phiên bản]. Đọc code liên quan để kiểm tra các lỗi có thể xảy ra theo REVIEW.md. Không giả định rằng test đã chạy hay tác giả đúng.

Báo mỗi finding với mức độ, file/dòng, điều kiện kích hoạt, tác động và bằng chứng. Phân biệt vấn đề đã có từ trước. Nếu không có finding, nói rõ và liệt kê các giới hạn kiểm tra. Không sửa code trong lượt review này.
```

## Kiểm chứng finding

```text
Kiểm tra độc lập finding sau: [finding và vị trí]. Tìm đường đi thực tế, điều kiện kích hoạt và test hoặc bằng chứng liên quan. Kết luận: xác nhận / không xác nhận / chưa đủ bằng chứng, kèm lý do. Không bỏ finding chỉ vì reviewer khác không đồng ý.
```
