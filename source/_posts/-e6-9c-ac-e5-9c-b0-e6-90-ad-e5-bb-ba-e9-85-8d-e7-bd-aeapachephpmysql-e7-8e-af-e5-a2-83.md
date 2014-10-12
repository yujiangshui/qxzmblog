title: 本地搭建配置apache+php+mysql环境
id: 455
categories:
  - 网站与后台开发
date: 2012-02-03 15:50:09
tags:
---

**前言：**我以前一直用的是类似wamp之类的综合网络服务器系统软件。这些软件使用很简单，整合了apache、php、mysql等。但是这些软件也有很多弊端。比如功能限制大，自己配置一些信息不方便，不方便组件的升级等。为了更好的学习apache服务器配置以及php环境，我决定不再用这些软件，自己手动搭建环境。首先先在网上搜索了一下这方面的文章，结果发现大都是06年、07年的，那时候的配置方法都太古老了，现在已经是2012年了。我自己安装了一下，非常简单，根本没有以前那么麻烦。这样，就写这篇比较新的教程供新手参考。

**第一步，准备**：先介绍一下我的系统配置。我的系统是**vista 32位旗舰版**，其他windows系统环境下的操作应该是差不多一样的。我们需要的程序就是**httpd-2.2.21-win32-x86-no_ssl.msi**、**php-5.2.17-Win32-VC6-x86.zip**和**mysql-5.5.20-win32.msi**。在这里我都是从官方下载的最新原版。

**httpd-2.2.21-win32-x86-no_ssl.msi**这个文件是最新版的apache服务器软件，下载地址：http://httpd.apache.org/download.cgi#apache22 跳转到这里之后，找到适合自己系统的apache程序，下载即可。

**php-5.2.17-Win32-VC6-x86.zip**这个压缩包是php最新的环境包，下载地址：http://windows.php.net/download/下载php环境包的时候，一定要注意看清楚左边等说明。它分为VC9和VC6两种，这两种还分别有不同功能等包，分别是多线程安全（Thread Safe）和无多线程安全（Non Thread Safe）。其中VC9是适合IIS服务器等，VC6是适合apache服务器的。

**mysql-5.5.20-win32.msi**这是mysql的最新版windows安装包，下载地址：http://www.mysql.com/downloads/mysql/找到适合自己系统的版本下载即可。

**第二步，安装：**下载完之后，我们就开始安装。首先，我们先安装apache服务器。双击**httpd-2.2.21-win32-x86-no_ssl.msi**，出现安装向导。一步一步的按照向导来安装，非常简单。需要注意的是，到了**【Server Information】**安装界面时，如果你是在本地调试，不是一台可用的服务器，甚至没有联网。那么你就得在前面两个框中直接输入**localhost**，在第三栏中任意输入你的邮箱地址。之后如果没有提示什么错误，就算是安装完成了。右下角等任务栏会出现apache羽毛图标，显示绿色正在运行。这时，打开你的浏览器，在地址栏上输入** “localhost”**，浏览器会显示**“It works”**这就说明apache服务器已经成功的安装完成了。

下面是更简单的php安装。打开**php-5.2.17-Win32-VC6-x86.zip**这个压缩包，将里面的所有文件随便复制到一个文件夹中即可。在我的电脑里，是复制在E盘的php文件夹里。

mysql的安装也是很简单的，有向导，根据向导一步一步的来，如果看不懂什么意思的话，一般保持默认选项即可。需要注意的是，在设置密码的地方，设置上一个密码，并且记住，这样使你的系统更安全。安装完成后，会自动注册为系统服务，并且开机会自动运行。

**第三步，连接：**这是在安装配置这个环境中，最重要的一步。要apache服务器能正常的解析php，必须把php和apache链接起来。在windows系统中，打开“**控制面板**”找到“**系统**”，之后打开“**高级系统设置**”，选择“**高级**”标签。点击下面的“**环境变量**”，找到下面的“**系统变量**”，在列表中选择“**Path**”，双击打开，在变量值中，加上你php的路径（本例为E:php）。注意：**使用“；”分号与前面的值分开，不要修改原有的值，否则会产生系统错误。**

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache.jpg "apache")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache.jpg)

之后，打开apache安装目录，找到“conf”文件夹中的“**httpd.conf**”文件，使用记事本打开编辑。在**LoadModule**段落的最下面，按照下图的格式，写下如下代码：
<pre>LoadModule php5_module "e:/php/php5apache2_2.dll"
LoadFile  E:/php/libmysql.dll
AddType application/x-httpd-php .php
AddType application/x-httpd-php .htm
PHPIniDir "E:/php"</pre>
[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache2.jpg "apache2")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache2.jpg)

简单解释一下，**LoadModule**是指加载模块，前两句的意思就是，加载php编译模块和php链接mysql模块，如果不添加第二句的话，mysql是无法链接的。**AddType**是增加文件类型，这两句的意思是，遇到文件后缀为 php、htm的文件，都使用php对其进行编译。在这里，你可以随便添加文件类型，比如php3、html等等，访问它们的时候，文档中的php代码都会被运行。**PHPIniDir** 是制定了php安装的目录。

再进入php安装目录，找到“**php.ini-dist**”文件，把它的文件名修改成“**php.ini**”，这样大功告成！之后，重启apache服务器，如果apache服务器成功重启，则说明你的apache+php+mysql环境已经成功安装。如果无法重启，说明你修改httpd.conf文件的时候，没有按照指定的格式书写，也有可能是因为一些其他原因。但是如果按照我上面的步骤，是没有问题的。如果你遇到了问题，可以与我联系（qianxingzhem#163.com）。

