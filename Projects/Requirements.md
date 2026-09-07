# SYSTEM REQUIREMENTS SPECIFICATION (TASK 1)
**Project:** Task Management System

---

## 1. YÊU CẦU CHỨC NĂNG (FUNCTIONAL REQUIREMENTS - FR)

* **FR-01 (Đăng ký & Đăng nhập):**
  * **Input:** Email, Mật khẩu (tối thiểu 8 ký tự) hoặc Đăng nhập qua Google OAuth 2.0.
  * **Processing:** Hệ thống xác thực thông tin tài khoản. Nếu đăng nhập bằng Google lần đầu, tự động khởi tạo hồ sơ người dùng mới. Sinh mã xác thực JWT (Access Token có hiệu lực 1 giờ, Refresh Token có hiệu lực 7 ngày).
  * **Output:** Trả về kết quả đăng nhập thành công, điều hướng người dùng vào giao diện Bảng điều khiển (Dashboard).

* **FR-02 (Tạo mới Công việc - Task Creation):**
  * **Input:** Tên task (bắt buộc, 1-200 ký tự), Mô tả, Deadline (ngày/giờ), Mức độ ưu tiên (`LOW`, `MEDIUM`, `HIGH`), Người thực hiện (`Assignee_ID`), Nhãn (`Tags`).
  * **Processing:** Kiểm tra dữ liệu đầu vào. Xác minh `Assignee_ID` có thuộc danh sách thành viên active trong dự án hay không. Nếu hợp lệ, lưu bản ghi mới vào CSDL với trạng thái mặc định là `TO_DO`.
  * **Output:** Trả về mã HTTP `201 Created`, hiển thị ngay thẻ task mới lên cột `To-Do` trên Bảng Kanban.

* **FR-03 (Quản lý Bảng Kanban & Cập nhật Trạng thái):**
  * **Input:** Thao tác kéo-thả (Drag & Drop) thẻ task từ cột này sang cột khác (`TO_DO` $\rightarrow$ `IN_PROGRESS` $\rightarrow$ `DONE`).
  * **Processing:** Cập nhật trường `status` của task tương ứng trong CSDL. Nếu task được chuyển sang trạng thái `DONE`, tự động ghi nhận thời gian hoàn thành (`completed_at = NOW()`).
  * **Output:** Giao diện Kanban cập nhật vị trí thẻ task tức thì mà không cần tải lại toàn bộ trang (Full Page Reload).

* **FR-04 (Phân công & Đổi người thực hiện):**
  * **Input:** Chọn một hoặc nhiều thành viên từ danh sách Dropdown để gán vào Task.
  * **Processing:** Kiểm tra quyền hạn của người thực hiện thao tác (phải là Admin/PM/Project Owner). Cập nhật lại danh sách `Assignee_ID`.
  * **Output:** Hệ thống gửi thông báo In-app (Notification) đến người vừa được gán công việc.

* **FR-05 (Tìm kiếm & Lọc công việc):**
  * **Input:** Từ khóa tìm kiếm (Tên task/Mô tả) hoặc các tiêu chí lọc (Trạng thái, Priority, Assignee).
  * **Processing:** Hệ thống truy vấn CSDL theo bộ lọc tương ứng.
  * **Output:** Trả về danh sách các task thỏa mãn điều kiện lọc trong thời gian thực.

---

## 2. YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS - NFR)

### 2.1. Danh sách các yêu cầu phi chức năng

1. **NFR-PERF-01:** Thời gian phản hồi API tải bảng Kanban phải $\le 2$ giây.
2. **NFR-SEC-01:** Mật khẩu mã hóa bằng `bcrypt` (Cost factor $\ge 12$), khóa tài khoản sau 5 lần nhập sai.
3. **NFR-SEC-02:** Giới hạn tần suất gọi API tối đa 100 requests / 1 phút / IP.
4. **NFR-REL-01:** Độ sẵn sàng hoạt động của hệ thống (Uptime) đạt tối thiểu $99.5\%$/tháng.

---

