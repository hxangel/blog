---
title: 如何用电脑安装微信
tags:
  - Android
  - qq
  - 安装
  - 微信
  - 电脑
  - 腾讯
id: 327
categories:
  - 笔记分享
date: 2011-08-11 16:04:00
---

电子数码类产品更新的速度比钱包的更新速度要快。故很多人现在使用的还是非智能手机（我就是其中一个），然而爱玩手机的玩家都知道智能手机能给人带来好多新鲜的好玩的东西，更人以最好的体验。如腾讯(qq)最新推出的微信，不但可以发文本，表情，图片，还可以发语音和视频。   

但是如我这样还在使用非智能机的朋友就只有叫苦了。同时很多小盆友会问：

### 电脑上能装微信么？

### 如何在电脑上安装微信客户端？

### 如何使用电脑玩微信？

回答是肯定的，至于你信不信，由你，反正我是信了！

这个问题搞Android开发的程序员都知道。

### 那什么是Android呢？

Android是基于Linux开放性内核的操作系统，是Google公司在2007年11月5日公布的手机操作系统。

Android早期由原名为&quot;Android&quot;的公司开发，谷歌在2005年收购&quot;Android.Inc&quot;后，继续对Android系统开发运营，它采用了软件堆层（software stack，又名软件叠层）的架构，主要分为三部分。底层Linux内核只提供基本功能，其他的应用软件则由各公司自行开发，部分程序以Java编写。

解决思路：电脑模拟智能手机，省流量，也方便！通过电脑安装一个Android系统（因为Android开源）。前面均废话，误入正题先！

## <font color="#009797">Setup 1：搭建java环境&#160; jdk（not jre）的安装</font>

* * *

原来我写过一篇博文：[JDK环境变量的设置](http://hi.baidu.com/yuanljuan/blog/item/9681520b02a6d71194ca6bca.html) 这里写的比较详细，我这里重新说下步骤。

1、到oracle去下载j2ee or javase:&#160; [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html "http://www.oracle.com/technetwork/java/javase/downloads/index.html")

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb6.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image6.png)

