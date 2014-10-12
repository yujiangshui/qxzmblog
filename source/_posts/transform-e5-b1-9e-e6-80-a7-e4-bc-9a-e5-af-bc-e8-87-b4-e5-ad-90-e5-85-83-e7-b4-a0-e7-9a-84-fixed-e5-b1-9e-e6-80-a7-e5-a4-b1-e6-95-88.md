title: Transform 属性会导致子元素的 fixed 属性失效
tags:
  - CSS3
id: 1985
categories:
  - CSS
  - 前端相关
date: 2013-06-07 05:35:47
---

在项目中，需要为顶部导航条增加滚动跟随效果。很显然，只需要为 #header 加上 position:fixed; 属性即可，但是加上之后却无效。只能用监测浏览器滚动距离然后实时的赋值到 top 属性来模拟跟随。

但是这种方法由于浏览器之间滚动的距离不同等缘故，会导致闪烁等问题，只在 Firefox 效果完美。同时会影响性能，在中低端安卓设备中效果很差。这种影响用户体验的事情，是肯定要避免的。还是得回来使用 fixed，但是从未发现过 fixed 失效的情况啊，只能挨个测试一下。

## 问题发现

先写了一个 div ，赋值 fixed 属性，然后在普通网页中效果正常。将其插入无效代码平级位置，结果失效。将其插入 body 标签下级，正常。说明问题出在其父属性值中。

然后使用 Firebug 依次取消父属性值，当去掉 transform 属性值之后，fixed 生效。原来问题出在 transform 上。

[然后就做了个 Demo 测试一下。](http://www.qianxingzhem.com/demo/1985/)

这是一个坑，如果不知道的，可以记一下。因为 transform 是一个 CSS3 中比较重要的动画属性，以后的应用会越来越多。对于 position 的其他属性尚未测试，因为 fixed 比较特殊，效果比较明显。在 google 上搜索了一下，发现了一篇 Eric 写的 [Un-fixing Fixed Elements with CSS Transforms](http://meyerweb.com/eric/thoughts/2011/09/12/un-fixing-fixed-elements-with-css-transforms/ "Permanent Link: Un-fixing Fixed Elements with CSS Transforms") ，不过没看懂，还望各位有知道的指点一下。