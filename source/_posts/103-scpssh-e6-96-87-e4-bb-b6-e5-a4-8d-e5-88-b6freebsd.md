---
title: 'scp(ssh文件复制)[freebsd]'
tags:
  - unix
url: 103.html
id: 103
categories:
  - 'NULL'
date: 2007-12-25 01:18:00
---

SSH提供了一些命令和shell用来登录远程服务器。在默认情况下它不允许你拷贝文件，但是还是提供了一个"scp"命令。上传：scp 源文件 用户名＠主机：目的文件名。scp －r 原文件夹 用户名＠主机：目的文件夹。下载：scp 用户名＠主机：／path／文件名 ／path／文件名。

humen1 Tech