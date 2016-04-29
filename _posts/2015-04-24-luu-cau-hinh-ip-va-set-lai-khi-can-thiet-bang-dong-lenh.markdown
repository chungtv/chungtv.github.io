---
layout: post
title: Lưu cấu hình IP Profile và thiết lập lại khi cần thiết
date: '2015-04-24 02:23:16'
categories: [Work, Tips and tricks]
tags: [Windows, Network]
redirect_from: 
  - /luu-cau-hinh-ip-va-set-lai-khi-can-thiet-bang-dong-lenh/
  - /2015/04/24/luu-cau-hinh-ip-va-set-lai-khi-can-thiet-bang-dong-lenh.html
  - /work/tips%20and%20tricks/2015/04/24/luu-cau-hinh-ip-va-set-lai-khi-can-thiet-bang-dong-lenh.html
---

> Đôi khi, chúng ta cần phải thực hiện những công việc mang tính lặp đi lặp lại như việc thay đổi địa chỉ IP trên máy tính cá nhân khi kết nối mạng ở vài nơi. Việc thay đổi này lặp đi lặp lại hàng ngày. 

> Sau khi tìm hiểu, tôi tìm được cách khá đơn giản để làm việc đó.

##### Lưu cấu hình IP ra file text
Gõ lệnh sau:  

~~~ bash
netsh –c interface dump > D:\\profileIp1.txt
~~~

##### Thiết lập lại cấu hình IP từ file text
Gõ lệnh sau:  

~~~ bash
netsh –f D:\\profileIp1.txt 
~~~

> Để thuận tiện hơn (mổi lần thực hiện lại phải mở cửa sổ dòng lệnh ra gõ), bạn có thể tạo file bash (.bat) để thực hiện việc này.
