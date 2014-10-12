title: wordpress中bloginfo()函数详解
tags:
  - WP主题函数
id: 364
categories:
  - 网站与后台开发
date: 2012-01-19 12:56:45
---

bloginfo()函数，顾名思义，是用来显示博客相关信息的函数。常用的有如下几种：

**&lt;?php bloginfo('name'); ?&gt;** 输出博客名称，例如“潜行者M”，在后台设置常规里面可以设置；
**&lt;?php bloginfo('stylesheet_url'); ?&gt;** 输出模板style.css文件的地址，使用如下语句来加载模板的css样式表：&lt;link rel="stylesheet" href="&lt;?php bloginfo('stylesheet_url'); ?&gt;" type="text/css" media="screen" /&gt;；
**&lt;?php bloginfo('url'); ?&gt;** 输出博客的网址，在后台设置常规里面可以设置；
**&lt;?php bloginfo('template_url'); ?&gt;** 输出博客模板的位置；
**&lt;?php bloginfo('rss2_url'); ?&gt;** 输出博客RSS2.0 feed地址；
**&lt;?php bloginfo('charset'); ?&gt;** 输出博客所采用的编码；
**&lt;?php bloginfo( 'description' ); ?&gt;** 输出博客的描述，即副标题，在后台设置常规里面可以设置。

此外，与此函数相近的函数有get_bloginfo()，它的用法与此函数相同，区别在于get_bloginfo()函数用来输出到变量中。
用法：**&lt;?php $bloginfo = get_bloginfo( $show ); ?&gt;**更多的用法请参考：
http://www.wordpress.la/codex-%E6%A8%A1%E6%9D%BF%E6%A0%87%E7%AD%BE-bloginfo%28%29.html

此外，本人总结了一些[ wordpress模板开发常用的函数](http://www.qianxingzhem.com/post-354.html)

本人正在写wordpress模板制作教程，详情可以查看：[wordpress模板开发](http://www.qianxingzhem.com/post-tag/wp%E6%A8%A1%E6%9D%BF%E5%BC%80%E5%8F%91)