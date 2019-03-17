---
title: 修改wordpress密码的最好办法
tags:
  - wordpress密码
  - 修改wordpress密码
  - 修改wordpress密码源码
  - 修改wordpress密码的最好办法
id: 173
categories:
  - 笔记分享
date: 2010-12-14 11:50:16
---

很多时候因为搬家或者是升级导致了wordpress密码不对，其实是部分文件没有更新从配置文件更新过来。发邮件的方式是可以，但是邮件要花时间，而且要是邮箱都高忘记了怎么办呢？如何修改wordpress密码？下面给你推荐一种个人认为修改wordpress密码的最好办法！

将下列代码保存为fliename.php.传到你得wordpress根目录，然后在网址中网页中打开上传的文件。输入新的密码。点击提交查询！

> &lt;?php
> 
> //password resetter
> 
> include("wp-config.php");
> 
> include("wp-blog-header.php");
> 
> if (empty($_POST['emergency_pass'])) {
> 
> ?&gt;
> 
> &lt;form method="post"&gt;
> 
> 设置 username 密码: &lt;input name="emergency_pass" type="password" /&gt;
> 
> &lt;input type="submit" /&gt;
> 
> &lt;/form&gt;
> 
> &lt;?php
> 
> } else {
> 
> $sql = "UPDATE ".$wpdb-&gt;users." SET user_pass = '".md5($_POST['emergency_pass'])."' WHERE User_login = 'username";
> 
> $link = $wpdb-&gt;query($sql);
> 
> wp_redirect('wp-login.php');
> 
> exit();
> 
> }
> 
> ?&gt;

把对应的用户名修改。