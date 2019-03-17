---
title: vim 命令与快捷键
id: 558
categories:
  - Linux系统
date: 2013-07-07 14:30:35
tags:
---

:set nu 设置行号

&nbsp;

插入命令

i：光标后

I：行首

a:光标前

A:行末

o:光标后插入新行

O:光标上插入新行

定位

h:left

j:down

k:up

l:right

$:行尾

0：行首

H:(hight)屏幕上端

M:(mediun)屏幕中央

L:(lower)屏幕下方

&nbsp;

定位命令

:set nu

:set nonu

gg:到第一行

G:到最后一行

nG:到第n行

:n：到第n行

&nbsp;

删除命令

x:删除光标所在处的字符

nx:删除光标所在处后的n个字符

dd:删除光标所在行

ndd:删除第n行字符

gG:删除光标所在到文章底部的内容

D:删除光标所在到行首的

:n1,n2d:删除n1到n2行的所有内容

&nbsp;

复制粘贴

yy,Y:复制当前行

nyy,nY 复制当前行以下n行

dd:剪切当前行

ndd :剪切当前行以下n行

p,P：粘贴在当前光标所在行下或行上

&nbsp;

查找/替换

r:替换光标所在处

R:替换光标后的字符直到esc

u:取消，上一步ctrl+z(undo)

&nbsp;

/string: 查找n next，N pre set:ic(忽略大小写)

:%s/old/new/g:全文替换

：n1,n2s/old/new/g n1 to n2

：n1,n2s/old/new/c 询问

保存/退出

ZZ=:wq

:wq! owner root

:w dir/filename

:r filename 倒入文件内容

:r !date 倒入当前日期

:map ^p 0x&lt;ESC&gt;

^ 行首

：n1,n2s/^/#/g 添加行首#

：n1,n2s/^#//g 删除行首#

特殊字符转义\/\/\/

:ab a b  定义a =b

^p = ctrl+v+p