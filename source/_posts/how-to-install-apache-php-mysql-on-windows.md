---
title: 最新php环境apache+php+mysql配置
tags:
  - apache+php+mysql
  - mysql
  - php
  - phpMyAdmin
  - 下载地址
  - 最新
  - 最新php环境
id: 253
categories:
  - Linux系统
date: 2011-02-16 17:34:00
---

## apache+php+mysql下载(for windows)

* * *
最新apache下载地址：[httpd-2.2.17-win32-x86-no_ssl.msi](http://apache.etoak.com//httpd/binaries/win32/httpd-2.2.17-win32-x86-no_ssl.msi)&#160;&#160;&#160; |&#160;&#160; [更多版本点击此处](http://httpd.apache.org/download.cgi)   

最新php下载地址：[php-5.3.5-nts-Win32-VC6-x86.msi](http://windows.php.net/downloads/releases/php-5.3.5-nts-Win32-VC6-x86.msi "http://windows.php.net/downloads/releases/php-5.3.5-nts-Win32-VC6-x86.msi") 或者 [php-5.3.5-nts-Win32-VC6-x86.zip](http://windows.php.net/downloads/releases/php-5.3.5-nts-Win32-VC6-x86.zip "http://windows.php.net/downloads/releases/php-5.3.5-nts-Win32-VC6-x86.zip")&#160; |&#160; [更多版本请移驾到官方](http://windows.php.net/download/)

最新mysql下载地址：[http://dev.mysql.com/downloads/mysql/#downloads](http://dev.mysql.com/downloads/mysql/#downloads "http://dev.mysql.com/downloads/mysql/#downloads")

phpmyadmin下载地址：[phpMyAdmin-3.3.9.2-all-languages.7z](http://sourceforge.net/projects/phpmyadmin/files%2FphpMyAdmin%2F3.3.9.2%2FphpMyAdmin-3.3.9.2-all-languages.7z/download#%21md5%2140af9db4cf535ee67481ffb324cb85ae)

<font color="#ff0000">PS</font>: php <font color="#ff0000">VC9</font>是专门为<font color="#ff0000">IIS</font>定制的，<font color="#ff0000">VC6</font> 是为了其他<font color="#ff0000">WEB服务软件</font>提供的，所以这里下载<font color="#ff0000">VC6</font>的版本！

## apache+php+mysql安装与配置

* * *

首先安装apache，apache引导安装后，输入：[http://localhost](http://localhost) 或者 [http://127.0.0.1](http://127.0.0.1)&#160; 测试 会出现“It works”的字样。

PS:你也可以使用其他的如[http://web](http://web)&#160; 只需在
  > %windir%\System32\drivers\etc\hosts  

的后面加上
  > 127.0.0.1&#160;&#160;&#160;&#160;&#160;&#160;&#160; web  

保存，但是在安装apache的时候域名处请填写web如下图：

[![001](http://www.vkilo.com/wp-content/uploads/2011/02/001.jpg "001")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

接下来安装php，因为我这里采用的是windows 安装文件，安装的时候选apache 2.2.x Module

安装完成后会在apache 配置文件(httpd.conf)最后加上
  > #BEGIN PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL       
> PHPIniDir &quot;&quot;       
> LoadModule php5_module &quot;php5apache2_2.dll&quot;       
> #END PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL  

后面安装mysql 安装的时候可以选择数据库安装的位置 你也可以安装后再修改 如图：

[![004](http://www.vkilo.com/wp-content/uploads/2011/02/004.jpg "004")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

### 配置mysql(方法很多，仅供参考)

1、这里选择详细配置（detailed configuration）

[![005](http://www.vkilo.com/wp-content/uploads/2011/02/005.jpg "005")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

2、这里选服务器（server machine）

[![006](http://www.vkilo.com/wp-content/uploads/2011/02/006.jpg "006")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

3、这里选Non-Transactional Database Only

[![007](http://www.vkilo.com/wp-content/uploads/2011/02/007.jpg "007")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

4、这里选默认编码类型

[![008](http://www.vkilo.com/wp-content/uploads/2011/02/008.jpg "008")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

5、这里把选框都勾上

[![010](http://www.vkilo.com/wp-content/uploads/2011/02/010.jpg "010")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

6、这里需要输入你的密码然后重复输入密码（要是有三个输入框第一个留空，后面两个输入密码即可），选框都不用选

[![011](http://www.vkilo.com/wp-content/uploads/2011/02/011.jpg "011")](http://www.vkilo.com "最新php环境apache+php+mysql配置")

到此下一步配置完成！

### 修改配置apache 

打开httpd.conf&#160; 

1、修改默认文件，找到DirectoryIndex 替换成如下的样子（根据个人需要）
  > &lt;IfModule dir_module&gt;      
> &#160;&#160;&#160; DirectoryIndex index.html index.php default.php default.html 
> 
> index.htm index.html      
> &lt;/IfModule&gt;  

2、修改网站目录 找到DocumentRoot 在双引号内输入你的网站路径如我的
  > DocumentRoot &quot;F:/htdocs&quot;  

然后找到&lt;Directory &quot;Your apache path/htdocs&quot;&gt;

同样在双引号内输入你网站路径跟上面路径保持一致如我的
  > &lt;Directory &quot;F:/htdocs&quot;&gt;
> 
> 这里略去很多英文字
> 
> &lt;/Directory&gt;  

3、修改php支持找到
  > #BEGIN PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL      
> PHPIniDir &quot;&quot;       
> LoadModule php5_module &quot;php5apache2_2.dll&quot;       
> #END PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL  

修改为你的php所在的路径 如我的：
  > #BEGIN PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL       
> PHPIniDir &quot;D:/web/php&quot;       
> LoadModule php5_module &quot;D:/web/php/php5apache2_2.dll&quot;       
> #END PHP INSTALLER EDITS - REMOVE ONLY ON UNINSTALL  

### 配置php

最新php默认支持mysql 也不需要修改extension_dir&#160; 如果不能正常运行 。则：打开php.ini 找到Dynamic Extensions

再后面加入：
  > extension=php_curl.dll      
> extension=php_gd2.dll       
> extension=php_mbstring.dll       
> extension=php_mysql.dll       
> extension=php_pdo_mysql.dll       
> extension=php_pdo_odbc.dll       
> extension=php_xmlrpc.dll  

开启mysql 支持 ，找到; extension_dir = &quot;ext&quot;

修改为extension_dir=&quot;D:\web\php\ext&quot;

PS:我的安装目录分别为

apache：D:\web\Apache

mysql：D:\web\MySQL

php：D:\web\php

mysql数据库：D:\web\Data\data

所以以上安装路径如跟我的不同需做对应的更改。

## php环境测试

* * *
新建文件info.php   

写入代码：
  > &lt;?php phpinfo(); ?&gt;  

放到网站对应根目录重启apache 打开[http://localhost/info.php](http://localhost/info.php) 查看配置好的php环境功能

测试mysql

新建文件db_test.php

写入代码：
  > &lt;?php      
> $connect=mysql_connect(“127.0.0.1″,”root”,”mysql数据库密码”);       
> if(!$connect) echo “[恭喜俺 出错鸟](http://www.vkilo.com)”;       
> else echo “[恭喜俺！链接成功](http://www.vkilo.com)”;       
> mysql_close();       
> ?&gt;  

打开[http://localhost/db_test.php](http://localhost/db_test.php) 查看效果

不明白请本站冒个泡泡，更多请参考官方手册。