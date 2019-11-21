---
title: vhost 配置
tags:
  - unix
url: 152.html
id: 152
categories:
  - 'NULL'
date: 2007-11-01 09:51:00
---

#举例说明。  

#此例目的在于用不同的域名访问同一ip下的不同目录层次

#  
\# Virtual Hosts  
#  
\# If you want to maintain multiple domains/hostnames on your  
\# machine you can setup VirtualHost containers for them. Most configurations  
\# use only name-based virtual hosts so the server doesn't need to worry about  
\# IP addresses. This is indicated by the asterisks in the directives below.  
#  
\# Please see the documentation at  
\# <[URL:http://httpd.apache.org/docs/2.2/vhosts/](http://httpd.apache.org/docs/2.2/vhosts/) >  
\# for further details before you try to setup virtual hosts.  
#  
\# You may use the command line option '-S' to verify your virtual host  
\# configuration.

#  
\# Use name-based virtual hosting.  
#  
NameVirtualHost *:80

#  
\# VirtualHost example:  
\# Almost any Apache directive may go into a VirtualHost container.  
\# The first VirtualHost section is used for all requests that do not  
\# match a ServerName or ServerAlias in any block.  
#  
  
    ServerAdmin [webmaster@dummy-host.localhost](mailto:webmaster@dummy-host.localhost)  
#文件目录

    DocumentRoot c:/wamp/www

#服务名-我理解为主域名  
    ServerName [seven.com](http://seven.com)  
#别名-这里是关键了在这里设定子域名

    ServerAlias [www.seven.com](http://www.seven.com/)  
    ErrorLog logs/dummy-host.localhost-error_log  
    CustomLog logs/dummy-host.localhost-access_log common  

  
    ServerAdmin [webmaster@dummy-host.localhost](mailto:webmaster@dummy-host.localhost)  
    DocumentRoot c:/wamp/www/sns/public_html  
    ServerName [seven.com](http://seven.com)  
    ServerAlias [sns.seven.com](http://sns.seven.com)  
    ErrorLog logs/dummy-host.localhost-error_log  
    CustomLog logs/dummy-host.localhost-access_log common  

 #以上配置使 [www.seven.com](http://www.seven.com)访问www下文件  sns.seven.com访问 www/sns/public_html下文件 

  

humen1 Tech