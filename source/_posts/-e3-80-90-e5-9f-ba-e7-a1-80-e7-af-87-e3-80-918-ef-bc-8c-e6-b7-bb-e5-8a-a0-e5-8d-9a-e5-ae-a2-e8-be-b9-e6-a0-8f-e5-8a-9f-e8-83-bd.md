title: 【基础篇】8，添加博客边栏功能
tags:
  - wp主题制作教程
id: 1556
categories:
  - 网站与后台开发
date: 2012-11-18 17:44:58
---

通常的博客都有边栏功能，边栏通常放置文章分类、友情链接等等信息。本节课讲解如何添加博客的边栏相关功能。在 WordPress 系统中，不得不提到的一个强大的功能，那就是 “小工具” ，即在后台中，找到 “外观” 选项下面的 “小工具”。当一款主题支持小工具的时候，我们只需要配置一下小工具，把需要的模块拖动进去，就可以在博客中显示出来。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar0.png "WordPress 小工具")](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar0.png)

对于初学者来说，本文暂时不讲解复杂的边栏相关的函数使用，而是直接介绍如何为主题添加“小工具”这个功能的支持。这样就可以实现快速定义博客的边栏。

为主题添加小工具功能，需要两个步骤：1，**在 functions.php 文件中声明注册这个功能**。2，**在主题模板的相应位置，添加对边栏的调用**。

## 在 functions.php 文件中声明这个功能

需要用到 [register_sidebar](http://codex.wordpress.org/Function_Reference/register_sidebar) 这个函数。这个函数用于注册一个边栏小工具，当然还有一个函数 [ register_sidebars ](http://codex.wordpress.org/Function_Reference/register_sidebars "Function Reference/register sidebars")与之类似，但是可以注册多个边栏小工具。但是如果你想在主题中，加入多个边栏小工具，我更推荐的是 [ register_sidebar](http://codex.wordpress.org/Function_Reference/register_sidebars "Function Reference/register sidebars") 函数，因为它可以自己定义更多的输出信息，注册多个，只需要复制几遍即可，更加灵活。

下面介绍一下这个函数的相关参数：
<pre>'name'          =&gt; __( 'Sidebar name', 'theme_text_domain' ),
'id'            =&gt; 'unique-sidebar-id',
'description'   =&gt; '',
'class'         =&gt; '',
'before_widget' =&gt; '&lt;li id="%1$s"&gt;',
'after_widget'  =&gt; '&lt;/li&gt;',
'before_title'  =&gt; '&lt;h2&gt;',
'after_title'   =&gt; '&lt;/h2&gt;' );</pre>

*   **name**：设置这个边栏的名称，在之后的主题中的数据调用中，会用到这个名称。
*   **id** ：用于在 WordPress 内部对这个特定的边栏小工具进行标记，必须是唯一的值，同主题不能有两个相同的 id。
*   **description**：这个边栏小工具的描述，填写之后，在后台小工具选项配置的时候，可以看到当前工具的描述。
*   **class**：当前边栏小工具在生成的时候，在 HTML 结构中，加入的 class 属性，这样可以自定义接口，方便 CSS 对其样式的控制。
*   **before_widget**：在小工具生成的内容前面加上什么？默认加上 li 标签。
*   **after_widget**：同上。
*   **before_title**：在后台小工具设置中，添加小工具之后，可以设置小工具的标题，这个属性是为设置的标题包裹什么标签？默认 h2.
*   **after_title**：同上。
这个函数还是比较简单的，参数也都容易理解。那么在主题中，想声明一个边栏，就可以编写下面代码：
<pre>if ( function_exists('register_sidebar') ){ //先判断当前 WordPress 是否支持边栏小工具功能
    register_sidebar(array( //以数组的方式，传递参数
    'name' =&gt; '小工具',
    'id' =&gt; 'sidebar1',
    'description' =&gt; '拖动小工具会在边栏显示出来',
));
}</pre>
你也可以编写更多的参数，例如制定元素包裹的标签等等，但是在这里，为了演示，其他属性均保持默认。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar1.png "添加 小工具 声明代码")](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar1.png)

