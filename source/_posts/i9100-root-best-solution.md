---
title: Samsung I9100 Galaxy S II 最简单root方法
tags:
  - Android
  - root
  - 工具
id: 542
categories:
  - 移动设备
date: 2013-06-23 13:51:05
---

因为本人没有android设备，更准确说，我没有智能手持设备，故对android设备我果断不熟，每次刷机以及刷机还有刷机都要花良久时间方可完事儿，这里分享一下如何root Samsung I9100 Galaxy S II 获取root权限
设备上面刷的是官方4.1.2的rom，折腾良久未果，其中原因不说的好，因为存储卡不能用，所以确定改用adb命令来root。开始

### 1.当然要安装驱动

建议去官方网站下载最新驱动
地址：[http://www.samsung.com/us/support/downloads/global](http://www.samsung.com/us/support/downloads/global)

选择对应型号下载即可。

安装驱动时注意查看设备管理器的com端口是否驱动成功，安装后会有Samsung的设备字样，而且不应该有叹号。

### 2. 准备root需要的工具

去[http://pan.baidu.com/share/link?shareid=2123502885&amp;uk=1107686635](http://pan.baidu.com/share/link?shareid=2123502885&amp;uk=1107686635)下载

adb usb通信命令行工具adbtool.zip 也可以到Google官方下载[https://dl-ssl.google.com/android/repository/tools_r22.0.1-windows.zip](https://dl-ssl.google.com/android/repository/tools_r22.0.1-windows.zip)最新的工具包。

当然这都是针对windows的，其他平台MAC/Linux请使用对应的工具。

以及拿root权限工具CWM-SuperSU-v0.97.zip(有0.99版本的，我这里为测试)

### 3.现在开始执行root操作

a.手机链接到电脑，确认已经链接好，使用手机管家之类的进行备份。

b.按住Volume 上＋Home键＋power键就是（加音量键＋主页键＋电源键）3秒以上放开，重启后进入recovery模式，选择Install Update with adb，接着手机进入等待传送状态。

c.解压adb工具包，将并将CWM-SuperSU-v0.97.zip放入到adb工具对应的目录中

打开终端工具（命令行工具），并cd到adb所在目录，当然这里你可以用绝对路径执行adb操作。

输入
<pre class="lang:sh decode:true">adb usb</pre>
然后输入
<pre class="lang:default decode:true">adb sideload CWM-SuperSU-v0.97.zip</pre>
这里确保CWM-SuperSU-v0.97.zip 与adb.exe在同一目录。假如不在同一目录请使用相应的路径。

输入命令后你可以看到手机屏幕上面有安装的信息，手机重启后任务完成。

&nbsp;