---
title: 解决LC IS UPDATE SITEMAP WHEN POST
id: 699
categories:
  - 笔记分享
date: 2015-03-24 14:39:44
tags:
---

如何解决BAIDU SITEMAP GENERATOR插件出现 ILLEGAL STRING OFFSET LC_IS_UPDATE_SITEMAP_WHEN_POST问题呢？当发布文章的时候，出现了这个，于是便有了下文。 ILLEGAL STRING OFFSET   这个错误请看鸟哥的《[PHP5.4更新注意点](http://www.laruence.com/2011/12/19/2409.html)》

wordpress网址地图插件现在用得比较多的就是柳城的《[Baidu Sitemap Generator](http://www.liuzhishi.com/314.html)》，我现在用的也是这个！但是有时候会报一个这样的问题！在发布或更新文章，出现的 PHP Warning:Illegal string offset ‘ lc_is_update_sitemap_when_post ’ in ……/wp-content/plugins/baidu-sitemap-generator/baidu_sitemap.php on line 406， 出现这问题的解决办法是：
打开 baidu-sitemap.php 文件中的第 406 行：
把下面的代码：
<pre class="lang:php decode:true ">if($get_baidu_sitemap_options[' lc_is_update_sitemap_when_post '] == ’1′){
    wp_clear_scheduled_hook(‘do_baidu_sitemap_by_post’);
    wp_clear_scheduled_hook(‘do_this_auto_daily’);
    wp_schedule_single_event(time()+10, ‘do_baidu_sitemap_by_post’);
}</pre>
直接把条件语句注释掉， 改为：
<pre class="lang:php decode:true">//if($get_baidu_sitemap_options[' lc_is_update_sitemap_when_post '] == ’1′){
wp_clear_scheduled_hook(‘do_baidu_sitemap_by_post’);
wp_clear_scheduled_hook(‘do_this_auto_daily’);
wp_schedule_single_event(time()+10, ‘do_baidu_sitemap_by_post’);
//}</pre>
就行了。

修改后的代码大致意思是：每当发布文章时，sitemap都会自动更新。