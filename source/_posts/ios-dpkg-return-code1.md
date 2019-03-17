---
title: IOS 用Cydia安装软件 出现dpkg return code(1)
tags:
  - Cydia
  - dpkg return code(1)
  - ios
  - iPhone
id: 417
categories:
  - 移动设备
date: 2013-02-24 16:01:00
---

&nbsp;

### 用Cydia安装软件 出现dpkg return code(1)错误解决办法

* * *

用工具这里就不多说了。不过推荐使用SSH访问IOS的办法。这里的其实iTool之类的比较方便。

删掉所有/var/cache/apt/archives目录下与/var/lib/dpkg/info下相同的文件。

PS:

也就是/var/lib/dpkg/info下有的/var/cache/apt/archives下不能有。/var/cache/apt/archives目录为操作对象，/var/lib/dpkg/info 为参考对象。