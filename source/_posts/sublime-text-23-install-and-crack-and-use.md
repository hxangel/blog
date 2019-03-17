---
title: Sublime Text 2/3安装与注册及使用
id: 633
categories:
  - 笔记分享
date: 2014-05-31 20:02:05
tags:
---

久闻sublime text editor 是个神器，其实平时很少用，今天闲来无事儿，特地安装尝试一下，果断各种黑

## 1.Sublime Text 安装

下载地址：http://www.sublimetext.com/
<pre class="lang:sh decode:true">tar -jxf tar -jxf Sublime\ Text\ 2.0.2\ x64.tar.bz2
mv Sublime\ Text\ 2 /usr/local/sublime
ln -s /usr/local/sublime/sublime_text /usr/bin/sublime
#假如为Sublime text 3 安装于/opt/sublime_text_3
vim /usr/bin/subl
#输入以下内容并保存
#!/bin/bash

SUBLIME_HOME="/opt/sublime_text"
LD_LIB=$SUBLIME_HOME/libsublime-imfix.so
sh -c "LD_PRELOAD=$LD_LIB $SUBLIME_HOME/sublime_text $@"
</pre>

## 2.Sublime Text 注册与破解

安装16进制编辑器
<pre class="lang:sh decode:true">yum install ghex
ghex /usr/local/sublime/sublime_text</pre>
在菜单悬在[Edit]-&gt;[Replace]

找到

33 42

替换为

32 42
选择Replace All

保存退出（[File]&gt;[Save]-&gt;[Exit]）

打开sublime

点击菜单[Help]-&gt;[Enter License]

输入以下License
sublime text 2
<pre class="lang:default decode:true">—–BEGIN LICENSE—–
Patrick Carey
Unlimited User License
EA7E-18848
4982D83B6313800EBD801600D7E3CC13
F2CD59825E2B4C4A18490C5815DF68D6
A5EFCC8698CFE589E105EA829C5273C0
C5744F0857FAD2169C88620898C3845A
1F4521CFC160EEC7A9B382DE605C2E6D
DE84CD0160666D30AA8A0C5492D90BB2
75DEFB9FD0275389F74A59BB0CA2B4EF
EA91E646C7F2A688276BCF18E971E372
—–END LICENSE—–
</pre>
sublime text 3
<pre class="lang:default decode:true">----- BEGIN LICENSE ----
Andrew Weber
Single User License
EA7E-855605
813A03DD 5E4AD9E6 6C0EEB94 BC99798F
942194A6 02396E98 E62C9979 4BB979FE
91424C9D A45400BF F6747D88 2FB88078
90F5CC94 1CDC92DC 8457107A F151657B
1D22E383 A997F016 42397640 33F41CFC
E1D0AE85 A0BBD039 0E9C8D55 E1B89D5D
5CDB7036 E56DE1C0 EFCC0840 650CD3A6
B98FC99C 8FAC73EE D2B95564 DF450523
------ END LICENSE ------</pre>
&nbsp;

点击[Use License]

## 3.Sublime Text中文输入法问题

Fcitx输入法无法在Sublime Text 中输入中文的解决办法如下：
新建sublime-imfix.c文件
<pre class="lang:default decode:true">vim sublime-imfix.c</pre>
粘帖以下代码到sublime-imfix.c
<pre class="lang:c++ decode:true">/*
sublime-imfix.c
Use LD_PRELOAD to interpose some function to fix sublime input method support for linux.
By Cjacker Huang

gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
LD_PRELOAD=./libsublime-imfix.so subl
*/
#include &lt;gtk/gtk.h&gt;
#include &lt;gdk/gdkx.h&gt;
typedef GdkSegment GdkRegionBox;

struct _GdkRegion
{
  long size;
  long numRects;
  GdkRegionBox *rects;
  GdkRegionBox extents;
};

GtkIMContext *local_context;

