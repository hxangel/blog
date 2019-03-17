---
title: symfony 环境配置
id: 5
date: 2012-04-04 15:17:32
tags:
---

## symfony 闲话

* * *
 对于php我也就是能看懂一点代码，要我写一个留言板，里面加些杂七杂八的东西（如：ajax,json，jquery,缓存，模板，MVC）的话可能半年的时间不知道弄不弄的出来。因为这些东西只是看起来面熟，不知道是干啥用的。上帝，请原谅我的无知。最近闲来无事，到说听闻php框架可以不需要20分钟就能完成一个很牛X的东西，我就琢磨着，以前也没有做过啥玩意儿，出于好奇，开始了symfony的学习，我这人有一个缺点，就是做事有头无尾，开始是激情和调子都比较高，不过被他们折腾的死去活来的时候就有放弃的思想；这次我对自己提出点希望，就是希望能坚持到底。多嘴完毕，just do it.  

## php环境搭建for symfony
 <p> 

* * *
 我原来曾经做过一篇文章(笔记) named: [最新php环境apache+php+mysql配置](www.kimozh.net/253-link.html) 当然现在不是最新的了。下面我不得不引用一段话。  > <p>最新apache下载地址：[httpd-2.2.22-win32-x86-no_ssl.msi](http://labs.mop.com/apache-mirror//httpd/binaries/win32/httpd-2.2.22-win32-x86-no_ssl.msi)&nbsp;&nbsp; |&nbsp;&nbsp; [更多版本点击此处](http://httpd.apache.org/download.cgi)  <p>最新php下载地址：[Installer](http://windows.php.net/downloads/releases/php-5.3.10-Win32-VC9-x86.msi) 或者 [Zip](http://windows.php.net/downloads/releases/php-5.3.10-Win32-VC9-x86.zip)&nbsp; |&nbsp; [更多版本请移驾到官方](http://windows.php.net/download/)  <p>最新mysql下载地址：[http://dev.mysql.com/downloads/mysql/#downloads](http://dev.mysql.com/downloads/mysql/#downloads)（注册need）  <p>phpmyadmin下载地址：[phpMyAdmin-3.3.9.2-all-languages.7z](http://sourceforge.net/projects/phpmyadmin/files%2FphpMyAdmin%2F3.3.9.2%2FphpMyAdmin-3.3.9.2-all-)  <p>安装我就不说了。装软件根据个人喜好，安装到对应的位置就OK了。我个人一般软件都不喜欢装到目录带空格的。这里貌似没有什么影响，就随便。  <p>接下来是配置php的配置基本不需要我们管（intaller的安装方法）。  <p>看看apache  
> 
> ### 修改配置apache
>  <p>打开httpd.conf&nbsp; <p>1、修改默认文件，找到DirectoryIndex 替换成如下的样子（根据个人需要）  > <p>&lt;IfModule dir_module&gt;
> > &nbsp;&nbsp;&nbsp; DirectoryIndex index.html index.php default.php default.html  <p>index.htm index.html
> > &lt;/IfModule&gt; 
> 
> 2、修改网站目录 找到DocumentRoot 在双引号内输入你的网站路径如我的  > <p>DocumentRoot "F:/htdocs" 
> 
> 然后找到&lt;Directory "Your apache path/htdocs"&gt;  <p>同样在双引号内输入你网站路径跟上面路径保持一致如我的  > <p>&lt;Directory "F:/htdocs"&gt;  <p>这里略去很多英文字  <p>&lt;/Directory&gt; 
> 
> 3、修改php支持找到  > <p>#BEGIN PHP INSTALLER EDITS – REMOVE ONLY ON UNINSTALL
> > PHPIniDir ""
> > LoadModule php5_module "php5apache2_2.dll"
> > #END PHP INSTALLER EDITS – REMOVE ONLY ON UNINSTALL 
> 
> 修改为你的php所在的路径 如我的：  > <p>#BEGIN PHP INSTALLER EDITS – REMOVE ONLY ON UNINSTALL
> > PHPIniDir "D:/web/php"#php安装的目录
> > LoadModule php5_module "D:/web/php/php5apache2_2.dll"#确保这个破玩意儿路径是对的
> > #END PHP INSTALLER EDITS – REMOVE ONLY ON UNINSTALL  <p>然后把LoadModule vhost_alias_module modules/mod_vhost_alias.so和  <p>LoadModule rewrite_module modules/mod_rewrite.so以及Include conf/extra/httpd-vhosts.conf前面的#号去掉。  <p>对应需要起用rewrite功能（也就是让.htaccess起作用 it is just my mean ）
> > 
> > AllowOverride None
> > Order deny,allow
> > Deny from all
> > 
> > 修改成
> > AllowOverride None
> > 
> > Order allow,deny
> > Allow from all
> > 
> > 把apache重启放一边，配置mysql
> > 
> > 双击MySQL安装目录下的bin目录下的MySQLInstanceConfig.exe，选择detailed configuration，下一步——&gt;选择server machine ,下一步——&gt;Non-Transactional Database Only——&gt;下一步——&gt;选择手动（manual setting）,下一步——&gt;默认，勾勾都打上，下一步——&gt;选择手动（最后一项），选择utf8,下一步——&gt;勾上，下一步，设置密码for root user of mysql,后面最后那个勾勾掉进入最后一步点击中间那个button，完成配置。
> > 
> > &nbsp; 

到目前测试下你的环境，就基本上可以满足symfony的需求了。后面说下新建项目的问题。

这里简单的说下项目的地址配置，去下载一个sf_sandbox（这个名字我灰常喜欢），把文件拷贝到你放网站项目的地方，然后我们apache配置使其能够正常访问。

在pathToApache\conf\extra 下有httpd-vhosts.conf 这么一个文件（也就是刚刚去掉#号的原因，因为我们现在需要用到它），用编辑器打开

我们在后面增加以下代码
 > Listen 81
> NameVirtualHost *:81
> &lt;VirtualHost *:81&gt;
> &nbsp;&nbsp;&nbsp; DocumentRoot "D:/htdocs/web"#这里表示你项目存放位置下的web目录如我的放到d:\htdocs下
> &nbsp;&nbsp;&nbsp; ServerName localhost：81
> &nbsp;&nbsp;&nbsp; #ErrorLog "logs/dummy-host.localhost-error.log"
> &nbsp;&nbsp;&nbsp; #CustomLog "logs/dummy-host.localhost-access.log" common
> &lt;/VirtualHost&gt;这样再我们访问localhost:81是不是出现奇迹就在于你。完事了。因为时间问题所以弄的有点草率，有空会修改的更好些。谢谢阅读。