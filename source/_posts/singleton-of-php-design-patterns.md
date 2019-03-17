---
title: 设计模式之PHP单例模式
id: 477
categories:
  - 编程
date: 2013-05-14 23:30:38
tags:
---

> 单例模式是一种常用的软件设计模式。在它的核心结构中只包含一个被称为单例类的特殊类。通过单例模式可以保证系统中一个类只有一个实例而且该实例易于外界访问，从而方便对实例个数的控制并节约系统资源。如果希望在系统中某个类的对象只能存在一个，单例模式是最好的解决方案。
上面的话来自百度。我个人的理解就是只能是实例化一次，如DB类等。

接下来自己写了一个PHP的单例模式实例。仅仅参考
<pre class="lang:php decode:true">&lt;?php
/**
 *
 */
class Singleton
{  
    private static $_instance;
    //私有化__construct，禁止外部直接实例化
    private function __construct()
    {
    }
    //私有化克隆外部克隆
    private function __clone()
    {
    }
    //获取实例，假如没有单例的实例，这返回new一个进行实例化，并返回实例
    public static function getInstance()
    {
        if (is_null(self::$_instance)||!isset(self::$_instance)) {
            self::$_instance = new Singleton();
        }
        return self::$_instance;
    }
    //测试函数
    public function aa(){
      $this-&gt;bb();
    }
    private function bb(){
        return 'bb';
    }
}</pre>
上面是一个最基本的PHP单例模式，后面可以封装很多函数供外部调用；

下面访问Class中的aa函数进行测试代码如下：
<pre class="lang:php decode:true">&lt;?php
echo Singleton::getInstance()-&gt;aa();</pre>
这样可以看到打印出了'bb'；