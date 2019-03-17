---
title: MAC OS X 不能安装在这台机器上的解决办法
tags:
  - MAC OS X
  - 不能安装在这台机器上
  - 不能安装在这台电脑上
  - 解决办法
id: 157
categories:
  - Linux系统
date: 2010-12-13 12:29:00
---

一般出错会提示：MAC OS X 不能安装在这台机器上或者MAC OS X 不能安装在这台电脑上等。

关于这个错误是MBR分区的问题。这个我们通过替换了OSIntall还不够，还需要找到对应的OSIntall.mpkg替换原来的OSIntall.mpkg。

* * *

OSIntall替换位置在：
  <div>   <pre>/System/Library/PrivateFrameworks/Install.framework/Frameworks/OSInstall.framework/Versions/A</pre>
</div>

OSIntall.mpkg替换位置在：

<div>
  <pre>/System/Installation/Packages</pre>
</div>