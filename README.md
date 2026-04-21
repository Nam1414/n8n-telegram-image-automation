# 🤖 Hệ Thống Tự Động Xử Lý Ảnh Qua Telegram & Lưu Trữ Google Drive (n8n)

Dự án báo cáo giữa kỳ: Ứng dụng Workflow Automation (n8n) để xây dựng luồng tiếp nhận, xử lý (tách nền ảnh) và tự động hóa lưu trữ trên nền tảng đám mây.

## 🎓 Thông tin sinh viên
* **Họ và tên:** Nguyễn Thanh Nam
* **MSSV:** 123000156
* **Trường:** Đại học Lạc Hồng (LHU)
* **Email:** thanhnam14112005@gmail.com

---

## 🎯 Yêu cầu bài toán
Hệ thống giải quyết bài toán tự động hóa với các luồng công việc cụ thể:
1. Nhận hình ảnh và yêu cầu (caption) từ người dùng thông qua Telegram Bot.
2. Tự động tải dữ liệu ảnh dạng Binary về máy chủ nội bộ (n8n).
3. Gọi API bên thứ 3 (Remove.bg) để thực hiện tách nền ảnh.
4. Chạy script xử lý logic để tự động đổi tên file theo định dạng: `Nam_KetQua_[Yêu_cầu]_[Timestamp].jpg` nhằm tránh trùng lặp.
5. Upload file ảnh đã xử lý hoàn thiện lên thư mục chỉ định trên Google Drive.

---

## 🔄 Sơ đồ khối (Workflow Diagram)

```text
[ Telegram Bot ] ──(Nhận Ảnh + Caption)──┐
                                         ▼
                               [ Telegram Trigger Node ]
                                         │
                                         ▼
                               [ Telegram: Get File Node ]
                                         │
                                         ▼
                            [ HTTP Request: Remove.bg API ] ──(Xử lý tách nền)
                                         │
                                         ▼
                             [ Code Node (JavaScript) ] ──(Đổi tên file tự động)
                                         │
                                         ▼
                             [ Google Drive: Upload Node ]
                                         │
                                         ▼
                                [ Google Drive Folder ]

🛠️ Công nghệ & API sử dụng
Core Engine: n8n (Workflow Automation Tool)

Telegram Bot API: Nhận sự kiện, dữ liệu ảnh và text từ người dùng.

Remove.bg API: Xử lý đồ họa trực tuyến (tách nền ảnh) thông qua phương thức HTTP POST.

Google Drive API: Lưu trữ đám mây qua giao thức OAuth2.

JavaScript: Xử lý chuỗi (String manipulation), thời gian (Date/Time) và chuẩn hóa tên file.

🚀 Hướng dẫn cài đặt (Installation)
Nếu bạn muốn triển khai lại hệ thống này trên môi trường n8n cục bộ hoặc cloud:

Clone repository này về máy.

Tại giao diện Workflows của n8n, chọn Import from File.

Chọn file telegram_to_drive.json đính kèm trong dự án này.

Cấu hình lại các thông tin Credentials:

Telegram account: Nhập Bot Token lấy từ BotFather.

Remove.bg API: Nhập API Key ở phần Header X-Api-Key trong node HTTP Request.

Google Drive OAuth2: Cấp quyền truy cập tài khoản Google Drive và điền Folder ID thư mục đích.

Lưu và kích hoạt (Active) Workflow.
