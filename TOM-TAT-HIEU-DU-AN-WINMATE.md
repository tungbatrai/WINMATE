# Tóm tắt cách hiểu dự án WINMATE

Ngày tổng hợp: 29/10/2026

## 1. WINMATE cần giải quyết vấn đề gì?

WINMATE là phần mềm cho doanh nghiệp tạo và vận hành các **trợ lý tự động**. Mỗi trợ lý thực chất là một workflow gồm nhiều bước: nhận sự kiện hoặc yêu cầu, lấy dữ liệu, dùng AI hoặc gọi phần mềm khác, xử lý điều kiện, chờ người duyệt và thực hiện hành động.

Người dùng có thể trò chuyện với Agent bằng ngôn ngữ tự nhiên để chạy hoặc dựng trợ lý, tự thiết kế workflow trên giao diện, hoặc cài trợ lý mẫu từ kho. Doanh nghiệp quản lý chung kết nối, máy chạy, tệp, thành viên, quyền và gói dịch vụ.

**Cách hiểu cốt lõi:** sản phẩm cần cả giao diện quản lý lẫn hệ thống thực thi workflow thực tế, kết nối với ứng dụng bên ngoài, theo dõi trạng thái và xử lý gián đoạn. Bản HTML hiện có là prototype mô phỏng, chưa thể xem là sản phẩm hoàn chỉnh.

## 2. Nguồn tài liệu và cách ưu tiên

- `WINMATE-chuc-nang-v1.3.docx`, ngày 28/10/2026: đặc tả chức năng cho dev và QA, bao gồm màn 1A–8D, 17 loại node, quy tắc chạy, phân quyền, tiêu chí nghiệm thu và mô hình dữ liệu. **Khi tài liệu và prototype khác nhau, ưu tiên tài liệu**; trong tài liệu, quyết định mới hơn thay quyết định cũ.
- `WINMATE_Prototype_Final_v25.18.html`: prototype giao diện đi cùng đặc tả. Theo chính phụ lục B của tài liệu, các màn chưa dùng dữ liệu chung và nhiều hành vi chỉ được mô phỏng.
- `target.txt`: có liên kết tới bảng `WINMATE_Backlog_Stories_Tasks_Estimate_v1.1_2h_per_SP.xlsm` trên Google Drive. Đã xác định đây là bảng backlog/ước lượng; nội dung các sheet chưa được đọc, nên bản tóm tắt này chưa kết luận về tiến độ, thứ tự ưu tiên hay ước lượng dự án.

Đây là bản diễn giải tổng quan để đối chiếu cách hiểu; khi xây dựng và nghiệm thu từng tính năng vẫn cần dùng đặc tả gốc, đặc biệt các bảng hành vi, quyền và tiêu chí nghiệm thu.

## 3. Những phần sản phẩm cần có

| Khu vực | Nhu cầu chính |
| --- | --- |
| 1A–1B · Trò chuyện | Chat với Agent; chọn engine/model; đưa tệp, thư mục, skill, connector vào ngữ cảnh; chạy trợ lý được cấp quyền; tạo trợ lý nháp bằng chat; quản lý cuộc trò chuyện. |
| 2A–2C · Trợ lý | Danh sách, tạo, bật/tắt, chạy tay; trình tạo workflow trên canvas; cấu hình từng bước, biến, nơi chạy; có chat AI hỗ trợ sửa bản nháp; lưu, chạy thử và kích hoạt. |
| 3A–3B · Kho trợ lý | Xem và cài mẫu từ WINMATE hoặc đối tác; ghép các khả năng cần thiết với kết nối, dữ liệu, người duyệt và cấu hình của doanh nghiệp. |
| 4A · Lịch sử chạy | Theo dõi từng lượt và từng bước, dữ liệu, lỗi, duyệt, hàng chờ máy tắt; chạy lại, huỷ, xem các webhook không tạo lượt. |
| 5A–5L · Kết nối | Thêm, kiểm tra, cấu hình và phân quyền kết nối AI, ứng dụng và webhook; quản lý hành động đọc/ghi, giới hạn gọi, khoá và phạm vi sử dụng. |
| 6A · Thư mục dùng chung | Quản lý thư mục và tệp, nơi lưu, thao tác tải lên/tải về/chuyển/xoá, thùng rác và quyền theo nhóm. |
| 7A · Gói & ví | Quản lý hạn mức, tiền trong ví, nạp tiền, lịch sử giao dịch, mua thêm và gia hạn; xử lý hết hạn và ân hạn. |
| 8A–8D · Thành viên | Mời, khoá, xoá thành viên; quản lý nhóm, vai trò và quyền riêng; chuyển người sở hữu trợ lý khi cần. |

