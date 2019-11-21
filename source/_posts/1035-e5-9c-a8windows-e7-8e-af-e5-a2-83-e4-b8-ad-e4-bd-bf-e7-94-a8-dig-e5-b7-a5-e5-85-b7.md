---
title: 在Windows 环境中使用 Dig 工具
tags:
  - dns
url: 1035.html
id: 1035
categories:
  - network
  - Windows
date: 2017-06-03 02:20:17
---

Dig 在Linux 里一般是在 bind-utils这个包里的。 作者Windows 环境用的模拟终端为 Babun [https://github.com/babun/babun](https://github.com/babun/babun) 是基于Cygwin的。可惜，没有提供dig的二进制包。可惜。 好，其实解决方法很简单，去网上直接下个dig.exe放到Windows path里就好了=）  

### 重点 ### 此方法适用于所有Windows 命令行

A）下载： 下载地址 \[[ftp://ftp.nominum.com/pub/isc/bind9/](ftp://ftp.nominum.com/pub/isc/bind9/)\] 拉到最下面找最新版本的 ![](/uploads/2017/06/bc521979dc91c867e703522b0d1eba3e.png) 下这个 ![](/uploads/2017/06/17d81d7a6365538765dfd2166c99b981.png) A1) 准备： 解压后在目录里找到C++安装文件，双击安装 ![](/uploads/2017/06/166a3c4ba8d6b3de647fab52b8ee77e1.png) ![](/uploads/2017/06/3dd4d022aafb71fc38a29d7af49cf983.png)) B) 安装DLL文件 ![](/uploads/2017/06/968a8da2625dab1e7c0169862a806693.png) 把目录里lib*.dll拷贝到 C:\\WINDOWS\\System32\ 目录下 B1)安装dig.exe ![](/uploads/2017/06/06a9d77227053a70030916f92b92e481.png) 把目录里的dig.exe 也拷贝到 C:\\WINDOWS\\System32\ 目录下 C)完成！ 测试！ babun ![](/uploads/2017/06/40aa13970d99724a673b40d2ac1836b4.png) powershell ![](/uploads/2017/06/3fdb6b909072225d8b6de372f4f6c586.png)