---
title: 'windows 8 pid 4 system  80 port '
id: 556
categories:
  - 笔记分享
date: 2013-07-04 10:46:51
tags:
---

<span style="text-decoration: underline;">Start Command Prompt:</span>
1\. Hit the combination key of Windows+R (or start run window)
2\. Type cmd and hit enter.
3\. This will open the command prompt

<span style="text-decoration: underline;">Check which process is using port 80:</span>
1\. On the command prompt window, type the following command (copy and paste) without the " ".

"netstat -o -n -a | findstr 0.0:80"

1\. The last column is what is called as the process ID column.

<span style="text-decoration: underline;">Open Task Manager to check the process ID:</span>
1\. Right click on the taskbar to open the the task manager.
2\. Go to the Processes tab.
3\. Click the View menu
4\. And make sure you select the PID (Process Identifier) as shown in the image below.
5\. Now you’ll be able to see which process is using the PID in question. In my case the process ID was 4 which stood for NT AUTHORITY/SYSTEM.
Do not kill that process! If you do you will get a blue screen of death (BSOD). This is an important process comprised of various services. The service in question is (the one using port 80) “World Wide Web Publishing Service (W3SVC)“. This is the service using port 80\. Go to the service and stop it..

<span style="text-decoration: underline;">To stop this service:</span>
1\. Go to Task Manager.
2\. Click the Services tab
3\. Arrange the Services by description.
4\. Look for something that reads World Wide Web Publishing Service in the description column
5\. Right click on it and select Stop Sevice.

That's it, now try and connect with tiny umbrella and you will see that it will not give you the dreaded error that something is using port 80\. I do not know how important the W3SVC service is, so, once you finish with tiny umbrella turn it back on again.

This tut was not done by me, my only credit is to find it and modify it a bit and posting it here.

Hope this helps you guys and if it does you know what to do! PRESS THANKS!