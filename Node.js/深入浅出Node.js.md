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
console.log("发送Ajax结束");
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

在 CommonJS 规范中，存在 `require()`方法，这个方法接受模块标识，以此引入一个模块的 API 到当前上下文中。

2. 模块定义在模块中，上下文提供 `require()`方法来引入外部模块。对应引入的功能，上下文提供了 exports 对象用于导出当前模块的方法或者变量，并且它是唯一导出的出口。在模块中，还存在一个 module 对象，它代表模块自身，而 exports 是 module 的属性。在 Node 中，一个文件就是一个模块，将方法挂载在 exports 对象上作为属性即可定义导出的方式：

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

3. 模块标识模块标识其实就是传递给 `require()`方法的参数，它必须是符合小驼峰命名的字符串，或者以`.`、`..`开头的相对路径，或者绝对路径。它可以没有文件名后缀`.js`。

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

## 2.2.1 优先从缓存加载

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

其中，`Module._extensions` 会被赋值给 `require()`的 extensions 属性，所以通过在代码中访问 require.extensions 可以知道系统中已有的扩展加载方式。编写如下代码测试一下：

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

回到 CommonJS 模块规范，我们知道每个模块文件中存在着 require、exports、module 这 3 个变量，但是它们在模块文件中并没有定义，那么从何而来呢？甚至在 Node 的 API 文档中，我们知道每个模块中还有 filename、dirname 这两个变量的存在，它们又是从何而来的呢？如果我们把直接定义模块的过程放诸在浏览器端，会存在污染全局变量的情况。

事实上，在编译的过程中，Node 对获取的 JavaScript 文件内容进行了头尾包装。在头部添加了`(function (exports, require, module,filename, dirname) {\n，在尾部添加了\n});`。一个正常的 JavaScript 文件会被包装成如下的样子：

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

至此，require、exports、module 的流程已经完整，这就是 Node 对 CommonJS 模块规范的实现。此外，许多初学者都曾经纠结过为何存在 exports 的情况下，还存在 `module.exports`。理想情况下，只要赋值给 exports 即可：

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

2. C/C++模块的编译 Node 调用 `process.dlopen()`方法进行加载和执行。在 Node 的架构下，`dlopen()`方法在 Windows 和\*nix 平台下分别有不同的实现，通过 libuv 兼容层进行了封装。

实际上，`.node` 的模块文件并不需要编译，因为它是编写 C/C++模块之后编译生成的，所以这里只有加载和执行的过程。在执行的过程中，模块的 exports 对象与`.node` 模块产生联系，然后返回给调用者。

C/C++模块给 Node 使用者带来的优势主要是执行效率方面的，劣势则是 C/C++模块的编写门槛比 JavaScript 高。

3. JSON 文件的编译

.json 文件的编译是 3 种编译方式中最简单的。Node 利用 fs 模块同步读取 JSON 文件的内容之后，调用 `JSON.parse()`方法得到对象，然后将它赋给模块对象的 exports，以供外部调用。

JSON 文件在用作项目的配置文件时比较有用。如果你定义了一个 JSON 文件作为配置，那就不必调用 fs 模块去异步读取和解析，直接调用 `require()`引入即可。此外，你还可以享受到模块缓存的便利，并且二次引入时也没有性能影响。

这里我们提到的模块编译都是指文件模块，即用户自己编写的模块。在下一节中，我们将展开介绍核心模块中的 JavaScript 模块和 C/C++模块。

## 2.3 核心模块

前面提到，Node 的核心模块在编译成可执行文件的过程中被编译进了二进制文件。核心模块其实分为 C/C++编写的和 JavaScript 编写的两部分，其中 C/C++文件存放在 Node 项目的 src 目录下，JavaScript 文件存放在 lib 目录下。

### 2.3.1 JavaScript 核心模块的编译过程

在编译所有 C/C++文件之前，编译程序需要将所有的 JavaScript 模块文件编译为 C/C++代码，此时是否直接将其编译为可执行代码了呢？其实不是。

1.转存为 C/C++代码 Node 采用了 V8 附带的 js2c.py 工具，将所有内置的 JavaScript 代码（src/node.js 和 lib/\*.js）转换成 C++里的数组，生成 node_natives.h 头文件，相关代码如下：

```c#
namespace node {
const char node_native[] = { 47, 47, ..}; const char dgram_native[] = { 47, 47, ..}; const char console_native[] = { 47, 47, ..}; const char buffer_native[] = { 47, 47, ..}; const char querystring_native[] = { 47, 47, ..}; const char punycode_native[] = { 47, 42, ..}; ... struct _native {
 const char* name;  const char* source;  size_t source_len;
};
static const struct _native natives[] = {  { "node", node_native, sizeof(node_native)-1 },  { "dgram", dgram_native, sizeof(dgram_native)-1 },  ...
};
}
```

在这个过程中，JavaScript 代码以字符串的形式存储在 node 命名空间中，是不可直接执行的。在启动 Node 进程时，JavaScript 代码直接加载进内存中。在加载的过程中，JavaScript 核心模块经历标识符分析后直接定位到内存中，比普通的文件模块从磁盘中一处一处查找要快很多。

2. 编译 JavaScript 核心模块

lib 目录下的所有模块文件也没有定义 require、module、exports 这些变量。在引入 JavaScript 核心模块的过程中，也经历了头尾包装的过程，然后才执行和导出了 exports 对象。与文件模块有区别的地方在于：获取源代码的方式（核心模块是从内存中加载的）以及缓存执行结果的位置。

JavaScript 核心模块的定义如下面的代码所示，源文件通过 `process.binding('natives')`取出，编译成功的模块缓存到 NativeModule.\_cache 对象上，文件模块则缓存到 Module.\_cache 对象上：

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

1. 内建模块的组织形式在 Node 中，内建模块的内部结构定义如下：

```js
struct node_module_struct {
int version;
void *dso_handle;
const char *filename;
void (*register_func) (v8::Handle<v8::Object> target);
const char *modname; };
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
static Handle<Value> Binding(const Arguments& args) { HandleScope scope;
Local<String> module = args[0]->ToString(); String::Utf8Value module*v(module); node_module_struct* modp;
if (binding*cache.IsEmpty()) {
binding_cache = Persistent<Object>::New(Object::New()); }
Local<Object> exports;
if (binding_cache->Has(module)) { exports = binding_cache->Get(module)->ToObject(); return scope.Close(exports);
}
// Append a string to process.moduleLoadList char buf[1024]; snprintf(buf, 1024, "Binding %s", *module*v); uint32_t l = module_load_list->Length(); module_load_list->Set(l, String::New(buf));
if ((modp = get_builtin_module(*module*v)) != NULL) { exports = Object::New(); modp->register_func(exports); binding_cache->Set(module, exports);
} else if (!strcmp(\_module_v, "constants")) { exports = Object::New(); DefineConstants(exports); binding_cache->Set(module, exports);
#ifdef **POSIX**
} else if (!strcmp(\_module_v, "io_watcher")) { exports = Object::New(); IOWatcher::Initialize(exports); binding_cache->Set(module, exports);
#endif
} else if (!strcmp(\_module_v, "natives")) { exports = Object::New(); DefineJavaScript(exports); binding_cache->Set(module, exports);
} else {
return ThrowException(Exception::Error(String::New("No such module"))); }
return scope.Close(exports); }
```

在加载内建模块时，我们先创建一个 exports 空对象，然后调用 `get_builtin_module()`方法取出内建模块对象，通过执行 `register_func()`填充 exports 对象，最后将 exports 对象按模块名缓存，并返回给调用方完成导出。

这个方法不仅可以导出内建方法，还能导出一些别的内容。前面提到的 JavaScript 核心文件被转换为 C/C++数组存储后，便是通过 `process.binding('natives')`取出放置在 NativeModule.\_source 中的：

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

下面我们以 C/C++模块为例演示如何编写内建模块。为了便于理解，我们先编写一个极其简单的 JavaScript 版本的原型，这个方法返回一个 Helloworld！字符串：

```js
exports.sayHello = function () {
  return "Hello world!";
};
```

编写内建模块通常分两步完成：编写头文件和编写 C/C++文件。

(1) 将以下代码保存为 node_hello.h，存放到 Node 的 src 目录下：

```js
#ifndef NODE_HELLO_H* #define NODE*HELLO_H* #include <v8.h>
namespace node { // 定义方法 v8::Handle<v8::Value> SayHello(const v8::Arguments& args);
} #endif
```

(2) 编写 node_hello.cc，并存储到 src 目录下：

```js
#include <node.h> #include <node_hello.h> #include <v8.h>
namespace node {
using namespace v8; //实现定义的方法 Handle<Value> SayHello(const Arguments& args) {
HandleScope scope; return scope.Close(String::New("Hello world!")); }
//给传入的目对象加 sayHello 方法 void Init_Hello(Handle<Object> target) { target->Set(String::NewSymbol("sayHello"), FunctionTemplate::New(SayHello)->GetFunction()); }
} //调用 NODE_MODULE()将注方法定义内存中 NODE_MODULE(node_hello, node::Init_Hello)
```

以上两步完成了内建模块的编写，但是真正要让 Node 认为它是内建模块，还需要更改 src/node_extensions.h，在 NODE_EXT_LIST_END 前添加 `NODE_EXT_LIST_ITEM(node_hello)`，以将 node_hello 模块添加进 node_module_list 数组中。

其次，还需要让编写的两份代码编译进执行文件，同时需要更改 Node 的项目生成文件 node.gyp，并在’target_name': 'node’节点的 sources 中添加上新编写的两个文件。然后编译整个 Node 项目，具体的编译步骤请参见附录 A。

编译和安装后，直接在命令行中运行以下代码，将会得到期望的效果：

```shell
$ node > var hello = process.binding('hello'); undefined > hello.sayHello(); 'Hello world!' >
```

至此，原生编写过程中需要注意的细节都已表述过了。可以看出，简单的模块通过 JavaScript 来编写可以大大提高生产效率。这里我们写作本节的目的是希望有能力的读者可以深入 Node 的核心模块，去学习它或者改进它。

## 2.4 C/C++扩展模块

对于前端工程师来说，C/C++扩展模块或许比较生疏和晦涩，但是如果你了解了它，在模块出现性能瓶颈时将会对你有极大的帮助。JavaScript 的一个典型弱点就是位运算。JavaScript 的位运算参照 Java 的位运算实现，但是 Java 位运算是在 int 型数字的基础上进行的，而 JavaScript 中只有 double 型的数据类型，在进行位运算的过程中，需要将 double 型转换为 int 型，然后再进行。所以，在 JavaScript 层面上做位运算的效率不高。在应用中，会频繁出现位运算的需求，包括转码、编码等过程，如果通过 JavaScript 来实现，CPU 资源将会耗费很多，这时编写 C/C++扩展模块来提升性能的机会来了。C/C++扩展模块属于文件模块中的一类。前面讲述文件模块的编译部分时提到，C/C++模块通过预先编译为．node 文件，然后调用 process.dlopen()方法加载执行。在这一节中，我们将分析整个 C/C++扩展模块的编写、编译、加载、导出的过程。

在开始编写扩展模块之前，需要强调的一点是，Node 的原生模块一定程度上是可以跨平台的，其前提条件是源代码可以支持在*nix 和 Windows 上编译，其中*nix 下通过 g++/gcc 等编译器编译为动态链接共享对象文件（.so），在 Windows 下则需要通过 Visual C++的编译器编译为动态链接库文件（.dll），如图 2-6 所示。这里有一个让人迷惑的地方，那就是引用加载时却是．node 文件。其实．node 的扩展名只是为了看起来更自然一点，不会因为平台差异产生不同的感觉。实际上，在 Windows 下它是一个．dll 文件，在\*nix 下则是一个．so 文件。为了实现跨平台，dlopen()方法在内部实现时区分了平台，分别用的是加载．so 和．dll 的方式。图 2-6 为扩展模块在不同平台上编译和加载的详细过程。

图 2-6 扩展模块不同平台上的编译和加载过程值得注意的是，一个平台下的．node 文件在另一个平台下是无法加载执行的，必须重新用各自平台下的编译器编译为正确的．node 文件。

### 2.4.1 前提条件

如果想要编写高质量的 C/C++扩展模块，还需要深厚的 C/C++编程功底才行。除此之外，以下这些条目都是不能避开的，在了解它们之后，可以让你在编写过程中事半功倍。

- GYP 项目生成工具。在 Node 0.6 中，第三方模块通过它自身提供的 node_waf 工具实现编译，但是它是\*nix 平台下的产物，无法实现跨平台编译。在 Node 0.8 中，Node 决定摒弃掉 node_waf 而采用跨平台效果更好的项目生成器，它就是 GYP 工具，即“Generate YourProjects”短句的缩写。它的好处在于，可以帮助你生成各个平台下的项目文件，比如 Windows 下的 Visual Studio 解决方案文件（.sln）、Mac 下的 XCode 项目配置文件以及 Scons 工具。在这个基础上，再动用各自平台下的编译器编译项目。这大大减少了跨平台模块在项目组织上的精力投入。Node 源码中一度出现过各种项目文件，后来均统一为 GYP 工具。这除了可以减少编写跨平台项目文件的工作量外，另一个简单的原因就是 Node 自身的源码就是通过 GYP 编译的。为此，NathanRajlich 基于 GYP 为 Node 提供了一个专有的扩展构建工具 node-gyp，这个工具通过 npm install -gnode-gyp 这个命令即可安装。
- V8 引擎 C++库。V8 是 Node 自身的动力来源之一。它自身由 C++写成，可以实现 JavaScript 与 C++的互相调用。
- libuv 库。它是 Node 自身的动力来源之二。Node 能够实现跨平台的一个诀窍就是它的 libuv 库，这个库是跨平台的一层封装，通过它去调用一些底层操作，比自己在各个平台下编写实现要高效得多。libuv 封装的功能包括事件循环、文件操作等。
- Node 内部库。写 C++模块时，免不了要做一些面向对象的编程工作，而 Node 自身提供了一些 C++代码，比如 node::ObjectWrap 类可以用来包装你的自定义类，它可以帮助实现对象回收等工作。
- 其他库。其他存在 deps 目录下的库在编写扩展模块时也许可以帮助你，比如 zlib、openssl、http_parser 等。

### 2.4.2 C/C++扩展模块的编写

在介绍 C/C++内建模块时，其实已经介绍了 C/C++模块的编写方式。普通的扩展模块与内建模块的区别在于无须将源代码编译进 Node，而是通过 dlopen()方法动态加载。所以在编写普通的扩展模块时，无须将源代码写进 node 命名空间，也不需要提供头文件。下面我们将采用同一个例子来介绍 C/C++扩展模块的编写。

它的 JavaScript 原型代码与前面的例子一样：

```js
exports.sayHello = function () {
  return "Hello world!";
};
```

新建 hello 目录作为自己的项目位置，编写 hello.cc 并将其存储到 src 目录下，相关代码如下：

```c#
#include <node.h> #include <v8.h>
using namespace v8; //实现定义的方法 Handle<Value> SayHello(const Arguments& args) {
HandleScope scope; return scope.Close(String::New("Hello world!")); }
//给传入的目对象加 sayHello()方法 void Init_Hello(Handle<Object> target) {
target->Set(String::NewSymbol("sayHello"), FunctionTemplate::New(SayHello)->GetFunction()); } //调用 NODE_MODULE()方法将注方法定义内存中 NODE_MODULE(hello, Init_Hello)
```

