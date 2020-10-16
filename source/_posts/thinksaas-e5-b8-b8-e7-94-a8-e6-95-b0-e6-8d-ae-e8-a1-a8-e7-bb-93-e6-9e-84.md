title: ThinkSAAS 常用数据表结构
tags:
  - ThinkSAAS
id: 1226
categories:
  - 网站与后台开发
date: 2012-08-30 21:46:02
---

本文仅列出开发ThinkSAAS app比较常用的数据表结构，这样，可以方便构造sql语句，对数据库的信息进行操作。

## ts_article                                       =&gt;文章列表

+---------------+------------+------+-----+---------------------+----------------+
| Field         | Type       | Null | Key | Default             | Extra |
+---------------+------------+------+-----+---------------------+----------------+
| articleid     | int(11)    | NO   | PRI | NULL                | auto_increment |
| userid        | int(11)    | NO   |     | 0                   | |
| cateid        | int(11)    | NO   |     | 0                   | |
| title         | char(64)   | NO   |     |                     | |
| content       | text       | NO   |     | NULL                ||
| path          | char(32)   | NO   |     |                     | |
| photo         | char(32)   | NO   |     |                     | |
| isaudit       | tinyint(1) | NO   |     | 0                   | |
| isrecommend   | tinyint(1) | NO   |     | 0                   | |
| count_comment | int(11)    | NO   |     | 0                   | |
| addtime       | datetime   | NO   |     | 0000-00-00 00:00:00 | |
| isrecommend   | tinyint(1) | NO   |     | 0                   ||
| count_comment | int(11)    | NO   |     | 0                   ||
|addtime       | datetime   | NO   |     | 0000-00-00 00:00:00 |
+---------------+------------+------+-----+---------------------+----------------+

## ts_article_cate                              =&gt;文章目录

+----------+----------+------+-----+---------+----------------+
| Field    | Type     | Null | Key | Default | Extra                   |
+----------+----------+------+-----+---------+----------------+
| cateid   | int(11)  | NO   | PRI | NULL    | auto_increment |
| catename | char(16) | NO   |     |         |                |
| orderid  | int(11)  | NO   |    | 0       |                |
+----------+----------+------+-----+---------+----------------+

##  ts_article_comment                    =&gt;文章评论

+-----------+---------+------+-----+---------+----------------+
| Field     | Type    | Null | Key | Default | Extra          |
+-----------+---------+------+-----+---------+----------------+
| commentid | int(11) | NO   | PRI | NULL    | auto_increment |
| articleid | int(11) | NO   |     | 0       |                |
| userid    | int(11) | NO   |     | 0       |                |
| content   | text    | NO   |     | NULL    |                |
| addtime   | int(11) | NO   |     | 0       |                |
+-----------+---------+------+-----+---------+----------------+

## ts_group                                      =&gt;小组列表

+-------------------+------------+------+-----+---------+----------------+
| Field             | Type       | Null | Key | Default | Extra          |
+-------------------+------------+------+-----+---------+----------------+
| groupid           | int(11)    | NO   | PRI | NULL    | auto_increment |
| userid            | int(11)    | NO   | MUL | 0       |                |
| cateid            | int(11)    | NO   | MUL | 0       |                |
| cateid2           | int(11)    | NO   |     | 0       |                |
| cateid3           | int(11)    | NO   |     | 0       |                |
| groupname         | char(32)   | NO   | MUL |         |                |
| groupname_en      | char(32)   | NO   |     |         |                |
| groupdesc         | text       | NO   |     | NULL    |                |
| path              | char(32)   | NO   |     |         |                |
| groupicon         | char(32)   | NO   |     |         |                |
| count_topic       | int(11)    | NO   |     | 0       |                |
| count_topic_today | int(11)    | NO   |     | 0       |                |
| count_user        | int(11)    | NO   |     | 0       |                |
| count_topic_audit | int(11)    | NO   |     | 0       |                |
| joinway           | tinyint(1) | NO   |     | 0       |                |
| role_leader       | char(32)   | NO   |     | ??      |                |
| role_admin        | char(32)   | NO   |     | ???     |                |
| role_user         | char(32)   | NO   |     | ??      |                |
| addtime           | int(11)    | YES  |     | 0       |                |
| isrecommend       | tinyint(1) | NO   |     | 0       |                |
| isopen            | tinyint(1) | NO   |     | 0       |                |
| isaudit           | tinyint(1) | NO   |     | 0       |                |
| ispost            | tinyint(1) | NO   |     | 0       |                |
| isshow            | tinyint(1) | NO   | MUL | 0       |                |
| ispostaudit       | tinyint(1) | NO   |     | 0       |                |
| uptime            | int(11)    | NO   |     | 0       |                |
+-------------------+------------+------+-----+---------+----------------+

