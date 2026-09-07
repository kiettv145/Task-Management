## 1. CHỌN DỰ ÁN (PROJECT SELECTION)

* **Tên dự án:** Hệ thống Quản lý Công việc Cá nhân & Nhóm (**Task Management**)
* **Loại hình dự án:** Dự án cá nhân (Personal Project / Side Project)
* **Định hướng mục tiêu:** Làm sản phẩm Portfolio cá nhân phục vụ ứng tuyển Vị trí **Software Engineering / Frontend / Fullstack Intern**.
* **Công nghệ dự kiến (Tech Stack):** 
  * **Frontend:** React.js / Next.js, Tailwind CSS (hoặc Material UI/Ant Design).
  * **Backend:** Node.js (Express.js) hoặc Java (Spring Boot) / Python (FastAPI).
  * **Database:** PostgreSQL / MongoDB.
  * **Khác:** JWT Authentication, RESTful API, Git/GitHub, Docker cơ bản.

---

## 2. BỐI CẢNH DỰ ÁN (PROJECT CONTEXT)

### 2.1 Bối cảnh thực tế & Động lực làm dự án
* **Vấn đề thực tế (Problem Statement):** Trong quá trình học tập và làm đồ án nhóm ở đại học, sinh viên và các nhóm làm việc nhỏ thường gặp tình trạng thông báo bị trôi trên Zalo/Facebook, quên deadline bài tập và khó theo dõi tiến độ công việc của từng thành viên.
* **Động lực cá nhân (Personal Motivation):** 
  * Muốn tự tay xây dựng một sản phẩm **end-to-end** hoàn chỉnh từ khâu phân tích yêu cầu, thiết kế cơ sở dữ liệu, lập trình API đến xây dựng giao diện người dùng.
  * Cần một sản phẩm đủ độ phức tạp (vượt qua các bài tutorial To-Do List cơ bản) để chứng minh năng lực tư duy logic, tổ chức code và giải quyết vấn đề với Nhà tuyển dụng (Recruiter / Tech Lead).

---

## 3. MỤC TIÊU DỰ ÁN (PROJECT OBJECTIVES)

### 3.1 Mục tiêu Kỹ thuật & Sự nghiệp (Career & Technical Objectives)
* **Xây dựng Portfolio ấn tượng:** Có một dự án chất lượng đưa vào CV và GitHub cá nhân, thể hiện được tư duy viết Clean Code, tổ chức thư mục chuẩn và sử dụng Git Flow chuyên nghiệp.
* **Luyện tập các Kỹ năng cốt lõi (Core Competencies):**
  * Nắm vững cách thiết kế **RESTful API** đúng chuẩn và tối ưu hóa truy vấn Database (Indexing, Pagination).
  * Làm quen với các luồng thực tế: Xác thực người dùng (Auth/JWT), Phân quyền (RBAC), Kéo thả (Drag & Drop UI), Xử lý bất đồng bộ.
  * Biết cách viết tài liệu API (Swagger/Postman Documentation) và Deploy ứng dụng lên Cloud (Vercel/Render/Render/Docker).

### 3.2 Mục tiêu Sản phẩm (Product Objectives)
* Xây dựng giao diện web phản hồi nhanh (< 300ms), trực quan, hỗ trợ kéo thả công việc dễ dàng.
* Đảm bảo hệ thống chạy ổn định, không bị lỗi luồng dữ liệu chính và hỗ trợ Responsive tốt trên cả Desktop và Điện thoại.

---

## 4. PHẠM VI DỰ ÁN (PROJECT SCOPE)

### 4.1 Phạm vi thực hiện (In-Scope - Tính năng MVP)

#### A. Xác thực & Phân quyền (Authentication & Authorization)
* Đăng ký / Đăng nhập tài khoản (bảo mật mật khẩu với `bcrypt`, cấp chứng thực bằng `JWT`).
* Phân quyền truy cập: Người tạo Workspace (Owner), Thành viên (Member).

