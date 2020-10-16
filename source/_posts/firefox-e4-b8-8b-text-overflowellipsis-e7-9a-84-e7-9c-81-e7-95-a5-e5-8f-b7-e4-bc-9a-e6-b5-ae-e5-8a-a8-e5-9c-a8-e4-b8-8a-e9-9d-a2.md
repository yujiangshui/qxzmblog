title: "Firefox 下 text-overflow:ellipsis 的省略号会浮动在上面"
tags:
  - BUG
id: 1993
categories:
  - CSS
  - 前端相关
date: 2013-06-26 07:16:04
---

`text-overflow:ellipsis` 属性通常用于隐藏超出长度的文本，并在文本最后面增加省略号。

[456bereastreet](http://www.456bereastreet.com/archive/201305/firefox_and_the_magical_text-overflowellipsis_z-index/) 发现：如果在网页的交互等过程中，出现一个新层（例如鼠标移动到下拉菜单，弹出下拉菜单内容），在 Firefox 下，文本内容当然会被新弹出内容遮住，但是省略号并不会。它会出现在新层的上面。

可以使用 Firefox 打开 [Demo ](http://www.456bereastreet.com/lab/text-overflow-ellipsis-firefox/)看一下具体效果。

如果你也遇到了这个问题，解决方法很简单，只需要为新弹出的覆盖层的 z-index 属性赋值为 `>1` 的数值即可，这样就可以解决了。你可以在上面的 Demo 中，使用 Firebug 增加一下。