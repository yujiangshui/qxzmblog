title: Jquery.lazyload.js究竟要怎么使用
tags:
  - jQuery
  - jQuery插件
id: 1192
categories:
  - 前端相关
date: 2012-08-25 12:06:28
---

Jquery.lazyload.js 这个jquery插件，是用来缓冲加载图片的插件。如果一篇文章很长有很多图片的话，下载图片就需要很多时间。而这款插件，会检测你的滚动情况，只有你要看到那个图片的时候，它才会从后台请求下载图片，然后显示出来。使用这个插件，可以在需要显示图片的时候，才下载图片，所以可以减少服务器的压力，避免不必要的资源下载。一个简单的例子，如果一个人不看下面的图片，那加载下面的图片就是一种浪费。

但是现在，很多javascript大牛分析得出，这个插件其实并没有真正的缓加载效果。确实，官方也已经给出了说明和解决方法了。
<pre>插件原理：修改目标的src属性为orginal属性，从而中断图片的加载。检测滚动状态，然后把视野中的目标src属性还原，制造缓冲加载的效果。
原因：在新版的浏览器中，即使你删除了javascript控制的src属性，浏览器仍然会去加载这个图像。
解决方法：修改html的结构，在img标签中添加新的属性，把src属性的值指向占位图片，添加data-original属性，让其指向真正的图像地址。
例如：&lt;img data-original=“img/example.jpg” src=“img/grey.gif”&gt;</pre>
这样我们就需要判断一下，我们究竟还要不要使用这个插件。

## 使用：

1.  必须按照这种结构才有实际作用，需要对输出进行定义。
2.  可以节约服务器资源，并且有较好的用户体验。
3.  如果图片很大，当用户滚动到目标位置，需要较长时间下载。

## 不使用：

1.  增加服务器压力，浪费系统资源。
究竟使用不使用，还是要看你自己的实际需求。如果你图片比较少，就不必使用了，如果你图片比较多，可以考虑一下。但是，使用的话，你可能需要把每一个img标签上自己加上这个属性，会稍微麻烦一点。潜行者m博客上，就用了这个插件，不过没用使用官方说的那种结构，要的只是一个缓冲加载的效果。

## 如何使用：

如何使用这个插件呢？

第一步：加载相关文件。

很明显，你要加载jquery和这个插件。你可以使用以下代码，加载这几个文件：
<pre>&lt;script src="jquery.js" type="text/javascript"&gt;&lt;/script&gt;
&lt;script src="jquery.lazyload.js" type="text/javascript"&gt;&lt;/script&gt;</pre>
第二步：定义图片结构。

按照官方的建议，定义你的img结构：
<pre>&lt;img class="lazy" src="img/grey.gif" data-original="img/example.jpg" width="640" heigh="480"&gt;</pre>
第三步：触发这个插件，生效。

激活以下，你就可以在目标中使用了。
<pre> $("img.lazy").lazyload();</pre>

## 高级使用方法：

### 更周全的做法

我们不得不思考这样一个问题。我们定义了这样一个结构，那么网页中，就不会加载源图像了。只有当javascript执行，才会显示这个源图像。如果用户的浏览器不支持或者用户关掉了支持javascript的选项，那么我们的这个图像就无法显示出来。也就是说，没有javascript的支持，我们的图像就无法显示出来。

应对这个问题，我们需要引入noscript标签。大体思路如下：用noscript包含真实的图像位置，当浏览器不支持javascript，直接显示图像。对现有图像，隐藏处理，使用show（）方法触发显示。这样，如果浏览器不支持javascript，我们自定义的img就不会出现，而显示noscript里面的图像。具体实现代码如下：
<pre>&lt;img class="lazy" src="img/grey.gif" data-original="img/example.jpg"  width="640" heigh="480"&gt;
&lt;noscript&gt;&lt;img src="img/example.jpg" width="640" heigh="480"&gt;&lt;/noscript&gt;
.lazy {
  display: none;
}
$("img.lazy").show().lazyload();</pre>

### 提前加载

默认的情况是，当你滚动到图片位置的时候，插件开始加载。这样，用户可能首先看到的是一个空白图像，然后再缓慢出现。如果你想在用户滚动之前，提前加载这个图像，你可以配置一下参数。
<pre>$("img.lazy").lazyload({ threshold : 200 });</pre>
threshold这个参数，就是用来提前加载的。上面这个语句的意思是，当距离图片还有200像素的时候，就开始加载图片。

### 自定义触发事件

默认的触发事件，是滚动，当你滚动的时候，就会检查然后加载。你可以使用event属性，设置你自己的加载事件，之后你可以自定义触发这个事件的条件，然后去加载图像。
<pre>$("img.lazy").lazyload({ 
    event : "click"
});</pre>

### 自定义显示效果

默认的图片实现效果，就是没有效果，下载完成之后，直接显示出来。这样的用户体验并不好，你可以设置effect属性，来控制显示图片的效果。例如
<pre>$("img.lazy").lazyload({ 
    effect : "fadeIn"
});</pre>
fadeIn的效果就是，改变图片的透明度，渐现的方式出现。效果： [effect demo page](http://www.appelsiini.net/projects/lazyload/enabled_fadein.html)

### 把图像插入某个容器

大家如果使用智能手机的话，经常去应用网站下载应用，他们通常使用一个横着的容器，放一些手机截图。使用container属性，能很轻松在容器中实现缓冲加载。首先，我们需要用css定义这个容器，然后用这个插件进行加载。效果： [vertical](http://www.appelsiini.net/projects/lazyload/enabled_wide_container.html)
<pre>#container {
    height: 600px;
    overflow: scroll;
}</pre>
<pre>$("img.lazy").lazyload({         
     container: $("#container")
});</pre>

### 加载不可见图像

有部分图像是不可见的，我们对其加上类似display：none等属性的图像。默认的情况下，这个插件是不会加载隐藏的不可见图像。如果我们需要它加载不可见图像，我们需要使用skip_invisible属性，对其赋予false
<pre>$("img.lazy").lazyload({ 
    skip_invisible : false
});</pre>
官方说明：http://www.appelsiini.net/projects/lazyload