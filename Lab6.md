
# Thiết Kế Lớp - Hệ Thống Payroll System

## 1. BankSystem::deposit

### **Phân tích chi tiết**

#### **Lớp và thuộc tính**:
- **BankSystem**: Đại diện hệ thống ngân hàng.
- **BankTransaction**: Quản lý giao dịch.
- **Paycheck**: Đại diện bảng lương, chứa số tiền và thông tin nhân viên.
- **BankInformation**: Thông tin ngân hàng (tên, số định tuyến).

#### **Phương thức (operations)**:
- `BankSystem.deposit(Paycheck, BankInformation)`
- `BankTransaction.create(op, amount, routingNum)`
- `BankTransaction.submit()`

#### **Biểu đồ lớp (Class Diagram)**:
```plantuml
@startuml
class BankSystem {
    + deposit(Paycheck, BankInformation): void
}

class BankTransaction {
    + create(op: String, amount: double, routingNum: String): void
    + submit(): void
}

class Paycheck {
    - amount: double
    - employeeInfo: String
}

class BankInformation {
    - bankName: String
    - routingNumber: String
}

BankSystem --> BankTransaction
BankTransaction --> Paycheck
Paycheck --> BankInformation
@enduml
```

#### **Biểu đồ trạng thái (State Diagram)**:
```plantuml
@startuml
state "Khởi tạo" as Init
state "Đang xử lý" as Processing
state "Hoàn tất" as Completed

Init --> Processing: Tạo giao dịch
Processing --> Completed: Gửi giao dịch
@enduml
```

---

## 2. PrintService::print

### **Phân tích chi tiết**

#### **Lớp và thuộc tính**:
- **PrintService**: Quản lý việc in.
- **PaycheckPrinterImage**: Tạo hình ảnh in từ bảng lương.
- **PrinterInterface**: Kết nối với máy in.
- **Employee**: Thông tin nhân viên.

#### **Phương thức (operations)**:
- `PrintService.print(Paycheck, String)`
- `PaycheckPrinterImage.buildPrintImage(fromPaycheck)`

#### **Biểu đồ lớp (Class Diagram)**:
```plantuml
@startuml
class PrintService {
    + print(Paycheck, printerName: String): void
}

class PaycheckPrinterImage {
    + buildPrintImage(fromPaycheck: Paycheck): Image
}

class Paycheck {
    - amount: double
    - employeeInfo: String
}

PrintService --> PaycheckPrinterImage
PaycheckPrinterImage --> Paycheck
@enduml
```

#### **Biểu đồ trạng thái (State Diagram)**:
```plantuml
@startuml
state "Chuẩn bị in" as Prepare
state "Đang in" as Printing
state "Hoàn thành" as Done

Prepare --> Printing: Bắt đầu in
Printing --> Done: Hoàn tất in
@enduml
```

---

## 3. ProjectManagementDatabase::getChargeNumbers

### **Phân tích chi tiết**

#### **Lớp và thuộc tính**:
- **ProjectManagementDatabase**: Đại diện hệ thống cơ sở dữ liệu.
- **ChargeNumList**: Danh sách số tính phí.
- **ChargeNum**: Đối tượng số tính phí, chứa tên dự án và giá trị.

#### **Phương thức (operations)**:
- `getChargeNumbers(String): ChargeNumList`
- `ChargeNumList.add(theChargeNum)`

#### **Biểu đồ lớp (Class Diagram)**:
```plantuml
@startuml
class ProjectManagementDatabase {
    + getChargeNumbers(query: String): ChargeNumList
}

class ChargeNumList {
    + add(chargeNum: ChargeNum): void
}

class ChargeNum {
    - projectName: String
    - chargeValue: double
}

ProjectManagementDatabase --> ChargeNumList
ChargeNumList --> ChargeNum
@enduml
```

#### **Biểu đồ trạng thái (State Diagram)**:
```plantuml
@startuml
state "Rỗng" as Empty
state "Đang cập nhật" as Updating
state "Hoàn tất" as Complete

Empty --> Updating: Thêm dữ liệu
Updating --> Complete: Hoàn tất danh sách
@enduml
```

---

## 4. ProjectManagementDatabase::initialize

### **Phân tích chi tiết**

#### **Lớp và thuộc tính**:
- **DBChargeNumbers**: Kết nối cơ sở dữ liệu.
- **DriverManager**: Quản lý kết nối.

#### **Phương thức (operations)**:
- `initialize()`: Thiết lập kết nối.
- `getConnection(url, user, pass): Connection`

#### **Biểu đồ lớp (Class Diagram)**:
```plantuml
@startuml
class DBChargeNumbers {
    + initialize(): void
}

class DriverManager {
    + getConnection(url: String, user: String, pass: String): Connection
}

DBChargeNumbers --> DriverManager
@enduml
```

#### **Biểu đồ trạng thái (State Diagram)**:
```plantuml
@startuml
state "Chưa kết nối" as Disconnected
state "Đang kết nối" as Connecting
state "Kết nối thành công" as Connected

Disconnected --> Connecting: Thiết lập kết nối
Connecting --> Connected: Kết nối thành công
@enduml
```

---

