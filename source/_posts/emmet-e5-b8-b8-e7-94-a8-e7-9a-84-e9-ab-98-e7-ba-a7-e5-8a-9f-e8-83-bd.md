title: Emmet 常用的高级功能
tags:
  - emmet
  - sublime text 2
id: 1995
categories:
  - 前端相关
date: 2013-06-28 18:14:10
---

Emmet 的功能不仅仅局限在快速生成标记语言结构或者生成 CSS 代码，它还具有很多常用的前端相关的功能，下面就来介绍几个比较常用的功能。

## 生成 Lorem Ipsum

`Lorem Ipsum` 表示一段随机看不懂的文字。`Lorem Ipsum` 的文字让人看不懂，这样才能忽略内容的含义而专注内容的排版，作为测试数据填充用的。使用 Emmet 生成 `Lorem Ipsum` 文本非常简单，只需要使用 `lorem `这一条命令即可，敲击 Tab 键之后，就会生成如下一段文字：
<pre>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Qui, dolor, aperiam ab repellendus blanditiis eum exercitationem. Quae, reprehenderit repellat impedit asperiores consequatur? Illum quos magnam odit omnis recusandae natus similique.</pre>
Emmet 的 lorem 命令不仅仅只有输出这么一段文字这样一个简单的功能，它既然作为测试数据，可以加上参数指定要输出的字符数量。例如，我们如果想输出一个十个单词的 h1 标题，我们就可以使用如下命令 `h1&gt;lorem10` 。但是这项功能对于使用中文的网页测试来说，好像没有多大用处，毕竟中文和英语单词的排版是不同的。

##  跳转编辑区域

写代码一般要用到两只手，有时候需要跳转到别的代码段等，你可以使用键盘方向键也可以使用鼠标。但是这都有缺陷，使用键盘方向键移动太慢了，而且需要按住 shift 键和方向键选中代码；使用鼠标的话，手就必须离开键盘，来回也会浪费一些时间。而 Emmet 提供了一个很实用的功能，就是整块的跳转。

为了方便理解，先看一下[官方的 Demo 动画](http://docs.emmet.io/actions/select-item/)。这个功能，使用 `Shift+Ctrl+.` 和 `Shift+Ctrl+,` 分别向下或者向上移动，选取的是一整块，先从标签开始，再是整个属性，再是属性值。这样，比键盘的方向键移动高效多了。

## 增加图片的尺寸大小

有时候，我们需要给 &lt;img&gt; 标签增加对应的 width、height 属性来表示图片的大小或者给通过 background-image 属性引用的背景图片一个尺寸大小。通常的做法是看一下图片的尺寸，然后加上，而现在，你只需要将光标移动到代码段，摁下 `Ctrl+U` 即可让 Emmet 自动读取图片的尺寸添加上。前提条件是图片比较存在并且正确引用进来了。

如果是针对 &lt;img&gt; 标签的，会在后面加上 width、height 属性，如果是 background 引入的，会在下面加上 width、height 的 CSS 属性。可以看一下[官方的 Demo ](http://docs.emmet.io/actions/update-image-size/)。但是这里有个问题，官方的 Demo 中，实现这个功能的快捷键是 `Shift+Ctrl+U` 但实际使用中，这个快捷键不起作用。关于 Emmet 的 Mac、Win 下的快捷键，以这个页面上的为准：[https://github.com/sergeche/emmet-sublime#available-actions](https://github.com/sergeche/emmet-sublime#available-actions)。

## 更新 CSS 的属性值

我们在写 CSS 的时候，有时候为了 hack 写很多带有前缀的属性。例如：
<pre>-webkit-transform: rotate(30deg);
-moz-transform: rotate(30deg);
-ms-transform: rotate(30deg);
-o-transform: rotate(30deg);
transform: rotate(30deg);</pre>
如果我们突然想修改一下旋转的角度值，那么我们就需要依次修改或者按住 Ctrl 多个选中进行修改。使用 Emmet 的话，就方便多了，我们只需要修改其中一个，然后摁下 `Shift+Ctrl+R` 键即可更新其他的相关属性值。

## 将图片资源转换成 data url 形式

data url 图片具有很多优点，在某些情况下比较实用，但是将图片转换成 data url 格式就比较麻烦了，得使用一些工具。而在 Emmet 中，将光标移动到 background: url() 中的图片位置的地方，按下` Ctrl+’` 即可将图片编码成 data url 格式。当然，前提条件是图片资源引用正确。

除此之外，Emmet 还有一些其他的诸如快速跳转、计算等等常用功能，在这里只是介绍了几个更常用的功能，有兴趣的朋友可以打开[Emmet Action 的官方文档](http://docs.emmet.io/actions/)看一下 Demo，这里不再赘述。