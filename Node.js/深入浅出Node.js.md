> 深入浅出 Node.js  
> 出版时间：2013-12-01  
> 作者：朴灵

# 第 1 章 Node 简介

Node 应该是如今最火热的技术了，从本章开始，我们将逐步揭示它的诸多细节。

## 1.1 Node 的诞生历程

Node 的诞生历程如下所示。

- 2009 年 3 月，Ryan Dahl 在其博客上宣布准备基于 V8 创建一个轻量级的 Web 服务器并提供一套库。
- 2009 年 5 月，Ryan Dahl 在 GitHub 上发布了最初的版本。
- 2009 年 12 月和 2010 年 4 月，两届 JSConf 大会都安排了 Node 的讲座。
- 2010 年年底，Node 获得硅谷云计算服务商 Joyent 公司的资助，其创始人 Ryan Dahl 加入 Joyent 公司全职负责 Node 的发展。
- 2011 年 7 月，Node 在微软的支持下发布了其 Windows 版本。
- 2011 年 11 月，Node 超越 Ruby on Rails，成为 GitHub 上关注度最高的项目（随后被 Bootstrap 项目超越，目前仍居第二）。
- 2012 年 1 月底，Ryan Dahl 在对 Node 架构设计满意的情况下，将掌门人的身份转交给 Isaac Z. Schlueter，自己转向一些研究项目。Isaac Z. Schlueter 是 Node 的包管理器 NPM 的作者，之后 Node 的版本发布和 bug 修复等工作由他接手
- 截至笔者执笔之日（2013 年 7 月 13 日），发布的 Node 稳定版为 v0.10.13，非稳定版为 v0.11.4, NPM 的官方模块数达到 34943 个，模块的周下载量为 1479 万次。
- 随后，Node 的发布计划主要集中在性能提升上，在 v0.14 之后，正式发布出 v1.0 版本。

## 1.2 Node 的命名与起源

在 Node 的[官方网站](http://nodejs.org)之外，Node 具有很多别称：Nodejs、NodeJS、Node.js 等。本书在写作过程中遵循官方的说法，将会一直使用 Node 这个名字，但是在当前语境之外，为了与其余表示节点的技术或名词相区别，均可以带上`.js`表明它是 Node。在听到这些词汇时，应该意识到，它们说的是一码事。除了本书的封面和此处会用到 Node.js 外，其余地方都会以 Node 作为正式称谓。

Node 名字的来由，其实跟它的起源是有密切关系的。

### 1.2.1 为什么是 JavaScript

Ryan Dahl 是一名资深的 C/C++程序员，在创造出 Node 之前，他的主要工作都是围绕高性能 Web 服务器进行的。经历过一些尝试和失败之后，他找到了设计高性能，Web 服务器的几个要点：事件驱动、非阻塞 I/O。

所以 Ryan Dahl 最初的目标是写一个基于事件驱动、非阻塞 I/O 的 Web 服务器，以达到更高的性能，提供 Apache 等服务器之外的选择。他提到，大多数人不设计一种更简单和更有效率的程序的主要原因是他们用到了阻塞 I/O 的库。写作 Node 的时候，Ryan Dahl 曾经评估过 C、Lua、Haskell、Ruby 等语言作为备选实现，结论为：C 的开发门槛高，可以预见不会有太多的开发者能将它用于日常的业务开发，所以舍弃它；Ryan Dahl 觉得自己还不足够玩转 Haskell，所以舍弃它；Lua 自身已经含有很多阻塞 I/O 库，为其构建非阻塞 I/O 库也不能改变人们继续使用阻塞 I/O 库的习惯，所以也舍弃它；而 Ruby 的虚拟机由于性能不好而落选。

相比之下，JavaScript 比 C 的开发门槛要低，比 Lua 的历史包袱要少。尽管服务器端 JavaScript 存在已经很多年了，但是后端部分一直没有市场，可以说历史包袱为零，为其导入非阻塞 I/O 库没有额外阻力。另外，JavaScript 在浏览器中有广泛的事件驱动方面的应用，暗合 Ryan Dahl 喜好基于事件驱动的需求。当时，第二次浏览器大战也渐渐分出高下，Chrome 浏览器的 JavaScript 引擎 V8 摘得性能第一的桂冠，而且其基于新 BSD 许可证发布，自然受到 Ryan Dahl 的欢迎。考虑到高性能、符合事件驱动、没有历史包袱这 3 个主要原因，JavaScript 成为了 Node 的实现语言。

### 1.2.2 为什么叫 Node

起初，Ryan Dahl 称他的项目为 web.js，就是一个 Web 服务器，但是项目的发展超过了他最初单纯开发一个 Web 服务器的想法，变成了构建网络应用的一个基础框架，这样可以在它的基础上构建更多的东西，诸如服务器、客户端、命令行工具等。Node 发展为一个强制不共享任何资源的单线程、单进程系统，包含十分适宜网络的库，为构建大型分布式应用程序提供基础设施，其目标也是成为一个构建快速、可伸缩的网络应用平台。它自身非常简单，通过通信协议来组织许多 Node，非常容易通过扩展来达成构建大型网络应用的目的。每一个 Node 进程都构成这个网络应用中的一个节点，这是它名字所含意义的真谛。

## 1.3 Node 给 JavaScript 带来的意义

V8 给 Chrome 浏览器带来了一个强劲的心脏，使得它在浏览器大战中脱颖而出，也使得 Ryan Dahl 在语言评估中为选择 JavaScript 增加了一个极大的权重值。这里我们要谈谈 Node 给 JavaScript 带来的一个新局面。鉴于 Node 之前那些不给力的后端 JavaScript 实现，在性能和编程模型等方面没能达到与其他语言一较高下的程度，这里先撇开不谈，先谈谈 Node 与浏览器的对比。

Chrome 浏览器和 Node 的组件构成如图 1-1 所示。我们知道浏览器中除了 V8 作为 JavaScript 引擎外，还有一个 WebKit 布局引擎。HTML5 在发展过程中定义了更多更丰富的 API。在实现上，浏览器提供了越来越多的功能暴露给 JavaScript 和 HTML 标签。这个愿景美好，但对于前端浏览器的发展现状而言，HTML5 标准统一的过程是相对缓慢的。JavaScript 作为一门图灵完备的语言，长久以来却限制在浏览器的沙箱中运行，它的能力取决于浏览器中间层提供的支持有多少。

除了 HTML、WebKit 和显卡这些 UI 相关技术没有支持外，Node 的结构与 Chrome 十分相似。它们都是基于事件驱动的异步架构，浏览器通过事件驱动来服务界面上的交互，Node 通过事件驱动来服务 I/O，这个细节将在第 3 章中详述。在 Node 中，JavaScript 可以随心所欲地访问本地文件，可以搭建 WebSocket 服务器端，可以连接数据库，可以如 Web Workers 一样玩转多进程。如今，JavaScript 可以运行在不同的地方，不再继续限制在浏览器中与 CSS 样式表、DOM 树打交道。如果 HTTP 协议栈是水平面，Node 就是浏览器在协议栈另一边的倒影。Node 不处理 UI，但用与浏览器相同的机制和原理运行。Node 打破了过去 JavaScript 只能在浏览器中运行的局面。前后端编程环境统一，可以大大降低前后端转换所需要的上下文交换代价。

对于前端工程师而言，自己所熟悉的 JavaScript 如今竟然可以在另一个地方放出异彩，不谈其他原因，仅仅因为好奇，就值得去关注和探究它。

> 随着 Node 的出现，关于 JavaScript 的想象总是无限的。目前，社区已经出现 node-webkit 这样的项目，这个项目在 2012 年的沪 JS 会议上首次介绍给了公众。如同上文提及的关于浏览器的优势和限制，在 node-webkit 项目中，它将 Node 中的事件循环和 WebKit 的事件循环融合在一起，既可以通过它享受 HTML、CSS 带来的 UI 构建，也能通过它访问本地资源，将两者的优势整合到一起。桌面应用程序的开发可以完全通过 HTML、CSS、JavaScript 完成。

## 1.4 Node 的特点

作为后端 JavaScript 的运行平台，Node 保留了前端浏览器 JavaScript 中那些熟悉的接口，没有改写语言本身的任何特性，依旧基于作用域和原型链，区别在于它将前端中广泛运用的思想迁移到了服务器端。下面我们来看看 Node 相较其他语言的一些特点。

### 1.4.1 异步 I/O

关于异步 I/O，向前端工程师解释起来或许会容易一些，因为发起 Ajax 调用对于前端工程师而言是再熟悉不过的场景了。下面的代码用于发起一个 Ajax 请求：

```js
$.post("/url", { title: "深入浅出 Node.js" }, function (data) {
  console.log("收到响应");
});
console.log("发送 Ajax 结束");
```

熟悉异步的用户必然知道，“收到响应”是在“发送 Ajax 结束”之后输出的。在调用`$.post()`后，后续代码是被立即执行的，而“收到响应”的执行时间是不被预期的。我们只知道它将在这个异步请求结束后执行，但并不知道具体的时间点。异步调用中对于结果值的捕获是符合“Don't call me, I willcall you”的原则的，这也是注重结果，不关心过程的一种表现。图 1-2 是一个经典的 Ajax 调用。

在 Node 中，异步 I/O 也很常见。以读取文件为例，我们可以看到它与前端 Ajax 调用的方式是极其类似的：

```js
var fs = require("fs");
fs.readFile("/path", function (err, file) {
  console.log("读取文件完成");
});
console.log("发起读取文件");
```

这里的“发起读取文件”是在“读取文件完成”之前输出的。同样，“读取文件完成”的执行也取决于读取文件的异步调用何时结束。图 1-3 是一个经典的异步调用。

在 Node 中，绝大多数的操作都以异步的方式进行调用。Ryan Dahl 排除万难，在底层构建了很多异步 I/O 的 API，从文件读取到网络请求等，均是如此。这样的意义在于，在 Node 中，我们可以从语言层面很自然地进行并行 I/O 操作。每个调用之间无须等待之前的 I/O 调用结束。在编程模型上可以极大提升效率。

下面的两个文件读取任务的耗时取决于最慢的那个文件读取的耗时：

```js
fs.readFile("/path1", function (err, file) {
  console.log("读取文件1完成");
});
fs.readFile("/path2", function (err, file) {
  console.log("读取文件2完成");
});
```

而对于同步 I/O 而言，它们的耗时是两个任务的耗时之和。这里异步带来的优势是显而易见的。

关于异步 I/O 是如何提升效率的及其本身的机制和实现，我们将在第 3 章中详述。

### 1.4.2 事件与回调函数

随着 Web 2.0 时代的到来，JavaScript 在前端担任了更多的职责，事件也得到了广泛的应用。Node 不像 Rhino 那样受 Java 的影响很大，而是将前端浏览器中应用广泛且成熟的事件引入后端，配合异步 I/O，将事件点暴露给业务逻辑。

下面的例子展示的是 Ajax 异步提交的服务器端处理过程。Node 创建一个 Web 服务器，并侦听 8080 端口。对于服务器，我们为其绑定了 request 事件，对于请求对象，我们为其绑定了 data 事件和 end 事件：

```js
var http = require("http");
var querystring = require("querystring");
// 侦听服务器的request事件
http
  .createServer(function (req, res) {
    var postData = "";
    req.setEncoding("utf8");
    // 侦听请求的data事件
    req.on("data", function (trunk) {
      postData += trunk;
    });
    // 侦听请求的end事件
    req.on("end", function () {
      res.end(postData);
    });
  })
  .listen(8080);
console.log("服务器启动成 ");
```

相应地，我们在前端为 Ajax 请求绑定了 success 事件，在发出请求后，只需关心请求成功时执行相应的业务逻辑即可，相关代码如下：

```js
$.ajax({
  url: "/url",
  method: "POST",
  data: {},
  success: function (data) {
    // success事件
  },
});
```

相比之下，无论在前端还是后端，事件都是常用的。对于其他语言来说，这种俯拾皆是 JavaScript 的熟悉感觉是基本不会出现的。

事件的编程方式具有轻量级、松耦合、只关注事务点等优势，但是在多个异步任务的场景下，事件与事件之间各自独立，如何协作是一个问题。

从前面可以看到，回调函数无处不在。这是因为在 JavaScript 中，我们将函数作为第一等公民来对待，可以将函数作为对象传递给方法作为实参进行调用。

与其他的 Web 后端编程语言相比，Node 除了异步和事件外，回调函数是一大特色。纵观下来，回调函数也是最好的接受异步调用返回数据的方式。但是这种编程方式对于很多习惯同步思路编程的人来说，也许是十分不习惯的。代码的编写顺序与执行顺序并无关系，这对他们可能造成阅读上的障碍。在流程控制方面，因为穿插了异步方法和回调函数，与常规的同步方式相比，变得不那么一目了然了。

在转变为异步编程思维后，通过对业务的划分和对事件的提炼，在流程控制方面处理业务的复杂度与同步方式实际上是一致的。

关于流程控制和事件协作的方法和技巧，我们将在第 4 章中进一步探讨。

### 1.4.3 单线程

Node 保持了 JavaScript 在浏览器中单线程的特点。而且在 Node 中，JavaScript 与其余线程是无法共享任何状态的。单线程的最大好处是不用像多线程编程那样处处在意状态的同步问题，这里没有死锁的存在，也没有线程上下文交换所带来的性能上的开销。

同样，单线程也有它自身的弱点，这些弱点是学习 Node 的过程中必须要面对的。积极面对这些弱点，可以享受到 Node 带来的好处，也能避免潜在的问题，使其得以高效利用。单线程的弱点具体有以下 3 方面。

- 无法利用多核 CPU。
- 错误会引起整个应用退出，应用的健壮性值得考验。
- 大量计算占用 CPU 导致无法继续调用异步 I/O。

像浏览器中 JavaScript 与 UI 共用一个线程一样，JavaScript 长时间执行会导致 UI 的渲染和响应被中断。在 Node 中，长时间的 CPU 占用也会导致后续的异步 I/O 发不出调用，已完成的异步 I/O 的回调函数也会得不到及时执行。

最早解决这种大计算量问题的方案是 Google 公司开发的 Gears。它启用一个完全独立的进程，将需要计算的程序发送给这个进程，在结果得出后，通过事件将结果传递回来。这个模型将计算量分发到其他进程上，以此来降低运算造成阻塞的几率。后来，HTML5 定制了 Web Workers 的标准，Google 放弃了 Gears，全力支持 Web Workers。Web Workers 能够创建工作线程来进行计算，以解决 JavaScript 大计算阻塞 UI 渲染的问题。工作线程为了不阻塞主线程，通过消息传递的方式来传递运行结果，这也使得工作线程不能访问到主线程中的 UI。

Node 采用了与 Web Workers 相同的思路来解决单线程中大计算量的问题：child_process。

子进程的出现，意味着 Node 可以从容地应对单线程在健壮性和无法利用多核 CPU 方面的问题。通过将计算分发到各个子进程，可以将大量计算分解掉，然后再通过进程之间的事件消息来传递结果，这可以很好地保持应用模型的简单和低依赖。通过 Master-Worker 的管理方式，也可以很好地管理各个工作进程，以达到更高的健壮性。

关于如何通过子进程来充分利用硬件资源和提升应用的健壮性，这是一个值得探究的话题。怎样才能使我们既享受到无忧无虑的单线程编程，又高效利用资源呢？请挪步到第 9 章。

### 1.4.4 跨平台

起初，Node 只可以在 Linux 平台上运行。如果想在 Windows 平台上学习和使用 Node，则必须通过 Cygwin 或者 MinGW。随着 Node 的发展，微软注意到了它的存在，并投入了一个团队帮助 Node 实现 Windows 平台的兼容，在 v0.6.0 版本发布时，Node 已经能够直接在 Windows 平台上运行了。图 1-4 是 Node 基于 libuv 实现跨平台的架构示意图。

兼容 Windows 和 Linux 平台主要得益于 Node 在架构层面的改动，它在操作系统与 Node 上层模块系统之间构建了一层平台层架构，即 libuv。目前，libuv 已经成为许多系统实现跨平台的基础组件。关于 libuv 的设计，我们将在第 3 章中介绍。

通过良好的架构，Node 的第三方 C++模块也可以借助 libuv 实现跨平台。目前，除了没有保持更新的 C++模块外，大部分 C++模块都能实现跨平台的兼容。

## 1.5 Node 的应用场景

在进行技术选型之前，需要了解一项新技术具体适合什么样的场景，毕竟合适的技术用在合适的场景可以起到意想不到的效果。关于 Node，探讨得较多的主要有 I/O 密集型和 CPU 密集型。

### 1.5.1 I/O 密集型

在 Node 的推广过程中，无数次有人问起 Node 的应用场景是什么。如果将所有的脚本语言拿到一处来评判，那么从单线程的角度来说，Node 处理 I/O 的能力是值得竖起拇指称赞的。通常，说 Node 擅长 I/O 密集型的应用场景基本上是没人反对的。Node 面向网络且擅长并行 I/O，能够有效地组织起更多的硬件资源，从而提供更多好的服务。

I/O 密集的优势主要在于 Node 利用事件循环的处理能力，而不是启动每一个线程为每一个请求服务，资源占用极少。

### 1.5.2 是否不擅长 CPU 密集型业务

换一个角度，在 CPU 密集的应用场景中，Node 是否能胜任呢？实际上，V8 的执行效率是十分高的。单以执行效率来做评判，V8 的执行效率是毋庸置疑的。

我们将相同的斐波那契数列计算`F0=0, F1=1, Fn=F(n-1)+F(n-2)(n≥2)`分别用各种脚本语言写了算法实现，并进行了 `n = 40` 的计算，以比较性能。这个测试主要偏重 CPU 栈操作，表 1-1 是其中一次运算耗时的排行。在这些脚本语言中（其中 C 和 Go 语言是静态语言，用于参考）, Node 是足够高效的，它优秀的运算能力主要来自 V8 的深度性能优化。

这样的测试结果尽管不能完全反映出各个语言的性能优劣，但已经可以表明 Node 在性能上不俗的表现。从另一个角度来说，这可以表明 CPU 密集型应用其实并不可怕。CPU 密集型应用给 Node 带来的挑战主要是：由于 JavaScript 单线程的原因，如果有长时间运行的计算（比如大循环），将会导致 CPU 时间片不能释放，使得后续 I/O 无法发起。但是适当调整和分解大型运算任务为多个小任务，使得运算能够适时释放，不阻塞 I/O 调用的发起，这样既可同时享受到并行异步 I/O 的好处，又能充分利用 CPU。

关于 CPU 密集型应用，Node 的异步 I/O 已经解决了在单线程上 CPU 与 I/O 之间阻塞无法重叠利用的问题，I/O 阻塞造成的性能浪费远比 CPU 的影响小。对于长时间运行的计算，如果它的耗时超过普通阻塞 I/O 的耗时，那么应用场景就需要重新评估，因为这类计算比阻塞 I/O 还影响效率，甚至说就是一个纯计算的场景，根本没有 I/O。此类应用场景或许应当采用多线程的方式进行计算。Node 虽然没有提供多线程用于计算支持，但是还是有以下两个方式来充分利用 CPU。

- Node 可以通过编写 C/C++扩展的方式更高效地利用 CPU，将一些 V8 不能做到性能极致的地方通过 C/C++来实现。由上面的测试结果可以看到，通过 C/C++ 扩展的方式实现斐波那契数列计算，速度比 Java 还快。
- 如果单线程的 Node 不能满足需求，甚至用了 C/C++扩展后还觉得不够，那么通过子进程的方式，将一部分 Node 进程当做常驻服务进程用于计算，然后利用进程间的消息来传递结果，将计算与 I/O 分离，这样还能充分利用多 CPU。

CPU 密集不可怕，如何合理调度是诀窍。

### 1.5.3 与遗留系统和平共处

有人会说：“JavaScript 一统前后端了，将来会不会干掉其他的语言？”言语中充满了危机感。

在 Web 端，过去大多都是同步的方式编写的程序，这种串行调用下层应用数据的过程中充斥着串行的等待时间，如果采用多线程来解决这种串行等待，又或多或少地显得小题大作。在 Node 中，语言层面即可天然并行的特性在这种场景中显得十分有效。对于已有的稳定系统，并非意味着我们要抛弃掉。

LinkedIn 在他们的移动版网站上的实践非常典型地说明了这个问题。旧有的系统具有非常稳定的数据输出，持续为传统网站服务，同时为移动版提供数据源，Node 将该数据源当做数据接口，发挥异步并行的优势，而不用关心它背后是用什么语言实现的。

这方面，国内的雪球财经也有很好的实践。雪球财经是从旧有的 Java 项目中分离出一个子项目，在这个子项目中，没有继续采用 Java/JSP 而是采用 Node 来完成 Web 端的开发，使得前端工程师在 HTTP 协议栈的两端能够高效灵活地开发，避免了 Java 烦琐的表达；另一方面，又利用 Java 作为后端接口和中间件，使其具有良好的稳定性。两者互相结合，取长补短。

### 1.5.4 分布式应用

阿里巴巴的数据平台对 Node 的分布式应用算是一个典型的例子。分布式应用意味着对可伸缩性的要求非常高。数据平台通常要在一个数据库集群中去寻找需要的数据。阿里巴巴开发了中间层应用 NodeFox、ITier，将数据库集群做了划分和映射，查询调用依旧是针对单张表进行 SQL 查询，中间层分解查询 SQL，并行地去多台数据库中获取数据并合并。NodeFox 能实现对多台 MySQL 数据库的查询，如同查询一台 MySQL 一样，而 ITier 更强大，查询多个数据库如同查询单个数据库一样，这里的多个数据库是指不同的数据库，如 MySQL 或其他的数据库。

这个案例其实也是高效利用并行 I/O 的例子。Node 高效利用并行 I/O 的过程，也是高效使用数据库的过程。对于 Node，这个行为只是一次普通的 I/O。对于数据库而言，却是一次复杂的计算，所以也是进而充分压榨硬件资源的过程。

## 1.6 Node 的使用者

在短短四年多的时间里，Node 变得非常热门，使用者也非常多。这些使用者对于 Node 的各自倚重点也各不相同。经过整理，主要有下面几类。

- 前后端编程语言环境统一。这类倚重点的代表是雅虎。雅虎开放了 Cocktail 框架，利用自己深厚的前端沉淀，将 YUI3 这个前端框架的能力借助 Node 延伸到服务器端，使得使用者摆脱了日常工作中一边写 JavaScript 一边写 PHP 所带来的上下文交换负担。
- Node 带来的高性能 I/O 用于实时应用。Voxer 将 Node 应用在实时语音上。国内腾讯网的朋友将 Node 应用在长连接中，以提供实时功能，花瓣网、蘑菇街等公司通过 socket.io 实现实时通知的功能。
- 并行 I/O 使得使用者可以更高效地利用分布式环境。阿里巴巴和 eBay 是这方面的典型。阿里巴巴的 NodeFox 和 eBay 的 ql.io 都是借用 Node 并行 I/O 的能力，更高效地使用已有的数据。
- 并行 I/O，有效利用稳定接口提升 Web 渲染能力。雪球财经和 LinkedIn 的移动版网站均是这种案例，撇弃同步等待式的顺序请求，大胆采用并行 I/O，加速数据的获取进而提升 Web 的渲染速度。
- 云计算平台提供 Node 支持。微软将 Node 引入 Azure 的开发中，阿里云、百度均纷纷在云服务器上提供 Node 应用托管服务，Joyent 更是云计算中提供 Node 支持的代表。这类平台看重 JavaScript 带来的开发上的优势，以及低资源占用、高性能的特点。
- 游戏开发领域。游戏领域对实时和并发有很高的要求，网易开源了 pomelo 实时框架，可以应用在游戏和高实时应用中。
- 工具类应用。过去依赖 Java 或其他语言构建的前端工具类应用，纷纷被一些前端工程师用 Node 重写，用前端熟悉的语言为前端构建熟悉的工具。

## 1.7 参考资源

本章参考的资源如下：

- http://www.infoq.com/cn/articles/what-is-nodejs
- https://github.com/popular/watched
- http://groups.google.com/group/nodejs/browse_thread/thread/85f6a3829bc64cb6
- http://groups.google.com/groups/profile?enc_user=dPo6jggAAACthftLMWCfUq8U6obMz179
- http://search.npmjs.org/
- http://code.google.com/p/v8/
- http://cnodejs.org/topic/4f16442ccae1f4aa27001137
- http://weibo.com/1744667943/eBszJXcEsX1
- http://stackoverflow.com/questions/5621812/why-is-node-js-named-node-js
- http://www.theregister.co.uk/2011/03/01/the_rise_and_rise_of_node_dot_js/page4.html
- http://ued.taobao.com/blog/2011/09/02/what-is-nod/
- http://www.infoq.com/cn/news/2012/04/interview-xueqiu-using-nodejs
- http://teddziuba.com/2011/10/node-js-is-cancer.html
- http://www.cnblogs.com/fengmk2/archive/2011/12/14/2288147.html

# 第 2 章 模块机制

首先，我想从模块为你娓娓道来 Node。

JavaScript 自诞生以来，曾经没有人拿它当做一门真正的编程语言，认为它不过是一种网页小脚本而已，在 Web 1.0 时代，这种脚本语言在网络中主要有两个作用广为流传，一个是表单校验，另一个是网页特效。另一方面，由于仓促地被创造出来，所以它自身的各种陷阱和缺点也被各种编程人员广为诟病。直到 Web 2.0 时代，前端工程师利用它大大提升了网页上的用户体验。在这个过程中，B/S 应用展现出比 C/S 应用优越的地方。至此，JavaScript 才被广泛重视起来。

在 Web 2.0 流行的过程中，各种前端库和框架被开发出来，它们最初用于兼容各个版本的浏览器，随后随着更多的用户需求在前端被实现，JavaScript 也从表单校验跃迁到应用开发的级别上。在这个过程中，它大致经历了工具类库、组件库、前端框架、前端应用的变迁，如图 2-1 所示。

经历了长长的后天努力过程，JavaScript 不断被类聚和抽象，以更好地组织业务逻辑。从另一个角度而言，它也道出了 JavaScript 先天就缺乏的一项功能：模块。

在其他高级语言中，Java 有类文件，Python 有 import 机制，Ruby 有 require, PHP 有 include 和 require。而 JavaScript 通过`<script>`标签引入代码的方式显得杂乱无章，语言自身毫无组织和约束能力。人们不得不用命名空间等方式人为地约束代码，以求达到安全和易用的目的。

但是看起来凌乱的 JavaScript 编程现状并不代表着社区没有进步，JavaScript 的本地化编程之路一直在探索中。在 Node 出现之前，服务器端 JavaScript 基本没有市场，与欣欣向荣的前端 JavaScript 应用相比，Rhino 等后端 JavaScript 运行环境基本只是用于小工具，但是经历十多年的发展后，社区也为 JavaScript 制定了相应的规范，其中 CommonJS 规范的提出算是最为重要的里程碑。

## 2.1 CommonJS 规范

CommonJS 规范为 JavaScript 制定了一个美好的愿景——希望 JavaScript 能够在任何地方运行。

### 2.1.1 CommonJS 的出发点

在 JavaScript 的发展历程中，它主要在浏览器前端发光发热。由于官方规范（ECMAScript）规范化的时间较早，规范涵盖的范畴非常小。这些规范中包含词法、类型、上下文、表达式、声明（statement）、方法、对象等语言的基本要素。在实际应用中，JavaScript 的表现能力取决于宿主环境中的 API 支持程度。在 Web 1.0 时代，只有对 DOM、BOM 等基本的支持。随着 Web 2.0 的推进，HTML5 崭露头角，它将 Web 网页带进 Web 应用的时代，在浏览器中出现了更多、更强大的 API 供 JavaScript 调用，这得感谢 W3C 组织对 HTML5 规范的推进以及各大浏览器厂商对规范的大力支持。但是，Web 在发展，浏览器中出现了更多的标准 API，这些过程发生在前端，后端 JavaScript 的规范却远远落后。对于 JavaScript 自身而言，它的规范依然是薄弱的，还有以下缺陷。

- 没有模块系统。
- 标准库较少。ECMAScript 仅定义了部分核心库，对于文件系统，I/O 流等常见需求却没有标准的 API。就 HTML5 的发展状况而言，W3C 标准化在一定意义上是在推进这个过程，但是它仅限于浏览器端。
- 没有标准接口。在 JavaScript 中，几乎没有定义过如 Web 服务器或者数据库之类的标准统一接口。
- 缺乏包管理系统。这导致 JavaScript 应用中基本没有自动加载和安装依赖的能力。

CommonJS 规范的提出，主要是为了弥补当前 JavaScript 没有标准的缺陷，以达到像 Python、Ruby 和 Java 具备开发大型应用的基础能力，而不是停留在小脚本程序的阶段。他们期望那些用 CommonJS API 写出的应用可以具备跨宿主环境执行的能力，这样不仅可以利用 JavaScript 开发富客户端应用，而且还可以编写以下应用。

- 服务器端 JavaScript 应用程序。
- 命令行工具。
- 桌面图形界面应用程序。
- 混合应用（Titanium 和 Adobe AIR 等形式的应用）。

如今，CommonJS 中的大部分规范虽然依旧是草案，但是已经初显成效，为 JavaScript 开发大型应用程序指明了一条非常棒的道路。目前，它依旧在成长中，这些规范涵盖了模块、二进制、Buffer、字符集编码、I/O 流、进程环境、文件系统、套接字、单元测试、Web 服务器网关接口、包管理等。

理论和实践总是相互影响和促进的，Node 能以一种比较成熟的姿态出现，离不开 CommonJS 规范的影响。在服务器端，CommonJS 能以一种寻常的姿态写进各个公司的项目代码中，离不开 Node 优异的表现。实现的优良表现离不开规范最初优秀的设计，规范因实现的推广而得以普及。图 2-2 是 Node 与浏览器以及 W3C 组织、CommonJS 组织、ECMAScript 之间的关系，共同构成了一个繁荣的生态系统。

图 2-2 Node 与浏览器以及 W3C 组织、CommonJS 组织、ECMAScript 之间的关系

Node 借鉴 CommonJS 的 Modules 规范实现了一套非常易用的模块系统，NPM 对 Packages 规范的完好支持使得 Node 应用在开发过程中事半功倍。在本章中，我们主要就 Node 的模块和包的实现进行展开说明。

### 2.1.2 CommonJS 的模块规范

CommonJS 对模块的定义十分简单，主要分为模块引用、模块定义和模块标识 3 个部分。

1. 模块引用

模块引用的示例代码如下：

```js
var math = require("math");
```

在 CommonJS 规范中，存在`require()`方法，这个方法接受模块标识，以此引入一个模块的 API 到当前上下文中。

2. 模块定义在模块中，上下文提供`require()`方法来引入外部模块。对应引入的功能，上下文提供了 exports 对象用于导出当前模块的方法或者变量，并且它是唯一导出的出口。在模块中，还存在一个 module 对象，它代表模块自身，而 exports 是 module 的属性。在 Node 中，一个文件就是一个模块，将方法挂载在 exports 对象上作为属性即可定义导出的方式：

```js
// math.js
exports.add = function () {
  var sum = 0,
    i = 0,
    args = arguments,
    l = args.length;
  while (i < l) {
    sum += args[i++];
  }
  return sum;
};
```

在另一个文件中，我们通过 `require()`方法引入模块后，就能调用定义的属性或方法了：

```js
// program.js
var math = require("math");
exports.increment = function (val) {
  return math.add(val, 1);
};
```

3. 模块标识

模块标识其实就是传递给 `require()`方法的参数，它必须是符合小驼峰命名的字符串，或者以`.`、`..`开头的相对路径，或者绝对路径。它可以没有文件名后缀`.js`。

模块的定义十分简单，接口也十分简洁。它的意义在于将类聚的方法和变量等限定在私有的作用域中，同时支持引入和导出功能以顺畅地连接上下游依赖。如图 2-3 所示，每个模块具有独立的空间，它们互不干扰，在引用时也显得干净利落。

图 2-3 模块定义

CommonJS 构建的这套模块导出和引入机制使得用户完全不必考虑变量污染，命名空间等方案与之相比相形见绌。

## 2.2 Node 的模块实现

Node 在实现中并非完全按照规范实现，而是对模块规范进行了一定的取舍，同时也增加了少许自身需要的特性。尽管规范中 exports、require 和 module 听起来十分简单，但是 Node 在实现它们的过程中究竟经历了什么，这个过程需要知晓。

在 Node 中引入模块，需要经历如下 3 个步骤。

1. 路径分析
2. 文件定位
3. 编译执行

在 Node 中，模块分为两类：一类是 Node 提供的模块，称为核心模块；另一类是用户编写的模块，称为文件模块。

- 核心模块部分在 Node 源代码的编译过程中，编译进了二进制执行文件。在 Node 进程启动时，部分核心模块就被直接加载进内存中，所以这部分核心模块引入时，文件定位和编译执行这两个步骤可以省略掉，并且在路径分析中优先判断，所以它的加载速度是最快的。
- 文件模块则是在运行时动态加载，需要完整的路径分析、文件定位、编译执行过程，速度比核心模块慢。

接下来，我们展开详细的模块加载过程。

### 2.2.1 优先从缓存加载

展开介绍路径分析和文件定位之前，我们需要知晓的一点是，与前端浏览器会缓存静态脚本文件以提高性能一样，Node 对引入过的模块都会进行缓存，以减少二次引入时的开销。不同的地方在于，浏览器仅仅缓存文件，而 Node 缓存的是编译和执行之后的对象。

不论是核心模块还是文件模块，`require()`方法对相同模块的二次加载都一律采用缓存优先的方式，这是第一优先级的。不同之处在于核心模块的缓存检查先于文件模块的缓存检查。

### 2.2.2 路径分析和文件定位

因为标识符有几种形式，对于不同的标识符，模块的查找和定位有不同程度上的差异。

1. 模块标识符分析

前面提到过，`require()`方法接受一个标识符作为参数。在 Node 实现中，正是基于这样一个标识符进行模块查找的。模块标识符在 Node 中主要分为以下几类。

- 核心模块，如 http、fs、path 等。
- `.`或`..`开始的相对路径文件模块。
- 以`/`开始的绝对路径文件模块。
- 非路径形式的文件模块，如自定义的 connect 模块。

**核心模块**

核心模块的优先级仅次于缓存加载，它在 Node 的源代码编译过程中已经编译为二进制代码，其加载过程最快。

如果试图加载一个与核心模块标识符相同的自定义模块，那是不会成功的。如果自己编写了一个 http 用户模块，想要加载成功，必须选择一个不同的标识符或者换用路径的方式。

**路径形式的文件模块**

以`.`、`..`和`/`开始的标识符，这里都被当做文件模块来处理。在分析文件模块时，`require()`方法会将路径转为真实路径，并以真实路径作为索引，将编译执行后的结果存放到缓存中，以使二次加载时更快。

由于文件模块给 Node 指明了确切的文件位置，所以在查找过程中可以节约大量时间，其加载速度慢于核心模块。

**自定义模块**

自定义模块指的是非核心模块，也不是路径形式的标识符。它是一种特殊的文件模块，可能是一个文件或者包的形式。这类模块的查找是最费时的，也是所有方式中最慢的一种。

在介绍自定义模块的查找方式之前，需要先介绍一下模块路径这个概念。

模块路径是 Node 在定位文件模块的具体文件时制定的查找策略，具体表现为一个路径组成的数组。关于这个路径的生成规则，我们可以手动尝试一番。

1. 创建 module_path.js 文件，其内容为 `console.log(module.paths)`;。
2. 将其放到任意一个目录中然后执行 nodemodule_path.js。

在 Linux 下，你可能得到的是这样一个数组输出：

```js
[
  "/home/jackson/research/node_modules",
  "/home/jackson/node_modules",
  "/home/node_modules",
  "/node_modules",
];
```

而在 Windows 下，也许是这样：

```js
["c:\\nodejs\\node_modules", "c:\\node_modules"];
```

可以看出，模块路径的生成规则如下所示。

- 当前文件目录下的 node_modules 目录。
- 父目录下的 node_modules 目录。
- 父目录的父目录下的 node_modules 目录。
- 沿路径向上逐级递归，直到根目录下的 node_modules 目录。

它的生成方式与 JavaScript 的原型链或作用域链的查找方式十分类似。在加载的过程中，Node 会逐个尝试模块路径中的路径，直到找到目标文件为止。可以看出，当前文件的路径越深，模块查找耗时会越多，这是自定义模块的加载速度是最慢的原因。

2. 文件定位

从缓存加载的优化策略使得二次引入时不需要路径分析、文件定位和编译执行的过程，大大提高了再次加载模块时的效率。

但在文件的定位过程中，还有一些细节需要注意，这主要包括文件扩展名的分析、目录和包的处理。

**文件扩展名分析**

`require()`在分析标识符的过程中，会出现标识符中不包含文件扩展名的情况。CommonJS 模块规范也允许在标识符中不包含文件扩展名，这种情况下，Node 会按`.js`、`.json`、`.node` 的次序补足扩展名，依次尝试。

在尝试的过程中，需要调用 fs 模块同步阻塞式地判断文件是否存在。因为 Node 是单线程的，所以这里是一个会引起性能问题的地方。小诀窍是：如果是`.node` 和`.json` 文件，在传递给 `require()`的标识符中带上扩展名，会加快一点速度。另一个诀窍是：同步配合缓存，可以大幅度缓解 Node 单线程中阻塞式调用的缺陷。

**目录分析和包**

在分析标识符的过程中，`require()`通过分析文件扩展名之后，可能没有查找到对应文件，但却得到一个目录，这在引入自定义模块和逐个模块路径进行查找时经常会出现，此时 Node 会将目录当做一个包来处理。

在这个过程中，Node 对 CommonJS 包规范进行了一定程度的支持。首先，Node 在当前目录下查找 package.json（CommonJS 包规范定义的包描述文件），通过 `JSON.parse()`解析出包描述对象，从中取出 main 属性指定的文件名进行定位。如果文件名缺少扩展名，将会进入扩展名分析的步骤。

而如果 main 属性指定的文件名错误，或者压根没有 package.json 文件，Node 会将 index 当做默认文件名，然后依次查找 index.js、index.json、index.node。

如果在目录分析的过程中没有定位成功任何文件，则自定义模块进入下一个模块路径进行查找。如果模块路径数组都被遍历完毕，依然没有查找到目标文件，则会抛出查找失败的异常。

### 2.2.3 模块编译

在 Node 中，每个文件模块都是一个对象，它的定义如下：

```js
function Module(id, parent) {
  this.id = id;
  this.exports = {};
  this.parent = parent;
  if (parent && parent.children) {
    parent.children.push(this);
  }
  this.filename = null;
  this.loaded = false;
  this.children = [];
}
```

编译和执行是引入文件模块的最后一个阶段。定位到具体的文件后，Node 会新建一个模块对象，然后根据路径载入并编译。对于不同的文件扩展名，其载入方法也有所不同，具体如下所示。

- `.js` 文件。通过 fs 模块同步读取文件后编译执行。
- `.node` 文件。这是用 C/C++编写的扩展文件，通过 `dlopen()`方法加载最后编译生成的文件。
- `.json` 文件。通过 fs 模块同步读取文件后，用 `JSON.parse()`解析返回结果。
- 其余扩展名文件。它们都被当做`.js` 文件载入。

每一个编译成功的模块都会将其文件路径作为索引缓存在 `Module._cache` 对象上，以提高二次引入的性能。

根据不同的文件扩展名，Node 会调用不同的读取方式，如`.json` 文件的调用如下：

```js
// Native extension for .json
Module._extensions[".json"] = function (module, filename) {
  var content = NativeModule.require("fs").readFileSync(filename, "utf8");
  try {
    module.exports = JSON.parse(stripBOM(content));
  } catch (err) {
    err.message = filename + ": " + err.message;
    throw err;
  }
};
```

其中，`Module._extensions` 会被赋值给 `require()`的 extensions 属性，所以通过在代码中访问 `require.extensions` 可以知道系统中已有的扩展加载方式。编写如下代码测试一下：

```js
console.log(require.extensions);
```

得到的执行结果如下：

```js
{ '.js': [Function], '.json': [Function], '.node': [Function] }
```

如果想对自定义的扩展名进行特殊的加载，可以通过类似 `require.extensions['.ext']`的方式实现。早期的 CoffeeScript 文件就是通过添加 `require.extensions['.coffee']`扩展的方式来实现加载的。但是从 v0.10.6 版本开始，官方不鼓励通过这种方式来进行自定义扩展名的加载，而是期望先将其他语言或文件编译成 JavaScript 文件后再加载，这样做的好处在于不将烦琐的编译加载等过程引入 Node 的执行过程中。

在确定文件的扩展名之后，Node 将调用具体的编译方式来将文件执行后返回给调用者。

1. JavaScript 模块的编译

回到 CommonJS 模块规范，我们知道每个模块文件中存在着 require、exports、module 这 3 个变量，但是它们在模块文件中并没有定义，那么从何而来呢？甚至在 Node 的 API 文档中，我们知道每个模块中还有 `__filename`、`__dirname` 这两个变量的存在，它们又是从何而来的呢？如果我们把直接定义模块的过程放诸在浏览器端，会存在污染全局变量的情况。

事实上，在编译的过程中，Node 对获取的 JavaScript 文件内容进行了头尾包装。在头部添加了`(function (exports, require, module,filename, dirname) {\n`，在尾部添加了`\n});`。一个正常的 JavaScript 文件会被包装成如下的样子：

```js
(function (exports, require, module, __filename, __dirname) {
  var math = require("math");
  exports.area = function (radius) {
    return Math.PI * radius * radius;
  };
});
```

这样每个模块文件之间都进行了作用域隔离。包装之后的代码会通过 vm 原生模块的 `runInThisContext()`方法执行（类似 eval，只是具有明确上下文，不污染全局），返回一个具体的 function 对象。最后，将当前模块对象的 exports 属性、`require()`方法、module（模块对象自身），以及在文件定位中得到的完整文件路径和文件目录作为参数传递给这个 `function()`执行。

这就是这些变量并没有定义在每个模块文件中却存在的原因。在执行之后，模块的 exports 属性被返回给了调用方。exports 属性上的任何方法和属性都可以被外部调用到，但是模块中的其余变量或属性则不可直接被调用。

至此，require、exports、module 的流程已经完整，这就是 Node 对 CommonJS 模块规范的实现。

此外，许多初学者都曾经纠结过为何存在 exports 的情况下，还存在 `module.exports`。理想情况下，只要赋值给 exports 即可：

```js
exports = function () {
  // My Class
};
```

但是通常都会得到一个失败的结果。其原因在于，exports 对象是通过形参的方式传入的，直接赋值形参会改变形参的引用，但并不能改变作用域外的值。测试代码如下：

```js
var change = function (a) {
  a = 100;
  console.log(a); // => 100
};
var a = 10;
change(a);
console.log(a); // => 10
```

如果要达到 require 引入一个类的效果，请赋值给 `module.exports` 对象。这个迂回的方案不改变形参的引用。

2. C/C++模块的编译

Node 调用 `process.dlopen()`方法进行加载和执行。在 Node 的架构下，`dlopen()`方法在 Windows 和 `*nix` 平台下分别有不同的实现，通过 libuv 兼容层进行了封装。

实际上，`.node` 的模块文件并不需要编译，因为它是编写 C/C++模块之后编译生成的，所以这里只有加载和执行的过程。在执行的过程中，模块的 exports 对象与`.node` 模块产生联系，然后返回给调用者。

C/C++模块给 Node 使用者带来的优势主要是执行效率方面的，劣势则是 C/C++模块的编写门槛比 JavaScript 高。

3. JSON 文件的编译

`.json` 文件的编译是 3 种编译方式中最简单的。Node 利用 fs 模块同步读取 JSON 文件的内容之后，调用 `JSON.parse()`方法得到对象，然后将它赋给模块对象的 exports，以供外部调用。

JSON 文件在用作项目的配置文件时比较有用。如果你定义了一个 JSON 文件作为配置，那就不必调用 fs 模块去异步读取和解析，直接调用 `require()`引入即可。此外，你还可以享受到模块缓存的便利，并且二次引入时也没有性能影响。

这里我们提到的模块编译都是指文件模块，即用户自己编写的模块。在下一节中，我们将展开介绍核心模块中的 JavaScript 模块和 C/C++模块。

## 2.3 核心模块

前面提到，Node 的核心模块在编译成可执行文件的过程中被编译进了二进制文件。核心模块其实分为 C/C++编写的和 JavaScript 编写的两部分，其中 C/C++文件存放在 Node 项目的 src 目录下，JavaScript 文件存放在 lib 目录下。

### 2.3.1 JavaScript 核心模块的编译过程

在编译所有 C/C++文件之前，编译程序需要将所有的 JavaScript 模块文件编译为 C/C++代码，此时是否直接将其编译为可执行代码了呢？其实不是。

1. 转存为 C/C++代码

Node 采用了 V8 附带的 js2c.py 工具，将所有内置的 JavaScript 代码（src/node.js 和 `lib/*.js`）转换成 C++里的数组，生成 node_natives.h 头文件，相关代码如下：

```c#
namespace node {
  const char node_native[] = { 47, 47, ..};
  const char dgram_native[] = { 47, 47, ..};
  const char console_native[] = { 47, 47, ..};
  const char buffer_native[] = { 47, 47, ..};
  const char querystring_native[] = { 47, 47, ..};
  const char punycode_native[] = { 47, 42, ..};
  // ...
  struct _native {
    const char* name;
    const char* source;
    size_t source_len;
  };
  static const struct _native natives[] = {
    { "node", node_native, sizeof(node_native)-1 },
    { "dgram", dgram_native, sizeof(dgram_native)-1 },
    // ...
  };
}
```

在这个过程中，JavaScript 代码以字符串的形式存储在 node 命名空间中，是不可直接执行的。在启动 Node 进程时，JavaScript 代码直接加载进内存中。在加载的过程中，JavaScript 核心模块经历标识符分析后直接定位到内存中，比普通的文件模块从磁盘中一处一处查找要快很多。

2. 编译 JavaScript 核心模块

lib 目录下的所有模块文件也没有定义 require、module、exports 这些变量。在引入 JavaScript 核心模块的过程中，也经历了头尾包装的过程，然后才执行和导出了 exports 对象。与文件模块有区别的地方在于：获取源代码的方式（核心模块是从内存中加载的）以及缓存执行结果的位置。

JavaScript 核心模块的定义如下面的代码所示，源文件通过 `process.binding('natives')`取出，编译成功的模块缓存到 `NativeModule._cache` 对象上，文件模块则缓存到 `Module._cache` 对象上：

```js
function NativeModule(id) {
  this.filename = id + ".js";
  this.id = id;
  this.exports = {};
  this.loaded = false;
}
NativeModule._source = process.binding("natives");
NativeModule._cache = {};
```

### 2.3.2 C/C++核心模块的编译过程

在核心模块中，有些模块全部由 C/C++编写，有些模块则由 C/C++完成核心部分，其他部分则由 JavaScript 实现包装或向外导出，以满足性能需求。后面这种 C++模块主内完成核心，JavaScript 主外实现封装的模式是 Node 能够提高性能的常见方式。通常，脚本语言的开发速度优于静态语言，但是其性能则弱于静态语言。而 Node 的这种复合模式可以在开发速度和性能之间找到平衡点。

这里我们将那些由纯 C/C++编写的部分统一称为内建模块，因为它们通常不被用户直接调用。Node 的 buffer、crypto、evals、fs、os 等模块都是部分通过 C/C++编写的。

1. 内建模块的组织形式

在 Node 中，内建模块的内部结构定义如下：

```c#
struct node_module_struct {
  int version;
  void *dso_handle;
  const char *filename;
  void (*register_func) (v8::Handle<v8::Object> target);
  const char *modname;
};
```

每一个内建模块在定义之后，都通过 NODE_MODULE 宏将模块定义到 node 命名空间中，模块的具体初始化方法挂载为结构的 register_func 成员：

```c#
#define NODE_MODULE(modname, regfunc)  \
  extern "C" {  \
    NODE_MODULE_EXPORT node::node_module_struct modname ## _module =  \
    {  \
      NODE_STANDARD_MODULE_STUFF,  \
      regfunc,  \
      NODE_STRINGIFY(modname)  \
    };  \
  }
```

node_extensions.h 文件将这些散列的内建模块统一放进了一个叫 node_module_list 的数组中，这些模块有：

- node_buffer
- node_crypto
- node_evals
- node_fs
- node_http_parser
- node_os
- node_zlib
- node_timer_wrap
- node_tcp_wrap
- node_udp_wrap
- node_pipe_wrap
- node_cares_wrap
- node_tty_wrap
- node_process_wrap
- node_fs_event_wrap
- node_signal_watcher

这些内建模块的取出也十分简单。Node 提供了 `get_builtin_module()`方法从 node_module_list 数组中取出这些模块。

内建模块的优势在于：首先，它们本身由 C/C++编写，性能上优于脚本语言；其次，在进行文件编译时，它们被编译进二进制文件。一旦 Node 开始执行，它们被直接加载进内存中，无须再次做标识符定位、文件定位、编译等过程，直接就可执行。

2. 内建模块的导出

在 Node 的所有模块类型中，存在着如图 2-4 所示的一种依赖层级关系，即文件模块可能会依赖核心模块，核心模块可能会依赖内建模块。

图 2-4 依赖层级关系

通常，不推荐文件模块直接调用内建模块。如需调用，直接调用核心模块即可，因为核心模块中基本都封装了内建模块。那么内建模块是如何将内部变量或方法导出，以供外部 JavaScript 核心模块调用的呢？

Node 在启动时，会生成一个全局变量 process，并提供 `Binding()`方法来协助加载内建模块。`Binding()`的实现代码在 src/node.cc 中，具体如下所示：

```c#
static Handle < Value > Binding(const Arguments & args) {
  HandleScope scope;
  Local < String > module = args[0] - > ToString();
  String::Utf8Value module * v(module);
  node_module_struct * modp;
  if(binding * cache.IsEmpty()) {
    binding_cache = Persistent < Object > ::New(Object::New());
  }
  Local < Object > exports;
  if(binding_cache - > Has(module)) {
    exports = binding_cache - > Get(module) - > ToObject();
    return scope.Close(exports);
  }
  // Append a string to process.moduleLoadList
  char buf[1024];
  snprintf(buf, 1024, "Binding %s", * module * v);
  uint32_t l = module_load_list - > Length();
  module_load_list - > Set(l, String::New(buf));
  if((modp = get_builtin_module( * module * v)) != NULL) {
    exports = Object::New();
    modp - > register_func(exports);
    binding_cache - > Set(module, exports);
  } else if(!strcmp(\_module_v, "constants")) {
    exports = Object::New();
    DefineConstants(exports);
    binding_cache - > Set(module, exports);#
    ifdef * * POSIX * *
  } else if(!strcmp(\_module_v, "io_watcher")) {
    exports = Object::New();
    IOWatcher::Initialize(exports);
    binding_cache - > Set(module, exports);#
    endif
  } else if(!strcmp(\_module_v, "natives")) {
    exports = Object::New();
    DefineJavaScript(exports);
    binding_cache - > Set(module, exports);
  } else {
    return ThrowException(Exception::Error(String::New("No such module")));
  }
  return scope.Close(exports);
}
```

在加载内建模块时，我们先创建一个 exports 空对象，然后调用 `get_builtin_module()`方法取出内建模块对象，通过执行 `register_func()`填充 exports 对象，最后将 exports 对象按模块名缓存，并返回给调用方完成导出。

这个方法不仅可以导出内建方法，还能导出一些别的内容。前面提到的 JavaScript 核心文件被转换为 C/C++数组存储后，便是通过 `process.binding('natives')`取出放置在 `NativeModule._source` 中的：

```js
NativeModule._source = process.binding("natives");
```

该方法将通过 js2c.py 工具转换出的字符串数组取出，然后重新转换为普通字符串，以对 JavaScript 核心模块进行编译和执行。

### 2.3.3 核心模块的引入流程

前面讲述了核心模块的原理，也解释了核心模块的引入速度为何是最快的。

从图 2-5 所示的 os 原生模块的引入流程可以看到，为了符合 CommonJS 模块规范，从 JavaScript 到 C/C++的过程是相当复杂的，它要经历 C/C++层面的内建模块定义、（JavaScript）核心模块的定义和引入以及（JavaScript）文件模块层面的引入。但是对于用户而言，`require()`十分简洁、友好。

图 2-5 os 原生模块的引入流程

### 2.3.4 编写核心模块

核心模块被编译进二进制文件需要遵循一定规则。作为 Node 的使用者，尽管几乎没有机会参与核心模块的开发，但是了解如何开发核心模块有助于我们更加深入地了解 Node。

核心模块中的 JavaScript 部分几乎与文件模块的开发相同，遵循 CommonJS 模块规范，上下文中除了拥有 require、module、exports 外，还可以调用 Node 中的一些全局变量，这里不做描述。

下面我们以 C/C++模块为例演示如何编写内建模块。为了便于理解，我们先编写一个极其简单的 JavaScript 版本的原型，这个方法返回一个 `Helloworld！`字符串：

```js
exports.sayHello = function () {
  return "Hello world!";
};
```

编写内建模块通常分两步完成：编写头文件和编写 C/C++文件。

(1) 将以下代码保存为 node_hello.h，存放到 Node 的 src 目录下：

```c
#ifndef NODE_HELLO_H_
#define NODE_HELLO_H_
#include <v8.h>
namespace node {
  // 定义方法
  v8::Handle<v8::Value> SayHello(const v8::Arguments& args);
}
#endif
```

(2) 编写 node_hello.cc，并存储到 src 目录下：

```c#
#include <node.h>
#include <node_hello.h>
#include <v8.h>
namespace node {
	using namespace v8;
	//实现定义的方法
	Handle<Value> SayHello(const Arguments& args) {
		HandleScope scope;
		return scope.Close(String::New("Hello world!"));
	}
	//给传入的目对象加 sayHello 方法
	void Init_Hello(Handle<Object> target) {
		target->Set(String::NewSymbol("sayHello"), FunctionTemplate::New(SayHello)->GetFunction());
	}
}
//调用 NODE_MODULE()将注方法定义内存中
NODE_MODULE(node_hello, node::Init_Hello)
```

以上两步完成了内建模块的编写，但是真正要让 Node 认为它是内建模块，还需要更改 src/node_extensions.h，在 NODE_EXT_LIST_END 前添加 `NODE_EXT_LIST_ITEM(node_hello)`，以将 node_hello 模块添加进 node_module_list 数组中。

其次，还需要让编写的两份代码编译进执行文件，同时需要更改 Node 的项目生成文件 node.gyp，并在`'target_name': 'node'`节点的 sources 中添加上新编写的两个文件。然后编译整个 Node 项目，具体的编译步骤请参见附录 A。

编译和安装后，直接在命令行中运行以下代码，将会得到期望的效果：

```shell
$ node
> var hello = process.binding('hello');
undefined
> hello.sayHello();
'Hello world!'
>
```

至此，原生编写过程中需要注意的细节都已表述过了。可以看出，简单的模块通过 JavaScript 来编写可以大大提高生产效率。这里我们写作本节的目的是希望有能力的读者可以深入 Node 的核心模块，去学习它或者改进它。

## 2.4 C/C++扩展模块

对于前端工程师来说，C/C++扩展模块或许比较生疏和晦涩，但是如果你了解了它，在模块出现性能瓶颈时将会对你有极大的帮助。

JavaScript 的一个典型弱点就是位运算。JavaScript 的位运算参照 Java 的位运算实现，但是 Java 位运算是在 int 型数字的基础上进行的，而 JavaScript 中只有 double 型的数据类型，在进行位运算的过程中，需要将 double 型转换为 int 型，然后再进行。所以，在 JavaScript 层面上做位运算的效率不高。

在应用中，会频繁出现位运算的需求，包括转码、编码等过程，如果通过 JavaScript 来实现，CPU 资源将会耗费很多，这时编写 C/C++扩展模块来提升性能的机会来了。

C/C++扩展模块属于文件模块中的一类。前面讲述文件模块的编译部分时提到，C/C++模块通过预先编译为`.node` 文件，然后调用 `process.dlopen()`方法加载执行。在这一节中，我们将分析整个 C/C++扩展模块的编写、编译、加载、导出的过程。

在开始编写扩展模块之前，需要强调的一点是，Node 的原生模块一定程度上是可以跨平台的，其前提条件是源代码可以支持在`*nix` 和 Windows 上编译，其中`*nix` 下通过 g++/gcc 等编译器编译为动态链接共享对象文件（.so），在 Windows 下则需要通过 Visual C++的编译器编译为动态链接库文件（.dll），如图 2-6 所示。这里有一个让人迷惑的地方，那就是引用加载时却是`.node` 文件。其实`.node` 的扩展名只是为了看起来更自然一点，不会因为平台差异产生不同的感觉。实际上，在 Windows 下它是一个`.dll` 文件，在`*nix` 下则是一个`.so` 文件。为了实现跨平台，`dlopen()`方法在内部实现时区分了平台，分别用的是加载`.so` 和`.dll` 的方式。图 2-6 为扩展模块在不同平台上编译和加载的详细过程。

图 2-6 扩展模块不同平台上的编译和加载过程

值得注意的是，一个平台下的`.node` 文件在另一个平台下是无法加载执行的，必须重新用各自平台下的编译器编译为正确的`.node` 文件。

### 2.4.1 前提条件

如果想要编写高质量的 C/C++扩展模块，还需要深厚的 C/C++编程功底才行。除此之外，以下这些条目都是不能避开的，在了解它们之后，可以让你在编写过程中事半功倍。

1. GYP 项目生成工具。

在 Node 0.6 中，第三方模块通过它自身提供的 node_waf 工具实现编译，但是它是`*nix` 平台下的产物，无法实现跨平台编译。在 Node 0.8 中，Node 决定摒弃掉 node_waf 而采用跨平台效果更好的项目生成器，它就是 GYP 工具，即“Generate YourProjects”短句的缩写。它的好处在于，可以帮助你生成各个平台下的项目文件，比如 Windows 下的 Visual Studio 解决方案文件（.sln）、Mac 下的 XCode 项目配置文件以及 Scons 工具。在这个基础上，再动用各自平台下的编译器编译项目。这大大减少了跨平台模块在项目组织上的精力投入。

Node 源码中一度出现过各种项目文件，后来均统一为 GYP 工具。这除了可以减少编写跨平台项目文件的工作量外，另一个简单的原因就是 Node 自身的源码就是通过 GYP 编译的。为此，NathanRajlich 基于 GYP 为 Node 提供了一个专有的扩展构建工具 node-gyp，这个工具通过 `npm install -g node-gyp` 这个命令即可安装。

2. V8 引擎 C++库。

V8 是 Node 自身的动力来源之一。它自身由 C++写成，可以实现 JavaScript 与 C++的互相调用。

3. libuv 库。

它是 Node 自身的动力来源之二。Node 能够实现跨平台的一个诀窍就是它的 libuv 库，这个库是跨平台的一层封装，通过它去调用一些底层操作，比自己在各个平台下编写实现要高效得多。libuv 封装的功能包括事件循环、文件操作等。

4. Node 内部库。

写 C++模块时，免不了要做一些面向对象的编程工作，而 Node 自身提供了一些 C++代码，比如 `node::ObjectWrap` 类可以用来包装你的自定义类，它可以帮助实现对象回收等工作。

5. 其他库。其他存在 deps 目录下的库在编写扩展模块时也许可以帮助你，比如 zlib、openssl、http_parser 等。

### 2.4.2 C/C++扩展模块的编写

在介绍 C/C++内建模块时，其实已经介绍了 C/C++模块的编写方式。普通的扩展模块与内建模块的区别在于无须将源代码编译进 Node，而是通过 `dlopen()`方法动态加载。所以在编写普通的扩展模块时，无须将源代码写进 node 命名空间，也不需要提供头文件。下面我们将采用同一个例子来介绍 C/C++扩展模块的编写。

它的 JavaScript 原型代码与前面的例子一样：

```js
exports.sayHello = function () {
  return "Hello world!";
};
```

新建 hello 目录作为自己的项目位置，编写 hello.cc 并将其存储到 src 目录下，相关代码如下：

```c#
#include <node.h>
#include <v8.h>
using namespace v8;
//实现定义的方法
Handle<Value> SayHello(const Arguments& args) {
	HandleScope scope;
	return scope.Close(String::New("Hello world!"));
}
//给传入的目对象加
sayHello()方法 void Init_Hello(Handle<Object> target) {
	target->Set(String::NewSymbol("sayHello"), FunctionTemplate::New(SayHello)->GetFunction());
}
//调用 NODE_MODULE()方法将注方法定义内存中
NODE_MODULE(hello, Init_Hello)
```

C/C++扩展模块与内建模块的套路一样，将方法挂载在 target 对象上，然后通过 NODE_MODULE 声明即可。

由于不像编写内建模块那样将对象声明到 node_module_list 链表中，所以无法被认作是一个原生模块，只能通过 `dlopen()`来动态加载，然后导出给 JavaScript 调用。

### 2.4.3 C/C++扩展模块的编译

在 GYP 工具的帮助下，C/C++扩展模块的编译是一件省心的事情，无须为每个平台编写不同的项目编译文件。写好`.gyp` 项目文件是除编码外的头等大事，然而你也无须担心此事太难，因为`.gyp` 项目文件是足够简单的。node-gyp 约定`.gyp` 文件为 binding.gyp，其内容如下所示：

```js
{ 'targets': [
{ 'target_name': 'hello', 'sources': [
'src/hello.cc' ], 'conditions': [
['OS == "win"', {
'libraries': ['-lnode.lib'] } ]
] } ] }
```

然后调用：

```
$ node-gyp configure
```

会得到如下的输出结果：

```
gyp info it worked if it ends with ok
gyp info using node-gyp@0.8.3
gyp info using node@0.8.14 | darwin | x64
gyp info spawn python
gyp info spawn args [ '/usr/local/lib/node_modules/node-gyp/gyp/gyp',
gyp info spawn args 'binding.gyp',
gyp info spawn args '-f',
gyp info spawn args 'make',
gyp info spawn args '-I',
gyp info spawn args '/Users/jacksontian/git/diveintonode/examples/02/addon/build/config.gypi',
gyp info spawn args '-I',
gyp info spawn args '/usr/local/lib/node_modules/node-gyp/addon.gypi',
gyp info spawn args '-I',
gyp info spawn args '/Users/jacksontian/.node-gyp/0.8.14/common.gypi',
gyp info spawn args '-Dlibrary=shared_library',
gyp info spawn args '-Dvisibility=default',
gyp info spawn args '-Dnode_root_dir=/Users/jacksontian/.node-gyp/0.8.14',
gyp info spawn args '-Dmodule_root_dir=/Users/jacksontian/git/diveintonode/examples/02/addon',
gyp info spawn args '--depth=.',
gyp info spawn args '--generator-output',
gyp info spawn args 'build',
gyp info spawn args '-Goutput_dir=.' ]
gyp info ok
```

`node-gyp configure` 这个命令会在当前目录中创建 build 目录，并生成系统相关的项目文件。

在`*nix` 平台下，build 目录中会出现 Makefile 等文件；在 Windows 下，则会生成 vcxproj 等文件。

继续执行如下代码：

```shell
$ node-gyp build
```

会得到如下的输出结果：

```
gyp info it worked if it ends with ok
gyp info using node-gyp@0.8.3
gyp info using node@0.8.14 | darwin | x64
gyp info spawn make
gyp info spawn args [ 'BUILDTYPE=Release', '-C', 'build' ]
CXX(target) Release/obj.target/hello/hello.o
SOLINK_MODULE(target) Release/hello.node
SOLINK_MODULE(target) Release/hello.node: Finished
gyp info ok
```

编译过程会根据平台不同，分别通过 make 或 vcbuild 进行编译。编译完成后，hello.node 文件会生成在 build/Release 目录下。

### 2.4.4 C/C++扩展模块的加载

得到 hello.node 结果文件后，如何调用扩展模块其实在前面已经提及。`require()`方法通过解析标识符、路径分析、文件定位，然后加载执行即可。下面的代码引入前面编译得到的`.node` 文件，并调用执行其中的方法：

```js
var hello = require("./build/Release/hello.node");
console.log(hello.sayHello());
```

以上代码存为 hello.js，调用 `node hello.js` 命令即可得到如下的输出结果：

```
Hello world!
```

对于以`.node` 为扩展名的文件，Node 将会调用 `process.dlopen()`方法去加载文件：

```js
//Native extension for .node
Module._extensions[".node"] = process.dlopen;
```

对于调用者而言，`require()`是轻松愉快的。对于扩展模块的编写者来说，`process.dlopen()`中隐含的过程值得了解一番。

如图 2-7 所示，`require()`在引入`.node` 文件的过程中，实际上经历了 4 个层面上的调用。

图 2-7 `require()`引入`.node` 文件的过程

加载`.node` 文件实际上经历了两个步骤，第一个步骤是调用 `uv_dlopen()`方法去打开动态链接库，第二个步骤是调用 `uv_dlsym()`方法找到动态链接库中通过 NODE_MODULE 宏定义的方法地址。这两个过程都是通过 libuv 库进行封装的：在`*nix` 平台下实际上调用的是 dlfcn.h 头文件中定义的 dlopen()和 dlsym()两个方法；在 Windows 平台则是通过 `LoadLibraryExW()`和 `GetProcAddress()`这两个方法实现的，它们分别加载`.so` 和`.dll` 文件（实际为`.node` 文件）。

这里对 libuv 函数的调用充分表现 Node 利用 libuv 实现跨平台的方式，这样的情景在很多地方还会出现。

由于编写模块时通过 NODE_MODULE 将模块定义为 node_module_struct 结构，所以在获取函数地址之后，将它映射为 node_module_struct 结构几乎是无缝对接的。接下来的过程就是将传入的 exports 对象作为实参运行，将 C++中定义的方法挂载在 exports 对象上，然后调用者就可以轻松调用了。

C/C++扩展模块与 JavaScript 模块的区别在于加载之后不需要编译，直接执行之后就可以被外部调用了，其加载速度比 JavaScript 模块略快。

使用 C/C++扩展模块的一个好处在于可以更灵活和动态地加载它们，保持 Node 模块自身简单性的同时，给予 Node 无限的可扩展性。

关于 node-gyp 工具的更多细节可以参见https://github.com/TooTallNate/node-gyp（作者为Nathan Rajlich, Node 源码的核心贡献者之一）。

## 2.5 模块调用栈

结束文件模块、核心模块、内建模块、C/C++扩展模块等的阐述之后，有必要明确一下各种模块之间的调用关系，如图 2-8 所示。

图 2-8 模块之间的调用关系

C/C++内建模块属于最底层的模块，它属于核心模块，主要提供 API 给 JavaScript 核心模块和第三方 JavaScript 文件模块调用。如果你不是非常了解要调用的 C/C++内建模块，请尽量避免通过 `process.binding()`方法直接调用，这是不推荐的。

JavaScript 核心模块主要扮演的职责有两类：一类是作为 C/C++内建模块的封装层和桥接层，供文件模块调用；一类是纯粹的功能模块，它不需要跟底层打交道，但是又十分重要。

文件模块通常由第三方编写，包括普通 JavaScript 模块和 C/C++扩展模块，主要调用方向为普通 JavaScript 模块调用扩展模块。

## 2.6 包与 NPM

Node 组织了自身的核心模块，也使得第三方文件模块可以有序地编写和使用。但是在第三方模块中，模块与模块之间仍然是散列在各地的，相互之间不能直接引用。而在模块之外，包和 NPM 则是将模块联系起来的一种机制。

在介绍 NPM 之前，不得不提起 CommonJS 的包规范。JavaScript 不似 Java 或者其他语言那样，具有模块和包结构。Node 对模块规范的实现，一定程度上解决了变量依赖、依赖关系等代码组织性问题。包的出现，则是在模块的基础上进一步组织 JavaScript 代码。图 2-9 为包组织模块示意图。

图 2-9 包组织模块示意图

CommonJS 的包规范的定义其实也十分简单，它由包结构和包描述文件两个部分组成，前者用于组织包中的各种文件，后者则用于描述包的相关信息，以供外部读取分析。

### 2.6.1 包结构

包实际上是一个存档文件，即一个目录直接打包为.zip 或 tar.gz 格式的文件，安装后解压还原为目录。完全符合 CommonJS 规范的包目录应该包含如下这些文件。

- package.json：包描述文件。
- bin：用于存放可执行二进制文件的目录。
- lib：用于存放 JavaScript 代码的目录。
- doc：用于存放文档的目录。
- test：用于存放单元测试用例的代码。

可以看到，CommonJS 包规范从文档、测试等方面都做过考虑。当一个包完成后向外公布时，用户看到单元测试和文档的时候，会给他们一种踏实可靠的感觉。

### 2.6.2 包描述文件与 NPM

包描述文件用于表达非代码相关的信息，它是一个 JSON 格式的文件——package.json，位于包的根目录下，是包的重要组成部分。而 NPM 的所有行为都与包描述文件的字段息息相关。由于 CommonJS 包规范尚处于草案阶段，NPM 在实践中做了一定的取舍，具体细节在后面会介绍到。

CommonJS 为 package.json 文件定义了如下一些必需的字段。

- name。包名。规范定义它需要由小写的字母和数字组成，可以包含`.`、`_`和`-`，但不允许出现空格。包名必须是唯一的，以免对外公布时产生重名冲突的误解。除此之外，NPM 还建议不要在包名中附带上 node 或 js 来重复标识它是 JavaScript 或 Node 模块。
- description。包简介。
- version。版本号。一个语义化的版本号，这在 http://semver.org/ 上有详细定义，通常为 major.minor.revision 格式。该版本号十分重要，常常用于一些版本控制的场合。
- keywords。关键词数组，NPM 中主要用来做分类搜索。一个好的关键词数组有利于用户快速找到你编写的包。
- maintainers。包维护者列表。每个维护者由 name、email 和 web 这 3 个属性组成。示例如下：`"maintainers": [{ "name": "JacksonTian", "email": "shyvo1987@gmail.com","web": "http://html5ify.com" }]`NPM 通过该属性进行权限认证。
- contributors。贡献者列表。在开源社区中，为开源项目提供代码是经常出现的事情，如果名字能出现在知名项目的 contributors 列表中，是一件比较有荣誉感的事。列表中的第一个贡献应当是包的作者本人。它的格式与维护者列表相同。
- bugs。一个可以反馈 bug 的网页地址或邮件地址。
- licenses。当前包所使用的许可证列表，表示这个包可以在哪些许可证下使用。它的格式如下：`"licenses": [{ "type": "GPLv2", "url": "http://www.example.com/licenses/gpl.html", }]`
- repositories。托管源代码的位置列表，表明可以通过哪些方式和地址访问包的源代码。
- dependencies。使用当前包所需要依赖的包列表。这个属性十分重要，NPM 会通过这个属性帮助自动加载依赖的包。

除了必选字段外，规范还定义了一部分可选字段，具体如下所示。

- homepage。当前包的网站地址。
- os。操作系统支持列表。这些操作系统的取值包括 aix、freebsd、linux、macos、solaris、vxworks、windows。如果设置了列表为空，则不对操作系统做任何假设。
- cpu。CPU 架构的支持列表，有效的架构名称有 arm、mips、ppc、sparc、x86 和 x86_64。同 os 一样，如果列表为空，则不对 CPU 架构做任何假设。
- engine。支持的 JavaScript 引擎列表，有效的引擎取值包括 ejs、flusspferd、gpsee、jsc、spidermonkey、narwhal、node 和 v8。
- builtin。标志当前包是否是内建在底层系统的标准组件。
- directories。包目录说明。
- implements。实现规范的列表。标志当前包实现了 CommonJS 的哪些规范。
- scripts。脚本说明对象。它主要被包管理器用来安装、编译、测试和卸载包。示例如下：

```json
"scripts": { "install": "install.js",
"uninstall": "uninstall.js",
"build": "build.js",
"doc": "make-doc.js",
"test": "test.js" }
```

包规范的定义可以帮助 Node 解决依赖包安装的问题，而 NPM 正是基于该规范进行了实现。最初，NPM 工具是由 Isaac Z. Schlueter 单独创建，提供给 Node 服务的 Node 包管理器，需要单独安装。后来，在 v0.6.3 版本时集成进 Node 中作为默认包管理器，作为软件包的一部分一起安装。之后，Isaac Z. Schlueter 也成为 Node 的掌门人。

在包描述文件的规范中，NPM 实际需要的字段主要有 name、version、description、keywords、repositories、author、bin、main、scripts、engines、dependencies、devDependencies。

与包规范的区别在于多了 author、bin、main 和 devDependencies 这 4 个字段，下面补充说明一下。

- author。包作者。
- bin。一些包作者希望包可以作为命令行工具使用。配置好 bin 字段后，通过 `npm installpackage_name -g` 命令可以将脚本添加到执行路径中，之后可以在命令行中直接执行。前面的 node-gyp 即是这样安装的。通过`-g` 命令安装的模块包称为全局模式。
- main。模块引入方法 `require()`在引入包时，会优先检查这个字段，并将其作为包中其余模块的入口。如果不存在这个字段，`require()`方法会查找包目录下的 index.js、index.node、index.json 文件作为默认入口。
- devDependencies。一些模块只在开发时需要依赖。配置这个属性，可以提示包的后续开发者安装依赖包。

下面是知名框架 express 项目的 package.json 文件，具有一定的参考意义：

```json
{
  "name": "express",
  "description": "Sinatra inspired web development framework",
  "version": "3.3.4",
  "author": "TJ Holowaychuk <tj@vision-media.ca>",
  "contributors": [
    {
      "name": "TJ Holowaychuk",
      "email": "tj@vision-media.ca"
    },
    {
      "name": "Aaron Heckmann",
      "email": "aaron.heckmann+github@gmail.com"
    },
    {
      "name": "Ciaran Jessup",
      "email": "ciaranj@gmail.com"
    },
    {
      "name": "Guillermo Rauch",
      "email": "rauchg@gmail.com"
    }
  ],
  "dependencies": {
    "connect": "2.8.4",
    "commander": "1.2.0",
    "range-parser": "0.0.4",
    "mkdirp": "0.3.5",
    "cookie": "0.1.0",
    "buffer-crc32": "0.2.1",
    "fresh": "0.1.0",
    "methods": "0.0.1",
    "send": "0.1.3",
    "cookie-signature": "1.0.1",
    "debug": "*"
  },
  "devDependencies": {
    "ejs": "*",
    "mocha": "*",
    "jade": "0.30.0",
    "hjs": "*",
    "stylus": "*",
    "should": "*",
    "connect-redis": "*",
    "marked": "*",
    "supertest": "0.6.0"
  },
  "keywords": [
    "express",
    "framework",
    "sinatra",
    "web",
    "rest",
    "restful",
    "router",
    "app",
    "api"
  ],
  "repository": "git://github.com/visionmedia/express",
  "main": "index",
  "bin": {
    "express": "./bin/express"
  },
  "scripts": {
    "prepublish": "npm prune",
    "test": "make test"
  },
  "engines": {
    "node": "*"
  }
}
```

### 2.6.3 NPM 常用功能

CommonJS 包规范是理论，NPM 是其中的一种实践。NPM 之于 Node，相当于 gem 之于 Ruby,pear 之于 PHP。对于 Node 而言，NPM 帮助完成了第三方模块的发布、安装和依赖等。借助 NPM,Node 与第三方模块之间形成了很好的一个生态系统。

借助 NPM，可以帮助用户快速安装和管理依赖包。除此之外，NPM 还有一些巧妙的用法，下面我们详细介绍一下。

1. 查看帮助

在安装 Node 之后，执行 `npm -v` 命令可以查看当前 NPM 的版本：

```
$ npm -v
1.2.32
```

在不熟悉 NPM 的命令之前，可以直接执行 NPM 查看到帮助引导说明：

```
$ npm
Usage: npm <command>
where <command> is one of:
add-user, adduser, apihelp, author, bin, bugs, c, cache,
completion, config, ddp, dedupe, deprecate, docs, edit,
explore, faq, find, find-dupes, get, help, help-search,
home, i, info, init, install, isntall, issues, la, link,
list, ll, ln, login, ls, outdated, owner, pack, prefix,
prune, publish, r, rb, rebuild, remove, restart, rm, root,
run-script, s, se, search, set, show, shrinkwrap, star,
stars, start, stop, submodule, tag, test, tst, un,
uninstall, unlink, unpublish, unstar, up, update, version,
view, whoami
npm <cmd> -h quick help on <cmd>
npm -l display full usage info
npm faq commonly asked questions
npm help <term> search for help on <term>
npm help npm involved overview
Specify configs in the ini-formatted file:
/Users/jacksontian/.npmrc
or on the command line via: npm <command> --key value
Config info can be viewed via: npm help config
npm@1.2.32 /usr/local/lib/node_modules/npm
```

可以看到，帮助中列出了所有的命令，其中 `npm help <command>`可以查看具体的命令说明。

2. 安装依赖包

安装依赖包是 NPM 最常见的用法，它的执行语句是 `npm install express`。执行该命令后，NPM 会在当前目录下创建 node_modules 目录，然后在 node_modules 目录下创建 express 目录，接着将包解压到这个目录下。

安装好依赖包后，直接在代码中调用 `require('express');` 即可引入该包。`require()`方法在做路径分析的时候会通过模块路径查找到 express 所在的位置。模块引入和包的安装这两个步骤是相辅相承的。

**全局模式安装**

如果包中含有命令行工具，那么需要执行 `npm install express -g` 命令进行全局模式安装。需要注意的是，全局模式并不是将一个模块包安装为一个全局包的意思，它并不意味着可以从任何地方通过 `require()`来引用到它。

全局模式这个称谓其实并不精确，存在诸多误导。实际上，`-g` 是将一个包安装为全局可用的可执行命令。它根据包描述文件中的 bin 字段配置，将实际脚本链接到与 Node 可执行文件相同的路径下：

```js
"bin": {
"express": "./bin/express"
},
```

事实上，通过全局模式安装的所有模块包都被安装进了一个统一的目录下，这个目录可以通过如下方式推算出来：

```js
path.resolve(process.execPath, "..", "..", "lib", "node_modules");
```

如果 Node 可执行文件的位置是/usr/local/bin/node，那么模块目录就是/usr/local/lib/node_modules。最后，通过软链接的方式将 bin 字段配置的可执行文件链接到 Node 的可执行目录下。

**从本地安装**

对于一些没有发布到 NPM 上的包，或是因为网络原因导致无法直接安装的包，可以通过将包下载到本地，然后以本地安装。本地安装只需为 NPM 指明 package.json 文件所在的位置即可：它可以是一个包含 package.json 的存档文件，也可以是一个 URL 地址，也可以是一个目录下有 package.json 文件的目录位置。具体参数如下：

```
npm install <tarball file>
npm install <tarball url>
npm install <folder>
```

**从非官方源安装**

如果不能通过官方源安装，可以通过镜像源安装。在执行命令时，添加 `--registry=http://registry.url` 即可，示例如下：

```
npm install underscore --registry=http://registry.url
```

如果使用过程中几乎都采用镜像源安装，可以执行以下命令指定默认源：

```
npm config set registry http://registry.url
```

3. NPM 钩子命令

另一个需要说明的是 C/C++模块实际上是编译后才能使用的。package.json 中 scripts 字段的提出就是让包在安装或者卸载等过程中提供钩子机制，示例如下：

```json
"scripts": {
"preinstall": "preinstall.js",
"install": "install.js",
"uninstall": "uninstall.js",
"test": "test.js"
}
```

在以上字段中执行 `npm install <package>`时，preinstall 指向的脚本将会被加载执行，然后 install 指向的脚本会被执行。在执行 `npm uninstall <package>`时，uninstall 指向的脚本也许会做一些清理工作等。

当在一个具体的包目录下执行 `npm test` 时，将会运行 test 指向的脚本。一个优秀的包应当包含测试用例，并在 package.json 文件中配置好运行测试的命令，方便用户运行测试用例，以便检验包是否稳定可靠。

4. 发布包

为了将整个 NPM 的流程串联起来，这里将演示如何编写一个包，将其发布到 NPM 仓库中，并通过 NPM 安装回本地。

**编写模块**

模块的内容我们尽量保持简单，这里还是以 sayHello 作为例子，相关代码如下：

```js
exports.sayHello = function () {
  return "Hello, world.";
};
```

将这段代码保存为 hello.js 即可。

**初始化包描述文件**

package.json 文件的内容尽管相对较多，但是实际发布一个包时并不需要一行一行编写。NPM 提供的 npm init 命令会帮助你生成 package.json 文件，具体如下所示：

```
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.
See `npm help json` for definitive documentation on these fields
and exactly what they do.
Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.
Press ^C at any time to quit.
name: (module) hello_test_jackson
version: (0.0.0) 0.0.1
description: A hello world package
entry point: (hello.js) ./hello.js
test command:
git repository:
keywords: Hello world
author: Jackson Tian
license: (BSD) MIT
About to write to /Users/jacksontian/git/diveintonode/examples/03/module/package.json:
{
"name": "hello_test_jackson",
"version": "0.0.1",
"description": "A hello world package",
"main": "./hello.js",
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1"
},
"repository": "",
"keywords": [
"Hello",
"world"
],
"author": "Jackson Tian",
"license": "MIT"
}
Is this ok? (yes) yes
npm WARN package.json hello_test_jackson@0.0.1 No README.md file found!
```

NPM 通过提问式的交互逐个填入选项，最后生成预览的包描述文件。如果你满意，输入 yes，此时会在目录下得到 package.json 文件。

**注册包仓库账号**

为了维护包，NPM 必须要使用仓库账号才允许将包发布到仓库中。注册账号的命令是 npmadduser。这也是一个提问式的交互过程，按顺序进行即可：

```
$ npm adduser
Username: (jacksontian)
Email: (shyvo1987@gmail.com)
```

**上传包**

上传包的命令是 `npm publish <folder>`。在刚刚创建的 package.json 文件所在的目录下，执行 npm publish .开始上传包，相关代码如下：

```shell
$ npm publish .
npm http PUT http://registry.npmjs.org/hello_test_jackson
npm http 201 http://registry.npmjs.org/hello_test_jackson
npm http GET http://registry.npmjs.org/hello_test_jackson
npm http 200 http://registry.npmjs.org/hello_test_jackson
npm http PUT http://registry.npmjs.org/hello_test_jackson/0.0.1/-tag/latest
npm http 201 http://registry.npmjs.org/hello_test_jackson/0.0.1/-tag/latest
npm http GET http://registry.npmjs.org/hello_test_jackson
npm http 200 http://registry.npmjs.org/hello_test_jackson
npm http PUT http://registry.npmjs.org/hello_test_jackson/-/hello_test_jackson-0.0.1.tgz/-rev/2-2d64e0946b866878bb252f182070c1d5
npm http 201 http://registry.npmjs.org/hello_test_jackson/-/hello_test_jackson-0.0.1.tgz/-rev/2-2d64e0946b866878bb252f182070c1d5
+ hello_test_jackson@0.0.1
```

在这个过程中，NPM 会将目录打包为一个存档文件，然后上传到官方源仓库中。

**安装包**

为了体验和测试自己上传的包，可以换一个目录执行 `npm install hello_test_jackson` 安装它：

```
$ npm install hello_test_jackson --registry=http://registry.npmjs.org
npm http GET http://registry.npmjs.org/hello_test_jackson
npm http 200 http://registry.npmjs.org/hello_test_jackson
hello_test_jackson@0.0.1 ./node_modules/hello_test_jackson
```

**管理包权限**

通常，一个包只有一个人拥有权限进行发布。如果需要多人进行发布，可以使用 `npm owner` 命令帮助你管理包的所有者：

```
$ npm owner ls eventproxy
npm http GET https://registry.npmjs.org/eventproxy
npm http 200 https://registry.npmjs.org/eventproxy
jacksontian <shyvo1987@gmail.com>
```

使用这个命令，也可以添加包的拥有者，删除一个包的拥有者：

```
npm owner ls <package name>
npm owner add <user> <package name>
npm owner rm <user> <package name>
```

5. 分析包

在使用 NPM 的过程中，或许你不能确认当前目录下能否通过 `require()`顺利引入想要的包，这时可以执行 npm ls 分析包。

这个命令可以为你分析出当前路径下能够通过模块路径找到的所有包，并生成依赖树，如下：

```
$ npm ls
/Users/jacksontian
├─┬ connect@2.0.3
│ ├── crc@0.1.0
│ ├── debug@0.6.0
│ ├── formidable@1.0.9
│ ├── mime@1.2.4
│ └── qs@0.4.2
├── hello_test_jackson@0.0.1
└── urllib@0.2.3
```

### 2.6.4 局域 NPM

在企业的内部应用中使用 NPM 与开源社区中使用有一定的差别。企业的限制在于，一方面需要享受到模块开发带来的低耦合和项目组织上的好处，另一方面却要考虑到模块保密性的问题。所以，通过 NPM 共享和发布存在潜在的风险。

为了同时能够享受到 NPM 上众多的包，同时对自己的包进行保密和限制，现有的解决方案就是企业搭建自己的 NPM 仓库。

所幸，NPM 自身是开源的，无论是它的服务器端和客户端。通过源代码搭建自己的仓库并不是什么秘密。

局域 NPM 仓库的搭建方法与搭建镜像站（详情可参见附录 D）的方式几乎一样。

与镜像仓库不同的地方在于，企业局域 NPM 可以选择不同步官方源仓库中的包。图 2-10 为企业中混合使用官方仓库和局域仓库的示意图。

图 2-10 混合使用官方仓库和局域仓库的示意图

对于企业内部而言，私有的可重用模块可以打包到局域 NPM 仓库中，这样可以保持更新的中心化，不至于让各个小项目各自维护相同功能的模块，杜绝通过复制粘贴实现代码共享的行为。

### 2.6.5 NPM 潜在问题

作为为模块和包服务的工具，NPM 十分便捷。它实质上已经是一个包共享平台，所有人都可以贡献模块并将其打包分享到这个平台上，也可以在许可证（大多是 MIT 许可证）的允许下免费使用它们。NPM 提供的这些便捷，将模块链接到一个共享平台上，缩短了贡献者与使用者之间的距离，这十分有利于模块的传播，进而也十分利于 Node 的推广。几乎没有一种语言或平台有 Node 这样出现才 3 年多就拥有成千上万个第三方模块的情景。这个功劳一部分是因为 Node 选择了 JavaScript，这门语言拥有极大的开发人员基数，具有强大的生产力；另一部分则是因为 CommonJS 规范和 NPM，它们使得产品能够更好地组织、传播和使用。

潜在的问题在于，在 NPM 平台上，每个人都可以分享包到平台上，鉴于开发人员水平不一，上面的包的质量也良莠不齐。另一个问题则是，Node 代码可以运行在服务器端，需要考虑安全问题。

对于包的使用者而言，包质量和安全问题需要作为是否采纳模块的一个判断条件。

尽管 NPM 没有硬性的方式去评判一个包的质量和安全，好在开源社区也有它内在的健康发展机制，那就是口碑效应，其中 [NPM 模块首页](https://npmjs.org/)上的依赖榜可以说明模块的质量和可靠性。第二个可以考查质量的地方是 GitHub, NPM 中大多的包都是通过 GitHub 托管的，模块项目的观察者数量和分支数量也能从侧面反映这个模块的可靠性和流行度。第三个可以考量包质量的地方在于包中的测试用例和文档的状况，一个没有单元测试的包基本上是无法被信任的，没有文档的包，使用者使用时内心也是不踏实的。

在安全问题上，在经过模块质量的考查之后，应该可以去掉一大半候选包。基于使用者大多是 JavaScript 程序员，难点其实存在于第三方 C/C++扩展模块，这类模块建议在企业的安全部门检查之后方可允许使用。

事实上，为了解决上述问题，Isaac Z. Schlueter 计划引入 CPAN 社区中的 Kwalitee 风格来让模块进行自然排序。Kwalitee 是一个拟声词，发音与 quality 相同。CPAN 社区对它的原始定义如下：

“Kwalitee”is something that looks likequality, sounds like quality, but is not quitequality.

大致意思就是确认一个模块的质量是否优秀并不是那么容易，只能从一些表象来进行考查，但即便考查都通过，也并不能确定它就是高质量的模块。这个方法能够排除大部分不合格的模块，虽然不够精确但是有效。总体而言，符合 Kwalitee 的模块要满足的条件与上述提及的考查点大致相同。

- 具备良好的测试。
- 具备良好的文档（README、API）。
- 具备良好的测试覆盖率。
- 具备良好的编码规范。
- 更多条件。

CPAN 社区制定了相当多的规范来考查模块。未来，NPM 社区也会有更多的规范来考查模块。读者可以根据这些条款区分出那些优秀的模块和糟粕的模块。

## 2.7 前后端共用模块

谈论了许多后端模块的具体实现后，现在我们围绕 CommonJS 规范再次回到前端模块上。JavaScript 在 Node 出现之后，比别的编程语言多了一项优势，那就是一些模块可以在前后端实现共用，这是因为很多 API 在各个宿主环境下都提供。但是在实际情况中，前后端的环境是略有差别的。

### 2.7.1 模块的侧重点

前后端 JavaScript 分别搁置在 HTTP 的两端，它们扮演的角色并不同。浏览器端的 JavaScript 需要经历从同一个服务器端分发到多个客户端执行，而服务器端 JavaScript 则是相同的代码需要多次执行。前者的瓶颈在于带宽，后者的瓶颈则在于 CPU 和内存等资源。前者需要通过网络加载代码，后者从磁盘中加载，两者的加载速度不在一个数量级上。

纵观 Node 的模块引入过程，几乎全都是同步的。尽管与 Node 强调异步的行为有些相反，但它是合理的。但是如果前端模块也采用同步的方式来引入，那将会在用户体验上造成很大的问题。UI 在初始化过程中需要花费很多时间来等待脚本加载完成。

鉴于网络的原因，CommonJS 为后端 JavaScript 制定的规范并不完全适合前端的应用场景。经过一段争执之后，AMD 规范最终在前端应用场景中胜出。它的全称是 Asynchronous ModuleDefinition，即是“异步模块定义”，详见https://github.com/amdjs/amdjs-api/wiki/AMD。除此之外，还有玉伯定义的CMD规范。

### 2.7.2 AMD 规范

AMD 规范是 CommonJS 模块规范的一个延伸，它的模块定义如下：

```
define(id?, dependencies?, factory);
```

它的模块 id 和依赖是可选的，与 Node 模块相似的地方在于 factory 的内容就是实际代码的内容。下面的代码定义了一个简单的模块：

```js
define(function () {
  var exports = {};
  exports.sayHello = function () {
    alert("Hello from module: " + module.id);
  };
  return exports;
});
```

不同之处在于 AMD 模块需要用 define 来明确定义一个模块，而在 Node 实现中是隐式包装的，它们的目的是进行作用域隔离，仅在需要的时候被引入，避免掉过去那种通过全局变量或者全局命名空间的方式，以免变量污染和不小心被修改。另一个区别则是内容需要通过返回的方式实现导出。

### 2.7.3 CMD 规范

CMD 规范由国内的玉伯提出，与 AMD 规范的主要区别在于定义模块和依赖引入的部分。AMD 需要在声明模块的时候指定所有的依赖，通过形参传递依赖到模块内容中：

```js
define(["dep1", "dep2"], function (dep1, dep2) {
  return function () {};
});
```

与 AMD 模块规范相比，CMD 模块更接近于 Node 对 CommonJS 规范的定义：

```js
define(factory);
```

在依赖部分，CMD 支持动态引入，示例如下：

```js
define(function (require, exports, module) {
  // The module code goes here
});
```

require、exports 和 module 通过形参传递给模块，在需要依赖模块时，随时调用 `require()`引入即可。

### 2.7.4 兼容多种模块

规范为了让同一个模块可以运行在前后端，在写作过程中需要考虑兼容前端也实现了模块规范的环境。为了保持前后端的一致性，类库开发者需要将类库代码包装在一个闭包内。以下代码演示如何将 `hello()`方法定义到不同的运行环境中，它能够兼容 Node、AMD、CMD 以及常见的浏览器环境中：

```js
(function (name, definition) {
  // 检测上ူ文环境是否为AMDई CMD
  var hasDefine = typeof define === "function",
    // 检查上ူ文环境是否为Node
    hasExports = typeof module !== "undefined" && module.exports;
  if (hasDefine) {
    // AMD环境ई CMD环境
    define(definition);
  } else if (hasExports) {
    // 定义为೵通Node模块
    module.exports = definition();
  } else {
    // 将模块的执行结ࠬࡕ在windowՎ量中ǈ在៓બ器中thisኸၠ window对象
    this[name] = definition();
  }
})("hello", function () {
  var hello = function () {};
  return hello;
});
```

## 2.8 总结

CommonJS 提出的规范均十分简单，但是现实意义却十分强大。Node 通过模块规范，组织了自身的原生模块，弥补 JavaScript 弱结构性的问题，形成了稳定的结构，并向外提供服务。NPM 通过对包规范的支持，有效地组织了第三方模块，这使得项目开发中的依赖问题得到很好的解决，并有效提供了分享和传播的平台，借助第三方开源力量，使得 Node 第三方模块的发展速度前所未有，这对于其他后端 JavaScript 语言实现而言是从未有过的。从一定的角度上讲，CommonJS 规范帮助 Node 形成了它的骨骼。只有茁壮的根，才能培养出茂盛的枝叶，并成长为参天大树。正是这些底层的规范和实践，使得 Node 有序地发展着，摆脱掉过去 JavaScript 纷乱和被误解的局面，进而进化成良性的生态系统。

## 2.9 参考资源

本章参考的资源如下：

- http://www.commonjs.org
- http://npmjs.org/doc/README.html
- http://www.infoq.com/cn/articles/msh-using-npm-manage-node.js-dependence
- http://nodejs.org/docs/latest/api/modules.html
- http://addyosmani.com/writing-modular-js/
- http://seajs.org/docs/
- http://zh.wikipedia.org/zh/JavaScript
- http://zh.wikipedia.org/wiki/ECMAScript
- http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf
- http://www.w3.org/TR/html5/
- http://arstechnica.com/web/news/2009/12/commonjs-effort-sets-javascript-on-path-for-world-domination.ars
- http://cnodejs.org/topic/4f16442ccae1f4aa270010d7
- http://wiki.commonjs.org/wiki/Packages/1.0
- http://npmjs.org/doc/developers.html#The-package-json-File

# 第 3 章 异步 I/O

在第 1 章中，我们曾简单介绍过异步 I/O。“异步”这个名词其实很早就诞生了，但它的大规模流行却是在 Web 2.0 浪潮中，它伴随着 AJAX 的第一个 A（Asynchronous）席卷了 Web。Node 在出现之前，最习惯异步编程的程序员莫过于前端工程师了。前端编程算 GUI 编程的一种，其中充斥了各种 Ajax 和事件，这些都是典型的异步应用场景。

但事实上，异步早就存在于操作系统的底层。在底层系统中，异步通过信号量、消息等方式有了广泛的应用。意外的是，在绝大多数高级编程语言中，异步并不多见，疑似被屏蔽了一般。造成这个现象的主要原因也许令人惊讶：程序员不太适合通过异步来进行程序设计。

PHP 这门语言的设计最能体现这个观点。它对调用层不仅屏蔽了异步，甚至连多线程都不提供。PHP 语言从头到脚都是以同步阻塞的方式来执行的。它的优点十分明显，利于程序员顺序编写业务逻辑；它的缺点在小规模站点中基本不存在，但是在复杂的网络应用中，阻塞导致它无法更好地并发。

而在其他语言中，尽管可能存在异步的 API，但是程序员还是习惯采用同步的方式来编写应用。在众多高级编程语言或运行平台中，将异步作为主要编程方式和设计理念的，Node 是首个。

伴随着异步 I/O 的还有事件驱动和单线程，它们构成 Node 的基调，Ryan Dahl 正是基于这几个因素设计了 Node。Ryan Dahl 最初期望设计出一个高性能的 Web 服务器，后来则演变为一个可以基于它构建各种高速、可伸缩网络应用的平台，因为一个 Web 服务器已经无法完全涵盖和代表它的能力了。尽管它不再是一个服务器，但是可以基于它搭建更多更丰富、更强大的网络应用。

与 Node 的事件驱动、异步 I/O 设计理念比较相近的一个知名产品为 Nginx。Nginx 采用纯 C 编写，性能表现非常优异。它们的区别在于，Nginx 具备面向客户端管理连接的强大能力，但是它的背后依然受限于各种同步方式的编程语言。但 Node 却是全方位的，既可以作为服务器端去处理客户端带来的大量并发请求，也能作为客户端向网络中的各个应用进行并发请求。

Web 的含义是网，Node 的表现就如它的名字一样，是网络中灵活的一个节点。

## 3.1 为什么要异步 I/O

关于异步 I/O 为何在 Node 里如此重要，这与 Node 面向网络而设计不无关系。Web 应用已经不再是单台服务器就能胜任的时代了，在跨网络的结构下，并发已经是现代编程中的标准配备了。具体到实处，则可以从用户体验和资源分配这两个方面说起。

### 3.1.1 用户体验

异步的概念之所以首先在 Web 2.0 中火起来，是因为在浏览器中 JavaScript 在单线程上执行，而且它还与 UI 渲染共用一个线程。这意味着 JavaScript 在执行的时候 UI 渲染和响应是处于停滞状态的。《高性能 JavaScript》一书中曾经总结过，如果脚本的执行时间超过 100 毫秒，用户就会感到页面卡顿，以为网页停止响应。而在 B/S 模型中，网络速度的限制给网页的实时体验造成很大的麻烦。如果网页临时需要获取一个网络资源，通过同步的方式获取，那么 JavaScript 则需要等待资源完全从服务器端获取后才能继续执行，这期间 UI 将停顿，不响应用户的交互行为。可以想象，这样的用户体验将会多差。而采用异步请求，在下载资源期间，JavaScript 和 UI 的执行都不会处于等待状态，可以继续响应用户的交互行为，给用户一个鲜活的页面。

同理，前端通过异步可以消除掉 UI 阻塞的现象，但是前端获取资源的速度也取决于后端的响应速度。假如一个资源来自于两个不同位置的数据的返回，第一个资源需要 M 毫秒的耗时，第二个资源需要 N 毫秒的耗时。如果采用同步的方式，代码大致如下：

```js
// 消费时间为M
getData("from_db");
// 消费时间为N
getData("from_remote_api");
```

但是如果采用异步方式，第一个资源的获取并不会阻塞第二个资源，也即第二个资源的请求并不依赖第一个资源的结束。如此，我们可以享受到并发的优势，相关代码如下：

```js
getData("from_db", function (result) {
  // 消费时间为M
});
getData("from_remote_api", function (result) {
  // 消费时间为N
});
```

对比两者的时间总消耗，前者为 M+N，后者为 max（M, N）。

随着应用复杂性的增加，情景将会变成 M + N + … 和 max（M, N, …），同步与异步的优劣将会凸显出来。另一方面，随着网站或应用不断膨胀，数据将会分布到多台服务器上，分布式将会是常态。分布也意味着 M 与 N 的值会线性增长，这也会放大异步和同步在性能方面的差异。为了让读者感知到 M 和 N 值具体多昂贵，表 3-1 列出了从 CPU 一级缓存到网络的数据访问所需要的开销。

表 3-1 不同的 I/O 类型及其对应的开销

这就是异步 I/O 在 Node 中如此盛行，甚至将其作为主要理念进行设计的原因。I/O 是昂贵的,分布式 I/O 是更昂贵的。

只有后端能够快速响应资源，才能让前端的体验变好。

### 3.1.2 资源分配

排除用户体验的因素，我们从资源分配的层面来分析一下异步 I/O 的必要性。我们知道计算机在发展过程中将组件进行了抽象，分为 I/O 设备和计算设备。

假设业务场景中有一组互不相关的任务需要完成，现行的主流方法有以下两种。

- 单线程串行依次执行。
- 多线程并行完成。

如果创建多线程的开销小于并行执行，那么多线程的方式是首选的。多线程的代价在于创建线程和执行期线程上下文切换的开销较大。另外，在复杂的业务中，多线程编程经常面临锁、状态同步等问题，这是多线程被诟病的主要原因。但是多线程在多核 CPU 上能够有效提升 CPU 的利用率，这个优势是毋庸置疑的。

单线程顺序执行任务的方式比较符合编程人员按顺序思考的思维方式。它依然是最主流的编程方式，因为它易于表达。但是串行执行的缺点在于性能，任意一个略慢的任务都会导致后续执行代码被阻塞。在计算机资源中，通常 I/O 与 CPU 计算之间是可以并行进行的。但是同步的编程模型导致的问题是，I/O 的进行会让后续任务等待，这造成资源不能被更好地利用。

操作系统会将 CPU 的时间片分配给其余进程，以公平而有效地利用资源，基于这一点，有的服务器为了提升响应能力，会通过启动多个工作进程来为更多的用户服务。但是对于这一组任务而言，它无法分发任务到多个进程上，所以依然无法高效利用资源，结束所有任务所需的时间将会较长。这种模式类似于加三倍服务器，达到占用更多资源来提升服务速度，它并没能真正改善问题。

添加硬件资源是一种提升服务质量的方式，但它不是唯一的方式。

单线程同步编程模型会因阻塞 I/O 导致硬件资源得不到更优的使用。多线程编程模型也因为编程中的死锁、状态同步等问题让开发人员头疼。

Node 在两者之间给出了它的方案：利用单线程，远离多线程死锁、状态同步等问题；利用异步 I/O，让单线程远离阻塞，以更好地使用 CPU。

异步 I/O 可以算作 Node 的特色，因为它是首个大规模将异步 I/O 应用在应用层上的平台，它力求在单线程上将资源分配得更高效。为了弥补单线程无法利用多核 CPU 的缺点，Node 提供了类似前端浏览器中 WebWorkers 的子进程，该子进程可以通过工作进程高效地利用 CPU 和 I/O。这部分内容将在第 9 章中详述。

异步 I/O 的提出是期望 I/O 的调用不再阻塞后续运算，将原有等待 I/O 完成的这段时间分配给其余需要的业务去执行。图 3-1 为异步 I/O 的调用示意图。

图 3-1 异步 I/O 的调用示意图

## 3.2 异步 I/O 实现现状

异步 I/O 在 Node 中应用最为广泛，但是它并非 Node 的原创。

如同 Brendan Eich 援引 18 世纪英国文学家约翰逊所说，“它的优秀之处并非原创，它的原创之处并不优秀”，以之评价他自己创造的 JavaScript 一样，Node 的优秀之处也并非原创。下面我们看看操作系统对异步 I/O 实现的支持状况。

### 3.2.1 异步 I/O 与非阻塞 I/O

在听到 Node 的介绍时，我们时常会听到异步、非阻塞、回调、事件这些词语混合在一起推介出来，其中异步与非阻塞听起来似乎是同一回事。从实际效果而言，异步和非阻塞都达到了我们并行 I/O 的目的。但是从计算机内核 I/O 而言，异步/同步和阻塞/非阻塞实际上是两回事。

操作系统内核对于 I/O 只有两种方式：阻塞与非阻塞。在调用阻塞 I/O 时，应用程序需要等待 I/O 完成才返回结果，如图 3-2 所示。

图 3-2 调用阻塞 I/O 的过程

阻塞 I/O 的一个特点是调用之后一定要等到系统内核层面完成所有操作后，调用才结束。以读取磁盘上的一段文件为例，系统内核在完成磁盘寻道、读取数据、复制数据到内存中之后，这个调用才结束。

阻塞 I/O 造成 CPU 等待 I/O，浪费等待时间，CPU 的处理能力不能得到充分利用。为了提高性能，内核提供了非阻塞 I/O。非阻塞 I/O 跟阻塞 I/O 的差别为调用之后会立即返回，如图 3-3 所示。

> 操作系统对计算机进行了抽象，将所有输入输出设备抽象为文件。内核在进行文件 I/O 操作时，通过文件描述符进行管理，而文件描述符类似于应用程序与系统内核之间的凭证。应用程序如果需要进行 I/O 调用，需要先打开文件描述符，然后再根据文件描述符去实现文件的数据读写。此处非阻塞 I/O 与阻塞 I/O 的区别在于阻塞 I/O 完成整个获取数据的过程，而非阻塞 I/O 则不带数据直接返回，要获取数据，还需要通过文件描述符再次读取。

图 3-3 调用非阻塞 I/O 的过程

非阻塞 I/O 返回之后，CPU 的时间片可以用来处理其他事务，此时的性能提升是明显的。

但非阻塞 I/O 也存在一些问题。由于完整的 I/O 并没有完成，立即返回的并不是业务层期望的数据，而仅仅是当前调用的状态。为了获取完整的数据，应用程序需要重复调用 I/O 操作来确认是否完成。这种重复调用判断操作是否完成的技术叫做轮询，下面我们就来简要介绍这种技术。

任意技术都并非完美的。阻塞 I/O 造成 CPU 等待浪费，非阻塞带来的麻烦却是需要轮询去确认是否完全完成数据获取，它会让 CPU 处理状态判断，是对 CPU 资源的浪费。这里我们且看轮询技术是如何演进的，以减小 I/O 状态判断的 CPU 损耗。

现存的轮询技术主要有以下这些。

- read。它是最原始、性能最低的一种，通过重复调用来检查 I/O 的状态来完成完整数据的读取。在得到最终数据前，CPU 一直耗用在等待上。图 3-4 为通过 read 进行轮询的示意图。

图 3-4 通过 read 进行轮询的示意图

- select。它是在 read 的基础上改进的一种方案，通过对文件描述符上的事件状态来进行判断。图 3-5 为通过 select 进行轮询的示意图。

图 3-5 通过 select 进行轮询的示意图

select 轮询具有一个较弱的限制，那就是由于它采用一个 1024 长度的数组来存储状态，所以它最多可以同时检查 1024 个文件描述符。

- poll。该方案较 select 有所改进，采用链表的方式避免数组长度的限制，其次它能避免不需要的检查。但是当文件描述符较多的时候，它的性能还是十分低下的。图 3-6 为通过 poll 实现轮询的示意图，它与 select 相似，但性能限制有所改善。

图 3-6 通过 poll 实现轮询的示意图

- epoll。该方案是 Linux 下效率最高的 I/O 事件通知机制，在进入轮询的时候如果没有检查到 I/O 事件，将会进行休眠，直到事件发生将它唤醒。它是真实利用了事件通知、执行回调的方式，而不是遍历查询，所以不会浪费 CPU，执行效率较高。图 3-7 为通过 epoll 方式实现轮询的示意图。

图 3-7 通过 epoll 方式实现轮询的示意图

- kqueue。该方案的实现方式与 epoll 类似，不过它仅在 FreeBSD 系统下存在。

轮询技术满足了非阻塞 I/O 确保获取完整数据的需求，但是对于应用程序而言，它仍然只能算是一种同步，因为应用程序仍然需要等待 I/O 完全返回，依旧花费了很多时间来等待。等待期间，CPU 要么用于遍历文件描述符的状态，要么用于休眠等待事件发生。结论是它不够好。

### 3.2.2 理想的非阻塞异步 I/O

尽管 epoll 已经利用了事件来降低 CPU 的耗用，但是休眠期间 CPU 几乎是闲置的，对于当前线程而言利用率不够。那么，是否有一种理想的异步 I/O 呢？

我们期望的完美的异步 I/O 应该是应用程序发起非阻塞调用，无须通过遍历或者事件唤醒等方式轮询，可以直接处理下一个任务，只需在 I/O 完成后通过信号或回调将数据传递给应用程序即可。图 3-8 为理想中的异步 I/O 示意图。

图 3-8 理想中的异步 I/O 示意图

幸运的是，在 Linux 下存在这样一种方式，它原生提供的一种异步 I/O 方式（AIO）就是通过信号或回调来传递数据的。

但不幸的是，只有 Linux 下有，而且它还有缺陷——AIO 仅支持内核 I/O 中的 O_DIRECT 方式读取，导致无法利用系统缓存。

### 3.2.3 现实的异步 I/O

现实比理想要骨感一些，但是要达成异步 I/O 的目标，并非难事。前面我们将场景限定在了单线程的状况下，多线程的方式会是另一番风景。通过让部分线程进行阻塞 I/O 或者非阻塞 I/O 加轮询技术来完成数据获取，让一个线程进行计算处理，通过线程之间的通信将 I/O 得到的数据进行传递，这就轻松实现了异步 I/O（尽管它是模拟的），示意图如图 3-9 所示。

图 3-9 异步 I/O

glibc 的 AIO 便是典型的线程池模拟异步 I/O。然而遗憾的是，它存在一些难以忍受的缺陷和 bug，不推荐采用。libev 的作者 Marc Alexander Lehmann 重新实现了一个异步 I/O 的库：libeio。libeio 实质上依然是采用线程池与阻塞 I/O 模拟异步 I/O。最初，Node 在`*nix`平台下采用了 libeio 配合 libev 实现 I/O 部分，实现了异步 I/O。在 Node v0.9.3 中，自行实现了线程池来完成异步 I/O。

另一种我迟迟没有透露的异步 I/O 方案则是 Windows 下的 IOCP，它在某种程度上提供了理想的异步 I/O：调用异步方法，等待 I/O 完成之后的通知，执行回调，用户无须考虑轮询。但是它的内部其实仍然是线程池原理，不同之处在于这些线程池由系统内核接手管理。

IOCP 的异步 I/O 模型与 Node 的异步调用模型十分近似。在 Windows 平台下采用了 IOCP 实现异步 I/O。

由于 Windows 平台和`*nix`平台的差异，Node 提供了 libuv 作为抽象封装层，使得所有平台兼容性的判断都由这一层来完成，并保证上层的 Node 与下层的自定义线程池及 IOCP 之间各自独立。Node 在编译期间会判断平台条件，选择性编译 unix 目录或是 win 目录下的源文件到目标程序中，其架构如图 3-10 所示。

图 3-10 基于 libuv 的架构示意图

需要强调一点的是，这里的 I/O 不仅仅只限于磁盘文件的读写。`*nix`将计算机抽象了一番，磁盘文件、硬件、套接字等几乎所有计算机资源都被抽象为了文件，因此这里描述的阻塞和非阻塞的情况同样能适合于套接字等。

另一个需要强调的地方在于我们时常提到 Node 是单线程的，这里的单线程仅仅只是 JavaScript 执行在单线程中罢了。在 Node 中，无论是`*nix`还是 Windows 平台，内部完成 I/O 任务的另有线程池。

## 3.3 Node 的异步 I/O

介绍完系统对异步 I/O 的支持后，我们将继续介绍 Node 是如何实现异步 I/O 的。这里我们除了介绍异步 I/O 的实现外，还将讨论 Node 的执行模型。完成整个异步 I/O 环节的有事件循环、观察者和请求对象等。

### 3.3.1 事件循环

首先，我们着重强调一下 Node 自身的执行模型——事件循环，正是它使得回调函数十分普遍。

在进程启动时，Node 便会创建一个类似于 `while(true)`的循环，每执行一次循环体的过程我们称为 Tick。每个 Tick 的过程就是查看是否有事件待处理，如果有，就取出事件及其相关的回调函数。如果存在关联的回调函数，就执行它们。然后进入下个循环，如果不再有事件处理，就退出进程。流程图如图 3-11 所示。

图 3-11 Tick 流程图

### 3.3.2 观察者

在每个 Tick 的过程中，如何判断是否有事件需要处理呢？这里必须要引入的概念是观察者。每个事件循环中有一个或者多个观察者，而判断是否有事件要处理的过程就是向这些观察者询问是否有要处理的事件。

这个过程就如同饭馆的厨房，厨房一轮一轮地制作菜肴，但是要具体制作哪些菜肴取决于收银台收到的客人的下单。厨房每做完一轮菜肴，就去问收银台的小妹，接下来有没有要做的菜，如果没有的话，就下班打烊了。在这个过程中，收银台的小妹就是观察者，她收到的客人点单就是关联的回调函数。当然，如果饭馆经营有方，它可能有多个收银员，就如同事件循环中有多个观察者一样。收到下单就是一个事件，一个观察者里可能有多个事件。

浏览器采用了类似的机制。事件可能来自用户的点击或者加载某些文件时产生，而这些产生的事件都有对应的观察者。在 Node 中，事件主要来源于网络请求、文件 I/O 等，这些事件对应的观察者有文件 I/O 观察者、网络 I/O 观察者等。观察者将事件进行了分类。

事件循环是一个典型的生产者/消费者模型。异步 I/O、网络请求等则是事件的生产者，源源不断为 Node 提供不同类型的事件，这些事件被传递到对应的观察者那里，事件循环则从观察者那里取出事件并处理。

在 Windows 下，这个循环基于 IOCP 创建，而在`*nix`下则基于多线程创建。

### 3.3.3 请求对象

在这一节中，我们将通过解释 Windows 下异步 I/O（利用 IOCP 实现）的简单例子来探寻从 JavaScript 代码到系统内核之间都发生了什么。

对于一般的（非异步）回调函数，函数由我们自行调用，如下所示：

```js
var forEach = function (list, callback) {
  for (var i = 0; i < list.length; i++) {
    callback(list[i], i, list);
  }
};
```

对于 Node 中的异步 I/O 调用而言，回调函数却不由开发者来调用。那么从我们发出调用后，到回调函数被执行，中间发生了什么呢？事实上，从 JavaScript 发起调用到内核执行完 I/O 操作的过渡过程中，存在一种中间产物，它叫做请求对象。

下面我们以最简单的 `fs.open()`方法来作为例子，探索 Node 与底层之间是如何执行异步 I/O 调用以及回调函数究竟是如何被调用执行的：

```js
fs.open = function (path, flags, mode, callback) {
  // ...
  binding.open(
    pathModule._makeLong(path),
    stringToFlags(flags),
    mode,
    callback
  );
};
```

`fs.open()`的作用是根据指定路径和参数去打开一个文件，从而得到一个文件描述符，这是后续所有 I/O 操作的初始操作。从前面的代码中可以看到，JavaScript 层面的代码通过调用 C++核心模块进行下层的操作。图 3-12 为调用示意图。

图 3-12 调用示意图

从 JavaScript 调用 Node 的核心模块，核心模块调用 C++内建模块，内建模块通过 libuv 进行系统调用，这是 Node 里经典的调用方式。这里 libuv 作为封装层，有两个平台的实现，实质上是调用了 `uv_fs_open()`方法。在 `uv_fs_open()`的调用过程中，我们创建了一个 FSReqWrap 请求对象。从 JavaScript 层传入的参数和当前方法都被封装在这个请求对象中，其中我们最为关注的回调函数则被设置在这个对象的 oncomplete_sym 属性上：

```
req_wrap->object_->Set(oncomplete_sym, callback);
```

对象包装完毕后，在 Windows 下，则调用 `QueueUserWorkItem()`方法将这个 FSReqWrap 对象推入线程池中等待执行，该方法的代码如下所示：

```c#
QueueUserWorkItem(&uv_fs_thread_proc, \
req, \
WT_EXECUTEDEFAULT)
```

`QueueUserWorkItem()`方法接受 3 个参数：第一个参数是将要执行的方法的引用，这里引用的是 uv_fs_thread_proc，第二个参数是 uv_fs_thread_proc 方法运行时所需要的参数；第三个参数是执行的标志。当线程池中有可用线程时，我们会调用 `uv_fs_thread_proc()``方法。uv_fs_thread_proc()`方法会根据传入参数的类型调用相应的底层函数。以 `uv_fs_open()`为例，实际上调用 `fs__open()`方法。

至此，JavaScript 调用立即返回，由 JavaScript 层面发起的异步调用的第一阶段就此结束。JavaScript 线程可以继续执行当前任务的后续操作。当前的 I/O 操作在线程池中等待执行，不管它是否阻塞 I/O，都不会影响到 JavaScript 线程的后续执行，如此就达到了异步的目的。

请求对象是异步 I/O 过程中的重要中间产物，所有的状态都保存在这个对象中，包括送入线程池等待执行以及 I/O 操作完毕后的回调处理。

### 3.3.4 执行回调

组装好请求对象、送入 I/O 线程池等待执行，实际上完成了异步 I/O 的第一部分，回调通知是第二部分。

线程池中的 I/O 操作调用完毕之后，会将获取的结果储存在 req->result 属性上，然后调用 `PostQueuedCompletionStatus()`通知 IOCP，告知当前对象操作已经完成：

```c#
PostQueuedCompletionStatus((loop)->iocp, 0, 0, &((req)->overlapped))
```

`PostQueuedCompletionStatus()`方法的作用是向 IOCP 提交执行状态，并将线程归还线程池。通过 `PostQueuedCompletionStatus()`方法提交的状态，可以通过 `GetQueuedCompletionStatus()`提取。

在这个过程中，我们其实还动用了事件循环的 I/O 观察者。在每次 Tick 的执行中，它会调用 IOCP 相关的 `GetQueuedCompletionStatus()`方法检查线程池中是否有执行完的请求，如果存在，会将请求对象加入到 I/O 观察者的队列中，然后将其当做事件处理。

I/O 观察者回调函数的行为就是取出请求对象的 result 属性作为参数，取出 oncomplete_sym 属性作为方法，然后调用执行，以此达到调用 JavaScript 中传入的回调函数的目的。

至此，整个异步 I/O 的流程完全结束，如图 3-13 所示。

图 3-13 整个异步 I/O 的流程

事件循环、观察者、请求对象、I/O 线程池这四者共同构成了 Node 异步 I/O 模型的基本要素。

Windows 下主要通过 IOCP 来向系统内核发送 I/O 调用和从内核获取已完成的 I/O 操作，配以事件循环，以此完成异步 I/O 的过程。在 Linux 下通过 epoll 实现这个过程，FreeBSD 下通过 kqueue 实现，Solaris 下通过 Event ports 实现。不同的是线程池在 Windows 下由内核（IOCP）直接提供，`*nix`系列下由 libuv 自行实现。

### 3.3.5 小结

从前面实现异步 I/O 的过程描述中，我们可以提取出异步 I/O 的几个关键词：单线程、事件循环、观察者和 I/O 线程池。这里单线程与 I/O 线程池之间看起来有些悖论的样子。由于我们知道 JavaScript 是单线程的，所以按常识很容易理解为它不能充分利用多核 CPU。事实上，在 Node 中，除了 JavaScript 是单线程外，Node 自身其实是多线程的，只是 I/O 线程使用的 CPU 较少。另一个需要重视的观点则是，除了用户代码无法并行执行外，所有的 I/O（磁盘 I/O 和网络 I/O 等）则是可以并行起来的。

## 3.4 非 I/O 的异步 API

尽管我们在介绍 Node 的时候，多数情况下都会提到异步 I/O，但是 Node 中其实还存在一些与 I/O 无关的异步 API，这一部分也值得略微关注一下，它们分别是 `setTimeout()`、`setInterval()`、`setImmediate()`和 `process.nextTick()`。

### 3.4.1 定时器

`setTimeout()`和 `setInterval()`与浏览器中的 API 是一致的，分别用于单次和多次定时执行任务。它们的实现原理与异步 I/O 比较类似，只是不需要 I/O 线程池的参与。调用 `setTimeout()`或者 `setInterval()`创建的定时器会被插入到定时器观察者内部的一个红黑树中。每次 Tick 执行时，会从该红黑树中迭代取出定时器对象，检查是否超过定时时间，如果超过，就形成一个事件，它的回调函数将立即执行。

图 3-14 提到的主要是 `setTimeout()`的行为。`setInterval()`与之相同，区别在于后者是重复性的检测和执行。

图 3-14 setTimeout()的行为

定时器的问题在于，它并非精确的（在容忍范围内）。尽管事件循环十分快，但是如果某一次循环占用的时间较多，那么下次循环时，它也许已经超时很久了。譬如通过 `setTimeout()`设定一个任务在 10 毫秒后执行，但是在 9 毫秒后，有一个任务占用了 5 毫秒的 CPU 时间片，再次轮到定时器执行时，时间就已经过期 4 毫秒。

### 3.4.2 process.nextTick()

在未了解 `process.nextTick()`之前，很多人也许为了立即异步执行一个任务，会这样调用 `setTimeout()`来达到所需的效果：

```js
setTimeout(function () {
  // TODO
}, 0);
```

由于事件循环自身的特点，定时器的精确度不够。而事实上，采用定时器需要动用红黑树，创建定时器对象和迭代等操作，而 `setTimeout(fn, 0)`的方式较为浪费性能。实际上，`process.nextTick()`方法的操作相对较为轻量，具体代码如下：

```js
process.nextTick = function (callback) {
  // on the way out, don't bother.
  // it won't get fired anyway
  if (process._exiting) return;
  if (tickDepth >= process.maxTickDepth) maxTickWarn();
  var tock = { callback: callback };
  if (process.domain) tock.domain = process.domain;
  nextTickQueue.push(tock);
  if (nextTickQueue.length) {
    process._needTickCallback();
  }
};
```

每次调用 `process.nextTick()`方法，只会将回调函数放入队列中，在下一轮 Tick 时取出执行。定时器中采用红黑树的操作时间复杂度为 O(lg(n)), `nextTick()`的时间复杂度为 O(1)。相较之下，`process.nextTick()`更高效。

### 3.4.3 setImmediate()

`setImmediate()`方法与 `process.nextTick()`方法十分类似，都是将回调函数延迟执行。在 Node v0.9.1 之前，`setImmediate()`还没有实现，那时候实现类似的功能主要是通过 `process.nextTick()`来完成，该方法的代码如下所示：

```js
process.nextTick(function () {
  console.log("延迟执行");
});
console.log("正常执行");
// 上述代码的输出结果如下：
// 正常执行
// 延迟执行
```

而用 `setImmediate()`实现时，相关代码如下：

```js
setImmediate(function () {
  console.log("延迟执行");
});
console.log("正常执行");
// 其结果完全一样：
// 正常执行
// 延迟执行
```

但是两者之间其实是有细微差别的。将它们放在一起时，又会是怎样的优先级呢。示例代码如下：

```js
process.nextTick(function () {
  console.log("nextTick延迟执行");
});
setImmediate(function () {
  console.log("setImmediate延迟执行");
});
console.log("正常执行");
// 其执行结果如下：
// 正常执行
// nextTick延迟执行
// setImmediate延迟执行
```

从结果里可以看到，`process.nextTick()`中的回调函数执行的优先级要高于 `setImmediate()`。这里的原因在于事件循环对观察者的检查是有先后顺序的，`process.nextTick()`属于 idle 观察者，`setImmediate()`属于 check 观察者。在每一个轮循环检查中，idle 观察者先于 I/O 观察者，I/O 观察者先于 check 观察者。

在具体实现上，`process.nextTick()`的回调函数保存在一个数组中，`setImmediate()`的结果则是保存在链表中。在行为上，`process.nextTick()`在每轮循环中会将数组中的回调函数全部执行完，而 `setImmediate()`在每轮循环中执行链表中的一个回调函数。如下的示例代码可以佐证：

```js
// 加入两个nextTick()的回调函数
process.nextTick(function () {
  console.log("nextTick延迟执行1");
});
process.nextTick(function () {
  console.log("nextTick延迟执行2");
});
// 加入两个setImmediate()的回调函数
setImmediate(function () {
  console.log("setImmediate延迟执行1");
  // 进入下次循环
  process.nextTick(function () {
    console.log("强势插入");
  });
});
setImmediate(function () {
  console.log("setImmediate延迟执行2");
});
console.log("正常执行");
// 其执行结果如下：
// 正常执行
// nextTick延迟执行1
// nextTick延迟执行2
// setImmediate延迟执行1
// 强势插入
// setImmediate延迟执行2
```

从执行结果上可以看出，当第一个 `setImmediate()`的回调函数执行后，并没有立即执行第二个，而是进入了下一轮循环，再次按 `process.nextTick()`优先、`setImmediate()`次后的顺序执行。之所以这样设计，是为了保证每轮循环能够较快地执行结束，防止 CPU 占用过多而阻塞后续 I/O 调用的情况。

## 3.5 事件驱动与高性能服务器

前面主要介绍了异步的实现原理，在这个过程中，我们也基本勾勒出了事件驱动的实质，即通过主循环加事件触发的方式来运行程序。

尽管本章只用了 `fs.open()`方法作为例子来阐述 Node 如何实现异步 I/O。而实质上，异步 I/O 不仅仅应用在文件操作中。对于网络套接字的处理，Node 也应用到了异步 I/O，网络套接字上侦听到的请求都会形成事件交给 I/O 观察者。事件循环会不停地处理这些网络 I/O 事件。如果 JavaScript 有传入回调函数，这些事件将会最终传递到业务逻辑层进行处理。利用 Node 构建 Web 服务器，正是在这样一个基础上实现的，其流程图如图 3-15 所示。

图 3-15 利用 Node 构建 Web 服务器的流程图

下面为几种经典的服务器模型，这里对比下它们的优缺点。

- 同步式。对于同步式的服务，一次只能处理一个请求，并且其余请求都处于等待状态。
- 每进程/每请求。为每个请求启动一个进程，这样可以处理多个请求，但是它不具备扩展性，因为系统资源只有那么多。
- 每线程/每请求。为每个请求启动一个线程来处理。尽管线程比进程要轻量，但是由于每个线程都占用一定内存，当大并发请求到来时，内存将会很快用光，导致服务器缓慢。每线程/每请求的扩展性比每进程/每请求的方式要好，但对于大型站点而言依然不够。

每线程/每请求的方式目前还被 Apache 所采用。Node 通过事件驱动的方式处理请求，无须为每一个请求创建额外的对应线程，可以省掉创建线程和销毁线程的开销，同时操作系统在调度任务时因为线程较少，上下文切换的代价很低。这使得服务器能够有条不紊地处理请求，即使在大量连接的情况下，也不受线程上下文切换开销的影响，这是 Node 高性能的一个原因。

事件驱动带来的高效已经渐渐开始为业界所重视。知名服务器 Nginx，也摒弃了多线程的方式，采用了和 Node 相同的事件驱动。如今，Nginx 大有取代 Apache 之势。Node 具有与 Nginx 相同的特性，不同之处在于 Nginx 采用纯 C 写成，性能较高，但是它仅适合于做 Web 服务器，用于反向代理或负载均衡等服务，在处理具体业务方面较为欠缺。Node 则是一套高性能的平台，可以利用它构建与 Nginx 相同的功能，也可以处理各种具体业务，而且与背后的网络保持异步畅通。两者相比，Node 没有 Nginx 在 Web 服务器方面那么专业，但场景更大，自身性能也不错。在实际项目中，我们可以结合它们各自优点，以达到应用的最优性能。

事实上，Node 的异步 I/O 并非首创，但却是第一个成功的平台。在那之前，也有一些知名的基于事件驱动的实现，具体如下所示。

- Ruby 的 Event Machine。
- Perl 的 AnyEvent。
- Python 的 Twisted。

在这些平台上采用事件驱动的方式时，需要花一定精力了解这些库。这些库没能成功的原因则是同步 I/O 库的存在。本章描述的异步 I/O 实现，其主旨是使 I/O 操作与 CPU 操作分离。奈何这些语言平台上的标准 I/O 库都是阻塞式的，一旦事件循环中存在阻塞 I/O，将导致其余 I/O 无法立即进行，性能会急剧下降，其效果类似于同步式服务，其他请求将不能立即处理。

因为在这些成熟的语言平台上，异步不是主流，尽管有这些事件驱动的实现库，但开发者总会习惯性地采用同步 I/O 库，这导致预想的高性能直接落空。Ryan Dahl 在评估他最早的选型时，Lua 一度是最贴近他选型的语言，但是由于标准 I/O 库是同步 I/O，他知道即使完成这样一个事件驱动的实现，也将不会得到较大范围的使用。在 Node 广泛流行之后，社区的 Tim Caswell 将 Node 的这套思想重新移植到了 Lua 平台，该项目叫 luvit。

JavaScript 中的作用域和函数在浏览器端已有成熟的应用，也很好地帮助了 RyanDahl 实现它的想法。JavaScript 在服务器端近乎空白，使得 Node 没有任何历史包袱，而 Node 在性能上的表现使得它一下子就在社区中流行起来了。

## 3.6 总结

本章介绍了异步 I/O 和另一些非 I/O 的异步方法。可以看出，事件循环是异步实现的核心，它与浏览器中的执行模型基本保持了一致。而像古老的 Rhino，尽管是较早就能在服务器端运行的 JavaScript 运行时，但是执行模型并不像浏览器采用事件驱动，而是像其他语言一般采用同步 I/O 作为主要模型，这造成它在性能上无所发挥。Node 正是依靠构建了一套完善的高性能异步 I/O 框架，打破了 JavaScript 在服务器端止步不前的局面。

## 3.7 参考资源

本章参考的资源如下：

- http://cnodejs.org/blog/?p=244
- http://cnodejs.org/blog/?p=2426
- http://cnodejs.org/blog/?p=2489
- http://nodejs.org/nodeconf.pdf
- http://blog.dccmx.com/2011/04/select-poll-epoll-in-kernel/
- http://www.ibm.com/developerworks/cn/linux/l-async/
- http://twistedmatrix.com/trac/
- http://luvit.io/
- http://forum.nginx.org/read.php?2,113524,113587#msg-113587

# 第 4 章 异步编程

有异步 I/O，必有异步编程。

上一章描述了 Node 如何通过事件循环实现异步，包括与各种 I/O 多路复用搭配实现的异步 I/O 以及与 I/O 无关的异步。Node 是首个将异步大规模带到应用层面的平台，它从内在运行机制到 API 的设计，无不透露出异步的气息来。异步的高性能为它带来了高度的赞誉，而异步编程也为其带来部分的诋毁。

前述章节中亦描述过异步 I/O 在应用层面不流行的原因，那便是异步编程在流程控制中，业务表达并不太适合自然语言的线性思维习惯。较少人能适应直接面对事件驱动进行编程，唯独对它熟悉的主要是 GUI 开发者，如前端工程师或 GUI 工程师。前端工程师习以为常并能够娴熟地处理各种 DOM 事件和浏览器中的事件。RyanDahl 偏好事件驱动，而 Java Script 在浏览器中也正契合事件驱动的执行过程，这也使得前后端的 JavaScript 在执行原理和风格上都趋于一致。虽然语言执行在不同的环境，但除了宿主提供的 API 有所不同外，并不让人觉得是一门新语言。

V8 和异步 I/O 在性能上带来的提升，前后端 JavaScript 编程风格一致，是 Node 能够迅速成功并流行起来的主要原因。

## 4.1 函数式编程

在开始异步编程之前，先得知晓 JavaScript 现今的回调函数和深层嵌套的来龙去脉。在 JavaScript 中，函数（function）作为一等公民，使用上非常自由，无论调用它，或者作为参数，或者作为返回值均可。函数的灵活性是 JavaScript 比较吸引人的地方之一，它与古老的 Lisp 语言颇具渊源。JavaScript 在诞生之前，BrendanEich 借鉴了 Scheme 语言（Scheme 作为 Lisp 的派生），吸收了函数式编程的精华，将函数作为一等公民便是典型案例。

鉴于函数式编程在近年来重新火热，而前端类图书中较少述及这部分知识，这里稍作补充，因为它是 JavaScript 异步编程的基础。

### 4.1.1 高阶函数

在通常的语言中，函数的参数只接受基本的数据类型或是对象引用，返回值也只是基本数据类型和对象引用。下面的代码为常规的参数传递和返回：

```js
function foo(x) {
  return x;
}
```

高阶函数则是可以把函数作为参数，或是将函数作为返回值的函数，如下面的代码所示：

```js
function foo(x) {
  return function () {
    return x;
  };
}
```

高阶函数可以将函数作为输入或返回值的变化看起来虽细小，但是对于 C/C++语言而言，通过指针也可以达到相同的效果。但对于程序编写，高阶函数则比普通的函数要灵活许多。除了通常意义的函数调用返回外，还形成了一种后续传递风格（Continuation Passing Style）的结果接收方式，而非单一的返回值形式。后续传递风格的程序编写将函数的业务重点从返回值转移到了回调函数中：

```js
function foo(x, bar) {
  return bar(x);
}
```

以上面的代码为例，对于相同的 `foo()`函数，传入的 bar 参数不同，则可以得到不同的结果。一个经典的例子便是数组的 `sort()`方法，它是一个货真价实的高阶函数，可以接受一个方法作为参数参与运算排序：

```js
var points = [40, 100, 1, 5, 25, 10];
points.sort(function (a, b) {
  return a - b;
});
// [ 1, 5, 10, 25, 40, 100 ]
```

通过改动 `sort()`方法的参数，可以决定不同的排序方式，从这里可以看出高阶函数的灵活性来。结合 Node 提供的最基本的事件模块可以看到，事件的处理方式正是基于高阶函数的特性来完成的。在自定义事件实例中，通过为相同事件注册不同的回调函数，可以很灵活地处理业务逻辑。示例代码如下：

```js
var emitter = new events.EventEmitter();
emitter.on("event_foo", function () {
  // TODO
});
```

本书时常提到事件可以十分方便地进行复杂业务逻辑的解耦，它其实受益于高阶函数。

高阶函数在 JavaScript 中比比皆是，其中 ECMAScript5 中提供的一些数组方法（`forEach()`、`map()`、`reduce()`、`reduceRight()`、`filter()`、`every()`、`some()`）十分典型。

### 4.1.2 偏函数用法

偏函数用法是指创建一个调用另外一个部分——参数或变量已经预置的函数——的函数的用法。这句话相对较为拗口，下面我们以实例来说明：

```js
var toString = Object.prototype.toString;
var isString = function (obj) {
  return toString.call(obj) == "[object String]";
};
var isFunction = function (obj) {
  return toString.call(obj) == "[object Function]";
};
```

在 JavaScript 中进行类型判断时，我们通常会进行类似上述代码的方法定义。这段代码固然不复杂，只有两个函数的定义，但是里面存在的问题是我们需要重复去定义一些相似的函数，如果有更多的 `isXXX()`，就会出现更多的冗余代码。为了解决重复定义的问题，我们引入一个新函数，这个新函数可以如工厂一样批量创建一些类似的函数。在下面的代码中，我们通过 `isType()`函数预先指定 type 的值，然后返回一个新的函数：

```js
var isType = function (type) {
  return function (obj) {
    return toString.call(obj) == "[object " + type + "]";
  };
};
var isString = isType("String");
var isFunction = isType("Function");
```

可以看出，引入 `isType()`函数后，创建 `isString()`、`isFunction()`函数就变得简单多了。这种通过指定部分参数来产生一个新的定制函数的形式就是偏函数。

偏函数应用在异步编程中也十分常见，著名类库 Underscore 提供的 `after()`方法即是偏函数应用，其定义如下：

```js
_.after = function (times, func) {
  if (times <= 0) return func();
  return function () {
    if (--times < 1) {
      return func.apply(this, arguments);
    }
  };
};
```

这个函数可以根据传入的 times 参数和具体方法，生成一个需要调用多次才真正执行实际函数的函数。

## 4.2 异步编程的优势与难点

曾经的单线程模型在同步 I/O 的影响下，由于 I/O 调用缓慢，在应用层面导致 CPU 与 I/O 无法重叠进行。为了照顾编程人员的阅读思维习惯，同步 I/O 盛行了很多年。但在日新月异的技术大潮面前，性能问题摆在了编程人员的面前。提升性能的方式过去多用多线程的方式解决，但是多线程的引入在业务逻辑方面制造的麻烦也不少。从操作系统调度多线程的上下文切换开销，到实际编程里的锁、同步等问题，让开发人员头疼的时候也并不少。另一个解决 I/O 性能的方案是通过 C/C++调用操作系统底层接口，自己手工完成异步 I/O，这能够达到很高的性能，但是调试和开发门槛均十分高，在帮助业务解决问题上，需要花费较大的精力。Node 利用 JavaScript 及其内部异步库，将异步直接提升到业务层面，这是一种创新。

### 4.2.1 优势

Node 带来的最大特性莫过于基于事件驱动的非阻塞 I/O 模型，这是它的灵魂所在。非阻塞 I/O 可以使 CPU 与 I/O 并不相互依赖等待，让资源得到更好的利用。对于网络应用而言，并行带来的想象空间更大，延展而开的是分布式和云。并行使得各个单点之间能够更有效地组织起来，这也是 Node 在云计算厂商中广受青睐的原因，图 4-1 为异步 I/O 调用的示意图。

图 4-1 异步 I/O 调用的示意图

如果采用传统的同步 I/O 模型，分布式计算中性能的折扣将会是明显的，如图 4-2 所示。

图 4-2 同步 I/O 调用示意图

在第 3 章中，我们讨论过 Node 实现异步 I/O 的原理。利用事件循环的方式，JavaScript 线程像一个分配任务和处理结果的大管家，I/O 线程池里的各个 I/O 线程都是小二，负责兢兢业业地完成分配来的任务，小二与管家之间互不依赖，所以可以保持整体的高效率。这个利用事件循环的经典调度方式在很多地方都存在应用，最典型的是 UI 编程，如 iOS 应用开发等。

这个模型的缺点则在于管家无法承担过多的细节性任务，如果承担太多，则会影响到任务的调度，管家忙个不停，小二却得不到活干，结局则是整体效率的降低。

换言之，Node 是为了解决编程模型中阻塞 I/O 的性能问题的，采用了单线程模型，这导致 Node 更像一个处理 I/O 密集问题的能手，而 CPU 密集型则取决于管家的能耐如何。

在第 1 章中，从斐波那契数列计算的测试结果中可以看到，这个管家具体的能力如何。如果形象地去评判的话，C 语言是性能至尊，得益于 V8 性能的 Node 则是一流武林高手，在具备武功秘笈的情况下（调用 C/C++扩展模块）, Node 的能力可以逼近顶尖之列。

由于事件循环模型需要应对海量请求，海量请求同时作用在单线程上，就需要防止任何一个计算耗费过多的 CPU 时间片。至于是计算密集型，还是 I/O 密集型，只要计算不影响异步 I/O 的调度，那就不构成问题。建议对 CPU 的耗用不要超过 10ms，或者将大量的计算分解为诸多的小量计算，通过 `setImmediate()`进行调度。只要合理利用 Node 的异步模型与 V8 的高性能，就可以充分发挥 CPU 和 I/O 资源的优势。

### 4.2.2 难点

Node 令异步编程如此风行，这也是异步编程首次大规模出现在业务层面。它借助异步 I/O 模型及 V8 高性能引擎，突破单线程的性能瓶颈，让 JavaScript 在后端达到实用价值。另一方面，它也统一了前后端 JavaScript 的编程模型。对于异步编程带来的新鲜感与不适感，开发者们有着不同程度的感受。接下来，我们梳理一下异步编程的难点，以更好地利用 Node。

1. 难点 1：异常处理

过去我们处理异常时，通常使用类 Java 的 try/catch/final 语句块进行异常捕获，示例代码如下：

```js
try {
  JSON.parse(json);
} catch (e) {
  // TODO
}
```

但是这对于异步编程而言并不一定适用。第 3 章提到过，异步 I/O 的实现主要包含两个阶段：提交请求和处理结果。这两个阶段中间有事件循环的调度，两者彼此不关联。异步方法则通常在第一个阶段提交请求后立即返回，因为异常并不一定发生在这个阶段，try/catch 的功效在此处不会发挥任何作用。异步方法的定义如下所示：

```js
var async = function (callback) {
  process.nextTick(callback);
};
```

调用 `async()`方法后，callback 被存放起来，直到下一个事件循环（Tick）才会取出来执行。尝试对异步方法进行 try/catch 操作只能捕获当次事件循环内的异常，对 callback 执行时抛出的异常将无能为力，示例代码如下：

```js
try {
  async(callback);
} catch (e) {
  // TODO
}
```

Node 在处理异常上形成了一种约定，将异常作为回调函数的第一个实参传回，如果为空值，则表明异步调用没有异常抛出：

```js
async(function (err, results) {
  // TODO
});
```

在我们自行编写的异步方法上，也需要去遵循这样一些原则：

- 原则一：必须执行调用者传入的回调函数；
- 原则二：正确传递回异常供调用者判断。

示例代码如下：

```js
var async = function (callback) {
  process.nextTick(function () {
    var results = something;
    if (error) {
      return callback(error);
    }
    callback(null, results);
  });
};
```

在异步方法的编写中，另一个容易犯的错误是对用户传递的回调函数进行异常捕获，示例代码如下：

```js
try {
  req.body = JSON.parse(buf, options.reviver);
  callback();
} catch (err) {
  err.body = buf;
  err.status = 400;
  callback(err);
}
```

上述代码的意图是捕获 `JSON.parse()`中可能出现的异常，但是却不小心包含了用户传递的回调函数。这意味着如果回调函数中有异常抛出，将会进入 `catch()`代码块中执行，于是回调函数将会被执行两次。这显然不是预期的情况，可能导致业务混乱。正确的捕获应当为：

```js
try {
  req.body = JSON.parse(buf, options.reviver);
} catch (err) {
  err.body = buf;
  err.status = 400;
  return callback(err);
}
callback();
```

在编写异步方法时，只要将异常正确地传递给用户的回调方法即可，无须过多处理。

2. 难点 2：函数嵌套过深

这或许是 Node 被人诟病最多的地方。在前端开发中，DOM 事件相对而言不会存在互相依赖或需要多个事件一起协作的场景，较少存在异步多级依赖的情况。下面的代码为彼此独立的 DOM 事件绑定：

```js
$(selector).click(function (event) {
  // TODO
});
$(selector).change(function (event) {
  // TODO
});
```

但是对于 Node 而言，事务中存在多个异步调用的场景比比皆是。比如一个遍历目录的操作，其代码如下：

```js
fs.readdir(path.join(__dirname, ".."), function (err, files) {
  files.forEach(function (filename, index) {
    fs.readFile(filename, "utf8", function (err, file) {
      // TODO
    });
  });
});
```

对于上述场景，由于两次操作存在依赖关系，函数嵌套的行为也许情有可原。那么，在网页渲染的过程中，通常需要数据、模板、资源文件，这三者互相之间并不依赖，但最终渲染结果中三者缺一不可。如果采用默认的异步方法调用，程序也许将会如下所示：

```js
fs.readFile(template_path, "utf8", function (err, template) {
  db.query(sql, function (err, data) {
    l10n.get(function (err, resources) {
      // TODO
    });
  });
});
```

这在结果的保证上是没有问题的，问题在于这并没有利用好异步 I/O 带来的并行优势。这是异步编程的典型问题，为此有人曾说，因为嵌套的深度，未来最难看的代码必将从 Node 中诞生。但是实际情况没有想象得那么糟糕，且看后面如何解决该问题。

3. 难点 3：阻塞代码

对于进入 JavaScript 世界不久的开发者，比较纳闷这门编程语言竟然没有 `sleep()`这样的线程沉睡功能，唯独能用于延时操作的只有 `setInterval()`和 `setTimeout()`这两个函数。但是让人惊讶的是，这两个函数并不能阻塞后续代码的持续执行。所以，有多半的开发者会写出下述这样的代码来实现 `sleep(1000)`的效果：

```js
// TODO
var start = new Date();
while (new Date() - start < 1000) {
  // TODO
}
// 需要阻塞的代码
```

但是事实是糟糕的，这段代码会持续占用 CPU 进行判断，与真正的线程沉睡相去甚远，完全破坏了事件循环的调度。由于 Node 单线程的原因，CPU 资源全都会用于为这段代码服务，导致其余任何请求都会得不到响应。

遇见这样的需求时，在统一规划业务逻辑之后，调用 `setTimeout()`的效果会更好。

4. 难点 4：多线程编程

我们在谈论 JavaScript 的时候，通常谈的是单一线程上执行的代码，这在浏览器中指的是 JavaScript 执行线程与 UI 渲染共用的一个线程；在 Node 中，只是没有 UI 渲染的部分，模型基本相同。对于服务器端而言，如果服务器是多核 CPU，单个 Node 进程实质上是没有充分利用多核 CPU 的。随着现今业务的复杂化，对于多核 CPU 利用的要求也越来越高。浏览器提出了 Web Workers，它通过将 JavaScript 执行与 UI 渲染分离，可以很好地利用多核 CPU 为大量计算服务。同时前端 WebWorkers 也是一个利用消息机制合理使用多核 CPU 的理想模型。图 4-3 为 WebWorkers 的工作示意图。

图 4-3 Web Workers 的工作示意图

遗憾在于前端浏览器存在对标准的滞后性，Web Workers 并没有广泛应用起来。另外 Web Workers 能解决利用 CPU 和减少阻塞 UI 渲染，但是不能解决 UI 渲染的效率问题。Node 借鉴了这个模式，child_process 是其基础 API, cluster 模块是更深层次的应用。借助 Web Workers 的模式，开发人员要更多地去面临跨线程的编程，这对于以往的 JavaScript 编程经验是较少考虑的。在第 9 章中，我们将详细分析 Node 的进程，以展开这部分内容。

5. 难点 5：异步转同步

习惯异步编程的同学，也许能够从容面对异步编程带来的副产品，比如嵌套回调、业务分散等问题。Node 提供了绝大部分的异步 API 和少量的同步 API，偶尔出现的同步需求将会因为没有同步 API 让开发者突然无所适从。目前，Node 中试图同步式编程，但并不能得到原生支持，需要借助库或者编译等手段来实现。但对于异步调用，通过良好的流程控制，还是能够将逻辑梳理成顺序式的形式。

## 4.3 异步编程解决方案

前面列举了因异步编程带来的一些问题，与异步编程提升的性能成果相比，编程过程看起来似乎没有想象中那么美好，但是事实却也没有那么糟糕。与问题相比，解决问题的方案总是更多，本节将展开各个典型的解决方案。

目前，异步编程的主要解决方案有如下 3 种。

- 事件发布/订阅模式。
- Promise/Deferred 模式。
- 流程控制库。

### 4.3.1 事件发布/订阅模式

事件监听器模式是一种广泛用于异步编程的模式，是回调函数的事件化，又称发布/订阅模式。

Node 自身提供的[events 模块](http://nodejs.org/docs/latest/api/events.html)是发布/订阅模式的一个简单实现，Node 中部分模块都继承自它，这个模块比前端浏览器中的大量 DOM 事件简单，不存在事件冒泡，也不存在 `preventDefault()`、`stopPropagation()`和 `stopImmediatePropagation()`等控制事件传递的方法。它具有 `addListener/on()`、`once()`、`removeListener()`、`removeAllListeners()`和 `emit()`等基本的事件监听模式的方法实现。事件发布/订阅模式的操作极其简单，示例代码如下：

```js
// 订阅
emitter.on("event1", function (message) {
  console.log(message);
});
// 发布
emitter.emit("event1", "I am message!");
```

可以看到，订阅事件就是一个高阶函数的应用。事件发布/订阅模式可以实现一个事件与多个回调函数的关联，这些回调函数又称为事件侦听器。通过 `emit()`发布事件后，消息会立即传递给当前事件的所有侦听器执行。侦听器可以很灵活地添加和删除，使得事件和具体处理逻辑之间可以很轻松地关联和解耦。

事件发布/订阅模式自身并无同步和异步调用的问题，但在 Node 中，`emit()`调用多半是伴随事件循环而异步触发的，所以我们说事件发布/订阅广泛应用于异步编程。

事件发布/订阅模式常常用来解耦业务逻辑，事件发布者无须关注订阅的侦听器如何实现业务逻辑，甚至不用关注有多少个侦听器存在，数据通过消息的方式可以很灵活地传递。在一些典型场景中，可以通过事件发布/订阅模式进行组件封装，将不变的部分封装在组件内部，将容易变化、需自定义的部分通过事件暴露给外部处理，这是一种典型的逻辑分离方式。在这种事件发布/订阅式组件中，事件的设计非常重要，因为它关乎外部调用组件时是否优雅，从某种角度来说事件的设计就是组件的接口设计。

从另一个角度来看，事件侦听器模式也是一种钩子（hook）机制，利用钩子导出内部数据或状态给外部的调用者。Node 中的很多对象大多具有黑盒的特点，功能点较少，如果不通过事件钩子的形式，我们就无法获取对象在运行期间的中间值或内部状态。这种通过事件钩子的方式，可以使编程者不用关注组件是如何启动和执行的，只需关注在需要的事件点上即可。下面的 HTTP 请求是典型场景：

```js
var options = {
  host: "www.google.com",
  port: 80,
  path: "/upload",
  method: "POST",
};
var req = http.request(options, function (res) {
  console.log("STATUS: " + res.statusCode);
  console.log("HEADERS: " + JSON.stringify(res.headers));
  res.setEncoding("utf8");
  res.on("data", function (chunk) {
    console.log("BODY: " + chunk);
  });
  res.on("end", function () {
    // TODO
  });
});
req.on("error", function (e) {
  console.log("problem with request: " + e.message);
});
// write data to request body
req.write("data\n");
req.write("data\n");
req.end();
```

在这段 HTTP 请求的代码中，程序员只需要将视线放在 error、data、end 这些业务事件点上即可，至于内部的流程如何，无需过于关注。

值得一提的是，Node 对事件发布/订阅的机制做了一些额外的处理，这大多是基于健壮性而考虑的。下面为两个具体的细节点。

- 如果对一个事件添加了超过 10 个侦听器，将会得到一条警告。这一处设计与 Node 自身单线程运行有关，设计者认为侦听器太多可能导致内存泄漏，所以存在这样一条警告。调用 `emitter.setMaxListeners(0)`；可以将这个限制去掉。另一方面，由于事件发布会引起一系列侦听器执行，如果事件相关的侦听器过多，可能存在过多占用 CPU 的情景。
- 为了处理异常，EventEmitter 对象对 error 事件进行了特殊对待。如果运行期间的错误触发了 error 事件，EventEmitter 会检查是否有对 error 事件添加过侦听器。如果添加了，这个错误将会交由该侦听器处理，否则这个错误将会作为异常抛出。如果外部没有捕获这个异常，将会引起线程退出。一个健壮的 EventEmitter 实例应该对 error 事件做处理。

1. 继承 events 模块

实现一个继承 EventEmitter 的类是十分简单的，以下代码是 Node 中 Stream 对象继承 EventEmitter 的例子：

```js
var events = require("events");
function Stream() {
  events.EventEmitter.call(this);
}
util.inherits(Stream, events.EventEmitter);
```

Node 在 util 模块中封装了继承的方法，所以此处可以很便利地调用。开发者可以通过这样的方式轻松继承 EventEmitter 类，利用事件机制解决业务问题。在 Node 提供的核心模块中，有近半数都继承自 EventEmitter。

2. 利用事件队列解决雪崩问题

在事件订阅/发布模式中，通常也有一个 `once()`方法，通过它添加的侦听器只能执行一次，在执行之后就会将它与事件的关联移除。这个特性常常可以帮助我们过滤一些重复性的事件响应。下面我们介绍一下如何采用 `once()`来解决雪崩问题。

在计算机中，缓存由于存放在内存中，访问速度十分快，常常用于加速数据访问，让绝大多数的请求不必重复去做一些低效的数据读取。所谓雪崩问题，就是在高访问量、大并发量的情况下缓存失效的情景，此时大量的请求同时涌入数据库中，数据库无法同时承受如此大的查询请求，进而往前影响到网站整体的响应速度。

以下是一条数据库查询语句的调用：

```js
var select = function (callback) {
  db.select("SQL", function (results) {
    callback(results);
  });
};
```

如果站点刚好启动，这时缓存中是不存在数据的，而如果访问量巨大，同一句 SQL 会被发送到数据库中反复查询，会影响服务的整体性能。一种改进方案是添加一个状态锁，相关代码如下：

```js
var status = "ready";
var select = function (callback) {
  if (status === "ready") {
    status = "pending";
    db.select("SQL", function (results) {
      status = "ready";
      callback(results);
    });
  }
};
```

但是在这种情景下，连续地多次调用 `select()`时，只有第一次调用是生效的，后续的 `select()`是没有数据服务的，这个时候可以引入事件队列，相关代码如下：

```js
var proxy = new events.EventEmitter();
var status = "ready";
var select = function (callback) {
  proxy.once("selected", callback);
  if (status === "ready") {
    status = "pending";
    db.select("SQL", function (results) {
      proxy.emit("selected", results);
      status = "ready";
    });
  }
};
```

这里我们利用了 `once()`方法，将所有请求的回调都压入事件队列中，利用其执行一次就会将监视器移除的特点，保证每一个回调只会被执行一次。对于相同的 SQL 语句，保证在同一个查询开始到结束的过程中永远只有一次。SQL 在进行查询时，新到来的相同调用只需在队列中等待数据就绪即可，一旦查询结束，得到的结果可以被这些调用共同使用。这种方式能节省重复的数据库调用产生的开销。由于 Node 单线程执行的原因，此处无须担心状态同步问题。这种方式其实也可以应用到其他远程调用的场景中，即使外部没有缓存策略，也能有效节省重复开销。

此处可能因为存在侦听器过多引发的警告，需要调用 `setMaxListeners(0)`移除掉警告，或者设更大的警告阈值。

`once()`方法产生的效果，也可以在著名的 Gearman 异步应用框架中实现。但在 JavaScript 中，实现这个效果十分容易。

3. 多异步之间的协作方案

事件发布/订阅模式有着它的优点。利用高阶函数的优势，侦听器作为回调函数可以随意添加和删除，它帮助开发者轻松处理随时可能添加的业务逻辑。也可以隔离业务逻辑，保持业务逻辑单元的职责单一。一般而言，事件与侦听器的关系是一对多，但在异步编程中，也会出现事件与侦听器的关系是多对一的情况，也就是说一个业务逻辑可能依赖两个通过回调或事件传递的结果。前面提及的回调嵌套过深的原因即是如此。

这里我们尝试通过原生代码解决“难点 2”中为了最终结果的处理而导致可以并行调用但实际只能串行执行的问题。我们的目标是既要享受异步 I/O 带来的性能提升，也要保持良好的编码风格。这里以渲染页面所需要的模板读取、数据读取和本地化资源读取为例简要介绍一下，相关代码如下：

```js
var count = 0;
var results = {};
var done = function (key, value) {
  results[key] = value;
  count++;
  if (count === 3) {
    // 渲染页面
    render(results);
  }
};
fs.readFile(template_path, "utf8", function (err, template) {
  done("template", template);
});
db.query(sql, function (err, data) {
  done("data", data);
});
l10n.get(function (err, resources) {
  done("resources", resources);
});
```

由于多个异步场景中回调函数的执行并不能保证顺序，且回调函数之间互相没有任何交集，所以需要借助一个第三方函数和第三方变量来处理异步协作的结果。通常，我们把这个用于检测次数的变量叫做哨兵变量。聪明的你也许已经想到利用偏函数来处理哨兵变量和第三方函数的关系了，相关代码如下：

```js
var after = function (times, callback) {
  var count = 0,
    results = {};
  return function (key, value) {
    results[key] = value;
    count++;
    if (count === times) {
      callback(results);
    }
  };
};
var done = after(times, render);
```

上述方案实现了多对一的目的。如果业务继续增长，我们依然可以继续利用发布/订阅方式来完成多对多的方案，相关代码如下：

```js
var emitter = new events.Emitter();
var done = after(times, render);
emitter.on("done", done);
emitter.on("done", other);
fs.readFile(template_path, "utf8", function (err, template) {
  emitter.emit("done", "template", template);
});
db.query(sql, function (err, data) {
  emitter.emit("done", "data", data);
});
l10n.get(function (err, resources) {
  emitter.emit("done", "resources", resources);
});
```

这种方案结合了前者用简单的偏函数完成多对一的收敛和事件订阅/发布模式中一对多的发散。

在上面的方法中，有一个令调用者不那么舒服的问题，那就是调用者要去准备这个 `done()`函数，以及在回调函数中需要从结果中把数据一个一个提取出来，再进行处理。

另一个方案则是来自笔者自己写的 EventProxy 模块，它是对事件订阅/发布模式的扩充，可以自由订阅组合事件。由于依旧采用的是事件订阅/发布模式，与 Node 十分契合，相关代码如下：

```js
var proxy = new EventProxy();
proxy.all("template", "data", "resources", function (
  template,
  data,
  resources
) {
  // TODO
});
fs.readFile(template_path, "utf8", function (err, template) {
  proxy.emit("template", template);
});
db.query(sql, function (err, data) {
  proxy.emit("data", data);
});
l10n.get(function (err, resources) {
  proxy.emit("resources", resources);
});
```

EventProxy 提供了一个 `all()`方法来订阅多个事件，当每个事件都被触发之后，侦听器才会执行。另外的一个方法是 `tail()`方法，它与 `all()`方法的区别在于 `all()`方法的侦听器在满足条件之后只会执行一次，`tail()`方法的侦听器则在满足条件时执行一次之后，如果组合事件中的某个事件被再次触发，侦听器会用最新的数据继续执行。

`all()`方法带来的另一个改进则是：在侦听器中返回数据的参数列表与订阅组合事件的事件列表是一致对应的。

除此之外，在异步的场景下，我们常常需要从一个接口多次读取数据，此时触发的事件名或许是相同的。EventProxy 提供了 `after()`方法来实现事件在执行多少次后执行侦听器的单一事件组合订阅方式，示例代码如下：

```js
var proxy = new EventProxy();
proxy.after("data", 10, function (datas) {
  // TODO
});
```

这段代码表示执行 10 次 data 事件后执行侦听器。这个侦听器得到的数据为 10 次按事件触发次序排序的数组。

EventProxy 模块除了可以应用于 Node 中外，还可以用在前端浏览器中。

4. EventProxy 的原理

EventProxy 来自于 Backbone 的事件模块，Backbone 的事件模块是 Model、View 模块的基础功能，在前端有广泛的使用。它在每个非 all 事件触发时都会触发一次 all 事件，相关代码如下：

```js
// Trigger an event, firing all bound callbacks. Callbacks are passed the
// same arguments as `trigger` is, apart from the event name.
// Listening for `"all"` passes the true event name as the first argument
trigger : function(eventName) {
  var list, calls, ev, callback, args;
  var both = 2;
  if (!(calls = this._callbacks)) return this;
  while (both--) {
    ev = both ? eventName : 'all';
    if (list = calls[ev]) {
      for (var i = 0, l = list.length; i < l; i++) {
        if (!(callback = list[i])) {
          list.splice(i, 1); i--; l--;
        } else {
          args = both ? Array.prototype.slice.call(arguments, 1) : arguments;
          callback[0].apply(callback[1] || this, args);
        }
      }
    }
  }
  return this;
}
```

EventProxy 则是将 all 当做一个事件流的拦截层，在其中注入一些业务来处理单一事件无法解决的异步处理问题。类似的扩展方法还有 `all()`、`tail()`、`after()`、`not()`和 `any()`等。

5. EventProxy 的异常处理

EventProxy 在事件发布/订阅模式的基础上还完善了异常处理。在异步方法中，异常处理需要占用一定比例的精力。在过去一段时间内，我们都是通过额外添加 error 事件来进行异常统一处理的，代码大致如下：

```js
exports.getContent = function (callback) {
  var ep = new EventProxy();
  ep.all("tpl", "data", function (tpl, data) {
    // 成功回调
    callback(null, {
      template: tpl,
      data: data,
    });
  });
  // 侦听error事件
  ep.bind("error", function (err) {
    // 卸载掉所有处理函数
    ep.unbind();
    // 异常回调
    callback(err);
  });
  fs.readFile("template.tpl", "utf-8", function (err, content) {
    if (err) {
      // 一旦发生异常，一律交给error事件的处理函数处理
      return ep.emit("error", err);
    }
    ep.emit("tpl", content);
  });
  db.get("some sql", function (err, result) {
    if (err) {
      // 一旦发生异常，一律交给error事件的处理函数处理
      return ep.emit("error", err);
    }
    ep.emit("data", result);
  });
};
```

因为异常处理的原因，代码量一下子多起来了，而 EventProxy 在实践过程中改进了这个问题，相关代码如下：

```js
exports.getContent = function (callback) {
  var ep = new EventProxy();
  ep.all("tpl", "data", function (tpl, data) {
    // 成功回调
    callback(null, {
      template: tpl,
      data: data,
    });
  });
  //绑定错误处理函数
  ep.fail(callback);
  fs.readFile("template.tpl", "utf-8", ep.done("tpl"));
  db.get("some sql", ep.done("data"));
};
```

在上述代码中，EventProxy 提供了 `fail()`和 `done()`这两个实例方法来优化异常处理，使得开发者将精力关注在业务部分，而不是在异常捕获上。

关于 `fail()`方法的实现，可以参见以下的变换：

```js
ep.fail(callback);
```

上面这行代码等价于下面的代码：

```js
ep.fail(function (err) {
  callback(err);
});
```

又等价于：

```js
ep.bind("error", function (err) {
  // 卸载所有处理函数
  ep.unbind();
  // 异常回调
  callback(err);
});
```

而 `done()`方法的实现，也可参见以下的变换：

```js
ep.done("tpl");
```

它等价于：

```js
function (err, content) {
  if (err) {
    // 一旦发生异常，一律交给error事件处理函数处理
    return ep.emit('error', err);
  }
  ep.emit('tpl', content);
}
```

同时，`done()`方法也接受一个函数作为参数，相关代码如下所示：

```js
ep.done(function (content) {
  // TODO
  // 这里无须考虑异常
  ep.emit("tpl", content);
});
```

这段代码等价于：

```js
function (err, content) {
  if (err) {
    // 一旦发生异常，一律交给error事件的处理函数处理
    return ep.emit('error', err);
  }
  (function (content) {
    // TODO
    // 这里无须考虑异常
    ep.emit('tpl', content);
  }(content));
}
```

当只传入一个回调函数时，需要手工调用 `emit()`触发事件。另一个改进是同时传入事件名和回调函数，相关代码如下：

```js
ep.done("tpl", function (content) {
  // content.replace('s', 'S');
  // TODO
  // 无须关注异常
  return content;
});
```

在这种方式下，我们无须在回调函数中处理事件的触发，只需将处理过的数据返回即可。返回的结果将在 `done()`方法中用作事件的数据而触发。

这里的 `fail()`和 `done()`十分类似 Promise 模式中的 `fail()`和 `done()`。换句话而言，这可以算作事件发布/订阅模式向 Promise 模式的借鉴。这样的完善既提升了程序的健壮性，同时也降低了代码量。

### 4.3.2 Promise/Deferred 模式

使用事件的方式时，执行流程需要被预先设定。即便是分支，也需要预先设定，这是由发布/订阅模式的运行机制所决定的。下面为普通的 Ajax 调用：

```js
$.get("/api", {
  success: onSuccess,
  error: onError,
  complete: onComplete,
});
```

在上面的异步调用中，必须严谨地设置目标。那么是否有一种先执行异步调用，延迟传递处理的方式呢？答案是 Promise/Deferred 模式。

Promise/Deferred 模式在 JavaScript 框架中最早出现于 Dojo 的代码中，被广为所知则来自于 jQuery 1.5 版本，该版本几乎重写了 Ajax 部分，使得调用 Ajax 时可以通过如下的形式进行：

```js
$.get("/api")
  .success(onSuccess)
  .error(onError)
  .complete(onComplete);
```

这使得即使不调用 `success()``、error()`等方法，Ajax 也会执行，这样的调用方式比预先传入回调让人觉得舒适一些。在原始的 API 中，一个事件只能处理一个回调，而通过 Deferred 对象，可以对事件加入任意的业务处理逻辑，示例代码如下：

```js
$.get("/api")
  .success(onSuccess1)
  .success(onSuccess2);
```

Promise/Deferred 模式在 2009 年时被 Kris Zyp 抽象为一个提议草案，发布在 CommonJS 规范中。随着使用 Promise/Deferred 模式的应用逐渐增多，CommonJS 草案目前已经抽象出了 Promises/A、Promises/B、Promises/D 这样典型的异步 Promise/Deferred 模型，这使得异步操作可以以一种优雅的方式出现。

异步的广度使用使得回调、嵌套出现，但是一旦出现深度的嵌套，就会让编程的体验变得不愉快，而 Promise/Deferred 模式在一定程度上缓解了这个问题。这里我们将着重介绍 Promises/A 来以点代面介绍 Promise/Deferred 模式。

1. Promises/A

Promise/Deferred 模式其实包含两部分，即 Promise 和 Deferred。这里暂且不提两者的区别是什么，先看看 Promises/A 的行为吧。

Promises/A 提议对单个异步操作做出了这样的抽象定义，具体如下所示。

- Promise 操作只会处在 3 种状态的一种：未完成态、完成态和失败态。
- Promise 的状态只会出现从未完成态向完成态或失败态转化，不能逆反。完成态和失败态不能互相转化。
- Promise 的状态一旦转化，将不能被更改。

Promise 的状态转化示意图如图 4-4 所示。

图 4-4 Promise 的状态转化示意图

在 API 的定义上，Promises/A 提议是比较简单的。一个 Promise 对象只要具备 `then()`方法即可。但是对于 `then()`方法，有以下简单的要求。

- 接受完成态、错误态的回调方法。在操作完成或出现错误时，将会调用对应方法。
- 可选地支持 progress 事件回调作为第三个方法。
- `then()`方法只接受 function 对象，其余对象将被忽略。
- `then()`方法继续返回 Promise 对象，以实现链式调用。

`then()`方法的定义如下：

```js
then(fulfilledHandler, errorHandler, progressHandler);
```

为了演示 Promises/A 提议，这里我们尝试通过继承 Node 的 events 模块来完成一个简单的实现，相关代码如下：

```js
var Promise = function () {
  EventEmitter.call(this);
};
util.inherits(Promise, EventEmitter);
Promise.prototype.then = function (
  fulfilledHandler,
  errorHandler,
  progressHandler
) {
  if (typeof fulfilledHandler === "function") {
    // 利用once()方法，保证成功回调只执行一次
    this.once("success", fulfilledHandler);
  }
  if (typeof errorHandler === "function") {
    // 利用once()方法，保证异常回调只执行一次
    this.once("error", errorHandler);
  }
  if (typeof progressHandler === "function") {
    this.on("progress", progressHandler);
  }
  return this;
};
```

这里看到 `then()`方法所做的事情是将回调函数存放起来。为了完成整个流程，还需要触发执行这些回调函数的地方，实现这些功能的对象通常被称为 Deferred，即延迟对象，示例代码如下：

```js
var Deferred = function () {
  this.state = "unfulfilled";
  this.promise = new Promise();
};
Deferred.prototype.resolve = function (obj) {
  this.state = "fulfilled";
  this.promise.emit("success", obj);
};
Deferred.prototype.reject = function (err) {
  this.state = "failed";
  this.promise.emit("error", err);
};
Deferred.prototype.progress = function (data) {
  this.promise.emit("progress", data);
};
```

这里的状态和方法之间的对应关系如图 4-5 所示。

图 4-5 状态和方法之间的对应关系

利用 Promises/A 提议的模式，我们可以对一个典型的响应对象进行封装，相关代码如下：

```js
res.setEncoding("utf8");
res.on("data", function (chunk) {
  console.log("BODY: " + chunk);
});
res.on("end", function () {
  // Done
});
res.on("error", function (err) {
  // Error
});
```

上述代码可以转换为如下的简略形式：

```js
res.then(
  function () {
    // Done
  },
  function (err) {
    // Error
  },
  function (chunk) {
    console.log("BODY: " + chunk);
  }
);
```

要实现如此简单的 API，只需要简单地改造一下即可，相关代码如下：

```js
var promisify = function (res) {
  var deferred = new Deferred();
  var result = "";
  res.on("data", function (chunk) {
    result += chunk;
    deferred.progress(chunk);
  });
  res.on("end", function () {
    deferred.resolve(result);
  });
  res.on("error", function (err) {
    deferred.reject(err);
  });
  return deferred.promise;
};
```

如此就得到了简单的结果。这里返回 deferred.promise 的目的是为了不让外部程序调用 `resolve()`和 `reject()`方法，更改内部状态的行为交由定义者处理。下面为定义好 Promise 后的调用示例：

```js
promisify(res).then(
  function () {
    // Done
  },
  function (err) {
    // Error
  },
  function (chunk) {
    // progress
    console.log("BODY: " + chunk);
  }
);
```

这里回到 Promise 和 Deferred 的差别上。从上面的代码可以看出，Deferred 主要是用于内部，用于维护异步模型的状态；Promise 则作用于外部，通过 `then()`方法暴露给外部以添加自定义逻辑。Promise 和 Deferred 的整体关系如图 4-6 所示。

图 4-6 Promise 和 Deferred 整体关系示意图

与事件发布/订阅模式相比，Promise/Deferred 模式的 API 接口和抽象模型都十分简洁。从图 4-6 中也可以看出，它将业务中不可变的部分封装在了 Deferred 中，将可变的部分交给了 Promise。此时问题就来了，对于不同的场景，都需要去封装和改造其 Deferred 部分，然后才能得到简洁的接口。如果场景不常用，封装花费的时间与带来的简洁相比并不一定划算。

Promise 是高级接口，事件是低级接口。低级接口可以构成更多更复杂的场景，高级接口一旦定义，不太容易变化，不再有低级接口的灵活性，但对于解决典型问题非常有效。Promises/A 的模型抽象在几种 Promise 提议中相对简洁。

这里再介绍一下 Q。Q 模块是 Promises/A 规范的一个实现，可以通过 `npm install q` 进行安装使用。它对 Node 中常见回调函数的 Promise 实现如下：

```js
/**
 * Creates a Node-style callback that will resolve or reject the deferred
 * promise.
 * @returns a nodeback
 */
defer.prototype.makeNodeResolver = function () {
  var self = this;
  return function (error, value) {
    if (error) {
      self.reject(error);
    } else if (arguments.length > 2) {
      self.resolve(array_slice(arguments, 1));
    } else {
      self.resolve(value);
    }
  };
};
```

可以看到这里是一个高阶函数的使用，makeNodeResolver 返回了一个 Node 风格的回调函数。对于 `fs.readFile()`的调用，将会演化为如下形式：

```js
var readFile = function (file, encoding) {
  var deferred = Q.defer();
  fs.readFile(file, encoding, deferred.makeNodeResolver());
  return deferred.promise;
};
```

定义之后的调用示例如下：

```js
readFile("foo.txt", "utf-8").then(
  function (data) {
    // Success case
  },
  function (err) {
    // Failed case
  }
);
```

Promise 通过封装异步调用，实现了正向用例和反向用例的分离以及逻辑处理延迟，这使得回调函数相对优雅。

前面分析了 Q 对 Node 异步回调的处理。事实上，异步编程中需要花费很多精力进行异常的判断和处理，为了分离异常和正常情况，我写了一个模块 memeda 用于处理 makeNodeResolver 相似的事情。在下面的调用示例中可以看到，正常结果和异常结果被分离到两个函数中：

```js
var failing = require("memeda").failing;
fs.readFile(
  file,
  encoding,
  failing(function (err) {
    // TODO
  }).passing(function (data) {
    // TODO
  })
);
```

我们可以对 Q 和 memeda 模块略做比较。两者相似之处在于分离逻辑，使开发者侧重关注正常情况。不同之处在于 Q 通过 `promise()`可以实现延迟处理，以及通过多次调用 `then()`附加更多结果处理逻辑。可以看到，Promise 需要封装，但是强大，具备很强的侵入性；纯粹的函数则较为轻量，但功能相对弱小。

2. Promise 中的多异步协作

在 Promise 的介绍中说过，主要解决的是单个异步操作中存在的问题。回到我们的难点，当我们需要处理多个异步调用时，又该如何处理呢？

类似于 EventProxy，这里给出了一个简单的原型实现，相关代码如下：

```js
Deferred.prototype.all = function (promises) {
  var count = promises.length;
  var that = this;
  var results = [];
  promises.forEach(function (promise, i) {
    promise.then(
      function (data) {
        count--;
        results[i] = data;
        if (count === 0) {
          that.resolve(results);
        }
      },
      function (err) {
        that.reject(err);
      }
    );
  });
  return this.promise;
};
```

对于多次文件的读取场景，以下面的代码为例，`all()`方法将两个单独的 Promise 重新抽象组合成一个新的 Promise：

```js
var promise1 = readFile("foo.txt", "utf-8");
var promise2 = readFile("bar.txt", "utf-8");
var deferred = new Deferred();
deferred.all([promise1, promise2]).then(
  function (results) {
    // TODO
  },
  function (err) {
    // TODO
  }
);
```

这里通过 `all()`方法抽象多个异步操作。只有所有异步操作成功，这个异步操作才算成功，一旦其中一个异步操作失败，整个异步操作就失败。

本节的代码主要用于描述 Promise 的原理，在成熟度上并未如 when 和 Q 模块。在实际的应用中，可以通过 NPM 安装这两个模块，它们是完整的 Promise 提议的实现。

3. Promise 的进阶知识

在 API 的暴露上，Promise 模式比原始的事件侦听和触发略为优美，它的缺陷则是需要为不同的场景封装不同的 API，没有直接的原生事件那么灵活。但对于经典的场景，封装出 API 的成本也并不高，值得一做。

Promise 的秘诀其实在于对队列的操作。这里介绍一个实际的案例，我在处理自动化测试时，要跟远程服务器之间进行多次指令发送，这些指令是按顺序依次进行的。在 Node 中，网络库是完全异步的，无法在编程层面实现像其他语言那般的同步调用。由于网站界面通常都是由前端工程师完成的，用 JavaScript 编写自动化测试可以减轻他们切换环境的痛苦，所以不能因为无法同步调用就放弃掉 Node。解决同步调用问题的答案也就是采用 Deferred 模式。

现在有一组纯异步的 API，为了完成一串事情，我们的代码大致如下：

```js
obj.api1(function (value1) {
  obj.api2(value1, function (value2) {
    obj.api3(value2, function (value3) {
      obj.api4(value3, function (value4) {
        callback(value4);
      });
    });
  });
});
```

由于有按每个步骤依次执行的需求，所以必须嵌套执行。但那样我们会得到难看的嵌套，超过 10 个连续嵌套就会让代码十分难看。于是我们得到了“Pyramid ofDoom”，译为中文，是谓“恶魔金字塔”。相信初入 Node 世界的人，也写过不少此类代码。

下面我们通过普通的函数将上面的代码尝试展开：

```js
var handler1 = function (value1) {
  obj.api2(value1, handler2);
};
var handler2 = function (value2) {
  obj.api3(value2, handler3);
};
var handler3 = function (value3) {
  obj.api4(value3, hander4);
};
var handler4 = function (value4) {
  callback(value4);
});

obj.api1(handler1);
```

对于喜欢利用事件的开发者，我们展开后的代码又将会是怎样的情况呢？具体如下所示：

```js
var emitter = new event.Emitter();
emitter.on("step1", function () {
  obj.api1(function (value1) {
    emitter.emit("step2", value1);
  });
});
emitter.on("step2", function (value1) {
  obj.api2(value1, function (value2) {
    emitter.emit("step3", value2);
  });
});
emitter.on("step3", function (value2) {
  obj.api3(value2, function (value3) {
    emitter.emit("step4", value3);
  });
});
emitter.on("step4", function (value3) {
  obj.api4(value3, function (value4) {
    callback(value4);
  });
});
emitter.emit("step1");
```

利用事件展开后的效果变得越来越糟糕了。与纯粹嵌套相比，代码量明显增加了，这显然不会带来良好的编程体验。为此，我们需要一种更好的方式。

**支持序列执行的 Promise**

理想的编程体验应当是前一个的调用结果作为下一个调用的开始，是传说中的链式调用，相关代码如下：

```js
promise()
  .then(obj.api1)
  .then(obj.api2)
  .then(obj.api3)
  .then(obj.api4)
  .then(
    function (value4) {
      // Do something with value4
    },
    function (error) {
      // Handle any error from step1 through step4
    }
  )
  .done();
```

尝试改造一下代码以实现链式调用，具体如下所示：

```js
var Deferred = function () {
  this.promise = new Promise();
};
//完成态
Deferred.prototype.resolve = function (obj) {
  var promise = this.promise;
  var handler;
  while ((handler = promise.queue.shift())) {
    if (handler && handler.fulfilled) {
      var ret = handler.fulfilled(obj);
      if (ret && ret.isPromise) {
        ret.queue = promise.queue;
        this.promise = ret;
        return;
      }
    }
  }
};
//失败态
Deferred.prototype.reject = function (err) {
  var promise = this.promise;
  var handler;
  while ((handler = promise.queue.shift())) {
    if (handler && handler.error) {
      var ret = handler.error(err);
      if (ret && ret.isPromise) {
        ret.queue = promise.queue;
        this.promise = ret;
        return;
      }
    }
  }
};
// 生成回调函数
Deferred.prototype.callback = function () {
  var that = this;
  return function (err, file) {
    if (err) {
      return that.reject(err);
    }
    that.resolve(file);
  };
};
var Promise = function () {
  // 队列用于存储待执行的回调函数
  this.queue = [];
  this.isPromise = true;
};
Promise.prototype.then = function (
  fulfilledHandler,
  errorHandler,
  progressHandler
) {
  var handler = {};
  if (typeof fulfilledHandler === "function") {
    handler.fulfilled = fulfilledHandler;
  }
  if (typeof errorHandler === "function") {
    handler.error = errorHandler;
  }
  this.queue.push(handler);
  return this;
};
```

这里我们以两次文件读取作为例子，以验证该设计的可行性。这里假设读取第二个文件是依赖于第一个文件中的内容的，相关代码如下：

```js
var readFile1 = function (file, encoding) {
  var deferred = new Deferred();
  fs.readFile(file, encoding, deferred.callback());
  return deferred.promise;
};
var readFile2 = function (file, encoding) {
  var deferred = new Deferred();
  fs.readFile(file, encoding, deferred.callback());
  return deferred.promise;
};
readFile1("file1.txt", "utf8")
  .then(function (file1) {
    return readFile2(file1.trim(), "utf8");
  })
  .then(function (file2) {
    console.log(file2);
  });
```

将这段代码存为 sequence.js 文件。执行该代码，将会得到以下的输出结果：

```
$ node sequence.js
I am file2
```

要让 Promise 支持链式执行，主要通过以下两个步骤。

1. 将所有的回调都存到队列中。
2. Promise 完成时，逐个执行回调，一旦检测到返回了新的 Promise 对象，停止执行，然后将当前 Deferred 对象的 promise 引用改变为新的 Promise 对象，并将队列中余下的回调转交给它。

写到这里，你是否明了恶魔金字塔该如何优化？

再次重申，这里的代码主要用于研究 Promise 的实现原理。在更多细节的优化方面，Q 或者 when 等 Promise 库做得更好，实际应用时请采用这些成熟库。

**将 API Promise 化**

这里仍然会发现，为了体验更好的 API，需要做较多的准备工作。这里提供了一个方法可以批量将方法 Promise 化，相关代码如下：

```js
// smooth(fs.readFile);
var smooth = function (method) {
  return function () {
    var deferred = new Deferred();
    var args = Array.prototype.slice.call(arguments, 1);
    args.push(deferred.callback());
    method.apply(null, args);
    return deferred.promise;
  };
};
```

于是前面的两次文件读取的构造：

```js
var readFile1 = function (file, encoding) {
  var deferred = new Deferred();
  fs.readFile(file, encoding, deferred.callback());
  return deferred.promise;
};
var readFile2 = function (file, encoding) {
  var deferred = new Deferred();
  fs.readFile(file, encoding, deferred.callback());
  return deferred.promise;
};
```

可以简化为：

```js
var readFile = smooth(fs.readFile);
```

要实现同样的效果，代码量将会锐减到：

```js
var readFile = smooth(fs.readFile);
readFile("file1.txt", "utf8")
  .then(function (file1) {
    return readFile(file1.trim(), "utf8");
  })
  .then(function (file2) {
    // file2 => I am file2
    console.log(file2);
  });
```

### 4.3.3 流程控制库

前面叙述了最为主流的模式——事件发布/订阅模式和 Promise/Deferred 模式，这些是经典的模式或者是写进规范里的解决方案，但一旦涉及模式或者规范，就需要为它们做较多的准备工作。这一节将会介绍一些非模式化的应用，虽非规范，但更灵活。

1. 尾触发与 Next

除了事件和 Promise 外，还有一类方法是需要手工调用才能持续执行后续调用的，我们将此类方法叫做尾触发，常见的关键词是 next。事实上，尾触发目前应用最多的地方是 Connect 的中间件。

这里我们暂且不关注 Connect 的具体应用，先看一下 Connect 的 API 暴露方式，相关代码如下：

```js
var app = connect();
// Middleware
app.use(connect.staticCache());
app.use(connect.static(__dirname + "/public"));
app.use(connect.cookieParser());
app.use(connect.session());
app.use(connect.query());
app.use(connect.bodyParser());
app.use(connect.csrf());
app.listen(3001);
```

在通过 `use()`方法注册好一系列中间件后，监听端口上的请求。中间件利用了尾触发的机制，最简单的中间件如下：

```js
function (req, res, next) {
  // 中间件
}
```

每个中间件传递请求对象、响应对象和尾触发函数，通过队列形成一个处理流，如图 4-7 所示。

图 4-7 中间件通过队列形成一个处理流中间件机制使得在处理网络请求时，可以像面向切面编程一样进行过滤、验证、日志等功能，而不与具体业务逻辑产生关联，以致产生耦合。

下面我们来看 Connect 的核心实现，相关代码如下：

```js
function createServer() {
  function app(req, res) {
    app.handle(req, res);
  }
  utils.merge(app, proto);
  utils.merge(app, EventEmitter.prototype);
  app.route = "/";
  app.stack = [];
  for (var i = 0; i < arguments.length; ++i) {
    app.use(arguments[i]);
  }
  return app;
}
```

这段代码通过如下代码创建了 HTTP 服务器的 request 事件处理函数：

```js
function app(req, res) {
  app.handle(req, res);
}
```

但真正的核心代码是 `app.stack = [];`这句。stack 属性是这个服务器内部维护的中间件队列。通过调用 `use()`方法我们可以将中间件放进队列中。下面的代码为 `use()`方法的重要部分：

```js
app.use = function (route, fn) {
  // some code
  this.stack.push({ route: route, handle: fn });
  return this;
};
```

此时就建好处理模型了。接下来，结合 Node 原生 http 模块实现监听即可。监听函数的实现如下：

```js
app.listen = function () {
  var server = http.createServer(this);
  return server.listen.apply(server, arguments);
};
```

最终回到 `app.handle()`方法，每一个监听到的网络请求都将从这里开始处理。该方法的代码如下：

```js
app.handle = function (req, res, out) {
  // some code
  next();
};
```

原始的 `next()`方法较为复杂，下面是简化后的内容，其原理十分简单，取出队列中的中间件并执行，同时传入当前方法以实现递归调用，达到持续触发的目的：

```js
function next(err) {
  // some code
  // next callback
  layer = stack[index++];
  layer.handle(req, res, next);
}
```

所有嫌异步编程复杂的开发者均可以参考 Connect 的流式处理，这对于划分业务逻辑、逐步处理均有效。

值得提醒的是，尽管中间件这种尾触发模式并不要求每个中间方法都是异步的，但是如果每个步骤都采用异步来完成，实际上只是串行化的处理，没办法通过并行的异步调用来提升业务的处理效率。流式处理可以将一些串行的逻辑扁平化，但是并行逻辑处理还是需要搭配事件或者 Promise 完成的，这样业务在纵向和横向都能够各自清晰。

在 Connect 中，尾触发十分适合处理网络请求的场景。将复杂的处理逻辑拆解为简洁、单一的处理单元，逐层次地处理请求对象和响应对象。

2. async

接下来，我们要介绍最知名的流程控制模块 async。async 长期占据 NPM 依赖榜的前三名，可见在 Node 开发中，流程控制是开发过程中的基本需求。async 模块提供了 20 多个方法用于处理异步的各种协作模式，这里我们介绍几种典型用法。

**异步的串行执行**

这里我们依旧采用前面读取两个文件的例子，看一下 async 是如何解决“恶魔金字塔”问题的。

async 提供了 `series()`方法来实现一组任务的串行执行，示例代码如下：

```js
async.series(
  [
    function (callback) {
      fs.readFile("file1.txt", "utf-8", callback);
    },
    function (callback) {
      fs.readFile("file2.txt", "utf-8", callback);
    },
  ],
  function (err, results) {
    // results => [file1.txt, file2.txt]
  }
);
```

这段代码等价于：

```js
fs.readFile("file1.txt", "utf-8", function (err, content) {
  if (err) {
    return callback(err);
  }
  fs.readFile("file2.txt ", "utf-8", function (err, data) {
    if (err) {
      return callback(err);
    }
    callback(null, [content, data]);
  });
});
```

这段代码值得玩味的是回调函数。可以发现，`series()`方法中传入的函数 `callback()`并非由使用者指定。事实上，此处的回调函数由 async 通过高阶函数的方式注入，这里隐含了特殊的逻辑。每个 `callback()`执行时会将结果保存起来，然后执行下一个调用，直到结束所有调用。最终的回调函数执行时，队列里的异步调用保存的结果以数组的方式传入。这里的异常处理规则是一旦出现异常，就结束所有调用，并将异常传递给最终回调函数的第一个参数。

**异步的并行执行**

当我们需要通过并行来提升性能时，async 提供了 `parallel()`方法，用以并行执行一些异步操作。以下为读取两个文件的并行版本：

```js
async.parallel(
  [
    function (callback) {
      fs.readFile("file1.txt", "utf-8", callback);
    },
    function (callback) {
      fs.readFile("file2.txt", "utf-8", callback);
    },
  ],
  function (err, results) {
    // results => [file1.txt, file2.txt]
  }
);
```

上面这段代码等价于下面的代码：

```js
var counter = 2;
var results = [];
var done = function (index, value) {
  results[index] = value;
  counter--;
  if (counter === 0) {
    callback(null, results);
  }
};
// 只传递第一个异常
var hasErr = false;
var fail = function (err) {
  if (!hasErr) {
    hasErr = true;
    callback(err);
  }
};
fs.readFile("file1.txt", "utf-8", function (err, content) {
  if (err) {
    return fail(err);
  }
  done(0, content);
});
fs.readFile("file2.txt", "utf-8", function (err, data) {
  if (err) {
    return fail(err);
  }
  done(1, data);
});
```

同样，通过 async 编写的代码既没有深度的嵌套，也没有复杂的状态判断，它的诀窍依然来自于注入的回调函数。`parallel()`方法对于异常的判断依然是一旦某个异步调用产生了异常，就会将异常作为第一个参数传入给最终的回调函数。只有所有异步调用都正常完成时，才会将结果以数组的方式传入。

也许你还记得 EventProxy 的方案，如下所示：

```js
var EventProxy = require("eventproxy");
var proxy = new EventProxy();
proxy.all("content", "data", function (content, data) {
  callback(null, [content, data]);
});
proxy.fail(callback);
fs.readFile("file1.txt", "utf-8", proxy.done("content"));
fs.readFile("file2.txt", "utf-8", proxy.done("data"));
```

与通过 async 编写所产生的代码量相差并不大。EventProxy 虽然基于事件发布/订阅模式而设计，但也用到了与 async 相同的原理，通过特殊的回调函数来隐含返回值的处理。所不同的是，在 async 的框架模式下，这个回调函数由 async 封装后传递出来，而 EventProxy 则通过 `done()`和 `fail()`方法来生成新的回调函数。这两种实现方式都是高阶函数的应用。

**异步调用的依赖处理**

`series()`适合无依赖的异步串行执行，但当前一个的结果是后一个调用的输入时，`series()`方法就无法满足需求了。所幸，这种典型场景的需求，async 提供了 `waterfall()`方法来满足，相关代码如下：

```js
async.waterfall(
  [
    function (callback) {
      fs.readFile("file1.txt", "utf-8", function (err, content) {
        callback(err, content);
      });
    },
    function (arg1, callback) {
      // arg1 => file2.txt
      fs.readFile(arg1, "utf-8", function (err, content) {
        callback(err, content);
      });
    },
    function (arg1, callback) {
      // arg1 => file3.txt
      fs.readFile(arg1, "utf-8", function (err, content) {
        callback(err, content);
      });
    },
  ],
  function (err, result) {
    // result => file4.txt
  }
);
```

这段代码等价于如下代码：

```js
fs.readFile("file1.txt", "utf-8", function (err, data1) {
  if (err) {
    return callback(err);
  }
  fs.readFile(data1, "utf-8", function (err, data2) {
    if (err) {
      return callback(err);
    }
    fs.readFile(data2, "utf-8", function (err, data3) {
      if (err) {
        return callback(err);
      }
      callback(null, data3);
    });
  });
});
```

**自动依赖处理**

在现实的业务环境中，具有很多复杂的依赖关系，这些业务或是异步，或是同步。这种混杂的编程环境经常让人处于理不清顺序的情况。为此，async 提供了一个强大的方法 `auto()`实现复杂业务处理。

假设我们的业务场景如下：

1. 从磁盘读取配置文件。
2. 根据配置文件连接 MongoDB。
3. 根据配置文件连接 Redis。
4. 编译静态文件。
5. 上传静态文件到 CDN。
6. 启动服务器。

简单映射一下上述业务：

```js
{
  readConfig: function () {},
  connectMongoDB: function () {},
  connectRedis: function () {},
  complieAsserts: function () {},
  uploadAsserts: function () {},
  startup: function () {}
}
```

接下来分析一下依赖关系。可以看出，connectMongoDB 和 connectRedis 依赖 readConfig, uploadAsserts 依赖 complieAsserts, startup 则依赖所有完成。依赖关系如下：

```js
var deps = {
  readConfig: function (callback) {
    // read config file
    callback();
  },
  connectMongoDB: [
    "readConfig",
    function (callback) {
      // connect to mongodb
      callback();
    },
  ],
  connectRedis: [
    "readConfig",
    function (callback) {
      // connect to redis
      callback();
    },
  ],
  complieAsserts: function (callback) {
    // complie asserts
    callback();
  },
  uploadAsserts: [
    "complieAsserts",
    function (callback) {
      // upload to assert
      callback();
    },
  ],
  startup: [
    "connectMongoDB",
    "connectRedis",
    "uploadAsserts",
    function (callback) {
      // startup
    },
  ],
};
```

`auto()`方法能根据依赖关系自动分析，以最佳的顺序执行以上业务：

```js
async.auto(deps);
```

转换到 EventProxy 的实现，则需要更细腻的事件分配，相关代码如下：

```js
proxy
  .assp("readtheconfig", function () {
    // read config file
    proxy.emit("readConfig");
  })
  .on("readConfig", function () {
    // connect to mongodb
    proxy.emit("connectMongoDB");
  })
  .on("readConfig", function () {
    // connect to redis
    proxy.emit("connectRedis");
  })
  .assp("complietheasserts", function () {
    // complie asserts
    proxy.emit("complieAsserts");
  })
  .on("complieAsserts", function () {
    // upload to assert
    proxy.emit("uploadAsserts");
  })
  .all("connectMongoDB", "connectRedis", "uploadAsserts", function () {
    // Startup
  });
```

**小结**

本节主要介绍 async 的几种常见用法。此外，async 还提供了 forEach、map 等类 ECMAScript5 中数组的方法，更多细节可关注 https://github.com/caolan/async 。

3. Step

另一个知名的流程控制库是 Tim Caswell 的 Step，它比 async 更轻量，在 API 的暴露上也更具备一致性，因为它只有一个接口 Step。通过 `npm install step` 即可安装使用。示例代码如下：

```js
Step(task1, task2, task3);
```

Step 接受任意数量的任务，所有的任务都将会串行依次执行。下面的示例代码将依次读取文件：

```js
Step(
  function readFile1() {
    fs.readFile("file1.txt", "utf-8", this);
  },
  function readFile2(err, content) {
    fs.readFile("file2.txt", "utf-8", this);
  },
  function done(err, content) {
    console.log(content);
  }
);
```

可以看到，Step 与前面介绍的事件模式、Promise 甚至 async 都不同的一点在于 Step 用到了 this 关键字。事实上，它是 Step 内部的一个 `next()`方法，将异步调用的结果传递给下一个任务作为参数，并调用执行。

**并行任务执行**

那么，Step 如何实现多个异步任务并行执行呢？this 具有一个 `parallel()`方法，它告诉 Step，需要等所有任务完成时才进行下一个任务，相关代码如下：

```js
Step(
  function readFile1() {
    fs.readFile("file1.txt", "utf-8", this.parallel());
    fs.readFile("file2.txt", "utf-8", this.parallel());
  },
  function done(err, content1, content2) {
    // content1 => file1
    // content2 => file2
    console.log(arguments);
  }
);
```

使用 `parallel()`的时候需要小心的是，如果异步方法的结果传回的是多个参数，Step 将只会取前两个参数，相关代码如下：

```js
var asyncCall = function (callback) {
  process.nextTick(function () {
    callback(null, "result1", "result2");
  });
};
```

在调用 `parallel()`时，result2 将会被丢弃。

Step 的 `parallel()`方法的原理是每次执行时将内部的计数器加 1，然后返回一个回调函数，这个回调函数在异步调用结束时才执行。当回调函数执行时，将计数器减 1。当计数器为 0 的时候，告知 Step 所有异步调用结束了，Step 会执行下一个方法。

Step 与 async 相同的是异常处理，一旦有一个异常产生，这个异常会作为下一个方法的第一个参数传入。

**结果分组**

Step 提供的另外一个方法是 `group()`，它类似于 `parallel()`的效果，但是在结果传递上略有不同。下面的代码用于读取一个目录，然后迭代其中文件的操作：

```js
Step(
  function readDir() {
    fs.readdir(__dirname, this);
  },
  function readFiles(err, results) {
    if (err) throw err;
    // Create a new group
    var group = this.group();
    results.forEach(function (filename) {
      if (/\.js$/.test(filename)) {
        fs.readFile(__dirname + "/" + filename, "utf8", group());
      }
    });
  },
  function showAll(err, files) {
    if (err) throw err;
    console.dir(files);
  }
);
```

我们注意到有两次 `group()`的调用。第一次调用是告知 Step 要并行执行，第二次调用的结果将会生成一个回调函数，而回调函数接受的返回值将会按组存储。`parallel()`传递给下一个任务的结果是如下形式：

```js
function (err, result1, result2, ...);
```

`group()`传递的结果是：

```js
function (err, results);
```

这个函数返回的数据保存在数组中。

4. wind

这里还要介绍一种思路完全不同的异步编程方案[wind](https://github.com/JeffreyZhao/wind)。它的前身为 Jscex，由国内知名码农赵劼完成开发。它为 JavaScript 语言提供了一个 monadic 扩展，能够显著提高一些常见场景下的异步编程体验。

异步编程有时需要面临的场景非常特殊，下面我们由一个冒泡排序来了解 wind 的特殊之处：

```js
var compare = function (x, y) {
  return x - y;
};
var swap = function (a, i, j) {
  var t = a[i];
  a[i] = a[j];
  a[j] = t;
};
var bubbleSort = function (array) {
  for (var i = 0; i < array.length; i++) {
    for (var j = 0; j < array.length - i - 1; j++) {
      if (compare(array[j], array[j + 1]) > 0) {
        swap(array, j, j + 1);
      }
    }
  }
};
```

现在我们要添加的需求是，将这个冒泡排序动画起来。这意味着在 `swap()`方法中需要添加动画逻辑，这在 JavaScript 中并不是一件难事，困难的地方在于动画需要延时的方式完成。但在 JavaScript 中只有 `setTimeout()`能够实现延时功能（用 while 判断时间的方式不可取，这在前面有所描述）。我们知道，`setTimeout()`是一个异步方法，在执行后，将立即返回。所以，难点出现在：

- 动画执行时无法停止排序算法的执行；
- 排序算法的继续执行将会启动更多动画。

因此，逐步骤的动画将难以实现，而 wind 在解决这个问题上体现出了它的独特魅力之处，相关代码如下：

```js
var compare = function (x, y) {
  return x - y;
};
var swapAsync = eval(
  Wind.compile("async", function (a, i, j) {
    $await(Wind.Async.sleep(20)); // 暂停20毫秒
    var t = a[i];
    a[i] = a[j];
    a[j] = t;
    paint(a); // 重重绘数组
  })
);
var bubbleSort = eval(
  Wind.compile("async", function (array) {
    for (var i = 0; i < array.length; i++) {
      for (var j = 0; j < array.length - i - 1; j++) {
        if (compare(array[j], array[j + 1]) > 0) {
          $await(swapAsync(array, j, j + 1));
        }
      }
    }
  })
);
```

上述代码实现了暂停 20 毫秒、绘制动画、继续排序的效果。从代码的角度来说，这里虽然介入了异步方法，但是并没有如同其他异步流程控制库那样变得异步化，逻辑并没有因为异步被拆分。同时可以注意到，我们的代码中引入了一些新的东西：

- `eval(Wind.compile("async", function() {}));`
- `$await();`
- `Wind.Async.sleep(20);`

下面我们将详细介绍以上 3 行代码的特异之处。

**异步任务定义**

`eval()`函数在业界一向是一个需要谨慎对待的函数，Douglas Crockford 更是深恶痛绝地将其称为魔鬼，因为它能访问上下文和编译器，可能导致上下文混乱。大多数利用 `eval()`函数的人都不能把握好它的用法，导致 Douglas Crockford 认为它是 JavaScript 可有可无的功能。

但是在 wind 的世界里，恰好反 Douglas Crockford 之道而行之，巧妙地利用了 `eval()`访问上下文的特性。`Wind.compile()`会将普通的函数进行编译，然后交给 `eval()`执行。换言之，`eval(Wind.compile("async", function () {}));`定义了异步任务。`Wind.Async.sleep();`则内置了对 `setTimeout()`的封装。

**$await()与任务模型**

在定义完异步方法后，wind 提供了`$await()`方法实现等待完成异步方法。但事实上，它并不是一个方法，也不存在于上下文中，只是一个等待的占位符，告之编译器这里需要等待。

`$await()`接受的参数是一个任务对象，表示等待任务结束后才会执行后续操作。每一个异步操作都可以转化为一个任务，wind 正是基于任务模型实现的。下面的代码用于将 `fs.readFile()`调用转化为一个任务模型：

```js
var Wind = require("wind");
var Task = Wind.Async.Task;

var readFileAsync = function (file, encoding) {
  return Task.create(function (t) {
    fs.readFile(file, encoding, function (err, file) {
      if (err) {
        t.complete("failure", err);
      } else {
        t.complete("success", file);
      }
    });
  });
};
```

除了通过 `eval(Wind.compile("async", function () {}));`定义任务外，正式的任务创建方法为 `Task.create()`。执行 `readFileAsync()`进行偏函数转换得到真正的任务。异步方法在执行结束时，可以通过 `complete()`传递 failure 或 success 信息，告知任务执行完毕。如果是 failure 则可以通过 try/catch 捕获异常。这略微有些打破前述 try/catch 无法捕获回调函数中异常的定论。下面的代码为调用 `readFileAsync()`得到一个任务的示例：

```js
var task = readFileAsync("file1.txt", "utf-8");
```

下面我们如同介绍 async 或者 Step 的串行执行示例一样，尝试感受一下 wind 的风采：

```js
var serial = eval(
  Wind.compile("async", function () {
    var file1 = $await(readFileAsync("file1.txt", "utf-8"));
    console.log(file1);
    var file2 = $await(readFileAsync("file2.txt", "utf-8"));
    console.log(file2);
    try {
      var file3 = $await(readFileAsync("file3.txt", "utf-8"));
    } catch (err) {
      console.log(err);
    }
  })
);
serial().start();
```

执行上述代码，将得到如下输出：

```
file1
file2
{ [Error: ENOENT, open 'file3.txt'] errno: 34, code: 'ENOENT', path: 'file3.txt' }
```

异步方法在 JavaScript 中通常会立即返回，在 wind 中做到了不阻塞 CPU 但阻塞代码的目的。接下来我们尝试下并行的效果，相关代码如下：

```js
var parallel = eval(
  Wind.compile("async", function () {
    var result = $await(
      Task.whenAll({
        file1: readFileAsync("file1.txt", "utf-8"),
        file2: readFileAsync("file2.txt", "utf-8"),
      })
    );
    console.log(result.file1);
    console.log(result.file2);
  })
);
parallel().start();
```

得到输出：

```
file1
file2
```

wind 提供了 `whenAll()`来处理并发，通过`$await`关键字将等待配置的所有任务完成后才向下继续执行。

**异步方法转换辅助函数**

可以看到，除了 `eval(Wind.compile("async", function () {}))`在实际代码中稍显冗长外，异步调用在代码层面上已经与同步调用相差无几。这十分适合从已有的采用同步编写方式的代码向 Node 迁移，可以省掉重写代码的开销。

如同 Promise/Deferred 模式可以让异步编程模型变简单，这种近同步编程的体验需要我们额外或者提前完成的事情是：将异步方法任务化。这种任务化的过程可以看作是 Promise/Deferred 的封装。如果每个方法都如 readFileAsync 一般去定义，将会是一个庞大的工作量。wind 提供了两个方法来辅助转换：

- Wind.Async.Binding.fromCallback
- Wind.Async.Binding.fromStandard

在 Node 中异步方法的回调传值有两种，一种是无异常的调用，通常只有一个参数返回，如下所示：

```js
fs.exists("/etc/passwd", function (exists) {
  // exists参数表示是否存在
});
```

而 fromCallback 用于转换这类异步调用为 wind 中的任务。

另一类是带异常的调用，遵循规范将返回参数列表的第一个参数作为异常标示，如下所示：

```js
fs.readFile("file1.txt", function (err, data) {
  // err表示异常
});
```

而 fromStandard 用于转换这类异步调用到 wind 中的任务。

是故，readFileAsync 的定义其实只要一行代码即可实现：

```js
var readFileAsync = Wind.Async.Binding.fromStandard(fs.readFile);
```

5. 流程控制小结

从本书介绍的各个流程控制案例来看，从解决“恶魔金字塔”到解决异步协作的方法有多种，几个类库几乎各显神通。异步编程虽然相对复杂，但并非难事，相同的问题通过各种技巧依然能将复杂的事情简化。

这里简单对比下几种方案的区别：事件发布/订阅模式相对算是一种较为原始的方式，Promise/Deferred 模式贡献了一个非常不错的异步任务模型的抽象。而上述的这些异步流程控制方案与 Promise/Deferred 模式的思路不同，Promise/Deferred 的重头在于封装异步的调用部分，流程控制库则显得没有模式，将处理重点放置在回调函数的注入上。从自由度上来讲，async、Step 这类流控库要相对灵活得多。EventProxy 库则主要借鉴事件发布/订阅模式和流程控制库通过高阶函数生成回调函数的方式实现。

除了 async、Step、EventProxy、wind 等方案外，还有一类通过源代码编译的方案来实现流程控制的简化，streamline 是典型的例子。这类例子并不在本章的讨论范围内，如果读者有兴趣，可以自行查阅相关资料。

## 4.4 异步并发控制

在陆续介绍的各种异步编程方法里，解决的问题无外乎保持异步的性能优势，提升编程体验，但是这里有一个过犹不及的案例。

在 Node 中，我们可以十分方便地利用异步发起并行调用。使用下面的代码，我们可以轻松发起 100 次异步调用：

```js
for (var i = 0, i < 100; i++) {
async();
}
```

但是如果并发量过大，我们的下层服务器将会吃不消。如果是对文件系统进行大量并发调用，操作系统的文件描述符数量将会被瞬间用光，抛出如下错误：

```
Error: EMFILE, too many open files
```

可以看出，异步 I/O 与同步 I/O 的显著差距：同步 I/O 因为每个 I/O 都是彼此阻塞的，在循环体中，总是一个接着一个调用，不会出现耗用文件描述符太多的情况，同时性能也是低下的；对于异步 I/O，虽然并发容易实现，但是由于太容易实现，依然需要控制。换言之，尽管是要压榨底层系统的性能，但还是需要给予一定的过载保护，以防止过犹不及。

### 4.4.1 bagpipe 的解决方案

如何对既有的异步 API 添加过载保护，我们期望的当然不是去改动 API。那么如何实现呢？我写的 bagpipe 模块的解决思路是这样的。

- 通过一个队列来控制并发量。
- 如果当前活跃（指调用发起但未执行回调）的异步调用量小于限定值，从队列中取出执行。
- 如果活跃调用达到限定值，调用暂时存放在队列中。
- 每个异步调用结束时，从队列中取出新的异步调用执行。

bagpipe 的 API 主要暴露了一个 `push()`方法和 full 事件，示例代码如下：

```js
var Bagpipe = require("bagpipe");
// 设定最大并发数为10
var bagpipe = new Bagpipe(10);
for (var i = 0; i < 100; i++) {
  bagpipe.push(async, function () {
    // 异步回调执行
  });
}
bagpipe.on("full", function (length) {
  console.warn(
    "֫底层系统处理不能及时完成时，队列拥堵，目前队列长度为:" + length
  );
});
```

这里的实现细节类似于前文的 `smooth()`。`push()`方法依然是通过函数变换的方式实现，假设第一个参数是方法，最后一个参数是回调函数，其余为其他参数，其核心实现如下：

```js
/**
 *推入方法，参数。最后一个参数为回调函数
 * @param {Function} method 异步方法
 * @param {Mix} args 参数列表，最后一个参数为回调函数
 */
Bagpipe.prototype.push = function (method) {
  var args = [].slice.call(arguments, 1);
  var callback = args[args.length - 1];
  if (typeof callback !== "function") {
    args.push(function () {});
  }
  if (this.options.disabled || this.limit < 1) {
    method.apply(null, args);
    return this;
  }
  // 队列长度也超过限制值时
  if (this.queue.length < this.queueLength || !this.options.refuse) {
    this.queue.push({
      method: method,
      args: args,
    });
  } else {
    var err = new Error("Too much async call in queue");
    err.name = "TooMuchAsyncCallError";
    callback(err);
  }
  if (this.queue.length > 1) {
    this.emit("full", this.queue.length);
  }
  this.next();
  return this;
};
```

将调用推入队列后，调用一次 `next()`方法尝试触发。`next()`方法的定义如下：

```js
/*!
 * 继续执行队列中的后续动作
 */
Bagpipe.prototype.next = function () {
  var that = this;
  if (that.active < that.limit && that.queue.length) {
    var req = that.queue.shift();
    that.run(req.method, req.args);
  }
};
```

`next()`方法主要判断活跃调用的数量，如果正常，将调用内部方法 `run()`来执行真正的调用。这里为了判断回调函数是否执行，采用了一个注入代码的技巧，具体代码如下：

```js
/*!
 * 执行队列中的方法
 */
Bagpipe.prototype.run = function (method, args) {
  var that = this;
  that.active++;
  var callback = args[args.length - 1];
  var timer = null;
  var called = false;
  // inject logic
  args[args.length - 1] = function (err) {
    // anyway, clear the timer
    if (timer) {
      clearTimeout(timer);
      timer = null;
    }
    // if timeout, don't execute
    if (!called) {
      that._next();
      callback.apply(null, arguments);
    } else {
      // pass the outdated error
      if (err) {
        that.emit("outdated", err);
      }
    }
  };
  var timeout = that.options.timeout;
  if (timeout) {
    timer = setTimeout(function () {
      // set called as true
      called = true;
      that._next();
      // pass the exception
      var err = new Error(timeout + "ms timeout");
      err.name = "BagpipeTimeoutError";
      err.data = {
        name: method.name,
        method: method.toString(),
        args: args.slice(0, -1),
      };
      callback(err);
    }, timeout);
  }
  method.apply(null, args);
};
```

用户传入的回调函数被真正执行前，被封装替换过。这个封装的回调函数内部的逻辑将活跃值的计数器减 1 后，主动调用 `next()`执行后续等待的异步调用。

bagpipe 类似于打开了一道窗口，允许异步调用并行进行，但是严格限定上限。仅仅在调用 `push()`时分开传递，并不对原有 API 有任何侵入。

**拒绝模式**

事实上，bagpipe 还有一些深度的使用方式。对于大量的异步调用，也需要分场景进行区分，因为涉及并发控制，必然会造成部分调用需要进行等待。如果调用有实时方面的需求，那么需要快速返回，因为等到方法被真正执行时，可能已经超过了等待时间，即使返回了数据，也没有意义了。这种场景下需要快速失败，让调用方尽早返回，而不用浪费不必要的等待时间。bagpipe 为此支持了拒绝模式。

拒绝模式的使用只要设置下参数即可，相关代码如下：

```js
// 设定最大并发数为10
var bagpipe = new Bagpipe(10, {
  refuse: true,
});
```

在拒绝模式下，如果等待的调用队列也满了之后，新来的调用就直接返给它一个队列太忙的拒绝异常。

**超时控制**

造成队列拥塞的主要原因是异步调用耗时太久，调用产生的速度远远高于执行的速度。为了防止某些异步调用使用了太多的时间，我们需要设置一个时间基线，将那些执行时间太久的异步调用清理出活跃队列，让排队中的异步调用尽快执行。否则在拒绝模式下，会有太多的调用因为某个执行得慢，导致得到拒绝异常。相对而言，这种场景下得到拒绝异常显得比较无辜。为了公平地对待在实时需求场景下的每个调用，必须要控制每个调用的执行时间，将那些害群之马踢出队伍。

为此，bagpipe 也提供了超时控制。超时控制是为异步调用设置一个时间阈值，如果异步调用没有在规定时间内完成，我们先执行用户传入的回调函数，让用户得到一个超时异常，以尽早返回。然后让下一个等待队列中的调用执行。

超时的设置如下：

```js
// 设定最大并发数为10
var bagpipe = new Bagpipe(10, {
  timeout: 3000,
});
```

**小结**

异步调用的并发限制在不同场景下的需求不同：非实时场景下，让超出限制的并发暂时等待执行已经可以满足需求；但在实时场景下，需要更细粒度、更合理的控制。

### 4.4.2 async 的解决方案

无独有偶，async 也提供了一个方法用于处理异步调用的限制：`parallelLimit()`。如下是 async 的示例代码：

```js
async.parallelLimit(
  [
    function (callback) {
      fs.readFile("file1.txt", "utf-8", callback);
    },
    function (callback) {
      fs.readFile("file2.txt", "utf-8", callback);
    },
  ],
  1,
  function (err, results) {
    // TODO
  }
);
```

`parallelLimit()`与 `parallel()`类似，但多了一个用于限制并发数量的参数，使得任务只能同时并发一定数量，而不是无限制并发。

`parallelLimit()`方法的缺陷在于无法动态地增加并行任务。为此，async 提供了 `queue()`方法来满足该需求，这对于遍历文件目录等操作十分有效。以下是 `queue()`的示例代码：

```js
var q = async.queue(function (file, callback) {
  fs.readFile(file, "utf-8", callback);
}, 2);
q.drain = function () {
  // 完成了队列中的所有任务
};
fs.readdirSync(".").forEach(function (file) {
  q.push(file, function (err, data) {
    // TODO
  });
});
```

尽管 `queue()`实现了动态添加并行任务，但是相比 `parallelLimit()`，由于 `queue()`接收的参数是固定的，它丢失了 `parallelLimit()`的多样性，我私心地认为 bagpipe 更灵活，可以添加任意类型的异步任务，也可以动态添加异步任务，同时还能够在实时处理场景中加入拒绝模式和超时控制。在实际应用中，开发者可以根据场景进行取舍。

## 4.5 总结

在接触 Node 的过程中，很多人粗略地接触了几个回调函数之后就放弃了。尽管异步编程略微艰难，但是并非一无是处，一旦习惯，就显得自然。从社区和过往的经验而言，JavaScript 异步编程的难题已经基本解决，无论是通过事件，还是通过 Promise/Deferred 模式，或者流程控制库。相信在掌握以上技巧之后，异步编程不是难事，习惯异步编程之后，将会收获许多值得享受的编程体验。

本章主要介绍了主流的几种异步编程解决方案，这是目前 JavaScript 中主要使用的方案。但对于其他语言而言，还有协程（coroutine）等方式。但是由于 Node 基于 V8 的原因，在目前 EMCAScript5 的实现下还不支持协程。这些标准和规范还在制定中，所以暂时不作介绍。未来的 V8 如果支持 Generator，也将在 Node 中能直接使用。

最后，因为人们总是习惯性地以线性的方式进行思考，以致异步编程相对较为难以掌握。这个世界以异步运行的本质是不会因为大家线性思维的惯性而改变。就像日出月落不会因为你的心情而改变其自有的运行轨迹。

## 4.6 参考资源

本章参考的资源如下：

- http://nodejs.org/docs/latest/api/events.html
- https://github.com/JacksonTian/eventproxy/blob/master/README.md
- https://github.com/JeffreyZhao/jscex/blob/master/README-cn.md
- http://documentup.com/kriskowal/q/
- http://gearman.org/
- https://github.com/JacksonTian/bagpipe
- http://www.jslint.com/lint.html
- https://github.com/JeffreyZhao/wind
- http://wiki.commonjs.org/wiki/Promises

# 第 5 章 内存控制

也许读者会好奇为何会有这样一章存在于本书中，因为在过去很长一段时间内，JavaScript开发者很少在开发过程中遇到需要对内存精确控制的场景，也缺乏控制的手段。说到内存泄漏，大家首先想起的也只是早期版本的IE中JavaScript与DOM交互时发生的问题。如果页面里的内存占用过多，基本等不到进行代码回收，用户已经不耐烦地刷新了当前页面。

随着Node的发展，JavaScript已经实现了CommonJS的生态圈大一统的梦想，JavaScript的应用场景早已不再局限在浏览器中。本章将暂时抛开那些短时间执行的场景，比如网页应用、命令行工具等，这类场景由于运行时间短，且运行在用户的机器上，即使内存使用过多或内存泄漏，也只会影响到终端用户。由于运行时间短，随着进程的退出，内存会释放，几乎没有内存管理的必要。但随着Node在服务器端的广泛应用，其他语言里存在着的问题在JavaScript中也暴露出来了。

基于无阻塞、事件驱动建立的Node服务，具有内存消耗低的优点，非常适合处理海量的网络请求。在海量请求的前提下，开发者就需要考虑一些平常不会形成影响的问题。本书写到这里算是正式迈进服务器端编程的领域了，内存控制正是在海量请求和长时间运行的前提下进行探讨的。在服务器端，资源向来就寸土寸金，要为海量用户服务，就得使一切资源都要高效循环利用。在第3章中，差不多已介绍完Node是如何利用CPU和I/O这两个服务器资源，而本章将介绍在Node中如何合理高效地使用内存。

## 5.1 V8 的垃圾回收机制与内存限制

我们在学习JavaScript编程时听说过，它与Java一样，由垃圾回收机制来进行自动内存管理，这使得开发者不需要像C/C++程序员那样在编写代码的过程中时刻关注内存的分配和释放问题。但在浏览器中进行开发时，几乎很少有人能遇到垃圾回收对应用程序构成性能影响的情况。Node极大地拓宽了JavaScript的应用场景，当主流应用场景从客户端延伸到服务器端之后，我们就能发现，对于性能敏感的服务器端程序，内存管理的好坏、垃圾回收状况是否优良，都会对服务构成影响。而在Node中，这一切都与Node的JavaScript执行引擎V8息息相关。

### 5.1.1 Node与V8

回溯历史可以发现，Node在发展历程中离不开V8，所以在官方的主页介绍中就提到Node是一个构建在Chrome的JavaScript运行时上的平台。2009年，Node的创始人Ryan Dahl选择了V8来作为Node的JavaScript脚本引擎，这离不开当时硝烟四起的第三次浏览器大战。那次大战中，来自Google的Chrome浏览器以其优异的性能成为焦点。Chrome成功的背后离不开JavaScript引擎V8。V8出现后，JavaScript一改它作为脚本语言性能低下的形象。在接下来的性能跑分中，V8持续领跑至今。V8的性能优势使得用JavaScript写高性能后台服务程序成为可能。在这样的契机下，Ryan Dahl选择了JavaScript，选择了V8，在事件驱动、非阻塞I/O模型的设计下实现了Node。

关于V8，它的来历与背景亦是大有来头。作为虚拟机，V8的性能表现优异，这与它的领导者有莫大的渊源，Chrome的成功也离不开它背后的天才——Lars Bak。在Lars的工作履历里，绝大部分都是与虚拟机相关的工作。在开发V8之前，他曾经在Sun公司工作，担任HotSpot团队的技术领导，主要致力于开发高性能的Java虚拟机。在这之前，他也曾为Self、Smalltalk语言开发过高性能虚拟机。这些无与伦比的经历让V8一出世就超越了当时所有的JavaScript虚拟机。

Node在JavaScript的执行上直接受益于V8，可以随着V8的升级就能享受到更好的性能或新的语言特性（如ES5和ES6）等，同时也受到V8的一些限制，尤其是本章要重点讨论的内存限制。

### 5.1.2 V8的内存限制

在一般的后端开发语言中，在基本的内存使用上没有什么限制，然而在Node中通过JavaScript使用内存时就会发现只能使用部分内存（64位系统下约为1.4 GB,32位系统下约为0.7 GB）。在这样的限制下，将会导致Node无法直接操作大内存对象，比如无法将一个2 GB的文件读入内存中进行字符串分析处理，即使物理内存有32 GB。这样在单个Node进程的情况下，计算机的内存资源无法得到充足的使用。

造成这个问题的主要原因在于Node基于V8构建，所以在Node中使用的JavaScript对象基本上都是通过V8自己的方式来进行分配和管理的。V8的这套内存管理机制在浏览器的应用场景下使用起来绰绰有余，足以胜任前端页面中的所有需求。但在Node中，这却限制了开发者随心所欲使用大内存的想法。

尽管在服务器端操作大内存也不是常见的需求场景，但有了限制之后，我们的行为就如同带着镣铐跳舞，如果在实际的应用中不小心触碰到这个界限，会造成进程退出。要知晓V8为何限制了内存的用量，则需要回归到V8在内存使用上的策略。知晓其原理后，才能避免问题并更好地进行内存管理。

### 5.1.3 V8的对象分配

在V8中，所有的JavaScript对象都是通过堆来进行分配的。Node提供了V8中内存使用量的查看方式，执行下面的代码，将得到输出的内存信息：

```
$ node
> process.memoryUsage();
{ rss: 14958592,
heapTotal: 7195904,
heapUsed: 2821496 }
```

在上述代码中，在`memoryUsage()`方法返回的3个属性中，heapTotal和heapUsed是V8的堆内存使用情况，前者是已申请到的堆内存，后者是当前使用的量。至于rss为何，我们在后续的内容中会介绍到。图5-1为V8的堆示意图：

图5-1 V8的堆示意图

当我们在代码中声明变量并赋值时，所使用对象的内存就分配在堆中。如果已申请的堆空闲内存不够分配新的对象，将继续申请堆内存，直到堆的大小超过V8的限制为止。

至于V8为何要限制堆的大小，表层原因为V8最初为浏览器而设计，不太可能遇到用大量内存的场景。对于网页来说，V8的限制值已经绰绰有余。深层原因是V8的垃圾回收机制的限制。按官方的说法，以1.5 GB的垃圾回收堆内存为例，V8做一次小的垃圾回收需要50毫秒以上，做一次非增量式的垃圾回收甚至要1秒以上。这是垃圾回收中引起JavaScript线程暂停执行的时间，在这样的时间花销下，应用的性能和响应能力都会直线下降。这样的情况不仅仅后端服务无法接受，前端浏览器也无法接受。因此，在当时的考虑下直接限制堆内存是一个好的选择。

当然，这个限制也不是不能打开，V8依然提供了选项让我们使用更多的内存。Node在启动时可以传递`--max-old-space-size`或`--max-new-space-size`来调整内存限制的大小，示例如下：

上述参数在V8初始化时生效，一旦生效就不能再动态改变。如果遇到Node无法分配足够内存给JavaScript对象的情况，可以用这个办法来放宽V8默认的内存限制，避免在执行过程中稍微多用了一些内存就轻易崩溃。

接下来，让我们更深入地了解V8在垃圾回收方面的策略。在限制的前提下，带着镣铐跳出的舞蹈并不一定就难看。

### 5.1.4 V8的垃圾回收机制

在展开介绍V8的垃圾回收机制前，有必要简略介绍下V8用到的各种垃圾回收算法。

1. V8主要的垃圾回收算法

V8的垃圾回收策略主要基于分代式垃圾回收机制。在自动垃圾回收的演变过程中，人们发现没有一种垃圾回收算法能够胜任所有的场景。因为在实际的应用中，对象的生存周期长短不一，不同的算法只能针对特定情况具有最好的效果。为此，统计学在垃圾回收算法的发展中产生了较大的作用，现代的垃圾回收算法中按对象的存活时间将内存的垃圾回收进行不同的分代，然后分别对不同分代的内存施以更高效的算法。

**V8的内存分代**

在V8中，主要将内存分为新生代和老生代两代。新生代中的对象为存活时间较短的对象，老生代中的对象为存活时间较长或常驻内存的对象。图5-2为V8的分代示意图。



图5-2 V8的分代示意图V8堆的整体大小就是新生代所用内存空间加上老生代的内存空间。前面我们提及的`--max-old-space-size`命令行参数可以用于设置老生代内存空间的最大值，`--max-new-space-size`命令行参数则用于设置新生代内存空间的大小的。比较遗憾的是，这两个最大值需要在启动时就指定。这意味着V8使用的内存没有办法根据使用情况自动扩充，当内存分配过程中超过极限值时，就会引起进程出错。

前面提到过，在默认设置下，如果一直分配内存，在64位系统和32位系统下会分别只能使用约1.4GB和约0.7 GB的大小。这个限制可以从V8的源码中找到。在下面的代码中，`Page::kPageSize`的值为1MB。可以看到，老生代的设置在64位系统下为1400 MB，在32位系统下为700 MB：

对于新生代内存，它由两个`reserved_semispace_size_`所构成，后面将描述其原因。按机器位数不同，`reserved_semispace_size_`在64位系统和32位系统上分别为16 MB和8 MB。所以新生代内存的最大值在64位系统和32位系统上分别为32 MB和16MB。V8堆内存的最大保留空间可以从下面的代码中看出来，其公式为`4 * reserved_semispace_size_ +max_old_generation_size_：`



因此，默认情况下，V8堆内存的最大值在64位系统上为1464 MB,32位系统上则为732 MB。这个数值可以解释为何在64位系统下只能使用约1.4GB内存和在32位系统下只能使用约0.7 GB内存。

**Scavenge算法**

在分代的基础上，新生代中的对象主要通过Scavenge算法进行垃圾回收。在Scavenge的具体实现中，主要采用了Cheney算法，该算法由C. J.Cheney于1970年首次发表在ACM论文上。

Cheney算法是一种采用复制的方式实现的垃圾回收算法。它将堆内存一分为二，每一部分空间称为semispace。在这两个semispace空间中，只有一个处于使用中，另一个处于闲置状态。处于使用状态的semispace空间称为From空间，处于闲置状态的空间称为To空间。当我们分配对象时，先是在From空间中进行分配。当开始进行垃圾回收时，会检查From空间中的存活对象，这些存活对象将被复制到To空间中，而非存活对象占用的空间将会被释放。完成复制后，From空间和To空间的角色发生对换。简而言之，在垃圾回收的过程中，就是通过将存活对象在两个semispace空间之间进行复制。

Scavenge的缺点是只能使用堆内存中的一半，这是由划分空间和复制机制所决定的。但Scavenge由于只复制存活的对象，并且对于生命周期短的场景存活对象只占少部分，所以它在时间效率上有优异的表现。

由于Scavenge是典型的牺牲空间换取时间的算法，所以无法大规模地应用到所有的垃圾回收中。但可以发现，Scavenge非常适合应用在新生代中，因为新生代中对象的生命周期较短，恰恰适合这个算法。

是故，V8的堆内存示意图应当如图5-3所示。

图5-3 V8的堆内存示意图

实际使用的堆内存是新生代中的两个semispace空间大小和老生代所用内存大小之和。

当一个对象经过多次复制依然存活时，它将会被认为是生命周期较长的对象。这种较长生命周期的对象随后会被移动到老生代中，采用新的算法进行管理。对象从新生代中移动到老生代中的过程称为晋升。

在单纯的Scavenge过程中，From空间中的存活对象会被复制到To空间中去，然后对From空间和To空间进行角色对换（又称翻转）。但在分代式垃圾回收的前提下，From空间中的存活对象在复制到To空间之前需要进行检查。在一定条件下，需要将存活周期长的对象移动到老生代中，也就是完成对象晋升。

对象晋升的条件主要有两个，一个是对象是否经历过Scavenge回收，一个是To空间的内存占用比超过限制。

在默认情况下，V8的对象分配主要集中在From空间中。对象从From空间中复制到To空间时，会检查它的内存地址来判断这个对象是否已经经历过一次Scavenge回收。如果已经经历过了，会将该对象从From空间复制到老生代空间中，如果没有，则复制到To空间中。这个晋升流程如图5-4所示。

图5-4 晋升流程

另一个判断条件是To空间的内存占用比。当要从From空间复制一个对象到To空间时，如果To空间已经使用了超过25%，则这个对象直接晋升到老生代空间中，这个晋升的判断示意图如图5-5所示。

图5-5 晋升的判断示意图

设置25%这个限制值的原因是当这次Scavenge回收完成后，这个To空间将变成From空间，接下来的内存分配将在这个空间中进行。如果占比过高，会影响后续的内存分配。

对象晋升后，将会在老生代空间中作为存活周期较长的对象来对待，接受新的回收算法处理。

**Mark-Sweep & Mark-Compact**

对于老生代中的对象，由于存活对象占较大比重，再采用Scavenge的方式会有两个问题：一个是存活对象较多，复制存活对象的效率将会很低；另一个问题依然是浪费一半空间的问题。这两个问题导致应对生命周期较长的对象时Scavenge会显得捉襟见肘。为此，V8在老生代中主要采用了Mark-Sweep和Mark-Compact相结合的方式进行垃圾回收。

Mark-Sweep是标记清除的意思，它分为标记和清除两个阶段。与Scavenge相比，Mark-Sweep并不将内存空间划分为两半，所以不存在浪费一半空间的行为。与Scavenge复制活着的对象不同，Mark-Sweep在标记阶段遍历堆中的所有对象，并标记活着的对象，在随后的清除阶段中，只清除没有被标记的对象。可以看出，Scavenge中只复制活着的对象，而Mark-Sweep只清理死亡对象。活对象在新生代中只占较小部分，死对象在老生代中只占较小部分，这是两种回收方式能高效处理的原因。图5-6为Mark-Sweep在老生代空间中标记后的示意图，黑色部分标记为死亡的对象。



图5-6 Mark-Sweep在老生代空间中标记后的示意图

Mark-Sweep最大的问题是在进行一次标记清除回收后，内存空间会出现不连续的状态。这种内存碎片会对后续的内存分配造成问题，因为很可能出现需要分配一个大对象的情况，这时所有的碎片空间都无法完成此次分配，就会提前触发垃圾回收，而这次回收是不必要的。

为了解决Mark-Sweep的内存碎片问题，Mark-Compact被提出来。Mark-Compact是标记整理的意思，是在Mark-Sweep的基础上演变而来的。它们的差别在于对象在标记为死亡后，在整理的过程中，将活着的对象往一端移动，移动完成后，直接清理掉边界外的内存。图5-7为Mark-Compact完成标记并移动存活对象后的示意图，白色格子为存活对象，深色格子为死亡对象，浅色格子为存活对象移动后留下的空洞。

图5-7 Mark-Compact完成标记并移动存活对象后的示意图

完成移动后，就可以直接清除最右边的存活对象后面的内存区域完成回收。

这里将Mark-Sweep和Mark-Compact结合着介绍不仅仅是因为两种策略是递进关系，在V8的回收策略中两者是结合使用的。表5-1是目前介绍到的3种主要垃圾回收算法的简单对比。

表5-1 3种垃圾回收算法的简单对比

从表5-1中可以看到，在Mark-Sweep和Mark-Compact之间，由于Mark-Compact需要移动对象，所以它的执行速度不可能很快，所以在取舍上，V8主要使用Mark-Sweep，在空间不足以对从新生代中晋升过来的对象进行分配时才使用Mark-Compact。

**Incremental Marking**

为了避免出现JavaScript应用逻辑与垃圾回收器看到的不一致的情况，垃圾回收的3种基本算法都需要将应用逻辑暂停下来，待执行完垃圾回收后再恢复执行应用逻辑，这种行为被称为“全停顿”（stop-the-world）。在V8的分代式垃圾回收中，一次小垃圾回收只收集新生代，由于新生代默认配置得较小，且其中存活对象通常较少，所以即便它是全停顿的影响也不大。但V8的老生代通常配置得较大，且存活对象较多，全堆垃圾回收（full垃圾回收）的标记、清理、整理等动作造成的停顿就会比较可怕，需要设法改善。

为了降低全堆垃圾回收带来的停顿时间，V8先从标记阶段入手，将原本要一口气停顿完成的动作改为增量标记（incremental marking），也就是拆分为许多小“步进”，每做完一“步进”就让JavaScript应用逻辑执行一小会儿，垃圾回收与应用逻辑交替执行直到标记阶段完成。图5-8为增量标记示意图。

图5-8 增量标记示意图

V8在经过增量标记的改进后，垃圾回收的最大停顿时间可以减少到原本的1/6左右。

V8后续还引入了延迟清理（lazy sweeping）与增量式整理（incremental compaction），让清理与整理动作也变成增量式的。同时还计划引入并行标记与并行清理，进一步利用多核性能降低每次停顿的时间。鉴于篇幅有限，此处不再深入讲解了。

2. 小结

从V8的自动垃圾回收机制的设计角度可以看到，V8对内存使用进行限制的缘由。新生代设计为一个较小的内存空间是合理的，而老生代空间过大对于垃圾回收并无特别意义。V8对内存限制的设置对于Chrome浏览器这种每个选项卡页面使用一个V8实例而言，内存的使用是绰绰有余了。对于Node编写的服务器端来说，内存限制也并不影响正常场景下的使用。但是对于V8的垃圾回收特点和JavaScript在单线程上的执行情况，垃圾回收是影响性能的因素之一。想要高性能的执行效率，需要注意让垃圾回收尽量少地进行，尤其是全堆垃圾回收。

以Web服务器中的会话实现为例，一般通过内存来存储，但在访问量大的时候会导致老生代中的存活对象骤增，不仅造成清理/整理过程费时，还会造成内存紧张，甚至溢出（详情可参见第8章）。

### 5.1.5 查看垃圾回收日志

查看垃圾回收日志的方式主要是在启动时添加`--trace_gc`参数。在进行垃圾回收时，将会从标准输出中打印垃圾回收的日志信息。下面是一段示例，执行结束后，将会在gc.log文件中得到所有垃圾回收信息：

下面是我截取的垃圾回收日志中的部分重要内容：

通过分析垃圾回收日志，可以了解垃圾回收的运行状况，找出垃圾回收的哪些阶段比较耗时，触发的原因是什么。

通过在Node启动时使用`--prof`参数，可以得到V8执行时的性能分析数据，其中包含了垃圾回收执行时占用的时间。下面的代码不断创建对象并将其分配给局部变量a，这里将以下代码存为test01.js文件：

然后执行以下命令：



这将会在目录下得到一个v8.log日志文件。该日志文件基本不具备可读性，内容大致如下：

所幸，V8提供了linux-tick-processor工具用于统计日志信息。该工具可以从Node源码的deps/v8/tools目录下找到，Windows下的对应命令文件为windows-tick-processor.bat。将该目录添加到环境变量PATH中，即可直接调用：

下面为我某次运行日志的统计结果：

统计内容较多，其中垃圾回收部分如下：



由于不断分配对象，垃圾回收所占的时间为5.4%。按此比例，这意味着事件循环执行1000毫秒的过程中要给出54毫秒的时间用于垃圾回收。

## 5.2 高效使用内存

在V8面前，开发者所要具备的责任是如何让垃圾回收机制更高效地工作。

### 5.2.1 作用域

提到如何触发垃圾回收，第一个要介绍的是作用域（scope）。在JavaScript中能形成作用域的有函数调用、with以及全局作用域。以如下代码为例：

`foo()`函数在每次被调用时会创建对应的作用域，函数执行结束后，该作用域将会销毁。同时作用域中声明的局部变量分配在该作用域上，随作用域的销毁而销毁。只被局部变量引用的对象存活周期较短。在这个示例中，由于对象非常小，将会分配在新生代中的From空间中。在作用域释放后，局部变量local失效，其引用的对象将会在下次垃圾回收时被释放。

以上就是最基本的内存回收过程。

1. 标识符查找

与作用域相关的即是标识符查找。所谓标识符，可以理解为变量名。在下面的代码中，执行`bar()`函数时，将会遇到local变量：

JavaScript在执行时会去查找该变量定义在哪里。它最先查找的是当前作用域，如果在当前作用域中无法找到该变量的声明，将会向上级的作用域里查找，直到查到为止。

2. 作用域链

在下面的代码中：

local变量在`baz()`函数形成的作用域里查找不到，继而将在`bar()`的作用域里寻找。如果去掉上述代码`bar()`中的local声明，将会继续向上查找，一直到全局作用域。这样的查找方式使得作用域像一个链条。由于标识符的查找方向是向上的，所以变量只能向外访问，而不能向内访问。图5-9为变量在作用域中的查找示意图。

图5-9 变量在作用域中的查找示意图

当我们在`baz()`函数中访问local变量时，由于作用域中的变量列表中没有local，所以会向上一个作用域中查找，接着会在`bar()`函数执行得到的变量列表中找到了一个local变量的定义，于是使用它。尽管在再上一层的作用域中也存在local的定义，但是不会继续查找了。如果查找一个不存在的变量，将会一直沿着作用域链查找到全局作用域，最后抛出未定义错误。

了解了作用域，有助于我们了解变量的分配和释放。

3. 变量的主动释放

如果变量是全局变量（不通过var声明或定义在global变量上），由于全局作用域需要直到进程退出才能释放，此时将导致引用的对象常驻内存（常驻在老生代中）。如果需要释放常驻内存的对象，可以通过delete操作来删除引用关系。或者将变量重新赋值，让旧的对象脱离引用关系。在接下来的老生代内存清除和整理的过程中，会被回收释放。下面为示例代码：

同样，如果在非全局作用域中，想主动释放变量引用的对象，也可以通过这样的方式。虽然delete操作和重新赋值具有相同的效果，但是在V8中通过delete删除对象的属性有可能干扰V8的优化，所以通过赋值方式解除引用更好。

### 5.2.2 闭包

我们知道作用域链上的对象访问只能向上，这样外部无法向内部访问。如下代码可以正常打印：

但在下面的代码中，却会得到local未定义的异常：



在JavaScript中，实现外部作用域访问内部作用域中变量的方法叫做闭包（closure）。这得益于高阶函数的特性：函数可以作为参数或者返回值。示例代码的如下：

一般而言，在`bar()`函数执行完成后，局部变量local将会随着作用域的销毁而被回收。但是注意这里的特点在于返回值是一个匿名函数，且这个函数中具备了访问local的条件。虽然在后续的执行中，在外部作用域中还是无法直接访问local，但是若要访问它，只要通过这个中间函数稍作周转即可。

闭包是JavaScript的高级特性，利用它可以产生很多巧妙的效果。它的问题在于，一旦有变量引用这个中间函数，这个中间函数将不会释放，同时也会使原始的作用域不会得到释放，作用域中产生的内存占用也不会得到释放。除非不再有引用，才会逐步释放。

### 5.2.3 小结

在正常的JavaScript执行中，无法立即回收的内存有闭包和全局变量引用这两种情况。由于V8的内存限制，要十分小心此类变量是否无限制地增加，因为它会导致老生代中的对象增多。

## 5.3 内存指标

一般而言，应用中存在一些全局性的对象是正常的，而且在正常的使用中，变量都会自动释放回收。但是也会存在一些我们认为会回收但是却没有被回收的对象，这会导致内存占用无限增长。一旦增长达到V8的内存限制，将会得到内存溢出错误，进而导致进程退出。

### 5.3.1 查看内存使用情况

前面我们提到了`process.memoryUsage()`可以查看内存使用情况。除此之外，os模块中的`totalmem()`和`freemem()`方法也可以查看内存使用情况。

1. 查看进程的内存占用

调用`process.memoryUsage()`可以看到Node进程的内存占用情况，示例代码如下：

rss是resident set size的缩写，即进程的常驻内存部分。进程的内存总共有几部分，一部分是rss，其余部分在交换区（swap）或者文件系统（filesystem）中。

除了rss外，heapTotal和heapUsed对应的是V8的堆内存信息。heapTotal是堆中总共申请的内存量，heapUsed表示目前堆中使用中的内存量。这3个值的单位都是字节。

为了更好地查看效果，我们格式化一下输出结果：

同时，写一个方法用于不停地分配内存但不释放内存，相关代码如下：



将以上代码存为outofmemory.js并执行它，得到的输出结果如下：

可以看到，每次调用useMem都导致了3个值的增长。在接近1500 MB的时候，无法继续分配内存，然后进程内存溢出了，连循环体都无法执行完成，仅执行了7次。

2. 查看系统的内存占用

与`process.memoryUsage()`不同的是，os模块中的`totalmem()`和`freemem()`这两个方法用于查看操作系统的内存使用情况，它们分别返回系统的总内存和闲置内存，以字节为单位。示例代码如下：

从输出信息可以看到我的电脑的总内存为8 GB，当前闲置内存大致为4.2 GB。



### 5.3.2 堆外内存

通过`process.memoryUsage()`的结果可以看到，堆中的内存用量总是小于进程的常驻内存用量，这意味着Node中的内存使用并非都是通过V8进行分配的。我们将那些不是通过V8分配的内存称为堆外内存。

这里我们将前面的`useMem()`方法稍微改造一下，将Array变为Buffer，将size变大，每一次构造200MB的对象，相关代码如下：

重新执行该代码，得到的输出结果如下所示：

我们看到15次循环都完整执行，并且三个内存占用值与前一个示例完全不同。在改造后的输出结果中，heapTotal与heapUsed的变化极小，唯一变化的是rss的值，并且该值已经远远超过V8的限制值。这其中的原因是Buffer对象不同于其他对象，它不经过V8的内存分配机制，所以也不会有堆内存的大小限制。

这意味着利用堆外内存可以突破内存限制的问题。

为何Buffer对象并非通过V8分配？这在于Node并不同于浏览器的应用场景。在浏览器中，JavaScript直接处理字符串即可满足绝大多数的业务需求，而Node则需要处理网络流和文件I/O流，操作字符串远远不能满足传输的性能需求。

关于Buffer的细节可参见第6章。

### 5.3.3 小结

从上面的介绍可以得知，Node的内存构成主要由通过V8进行分配的部分和Node自行分配的部分。受V8的垃圾回收限制的主要是V8的堆内存。

## 5.4 内存泄漏

Node对内存泄漏十分敏感，一旦线上应用有成千上万的流量，那怕是一个字节的内存泄漏也会造成堆积，垃圾回收过程中将会耗费更多时间进行对象扫描，应用响应缓慢，直到进程内存溢出，应用崩溃。

在V8的垃圾回收机制下，在通常的代码编写中，很少会出现内存泄漏的情况。但是内存泄漏通常产生于无意间，较难排查。尽管内存泄漏的情况不尽相同，但其实质只有一个，那就是应当回收的对象出现意外而没有被回收，变成了常驻在老生代中的对象。

通常，造成内存泄漏的原因有如下几个。
- 缓存。
- 队列消费不及时。
- 作用域未释放。

### 5.4.1 慎将内存当做缓存

缓存在应用中的作用举足轻重，可以十分有效地节省资源。因为它的访问效率要比I/O的效率高，一旦命中缓存，就可以节省一次I/O的时间。

但是在Node中，缓存并非物美价廉。一旦一个对象被当做缓存来使用，那就意味着它将会常驻在老生代中。缓存中存储的键越多，长期存活的对象也就越多，这将导致垃圾回收在进行扫描和整理时，对这些对象做无用功。

另一个问题在于，JavaScript开发者通常喜欢用对象的键值对来缓存东西，但这与严格意义上的缓存又有着区别，严格意义的缓存有着完善的过期策略，而普通对象的键值对并没有。

如下代码虽然利用JavaScript对象十分容易创建一个缓存对象，但是受垃圾回收机制的影响，只能小量使用：

上述示例在解释原理后，十分容易理解，如果需要，只要限定缓存对象的大小，加上完善的过期策略以防止内存无限制增长，还是可以一用的。

这里给出一个可能无意识造成内存泄漏的场景：memoize。下面是著名类库underscore对memoize的实现：

它的原理是以参数作为键进行缓存，以内存空间换CPU执行时间。这里潜藏的陷阱即是每个被执行的结果都会按参数缓存在memo对象上，不会被清除。这在前端网页这种短时应用场景中不存在大问题，但是执行量大和参数多样性的情况下，会造成内存占用不释放。

所以在Node中，任何试图拿内存当缓存的行为都应当被限制。当然，这种限制并不是不允许使用的意思，而是要小心为之。

1. 缓存限制策略

为了解决缓存中的对象永远无法释放的问题，需要加入一种策略来限制缓存的无限增长。为此我曾写过一个模块limitablemap，它可以实现对键值数量的限制。下面是其实现：

可以看到，实现过程还是非常简单的。记录键在数组中，一旦超过数量，就以先进先出的方式进行淘汰。

当然，这种淘汰策略并不是十分高效，只能应付小型应用场景。如果需要更高效的缓存，可以参见Isaac Z. Schlueter采用LRU算法的缓存，地址为 https://github.com/isaacs/node-lru-cache 。结合有限制的缓存，memoize还是可用的。

另一个案例在于模块机制。在第2章的模块介绍中，为了加速模块的引入，所有模块都会通过编译执行，然后被缓存起来。由于通过exports导出的函数，可以访问文件模块中的私有变量，这样每个文件模块在编译执行后形成的作用域因为模块缓存的原因，不会被释放。示例代码如下所示：

由于模块的缓存机制，模块是常驻老生代的。在设计模块时，要十分小心内存泄漏的出现。在下面的代码，每次调用`leak()`方法时，都导致局部变量leakArray不停增加内存的占用，且不被释放：

如果模块不可避免地需要这么设计，那么请添加清空队列的相应接口，以供调用者释放内存。

2. 缓存的解决方案

直接将内存作为缓存的方案要十分慎重。除了限制缓存的大小外，另外要考虑的事情是，进程之间无法共享内存。如果在进程内使用缓存，这些缓存不可避免地有重复，对物理内存的使用是一种浪费。如何使用大量缓存，目前比较好的解决方案是采用进程外的缓存，进程自身不存储状态。外部的缓存软件有着良好的缓存过期淘汰策略以及自有的内存管理，不影响Node进程的性能。它的好处多多，在Node中主要可以解决以下两个问题。

- 将缓存转移到外部，减少常驻内存的对象的数量，让垃圾回收更高效。
- 进程之间可以共享缓存。目前，市面上较好的缓存有Redis和Memcached。Node模块的生态系统十分完善，这两个产品的客户端都有，通过以下地址可以查看具体使用详情。
  - Redis:https://github.com/mranney/node_redis。
  - Memcached:https://github.com/3rd-Eden/node-memcached。

### 5.4.2 关注队列状态

在解决了缓存带来的内存泄漏问题后，另一个不经意产生的内存泄漏则是队列。在第4章中可以看到，在JavaScript中可以通过队列（数组对象）来完成许多特殊的需求，比如Bagpipe。队列在消费者-生产者模型中经常充当中间产物。这是一个容易忽略的情况，因为在大多数应用场景下，消费的速度远远大于生产的速度，内存泄漏不易产生。但是一旦消费速度低于生产速度，将会形成堆积。

举个实际的例子，有的应用会收集日志。如果欠缺考虑，也许会采用数据库来记录日志。日志通常会是海量的，数据库构建在文件系统之上，写入效率远远低于文件直接写入，于是会形成数据库写入操作的堆积，而JavaScript中相关的作用域也不会得到释放，内存占用不会回落，从而出现内存泄漏。

遇到这种场景，表层的解决方案是换用消费速度更高的技术。在日志收集的案例中，换用文件写入日志的方式会更高效。需要注意的是，如果生产速度因为某些原因突然激增，或者消费速度因为突然的系统故障降低，内存泄漏还是可能出现的。

深度的解决方案应该是监控队列的长度，一旦堆积，应当通过监控系统产生报警并通知相关人员。另一个解决方案是任意异步调用都应该包含超时机制，一旦在限定的时间内未完成响应，通过回调函数传递超时异常，使得任意异步调用的回调都具备可控的响应时间，给消费速度一个下限值。

对于Bagpipe而言，它提供了超时模式和拒绝模式。启用超时模式时，调用加入到队列中就开始计时，超时就直接响应一个超时错误。启用拒绝模式时，当队列拥塞时，新到来的调用会直接响应拥塞错误。这两种模式都能够有效地防止队列拥塞导致的内存泄漏问题。

## 5.5 内存泄漏排查

前面提及了几种导致内存泄漏的常见类型。在Node中，由于V8的堆内存大小的限制，它对内存泄漏非常敏感。当在线服务的请求量变大时，哪怕是一个字节的泄漏都会导致内存占用过高。这里介绍一下遇到内存泄漏时的排查方案。

现在已经有许多工具用于定位Node应用的内存泄漏，下面是一些常见的工具。
- v8-profiler。由Danny Coates提供，它可以用于对V8堆内存抓取快照和对CPU进行分析，但该项目已经有3年没有维护了。
- node-heapdump。这是Node核心贡献者之一Ben Noordhuis编写的模块，它允许对V8堆内存抓取快照，用于事后分析。
- node-mtrace。由Jimb Esser提供，它使用了GCC的mtrace工具来分析堆的使用。
- dtrace。在Joyent的SmartOS系统上，有完善的dtrace工具用来分析内存泄漏。
- node-memwatch。来自Mozilla的LloydHilaiel贡献的模块，采用WTFPL许可发布。由于各种条件限制，这里将只着重介绍通过node-heapdump和node-memwatch两种方式进行内存泄漏的排查。

### 5.5.1 node-heapdump

想要了解node-heapdump对内存泄漏进行排查的方式，我们需要先构造如下一份包含内存泄漏的代码示例，并将其存为server.js文件：

在上面这段代码中，每次访问服务进程都将引起leakArray数组中的元素增加，而且得不到回收。我们可以用curl工具输入 http://127.0.0.1:1337/ 命令来模拟用户访问。

**安装node-heapdump**

安装node-heapdump非常简单，执行以下命令即可：

安装node-heapdump后，在代码的第一行添加如下代码将其引入：

引入node-heapdump后，就可以启动服务进程，并接受客户端的请求。访问多次之后，leakArray中就会具备大量的元素。这个时候我们通过向服务进程发送SIGUSR2信号，让node-heapdump抓拍一份堆内存的快照。发送信号的命令如下：

这份抓取的快照将会在文件目录下以`heapdump-<sec>.<usec>.heapsnapshot`的格式存放。这是一份较大的JSON文件，需要通过Chrome的开发者工具打开查看。

在Chrome的开发者工具中选中Profiles面板，右击该文件后，从弹出的快捷菜单中选择Load...选项，打开刚才的快照文件，就可以查看堆内存中的详细信息，如图5-10所示。

图5-10 查看堆内存中的详细信息

在图5-10中可以看到有大量的leak字符串存在，这些字符串就是一直未能得到回收的数据。通过在开发者工具的面板中查看内存分布，我们可以找到泄漏的数据，然后根据这些信息找到造成泄漏的代码。

### 5.5.2 node-memwatch

node-memwatch的用法和node-heapdump一样，我们需要准备一份具有内存泄漏的代码。这里不再赘述node-memwatch的安装过程。整个示例代码如下：

1. stats事件

在进程中使用node-memwatch之后，每次进行全堆垃圾回收时，将会触发一次stats事件，这个事件将会传递内存的统计信息。在对上述代码创建的服务进程进行访问时，某次stats事件打印的数据如下所示，其中每项的意义写在注释中了：

在这些数据中，num_full_gc和num_inc_gc比较直观地反应了垃圾回收的情况。

2. leak事件

如果经过连续5次垃圾回收后，内存仍然没有被释放，这意味着有内存泄漏的产生，node-memwatch会出发一个leak事件。某次leak事件得到的数据如下所示：

这个数据能显示5次垃圾回收的过程中内存增长了多少。

3. 堆内存比较

最终得到的leak事件的信息只能告知我们应用中存在内存泄漏，具体问题产生在何处还需要从V8的堆内存上定位。node-memwatch提供了抓取快照和比较快照的功能，它能够比较堆上对象的名称和分配数量，从而找出导致内存泄漏的元凶。

下面为一段导致内存泄漏的代码，这是通过node-memwatch获取堆内存差异结果的示例：

执行上面这段代码，得到的输出结果如下所示：

在上面的输出结果中，主要关注change节点下的freed_nodes和allocated_nodes，它们记录了释放的节点数量和分配的节点数量。这里由于有内存泄漏，分配的节点数量远远多余释放的节点数量。在details下可以看到具体每种类型的分配和释放数量，主要问题展现在下面这段输出中：

在上述代码中，加号和减号分别表示分配和释放的字符串对象数量。可以通过上面的输出结果猜测到，有大量的字符串没有被回收。

### 5.5.3 小结

从本节的内容我们可以得知，排查内存泄漏的原因主要通过对堆内存进行分析而找到。node-heapdump和node-memwatch各有所长，读者可以结合它们的优势进行内存泄漏排查。

## 5.6 大内存应用

在Node中，不可避免地还是会存在操作大文件的场景。由于Node的内存限制，操作大文件也需要小心，好在Node提供了stream模块用于处理大文件。

stream模块是Node的原生模块，直接引用即可。stream继承自EventEmitter，具备基本的自定义事件功能，同时抽象出标准的事件和方法。它分可读和可写两种。Node中的大多数模块都有stream的应用，比如fs的`createReadStream()`和`createWriteStream()`方法可以分别用于创建文件的可读流和可写流，process模块中的stdin和stdout则分别是可读流和可写流的示例。

由于V8的内存限制，我们无法通过`fs.readFile()`和`fs.writeFile()`直接进行大文件的操作，而改用`fs.createReadStream()`和`fs.createWriteStream()`方法通过流的方式实现对大文件的操作。下面的代码展示了如何读取一个文件，然后将数据写入到另一个文件的过程：

由于读写模型固定，上述方法有更简洁的方式，具体如下所示：

可读流提供了管道方法`pipe()`，封装了data事件和写入操作。通过流的方式，上述代码不会受到V8内存限制的影响，有效地提高了程序的健壮性。

如果不需要进行字符串层面的操作，则不需要借助V8来处理，可以尝试进行纯粹的Buffer操作，这不会受到V8堆内存的限制。但是这种大片使用内存的情况依然要小心，即使V8不限制堆内存的大小，物理内存依然有限制。

## 5.7 总结

Node将JavaScript的主要应用场景扩展到了服务器端，相应要考虑的细节也与浏览器端不同，需要更严谨地为每一份资源作出安排。总的来说，内存在Node中不能随心所欲地使用，但也不是完全不擅长。本章介绍了内存的各种限制，希望读者可以在使用中规避禁忌，与生态系统中的各种软件搭配，发挥Node的长处。

## 5.8 参考资源

在这里，我特别感谢莫枢对本章的指导。本章参考的资源如下所示：

- https://github.com/joyent/node/wiki/FAQ
- http://www.cs.sunysb.edu/~cse304/Fall08/Lectures/mem-handout.pdf
- http://en.wikipedia.org/wiki/Resident_set_size
- https://github.com/isaacs/node-lru-cache
- https://github.com/mranney/node_redis
- https://github.com/3rd-Eden/node-memcached
- http://nodejs.org/docs/latest/api/stream.html
- http://www.showmuch.com/a/20111012/215033.html
- https://github.com/lloyd/node-memwatch
- https://github.com/bnoordhuis/node-heapdump
- http://www.williamlong.info/archives/3042.html
- https://code.google.com/p/v8/issues/detail?id=847
- http://blog.chromium.org/2011/11/game-changer-for-interactive.html

# 第 6 章 理解 Buffer

JavaScript对于字符串（string）的操作十分友好，无论是宽字节字符串还是单字节字符串，都被认为是一个字符串。示例代码如下所示：

对比PHP中的字符串统计，我们需要动用额外的函数来获取字符串的长度。示例代码如下所示：

与第5章介绍的内容一样，本章讲述的也是前端JavaScript开发者不曾涉及的内容。文件和网络I/O对于前端开发者而言都是不曾有的应用场景，因为前端只需做一些简单的字符串操作或DOM操作基本就能满足业务需求，在ECMAScript规范中，也没有对这些方面做任何的定义，只有CommonJS中有部分二进制的定义。由于应用场景不同，在Node中，应用需要处理网络协议、操作数据库、处理图片、接收上传文件等，在网络流和文件的操作中，还要处理大量二进制数据，JavaScript自有的字符串远远不能满足这些需求，于是Buffer对象应运而生。

## 6.1 Buffer 结构

Buffer是一个像Array的对象，但它主要用于操作字节。下面我们从模块结构和对象结构的层面上来认识它。

### 6.1.1 模块结构

Buffer是一个典型的JavaScript与C++结合的模块，它将性能相关部分用C++实现，将非性能相关的部分用JavaScript实现，如图6-1所示。

图6-1 Buffer的分工第5章揭示了Buffer所占用的内存不是通过V8分配的，属于堆外内存。由于V8垃圾回收性能的影响，将常用的操作对象用更高效和专有的内存分配回收策略来管理是个不错的思路。由于Buffer太过常见，Node在进程启动时就已经加载了它，并将其放在全局对象（global）上。所以在使用Buffer时，无须通过require()即可直接使用。

### 6.1.2 Buffer对象

Buffer对象类似于数组，它的元素为16进制的两位数，即0到255的数值。示例代码如下所示：

由上面的示例可见，不同编码的字符串占用的元素个数各不相同，上面代码中的中文字在UTF-8编码下占用3个元素，字母和半角标点符号占用1个元素。Buffer受Array类型的影响很大，可以访问length属性得到长度，也可以通过下标访问元素，在构造对象时也十分相似，代码如下：

上述代码分配了一个长100字节的Buffer对象。可以通过下标访问刚初始化的Buffer的元素，代码如下：

这里会得到一个比较奇怪的结果，它的元素值是一个0到255的随机值。同样，我们也可以通过下标对它进行赋值：

值得注意的是，如果给元素赋值不是0到255的整数而是小数时会怎样呢？示例代码如下所示：

给元素的赋值如果小于0，就将该值逐次加256，直到得到一个0到255之间的整数。如果得到的数值大于255，就逐次减256，直到得到0~255区间内的数值。如果是小数，舍弃小数部分，只保留整数部分。

### 6.1.3 Buffer内存分配

Buffer对象的内存分配不是在V8的堆内存中，而是在Node的C++层面实现内存的申请的。因为处理大量的字节数据不能采用需要一点内存就向操作系统申请一点内存的方式，这可能造成大量的内存申请的系统调用，对操作系统有一定压力。为此Node在内存的使用上应用的是在C++层面申请内存、在JavaScript中分配内存的策略。为了高效地使用申请来的内存，Node采用了slab分配机制。slab是一种动态内存管理机制，最早诞生于SunOS操作系统（Solaris）中，目前在一些*nix操作系统中有广泛的应用，如FreeBSD和Linux。简单而言，slab就是一块申请好的固定大小的内存区域。slab具有如下3种状态。
- full：完全分配状态。
- partial：部分分配状态。
- empty：没有被分配状态。

当我们需要一个Buffer对象，可以通过以下方式分配指定大小的Buffer对象：

Node以8 KB为界限来区分Buffer是大对象还是小对象：

这个8 KB的值也就是每个slab的大小值，在JavaScript层面，以它作为单位单元进行内存的分配。

1. 分配小Buffer对象

如果指定Buffer的大小少于8 KB, Node会按照小对象的方式进行分配。Buffer的分配过程中主要使用一个局部变量pool作为中间处理对象，处于分配状态的slab单元都指向它。以下是分配一个全新的slab单元的操作，它会将新申请的SlowBuffer对象指向它：

图6-2为一个新构造的slab单元示例。

图6-2 新构造的slab单元示例在图6-2中，slab处于empty状态。构造小Buffer对象时的代码如下：

这次构造将会去检查pool对象，如果pool没有被创建，将会创建一个新的slab单元指向它：

同时当前Buffer对象的parent属性指向该slab，并记录下是从这个slab的哪个位置（offset）开始使用的，slab对象自身也记录被使用了多少字节，代码如下：

图6-3为从一个新的slab单元中初次分配一个Buffer对象的示意图。

图6-3 从一个新的slab单元中初次分配一个Buffer对象这时候的slab状态为partial。当再次创建一个Buffer对象时，构造过程中将会判断这个slab的剩余空间是否足够。如果足够，使用剩余空间，并更新slab的分配状态。下面的代码创建了一个新的Buffer对象，它会引起一次slab分配：

图6-4为再次分配的示意图。

图6-4 从slab单元中再次分配一个Buffer对象如果slab剩余的空间不够，将会构造新的slab，原slab中剩余的空间会造成浪费。例如，第一次构造1字节的Buffer对象，第二次构造8192字节的Buffer对象，由于第二次分配时slab中的空间不够，所以创建并使用新的slab，第一个slab的8 KB将会被第一个1字节的Buffer对象独占。下面的代码一共使用了两个slab单元：

这里要注意的事项是，由于同一个slab可能分配给多个Buffer对象使用，只有这些小Buffer对象在作用域释放并都可以回收时，slab的8 KB空间才会被回收。尽管创建了1个字节的Buffer对象，但是如果不释放它，实际可能是8 KB的内存没有释放。

2. 分配大Buffer对象

如果需要超过8 KB的Buffer对象，将会直接分配一个SlowBuffer对象作为slab单元，这个slab单元将会被这个大Buffer对象独占。

这里的SlowBuffer类是在C++中定义的，虽然引用buffer模块可以访问到它，但是不推荐直接操作它，而是用Buffer替代。上面提到的Buffer对象都是JavaScript层面的，能够被V8的垃圾回收标记回收。但是其内部的parent属性指向的SlowBuffer对象却来自于Node自身C++中的定义，是C++层面上的Buffer对象，所用内存不在V8的堆中。

3. 小结

简单而言，真正的内存是在Node的C++层面提供的，JavaScript层面只是使用它。当进行小而频繁的Buffer操作时，采用slab的机制进行预先申请和事后分配，使得JavaScript到操作系统之间不必有过多的内存申请方面的系统调用。对于大块的Buffer而言，则直接使用C++层面提供的内存，而无需细腻的分配操作。

## 6.2 Buffer 的转换

Buffer对象可以与字符串之间相互转换。目前支持的字符串编码类型有如下这几种。
- ASCII
- UTF-8
- UTF-16LE/UCS-2
- Base64
- Binary
- Hex

### 6.2.1 字符串转Buffer

字符串转Buffer对象主要是通过构造函数完成的：

通过构造函数转换的Buffer对象，存储的只能是一种编码类型。encoding参数不传递时，默认按UTF-8编码进行转码和存储。

一个Buffer对象可以存储不同编码类型的字符串转码的值，调用write()方法可以实现该目的，代码如下：

由于可以不断写入内容到Buffer对象中，并且每次写入可以指定编码，所以Buffer对象中可以存在多种编码转化后的内容。需要小心的是，每种编码所用的字节长度不同，将Buffer反转回字符串时需要谨慎处理。

### 6.2.2 Buffer转字符串

实现Buffer向字符串的转换也十分简单，Buffer对象的toString()可以将Buffer对象转换为字符串，代码如下：

比较精巧的是，可以设置encoding（默认为UTF-8）、start、end这3个参数实现整体或局部的转换。如果Buffer对象由多种编码写入，就需要在局部指定不同的编码，才能转换回正常的编码。

### 6.2.3 Buffer不支持的编码类型

目前比较遗憾的是，Node的Buffer对象支持的编码类型有限，只有少数的几种编码类型可以在字符串和Buffer之间转换。为此，Buffer提供了一个isEncoding()函数来判断编码是否支持转换：

将编码类型作为参数传入上面的函数，如果支持转换返回值为true，否则为false。很遗憾的是，在中国常用的GBK、GB2312和BIG-5编码都不在支持的行列中。对于不支持的编码类型，可以借助Node生态圈中的模块完成转换。iconv和iconv-lite两个模块可以支持更多的编码类型转换，包括Windows 125系列、ISO-8859系列、IBM/DOS代码页系列、Macintosh系列、KOI8系列，以及Latin1、US-ASCII，也支持宽字节编码GBK和GB2312。iconv-lite采用纯JavaScript实现，iconv则通过C++调用libiconv库完成。前者比后者更轻量，无须编译和处理环境依赖直接使用。在性能方面，由于转码都是耗用CPU，在V8的高性能下，少了C++到JavaScript的层次转换，纯JavaScript的性能比C++实现得更好。

以下为iconv-lite的示例代码：

另外，iconv和iconv-lite对无法转换的内容进行降级处理时的方案不尽相同。iconv-lite无法转换的内容如果是多字节，会输出

；如果是单字节，则输出？。iconv则有三级降级策略，会尝试翻译无法转换的内容，或者忽略这些内容。如果不设置忽略，iconv对于无法转换的内容将会得到EILSEQ异常。如下是iconv的示例代码兼选项设置方式：



## 6.3 Buffer 的拼接

Buffer在使用场景中，通常是以一段一段的方式传输。以下是常见的从输入流中读取内容的示例代码：

上面这段代码常见于国外，用于流读取的示范，data事件中获取的chunk对象即是Buffer对象。对于初学者而言，容易将Buffer当做字符串来理解，所以在接受上面的示例时不会觉得有任何异常。一旦输入流中有宽字节编码时，问题就会暴露出来。如果你在通过Node开发的网站上看到

乱码符号，那么该问题的起源多半来自于这里。

这里潜藏的问题在于如下这句代码：

这句代码里隐藏了toString()操作，它等价于如下的代码：

值得注意的是，外国人的语境通常是指英文环境，在他们的场景下，这个toString()不会造成任何问题。但对于宽字节的中文，却会形成问题。为了重现这个问题，下面我们模拟近似的场景，将文件可读流的每次读取的Buffer长度限制为11，代码如下：

搭配该代码的测试数据为李白的《静夜思》。执行该程序，将会得到以下输出：

### 6.3.1 乱码是如何产生的

上面的诗歌中，“月”、“是”、“望”、“低”4个字没有被正常输出，取而代之的是3个

。产生这个输出结果的原因在于文件可读流在读取时会逐个读取Buffer。这首诗的原始Buffer应存储为：

由于我们限定了Buffer对象的长度为11，因此只读流需要读取7次才能完成完整的读取，结果是以下几个Buffer对象依次输出：

上文提到的buf.toString()方法默认以UTF-8为编码，中文字在UTF-8下占3个字节。所以第一个Buffer对象在输出时，只能显示3个字符，Buffer中剩下的2个字节（e6 9c）将会以乱码的形式显示。第二个Buffer对象的第一个字节也不能形成文字，只能显示乱码。于是形成一些文字无法正常显示的问题。在这个示例中我们构造了11这个限制，但是对于任意长度的Buffer而言，宽字节字符串都有可能存在被截断的情况，只不过Buffer的长度越大出现的概率越低而已，但该问题依然不可忽视。

### 6.3.2 setEncoding()与string_decoder()

在看过上述的示例后，也许我们忘记了可读流还有一个设置编码的方法setEncoding()，示例如下：

该方法的作用是让data事件中传递的不再是一个Buffer对象，而是编码后的字符串。为此，我们继续改进前面诗歌的程序，添加setEncoding()的步骤如下：

重新执行程序，得到输出：

这是令人开心的输出结果，说明输出不再受Buffer大小的影响了。那Node是如何实现这个输出结果的呢？要知道，无论如何设置编码，触发data事件的次数依旧相同，这意味着设置编码并未改变按段读取的基本方式。事实上，在调用setEncoding()时，可读流对象在内部设置了一个decoder对象。每次data事件都通过该decoder对象进行Buffer到字符串的解码，然后传递给调用者。是故设置编码后，data不再收到原始的Buffer对象。但是这依旧无法解释为何设置编码后乱码问题被解决掉了，因为在前述分析中，无论如何转码，总是存在宽字节字符串被截断的问题。最终乱码问题得以解决，还是在于decoder的神奇之处。decoder对象来自于string_decoder模块StringDecoder的实例对象。它神奇的原理是什么，下面我们以代码来说明：

我将前文提到的前两个Buffer对象写入decoder中。奇怪的地方在于“月”的转码并没有如平常一样在两个部分分开输出。StringDecoder在得到编码后，知道宽字节字符串在UTF-8编码下是以3个字节的方式存储的，所以第一次write()时，只输出前9个字节转码形成的字符，“月”字的前两个字节被保留在StringDecoder实例内部。第二次write()时，会将这2个剩余字节和后续11个字节组合在一起，再次用3的整数倍字节进行转码。于是乱码问题通过这种中间形式被解决了。虽然string_decoder模块很奇妙，但是它也并非万能药，它目前只能处理UTF-8、Base64和UCS-2/UTF-16LE这3种编码。所以，通过setEncoding()的方式不可否认能解决大部分的乱码问题，但并不能从根本上解决该问题。

### 6.3.3 正确拼接Buffer

淘汰掉setEncoding()方法后，剩下的解决方案只有将多个小Buffer对象拼接为一个Buffer对象，然后通过iconv-lite一类的模块来转码这种方式。+=的方式显然不行，那么正确的Buffer拼接方法应该如下面展示的形式：

正确的拼接方式是用一个数组来存储接收到的所有Buffer片段并记录下所有片段的总长度，然后调用Buffer.concat()方法生成一个合并的Buffer对象。Buffer.concat()方法封装了从小Buffer对象向大Buffer对象的复制过程，实现十分细腻，值得围观学习：

## 6.4 Buffer 与性能

Buffer在文件I/O和网络I/O中运用广泛，尤其在网络传输中，它的性能举足轻重。在应用中，我们通常会操作字符串，但一旦在网络中传输，都需要转换为Buffer，以进行二进制数据传输。在Web应用中，字符串转换到Buffer是时时刻刻发生的，提高字符串到Buffer的转换效率，可以很大程度地提高网络吞吐率。在展开Buffer与网络传输的关系之前，我们可以先来进行一次性能测试。下面的例子中构造了一个10 KB大小的字符串。我们首先通过纯字符串的方式向客户端发送，代码如下：

我们通过ab进行一次性能测试，发起200个并发客户端：

得到的测试结果如下所示：

测试的QPS（每秒查询次数）是2527.64，传输率为每秒25370.16KB。接下来我们取消掉helloworld = new Buffer(helloworld)；前的注释，使向客户端输出的是一个Buffer对象，无须在每次响应时进行转换。再次进行性能测试的结果如下所示：

QPS的提升到4843.28，传输率为每秒48612.56 KB，性能提高近一倍。通过预先转换静态内容为Buffer对象，可以有效地减少CPU的重复使用，节省服务器资源。在Node构建的Web应用中，可以选择将页面中的动态内容和静态内容分离，静态内容部分可以通过预先转换为Buffer的方式，使性能得到提升。由于文件自身是二进制数据，所以在不需要改变内容的场景下，尽量只读取Buffer，然后直接传输，不做额外的转换，避免损耗。

●文件读取

Buffer的使用除了与字符串的转换有性能损耗外，在文件的读取时，有一个highWaterMark设置对性能的影响至关重要。在fs.createReadStream(path,opts)时，我们可以传入一些参数，代码如下：

我们还可以传递start和end来指定读取文件的位置范围：

fs.createReadStream()的工作方式是在内存中准备一段Buffer，然后在fs.read()读取时逐步从磁盘中将字节复制到Buffer中。完成一次读取时，则从这个Buffer中通过slice()方法取出部分数据作为一个小Buffer对象，再通过data事件传递给调用方。如果Buffer用完，则重新分配一个；如果还有剩余，则继续使用。下面为分配一个新的Buffer对象的操作：

在理想的状况下，每次读取的长度就是用户指定的highWaterMark。但是有可能读到了文件结尾，或者文件本身就没有指定的highWaterMark那么大，这个预先指定的Buffer对象将会有部分剩余，不过好在这里的内存可以分配给下次读取时使用。pool是常驻内存的，只有当pool单元剩余数量小于128（kMinPoolSpace）字节时，才会重新分配一个新的Buffer对象。Node源代码中分配新的Buffer对象的判断条件如下所示：

这里与Buffer的内存分配比较类似，highWaterMark的大小对性能有两个影响的点。
- highWaterMark设置对Buffer内存的分配和使用有一定影响。
- highWaterMark设置过小，可能导致系统调用次数过多。

文件流读取基于Buffer分配，Buffer则基于SlowBuffer分配，这可以理解为两个维度的分配策略。如果文件较小（小于8 KB），有可能造成slab未能完全使用。由于fs.createReadStream()内部采用fs.read()实现，将会引起对磁盘的系统调用，对于大文件而言，highWaterMark的大小决定会触发系统调用和data事件的次数。以下为Node自带的基准测试，在benchmark/fs/read-stream-throughput.js中可以找到：

下面为某次执行的结果：

从上面的执行结果我们可以看到，读取一个相同的大文件时，highWaterMark值的大小与读取速度的关系：该值越大，读取速度越快。

## 6.5 总结

体验过JavaScript友好的字符串操作后，有些开发者可能会形成思维定势，将Buffer当做字符串来理解。但字符串与Buffer之间有实质上的差异，即Buffer是二进制数据，字符串与Buffer之间存在编码关系。因此，理解Buffer的诸多细节十分必要，对于如何高效处理二进制数据十分有用。

## 6.6 参考资源

本章参考的资源如下：

- http://nodejs.org/docs/latest/api/buffer.html
- http://nodejs.org/docs/latest/api/string_decoder.html
- https://github.com/bnoordhuis/node-iconv
- https://github.com/ashtuchkin/iconv-lite
- http://httpd.apache.org/docs/2.2/programs/ab.html
- http://cnodejs.org/user/fool
- http://en.wikipedia.org/wiki/Slab_allocation
- https://www.ibm.com/developerworks/cn/linux/l-linux-slab-allocator/

# 第 7 章 网络编程

Node是一个面向网络而生的平台，它具有事件驱动、无阻塞、单线程等特性，具备良好的可伸缩性，使得它十分轻量，适合在分布式网络中扮演各种各样的角色。同时Node提供的API十分贴合网络，适合用它基础的API构建灵活的网络服务。从本章起，我将介绍Node在网络服务器方面的具体能力。利用Node可以十分方便地搭建网络服务器。在Web领域，大多数的编程语言需要专门的Web服务器作为容器，如ASP、ASP.NET需要IIS作为服务器，PHP需要搭载Apache或Nginx环境等，JSP需要Tomcat服务器等。但对于Node而言，只需要几行代码即可构建服务器，无需额外的容器。Node提供了net、dgram、http、https这4个模块，分别用于处理TCP、UDP、HTTP、HTTPS，适用于服务器端和客户端。

## 7.1 构建 TCP 服务

TCP服务在网络应用中十分常见，目前大多数的应用都是基于TCP搭建而成的。

### 7.1.1 TCP

TCP全名为传输控制协议，在OSI模型（由七层组成，分别为物理层、数据链结层、网络层、传输层、会话层、表示层、应用层）中属于传输层协议。许多应用层协议基于TCP构建，典型的是HTTP、SMTP、IMAP等协议。七层协议示意图如图7-1所示。

图7-1 OSI模型（七层协议）TCP是面向连接的协议，其显著的特征是在传输之前需要3次握手形成会话，如图7-2所示。

图7-2 TCP在传输之前的3次握手只有会话形成之后，服务器端和客户端之间才能互相发送数据。在创建会话的过程中，服务器端和客户端分别提供一个套接字，这两个套接字共同形成一个连接。服务器端与客户端则通过套接字实现两者之间连接的操作。

### 7.1.2 创建TCP服务器端

在基本了解TCP的工作原理之后，我们可以开始创建一个TCP服务器端来接受网络请求，代码如下：

我们通过net.createServer(listener)即可创建一个TCP服务器，listener是连接事件connection的侦听器，也可以采用如下的方式进行侦听：

我们可以利用Telnet工具作为客户端对刚才创建的简单服务器进行会话交流，相关代码如下所示：

除了端口外，同样我们也可以对Domain Socket进行监听，代码如下：

通过nc工具进行会话，测试上面构建的TCP服务的代码如下所示：

通过net模块自行构造客户端进行会话，测试上面构建的TCP服务的代码如下所示：

将以上客户端代码存为client.js并执行，如下所示：

其结果与使用Telnet和nc的会话结果并无差别。如果是Domain Socket，在填写选项时，填写path即可，代码如下：

### 7.1.3 TCP服务的事件

在上述的示例中，代码分为服务器事件和连接事件。1．服务器事件对于通过net.createServer()创建的服务器而言，它是一个EventEmitter实例，它的自定义事件有如下几种。
- listening：在调用server.listen()绑定端口或者Domain Socket后触发，简洁写法为server.listen(port, listeningListener)，通过listen()方法的第二个参数传入。
- connection：每个客户端套接字连接到服务器端时触发，简洁写法为通过net.create-Server()，最后一个参数传递。
- close：当服务器关闭时触发，在调用server.close()后，服务器将停止接受新的套接字连接，但保持当前存在的连接，等待所有连接都断开后，会触发该事件。
- error：当服务器发生异常时，将会触发该事件。比如侦听一个使用中的端口，将会触发一个异常，如果不侦听error事件，服务器将会抛出异常。2．连接事件

服务器可以同时与多个客户端保持连接，对于每个连接而言是典型的可写可读Stream对象。Stream对象可以用于服务器端和客户端之间的通信，既可以通过data事件从一端读取另一端发来的数据，也可以通过write()方法从一端向另一端发送数据。它具有如下自定义事件。
- data：当一端调用write()发送数据时，另一端会触发data事件，事件传递的数据即是write()发送的数据。
- end：当连接中的任意一端发送了FIN数据时，将会触发该事件。
- connect：该事件用于客户端，当套接字与服务器端连接成功时会被触发。
- drain：当任意一端调用write()发送数据时，当前这端会触发该事件。
- error：当异常发生时，触发该事件。
- close：当套接字完全关闭时，触发该事件。
- timeout：当一定时间后连接不再活跃时，该事件将会被触发，通知用户当前该连接已经被闲置了。

另外，由于TCP套接字是可写可读的Stream对象，可以利用pipe()方法巧妙地实现管道操作，如下代码实现了一个echo服务器：

值得注意的是，TCP针对网络中的小数据包有一定的优化策略：Nagle算法。如果每次只发送一个字节的内容而不优化，网络中将充满只有极少数有效数据的数据包，将十分浪费网络资源。Nagle算法针对这种情况，要求缓冲区的数据达到一定数量或者一定时间后才将其发出，所以小数据包将会被Nagle算法合并，以此来优化网络。这种优化虽然使网络带宽被有效地使用，但是数据有可能被延迟发送。在Node中，由于TCP默认启用了Nagle算法，可以调用socket.setNoDelay(true)去掉Nagle算法，使得write()可以立即发送数据到网络中。另一个需要注意的是，尽管在网络的一端调用write()会触发另一端的data事件，但是并不意味着每次write()都会触发一次data事件，在关闭掉Nagle算法后，另一端可能会将接收到的多个小数据包合并，然后只触发一次data事件。

## 7.2 构建 UDP 服务

UDP又称用户数据包协议，与TCP一样同属于网络传输层。UDP与TCP最大的不同是UDP不是面向连接的。TCP中连接一旦建立，所有的会话都基于连接完成，客户端如果要与另一个TCP服务通信，需要另创建一个套接字来完成连接。但在UDP中，一个套接字可以与多个UDP服务通信，它虽然提供面向事务的简单不可靠信息传输服务，在网络差的情况下存在丢包严重的问题，但是由于它无须连接，资源消耗低，处理快速且灵活，所以常常应用在那种偶尔丢一两个数据包也不会产生重大影响的场景，比如音频、视频等。UDP目前应用很广泛，DNS服务即是基于它实现的。

### 7.2.1 创建UDP套接字

创建UDP套接字十分简单，UDP套接字一旦创建，既可以作为客户端发送数据，也可以作为服务器端接收数据。下面的代码创建了一个UDP套接字：

### 7.2.2 创建UDP服务器端

若想让UDP套接字接收网络消息，只要调用dgram.bind(port, [address])方法对网卡和端口进行绑定即可。以下为一个完整的服务器端示例：

该套接字将接收所有网卡上41234端口上的消息。在绑定完成后，将触发listening事件。

### 7.2.3 创建UDP客户端

接下来我们创建一个客户端与服务器端进行对话，代码如下：

保存为client.js并执行，服务器端的命令行将会有如下输出：

当套接字对象用在客户端时，可以调用send()方法发送消息到网络中。send()方法的参数如下：

这些参数分别为要发送的Buffer、Buffer的偏移、Buffer的长度、目标端口、目标地址、发送完成后的回调。与TCP套接字的write()相比，send()方法的参数列表相对复杂，但是它更灵活的地方在于可以随意发送数据到网络中的服务器端，而TCP如果要发送数据给另一个服务器端，则需要重新通过套接字构造新的连接。

### 7.2.4 UDP套接字

事件UDP套接字相对TCP套接字使用起来更简单，它只是一个EventEmitter的实例，而非Stream的实例。它具备如下自定义事件。
- message：当UDP套接字侦听网卡端口后，接收到消息时触发该事件，触发携带的数据为消息Buffer对象和一个远程地址信息。
- listening：当UDP套接字开始侦听时触发该事件。
- close：调用close()方法时触发该事件，并不再触发message事件。如需再次触发message事件，重新绑定即可。
- error：当异常发生时触发该事件，如果不侦听，异常将直接抛出，使进程退出。

## 7.3 构建 HTTP 服务

TCP与UDP都属于网络传输层协议，如果要构造高效的网络应用，就应该从传输层进行着手。但是对于经典的应用场景，则无须从传输层协议入手构造自己的应用，比如HTTP或SMTP等，这些经典的应用层协议对于普通应用而言绰绰有余。Node提供了基本的http和https模块用于HTTP和HTTPS的封装，对于其他应用层协议的封装，也能从社区中轻松找到其实现。在Node中构建HTTP服务极其容易，Node官网上的经典例子就展示了如何用寥寥几行代码实现一个HTTP服务器，代码如下：

尽管这个HTTP服务器简单到只能回复Hello World，但是它能维持的并发量和QPS都是不容小觑的，其背后的原因在第3章中有叙述，此处我们不再探讨。这里我们抛开性能，只对其HTTP服务在应用层的实现原理进行展开、讨论和研究。

### 7.3.1 HTTP1．

初识HTTPHTTP的全称是超文本传输协议，英文写作HyperText Transfer Protocol。欲了解Web，先了解HTTP将会极大地提高我们对Web的认知。HTTP构建在TCP之上，属于应用层协议。在HTTP的两端是服务器和浏览器，即著名的B/S模式，如今精彩纷呈的Web即是HTTP的应用。

HTTP得以发展是W3C和IETF两个组织合作的结果，他们最终发布了一系列RFC标准，目前最知名的HTTP标准为RFC 2616。2. HTTP报文为了详细解释HTTP的报文，在启动上述服务器端代码后，我们对经典示例代码进行一次报文的获取，这里采用的工具是curl，通过-v选项，可以显示这次网络通信的所有报文信息，如下所示：

从上述信息中我们可以看到这次网络通信的报文信息分为几个部分，第一部分内容为经典的TCP的3次握手过程，如下所示：

第二部分是在完成握手之后，客户端向服务器端发送请求报文，如下所示：

第三部分是服务器端完成处理后，向客户端发送响应内容，包括响应头和响应体，如下所示：

最后部分是结束会话的信息，如下所示：

从上述的报文信息中可以看出HTTP的特点，它是基于请求响应式的，以一问一答的方式实现服务，虽然基于TCP会话，但是本身却并无会话的特点。

从协议的角度来说，现在的应用，如浏览器，其实是一个HTTP的代理，用户的行为将会通过它转化为HTTP请求报文发送给服务器端，服务器端在处理请求后，发送响应报文给代理，代理在解析报文后，将用户需要的内容呈现在界面上。以浏览器打开一张图片地址为例：首先，浏览器构造HTTP报文发向图片服务器端；然后，服务器端判断报文中的要请求的地址，将磁盘中的图片文件以报文的形式发送给浏览器；浏览器接收完图片后，调用渲染引擎将其显示给用户。简而言之，HTTP服务只做两件事情：处理HTTP请求和发送HTTP响应。无论是HTTP请求报文还是HTTP响应报文，报文内容都包含两个部分：报文头和报文体。上文的报文代码中>和<部分属于报文的头部，由于是GET请求，请求报文中没有包含报文体，响应报文中的Hello World即是报文体。

### 7.3.2 http模块

Node的http模块包含对HTTP处理的封装。在Node中，HTTP服务继承自TCP服务器（net模块），它能够与多个客户端保持连接，由于其采用事件驱动的形式，并不为每一个连接创建额外的线程或进程，保持很低的内存占用，所以能实现高并发。HTTP服务与TCP服务模型有区别的地方在于，在开启keepalive后，一个TCP会话可以用于多次请求和响应。TCP服务以connection为单位进行服务，HTTP服务以request为单位进行服务。http模块即是将connection到request的过程进行了封装，示意图如图7-3所示。

图7-3 http模块将connection到request的过程进行了封装除此之外，http模块将连接所用套接字的读写抽象为ServerRequest和ServerResponse对象，它们分别对应请求和响应操作。在请求产生的过程中，http模块拿到连接中传来的数据，调用二进制模块http_parser进行解析，在解析完请求报文的报头后，触发request事件，调用用户的业务逻辑。该流程的示意图如图7-4所示。

图7-4 http模块产生请求的流程图7-4中的处理程序对应到示例中的代码就是响应Hello World这部分，代码如下：

1. HTTP请求

对于TCP连接的读操作，http模块将其封装为ServerRequest对象。让我们再次查看前面的请求报文，报文头部将会通过http_parser进行解析。请求报文的代码如下所示：

报文头第一行GET / HTTP/1.1被解析之后分解为如下属性。
- req.method属性：值为GET，是为请求方法，常见的请求方法有GET、POST、DELETE、PUT、CONNECT等几种。
- req.url属性：值为/。
- req.httpVersion属性：值为1.1。其余报头是很规律的Key: Value格式，被解析后放置在req.headers属性上传递给业务逻辑以供调用，如下所示：

报文体部分则抽象为一个只读流对象，如果业务逻辑需要读取报文体中的数据，则要在这个数据流结束后才能进行操作，如下所示：

HTTP请求对象和HTTP响应对象是相对较底层的封装，现行的Web框架如Connect和Express都是在这两个对象的基础上进行高层封装完成的。

2. HTTP响应

再来看看HTTP响应对象。HTTP响应相对简单一些，它封装了对底层连接的写操作，可以将其看成一个可写的流对象。它影响响应报文头部信息的API为res.setHeader()和res. writeHead()。在上述示例中：

其分为setHeader()和writeHead()两个步骤。它在http模块的封装下，实际生成如下报文：

我们可以调用setHeader进行多次设置，但只有调用writeHead后，报头才会写入到连接中。除此之外，http模块会自动帮你设置一些头信息，如下所示：

报文体部分则是调用res.write()和res.end()方法实现，后者与前者的差别在于res.end()会先调用write()发送数据，然后发送信号告知服务器这次响应结束，响应结果如下所示：

响应结束后，HTTP服务器可能会将当前的连接用于下一个请求，或者关闭连接。值得注意的是，报头是在报文体发送前发送的，一旦开始了数据的发送，writeHead()和setHeader()将不再生效。这由协议的特性决定。另外，无论服务器端在处理业务逻辑时是否发生异常，务必在结束时调用res.end()结束请求，否则客户端将一直处于等待的状态。当然，也可以通过延迟res.end()的方式实现客户端与服务器端之间的长连接，但结束时务必关闭连接。

3. HTTP服务的事件

如同TCP服务一样，HTTP服务器也抽象了一些事件，以供应用层使用，同样典型的是，服务器也是一个EventEmitter实例。
- connection事件：在开始HTTP请求和响应前，客户端与服务器端需要建立底层的TCP连接，这个连接可能因为开启了keep-alive，可以在多次请求响应之间使用；当这个连接建立时，服务器触发一次connection事件。
- request事件：建立TCP连接后，http模块底层将在数据流中抽象出HTTP请求和HTTP响应，当请求数据发送到服务器端，在解析出HTTP请求头后，将会触发该事件；在res.end()后，TCP连接可能将用于下一次请求响应。
- close事件：与TCP服务器的行为一致，调用server.close()方法停止接受新的连接，当已有的连接都断开时，触发该事件；可以给server.close()传递一个回调函数来快速注册该事件。
- checkContinue事件：某些客户端在发送较大的数据时，并不会将数据直接发送，而是先发送一个头部带Expect: 100-continue的请求到服务器，服务器将会触发checkContinue事件；如果没有为服务器监听这个事件，服务器将会自动响应客户端100 Continue的状态码，表示接受数据上传；如果不接受数据的较多时，响应客户端400 Bad Request拒绝客户端继续发送数据即可。需要注意的是，当该事件发生时不会触发request事件，两个事件之间互斥。当客户端收到100 Continue后重新发起请求时，才会触发request事件。
- connect事件：当客户端发起CONNECT请求时触发，而发起CONNECT请求通常在HTTP代理时出现；如果不监听该事件，发起该请求的连接将会关闭。
- upgrade事件：当客户端要求升级连接的协议时，需要和服务器端协商，客户端会在请求头中带上Upgrade字段，服务器端会在接收到这样的请求时触发该事件。这在后文的WebSocket部分有详细流程的介绍。如果不监听该事件，发起该请求的连接将会关闭。
- clientError事件：连接的客户端触发error事件时，这个错误会传递到服务器端，此时触发该事件。

### 7.3.3 HTTP客户端

在对服务器端的实现进行了描述后，HTTP客户端的原理几乎不用再描述，因为它就是服务器端服务模型的另一部分，处于HTTP的另一端，在整个报文的参与中，报文头和报文体由它产生。同时http模块提供了一个底层API:http.request(options, connect)，用于构造HTTP客户端。下面的示例与上文的curl命令大致相同：

执行上述代码得到以下输出：

其中options参数决定了这个HTTP请求头中的内容，它的选项有如下这些。
- host：服务器的域名或IP地址，默认为localhost。
- hostname：服务器名称。
- port：服务器端口，默认为80。
- localAddress：建立网络连接的本地网卡。
- socketPath:Domain套接字路径。
- method:HTTP请求方法，默认为GET。
- path：请求路径，默认为/。
- headers：请求头对象。
- auth:Basic认证，这个值将被计算成请求头中的Authorization部分。报文体的内容由请求对象的write()和end()方法实现：通过write()方法向连接中写入数据，通过end()方法告知报文结束。它与浏览器中的Ajax调用几近相同，Ajax的实质就是一个异步的网络HTTP请求。

1. HTTP响应

HTTP客户端的响应对象与服务器端较为类似，在ClientRequest对象中，它的事件叫做response。ClientRequest在解析响应报文时，一解析完响应头就触发response事件，同时传递一个响应对象以供操作ClientResponse。后续响应报文体以只读流的方式提供，如下所示：

由于从响应读取数据与服务器端ServerRequest读取数据的行为较为类似，此处不再赘述。

2. HTTP代理如

同服务器端的实现一般，http提供的ClientRequest对象也是基于TCP层实现的，在keepalive的情况下，一个底层会话连接可以多次用于请求。为了重用TCP连接，http模块包含一个默认的客户端代理对象http.globalAgent。它对每个服务器端（host + port）创建的连接进行了管理，默认情况下，通过ClientRequest对象对同一个服务器端发起的HTTP请求最多可以创建5个连接。它的实质是一个连接池，示意图如图7-5所示。

图7-5 HTTP代理对服务器端创建的连接进行管理调用HTTP客户端同时对一个服务器发起10次HTTP请求时，其实质只有5个请求处于并发状态，后续的请求需要等待某个请求完成服务后才真正发出。这与浏览器对同一个域名有下载连接数的限制是相同的行为。

如果你在服务器端通过ClientRequest调用网络中的其他HTTP服务，记得关注代理对象对网络请求的限制。一旦请求量过大，连接限制将会限制服务性能。如需要改变，可以在options中传递agent选项。默认情况下，请求会采用全局的代理对象，默认连接数限制的为5。我们既可以自行构造代理对象，代码如下：

也可以设置agent选项为false值，以脱离连接池的管理，使得请求不受并发的限制。Agent对象的sockets和requests属性分别表示当前连接池中使用中的连接数和处于等待状态的请求数，在业务中监视这两个值有助于发现业务状态的繁忙程度。

3. HTTP客户端事件

与服务器端对应的，HTTP客户端也有相应的事件。
- response：与服务器端的request事件对应的客户端在请求发出后得到服务器端响应时，会触发该事件。
- socket：当底层连接池中建立的连接分配给当前请求对象时，触发该事件。
- connect：当客户端向服务器端发起CONNECT请求时，如果服务器端响应了200状态码，客户端将会触发该事件。
- upgrade：客户端向服务器端发起Upgrade请求时，如果服务器端响应了101 Switching Protocols状态，客户端将会触发该事件。
- continue：客户端向服务器端发起Expect: 100-continue头信息，以试图发送较大数据量，如果服务器端响应100 Continue状态，客户端将触发该事件。

## 7.4 构建 WebSocket 服务

提到Node，不能错过的是WebSocket协议。它与Node之间的配合堪称完美，其理由有两条。
- WebSocket客户端基于事件的编程模型与Node中自定义事件相差无几。
- WebSocket实现了客户端与服务器端之间的长连接，而Node事件驱动的方式十分擅长与大量的客户端保持高并发连接。除此之外，WebSocket与传统HTTP有如下好处。
- 客户端与服务器端只建立一个TCP连接，可以使用更少的连接。
- WebSocket服务器端可以推送数据到客户端，这远比HTTP请求响应模式更灵活、更高效。
- 有更轻量级的协议头，减少数据传送量。WebSocket最早是作为HTML5重要特性而出现的，最终在W3C和IETF的推动下，形成RFC 6455规范。现代浏览器大多都支持WebSocket协议，接下来我们用一段代码来展现WebSocket在客户端的应用示例：

上述代码中，浏览器与服务器端创建WebSocket协议请求，在请求完成后连接打开，每50毫秒向服务器端发送一次数据，同时可以通过onmessage()方法接收服务器端传来的数据。这行为与TCP客户端十分相似，相较于HTTP，它能够双向通信。浏览器一旦能够使用WebSocket，可以想象应用的使用空间极大。

在WebSocket之前，网页客户端与服务器端进行通信最高效的是Comet技术。实现Comet技术的细节是采用长轮询（long-polling）或iframe流。长轮询的原理是客户端向服务器端发起请求，服务器端只在超时或有数据响应时断开连接（res.end()）；客户端在收到数据或者超时后重新发起请求。这个请求行为拖着长长的尾巴，是故用Comet（彗星）来命名它。使用WebSocket的话，网页客户端只需一个TCP连接即可完成双向通信，在服务器端与客户端频繁通信时，无须频繁断开连接和重发请求。连接可以得到高效应用，编程模型也十分简洁。前文也或多或少提到了WebSocket与HTTP的区别，相比HTTP, WebSocket更接近于传输层协议，它并没有在HTTP的基础上模拟服务器端的推送，而是在TCP上定义独立的协议。让人迷惑的部分在于WebSocket的握手部分是由HTTP完成的，使人觉得它可能是基于HTTP实现的。WebSocket协议主要分为两个部分：握手和数据传输。下面我们来详细说一说这两个部分。

### 7.4.1 WebSocket握手

客户端建立连接时，通过HTTP发起请求报文，如下所示：

与普通的HTTP请求协议略有区别的部分在于如下这些协议头：

上述两个字段表示请求服务器端升级协议为WebSocket。其中Sec-WebSocket-Key用于安全校验：

Sec-WebSocket-Key的值是随机生成的Base64编码的字符串。服务器端接收到之后将其与字符串258EAFA5-E914-47DA-95CA-C5AB0DC85B11相连，形成字符串dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11，然后通过sha1安全散列算法计算出结果后，再进行Base64编码，最后返回给客户端。这个算法如下所示：

另外，下面两个字段指定子协议和版本号：

服务器端在处理完请求后，响应如下报文：

上面的报文告之客户端正在更换协议，更新应用层协议为WebSocket协议，并在当前的套接字连接上应用新协议。剩余的字段分别表示服务器端基于Sec-WebSocket-Key生成的字符串和选中的子协议。客户端将会校验Sec-WebSocket-Accept的值，如果成功，将开始接下来的数据传输。这里我们用Node模拟浏览器发起协议切换的行为，代码如下：

下面是服务器端的响应行为：

一旦WebSocket握手成功，服务器端与客户端将会呈现对等的效果，都能接收和发送消息。

### 7.4.2 WebSocket数据传输

在握手顺利完成后，当前连接将不再进行HTTP的交互，而是开始WebSocket的数据帧协议，实现客户端与服务器端的数据交换。图7-6为协议升级过程示意图。

图7-6 协议升级过程示意图握手完成后，客户端的onopen()将会被触发执行，代码如下：

服务器端则没有onopen()方法可言。为了完成TCP套接字事件到WebSocket事件的封装，需要在接收数据时进行处理，WebSocket的数据帧协议即是在底层data事件上封装完成的，代码如下：

同样的数据发送时，也需要做封装操作，代码如下：

当客户端调用send()发送数据时，服务器端触发onmessage()；当服务器端调用send()发送数据时，客户端的onmessage()触发。当我们调用send()发送一条数据时，协议可能将这个数据封装为一帧或多帧数据，然后逐帧发送。

为了安全考虑，客户端需要对发送的数据帧进行掩码处理，服务器一旦收到无掩码帧（比如中间拦截破坏），连接将关闭。而服务器发送到客户端的数据帧则无须做掩码处理，同样，如果客户端收到带掩码的数据帧，连接也将关闭。我们以客户端发送hello world！到服务器端，服务器端回以yakexi作为一个流程来研究数据帧协议的实现过程。图7-7中为WebSocket数据帧的定义，每8位为一列，也即1个字节。其中每一位都有它的意义。

图7-7 WebSocket数据帧的定义
- fin：如果这个数据帧是最后一帧，这个fin位为1，其余情况为0。当一个数据没有被分为多帧时，它既是第一帧也是最后一帧。
- rsv1、rsv2、rsv3：各为1位长，3个标识用于扩展，当有已协商的扩展时，这些值可能为1，其余情况为0。
- opcode：长为4位的操作码，可以用来表示0到15的值，用于解释当前数据帧。0表示附加数据帧，1表示文本数据帧，2表示二进制数据帧，8表示发送一个连接关闭的数据帧，9表示ping数据帧，10表示pong数据帧，其余值暂时没有定义。ping数据帧和pong数据帧用于心跳检测，当一端发送ping数据帧时，另一端必须发送pong数据帧作为响应，告知对方这一端仍然处于响应状态。


- masked：表示是否进行掩码处理，长度为1。客户端发送给服务器端时为1，服务器端发送给客户端时为0。
- payload length：一个7、7+16或7+64位长的数据位，标识数据的长度，如果值在0~125之间，那么该值就是数据的真实长度；如果值是126，则后面16位的值是数据的真实长度；如果值是127，则后面64位的值是数据的真实长度。
- masking key：当masked为1时存在，是一个32位长的数据位，用于解密数据。
- payload data：我们的目标数据，位数为8的倍数。客户端发送消息时，需要构造一个或多个数据帧协议报文。由于hello world！较短，不存在分割为多个数据帧的情况，又由于hello world！会以文本的方式发送，它的payload length长度为96（12字节×8位/字节），二进制表示为1100000。所以报文应当如下：

当以文本方式发送时，文本的编码为UTF-8，由于这里发送的不存在中文，所以一个字符占一个字节，即8位。

客户端发送消息后，服务器端在data事件中接收到这些编码数据，然后解析为相应的数据帧，再以数据帧的格式，通过掩码将真正的数据解密出来，然后触发onmessage()执行，如下所示：

服务器端再回复yakexi的时候，剩下的事情就是无须掩码，其余相同，如下所示：

这里的行为与纯TCP连接的行为十分类似，近似地可以理解为TCP客户端套接字的connect事件和data事件。至此，WebSocket的原理介绍完毕，具体如何解析数据帧和触发onmessage()，请参考ws模块的实现，由于其有过多细节，这里不再展开描述。

### 7.4.3 小结

在所有的WebSocket服务器端实现中，没有比Node更贴近WebSocket的使用方式了。它们的共性有以下内容。
- 基于事件的编程接口。
- 基于JavaScript，以封装良好的WebSocket实现，API与客户端可以高度相似。另外，Node基于事件驱动的方式使得它应对WebSocket这类长连接的应用场景可以轻松地处理大量并发请求。尽管Node没有内置WebSocket的库，但是社区的ws模块封装了WebSocket的底层实现。socket.io即是在它的基础上构建实现的。

## 7.5 网络服务与安全

在网络中，数据在服务器端和客户端之间传递，由于是明文传递的内容，一旦在网络被人监控，数据就可能一览无余地展现在中间的窃听者面前。为此我们需要将数据加密后再进行网络传输，这样即使数据被截获和窃听，窃听者也无法知道数据的真实内容是什么。但是对于我们的应用层协议而言，如HTTP、FTP等，我们仍然希望能够透明地处理数据，而无须操心网络传输过程中的安全问题。在网景公司的NetScape浏览器推出之初就提出了SSL（Secure Sockets Layer，安全套接层）。SSL作为一种安全协议，它在传输层提供对网络连接加密的功能。对于应用层而言，它是透明的，数据在传递到应用层之前就已经完成了加密和解密的过程。最初的SSL应用在Web上，被服务器端和浏览器端同时支持，随后IETF将其标准化，称为TLS（Transport Layer Security，安全传输层协议）。Node在网络安全上提供了3个模块，分别为crypto、tls、https。其中crypto主要用于加密解密，SHA1、MD5等加密算法都在其中有体现，在这里我们不用再提。真正用于网络的是另外两个模块，tls模块提供了与net模块类似的功能，区别在于它建立在TLS/SSL加密的TCP连接上。对于https而言，它完全与http模块接口一致，区别也仅在于它建立于安全的连接之上。

### 7.5.1 TLS/SSL

1．密钥

TLS/SSL是一个公钥/私钥的结构，它是一个非对称的结构，每个服务器端和客户端都有自己的公私钥。公钥用来加密要传输的数据，私钥用来解密接收到的数据。公钥和私钥是配对的，通过公钥加密的数据，只有通过私钥才能解密，所以在建立安全传输之前，客户端和服务器端之间需要互换公钥。客户端发送数据时要通过服务器端的公钥进行加密，服务器端发送数据时则需要客户端的公钥进行加密，如此才能完成加密解密的过程，如图7-8所示。

图7-8 客户端和服务器端交换密钥Node在底层采用的是openssl实现TLS/SSL的，为此要生成公钥和私钥可以通过openssl完成。我们分别为服务器端和客户端生成私钥，如下所示：

上述命令生成了两个1024位长的RSA私钥文件，我们可以通过它继续生成公钥，如下所示：

公私钥的非对称加密虽好，但是网络中依然可能存在窃听的情况，典型的例子是中间人攻击。客户端和服务器端在交换公钥的过程中，中间人对客户端扮演服务器端的角色，对服务器端扮演客户端的角色，因此客户端和服务器端几乎感受不到中间人的存在。为了解决这种问题，数据传输过程中还需要对得到的公钥进行认证，以确认得到的公钥是出自目标服务器。如果不能保证这种认证，中间人可能会将伪造的站点响应给用户，从而造成经济损失。图7-9是中间人攻击的示意图。

图7-9 中间人攻击示意图为了解决这个问题，TLS/SSL引入了数字证书来进行认证。与直接用公钥不同，数字证书中包含了服务器的名称和主机名、服务器的公钥、签名颁发机构的名称、来自签名颁发机构的签名。在连接建立前，会通过证书中的签名确认收到的公钥是来自目标服务器的，从而产生信任关系。

2．数字证书

为了确保我们的数据安全，现在我们引入了一个第三方：CA（CertificateAuthority，数字证书认证中心）。CA的作用是为站点颁发证书，且这个证书中具有CA通过自己的公钥和私钥实现的签名。为了得到签名证书，服务器端需要通过自己的私钥生成CSR（Certificate SigningRequest，证书签名请求）文件。CA机构将通过这个文件颁发属于该服务器端的签名证书，只要通过CA机构就能验证证书是否合法。通过CA机构颁发证书通常是一个烦琐的过程，需要付出一定的精力和费用。对于中小型企业而言，多半是采用自签名证书来构建安全网络的。所谓自签名证书，就是自己扮演CA机构，给自己的服务器端颁发签名证书。以下为生成私钥、生成CSR文件、通过私钥自签名生成证书的过程：

其流程如图7-10所示。

图7-10 生成自签名证书示意图上述步骤完成了扮演CA角色需要的文件。接下来回到服务器端，服务器端需要向CA机构申请签名证书。在申请签名证书之前依然是要创建自己的CSR文件。值得注意的是，这个过程中的Common Name要匹配服务器域名，否则在后续的认证过程中会出错。如下是生成CSR文件所用的命令：

得到CSR文件后，向我们自己的CA机构申请签名吧。签名过程需要CA的证书和私钥参与，最终颁发一个带有CA签名的证书，如下所示：

客户端在发起安全连接前会去获取服务器端的证书，并通过CA的证书验证服务器端证书的真伪。除了验证真伪外，通常还含有对服务器名称、IP地址等进行验证的过程。这个验证过程如图7-11所示。

图7-11 客户端通过CA验证服务器端证书的真伪过程示意图CA机构将证书颁发给服务器端后，证书在请求的过程中会被发送给客户端，客户端需要通过CA的证书验证真伪。如果是知名的CA机构，它们的证书一般预装在浏览器中。如果是自己扮演CA机构，颁发自有签名证书则不能享受这个福利，客户端需要获取到CA的证书才能进行验证。上述的过程中可以看出，签名证书是一环一环地颁发的，但是在CA那里的证书是不需要上级证书参与签名的，这个证书我们通常称为根证书。

### 7.5.2 TLS服务

1．创建服务器端

将构建服务所需要的证书都备齐之后，我们通过Node的tls模块来创建一个安全的TCP服务，这个服务是一个简单的echo服务，代码如下：

启动上述服务后，通过下面的命令可以测试证书是否正常：

2. TLS客户端为了完善整个体系，接下来我们用Node来模拟客户端，如同net模块一样，tls模块也提供了connect()方法来构建客户端。在构建我们的客户端之前，需要为客户端生成属于自己的私钥和签名，代码如下：

并创建客户端，代码如下：

启动客户端的过程中，用到了为客户端生成的私钥、证书、CA证书。客户端启动之后可以在输入流中输入数据，服务器端将会回应相同的数据。至此我们完成了TLS的服务器端和客户端的创建。与普通的TCP服务器端和客户端相比，TLS的服务器端和客户端仅仅只在证书的配置上有差别，其余部分基本相同。

### 7.5.3 HTTPS服务

HTTPS服务就是工作在TLS/SSL上的HTTP。在了解了TLS服务后，创建HTTPS服务是再简单不过的事情。

1．准备证书

HTTPS服务需要用到私钥和签名证书，我们可以直接用上文生成的私钥和证书。

2．创建HTTPS服务

创建HTTPS服务只比HTTP服务多一个选项配置，其余地方几乎相同，代码如下：

启动之后通过curl进行测试，相关代码如下所示：

由于是自签名的证书，curl工具无法验证服务器端证书是否正确，所以出现了上述的抛错，要解决上面的问题有两种方式。一种是加-k选项，让curl工具忽略掉证书的验证，这样的结果是数据依然会通过公钥加密传输，但是无法保证对方是可靠的，会存在中间人攻击的潜在风险。其结果如下所示：

另一种解决的方式是给curl设置--cacert选项，告知CA证书使之完成对服务器证书的验证，如下所示：

3. HTTPS客户端

对应的，我们也会用Node来实现HTTPS的客户端，与HTTP的客户端相差不大，除了指定证书相关的参数外，如下所示：

执行上面的操作得到以下输出：

如果不设置ca选项，将会得到如下异常：

解决该异常的方案是添加选项属性rejectUnauthorized为false，它的效果与curl工具加-k一样，都会在数据传输过程中会加密，但是无法保证服务器端的证书不是伪造的。

## 7.6 总结

Node基于事件驱动和非阻塞设计，在分布式环境中尤其能发挥出它的特长，基于事件驱动可以实现与大量的客户端进行连接，非阻塞设计则让它可以更好地提升网络的响应吞吐。Node提供了相对底层的网络调用，以及基于事件的编程接口，使得开发者在这些模块上十分轻松地构建网络应用。下一章我们将在本章的基础上探讨具体的Web应用。

## 7.7 参考资源

本章参考的资源如下：

- http://tools.ietf.org/html/rfc2616
- http://hi.baidu.com/miracletan2008/item/0bc16c9d7af261de7b7f01a2
- http://tools.ietf.org/html/rfc6455
- http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
- http://en.wikipedia.org/wiki/OSI_model
- http://upload.wikimedia.org/wikipedia/commons/a/ae/SSL_handshake_with_two_way_authentication_with_certificates.svg

# 第 8 章 构建 Web 应用

如今看来，Web应用俨然是互联网的主角，伴随Web 1.0、Web 2.0一路走来，HTTP占据了网络中的大多数流量。随着移动互联网时代的到来，Web又开始在移动浏览器上发挥光和热。在Web标准化的努力过后，Web又开始朝向应用化发展，JavaScript在前端变得炙手可热。许多原本在服务器端实现的业务细节，纷纷前移到浏览器端，前端MV*的架构也日趋成熟。与之逆流的是，Node的出现将前后端的壁垒再次打破，JavaScript这门最初就能运行在服务器端的语言，在经历了前端的辉煌和后端的低迷后，借助事件驱动和V8的高性能，再次成为了服务器端的佼佼者。在Web应用中，JavaScript将不再仅仅出现在前端浏览器中，因为Node的出现，“前端”将会被重新定义。为了胜任Web应用的开发工作，各种语言、模式、框架层出不穷。单从框架而言，在后端数得出来大名的就有Struts、CodeIgniter、Rails、Django、web.py等，在前端也有知名的BackBone、Knockout. js、AngularJS、Meteor等。在Node中，有Connect中间件，也有Express这样的MVC框架。值得注意的是Meteor框架，它在后端是Node，在前端是JavaScript，它是一个融合了前后端JavaScript的框架。由于前后端采用的语言都是JavaScript，在跨越HTTP进行沟通时，会有一些额外的好处。
 
- 无须切换语言环境，部分知识不会因为语言环境的切换而丢失，上下文一致性较好。
- 数据（因为JSON）可以很好地实现跨前后端直接使用。
- 一些业务（如模板渲染）可以很自由地轻量地选择是在前端还是在后端进行，因为编程语言相同，所以切换代价小。本章会展开描述Web应用在后端实现中的细节和原理。

## 8.1 基础功能

在第7章中，我们介绍了Node的网络编程部分。从中我们可以发现，Node是十分贴近网络协议的，它的非阻塞、事件机制使得我们在网络编程时十分轻便。而本章的Web应用方面的内容，将从http模块中服务器端的request事件开始分析。request事件发生于网络连接建立，客户端向服务器端发送报文，服务器端解析报文，发现HTTP请求的报头时。在已触发reqeust事件前，它已准备好ServerRequest和ServerResponse对象以供对请求和响应报文的操作。以官方经典的Hello World为例，就是调用ServerResponse实现响应的，如下所示：

对于一个Web应用而言，仅仅只是上面这样的响应远远达不到业务的需求。在具体的业务中，我们可能有如下这些需求。
- 请求方法的判断。
- URL的路径解析。
- URL中查询字符串解析。
- Cookie的解析。
- Basic认证。
- 表单数据的解析。
- 任意格式文件的上传处理。

除此之外，可能还有Session（会话）的需求。尽管Node提供的底层API相对来说比较简单，但要完成业务需求，还需要大量的工作，仅仅一个request事件似乎无法满足这些需求。但是要实现这些需求并非难事，一切的一切，都从如下这个函数展开：

在第4章中，我们曾对高阶函数有过简单的介绍：我们的应用可能无限地复杂，但是只要最终结果返回一个上面的函数作为参数，传递给createServer()方法作为request事件的侦听器就可以了。你可能看到Connect或Express的示例中有如下这样的代码：

它的原理即是如此。我们在具体业务开始前，需要为业务预处理一些细节，这些细节将会挂载在req或res对象上，供业务代码使用。

### 8.1.1 请求方法

在Web应用中，最常见的请求方法是GET和POST，除此之外，还有HEAD、DELETE、PUT、CONNECT等方法。请求方法存在于报文的第一行的第一个单词，通常是大写。如下为一个报文头的示例：

HTTP_Parser在解析请求报文的时候，将报文头抽取出来，设置为req.method。通常，我们只需要处理GET和POST两类请求方法，但是在RESTful类Web服务中请求方法十分重要，因为它会决定资源的操作行为。PUT代表新建一个资源，POST表示要更新一个资源，GET表示查看一个资源，而DELETE表示删除一个资源。我们可以通过请求方法来决定响应行为，如下所示：

上述代码代表了一种根据请求方法将复杂的业务逻辑分发的思路，是一种化繁为简的方式。

### 8.1.2 路径解析

除了根据请求方法来进行分发外，最常见的请求判断莫过于路径的判断了。路径部分存在于报文的第一行的第二部分，如下所示：

HTTP_Parser将其解析为req.url。一般而言，完整的URL地址是如下这样的：

客户端代理（浏览器）会将这个地址解析成报文，将路径和查询部分放在报文第一行。需要注意的是，hash部分会被丢弃，不会存在于报文的任何地方。最常见的根据路径进行业务处理的应用是静态文件服务器，它会根据路径去查找磁盘中的文件，然后将其响应给客户端，如下所示：

还有一种比较常见的分发场景是根据路径来选择控制器，它预设路径为控制器和行为的组合，无须额外配置路由信息，如下所示：

这里的controller会对应到一个控制器，action对应到控制器的行为，剩余的值会作为参数进行一些别的判断。

这样我们的业务部分可以只关心具体的业务实现，如下所示：

### 8.1.3 查询字符串

查询字符串位于路径之后，在地址栏中路径后的？foo=bar&baz=val字符串就是查询字符串。这个字符串会跟随在路径后，形成请求报文首行的第二部分。这部分内容经常需要为业务逻辑所用，Node提供了querystring模块用于处理这部分数据，如下所示：

更简洁的方法是给url.parse()传递第二个参数，如下所示：

它会将foo=bar&baz=val解析为一个JSON对象，如下所示：

在业务调用产生之前，我们的中间件或者框架会将查询字符串转换，然后挂载在请求对象上供业务使用，如下所示：

要注意的点是，如果查询字符串中的键出现多次，那么它的值会是一个数组，如下所示：

业务的判断一定要检查值是数组还是字符串，否则可能出现TypeError异常的情况。

### 8.1.4 Cookie

1．初识Cookie

在Web应用中，请求路径和查询字符串对业务至关重要，通过它们已经可以进行很多业务操作了，但是HTTP是一个无状态的协议，现实中的业务却是需要一定的状态的，否则无法区分用户之间的身份。如何标识和认证一个用户，最早的方案就是Cookie（曲奇饼）了。Cookie最早由文本浏览器Lynx合作开发者Lou Montulli在1994年网景公司开发Netscape浏览器的第一个版本时发明。它能记录服务器与客户端之间的状态，最早的用处就是用来判断用户是否第一次访问网站。在1997年形成规范RFC 2109，目前最新的规范为RFC 6265，它是一个由浏览器和服务器共同协作实现的规范。Cookie的处理分为如下几步。
- 服务器向客户端发送Cookie。
- 浏览器将Cookie保存。
- 之后每次浏览器都会将Cookie发向服务器端。客户端发送的Cookie在请求报文的Cookie字段中，我们可以通过curl工具构造这个字段，如下所示：

HTTP_Parser会将所有的报文字段解析到req.headers上，那么Cookie就是req.headers. cookie。根据规范中的定义，Cookie值的格式是key=value;key2=value2形式的，如果我们需要Cookie，解析它也十分容易，如下所示：

在业务逻辑代码执行之前，我们将其挂载在req对象上，让业务代码可以直接访问，如下所示：

这样我们的业务代码就可以进行判断处理了，如下所示：

任何请求报文中，如果Cookie值没有isVisit，都会收到“欢迎第一次来到动物园”这样的响应。这里提出一个问题，如果识别到用户没有访问过我们的站点，那么我们的站点是否应该告诉客户端已经访问过的标识呢？告知客户端的方式是通过响应报文实现的，响应的Cookie值在Set-Cookie字段中。它的格式与请求中的格式不太相同，规范中对它的定义如下所示：

其中name=value是必须包含的部分，其余部分皆是可选参数。这些可选参数将会影响浏览器在后续将Cookie发送给服务器端的行为。以下为主要的几个选项。

- path表示这个Cookie影响到的路径，当前访问的路径不满足该匹配时，浏览器则不发送这个Cookie。
- Expires和Max-Age是用来告知浏览器这个Cookie何时过期的，如果不设置该选项，在关闭浏览器时会丢失掉这个Cookie。如果设置了过期时间，浏览器将会把Cookie内容写入到磁盘中并保存，下次打开浏览器依旧有效。Expires的值是一个UTC格式的时间字符串，告知浏览器此Cookie何时将过期，Max-Age则告知浏览器此Cookie多久后过期。前者一般而言不存在问题，但是如果服务器端的时间和客户端的时间不能匹配，这种时间设置就会存在偏差。为此，Max-Age告知浏览器这条Cookie多久之后过期，而不是一个具体的时间点。
- HttpOnly告知浏览器不允许通过脚本document.cookie去更改这个Cookie值，事实上，设置HttpOnly之后，这个值在document.cookie中不可见。但是在HTTP请求的过程中，依然会发送这个Cookie到服务器端。
- Secure。当Secure值为true时，在HTTP中是无效的，在HTTPS中才有效，表示创建的Cookie只能在HTTPS连接中被浏览器传递到服务器端进行会话验证，如果是HTTP连接则不会传递该信息，所以很难被窃听到。知道Cookie在报文头中的具体格式后，下面我们将Cookie序列化成符合规范的字符串，相关代码如下：

略改前文的访问逻辑，我们就能轻松地判断用户的状态了，如下所示：

客户端收到这个带Set-Cookie的响应后，在之后的请求时会在Cookie字段中带上这个值。值得注意的是，Set-Cookie是较少的，在报头中可能存在多个字段。为此res.setHeader的第二个参数可以是一个数组，如下所示：

这会在报文头部中形成两条Set-Cookie字段：

2. Cookie的性能影响

由于Cookie的实现机制，一旦服务器端向客户端发送了设置Cookie的意图，除非Cookie过期，否则客户端每次请求都会发送这些Cookie到服务器端，一旦设置的Cookie过多，将会导致报头较大。大多数的Cookie并不需要每次都用上，因为这会造成带宽的部分浪费。在YSlow的性能优化规则中有这么一条：

●减小Cookie的大小

更严重的情况是，如果在域名的根节点设置Cookie，几乎所有子路径下的请求都会带上这些Cookie，这些Cookie在某些情况下是有用的，但是在有些情况下是完全无用的。其中以静态文件最为典型，静态文件的业务定位几乎不关心状态，Cookie对它而言几乎是无用的，但是一旦有Cookie设置到相同域下，它的请求中就会带上Cookie。好在Cookie在设计时限定了它的域，只有域名相同时才会发送。所以YSlow中有另外一条规则用来避免Cookie带来的性能影响。

●为静态组件使用不同的域名

简而言之就是，为不需要Cookie的组件换个域名可以实现减少无效Cookie的传输。所以很多网站的静态文件会有特别的域名，使得业务相关的Cookie不再影响静态资源。当然换用额外的域名带来的好处不只这点，还可以突破浏览器下载线程数量的限制，因为域名不同，可以将下载线程数翻倍。但是换用额外域名还是有一定的缺点的，那就是将域名转换为IP需要进行DNS查询，多一个域名就多一次DNS查询。YSlow中有这样一条规则：

●减少DNS查询

看起来减少DNS查询和使用不同的域名是冲突的两条规则，但是好在现今的浏览器都会进行DNS缓存，以削弱这个副作用的影响。Cookie除了可以通过后端添加协议头的字段设置外，在前端浏览器中也可以通过JavaScript进行修改，浏览器将Cookie通过document.cookie暴露给了JavaScript。前端在修改Cookie之后，后续的网络请求中就会携带上修改过后的值。目前，广告和在线统计领域是最为依赖Cookie的，通过嵌入第三方的广告或者统计脚本，将Cookie和当前页面绑定，这样就可以标识用户，得到用户的浏览行为，广告商就可以定向投放广告了。尽管这样的行为看起来很可怕，但是从Cookie的原理来说，它只能做到标识，而不能做任何具有破坏性的事情。如果依然担心自己站点的用户被记录下行为，那就不要挂任何第三方的脚本。

### 8.1.5 Session

通过Cookie，浏览器和服务器可以实现状态的记录。但是Cookie并非是完美的，前文提及的体积过大就是一个显著的问题，最为严重的问题是Cookie可以在前后端进行修改，因此数据就极容易被篹改和伪造。如果服务器端有部分逻辑是根据Cookie中的isVIP字段进行判断，那么一个普通用户通过修改Cookie就可以轻松享受到VIP服务了。综上所述，Cookie对于敏感数据的保护是无效的。为了解决Cookie敏感数据的问题，Session应运而生。Session的数据只保留在服务器端，客户端无法修改，这样数据的安全性得到一定的保障，数据也无须在协议中每次都被传递。虽然在服务器端存储数据十分方便，但是如何将每个客户和服务器中的数据一一对应起来，这里有常见的两种实现方式。

●第一种：基于Cookie来实现用户和数据的映射

虽然将所有数据都放在Cookie中不可取，但是将口令放在Cookie中还是可以的。因为口令一旦被篹改，就丢失了映射关系，也无法修改服务器端存在的数据了。并且Session的有效期通常较短，普遍的设置是20分钟，如果在20分钟内客户端和服务器端没有交互产生，服务器端就将数据删除。由于数据过期时间较短，且在服务器端存储数据，因此安全性相对较高。那么口令是如何产生的呢？一旦服务器端启用了Session，它将约定一个键值作为Session的口令，这个值可以随意约定，比如Connect默认采用connect_uid, Tomcat会采用jsessionid等。一旦服务器检查到用户请求Cookie中没有携带该值，它就会为之生成一个值，这个值是唯一且不重复的值，并设定超时时间。以下为生成session的代码：

每个请求到来时，检查Cookie中的口令与服务器端的数据，如果过期，就重新生成，如下所示：

当然仅仅重新生成Session还不足以完成整个流程，还需要在响应给客户端时设置新的值，以便下次请求时能够对应服务器端的数据。这里我们hack响应对象的writeHead()方法，在它的内部注入设置Cookie的逻辑，如下所示：

至此，session在前后端进行对应的过程就完成了。这样的业务逻辑可以判断和设置session，以此来维护用户与服务器端的关系，如下所示：

这样在session中保存的数据比直接在Cookie中保存数据要安全得多。这种实现方案依赖Cookie实现，而且也是目前大多数Web应用的方案。如果客户端禁止使用Cookie，这个世界上大多数的网站将无法实现登录等操作。

●第二种：通过查询字符串来实现

浏览器端和服务器端数据的对应它的原理是检查请求的查询字符串，如果没有值，会先生成新的带值的URL，如下所示：

然后形成跳转，让客户端重新发起请求，如下所示：

用户访问 http://localhost/pathname 时，如果服务器端发现查询字符串中不带session_id参数，就会将用户跳转到 http://localhost/pathname?session_id=12344567 这样一个类似的地址。如果浏览器收到302状态码和Location报头，就会重新发起新的请求，如下所示：

这样，新的请求到来时就能通过Session的检查，除非内存中的数据过期。有的服务器在客户端禁用Cookie时，会采用这种方案实现退化。通过这种方案，无须在响应时设置Cookie。但是这种方案带来的风险远大于基于Cookie实现的风险，因为只要将地址栏中的地址发给另外一个人，那么他就拥有跟你相同的身份。Cookie的方案在换了浏览器或者换了电脑之后无法生效，相对较为安全。还有一种比较有趣的处理Session的方式是利用HTTP请求头中的ETag，同样对于更换浏览器和电脑后也是无效的，具体的细节这里就不展开了，感兴趣的朋友可以到网上查阅相关资料。

1. Session与内存

在上面的示例代码中，我们都将Session数据直接存在变量sessions中，它位于内存中。然而在第5章的内存控制部分，我们分析了为什么Node会存在内存限制，这里将数据存放在内存中将会带来极大的隐患，如果用户增多，我们很可能就接触到了内存限制的上限，并且内存中的数据量加大，必然会引起垃圾回收的频繁扫描，引起性能问题。

另一个问题则是我们可能为了利用多核CPU而启动多个进程，这个细节在第9章中有详细描述。用户请求的连接将可能随意分配到各个进程中，Node的进程与进程之间是不能直接共享内存的，用户的Session可能会引起错乱。为了解决性能问题和Session数据无法跨进程共享的问题，常用的方案是将Session集中化，将原本可能分散在多个进程里的数据，统一转移到集中的数据存储中。目前常用的工具是Redis、Memcached等，通过这些高效的缓存，Node进程无须在内部维护数据对象，垃圾回收问题和内存限制问题都可以迎刃而解，并且这些高速缓存设计的缓存过期策略更合理更高效，比在Node中自行设计缓存策略更好。采用第三方缓存来存储Session引起的一个问题是会引起网络访问。理论上来说访问网络中的数据要比访问本地磁盘中的数据速度要慢，因为涉及到握手、传输以及网络终端自身的磁盘I/O等，尽管如此但依然会采用这些高速缓存的理由有以下几条：
- Node与缓存服务保持长连接，而非频繁的短连接，握手导致的延迟只影响初始化。
- 高速缓存直接在内存中进行数据存储和访问。
- 缓存服务通常与Node进程运行在相同的机器上或者相同的机房里，网络速度受到的影响较小。

尽管采用专门的缓存服务会比直接在内存中访问慢，但其影响小之又小，带来的好处却远远大于直接在Node中保存数据。为此，一旦Session需要异步的方式获取，代码就需要略作调整，变成异步的方式，如下所示：

在响应时，将新的session保存回缓存中，如下所示：

2. Session与安全

从前文可以知道，尽管我们的数据都放置在后端了，使得它能保障安全，但是无论通过Cookie，还是查询字符串的实现方式，Session的口令依然保存在客户端，这里会存在口令被盗用的情况。如果Web应用的用户十分多，自行设计的随机算法的一些口令值就有理论机会命中有效的口令值。一旦口令被伪造，服务器端的数据也可能间接被利用。这里提到的Session的安全，就主要指如何让这个口令更加安全。有一种做法是将这个口令通过私钥加密进行签名，使得伪造的成本较高。客户端尽管可以伪造口令值，但是由于不知道私钥值，签名信息很难伪造。如此，我们只要在响应时将口令和签名进行对比，如果签名非法，我们将服务器端的数据立即过期即可，如下所示：

在响应时，设置session值到Cookie中或者跳转URL中，如下所示：

接收请求时，检查签名，如下所示：

这样一来，即使攻击者知道口令中．号前的值是服务器端Session的ID值，只要不知道secret私钥的值，就无法伪造签名信息，以此实现对Session的保护。该方法被Connect中间件框架所使用，保护好私钥，就是在保障自己Web应用的安全。当然，将口令进行签名是一个很好的解决方案，但是如果攻击者通过某种方式获取了一个真实的口令和签名，他就能实现身份的伪装。一种方案是将客户端的某些独有信息与口令作为原值，然后签名，这样攻击者一旦不在原始的客户端上进行访问，就会导致签名失败。这些独有信息包括用户IP和用户代理（User Agent）。但是原始用户与攻击者之间也存在上述信息相同的可能性，如局域网出口IP相同，相同的客户端信息等，不过纳入这些考虑能够提高安全性。通常而言，将口令存在Cookie中不容易被他人获取，但是一些别的漏洞可能导致这个口令被泄漏，典型的有XSS漏洞，下面简单介绍一下如何通过XSS拿到用户的口令，实现伪造。

●XSS漏洞

XSS的全称是跨站脚本攻击（Cross Site Scripting，通常简称为XSS），通常都是由网站开发者决定哪些脚本可以执行在浏览器端，不过XSS漏洞会让别的脚本执行。它的主要形成原因多数是用户的输入没有被转义，而被直接执行。

下面是某个网站的前端脚本，它会将URL hash中的值设置到页面中，以实现某种逻辑，如下所示：

攻击者在发现这里的漏洞后，构造了这样的URL：

为了不让受害者直接发现这段URL中的猫腻，它可能会通过URL压缩成一个短网址，如下所示：

然后将最终的短网址发给某个登录的在线用户。这样一来，这段hash中的脚本将会在这个用户的浏览器中执行，而这段脚本中的内容如下所示：

这段代码将该用户的Cookie提交给了c.com站点，这个站点就是攻击者的服务器，他也就能拿到该用户的Session口令。然后他在客户端中用这个口令伪造Cookie，从而实现了伪装用户的身份。如果该用户是网站管理员，就可能造成极大的危害。XSS造成的危害远远不止这些，这里不再过多介绍。在这个案例中，如果口令中有用户的客户端信息的签名，即使口令被泄漏，除非攻击者与用户客户端完全相同，否则不能实现伪造。

### 8.1.6 缓存

我们知道软件的架构经历过一次C/S模式到B/S模式的演变，在HTTP之上构建的应用，其客户端除了比普通桌面应用具备更轻量的升级和部署等特性外，在跨平台、跨浏览器、跨设备上也具备独特优势。传统客户端在安装后的应用过程中仅仅需要传输数据，Web应用还需要传输构成界面的组件（HTML、JavaScript、CSS文件等）。这部分内容在大多数场景下并不经常变更，却需要在每次的应用中向客户端传递，如果不进行处理，那么它将造成不必要的带宽浪费。如果网络速度较差，就需要花费更多时间来打开页面，对于用户的体验将会造成一定影响。因此节省不必要的传输，对用户和对服务提供者来说都有好处。为了提高性能，YSlow中也提到几条关于缓存的规则。
- 添加Expires或Cache-Control到报文头中。
- 配置ETags。
- 让Ajax可缓存。

这里我们将展开这几条规则的来源。如何让浏览器缓存我们的静态资源，这也是一个需要由服务器与浏览器共同协作完成的事情。RFC 2616规范对此有一定的描述，只有遵循约定，整个缓存机制才能有效建立。通常来说，POST、DELETE、PUT这类带行为性的请求操作一般不做任何缓存，大多数缓存只应用在GET请求中。使用缓存的流程如图8-1所示。

图8-1 使用缓存的流程示意图简单来讲，本地没有文件时，浏览器必然会请求服务器端的内容，并将这部分内容放置在本地的某个缓存目录中。在第二次请求时，它将对本地文件进行检查，如果不能确定这份本地文件是否可以直接使用，它将会发起一次条件请求。所谓条件请求，就是在普通的GET请求报文中，附带If-Modified-Since字段，如下所示：

它将询问服务器端是否有更新的版本，本地文件的最后修改时间。如果服务器端没有新的版本，只需响应一个304状态码，客户端就使用本地版本。如果服务器端有新的版本，就将新的内容发送给客户端，客户端放弃本地版本。代码如下所示：

这里的条件请求采用时间戳的方式实现，但是时间戳有一些缺陷存在。
- 文件的时间戳改动但内容并不一定改动。
- 时间戳只能精确到秒级别，更新频繁的内容将无法生效。

为此HTTP1.1中引入了ETag来解决这个问题。ETag的全称是Entity Tag，由服务器端生成，服务器端可以决定它的生成规则。如果根据文件内容生成散列值，那么条件请求将不会受到时间戳改动造成的带宽浪费。下面是根据内容生成散列值的方法：

与If-Modified-Since/Last-Modified不同的是，ETag的请求和响应是If-None-Match/ETag，如下所示：

浏览器在收到ETag: "83-1359871272000"这样的响应后，在下次的请求中，会将其放置在请求头中：If-None-Match:"83-1359871272000"。尽管条件请求可以在文件内容没有修改的情况下节省带宽，但是它依然会发起一个HTTP请求，使得客户端依然会花一定时间来等待响应。可见最好的方案就是连条件请求都不用发起。那么如何让浏览器知晓是否能直接使用本地版本呢？答案就是服务器端在响应内容时，让浏览器明确地将内容缓存起来。如同YSlow规则里提到的，在响应里设置Expires或Cache-Control头，浏览器将根据该值进行缓存。那么这两个值有何区别呢？

HTTP1.0时，在服务器端设置Expires可以告知浏览器要缓存文件内容，如下代码所示：

Expires是一个GMT格式的时间字符串。浏览器在接到这个过期值后，只要本地还存在这个缓存文件，在到期时间之前它都不会再发起请求。YUI3的CDN实践是缓存文件在10年后过期。但是Expires的缺陷在于浏览器与服务器之间的时间可能不一致，这可能会带来一些问题，比如文件提前过期，或者到期后并没有被删除。在这种情况下，Cache-Control以更丰富的形式，实现相同的功能，如下所示：

上面的代码为Cache-Control设置了max-age值，它比Expires优秀的地方在于，Cache-Control能够避免浏览器端与服务器端时间不同步带来的不一致性问题，只要进行类似倒计时的方式计算过期时间即可。除此之外，Cache-Control的值还能设置public、private、no-cache、no-store等能够更精细地控制缓存的选项。由于在HTTP1.0时还不支持max-age，如今的服务器端在模块的支持下多半同时对Expires和Cache-Control进行支持。在浏览器中如果两个值同时存在，且被同时支持时，max-age会覆盖Expires。

●清除缓存

虽然我们知晓了如何设置缓存，以达到节省网络带宽的目的，但是缓存一旦设定，当服务器端意外更新内容时，却无法通知客户端更新。这使得我们在使用缓存时也要为其设定版本号，所幸浏览器是根据URL进行缓存，那么一旦内容有所更新时，我们就让浏览器发起新的URL请求，使得新内容能够被客户端更新。一般的更新机制有如下两种。
- 每次发布，路径中跟随Web应用的版本号：http://url.com/?v=20130501。
- 每次发布，路径中跟随该文件内容的hash值：http://url.com/?hash=afadfadwe。大体来说，根据文件内容的hash值进行缓存淘汰会更加高效，因为文件内容不一定随着Web应用的版本而更新，而内容没有更新时，版本号的改动导致的更新毫无意义，因此以文件内容形成的hash值更精准。

### 8.1.7 Basic认证

Basic认证是当客户端与服务器端进行请求时，允许通过用户名和密码实现的一种身份认证方式。这里简要介绍它的原理和它在服务器端通过Node处理的流程。如果一个页面需要Basic认证，它会检查请求报文头中的Authorization字段的内容，该字段的值由认证方式和加密值构成，如下所示：

在Basic认证中，它会将用户和密码部分组合：username + ":" + password。然后进行Base64编码，如下所示：

如果用户首次访问该网页，URL地址中也没携带认证内容，那么浏览器会响应一个401未授权的状态码，如下所示：

在上面的代码中，响应头中的WWW-Authenticate字段告知浏览器采用什么样的认证和加密方式。一般而言，未认证的情况下，浏览器会弹出对话框进行交互式提交认证信息，如图8-2所示。

图8-2 浏览器弹出的交互式提交认证信息的对话框当认证通过，服务器端响应200状态码之后，浏览器会保存用户名和密码口令，在后续的请求中都携带上Authorization信息。

Basic认证有太多的缺点，它虽然经过Base64加密后在网络中传送，但是这近乎于明文，十分危险，一般只有在HTTPS的情况下才会使用。不过Basic认证的支持范围十分广泛，几乎所有的浏览器都支持它。为了改进Basic认证，RFC 2069规范提出了摘要访问认证，它加入了服务器端随机数来保护认证过程，在此不做深入的解释。

## 8.2 数据上传

上述的内容基本都集中在HTTP请求报文头中，适用于GET请求和大多数其他请求。头部报文中的内容已经能够让服务器端进行大多数业务逻辑操作了，但是单纯的头部报文无法携带大量的数据，在业务中，我们往往需要接收一些数据，比如表单提交、文件提交、JSON上传、XML上传等。Node的http模块只对HTTP报文的头部进行了解析，然后触发request事件。如果请求中还带有内容部分（如POST请求，它具有报头和内容），内容部分需要用户自行接收和解析。通过报头的Transfer-Encoding或Content-Length即可判断请求中是否带有内容，如下所示：

在HTTP_Parser解析报头结束后，报文内容部分会通过data事件触发，我们只需以流的方式处理即可，如下所示：

将接收到的Buffer列表转化为一个Buffer对象后，再转换为没有乱码的字符串，暂时挂置在req.rawBody处。

### 8.2.1 表单数据

最为常见的数据提交就是通过网页表单提交数据到服务器端，如下所示：

默认的表单提交，请求头中的Content-Type字段值为application/x-www-form-urlencoded，如下所示：

由于它的报文体内容跟查询字符串相同：

因此解析它十分容易：

后续业务中直接访问req.body就可以得到表单中提交的数据。

### 8.2.2 其他格式

除了表单数据外，常见的提交还有JSON和XML文件等，判断和解析他们的原理都比较相似，都是依据Content-Type中的值决定，其中JSON类型的值为application/json, XML的值为application/xml。

需要注意的是，在Content-Type中可能还附带如下所示的编码信息：

所以在做判断时，需要注意区分，如下所示：

1. JSON文件如果从客户端提交JSON内容，这对于Node来说，要处理它都不需要额外的任何库，如下所示：
2. XML文件解析XML文件稍微复杂一点，但是社区有支持XML文件到JSON对象转换的库，这里以xml2js模块为例，如下所示：

采用类似的方式，无论客户端提交的数据是什么格式，我们都可以通过这种方式来判断该数据是何种类型，然后采用对应的解析方法解析即可。

### 8.2.3 附件上传

除了常见的表单和特殊格式的内容提交外，还有一种比较独特的表单。通常的表单，其内容可以通过urlencoded的方式编码内容形成报文体，再发送给服务器端，但是业务场景往往需要用户直接提交文件。在前端HTML代码中，特殊表单与普通表单的差异在于该表单中可以含有file类型的控件，以及需要指定表单属性enctype为multipart/form-data，如下所示：

浏览器在遇到multipart/form-data表单提交时，构造的请求报文与普通表单完全不同。首先它的报头中最为特殊的如下所示：

它代表本次提交的内容是由多部分构成的，其中boundary=AaB03x指定的是每部分内容的分界符，AaB03x是随机生成的一段字符串，报文体的内容将通过在它前面添加--进行分割，报文结束时在它前后都加上--表示结束。另外，Content-Length的值必须确保是报文体的长度。假设上面的表单选择了一个名为diveintonode.js的文件，并进行提交上传，那么生成的报文如下所示：

普通的表单控件的报文体如下所示：

文件控件形成的报文如下所示：

一旦我们知晓报文是如何构成的，那么解析它就变得十分容易。值得注意的一点是，由于是文件上传，那么像普通表单、JSON或XML那样先接收内容再解析的方式将变得不可接受。接收大小未知的数据量时，我们需要十分谨慎，如下所示：

这里我们将req这个流对象直接交给对应的解析方法，由解析方法自行处理上传的内容，或接收内容并保存在内存中，或流式处理掉。这里要介绍到的模块是formidable。它基于流式处理解析报文，将接收到的文件写入到系统的临时文件夹中，并返回对应的路径，如下所示：

因此在业务逻辑中只要检查req.body和req.files中的内容即可。

### 8.2.4 数据上传与安全

Node提供了相对底层的API，通过它构建各种各样的Web应用都是相对容易的，但是在Web应用中，不得不重视与数据上传相关的安全问题。由于Node与前端JavaScript的近缘性，前端JavaScript甚至可以上传到服务器直接执行，但在这里我们并不讨论这样危险的动作，而是介绍内存和CSRF相关的安全问题。

1. 内存限制

在解析表单、JSON和XML部分，我们采取的策略是先保存用户提交的所有数据，然后再解析处理，最后才传递给业务逻辑。这种策略存在潜在的问题是，它仅仅适合数据量小的提交请求，一旦数据量过大，将发生内存被占光的情况。攻击者通过客户端能够十分容易地模拟伪造大量数据，如果攻击者每次提交1 MB的内容，那么只要并发请求数量一大，内存就会很快地被吃光。要解决这个问题主要有两个方案。
- 限制上传内容的大小，一旦超过限制，停止接收数据，并响应400状态码。
- 通过流式解析，将数据流导向到磁盘中，Node只保留文件路径等小数据。流式处理在上文的文件上传中已经有所体现，这里介绍一下Connect中采用的上传数据量的限制方式，如下所示：

从上面的代码中我们可以看到，数据是由包含Content-Length的请求报文判断是否长度超过限制的，超过则直接响应413状态码。对于没有Content-Length的请求报文，略微简略一点，在每个data事件中判定即可。一旦超过限制值，服务器停止接收新的数据片段。如果是JSON文件或XML文件，极有可能无法完成解析。对于上线的Web应用，添加一个上传大小限制十分有利于保护服务器，在遭遇攻击时，能镇定从容应对。

2. CSRFCSRF的全称是Cross-Site Request Forgery，中文意思为跨站请求伪造。前文提及了服务器端与客户端通过Cookie来标识和认证用户，通常而言，用户通过浏览器访问服务器端的Session ID是无法被第三方知道的，但是CSRF的攻击者并不需要知道Session ID就能让用户中招。为了详细解释CSRF攻击是怎样一个过程，这里以一个留言的例子来说明。假设某个网站有这样一个留言程序，提交留言的接口如下所示：

用户通过POST提交content字段就能成功留言。服务器端会自动从Session数据中判断是谁提交的数据，补足username和updatedAt两个字段后向数据库中写入数据，如下所示：

正常的情况下，谁提交的留言，就会在列表中显示谁的信息。如果某个攻击者发现了这里的接口存在CSRF漏洞，那么他就可以在另一个网站（http://domain_b.com/attack）上构造了一个表单提交，如下所示：

这种情况下，攻击者只要引诱某个domain_a的登录用户访问这个domain_b的网站，就会自动提交一个留言。由于在提交到domain_a的过程中，浏览器会将domain_a的Cookie发送到服务器，尽管这个请求是来自domain_b的，但是服务器并不知情，用户也不知情。以上过程就是一个CSRF攻击的过程。这里的示例仅仅是一个留言的漏洞，如果出现漏洞的是转账的接口，那么其危害程度可想而知。

尽管通过Node接收数据提交十分容易，但是安全问题还是不容忽视。好在CSRF并非不可防御，解决CSRF攻击的方案有添加随机值的方式，如下所示：

也就是说，为每个请求的用户，在Session中赋予一个随机值，如下所示：

在做页面渲染的过程中，将这个_csrf值告之前端，如下所示：

由于该值是一个随机值，攻击者构造出相同的随机值的难度相当大，所以我们只需要在接收端做一次校验就能轻易地识别出该请求是否为伪造的，如下所示：

_csrf字段也可以存在于查询字符串或者请求头中。

## 8.3 路由解析

前文讲述了许多Web请求过程中的预处理过程，对于不同的业务，我们还是期望有不同的处理方式，这带来了路由的选择问题。本节将会介绍文件路径、MVC、RESTful等路由方式。

### 8.3.1 文件路径型

1．静态文件这种方式的路由在路径解析的部分有过简单描述，其让人舒服的地方在于URL的路径与网站目录的路径一致，无须转换，非常直观。这种路由的处理方式也十分简单，将请求路径对应的文件发送给客户端即可。这在前文路径解析部分有介绍，不再重复。
2．动态文件在MVC模式流行起来之前，根据文件路径执行动态脚本也是基本的路由方式，它的处理原理是Web服务器根据URL路径找到对应的文件，如/index.asp或/index.php。Web服务器根据文件名后缀去寻找脚本的解析器，并传入HTTP请求的上下文。以下是Apache中配置PHP支持的方式：

解析器执行脚本，并输出响应报文，达到完成服务的目的。现今大多数的服务器都能很智能地根据后缀同时服务动态和静态文件。这种方式在Node中不太常见，主要原因是文件的后缀都是．js，分不清是后端脚本，还是前端脚本，这可不是什么好的设计。而且Node中Web服务器与应用业务脚本是一体的，无须按这种方式实现。

### 8.3.2 MVC

在MVC流行之前，主流的处理方式都是通过文件路径进行处理的，甚至以为是常态。直到有一天开发者发现用户请求的URL路径原来可以跟具体脚本所在的路径没有任何关系。MVC模型的主要思想是将业务逻辑按职责分离，主要分为以下几种。
- 控制器（Controller），一组行为的集合。
- 模型（Model），数据相关的操作和封装。
- 视图（View），视图的渲染。这是目前最为经典的分层模式（如图8-3所示），大致而言，它的工作模式如下说明。

图8-3 分层模式
- 路由解析，根据URL寻找到对应的控制器和行为。
- 行为调用相关的模型，进行数据操作。
- 数据操作结束后，调用视图和相关数据进行页面渲染，输出到客户端。控制器如何调用模型和如何渲染页面，各种实现都大同小异，我们在后续章节中再展开，此处暂且略过。如何根据URL做路由映射，这里有两个分支实现。一种方式是通过手工关联映射，一种是自然关联映射。前者会有一个对应的路由文件来将URL映射到对应的控制器，后者没有这样的文件。

1．手工映射

手工映射除了需要手工配置路由外较为原始外，它对URL的要求十分灵活，几乎没有格式上的限制。如下的URL格式都能自由映射：

这里假设已经拥有了一个处理设置用户信息的控制器，如下所示：

再添加一个映射的方法就行，为了方便后续的行文，这个方法名叫use()，如下所示：

我们在入口程序中判断URL，然后执行对应的逻辑，于是就完成了基本的路由映射过程，如下所示：

手工映射十分方便，由于它对URL十分灵活，所以我们可以将两个路径都映射到相同的业务逻辑，如下所示：

●正则匹配

对于简单的路径，采用上述的硬匹配方式即可，但是如下的路径请求就完全无法满足需求了：

这些请求需要根据不同的用户显示不同的内容，这里只有两个用户，假如系统中存在成千上万个用户，我们就不太可能去手工维护所有用户的路由请求，因此正则匹配应运而生，我们期望通过以下的方式就可以匹配到任意用户：

于是我们改进我们的匹配方式，在通过use注册路由时需要将路径转换为一个正则表达式，然后通过它来进行匹配，如下所示：

上述正则表达式十分复杂，总体而言，它能实现如下的匹配：

现在我们重新改进注册部分：

以及匹配部分：

现在我们的路由功能就能够实现正则匹配了，无须再为大量的用户进行手工路由映射了。

●参数解析

尽管完成了正则匹配，可以实现相似URL的匹配，但是：username到底匹配了啥，还没有解决。为此我们还需要进一步将匹配到的内容抽取出来，希望在业务中能如下这样调用：

这里的目标是将抽取的内容设置到req.params处。那么第一步就是将键值抽取出来，如下所示：

我们将根据抽取的键值和实际的URL得到键值匹配到的实际值，并设置到req.params处，如下所示：

至此，我们除了从查询字符串（req.query）或提交数据（req.body）中取到值外，还能从路径的映射里取到值。

2．自然映射

手工映射的优点在于路径可以很灵活，但是如果项目较大，路由映射的数量也会很多。从前端路径到具体的控制器文件，需要进行查阅才能定位到实际代码的位置，为此有人提出，尽是路由不如无路由。实际上并非没有路由，而是路由按一种约定的方式自然而然地实现了路由，而无须去维护路由映射。上文的路径解析部分对这种自然映射的实现有稍许介绍，简单而言，它将如下路径进行了划分处理：

以/user/setting/12/1987为例，它会按约定去找controllers目录下的user文件，将其require出来后，调用这个文件模块的setting()方法，而其余的值作为参数直接传递给这个方法。

由于这种自然映射的方式没有指明参数的名称，所以无法采用req.params的方式提取，但是直接通过参数获取更简洁，如下所示：

事实上手工映射也能将值作为参数进行传递，而不是通过req.params。但是这个观点见仁见智，这里不做比较和讨论。自然映射这种路由方式在PHP的MVC框架CodeIgniter中应用十分广泛，设计十分简洁，在Node中实现它也十分容易。与手工映射相比，如果URL变动，它的文件也需要发生变动，手工映射只需要改动路由映射即可。

### 8.3.3 RESTful

MVC模式大行其道了很多年，直到RESTful的流行，大家才意识到URL也可以设计得很规范，请求方法也能作为逻辑分发的单元。REST的全称是Representational State Transfer，中文含义为表现层状态转化。符合REST规范的设计，我们称为RESTful设计。它的设计哲学主要将服务器端提供的内容实体看作一个资源，并表现在URL上。比如一个用户的地址如下所示：

这个地址代表了一个资源，对这个资源的操作，主要体现在HTTP请求方法上，不是体现在URL上。过去我们对用户的增删改查或许是如下这样设计URL的：

操作行为主要体现在行为上，主要使用的请求方法是POST和GET。在RESTful设计中，它是如下这样的：

它将DELETE和PUT请求方法引入设计中，参与资源的操作和更改资源的状态。对于这个资源的具体表现形态，也不再如过去一样表现在URL的文件后缀上。过去设计资源的格式与后缀有很大的关联，例如：

在RESTful设计中，资源的具体格式由请求报头中的Accept字段和服务器端的支持情况来决定。如果客户端同时接受JSON和XML格式的响应，那么它的Accept字段值是如下这样的：

靠谱的服务器端应该要顾及这个字段，然后根据自己能响应的格式做出响应。在响应报文中，通过Content-Type字段告知客户端是什么格式，如下所示：

具体格式，我们称之为具体的表现。所以REST的设计就是，通过URL设计资源、请求方法定义资源的操作，通过Accept决定资源的表现形式。RESTful与MVC设计并不冲突，而且是更好的改进。相比MVC, RESTful只是将HTTP请求方法也加入了路由的过程，以及在URL路径上体现得更资源化。

●请求方法

为了让Node能够支持RESTful需求，我们改进了我们的设计。如果use是对所有请求方法的处理，那么在RESTful的场景下，我们需要区分请求方法设计。示例如下所示：

上面的代码添加了get()、put()、delete()、post()4个方法后，我们希望通过如下的方式完成路由映射：

这样的路由能够识别请求方法，并将业务进行分发。为了让分发部分更简洁，我们先将匹配的部分抽取为match()方法，如下所示：

然后改进我们的分发部分，如下所示：

如此，我们完成了实现RESTful支持的必要条件。这里的实现过程采用了手工映射的方法完成，事实上通过自然映射也能完成RESTful的支持，但是根据Controller/Action的约定必须要转化为Resource/Method的约定，此处已经引出实现思路，不再详述。目前RESTful应用已经开始广泛起来，随着业务逻辑前端化、客户端的多样化，RESTful模式以其轻量的设计，得到广大开发者的青睐。对于多数的应用而言，只需要构建一套RESTful服务接口，就能适应移动端、PC端的各种客户端应用。

## 8.4 中间件

片段式地接触完Web应用的基础功能和路由功能后，我们发现从响应Hello World的示例代码到实际的项目，其实有太多琐碎的细节工作要完成，上述内容只是介绍了主要的部分。对于Web应用而言，我们希望不用接触到这么多细节性的处理，为此我们引入中间件（middleware）来简化和隔离这些基础设施与业务逻辑之间的细节，让开发者能够关注在业务的开发上，以达到提升开发效率的目的。在最早的中间件的定义中，它是一种在操作系统上为应用软件提供服务的计算机软件。它既不是操作系统的一部分，也不是应用软件的一部分，它处于操作系统与应用软件之间，让应用软件更好、更方便地使用底层服务。如今中间件的含义借指了这种封装底层细节，为上层提供更方便服务的意义，并非限定在操作系统层面。这里要提到的中间件，就是为我们封装上文提及的所有HTTP请求细节处理的中间件，开发者可以脱离这部分细节，专注在业务上。中间件的行为比较类似Java中过滤器（filter）的工作原理，就是在进入具体的业务处理之前，先让过滤器处理。它的工作模型如图8-4所示。

图8-4 中间件的工作模型

如同图8-4所示，从HTTP请求到具体业务逻辑之间，其实有很多的细节要处理。Node的http模块提供了应用层协议网络的封装，对具体业务并没有支持，在业务逻辑之下，必须有开发框架对业务提供支持。这里我们通过中间件的形式搭建开发框架，这个开发框架用来组织各个中间件。对于Web应用的各种基础功能，我们通过中间件来完成，每个中间件处理掉相对简单的逻辑，最终汇成强大的基础框架。由于中间件就是前述的那些基本功能，所以它的上下文也就是请求对象和响应对象：req和res。有一点区别的是，由于Node异步的原因，我们需要提供一种机制，在当前中间件处理完成后，通知下一个中间件执行。在第4章中其实已经对中间件做了介绍，这里我们还是采用Connect的设计，通过尾触发的方式实现。一个基本的中间件会是如下的形式：

按照预期的设计，我们为具体的业务逻辑添加中间件应该是很轻松的事情，通过框架支持，能够将所有的基础功能支持串联起来，如下所示：

这里的querystring、cookie、session中间件与前文描述的功能大同小异如下所示：

可以看到这里的中间件都是十分简洁的，接下来我们需要组织起这些中间件。这里我们将路由分离开来，将中间件和具体业务逻辑都看成业务处理单元，改进use()方法如下所示：

改进后的use()方法将中间件都存进了stack数组中保存，等待匹配后触发执行。由于结构发生改变，那么我们的匹配部分也需要进行修改，如下所示：

一旦匹配成功，中间件具体如何调动都交给了handle()方法处理，该方法封装后，递归性地执行数组中的中间件，每个中间件执行完成后，按照约定调用传入next()方法以触发下一个中间件执行（或者直接响应），直到最后的业务逻辑。代码如下所示：

这里带来的疑问是，像querystring、cookie、session这样基础的功能中间件是否需要为每个路由都进行设置呢？如果都设置将会演变成如下的路由配置：

为每个路由都配置中间件并不是一个好的设计，既然中间件和业务逻辑是等价的，那么我们是否可以将路由和中间件进行结合？设计是否可以更人性？既能照顾普适的需求，又能照顾特殊的需求？答案是Yes，如下所示：

为了满足更灵活的设计，这里持续改进我们的use()方法以适应参数的变化，如下所示：

除了改进use()方法外，还要持续改进我们的匹配过程，与前面一旦一次匹配后就不再执行后续匹配不同，还会继续后续逻辑，这里我们将所有匹配到中间件的都暂时保存起来，如下所示：

改进完use()方法后，还要持续改进分发的过程：

综上所述，通过中间件和路由的协作，我们不知不觉之间已经将复杂的事情简化下来，Web应用开发者可以只关注业务开发就能胜任整个开发工作。

### 8.4.1 异常处理

但是等等，如果某个中间件出现错误该怎么办？我们需要为自己构建的Web应用的稳定性和健壮性负责。于是我们为next()方法添加err参数，并捕获中间件直接抛出的同步异常，如下所示：

由于异步方法的异常不能直接捕获（在第4章中有过阐述），中间件异步产生的异常需要自己传递出来，如下所示：

Next()方法接到异常对象后，会将其交给handle500()进行处理。为了将中间件的思想延续下去，我们认为进行异常处理的中间件也是能进行数组式处理的。由于要同时传递异常，所以用于处理异常的中间件的设计与普通中间件略有差别，它的参数有4个，如下所示：

我们通过use()可以将所有异常处理的中间件注册起来，如下所示：

为了区分普通中间件和异常处理中间件，handle500()方法将会对中间件按参数进行选取，然后递归执行。

### 8.4.2 中间件与性能

前文我们添加了强大的中间件组织能力，如果注意到一个现象的话，那就是我们的业务逻辑往往是在最后才执行。为了让业务逻辑提早执行，尽早响应给终端用户，中间件的编写和使用是需要一番考究的。下面是两个主要的能提升的点。
- 编写高效的中间件。
- 合理利用路由，避免不必要的中间件执行。1．编写高效的中间件编写高效的中间件其实就是提升单个处理单元的处理速度，以尽早调用next()执行后续逻辑。需要知道的事情是，一旦中间件被匹配，那么每个请求都会使该中间件执行一次，哪怕它只浪费1毫秒的执行时间，都会让我们的QPS显著下降。常见的优化方法有几种。
- 使用高效的方法。必要时通过jsperf.com测试基准性能。
- 缓存需要重复计算的结果（需要控制缓存用量，原因在第5章阐述过）。
- 避免不必要的计算。比如HTTP报文体的解析，对于GET方法完全不需要。2．合理使用路由

在拥有一堆高效的中间件后，并不意味着每个中间件我们都使用，合理的路由使得不必要的中间件不参与请求处理的过程。这里以一个示例来说明该问题。假设我们这里有一个静态文件的中间件，它会对请求进行判断，如果磁盘上存在对应文件，就响应对应的静态文件，否则就交由下游中间件处理，如下所示：

如果我们以如下的方式注册路由：

那么意味着对/路径下的所有URL请求都会进行判断。又由于它中间涉及到了磁盘I/O，如果成功匹配，它的效率还行，但是如果不成功匹配，每次的磁盘I/O都是对性能的浪费，使QPS直线下降。对于这种情况，我们需要做的是提升匹配成功率，那么就不能使用默认的/路径来进行匹配了，因为它的误伤率太高。给它添加一个更好的路由路径是个不错的选择，如下所示：

这样只有/public路径会匹配上，其余路径根本不会涉及该中间件。

### 8.4.3 小结

中间件使得前文的基础功能，从凌乱的发散状态收敛成很规整的组织方式。对于单个中间件而言，它足够简单，职责单一。与像面条一样杂糅在一起的逻辑判断相比，它具备更好的可测试性。中间件机制使得Web应用具备良好的可扩展性和可组合性，可以轻易地进行数据增删。从某种角度来讲它就是Unix哲学的一个实现，专注简单，小而美，然后通过组合使用，发挥出强大的能量。中间件是Connect的经典模式，通过本节的叙述，我们已经可以看到整个Connect是如何搭建轮廓的。本节试图解释Web开发过程的前置思路，省略了许多细节，尽管与实际的Connect代码不尽相同，希望借着这些思路，每位开发者都能独立写出适应自己业务需求的框架。

## 8.5 页面渲染


## 8.6 总结


## 8.7 参考资源

本章参考的资源如下：
- http://tools.ietf.org/html/rfc3875 
- http://tools.ietf.org/html/rfc2069 
- http://www.ietf.org/rfc/rfc1867.txt 
- http://en.wikipedia.org/wiki/Cross-site_request_forgery 
- https://github.com/senchalabs/connect/blob/master/lib/middleware/csrf.js 
- http://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller 
- http://www.ibm.com/developerworks/webservices/library/ws-restful/ 
- http://en.wikipedia.org/wiki/Middleware 
- http://mustache.github.io/ 
- https://github.com/joyent/node/wiki/modules#wiki-templating 
- https://developer.mozilla.org/zh-CN/docs/JavaScript/Reference/Global_Objects/Function

# 第 9 章 玩转进程


## 9.1 服务模型的变迁


## 9.2 多进程架构


## 9.3 集群稳定之路


## 9.4 Cluster 模块


## 9.5 总结


## 9.6 参考资源

本章参考的资源如下：

- http://nodejs.org/docs/latest/api/child_process.html
- http://nodejs.org/docs/latest/api/cluster.html
- https://github.com/aleafs/pmProcess
- http://en.wikipedia.org/wiki/Inter-process_communication
- http://en.wikipedia.org/wiki/Pipeline_(Unix)
- http://www.w3.org/TR/workers/
- http://man7.org/linux/man-pages/man7/unix.7.html

# 第 10 章 测试


## 10.1 单元测试


## 10.2 性能测试


## 10.3 总结


## 10.4 参考资源

本章参考的资源如下：

- http://nodejs.org/docs/latest/api/assert.html
- http://visionmedia.github.com/mocha/
- https://github.com/visionmedia/should.js
- https://github.com/fent/node-muk
- https://github.com/alex-seville/blanket
- http://about.travis-ci.org/docs/
- https://github.com/JacksonTian/unittesting
- https://speakerdeck.com/felixge/faster-than-c-3

# 第 11 章 产品化


## 11.1 项目工程化


## 11.2 部署流程


## 11.3 性能


## 11.4 日志


## 11.5 监控报警


## 11.6 稳定性


## 11.7 异构共存


## 11.8 总结


## 11.9 参考资源


# 附录 A 安装 Node


## A.1 Windows 系统下的 Node 安装


## A.2 Mac 系统下 Node 的安装


## A.3 Linux 系统下 Node 的安装


## A.4 总结


## A.5 参考资源


# 附录 B 调试 Node


## B.1 Debugger


## B.2 Node Inspector


## B.3 总结


# 附录 C Node 编码规范

## C.1 根源


## C.2 编码规范


## C.3 最佳实践


## C.4 总结


## C.5 参考资源

本章参考的资源如下：

- http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
- http://caolanmcmahon.com/posts/nodejs_style_and_structure/
- http://nodeguide.com/style.htmlFelix’sNode.js
- https://npmjs.org/doc/coding-style.htmlNPM

# 附录 D 搭建局域 NPM 仓库


## D.1 NPM 仓库的安装


## D.2 高阶应用


## D.3 总结


## D.4 参考资源

- https://www.irisnpm.com/
- http://www.erlang.org/doc/installation_guide/INSTALL.html
- http://wiki.apache.org/couchdb/Installation
- https://github.com/isaacs/npmjs.org
- https://github.com/isaacs/npm-www
- https://developer.mozilla.org/en-US/docs/SpiderMonkey/Build_Documentation
- https://github.com/mikeal/replicate
- https://github.com/TBEDP/sync_package
