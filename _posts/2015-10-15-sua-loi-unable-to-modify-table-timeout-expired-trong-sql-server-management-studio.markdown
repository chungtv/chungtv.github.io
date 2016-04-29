---
layout: post
title: Sửa lỗi Unable to modify table. Timeout expired trong SQL Server Management Studio
date: 2015-10-15 22:00:32
categories: [Work, Tips and tricks]
tags: [MS SQL Server]
published: True
share: True
redirect_from:
  - /ms%20sql%20server/2015/10/16/s%E1%BB%ADa-l%E1%BB%97i-unable-to-modify-table-timeout-expired-trong-sql-server-management-studio.html
  - /work/tips%20and%20tricks/2015/10/16/sửa-lỗi-unable-to-modify-table-timeout-expired-trong-sql-server-management-studio.html
---

Trong SQL Server Management Studio, khi làm việc với bảng dữ liệu lớn hoặc vì lý do gì đó, bạn phải sửa lại cấu trúc bảng, sửa kiểu dữ liệu ... Sau khi tiến hành thay đổi cấu trúc bảng xong, lưu bản lại, nhiều khả năng bạn sẽ nhận được thông báo:


~~~

- Unable to modify table. 
Timeout expired. The timeout period elapsed prior to completion of the operation or the server is not responding.

~~~


**Đây là cách sửa lỗi này**

- Trong SQL Server Management Studio, vào menu `Tools \ Options`
- Trong cửa sổ `Options`, tại danh sách bên tay trái, bạn vào phần `Designers`.
- Tại phần đầu tiên của `Table Options` bên tay phải. Bạn check vào tùy chọn **Overrides connections string time-out value for table designer update**. Tại ô **Transaction time-out after:**, thường thì mặc định là 30. Bạn sửa lại giá trị lớn hơn (tối đa là 65535).
- Sau đó nhấn `OK` và thử lại.


**Chúc các bạn thành công**
