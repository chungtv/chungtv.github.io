---
title: Bạn có gì khi đi Khách
layout: post
categories: [Work]
tags: [MS SQL Server,Tools]
---

*Đi khách là một niềm tự hào rất lớn của anh chị em triển khai phần mềm tại ASIA. Theo những con số thống kê chưa được xác minh từ Tổng cục thống kê ASIA thì:*

- Bình quân tại ASIA, đến thời điểm này mỗi nhân viên triển khai đi khoảng 69 khách.
- Mỗi tuần, 1 triển khai đi bình quân 4.69 lượt khách
- Mỗi khách đi hết 169 giờ tính từ lúc dạo đầu đến lúc kết thúc (tức là triển khai rút, chuyển khách sang cho bảo trì)
- ...

Rõ ràng, với hàm lượng chất xám, thời gian, làm việc với cường độ cao trong việc đi khách qua những con số trên. Nếu chúng ta không có được phương pháp làm việc khoa học, các công cụ hỗ trợ tốt phù hợp và hiệu quả thì sẽ rất dễ bị sa lầy và kéo dài thời gian đi khách.

Trong bài viết này, tôi xin chia sẽ với anh chị em một số "hàng" mà tôi thường dùng (có thể một số anh chị em cũng đã dùng rồi).

### SQL Client

Như chúng ta đã biết, hầu hết các sản phẩm của ASIA sử dụng MS SQL Server làm hệ quản trị CSDL (DBMS). Để làm việc với MS SQL Server cách thông thường và dễ dàng nhất là thông qua SQL Server Management, một ứng dụng của Microsoft có sẵn khi cài đặt SQL Server lên máy chủ. 

Việc gì sẽ xảy ra khi bạn không có quyền truy cập vào máy chủ nhưng vẫn phải làm việc với MS SQL Server từ máy trạm. Kiểm tra dữ liệu, cập nhật chương trình, ...

Cài đặt SQL Server trên máy trạm để có SQL Server Management rồi kết nối tới máy chủ? Ý kiến không tồi, tuy nhiên thật là phức tạp, nặng nề và mất thời gian. Một vài công cụ thay thế sau đây, sẽ giúp bạn làm việc đó một cách dễ dàng mà không cần phải cài đặt gì cả. 

#### SQLDbx

