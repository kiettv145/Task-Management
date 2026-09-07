# SYSTEM REQUIREMENTS SPECIFICATION (TASK 1)
**Project:** Task Management System

---

## 1. YÊU CẦU CHỨC NĂNG (FUNCTIONAL REQUIREMENTS - FR)

* **FR-01 (Đăng ký/Đăng nhập):** Hệ thống cho phép người dùng đăng ký tài khoản mới và đăng nhập bằng Email/Password hoặc Google OAuth.
* **FR-02 (Tạo & Quản lý Task):** Hệ thống cho phép người dùng tạo công việc mới bao gồm các thông tin: Tên task, Mô tả, Hạn hoàn thành (Deadline), Mức độ ưu tiên (`LOW`, `MEDIUM`, `HIGH`), Người thực hiện (Assignee) và Nhãn (Tag).
* **FR-03 (Bảng Kanban):** Hệ thống cho phép người dùng cập nhật trạng thái công việc (`TO_DO`, `IN_PROGRESS`, `DONE`) bằng thao tác kéo thả các thẻ task trên bảng Kanban.
* **FR-04 (Phân công nhiệm vụ):** Hệ thống cho phép Trưởng nhóm gán/đổi người thực hiện công việc. Chỉ những người thuộc danh sách thành viên dự án mới được phép gán.
* **FR-05 (Tìm kiếm & Lọc):** Hệ thống cho phép người dùng tìm kiếm task theo từ khóa và lọc task theo trạng thái, mức độ ưu tiên hoặc người thực hiện.

---

## 2. YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS - NFR)

### 2.1. Danh sách các yêu cầu phi chức năng

1. **NFR-PERF-01:** Thời gian đáp ứng của chức năng tải bảng Kanban.
2. **NFR-SEC-01:** Bảo mật thông tin mật khẩu và mã hóa dữ liệu người dùng.
3. **NFR-SEC-02:** Ràng buộc giới hạn tần suất gọi API (Rate Limiting) phòng chống tấn công.
4. **NFR-REL-01:** Độ sẵn sàng và khả năng hoạt động liên tục của hệ thống.

---

### 2.2. Đặc tả chi tiết từng yêu cầu phi chức năng

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-PERF-01 |
| **Loại** | Performance Efficiency |
| **Mô tả** | Thời gian đáp ứng khi tải và thao tác kéo thả trên bảng Kanban |
| **Nguồn** | Biên bản họp thống nhất hiệu năng hệ thống |
| **Thang đo** | Thời gian từ lúc người dùng thao tác đến khi giao diện Kanban cập nhật xong (giây) |
| **Tiêu chí** | $P_{95} \le 2\text{s}$ (ít nhất 95% request được xử lý trong vòng 2 giây) khi có 500 người dùng đồng thời, CSDL có 100.000 tasks |
| **Cách đo** | Kịch bản JMeter chạy 15 phút trên môi trường Staging |
| **Độ ưu tiên** | Must have |
| **Liên quan** | FR-03 (Bảng Kanban) |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-SEC-01 |
| **Loại** | Security |
| **Mô tả** | Cơ chế lưu trữ mật khẩu an toàn và mã hóa luồng dữ liệu |
| **Nguồn** | Tiêu chuẩn an toàn thông tin OWASP Top 10 |
| **Thang đo** | Thuật toán mã hóa mật khẩu và giao thức kết nối mạng |
| **Tiêu chí** | Mật khẩu mã hóa bằng `bcrypt` (Cost factor $\ge 12$). Toàn bộ kết nối API bắt buộc dùng HTTPS (TLS 1.3). Tự động khóa tài khoản 15 phút nếu nhập sai 5 lần. |
| **Cách đo** | Kiểm tra mã nguồn (Static Code Analysis) và quét lỗ hổng bằng OWASP ZAP |
| **Độ ưu tiên** | Must have |
| **Liên quan** | FR-01 (Đăng ký/Đăng nhập) |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-SEC-02 |
| **Loại** | Security & Resiliency |
| **Mô tả** | Giới hạn tần suất gửi yêu cầu để chống tấn công từ chối dịch vụ (DDoS) |
| **Nguồn** | Tài liệu thiết kế kiến trúc Backend |
| **Thang đo** | Số lượng request tối đa được chấp nhận trong một khoảng thời gian |
| **Tiêu chí** | Tối đa 100 requests / 1 phút cho mỗi địa chỉ IP. Vượt quá ngưỡng trả về lỗi HTTP 429 (Too Many Requests). |
| **Cách đo** | Chạy script tự động gửi 150 requests/phút từ một IP và kiểm tra phản hồi HTTP |
| **Độ ưu tiên** | Should have |
| **Liên quan** | Toàn bộ các yêu cầu FR |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-REL-01 |
| **Loại** | Reliability & Availability |
| **Mô tả** | Mức độ sẵn sàng phục vụ của hệ thống quản lý công việc |
| **Nguồn** | Cam kết chất lượng dịch vụ (SLA) với khách hàng |
| **Thang đo** | Tỷ lệ phần trăm thời gian hệ thống hoạt động bình thường trong tháng |
| **Tiêu chí** | Uptime $\ge 99.5\%$/tháng (thời gian gián đoạn tối đa không quá 3.6 giờ/tháng, không tính lịch bảo trì định kỳ) |
| **Cách đo** | Theo dõi bằng công cụ UptimeRobot / Datadog trong 30 ngày |
| **Độ ưu tiên** | Must have |
| **Liên quan** | Toàn bộ hệ thống |

