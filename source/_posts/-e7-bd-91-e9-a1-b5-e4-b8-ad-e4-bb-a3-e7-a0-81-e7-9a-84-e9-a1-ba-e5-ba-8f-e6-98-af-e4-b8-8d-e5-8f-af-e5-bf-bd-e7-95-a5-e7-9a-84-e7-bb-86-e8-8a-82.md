title: 网页中代码的顺序是不可忽略的细节
tags:
  - CSS
  - jQuery
id: 1539
categories:
  - 前端相关
date: 2012-11-14 21:40:48
---

仿佛奇怪的问题总是喜欢找上那些初学者。当我在学习制作网页的时候，经常遇到一些很特别的问题。例如：刚刚添加的样式不起作用、jQuery的代码老是不起作用等等。这往往是不关注细节导致的。而今天我要谈的这个细节，就是关于网页中代码的顺序。没错，代码也是有顺序的，顺序不对有可能会出现一些意外的情况。

## HTML 相关的代码顺序

下面先来介绍 HTML 中的代码顺序。

### HTML 代码的排序原理

排序原理很简单，因为当浏览器访问一个网页的时候，要下载这个网页。现在的网速，对于一个几百K的网页来说，很快就能下载完。但是如果网页比较大或者网速比较卡，网页下载就会需要一定的时间。这样的话，浏览器显示网页的过程就很明显了。从 HTML 代码的上到下，依次下载。**重要的内容要优先加载**，所以就产生了 HTML 代码排序的问题。

### head 里面的元素排序

HTML 中的 head 元素里面，通常放置着文档的描述信息。一般有：网页编码、title标题、meta 描述网页关键字、link 引入 CSS 文件、script 引入 Javascript 文件等等。下面就这几个内容进行一个讨论（以 HTML5 为例）：

