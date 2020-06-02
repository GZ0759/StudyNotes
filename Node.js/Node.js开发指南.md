> Node.js开发指南  
> 2012年7月第一版  
> 作者:：郭家宝（BYVoid）  

# 第一章 Node.js简介

Node.js，或者 Node，是一个可以让 JavaScript 运行在服务器端的平台。它可以让JavaScript 脱离浏览器的束缚运行在一般的服务器环境下，就像运行 Python、 Perl、 PHP、 Ruby 程序一样。你可以用 Node.js 轻松地进行服务器端应用开发， Python、 Perl、 PHP、 Ruby 能做的事情 Node.js 几乎都能做，而且可以做得更好。

Node.js 是一个为实时Web（ Real-time Web）应用开发而诞生的平台，它从诞生之初就充分考虑了在实时响应、超大规模数据要求下架构的可扩展性。这使得它摒弃了传统平台依靠多线程来实现高并发的设计思路，而采用了单线程、异步式I/O、事件驱动式的程序设计模型。这些特性不仅带来了巨大的性能提升，还减少了多线程程序设计的复杂性，进而提高了开发效率。

Node.js 最初是由 Ryan Dahl 发起的开源项目，后来被 Joyent 公司注意到。 Joyent 公司将 Ryan Dahl 招入旗下，因此现在的 Node.js 由 Joyent 公司管理并维护。尽管它诞生的时间（ 2009年）还不长，但它的周围已经形成了一个庞大的生态系统。 Node.js 有着强大而灵活的包管理器（ node package manager， npm），目前已经有上万个第三方模块，其中有网站开发框架，有 MySQL、 PostgreSQL、 MongoDB 数据库接口，有模板语言解析、 CSS 生成工具、邮件、加密、图形、调试支持，甚至还有图形用户界面和操作系统 API工具。由 VMware 公司建立的云计算平台 Cloud Foundry 率先支持了 Node.js。 2011年6月，微软宣布与 Joyent 公司合作，将 Node.js 移植到 Windows，同时 Windows Azure 云计算平台也支持 Node.js。 Node.js 目前还处在迅速发展阶段，相信在不久的未来它一定会成为流行的Web应用开发平台。让我们从现在开始，一同探索 Node.js 的美妙世界吧！

## 1.1 Node.js 是什么 

Node.js 不是一种独立的语言，与 PHP、 Python、 Perl、 Ruby 的“既是语言也是平台”不同。 Node.js 也不是一个 JavaScript 框架，不同于 CakePHP、 Django、 Rails。 Node.js 更不是浏览器端的库，不能与 jQuery、 ExtJS 相提并论。 Node.js 是一个让 JavaScript 运行在服务端的开发平台，它让 JavaScript 成为脚本语言世界的一等公民，在服务端堪与 PHP、 Python、 Perl、 Ruby 平起平坐。

Node.js 是一个划时代的技术，它在原有的 Web 前端和后端技术的基础上总结并提炼出了许多新的概念和方法，堪称是十多年来 Web 开发经验的集大成者。 Node.js 可以作为服务器向用户提供服务，与 PHP、 Python、 Ruby on Rails 相比，它跳过了 Apache、 Nginx 等 HTTP 服务器，直接面向前端开发。 Node.js 的许多设计理念与经典架构（如 LAMP）有着很大的不同，可提供强大的伸缩能力，以适应21世纪10年代以后规模越来越庞大的互联网环境。

Node.js 与 JavaScript

说起 JavaScript，不得不让人想到浏览器。传统意义上， JavaScript 是由 ECMAScript、文档对象模型（ DOM）和浏览器对象模型（ BOM）组成的，而 Mozilla 则指出 JavaScript 由 Core JavaScript 和 Client JavaScript 组成。之所以会有这种分歧，是因为 JavaScript 和浏览器之间复杂的历史渊源，以及其命途多舛的发展历程所共同造成的，我们会在后面详述。我们可以认为， Node.js 中所谓的 JavaScript 只是 Core JavaScript，或者说是 ECMAScript 的一个实现，不包含 DOM、 BOM 或者 Client JavaScript。这是因为 Node.js 不运行在浏览器中，所以不需要使用浏览器中的许多特性。

Node.js 是一个让 JavaScript 运行在浏览器之外的平台。它实现了诸如文件系统、模块、包、操作系统 API、网络通信等 Core JavaScript 没有或者不完善的功能。历史上将 JavaScript 移植到浏览器外的计划不止一个，但 Node.js 是最出色的一个。随着 Node.js 的成功，各种浏览器外的 JavaScript 实现逐步兴起，因此产生了 CommonJS 规范。 CommonJS 试图拟定一套完整的 JavaScript 规范，以弥补普通应用程序所需的 API，譬如文件系统访问、命令行、模块管理、函数库集成等功能。 CommonJS 制定者希望众多服务端 JavaScript 实现遵循CommonJS 规范，以便相互兼容和代码复用。 Node.js 的部份实现遵循了CommonJS规范，但由于两者还都处于诞生之初的快速变化期，也会有不一致的地方。

Node.js 的 JavaScript 引擎是 V8，来自 Google Chrome 项目。 V8 号称是目前世界上最快的 JavaScript 引擎，经历了数次引擎革命，它的 JIT（ Just-in-time Compilation，即时编译）执行速度已经快到了接近本地代码的执行速度。 Node.js 不运行在浏览器中，所以也就不存在 JavaScript 的浏览器兼容性问题，你可以放心地使用 JavaScript 语言的所有特性。

## 1.2 Node.js 能做什么 

正如 JavaScript 为客户端而生， Node.js 为网络而生。 Node.js 能做的远不止开发一个网站那么简单，使用 Node.js，你可以轻松地开发：

- 具有复杂逻辑的网站；
- 基于社交网络的大规模 Web 应用；
- Web Socket 服务器；
- TCP/UDP 套接字应用程序；
- 命令行工具；
- 交互式终端程序；
- 带有图形用户界面的本地应用程序；
- 单元测试工具；
- 客户端 JavaScript 编译器。

Node.js 内建了 HTTP 服务器支持，也就是说可以轻而易举地实现一个网站和服务器的组合。这和 PHP、 Perl 不一样，因为在使用 PHP 的时候，必须先搭建一个 Apache 之类的HTTP 服务器，然后通过 HTTP 服务器的模块加载或 CGI 调用，才能将 PHP 脚本的执行结果呈现给用户。而当你使用 Node.js 时，不用额外搭建一个 HTTP 服务器，因为 Node.js 本身就内建了一个。这个服务器不仅可以用来调试代码，而且它本身就可以部署到产品环境，它的性能足以满足要求。

Node.js 还可以部署到非网络应用的环境下，比如一个命令行工具。 Node.js 还可以调用C/C++ 的代码，这样可以充分利用已有的诸多函数库，也可以将对性能要求非常高的部分用、C/C++ 来实现。

## 1.3 异步式 I/O 与事件驱动 

Node.js 最大的特点就是采用异步式 I/O 与事件驱动的架构设计。对于高并发的解决方案，传统的架构是多线程模型，也就是为每个业务逻辑提供一个系统线程，通过系统线程切换来弥补同步式 I/O 调用时的时间开销。 Node.js 使用的是单线程模型，对于所有 I/O 都采用异步式的请求方式，避免了频繁的上下文切换。 Node.js 在执行的过程中会维护一个事件队列，程序在执行时进入事件循环等待下一个事件到来，每个异步式 I/O 请求完成后会被推送到事件队列，等待程序进程进行处理。

例如，对于简单而常见的数据库查询操作，按照传统方式实现的代码如下：

```js
res = db.query('SELECT * from some_table');
res.output();
```

以上代码在执行到第一行的时候，线程会阻塞，等待数据库返回查询结果，然后再继续处理。然而，由于数据库查询可能涉及磁盘读写和网络通信，其延时可能相当大（长达几个到几百毫秒，相比CPU的时钟差了好几个数量级），线程会在这里阻塞等待结果返回。对于高并发的访问，一方面线程长期阻塞等待，另一方面为了应付新请求而不断增加线程，因此会浪费大量系统资源，同时线程的增多也会占用大量的 CPU 时间来处理内存上下文切换，而且还容易遭受低速连接攻击。

看看 Node.js 是如何解决这个问题的：

```js
db.query('SELECT * from some_table', function(res) {
  res.output();
});
```

这段代码中 db.query 的第二个参数是一个函数，我们称为回调函数。进程在执行到 db.query 的时候，不会等待结果返回，而是直接继续执行后面的语句，直到进入事件循环。当数据库查询结果返回时，会将事件发送到事件队列，等到线程进入事件循环以后，才会调用之前的回调函数继续执行后面的逻辑。

Node.js 的异步机制是基于事件的，所有的磁盘 I/O、网络通信、数据库查询都以非阻塞的方式请求，返回的结果由事件循环来处理。图1-1 描述了这个机制。 Node.js 进程在同一时刻只会处理一个事件，完成后立即进入事件循环检查并处理后面的事件。这样做的好处是，CPU 和内存在同一时间集中处理一件事，同时尽可能让耗时的 I/O 操作并行执行。对于低速连接攻击， Node.js 只是在事件队列中增加请求，等待操作系统的回应，因而不会有任何多线程开销，很大程度上可以提高 Web 应用的健壮性，防止恶意攻击。

