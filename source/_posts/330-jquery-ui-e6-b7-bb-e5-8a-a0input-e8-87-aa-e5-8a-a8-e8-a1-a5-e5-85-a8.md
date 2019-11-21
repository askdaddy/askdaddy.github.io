---
title: jquery ui - 添加input & 自动补全
url: 330.html
id: 330
categories:
  - AJAX
date: 2010-04-18 16:31:51
tags:
---

`var availableTags = ["上海","北京","c++", "java", "php", "coldfusion", "javascript", "asp", "ruby", "python", "c", "scala", "groovy", "haskell", "perl"]; $(function() { $("input#add").click(function(){ addSpot(this); }); });function addSpot(obj) { $('div.ui-widget').append('<input type="text" class="ii" value="'+$('input.ii').size()+'" />'); $("input.ii").autocomplete({ source: availableTags });};

`