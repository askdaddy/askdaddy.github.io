---
title: 关于使用zend studio for eclipse不能激活代码提示功能的解决办法
url: 10.html
id: 10
categories:
  - 技术杂文
date: 2009-04-08 10:54:00
tags:
---

相信有蛮多人用zend studio for  
eclipse写代码吧，但有时候好好的一个项目就突然没得语法提示，很郁闷。其实这是项目没有经过zend studio for eclipse  
编译（应该是建立索引吧）导致的，那么就只要让它重新编译项目代码即可。  
操作如下：  
随便新建一个项目，比如test。然后找到test项目所在的目录，把目录下的.cache和.setting都复制到要重编译的项目的目录下，把test项目中的.project中的name改成要重编译的项目的项目名称，再复制到该目录下替换掉原有的.project.重启等待编译完成即可解决代码提示问题。

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-6011607723432257322?l=www.humen1.net)