这种异步事件模式的弊端也是显而易见的，因为它不符合开发者的常规线性思路，往往需要把一个完整的逻辑拆分为一个个事件，增加了开发和调试难度。针对这个问题， Node.js 第三方模块提出了很多解决方案，我们会在第6章中详细讨论。

## 1.4 Node.js 的性能 

1.4.1 Node.js 架构简介

Node.js 用异步式 I/O 和事件驱动代替多线程，带来了可观的性能提升。 Node.js 除了使用 V8 作为JavaScript引擎以外，还使用了高效的 libev 和 libeio 库支持事件驱动和异步式 I/O。

图1-2 是 Node.js 架构的示意图。

Node.js 的开发者在 libev 和 libeio 的基础上还抽象出了层 libuv。对于 POSIX 操作系统，libuv 通过封装 libev 和 libeio 来利用 epoll 或 kqueue。而在 Windows 下， libuv 使用了 Windows的 IOCP（ Input/Output Completion Port，输入输出完成端口）机制，以在不同平台下实现同样的高性能。

1.4.2 Node.js 与 PHP + Nginx

Snoopyxd 详细对比了 Node.js 与 PHP+Nginx 组合，结果显示在3000并发连接、 30秒的测试下，输出“hello world”请求：

- PHP 每秒响应请求数为3624，平均每个请求响应时间为0.39秒；
- Node.js 每秒响应请求数为7677，平均每个请求响应时间为0.13秒。而同样的测试，对MySQL查询操作：
- PHP 每秒响应请求数为1293，平均每个请求响应时间为0.82秒；
- Node.js 每秒响应请求数为2999，平均每个请求响应时间为0.33秒。

关于 Node.js 的性能优化及生产部署，我们会在第6章详细讨论。

## 1.5 JavaScript 简史

作为 Node.js 的基础， JavaScript 是一个完全为网络而诞生的语言。在今天看来， JavaScript 具有其他诸多语言不具备的优势，例如速度快、开销小、容易学习等，但在一开始它却并不是这样。多年以来， JavaScript 因为其低效和兼容性差而广受诟病，一直是一个被人嘲笑的“丑小鸭”，它在成熟之前经历了无数困难和坎坷，个中究竟，还要从它的诞生讲起。

1.5.1 Netscape 与 LiveScript

JavaScript 首次出现在1995年，正如现在的 Node.js 一样，当年 JavaScript 的诞生决不是偶然的。在1992年，一个叫 Nombas 的公司开发了“C减减”（ C minus minus， Cmm）语言，后来改名为 ScriptEase。 ScriptEase 最初的设计是将一种微型脚本语言与一个叫做 Espresso Page 的工具配合，使脚本能够在浏览器中运行，因此 ScriptEase 成为了第一个客户端脚本语言。

网景公司也想独立开发一种与 ScriptEase 相似的客户端脚本语言， Brendan Eich①接受了这一任务。起初这个语言的目标是为非专业的开发人员（如网站设计者），提供一个方便的工具。大多数网站设计者没有任何编程背景，因此这个语言应该尽可能简单、易学，最终一个弱类型的动态解释语言 LiveWire 就此诞生。 LiveWire 没过多久就改名为 LiveScript 了，直到现在，在一些古老的 Web 页面中还能看到这个名字。

1.5.2 Java 与 Javascript

在JavaScript 诞生之前， Java applet 曾经被热炒。之前 Sun 公司一直在不遗余力地推广Java，宣称 Java applet 将会改变人们浏览网页的方式。然而市场并没有像 Sun 公司预期的那样好，这很大程度上是因为 Java applet 速度慢而且操作不便。网景公司的市场部门抓住了这个机遇，与 Sun 合作完成了 LiveScript 实现，并在网景的Navigator 2.0 发布前，将 LiveScript 更名为 JavaScript。网景公司为了取得 Sun 公司的支持，把 JavaScript 称为 Java applet 和 HTML 的补充工具，目的之一就是为了帮助开发者更好地操纵 Java applet。

Netscape 决不会预料到当年那个市场策略带来的副作用有多大。多年来，到处都有人混淆 Java 和 JavaScript 这两个不相干的语言。两者除了名字相似和历史渊源之外，几乎没有任何关系。现在看来，从论坛到邮件列表，从网站到图书馆，能把 Java 和 JavaScript 区分开的倒是少数。图1-3 是百度知道上的“Java 相关”分类。

1.5.3 微软的加入—— JScript

就在网景公司如日中天之时，微软的 Internet Explorer 3 随 Windows 95 OSR2 捆绑销售的策略堪称一颗重磅炸弹，轻松击败了强劲的对手——网景公司的Navigator。尽管这个做法致使微软后来声名狼藉（以及一系列的反垄断诉讼），但 Internet Explorer3 的成功却有目共睹，其成功不仅仅在于市场营销策略，也源于产品本身。 Internet Explorer 3 是一个划时代产品，因为它也实现了类似于 JavaScript 的客户端语言—— JScript，除此之外还有微软的“老本行” VBScript。 JScript 的诞生成为 JavaScript 发展的一个重要里程碑，标志了动态网页时代的全面到来。图1-4 是 Windows 95 上的 Internet Explorer 3。

图1-4 Windows 95 上的 Internet Explorer 3

1.5.4 标准化—— ECMAScript

最初 JavaScript 并没有一个标准，因此在不同浏览器间有各种各样的兼容性的问题。Internet Explorer 占领市场以后这个问题变得更加尖锐，因此 JavaScript 的标准化势在必行。在1996年， JavaScript 标准由诸多软件厂商共同提交给ECMA（欧洲计算机制造商协会）。ECMA 通过了标准 ECMA-262，也就是 ECMAScript。紧接着国际标准化组织也采纳了ECMAScript 标准（ ISO-16262）。在接下来的几年里，浏览器开发者们就开始以 ECMAScript作为规范来实现 JavaScript 解析引擎。

ECMAScript 诞生至今已经有了多个版本，最新的版本是在 2009 年 12 月发布的ECMAScript 5，而到2012年为止，业界普遍支持的仍是 ECMAScript 3，只有新版的 Chrome 和 Firefox 实现了 ECMAScript 5。

> ECMAScript 仅仅是一个标准，而不是一个语言的具体实现，而且这个标准不像 C++ 语言规范那样严格而详细。除了 JavaScript 之外， ActionScript、QtScript、 WMLScript③也是 ECMAScript 的实现。

1.5.5 浏览器兼容性问题

尽管有 ECMAScript 作为 JavaScript 的语法和语言特性标准，但是关于 JavaScript 其他方面的规范还是不明确，同时不同浏览器又加入了各自特有的对象、函数。这也就是为什么这么多年来同样的 JavaScript 代码会在不同的浏览器中呈现出不同的效果，甚至在一个浏览器中可以执行，而在另一个浏览器中却不可以。

要注意的是，浏览器的兼容性问题并不只是由 JavaScript 的兼容性造成的，而是 DOM、BOM、 CSS 解析等不同的行为导致的。万维网联盟（ World Wide Web Consortium， W3C）针对这个问题提出了很多标准建议，目前已经几乎被所有厂商和社区接受，浏览器的兼容性问题迅速得到了改善。

1.5.6 引擎效率革命和 JavaScript 的未来

第一款 JavaScript 引擎是由 Brendan Eich 在网景的 Navigator 中开发的，它的名字叫做SpiderMonkey。 SpiderMonkey 在这之后还用作 Mozilla Firefox 1.0~3.0版本的引擎，而从Firefox 3.5 开始换为 TraceMonkey， 4.0版本以后又换为 JaegerMonkey。 Google Chrome 的JavaScript 引擎是 V8，同时 V8 也是 Node.js 的引擎。微软从 Internet Explorer 9 开始使用其新的 JavaScript 引擎 Chakra。

过去， JavaScript 一直不被人重视，很大程度上是因为它效率不高——不仅速度慢，还占用大量内存。但如今JavaScript的效率却令人刮目相看。历史总是如此相似，正如没有Shockley 发明晶体管就没有电子科技革命一样，如果没有2008年以来的 JavaScript 引擎革命，Node.js 也不会这么快诞生。

2008年 Mozilla Firefox 的一次改动，使 Firefox 3.0的 JavaScript 性能大幅提升，从而引发了 JavaScript 引擎之间的效率竞赛。紧接着 WebKit①开发团队宣告了 Safari 4 新的 JavaScript 引擎 SquirrelFish（后来改名 Nitro）可以大幅度提升脚本执行速度。 Google Chrome 刚刚诞生就因它的 JavaScript 性能而备受称赞，但随着 WebKit 的 Squirrelfish Extreme 和 Mozilla 的 TraceMonkey 技术的出现， Chrome 的 JavaScript 引擎速度被超越了，于是 Chrome 2 发布时使用了更快速的 V8 引擎。 V8 一出场就以其一骑绝尘般的速度打败了所有对手，一度成为 JavaScript 引擎的速度之王。于是其他浏览器的开发者开始奋力追赶，与以往不同的是， Internet Explorer 也加入了这次竞赛，并取得了不俗的成绩。

