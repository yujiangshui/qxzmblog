title: 潜行者m的CSS2笔记（一）
tags:
  - CSS
id: 994
categories:
  - 前端相关
date: 2012-05-14 17:03:11
---

以前读书，被强迫着做笔记，但是从来没认真的做过。现在读书，基本上每本书看完都要做一下笔记，这个真的非常重要，一本书你看完会有很多之前没有见过的知识点等，这些东西，就需要记下来，一方面用到的时候快速查询，另一方面记下来。《css网站布局实录-基于web标准的网站设计指南》（第二版）这本书，我买了很久了，看了也有3遍了，2个月前又看了一遍，做了一下笔记，现在拿出来共享一下。

**注意，这份笔记不适合新手，这里面的知识点，不是系统的基础的，而是经常不小心忽略掉但是又常用的。**有经验的朋友，可以看一下，里面的知识点你忽略了多少。

1，相同类型的css定义，默认执行后面的一个，可以用！important语法修改优先性。例如：background-color:red;!important

2，标注某些css hack的地方，使用hack；没完成的地方使用todo。（在大型的工程中，用注释标注一下，方便查询修改）

3，block块状对象占据整行，其他的都移到下一行；in-line行间（内联）允许与下一对象共享一行。

4，尽量减少div的嵌套，会增加浏览器解析的难度。

5，最终宽度=左外边距+左边框+左内边距+宽度+右内边距+右边框+右外边距，最终高度也是如此，需要精确计算，放置错位。

6，重叠的margin会叠加显示，以大值为准。当两个div设定float之后，就不会叠加了。

7，浮动的清理（clear）。使用clear属性来拒绝某个方向上的浮动，这样就不会浮动到上一层了。（这个最好实践一下）

8，父position:relative;子position:absolute。子在父中绝对定位，将以父位置为基准。

9，div应当重点放在大面积区域上，对于简单的导航等，用ul解决。

10，下拉菜单等，可以通过伪类选择器以及display属性来控制。display:none;表示隐藏当前元素。（通常使用javascript来实现下拉菜单，但是现在用纯css也可以实现的很好）

11，css hack:*html—这种方式仅被IE浏览器支持解析，是最常用的css hack之一。

12，div是一个块，用来整体布局设计——block
span是一个范围，用来区别内容——in-line

13，background-attachment:scroll/fixed;设置背景图片的滚动方式。

14，background-color:transparent;透明模式，显示背景。

15，background-position:左对齐方式 上对齐方式 ;用它可以对图像进行精确的定位，同时实现css sprites功能。例如：background-position:0px -27px;

16，ul/ol属性：
list-style-image:none/url;设置图片作为列表中的项目。
list-style-position:inside/outside;设置项目符号的放置位置。
list-style-type:none/disc/......;设置li的表现形式（没有/点状/圆圈/方块等等）

17，display属性：
block：将对象显示成盒状，后一个对象换行显示。
none：隐藏/不显示对象。
inline：行间内联样式，将对象排列成一行。
inline-block：对象显示成块状，但呈现内联样式。
list-item：将对象作为列表项显示

18，float:left;更适合对象布局，但是浮动多了，容易造成浏览器解析混乱。希望让信息显示为段落，最好使用display:inline;（通常设置一个原子类fl{float:left;display:inline;}，元素浮动的时候，加上class="fl")

19，text-indent:value;用于控制段落文本的首行缩进想过。text-indent:20px;表示对象首行缩进20px。如果想要比其他提前一些，可以使用负数值来实现。text-indent:-88888px;设置超大的数值，还可以起到隐藏文本的效果。

20，对于表单样式的控制最基本的方法就是使用border以及background-color。即对表单元素的背景、边框进行设置优化，消除默认难看的样式。

先打这么多，剩下的留在**潜行者m的CSS2笔记（二）**中。