## ts_group_cates                           =&gt;小组分类

+-------------+----------+------+-----+---------+----------------+
| Field       | Type     | Null | Key | Default | Extra          |
+-------------+----------+------+-----+---------+----------------+
| cateid      | int(11)  | NO   | PRI | NULL    | auto_increment |
| catename    | char(32) | NO   |     |         |                |
| referid     | int(11)  | NO   | MUL | 0       |                |
| count_group | int(11)  | NO   |     | 0       |                |
| uptime      | int(11)  | NO   |     | 0       |                |
+-------------+----------+------+-----+---------+----------------+

## ts_group_options                       =&gt;小组配置

+-------------+-----------+------+-----+---------+-------+
| Field       | Type      | Null | Key | Default | Extra |
+-------------+-----------+------+-----+---------+-------+
| optionname  | char(12)  | NO   | PRI |         |       |
| optionvalue | char(255) | NO   |     |         |       |
+-------------+-----------+------+-----+---------+-------+

## ts_group_topics                          =&gt;小组帖子

+---------------+--------------+------+-----+---------+----------------+
| Field         | Type         | Null | Key | Default | Extra          |
+---------------+--------------+------+-----+---------+----------------+
| topicid       | int(11)      | NO   | PRI | NULL    | auto_increment |
| typeid        | int(11)      | NO   | MUL | 0       |                |
| groupid       | int(11)      | NO   | MUL | 0       |                |
| userid        | int(11)      | NO   | MUL | 0       |                |
| appkey        | char(32)     | NO   |     | group   |                |
| appname       | char(32)     | NO   |     | ??      |                |
| appaction     | char(32)     | NO   |     | topic   |                |
| appid         | int(11)      | NO   |     | 0       |                |
| title         | char(64)     | NO   | MUL |         |                |
| content       | text         | NO   |     | NULL    |                |
| thread_type   | char(16)     | NO   |     |         |                |
| path          | char(32)     | NO   |     |         |                |
| photo         | char(32)     | NO   |     |         |                |
| photoshow     | tinyint(1)   | NO   |     | 0       |                |
| attach        | char(32)     | NO   |     |         |                |
| attachname    | char(64)     | NO   |     |         |                |
| attachshow    | tinyint(1)   | NO   |     | 0       |                |
| attachscore   | int(11)      | NO   |     | 0       |                |
| music         | varchar(512) | NO   |     |         |                |
| video         | varchar(512) | NO   |     |         |                |
| count_comment | int(11)      | NO   |     | 0       |                |
| count_view    | int(11)      | NO   |     | 0       |                |
| count_love    | int(11)      | NO   |     | 0       |                |
| istop         | tinyint(1)   | NO   |     | 0       |                |
| isshow        | tinyint(1)   | NO   |     | 0       |                |
| isclose       | int(4)       | NO   |     | 0       |                |
| color         | int(4)       | NO   |     | 0       |                |
| iscomment     | tinyint(1)   | NO   |     | 0       |                |
| isposts       | tinyint(1)   | NO   |     | 0       |                |
| isaudit       | tinyint(1)   | NO   |     | 0       |                |
| addtime       | int(11)      | YES  |     | 0       |                |
| uptime        | int(11)      | NO   |     | 0       |                |
+---------------+--------------+------+-----+---------+----------------+

## ts_group_topics_comments     =&gt;小组主题评论

+------------+----------+------+-----+---------+----------------+
| Field      | Type     | Null | Key | Default | Extra          |
+------------+----------+------+-----+---------+----------------+
| commentid  | int(11)  | NO   | PRI | NULL    | auto_increment |
| referid    | int(11)  | NO   | MUL | 0       |                |
| topicid    | int(11)  | NO   | MUL | 0       |                |
| userid     | int(11)  | NO   | MUL | 0       |                |
| content    | text     | NO   |     | NULL    |                |
| path       | char(32) | NO   |     |         |                |
| photo      | char(32) | NO   |     |         |                |
| attach     | char(32) | NO   |     |         |                |
| attachname | char(64) | NO   |     |         |                |
| addtime    | int(11)  | YES  |     | 0       |                |
+------------+----------+------+-----+---------+----------------+

