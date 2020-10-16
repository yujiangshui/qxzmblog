title: DD_belatedPNG 与 unitpngfix 两种解决 IE6 中 PNG 文件透明问题方案横向对比
tags:

- JavaScript
  id: 1641
  categories:
- 前端相关
  date: 2013-02-19 04:45:08

---

虽然 IE6 骂声不断，但是仍然还有不少的市场份额。而在网页中，png 文件体积小、无锯齿、透明度好而被广泛使用。当这两件事情碰在一起，问题就来了，IE6 不支持 png 的透明，它会把透明的部分显示成白色的。

有问题就会有解决方法，可以使用早期 IE6 支持的滤镜来实现透明效果，有些牛人就根据这个原理进行了封装，做成了 JS 来使用。所以，我们只需要调用他们编写 JS 文件即可。在网上有众多解决这种问题的方法和插件，但是实际上目前有这两种方式比较有效，那就是 DD_belatedPNG.js 和 unitpngfix.js 这两种方法。本文就是简单介绍一下使用方法和特点，然后将其进行一个对比。

## DD_belatedPNG.js 方法

DD_belatedPNG.js 这个插件功能非常强大，强大的背后就是复杂的使用方法和体积大小。首先要下载这个 JS 文件，然后引用到页面中，之后就要为其填写配置一些参数。通常要用两个参数，一个是 CSS 选择器，使用这个选择需要处理的层或者图片，另一个是类型，就是这个图片是作为 img 图片还是 background 背景图片来使用的。插件体积的话，压缩版也有 7KB。

知更鸟已经写了一篇比较简单的使用方法：[使用 DD_belatedPNG 让 IE6 支持 PNG 透明图片](http://zmingcx.com/dd_belatedpng-solve-png-images-under-ie6-transparent-application-tutorial.html)

官方的英文版提供了更加详细的教程：[点击这里](http://www.dillerdesign.com/experiment/DD_belatedPNG/)

## unitpngfix.js 方法

unitpngfix.js 这个插件使用起来非常简单，不需要配置什么参数，只需要引入 JS 插件即可。而且非常小巧，只有 2KB，不需要进行任何配置。但是要注意，JS 文件里面还要配置一个小图片地址，这个图片就是一个 1 像素的透明图片，是这个插件必须的素材。所以你需要上传或者在网上找个，然后填写进去。

更加详细的使用方法请看官方页面：[点击这里](http://labs.unitinteractive.com/unitpngfix.php)

上面介绍两种方法的两种方法的使用方法，下面我们从实际应用来对比一下。

## 实践对比测试

介绍的再怎么好，也要通过实践检验。下面就来动手做个 Demo 亲自测试一下使用过程和效果。Demo 页面非常简单，就是一个带有透明 png 背景图片的 div ，并且把背景图片放在了右下角，关键代码：

<pre>div{width:400px;height:400px;margin:20px;background:url(222.png) bottom right no-repeat;border:1px solid #000;}</pre>

打开之后的效果是正常的

[![png 正常效果](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix0.png)](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix0.png)

现在我们启动伟大的经常无条件崩溃的 ieTest ，使用 IE6 来加载这个页面

[![IE6 下 png 文件的出错效果](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix1.png)](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix1.png)

成功的显示出了白色的背景，哦也！

**使用 DD_belatedPNG.js 方法：**先引用 JS 文件，然后设置上属性和参数。具体代码如下：

<pre>&lt;!–[if IE 6]&gt;
&lt;script src="DD_belatedPNG_0.0.8a-min.js"&gt;&lt;/script&gt;
&lt;script&gt;
DD_belatedPNG.fix('div,background');
&lt;/script&gt;
&lt;![endif]–&gt;</pre>

[![DD_belatedPNG 在 IE6 下修正效果](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix2.png)](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix2.png)

刷新之后，成功修正！

**使用 unitpngfix.js 方法：**上传并且设置好小图片，然后引用 JS 文件。具体代码如下：

<pre>&lt;script src="unitpngfix.js"&gt;&lt;/script&gt;</pre>

[![Unitpngfix 在 IE6 下的修正效果](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix3.png)](https://qxzm-cdn.sapi.work/blog/2013/02/1641/pngfix3.png)

但是刷新之后，背景图片却出不来了。当然这个与 IEtest 的不稳定也有关，在原生 IE6 下测试应该不会出现这种情况（未测试），在之前的实际使用中，偶尔会出现这种情况。大部分时候，作为背景图片会跑到左上方，因为 unitpngfix 对 background 的属性支持不太好（官方有提到）。

## 用户体验对比

**DD_belatedPNG.js** 的使用效果比较好，达到了要求，但是使用起来比较繁琐，需要针对性的对要使用的图片添加参数，这样就不便于后期的修改。当然，可以新建一个专用的类，为所有需要处理的图片，添加这个类即可，总体上也是比较方便的。此外体积也稍大。

**unitpngfix.js** 使用起来非常简单，只需要引入这个文件，就可以对页面中所有的 png 图片进行处理。但是对于原图片的 background 属性支持不太好。尤其对 background-position、background-repeat 等属性，容易失效。而且有时不太稳定（未在原生 IE6 下测试）。体积较小。

从效果出发，自然是选择 DD_belatedPNG.js ，但 unitpngfix.js 也是有价值的。如果要你为一个包含很多 png 图片的页面做兼容处理，你是选择使用 DD_belatedPNG.js ，为图片一一添加属性或者把选择器一一填上，还是直接引用一个 unitpngfix.js ，忍受一点效果的缺失？
