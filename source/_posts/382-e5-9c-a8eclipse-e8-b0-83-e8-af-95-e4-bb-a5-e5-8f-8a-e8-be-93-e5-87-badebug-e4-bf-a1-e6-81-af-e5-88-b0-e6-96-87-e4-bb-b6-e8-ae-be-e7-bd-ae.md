---
title: 在eclipse调试以及输出Debug信息到文件设置
tags:
  - flash debugger
url: 382.html
id: 382
categories:
  - Actionscript
  - linux桌面
date: 2011-01-25 11:00:06
---

在eclipse调试 首先安装调试版flashplayer，官方下载地址为（目前最新版本） http://download.macromedia.com/pub/flashplayer/updaters/10/flashplayer\_10\_ax\_debug.exe 退出MSN,安装flashplayer 在eclipse中点击项目（右键）——properties——Run/Debug Settings——new——Flex Application配置路径即可。 Flex输出Debug信息到文件 Flash Debug Player有两种方法记录日志信息到日志文件中。 1、全局的trace()函数。 2、Logging API。Logging API实现了TraceTarget类，提供类似trace()函数一样的功能。 例如可以记录Flex程序运行时产生的deubg、error、warning信息。 Flash Debug Player保存日志信息到一个叫flashlog.txt的文件中。 flashlog.txt文件的位置 --------------------------------------------------------------------------------- Windows 95/98/ME/2000/XP C:\\Documents and Settings\\username\\Application Data\\Macromedia\\Flash Player\\Logs\ Windows Vista 　　 C:\\Users\\username\\AppData\\Roaming\\Macromedia\\Flash Player\\Logs\ Mac OS X 　　　　/Users/username/Library/Preferences/Macromedia/Flash Player/Logs/ Linux 　　　　 /home/username/.macromedia/Flash\_Player/Logs/ --------------------------------------------------------------------------------- 提示1：你需要手动创建Logs目录，至少在Windows系统中是这样的。 提示2：上面的路径中提到的username为你的用户名 如果要让Flash Debug Player把日志记录到日志文件中，我们还需要手动创建一个mm.cfg的文件。 mm.cfg文件的位置 --------------------------------------------------------------------------------- Windows 95/98/ME/2000/XP 　 %HOMEDRIVE%\\%HOMEPATH% Windows 2000/XP 　　 C:\\Documents and Settings\\username\ Windows Vista 　　　　C:\\Users\\username\ Mac OS X 　　　　 /Library/Application Support/Macromedia Linux 　　　　 /home/username/ --------------------------------------------------------------------------------- 提示：上面的路径中提到的username为你的用户名 mm.cfg文件包含许多控制日志信息的设置项 如果只是记录Error和trace信息到日志文件，只需要在mm.cfg文件中加入下面两行文字。 ErrorReportingEnable=1 TraceOutputFileEnable=1 设置之后，调用trace()方法就可以把输出的日志信息写入到flashlog.txt文件中了。 例如： trace("Hello,1901!"); 在MXML中加入如下代码，允许记录所有Flex产生的日志信息到flashlog.txt文件中：