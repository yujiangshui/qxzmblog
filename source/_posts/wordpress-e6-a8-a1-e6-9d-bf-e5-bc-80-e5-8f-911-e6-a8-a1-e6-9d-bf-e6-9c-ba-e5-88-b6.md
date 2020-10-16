title: wordpress 模板开发 1——模板机制
tags:

- wp 主题制作教程
  id: 520
  categories:
- 网站与后台开发
  date: 2012-02-08 23:21:46

---

经过前面第一篇的介绍，相信你对于 wordpress 模板制作有一点简单的了解。今天，潜行者 m 带着你正式进入 wordpress 模板开发，在这里，潜行者 m 认为你已经对 html、css 等已经有了基础，因为任何的模板都离不开 html 和 CSS 去设计，如果你对这两个词还很陌生的话，建议你先去学习这两个东西，之后再来学习，不然看也看的一脸茫然。

进入正题，每套成熟的网站系统，都有自己的模板机制，我们要是想制作模板，就必须按照这个网站系统的模板机制来制作。首先先来介绍一下 wordpress 模板最标准的文件目录，也就是说，一个标准的 wordpress 模板，应该包含一下文件：

**index.php** 显示网站首页（就是你一打开看到的）
**header.php**头部文件
**sidebar.php**边栏文件
**footer.php**底部文件
**single.php** 显示博客文章页面（打开一篇文章看到的）
**page.php** 显示静态页的页面内容（打开一个页面看到的）
**category.php**显示分类页的页面（相当于栏目页）
**archive.php** 显示存档页的页面（相当于按时间归类的栏目页）
**search.php** 显示搜索结果的页面（搜索之后，显示搜索结果）
**comments.php** 显示评论的页面
**comments-popup.php** 显示弹出式评论的页面
**404.php** 显示 404 错误信息的页面(如果网站出现 404 错误显示的页面）
**style.css** 控制页面布局外观（博客全局样式表）

如果一个符合规范标准的 wordpress 模板，就应该包含以上文件。下面，我就来介绍 wordpress 的模板机制：

**1，模板自动代替机制。**我们可以随便打开一个 wordpress 模板，可以看到模板文件夹下面有很多以 PHP 为后缀的文件。两个不同的模板，可能都有 index.php 文件，也有可能其中一个模板没有 404.php 文件，另一个模板有。从上面，我们知道，不同的页面有不同的功能，如果我们缺少了某个页面，为什么还能正常运作？这就是模板自动代替机制的功能，简单的说，wordpress 模板文件分为不同的等级，最核心的文件就是 index.php 和 style.css 这两个文件。如果其他文件不存在，就以 index.php 作为当前页面的模板。例如：我们想看一篇文章，就需要调用 single.php 文件，作为文章的模板。但是我们没有编写 single.php 这个模板，那么 wordpress 系统模板机制就会向上寻找上一级的 index.php 文件作为显示文章的模板。大家可以看下图：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/wpstruct.png "wpstruct")](https://qxzm-cdn.sapi.work/blog/2012/02/wpstruct.png)

这就是文件等级结构，如果下面的文件有缺损，就会找到上面的文件替换。这样，我们制作模板的过程就很明确了。就是设计 index.php 文件就可以了，只要有一个 index.php 文件，再加上定义样式的 style.css 文件，就成了一个简单的 wordpress 模板。

**2，文件分割机制。**[一个博客](http://www.qianxingzhem.com)，有文章页面，有 Page 页面，还有分类目录页面，日期存档页面等。这些都可以算是相对独立的功能模块，所以 wordpress 要求对 index.php 进行分割，然后修改设计出不同功能模块的模板。比如文章页面，就需要显示全部文章，而不能仅仅像首页那样显示文章摘要等。此外，wordpress 模板系统把整套模板从大的方面划分成四个模块，即：**头部，主体，边栏，底部**。因为一个博客网站，头部，边栏，底部都相对稳定，可以重复使用，而重点变化的就是主体。主体可以是文章，可以是分类目录下的文章列表，可以是错误的 404 提示等，但是网站主要风格是不变的，所以头部、边栏、底部一般不会变化，于是就划分出这四个部分。之后，在原本的地方加上 wordpress 函数来引用文件，例如：&lt;?php get_header(); ?&gt;表示将 header.php 文件内容包含进当前页面。一个标准的结构如下图：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/bodystruct.png "bodystruct")](https://qxzm-cdn.sapi.work/blog/2012/02/bodystruct.png)

例如本人的博客模板，就是使用了这个标准的结构：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/myblog.png "myblog")](https://qxzm-cdn.sapi.work/blog/2012/02/myblog.png)

这两个模板机制，在其他成熟的网站系统中，同样适用，而 wordpress 是比较简单的应用。正是这样，掌握了 wordpress 模板开发，理解了模板开发的流程，再去开发其他系统的模板就变得非常简单。

通过上面两个模板机制的介绍，我们可以彻底的了解 wordpress 模板制作过程：**使用 html+css 设计出 index.php 和 style.css**——&gt;&gt;**将 index.php 文件分割成头部(header.php)、边栏(sidebar.php）、底部(footer.php)**——&gt;&gt;**设计文章显示页面(singel.php)、分类列表页面(category.php)等细节页面，并且在每个页面上相应地方加上类似&lt;?php get_header(); ?&gt;的函数，将头部、边栏、底部内容包含进来，在需要内容的地方加上相应的 wordpress 调用函数**——&gt;&gt;**观察调试，修改需要修改的地方**——&gt;&gt;**制作完成！**

在这里，说起来很简单，但是做起来比较难。在后面的教程中，我会根据上面的流程一步一步的教大家如何制作出一套自己的 wordpress 模板。认真学习看完这系列文章之后，你至少会制作出像我的博客这样简单的模板。因为我就是按照这个过程一步一步制作的。

&nbsp;
