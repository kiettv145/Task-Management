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

| Vai trò | Người đảm nhiệm | Trách nhiệm & Mức độ ảnh hưởng |
| :--- | :--- | :--- |
| **Developer / Product Owner** | **Bản thân bạn (Sinh viên)** | - Chịu trách nhiệm 100% từ lên ý tưởng, thiết kế UI/DB, viết Code Frontend/Backend, Testing và Deployment.<br>- Quản lý tiến độ dự án cá nhân theo các mốc thời gian (Milestones). |
| **Nhà tuyển dụng (Recruiter / Tech Lead)** | Các công ty/doanh nghiệp ứng tuyển Intern | - Đánh giá chất lượng Source Code trên GitHub, kiến trúc hệ thống và tư duy thiết kế phần mềm.<br>- Đặt câu hỏi phỏng vấn dựa trên dự án này để kiểm tra năng lực thực tế. |
| **Người dùng trải nghiệm (Beta Testers)** | Bạn bè sinh viên / Đồng học | - Dùng thử ứng dụng, feedback về trải nghiệm người dùng (UX) và tìm lỗi (Bugs) giúp bạn hoàn thiện sản phẩm trước khi đi phỏng vấn. |