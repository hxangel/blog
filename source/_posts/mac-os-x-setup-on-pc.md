---
title: MAC OS X 硬盘安装详细分解教程
id: 166
categories:
  - Linux系统
date: 2010-12-13 16:30:12
tags:
---

## 第一部分:工具整理

引导工具：<span style="color: #ff0000;">BootThink</span> 、<span style="color: #ff0000;">Nawcom</span>的<span style="color: #ff0000;">Boot CD</span>、<span style="color: #ff0000;">Chameleon</span>（变色龙）、<span style="color: #ff0000;">EmpireEFI </span>等；

Ps:你只需要一个就够了，个人推荐用BootThink 。

<span style="color: #ff0000;">HFS Explorer</span>（需要java环境，装java VM即可）

<span style="color: #ff0000;">MacDrive</span>或<span style="color: #ff0000;">TransMac</span>（用于在windows环境下读写Mac OS分区）

磁盘工具：<span style="color: #ff0000;">DiskGenius</span>或者<span style="color: #ff0000;">[Acronis Disk Director Suite](http://www.vkilo.com/75-link.html)</span>（win7可以不用下载）

启动盘一张（能运行分区工具）

<span style="color: #ff0000;">硬盘安装助手</span>

替换文件:OSInstall+OSInstall.mpkg(个人推荐)

相见我的另一篇：[MAC OS X 不能安装在这台机器上的解决办法](http://www.vkilo.com/157-link.html "MAC OS X 不能安装在这台机器上的解决办法")

kext（驱动文件）:

<span style="color: #ff0000;">FakeSMC.kext</span> : bootthink原来已经带有，这个kext模拟真正苹果机上的SMC部件，必备
<span style="color: #ff0000;">NullCPUPowerManagement.kext</span> :将电源管理功能禁用，解决IntelCPUPowerManagement.kext的HPET错误
<span style="color: #ff0000;">OpenHaltRestart.kext</span>:解决重启/关机无法断电问题
<span style="color: #ff0000;">PlatformUUID.kext</span>:解决Unable to determine UUID for host. Error : 35的问题
<span style="color: #ff0000;">VoodooPS2Controller.kext</span>
<span style="color: #ff0000;">AppleACPIPS2Nub.kext</span> 组合或
<span style="color: #ff0000;">ApplePS2Controller.kext
</span><span style="color: #ff0000;">AppleACPIPS2Nub.kext</span> 组合

Ps:2个要一起使用，提供传统PS/2插口鼠标/键盘或笔记本触摸板支持

* * *

## 第二部分：安装前准备

1、建立disk img

首先把我们安装<span style="color: #ff0000;">HFS Explorer</span>，注意需要[安装java环境](http://hi.baidu.com/yuanljuan/blog/item/9681520b02a6d71194ca6bca.html)；这里安装就不多说。

打开<span style="color: #ff0000;">HFS Explore</span>, 载入你的MAC OS X iso镜像文件选择<span style="color: #ff0000;">file</span> ——<span style="color: #ff0000;">load file system from file</span> 打开你的

然后点击<span style="color: #ff0000;">tool</span>——<span style="color: #ff0000;">creat disk image</span>, 然后保存到你的某个NTFS盘下面（文件时相当的大）。

Ps：这一步你也可以替换掉[OSInstall+OSInstall.mpkg](http://www.vkilo.com/157-link.html "MAC OS X 不能安装在这台机器上的解决办法")，这样你后面可以稍微的免掉第4部分到需要的时候才装。

2、准备分区

为我们的<span style="color: #ff0000;">MAC OS X</span>分区。我这里是7G（安装盘）+20G（安装位置）；

操作见<span style="color: #ff0000;">[Acronis Disk Director Suite](http://www.vkilo.com/75-link.html) </span>

分区的时候不要选择任何格式也不要格式化，如有提醒直接取消。

当然20G的你可以不管先。

这里我不多言。

3、刻录disk img

打开下载好的硬盘安装助手（管理员身份）。

[![image](http://www.vkilo.com/wp-content/uploads/2010/12/image_thumb.png "image")](http://www.vkilo.com/wp-content/uploads/2010/12/image.png)

打开第一步里面的<span style="color: #ff0000;">DMG</span>镜像文件

选择第二步分好的7G的分区。

选择下面三个复选框都不要选（因为过时了）。

单击开始写入文件。可能会出现未响应之类的，请不要搭理，干别的事去。

注意完成后会出现<span style="color: #ff0000;">Change Partition type to AF: success</span>

要没有完成可以手动设置为AF。

手动设置为AF方法：

win+R：<span style="color: #ff0000;">cmd</span>，回车，打开windows命令窗口
在命令窗口中键入：<span style="color: #ff0000;">diskpart</span>，回车，启动该程序，可能在vista或7中还会询问权限之类的，只管点是就好，打开diskpart窗口
当光标前面变成<span style="color: #ff0000;">DISKPART&gt;</span>后，键入<span style="color: #ff0000;">select disk 0</span> 回车（此步即选择你安装雪豹的那个硬盘，如果是单硬盘的话，一般都是<span style="color: #ff0000;">disk 0</span>，注意disk和0之间有空格）
窗口提示：磁盘0是所选磁盘，再键入<span style="color: #ff0000;">list partition</span> 回车，屏幕显示硬盘上的各个分区
找到你想更改ID的<span style="color: #ff0000;">7G</span>的分区，记住分区号，这里假设是<span style="color: #ff0000;">x</span>分区
键入：<span style="color: #ff0000;">select partition x</span>，回车，屏幕提示：分区x是所选分区
键入：<span style="color: #ff0000;">set ID=AF</span> 回车，屏幕提示：<span style="color: #ff0000;">diskpart已成功更改分区ID</span>

4、替换文件

安装<span style="color: #ff0000;">Macdrive</span>（个人推荐同时需要重启）或<span style="color: #ff0000;">TrankMac</span>

#### [macdrive安装及使用详细教程](http://www.vkilo.com/169-link.html)

替换[OSInstall+OSInstall.mpkg](http://www.vkilo.com/157-link.html "MAC OS X 不能安装在这台机器上的解决办法")（个人推荐）

PS：假如你是非<span style="color: #ff0000;">intel多核CPU</span>（如<span style="color: #ff0000;">AMD</span>）需要下载对对应的<span style="color: #ff0000;">mach_kernel</span>

我的是intel的所以飘过。

5、安装引导工具

打开<span style="color: #ff0000;">bootThink</span>，直接安装。

安装后你会发现你的<span style="color: #ff0000;">C盘</span>有个<span style="color: #ff0000;">Darwin</span>目录。

打开<span style="color: #ff0000;">Darwin</span>，以<span style="color: #ff0000;">管理员的身份</span>运行<span style="color: #ff0000;">Install.bat</span>完成安装。

复制我们下载好的<span style="color: #ff0000;">kext</span>文件到
<div>
<pre>C:\Darwin\System\LibrarySL\Extensions</pre>
</div>
因为怕有冲突所以建议删除
<div>
<pre>C:\Darwin\System\LibrarySL\Extensions\Extensions.mkext
C:\Darwin\System\LibrarySL\x32\Extensions\Extensions.mkext
C:\Darwin\System\LibrarySL\x64\Extensions\Extensions.mkext</pre>
</div>
如果你用的是变色龙

把<span style="color: #ff0000;">kext</span>文件复制到安装光盘（<span style="color: #ff0000;">7G</span>）的<span style="color: #ff0000;">\Extra\Extensions</span>下；

其他的自己网上找教程；

<span style="color: #ff0000;">Ps</span>：<span style="color: #ff0000;">C盘要为NTFS格式</span>，如果是FAT32需转换（基本不会数据丢失）

方法：[FAT32与NTFS互转换](http://hi.baidu.com/yuanljuan/blog/item/147b06fcbbd7614bd7887dfe.html "FAT32与NTFS互转换")

* * *

## 第三部分：正式安装

需要在<span style="color: #ff0000;">bios</span>里面开启<span style="color: #ff0000;"> SATA AHCI</span>

当然假如机器不支持有补丁。

准备工作做完后我们重启电脑，用<span style="color: #ff0000;">bootThink</span>启动。

选择选择刚刚做好镜像的那个盘（<span style="color: #ff0000;">Mac OS X Install DVD</span>）。

正常状况下是能够顺利进入语言选择界面的。那么have fun!

恭喜85%成功！

假如人品不好（自己拿人品计算器算一下，不一定准，我是99分都死翘翘^_^）,

出现了五国或者是其他的自动重启（反正五花八门）

[![image](http://www.vkilo.com/wp-content/uploads/2010/12/image_thumb1.png "image")](http://www.vkilo.com/wp-content/uploads/2010/12/image1.png)

图X-1:五国

[![image](http://www.vkilo.com/wp-content/uploads/2010/12/image_thumb2.png "image")](http://www.vkilo.com/wp-content/uploads/2010/12/image2.png)

图X-2:禁止

我们开机进入<span style="color: #ff0000;">bootThink</span> 按<span style="color: #ff0000;">F8</span> 然后选择安装盘（7G）

利用<span style="color: #ff0000;">-cpus=1</span>（cpu为一个） <span style="color: #ff0000;">-x32</span>(32位模式) <span style="color: #ff0000;">–f</span>（修复错误，不是一定能够帮你解决问题） <span style="color: #ff0000;">–x</span>（相当于安全模式）<span style="color: #ff0000;"> –v</span> （哆嗦模式 ，这个很关键你可以看到你出错的地方）

以上可以一起使用。

找出你的问题，然后就百度google墙内强外翻个遍。

好了。这里接着你顺利解决了各个方面的问题。顺利进入安装界面。我们先不要管安装器，选择实用工具——磁盘工具

选择分好的<span style="color: #ff0000;">20G</span>的分区，选择在右边选“<span style="color: #ff0000;">抹掉</span>”;在格式选择<span style="color: #ff0000;">”Mac OS扩展(日志式)” </span>然后在下面写上你喜欢的<span style="color: #ff0000;">名字</span>(英文，个人建议)，点击右下角的“<span style="color: #ff0000;">抹掉</span>”。

数据无价，你的失误操作本人概不负责&lt;^_^&gt;。抹干净后直接点左上角叉叉。关闭磁盘工具。

假如出现<span style="color: #ff0000;">MAC OS X不能安装在这台机器</span>或者电脑上，见详情：

#### [MAC OS X 不能安装在这台机器上的解决办法](http://www.vkilo.com/157-link.html "MAC OS X 不能安装在这台机器上的解决办法")

好了，接下来就是安装了。

安装器里面选择相应的安装（可以默认下一步）；

选择刚刚抹掉的那个盘；选择下一步开始安装。

大约30分钟后重启。

天啦。前面已经折腾够了，怎么还要折腾呢。整个<span style="color: #ff0000;">电脑啥玩意儿</span>都进不去了（bios还是可以滴）。

OK，我们用刚刚提到启动盘，在<span style="color: #ff0000;">bios</span>里面设置好后重启，把C盘（通常，反正原来是哪一个就是哪一个）设为活动！

重启后<span style="color: #ff0000;">开机菜单</span>还原了。用bootThink引导进入你的MAC OS X系统,五国还有别的情况自己找解决办法。

进系统后你会发现有很多表单，这个我这里不用啰嗦。自己填写好后应该能顺利进入系统。

安装完成！我是要收工了。你自己要折腾的东西就来了（<span style="color: #ff0000;">安装驱动</span>之类的教程很多，自己去折腾）。

用到的部分玩意儿打包：

[![image](http://www.vkilo.com/wp-content/uploads/2010/12/image_thumb3.png "image")](http://www.vkilo.com/wp-content/uploads/2010/12/image3.png)

下载地址：[点击这里](http://u.115.com/file/f5711a885e "mac_tool")

* * *

后记：其实我还有话说

@vkilo是个新手，做的不是很完善，老鸟请移驾到别的地方去玩下。小鸟不要唾骂，有什么不懂的地方到博客留言或颖佳论坛回帖！有些不足我会再后面不断的补充。

配置一般都不成什么大的问题（个人感觉,所以就不把自己破机子的配置传上来了）。

我的测试环境：win 7+xp +ubuntu+mac os x

祝大家顺利完成MAC OX X的安装以及有一个很好的体验。