时至今日，各个 JavaScript 引擎的效率已经不相上下，通过不同引擎根据不同测试基准测得的结果各有千秋。更有趣的是， JavaScript 的效率在不知不觉中已经超越了其他所有传统的脚本语言，并带动了解释器的革新运动。 JavaScript 已经成为了当今速度最快的脚本语言之一，昔日“丑小鸭”终于成了惊艳绝俗的“白天鹅”。

尽管如此，我们不能否认 JavaScript 还有很多不完美之处，譬如一些违反直觉的特性，这几乎成了 JavaScript 遭受批评和攻击的焦点。如今 JavaScript 还在继续发展， ECMAScript 6 也正在起草中，更有像 CoffeeScript 这样专门为了弥补 JavaScript 语言特性的不足而诞生的语言。 Google 也专门针对客户端 JavaScript 不完美的地方推出了 Dart 语言。随着大规模的应用推广，我们有理由相信 JavaScript 会变得越来越好。

## 1.6 CommonJS

1.6.1 服务端 JavaScript 的重生
Node.js 并不是第一个尝试使 JavaScript 运行在浏览器之外的项目。追根溯源，在
JavaScript 诞生之初，网景公司就实现了服务端的 JavaScript，但由于需要支付一大笔授权费
用才能使用，服务端 JavaScript 在当年并没有像客户端 JavaScript 一样流行开来。真正使大
多数人见识到 JavaScript 在服务器开发威力的，是微软的 ASP。
2000年左右，也就是 ASP 蒸蒸日上的年代，很多开发者开始学习 JScript。然而 JScript 在
当时并不是很受欢迎，一方面是早期的 JScript 和 JavaScript 兼容较差，另一方面微软大力推
广的是 VBScript，而不是 JScript。随着后来 LAMP 的兴起，以及Web 2.0 时代的到来， Ajax
等一系列概念的提出， JavaScript 成了前端开发的代名词，同时服务端 JavaScript 也逐渐被人
遗忘。
直至几年前， JavaScript 的种种优势才被重新提起， JavaScript 又具备了在服务端流行的
条件， Node.js 应运而生。与此同时， RingoJS 也基于 Rhino 实现了类似的服务端 JavaScript 平
台，还有像 CouchDB、 MongoDB 等新型非关系型数据库也开始用 JavaScript 和 JSON 作为
其数据操纵语言，基于 JavaScript 的服务端实现开始遍地开花。

1.6.2 CommonJS 规范与实现
正如当年为了统一 JavaScript 语言标准，人们制定了 ECMAScript 规范一样，如今为了
统一 JavaScript 在浏览器之外的实现， CommonJS 诞生了。 CommonJS 试图定义一套普通应
用程序使用的API，从而填补 JavaScript 标准库过于简单的不足。 CommonJS 的终极目标是
制定一个像 C++ 标准库一样的规范，使得基于 CommonJS API 的应用程序可以在不同的环
境下运行，就像用 C++ 编写的应用程序可以使用不同的编译器和运行时函数库一样。为了
保持中立， CommonJS 不参与标准库实现，其实现交给像 Node.js 之类的项目来完成。图1-5
是 CommonJS 的各种实现。
CommonJS 规范包括了模块（ modules）、包（ packages）、系统（ system）、二进制（ binary）、
控制台（ console）、编码（ encodings）、文件系统（ filesystems）、套接字（ sockets）、单元测
试（ unit testing）等部分。目前大部分标准都在拟定和讨论之中，已经发布的标准有
Modules/1.0、 Modules/1.1、 Modules/1.1.1、 Packages/1.0、 System/1.0。
Node.js 是目前 CommonJS 规范最热门的一个实现，它基于 CommonJS 的 Modules/1.0 规
范实现了 Node.js 的模块，同时随着 CommonJS 规范的更新， Node.js 也在不断跟进。由于目
前 CommonJS 大部分规范还在起草阶段， Node.js 已经率先实现了一些功能，并将其反馈给
CommonJS 规范制定组织，但 Node.js 并不完全遵循 CommonJS 规范。这是所有规范制定者
都会遇到的尴尬局面，因为规范的制定总是滞后于技术的发展。

# 第二章 安装和配置Node.js

编译源代码。Node.js 从 0.6 版本开始已经实现了源代码级别的跨平台，因此我们可以使用不同的编译命令将同一份源代码的基础上编译为不同平台下的原生可执行代码。在编译之前，要先获取源码包。我们建议访问http://nodejs.org，点击Download链接，然后选择Source Code，下载正式发布的源码包。如果你需要开发中的版本，可以通过https://github.com/joyent/node/zipball/master 获得，或者在命令行下输入`git clone git://github.com/joyent/node.git` 从git获得最新的分支。

安装 Node 包管理器。Node 包管理器（ npm）是一个由 Node.js 官方提供的第三方包管理工具，就像 PHP 的Pear、 Python 的 PyPI 一样。 npm 是一个完全由 JavaScript 实现的命令行工具，通过 Node.js 执行，因此严格来讲它不属于 Node.js 的一部分。在最初的版本中，我们需要在安装完 Node.js 以后手动安装npm。但从 Node.js 0.6 开始， npm 已包含在发行包中了，我们在 Windows、
Mac 上安装包和源代码包时会自动同时安装 npm。

安装多版本管理器。迄今为止 Node.js 更新速度还很快，有时候新版本还会将旧版本的一些 API 废除，以至于写好的代码不能向下兼容。有时候可能想要尝试一下新版本有趣的特性，但又想要保持一个相对稳定的环境。基于这种需求， Node.js 的社区开发了多版本管理器，用于在一台机器上维护多个版本的 Node.js 实例，方便按需切换。 Node 多版本管理器（ Node Version Manager， nvm）是一个通用的叫法，它目前有许多不同的实现。

n 是一个十分简洁的 Node 多版本管理器，就连它的名字也不例外。它的名字就是 n，没错，就一个字母。 如果已经安装好了 Node.js 和 npm 环境，就可以直接使用`npm install -g n`命令来安装 n。如果想完全通过 n 来管理 Node.js，那么没安装之前哪来的 npm 呢？事实上， n 并不需要 Node.js 驱动，它只是 bash 脚本，使用 npm 安装只是采取一种简便的方式而已。我们可以在 https://github.com/visionmedia/n 下载它的代码，然后使用 make install 命令安装。

# 第三章 Node.js快速入门

## 3.1 开始用 Node.js 编程

输入 `node --help` 可以看到详细的帮助信息。

运行 Node.js 程序的基本方法就是执行 `node script.js`，其中 script.js 是脚本的文件名。

除了直接运行脚本文件外， `node --help` 显示的使用方法中说明了另一种输出 Hello World 的方式：我们可以把要执行的语句作为 `node -e` 的参数直接执行。

```
$ node -e "console.log('Hello World');"
Hello World
```

使用 node 的 REPL 模式。REPL （ Read-eval-print loop），即输入—求值—输出循环。运行无参数的 node 将会启动一个 JavaScript 的交互式 shell。在任何时候，连续按两次 Ctrl + C 即可推出 Node.js 的 REPL 模式。node 提出的 REPL 在应用开发时会给人带来很大的便利，例如我们可以测试一个包能否正常使用，单独调用应用的某一个模块，执行简单的计算等。

```shell
$ node
> console.log('Hello World');
Hello World
undefined
> consol.log('Hello World');
ReferenceError: consol is not defined
  at repl:1:1
  at REPLServer.eval (repl.js:80:21)
  at repl.js:190:20
  at REPLServer.eval (repl.js:87:5)
  at Interface.<anonymous> (repl.js:182:12)
  at Interface.emit (events.js:67:17)
  at Interface._onLine (readline.js:162:10)
  at Interface._line (readline.js:426:8)
  at Interface._ttyWrite (readline.js:603:14)
  at ReadStream.<anonymous> (readline.js:82:12)
```

建立 HTTP 服务器。Node.js 是为网络而诞生的平台，但又与 ASP、PHP 很很大的不同。成功运行 PHP 之前先要配置一个功能强大而复杂的 HTTP 服务器，譬如 Apache、 IIS 或 Nginx，还需要将 PHP 配置为 HTTP 服务器的模块，或者使用FastCGI 协议调用 PHP 解释器。这种架构是“浏览器 - HTTP 服务器 - PHP 解释器”的组织方式，而Node.js采用了一种不同的组织方式。Node.js 将“HTTP服务器”这一层抽离，直接面向浏览器用户。

```JavaScript
var http = require('http');

http.createServer(function(req, res) {
  res.writeHead(200, {'Content-Type': 'text/html'});
  res.write('<h1>Node.js</h1>');
  res.end('<p>Hello World</p>');
}).listen(3000);

console.log("HTTP server is listening at port 3000.");
```

这个程序调用了 Node.js 提供的http 模块，对所有 HTTP 请求答复同样的内容并监听 3000 端口。在终端中运行这个脚本时，它并不像 Hello World 一样结束后立即退出，而是一直等待，直到按下 Ctrl + C 才会结束。这是因为 listen 函数中创建了事件监听器，使得 Node.js 进程不会退出事件循环。

