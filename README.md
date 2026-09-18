# Xây dựng hệ thống quản lý bán sách
# Xây dựng hệ thống quản lý bán sách

## Thành viên của nhóm

- Võ Quốc Anh

## Hướng dẫn chạy dự án

### Bước 1: Clone project

git clone https://github.com/Quocanh0201/PTTK_HDT-QuanLyBanSach.git

### Bước 2: Cấu hình cơ sở dữ liệu

Mở MySQL/phpMyAdmin và tạo database:

quanlibansach

Sau đó import file SQL trong thư mục `src/Database`.

### Bước 3: Cấu hình kết nối database

Kiểm tra thông tin kết nối trong:

`src/connectDB/JDBCUtil.java`

### Bước 4: Chạy chương trình

Mở project bằng NetBeans và chạy:

`DangNhapFrame`
