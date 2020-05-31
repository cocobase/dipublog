---
layout: hexo文章分类菜单和功能支持的配置
title: hexo-category-config
date: 2020-05-30 16:22:51
tags: Hexo
---

Hexo的Category分类管理文章功能是需要配置以后才会正常显示的。

## 创建“分类”选项
1. 生成分类页并添加type属性
   打开命令行，进入博客所在的文件夹，执行命令
```
hexo new page categories
```
成功后会提示： Info Created: ~/....../blog/source/categories/index.md  
根据上面提示的路径找到index.md这个文件，打开后修改默认的内容，重点是增加了一样内容：type: "categories"
```
---
title: 文章分类
date：
type: "categories"
layout: "categories"
comments: false
---
```  

配置theme下面的_config.yml文件，寻找到其中的menu部分，将categories:前面的注释符号去掉，以开启分类菜单
``` bash
menu:
  home: / || home
  #about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
```

2. 给文章增加"categories"属性
   打开需要添加分类的文章，为该文章添加categories属性。hexo文章只能属于一个分类。如果在下面举例中的"-web前端"分类下方添加"-xxx"分类，hexo不会产生两个分类，而是把分类嵌套（该文章属于“-web前端"分类下的"-xxx”分类
```
---
title: xxxx
date: xxxx-xx-xx xx:xx:xx
categories:
- web前端
---
```
