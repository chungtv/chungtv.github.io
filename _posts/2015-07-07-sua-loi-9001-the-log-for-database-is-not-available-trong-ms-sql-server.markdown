---
layout: post
title: 'Sửa lỗi 9001: The log for database is not available trong MS SQL Server'
date: '2015-07-07 03:15:43'
redirect_from: /sua-loi-9001-the-log-for-database-is-not-available-trong-ms-sql-server/
---

Một số Database của tôi bị lỗi 9001 khi thực hiện thao tác dữ liệu (Insert, update). Tôi kiểm tra thì thấy thuộc tính `Auto Close` đang là True. Tôi cố chuyển nó sang False nhưng không được. Sau khi nghiên cứu, thì đây là cách tôi giải quyết.

1. Click phải vào Database, chọn `Tasks -> Take Offline`
2. Sau đó Click phải lại vào Database, chọn `Tasks -> Bring Online`
3. Click phải, chọn `Properties`. Trong màn hình `Database Properties`, chọn `Options`. Sau đó thiết lập thuộc tính `Auto Close` về **False** là xong.