---
layout: post
title: Bảng tạm trong MS SQL Server – Temporary tables in MS SQL Server
date: '2012-05-23 05:00:00'
categories: [Work, Tutorials]
tags: [MS SQL Server]
redirect_from: 
    - /bang-tam-trong-ms-sql-server-temporary-tables-in-ms-sql-server/
    - /work/tutorials/2012/05/23/bang-tam-trong-ms-sql-server-temporary-tables-in-ms-sql-server.html
---

Khi làm việc với MS SQL Server, hẳn bạn cũng khá quen thuộc với khái niệm bảng tạm (Temporary table). Ít nhiều bạn đã từng làm hoặc từng gặp các đoạn:

~~~ sql
SELECT Col1, Col2 INTO #tTmpTable FROM TableName WHERE ...
~~~

hay

```sql
CREATE TABLE #tTmpTable (col1 varchar(8), ...)
```

Trong bài viết này mình xin trình bày với các bạn cái nhìn tổng quan về Temporary table.

### Các loại bảng tạm
MS SQL Server cung cấp cho chúng ta 2 loại bảng tạm là **Local Temporary table** và **Global Temporary table**. Mỗi loại bảng tạm có phạm vi ảnh hưởng và truy cập khác nhau.

**Local temporary table** là bảng tạm được tạo ra và tồn tại trong 1 kết nối. Khi kết thúc kết nối thì bảng tạm này sẽ tự động được xóa. Tên của bảng tạm kiểu Local được bắt đầu bằng ký tự #.

**Global temporary table** là bảng tạm có phạm vi ảnh hưởng trong tất cả các kết nối và nó chỉ tự động được xóa đi khi tất cà kết nối đã được ngắt. Tên bảng tạm kiểu Global được bắt đầu  bằng ##.

Để minh chứng cho 2 loại bảng tạm này, các bạn hãy làm thử ví dụ sau:

* Mở Microsoft SQL Server Management Studio (SSMS) và chọn <kbd>New Query</kbd>
* Gõ đoạn lệnh sau:

```sql
CREATE TABLE #LocalTmpTable
(
    ID int,
    Name nvarchar(32)
)
```

Đoạn lệnh này sẽ tạo ra trong Database **tempdb** một bảng có tên là #LocalTmpTable____000002

![](http://trinhvanchung.files.wordpress.com/2012/04/image.png)

SQL Server sẽ tự động tăng số thứ tự vào phía sau tên bảng nhằm quản lý việc nhiều kết nối tạo bảng tạm có cùng tên.

* Gõ đoạn sau và <kbd>F5</kbd> để kiểm tra, bạn sẽ nhận được kết quả là ID của bảng tạm đã tạo.
    
```sql
PRINT OBJECT_ID('Tempdb.dbo.#LocalTmpTable')
```


* Mở 1 cửa sổ Query khác bằng <kbd>New Query</kbd>, gõ lại đoạn lệnh trên và <kbd>F5</kbd> bạn sẽ không nhận được kết quả.

Để Test về phạm vi của **Global Temp table**, bạn hãy thực hiện lại các thao tác trên với tên bảng là ##GlobalTmpTable.

### Tạo và thao tác trên bảng tạm
Để tạo bảng tạm, bạn có thể sử dụng lệnh `CREATE TABLE`

```sql
CREATE TABLE #LocalTmpTable ( ID int, Name nvarchar(32))
```

hoặc sử dụng lệnh SELECT INTO

```sql
SELECT Ma, Ten INTO ##GlobalTmpTable FROM TableName WHERE ...
```

Với `Temporary Table`, bạn  hoàn toàn có thể truy vấn, thao tác dữ liệu như đối với các table bình thường.

### Sử dụng bảng tạm
Bảng tạm và biến bảng thường được sử dụng khi cần xử lý một tập dữ liệu con trong tạp dữ liệu lớn được lưu trữ trong Table của Database hoặc từ nhiều Tables. (Đặc biệt là khi viết các Store procedures xử lý báo cáo).

Bảng tạm được tạo ra trong Database Tempdb khác với Database của bạn vì thế có thể gây ra các vấn đề về hiệu suất. Do đó, bạn cần tính toán kỹ số lượng các Fields cần thiết phải lấy ra.

### Tham khảo
- [Quick Overview: Temporary Tables in SQL Server 2005](http://www.codeproject.com/Articles/42553/Quick-Overview-Temporary-Tables-in-SQL-Server-2005)