# HTML

## Doctype 作用

Doctype 作用，严格模式与混杂模式

`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前。`<!DOCTYPE>` 声明不是 HTML 标签；它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。HTML5 不基于 SGML，所以不需要引用 DTD。

严格模式：又称标准模式，是指浏览器按照 W3C 标准解析代码。混杂模式：又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。浏览器解析时到底使用严格模式还是混杂模式，与网页中的 DTD 直接相关。DOCTYPE 不存在或格式不正确会导致文档以混杂模式呈现。

## HTML5 新特性

- 语义化标签（header、section、article、aside、nav、footer）
- 增强型表单：新增属性（例如 require、placeholder）、新增元素（datalist、output）
- Canvas 画布，`getContext()` 方法可返回一个对象，该对象提供了用于在画布上绘图的方法和属性。
- 多媒体相关 API。音频（audio）和视频（video）。
- History API。通过脚本管理浏览器的历史记录。
- 本地储存。sessionStorage 和 localStorage。
- 离线应用程序。cache manifest 文件
- 文件 API。FileReader API。
- 通信 API。跨文档消息传输功能、使用 WebSockets API 来通过 socket 端口传递数据的功能和通过 Server-Sent Eventsource API 将服务器端事件主动推动到客户端的功能。
- Web Workers 处理线程。web worker 是运行在后台的 JavaScript，不会影响页面的性能。
- 获取地理位置信息。获取用户地理位置信息的 Geolocation API。
- 拖放 API 和通知 API。

### WebSocket

它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息，是真正的双向平等对话，属于服务器推送技术的一种。

WebSocket 对象作为一个构造函数，用于新建 WebSocket 实例。readyState 属性返回实例对象的当前状态，共有四种。实例对象的 onopen 属性，用于指定连接成功后的回调函数。实例对象的 onclose 属性，用于指定连接关闭后的回调函数。实例对象的 onmessage 属性，用于指定收到服务器数据后的回调函数。实例对象的 `send()` 方法用于向服务器发送数据。

### Web Workers

Javascript 是运行在单线程环境中，也就是说无法同时运行多个脚本。但是，如果将这段代码交给 Web Worker 去运行的话，那么情况就不一样了：浏览器会在后台启动一个独立的 worker 线程来专门负责代码的运行，因此，页面在这段 Javascript 代码运行期间依然可以响应用户的其他操作。

Web Worker 规范中定义了两类工作线程，分别是专用线程 Dedicated Worker 和共享线程 Shared Worker，其中，Dedicated Worker 只能为一个页面所使用，而 Shared Worker 则可以被多个页面所共享。

只需调用 `Worker()` 构造函数并传入一个要在 worker 线程内运行的脚本的 URI，即可创建一个新的 worker。Worker 与其主页面之间的通信是通过 onmessage 事件和 `postMessage()` 方法实现的。

## HTML5 兼容性

IE9+以及谷歌、火狐、苹果等主流浏览器对大部分 HTML5 属性均为支持状态。IE8/IE7/IE6 支持通过 document.createElement 方法产生的标签，可以利用这一特性让这些浏览器支持 HTML5 新标签。浏览器支持新标签后，还需要添加标签默认的样式（当然最好的方式是直接使用成熟的框架、使用最多的是 html5shim 框架）。

```html
<!--[if lt IE 9]>
  <script>
    src = "http://html5shim.googlecode.com/svn/trunk/html5.js";
  </script>
