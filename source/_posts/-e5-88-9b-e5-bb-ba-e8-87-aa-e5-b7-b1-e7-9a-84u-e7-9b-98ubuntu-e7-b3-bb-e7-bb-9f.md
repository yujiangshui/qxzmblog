title: 创建自己的U盘ubuntu系统
tags:
  - Ubuntu
id: 438
categories:
  - 其他
date: 2012-01-29 07:40:26
---

这些天终于把vista系统整理的差不多了，为了学习的考虑，打算再装上个linux系统。最终还是选择了ubuntu，确实不错的系统。

下面，安装就成了一个问题。我的笔记本电脑光驱已经用了四年了，基本上报废了，盗版光盘和自己刻录的光盘读不出来了。以前刻录的那个ubuntu安装光盘也已经不行了。那么就用U盘吧。自己在网上找了找，官方就有这个教程，是英文的，我现在用中文写一遍。

首先，你需要的东西是**ubuntu操作系统的镜像文件**、**一个4G以上的U盘**和**Universal-USB-Installer**这个程序。这个程序是主角，下载地址是http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/。本文重点讲的也是如何使用这个程序来把linux系统装到u盘上。

以上三个东西都准备好了之后，运行这个程序，点击“I agree”之后，就进入了程序配置页面，请看下面说明：

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux1.jpg "linux1")](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux1.jpg)

之后，点击“create”就开始格式化你的u盘、解压缩系统、安装系统了。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux2.jpg "linux2")](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux2.jpg)

接着等待即可，大约半个多小时之后，linux操作系统就已经安装到了u盘上。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux3.jpg "linux3")](http://qxzm-img.b0.upaiyun.com/blog/2012/01/linux3.jpg)

这样，我们只要插着u盘重启电脑就可以进入u盘linux了，就和光盘版的一样。如果有同学重启之后，还是自动进入了windows系统，说明你的电脑默认从硬盘加载系统，在开机界面的时候，按下F8（通常是F8，有的电脑可能不同），选择USB那一项就可以了。