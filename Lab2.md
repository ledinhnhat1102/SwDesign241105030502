# 1. Ca sử dụng Record Purchase Orders

## 1.1 Mô tả tổng quan ca sử dụng "Record Purchase Orders"

**Mục tiêu:**  
Nhân viên ghi nhận các đơn hàng mới với thông tin về ngày giao dịch và giá trị đơn hàng.

**Tác nhân chính:**  
Nhân viên hưởng lương hoa hồng.

**Kết quả mong muốn:**  
Đơn hàng được ghi nhận và lưu trữ vào hệ thống để tính hoa hồng cho nhân viên.

---

## 1.2 Phân tích theo lớp Boundary, Control, và Entity

### **Boundary (Giao diện)**
- **PurchaseOrderForm:**
  - Là giao diện người dùng để nhân viên nhập thông tin đơn hàng.
  - Giao diện này cung cấp các trường để nhập ngày giao dịch và giá trị đơn hàng.
  - Giao diện cũng cung cấp các nút như "Lưu" hoặc "Hủy bỏ".
- **PurchaseOrderConfirmationView:**
  - Hiển thị xác nhận sau khi đơn hàng được ghi nhận thành công hoặc thông báo lỗi khi có sự cố.

### **Control (Điều khiển)**
- **PurchaseOrderController:**
  - Quản lý luồng dữ liệu giữa giao diện và lớp thực thể.
  - Khi nhân viên nhập thông tin và nhấn "Lưu", lớp này thực hiện các công việc:
    - Xác nhận dữ liệu đầu vào (ví dụ: kiểm tra ngày có hợp lệ hay không, giá trị đơn hàng có phù hợp không).
    - Gửi thông tin tới lớp thực thể để lưu trữ.
    - Trả về thông báo xác nhận hoặc thông báo lỗi cho giao diện.

### **Entity (Thực thể)**
- **PurchaseOrder:**
  - Đại diện cho một đơn hàng trong hệ thống.
  - Bao gồm các thuộc tính:
    - `orderId`: Mã đơn hàng.
    - `employeeId`: Mã nhân viên (liên kết tới nhân viên ghi nhận đơn hàng).
    - `orderDate`: Ngày giao dịch.
    - `orderValue`: Giá trị đơn hàng.
- **CommissionEmployee:**
  - Thực thể liên kết đến thông tin nhân viên hưởng hoa hồng.
  - Bao gồm các thuộc tính cần thiết để tính toán và cập nhật hoa hồng dựa trên đơn hàng.

---

## 1.3 Luồng hoạt động của hệ thống (Control Flow)

1. Nhân viên nhập thông tin đơn hàng trên **PurchaseOrderForm** và nhấn "Lưu".
2. **PurchaseOrderController** nhận dữ liệu, kiểm tra tính hợp lệ (ngày và giá trị).
3. Nếu dữ liệu không hợp lệ, thông báo lỗi được gửi lại **PurchaseOrderForm**.
4. Nếu dữ liệu hợp lệ, **PurchaseOrderController** chuyển dữ liệu tới lớp **PurchaseOrder** để lưu vào cơ sở dữ liệu.
5. Sau khi lưu thành công, **PurchaseOrderController** gửi xác nhận thành công tới **PurchaseOrderConfirmationView** để hiển thị cho nhân viên.
