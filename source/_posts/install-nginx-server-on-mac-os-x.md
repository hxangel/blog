---
title: Mac 下Nginx的安装教程
id: 468
categories:
  - 编程
date: 2013-05-14 23:12:49
tags:
---

听闻Nginx有很多优点，我不知道。你也许知道。下面简述安装过程。Mac下编译安装Nginx需要有好多支持库，不过我默认最简单的安装，其他扩展我也用不到。开始

A.[PCRE](http://www.pcre.org/)是必须的。所以先安装PCRE

在终端执行如下命令下载最新稳定源码包
<pre class="lang:sh decode:true">curl -O ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.32.tar.gz</pre>
然后执行解压安装
<pre class="lang:sh decode:true">tar -vzxf pcre-8.32.tar.gz 

cd pcre-8.32

./configure 

make 

sudo make install</pre>
分别执行以上几条命令。加入没有错的话，安装完成。

B.安装Nginx，终端返回上层目录。下载最新稳定版Nginx源码包，并解压进入到Nginx的源码目录
<pre class="lang:sh decode:true">cd ..

curl -O http://nginx.org/download/nginx-1.4.0.tar.gz

tar -vzxf nginx-1.4.0.tar.gz 

cd nginx-1.4.0</pre>
配置Nginx
<pre class="lang:sh decode:true"> ./configure</pre>
这里说明一点。我这里是默认的配置。假如有特殊需要的话。请后面跟参数。如ssl之类的。请参阅官方安装文档及参数说明。这里不一一例举。配置完成后。假如没有出错的话。执行以下两条命令进行编译安装。
<pre class="lang:default decode:true">make 
sudo make install</pre>
上面命令没有出错的情况下说明已经安装完成 ，接下来做一个连接，方便使用Nginx的命令
<pre class="lang:default decode:true">sudo ln -s /usr/local/nginx/sbin/nginx /usr/local/bin/nginx</pre>
然后再输入
<pre class="lang:default decode:true">sudo nginx</pre>
就可以启动Nginx了。然后可以打开127.0.0.1进行测试就可以看到Nginx的默认页面（假如没有端口冲突等问题存在，Nginx使用80端口，可能与其他web服务软件冲突，请先停止在打开Nginx）；

C.Nginx 控制命令如下
<pre class="lang:default decode:true">nginx -s stop
nginx -s quit
nginx -s reopen
nginx -s reload</pre>
D.Nginx 的默认配置文件在
<pre class="lang:default decode:true">/usr/local/nginx/conf/nginx.conf</pre>
&nbsp;

&nbsp;

&nbsp;