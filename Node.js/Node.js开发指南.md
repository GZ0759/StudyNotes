> Node.js开发指南
> 2012年7月第一版

# 第一章 Node.js简介

Node.js，或者 Node，可以让 JavaScript 脱离浏览器的束缚运行在一般的服务器环境下，从而轻松地进行服务器端应用开发。Node.js 是一个为实时 Web 应用开发而诞生的平台，它从诞生之初就充分考虑了在实时响应、超大规模数据要求下架构的可扩展性。这使得它摒弃了传统平台依靠多线程来实现高并发的设计思路，而采用了单线程、异步式I/O、事件驱动式的程序设计模型。这些特性不仅带来了巨大的性能提升，还减少了多线程程序设计的复杂性，进而提高了开发效率。

尽管它诞生的时间（ 2009年）还不长，但它的周围已经形成了一个庞大的生态系统。 Node.js 有着强大而灵活的包管理器（ node package manager， npm），目前已经有上万个第三方模块，其中有网站开发框架，有 MySQL、 PostgreSQL、 MongoDB 数据库接口，有模板语言解析、 CSS 生成工具、邮件、加密、图形、调试支持，甚至还有图形用户界面和操作系统 API工具。

## 1.1 Node.js 是什么 

Node.js 不是一种独立的语言，与 PHP、 Python、 Perl、 Ruby 的“既是语言也是平台”
不同。 Node.js 也不是一个 JavaScript 框架，不同于 CakePHP、 Django、 Rails。 Node.js 更不是浏览器端的库，不能与 jQuery、 ExtJS 相提并论。 Node.js 是一个让 JavaScript 运行在服务端的开发平台，它让 JavaScript 成为脚本语言世界的一等公民，在服务端堪与 PHP、 Python、Perl、 Ruby 平起平坐。

Node.js 是一个让 JavaScript 运行在浏览器之外的平台。它实现了诸如文件系统、模块、包、操作系统 API、网络通信等 Core JavaScript 没有或者不完善的功能。

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

Node.js 内建了 HTTP 服务器支持，也就是说可以轻而易举地实现一个网站和服务器
的组合。这和 PHP、 Perl 不一样，因为在使用 PHP 的时候，必须先搭建一个 Apache 之类的HTTP 服务器，然后通过 HTTP 服务器的模块加载或 CGI 调用，才能将 PHP 脚本的执行结果呈现给用户。而当你使用 Node.js 时，不用额外搭建一个 HTTP 服务器，因为 Node.js 本身就内建了一个。这个服务器不仅可以用来调试代码，而且它本身就可以部署到产品环境，它的性能足以满足要求。Node.js 还可以部署到非网络应用的环境下，比如一个命令行工具。 Node.js 还可以调用C/C++ 的代码，这样可以充分利用已有的诸多函数库，也可以将对性能要求非常高的部分用、C/C++ 来实现。

## 1.3 异步式 I/O 与事件驱动 

Node.js 最大的特点就是采用异步式 I/O 与事件驱动的架构设计。Node.js 使用的是单线程模型，对于所有 I/O 都采用异步式的请求方式，避免了频繁的上下文切换。Node.js 在执行的过程中会维护一个事件队列，程序在执行时进入事件循环等待下一个事件来，每个异步式 I/O 请求完成后回被推送到事件队列，等待程序进程进行处理。

传统的架构是多线程模型，也就是为每个业务逻辑提供一个系统线程，通过系统线程切换来弥补同步式 I/O 调用时的时间开销。对于高并发的访问，一方面线程长期阻塞等待，另一方面为了应付新请求而不断增加线程，因此会浪费大量系统资源，同时线程的增多也会占用大量的 CPU 时间来处理内存上下文切换，而且还容易遭受低速连接攻击。

Node.js 的异步机制是基于事件的，所有的磁盘 I/O、网络通信、数据库查询都以非阻塞的方式请求，返回的结果由事件循环来处理。 Node.js 进程在同一时刻只会处理一个事件，完成后立即进入事件循环检查并处理后面的事件。这样做的好处是，CPU 和内存在同一时间集中处理一件事，同时尽可能让耗时的 I/O 操作并行执行。对于低速连接攻击，Node.js 只是在事件队列中增加请求，等待操作系统的回应，因而不会有任何多线程开销，很大程度上可以提高 Web 应用的健壮性，防止恶意攻击。

## 1.4 Node.js 的性能 

Node.js 用异步式 I/O 和事件驱动代替多线程，带来了可观的性能提升。 Node.js 除了使用 V8 作为JavaScript引擎以外，还使用了高效的 libev 和 libeio 库支持事件驱动和异步式 I/O。

## 1.5 JavaScript 简史

网景公司与 liveScript。在1992年，一个叫 Nombas 的公司开发了“C减减”（ C minus minus， Cmm）语言，后来改名为 ScriptEase。 ScriptEase 最初的设计是将一种微型脚本语言与一个叫做 Espresso Page 的工具配合，使脚本能够在浏览器中运行，因此 ScriptEase 成为了第一个客户端脚本语言。网景公司也想独立开发一种与 ScriptEase 相似的客户端脚本语言，最终一个弱类型的动态解释语言 LiveWire 就此诞生。 LiveWire 没过多久就改名为 LiveScript 了。

