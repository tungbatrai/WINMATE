# Tiêu chí review

Review dựa trên yêu cầu, diff và ngữ cảnh code liên quan. Ưu tiên lỗi có thể gây sai hành vi, mất dữ liệu, lộ dữ liệu, gián đoạn hoặc khó hoàn tác.

## Kiểm tra
- Hành vi có đáp ứng tiêu chí nghiệm thu và giữ tương thích cần thiết không?
- Đầu vào bất thường, lỗi phụ thuộc, đồng thời, retry và dữ liệu cũ được xử lý thế nào khi liên quan?
- Quyền, xác thực, dữ liệu nhạy cảm và ranh giới tin cậy có được bảo vệ không?
- Test có kiểm tra hành vi quan trọng và trường hợp thất bại không? Bằng chứng có khớp phiên bản thay đổi không?
- Có thay đổi thừa, phụ thuộc không cần thiết hoặc tác động vận hành khó đảo ngược không?

## Cách ghi finding

Ghi mức độ, file và dòng, điều kiện kích hoạt, tác động cụ thể và đề xuất nếu rõ. Phân biệt lỗi mới với vấn đề có sẵn; nhận xét phong cách chỉ nêu khi ảnh hưởng đáng kể. Không khẳng định lỗi khi thiếu bằng chứng: ghi giả thuyết và cách kiểm tra.

Mỗi finding phải được sửa, bác bỏ kèm lý do, hoặc được người có thẩm quyền chấp nhận rủi ro theo chính sách dự án. Finding bảo mật chưa giải quyết chặn merge. Không coi sự im lặng là đã xử lý.

Review lại phần đã sửa và vùng liên quan; tránh lặp nhận xét đã giải quyết. Mặc định tối đa ba vòng review tự động để tránh lặp; nếu còn vấn đề thực chất sau ba vòng, chuyển cho người phụ trách, không tự động đánh dấu đạt.
