---
layout: post
title: Authentication in SVN
date: '2010-11-12 05:00:00'
redirect_from: /authentication-in-svn/
---

Trong các bài trước, tôi đã hướng dẫn các bạn cài đặt, cấu hình đơn giản, tạo repository, sử dụng một số lệnh cơ bản của giao thức SVN để thao tác với Repository.

Vấn đề đặt ra là trong trường hợp dự án có nhiều thành viên tham gia, có nhiều team cùng tham gia dự án và role của mỗi team hoặc mỗi thành viên là khác nhau trên từng dự án, thậm chí trên từng thư mục con của dự án. 

Vậy làm sao để phân quyền truy cập cho các thành viên, các team đó trong SVN.

Với VisualSVN, mọi việc rất dễ dàng, tuy nhiên trong bài này tôi không có ý định hướng dẫn các bạn tạo user và cấu hình xác thực trong VisualSVN. Trong phạm vi bài này, tôi sẽ giới thiệu với các bạn cách cấu hình Authentication cho các user, các team truy cập vào Repository và các dự án bằng text file.

Để thực hiện việc phân quyền trong SVN, các bạn sử dụng file `authz` trong thư mục `conf` của repository. Để chỉ định việc kiểm tra quyền được cấu hình trong file `authz`, bạn phải mở chỉ thị trong `authz-db` trong file `svnserve.conf` ra. Khi đó, bạn có được file `svnserve.conf` như sau:

```
[general]
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

Để bất đầu hãy mở file `authz` bằng notepad và xóa trắng nó đi.

### Phân nhóm user

Trong svn, việc phân nhóm user trong file `authz` được thực hiện trong 1 session, dòng đầu tiên của session này là `[groups]`. Các dòng tiếp theo của session này là định nghĩa các nhóm tham gia vào dự án (sẽ được phân quyền để truy cập vào repository). Cấu trúc của 1 dòng như sau:

```
    group_name = user_name1, user_name2
```
> *Các user name ngăn cách nhau bởi dấu phẩy (,) và hãy chắc chắn rằng các user này đã được tạo trong file passwd.*

Ví dụ, bạn tạo ra 2 nhóm tham gia dự án, khi đó session groups sẽ như sau:

```
    [groups]
    dev_team = dev1, dev2, dev3
    test_team = test1, test2
```

### Phân quyền cho user hoặc nhóm user

Trước khi phân quyền, bạn cần biết: Trong SVN, quyền truy cập vào 1 thư mục nào đó có 2 mức: `read (r)` và `write(w)`. Việc phân quyền cho user được access vào thư mục ở quyền nào được gán bởi các ký tự đại diện `r` hoặc `w`.

Để gán quyền cho các user hoặc group access vào một thư mục nào đó trong repository, bạn hãy tạo ra 1 session với tên session là đường dẫn tới thư mục cần phân quyền `[đường dẫn]` (trong trường hợp phân quyền truy cập cho repository (thư mục gốc) thì tên session sẽ để trống `[/]`). Trong 1 file `authz` có thể có nhiều session phân quyền khác nhau.

Ngay phía dưới tên, các dòng tiếp theo trong session sẽ thể hiện quyền của user hay nhóm.

Ví dụ, tôi phân quyền cho user `admin` toàn quyền trên toàn repository này thì sử dụng thì sử dụng session `[/]` như sau:

```
[/]
admin = rw
```
Phân quyền cho `user1` có toàn quyền trên dự án `AP` thì như sau:

```
[/ap]
user1=rw
```

Phân quyền cho nhóm `dev` đã tạo ở trên toàn quyền trên thư mục `src` của dự án `AP` và nhóm `test` chỉ có quyền `read` trên thư mục src này. (chú ý đặt đấu @ trước tên nhóm)

```
[/ap/src]
@dev=rw
@test=r
```

Phân quyền cho tất cả mọi người đều được truy cập vào thư mục `docs` của dự án `AP`.

```
[/ap/docs]
*=rw
```

Kết quả, file `authz` sẽ như sau:

```
[groups]
dev=dev1,dev2,dev3
test=test1,test2

[/]
admin=rw

[/ap]
user1=rw

[/ap/src]
@dev=rw
@test=r

[/ap/docs]
*=rw
```

Bạn hãy thử sử dụng lệnh `ls` để kiểm tra hiệu lực của quyền `read`, lệnh `mkdir` để kiểm tra hiệu lực của lệnh `write` xem sao nhé. Cách sử dụng cách lệnh thì đã được giới thiệu trong các bài trước rồi. 