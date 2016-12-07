---
title: hero博客的yilia主题修改头像和网页favicon图标
date: 2016-11-13 21:12:50
tags: [hexo,yilia,修改头像,修改favicon]
---
hexo下载yilia主题，使用后，可以自己修改左侧头像和页卡favicon图标，具体方法如下：
- 在hexo项目的路径/themes/yilia下有"_config.yml"文件，找到并打开
- 找到"avatar:"项或"favicon:"项，后面写上你的图片路径
##### ps：需要注意的是这里路径可以写相对路径或网上的在线图片地址，
- 相对路径的话，在工程的source目录下，新建一个img文件夹，把头像图片放在此文件夹下，则地址可以写为'../../img/avatar.jpeg'
- 在线路径：例如：http://imgsrc.baidu.com/forum/pic/item/e00473f082025aaf2a507b70f9edab64024f1ac5.jpg