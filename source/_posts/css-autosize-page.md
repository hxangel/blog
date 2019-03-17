---
title: 如何让页面自适应大小
id: 386
categories:
  - 笔记分享
date: 2012-02-21 20:45:32
tags:
---

话说这是深圳市德科科技有限公司的面试题目，住的是高楼，由于手机问题，结果走错地方了（面试的时候），心里甚是尴尬。完事了之后我内心是灰常的纠结。学习web有N年了，但是一些简单的东西都要借助网络或者是工具书。来这里折腾了好多天了都没有找到一份适合自己的工作。加之发骚，身体灰常不适。每天的生活就是去网吧投简历，然后等待电话通知面试。在找工作这一块还真不是我的强项。应聘的时候老是被一些很纠结的问题给把自己整out了。好久没有更新日志了。顺道来发泄下。发泄完毕。接下来说下面试题目的解决过程。

一个简单的单页面 头部(header)和底部(footer)高度为60px，背景色为RGB(787878)，宽度自适应;中间一个工具栏（sidebar）和内容区(content)并列 ，高度自适应;sidebar背景为RGB(007777)（这里我不记得了，随便弄的）宽度为160px ,在左边；content居右，宽度自适应；
刚拿到是不知道，所以在网上搜索了一下。得如下代码：
> &lt;script type="text/javascript"&gt;> 
> window.onload = windowHeight;//页面载入完毕执行函数> 
> function windowHeight() {> 
> var h = document.documentElement.clientHeight;//获取当前窗口可视操作区域高度> 
> var bodyHeight = document.getElementById("content");//寻找ID为content的对象（也就是你想要自适应高度的对象）> 
> if (h &lt; 598){//因为前边是获取的当前窗口的可视操作区域的高度 所以当调小窗口的时候 会造成不美观> 
> h = 598 ;> 
> bodyHeight.style.height = (h-289) + "px";// +“px” 是解决 firefox不识别 bodyHeight.style.height =h。289数字可以根据需要更改！> 
> }> 
> else bodyHeight.style.height = (h-289) + "px";
}
setInterval(windowHeight,500)//每半秒执行一次windowHeight函数

&lt;/script&gt;

根据这个稍微修改得到如下：
> &lt;!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"&gt;> 
> &lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;> 
> &lt;head&gt;> 
> &lt;title&gt;窗口特效-自适应高度的窗口&lt;/title&gt;> 
> &lt;meta http-equiv="content-type" content="text/html;charset=gb2312"&gt;> 
> &lt;style type="text/css"&gt;> 
> *{margin:0;padding:0px;}> 
> body{width:100%}> 
> #header,#footer{height:60px;width:100%;> 
> background:#787878;}> 
> #sidebar{width:160px;> 
> background:#336699;> 
> float:left;> 
> }> 
> #content{background:#669999;> 
> float:left;> 
> }#footer{> 
> clear:both;}> 
> &lt;/style&gt;> 
> &lt;script type="text/javascript"&gt;> 
> window.onload = windowHeight;//页面载入完毕执行函数> 
> function windowHeight() {> 
> var h = document.documentElement.clientHeight;//获取当前窗口可视操作区域高度> 
> var w= document.documentElement.clientWidth;//获取当前窗口可视操作区的宽度> 
> var sidebar = document.getElementById("sidebar");> 
> var content = document.getElementById("content");> 
> sidebar.style.height = (h-120) + "px";// +“px” 是解决 firefox不识别 bodyHeight.style.height =h。289数字可以根据需要更改！> 
> content.style.height = (h-120) + "px";> 
> content.style.width = (w-160) + "px";> 
> }> 
> &lt;/script&gt;&lt;/head&gt;> 
> &lt;body&gt;> 
> &lt;div id="header"&gt;&lt;/div&gt;> 
> &lt;div id="sidebar"&gt;&lt;/div&gt;> 
> &lt;div id="content"&gt;&lt;/div&gt;> 
> &lt;div id="footer"&gt;&lt;/div&gt;> 
> &lt;/body&gt;> 
> &lt;/html&gt;
这样就基本上实现了要求。

这里可以看[demo](http://www.vkilo.com/demo/auto_height_weight.html "自适应窗口高度宽度的方法")
还有一种css方法是margin-buttom:-9999px来实现。
不过个人感觉javascript的比较好。