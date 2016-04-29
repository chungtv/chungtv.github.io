---
layout: post
title: Thay đổi đường dẫn Local trong Team Foundation Server
date: 2015-10-23 08:57:17
categories: [Work, Tips and tricks]
tags: [TFS,Source Control,Visual Studio]
published: True
redirect_from:
  - /tfs/2015/10/23/thay-%C4%91%E1%BB%95i-%C4%91%C6%B0%E1%BB%9Dng-d%E1%BA%ABn-local-trong-team-foundation-server.html
---

Đôi khi vì lý do gì đó bạn cần thay đổi đường dẫn `Local path` đã được map bởi Team Foundation Server Source control. Để thực hiện việc này, bạn mở Visual Studio, vào `File / Source Control / Workspaces`. 

![](/images/2015/10/tfs_manage_workspaces.png)

Trên cửa sổ `Manage Workspaces`, bạn chọn Workspace cần thay đổi, nhấn **Edit ...**, chương trình hiển thị màn hình `Edit Workspace`

![](/images/2015/10/tfs_edit_workspace.png)

Trên màn hình này, bạn thay đổi đường dẫn mới tại cột **Local Folder**