### 2.2. Đặc tả chi tiết từng yêu cầu phi chức năng

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-PERF-01 |
| **Loại** | Performance Efficiency |
| **Mô tả** | Thời gian đáp ứng của API tải dữ liệu và thao tác kéo thả trên bảng Kanban phải $\le 2$ giây |
| **Nguồn** | Biên bản họp thống nhất hiệu năng hệ thống ngày 15/03 |
| **Thang đo** | Thời gian phản hồi (Response Time) từ lúc gửi request đến khi nhận data kết thúc (tính bằng giây) |
| **Tiêu chí** | Mốc $P_{95} \le 2\text{s}$ (95% số request hoàn tất dưới 2 giây) khi có 500 người dùng đồng thời, CSDL đạt 100.000 tasks |
| **Cách đo** | Kịch bản JMeter/K6 chạy kiểm thử tải trong 15 phút trên môi trường Staging |
| **Độ ưu tiên** | Must have |
| **Liên quan** | FR-03 (Bảng Kanban) |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-SEC-01 |
| **Loại** | Security |
| **Mô tả** | Mật khẩu phải mã hóa `bcrypt` (Salt factor $\ge 12$), kết nối mã hóa TLS 1.3, khóa tài khoản 15 phút nếu đăng nhập sai 5 lần liên tiếp |
| **Nguồn** | Tiêu chuẩn an toàn thông tin OWASP Top 10 |
| **Thang đo** | Thuật toán mã hóa mật khẩu, độ dài khóa TLS, số lần đăng nhập sai tối đa và thời gian khóa |
| **Tiêu chí** | $100\%$ mật khẩu lưu DB được hash bằng `bcrypt` (cost $\ge 12$). $100\%$ kết nối API qua HTTPS (TLS 1.3). Tự động khóa tài khoản đúng 15 phút ngay sau lần đăng nhập sai thứ 5. |
| **Cách đo** | Rà soát mã nguồn (Static Code Analysis) và chạy công cụ thử nghiệm tấn công OWASP ZAP |
| **Độ ưu tiên** | Must have |
| **Liên quan** | FR-01 (Đăng ký & Đăng nhập) |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-SEC-02 |
| **Loại** | Security & Resiliency |
| **Mô tả** | Tần suất gửi request tối đa không vượt quá 100 requests / 1 phút / địa chỉ IP |
| **Nguồn** | Tài liệu thiết kế kiến trúc Backend chống tấn công DDoS |
| **Thang đo** | Số lượng HTTP Request ghi nhận được từ 1 địa chỉ IP trong cửa sổ thời gian 60 giây |
| **Tiêu chí** | Giới hạn chính xác $\le 100\text{ req/min/IP}$. Request thứ 101 trong cùng phút phải bị chặn và trả về lỗi HTTP 429 (Too Many Requests) trong vòng $< 50\text{ms}$. |
| **Cách đo** | Chạy script tự động gửi 150 requests/phút từ 1 IP kiểm tra HTTP Status Code phản hồi |
| **Độ ưu tiên** | Should have |
| **Liên quan** | Toàn bộ các yêu cầu FR |

---

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NFR-REL-01 |
| **Loại** | Reliability & Availability |
| **Mô tả** | Độ sẵn sàng hệ thống đạt tối thiểu $99.5\%$/tháng (thời gian gián đoạn không quá 3.6 giờ/tháng) |
| **Nguồn** | Cam kết chất lượng dịch vụ (SLA) với khách hàng |
| **Thang đo** | Tỷ lệ phần trăm thời gian hệ thống phản hồi HTTP 2xx/3xx thành công trong tháng |
| **Tiêu chí** | Tỷ lệ Uptime $\ge 99.5\%$/tháng (Tổng thời gian ngắt quãng hệ thống ngoài dự kiến $\le 3\text{ giờ } 36\text{ phút}$ / 30 ngày) |
| **Cách đo** | Giám sát tự động 24/7 bằng công cụ UptimeRobot / Datadog với tần suất ping 1 phút/lần |
| **Độ ưu tiên** | Must have |
| **Liên quan** | Toàn bộ hệ thống |

---

## 3. YÊU CẦU CHỨC NĂNG KHÔNG TƯƠNG TÁC (NON-INTERACTIVE FUNCTIONAL REQUIREMENTS - NIFR)

### 3.1. Danh sách các yêu cầu chức năng không tương tác

1. **NIFR-01:** Tự động gửi email nhắc hạn công việc (Task Deadline Reminder) lúc 00:00 hằng ngày.
2. **NIFR-02:** Tự động cập nhật trạng thái Task cha sang `DONE` khi $100\%$ Sub-tasks hoàn thành.
3. **NIFR-03:** Tự động ghi nhật ký hệ thống (Audit Log) cho các thao tác Thêm/Sửa/Xóa dữ liệu.

---

### 3.2. Đặc tả chi tiết từng yêu cầu chức năng không tương tác

| Trường | Nội dung |
| :--- | :--- |
| **Mã** | NIFR-01 |
| **Tên** | Gửi email nhắc hạn công việc (Task Deadline Reminder) |
| **Loại** | Chức năng theo lịch (Temporal) |
| **Điều kiện kích hoạt** | Đúng `00:00` hằng ngày (Múi giờ UTC+7) |
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