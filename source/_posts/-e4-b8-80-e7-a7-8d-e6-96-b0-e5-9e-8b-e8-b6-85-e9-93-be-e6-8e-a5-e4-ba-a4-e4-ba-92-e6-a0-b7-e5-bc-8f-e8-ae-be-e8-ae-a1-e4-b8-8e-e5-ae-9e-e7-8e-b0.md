title: 一种新型超链接交互样式设计与实现
tags:
  - CSS
id: 1649
categories:
  - 前端相关
date: 2013-01-17 00:48:56
---

超链接是网页中，必不可少的内容。超链接的交互设计，也是一个网页中最重要的细节。CSS 也为链接准备了几个伪类选择器，用来设置超链接的交互操作。但是在绝大多数网站中，我们看到的超链接交互样式，通常是：改变一下链接的颜色、取消或者增加下划线、点击链接文本变色或者下划线消失等等。但实际上，超链接的交互设计，并非只能这么简单。

很久没有登录 W3C 的官方网站，今天上去看了一下，从第一眼就看到了他们的超练级的与众不同。把鼠标放上，点击，测试了一下他们的超链接交互设计，感觉非常不错，就稍微思考了一下这个设计是如何实现的。稍微思考一下之后，才发现实现这个效果非常的容易，而且兼容性较好。下面就来介绍一下。

先来看一下他们的效果图片，当然，我更推荐直接去 [W3C 官方网站](http://www.w3.org/)看效果。

[![w3c 的超链接交互性演示](http://qxzm-img.b0.upaiyun.com/blog/2013/01/1649/link0.png "w3c 的超链接交互性演示")](http://qxzm-img.b0.upaiyun.com/blog/2013/01/1649/link0.png)

## 实现原理和分析

首先，仍然是常规的超链接样式，带一条下划线，但是与普通的超链接样式不同的是，这条下划线要粗（2px 普通的 1px），同时这个下划线和文字颜色不同（用 color 和 text-decoration 定义的超链接下划线颜色是和文本相同的）。所以可以肯定，这个下划线是使用 border-bottom 属性定义的，并且 padding-bottom 了几个像素，空开一定距离。然后交互性操作就很简单了，只需要改变一下底边框的颜色就可以了。当点击事件发生的时候，超链接不是简单的改变了颜色，而是向下移动了几个像素，这样给人的错觉就是按下去了一样，这种用户体验是传统超链接仅仅变换颜色所体验不到的。关于这个的实现，需要使用 position 的 relative 属性，激活 top 属性，即可让超链接脱离原来位置向下偏移一定距离。

既然原理分析完毕，那么我们就开始写出相应代码吧。

## HTML 结构

随便输入一些字，加上个链接就OK了。
<pre>&lt;div&gt;
 这里是 潜行者m 随便打的一些字，用来做链接交互样式的演示，&lt;a href="#"&gt;链接在这里&lt;/a&gt;。这里是 潜行者m 随便打的一些字，用来做链接交互样式的演示，&lt;a href="#"&gt;链接在这里&lt;/a&gt;。这里是 潜行者m 随便打的一些字，用来做链接交互样式的演示，&lt;a href="#"&gt;链接在这里&lt;/a&gt;。
 &lt;/div&gt;</pre>

## CSS 样式

<pre>div{width:300px;margin:20px auto;line-height:24px;}
 div a{text-decoration:none;color:#000;padding-bottom:1px;}
 div a:link,div a:visited{border-bottom:2px solid #f00;}
 div a:hover{border-bottom:2px solid #00f;}
 div a:active{border-bottom:2px solid #00f;outline:0 none;position:relative;top:1px;}</pre>
对 div 的宽度定义只是为了好看而已，对行高的定义，是为了不让下划线影响到下一行文字，这个可以自己决定。然后先对 a 标签取消默认的下划线和颜色，再就是交互性的操作。注意，对 :active 使用了 outline 属性，防止有些浏览器在点击超链接的时候，超链接会出现边框。

## 发散思维

既然是用了边框的方式模拟下划线，那么可不可以通过调整超链接的高度让这条线变成一条可以交互操作的 “删除线” 呢？当然是可以的，我们只需要把 height 属性调小一点同时还需要让 a 的 display 属性变成 inline-block，就可以让边框穿过文字，由于 overflow 的默认属性是 visible 所以文本仍然是可见的。
<pre>div a{text-decoration:none;color:#000;padding-bottom:1px;height:6px;display:inline-block;}</pre>
这样就实现了下图效果

[![具有交互性的边框模拟删除线样式](http://qxzm-img.b0.upaiyun.com/blog/2013/01/1649/link1.png)](http://qxzm-img.b0.upaiyun.com/blog/2013/01/1649/link1.png)

需要注意的是 a 元素是行间元素，直接对其使用 height 是没有作用的，但是对其加上 display：block 变成块元素，则会脱离文本，所以需要添加 inline-block 属性。但是这样，对于早期的 IE 浏览器兼容性不太好。

制作这样一个超链接的交互样式非常简单，而且交互效果很不错，平时我们应该多一点细心和发散思维，才能不断提高用户体验。

## 推荐阅读

[a 标签的样式规划](http://www.neoease.com/a-tag-css-design/)

[inline-block 前世今生](http://ued.taobao.com/blog/2012/08/inline-block/)