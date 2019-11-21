---
title: 为什么要使用PDO进行PHP程序开发？
url: 123.html
id: 123
categories:
  - 'NULL'
date: 2007-12-29 11:38:00
tags:
---

  

先来看看PHP MANUAL对PDO的定义。  
\[原文\]  
The PHP Data Objects (PDO) extension defines a lightweight, consistent interface for accessing databases in PHP. Each database driver that implements the PDO interface can expose database-specific features as regular extension functions. Note that you cannot perform any database functions using the PDO extension by itself; you must use a database-specific PDO driver to access a database server.

PDO provides a data-access abstraction layer, which means that, regardless of which database you're using, you use the same functions to issue queries and fetch data. PDO does not provide a database abstraction; it doesn't rewrite SQL or emulate missing features. You should use a full-blown abstraction layer if you need that facility.  
\[译文\]  
PDO扩展为PHP定义了一个访问数据库的轻量的，持久的接口。实现了PDO接口的每一种数据库驱动都能以正则扩展的形式把他们各自的特色表现出来。注意；利用PDO扩展本身并不能实现任何数据库函数。你必须使用一个特定的数据库PDO驱动去访问数据库。  
PDO提供了一个数据访问抽象层，这就意味着，不管你使用的是哪种数据库，你都可以用同样的函数去进行查询的获取数据。PDO并不提供数据提取，它不会重写SQL语句，或者模仿这些 功能![](http://leiyanstatic.xunlei.com/img/defaultflag.gif)。你需要使用一个成熟的提取层，如果你需要的话。

怎么样，是不是看了译文就有一种恍然大悟的感觉了？  
没有？  
那说的再详细点。  
我们为什么要使用PDO？  
1、更换数据库时取得极大便利  
在PHP4/3时代，PHP要利用php\_mysql.dll、php\_pgsql.dll、php\_mssql.dll、php\_sqlite.dll等等扩展来连接MySQL、PostgreSQL、MS SQL Server、SQLite，这其实也没什么。也就是在配置时多添句话就行了。  
可怕的是，这些扩展和各自对应的数据库打交道时，他们各自的函数有很多是不一样的。  
比如：  
PHP利用libmysql.dll和MYSQL打交道时，如果要从数据表中提取数据作为关联数组，用的是mysql\_fetch\_accoc，而如果要从postgre数据库取得同样的结果，你就不得不用pg\_fetch\_assoc。  
很简单的例子说明了很重要的问题，假如你要更换数据库类型，比如从MYSQL更换成POSTGRE，你就不得把你所有和数据库有关的程序都改一遍。这时候，你应该会明白，为什么我不用PDO？？  
2、极大提高程序运行效率  
针对上面的情况，也许你会说，我可以使用ADODB(LITE)，PEAR::db来实现对不同类型数据库函数的封装啊。这样子，即使我更换数据库，也不需要修改程序。  
答：php代码的效率怎么能够和直接用C/C++写的扩展效率比较呢？根本不是一个数量级的。  
OK，从现在开始用PDO进行你的开发吧。

humen1 Tech