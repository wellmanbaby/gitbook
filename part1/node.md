# node.js
## 用node.js写一个简单的服务器

```
//获取node提供的http模块，不会再改这个变量，采用cosnt定义来代替var
const http = require('http');
//调用http模块的createServer方法，创建一台服务器
http.createServer(function(request,response){
   console.log('someone is coming');
   console.log(request.url);
   switch(request.url){
       case '/1.html'
         response.write("1111");
         break;
       case '/2.html'
         response.write("2222");
         break;
       default:
         response.write('404');
         break;
   }
   response.end();
});

//监听--等待访问
//端口--服务器门牌号
server.listen(8080);
```
## 处理简单服务器的遗留问题

首先是这么写比较麻烦，要是有多个页面的话，那得多少个case呀，显然是不合理的。

另外是一旦修改了response的内容，服务器就得重启，显然是更加不合理的。

### 读文件
```
const fs = require('fs');

//readFile(文件名，回调函数)
fs.readFile('aaa.txt',function(err,data){
  if(err){
      console.log('读取失败')；
  }else{
      console.log(data.toString());
  }
})
```
### 写文件

```
const fs = require('fs');

//writeFile(文件名，内容，回调)
fs.writeFile("bbb.txt","ssssdsds",function(err){
    console.log(err);
})
```
### 利用磁盘写出比较合理的server

server.js
```
const http = require('http');
const fs = require('fs');

var server = http.createServer(function(req,res){
    //req.url => '/index.html'
    //读取 => './www/index.html'
    // './www'+req.url
    var file_name = './www'+req.url;

    fs.readFile(file_name,function(err,data){
        if(err){
            res.write('404');
        }else{
            res.write(data);
        }
        res.end();
    });
});
server.listen(8080);
```
把内容文件写在磁盘中，不用每次刷新服务器

### form表单提交到server的例子(GET数据解析)

**server2.js**
```
const http = require('http');

http.createServer(function(req,res){
    var GET = {};
    if(req.url.indexOf('?')!=-1){
        var arr = req.url.split('?');
        //arr[0] => 地址 '/aaa'
        var url = arr[0];
        //arr[1] => 数据 'user = blue&pass = 123456'
        var arr2 = arr[1].split('&');
        //arr2 =>['user=blue','pass=123456']
    
        for(var i=0;i<arr2.length;i++){
            var arr3 = arr2[i].split('=');
            //arr3[0] => 名字 'user'
            //arr3[1] => 数据 'blue'
            GET[arr3[0]] = arr3[1];
        }
    }else{
        var url = req.url;
    }
    
    console.log(url,GET);
    //console.log(req.url);
    //req获取前台请求的数据
    res.write('aaaa');
    res.end();
}).listen(8080);
```
form.html

```
    <form action="http://localhost:8080/aaa" method="GET">
        用户：<input type="text" name="user" value=""> <br> 
        密码：<input type="password" name="pass" value=""><br>
        <input type="submit" value="提交">
    </form>
```
### 利用querystring代替正则部分

server3.js

```
const http = require('http');
const querystring = require('querystring');

http.createServer(function(req,res){
    var GET = {};
    if(req.url.indexOf('?')!=-1){
        var arr = req.url.split('?');
        //arr[0] => 地址 '/aaa'
        var url = arr[0];
        GET = querystring.parse(arr[1]);
    }else{
        var url = req.url;
    }
    
    console.log(url,GET);
    //console.log(req.url);
    //req获取前台请求的数据
    res.write('aaaa');
    res.end();
}).listen(8080);
```
### 利用url模块更加简便的实现GET数据解析

```
const http = require('http');
const urlLib = require('url');

http.createServer(function(req,res){
    
    var obj = urlLib.parse(req.url,true);

    var url = obj.pathname;
    var GET = obj.query;
    console.log(url,GET);
    //console.log(req.url);
    //req获取前台请求的数据
    res.write('aaaa');
    res.end();
}).listen(8080);
```
### 总结GET数据解析

1. 自己解析，麻烦

2. querystring, 已经相当简化

3. url， urlLib.parse(url,true):地址：pathname,内容：query

### Post数据解析
POST太大，所以是分段发送的

```
var http = require('http');
var querystring = require('querystring');

http.createServer(function(req,res){
    //POST-req

    var str = '';//接收数据
    //data-有一段数据到达（很多次）
    var i = 0;
    req.on('data',function(data){
        console.log(`第${i++}次收到数据`);
          str+=data;
    });
    //end-数据全部到达（一次）
    req.on('end',function(){
        var POST = querystring.parse(str);
        console.log(POST);
    });
}).listen(8080);
```
结合POST和GET的server

```
const http = require('http');
const fs = require('fs');
const querystring = require('querystring');
const urlLib = require('url');

var server = http.createServer(function (req, res) {
    //GET
    var obj = urlLib.parse(req.url, true);
    var url = obj.pathname;
    const GET = obj.query;


    //POST
    var str = '';
    req.on('data', function (data) {
        str += data;
    });
    req.on('end', function () {
        const POST = querystring.parse(str);
        console.log(url,GET,POST);
    })
});
server.listen(8080);
```