最后，我们进行mysql数据库功能的加载，只有配置了这一步，才能连接mysql使用。打开php.ini文件，搜索找到“**extension_dir**”，把引号内的内容(如”./”)改成”**e:/php/ext**”，即指定扩展模块的目录。之后，继续查找”;extension=php_mysql.dll”，把**;extension=php_mysql.dll**和**;extension=php_mysql.dll** 前的”**;**”注释号去掉，这样就可以让PHP加载扩展模块**mysql**及**mysqli**模块。保存退出即可。

**第四步，使用：**安装完了之后，使用才是最关键的。按照上面的步骤完成后，你的网页文件应该存放在：E:apachehtdocs（就是apache安装目录的htdocs文件夹中）

我们先来测试一下自己环境是否搭建成功。打开记事本，编写一句显示php环境的函数：
<pre>&lt;?php phpinfo(); ?&gt;</pre>
保存为index.php文件，复制到apache的htdocs目录下，在浏览器中输入：localhost。这时候，就可以看到你的php环境的配置了。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache3.jpg "apache3")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache3.jpg)

这样，apache和php就算是完美的连接到一起了。只要把你的php网站源码放在这个目录下，访问localhost就可以看到。下面重点来讲解一下关于mysql数据库的使用。mysql数据库使用默认配置安装后，它的默认数据库存放地址是：**C:ProgramDataMySQLMySQL Server 5.5data**。我们如果想要对数据库进行操作，打开这么多文件夹实在不是明智之举。这样，我们就需要修改一下它的默认位置。我在网上搜索了一下，结果发现，修改默认位置的文章大都是在linux下的。下面我就教大家如何在windows系统下，修改数据库的默认位置：

我们需要找到mysql数据库安装位置下面的**my.ini**文件，下拉找到
<pre>#Path to installation directory. All paths are usually resolved relative to this.
basedir="C:/Program Files/MySQL/MySQL Server 5.5/"

#Path to the database root
datadir="E:/mysql/data"</pre>
[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache4.jpg "apache4")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache4.jpg)
这两段，第一段的**basedir**是安装目录，不要修改，第二段的**datadir**是你的数据库位置，在这里我修改成了“E:/mysql/data"，这里是你指定的位置。修改完成之后，关掉保存。之后，需要暂停mysql服务，然后把原来默认的数据库文件，全部不变的复制到你的新目录里面，之后再重启即可。至于如何停止mysql服务，你可以摁下“WIN+R”键，打开运行，输入“cmd”回车，打开DOS命令窗口。在里面输入：**net stop mysql**。这样就停止服务了。当文件复制完成，再输入：**net start mysql**，即可开启服务。

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache5.jpg "apache5")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache5.jpg)

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache6.jpg "apache6")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache6.jpg)

必须要注意的是，原来的文件目录等，都要完全一致，否则可能会出现意外情况。下面，我带着大家亲自安装一下wordpress程序，让大家了解mysql该如何配置使用。

在上图中，我新建了一个“wp”文件夹，这样，就相当于建立了一个新的数据库，名称“wp”。我们进入wordpress安装界面：

[![](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache7.jpg "apache7")](http://qxzm-img.b0.upaiyun.com/blog/2012/02/apache7.jpg)

**数据库名称**，就是你新建的文件夹名称；**用户名**，就是mysql用户名，默认为root；**密码**就是在上面安装mysql过程中，你配置的密码，如果你在安装时，没有配置密码则此处留空；数据库主机，就是你本地，输入localhost即可；**表名前缀**，随便填写即可，如果一个数据库中安装多个wordpress程序，这个前缀是用来表明不同wordpress程序的。点击“提交”，OK，安装完成！

这样，我们的apache+php+mysql就彻底的完成了，是不是很简单？在运行php网站的时候，你可能会遇到一些错误，这多半是由于php.ini没有配置的缘故。我们使用的虚拟主机等，都是他们已经配置好的，而原官方的php.ini是全新的，没有经过任何配置，大多数模块由于安全考虑，都是关闭的。如果你遇到什么问题，可以上网搜索一下，修改一下php.ini文件就可以了。

最后说明一下，这个步骤和方法在本人的电脑上是完全正常可以的，如果在你的电脑上不能正常，有可能是由于操作系统、apache版本、php版本、mysql版本不同造成的，推荐使用搜索引擎寻找解决方案，也可以与本人联系看看能不能帮你解决。

&nbsp;

**PS：有些朋友安装完成后，apache有可能无法启动，怎么也找不到原因。这有可能是由于端口冲突造成的。**

我们在访问一个网站的时候，默认使用的80端口，输入一个网址（例如 qianxingzhem.com），在浏览器请求实际上是这样的http://qianxingzhem.com:80/，表示使用80端口访问。由于默认就是80端口，所以在浏览器中就省略了“:80”。apache、IIS等服务器的服务端口，默认也是80，这样的话，如果你之前安装过IIS或者安装过其他使用80端口的程序，那么你使用localhost是无法访问apache服务其上的网页文件（因为端口被占用）。关于这种情况，可以有两种解决方式：

1，结束掉占用80端口的程序。方法可以看这里：[关于Apache端口冲突问题](http://down.cnzz.cn/HelpInfo/49.aspx)。就是把占用的程序关掉即可。

2，修改apache的默认端口，改变成其他不常用的端口。方法可以看这篇文章：[如](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[何](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[改](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[变](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[A](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[p](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[a](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[c](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[h](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[e](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[端](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr>[口](http://wenku.baidu.com/view/f422521b6bd97f192279e92e.html)<wbr><wbr>
</wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr></wbr>

如果还出现其他问题，欢迎与我联系，我会帮忙看一下如何解决。