void
gdk_region_get_clipbox (const GdkRegion *region,
            GdkRectangle    *rectangle)
{
  g_return_if_fail (region != NULL);
  g_return_if_fail (rectangle != NULL);

  rectangle-&gt;x = region-&gt;extents.x1;
  rectangle-&gt;y = region-&gt;extents.y1;
  rectangle-&gt;width = region-&gt;extents.x2 - region-&gt;extents.x1;
  rectangle-&gt;height = region-&gt;extents.y2 - region-&gt;extents.y1;
  GdkRectangle rect;
  rect.x = rectangle-&gt;x;
  rect.y = rectangle-&gt;y;
  rect.width = 0;
  rect.height = rectangle-&gt;height;
  //The caret width is 2;
  //Maybe sometimes we will make a mistake, but for most of the time, it should be the caret.
  if(rectangle-&gt;width == 2 &amp;&amp; GTK_IS_IM_CONTEXT(local_context)) {
        gtk_im_context_set_cursor_location(local_context, rectangle);
  }
}

//this is needed, for example, if you input something in file dialog and return back the edit area
//context will lost, so here we set it again.

static GdkFilterReturn event_filter (GdkXEvent *xevent, GdkEvent *event, gpointer im_context)
{
    XEvent *xev = (XEvent *)xevent;
    if(xev-&gt;type == KeyRelease &amp;&amp; GTK_IS_IM_CONTEXT(im_context)) {
       GdkWindow * win = g_object_get_data(G_OBJECT(im_context),"window");
       if(GDK_IS_WINDOW(win))
         gtk_im_context_set_client_window(im_context, win);
    }
    return GDK_FILTER_CONTINUE;
}

void gtk_im_context_set_client_window (GtkIMContext *context,
          GdkWindow    *window)
{
  GtkIMContextClass *klass;
  g_return_if_fail (GTK_IS_IM_CONTEXT (context));
  klass = GTK_IM_CONTEXT_GET_CLASS (context);
  if (klass-&gt;set_client_window)
    klass-&gt;set_client_window (context, window);

  if(!GDK_IS_WINDOW (window))
    return;
  g_object_set_data(G_OBJECT(context),"window",window);
  int width = gdk_window_get_width(window);
  int height = gdk_window_get_height(window);
  if(width != 0 &amp;&amp; height !=0) {
    gtk_im_context_focus_in(context);
    local_context = context;
  }
  gdk_window_add_filter (window, event_filter, context);
}</pre>
保存并退出
编译代码，先安装支持库，然后编译，并且拷贝到安装目录下
<pre class="lang:sh decode:true">yum install gtk3 gtk2 gtk3-devel gtk2-devel
gcc -shared -o libsublime-imfix.so sublime-imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
cp libsublime-imfix.so /usr/local/sublime/lib/</pre>
将编译好的扩展文件加入到参数中就会见到奇迹

## 4.设置

### 启动图标

上面我们已经编译好了输入法支持的扩展，现在通过启动参数加进来，具体操作如下
<pre class="lang:sh decode:true">sublime /usr/share/applications/sublime.desktop</pre>
<pre class="lang:default decode:true">[Desktop Entry]
Version=2.0.2
Name=Sublime Text 2
# Only KDE 4 seems to use GenericName, so we reuse the KDE strings.
# From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.
GenericName=Text Editor

Exec=bash -c 'LD_PRELOAD=/usr/local/sublime/lib/libsublime-imfix.so sublime'
Terminal=false
Icon=/usr/local/sublime/Icon/48x48/sublime_text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow

[NewWindow Shortcut Group]
Name=New Window
Exec=bash -c 'LD_PRELOAD=/usr/local/sublime/lib/libsublime-imfix.so sublime' -n
TargetEnvironment=Unity</pre>
如果在sublime_text_3中请编辑
<pre class="lang:default decode:true ">/usr/share/applications/sublime_text.desktop</pre>
修改对应的Exec如下
<pre class="lang:default decode:true ">[Desktop Entry]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text %F
[...]

[Desktop Action Window]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text -n
[...]

[Desktop Action Document]
[...]
Exec=env LD_PRELOAD=/opt/sublime_text/libsublime-imfix.so /opt/sublime_text/sublime_text --command new_file
[...]</pre>
保存后就可以输入中文了

&nbsp;

然后在你的Applications里面会出现Sublime Text菜单

### 安装 Package Control

基本上是必备扩展打开如下网站
https://sublime.wbond.net/installation
ctrl+`/[View] &gt; [Show Console]
从网站复制相应版本代码——粘帖——回车
重启Sublime Text
安装成功后，接下来安装Emmet（ZenCoding）举例
快捷键Ctrl + Shift + P 调出输入输入Install 回车，输入 Emmet 重启Sublime Text后便可以使用Emmet（ZenCoding）