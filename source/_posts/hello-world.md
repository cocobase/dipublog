---
title: 你好新世界
date: 2020-1-30 20:00:00
author: hunter huang
tags: Hexo
---
无比喜悦地使用 [Hexo](https://hexo.io/)! 这是第一篇博客文章。前往 [说明文档](https://hexo.io/docs/) 获取更多的信息。 如果在使用Hexo的过程中发现任何问题，你可以到[troubleshooting](https://hexo.io/docs/troubleshooting.html) 中找到答案或者你可以去[GitHub](https://github.com/hexojs/hexo/issues) 向开发人员提问。

## 快速开始

### 发表一篇新的文章

``` bash
$ hexo new "My New Post"
```

更多信息参考： [Writing](https://hexo.io/docs/writing.html)

### 启动网站服务器

``` bash
$ hexo server
```

更多信息参考： [Server](https://hexo.io/docs/server.html)

### 生产静态文件

``` bash
$ hexo generate
```

更多信息参考： [Generating](https://hexo.io/docs/generating.html)

### 部署内容到远程的站点

``` bash
$ hexo deploy
```

更多信息参考： [Deployment](https://hexo.io/docs/one-command-deployment.html)

### Markdown语法
* 分段：两个回车,注意：换行不是分段的标识，空行才是
* 换行：两个空格加回车
* 引用：>
> 这是引用的文字效果和显示，如何分成两行
* 转义：针对>需要转义的一些场合
```
\<
&lt;
&#60;
```
* 标题：标题 # ~ ###### 井号的个数表示几级标题，即Markdown可以表示一级标题到六级标题
* 列表：*，+， -，1. 四个任选其一都可以，注意后面的空格
* 强调：
```
**文字**， __文字__, _文字_, *文字*, ~~删除文字~~
```
效果：**文字**， __文字__, _文字_, *文字*, ~~删除文字~~
* 图片的使用：
```
{% asset_img xxxx.jpeg 图片说明文字 %} 
```
* 分级显示的代码和效果
```
+ Level1
  + level2
    + level3 
```
+ Level1
  + level2
    + level3 


* 脚注
  
  为名词提供注释，注释将显示在文章末尾
    
    语法：
  
  待解释文字\[^脚注 id]
  
  \[^脚注 id]:注释内容
  ```
  Hello World[^hello]
  [^hello]:你好, 世界
  ```
  Hello World[^hello]  
  [^hello]:你好，世界


* 表格
  ```
  |姓名|年龄|性别|身高(cm)|  
  |-|:-|:-:|-:|  
  |张三|22|男|180|  
  |李四|18|女|165|
  ```
  |姓名|年龄|性别|身高(cm)|  
  |-|:-|:-:|-:|  
  |张三|22|男|180|  
  |李四|18|女|165|