## 4. Workflow và các loại bước

Mỗi trợ lý có đúng một cách kích hoạt tự động: webhook, lịch, từ trò chuyện hoặc được trợ lý khác gọi; ngoài ra có thể chạy tay. Bước đầu luôn là Kích hoạt. Đầu ra của bước trước trở thành biến cho các bước sau.

17 loại node theo đặc tả:

1. Kích hoạt.
2. Lark CLI, Facebook CLI, Facebook MCP, Pancake MCP, POSCake MCP, HTTP Request.
3. Claude Code, Codex, Claude API, OpenAI API.
4. Trợ lý, Nếu / Nếu không, Nhiều nhánh, Vòng lặp, Chờ người duyệt, Chờ một khoảng thời gian.

Các node dữ liệu chỉ thêm được khi đã có kết nối phù hợp và người dùng có quyền; chỉ chọn được hành động đang bật. Node logic luôn có. Có thể đổi loại trong cùng nhóm theo quy tắc R14; dấu `+` dùng để chèn node mới. Nhánh, vòng lặp, gọi trợ lý con và các bước chờ cần được hệ thống thực thi, không chỉ vẽ trên canvas.

Bản nháp và phiên bản đang chạy được quản lý riêng. Chạy thử thực hiện thật các bước đọc; mỗi bước ghi hỏi người chạy có thực hiện thật hay bỏ qua. Bước lỗi thông thường dừng lượt và báo lỗi, không tự thử lại để tránh ghi trùng. Duyệt nghiệp vụ được cấu hình bằng node Chờ người duyệt; nếu nội dung đã duyệt thay đổi thì phải duyệt lại.

## 5. Hai nơi chạy và xử lý máy tắt

Mỗi trợ lý chọn một nơi chạy rõ ràng:

- **Desktop:** chạy trên máy được chọn có app WINMATE Desktop đang mở. Các node Claude Code/Codex dùng gói tháng chỉ chạy ở đây; tài khoản gói tháng gắn với người đăng nhập trên máy.
- **WINMATE:** chạy trên server, phù hợp vận hành liên tục; cần quyền tạo trợ lý chạy trên WINMATE và còn suất. Không dùng được Claude Code/Codex gói tháng hoặc kết nối chỉ chạy trên Desktop.

Vị trí gọi Claude API/OpenAI API phụ thuộc nơi lưu key: key trong Kho khoá thì gọi từ server, kể cả workflow Desktop; key “Chỉ máy này” thì gọi từ máy. Không tự đổi nơi chạy, máy hay loại key khi xảy ra sự cố.

Server vẫn giữ lịch và nhận webhook cho trợ lý Desktop. Khi máy mất tín hiệu quá 2 phút, hệ thống ghi lỗi “Máy tắt”, thông báo người sở hữu và giữ các lượt đủ điều kiện trong hàng chờ tối đa 24 giờ, 3 ngày hoặc 7 ngày theo cấu hình. Webhook đã nhận trong trường hợp này trả 202. Khi máy trở lại, lượt được tiếp tục theo thứ tự, giữ nguyên số lượt và phiên bản lúc phát sinh; các bước đã hoàn thành không chạy lại. Quá hạn thì huỷ lượt chờ, giữ dữ liệu để xem/chạy tay. Riêng yêu cầu từ chat khi máy tắt phải hỏi trước khi đưa vào hàng chờ.

