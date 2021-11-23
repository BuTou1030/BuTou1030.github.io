---
title: Node.js学习day01
copyright: true
date: 2020-11-23 23:40:57
toc: true
tags: [前端,nodejs]
categories: [前端,nodejs]
---
# Node.js学习day01
---
<!-- more -->

## 1.1http模块的初步使用

```javascript
//引入http模块
var http = require('http');

/*
	request 获取客户端传过来的信息
	response 给浏览器响应信息
*/
http.createServer(function(request, response) {
    //设置响应头
    //状态码 200, 文件类型 html, 字符集 utf-8
    response.writeHead(200, {'Content-Type': 'text/html; charset=utf-8'});
    //表示给页面上输出一句话，并结束响应
    response.end('Hello World');
}).listen(3000); //端口

```

## 1.2url模块的初步使用

```javascript
const url = require('url');

var api = 'http://www.butou1030.com?name=zhangsan&age=20';

var getValue = url.parse(api, true).query;

console.log(getValue); //{ name: 'zhangsan', age: '20' }

console.log(`姓名：${getValue.name}--年龄：${getValue.age}`);

```

## 1.3http模块与url模块组合创建简单的web服务

```javascript
const http = require('http');
const url = require('url');

/*
	req 获取客户端传过来的信息
	res 给浏览器响应信息
*/

http.createServer((req, res) => {
    // http://www.butou1030.com?name=zhangsan&age=20 想获取url传过来的name和age
    //设置响应头
    //状态码 200, 文件类型 html, 字符集 utf-8
    res.writeHead(200, {'Content-Type': "text/html; charset=utf-8"});
    console.log(req.url); //获取浏览器访问的地址
	if(req.url != '/favicon.ico') {//排除最开始访问的页面图标
        var userinfo = url.parse(req.url, true).query;
        console.log(`姓名：${userinfo.name}--年龄：${userinfo.age}`);
    }
    res.end('你好nodejs'); //结束响应
}).listen(3000);
```

## 1.4模块化创建简单web服务示例

```javascript
// tool.js -- tool模块
function formatApi(api) { //格式化api
    return 'http://www.butou1030.com/' + api;
}
exports.formatApi = formatApi;
```

```javascript
const http = require('http');
const tools = require('./module/tool');
console.log(tools);

http.createServer((req, res) => {
    console.log(req.url); //获取url
    
    res.writeHead(200, {'Content-Type': "text/html; charset=utf-8"});
    res.write('this is nodejs<br>');
    
    var api = tools.formatApi('api/focus');
    res.write(api);
    res.end(); //结束响应
}).listen(3000);
```

## 1.5一些细节

```javascript
// const axios = require('./node_modules/axios/index');

// axios.get();

//在node_modules文件夹下的模块的相对路径可以直接使用相对于node_modules文件夹的路径
// const axios = require('axios/index');

// axios.get();

// axios.post();

//直接使用文件夹的名称可以引入文件夹下对应的index.js模块(默认找名为index.js的文件)
const axios = require('axios');
axios.get();
axios.post();
```

```javascript
//index.js
exports.get = function() {
    console.log('从服务器获取数据');
}
exports.post = function() {
    console.log('提交数据');
}
```

## 2. 第三方模块的使用方法(silly-datetime为例)

```javascript
//1. 安装silly-datetime cnpm i silly-datetime -D
//2. 引入silly-datetime
var sd = require('silly-datetime');
//3. 根据文档进行使用
var d = sd.format(new Date(), 'YYYY-MM-DD HH:mm');
console.log(d);
```

---
