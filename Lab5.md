# Thiết Kế Hệ Thống Payroll 
## Mô Tả Hệ Thống

Hệ thống **Payroll** được thiết kế để quản lý toàn bộ quy trình liên quan đến chấm công, tính toán lương, và quản lý nhân sự. Các hệ thống con (Subsystems) được phân chia theo chức năng chính để đảm bảo tính linh hoạt và dễ bảo trì.

---

### **1. Hệ Thống Đăng Nhập**

#### **Chức năng:**
- Cung cấp giao diện cho người dùng (nhân viên, quản trị viên) để đăng nhập vào hệ thống.
- Kiểm tra thông tin đăng nhập và xác thực quyền truy cập dựa trên vai trò.

#### **Thành phần chính:**
- **Giao diện người dùng:** Form đăng nhập.
- **Auth Service:** Xử lý xác thực thông tin đăng nhập.
- **Cơ sở dữ liệu:** Lưu trữ thông tin người dùng (username, password được mã hóa, vai trò).

#### **Luồng hoạt động:**
1. Người dùng nhập thông tin đăng nhập.
2. Hệ thống gửi yêu cầu xác thực đến **Auth Service**.
3. Nếu xác thực thành công, hệ thống chuyển hướng đến màn hình chính.
4. Nếu thất bại, hiển thị thông báo lỗi.

---

### **2. Hệ Thống Nhập Thông Tin Giờ Làm Việc**

#### **Chức năng:**
- Cho phép nhân viên nhập giờ làm việc hàng ngày/tuần.
- Lưu trữ và quản lý dữ liệu giờ làm việc để phục vụ tính toán lương.

#### **Thành phần chính:**
- **Giao diện nhập liệu:** Nhập thông tin giờ làm.
- **Timesheet Service:** Xử lý lưu trữ và quản lý giờ làm việc.
- **Cơ sở dữ liệu:** Lưu trữ bảng giờ làm việc của nhân viên.

#### **Luồng hoạt động:**
1. Nhân viên nhập thông tin giờ làm việc qua giao diện.
2. Dữ liệu được gửi đến **Timesheet Service** để xử lý.
3. Hệ thống lưu thông tin vào cơ sở dữ liệu và phản hồi kết quả.

---

### **3. Hệ Thống Tính Toán Lương**

#### **Chức năng:**
- Tự động tính toán lương dựa trên giờ làm việc, phụ cấp, thưởng và khấu trừ.
- Cung cấp thông tin lương cho nhân viên và quản trị viên.

#### **Thành phần chính:**
- **Payroll Service:** Tính toán lương.
- **Timesheet Service:** Cung cấp dữ liệu giờ làm.
- **Cơ sở dữ liệu:** Lưu trữ thông tin lương bổ sung như phụ cấp và khấu trừ.

#### **Luồng hoạt động:**
1. Quản trị viên gửi yêu cầu tính toán lương.
2. **Payroll Service** truy vấn giờ làm và thông tin bổ sung từ cơ sở dữ liệu.
3. Kết quả tính toán lương được lưu lại và hiển thị.

---

### **4. Hệ Thống Tạo Phiếu Lương**

#### **Chức năng:**
- Tạo phiếu lương cho từng nhân viên dựa trên kết quả tính toán.
- Hỗ trợ xuất phiếu lương dưới dạng PDF/email.

#### **Thành phần chính:**
- **Payroll Report Generator:** Tạo phiếu lương.
- **Cơ sở dữ liệu:** Lưu trữ thông tin phiếu lương đã tạo.
- **Email Service:** Gửi phiếu lương qua email.

#### **Luồng hoạt động:**
1. Quản trị viên yêu cầu tạo phiếu lương.
2. **Payroll Report Generator** tạo phiếu lương dựa trên dữ liệu từ cơ sở dữ liệu.
3. Phiếu lương được xuất và gửi qua email (nếu cần).

---

### **5. Hệ Thống Tạo Báo Cáo Lương**

#### **Chức năng:**
- Tạo báo cáo tổng hợp lương theo tháng, quý, năm.
- Hỗ trợ quản trị viên phân tích chi phí nhân sự.

#### **Thành phần chính:**
- **Reporting Module:** Tổng hợp và xuất báo cáo.
- **Cơ sở dữ liệu:** Lưu trữ dữ liệu lương để phân tích.

#### **Luồng hoạt động:**
1. Quản trị viên chọn khoảng thời gian cần báo cáo.
2. **Reporting Module** truy xuất và tổng hợp dữ liệu từ cơ sở dữ liệu.
3. Báo cáo được hiển thị hoặc xuất file.

---