Các lượt của cùng một trợ lý được xếp hàng lần lượt; lượt đang chờ duyệt hoặc chờ thời gian không chiếm chỗ xử lý. Tài liệu quy định hàng đợi không giới hạn. Giới hạn chạy song song của máy áp dụng cho số trợ lý khác nhau cùng chạy trên máy.

## 6. Kết nối, bảo mật và quyền

Có sáu nhóm kết nối: ứng dụng Desktop, AI API, MCP, CLI, HTTP Request API và webhook. Webhook thuộc tài khoản người dùng, được quản lý trong Kết nối và có thể dùng cho nhiều trợ lý được cấp quyền; điều kiện lọc được xét riêng cho từng trợ lý. HTTP node chọn endpoint đã khai báo và bật trong kết nối, không nhập URL tự do trong node.

Hành động được phân loại đọc/ghi; hành động ghi mặc định tắt. Ngoài node duyệt nghiệp vụ, đặc tả còn giữ lựa chọn **hỏi người tạo ở lần chạy đầu** đối với hành động ghi theo R12; cần thực hiện đúng điều kiện và phạm vi cho phép trong phần Kết nối, không coi đây là cùng một cơ chế với node duyệt.

Quyền gồm ba lớp: vai trò cho quyền chung, nhóm cho quyền mặc định trên tài nguyên, và quyền riêng từng người. Quyền riêng ưu tiên; nếu thuộc nhiều nhóm thì lấy mức cao nhất theo từng tài nguyên. Trợ lý có các mức Không / Xem / Dùng / Sửa; kết nối có Quản lý / Dùng / Dùng – chỉ Đọc / Không được dùng. Phạm vi có thể giới hạn theo Trang, tài khoản quảng cáo, Base hoặc cửa hàng. Người phân quyền không được cấp cao hơn quyền của mình.

Mỗi trợ lý luôn có đúng một người sở hữu để chịu trách nhiệm và nhận thông báo lỗi. Khoá và token không hiển thị trong node; thông tin xác thực cần được lưu mã hoá theo nơi lưu đã chọn. Kết nối gói tháng là riêng của người đăng nhập, không chia sẻ như kết nối thông thường.

## 7. Mô hình kinh doanh và giới hạn

Phí/hạn mức được tính theo số trợ lý **đang bật đồng thời**, tách riêng Desktop và WINMATE; không tính theo số lượt chạy. Các thành phần khác gồm số thành viên và dung lượng thư mục trên WINMATE. Chạy thử, chạy tay trợ lý đang tắt và bản nháp không chiếm suất trợ lý đang bật.

Khi hết suất ở một nơi chạy, không bật thêm trợ lý ở nơi đó; các trợ lý đang chạy không bị dừng chỉ vì đạt hạn mức. Gói mặc định tự gia hạn từ số dư nếu đủ tiền; khi không gia hạn được có 3 ngày ân hạn. Sau ân hạn, trợ lý tự tắt, chặn lượt mới; lượt đang thực thi chạy nốt, lượt chờ không tiếp tục cho đến khi gia hạn. Dữ liệu và lịch sử vẫn được giữ; sau gia hạn cần bật lại trợ lý bằng tay.

## 8. Các luồng tiêu biểu cần hoạt động xuyên suốt

