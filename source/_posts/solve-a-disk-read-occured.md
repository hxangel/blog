---
title: 解决a disk read error occured  press ctrl+alt+alt to restart
tags:
  - a disk read error occured
  - a disk read error occured press ctrl+alt+alt to restart的解决方法
  - 解决a disk read
id: 205
categories:
  - 笔记分享
date: 2010-12-23 22:20:16
---

a disk read error occured&#160; press ctrl+alt+alt to restart的解决方法

因为很多人是用的是串口的硬盘。换接口是不行的。前不久一个兄弟电脑坏了。老是开机出现这个错误。

弄了好几回都没有效果；感觉相当的纠结。不过几经折腾呢，我感觉也不是问题的问题。我再也不弄那个bios了，弄的太累了，越搞越糊涂。

我是这么弄的。把机子拆开，把cmos电池反装一会儿，重新给正确的装上去。然后开机会出现Floppy disk&#160; fail (40)；还有就是cmos没有设置什么的；我们点击delete键进入bios，然后把Floppy disk默认的1.44M设置为 none。启动磁盘里面该选什么选什么。这样应该就不存在什么问题了。 

还有一个需要检查的地方就是你的硬盘是不是存在活动分区，假如说不存在，请把你装的最早的系统所在的分区设为活动分区。