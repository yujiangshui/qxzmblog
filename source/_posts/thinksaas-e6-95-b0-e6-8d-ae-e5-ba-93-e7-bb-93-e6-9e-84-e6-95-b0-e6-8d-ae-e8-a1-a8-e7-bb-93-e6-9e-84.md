title: "ThinkSAAS 数据库结构 -> 数据表结构"
tags:
  - ThinkSAAS
id: 1061
categories:
  - 网站与后台开发
date: 2012-08-19 14:57:56
---

注:这段时间,要用来研究一套系统ThinkSAAS,一个目前还不是很成熟的轻量化论坛系统.

看到很多app都需要数据库的操作,再看了一下,好像没有关于数据库结构的文章,然后我就整理了一下.

这是第一篇文章,关于数据表的结构,之后会陆续把一些app开发常用的数据表的结构整理出来.

完全是音译,有部分还是不理解功能是什么,还望邱君和高手把这部分用处说一下,不确定的后面有"???"

+-------------------------------------------------------------------+

| ts_anti_email                                =&gt; 阻止邮件名单

| ts_anti_ip                                      =&gt; 禁止IP

| ts_anti_word                                =&gt;禁止关键词

| ts_area                                          =&gt;用户区域

| ts_area_city                                  =&gt;用户居住城市

| ts_area_province                         =&gt;用户居住省

| ts_article                                       =&gt;文章列表

| ts_article_cate                              =&gt;文章目录

| ts_article_comment                    =&gt;文章评论

| ts_attach                                      =&gt;附件列表

| ts_feed                                         =&gt;订阅列表

| ts_group                                      =&gt;小组列表

| ts_group_cates                           =&gt;小组分类

| ts_group_options                       =&gt;小组配置

| ts_group_topics                          =&gt;小组帖子

| ts_group_topics_add                  =&gt;添加小组主题???

| ts_group_topics_collects           =&gt;收藏主题?

| ts_group_topics_comments     =&gt;小组主题评论

| ts_group_topics_type                =&gt;小组主题类别

| ts_group_users                          =&gt;小组成员

| ts_home_info                             =&gt;首页信息

| ts_mail_options                         =&gt;邮件配置就是系统发邮件的配置

| ts_message                                =&gt;消息

| ts_photo                                     =&gt;照片列表

| ts_photo_album                         =&gt;相册列表

| ts_photo_comment                    =&gt;照片评论

| ts_photo_options                        =&gt;照片选项

| ts_session                                    =&gt;session 你懂得

| ts_system_options                      =&gt;系统配置

| ts_tag                                           =&gt;标签列表

| ts_tag_article_index                    =&gt;文章标签指数???

| ts_tag_group_index                   =&gt;小组标签指数???

| ts_tag_photo_index                  =&gt;图片标签指数???

| ts_tag_topic_index                    =&gt;主题标签指数???

| ts_tag_user_index                      =&gt;用户标签指数???

| ts_user                                          =&gt;用户列表

| ts_user_follow                             =&gt;用户关注跟随

| ts_user_gb                                  =&gt;用户留言

| ts_user_info                                   =&gt;用户信息

| ts_user_invites                            =&gt;邀请用户

| ts_user_open                              =&gt;第三方登录

| ts_user_options                           =&gt;用户选项

| ts_user_role                               =&gt;用户参与任务

| ts_user_scores                          =&gt;用户积分

+----------------------------------------------------------------------+