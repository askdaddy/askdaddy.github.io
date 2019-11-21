---
title: iframe自适应高度和宽度
tags:
  - php
url: 117.html
id: 117
categories:
  - 'NULL'
date: 2008-02-18 16:30:00
---

iframe自适应高度和宽度,在页面标签内写入如下。

</p> <p>function SetWinHeight(obj)<br />{<br />var win=obj;<br />if (document.getElementById)<br />{<br />&nbsp;&nbsp;&nbsp; if (win && !window.opera)<br />&nbsp;&nbsp;&nbsp; {<br />&nbsp;&nbsp;&nbsp;&nbsp; if (win.contentDocument && win.contentDocument.body.offsetHeight) <br /> &nbsp;&nbsp;&nbsp;&nbsp; {<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; win.height = win.contentDocument.body.offsetHeight; <br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; win.width =win.contentDocument.body.offsetWidth;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br />&nbsp;&nbsp;&nbsp;&nbsp; else if(win.Document && win.Document.body.scrollHeight)<br />&nbsp;&nbsp;&nbsp;&nbsp; {<br /> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; win.height = win.Document.body.scrollHeight;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; win.width=win.Document.body.scrollWidth;<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; }<br />&nbsp;&nbsp;&nbsp; }<br />}<br />}</p> <p></p> <p>

然后在里面写入如下

  

humen1 Tech