#### B. Quản lý Không gian làm việc (Workspace Management)
* Tạo mới các Workspace (ví dụ: "Dự án Học tập", "Việc Cá nhân", "Đồ án Web").
* Mời thành viên tham gia vào Workspace qua Email hoặc Mã mời (Invite Code).

#### C. Quản lý Công việc & Trạng thái (Task Core Operations)
* **CRUD Task:** Tạo mới, sửa nội dung, xóa và xem chi tiết công việc.
* **Trạng thái & Mức độ:** Gán trạng thái (*To Do, In Progress, Done*) và độ ưu tiên (*Low, Medium, High*).
* **Quản lý Hạn nộp:** Đặt deadline, hiển thị cảnh báo bài tập/việc quá hạn hoặc sắp đến hạn.
* **Checklist/Subtasks:** Chia nhỏ task lớn thành các bước thực hiện nhỏ.

#### D. Trải nghiệm & Giao diện (UI/UX Views)
* **Kanban Board View:** Chế độ kéo-thả (Drag & Drop) mượt mà để đổi trạng thái task.
* **List View:** Xem dạng danh sách có các tính năng Tìm kiếm (Search), Bộ lọc (Filter theo status/priority) và Phân trang (Pagination).

### 4.2 Phạm vi mở rộng / Phát triển về sau (Out-of-Scope)
* Chưa làm tính năng Chat trực tiếp thời gian thực (Real-time Chat via WebSockets) – chỉ tập trung vào quản lý task.
* Chưa làm tích hợp thanh toán (Payment Gateway).
* Chưa phát triển Mobile App (React Native/Flutter) – ưu tiên hoàn thiện bản Web trước.

---

## 5. CÁC BÊN LIÊN QUAN (PROJECT STAKEHOLDERS)

| Bên liên quan (Stakeholder) | Phân loại | Vai trò & Trách nhiệm trong hệ thống | Kỳ vọng & Mục tiêu chính |
| :--- | :--- | :--- | :--- |
| **Product Owner / Project Lead** | Internal (Nội bộ) | - Quản lý định hướng sản phẩm, lập kế hoạch phát triển (Roadmap).<br>- Ưu tiên danh sách tính năng (Backlog) và phê duyệt các yêu cầu nghiệp vụ. | Sản phẩm hoàn thành đúng tiến độ, đảm bảo chất lượng kỹ thuật, tính năng hoạt động ổn định. |
| **Development Team (Fullstack Developer)** | Internal (Nội bộ) | - Thiết kế kiến trúc hệ thống, Cơ sở dữ liệu và API.<br>- Lập trình các chức năng Frontend/Backend, thực hiện kiểm thử (Testing) và triển khai (Deployment). | Yêu cầu nghiệp vụ rõ ràng, hệ thống dễ mở rộng, tối ưu hiệu năng và ít phát sinh lỗi (Bugs). |
| **Người dùng cá nhân (Individual End-Users)** | External (Bên ngoài) | - Sử dụng ứng dụng để quản lý công việc, lịch học, checklist và deadline cá nhân hàng ngày. | Giao diện đơn giản, dễ thao tác, tốc độ phản hồi nhanh, hệ thống nhắc nhở deadline chính xác. |
| **Nhóm làm việc / Đội ngũ dự án (Team Members & Leaders)** | External (Bên ngoài) | - Tạo dự án nhóm, phân công nhiệm vụ (Task Allocation), theo dõi tiến độ công việc chung và trao đổi thông tin. | Trực quan hóa tiến độ (Kanban board), minh bạch trong phân công việc, không bị bỏ sót thông tin. |
| **Quản trị viên hệ thống (System Administrator)** | Internal (Nội bộ) | - Quản lý tài khoản người dùng, phân quyền truy cập, giám sát trạng thái máy chủ và bảo mật dữ liệu. | Hệ thống hoạt động liên tục (High Availability), bảo mật thông tin người dùng và dễ dàng bảo trì. |