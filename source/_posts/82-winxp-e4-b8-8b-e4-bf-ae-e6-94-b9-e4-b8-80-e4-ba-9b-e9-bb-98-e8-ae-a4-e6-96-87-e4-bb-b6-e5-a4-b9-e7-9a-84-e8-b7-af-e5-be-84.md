---
title: winxp下修改一些默认文件夹的路径
url: 82.html
id: 82
categories:
  - 'NULL'
date: 2008-04-03 08:51:00
tags:
---

首先要在"开始"――"运行"内输入"regedit"打开注册表编辑器，然后要在"文件"下拉菜单中的"导出"功能备份好注册表，以防万一，接着在左侧窗口依次打开：  
HKEY\_CURRENT\_USER\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\\Shell Folders  
在右侧窗口里，你看到的"名称"就代表那些特殊的文件夹，"数据"就是它们所对应的默认存储路径。

  
下面介绍一下各个"名称"所代表的文件夹  
名称 含义 默认路径  
AppData 应用程序数据目录 C:\\Documents and Settings\\User name\\Application Data  
Cookies Cookies路径 C:\\Documents and Settings\\User name\\Cookies  
Desktop 桌面路径 C:\\Documents and Settings\\User name\\桌面  
Favorites 收藏夹 C:\\Documents and Settings\\User name\\Favorites  
NetHood NetHood路径 C:\\Documents and Settings\\User name\\NetHood  
Personal 我的文档 C:\\Documents and Settings\\User name\\My Documents  
PrintHood 打印 C:\\Documents and Settings\\User name\\PrintHood  
Recent 文档项路径 C:\\Documents and Settings\\User name\\Recent  
SendTo SendTo路径 C:\\Documents and Settings\\User name\\SendTo  
Start Menu 开始菜单路径 C:\\Documents and Settings\\User name\\「开始」菜单  
Templates 新建文件目录 C:\\Documents and Settings\\User name\\Templates  
Programs 程序菜单路径 C:\\Documents and Settings\\User name\\「开始」菜单\\程序  
Startup 启动路径 C:\\Documents and Settings\\User name\\「开始」菜单\\程序\\启动  
History 网页历史记录 C:\\Documents and Settings\ User name \\Local Settings\\History  
My Pictures 图片收藏 C:\\Documents and Settings\\User name\\My Documents\\My Pictures  
My Music 我的音乐 C:\\Documents and Settings\\User name\\My Documents\\My Music  
My Video 我的视频 C:\\Documents and Settings\\User name\\My Documents\\My Videos  
Cache Internet临时文件夹 C:\ Documents and Settings\\User name \\Temporary Internet Files  
这些文件夹称为Shell文件夹  
其中"User name"为当前用户的名称  
了解了对应的文件夹，就可以根据自己的需要去更改对应的路径了。（千万不要在这儿改啊，那样可就瞎忙乎了，系统重起后它会恢复成原来的路径）  
在同一层中你可以看到一个"User Shell Folders"的子键，即在HKEY\_CURRENT\_USER\\Software\\Microsoft\\Windows\\CurrentVersion\\Explorer\ User Shell Folders  
这里包括了用户定制的所有Shell文件夹的值项。只要通过修改"数据"，就可以改变它们的存储路径。双击需要修改的名称，在弹出的"编辑字符串"的"数值数据"里填上你要更改的完整路径，按下"确定"就完成了。如果没有你需要的，可以在右边窗口单击鼠标右键，选择"新建"菜单中的"字符串值"命令，对应上表，添加一个用于Shell文件夹的字符串值。  
在上面的文件夹中，并没有outlook的通讯簿和邮件存放路径，它们分别在  
通讯簿路径：  
HKEY\_CURRENT\_USER\\Software\\Microsoft\\WAB\\WAB4\\Wab File Name主键下，将"默认"键值改为你需要的路径。  
邮件存放路径：  
HKEY\_CURRENT\_USER\\Identities\\{8150FA22-A51C-4993-8A96-DC4B9A6B4C55}\\Software\\Microsoft\\Outlook Express\\5.0下，将 "Store Root"键值改为你需要的路径。  
最后别忘了将修改好的这部分注册表导出保存，以便重装系统后可以直接导入而无须再次修改。  
注意：修改了文件夹的路径值后，原有文件夹中的文件并不会移到新的文件夹中，这样做只改变了文件夹的指向。  
提示：此方法在win9x 中同样可行。此外，我的文档、Internet临时文件夹可以在它们的属性中修改，邮件存放路径可以在outlook的"工具"→"选项"→"维护"中修改。  
如果你是多操作系统的用户，可以将相同的文件夹放在同一路径下，这样既减少了硬盘的存储量，也方便了管理和访问，只是"Internet临时文件夹"的"使用的磁盘空间"要设置的相同。  
 

humen1 Tech