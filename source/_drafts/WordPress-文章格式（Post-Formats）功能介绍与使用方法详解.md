title: WordPress 文章格式（Post Formats）功能介绍与使用方法详解
tags:
  - WP主题函数
id: 1743
categories:
  - 网站与后台开发
---

众所周知，在 WordPress 中，有两种内容模式：**文章、页面**。文章就是一些文章，页面通常用来放置比较静态的内容。但是这两种形式实在是太普通，无法满足用户更多的个性需求。所以在 WordPress 3.1 的版本中出现了这个新功能，增强了文章类型。这个功能主要用来定义多种类型的文章，从而方便进行修饰等。

使用这个功能，可以新增：**aside、gallery、link、image、quote、status、video、audio、chat** 这九种文章格式。为主题增加这个功能之后，在发布文章之后，就可以选择这几个文章格式中的一个。不同的文章格式，有它们自己的特点和标示，可以让你很方便的使用 CSS 来定义，这样就丰富了博客的功能，增强了用户体验。

简而言之，在支持这个功能的主题中，博主可以从类型列表中选择一个类型来展示要发表的文章外观。

九种文章格式的特点和功能

不同的文章类型对应着不同的文章输出样式，下面就来一一介绍：

*   **aside** - 没有标题的传统文章形式。
*   **gallery** -图集类型。文章将会包含图片附件，并像图集那样展示出来。
*   **link** - 链接类型。有时候文章只想放一个链接，引导人们去观看，就用这种类型。
*   **image** - 图片类型。文章中的第一个&lt;img /&gt;标签引用的图片将会显示在这里。此外，如果文中只包含了一个链接，那么就为这个图片加上这个 链接。注意，与图集不同，这个类型只获取一个图片。
*   **quote** - 引用类型。通常在引用类型中包含一个 blockquote 。此外，引用也可以是正文内容，在标题中显示内容的来源或作者。
*   **status** - 状态类型。一段短文字，就想微博那样。
*   **video** - 视频类型。获取文中第一个 &lt;video /&gt; 或者 object/embed 引用的视频文件显示出来。如果文章只有一个连接，就会当做视频地址。
*   **audio** - 音频类型。显示一个音乐播放形式，可以用作播客。
*   **chat** - 聊天形式。
注意：当编写或者编辑文章的时候，如果遇到没有声明过的文章格式，就会采用“标准文章格式”。

文章格式相关功能函数列表

主要函数：

*   [ set_post_format()](http://codex.wordpress.org/Function_Reference/set_post_format "Function Reference/set post format")
*   [ get_post_format()](http://codex.wordpress.org/Function_Reference/get_post_format "Function Reference/get post format")
*   [ has_post_format()](http://codex.wordpress.org/Function_Reference/has_post_format "Function Reference/has post format")
其他函数：

*   [ get_post_format_link()](http://codex.wordpress.org/Function_Reference/get_post_format_link "Function Reference/get post format link")
*   [ get_post_format_string()](http://codex.wordpress.org/Function_Reference/get_post_format_string "Function Reference/get post format string")
关于函数的更加详细功能，请自行打开文档查看。在下面的实现中，会介绍到主要函数的主要功能。

为主题添加文章格式功能

增加主题支持

首先要在 functions.php 文件中使用 [add_theme_support()](http://codex.wordpress.org/Function_Reference/add_theme_support "Function Reference/add theme support") 函数通过一个数组告诉 WordPress 你的主题支持哪些格式。用法：
<pre>add_theme_support( 'post-formats', array( 'aside', 'gallery' ) );</pre>
增加文章类型支持

在 functions.php 文件中使用 [add_post_type_support()](http://codex.wordpress.org/Function_Reference/add_post_type_support "Function Reference/add post type support") 函数声明支持哪种文章格式，例如：
<pre>// add post-formats to post_type 'page'
add_post_type_support( 'page', 'post-formats' );

// add post-formats to post_type 'my_custom_post_type'
add_post_type_support( 'my_custom_post_type', 'post-formats' );</pre>
&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;