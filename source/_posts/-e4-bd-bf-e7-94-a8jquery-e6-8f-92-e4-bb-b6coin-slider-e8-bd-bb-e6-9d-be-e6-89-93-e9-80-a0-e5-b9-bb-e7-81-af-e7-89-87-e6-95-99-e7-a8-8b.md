title: 使用jquery插件coin-slider轻松打造幻灯片教程
tags:
  - jQuery
  - jQuery插件
id: 1085
categories:
  - 前端相关
date: 2012-08-21 00:00:40
---

今天为了做一个模板，来收集幻灯片插件，最终确定了两款比较合适的。coin-slider和nivoslider，为此，研究了一下午，从各个方面来实验这两款插件，究竟哪款比较适合、比较好。

当然，聪明的你看题目就已经知道了。我必须要吐槽一下nivoslider这个jquery插件。这两款插件，在看官方的demo时，这个插件的效果要比coin-slider好一些。看了一下教程，可以自定义的参数较多，貌似功能要更强大一下。于是我就首先研究了一下这款插件的使用方法。由于网上教程比较少，大部分都是直接复制的官方教程，我就直接拿官方的demo代码来看了。这一看，直接晕死。加载了N个css文件，以及各种图片文件，当场晕死。demo里面的代码，也是很多很乱，不是怕多、乱的代码，就怕引用的各种文件各种效果的叠加，分析起来累死个人。

干脆自己按照步骤，自己写个小demo，看一下这款插件的易用性怎么样。按照官方的步骤，写好了图片链接，加载了需要的javascript文件等。打开一看，立刻没有了官方demo的美观和强大，上面的翻页等，都是需要css定义，这个暂时没有管理，所以难看就难看吧。图片切换也算正常，不正常的地方就是，在某个地方，出现了下一张图片的一大堆图片块。这种切换的原理很简单，生成很多div，每个div用css中的background-position属性，把整体的图片切成块，然后对每块进行透明度等的变化，显示的效果就是你看到的那种。但是现在，在旁边出现了一堆块都是乱的，直接无语。具体什么情况，我已经删了，也不截图了。估计是某块css没有定义好，当我打开官方demo的css时，又怵头了，这么多，这么乱的代码。功能的强大，必定面临使用的难度提升，估计这个是给专家级用户使用的，我等小白还是趁早溜走吧。研究了两三个小时，无疾而终。转身向coin-slider走去。

先在网上搜索一下相关资料，某前辈已经写出了一个教程，并且自己做了一个demo，下载下来看了下，效果挺好，代码挺少。同时也下载了官方的demo，打开官方demo，下面的说明，说的清清楚楚的。简而言之就是：加载必备组件=》你自己写图片链接=》执行那个操作。实事也是如此，可能我之前研究nivoslider，而coin-slider和它的原理和操作类似，所以我很快就上手并且做出了自己想要的效果。下面来依次讲解：

**1，加载必备组件**

这个coin-slider是jquery的一个插件，当然离不开jquery了。所以我们要加载三个项目：jquery、coin-slider和coin-slider-styles.css这三个。后面两个就是这个插件包，最后的那个css文件，是用来格式化幻灯片的相关样式。我估计nivoslider就是因为缺少了一个这个，所以才导致的乱，也有可能是我没有发现这个东西。代码如下：
<pre>&lt;script type="text/javascript" src="jquery.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="coin-slider.min.js"&gt;&lt;/script&gt;
&lt;link rel="stylesheet" href="coin-slider-styles.css" type="text/css" /&gt;</pre>
**2，编写你的图片链接**

我们首先需要指定一个带有id的div标签，这样在第三步执行的时候，插件才能找到我们想要播出的图片。它的图片的写法，也有几个特点，就是如果你想点击图片跳转到某链接，在外面加上a标签；在img标签后面，新建一个span标签，里面的内容，将会作为图片的说明文字出现。直接看代码：
<pre>&lt;div id="coin-slider"&gt; 
    &lt;a href="#" &gt;
        &lt;img src="images/walle.jpg" &gt;
        &lt;span&gt;
            Description for nem&lt;br /&gt;oDescription for nemoDescription for nemoDescription for nemoDescription for nemoDescription for nemoDescription for nemoDescription for nemoDescription for nemoDescription for nemo
        &lt;/span&gt;
    &lt;/a&gt;
    &lt;a href="#111"&gt;
        &lt;img src='images/nemo.jpg' &gt; //加载的图片
        &lt;span&gt; //图片对应的说明
            Description for nemo
        &lt;/span&gt;
    &lt;/a&gt;    
&lt;/div&gt;</pre>
这个代码的大体框架,是我从官方的demo中提取出来的,这里我又要吐槽一下了,官方的demo文件,写的实在是太不规范了，html标签都用的是大写，而且从上面的img的src就可以看出来，他们竟然用了单引号！css文件里也是这样，患有代码强迫症的潜行者m，花了好几分钟，才把大部分代码变成小写，添加合适的换号，真无语。看了一下开发时间，2010年的作品，那时候xhtml应该普及了，为什么还用大写的写法，无语了。

**3，执行操作**

确保上面两个步骤完成之后，就需要触发它的方法，来实现幻灯片的功能了。方法当然是
<pre>    $(document).ready(function() {
        $('#coin-slider').coinslider({ height:248 }); //使用各种参数配置来扩充他的功能
    });</pre>
当然，你也可以使用window.onload，那样可以确保幻灯片图片被完全下载下来之后，再出现幻灯片。

很显然，还可以配置很多参数，让幻灯片的功能更加强大。在上面的代码中，我添加了一个参数height：248，因为我的照片高度是248px。下面介绍一下其他参数，我在官方注释后面，小小的翻译了一下，不准确的话，还望见谅。
<pre>width: 565, // width of slider panel 幻灯片的宽度
height: 290, // height of slider panel 幻灯片的高度
spw: 7, // squares per width 幻灯片切出小方框的宽度
sph: 5, // squares per height 幻灯片切出小方框的高度
delay: 3000, // delay between images in ms 切换图片的时间，毫秒单位
sDelay: 30, // delay beetwen squares in ms 小方框变化的时间，毫秒单位（这两个尽量不要改，官方说改了容易出现过度问题）
opacity: 0.7, // opacity of title and navigation 图片下面的说明文字背景的透明度
titleSpeed: 500, // speed of title appereance in ms 标题消失的速度，毫秒单位
effect: '', // random, swirl, rain, straight 变换样式，随机，漩涡，下雨，连续（自己试试就知道效果）
navigation: true, // prev next and buttons 是否显示前个、后个按钮
links : true, // show images as links  是否把图片当做一个链接
hoverPause: true // pause on hover 你把鼠标放上去的时候，图片是否继续变化</pre>
我们只需要像这样，填上自己定义的参数即可：
<pre>$('#coin-slider').coinslider({ width: 900, navigation: false, delay: 5000 });</pre>
**4，高级用法**

在具体的使用过程中，它的默认样式，肯定不符合我的模板需求，所以我需要对它进行更加细致的修正。那就是通过css，官方的css文件里，你可以直接修改，你也可以新建css文件，对它进行定义。在火狐浏览器中，可以方便观看这个插件生成了些什么div标签，以及相应的id和class。既然你是高级用户，当然难不倒你，我只是在这里提一个思路，具体的就要靠你自己去修改了。

最后，打包一下本教程的资源，放上来。**点击下载：**[coin-slider](http://pan.baidu.com/share/link?shareid=90714&uk=706095745)

&nbsp;