添加到 functions.php 文件之后，我们登录后台会发现小工具已经可以用了，并且显示出来了设置的信息。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar2.png "配置小工具功能")](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar2.png)

这时，我们就可以把左边的内容拖动到右边去，即可显示出相应的功能。例如拖动“搜索”会生成一个搜索框，拖动“链接”会生成一个有情链接列表。但是刷新主题之后，并没有出现，因为这时候我们还没有在主题中调用这个边栏数据。

## 在主题中调用边栏数据

声明完成之后，我们找到主题，在相应的位置使用 下面一句代码即可调用某边栏数据：
<pre>&lt;?php if ( !function_exists('dynamic_sidebar') || !dynamic_sidebar('小工具') ) : ?&gt;&lt;?php endif; ?&gt;</pre>
这句代码的意思就是：首先检测是否存在边栏小工具功能，如果存在，检测是否有 “name” 为 “小工具” 的小工具。如果有（即在 functions.php 声明过了）就调用它的数据。即后面的单引号中的内容，就是在 functions.php 文件中声明的 sidebar 的 name 参数值。

在本系列教程的演示主题 myTheme 中，我们需要添加到 id 为  sidebar 的元素中，添加在下面。要注意的是，由于采用了默认的参数，所以每个小工具将会以 li 标签标记，为了符合 W3C 的标准，我们需要在外面加上 ul 标签。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar3.png "配置小工具")](http://qxzm-img.b0.upaiyun.com/blog/2012/11/1556/sidebar3.png)

在后台拖动小工具到边栏，配置一下，然后刷新首页就可以看到添加好的小工具内容了。这样，我们的边栏功能就实现了。

## 为主题添加多个小工具功能

再扩展的多说一些。小工具这个功能非常的使用，而且功能很多。我们可以在主题中添加多个小工具功能，这样修改主题的相关内容，直接在后台编辑小工具即可。例如：在底部添加小工具功能，想修改底部版权文字等，直接通过后台小工具进行编辑就可以了。

前面也说过，添加多个小工具可以使用  [ register_sidebars ](http://codex.wordpress.org/Function_Reference/register_sidebars "Function Reference/register sidebars") 但是我更推荐的是复制多遍 [register_sidebar](http://codex.wordpress.org/Function_Reference/register_sidebar) 这个函数，因为它可以对每个边栏都进行描述，让别人更容易看懂。

我们只需要把上面的代码，复制一遍：
<pre>if ( function_exists('register_sidebar') ){ 
    register_sidebar(array( 
    'name' =&gt; '小工具',
    'id' =&gt; 'sidebar1',
    'description' =&gt; '拖动小工具会在边栏显示出来',
));
   register_sidebar(array( 
    'name' =&gt; '底部',
    'id' =&gt; 'footer',
    'description' =&gt; '这里是底部的小工具',
));
}</pre>
然后重新配置一下参数，特别要注意的是，name 和 id 一定不能和其他小工具相同，否则会产生数据调用冲突。之后像上面一样，在相应的位置，加上调用代码即可，当然要修改后面单引号里面的内容为要调用数据的 name 参数值。

## 本节课相关资源下载

[myTheme(基础篇-8) 主题下载](http://pan.baidu.com/share/link?shareid=133909&amp;uk=706095745)

## 本系列文章

1.  [开始执行的wordpress主题教程计划](http://www.qianxingzhem.com/post-1235.html)
2.  [【基础篇】1、学习制作主题之前的准备](http://www.qianxingzhem.com/post-1247.html)
3.  [【基础篇】2、WordPress的主题机制](http://www.qianxingzhem.com/post-1251.html)
4.  [【基础篇】3、设计制作你的HTML主题文件](http://www.qianxingzhem.com/post-1259.html)
5.  [【基础篇】4、安装主题文件](http://www.qianxingzhem.com/post-1268.html)
6.  [【基础篇】5、制作主题的头部区域](http://www.qianxingzhem.com/post-1304.html)
7.  [【基础篇】6，使用主循环调用显示日志摘要等数据](http://www.qianxingzhem.com/post-1502.html)
8.  [【基础篇】7，制作博客的搜索模块](http://www.qianxingzhem.com/post-1551.html)