C/C++扩展模块与内建模块的套路一样，将方法挂载在 target 对象上，然后通过 NODE_MODULE 声明即可。由于不像编写内建模块那样将对象声明到 node_module_list 链表中，所以无法被认作是一个原生模块，只能通过 dlopen()来动态加载，然后导出给 JavaScript 调用。

### 2.4.3 C/C++扩展模块的编译

在 GYP 工具的帮助下，C/C++扩展模块的编译是一件省心的事情，无须为每个平台编写不同的项目编译文件。写好．gyp 项目文件是除编码外的头等大事，然而你也无须担心此事太难，因为．gyp 项目文件是足够简单的。node-gyp 约定．gyp 文件为 binding.gyp，其内容如下所示：

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

node-gyp configure 这个命令会在当前目录中创建 build 目录，并生成系统相关的项目文件。在\*nix 平台下，build 目录中会出现 Makefile 等文件；在 Windows 下，则会生成 vcxproj 等文件。继续执行如下代码：

会得到如下的输出结果：

编译过程会根据平台不同，分别通过 make 或 vcbuild 进行编译。编译完成后，hello.node 文件会生成在 build/Release 目录下。

### 2.4.4 C/C++扩展模块的加载

得到 hello.node 结果文件后，如何调用扩展模块其实在前面已经提及。`require()`方法通过解析标识符、路径分析、文件定位，然后加载执行即可。下面的代码引入前面编译得到的．node 文件，并调用执行其中的方法：

以上代码存为 hello.js，调用 node hello.js 命令即可得到如下的输出结果：

对于以．node 为扩展名的文件，Node 将会调用 process.dlopen()方法去加载文件：

对于调用者而言，`require()`是轻松愉快的。对于扩展模块的编写者来说，process.dlopen()中隐含的过程值得了解一番。如图 2-7 所示，`require()`在引入．node 文件的过程中，实际上经历了 4 个层面上的调用。

图 2-7 `require()`引入．node 文件的过程加载．node 文件实际上经历了两个步骤，第一个步骤是调用 uv_dlopen()方法去打开动态链接库，第二个步骤是调用 uv_dlsym()方法找到动态链接库中通过 NODE_MODULE 宏定义的方法地址。这两个过程都是通过 libuv 库进行封装的：在\*nix 平台下实际上调用的是 dlfcn.h 头文件中定义的 dlopen()和 dlsym()两个方法；在 Windows 平台则是通过 LoadLibraryExW()和 GetProcAddress()这两个方法实现的，它们分别加载．so 和．dll 文件（实际为．node 文件）。这里对 libuv 函数的调用充分表现 Node 利用 libuv 实现跨平台的方式，这样的情景在很多地方还会出现。

由于编写模块时通过 NODE_MODULE 将模块定义为 node_module_struct 结构，所以在获取函数地址之后，将它映射为 node_module_struct 结构几乎是无缝对接的。接下来的过程就是将传入的 exports 对象作为实参运行，将 C++中定义的方法挂载在 exports 对象上，然后调用者就可以轻松调用了。C/C++扩展模块与 JavaScript 模块的区别在于加载之后不需要编译，直接执行之后就可以被外部调用了，其加载速度比 JavaScript 模块略快。使用 C/C++扩展模块的一个好处在于可以更灵活和动态地加载它们，保持 Node 模块自身简单性的同时，给予 Node 无限的可扩展性。关于 node-gyp 工具的更多细节可以参见https://github.com/TooTallNate/node-gyp（作者为Nathan Rajlich, Node 源码的核心贡献者之一）。

## 2.5 模块调用栈

结束文件模块、核心模块、内建模块、C/C++扩展模块等的阐述之后，有必要明确一下各种模块之间的调用关系，如图 2-8 所示。

图 2-8 模块之间的调用关系 C/C++内建模块属于最底层的模块，它属于核心模块，主要提供 API 给 JavaScript 核心模块和第三方 JavaScript 文件模块调用。如果你不是非常了解要调用的 C/C++内建模块，请尽量避免通过 process.binding()方法直接调用，这是不推荐的。JavaScript 核心模块主要扮演的职责有两类：一类是作为 C/C++内建模块的封装层和桥接层，供文件模块调用；一类是纯粹的功能模块，它不需要跟底层打交道，但是又十分重要。文件模块通常由第三方编写，包括普通 JavaScript 模块和 C/C++扩展模块，主要调用方向为普通 JavaScript 模块调用扩展模块。

## 2.6 包与 NPM

Node 组织了自身的核心模块，也使得第三方文件模块可以有序地编写和使用。但是在第三方模块中，模块与模块之间仍然是散列在各地的，相互之间不能直接引用。而在模块之外，包和 NPM 则是将模块联系起来的一种机制。在介绍 NPM 之前，不得不提起 CommonJS 的包规范。JavaScript 不似 Java 或者其他语言那样，具有模块和包结构。Node 对模块规范的实现，一定程度上解决了变量依赖、依赖关系等代码组织性问题。包的出现，则是在模块的基础上进一步组织 JavaScript 代码。图 2-9 为包组织模块示意图。

图 2-9 包组织模块示意图 CommonJS 的包规范的定义其实也十分简单，它由包结构和包描述文件两个部分组成，前者用于组织包中的各种文件，后者则用于描述包的相关信息，以供外部读取分析。

### 2.6.1 包结构

包实际上是一个存档文件，即一个目录直接打包为.zip 或 tar.gz 格式的文件，安装后解压还原为目录。完全符合 CommonJS 规范的包目录应该包含如下这些文件。

- package.json：包描述文件。
- bin：用于存放可执行二进制文件的目录。
- lib：用于存放 JavaScript 代码的目录。
- doc：用于存放文档的目录。
- test：用于存放单元测试用例的代码。可以看到，CommonJS 包规范从文档、测试等方面都做过考虑。当一个包完成后向外公布时，用户看到单元测试和文档的时候，会给他们一种踏实可靠的感觉。

### 2.6.2 包描述文件

与 NPM 包描述文件用于表达非代码相关的信息，它是一个 JSON 格式的文件——package.json，位于包的根目录下，是包的重要组成部分。而 NPM 的所有行为都与包描述文件的字段息息相关。由于 CommonJS 包规范尚处于草案阶段，NPM 在实践中做了一定的取舍，具体细节在后面会介绍到。CommonJS 为 package.json 文件定义了如下一些必需的字段。

- name。包名。规范定义它需要由小写的字母和数字组成，可以包含.、\_和-，但不允许出现空格。包名必须是唯一的，以免对外公布时产生重名冲突的误解。除此之外，NPM 还建议不要在包名中附带上 node 或 js 来重复标识它是 JavaScript 或 Node 模块。
- description。包简介。
- version。版本号。一个语义化的版本号，这在http://semver.org/上有详细定义，通常为major.minor.revision格式。该版本号十分重要，常常用于一些版本控制的场合。
- keywords。关键词数组，NPM 中主要用来做分类搜索。一个好的关键词数组有利于用户快速找到你编写的包。
- maintainers。包维护者列表。每个维护者由 name、email 和 web 这 3 个属性组成。示例如下："maintainers": [{ "name": "JacksonTian", "email": "shyvo1987@gmail.com","web": "http://html5ify.com" }]NPM 通过该属性进行权限认证。
- contributors。贡献者列表。在开源社区中，为开源项目提供代码是经常出现的事情，如果名字能出现在知名项目的 contributors 列表中，是一件比较有荣誉感的事。列表中的第一个贡献应当是包的作者本人。它的格式与维护者列表相同。
- bugs。一个可以反馈 bug 的网页地址或邮件地址。
- licenses。当前包所使用的许可证列表，表示这个包可以在哪些许可证下使用。它的格式如下：

* repositories。托管源代码的位置列表，表明可以通过哪些方式和地址访问包的源代码。
* dependencies。使用当前包所需要依赖的包列表。这个属性十分重要，NPM 会通过这个属性帮助自动加载依赖的包。

除了必选字段外，规范还定义了一部分可选字段，具体如下所示。

- homepage。当前包的网站地址。
- os。操作系统支持列表。这些操作系统的取值包括 aix、freebsd、linux、macos、solaris、vxworks、windows。如果设置了列表为空，则不对操作系统做任何假设。
- cpu。CPU 架构的支持列表，有效的架构名称有 arm、mips、ppc、sparc、x86 和 x86_64。同 os 一样，如果列表为空，则不对 CPU 架构做任何假设。
- engine。支持的 JavaScript 引擎列表，有效的引擎取值包括 ejs、flusspferd、gpsee、jsc、spidermonkey、narwhal、node 和 v8。
- builtin。标志当前包是否是内建在底层系统的标准组件。
- directories。包目录说明。
- implements。实现规范的列表。标志当前包实现了 CommonJS 的哪些规范。
- scripts。脚本说明对象。它主要被包管理器用来安装、编译、测试和卸载包。示例如下：

包规范的定义可以帮助 Node 解决依赖包安装的问题，而 NPM 正是基于该规范进行了实现。最初，NPM 工具是由 Isaac Z. Schlueter 单独创建，提供给 Node 服务的 Node 包管理器，需要单独安装。后来，在 v0.6.3 版本时集成进 Node 中作为默认包管理器，作为软件包的一部分一起安装。之后，Isaac Z. Schlueter 也成为 Node 的掌门人。在包描述文件的规范中，NPM 实际需要的字段主要有 name、version、description、keywords、repositories、author、bin、main、scripts、engines、dependencies、devDependencies。

与包规范的区别在于多了 author、bin、main 和 devDependencies 这 4 个字段，下面补充说明一下。

- author。包作者。
- bin。一些包作者希望包可以作为命令行工具使用。配置好 bin 字段后，通过 npm installpackage_name -g 命令可以将脚本添加到执行路径中，之后可以在命令行中直接执行。前面的 node-gyp 即是这样安装的。通过-g 命令安装的模块包称为全局模式。
- main。模块引入方法 `require()`在引入包时，会优先检查这个字段，并将其作为包中其余模块的入口。如果不存在这个字段，`require()`方法会查找包目录下的 index.js、index.node、index.json 文件作为默认入口。
- devDependencies。一些模块只在开发时需要依赖。配置这个属性，可以提示包的后续开发者安装依赖包。下面是知名框架 express 项目的 package.json 文件，具有一定的参考意义：

### 2.6.3 NPM 常用功能

CommonJS 包规范是理论，NPM 是其中的一种实践。NPM 之于 Node，相当于 gem 之于 Ruby,pear 之于 PHP。对于 Node 而言，NPM 帮助完成了第三方模块的发布、安装和依赖等。借助 NPM,Node 与第三方模块之间形成了很好的一个生态系统。借助 NPM，可以帮助用户快速安装和管理依赖包。除此之外，NPM 还有一些巧妙的用法，下面我们详细介绍一下。

1.查看帮助在安装 Node 之后，执行 npm -v 命令可以查看当前 NPM 的版本：

在不熟悉 NPM 的命令之前，可以直接执行 NPM 查看到帮助引导说明：

可以看到，帮助中列出了所有的命令，其中 npmhelp <command>可以查看具体的命令说明。2.安装依赖包安装依赖包是 NPM 最常见的用法，它的执行语句是 npm install express。执行该命令后，NPM 会在当前目录下创建 node_modules 目录，然后在 node_modules 目录下创建 express 目录，接着将包解压到这个目录下。

安装好依赖包后，直接在代码中调用 require('express')；即可引入该包。`require()`方法在做路径分析的时候会通过模块路径查找到 express 所在的位置。模块引入和包的安装这两个步骤是相辅相承的。● 全局模式安装如果包中含有命令行工具，那么需要执行 npminstall express -g 命令进行全局模式安装。需要注意的是，全局模式并不是将一个模块包安装为一个全局包的意思，它并不意味着可以从任何地方通过 `require()`来引用到它。全局模式这个称谓其实并不精确，存在诸多误导。实际上，-g 是将一个包安装为全局可用的可执行命令。它根据包描述文件中的 bin 字段配置，将实际脚本链接到与 Node 可执行文件相同的路径下：

事实上，通过全局模式安装的所有模块包都被安装进了一个统一的目录下，这个目录可以通过如下方式推算出来：

如果 Node 可执行文件的位置是/usr/local/bin/node，那么模块目录就是/usr/local/lib/node_modules。最后，通过软链接的方式将 bin 字段配置的可执行文件链接到 Node 的可执行目录下。● 从本地安装对于一些没有发布到 NPM 上的包，或是因为网络原因导致无法直接安装的包，可以通过将包下载到本地，然后以本地安装。本地安装只需为 NPM 指明 package.json 文件所在的位置即可：它可以是一个包含 package.json 的存档文件，也可以是一个 URL 地址，也可以是一个目录下有 package.json 文件的目录位置。具体参数如下：

● 从非官方源安装如果不能通过官方源安装，可以通过镜像源安装。在执行命令时，添加--registry=http://registry.url即可，示例如下：

如果使用过程中几乎都采用镜像源安装，可以执行以下命令指定默认源：

3. NPM 钩子命令另一个需要说明的是 C/C++模块实际上是编译后才能使用的。package.json 中 scripts 字段的提出就是让包在安装或者卸载等过程中提供钩子机制，示例如下：

在以上字段中执行 npm install <package>时，preinstall 指向的脚本将会被加载执行，然后 install 指向的脚本会被执行。在执行 npmuninstall <package>时，uninstall 指向的脚本也许会做一些清理工作等。当在一个具体的包目录下执行 npm test 时，将会运行 test 指向的脚本。一个优秀的包应当包含测试用例，并在 package.json 文件中配置好运行测试的命令，方便用户运行测试用例，以便检验包是否稳定可靠。4.发布包为了将整个 NPM 的流程串联起来，这里将演示如何编写一个包，将其发布到 NPM 仓库中，并通过 NPM 安装回本地。● 编写模块模块的内容我们尽量保持简单，这里还是以 sayHello 作为例子，相关代码如下：

将这段代码保存为 hello.js 即可。● 初始化包描述文件 package.json 文件的内容尽管相对较多，但是实际发布一个包时并不需要一行一行编写。NPM 提供的 npm init 命令会帮助你生成 package.json 文件，具体如下所示：

NPM 通过提问式的交互逐个填入选项，最后生成预览的包描述文件。如果你满意，输入 yes，此时会在目录下得到 package.json 文件。● 注册包仓库账号为了维护包，NPM 必须要使用仓库账号才允许将包发布到仓库中。注册账号的命令是 npmadduser。这也是一个提问式的交互过程，按顺序进行即可：

● 上传包上传包的命令是 npm publish <folder>。在刚刚创建的 package.json 文件所在的目录下，执行 npm publish .开始上传包，相关代码如下：

在这个过程中，NPM 会将目录打包为一个存档文件，然后上传到官方源仓库中。● 安装包为了体验和测试自己上传的包，可以换一个目录执行 npm install hello_test_jackson 安装它：

● 管理包权限通常，一个包只有一个人拥有权限进行发布。如果需要多人进行发布，可以使用 npm owner 命令帮助你管理包的所有者：