Sun 公司与 JavaScript。在JavaScript 诞生之前， Java applet②曾经被热炒。之前 Sun 公司一直在不遗余力地推广Java，宣称 Java applet 将会改变人们浏览网页的方式。网景公司的市场部门抓住了这个机遇，与 Sun 合作完成了 LiveScript 实现，并在网景的 Navigator 2.0 发布前，将 LiveScript 更名为 JavaScript。

微软公司与 JScript。就在网景公司如日中天之时，微软的 Internet Explorer 3 随 Windows 95 OSR2 捆绑销售的策略堪称一颗重磅炸弹，轻松击败了强劲的对手——网景公司的Navigator。Internet Explorer 3 是一个划时代产品，因为它也实现了类似于 JavaScript 的客户端语言—— JScript，除此之外还有微软的“老本行” VBScript。 JScript 的诞生成为 JavaScript 发展的一个重要里程碑，标志了动态网页时代的全面到来。

标准化——ECMAScript。在1996年， JavaScript 标准由诸多软件厂商共同提交给ECMA（欧洲计算机制造商协会）。ECMA 通过了标准 ECMA-262，也就是 ECMAScript。紧接着国际标准化组织也采纳了 ECMAScript 标准（ ISO-16262）。在接下来的几年里，浏览器开发者们就开始以 ECMAScript 作为规范来实现 JavaScript 解析引擎。ECMAScript 仅仅是一个标准，而不是一个语言的具体实现，而且这个标准不像 C++ 语言规范那样严格而详细。除了 JavaScript 之外， ActionScript、QtScript、 WMLScript也是 ECMAScript 的实现。

浏览器兼容性问题。尽管有 ECMAScript 作为 JavaScript 的语法和语言特性标准，但是关于 JavaScript 其他方面的规范还是不明确，同时不同浏览器又加入了各自特有的对象、函数。这也就是为什么这么多年来同样的 JavaScript 代码会在不同的浏览器中呈现出不同的效果，甚至在一个浏览器中可以执行，而在另一个浏览器中却不可以。要注意的是，浏览器的兼容性问题并不只是由 JavaScript 的兼容性造成的，而是 DOM、BOM、 CSS 解析等不同的行为导致的。

引擎效率革命和 JavaScript 的未来。第一款 JavaScript 引擎是由 Brendan Eich 在网景的 Navigator 中开发的，它的名字叫做SpiderMonkey。Google Chrome 的JavaScript 引擎是 V8，同时 V8 也是 Node.js 的引擎。微软从 Internet Explorer 9 开始使用其新的 JavaScript 引擎 Chakra。 

## 1.6 CommonJS

服务器端 JavaScript 的重生。在JavaScript 诞生之初，网景公司就实现了服务端的 JavaScript，但由于需要支付一大笔授权费用才能使用，服务端 JavaScript 在当年并没有像客户端 JavaScript 一样流行开来。真正使大多数人见识到 JavaScript 在服务器开发威力的，是微软的 ASP。随着后来 LAMP 的兴起，以及Web 2.0 时代的到来， Ajax 等一系列概念的提出， JavaScript 成了前端开发的代名词，同时服务端 JavaScript 也逐渐被人遗忘。

直至几年前， JavaScript 的种种优势才被重新提起， JavaScript 又具备了在服务端流行的条件， Node.js 应运而生。与此同时， RingoJS 也基于 Rhino 实现了类似的服务端 JavaScript 平台，还有像 CouchDB、 MongoDB 等新型非关系型数据库也开始用 JavaScript 和 JSON 作为其数据操纵语言，基于 JavaScript 的服务端实现开始遍地开花。

Common.js 规范与实现。正如当年为了统一 JavaScript 语言标准，人们制定了 ECMAScript 规范一样，如今为了统一 JavaScript 在浏览器之外的实现， CommonJS 诞生了。 CommonJS 试图定义一套普通应用程序使用的API，从而填补 JavaScript 标准库过于简单的不足。 CommonJS 的终极目标是制定一个像 C++ 标准库一样的规范，使得基于 CommonJS API 的应用程序可以在不同的环境下运行，就像用 C++ 编写的应用程序可以使用不同的编译器和运行时函数库一样。为了保持中立， CommonJS 不参与标准库实现，其实现交给像 Node.js 之类的项目来完成。

CommonJS 规范包括了模块（ modules）、包（ packages）、系统（ system）、二进制（ binary）、控制台（ console）、编码（ encodings）、文件系统（ filesystems）、套接字（ sockets）、单元测试（ unit testing）等部分。Node.js 是目前 CommonJS 规范最热门的一个实现，它基于 CommonJS 的 Modules/1.0 规范实现了 Node.js 的模块，同时随着 CommonJS 规范的更新， Node.js 也在不断跟进。由于目前 CommonJS 大部分规范还在起草阶段， Node.js 已经率先实现了一些功能，并将其反馈给CommonJS 规范制定组织，但 Node.js 并不完全遵循 CommonJS 规范。这是所有规范制定者都会遇到的尴尬局面，因为规范的制定总是滞后于技术的发展。

# 第二章 安装和配置Node.js

# 第三章 Node.js快速入门

# 第四章 Node.js核心模块

# 第五章 使用Node.js进行Web开发

# 第六章 Node.js进阶话题

# 附录A JavaScript的高级特性

# 附录B Node.js编程规范