在开发 Node.js 实现的 HTTP 应用时会发现，无论你修改了代码的哪一部份，都必须终止Node.js 再重新运行才会奏效。这是因为 Node.js 只有在第一次引用到某部份时才会去解析脚本文件，以后都会直接访问内存，避免重复载入，而 PHP 则总是重新读取并解析脚本（如果没有专门的优化配置）。 Node.js的这种设计虽然有利于提高性能，却不利于开发调试，因为我们在开发过程中总是希望修改后立即看到效果，而不是每次都要终止进程并重启。

supervisor 可以帮助你实现这个功能，它会监视你对代码的改动，并自动重启 Node.js。使用方法很简单，首先使用 npm 安装 supervisor。接下来，使用 supervisor 命令启动 app.js。

```shell
$ npm install -g supervisor
$ supervisor app.js

DEBUG: Running node-supervisor with
DEBUG: program 'app.js'
DEBUG: --watch '.'
DEBUG: --extensions 'node|js'
DEBUG: --exec 'node'

DEBUG: Starting child process with 'node app.js'
DEBUG: Watching directory '/home/byvoid/.' for changes.
HTTP server is listening at port 3000.
```

当代码被改动时，运行的脚本会被终止，然后重新启动。在终端中显示的结果如下：

```shell
DEBUG: crashing child
DEBUG: Starting child process with 'node app.js'
HTTP server is listening at port 3000.
```

## 3.2 异步式 I/O 与事件式编程

Node.js 最大的特点就是异步式 I/O（或者非阻塞 I/O）与事件紧密结合的编程模式。这
种模式与传统的同步式 I/O 线性的编程思路有很大的不同，因为控制流很大程度上要靠事件
和回调函数来组织，一个逻辑要拆分为若干个单元。

3.2.1 阻塞与线程

什么是阻塞（ block）呢？线程在执行中如果遇到磁盘读写或网络通信（统称为 I/O 操作），
通常要耗费较长的时间，这时操作系统会剥夺这个线程的 CPU 控制权，使其暂停执行，同
时将资源让给其他的工作线程，这种线程调度方式称为 阻塞。当 I/O 操作完毕时，操作系统
将这个线程的阻塞状态解除，恢复其对CPU的控制权，令其继续执行。这种 I/O 模式就是通
常的同步式 I/O（ Synchronous I/O）或阻塞式 I/O （ Blocking I/O）。

相应地，异步式 I/O （ Asynchronous I/O）或非阻塞式 I/O （ Non-blocking I/O）则针对
所有 I/O 操作不采用阻塞的策略。当线程遇到 I/O 操作时，不会以阻塞的方式等待 I/O 操作
的完成或数据的返回，而只是将 I/O 请求发送给操作系统，继续执行下一条语句。当操作
系统完成 I/O 操作时，以事件的形式通知执行 I/O 操作的线程，线程会在特定时候处理这个
事件。为了处理异步 I/O，线程必须有事件循环，不断地检查有没有未处理的事件，依次予
以处理。

阻塞模式下，一个线程只能处理一项任务，要想提高吞吐量必须通过多线程。而非阻塞
模式下，一个线程永远在执行计算操作，这个线程所使用的 CPU 核心利用率永远是 100%，
I/O 以事件的方式通知。在阻塞模式下，多线程往往能提高系统吞吐量，因为一个线程阻塞
时还有其他线程在工作，多线程可以让 CPU 资源不被阻塞中的线程浪费。而在非阻塞模式
下，线程不会被 I/O 阻塞，永远在利用 CPU。多线程带来的好处仅仅是在多核 CPU 的情况
下利用更多的核，而Node.js的单线程也能带来同样的好处。这就是为什么 Node.js 使用了单
线程、非阻塞的事件编程模式。

图3-3 和图3-4 分别是多线程同步式 I/O 与单线程异步式 I/O 的示例。假设我们有一项工
作，可以分为两个计算部分和一个 I/O 部分， I/O 部分占的时间比计算多得多（通常都是这
样）。如果我们使用阻塞 I/O，那么要想获得高并发就必须开启多个线程。而使用异步式 I/O
时，单线程即可胜任。

单线程事件驱动的异步式 I/O 比传统的多线程阻塞式 I/O 究竟好在哪里呢？简而言之，
异步式 I/O 就是少了多线程的开销。对操作系统来说，创建一个线程的代价是十分昂贵的，
需要给它分配内存、列入调度，同时在线程切换的时候还要执行内存换页， CPU 的缓存被
清空，切换回来的时候还要重新从内存中读取信息，破坏了数据的局部性。 

当然，异步式编程的缺点在于不符合人们一般的程序设计思维，容易让控制流变得晦涩
难懂，给编码和调试都带来不小的困难。习惯传统编程模式的开发者在刚刚接触到大规模的异
步式应用时往往会无所适从，但慢慢习惯以后会好很多。尽管如此，异步式编程还是较为困难，
不过可喜的是现在已经有了不少专门解决异步式编程问题的库（如async），参见6.2.2节。

表3-1比较了同步式 I/O 和异步式 I/O 的特点。

同步式 I/O（阻塞式）| 异步式 I/O（非阻塞式）
利用多线程提供吞吐量 | 单线程即可实现高吞吐量
通过事件片分割和线程调度利用多核CPU | 通过功能划分利用多核CPU
需要由操作系统调度多线程使用多核 CPU | 可以将单进程绑定到单核 CPU
难以充分利用 CPU 资源 | 可以充分利用 CPU 资源
内存轨迹大，数据局部性弱|  内存轨迹小，数据局部性强
符合线性的编程思维 | 不符合传统编程思维

3.2.2 回调函数

同步式读取文件的方式比较容易理解，将文件名作为参数传入 fs.readFileSync 函
数，阻塞等待读取完成后，将文件的内容作为函数的返回值赋给 data 变量，接下来控制台
输出 data 的值，最后输出 end.。

异步式读取文件就稍微有些违反直觉了， end.先被输出。要想理解结果，我们必须先
知道在 Node.js 中，异步式 I/O 是通过回调函数来实现的。 fs.readFile 接收了三个参数，
第一个是文件名，第二个是编码方式，第三个是一个函数，我们称这个函数为回调函数。
JavaScript 支 持匿 名 的函 数定 义 方式。

```JavaScript
// 异步
var fs = require('fs');
fs.readFile('file.txt', 'utf-8', function(err, data) {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
});
console.log('end.');
// end.
// Contents of the file.

// 同步
var fs = require('fs');
var data = fs.readFileSync('file.txt', 'utf-8');
console.log(data);
console.log('end.');
// Contents of the file.
// end.
```

fs.readFile 调用时所做的工作只是将异步式 I/O 请求发送给了操作系统，然后立即
返回并执行后面的语句，执行完以后进入事件循环监听事件。当 fs 接收到 I/O 请求完成的
事件时，事件循环会主动调用回调函数以完成后续工作。因此我们会先看到 end.，再看到
file.txt 文件的内容。

> Node.js 中，并不是所有的 API 都提供了同步和异步版本。 Node.js 不
鼓励使用同步 I/O。

3.2.3 事件
Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。在开发者看来，事
件由 EventEmitter 对象提供。前面提到的 fs.readFile 和 http.createServer 的回
调函数都是通过 EventEmitter 来实现的。下面我们用一个简单的例子说明 EventEmitter
的用法：

```JavaScript
var EventEmitter = require('events').EventEmitter;
var event = new EventEmitter();

event.on('some_event', function() {
  console.log('some_event occured.');
});

setTimeout(function() {
  event.emit('some_event');
}, 1000);
```

运行这段代码， 1秒后控制台输出了 some_event occured.。其原理是 event 对象
注册了事件 some_event 的一个监听器，然后我们通过 setTimeout 在1000毫秒以后向
event 对象发送事件 some_event，此时会调用 some_event 的监听器。

我们将在 4.3.1节中详细讨论 EventEmitter 对象的用法。

Node.js 的事件循环机制

Node.js 在什么时候会进入事件循环呢？答案是 Node.js 程序由事件循环开始，到事件循
环结束，所有的逻辑都是事件的回调函数，所以 Node.js 始终在事件循环中，程序入口就是
事件循环第一个事件的回调函数。事件的回调函数在执行的过程中，可能会发出 I/O 请求或
直接发射（ emit）事件，执行完毕后再返回事件循环，事件循环会检查事件队列中有没有未
处理的事件，直到程序结束。图3-5说明了事件循环的原理。

与其他语言不同的是， Node.js 没有显式的事件循环，类似 Ruby 的 EventMachine::run()
的函数在 Node.js 中是不存在的。 Node.js 的事件循环对开发者不可见， 由 libev 库实现。 libev
支持多种类型的事件，如 ev_io、 ev_timer、 ev_signal、 ev_idle 等，在 Node.js 中均被
EventEmitter 封装。 libev 事件循环的每一次迭代，在 Node.js 中就是一次 Tick， libev 不
断检查是否有活动的、可供检测的事件监听器，直到检测不到时才退出事件循环，进程结束。

## 3.3 模块和包

模块（ Module）和包（ Package）是 Node.js 最重要的支柱。开发一个具有一定规模的程序不可能只用一个文件，通常需要把各个功能拆分、封装，然后组合起来，模块正是为了实现这种方式而诞生的。在浏览器 JavaScript 中，脚本模块的拆分和组合通常使用 HTML 的script 标签来实现。 Node.js 提供了 require 函数来调用其他模块，而且模块都是基于文件的，机制十分简单。Node.js 的模块和包机制的实现参照了 CommonJS 的标准，但并未完全遵循。

