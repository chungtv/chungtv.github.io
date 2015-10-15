---
layout: post
title: Truy vấn dữ liệu từ xa thông qua MS SQL linked server
date: '2011-05-25 05:00:00'
categories: [MS SQL Server]
tags: [MS SQL Server]
redirect_from: /truy-van-du-lieu-tu-xa-thong-qua-ms-sql-linked-server/
---

> *Đôi khi vì một lý do gì đó mà bạn phải truy vấn dữ liệu từ một database đặt tại server khác (hoặc một instance khác của SQL Server) – ví dụ: so sánh dữ liệu giữa 2 database, hay các giải pháp phân tán …*

> *Bạn sẽ làm thế nào? Tôi xin giới thiệu với các bạn sử dụng Linked Server để giải quyết vấn đề này.*

Trong bài này, tôi giả sử tôi đang ở SQL server 2000 máy local (instance là `CHUNGTV\SQL2K`), tôi cần lấy dữ liệu của bảng DMKH ở database `HungLong` để tại SQL Server 2008 trên máy chủ (instance là `ServerDB\SQL2008`)

### Cách 1: Cấu hình bằng giao diện

- Mở trình quản lý database lên, hiện tôi đang dùng Microsoft SQL Server Management Studio 2008 (10.x); đối với Microsoft SQL Server Management Studio 2005 (9.x) thì làm tương tự, với Microsoft SQL Enterprise Manager 8 (2000) thì có khác một ít tôi sẽ nói sau.

- Expand thư mục `Server Objects`, sẽ thấy thư mục `Linked Servers`

![](http://trinhvanchung.files.wordpress.com/2011/05/image1.png)

*Đối với Microsoft SQL Enterprise Manager 8 (2000) thì phần Linked Servers lại nằm trong phần Security*

![](http://trinhvanchung.files.wordpress.com/2011/05/image2.png)

- Righ-click lên mục `Linked Servers`, và chọn `New Linked Servers…`, màn hình `New Linked Server` sẽ hiện lên

![](http://trinhvanchung.files.wordpress.com/2011/05/image3.png)

**Tại phần General, bạn nhập các thông tin:**
> - **Linked server**: Tên bạn đặt cho linked server sẽ được truy xuất khi bạn thực hiện truy vấn dữ liệu (ở đây tôi đặt là SERVERDB2K8)

> - **Server type**: Bạn chọn là Other data source

> - **Provider**: Chọn Microsoft OLE DB Provider for SQL Server (ở đây bạn có thể chọn loại khác tùy vào nguồn dữ liệu bạn sẽ link tới – có thể là Access, Oracle, Excel …)

> - **Product name**: đặt tên product (ở đây tôi đặt là Sql2K8)

> - **Data source**: nhập instance của server bạn muốn link tới (ở đây tôi gõ ServerDB\SQL2008)

> - Các thông tin khác để mặc định.

**Tại phần Security:**

![](http://trinhvanchung.files.wordpress.com/2011/05/image4.png)

> - Bạn chọn tùy chọn “Be made using this security context”

> - Nhập user đăng nhập vào SQL tại `Remote login:`

> - Nhập Password đăng nhập tại `With password:`

Sau đó bạn nhấn <kbd>OK</kbd>

- Thực hiện truy vấn dữ liệu: bạn chọn <kbd>New Query</kbd> và gõ câu truy vấn dữ liệu thử. Ví dụ:
```sql
SELECT TOP 100 * FROM SERVERDB2K8.HungLong.dbo.DMKH
```

### Thực hiện bằng lệnh
Tại cửa sổ query, bạn hoàn toàn có thể thực hiện các công việc như bước 1 bằng cách sau:
- Tạo mới Linked server bằng lệnh sau:

```sql
EXEC master.dbo.sp_addlinkedserver @server = N'SERVERDB2K8', @provider=N'SQLOLEDB', @datasrc=N'ServerDB\SQL2008', @srvproduct=N'Sql2K8'
```

- Kiểm tra đã tạo thành công chưa bằng:
```sql
EXEC sp_linkedservers
```
kết quả:
![](https://trinhvanchung.files.wordpress.com/2011/05/image_thumb5.png?w=575&h=87)

- Đăng nhập vào Linked server
```sql
EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'SERVERDB2K8', @useself=N'False', @locallogin=NULL, @rmtuser=N'tentruycap', @rmtpassword='matkhautruycap'
```

- Kiểm tra kết quả
```sql
SELECT TOP 100 * FROM SERVERDB2K8.HungLong.dbo.DMKH
```

Chúc các bạn thành công.