---
layout: post
title: '[Tips] Lấy thuộc tính của tất cả Database trong MS SQL Server'
date: '2015-07-07 03:10:37'
categories: [Work, Tips and tricks]
tags: [MS SQL Server]
redirect_from: /tips-lay-thuoc-tinh-cua-tat-ca-database-trong-ms-sql-server-2/
---

Trong quá trình quản lý Cơ sở dữ liệu MS SQL Server, tôi cần kiểm tra thuộc tính bất kỳ của tất cả Database đang có trong MS SQL Server. Đây là câu truy vấn làm việc này:

~~~ sql
SELECT name, 
       DATABASEPROPERTYEX(name, 'IsAutoClose')
FROM   master.dbo.sysdatabases
~~~

Tham khảo thêm tại đây [mssqltips.com](https://www.mssqltips.com/sqlservertip/1033/retrieving-sql-server-database-properties-with-databasepropertyex/)