### **6. Hệ Thống Quản Lý Phân Quyền và Bảo Mật**

#### **Chức năng:**
- Quản lý quyền truy cập của người dùng dựa trên vai trò (nhân viên, quản trị viên).
- Bảo mật dữ liệu bằng cách mã hóa thông tin và kiểm tra quyền truy cập.

#### **Thành phần chính:**
- **Role Management Service:** Quản lý vai trò.
- **Security Module:** Xử lý bảo mật.
- **Cơ sở dữ liệu:** Lưu trữ thông tin vai trò và chính sách bảo mật.

#### **Luồng hoạt động:**
1. Quản trị viên phân quyền cho người dùng.
2. Hệ thống kiểm tra quyền trước khi cho phép truy cập tài nguyên.

---

### **7. Hệ Thống Quản Lý Mở Rộng và Linh Hoạt**

#### **Chức năng:**
- Dễ dàng mở rộng để thêm các chức năng mới.
- Hỗ trợ tích hợp với các hệ thống khác.

#### **Thành phần chính:**
- **Integration Layer:** Xử lý kết nối với hệ thống bên ngoài.
- **Modular Architecture:** Thiết kế hệ thống theo module linh hoạt.

#### **Luồng hoạt động:**
1. Hệ thống được thiết kế theo cấu trúc module, dễ dàng thêm mới chức năng.
2. Tích hợp qua API hoặc các giao thức chuẩn như REST/GraphQL.

---

