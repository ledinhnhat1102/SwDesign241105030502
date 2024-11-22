# Thiết Kế Ca Sử Dụng cho Hệ Thống "Payroll System"

## Tổng Quan
Hệ thống lương được thiết kế để tự động hóa quá trình tính toán, lưu trữ và phân phối tiền lương cho nhân viên. Các ca sử dụng chính bao gồm "Login", "Maintain Timecard", và "Run Payroll". Mỗi ca sử dụng được thiết kế để đáp ứng nhu cầu cụ thể của các bên liên quan khác nhau trong tổ chức.

## Các Ca Sử Dụng Chính

### 1. Login
#### Mục Đích
Cho phép người dùng truy cập an toàn vào hệ thống để quản lý và xem xét thông tin liên quan đến lương và thời gian làm việc.

#### Các Đối Tượng Tham Gia
- Người dùng (nhân viên hoặc quản lý).

#### Luồng Chính
- **Người Dùng Nhập Thông Tin**: Người dùng nhập tên đăng nhập và mật khẩu vào giao diện LoginForm.
- **Hệ Thống Xác Thực Thông Tin**: Hệ thống kiểm tra thông tin đăng nhập với cơ sở dữ liệu.
  - **Thành Công**: Người dùng được phép truy cập vào các tính năng của hệ thống.
  - **Thất Bại**: Hệ thống hiển thị thông báo lỗi và yêu cầu nhập lại thông tin.

#### Kết quả
Người dùng được truy cập hệ thống hoặc được thông báo lỗi nếu thông tin không hợp lệ.

---

### 2. Maintain Timecard
#### Mục Đích
Cho phép nhân viên ghi chép và cập nhật thời gian làm việc của họ để đảm bảo tính chính xác của dữ liệu lương.

#### Các Đối Tượng Tham Gia
- Nhân viên.

#### Luồng Chính
- **Truy Cập Timecard**: Nhân viên truy cập vào TimecardForm sau khi đăng nhập.
- **Nhập/Cập Nhật Giờ Làm**: Nhập hoặc cập nhật các giờ làm việc.
- **Gửi Timecard**: Lưu thẻ giờ và gửi thông tin đến hệ thống.
- **Xác Nhận Của Hệ Thống**: Hệ thống xác nhận thông tin đã được lưu thành công và cập nhật cơ sở dữ liệu.

#### Kết quả
Thẻ giờ được cập nhật trong hệ thống.

---

### 3. Run Payroll
#### Mục Đích
Xử lý và phân phối lương dựa trên thông tin thẻ giờ và các quy định lương áp dụng.

#### Các Đối Tượng Tham Gia
- Quản lý.

#### Điều Kiện Tiên Quyết
- Có ít nhất một thẻ giờ đã được nhập và xác minh trong hệ thống.

#### Luồng Chính
- **Khởi Tạo Quá Trình Chạy Lương**: Quản lý khởi tạo quá trình chạy lương.
- **Thu Thập Dữ Liệu Thẻ Giờ**: Hệ thống thu thập dữ liệu từ các thẻ giờ.
- **Tính Toán Lương**: Tính toán lương dựa trên dữ liệu thẻ giờ và các quy định.
- **Xử Lý Phương Thức Thanh Toán**: Chọn phương thức thanh toán (in séc hoặc chuyển khoản ngân hàng).
- **Phân Phối Lương**: Gửi lương đến nhân viên qua phương thức đã chọn.

#### Kết quả
Lương được xử lý và phân phối thành công đến nhân viên.

---

## Các Ca Sử Dụng Bổ Sung

### 4. Edit Employee Information
#### Mục Đích
Cho phép quản lý hoặc nhân viên cập nhật thông tin cá nhân và lao động.

#### Các Đối Tượng Tham Gia
- Quản lý, Nhân viên.

#### Luồng Chính
- **Truy Cập Thông Tin**: Truy cập thông tin cá nhân hoặc hợp đồng lao động.
- **Cập Nhật Thông Tin**: Thực hiện cập nhật thông tin cần thiết.
- **Xác Nhận Của Hệ Thống**: Hệ thống lưu và xác nhận thay đổi.

#### Kết quả
Thông tin nhân viên được cập nhật.

---

### 5. Generate Reports
#### Mục Đích
Tạo báo cáo lương và báo cáo giờ làm cho quản lý hoặc yêu cầu bên ngoài.

#### Các Đối Tượng Tham Gia
- Quản lý.

#### Luồng Chính
- **Chọn Báo Cáo**: Chọn loại báo cáo (lương hoặc giờ làm) và tiêu chí (khoảng thời gian, phòng ban, nhân viên).
- **Xử Lý Báo Cáo**: Hệ thống xử lý dữ liệu dựa trên tiêu chí.
- **Tạo và Phân Phối Báo Cáo**: Hệ thống tạo báo cáo và phân phối theo yêu cầu.

#### Kết quả
Báo cáo được tạo và phân phối.

---

### 6. Handle Exceptions
#### Mục Đích
Xử lý các ngoại lệ hoặc lỗi trong quá trình nhập dữ liệu hoặc xử lý lương.

#### Các Đối Tượng Tham Gia
- Quản lý, Hệ thống IT.

#### Luồng Chính
- **Phát Hiện Sự Cố**: Hệ thống hoặc người dùng phát hiện lỗi hoặc ngoại lệ.
- **Báo Cáo và Xử Lý**: Hệ thống báo cáo lỗi cho quản lý hoặc IT xử lý.
- **Xác Nhận Xử Lý Thành Công**: Hệ thống hoặc IT khắc phục lỗi và tiếp tục quá trình.

#### Kết quả
Sự cố được xử lý, hệ thống tiếp tục hoạt động bình thường.

---

## Lý Do Đưa Ra Thiết Kế

- **Hiệu Quả Quản Lý**: Tất cả các ca sử dụng được thiết kế để tối đa hóa hiệu quả quản lý và minh bạch trong quá trình làm việc.
- **Dễ Dàng Bảo Trì và Mở Rộng**: Hệ thống được thiết kế để dễ dàng bảo trì và mở rộng, hỗ trợ tích hợp với các công nghệ mới và thay đổi trong quy trình doanh nghiệp.
- **Tối Ưu Hóa Trải Nghiệm Người Dùng**: Giao diện người dùng thân thiện và dễ dàng truy cập, giúp người dùng dễ dàng thao tác và giảm thiểu lỗi.
