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

编译源代码。Node.js 从 0.6 版本开始已经实现了源代码级别的跨平台，因此我们可以使用不同的编译
命令将同一份源代码的基础上编译为不同平台下的原生可执行代码。在编译之前，要先获取源码包。我们建议访问http://nodejs.org，点击Download链接，然后选择Source Code，下载正式发布的源码包。如果你需要开发中的版本，可以通过https://github.com/joyent/node/zipball/master 获得，或者在命令行下输入`git clone git://github.com/joyent/node.git` 从git获得最新的分支。

安装多版本管理器。迄今为止Node.js 更新速度还很快，有时候新版本还会将旧版本的一些 API 废除，以至于写好的代码不能向下兼容。有时候可能想要尝试一下新版本有趣的特性，但又想要保持一个相对稳定的环境。基于这种需求， Node.js 的社区开发了多版本管理器，用于在一台机器上维护多个版本的 Node.js 实例，方便按需切换。 Node 多版本管理器（ Node Version Manager， nvm）是一个通用的叫法，它目前有许多不同的实现。

n 是一个十分简洁的 Node 多版本管理器，就连它的名字也不例外。它的名字就是 n，
没错，就一个字母。 如果已经安装好了 Node.js 和 npm 环境，就可以直接使用`npm install -g n`命令来安装 n。如果想完全通过 n 来管理 Node.js，那么没安装之前哪来的 npm 呢？事实上， n 并不需要 Node.js 驱动，它只是 bash 脚本，使用 npm 安装只是采取一种简便的方式而已。我们可以在 https://github.com/visionmedia/n 下载它的代码，然后使用 make install 命令安装。

# 第三章 Node.js快速入门

## 3.1 开始用 Node.js 编程

输入 `node --help` 可以看到详细的帮助信息。

运行 Node.js 程序的基本方法就是执行 `node script.js`，其中 script.js 是脚本的文件名。

除了直接运行脚本文件外， `node --help` 显示的使用方法中说明了另一种输出 Hello
World 的方式：我们可以把要执行的语句作为 `node -e` 的参数直接执行。
```
$ node -e "console.log('Hello World');"
Hello World
```

使用 node 的 REPL 模式。REPL （ Read-eval-print loop），即输入—求值—输出循环。运行无参数的 node 将会启动一个 JavaScript 的交互式 shell。在任何时候，连续按两次 Ctrl + C 即可推出 Node.js 的 REPL 模式。node 提出的 REPL 在应用开发时会给人带来很大的便利，例如我们可以测试一个包能否正常使用，单独调用应用的某一个模块，执行简单的计算等。

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

## 3.2 异步式 I/O 与事件式编程

Node.js 最大的特点就是异步式 I/O（或者非阻塞 I/O）与事件紧密结合的编程模式。这种模式与传统的同步式 I/O 线性的编程思路有很大的不同，因为控制流很大程度上要靠事件和回调函数来组织，一个逻辑要拆分为若干个单元。

什么是阻塞（ block）呢？线程在执行中如果遇到磁盘读写或网络通信（统称为 I/O 操作），通常要耗费较长的时间，这时操作系统会剥夺这个线程的 CPU 控制权，使其暂停执行，同时将资源让给其他的工作线程，这种线程调度方式称为阻塞。当 I/O 操作完毕时，操作系统将这个线程的阻塞状态解除，恢复其对CPU的控制权，令其继续执行。这种 I/O 模式就是通常的同步式 I/O（ Synchronous I/O）或阻塞式 I/O （ Blocking I/O）。

相应地，异步式 I/O （ Asynchronous I/O）或非阻塞式 I/O （ Non-blocking I/O）则针对所有 I/O 操作不采用阻塞的策略。当线程遇到 I/O 操作时，不会以阻塞的方式等待 I/O 操作的完成或数据的返回，而只是将 I/O 请求发送给操作系统，继续执行下一条语句。当操作系统完成 I/O 操作时，以事件的形式通知执行 I/O 操作的线程，线程会在特定时候处理这个事件。为了处理异步 I/O，线程必须有事件循环，不断地检查有没有未处理的事件，依次予以处理。

