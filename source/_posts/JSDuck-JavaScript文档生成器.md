---
title: 'JSDuck - JavaScript文档生成器'
date: 2016-12-02 23:55:52
tags: ['JSDuck','js文档注释']
---
__文档的重要性不言而喻，对于像Javascript这种的动态语言来说就更重要了，目前流行的JDoc工具挺多的，最好的当属JSDuck，可是JSDuck在Windows下的安装非常麻烦，下面整理了一下步骤：__
### JSDuck安装步骤

##### 第一步：安装Ruby

Ruby下载地址：http://rubyinstaller.org/downloads/。
我是64位操作系统，下载的文件如下：

    rubyinstaller-2.0.0-p648-x64.exe
    安装程序到指定目录，例如我的是D盘根目录，
    注意: 安装的路径中不要有空格！（例如："D:\Program Files"是不合法的！此坑让我找了一下午啊啊啊）

##### 第二步：安装Development Kit

1、去官网下载对应的Dev Kit，例如：DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe，并解压到指定目录（我是解压到ruby安装目录下新建的“dev”目录下）；
2、进入解压的开发工具包目录：例如我的是"D:\Ruby200-x64\dev"，执行以下命令：

    cd /d D:\Ruby200-x64\dev
    ruby dk.rb init
    ruby dk.rb install


##### 第三步：安装rdiscount

    //执行如下批处理程序：
    gem install rdiscount

##### 第四步：安装jsduck

    //执行如下批处理程序：
    gem install jsduck


### JSDuck教程

##### 到此,jsduck安装完毕，让我们来尝试一下jsduck：
在命名行输入 ： jsduck jsfilepath –output outputdirectory,其中jsfilepath 代表的是js文件路径，可以是js存放的文件夹的路径，这样的话，会把整个文件夹的js文件文档生成出来，也可以单独制定某个文件，outputdirectory 是文档的输出路径

##### 官方永远是最好的学习地方：https://github.com/senchalabs/jsduck/wiki。
