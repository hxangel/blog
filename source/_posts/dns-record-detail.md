---
title: 域名记录详解 DNS记录详解 免费域名解析服务推荐
tags:
  - dns记录
  - 免费域名
  - 域名
  - 域名解析服务
  - 域名记录
  - 子域名
  - 推荐
id: 46
categories:
  - 笔记分享
date: 2010-11-14 11:06:35
---

## A记录

A (Address) 记录是用来指定主机名（或域名）对应的IP地址记录。用户可以将该域名下的网站服务器指向到自己的web server上。同时也可以设置您域名的子域名。通俗来说A记录就是服务器的IP,域名绑定A记录就是告诉DNS,当你输入域名的时候给你引导向设置在DNS的A记录所对应的服务器    

## 子域名

子域名道理等同二级域名，不过比二级域名更加延伸，比如我们继续扩展该域名的主机名，设置主机名为bbs.at,那么就可以建立一个三级域名：bbs.at.abc.com，当然也可以建立四级域名bbs.at.go.abc.com，五级域名bbs.at.go.home.abc.com……，依次类推，可以建立无限级别的域名，我们统称这些域名为顶级域名abc.com的子域名。    

## CNAME别名指向记录

NAME (Canonical Name)记录，通常称别名指向。在这里，您可以定义一个主机别名，比如设置ftp.***.com，用来指向一个主机www.***.com,那么以后就可以用FTP.***.com来代替访问www.***.com了。    

## MX记录

MX记录也叫做邮件路由记录，用户可以将该域名下的邮件服务器指向到自己的mail server上，然后即可自行操控所有的邮箱设置。您只需在线填写您服务器的IP地址，即可将您域名下的邮件全部转到您自己设定相应的邮件服务器上。    
简单的说，通过操作MX记录，您才可以得到以您域名结尾的邮局。现在很多公司都免费提供域名邮箱，你可以申请属于自己的域名邮箱，如TX     

## TXT 记录

TXT 记录，一般指为某个主机名或域名设置的说明，如：    
admin IN TXT &quot;管理员, 电话： 13901234567&quot;     
mail IN TXT &quot;邮件主机, 存放在xxx , 管理人：AAA&quot;     
Jim IN TXT &quot;contact: [abc@mailserver.com](mailto:abc@mailserver.com)&quot;     
也就是您可以设置 TXT ，以便使别人联系到您     

## SRV 记录

SRV 记录：一般是为Microsoft的活动目录设置时的应用。DNS可以独立于活动目录，但是活动目录必须有DNS的帮助才能工作。为了活动目录能够正常的工作，DNS服务器必须支持服务定位（SRV）资源记录，资源记录把服务名字映射为提供服务的服务器名字。活动目录客户和域控制器使用SRV资源记录决定域控制器的IP地址。    
此技术细节请参考相应网站     

## TTL值

TTL值全称是“生存时间（Time To Live)”，简单的说它表示DNS记录在DNS服务器上缓存时间。要理解TTL值，请先看下面的一个例子：    
假设，有这样一个域名myhost.abc.com（其实，这就是一条DNS记录，通常表示在abc.com域中有一台名为myhost的主机）对应IP地址为1.1.1.1，它的TTL为10分钟。这个域名或称这条记录存储在一台名为dns.abc.com的DNS服务器上。     
现在有一个用户在浏览器中键入一下地址（又称URL)[http://myhost.abc.com](http://myhost.abc.com) 这时会发生什么呢？     
该访问者指定的DNS服务器（或是他的ISP,互联网服务商, 动态分配给他的)8.8.8.8就会试图为他解释myhost.abc.com，当然8.8.8.8这台DNS服务器由于没有包含myhost.abc.com这条信息，因此无法立即解析，但是通过全球DNS的递归查询后，最终定位到dns.abc.com这台DNS服务器，dns.abc.com这台DNS服务器将myhost.abc.com对应的IP地址1.1.1.1告诉8.8.8.8这台DNS服务器，然有再由8.8.8.8告诉用户结果。8.8.8.8为了以后加快对myhost.abc.com这条记录的解析，就将刚才的1.1.1.1结果保留一段时间，这就是TTL时间，在这段时间内如果用户又有对myhost.abc.com这条记录的解析请求，它就直接告诉用户1.1.1.1，当TTL到期则又会重复上面的过程     

## 泛域名与泛解析

泛域名是指在一个域名根下，以 *.Domain.com 的形式表示这个域名根所有未建立的子域名。

这里我推荐免费域名解析服务gogaddy,算是世界上最大的域名提供商，服务很好！

地址：[https://www.godaddy.com/](https://www.godaddy.com/ "https://www.godaddy.com/")