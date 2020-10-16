title: wordpress 模板开发 2——配置本地开发环境
tags:
  - wp 主题制作教程
id: 602
categories:
  - 网站与后台开发
date: 2012-02-14 14:12:08

---

模板开发有两种方法：**第一种，就是在 wordpress 程序上，新建一个模板文件夹，之后不断设计模板，然后使用浏览器访问即时的看到效果。**这种方法比较适合新手，开发比较慢，但是能够边制作边学习。**第二种，就是直接写，制作完成之后，放在博客上面测试一下。**这种方法需要有一定的开发经验。

本系列教程采用第一种方法。即在本地搭建一个 wordpress 程序，然后使用工具（例如[dreamweaver](http://www.qianxingzhem.com/post-620.html)）新建一个站点，指向新建的模板目录，在 wordpress 后台配置一下使用模板，之后开始制作模板，并且不断的通过浏览器观看模板制作的效果。

**第一步，wordpress 程序安装：**

为了调试方便，我们在本地安装 wordpress 程序。这样，我们首先应该搭建一个本地 apache、php、mysql 环境。关于如何搭建，可以观看本人的这篇文章教程：[本地搭建配置 apache+php+mysql 环境](http://www.qianxingzhem.com/post-455.html)，在这里不再赘述。

安装 wordpress 也同样不再多说了，如果你连 wordpress 都安装不上，肯定不会去学习[模板开发](http://www.qianxingzhem.com/post-tag/wordpresstheme)了。

这里要注意的是，我们要从现有的博客中导出部分测试数据，导入到新的博客中。在模板开发中，要看到具体的效果，本地 wordpress 里面必须要有数据才能看到。完成上面的步骤之后，我们的本地 wordpress 程序就安装好了，打开浏览器，输入 localhost，我们应该可以看到本地的测试博客。

[![](https://qxzm-cdn.sapi.work/blog/2012/02/wpkf.jpg "wpkf")](https://qxzm-cdn.sapi.work/blog/2012/02/wpkf.jpg)

**第二步，配置 dreamweaver：**

你可以选择记事本进行手写，但是我更加推荐使用第三方强大的软件，来进行模板的开发，这样可以节省大量的时间和精力。关于 dreamweaver，如果不熟悉或者不会使用的朋友，可以观看我制作的[dreamweaver 基础视频教程](http://www.qianxingzhem.com/post-620.html)。

在这里的配置，主要是新建一个站点，设置站点文件夹指向你的 wordpress 程序目录，或者直接指向模板目录。还可以在配置的过程中，使用 php 服务器技术，这样，我们在制作完成模板的时候，可以不需要打开浏览器，直接在 dreamweaver 中就可以看到效果。

新建一个站点的具体操作在这里不再赘述，如果有不会的朋友，可以搜索一下或者看我的视频教程。在这里，我们新建好了。

[![](https://qxzm-cdn.sapi.work/blog/2012/02/wpkf1.jpg "wpkf1")](https://qxzm-cdn.sapi.work/blog/2012/02/wpkf1.jpg)

这样，我们开发 wordpress 模板的第一步—搭建本地测试环境就这样完成了，下一节开始，我们就进行模板相应模块的开发。
