# PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## Mục đích
Phân tích kiến trúc và ca sử dụng của hệ thống "Payroll System".

## Thực hiện

### 1. Phân tích kiến trúc

#### 1.1 Đề xuất kiến trúc
Kiến trúc tổng thể của hệ thống "Payroll System" được thiết kế theo mô hình client-server, cho phép tách biệt rõ ràng giữa giao diện người dùng và logic xử lý nghiệp vụ, giúp hệ thống dễ dàng mở rộng và bảo trì.

- **Thành phần trong kiến trúc**:
  1. **Giao diện người dùng (Client)**:
     - **Ý nghĩa**: Cung cấp trải nghiệm người dùng cho nhân viên và quản trị viên để thực hiện các chức năng như xem thông tin, quản lý thanh toán, và cập nhật thông tin.
     - **Lý do lựa chọn**: Giao diện đồ họa dễ sử dụng giúp người dùng thực hiện nhiệm vụ một cách hiệu quả và nhanh chóng.

  2. **Backend Server**:
     - **Ý nghĩa**: Xử lý tất cả các yêu cầu từ giao diện người dùng, thực hiện các tính toán tiền lương, và tương tác với cơ sở dữ liệu.
     - **Lý do lựa chọn**: Tách biệt logic nghiệp vụ với giao diện giúp dễ dàng cập nhật và mở rộng trong tương lai.

  3. **Cơ sở dữ liệu (Database)**:
     - **Ý nghĩa**: Lưu trữ tất cả thông tin liên quan đến nhân viên, tiền lương, thời gian làm việc và phương thức thanh toán.
     - **Lý do lựa chọn**: Sử dụng cơ sở dữ liệu quan hệ để quản lý dữ liệu hiệu quả và đảm bảo tính toàn vẹn.

  4. **API (Application Programming Interface)**:
     - **Ý nghĩa**: Là cầu nối giữa giao diện người dùng và backend server, cho phép các thành phần giao tiếp với nhau.
     - **Lý do lựa chọn**: API giúp tổ chức mã nguồn rõ ràng và dễ bảo trì, đồng thời có thể hỗ trợ tích hợp với các hệ thống khác trong tương lai.

#### 1.2 Biểu đồ package mô tả kiến trúc
![Diagram](http://www.plantuml.com/plantuml/png/TP7TQiCm38NlynIczts5qPQECTXWxES1L4VhmlmJ9EKYZBxxD3EAZTn0RdGEvvEFTYn0iiGmpE2_uOnkym8hvH3Ssyg2SUD-1kUkuWSZkSSaI9_WiOZw-G3CxZxE8Q-8H-2lKmOQAsq_nYdLmaN_ElYmy9HGdK_vFFas-7-ZPqXgfKfudo9wpRFAAywPv04J4aYc3l080cxllJBxp_YBu4aohUqg4PDOhTgc4NlO4_2jwWwMfJFBqE4rs_JkjjixMrfxWhwd7HHFjmxhwpRJtgVu-YrPIF4sjHX0ZIqE6zqGrNCPTfZ69OPV)

## 2. Cơ chế phân tích

### 2.1 Đề xuất cơ chế cần giải quyết trong bài toán
Dựa trên phân tích yêu cầu, các cơ chế cần thiết cho hệ thống "Payroll System" bao gồm:

1. **Xác thực và phân quyền người dùng**:
   - **Lý do**: Đảm bảo chỉ những người dùng hợp lệ mới có thể truy cập hệ thống và thực hiện các chức năng nhất định.

2. **Quản lý thông tin nhân viên**:
   - **Lý do**: Hệ thống cần lưu trữ và quản lý thông tin của một số lượng lớn nhân viên (có thể lên đến hàng nghìn người).

3. **Tính toán tiền lương**:
   - **Lý do**: Hệ thống cần tính toán chính xác tiền lương cho từng nhân viên dựa trên số giờ làm việc, tỷ lệ lương, và các khoản phụ cấp.

4. **Quản lý thời gian làm việc (Timecard)**:
   - **Lý do**: Cần ghi lại thời gian làm việc của nhân viên để tính toán tiền lương.

5. **Tạo báo cáo**:
   - **Lý do**: Cung cấp báo cáo về tiền lương, thời gian làm việc, và các thông tin liên quan cho quản lý.

6. **Bảo mật và bảo vệ dữ liệu**:
   - **Lý do**: Dữ liệu về tiền lương và thông tin nhân viên rất nhạy cảm và cần được bảo vệ khỏi truy cập trái phép.

7. **Tích hợp với hệ thống hiện tại**:
   - **Lý do**: Hệ thống mới có thể cần truy cập thông tin từ các hệ thống hiện có hoặc được tích hợp với chúng.

### 2.2 Danh sách cơ chế
- a. Cơ chế xác thực người dùng
- b. Cơ chế phân quyền người dùng
- c. Cơ chế quản lý cơ sở dữ liệu
- d. Cơ chế tính toán tiền lương
- e. Cơ chế quản lý thời gian làm việc
- f. Cơ chế tạo báo cáo
- g. Cơ chế mã hóa dữ liệu và bảo vệ thông tin
- h. Cơ chế truy cập hệ thống hiện tại

