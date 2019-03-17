---
title: 解决VPN服务器出现PTY read or GRE write failed问题
id: 707
categories:
  - Linux系统
date: 2015-03-29 12:27:48
tags:
---

[在REHL系搭建pptp vpn服务器](http://www.vkilo.com/install-pptp-vpn-rhel-linux.html "如何在RHEL/Centos/Fedora/下搭建vpn pptp 服务器") 连接的时候出现（619等错误）查看系统日志[cat /var/log/messages |grep pptpd]后发现每次连接失败都会出现以下日志内容:
<pre class="lang:default decode:true">GRE: read(fd=6,buffer=80504c0,len=8196) from PTY failed: status = -1 error = Input/output error, usually caused by unexpected termination of pppd, check option syntax and pppd logs
CTRL: PTY read or GRE write failed (pty,gre)=(6,7)
CTRL: Reaping child PPP[13354]
CTRL: Client XXX.XXX.XXX.XXX control connection finished</pre>
于是把打开调试模式，修改/etc/ppp/pptp-options 文件，找到
<div class="wp_codebox">
<pre class="lang:default decode:true">#取消如下行前#
debug
#执行
service pptpd restart</pre>
</div>
取消行前的注释，重启pptpd服务进入调试模式

分析日志后发现是logwtmp版本的与pptpd版本不一致的原因导致的问题，于是打开/etc/pptpd.conf文件,找到
<div class="wp_codebox">
<pre class="lang:default decode:true">logwtmp</pre>
注释掉logwtmp后，重新启动pptpd，再次连接后一切恢复正常。

</div>
默认启用了proxyarp（在/etc/ppp/pptp-options中）功能，每次非正常断开连接后，执行以下命令：
<div class="wp_codebox">
<pre class="lang:sh decode:true">#windows 
arp -d
#linux
sudo arp -d -a</pre>
&nbsp;

</div>