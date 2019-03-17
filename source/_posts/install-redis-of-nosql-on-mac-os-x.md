---
title: Mac 下载安装Redis
id: 465
categories:
  - 编程
date: 2013-05-14 22:49:48
tags:
---

直入主题。当然安装Redis方法不唯一。我这里讲源码编译方式。

A.到Redis官方下载最新的稳定版本源码包或者利用Curl以及其他的工具下载
<pre class="lang:sh decode:true">curl －O http://redis.googlecode.com/files/redis-2.6.13.tar.gz</pre>
B.下载完成后进行输入下面命令解压Redis压缩包
<pre class="lang:sh decode:true">tar vzxf redis-2.6.13.tar.gz</pre>
C.进入Redis解压后的目录进行编译安装
<pre class="lang:default decode:true">cd redis-2.6.13
make 
sudo make install</pre>
当你看到4个Install的高亮。说明已经安装完成

D.建立配置文件以及对配置文件进行修改
<pre class="lang:sh decode:true">sudo cp  redis.conf /private/etc/

sudo vi /private/etc/redis.conf</pre>
找到daemonize 把 后面的no改成yes，不然每次启动会占用一个终端的session。

其他的配置根据需要来。我这里不啰嗦。然后保持退出
<pre class="lang:default decode:true">:wq!</pre>
E.给启动命令加上参数
<pre class="lang:default decode:true">alias redis-server="redis-server /etc/redis.conf"</pre>
这样保证每次加载的时候都使用你编辑好的配置文件。

F.安装PHP Redi扩展 这里采用PECl安装方式
<pre class="lang:default decode:true">sudo pecl install redis</pre>
执行完毕后说明已经安装完成，编辑php.ini 加入下面这一句
<pre class="lang:default decode:true">extension=redis.so</pre>
然后重启web 服务并重启PHP-FPM,在phpinfo中查看是否配置成功。

G.开启Redis，并进行测试

先执行如下命令启动Redis
<pre class="lang:default decode:true">sudo redis-server</pre>
然后新建一个PHP文件,加入以下代码
<pre class="lang:default decode:true">&lt;?php
$redis = new Redis();

$redis-&gt;connect('127.0.0.1', 6379);

$redis-&gt;connect('127.0.0.1'); // port 6379 by default

$redis-&gt;connect('127.0.0.1', 6379, 60); // 2.5 sec timeout.

$redis-&gt;set('test','Hello World');

echo $redis-&gt;get('test');</pre>
保存后访问该文件。看下是否成功返回数据。