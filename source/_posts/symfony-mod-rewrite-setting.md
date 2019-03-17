---
title: symfony 之mod_rewrite配置
id: 6
date: 2012-04-05 15:29:56
tags:
---

前段时间折腾zend framework ，然后访问目录默认并非网站的根目录，甚是郁闷；接下来symfony也是如此。假如我用的是虚拟主机，那么应用程序根目录肯定是入口，访问的时候不会再带一个web啥的跟到后面怪难看了。

默认的symfony的.htaccess文件如下：
 > Options +FollowSymLinks +ExecCGI
> 
> &lt;IfModule mod_rewrite.c&gt;
> &nbsp; RewriteEngine On
> 
> &nbsp; # uncomment the following line, if you are having trouble
> &nbsp; # getting no_script_name to work
> &nbsp; #RewriteBase /
> 
> &nbsp; # we skip all files with .something
> &nbsp; #RewriteCond %{REQUEST_URI} \..+$
> &nbsp; #RewriteCond %{REQUEST_URI} !\.html$
> &nbsp; #RewriteRule .* - [L]
> 
> &nbsp; # we check if the .html version is here (caching)
> &nbsp; RewriteRule ^$ index.html [QSA]
> &nbsp; RewriteRule ^([^.]+)$ $1.html [QSA]
> &nbsp; RewriteCond %{REQUEST_FILENAME} !-f
> 
> &nbsp; # no, so we redirect to our front web controller
> &nbsp; RewriteRule ^(.*)$ index.php [QSA,L]
> &lt;/IfModule&gt; 

这个放到了web目录下，于是要么就域名绑定到web目录，要么就绑定到根目录，然后跟一个[http://host/web/](http://host/web/)这样地址来访问。现在我们把这个修改成：
 > Options +FollowSymLinks +ExecCGI
> 
> &lt;IfModule mod_rewrite.c&gt;
> &nbsp; RewriteEngine On
> &nbsp; 
> &nbsp; # we skip all files in /web
> &nbsp; RewriteCond %{REQUEST_URI} ^/web/
> &nbsp; RewriteRule .* - [L]
> &nbsp; 
> &nbsp; # we rewrite all other files with .something to /web
> &nbsp; RewriteCond %{REQUEST_URI} \..+$
> &nbsp; RewriteCond %{REQUEST_URI} !\.html$
> &nbsp; RewriteRule ^(.*)$ /web/$1 [L]
> &nbsp; 
> &nbsp; # !!! UNTESTED !!! ##################################
> &nbsp; # we check if the .html version is in /web (caching)
> &nbsp; RewriteRule ^$ /web/index.html [QSA]
> &nbsp; RewriteRule ^([^.]+)$ /web/$1.html [QSA]
> &nbsp; #####################################################
> &nbsp; 
> &nbsp; # no, so we redirect to our front web controller
> &nbsp; RewriteRule ^(.*)$ /web/index.php [QSA,L]
> &nbsp; 
> &lt;/IfModule&gt; 

 然后将其移动到网站根目录。直接访问index.php你会发现世界是多么的美好。睡觉！ 