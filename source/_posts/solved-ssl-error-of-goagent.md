---
title: 解决goagent 翻墙 在mac os 下的证书错误问题
tags:
  - facebook
  - goagent
  - mac os twitter
  - vpn
  - youtube
  - 翻墙
id: 391
categories:
  - Linux系统
date: 2012-04-30 15:43:38
---

话说很久以前看到goagent 翻墙的教程，折腾一番，后面因为不知道啥原因，就一直都木有用了。然后就把所有的都忘记了。现在重抄旧业，翻出来折腾一番。在翻墙软件中，最好的翻墙软件是goagent了，主要针对国内的宽带问题，速度依然猫猫快，然而vpn也很难做到这一点。通过goagent上twitter，facebook，youtube 都灰常流畅。其他vpn啥的用起来是各种掉线，各种不爽，当然我用的是免费的,有一点就是个goagent是浏览器端的，而vpn是整个系统的。

博客也关闭老久了。路过的都没有几个，打酱油的就更少了。长满了草，所以发一篇笔记来晒晒，望路过的人更多些。偏题内容就还是割掉。

* * *

具体的安装过程就不多说了，有需要的请留言。首先去这里[goAgentX传送门](https://github.com/ohdarling/GoAgentX/downloads)，下载dmg package，你也可以下载源码自己编译，不过需要安装xcode，貌似不是很小，我这里当时下载了3天3夜（某个地方的宽带你是知道的）。解压，放到你稀饭的位置，
1.右键选择 Show Package Contents 进入目录,找到GoAgentX.app/Contents/Resources/goagent/CA.crt 文件；

2.双击打开找到的文件，会自动打开钥匙串访问，会出现各种提示，你就接受所有就ok。

3.然后选择刚刚导入的证书文件GoAgent CA，双击，展开trust，在第一下拉列表中选择 Always Trust。

4.基本上就酱紫就可以了。重启下浏览器，登陆，收工。

<div class="posttagsblock">[mac os x](http://technorati.com/tag/mac%20os%20x)</div>