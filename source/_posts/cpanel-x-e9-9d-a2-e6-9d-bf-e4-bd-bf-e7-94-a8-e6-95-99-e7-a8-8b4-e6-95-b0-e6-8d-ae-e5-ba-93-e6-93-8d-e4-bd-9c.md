title: cPanel X面板使用教程4—数据库操作
tags:
  - cPanel X
id: 693
categories:
  - 其他
date: 2012-02-16 23:40:43
---

使用[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)面板的主机，通常的配置是[linux+php+mysql+apache](www.qianxingzhem.com/post-455.html)（或nginx）。所以，[mysql数据库](www.qianxingzhem.com/post-455.html)的功能不容忽视，在[cPanel X面板](http://www.qianxingzhem.com/post-tag/cpanel-x)上，可以新建数据库，也可以管理数据库等。

[![mysql0](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql0.jpg)](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql0.jpg)

**1，mysql数据库：**

在这里，我们可以新建数据库，新建数据库用户和密码，并且绑定用户到数据库当中。

新建数据库的方法，很简单，按照上面的步骤，输入数据库名称，点击生成，之后新建的数据库就出现在了下面的数据库列表中。

[![mysql1](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql1.jpg)](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql1.jpg)

虽然已经生成了，但是这个数据库目前是无法使用的，因为没有数据库用户名。我们还需要添加一个数据库用户，之后才能用程序使用这个数据库用户连接数据库使用。生成一个用户名也很简单，在下面生成即可。要注意的是，需要在相应数据库中，插入相应的用户，才能正常使用。

[![mysql2](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql2.jpg)](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql2.jpg)

插入的时候，它还会提示你，你插入的用户的权限

[![mysql3](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql3.jpg)](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql3.jpg)

这里，我们可以对不同的用户勾选不同的权限配置，来确保数据库的安全。如果不懂的朋友，可以像我一样，勾选全部权限即可。

**2，mysql 数据库向导：**

向导就是把上面的内容，一步步的显示出来而不是一次性都出来，所以在这里就不多说了。建议第一次，先使用向导有一个大体的了解，以后为了方便，就不要用向导了。

**3，phpmy 管理：**

这里，不得不提一下翻译者的水平，一看就不是一个电脑专业的。这里应该是phpmyadmin，一款著名的mysql数据库管理工具。打开看一下，和以往的phpmyadmin有很大的不同。

[![mysql4](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql4.jpg)](http://qxzm-img.b0.upaiyun.com/blog/2012/02/mysql4.jpg)

效果华丽多了，我一直不太喜欢用phpmyadmin，就是因为它的实现效果实在是太差劲了，没想到这个主题还不错。在这里面，可以方便的导入导出数据库、修改数据等。具体的使用，不再赘述了。

**4，远程mysql：**

通常来说，数据库和网站都是放在一个服务器上的，这样使用localhost或者127.0.0.1作为数据库地址即可。但是，数据库也是可以远程调用的，这样有一个安全隐患。例如，有人通过程序漏洞等，读取了你的网站的配置文件，得到了你数据库地址和用户名密码等信息，就可以连接你的数据库，导出这些信息。但是[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)的默认配置是无法让外部连接的，如果想要外部连接，我们必须在这里添加上域名或者服务器IP。

## 相关文章：

[1，cPanel X面板使用教程1—网站备份功能](http://www.qianxingzhem.com/post-589.html )

[2，cPanel X面板使用教程2—FTP功能](http://www.qianxingzhem.com/post-623.html)

[3，cPanel X面板使用教程3—域名相关](http://www.qianxingzhem.com/post-661.html )

[4，cPanel X面板使用教程4—数据库操作](http://www.qianxingzhem.com/post-693.html)

&nbsp;

**PS：**[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中，我们最常用的就是 网站备份、FTP相关、域名相关和数据库相关的操作。再加上目前网络上已经有很多关于[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)的文章，再次就不再继续编写这类文章。