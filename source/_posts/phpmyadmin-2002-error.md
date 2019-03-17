---
title: phpMyAdmin – 错误 无法在发生错误时创建会话，请检查 PHP 或网站服务器日志，并正确配置 PHP 安装。
tags:
  - phpMyAdmin
  - phpMyAdmin错误
  - 无法在发生错误时创建会话
  - 请检查 PHP 或网站服务器日志
id: 139
categories:
  - 笔记分享
date: 2010-12-04 09:53:57
---

方法1.开始运行、输入%windir%\temp;清空里面的所有内容，返回到windows目录，右键temp目录——属性，点到安全选项，如果没有你可以在窗口的上边点开 工具——文件夹选项——查看——将“使用单文件共享(推荐)”钱的勾去掉就有了;将此文件夹USER用户权限设置为完全控制就能解决。

方法2.  在c盘windows目录下 php.ini
比如你可以找到这一行session.save_path = “某个路径”
改为 session.save_path = “yourpath”
然后要建yourpath对应的目录。