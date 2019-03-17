---
title: php 实时输出显示
id: 618
categories:
  - 笔记分享
date: 2014-04-24 22:52:57
tags:
---

网上找了许多办法都行不通，经过半天的折腾。终于弄出来下面能够实时显示当前时间
<pre class="lang:default decode:true">&lt;?php
//ob_end_flush(); //关闭php缓存，或者在flush前ob_flush();

 //ie下 需要先发送256个字节, firefox 1024, chrome 2048
 date_default_timezone_set("PRC");//设置当前时区
set_time_limit(0);

for($i=1; $i&lt;=10; $i++)
{
    ob_end_clean();
    ob_start();
    echo str_repeat(" ", 4096);
    echo "Now is :". date("H:i:s")."&lt;br&gt;";
    echo str_repeat(" ", 4096);
    ob_flush(); //把php缓存推送到apache去，前面已经关闭了php缓存了，这里再推就报错了
//    flush(); //把apache缓存推送到浏览器去
    sleep(1);
}</pre>