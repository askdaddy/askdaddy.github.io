---
title: 函数sprintf()
tags:
  - php
url: 143.html
id: 143
categories:
  - 'NULL'
date: 2007-11-17 13:20:00
---

sprintf  
将字符串格式化。  
语法: string sprintf(string format, mixed \[args\]...);  
返回值: 字符串  
函数种类: 资料处理  
内容说明  
本函数用来将字符串格式化。参数 format 是转换的格式，以百分比符号 % 开始到转换字符为止。而在转换的格式间依序包括了  
填空字符。0 的话表示空格填 0；空格是默认值，表示空格就放着。  
对齐方式。默认值为向右对齐，负号表向左对齐。  
字段宽度。为最小宽度。  
精确度。指在小数点后的浮点数位数。  
类型，见下表  
% 印出百分比符号，不转换。  
b 整数转成二进位。  
c 整数转成对应的 ASCII 字符。  
d 整数转成十进位。  
f 倍精确度数字转成浮点数。  
o 整数转成八进位。  
s 整数转成字符串。  
x 整数转成小写十六进位。  
X 整数转成大写十六进位。  
使用范例  
$money1 = 68.75;  
$money2 = 54.35;  
$money = $money1 + $money2;// 此时变量 $money 值为 "123.1";  
$formatted = sprintf ("%01.2f", $money);// 此时变量 $ formatted 值为 "123.10"  
?>

humen1 Tech