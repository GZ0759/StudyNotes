[原文](https://juejin.im/post/58c883ecb123db005311861a)


# 目录

## 1. 导读

Ajax 全称 Asynchronous JavaScript and XML, 即异步JS与XML. 它最早在IE5中被使用, 然后由Mozilla, Apple, Google推广开来. 典型的代表应用有 Outlook Web Access, 以及 GMail. 现代网页中几乎无ajax不欢. 前后端分离也正是建立在ajax异步通信的基础之上.

## 2. 浏览器为ajax做了什么

现代浏览器中，虽然几乎全部支持 ajax，但它们的技术方案却分为两种：

标准浏览器通过 XMLHttpRequest 对象实现了 ajax 的功能，只需要通过一行代码便可创建一个用于发送 ajax 请求的对象。

```JavaScript
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

XMLHttpRequest 实例对象没有自有属性. 实际上, 它的所有属性均来自于 XMLHttpRequest.prototype 。通常, 一个 xhr 实例对象拥有10个普通属性+9个方法。

readyState。只读属性，该属性记录了 ajax 调用过程中所有可能的状态。

| readyState | 对应常量 | 描述 |
| ----- | ----- | ----- |
| 0 (未初始化) | xhr.UNSENT | 请求已建立, 但未初始化(此时未调用open方法)
| 1 (初始化) | xhr.OPENED | 请求已建立, 但未发送 (已调用open方法, 但未调用send方法)
| 2 (发送数据) | xhr.HEADERS_RECEIVED | 请求已发送 (send方法已调用, 已收到响应头)
| 3 (数据传送中) | xhr.LOADING | 请求处理中, 因响应内容不全, 这时通过responseBody和responseText获取可能会出现错误
| 4 (完成) | xhr.DONE | 数据接收完毕, 此时可以通过通过responseBody和responseText获取完整的响应数据

onreadystatechange。该事件回调方法在 readystate 状态改变时触发，在一个收到响应的 ajax 请求周期中，onreadystatechange 方法会被触发4次，因此可以在 onreadytstatechange 方法中绑定一些事件回调。

```JavaScript
xhr.onreadystatechange = function(e){
  if(xhr.readystate==4){
    var s = xhr.status;
    if((s >= 200 && s < 300) || s == 304){
      var resp = xhr.responseText;
      //TODO ...
    }
  }
}
```

status。只读属性，status 表示 http 请求的状态，初始值为0，如果服务器没有显式地指定状态码，那么 status 将被设置为默认值，即200。

statusText。只读属性，statusText 表示服务器的响应状态信息，它是一个 UTF-16 的字符串，请求成功且 status==20X 时，返回大写的 OK，请求失败时返回空字符串，其他情况下返回相应的状态描述。比如: 301的 Moved Permanently , 302的 Found , 303的 See Other , 307 的 Temporary Redirect , 400的 Bad Request , 401的 Unauthorized 等等。

onloadstart。事件回调方法在ajax请求发送之前触发, 触发时机在 readyState==1 状态之后, readyState==2 状态之前。onloadstart方法中默认将传入一个ProgressEvent事件进度对象。ProgressEvent对象具有三个重要的Read only属性.
- lengthComputable 表示长度是否可计算, 它是一个布尔值, 初始值为false.
- loaded 表示已加载资源的大小, 如果使用http下载资源, 它仅仅表示已下载内容的大小, 而不包括http headers等. 它是一个无符号长整型, 初始值为0.
- total 表示资源总大小, 如果使用http下载资源, 它仅仅表示内容的总大小, 而不包括http headers等, 它同样是一个无符号长整型, 初始值为0.

onprogress。事件回调方法在 readyState==3 状态时开始触发, 默认传入 ProgressEvent 对象, 可通过 e.loaded/e.total 来计算加载资源的进度, 该方法用于获取资源的下载进度。

onload。事件回调方法在ajax请求成功后触发, 触发时机在 readyState==4 状态之后.
想要捕捉到一个ajax异步请求的成功状态, 并且执行回调, 一般下面的语句就足够了:
```JavaScript
xhr.onload = function(){
  var s = xhr.status;
  if((s >= 200 && s < 300) || s == 304){
    var resp = xhr.responseText;
    //TODO ...
  }
}
```

onloadend。事件回调方法在ajax请求完成后触发, 触发时机在 readyState==4 状态之后(收到响应时) 或者 readyState==2 状态之后(未收到响应时).onloadend方法中默认将传入一个ProgressEvent事件进度对象。

timeout。timeout属性用于指定ajax的超时时长. 通过它可以灵活地控制ajax请求时间的上限. timeout的值满足如下规则:
- 通常设置为0时不生效.
- 设置为字符串时, 如果字符串中全部为数字, 它会自动将字符串转化为数字, 反之该设置不生效.
- 设置为对象时, 如果该对象能够转化为数字, 那么将设置为转化后的数字.

ontimeout。方法在ajax请求超时时触发, 通过它可以在ajax请求超时时做一些后续处理。

response responseText。均为只读属性, response表示服务器的响应内容, 相应的, responseText表示服务器响应内容的文本形式

responseXML。只读属性, responseXML表示xml形式的响应数据, 缺省为null, 若数据不是有效的xml, 则会报错。

responseType。responseType表示响应的类型, 缺省为空字符串, 可取 "arraybuffer" , "blob" , "document" , "json" , and "text" 共五种类型。

responseURL。responseURL返回ajax请求最终的URL, 如果请求中存在重定向, 那么responseURL表示重定向之后的URL。

withCredentials。withCredentials是一个布尔值, 默认为false, 表示跨域请求中不发送cookies等信息. 当它设置为true时, cookies , authorization headers 或者TLS客户端证书 都可以正常发送和接收. 显然它的值对同域请求没有影响.

abort。abort方法用于取消ajax请求, 取消后, readyState 状态将被设置为 0 (UNSENT). 如下, 调用abort 方法后, 请求将被取消。

getResponseHeader。getResponseHeader方法用于获取ajax响应头中指定name的值. 如果response headers中存在相同的name, 那么它们的值将自动以字符串的形式连接在一起。

getAllResponseHeaders。getAllResponseHeaders方法用于获取所有安全的ajax响应头, 响应头以字符串形式返回. 每个HTTP报头名称和值用冒号分隔, 如key:value, 并以\r\n结束。

setRequestHeader。既然可以获取响应头, 那么自然也可以设置请求头, setRequestHeader就是干这个的。

onerror。方法用于在ajax请求出错后执行. 通常只在网络出现问题时或者ERR_CONNECTION_RESET时触发(如果请求返回的是407状态码, chrome下也会触发onerror)。

upload。属性默认返回一个 XMLHttpRequestUpload 对象, 用于上传资源. 该对象具有如下方法:

- onloadstart
- onprogress
- onabort
- onerror
- onload
- ontimeout
- onloadend

上述方法功能同 xhr 对象中同名方法一致. 其中, onprogress 事件回调方法可用于跟踪资源上传的进度。


overrideMimeType。方法用于强制指定response 的 MIME 类型, 即强制修改response的 Content-Type。

## XHR一级

XHR1 即 XMLHttpRequest Level 1. XHR1时, xhr对象具有如下缺点:

- 仅支持文本数据传输, 无法传输二进制数据.
- 传输数据时, 没有进度信息提示, 只能提示是否完成.
- 受浏览器 同源策略 限制, 只能请求同域资源.
- 没有超时机制, 不方便掌控ajax请求节奏.

## XHR二级

XHR2 即 XMLHttpRequest Level 2. XHR2针对XHR1的上述缺点做了如下改进:

- 支持二进制数据, 可以上传文件, 可以使用FormData对象管理表单.
- 提供进度提示, 可通过 xhr.upload.onprogress 事件回调方法获取传输进度.
- 依然受 同源策略 限制, 这个安全机制不会变. XHR2新提供 Access-Control-Allow-Origin 等headers, 设置为 * 时表示允许任何域名请求, 从而实现跨域CORS访问(有关CORS详细介绍请耐心往下读).
- 可以设置timeout 及 ontimeout, 方便设置超时时长和超时后续处理.

目前, 主流浏览器基本上都支持XHR2, 除了IE系列需要IE10及更高版本. 因此IE10以下是不支持XHR2的。

## XDomainRequest

对象是IE8,9折腾出来的, 用于支持CORS请求非成熟的解决方案. 以至于IE10中直接移除了它, 并重新回到了 XMLHttpRequest 的怀抱。XDomainRequest 仅可用于发送 GET和 POST 请求。

## $.ajax

$.ajax是jquery对原生ajax的一次封装. 通过封装ajax, jquery抹平了不同版本浏览器异步http的差异性, 取而代之的是高度统一的api. jquery作为js类库时代的先驱, 对前端发展有着深远的影响. 了解并熟悉其ajax方法, 不可谓不重要。

## Axios

实际上, 如果你仅仅只是想要一个不错的http库, 相比于庞大臃肿的jquery, 短小精悍的Axios可能更加适合你. 原因如下:

- Axios支持node, jquery并不支持.
- Axios基于promise语法, jq3.0才开始全面支持.
- Axios短小精悍, 更加适合http场景, jquery大而全, 加载较慢.

## Fetch

Fetch 是 web异步通信的未来. 从chrome42, Firefox39, Opera29, EdgeHTML14(并非Edge版本)起, fetch就已经被支持了. 其中chrome42~45版本, fetch对中文支持有问题, 建议从chrome46起使用fetch。

## ajax跨域请求
什么是CORS
移动端CORS兼容性
CORS有关的headers
CORS请求
HTML启用CORS
图片启用CORS
## ajax文件上传
js文件上传
fetch上传
jquery文件上传
angular文件上传
## ajax请求二进制文件
FileReader
ajax请求二进制图片并预览
ajax请求二进制文本并展示
## 如何等待多个ajax请求完成
## ajax与history的兼容
pjax
## ajax缓存处理
## ajax的错误处理
## ajax调试技巧
hosts+nginx+node-webserver
编码问题
## 后端接口测试技巧
使用命令测试OPTIONS请求
postman
## ajax移动端兼容性
