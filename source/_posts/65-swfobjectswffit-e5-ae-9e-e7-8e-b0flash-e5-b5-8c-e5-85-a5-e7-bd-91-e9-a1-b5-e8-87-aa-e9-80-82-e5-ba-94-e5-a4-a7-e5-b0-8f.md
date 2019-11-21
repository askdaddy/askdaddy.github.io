---
title: swfobject+swffit实现flash嵌入网页自适应大小
url: 65.html
id: 65
categories:
  - 'NULL'
date: 2008-06-04 11:56:00
tags:
---

  

swfobject [http://code.google.com/p/swfobject/](http://code.google.com/p/swfobject/)  
swffit [http://swffit.millermedeiros.com/comments.php](http://swffit.millermedeiros.com/comments.php)

  
简介：  
swfobject 是一个轻量级的第三方flash网页嵌入js脚本，它吸引我的一些特性有，插入代码简洁，flash免激活，后台更新flash player 和版本侦测。

swffit 可以实现flash自适应大小

  
  
    
  <br /> &nbsp;&nbsp;&nbsp;swfobject.embedSWF(&quot;example.swf&quot;, &quot;my\_flash&quot;, &quot;550&quot;, &quot;400&quot;, &quot;8.0.0&quot;);<br />&nbsp;&nbsp;&nbsp;swffit(&quot;my\_flash&quot;,550,400);<br />&nbsp;&nbsp;

Loading... 

  
注意了swffit（）还有2个隐藏参数  
swffit("my_flash",550,400,1000,800);  
第一个参数是填充flash的层id  
第二、三个参数是最小尺寸  
第四、五个参数是最大尺寸  
 

humen1 Tech