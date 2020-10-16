title: 前端开发神器 Emmet 介绍
tags:

- sublime text 2
  id: 1937
  categories:
- 前端相关
  date: 2013-05-06 21:17:09

---

在前端开发的过程中，一大部分的工作是写 HTML、CSS 代码。特别是手动编写 HTML 代码的时候，效率会特别低下，因为需要敲打很多尖括号，而且很多标签都需要闭合标签等。于是，就有了 Emmet，它可以极大的提高代码编写的效率，它提供了一种非常简练的语法规则，然后立刻生成对应的 HTML 结构或者 CSS 代码，同时还有多种实用的功能帮助进行前端开发。

你可能听说过一款强大的功能相似的工具：Zen Coding，那个比较老了，而现在的 Emmet 则是 Zen Coding 的升级版，由 Zen Coding 的原作者进行开发等。

Emmet 严格意义上来说，并不是一款软件或者工具，它是一款编辑器插件，必须要基于某个编辑器使用。目前它支持如下编辑器：

- [Sublime Text 2](https://github.com/sergeche/emmet-sublime)
- [TextMate 1.x](https://github.com/emmetio/Emmet.tmplugin)
- [Eclipse/Aptana](https://github.com/emmetio/emmet-eclipse)
- [Coda 1.6 and 2.x](https://github.com/emmetio/Emmet.codaplugin)
- [Espresso](https://github.com/emmetio/Emmet.sugar)
- [Chocolat](https://github.com/sergeche/emmet.chocmixin) (可以通过 “Install Mixin” 对话框安装)
- [Komodo Edit/IDE](https://github.com/emmetio/emmet/downloads) ( Tools → Add-ons)
- [Notepad++](https://github.com/emmetio/emmet/downloads)
- [PSPad](https://github.com/emmetio/emmet/downloads)
- [&lt;textarea&gt;](https://github.com/emmetio/emmet/downloads)
- [CodeMirror2/3](https://github.com/emmetio/codemirror)
- [Brackets](https://github.com/emmetio/brackets-emmet)
  在 上面列表点击你目前使用的编辑器，就可以获得对应的插件文件，安装之后就可以使用 Emmet 的相关功能了。由于 Sublime text 2 是目前最好最强大的前端开发代码编辑器，所以本文就以 Sublime text 2 为例，讲解 Emmet 的安装、基础语法。

## 在 Sublime text 2 中安装 Emmet

Sbulime text 2 安装插件肯定要通过 Package Control 这个插件了，如果你还没有安装这个插件，抓紧先去安装一下吧。安装完成之后，我们摁下“shift + ctrl + p”呼出面板，输入“pci”即可锁定“Package Control：Install Package”这个功能，回车之后就可以看到一个列表，我们继续输入“emmet”即可找到这个插件，回车之后等待一会就安装完成了。

![sublime text 2 安装 emmet ](https://qxzm-cdn.sapi.work/blog/2013/04/1907/emmet0.png)

## 开始使用 Emmet

Emmet 可以快速的编写 HTML、CSS 以及实现其他的功能。它根据当前文件的解析模式来判断要使用 HTML 语法还是 CSS 语法来解析。例如当前文件的后缀为 .html 那 Sublime text 2 就会用 HTML 的解析模式来解析高亮这个文件，Emmet 遇到里面的指令就会根据 HTML 的语法把它编译成 HTML 结构。如果是在一个 .c 的 C 语言 文件中，你写出来的用于编译 HTML 指令就不会被 Emmet 识别编译。

此外，在没有后缀的文件中，你可以摁下“shift + ctrl + p”呼出面板，输入“seth”就可以设置当前文件的解析模式为 HTML 。了解这些之后，下面我们来见证强大的 Emmet 。

如果让你编写下面的这个 HTML 结构，你需要多长时间？

<pre>&lt;div id="page"&gt;
    &lt;div class="logo"&gt;&lt;/div&gt;
    &lt;ul id="navigation"&gt;
        &lt;li&gt;&lt;a href=""&gt;Item 1&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=""&gt;Item 2&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=""&gt;Item 3&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=""&gt;Item 4&lt;/a&gt;&lt;/li&gt;
        &lt;li&gt;&lt;a href=""&gt;Item 5&lt;/a&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;</pre>

然而，这一切你只需要编写下面这一句按照 Emmet 语法写出来的语句，然后用 Emmet 编译一下，就可以生成了！

<pre>#page&gt;div.logo+ul#navigation&gt;li*5&gt;a{Item $}</pre>

我们把它复制到 Sublime text 2 中已经打开的 HTML 文件中，这时候紧跟着敲击一下 TAB 键，见证奇迹的时刻到来了。

怎么样？很神奇吧，仅仅写一行代码，就可以生成这么一个复杂的 HTML 结构，而且还可以生成对应的 class 、id 和有序号的内容。而且 Emmet 的语法很简单，虽然你现在可能还看不懂，后面的系列教程会详细讲解它的语法，你现在只需要知道 Emmet 的工作流程：**打开 HTML 或 CSS 文件**-&gt;**按语法编写指令**-&gt;**摁下 TAB 键**-&gt;**生成！**
