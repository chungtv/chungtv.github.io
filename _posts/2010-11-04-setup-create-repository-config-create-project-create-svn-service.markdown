---
layout: post
title: Setup, create repository, config, create project, create svn service
date: '2010-11-04 05:00:00'
categories: [Work, Tutorials]
tags: [SVN, Source Control]
redirect_from: 
    - /setup-create-repository-config-create-project-create-svn-service/
    - /2010/11/04/setup-create-repository-config-create-project-create-svn-service.html
    - /work/tutorials/2010/11/04/setup-create-repository-config-create-project-create-svn-service.html
---

![Subversion](https://trinhvanchung.files.wordpress.com/2010/11/image.png)

## Đặt vấn đề
Kỳ này có tham gia tại trường học phần Công cụ và môi trường Phát triển phần mềm, trong đó có giới thiệu với các bạn công cụ quản lý mã nguồn Subversion.

Rằng thì là chẳng bao giờ dùng SVN nên nhiều khi demo cứ hay quên mấy cái 1 trừ hay 2 trừ.  Viết cái chủ đề này phần để cho các bạn tham khảo phần để tra cứu lại khi cần thiết.

## Giới thiệu về Subversion
Anh em chịu khó wiki hay nhờ [“anh hai google”](https://www.google.com/?gws_rd=ssl#q=subversion) cho nó rõ nghĩa nhé. Mình chỉ đại khái thôi.

**Subversion** là một phần mềm cung cấp các chức năng quản lý phiên bản mã nguồn và tài liệu. Hiểu đơn giản nó cũng chỉ là một trình quản lý file, thư mục. Tuy nhiên, nó cao cấp hơn ở chỗ nó cho phép quản lý nhiều phiên bản của cùng 1 file, có thể rollback lại khi có sai sót; quản lý lịch sử sửa đổi; quản lý người dùng . Hỗ trợ giải quyết đụng độ, tranh chấp … và nhiều thứ mà nói thật mình cũng chưa tìm hiểu hết.

Tóm lại, anh em cứ google là ra hết hoặc là vào trang chủ của nó mà nghiên cứu [http://subverion.tigris.org](http://subverion.tigris.org)

## Cài đặt SVN
### Download và cài đặt.
Download SVN tại: [http://subverion.tigris.org](http://subverion.tigris.org) (đừng có nói là vào đó xong hổng biết download ở đâu nhé :), còn nếu không biết thật thì vào đây [http://sourceforge.net/projects/win32svn/](http://sourceforge.net/projects/win32svn/)). Sau khi download về máy ta được file svn-win32-3.5.6.zip (phiên bản có thể khác, nhưng cách cài thì như nhau).

Có thể dùng VisualSVN cũng được, nhưng để hiểu rõ hơn bản chất của nó mình sẽ giới thiệu về svn-win32 và quản lý nó bằng Command-line và text file.

Giải nén svn-win32-3.5.6.zip vào đâu đó (trong ví dụ này mình giải nén vào ổ C), được thư mục C:\svn-win32-3.5.6\

![](https://trinhvanchung.files.wordpress.com/2010/11/image1.png)

### Thiết lập biến môi trường
Mục đích của việc thiết lập biến môi trường là để trên cửa sổ command có thể truy xuất trực tiếp tới các thư viện của svn mà không cần phải gõ đường dẫn.

Thêm các biến môi trường như sau:

+ Right-click lên My Computer, chọn Properties.
+ Trong màn hình System Properties chọn tab Advanced.
+ Trong tab Advanced Click vào nút lệnh Environtment Variables.
+ Tại cửa sổ Environtment Variables có 2 phần (user variables và system variables).
+ Trong phần system variables, tìm đến dòng có tên Variable là “Path”, chọn dòng đó và nhấn nút edit.  (ở đây bạn có thể thêm vào user variable hoặc system variable đều được).
+ Sau khi nhấn nút Edit, trong màn hình Edit system variable, tại ô Variable value, bạn đưa con trỏ tới cuối ô; trong trường hợp cuối ô chưa có dấu “;” thì bạn thêm dấu “;” vào, sau đó thêm đường dẫn tới thư mục Bin của svn (thêm C:\svn-win32-1.5.6\bin). Đây là thư mục chứa các tập tin exe của svn.
+ Tiếp theo các bạn thêm biến SVN_EDITOR bằng cách tại vùng User variables hoặc System variables trên của sổ Environment variables, nhấn nút New
+ Trong cửa sổ New variable, thêm như hình sau, sau đó nhấn nút OK.

![](https://trinhvanchung.files.wordpress.com/2010/11/image2.png)

## Tạo kho lưu trữ tài liệu, mã nguồn (Repository)
Kho lưu trữ tài liệu, mã nguồn (Repository) là thư mục chứa dữ liệu về dự án của bạn và các cấu hình truy cập các dữ liệu đó.

Để tạo kho lưu dữ liệu, bạn sử dụng `svnadmin`, trong cửa sổ cmd của window, gõ lệnh sau:

~~~ bash
svnadmin create <đường dẫn kho lưu>
~~~

Ví dụ:
~~~ bash
svnadmin create C:\ARDRepository\
~~~

Sau khi thực hiện xong, SVN sẽ tạo ra trong ổ đĩa của bạn thư mục kho lưu (thư mục chứa dữ liệu các phiên bản tài liệu, mã nguồn, các cấu hình truy cập kho). Bên trong thư mục kho lưu, SVN đã tạo sẳn ra một số thư mục. Là người quản trị, bạn quan tâm đến thư mục Conf.

![](https://trinhvanchung.files.wordpress.com/2010/11/image3.png)

## Cấu hình đơn giản trong Repository

Trong phạm vi bài này, tôi chỉ giới thiệu các bạn tạo user và phân quyền đơn giản cho repository. (Bài sau sẽ giới thiệu chi tiết hơn về `Authentication` trong SVN)

Như phần trên tôi đã nói, các bạn quan tâm đến thư mục `conf`. Trong thư mục `conf`, SVN đã tạo sẵn cho các bạn 3 file: `svnserve.conf`, `passwd`, `authz`.

Điều đầu tiên các bạn làm là chỉnh sửa file `svnserve.conf`

Các bạn có thể đọc hoặc xóa trắng file `svnserve.conf` đi và cấu hình lại từ đầu (vì thực chất nó cũng đơn giản – có mấy dòng thôi).

Trong phạm vi bài này, bạn chỉ quan tâm đến 4 dòng sau:

~~~ config
    [general]
    anon-access = read
    auth-access = write
    password-db = passwd
~~~

- **[general]**: đánh dấu bắt đầu session
- **anon-access**: Cấu hình truy cập khi truy cập vào repository lưu không xác thực (không thông qua đăng nhập username, password). Có các giá trị hiệu lực tăng dần: none, read, write (chắc ko cần nói ý nghĩa của các giá trị này nhỉ :) )
- **auth-access**: Cấu hình khi truy cập vào repository có xác thực (đăng nhập bằng username, password). Các giá trị tương tự như trên
- **password-db**: Tên file chứa thông tin username và password truy cập vào kho lưu. Trong trường hợp trên là file passwd (đã được svn tạo sẵn).

Bạn có thể xóa trắng file `svnserve.conf` và copy 4 dòng trên paste vào là ok.

***Việc tiếp theo bạn làm là tạo ra một vài user truy cập vào repository.***
Để tạo user truy cập vào repository, bạn mở file `passwd`  đã có sẵn trong thư mục `conf` (mở bằng trình soạn thảo văn bản) và xóa trắng đi, gõ lại từ đầu (cho nó chuyên nghiệp ;) )

Tạo một vài user (trong ví dụ sau tôi sẽ tạo user `admin` mật khẩu là `nimda`, `user1` mật khẩu `1resu`, `user2` có mật khẩu `2resu`  

~~~ config
[users]
admin = nimda
user1 = 1resu
user2 = 2resu
~~~

Bắt đầu bằng dòng báo hiệu session cấu hình User `[users]`, mỗi dòng tiếp theo sẽ là `username` và `password` của mỗi user. Cấu trúc `Username = password`

*Phù, như thế là xong phần cấu hình đơn giản.*

Hãy test lại xem cấu hình của bạn có OK hay không, hãy mở cmd lên, gõ lệnh sau vào để chạy `service` của SVN.  

~~~ bash
svnserve –d –r C:\ARDRepository
~~~

<kbd>Enter</kbd>, nếu không có báo gì thì là OK (đừng hụt hẫng nhé, không báo gì lại nghĩ cấu hình sai)

## Tạo dự án để lưu trữ trong Repository

Giữ nguyên cửa sổ cmd đang chạy service SVN ở trên (đừng tắt đi nhé) và mở một cửa sổ CMD khác để thao tác với các lệnh của giao thức SVN.

Mở 1 cửa sở cmd khác, gõ lệnh sau để tạo mới 1 Project lưu trong `ARDRepository`.  

~~~ bash
svn mkdir svn://localhost/<tên dự án> –m “<Mô tả thông tin về dự án>” ––username  <tên user> ––password <password>
~~~

Ví dụ:  

~~~ bash
svn mkdir svn://localhost/AS –m “Asia Standard” ––username admin ––password nimda
~~~

Khi đó, nếu thành công bạn sẽ nhận được:  

~~~ 
Committed revision 1.
~~~

Có thể không cần sử dụng tham số password  

~~~ bash
svn mkdir svn://localhost/AP –m “Asia Professional” ––username admin
~~~

Khi đó, sau khi <kbd>Enter</kbd>, SVN yêu cầu bạn phải nhập password cho `admin`, bạn nhập mật khẩu xong, nếu thành công nó cũng sẽ báo `commited`.  

~~~ bash
C:\Documents and Settings\Chungtv>svn mkdir svn://localhost/AP –m “Asia Professional” ––username admin
Authentication realm: <svn://localhost:3690> 58a7a8ca-296d-2d48-a4a5-f5420ae2ca80
Password for ‘admin‘: *****

Committed revision 2.
~~~ 

Kiểm tra lại danh sách dự án bạn mới tạo bằng lệnh list (hoặc ls) của SVN.

~~~ bash
svn ls svn://localhost
~~~


## Tạo service trong window để chạy svn service
Bước tiếp theo, các bạn tạo 1 service để chạy svn service cho repository bạn đã tạo.

Tại sao phải tạo service? ở bước trên, các bạn để ý là muốn sử dụng được các lệnh của giao thức `SVN (mkdir, list …)` thì không được tắt cửa sổ cmd đang chạy lệnh `svnserve –d –r C:\ARDRepository`

Như vậy là mỗi khi khởi động lại máy chủ, muốn cho các máy trạm có thể truy cập vào repository của bạn thì bạn phải lên server và chạy lệnh đó để start service svn (bất tiện quá đúng không). Bước này, bạn sẽ tạo 1 service khởi động cùng window.

Bạn tắt của sổ cmd đang chạy service SVN đi để tiếp tục.

Để tạo service, bạn sử dụng lệnh `SC` (chú ý là bạn phải có quyền admin trên máy này nhé, nhất là các bạn đang dùng win7, hãy righ-click vào cmd.exe và `Run as Administrator` trước khi tiếp tục).

Trong cửa sổ cmd, bạn gõ lệnh sau để tạo service.  

~~~ bash
sc create <ARDSVN> binpath= “c:\svn-win32-3.5.6\bin\svnserve.exe ––service –r C:\ARDRepository” displayname= “ARD SVN Server” depend= TCPIP start= auto
~~~

> + **ARDSVN**: Tên của service.
> + **binpath= “…”**: Đường dẫn thực thi service và chỉ định các tham số (chú ý là sau dấu = có khoảng trắng còn trước nó thì không nhé)
> + **displayname= “…”**: Tên của service sẽ hiện thị trong Services Management (cũng chú ý khoảng trắng sau dấu ‘=).
> + **depend = TCPIP**: Danh sách các service Dependencies, cần thiết để sử dụng service svn (trong trường hợp này cần phải có service TCPIP)|
> + **start= auto**: Xác định service này sẽ tự động chạy khi khởi động window.

OK, nếu không có gì sai sót thì sau khi <kbd>ENTER</kbd>, bạn sẽ nhận được thông báo:  

~~~
[SC] CreateService SUCCESS
~~~

Tạo xong chưa chắc đã chạy được (vì có thể cấu trúc trong binpath của bạn sau – thiếu dấu “-“ trước service chẳng hạn)

Bây giờ bạn thử chạy service đó lên bằng lệnh sau:  

~~~ bash
sc start ARDSVN
~~~

Nếu thành công bạn sẽ nhận được thông báo thông tin của service.

Trong trường hợp không thành công, bạn có thể xóa service đi bằng lệnh `sc delete ARDSVN` và tạo lại từ đầu.

Chúc các bạn thành công. 
