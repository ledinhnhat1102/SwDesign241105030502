# Thiết Kế Hệ Thống Payroll - Mô Tả Hệ Thống

Hệ thống **Payroll** được thiết kế để quản lý toàn bộ quy trình liên quan đến chấm công, tính toán lương, và quản lý nhân sự. Các hệ thống con (Subsystems) được phân chia theo chức năng chính để đảm bảo tính linh hoạt và dễ bảo trì.

---

## **1. Hệ Thống Đăng Nhập**

### **Chức năng:**
- Cung cấp giao diện cho người dùng (nhân viên, quản trị viên) để đăng nhập vào hệ thống.
- Kiểm tra thông tin đăng nhập và xác thực quyền truy cập dựa trên vai trò.

### **Thành phần chính:**
- **Giao diện người dùng:** Form đăng nhập.
- **Auth Service:** Xử lý xác thực thông tin đăng nhập.
- **Cơ sở dữ liệu:** Lưu trữ thông tin người dùng (username, password được mã hóa, vai trò).

### **Luồng hoạt động:**
1. Người dùng nhập thông tin đăng nhập.
2. Hệ thống gửi yêu cầu xác thực đến **Auth Service**.
3. Nếu xác thực thành công, hệ thống chuyển hướng đến màn hình chính.
4. Nếu thất bại, hiển thị thông báo lỗi.

---

## **2. Hệ Thống Nhập Thông Tin Giờ Làm Việc**

### **Chức năng:**
- Cho phép nhân viên nhập giờ làm việc hàng ngày/tuần.
- Lưu trữ và quản lý dữ liệu giờ làm việc để phục vụ tính toán lương.

### **Thành phần chính:**
- **Giao diện nhập liệu:** Nhập thông tin giờ làm.
- **Timesheet Service:** Xử lý lưu trữ và quản lý giờ làm việc.
- **Cơ sở dữ liệu:** Lưu trữ bảng giờ làm việc của nhân viên.

### **Luồng hoạt động:**
1. Nhân viên nhập thông tin giờ làm việc qua giao diện.
2. Dữ liệu được gửi đến **Timesheet Service** để xử lý.
3. Hệ thống lưu thông tin vào cơ sở dữ liệu và phản hồi kết quả.

---

## **3. Hệ Thống Tính Toán Lương**

### **Chức năng:**
- Tự động tính toán lương dựa trên giờ làm việc, phụ cấp, thưởng và khấu trừ.
- Cung cấp thông tin lương cho nhân viên và quản trị viên.

### **Thành phần chính:**
- **Payroll Service:** Tính toán lương.
- **Timesheet Service:** Cung cấp dữ liệu giờ làm.
- **Cơ sở dữ liệu:** Lưu trữ thông tin lương bổ sung như phụ cấp và khấu trừ.

### **Luồng hoạt động:**
1. Quản trị viên gửi yêu cầu tính toán lương.
2. **Payroll Service** truy vấn giờ làm và thông tin bổ sung từ cơ sở dữ liệu.
3. Kết quả tính toán lương được lưu lại và hiển thị.

---

## **4. Hệ Thống Tạo Phiếu Lương**

### **Chức năng:**
- Tạo phiếu lương cho từng nhân viên dựa trên kết quả tính toán.
- Hỗ trợ xuất phiếu lương dưới dạng PDF/email.

### **Thành phần chính:**
- **Payroll Report Generator:** Tạo phiếu lương.
- **Cơ sở dữ liệu:** Lưu trữ thông tin phiếu lương đã tạo.
- **Email Service:** Gửi phiếu lương qua email.

### **Luồng hoạt động:**
1. Quản trị viên yêu cầu tạo phiếu lương.
2. **Payroll Report Generator** tạo phiếu lương dựa trên dữ liệu từ cơ sở dữ liệu.
3. Phiếu lương được xuất và gửi qua email (nếu cần).

---

## **5. Hệ Thống Tạo Báo Cáo Lương**

### **Chức năng:**
- Tạo báo cáo tổng hợp lương theo tháng, quý, năm.
- Hỗ trợ quản trị viên phân tích chi phí nhân sự.

### **Thành phần chính:**
- **Reporting Module:** Tổng hợp và xuất báo cáo.
- **Cơ sở dữ liệu:** Lưu trữ dữ liệu lương để phân tích.

### **Luồng hoạt động:**
1. Quản trị viên chọn khoảng thời gian cần báo cáo.
2. **Reporting Module** truy xuất và tổng hợp dữ liệu từ cơ sở dữ liệu.
3. Báo cáo được hiển thị hoặc xuất file.

---

## **6. Hệ Thống Quản Lý Phân Quyền và Bảo Mật**

### **Chức năng:**
- Quản lý quyền truy cập của người dùng dựa trên vai trò (nhân viên, quản trị viên).
- Bảo mật dữ liệu bằng cách mã hóa thông tin và kiểm tra quyền truy cập.

### **Thành phần chính:**
- **Role Management Service:** Quản lý vai trò.
- **Security Module:** Xử lý bảo mật.
- **Cơ sở dữ liệu:** Lưu trữ thông tin vai trò và chính sách bảo mật.

### **Luồng hoạt động:**
1. Quản trị viên phân quyền cho người dùng.
2. Hệ thống kiểm tra quyền trước khi cho phép truy cập tài nguyên.

---

## **7. Hệ Thống Quản Lý Mở Rộng và Linh Hoạt**

### **Chức năng:**
- Dễ dàng mở rộng để thêm các chức năng mới.
- Hỗ trợ tích hợp với các hệ thống khác.

### **Thành phần chính:**
- **Integration Layer:** Xử lý kết nối với hệ thống bên ngoài.
- **Modular Architecture:** Thiết kế hệ thống theo module linh hoạt.

### **Luồng hoạt động:**
1. Hệ thống được thiết kế theo cấu trúc module, dễ dàng thêm mới chức năng.
2. Tích hợp qua API hoặc các giao thức chuẩn như REST/GraphQL.

---

## **Sơ Đồ Các Hệ Thống Con (Subsystems)**

Dựa trên mô tả các hệ thống con trên, sơ đồ các hệ thống con có dạng:

