---
title: 如何在RHEL/Centos/Fedora/下搭建vpn pptp 服务器
id: 710
categories:
  - Linux系统
date: 2015-03-29 12:16:17
tags:
---

用vpn已经有很多年，然而一直因为懒惰原因，所以一直都没有写关于如何搭建vpn服务器的文章，今年兴致所致，分享一下个人搭建vpn server的过程，写的简陋，请勿拍砖。vpn的使用非常广泛，可谓大多网虫和技术股都需要用到的东西，不过看下文之前请先看看自己的服务器是否支持pptp方式的vpn服务器，具体请执行命令
<pre class="lang:sh decode:true">modprobe ppp-compress-18 &amp;&amp; echo ok</pre>
假如输出ok请继续， 假如不ok，说明服务器不支持。下面的文章可能对你没啥用。

## 第一步：安装pptpd

通常情况下可以通过yum直接安装pptpd，执行
<pre class="lang:sh decode:true">yum list pptpd
</pre>
假如有则执行
<pre class="lang:sh decode:true">yum install pptpd
</pre>
如果没有需要到sf.net下载，执行如下命令进行安装
<pre class="lang:default decode:true">cd /usr/local/src

#For 64bit OS
wget http://poptop.sourceforge.net/yum/stable/packages/pptpd-1.4.0-1.el6.x86_64.rpm
rpm -Uhv pptpd-1.4.0-1.el6.x86_64.rpm

#For 32bit os
wget http://poptop.sourceforge.net/yum/stable/packages/pptpd-1.4.0-1.el6.i686.rpm
rmp -Uhv pptpd-1.4.0-1.el6.i686.rpm</pre>
到此pptpd vpn 服务器安装完毕

## pptp vpn服务器配置

### 配置pptp vpn ip地址

### 编辑/etc/pptpd.conf设置：

<pre class="lang:default decode:true">vim /etc/pptpd.conf</pre>
找到39行logwtmp处前面加上#号注释（详细见：[解决VPN服务器出现PTY read or GRE write failed问题](http://www.vkilo.com/slove-pptpd-vpn-pty-read-or-gre-write-failed.html "解决VPN服务器出现PTY read or GRE write failed问题")）;并且设置本地ip（localip）和客户端ip（remoteid）分配ip大约在102行
<pre class="lang:sh decode:true ">#logwtmp

localip 192.168.0.1
remoteip 192.168.0.234-238,192.168.0.245
</pre>
这样在pptp  vpn 服务器上面ip为192.168.0.1进行转发，客户端可以分配ip号段为remoteip，根据自己的数量需要设置ip号段。

### 添加pptp vpn账户和密码

### 编辑/etc/ppp/chap-secrets，添加格式为：

用户名       pptpd的名称（默认为pptpd）密码       ip地址

这里需要注意：位置一定不能弄错，最后一个ip地址随机分配请填写*,但是一定要加上，否则在验证的时候会出错具体示例如下：
<pre class="lang:default decode:true"># client        server  secret                  IP addresses
vpnuser0        pptpd   vpnpass1                  *
</pre>

### 配置pptp vpn dns服务器

通常情况下使用google的DNS服务器，编辑/etc/ppp/options.pptpd文件
<pre class="lang:sh decode:true">vim /etc/ppp/options.pptpd
#把ms-dns处修改为：

ms-dns 8.8.8.8
ms-dns 4.2.2.2

#推荐把调试模式开启，取消以下文字前面的#号取消注释
debug</pre>

### 开启网络转发功能

<pre class="lang:default decode:true">#打开 /etc/sysctl.conf
vim /etc/sysctl.conf
#添加（如果有则去掉前面的#号取消注释）
net.ipv4.ip_forward = 1
#执行如下命令使刚刚操作在系统生效
sysctl -p</pre>
&nbsp;

## pptp vpn防火墙配置

通过以上步骤基本上可以连接到重启后的vpn服务器，但是要让外部用户能连接<span lang="EN-US">PPTP VPN</span>，还需要在防火墙中将<span lang="EN-US">Linux</span>服务器的<span lang="EN-US">1723</span>端口和<span lang="EN-US">47</span>端口打开，并打开<span lang="EN-US">GRE</span>协议：
<pre class="lang:default decode:true">#注意下面的eth1为网卡，通常有一张内网卡和外网卡，请通过ifconfig命令查看
#请选择显示为外网ip的网卡
iptables -A INPUT -i eth1 -p tcp --dport 1723 -j ACCEPT
iptables -A INPUT -i eth1 -p gre -j ACCEPT
iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
#保存防火墙设置并重启防火墙
service iptables save
service iptables restart</pre>
如果出现"Failed to restart iptables.service: Unit iptables.service failed to load: No such file or directory." 请查看[解决 RHEL 7/ CentOS 7/Fedora 找不到iptables service](http://www.vkilo.com/rhel-7-centos-7-fedora-firewalld-to-iptables-service.html "解决 RHEL 7/ CentOS 7/Fedora 找不到iptables service")

## 调试pptp vpn服务器

<pre class="lang:sh decode:true">#开启pptpd
service pptpd restart
#设置开机启动pptpd
chkconfig pptpd on
</pre>
到以上步骤，基本上配置已经完成。接下来连接客户端并执行如下命令查看pptp vpn服务器日志
<pre class="lang:sh decode:true ">tail -f /var/log/messages</pre>
假如正常，便可收工，如果有问题，请根据日志提示自动爬文

&nbsp;