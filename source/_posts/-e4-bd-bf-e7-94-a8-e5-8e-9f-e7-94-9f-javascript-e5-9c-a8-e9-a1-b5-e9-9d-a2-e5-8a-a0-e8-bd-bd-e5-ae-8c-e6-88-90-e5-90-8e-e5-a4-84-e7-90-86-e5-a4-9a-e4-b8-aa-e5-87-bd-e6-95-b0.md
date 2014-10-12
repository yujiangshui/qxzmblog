title: 使用原生 JavaScript 在页面加载完成后处理多个函数
tags:
  - JavaScript
id: 1850
categories:
  - JS/JQ
  - 前端相关
date: 2013-04-01 22:37:08
---

JavaScript 脚本语言的执行，是需要触发的。一般的做法就是在网页中，直接编写几个函数，有的在代码被加载的时候就被浏览器处理，或者使用类似下面的代码来触发实现函数的相关功能。
<pre>&lt;div id="link" onclick="fun()" &gt;&lt;/div&gt;</pre>
上面代码的意思就是，当鼠标点击 id 为 link 的元素的时候，就触发了它的 onclick 事件，然后执行使用 JavaScript 定义的 fun 函数。这样的做法肯定是很不合理的，因为触发操作直接写进了 HTML 结构里面，内容和行为没有隔离开，对日后的二次开发或者修改带来不便。

需要注意的是，当事件处理与对应元素绑定起来的时候，只有在那个元素加载完之后才能进行操作。如果说把处理的脚本放在了 head 区域，浏览器会报错。因为下面的 HTML 元素还没有加载出来，head 中的处理脚本已经被处理了。

一个好的执行 JavaScript 代码的方法应该是 **行为内容分离的**、**在页面加载后处理 **的。所以，处理 JavaScript 代码我们要用到 **监听器 **和** window 对象的 load 事件**。

## 监听器

监听器实际上的功能就是行为与内容分离的。以前需要在 HTML 中加上一些触发事件来触发 JavaScript 的相关函数，而现在直接在 JavaScript 中对某个元素的使用监听器，监听这个元素的事件，如果这个元素被触发了某些事件，在监听器中又定义了这个事件对应的处理函数，那么就会处理这个函数。

W3C 的标准方法叫做 addEventListener ，被IE9，chrome，firefox，opera所支持，写法：
<pre>window.addEventListener('load',function,false);</pre>
早期 IE 中有 attachEvent 方法效果类似：
<pre>window.attachEvent('onload',function);</pre>
使用监听器的方法也很简单，就是先获取页面中的某个元素，然后对这个元素使用监听器，定义监听的事件和对应的事件处理函数，就上文例子：
<pre>document.getElementById('link').addEventListener('click',fun,false);</pre>
关于监听器更加详细的使用说明，请见文末补充资料。

## window.onload 事件

onload 事件只有在整个页面已经完全载入的时候才会被触发，我们将 JavaScript 代码写进 onload 事件中，就可以保证在 HTML 元素被加载完成之后，浏览器才会处理我们的 JavaScript 代码。基础的写法：
<pre>window.onload = function(){
 //code
}</pre>
这样，这个函数里面的 code 会在加载完成之后被处理。但是，这种方法有个缺陷，就是只能用于这一个函数。页面中无法出现多个 window.onload 事件，如果出现了多个 onload 事件，那么后面的内容会覆盖前面的。

那么，我们可以这样做，在一个 window.onload 事件中，写上所有需要加载的函数名，然后在外面定义函数：
<pre>window.onload = function(){
   func1();
   func2();
 }

function func1(){...}
function func2(){...}</pre>
这样做虽然可以，但是很不方便，因为我们需要把所有要加载的函数名都写进去，修改起来就会很麻烦。当然办法肯定是有的，jQuery 就特别提供了很强大的多脚本加载方法，那么原生的 JavaScript 肯定也有办法。

## window.onload 同时处理多个函数

我们需要编写一个处理函数，先看一下代码：
<pre>    function addLoadListener(fn){
        if (typeof window.addEventListener != 'undefined'){
            window.addEventListener('load',fn,false);
        }else if(typeof document.addEventListener != 'undefined'){
            document.addEventListener('load',fn,false);
        }else if (typeof window.attachEvent != 'undefined'){
            window.attachEvent('onload',fn);
        }else{
            var oldfn = window.onload;
            if(typeof window.onload != 'function'){
                window.onload = fn;
            }else{
                window.onload = function(){
                    oldfn();
                    fn();
                };
            }
        }
    }</pre>
简单的来解析一下，这个自定义的 addLoadListener 函数，传递一个 函数名称 作为参数。它首先判断浏览器是否支持相关的 监听器，如果支持 监听器，就使用 监听器 监听 window 对象的 onload 事件，然后处理这个函数。这段代码使用 if 语句判断了所有浏览器的监听事件，是跨浏览器兼容的。

我们把这段代码放在 JavaScript 代码段的最上面，然后在下面定义相关函数，然后使用下面语句来加载 JavaScript 函数了。
<pre>addLoadListener(func);
function func() {...}</pre>
这样，有什么 JavaScript 函数是需要在页面加载完成之后处理的，直接使用 addLoadListener 函数即可，而且可以使用多个。通常来说，所有的 JavaScript 最好都使用 onload 事件加载，以避免意外情况发生。

## 引用和补充资料

*   这段代码来自《JavaScript 精粹（修订版）》 一书
*   [addEventListener 百度百科介绍](http://baike.baidu.com/view/2965912.htm)
*   [addEventListener 和 attachEvent用法](http://parkmy.iteye.com/blog/431306)
*   [道听途说之JavaScript事件监听器](http://www.cnblogs.com/yihai/articles/2234592.html)
*   [javascript中addEventListener方法和removeEventListener方法](http://www.candoudou.com/archives/523)