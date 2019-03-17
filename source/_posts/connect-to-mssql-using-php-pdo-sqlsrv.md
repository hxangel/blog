---
title: '使用php pdo 连接到mssql sqlsrv '
id: 561
categories:
  - 笔记分享
date: 2013-07-19 20:43:58
tags:
---

首先到官方http://msdn.microsoft.com/en-us/sqlserver/ff657782.aspx 下载相应的驱动。
然后windows为例
<pre class="lang:sh decode:true">extension=php_pdo_odbc.dll
extension=php_pdo_sqlsrv_54_nts.dll
extension=php_sqlsrv_54_nts.dll</pre>
 查看phpinfo中是否已经开启MsSQL
 接下来用代码测试即可
<pre class="lang:php decode:true">$DSN  = "mssql:host=localhost;dbname=testdb";//mssql dsn
$DSN="sybase:host=localhost;dbname=testdb";//sybase dsn
$DSN="dblib:host=localhost;dbname=testdb";//any dsn
$DSN = "sqlsrv:Server=localhost,1521;Database=testdb";//ms sql server
$dbUser = "dbuser";//username
$dbPass = "password";//password
$conn = new PDO($DSN,$dbUser,$dbPass);//connect handle
$conn-&gt;setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);// set some attribute of pdo object
$query = "select * from table where field=:field;"; //T_SQL query 
$fieldValue = 'Value';//
$params = array(":field"=&gt;$fieldValue);
$getProducts = $conn-&gt;prepare($query);
$getProducts-&gt;execute($params);
$products= $getProducts-&gt;fetchAll(PDO::FETCH_ASSOC);</pre>