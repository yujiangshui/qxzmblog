title: WordPress 自定义菜单功能介绍和使用详解
tags:

- WP 主题函数
  id: 1521
  categories:
- 网站与后台开发
  date: 2012-11-02 22:10:52

---

一个常规的网站，一般都会有一个网站导航。这里的导航，通常包含网站的栏目、特殊的页面等等。对于一个博客来说，有的时候也需要一个这样的导航。如果仅仅是调用 文章分类 或者 页面链接 作为导航的话，会比较难控制，无法自由的添加链接等。当然，成熟的 WordPress 系统已经为我们考虑到了这一点，添加了一个 “自定义菜单” 功能。使用这个功能，可以在 **后台 -》 外观 -》 菜单** 中编辑，当然最好前提是你使用的主题支持这一个功能。

## 自定义菜单功能介绍

当我们在后台打开 “菜单” 的时候，通常会看到类似这样的界面：

[![](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan0.png "后台设置 自定义菜单")](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan0.png)

没有配置之前，是无法使用的。我们需要先输入一个 菜单名称 才能继续使用。这里的菜单名称，仅仅作为一个关联数据用的标记，所以可以随便起名。完成之后，左边的区域就可以配置使用了。

如果你的主题不支持 自定义菜单 功能，那么左边的 主题位置 面板会提示你，这个自定义菜单的选项将会在 边栏 中显示。如果主题支持 自定义菜单 功能，那么这个面板则会提示有支持几个自定义菜单、自定义菜单的名称（需要定义）是什么。

[![](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan1.png "设置面板")](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan1.png)

上面提示，有一个自定义菜单，并且名称为 topnav 。现在，我要制作这个 自定义菜单 的内容。在左边有三个面板：分类目录、自定义链接、页面。里面包含着你当前博客里面的相关数据。

[![](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan2.png "主题位置 面板")](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan2.png)

我们只需要勾选相应的内容或者直接拖动到右边的刚刚设置的菜单面板中即可。

[![](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan3.png "定义菜单")](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan3.png)

注意的是，可以通过拖动改变显示顺序，而且还可以修改显示的名称。所以说，这个功能非常的强大而且灵活。这样，一个导航链接就做好了。

