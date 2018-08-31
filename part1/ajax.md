# 梳理Ajax
**Ajax全称Asychronous JavaScript and xml，主要用来实现客户端与服务器端异步通信效果，实现页面的局部刷新。**

**使用ajax原生方式发送请求主要通过XMLHttpRequest（标准浏览器）、Activeobject（IE浏览器）对象实现异步通信效果**

## 同步和异步的区别

### 同步
同步是阻塞的

浏览器向服务器请求数据，服务器比较忙，浏览器一直等待（白屏），直到服务器返回数据，浏览器才能显示页面

### 异步
异步是非阻塞的

浏览器向服务器请求数据，服务器比较忙，浏览器可以自如干原来的事情，比如显示页面，服务器返回数据的时候通知浏览器，浏览器再把请求到的数据渲染到页面，实现局部刷新。

## 简述Ajax的过程
1. 创建一个XMLHttpRequest对象，即创建一个异步调用对象；

2. 创建一个新的HTTP请求，并指定该HTTP请求的方法、URL以及验证信息；

3. 设置响应HTTP请求状态变化的函数；

4. 发送HTTP请求；

5. 获取异步调用返回的数据；

6. 使用JavaScript和DOM实现局部刷新

## 简述一下异步加载JS
1. 动态插入Script标签

2. 通过Ajax去获取js代码，然后通过eval执行

3. Script标签上添加defer或者async

4. 创建并插入iframe，让它异步执行js

## XMLHTTPRequest对象的常用方法和属性
1. open("method","URL",true)方法：建立对服务器的请求，第一个参数是HTTP请求方法，可以为GET，POST等，第二个参数是请求页面的URL

2. send()方法：发送具体请求

3. abort()方法: 停止当前请求

4. readyState属性：请求的状态：

     5个可取状态值

     0：未初始化，但XMLHTTP实例已经生成，open方法未调用
     
     1：正在加载，open方法调用，sent方法未调用，没有发送请求
     
     2: 加载完成，调用了sent方法，服务器收到了请求信息
     
     3: 交互中，服务器返回数据，浏览器接收数据
     
     4: 完成
     
5. responseText属性：服务器响应，表示为一个字符串

6. responseXML属性：服雾器响应，表示为XML
## 封装一个Ajax

```
function ajax(url,fnSucc,fnFail){
    if(window.XMLHTTPRequest){
        var aAjax = new XMLHTTPRequest();
    }
    else{
        var oAjax = new ActiveXObject("Microsoft.XMLHTTP");
    }
oAjax.open('GET',url,true);
oAjax.send();
oAjax.onreadystatechange = function(){
    if(oAjax.readystatechange == 4){
        if(oAjax.status ==200){
            fnSucc(oAjax.responseText);
        }
        else{
            if(fnFaild){
                fnFaild(oAjax.status);
            }
        }
    }
}
}
```