<![endif]-->
```

## HTML5 标签变化

新增的标签

- 结构标签
  - article 一篇文章
  - header 一个页面或一个区域的头部
  - nav 导航链接
  - section 一个区域
  - aside 页面内容部分的侧边栏
  - hgroup 文件中一个区域的相关信息
  - figure 一组媒体内容以及它们的标题
  - figcaption figure 元素的标题
  - footer 一个页面或一个区域的底部
  - dialog 一个对话框

- 多媒体标签
  - videa 一个视频
  - audio 音频内容
  - source 媒体资源
  - canvas 图片
  - embed 外部的可交互的内容或插件，例如 flash

- Web 应用标签
  - meter 状态标签（实时状态显示：气压、气温）
  - progress 状态标签（任务过程：安装、加载）
  - menu 命令列表
  - menuitem menu 命令列表标签
  - command menu 标记定义一个命令按钮

- 其它标签
  - ruby 注释或音标
  - rp 不支持 ruby 元素的显示内容
  - rt 对 ruby 的注释内容文本
  - mark 有标记的文本（黄色选中状态）
  - output 一些输入类型
  - keygen 表单里一个生成的键值
  - time 一个日期/时间

移除的元素有纯表现的元素（basefont/big/center/font/s/strike/tt/u）、对可用性产生负面影响的元素（frame/frameset/noframes）、产生混淆的元素（acronym/applet/isindex/dir）。

重定义标签。显示不变，只是表达的含义进行了重新定义的标签。

- b 代表内联文本，通常是粗体，没有传递表示重要的意思
- i 代表内联文本，通常是斜体，没有传递表示重要的意思
- dd 可以同 details 与 figure 一同使用，定义包含文本，dialog 也可用
- dt 可以同 details 与 figure 一同使用，汇总细节，dialog 也可用
- hr 表示主题结束，而不是水平线，虽然显示相同
- menu 重新定义用户界面的菜单，配合 commond 或者 menuitem 使用
- small 表示小字体，例如打印注释或者法律条款
- strong 表示重要性而不是强调符号

## 如何区分 HTML 和 HTML5?

HTML5 文档类型声明：`<!doctype html>`。DOCTYPE 声明的方式是区分 HTML 和 HTML5 标志的一个重要因素，此外，还可以根据新增的结构、功能元素来加以区分。

## 语义化的理解

HTML 语义化就是让页面的内容结构化，便于阅读和维护，便于浏览器、搜索引擎解析，利于 SEO。

## iframe 缺点

iframe 会阻塞主页面的 Onload 事件；iframe 和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载。

使用 iframe 之前需要考虑这两个缺点。如果需要使用 iframe，最好是通过 javascript 动态给 iframe 添加 src 属性值，这样可以可以绕开以上两个问题。

## HTML5

HTML5 建立的一些规则：

- 新特性应该基于 HTML、CSS、DOM 以及 JavaScript。
- 减少对外部插件的需求（比如 Flash）
- 更优秀的错误处理
- 更多取代脚本的标记
- HTML5 应该独立于设备
- 开发进程应对公众透明

HTML5 中的一些有趣的新特性：

- 用于绘画的 canvas 元素
- 用于媒介回放的 video 和 audio 元素
- 对本地离线存储的更好的支持
- 新的特殊内容元素，比如 article、footer、header、nav、section
- 新的表单控件，比如 calendar、date、time、email、url、search

### 普通元素

语意化更好的内容元素，比如article、footer、header、nav、section

移除的元素：
- 纯表现的元素：basefont，big，center，font, s，strike，tt，u
- 对可用性产生负面影响的元素：frame，frameset，noframes


### 多媒体 Video/Audio

HTML5 最大特色之一就是支持音频视频，在通过增加了`<audio>`、`<video>`两个标签来实现对多媒体中的音频、视频使用的支持，只要在 Web 网页中嵌入这两个标签，而无需第三方插件（如 Flash）就可以实现音视频的播放功能。HTML5 对音频、视频文件的支持使得浏览器摆脱了对插件的依赖，加快了页面的加载速度，扩展了互联网多媒体技术的发展空间

### HTML5 拖放

拖放（Drag 和 drop）是 HTML5 标准的组成部分。

### 绘画 Canvas

HTML5 的 canvas 元素可以实现画布功能，该元素通过自带的 API 结合使用 JavaScript 脚本语言在网页上绘制图形和处理，拥有实现绘制线条、弧线以及矩形，用样式和颜色填充区域，书写样式化文本，以及添加图像的方法，且使用 JavaScript 可以控制其每一个像素。HTML5 的 canvas 元素使得浏览器无需 Flash 或 Silverlight 等插件就能直接显示图形或动画图像。

### HTML5 SVG

HTML5 支持内联 SVG。

### 地理定位

现今移动网络备受青睐，用户对实时定位的应用越来，要求也越来越高。HTML5 通过引入 Geolocation 的 API 可以通过 GPS 或网络信息实现用户的定位功能，定位更加准确、灵活。通过 HTML5 进行定位，除了可以定位自己的位置，还可以在他人对你开放信息的情况下获得他人的定位信息。

### 数据储存

HTML5 较之传统的数据存储有自已的存储方式，允许在客户端实现较大规模的数据存储。为了满足不同的需求，HTML5 支持 DOM Storage 和 Web SQL Database 两种存储机制。其中，DOM Storage 适用于具有 key/value 对的基本本地存储；而 WebSQLDatabase 是适用于关系型数据库的存储方式，开发者可以使用 SQL 语法对这些数据进行查询、插入等操作。

**DOM Storage/webstorage**

本地存储，存储在客户端，包括 localStorage 和 sessionStorage。存放数据大小为一般为5MB，不参与和服务器的通信。

- localStorage 长期存储数据，浏览器关闭后数据不丢失，除非用户主动在浏览器清除 localStorage 信息
- sessionStorage 仅在当前会话下有效，关闭页面或浏览器后被清除

**cookie**

在浏览器和服务器间来回传递。生命期为只在设置的 cookie 过期时间之前一直有效，即使窗口或浏览器关闭。存放数据大小为 4K 左右。有个数限制（各浏览器不同），一般不能超过 20 个。与服务器端通信：每次都会携带在 HTTP 头中，如果使用 cookie 保存过多数据会带来性能问题。

- cookie 是网站为了标示用户身份而储存在用户本地终端上的数据（通常经过加密）
- cookie 数据始终在同源的 http 请求中携带（即使不需要），记会在浏览器和服务器间来回传递

### HTML5 应用缓存

使用 HTML5，通过创建 cache manifest 文件，可以轻松地创建 web 应用的离线版本。

原理：HTML5的离线存储是基于一个新建的 `.appcache`文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示

如何使用：
- 页面头部像下面一样加入一个manifest的属性；
- 在cache.manifest文件的编写离线存储的资源
- 在离线状态时，操作window.applicationCache进行需求实现

### 多线程

HTML5 利用 Web Worker 将 Web 应用程序从原来的单线程业界中解放出来，通过创建一个 Web Worker 对象就可以实现多线程操作。JavaScript 创建的 Web 程序处理事务都是在单线程中执行，响应时间较长，而当 JavaScript 过于复杂时，还有可能出现死锁的局面。HTML5 新增加了一个 WebWorkerAPI，用户可以创建多个在后台的线程，将耗费较长时间的处理交给后台面不影响用户界面和响应速度，这些处理不会因用户交互而运行中断。使用后台线程不能访问页面和窗口对象，但后台线程可以和页面之间进行数据交互。子线程与子线程之间的数据交互，大致步骤如下：

- 先创建发送数据的子线程；
- 执行子线程任务，把要传递的数据发送给主线程；
- 在主线程接受到子线程传递回的消息时创建接收数据的子线程，然后把发送数据的子线程中返回的消息传递给接收数据的子线程；
- 执行接收数据子线程中的代码。

### HTML5 服务器发送事件

HTML5 服务器发送事件（server-sent event）允许网页获得来自服务器的更新。

### HTML5 表单输入类型

HTML5 拥有多个新的表单输入类型。这些新特性提供了更好的输入控制和验证。

- email
- url
- number
- range
- Date pickers (date, month, week, time, datetime, datetime-local)
- search
- color

### HTML5 表单元素

HTML5 拥有若干涉及表单的元素和属性。

- datalist
- keygen
- output

### HTML5 表单属性

新的 form 属性：

- autocomplete
- novalidate

新的 input 属性：

- autocomplete
- autofocus
- form
- form overrides (formaction, formenctype, formmethod, formnovalidate, formtarget)
- height 和 width
- list
- min, max 和 step
- multiple
- pattern (regexp)
- placeholder
- required