---

## 3. YÊU CẦU CHỨC NĂNG KHÔNG TƯƠNG TÁC (NON-INTERACTIVE FUNCTIONAL REQUIREMENTS - NIFR)

### 3.1. Danh sách các yêu cầu chức năng không tương tác

1. **NIFR-01:** Tự động gửi email nhắc hạn công việc (Task Deadline Reminder).
2. **NIFR-02:** Tự động cập nhật trạng thái Task cha khi các Sub-tasks hoàn thành.
3. **NIFR-03:** Tự động ghi nhật ký hệ thống (Audit Log) cho các thao tác dữ liệu.

---

### 3.2. Đặc tả chi tiết từng yêu cầu chức năng không tương tác

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NIFR-01 |
| **Tên** | Gửi email nhắc hạn công việc (Task Deadline Reminder) |
| **Loại** | Chức năng theo lịch (Temporal) |
| **Điều kiện kích hoạt** | `00:00` hằng ngày (Múi giờ UTC+7) |
| **Điều kiện tiền đề** | Tồn tại công việc có trạng thái khác `DONE` và chưa hoàn thành. |
| **Hành vi** | 1. Quét toàn bộ bảng dữ liệu công việc (`Tasks`).<br>2. Chọn các công việc có hạn hoàn thành (`due_date`) trong vòng 24 giờ tới hoặc đã quá hạn.<br>3. Sinh email nhắc nhở theo mẫu HTML tương ứng.<br>4. Gửi qua dịch vụ SMTP và ghi nhật ký kết quả. |
| **Kết quả** | Mỗi thành viên nhận tối đa 1 email/ngày; Nhật ký được lưu vết đầy đủ. |
| **Xử lý ngoại lệ** | Nếu SMTP lỗi, hệ thống thử lại tối đa 3 lần cách nhau 10 phút; sau đó ghi cảnh báo cho quản trị viên. |
| **Cách kiểm thử** | Giả lập đồng hồ hệ thống về `00:00`, tạo dữ liệu mẫu, kiểm tra hàng đợi email và bản ghi nhật ký. |
| **Độ ưu tiên** | Should have |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NIFR-02 |
| **Tên** | Tự động cập nhật trạng thái công việc cha |
| **Loại** | Quy tắc nghiệp vụ (Business Rule Driven) |
| **Điều kiện kích hoạt** | Trạng thái của một Sub-task thuộc Task cha được chuyển sang `DONE` |
| **Điều kiện tiền đề** | Task cha đang ở trạng thái `TO_DO` hoặc `IN_PROGRESS` và có chứa Sub-tasks. |
| **Hành vi** | 1. Hệ thống kiểm tra trạng thái của tất cả các Sub-tasks còn lại thuộc Task cha đó.<br>2. Nếu $100\%$ các Sub-tasks đều có trạng thái `DONE`, tự động chuyển trạng thái Task cha sang `DONE`.<br>3. Gửi thông báo đến người quản lý dự án (Project Manager). |
| **Kết quả** | Trạng thái Task cha được cập nhật chính xác trên bảng Kanban mà không cần thao tác thủ công. |
| **Xử lý ngoại lệ** | Nếu có lỗi DB transaction khi update Task cha, rollback trạng thái Sub-task và hiển thị thông báo lỗi cho người dùng. |
| **Cách kiểm thử** | Tạo 1 Task cha có 3 Sub-tasks, lần lượt đổi 3 Sub-tasks sang `DONE` và kiểm tra trạng thái Task cha. |
| **Độ ưu tiên** | Must have |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NIFR-03 |
| **Tên** | Ghi nhật ký kiểm toán hệ thống (Audit Logging) |
| **Loại** | Toàn vẹn & Kiểm toán (Integrity & Audit) |
| **Điều kiện kích hoạt** | Phát sinh sự kiện `INSERT`, `UPDATE`, hoặc `DELETE` trên bảng `Tasks` |
| **Điều kiện tiền đề** | Người dùng đã đăng nhập và thực hiện thao tác thay đổi dữ liệu. |
| **Hành vi** | 1. Bắt sự kiện thay đổi dữ liệu từ hệ thống.<br>2. Trích xuất thông tin: `user_id`, `action_type`, `old_value`, `new_value`, `ip_address`.<br>3. Tự động ghi bản ghi mới vào bảng `audit_logs` cùng với thời gian thực (Server Timestamp). |
| **Kết quả** | Mọi biến động dữ liệu quan trọng đều được ghi vết lại phục vụ việc truy vết sự cố. |
| **Xử lý ngoại lệ** | Nếu ghi log thất bại, ghi nhận vào file log dự phòng (Fallback File Log) trên server để không làm gián đoạn luồng nghiệp vụ chính của người dùng. |
| **Cách kiểm thử** | Thực hiện chỉnh sửa Tên/Deadline của task, sau đó kiểm tra dữ liệu tương ứng xuất hiện trong bảng `audit_logs`. |
| **Độ ưu tiên** | Must have |