---
title: lvs-tun 配置memo
tags:
  - lvs
url: 685.html
id: 685
categories:
  - linux server
date: 2013-12-24 13:16:53
---

director:192.168.8.220, vip:192.168.8.224 realserver:192.168.8.221 director.sh \[bash\] #!/bin/sh VIP=192.168.8.224 RIP=192.168.8.221 modprobe ip\_vs modprobe ipip /etc/init.d/iptables stop ifconfig eth0:0 down ifconfig eth0:0 $VIP broadcast $VIP netmask 255.255.255.255 up route add -host $VIP dev eth0:0 ipvsadm -A -t $VIP:80 -s rr ipvsadm -a -t $VIP:80 -r $RIP -i ipvsadm \[/bash\] realserver.sh \[bash\] #!/bin/sh VIP=192.168.8.224 RIP=192.168.8.221 modprobe ipip /etc/init.d/iptables stop ifconfig tunl0 down ifconfig tunl0 $VIP broadcast $VIP netmask 255.255.255.255 up route add -host $VIP dev tunl0 echo 0 > /proc/sys/net/ipv4/conf/tunl0/rp\_filter echo 0 > /proc/sys/net/ipv4/conf/all/rp\_filter arptables -A IN -j DROP -d $VIP arptables -A OUT -j DROP -d $VIP /etc/init.d/arptables\_jf save \[/bash\]