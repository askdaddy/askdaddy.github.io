---
title: Zend studio 6 for eclipse 自带插件 phpDocumentor 生成文档 编码问题
url: 78.html
id: 78
categories:
  - 'NULL'
date: 2008-04-12 10:51:00
tags:
---

  
  
  
用了大概2个月的Zend for eclipse  
其中一个插件功能我很喜欢，就是phpDocumentor 了，自动生成代码文档  
但是其中还是有个小问题的，默认的生成编码是iso-8859-1。但是我是用utf-8来编写代码的，而且注释用了中文。直接打开生成后的文档就会出现乱码\[这个时候放在apache里用网站方式浏览倒不会出现乱码了，因为编码以apache指定的优先\]。  
于是我决定应该解决这个小问题。  
  
开始第一步查出什么地方指定了编码  
我用emedit在文件中查找，发现了原来编码的指定是做在模板里的而不是想我想的放在某个配置文件里。  
模板路径见下，我的zend按在D:\  
D:\\Program Files\\Zend\\Zend Studio for Eclipse - 6.0.0\\plugins\\com.zend.php.phpdocumentor_6.0.0.v20080107\\Resources\\phpdocumentor\\phpDocumentor\\Converters\\HTML  
我只用html，在上一层目录里还有 chm、xml、pdf等  
  
这个目录里还分frames和smarty这两类生成的时候我都要用所以替换编码就在这个目录进行  
  
用emedit 在文件中替换 功能将iso-8859-1替换成 utf-8就好了  
  
然后再生成下，发现可以直接打开而不乱码了。

humen1 Tech