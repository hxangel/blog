---
title: plupload图片上传插件的使用
id: 624
categories:
  - 笔记分享
date: 2014-04-30 18:05:25
tags:
---

plupload算是一个好东西（用过的人都知道），用起来不好不坏的，当然每个插件在使用过程中未必跟业务完全耦合，就看你修改插件让其符合业务还是业务适应插件，这里对plupload作一个简单的介绍和分享一些个人心得。

### plupload简介

Plupload是有TinyMCE的开发者开发的，为您的内容管理系统或是类似上传程序提供一个高度可用的上传插件。Plupload 目前分为一个核心API 和一个jQuery上传队列部件，这样使你可以直接使用或是自己定制。

### plupload特性

*   Plupload使用jQuery的组件做为选择文件和上传文件的队列组件。
*   Plupload使用Flash，Silverlight，HTML5，Gears，BrowserPlus、FileUpload上传文件技术引擎。
*   Plupload允许自定义使用Plupload核心API来进行选择文件与上传文件。
*   JavaScript用来激活文件选择对话框。此文件选择对话框是可以设置允许用户选择一个单独的文件或者是多个文件。 选择的的文件类型也是可以被限制的，因此用户只能选择指定的适当的文件，例如jgp;gif。
*   Plupload允许对上传过程中的一些事件进行自定义，写上自己的处理方式。
*   选定的文件的上传和它所在页面、表单是独立的。每个文件都是单独上传的，这就保证了服务端脚本能够在一个时间点更容易地处理单个文件。具体信息可以访问Plupload官方网站：http://www.plupload.com/

### plupload配置说明

*   Browse_button:触发浏览文件按钮标签的唯一id,,在flash、html5、和silverlight中能找到触发事件的源（我理解的，这个参数在队列部件不需要参见）
*   Container: 展现上传文件列表的容器，[默认是body]
*   chunk_size：当上传文件大于服务器接收端文件大小限制的时候，可以分多次请求发给服务器，如果不需要从设置中移出
*   drop_element：当浏览器支持拖拽的情况下，能够文件拖放到你想要的容器ID里
*   file_data_name：设置上传字段的名称。默认情况下被设置为文件。（我试验了没找到该如何使用它，暂且不提）
*   filters:选择文件扩展名的过滤器,每个过滤规则中只有title和ext两项[{title:'', extensions:''}]
*   flash_swf_url:flash文件地址
*   headers：自定义的插入http请求的键值对
*   max_file_size：最大上传文件大小（格式100b, 10kb, 10mb, 1gb）
*   multipart：布尔值，如果用mutlipart 代替二进制流的方式，在webkit下无法工作
*   multipart_params： 跟 multipart关联在一起的键值
*   multi_selection： 多选对话框
*   resize：修改图片属性 resize: {width: 320, height: 240, quality: 90}
*   runtimes:上传插件初始化选用那种方式的优先级顺序，如果第一个初始化失败就走第二个，依次类推
*   required_features：需要那些特性，才能初始化插件
*   url：上传服务器地址
*   unique_names：是否生成唯一的文件名，避免与服务器文件重名
*   urlstream_upload：布尔值 如果是flash上传应该用URLStream 代替FileReference.upload

### pluload API文档

#### 方法列表

方法列表：

*   Uploader(setting)：创建实例的构造方法
*   bind(event, function[, scope])：绑定事件
*   destroy()：销毁plupload的实例对象
*   uploader.destroy()
*   getFile(id): 获取上传文件信息
*   init:初始化plupload实例，添加监听对象
*   uploader.destroy()
*   refresh：重新实例化uploader
*   removeFile(id):从file中移除某个文件
*   splice(start,length)：从队列中start开始删除length个文件， 返回被删除的文件列表
*   start() 开始上传
*   stop()停止上传
*   unbind(name, function): 接触事件绑定
*   unbindAll()解绑所有事件

#### 属性集合

