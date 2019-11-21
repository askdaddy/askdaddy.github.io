---
title: elasticsearch+logstash+kibana 初探
tags:
  - bigdata
  - elasticsearch
  - kibana
  - logstash
url: 794.html
id: 794
categories:
  - linux server
date: 2014-05-25 10:07:50
---

花了一点时间搭了个初步的测试环境，分析的apache日志。 鉴于网络上的资料都比较过时了，所以在这里log一下。 
测试环境 centos6.3 64bit 
## 安装： 
- elasticsearch [[goto](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/setup-repositories.html#_yum)] 
```
# Download and install the Public Signing Key 
rpm --import http://packages.elasticsearch.org/GPG-KEY-elasticsearch 
# Add the following in your /etc/yum.repos.d/elasticsearch.repo \[elasticsearch-1.1\] 
name=Elasticsearch repository for 1.1.x packages baseurl=http://packages.elasticsearch.org/elasticsearch/1.1/centos gpgcheck=1 gpgkey=http://packages.elasticsearch.org/GPG-KEY-elasticsearch enabled=1 
# Install 
yum install elasticsearch 
```

- logstash [[goto](http://logstash.net/docs/1.4.1/repositories)] 
```
# Add the key 
rpm --import http://packages.elasticsearch.org/GPG-KEY-elasticsearch 
# Add the following in your /etc/yum.repos.d/logstash.repo 
[logstash-1.4] 
name=logstash repository for 1.4.x packages 
baseurl=http://packages.elasticsearch.org/logstash/1.4/centos gpgcheck=1 
gpgkey=http://packages.elasticsearch.org/GPG-KEY-elasticsearch enabled=1 

# Install logstash with: 
yum install logstash 

```

- kibana [[download](https://download.elasticsearch.org/kibana/kibana/kibana-3.1.0.tar.gz)] 

这个不用安装，解压然后放在httpd服务的目录里可以直接用是个纯html5应用（就是个网站），而且装在本机不需要配置，如果elasticsearch不在本机请编辑目录下的config.js指定url 
/********************************************************/
 配置： elasticsearch 不需要配置，直接run起 ` /etc/init.d/elasticsearch start ` P.S. 这个软件很奇葩，默认装的路径在 /usr/share 下。 logstash 配置文件默认是没有的，配置目录在 /etc/logstash/conf.d/ 比如我在此目录下创建了一个配置文件 
 
```
  # /etc/logstash/conf.d/seven.conf input 
  { file { path => "/var/log/httpd/access\_json.log" type => "apache" # This format tells logstash to expect 'logstash' json events from the file. format => json\_event } } output { elasticsearch { host => "127.0.0.1" }
```
  
  
解释一下，input 这里设置的apache日志格式是个json格式，这就意味着apache的日志要进行改造，这个方式比用redis，grok等方案更简单，apache的配置见后文。 重点注意：
  
```
# /etc/init.d/logstash 
... 
name=logstash pidfile="/var/run/$name.pid" 
# 请把原来用户和用户组logstash改成root，不然没有权限读apache日志 
LS_USER=root 
LS_GROUP=root 
LS_HOME=/var/lib/logstash 
LS_HEAP_SIZE="500m" 
...
```
kibana 这个也不用配置，直接可以跑 

- apache [[goto](http://cookbook.logstash.net/recipes/apache-json-logs/)] 

```
# Create a log format called 'logstash\_json' that emits, in json, the parts of an http 
# request I care about. For more details on the features of the 'LogFormat' 
# directive, see the apache docs: 
# http://httpd.apache.org/docs/2.2/mod/mod\_log\_config.html#formats 
LogFormat "{ \"@timestamp\": \"%{%Y-%m-%dT%H:%M:%S%z}t\", \"@fields\": { \"client\": \"%a\", \"duration_usec\": %D, \"status\": %s, \"request\": \"%U%q\", \"method\": \"%m\", \"referrer\": \"%{Referer}i\" } }" logstash_json 

LogFormat "{ \"@timestamp\": \"%{%Y-%m-%dT%H:%M:%S%z}t\", \"@message\": \"%r\", \"@fields\": { \"user-agent\": \"%{User-agent}i\", \"client\": \"%a\", \"duration_usec\": %D, \"duration_sec\": %T, \"status\": %s, \"request_path\": \"%U\", \"request\": \"%U%q\", \"method\": \"%m\", \"referrer\": \"%{Referer}i\" } }" logstash_ext_json 

# Write our 'logstash_json' logs to logs/access_json.log CustomLog logs/access_json.log logstash_ext_json 
```

提供的cookbook[[goto](http://cookbook.logstash.net/recipes/apache-json-logs/)]里还有让apache同时支持传统raw data和json日志的方法，我没试过。 [![kibana](/uploads/2014/05/5o-9x-leglkghciouwop-300x140.jpg)](/uploads/2014/05/5o-9x-leglkghciouwop.jpg)