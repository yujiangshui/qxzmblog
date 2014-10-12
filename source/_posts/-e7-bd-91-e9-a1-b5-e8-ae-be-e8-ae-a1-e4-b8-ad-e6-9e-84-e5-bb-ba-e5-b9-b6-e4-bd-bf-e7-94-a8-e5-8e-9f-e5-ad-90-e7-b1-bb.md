title: 网页设计中构建并使用原子类
tags:
  - CSS
id: 939
categories:
  - 前端相关
date: 2012-04-08 13:36:04
---

在《编写高质量代码 Web前端开发修炼之道》一书中，作者总结经验，认为网页设计中，css应当分为三层，分别为base层、common层、page层。其中base层为样式最底层，里面包含css reset代码和原子类，基本不需要维护。common层是中层的样式，设置一个网站频道等的样式。page层，则是具体页面的样式。如果把网页设计比作盖房子，base层就是地基，common层就是你这个房子的墙壁、结构，page层就是你房子的内饰等。

之前，[潜行者m](http://www.qianxingzhem.com/)已经写过[一篇关于css reset的文章](http://www.qianxingzhem.com/post-610.html)，而今天，潜行者m就来介绍一下原子类。

原子类是可以高度重用的css样式。例如width:10px;或者是float:left;这类样式，很多的元素都要用到这类样式，但是在每个元素的css样式中，都添加这条语句，无疑会增加代码数量，使其不够简洁，而且当css样式很多的时候，维护起来就会非常麻烦。于是就有了css通用原子类。

如何编写？

在css文件中，编写简单简洁的类，每个类实现一个具体的小功能，并且命名一个非常简单直观的名字，例如：

.w{width:auto;}

.w10{width:10px;}

.fl{float:left;}

.fr{float:right;}

............

在上面，只写了几个样式，作为例子，实际的原子类文件中，会包含各种原子类。

如何使用？

编写完成之后，我们应该如何在元素中，使用原子类？这就要用到元素的class属性了。在一个页面元素中，class属性值可以重复，并且可以指定多个样式。例如，我想要让这个div元素，宽度为10px，并且向左浮动，那么我就可以这样写：

&lt;div class="w10 fl"&gt;&lt;/div&gt;

这样写之后，就说明这个div元素，同时具有.w10 .fl两个类的css样式。而如果我想要另一个div元素，宽度10px，并且向右浮动，我们就可以这样写：

&lt;div class="w10 fr"&gt;&lt;/div&gt;

而不必为每个div分别制定width:10px;，这样就可以节约代码，高度重用代码了。同时，简短形象的名字，也可以让人非常容易理解样式的意思，例如一个div的class属性是w100 h100 fl，我们就可以知道，这个div宽100px，高100px，向左浮动，日后修改等都是非常方便的。

推荐使用 潜行者m 的 [CSS creater](http://lab.qianxingzhem.com/app/csscreater/) 在线生成包含 常用原子类的 CSS 文件。地址：[http://lab.qianxingzhem.com/app/csscreater/](http://lab.qianxingzhem.com/app/csscreater/)
<div></div>