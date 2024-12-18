
# 1. Subsystem Context Diagrams

## 1.1 Hệ Thống Ngân Hàng (BankSystem)

### **Mô Tả**
Hệ thống Ngân Hàng chịu trách nhiệm xử lý các giao dịch tài chính trong tổ chức, đặc biệt là thanh toán lương cho nhân viên. Mỗi khi đến ngày thanh toán lương, hệ thống sẽ tự động chuyển tiền vào tài khoản của từng nhân viên. Ngoài ra, hệ thống cũng cho phép nạp tiền vào tài khoản ngân hàng của nhân viên thông qua các giao dịch từ hệ thống ngân hàng.
### **Sơ Đồ**
![Sơ Đồ BankSystem](https://www.plantuml.com/plantuml/png/jPB1JiCm38RlVGghbmt1zW3JL4qW3hqXzWGXzRQeQLB5AQA2lJk9wJ9IZICvLB7zv_Flf3lomlcXqqKlP2kE2EMZCAqoHzWFRpIInww4pmB2Mi2JDTvP3L8B8ixn3bx46D9wAcjqiDtAdw2gfjDntRl1JDhb7MVFnOIkZKTt418vLfS8wcXdppu2DAboR8Ez9UMN8i3b2MMxWSlk8R9iX6mWVcjpiAuJNbapSv3cXTxPZ_7NU9a5ocN_OEJPUEKLpYwO8Q4_nYgtJQUIRCRzKxs0LzGiePFgkT6DDrojgkpwDr0sog7qC8r9mAO8tfKe6PAzrjTw3TUOwzUGwMciW1u8gRmbcW-LjETYXwQ9_-ut)
### **Các Thành Phần**
- **PayrollController**: Điều khiển quy trình thanh toán lương cho nhân viên, đảm bảo việc chuyển tiền đúng hạn.
- **IBankSystem (Giao diện)**: Định nghĩa các phương thức cần thiết để thực hiện các giao dịch ngân hàng, bao gồm việc nạp tiền vào tài khoản nhân viên.
- **BankSystem (Proxy)**: Là lớp proxy đại diện cho hệ thống ngân hàng thực tế, thực hiện giao dịch thanh toán lương vào tài khoản nhân viên.
- **Paycheck**: Đại diện cho bảng lương của nhân viên, chứa thông tin về lương, phụ cấp, và các khoản khấu trừ.
- **BankInformation**: Chứa thông tin tài khoản ngân hàng của nhân viên, giúp xác định tài khoản cần chuyển tiền.

### **Giao Diện (IBankSystem)**
- **deposit(aPaycheck: Paycheck, intoBank: BankInformation)**: Phương thức này thực hiện việc nạp tiền vào tài khoản ngân hàng của nhân viên, nhận vào thông tin bảng lương và tài khoản ngân hàng.

---

## 1.2 Dịch Vụ In (PrintService)

### **Mô Tả**
Dịch vụ In hỗ trợ việc tạo ra các báo cáo lương và các tài liệu liên quan, và cung cấp khả năng in các báo cáo khi cần thiết. Đây là một dịch vụ quan trọng giúp quản lý các báo cáo liên quan đến công việc quản lý nhân sự và lương của nhân viên.
### **Sơ Đồ**
![Sơ Đồ PrintService](https://www.plantuml.com/plantuml/png/dP0n2y8m48Nt-nL79rs2hgM4WfERw2y8xLa3CIcNQnt4_sxRe92wcILvZ_Vb7bT7CIp3tG4qpiI89xPU3i4B1-U8yGaudNvspzG7biqMNW2J9BwQXl2u41VYqKxgDsxIZIMcnuAdMV-JoG1OjorsIkqBL6oxcoZzqNd74Zlon4Oe8YyVHHojWJnLgJOylC8LMbL39AqXirDKVslLvDjvfsy0)
### **Các Thành Phần**
- **PrintController**: Điều khiển các yêu cầu tạo và in các báo cáo. Nó gọi các phương thức của dịch vụ in thực tế để hoàn tất việc in ấn.
- **IPrintService (Giao diện)**: Định nghĩa các phương thức cần thiết cho việc in báo cáo. Giao diện này giúp tạo sự nhất quán trong cách dịch vụ in được thực hiện trong hệ thống.
- **PrintService (Proxy)**: Đại diện cho dịch vụ in thực tế, cung cấp khả năng in các báo cáo. Proxy này có thể bao gồm các cơ chế bảo mật và xác thực người dùng trước khi in.
- **Report**: Đại diện cho các báo cáo cần in, ví dụ như bảng lương, danh sách nhân viên, báo cáo tài chính.

### **Giao Diện (IPrintService)**
- **printReport(aReport: Report)**: Phương thức này thực hiện việc in một báo cáo đã được tạo ra, dựa trên đối tượng báo cáo được truyền vào.

---

## 1.3 Cơ Sở Dữ Liệu Quản Lý Dự Án (ProjectManagementDatabase)

### **Mô Tả**
Hệ thống Cơ Sở Dữ Liệu Quản Lý Dự Án quản lý các hoạt động liên quan đến các dự án trong tổ chức. Hệ thống này bao gồm việc cập nhật, truy vấn thông tin dự án và theo dõi tiến độ của từng dự án.
### **Sơ Đồ**
![Sơ Đồ ProjectManagementDatabase](https://www.plantuml.com/plantuml/png/hP6nZi8m38PtFuNLwMv8TBTMLLJfRhdX95x1jAOKfKcLk30WtfqMMJ0WEf79Jln_Vtwvpa99fi43D9vonasA1sxa9mP9qNjEU0QSpq21EjRNZq-u0FH1EEseOVpJ-__RqC11VabeIvbLFOqjoLrDMc29MYqy_S3xKG3FeOelQxyBDAdlzcASzcj1IdNEEAhbt14UUu8LLMNRU0eMrxXLDMLs3bxFc0LYt2DGpQ5TbdO5)
### **Các Thành Phần**
- **ProjectController**: Quản lý các yêu cầu thay đổi và cập nhật thông tin dự án. Thành phần này có thể nhận yêu cầu từ người dùng để thay đổi thông tin của dự án.
- **IProjectManagementDatabase (Giao diện)**: Định nghĩa các phương thức cần thiết để tương tác với cơ sở dữ liệu dự án, bao gồm việc thêm, cập nhật và truy vấn thông tin dự án.
- **ProjectManagementDatabase (Proxy)**: Lớp proxy đại diện cho cơ sở dữ liệu quản lý dự án thực tế, thực hiện việc kết nối và thao tác với cơ sở dữ liệu.
- **Project**: Đại diện cho một dự án trong hệ thống. Lớp này chứa các thông tin về tên dự án, tiến độ, tài nguyên, và các thông tin khác liên quan đến dự án.

### **Giao Diện (IProjectManagementDatabase)**
- **updateProject(aProject: Project)**: Phương thức này cập nhật thông tin của dự án trong cơ sở dữ liệu, bao gồm việc thay đổi các thông tin về tiến độ, người quản lý và các tài nguyên liên quan.

# 2. Analysis Class to Design Element Map

| Analysis Class              | Design Elements                                             |
|-----------------------------|-------------------------------------------------------------|
| LoginForm                   | LoginForm                                                   |
| MaintainTimecardForm        | MainEmployeeForm, TimecardForm, MainApplicationForm         |
| TimecardController          | TimecardController                                          |
| SystemClockInterface        | SystemClockInterface                                        |
| PayrollController           | PayrollController                                           |
| Paycheck                    | Paycheck                                                    |
| Employee                    | Employee, EmployeeForm, EmployeeController                  |
| PurchaseOrder               | PurchaseOrder, PurchaseOrderForm, PurchaseOrderController   |
| BankSystemInterface         | BankSystemInterface, BankSystemProxy                        |
| PrintService                | PrintService, PrintController                               |
| ProjectManagementDatabase   | ProjectManagementDatabase, DatabaseController               |
| PaycheckCalculator          | PaycheckCalculator, SalaryCalculator                        |
| CommissionedEmployee        | CommissionedEmployeeForm, CommissionedEmployeeController    |
| EmployeeDatabase            | EmployeeDatabase, DatabaseService                           |
| PayrollDatabase             | PayrollDatabase, DatabaseController                         |
| PaymentMethod               | PaymentMethod, DirectDeposit, CheckPayment                  |
| Timecard                    | Timecard, TimecardEntryForm                                 |
| BankInformation             | BankInformation, BankService                                |

# 3. Design Element to Owning Package Map

| Design Element              | Owning Package                           |
|-----------------------------|------------------------------------------|
| LoginForm                   | Middleware::Security:GUI Framework       |
| MainEmployeeForm            | Applications::Employee Activities        |
| TimecardForm                | Applications::Employee Activities        |
| MainApplicationForm         | Middleware::Security:GUI Framework       |
| TimecardController          | Applications::Employee Activities        |
| SystemClockInterface        | Applications::Payroll                    |
| PayrollController           | Applications::Payroll                    |
| Paycheck                    | Business Services::Payroll Artifacts     |
| Employee                    | Applications::Employee Activities        |
| PurchaseOrder               | Business Services::Purchase Management   |
| BankSystemInterface         | Business Services::Bank Integration      |
| PrintService                | Business Services::Printing              |
| ProjectManagementDatabase   | Infrastructure::Database Management      |
| PaycheckCalculator          | Business Services::Payroll Artifacts     |
| CommissionedEmployee        | Applications::Employee Activities        |
| EmployeeDatabase            | Infrastructure::Database Management      |
| PayrollDatabase             | Infrastructure::Database Management      |
| PaymentMethod               | Business Services::Payment Integration   |
| Timecard                    | Applications::Employee Activities        |
| BankInformation             | Business Services::Bank Integration      |
# 4. Architectural layers and their dependencies
![Sơ Đồ Architectural](https://www.plantuml.com/plantuml/png/ZPB1IiD048Rl-nH3Jthf0tYGLkkX444eFKaEmpfPbpQpPMPMBEAxssWMab0ajy3Cz-N_XrsfeLXkZquFaKyes4AREFbtIIs1IIRdJkWF60WMBq9AR6WnCLHu9e6R_VPs0LyEu7Ml9B1b8sdGK-s-1-H3riYa2bKAqHTsH_8HFManF2OX6A-EDHiqXBM_85eSctLLyD_fCp86QebjZ7R1WWoYzz3Jfv4m7g4F0uF5gQ4HL9FiBGkD99Ue8NAek-yT-IpHplLV8svYo0FTz4omNDvVRmvta9NKNHzssBJn3EJ_leMVYdksr9pnctA5ERlZ8nN0hOZVkfVv0m00)