使用这个命令，也可以添加包的拥有者，删除一个包的拥有者：

5.分析包在使用 NPM 的过程中，或许你不能确认当前目录下能否通过 `require()`顺利引入想要的包，这时可以执行 npm ls 分析包。这个命令可以为你分析出当前路径下能够通过模块路径找到的所有包，并生成依赖树，如下：

### 2.6.4 局域 NPM

在企业的内部应用中使用 NPM 与开源社区中使用有一定的差别。企业的限制在于，一方面需要享受到模块开发带来的低耦合和项目组织上的好处，另一方面却要考虑到模块保密性的问题。所以，通过 NPM 共享和发布存在潜在的风险。为了同时能够享受到 NPM 上众多的包，同时对自己的包进行保密和限制，现有的解决方案就是企业搭建自己的 NPM 仓库。

所幸，NPM 自身是开源的，无论是它的服务器端和客户端。通过源代码搭建自己的仓库并不是什么秘密。局域 NPM 仓库的搭建方法与搭建镜像站（详情可参见附录 D）的方式几乎一样。与镜像仓库不同的地方在于，企业局域 NPM 可以选择不同步官方源仓库中的包。图 2-10 为企业中混合使用官方仓库和局域仓库的示意图。

图 2-10 混合使用官方仓库和局域仓库的示意图对于企业内部而言，私有的可重用模块可以打包到局域 NPM 仓库中，这样可以保持更新的中心化，不至于让各个小项目各自维护相同功能的模块，杜绝通过复制粘贴实现代码共享的行为。

### 2.6.5 NPM 潜在问题

作为为模块和包服务的工具，NPM 十分便捷。它实质上已经是一个包共享平台，所有人都可以贡献模块并将其打包分享到这个平台上，也可以在许可证（大多是 MIT 许可证）的允许下免费使用它们。NPM 提供的这些便捷，将模块链接到一个共享平台上，缩短了贡献者与使用者之间的距离，这十分有利于模块的传播，进而也十分利于 Node 的推广。几乎没有一种语言或平台有 Node 这样出现才 3 年多就拥有成千上万个第三方模块的情景。这个功劳一部分是因为 Node 选择了 JavaScript，这门语言拥有极大的开发人员基数，具有强大的生产力；另一部分则是因为 CommonJS 规范和 NPM，它们使得产品能够更好地组织、传播和使用。潜在的问题在于，在 NPM 平台上，每个人都可以分享包到平台上，鉴于开发人员水平不一，上面的包的质量也良莠不齐。另一个问题则是，Node 代码可以运行在服务器端，需要考虑安全问题。对于包的使用者而言，包质量和安全问题需要作为是否采纳模块的一个判断条件。

尽管 NPM 没有硬性的方式去评判一个包的质量和安全，好在开源社区也有它内在的健康发展机制，那就是口碑效应，其中 NPM 模块首页（https://npmjs.org/）上的依赖榜可以说明模块的质量和可靠性。第二个可以考查质量的地方是GitHub, NPM 中大多的包都是通过 GitHub 托管的，模块项目的观察者数量和分支数量也能从侧面反映这个模块的可靠性和流行度。第三个可以考量包质量的地方在于包中的测试用例和文档的状况，一个没有单元测试的包基本上是无法被信任的，没有文档的包，使用者使用时内心也是不踏实的。在安全问题上，在经过模块质量的考查之后，应该可以去掉一大半候选包。基于使用者大多是 JavaScript 程序员，难点其实存在于第三方 C/C++扩展模块，这类模块建议在企业的安全部门检查之后方可允许使用。事实上，为了解决上述问题，Isaac Z. Schlueter 计划引入 CPAN 社区中的 Kwalitee 风格来让模块进行自然排序。Kwalitee 是一个拟声词，发音与 quality 相同。CPAN 社区对它的原始定义如下：“Kwalitee”is something that looks likequality, sounds like quality, but is not quitequality.

大致意思就是确认一个模块的质量是否优秀并不是那么容易，只能从一些表象来进行考查，但即便考查都通过，也并不能确定它就是高质量的模块。这个方法能够排除大部分不合格的模块，虽然不够精确但是有效。总体而言，符合 Kwalitee 的模块要满足的条件与上述提及的考查点大致相同。

- 具备良好的测试。
- 具备良好的文档（README、API）。
- 具备良好的测试覆盖率。
- 具备良好的编码规范。
- 更多条件。CPAN 社区制定了相当多的规范来考查模块。未来，NPM 社区也会有更多的规范来考查模块。读者可以根据这些条款区分出那些优秀的模块和糟粕的模块。

## 2.7 前后端共用模块

谈论了许多后端模块的具体实现后，现在我们围绕 CommonJS 规范再次回到前端模块上。JavaScript 在 Node 出现之后，比别的编程语言多了一项优势，那就是一些模块可以在前后端实现共用，这是因为很多 API 在各个宿主环境下都提供。但是在实际情况中，前后端的环境是略有差别的。

### 2.7.1 模块的侧重点

前后端 JavaScript 分别搁置在 HTTP 的两端，它们扮演的角色并不同。浏览器端的 JavaScript 需要经历从同一个服务器端分发到多个客户端执行，而服务器端 JavaScript 则是相同的代码需要多次执行。前者的瓶颈在于带宽，后者的瓶颈则在于 CPU 和内存等资源。前者需要通过网络加载代码，后者从磁盘中加载，两者的加载速度不在一个数量级上。纵观 Node 的模块引入过程，几乎全都是同步的。尽管与 Node 强调异步的行为有些相反，但它是合理的。但是如果前端模块也采用同步的方式来引入，那将会在用户体验上造成很大的问题。UI 在初始化过程中需要花费很多时间来等待脚本加载完成。鉴于网络的原因，CommonJS 为后端 JavaScript 制定的规范并不完全适合前端的应用场景。经过一段争执之后，AMD 规范最终在前端应用场景中胜出。它的全称是 Asynchronous ModuleDefinition，即是“异步模块定义”，详见https://github.com/amdjs/amdjs-api/wiki/AMD。除此之外，还有玉伯定义的CMD规范。

### 2.7.2 AMD 规范

AMD 规范是 CommonJS 模块规范的一个延伸，它的模块定义如下：

它的模块 id 和依赖是可选的，与 Node 模块相似的地方在于 factory 的内容就是实际代码的内容。下面的代码定义了一个简单的模块：

不同之处在于 AMD 模块需要用 define 来明确定义一个模块，而在 Node 实现中是隐式包装的，它们的目的是进行作用域隔离，仅在需要的时候被引入，避免掉过去那种通过全局变量或者全局命名空间的方式，以免变量污染和不小心被修改。另一个区别则是内容需要通过返回的方式实现导出。

### 2.7.3 CMD 规范

CMD 规范由国内的玉伯提出，与 AMD 规范的主要区别在于定义模块和依赖引入的部分。AMD 需要在声明模块的时候指定所有的依赖，通过形参传递依赖到模块内容中：

与 AMD 模块规范相比，CMD 模块更接近于 Node 对 CommonJS 规范的定义：

在依赖部分，CMD 支持动态引入，示例如下：

require、exports 和 module 通过形参传递给模块，在需要依赖模块时，随时调用 `require()`引入即可。

### 2.7.4 兼容多种模块

规范为了让同一个模块可以运行在前后端，在写作过程中需要考虑兼容前端也实现了模块规范的环境。为了保持前后端的一致性，类库开发者需要将类库代码包装在一个闭包内。以下代码演示如何将 hello()方法定义到不同的运行环境中，它能够兼容 Node、AMD、CMD 以及常见的浏览器环境中：

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

I/O

# 第 3 章 异步 I/O

在第1章中，我们曾简单介绍过异步I/O。“异步”这个名词其实很早就诞生了，但它的大规模流行却是在Web 2.0浪潮中，它伴随着AJAX的第一个A（Asynchronous）席卷了Web。Node在出现之前，最习惯异步编程的程序员莫过于前端工程师了。前端编程算GUI编程的一种，其中充斥了各种Ajax和事件，这些都是典型的异步应用场景。但事实上，异步早就存在于操作系统的底层。在底层系统中，异步通过信号量、消息等方式有了广泛的应用。意外的是，在绝大多数高级编程语言中，异步并不多见，疑似被屏蔽了一般。造成这个现象的主要原因也许令人惊讶：程序员不太适合通过异步来进行程序设计。PHP这门语言的设计最能体现这个观点。它对调用层不仅屏蔽了异步，甚至连多线程都不提供。PHP语言从头到脚都是以同步阻塞的方式来执行的。它的优点十分明显，利于程序员顺序编写业务逻辑；它的缺点在小规模站点中基本不存在，但是在复杂的网络应用中，阻塞导致它无法更好地并发。而在其他语言中，尽管可能存在异步的API，但是程序员还是习惯采用同步的方式来编写应用。在众多高级编程语言或运行平台中，将异步作为主要编程方式和设计理念的，Node是首个。

伴随着异步I/O的还有事件驱动和单线程，它们构成Node的基调，Ryan Dahl正是基于这几个因素设计了Node。Ryan Dahl最初期望设计出一个高性能的Web服务器，后来则演变为一个可以基于它构建各种高速、可伸缩网络应用的平台，因为一个Web服务器已经无法完全涵盖和代表它的能力了。尽管它不再是一个服务器，但是可以基于它搭建更多更丰富、更强大的网络应用。与Node的事件驱动、异步I/O设计理念比较相近的一个知名产品为Nginx。Nginx采用纯C编写，性能表现非常优异。它们的区别在于，Nginx具备面向客户端管理连接的强大能力，但是它的背后依然受限于各种同步方式的编程语言。但Node却是全方位的，既可以作为服务器端去处理客户端带来的大量并发请求，也能作为客户端向网络中的各个应用进行并发请求。Web的含义是网，Node的表现就如它的名字一样，是网络中灵活的一个节点。

## 3.1 为什么要异步 I/O

关于异步I/O为何在Node里如此重要，这与Node面向网络而设计不无关系。Web应用已经不再是单台服务器就能胜任的时代了，在跨网络的结构下，并发已经是现代编程中的标准配备了。具体到实处，则可以从用户体验和资源分配这两个方面说起。3.1.1 用户体验异步的概念之所以首先在Web 2.0中火起来，是因为在浏览器中JavaScript在单线程上执行，而且它还与UI渲染共用一个线程。这意味着JavaScript在执行的时候UI渲染和响应是处于停滞状态的。《高性能JavaScript》一书中曾经总结过，如果脚本的执行时间超过100毫秒，用户就会感到页面卡顿，以为网页停止响应。而在B/S模型中，网络速度的限制给网页的实时体验造成很大的麻烦。如果网页临时需要获取一个网络资源，通过同步的方式获取，那么JavaScript则需要等待资源完全从服务器端获取后才能继续执行，这期间UI将停顿，不响应用户的交互行为。可以想象，这样的用户体验将会多差。而采用异步请求，在下载资源期间，JavaScript和UI的执行都不会处于等待状态，可以继续响应用户的交互行为，给用户一个鲜活的页面。

同理，前端通过异步可以消除掉UI阻塞的现象，但是前端获取资源的速度也取决于后端的响应速度。假如一个资源来自于两个不同位置的数据的返回，第一个资源需要M 毫秒的耗时，第二个资源需要N 毫秒的耗时。如果采用同步的方式，代码大致如下：[插图]但是如果采用异步方式，第一个资源的获取并不会阻塞第二个资源，也即第二个资源的请求并不依赖第一个资源的结束。如此，我们可以享受到并发的优势，相关代码如下：[插图]对比两者的时间总消耗，前者为M+N，后者为max（M, N）。随着应用复杂性的增加，情景将会变成M + N + …和max（M, N, …），同步与异步的优劣将会凸显出来。另一方面，随着网站或应用不断膨胀，数据将会分布到多台服务器上，分布式将会是常态。分布也意味着M与N的值会线性增长，这也会放大异步和同步在性能方面的差异。为了让读者感知到M和N值具体多昂贵，表3-1列出了从CPU一级缓存到网络的数据访问所需要的开销。表3-1 不同的I/O类型及其对应的开销[插图]这就是异步I/O在Node中如此盛行，甚至将其作为主要理念进行设计的原因。I/O是昂贵的,分布式I/O是更昂贵的。只有后端能够快速响应资源，才能让前端的体验变好。

3.1.2 资源分配排除用户体验的因素，我们从资源分配的层面来分析一下异步I/O的必要性。我们知道计算机在发展过程中将组件进行了抽象，分为I/O设备和计算设备。假设业务场景中有一组互不相关的任务需要完成，现行的主流方法有以下两种。❑ 单线程串行依次执行。❑ 多线程并行完成。如果创建多线程的开销小于并行执行，那么多线程的方式是首选的。多线程的代价在于创建线程和执行期线程上下文切换的开销较大。另外，在复杂的业务中，多线程编程经常面临锁、状态同步等问题，这是多线程被诟病的主要原因。但是多线程在多核CPU上能够有效提升CPU的利用率，这个优势是毋庸置疑的。单线程顺序执行任务的方式比较符合编程人员按顺序思考的思维方式。它依然是最主流的编程方式，因为它易于表达。但是串行执行的缺点在于性能，任意一个略慢的任务都会导致后续执行代码被阻塞。在计算机资源中，通常I/O与CPU计算之间是可以并行进行的。但是同步的编程模型导致的问题是，I/O的进行会让后续任务等待，这造成资源不能被更好地利用。

操作系统会将CPU的时间片分配给其余进程，以公平而有效地利用资源，基于这一点，有的服务器为了提升响应能力，会通过启动多个工作进程来为更多的用户服务。但是对于这一组任务而言，它无法分发任务到多个进程上，所以依然无法高效利用资源，结束所有任务所需的时间将会较长。这种模式类似于加三倍服务器，达到占用更多资源来提升服务速度，它并没能真正改善问题。添加硬件资源是一种提升服务质量的方式，但它不是唯一的方式。单线程同步编程模型会因阻塞I/O导致硬件资源得不到更优的使用。多线程编程模型也因为编程中的死锁、状态同步等问题让开发人员头疼。Node在两者之间给出了它的方案：利用单线程，远离多线程死锁、状态同步等问题；利用异步I/O，让单线程远离阻塞，以更好地使用CPU。异步I/O可以算作Node的特色，因为它是首个大规模将异步I/O应用在应用层上的平台，它力求在单线程上将资源分配得更高效。为了弥补单线程无法利用多核CPU的缺点，Node提供了类似前端浏览器中WebWorkers的子进程，该子进程可以通过工作进程高效地利用CPU和I/O。这部分内容将在第9章中详述。

异步I/O的提出是期望I/O的调用不再阻塞后续运算，将原有等待I/O完成的这段时间分配给其余需要的业务去执行。图3-1为异步I/O的调用示意图。[插图]图3-1 异步I/O的调用示意图

## 3.2 异步 I/O 实现现状

