---
layout: post
title: Thay đổi đường dẫn Local trong Team Foundation Server
date: 2015-10-23 08:57:17
categories: [Work, Tips and tricks]
tags: [TFS,Source Control,Visual Studio]
published: True
---

Đôi khi vì lý do gì đó bạn cần thay đổi đường dẫn `Local path` đã được map bởi Team Foundation Server Source control. Để thực hiện việc này, bạn mở Visual Studio, vào `File / Source Control / Workspaces`. 

![](/images/2015/10/tfs_manage_workspaces.png)

Trên cửa sổ `Manage Workspaces`, bạn chọn Workspace cần thay đổi, nhấn **Edit ...**, chương trình hiển thị màn hình `Edit Workspace`

![](/images/2015/10/tfs_edit_workspace.png)

Trên màn hình này, bạn thay đổi đường dẫn mới tại cột **Local Folder**


{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}

{% highlight sql linenos %}
select * from abc where t = '11'
{% endhighlight %}

~~~ ruby
module Jekyll
  class TagIndex < Page
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      tag_title_prefix = site.config['tag_title_prefix'] || 'Tagged: '
      tag_title_suffix = site.config['tag_title_suffix'] || '&#8211;'
      self.data['title'] = "#{tag_title_prefix}#{tag}"
      self.data['description'] = "An archive of posts tagged #{tag}."
    end
  end
end
~~~

[Link link]({% post_url 2015-05-21-mo-2-tai-khoan-skype-tren-cung-mot-may-tinh %})