模块和包是没有本质区别的，两个概念也时常混用。如果要辨析，那么可以把包理解成是实现了某个功能模块的集合，用于发布和维护。对使用者来说，模块和包的区别是透明的，因此经常不作区分。

什么是模块。模块是 Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是 JavaScript 代码、 JSON 或者编译过的 C/C++ 扩展。在前面章节的例子中，用到了 `var http = require('http')`， 其中 http 是 Node.js 的一个核心模块，其内部是用 C++ 实现的，外部用 JavaScript 封装。我们通过require 函数获取了这个模块，然后才能使用其中的对象。

创建及加载模块。Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口， require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。这种接口封装方式比许多语言要简洁得多，同时也不失优雅，未引入违反语义的特性，符合传统的编程逻辑。因为 require 不会重复加载模块，也就是说无论调用多少次 require， 获得的模块都是同一个。

覆盖 exports。有时候只是想把一个对象封装到模块中。模块接口的唯一变化是使用 `module.exports = Hello` 代替了 `exports.Hello=Hello`。在外部引用该模块时，其接口对象就是要输出的 Hello 对象本身，而不是原先的exports。事实上， exports 本身仅仅是一个普通的空对象，即 `{}`，它专门用来声明接口，本质上是通过它为模块闭包的内部建立了一个有限的访问接口。因为它没有任何特殊的地方，所以可以用其他东西来代替，譬如我们上面例子中的 Hello 对象。

## 3.4 调试

命令行调试。Node.js 支持命令行下的单步调试。在命令行下执行`node debug debug.js`，将会启动调试工具。

远程调试。V8 提供的调试功能是基于 TCP 协议的，因此 Node.js 可以轻松地实现远程调试。在命令行下使用以下两个语句之一可以打开调试服务器。`node --debug`命令选项可以启动调试服务器，默认情况下调试端口是 5858，也可以使用 --debug=1234 指定调试端口为 1234。使用 --debug 选项运行脚本时，脚本会正常执行，但不会暂停，在执行过程中调试客户端可以连接到调试服务器。如果要求脚本暂停执行等待客户端连接，则应该使用 --debug-brk 选项。这时调试服务器在启动后会立刻暂停执行脚本，等待调试客户端连接。
`
node --debug[=port] script.js
node --debug-brk[=port] script.js
`

使用 Eclipse 调试 Node.js。基于 Node.js 的远程调试功能，我们甚至可以用支持 V8 调试协议的 IDE 调试，例如强大的 Eclipse。

使用 node-inspector 调试 Node.js。大部分基于 Node.js 的应用都是运行在浏览器中的，例如强大的调试工具 node-inspector。node-inspector 是一个完全基于 Node.js 的开源在线调试工具，提供了强大的调试功能和友好的用户界面，它的使用方法十分简便。

# 第四章 Node.js核心模块

## 4.1 全局对象

JavaScript 中有一个特殊的对象，称为全局对象（Global Object），它及其所有属性都可以在程序的任何地方访问，即全局变量。在浏览器 JavaScript 中，通常 window 是全局对象，而 Node.js 中的全局对象是 global，所有全局变量（除了 global 本身以外）都是 global 对象的属性。

process 是一个全局变量，即 global 对象的属性。它用于描述当前 Node.js 进程状态的对象，提供了一个与操作系统的简单接口。

`process.argv` 是命令行参数数组，第一个元素是 node， 第二个元素是脚本文件名，从第三个元素开始每个元素是一个运行参数。

`process.stdout`是标准输出流，通常我们使用的 `console.log()` 向标准输出打印字符，而 `process.stdout.write()` 函数提供了更底层的接口。

`process.stdin`是标准输入流，初始时它是被暂停的，要想从标准输入读取数据，你必须恢复流，并手动编写流的事件响应函数。

`process.nextTick(callback)`的功能是为事件循环设置一项任务， Node.js 会在下次事件循环调响应时调用 callback。

console 用于提供控制台标准输出，它是由 Internet Explorer 的JScript引擎提供的调试工具，后来逐渐成为浏览器的事实标准。Node.js 沿用了这个标准，提供与习惯行为一致的 console 对象，用于向标准输出流或标准错误流输出字符。

`console.log()`：向标准输出流打印字符并以换行符结束。 console.log 接受若干个参数，如果只有一个参数，则输出这个参数的字符串形式。如果有多个参数，则以类似于 C 语言 printf() 命令的格式输出。第一个参数是一个字符串，如果没有参数，只打印一个换行。

`console.error()`：与 `console.log()` 用法相同，只是向标准错误流输出。

`console.trace()`：向标准错误流输出当前的调用栈。

## 4.2 常用工具util

util 是一个 Node.js 核心模块，提供常用函数的集合，用于弥补核心 JavaScript 的功能过于精简的不足。

`util.inherits(constructor, superConstructor)`是一个实现对象间原型继承的函数。

`util.inspect(object,[showHidden],[depth],[colors])`是一个将任意对象转换为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。

## 4.3 事件驱动events

events 是 Node.js 最重要的模块，没有“之一”，原因是 Node.js 本身架构就是事件式的，而它提供了唯一的接口，所以堪称 Node.js 事件编程的基石。events 模块不仅用于用户代码与 Node.js 下层事件循环的交互，还几乎被所有的模块依赖。

事件发射器。events 模块只提供了一个对象：events:EventEmitter。EventEmitter 的核心就是事件发射与事件监听器功能的封装。EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件， EventEmitter 支持若干个事件监听器。当事件发射时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。

- `EventEmitter.on(event, listener)` 为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数 listener。
- `EventEmitter.emit(event, [arg1], [arg2], [...])` 发射 event 事件，传递若干可选参数到事件监听器的参数表。
- `EventEmitter.once(event, listener)` 为指定事件注册一个单次监听器，即监听器最多只会触发一次，触发后立刻解除该监听器。
- `EventEmitter.removeListener(event, listener)` 移除指定事件的某个监听器， listener 必须是该事件已经注册过的监听器。
- `EventEmitter.removeAllListeners([event])` 移除所有事件的所有监听器，如果指定 event，则移除指定事件的所有监听器。

EventEmitter 定义了一个特殊的事件 error，它包含了“错误”的语义，我们在遇到异常的时候通常会发射 error 事件。当 error 被发射时， EventEmitter 规定如果没有响应的监听器， Node.js 会把它当作异常，退出程序并打印调用栈。我们一般要为会发射 error 事件的对象设置监听器，避免遇到错误后整个程序崩溃。

继承 EventEmitter。大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、 net、http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。为什么要这样做呢？原因有两点。首先，具有某个实体功能的对象实现事件符合语义，事件的监听和发射应该是一个对象的方法。其次 JavaScript 的对象机制是基于原型的，支持部分多重继承，继 EventEmitter 不会打乱对象原有的继承关系。

## 4.4 文件系统fs

fs 模块是文件操作的封装，它提供了文件的读取、写入、更名、删除、遍历目录、链接等 POSIX 文件系统操作。与其他模块不同的是， fs 模块中所有的操作都提供了异步的和同步的两个版本，例如读取文件内容的函数有异步的`fs.readFile()`和同步的`fs.readFileSync()`。

`fs.readFile(filename,[encoding],[callback(err,data)])`是最简单的读取文件的函数。它接受一个必选参数 filename，表示要读取的文件名。第二个参数 encoding 是可选的，表示文件的字符编码。 callback 是回调函数，用于接收文件的内容。如果不指定 encoding，则 callback 就是第二个参数。回调函数提供两个参数 err 和 data， err 表示有没有错误发生， data 是文件内容。如果指定了 encoding， data 是一个解析后的字符串，否则 data 将会是以 Buffer 形式表示的二进制数据。

```JavaScript
var fs = require('fs');
fs.readFile('content.txt', 'utf-8', function(err, data) {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
});
```

`fs.readFileSync(filename, [encoding])`是 fs.readFile 同步的版本。它接受的参数和 fs.readFile 相同，而读取到的文件内容会以函数返回值的形式返回。如果有错误发生， fs 将会抛出异常，你需要使用 try 和 catch 捕捉并处理异常。

`fs.open(path, flags, [mode], [callback(err, fd)])`是 POSIX open 函数的
封装，与 C 语言标准库中的 fopen 函数类似。它接受两个必选参数， path 为文件的路径，
flags 可以是以下值。
- r ：以读取模式打开文件。
- r+ ：以读写模式打开文件。
- w ：以写入模式打开文件，如果文件不存在则创建。
- w+ ：以读写模式打开文件，如果文件不存在则创建。
- a ：以追加模式打开文件，如果文件不存在则创建。
- a+ ：以读取追加模式打开文件，如果文件不存在则创建。

mode 参数用于创建文件时给文件指定权限，默认是 0666。回调函数将会传递一个文件描述符 fd。

`fs.read(fd, buffer, offset, length, position, [callback(err, bytesRead, buffer)])`是 POSIX read 函数的封装，相比 fs.readFile 提供了更底层的接口。fs.read 的功能是从指定的文件描述符 fd 中读取数据并写入 buffer 指向的缓冲区对象。 offset 是buffer 的写入偏移量。 length 是要从文件中读取的字节数。 position 是文件读取的起始位置，如果 position 的值为 null，则会从当前文件指针的位置读取。回调函数传递bytesRead 和 buffer，分别表示读取的字节数和缓冲区对象。

