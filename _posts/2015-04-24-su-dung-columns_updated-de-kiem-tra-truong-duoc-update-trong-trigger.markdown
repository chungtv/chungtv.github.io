---
layout: post
title: Sử dụng COLUMNS_UPDATED() kiểm tra trường được update trong trigger
date: '2015-04-24 01:47:26'
categories: [MS SQL Server]
tags: [MS SQL Server]
redirect_from: /su-dung-columns_updated-de-kiem-tra-truong-duoc-update-trong-trigger/
---


> Đôi khi, vì lý do gì đó mà triger của bảng trong SQL Server bạn cần phải kiểm tra xem trường nào đang được update trước khi thực thi các lệnh tiếp theo. [Xem thêm bài viết này của tôi tại đây](https://trinhvanchung.wordpress.com/2010/11/03/s%e1%bb%ad-d%e1%bb%a5ng-columns_updated-d%e1%bb%83-ki%e1%bb%83m-tra-tr%c6%b0%e1%bb%9dng-d%c6%b0%e1%bb%a3c-update-trong-trigger/). Bài này được tôi viết lại từ bài đó.

> Một phương pháp được tôi giới thiệu trong bài này là sử dụng `COLUMNS_UPDATED()`.

![](https://www.dropbox.com/s/90ymmfk4t8l036g/04-mssql_columns_updated.jpg?dl=1)

#### Giới thiệu

Về `COLUMNS_UPDATED()` các bạn có thể xem chi tiết ở [site chính chủ](https://msdn.microsoft.com/en-us/library/ms186329.aspx). Ở đây, tôi chỉ giới thiệu qua những điểm cơ bản.

`COLUMNS_UPDATED()` là một Build-in Functions của SQL Server trả về một mẫu giá trị dạng nhị phân (varbinary bit pattern) để xác định vị trí cột nào được insert hoặc update. `COLUMNS_UPDATED()` thường được sử dụng trong INSERT hoặc UPDATE Trigger để kiểm tra vị trí cột được update nhằm xác định có hay không thực thi một số hành động nào đó.

Để kiểm tra vị trí cột nào được thay đổi chúng ta sử dụng các phép toán trên bit (bitwise operators) và bit mặt nạ (bitmask) tương ứng cho vị trí của mỗi cột.

#### Kiểm tra các cột có vị trí <=8
Kiểm tra cột tại vị trí n (n<=8) có phải là cột thay đổi hay không thì sử dụng biểu thức sau:

```sql
COLUMNS_UPDATED() & Power(2,(n-1))
```

Nếu biểu thức trả về > 0 thì cột n là cột bị thay đổi, ngược lại cột n không thay đổi.

Trong trường hợp kiểm tra 2 hoặc nhiều cột có thay đổi hay không thì làm tương tự. Ví dụ kiểm tra cột 3 cột thứ i,j,k có thay đổi hay không (i,j,k<=8) thì sử dụng biểu thức sau:

```sql
COLUMNS_UPDATED() & (Power(2,(i-1)) + Power(2,(j-1)) + Power(2,(k-1)))
```

*Chú ý: Để đỡ phải tính toán khi thực thi thì mình nên tính ra giá trị nguyên của các hàm `Power()` ở ngoài luôn rồi dùng kết quả đó để kiểm tra. Ví dụ thay vì viết như cách trên, mình viết như sau:*

```sql
COLUMNS_UPDATED() & kq 
-- với kq = (Power(2,(i-1)) + Power(2,(j-1)) + Power(2,(k-1)))
```

#### Kiểm tra các cột có vị trí >8

Sử dụng hàm `SUBSTRING()` cho giá trị trả về của `COLUMNS_UPDATED()`.

Ví dụ cần kiểm tra có update cột 10 hay không, sử dụng biểu thức sau:

```sql
SUBSTRING(COLUMNS_UPDATED(),2,1) & Power(2,(10-8-1))
```

Còn nếu cột cần kiểm tra > 16 thì làm tương tự. Ví dụ cần kiểm tra cột 19 có Update không thì sử dụng biểu thức:

```sql
SUBSTRING(COLUMNS_UPDATED(),3,1) & Power(2,(19-16-1))
```