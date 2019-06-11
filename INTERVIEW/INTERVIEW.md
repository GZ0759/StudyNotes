<!-- TOC -->

- [一、YN](#一yn)
  - [**link 和@import 的区别。**](#link和import的区别)
  - [**HTML5 有哪些新特性，移除了哪些元素？如何处理 HTML5 新标签的浏览器兼容问题？如何区分 HTML 和 HTML5?**](#html5有哪些新特性移除了哪些元素如何处理html5新标签的浏览器兼容问题如何区分html和html5)
  - [**position 为 relative 和为 absolute 的相对定位元素。**](#position为relative和为absolute的相对定位元素)
  - [**离线存储的方式和原理。**](#离线存储的方式和原理)
  - [**创建 Ajax 的步骤。**](#创建ajax的步骤)
  - [**GET 请求和 POST 请求。**](#get请求和post请求)
  - [**angular 和 react 使用的 TypeScript 语法**](#angular和react使用的typescript语法)

<!-- /TOC -->

# 一、YN

## **link 和@import 的区别。**

从属关系区别。@import 是 CSS 提供的语法规则，只有导入样式表的作用；link 是 HTML 提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。

加载顺序区别。加载页面时，link 标签引入的 CSS 被同时加载；@import 引入的 CSS 将在页面加载完毕后被加载。

兼容性区别。@import 是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；link 标签作为 HTML 元素，不存在兼容性问题。

DOM 可控性区别。可以通过 JS 操作 DOM ，插入 link 标签来改变样式；由于 DOM 方法是基于文档的，无法使用@import 的方式插入样式。

权重区别。link 引入的样式权重大于@import 引入的样式。

## **HTML5 有哪些新特性，移除了哪些元素？如何处理 HTML5 新标签的浏览器兼容问题？如何区分 HTML 和 HTML5?**

语义化标签、增强型表单、视频和音频标准、Canvas 绘图、拖放 API、Web Worker、Web Storage、WebSocket。

移除的元素有纯表现的元素（basefont,big,center,font,s,strike,tt,u）、对可用性产生负面影响的元素（frame,frameset,noframes）

IE8/IE7/IE6 支持通过 document.createElement 方法产生的标签， 可以利用这一特性让这些浏览器支持 HTML5 新标签， 浏览器支持新标签后，还需要添加标签默认的样式。 当然也可以直接使用成熟的框架、比如 html5shim;

```html
<!--[if lt IE 9]>
  <script>
    src = "http://html5shim.googlecode.com/svn/trunk/html5.js";
  </script>
<![endif]-->
```

HTML5 文档类型声明：<!doctype html>。DOCTYPE 声明的方式是区分 HTML 和 HTML5 标志的一个重要因素，此外，还可以根据新增的结构、功能元素来加以区分。

## **position 为 relative 和为 absolute 的相对定位元素。**

对于其他元素，如果该元素的 position 是 relative 或者 static，则“包含块” 由其最近的块容器祖先盒的 content box 边界形成。

如果元素 position:fixed，则“包含块”是“初始包含块”。根元素（很多场景下可以看成是<html>）被称为“初始包含块”，其尺寸等同于浏览器可视窗口的大小。

如果元素 position:absolute，则“包含块”由最近的 position 不为 static 的祖先元素建立。

## **离线存储的方式和原理。**

HTML5 提供了两种在客户端存储数据的新方法：

- localStorage - 没有时间限制的数据存储。
- sessionStorage - 针对一个 session 的数据存储。

## **创建 Ajax 的步骤。**

step1. 创建 XMLHttpRequest 对象，也就是创建一个异步调用对象；

step2. 创建一个新的 HTTP 请求，并指定改 HTTP 请求的方法、URL 以及验证信息；

step3. 设置响应 HTTP 状态变化的函数；

step4. 发送 HTTP 请求；

step5. 获取异步调用返回的数据；

step6. 使用 javascript 和 DOM 实现局部刷新；

```javascript
<script type="text/javascript">
    window.onload = function(){
        //第一步：创建xhr对象
        //xhr是一个对象；里面可以放很多东西，数据；
        var xhr = null;
        if(window.XMLHttpRequest){//标准浏览器
            xhr = new XMLHttpRequest();//创建一个对象
        }else{//早期的IE浏览器
            xhr = new ActiveXObject('Microsoft.XMLHTTP');//参数是规定的；
        }
        console.log("状态q"+xhr.readyState);//0
        //第二步：准备发送请求-配置发送请求的一些行为
        //open即打开链接，第一个参数是以什么方式；第二个是往哪儿发送请求，第三个可以不写，默认true,表示异步，false表示同步；；
        xhr.open('get','03form.php',true);
        console.log("状态w"+xhr.readyState);//1

        //第三步：执行发送的动作
        //send也可以写在前面，推荐写在后面；写null是兼容问题；
        xhr.send(null);
        console.log("状态e"+xhr.readyState);//1

        //第四步：指定一些回调函数，也属于事件函数；不触发不执行，触发条件是xhr.readyState;z这个值有0-4，共5个状态，是由浏览器控制的；
        xhr.onreadystatechange = function(){
            if(xhr.readyState == 4){//4指服务器返回的数据可以使用；
                if(xhr.status == 200){ //判断已经成功的获取了数据；200表示hTTP请求成功；404表示找不到页面；503表示服务器端有语法错误；
                    var data = xhr.responseText;//json，文本，主角；
                    // var data1 = xhr.responseXML;
                }
            }
            // console.log("状态t"+xhr.readyState);//2表示已经发送完成；

            // console.log(1234);
        }

        // console.log(456);
        console.log("状态r"+xhr.readyState);//1


    }
    </script>
```

## **GET 请求和 POST 请求。**

（1）使用 Get 请求时,参数在 URL 中显示,而使用 Post 请求,则不会显示出来；

（2）Post 传输的数据量大，可以达到 2M，而 Get 方法由于受到 URL 长度的限制,只能传递大约 1024 字节.

（3）Get 请求请求需注意缓存问题,Post 请求不需担心这个问题；

（4）Post 请求必须设置 Content-Type 值为 application/x-form-www-urlencoded；

（5）发送请求时,因为 Get 请求的参数都在 url 里,所以 send 函数发送的参数为 null,而 Post 请求在使用 send 方法时,却需赋予其参数；

（6）GET 方式请求的数据会被浏览器缓存起来，因此其他人就可以从浏览器的历史记录中读取到这些数据，例如账号和密码等。在某种情况下，GET 方式会带来严重的安全问题。而 POST 方式相对来说就可以避免这些问题。

## **angular 和 react 使用的 TypeScript 语法**

简单笼统地说，TypeScript 是 JavaScript 的超集，是微软开发的一种脚本语言。和 JavaScript 一样，是现在项目开发中热门的脚本语言。

TypeScript 是一种强类型语言，可编译成 JavaScript，包含了 JavaScript 的所有元素，可以载入 JavaScript 代码运行，扩展了 JavaScript 的语法。相比 JavaScript，TypeScript 是真面向对象，增加了静态类型，类，模块，接口和类型注解。

TypeScript 的编译器很智能，会进行冲突检测，举个例子，一个 enum 的数据，你初始化一个数据，再用一个 switch 语句，编译器会判定其他选项为无效的，会编译错误，直接指出错误原因，这在 JavaScript 是不会指出错误的。

# 二、IN

## Vue 工作原理

数据响应原理。

当把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的属性，并使用 Object.defineProperty 把这些属性全部转为 getter/setter。Object.defineProperty 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

这些 getter/setter 对用户来说是不可见的，但是在内部它们让 Vue 能够追踪依赖，在属性被访问和修改时通知变更。

每个组件实例都对应一个 watcher 实例，它会在组件渲染的过程中把“接触”过的数据属性记录为依赖。之后当依赖项的 setter 触发时，会通知 watcher，从而使它关联的组件重新渲染。

Virtual Dom。

为什么使用virtual-dom？因为直接频繁地操作dom会有很高的性能消耗。

虚拟dom，使用JS对象模拟dom进行操作。Vnode 是虚拟 DOM 节点类，其实例 vnode 是一个包含着渲染 DOM 节点所需要的一切信息的普通对象。render() 方法根据当前 vm 的数据生成 vnode。

简单来说，新老vnode基本属性相同时，进行diff（过程较复杂）；新老vnode基本属性不同时，删除老的dom，新建新的真实dom。

更新真实dom流程与diff过程交叉，利用了源码中重要的patch函数，生成真实dom更新视图。

## Web 客户端

主流浏览器的内核。IE浏览器是Trident，Mozilla浏览器是Gecko，Safari浏览器是Webkit，Chrome浏览器是Blink，Opera浏览器现在也是Blink。

同源策略是对 XHR 的一个主要约束，它为通信设置了“相同的域、相同的端口、相同的协议”这一限制。试图访问上述限制之外的资源，都会引发安全错误，除非采用被认可的跨域解决方案。这个解决方案叫做 CORS（ Cross-Origin Resource Sharing，跨源资源共享）， IE8 通过 XDomainRequest 对象支持CORS，其他浏览器通过 XHR 对象原生支持 CORS。图像 Ping 和 JSONP 是另外两种跨域通信的技术，但不如 CORS 稳妥。

## HTML5 新特性

- 语义化标签（header、section、article、aside、nav、footer）
- 增强型表单：新增属性（例如require、placeholder）、新增元素（datalist、output）
- Canvas画布，getContext() 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。
- 多媒体相关API。音频（audio）和视频（video）。
- History API。通过脚本管理浏览器的历史记录。
- 本地储存。sessionStorage和localStorage。
- 离线应用程序。cache manifest 文件
- 文件API。FileReader API。
- 通信API。跨文档消息传输功能、使用WebSockets API来通过 socket 端口传递数据的功能和通过 Server-Sent Eventsource API将服务器端事件主动推动到客户端的功能。
- Web Workers处理线程。web worker 是运行在后台的 JavaScript，不会影响页面的性能。
- 获取地理位置信息。获取用户地理位置信息的 Geolocation API。
- 拖放API和通知API。

WebSocket

它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种。

WebSocket 对象作为一个构造函数，用于新建 WebSocket 实例。readyState属性返回实例对象的当前状态，共有四种。实例对象的onopen属性，用于指定连接成功后的回调函数。实例对象的onclose属性，用于指定连接关闭后的回调函数。实例对象的onmessage属性，用于指定收到服务器数据后的回调函数。实例对象的send()方法用于向服务器发送数据。


Web Workers

Javascript是运行在单线程环境中，也就是说无法同时运行多个脚本。但是，如果将这段代码交给Web Worker去运行的话，那么情况就不一样了：浏览器会在后台启动一个独立的worker线程来专门负责代码的运行，因此，页面在这段Javascript代码运行期间依然可以响应用户的其他操作。

Web Worker 规范中定义了两类工作线程，分别是专用线程Dedicated Worker和共享线程 Shared Worker，其中，Dedicated Worker只能为一个页面所使用，而Shared Worker则可以被多个页面所共享。

只需调用Worker() 构造函数并传入一个要在 worker 线程内运行的脚本的URI，即可创建一个新的worker。Worker 与其主页面之间的通信是通过 onmessage 事件和 postMessage() 方法实现的。

## HTTP 协议

## 小程序