异步I/O在Node中应用最为广泛，但是它并非Node的原创。如同Brendan Eich援引18世纪英国文学家约翰逊所说，“它的优秀之处并非原创，它的原创之处并不优秀”，以之评价他自己创造的JavaScript一样，Node的优秀之处也并非原创。下面我们看看操作系统对异步I/O实现的支持状况。3.2.1 异步I/O与非阻塞I/O在听到Node的介绍时，我们时常会听到异步、非阻塞、回调、事件这些词语混合在一起推介出来，其中异步与非阻塞听起来似乎是同一回事。从实际效果而言，异步和非阻塞都达到了我们并行I/O的目的。但是从计算机内核I/O而言，异步/同步和阻塞/非阻塞实际上是两回事。操作系统内核对于I/O只有两种方式：阻塞与非阻塞。在调用阻塞I/O时，应用程序需要等待I/O完成才返回结果，如图3-2所示。[插图]图3-2 调用阻塞I/O的过程阻塞I/O的一个特点是调用之后一定要等到系统内核层面完成所有操作后，调用才结束。以读取磁盘上的一段文件为例，系统内核在完成磁盘寻道、读取数据、复制数据到内存中之后，这个调用才结束。

阻塞I/O造成CPU等待I/O，浪费等待时间，CPU的处理能力不能得到充分利用。为了提高性能，内核提供了非阻塞I/O。非阻塞I/O跟阻塞I/O的差别为调用之后会立即返回，如图3-3所示。[插图]图3-3 调用非阻塞I/O的过程操作系统对计算机进行了抽象，将所有输入输出设备抽象为文件。内核在进行文件I/O操作时，通过文件描述符进行管理，而文件描述符类似于应用程序与系统内核之间的凭证。应用程序如果需要进行I/O调用，需要先打开文件描述符，然后再根据文件描述符去实现文件的数据读写。此处非阻塞I/O与阻塞I/O的区别在于阻塞I/O完成整个获取数据的过程，而非阻塞I/O则不带数据直接返回，要获取数据，还需要通过文件描述符再次读取。非阻塞I/O返回之后，CPU的时间片可以用来处理其他事务，此时的性能提升是明显的。但非阻塞I/O也存在一些问题。由于完整的I/O并没有完成，立即返回的并不是业务层期望的数据，而仅仅是当前调用的状态。为了获取完整的数据，应用程序需要重复调用I/O操作来确认是否完成。这种重复调用判断操作是否完成的技术叫做轮询，下面我们就来简要介绍这种技术。

任意技术都并非完美的。阻塞I/O造成CPU等待浪费，非阻塞带来的麻烦却是需要轮询去确认是否完全完成数据获取，它会让CPU处理状态判断，是对CPU资源的浪费。这里我们且看轮询技术是如何演进的，以减小I/O状态判断的CPU损耗。现存的轮询技术主要有以下这些。❑ read。它是最原始、性能最低的一种，通过重复调用来检查I/O的状态来完成完整数据的读取。在得到最终数据前，CPU一直耗用在等待上。图3-4为通过read进行轮询的示意图。[插图]图3-4 通过read进行轮询的示意图❑ select。它是在read的基础上改进的一种方案，通过对文件描述符上的事件状态来进行判断。图3-5为通过select进行轮询的示意图。[插图]图3-5 通过select进行轮询的示意图select轮询具有一个较弱的限制，那就是由于它采用一个1024长度的数组来存储状态，所以它最多可以同时检查1024个文件描述符。❑ poll。该方案较select有所改进，采用链表的方式避免数组长度的限制，其次它能避免不需要的检查。但是当文件描述符较多的时候，它的性能还是十分低下的。图3-6为通过poll实现轮询的示意图，它与select相似，但性能限制有所改善。[插图]图3-6 通过poll实现轮询的示意图❑ epoll。该方案是Linux下效率最高的I/O事件通知机制，在进入轮询的时候如果没有检查到I/O事件，将会进行休眠，直到事件发生将它唤醒。它是真实利用了事件通知、执行回调的方式，而不是遍历查询，所以不会浪费CPU，执行效率较高。图3-7为通过epoll方式实现轮询的示意图。[插图]图3-7 通过epoll方式实现轮询的示意图❑ kqueue。该方案的实现方式与epoll类似，不过它仅在FreeBSD系统下存在。轮询技术满足了非阻塞I/O确保获取完整数据的需求，但是对于应用程序而言，它仍然只能算是一种同步，因为应用程序仍然需要等待I/O完全返回，依旧花费了很多时间来等待。等待期间，CPU要么用于遍历文件描述符的状态，要么用于休眠等待事件发生。结论是它不够好。

3.2.2 理想的非阻塞异步I/O尽管epoll已经利用了事件来降低CPU的耗用，但是休眠期间CPU几乎是闲置的，对于当前线程而言利用率不够。那么，是否有一种理想的异步I/O呢？我们期望的完美的异步I/O应该是应用程序发起非阻塞调用，无须通过遍历或者事件唤醒等方式轮询，可以直接处理下一个任务，只需在I/O完成后通过信号或回调将数据传递给应用程序即可。图3-8为理想中的异步I/O示意图。[插图]图3-8 理想中的异步I/O示意图幸运的是，在Linux下存在这样一种方式，它原生提供的一种异步I/O方式（AIO）就是通过信号或回调来传递数据的。但不幸的是，只有Linux下有，而且它还有缺陷——AIO仅支持内核I/O中的O_DIRECT方式读取，导致无法利用系统缓存。3.2.3 现实的异步I/O现实比理想要骨感一些，但是要达成异步I/O的目标，并非难事。前面我们将场景限定在了单线程的状况下，多线程的方式会是另一番风景。通过让部分线程进行阻塞I/O或者非阻塞I/O加轮询技术来完成数据获取，让一个线程进行计算处理，通过线程之间的通信将I/O得到的数据进行传递，这就轻松实现了异步I/O（尽管它是模拟的），示意图如图3-9所示。[插图]图3-9 异步I/O

glibc的AIO便是典型的线程池模拟异步I/O。然而遗憾的是，它存在一些难以忍受的缺陷和bug，不推荐采用。libev的作者Marc Alexander Lehmann重新实现了一个异步I/O的库：libeio。libeio实质上依然是采用线程池与阻塞I/O模拟异步I/O。最初，Node在*nix平台下采用了libeio配合libev实现I/O部分，实现了异步I/O。在Node v0.9.3中，自行实现了线程池来完成异步I/O。另一种我迟迟没有透露的异步I/O方案则是Windows下的IOCP，它在某种程度上提供了理想的异步I/O：调用异步方法，等待I/O完成之后的通知，执行回调，用户无须考虑轮询。但是它的内部其实仍然是线程池原理，不同之处在于这些线程池由系统内核接手管理。IOCP的异步I/O模型与Node的异步调用模型十分近似。在Windows平台下采用了IOCP实现异步I/O。由于Windows平台和*nix平台的差异，Node提供了libuv作为抽象封装层，使得所有平台兼容性的判断都由这一层来完成，并保证上层的Node与下层的自定义线程池及IOCP之间各自独立。Node在编译期间会判断平台条件，选择性编译unix目录或是win目录下的源文件到目标程序中，其架构如图3-10所示。[插图]图3-10 基于libuv的架构示意图

需要强调一点的是，这里的I/O不仅仅只限于磁盘文件的读写。*nix将计算机抽象了一番，磁盘文件、硬件、套接字等几乎所有计算机资源都被抽象为了文件，因此这里描述的阻塞和非阻塞的情况同样能适合于套接字等。另一个需要强调的地方在于我们时常提到Node是单线程的，这里的单线程仅仅只是JavaScript执行在单线程中罢了。在Node中，无论是*nix还是Windows平台，内部完成I/O任务的另有线程池。

## 3.3 Node 的异步 I/O

介绍完系统对异步I/O的支持后，我们将继续介绍Node是如何实现异步I/O的。这里我们除了介绍异步I/O的实现外，还将讨论Node的执行模型。完成整个异步I/O环节的有事件循环、观察者和请求对象等。3.3.1 事件循环首先，我们着重强调一下Node自身的执行模型——事件循环，正是它使得回调函数十分普遍。在进程启动时，Node便会创建一个类似于while(true)的循环，每执行一次循环体的过程我们称为Tick。每个Tick的过程就是查看是否有事件待处理，如果有，就取出事件及其相关的回调函数。如果存在关联的回调函数，就执行它们。然后进入下个循环，如果不再有事件处理，就退出进程。流程图如图3-11所示。[插图]图3-11 Tick流程图3.3.2 观察者在每个Tick的过程中，如何判断是否有事件需要处理呢？这里必须要引入的概念是观察者。每个事件循环中有一个或者多个观察者，而判断是否有事件要处理的过程就是向这些观察者询问是否有要处理的事件。

这个过程就如同饭馆的厨房，厨房一轮一轮地制作菜肴，但是要具体制作哪些菜肴取决于收银台收到的客人的下单。厨房每做完一轮菜肴，就去问收银台的小妹，接下来有没有要做的菜，如果没有的话，就下班打烊了。在这个过程中，收银台的小妹就是观察者，她收到的客人点单就是关联的回调函数。当然，如果饭馆经营有方，它可能有多个收银员，就如同事件循环中有多个观察者一样。收到下单就是一个事件，一个观察者里可能有多个事件。浏览器采用了类似的机制。事件可能来自用户的点击或者加载某些文件时产生，而这些产生的事件都有对应的观察者。在Node中，事件主要来源于网络请求、文件I/O等，这些事件对应的观察者有文件I/O观察者、网络I/O观察者等。观察者将事件进行了分类。事件循环是一个典型的生产者/消费者模型。异步I/O、网络请求等则是事件的生产者，源源不断为Node提供不同类型的事件，这些事件被传递到对应的观察者那里，事件循环则从观察者那里取出事件并处理。在Windows下，这个循环基于IOCP创建，而在*nix下则基于多线程创建。3.3.3 请求对象在这一节中，我们将通过解释Windows下异步I/O（利用IOCP实现）的简单例子来探寻从JavaScript代码到系统内核之间都发生了什么。

对于一般的（非异步）回调函数，函数由我们自行调用，如下所示：[插图]对于Node中的异步I/O调用而言，回调函数却不由开发者来调用。那么从我们发出调用后，到回调函数被执行，中间发生了什么呢？事实上，从JavaScript发起调用到内核执行完I/O操作的过渡过程中，存在一种中间产物，它叫做请求对象。下面我们以最简单的fs.open()方法来作为例子，探索Node与底层之间是如何执行异步I/O调用以及回调函数究竟是如何被调用执行的：[插图]fs.open()的作用是根据指定路径和参数去打开一个文件，从而得到一个文件描述符，这是后续所有I/O操作的初始操作。从前面的代码中可以看到，JavaScript层面的代码通过调用C++核心模块进行下层的操作。图3-12为调用示意图。[插图]图3-12 调用示意图从JavaScript调用Node的核心模块，核心模块调用C++内建模块，内建模块通过libuv进行系统调用，这是Node里经典的调用方式。这里libuv作为封装层，有两个平台的实现，实质上是调用了uv_fs_open()方法。在uv_fs_open()的调用过程中，我们创建了一个FSReqWrap请求对象。从JavaScript层传入的参数和当前方法都被封装在这个请求对象中，其中我们最为关注的回调函数则被设置在这个对象的oncomplete_sym属性上：

[插图]对象包装完毕后，在Windows下，则调用QueueUserWorkItem()方法将这个FSReqWrap对象推入线程池中等待执行，该方法的代码如下所示：[插图]QueueUserWorkItem()方法接受3个参数：第一个参数是将要执行的方法的引用，这里引用的是uv_fs_thread_proc，第二个参数是uv_fs_thread_proc方法运行时所需要的参数；第三个参数是执行的标志。当线程池中有可用线程时，我们会调用uv_fs_thread_proc()方法。uv_fs_thread_proc()方法会根据传入参数的类型调用相应的底层函数。以uv_fs_open()为例，实际上调用fs__open()方法。至此，JavaScript调用立即返回，由JavaScript层面发起的异步调用的第一阶段就此结束。JavaScript线程可以继续执行当前任务的后续操作。当前的I/O操作在线程池中等待执行，不管它是否阻塞I/O，都不会影响到JavaScript线程的后续执行，如此就达到了异步的目的。请求对象是异步I/O过程中的重要中间产物，所有的状态都保存在这个对象中，包括送入线程池等待执行以及I/O操作完毕后的回调处理。3.3.4 执行回调组装好请求对象、送入I/O线程池等待执行，实际上完成了异步I/O的第一部分，回调通知是第二部分。

线程池中的I/O操作调用完毕之后，会将获取的结果储存在req->result属性上，然后调用PostQueuedCompletionStatus()通知IOCP，告知当前对象操作已经完成：[插图]PostQueuedCompletionStatus()方法的作用是向IOCP提交执行状态，并将线程归还线程池。通过PostQueuedCompletionStatus()方法提交的状态，可以通过GetQueuedCompletionStatus()提取。在这个过程中，我们其实还动用了事件循环的I/O观察者。在每次Tick的执行中，它会调用IOCP相关的GetQueuedCompletionStatus()方法检查线程池中是否有执行完的请求，如果存在，会将请求对象加入到I/O观察者的队列中，然后将其当做事件处理。I/O观察者回调函数的行为就是取出请求对象的result属性作为参数，取出oncomplete_sym属性作为方法，然后调用执行，以此达到调用JavaScript中传入的回调函数的目的。至此，整个异步I/O的流程完全结束，如图3-13所示。

[插图]图3-13 整个异步I/O的流程事件循环、观察者、请求对象、I/O线程池这四者共同构成了Node异步I/O模型的基本要素。Windows下主要通过IOCP来向系统内核发送I/O调用和从内核获取已完成的I/O操作，配以事件循环，以此完成异步I/O的过程。在Linux下通过epoll实现这个过程，FreeBSD下通过kqueue实现，Solaris下通过Event ports实现。不同的是线程池在Windows下由内核（IOCP）直接提供，*nix系列下由libuv自行实现。

3.3.5 小结从前面实现异步I/O的过程描述中，我们可以提取出异步I/O的几个关键词：单线程、事件循环、观察者和I/O线程池。这里单线程与I/O线程池之间看起来有些悖论的样子。由于我们知道JavaScript是单线程的，所以按常识很容易理解为它不能充分利用多核CPU。事实上，在Node中，除了JavaScript是单线程外，Node自身其实是多线程的，只是I/O线程使用的CPU较少。另一个需要重视的观点则是，除了用户代码无法并行执行外，所有的I/O（磁盘I/O和网络I/O等）则是可以并行起来的。

## 3.4 非 I/O 的异步 API

尽管我们在介绍Node的时候，多数情况下都会提到异步I/O，但是Node中其实还存在一些与I/O无关的异步API，这一部分也值得略微关注一下，它们分别是setTimeout()、setInterval()、setImmediate()和process.nextTick()。3.4.1 定时器setTimeout()和setInterval()与浏览器中的API是一致的，分别用于单次和多次定时执行任务。它们的实现原理与异步I/O比较类似，只是不需要I/O线程池的参与。调用setTimeout()或者setInterval()创建的定时器会被插入到定时器观察者内部的一个红黑树中。每次Tick执行时，会从该红黑树中迭代取出定时器对象，检查是否超过定时时间，如果超过，就形成一个事件，它的回调函数将立即执行。图3-14提到的主要是setTimeout()的行为。setInterval()与之相同，区别在于后者是重复性的检测和执行。[插图]图3-14 setTimeout()的行为定时器的问题在于，它并非精确的（在容忍范围内）。尽管事件循环十分快，但是如果某一次循环占用的时间较多，那么下次循环时，它也许已经超时很久了。譬如通过setTimeout()设定一个任务在10毫秒后执行，但是在9毫秒后，有一个任务占用了5毫秒的CPU时间片，再次轮到定时器执行时，时间就已经过期4毫秒。3.4.2 process.nextTick()

