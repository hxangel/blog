---
title: MySQL 编译安装
id: 589
categories:
  - Linux系统
date: 2013-11-08 00:19:04
tags:
---

最近各种工作没有状态，本来很想写点心情日志啥的。可惜文笔有限制，就当在这里抱怨一下。MySQL 编译安装各种疼。顺便整理下笔记，不说了。都是泪。

－－－－－－－－－－－－－－－土豪金分割线－－－－－－－－－－－－－－－－－－－－
直入主题：依赖安装
安装环境：centos 6.4 x86_64
安装c＋＋编译环境：
<pre class="lang:sh decode:true ">

yum install gcc gcc-c++ ncurses-devel</pre>
bision：
<pre class="lang:sh decode:true ">

cd /usr/local/src 
wget http://ftp.gnu.org/gnu/bison/bison-2.7.1.tar.gz
tar -zxf bison-2.7.1.tar.gz
cd bison-2.7.1
./configure
make &amp;&amp; sudo make install
cd ..</pre>
cmake：
<pre class="lang:sh decode:true ">

wget http://www.cmake.org/files/v2.8/cmake-2.8.11.tar.gz
tar -zxf cmake-2.8.11.tar.gz
cd cmake-2.8.11
./bootstrap
make
sudo make install
或者
./configure
gmake
sudo make install
cd ..</pre>
<pre class="lang:default decode:true ">

curl -O http://cdn.mysql.com/Downloads/MySQL-5.6/mysql-5.6.12.tar.gz
tar -zxf mysql-5.6.12
cd mysql-5.6.12

#添加执行用户名和组
groupadd mysql
useradd -g mysql mysql

#开始编译安装
cmake -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
-DMYSQL_UNIX_ADDR=/tmp/mysql.sock \
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DWITH_EXTRA_CHARSETS=all \
-DWITH_MYISAM_STORAGE_ENGINE=1 \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_MEMORY_STORAGE_ENGINE=1 \
-DWITH_READLINE=1 \
-DENABLED_LOCAL_INFILE=1 \
-DMYSQL_DATADIR=/var/mysql/data \
-DMYSQL_USER=mysql
make -j8
make install

#改变所有者及控制权限
chmod +w /usr/local/mysql
chown -R mysql:mysql /usr/local/mysql
mkdir -p /var/mysql/
mkdir -p /var/mysql/data/
mkdir -p /var/mysql/log/
chown -R mysql:mysql /var/mysql/

#配置文件及安装服务
cd support-files/
cp my-default.cnf  /var/mysql/my.cnf
cp mysql.server /etc/rc.d/init.d/mysqld
chmod +x /etc/init.d/mysqld
chkconfig --level 345 mysqld on

#初始化数据库
/usr/local/mysql/scripts/mysql_install_db \
--defaults-file=/etc/my.cnf \
--basedir=/usr/local/mysql \
--datadir=/var/mysql/data \
--user=mysql

#建立软链接
ln -s /usr/local/mysql/bin/mysqladmin /usr/bin/
ln -s /usr/local/mysql/bin/mysql /usr/bin/

#启动MySQL服务
service mysqld start
#修改root帐户密码
mysqladmin -u root password 123456

#登陆MySQL
mysql -uroot -p

#创建一个MySQL 帐户
CREATE USER 'ryan'@'localhost' IDENTIFIED BY 'some_pass';#some_pass就是ryan帐户密码

#对用户ryan进行授权，当然你最好不要这么做
GRANT ALL PRIVILEGES ON *.* TO 'ryan'@'%'  IDENTIFIED BY 'some_pass'  WITH GRANT OPTION;

#刷新权限
flush privileges;

#修改默认的引擎
set global storage_engine=MYISAM
set storage_engine=MYISAM</pre>
写的简单，很少文字说明，当给自己参考。收工！