## ts_group_users                          =&gt;小组成员

+-----------+------------+------+-----+---------+-------+
| Field     | Type       | Null | Key | Default | Extra |
+-----------+------------+------+-----+---------+-------+
| userid    | int(11)    | NO   | PRI | 0       |       |
| groupid   | int(11)    | NO   | PRI | 0       |       |
| isadmin   | int(11)    | NO   |     | 0       |       |
| isfounder | tinyint(1) | NO   |     | 0       |       |
| addtime   | int(11)    | NO   |     | 0       |       |
+-----------+------------+------+-----+---------+-------+

## ts_photo                                     =&gt;照片列表

+-------------+------------+------+-----+---------+----------------+
| Field       | Type       | Null | Key | Default | Extra          |
+-------------+------------+------+-----+---------+----------------+
| photoid     | int(11)    | NO   | PRI | NULL    | auto_increment |
| albumid     | int(11)    | NO   |     | 0       |                |
| userid      | int(11)    | NO   |     | 0       |                |
| photoname   | char(64)   | NO   |     |         |                |
| phototype   | char(32)   | NO   |     |         |                |
| path        | char(32)   | NO   |     |         |                |
| photourl    | char(120)  | NO   |     |         |                |
| photosize   | char(32)   | NO   |     |         |                |
| photodesc   | char(120)  | NO   |     |         |                |
| count_view  | int(11)    | NO   |     | 0       |                |
| isrecommend | tinyint(1) | NO   |     | 0       |                |
| addtime     | int(11)    | NO   |     | 0       |                |
+-------------+------------+------+-----+---------+----------------+

## ts_photo_album                         =&gt;相册列表

+-------------+--------------+------+-----+---------+----------------+
| Field       | Type         | Null | Key | Default | Extra          |
+-------------+--------------+------+-----+---------+----------------+
| albumid     | int(11)      | NO   | PRI | NULL    | auto_increment |
| userid      | int(11)      | NO   | MUL | 0       |                |
| path        | char(32)     | NO   |     |         |                |
| albumface   | char(64)     | NO   |     |         |                |
| albumname   | char(64)     | NO   |     |         |                |
| albumdesc   | varchar(400) | NO   |     |         |                |
| count_photo | int(11)      | NO   |     | 0       |                |
| count_view  | int(11)      | NO   |     | 0       |                |
| isrecommend | tinyint(1)   | NO   | MUL | 0       |                |
| addtime     | int(11)      | NO   |     | 0       |                |
| uptime      | int(11)      | NO   |     | 0       |                |
+-------------+--------------+------+-----+---------+----------------+

## ts_photo_comment                    =&gt;照片评论

+-----------+-----------+------+-----+---------+----------------+
| Field     | Type      | Null | Key | Default | Extra          |
+-----------+-----------+------+-----+---------+----------------+
| commentid | int(11)   | NO   | PRI | NULL    | auto_increment |
| referid   | int(11)   | NO   | MUL | 0       |                |
| photoid   | int(11)   | NO   | MUL | 0       |                |
| userid    | int(11)   | NO   | MUL | 0       |                |
| content   | char(255) | NO   |     |         |                |
| addtime   | int(11)   | YES  |     | 0       |                |
+-----------+-----------+------+-----+---------+----------------+

## ts_tag                                           =&gt;标签列表

+---------------+------------+------+-----+---------+----------------+
| Field         | Type       | Null | Key | Default | Extra          |
+---------------+------------+------+-----+---------+----------------+
| tagid         | int(11)    | NO   | PRI | NULL    | auto_increment |
| tagname       | char(16)   | NO   | UNI |         |                |
| count_user    | int(11)    | NO   |     | 0       |                |
| count_group   | int(11)    | NO   |     | 0       |                |
| count_topic   | int(11)    | NO   |     | 0       |                |
| count_bang    | int(11)    | NO   |     | 0       |                |
| count_article | int(11)    | NO   |     | 0       |                |
| count_photo   | int(11)    | NO   |     | 0       |                |
| isenable      | tinyint(1) | NO   |     | 0       |                |
| uptime        | int(11)    | NO   |     | 0       |                |
+---------------+------------+------+-----+---------+----------------+

## ts_system_options                      =&gt;系统配置