在未了解process.nextTick()之前，很多人也许为了立即异步执行一个任务，会这样调用setTimeout()来达到所需的效果：[插图]由于事件循环自身的特点，定时器的精确度不够。而事实上，采用定时器需要动用红黑树，创建定时器对象和迭代等操作，而setTimeout(fn, 0)的方式较为浪费性能。实际上，process.nextTick()方法的操作相对较为轻量，具体代码如下：[插图]每次调用process.nextTick()方法，只会将回调函数放入队列中，在下一轮Tick时取出执行。定时器中采用红黑树的操作时间复杂度为O(lg(n)), nextTick()的时间复杂度为O(1)。相较之下，process.nextTick()更高效。3.4.3 setImmediate()

setImmediate()方法与process.nextTick()方法十分类似，都是将回调函数延迟执行。在Node v0.9.1之前，setImmediate()还没有实现，那时候实现类似的功能主要是通过process.nextTick()来完成，该方法的代码如下所示：[插图]上述代码的输出结果如下：[插图]而用setImmediate()实现时，相关代码如下：[插图]其结果完全一样：[插图]但是两者之间其实是有细微差别的。将它们放在一起时，又会是怎样的优先级呢。示例代码如下：[插图]其执行结果如下：[插图]从结果里可以看到，process.nextTick()中的回调函数执行的优先级要高于setImmediate()。这里的原因在于事件循环对观察者的检查是有先后顺序的，process.nextTick()属于idle观察者，setImmediate()属于check观察者。在每一个轮循环检查中，idle观察者先于I/O观察者，I/O观察者先于check观察者。

在具体实现上，process.nextTick()的回调函数保存在一个数组中，setImmediate()的结果则是保存在链表中。在行为上，process.nextTick()在每轮循环中会将数组中的回调函数全部执行完，而setImmediate()在每轮循环中执行链表中的一个回调函数。如下的示例代码可以佐证：[插图]其执行结果[插图]如下：[插图]从执行结果上可以看出，当第一个setImmediate()的回调函数执行后，并没有立即执行第二个，而是进入了下一轮循环，再次按process.nextTick()优先、setImmediate()次后的顺序执行。之所以这样设计，是为了保证每轮循环能够较快地执行结束，防止CPU占用过多而阻塞后续I/O调用的情况。

## 3.5 事件驱动与高性能服务器

前面主要介绍了异步的实现原理，在这个过程中，我们也基本勾勒出了事件驱动的实质，即通过主循环加事件触发的方式来运行程序。尽管本章只用了fs.open()方法作为例子来阐述Node如何实现异步I/O。而实质上，异步I/O不仅仅应用在文件操作中。对于网络套接字的处理，Node也应用到了异步I/O，网络套接字上侦听到的请求都会形成事件交给I/O观察者。事件循环会不停地处理这些网络I/O事件。如果JavaScript有传入回调函数，这些事件将会最终传递到业务逻辑层进行处理。利用Node构建Web服务器，正是在这样一个基础上实现的，其流程图如图3-15所示。[插图]图3-15 利用Node构建Web服务器的流程图下面为几种经典的服务器模型，这里对比下它们的优缺点。

❑ 同步式。对于同步式的服务，一次只能处理一个请求，并且其余请求都处于等待状态。❑ 每进程/每请求。为每个请求启动一个进程，这样可以处理多个请求，但是它不具备扩展性，因为系统资源只有那么多。❑ 每线程/每请求。为每个请求启动一个线程来处理。尽管线程比进程要轻量，但是由于每个线程都占用一定内存，当大并发请求到来时，内存将会很快用光，导致服务器缓慢。每线程/每请求的扩展性比每进程/每请求的方式要好，但对于大型站点而言依然不够。每线程/每请求的方式目前还被Apache所采用。Node通过事件驱动的方式处理请求，无须为每一个请求创建额外的对应线程，可以省掉创建线程和销毁线程的开销，同时操作系统在调度任务时因为线程较少，上下文切换的代价很低。这使得服务器能够有条不紊地处理请求，即使在大量连接的情况下，也不受线程上下文切换开销的影响，这是Node高性能的一个原因。

事件驱动带来的高效已经渐渐开始为业界所重视。知名服务器Nginx，也摒弃了多线程的方式，采用了和Node相同的事件驱动。如今，Nginx大有取代Apache之势。Node具有与Nginx相同的特性，不同之处在于Nginx采用纯C写成，性能较高，但是它仅适合于做Web服务器，用于反向代理或负载均衡等服务，在处理具体业务方面较为欠缺。Node则是一套高性能的平台，可以利用它构建与Nginx相同的功能，也可以处理各种具体业务，而且与背后的网络保持异步畅通。两者相比，Node没有Nginx在Web服务器方面那么专业，但场景更大，自身性能也不错。在实际项目中，我们可以结合它们各自优点，以达到应用的最优性能。事实上，Node的异步I/O并非首创，但却是第一个成功的平台。在那之前，也有一些知名的基于事件驱动的实现，具体如下所示。❑ Ruby的Event Machine。❑ Perl的AnyEvent。❑ Python的Twisted。在这些平台上采用事件驱动的方式时，需要花一定精力了解这些库。这些库没能成功的原因则是同步I/O库的存在。本章描述的异步I/O实现，其主旨是使I/O操作与CPU操作分离。奈何这些语言平台上的标准I/O库都是阻塞式的，一旦事件循环中存在阻塞I/O，将导致其余I/O无法立即进行，性能会急剧下降，其效果类似于同步式服务，其他请求将不能立即处理。

因为在这些成熟的语言平台上，异步不是主流，尽管有这些事件驱动的实现库，但开发者总会习惯性地采用同步I/O库，这导致预想的高性能直接落空。Ryan Dahl在评估他最早的选型时，Lua一度是最贴近他选型的语言，但是由于标准I/O库是同步I/O，他知道即使完成这样一个事件驱动的实现，也将不会得到较大范围的使用。在Node广泛流行之后，社区的Tim Caswell将Node的这套思想重新移植到了Lua平台，该项目叫luvit。JavaScript中的作用域和函数在浏览器端已有成熟的应用，也很好地帮助了RyanDahl实现它的想法。JavaScript在服务器端近乎空白，使得Node没有任何历史包袱，而Node在性能上的表现使得它一下子就在社区中流行起来了。

## 3.6 总结

本章介绍了异步I/O和另一些非I/O的异步方法。可以看出，事件循环是异步实现的核心，它与浏览器中的执行模型基本保持了一致。而像古老的Rhino，尽管是较早就能在服务器端运行的JavaScript运行时，但是执行模型并不像浏览器采用事件驱动，而是像其他语言一般采用同步I/O作为主要模型，这造成它在性能上无所发挥。Node正是依靠构建了一套完善的高性能异步I/O框架，打破了JavaScript在服务器端止步不前的局面。

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

有异步I/O，必有异步编程。上一章描述了Node如何通过事件循环实现异步，包括与各种I/O多路复用搭配实现的异步I/O以及与I/O无关的异步。Node是首个将异步大规模带到应用层面的平台，它从内在运行机制到API的设计，无不透露出异步的气息来。异步的高性能为它带来了高度的赞誉，而异步编程也为其带来部分的诋毁。前述章节中亦描述过异步I/O在应用层面不流行的原因，那便是异步编程在流程控制中，业务表达并不太适合自然语言的线性思维习惯。较少人能适应直接面对事件驱动进行编程，唯独对它熟悉的主要是GUI开发者，如前端工程师或GUI工程师。前端工程师习以为常并能够娴熟地处理各种DOM事件和浏览器中的事件。RyanDahl偏好事件驱动，而Java Script在浏览器中也正契合事件驱动的执行过程，这也使得前后端的JavaScript在执行原理和风格上都趋于一致。虽然语言执行在不同的环境，但除了宿主提供的API有所不同外，并不让人觉得是一门新语言。V8和异步I/O在性能上带来的提升，前后端JavaScript编程风格一致，是Node能够迅速成功并流行起来的主要原因。

## 4.1 函数式编程

在开始异步编程之前，先得知晓JavaScript现今的回调函数和深层嵌套的来龙去脉。在JavaScript中，函数（function）作为一等公民，使用上非常自由，无论调用它，或者作为参数，或者作为返回值均可。函数的灵活性是JavaScript比较吸引人的地方之一，它与古老的Lisp语言颇具渊源。JavaScript在诞生之前，BrendanEich借鉴了Scheme语言（Scheme作为Lisp的派生），吸收了函数式编程的精华，将函数作为一等公民便是典型案例。鉴于函数式编程在近年来重新火热，而前端类图书中较少述及这部分知识，这里稍作补充，因为它是JavaScript异步编程的基础。4.1.1 高阶函数在通常的语言中，函数的参数只接受基本的数据类型或是对象引用，返回值也只是基本数据类型和对象引用。下面的代码为常规的参数传递和返回：[插图]高阶函数则是可以把函数作为参数，或是将函数作为返回值的函数，如下面的代码所示：[插图]高阶函数可以将函数作为输入或返回值的变化看起来虽细小，但是对于C/C++语言而言，通过指针也可以达到相同的效果。但对于程序编写，高阶函数则比普通的函数要灵活许多。除了通常意义的函数调用返回外，还形成了一种后续传递风格（Continuation Passing Style）的结果接收方式，而非单一的返回值形式。后续传递风格的程序编写将函数的业务重点从返回值转移到了回调函数中：[插图]以上面的代码为例，对于相同的foo()函数，传入的bar参数不同，则可以得到不同的结果。一个经典的例子便是数组的sort()方法，它是一个货真价实的高阶函数，可以接受一个方法作为参数参与运算排序：[插图]通过改动sort()方法的参数，可以决定不同的排序方式，从这里可以看出高阶函数的灵活性来。结合Node提供的最基本的事件模块可以看到，事件的处理方式正是基于高阶函数的特性来完成的。在自定义事件实例中，通过为相同事件注册不同的回调函数，可以很灵活地处理业务逻辑。示例代码如下：[插图]本书时常提到事件可以十分方便地进行复杂业务逻辑的解耦，它其实受益于高阶函数。高阶函数在JavaScript中比比皆是，其中ECMAScript5中提供的一些数组方法（forEach()、map()、reduce()、reduceRight()、filter()、every()、some()）十分典型。

4.1.2 偏函数用法偏函数用法是指创建一个调用另外一个部分——参数或变量已经预置的函数——的函数的用法。这句话相对较为拗口，下面我们以实例来说明：[插图]在JavaScript中进行类型判断时，我们通常会进行类似上述代码的方法定义。这段代码固然不复杂，只有两个函数的定义，但是里面存在的问题是我们需要重复去定义一些相似的函数，如果有更多的isXXX()，就会出现更多的冗余代码。为了解决重复定义的问题，我们引入一个新函数，这个新函数可以如工厂一样批量创建一些类似的函数。在下面的代码中，我们通过isType()函数预先指定type的值，然后返回一个新的函数：[插图]可以看出，引入isType()函数后，创建isString()、isFunction()函数就变得简单多了。这种通过指定部分参数来产生一个新的定制函数的形式就是偏函数。偏函数应用在异步编程中也十分常见，著名类库Underscore提供的after()方法即是偏函数应用，其定义如下：[插图]这个函数可以根据传入的times参数和具体方法，生成一个需要调用多次才真正执行实际函数的函数。

## 4.2 异步编程的优势与难点

曾经的单线程模型在同步I/O的影响下，由于I/O调用缓慢，在应用层面导致CPU与I/O无法重叠进行。为了照顾编程人员的阅读思维习惯，同步I/O盛行了很多年。但在日新月异的技术大潮面前，性能问题摆在了编程人员的面前。提升性能的方式过去多用多线程的方式解决，但是多线程的引入在业务逻辑方面制造的麻烦也不少。从操作系统调度多线程的上下文切换开销，到实际编程里的锁、同步等问题，让开发人员头疼的时候也并不少。另一个解决I/O性能的方案是通过C/C++调用操作系统底层接口，自己手工完成异步I/O，这能够达到很高的性能，但是调试和开发门槛均十分高，在帮助业务解决问题上，需要花费较大的精力。Node利用JavaScript及其内部异步库，将异步直接提升到业务层面，这是一种创新。4.2.1 优势Node带来的最大特性莫过于基于事件驱动的非阻塞I/O模型，这是它的灵魂所在。非阻塞I/O可以使CPU与I/O并不相互依赖等待，让资源得到更好的利用。对于网络应用而言，并行带来的想象空间更大，延展而开的是分布式和云。并行使得各个单点之间能够更有效地组织起来，这也是Node在云计算厂商中广受青睐的原因，图4-1为异步I/O调用的示意图。

[插图]图4-1 异步I/O调用的示意图如果采用传统的同步I/O模型，分布式计算中性能的折扣将会是明显的，如图4-2所示。[插图]图4-2 同步I/O调用示意图在第3章中，我们讨论过Node实现异步I/O的原理。利用事件循环的方式，JavaScript线程像一个分配任务和处理结果的大管家，I/O线程池里的各个I/O线程都是小二，负责兢兢业业地完成分配来的任务，小二与管家之间互不依赖，所以可以保持整体的高效率。这个利用事件循环的经典调度方式在很多地方都存在应用，最典型的是UI编程，如iOS应用开发等。这个模型的缺点则在于管家无法承担过多的细节性任务，如果承担太多，则会影响到任务的调度，管家忙个不停，小二却得不到活干，结局则是整体效率的降低。换言之，Node是为了解决编程模型中阻塞I/O的性能问题的，采用了单线程模型，这导致Node更像一个处理I/O密集问题的能手，而CPU密集型则取决于管家的能耐如何。在第1章中，从斐波那契数列计算的测试结果中可以看到，这个管家具体的能力如何。如果形象地去评判的话，C语言是性能至尊，得益于V8性能的Node则是一流武林高手，在具备武功秘笈的情况下（调用C/C++扩展模块）, Node的能力可以逼近顶尖之列。

由于事件循环模型需要应对海量请求，海量请求同时作用在单线程上，就需要防止任何一个计算耗费过多的CPU时间片。至于是计算密集型，还是I/O密集型，只要计算不影响异步I/O的调度，那就不构成问题。建议对CPU的耗用不要超过10ms，或者将大量的计算分解为诸多的小量计算，通过setImmediate()进行调度。只要合理利用Node的异步模型与V8的高性能，就可以充分发挥CPU和I/O资源的优势。4.2.2 难点Node令异步编程如此风行，这也是异步编程首次大规模出现在业务层面。它借助异步I/O模型及V8高性能引擎，突破单线程的性能瓶颈，让JavaScript在后端达到实用价值。另一方面，它也统一了前后端JavaScript的编程模型。对于异步编程带来的新鲜感与不适感，开发者们有着不同程度的感受。接下来，我们梳理一下异步编程的难点，以更好地利用Node。1．难点1：异常处理过去我们处理异常时，通常使用类Java的try/catch/final语句块进行异常捕获，示例代码如下：

