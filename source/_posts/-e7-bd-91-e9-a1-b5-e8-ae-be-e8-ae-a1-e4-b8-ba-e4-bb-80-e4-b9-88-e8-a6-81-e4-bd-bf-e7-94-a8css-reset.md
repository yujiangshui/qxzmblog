title: 网页设计为什么要使用 CSS reset
tags:
  - CSS
id: 610
categories:
  - 前端相关
date: 2012-02-15 15:27:03
---

## 先来简单的介绍一些 css reset

从字面意思中，我们可以看出，css reset的功能就是把网页标签样式使用 css 重置。学过 html 的朋友都知道，html 标签是有它默认的样式的，例如：&lt;h*&gt;标签表示标题，通常会对文字进行加粗，并且会让文字变大；&lt;p&gt;是段落标签，表示一个段落，通常会与其他文字空开一段距离。

那我们为什么要把网页的标签样式进行重置呢？原因很简单，[内核不同的浏览器，它对于网页标签的解析是不同的。](http://www.qianxingzhem.com/post-612.html)举个不恰当的例子，某浏览器对于&lt;h1&gt;标签，可能会对文字进行加粗，并且调整文字大小为24px，之后在屏幕中输出。但是另一个浏览器，可能不会这样解析，它可能不会对文字进行加粗，文字大小也可能是20px。这样，同一个网页，在不同浏览器的浏览下，就会发生较大的区别，可能在某浏览器中是正常的，在另一个浏览器中，就错位了不正常了。潜行者m之前写过比较一篇关于几个主流浏览器的区别，有兴趣的可以看一下  [firefox、chrome、opera和IE 7的区别](http://www.qianxingzhem.com/post-612.html) 。

但是，所有的主流浏览器，对于css的支持都是不错的，所以我们可以使用css reset来解决上面的问题。我们使用css来控制页面标签的样式，比如把&lt;h*&gt;标题的加粗、扩大、边距等样式清除，让它和普通文字一样；把&lt;ul&gt;等列表标签的前面标志、空格等清除。这样，把所有的标签样式清除了，当我们需要某一种样式的时候，只需要在css文件中，对其进行控制即可。这样的好处就是，能够尽量的消除各个浏览器对于页面标签样式的解析，尽量使网页在各个浏览器中显示效果一样。

## 那么css reset如何编写

目前在网络上，已经有很多关于css reset的框架，例如雅虎的 YUI 等，我们可以下载下来看看他们是怎么写的，是怎么处理的。同时也可以直接在网页中引用。但是对于小的页面，潜行者m并不推荐这种做法，那些大的框架，适合大型网站使用，里面几乎对所有的html标签进行了css reset，而我们制作的小页面，并不需要太多的标签，如果使用那么多无用的css reset代码，会导致页面体积变大。所以我推荐的做法是，根据自己页面用到的标签，去寻找相应的css reset代码。下面，是我从《编写高质量代码—web前端开发修炼之道》一书中，提取出来的一段css reset代码，大家可以根据自己的需要，选择引用：
<pre id="line1">/*CSS reset*/
html{color:#000;background:#fff;}
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre,code,
form,fieldset,legend,input,button,textarea,p,blockquote,
th,td{margin:0;padding:0;}table{border-collapse:collapse;
border-spacing:0;}fieldset,img{border:0;}address,caption,
cite,code,dfn,em,strong,th,var,optgroup{font-style:inherit;
font-weight:inherit;}del,ins{text-decoration:none;}
li{list-style:none;}caption,th{text-align:left;}h1,h2,
h3,h4,h5,h6{font-size:100%;font-weight:normal;}q:before,
q:after{content:'';}abbr,acronym{border:0;font-variant:normal;}
sup{vertical-align:baseline;}sub{vertical-align:baseline;}
legend{color:#000;}input,button,textarea,select,optgroup,
option{font-family:inherit;font-size:inherit;font-style:inherit;font-weight:inherit;}
input,button,textarea,select{*font-size:100%;}input,button,select,
textarea{outline:none;}a {outline: 0;}</pre>
上面就是一段还不错的css reset代码，在文章的后面，我补充了一些css reset资源。

## 关于*{margin:0;padding:0}

*{margin:0;padding:0}这就是一段非常简洁的css reset代码，有一些人仅仅使用这一句代码，表示将所有标签的内边距和外边距清除，达到css reset的效果。但是潜行者m不推荐使用。原因很简单，这一行代码不能算作是css reset代码，它仅仅清除了标签的内边距和外边距而已，而我们要的css reset效果，是要把ol和ul的列表样式、th的加粗、h标签的变大加粗等样式都清除，全部重置。之后，根据自己的设计需要来进行css的控制。而这句*{margin:0;padding:0}，没有把所有的样式清除。

PS：补充一个资源 [10款浏览器CSS Reset的方法](http://sofish.de/736 "Permanent Links to 10款浏览器CSS Reset的方法")