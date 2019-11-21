---
title: Document root must be a directory
url: 9.html
id: 9
categories:
  - 技术杂文
date: 2009-04-11 20:33:00
tags:
---

这是系统起了SELinux的策略。把目录或文件设成了user\_home\_t类型，因此apache的进程没有权限，无法访问。针对Apache的进程所使用的SELinux  
target policy规定了apache的进程只能访问httpd\_sys\_content_t类型的目录或文件。  
解决办法：  
把目录或文件的策略类型改成 httpd\_sys\_content_t 就可以了。  
\# chcon -R -h -t httpd\_sys\_content_t /data  
然后可以用 ls -laZ 命令查看文件目录的策略类型。

humen1 Tech![](https://blogger.googleusercontent.com/tracker/7269874978253342363-4738905437927691155?l=www.humen1.net)