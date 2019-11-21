---
title: Google排名优化－面向Google(Search Engine Friendly)的URL设计
tags:
  - php
url: 97.html
id: 97
categories:
  - 'NULL'
date: 2008-01-30 14:13:00
---

不得不承认，将动态网页链接rewriting成静态链接是最保险和稳定的面向搜索引擎优化方式 此外随着互联网上的内容以惊人速度的增长也越来越突出了搜索引擎的重要性，如果网站想更好地被搜索引擎收录，网站设计除了面向用户友好（User Friendly）外，搜索引擎友好（Search Engine Friendly）的设计也是非常重要的。进入搜索引擎的页面内容越多，则被用户用不同的关键词找到的几率越大。在Google的算法调查一文中提到一个站点被Google索引页面的数量其实对PageRank也是有一定影响的。由于Google 突出的是整个网络中相对静态的部分（动态网页索引量比较小）,链接地址相对固定的静态网页比较适合被Google索引（怪不得很多大网站的邮件列表归档和BLOG按日期归档的文档很容被搜的到），因此很多关于面向搜索引擎 URL设计优化(URI Pretty)的文章中提到了很多利用一定机制将动态网页参数变成像静态网页的形式：比如可以将：[http://phpunixman.sourceforge.net/index.php?mode=man¶meter;=ls](http://phpunixman.sourceforge.net/index.php?mode=man&parameter=ls)变成：[http://phpunixman.sourceforge.net/index.php/man/ls](http://phpunixman.sourceforge.net/index.php/man/ls)  
  
实现方式主要有2种：  
  
基于url rewriteIIS的ISAPI REWRITE下载（免费） 基于path_info 把URI地址用作参数传递：URL REWRITE  
  
最简单的是基于各种WEB服务器中的URL重写转向（Rewrite）模块的URL转换：这样几乎可以不修改程序的实现将 news.asp?id=234 这样的链接映射成 news/234.html，从外面看上去和静态链接一样。Apache服务器上有一个模块（非缺省）：mod_rewrite：URL REWRITE功能之强大足够写上一本书。  
  
当我需要将将news.asp?id=234的映射成news/234.html时，只需设置：RewriteRule /news/(\\d+)\\.html /news\\.asp\\?id=$1 \[N,I\]这样就把 /news/234.html 这样的请求映射成了 /news.asp?id=234当有对/news/234.html的请求时：web服务器会把实际请求转发给/news.asp?id=234  
  
而在IIS也有相应的REWRITE模块：比如ISAPI REWRITE和IIS REWRITE，语法都是基于正则表达式，因此配置几乎和apache的mod_rewrite是相同的：  
  
比对于某一个简单应用可以是：RewriteRule /news/(\\d+)\\.html /news/news\\.php\\?id=$1 \[N,I\]这样就把 [http://www.chedong.com/news/234.html](http://www.chedong.com/news/234.html) 映射到了 [http://www.chedong.com/news/news.php?id=234](http://www.chedong.com/news/news.php?id=234)  
  
一个更通用的能够将所有的动态页面进行参数映射的表达式是：把 [http://www.myhost.com/foo.php?a=A&b;=B&c;=C](http://www.myhost.com/foo.php?a=A&b=B&c=C) 表现成 [http://www.myhost.com/foo.php/a/A/b/B/c/C](http://www.myhost.com/foo.php/a/A/b/B/c/C)。RewriteRule (.*?\\.php)(\\?\[^/\]*)?/(\[^/\]*)/(\[^/\]*)(.+?)?$1(?2$2&:\\?)$3=$4?5$5: \[N,I\]  
  
以下是针对phpBB的一个Apache mod_rewrite配置样例：  
  
RewriteEngine On RewriteRule /forum/topic_(.+)\\.html$ /forum/viewtopic.php?t=$1 \[L\] RewriteRule /forum/forum_(.+)\\.html$ /forum/viewforum.php?f=$1 \[L\] RewriteRule /forum/user_(.+)\\.html$ /forum/profile.php?mode=viewprofile&u;=$1 \[L\] 这样设置后就可以通过topic\_1234.html forum\_2.html user_34.html这样的链接访问原来的动态页面了。  
  
通过URL REWRITE还有一些好处：mod\_rewrite和isapirewrite基本兼容，但是还是有些不同，比如：isapirewrite中"?"需要转义成"\\?"，mod\_rewrite不用，isapirewrite支持 "\\d+" （全部数字），mod_rewrite不支持  
  
隐藏后台实现：这在后台应用平台的迁移时非常有用：当从asp迁移到java平台时，对于前台用户来说，根本感受不到后台应用的变化； 简化数据校验：因为像(\\d+)这样的参数，可以有效的控制数字的格式甚至位数； 比如我们需要将应用从news.asp?id=234迁移成news.php?query=234时，前台的表现可以一直保持为 news/234.html。从实现应用和前台表现的分离：保持了URL的稳定性，而使用mod_rewrite甚至可以把请求转发到其他后台服务器上。  
  
基于PATH\_INFO的URL美化Url美化的另外一个方式就是基于PATH\_INFO：PATH\_INFO是一个CGI 1.1的标准，经常发现很多跟在CGI后面的"/value\_1/value\_2"就是PATH\_INFO参数：比如：[http://phpunixman.sourceforge.net/index.php/man/ls](http://phpunixman.sourceforge.net/index.php/man/ls) 中：$PATH_INFO = "/man/ls"  
  
PATH\_INFO是CGI标准，因此PHP Servlet等都有的支持。比如Servlet中就有request.getPathInfo()方法。注意：/myapp/servlet/Hello/foo的 getPathInfo()返回的是/foo，而/myapp/dir/hello.jsp/foo的getPathInfo()将返回的 /hello.jsp，从这里你也可以知道jsp其实就是一个Servlet的PATH\_INFO参数。ASP不支持PATH\_INFO PHP中基于PATH\_INFO的参数解析的例子如下：//注意：参数按"/"分割，第一个参数是空的：从/param1/param2中解析出$param1 $param2这2个参数if ( isset($\_SERVER\["PATH\_INFO"\]) ) { list($nothing, $param1, $param2) = explode('/', $\_SERVER\["PATH\_INFO"\]);}  
  
如何隐蔽应用：例如 .php，的扩展名：在APACHE中这样配置： ForceType application/x-httpd-php  
  
如何更像静态页面：app\_name/my/app.html解析的PATH\_INFO参数的时候，把最后一个参数的最后5个字符".html"截断即可。注意：APACHE2中缺省是不允许PATH_INFO的，需要设置 AcceptPathInfo on  
  
特别是针对使用虚拟主机用户，无权安装和配置mod\_rewrite的时候，PATH\_INFO往往就成了唯一的选择。  
  
OK，这样以后看见类似于[http://www.example.com/article/234](http://www.example.com/article/234)这样的网页你就知道可能是 article/show.php?id=234这个php程序生成的动态网页，很多站点表面看上去可能有很多静态目录，其实很有可能都是使用1，2个程序实现的内容发布。比如很多WIKIWIKI系统都使用了这个机制：整个系统就一个简单的wiki程序，而看上去的目录其实都是这个应用拿后面的地址作为参数的查询结果。  
  
利用基于MOD\_REWRITE/PATH\_INFO ＋ CACHE服务器的解决方案对原有的动态发布系统进行改造，也可以大大降低旧有系统升级到新的内容管理系统的成本。并且方便了搜索引擎收录入索引。  
  
附：如何在IIS上利用PHP支持PATH_INFOPHP的ISAPI模式安装备忘：只试成 php-4.2.3-Win32  
  
解包目录========php-4.2.3-Win32.zip c:\\php  
  
PHP.INI初始化文件=================复制：c:\\php\\php.ini-dist 到 c:\\winnt\\php.ini  
  
配置文件关联============按照install.txt中的说明配置文件关联  
  
运行库文件==========复制 c:\\php\\php4ts.dll 到 c:\\winnt\\system32\\php4ts.dll  
  
这样运行后：会发现php把PATH_INFO映射到了物理路径上Warning: Unknown(C:\\CheDong\\Downloads\\ariadne\\www\\test.php\\path): failed to create stream: No such file or directory in Unknown on line 0  
  
Warning: Unknown(): Failed opening 'C:\\CheDong\\Downloads\\ariadne\\www\\test.php\\path' for inclusion (include_path='.;c:\\php4\\pear') in Unknown on line 0  
  
安装ariadne的PATCH==================停止IIS服务net stop iisadmin[ftp://ftp.muze.nl/pub/ariadne/win/iis/php-4.2.3/php4isapi.dll](ftp://ftp.muze.nl/pub/ariadne/win/iis/php-4.2.3/php4isapi.dll)覆盖原有的c:\\php\\sapi\\php4isapi.dll  
  
注：ariadne是一个基于PATH\_INFO的内容发布系统，PHP 4.3.2 RC2中CGI模式的PATH\_INFO已经修正，照常安装即可。  
  
参考资料：URL Rewrite文档：ISAPI REWRITE文档IIS的ISAPI REWRITE下载（免费）[http://httpd.apache.org/docs/mod/mod_rewrite. html](http://httpd.apache.org/docs/mod/mod_rewrite.html)[http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html](http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html)  
  
搜索引擎友好的URL设计[http://www.sitepoint.com/article/485](http://www.sitepoint.com/article/485)说不定这个URL原来就是articel.php?id=485  
  
一个基于PATH_INFO的开源内容管理系统[http://typo3.com/](http://typo3.com/)  
  
Google的PageRank算法说明：[http://pr.efactory.de/](http://pr.efactory.de/)

humen1 Tech