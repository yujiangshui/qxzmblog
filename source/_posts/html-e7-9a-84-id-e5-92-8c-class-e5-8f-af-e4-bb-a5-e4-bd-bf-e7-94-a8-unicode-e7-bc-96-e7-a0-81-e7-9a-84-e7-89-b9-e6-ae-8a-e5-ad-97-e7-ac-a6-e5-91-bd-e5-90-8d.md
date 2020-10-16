title: HTML 的 id 和 class 可以使用 Unicode 编码的特殊字符命名
id: 1927
categories:
  - HTML
  - 前端相关
date: 2013-05-02 02:00:05
tags:
---

先简单的普及一下 Unicode 编码的基础知识，关于网页中的编码，详情请看 [潜行者m](http://www.qianxingzhem.com) 的文章：[网页编码就是那点事](http://www.qianxingzhem.com/post-1499.html)。好了普及完毕，开始正文内容。

HTML 结构中的 id 和 class 属性，最重要的目的就是作为结构的标识，可以被 CSS 选择器和 JS 选择器获取，增加样式和行为。由于结构通常比较复杂，id、class 的命名就成了一个大问题。于是出现了很多种命名方案，什么驼峰命名法等等。此外还有很多团队规范，规定命名规则等等。

但是这些命名，通常都逃不过：数字、字母、下划线、横杠。虽然这些比较直观，但是会不会太枯燥？其实 HTML、CSS、JS 支持的命名字符，远不止这点，你可以使用 Unicode 编码的特殊字符来让你的命名变得丰富多彩。

Unicode 由于有很多存储空间，所以拿出了很多 Unicode 编码代表一些比较常用的“字符图像”。比较常见的是 copyright 的图标：©，这就是一个 Unicode 编码存储的图标。其他的各种字符：Ϭ、ϻ、Ѽ 等，都是 Unicode 编码的字符。而 HTML、CSS、JS 支持使用它们来做命名。所有的 Unicode 字符列表，请看这里：[http://en.wikipedia.org/wiki/List_of_Unicode_characters](http://en.wikipedia.org/wiki/List_of_Unicode_characters)

在使用之前，请先确保你理解 Unicode 等这些编码，你必须让你的文件保存成 UTF-8 等格式才能使用，否则可能会显示成乱码。

然后我做了一个 [Demo ](http://www.qianxingzhem.com/demo/1927/)来做测试，Demo 中就使用特殊字符来命名，你可以在不同的测试环境浏览器进行测试，可以反馈一下看下有没有平台不支持。具体的代码不再贴出，请看 Demo 页面中代码。Demo 地址：[http://www.qianxingzhem.com/demo/1927/](http://www.qianxingzhem.com/demo/1927/)

应用的话，以后代码就丰富多彩了哈哈。