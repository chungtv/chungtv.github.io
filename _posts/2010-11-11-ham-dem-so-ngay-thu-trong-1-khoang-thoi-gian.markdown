---
layout: post
title: Hàm đếm số ngày thứ trong 1 khoảng thời gian
date: '2010-11-11 05:00:00'
categories: [Work, Tips and tricks]
tags: [MS SQL Server]
redirect_from: /ham-dem-so-ngay-thu-trong-1-khoang-thoi-gian/
---

> Đôi khi mình cần phải đếm số thứ trong một khoảng thời gian nào đó. Ví dụ: Cần đếm xem trong tháng 11 có bao nhiêu ngày thứ 2, hay bao nhiêu ngày thứ 3. 

`User Defined Function` sau đây nhận vào 3 tham số ngày bắt đầu, ngày kết thúc và ngày thứ cần đếm. Trả về số ngày thứ trong khoảng thời gian truyền vào (từ ngày bắt đầu đến ngày kết thúc)

~~~ sql
-- =============================================
-- Author:        Chungtv
-- Create date: 11/11/2010
-- Description:    Dem so ngay thu trong mot khoang thoi gian bat ky
-- @pBeginDate: Ngay bat dau khoang thoi gian can dem
-- @pEndDate: Ngay ket thuc khoang thoi gian can dem
-- @pWeekday: Ngay thu can dem (CN~1; Thu2~2, Thu3~3 ...)
-- Example:
--        SET DATEFORMAT DMY
--        SET DATEFIRST 1
--        PRINT [dbo].[afCountOfWeekday]('01/11/2010','30/11/2010',2)
-- =============================================
CREATE FUNCTION [dbo].[afCountOfWeekday]
(
    @pBeginDate smalldatetime,
    @pEndDate smalldatetime,
    @pWeekday int
)
RETURNS int
AS
BEGIN
    declare @iBeginWd int, @d1 int, @d2 int
    set @iBeginWd = datepart(dw,@pBeginDate)
    set @d1 = datediff(day,@pBeginDate,@pEndDate) 
    if @pWeekday >= @iBeginWd
        set @d2 = @pWeekday - @iBeginWd
    else
        set @d2 = @pWeekday + 7 - @iBeginWd
    return (@d1 - @d2) / 7 + 1
END
~~~