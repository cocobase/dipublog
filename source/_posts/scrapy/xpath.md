---
title: Scrapy的Xpath用法
date: 2020-04-21 09:26:18
tags: [爬虫,Scrapy]
keywords: 爬虫,Scrapy
---

## 什么是xpath
Xpath是一门在XML文档中查找信息的语言，可以对XML文档中的元素和属性使用路径表达式进行导航，Xpath包含一个标准函数库。  
一般来说，使用id、name、class等属性就能对节点进行定位就能解决绝大部分解析需求，但有时候遇到以下情况，使用Xpath就更方便：
* 没有id、name、class等
* 标签的属性或者文本特征不显著
* 标签嵌套层次太复杂

<!--more-->

## xpath常用标签  
/ ------提取某个标签下的所有内容  
text() ------- 提取标签所包含的文本内容  
@ ---------- 提取标签属性的信息  
// ---------- 寻找所有的标签  
[@属性=值] ------ 定位标签  

### Xpath定位方法：Xpath路径
{% asset_img xpath-route.png xpath路径 %} 
举例一:定位节点  
```js
#查找html下的body下的form下的所有input节点
/html/body/form/input

#查找所有input节点
//input
```
举例二:通配符*选择未知的节点  
```js
#查找form节点下的所有节点
//form/*#查找所有节点//*

#查找所有input节点（input至少有爷爷辈亲戚节点）

//*/input
```
{% asset_img xpath-main.png 主语 %}

## 使用索引
如果筛选时元素时出现多个节点，但我们想确定唯一节点。可以使用类似于列表索引的方式精确定位。  
举例一：  
```js
#定位 第8个td下的 第2个a节点
//*/td[7]/a[1]

#定位 第8个td下的 第3个span节点
//*/td[7]/span[2]

#定位 最后一个td下的  最后一个a节点
//*/td[last()]/a[last()]
```
{% asset_img xpath-wei.png 谓语 %}  

## 使用属性
为了让定位更精准，跟使用索引类似，我们要增加信息量，那么还可以使用属性。@符号是属性符  
举例一：  
```js
#定位所有包含name属性的input节点
//input[@name]

#定位含有属性的所有的input节点
//input[@*]

#定位所有value=2的input节点
//input[@value='2']

#使用多个属性定位
//input[@value='2'][@id='3']
或者//input[@value='2' and @id='3']
```
{% asset_img xpath-express.png 表达式 %}

## 使用举例
/html -----代表提取html标签内的所有内容  
/html/head/title -----代表提取title下面的所有信息  
//li ------ 代表提取所有的li标签  
//li[@class='hidden-xs'] -------- 直接定位到满足条件的标签  
//li[@class='hidden-xs']/a/@heef ---------- 提取到class = hidden-cs的li标签下面的a标签的href的值

## 常用函数
除了索引、属性外，Xpath还可以使用便捷的函数来增强定位的准确性。下面试常用的几个函数：  
{% asset_img xpath-func.png 常用函数 %}
```html
<a class="menu_hot" href="/ads/auth/promote.html">应用推广</a>
```
```js
#定位href属性中包含“promote.html”的所有a节点
//a[contains(@href,'promote.html')]

#元素内的文本为“应用推广”的所有a节点
//a[text()='应用推广']

#href属性值是以“/ads”开头的所有a节点
//a[starts-with(@href,'/ads')]
```

## xpath轴
这部分类似BeautifulSoup中的sibling、parents、children方法。  
{% asset_img xpath-zhou.png xpath轴 %}

## scrapy中使用xpath
爬取html页面的title标签内容和class=‘note’的div标签下的内容
```python
def next(self,response):
    title = response.xpath("/html/head/title/text()").extract()
    note = response.xpath("//div[@class = 'note']/text()").extract()
    print(title)
    print(note)
```

## 常用学习参考链接
[Scrapy官方文档中的xpath使用方法](https://doc.scrapy.org/en/xpath-tutorial/topics/xpath-tutorial.html)