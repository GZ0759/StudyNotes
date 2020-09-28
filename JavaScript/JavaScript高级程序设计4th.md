> JavaScript 高级程序设计第四版  
> Professional JavaScript for Web Developers  
> [图灵程序设计丛书](https://www.ituring.com.cn/book/2472)

# 第 1 章 什么是 JavaScript

本章内容

- JavaScript 历史回顾
- JavaScript 是什么
- JavaScript 与 ECMAScript 的关系
- JavaScript 的不同版本

1995 年，JavaScript 问世。当时，它的主要用途是代替 Perl 等服务器端语言处理输入验证。在此之前，要验证某个必填字段是否已填写，或者某个输入的值是否有效，需要与服务器的一次往返通信。网景公司希望通过在其 Navigator 浏览器中加入 JavaScript 来改变这个局面。在那个普遍通过电话拨号上网的年代，由客户端处理某些基本的验证是让人兴奋的新功能。缓慢的网速让页面每次刷新都考验着人们的耐心。

从那时起，JavaScript 逐渐成为市面上所有主流浏览器的标配。如今，JavaScript 的应用也不再局限于数据验证，而是渗透到浏览器窗口及其内容的方方面面。JavaScript 已被公认为主流的编程语言，能够实现复杂的计算与交互，包括闭包、匿名（lambda）函数，甚至元编程等特性。不仅是桌面浏览器，手机浏览器和屏幕阅读器也支持 JavaScript，其重要性可见一斑。就连拥有自家客户端脚本语言 VBScript 的微软公司，也在其 Internet Explorer（以下简称 IE）浏览器最初的版本中包含了自己的 JavaScript 实现。

从简单的输入验证脚本到强大的编程语言，JavaScript 的崛起没有任何人预测到。它很简单，学会用只要几分钟；它又很复杂，掌握它要很多年。要真正学好用好 JavaScript，理解其本质、历史及局限性是非常重要的。

## 1.1 简短的历史回顾

随着 Web 日益流行，对客户端脚本语言的需求也越来越强烈。当时，大多数用户使用 28.8kbit/s 的调制解调器上网，但网页变得越来越大、越来越复杂。为验证简单的表单而需要大量与服务器的往返通信成为用户的痛点。想象一下，你填写完表单，单击“提交”按钮，等 30 秒处理，然后看到一条消息，告诉你有一个必填字段没填。网景在当时是引领技术革新的公司，它将开发一个客户端脚本语言来处理这种简单的数据验证提上了日程。

1995 年，网景公司一位名叫 Brendan Eich 的工程师，开始为即将发布的 Netscape Navigator 2 开发一个叫 Mocha（后来改名为 LiveScript）的脚本语言。当时的计划是在客户端和服务器端都使用它，它在服务器端叫 LiveWire。

为了赶上发布时间，网景与 Sun 公司结为开发联盟，共同完成 LiveScript 的开发。就在 Netscape Navigator 2 正式发布前，网景把 LiveScript 改名为 JavaScript，以便搭上媒体当时热烈炒作 Java 的顺风车。

由于 JavaScript 1.0 很成功，网景又在 Netscape Navigator 3 中发布了 1.1 版本。尚未成熟的 Web 的受欢迎程度创造了历史新高，而网景则稳居市场领导者的位置。这时候，微软决定向 IE 投入更多资源。就在 Netscape Navigator 3 发布后不久，微软发布了 IE3，其中包含自己名为 JScript（叫这个名字是为了避免与网景发生许可纠纷）的 JavaScript 实现。1996 年 8 月，微软重磅进入 Web 浏览器领域，这是网景永远的痛，但它代表 JavaScript 作为一门语言向前迈进了一大步。

微软的 JavaScript 实现意味着出现了两个版本的 JavaScript： Netscape Navigator 中的 JavaScript，以及 IE 中的 JScript。与 C 语言以及很多其他编程语言不同，JavaScript 还没有规范其语法或特性的标准，两个版本并存让这个问题更加突出了。随着业界担忧日甚，JavaScript 终于踏上了标准化的征程。

1997 年，JavaScript 1.1 作为提案被提交给欧洲计算机制造商协会（Ecma）。第 39 技术委员会（TC39）承担了“标准化一门通用、跨平台、厂商中立的脚本语言的语法和语义”的任务（参见 TC39-ECMAScript）。TC39 委员会由来自网景、Sun、微软、Borland、Nombas 和其他对这门脚本语言有兴趣的公司的工程师组成。他们花了数月时间打造出 ECMA-262，也就是 ECMAScript（发音为“ek-ma- script”）这个新的脚本语言标准。

1998 年，国际标准化组织（ISO）和国际电工委员会（IEC）也将 ECMAScript 采纳为标准（ISO/IEC-16262）。自此以后，各家浏览器均以 ECMAScript 作为自己 JavaScript 实现的依据，虽然具体实现各有不同。

## 1.2 JavaScript 实现

虽然 JavaScript 和 ECMAScript 基本上是同义词，但 JavaScript 远远不限于 ECMA-262 所定义的那样。没错，完整的 JavaScript 实现包含以下几个部分（见图 1-1）：

- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

图 1-1

### 1.2.1 ECMAScript

ECMAScript，即 ECMA-262 定义的语言，并不局限于 Web 浏览器。事实上，这门语言没有输入和输出之类的方法。ECMA-262 将这门语言作为一个基准来定义，以便在它之上再构建更稳健的脚本语言。Web 浏览器只是 ECMAScript 实现可能存在的一种宿主环境（host environment）。宿主环境提供 ECMAScript 的基准实现和与环境自身交互必需的扩展。扩展（比如 DOM）使用 ECMAScript 核心类型和语法，提供特定于环境的额外功能。其他宿主环境还有服务器端 JavaScript 平台 Node.js 和即将被淘汰的 Adobe Flash。

如果不涉及浏览器的话，ECMA-262 到底定义了什么？在基本的层面，它描述这门语言的如下部分：

- 语法
- 类型
- 语句
- 关键字保留字操作符
- 全局对象

ECMAScript 只是对实现这个规范描述的所有方面的一门语言的称呼。JavaScript 实现了 ECMAScript，而 Adobe ActionScript 同样也实现了 ECMAScript。

1.  ECMAScript 版本

ECMAScript 不同的版本以“edition”表示（也就是描述特定实现的 ECMA-262 的版本）。ECMA-262 最近的版本是第 10 版，发布于 2019 年 6 月。ECMA-262 的第 1 版本质上跟网景的 JavaScript 1.1 相同，只不过删除了所有浏览器特定的代码，外加少量细微的修 改。ECMA-262 要求支持 Unicode 标准（以支持多语言），而且对象要与平台无关（Netscape JavaScript 1.1 的对象不是这样，比如它的 Date 对象就依赖平台）。这也是 JavaScript 1.1 和 JavaScript1.2 不符合 ECMA-262 第 1 版要求的原因。

ECMA-262 第 2 版只是做了一些编校工作，主要是为了更新之后严格符合 ISO/IEC-16262 的要求，并没有增减或改变任何特性。 ECMAScript 实现通常不使用第 2 版来衡量符合性（conformance）。

ECMA-262 第 3 版第一次真正对这个标准进行更新，更新了字符串处理、错误定义和数值输出。此外还增加了对正则表达式、新的控制语句、 try / catch 异常处理的支持，以及为了更好地让标准国际化所做的少量修改。对很多人来说，这标志着 ECMAScript 作为一门真正的编程语言的时代终于到来了。 ECMA-262 第 4 版是对这门语言的一次彻底修订。作为对 JavaScript 在 Web 上日益成功的回应，开发者开始修订 ECMAScript 以满足全球 Web 开发日益增长的需求。为此，Ecma T39 再次被召集起来，以决定这门语言的未来。结果，他们制定的规范几乎在第 3 版基础上完全定义了一门新语言。第 4 版包括强类型变量、新语句和数据结构、真正的类和经典的继承，以及操作数据的新手段。

与此同时，TC39 委员会的一个子委员会也提出了另外一份提案，叫作“ECMAScript 3.1”，只对这门语言进行了较少的改进。这个子委员会的人认为第 4 版对这门语言来说跳跃太大了。因此，他们提出了一个改动较小的提案，只要在现有 JavaScript 引擎基础上做一些增改就可以实现。最终，ES3.1 子委员会赢得了 TC39 委员会的支持，ECMA-262 第 4 版在正式发布之前被放弃。

ECMAScript 3.1 变成了 ECMA-262 的第 5 版，于 2009 年 12 月 3 日正式发布。第 5 版致力于厘清第 3 版存在的歧义，也增加了新功能。新功能包括原生的解析和序列化 JSON 数据的 JSON 对象、方便继承和高级属性定义的方法，以及新的增强 ECMAScript 引擎解释和执行代码能力的严格模式。第 5 版在 2011 年 6 月发布了一个维护性修订版，这个修订版只更正了规范中的错误，并未增加任何新的语言或库特性。

ECMA-262 第 6 版，俗称 ES6、ES2015 或 ES Harmony（和谐版），于 2015 年 6 月发布。这一版包含了大概这个规范有史以来最重要的一批增强特性。ES6 正式支持了类、模块、迭代器、生成器、箭头函数、期约、反射、代理和众多新的数据类型。

ECMA-262 第 7 版，也称为 ES7 或 ES2016，于 2016 年 6 月发布。这次修订只包含少量语法层面的增强，如 Array.prototype.includes 和指数操作符。

ECMA-262 第 8 版，也称为 ES8、ES2017，完成于 2017 年 6 月。这一版主要增加了异步函数（async/await）、SharedArrayBuffer 及 Atomics API，以及 Object.values\(\) / Object.entries\(\) / Object.getOwnPropertyDescriptors\(\) 和字符串填充方法，另外明确支持对象字面量最后的逗号。

ECMA-262 第 9 版，也称为 ES9、ES2018，发布于 2018 年 6 月。这次修订包括异步迭代、剩余和扩展属性、一组新的正则表达式特性、 Promise finally\(\) ，以及模板字面量修订。

ECMA-262 第 10 版，也称为 ES10、ES2019，发布于 2019 年 6 月。这次修订增加了 Array.prototype.flat\(\) / flatMap\(\) 、 String.prototype.trimStart\(\) / trimEnd\(\) 、 Object.fromEntries\(\) 方法，以及 Symbol.prototype.description 属性，明确定义了 Function.prototype.toString\(\) 的返回值并固定了 Array.prototype.sort\(\) 的顺序。另外，这次修订解决了与 JSON 字符串兼容的问题，并定义了 catch 子句的可选绑定。

2. ECMAScript 符合性是什么意

ECMA-262 阐述了什么是 ECMAScript 符合性。要成为 ECMAScript 实现，必须满足下列条件：

- 支持 ECMA-262 中描述的所有“类型、值、对象、属性、函数，以及程序语法与语义”；
- 支持 Unicode 字符标准。

此外，符合性实现还可以满足下列要求。

增加 ECMA-262 中未提及的“额外的类型、值、对象、属性和函数”。ECMA-262 所说的这些额外内容主要指规范中未给出的新对象或对象的新属性。

支持 ECMA-262 中没有定义的“程序和正则表达式语法”（意思是允许修改和扩展内置的正则表达式特性）。

以上条件为实现开发者基于 ECMAScript 开发语言提供了极大的权限和灵活度，也是其广受欢迎的原因之一。

3.  浏览器对 ECMAScript 的支持

1996 年，Netscape Navigator 3 发布时包含了 JavaScript 1.1。 JavaScript 1.1 规范随后被提交给 Ecma，作为对新的 ECMA-262 标准的建议。随着 JavaScript 迅速走红，网景非常愿意开发 1.2 版。可是有个问题：Ecma 尚未接受网景的建议。

Netscape Navigator 3 发布后不久，微软推出了 IE3。IE 的这个版本包含了 JScript 1.0，本意是提供与 JavaScript 1.1 相同的功能。不过，由于缺少很多文档，而且还有不少重复性功能，JScript 1.0 远远没有 JavaScript 1.1 那么强大。

JScript 的再次更新出现在 IE4 中的 JScript 3.0（2.0 版是在 Microsoft Internet Information Server 3.0 中发布的，但从未包含在浏览器 中）。微软发新闻稿称 JScript 3.0 是世界上第一门真正兼容 Ecma 标准的脚本语言。当时 ECMA-262 还没制定完成，因此 JScript 3.0 遭受了与 JavaScript 1.2 同样的命运，它同样没有遵守最终的 ECMAScript 标准。

网景又在 Netscape Navigator 4.06 中将其 JavaScript 版本升级到 1.3，因此做到了与 ECMA-262 第 1 版完全兼容。JavaScript 1.3 增加了对 Unicode 标准的支持，并做到了所有对象都与平台无关，同时保留了 JavaScript 1.2 所有的特性。

后来，当网景以 Mozilla 项目的名义向公众发布其源代码时，人们都期待 Netscape Navigator 5 中会包含 JavaScript 1.4。可是，一个完全重新设计网景代码的激进决定导致了人们的希望落空。 JavaScript 1.4 只在 Netscape Enterprise Server 中作为服务器端语言发布了，从来就没有进入浏览器。

到了 2008 年，五大浏览器（IE、Firefox、Safari、Chrome 和 Opera）全部兼容 ECMA-262 第 3 版。IE8 率先实现 ECMA-262 第 5 版，并在 IE9 中完整支持。Firefox 4 很快也做到了。下表列出了主要的浏览器版本对 ECMAScript 的支持情况。

### 1.2.2 DOM

文档对象模型（DOM，Document Object Model）是一个应用编程接口（API），用于在 HTML 中使用扩展的 XML。DOM 将整个页面抽象为一组分层节点。HTML 或 XML 页面的每个组成部分都是一种节 点，包含不同的数据。比如下面的 HTML 页面：

```js
\<html> \<head> \<title>Sample Page\</title> \</head>

\<body> \<p> Hello World\!\</p> \</body> \</html>
```

这些代码通过 DOM 可以表示为一组分层节点，如图 1-2 所示。

图 1-2

DOM 通过创建表示文档的树，让开发者可以随心所欲地控制网页的内容和结构。使用 DOM API，可以轻松地删除、添加、替换、修改节点。

1.  为什么 DOM 是必需的

在 IE4 和 Netscape Navigator 4 支持不同形式的动态 HTML（DHTML）的情况下，开发者首先可以做到不刷新页面而修改页面外观和内容。这代表了 Web 技术的一个巨大进步，但也暴露了很大的问题。由于网景和微软采用不同思路开发 DHTML，开发者写一个 HTML 页面就可以在任何浏览器中运行的好日子就此终结。

为了保持 Web 跨平台的本性，必须要做点什么。人们担心如果无法控制网景和微软各行其是，那么 Web 就会发生分裂，导致人们面向浏览器开发网页。就在这时，万维网联盟（W3C，World Wide Web Consortium）开始了制定 DOM 标准的进程。

2.  DOM 级别

1998 年 10 月，DOM Level 1 成为 W3C 的推荐标准。这个规范由两个模块组成：DOM Core 和 DOM HTML。前者提供了一种映射 XML 文档，从而方便访问和操作文档任意部分的方式；后者扩展了前者，并增加了特定于 HTML 的对象和方法。

注意 DOM 并非只能通过 JavaScript 访问，而且确实被其他很多语言实现了。不过对于浏览器来说，DOM 就是使用 ECMAScript 实现的，如今已经成为 JavaScript 语言的一大组成部分。

DOM Level 1 的目标是映射文档结构，而 DOM Level 2 的目标则宽泛得多。这个对最初 DOM 的扩展增加了对（DHTML 早就支持的）鼠标和用户界面事件、范围、遍历（迭代 DOM 节点的方法）的支持，而且通过对象接口支持了层叠样式表（CSS）。另外， DOM Level 1 中的 DOM Core 也被扩展以包含对 XML 命名空间的支持。

DOM Level 2 新增了以下模块，以支持新的接口。

- DOM 视图：描述追踪文档不同视图（如应用 CSS 样式前后的文档）的接口。
- DOM 事件：描述事件及事件处理的接口。
- DOM 样式：描述处理元素 CSS 样式的接口。
- DOM 遍历和范围：描述遍历和操作 DOM 树的接口。

DOM Level 3 进一步扩展了 DOM，增加了以统一的方式加载和保存文档的方法（包含在一个叫 DOM Load and Save 的新模块中），还有验证文档的方法（DOM Validation）。在 Level 3 中，DOMCore 经过扩展支持了所有 XML 1.0 的特性，包括 XML Infoset、XPath 和 XML Base。

目前，W3C 不再按照 Level 来维护 DOM 了，而是作为 DOM Living Standard 来维护，其快照称为 DOM4。DOM4 新增的内容包括替代 Mutation Events 的 Mutation Observers。

注意 在阅读关于 DOM 的资料时，你可能会看到 DOM Level 0 的说法。注意，并没有一个标准叫“DOM Level 0”，这只是 DOM 历史中的一个参照点。DOM Level 0 可以看作 IE4 和 Netscape Navigator 4 中最初支持的 DHTML。

3.  其他 DOM

除了 DOM Core 和 DOM HTML 接口，有些其他语言也发布了自己的 DOM 标准。下面列出的语言是基于 XML 的，每一种都增加了该语言独有的 DOM 方法和接口：

- 可伸缩矢量图（SVG，Scalable Vector Graphics）
- 数学标记语言（MathML，Mathematical Markup Language）
- 同步多媒体集成语言（SMIL，Synchronized Multimedia Integration Language）

此外，还有一些语言开发了自己的 DOM 实现，比如 Mozilla 的 XML 用户界面语言（XUL，XML User Interface Language）。不过，只有前面列表中的语言是 W3C 推荐标准。

4. Web 浏览器对 DOM 的支持情况

DOM 标准在 Web 浏览器实现它之前就已经作为标准发布了。IE 在第 5 版中尝试支持 DOM，但直到 5.5 版才开始真正支持，该版本实现了 DOM Level 1 的大部分。IE 在第 6 版和第 7 版中都没有实现新特性，第 8 版中修复了一些问题。

网景在 Netscape 6（Mozilla 0.6.0）之前都不支持 DOM。Netscape 7 之后，Mozilla 把开发资源转移到开发 Firefox 浏览器上。Firefox 3+支持全部的 Level 1、几乎全部的 Level 2，以及 Level 3 的某些部分。（Mozilla 开发团队的目标是打造百分之百兼容标准的浏览器，他们的工作也得到了应有的回报。）

支持 DOM 是浏览器厂商的重中之重，每个版本发布都会改进支持度。下表展示了主流浏览器支持 DOM 的情况。

注意 上表中兼容性的状态会随时间而变化，其中的内容仅反映本书写作时的状态。

### 1.2.3 BOM

IE3 和 Netscape Navigator 3 提供了浏览器对象模型（BOM） API，用于支持访问和操作浏览器的窗口。使用 BOM，开发者可以操控浏览器显示页面之外的部分。而 BOM 真正独一无二的地方，当然也是问题最多的地方，就是它是唯一一个没有相关标准的 JavaScript 实现。

HTML5 改变了这个局面，这个版本的 HTML 以正式规范的形式涵盖了尽可能多的 BOM 特性。由于 HTML5 的出现，之前很多与 BOM 有关的问题都迎刃而解了。

总体来说，BOM 主要针对浏览器窗口和子窗口（frame），不过人们通常会把任何特定于浏览器的扩展都归在 BOM 的范畴内。比如，下面就是这样一些扩展：

弹出新浏览器窗口的能力；

- 移动、缩放和关闭浏览器窗口的能力；
- navigator 对象，提供关于浏览器的详尽信息；
- location 对象，提供浏览器加载页面的详尽信息；
- screen 对象，提供关于用户屏幕分辨率的详尽信息；
- performance 对象，提供浏览器内存占用、导航行为和时间统计的详尽信息；

对 cookie 的支持；

其他自定义对象，如 XMLHttpRequest 和 IE 的 ActiveXObject 。

因为在很长时间内都没有标准，所以每个浏览器实现的都是自己的 BOM。有一些所谓的事实标准，比如对于 window 对象和 navigator 对象，每个浏览器都会给它们定义自己的属性和方法。现在有了 HTML5，BOM 的实现细节应该会日趋一致。关于 BOM，本书会在第 12 章再专门详细介绍。

## 1.3 JavaScript 版本

作为网景的继承者，Mozilla 是唯一仍在延续最初 JavaScript 版本编号的浏览器厂商。当初网景在将其源代码开源时（项目名为 Mozilla Project），JavaScript 在其浏览器中最后的版本是 1.3。（前面提到过， 1.4 版是专门为服务器实现的。）因为 Mozilla Foundation 在持续开发 JavaScript，为它增加新特性、关键字和语法，所以 JavaScript 的版本号也在不断递增。下表展示了 Netscape/Mozilla 浏览器发布的历代 JavaScript 版本。

这种版本编号方式是根据 Firefox 4 要发布 JavaScript 2.0 决定的，在此之前版本号的每次递增，反映的是 JavaScript 实现逐渐接近 2.0 建议。虽然这是最初的计划，但 JavaScript 的发展让这个计划变得不可能。 JavaScript 2.0 作为一个目标已经不存在了，而这种版本号编排方式在 Firefox 4 发布后就终止了。

注意 Netscape/Mozilla 仍然沿用这种版本方案。而 IE 的 JScript 有不同的版本号规则。这些 JScript 版本与上表提到的 JavaScript 版本并不对应。此外，多数浏览器对 JavaScript 的支持，指的是实现 ECMAScript 和 DOM 的程度。

## 1.4 小结

JavaScript 是一门用来与网页交互的脚本语言，包含以下三个组成部分。

ECMAScript：由 ECMA-262 定义并提供核心功能。

文档对象模型（DOM）：提供与网页内容交互的方法和接口。浏览器对象模型（BOM）：提供与浏览器交互的方法和接口。

JavaScript 的这三个部分得到了五大 Web 浏览器（IE、Firefox、Chrome、Safari 和 Opera）不同程度的支持。所有浏览器基本上对 ES5（ECMAScript 5）提供了完善的支持，而对 ES6（ECMAScript 6）和 ES7（ECMAScript 7）的支持度也在不断提升。这些浏览器对 DOM 的支持各不相同，但对 Level 3 的支持日益趋于规范。HTML5 中收录的 BOM 会因浏览器而异，不过开发者仍然可以假定存在很大一部分公共特性。

# 第 2 章 HTML 中的 JavaScript

本章内容

使用 \<script> 元素

行内脚本与外部脚本的比较

文档模式对JavaScript有什么影响确保JavaScript不可用时的用户体验

将JavaScript引入网页，首先要解决它与网页的主导语言HTML的关系问题。在JavaScript早期，网景公司的工作人员希望在将JavaScript引入HTML页面的同时，不会导致页面在其他浏览器中渲染出问题。通过反复试错和讨论，他们最终做出了一些决定，并达成了向网页中引入通用脚本能力的共识。当初他们的很多工作得到了保留，并且最终形成了HTML规范。

1.  \<script> 元素

     将JavaScript插入HTML的主要方法是使用 \<script> 元素。这个元素是由网景公司创造出来，并最早在Netscape Navigator 2中实现的。后来，这个元素被正式加入到HTML规范。 \<script> 元素有下列8个属性。

  

     async ：可选。表示应该立即开始下载脚本，但不能阻止其他页面动作，比如下载资源或等待其他脚本加载。只对外部脚本文件有效。

     charset ：可选。使用 src 属性指定的代码字符集。这个属性很少使用，因为大多数浏览器不在乎它的值。 crossorigin ：可选。配置相关请求的CORS（跨源资源共 享）设置。默认不使用CORS。 crossorigin="anonymous" 配置文件请求不必设置凭据标

     志。 crossorigin="use-credentials" 设置凭据标志，意味着出站请求会包含凭据。

     defer ：可选。表示在文档解析和显示完成后再执行脚本是没有问题的。只对外部脚本文件有效。在IE7及更早的版本中，对行内脚本也可以指定这个属性。

     integrity ：可选。允许比对接收到的资源和指定的加密签名以验证子资源完整性（SRI，Subresource Intergrity）。如果接收到的资源的签名与这个属性指定的签名不匹配，则页面会报错，脚本不会执行。这个属性可以用于确保内容分发网络（CDN， Content Delivery Network）不会提供恶意内容。

     language ：废弃。最初用于表示代码块中的脚本语言

     （如 "JavaScript" 、 "JavaScript 1.2" 或 "VBScript" ）。大多数浏览器都会忽略这个属性，不应该再使用它。

     src ：可选。表示包含要执行的代码的外部文件。

     type ：可选。代替 language ，表示代码块中脚本语言的内容类型（也称MIME类型）。按照惯例，这个值始终都

     是 "text/javascript" ， 尽

     管 "text/javascript" 和 "text/ecmascript" 都已经废

     弃了。JavaScript文件的MIME类型通常是 "application/x- javascript" ，不过给type属性这个值有可能导致脚本被忽略。在非IE的浏览器中有效的其他值还

     有 "application/javascript" 和 "application/ecmas cript" 。如果这个值是 module ，则代码会被当成ES6模块，而且只有这时候代码中才能出现 import 和 export 关键字。

     使用 \<script> 的方式有两种：通过它直接在网页中嵌入

     JavaScript代码，以及通过它在网页中包含外部JavaScript文件。

     要嵌入行内JavaScript代码，直接把代码放在 \<script> 元素中就行：

  

     \<script>

     function sayHi\(\) \{ console.log\("Hi\!"\);

     \}

     \</script>

     包含在 \<script> 内的代码会被从上到下解释。在上面的例子中，被解释的是一个函数定义，并且该函数会被保存在解释器环境中。在 \<script> 元素中的代码被计算完成之前，页面的其余内容不会被加载，也不会被显示。

     在使用行内JavaScript代码时，要注意代码中不能出现字符串

     \</script> 。比如，下面的代码会导致浏览器报错：

  

     \<script>

     function sayScript\(\) \{ console.log\("\</script>"\);

     \}

     \</script>

     浏览器解析行内脚本的方式决定了它在看到字符串 \</script>时，会将其当成结束的 \</script> 标签。想避免这个问题，只需要转义字符“\\”1即可：

     1此处的转义字符指在JavaScript中使用反斜杠“ \\ ”来向文本字符串添加特殊字符。——编者注

  

     \<script>

     function sayScript\(\) \{ console.log\("\<\\/script>"\);

     \}

     \</script>

     这样修改之后，代码就可以被浏览器完全解释，不会导致任何错误。

     要包含外部文件中的JavaScript，就必须使用 src 属性。这个属性的值是一个URL，指向包含JavaScript代码的文件，比如：

  

     \<script src\="example.js"\>\</script>

     这个例子在页面中加载了一个名为example.js的外部文件。文件本身只需包含要放在 \<script> 的起始及结束标签中间的JavaScript代码。与解释行内JavaScript一样，在解释外部JavaScript文件时，页面也会阻塞。（阻塞时间也包含下载文件的时间。）在XHTML文档中，可以忽略结束标签，比如：

  

     \<script src\="example.js"/>

     以上语法不能在HTML文件中使用，因为它是无效的HTML，有些浏览器不能正常处理，比如IE。

  

     注意 按照惯例，外部JavaScript文件的扩展名是.js。这不是必需的，因为浏览器不会检查所包含JavaScript文件的扩展名。这就为使用服务器端脚本语言动态生成JavaScript代码，或者在浏览器中将JavaScript扩展语言（如TypeScript，或React的JSX）转译为JavaScript提供了可能性。不过要注意，服务器经常会根据文件扩展来确定响应的正确MIME类型。如果不打算使用.js扩展名，一定要确保服务器能返回正确的MIME类型。

     另外，使用了 src 属性的 \<script> 元素不应该再在

     \<script> 和 \</script> 标签中再包含其他JavaScript代码。如果两者都提供的话，则浏览器只会下载并执行脚本文件，从而忽略行内代码。

     \<script> 元素的一个最为强大、同时也备受争议的特性是，它可以包含来自外部域的JavaScript文件。跟 \<img> 元素很像，

     \<script> 元素的 src 属性可以是一个完整的URL，而且这个URL指向的资源可以跟包含它的HTML页面不在同一个域中，比如这个例子：

  

     \<script src[\=](http://www.somewhere.com/afile.js)"http://www.somewhere.com/afile.js"\>

     \</script>

     浏览器在解析这个资源时，会向 src 属性指定的路径发送一个

     GET 请求，以取得相应资源，假定是一个JavaScript文件。这个初始的请求不受浏览器同源策略限制，但返回并被执行的JavaScript则受限制。当然，这个请求仍然受父页面HTTP/HTTPS协议的限制。

     来自外部域的代码会被当成加载它的页面的一部分来加载和解 释。这个能力可以让我们通过不同的域分发JavaScript。不过，引用了放在别人服务器上的JavaScript文件时要格外小心，因为恶意的程序员随时可能替换这个文件。在包含外部域的JavaScript文件时，要确保该域是自己所有的，或者该域是一个可信的来源。 \<script> 标签的 integrity 属性是防范这种问题的一个武器，但这个属性也不是所有浏览器都支持。

     不管包含的是什么代码，浏览器都会按照 \<script> 在页面中出现的顺序依次解释它们，前提是它们没有使用 defer 和 async  属性。第二个 \<script> 元素的代码必须在第一个 \<script> 元素的代码解释完毕才能开始解释，第三个则必须等第二个解释完，以此类推。

     1.  标签占位符

      过去，所有 \<script> 元素都被放在页面的 \<head> 标签内，如下面的例子所示：

  

      \<\!DOCTYPE html>

      \<html>

      \<head>

      \<title>Example HTML Page\</title>

      \<script src\="example1.js"\>\</script>

      \<script src\="example2.js"\>\</script>

      \</head>

      \<body>

      \<\!-- 这里是页面内容 \-->

      \</body>

      \</html>

      这种做法的主要目的是把外部的CSS和JavaScript文件都集中放到一起。不过，把所有JavaScript文件都放在 \<head> 里，也就意味着必须把所有JavaScript代码都下载、解析和解释完成后，才能开始渲染页面（页面在浏览器解析到 \<body> 的起始标签时开始渲染）。对于需要很多JavaScript的页面，这会导致页面渲染的明显延迟，在此期间浏览器窗口完全空白。为解决这个问题，现代Web应用程序通常将所有JavaScript引用放在 \<body> 元素中的页面内容后面，如下面的例子所示：

  

      \<\!DOCTYPE html>

      \<html>

      \<head>

      \<title>Example HTML Page\</title>

      \</head>

      \<body>

      \<\!-- 这里是页面内容 \-->

      \<script src\="example1.js"\>\</script>

      \<script src\="example2.js"\>\</script>

      \</body>

      \</html>

      这样一来，页面会在处理JavaScript代码之前完全渲染页面。用户会感觉页面加载更快了，因为浏览器显示空白页面的时间短了。

     2.  推迟执行脚本

      HTML 4.01为 \<script> 元素定义了一个叫 defer 的属性。这个属性表示脚本在执行的时候不会改变页面的结构。因此，这个脚本

      完全可以在整个页面解析完之后再运行。在 \<script> 元素上设置

      defer 属性，会告诉浏览器应该立即开始下载，但执行应该推迟：

  

      \<\!DOCTYPE html>

      \<html>

      \<head>

      \<title>Example HTML Page\</title>

      \<script defer src\="example1.js"\>\</script>

      \<script defer src\="example2.js"\>\</script>

      \</head>

      \<body>

      \<\!-- 这里是页面内容 \-->

      \</body>

      \</html>

      虽然这个例子中的 \<script> 元素包含在页面的 \<head> 中，但它们会在浏览器解析到结束的 \</html> 标签后才会执行。HTML5规范要求脚本应该按照它们出现的顺序执行，因此第一个推迟的脚本会在第二个推迟的脚本之前执行，而且两者都会在 DOMContentLoaded 事件之前执行（关于事件，请参考第17章）。不过在实际当中，推迟执行的脚本不一定总会按顺序执行或者在

      DOMContentLoaded 事件之前执行，因此最好只包含一个这样的脚本。

      如前所述， defer 属性只对外部脚本文件才有效。这是HTML5中明确规定的，因此支持HTML5的浏览器会忽略行内脚本的 defer属性。IE4\~7展示出的都是旧的行为，IE8及更高版本则支持HTML5定义的行为。

      对 defer 属性的支持是从IE4、Firefox 3.5、Safari 5和Chrome 7开始的。其他所有浏览器则会忽略这个属性，按照通常的做法来处理脚本。考虑到这一点，还是把要推迟执行的脚本放在页面底部比较 好。

  

      注意 对于XHTML文档，指定 defer 属性时应该写成

      defer="defer" 。

     3.  异步执行脚本

      HTML5为 \<script> 元素定义了 async 属性。从改变脚本处理方式上看， async 属性与 defer 类似。当然，它们两者也都只适用于外部脚本，都会告诉浏览器立即开始下载。不过，与 defer不同的是，标记为 async 的脚本并不保证能按照它们出现的次序执行，比如：

  

      \<\!DOCTYPE html>

      \<html>

      \<head>

      \<title>Example HTML Page\</title>

      \<script async src\="example1.js"\>\</script>

      \<script async src\="example2.js"\>\</script>

      \</head>

      \<body>

      \<\!-- 这里是页面内容 \-->

      \</body>

      \</html>

      在这个例子中，第二个脚本可能先于第一个脚本执行。因此，重点在于它们之间没有依赖关系。给脚本添加 async 属性的目的是告诉浏览器，不必等脚本下载和执行完后再加载页面，同样也不必等到该异步脚本下载和执行后再加载其他脚本。正因为如此，异步脚本不应该在加载期间修改DOM。

      异步脚本保证会在页面的 load 事件前执行，但可能会在 DOMContentLoaded （参见第17章）之前或之后。Firefox 3.6、 Safari 5和Chrome 7支持异步脚本。使用 async 也会告诉页面你不会使用 document.write ，不过好的Web开发实践根本就不推荐使用这个方法。

  

      注意 对于XHTML文档，指定 async 属性时应该写成

      async="async" 。

     4.  动态加载脚本

      除了 \<script> 标签，还有其他方式可以加载脚本。因为 JavaScript可以使用DOM API，所以通过向DOM中动态添加 script元素同样可以加载指定的脚本。只要创建一个 script 元素并将其添加到DOM即可。

  

      let script \= document.createElement\('script'\); script.src \= 'gibberish.js'; document.head.appendChild\(script\);

      当然，在把 HTMLElement 元素添加到DOM且执行到这段代码之前不会发送请求。默认情况下，以这种方式创建的 \<script> 元素是以异步方式加载的，相当于添加了 async 属性。不过这样做可能会有问题，因为所有浏览器都支持 createElement\(\) 方法，但

      不是所有浏览器都支持 async 属性。因此，如果要统一动态脚本的加载行为，可以明确将其设置为同步加载：

  

      let script \= document.createElement\('script'\); script.src \= 'gibberish.js';

      script.async \= false; document.head.appendChild\(script\);

      以这种方式获取的资源对浏览器预加载器是不可见的。这会严重影响它们在资源获取队列中的优先级。根据应用程序的工作方式以及怎么使用，这种方式可能会严重影响性能。要想让预加载器知道这些动态请求文件的存在，可以在文档头部显式声明它们：

  

      \<link rel\="preload" href\="gibberish.js"\>

     5.  XHTML中的变化

      可扩展超文本标记语言（XHTML，Extensible HyperText Markup

      Language）是将HTML作为XML的应用重新包装的结果。与HTML不同，在XHTML中使用JavaScript必须指定 type 属性且值为 text/javascript ，HTML中则可以没有这个属性。XHTML虽然已经退出历史舞台，但实践中偶尔可能也会遇到遗留代码，为此本节稍作介绍。

      在XHTML中编写代码的规则比HTML中严格，这会影响使用

      \<script> 元素嵌入JavaScript代码。下面的代码块虽然在HTML中有效，但在XHML中是无效的。

  

      \<script type\="text/javascript"\> function compare\(a, b\) \{

      if \(a \< b\) \{

      console.log\("A is less than B"\);

      \} else if \(a \> b\) \{

      console.log\("A is greater than B"\);

      \} else \{

      console.log\("A is equal to B"\);

      \}

      \}

      \</script>

      在HTML中，解析 \<script> 元素会应用特殊规则。XHTML中则没有这些规则。这意味着 a \< b 语句中的小于号（ \< ）会被解释成一个标签的开始，并且由于作为标签开始的小于号后面不能有空 格，这会导致语法错误。

      避免XHTML中这种语法错误的方法有两种。第一种是把所有小于号（ \< ）都替换成对应的HTML实体形式（ \&lt; ）。结果代码就是这样的：

  

      \<script type\="text/javascript"\> function compare\(a, b\) \{

      if \(a \&lt; b\) \{

      console.log\("A is less than B"\);

      \} else if \(a \> b\) \{

      console.log\("A is greater than B"\);

      \} else \{

      console.log\("A is equal to B"\);

      \}

      \}

      \</script>

      这样代码就可以在XHTML页面中运行了。不过，缺点是会影响阅读。好在还有另一种方法。

      第二种方法是把所有代码都包含到一个CDATA块中。在 XHTML（及XML）中，CDATA块表示文档中可以包含任意文本的区块，其内容不作为标签来解析，因此可以在其中包含任意字符，包括小于号，并且不会引发语法错误。使用CDATA的格式如下：

  

      \<script type\="text/javascript"\>\<\!\[CDATA\[ function compare\(a, b\) \{

      if \(a \< b\) \{

      console.log\("A is less than B"\);

      \} else if \(a \> b\) \{

      console.log\("A is greater than B"\);

      \} else \{

      console.log\("A is equal to B"\);

      \}

      \}

      \]\]>\</script>

      在兼容XHTML的浏览器中，这样能解决问题。但在不支持

      CDATA块的非XHTML兼容浏览器中则不行。为此，CDATA标记必须使用JavaScript注释来抵消：

  

      \<script type\="text/javascript"\>

      //\<\!\[CDATA\[

      function compare\(a, b\) \{

      if \(a \< b\) \{

      console.log\("A is less than B"\);

      \} else if \(a \> b\) \{

      console.log\("A is greater than B"\);

      \} else \{

      console.log\("A is equal to B"\);

      \}

      \}

      //\]\]>

      \</script>

      这种格式适用于所有现代浏览器。虽然有点黑科技的味道，但它可以通过XHTML验证，而且对XHTML之前的浏览器也能优雅地降级。

  

      注意 XHTML模式会在页面的MIME类型被指定

      为 "application/xhtml+xml" 时触发。并不是所有浏览器都支持以这种方式送达的XHTML。

     6.  废弃的语法

自1995年Netscape 2发布以来，所有浏览器都将JavaScript作为默认的编程语言。 type 属性使用一个MIME类型字符串来标识

\<script> 的内容，但MIME类型并没有跨浏览器标准化。即使浏览器默认使用JavaScript，在某些情况下某个无效或无法识别的MIME类型也可能导致浏览器跳过（不执行）相关代码。因此，除非你使用

XHML或 \<script> 标签要求或包含非JavaScript代码，最佳做法是不指定 type 属性。

在最初采用 script 元素时，它标志着开始走向与传统HTML解析不同的流程。对这个元素需要应用特殊的解析规则，而这在不支持

JavaScript的浏览器（特别是Mosaic）中会导致问题。不支持的浏览器会把 \<script> 元素的内容输出到页面上，从而破坏页面的外观。

Netscape联合Mosaic拿出了一个解决方案，对不支持JavaScript的浏览器隐藏嵌入的JavaScript代码。最终方案是把脚本代码包含在一个

HTML注释中，像这样：

  

\<script>\<\!-- function sayHi\(\)\{

console.log\("Hi\!"\);

\}

//-->\</script>

使用这种格式，Mosaic等浏览器就可以忽略 \<script> 标签中的内容，而支持JavaScript的浏览器则必须识别这种模式，将其中的内容作为JavaScript来解析。

虽然这种格式仍然可以被所有浏览器识别和解析，但已经不再必要，而且不应该再使用了。在XHTML模式下，这种格式也会导致脚本被忽略，因为代码处于有效的XML注释当中。

1.  行内代码与外部文件

     虽然可以直接在HTML文件中嵌入JavaScript代码，但通常认为最佳实践是尽可能将JavaScript代码放在外部文件中。不过这个最佳实践并不是明确的强制性规则。推荐使用外部文件的理由如下。

     可维护性。JavaScript代码如果分散到很多HTML页面，会导致维护困难。而用一个目录保存所有JavaScript文件，则更容易维护，

     这样开发者就可以独立于使用它们的HTML页面来编辑代码。

     缓存。浏览器会根据特定的设置缓存所有外部链接的JavaScript文件，这意味着如果两个页面都用到同一个文件，则该文件只需下载一次。这最终意味着页面加载更快。

     适应未来。通过把JavaScript放到外部文件中，就不必考虑用

     XHTML或前面提到的注释黑科技。包含外部JavaScript文件的语法在HTML和XHTML中是一样的。

  

     在配置浏览器请求外部文件时，要重点考虑的一点是它们会占用多少带宽。在SPDY/HTTP2中，预请求的消耗已显著降低，以轻量、独立JavaScript组件形式向客户端送达脚本更具优势。

     比如，第一个页面包含如下脚本：

  

     \<script src\="mainA.js"\>\</script>

     \<script src\="component1.js"\>\</script>

     \<script src\="component2.js"\>\</script>

     \<script src\="component3.js"\>\</script>

     ...

     后续页面可能包含如下脚本：

  

     \<script src\="mainB.js"\>\</script>

     \<script src\="component3.js"\>\</script>

     \<script src\="component4.js"\>\</script>

     \<script src\="component5.js"\>\</script>

     ...

     在初次请求时，如果浏览器支持SPDY/HTTP2，就可以从同一个地方取得一批文件，并将它们逐个放到浏览器缓存中。从浏览器角度看，通过SPDY/HTTP2获取所有这些独立的资源与获取一个大 JavaScript文件的延迟差不多。

     在第二个页面请求时，由于你已经把应用程序切割成了轻量可缓存的文件，第二个页面也依赖的某些组件此时已经存在于浏览器缓存中了。

     当然，这里假设浏览器支持SPDY/HTTP2，只有比较新的浏览器才满足。如果你还想支持那些比较老的浏览器，可能还是用一个大文件更合适。

2.  文档模式

     IE5.5发明了文档模式的概念，即可以使用 doctype 切换文档模式。最初的文档模式有两种：混杂模式（quirks mode）和标准模式

     （standards mode）。前者让IE像IE5一样（支持一些非标准的特

     性），后者让IE具有兼容标准的行为。虽然这两种模式的主要区别只体现在通过CSS渲染的内容方面，但对JavaScript也有一些关联影响，或称为副作用。本书会经常提到这些副作用。

     IE初次支持文档模式切换以后，其他浏览器也跟着实现了。随着浏览器的普遍实现，又出现了第三种文档模式：准标准模式（almost standards mode）。这种模式下的浏览器支持很多标准的特性，但是没有标准规定得那么严格。主要区别在于如何对待图片元素周围的空白

     （在表格中使用图片时最明显）。

     混杂模式在所有浏览器中都以省略文档开头的 doctype 声明作为开关。这种约定并不合理，因为混杂模式在不同浏览器中的差异非常大，不使用黑科技基本上就没有浏览器一致性可言。

     标准模式通过下列几种文档类型声明开启：

     \<\!-- HTML 4.01 Strict \-->

     \<\!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"

     ["http://www.w3.org/TR/html4/strict.dtd">](http://www.w3.org/TR/html4/strict.dtd)

  

     \<\!-- XHTML 1.0 Strict \-->

     \<\!DOCTYPE html PUBLIC

     ["-//W3C//DTD XHTML 1.0 Strict//EN"](http://www.w3.org/TR/xhtml1/DTD/xhtml1-) "http://www.w3.org/TR/xhtml1/DTD/xhtml1- strict.dtd">

     \<\!-- HTML5 \-->

     \<\!DOCTYPE html>

     准标准模式通过过渡性文档类型（ Transitional ）和框架集文档类型（ Frameset ）来触发：

  

     \<\!-- HTML 4.01 Transitional \-->

     \<\!DOCTYPE HTML PUBLIC

     ["-//W3C//DTD HTML 4.01 Transitional//EN"](http://www.w3.org/TR/html4/loose.dtd) ["http://www.w3.org/TR/html4/loose.dtd">](http://www.w3.org/TR/html4/loose.dtd)

  

     \<\!-- HTML 4.01 Frameset \-->

     \<\!DOCTYPE HTML PUBLIC

     ["-//W3C//DTD HTML 4.01 Frameset//EN"](http://www.w3.org/TR/html4/frameset.dtd) ["http://www.w3.org/TR/html4/frameset.dtd">](http://www.w3.org/TR/html4/frameset.dtd)

  

     \<\!-- XHTML 1.0 Transitional \-->

     \<\!DOCTYPE html PUBLIC

     ["-//W3C//DTD XHTML 1.0 Transitional//EN"](http://www.w3.org/TR/xhtml1/DTD/xhtml1-) "http://www.w3.org/TR/xhtml1/DTD/xhtml1- transitional.dtd">

  

     \<\!-- XHTML 1.0 Frameset \-->

     \<\!DOCTYPE html PUBLIC

     ["-//W3C//DTD XHTML 1.0 Frameset//EN"](http://www.w3.org/TR/xhtml1/DTD/xhtml1-) "http://www.w3.org/TR/xhtml1/DTD/xhtml1- frameset.dtd">

     准标准模式与标准模式非常接近，很少需要区分。人们在说到“标准模式”时，可能指其中任何一个。而对文档模式的检测（本书后面会讨论）也不会区分它们。本书后面所说的标准模式，指的就是除混杂模式以外的模式。

3.  \<noscript> 元素

     针对早期浏览器不支持JavaScript的问题，需要一个页面优雅降级的处理方案。最终， \<noscript> 元素出现，被用于给不支持 JavaScript的浏览器提供替代内容。虽然如今的浏览器已经100\%支持 JavaScript，但对于禁用JavaScript的浏览器来说，这个元素仍然有它的用处。

     \<noscript> 元素可以包含任何可以出现在 \<body> 中的 HTML元素， \<script> 除外。在下列两种情况下，浏览器将显示包含在 \<noscript> 中的内容：

     浏览器不支持脚本；

     浏览器对脚本的支持被关闭。

     任何一个条件被满足，包含在 \<noscript> 中的内容就会被渲染。否则，浏览器不会渲染 \<noscript> 中的内容。

     下面是一个例子：

  

     \<\!DOCTYPE html>

     \<html>

     \<head>

     \<title>Example HTML Page\</title>

     \<script ""defer\="defer" src\="example1.js"\>

     \</script>

     \<script ""defer\="defer" src\="example2.js"\>

     \</script>

     \</head>

     \<body>

     \<noscript>

     \<p>This page requires a JavaScript-enabled browser.\</p>

     \</noscript>

     \</body>

     \</html>

     这个例子是在脚本不可用时让浏览器显示一段话。如果浏览器支持脚本，则用户永远不会看到它。

4.  小结

JavaScript是通过 \<script> 元素插入到HTML页面中的。这个元素可用于把JavaScript代码嵌入到HTML页面中，跟其他标记混合在

一起，也可用于引入保存在外部文件中的JavaScript。本章的重点可以总结如下。

  

要包含外部JavaScript文件，必须将 src 属性设置为要包含文件的URL。文件可以跟网页在同一台服务器上，也可以位于完全不同的域。

所有 \<script> 元素会依照它们在网页中出现的次序被解释。在不使用 defer 和 async 属性的情况下，包含在 \<script>元素中的代码必须严格按次序解释。

对不推迟执行的脚本，浏览器必须解释完位于 \<script> 元素中的代码，然后才能继续渲染页面的剩余部分。为此，通常应该把 \<script> 元素放到页面末尾，介于主内容之后及

\</body> 标签之前。

可以使用 defer 属性把脚本推迟到文档渲染完毕后再执行。推迟的脚本总是按照它们被列出的次序执行。

可以使用 async 属性表示脚本不需要等待其他脚本，同时也不阻塞文档渲染，即异步加载。异步脚本不能保证按照它们在页面中出现的次序执行。

通过使用 \<noscript> 元素，可以指定在浏览器不支持脚本时显示的内容。如果浏览器支持并启用脚本，则 \<noscript> 元素中的任何内容都不会被渲染。


# 第 3 章 语言基础

# 第 4 章 变量、作用域与内存

# 第 5 章 基本引用类型

# 第 6 章 集合引用类型

# 第 7 章 迭代器与生成器

# 第 8 章 对象、类与面向对象编程

# 第 9 章 代理与反射

# 第 10 章 函数

# 第 11 章 期约与异步函数

# 第 12 章 BOM

# 第 13 章 客户端检测

# 第 14 章 DOM

# 第 15 章 DOM 扩展

# 第 16 章 DOM2 和 DOM3

# 第 17 章 事件

# 第 18 章 动画与 Canvas 图形

# 第 19 章 表单脚本

# 第 20 章 JavaScript API

# 第 21 章 错误处理与调试

# 第 22 章 处理 XML

# 第 23 章 JSON

# 第 24 章 网络请求与远程资源

# 第 25 章 客户端存储

# 第 26 章 模块

# 第 27 章 工作者线程

# 第 28 章 最佳实践

# 附录 A ES2018 和 ES2019

# 附录 B 严格模式

# 附录 C JavaScript 库和框架

# 附录 D JavaScript 工具
