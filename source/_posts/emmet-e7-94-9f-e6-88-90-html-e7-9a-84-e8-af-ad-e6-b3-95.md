title: Emmet 生成 HTML 的语法
tags:
  - sublime text 2
id: 1940
categories:
  - 前端相关
date: 2013-05-07 23:26:32
---

在上篇文章[前端开发神器 Emmet 介绍](http://www.qianxingzhem.com/post-1937.html)中，我简单的介绍了一下 Emmet ，并且用了一句指令迅速生成了一大片 HTML 代码。本文，就会介绍 Emmet 的 HTML 语法，看完之后，你就会看懂并且写出那句代码了。

现在，打开你的 ST2 然后新建一个 HTML 文档，跟着文章，即时输入对应的指令然后亲自尝试一下！

## 生成 HTML 文档初始结构

HTML 文档的初始结构，就是包括 doctype、html、head、body 以及 meta 等内容。你只需要输入一个 “!” 就可以生成一个 HTML5 的标准文档初始结构，你没有看错，输入一个感叹号（当然是英文符号），然后摁下 TAB 键，就会发现生成了下面的结构：
<pre>&lt;!doctype html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;meta charset="UTF-8"&gt;
    &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>
这就是一个 HTML5 的标准结构，也是默认的 HTML 结构。如果你想生成 HTML4 的过渡型结构，那么输入指令 `html:xt` 即可生成如下结构：
<pre>&lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en"&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html;charset=UTF-8"&gt;
    &lt;title&gt;Document&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;

&lt;/body&gt;
&lt;/html&gt;</pre>
Emmet 会自动把 doctype 给你补全了，怎么样，这样的功能会不会让你动心？简单总结一下常用的 HTML 结构指令：

*   `html:5` `或者 !` 生成 HTML5 结构
*   `html:xt` 生成 HTML4 过渡型
*   `html:4s` 生成 HTML4 严格型

## 生成带有 id 、class 的 HTML 标签

Emmet 的语法有点类似 CSS 的语法，生成 id 为 aaa 的 div 标签，我们只需要编写下面指令：
<pre>#aaa</pre>
Emmet 默认的标签为 div ，如果我们不给出标签名称的话，默认就生成 div 标签。如果编写一个 class 为 bbb 的 span 标签，我们需要编写下面指令：
<pre>span.bbb</pre>
然后就生成了对应的结构。同理，如果想要编写一个 id 为 ccc 的 class 为 ddd 的 ul 标签，我们可以这样写：
<pre>ul#ccc.ddd</pre>
很简单吧？比你用手写 id 、class 方便多了吧

## 生成后代：&gt;

大于号表示后面要生成的内容是当前标签的后代。例如我要生成一个无序列表，而且被 class 为 aaa 的 div 包裹，那么可以使用下面指令：
<pre>div.aaa&gt;ul&gt;li</pre>
可以生成如下的结构：
<pre>&lt;div&gt;
    &lt;ul&gt;
        &lt;li&gt;&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;</pre>

## 生成兄弟：+

上面是生成下级元素，如果想要生成平级的元素，就需要使用 + 号。例如下面指令：

    div+p+bq`</pre>
    就可以生成如下的 HTML 结构：
    <pre>`&lt;div&gt;&lt;/div&gt;
    &lt;p&gt;&lt;/p&gt;
    &lt;blockquote&gt;&lt;/blockquote&gt;`</pre>

    ## 生成上级元素：^

    上级 （Climb-up）元素是什么意思呢？前面咱们说过了生成下级元素的符号“&gt;”，当使用 div&gt;ul&gt;li 的指令之后，再继续写下去，那么后续内容都是在 li 下级的。如果我想编写一个跟 ul 平级的 span 标签，那么我需要先用 “^” 提升一下层次。例如：
    <pre>div&gt;ul&gt;li^span</pre>
    就会生成如下结构：
    <pre>&lt;div&gt;
        &lt;ul&gt;
            &lt;li&gt;&lt;/li&gt;
        &lt;/ul&gt;
        &lt;span&gt;&lt;/span&gt;
    &lt;/div&gt;</pre>
    如果我想相对与 div 生成一个平级元素，那么就再上升一个层次，多用一个“^”符号：
    <pre>div&gt;ul&gt;li^^span</pre>

    ## 重复生成多份：*

    特别是一个无序列表，ul 下面的 li 肯定不只是一份，通常要生成很多个 li 标签。那么我们可以直接在 li 后面 * 上一些数字：
    <pre>ul&gt;li*5</pre>
    这样就直接生成五个项目的无序列表了。如果想要生成多份其他结构，方法类似。

    ## 生成分组：()

    用括号进行分组，这样可以更加明确要生成的结构，特别是层次关系，例如：
    <pre>`div&gt;(header&gt;ul&gt;li*2&gt;a)+footer&gt;p`</pre>
    这样很明显就可以看出层次关系和并列关系，生成如下结构：
    <pre>`&lt;div&gt;
        &lt;header&gt;
            &lt;ul&gt;
                &lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
                &lt;li&gt;&lt;a href=""&gt;&lt;/a&gt;&lt;/li&gt;
            &lt;/ul&gt;
        &lt;/header&gt;
        &lt;footer&gt;
            &lt;p&gt;&lt;/p&gt;
        &lt;/footer&gt;
    &lt;/div&gt;`</pre>
    此外，分组还可以很方便的结合上面说的 “*” 符号生成重复结构：
    <pre>`(div&gt;dl&gt;(dt+dd)*3)+footer&gt;p`</pre>
    生成结构：
    <pre>`&lt;div&gt;
        &lt;dl&gt;
            &lt;dt&gt;&lt;/dt&gt;
            &lt;dd&gt;&lt;/dd&gt;
            &lt;dt&gt;&lt;/dt&gt;
            &lt;dd&gt;&lt;/dd&gt;
            &lt;dt&gt;&lt;/dt&gt;
            &lt;dd&gt;&lt;/dd&gt;
        &lt;/dl&gt;
    &lt;/div&gt;
    &lt;footer&gt;
        &lt;p&gt;&lt;/p&gt;
    &lt;/footer&gt;`</pre>

    ## 生成自定义属性：[attr]

    a 标签中往往需要附带 href 属性和 title 属性，如果我们想生成一个 href 为 “http://www.qianxingzhem.com” ，title 为“潜行者m 博客”的 a 标签，可以这样写：
    <pre>a[href="http://www.qianxingzhem.com" title="潜行者m 博客"]</pre>
    其他标签和属性都类似。

    ## 对生成内容编号：$

    例如无序列表，我想为五个个 li 增加一个 class 属性值 item1 ，然后依次递增从 1-5，那么就需要使用 $ 符号：
    <pre>`ul&gt;li.item$*5`</pre>
    这样就生成了如下结构：
    <pre>&lt;ul&gt;
     &lt;li class="item1"&gt;&lt;/li&gt;
     &lt;li class="item2"&gt;&lt;/li&gt;
     &lt;li class="item3"&gt;&lt;/li&gt;
     &lt;li class="item4"&gt;&lt;/li&gt;
     &lt;li class="item5"&gt;&lt;/li&gt;
    &lt;/ul&gt;</pre>
    $ 就表示一位数字，只出现一个的话，就从1开始。如果出现多个，就从0开始。如果我想生成三位数的序号，那么要写三个 $：
    <pre>`ul&gt;li.item$$$*5`</pre>
    输出：
    <pre>`&lt;ul&gt;
        &lt;li class="item001"&gt;&lt;/li&gt;
        &lt;li class="item002"&gt;&lt;/li&gt;
        &lt;li class="item003"&gt;&lt;/li&gt;
        &lt;li class="item004"&gt;&lt;/li&gt;
        &lt;li class="item005"&gt;&lt;/li&gt;
    &lt;/ul&gt;`</pre>
    只能这样单调的生成序号？对于强大的 Emmet 来说，肯定不会会了，我们也可以在 $ 后面增加 @- 来实现倒序排列：
    <pre>`ul&gt;li.item$@-*5`</pre>
    生成如下结构：
    <pre>`&lt;ul&gt;
        &lt;li class="item5"&gt;&lt;/li&gt;
        &lt;li class="item4"&gt;&lt;/li&gt;
        &lt;li class="item3"&gt;&lt;/li&gt;
        &lt;li class="item2"&gt;&lt;/li&gt;
        &lt;li class="item1"&gt;&lt;/li&gt;
    &lt;/ul&gt;`</pre>
    同样，我们也可以使用 @N 指定开始的序号：
    <pre>`ul&gt;li.item$@3*5`</pre>
    这样就会从 3 开始排序，生成如下代码：
    <pre>`&lt;ul&gt;
        &lt;li class="item3"&gt;&lt;/li&gt;
        &lt;li class="item4"&gt;&lt;/li&gt;
        &lt;li class="item5"&gt;&lt;/li&gt;
        &lt;li class="item6"&gt;&lt;/li&gt;
        &lt;li class="item7"&gt;&lt;/li&gt;
    &lt;/ul&gt;`</pre>
    配合上面倒序输出，可以这样写：
    <pre>`ul&gt;li.item$@-3*5`</pre>
    生成的就是以 3 为底倒序：
    <pre>`&lt;ul&gt;
        &lt;li class="item7"&gt;&lt;/li&gt;
        &lt;li class="item6"&gt;&lt;/li&gt;
        &lt;li class="item5"&gt;&lt;/li&gt;
        &lt;li class="item4"&gt;&lt;/li&gt;
        &lt;li class="item3"&gt;&lt;/li&gt;
    &lt;/ul&gt;`</pre>

    ## 生成文本内容：{}

    上面讲解了如何生成 HTML 标签，那里面的内容呢？当然也可以生成了：
    <pre>`a[href="http://www.qianxingzhem.com"]{点击这里到 潜行者m 的博客}`</pre>
    这样就生成了一个到我博客的超链接了。在生成内容的时候，特别要注意前后的符号关系，虽然 a&gt;{Click me} 和 a{Click me} 生成的结构是相同的，但是加上其他的内容就不一定了，例如：
    <pre>`&lt;!-- a{click}+b{here} --&gt;
    &lt;a href=""&gt;click&lt;/a&gt;&lt;b&gt;here&lt;/b&gt;

    &lt;!-- a&gt;{click}+b{here} --&gt;
    &lt;a href=""&gt;click&lt;b&gt;here&lt;/b&gt;&lt;/a&gt;`</pre>
    这样就生成了完全不同的结构，注意这些小细节哦。

    ##  不要有空格

    在写指令的时候，你可能为了代码的可读性，使用一些空格什么的排版一下。这就会导致代码无法使用。例如下面这句：
    <pre>`(header &gt; ul.nav &gt; li*5) + footer

而去掉空格之后，就可以正常执行生成结构了。HTML 语法部分说完了，现在回头看看第一篇文字，你是否已经看懂了那一串指令？下一篇将会讲解快速编写 CSS 的技巧。