[插图]但是这对于异步编程而言并不一定适用。第3章提到过，异步I/O的实现主要包含两个阶段：提交请求和处理结果。这两个阶段中间有事件循环的调度，两者彼此不关联。异步方法则通常在第一个阶段提交请求后立即返回，因为异常并不一定发生在这个阶段，try/catch的功效在此处不会发挥任何作用。异步方法的定义如下所示：[插图]调用async()方法后，callback被存放起来，直到下一个事件循环（Tick）才会取出来执行。尝试对异步方法进行try/catch操作只能捕获当次事件循环内的异常，对callback执行时抛出的异常将无能为力，示例代码如下：[插图]Node在处理异常上形成了一种约定，将异常作为回调函数的第一个实参传回，如果为空值，则表明异步调用没有异常抛出：[插图]在我们自行编写的异步方法上，也需要去遵循这样一些原则：原则一：必须执行调用者传入的回调函数；原则二：正确传递回异常供调用者判断。示例代码如下：

[插图]在异步方法的编写中，另一个容易犯的错误是对用户传递的回调函数进行异常捕获，示例代码如下：[插图]上述代码的意图是捕获JSON.parse()中可能出现的异常，但是却不小心包含了用户传递的回调函数。这意味着如果回调函数中有异常抛出，将会进入catch()代码块中执行，于是回调函数将会被执行两次。这显然不是预期的情况，可能导致业务混乱。正确的捕获应当为：[插图]在编写异步方法时，只要将异常正确地传递给用户的回调方法即可，无须过多处理。2．难点2：函数嵌套过深这或许是Node被人诟病最多的地方。在前端开发中，DOM事件相对而言不会存在互相依赖或需要多个事件一起协作的场景，较少存在异步多级依赖的情况。下面的代码为彼此独立的DOM事件绑定：[插图]但是对于Node而言，事务中存在多个异步调用的场景比比皆是。比如一个遍历目录的操作，其代码如下：[插图]对于上述场景，由于两次操作存在依赖关系，函数嵌套的行为也许情有可原。那么，在网页渲染的过程中，通常需要数据、模板、资源文件，这三者互相之间并不依赖，但最终渲染结果中三者缺一不可。如果采用默认的异步方法调用，程序也许将会如下所示：

[插图]这在结果的保证上是没有问题的，问题在于这并没有利用好异步I/O带来的并行优势。这是异步编程的典型问题，为此有人曾说，因为嵌套的深度，未来最难看的代码必将从Node中诞生。但是实际情况没有想象得那么糟糕，且看后面如何解决该问题。3．难点3：阻塞代码对于进入JavaScript世界不久的开发者，比较纳闷这门编程语言竟然没有sleep()这样的线程沉睡功能，唯独能用于延时操作的只有setInterval()和setTimeout()这两个函数。但是让人惊讶的是，这两个函数并不能阻塞后续代码的持续执行。所以，有多半的开发者会写出下述这样的代码来实现sleep(1000)的效果：[插图]但是事实是糟糕的，这段代码会持续占用CPU进行判断，与真正的线程沉睡相去甚远，完全破坏了事件循环的调度。由于Node单线程的原因，CPU资源全都会用于为这段代码服务，导致其余任何请求都会得不到响应。遇见这样的需求时，在统一规划业务逻辑之后，调用setTimeout()的效果会更好。4．难点4：多线程编程

我们在谈论JavaScript的时候，通常谈的是单一线程上执行的代码，这在浏览器中指的是JavaScript执行线程与UI渲染共用的一个线程；在Node中，只是没有UI渲染的部分，模型基本相同。对于服务器端而言，如果服务器是多核CPU，单个Node进程实质上是没有充分利用多核CPU的。随着现今业务的复杂化，对于多核CPU利用的要求也越来越高。浏览器提出了Web Workers，它通过将JavaScript执行与UI渲染分离，可以很好地利用多核CPU为大量计算服务。同时前端WebWorkers也是一个利用消息机制合理使用多核CPU的理想模型。图4-3为WebWorkers的工作示意图。[插图]图4-3 Web Workers的工作示意图遗憾在于前端浏览器存在对标准的滞后性，Web Workers并没有广泛应用起来。另外Web Workers能解决利用CPU和减少阻塞UI渲染，但是不能解决UI渲染的效率问题。Node借鉴了这个模式，child_process是其基础API, cluster模块是更深层次的应用。借助Web Workers的模式，开发人员要更多地去面临跨线程的编程，这对于以往的JavaScript编程经验是较少考虑的。在第9章中，我们将详细分析Node的进程，以展开这部分内容。

5．难点5：异步转同步习惯异步编程的同学，也许能够从容面对异步编程带来的副产品，比如嵌套回调、业务分散等问题。Node提供了绝大部分的异步API和少量的同步API，偶尔出现的同步需求将会因为没有同步API让开发者突然无所适从。目前，Node中试图同步式编程，但并不能得到原生支持，需要借助库或者编译等手段来实现。但对于异步调用，通过良好的流程控制，还是能够将逻辑梳理成顺序式的形式。

## 4.3 异步编程解决方案

前面列举了因异步编程带来的一些问题，与异步编程提升的性能成果相比，编程过程看起来似乎没有想象中那么美好，但是事实却也没有那么糟糕。与问题相比，解决问题的方案总是更多，本节将展开各个典型的解决方案。目前，异步编程的主要解决方案有如下3种。❑ 事件发布/订阅模式。❑ Promise/Deferred模式。❑ 流程控制库。4.3.1 事件发布/订阅模式事件监听器模式是一种广泛用于异步编程的模式，是回调函数的事件化，又称发布/订阅模式。Node自身提供的events模块（http://nodejs.org/docs/latest/api/events.html）是发布/订阅模式的一个简单实现，Node中部分模块都继承自它，这个模块比前端浏览器中的大量DOM事件简单，不存在事件冒泡，也不存在preventDefault()、stopPropagation()和stopImmediatePropagation()等控制事件传递的方法。它具有addListener/on()、once()、removeListener()、removeAllListeners()和emit()等基本的事件监听模式的方法实现。事件发布/订阅模式的操作极其简单，示例代码如下：[插图]可以看到，订阅事件就是一个高阶函数的应用。事件发布/订阅模式可以实现一个事件与多个回调函数的关联，这些回调函数又称为事件侦听器。通过emit()发布事件后，消息会立即传递给当前事件的所有侦听器执行。侦听器可以很灵活地添加和删除，使得事件和具体处理逻辑之间可以很轻松地关联和解耦。事件发布/订阅模式自身并无同步和异步调用的问题，但在Node中，emit()调用多半是伴随事件循环而异步触发的，所以我们说事件发布/订阅广泛应用于异步编程。事件发布/订阅模式常常用来解耦业务逻辑，事件发布者无须关注订阅的侦听器如何实现业务逻辑，甚至不用关注有多少个侦听器存在，数据通过消息的方式可以很灵活地传递。在一些典型场景中，可以通过事件发布/订阅模式进行组件封装，将不变的部分封装在组件内部，将容易变化、需自定义的部分通过事件暴露给外部处理，这是一种典型的逻辑分离方式。在这种事件发布/订阅式组件中，事件的设计非常重要，因为它关乎外部调用组件时是否优雅，从某种角度来说事件的设计就是组件的接口设计。从另一个角度来看，事件侦听器模式也是一种钩子（hook）机制，利用钩子导出内部数据或状态给外部的调用者。Node中的很多对象大多具有黑盒的特点，功能点较少，如果不通过事件钩子的形式，我们就无法获取对象在运行期间的中间值或内部状态。这种通过事件钩子的方式，可以使编程者不用关注组件是如何启动和执行的，只需关注在需要的事件点上即可。下面的HTTP请求是典型场景：[插图]

在这段HTTP请求的代码中，程序员只需要将视线放在error、data、end这些业务事件点上即可，至于内部的流程如何，无需过于关注。值得一提的是，Node对事件发布/订阅的机制做了一些额外的处理，这大多是基于健壮性而考虑的。下面为两个具体的细节点。❑ 如果对一个事件添加了超过10个侦听器，将会得到一条警告。这一处设计与Node自身单线程运行有关，设计者认为侦听器太多可能导致内存泄漏，所以存在这样一条警告。调用emitter.setMaxListeners(0)；可以将这个限制去掉。另一方面，由于事件发布会引起一系列侦听器执行，如果事件相关的侦听器过多，可能存在过多占用CPU的情景。❑ 为了处理异常，EventEmitter对象对error事件进行了特殊对待。如果运行期间的错误触发了error事件，EventEmitter会检查是否有对error事件添加过侦听器。如果添加了，这个错误将会交由该侦听器处理，否则这个错误将会作为异常抛出。如果外部没有捕获这个异常，将会引起线程退出。一个健壮的EventEmitter实例应该对error事件做处理。

1．继承events模块实现一个继承EventEmitter的类是十分简单的，以下代码是Node中Stream对象继承EventEmitter的例子：[插图]Node在util模块中封装了继承的方法，所以此处可以很便利地调用。开发者可以通过这样的方式轻松继承EventEmitter类，利用事件机制解决业务问题。在Node提供的核心模块中，有近半数都继承自EventEmitter。2．利用事件队列解决雪崩问题在事件订阅/发布模式中，通常也有一个once()方法，通过它添加的侦听器只能执行一次，在执行之后就会将它与事件的关联移除。这个特性常常可以帮助我们过滤一些重复性的事件响应。下面我们介绍一下如何采用once()来解决雪崩问题。在计算机中，缓存由于存放在内存中，访问速度十分快，常常用于加速数据访问，让绝大多数的请求不必重复去做一些低效的数据读取。所谓雪崩问题，就是在高访问量、大并发量的情况下缓存失效的情景，此时大量的请求同时涌入数据库中，数据库无法同时承受如此大的查询请求，进而往前影响到网站整体的响应速度。以下是一条数据库查询语句的调用：[插图]如果站点刚好启动，这时缓存中是不存在数据的，而如果访问量巨大，同一句SQL会被发送到数据库中反复查询，会影响服务的整体性能。一种改进方案是添加一个状态锁，相关代码如下：

[插图]但是在这种情景下，连续地多次调用select()时，只有第一次调用是生效的，后续的select()是没有数据服务的，这个时候可以引入事件队列，相关代码如下：[插图]这里我们利用了once()方法，将所有请求的回调都压入事件队列中，利用其执行一次就会将监视器移除的特点，保证每一个回调只会被执行一次。对于相同的SQL语句，保证在同一个查询开始到结束的过程中永远只有一次。SQL在进行查询时，新到来的相同调用只需在队列中等待数据就绪即可，一旦查询结束，得到的结果可以被这些调用共同使用。这种方式能节省重复的数据库调用产生的开销。由于Node单线程执行的原因，此处无须担心状态同步问题。这种方式其实也可以应用到其他远程调用的场景中，即使外部没有缓存策略，也能有效节省重复开销。此处可能因为存在侦听器过多引发的警告，需要调用setMaxListeners(0)移除掉警告，或者设更大的警告阈值。once()方法产生的效果，也可以在著名的Gearman异步应用框架中实现。但在JavaScript中，实现这个效果十分容易。

3．多异步之间的协作方案事件发布/订阅模式有着它的优点。利用高阶函数的优势，侦听器作为回调函数可以随意添加和删除，它帮助开发者轻松处理随时可能添加的业务逻辑。也可以隔离业务逻辑，保持业务逻辑单元的职责单一。一般而言，事件与侦听器的关系是一对多，但在异步编程中，也会出现事件与侦听器的关系是多对一的情况，也就是说一个业务逻辑可能依赖两个通过回调或事件传递的结果。前面提及的回调嵌套过深的原因即是如此。这里我们尝试通过原生代码解决“难点2”中为了最终结果的处理而导致可以并行调用但实际只能串行执行的问题。我们的目标是既要享受异步I/O带来的性能提升，也要保持良好的编码风格。这里以渲染页面所需要的模板读取、数据读取和本地化资源读取为例简要介绍一下，相关代码如下：[插图]由于多个异步场景中回调函数的执行并不能保证顺序，且回调函数之间互相没有任何交集，所以需要借助一个第三方函数和第三方变量来处理异步协作的结果。通常，我们把这个用于检测次数的变量叫做哨兵变量。聪明的你也许已经想到利用偏函数来处理哨兵变量和第三方函数的关系了，相关代码如下：

[插图]上述方案实现了多对一的目的。如果业务继续增长，我们依然可以继续利用发布/订阅方式来完成多对多的方案，相关代码如下：[插图]这种方案结合了前者用简单的偏函数完成多对一的收敛和事件订阅/发布模式中一对多的发散。在上面的方法中，有一个令调用者不那么舒服的问题，那就是调用者要去准备这个done()函数，以及在回调函数中需要从结果中把数据一个一个提取出来，再进行处理。另一个方案则是来自笔者自己写的EventProxy模块，它是对事件订阅/发布模式的扩充，可以自由订阅组合事件。由于依旧采用的是事件订阅/发布模式，与Node十分契合，相关代码如下：[插图]EventProxy提供了一个all()方法来订阅多个事件，当每个事件都被触发之后，侦听器才会执行。另外的一个方法是tail()方法，它与all()方法的区别在于all()方法的侦听器在满足条件之后只会执行一次，tail()方法的侦听器则在满足条件时执行一次之后，如果组合事件中的某个事件被再次触发，侦听器会用最新的数据继续执行。

all()方法带来的另一个改进则是：在侦听器中返回数据的参数列表与订阅组合事件的事件列表是一致对应的。除此之外，在异步的场景下，我们常常需要从一个接口多次读取数据，此时触发的事件名或许是相同的。EventProxy提供了after()方法来实现事件在执行多少次后执行侦听器的单一事件组合订阅方式，示例代码如下：[插图]这段代码表示执行10次data事件后执行侦听器。这个侦听器得到的数据为10次按事件触发次序排序的数组。EventProxy模块除了可以应用于Node中外，还可以用在前端浏览器中。4. EventProxy的原理EventProxy来自于Backbone的事件模块，Backbone的事件模块是Model、View模块的基础功能，在前端有广泛的使用。它在每个非all事件触发时都会触发一次all事件，相关代码如下：

[插图]EventProxy则是将all当做一个事件流的拦截层，在其中注入一些业务来处理单一事件无法解决的异步处理问题。类似的扩展方法还有all()、tail()、after()、not()和any()等。5. EventProxy的异常处理EventProxy在事件发布/订阅模式的基础上还完善了异常处理。在异步方法中，异常处理需要占用一定比例的精力。在过去一段时间内，我们都是通过额外添加error事件来进行异常统一处理的，代码大致如下：[插图]因为异常处理的原因，代码量一下子多起来了，而EventProxy在实践过程中改进了这个问题，相关代码如下：[插图]在上述代码中，EventProxy提供了fail()和done()这两个实例方法来优化异常处理，使得开发者将精力关注在业务部分，而不是在异常捕获上。关于fail()方法的实现，可以参见以下的变换：[插图]上面这行代码等价于下面的代码：

