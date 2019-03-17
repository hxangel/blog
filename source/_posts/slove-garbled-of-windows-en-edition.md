---
title: 解决英文版windows出现软件乱码问题
tags:
  - win 7
  - windows xp
  - xp
  - 乱码
  - 系统
  - 英文
  - 英文版
  - 设置
  - 配置
id: 360
categories:
  - 笔记分享
date: 2011-11-07 10:50:00
---

我系统是win 7 sp1 x86，下载了个小软件却界面上全是问号（就是这个“？”，一个很讨嫌的家伙）。百思不得其解，因为设置上的话通常我配置都没有问题的，而且用了1年多了都没有问题，找了良久，未果。

我记得前面写过一篇关于xp乱码的问题 ：&#160; [<font color="#ff0000">从这里去，去了就不要回来了</font>](http://hi.baidu.com/yuanljuan/blog/item/af453237fc1f6a3e0b55a9c7.html)

那篇文章是<font color="#ff0000">[<font color="#ff0000">解决英文版windows XP中文软件乱码的方法</font>](http://hi.baidu.com/yuanljuan/blog/item/af453237fc1f6a3e0b55a9c7.html)</font><font color="#ff0000">&#160;</font><font color="#000000">，其实win 7设置与其类似。</font>

<font color="#000000">因为这次问号是个很小的问题，不值一提，所以就顺便说下基本设置步骤。</font>

* * *

1.打开“<font color="#ff0000">Control Panel</font>”，点击“<font color="#ff0000">Clock,Language,and Region</font>”。

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image.png)

2.点击“Region and language”；

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb1.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image1.png)

进去之后有4个选项卡，这里只需要设置两个地方。

3.选择“<font color="#ff0000">Location</font>”，把”<font color="#ff0000">Current location</font>” 设置成“<font color="#ff0000">China</font>”。

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb2.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image2.png)

4.<font color="#ff0000">关键步骤</font>，选择”<font color="#ff0000">Administrative</font>”选项卡。       [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb3.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image3.png)

点击“<font color="#ff0000">Change system locale</font>”，把“<font color="#ff0000">Current system locale</font>”设置成“<font color="#ff0000">Chinese（Simplified PRC）</font><font color="#000000">”。</font>

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb4.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image4.png)

到现在已经完成了。假如还有问题呢。最好是“拷贝设置”如下图（也就是把系统的，用户的之类的设置跟当前用户设置一致）。进去之后把√勾上。

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb5.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image5.png)

&#160;

如果你也跟我一样手贱。不小心把“<font color="#ff0000">Additional settings</font>”下的“<font color="#ff0000">sorting</font>”更改过，请点击”<font color="#ff0000">Reset</font>”按钮。

收工。