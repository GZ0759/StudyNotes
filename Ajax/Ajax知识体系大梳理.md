[原文](https://juejin.im/post/58c883ecb123db005311861a#heading-1)


# 目录

## 1. 导读

Ajax 全称 Asynchronous JavaScript and XML, 即异步JS与XML. 它最早在IE5中被使用, 然后由Mozilla, Apple, Google推广开来. 典型的代表应用有 Outlook Web Access, 以及 GMail. 现代网页中几乎无ajax不欢. 前后端分离也正是建立在ajax异步通信的基础之上.

## 2. 浏览器为ajax做了什么

现代浏览器中，虽然几乎全部支持 ajax，但它们的技术方案却分为两种：

标准浏览器通过 XMLHttpRequest 对象实现了 ajax 的功能，只需要通过一行代码便可创建一个用于发送 ajax 请求的对象。

```
var xhr = new XMLHttpRequest();
```

IE 浏览器通过 XMLHttpRequest 或者 ActiveXObject 对象同样实现了 ajax 的功能。

IE下的使用环境略显复杂, IE7及更高版本浏览器可以直接使用BOM的 XMLHttpRequest 对象. IE6及更低版本浏览器只能使用 ActiveXObject 对象来创建 XMLHttpRequest 对象实例。

全平台兼容的XMLHttpRequest对象。

```JavaScript
function getXHR(){
  var xhr = null;
  if(window.XMLHttpRequest) {
    xhr = new XMLHttpRequest();
  } else if (window.ActiveXObject) {
    try {
      xhr = new ActiveXObject("Msxml2.XMLHTTP");
    } catch (e) {
      try {
        xhr = new ActiveXObject("Microsoft.XMLHTTP");
      } catch (e) { 
        alert("您的浏览器暂不支持Ajax!");
      }
    }
  }
  return xhr;
}
```

## 5. ajax有没有破坏js单线程机制

浏览器有如下四种线程:

- GUI渲染线程
- javascript引擎线程
- 浏览器事件触发线程
- HTTP请求线程

通常, 它们的线程间交互以事件的方式发生, 通过事件回调的方式予以通知. 而事件回调, 又是以先进先出的方式添加到任务队列的末尾 , 等到js引擎空闲时, 任务队列 中排队的任务将会依次被执行. 这些事件回调包括 setTimeout, setInterval, click, ajax异步请求等回调.

浏览器中, js引擎线程会循环从 任务队列 中读取事件并且执行, 这种运行机制称作 Event Loop (事件循环).

对于一个ajax请求, js引擎首先生成 XMLHttpRequest 实例对象, open过后再调用send方法. 至此, 所有的语句都是同步执行. 但从send方法内部开始, 浏览器为将要发生的网络请求创建了新的http请求线程, 这个线程独立于js引擎线程, 于是网络请求异步被发送出去了. 另一方面, js引擎并不会等待 ajax 发起的http请求收到结果, 而是直接顺序往下执行.

当ajax请求被服务器响应并且收到response后, 浏览器事件触发线程捕获到了ajax的回调事件 onreadystatechange (当然也可能触发onload, 或者 onerror等等) . 该回调事件并没有被立即执行, 而是被添加到 任务队列 的末尾. 直到js引擎空闲了, 任务队列 的任务才被捞出来, 按照添加顺序, 挨个执行, 当然也包括刚刚append到队列末尾的 onreadystatechange 事件.

在 onreadystatechange 事件内部, 有可能对dom进行操作. 此时浏览器便会挂起js引擎线程, 转而执行GUI渲染线程, 进行UI重绘(repaint)或者回流(reflow). 当js引擎重新执行时, GUI渲染线程又会被挂起, GUI更新将被保存起来, 等到js引擎空闲时立即被执行.

以上整个ajax请求过程中, 有涉及到浏览器的4种线程. 其中除了 GUI渲染线程 和 js引擎线程 是互斥的. 其他线程相互之间, 都是可以并行执行的. 通过这样的一种方式, ajax并没有破坏js的单线程机制.

## 6. ajax与setTimeout排队问题

通常, ajax 和 setTimeout 的事件回调都被同等的对待, 按照顺序自动的被添加到 任务队列 的末尾, 等待js引擎空闲时执行. 但请注意, 并非xhr的所有回调执行都滞后于setTImeout的回调. 请看如下代码:
```JavaScript
function ajax(url, method){
  var xhr = getXHR();
  xhr.onreadystatechange = function(){
      console.log('xhr.readyState:' + this.readyState);
  }
  xhr.onloadstart = function(){
      console.log('onloadStart');
  }
  xhr.onload = function(){
      console.log('onload');
  }
  xhr.open(method, url, true);
  xhr.setRequestHeader('Cache-Control',3600);
  xhr.send();
}
var timer = setTimeout(function(){
  console.log('setTimeout');
},0);
ajax('https://user-gold-cdn.xitu.io/2017/3/15/c6eacd7c2f4307f34cd45e93885d1cb6.png','GET');
console.warn('这里的log并不是最先打印出来的.');
//  xhr.readyState:1
//  onloadStart
//  这里的log并不是最先打印出来的.
//  undefined
//  setTimeout
//  xhr.readyState:2
//  xhr.readyState:3
//  xhr.readyState:4
//  onload
```

由于ajax异步, setTimeout回调本应该最先被执行, 然而实际上, 一次ajax请求, 并非所有的部分都是异步的, 至少"readyState==1"的 onreadystatechange 回调以及 onloadstart 回调就是同步执行的. 因此它们的输出排在最前面.

## 7. XMLHttpRequest 属性解读

inherit
readyState
onreadystatechange
目录
导读
浏览器为ajax做了什么
MSXML
全平台兼容的XMLHttpRequest对象
ajax有没有破坏js单线程机制
ajax与setTimeout排队问题
XMLHttpRequest 属性解读
inherit
readyState
onreadystatechange
status
statusText
onloadstart
onprogress
onload
onloadend
timeout
ontimeout
response responseText
responseXML
responseType
responseURL
withCredentials
abort
getResponseHeader
getAllResponseHeaders
setRequestHeader
onerror
upload
overrideMimeType
XHR一级
XHR二级
XDomainRequest
$.ajax
参数列表
支持promise
使用转换器
事件触发顺序
Axios
Fetch
ajax跨域请求
什么是CORS
移动端CORS兼容性
CORS有关的headers
CORS请求
HTML启用CORS
图片启用CORS
ajax文件上传
js文件上传
fetch上传
jquery文件上传
angular文件上传
ajax请求二进制文件
FileReader
ajax请求二进制图片并预览
ajax请求二进制文本并展示
如何等待多个ajax请求完成
ajax与history的兼容
pjax
ajax缓存处理
ajax的错误处理
ajax调试技巧
hosts+nginx+node-webserver
编码问题
后端接口测试技巧
使用命令测试OPTIONS请求
postman
ajax移动端兼容性

status
statusText
onloadstart
onprogress
onload
onloadend
timeout
ontimeout
response responseText
responseXML
responseType
responseURL
withCredentials
abort
getResponseHeader
getAllResponseHeaders
setRequestHeader
onerror
upload
overrideMimeType
XHR一级
XHR二级
XDomainRequest
$.ajax
参数列表
支持promise
使用转换器
事件触发顺序
Axios
Fetch
ajax跨域请求
什么是CORS
移动端CORS兼容性
CORS有关的headers
CORS请求
HTML启用CORS
图片启用CORS
ajax文件上传
js文件上传
fetch上传
jquery文件上传
angular文件上传
ajax请求二进制文件
FileReader
ajax请求二进制图片并预览
ajax请求二进制文本并展示
如何等待多个ajax请求完成
ajax与history的兼容
pjax
ajax缓存处理
ajax的错误处理
ajax调试技巧
hosts+nginx+node-webserver
编码问题
后端接口测试技巧
使用命令测试OPTIONS请求
postman
ajax移动端兼容性
