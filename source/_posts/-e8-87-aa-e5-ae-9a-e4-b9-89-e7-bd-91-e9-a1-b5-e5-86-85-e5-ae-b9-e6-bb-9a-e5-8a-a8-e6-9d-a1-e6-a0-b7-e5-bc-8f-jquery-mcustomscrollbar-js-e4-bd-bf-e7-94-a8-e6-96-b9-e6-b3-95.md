title: jQuery 自定义网页滚动条样式插件 mCustomScrollbar 的介绍和使用方法
tags:

- jQuery 插件
  id: 1602
  categories:
- 前端相关
  date: 2012-12-20 23:04:45

---

系统默认的滚动条样式，真的已经看的够恶心了。试想一下，如果在一个很有特色和创意的网页中，出现了一根系统中默认的滚动条样式，会有多么的别扭。 为了自己定义网页中的滚动条的方法，我真的已经找了很久了，就目前寻找的成果来说，找到了两个比较不错的 jQuery 插件：[jScrollPane ](http://www.kelvinluck.com/assets/jquery/jScrollPane/jScrollPane.html)和 [mCustomScrollbar ](http://manos.malihu.gr/jquery-custom-content-scroller/)。关于前者，大家见过的可能比较多，但是这个插件太过于古老而且功能不强大。效果在几年前非常不错，但是放在现在就不好说了。所以我选择了后者： [mCustomScrollbar](http://manos.malihu.gr/jquery-custom-content-scroller/)。下图是两者官方示例的简单对比：

[![jScrollPane 和 mCustomScrollbar 的对比](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll0.png "scroll")](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll0.png)

本文就是介绍如何使用这个插件，大部分的内容，是根据[mCustomScrollbar 官方的介绍页面](http://manos.malihu.gr/jquery-custom-content-scroller/)进行一个翻译，但将其部分内容修改，同时增加一些自己在使用中的一些技巧。

## 关于 mCustomScrollbar

mCustomScrollbar 使用了 jQuery UI，可以通过灵活的通过 CSS 定义你的滚动条。同时可以定义垂直的和水平的滚动条，并且通过 [Brandon Aaron jquery mouse-wheel plugin](http://brandonaaron.net) 提供了鼠标滚动的支持，滚动的过程中，还可以缓冲滚动使得滚动更加的平滑。可以自动调整滚动条的位置并且可以定义滚动到的位置等。总之，你知道非常好用就好了。

[![mCustomScrollbar 效果图](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll1.png "scroll")](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll1.png)

[点击这里可以下载这个 mCustomScrollbar](https://github.com/malihu/malihu-custom-scrollbar-plugin/archive/master.zip)

[点击这里可以查看这个 mCustomScrollbar 的 Demo](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/complete_examples.html)

## 如何使用 mCustomScrollbar

首先，先请你下载作者提供的插件包，里面包含了所有的插件文件和一些例子。以下的四个文件时必须要上传到你的服务器上的：jquery.mCustomScrollbar.js, jquery.mousewheel.min.js, jquery.mCustomScrollbar.css and mCSB*buttons.png*。\_

**第一步：加载插件的样式文件。**

可以使用以下代码，引入插件包中的 jquery.mCustomScrollbar.css 样式表文件。

<pre data-language="html">&lt;link href="jquery.mCustomScrollbar.css" rel="stylesheet" type="text/css" /&gt;</pre>

**第二步：加载必须的 JS 文件。**

需要加载的文件有如下几个：jQuery、jQuery UI， jquery.mousewheel.min.js 和 jquery.mCustomScrollbar.js。jQuery 和 jQuery UI 是必须的， jquery.mousewheel.min.js 是用来提供滚动支持的，jquery.mCustomScrollbar.js 则是插件的主文件。要注意的是，加载顺序也要按照上面说的来，如果不注意加载的顺序，可能会导致失败，原因请看本人的：[网页中代码的顺序是不可忽略的细节](http://www.qianxingzhem.com/post-1539.html)。

你可以使用如下代码加载：

<pre data-language="html">&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7/jquery.min.js"&gt;&lt;/script&gt;
&lt;script src="http://ajax.googleapis.com/ajax/libs/jqueryui/1.8/jquery-ui.min.js"&gt;&lt;/script&gt;
&lt;script src="jquery.mousewheel.min.js"&gt;&lt;/script&gt;
&lt;script src="jquery.mCustomScrollbar.js"&gt;&lt;/script&gt;</pre>

你可以把这段代码放在文档的底部来缩短加载网页内容的时间，原因也可以在上面介绍的那篇文章中看到。这里的加载的代码使用了 Google 的 CDN 加速服务来获得 jQuery 和 jQuery UI，这样的有好处也有坏处。在插件包中，包含了 jQuery 和 jQuery UI（这个 UI 被作者精简了，包含这个插件必须的模块，大小只有 43KB），你当然可以把插件包中的这两个库上传到服务器上使用。它们在插件包的 jquery 目录里面。

如果当你在使用类似 Google 或者 Sina 的常用 Javascript 库的加速服务的话，更推荐采用下面的写法（以 Google 为例）：

<pre data-language="html">&lt;script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7/jquery.min.js"&gt;&lt;/script&gt;
&lt;script&gt;!window.jQuery &amp;&amp; document.write(unescape('%3Cscript src="jquery/jquery-1.7.2.min.js"%3E%3C/script%3E'))&lt;/script&gt;
&lt;script src="http://ajax.googleapis.com/ajax/libs/jqueryui/1.8/jquery-ui.min.js"&gt;&lt;/script&gt;
&lt;script&gt;!window.jQuery.ui &amp;&amp; document.write(unescape('%3Cscript src="jquery/jquery-ui-1.8.21.custom.min.js"%3E%3C/script%3E'))&lt;/script&gt;</pre>

如果这样写，它会在 库 加载完成之后，做一个判断：**如果没有成功加载这个库，那么就生成一段新的 Javascript 引用代码，用来引用本地的文件**。这样，如果外面的库无法使用，就会加载本地的库，而不会导致插件无法使用。推荐这种写法。

**第三步：对 内容块 激活这个插件**

<pre data-language="javascript">&lt;script&gt;
    (function($){
        $(window).load(function(){
            $(".content").mCustomScrollbar();
        });
    })(jQuery);
&lt;/script&gt;</pre>

这里我使用了(function($){ ... })(jQuery)；来包裹 jQuery 代码，这是为了避免 jQuery 和其他的 库 在使用中产生冲突。我还用了window load ($(window).load()) 来激活我的插件功能，因为这样，就可以保证在页面对象全部加载完成之后，加载我的插件。当然，你也可以使用常规的 jQuery 代码加载方法，但是你要明白 ready 和 load 方法之间的不同。一般的 jQuery 代码加载方法如下：

<pre data-language="javascript">&lt;script&gt;
    (function($){
        $(document).ready(function(){
            $(".content").mCustomScrollbar();
        });
    })(jQuery);
&lt;/script&gt;</pre>

**第四步：在页面中添加内容和样式**

没有内容当然谈不上出现这个插件的效果了。就上述示例代码来说，我们应该在页面中定义一个 class 为 content 的 内容块。并添加一些测试数据：

<pre>&lt;div class=".content"&gt;
    &lt;p&gt;测试数据.......还有很多很多&lt;/p&gt;
&lt;/div&gt;</pre>

这样当然不算完，**自定义滚动条的样式，必须要出现滚动条才可以**。所以我们还要对这个块加上一些 CSS 来让它出现滚动条，否则是没有效果的。加上的样式很简单，就是定义一个宽或者高或者宽高都定义，然后再定义一个 overflow 值为 auto。这样如果内容超出了指定的宽高，就会出现一个滚动条。例：

<pre>width:100px;height:100px;overflow:auto;</pre>

完成上述的操作之后，带有滚动条的内容块的滚动条，就变成这个插件的默认样式了。

[![使用 mCustomScrollbar 之后的效果图](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll2.png "scroll")](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll2.png)

官方的默认样式相对于白色的对比度不高，所以为了显示的明显一点，我加了一个深色的背景色。

当然还有很多参数开扩展插件的功能，这些参数的使用方法过后再讲。先来说说上面用到的这些文件的用途和简单介绍：

**jQuery**：这个插件的必备库，你懂。

**jQuery UI**：扩展 jQuery 库并且为我们的滚动条提供了简单的动画和拖动功能。

**jquery.mousewheel.min.js**：这是 [Brandon Aaron](http://brandonaaron.net) 编写的一个伟大的只有 2kb 的插件，它面向所有的操作系统和浏览器，为我们提供了鼠标滚动事件的支持。

**jquery.mCustomScrollbar.js**：这是我们的插件主文件。在插件包的 minified 你可以找到它的压缩版。

**jquery.mCustomScrollbar.css**： 这个 CSS 文件是让我们来定义边栏用的。你可以在这个文件中定义你的边栏，当然你可以在其他的 CSS 文件中定义，要注意的是，你要用 CSS 中的顺序，其中的优先级关系来覆盖这个文件中的定义。否则可能会无效，关于网页中代码顺序，详情可以看一下 [潜行者 m](http://www.qianxingzhem.com) 的这篇文章：[网页中代码的顺序是不可忽略的细节](http://www.qianxingzhem.com/post-1539.html)。

**mCSB_buttons.png**： 这个 png 图片文件，包含了向上向下向左向右滚动的按钮。可以使用 CSS sprites 技术，来使用这个图片中的相应按钮。插件包中包含了这个图片的 PSD 源文件（sources/mCSB_buttons.psd ），你可以根据自己的需求自定义。

完成这些，你已经可以正确的使用这个插件，并且看到了相应的效果。但是没有人愿意使用如此强大的插件来实现这个默认的效果，下面来说一下进阶的使用。

## mCustomScrollbar 的参数介绍

这个插件的功能巨大，所以参数也很多，参数值当然更多。在介绍参数的时候，我想先为新手介绍两种参数值的写法，分别是直接的和合并的。

我 们平时接触的插件用的参数，都是直接跟着参数写上参数值，这个比较直观简单。在这个插件中，参数值太多，所以把一些参数合并起来写。例如下面要介绍到的 scrollButtons 这个参数，它下面有四个属性：enable、scrollType、scrollSpeed、scrollAmount，这四个属性也分别有自己的值，来 实现相应的功能。如果再加上其他的参数，那么我们应该这样写：

<pre>$("#main").mCustomScrollbar({
 scrollButtons:{
 enable:false,
 scrollType:"continuous",
 scrollSpeed:20,
 scrollAmount:40
 },
 horizontalScroll:false,
 });</pre>

一定要注意闭合的括号和语句之间的逗号，新手可能会因为不小心，没有严格的按照这个规则写导致插件无法运行。好，下面我们介绍详细的参数。

- **set_width:false** | 设置你内容的宽度 值可以是像素或者百分比
- **set_height:false** | 设置你内容的高度 值可以是像素或者百分比
- **horizontalScroll:Boolean** | 是否创建一个水平滚动条 默认是垂直滚动条 值可为:true(创建水平滚动条) 或 false
- **scrollInertia:Integer** | 滚动的惯性值 在毫秒中 使用 0 可以无滚动惯性 (滚动惯性可以使区块滚动更加平滑)
- **scrollEasing:String** | 滚动动作类型 查看 [jquery UI easing](http://view.jqueryui.com/formcontrols/demos/effect/easing.html) 可以看到所有的类型
- **mouseWheel:String/Boolean** | 鼠标滚动的支持 值为:true.false,像素 默认的情况下 鼠标滚动设置成像素值 填写 false 取消鼠标滚动功能
- **mouseWheelPixels:Integer** | 鼠标滚动中滚动的像素数目 值为以像素为单位的数值
- **autoDraggerLength:Boolean** | 根据内容区域自动调整滚动条拖块的长度 值:true,false
- **scrollButtons:{   enable:Boolean  }** | 是否添加 滚动条两端按钮支持 值:true,false
- **scrollButtons:{   scrollType:String  }** | 滚动按钮滚动类型 值:"continuous"(当你点击滚动控制按钮时断断续续滚动)  "pixels"(根据每次点击的像素数来滚动) [点击这里可以看到形象的例子](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/scroll_buttons_and_snap_scrolling_examples.html)
- **scrollButtons:{   scrollSpeed:Integer  }** | 设置点击滚动按钮时候的滚动速度(默认 20) 设置一个更高的数值可以更快的滚动
- **scrollButtons:{   scrollAmount:Integer   }** | 设置点击滚动按钮时候每次滚动的数值 像素单位 默认 40 像素
- **advanced:{   updateOnBrowserResize:Boolean  }** | 根据百分比为自适应布局 调整浏览器上滚动条的大小 值:true,false 设置 false 如果你的内容块已经被固定大小
- **advanced:{   updateOnContentResize:Boolean   }** | 自动根据动态变换的内容调整滚动条的大小 值:true,false 设置成 true 将会不断的检查内容的长度并且据此改变滚动条大小 建议除非必要不要设置成 true 如果页面中有很多滚动条的时候 它有可能会产生额外的移出 你可以使用 update 方法来替代这个功能
- **advanced:{   autoExpandHorizontalScroll:Boolean   }** | 自动扩大水平滚动条的长度 值:true,false 设置 true 你可以根据内容的动态变化自动调整大小 [可以看 Demo](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/complete_examples.html)
- **advanced:{   autoScrollOnFocus:Boolean   }** | 是否自动滚动到聚焦中的对象 例如表单使用类似 TAB 键那样跳转焦点 值:true false
- **callbacks:{   onScrollStart:function(){}   }** | 使用自定义的回调函数在滚动时间开始的时候执行 [具体请看 Demo](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/callbacks_example.html)
- **callbacks:{   onScroll:function(){}   }** | 自定义回调函数在滚动中执行 Demo 同上
- **callbacks:{   onTotalScroll:function(){}  }** | 当滚动到底部的时候调用这个自定义回调函数 Demo 同上
- **callbacks:{   onTotalScrollBack:function(){}   }** | 当滚动到顶部的时候调用这个自定义回调函数 Demo 同上
- **callbacks:{   onTotalScrollOffset:Integer   }** | 设置到达顶部或者底部的偏移量 像素单位
- **callbacks:{  whileScrolling:function(){}  }** | 当用户正在滚动的时候执行这个自定义回调函数
- **callbacks:{  whileScrollingInterval:Integer  }** | 设置调用 whileScrolling 回调函数的时间间隔 毫秒单位
下面是所有参数的列表和它们的默认值
<pre data-language="javascript">$(".content").mCustomScrollbar({
  set_width:false,
  set_height:false,
  horizontalScroll:false,
  scrollInertia:550,
  scrollEasing:"easeOutCirc",
  mouseWheel:"auto",
  autoDraggerLength:true,
  scrollButtons:{
    enable:false,
    scrollType:"continuous",
    scrollSpeed:20,
    scrollAmount:40
  },
  advanced:{
    updateOnBrowserResize:true,
    updateOnContentResize:false,
    autoExpandHorizontalScroll:false,
    autoScrollOnFocus:true
  },
  callbacks:{
    onScrollStart:function(){},
    onScroll:function(){},
    onTotalScroll:function(){},
    onTotalScrollBack:function(){},
    onTotalScrollOffset:0,
    whileScrolling:false,
    whileScrollingInterval:30
  }</pre>

## mCustomScrollbar 的方法

### update

用法：\$(selector).mCustomScrollbar("update");

调用 mCustomScrollbar 函数的 update 方法去实时更新滚动条当内容发生变化（例如 通过 Javascript 增加或者移除一个对象、通过 ajax 插入一段新内容、隐藏或者显示一个新内容等）

下面是例子：

<pre data-language="javascript">$(".content .mCSB_container").append("&lt;p&gt;New content here...&lt;/p&gt;");
$(".content").mCustomScrollbar("update");</pre>
<pre data-language="javascript">$(".content .myImagesContainer").append("&lt;img src='myNewImage.jpg' /&gt;");
$(".content .myImagesContainer img").load(function(){
  $(".content").mCustomScrollbar("update");
});</pre>
<pre data-language="javascript">$("#content-1").animate({height:800},"slow",function(){
  $(this).mCustomScrollbar("update");
});</pre>

当新内容完全加载或者动画完成之后，update 方法一直被调用。

### scrollTo

用法：\$(selector).mCustomScrollbar("scrollTo",position);

你可以使用这个方法自动的滚动到你想要滚动到的位置。这个位置可以使用字符串（例如 “#element-id”，“bottom” 等）描述或者是一个数值（像素单位）。下面的例子将会滚动到最下面的对象

<pre data-language="generic">$(".content").mCustomScrollbar("scrollTo","last");</pre>

scrollTo 方法的参数

- **\$(selector).mCustomScrollbar("scrollTo",String);** | 滚动到某个对象的位置，字符串型的值可以是 id 或者 class 的名字
- ** \$(selector).mCustomScrollbar("scrollTo","top");** | 滚动到顶部（垂直滚动条）
- **\$(selector).mCustomScrollbar("scrollTo","bottom");** | 滚动到底部（垂直滚动条）
- ** \$(selector).mCustomScrollbar("scrollTo","left");** | 滚动到最左边（水平滚动条）
- **\$(selector).mCustomScrollbar("scrollTo","right");** | 滚动到最右边（水平滚动条
- **\$(selector).mCustomScrollbar("scrollTo","first");** | 滚动到内容区域中的第一个对象位置
- **\$(selector).mCustomScrollbar("scrollTo","last");** | 滚动到内容区域中的最后一个对象位置
- **\$(selector).mCustomScrollbar("scrollTo",Integer);** | 滚动到某个位置（像素单位）
  scrollTo 方法还有两个额外的选项参数

**moveDragger: Boolean** | 滚动滚动条的滑块到某个位置像素单位，值：true，flase。例如：\$(selector).mCustomScrollbar("scrollTo",200,{ moveDragger:true });

**callback：Boolean** | 执行回调函数当 scroll-to 完成之后，值：true，false 例如：\$(selector).mCustomScrollbar("scrollTo",200,{ callback:true });

### disable

用法：\$(selector).mCustomScrollbar("disable");

调用 disable 方法去使滚动条不可用。如果想使其重新可用，调用 update 方法。disable 方法使用一个可选参数（默认 false）你可以设置 true 如果你想重新让内容区域滚动当 scrollbar 不可用时。例如：

<pre>$(".content").mCustomScrollbar("disable",true);</pre>

[可以看一些使用 disable 的例子](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/disable_destroy_example.html)

### destroy

用法：\$(selector).mCustomScrollbar("destroy");

调用 destroy 方法可以移除某个对象的自定义滚动条并且恢复默认样式

[可以看一些使用 destroy 的例子](http://manos.malihu.gr/tuts/custom-scrollbar-plugin/disable_destroy_example.html)

## mCustomScrollbar 的原理

通过潜行者 m 对这些插件的使用，对这些插件的实现原理也做了一些分析。原理就是这样的：

首先获取要修改滚动条样式的内容区块，然后使用 CSS 隐藏掉默认滚动条，然后使用 Javascript 添加很多 HTML 结构，再配合 CSS 做出一个滚动条的效果。然后再使用 CSS 定义滚动条的样式，使用 Javascript 相应鼠标的滚动事件，产生滚动下滑的效果。

明白了这点，下面我们就可以看一下滚动条的结构，然后使用 CSS 对其进行定义了。

## 定义滚动条外观

先了解一下滚动条的 HTML 结构，下面是默认的垂直滚动条结构：

<pre data-language="html">&lt;div class="content mCustomScrollbar _mCS_1"&gt;
  &lt;div class="mCustomScrollBox"&gt;
    &lt;div class="mCSB_container"&gt;
      &lt;!-- your long content here... --&gt;
    &lt;/div&gt;
    &lt;div class="mCSB_scrollTools"&gt;
      &lt;a class="mCSB_buttonUp"&gt;&lt;/a&gt;
      &lt;div class="mCSB_draggerContainer"&gt;
        &lt;div class="mCSB_dragger ui-draggable"&gt;
          &lt;div class="mCSB_dragger_bar"&gt;&lt;/div&gt;
        &lt;/div&gt;
        &lt;div class="mCSB_draggerRail"&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;a class="mCSB_buttonDown"&gt;&lt;/a&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;</pre>

mCSB_buttonUp 和 mCSB_buttonDown 这两个 a 标签只有当你启用了 scroll buttons 功能的时候，才可用。下面这个结构是 水平滚动条 的结构：

<pre data-language="html">&lt;div class="content mCustomScrollbar _mCS_1"&gt;
  &lt;div class="mCustomScrollBox mCSB_horizontal"&gt;
    &lt;div class="mCSB_container"&gt;
      &lt;!-- your long content here... --&gt;
    &lt;/div&gt;
    &lt;div class="mCSB_scrollTools"&gt;
      &lt;a class="mCSB_buttonLeft"&gt;&lt;/a&gt;
      &lt;div class="mCSB_draggerContainer"&gt;
        &lt;div class="mCSB_dragger ui-draggable"&gt;
          &lt;div class="mCSB_dragger_bar"&gt;&lt;/div&gt;
        &lt;/div&gt;
        &lt;div class="mCSB_draggerRail"&gt;&lt;/div&gt;
      &lt;/div&gt;
      &lt;a class="mCSB_buttonRight"&gt;&lt;/a&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;</pre>

知道这些之后，我们就可以来定义滚动条样式了，对于同一页面多个滚动条，官方推荐如下的写法：

<pre data-language="css">._mCS_1 .mCSB_scrollTools .mCSB_dragger .mCSB_dragger_bar{
    /* 1st scrollbar dragger style... */
}
._mCS_2 .mCSB_scrollTools .mCSB_dragger .mCSB_dragger_bar{
    /* 2nd scrollbar dragger style... */
}
._mCS_3 .mCSB_scrollTools .mCSB_dragger .mCSB_dragger_bar{
    /* 3rd scrollbar dragger style... */
}</pre>

为了更加直观的看到要定义的滚动条区域，官方给出了一张非常形象的图片

[![mCustomScrollbar 的滚动条结构图](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll3.png "scroll")](https://qxzm-cdn.sapi.work/blog/2012/12/1602/scroll3.png)

根据这张图片，就可以很容易的定义滚动条的样式了。

## 更加进阶的使用

### 修改浏览器的滚动条

单单是修改某个内容区域的边栏已经无法满足我们的需求了，我们还想修改浏览器边栏应该怎么办？这当然是无法用 Javascript 来实现，因为浏览器是一个容器，Javascript 是容器里面的代码，怎么会把容器修改了呢？当然，有问题就肯定有解决方法。面对这个问题，解决方法很简单，就是虚拟出来一个浏览器窗口。

我们先添加一个 div 块，然后对这个 div 添加 position：absolute 属性，然后就可以指定它的 width 和 height 为 100% 或者稍微小点的 98%。这样，这个 div 就扩充到了整个浏览器界面，这样就可以被当做是一个网页的 body。然后加上 overflow：auto 让其超出自动出现滚动条。这样就可以模拟出修改了浏览器滚动条的效果。

关于更多的进阶使用和技巧，欢迎跟我交流，也可以关注本文，会在后面陆续添加。
