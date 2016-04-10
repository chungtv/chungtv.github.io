---
layout: post
title: Mở nhiều tài khoản Skype trên cùng một máy tính
date: '2015-05-21 07:32:19'
categories: [Work, Tips and tricks]
tags: [Skype]
redirect_from: /mo-2-tai-khoan-skype-tren-cung-mot-may-tinh/
---

Trong công việc, vì lý do gì đó mà bạn cần phải mở nhiều tài khoản Skype trên cùng một máy tính để trao đổi.
Mặc định, Skype chỉ cho phép mở một chương trình (đăng nhập bằng một tài khoản) trên một máy tính. Để có thể mở nhiều hơn một chương trình Skype khác và đăng nhập vào tài khoản khác, bạn làm như sau:
# Đối với máy tính windows

![](/images/2015/05/2015-05-21_142908.png)

### Chạy chương trình Skype khác
1. Vào Start > Run hoặc nhấn tổ hợp phím <kbd>Windows+R</kbd>
2. Trong cửa sổ Run, bạn gõ vào: `c:\Program Files (x86)\Skype\Phone\Skype.exe /secondary` **(chú ý tham số /secondary)**

![](/images/2015/05/2015-05-21_141718.png)

3. Nhấn <kbd>OK</kbd>. 

Một cửa sổ Skype mới sẽ hiện ra và bạn có thể đăng nhập bằng tài khoản mới rối.

### Tạo shortcut trên màn hình desktop
Mỗi lần muốn chạy chương trình Skype khác, bạn lại phải làm lại thao tác rườm rà như trên. Hãy tạo shortcut trên màn hình desktop của bạn để lần sau truy cập nhanh hơn, làm như sau:
1. Click chuột phải lên trỗ trống trên màn hình desktop và chọn New > Shortcut.
2. Trên màn hình `[Create Shortcut]`, tải ô `[Type the location of the item]`, bạn copy nguyên đoạn sau và paste vào: `"C:\Program Files (x86)\Skype\Phone\Skype.exe" /secondary`. Sau đó nhấn nút <kbd>Next</kbd>
3. Đặt tên cho shortcut mới, ví dụ `Skype 2`. Sau đó nhấn <kbd>Finish</kbd> là bạn đã hoàn thành.

# Đối với máy chạy MACOS
Mở terminal và gõ vào dòng lệnh sau:
```
sudo /Applications/Skype.app/Contents/MacOS/Skype
```
Sau đó nhập Password. Một chương trình Skype thứ 2 đã được chạy lên.

Chúc bạn thành công.