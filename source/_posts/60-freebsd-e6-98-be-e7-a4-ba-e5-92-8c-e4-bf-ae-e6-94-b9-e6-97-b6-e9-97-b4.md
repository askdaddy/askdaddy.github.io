---
title: freebsd 显示和修改时间
url: 60.html
id: 60
categories:
  - 'NULL'
date: 2008-06-25 00:35:00
tags:
---

可以用date查看和修改本地时间

  
显示当前的时间：  
date  
Fri Oct 22 21:38:29 CST 2004

设置时间：  
date 0410222141  
时间格式为年、月、日、时、分，每个各占两个数字，其形式即为yymmddhhmm，大部分情况下是对时间进行小调整，可以略去前面的年月日部分，而仅使用四位数字表示时、分，形如hhmm

也可以通过Internet同步时间：  
ntpdate [nist1.symmetricom.com](http://nist1.symmetricom.com)

附:国际通用时间服务器地址列表：  
Name                IP Address          Location  
[time-a.nist.gov](http://time-a.nist.gov) [129.6.15.28](http://129.6.15.28) NIST, Gaithersburg, Maryland  
[time-b.nist.gov](http://time-b.nist.gov) [129.6.15.29](http://129.6.15.29) NIST, Gaithersburg, Maryland  
[time-a.timefreq.bldrdoc.gov](http://time-a.timefreq.bldrdoc.gov) [132.163.4.101](http://132.163.4.101) NIST, Boulder, Colorado  
[time-b.timefreq.bldrdoc.gov](http://time-b.timefreq.bldrdoc.gov) [132.163.4.102](http://132.163.4.102) NIST, Boulder, Colorado  
[time-c.timefreq.bldrdoc.gov](http://time-c.timefreq.bldrdoc.gov) [132.163.4.103](http://132.163.4.103) NIST, Boulder, Colorado  
[utcnist.colorado.edu](http://utcnist.colorado.edu) [128.138.140.44](http://128.138.140.44) University of Colorado, Boulder  
[time.nist.gov](http://time.nist.gov) [192.43.244.18](http://192.43.244.18) NCAR, Boulder, Colorado  
[time-nw.nist.gov](http://time-nw.nist.gov) [131.107.1.10](http://131.107.1.10) Microsoft, Redmond, Washington  
[nist1.symmetricom.com](http://nist1.symmetricom.com) [69.25.96.13](http://69.25.96.13) Symmetricom, San Jose, California  
[nist1-dc.glassey.com](http://nist1-dc.glassey.com) [216.200.93.8](http://216.200.93.8) Abovenet, Virginia  
[nist1-ny.glassey.com](http://nist1-ny.glassey.com) [208.184.49.9](http://208.184.49.9) Abovenet, New York City  
[nist1-sj.glassey.com](http://nist1-sj.glassey.com) [207.126.98.204](http://207.126.98.204) Abovenet, San Jose, California  
[nist1.aol-ca.truetime.com](http://nist1.aol-ca.truetime.com) [207.200.81.113](http://207.200.81.113) TrueTime, AOL facility, Sunnyvale, California  
[nist1.aol-va.truetime.com](http://nist1.aol-va.truetime.com) [64.236.96.53](http://64.236.96.53) TrueTime, AOL facility, Virginia

humen1 Tech