1. Quản trị viên tạo kết nối, kiểm tra xác thực, bật hành động và cấp quyền phù hợp.
2. Người tạo dựng trợ lý bằng canvas, chat hoặc cài từ kho; chọn kích hoạt, nơi chạy, kết nối, biến và người duyệt.
3. Người tạo chạy thử, kiểm tra từng bước và xác nhận hành động ghi; sau đó lưu/kích hoạt nếu đủ quyền và hạn mức.
4. Sự kiện webhook, lịch, chat, lượt chạy tay hoặc lời gọi từ trợ lý khác tạo lượt; hệ thống xếp hàng và thực thi theo phiên bản tương ứng.
5. Khi đến bước duyệt hoặc chờ, lượt tạm dừng và tiếp tục theo kết quả; khi lỗi thì ghi lịch sử và thông báo người sở hữu.
6. Nếu máy Desktop gián đoạn, server giữ lượt theo thời hạn; khi máy mở lại tiếp tục và lưu dấu vết trong lịch sử.
7. Quản trị viên theo dõi kết quả, quản lý quyền, thành viên, dung lượng và gói dịch vụ.

## 9. Dữ liệu và thành phần cần có — suy luận từ đặc tả

Đây là cách phân nhóm để hiểu khối lượng công việc, chưa phải quyết định công nghệ hay thiết kế kiến trúc đã chốt:

- Giao diện web và ứng dụng desktop; hệ thống tài khoản/doanh nghiệp và phân quyền.
- Bộ quản lý workflow, phiên bản, node, biến và cơ chế chạy thử.
- Bộ điều phối lượt chạy, lịch, webhook, hàng đợi, trạng thái chờ, phục hồi khi máy tắt và nhật ký chi tiết.
- Quản lý kết nối, thông tin xác thực, phạm vi và giới hạn gọi; các tích hợp AI, Lark, Facebook, Pancake, POSCake, HTTP, MCP và CLI theo đặc tả.
- Dịch vụ duyệt và thông báo qua các kênh được cấu hình; quản lý tệp và nơi lưu.
- Quản lý kho mẫu, cài đặt mẫu, thành viên, nhóm, vai trò, gói, ví và giao dịch.

Phụ lục A của tài liệu gốc liệt kê các bảng dữ liệu chính và quy định liên kết bằng ID. Các nhóm trên không đồng nghĩa tài liệu đã chọn sẵn framework, ngôn ngữ, cơ sở dữ liệu hay phương án triển khai.

## 10. Giới hạn của bản prototype và điểm cần làm rõ khi triển khai

Theo phụ lục B, prototype v25.18 chưa chia sẻ dữ liệu giữa các màn; nhiều luồng chỉ giả lập, trong đó kiểm tra khoá dựa trên định dạng, QR minh hoạ và gửi chat là demo. Canvas còn hạn chế về node mới, nhánh và kéo thả; một số trạng thái gói, phân quyền và nơi xem/thu hồi quyền ghi chưa được mô phỏng đầy đủ. Vì vậy cần xem đặc tả gốc là cơ sở cho các phần prototype chưa thể hiện.

Các nội dung sau chưa được xác định đầy đủ từ phần đã khảo sát và cần đối chiếu thêm trước khi chốt kế hoạch kỹ thuật:

- Phạm vi bản phát hành đầu, thứ tự ưu tiên, nhân sự, tiến độ và ước lượng: cần đọc và đối chiếu bảng backlog liên kết.
- Công nghệ, kiến trúc triển khai, hạ tầng, môi trường và quy trình vận hành thực tế.
- Các chỉ tiêu phi chức năng cụ thể như tải, độ sẵn sàng, sao lưu, phục hồi, lưu trữ và kiểm thử bảo mật; tài liệu đã có một số quy tắc nghiệp vụ cụ thể nhưng không nên tự suy ra các chỉ tiêu còn thiếu.
- Chi tiết tích hợp thực tế, điều kiện tài khoản/giấy phép và môi trường thử nghiệm cho từng dịch vụ bên ngoài.

**Đánh giá mức độ hiểu:** đã nắm mục tiêu, phạm vi chức năng và các quy tắc vận hành quan trọng để trao đổi và phân tích tiếp. Chưa đủ cơ sở kết luận tiến độ hoặc chốt kiến trúc, và bản tóm tắt không thay thế tiêu chí nghiệm thu chi tiết trong tài liệu v1.3.
