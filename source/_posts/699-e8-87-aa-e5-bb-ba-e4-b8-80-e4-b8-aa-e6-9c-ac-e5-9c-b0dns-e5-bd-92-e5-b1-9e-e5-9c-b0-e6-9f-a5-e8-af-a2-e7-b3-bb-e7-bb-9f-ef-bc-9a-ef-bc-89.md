---
title: 自建一个本地dns归属地查询系统：）
url: 699.html
id: 699
categories:
  - CDN
date: 2014-01-06 20:49:58
tags:
---

1.首先要搞个dns 服务器，自己用bind架一个就好，2个关键性配置文件如下 /opt/bind/etc/named.conf \[text\] options { listen-on port 53 { localhost; }; allow-query { any; }; directory "/opt/bind/var"; recursion yes; allow-transfer { none; }; }; logging { channel default\_debug { file "/opt/bind/var/named.run"; severity dynamic; }; channel query\_log { file "/opt/bind/var/query.log"; severity debug; print-time yes; print-category yes; }; category queries{ query\_log; }; }; zone "." IN { type master; file "anyhosts"; }; key "rndc-key" { algorithm hmac-md5; secret "tLUFCQE/OZkFMPo2NMERMA=="; }; controls { inet 127.0.0.1 port 953 allow { 127.0.0.1; } keys { "rndc-key"; }; }; \[/text\] /opt/bind/var/anyhosts \[text\] $TTL 60 $ORIGIN . @ IN SOA ns1. root.localhost. ( 20051213; 7000; 3000; 15000; 86400; ); @ 86400 IN NS ns1 ns1 86400 IN A 127.0.0.1 * IN A xxx.xxx.xxx.xxx \[/text\] 注意：xxx.xxx.xxx.xxx是这台ns服务器的外网ip 2. 需要一个顶级域名，这里用我自己的域名代替，我的域名为 humen1.net. 去域名提供商那里解析以下域名 记录名--------记录类型--------记录值 ldns ---------NS --------ns1.humen1.net. ns1 ---------A --------xxx.xxx.xxx.xxx 3. 配置apache vhosts 配置如下 \[bash\] <VirtualHost *:80> ServerName *.ldns.humen1.net DocumentRoot /ldns DirectoryIndex index.php index.html index.htm </VirtualHost> \[/bash\] 4. 写一个php脚本在 /ldns 目录下 index.php \[php\] <?php $str=array(); exec("tail -n 50 /opt/bind/var/query.log",$str); $str=implode("\\n\\n",$str); $host= $\_SERVER\['HTTP\_HOST'\]; $pattern='/(client\\s(?P<ip>\\d*\\.\\d*\\.\\d*\\.\\d*)#\\d*\\s\\('.$host.'\\):)/'; $jsonp=$\_GET\["jsonpcallback"\]; if (preg\_match($pattern,$str,$ma)) { echo $jsonp.'({"error":"0","ip":"'.$ma\['ip'\].'"})'; print $ips=file\_get_contents("http://ip.taobao.com/service/getIpInfo.php?ip=".$ma\['ip'\]); }else{ echo $jsonp. '({"error":"1")}'; } ?> \[/php\] 5. 使用 curl http://xxxyyyzzz.ldns.humen1.net 注意 xxxyyyzzz是随机数保证不要重复哦~~