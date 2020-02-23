---
title: Hexo中的Markdown文件里图片的显示问题
date: 2020-2-15 20:00:00
author: hunter huang
tags: Hexo
---

hexo的博客系统默认无法自动处理文章中插入本地图片的问题。需要通过扩展的插件来完成图片支持。

## 图片路径设置
配置_config.yml文件里面的 post_asset_folder:false 这个选项为 true。
  
安装[hexo-asset-image](https://github.com/7ym0n/hexo-asset-image)插件，运行hexo n "xxx"来生成新的博客文章时候，/source/_posts文件夹内除了 xxx.md文件之外，还会有一个同名的文件夹，把需要在md文件中显示的图片放入该文件夹。使用!就可以插入图片。
  
```  
npm install hexo-asset-image --save
```
    
如果觉得速度太慢，可以从淘宝的镜像站点，cnpm站点安装该插件的程序包。前提是你要安装好了[cnpm](https://npm.taobao.org)。
```
cnpm install hexo-asset-image --save
```

## hexo-asset-image插件的问题
由于hexo3版本后对很多插件支持有问题，hexo-asset-image插件在处理data.permalink链接时出现路径错误，把年月去掉了，导致最后生成的路径为%d/xxx/xxx需要对其做兼容处理。通过判断当前版本是否等于3的版本做不同的路径分割。

## 该方法经过尝试存在BUG，不建议使用
参考另外一个博客中图片的使用方法【图片测试博客】{% post_link hello-image 图片测试文章 %}