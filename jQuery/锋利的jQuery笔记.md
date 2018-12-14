# 第六章 jQuery与AJAX的应用

Ajax 全称为“Asynchronous JavaScript and XML”（异步JavaScript和XML），它并不是指一种单一的技术，而是有机地利用了一系列交互式网页应用相关的技术所形成的结合体。

## 6.1 Ajax的优势和不足

Ajax 不需要插件支持，有优秀的用户体验，提高Web程序的性能，减轻服务器和带宽的负担。

浏览器对 XMLHttpRequest 对象的支持度不足，破坏浏览器前进、“后退”按钮的正常功能，对搜索引擎的支持不足，开发和调试工具的缺乏。

## 6.2 Ajax的XMLHttpRequest对象

Ajax 的核心是 XMLHttpRequest 对象，它是 Ajax 实现的关键——发送异步请求、接收相应以及执行回调都是通过它来完成的。

## 6.3 安装Web环境——AppServ

## 6.4 编写第一个Ajax例子

通过创建的 JavaScript 的 Ajax 的方式从服务器端取回一个“Hello Ajax！”的字符串并显示在页面上。

1. 定义一个函数，通过该函数来异步获取信息
2. 声明一个空对象用来装入 XMLHttpRequest 对象
3. 给 XMLHttpRequest 对象赋值
4. 实例化成功后，使用 open() 方法初始化 XMLHttpRequest 对象，指定 HTTP 方法和要使用的服务器 URL。默认情况下，使用 XMLHttpRequest 对象发送的 HTTP 请求是异步进行的，但是可以显示地把 async 参数设置为 true
5. 注册一个 XMLHttpRequest 对象将调用的回调事件处理器当它的 readyState 指改变时调用。
6. 使用 send() 方法发送该请求。因为这个请求使用的是 HTTP 的 GET 方式，所以可以在不指定参数或使用 null 参数的情况下调用 send() 方法。

```javascript
function Ajax(){ 
	var xmlHttpReq = null;	//声明一个空对象用来装入XMLHttpRequest
	if (window.ActiveXObject){//IE5 IE6是以ActiveXObject的方式引入XMLHttpRequest的
		xmlHttpReq = new ActiveXObject("Microsoft.XMLHTTP");
	} 
	else if (window.XMLHttpRequest){//除IE5 IE6 以外的浏览器XMLHttpRequest是window的子对象
		xmlHttpReq = new XMLHttpRequest();//实例化一个XMLHttpRequest
	}
	if(xmlHttpReq != null){	//如果对象实例化成功 
		xmlHttpReq.open("GET","test.php",true);	//调用open()方法并采用异步方式
		xmlHttpReq.onreadystatechange=RequestCallBack; //设置回调函数
		xmlHttpReq.send(null);	//因为使用get方式提交，所以可以使用null参调用
	}
	function RequestCallBack(){//一旦readyState值改变，将会调用这个函数
		if(xmlHttpReq.readyState == 4){
				if(xmlHttpReq.status == 200){
					//将xmlHttpReq.responseText的值赋给ID为 resText 的元素
					document.getElementById("resText").innerHTML = xmlHttpReq.responseText;
				}
		}
	}
}
```



## 6.5 jQuery中的Ajax

jQuery 对 Ajax 操作进行了封装，在 jQuery 中 `$.ajax()` 方法术语最底层的方法，第2层是 `load()`、`$.get()`和`$.post()`方法，第三层是`$.getScript()`和`$.getJSON()`方法。

load() 方法。load() 方法使 jQuery 中最为简单和常用的 Ajax 方法，能载入远程 HTML 代码并插入 DOM 中。它的结构如下，url 是请求 HTML 页面的 URL 地址，data 是发送至服务器的 key/value 数据，是一个对象，callback 是请求完成时的回调函数，无论请求成功或失败。后两个是可选参数。

```
.load( url [, data ] [, complete ] )
```



通过为 URL 参数指定选择符，就可以很方便地从加载过来的 HTML 文档里筛选出所需要的内容。

load() 方法的传递方式根据参数 data 来自动指定。如果没有参数传递，则采用 GET 方式传递；反之，则会自动转换为 POST 方式。

