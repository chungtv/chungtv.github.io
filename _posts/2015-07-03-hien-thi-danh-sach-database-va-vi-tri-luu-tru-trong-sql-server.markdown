---
layout: post
title: Hiển thị danh sách database và vị trí lưu trữ trong SQL Server
date: '2015-07-03 02:51:15'
redirect_from: /hien-thi-danh-sach-database-va-vi-tri-luu-tru-trong-sql-server/
---

Trong quá trình làm việc với SQL Server, đôi khi bạn cần hiển thị danh sách database cùng với vị trí lưu trữ các file Data, Log của các Database đó. 
Đây là Query sẽ trả về kết quả mong muốn.

```
SELECT
    db.name AS [DB Name],
    mf.name AS [Logical Name],
    type_desc AS [File Type],
    Physical_Name AS [Location]
FROM
    sys.master_files mf
INNER JOIN 
    sys.databases db ON db.database_id = mf.database_id
```