阻塞模式下，一个线程只能处理一项任务，要想提高吞吐量必须通过多线程。而非阻塞模式下，一个线程永远在执行计算操作，这个线程所使用的 CPU 核心利用率永远是 100%，I/O 以事件的方式通知。在阻塞模式下，多线程往往能提高系统吞吐量，因为一个线程阻塞时还有其他线程在工作，多线程可以让 CPU 资源不被阻塞中的线程浪费。而在非阻塞模式下，线程不会被 I/O 阻塞，永远在利用 CPU。多线程带来的好处仅仅是在多核 CPU 的情
下利用更多的核，而 Node.js 的单线程也能带来同样的好处。这就是为什么 Node.js 使用了单线程、非阻塞的事件编程模式。

异步式 I/O 就是少了多线程的开销。对操作系统来说，创建一个线程的代价是十分昂贵的，需要给它分配内存、列入调度，同时在线程切换的时候还要执行内存换页， CPU 的缓存被清空，切换回来的时候还要重新从内存中读取信息，破坏了数据的局部性。 当然，异步式编程的缺点在于不符合人们一般的程序设计思维，容易让控制流变得晦涩难懂，给编码和调试都带来不小的困难。习惯传统编程模式的开发者在刚刚接触到大规模的异步式应用时往往会无所适从，但慢慢习惯以后会好很多。尽管如此，异步式编程还是较为困难，不过可喜的是现在已经有了不少专门解决异步式编程问题的库（如async）。

| 同步式 I/O（阻塞式） | 异步式 I/O（非阻塞式）   |
| ----- | --------- |
| 通过事件片分割和线程调度利用多核CPU | 通过功能划分利用多核CPU
| 需要由操作系统调度多线程使用多核 | CPU 可以将单进程绑定到单核 CPU
| 难以充分利用 | CPU 资源 可以充分利用 CPU 资源
| 内存轨迹大，数据局部性弱 | 内存轨迹小，数据局部性强
| 符合线性的编程思维 | 不符合传统编程思维

回调函数。Node.js 中，并不是所有的 API 都提供了同步和异步版本。 Node.js 不鼓励使用同步 I/O。

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

