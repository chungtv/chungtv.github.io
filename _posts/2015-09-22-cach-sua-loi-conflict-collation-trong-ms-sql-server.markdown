---
layout: post
title: 'Cách sửa lỗi conflict collation trong MS SQL Server'
date: '2015-09-22 04:16:35'
categories: [MS SQL Server]
tags: [MS SQL Server]
redirect_from: /cach-sua-loi-conflict-collation-trong-ms-sql-server/post
---

> Trong quá trình cài đặt SQL Server, do không chú chọn Collation phù hợp dẫn đến khi vận hành thường bị conflic collation của SQL Server và Database.

Có nhiều cách để sửa lỗi này.
1. Cách tốt nhất là cài lại SQL Server và chọn Collation phù hợp.
2. Nếu không muốn cài lại SQL Server, đây là một trong những cách mà tôi đã làm thành công.

- Tìm một instance SQL ở máy nào đó, đã cài đúng collation (chú ý là cũng phải đúng phiên bản SQL server).
- Backup database `Model` (đây là một database nằm trong phần Sys Databases).
- Restore database Model đúng đã backup ở bước trên sang instance SQL bị lỗi Conflic Collation.
- Restart lại service SQL Server và kiểm tra lại.

Chúc các bạn thành công.