Khoảng cách đây 1 năm trở về trước, [SQLDbx](http://www.sqldbx.com/) là lựa chọn duy nhất của tôi trong trường hợp này. **SQLDbx** có bản **Personal**, bản này miễn phí, có thể chép vào và dùng được liền.

- **Ưu điểm**: Chép vào và chạy, không cần cài đặt .Net Framework, hỗ trợ kết nối nhiều loại DBMS.
- **Nhược điểm**: Bản miễn phí không hỗ trợ Unicode, chỉ mở được 1 kết nối và tối đa 2 tab Query, không hỗ trợ vi xử lý 64bit … (và nhiều nhược điểm khác)

**Link download**:  http://www.sqldbx.com/

#### Query Express, Query ExPlus

Cơ bản thì **SQLDbx** chỉ phù hợp khi làm việc với các Database của sản phẩm AP trở về trước. Từ khi AE ra đời, SQLDbx thực sự là một bất lợi nhức nhối khi không hỗ trợ Unicode.

Vào một ngày đẹp trời khi đang lang thang Internet, tôi tình cờ biết đến [Query Express](http://www.albahari.com/queryexpress.aspx) và phiên bản Branch từ [Query Express](http://www.albahari.com/queryexpress.aspx)  là [Query ExPlus](https://sourceforge.net/projects/queryexplus/). Đây quả là hàng siêu nhỏ nhưng có võ. Sở dĩ tôi nói nó siêu nhỏ vì dung lượng của file chạy chỉ khoảng 100KB. Nếu ai đã từng làm việc với SQL server 2000 thì **Query Express** và **Query ExPlus** có giao diện tương tự với **Query Analyzer** của SQL Server 2000. 

Đặc điểm của 2 công cụ này là Mã nguồn mở, hỗ trợ full Unicode, hỗ trợ kết nối thoải mái, tạo thoải mái cửa số query cùng lúc. Nhược điểm là phải có .Net Framework 2.0 trở lên (đây không phải trở ngại vì để chạy được AE thì đã phải có .Net Framework 3.5) 

Và do nó là mã mở nên bạn hoàn toàn có thể download code về và chỉnh sửa thêm nhiều tính năng vào đó nữa cho phù hợp với công việc đi khách của mình.

**Link download:** 
- Query Express: http://www.albahari.com/queryexpress.aspx
- Query ExPlus: http://queryexplus.sourceforge.net/

### Công cụ backup tự động

Sao lưu dữ liệu là một công việc cực kỳ nhức nhối của dân IT, triển khai hay bảo trì. Việc đưa ra chiến lược sao lưu, phương pháp sao lưu cho khách hàng là một câu chuyện dài kỳ (xin không phép bàn tại đây). Trong quá trình triển khai, bắt buộc nhân viên triển khai phải hỗ trợ khách hàng cài đặt Sao lưu dữ liệu tự động trên server của khách hàng.

Đối với MS SQL Server các bản có phí (tức không phải bản Express), Microsoft có sẵn dịch vụ **SQL Agent Services** cho phép bạn cấu hình Backup tự động trong SQL Server Management. Tuy nhiên, rất nhiều khách hàng đang dùng phần mềm của ASIA lại dùng bản Express. Rất tiếc bản SQL này không đi kèm SQL Agent để có thể cấu hình backup tự động.

Có nhiều giải pháp thay thế vàhầu hết đều dựa trên tính năng **Task Scheduler** của **Windows** `(Control Panel\Administrative Tools\Task Scheduler)`  ví dụ: Tạo file Script backup, tạo file Bat để gọi đến file script đó rồ tạo Task Scheduler cho file Bat đó.

Trong bài này, tôi xin giới thiệu với anh em một món "hàng" mà mọi người nên bỏ nó vào trong bóp (ví) của mình khi đi khách, đó là [SQL Backup And FTP](https://sqlbackupandftp.com).

Bản chất của chú này cũng xây dựng trên Windows Task Scheduler, tuy nhiên nó mần một cách tự động mà anh em không cần phải quan tâm nhiều đến viết scrip, cấu hình Task. Khi dùng cái này, nó cũng sẽ tạo 1 Task trong Task Scheduler và chạy như bình thường.

Hàng này có nhiều loại, nhiều giá khác nhau và tất nhiên có cả loại miễn phí. Hạn chế của loại này là giới hạn tối đa 2 database, nén không mã hóa, không lên mây tự động được mà phải chơi thủ công … Mà với nhu cầu cảu anh em, mình thấy quả miễn phí của nó cũng đủ dùng đối với khách hàng đang chạy Express rồi.

Link download tại đây: [https://sqlbackupandftp.com](https://sqlbackupandftp.com)

### Script backup - restore database

Cũng dính tới SQL Server nữa, công việc Backup Database ở khách hàng sau đó mang về ServerDB của mình Restore lại thật là công việc nhàm chán, quá nhiều thao tác từ chọn thư mục, thay đổi đường dẫn file …

Đặc biệt trong quá trình restore, có đồng chí nào đang mở connection đến database đó mà mình quên check vào `"Close existing connection to destination database"` là coi như laị phải làm lại từ đầu.

Đề giải quyết cái việc nhàm chán này, tôi thường sử dụng script T-SQL để làm việc này

#### Backup

```sql
-- =================================================================
-- 17/11/2015 # Chung Trinh @ Backup Database

BACKUP DATABASE TenDatabase
TO DISK = 'D:\Database_ServerDB\Database_TrienKhai\Database\Backup\TenDataBase_20151117.bak'
```

#### Restore

```sql
-- =================================================================
-- 17/11/2015 # Chung Trinh @ Restore Database
DECLARE @SQL AS VARCHAR(20), @spid AS INT     
SELECT @spid = MIN(spid) FROM master..sysprocesses WHERE dbid = db_id('TenDatabase') AND spid != @@spid    

-- Kill processes that currently use the database and could block the restoration     
while (@spid IS NOT NULL)
BEGIN
    print 'Killing process ' + CAST(@spid AS VARCHAR) + ' ...'
    SET @SQL = 'kill ' + CAST(@spid AS VARCHAR)
    EXEC (@SQL)

    SELECT @spid = MIN(spid) FROM master..sysprocesses WHERE dbid = db_id('TenDatabase') AND spid != @@spid
END 
GO

-- Restore database
RESTORE DATABASE TenDatabase
FROM DISK = 'D:\Database_ServerDB\Database_TrienKhai\Database\Backup\TenDataBase_20151117.bak' WITH REPLACE, RECOVERY;
GO   
```

Đó là một vài món hàng mà tôi thường bỏ bóp khi đi khách, còn bạn, bạn bỏ gì vào bóp của mình để phòng thân khi đi khách? có chuyện gì vui khi đi khách không? hãy share cùng mọi người nhé.
