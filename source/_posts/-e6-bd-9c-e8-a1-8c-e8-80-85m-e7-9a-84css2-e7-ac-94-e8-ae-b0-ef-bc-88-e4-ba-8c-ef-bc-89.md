title: 潜行者m的CSS2笔记（二）
tags:
  - CSS
id: 1005
categories:
  - 前端相关
date: 2012-05-18 14:24:46
---

接上面的文章，[潜行者m的CSS2笔记（一）](http://www.qianxingzhem.com/post-994.html)。

21，使用line-height属性来控制行高，使文字居中，控制文字排版。

22，使用&lt;label&gt;标签，可以让人点击文本选中相应单选复选，提高网站交互性。例子&lt;label for="c1"&gt;点击此文本&lt;/label&gt;&lt;input type="checkbox" name="c1" id="c1" value="ckbox"/&gt;

23，对于文本下划线，可以使用border-bottom来实现丰富的定义。

24，li{width:120px;text-overflow:ellipsis;}当内容超出对象宽度时，显示为省略号。clip将不显示。必须使用word-break:keep-all;使其被强制不能换行。

25，em是一种相对弹丸。text-indent:2em;表示空出两个字符的距离，em长度相当于本行中字符的倍数，这个单位非常实用。

26，首字下沉使用css伪类。p:first-letter{font-size:2em;float:left;}。first-line伪类对第一行进行设置。

27，在布局中，出现布局的错位等，可以使用相对定位。尽量避免绝对定位。

28，剪切图像可以使用clip。使用div overflow属性进行剪切图像，用img margin移动剪切区域。

29，图片代替文本，内含不显示文本，表明图像的内容，非alt属性。两种实现方法：display:none;text-indent:-99999px;

30，a:link只会对拥有href=“”的a发生作用。

31，使用图片代替文本，对搜索引擎有利，有利seo。

32，使用导航等，显示边框的时候，最好加上一个背景边框，防止错位。

33，pimg{float:left;padding:10px;}设置图片浮动方式，可以将图片嵌入文字流。

34，如果想要添加图片说明，将文字与img放在一个div中，之后对文字等进行设置。

35，表格布局对table、tr、td进行定位，border-collapse：collapse;属性表示将表格中单元格之间线条合并。border-collapse：separate:则将使各单元格的边框独立存在。

36，@import导入命令是将目的文件包含进来。例如：@import url("home.css");
还可以指定一个设备类型，指明当前的样式表用于什么操作，例如：
@import url("pageprint.css") print;表示在打印文件的时候，使用pageprint.css这个样式表。

37，提高css效率的方法：
1，按照功能划分css文件。
2，在需要这方面功能的页面，引用相应的样式表文件。引用用上面的import

38，用css制造进度条等，使用行间样式。

整本书大部分的内容，都已经吸收同化进潜行者m的身体中，对于这38条笔记的内容，掌握的还不是很熟悉，所以做成笔记，以便在日后进行翻阅。

在随后的一段时间内，我将继续公布潜行者m的个人笔记，包括seo、html5、css3、php、javascript等等。