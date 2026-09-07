# BÀI THỰC HÀNH 01
## Làm quen với ASP.NET Core và GitHub

## 1. Mục tiêu

Sau khi hoàn thành bài thực hành, sinh viên có thể:

- Kiểm tra môi trường và phiên bản .NET SDK.
- Tạo ứng dụng ASP.NET Core MVC.
- Sử dụng Visual Studio hoặc Visual Studio Code.
- Nhận diện cấu trúc cơ bản của dự án ASP.NET Core MVC.
- Chỉnh sửa Razor View có sẵn.
- Tạo một endpoint đơn giản.
- Biên dịch và chạy ứng dụng bằng Kestrel.
- Commit và push mã nguồn lên GitHub.
- Kiểm tra kết quả bằng GitHub Actions.

## 2. Công cụ được phép sử dụng

Sinh viên được sử dụng một trong các môi trường sau:

- Visual Studio 2022;
- Visual Studio 2026;
- Visual Studio Code.

Ứng dụng được phép sử dụng một trong các phiên bản:

```text
.NET 8.0
.NET 9.0
.NET 10.0
```

Target Framework tương ứng:

| Phiên bản | Target Framework |
|---|---|
| .NET 8 | `net8.0` |
| .NET 9 | `net9.0` |
| .NET 10 | `net10.0` |

Sinh viên chỉ chọn một phiên bản phù hợp với SDK đã cài trên máy.

Các yêu cầu chung:

- Tên dự án bắt buộc là `Lab01.Web`.
- Dự án phải sử dụng `net8.0`, `net9.0` hoặc `net10.0`.
- Không đổi tên hoặc vị trí các tệp được quy định trong đề bài.
- Không sửa hoặc xóa workflow chấm tự động.

## 3. Chuẩn bị môi trường

### Visual Studio

Nếu sử dụng Visual Studio, cần cài workload:

```text
ASP.NET and web development
```

Sinh viên chỉ chọn phiên bản .NET xuất hiện và được hỗ trợ trong Visual Studio đang sử dụng.

### Visual Studio Code

Nếu sử dụng Visual Studio Code, nên cài:

- C# Dev Kit;
- C#;
- .NET Install Tool.

## 4. Kiểm tra .NET SDK

Mở Terminal, Command Prompt hoặc PowerShell:

```bash
dotnet --version
dotnet --info
dotnet --list-sdks
git --version
```

Ví dụ máy có thể hiển thị:

```text
8.0.xxx
9.0.xxx
10.0.xxx
```

Sinh viên phải chọn Target Framework tương ứng với SDK đã được cài đặt.

## 5. Nhận repository bài tập

Mở đường dẫn Assignment do giảng viên cung cấp và chọn:

```text
Accept assignment
```

Sau khi repository được tạo, chọn:

```text
Code → HTTPS → Copy URL
```

Clone repository:

```bash
git clone <repository-url>
cd <repository-name>
```

Không sử dụng **Download ZIP**, vì bài làm cần có lịch sử commit.

# PHẦN A. TẠO DỰ ÁN

Sinh viên chọn một trong hai cách sau.

## Cách 1. Sử dụng .NET CLI

### Lựa chọn .NET 8

```bash
dotnet new mvc -n Lab01.Web --framework net8.0 --no-https
```

### Lựa chọn .NET 9

```bash
dotnet new mvc -n Lab01.Web --framework net9.0 --no-https
```

### Lựa chọn .NET 10

```bash
dotnet new mvc -n Lab01.Web --framework net10.0 --no-https
```

Chỉ chạy một trong ba lệnh trên.

Biên dịch:

```bash
dotnet build Lab01.Web/Lab01.Web.csproj
```

Chạy ứng dụng:

```bash
dotnet run --project Lab01.Web/Lab01.Web.csproj
```

## Cách 2. Sử dụng Visual Studio

1. Mở Visual Studio.
2. Chọn **Create a new project**.
3. Chọn:

```text
ASP.NET Core Web App (Model-View-Controller)
```

