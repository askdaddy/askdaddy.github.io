---
title: freebsd Tar的详细用法
url: 37.html
id: 37
categories:
  - 'NULL'
date: 2008-11-26 14:56:00
tags:
---

tar命令   
tar 文件是几个文件和（或）目录在一个文件中的集合。这是创建备份和归档的佳径。  
  
tar 使用的选项有：  
  
-c ― 创建一个新归档。  
  
-f ― 当与 -c 选项一起使用时，创建的 tar 文件使用该选项指定的文件名；当与 -x 选项  
一起使用时，则解除该选项指定的归档。  
  
-t ― 显示包括在 tar 文件中的文件列表。  
  
-v ― 显示文件的归档进度。  
  
-x ― 从归档中抽取文件。  
  
-z ― 使用 gzip 来压缩 tar 文件。   
  
-j ― 使用 bzip2 来压缩 tar 文件。   
  
要创建一个 tar 文件，键入：  
  
tar -cvf filename.tar directory/file  
  
可以使用 tar 命令同时处理多个文件和目录，方法是将它们逐一列出，并用空格间隔：  
  
tar -cvf filename.tar /home/mine/work /home/mine/school  
  
上面的命令把 /home/mine 目录下的 work 和 school 子目录内的所有文件都放入当前  
目录中一个叫做 filename.tar 的新文件里。   
  
要列出 tar 文件的内容，键入：  
tar -tvf filename.tar  
  
要抽取 tar 文件的内容，键入  
tar -xvf filename.tar  
  
这个命令不会删除 tar 文件，但是它会把被解除归档的内容  
复制到当前的工作目录下，并保留归档文件所使用的任何  
目录结构。譬如，如果这个 tar 文件中包含一个叫做  
bar.txt 的文件，而这个文件包含在 foo/ 目录中，那么，  
抽取归档文件将会导致在你当前的工作目录中创建  
foo/ 目录，该目录中包含 bar.txt 文件  
  
tar 默认不压缩文件。  
  
要创建一个使用 tar 和 bzip 来归档压缩的文件，使用 -j 选项：  
tar -cjvf filename.tbz file  
  
以上命令创建了一个归档文件，然后将其压缩为 filename.tbz 文件。如果你使用 bunzip2 命令为 filename.tbz 文件解压，filename.tbz 文件会被删除，继之以 filename.tar 文件。   
  
你还可以用一个命令来扩展并解除归档 bzip tar 文件：  
tar -xjvf filename.tbz  
  
要创建一个用 tar 和 gzip 归档并压缩的文件，使用 -z 选项：   
tar -czvf filename.tgz file  
  
这个命令创建归档文件 filename.tar，然后把它压缩为 filename.tgz 文件（文件 filename.tar 不被保留）。  
如果你使用 gunzip 命令来给 filename.tgz 文件解压，filename.tgz 文件会被删除，并被  
替换为 filename.tar。  
  
你可以用单个命令来扩展 gzip tar 文件：  
tar -xzvf filename.tgz  
  
  
  
  
一. tar  
  
1.压缩一组文件为tar.gz后缀。  
\# tar cvf backup.tar /etc  
#gzip -q backup.tar  
或  
\# tar cvfz backup.tar.gz /etc/  
tar zxvf XXXX.tar.gz  
  
tar jxvf XXXX tar.bz2  
  
2.释放一个后缀为tar.gz的文件。  
#gunzip backup.tar.gz  
#tar xvf backup.tar  
或  
\# tar xvfz backup.tar.gz  
  
3.用一个命令完成压缩  
#tar cvf - /etc/ | gzip -qc > backup.tar.gz  
  
4.用一个命令完成释放  
\# gunzip -c backup.tar.gz | tar xvf -  
  
5.如何解开tar.Z的文件？  
\# tar xvfz backup.tar.Z  
或  
\# uncompress backup.tar.Z  
#tar xvf backup.tar  
  
6.如何解开.tgz文件？  
#gunzip backup.tgz  
  
7.如何压缩和解压缩.bz2的包？  
#bzip2 /etc/smb.conf  
这将压缩文件smb.conf成smb.conf.bz2  
#bunzip2 /etc/smb.conf.bz2  
这将在当前目录下还原smb.conf.bz2为smb.conf  
注: .bz2压缩格式不是很常用，你可以man bzip2

humen1 Tech