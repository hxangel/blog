---
title: firefox内存及资源优化
tags:
  - firefox
  - firefox优化
  - firefox内存问题
id: 203
categories:
  - 笔记分享
date: 2010-12-23 21:43:00
---

## firefox几点优化 

* * *

在firefox地址栏中输入about:config）   
1、加入一个boolean（布尔）项：config.trim_on_minimize,并设置为true,这样就可以在最小化时自动释放内存。    
2、修改browser.sessionhistory.max_total_viewers修改值为5或更小{页面快进/快退功能中保存的页面总数，默认是-1(无限)}。    
3、创建一个browser.cache.memory.capacity设置firefox使用多少内存来进行缓存，默认值-1基于系统内存自动设置，18432=18MB一般适用于512M~1G内存。    
4、 browser.cache.memory.enable[布尔值]该项和browser.cache.memory.capacity联合起作用。如果 设置为true，firefox将使用browser.cache.memory.capacity指定的内存大小来进行缓存。    
5、browser.urlbar.clickSelectsAll [布尔值]决定在地址栏单击时是高亮选中还是插入光标。    
6、browser.urlbar.hideGoButton [布尔值]决定是否显示地址栏右侧绿色的箭头（一般人都是敲回车的，这个实在是鸡肋）。    
7、 创建config.trim_on_minimize[布尔值]（仅限于windows）决定是否象其它windows应用程序一样最小化到任务栏时释放 内存，对于配置较低的电脑建议设置为true，配置还过的去的设置为false，这将加速firefox的最小化、最大化过程。    
8、 dom.disable_window_open_feature.*[布尔值]以 dom.disable_window_open_feature. 开头的设置总共有11个，*可以是 close，directories，location，menubar，minimizable，personalbar，resizable，scrollbars，status，titlebar，toolbar。 这些设置控制弹出窗口（主要是广告）的显示元素，比如将dom.disable_window_open_feature.close设置为true，则 会强迫弹出窗口在右上角显示一个关闭按钮。建议将close和resizeable设置为true。    
9、dom.popup_maximum [整数]能够同时打开的弹出窗口的数目。经常有一些恶意站点会冒出一大堆弹出窗口，直到屏幕崩溃为止。建议将该值设置为5或更小。    
10、extensions.dss.enabled [布尔值]决定是否能够动态主题切换。假如设置为true，在安装或切换主题时，将立刻显现出新主题的效果，而不用关闭firefox后重新引导firefox。    
11、 network.cookie.cookieBehavior[整数]决定firefox处理cookies的政策。设置为1允许所有的 cookies，设置为2禁止所有的cookies，设置为1仅允许原始站点的cookies，不允许第三方（大多是广告）的cookies。建议设置为 1。    
12、network.dnsCacheEntries [整数]（需创建）决定在firefox的DNS缓存中保存条目的数目。当在firefox中键入一个web地址时，它通过查询DNS服务器将web地址 转化为IP，在当地缓存中保存一定数量的DNS条目，下次再键入同样的web地址时，就能加快浏览速度。默认firefox将该值设置为20，建议将该值 设置为一般情况浏览web站点的数目。    
13、network.dnsCacheExpiration [整数]（需创建）决定缓存的DNS条目过期的时间。默认为60秒。    
14、 network.http.max-connections[整数]决定同时能够打开多少http连接。默认值是24，如果你的网络连接够快，可以尝试增 大此值，最大值为65535。但要注意的是，增大该值仅仅增大了同时打开http连接数目的可能，你并不能强迫firefox每次都打开那么多的 http连接。    
15、network.http.max-connections-per-server[整数]决定在单个服务器能够同时打开的 连接数。默认值为8，你可以增大此值来加快浏览速度，最大值为255。但要注意的是，此值改的太大，一些服务器会认为你在进行DDoS攻击，从而拒绝你的 连接请求。事实上，如果所有的firefox用户都不理智的把此值改的太大，大多数站点的浏览速度不会得到提升，反而会非常慢。    
16、 network.http.max-persistent-connections-per-proxy[整数]假如你使用的是代理，该值决定同时有多少 连接处于活动状态。默认值为4，可以适当增大此值加快浏览速度。但要注意的是，此值改的太大，会增大代理服务器的压力，从而影响每个使用该代理的用户的浏 览速度。    
17、network.http.max-persistent-connections-per-server[整数]假如没有使用代 理，该值决定在单个服务器上同时有多少连接处于活动状态。默认值为2，可以适当增大此值加快浏览速度，最大值为255。但要注意的是，此值改的太大会增大 服务器的压力，从而有可能被该服务器拒绝连接请求。    
18、network.http.pipelining [布尔值]决定是否使用HTTP Pipelining特性，建议设置为true，加快浏览速度，尽管该特性不是所有的服务器和代理都支持。    
19、 network.http.pipelining.maxrequests [整数]决定使用HTTPPipelining特性时发送的最大连接请求。默认值为4，最大值为8，比8大的值会被忽略，1表示不使用 HTTPPipelining特性，建议将该值设置为8。    
20、network.http.proxy.pipelining [布尔值]决定是否在使用代理时使用HTTP Pipelining特性。建议设置为true，要注意的是，该值有效的前提是network.http.proxy.keep-alive值为true。    
21、network.http.redirection-limit [整数]决定接受多少连续的重定向。比如说你进入一个站点旧的网址，可能会被重定向到一个新的网址，这叫一个重定向。    
22、network.prefetch-next [布尔值]决定是否使用Link Prefetching特性。建议设置为false。    
23、nglayout.initialpaint.delay [整数]（需创建）决定在显示页面内容时等待多少毫秒。适当的延迟可以让firefox引导和调整各种各样的页面元素以便正确显示。默认值是250毫秒，你可以增大或减小该值，当然，这取决于你的浏览习惯。    
24、plugin.default_plugin_disabled [布尔值]当浏览某个网页缺少某个插件（比如flash）时是否提示安装。    
25、privacy.popups.disable_from_plugins [整数]设置为0不阻止任何弹出窗口，设置为1阻止弹出窗口的最大数目取决于dom.popup_maximum，设置为3阻止所有的弹出窗口，设置为2 仅阻止来自插件的弹出窗口 

## firefox占很大资源(内存)问题

* * *

firefox地址栏输入about:cache查询缓存位置

firefox地址栏输入about:config 回车   
browser.cache.disk.capacity 磁盘缓存容量自己适当更改    
双击browser.cache.memory.enable 让它值为true    
新建字符串(string) 名称为browser.cache.disk.parent_directory 值为 /tmp

browser.cache.offline.capacity 磁盘缓存容量自己适当更改   
双击browser.cache.offline.enable 让它值为true    
新建字符串(string) 名称为browser.cache.offline.parent_directory 值为 /tmp 