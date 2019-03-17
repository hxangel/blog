---
title: Mac下安装MongoDB教程
tags:
  - 数据库
id: 457
categories:
  - 编程
date: 2013-05-14 21:29:19
---

在mac下面如何安装[MongoDB](http://www.mongodb.org/ "MongoDB")呢，其实方法很简单。按照官方的三种方法安装就可以了。我这里是针对PHP的安装。多了一个PHP的MongoDB扩展安装。

A.执行终端命令

<pre>brew install mongodb</pre>

当然。这是在你安装好[Homebrew](https://github.com/mxcl/homebrew "homebrew")的情况下。假如没有安装的话请猛戳[这里](http://mxcl.github.io/homebrew/ "homebrew")

至此MongoDB已经安装完成。

B.接下来执行命令即可启动MongoDB

<pre>mongod</pre>

C.现在要做的就是把PHP对MongoDB的支持扩展安装上。直接执行如下命令

<pre>pecl install  mongo</pre>

这里需要说明的是你需要安装好pear才可以执行这个命令。而且要有安装autoconf工具，phpize才可以自动配置到PHP的扩展目录

在php.ini中添加

<pre>extension=mongo.so</pre>

重启PHP-FPM以及Web Server软件（如Nginx或Apache）

新建一个PHP文件，加入以下代码

<pre class="lang:php decode:true ">$mongo = new Mongo("mongodb://localhost:27017",array("connect"=&gt;TRUE));
        $mongo-&gt;connect();
        $db = $mongo-&gt;selectDB('test');
         $obj = new stdClass();
        $obj-&gt;name = 'MongoDB';
        $obj-&gt;age = 25;
        $dataA = $db-&gt;testdb;
        $dataA-&gt;insert($obj);
        $r = $dataA-&gt;find();
        echo $obj-&gt;name; 
        $mongo-&gt;close();</pre>

&nbsp;