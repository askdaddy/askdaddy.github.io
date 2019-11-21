---
title: 如何使用robots.txt ！！？？
url: 66.html
id: 66
categories:
  - 'NULL'
date: 2008-05-22 15:25:00
tags:
---

◆什么是robots.txt文件?  
robots.txt 文件对抓取网络的搜索引擎漫游器（称为漫游器）进行限制。这些漫游器是自动的，在它们访问网页前会查看是否存在限制其访问特定网页的 robots.txt 文件。如果你想保护网站上的某些内容不被搜索引擎收入的话，robots.txt 是一个简单有效的工具。这里简单介绍一下怎么使用它。

◆如何放置 Robots.txt 文件  
robots.txt自身是一个文本文件。它必须位于域名的根目录中并 被命名为"robots.txt"。位于子目录中的 robots.txt 文件无效，因为漫游器只在域名的根目录中查找此文件。例如，[http://www.example.com/robots.txt](http://www.example.com/robots.txt) 是有效位置，[http://www.example.com/mysite/robots.txt](http://www.example.com/mysite/robots.txt) 则不是。

这里举一个robots.txt的例子:

User-agent: *

Disallow: /cgi-bin/

Disallow: /tmp/

Disallow: /~name/

◆使用 robots.txt 文件拦截或删除整个网站  
要从搜索引擎中删除您的网站，并防止所有漫游器在以后抓取您的网站，请将以下 robots.txt 文件放入您服务器的根目录：

User-agent: *  
Disallow: /

要只从 Google 中删除您的网站，并只是防止 Googlebot 将来抓取您的网站，请将以下 robots.txt 文件放入您服务器的根目录：

User-agent: Googlebot  
Disallow: /

每个端口都应有自己的 robots.txt 文件。尤其是您通过 http 和 https 托管内容的时候，这些协议都需要有各自的 robots.txt 文件。例如，要让 Googlebot 只为所有的 http 网页而不为 https 网页编制索引，应使用下面的 robots.txt 文件。

对于 http 协议 ([http://yourserver.com/robots.txt](http://yourserver.com/robots.txt)):

User-agent: *  
Allow: /

对于 https 协议 ([https://yourserver.com/robots.txt](https://yourserver.com/robots.txt)):

User-agent: *  
Disallow: /

  
◆允许所有的漫游器访问您的网页  
User-agent: *  
Disallow:

(另一种方法: 建立一个空的 "/robots.txt" 文件, 或者不使用robot.txt。)

◆使用 robots.txt 文件拦截或删除网页

您可以使用 robots.txt 文件来阻止 Googlebot 抓取您网站上的网页。 例如，如果您正在手动创建 robots.txt 文件以阻止 Googlebot 抓取某一特定目录下（例如，private）的所有网页，可使用以下 robots.txt 条目：

User-agent: Googlebot  
Disallow: /private

要阻止 Googlebot 抓取特定文件类型（例如，.gif）的所有文件，可使用以下 robots.txt 条目：

User-agent: Googlebot  
Disallow: /*.gif$

要阻止 Googlebot 抓取所有包含 ? 的网址（具体地说，这种网址以您的域名开头，后接任意字符串，然后是问号，而后又是任意字符串），可使用以下条目：

User-agent: Googlebot  
Disallow: /*?

尽管我们不抓取被 robots.txt 拦截的网页内容或为其编制索引，但如果我们在网络上的其他网页中发现这些内容，我们仍然会抓取其网址并编制索引。因此，网页网址及其他公开的信息，例如指 向该网站的链接中的定位文字，有可能会出现在 Google 搜索结果中。不过，您网页上的内容不会被抓取、编制索引和显示。

  
◆robots.txt文件的格式  
User-agent:  
　　 该项的值用于描述搜索引擎robot的名字。在"robots.txt"文件中，如果有多条User-agent记录说明有多个robot会受到"robots.txt"的限制，对该文件来说，至少要有一条User-agent记录。如果该项的值设为*，则对任何robot均有效，在"robots.txt"文件中，"User-agent:*"这样的记录只能有一条。如果在"robots.txt"文件中，加入"User-agent:SomeBot"和若干Disallow、Allow行，那么名为"SomeBot"只受到"User-agent:SomeBot"后面的Disallow和Allow行的限制。  
Disallow:  
　　 该项的值用于描述不希望被访问的一组URL，这个值可以是一条完整的路径，也可以是路径的非空前缀，以Disallow项的值开头的URL不会被robot访问。例如"Disallow:/help"禁止robot访问/help.html、/helpabc.html、/help/index.html，而"Disallow:/help/"则允许robot访问/help.html、/helpabc.html，不能访问/help/index.html。"Disallow:"说明允许robot访问该网站的所有url，在"/robots.txt"文件中，至少要有一条Disallow记录。如果"/robots.txt"不存在或者为空文件，则对于所有的搜索引擎robot，该网站都是开放的。  
Allow:  
　　 该项的值用于描述希望被访问的一组URL，与Disallow项相似，这个值可以是一条完整的路径，也可以是路径的前缀，以Allow项的值开头的URL是允许robot访问的。例如"Allow:/hibaidu"允许robot访问/hibaidu.htm、/hibaiducom.html、/hibaidu/com.html。一个网站的所有URL默认是Allow的，所以Allow通常与Disallow搭配使用，实现允许访问一部分网页同时禁止访问其它所有URL的功能。  
需要特别注意的是Disallow与Allow行的顺序是有意义的，robot会根据第一个匹配成功的Allow或Disallow行确定是否访问某个URL。

使用"*"和"$":  
baiduspider支持使用通配符"*"和"$"来模糊匹配url。

　　 "$" 匹配行结束符。  
　　 "*" 匹配0或多个任意字符。

  
◆后记  
1\. Google爬虫名称

1） Googlebot：从Google的网站索引和新闻索引中抓取网页

2） Googlebot-Mobile针对Google的移动索引抓取网页

3） Googlebot-Image：针对Google的图片索引抓取网页

4） Mediapartners-Google：抓取网页确定 AdSense 的内容。只有在你的网站上展示 AdSense 广告的情况下，Google才会使用此漫游器来抓取您的网站。

5） Adsbot-Google：抓取网页来衡量 AdWords 目标网页的质量。只有在你使用 Google AdWords 为你的网站做广告的情况下，Google才会使用此漫游器。

2\. 百度（Baidu）爬虫名称：Baiduspider

3\. 雅虎（Yahoo）爬虫名称：Yahoo Slurp

4\. 有道（Yodao）蜘蛛名称：YodaoBot

5\. 搜狗（sogou）蜘蛛名称：sogou spider

6\. MSN的蜘蛛名称：Msnbot

humen1 Tech