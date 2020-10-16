title: wordpress模板开发3——制作博客首页（index.php）
tags:
  - WordPress
id: 777
categories:
  - 网站与后台开发
---

===============================================================

注意:本文只是一篇未完成的草稿,并且不打算更新,但是里面有些资源需要保留,所以发布出来

===============================================================

当我们已经准备完开发环境之后，我们就要来开始制作模板了。与其他有关wordpress教程不同，我的制作流程是，先制作index.php和style.css，把整体的网站风格确定下来，之后，再进行模块的分割，对于不同的页面，添加不同的功能。

现在，你应该使用html和css做出自己的网站风格。下面是我为大家做的一个简单的html首页模板图，由于作为教程演示使用，非常简洁简单。如果没有制作的朋友，可以在文章后面，下载这个文件。先看一下页面的大体布局（为了方便，我把所有的div都加上了虚线）：

[![index](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index8.jpg)

这个简单的模板中，包含了一个普通博客必须的元素，本套教程就以此为例。

制作完成的模板风格是有两个文件的，分别是index.html和style.css，下面，我们把index.html重命名为index.php放进wordpress网站模板目录下的一个新建文件夹mytheme中。在wordpress的wp-contentthemes目录中，新建一个文件夹表示新建了一个模板，我们把这两个文件放进去。

[![index1](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index1_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index11.jpg)

之后，我们登陆wordpress后台，设置模板为mytheme。

[![index2](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index2_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index21.jpg)

我们点击启用之后，wordpress模板就开始使用这套模板了，我们访问主页就可以看到你刚刚设计的模板的内容了。结果出现问题了，访问之后全部变成乱码了。

[![index3](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index3_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index31.jpg)

这在开发中，是经常出现的常见问题，原因就是编码不同造成的。我编写这个页面使用的是dreamweaver，它默认的网页编码是GB2312，而我这个博客使用的编码却是utf-8这样，就成了乱码。我们需要修改一下网页的编码以及模板文件的编码。

1，修改网页的编码，可以打开网页文件，在最上面的&lt;meta&gt;标签中，把&lt;meta http-equiv="Content-Type" content="text/html; charset=gb2312" /&gt;中的gb2312改成utf-8。这样还不行，我们还得修改文件的编码。

2，用文本编辑器打开文件，另存为，在编码中选择“utf-8”。保存即可，可以看下图：

[![index4](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index4_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index41.jpg)

这样，我们的模板首页就算是正常了

[![index5](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index5_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index51.jpg)

我之所以拿出一定的篇幅来介绍这个问题的解决方法，是因为这个问题比较常见，此外还想说明一点，在模板开发的过程中是会出现很多意外的问题，对于这些问题都得一个一个仔细认真的解决。

我们通过访问主页发现，我们原先设计的样式都失效了，为什么？可以这样说，我们设计的style.css是放在模板文件的根目录下，当wordpress程序读取使用模板的时候，根目录就变成了wordpress的根目录，wordpress的根目录是没有我们模板的样式表文件的，所以就找不到样式表了。要使样式表工作，我们就要在index.php中，把原先引用样式表的代码

&lt;link rel="stylesheet" media="all" href="style.css" /&gt;

更换成

&lt;link rel="stylesheet" type="text/css" media="all" href="&lt;?php bloginfo( 'stylesheet_url' ); ?&gt;" /&gt;

这里，就涉及到wordpress模板制作函数了，这是wordpress模板制作中，最重要的部分。上面代码中，用了&lt;?php bloginfo( 'stylesheet_url' ); ?&gt;这一句php代码，其中用了wordpress中的bloginfo();函数，bloginfo( 'stylesheet_url' ); 通过这一句，就调用了对应模板的style.css文件。我们修改完成之后，再来看看我们的首页

[![index6](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index6_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index61.jpg)

这样就显示正常了。刚刚上面提到了bloginfo();函数，我写过一篇文章，介绍了这个函数的详细应用，现在在下面贴出来：

**&lt;?php bloginfo(‘name’); ?&gt;** 输出博客名称，例如“潜行者M”，在后台设置常规里面可以设置；
**&lt;?php bloginfo(‘stylesheet_url’); ?&gt;** 输出模板style.css文件的地址，使用如下语句来加载模板的css样式表：&lt;link rel=”stylesheet” href=”&lt;?php bloginfo(‘stylesheet_url’); ?&gt;” type=”text/css” media=”screen” /&gt;；
**&lt;?php bloginfo(‘url’); ?&gt;** 输出博客的网址，在后台设置常规里面可以设置；
**&lt;?php bloginfo(‘template_url’); ?&gt;** 输出博客模板的位置；
**&lt;?php bloginfo(‘rss2_url’); ?&gt;** 输出博客RSS2.0 feed地址；
**&lt;?php bloginfo(‘charset’); ?&gt;** 输出博客所采用的编码；
**&lt;?php bloginfo( ‘description’ ); ?&gt;** 输出博客的描述，即副标题，在后台设置常规里面可以设置。

在后面，我们还要用到这个函数，同时也跟大家说一下。wordpress模板制作简单就在于，有很多这样的函数，我们要想实现某种功能，就在相应地方插入这些wordpress函数加上相应的参数。

## 制作模板的&lt;head&gt;头部标签

一个标准的网页，少不了规范标准的&lt;head&gt;标签，但是&lt;head&gt;标签内的内容是相对固定的，所以它的代码是相对通用的。我从官方默认的模板中，提取出了下面的&lt;head&gt;标签中代码：

&lt;head&gt;
&lt;meta http-equiv="Content-Type" content="&lt;?php bloginfo('html_type'); ?&gt;; charset=&lt;?php bloginfo('charset'); ?&gt;" /&gt;
&lt;title&gt;&lt;?php wp_title('&amp;laquo;', true, 'right'); ?&gt;&lt;?php bloginfo('name'); ?&gt;&lt;/title&gt;
&lt;link rel="stylesheet" type="text/css" media="all" href="&lt;?php bloginfo( 'stylesheet_url' ); ?&gt;" /&gt;
&lt;link rel="pingback" href="&lt;?php bloginfo('pingback_url'); ?&gt;" /&gt;
&lt;link rel="profile" href="[http://gmpg.org/xfn/11"](http://gmpg.org/xfn/11) /&gt;
&lt;?php if ( is_singular() &amp;&amp; get_option( 'thread_comments' ) )
wp_enqueue_script( 'comment-reply' ); ?&gt;
&lt;?php wp_head(); ?&gt;
&lt;/head&gt;

我们只需要在自己的模板中，把上面的语句复制进去就可以了。在这里，潜行者m只对其中代码进行一个简单的解释：

1，charset=&lt;?php bloginfo('charset'); 调用了博客的编码，由博客的编码决定模板的编码，提高了模板的适应性。

2，&lt;title&gt;&lt;?php wp_title('&amp;laquo;', true, 'right'); ?&gt;&lt;?php bloginfo('name'); ?&gt;&lt;/title&gt; 这是标题，显示你在博客后台设置的你博客名称（bloginfo('name'); ），前面的一句&lt;?php wp_title('&amp;laquo;', true, 'right'); ?&gt;的用处就是显示文章等名称，如果你访问的是首页，那么标题就会显示博客名称（例如：潜行者m），如果你访问的某篇文章，标题就会显示“文章名称 &amp;laquo; 博客名称”（例如：XXX《潜行者m）。

3，&lt;?php wp_head(); ?&gt;很多博客模板都会添加这一句，这个函数会生成很多代码。某些wordpress的插件，使用时会需要这个函数提供的代码。所以，尽量在自己模板中加上这句代码。要注意的是，这句代码，只能添加在&lt;head&gt;标签中，不能添加在其他地方。

对于上述代码，就解释这么多，想了解更多的，可以搜索一下他们的函数名称，查看，在这里不再赘述。

复制完成之后，我们的head标签内容，就已经完成了，下面我们应该进行&lt;body&gt;标签中的头部制作。

## 制作模板的头部

在头部，我们通常需要放置我们博客的名称和博客的描述，就像这样：

[![index7](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index7_thumb1.jpg)](http://yujiangshui.com/qianxingzhem.com/wp-content/uploads/2012/02/index71.jpg)

这样，我们就在头部新建一个