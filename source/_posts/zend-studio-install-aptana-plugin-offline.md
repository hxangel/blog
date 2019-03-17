---
title: zend studio 整合aptana
id: 25
categories:
  - 笔记分享
date: 2012-04-07 11:50:28
tags:
---

zend studio 以及aptana 是干啥用的我这里就不多嘴了。

为啥要整合也轮不到我在这里胡说八道。so there we go。

## zend studio 9 与aptana 3的办法

* * *

1、打开zend studio,点击菜单栏上面的help-&gt;install new software
![Screen Shot 2012-04-07 at 5.36.59 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-5.36.59-PM1.png)

则跳出如下所示界面。

![Screen Shot 2012-04-07 at 7.08.03 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-7.08.03-PM.png)

2、安装aptana 3 在地址输入的地方直接输入：http://download.aptana.com/studio3/plugin/install 然后会出现界面如下：![Screen Shot 2012-04-07 at 7.12.49 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-7.12.49-PM.png)

这样我们直接下一步，下一步，同意协议，再下一步等待完成。当然这不是重点和我写这博文的目的。So you know ，继续往下。

## zend studio 9 与aptana 3离线整合的办法

* * *

首先打开：[http://download.aptana.com/studio3/plugin/install](http://download.aptana.com/studio3/plugin/install) 你会发现链接自动跳转到一个xml文件，并提示你错误的类型，木有关系。我们在跳转完成后的地址后面加上index.html like this: [http://d1iwq2e2xrohf.cloudfront.net/tools/studio/plugin/install/studio3/3.0.9.201202140953/index.html](http://d1iwq2e2xrohf.cloudfront.net/tools/studio/plugin/install/studio3/3.0.9.201202140953/index.html)

按照官方手动安装方法来安装aptana 3

1.下载点击页面中以下按钮进行下载
![Screen Shot 2012-04-07 at 7.27.13 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-7.27.13-PM.png)

2.等待下载完成后打开zend studio 在菜单点击help-&gt;Install New Software如图：
![Screen Shot 2012-04-07 at 5.36.59 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-5.36.59-PM.png)3.点击界面中的add 按钮————&gt;点击Archive…按钮 ，选中刚刚下载好的文件
![Screen Shot 2012-04-07 at 5.41.05 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-5.41.05-PM.png)

4.点击open打开文件 ，然后选中列表中的文件，点击下一步——&gt;下一步——&gt;接受协议——&gt;下一步——&gt;等待完成。

5.完成后重启zend studio ，选择菜单栏中的Zend Studio 中的 Preferences…(Note:Windows中不是这里，你懂得)
![Screen Shot 2012-04-07 at 7.43.19 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-7.43.19-PM.png)

6.在偏好设置里面你会发现Aptana 表示安装成功，这里我就不说配置的事儿了。![Screen Shot 2012-04-07 at 5.48.27 PM.png](http://www.vkilo.com/wp-content/uploads/2012/04/Screen-Shot-2012-04-07-at-5.48.27-PM.png)

### 引用官方的话：

### Manual Installation

<div class="download_box plugin_download" style="background-color: #cccccc; border-top-left-radius: 15px; border-top-right-radius: 15px; border-bottom-right-radius: 15px; border-bottom-left-radius: 15px; width: 200px; margin-left: 20px; border-top-color: #BBBBBB; border-right-color: #BBBBBB; border-bottom-color: #bbbbbb; border-left-color: #bbbbbb; border-image: initial; color: #535353; font-family: Arial, verdana, sans-serif; font-size: 13px; font-style: normal; font-variant: normal; font-weight: normal; letter-spacing: normal; line-height: 20px; orphans: 2; text-align: -webkit-auto; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-size-adjust: auto; -webkit-text-stroke-width: 0px; border-width: 1px; border-style: solid; padding: 10px;">
<div class="download_padded" style="text-align: center;">[Download Plugin Update Site](http://d1iwq2e2xrohf.cloudfront.net/tools/studio/plugin/install/studio3/3.0.9.201202140953/com.aptana.feature.studio-3.0.9.201202140953-7E777Q7HFGVBKBSEW7S_Iz0JktqM.zip)</div>
</div>

1.  Save the above file to an easy-to-find location.
2.  Open Eclipse distribution, and go to **Help** -&gt; **Install New Software...**.
3.  Click the **Add...** button to open the **Add Site** window.
4.  Click the **Archive...** button, and select the file saved in step 1.
5.  Select the appropriate plugins to install, and click **Next** -&gt; **Next**.
6.  Click the **Finish** button.
收工。洗澡去先。