4. Khai báo:

```text
Project name: Lab01.Web
Solution name: Lab01.Web
Location: thư mục repository đã clone
```

5. Chọn **Place solution and project in the same directory**.
6. Chọn một framework được phép:

```text
.NET 8.0
.NET 9.0
.NET 10.0
```

7. Cấu hình:

```text
Authentication type: None
Configure for HTTPS: bỏ chọn
Enable Docker: bỏ chọn
```

8. Nhấn **Create**.

Sau khi tạo, phải có file:

```text
Lab01.Web/Lab01.Web.csproj
```

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

# PHẦN B. CÁ NHÂN HÓA TRANG CHỦ

Mở:

```text
Lab01.Web/Views/Home/Index.cshtml
```

Thay nội dung bằng:

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
        <p><strong>Phiên bản .NET:</strong> .NET 8/9/10</p>
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
.NET 8/9/10
```

bằng thông tin thực tế.

Không được xóa các cụm từ:

```text
Ứng dụng ASP.NET Core đầu tiên
Công nghệ phát triển ứng dụng
Họ và tên
Mã sinh viên
Lớp
Kestrel
```

# PHẦN C. TẠO ENDPOINT KIỂM TRA

Mở:

```text
Lab01.Web/Program.cs
```

Thêm trước `app.Run();`:

```csharp
app.MapGet("/health", () => "LAB01_OK");
```

Phần cuối của `Program.cs`:

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

# PHẦN D. CHẠY VÀ KIỂM TRA

## Visual Studio

Nhấn:

```text
Ctrl + F5
```

## Visual Studio Code hoặc Terminal

```bash
dotnet run --project Lab01.Web/Lab01.Web.csproj
```

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

Dừng ứng dụng:

```text
Ctrl + C
```

# PHẦN E. COMMIT VÀ PUSH

Sinh viên phải có ít nhất bốn commit phát triển, không tính các commit được Classroom tạo tự động.

```bash
git add .
git commit -m "Create ASP.NET Core MVC project"
git push
```

```bash
git add .
git commit -m "Customize student home page"
git push
```

```bash
git add .
git commit -m "Add health check endpoint"
git push
```

```bash
git add .
git commit -m "Complete Lab 01"
git push
```

Không sử dụng commit message thiếu ý nghĩa như:

```text
update
fix
abc
123
nop bai
```

# PHẦN F. KIỂM TRA KẾT QUẢ

Sau khi push:

1. Mở repository trên GitHub.
2. Chọn tab **Actions**.
3. Chọn **Autograding Lab 01**.
4. Mở lần chạy mới nhất.
5. Kiểm tra từng bước.

- Dấu tích xanh: bài kiểm tra thành công.
- Dấu X đỏ: bài chưa đáp ứng một hoặc nhiều yêu cầu.
- Dấu tròn vàng: hệ thống đang kiểm tra.

Nếu bị lỗi, sinh viên phải sửa bài, commit và push lại.

# PHẦN G. TIÊU CHÍ ĐÁNH GIÁ

| Nội dung | Điểm |
|---|---:|
| Đúng tên và cấu trúc dự án | 1,0 |
| Sử dụng `net8.0`, `net9.0` hoặc `net10.0` | 1,0 |
| Dự án biên dịch thành công | 2,0 |
| Trang chủ có đầy đủ nội dung | 2,0 |
| Đã thay thông tin mẫu | 1,0 |
| Endpoint `/health` hoạt động | 2,0 |
| Có ít nhất bốn commit hợp lệ | 1,0 |
| **Tổng cộng** | **10,0** |

## Lưu ý

- Không đổi tên `Lab01.Web`.
- Không sử dụng phiên bản thấp hơn .NET 8.
- Không sử dụng phiên bản cao hơn .NET 10.
- Không sửa hoặc xóa `.github/workflows/autograding.yml`.
- Không đưa các thư mục `bin`, `obj` và `.vs` lên GitHub.
- Phải kiểm tra trạng thái GitHub Actions trước hạn nộp bài.