对于必须在加载完成后才能继续的操作，load() 方法提供了回调函数，该函数有3个参数，分别代表请求返回的内容、请求状态和 XMLHttpRequest 对象。其中请求状态 textStatus 主要有 success、error、notmodified、timeout 四种。

如果需要传递一些参数给服务器中的页面，那么可以使用`$.get()`或者`$.post()`方法。

`$.get()`方法使用 GET 方式来进行异步请求，其中 url 是请求的 HTML 页的 URL 地址，data 是发送至服务器的 key/value 数据会作为 QueryString 附加到请求的 URL 中，callback 是载入成功时回调函数，只有当Response 的返回状态是 success 才调用该方法，回调函数自动将请求结果和状态传递给该方法，type 是服务器返回内容的格式，包括 xml、html、script、json、text 和 _default。

```
jQuery.get( url [, data ] [, callback ] [, type ] )
```



服务器返回的数据格式可以有多种，如果是 HTML 片段，不需要经过处理就可以将新的 HTML 数据插入到主页面中。如果是 XML 文档，需要对返回的数据进行处理，可以使用常规的 attr()、find()、filter() 以及其他方法，这种文档的可移植性是其他数据格式无法比拟的。而 JSON 文件和 XML 文档一样，也可以方便的被重用，而且 JSON 文件非常简洁，也容易阅读。

$.post() 方法的结构和使用方式都相同，不过它们之间仍然有以下区别。

- GET请求会将参数跟在URL后进行传递，而POST请求则是作为HTTP消息的实体内容发送个Web服务器，当然，在Ajax中，这种区别对用户是不可见的。
- GET方式对传输的数据有大小限制（通常不能大于2KB），而使用POST方式传递的数据量要比GET方式大得多（理论上不受限制，但是可以在服务端进行限制）。
- GET方式请求的数据会被浏览器缓存起来，因此其他人就可以从浏览器的历史记录中读取这些数据，例如账号和密码等。在某种情况下，GET方式会带来严重的安全性问题，而POST方式相对来说就可以避免这些问题。（但是也是不安全的，所以密码之类的还是要加密的）
- GET方式和POST方式传递的数据在服务器的获取方式也不相同。在PHP中，GET方式数据可以用`$_GET[]`获取，而POST可以用`$_POST[]`获取、两种方式都可以用`$_REQUEST[]`来获取。 

`$.getScript()`方法用来直接加载 .js 文件，与加载一个 THML 片段一样简单方便，并且不需要对JavaScript文件进行吹，JavaScript 文件会自动执行。与其他 Ajax 方法一样，这个方法也有回调函数，它会在 JavaScript 文件成功载入后运行。

`$.getJSON()`方法用于加载 JSON 文件，与`$.getScript()`方法的用法一样。可以在函数中通过 data 变量来遍历相应的数据，也可以使用迭代方法为每个项构建相应的 HTML 代码。jQuery 提供了一个通用的遍历方法`$.each()`，用于遍历对象和数组，这个函数不同于 jQuery 对象的 each() 方法，它是一个全局函数，不操作 jQuery 对象，而是以一个数组或者对象作为第1个参数，以一个回调函数作为第2个参数。

`$.ajax()`方法是 jQuery 最底层的 Ajax 实现。该方法只有1个参数，但在这个对象里包含了`$.ajax()`方法所需要的请求设置以及回调函数等信息，参数以 key/value 的形式存在，所有参数都是可选的。其中包括 url、type、timeout、data、dataType、beforeSend、complete、success、error、global。前面那些方法都是基于`$.ajax()`方法构建的。

## 6.6 序列化元素

常规的表单提交方法使使表单提交到另一个页面，整个浏览器都会被刷新，而使用 Ajax 技术能够异步提交表单，并将服务区返回的数据显示在当前页面中。

serialize() 方法也是作用于一个 jQuery 对象 ，它能够将 DOM 元素内容序列化为字符串，用于 Ajax 请求。需要注意的是，`$.get()`方法中 data 参数不仅可以使用映射方式，也可以使用字符串方式。用字符串方式时，需要注意对字符编码（中问问题），如果不希望编码带来麻烦，可以使用 serialize() 方法，它会自动编码。

