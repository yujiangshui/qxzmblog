title: "网页中的 cookie 操作总结（PHP & JavaScript）"
id: 1878
categories:
  - 其他
tags:
---

如果你连 cookie 是什么都不知道，那么这篇文章请略过。如果你执意想看，那么可以先看一下 [cookie 的百度百科介绍](http://baike.baidu.com/view/835.htm)，大体了解一下关于 cookie 的基础知识。网上太多介绍，本文不再赘述。

使用 PHP 操作 cookie

PHP 中操作 cookie 主要使用 setcookie 函数来实现。它的语法：

bool setcookie(string name [, string value [, int expire [, string path [,string domain [, int secure ]]]]])

返回一个布尔值，具体的参数说明如下：

*   name：cookie 的名称
*   value：cookie 的内容
*   expire：cookie 失效时间
*   path：cookie 在服务器上的有效路径
*   domain：cookie 在服务器上的有效域名
*   secure：cookie 是否仅允许通过安全的 HTTP 协议传输。1 仅允许安全传输，0 允许普通传输。

创建 cookie

cookie 常用的两个属性是 name、value ，创建一个简单的 cookie 代码如下：

<?php
  setcookie("username","潜行者m");
>

这样，就在你电脑中创建了一个 cookie，它的名字是 username 记录的值是 qianxingzhem 。PHP 中使用预定义数组 $_COOKIE[] 来读取 cookie，可以使用下面代码来读取刚刚创建的 cookie 

<?php
  if(isset($_COOKIE["username"])){
    echo $_COOKIE["username"];
  }else{
    echo '没有 username cookie 信息';
  }
?>

使用 isset 函数来检查是否有对应的 cookie，然后在页面中输出。

创建具有时间限制的 cookie

有些时候，为了用户安全，cookie 要设置失效时间。有些网站在登陆的时候也会提供一个选项，可以选择保持登陆失效时间。直接使用下面语句即可实现：

<?php
  setcookie("username","潜行者m",time() + 60*60*24);
?>

设置 expire 一般通过在当前时间加上相应的秒数实现，上面的意思就是这个 cookie 将会保存一天。

创建具有范围限制的 cookie

cookie 通常要有范围限制，主要有 路径、域名 两种范围限制。