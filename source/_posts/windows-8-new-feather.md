---
title: 如何开启windows 8的隐藏功能
tags:
  - windows 8
  - windows 8 M1 build 7850
  - windows 8 M2 build 7955
  - Windows 8 Milestone-2 (7955.0.110228-1930)
  - windows 8隐藏功能
  - 开启windows 8的隐藏功能
id: 269
categories:
  - 笔记分享
date: 2011-04-28 00:00:00
---

假如你安装并激活了 Windows 8 M1 Build 7850 或者 Windows 8 M2 (Pre-M3) Build 8955, 或许很多人会失望windows 8 跟windows 7没有什么区别，我当时也有这样的感觉，而且windows 8采用了windows 7 安装器，刚刚下载回来的时候还怀疑是不是镜像文件下载错了。其实windows 8 build 里面加入了很多功能。只是默认是关闭的。我们需要自己手动开启才能看到效果。

## 在Windows 8 M2 (Pre-M3) Build 7955 中可以开启的功能

* * *

### Ribbon UI

在 HKEY_CLASSES_ROOT\CLSID\ 下创建一个{4F12FF5D-D319-4A79-8380-9CC80384DC08} 键, 在这个键下然后创建一个名字为**AppID** 字符串的键，键值为**{9198DA45-C7D5-4EFF-A726-78FC547DFF53}** 
  > [HKEY_CLASSES_ROOT\CLSID\{4F12FF5D-D319-4A79-8380-9CC80384DC08}]      
> &quot;AppID&quot;=&quot;{9198DA45-C7D5-4EFF-A726-78FC547DFF53}&quot;  

重启explorer或者重启电脑。打开资源管理器即可看到效果。

[![clip_image001](http://www.vkilo.com/wp-content/uploads/2011/04/clip_image001_thumb.jpg "clip_image001")](http://www.vkilo.com/wp-content/uploads/2011/04/clip_image001.jpg)

### Application Explorer

Application Explorer 可以通过创建或者是重命名一个目录名字为
  > Applications.{4234d49b-0245-4df3-b780-3893943456e1}  

### Full DWM

在
  > HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\DWM  

新建 名字为 **hide blur** 类型为DWORD 的键值1

然后, 按 Ctrl + Shirt + F9 两次激活

### Metro UI

打开
  > %windir%**\System32\oobe\windeploy.exe**&#160;  

或者
  > %windir%**\System32\oobe\msoobe.exe**  

## 在 Windows 8 M1 Build 7850 可开启功能

* * *

### 资源管理器 Ribbon UI 

同 Windows 8 M2 (Pre-M3) Build 7955 

&#160;

### WebCam (Microsoft MoCam) 

在
  > <ins>HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\GRE_Initialize\</ins>  

下新建一个DWORD 类型名字为 **RemoteFontBootCacheFlags**, 值为**0x0000100f** 或者**4111十进制。**
  > [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\GRE_Initialize]      
> &quot;RemoteFontBootCacheFlags&quot;=dword:0000100f  

### PDF Reader (Modern Reader)（PDF阅读器）

在

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Curr entVersion\Applets\Paint\Capabilities

下新建一个字符串类型名字为 **CLSID**,键值为**{D3E34B21-9D75-101A-8C3D-00AA001A1652}** 键。

打开 **glcnd.exe** 允许 PDF Modern Reader.
  > <ins>[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Applets\Paint\Capabilities]        
> &quot;CLSID&quot;=&quot;{D3E34B21-9D75-101A-8C3D-00AA001A1652}&quot;</ins>  

**TaskUI **

<ins>在 </ins>
  > HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\TaskUI  

新建一个 32位 DWORD 键名字为**TaskUIEnabled**, 值为**1**。
  > [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\TaskUI]      
> &quot;TaskUIEnabled&quot;=dword:00000001  

假如你不想折腾那么你也可以直接下载以下文件来开启相应的功能。[Win8-M1-8750-Registry.zip](http://www.mediafire.com/?2ob6ka38k8n98z5).

还有几个软件分别名字叫 Windows 8 Tweaker, Windows 8 BluePoison, SK Patch v2 Beta1 和一些其他不同的工具他们的功能都是一样的, 也可以根据自己喜欢下载。