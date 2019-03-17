---
title: 如何 激活 windows 8 M2/M3 build 7955
tags:
  - window 8 M2
  - window 8 下载
  - windows 8
  - windows 8 M2 build 7955
  - windows 8 产品密钥
  - windows 8 的激活方法
  - windows 8激活
  - 如何激活windows 8
id: 286
categories:
  - 笔记分享
date: 2011-04-29 12:38:00
---

windows 8 激活的目前因为是泄露版本。激活步骤很简单，只是用来测试获得更好的体验。而且从[windows 8 已知builds(编译版本)列表及版本详解](http://www.vkilo.com/270-link.html)知道fre这个关键字。可以用windows 7 beta版的产品密钥激活。

## windows 8 产品密钥(目前可用)

* * *

**Windows 7 Beta 32位 产品密钥**

6JKV2-QPB8H-RQ893-FW7TM-PBJ73    
TQ32R-WFBDM-GFHD2-QGVMH-3P9GC     
GG4MQ-MGK72-HVXFW-KHCRF-KW6KY     
4HJRK-X6Q28-HWRFY-WDYHJ-K8HDH     
QXV7B-K78W2-QGPR6-9FWH9-KGMM7

**Windows 7 Beta 64位 产品密钥**

7XRCQ-RPY28-YY9P8-R6HD8-84GH3    
RFFTV-J6K7W-MHBQJ-XYMMJ-Q8DCH     
482XP-6J9WR-4JXT3-VBPP6-FQF4M     
JYDV8-H8VXG-74RPT-6BJPB-X42V4     
D9RHV-JG8XC-C77H2-3YF6D-RYRJ9

## windows 8 的激活方法（[windows 8 M2（pre-M3) build 7955](http://www.vkilo.com/266-link.html)）[图文]

* * *

这里针对window 8 M2 build 7955 下载地址详见：[window 8 下载](http://www.vkilo.com/266-link.html)

方法1：打开**Control Panel（控制面板）** -&gt; **Action Center** -&gt; **Genuine Center**. 点击 **Enter a new product key** 按钮[![image](http://www.vkilo.com/wp-content/uploads/2011/04/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2011/04/image.png)

然后输入上面32位 产品密钥中的其中一枚。会自动验证你的产品密钥，一般都会成功如下图：

[![image](http://www.vkilo.com/wp-content/uploads/2011/04/image_thumb1.png "image")](http://www.vkilo.com/wp-content/uploads/2011/04/image1.png)

点击关闭后这里已经变成已激活的标志了。

[![image](http://www.vkilo.com/wp-content/uploads/2011/04/image_thumb2.png "image")](http://www.vkilo.com/wp-content/uploads/2011/04/image2.png)

然后右键computer (计算机)–&gt;properties（属性）查看可以看到如下效果图。

[![XRC2FON1QY@SKFLILI9NXCA](http://www.vkilo.com/wp-content/uploads/2011/04/XRC2FON1QYSKFLILI9NXCA_thumb.jpg "XRC2FON1QY@SKFLILI9NXCA")](http://www.vkilo.com/wp-content/uploads/2011/04/XRC2FON1QYSKFLILI9NXCA.jpg)

方法2：按 Ctrl + Shift + F9切换到非aero主体模式。按下windows 键输入cmd 看到上面有个cmd命令行工具。右键单击选择run as administrator

然后输入：
  > `slmgr.vbs -ipk 产品密钥 `  

`回车等待片刻执行完成后输入：`
  > slmgr.vbs -ato  

`回车等待结束。`

`**<font color="#ff0080" size="3">PS</font>**:[开启windows 8 隐藏功](http://www.vkilo.com/269-link.html)能对激活与否没有多大的关系。你激活不会自动[开启windows 8的隐藏功能](http://www.vkilo.com/269-link.html)。不激活也有30天的试用期。`