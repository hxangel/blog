---
title: 遍历目录文件编码转换
id: 605
categories:
  - 笔记分享
date: 2014-04-11 11:20:40
tags:
---

遍历当前目录及子目录。把所有的文件转换编码到UTF-8

<pre class="lang:php decode:true " >&lt; ?php
//php iconv.php
//exec it on root dir
$path = dirname(__FILE__);
tree($path);

function encodeFiles($fileName)
{
//    echo $fileName;
    if (file_exists($fileName)) {
        // Read in the contents
        $res = file_get_contents($fileName);
        $i = pathinfo($fileName);
        if(!in_array($i['extension'],array('js','css','php','html','htm'))){
            return ;
        }
        // Just display on the screen the file being modified
        echo  $fileName . "---form---";
        // Convert the contents
        echo  $encode = mb_detect_encoding($res, array("ASCII", "UTF-8", "GB2312", "GBK"));
        echo "---to---UTF-8!\n";
        $res = iconv($encode, "UTF-8", $res);
        // Write back out to the same file
        file_put_contents($fileName, $res);
    } //
}

function tree($directory)
{
    $mydir = dir($directory);
    while ($file = $mydir-&gt;read()) {
        if ((is_dir("$directory/$file")) AND ($file != ".") AND ($file != "..")) {
            tree("$directory/$file");
        } else {
            $file ="$directory/$file";

//            echo "&lt;li&gt;$file&lt;/li&gt;\n";
            if(is_file($file)){
                encodeFiles($file);
            }
        }
    }
}</pre> 