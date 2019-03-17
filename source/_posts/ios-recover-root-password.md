---
title: IOS 设备忘记root密码怎么找回
id: 425
categories:
  - 移动设备
date: 2013-02-24 18:02:06
tags:
---

上次我拿iPhone准备登陆终端进行操作的时候发现我的root密码被修改过，但是很久没有登陆过了。于是自己改成什么密码都忘记了。最开始准备重新刷机，感觉太麻烦，刷机之后还要重新越狱，有很多软件又要重新安装和配置。

于是找了一下有没有什么办法找回。结果很幸运。接下来讲下具体过程。

需要安装iFile，不过iFile是越狱必装软件之一。

1.  打开Cydia
2.  搜索iFile
3.  然后打开iFile找到etc/scroll目录
4.  找到'master.passwd'文件
5.  使用Text Viewer,按编辑按钮打开编辑器
6.  找到类似于root:UlGASB5XWDrOc:0:0::0:0:
7.  我们需要编辑的UlGASB5XWDrOc这一段
8.  使用'crypt'函数进行算新密码,这里推荐一个网页 [Crypt Tool](http://www.functions-online.com/crypt.html)，在$str输入你新密码，然后$salt输入任意两个字符点击run按钮得到result值
9.  用8中获取的result值替换root:到第一个:0的值也就是这里的UlGASB5XWDrOc
10.  点击顶部的保存保存文件。
11.  完成，你可以使用新设置的密码了