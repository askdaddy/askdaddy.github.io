---
title: 类UNIX操作系统中查看BOIS信息
tags:
  - linux
url: 529.html
id: 529
categories:
  - linux server
date: 2013-02-19 15:52:09
---

DMI (Desktop Management Interface, DMI)就是帮助收集电脑系统信息的管理系统。 使用 Dmidecode 这个工具可以查看硬件的各种信息。 Dmidecode 应该在主流的 Linux 发行版中都可以找到，因此你只需通过所用发行版的包管理器安装即可，如： aptitude install dmidecode # Debian/Ubuntu yum install dmidecode # Fedora pacman -S dmidecode # Arch Linux emerge -av dmidecode # Gentoo 在linux上，我们可以使用dmidecode来查找DMI信息，其中的“system information”就包含了这些系统信息，如： [![命令截图](/uploads/2013/02/选区_002.png "选区_002")](http://www.humen1.net/?attachment_id=530)               -t 是指定要查看的信息类型 可以看下dmidecode的在线帮助，还有很多种信息的 [![](/uploads/2013/02/选区_003.png "选区_003")](http://www.humen1.net/?attachment_id=531)