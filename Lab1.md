
# Phân tích Hệ thống Quản lý Tiền lương

## 1. Phân tích Kiến trúc

### 1.1 Đề xuất Kiến trúc
Kiến trúc tổng quát: Hệ thống Quản lý Tiền lương được thiết kế theo mô hình client-server, bao gồm các thành phần chính sau:

- **Giao diện người dùng (Client)**: Ứng dụng desktop dành cho nhân viên và quản trị viên.
- **Backend Server**: Máy chủ xử lý logic nghiệp vụ và tương tác với cơ sở dữ liệu.
- **Cơ sở dữ liệu (Database)**: Lưu trữ thông tin nhân viên, tiền lương, thời gian làm việc, đơn đặt hàng mua hàng, và thông tin liên quan đến dự án.

### 1.2 Ý nghĩa và lý do lựa chọn từng thành phần
- **Giao diện người dùng (UI)**:
  - **Ý nghĩa**: Cung cấp giao diện tương tác cho nhân viên và quản trị viên để nhập thông tin và truy xuất báo cáo.
  - **Lý do**: Một giao diện người dùng thân thiện giúp người dùng dễ dàng thao tác mà không cần kiến thức kỹ thuật.

- **API (Application Programming Interface)**:
  - **Ý nghĩa**: Đóng vai trò cầu nối giữa giao diện người dùng và backend, cho phép truyền tải dữ liệu từ người dùng đến server.
  - **Lý do**: Tổ chức mã nguồn rõ ràng và dễ bảo trì, cho phép phát triển ứng dụng khác trong tương lai.

- **Backend Server**:
  - **Ý nghĩa**: Xử lý logic nghiệp vụ, quản lý các yêu cầu từ người dùng và tính toán tiền lương.
  - **Lý do**: Tách biệt logic nghiệp vụ với giao diện người dùng, dễ bảo trì và mở rộng.

- **Cơ sở dữ liệu (DB)**:
  - **Ý nghĩa**: Lưu trữ thông tin liên quan đến nhân viên, tiền lương, đơn đặt hàng, và các thông tin khác.
  - **Lý do**: Sử dụng cơ sở dữ liệu quan hệ để dễ dàng quản lý và truy vấn dữ liệu.

- **Project Management Database**:
  - **Ý nghĩa**: Cơ sở dữ liệu hiện có lưu trữ thông tin về dự án và số charge, mà hệ thống mới sẽ truy cập.
  - **Lý do**: Tránh thay thế hệ thống cũ, tiết kiệm chi phí và đảm bảo tính nhất quán.
### 1.3 Biểu đồ Package Mô tả Kiến trúc

![Diagram](http://www.plantuml.com/plantuml/png/NO-n3e8m48RtFiM5dLSmY3gGQCBYH1ZEUXAqN4dl68ZntIscHiFMVFtptVyNeXXq6fmPqJwm8yXshYVM39u6e3aB1QXOATpGKcjUvXSiuuFucfBRkceXppVGb9FqJ29mz5rlMmDhb79xLBoWhAnVchI7ONH-9eA5Vrmrpi4xzmU2lvDLE257mq2iwIzgLmFIvQMhAMBtEFmD