[插图]又等价于：[插图]而done()方法的实现，也可参见以下的变换：[插图]它等价于：[插图]同时，done()方法也接受一个函数作为参数，相关代码如下所示：[插图]这段代码等价于：[插图]当只传入一个回调函数时，需要手工调用emit()触发事件。另一个改进是同时传入事件名和回调函数，相关代码如下：[插图]在这种方式下，我们无须在回调函数中处理事件的触发，只需将处理过的数据返回即可。返回的结果将在done()方法中用作事件的数据而触发。这里的fail()和done()十分类似Promise模式中的fail()和done()。换句话而言，这可以算作事件发布/订阅模式向Promise模式的借鉴。这样的完善既提升了程序的健壮性，同时也降低了代码量。4.3.2 Promise/Deferred模式使用事件的方式时，执行流程需要被预先设定。即便是分支，也需要预先设定，这是由发布/订阅模式的运行机制所决定的。下面为普通的Ajax调用：[插图]在上面的异步调用中，必须严谨地设置目标。那么是否有一种先执行异步调用，延迟传递处理的方式呢？答案是Promise/Deferred模式。Promise/Deferred模式在JavaScript框架中最早出现于Dojo的代码中，被广为所知则来自于jQuery 1.5版本，该版本几乎重写了Ajax部分，使得调用Ajax时可以通过如下的形式进行：

[插图]这使得即使不调用success()、error()等方法，Ajax也会执行，这样的调用方式比预先传入回调让人觉得舒适一些。在原始的API中，一个事件只能处理一个回调，而通过Deferred对象，可以对事件加入任意的业务处理逻辑，示例代码如下：[插图]Promise/Deferred模式在2009年时被Kris Zyp抽象为一个提议草案，发布在CommonJS规范中。随着使用Promise/Deferred模式的应用逐渐增多，CommonJS草案目前已经抽象出了Promises/A、Promises/B、Promises/D这样典型的异步Promise/Deferred模型，这使得异步操作可以以一种优雅的方式出现。异步的广度使用使得回调、嵌套出现，但是一旦出现深度的嵌套，就会让编程的体验变得不愉快，而Promise/Deferred模式在一定程度上缓解了这个问题。这里我们将着重介绍Promises/A来以点代面介绍Promise/Deferred模式。1. Promises/APromise/Deferred模式其实包含两部分，即Promise和Deferred。这里暂且不提两者的区别是什么，先看看Promises/A的行为吧。Promises/A提议对单个异步操作做出了这样的抽象定义，具体如下所示。❑ Promise操作只会处在3种状态的一种：未完成态、完成态和失败态。❑ Promise的状态只会出现从未完成态向完成态或失败态转化，不能逆反。完成态和失败态不能互相转化。❑ Promise的状态一旦转化，将不能被更改。Promise的状态转化示意图如图4-4所示。[插图]图4-4 Promise的状态转化示意图

在API的定义上，Promises/A提议是比较简单的。一个Promise对象只要具备then()方法即可。但是对于then()方法，有以下简单的要求。❑ 接受完成态、错误态的回调方法。在操作完成或出现错误时，将会调用对应方法。❑ 可选地支持progress事件回调作为第三个方法。❑ then()方法只接受function对象，其余对象将被忽略。❑ then()方法继续返回Promise对象，以实现链式调用。then()方法的定义如下：[插图]为了演示Promises/A提议，这里我们尝试通过继承Node的events模块来完成一个简单的实现，相关代码如下：[插图]这里看到then()方法所做的事情是将回调函数存放起来。为了完成整个流程，还需要触发执行这些回调函数的地方，实现这些功能的对象通常被称为Deferred，即延迟对象，示例代码如下：

[插图]这里的状态和方法之间的对应关系如图4-5所示。[插图]图4-5 状态和方法之间的对应关系利用Promises/A提议的模式，我们可以对一个典型的响应对象进行封装，相关代码如下：[插图]要实现如此简单的API，只需要简单地改造一下即可，相关代码如下：[插图]如此就得到了简单的结果。这里返回deferred.promise的目的是为了不让外部程序调用resolve()和reject()方法，更改内部状态的行为交由定义者处理。下面为定义好Promise后的调用示例：[插图]这里回到Promise和Deferred的差别上。从上面的代码可以看出，Deferred主要是用于内部，用于维护异步模型的状态；Promise则作用于外部，通过then()方法暴露给外部以添加自定义逻辑。Promise和Deferred的整体关系如图4-6所示。

[插图]图4-6 Promise和Deferred整体关系示意图与事件发布/订阅模式相比，Promise/Deferred模式的API接口和抽象模型都十分简洁。从图4-6中也可以看出，它将业务中不可变的部分封装在了Deferred中，将可变的部分交给了Promise。此时问题就来了，对于不同的场景，都需要去封装和改造其Deferred部分，然后才能得到简洁的接口。如果场景不常用，封装花费的时间与带来的简洁相比并不一定划算。Promise是高级接口，事件是低级接口。低级接口可以构成更多更复杂的场景，高级接口一旦定义，不太容易变化，不再有低级接口的灵活性，但对于解决典型问题非常有效。Promises/A的模型抽象在几种Promise提议中相对简洁。这里再介绍一下Q。Q模块是Promises/A规范的一个实现，可以通过npm install q进行安装使用。它对Node中常见回调函数的Promise实现如下：[插图]可以看到这里是一个高阶函数的使用，makeNodeResolver返回了一个Node风格的回调函数。对于fs.readFile()的调用，将会演化为如下形式：[插图]定义之后的调用示例如下：[插图]Promise通过封装异步调用，实现了正向用例和反向用例的分离以及逻辑处理延迟，这使得回调函数相对优雅。

前面分析了Q对Node异步回调的处理。事实上，异步编程中需要花费很多精力进行异常的判断和处理，为了分离异常和正常情况，我写了一个模块memeda用于处理makeNodeResolver相似的事情。在下面的调用示例中可以看到，正常结果和异常结果被分离到两个函数中：[插图]我们可以对Q和memeda模块略做比较。两者相似之处在于分离逻辑，使开发者侧重关注正常情况。不同之处在于Q通过promise()可以实现延迟处理，以及通过多次调用then()附加更多结果处理逻辑。可以看到，Promise需要封装，但是强大，具备很强的侵入性；纯粹的函数则较为轻量，但功能相对弱小。2. Promise中的多异步协作在Promise的介绍中说过，主要解决的是单个异步操作中存在的问题。回到我们的难点，当我们需要处理多个异步调用时，又该如何处理呢？类似于EventProxy，这里给出了一个简单的原型实现，相关代码如下：[插图]对于多次文件的读取场景，以下面的代码为例，all()方法将两个单独的Promise重新抽象组合成一个新的Promise：[插图]这里通过all()方法抽象多个异步操作。只有所有异步操作成功，这个异步操作才算成功，一旦其中一个异步操作失败，整个异步操作就失败。

本节的代码主要用于描述Promise的原理，在成熟度上并未如when和Q模块。在实际的应用中，可以通过NPM安装这两个模块，它们是完整的Promise提议的实现。3. Promise的进阶知识在API的暴露上，Promise模式比原始的事件侦听和触发略为优美，它的缺陷则是需要为不同的场景封装不同的API，没有直接的原生事件那么灵活。但对于经典的场景，封装出API的成本也并不高，值得一做。Promise的秘诀其实在于对队列的操作。这里介绍一个实际的案例，我在处理自动化测试时，要跟远程服务器之间进行多次指令发送，这些指令是按顺序依次进行的。在Node中，网络库是完全异步的，无法在编程层面实现像其他语言那般的同步调用。由于网站界面通常都是由前端工程师完成的，用JavaScript编写自动化测试可以减轻他们切换环境的痛苦，所以不能因为无法同步调用就放弃掉Node。解决同步调用问题的答案也就是采用Deferred模式。现在有一组纯异步的API，为了完成一串事情，我们的代码大致如下：[插图]由于有按每个步骤依次执行的需求，所以必须嵌套执行。但那样我们会得到难看的嵌套，超过10个连续嵌套就会让代码十分难看。于是我们得到了“Pyramid ofDoom”，译为中文，是谓“恶魔金字塔”。相信初入Node世界的人，也写过不少此类代码。

下面我们通过普通的函数将上面的代码尝试展开：[插图]对于喜欢利用事件的开发者，我们展开后的代码又将会是怎样的情况呢？具体如下所示：[插图]利用事件展开后的效果变得越来越糟糕了。与纯粹嵌套相比，代码量明显增加了，这显然不会带来良好的编程体验。为此，我们需要一种更好的方式。●支持序列执行的Promise理想的编程体验应当是前一个的调用结果作为下一个调用的开始，是传说中的链式调用，相关代码如下：[插图]尝试改造一下代码以实现链式调用，具体如下所示：[插图]这里我们以两次文件读取作为例子，以验证该设计的可行性。这里假设读取第二个文件是依赖于第一个文件中的内容的，相关代码如下：

[插图]将这段代码存为sequence.js文件。执行该代码，将会得到以下的输出结果：[插图]要让Promise支持链式执行，主要通过以下两个步骤。(1) 将所有的回调都存到队列中。(2) Promise完成时，逐个执行回调，一旦检测到返回了新的Promise对象，停止执行，然后将当前Deferred对象的promise引用改变为新的Promise对象，并将队列中余下的回调转交给它。写到这里，你是否明了恶魔金字塔该如何优化？再次重申，这里的代码主要用于研究Promise的实现原理。在更多细节的优化方面，Q或者when等Promise库做得更好，实际应用时请采用这些成熟库。●将API Promise化这里仍然会发现，为了体验更好的API，需要做较多的准备工作。这里提供了一个方法可以批量将方法Promise化，相关代码如下：[插图]于是前面的两次文件读取的构造：[插图]可以简化为：[插图]要实现同样的效果，代码量将会锐减到：[插图]4.3.3 流程控制库

前面叙述了最为主流的模式——事件发布/订阅模式和Promise/Deferred模式，这些是经典的模式或者是写进规范里的解决方案，但一旦涉及模式或者规范，就需要为它们做较多的准备工作。这一节将会介绍一些非模式化的应用，虽非规范，但更灵活。1．尾触发与Next除了事件和Promise外，还有一类方法是需要手工调用才能持续执行后续调用的，我们将此类方法叫做尾触发，常见的关键词是next。事实上，尾触发目前应用最多的地方是Connect的中间件。这里我们暂且不关注Connect的具体应用，先看一下Connect的API暴露方式，相关代码如下：[插图]在通过use()方法注册好一系列中间件后，监听端口上的请求。中间件利用了尾触发的机制，最简单的中间件如下：[插图]每个中间件传递请求对象、响应对象和尾触发函数，通过队列形成一个处理流，如图4-7所示。[插图]图4-7 中间件通过队列形成一个处理流中间件机制使得在处理网络请求时，可以像面向切面编程一样进行过滤、验证、日志等功能，而不与具体业务逻辑产生关联，以致产生耦合。下面我们来看Connect的核心实现，相关代码如下：[插图]这段代码通过如下代码创建了HTTP服务器的request事件处理函数：

[插图]但真正的核心代码是app.stack = []；这句。stack属性是这个服务器内部维护的中间件队列。通过调用use()方法我们可以将中间件放进队列中。下面的代码为use()方法的重要部分：[插图]此时就建好处理模型了。接下来，结合Node原生http模块实现监听即可。监听函数的实现如下：[插图]最终回到app.handle()方法，每一个监听到的网络请求都将从这里开始处理。该方法的代码如下：[插图]原始的next()方法较为复杂，下面是简化后的内容，其原理十分简单，取出队列中的中间件并执行，同时传入当前方法以实现递归调用，达到持续触发的目的：[插图]所有嫌异步编程复杂的开发者均可以参考Connect的流式处理，这对于划分业务逻辑、逐步处理均有效。

值得提醒的是，尽管中间件这种尾触发模式并不要求每个中间方法都是异步的，但是如果每个步骤都采用异步来完成，实际上只是串行化的处理，没办法通过并行的异步调用来提升业务的处理效率。流式处理可以将一些串行的逻辑扁平化，但是并行逻辑处理还是需要搭配事件或者Promise完成的，这样业务在纵向和横向都能够各自清晰。在Connect中，尾触发十分适合处理网络请求的场景。将复杂的处理逻辑拆解为简洁、单一的处理单元，逐层次地处理请求对象和响应对象。2. async接下来，我们要介绍最知名的流程控制模块async。async长期占据NPM依赖榜的前三名，可见在Node开发中，流程控制是开发过程中的基本需求。async模块提供了20多个方法用于处理异步的各种协作模式，这里我们介绍几种典型用法。●异步的串行执行这里我们依旧采用前面读取两个文件的例子，看一下async是如何解决“恶魔金字塔”问题的。async提供了series()方法来实现一组任务的串行执行，示例代码如下：[插图]这段代码等价于：

[插图]这段代码值得玩味的是回调函数。可以发现，series()方法中传入的函数callback()并非由使用者指定。事实上，此处的回调函数由async通过高阶函数的方式注入，这里隐含了特殊的逻辑。每个callback()执行时会将结果保存起来，然后执行下一个调用，直到结束所有调用。最终的回调函数执行时，队列里的异步调用保存的结果以数组的方式传入。这里的异常处理规则是一旦出现异常，就结束所有调用，并将异常传递给最终回调函数的第一个参数。●异步的并行执行当我们需要通过并行来提升性能时，async提供了parallel()方法，用以并行执行一些异步操作。以下为读取两个文件的并行版本：[插图]上面这段代码等价于下面的代码：[插图]同样，通过async编写的代码既没有深度的嵌套，也没有复杂的状态判断，它的诀窍依然来自于注入的回调函数。parallel()方法对于异常的判断依然是一旦某个异步调用产生了异常，就会将异常作为第一个参数传入给最终的回调函数。只有所有异步调用都正常完成时，才会将结果以数组的方式传入。

也许你还记得EventProxy的方案，如下所示：[插图]与通过async编写所产生的代码量相差并不大。EventProxy虽然基于事件发布/订阅模式而设计，但也用到了与async相同的原理，通过特殊的回调函数来隐含返回值的处理。所不同的是，在async的框架模式下，这个回调函数由async封装后传递出来，而EventProxy则通过done()和fail()方法来生成新的回调函数。这两种实现方式都是高阶函数的应用。●异步调用的依赖处理series()适合无依赖的异步串行执行，但当前一个的结果是后一个调用的输入时，series()方法就无法满足需求了。所幸，这种典型场景的需求，async提供了waterfall()方法来满足，相关代码如下：[插图]这段代码等价于如下代码：[插图]●自动依赖处理在现实的业务环境中，具有很多复杂的依赖关系，这些业务或是异步，或是同步。这种混杂的编程环境经常让人处于理不清顺序的情况。为此，async提供了一个强大的方法auto()实现复杂业务处理。

