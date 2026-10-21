# BÀI LÀM – ÔN TẬP NGÀY 2

- **Họ tên:** Bùi Hải Đăng
- **Lớp:** CNTT2
- **Link repository:**
- **Hệ điều hành (Windows/macOS):** Window

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content logs/access.log | Select-String "ERROR" > logs/error_report.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content logs/error_report.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\error_report.txt | Select-Object -First 2
```

### 2 dòng lỗi đầu tiên trong error_report.txt

```text

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)

## Bài 2. Đếm bằng pipeline

### Lệnh

```shell
\Get-Content .\logs\access.log | Select-String "WARNING" | Measure-Object | Select-Object -ExpandProperty Count
Get-Content .\logs\payment.log | Select-String "ERROR" | Measure-Object | Select-Object -ExpandProperty Count
```

### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log: 4
ERROR trong payment.log: 3
```

## Bài 3. Chạy script auto_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell

PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Write-Host "Dang loc canh bao thanh toan..."
Dang loc canh bao thanh toan...
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> "=== CANH BAO THANH TOAN ===" > logs/warning_report.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content logs/payment.log | Select-String "WARNING" >> logs/warning_report.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Write-Host "Hoan thanh!"
Hoan thanh!
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> .\auto_warning.ps1

```

### Nội dung file logs/warning_report.txt

```text
=== CANH BAO THANH TOAN ===
2025-10-18 10:15:30 [WARNING] Cong thanh toan Phan hoi cham (timeout > 5s)
2025-10-18 14:22:01 [WARNING] Tai khoan Ngan hang ghi nhận giao dịch trung lap

```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> "=== TONG HOP ACCESS LOG ===" > logs/tong_hop_ngay2.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content logs/access.log | Select-String "ERROR" >> logs/tong_hop_ngay2.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> (Get-Content logs/payment.log | Select-String "WARNING" | Measure-Object -Line).Lines >> logs/tong_hop_ngay2.txt
PS C:\Users\BUI HAI DANG\Desktop\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\tong_hop_ngay2.txt
```

### Nội dung file logs/tong_hop_ngay2.txt

```text
=== TONG HOP ACCESS LOG ===

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout)

```

## Bài 5. Câu hỏi ngắn

- **a)  Toán tử ">" ghi đè nội dung file (nếu file đã tồn tại thì toàn bộ nội dung cũ sẽ bị xóa hoàn toàn để thay bằng nội dung mới, nếu file chưa tồn tại sẽ tạo mới). Còn toán tử ">>" ghi nối tiếp nội dung mới vào cuối file mà không làm mất hoặc xóa đi các dòng nội dung cũ đã có trước đó.**
- **b) Dòng tiêu đề "=== TONG HOP ACCESS LOG ===" vừa được ghi ở lệnh đầu tiên sẽ bị xóa hoàn toàn. File "tong_hop_ngay2.txt" sẽ chỉ còn chứa nội dung của các dòng ERROR thu được từ lệnh thứ hai.**
- **c) Đường dẫn tương đối giúp script có tính linh hoạt và khả năng di động cao, có thể chạy đúng trên bất kỳ máy tính hay môi trường làm việc nào khi thư mục dự án được di chuyển hoặc tải về. Đường dẫn tuyệt đối cố định vị trí thư mục cá nhân, nên sẽ bị lỗi "File not found" khi mở và thực thi trên máy khác.**

## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** ..../100
- **Lỗi mình đã mắc và cách sửa:**