## 4.5 HTTP服务器与客户端

Node.js 标准库提供了 http 模块，其中封装了一个高效的 HTTP 服务器和一个简易的HTTP客户端。http.Server 是一个基于事件的 HTTP 服务器，它的核心由 Node.js 下层 C++ 部分实现，而接口由 JavaScript 封装，兼顾了高性能与简易性。 http.request 则是一个 HTTP 客户端工具，用于向 HTTP 服务器发起请求，例如实现 Pingback 或者内容抓取。

HTTP 服务器。http.Server 是 http 模块中的 HTTP 服务器对象，用 Node.js 做的所有基于 HTTP 协议的系统，如网站、社交应用甚至代理服务器，都是基于 http.Server 实现的。它提供了一套封装级别很低的 API，仅仅是流控制和简单的消息解析，所有的高层功能都要通过它的接口来实现。

`http.ClientRequest` 是由 http.request 或 http.get 返回产生的对象，表示一个已经产生而且正在进行中的 HTTP 请求。它提供一个 response 事件，即 http.request 或 http.get 第二个参数指定的回调函数的绑定对象。

# 第五章 使用Node.js进行Web开发

## 5.1 准备工作

Node.js 和 PHP、Perl、 ASP、 JSP 一样，目的都是实现动态网页，也就是说由服务器动态生成 HTML 页面。之所以要这么做，是因为静态 HTML 的可扩展性非常有限，无法与用户有效交互。同时如果有大量相似的内容，例如产品介绍页面，那么1000个产品就要1000个静态的 HTML 页面，维护这1000个页面简直是一场灾难，因此动态生成 HTML 页面的技术应运而生。最早实现动态网页的方法是使用Perl ①和 CGI。在 Perl 程序中输出 HTML 内容，由 HTTP 服务器调用 Perl 程序，将结果返回给客户端。大概在 2000 年左右，以 ASP、 PHP、 JSP 的为代表的以模板为基础的语言出现了，这种语言的使用方法与 CGI 相反，是在以 HTML 为主的模板中插入程序代码。

但它的问题是页面和程序逻辑紧密耦合。为了解决这种问题，以 MVC 架构为基础的平台逐渐兴起，著名的 Ruby on Rails、 Django、 Zend Framework 都是基于 MVC 架构的。MVC（Model-View-Controller，模型视图控制器）是一种软件的设计模式，它最早是由 20 世纪 70 年代的 Smalltalk 语言提出的，即把一个复杂的软件工程分解为三个层面：模型、视图和控制器。
- 模型是对象及其数据结构的实现，通常包含数据库操作。
- 视图表示用户界面，在网站中通常就是 HTML 的组织结构。
- 控制器用于处理用户请求和数据流、复杂模型，将输出传递给视图。
我们称 PHP、 ASP、 JSP 为“模板为中心的架构”

Node.js 本质上和 Perl 或 C++ 一样，都可以作为 CGI 扩展被调用，但它还可以跳过 HTTP 服务器，因为它本身就是。传统的架构中 HTTP 服务器的角色会由 Apache、 Nginx、 IIS 之类的软件来担任，而 Node.js 不需要②。 Node.js 提供了 http 模块，它是由 C++ 实现的，性能可靠，可以直接应用到生产环境。Node.js 和其他的语言相比的另一个显著区别，在于它的原始封装程度较低。例如 PHP 中你可以访问 $_REQUEST 获取客户端的 POST 或 GET 请求，通常不需要直接处理 HTTP 协议①。这些语言要求由 HTTP 服务器来调用，因此你需要设置一个 HTTP 服务器来处理客户端的请求， HTTP 服务器通过 CGI 或其他方式调用脚本语言解释器，将运行的结果传递回HTTP 服务器，最终再把内容返回给客户端。而在 Node.js 中，很多工作需要你自己来做（并不是都要自己动手，因为有第三方框架的帮助）。

Express 除了为 http 模块提供了更高层的接口外，还实现了许多功能，其中包括：
- 路由控制；
- 模板解析支持；
- 动态视图；
- 用户会话；
- CSRF 保护；
- 静态文件服务；
- 错误控制器；
- 访问日志；
- 缓存；
- 插件支持。

需要指出的是， Express 不是一个无所不包的全能框架，像 Rails 或 Django 那样实现了模板引擎甚至 ORM （Object Relation Model，对象关系模型）。它只是一个轻量级的 Web 框架，多数功能只是对 HTTP 协议中常用操作的封装，更多的功能需要插件或者整合其他模块来完成。

## 5.2 快速开始

Express 像很多框架一样都提供了 Quick Start（快速开始）工具，这个工具的功能通常是建立一个网站最小的基础框架，在此基础上完成开发。为了使用这个工具，我们需要用全局模式安装 Express，因为只有这样我们才能在命令行中使用它。

通过以下命令建立网站基本结构：

```
express -t ejs microblog
```

无参数的`npm install`的功能就是检查当前目录下的 package.json，并自动安装所有指定的依赖。

用 Express 实现的网站实际上就是一个 Node.js 程序，因此可以直接运行。我们运行`node app.js`， 看到`Express server listening on port 3000 in development mode`。接下来，打开浏览器，输入地址 http://localhost:3000， 就可以看到一个简单的 Welcome to Express 页面了。

## 5.3 路由控制

当通过浏览器访问 app.js 建立的服务器时，会看到一个简单的页面，实际上它已经完成了许多透明的工作，现在就让我们来解释一下它的工作机制，以帮助理解网站的整体架构。访问 http://localhost:3000，浏览器会向服务器发送以下请求。

```
GET / HTTP/1.1
Host: localhost:3000
Connection: keep-alive
Cache-Control: max-age=0
User-Agent: Mozilla/5.0 AppleWebKit/535.19 (KHTML, like Gecko) Chrome/18.0.1025.142
Safari/535.19
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate,sdch
Accept-Language: zh;q=0.8,en-US;q=0.6,en;q=0.4
Accept-Charset: UTF-8,*;q=0.5
```

服务器在开始监听之前，设置好了所有的路由规则，当请求到达时直接分配到响应函数。`app.get` 是路由规则创建函数，它接受两个参数，第一个参数是请求的路径，第二个参数是一个回调函数，该路由规则被触发时调用回调函数，其参数表传递两个参数，分别是 req 和 res，表示请求信息和响应信息。

Express 还支持更高级的路径匹配模式。例如我们想要展示一个用户的个人页面，路径为`/user/[username]`，可以用下面的方法定义路由规则。

```js
app.get('/user/:username', function(req, res) {
  res.send('user: ' + req.params.username);
});
```

路径规则 `/user/:username` 会被自动编译为正则表达式，类似于 `\/user\/([^\/]+)\/?` 这样的形式。路径参数可以在响应函数中通过 req.params 的属性访问。

路径规则同样支持 JavaScript 正则表达式，例如 `app.get(\/user\/([^\/]+)\/?,callback)`。这样的好处在于可以定义更加复杂的路径规则，而不同之处是匹配的参数是匿名的，因此需要通过`req.params[0]`、 `req.params[1]`这样的形式访问。

Express 支持 REST 风格的请求方式，在介绍之前我们先说明一下什么是 REST。REST 的意思是 表征状态转移（Representational State Transfer），它是一种基于 HTTP 协议的网络应用的接口风格，充分利用 HTTP 的方法实现统一风格接口的服务。

Express 支持同一路径绑定多个路由响应函数。

```js
app.all('/user/:username', function(req, res) {
  res.send('all methods captured');
});
app.get('/user/:username', function(req, res) {
  res.send('user: ' + req.params.username);
});
```

但当访问任何被这两条同样的规则匹配到的路径时，会发现请求总是被前一条路由规则捕获，后面的规则会被忽略。原因是 Express 在处理路由规则时，会优先匹配先定义的路由规则，因此后面相同的规则被屏蔽。Express 提供了路由控制权转移的方法，即回调函数的第三个参数next，通过调用`next()`，会将路由控制权转移给后面的规则。

```
app.all('/user/:username', function(req, res, next) {
  console.log('all methods captured');
  next();
});
app.get('/user/:username', function(req, res) {
  res.send('user: ' + req.params.username);
});
```

这是一个非常有用的工具，可以让我们轻易地实现中间件，而且还能提高代码的复用程度。例如我们针对一个用户查询信息和修改信息的操作，分别对应了 GET 和 PUT 操作，而两者共有的一个步骤是检查用户名是否合法，因此可以通过 `next()` 方法实现。

```
var users = {
  'byvoid': {
    name: 'Carbo',
    website: 'http://www.byvoid.com'
  }
};
app.all('/user/:username', function(req, res, next) {
  // 检查用户是否存在
  if (users[req.params.username]) {
    next();
  } else {
   next(new Error(req.params.username + ' does not exist.'));
  }
});
app.get('/user/:username', function(req, res) {
  // 用户一定存在，直接展示
  res.send(JSON.stringify(users[req.params.username]));
});
app.put('/user/:username', function(req, res) {
  // 修改用户信息
  res.send('Done');
});
```

