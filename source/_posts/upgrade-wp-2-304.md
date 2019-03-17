---
title: 手动升级wordpress到wordpress 3.0.4
tags:
  - wordpress 3.0.4
  - wordpress 3.0.4下载地址
  - wordpress更新
  - 手动升级wordpress到wordpress 3.0.4
  - 手动升级到wordpress 3.0.4
id: 209
categories:
  - 笔记分享
date: 2010-12-30 19:56:37
---

<div>wordpress 3.0.4发布，这次更新修复了以往版本使用的叫做 KSES 的 HTML 转义库（HTML sanitation library）的重大问题。 </div>  

## wordpress 3.0.4下载地址
  <div>   

* * *
</div>  <div>简体中文版下载地址：[http://cn.wordpress.org/wordpress-3.0.4-zh_CN.zip](http://cn.wordpress.org/wordpress-3.0.4-zh_CN.zip "http://cn.wordpress.org/wordpress-3.0.4-zh_CN.zip")</div>  <div>英文版下载地址：[http://wordpress.org/wordpress-3.0.4.zip](http://wordpress.org/wordpress-3.0.4.zip "http://wordpress.org/wordpress-3.0.4.zip") </div>  

## 手动升级到wordpress 3.0.4
  <div>   

* * *
</div>  <div>只需更新以下文件即可</div>  <div>   <pre>wp-includes/version.php
wp-includes/formatting.php
wp-includes/kses.php
readme.html
wp-admin/includes/update-core.php</pre>
</div>