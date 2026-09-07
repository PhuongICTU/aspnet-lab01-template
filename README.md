# BÀI THỰC HÀNH 01  
## Làm quen với ASP.NET Core và GitHub

## 1. Mục tiêu

Sau khi hoàn thành bài thực hành, sinh viên có thể:

- Kiểm tra môi trường phát triển .NET.
- Tạo ứng dụng ASP.NET Core MVC.
- Sử dụng Visual Studio hoặc Visual Studio Code để phát triển ứng dụng.
- Nhận diện một số thành phần cơ bản của dự án ASP.NET Core MVC.
- Chỉnh sửa giao diện trang chủ.
- Tạo một endpoint đơn giản.
- Biên dịch và chạy ứng dụng bằng Kestrel.
- Commit và push mã nguồn lên GitHub.
- Xem kết quả chấm tự động bằng GitHub Actions.

## 2. Công cụ được phép sử dụng

Sinh viên được sử dụng một trong các môi trường sau:

- Visual Studio 2022;
- Visual Studio 2026;
- Visual Studio Code.

Yêu cầu chung:

- Cài đặt .NET 8 SDK.
- Dự án phải sử dụng framework `net8.0, .net10.0, .net 9.0`.
- Tên dự án phải là `Lab01.Web`.
- Không thay đổi tên hoặc vị trí các tệp do đề bài quy định.

### Visual Studio

Nếu sử dụng Visual Studio, cần cài workload:

```text
ASP.NET and web development
```

### Visual Studio Code

Nếu sử dụng Visual Studio Code, nên cài:

- C# Dev Kit;
- C#;
- .NET Install Tool.

## 3. Kiểm tra môi trường

Mở Terminal, Command Prompt hoặc PowerShell và chạy:

```bash
dotnet --version
dotnet --info
dotnet --list-sdks
git --version
```

Máy phải có .NET 8 SDK, ví dụ:

```text
8.0.xxx
```

## 4. Nhận repository bài tập

Mở repository được giảng viên cung cấp và chọn:

```text
Code → HTTPS → Copy URL
```

Clone repository:

```bash
git clone <repository-url>
cd <repository-name>
```

Không sử dụng **Download ZIP**, vì bài làm cần có lịch sử commit.

---

# PHẦN A. TẠO DỰ ÁN

Sinh viên chọn một trong hai cách dưới đây.

## Cách 1. Tạo bằng .NET CLI

Cách này phù hợp với Visual Studio Code và cũng có thể sử dụng trong Terminal của Visual Studio.

Tại thư mục gốc của repository, chạy:

```bash
dotnet new mvc -n Lab01.Web --framework net8.0 --no-https
```

Biên dịch dự án:

```bash
dotnet build Lab01.Web/Lab01.Web.csproj
```

Chạy ứng dụng:

```bash
dotnet run --project Lab01.Web/Lab01.Web.csproj
```

## Cách 2. Tạo bằng Visual Studio 2022 hoặc 2026

Thực hiện các bước sau:

1. Mở Visual Studio.
2. Chọn **Create a new project**.
3. Chọn mẫu:

```text
ASP.NET Core Web App (Model-View-Controller)
```

4. Nhập thông tin:

```text
Project name: Lab01.Web
Solution name: Lab01.Web
Location: thư mục gốc của repository
```

5. Chọn **Place solution and project in the same directory**.
6. Chọn **Next**.
7. Cấu hình:

```text
Framework: .NET 8.0
Authentication type: None
Configure for HTTPS: bỏ chọn
Enable Docker: bỏ chọn
```

8. Nhấn **Create**.

Sau khi tạo xong, phải bảo đảm có đường dẫn:

```text
Lab01.Web/Lab01.Web.csproj
```

Nếu `Lab01.Web.csproj` không nằm đúng đường dẫn trên, bài sẽ không được hệ thống nhận diện.

## Cấu trúc bắt buộc

```text
repository/
├── .github/
│   └── workflows/
│       └── autograding.yml
├── Lab01.Web/
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   │   └── Home/
│   │       └── Index.cshtml
│   ├── wwwroot/
│   ├── Program.cs
│   ├── appsettings.json
│   └── Lab01.Web.csproj
└── README.md
```

---

# PHẦN B. CÁ NHÂN HÓA TRANG CHỦ

Mở tệp:

```text
Lab01.Web/Views/Home/Index.cshtml
```

Thay nội dung bằng mẫu dưới đây:

