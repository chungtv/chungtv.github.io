---
layout: post
title: Xóa code trên Forms và Class của Foxpro
date: '2011-05-16 05:00:00'
---

> Tiện có bạn trên DDTH hỏi về vấn đề này, mình viết một bài hướng dẫn:

Các bạn có thể thấy, phần lớn các sản phẩm Fox thương mại đều bị xóa code trên form và class vì thế nên khi modify lên mọi người đều không thể đọc được code.

Vậy tôi đã làm như thế nào để có thể xóa code trên form và class?

Bản chất các đối tượng trong VFP đều là table. Form, class hay report cũng đều là table cả thôi. Khi code trên form và class, sau khi lưu lại toàn bộ nội dung code sẽ được vfp compile và lưu vào trường ObjCode, còn nội dung code thì sẽ được lưu tại trường Methods.

Khi run form hay class, VFP sẽ thực hiện từ cái đã compile chứ không bao giờ lại đi compile lại. Vì thế, bạn có thể yên tâm khi xóa nội dung của trường Methods đi mà không sợ chương trình không chạy được và cũng không sợ người khác đọc được bạn đã code gì trên form đó (tất nhiên, bạn phải backup project của mình trước).

Sau đây là ví dụ dùng để xóa code của form cactpc1

```
	USE ../Forms/Cactpc1.scx

	REPLACE ALL Methods WITH []

	USE IN cactpc1
```

Hay xóa code trong class lib Startup

```
    USE ../Libs/Startup.vcx

    REPLACE ALL Methods

    WITH [] USE IN startup
```

