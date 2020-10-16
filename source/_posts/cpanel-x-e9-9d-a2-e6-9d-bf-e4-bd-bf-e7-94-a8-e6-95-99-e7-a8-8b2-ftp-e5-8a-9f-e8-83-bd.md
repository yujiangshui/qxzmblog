title: cPanel X面板使用教程2—FTP功能
tags:
  - cPanel X
id: 623
categories:
  - 其他
date: 2012-02-14 10:48:50
---

FTP对于一个强大的空间来说，是一个必不可少的东西。在[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中ftp功能就比较强大，但是强大的背后也是难以接触。我第一次使用的时候，真的不会用，新开辟的ftp账号，链接不上。后来看了一些网上的文章之后，才会使用的。

我们来看一下关于ftp功能的面板：

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp5.jpg "cPanel xftp")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp5.jpg)

**1，ftp账号**

通常来说，使用[cPanel X面板](http://www.qianxingzhem.com/post-tag/cpanel-x)的主机，ftp账号是可以开通无限个的。点击“ftp账号”，我们就可以去新建ftp登陆账号。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp1.jpg "cPanel xftp1")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp1.jpg)

配置的ftp账号，可以设置一个特定的文件夹，并且也有大小的限制，非常方便进行控制。之后，我们点击“生成邮件列表”就可以了，这里是翻译错了 。

配置好之后，在下面的ftp列表中就可以看到了，并且可以点击右边的按钮进行一些配置。下面说说最关键的链接使用，因为我第一次配置之后，就不会链接。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp2.jpg "cPanel xftp2")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp2.jpg)

这样，我们使用ftp软件进行连接的时候，应该在用户名那里输入：账户@域名 而不能仅仅输入账户。这里，就体现出了在一开始设置主域名的用处，就是用来标记你的空间用的。

**2，ftp进程控制**

这是一个比较实用的功能，当我使用ftp软件连接上去的时候，就可以在后台看到连接信息。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp3.jpg "cPanel xftp3")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp3.jpg)

这样的好处就是，如果你看到了陌生的ftp连接，这有可能是黑客入侵以及其他的行为，你可以人为的控制断掉他的链接，保证网站的安全。

**3，匿名ftp**

匿名ftp就是可以不需要用户名和密码就可以登录的ftp。在[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中默认允许匿名访问你空间主域ftp的。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp4.jpg "cPanel xftp4")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/cPanel-xftp4.jpg)

为了减少不必要的安全隐患，潜行者m在这里提醒大家，如果没有必要的话，请关闭匿名ftp功能。

但是从这个匿名ftp功能中，我们又可以得到一些启发。如果服务器进行了http网速等的限制，我们可以给出ftp下载地址，让用户可以通过匿名ftp的方式，从服务器上下载文件。这样就能突破某些下载限制了，呵呵，说多了。

## 相关文章：

[1，cPanel X面板使用教程1—网站备份功能](http://www.qianxingzhem.com/post-589.html )

[2，cPanel X面板使用教程2—FTP功能](http://www.qianxingzhem.com/post-623.html)

[3，cPanel X面板使用教程3—域名相关](http://www.qianxingzhem.com/post-661.html )

[4，cPanel X面板使用教程4—数据库操作](http://www.qianxingzhem.com/post-693.html)

&nbsp;

**PS：**[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中，我们最常用的就是 网站备份、FTP相关、域名相关和数据库相关的操作。再加上目前网络上已经有很多关于[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)的文章，再次就不再继续编写这类文章。