假设我们的业务场景如下：(1) 从磁盘读取配置文件。(2) 根据配置文件连接MongoDB。(3) 根据配置文件连接Redis。(4) 编译静态文件。(5) 上传静态文件到CDN。(6) 启动服务器。简单映射一下上述业务：[插图]接下来分析一下依赖关系。可以看出，connectMongoDB和connectRedis依赖readConfig, uploadAsserts依赖complieAsserts, startup则依赖所有完成。依赖关系如下：[插图]auto()方法能根据依赖关系自动分析，以最佳的顺序执行以上业务：[插图]转换到EventProxy的实现，则需要更细腻的事件分配，相关代码如下：[插图]●小结本节主要介绍async的几种常见用法。此外，async还提供了forEach、map等类ECMAScript5中数组的方法，更多细节可关注https://github.com/caolan/async。3. Step另一个知名的流程控制库是Tim Caswell的Step，它比async更轻量，在API的暴露上也更具备一致性，因为它只有一个接口Step。通过npm install step即可安装使用。示例代码如下：

[插图]Step接受任意数量的任务，所有的任务都将会串行依次执行。下面的示例代码将依次读取文件：[插图]可以看到，Step与前面介绍的事件模式、Promise甚至async都不同的一点在于Step用到了this关键字。事实上，它是Step内部的一个next()方法，将异步调用的结果传递给下一个任务作为参数，并调用执行。●并行任务执行那么，Step如何实现多个异步任务并行执行呢？this具有一个parallel()方法，它告诉Step，需要等所有任务完成时才进行下一个任务，相关代码如下：[插图]使用parallel()的时候需要小心的是，如果异步方法的结果传回的是多个参数，Step将只会取前两个参数，相关代码如下：[插图]在调用parallel()时，result2将会被丢弃。Step的parallel()方法的原理是每次执行时将内部的计数器加1，然后返回一个回调函数，这个回调函数在异步调用结束时才执行。当回调函数执行时，将计数器减1。当计数器为0的时候，告知Step所有异步调用结束了，Step会执行下一个方法。Step与async相同的是异常处理，一旦有一个异常产生，这个异常会作为下一个方法的第一个参数传入。

●结果分组Step提供的另外一个方法是group()，它类似于parallel()的效果，但是在结果传递上略有不同。下面的代码用于读取一个目录，然后迭代其中文件的操作：[插图]我们注意到有两次group()的调用。第一次调用是告知Step要并行执行，第二次调用的结果将会生成一个回调函数，而回调函数接受的返回值将会按组存储。parallel()传递给下一个任务的结果是如下形式：[插图]group()传递的结果是：[插图]这个函数返回的数据保存在数组中。4. wind这里还要介绍一种思路完全不同的异步编程方案wind（https://github.com/JeffreyZhao/wind）。它的前身为Jscex，由国内知名码农赵劼完成开发。它为JavaScript语言提供了一个monadic扩展，能够显著提高一些常见场景下的异步编程体验。异步编程有时需要面临的场景非常特殊，下面我们由一个冒泡排序来了解wind的特殊之处：[插图]现在我们要添加的需求是，将这个冒泡排序动画起来。这意味着在swap()方法中需要添加动画逻辑，这在JavaScript中并不是一件难事，困难的地方在于动画需要延时的方式完成。但在JavaScript中只有setTimeout()能够实现延时功能（用while判断时间的方式不可取，这在前面有所描述）。我们知道，setTimeout()是一个异步方法，在执行后，将立即返回。所以，难点出现在：

❑ 动画执行时无法停止排序算法的执行；❑ 排序算法的继续执行将会启动更多动画。因此，逐步骤的动画将难以实现，而wind在解决这个问题上体现出了它的独特魅力之处，相关代码如下：[插图]上述代码实现了暂停20毫秒、绘制动画、继续排序的效果。从代码的角度来说，这里虽然介入了异步方法，但是并没有如同其他异步流程控制库那样变得异步化，逻辑并没有因为异步被拆分。同时可以注意到，我们的代码中引入了一些新的东西：❑ eval(Wind.compile("async", function() {}));❑ $await();❑ Wind.Async.sleep(20);下面我们将详细介绍以上3行代码的特异之处。●异步任务定义eval()函数在业界一向是一个需要谨慎对待的函数，Douglas Crockford更是深恶痛绝地将其称为魔鬼，因为它能访问上下文和编译器，可能导致上下文混乱。大多数利用eval()函数的人都不能把握好它的用法，导致Douglas Crockford认为它是JavaScript可有可无的功能。但是在wind的世界里，恰好反Douglas Crockford之道而行之，巧妙地利用了eval()访问上下文的特性。Wind.compile()会将普通的函数进行编译，然后交给eval()执行。换言之，eval(Wind.compile("async", function () {}))；定义了异步任务。Wind.Async.sleep()；则内置了对setTimeout()的封装。●$await()与任务模型

在定义完异步方法后，wind提供了$await()方法实现等待完成异步方法。但事实上，它并不是一个方法，也不存在于上下文中，只是一个等待的占位符，告之编译器这里需要等待。$await()接受的参数是一个任务对象，表示等待任务结束后才会执行后续操作。每一个异步操作都可以转化为一个任务，wind正是基于任务模型实现的。下面的代码用于将fs.readFile()调用转化为一个任务模型：[插图]除了通过eval(Wind.compile("async", function () {}))；定义任务外，正式的任务创建方法为Task.create()。执行readFileAsync()进行偏函数转换得到真正的任务。异步方法在执行结束时，可以通过complete()传递failure或success信息，告知任务执行完毕。如果是failure则可以通过try/catch捕获异常。这略微有些打破前述try/catch无法捕获回调函数中异常的定论。下面的代码为调用readFileAsync()得到一个任务的示例：[插图]下面我们如同介绍async或者Step的串行执行示例一样，尝试感受一下wind的风采：[插图]执行上述代码，将得到如下输出：[插图]异步方法在JavaScript中通常会立即返回，在wind中做到了不阻塞CPU但阻塞代码的目的。接下来我们尝试下并行的效果，相关代码如下：

[插图]得到输出：[插图]wind提供了whenAll()来处理并发，通过$await关键字将等待配置的所有任务完成后才向下继续执行。●异步方法转换辅助函数可以看到，除了eval(Wind.compile("async", function () {}))在实际代码中稍显冗长外，异步调用在代码层面上已经与同步调用相差无几。这十分适合从已有的采用同步编写方式的代码向Node迁移，可以省掉重写代码的开销。如同Promise/Deferred模式可以让异步编程模型变简单，这种近同步编程的体验需要我们额外或者提前完成的事情是：将异步方法任务化。这种任务化的过程可以看作是Promise/Deferred的封装。如果每个方法都如readFileAsync一般去定义，将会是一个庞大的工作量。wind提供了两个方法来辅助转换：❑ Wind.Async.Binding.fromCallback❑ Wind.Async.Binding.fromStandard在Node中异步方法的回调传值有两种，一种是无异常的调用，通常只有一个参数返回，如下所示：[插图]而fromCallback用于转换这类异步调用为wind中的任务。另一类是带异常的调用，遵循规范将返回参数列表的第一个参数作为异常标示，如下所示：[插图]而fromStandard用于转换这类异步调用到wind中的任务。是故，readFileAsync的定义其实只要一行代码即可实现：

[插图]5．流程控制小结从本书介绍的各个流程控制案例来看，从解决“恶魔金字塔”到解决异步协作的方法有多种，几个类库几乎各显神通。异步编程虽然相对复杂，但并非难事，相同的问题通过各种技巧依然能将复杂的事情简化。这里简单对比下几种方案的区别：事件发布/订阅模式相对算是一种较为原始的方式，Promise/Deferred模式贡献了一个非常不错的异步任务模型的抽象。而上述的这些异步流程控制方案与Promise/Deferred模式的思路不同，Promise/Deferred的重头在于封装异步的调用部分，流程控制库则显得没有模式，将处理重点放置在回调函数的注入上。从自由度上来讲，async、Step这类流控库要相对灵活得多。EventProxy库则主要借鉴事件发布/订阅模式和流程控制库通过高阶函数生成回调函数的方式实现。除了async、Step、EventProxy、wind等方案外，还有一类通过源代码编译的方案来实现流程控制的简化，streamline是典型的例子。这类例子并不在本章的讨论范围内，如果读者有兴趣，可以自行查阅相关资料。


## 4.4 异步并发控制

在陆续介绍的各种异步编程方法里，解决的问题无外乎保持异步的性能优势，提升编程体验，但是这里有一个过犹不及的案例。在Node中，我们可以十分方便地利用异步发起并行调用。使用下面的代码，我们可以轻松发起100次异步调用：[插图]但是如果并发量过大，我们的下层服务器将会吃不消。如果是对文件系统进行大量并发调用，操作系统的文件描述符数量将会被瞬间用光，抛出如下错误：[插图]可以看出，异步I/O与同步I/O的显著差距：同步I/O因为每个I/O都是彼此阻塞的，在循环体中，总是一个接着一个调用，不会出现耗用文件描述符太多的情况，同时性能也是低下的；对于异步I/O，虽然并发容易实现，但是由于太容易实现，依然需要控制。换言之，尽管是要压榨底层系统的性能，但还是需要给予一定的过载保护，以防止过犹不及。4.4.1 bagpipe的解决方案如何对既有的异步API添加过载保护，我们期望的当然不是去改动API。那么如何实现呢？我写的bagpipe模块的解决思路是这样的。

❑ 通过一个队列来控制并发量。❑ 如果当前活跃（指调用发起但未执行回调）的异步调用量小于限定值，从队列中取出执行。❑ 如果活跃调用达到限定值，调用暂时存放在队列中。❑ 每个异步调用结束时，从队列中取出新的异步调用执行。bagpipe的API主要暴露了一个push()方法和full事件，示例代码如下：[插图]这里的实现细节类似于前文的smooth()。push()方法依然是通过函数变换的方式实现，假设第一个参数是方法，最后一个参数是回调函数，其余为其他参数，其核心实现如下：[插图]将调用推入队列后，调用一次next()方法尝试触发。next()方法的定义如下：

[插图]next()方法主要判断活跃调用的数量，如果正常，将调用内部方法run()来执行真正的调用。这里为了判断回调函数是否执行，采用了一个注入代码的技巧，具体代码如下：[插图]用户传入的回调函数被真正执行前，被封装替换过。这个封装的回调函数内部的逻辑将活跃值的计数器减1后，主动调用next()执行后续等待的异步调用。bagpipe类似于打开了一道窗口，允许异步调用并行进行，但是严格限定上限。仅仅在调用push()时分开传递，并不对原有API有任何侵入。

●拒绝模式事实上，bagpipe还有一些深度的使用方式。对于大量的异步调用，也需要分场景进行区分，因为涉及并发控制，必然会造成部分调用需要进行等待。如果调用有实时方面的需求，那么需要快速返回，因为等到方法被真正执行时，可能已经超过了等待时间，即使返回了数据，也没有意义了。这种场景下需要快速失败，让调用方尽早返回，而不用浪费不必要的等待时间。bagpipe为此支持了拒绝模式。拒绝模式的使用只要设置下参数即可，相关代码如下：[插图]在拒绝模式下，如果等待的调用队列也满了之后，新来的调用就直接返给它一个队列太忙的拒绝异常。●超时控制造成队列拥塞的主要原因是异步调用耗时太久，调用产生的速度远远高于执行的速度。为了防止某些异步调用使用了太多的时间，我们需要设置一个时间基线，将那些执行时间太久的异步调用清理出活跃队列，让排队中的异步调用尽快执行。否则在拒绝模式下，会有太多的调用因为某个执行得慢，导致得到拒绝异常。相对而言，这种场景下得到拒绝异常显得比较无辜。为了公平地对待在实时需求场景下的每个调用，必须要控制每个调用的执行时间，将那些害群之马踢出队伍。

为此，bagpipe也提供了超时控制。超时控制是为异步调用设置一个时间阈值，如果异步调用没有在规定时间内完成，我们先执行用户传入的回调函数，让用户得到一个超时异常，以尽早返回。然后让下一个等待队列中的调用执行。超时的设置如下：[插图]●小结异步调用的并发限制在不同场景下的需求不同：非实时场景下，让超出限制的并发暂时等待执行已经可以满足需求；但在实时场景下，需要更细粒度、更合理的控制。4.4.2 async的解决方案无独有偶，async也提供了一个方法用于处理异步调用的限制：parallelLimit()。如下是async的示例代码：[插图]parallelLimit()与parallel()类似，但多了一个用于限制并发数量的参数，使得任务只能同时并发一定数量，而不是无限制并发。parallelLimit()方法的缺陷在于无法动态地增加并行任务。为此，async提供了queue()方法来满足该需求，这对于遍历文件目录等操作十分有效。以下是queue()的示例代码：[插图]尽管queue()实现了动态添加并行任务，但是相比parallelLimit()，由于queue()接收的参数是固定的，它丢失了parallelLimit()的多样性，我私心地认为bagpipe更灵活，可以添加任意类型的异步任务，也可以动态添加异步任务，同时还能够在实时处理场景中加入拒绝模式和超时控制。在实际应用中，开发者可以根据场景进行取舍。

## 4.5 总结

在接触Node的过程中，很多人粗略地接触了几个回调函数之后就放弃了。尽管异步编程略微艰难，但是并非一无是处，一旦习惯，就显得自然。从社区和过往的经验而言，JavaScript异步编程的难题已经基本解决，无论是通过事件，还是通过Promise/Deferred模式，或者流程控制库。相信在掌握以上技巧之后，异步编程不是难事，习惯异步编程之后，将会收获许多值得享受的编程体验。本章主要介绍了主流的几种异步编程解决方案，这是目前JavaScript中主要使用的方案。但对于其他语言而言，还有协程（coroutine）等方式。但是由于Node基于V8的原因，在目前EMCAScript5的实现下还不支持协程。这些标准和规范还在制定中，所以暂时不作介绍。未来的V8如果支持Generator，也将在Node中能直接使用。最后，因为人们总是习惯性地以线性的方式进行思考，以致异步编程相对较为难以掌握。这个世界以异步运行的本质是不会因为大家线性思维的惯性而改变。就像日出月落不会因为你的心情而改变其自有的运行轨迹。

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


## 5.1 V8 的垃圾回收机制与内存限制


## 5.2 高效使用内存


## 5.3 内存指标


## 5.4 内存泄漏


## 5.5 内存泄漏排查


## 5.6 大内存应用


## 5.7 总结


## 5.8 参考资源

本章参考的资源如下：

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


## 6.1 Buffer 结构


## 6.2 Buffer 的转换


## 6.3 Buffer 的拼接


## 6.4 Buffer 与性能


## 6.5 总结


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


## 7.1 构建 TCP 服务


## 7.2 构建 UDP 服务


## 7.3 构建 HTTP 服务



## 7.4 构建 WebSocket 服务


## 7.5 网络服务与安全


## 7.6 总结


## 7.7 参考资源

本章参考的资源如下：

- http://tools.ietf.org/html/rfc2616
- http://hi.baidu.com/miracletan2008/item/0bc16c9d7af261de7b7f01a2
- http://tools.ietf.org/html/rfc6455
- http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
- http://en.wikipedia.org/wiki/OSI_model
- http://upload.wikimedia.org/wikipedia/commons/a/ae/SSL_handshake_with_two_way_authentication_with_certificates.svg

# 第 8 章 构建 Web 应用


## 8.1 基础功能


## 8.2 数据上传


## 8.3 路由解析


## 8.4 中间件


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