## 5.4 模板引擎

模板引擎（Template Engine）是一个从页面模板根据一定的规则生成 HTML 的工具。它的发轫可以追溯到 1996 年 PHP 2.0 的诞生。 PHP 原本是 Personal Home Page Tools（个人主页工具）的简称，用于取代 Perl 和 CGI 的组合，其功能是让代码嵌入在 HTML 中执行，以产生动态的页面，因此 PHP 堪称是最早的模板引擎的雏形。随后的 ASP、JSP 都沿用了这个模式，即建立一个 HTML 页面模板，插入可执行的代码，运行时动态生成 HTML。

模板引擎的功能是将页面模板和要显示的数据结合起来生成 HTML 页面。它既可以运行在服务器端又可以运行在客户端，大多数时候它都在服务器端直接被解析为 HTML，解析完成后再传输给客户端，因此客户端甚至无法判断页面是否是模板引擎生成的。有时候模板引擎也可以运行在客户端，即浏览器中，典型的代表就是 XSLT，它以 XML 为输入，在客户端生成 HTML 页面。但是由于浏览器兼容性问题， XSLT 并不是很流行。目前的主流还是由服务器运行模板引擎。

在 MVC 架构中，模板引擎包含在服务器端。控制器得到用户请求后，从模型获取数据，调用模板引擎。模板引擎以数据和页面模板为输入，生成 HTML 页面，然后返回给控制器，由控制器交回客户端。

基于 JavaScript 的模板引擎有许多种实现，我们推荐使用 ejs （Embedded JavaScript），因为它十分简单，而且与 Express 集成良好。由于它是标准 JavaScript 实现的，因此它不仅可以运行在服务器端，还可以运行在浏览器中。在 app.js 中通过以下两个语句设置了模板引擎和页面模板的位置。

```
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
```

Express 的视图系统还支持片段视图（partials），它就是一个页面的片段，通常是重复的内容，用于迭代显示。通过它你可以将相对独立的页面块分割出去，而且可以避免显式地使用 for 循环。partial 是一个可以在视图中使用函数，它接受两个参数，第一个是片段视图的名称，第二个可以是一个对象或一个数组，如果是一个对象，那么片段视图中上下文变量引用的就是这个对象；如果是一个数组，那么其中每个元素依次被迭代应用到片段视图。片段视图中上下文变量名就是视图文件名。

Express 提供了一种叫做视图助手的工具，它的功能是允许在视图中访问一个全局的函数或对象，不用每次调用视图解析的时候单独传入。前面提到的 partial 就是一个视图助手。视图助手有两类，分别是静态视图助手和动态视图助手。这两者的差别在于，静态视图助手可以是任何类型的对象，包括接受任意参数的函数，但访问到的对象必须是与用户请求无关的，而动态视图助手只能是一个函数，这个函数不能接受参数，但可以访问 req 和 res 对象。

## 5.5 建立微博网站

根据功能设计，我们把路由按照以下方案规划。

- `/`：首页
- `/u/[user]`：用户的主页
- `/post`：发表信息
- `/reg`：用户注册
- `/login`：用户登录
- `/logout`：用户登出

以上页面还可以根据用户状态细分。发表信息以及用户登出页面必须是已登录用户才能操作的功能，而用户注册和用户登入所面向的对象必须是未登入的用户。首页和用户主页则针对已登入和未登入的用户显示不同的内容。

```
app.get('/', routes.index);
app.get('/u/:user', routes.user);
app.post('/post', routes.post);
app.get('/reg', routes.reg);
app.post('/reg', routes.doReg);
app.get('/login', routes.login);
app.post('/login', routes.doLogin);
app.get('/logout', routes.logout);
```

其中 /post、 /login 和 /reg 由于要接受表单信息，因此使用 app.post 注册路由。 /login 和 /reg 还要显示用户注册时要填写的表单，所以要以 app.get 注册。

## 5.6 用户注册和登录

访问数据库。选用 MongoDB 作为网站的数据库系统，它是一个开源的 NoSQL 数据库，相比MySQL 那样的关系型数据库，它更为轻巧、灵活，非常适合在数据规模很大、事务性不强的场合下使用。

NoSQL 是 1998 年被提出的，它曾经是一个轻量、开源、不提供SQL功能的关系数据库。但现在 NoSQL 被认为是 Not Only SQL 的简称，主要指非关系型、分布式、不提供 ACID①的数据库系统。正如它的名称所暗示的， NoSQL 设计初衷并不是为了取代 SQL 数据库的，而是作为一个补充，它和 SQL 数据库有着各自不同的适应领域。 NoSQL 不像 SQL 数据库一样都有着统一的架构和接口，不同的 NoSQL 数据库系统从里到外可能完全不同。

MongoDB 是一个对象数据库，它没有表、行等概念，也没有固定的模式和结构，所有的数据以文档的形式存储。所谓文档就是一个关联数组式的对象，它的内部由属性组成，一个属性对应的值可能是一个数、字符串、日期、数组，甚至是一个嵌套的文档。

会话支持。会话是一种持久的网络协议，用于完成服务器和客户端之间的一些交互行为。会话是一个比连接粒度更大的概念，一次会话可能包含多次连接，每次连接都被认为是会话的一次操作。在网络应用开发中，有必要实现会话以帮助用户交互。

为了在无状态的 HTTP 协议之上实现会话， Cookie 诞生了。 Cookie 是一些存储在客户端的信息，每次连接的时候由浏览器向服务器递交，服务器也向浏览器发起存储 Cookie 的请求，依靠这样的手段服务器可以识别客户端。我们通常意义上的 HTTP 会话功能就是这样实现的。具体来说，浏览器首次向服务器发起请求时，服务器生成一个唯一标识符并发送给客户端浏览器，浏览器将这个唯一标识符存储在 Cookie 中，以后每次再发起请求，客户端浏览器都会向服务器传送这个唯一标识符，服务器通过这个唯一标识符来识别用户。

对于开发者来说，我们无须关心浏览器端的存储，需要关注的仅仅是如何通过这个唯一标识符来识别用户。很多服务端脚本语言都有会话功能，如 PHP，把每个唯一标识符存储到文件中。 Express 也提供了会话中间件，默认情况下是把用户信息存储在内存中，但我们既然已经有了 MongoDB，不妨把会话信息存储在数据库中，便于持久维护。

## 5.7 发表微博


# 第六章 Node.js进阶话题

## 6.1 模块加载机制

Node.js 的模块加载对用户来说十分简单，只需调用 require 即可，但其内部机制较为复杂。

模块的类型。Node.js 的模块可以分为两大类，一类是核心模块，另一类是文件模块。核心模块就是Node.js 标准 API 中提供的模块，如 fs、 http、 net、 vm 等，这些都是由 Node.js 官方提供的模块，编译成了二进制代码。我们可以直接通过 require 获取核心模块，例如 `require('fs')`。核心模块拥有最高的加载优先级，换言之如果有模块与其命名冲突，Node.js 总是会加载核心模块。

文件模块则是存储为单独的文件（或文件夹）的模块，可能是 JavaScript 代码、 JSON 或编译好的 C/C++ 代码。文件模块的加载方法相对复杂，但十分灵活，尤其是和 npm 结合使用时。在不显式指定文件模块扩展名的时候， Node.js 会分别试图加上 .js、 .json 和 .node扩展名。 .js 是 JavaScript 代码， .json 是 JSON 格式的文本， .node 是编译好的 C/C++ 代码。

文件模块的加载有两种方式，一种是按路径加载，一种是查找 node_modules 文件夹。如果 require 参数以“/ ”开头，那么就以绝对路径的方式查找模块名称，例如 require ('/home/byvoid/module') 将会按照优先级依次尝试加载 /home/byvoid/module.js、/home/byvoid/module.json 和 /home/byvoid/module.node。

如果 require 参数以“./ ”或“../ ”开头，那么则以相对路径的方式来查找模块，这种方式在应用中是最常见的。

如果require参数不以“/ ”、“./ ”或“../ ”开头，而该模块又不是核心模块，那么就要通过查找 node_modules 加载模块了。我们使用npm获取的包通常就是以这种方式加载的。在 node_modules 目录的外面一层，我们可以直接使用 `require('express')` 来代替`require('./node_modules/express')`。这是Node.js模块加载的一个重要特性：通过查找 node_modules 目录来加载模块。

当 require 遇到一个既不是核心模块，又不是以路径形式表示的模块名称时，会试图在当前目录下的 node_modules 目录中来查找是不是有这样一个模块。如果没有找到，则会在当前目录的上一层中的 node_modules 目录中继续查找，反复执行这一过程，直到遇到根目录为止。

加载缓存。Node.js 模块不会被重复加载，这是因为 Node.js 通过文件名缓存所有加载过的文件模块，所以以后再访问到时就不会重新加载了。注意， Node.js 是根据实际文件名缓存的，而不是`require()`提供的参数缓存的，也就是说即使你分别通过 `require('express')` 和 `require('./node_modules/express')` 加载两次，也不会重复加载，因为尽管两次参数不同，解析到的文件却是同一个。

## 6.2 控制流

Node.js 的异步机制由事件和回调函数实现，一开始接触可能会感觉违反常规，但习惯以后就会发现还是很简单的。然而这之中其实暗藏了不少陷阱，一个很容易遇到的问题就是循环中的回调函数，初学者经常容易陷入这个圈套。

