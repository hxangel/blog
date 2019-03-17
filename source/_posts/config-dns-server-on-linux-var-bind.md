---
title: linux 通过bind下搭建DNS Server
id: 614
categories:
  - Linux系统
date: 2014-04-24 22:42:47
tags:
---

作为一个web开发人员，开发过程中肯定有很多项目需要分配不同的域名来访问，这样避免一个localhost不够用和避免加端口各种麻烦，以及子目录超级麻烦等问题。那么很多时候需要在开发环境上门绑定多个域名。假如是一个团队开发。那么每个人都去修改hosts是一件很悲剧的事情，那么你需要的就是一台内部的dns服务器。其实本人对理论这块了解甚少，所以重在实用。

### 1.理论普及

#### DNS服务器分为:

1.  master（主DNS服务器）：拥有区域数据的文件，并对整个区域数据进行管理。
2.  slave(从服务器或叫辅助服务器）：拥有主DNS服力器的区域文件的副 本，辅助主DNS服务器对客户端进行解析，当主DNS服务器坏了后，可以完全接替主服务器的工作。
3.  forward:将任何查询请求都转发给其他服务器。起到一个代理的作用。
4.  cache:缓存服务器。
5.  hint：根DNS internet服务器集。

### 2.软件安装

<pre class="lang:sh decode:true ">#For Debian/Ubuntu
apt-get install bind*
#For CentOS/Fedora/RedHat
yum install bind*</pre>
其他的根据自己的功能需要安装相应的安装包。

### 3.配置

通过以下命令
<pre class="lang:sh decode:true ">cat /etc/sysconfig/named</pre>
可以看到系统将named的目录指向哪里。
<pre class="lang:sh decode:true ">/etc/sysconfig/named  #由该文件控制是否动chroot及其他参数
/etc/named.conf       #配置文件
/var/named/           #数据库文件（如正向、反向、根文件）存放位置
/var/run/named:       #named程序默认将pid文件放置此目录下</pre>
这里主要需要配置的文件就/etc/named.conf
<pre class="lang:default decode:true ">vim /etc/named.conf
#修改文件 主意any的地方根据自己需要
options {
    listen-on port 53 { any; };
    listen-on-v6 port 53 { ::1; };
    directory     "/var/named";
    dump-file     "/var/named/data/cache_dump.db";
    statistics-file "/var/named/data/named_stats.txt";
    memstatistics-file "/var/named/data/named_mem_stats.txt";
    query-source    port 53;  
    query-source-v6 port 53;
    allow-query     { any; };
};
logging {
        channel default_debug {
                file "data/named.run";
                severity dynamic;
        };
};
view localhost_resolver {
    match-clients         { any; };
    match-destinations { any; };
    recursion yes;
    include "/etc/named.rfc1912.zones";
};</pre>
假如我想绑定ryan.com到192.168.0.5
<pre class="lang:default decode:true ">vim /etc/named.rfc1912.zones
#附加以下内容并保存
zone "ryan.com" IN {
        type master;
        file "ryan.com.zone";
        allow-update { none; };
};
zone "ryan.com-arpa" IN {
        type master;
        file "ryan.com.arpa";
        allow-update { none; };
};</pre>
然后分别新建两个文件
<pre class="lang:default decode:true ">vim /var/named/ryan.com.zone
#插入以下内容并保存
$TTL 1D
@       IN SOA  ryan.com.  root. (
                                        0       ; serial
                                        1D      ; refresh
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum
@       NS      ryan.com.
@       A       192.168.1.5
www     A       192.168.1.5
*       A       192.168.1.5</pre>
<pre class="lang:default decode:true">vim /var/named/ryan.com.arpa
#插入以下内容并保存
$TTL 1D
@       IN SOA  ryan.com.  root. (
                                        0       ; serial
                                        1D      ; refresh
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum
@       NS      ryan.com.
@       A       192.168.1.5
5       PTR     www.ryan.com.</pre>
以上编辑基本上完成了基本配置，接下来修改你机器的域名解析

<pre class="lang:default decode:true " >vim /etc/resolv.conf
#修改（没有添加）指向dns所在的机器ip
nameserver 192.168.0.5
</pre> 
到此配置结束。

### 4.测试

<pre class="lang:default decode:true " >#设置开机启动
chkconfig named --level 235 on
#开启dns 服务器
service named start
#如已经开启请使用下面的命令重启
service named restart</pre> 
然后在终端输入

<pre class="lang:default decode:true " >nslookup 
#enter进入nslookup的会话后直接输入需要测试的域名看看返回的结果是否正确如：
vkilo.ryan.com
</pre> 
还有一些如dig之类的测试命令，根据个人喜好和要求。还有主从这里就不再累赘。
< 收工>