serializeArray() 方法不是返回字符串，而是将 DOM 元素序列化后，返回 JSON 格式的数据。既然是一个对象，那么就可以使用`$.each()`函数对数据进行迭代输出。

```javascript
$(function(){
		 var fields = $(":checkbox,:radio").serializeArray();
		 console.log(fields);// Firebug输出
		 $.each( fields, function(i, field){
		    $("#results").append(field.value + " , ");
		}); 
   })
```



`$.param()`方法用来对一个数组或对象按照 key/value 进行序列化，比如将一个普通的对象序列化。

```javascript
var obj = {a:1, b:2,c:3};
var k = $.param(obj);
alert(k);  // 输出a=1&b=2&c=3
```



## 6.7 jQuery中的 Ajax 全局事件

jQuery 简化 Ajax 操作不仅体现在调用 Ajax 方法和处理相应方面，而且还体现在对调用 Ajax 方法的过程中的 HTTP 请求的控制。通过 jQuery 提供了一些自定义全局函数，能够与各种与 Ajax 相关的事件注册回调函数。例如当 Ajax 请求开始时，会触发 ajaxStart() 方法的回调函数；当 Ajax 请求结束时，会触发 ajaxStop() 方法的回调函数。这些方法都是全局的方法，因此无论创建它们的代码位于何处，只要有 Ajax 请求发生时，就会触发它们。

- ajaxStart：ajax请求开始前
- ajaxSend：ajax请求时
- ajaxSuccess：ajax获取数据后
- ajaxComplete：ajax请求完成时
- ajaxError：ajax请求发生错误后
- ajaxStop：ajax请求停止后

如果想使某个 Ajax 请求不受全局方法的影响，那么可以在使用`$.ajax(options)`方法时，将参数中的 global 设置为 false。

## 6.8 基于 jQuery 的Ajax 聊天室程序

设计数据库。首先构建一个聊天信息表，有4个字段，即消息编号（id），姓名（user），内容（msg）以及一个数字事件戳（timestamp）。

服务器端处理。服务器端主要用来处理用户提交的信息以及输出返回。

- 首先需要在服务器端链接数据库。
- 其次如果有用户提交新信息，则把信息插入数据库，同时删除旧的的数据信息（保持数据库中只有10条信息）。
- 最后从数据库中获取新的信息并以 XML 格式输出返回。

客户端处理。客户端需要做两项工作。

- 首先提交用户聊天信息，然后处理服务器端返回的聊天信息，将信息实时呈现出来。
- 每隔一定时间发起查询数据库中聊天记录的请求，然后处理服务器端返回的聊天信息，将信息实时呈现出来。

客户端代码。

设置当前消息的时间戳为0，并且调用函数来加载数据库已有的聊天信息。

```javascript
timestamp = 0;   
updateMsg();
```

表单提交的代码。在 submit 事件函数中，可以使用 jQuery 的`$.post()`方法来发送一个 POST 请求，把要传递的数据都放入第2个参数中，用 {} 包裹。

```javascript
$("#chatform").submit(function(){
    $.post("backend.php",{
        message: $("#msd").val(),
        name: $("#author").val(),
        action: "postmsg",
        time: timestamp
    },function(xml){
        $("#msg").val("");
        addMessages(xml)
    });
    return false;  // 阻止表单提交
})
```

 

再看 addMessage() 函数，它是用来处理 XML 相应信息的。

```javascript
function addMessages(xml) {   
  if($("status",xml).text() == "2") return;   
  timestamp = $("time",xml).text();   
  $("message",xml).each(function(id) {   
    message = $("message",xml).get(id);   
    $("#messagewindow").prepend("<b>"+$("author",message).text()+   
              "</b>: "+$("text",message).text()+   
              "<br />");   
  });   
}
```



updateMsg() 函数的功能是到服务器查询新信息，并且调用 addMessage() 函数来响应返回的 XML 文档，同时需要设置一个间隔时间，让聊天窗口自动更新。

```javascript
 function updateMsg() {   
      $.post("backend.php",{ time: timestamp }, function(xml) {   
        $("#loading").remove();   
        addMessages(xml);   
      });   
      setTimeout('updateMsg()', 4000);   
    }   
```