```JavaScript
//forloop.js
var fs = require('fs');
var files = ['a.txt', 'b.txt', 'c.txt'];
for (var i = 0; i < files.length; i++) {
  fs.readFile(files[i], 'utf-8', function(err, contents) {
    console.log(files[i] + ': ' + contents);
  });
}
// undefined: AAA
// undefined: BBB
// undefined: CCC
```

大多数情况下我们可以用数组的 forEach 方法解决这个问题：

```JavaScript
//callbackforeach.js
var fs = require('fs');
var files = ['a.txt', 'b.txt', 'c.txt'];
files.forEach(function(filename) {
  fs.readFile(filename, 'utf-8', function(err, contents) {
   console.log(filename + ': ' + contents);
  });
});
```

除了循环的陷阱， Node.js 异步式编程还有一个显著的问题，即深层的回调函数嵌套。在这种情况下，我们很难像看基本控制流结构一样一眼看清回调函数之间的关系，因此当程序规模扩大时必须采取手段降低耦合度，以实现更加优美、可读的代码。这个问题本身没有立竿见影的解决方法，只能通过改变设计模式，时刻注意降低逻辑之间的耦合关系来解决。

除此之外，还有许多项目试图解决这一难题。 async 是一个控制流解耦模块，它提供了async.series、 async.parallel、 async.waterfall 等函数，在实现复杂的逻辑时使用这些函数代替回调函数嵌套可以让程序变得更清晰可读且易于维护，但你必须遵循它的编程风格。

streamlinejs和jscex则采用了更高级的手段，它的思想是“变同步为异步”，实现了一个JavaScript 到JavaScript 的编译器，使用户可以用同步编程的模式写代码，编译后执行时却是异步的。

eventproxy 的思路与前面两者区别更大，它实现了对事件发射器的深度封装，采用一种完全基于事件松散耦合的方式来实现控制流的梳理。

## 6.3 Node.js应用部署

在开发的过程中，通过node app.js 命令运行服务器即可。但它不适合在产品环境下使用，为什么呢？因为到目前为止这个服务器还有几个重大缺陷。

- 不支持故障恢复
- 没有日志
- 无法利用多核提高性能
- 独占端口
- 需要手动启动

服务器的日志功能。Express 支持两种运行模式：开发模式和产品模式，前者的目的是利于调试，后者则是利于部署。使用产品模式运行服务器的方式很简单，只需设置 NODE_ENV 环境变量。通过 NODE_ENV=production node app.js 命令运行服务器可以看到。

```
Express server listening on port 3000 in production mode
```

接下来让我们实现访问日志和错误日志功能。访问日志就是记录用户对服务器的每个请求，包括客户端IP 地址，访问时间，访问路径，服务器响应以及客户端代理字符串。而错误日志则记录程序发生错误时的信息，由于调试中需要即时查看错误信息，将所有错误直接显示到终端即可，而在产品模式中，需要写入错误日志文件。

从0.6 版本开始， Node.js 提供了一个核心模块： cluster。 cluster的功能是生成与当前进程相同的子进程，并且允许父进程和子进程之间共享端口。 Node.js 的另一个核心模块child_process 也提供了相似的进程生成功能，但最大的区别在于cluster 允许跨进程端口复用，给我们的网络服务器开发带来了很大的方便。

共享80端口。默认的HTTP 端口是80，因此必须监听80端口才能使网址更加简洁。如果整个服务器只有一个网站，那么只需让app.js 监听80 端口即可。但很多时候一个服务器上运行着不止一个网站，尤其是还有用其他语言（如PHP）写成的网站，这该怎么办呢？此时虚拟主机可以粉墨登场了。虚拟主机，就是让多个网站共享使用同一服务器同一IP地址，通过域名的不同来划分请求。主流的HTTP服务器都提供了虚拟主机支持，如Nginx、 Apache、 IIS等。

## 6.4 Node.js不是银弹

Node.js 不适合做的事情。

计算密集型的程序。理想情况下，Node.js 单线程在执行的过程中会将一个 CPU 核心完全占满，所有的请求必须等待当前请求处理完毕以后进入事件循环才能响应。如果一个应用是计算密集型的，那么除非你手动将它拆散，否则请求响应延迟将会相当大。

单用户多任务型应用。如果面对的是单用户，譬如本地的命令行工具或者图形界面，那么所谓的大量并发请求就不存在了。但是用户提供界面的同时后台在进行某个计算，为了让用户界面不出现阻塞状态，不得不开启多线程或多进程。而Node.js 线程或进程之间的通信到目前为止还很不便，因为它根本没有锁，因而号称不会死锁。 Node.js 的多进程往往是在执行同一任务，通过多进程利用多处理器的资源，但遇到多进程相互协作时，就显得捉襟见肘了。

逻辑十分复杂的事务。Node.js 的控制流不是线性的，它被一个个事件拆散，但人的思维却是线性的。Node.js更善于处理那些逻辑简单但访问频繁的任务，而不适合完成逻辑十分复杂的工作。

Unicode与国际化。Node.js 不支持完整的Unicode，很多字符无法用string 表示。公平地说这不是Node.js 的缺陷，而是JavaScript 标准的问题。目前JavaScript 支持的字符集还是双字节的CS2，即用两个字节来表示一个Unicode 字符，这样能表示的字符数量是65536。

# 附录A JavaScript的高级特性

作用域。作用域（scope）是结构化编程语言中的重要概念，它决定了变量的可见范围和生命周期，正确使用作用域可以使代码更清晰、易懂。作用域可以减少命名冲突，而且是垃圾回收的基本单元。和 C、 C++、 Java 等常见语言不同， JavaScript 的作用域不是以花括号包围的块级作用域（block scope），这个特性经常被大多数人忽视，因而导致莫名其妙的错误。例如下面代码，在大多数类 C 的语言中会出现变量未定义的错误，而在 JavaScript 中却完全合法。

```JavaScript
if (true) {
var somevar = 'value';
}
console.log(somevar); // 输出 value
```

这是因为 JavaScript 的作用域完全是由函数来决定的， if、 for 语句中的花括号不是独立的作用域。

函数作用域。不同于大多数类 C 的语言，由一对花括号封闭的代码块就是一个作用域， JavaScript 的作用域是通过函数来定义的，在一个函数中定义的变量只对这个函数内部可见，我们称为函数作用域。在函数中引用一个变量时， JavaScript 会先搜索当前函数作用域，或者称为“局部作用域”，如果没有找到则搜索其上层作用域，一直到全局作用域。

有一点需要注意：函数作用域的嵌套关系是定义时决定的，而不是调用时决定的，也就是说， JavaScript 的作用域是静态作用域，又叫词法作用域，这是因为作用域的嵌套关系可以在语法分析时确定，而不必等到运行时确定。

在 JavaScript 中有一种特殊的对象称为 全局对象。这个对象在Node.js 对应的是 global 对象，在浏览器中对应的是 window 对象。由于全局对象的所有属性在任何地方都是可见的，所以这个对象又称为 全局作用域。全局作用域中的变量不论在什么函数中都可以被直接引用，而不必通过全局对象。

闭包。通俗地讲， JavaScript 中每个的函数都是一个闭包，但通常意义上嵌套的函数更能够体现出闭包的特性。

```JavaScript
var generateClosure = function() {
  var count = 0;
  var get = function() {
    count ++;
    return count;
  };
  return get;
};
var counter = generateClosure();
console.log(counter()); // 输出 1
console.log(counter()); // 输出 2
console.log(counter()); // 输出 3
```

这正是所谓闭包的特性。当一个函数返回它内部定义的一个函数时，就产生了一个闭包，闭包不但包括被返回的函数，还包括这个函数的定义环境。上面例子中，当函数generateClosure() 的内部函数 get 被一个外部变量 counter 引用时， counter 和 `generateClosure()` 的局部变量就是一个闭包。

```JavaScript
var generateClosure = function() {
  var count = 0;
  var get = function() {
    count ++;
    return count;
  };
  return get;
};
var counter1 = generateClosure();
var counter2 = generateClosure();
console.log(counter1()); // 输出 1
console.log(counter2()); // 输出 1
console.log(counter1()); // 输出 2
console.log(counter1()); // 输出 3
console.log(counter2()); // 输出 2
```

上面这个例子解释了闭包是如何产生的：counter1 和 counter2 分别调用了 generateClosure() 函数，生成了两个闭包的实例，它们内部引用的 count 变量分别属于各自的运行环境。

闭包的用途。闭包有两个主要用途，一是实现嵌套的回调函数，二是隐藏对象的细节。

对象。JavaScript 中的对象实际上就是一个由属性组成的关联数组，属性由名称和值组成，值的类型可以是任何数据类型，或者函数和其他对象。注意 JavaScript 具有函数式编程的特性，所以函数也是一种变量，大多数时候不用与一般的数据类型区分。

在 JavaScript 中，你可以用以下方法创建一个简单的对象：

```JavaScript
var foo = {};
foo.prop_1 = 'bar';
foo.prop_2 = false;
foo.prop_3 = function() {
  return 'hello world';
}
console.log(foo.prop_3());
```

# 附录B Node.js编程规范


