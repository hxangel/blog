---
title: 解决 RHEL 7/ CentOS 7/Fedora 出现Unit iptables.service failed to load
id: 718
categories:
  - Linux系统
date: 2015-03-29 12:43:37
tags:
---

一直用CentOS 6 习惯了，一下没适应过来。防火墙配置后执行service iptables save 出现"Failed to restart iptables.service: Unit iptables.service failed to load: No such file or directory."错误,在CentOS 7或RHEL 7或Fedora中防火墙由firewalld来管理，当然你可以还原传统的管理方式。或则使用新的命令进行管理。
假如采用传统请执行一下命令：
<pre class="lang:sh decode:true">systemctl stop firewalld
systemctl mask firewalld
</pre>
&nbsp;

并且安装iptables-services：
<pre class="lang:sh decode:true">yum install iptables-services</pre>
设置开机启动：
<pre class="lang:sh decode:true">systemctl enable iptables</pre>
<pre class="lang:sh decode:true">systemctl [stop|start|restart] iptables
#or
service iptables [stop|start|restart]
</pre>
&nbsp;
<pre class="lang:sh decode:true">service iptables save
#or
/usr/libexec/iptables/iptables.init save</pre>