title: 使用 PHP 获取并解析 JSON 显示在页面中
tags:

- JSON
- PHP
  id: 1904
  categories:
- 网站与后台开发
  date: 2013-04-22 18:01:19

---

很久没写过 PHP 的文章了，也很久没有用 PHP 了，差点忘了怎么做了。JSON 是现在比较流行的数据交流方式，比 XML 都流行，一般用作 api 接口进行数据获取、交流。

就文章的标题来说，本文介绍两个小要点：PHP 获取内容、PHP 解析 JSON 并显示。

## PHP 获取接口内容

你如果想解析 JSON 数据并且显示在页面中，第一步肯定要先得到 JSON 接口文件的内容。在 PHP 中获取一个页面的内容，可以使用 [fopen() 函数](http://php.net/manual/zh/function.fopen.php)远程页面然后使用 [fread() 函数](http://php.net/manual/en/function.fread.php)循环获取内容。

假设接口文件页面为：http://www.qttc.net/api.php?action=open_getBlogList&amp;only_recommend=1&amp;limit=5 ，那么我们可以使用下面语句获取这个接口文件内容：

<pre>$handle = fopen("http://www.qttc.net/api.php?action=open_getBlogList&amp;only_recommend=1&amp;limit=5","rb");
$content = "";
while (!feof($handle)) {
    $content .= fread($handle, 10000);
}
fclose($handle);</pre>

这样 content 保存的就是 JSON api 内容。

## PHP 解析 JSON 并显示

原始的内容是无法直接调用的，必须被 PHP 进行进一步处理，才能被调用显示在网页中。在 PHP 5.2 及后续版本中，使用 json_decode() 函数来解析 JSON 数据，将其转换成 PHP 可以调用的数据格式。例如：

<pre>$content = json_decode($content);</pre>

解析之后呢，我们就可以按照 PHP 中调用数组数据的方法一样的调用 JSON 中的数据。这个调用方法需要按照具体的 JSON 数据格式来写，演示请看下面。关于 json_decode 函数的使用，具体看 PHP 手册，这里不再赘述：[http://php.net/manual/en/function.json-decode.php](http://php.net/manual/en/function.json-decode.php)

## 实战调用琼台博客的 api

细心的朋友会发现 [潜行者 m 博客](http://www.qianxingzhem.com)的边栏最下面多了一个“友文推荐”模块，里面推荐了一些[琼台博客](http://www.qttc.net)的文章。

[![友文推荐](https://qxzm-cdn.sapi.work/blog/2013/04/1904/youwen.png)](https://qxzm-cdn.sapi.work/blog/2013/04/1904/youwen.png)

友文推荐是琼台博客倡议的一种博客之间交流方式，比传统的友情链接更有效，同时实现了博客内容互补。由于琼台博客的博客程序是他自己本人编写的，所以他提供了 JSON api 接口，可以获取到最新的可推荐的文章。

本人使用 PHP 获取这个 JSON 接口，然后输出到自己博客的边栏中，下面来实战操作一下。

### 第一步，查看 api 调用方式

调用之前，你肯定要看一下对方的 api 调用手册，包括调用地址、如何调用、数据输出格式等等。琼台博客的 api 说明地址如下：[http://www.qttc.net/openapi.html](http://www.qttc.net/openapi.html)。

根据文档，我使用了 http://www.qttc.net/api.php?action=open_getBlogList&amp;only_recommend=1&amp;limit=5 这样的参数，意思就是调用五条他推荐的文章。

### 第二步，获取 api 结构数据

很简单，上面说过了，具体代码如下：

<pre>$handle = fopen("http://www.qttc.net/api.php?action=open_getBlogList&amp;only_recommend=1&amp;limit=5","rb");
$content = "";
while (!feof($handle)) {
    $content .= fread($handle, 10000);
}
fclose($handle);</pre>

先打开这数据文件，然后把所有内容保存到 content 变量中，因为可以肯定 api 数据不会超过 10000 个字符，所以用 10000 作为 fread 函数的第二个参数。这样，api 返回的 JSON 数据就保存在了 content 变量中。

### 第三步，解析并输出内容

使用下面代码解析数据，然后调用输出

<pre>$content = json_decode($content);
foreach ($content-&gt;data as $key) {
    echo '&lt;li&gt;&lt;a target="_blank" href="'.$key-&gt;b_url.'"&gt;'.$key-&gt;b_title.'&lt;/a&gt;&lt;/li&gt;';
}</pre>

首先对 content 变量中的 JSON  数据处理，然后变成 PHP 可以调用的数据，再使用 foreach 遍历输出这五条内容，按照我需要的 HTML 格式，将内容插入进去即可。

再加上样式修饰，这样就完成了 获取并解析 JSON 显示在页面中了。调用其它 api 数据的方法大同小异。