## **Sơ Đồ Các Hệ Thống Con (Subsystems)**
### **1. Use Case Diagram (Sơ đồ ca sử dụng)**
![Use Case Diagram](https://www.plantuml.com/plantuml/png/PP31IiD054NtynMFxliBKX2XWfOQYhWTuoCPU7apPZALBiM5Mtz0iBeJ2kgoHLnCwN_aJon3oape9cJkFLpUlIFRoBfn5GcPDxg6mQJqxmnpvJzv0DB2MML8Bn0F_fLhrnyCv7-3VIbP5bWVt6dfVxW03Y6stNm7Q9m9uIpcqY8CjY_Rfu2qwvK9zeKk54TW4XmeLBjv1V9l5SptlyzvOC_Pk6QcAepy3LPWIjMk_npGxcktv2AWrmeVfd9XIPa8p_oAonvsAYbt91lSixKcwWVV-gM6VFyvYixGwBg9T1m6JAX_xnRjvf6JcJ9DQ8KuJ0h3uKbNFfLYnxwSzX7TxZ4YLTBxn3YBKFSuxjpfwPaZv3jNaVW7)
### **2. Sequence Diagrams (Sơ đồ tuần tự)**
#### **2.1. Đăng Nhập (Login)**
![Login Sequence Diagram](https://www.plantuml.com/plantuml/png/PL6_IiGm7Dxp51ytwN2uEyW9WiA929uFa4jB6xHfJTBgAZSw-G325N4yK72n7Hno-1vv4vEUzLBT-llw_Vb-lqoKfbANsJMXJESIbogMf70GPxoWGcDqcYTSu9mcyGXKeHlzD6GTbZh5HImhpZOy3_pCG-OHrNHErORL3uJuO8mFjlxOnrbgcrM1qlqID8jHcIKAgjHjBYEo9JfLaEPqnxPTSUZKl8i4cWki7zSBzoawFnAIdRRlu8HJRjj51Yrfg1R9rwjjdpWYyo4IyiiV_mkUITiyexBjFQviywbnKthWpjJC6ThsZGt3_-mx3JI3ojYPfMOfKZ1VQc_cm1UDkMrglXiUmldvEpgh4x-9w48V-btcfix3NcGIYyW__JS0)
#### **2.2. Nhập Thông Tin Giờ Làm Việc**
![Nhập Thông Tin Giờ Làm Việc](https://www.plantuml.com/plantuml/png/TP8nJiCm58Ptd-9NzrwW0-e0WW6XIlG2hcib5eaJOYSI8s9WO6H6f6AkO62g1uP8lOTlmdEhH4gKRCwlzttljvMbiRomPPemBcnMu2hDa-n9IfPJh8JAkRQOhLKgJIobnOf7SWPkq4MKJ4xVow9IOW2Smm5poItVS7CURJyOQ-jWVj7VY0NkOd_Ovx1nywiZMAKHAUy-a3Hrolh3H0_Na-3QkxqQvr7HyLMm8KMchXqPRey_vPIWgJE8umx6kqzilVj64fmbw_ZvUAqLtUjB8_RkNU717_ui7akAa9os5QGQwJNoGEiYK9LtprEQFX4StOClS4DrNpGi5NbhBxbfTbaurpg620bRIhqDlyy_)
#### **2.3. Tính Toán Lương**
![Tính Toán Lương](https://www.plantuml.com/plantuml/png/bPEnJlCm58NtFCLHvxyly0-e4aXaOAX25qOtZHAhgLCIkr96nC30p8YW85IfgA83KpmmMEfx-4suXIPgL2F1aiZ7ztmvlhxf5PBbKarIZuKooz7nWmvO0J_mfhJ1GpvbGgBJPsMUfIdwB8w-2dR2TkskF8_o6GzRnJkfNJ_WawX8eaYs78tgz9mmoOQi-2wj5vxd1-WUxIV3VroOfK9eguM2D2kHG6PcBf1krfkvYBtzOlAsWvBzrEeLH_aRIEqYpa5y8ftPwgN4oEetfDpg6uMONlT8pUC4iwqIUWSsGjN78yGWLoLcn167Negd5mmYCK-29BCKNkFiEXCHpbRFnDDNVuxbQjMn4Z52IZVz0UVeKnsnwOzCp3jX91SO9wGeoDpgrt-qiLbR_K3ThZtk5Ev3rLU5eTLtA9JZqjgJqoQDRVKXSQb8s0s0Stu8uGVazEcRru8YMtsBePbd2EdHU7gH66t_k4y0)
### **3. Class Diagram (Sơ đồ lớp)**
![Class Diagram](https://www.plantuml.com/plantuml/png/ZP7FIiD04CRl-nH3Jehq1NAGWXxq9bOVO9iTaiNPdR1_B4Ky-nI2zLxqR8-1laVVn7LhPGCzU1cIRtxvlfd9r0VfGZGa6fBUmxr71qy2O09QrQ1joCynoLOQh64MdBPj5llqmOAT6ecEgQJEWBZLzkHKF8lVY3jjq7U8uKWEcfvuYNXTQ4g6v7YPQdvDYGzN79slGN6S4-QKHqdw1yoTCkr6BXqJ_JFBIv9kMJYdU5In2Pgj7ycIY1VIDZYUev7KH981PzcfdEGMUtR7bZPiGrTi63X8kc0VHiujMdG9sTliZVFVcapEYvlMKDbkzxNkeTMxpIlGy6OgyTVFzE4cYLMxpGTG8byYqFPpkx9j9Gxzn1wcJcZV3UyMmh1kEfWFAuOcbKfCqQfeI7m3)
### **4. Activity Diagram (Sơ đồ hoạt động)**
#### **4.1. Đăng Nhập (Login)**
![Activity Diagram](https://www.plantuml.com/plantuml/png/7OwXheCm64Pzd-AJy0eWBl8g56QIZ4ARmD-cBLkc4OWfrEoIwRcf8U55-YOhDSsNzEJyfx2kDcuSUXO7oqhXls-DqN93zS1nsPxGjRLNPPgSoHP99ROFTN2I8FpwqkZzEl-bS88JaXEtAGEooemtdAChADI1pd3XNQZB6UyjHrAgYFvBlquKF--7x26nB_iKRb2C2JWriWs5IhCYx2Ft1m00)
#### **4.2. Nhập Thông Tin Giờ Làm Việc**
![Activity Diagram](https://www.plantuml.com/plantuml/png/SoWkIImgAStDuG8pkApyCWulobCeopoyAayXB-FXhhK52kcP3tVFLSWvl21NeGp8R4-svhBo1ZAQSnLAYX8LKXxkNg-G0v8eLSXuk7jnWK8Ea6tDbPcceE62LSvUKw4a8pLFGICojLYJIq71okVOXbAWqE4jUUaA9Pb0wmylo5T8FhPGeVZXxld85bXpfUOKfofe-EM3zNc0N96dK08qkXjaylHCg9iHolDICjE0Viilu780ia4U1G00)
### **5. Component Diagram (Sơ đồ thành phần)**
![Component Diagram](https:////www.plantuml.com/plantuml/png/RPB12e9048RlFiNWtLS8Y-ZKGSfEqM7KGPVMNTbTWuZUFOIXNGUF_lnyd_-mfG_emZpghBNZP0sP0Fd9MHF8T3byCe3xsVRAG8KzFPRFMeta1w8GemhVNgk9Ws-MmWxOFYDhFuS1hkHUgXMqVyf0PxLUPHUQh8ireJbYm0OziUVcoK6DZPQMcB4Z9cpWOE6dqw4eTlB_nIsuip4fkH3NDZQcS2wjTco0fP2RWYsDtEAzgv8yGaccMrx73m00)

