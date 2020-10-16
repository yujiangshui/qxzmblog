title: cPanel X 面板使用教程 1—网站备份功能
tags:

- cPanel X
  id: 589
  categories:
- 其他
  date: 2012-02-12 00:40:11

---

网站运营过程中，备份是一个必不可少的环节，一个网站，需要定期的进行数据和资源的备份，以防出现各种意外情况，这是血的教训！备份功能也是一个网站空间控制面板必不可少的功能。

[cPanel X 面板](http://www.qianxingzhem.com/post-tag/cpanel-x)的备份功能，可谓是非常的强大，是[潜行者 m](http://www.qianxingzhem.com)用过的所有的后台备份功能最强大的了。

我们登陆后，找到“文件”面板，有两个备份，一个是“备份”，另一个是“备份向导”。如果新手第一次使用，可以点击“备份向导”，有文字提示，而直接使用备份也是很方便的。我们打开：

[![](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen0.png "cbeifen0")](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen0.png)

[![](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen1.png "cbeifen1")](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen1.png)

我通常的做法是直接备份全部目录，这样，justhost 主机上所有目录的所有文件都会导出，而且数据库里面的数据也会导出，一起压缩成一个压缩包。

[![](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen2.png "cbeifen2")](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen2.png)

它的备份速度是很快的，用不了几分钟，我的邮箱收到了备份完成的邮件

[![](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen3.png "cbeifen3")](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen3.png)

这时候，我们就可以登陆面板，找到备份文件，进行下载，也可以使用 ftp 登陆远程服务器，备份的内容会在根目录下面显示。这种备份方式的优点很明确，就是体积小，下载等都非常的节约时间，它把网站所有的文件都压缩起来，众所周知，代码、数据库等文件的压缩比是很高的，而且下载一个大文件的速度也比下载多个小文件的速度要快，因为不用 ftp 软件依次进行连接。

关于备份的还原，也是很方便的。我们可以

[![](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen4.png "cbeifen4")](https://qxzm-cdn.sapi.work/blog/2012/02/cbeifen4.png)

上传相应备份的 tar.gz 文件包，如果没有经过修改，[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)是会自动识别文件，并且导入数据，非常方便。同样对于网站搬家来说，也是非常方便。如果我从一个使用 cPanel X 的主机，把网站搬到另一个使用 cPanel X 的主机，只需要进行一个全目录的备份，之后把这个备份上传到另一台主机上，恢复备份。之后，再把域名转向新主机，修改一些细节就可以了。

&nbsp;

## 相关文章：

[1，cPanel X 面板使用教程 1—网站备份功能](http://www.qianxingzhem.com/post-589.html)

[2，cPanel X 面板使用教程 2—FTP 功能](http://www.qianxingzhem.com/post-623.html)

[3，cPanel X 面板使用教程 3—域名相关](http://www.qianxingzhem.com/post-661.html)

[4，cPanel X 面板使用教程 4—数据库操作](http://www.qianxingzhem.com/post-693.html)

&nbsp;

**PS：**[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)中，我们最常用的就是 网站备份、FTP 相关、域名相关和数据库相关的操作。再加上目前网络上已经有很多关于[cPanel X](http://www.qianxingzhem.com/post-tag/cpanel-x)的文章，再次就不再继续编写这类文章。
