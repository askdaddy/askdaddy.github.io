---
title: Smokeping 发送告警邮件
tags:
  - 监控
url: 669.html
id: 669
categories:
  - coding那点事
date: 2013-11-27 14:06:35
---

smokeping 默认用sendmail发邮件，这样不好。 改了一下源码 这样可以使用 我QQ的smtp server来发告警邮件了 首先需要安装 Authen::SASL 模块（auth 需要用的） 我用CPAN装的，不细说了 修改 smokeping/lib/Smokeping.pm \[perl\] #头上加 use Authen::SASL; #定位到sendmail函数，改成下面这样 sub sendmail ($$$){ my $from = shift; my $to = shift; $to = $1 if $to =~ /<(.*?)>/; my $body = shift; if ($cfg->{General}{mailhost} and my $smtp = Net::SMTP->new(\[split /\\s*,\\s*/, $cfg->{General}{mailhost}\],Timeout=>5) ){ $smtp->auth(split(/\\s*,\\s*/, $cfg->{General}{mailusr}),split(/\\s*,\\s*/, $cfg->{General}{mailpwd})); $smtp->mail($from); $smtp->to(split(/\\s*,\\s*/, $to)); $smtp->data(); $smtp->datasend($body); $smtp->dataend(); $smtp->quit; } elsif ($cfg->{General}{sendmail} or -x "/usr/lib/sendmail"){ open (M, "|-") || exec (($cfg->{General}{sendmail} || "/usr/lib/sendmail"),"-f",$from,$to); print M $body; close M; } else { warn "ERROR: not sending mail to $to, as all methodes failed\\n"; } } #找到  '\_vars =>' ,把 mailusr mailpwd  加进去。不然不能启动哦！General configuration values valid for the whole SmokePing setup. DOC \_vars => \[ qw(owner imgcache imgurl datadir dyndir pagedir piddir sendmail offset smokemail cgiurl mailhost mailusr mailpwd snpphost contact display_name syslogfacility syslogpriority concurrentprobes changeprocessnames tmail changecgiprogramname linkstyle precreateperms ) \], \[/perl\] 然后修改配置文件 /etc/config \[perl\] mailhost = smtp.qq.com mailusr = noreply@qq.com mailpwd = xxxxxxxxx \[/perl\]