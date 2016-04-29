---
layout: post
title: SQL Server - Ctrl + R không làm việc trong SSMS
date: 2015-05-21 04:10:52
categories: [Work, Tips and tricks]
tags: [MS SQL Server]
redirect_from: 
 - /sql-server-ctrl-r-khong-lam-viec-trong-ssms/
 - /ms%20sql%20server/2015/05/21/sql-server-ctrl-r-khong-lam-viec-trong-ssms.html
---

Hôm nay, không biết vì lý do gì mà tổ hợp phím <kbd>Ctrl+R</kbd> không làm việc trên SQL Server Management Studio nữa. `Hiện tại tôi đang dùng SQL Management Studio 2012 (SSMS)`.

> Trong SSMS, <kbd>Ctrl+R</kbd> là tổ hợp phím tắt sử dụng để ẩn vùng kết quả truy vấn của SQL.

Khi nhấn <kbd>Ctrl+R</kbd> thì nhận được kết quả như sau dưới thanh Status bar:
![](/images/2015/05/2015-05-21_105035.png)
Nhấn thêm <kbd>Ctrl+R</kbd> lần nữa thì thanh Status Bar như sau:
![](/images/2015/05/2015-05-21_105259.png)

Vào menu Window thì thấy đã chuyển thành tổ hợp phím <kbd>Ctrl+Shift+Alt+R</kbd>
![](/images/2015/05/2015-05-21_105524.png)

Sau đây là các bước để lấy lại phím tắt <kbd>Ctrl+R</kbd> cho SSMS:
1. Vào menu Tools, chọn Options...;
2. Trong cửa sổ Options chọn Environment -> Keyboard -> Keyboard;
3. Tại Combobox "Apply the following additional keyboard mapping scheme" chọn default. Sau đó nhất nút Reset để trả về mặc định ban đầu.

Hoặc bạn có thể chọn Window.ShowResultsPane ở danh sách phía dưới và thiết lập phím tắt tại ô "Press shortcut keys:".

 
