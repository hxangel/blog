---
title: 使用SSH通过USB操控IOS设备
tags:
  - ios
  - iPhone
  - SSH
id: 419
categories:
  - 移动设备
date: 2013-02-24 17:35:00
---

玩VPS的人都知道，需要远程管理系统以及远程文件上传与下载。有时候操作iPhone的时候，是可以通过WiFi来操作的，但是那个时候我还没有安装WiFi设备，故淘汰，于是就想方设法通过USB来实现。

当然前提条件是已经越狱的设备。

为啥要使用SSH通过USB访问iPhone设备：

1.  操作比WiFi快很多。配置简单方便。2.  不是每个人都有WiFi，但是USB基本上都有。3.  iPhone下的终端操作很不方便，电脑操作就跟使用Linux终端一样。4.  文件传输方便。  

### 工具准备

* * *

1.  OpenSSH（通过Cydia）安装；2.  OpenSSL （通过Cydia）安装;3.  [itunnel_mux](https://code.google.com/p/iphonetunnel-usbmuxconnectbyport/downloads/list) 直接点击[itunnel_mux](https://code.google.com/p/iphonetunnel-usbmuxconnectbyport/downloads/list) 选择相应系统版本进行下载，然后解压，放在非中文目录下；4.  [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)&#160; 一个比较流行的SSH连接工具；5.  [WinSCP](http://winscp.net/download/winscp439setup.exe) Windows下比较好用的SFTP与FTP工具。  

### 连接IOS设备

* * *

将IOS设备通过USB连接到电脑上，连接完成以后打开“命令提示符（CMD）”工具,切换到itunnet_mux解压后对应的目录，例如我的是D:\itunnet_mux,先在cmd中输入 'D:'; 回车，再 'cd itunnet_mux' 就可以了。

输入（Windows）：'.\itunnel_mux --lport 9990 --iport 22'

lport 表示本地端口，iport 表示iPhone等IOS设备端口。

连接成功后有对应的提示。

操作IOS设备

* * *

1.  使用putty
    打开putty
    设置如图

    [![image](http://www.vkilo.com/wp-content/uploads/2013/02/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2013/02/image.png)

    点击open打开，要求输入用户和密码

    输入'root'回车

    在输入密码'alpine'（note:没有显示）回车

    然后就可以使用putty了。
2.  WinSCP 使用 asfaf
    如下图所示

    [![image](http://www.vkilo.com/wp-content/uploads/2013/02/image_thumb1.png "image")](http://www.vkilo.com/wp-content/uploads/2013/02/image1.png)

    主机为：127.0.0.1

    端口号为：9990

    用户名为：root

    密码：alpine

    登陆进去就可以进行各种文件传输了。  

### 使用putty修改默认密码

* * *

为了安全最好首次登陆后修改默认密码

登陆putty后

修改root密码

输入passwd

输入alpine作为旧密码

输入新密码回车确认

再次输入新密码

修改mobile密码

输入su mobile

输入alpine作为默认密码

输入新密码回车

再次输入新密码回车

完成

忘记root密码怎么办，请访问另一篇IOS设备忘记root密码怎么办