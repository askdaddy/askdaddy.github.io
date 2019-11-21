---
title: XHTML 和 DOCTYPE 切换
url: 455.html
id: 455
categories:
  - 技术杂文
date: 2012-06-21 09:55:22
tags:
---

为 Web页指定 DOCTYPE 会影响浏览器呈现页的方式。Internet Explorer、Mozilla Firefox 和 Opera 全都支持一种名为“DOCTYPE 切换”（也叫“DOCTYPE 嗅探”）的功能。

引入 DOCTYPE 切换的目的是使浏览器能够正确地呈现符合标准的 Web 站点以及旧式 Web 站点。大多数 Web 站点被开发为呈现 HTML 页而不是 XHTML 页。浏览器通过判断是否存在 DOCTYPE 来确定何时应该使用标准来呈现页。

Internet Explorer 6+ 支持两种呈现模式，分别叫做 Quirks 模式和 Standards 模式。当 Internet Explorer 呈现包含有效 XHTML（或 HTML 4.0）DOCTYPE 的页时，它会以 Standards 模式呈现该页；否则，它会以 Quirks模式呈现该页

Opera 浏览器 (Opera 7+) 支持与 Internet Explorer 相同的两种呈现模式：Quirks 和 Standards

Mozilla Firefox 1+ 支持三种呈现模式：Quirks 模式、Almost Standards 模式和 Standards 模式。Firefox 的 Almost Standards 模式对应于 Internet Explorer 和 Opera 的 Standards 模式。当页包含有效的 XHTML 1.0 Transitional DOCTYPE（并且该页被分配为 text/html MIME 类型）时，Firefox 会以 Almost Standards 模式呈现该页。当页包含 XHTML 1.0 Strict 或 XHTML 1.1 DOCTYPE（或者该页被分配为 XML MIME 类型）时，该页将以 Standards 模式呈现

可以通过临时向页中添加以下客户端脚本（该脚本在最新版本的 Internet Explorer、Firefox 和 Opera 中有效）确定浏览器的当前呈现模式。

alert( document.compatMode );

您需要关心浏览器的呈现模式，因为它会影响将层叠样式表应用于该页的方式。如果将现有 HTML 页转换为 XHTML 页，那么在浏览器中打开它们时，它们可能看起来非常不同。

例如，Internet Explorer 以不同方式计算页元素的大小，这取决于呈现模式（它使用不同的 CSS Box Model）。在 Quirks 模式下，元素的宽度是通过将元素的内容、内边距、边框和边距相加而计算得到的。在 Standards 模式下，元素的宽度是只考虑元素内容的宽度而计算得到的。