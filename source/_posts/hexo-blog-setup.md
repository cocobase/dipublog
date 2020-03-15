---
title: Hexo打造个人博客网站
date: 2020-02-16 21:42:08
tags: Hexo
category: Hexo
---

## 修改文章底部的那个带#号的标签
实现的效果{%  asset_image xiaoguo.png 标签效果%}

具体实现的方法

修改模板的配置文件_config.yml，找到其中的 tag_icon:false 修改成 true

## 开启标签菜单项
缺省的状态下，博客网站导航菜单中只显示【首页】【归档】俩个菜单项目，为了增加【标签】菜单项目，可以按照如下操作：
1. 在终端执行：hexo new page "tags"
2. 修改Next皮肤模板的配置文件_config.yml，找到其中的 #tags: /tags/ || tags，将前面的 # 注释符号去掉。严重提醒：在冒号和/之间一定要有空格。
3. 编辑tags/index.md文件，内容如下：
```
title: "tags"
type: tags
layout: "tags"
```
重点关注layout选项的设置内容。里面的参数对应的是你主题文件夹下 layout 文件夹下第一级的布局文件。比如，我的主题是用 ejs 写的，那么对应的就是 layout/tags.ejs，如果没有，那么就会出现空白的现象！如果你的 tags 文件的命名时 a.ejs，那么你就应该写成 layout: "a"

4. 编辑 hexo 配置文件 Directory 选项。检查一下名称是否对应。
```
# Directory
tag_dir: tags
```

5. 实现的效果{%  asset_image xiaoguo-1.png 标签效果%}