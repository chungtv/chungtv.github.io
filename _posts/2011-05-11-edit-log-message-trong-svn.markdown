---
layout: post
title: Edit log message in SVN
date: '2011-05-11 05:00:00'
redirect_from: /edit-log-message-trong-svn/
---

Hôm nay, vào show log của dự án (Click phải lên dự án –> TortoiseSVN –> Show Log). Xem lại log thì thấy một số cái message không hợp lý. Tính sửa lại, click phải lên revision dự định sửa, chọn Edit log message. Sau khi sửa xong, nhấn OK, thì nhận được lỗi từ TortoiseSVN là: `Repository has not been enabled to accept revision propchange; ask the administrator to create pre-revprop-change hook`.

![](http://trinhvanchung.files.wordpress.com/2011/05/image.png)

Để giải quyết lỗi trên bạn làm như sau:

- Truy cập lên server, mở thư mục hooks trong Repository ra.
- Trong thư mục này, tạo file `pre-revprop-change.bat`
- Mở file trên bằng notepad và gõ nội dung sau vào file:

```bash
REM Only allow log messages to be changed
if "%4" == "svn:log" exit 0
echo Property "%4" cannot be changed >&2
exit1
```

**Tham khảo:**

1. [Matt Refghi’s Blog](http://mattrefghi.com/wordpress/subversion-repository-has-not-been-enabled-to-accept-revision-propchanges/)
2. [TortoiseSVN Document](http://tortoisesvn.net/docs/release/TortoiseSVN_en/tsvn-repository-hooks.html)