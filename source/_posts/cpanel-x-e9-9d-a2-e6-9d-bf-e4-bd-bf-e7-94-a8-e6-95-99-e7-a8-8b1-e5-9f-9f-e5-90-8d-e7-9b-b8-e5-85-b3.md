title: cPanel X 面板使用教程 3—域名相关
tags:

- cPanel X
  id: 661
  categories:
- 其他
  date: 2012-02-16 12:47:19

---

在使用[cPanel X 面板](http://www.qianxingzhem.com/post-tag/cpanel-x)的过程中，不得不承认的是，它的域名相关功能非常的强大、方便。首先，先来看看域名相关控制面板：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/domain5.jpg "domain")](https://qxzm-cdn.sapi.work/blog/2012/02/domain5.jpg)

下面来依次介绍这几个功能。

**1，子域：**

子域就是主域名的二级域名。比如我绑定的主域名是 qianxingzhem.com ，那么我可以设置的子域名就是类似这种的 demo.qianxingzhem.com。使用子域这个功能，还可以设置子域对应的文件目录。之后，我们在 DNS 配置中，添加一条子域并且指向服务器 IP 就可以使用该子域。

[![](https://qxzm-cdn.sapi.work/blog/2012/02/domain11.jpg "domain1")](https://qxzm-cdn.sapi.work/blog/2012/02/domain11.jpg)

**2，附加域：**

附加域，就是你另外绑定的域名。比如你的空间不仅仅要做一个网站，还要把另外一个网站也绑定过来。那么就是用附加域功能，添加你的顶级域名，并且配置一下目录。之后，修改域名 dns 指向服务器 IP，就可以了。

**3，暂停的域：**

就是你暂停使用的域名，添加之后，就暂停使用你这个域名。

**4，重新定向：**

这是一个非常实用的功能，使用重定向，在 seo 上面有比较重要的应用，比如网站换用了新域名等等。

这个面板功能也是很强大的：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/domain21.jpg "domain2")](https://qxzm-cdn.sapi.work/blog/2012/02/domain21.jpg)

类型中有永久和临时两种选择，这样可以告诉搜索引擎你的网站是临时转移还是永久转移。在下面，我们可以选择要设置的域名，这里的域名包含绑定的主域名和附加域，还可以配置相应的目录。之后，在下面的重定向至里面，输入你要重定向的域名或者地址。

而下面的三个单选，第一个“只能使用 www 重定向”意思就是重定向的域名，都是以 www 开头的，例如www.qianxingzhem.com。中间的那个，就是不确定是不是使用www开头。最后一个，就是不要重定向www的域名，只定向类似 qianxingzhem.com 的域名。

至于最下面的 “wild card”功能，本人也没有见过，搞不清楚。

**5，简单 dns 编辑器和高级 dns 编辑器：**

justhost 有他们自己的 dns 服务器，为了方便，可以将域名直接绑定到 justhost 自己的 dns 服务器上面，这样设置子域等直接就可以生效。但是 justhost 的 dns 功能不是很强只能实现简单的 dns 功能，例如：添加 A 记录，添加 CNAME 记录等。添加的时候，首先要选择一个域：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/domain3.jpg "domain3")](https://qxzm-cdn.sapi.work/blog/2012/02/domain3.jpg)

关于图中的的“高级 dns 编辑器”，有些朋友的 cPanel X 面板可能没有这个功能，我的面板是被服务商修改过的，我之前用的就没有这个功能。“高级 dns 编辑器”就是把 dns 功能扩展了一些，可以多添加一个 TXT 记录而已。

[![](https://qxzm-cdn.sapi.work/blog/2012/02/domain4.jpg "domain4")](https://qxzm-cdn.sapi.work/blog/2012/02/domain4.jpg)

对于[cPanel X 面板](http://www.qianxingzhem.com/post-tag/cpanel-x)的 dns 功能，不是太强，所以建议把域名指向其他 dns 服务器，例如国内的 dnspod 等，之后再指向服务器 IP 即可。

## 相关文章：

[1，cPanel X 面板使用教程 1—网站备份功能](http://www.qianxingzhem.com/post-589.html)

[2，cPanel X 面板使用教程 2—FTP 功能](http://www.qianxingzhem.com/post-623.html)

[3，cPanel X 面板使用教程 3—域名相关](http://www.qianxingzhem.com/post-661.html)

[4，cPanel X 面板使用教程 4—数据库操作](http://www.qianxingzhem.com/post-693.html)

&nbsp;

**PS：**[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中，我们最常用的就是 网站备份、FTP 相关、域名相关和数据库相关的操作。再加上目前网络上已经有很多关于[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)的文章，再次就不再继续编写这类文章。
