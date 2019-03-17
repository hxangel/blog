---
title: wordpress更换域名及设置方法
tags:
  - wordpress如何更换域名
  - wordpress换域名完美301重定向
id: 204
categories:
  - 笔记分享
date: 2010-12-23 22:03:14
---

### wordpress如何更换域名

在phpmyadmin中执行下面的查询语句
<pre>UPDATE wp_options SET option_value = replace(option_value,'http://kimozh.net','http://www.vkilo.com') WHERE option_name = 'home' OR option_name = 'siteurl';

UPDATE wp_posts SET post_content = replace(post_content,'http://kimozh.net','http://www.vkilo.com');

UPDATE wp_posts SET guid = replace(guid,'http://kimozh.net','http://www.vkilo.com');</pre>
domain格式 [http://www.vkilo.com](http://www.vkilo.com) 最后不要带"/";

如果出错，检查是不是标点符号有问题！

wordpress换域名完美301重定向

假如你的linux主机只需要把 .htaccess 文件 WordPress 部分修改成下面样子：
<div>
<pre># BEGIN WordPress
<span style="color: #0000ff;">&lt;</span><span style="color: #800000;">IfModule</span> <span style="color: #ff0000;">mod_rewrite</span>.<span style="color: #ff0000;">c</span><span style="color: #0000ff;">&gt;</span>
Options +FollowSymLinks
RewriteEngine on
rewritecond %{http_host} ^www.old.com [nc]
rewriterule ^(.*)$ http://www.new.com/$1 [L,R=301]
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">IfModule</span><span style="color: #0000ff;">&gt;</span>
# END WordPress</pre>
</div>
假如是windows主机需修改 wordpress 根目录下的 **wp-blog-header.php** ，并在文件开头 &lt;?php 之后加入以下代码：
<div>
<pre>if (strtolower($_SERVER['SERVER_NAME'])!='www.kimozh.net')
{
$URIRedirect=$_SERVER['REQUEST_URI'];
if(strtolower($URIRedirect)=="/index.php")
{
$URIRedirect="/";
}
header('HTTP/1.1 301 Moved Permanently');
header('Location:http://www.vkilo.com'.$URIRedirect);
exit();
}</pre>
</div>
注意把[www.kimozh.net](http://www.vkilo.com)改成你自己的新玉米