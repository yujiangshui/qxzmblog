title: 实现网页换肤功能的最优解（带 Cookie 记录功能）
tags:

- jQuery
  id: 1980
  categories:
- JS/JQ
- 前端相关
  date: 2013-06-06 17:54:50

---

网页换肤是一门老技术了，老的现在都不怎么流行了。但是，有时候有些客户就是想要这个换肤功能。于是就实践做了一下网页换肤，结果遇到了很多问题。

## 网页换肤的基本原理

基本原理很简单，就是使用 JS 切换对应的 CSS 样式表。例如导航网站 [Hao123](http://www.hao123.com/) 的右上方就有网页换肤功能。除了切换 CSS 样式表文件之外，通常的网页换肤还需要通过 Cookie 来记录用户之前更换过的皮肤，这样下次用户访问的时候，就可以自动使用上次用户配置的选项。

那么基本工作流程就出来了：访问网页——JS 读取 Cookie ——如果没有，使用默认皮肤——如果有，使用指定皮肤；用户点击换肤选项——JS 控制替换对应的 CSS 样式表——将皮肤选项写进 Cookie 保存。

## 网页换肤事先需要的准备

首先你可能要准备多套 CSS 样式表文件，当点击换肤按钮的是，使用 JS 来切换对应的 CSS 样式表。之后，就是在网页上增加一个 ul li 列表，用 CSS 修饰一下做成换肤选项。例如：

![网页中的换肤选项](https://qxzm-cdn.sapi.work/blog/2013/06/1980/skin0.png)

下面我们就来看具体功能代码。

## 实现点击切换对应 CSS 功能

首先，我们的皮肤选项的 HTML 结构是这样的

<pre>&lt;div class="skin"&gt;
    &lt;ul&gt;
        &lt;li class="skin1 hover"&gt;&lt;/li&gt;
        &lt;li class="skin2"&gt;&lt;/li&gt;
        &lt;li class="skin3"&gt;&lt;/li&gt;
        &lt;li class="skin4"&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;</pre>

然后在网页的顶部偏下的位置放上一个空的 link 标签，我们将会使用 jQuery 为这个 link 标签赋予不同的 CSS 文件实现切换效果

<pre>&lt;link rel="stylesheet" href="" data-href="style-Teal.css" type="text/css" media="screen" class="skincsslittle" /&gt;</pre>

其中，我自定义了一个 data-href 属性来存放系统默认的皮肤，这样当页面加载完成之后，如果 JS 没有检测到 Cookie 中的皮肤信息，就会把 data-href 中的内容赋值上去。之后就是大家熟悉的 jQuery 代码：

<pre>jQuery('.skin li').click(function(){
    var currentClass = jQuery(this).attr('class');
    jQuery(this).siblings().removeClass('hover');
    jQuery(this).addClass('hover');
    var cc = currentClass.substring(0,5);
    cc = convertcsslittle(cc);
    var skincssurl = jQuery('.stylecssurl').attr('href').substring(0,jQuery('.stylecssurl').attr('href').indexOf('style')) + cc;
    jQuery('.skincsslittle').attr("href",skincssurl);

    createCookie('skin',currentClass,365);
});</pre>

大体的逻辑就是获取到当前皮肤的 class 然后截取出来 skin\* 然后通过一个函数得到其对应的 CSS 文件。skincssurl 记载的是网页的非皮肤 CSS 文件，主要用来获取当前网页的 CSS 目录 URL ，最后将混合好的 CSS 皮肤文件赋值准备好的空 link 中，实现换肤。

## 增加 Cookie 记录皮肤功能

这里主要用到两个自定义的函数，用来创建、读取 Cookie 内容。

<pre>function readCookie(name) {
  var nameEQ = name + "=";
  var ca = document.cookie.split(';');
  for(var i=0;i &lt; ca.length;i++) {
    var c = ca[i];
    while (c.charAt(0)==' ') c = c.substring(1,c.length);
    if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
  }
  return false;
}

function createCookie(name,value,days) {
    if (days) {
        var date = new Date();
        date.setTime(date.getTime()+(days*24*60*60*1000));
        var expires = "; expires="+date.toGMTString();
    }
    else expires = "";
    document.cookie = name+"="+value+expires+"; path=/";
}</pre>

你只需要把这两个函数复制到 JS 代码区域即可。在 jQuery 点击换肤的功能代码中，最后一句就创建了一个 Cookie，等网页加载完成之后，我们需要使用 JS 读取 Cookie 内容，然后使用 if 判断：

<pre id="line1">var cccc = readCookie("skin");

if (cccc){
    cccc = cccc.substring(0,5);
    jQuery('.'+cccc).addClass('hover').siblings().removeClass('hover');
    ccc = convertcsslittle(cccc);
    var skincssurl = jQuery('.stylecssurl').attr('href').substring(0,jQuery('.stylecssurl').attr('href').indexOf('style')) + ccc;
    jQuery('.skincsslittle').attr("href",skincssurl);
}else{
    var currentcss = jQuery('.skincsslittle').attr("data-href");
    var currentcssname = currentcss.substring(currentcss.indexOf('style'),currentcss.length);
    currentcssname = defaulttoclass(currentcssname);
    jQuery('.'+currentcssname).addClass('hover').siblings().removeClass('hover');
    jQuery('.skincsslittle').attr("href",jQuery('.skincsslittle').attr("data-href"));
}</pre>

不要被这么乱的代码吓晕了，实际上逻辑很简单，先获取 Cookie 的皮肤值，如果有就为对应的皮肤选项高亮并且转换得到对应的 CSS 皮肤文件赋值。如果没有 Cookie 内容，就将 data-href 属性中记录的值赋值进去。

## 网页换肤的闪烁问题和不完美解决方案

网页换肤中，会遇到闪烁的问题。就是当点击切换按钮的时候，更换颜色或者图片会闪烁一下。或者使用 Cookie 记录之后，用户使用了非默认的皮肤，也会闪烁一下，先出现默认的样式然后再闪烁切换成用户自己选择的样式。

这种影响用户体验的现象肯定要彻底消灭，但是一直没有找到完美的解决方法。因为浏览器默认的是优先渲染 CSS 之后再加载 JS，特别是使用 Cookie 记录的皮肤，先渲染现有的 CSS 之后，JS 才能读取然后切换到皮肤。原理是这样的，跟客户协商之后，客户给出了一个“无闪烁”的换肤效果示例，是 MG12 很早的一款主题。同样的 Cookie 记录等，但是他的作品确实没有闪烁情况。

于是我就查看了他的 JS 代码，没有发现特殊之处，后来才想明白，这种闪烁问题，在图片比较多的网页中效果尤其明显，因为切换的 CSS 需要加载图片需要更多时间。而 MG12 那款主题中，切换的 CSS 文件只是改变了几个 background 颜色，加载速度快到你眼球反应不过来就造成了不闪烁的假象。

不完美解决方案也是有的，点击切换按钮之后的闪烁情况，也是因为要加载图片等，那么我们可以在访问网页的时候，使用预加载技术将其他皮肤图片预加载或者使用 CSS Sprite 技术做成一张大图片。

至于 Cookie 记录闪烁的问题，这是浏览器渲染的硬伤，只能尽量减少换肤需要改变的地方，尽量压缩图片减小体积。然后优先加载没有任何皮肤的基础样式，之后使用 JS 加载默认样式或者读取 Cookie 获取的皮肤选项。这样处理，访问网页的时候会先显示白色或者无颜色，之后直接切换成之前选择的皮肤的颜色，而不会从默认的颜色闪烁变成另一种颜色从而提升一定的用户体验。

如果你在这方面有经验，知道更好的解决闪烁问题的方法，麻烦跟我说一下哈，先谢过了！
