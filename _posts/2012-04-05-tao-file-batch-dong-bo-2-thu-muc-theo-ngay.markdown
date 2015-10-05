---
layout: post
title: Tạo file Batch đồng bộ 2 thư mục theo ngày
date: '2012-04-05 05:00:00'
---

Trong quá trình triển khai phần mềm, việc sửa đổi chương trình theo yêu cầu người dùng là không tránh khỏi. Thường đội triển khai sẽ hiệu chỉnh chương trình trực tiếp trên server và client sẽ update xuống.

Việc update từ server xuống client cũng có nhiều giải pháp. Sau đây là giải pháp mình đang sử dụng:

Giải pháp của mình là sử dụng 1 [batch file window](http://en.wikipedia.org/wiki/Batch_file) để thực hiện việc này. Batch file này làm nhiệm vụ copy file từ server về client và chỉ copy những file nào có ngày modify >= ngày update gần nhất. Để xác định ngày update gần nhất mình dùng 1 file text lưu giá trị ngày update.

```bash
:: Author | Chungtv
:: Purpose | Synchronize files from server to client
@echo off
:: Lay ngay hien tai
call :GetDate y m d
echo TODAY: %m%-%d%-%y%
set ud=%m%-%d%-%y%
:: Neu ton tai file update thi gan ngay update la ngay luu trong file
if exist "D:\Asiasoft\AE81\LastSyn.txt" set /p ud = <"D:\Asiasoft\AE81\LastSyn.txt"
::Thuc hien viec copy
net use "\\server\AsiaSoft\AE81" password /user:user
xcopy "\\server\AsiaSoft\AE81" "D:\Asiasoft\AE81" /D:%ud% /I /Y /E
::Sau khi copy xong thi luu lai ngay update
set ud=%m%-%d%-%y%
if exist "D:\Asiasoft\AE81\LastSyn.txt" del "D:\Asiasoft\AE81\LastSyn.txt"
echo %ud% > "D:\Asiasoft\AE81\LastSyn.txt"
if errorlevel 5 goto writeerror
if errorlevel 0 goto eof
:writeerror
pause Disk write error occurred.
goto eof
:GetDate yy mm dd
setlocal ENABLEEXTENSIONS
set t=2&if "%date%z" LSS "A" set t=1
for /f "skip=1 tokens=2-4 delims=(-)" %%a in (‘echo/^|date’) do (
    for /f "tokens=%t%-4 delims=.-/ " %%d in (‘date/t’) do (

    set %%a=%%d&set %%b=%%e&set %%c=%%f))

    endlocal&set %1=%yy%&set %2=%mm%&set %3=%dd%&goto :eof

    :eof
```