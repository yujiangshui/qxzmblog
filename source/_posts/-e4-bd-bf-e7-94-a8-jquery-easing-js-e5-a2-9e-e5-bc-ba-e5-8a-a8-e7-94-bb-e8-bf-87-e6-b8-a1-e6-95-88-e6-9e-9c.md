title: 使用 jquery.easing.js 增强动画过渡效果
tags:
  - jQuery插件
id: 1778
categories:
  - JS/JQ
  - 前端相关
date: 2013-03-03 04:51:32
---

jQuery 提供了一些诸如 show、hide、slideUp、fadeIn 等等动画方法，可以方便的切换元素的显隐。更有强大的自定义动画方法 animate ，可以实现很多动画效果。为了让动画有好的过渡变化过程，官方为这些方法设置 easing 属性，但是官方没有给出很多过渡效果。

jquery.easing.js 这个插件，增加了很多过渡效果，引入之后可以让动画过渡过程更加多样化。

先来看一下：[Demo](http://www.qianxingzhem.com/demo/1778/)。官方也有案例：[打开官方主页](http://gsgd.co.uk/sandbox/jquery/easing/)。

## 如何使用 jquery.easing.js

### 第一步 引入插件

jQuery 插件嘛，当然要先引入 jQuery，然后再引入 jquery.easing.js  。
<pre>&lt;script type="text/javascript" src="http://lib.sinaapp.com/js/jquery/1.7.2/jquery.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="http://gsgd.co.uk/sandbox/jquery/easing/jquery.easing.1.3.js"&gt;&lt;/script&gt;</pre>
然后再在引入代码下面编写调用的 Javascript 代码，注意[代码顺序](http://www.qianxingzhem.com/post-1539.html)。

### 第二步 启用插件

首先先假设使用 animate 方法把网页上的 class 为 aa 的 div 的宽度，从原本的 300px 变成 600px。按照 animate 的写法，加上 easing 。
<pre>$('.aa').animate( {'width':'600'} , { duration:1000,easing:'easeInOutCirc' });</pre>
这样，就对 aa 对象，启用了一个 easeInOutCirc 过渡效果，在 1000毫秒 内变成 600px。

## 可以应用的动画方法

不仅仅支持 animate 方法，还支持 hide、show、slideDown、slideUp、fadeIn、fadeOut等等支持 easing 的动画方法。只需要按照官方对应的格式去写就可以，**这个插件相当于扩充了官方的过渡效果样式**。

## 插件的参数

这个插件有三个参数：**duration**、**easing**、**complete**。

### duration 参数

用来指定动画变化的时间，以毫秒为单位。

### easing 参数

指定这个动画要使用何种过渡样式。具体的过渡样式名和效果，需要在[官方主页上查看左边的 “Example”](http://gsgd.co.uk/sandbox/jquery/easing/)，选择找到自己想要的效果。

### complete 参数

设置一个回调函数，当动画完成之后，执行这个函数。

## 其他注意事项

### 使用 slideUp 动画方法

slideUp 这类的动画方法，要比 animate 简单一些，不需要复杂的属性参数，所以可以直接这样写：

    $(element).slideUp(1000, method, callback});
    $(element).slideUp({ duration: 1000, easing: method, complete: callback});`</pre>
    其他的 hide 、show 之类的方法，自行类比。

    ### 指定默认的 easing 样式

    在使用中 easing 参数是可以省略的，省略之后，就会调用默认的过渡样式。可以使用下面一句代码，指定默认的动画过渡样式。
    <pre>`jQuery.easing.def = "过渡样式名，例如 easeInOutCirc";

用起来挺简单的，但是有了更和谐的变化效果，可以增强用户体验。更多用法欢迎观看[ Demo ](http://www.qianxingzhem.com/demo/1778/)。