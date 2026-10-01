# Bài Tập 5: Quản lý quyền sở hữu thư mục Web (Directory Permission Management)

## 📋 1. Tổng quan & Mục tiêu
- **Mục tiêu**: Hiểu và áp dụng cơ chế phân quyền tệp tin/thư mục (`chown`, `chmod`) trên Linux theo nguyên tắc Đặc quyền Tối thiểu (Principle of Least Privilege).
- **Bối cảnh thực tế**: Phân quyền tối ưu cho thư mục web tĩnh `/var/www/ptit-app/` để user không phải root (`zeno-one`) có thể chỉnh sửa mã nguồn trực tiếp mà không cần dùng `sudo`, đồng thời dịch vụ Nginx (chạy dưới user/group `www-data`) vẫn có đủ quyền đọc để phục vụ nội dung cho người dùng qua **Cloudflare Tunnel**.

---

## 💻 2. Môi trường triển khai
- **Hệ điều hành**: Ubuntu Server (Máy ảo VirtualBox Local).
- **Tài khoản thao tác**: `zeno-one` (User thường có quyền `sudo`).
- **Web Server**: Nginx.
- **Giải pháp Công khai (Public Access)**: Cloudflare Tunnel (`cloudflared`).

---

## 🛠️ 3. Các bước thực hiện

### Bước 1: Khởi tạo cấu trúc thư mục Web
Tạo thư mục lưu trữ mã nguồn cho ứng dụng:
```bash
sudo mkdir -p /var/www/ptit-app/html