首先，先是标准的 DOCTYPE 声明、HTML 结构那一套。
<pre>&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;&lt;/head&gt;
&lt;body&gt;&lt;/body&gt;
&lt;/html&gt;</pre>
其次，编写网页编码，我个人认为编码是网页中最重要的，因为它决定浏览器采用什么编码来解析你的网页，如果编码没有设置好的话，网页显示出来就是一整个乱码。关于网页编码的更详细的文章，可以看一下 [潜行者m](http://www.qianxingzhem.com) 写的 [网页编码就是那点事](http://www.qianxingzhem.com/post-1499.html) 。编码写完之后，应该让浏览器立刻显示出网页的标题，这时候就应该写出 title 标题了。
<pre>&lt;meta charset="utf-8" /&gt;
&lt;title&gt;标题&lt;/title&gt;</pre>
接下来，就应该是声明文档的各种信息，例如 关键词、描述、作者等等信息。之后就要加载 CSS 样式表。让浏览器先下载好 CSS 样式表，之后下载的网页内容，就会立刻加上 CSS 的样式效果，谁也不希望打开网页的时候，是没有样式的，然后加载完内容之后才出现正常的页面。这也就是为什么 CSS 引用要写在 head 里面。
<pre id="line1">&lt;meta name="<a>keywords</a>" content="<a>潜行者m,网站建设,前端设计,Web开发</a>" /&gt;
&lt;meta name="<a>description</a>" content="<a>潜行者m 博客，是由 潜行者m 个人设计制作，完全原创写作，关注网站建设/前端设计/Web开发相关的独立博客。欢迎各位观看学习，并且与本人交流！！</a>" /&gt;

&lt;link rel="<a>stylesheet</a>" type="<a>text/css</a>" media="<a>screen</a>" href="http://www.qianxingzhem.com/wp-content/themes/qetro/style.css"/&gt;</pre>
关于 JavaScript 的位置一直比较有争议。因为 JavaScript 比较灵活，可以添加在页面的任何位置。通常推荐的是加在页面的最底部。因为JavaScript 文件通常比较大，浏览器下载比较费时间，由于 JavaScript 可能会影响到当前页面的结构内容，所以浏览器通常会先下载完JavaScript 代码，“运行” 之后，再下载网页的正文内容。这就导致了加载速度比较慢，因为要先加载  JavaScript 代码才会显示网页内容。所以要放在页面底部。这样浏览器会先下载网页的内容显示出来，然后再下载 JavaScript 对当前的网页进行处理。

### body 主体内容的排序

前面说过浏览器先依次下载网页然后显示，那么网页主体内容的排版布局就很明显了：**重要的内容排在前面**。

例如一个博客类型的网页，最重要的内容肯定是 文章 。所以文章的内容要尽量放在网页的顶部。虽然它可能要显示在下面，但是也要放在代码的上面，然后通过 CSS 布局等放在下面。当网速很卡的时候，排版合理的博客很明显就可以看到，先显示出来头部、文章主体内容，之后再显示 边栏、底部 内容。这就是为了让用户最快的看到他们想要看的内容，即使网速很卡下载很慢，内容出来了边栏等都下载不下来，用户也会得到他需要的内容。这就是 body 元素里面的代码排序原则。

## CSS 代码的排序

CSS中有很多排序的小细节需要注意，不注意的话很有可能就出现一些意外情况。

### 顺序解决样式冲突问题

当你对一个元素赋予了 background-color 属性，你在其他地方，忘了之前的设置，又对这个元素赋予了一个属性值与之前不同的 background-color 属性。那么浏览器究竟会对这个元素渲染哪一个背景颜色呢？答案是代码排在后面的属性值。冲突的内容，后面的属性值就会覆盖前面的属性值。因此要注意，一些 [CSS reset](http://www.qianxingzhem.com/post-610.html) 等要先加载，然后在后面加载自己写的属性值。例如：CSS reset 通常会取消 strong 的加粗，但有时我们的网页作品中，要 strong 显示成加粗效果，所以我们要设置 strong{font-weight：bold；} 这样的样式。但如果 CSS reset 代码放在后面，它之前对 strong 的取消加粗属性就会覆盖掉你的 加粗效果。所以无论刷新网页多少遍，你的 strong 标签里面的内容，还没有加粗。

如果有时候，你真的无法修改加载文件的顺序，那么面对这种情况，你可以使用 CSS 中的 ！important 语法，告诉浏览器要使用这个属性解决冲突。

### 链接的交互排序

一个超链接，默认是蓝色的，当我们把鼠标移动上去，会变色，点击的过程也会变色，访问过后回来一看，通常也不会是原来的蓝色了。控制这些颜色的，分别是 CSS 中的 ：link 、：visited 、：hover、：active 这四个伪类选择器，从名称就可以看出，控制的状态分别是：默认显示、访问过后、鼠标移动上去、点击激活。有时候会出现一些意外情况，例如：同时设置了 ：visited 和 ：hover 的样式，但一旦超链接访问后，hover 的样式就不出现了等。这是因为，这四个伪类选择器对 a 元素定义的时候，是有一个顺序的。如果不按照这个顺序，就会出现一些意外情况。

这个顺序有一个很好记的方法，那就是：love hate，即 l（link）ov（visited）e  h（hover ）a（active）te。
<pre>a:link{color:#666666; text-decoration:none;}
a:visited{color:#666666; text-decoration:none;}
a:hover{color:#666666; text-decoration:underline;}
a:active{color:#666666; text-decoration:none;}</pre>

### 属性值的顺序

CSS 中，有的属性既可以分开写，也可以合并起来写。例如 margin 属性，你可以分别制定 margin-left 、margin-right、margin-top、margin-bottom 的值，也可以直接写成 margin：top right bottom left； 也可以写两个参数，分别代表上下和左右的外边距。这样的写法简练而且灵活，但是对不熟练的新手来说，比较容易搞混。当类似 margin 、 padding 这样的属性，写四个参数的时候，以 top 开始，顺时针旋转。

除此之外，还有类似 font、background 这样的属性，它的属性值也要有顺序（虽然对顺序要求不严格），它们的参数有缺省值，所以不需要全部定义，只需要定义自己需要的样式即可。但是 border 这样的属性，就必须严格的按照语法编写属性值的顺序。例如：border ：1px solid #ccc；如果 1px solid #ccc 这三个值的顺序出问题了，那么浏览器就可能无法解读这段 CSS 的样式。

## JavaScript 代码的顺序

### JavaScript 文件加载顺序

jQuery 是一个比较常用的 JavaScript 库，通常我们还要配合它强大的插件使用。对于新手来说，经常会遇到没有产生相应效果的问题。就是说，代码没有检查出问题，但就是没有执行显示应有的效果。原因就出在加载顺序上面。你编写的 JavaScript 代码以及调用的 jQuery 插件，都需要基于 jQuery 库，所以应该在所有 JavaScript 代码之前，先引入 jQuery 库。浏览器先把库下载完了，才会识别后面的依赖这个库的代码实现相应的功能。同样的，激活使用某个插件的代码，也需要放在插件的后面才会有效。
<pre id="line1">&lt;script type="<a>text/javascript</a>" src="http://lib.sinaapp.com/js/jquery/1.7.2/jquery.min.js"&gt;&lt;/script&gt;
&lt;script type="<a>text/javascript</a>" src="jquery/jquery.lazyload.js"&gt;&lt;/script&gt;
&lt;script type="<a>text/javascript</a>" src="jquery/插件.js"&gt;&lt;/script&gt;
&lt;script type="<a>text/javascript</a>" src="自己编写的js/js.js"&gt;&lt;/script&gt;</pre>