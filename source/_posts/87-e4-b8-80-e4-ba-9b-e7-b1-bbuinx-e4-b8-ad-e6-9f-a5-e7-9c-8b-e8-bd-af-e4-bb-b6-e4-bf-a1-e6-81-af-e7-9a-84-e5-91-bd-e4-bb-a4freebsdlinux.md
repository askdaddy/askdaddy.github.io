---
title: '一些类uinx中查看软件信息的命令[freebsd&linux]'
url: 87.html
id: 87
categories:
  - 'NULL'
date: 2008-03-26 10:19:00
tags:
---

查看软件安装的位置  
  
\# pkg_info �L softwarename | less  
查看软件安装的版本  
  
\# pkg_info | grep softwarename  
查看这个软件的具体信息  
  
\# pkg_info software  
linux/freebsd查看目录大小的命令  
  
freebsd的命令:  
  
在某个目录里执行  
  
#du -h -d 1  
可以查看目录里的每个子目录的大小  
  
linux下的命令则为:  
  
#du -h --max-depth=1  
  

humen1 Tech