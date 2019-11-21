---
title: AIMD
tags:
  - TCP
url: 652.html
id: 652
categories:
  - network
date: 2013-09-11 14:54:28
---

Additive Increase Multiplicative Decrease: 当TCP发送方感受到端到端路径无拥塞时就线性的增加其发送速度，当察觉到路径拥塞时就乘性减小其发送速度。 TCP拥塞控制协议的线性增长阶段被称为避免拥塞。 当TCP发送端收到ACK，并且没有检测到丢包事件时，拥塞窗口加1；当TCP发送端检测到丢包事件后，拥塞窗口除以2。 \[cpp\] While(Sending\_Not\_Finish){ if(Not\_Loss\_Packet){ CongWin++; }else CongWin=\[CongWin/2\]; //\[\]的意思是取整 } \[/cpp\]