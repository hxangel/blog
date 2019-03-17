---
title: 关于android sdk 安装的一些问题补充
tags:
  - Android
  - j2ee
  - j2se
  - java
  - Java SE Development Kit 7
  - 下载
  - 安装微信
  - 微信
id: 347
categories:
  - 笔记分享
date: 2011-10-18 15:55:00
---

（本文决定只用句号。盆友们请自行划分）因为博客正在备案中。小blog暂时放在米国。速度那是相当的慢啊。话了50多刀整了一个破空间。好的就是有个独立的ip。以上废话就是说明鄙人为什么更新博客。在众多哥们的支持下。

### 原文：[如何用电脑安装微信](http://www.vkilo.com/327-link.html)

百度空间：[如何用电脑安装微信](http://hi.baidu.com/yuanljuan/blog/item/0717c9f5d77631f57709d7ca.html)&#160;

### 也就是这篇日志。发现了不少的问题。说明我自己做的不够好。让你们折腾的死去活来的。这里我讲文中的一些bug给大家讲一下。    

* * *

## 1、j2ee 和 j2se 该如何下载？

* * *

这个问题有很多盆友问我，其实我知道当时我疏忽了又很多盆友是第一次接触这个软件。只是听说。而且我在java环境变量里面也有提到（废话。立马打住）。

我这里上两个图相信大伙都能明白！

### [![image](http://www.vkilo.com/wp-content/uploads/2011/10/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2011/10/image.png)

其实中间那两个我都没有下载过。而且netbeans我这里没有安装。<font color="#006342">第一个和第四个根据自己喜欢。第四个小一点。</font>

### Java Platform, Enterprise Edition 6 SDK Update 3 (with JDK 7)

### 也就是java进去所指的j2ee列表。

[![image](http://www.vkilo.com/wp-content/uploads/2011/10/image_thumb1.png "image")](http://www.vkilo.com/wp-content/uploads/2011/10/image1.png)

下面红圈内的都是windows的版本。根据自己的需要（x86与X64）。32位系统的请选中32位版本。默认不加X的就死32位的。带ml的和不带ml的两个版本随便选择一个即可。

### Java SE Development Kit 7 

### 也就是java se所指向的列表。

[![image](http://www.vkilo.com/wp-content/uploads/2011/10/image_thumb2.png "image")](http://www.vkilo.com/wp-content/uploads/2011/10/image2.png)

这里我想下载错误的可能基本上为蛋。不过不管下哪一个版本都不要忘记 <font color="#ff0000">接受他们的协议 </font>。

* * *

## 2、为什么装微信后输入的声音会卡？

* * *

真个真是对不起大家。我<font color="#ff0000">老实不知道</font>。所以这个问题不要再问我。见谅![哭泣的脸](http://www.vkilo.com/wp-content/uploads/2011/10/wlEmoticon-cryingface.png)。要是感兴趣的盆友可以做装几个可以输入声音或者是录音的软件测试下是微信的原因还是android sdk的原因（我木有时间折腾![尴尬](http://www.vkilo.com/wp-content/uploads/2011/10/wlEmoticon-embarrassedsmile.png)）。So sorry! 

* * *

## 3、笼统的说下安装的时候注意的一些细节

* * *
1&gt;安装软件的时候养成良好的习惯。不要除非个别默认是中文目录外。不建议把软件放到中文目录下运行。而且对英文支持肯定要比中文好。   

2&gt;开虚拟机的时候<font color="#ff0000">卡</font>在<font color="#ff0000">启动界面</font>了肿么办？这里很有可能是版本的问题。个人推荐2.3.3版的。其实有些盆友的配置可能不是很好。我的配置基本上能运行所有的版本。建议试试<font color="#ff0000">低版本</font>的试试。

3&gt;包下载好了，没有新建new按钮肿么办?

[![image](http://www.vkilo.com/wp-content/uploads/2011/10/image_thumb3.png "image")](http://www.vkilo.com/wp-content/uploads/2011/10/image3.png)

首先调整窗口大小。然后就把鼠标放中间等到可以拖动状态的时候向左边拖。见证奇迹的时刻就回到来。然后就没有然后了。

4&gt;java环境变量不会设置。看我图中的指向。根据自己的软件目录。设置完后“win+R”。输入cmd（type “cmd”）。 enter（回车）。输入“java”回车。检查设置是不是正确。

假如你协助又安装，有可能有注册表冗余，打开注册表。去瞅瞅HKEY_LOCAL_MACHINE\SOFTWARE\JavaSoft\Java Runtime Environment目录是不是正确的。不对头就修改。

5&gt;为什么不做视频教程。主要是我外设不够。声音不好。讲的也稀里糊涂的，博客放的国外速度慢。视频数据量比较大。有需要的话我会录制放到115盘让大伙去下载。

6&gt;俺秋秋号码是[kimozh@qq.com](mailto:kimozh@qq.com)，可以加我秋秋！

<font size="6">没有后话。再见。</font>