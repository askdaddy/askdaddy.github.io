---
title: elasticsearch_river 配置
tags:
  - elasticsearch
  - log
  - logstash
url: 813.html
id: 813
categories:
  - linux server
date: 2014-08-12 11:44:18
---

1\. install es-river plugin /usr/share/elasticsearch/bin/plugin -install elasticsearch/elasticsearch-river-rabbitmq/2.0.0 2. install rabbitmq 2.1 add epel repo rpm --import https://fedoraproject.org/static/0608B895.txt wget http://mirrors.yun-idc.com/epel/6/i386/epel-release-6-8.noarch.rpm rpm -i epel-release-6-8.noarch.rpm 2.2 install erlang yum -y install erlang 2.3 install rabbitmq wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.3.4/rabbitmq-server-3.3.4-1.noarch.rpm rpm --import http://www.rabbitmq.com/rabbitmq-signing-key-public.asc yum -y install rabbitmq-server-3.3.4-1.noarch.rpm 2.4 start rabbitmq /etc/init.d/rabbitmq-server start 3 logstash conf ... output{ elasticsearch\_river { es\_host => "localhost" index => "rt-%{+dd.HH.mm.ss}" rabbitmq_host => "localhost" workers => 8 } } ... 4. restart elasticsearch 5. restart logstash