进入传送门之后得到上面的界面，这里有两个可选安装的，这里我推荐选择第一个。也就是：[<font color="#ff0033">Java SE Development Kit(JDK 7)</font>](http://www.oracle.com/technetwork/java/javase/downloads/jdk-7u1-download-513651.html)

[![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb7.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image7.png)

看到图中的红圈圈没有最上面需要接受协议，下面是你需要的版本。我这里讲的是windows下的。肯定是下windows版本的，所以当不确定系统是64位的还是32位的，那么请下载X86版本后面对应的链接。

2、按照提示安装。安装过程跟其他的软件一样，根据自己的喜好来安装到对应的目录，也可以保持默认。<font color="#ff0033">PS:前面不要安装到中文目录下（常识）！</font>

3、设置环境变量

右击<font color="#ff0000">我的电脑</font>-----&gt;<font color="#ff0000">属性</font><font color="#000000">------&gt;</font>高级<font color="#000000">------&gt;</font>环境变量 <font color="#000000">，可以看到环境变量设置界面如下：</font>

[![QQ截图20110811150808](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811150808_thumb.png "QQ截图20110811150808")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811150808.png)

上面那个框框是<font color="#ff0033">当前用户环境变量</font>设置，下面的框是<font color="#ff0033">系统环境变量</font>设置，这里最好是加到<font color="#ff0033">系统变量</font>里面，当你切换系统用户的时候还是使用（个人推荐）！

在系统环境变量的下方<font color="#009797">点击【</font><font color="#ff0033">新建</font>】按钮<font color="#000000">，</font><font color="#000000">新建一个</font>新的环境变量<font color="#009797">【</font><font color="#ff0033">JAVA_HOME</font> 】如下图:

[![QQ截图20110811150905](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811150905_thumb.png "QQ截图20110811150905")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811150905.png)

因为我这里JDK安装在<font color="#ff0033">D槽下的java目录（即D:\java）</font>下，所以设置如上图。设置好后点击OK。

继续添加其他的环境变量，设置的步骤基本上一样，3个环境变量配置如下：

&#160;
  <table border="1" cellspacing="0" cellpadding="2" width="650"><tbody>     <tr>       <td valign="top" width="90">变量名</td>        <td valign="top" width="311">变量值</td>        <td valign="top" width="325">说明</td>     </tr>      <tr>       <td valign="top" width="90">JAVA_HOME </td>        <td valign="top" width="311">安装java目录\jdk目录（如我的：D:\java\jdk7）</td>        <td valign="top" width="325">即你安装jdk所在的位置，需自己修改</td>     </tr>      <tr>       <td valign="top" width="90">CLASSPATH</td>        <td valign="top" width="311">         > %JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;%JAVA_HOME%\lib       </td>        <td valign="top" width="325">直接新建即可</td>     </tr>      <tr>       <td valign="top" width="90">PATH&#160;&#160;&#160; </td>        <td valign="top" width="311">.; %JAVA_HOME%\bin;</td>        <td valign="top" width="325">修改原有的，把这段代码加前面</td>     </tr>   </tbody></table>  

<font color="#ff0033">以上用分号隔开，就是左右对应关系</font>。设置完成后在命令行输入java（开始——&gt;运行——&gt;输入cmd，确定——&gt;输入java ，Enter），看下是否正确！到此jdk 安装完成！

## <font color="#009797">Setup 2 ：安装Android SDK</font>

* * *

1.  下载
    Android SDK下载地址：[http://developer.android.com/sdk/index.html](http://developer.android.com/sdk/index.html "http://developer.android.com/sdk/index.html")&#160;<font color="#ff0000">这个地址永久是最新的！</font>

    这里最好是下载<font color="#ff0000">zip包</font>（windows用户），目前最新的是[android-sdk_r15-windows.zip](http://dl.google.com/android/android-sdk_r15-windows.zip)

    [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb8.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image8.png)
2.  解压
    解压（<font color="#ff0000">请不要放到中文目录下！有些软件安装带空格的目录，都不支持不过是少数</font>）
3.  安装虚拟文件包
    在【<font color="#ff0000">android-sdk-windows</font>】目录下双击打开<font color="#ff0000">【AVD Manager.exe】</font><font color="#000000">，在【</font><font color="#ff0000">菜单栏</font>】选择【<font color="#ff0000">tools</font>】——&gt;【<font color="#ff0000">SDK Manager</font>】（直接打开【<font color="#ff0000">SDK Manager.exe</font>】<font color="#000000">具有相同的效果</font>）。

    [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb9.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image9.png)

    打开之后会得到上图界面，<font color="#000000">程序自动连接到google的服务器检查可用的包，这里需要几十秒到几分钟，请耐心等待。更新完成后，选择需要的安装包进行安装。（这里推荐使用</font><font color="#ff0000">2.3.3</font>，因为高版本的对配置要求高，可能会出现半天启动不了，进去之后很慢等现象，版本低的功能肯定没有高版本的强大。）

    [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb10.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image10.png)

    下面<font color="#ff0000">红圈内</font>的为<font color="#ff0000">可选</font>安装，意思就是可以不用下载，选择后点击【<font color="#ff0000">install </font><font color="#9b00d3">N</font> packages】（<font color="#9b00d3">N</font>=下载包数量）。

    [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb11.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image11.png)

    选择【<font color="#ff0000">Accept All</font>】接受所有，点击【<font color="#ff0000">Install</font>】安装，<font color="#ff0000">安装时间稍长，请耐心等待</font>!下载安装完成后直接关闭当前窗口。
4.  <font color="#000000">新建虚拟系统</font>
    [![image](http://www.vkilo.com/wp-content/uploads/2011/11/image_thumb12.png "image")](http://www.vkilo.com/wp-content/uploads/2011/11/image12.png)

    在窗口右边单击【<font color="#ff0000">New</font>】按钮（<font color="#ff0000">如果没有找到按钮请把窗口调节更大一些</font>）<font color="#000000">创建一个新的虚拟设备。输入名称（不要用中文名字），选择版本，SD Card的Size那里设置SD卡的大小（建议1G以上）。</font>  

[![QQ截图20110811154510](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811154510_thumb.png "QQ截图20110811154510")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811154510.png)

创建过程中可能出现<font color="#ff0000">程序未响应</font>之类的属于正常现象，请耐心等待至创建完毕。完成后会自动关闭对话框，弹出新的对话框<font color="#ff0000">恭喜你</font>一下已经创建成功。关闭返回，在【<font color="#ff0000">Virtual device </font>】<font color="#000000">中会出现刚刚新建的虚拟设备，选中已创建的虚拟设备，点击【</font><font color="#ff0000">Start</font>】<font color="#000000">按钮运行,</font>点击【<font color="#ff0000">Launch</font>】继续，假如前面的各个环节都没有出错的话，那么鸡动人心的一刻就会到来，等待系统装载完成。

## <font color="#009797">Setup 3 安装微信</font>

* * *

进入android系统后，点击上面那个【<font color="#ff0000">Search</font>】框打开Android中手机浏览器， 在地址栏中输入[http://weixin.qq.com](http://weixin.qq.com) 点击【<font color="#ff0000">免费下载</font><font color="#000000">】按钮！</font>

[![QQ截图20110811160212](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811160212_thumb.png "QQ截图20110811160212")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811160212.png)

左上角会神奇的出现一个<font color="#ff0000">下载图标</font>，鼠标按住图标往下一拖拽就会看到下载的内容，也可以到应用程序的【<font color="#ff0000">Download</font>】下去找。找到下载的<font color="#ff0000">apk</font>文件后单击，按引导操作完成安装！然后打开微信，后面的步骤就不再赘述。因为有了这个玩意儿相信你懂得。

[![QQ截图20110811160841](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811160841_thumb.png "QQ截图20110811160841")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811160841.png)

<font color="#ff8000">PS</font>：1、注意jdk环境配置不要整错了。因为需要jdk的环境支持。

&#160;&#160;&#160;&#160;&#160;&#160;&#160; 2、下载模拟器的时候如果出问题请把设置里面的这个勾给打上。

[![QQ截图20110811161313](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811161313_thumb.png "QQ截图20110811161313")](http://www.vkilo.com/wp-content/uploads/2011/08/QQ20110811161313.png)

&#160;&#160; 要是Android里面你看不惯E文, 请到

[![image](http://www.vkilo.com/wp-content/uploads/2011/08/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2011/08/image.png)

修改成中文滴。亲（没做过淘宝客服）

再见！（《老爸快跑》里面的）

Thanks for reading!