*   features：uploader中包含那些特性
*   files:当前队列中的文件列表
*   id：uploader实例的唯一id
*   runtime：当前运行环境（是html5、flash等等)
*   state:当前上传进度状态
*   total：当前上传文件的信息集合

#### 事件集合

*   BeforeUpload(up, file)：文件上传完之前触发的事件
*   ChunkUploaded(up, file,response)文件被分块上传的事件
*   Destroy(up):uploader的destroy调用的方法
*   Error(up, err)：上传出错的时候触发
*   Fileadded(up, files):用户选择文件时触发
*   FileRemoved(up, files):当文件从上传队列中移除触发
*   FileUploaded(up, file, res):文件上传成功的时候触发
*   Init(up):当初始化的时候触发
*   PostInit(up):init执行完以后要执行的事件触发
*   QueueChanged(up):当文件队列变化时触发
*   Refresh(up):当silverlight/flash或是其他运行环境需要移动的时候触发
*   StateChanged(up)当整个上传队列被改变的时候触发
*   UploadComplete(up,file)当队列中所有文件被上传完时触发
*   UploadFile(up,file)当一个文件被上传的时候触发
*   UploadProgress(up,file):当文件正在被上传中触发

### 应用实例

### 
1.hmtl部分
<pre class="lang:xhtml decode:true">&lt;div class="form-group"&gt;
    &lt;label class="control-label col-md-2"&gt;缩略图&amp;nbsp;&amp;nbsp;&lt;/label&gt;
    &lt;div class="col-10"&gt;
        &lt;div class="col-md-4" id="filelist"&gt;
            &lt;input type="text" name="thumbimg" class="form-control col-md-2"/&gt;
            &lt;label for="none" class="control-label processbar col-md-1"&gt;&lt;/label&gt;
        &lt;/div&gt;
        &lt;div id="uploader" class="col-md-5"&gt;
            &lt;button type="button" id="pickfiles" class="btn blue"&gt;选择图片&lt;/button&gt;
            &lt;button type="button" id="uploadfiles" class="btn default"&gt;上传文件&lt;/button&gt;
            &lt;pre id="console" class="display-hide"&gt;&lt;/pre&gt;
        &lt;/div&gt;
    &lt;/div&gt;
&lt;/div&gt;</pre>
2.js部分
<pre class="lang:js decode:true">   $(function () {
        var uploader = new plupload.Uploader({
            runtimes: 'html5,flash,silverlight,html4',
            browse_button: 'pickfiles', // you can pass in id...
            container: document.getElementById('uploader'), // ... or DOM Element itself
            url: '/extend/common/upload',
            flash_swf_url: '/assets/plugins/plupload/Moxie.swf',
            silverlight_xap_url: '/assets/plugins/plupload/Moxie.xap',

            filters: {
                max_file_size: '10mb',
                mime_types: [
                    {title : "Image files", extensions : "jpg,gif,png"},
                    {title : "Zip files", extensions : "zip"}
                ]
            },
            init: {
                PostInit: function () {
                    $('#uploadfiles').html("上传文件");
                    $("#uploadfiles").on('click', function () {
                        uploader.start();
                        return false;
                    });
                },
                FilesAdded: function (up, files) {
                    var html = "";
                    plupload.each(files, function (file) {

                        html = '&lt;input type="text" name="thumbimg" class="form-control '+file.id+'" value="' + file.name + '"/&gt;&lt;label for="none" class="control-label processbar col-md-1 ' + file.id + '" &gt;&lt;/label&gt;';
                    });
                    $("#filelist").html(html);
                },

                UploadProgress: function (up, file) {
                    $("label." + file.id).html(file.percent + '%');
                },
                FileUploaded: function (up, file,response) {
                    var res = $.parseJSON(response.response);
                    $("input." + file.id).val(res.result);
                },
                Error: function (up, err) {
                    document.getElementById('console').innerHTML += "\nError #" + err.code + ": " + err.message;
                }
            }
        });
        uploader.init();
    });</pre>
&nbsp;