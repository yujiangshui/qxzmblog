title: 在主题中添加 AdminBar 功能
tags:

- WP 主题函数
  id: 1297
  categories:
- 网站与后台开发
  date: 2012-09-24 12:34:48

---

首先，你必须的知道，什么叫做 AdminBar 。这是 WordPress 中的一个非常方便的功能，当管理员或者有管理权限的用户访问页面的时候，就会看到最上面有一个黑色的条条，上面有各种快捷链接。

[![adminbar](https://qxzm-cdn.sapi.work/blog/2012/09/Unnamed-QQ-Screenshot20120924122559.jpg "adminbar")](https://qxzm-cdn.sapi.work/blog/2012/09/Unnamed-QQ-Screenshot20120924122559.jpg)

不知道为什么，竟然还有很多人写如何去掉这个功能。但是很少有人写如何增加这个功能。

这个功能需要增加？对，没错。在早期我制作主题的时候，就出现了没有 AdminBar 的情况。要想在主题中，增加这个功能，必须要用到两个函数：

<pre>&lt;?php wp_head(); ?&gt;、&lt;?php wp_footer(); ?&gt;</pre>

这两个函数，是实现 WordPress 中某些功能而使用的。例如本文写的 AdminBar 的功能，就是使用这两个函数。新手制作主题的时候，往往会看到或者使用到 wp_head() 这个函数，但是会忽视 wp_footer() 这个函数。所以，AdminBar 不会显示，但是会空出那么高的高度。

这两个函数的位置也需要注意。

- wp_head() —— 通常放在&lt;/head&gt;上面的一行
- wp_footer() —— 通常放在最下面的&lt;/body&gt;的上面一行
  只有准确放置了这两个函数，AdminBar 才会出现。

<span style="color: #ff0000;">注意：</span>

忽略了一个地方，在现在的版本中，用户可以自定义在浏览博客的时候，是否显示最上面这个工具条。在 “用户”-》“我的个人资料” 中可以设置。在以前的版本中，记得好像没有这个选项。感谢 “[鬼娃娃](http://www.linyousai.cn/)” 提醒。