[![](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan4.png "导航做好了")](https://qxzm-cdn.sapi.work/blog/2012/11/1521/caidan4.png)

下面来详细讲解如何在主题中，添加这个功能。也很简单，只需要在两个地方，添加两小段代码即可！

## 在主题中添加函数调用

首先，你需要在主题的 functions.php 文件中，声明一下存在这个功能。只需要添加下面一段代码即可：

<pre>if(function_exists('register_nav_menus')){
    register_nav_menus( array(
        'header-menu' =&gt; __( 'topnav' )
    ) );
}</pre>

这段代码首先判断是否支持这个功能，然后注册一个 自定义菜单，并且我指定了一个参数，即这个自定义菜单的名称为 topnav。也就是上面在 主题位置 面板中看到的自定义菜单名称。下面引用官方的资料详细的介绍一下 [register_nav_menus](http://codex.wordpress.org/Function_Reference/register_nav_menus) 这个函数。

实现这个功能有两个函数 <tt>[register_nav_menu](http://codex.wordpress.org/Function_Reference/register_nav_menu "Function Reference/register nav menu")</tt> 和  [register_nav_menus](http://codex.wordpress.org/Function_Reference/register_nav_menus) 顾名思义，第一个函数用于创建一个自定义菜单，第二个函数用于创建多个自定义菜单。所以通常使用第二个就好了。下面也是根据第二个函数进行讲解。

介绍就不多说了，使用方法也很简单，只需要传递一个 数组 即可。

    &lt;?php register_nav_menus( $locations ); ?&gt;

这个数组是必选参数，记录着 位置标记（键名） 和 位置描述（键值）。例如：

<pre>register_nav_menus( array(
	'header-menu' =&gt; __( 'topnav' )，
	'footer_menu' =&gt; 'My Custom Footer Menu'
) );</pre>

上面的语句，定义了两个自定义菜单，它们的标记（可以随便起）分别为：header-menu、footer_menu。它们后面对应的描述，将会显示在后台的 主题位置 面板上，供你选择。在  'header-menu' =&gt; **( 'topnav' ) 这句代码中，我加了**() 这个函数，它是用于跨语言翻译用的，与这个功能无关。

之后，在主题中添加自定义菜单。在主题中合适的位置，添加下面的函数：

<pre>&lt;?php wp_nav_menu( array( 'theme_location' =&gt; 'header-menu' )); ?&gt;</pre>

这句代码使用了 [wp_nav_menu](http://codex.wordpress.org/Function_Reference/wp_nav_menu "Function Reference/wp nav menu") 函数。这个函数也是传递一个数组作为参数，但是这个数字里面的键名比较多。下面根据官方文档的说明选择几个重要的做了一个简单的翻译：

<pre>&lt;?php $defaults = array(
	'theme_location'  =&gt; '',
	'menu'            =&gt; '',
	'container'       =&gt; 'div',
	'container_class' =&gt; 'menu-{menu slug}-container',
	'container_id'    =&gt; '',
	'menu_class'      =&gt; 'menu',
	'menu_id'         =&gt; '',
	'echo'            =&gt; true,
	'fallback_cb'     =&gt; 'wp_page_menu',
	'before'          =&gt; '',
	'after'           =&gt; '',
	'link_before'     =&gt; '',
	'link_after'      =&gt; '',
	'items_wrap'      =&gt; '&lt;ul id="%1$s"&gt;%3$s&lt;/ul&gt;',
	'depth'           =&gt; 0,
	'walker'          =&gt; ''
); ?&gt;

&lt;?php wp_nav_menu( $defaults ); ?&gt;

'theme_location'  =&gt; 可选，值为之前在functions.php中 register_nav_menus 传递的数组参数中的键名，进行绑定。默认：无
'container'       =&gt; 可选，决定是否要对生成的 自定义菜单（ul） 进行包裹，以及使用什么包裹。如果不需要，传递参数 false。默认：div
'container_class' =&gt; 可选，为上面包裹的容器添加 class 属性。下面的 container_id 功能类似。
'before'          =&gt; 可选，在输出的列表中的 a 标签之前添加文本信息。after 功能类似。
'link_before'     =&gt; 可选，在输出的列表中的链接文字前面加上文字（注意与上面的区别）。link_after 功能类似。
'items_wrap'      =&gt; 可选，设置包裹自定义菜单的标签形式。默认：&lt;ul id="%1$s"&gt;%3$s&lt;/ul&gt;，通常不要修改 。</pre>

这样，刚刚我添加的那一句代码的意思很明确了，就是在这里调用名为 header-menu 的自定义菜单位置。而这个自定义菜单位置的名称为 topnav，在 WordPress 后台中，我新建了一个名为 “顶部导航” 的菜单，然后与这个 topnav 进行了关联。那么这句代码就调用了我设置的 “顶部导航” 菜单的内容。

我们不仅仅可以用它来做导航，还可以像上面那样，在多个位置添加多个自定义菜单。例如可以在底部加一个自定义菜单，这样在后台就可以设置底部的链接等等。功能非常强大，不过需要注意一点，WordPress 目前的较新版本 3.4.2 被爆出一个 BUG ，不支持 自定义菜单。当然很快就出了补丁。如果你使用 3.4.2 版本的时候，自定义菜单无法使用，可以自行[搜索一下解决方法](http://www.baidu.com/s?tn=monline_4_dg&ie=utf-8&bs=wordpress+%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95+3.4.2&f=8&rsv_bp=1&wd=wordpress+3.4.2++%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95+&rsv_sug3=4&rsv_sug=1&rsv_sug1=2&rsv_sug4=249&rsv_n=2&inputT=5575)。

<div><embed id="ciba_grabword_plugin" width="0" height="0" type="application/ciba-grabword-plugin" hidden="true" /></div>
