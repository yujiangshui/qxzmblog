title: wordpress模板开发常用的函数
tags:
  - WP主题函数
id: 354
categories:
  - 网站与后台开发
date: 2012-01-19 12:31:55
---

最近自己研究设计了这个你现在看到的模板。设计的过程，也是一个学习的过程，通过各方面查找资料，一步一步的组合成了这个模板。用本文梳理以下用到的wp函数，以方便日后开发其他模板。

### 全局整体：

**&lt;?php get_header(); ?&gt;** ：得到头部代码函数。wp模板将一个页面分为header、sidebar、footer、body四个部分。并且将header、sidebar、footer这三个部分分割出去，作为独立文件方便重用。使用这个函数，表示把header.php这个文件包含进了本文件。

**&lt;?php get_sidebar(); ?&gt;**：得到边栏代码函数，用法同上。

**&lt;?php get_footer(); ?&gt;** ：得到底部代码函数，用法同上。

**&lt;?php wp_title('&amp;laquo;', true, 'right'); ?&gt;**：当访问一篇文章（或页面）的时候，网页标题将显示文章的标题。常在header.php编写如下语句：&lt;title&gt;&lt;?php wp_title('&amp;laquo;', true, 'right'); ?&gt;&lt;?php bloginfo('name'); ?&gt;&lt;/title&gt;。

**&lt;?php echo mb_strimwidth(strip_tags(apply_filters('the_content',$post-&gt;post_content)), 0, 400,"…"); ?&gt;**：使用本语句，截取本文章制定的前400个字符，用于首页显示文章摘要，具体请看：[解决wp首页无法显示摘要而显示全文的方法](http://www.qianxingzhem.com/post-330.html)。

**&lt;?php previous_posts_link(); ?&gt;**：当文章为列表时，且一页存放不开时，使用此函数，会显示“上一页”。

**&lt;?php next_posts_link(); ?&gt;**：同上功能，会显示“下一页”。

**&lt;?php bloginfo(); ?&gt;** ：顾名思义，这是一个显示博客信息的函数。具体请看：[wordpress中bloginfo()函数详解](http://www.qianxingzhem.com/post-364.html)

**&lt;?php home_url(); ?&gt;**：输出博客首页地址。

**&lt;?php _e('Not Found'); ?&gt;**：_e();函数是根据本地汉化包的对应内容显示相应信息的，比如：_e('Not Found');如果我的wordpress是英文版的，则会显示“Not Found”，如果是中文版的，汉化包内对应的是“没有发现”，则显示“没有发现”。

### 文章相关：

**&lt;?php the_category(' , ') ?&gt;**：显示文章所在分类。

**&lt;?php the_title(); ?&gt;**：显示文章的标题。

**&lt;?php  the_author(); ?&gt;**：显示本文的作者。

**&lt;?php the_content(); ?&gt;**：显示本文的内容。

**&lt;?php if (has_tag()) the_tags('', ',',''); ?&gt;**：判断本文是否有标签，如果有就显示出来，多个标签用“，”分割。

**&lt;?php edit_post_link('Edit', ''); ?&gt;**：如果你有编辑文章的权限，且登陆，会在添加此函数的地方发现“edit”链接，点击可以快速跳转后台，对此文章内容进行编辑。

**&lt;?php the_time('y年m月d日') ?&gt;**：显示此文章的发布时间，括号内可以自定义时间格式。

**&lt;?php previous_post_link(); ?&gt;**：上一篇文章的链接，显示上一篇文章的名字以及链接，注意区别前面的“上一页”函数。

**&lt;?php next_post_link(); ?&gt;**：下一篇文章的链接，功能同上。

**&lt;?php comments_template(); ?&gt;**：调用评论模板函数，使用此函数，会显示评论模板的内容。

以上就是WP模板开发中，最常遇到的调用信息的函数。特别需要注意的一点是，调用显示日志的函数必须包含在日志主循环中，即：

&lt;?php if(have_posts()) : ?&gt;
&lt;?php while(have_posts()) : the_post(); ?&gt;
&lt;?php endwhile; ?&gt;
&lt;?php else : ?&gt;
&lt;?php endif; ?&gt;

这段函数使用了一个if判断语句，中间包含了while循环语句，意思是如果有文章的话，就开始循环的the_post()，这样就能使用上面的调用相应文章作者、发布日期、文章分类、文章标签等内容。

目前[潜行者m](http://www.qianxingzhem.com)在编写一套比较[简单基础的wordpress模板制作教程](http://www.qianxingzhem.com/post-tag/wp%E6%A8%A1%E6%9D%BF%E5%BC%80%E5%8F%91)，有兴趣的朋友可以关注这里：[http://www.qianxingzhem.com/post-tag/wp%E6%A8%A1%E6%9D%BF%E5%BC%80%E5%8F%91](http://www.qianxingzhem.com/post-tag/wp%E6%A8%A1%E6%9D%BF%E5%BC%80%E5%8F%91)