+-------------+-----------+------+-----+---------+-------+
| Field       | Type      | Null | Key | Default | Extra |
+-------------+-----------+------+-----+---------+-------+
| optionname  | char(32)  | NO   | PRI |         |       |
| optionvalue | char(255) | NO   |     |         |       |
+-------------+-----------+------+-----+---------+-------+

## ts_user                                          =&gt;用户列表

+----------+----------+------+-----+---------+----------------+
| Field    | Type     | Null | Key | Default | Extra          |
+----------+----------+------+-----+---------+----------------+
| userid   | int(11)  | NO   | PRI | NULL    | auto_increment |
| pwd      | char(32) | NO   | MUL |         |                |
| salt     | char(32) | NO   |     |         |                |
| email    | char(32) | NO   | UNI |         |                |
| resetpwd | char(32) | NO   |     |         |                |
+----------+----------+------+-----+---------+----------------+

## ts_user_gb                                  =&gt;用户留言

+----------+---------------+------+-----+---------------------+----------------+
| Field    | Type          | Null | Key | Default             | Extra          |
+----------+---------------+------+-----+---------------------+----------------+
| id       | int(11)       | NO   | PRI | NULL                | auto_increment |
| reid     | int(11)       | NO   |     | 0                   |                |
| userid   | int(11)       | NO   | MUL | 0                   |                |
| touserid | int(11)       | NO   | MUL | 0                   |                |
| content  | varchar(2000) | NO   |     |                     |                |
| addtime  | datetime      | NO   |     | 0000-00-00 00:00:00 |                |
+----------+---------------+------+-----+---------------------+----------------+

## ts_user_info                                   =&gt;用户信息

+-----------------+-------------+------+-----+---------+-------+
| Field           | Type        | Null | Key | Default | Extra |
+-----------------+-------------+------+-----+---------+-------+
| userid          | int(11)     | NO   | UNI | 0       |       |
| ucid            | int(11)     | NO   | MUL | 0       |       |
| fuserid         | int(11)     | NO   | MUL | 0       |       |
| username        | char(32)    | NO   | UNI |         |       |
| email           | char(32)    | NO   | PRI |         |       |
| sex             | tinyint(1)  | NO   |     | 0       |       |
| phone           | char(16)    | NO   |     |         |       |
| roleid          | int(11)     | NO   |     | 1       |       |
| province        | int(11)     | NO   |     | 0       |       |
| city            | int(11)     | NO   |     | 0       |       |
| area            | int(11)     | NO   |     | 0       |       |
| areaid          | int(11)     | NO   |     | 0       |       |
| path            | char(32)    | NO   |     |         |       |
| face            | char(64)    | NO   |     |         |       |
| signed          | char(64)    | NO   |     |         |       |
| blog            | char(32)    | NO   |     |         |       |
| about           | char(255)   | NO   |     |         |       |
| ip              | varchar(16) | NO   |     |         |       |
| address         | char(64)    | NO   |     |         |       |
| qq_openid       | char(32)    | NO   | MUL |         |       |
| qq_access_token | char(32)    | NO   |     |         |       |
| count_score     | int(11)     | NO   |     | 0       |       |
| count_follow    | int(11)     | NO   |     | 0       |       |
| count_followed  | int(11)     | NO   |     | 0       |       |
| isadmin         | tinyint(1)  | NO   |     | 0       |       |
| isenable        | tinyint(1)  | NO   |     | 0       |       |
| isverify        | tinyint(1)  | NO   |     | 0       |       |
| verifycode      | char(11)    | NO   |     |         |       |
| thems_other     | tinyint(1)  | NO   |     | 0       |       |
| addtime         | int(11)     | NO   |     | 0       |       |
| uptime          | int(11)     | YES  |     | 0       |       |
+-----------------+-------------+------+-----+---------+-------+

## ts_user_options                           =&gt;用户选项

+-------------+-----------+------+-----+---------+-------+
| Field       | Type      | Null | Key | Default | Extra |
+-------------+-----------+------+-----+---------+-------+
| optionname  | char(12)  | NO   | PRI |         |       |
| optionvalue | char(255) | NO   |     |         |       |
+-------------+-----------+------+-----+---------+-------+

这里只包含常用的数据表结构，至于其他的数据表请看这里[ThinkSAAS 数据库结构 -&gt; 数据表结构](http://www.qianxingzhem.com/post-1061.html)

至于本文中未列出的数据表，请在mysql命令行，使用describe命令查看。