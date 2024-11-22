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

### 2. Maintain Timecard
#### Mục Đích
Cho phép nhân viên ghi chép và cập nhật thời gian làm việc của họ để đảm bảo tính chính xác của dữ liệu lương.

#### Các Đối Tượng Tham Gia
- Nhân viên

#### Luồng Chính
- **Truy Cập Timecard**: Nhân viên truy cập vào TimecardForm sau khi đăng nhập.
- **Nhập/Cập Nhật Giờ Làm**: Nhập hoặc cập nhật các giờ làm việc.
- **Gửi Timecard**: Lưu thẻ giờ và gửi thông tin đến hệ thống.
- **Xác Nhận Của Hệ Thống**: Hệ thống xác nhận thông tin đã được lưu thành công và cập nhật cơ sở dữ liệu.

#### Kết quả
Thẻ giờ được cập nhật trong hệ thống.

### 3. Run Payroll
#### Mục Đích
Xử lý và phân phối lương dựa trên thông tin thẻ giờ và các quy định lương áp dụng.

#### Các Đối Tượng Tham Gia
- Quản lý

#### Điều Kiện Tiên Quyết
Có ít nhất một thẻ giờ đã được nhập và xác minh trong hệ thống.

#### Luồng Chính
- **Khởi Tạo Quá Trình Chạy Lương**: Quản lý khởi tạo quá trình chạy lương.
- **Thu Thập Dữ Liệu Thẻ Giờ**: Hệ thống thu thập dữ liệu từ các thẻ giờ.
- **Tính Toán Lương**: Tính toán lương dựa trên dữ liệu thẻ giờ và các quy định.
- **Xử Lý Phương Thức Thanh Toán**: Chọn phương thức thanh toán (in séc hoặc chuyển khoản ngân hàng).
- **Phân Phối Lương**: Gửi lương đến nhân viên qua phương thức đã chọn.

#### Kết quả
Lương được xử lý và phân phối thành công đến nhân viên.

## Lý Do Đưa Ra Thiết Kế
- **Rõ Ràng Về Quyền Hạn và Nhiệm Vụ**: Mỗi ca sử dụng được thiết kế để phân biệt rõ ràng quyền hạn và nhiệm vụ của từng loại người dùng, nhằm đảm bảo an ninh thông tin và hiệu quả trong quản lý.
- **Minh Bạch và Dễ Theo Dõi**: Thiết kế này giúp quá trình làm việc trở nên minh bạch và dễ dàng theo dõi, từ đó tăng cường hiệu quả công việc và giảm thiểu sai sót.
- **Khả Năng Mở Rộng và Bảo Trì**: Hệ thống được thiết kế một cách linh hoạt, dễ dàng mở rộng và bảo trì, cho phép tích hợp với các công nghệ và hệ thống mới một cách dễ dàng.
