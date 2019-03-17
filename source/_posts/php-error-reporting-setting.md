---
title: PHP error_reporting 设置
id: 525
categories:
  - 编程
date: 2013-06-14 23:55:11
tags:
---

<pre class="lang:php decode:true " title="错误报告函数">function setErrorReporting()
{
    //从配置文件读取当前是否为开发环境
    if (DEV_ENV == true) {
        ini_set("error_reprorting", "E_ALL &amp; ~E_NOTICE");
        ini_set("display_errors", "on");
    } else {
        error_reporting(E_ALL);
        ini_set('display_errors', 'Off');
        ini_set("log_errors" , "On");
        ini_set('error_log', '/var/log/phperror.log');

    }
}</pre>

error_reporting() 设置 PHP 的报错级别并返回当前级别。

语法：error_reporting(report_level)

下面列出了report_level可能值：
<table><tbody><tr><th class="td100">值</th><th>常量</th><th>描述</th></tr><tr><td>1</td><td>E_ERROR</td><td>这是一个严重错误，不可恢复，如位置异常，内存不足等</td></tr><tr><td>2</td><td>E_WARNING</td><td>警告，最一般的错误，如函数的参数错误等</td></tr><tr><td>4</td><td>E_PARSE</td><td>解析错误，在解析PHP文件时产生，并强制PHP在执行前退出</td></tr><tr><td>8</td><td>E_NOTICE</td><td>通告表示可能在操作一些未知的变量等。在开发时可开启通告，以保证程序是"安全通告"的，瑞在正式系统中，应关闭通告</td></tr><tr><td>16</td><td>E_CORE_ERROR</td><td>这个内部错误是由于PHP加载扩展失败而导致的，并且会导致PHP停止运行并退出</td></tr><tr><td>32</td><td>E_CORE_WARNING</td><td>PHP启动时初始化过程中的警告(非致命性错)</td></tr><tr><td>64</td><td>E_COMPILE_ERROR</td><td>编译错误是在编译时发生，这个错误将导致PHP运行退出</td></tr><tr><td>128</td><td>E_COMPILE_WARNING</td><td>编译警告用于告诉用户一些不推荐的语法信息</td></tr><tr><td>256</td><td>E_USER_ERROR</td><td>用户定义的错误将导致辞PHP退出，它对是来自PHP自身，而是来自脚本文件中。</td></tr><tr><td>512</td><td>E_USER_WARNING</td><td>脚本使用它来通知一个执行失败，同时PHP也会用E_WARNING通知</td></tr><tr><td>1024</td><td>E_USER_NOTICE</td><td>用户定义的通告用于在脚本中表示可能存在的错误</td></tr><tr><td>2048</td><td>E_STRICT</td><td>编码标准化警告(建议如何修改以向前兼容)</td></tr><tr><td>4096</td><td>E_RECOVERABLE_ERROR</td><td>接近致命的运行时错误，若未被捕获则视同E_ERROR</td></tr><tr><td>8191</td><td>E_ALL</td><td>除E_STRICT外的所有错误(PHP6中为8191,即包含所有)</td></tr></tbody></table>

&nbsp;