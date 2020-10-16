title: article 元素与 section 元素区别详解
tags:
  - HTML5
id: 915
categories:
  - 前端相关
date: 2012-03-26 08:16:51
---

**article 元素**与**section 元**素是 html5 中新增的两种元素，它们的功能与 div 是一样的，都是用来区分不同区域，它们的使用方法也相似，因此有很多朋友会将其混用。**html 5 中之所以新增这两种元素，就是为了更好的描述文档的内容，所以它们之间肯定是有区别的。**

## article 元素

**article 元素代表文档、页面或者应用程序中独立完整的可以被外部引用的内容。**例如：博客中的一篇文章，论坛中的一个帖子或者一段浏览者的评论等。因为article元素是一段独立的内容，所以article元素中，通常包含头部（header元素）、底部（footer元素）。例如博客中的一篇文章的结构：
<pre>&lt;article&gt;
    &lt;header&gt;
        &lt;h1&gt;潜行者m的个人介绍&lt;/h1&gt;
    &lt;/header&gt;
    &lt;p&gt;潜行者m是一个男的中国人。。。。。&lt;/p&gt;
    &lt;footer&gt;
        &lt;p&gt;潜行者m版权所有&lt;/p&gt;
    &lt;/footer&gt;
&lt;/article&gt;</pre>

## section 元素

**section 元素用于对网站或者应用程序中页面上的内容进行分块。**一个 section 元素通常由内容以及标题组成。例如：
<pre>&lt;section&gt;
    &lt;h1&gt;潜行者m的个人介绍&lt;/h1&gt;
    &lt;p&gt;潜行者m是一个男的中国人。。。。。。&lt;/p&gt;
&lt;/section&gt;</pre>
从上例可以看出，**section 元素中，需要包含一个&lt;hn&gt;标题元素**，而一般不用包含头部（header元素）或者底部（footer元素）。通常用 section 元素为那些有标题的内容进行分段。

section 元素的作用，是对页面上的内容分块处理，例如对文章分段等，相邻的 section 元素的内容，应当是相关的，而不是像 article 那样独立。例如一篇文章：
<pre>&lt;article&gt;
    &lt;header&gt;
        &lt;h1&gt;潜行者m喜欢的科技公司&lt;/h1&gt;
    &lt;/header&gt;
    &lt;p&gt;本文中，潜行者m列举了一下他喜欢的科技公司。。&lt;/p&gt;
    &lt;section&gt;
        &lt;h2&gt;google公司&lt;/h2&gt;
        &lt;p&gt;著名的搜索引擎公司。。。&lt;/p&gt;
    &lt;/section&gt;
    &lt;section&gt;
        &lt;h2&gt;苹果公司&lt;/h2&gt;
        &lt;p&gt;非常能创新的公司。。&lt;/p&gt;
    &lt;/section&gt;
    &lt;footer&gt;
        &lt;p&gt;版权所有，翻版不咎&lt;/p&gt;
    &lt;/footer&gt;
&lt;/article&gt;</pre>
通过上面的例子，你应该能感受到 article 元素与 section 元素的区别。事实上 article 元素可以看做是特殊的 section 元素。article 元素更强调独立性、完整性，section 更强调相关性。

## 一个比较完整的例子

<pre>&lt;article&gt;
    &lt;header&gt;
         &lt;h1&gt;潜行者m的个人介绍&lt;/h1&gt;
    &lt;/header&gt;
    &lt;p&gt;潜行者m是一个中国男人，是一个帅哥。。。。&lt;/p&gt;
    &lt;section&gt;
        &lt;h2&gt;评论&lt;/h2&gt;
        &lt;article&gt;
            &lt;h3&gt;评论者：潜行者n&lt;/h3&gt;
            &lt;p&gt;确实，m同学真的很帅&lt;/p&gt;
        &lt;/article&gt;
        &lt;article&gt;
            &lt;h3&gt;评论者：潜行者a&lt;/h3&gt;
            &lt;p&gt;M今天吃药了没？&lt;/p&gt;
        &lt;/article&gt;
    &lt;/section&gt;
&lt;/article&gt;</pre>

## article、section 与 div 的区别

既然 article、section 是用来划分区域的，又是html 5的新元素，那么我可不可以用article、section来取代div，用来布局网页呢？如果你真打算这样做，那么你就像使用ul来打造表格（table）一样愚蠢。**div的用处就是用来布局网页**，划分大的区域，只是html 4中，只有div、span来划分区域，所以我们就习惯性的把div当成了一个容器。而html 5改变了这个，它让div的工作更纯正。div就是用来布局大块，在不同的内容块中，我们按照需求添加 article、section 等内容块，并且显示其中的内容，这样才是合理的使用这些元素。