```cshtml
@{
    ViewData["Title"] = "Trang chủ";
}

<div class="container mt-4">
    <div class="text-center">
        <h1 class="display-4">
            Ứng dụng ASP.NET Core đầu tiên
        </h1>

        <p class="lead">
            Môn học: Công nghệ phát triển ứng dụng
        </p>
    </div>

    <hr />

    <section>
        <h2>Thông tin sinh viên</h2>

        <p><strong>Họ và tên:</strong> Nguyễn Văn A</p>
        <p><strong>Mã sinh viên:</strong> DTC123456</p>
        <p><strong>Lớp:</strong> CNTT KXX</p>
        <p><strong>Phiên bản:</strong> .NET 8</p>
    </section>

    <section class="mt-4">
        <h2>Đặc điểm của ASP.NET Core</h2>

        <ul>
            <li>Mã nguồn mở và đa nền tảng.</li>
            <li>Tích hợp Dependency Injection.</li>
            <li>Sử dụng Kestrel làm web server mặc định.</li>
        </ul>
    </section>
</div>
```

Sinh viên phải thay:

```text
Nguyễn Văn A
DTC123456
CNTT KXX
```

bằng thông tin thật của mình.

Không được xóa các cụm từ bắt buộc:

```text
Ứng dụng ASP.NET Core đầu tiên
Công nghệ phát triển ứng dụng
Họ và tên
Mã sinh viên
Lớp
Kestrel
```

---

# PHẦN C. TẠO ENDPOINT KIỂM TRA

Mở tệp:

```text
Lab01.Web/Program.cs
```

Thêm đoạn mã sau vào trước `app.Run();`:

```csharp
app.MapGet("/health", () => "LAB01_OK");
```

Phần cuối của `Program.cs` cần có dạng:

```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.MapGet("/health", () => "LAB01_OK");

app.Run();
```

Không thay đổi chuỗi:

```text
LAB01_OK
```

---

# PHẦN D. CHẠY VÀ KIỂM TRA

## Sử dụng Visual Studio

Nhấn:

```text
Ctrl + F5
```

hoặc chọn:

```text
Debug → Start Without Debugging
```

## Sử dụng Visual Studio Code

Mở Terminal tại thư mục repository:

```bash
dotnet run --project Lab01.Web/Lab01.Web.csproj
```

Ứng dụng sẽ hiển thị một địa chỉ tương tự:

```text
http://localhost:5000
```

Số cổng có thể khác nhau trên từng máy.

Kiểm tra trang chủ:

```text
http://localhost:<port>/
```

Kiểm tra endpoint:

```text
http://localhost:<port>/health
```

Kết quả bắt buộc:

```text
LAB01_OK
```

Dừng ứng dụng bằng tổ hợp phím:

```text
Ctrl + C
```

---

# PHẦN E. COMMIT VÀ PUSH

Sinh viên phải có tối thiểu bốn commit.

## Commit 1. Tạo dự án

```bash
git add .
git commit -m "Create ASP.NET Core MVC project"
git push
```

## Commit 2. Hoàn thiện trang chủ

```bash
git add .
git commit -m "Customize student home page"
git push
```

## Commit 3. Tạo endpoint

```bash
git add .
git commit -m "Add health check endpoint"
git push
```

## Commit 4. Hoàn thiện bài

```bash
git add .
git commit -m "Complete Lab 01"
git push
```

Không sử dụng những commit message không rõ nghĩa như:

```text
update
fix
abc
123
nop bai
```

---

# PHẦN F. XEM KẾT QUẢ CHẤM TỰ ĐỘNG

Sau khi push:

1. Mở repository trên GitHub.
2. Chọn tab **Actions**.
3. Chọn workflow **Autograding Lab 01**.
4. Mở lần chạy mới nhất.
5. Kiểm tra các bước chấm.

Ký hiệu:

- Dấu tích xanh: kiểm tra thành công.
- Dấu X đỏ: có yêu cầu chưa đạt.
- Dấu tròn vàng: hệ thống đang kiểm tra.

Nếu bài chưa đạt:

1. Mở bước bị lỗi.
2. Đọc thông báo.
3. Sửa mã nguồn.
4. Chạy lại trên máy.
5. Commit và push lại.

---

# PHẦN G. TIÊU CHÍ ĐÁNH GIÁ

| Nội dung | Điểm |
|---|---:|
| Đúng tên và cấu trúc dự án | 1,0 |
| Dự án sử dụng `.NET 8` | 1,0 |
| Dự án biên dịch thành công | 2,0 |
| Trang chủ có đủ nội dung bắt buộc | 2,0 |
| Đã thay thông tin mẫu bằng thông tin thật | 1,0 |
| Endpoint `/health` hoạt động đúng | 2,0 |
| Có tối thiểu bốn commit hợp lệ | 1,0 |
| **Tổng cộng** | **10,0** |

Hệ thống tự động kiểm tra 9 điểm đầu tiên. Giảng viên kiểm tra lịch sử commit để chấm 1 điểm còn lại.

## Lưu ý

- Không đổi tên dự án `Lab01.Web`.
- Không đổi framework khỏi `.NET 8`.
- Không sửa hoặc xóa workflow chấm tự động.
- Không đưa các thư mục `bin`, `obj` và `.vs` lên GitHub.
- Sinh viên chịu trách nhiệm kiểm tra trạng thái Actions trước thời hạn nộp bài.
