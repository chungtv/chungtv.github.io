---
layout: post
title: Start menu, Cotana và Modern Apps không hoạt động trong windows 10
date: '2015-08-04 09:16:52'
redirect_from: /start-menu-cotana-va-modern-apps-khong-hoat-dong-trong-windows-10/
---

![](/images/2015/08/windows_10.jpg)

Có rất nhiều lý do khiến Start menu hay các ứng dụng Modern không hoạt động trong Windows 10. Sau đây, tôi sẽ hướng dẫn sửa lỗi Start menu, Cortana, Search Box và các ứng dụng Modern không hoạt động trong windows 10.

1.- Mở Windows Powershell dưới quyền Administator

**a. Cách 1:**

- Nhấn tổ hợp phím <kbd>Windows + R</kbd>
- Gõ `Powershell` và nhấn <kbd>Enter</kbd>
- Sau khi Powershell đã chạy, Click phải lên icon PowerShell dưới thanh Taskbar và chọn `Run as Administrator `

**b. Cách 2:**

- Click phải lên nút `Start`
- Chọn `Command prompt (Admin)`
- Trong màn hình `Administrator: Command Prompt`, gõ `powershell` và nhấn <kbd>Enter</kbd>

2.- Copy và Paste đoạn sau vào màn hình `Administrator: Windows PowerShell window` và nhấn <kbd>Enter</kbd>:
```
Get-AppXPackage -AllUsers | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```

3.- Bỏ qua một số thông báo lỗi màu đỏ và đợi Power Shell thực hiện xong đoạn lệnh trên.

4.- Kiểm tra sẽ thấy Start menu đã hoạt động trở lại.

Chúc bạn thành công
