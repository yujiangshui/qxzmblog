title: WordPress 中的条件判断标签大全
id: 1764
categories:
  - 未分类
tags:
---

在 WordPress 中使用条件判断标签，可以非常灵活的根据一些条件实现一些功能。网上有很多类似的帖子和文章，但是只是一些简单的 is 函数，只是简单的说明。相比之下，[官方的文档](http://codex.wordpress.org/Conditional_Tags)就全面的多。然后[潜行者m](http://www.qianxingzhem.com)为了方便，就拿来翻译一下，部分删减，有能力的最好还是去官方看，翻译难免有不恰当的地方。

功能介绍

条件判断标签（Conditional Tags）通常用来根据匹配条件来控制内容的展示。例如，你想只在首页中显示一个文章片段，就可以使用 is_home() 这个条件判断标签。

警告，你只能在 posts_selection 钩子之前使用条件查询标签。对于主题来说，条件判断标签如果被你用在 functions.php 文件中的话，可能会出现意外情况。

所有的条件判断标签都会根据情况返回一个确定的值，True 或者 False。还有些标签可以接受一些参数。

判断主页

is_home()

判断当前页面是否为主页面，是的话，就会返回 True。

判断首页页面（Front Page）

is_front_page()

当文章或者是页面被访问的时候，只要这个页面与你后台设置的首页一致，就会返回 True。后台的阅读设置中，可以设置首页展示文章或者一个静态页面。

文章页面中的条件判断

is_single()

对于文章（包括附件页面、自定义文章类型）被访问的时候，返回 True。对于页面，返回 False。

is_single('17')

文章 ID 为17的文章被访问时，返回 True。

is_single('Irish Stew')

当文章标题或者别名为 Irish Stew 的页面被访问时，返回 True。

is_single( array( 17, 'beef-stew', 'Irish Stew' ) )

当文章的ID、别名、标题分别为 17、beef-stew、Irish Stew 的页面被访问时，返回 True

is_single( array( 17, 19, 1, 11 ) )

功能同上。根据 ID 判断。

is_single( array( 'beef-stew', 'pea-soup', 'chili' ) )

功能同上。根据文章标题、别名判断。

注意，这个功能并不会判断所传递的参数值是 ID、文章名、别名。如果你传递了 17，它会判断出 ID 为17的文章，也可能判断出文章名、别名为17的文章。

判断置顶文章（Sticky Post）

is_sticky()

当置顶文章被访问，返回 True。

is_sticky( '17' )
当 ID 为17的置顶文章被访问时返回 True。

判断文章类型（post type）

get_post_type()

这个函数不能算是一个条件判断标签，但是可以返回当前文章的文章类型。然后使用 if 语句进行判断，例如：if ( 'book' == get_post_type() )

is_singular()

当 is_single, is_page, and is_attachment 标签返回 True 的时候，这个标签返回 True。此外，它支持传递自定义文章类型，例如：is_singular('book')

post_type_exists()

当传递的文章类型是存在的，就会返回 True。但是它不会检测哪篇文章的明确文章类型。注意，这个函数取代了 3.0 版本中的 is_post_type 函数的功能。

判断文章类型的等级

is_post_type_hierarchical( $post_type )

检测 $post_type 是否设置了等级支持。has been set with hierarchical support when registered.
is_post_type_hierarchical( 'book' )
Returns true if the book post type was registered as having support for hierarchical.

A Post Type Archive

is_post_type_archive() : Returns true on any post type archive.
is_post_type_archive( $post_type ) : Returns true if on a post type archive page that matches $post_type (can be a single post type or an array of post types).

To turn on post type archives, use 'has_archive' =&gt; true, when registering the post type.
A Comments Popup

is_comments_popup()
When in Comments Popup window.

Any Page Containing Posts

comments_open()
When comments are allowed for the current Post being processed in the WordPress Loop.
pings_open()
When pings are allowed for the current Post being processed in the WordPress Loop.

A PAGE Page

This section refers to WordPress Pages, not any generic webpage from your blog, or in other words to the built in post_type 'page'.

is_page()
When any Page is being displayed.
is_page( 42 )
When Page 42 (ID) is being displayed.
is_page( 'About Me And Joe' )
When the Page with a post_title of "About Me And Joe" is being displayed.
is_page( 'about-me' )
When the Page with a post_name (slug) of "about-me" is being displayed.
is_page( array( 42, 'about-me', 'About Me And Joe' ) )
Returns true when the Pages displayed is either post ID = 42, or post_name is "about-me", or post_title is "About Me And Joe".
is_page( array( 42, 54, 6 ) )
Returns true when the Pages displayed is either post ID = 42, or post ID = 54, or post ID = 6.

Testing for paginated Pages

You can use this code to check whether you're on the nth page in a Post or PAGE Page that has been divided into pages using the <!--nextpage--> QuickTag. This can be useful, for example, if you wish to display meta-data only on the first page of a post divided into several pages.

Example 1

<!--?php 
 $paged = $wp_query-&gt;get( 'page' );

if ( ! $paged || $paged &lt; 2 )
{
// This is not a paginated page (or it's simply the first page of a paginated page/post)

}
else
{
// This is a paginated page.

}
?&gt;

Example 2

<!--?php 
 $paged = get_query_var( 'page' ) ? get_query_var( 'page' ) : false;
if ( $paged === false )
{
// This is not a paginated page (or it's simply the first page of a paginated page/post)

}
else
{
// This is a paginated page.

}
?&gt;

Testing for sub-Pages

There is no is_subpage() function yet, but you can test this with a little code:

Snippet 1

&nbsp;

global $post; // if outside the loop

if ( is_page() &amp;&amp; $post-&gt;post_parent ) {
// This is a subpage

} else {
// This is not a subpage
}
?&gt;

You can create your own is_subpage() function using the code in Snippet 2\. Add it to your functions.php file. It tests for a parent page in the same way as Snippet 1, but will return the ID of the page parent if there is one, or false if there isn't.

Snippet 2

function is_subpage() {
global $post; // load details about this page

if ( is_page() &amp;&amp; $post-&gt;post_parent ) { // test to see if the page has a parent
return $post-&gt;post_parent; // return the ID of the parent post

} else { // there is no parent so ...
return false; // ... the answer to the question is false
}
}

It is advisable to use a function like that in Snippet 2, rather than using the simple test like Snippet 1, if you plan to test for sub pages frequently.

To test if the parent of a page is a specific page, for instance "About" (page id pid 2 by default), we can use the tests in Snippet 3\. These tests check to see if we are looking at the page in question, as well as if we are looking at any child pages. This is useful for setting variables specific to different sections of a web site, so a different banner image, or a different heading.

Snippet 3

&nbsp;

if ( is_page( 'about' ) || '2' == $post-&gt;post_parent ) {
// the page is "About", or the parent of the page is "About"
$bannerimg = 'about.jpg';

} elseif ( is_page( 'learning' ) || '56' == $post-&gt;post_parent ) {
$bannerimg = 'teaching.jpg';

} elseif ( is_page( 'admissions' ) || '15' == $post-&gt;post_parent ) {
$bannerimg = 'admissions.jpg';

} else {
$bannerimg = 'home.jpg'; // just in case we are at an unclassified page, perhaps the home page
}

?&gt;

Snippet 4 is a function that allows you to carry out the tests above more easily. This function will return true if we are looking at the page in question (so "About") or one of its sub pages (so a page with a parent with ID "2").

Snippet 4

function is_tree( $pid ) { // $pid = The ID of the page we're looking for pages underneath
global $post; // load details about this page

if ( is_page($pid) )
return true; // we're at the page or at a sub page

$anc = get_post_ancestors( $post-&gt;ID );
foreach ( $anc as $ancestor ) {
if( is_page() &amp;&amp; $ancestor == $pid ) {
return true;
}
}

return false; // we arn't at the page, and the page is not an ancestor
}

Add Snippet 4 to your functions.php file, and call is_tree( 'id' ) to see if the current page is the page, or is a sub page of the page. In Snippet 3, is_tree( '2' ) would replace "is_page( 'about' ) || '2' == $post-&gt;post_parent" inside the first if tag.

Note that if you have more than one level of pages the parent page is the one directly above and not the one at the very top of the hierarchy.
Is a Page Template

Allows you to determine whether or not you are in a page template or if a specific page template is being used.

is_page_template()
Is a Page Template being used?
is_page_template( 'about.php' )
Is Page Template 'about' being used? Note that unlike with other conditionals, if you want to specify a particular Page Template, you need to use the filename, such as about.php or my_page_template.php.

A Category Page

is_category()
When any Category archive page is being displayed.
is_category( '9' )
When the archive page for Category 9 is being displayed.
is_category( 'Stinky Cheeses' )
When the archive page for the Category with Name "Stinky Cheeses" is being displayed.
is_category( 'blue-cheese' )
When the archive page for the Category with Category Slug "blue-cheese" is being displayed.
is_category( array( 9, 'blue-cheese', 'Stinky Cheeses' ) )
Returns true when the category of posts being displayed is either term_ID 9, or slug "blue-cheese", or name "Stinky Cheeses".
in_category( '5' )
Returns true if the current post is in the specified category id. read more
in_category( array( 1,2,3 ) )
Returns true if the current post is in either category 1, 2, or 3.
! in_category( array( 4,5,6 ) )
Returns true if the current post is NOT in either category 4, 5, or 6\. Note the ! at the beginning.

Note: Be sure to check your spelling when testing, "is" and "in" are a big difference.

See also is_archive() and Category Templates.
A Tag Page

is_tag()
When any Tag archive page is being displayed.
is_tag( 'mild' )
When the archive page for tag with the slug of 'mild' is being displayed.
is_tag( array( 'sharp', 'mild', 'extreme' ) )
Returns true when the tag archive being displayed has a slug of either "sharp", "mild", or "extreme".
has_tag()
When the current post has a tag. Must be used inside The Loop.
has_tag( 'mild' )
When the current post has the tag 'mild'.
has_tag( array( 'sharp', 'mild', 'extreme' ) )
When the current post has any of the tags in the array.

See also is_archive() and Tag Templates.
A Taxonomy Page

is_tax()
When any Taxonomy archive page is being displayed.
is_tax( 'flavor' )
When a Taxonomy archive page for the flavor taxonomy is being displayed.
is_tax( 'flavor', 'mild')
When the archive page for the flavor taxonomy with the slug of 'mild' is being displayed.
is_tax( 'flavor', array( 'sharp', 'mild', 'extreme' ) )
Returns true when the flavor taxonomy archive being displayed has a slug of either "sharp", "mild", or "extreme".
has_term()
Check if the current post has any of given terms. The first parameter should be an empty string. It expects a taxonomy slug/name as a second parameter.
has_term( 'green', 'color' )
When the current post has the term 'green' from taxonomy 'color'.
has_term( array( 'green', 'orange', 'blue' ), 'color' )
When the current post has any of the terms in the array.

See also is_archive().
A Registered Taxonomy

taxonomy_exists()
When a particular taxonomy is registered via register_taxonomy(). Formerly is_taxonomy(), which was deprecated in Version 3.0

An Author Page

is_author()
When any Author page is being displayed.
is_author( '4' )
When the archive page for Author number (ID) 4 is being displayed.
is_author( 'Vivian' )
When the archive page for the Author with Nickname "Vivian" is being displayed.
is_author( 'john-jones' )
When the archive page for the Author with Nicename "john-jones" is being displayed.
is_author( array( 4, 'john-jones', 'Vivian' ) )
When the archive page for the author is either user ID 4, or user_nicename "john-jones", or nickname "Vivian".

See also is_archive() and Author Templates.
A Multi-author Site

is_multi_author( )
When more than one author has published posts for a site. Available with Version 3.2.

A Date Page

is_date()
When any date-based archive page is being displayed (i.e. a monthly, yearly, daily or time-based archive).
is_year()
When a yearly archive is being displayed.
is_month()
When a monthly archive is being displayed.
is_day()
When a daily archive is being displayed.
is_time()
When an hourly, "minutely", or "secondly" archive is being displayed.
is_new_day()
If today is a new day according to post date. Should be used inside the loop.

See also is_archive().
Any Archive Page

is_archive()
When any type of Archive page is being displayed. Category, Tag, Author and Date based pages are all types of Archives.

A Search Result Page

is_search()
When a search result page archive is being displayed.

A 404 Not Found Page

is_404()
When a page displays after an "HTTP 404: Not Found" error occurs.

A Paged Page

is_paged()
When the page being displayed is "paged". This refers to an archive or the main page being split up over several pages and will return true on 2nd and subsequent pages of posts. This does not refer to a Post or Page whose content has been divided into pages using the <!--nextpage--> QuickTag. To check if a Post or Page has been divided into pages using the <!--nextpage--> QuickTag, see #Testing_for_paginated_Pages.

An Attachment

is_attachment()
When an attachment document to a post or Page is being displayed. An attachment is an image or other file uploaded through the post editor's upload utility. Attachments can be displayed on their own 'page' or template. For more information, see Using Image and File Attachments.

A Single Page, Single Post or Attachment

is_singular()
When any of the following return true: is_single(), is_page() or is_attachment().
is_singular( 'book' )
True when viewing a post of the Custom Post Types book.
is_singular( array( 'newspaper', 'book' ) )
True when viewing a post of the Custom Post Types newspaper or book.

A Syndication

is_feed()
When the site requested is a Syndication. This tag is not typically used by users; it is used internally by WordPress and is available for Plugin Developers.

A Trackback

is_trackback()
When the site requested is WordPress' hook into its Trackback engine. This tag is not typically used by users; it is used internally by WordPress and is available for Plugin Developers.

A Preview

is_preview()
When a single post being displayed is viewed in Draft mode.

Has An Excerpt

has_excerpt()
When the current post has an excerpt
has_excerpt( 42 )
When the post 42 (ID) has an excerpt.

<!--?php 
 // Get $post if you're inside a function
global $post;

if ( empty( $post-&gt;post_excerpt ) ) {
// This post has no excerpt
} else {
// This post has excerpt
}
?&gt;

Other Use

When you need to hide the auto displayed excerpt and only display your post's excerpts.

<!--?php if ( ! has_excerpt() ) {
 echo '';
} else {
the_excerpt();
}

Replace auto excerpt for a text or code.

<!--?php if ( ! has_excerpt() ) {?-->
<!-- you text or code -->
<!--?php } ?-->

Has A Nav Menu Assigned

has_nav_menu()
Whether a registered nav menu location has a menu assigned

Returns: assigned(true) or not(false)
Inside The Loop

in_the_loop()
Check to see if you are "inside the loop". Useful for plugin authors, this conditional returns as true when you are inside the loop.

Is Sidebar Active

is_active_sidebar()
Check to see if a given sidebar is active (in use). Returns true if the sidebar (identified by name, id, or number) is in use, otherwise the function returns false.

Part of a Network (Multisite)

is_multisite()
Check to see whether the current site is in a WordPress MultiSite install.

Main Site (Multisite)

is_main_site()
Determine if a site is the main site in a network.

Admin of a Network (Multisite)

is_super_admin()
Determine if user is a network (super) admin.

An Active Plugin

is_plugin_active()
Checks if a plugin is activated.

A Child Theme

is_child_theme()
Check whether a child theme is in use.

Theme supports a feature

current_theme_supports()
Check if various theme features exist.

Working Examples

Here are working samples to demonstrate how to use these conditional tags.
Single Post

This example shows how to use is_single() to display something specific only when viewing a single post page:

if ( is_single() ) {
echo 'This is just one of many fabulous entries in the ' . single_cat_title() . ' category!';
}

Other example how to use Conditional Tags into loop. choose display content or excerpt in the index.php, when this is unique archive for display single post, categories, home and page.

if ( is_home() || is_single() ) {
the_content();
}
else {
the_excerpt();
}

When you need display a code or element, in a place that is not the home page.

&nbsp;

Insert your markup ...

&nbsp;

Date-Based Differences

If someone browses our site by date, let's distinguish posts in different years by using different colors:

<!--?php 
 // this starts The Loop
if ( have_posts() ) : while ( have_posts() ) : the_post(); ?&gt;

## ">
<a title="Permanent Link to <?php the_title(); ?>" href="<?php the_permalink() ?>" rel="bookmark">
<!--?php the_title(); ?--></a>

&nbsp;

<!--?php 
 // are we showing a date-based archive?
if ( is_date() ) {
if ( date( 'Y' ) != get_the_date( 'Y' ) ) {
// this post was written in a previous year
// so let's style the content using the "oldentry" class
echo '
<div class="oldentry">';
} else {
echo '
<div class="entry">';
}
} else {
echo '
<div class="entry">';
}</div>
</div>
</div>
the_content( 'Read the rest of this entry »' );

?&gt;

Variable Sidebar Content

This example will display different content in your sidebar based on what page the reader is currently viewing.

&nbsp;
<div id="sidebar"><!--?php 
 // let's generate info appropriate to the page being displayed
if ( is_home() ) {
// we're on the home page, so let's show a list of all top-level categories
echo "

";
} elseif ( is_category() ) {
// we're looking at a single category view, so let's show _all_ the categories
echo "

";
} elseif ( is_single() ) {
// we're looking at a single page, so let's not show anything in the sidebar
} elseif ( is_page() ) {
// we're looking at a static page. Which one?
if ( is_page( 'About' ) ) {
// our about page.
echo "

This is my about page!

";
} elseif ( is_page( 'Colophon' ) ) {
echo "

This is my colophon page, running on WordPress " . bloginfo( 'version' ) . "

";
} else {
// catch-all for other pages
echo "

Vote for Pedro!

";
}
} else {
// catch-all for everything else (archives, searches, 404s, etc)
echo "

Pedro offers you his protection.

";
} // That's all, folks!
?&gt;
<div><input id="s" type="text" name="s" size="15" /> <input type="submit" value="<?php _e( 'Search' ); ?>" /></div>
</div>
&nbsp;

Helpful 404 Page

The Creating an Error 404 Page article has an example of using the PHP conditional function isset() in the Writing Friendly Messages section.
Dynamic Menu Highlighting

The Dynamic Menu Highlighting article discusses how to use the conditional tags to enable highlighting of the current page in a menu.
In a theme's footer.php file

At times queries performed in other templates such as sidebar.php may corrupt certain conditional tags. For instance, in header.php a conditional tag works properly but doesn't work in a theme's footer.php. The trick is to put wp_reset_query before the conditional test in the footer. For example:

<!--?php 
 wp_reset_query();
if ( is_page( '2' ) ) {
echo 'This is page 2!';
}
?&gt;

Conditional Tags Index
Aphabetical List

comments_open
has_tag
has_term
in_category
is_404
is_admin
is_archive
is_attachment
is_author
is_category
is_child_theme
is_comments_popup
is_date
is_day
is_feed
is_front_page
is_home
is_month
is_multi_author
is_multisite
is_main_site
is_page
is_page_template
is_paged
is_preview
is_rtl
is_search
is_single
is_singular
is_sticky
is_super_admin
is_tag
is_tax
is_time
is_trackback
is_year
pings_open

&nbsp;

&nbsp;

&nbsp;