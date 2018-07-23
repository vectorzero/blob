---
title: Nodejs上传图片
date: 2017-04-03 16:27:02
tags:
---

新建项目文件夹

在项目目录下打开命令窗口,输入

`npm install formidable --save-dev`

新建tmp,img文件夹

新建server.js,starter.js,uploader.js,shower.js文件

文件内容如下所示

<!-- more -->

### server.js
```javascript
var http = require('http'),
    url = require('url'),
    starter = require('./starter'),
    shower = require('./shower'),
    uploader = require('./uploader');

http.createServer(function(request, response){
    var pathname = url.parse(request.url).pathname;
    var routeurl = {
        '/' : starter.start,
        '/upload' : uploader.upload,
        '/show' : shower.show // 添加
    }

    if( typeof routeurl[pathname]=== 'function' ){
        routeurl[pathname](request, response);
    }else{
        console.log('404 not found!');
        response.end();
    }
}).listen(3000);
console.log('server has started...');
```

### starter.js
```javascript
function start(request, response){
    var html = '<html>\
        <head>\
        <meta charset=UTF-8" />\
        </head>\
        <body>\
        <form action="/upload" method="post" enctype="multipart/form-data">\
        <p>file : <input type="file" name="upload" multiple="multiple" /></p>\
        <p><input type="submit" value="submit" name="submit" /></p>\
        </form>\
        </body>\
        </html>';

    response.writeHead(200, {"Content-Type":"text/html"});
    response.write( html );
    response.end();
}
exports.start = start;
```

### uploader.js
```javascript
var formidable = require('formidable'),
    util = require('util'),
    fs = require('fs');

function upload(request, response){
    if( request.method.toLowerCase()=='post' ){
        var form = new formidable.IncomingForm();

        form.uploadDir = './tmp/';
        form.parse(request, function(err, fields, files) {
            var oldname = files.upload.name,
                newname = Date.now() + oldname.substr(oldname.lastIndexOf('.'));
            fs.renameSync(files.upload.path, "./img/"+newname ); // 同步上传图片
            var s = '<p><a href="/">back!</a></p><p><img src="/show?src='+newname+'" /></p>'; // 显示刚才的图片
            response.writeHead(200, {'content-type': 'text/html'});
            response.write(s);
            response.end();
        });
        return;
    }
}
exports.upload = upload;
```

### shower.js
```javascript
var fs = require('fs'),
    url = require('url');

function show(request, response){
    var query = url.parse(request.url, true).query,
        imgurl = query.src;

    // 读取图片并进行输出
    // 这里读取链接中的src参数，指定读取哪张图片  /show?src=1484234660592.png
    fs.readFile('./img/'+imgurl, "binary", function(err, file){
        if(err) throw err;
        response.writeHead(200, {"Content-Type": "image/png"});
        response.write(file, "binary");
        response.end();
    })
}
exports.show = show;
```

在目录下的命令窗口输入

`node server.js`

在浏览器地址了输入 [http://localhost:3000/](http://localhost:3000/)

即可预览到效果了！