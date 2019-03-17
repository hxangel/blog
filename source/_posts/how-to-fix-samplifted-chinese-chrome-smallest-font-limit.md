---
title: Chrome 中文版字体最小限制
tags:
  - Chrome
  - Chrome中文版
  - css
  - 字体12px
id: 415
categories:
  - 笔记分享
date: 2013-02-24 14:59:00
---

最近因为一个打印的页面在Chrome字体忽大忽小，错位很严重，其他的浏览器正常；于是我拿到我电脑上一看是正常的，于是对比一下两台电脑，我用的版本是英文版，显示正常。中文版本就有问题，我因为对CSS不是很感冒，我以为是默认字体的问题，于是我把英文版的字体配置与中文版本一致，但是结果我的英文版Chrome依然正常。于是我做了个艰难的决定，这肯定Chrome中文版本与英文版的区别。

原来是Chrome中文版字体显示问题，Google浏览器中文版本显示错位问题。默认的情况下，Chrome 中文版配置文件中对最小字体限制为12px，我的字体有9px或者更小的。于是：

### Chrome（Google浏览器）中文版本字体12px大小限制解决办法

* * *

需要使用 WebKit 私有CSS特性 '-webkit-text-size-adjust:none' 来避免最小字号限制；于是添加一个webkit的私有属性，就能解决问题。
> tag{-webkit-text-size-adjust:none;} /*tag为选择器*/
> html{-webkit-text-size-adjust: none;} /*也可以用全局的，但是影响范围很广*/
我用的是全局的，因为我这里需要对整个页面进行调整。而且错乱排列。