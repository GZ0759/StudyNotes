# HTML5

## 简介

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

## 普通元素

语意化更好的内容元素，比如article、footer、header、nav、section

移除的元素：
- 纯表现的元素：basefont，big，center，font, s，strike，tt，u
- 对可用性产生负面影响的元素：frame，frameset，noframes


## 多媒体 Video/Audio

HTML5 最大特色之一就是支持音频视频，在通过增加了`<audio>`、`<video>`两个标签来实现对多媒体中的音频、视频使用的支持，只要在 Web 网页中嵌入这两个标签，而无需第三方插件（如 Flash）就可以实现音视频的播放功能。HTML5 对音频、视频文件的支持使得浏览器摆脱了对插件的依赖，加快了页面的加载速度，扩展了互联网多媒体技术的发展空间

## HTML5 拖放

拖放（Drag 和 drop）是 HTML5 标准的组成部分。

## 绘画 Canvas

HTML5 的 canvas 元素可以实现画布功能，该元素通过自带的 API 结合使用 JavaScript 脚本语言在网页上绘制图形和处理，拥有实现绘制线条、弧线以及矩形，用样式和颜色填充区域，书写样式化文本，以及添加图像的方法，且使用 JavaScript 可以控制其每一个像素。HTML5 的 canvas 元素使得浏览器无需 Flash 或 Silverlight 等插件就能直接显示图形或动画图像。

## HTML5 SVG

HTML5 支持内联 SVG。

## 地理定位

现今移动网络备受青睐，用户对实时定位的应用越来，要求也越来越高。HTML5 通过引入 Geolocation 的 API 可以通过 GPS 或网络信息实现用户的定位功能，定位更加准确、灵活。通过 HTML5 进行定位，除了可以定位自己的位置，还可以在他人对你开放信息的情况下获得他人的定位信息。

## 数据储存

HTML5 较之传统的数据存储有自已的存储方式，允许在客户端实现较大规模的数据存储。为了满足不同的需求，HTML5 支持 DOM Storage 和 Web SQL Database 两种存储机制。其中，DOM Storage 适用于具有 key/value 对的基本本地存储；而 WebSQLDatabase 是适用于关系型数据库的存储方式，开发者可以使用 SQL 语法对这些数据进行查询、插入等操作。

- 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失
- sessionStorage 的数据在浏览器关闭后自动删除

请描述一下 cookies，sessionStorage 和 localStorage 的区别
- cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密）
- cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递
- sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存
- 存储大小：
    - cookie数据大小不能超过4k
    - sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大

- 有期时间：
    - localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据
    - sessionStorage  数据在当前浏览器窗口关闭后自动删除
    - cookie  设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭




## HTML5 应用缓存

使用 HTML5，通过创建 cache manifest 文件，可以轻松地创建 web 应用的离线版本。

原理：HTML5的离线存储是基于一个新建的 `.appcache`文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示

如何使用：
- 页面头部像下面一样加入一个manifest的属性；
- 在cache.manifest文件的编写离线存储的资源
- 在离线状态时，操作window.applicationCache进行需求实现

## 多线程

HTML5 利用 Web Worker 将 Web 应用程序从原来的单线程业界中解放出来，通过创建一个 Web Worker 对象就可以实现多线程操作。JavaScript 创建的 Web 程序处理事务都是在单线程中执行，响应时间较长，而当 JavaScript 过于复杂时，还有可能出现死锁的局面。HTML5 新增加了一个 WebWorkerAPI，用户可以创建多个在后台的线程，将耗费较长时间的处理交给后台面不影响用户界面和响应速度，这些处理不会因用户交互而运行中断。使用后台线程不能访问页面和窗口对象，但后台线程可以和页面之间进行数据交互。子线程与子线程之间的数据交互，大致步骤如下：

- 先创建发送数据的子线程；
- 执行子线程任务，把要传递的数据发送给主线程；
- 在主线程接受到子线程传递回的消息时创建接收数据的子线程，然后把发送数据的子线程中返回的消息传递给接收数据的子线程；
- 执行接收数据子线程中的代码。

## HTML5 服务器发送事件

HTML5 服务器发送事件（server-sent event）允许网页获得来自服务器的更新。

## HTML5 表单输入类型

HTML5 拥有多个新的表单输入类型。这些新特性提供了更好的输入控制和验证。

- email
- url
- number
- range
- Date pickers (date, month, week, time, datetime, datetime-local)
- search
- color

## HTML5 表单元素

HTML5 拥有若干涉及表单的元素和属性。

- datalist
- keygen
- output

## HTML5 表单属性

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

# CSS3
