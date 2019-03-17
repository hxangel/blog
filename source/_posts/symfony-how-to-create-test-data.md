---
title: symfony 测试数据的编写
id: 23
categories:
  - 编程
date: 2012-04-11 13:30:09
tags:
---

symfony里面用到yaml貌似比较多，先来唠叨几句,这里关于yaml是个什么东东，yaml干什么用的，我就不说了。由于yaml格式要求相当的严格，因此这里顺便说说yaml 的一些注意事项：

1.  注意缩进 ，2.  注意字段后面的空格 ，3.  注意对齐，4.  不要使用Tab来缩进，5.  不要在全角字符状态下输入分号与空格， 

下面来一段演示代码：
<pre lang="yaml" line="1">#@file /data/fixtures/region.yml
# 我是注释，前面加个#号
#假如这里是地区信息的yaml文件
Region:
  NestedSet: true#分号后面跟空格，是Region Model的参数，缩进俩空格
  worldwide:#与NestedSet 同级，首字母需对齐与上级有俩空格的缩进
    name: 'Worldwide'
    children:#worldwide 有很多仔，用children
      Asia:
        name: 'Asia'#这里分号可以不要,但是在带有分号或者是其他冲突的数据时请加上
        children:
          Eastern_Asia:
            name: 'Eastern Asia'
            children:
              CN:
                name: 'China'
                code: 'CN'</pre>

实例中主要就是一个分级关系。上下级托行并缩进。

## symfony 测试数据的编写

* * *

1.  普通的测试数据
如schema代码如下：
<pre lang="yaml" line="1">Category:
  columns:
    name: string(50)
    decription: string(1000)
Content:
  actAs:
    Timestampable: ~#不解释
  columns:
    title: string(250)
    content: clob
    view_count: integer
    reconmmend_level:
      type: enum
      values: [0,1,2]
      default: 2
    category_id: integer
  relations:#关系
    Category:
      local: category_id
      foreign: id
      foreignAlias: ContentsComment:
  actAs:
    Timestampable: ~
  columns:
    body: clob
    user_id: integer
    content_id: integer
  relations:
    Content:
      local: content_id
      foreign: id
      foreignAlias: Comments</pre>

那么测试数据应该格式如下:
<pre lang="yaml" line="1">Category:
  c1:
    name: 新闻
    decription: 最新新闻
  c2:
    name: 咨询
    decription: 最新咨询
  c3:
    name: 软文
    decription: 软文频道
Content:
   t1: #文章1,命名随便,但须不要要重复
    title: 新闻1
    content: 新闻１的内容
    view_count: 6
    reconmmend_level: 0
    Category: c1
    Comments: [m1,m2]#我有两条评论
   t2:#文章2
    title: 咨询1
    content: 咨询１的内容
    view_count: 8
    reconmmend_level: 1
    Category: c2
Comment:
   m1:
    body: 很好很强大
   m2:
    body: 介个灰常棒，信不信由你，反正我是不信
</pre>

这个例子比较全面,涉及到表与表之间的关系,如一篇文章有多条评论.

2.  下面来说下最常用的,加入了I18n<pre lang="yaml" line="1">Article:
  actAs:
    Timestampable: ~
    I18n:
      fields: [ title, body ]  columns:
    title: { type: string(255), notnull: true }
    body: { type: clob, notnull: true }
    author: { type: string(255), notnull: false }
</pre>