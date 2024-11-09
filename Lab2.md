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

---

## 1.4 Biểu đồ tuần tự (Sequence Diagram) cho "Record Purchase Orders"

![Diagram](https://www.plantuml.com/plantuml/png/VP6nJiOm38HtFuL762hs3gWIb1LUmKsCY9J4bUqCVNje4KX_ex_h-UxpoPxCIRsL31HS5EUoPjcOOP5M8-c67qt35nc_QsHz4oqGfBfAlfsy_8gP5RXwybCGu8-CmtFF776kpego2nZPAMM3plQVxRUEQ6qfoG_vuU2yajCZtF5tg163CZbV0t2uhX02cprz_jHlogXigrJZonBzBMAoDTDsni74DUwl-WO0)

Biểu đồ này minh họa cách các đối tượng giao tiếp trong quá trình ghi nhận đơn hàng của nhân viên.

### **Tác nhân:**  
- **Employee**

### **Các đối tượng:**  
- **PurchaseOrderForm (Boundary)**
- **PurchaseOrderController (Control)**
- **PurchaseOrder (Entity)**
- **CommissionEmployee (Entity)**

### **Các bước:**
1. **Employee** mở giao diện **PurchaseOrderForm**.
2. **Employee** nhập thông tin đơn hàng (ngày giao dịch, giá trị) và nhấn "Lưu".
3. **PurchaseOrderForm** gọi phương thức `submitOrder()` trên **PurchaseOrderController**.
4. **PurchaseOrderController** xác thực thông tin và gọi `createOrder()` trên **PurchaseOrder** để lưu dữ liệu.
5. **PurchaseOrder** lưu dữ liệu và trả về kết quả (thành công hoặc lỗi).
6. **PurchaseOrderController** gửi phản hồi tới **PurchaseOrderForm** để hiển thị thông báo cho **Employee**.

---

## 1.5 Biểu đồ lớp (Class Diagram) cho "Record Purchase Orders"
![Diagram](https://www.plantuml.com/plantuml/png/ZP71IWD138RlynGvhiY-m1waK2rugYXuZxD11p8JoMGAKdntEqjRg-EoNaBu-FF_2LbbGxKIsNd6dE6Xg7_3J5iTIJUY4VOEu3gNbnXiWftKUek60snFxPNxT7yvh2MP2ZFfFtsgQ8SSHZHQa7cbLhIuqt6JNcfxFmxmP1hIQqKKtra-Y7xIapKDKEiPFIEN0zkme4sduOwwYyorn1Xo3fBkZhwmdq_nP_KZsgMjH_Q53-pRhslofzZsTNr_C_SEDyD_pomesoFTYj9O8dy1)
### **Các lớp và mối quan hệ:**

- **PurchaseOrderForm (Boundary)**
  - **Attributes:** None
  - **Methods:**
    - `submitOrder(orderData: OrderData)`

- **PurchaseOrderController (Control)**
  - **Attributes:** None
  - **Methods:**
    - `submitOrder(orderData: OrderData)`
    - `validateOrder(orderData: OrderData)`
    - `createOrder(orderData: OrderData)`

- **PurchaseOrder (Entity)**
  - **Attributes:**
    - `orderId: String`
    - `employeeId: String`
    - `orderDate: Date`
    - `orderValue: Float`
  - **Methods:**
    - `save()`

- **CommissionEmployee (Entity)**
  - **Attributes:**
    - `employeeId: String`
    - `commissionRate: Float`
  - **Methods:**
    - `calculateCommission(orderValue: Float)`

### **Quan hệ:**
- **PurchaseOrderController** tương tác với **PurchaseOrderForm** (hướng 1 chiều từ Form sang Controller).
- **PurchaseOrderController** quản lý **PurchaseOrder** và liên kết đến **CommissionEmployee** để tính hoa hồng nếu cần.


# Mã nguồn Java cho mô phỏng ca sử dụng "Maintain Timecard"

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

// Lớp đại diện cho Timecard
class Timecard {
    private String employeeId;
    private String date;
    private int hoursWorked;

    public Timecard(String employeeId, String date, int hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public String getDate() {
        return date;
    }

    public int getHoursWorked() {
        return hoursWorked;
    }

    public void setHoursWorked(int hoursWorked) {
        this.hoursWorked = hoursWorked;
    }

    public void displayInfo() {
        System.out.println("Employee ID: " + employeeId + ", Date: " + date + ", Hours Worked: " + hoursWorked);
    }
}

// Lớp quản lý các Timecard
class TimecardManager {
    private List<Timecard> timecards;

    public TimecardManager() {
        timecards = new ArrayList<>();
    }

    // Thêm timecard
    public void addTimecard(String employeeId, String date, int hoursWorked) {
        Timecard timecard = new Timecard(employeeId, date, hoursWorked);
        timecards.add(timecard);
        System.out.println("Timecard added for Employee ID: " + employeeId);
    }

    // Sửa timecard theo employeeId và date
    public void editTimecard(String employeeId, String date, int newHoursWorked) {
        for (Timecard timecard : timecards) {
            if (timecard.getEmployeeId().equals(employeeId) && timecard.getDate().equals(date)) {
                timecard.setHoursWorked(newHoursWorked);
                System.out.println("Timecard updated for Employee ID: " + employeeId + " on " + date);
                return;
            }
        }
        System.out.println("Timecard not found for Employee ID: " + employeeId + " on " + date);
    }

    // Xóa timecard
    public void deleteTimecard(String employeeId, String date) {
        timecards.removeIf(tc -> tc.getEmployeeId().equals(employeeId) && tc.getDate().equals(date));
        System.out.println("Timecard deleted for Employee ID: " + employeeId + " on " + date);
    }

    // Hiển thị tất cả timecards
    public void displayTimecards() {
        if (timecards.isEmpty()) {
            System.out.println("No timecards available.");
        } else {
            for (Timecard timecard : timecards) {
                timecard.displayInfo();
            }
        }
    }
}

// Lớp Main để mô phỏng ca sử dụng "Maintain Timecard"
public class Main {
    public static void main(String[] args) {
        TimecardManager manager = new TimecardManager();
        Scanner scanner = new Scanner(System.in);
        boolean exit = false;

        while (!exit) {
            System.out.println("\n--- Maintain Timecard Menu ---");
            System.out.println("1. Add Timecard");
            System.out.println("2. Edit Timecard");
            System.out.println("3. Delete Timecard");
            System.out.println("4. Display All Timecards");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Đọc bỏ dòng xuống hàng

            switch (choice) {
                case 1:
                    System.out.print("Enter Employee ID: ");
                    String employeeId = scanner.nextLine();
                    System.out.print("Enter Date (yyyy-mm-dd): ");
                    String date = scanner.nextLine();
                    System.out.print("Enter Hours Worked: ");
                    int hoursWorked = scanner.nextInt();
                    manager.addTimecard(employeeId, date, hoursWorked);
                    break;
                case 2:
                    System.out.print("Enter Employee ID: ");
                    employeeId = scanner.nextLine();
                    System.out.print("Enter Date (yyyy-mm-dd): ");
                    date = scanner.nextLine();
                    System.out.print("Enter New Hours Worked: ");
                    int newHoursWorked = scanner.nextInt();
                    manager.editTimecard(employeeId, date, newHoursWorked);
                    break;
                case 3:
                    System.out.print("Enter Employee ID: ");
                    employeeId = scanner.nextLine();
                    System.out.print("Enter Date (yyyy-mm-dd): ");
                    date = scanner.nextLine();
                    manager.deleteTimecard(employeeId, date);
                    break;
                case 4:
                    manager.displayTimecards();
                    break;
                case 5:
                    exit = true;
                    break;
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }

        scanner.close();
    }
}

