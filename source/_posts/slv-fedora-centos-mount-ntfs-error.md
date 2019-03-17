---
title: 解决fedora/CentOS下不能挂载NTFS分区
id: 621
categories:
  - 笔记分享
date: 2014-04-24 23:03:11
tags:
---

进了Windows 8 再一次进入Fedora后，出现unable to mount NTFS partition fedora的错误，其实是Windows 8 快速启动造成的。关闭即可。具体操作如下：

打开**Control Panel** 点击 **Power Options**;

点击**Choose what the power buttons do**;
点击** Change settings that are currently unavailable**;
在 **Shutdown** 设置, 去掉勾选 **Turn on fast startup**然后点击**Save changes** 按钮保存.