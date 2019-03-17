---
title: 手动升级wordpress3.0.4到wordpress 3.0.5
tags:
  - wordpress 3.0.4
  - wordpress 3.0.4手动升级
  - wordpress 3.0.5
  - wordpress 3.0.5下载地址
  - wordpress 3.0.5简体中文版下载地址
  - wordpress升级
  - wordpress更新
  - 下载地址
id: 255
categories:
  - 笔记分享
date: 2011-02-16 17:56:01
---

最新wordpress 3.0.5

修复了**两个中等危险的安全问题**。在以往版本中，贡献者和作者可以自我提权。

修复了**一个信息泄露问题**。以往版本中，作者级别的用户可以通过某种方法看到他们不应看到的内容。

做出了**两个增强安全性的更改**。一个是为那些没有正确使用安全 API 的插件提供的，另一个是对我们之前发布的补丁进行更深层的修正。

wordpress 3.0.5简体中文版下载地址：[wordpress-3.0.5-zh_CN.zip](http://cn.wordpress.org/wordpress-3.0.5-zh_CN.zip "http://cn.wordpress.org/wordpress-3.0.5-zh_CN.zip")

为了避免升级不成功导致数据丢失可以直接更新以下文件进行手动升级
  <pre>wp-includes/default-filters.php
wp-includes/version.php
wp-includes/pluggable.php
wp-includes/kses.php
wp-includes/script-loader.php
readme.html
wp-admin/includes/post.php
wp-admin/includes/update-core.php
wp-admin/includes/template.php
wp-admin/js/post.dev.js
wp-admin/js/post.js
wp-admin/async-upload.php</pre>