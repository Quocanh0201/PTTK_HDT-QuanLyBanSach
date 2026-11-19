# Hệ thống quản lý bán sách

Ứng dụng desktop quản lý hoạt động bán sách: tài khoản và đăng nhập, nhân viên, khách hàng, sách, nhà cung cấp, nhà xuất bản, tác giả, thể loại, phiếu nhập/xuất, khuyến mãi, phân quyền và thống kê. Dự án được xây dựng bằng Java Swing, theo mô hình phân lớp BUS – DAO – DTO và lưu dữ liệu trong MySQL/MariaDB.

## Thành viên nhóm

- Võ Quốc Anh

## Tính năng chính

- Đăng nhập bằng tài khoản; hiển thị thông tin nhân viên và phân quyền theo nhóm quyền.
- Quản lý sách: thêm, sửa, xóa, tìm kiếm, sắp xếp và theo dõi số lượng tồn.
- Quản lý khách hàng, nhân viên, nhà cung cấp, nhà xuất bản, tác giả và thể loại.
- Quản lý phiếu nhập và phiếu xuất, gồm chi tiết từng cuốn sách.
- Tự động cập nhật số lượng tồn kho theo phiếu nhập và phiếu xuất.
- Quản lý tài khoản, nhóm quyền và danh mục chức năng.
- Quản lý khuyến mãi.
- Thống kê và hỗ trợ xuất dữ liệu ra Excel/PDF.
- Giao diện Java Swing với biểu tượng, ảnh nền và các bảng dữ liệu trực quan.

## Công nghệ sử dụng

- **Ngôn ngữ:** Java
- **Giao diện:** Java Swing/AWT
- **Cơ sở dữ liệu:** MySQL/MariaDB
- **Truy cập dữ liệu:** JDBC với MySQL Connector/J
- **Kiến trúc:** Các lớp `DTO`, `BUS`, `DAO` và `GUI`
- **IDE:** Apache NetBeans
- **Thư viện hỗ trợ:** Apache POI, iText, JCalendar, FlatLaf

## Cấu trúc thư mục

```text
PTTK_HDT-QuanLyBanSach/
├── lib/                         # Thư viện của dự án
├── nbproject/                   # Cấu hình dự án NetBeans
├── src/
│   ├── BUS/                     # Xử lý nghiệp vụ
│   ├── DAO/                     # Truy vấn cơ sở dữ liệu
│   ├── DTO/                     # Đối tượng dữ liệu
│   ├── Database/
│   │   └── quanlibansach.sql    # Tạo database và nạp dữ liệu mẫu
│   ├── Excel/                   # File Excel mẫu
│   ├── GUI/                     # Giao diện Swing và tài nguyên
│   │   ├── Controller/          # Điều khiển sự kiện
│   │   ├── Dialog/              # Cửa sổ dialog
│   │   ├── Format/              # Định dạng giao diện
│   │   ├── Image/               # Hình ảnh và biểu tượng
│   │   ├── ThongKe/             # Giao diện thống kê
│   │   └── View/                # Panel các chức năng
│   └── connectDB/
│       └── JDBCUtil.java        # Cấu hình kết nối JDBC
├── manifest.mf
└── mysql-connector-j-9.1.0.jar
```

## Yêu cầu môi trường

- JDK 23 hoặc phiên bản tương thích (dự án hiện cấu hình Java source/target 23).
- Apache NetBeans.
- MySQL hoặc MariaDB.
- phpMyAdmin hoặc công cụ quản lý cơ sở dữ liệu khác.

## Hướng dẫn cài đặt và chạy

### 1. Clone dự án

```bash
git clone https://github.com/Quocanh0201/PTTK_HDT-QuanLyBanSach.git
cd PTTK_HDT-QuanLyBanSach
```

### 2. Tạo và nạp cơ sở dữ liệu

Mở MySQL/phpMyAdmin và import file:

```text
src/Database/quanlibansach.sql
```

File SQL có sẵn lệnh tạo database `quanlibansach`, các bảng, khóa liên kết và dữ liệu mẫu.

### 3. Cấu hình kết nối database

Mở:

```text
src/connectDB/JDBCUtil.java
```

Kiểm tra hoặc thay đổi thông tin kết nối:

```java
String url = "jdbc:mysql://localhost:3306/quanlibansach";
String userName = "root";
String password = "";
```

### 4. Mở dự án bằng NetBeans

1. Chọn **File > Open Project**.
2. Mở thư mục `PTTK_HDT-QuanLyBanSach`.
3. Kiểm tra phần **Libraries** nếu NetBeans báo thiếu thư viện.
4. MySQL Connector/J đã có trong thư mục gốc: `mysql-connector-j-9.1.0.jar`.

> Nếu chương trình báo thiếu JAR do `nbproject/project.properties` chứa đường dẫn tuyệt đối của máy cũ, hãy liên kết lại các thư viện tương ứng trong **Properties > Libraries** của NetBeans.

### 5. Chạy ứng dụng

Mở class `src/GUI/DangNhapFrame.java`, sau đó chọn **Run File** hoặc chạy dự án.

Class chính của dự án là:

```text
GUI.DangNhapFrame
```

## Tài khoản mặc định

Các tài khoản được nạp trong `src/Database/quanlibansach.sql`:

| Tên đăng nhập | Mật khẩu | Nhóm quyền |
|---|---|---|
| `admin` | `12345` | Quản lý |
| `trung123` | `12345` | Nhân viên |
| `thuan123` | `12345` | Nhân viên |
| `khai123` | `12345` | Nhân viên |
| `dang123` | `12345` | Nhân viên |

Màn hình đăng nhập cũng điền sẵn tài khoản `admin` và mật khẩu `12345` để thuận tiện kiểm thử.

## Luồng hoạt động

1. `DangNhapFrame` nhận tên đăng nhập và mật khẩu.
2. `TaiKhoanBUS` gọi `TaiKhoanDAO` để xác thực tài khoản.
3. Sau khi đăng nhập thành công, hệ thống mở `WorkFrame`.
4. `WorkFrame` lấy danh sách chức năng được phân quyền và hiển thị menu phù hợp.
5. Giao diện `GUI/View` gọi lớp nghiệp vụ `BUS`.
6. Lớp `BUS` sử dụng `DAO` và `DTO` để truy xuất/cập nhật MySQL qua `JDBCUtil`.

## Đóng góp

```bash
git checkout -b feature/ten-chuc-nang
git commit -m "Thêm chức năng ..."
git push origin feature/ten-chuc-nang
```

Sau đó tạo Pull Request trên GitHub.

## Giấy phép

Repository hiện chưa cung cấp file giấy phép. Vui lòng liên hệ tác giả trước khi sử dụng ngoài mục đích học tập.