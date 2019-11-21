---
title: PHP   Pack()函数
url: 302.html
id: 302
categories:
  - PHP专题
date: 2009-12-14 17:44:45
tags:
---

定义和用法 pack() 函数把数据装入一个二进制字符串。 语法 pack(format,args+) 参数 描述 format 必需。规定在包装数据时所使用的格式。 args+ 可选。规定被包装的一个或多个参数。 format 参数的可能值： * a - NUL-padded string * A - SPACE-padded string * h - Hex string, low nibble first * H - Hex string, high nibble first * c - signed char * C - unsigned char * s - signed short (always 16 bit, machine byte order) * S - unsigned short (always 16 bit, machine byte order) * n - unsigned short (always 16 bit, big endian byte order) * v - unsigned short (always 16 bit, little endian byte order) * i - signed integer (machine dependent size and byte order) * I - unsigned integer (machine dependent size and byte order) * l - signed long (always 32 bit, machine byte order) * L - unsigned long (always 32 bit, machine byte order) * N - unsigned long (always 32 bit, big endian byte order) * V - unsigned long (always 32 bit, little endian byte order) * f - float (machine dependent size and representation) * d - double (machine dependent size and representation) * x - NUL byte * X - Back up one byte * @ - NUL-fill to absolute position

输出：

PHP

输出：

PHP