// 同步
var fs = require('fs');
var data = fs.readFileSync('file.txt', 'utf-8');
console.log(data);
console.log('end.');
```

事件。Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。在开发者看来，事件由 EventEmitter 对象提供。前面提到的 fs.readFile 和 http.createServer 的回调函数都是通过 EventEmitter 来实现的。

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

Node.js 在什么时候会进入事件循环呢？答案是 Node.js 程序由事件循环开始，到事件循环结束，所有的逻辑都是事件的回调函数，所以 Node.js 始终在事件循环中，程序入口就是事件循环第一个事件的回调函数。事件的回调函数在执行的过程中，可能会发出 I/O 请求或直接发射（ emit）事件，执行完毕后再返回事件循环，事件循环会检查事件队列中有没有未处理的事件，直到程序结束。

与其他语言不同的是， Node.js 没有显式的事件循环，类似 Ruby 的 EventMachine::run() 的函数在 Node.js 中是不存在的。 Node.js 的事件循环对开发者不可见， 由 libev 库实现。 libev 支持多种类型的事件，如 ev_io、 ev_timer、 ev_signal、 ev_idle 等，在 Node.js 中均被EventEmitter 封装。 libev 事件循环的每一次迭代，在 Node.js 中就是一次 Tick， libev 不断检查是否有活动的、可供检测的事件监听器，直到检测不到时才退出事件循环，进程结束。

## 3.3 模块和包

模块（ Module）和包（ Package）是 Node.js 最重要的支柱。开发一个具有一定规模的程序不可能只用一个文件，通常需要把各个功能拆分、封装，然后组合起来，模块正是为了实现这种方式而诞生的。在浏览器 JavaScript 中，脚本模块的拆分和组合通常使用 HTML 的script 标签来实现。 Node.js 提供了 require 函数来调用其他模块，而且模块都是基于文件的，机制十分简单。Node.js 的模块和包机制的实现参照了 CommonJS 的标准，但并未完全遵循。

模块和包是没有本质区别的，两个概念也时常混用。如果要辨析，那么可以把包理解成是实现了某个功能模块的集合，用于发布和维护。对使用者来说，模块和包的区别是透明的，因此经常不作区分。

什么是模块。模块是 Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个 Node.js 文件就是一个模块，这个文件可能是 JavaScript 代码、 JSON 或者编译过的 C/C++ 扩展。在前面章节的例子中，用到了 `var http = require('http')`， 其中 http 是 Node.js 的一个核心模块，其内部是用 C++ 实现的，外部用 JavaScript 封装。我们通过require 函数获取了这个模块，然后才能使用其中的对象。

创建及加载模块。Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口， require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。这种接口封装方式比许多语言要简洁得多，同时也不失优雅，未引入违反语义的特性，
符合传统的编程逻辑。因为 require 不会重复加载模块，也就是说无论调用多少次 require， 获得的模块都是同一个。

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

`process.stdout`是标准输出流，通常我们使用的 console.log() 向标准输出打印字符，而 process.stdout.write() 函数提供了更底层的接口。

`process.stdin`是标准输入流，初始时它是被暂停的，要想从标准输入读取数据，你必须恢复流，并手动编写流的事件响应函数。

`process.nextTick(callback)`的功能是为事件循环设置一项任务， Node.js 会在下次事件循环调响应时调用 callback。

console 用于提供控制台标准输出，它是由 Internet Explorer 的JScript引擎提供的调试工具，后来逐渐成为浏览器的事实标准。Node.js 沿用了这个标准，提供与习惯行为一致的 console 对象，用于向标准输出流或标准错误流输出字符。

`console.log()`：向标准输出流打印字符并以换行符结束。 console.log 接受若干个参数，如果只有一个参数，则输出这个参数的字符串形式。如果有多个参数，则以类似于 C 语言 printf() 命令的格式输出。第一个参数是一个字符串，如果没有参数，只打印一个换行。

`console.error()`：与 console.log() 用法相同，只是向标准错误流输出。

`console.trace()`：向标准错误流输出当前的调用栈。

## 4.2 常用工具util

util 是一个 Node.js 核心模块，提供常用函数的集合，用于弥补核心 JavaScript 的功能过于精简的不足。

`util.inherits(constructor, superConstructor)`是一个实现对象间原型继承的函数。

`util.inspect(object,[showHidden],[depth],[colors])`是一个将任意对象转换为字符串的方法，通常用于调试和错误输出。它至少接受一个参数 object，即要转换的对象。

## 4.3 事件驱动events

events 是 Node.js 最重要的模块，没有“之一”，原因是 Node.js 本身架构就是事件式的，而它提供了唯一的接口，所以堪称 Node.js 事件编程的基石。events 模块不仅用于用户代码与 Node.js 下层事件循环的交互，还几乎被所有的模块依赖。

事件发射器。events 模块只提供了一个对象：events:EventEmitter。EventEmitter 的核心就是事件发射与事件监听器功能的封装。EventEmitter 的每个事件由一个事件名和若干个参数组成，事件名是一个字符串，通常表达一定的语义。对于每个事件， EventEmitter 支持若干个事件监听器。当事件发射时，注册到这个事件的事件监听器被依次调用，事件参数作为回调函数参数传递。

- `EventEmitter.on(event, listener)` 为指定事件注册一个监听器，接受一个字
符串 event 和一个回调函数 listener。
- `EventEmitter.emit(event, [arg1], [arg2], [...])` 发射 event 事件，传
递若干可选参数到事件监听器的参数表。
- `EventEmitter.once(event, listener)` 为指定事件注册一个单次监听器，即
监听器最多只会触发一次，触发后立刻解除该监听器。
- `EventEmitter.removeListener(event, listener)` 移除指定事件的某个监听
器， listener 必须是该事件已经注册过的监听器。
- `EventEmitter.removeAllListeners([event])` 移除所有事件的所有监听器，
如果指定 event，则移除指定事件的所有监听器。

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

HTTP 服务器。http.Server 是 http 模块中的 HTTP 服务器对象，用 Node.js 做的所有基于 HTTP 协议的系统，如网站、社交应用甚至代理服务器，都是基于 http.Server 实现的。它提供了
一套封装级别很低的 API，仅仅是流控制和简单的消息解析，所有的高层功能都要通过它的接口来实现。

`http.ClientRequest` 是由 http.request 或 http.get 返回产生的对象，表示一个已经产生而且正在进行中的 HTTP 请求。它提供一个 response 事件，即 http.request 或 http.get 第二个参数指定的回调函数的绑定对象。

# 第五章 使用Node.js进行Web开发

# 第六章 Node.js进阶话题

# 附录A JavaScript的高级特性

# 附录B Node.js编程规范
