---
layout: post
title: Một số lệnh cơ bản trong SVN
date: '2010-11-05 05:00:00'
categories: [Work, Tutorials]
tags: [SVN, Source Control]
redirect_from: /mot-so-lenh-co-ban-trong-svn/
---

![Subversion](https://trinhvanchung.files.wordpress.com/2010/11/image_thumb.png?w=396&h=58)

Trong bài trước, các bạn đã cài đặt được SVN và làm quen với SVN. Trong bài này, xin giới thiệu với các bạn một số lệnh cơ bản để thao tác với SVN.

Bạn có thể dễ dàng thấy các lệnh được hỗ trợ trong SVN bằng cách trong của sổ Cmd, gõ dòng lệnh sau:

~~~ bash
svn help hoặc svn ?
~~~

Một số lệnh cơ bản, ý nghĩa và cách sử dụng chúng:

*Chú ý: trong cấu trúc các lệnh dưới đây tôi luôn kèm theo các tham số `Username` và `password`, tuy nhiên trên thực tế thì có những lệnh không cần, tùy vào cấu hình truy cập (bài sau sẽ nói về vấn đề này). ví dụ, trong file `svnserve.conf` ở bài trước, chúng ta cấu hình `nanon-access = read` thì thực chất trong lệnh `list` ở dưới không cần kèm theo tham số `username` và `password`. Tham số `username` và `password` thậm chí cũng chỉ cần gõ 1 lần ở lệnh đầu tiên, trong các lệnh tiếp theo svn sẽ tự nhận lại tham số ở lệnh trước đó.*

### mkdir | Lệnh tạo thư mục
###### Ý nghĩa
Lệnh này sử dụng để tạo thư mục trong `repository` của bạn. (giống lệnh MD trong Doc command)

###### Cấu trúc lệnh

~~~ bash
svn mkdir <đường dẫn thư mục mới tạo> –m <Mô tả về dự án> ––username <username> ––password <password>
~~~

Trong trường hợp bạn ko gõ tham số –m, chương trình sẽ hiển thị màn hình để các bạn nhập comment vào (chương trình này được thiết lập trong biến SVN_EDITOR ở bài trước)

###### Ví dụ
* Tạo dự án mới:

~~~ bash
svn mkdir svn://localhost/as –m “Asia standard, a product of asiasoft” ––username admin ––password nimda
~~~

* Tạo thư mục con của dự án mới tạo:

Tạo thư mục chứa Source của dự án

~~~ bash 
svn mkdir svn://localhost/as/Src –m “Source code store here” ––username admin ––password nimda
~~~

Tạo thư mục chứa tài liệu  

~~~ bash
svn mkdir svn://localhost/as/Docs –m “Documents of project store here” ––username admin ––password nimda
~~~

Tạo các thư mục con của thư mục chứa tài liệu

~~~ bash
svn mkdir svn://localhost/as/Docs/TechDocs –m “Documents for Technical” ––username admin ––password nimda

svn mkdir svn://localhost/as/Docs/UserDocs –m “Documents for End-User” ––username admin ––password nimda
~~~

### delete (del, remove, rm) | Xóa thư mục 
###### Ý nghĩa
Xóa thư mục (cái này thì giống RD trong dos command)

###### Cấu trúc lệnh

~~~ bash
svn delete <đường dẫn tới thư mục cần xóa> ––username <username> ––password <password>
~~~

Có thể thay thế lệnh `delete` bằng `del`, `remove` hoặc `rm`

###### Ví dụ

Xóa thư mục Docs

~~~ bash
svn delete svn://localhost/as/docs ––username admin ––password nimda
~~~

### list (ls) | Lệnh liệt kê thư mục, file
######Ý nghĩa

Dùng để liệt kê danh sách các thư mục và file bên trong thư mục đang được list (giống DIR trong Dos command)

###### Cấu trúc lệnh

~~~ bash
svn list <đường dẫn đến thư mục cần xem danh sách thư mục và file> ––username <username> ––password <password>
~~~
###### Ví dụ

Trong ví dụ này, tôi đã thử dùng SVN để liệt kê các thư mục và file bên trong dự án của nhóm `Quản lý xây dựng` trên google code (tại thời điểm 14h41 ngày 05/11/2010) và nhận được kết quả như sau:

~~~ bash
C:\svn-win32-1.5.6\bin>svn ls https://quanlyxaydung.googlecode.com/svn/trunk/code/

NhanVien/
congtrinh/
khachhang/
main/
quanlykho/
quanlyvattu/
~~~

Trong ví dụ trên, các bạn có thể thay lệnh list bằng lệnh ls

### checkout (co)
###### Ý nghĩa
Lệnh này sử dụng để lấy phiên bản mã nguồn mới nhất từ thư mục dự án trên repository về thư mục trên máy trạm.

###### Cấu trúc lệnh
~~~ bash
svn checkout <đường dẫn thư mục trên máy chủ> <đường dẫn thư mục trên máy trạm> ––username <username> ––password  <password>
~~~

Các bạn có thể thay thế lệnh checkout ở trên bằng lệnh co.

###### Ví dụ

Trong ví dụ này, tôi sẽ lấy mã nguồn mới nhất từ thư mục Src của dự án AS đã tạo ở trên về thư mục `D:/dev/as/src/` trên máy trạm.

~~~ bash
svn checkout svn://localhost/as/src d:/dev/as/src ––username admin ––password nimda
~~~

Nếu thành công, chương trình sẽ có thông báo:

~~~ bash
Checked out revision n. //(n là số phiên bản hiện tại mới nhất)
~~~

Trong trường hợp thư mục `d:/dev/as/src` chưa có, SVN sẽ tự tạo.

*Phù, tạm tới đây đã. Tôi sẽ cố gắng viết tiếp để các bạn tham khảo.*