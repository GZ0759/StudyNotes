> JavaScript高级程序设计第三版  
> Professional JavaScript for Web Developers  
> 2012年3月第一次出版  
> [看云笔记](https://www.kancloud.cn/crossken/professional_js_web_developers/207402)

# 第 1 章 JavaScript 简介　

JavaScript 诞生于 1995 年。当时，它的主要目的是处理以前由服务器端语言（如 Perl）负责的一些输入验证操作。

如今， JavaScript 的用途早已不再局限于简单的数据验证，而是具备了与浏览器窗口及其内容等几乎所有方面交互的能力。

## 1.1 JavaScript 简史　

当时就职于 Netscape 公司的布兰登·艾奇（ Brendan Eich），开始着手为计划于 1995 年 2 月发布的 Netscape Navigator 2 开发一种名为 LiveScript 的脚本语言——该语言将同时在浏览器和服务器中使用（它在服务器上的名字叫 LiveWire）。为了赶在发布日期前完成 LiveScript 的开发， Netscape 与 Sun 公司建立了一个开发联盟。在 Netscape Navigator 2 正式发布前夕， Netscape 为了搭上媒体热炒 Java 的顺风车，临时把 LiveScript 改名为 JavaScript。

ECMAScript 是一种由 Ecma 国际（前身为欧洲计算机制造商协会,英文名称是 European Computer Manufacturers Association）通过 ECMA-262 标准化的脚本程序设计语言。这种语言在万维网上应用广泛，它往往被称为 JavaScript 或 JScript，但实际上后两者是 ECMA-262 标准的实现和扩展。

## 1.2 JavaScript 实现　

一个完整的 JavaScript 实现应该由下列三个不同的部分组成。

- 核心（ECMAScript）
- 文档对象模型（DOM）
- 浏览器对象模型（BOM）

### 1.2.1 ECMAScript

由 ECMA-262 定义的 ECMAScript 与 Web 浏览器没有依赖关系。实际上，这门语言本身并不包含输入和输出定义。 ECMA-262 定义的只是这门语言的基础，而在此基础之上可以构建更完善的脚本语言。我们常见的 Web 浏览器只是 ECMAScript 实现可能的宿主环境之一。宿主环境不仅提供基本的 ECMAScript 实现，同时也会提供该语言的扩展，以便语言与环境之间对接交互。而这些扩展——如 DOM，则利用 ECMAScript 的核心类型和语法提供更多更具体的功能，以便实现针对环境的操作。其他宿主环境包括 Node（一种服务端 JavaScript 平台）和 Adobe Flash。

既然 ECMA-262 标准没有参照 Web 浏览器，那它都规定了些什么内容呢？大致说来，它规定了这门语言的下列组成部分：

- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
- 对象

### 1.2.2 文档对象模型（ DOM）

文档对象模型（ DOM， Document Object Model）是针对 XML 但经过扩展用于 HTML 的应用程序编程接口（ API， Application Programming Interface）。 DOM 把整个页面映射为一个多层节点结构。 HTML 或 XML 页面中的每个组成部分都是某种类型的节点，这些节点又包含着不同类型的数据。

DOM1 级（ DOM Level 1）于 1998 年 10 月成为 W3C 的推荐标准。 DOM1 级由两个模块组成： DOM 核心（ DOM Core）和 DOM HTML。其中， DOM 核心规定的是如何映射基于 XML 的文档结构，以便简化对文档中任意部分的访问和操作。 DOM HTML 模块则在 DOM 核心的基础上加以扩展，添加了针对 HTML 的对象和方法。

如果说 DOM1 级的目标主要是映射文档的结构，那么 DOM2 级的目标就要宽泛多了。 DOM2 级在原来 DOM 的基础上又扩充了（ DHTML 一直都支持的）鼠标和用户界面事件、范围、遍历（迭代 DOM 文档的方法）等细分模块，而且通过对象接口增加了对 CSS（ Cascading Style Sheets，层叠样式表）的支持。 DOM1 级中的 DOM 核心模块也经过扩展开始支持 XML 命名空间。DOM2 级引入了下列新模块，也给出了众多新类型和新接口的定义

- DOM 视图（ DOM Views）：定义了跟踪不同文档（例如，应用 CSS 之前和之后的文档）视图的接口；
- DOM 事件（ DOM Events）：定义了事件和事件处理的接口；
- DOM 样式（ DOM Style）：定义了基于 CSS 为元素应用样式的接口；
- DOM 遍历和范围（ DOM Traversal and Range）：定义了遍历和操作文档树的接口。

DOM3 级则进一步扩展了 DOM，引入了以统一方式加载和保存文档的方法——在 DOM 加载和保存（ DOM Load and Save）模块中定义；新增了验证文档的方法——在 DOM 验证（ DOM Validation）模块中定义。 DOM3 级也对 DOM 核心进行了扩展，开始支持 XML 1.0 规范，涉及 XML Infoset、 XPath 和 XML Base。

### 1.2.3 浏览器对象模型（ BOM）

浏览器对象模型（BOM）。可以访问和操作浏览器窗口，使用 BOM 可以控制浏览器显示的页面以外的部分。从本质上来说，BOM 只处理浏览器窗口和框架，但是人们习惯把所有针对浏览器的 JavaScript 扩展算作 BOM 的一部分。

- 弹出新浏览器窗口的功能；
- 移动、缩放和关闭浏览器窗口的功能；
- 提供浏览器详细信息的 navigator 对象；
- 提供浏览器所加载页面的详细信息的 location 对象；
- 提供用户显示器分辨率详细信息的 screen 对象；
- 对 cookies 的支持；
- 像 XMLHttpRequest 和 IE 的 ActiveXObject 这样的自定义对象。

1.3 JavaScript 版本　

## 1.4 小结

JavaScript 是一种专为与网页交互而设计的脚本语言，由下列三个不同的部分组成：

- ECMAScript，由 ECMA-262 定义，提供核心语言功能；
- 文档对象模型（ DOM），提供访问和操作网页内容的方法和接口；
- 浏览器对象模型（ BOM），提供与浏览器交互的方法和接口。

JavaScript 的这三个组成部分，在当前五个主要浏览器（ IE、 Firefox、 Chrome、 Safari 和 Opera）中都得到了不同程度的支持。其中，所有浏览器对 ECMAScript 第 3 版的支持大体上都还不错，而对 ECMAScript 5 的支持程度越来越高，但对 DOM 的支持则彼此相差比较多。对已经正式纳入 HTML5 标准的 BOM 来说，尽管各浏览器都实现了某些众所周知的共同特性，但其他特性还是会因浏览器而异。

# 第 2 章 在 HTML 中使用 JavaScript 　

只要一提到把 JavaScript 放到网页中，就不得不涉及 Web 的核心语言——HTML。在当初开发 JavaScript 的时候， Netscape 要解决的一个重要问题就是如何做到让 JavaScript 既能与 HTML 页面共存，又不影响那些页面在其他浏览器中的呈现效果。经过尝试、纠错和争论，最终的决定就是为 Web 增加统一的脚本支持。而 Web 诞生早期的很多做法也都保留了下来，并被正式纳入 HTML 规范当中。

## 2.1 \<script\>元素　

向 HTML 页面中插入 JavaScript 的主要方法，就是使用`<script>`元素。HTML 4.01 为`<script>`定义了六个属性。

- `async`：可选。异步，表示应该立即下载脚本，但不应妨碍页面中的其他操作。
- `charset`：可选。表示通过 src 属性指定的代码的字符集。
- `defer`：可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。
- `language`：已废弃。
- `src`：可选。表示包含要执行代码的外部文件。
- `type`：可选。可以看成是 language 的替代属性；表示编写代码使用的脚本语言的内容类型（也称为 MIME 类型）

使用`<script>`元素的方式有两种：直接在页面中嵌入 JavaScript 代码和包含外部 JavaScript 文件。

在使用`<script>`元素嵌入 JavaScript 代码时，只须为`<script>`指定 type 属性。然后，像下面这样把 JavaScript 代码直接放在元素内部即可：

```html
<script type="text/javascript">
  function sayHi() {
    alert("Hi!");
  }
</script>
```

包含在`<script>`元素内部的 JavaScript 代码将被从上至下依次解释。就拿前面这个例子来说，解释器会解释一个函数的定义，然后将该定义保存在自己的环境当中。在解释器对`<script>`元素内部的所有代码求值完毕以前，页面中的其余内容都不会被浏览器加载或显示。

在使用`<script>`嵌入 JavaScript 代码时，记住不要在代码中的任何地方出现`</script>`字符串。例如，浏览器在加载下面所示的代码时就会产生一个错误：

```html
<script type="text/javascript">
  function sayScript(){
    alert("</script>");
  }
</script>
```

因为按照解析嵌入式代码的规则，当浏览器遇到字符串`</script>`时，就会认为那是结束的`</script>`标签。而通过转义字符“/”可以解决这个问题，例如：

```html
<script type="text/javascript">
  function sayScript() {
    alert("<\/script>");
  }
</script>
```

这样写代码浏览器可以接受，因而也就不会导致错误了。

如果要通过`<script>`元素来包含外部 JavaScript 文件，那么 src 属性就是必需的。这个属性的值是一个指向外部 JavaScript 文件的链接，例如：

```html
<script type="text/javascript" src="example.js"></script>
```

在这个例子中，外部文件 example.js 将被加载到当前页面中。外部文件只须包含通常要放在开始的`<script>`和结束的`</script>`之间的那些 JavaScript 代码即可。与解析嵌入式 JavaScript 代码一样，在解析外部 JavaScript 文件（包括下载该文件）时，页面的处理也会暂时停止。如果是在 XHTML 文档中，也可以省略前面示例代码中结束的`</script>`标签，例如：

```html
<script type="text/javascript" src="example.js" />
```

但是，不能在 HTML 文档使用这种语法。原因是这种语法不符合 HTML 规范，而且也得不到某些浏览器（尤其是 IE）的正确解析。

需要注意的是，带有 src 属性的`<script>`元素不应该在其`<script>`和`</script>`标签之间再包含额外的 JavaScript 代码。如果包含了嵌入的代码，则只会下载并执行外部脚本文件，嵌入的代码会被忽略。

另外，通过`<script>`元素的 src 属性还可以包含来自外部域的 JavaScript 文件。这一点既让`<script>`元素倍显强大，又让它备受争议。在这一点上， `<script>`与`<img>`元素非常相似， 即它的 src 属性可以是指向当前 HTML 页面所在域之外的某个域中的完整 URL，例如：

```html
<script type="text/javascript" src="http://www.somewhere.com/afile.js"></script>
```

这样，位于外部域中的代码也会被加载和解析，就像这些代码位于加载它们的页面中一样。利用这一点就可以在必要时通过不同的域来提供 JavaScript 文件。不过，在访问自己不能控制的服务器上的 JavaScript 文件时则要多加小心。如果不幸遇到了怀有恶意的程序员，那他们随时都可能替换该文件中的代码。因此，如果想包含来自不同域的代码，则要么你是那个域的所有者，要么那个域的所有者值得信赖。

无论如何包含代码，只要不存在 defer 和 async 属性，浏览器都会按照`<script>`元素在页面中出现的先后顺序对它们依次进行解析。换句话说，在第一个`<script>`元素包含的代码解析完成后，第二个`<script>`包含的代码才会被解析，然后才是第三个、第四个……

### 2.1.1 标签的位置

标签的位置。按照传统的做法，所有`<script>`元素都应该放在页面的`<head>`元素中。这种做法的目的是把所有外部文件的引用都放在相同的地方。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </head>
  <body>
    <!-- 这里放内容 -->
  </body>
</html>
```

这种做法的目的就是把所有外部文件（包括 CSS 文件和 JavaScript 文件）的引用都放在相同的地方。可是，在文档的`<head>`元素中包含所有 JavaScript 文件，意味着必须等到全部 JavaScript 代码都被下载、解析和执行完成以后，才能开始呈现页面的内容（浏览器在遇到`<body>`标签时才开始呈现内容）。对于那些需要很多 JavaScript 代码的页面来说，这无疑会导致浏览器在呈现页面时出现明显的延迟，而延迟期间的浏览器窗口中将是一片空白。为了避免这个问题，现代 Web 应用程序一般都把全部 JavaScript 引用放在`<body>`元素中页面内容的后面，如下例所示：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
  </head>
  <body>
    <!-- 这里放内容 -->
    <script type="text/javascript" src="example1.js"></script>
    <script type="text/javascript" src="example2.js"></script>
  </body>
</html>
```

这样，在解析包含的 JavaScript 代码之前，页面的内容将完全呈现在浏览器中。而用户也会因为浏览器窗口显示空白页面的时间缩短而感到打开页面的速度加快了。

### 2.1.2 延迟脚本

HTML 4.01 为`<script>`标签定义了 defer 属性。这个属性的用途是表明脚本在执行时不会影响页面的构造。也就是说，脚本会被延迟到整个页面都解析完毕后再运行。因此，在`<script>`元素中设置 defer 属性，相当于告诉浏览器立即下载，但延迟执行。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
  </head>
  <body>
    <!-- 这里放内容 -->
  </body>
</html>
```

在这个例子中，虽然我们把`<script>`元素放在了文档的`<head>`元素中，但其中包含的脚本将延迟到浏览器遇到`</html>`标签后再执行。 HTML5 规范要求脚本按照它们出现的先后顺序执行，因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于 DOMContentLoaded 事件（详见第 13 章）执行。在现实当中，延迟脚本并不一定会按照顺序执行，也不一定会在 DOMContentLoaded 事件触发前执行，因此最好只包含一个延迟脚本。

前面提到过， defer 属性只适用于外部脚本文件。这一点在 HTML5 中已经明确规定，因此支持 HTML5 的实现会忽略给嵌入脚本设置的 defer 属性。 IE4 ～ IE7 还支持对嵌入脚本的 defer 属性，但 IE8 及之后版本则完全支持 HTML5 规定的行为。

IE4、 Firefox 3.5、 Safari 5 和 Chrome 是最早支持 defer 属性的浏览器。其他浏览器会忽略这个属性，像平常一样处理脚本。为此，把延迟脚本放在页面底部仍然是最佳选择。

> 在 XHTML 文档中，要把 defer 属性设置为 `defer="defer"`。

### 2.1.3 异步脚本

HTML5 为`<script>`元素定义了 async 属性。这个属性与 defer 属性类似，都用于改变处理脚本的行为。同样与 defer 类似， async 只适用于外部脚本文件，并告诉浏览器立即下载文件。但与 defer 不同的是，标记为 async 的脚本并不保证按照指定它们的先后顺序执行。例如：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" async src="example1.js"></script>
    <script type="text/javascript" async src="example2.js"></script>
  </head>
  <body>
    <!-- 这里放内容 -->
  </body>
</html>
```

在以上代码中，第二个脚本文件可能会在第一个脚本文件之前执行。因此，确保两者之间互不依赖非常重要。指定 async 属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。为此，建议异步脚本不要在加载期间修改 DOM。

异步脚本一定会在页面的 load 事件前执行，但可能会在 DOMContentLoaded 事件触发之前或之后执行。支持异步脚本的浏览器有 Firefox 3.6、 Safari 5 和 Chrome。

> 在 XHTML 文档中，要把 async 属性设置为 `async="async"`。

## 2.2 嵌入代码与外部文件　

在 HTML 中嵌入 JavaScript 代码虽然没有问题，但一般认为最好的做法还是尽可能使用外部文件来包含 JavaScript 代码。优点如下：

- 可维护性：遍及不同 HTML 页面的 JavaScript 会造成维护问题。
- 可缓存：浏览器能够根据具体的设置缓存链接的所有外部 JavaScript 文件，加快页面加载的速度。
- 适应未来：通过外部文件来包含 JavaScript 无须使用前面提到 XHTML 或注释 hack。

## 2.3 文档模式　

IE5.5 引入了文档模式的概念，而这个概念是通过使用文档类型（doctype）切换实现的。虽然这两种模式主要影响 CSS 内容的呈现，但在某些情况下也会影响到 JavaScript 的解释执行。在此之后， IE 又提出一种所谓的准标准模式（almost standards mode）。

- 混杂模式（quirks mode）。让 IE 的行为与（包含非标准特性的）IE5 相同。
- 标准模式（standards mode）。让 IE 的行为更接近标准行为。

如果在文档开始处没有发现文档类型声明，则所有浏览器都会默认开启混杂模式。但采用混杂模式不是什么值得推荐的做法，因为不同浏览器在这种模式下的行为差异非常大，如果不使用某些 hack 技术，跨浏览器的行为根本就没有一致性可言。

对于标准模式，可以通过使用下面任何一种文档类型来开启：

```html
<!-- HTML 4.01 严格型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">

<!-- XHTML 1.0 严格型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

<!-- HTML 5 -->
<!DOCTYPE html>
```

而对于准标准模式，则可以通过使用过渡型（transitional）或框架集型（frameset）文档类型来触发，如下所示：

```html
<!-- HTML 4.01 过渡型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<!-- HTML 4.01 框架集型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">

<!-- XHTML 1.0 过渡型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<!-- XHTML 1.0 框架集型 -->
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

## 2.4 \<noscript\>元素　

早期浏览器都面临一个特殊的问题，即当浏览器不支持 JavaScript 时如何让页面平稳地退化。对这个问题的最终解决方案就是创造一个`<noscript>`元素，用以在不支持 JavaScript 的浏览器中显示替代的内容。这个元素可以包含能够出现在文档`<body>`中的任何 HTML 元素——`<script>`元素除外。包含在`<noscript>`元素中的内容只有在下列情况下才会显示出来：

- 浏览器不支持脚本；
- 浏览器支持脚本，但脚本被禁用。

符合上述任何一个条件，浏览器都会显示`<noscript>`中的内容。而在除此之外的其他情况下，浏览器不会呈现`<noscript>`中的内容。请看下面这个简单的例子：

```html
<html>
  <head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer="defer" src="example1.js"></script>
    <script type="text/javascript" defer="defer" src="example2.js"></script>
  </head>
  <body>
    <noscript> <p>本页面需要浏览器支持（启用） JavaScript。</p></noscript>
  </body>
</html>
```

这个页面会在脚本无效的情况下向用户显示一条消息。而在启用了脚本的浏览器中，用户永远也不会看到它——尽管它是页面的一部分。

## 2.5 小结

把 JavaScript 插入到 HTML 页面中要使用`<script>`元素。使用这个元素可以把 JavaScript 嵌入到 HTML 页面中，让脚本与标记混合在一起；也可以包含外部的 JavaScript 文件。而我们需要注意的地方有：

- 在包含外部 JavaScript 文件时，必须将 src 属性设置为指向相应文件的 URL。而这个文件既可以是与包含它的页面位于同一个服务器上的文件，也可以是其他任何域中的文件。
- 所有`<script>`元素都会按照它们在页面中出现的先后顺序依次被解析。在不使用 defer 和 async 属性的情况下，只有在解析完前面`<script>`元素中的代码之后，才会开始解析后面`<script>`元素中的代码。
- 由于浏览器会先解析完不使用 defer 属性的`<script>`元素中的代码，然后再解析后面的内容，所以一般应该把`<script>`元素放在页面最后，即主要内容后面， `</body>`标签前面。
- 使用 defer 属性可以让脚本在文档完全呈现之后再执行。延迟脚本总是按照指定它们的顺序执行。
- 使用 async 属性可以表示当前脚本不必等待其他脚本，也不必阻塞文档呈现。不能保证异步脚本按照它们在页面中出现的顺序执行。

另外，使用`<noscript>`元素可以指定在不支持脚本的浏览器中显示的替代内容。但在启用了脚本的情况下，浏览器不会显示`<noscript>`元素中的任何内容。

# 第 3 章 基本概念　

## 3.1 语法　

### 3.1.1 区分大小写

ECMAScript 中的一切都区分大小写，例如变量、函数名和操作符。这也就意味着，变量名 test 和变量名 Test 分别表示两个不同的变量，而函数名不能使用 typeof，因为它是一个关键字，但 typeOf 则完全可以是一个有效的函数名。

### 3.1.2 标识符

所谓标识符，就是指变量、函数、属性的名字，或者函数的参数。标识符可以是按照下列格式规则组合起来的一或多个字符：

- 第一个字符必须是一个字母、下划线（\_）或一个美元符号（\$）；
- 其他字符可以是字母、下划线、美元符号或数字。

标识符中的字母也可以包含扩展的 ASCII 或 Unicode 字母字符（如 À 和 Æ），但不推荐这样做。

按照惯例， ECMAScript 标识符采用驼峰大小写格式，也就是第一个字母小写，剩下的每个单词的首字母大写，例如：

- firstSecond
- myCar
- doSomethingImportant

不能把关键字、保留字、 true、 false 和 null 用作标识符。

### 3.1.3 注释

ECMAScript 使用 C 风格的注释，包括单行注释和块级注释。单行注释以两个斜杠开头，块级注释以一个斜杠和一个星号`/*`开头，以一个星号和一个斜杠`*/`结尾。

```js
// 单行注释

/*
* 这是一个多行
* （块级）注释
*/
```

虽然上面注释中的第二和第三行都以一个星号开头，但这不是必需的。之所以添加那两个星号，纯粹是为了提高注释的可读性。

CSS无论是单行注释还是跨行注释都是使用`/*`和`*/`包围，而 HTML 则是使用`<!--注释内容-->`进行注释。

### 3.1.4 严格模式

ECMAScript 5 引入了严格模式（strict mode）的概念。严格模式是为 JavaScript 定义了一种不同的解析与执行模型。在严格模式下， ECMAScript 3 中的一些不确定的行为将得到处理，而且对某些不安全的操作也会抛出错误。要在整个脚本中启用严格模式，可以在顶部添加如下代码：

```js
"use strict";
```

这行代码看起来像是字符串，而且也没有赋值给任何变量，但其实它是一个编译指示（pragma），用于告诉支持的 JavaScript 引擎切换到严格模式。这是为不破坏 ECMAScript 3 语法而特意选定的语法。在函数内部的上方包含这条编译指示，也可以指定函数在严格模式下执行：

```js
function doSomething(){
"use strict";
//函数体
}
```

### 3.1.5 语句

ECMAScript 中的语句以一个分号结尾；如果省略分号，则由解析器确定语句的结尾，如下例所示：

```js
var sum = a + b // 即使没有分号也是有效的语句——不推荐
var diff = a - b; // 有效的语句——推荐
```

虽然语句结尾的分号不是必需的，但建议任何时候都不要省略它。因为加上这个分号可以避免很多错误（例如不完整的输入），开发人员也可以放心地通过删除多余的空格来压缩 ECMAScript 代码（代码行结尾处没有分号会导致压缩错误）。另外，加上分号也会在某些情况下增进代码的性能，因为这样解析器就不必再花时间推测应该在哪里插入分号了。

可以使用 C 风格的语法把多条语句组合到一个代码块中，即代码块以左花括号`{`开头，以右花括号`}`结尾：

```js
if (test){
  test = false;
  alert(test);
}
```

虽然条件控制语句（如 if 语句）只在执行多条语句的情况下才要求使用代码块，但最佳实践是始终在控制语句中使用代码块——即使代码块中只有一条语句，例如：

```js
if (test)
  alert(test); // 有效但容易出错，不要使用

if (test){ // 推荐使用
  alert(test);
}
```

在控制语句中使用代码块可以让编码意图更加清晰，而且也能降低修改代码时出错的几率。

## 3.2 关键字和保留字　

ECMA-262 描述了一组具有特定用途的关键字，这些关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。按照规则，关键字也是语言保留的，不能用作标识符。ECMA-262 还描述了另外一组不能用作标识符的保留字。尽管保留字在这门语言中还没有任何特定的用途，但它们有可能在将来被用作关键字。

第 5 版把在非严格模式下运行时的保留字缩减为下列这些：

| class | enum   | extends | super |
| const | export | import  |       |

在严格模式下，第 5 版还对以下保留字施加了限制：

| implements | package   | public |
| interface  | private   | static |
| let        | protected | yield  |

在实现 ECMAScript 3 的 JavaScript 引擎中使用关键字作标识符，会导致“Identifier Expected”错误。而使用保留字作标识符可能会也可能不会导致相同的错误，具体取决于特定的引擎。

第 5 版对使用关键字和保留字的规则进行了少许修改。关键字和保留字虽然仍然不能作为标识符使用，但现在可以用作对象的属性名。一般来说，最好都不要使用关键字和保留字作为标识符和属性名，以便与将来的 ECMAScript 版本兼容。

除了上面列出的保留字和关键字， ECMA-262 第 5 版对 eval 和 arguments 还施加了限制。在严格模式下，这两个名字也不能作为标识符或属性名，否则会抛出错误。

## 3.3 变量　

ECMAScript 的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据。换句话说，每个变量仅仅是一个用于保存值的占位符而已。定义变量时要使用 var 操作符（注意 var 是一个关键字），后跟变量名（即一个标识符）。如果变量是未经过初始化的，会保存一个特殊的值——undefined。 ECMAScript 也支持直接初始化变量，因此在定义变量的同时就可以设置变量的值。

```js
// 未经过初始化
var message;

// 初始化变量
var message = "hi";
```

可以在修改变量值的同时修改值的类型。但是不建议修改变量所保存值的类型，虽然这种操作在 ECMAScript 中完全有效。

```js
var message = "hi";
message = 100; // 有效，但不推荐
```

有一点必须注意，即用 var 操作符定义的变量将成为定义该变量的作用域中的局部变量。也就是说，如果在函数中使用 var 定义一个变量，那么这个变量在函数退出后就会被销毁。不过，可以省略 var 操作符，从而创建一个全局变量。虽然省略 var 操作符可以定义全局变量，但这不是推荐的做法。给未经声明的变量赋值在严格模式下会导致抛出 ReferenceError 错误。

```JavaScript
function test(){
  var message = "hi"; // 局部变量
}
test();
alert(message); // 错误！
```

```JavaScript
function test(){
  message = "hi"; // 全局变量
}
test();
alert(message); // "hi"
```

可以使用一条语句定义多个变量，只要像下面这样把每个变量（初始化或不初始化均可）用逗号分隔开即可。虽然代码里的换行和变量缩进不是必需的，但这样做可以提高可读性。在严格模式下，不能定义名为 eval 或 arguments 的变量，否则会导致语法错误。

```js
var message = "hi",
found = false,
age = 29;
```

## 3.4 数据类型　

ECMAScript 中有五种简单数据类型（也称为基本数据类型）：`Undefined`、`Null`、`Boolean`、`Number`和 `String`。还有一种复杂数据类型——`Object`，`Object` 本质上是由一组无序的名值对组成的。ECMAScript不支持任何创建自定义类型的机制，而所有值最终都将是上述六种数据类型之一。由于 ECMAScript 数据类型具有动态性，因此没有再定义其他数据类型的必要了。

### 3.4.1 typeof 操作符

鉴于 ECMAScript 是松散类型的，因此需要有一种手段来检测给定变量的数据类型——`typeof` 就是负责提供这方面信息的操作符。对一个值使用 `typeof` 操作符可能返回下列某个字符串：

1. "undefined"——如果这个值未定义；
2. "boolean"——如果这个值是布尔值；
3. "string"——如果这个值是字符串；
4. "number"——如果这个值是数值；
5. "object"——如果这个值是对象或 null；
6. "function"——如果这个值是函数。

`typeof` 操作符的操作数可以是变量，也可以是数值字面量。注意，`typeof` 是一个操作符而不是函数，因此例子中的圆括号尽管可以使用，但不是必需的。

```js
var message = "some string";
alert(typeof message); // "string"
alert(typeof(message)); // "string"
alert(typeof 95); // "number"
```

有些时候， `typeof` 操作符会返回一些令人迷惑但技术上却正确的值。比如，调用 `typeof null` 会返回"object"，因为特殊值 null 被认为是一个空的对象引用。从技术角度讲，函数在 ECMAScript 中是对象，不是一种数据类型。然而，函数也确实有一些特殊的属性，因此通过 `typeof` 操作符来区分函数和其他对象是有必要的。

### 3.4.2 Undefined 类型

`Undefined` 类型是只有一个值，即特殊的 undefined，在使用 var 声明但未对其加以初始化时，这个变量的值就是 undefined。

```js
var message1;
alert(message1 == undefined); //true

var message2 = undefined;
alert(message2 == undefined); //true
```

包含 undefined 值的变量与尚未定义的变量还是不一样的。如果未声明却在使用，则会报错。但是，两者使用 typeof 操作符检测时都显示为 undefined。

```js
var message; // 这个变量声明之后默认取得了 undefined 值
// 下面这个变量并没有声明
// var age

alert(message); // "undefined"
alert(age); // 产生错误

alert(typeof message); // "undefined"
alert(typeof age); // "undefined"
```

即便未初始化的变量会自动被赋予 undefined 值，但显式地初始化变量依然是明智的选择。如果能够做到这一点，那么当 typeof 操作符返回"undefined"值时，我们就知道被检测的变量还没有被声明，而不是尚未初始化。

### 3.4.3 Null 类型

`Null` 类型是第二个只有一个值的数据类型，这个特殊的值是 `null`。从逻辑角度来看， `null` 值表示一个空对象指针，而这也正是使用 typeof 操作符检测 `null` 值时会返回"object"的原因。

```js
var car = null;
alert(typeof car); // "object"
```

如果定义的变量准备在将来用于保存对象，那么最好将该变量初始化为 null 而不是其他值。这样一来，只要直接检查 null 值就可以知道相应的变量是否已经保存了一个对象的引用。

```js
if (car != null){
  // 对 car 对象执行某些操作
}
```

实际上， undefined 值是派生自 null 值的，因此 ECMA-262 规定对它们的相等性测试要返回 true：

```js
alert(null == undefined); //true
NullExample02.htm
```

尽管 null 和 undefined 有这样的关系，但它们的用途完全不同。如前所述，无论在什么情况下都没有必要把一个变量的值显式地设置为 undefined，可是同样的规则对 null 却不适用。换句话说，只要意在保存对象的变量还没有真正保存对象，就应该明确地让该变量保存 null 值。这样做不仅可以体现 null 作为空对象指针的惯例，而且也有助于进一步区分 null 和 undefined。

### 3.4.4 Boolean 类型

Boolean 类型是 ECMAScript 中使用得最多的一种类型，该类型只有两个字面值：`true `和 `false`。需要注意的是，Boolean 类型的字面值 `true `和 `false` 是区分大小写的。也就是说，True 和 False （以及其他的混合大小写形式）都不是 Boolean 值，只是标识符。

虽然 Boolean 类型的字面值只有两个，但 ECMAScript 中所有类型的值都有与这两个 Boolean 值等价的值。要将一个值转换为其对应的 Boolean 值，可以调用转型函数 `Boolean()`。下表给出了各种数据类型及其对应的转换规则。

| 数据类型  |        转换为true的值        | 转换为false的值 |
| --------- | ---------------------------- | --------------- |
| Boolean   | true                         | false           |
| String    | 任何非空字符串               | ""（空字符串）  |
| Number    | 任何非零数字值（包括无穷大） | 0和NaN          |
| Object    | 任何对象                     | null            |
| Undefined |                              | undefined       |

这些转换规则对理解流控制语句（如 if 语句）自动执行相应的 Boolean 转换非常重要。因此确切地知道在流控制语句中使用的是什么变量至关重要。错误地使用一个对象而不是一个 Boolean 值，就有可能彻底改变应用程序的流程。

```js
var message = "Hello world!";
if (message){
  alert("Value is true");
}
```

### 3.4.5 Number 类型

Number 类型使用 IEEE754 格式来表示整数和浮点数值（浮点数值在某些语言中也被称为双精度数值）。为支持各种数值类型， ECMA-262 定义了不同的数值字面量格式。最基本的数值字面量格式是十进制整数，十进制整数可以这样直接在代码中输入。整数还可以通过八进制（以 8 为基数）或十六进制（以 16 为基数）的字面值来表示。其中，八进制字面值的第一位必须是零（0），然后是八进制数字序列（0～7）。如果字面值中的数值超出了范围，那么前导零将被忽略，后面的数值将被当作十进制数值解析。

```js
var intNum = 55; // 整数
var octalNum1 = 070; // 八进制的 56
var octalNum2 = 079; // 无效的八进制数值——解析为 79
var octalNum3 = 08; // 无效的八进制数值——解析为 8
```

八进制字面量在严格模式下是无效的，会导致支持的 JavaScript 引擎抛出错误。十六进制字面值的前两位必须是 0x，后跟任何十六进制数字（0～9 及 A～F）。其中，字母 A～F 可以大写，也可以小写。

```js
var hexNum1 = 0xA; // 十六进制的 10
var hexNum2 = 0x1f; // 十六进制的 31
```

在进行算术计算时，所有以八进制和十六进制表示的数值最终都将被转换成十进制数值。

**浮点数值**。所谓浮点数值，就是该数值中必须包含一个小数点，并且小数点后面必须至少有一位数字。虽然小数点前面可以没有整数，但我们不推荐这种写法。由于保存浮点数值需要的内存空间是保存整数值的两倍，因此 ECMAScript 会不失时机地将浮点数值转换为整数值。显然，如果小数点后面没有跟任何数字，那么这个数值就可以作为整数值来保存。同样地，如果浮点数值本身表示的就是一个整数（如 1.0），那么该值也会被转换为整数。

对于那些极大或极小的数值，可以用 e 表示法（即科学计数法）表示的浮点数值表示。用 e 表示法表示的数值等于 e 前面的数值乘以 10 的指数次幂。 ECMAScript 中 e 表示法的格式也是如此，即前面是一个数值（可以是整数也可以是浮点数），中间是一个大写或小写的字母 E，后面是 10 的幂中的指数，该幂值将用来与前面的数相乘。

```js
var floatNum = 3.125e7; // 等于 31250000
```

浮点数值的最高精度是 17 位小数，但在进行算术计算时其精确度远远不如整数。例如， 0.1 加 0.2 的结果不是 0.3，而是 0.30000000000000004。这个小小的舍入误差会导致无法测试特定的浮点数值。关于浮点数值计算会产生舍入误差的问题，有一点需要明确：这是使用基于 IEEE754 数值的浮点计算的通病， ECMAScript 并非独此一家。

```js
var a = 0.1, b = 0.2
if (a + b == 0.3){ // 不要做这样的测试！
  alert("You got 0.3.");
}
```

**数值范围**。由于内存的限制， ECMAScript 并不能保存世界上所有的数值。 ECMAScript 能够表示的最小数值保存在 `Number.MIN_VALUE` 中——在大多数浏览器中，这个值是 5e-324；能够表示的最大数值保存在`Number.MAX_VALUE` 中——在大多数浏览器中，这个值是 1.7976931348623157e+308。如果某次计算的结果得到了一个超出 JavaScript 数值范围的值，那么这个数值将被自动转换成特殊的 Infinity 值。具体来说，如果这个数值是负数，则会被转换成-Infinity（负无穷），如果这个数值是正数，则会被转换成 Infinity（正无穷）。

如果某次计算返回了正或负的 Infinity 值，那么该值将无法继续参与下一次的计算，因为 Infinity 不是能够参与计算的数值。要想确定一个数值是不是有穷的（换句话说，是不是位于最
小和最大的数值之间），可以使用 `isFinite()`函数。这个函数在参数位于最小与最大数值之间时会返回 true。

```js
var result = Number.MAX_VALUE + Number.MAX_VALUE;
alert(isFinite(result)); //false
```

尽管在计算中很少出现某些值超出表示范围的情况，但在执行极小或极大数值的计算时，检测监控这些值是可能的，也是必需的。

**NaN**。`NaN`，即非数值（Not a Number）是一个特殊的数值，这个数值用于表示一个本来要返回数值的操作数未返回数值的情况（这样就不会抛出错误了）。例如，在其他编程语言中，任何数值除以 0 都会导致错误，从而停止代码执行。但在 ECMAScript 中，任何数值除以 0 会返回 NaN，因此不会影响其他代码的执行。NaN 本身有两个非同寻常的特点。首先，任何涉及 NaN 的操作（例如 NaN/10）都会返回 NaN，这个特点在多步计算中有可能导致问题。其次， NaN 与任何值都不相等，包括 NaN 本身。

```js
alert(NaN == NaN); //false
```

针对 NaN 的这两个特点， ECMAScript 定义了 `isNaN()`函数。这个函数接受一个参数，该参数可以是任何类型，而函数会帮我们确定这个参数是否“不是数值”。 `isNaN()`在接收到一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，例如字符串"10"或 Boolean 值。而任何不能被转换为数值的值都会导致这个函数返回 true。

```js
alert( isNaN(NaN) ); //true
alert( isNaN(10) ); //false（ 10 是一个数值）
alert( isNaN("10") ); //false（可以被转换成数值 10）
alert( isNaN("blue") ); //true（不能转换成数值）
alert( isNaN(true) ); //false（可以被转换成数值 1）
```

**数值转换**。有 3 个函数可以把非数值转换为数值： `Number()`、 `parseInt()`和 `parseFloat()`。第一个函数，即转型函数 `Number()`可以用于任何数据类型，而另两个函数则专门用于把字符串转换成数值。这 3 个函数对于同样的输入会有返回不同的结果。

`Number()`函数的转换规则如下。

- 如果是 Boolean 值， true 和 false 将分别被转换为 1 和 0。
- 如果是数字值，只是简单的传入和返回。
- 如果是 null 值，返回 0。
- 如果是 undefined，返回 NaN。
- 如果是字符串，遵循下列规则：
  - 如果字符串中只包含数字（包括前面带正号或负号的情况），则将其转换为十进制数值，即"1"会变成 1， "123"会变成 123，而"011"会变成 11（注意：前导的零被忽略了）；
  - 如果字符串中包含有效的浮点格式，如"1.1"，则将其转换为对应的浮点数值（同样，也会忽略前导零）；
  - 如果字符串中包含有效的十六进制格式，例如"0xf"，则将其转换为相同大小的十进制整数值；
  - 如果字符串是空的（不包含任何字符），则将其转换为 0；
  - 如果字符串中包含除上述格式之外的字符，则将其转换为 NaN。
- 如果是对象，则调用对象的 `valueOf()`方法，然后依照前面的规则转换返回的值。如果转换的结果是 NaN，则调用对象的 `toString()`方法，然后再次依照前面的规则转换返回的字符串值。

```js
var num1 = Number("Hello world!"); //NaN
var num2 = Number(""); //0
var num3 = Number("000011"); //11
var num4 = Number(true); //1
```

由于 `Number()`函数在转换字符串时比较复杂而且不够合理，因此在处理整数的时候更常用的是`parseInt()`函数。 `parseInt()`函数在转换字符串时，更多的是看其是否符合数值模式。它会忽略字符串前面的空格，直至找到第一个非空格字符。

- 如果第一个字符不是数字字符或者负号， `parseInt()`就会返回 NaN；也就是说，用 `parseInt()`转换空字符串会返回 NaN（`Number()`对空字符返回 0）。

- 如果第一个字符是数字字符， `parseInt()`会继续解析第二个字符，直到解析完所有后续字符或者遇到了一个非数字字符。

- 如果字符串中的第一个字符是数字字符， `parseInt()`也能够识别出各种整数格式（即前面讨论的十进制、八进制和十六进制数）。

```js
var num1 = parseInt("1234blue"); // 1234
var num2 = parseInt(""); // NaN
var num3 = parseInt("0xA"); // 10（十六进制数）
var num4 = parseInt(22.5); // 22
var num5 = parseInt("070"); // 56（八进制数）
var num6 = parseInt("70"); // 70（十进制数）
var num7 = parseInt("0xf"); // 15（十六进制数）
```

在使用 `parseInt()`解析像八进制字面量的字符串时， ECMAScript 3 和 5 存在分歧。例如：

```js
//ECMAScript 3 认为是 56（八进制）， ECMAScript 5 认为是 70（十进制）
var num = parseInt("070");
```

为了消除在使用 `parseInt()`函数时可能导致的上述困惑，可以为这个函数提供第二个参数：转换时使用的基数（即多少进制）。如果知道要解析的值是十六进制格式的字符串，那么指定基数 16 作为第二个参数，可以保证得到正确的结果。

与`parseInt()`函数类似， `parseFloat()`也是从第一个字符（位置 0）开始解析每个字符。而且也是一直解析到字符串末尾，或者解析到遇见一个无效的浮点数字字符为止。也就是说，字符串中的第一个小数点是有效的，而第二个小数点就是无效的了，因此它后面的字符串将被忽略。

除了第一个小数点有效之外， `parseFloat()`与 `parseInt()`的第二个区别在于它始终都会忽略前导的零。 `parseFloat()`可以识别前面讨论过的所有浮点数值格式，也包括十进制整数格式。但十六进制格式的字符串则始终会被转换成 0。由于 `parseFloat()`只解析十进制值，因此它没有用第二个参数指定基数的用法。最后还要注意一点：如果字符串包含的是一个可解析为整数的数（没有小数点，或者小数点后都是零）， `parseFloat()`会返回整数。

```js
var num1 = parseFloat("1234blue"); //1234 （整数）
var num2 = parseFloat("0xA"); //0
var num3 = parseFloat("22.5"); //22.5
var num4 = parseFloat("22.34.5"); //22.34
var num5 = parseFloat("0908.5"); //908.5
var num6 = parseFloat("3.125e7"); //31250000
```

### 3.4.6 String 类型

String 类型用于表示由零或多个 16 位 Unicode 字符组成的字符序列，即字符串。字符串可以由双引号（"）或单引号（'）表示。。用双引号表示的字符串和用单引号表示的字符串完全相同。不过，以双引号开头的字符串也必须以双引号结尾，而以单引号开头的字符串必须以单引号结尾。

```js
var firstName = "Nicholas";
var lastName = 'Zakas';
```

**字符字面量**。String 数据类型包含一些特殊的字符字面量，也叫转义序列，用于表示非打印字符，或者具有其他用途的字符。

| 字 面 量 |                          含 义                          |
| -------- | ------------------------------------------------------- |
| `\n`     | 换行                                                    |
| `\t`     | 制表                                                    |
| `\b`     | 空格                                                    |
| `\r`     | 回车                                                    |
| `\f`     | 进纸                                                    |
| `\\`     | 斜杠                                                    |
| `\'`     | 单引号（ '）                                            |
| `\"`     | 双引号（ "）                                            |
| `\xnn`   | 以十六进制代码nn表示的一个字符（其中n为0～ F）          |
| `\unnnn` | 以十六进制代码nnnn表示的一个Unicode字符（其中n为0～ F） |

这些字符字面量可以出现在字符串中的任意位置，而且也将被作为一个字符来解析。任何字符串的长度都可以通过访问其 length 属性取得，其中一个转义序列表示一个字符。

**字符串的特点**。ECMAScript 中的字符串是不可变的，也就是说，字符串一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量。

**转换为字符串**。要把一个值转换为一个字符串有两种方式。第一种是使用几乎每个值都有的 toString()方法。这个方法唯一要做的就是返回相应值的字符串表现。但 null 和 undefined 值没有这个方法。在调用数值的 toString()方法时，可以传递一个参数：输出数值的基数。

```js
var num = 10;
alert(num.toString()); // "10"
alert(num.toString(2)); // "1010"
alert(num.toString(8)); // "12"
alert(num.toString(10)); // "10"
alert(num.toString(16)); // "a"
```

在不知道要转换的值是不是 null 或 undefined 的情况下，还可以使用转型函数 `String()`，这个函数能够将任何类型的值转换为字符串。 `String()`函数遵循下列转换规则。

- 如果值有 `toString()` 方法，则调用该方法（没有参数）并返回相应的结果；
- 如果值是 null，则返回`"null"`；
- 如果值是 undefined，则返回`"undefined"`。

要把某个值转换为字符串，可以使用加号操作符。

### 3.4.7 Object 类型

ECMAScript 中的对象其实就是一组数据和功能的集合。对象可以通过执行 new 操作符后跟要创建的对象类型的名称来创建。而创建 Object 类型的实例并为其添加属性和（或）方法，就可以创建自定义对象。

```js
var o = new Object();
```

这个语法与 Java 中创建对象的语法相似；但在 ECMAScript 中，如果不给构造函数传递参数，则可以省略后面的那一对圆括号。也就是说，在像前面这个示例一样不传递参数的情况下，完全可以省略那对圆括号（但这不是推荐的做法）：

```js
var o = new Object; // 有效，但不推荐省略圆括号
```

仅仅创建 Object 的实例并没有什么用处，但关键是要理解一个重要的思想：即在 ECMAScript 中，（就像 Java 中的 java.lang.Object 对象一样） Object 类型是所有它的实例的基础。换句话说，Object 类型所具有的任何属性和方法也同样存在于更具体的对象中。

Object 的每个实例都有如下属性和方法。

1. `constructor`：保存着用于创建当前对象的函数。对于前面的例子而言，构造函数（constructor）就是 `Object()`。
2. `hasOwnProperty(propertyName)`：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。其中，作为参数的属性名（propertyName）必须以字符串形式指定（例如： `o.hasOwnProperty("name")`）。
3. `isPrototypeOf(object)`：用于检查传入的对象是否是传入对象的原型。
4. `propertyIsEnumerable(propertyName)`：用于检查给定的属性是否能够使用 for-in 语句来枚举。与 `hasOwnProperty()`方法一样，作为参数的属性名必须以字符串形式指定。
5. `toLocalString`：返回对象的字符串表示，该字符串与执行环境的地区对应。
6. `toString()`：返回对象的字符串表示。
7. `valueOf()`：返回对象的字符串、数值或布尔值表示。通常与 `toString()`方法的返回值相同。

由于在 ECMAScript 中 Object 是所有对象的基础，因此所有对象都具有这些基本的属性和方法。第 5 章和第 6 章将详细介绍 Object 与其他对象的关系。

## 3.5 操作符　

ECMA-262 描述了一组用于操作数据值的操作符，它们能够适用于很多值，例如字符串、数字值、布尔值，甚至对象。不过，在应用于对象时，相应的操作符通常都会调用对象的 `valueOf()` 和（或）`toString()`方法，以便取得可以操作的值。

### 3.5.1 一元操作符

递增和递减操作符

只能操作一个值的操作符叫做一元操作符。一元操作符是 ECMAScript 中最简单的操作符。

递增和递减操作符直接借鉴自 C，而且各有两个版本：前置型和后置型。顾名思义，前置型应该位于要操作的变量之前，而后置型则应该位于要操作的变量之后。因此，在使用前置递增操作符给一个数值加 1 时，要把两个加号（++）放在这个数值变量前面。

```js
var age = 29;
// 相当于age = age + 1;
++age;
```

执行前置递增和递减操作时，变量的值都是在语句被求值以前改变的。（在计算机科学领域，这种情况通常被称作副效应。）

```js
var age = 29;
var anotherAge = --age + 2;
alert(age); // 输出 28
alert(anotherAge); // 输出 30
```

后置型递增和递减操作符的语法不变（仍然分别是`++`和`--`），只不过要放在变量的后面而不是前面。后置递增和递减与前置递增和递减有一个非常重要的区别，即递增和递减操作是在包含它们的语句被求值之后才执行的。这个区别在某些情况下不是什么问题。

```js
var age = 29;
age++;
```

但是，当语句中还包含其他操作时，上述区别就会非常明显了。

```js
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2; // 等于 22
var num4 = num1 + num2; // 等于 21
```

所有这 4 个操作符对任何值都适用，也就是它们不仅适用于整数，还可以用于字符串、布尔值、浮点数值和对象。在应用于不同的值时，递增和递减操作符遵循下列规则。

- 在应用于一个包含有效数字字符的字符串时，先将其转换为数字值，再执行加减 1 的操作。字符串变量变成数值变量。
- 在应用于一个不包含有效数字字符的字符串时，将变量的值设置为 NaN 。字符串变量变成数值变量。
- 在应用于布尔值 false 时，先将其转换为 0 再执行加减 1 的操作。布尔值变量变成数值变量。
- 在应用于布尔值 true 时，先将其转换为 1 再执行加减 1 的操作。布尔值变量变成数值变量。
- 在应用于浮点数值时，执行加减 1 的操作。
- 在应用于对象时，先调用对象的 `valueOf()`方法以取得一个可供操作的值。然后对该值应用前述规则。如果结果是 NaN，则在调用 `toString()`方法后再应用前述规则。对象变量变成数值变量。

```js
var s1 = "2";
var s2 = "z";
var b = false;
var f = 1.1;
var o = {
  valueOf: function() {
    return -1;
  }
};
s1++; // 值变成数值 3
s2++; // 值变成 NaN
b++; // 值变成数值 1
f--; // 值变成 0.10000000000000009（由于浮点舍入错误所致）
o--; // 值变成数值-2
```

### 3.5.2 位操作符

位操作符，有按位非、按位与、按位或、按位异或、左移、有符号的右移、无符号的右移多种。

### 3.5.3 布尔操作符

布尔操作符，有逻辑非、逻辑与、逻辑或三种。

### 3.5.4 乘性操作符

乘性操作符有三个，乘法、除法和求模。

### 3.5.5 加性操作符

加性操作符有两种，加法、减法。

### 3.5.6 关系操作符

关系操作符有四种，小于、大于、小于等于和大于等于。

### 3.5.7 相等操作符

相等操作符有相等和不相等、全等和不全等四种，前面两种是先转换再比较，后面一种是比较而不转换。

### 3.5.8 条件操作符

条件操作符，条件（三元）运算符是JavaScript仅有的使用三个操作数的运算符。本运算符经常作为if语句的简短形式来使用。

### 3.5.9 赋值操作符

赋值操作符由等于号表示，每个主要算术操作符都有对应的复合赋值操作符，但设计这些操作符的主要目的就是简化赋值操作，使用他们不会带来任何性能的提升。

### 3.5.10 逗号操作符

逗号操作符，可以在一条语句中执行多个操作，主要用于声明多个变量、用于赋值。

## 3.6 语句　

ECMA-262 规定了一组语句（也称为流控制语句）。从本质上看，语句定义了 ECMAScript 中的主要语法，语句通常使用一或多个关键字来完成给定任务。语句可以很简单，例如通知函数退出；也可以比较复杂，例如指定重复执行某个命令的次数。

### 3.6.1 if语句

大多数编程语言中最为常用的一个语句就是 if 语句。

```js
if (condition) statement1 else statement2
```

其中的 condition（条件）可以是任意表达式；而且对这个表达式求值的结果不一定是布尔值。ECMAScript 会自动调用`Boolean()`转换函数将这个表达式的结果转换为一个布尔值。

如果对 condition 求值的结果是 true，则执行 statement1（语句 1），如果对 condition 求值的结果是 false，则执行 statement2 （语句 2）。而且这两个语句既可以是一行代码，也可以是一个代码块（以一对花括号括起来的多行代码）。不过，业界普遍推崇的最佳实践是始终使用代码块，即使要执行的只有一行代码。

```js
if (i > 25)
alert("Greater than 25."); // 单行语句
else {
alert("Less than or equal to 25."); // 代码块中的语句
}
IfStatementExample01.htm
```

### 3.6.2 do-while语句

do-while 语句是一种后测试循环语句，即只有在循环体中的代码执行之后，才会测试出口条件。换句话说，在对条件表达式求值之前，循环体内的代码至少会被执行一次。

```js
do {
statement
} while (expression);
```

### 3.6.3 while语句

while 语句属于前测试循环语句，也就是说，在循环体内的代码被执行之前，就会对出口条件求值。因此，循环体内的代码有可能永远不会被执行。

```js
while(expression) statement
```

### 3.6.4 for语句

for 语句也是一种前测试循环语句，但它具有在执行循环之前初始化变量和定义循环后要执行的代码的能力。使用 while 循环做不到的，使用 for 循环同样也做不到。也就是说， for 循环只是把与循环有关的代码集中在了一个位置。

```js
for (initialization; expression; post-loop-expression) statement
```

有必要指出的是，在 for 循环的变量初始化表达式中，也可以不使用 var 关键字。该变量的初始化可以在外部执行。由于 ECMAScript 中不存在块级作用域，因此在循环内部定义的变量也可以在外部访问到。

此外， for 语句中的初始化表达式、控制表达式和循环后表达式都是可选的。将这三个表达式全部省略，就会创建一个无限循环。

### 3.6.5 for-in语句

for-in 语句是一种精准的迭代语句，可以用来枚举对象的属性。

```js
for (property in expression) statement
```

ECMAScript 对象的属性没有顺序。因此，通过 for-in 循环输出的属性名的顺序是不可预测的。具体来讲，所有属性都会被返回一次，但返回的先后次序可能会因浏览器而异。

但是，如果表示要迭代的对象的变量值为 null 或 undefined， for-in 语句会抛出错误。ECMAScript 5 更正了这一行为；对这种情况不再抛出错误，而只是不执行循环体。为了保证最大限度的兼容性，建议在使用 for-in 循环之前，先检测确认该对象的值不是 null 或 undefined。

### 3.6.6 label语句

使用 label 语句可以在代码中添加标签，以便将来使用。

```js
label: statement
```

加标签的语句一般都要与 for 语句等循环语句配合使用。

```js
start: for (var i=0; i < count; i++) {
  alert(i);
}
```

### 3.6.7 break和continue语句

break 和 continue 语句用于在循环中精确地控制代码的执行。其中， break 语句会立即退出循环，强制继续执行循环后面的语句。而 continue 语句虽然也是立即退出循环，但退出循环后会从循环的顶部继续执行。

```js
var num = 0;
for (var i=1; i < 10; i++) {
  if (i % 5 == 0) {
    break;
  }
  num++;
}
alert(num); //4
```

```js
var num = 0;
for (var i=1; i < 10; i++) {
  if (i % 5 == 0) {
    continue;
  }
  num++;
}
alert(num); //8
```

break 和 continue 语句都可以与 label 语句联合使用，从而返回代码中特定的位置。这种联合使用的情况多发生在循环嵌套的情况下。

```js
var num = 0;
outermost:
for (var i=0; i < 10; i++) {
  for (var j=0; j < 10; j++) {
    if (i == 5 && j == 5) {
      break outermost;
    }
    num++; 
  }
}
alert(num); //55
```

```js
var num = 0;
outermost:
for (var i=0; i < 10; i++) {
  for (var j=0; j < 10; j++) {
    if (i == 5 && j == 5) {
      continue outermost;
    }
    num++;
  }
}
alert(num); //95
```

虽然联用 break、 continue 和 label 语句能够执行复杂的操作，但如果使用过度，也会给调试带来麻烦。在此，我们建议如果使用 label 语句，一定要使用描述性的标签，同时不要嵌套过多的循环。

### 3.6.8 with语句

with 语句的作用是将代码的作用域设置到一个特定的对象中。 

```js
with (expression) statement;
```

定义 with 语句的目的主要是为了简化多次编写同一个对象的工作

```js
var qs = location.search.substring(1);
var hostName = location.hostname;
var url = location.href;

// 相当于
with(location){
var qs = search.substring(1);
var hostName = hostname;
var url = href;
}
```

严格模式下不允许使用 with 语句，否则将视为语法错误。由于大量使用 with 语句会导致性能下降，同时也会给调试代码造成困难，因此在开发大型应用程序时，不建议使用 with 语句。

### 3.6.9 switch语句

switch 语句与 if 语句的关系最为密切，而且也是在其他语言中普遍使用的一种流控制语句。ECMAScript 中 switch 语句的语法与其他基于 C 的语言非常接近。

```js
switch (expression) {
  case value: statement
    break;
  case value: statement
    break;
  case value: statement
    break;
  case value: statement
    break;
  default: statement
}
```

通过为每个 case 后面都添加一个 break 语句，就可以避免同时执行多个 case 代码的情况。假如确实需要混合几种情形，不要忘了在代码中添加注释，说明是有意省略了 break 关键字。

虽然 ECMAScript 中的 switch 语句借鉴自其他语言，但这个语句也有自己的特色。首先，可以在 switch 语句中使用任何数据类型（在很多其他语言中只能使用数值），无论是字符串，还是对象都没有问题。其次，每个 case 的值不一定是常量，可以是变量，甚至是表达式。

```js
switch ("hello world") {
  case "hello" + " world":
    alert("Greeting was found.");
    break;
  case "goodbye":
    alert("Closing was found.");
    break;
  default:
    alert("Unexpected message was found.");
}
```

使用表达式作为 case 值还可以实现下列操作。

```js
var num = 25;
switch (true) {
  case num < 0:
    alert("Less than 0.");
    break;
  case num >= 0 && num <= 10:
    alert("Between 0 and 10.");
    break;
  case num > 10 && num <= 20:
    alert("Between 10 and 20.");
    break;
  default:
   alert("More than 20.");
}
```

switch 语句在比较值时使用的是全等操作符，因此不会发生类型转换。

## 3.7 函数　

函数对任何语言来说都是一个核心的概念。通过函数可以封装任意多条语句，而且可以在任何地方、任何时候调用执行。 ECMAScript 中的函数使用 function 关键字来声明，后跟一组参数以及函数体。函数的基本语法如下所示：

```js
function functionName(arg0, arg1,...,argN) {
  statements
}
```

函数可以通过其函数名来调用，后面还要加上一对圆括号和参数（圆括号中的参数如果有多个，可以用逗号隔开）。

```js
function sayHi(name, message) {
  alert("Hello " + name + "," + message);
}

sayHi("Nicholas", "how are you today?");
```

ECMAScript 中的函数在定义时不必指定是否返回值。实际上，任何函数在任何时候都可以通过 return 语句后跟要返回的值来实现返回值。而位于 return 语句之后的任何代码都永远不会执行。

```js
function sum(num1, num2) {
  return num1 + num2;
}
```

当然，一个函数中也可以包含多个 return 语句。

```js
function diff(num1, num2) {
  if (num1 < num2) {
    return num2 - num1;
  } else {
    return num1 - num2;
  }
}
```

另外， return 语句也可以不带有任何返回值。在这种情况下，函数在停止执行后将返回 undefined值。这种用法一般用在需要提前停止函数执行而又不需要返回值的情况下。

```js
function sayHi(name, message) {
  return;
  alert("Hello " + name + "," + message); //永远不会调用
}
```

> 推荐的做法是要么让函数始终都返回一个值，要么永远都不要返回值。否则，如果函数有时候返回值，有时候有不返回值，会给调试代码带来不便。

严格模式对函数有一些限制：

- 不能把函数命名为 eval 或 arguments；
- 不能把参数命名为 eval 或 arguments；
- 不能出现两个命名参数同名的情况。

如果发生以上情况，就会导致语法错误，代码无法执行。

### 3.7.1 理解参数

ECMAScript 函数的参数与大多数其他语言中函数的参数有所不同。 ECMAScript 函数不介意传递进来多少个参数，也不在乎传进来参数是什么数据类型。也就是说，即便你定义的函数只接收两个参数，在调用这个函数时也未必一定要传递两个参数。可以传递一个、三个甚至不传递参数，而解析器永远不会有什么怨言。之所以会这样，原因是 ECMAScript 中的参数在内部是用一个数组来表示的。函数接收到的始终都是这个数组，而不关心数组中包含哪些参数（如果有参数的话）。如果这个数组中不包含任何元素，无所谓；如果包含多个元素，也没有问题。实际上，在函数体内可以通过 arguments 对象来访问这个参数数组，从而获取传递给函数的每一个参数。

其实， arguments 对象只是与数组类似（它并不是 Array 的实例），因为可以使用方括号语法访问它的每一个元素（即第一个元素是 `arguments[0]`，第二个元素是 `argumetns[1]`，以此类推），使用 length 属性来确定传递进来多少个参数。在前面的例子中， `sayHi()`函数的第一个参数的名字叫name，而该参数的值也可以通过访问 `arguments[0]`来获取。因此，那个函数也可以像下面这样重写，即不显式地使用命名参数：

```js
function sayHi() {
  alert("Hello " + arguments[0] + "," + arguments[1]);
}
```

这个事实说明了 ECMAScript 函数的一个重要特点：命名的参数只提供便利，但不是必需的。另外，在命名参数方面，其他语言可能需要事先创建一个函数签名，而将来的调用必须与该签名一致。但在 ECMAScript 中，没有这些条条框框，解析器不会验证命名参数。

通过访问 arguments 对象的 length 属性可以获知有多少个参数传递给了函数。下面这个函数会在每次被调用时，输出传入其中的参数个数：

```js
unction howManyArgs() {
  alert(arguments.length);
}
howManyArgs("string", 45); // 2
howManyArgs(); // 0
howManyArgs(12); // 1
```

由此可见，开发人员可以利用这一点让函数能够接收任意个参数并分别实现适当的功能。

```js
function doAdd() {
  if(arguments.length == 1) {
    alert(arguments[0] + 10);
  } else if (arguments.length == 2) {
    alert(arguments[0] + arguments[1]);
  }
}
doAdd(10); //20
doAdd(30, 20); //50
```

虽然这个特性算不上完美的重载，但也足够弥补 ECMAScript 的这一缺憾了。

另一个与参数相关的重要方面，就是 arguments 对象可以与命名参数一起使用，如下面的例子所示：

```js
function doAdd(num1, num2) {
  if(arguments.length == 1) {
    alert(num1 + 10);
  } else if (arguments.length == 2) {
    alert(arguments[0] + num2);
  }
}
```

关于 arguments 的行为，还有一点比较有意思。那就是它的值永远与对应命名参数的值保持同步。

```js
function doAdd(num1, num2) {
  arguments[1] = 10;
  alert(arguments[0] + num2);
}
```

每次执行这个`doAdd()`函数都会重写第二个参数，将第二个参数的值修改为 10。因为 arguments 对象中的值会自动反映到对应的命名参数，所以修改`arguments[1]`，也就修改了 num2，结果它们的
值都会变成 10。不过，这并不是说读取这两个值会访问相同的内存空间；它们的内存空间是独立的，但它们的值会同步。另外还要记住，如果只传入了一个参数，那么为`arguments[1]`设置的值不会反应到命名参数中。这是因为 arguments 对象的长度是由传入的参数个数决定的，不是由定义函数时的命名参数的个数决定的。

关于参数还要记住最后一点：没有传递值的命名参数将自动被赋予 undefined 值。这就跟定义了变量但又没有初始化一样。例如，如果只给`doAdd()`函数传递了一个参数，则 num2 中就会保存undefined 值。

严格模式对如何使用 arguments 对象做出了一些限制。首先，像前面例子中那样的赋值会变得无效。也就是说，即使把`arguments[1]`设置为 10， num2 的值仍然还是 undefined。其次，重写 arguments 的值会导致语法错误（代码将不会执行）。

> ECMAScript 中的所有参数传递的都是值，不可能通过引用传递参数。

### 3.7.2 没有重载

ECMAScript 函数不能像传统意义上那样实现重载。而在其他语言（如 Java）中，可以为一个函数编写两个定义，只要这两个定义的签名（接受的参数的类型和数量）不同即可。如前所述， ECMAScirpt函数没有签名，因为其参数是由包含零或多个值的数组来表示的。而没有函数签名，真正的重载是不可能做到的。后定义的函数覆盖了先定义的函数。

```js
function addSomeNumber(num){
  return num + 100;
}
function addSomeNumber(num) {
  return num + 200;
}
var result = addSomeNumber(100); //300
```

但可以通过检查传入函数中的参数的类型和数量并做出不同的反应，模仿方法的重载。

## 3.8 小结　

JavaScript 的核心语言特性在 ECMA-262 中是以名为 ECMAScript 的伪语言的形式来定义的。ECMAScript 中包含了所有基本的语法、操作符、数据类型以及完成基本的计算任务所必需的对象，但没有对取得输入和产生输出的机制作出规定。理解 ECMAScript 及其纷繁复杂的各种细节，是理解其在Web 浏览器中的实现——JavaScript 的关键。目前大多数实现所遵循的都是 ECMA-262 第 3 版，但很多也已经着手开始实现第 5 版了。以下简要总结了 ECMAScript 中基本的要素。

+ ECMAScript 中的基本数据类型包括 Undefined、 Null、 Boolean、 Number 和 String。
+ 与其他语言不同， ECMScript 没有为整数和浮点数值分别定义不同的数据类型， Number 类型可用于表示所有数值。
+ ECMAScript 中也有一种复杂的数据类型，即 Object 类型，该类型是这门语言中所有对象的基础类型。
+ 严格模式为这门语言中容易出错的地方施加了限制。
+ ECMAScript 提供了很多与 C 及其他类 C 语言中相同的基本操作符，包括算术操作符、布尔操作符、关系操作符、相等操作符及赋值操作符等。
+ ECMAScript 从其他语言中借鉴了很多流控制语句，例如 if 语句、 for 语句和 switch 语句等。

ECMAScript 中的函数与其他语言中的函数有诸多不同之处。

+ 无须指定函数的返回值，因为任何 ECMAScript 函数都可以在任何时候返回任何值。
+ 实际上，未指定返回值的函数返回的是一个特殊的 undefined 值。
+ ECMAScript 中也没有函数签名的概念，因为其函数参数是以一个包含零或多个值的数组的形式传递的。
+ 可以向 ECMAScript 函数传递任意数量的参数，并且可以通过 arguments 对象来访问这些参数。
+ 由于不存在函数签名的特性， ECMAScript 函数不能重载。

# 第 4 章 变量、作用域和内存问题　

按照 ECMA-262 的定义，JavaScript 的变量与其他语言的变量有很大区别。JavaScript 变量松散类型的本质，决定了它只是在特定时间用于保存特定值的一个名字而已。由于不存在定义某个变量必须要保存何种数据类型值的规则，变量的值及其数据类型可以在脚本的生命周期内改变。尽管从某种角度看，这可能是一个既有趣又强大，同时又容易出问题的特性，但 JavaScript 变量实际的复杂程度还远不止如此。

## 4.1 基本类型和引用类型的值

ECMAScript 变量可能包含两种不同数据类型的值：基本类型值和引用类型值。基本类型值指的是简单的数据段，而引用类型值指那些可能由多个值构成的对象。

在将一个值赋给变量时，解析器必须确定这个值是基本类型值还是引用类型值。第 3 章讨论了 5 种基本数据类型：Undefined、Null、Boolean、Number 和 String。这 5 种基本数据类型是按值访问的，因为可以操作保存在变量中的实际的值。

引用类型的值是保存在内存中的对象。与其他语言不同，JavaScript 不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间。在操作对象时，实际上是在操作对象的引用而不是实际的对象。为此，引用类型的值是按引用访问的。

> 在很多语言中，字符串以对象的形式来表示，因此被认为是引用类型的。ECMAScript 放弃了这一传统。

### 4.1.1 动态的属性

定义基本类型值和引用类型值的方式是类似的：创建一个变量并为该变量赋值。但是，当这个值保存到变量中以后，对不同类型值可以执行的操作则大相径庭。对于引用类型的值，我们可以为其添加属性和方法，也可以改变和删除其属性和方法。请看下面的例子：

```js
var person = new Object();
person.name = "Nicholas";
alert(person.name); //"Nicholas"
```

以上代码创建了一个对象并将其保存在了变量 person 中。然后，我们为该对象添加了一个名为 name 的属性，并将字符串值"Nicholas"赋给了这个属性。紧接着，又通过 `alert()`函数访问了这个新属性。如果对象不被销毁或者这个属性不被删除，则这个属性将一直存在。

但是，我们不能给基本类型的值添加属性，尽管这样做不会导致任何错误。比如：

```js
var name = "Nicholas";
name.age = 27;
alert(name.age); //undefined
```

在这个例子中，我们为字符串 name 定义了一个名为 age 的属性，并为该属性赋值 27。但在下一行访问这个属性时，发现该属性不见了。这说明只能给引用类型值动态地添加属性，以便将来使用。

### 4.1.2 复制变量值

除了保存的方式不同之外，在从一个变量向另一个变量复制基本类型值和引用类型值时，也存在不同。如果从一个变量向另一个变量复制基本类型的值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配的位置上。来看一个例子：

```js
var num1 = 5;
var num2 = num1;
```

在此，num1 中保存的值是 5。当使用 num1 的值来初始化 num2 时，num2 中也保存了值 5。但 num2 中的 5 与 num1 中的 5 是完全独立的，该值只是 num1 中 5 的一个副本。此后，这两个变量可以参与任何操作而不会相互影响。图 4-1 形象地展示了复制基本类型值的过程。

图 4-1

当从一个变量向另一个变量复制引用类型的值时，同样也会将存储在变量对象中的值复制一份放到为新变量分配的空间中。不同的是，这个值的副本实际上是一个指针，而这个指针指向存储在堆中的一个对象。复制操作结束后，两个变量实际上将引用同一个对象。因此，改变其中一个变量，就会影响另一个变量，如下面的例子所示：

```js
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "Nicholas";
alert(obj2.name); //"Nicholas"
```

首先，变量 obj1 保存了一个对象的新实例。然后，这个值被复制到了 obj2 中；换句话说，obj1 和 obj2 都指向同一个对象。这样，当为 obj1 添加 name 属性后，可以通过 obj2 来访问这个属性，因为这两个变量引用的都是同一个对象。图 4-2 展示了保存在变量对象中的变量和保存在堆中的对象之间的这种关系。

图 4-2

### 4.1.3 传递参数

ECMAScript 中所有函数的参数都是按值传递的。也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。基本类型值的传递如同基本类型变量的复制一样，而引用类型值的传递，则如同引用类型变量的复制一样。有不少开发人员在这一点上可能会感到困惑，因为访问变量有按值和按引用两种方式，而参数只能按值传递。

在向参数传递基本类型的值时，被传递的值会被复制给一个局部变量（即命名参数，或者用 ECMAScript 的概念来说，就是 arguments 对象中的一个元素）。在向参数传递引用类型的值时，会把这个值在内存中的地址复制给一个局部变量，因此这个局部变量的变化会反映在函数的外部。请看下面这个例子：

```js
function addTen(num) {
  num += 10;
  return num;
}
var count = 20;
var result = addTen(count);
alert(count); //20，没有变化
alert(result); //30
```

这里的函数 `addTen()`有一个参数 num，而参数实际上是函数的局部变量。在调用这个函数时，变量 count 作为参数被传递给函数，这个变量的值是 20。于是，数值 20 被复制给参数 num 以便在 `addTen()`中使用。在函数内部，参数 num 的值被加上了 10，但这一变化不会影响函数外部的 count 变量。参数 num 与变量 count 互不相识，它们仅仅是具有相同的值。假如 num 是按引用传递的话，那么变量 count 的值也将变成 30，从而反映函数内部的修改。当然，使用数值等基本类型值来说明按值传递参数比较简单，但如果使用对象，那问题就不怎么好理解了。再举一个例子：

```js
function setName(obj) {
  obj.name = "Nicholas";
}
var person = new Object();
setName(person);
alert(person.name); //"Nicholas"
```

以上代码中创建一个对象，并将其保存在了变量 person 中。然后，这个变量被传递到 `setName()`函数中之后就被复制给了 obj。在这个函数内部，obj 和 person 引用的是同一个对象。换句话说，即使这个变量是按值传递的，obj 也会按引用来访问同一个对象。于是，当在函数内部为 obj 添加 name 属性后，函数外部的 person 也将有所反映；因为 person 指向的对象在堆内存中只有一个，而且是全局对象。有很多开发人员错误地认为：在局部作用域中修改的对象会在全局作用域中反映出来，就说明参数是按引用传递的。为了证明对象是按值传递的，我们再看一看下面这个经过修改的例子：

```js
function setName(obj) {
  obj.name = "Nicholas";
  obj = new Object();
  obj.name = "Greg";
}
var person = new Object();
setName(person);
alert(person.name); //"Nicholas"
```

这个例子与前一个例子的唯一区别，就是在 `setName()`函数中添加了两行代码：一行代码为 obj 重新定义了一个对象，另一行代码为该对象定义了一个带有不同值的 name 属性。在把 person 传递给 `setName()`后，其 name 属性被设置为"Nicholas"。然后，又将一个新对象赋给变量 obj，同时将其 name 属性设置为"Greg"。如果 person 是按引用传递的，那么 person 就会自动被修改为指向其 name 属性值为"Greg"的新对象。但是，当接下来再访问 person.name 时，显示的值仍然是"Nicholas"。这说明即使在函数内部修改了参数的值，但原始的引用仍然保持未变。实际上，当在函数内部重写 obj 时，这个变量引用的就是一个局部对象了。而这个局部对象会在函数执行完毕后立即被销毁。

> 可以把 ECMAScript 函数的参数想象成局部变量。

### 4.1.4 检测类型

要检测一个变量是不是基本数据类型？第 3 章介绍的 typeof 操作符是最佳的工具。说得更具体一点，typeof 操作符是确定一个变量是字符串、数值、布尔值，还是 undefined 的最佳工具。如果变量的值是一个对象或 null，则 typeof 操作符会像下面例子中所示的那样返回"object"：

```js
var s = "Nicholas";
var b = true;
var i = 22;
var u;
var n = null;
var o = new Object();
alert(typeof s); //string
alert(typeof i); //number
alert(typeof b); //boolean
alert(typeof u); //undefined
alert(typeof n); //object
alert(typeof o); //object
```

虽然在检测基本数据类型时 typeof 是非常得力的助手，但在检测引用类型的值时，这个操作符的用处不大。通常，我们并不是想知道某个值是对象，而是想知道它是什么类型的对象。为此，ECMAScript 提供了 instanceof 操作符，其语法如下所示：

```js
result = variable instanceof constructor;
```

如果变量是给定引用类型（根据它的原型链来识别；第 6 章将介绍原型链）的实例，那么 instanceof 操作符就会返回 true。请看下面的例子：

```js
alert(person instanceof Object); // 变量 person 是 Object 吗？
alert(colors instanceof Array); // 变量 colors 是 Array 吗？
alert(pattern instanceof RegExp); // 变量 pattern 是 RegExp 吗？
```

根据规定，所有引用类型的值都是 Object 的实例。因此，在检测一个引用类型值和 Object 构造函数时，instanceof 操作符始终会返回 true。当然，如果使用 instanceof 操作符检测基本类型的值，则该操作符始终会返回 false，因为基本类型不是对象。

> 使用 typeof 操作符检测函数时，该操作符会返回"function"。在 Safari 5 及之前版本和 Chrome 7 及之前版本中使用 typeof 检测正则表达式时，由于规范的原因，这个操作符也返回"function"。ECMA-262 规定任何在内部实现`[[Call]]`方法的对象都应该在应用 typeof 操作符时返回"function"。由于上述浏览器中的正则表达式也实现了这个方法，因此对正则表达式应用 typeof 会返回"function"。在 IE 和 Firefox 中，对正则表达式应用 typeof 会返回"object"。

## 4.2 执行环境及作用域　

执行环境（execution context，为简单起见，有时也称为“环境”）是 JavaScript 中最为重要的一个概念。执行环境定义了变量或函数有权访问的其他数据，决定了它们各自的行为。每个执行环境都有一个与之关联的变量对象（variableobject），环境中定义的所有变量和函数都保存在这个对象中。虽然我们编写的代码无法访问这个对象，但解析器在处理数据时会在后台使用它。

全局执行环境是最外围的一个执行环境。根据 ECMAScript 实现所在的宿主环境不同，表示执行环境的对象也不一样。在 Web 浏览器中，全局执行环境被认为是 window 对象（第 7 章将详细讨论），因此所有全局变量和函数都是作为 window 对象的属性和方法创建的。某个执行环境中的所有代码执行完毕后，该环境被销毁，保存在其中的所有变量和函数定义也随之销毁（全局执行环境直到应用程序退出——例如关闭网页或浏览器——时才会被销毁）。

每个函数都有自己的执行环境。当执行流进入一个函数时，函数的环境就会被推入一个环境栈中。而在函数执行之后，栈将其环境弹出，把控制权返回给之前的执行环境。ECMAScript 程序中的执行流正是由这个方便的机制控制着。

当代码在一个环境中执行时，会创建变量对象的一个作用域链（scope chain）。作用域链的用途，是保证对执行环境有权访问的所有变量和函数的有序访问。作用域链的前端，始终都是当前执行的代码所在环境的变量对象。如果这个环境是函数，则将其活动对象（activation object）作为变量对象。活动对象在最开始时只包含一个变量，即 arguments 对象（这个对象在全局环境中是不存在的）。作用域链中的下一个变量对象来自包含（外部）环境，而再下一个变量对象则来自下一个包含环境。这样，一直延续到全局执行环境；全局执行环境的变量对象始终都是作用域链中的最后一个对象。

标识符解析是沿着作用域链一级一级地搜索标识符的过程。搜索过程始终从作用域链的前端开始，然后逐级地向后回溯，直至找到标识符为止（如果找不到标识符，通常会导致错误发生）。

请看下面的示例代码：

```js
var color = "blue";
function changeColor() {
  if (color === "blue") {
    color = "red";
  } else {
    color = "blue";
  }
}
changeColor();
alert("Color is now " + color);
```

在这个简单的例子中，函数 `changeColor()`的作用域链包含两个对象：它自己的变量对象（其中定义着 arguments 对象）和全局环境的变量对象。可以在函数内部访问变量 color，就是因为可以在这个作用域链中找到它。

此外，在局部作用域中定义的变量可以在局部环境中与全局变量互换使用，如下面这个例子所示：

```js
var color = "blue";
function changeColor() {
  var anotherColor = "red";
  function swapColors() {
    var tempColor = anotherColor;
    anotherColor = color;
    color = tempColor;
    // 这里可以访问 color、 anotherColor 和 tempColor
  }
  // 这里可以访问 color 和 anotherColor，但不能访问 tempColor
  swapColors();
}
// 这里只能访问 color
changeColor();
```

以上代码共涉及 3 个执行环境：全局环境、`changeColor()`的局部环境和 `swapColors()`的局部环境。全局环境中有一个变量 color 和一个函数 `changeColor()`。`changeColor()`的局部环境中有一个名为 anotherColor 的变量和一个名为 `swapColors()`的函数，但它也可以访问全局环境中的变量 color。`swapColors()`的局部环境中有一个变量 tempColor，该变量只能在这个环境中访问到。无论全局环境还是 `changeColor()`的局部环境都无权访问 tempColor。然而，在 `swapColors()`内部则可以访问其他两个环境中的所有变量，因为那两个环境是它的父执行环境。图 4-3 形象地展示了前面这个例子的作用域链。

图 4-3

图 4-3 中的矩形表示特定的执行环境。其中，内部环境可以通过作用域链访问所有的外部环境，但外部环境不能访问内部环境中的任何变量和函数。这些环境之间的联系是线性、有次序的。每个环境都可以向上搜索作用域链，以查询变量和函数名；但任何环境都不能通过向下搜索作用域链而进入另一个执行环境。对于这个例子中的 `swapColors()`而言，其作用域链中包含 3 个对象：`swapColors()`的变量对象、`changeColor()`的变量对象和全局变量对象。`swapColors()`的局部环境开始时会先在自己的变量对象中搜索变量和函数名，如果搜索不到则再搜索上一级作用域链。`changeColor()`的作用域链中只包含两个对象：它自己的变量对象和全局变量对象。这也就是说，它不能访问 `swapColors()`的环境。

> 函数参数也被当作变量来对待，因此其访问规则与执行环境中的其他变量相同。

### 4.2.1 延长作用域链

虽然执行环境的类型总共只有两种——全局和局部（函数），但还是有其他办法来延长作用域链。这么说是因为有些语句可以在作用域链的前端临时增加一个变量对象，该变量对象会在代码执行后被移除。在两种情况下会发生这种现象。具体来说，就是当执行流进入下列任何一个语句时，作用域链就会得到加长：

- try-catch 语句的 catch 块；
- with 语句。

这两个语句都会在作用域链的前端添加一个变量对象。对 with 语句来说，会将指定的对象添加到作用域链中。对 catch 语句来说，会创建一个新的变量对象，其中包含的是被抛出的错误对象的声明。下面看一个例子。

```js
function buildUrl() {
  var qs = "?debug=true";
  with (location) {
    var url = href + qs;
  }
  return url;
}
```

在此，with 语句接收的是 location 对象，因此其变量对象中就包含了 location 对象的所有属性和方法，而这个变量对象被添加到了作用域链的前端。`buildUrl()`函数中定义了一个变量 qs。当在 with 语句中引用变量 href 时（实际引用的是 location.href），可以在当前执行环境的变量对象中找到。当引用变量 qs 时，引用的则是在 `buildUrl()`中定义的那个变量，而该变量位于函数环境的变量对象中。至于 with 语句内部，则定义了一个名为 url 的变量，因而 url 就成了函数执行环境的一部分，所以可以作为函数的值被返回。

> 在 IE8 及之前版本的 JavaScript 实现中，存在一个与标准不一致的地方，即在 catch 语句中捕获的错误对象会被添加到执行环境的变量对象，而不是 catch 语句的变量对象中。换句话说，即使是在 catch 块的外部也可以访问到错误对象。IE9 修复了这个问题。

### 4.2.2 没有块级作用域

JavaScript 没有块级作用域经常会导致理解上的困惑。在其他类 C 的语言中，由花括号封闭的代码块都有自己的作用域（如果用 ECMAScript 的话来讲，就是它们自己的执行环境），因而支持根据条件来定义变量。例如，下面的代码在 JavaScript 中并不会得到想象中的结果：

```js
if (true) {
  var color = "blue";
}
alert(color); //"blue"
```

这里是在一个 if 语句中定义了变量 color。如果是在 C、C++或 Java 中，color 会在 if 语句执行完毕后被销毁。但在 JavaScript 中，if 语句中的变量声明会将变量添加到当前的执行环境（在这里是全局环境）中。在使用 for 语句时尤其要牢记这一差异，例如：

```js
for (var i = 0; i < 10; i++) {
  doSomething(i);
}
alert(i); //10
```

对于有块级作用域的语言来说，for 语句初始化变量的表达式所定义的变量，只会存在于循环的环境之中。而对于 JavaScript 来说，由 for 语句创建的变量 i 即使在 for 循环执行结束后，也依旧会存在于循环外部的执行环境中。

1. 声明变量

使用 var 声明的变量会自动被添加到最接近的环境中。在函数内部，最接近的环境就是函数的局部环境；在 with 语句中，最接近的环境是函数环境。如果初始化变量时没有使用 var 声明，该变量会自动被添加到全局环境。如下所示：

```js
function add(num1, num2) {
  var sum = num1 + num2;
  return sum;
}
var result = add(10, 20); //30
alert(sum); //由于 sum 不是有效的变量，因此会导致错误
```

以上代码中的函数 `add()`定义了一个名为 sum 的局部变量，该变量包含加法操作的结果。虽然结果值从函数中返回了，但变量 sum 在函数外部是访问不到的。如果省略这个例子中的 var 关键字，那么当 `add()`执行完毕后，sum 也将可以访问到：

```js
function add(num1, num2) {
  sum = num1 + num2;
  return sum;
}
var result = add(10, 20); //30
alert(sum); //30
```

这个例子中的变量 sum 在被初始化赋值时没有使用 var 关键字。于是，当调用完 `add()`之后，添加到全局环境中的变量 sum 将继续存在；即使函数已经执行完毕，后面的代码依旧可以访问它。

> 在编写 JavaScript 代码的过程中，不声明而直接初始化变量是一个常见的错误做法，因为这样可能会导致意外。我们建议在初始化变量之前，一定要先声明，这样就可以避免类似问题。在严格模式下，初始化未经声明的变量会导致错误。

2. 查询标识符

当在某个环境中为了读取或写入而引用一个标识符时，必须通过搜索来确定该标识符实际代表什么。搜索过程从作用域链的前端开始，向上逐级查询与给定名字匹配的标识符。如果在局部环境中找到了该标识符，搜索过程停止，变量就绪。如果在局部环境中没有找到该变量名，则继续沿作用域链向上搜索。搜索过程将一直追溯到全局环境的变量对象。如果在全局环境中也没有找到这个标识符，则意味着该变量尚未声明。

通过下面这个示例，可以理解查询标识符的过程：

```js
var color = "blue";
function getColor() {
  return color;
}
alert(getColor()); //"blue"
```

调用本例中的函数 `getColor()`时会引用变量 color。为了确定变量 color 的值，将开始一个两步的搜索过程。首先，搜索 `getColor()`的变量对象，查找其中是否包含一个名为 color 的标识符。在没有找到的情况下，搜索继续到下一个变量对象（全局环境的变量对象），然后在那里找到了名为 color 的标识符。因为搜索到了定义这个变量的变量对象，搜索过程宣告结束。图 4-4 形象地展示了上述搜索过程。

图 4-4

在这个搜索过程中，如果存在一个局部的变量的定义，则搜索会自动停止，不再进入另一个变量对象。换句话说，如果局部环境中存在着同名标识符，就不会使用位于父环境中的标识符，如下面的例子所示：

```js
var color = "blue";
function getColor() {
  var color = "red";
  return color;
}
alert(getColor()); //"red"
```

修改后的代码在 `getColor()`函数中声明了一个名为 color 的局部变量。调用函数时，该变量就会被声明。而当函数中的第二行代码执行时，意味着必须找到并返回变量 color 的值。搜索过程首先从局部环境中开始，而且在这里发现了一个名为 color 的变量，其值为"red"。因为变量已经找到了，所以搜索即行停止，return 语句就使用这个局部变量，并为函数会返回"red"。也就是说，任何位于局部变量 color 的声明之后的代码，如果不使用 window.color 都无法访问全局 color 变量。

> 变量查询也不是没有代价的。很明显，访问局部变量要比访问全局变量更快，因为不用向上搜索作用域链。JavaScript 引擎在优化标识符查询方面做得不错，因此这个差别在将来恐怕就可以忽略不计了。

## 4.3 垃圾收集　

JavaScript 具有自动垃圾收集机制，也就是说，执行环境会负责管理代码执行过程中使用的内存。而在 C 和 C++之类的语言中，开发人员的一项基本任务就是手工跟踪内存的使用情况，这是造成许多问题的一个根源。在编写 JavaScript 程序时，开发人员不用再关心内存使用问题，所需内存的分配以及无用内存的回收完全实现了自动管理。这种垃圾收集机制的原理其实很简单：找出那些不再继续使用的变量，然后释放其占用的内存。为此，垃圾收集器会按照固定的时间间隔（或代码执行中预定的收集时间），周期性地执行这一操作。

下面我们来分析一下函数中局部变量的正常生命周期。局部变量只在函数执行的过程中存在。而在这个过程中，会为局部变量在栈（或堆）内存上分配相应的空间，以便存储它们的值。然后在函数中使用这些变量，直至函数执行结束。此时，局部变量就没有存在的必要了，因此可以释放它们的内存以供将来使用。在这种情况下，很容易判断变量是否还有存在的必要；但并非所有情况下都这么容易就能得出结论。垃圾收集器必须跟踪哪个变量有用哪个变量没用，对于不再有用的变量打上标记，以备将来收回其占用的内存。用于标识无用变量的策略可能会因实现而异，但具体到浏览器中的实现，则通常有两个策略。

### 4.3.1 标记清除

JavaScript 中最常用的垃圾收集方式是标记清除（mark-and-sweep）。当变量进入环境（例如，在函数中声明一个变量）时，就将这个变量标记为“进入环境”。从逻辑上讲，永远不能释放进入环境的变量所占用的内存，因为只要执行流进入相应的环境，就可能会用到它们。而当变量离开环境时，则将其标记为“离开环境”。

可以使用任何方式来标记变量。比如，可以通过翻转某个特殊的位来记录一个变量何时进入环境，或者使用一个“进入环境的”变量列表及一个“离开环境的”变量列表来跟踪哪个变量发生了变化。说到底，如何标记变量其实并不重要，关键在于采取什么策略。

垃圾收集器在运行的时候会给存储在内存中的所有变量都加上标记（当然，可以使用任何标记方式）。然后，它会去掉环境中的变量以及被环境中的变量引用的变量的标记。而在此之后再被加上标记的变量将被视为准备删除的变量，原因是环境中的变量已经无法访问到这些变量了。最后，垃圾收集器完成内存清除工作，销毁那些带标记的值并回收它们所占用的内存空间。

到 2008 年为止， IE、 Firefox、 Opera、 Chrome 和 Safari 的 JavaScript 实现使用的都是标记清除式的垃圾收集策略（或类似的策略），只不过垃圾收集的时间间隔互有不同。

### 4.3.2 引用计数

另一种不太常见的垃圾收集策略叫做引用计数（reference counting）。引用计数的含义是跟踪记录每个值被引用的次数。当声明了一个变量并将一个引用类型值赋给该变量时，则这个值的引用次数就是 1。如果同一个值又被赋给另一个变量，则该值的引用次数加 1。相反，如果包含对这个值引用的变量又取得了另外一个值，则这个值的引用次数减 1。当这个值的引用次数变成 0 时，则说明没有办法再访问这个值了，因而就可以将其占用的内存空间回收回来。这样，当垃圾收集器下次再运行时，它就会释放那些引用次数为零的值所占用的内存。

Netscape Navigator 3.0 是最早使用引用计数策略的浏览器，但很快它就遇到了一个严重的问题：循环引用。循环引用指的是对象 A 中包含一个指向对象 B 的指针，而对象 B 中也包含一个指向对象 A 的引用。请看下面这个例子：

```js
function problem() {
  var objectA = new Object();
  var objectB = new Object();
  objectA.someOtherObject = objectB;
  objectB.anotherObject = objectA;
}
```

在这个例子中， objectA 和 objectB 通过各自的属性相互引用；也就是说，这两个对象的引用次数都是 2。在采用标记清除策略的实现中，由于函数执行之后，这两个对象都离开了作用域，因此这种相互引用不是个问题。但在采用引用计数策略的实现中，当函数执行完毕后， objectA 和 objectB 还将继续存在，因为它们的引用次数永远不会是 0。假如这个函数被重复多次调用，就会导致大量内存得不到回收。为此， Netscape 在 Navigator 4.0 中放弃了引用计数方式，转而采用标记清除来实现其垃圾收集机制。可是，引用计数导致的麻烦并未就此终结。

我们知道， IE 中有一部分对象并不是原生 JavaScript 对象。例如，其 BOM 和 DOM 中的对象就是使用 C++以 COM（Component Object Model，组件对象模型）对象的形式实现的，而 COM 对象的垃圾收集机制采用的就是引用计数策略。因此，即使 IE 的 JavaScript 引擎是使用标记清除策略来实现的，但 JavaScript 访问的 COM 对象依然是基于引用计数策略的。换句话说，只要在 IE 中涉及 COM 对象，就会存在循环引用的问题。下面这个简单的例子，展示了使用 COM 对象导致的循环引用问题：

```js
var element = document.getElementById("some_element");
var myObject = new Object();
myObject.element = element;
element.someObject = myObject;
```

这个例子在一个 DOM 元素（element）与一个原生 JavaScript 对象（myObject）之间创建了循环引用。其中，变量 myObject 有一个名为 element 的属性指向 element 对象；而变量 element 也有一个属性名叫 someObject 回指 myObject。由于存在这个循环引用，即使将例子中的 DOM 从页面中移除，它也永远不会被回收。

为了避免类似这样的循环引用问题，最好是在不使用它们的时候手工断开原生 JavaScript 对象与 DOM 元素之间的连接。例如，可以使用下面的代码消除前面例子创建的循环引用：

```js
myObject.element = null;
element.someObject = null;
```

将变量设置为 null 意味着切断变量与它此前引用的值之间的连接。当垃圾收集器下次运行时，就会删除这些值并回收它们占用的内存。

为了解决上述问题， IE9 把 BOM 和 DOM 对象都转换成了真正的 JavaScript 对象。这样，就避免了两种垃圾收集算法并存导致的问题，也消除了常见的内存泄漏现象。

> 导致循环引用的情况不止这些，其他一些情况将在本书中陆续介绍。

### 4.3.3 性能问题

垃圾收集器是周期性运行的，而且如果为变量分配的内存数量很可观，那么回收工作量也是相当大的。在这种情况下，确定垃圾收集的时间间隔是一个非常重要的问题。说到垃圾收集器多长时间运行一次，不禁让人联想到 IE 因此而声名狼藉的性能问题。 IE 的垃圾收集器是根据内存分配量运行的，具体一点说就是 256 个变量、 4096 个对象（或数组）字面量和数组元素（slot）或者 64KB 的字符串。达到上述任何一个临界值，垃圾收集器就会运行。这种实现方式的问题在于，如果一个脚本中包含那么多变量，那么该脚本很可能会在其生命周期中一直保有那么多的变量。而这样一来，垃圾收集器就不得不频繁地运行。结果，由此引发的严重性能问题促使 IE7 重写了其垃圾收集例程。

随着 IE7 的发布，其 JavaScript 引擎的垃圾收集例程改变了工作方式：触发垃圾收集的变量分配、字面量和（或）数组元素的临界值被调整为动态修正。 IE7 中的各项临界值在初始时与 IE6 相等。如果垃圾收集例程回收的内存分配量低于 15%，则变量、字面量和（或）数组元素的临界值就会加倍。如果例程回收了 85%的内存分配量，则将各种临界值重置回默认值。这一看似简单的调整，极大地提升了 IE 在运行包含大量 JavaScript 的页面时的性能。

> 事实上，在有的浏览器中可以触发垃圾收集过程，但我们不建议读者这样做。在 IE 中，调用 `window.CollectGarbage()`方法会立即执行垃圾收集。在 Opera 7 及更高版本中，调用 `window.opera.collect()`也会启动垃圾收集例程。

### 4.3.4 管理内存

使用具备垃圾收集机制的语言编写程序，开发人员一般不必操心内存管理的问题。但是， JavaScript 在进行内存管理及垃圾收集时面临的问题还是有点与众不同。其中最主要的一个问题，就是分配给 Web 浏览器的可用内存数量通常要比分配给桌面应用程序的少。这样做的目的主要是出于安全方面的考虑，目的是防止运行 JavaScript 的网页耗尽全部系统内存而导致系统崩溃。内存限制问题不仅会影响给变量分配内存，同时还会影响调用栈以及在一个线程中能够同时执行的语句数量。

因此，确保占用最少的内存可以让页面获得更好的性能。而优化内存占用的最佳方式，就是为执行中的代码只保存必要的数据。一旦数据不再有用，最好通过将其值设置为 null 来释放其引用——这个做法叫做解除引用（dereferencing）。这一做法适用于大多数全局变量和全局对象的属性。局部变量会在它们离开执行环境时自动被解除引用，如下面这个例子所示：

```js
function createPerson(name) {
  var localPerson = new Object();
  localPerson.name = name;
  return localPerson;
}
var globalPerson = createPerson("Nicholas");
// 手工解除 globalPerson 的引用
globalPerson = null;
```

在这个例子中，变量 globalPerson 取得了 `createPerson()`函数返回的值。在 `createPerson()`函数内部，我们创建了一个对象并将其赋给局部变量 localPerson，然后又为该对象添加了一个名为 name 的属性。最后，当调用这个函数时， localPerson 以函数值的形式返回并赋给全局变量 globalPerson。由于 localPerson 在 `createPerson()`函数执行完毕后就离开了其执行环境，因此无需我们显式地去为它解除引用。但是对于全局变量 globalPerson 而言，则需要我们在不使用它的时候手工为它解除引用，这也正是上面例子中最后一行代码的目的。

不过，解除一个值的引用并不意味着自动回收该值所占用的内存。解除引用的真正作用是让值脱离执行环境，以便垃圾收集器下次运行时将其回收。

## 4.4 小结　

JavaScript 变量可以用来保存两种类型的值：基本类型值和引用类型值。基本类型的值源自以下 5 种基本数据类型： Undefined、 Null、 Boolean、 Number 和 String。基本类型值和引用类型值具有以下特点：

- 基本类型值在内存中占据固定大小的空间，因此被保存在栈内存中；
- 从一个变量向另一个变量复制基本类型的值，会创建这个值的一个副本；
- 引用类型的值是对象，保存在堆内存中；
- 包含引用类型值的变量实际上包含的并不是对象本身，而是一个指向该对象的指针；
- 从一个变量向另一个变量复制引用类型的值，复制的其实是指针，因此两个变量最终都指向同一个对象；
- 确定一个值是哪种基本类型可以使用 typeof 操作符，而确定一个值是哪种引用类型可以使用 instanceof 操作符。

所有变量（包括基本类型和引用类型）都存在于一个执行环境（也称为作用域）当中，这个执行环境决定了变量的生命周期，以及哪一部分代码可以访问其中的变量。以下是关于执行环境的几点总结：

- 执行环境有全局执行环境（也称为全局环境）和函数执行环境之分；
- 每次进入一个新执行环境，都会创建一个用于搜索变量和函数的作用域链；
- 函数的局部环境不仅有权访问函数作用域中的变量，而且有权访问其包含（父）环境，乃至全局环境；
- 全局环境只能访问在全局环境中定义的变量和函数，而不能直接访问局部环境中的任何数据；
- 变量的执行环境有助于确定应该何时释放内存。

JavaScript 是一门具有自动垃圾收集机制的编程语言，开发人员不必关心内存分配和回收问题。可以对 JavaScript 的垃圾收集例程作如下总结。

- 离开作用域的值将被自动标记为可以回收，因此将在垃圾收集期间被删除。
- “标记清除”是目前主流的垃圾收集算法，这种算法的思想是给当前不使用的值加上标记，然后再回收其内存。
- 另一种垃圾收集算法是“引用计数”，这种算法的思想是跟踪记录所有值被引用的次数。 JavaScript 引擎目前都不再使用这种算法；但在 IE 中访问非原生 JavaScript 对象（如 DOM 元素）时，这种算法仍然可能会导致问题。
- 当代码中存在循环引用现象时，“引用计数”算法就会导致问题。
- 解除变量的引用不仅有助于消除循环引用现象，而且对垃圾收集也有好处。为了确保有效地回收内存，应该及时解除不再使用的全局对象、全局对象属性以及循环引用变量的引用。

# 第5章 引用类型　

引用类型的值（对象）是引用类型的一个实例。在 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起。它也常被称为类，但这种称呼并不妥当。尽管 ECMAScript 从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。引用类型有时候也被称为对象定义，因为它们描述的是一类对象所具有的属性和方法。

如前所述，对象是某个特定引用类型的实例。新对象是使用 new 操作符后跟一个构造函数来创建的。构造函数本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的。请看下面这行代码：

```js
var person = new Object();
```

ECMAScript 提供了很多原生引用类型（例如 Object），以便开发人员用以实现常见的计算任务。

## 5.1 Object类型

大多数引用类型值都是 Object 类型的实例；而且， Object 也是ECMAScript 中使用最多的一个类型。虽然 Object 的实例不具备多少功能，但对于在应用程序中存储和传输数据而言，它们确实是非常理想的选择。

创建 Object 实例的方式有两种，第一种使用 new 操作符后跟 Object 构造函数。

```js
var person = new Object();
person.name = "Nicholas";
person.age = 29;
```

另一种方式是使用对象字面量表示法。对象字面量是对象定义的一种简写形式，目的在于简化创建包含大量属性的对象的过程。

```js
var person = {
  name : "Nicholas",
  age : 29
};
```

在对象字面量中，使用逗号来分隔不同的属性，因此"Nicholas"后面是一个逗号。但是，在 age 属性的值 29 的后面不能添加逗号，因为 age 是这个对象的最后一个属性。在最后一个属性后面添加逗号，会在 IE7 及更早版本和 Opera 中导致错误。

在使用对象字面量语法时，属性名也可以使用字符串，如下面这个例子所示。

```js
var person = {
  "name" : "Nicholas",
  "age" : 29,
  5 : true
};
```

另外，使用对象字面量语法时，如果留空其花括号，则可以定义只包含默认属性和方法的对象，如下所示：

```js
var person = {}; //与 new Object()相同
person.name = "Nicholas";
person.age = 29;
```

> 在通过对象字面量定义对象时，实际上不会调用 Object 构造函数（Firefox 2 及更早版本会调用 Object 构造函数；但 Firefox 3 之后就不会了）。

虽然可以使用前面介绍的任何一种方法来定义对象，但开发人员更青睐对象字面量语法，因为这种语法要求的代码量少，而且能够给人封装数据的感觉。实际上，对象字面量也是向函数传递大量可选参数的首选方式，例如：

```js
function displayInfo(args) {
  var output = "";
  if (typeof args.name == "string"){
    output += "Name: " + args.name + "\n";
  }
  if (typeof args.age == "number") {
    output += "Age: " + args.age + "\n";
  }
  alert(output);
}

displayInfo({
  name: "Nicholas",
  age: 29
});

displayInfo({
  name: "Greg"
});
```

> 这种传递参数的模式最适合需要向函数传入大量可选参数的情形。一般来讲，命名参数虽然容易处理，但在有多个可选参数的情况下就会显示不够灵活。最好的做法是对那些必需值使用命名参数，而使用对象字面量来封装多个可选参数。

一般来说，访问对象属性时使用的都是点表示法，这也是很多面向对象语言中通用的语法。不过，在 JavaScript 也可以使用方括号表示法来访问对象的属性。在使用方括号语法时，应该将要访问的属性以字符串的形式放在方括号中，如下面的例子所示。

```js
alert(person["name"]); //"Nicholas"
alert(person.name); //"Nicholas"
```

从功能上看，这两种访问对象属性的方法没有任何区别。但方括号语法的主要优点是可以通过变量来访问属性，例如：

```js
var propertyName = "name";
alert(person[propertyName]); //"Nicholas"
```

如果属性名中包含会导致语法错误的字符，或者属性名使用的是关键字或保留字，也可以使用方括号表示法。例如：

```js
person["first name"] = "Nicholas";
```

由于"first name"中包含一个空格，所以不能使用点表示法来访问它。然而，属性名中是可以包含非字母非数字的，这时候就可以使用方括号表示法来访问它们。

通常，除非必须使用变量来访问属性，否则我们建议使用点表示法。

## 5.2 Array类型　

虽然 ECMAScript 数组与其他语言中的数组都是数据的有序列表，但与其他语言不同的是， ECMAScript 数组的每一项可以保存任何类型的数据。而且， ECMAScript 数组的大小是可以动态调整的，即可以随着数据的添加自动增长以容纳新增数据。

创建数字的基本方式有两种，第一是使用 Array 构造函数，可以保留 new 操作符也可以省略；第二种基本方法是使用数组字面量表示法，数组字面量是由包含数组项的方括号表示，多个数组项之间以逗号隔开。如果在数组字面量的最后一项添加逗号，由于 IE 的实现与其他浏览器不一致，可能导致不同的结果，因此强烈建议不要使用这种语法。

```js
var colors = new Array(3); // 创建一个包含 3 项的数组
var names = new Array("Greg"); // 创建一个包含 1 项，即字符串"Greg"的数组

var colors = Array(3); // 创建一个包含 3 项的数组
var names = Array("Greg"); // 创建一个包含 1 项，即字符串"Greg"的数组

var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
var names = []; // 创建一个空数组
var values = [1,2,]; // 不要这样！这样会创建一个包含 2 或 3 项的数组
var options = [,,,,,]; // 不要这样！这样会创建一个包含 5 或 6 项的数组
```

在读取和设置数组的值时，要使用方括号并提供相应值的基于 0 的的数字索引。方括号中的索引表示要访问的值。如果索引小于数组中的项数，则返回对应项的值。

```js
var colors = ["red", "blue", "green"]; // 定义一个字符串数组
alert(colors[0]); // 显示第一项
colors[2] = "black"; // 修改第三项
colors[3] = "brown"; // 新增第四项
```
设置数组的值也使用相同的语法，但会替换指定位置的值。如果设置某个值的索引超过了数组现有项数，则数组的长度也会相应增加。

数组的项数保存在其 length 属性中，这个属性始终会返回 0 或更大的值。利用 length 属性也可以方便地在数组末尾添加新项。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
colors[99] = "black"; // （在位置 99）添加一种颜色
alert(colors.length); // 100
```

数组最多可以包含 4 294 967 295 个项，这几乎已经能够满足任何编程需求了。如果想添加的项数超过这个上限值，就会发生异常。而创建一个初始大小与这个上限值接近的数组，则可能会导致运行时间超长的脚本错误。

### 5.2.1 检查数组

自从 ECMAScript 3 做出规定以后，就出现了确定某个对象是不是数组的经典问题。对于一个网页，或者一个全局作用域而言，使用 `instanceof` 操作符就能得到满意的结果：

```js
if (value instanceof Array){
  //对数组执行某些操作
}
```

instanceof 操作符的问题在于，它假定只有一个全局执行环境。如果网页中包含多个框架，那实际上就存在两个以上不同的全局执行环境，从而存在两个以上不同版本的 Array 构造函数。如果你从一个框架向另一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。

为了解决这个问题， ECMAScript 5 新增了 `Array.isArray()`方法。这个方法的目的是最终确定某个值到底是不是数组，而不管它是在哪个全局执行环境中创建的。这个方法的用法如下。

```js
if (Array.isArray(value)){
  //对数组执行某些操作
}
```

### 5.2.2 转换方法

如前所述，所有对象都具有 `toLocaleString()`、`toString()`和` valueOf()`方法。其中，调用数组的 `toString()`方法会返回由数组中每个值的字符串形式拼接而成的一个以逗号分隔的字符串。而调用 `valueOf()`返回的还是数组。实际上，为了创建这个字符串会调用数组每一项的`toString()`方法。由于 `alert()`要接收字符串参数，所以它会在后台调用 `toString()`方法，由此会得到与直接调用 `toString()`方法相同的结果。

```js
var colors = ["red", "blue", "green"]; // 创建一个包含 3 个字符串的数组
alert(colors.toString()); // red,blue,green
alert(colors.valueOf()); // red,blue,green
alert(colors); // red,blue,green

console.log(colors.toString()); // red,blue,green
console.log(colors.valueOf()); // (3) ["red", "blue", "green"]
console.log(colors); // (3) ["red", "blue", "green"]
```

另外， `toLocaleString()`方法经常也会返回与 `toString()`和 `valueOf()`方法相同的值，但也不总是如此。当调用数组的 `toLocaleString()`方法时，它也会创建一个数组值的以逗号分隔的字符串。而与前两个方法唯一的不同之处在于，这一次为了取得每一项的值，调用的是每一项的 `toLocaleString()`方法，而不是 `toString()`方法。

```js
var person1 = {
  toLocaleString : function () {
    return "Nikolaos";
  },
  toString : function() {
    return "Nicholas";
  }
};
var person2 = {
  toLocaleString : function () {
    return "Grigorios";
  },
  toString : function() {
    return "Greg";
  }
};
var people = [person1, person2];
alert(people); //Nicholas,Greg
alert(people.toString()); //Nicholas,Greg
alert(people.toLocaleString()); //Nikolaos,Grigorios
```

数组继承的 `toLocaleString()`、 `toString()`和 `valueOf()`方法，在默认情况下都会以逗号分隔的字符串的形式返回数组项。而如果使用 `join()`方法，则可以使用不同的分隔符来构建这个字符串。 `join()`方法只接收一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串。

```js
var colors = ["red", "green", "blue"];
alert(colors.join(",")); //red,green,blue
alert(colors.join("||")); //red||green||blue
```

如果数组中的某一项的值是 null 或者 undefined，那么该值在 `join()`、`toLocaleString()`、 `toString()`和 `valueOf()`方法返回的结果中以空字符串表示。

### 5.2.3 栈方法

栈方法有 `push()` 和 `pop()` 方法。栈是一种 LIFO（ Last-In-First-Out，后进先出）的数据结构，也就是最新添加的项最早被移除。

- `push()` 方法可以接受任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度；
- `pop()` 方法则从数组末尾移除最后一项，减少数组的length值，然后返回移除的项。

```js
var colors = new Array(); // 创建一个数组
var count = colors.push("red", "green"); // 推入两项
alert(count); //2
count = colors.push("black"); // 推入另一项
alert(count); //3

var item = colors.pop(); // 取得最后一项
alert(item); //"black"
alert(colors.length); //2
```

### 5.2.4 队列方法

队列方法有 `unshift()` 和 `shift()` 方法。队列数据结构的访问规则是 FIFO（ First-In-First-Out，先进先出）。队列在列表的末端添加项，从列表的前端移除项。

- `unshift()` 方法能在数组的前端添加任意个项并返回新数组的长度。
- `shift()` 方法能够移除数组中的第一个项并返回该项，同时将数组长度减1。

### 5.2.5 重排序方法

数组中已经存在两个可以直接用来重排序的方法： `reverse()`和 `sort()`。

默认情况下， `sort()`方法按升序排列数组项——即最小的值位于最前面，最大的值排在最后面。为了实现排序， `sort()`方法会调用每个数组项的 `toString()`转型方法，然后比较得到的字符串，以确定如何排序。即使数组中的每一项都是数值， `sort()`方法比较的也是字符串。

```js
var values = [0, 1, 5, 10, 15];
values.sort();
alert(values); //0,1,10,15,5
```

不用说，这种排序方式在很多情况下都不是最佳方案。因此 `sort()`方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面。比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回 0，如果第一个参数应该位于第二个之后则返回一个正数。

```js
function compare(value1, value2) {
  if (value1 < value2) {
    return -1;
  } else if (value1 > value2) {
    return 1;
  } else {
    return 0;
  }
}

var values = [0, 1, 5, 10, 15];
values.sort(compare);
alert(values); //0,1,5,10,15
```

对于数值类型或者其 `valueOf()`方法会返回数值类型的对象类型，可以使用一个更简单的比较函数。这个函数只要用第二个值减第一个值即可。

```JavaScript
// 降序
function compare(value1, value2){
  return value2 - value1;
}
```

### 5.2.6 操作方法

ECMAScript 为操作已经包含在数组中的项提供了很多方法。其中， `concat()`方法可以基于当前数组中的所有项创建一个新数组。具体来说，这个方法会先创建当前数组一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。在没有给 `concat()`方法传递参数的情况下，它只是复制当前数组并返回副本。如果传递给 `concat()`方法的是一或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中。如果传递的值不是数组，这些值就会被简单地添加到结果数组的末尾。

```js
var colors = ["red", "green", "blue"];
var colors2 = colors.concat("yellow", ["black", "brown"]);
alert(colors); //red,green,blue
alert(colors2); //red,green,blue,yellow,black,brown
```

下一个方法是 `slice()`，它能够基于当前数组中的一或多个项创建一个新数组。 `slice()`方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下， `slice()`方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。注意， `slice()`方法不会影响原始数组。

```js
var colors = ["red", "green", "blue", "yellow", "purple"];
var colors2 = colors.slice(1);
var colors3 = colors.slice(1,4);
alert(colors2); //green,blue,yellow,purple
alert(colors3); //green,blue,yellow
```

如果 `slice()`方法的参数中有一个负数，则用数组长度加上该数来确定相应的位置。例如，在一个包含 5 项的数组上调用 `slice(-2,-1)`与调用 `slice(3,4)`得到的结果相同。如果结束位置小于起始位置，则返回空数组。

下面我们来介绍 `splice()`方法，这个方法恐怕要算是最强大的数组方法了，它有很多种用法。`splice()`的主要用途是向数组的中部插入项，但使用这种方法的方式则有如下 3 种。

- 删除：可以删除任意数量的项，只需指定 2 个参数：要删除的第一项的位置和要删除的项数。

- 插入：可以向指定位置插入任意数量的项，只需提供 3 个参数：起始位置、0（要删除的项数）和要插入的项。如果要插入多个项，可以再传入第四、第五，以至任意多个项。

- 替换：可以向指定位置插入任意数量的项，且同时删除任意数量的项，只需指定 3 个参数：起始位置、要删除的项数和要插入的任意数量的项。插入的项数不必与删除的项数相等。

`splice()`方法始终都会返回一个数组，该数组中包含从原始数组中删除的项（如果没有删除任何项，则返回一个空数组）。

```javascript
// slice()
// 删除第一项 
var colors = ["red", "green", "blue"]; 
var removed = colors.splice(0, 1); 
alert(colors); // green,blue 
alert(removed); // red

// splice()
// 从位置 1 开始插入一项 
removed = colors.splice(1, 0, "yellow"); 
alert(colors); // green,yellow,blue 
alert(removed); // []

// splice()
// 插入一项，删除一项
removed = colors.splice(1, 1, "red"); 
alert(colors); // green,red,blue 
alert(removed); // yellow
```

### 5.2.7 位置方法

ECMAScript 5 为数组实例添加了两个位置方法： `indexOf()`和 `lastIndexOf()`。这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中， `indexOf()`方法从数组的开头（位置 0）开始向后查找， `lastIndexOf()`方法则从数组的末尾开始向前查找。这两个方法都返回要查找的项在数组中的位置，或者在没找到的情况下返回-1。在比较第一个参数与数组中的每一项时，会使用全等操作符；也就是说，要求查找的项必须严格相等（就像使用===一样）。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
alert(numbers.indexOf(4)); //3
alert(numbers.lastIndexOf(4)); //5
alert(numbers.indexOf(4, 4)); //5
alert(numbers.lastIndexOf(4, 4)); //3

var person = { name: "Nicholas" };
var people = [{ name: "Nicholas" }];
var morePeople = [person];
alert(people.indexOf(person)); //-1
alert(morePeople.indexOf(person)); //0
```

### 5.2.8 迭代方法

ECMAScript 5 为数组定义了 5 个迭代方法。每个方法都接收两个参数：要在每一项上运行的函数和（可选的）运行该函数的作用域对象——影响 this 的值。传入这些方法中的函数会接收三个参数：数组项的值、该项在数组中的位置和数组对象本身。根据使用的方法不同，这个函数执行后的返回值可能会也可能不会影响方法的返回值。

以下方法都不会修改数组中的包含的值。

- `every()`：遍历运行函数，如果该函数对每一项都返回 true，则返回 true。
- `filter()`：遍历运行函数，返回该函数会返回 true 的项组成的数组。
- `forEach()`：遍历运行函数。这个方法没有返回值。
- `map()`：遍历运行函数，返回每次函数调用的结果组成的数组。
- `some()`：遍历运行函数，如果该函数对任一项返回 true，则返回 true。

在这些方法中，最相似的是 `every()`和 `some()`，它们都用于查询数组中的项是否满足某个条件。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var everyResult = numbers.every(function(item, index, array){
  return (item > 2);
});
alert(everyResult); //false

var someResult = numbers.some(function(item, index, array){
  return (item > 2);
});
alert(someResult); //true
```

再看一看 `filter()`函数，它利用指定的函数确定是否在返回的数组中包含某一项。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var filterResult = numbers.filter(function(item, index, array){
return (item > 2);
});
alert(filterResult); //[3,4,5,4,3]
```

`map()`也返回一个数组，而这个数组的每一项都是在原始数组中的对应项上运行传入函数的结果。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
var mapResult = numbers.map(function(item, index, array){
  return item * 2;
});
alert(mapResult); //[2,4,6,8,10,8,6,4,2]
```

最后一个方法是 `forEach()`，它只是对数组中的每一项运行传入的函数。这个方法没有返回值，本质上与使用 for 循环迭代数组一样。

```js
var numbers = [1,2,3,4,5,4,3,2,1];
numbers.forEach(function(item, index, array){
  //执行某些操作
});
```

### 5.2.9 归并方法

ECMAScript 5 还新增了两个归并数组的方法： `reduce()`和 `reduceRight()`。这两个方法都会迭代数组的所有项，然后构建一个最终返回的值。其中， `reduce()`方法从数组的第一项开始，逐个遍历到最后。而 `reduceRight()`则从数组的最后一项开始，向前遍历到第一项。

这两个方法都接收两个参数：一个在每一项上调用的函数和（可选的）作为归并基础的初始值。传给 `reduce()`和 `reduceRight()`的函数接收 4 个参数：前一个值、当前值、项的索引和数组对象。这个函数返回的任何值都会作为第一个参数自动传给下一项。第一次迭代发生在数组的第二项上，因此第一个参数是数组的第一项，第二个参数就是数组的第二项。

```js
// 求数组中所有值之和
var values = [1,2,3,4,5];
var sum = values.reduce(function(prev, cur, index, array){
  return prev + cur;
});
alert(sum); //15
```

## 5.3 Date类型 

Date类型使用自UTC国际协调时间，1970年1月1日零时开始经过的毫秒数来保存时间。在使用这种数据存储格式的条件下，Date类型保存的日期能够精确到1970年1月1日之前或之后的285616.

在调用Date构造函数而不传递参数的情况下，新创建的对象自动获得当前日期和时间。如果想获得特定的日期和时间创建日期对象，必须传入表示该日期的毫秒数。

而转化日期毫秒数，有方法 `Date.parse ()` 表示接收一个表示日期的字符串参数，然后返回相应日期的毫秒数，不能表示日期的字符串则会导致返回NaN；方法 Dare.UTC () 同样也返回表示日期的毫秒数，但它的参数分别是年份、基于0的月份、月中的哪一天、小时数、分钟、秒以及毫秒数，只有前面两个参数是必须的，如果省略其它的，月中的天数为1，其它为0.同样的， Date () 也可以传递日期数，从而返回毫秒数，但是这是基于本地时区而不是GMT来创建。`Data.now()`方法，则是返回调用方法时当前时间的毫秒。

## 5.4 RegExp类型 

ECMAScript 通过 RegExp 类型来支持正则表达式。使用下面类似 Perl 的语法，就可以创建一个正则表达式。

```js
var expression = / pattern / flags ;
```

其中的模式（pattern）部分可以是任何简单或复杂的正则表达式，可以包含字符类、限定符、分组、向前查找以及反向引用。每个正则表达式都可带有一或多个标志（flags），用以标明正则表达式的行为。正则表达式的匹配模式支持下列 3 个标志。

- g：表示全局（global）模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止；
- i：表示不区分大小写（case-insensitive）模式，即在确定匹配项时忽略模式与字符串的大小写；
- m：表示多行（multiline）模式，即在到达一行文本末尾时还会继续查找下一行中是否存在与模式匹配的项。

因此，一个正则表达式就是一个模式与上述 3 个标志的组合体。不同组合产生不同结果，如下面的例子所示。

```js
/*
* 匹配字符串中所有"at"的实例
*/
var pattern1 = /at/g;

/*
* 匹配第一个"bat"或"cat"，不区分大小写
*/
var pattern2 = /[bc]at/i;

/*
* 匹配所有以"at"结尾的 3 个字符的组合，不区分大小写
*/
var pattern3 = /.at/gi;
```

与其他语言中的正则表达式类似，模式中使用的所有元字符都必须转义。正则表达式中的元字符包括：`( [ { \ ^ $ | ) ? * + . ] }`

这些元字符在正则表达式中都有一或多种特殊用途，因此如果想要匹配字符串中包含的这些字符，就必须对它们进行转义。下面给出几个例子。

```js
/*
* 匹配第一个"bat"或"cat"，不区分大小写
*/
var pattern1 = /[bc]at/i;

/*
* 匹配第一个"[bc]at"，不区分大小写
*/
var pattern2 = /\[bc\]at/i;

/*
* 匹配所有以"at"结尾的 3 个字符的组合，不区分大小写
*/
var pattern3 = /.at/gi;

/*
* 匹配所有".at"，不区分大小写
*/
var pattern4 = /\.at/gi;
```

在上面的例子中，pattern1 匹配第一个"bat"或"cat"，不区分大小写。而要想直接匹配"[bc]at"的话，就需要像定义 pattern2 一样，对其中的两个方括号进行转义。对于 pattern3 来说，句点表示位于"at"之前的任意一个可以构成匹配项的字符。但如果想匹配".at"，则必须对句点本身进行转义，如 pattern4 所示。

前面举的这些例子都是以字面量形式来定义的正则表达式。另一种创建正则表达式的方式是使用 RegExp 构造函数，它接收两个参数：一个是要匹配的字符串模式，另一个是可选的标志字符串。可以使用字面量定义的任何表达式，都可以使用构造函数来定义，如下面的例子所示。

```js
/*
* 匹配第一个"bat"或"cat"，不区分大小写
*/
var pattern1 = /[bc]at/i;

/*
* 与 pattern1 相同，只不过是使用构造函数创建的
*/
var pattern2 = new RegExp("[bc]at", "i");
```

在此， pattern1 和 pattern2 是两个完全等价的正则表达式。要注意的是，传递给 RegExp 构造函数的两个参数都是字符串（不能把正则表达式字面量传递给 RegExp 构造函数）。由于 RegExp 构造函数的模式参数是字符串，所以在某些情况下要对字符进行双重转义。所有元字符都必须双重转义，那些已经转义过的字符也是如此，例如`\n`（字符`\`在字符串中通常被转义为`\\`，而在正则表达式字符串中就会变成`\\\\`）。下表给出了一些模式，左边是这些模式的字面量形式，右边是使用 RegExp 构造函数定义相同模式时使用的字符串。

| 字面量模式 | 等价的字符串 |
|---|---|
| `/\[bc\]at/` | `\\[bc\\]at` |
| `/\.at/` | `\\.at` |
| `/name\/age/` | `name\\/age` |
| `/\d.\d{1,2}/` | `\\d.\\d{1,2}` |
| `/\w\\hello\\123/` | `\\w\\\\hello\\\\123` |

使用正则表达式字面量和使用 RegExp 构造函数创建的正则表达式不一样。在 ECMAScript 3 中，正则表达式字面量始终会共享同一个 RegExp 实例，而使用构造函数创建的每一个新 RegExp 实例都是一个新实例。来看下面的例子。

```js
var re = null,
  i;
for (i=0; i < 10; i++){
  re = /cat/g;
  re.test("catastrophe");
}
for (i=0; i < 10; i++){
  re = new RegExp("cat", "g");
  re.test("catastrophe");
}
```

在第一个循环中，即使是循环体中指定的，但实际上只为`/cat/`创建了一个 RegExp 实例。由于实例属性（下一节介绍实例属性）不会重置，所以在循环中再次调用`test()`方法会失败。这是因为第一次调用`test()`找到了"cat"，但第二次调用是从索引为 3 的字符（上一次匹配的末尾）开始的，所以就找不到它了。由于会测试到字符串末尾，所以下一次再调用 `test()`就又从开头开始了。

第二个循环使用 RegExp 构造函数在每次循环中创建正则表达式。因为每次迭代都会创建一个新的 RegExp 实例，所以每次调用`test()`都会返回 true。

ECMAScript 5 明确规定，使用正则表达式字面量必须像直接调用 RegExp 构造函数一样，每次都创建新的 RegExp 实例。 IE9+、 Firefox 4+ 和 Chrome 都据此做出了修改。

### 5.4.1 RegExp实例属性

RegExp 的每个实例都具有下列属性，通过这些属性可以取得有关模式的各种信息。

- global：布尔值，表示是否设置了 g 标志。
- ignoreCase：布尔值，表示是否设置了 i 标志。
- lastIndex：整数，表示开始搜索下一个匹配项的字符位置，从 0 算起。
- multiline：布尔值，表示是否设置了 m 标志。
- source：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回。

通过这些属性可以获知一个正则表达式的各方面信息，但却没有多大用处，因为这些信息全都包含在模式声明中。例如：

```js
var pattern1 = /\[bc\]at/i;

alert(pattern1.global); //false
alert(pattern1.ignoreCase); //true
alert(pattern1.multiline); //false
alert(pattern1.lastIndex); //0
alert(pattern1.source); //"\[bc\]at"

var pattern2 = new RegExp("\\[bc\\]at", "i");

alert(pattern2.global); //false
alert(pattern2.ignoreCase); //true
alert(pattern2.multiline); //false
alert(pattern2.lastIndex); //0
alert(pattern2.source); //"\[bc\]at"
```

我们注意到，尽管第一个模式使用的是字面量，第二个模式使用了 RegExp 构造函数，但它们的 source 属性是相同的。可见， source 属性保存的是规范形式的字符串，即字面量形式所用的字符串。

### 5.4.2 RegExp实例方法

RegExp 对象的主要方法是 `exec()`，该方法是专门为捕获组而设计的。 `exec()`接受一个参数，即要应用模式的字符串，然后返回包含第一个匹配项信息的数组；或者在没有匹配项的情况下返回 null。返回的数组虽然是 Array 的实例，但包含两个额外的属性： index 和 input。其中， index 表示匹配项在字符串中的位置，而 input 表示应用正则表达式的字符串。在数组中，第一项是与整个模式匹配的字符串，其他项是与模式中的捕获组匹配的字符串（如果模式中没有捕获组，则该数组只包含一项）。请看下面的例子。

```js
var text = "mom and dad and baby";
var pattern = /mom( and dad( and baby)?)?/gi;

var matches = pattern.exec(text);
alert(matches.index); // 0
alert(matches.input); // "mom and dad and baby"
alert(matches[0]); // "mom and dad and baby"
alert(matches[1]); // " and dad and baby"
alert(matches[2]); // " and baby"
```

这个例子中的模式包含两个捕获组。最内部的捕获组匹配"and baby"，而包含它的捕获组匹配"anddad"或者"and dad and baby"。当把字符串传入`exec()`方法中之后，发现了一个匹配项。因为整个字符串本身与模式匹配，所以返回的数组 matchs 的 index 属性值为 0。数组中的第一项是匹配的整个字符串，第二项包含与第一个捕获组匹配的内容，第三项包含与第二个捕获组匹配的内容。

对于 `exec()`方法而言，即使在模式中设置了全局标志（g），它每次也只会返回一个匹配项。在不设置全局标志的情况下，在同一个字符串上多次调用 `exec()`将始终返回第一个匹配项的信息。而在设置全局标志的情况下，每次调用 `exec()`则都会在字符串中继续查找新匹配项，如下面的例子所示。

```js
var text = "cat, bat, sat, fat";
var pattern1 = /.at/;

var matches = pattern1.exec(text);
alert(matches.index); //0
alert(matches[0]); //cat
alert(pattern1.lastIndex); //0

matches = pattern1.exec(text);
alert(matches.index); //0
alert(matches[0]); //cat
alert(pattern1.lastIndex); //0

var pattern2 = /.at/g;

var matches = pattern2.exec(text);
alert(matches.index); //0
alert(matches[0]); //cat
alert(pattern2.lastIndex); //3

matches = pattern2.exec(text);
alert(matches.index); //5
alert(matches[0]); //bat
alert(pattern2.lastIndex); //8
```

这个例子中的第一个模式 pattern1 不是全局模式，因此每次调用 `exec()`返回的都是第一个匹配项（"cat"）。而第二个模式 pattern2 是全局模式，因此每次调用 `exec()`都会返回字符串中的下一个匹配项，直至搜索到字符串末尾为止。此外，还应该注意模式的 lastIndex 属性的变化情况。在全局匹配模式下， lastIndex 的值在每次调用 `exec()`后都会增加，而在非全局模式下则始终保持不变。

> IE 的 JavaScript 实现在 lastIndex 属性上存在偏差，即使在非全局模式下，lastIndex 属性每次也会变化。

正则表达式的第二个方法是 `test()`，它接受一个字符串参数。在模式与该参数匹配的情况下返回true；否则，返回 false。在只想知道目标字符串与某个模式是否匹配，但不需要知道其文本内容的情况下，使用这个方法非常方便。因此， `test()`方法经常被用在 if 语句中，如下面的例子所示。

```js
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;
if (pattern.test(text)){
  alert("The pattern was matched.");
}
```

在这个例子中，我们使用正则表达式来测试了一个数字序列。如果输入的文本与模式匹配，则显示一条消息。这种用法经常出现在验证用户输入的情况下，因为我们只想知道输入是不是有效，至于它为什么无效就无关紧要了。

RegExp 实例继承的`toLocaleString()`和`toString()`方法都会返回正则表达式的字面量，与创建正则表达式的方式无关。例如：

```js
var pattern = new RegExp("\\[bc\\]at", "gi");
alert(pattern.toString()); // /\[bc\]at/gi
alert(pattern.toLocaleString()); // /\[bc\]at/gi
```

即使上例中的模式是通过调用 RegExp 构造函数创建的，但 `toLocaleString()`和 `toString()`方法仍然会像它是以字面量形式创建的一样显示其字符串表示。

> 正则表达式的 `valueOf()`方法返回正则表达式本身。

### 5.4.3 RegExp构造函数属性

RegExp 构造函数包含一些属性（这些属性在其他语言中被看成是静态属性）。这些属性适用于作用域中的所有正则表达式，并且基于所执行的最近一次正则表达式操作而变化。关于这些属性的另一个独特之处，就是可以通过两种方式访问它们。换句话说，这些属性分别有一个长属性名和一个短属性名（Opera 是例外，它不支持短属性名）。下表列出了 RegExp 构造函数的属性。

| 长属性名 | 短属性名 | 说 明 |
|---|---|---|
| input | $_ | 最近一次要匹配的字符串。 Opera未实现此属性 |
| lastMatch | $& | 最近一次的匹配项。 Opera未实现此属性 |
| lastParen | $+ | 最近一次匹配的捕获组。 Opera未实现此属性 |
| leftContext | $` | input字符串中lastMatch之前的文本 |
| multiline | $* | 布尔值，表示是否所有表达式都使用多行模式。 IE和Opera未实现此属性 |
| rightContext | $' | Input字符串中lastMatch之后的文本 |

使用这些属性可以从 `exec()`或 `test()`执行的操作中提取出更具体的信息。请看下面的例子。

```js
var text = "this has been a short summer";
var pattern = /(.)hort/g;

/*
* 注意： Opera 不支持 input、 lastMatch、 lastParen 和 multiline 属性
* Internet Explorer 不支持 multiline 属性
*/
if (pattern.test(text)){
  alert(RegExp.input); // this has been a short summer
  alert(RegExp.leftContext); // this has been a
  alert(RegExp.rightContext); // summer
  alert(RegExp.lastMatch); // short
  alert(RegExp.lastParen); // s
  alert(RegExp.multiline); // false
}
```

以上代码创建了一个模式，匹配任何一个字符后跟 hort，而且把第一个字符放在了一个捕获组中。RegExp 构造函数的各个属性返回了下列值：

- input 属性返回了原始字符串；
- leftContext 属性返回了单词 short 之前的字符串，而 rightContext 属性则返回了 short 之后的字符串；
- lastMatch 属性返回最近一次与整个正则表达式匹配的字符串，即 short；
- lastParen 属性返回最近一次匹配的捕获组，即例子中的 s。

如前所述，例子使用的长属性名都可以用相应的短属性名来代替。只不过，由于这些短属性名大都不是有效的 ECMAScript 标识符，因此必须通过方括号语法来访问它们，如下所示。

```js
var text = "this has been a short summer";
var pattern = /(.)hort/g;

/*
* 注意： Opera 不支持 input、 lastMatch、 lastParen 和 multiline 属性
* Internet Explorer 不支持 multiline 属性
*/
if (pattern.test(text)){
  alert(RegExp.$_); // this has been a short summer
  alert(RegExp["$`"]); // this has been a
  alert(RegExp["$'"]); // summer
  alert(RegExp["$&"]); // short
  alert(RegExp["$+"]); // s
  alert(RegExp["$*"]); // false
}
```

除了上面介绍的几个属性之外，还有多达 9 个用于存储捕获组的构造函数属性。访问这些属性的语法是 `RegExp.$1`、 `RegExp.$2`…`RegExp.$9`，分别用于存储第一、第二……第九个匹配的捕获组。在调用 `exec()`或 `test()`方法时，这些属性会被自动填充。然后，我们就可以像下面这样来使用它们。

```js
var text = "this has been a short summer";
var pattern = /(..)or(.)/g;
if (pattern.test(text)){
  alert(RegExp.$1); //sh
  alert(RegExp.$2); //t
}
```

这里创建了一个包含两个捕获组的模式，并用该模式测试了一个字符串。即使 `test()`方法只返回一个布尔值，但 RegExp 构造函数的属性 $1 和 $2 也会被匹配相应捕获组的字符串自动填充。

### 5.4.4 模式的局限性

尽管 ECMAScript 中的正则表达式功能还是比较完备的，但仍然缺少某些语言（特别是 Perl）所支持的高级正则表达式特性。下面列出了 ECMAScript 正则表达式不支持的特性（要了解更多相关信息，请访问 www.regular-expressions.info）。

- 匹配字符串开始和结尾的`\A`和`\Z`锚
- 向后查找（lookbehind）
- 并集和交集类
- 原子组（atomic grouping）
- Unicode 支持（单个字符除外，如`\uFFFF`）
- 命名的捕获组
- s（single，单行）和 x（free-spacing，无间隔）匹配模式
- 条件匹配
- 正则表达式注释

即使存在这些限制， ECMAScript 正则表达式仍然是非常强大的，能够帮我们完成绝大多数模式匹配任务。

## 5.5 Function类型　

函数实际上是对象。每个函数都是 Function 类型的实例，而且都与其他引用类型一样具有属性和方法。由于函数是对象，因此函数名实际上也是一个指向函数对象的指针，不会与某个函数绑定。函数通常是使用函数声明语法定义的。这与使用函数表达式定义函数的方式几乎相差无几。另外，还要注意函数末尾有一个分号，就像声明其他变量时一样。

```js
// 函数声明语法
function sum (num1, num2) {
  return num1 + num2;
}

// 函数表达式
var sum = function(num1, num2){
  return num1 + num2;
};
```

最后一种定义函数的方式是使用 Function 构造函数。Function 构造函数可以接收任意数量的参数，但最后一个参数始终都被看成是函数体，而前面的参数则枚举出了新函数的参数。从技术角度讲，这是一个函数表达式。但是，不推荐使用这种方法定义函数，因为这种语法会导致解析两次代码（第一次是解析常规 ECMAScript 代码，第二次是解析传入构造函数中的字符串），从而影响性能。不过，这种语法对于理解“函数是对象，函数名是指针”的概念倒是非常直观的。

```js
var sum = new Function("num1", "num2", "return num1 + num2"); // 不推荐
```

由于函数名仅仅是指向函数的指针，因此函数名与包含对象指针的其他变量没有什么不同。换句话说，一个函数可能会有多个名字。注意，使用不带圆括号的函数名是访问函数指针，而非调用函数。

```js
function sum(num1, num2){
  return num1 + num2;
}
alert(sum(10,10)); //20
var anotherSum = sum;
alert(anotherSum(10,10)); //20
sum = null;
alert(anotherSum(10,10)); //20
```

### 5.1 没有重载（深入理解）

将函数名想象为指针，也有助于理解为什么 ECMAScript 中没有函数重载的概念。

```js
function addSomeNumber(num){
  return num + 100;
}
function addSomeNumber(num) {
  return num + 200;
}
var result = addSomeNumber(100); //300
```

这个例子中声明了两个同名函数，而结果则是后面的函数覆盖了前面的函数。以上代码实际与下面的代码没有什么区别。

```js
var addSomeNumber = function (num){
  return num + 100;
};
addSomeNumber = function (num) {
  return num + 200;
};
var result = addSomeNumber(100); //300
```

### 5.2 函数声明与函数表达式

实际上，解析器在向执行环境中加载数据时，对函数声明和函数表达式并非一视同仁。解析器会率先读取函数声明，并使其在执行任何代码之前可用（可以访问）；至于函数表达式，则必须等到解析器执行到它所在的代码行，才会真正被解释执行。

```js
alert(sum(10,10));
function sum(num1, num2){
  return num1 + num2;
}
```

因为在代码开始执行之前，解析器就已经通过一个名为函数声明提升（function declaration hoisting）的过程，读取并将函数声明添加到执行环境中。对代码求值时， JavaScript 引擎在第一遍会声明函数并将它们放到源代码树的顶部。所以，即使声明函数的代码在调用它的代码后面， JavaScript 引擎也能把函数声明提升到顶部。

如果把上面的函数声明改为等价的函数表达式，就会在执行期间导致错误。原因在于函数位于一个初始化语句中，而不是一个函数声明。而且，由于第一行代码就会导致“unexpected identifier”（意外标识符）错误，实际上也不会执行到下一行。

```js
alert(sum(10,10));
var sum = function(num1, num2){
return num1 + num2;
};
```

除了什么时候可以通过变量访问函数这一点区别之外，函数声明与函数表达式的语法其实是等价的。

### 5.3 作为值的函数

因为 ECMAScript 中的函数名本身就是变量，所以函数也可以作为值来使用。也就是说，不仅可以像传递参数一样把一个函数传递给另一个函数，而且可以将一个函数作为另一个函数的结果返回。

```js
function callSomeFunction(someFunction, someArgument){
  return someFunction(someArgument);
}
```

这个函数接受两个参数。第一个参数应该是一个函数，第二个参数应该是要传递给该函数的一个值。然后，就可以像下面的例子一样传递函数了。这里的`callSomeFunction()`函数是通用的，即无论第一个参数中传递进来的是什么函数，它都会返回执行第一个参数后的结果。

```js
function add10(num){
  return num + 10;
}

var result1 = callSomeFunction(add10, 10);
alert(result1); //20

function getGreeting(name){
  return "Hello, " + name;
}
var result2 = callSomeFunction(getGreeting, "Nicholas");
alert(result2); //"Hello, Nicholas"
```

当然，可以从一个函数中返回另一个函数，而且这也是极为有用的一种技术。例如，假设有一个对象数组，我们想要根据某个对象属性对数组进行排序。而传递给数组 `sort()`方法的比较函数要接收两个参数，即要比较的值。可是，我们需要一种方式来指明按照哪个属性来排序。要解决这个问题，可以定义一个函数，它接收一个属性名，然后根据这个属性名来创建一个比较函数，下面就是这个函数的定义。

```js
// 调用 createComparisonFunction("name")方法创建了一个比较函数，
// 以便按照每个对象的 name 属性值进行排序。
function createComparisonFunction(propertyName) {
  return function(object1, object2){
    var value1 = object1[propertyName];
    var value2 = object2[propertyName];
    if (value1 < value2){
      return -1;
    } else if (value1 > value2){
      return 1;
    } else {
      return 0;
    }
  };
}

var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];

data.sort(createComparisonFunction("name"));
alert(data[0].name); //Nicholas

data.sort(createComparisonFunction("age"));
alert(data[0].name); //Zachary
```

### 5.4 函数的内部属性

在函数内部，有两个特殊的对象： arguments 和 this。其中， arguments 是一个类数组对象，包含着传入函数中的所有参数。虽然 arguments 的主要用途是保存函数参数，但这个对象还有一个名叫 callee 的属性，该属性是一个指针，指向拥有这个 arguments 对象的函数。请看下面这个非常经典的阶乘函数。使用`arguments.callee`可以让函数与函数名解耦。

```js
function factorial(num){
  if (num <= 1) {
    return 1;
  } else {
    return num * arguments.callee(num-1)
  }
}

var trueFactorial = factorial;

factorial = function(){
  return 0;
};

alert(trueFactorial(5)); //120
alert(factorial(5)); //0
```

函数内部的另一个特殊对象是 this，其行为与 Java 和 C#中的 this 大致类似。换句话说， this 引用的是函数据以执行的环境对象——或者也可以说是 this 值（当在网页的全局作用域中调用函数时，this 对象引用的就是 window）。

```js
window.color = "red";
var o = { color: "blue" };

function sayColor(){
  alert(this.color);
}

sayColor(); //"red"
o.sayColor = sayColor;
o.sayColor(); //"blue"
```

> 函数的名字仅仅是一个包含指针的变量而已。因此，即使是在不同的环境中执行，全局的 `sayColor()`函数与 `o.sayColor()`指向的仍然是同一个函数。

ECMAScript 5 也规范化了另一个函数对象的属性： caller。这个属性中保存着调用当前函数的函数的引用，如果是在全局作用域中调用当前函数，它的值为 null。为了实现更松散的耦合，也可以通过 `arguments.callee.caller`来访问相同的信息。

```js
function outer(){
  inner();
}

function inner(){
  // alert(inner.caller);
  // 相当于
  alert(arguments.callee.caller);
}

outer();
```

当函数在严格模式下运行时，访问 `arguments.callee` 会导致错误。 ECMAScript 5 还定义了`arguments.caller` 属性，但在严格模式下访问它也会导致错误，而在非严格模式下这个属性始终是undefined。定义这个属性是为了分清 `arguments.caller` 和函数的 `caller` 属性。以上变化都是为了加强这门语言的安全性，这样第三方代码就不能在相同的环境里窥视其他代码了。严格模式还有一个限制：不能为函数的 caller 属性赋值，否则会导致错误。

### 5.5.5 函数属性和方法

函数是对象，因此函数也有属性和方法，每个函数都有 length 和 prototype 两个属性。 length 表示函数希望接收的命名函数的个数， prototype 是保存所有实例方法的真正所在，诸如 `toString ()` 和 `valueOf ()` 等方法都保存在 prototype 名下，不过只是通过各自对象的实例访问。在创建自定义引用类型以及实现继承时， prototype 属性的作用是极为重要的。在 ECMAScript 5 中， prototype 属性是不可枚举的，因此使用 for-in 无法发现。

```js
function sayName(name){
  alert(name);
}
function sum(num1, num2){
  return num1 + num2;
}
function sayHi(){
  alert("hi");
}
alert(sayName.length); //1
alert(sum.length); //2
alert(sayHi.length); //0
```

每个函数一般还包含连个非继承而来的方法： `apply ()` 和 `call ()` ，这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 this 对象的值。首先 `apply ()` 方法接收两个参数：第一个是在其中运行函数的作用域，另一个是参数数组。其中，第二个参数可以是 Array 的实例，也可以是 arguments 对象。

```js
function sum(num1, num2){
  return num1 + num2;
}
function callSum1(num1, num2){
  return sum.apply(this, arguments); // 传入 arguments 对象
}
function callSum2(num1, num2){
  return sum.apply(this, [num1, num2]); // 传入数组
}
alert(callSum1(10,10)); //20
alert(callSum2(10,10)); //20
```

`call()`方法与 `apply()`方法的作用相同，它们的区别仅在于接收参数的方式不同。对于 `call()`方法而言，第一个参数是 this 值没有变化，变化的是其余参数都直接传递给函数。换句话说，在使用`call()`方法时，传递给函数的参数必须逐个列举出来。

```js
function sum(num1, num2){
  return num1 + num2;
}
function callSum(num1, num2){
  return sum.call(this, num1, num2);
}
alert(callSum(10,10)); //20
```

事实上，传递参数并非 `apply()`和 `call()`真正的用武之地；它们真正强大的地方是能够扩充函数赖以运行的作用域。使用 `call()`（或 `apply()`）来扩充作用域的最大好处，就是对象不需要与方法有任何耦合关系。

```js
window.color = "red";
var o = { color: "blue" };
function sayColor(){
  alert(this.color);
}
sayColor(); //red
sayColor.call(this); //red
sayColor.call(window); //red
sayColor.call(o); //blue
```

ECMAScript 5 还定义了一个方法： `bind()`。这个方法会创建一个函数的实例，其 this 值会被绑定到传给`bind()`函数的值。

```javascript
window.color = "red";
var o = { color: "blue" };
function sayColor(){ 
  alert(this.color ); 
}
var objectSayColor = sayColor.bind(o);
objectSayColor(); //blue
```

每个函数继承的 `toLocaleString()`和 `toString()`方法始终都返回函数的代码。返回代码的格式则因浏览器而异——有的返回的代码与源代码中的函数代码一样，而有的则返回函数代码的内部表示，即由解析器删除了注释并对某些代码作了改动后的代码。由于存在这些差异，我们无法根据这两个方法返回的结果来实现任何重要功能；不过，这些信息在调试代码时倒是很有用。另外一个继承的`valueOf()`方法同样也只返回函数代码。

## 5.6 基本包装类型

为了便于操作基本类型值，ECMAScript还提供了三个特殊的引用类型： Boolean 、 Number 和 String ，这些类型与其他应用类型相似，但同时也具有各自的基本类型相应的特殊行为。实际上，每当读取一个基本类型值的时候，后台就会创建一个对应的基本包装类型的对象，从而让我们能够调用一些方法来操作这些数据。

```js
var s1 = "some text";
var s2 = s1.substring(2);
```

在读取模式中访问字符串时，后台都会自动完成下列处理。这也分别适用于 Boolean 和 Number 类型对应的布尔值和数字值。

1. 创建 String 类型的一个实例；
2. 在实例上调用指定的方法；
3. 销毁这个实例。

```js
var s1 = new String("some text");
var s2 = s1.substring(2);
s1 = null;
```

引用类型与基本包装类型的主要区别就是对象的生存期。使用 new 操作符创建的引用类型的实例，在执行流离开当前作用域之前都一直保存在内存中。而自动创建的基本包装类型的对象，则只存在于一行代码的执行瞬间，然后立即被销毁。这意味着我们不能在运行时为基本类型值添加属性和方法。

```js
var s1 = "some text";
s1.color = "red";
alert(s1.color); //undefined
```

当然，可以显式地调用 Boolean、 Number 和 String 来创建基本包装类型的对象。不过，应该在绝对必要的情况下再这样做，因为这种做法很容易让人分不清自己是在处理基本类型还是引用类型的值。对基本包装类型的实例调用 typeof 会返回"object"，而且所有基本包装类型的对象都会被转换为布尔值 true。

Object 构造函数也会像工厂方法一样，根据传入值的类型返回相应基本包装类型的实例。

```js
var obj = new Object("some text");
alert(obj instanceof String); //true
```

要注意的是，使用 new 调用基本包装类型的构造函数，与直接调用同名的转型函数是不一样的。

```js
var value = "25";
var number = Number(value); //转型函数
alert(typeof number); //"number"
var obj = new Number(value); //构造函数
alert(typeof obj); //"object"
```

尽管我们不建议显式地创建基本包装类型的对象，但它们操作基本类型值的能力还是相当重要的。而每个基本包装类型都提供了操作相应值的便捷方法。

### 5.6.1 Boolean类型

Boolean 类型是与布尔值对应的引用类型。要创建 Boolean 对象，可以像下面这样调用 Boolean 构造函数并传入 true 或 false 值。

```js
var booleanObject = new Boolean(true);
```

Boolean 类型的实例重写了 `valueOf()`方法，返回基本类型值 true 或 false；重写了 `toString()` 方法，返回字符串"true"和"false"。可是， Boolean 对象在 ECMAScript 中的用处不大，因为它经常会造成人们的误解。其中最常见的问题就是在布尔表达式中使用 Boolean 对象。

```js
var falseObject = new Boolean(false);

var result = falseObject && true;
alert(result); //true

var falseValue = false;
result = falseValue && true;
alert(result); //false
```

基本类型与引用类型的布尔值还有两个区别。首先， typeof 操作符对基本类型返回"boolean"，而对引用类型返回"object"。其次，由于 Boolean 对象是 Boolean 类型的实例，所以使用 instanceof 操作符测试 Boolean 对象会返回 true，而测试基本类型的布尔值则返回 false。

```js
alert(typeof falseObject); //object
alert(typeof falseValue); //boolean
alert(falseObject instanceof Boolean); //true
alert(falseValue instanceof Boolean); //false
```

### 5.6.2 Number类型

Number 是与数字值对应的引用类型。要创建 Number 对象，可以在调用 Number 构造函数时向其中传递相应的数值。

```js
var numberObject = new Number(10);
```

与 Boolean 类型一样， Number 类型也重写了 `valueOf()`、 `toLocaleString()`和` toString()` 方法。重写后的 `valueOf()`方法返回对象表示的基本类型的数值，另外两个方法则返回字符串形式的数值。

```js
var num = 10;
alert(num.toString()); //"10"
alert(num.toString(2)); //"1010"
alert(num.toString(8)); //"12"
alert(num.toString(10)); //"10"
alert(num.toString(16)); //"a"
```

除了继承的方法之外， Number 类型还提供了一些用于将数值格式化为字符串的方法。其中， `toFixed()`方法会按照指定的小数位返回数值的字符串表示。如果数值本身包含的小数位比指定的还多，那么接近指定的最大小数位的值就会舍入。其中的舍入是银行家舍入:所谓银行家舍入法，其实质是一种四舍六入五取偶（又称四舍六入五留双）法。

```js
var num = 10;
alert(num.toFixed(2)); //"10.00"

var num = 10.005;
alert(num.toFixed(2)); //"10.01"
```

另外可用于格式化数值的方法是 `toExponential()`，该方法返回以指数表示法（也称 e 表示法）表示的数值的字符串形式。与 `toFixed()`一样， `toExponential()`也接收一个参数，而且该参数同样也是指定输出结果中的小数位数。

```js
var num = 10;
alert(num.toExponential(1)); //"1.0e+1"
```

对于一个数值来说， toPrecision()方法可能会返回固定大小（fixed）格式，也可能返回指数（exponential）格式；具体规则是看哪种格式最合适。这个方法接收一个参数，即表示数值的所有数字的位数（不包括指数部分）。

```js
var num = 99;
alert(num.toPrecision(1)); //"1e+2"
alert(num.toPrecision(2)); //"99"
alert(num.toPrecision(3)); //"99.0"
```

与 Boolean 对象类似， Number 对象也以后台方式为数值提供了重要的功能。但与此同时，我们仍然不建议直接实例化 Number 类型，而原因与显式创建 Boolean 对象一样。具体来讲，就是在使用typeof 和 instanceof 操作符测试基本类型数值与引用类型数值时，得到的结果完全不同。

```javascript
var numberObject = new Number(10);
var numberValue = 10;
alert(typeof numberObject); //"object"
alert(typeof numberValue); //"number"
alert(numberObject instanceof Number); //true
alert(numberValue instanceof Number); //false
```

### 5.6.3 String类型

String 类型是字符串的对象包装类型，可以像下面这样使用 String 构造函数来创建。

```js
var stringObject = new String("hello world");
```

String 对象的方法也可以在所有基本的字符串值中访问到。其中，继承的 `valueOf()`、`toLocaleString()`和 `toString()`方法，都返回对象所表示的基本字符串值。

String 类型的每个实例都有一个 length 属性，表示字符串中包含多个字符。

```js
var stringValue = "hello world";
alert(stringValue.length); //"11"
```

String 类型提供了很多方法，用于辅助完成对 ECMAScript 中字符串的解析和操作。

#### 5.6.3.1 字符方法

两个用于访问字符串中特定字符的方法是： `charAt()`和 `charCodeAt()`。这两个方法都接收一个参数，即基于 0 的字符位置。其中， `charAt()`方法以单字符字符串的形式返回给定位置的那个字符（ECMAScript 中没有字符类型），`charCodeAt()`返回字符编码。

```js
var stringValue = "hello world";
alert(stringValue.charAt(1)); //"e"

alert(stringValue.charCodeAt(1)); //输出"101"
```

ECMAScript 5 还定义了另一个访问个别字符的方法。在支持此方法的浏览器中，可以使用方括号加数字索引来访问字符串中的特定字符

```js
var stringValue = "hello world";
alert(stringValue[1]); //"e"
```

#### 5.6.3.2 字符串操作方法

第一个就是 `concat()`，用于将一或多个字符串拼接起来，返回拼接得到的新字符串。实际上， `concat()`方法可以接受任意多个参数，也就是说可以通过它拼接任意多个字符串。

```js
var stringValue = "hello ";
var result = stringValue.concat("world", "!");
alert(result); //"hello world!"
alert(stringValue); //"hello"
```

虽然 `concat()`是专门用来拼接字符串的方法，但实践中使用更多的还是加号操作符（+）。而且，使用加号操作符在大多数情况下都比使用 `concat()`方法要简便易行（特别是在拼接多个字符串的情况下）。

ECMAScript还提供了三个基于子字符串创建新字符串的方法： `slice()`、 `substr()`和 `substring()`。这三个方法都会返回被操作字符串的一个子字符串，而且也都接受一或两个参数。第一个参数指定子字符串的开始位置，第二个参数（在指定的情况下）表示子字符串到哪里结束。   
具体来说， `slice()`和`substring()`的第二个参数指定的是子字符串最后一个字符后面的位置。而 `substr()`的第二个参数指定的则是返回的字符个数。如果没有给这些方法传递第二个参数，则将字符串的长度作为结束位置。 

```js
var stringValue = "hello world";

alert(stringValue.slice(3)); //"lo world"
alert(stringValue.substring(3)); //"lo world"
alert(stringValue.substr(3)); //"lo world"

alert(stringValue.slice(3, 7)); //"lo w"
alert(stringValue.substring(3,7)); //"lo w"
alert(stringValue.substr(3, 7)); //"lo worl"
```

与`concat()`方法一样， `slice()`、 `substr()`和 `substring()`也不会修改字符串本身的值——它们只是返回一个基本类型的字符串值，对原始字符串没有任何影响。

在传递给这些方法的参数是负值的情况下，它们的行为就不尽相同了。其中， `slice()`方法会将传入的负值与字符串的长度相加， `substr()`方法将负的第一个参数加上字符串的长度，而将负的第二个参数转换为 0。最后， `substring()`方法会把所有负值参数都转换为 0。

```js
// stringValue.length: 11
var stringValue = "hello world";

alert(stringValue.slice(-3)); //"rld" 
alert(stringValue.substring(-3)); //"hello world"
alert(stringValue.substr(-3)); //"rld"

alert(stringValue.slice(3, -4)); //"lo w"
alert(stringValue.substring(3, -4)); //"hel"
alert(stringValue.substr(3, -4)); //""（空字符串）
```

- 字符串位置方法。有两个可以从字符串中查找子字符串的方法： indexOf () 和 lastIndexOf () 。这两个方法都是从一个字符串中搜索给定的字符串，然后返回子字符串的位置，没有找到则返回 -1 。区别在于，前者从字符串的开头向后搜索子字符串  ，后者从字符串的末尾向前搜索子字符串。

#### 5.6.3.3 字符串位置方法

有两个可以从字符串中查找子字符串的方法： indexOf()和 lastIndexOf()。这两个方法都是从一个字符串中搜索给定的子字符串，然后返子字符串的位置（如果没有找到该子字符串，则返回-1）。这两个方法的区别在于： indexOf()方法从字符串的开头向后搜索子字符串，而 lastIndexOf()方法是从字符串的末尾向前搜索子字符串。

```js
var stringValue = "hello world";
alert(stringValue.indexOf("o")); //4
alert(stringValue.lastIndexOf("o")); //7
```

这两个方法都可以接收可选的第二个参数，表示从字符串中的哪个位置开始搜索。换句话说，indexOf()会从该参数指定的位置向后搜索，忽略该位置之前的所有字符；而 lastIndexOf()则会从指定的位置向前搜索，忽略该位置之后的所有字符。

```js
var stringValue = "hello world";
alert(stringValue.indexOf("o", 6)); //7
alert(stringValue.lastIndexOf("o", 6)); //4
```

在使用第二个参数的情况下，可以通过循环调用 indexOf()或 lastIndexOf()来找到所有匹配的子字符串。

```js
var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";
var positions = new Array();
var pos = stringValue.indexOf("e");
while(pos > -1){
  positions.push(pos);
  pos = stringValue.indexOf("e", pos + 1);
}
alert(positions); //"3,24,32,35,52"
```

#### 5.6.3.4 trim()方法

ECMAScript 5 为所有字符串定义了 `trim()`方法。这个方法会创建一个字符串的副本，删除前置及后缀的所有空格，然后返回结果。

```js
var stringValue = " hello world ";
var trimmedStringValue = stringValue.trim();
alert(stringValue); //" hello world "
alert(trimmedStringValue); //"hello world"
```

由于 `trim()`返回的是字符串的副本，所以原始字符串中的前置及后缀空格会保持不变。

#### 5.6.3.5 字符串大小写转换方法

CMAScript 中涉及字符串大小写转换的方法有 4 个： `toLowerCase()`、 `toLocaleLowerCase()`、 `toUpperCase()`和 `toLocaleUpperCase()`。其中， `toLowerCase()`和 `toUpperCase()`是两个经典的方法，借鉴自 java.lang.String 中的同名方法。而 `toLocaleLowerCase()`和 `toLocaleUpperCase()`方法则是针对特定地区的实现。对有些地区来说，针对地区的方法与其通用方法得到的结果相同，但少数语言（如土耳其语）会为 Unicode 大小写转换应用特殊的规则，这时候就必须使用针对地区的方法来保证实现正确的转换。

```js
var stringValue = "hello world";
alert(stringValue.toLocaleUpperCase()); //"HELLO WORLD"
alert(stringValue.toUpperCase()); //"HELLO WORLD"
alert(stringValue.toLocaleLowerCase()); //"hello world"
alert(stringValue.toLowerCase()); //"hello world"
```

#### 5.6.3.6 字符串的模式匹配方法

String 类型定义了几个用于在字符串中匹配模式的方法。第一个方法就是 `match()`，在字符串上调用这个方法，本质上与调用 RegExp 的 ``exec()``方法相同。 `match()`方法只接受一个参数，要么是一个正则表达式，要么是一个 RegExp 对象。

```js
var text = "cat, bat, sat, fat";
var pattern = /.at/;
//与 pattern.exec(text)相同
var matches = text.match(pattern);
alert(matches.index); //0
alert(matches[0]); //"cat"
alert(pattern.lastIndex); //0
```

另一个用于查找模式的方法是 `search()`。这个方法的唯一参数与 `match()`方法的参数相同：由字符串或 RegExp 对象指定的一个正则表达式。 `search()`方法返回字符串中第一个匹配项的索引；如果没有找到匹配项，则返回-1。而且， `search()`方法始终是从字符串开头向后查找模式。

```js
var text = "cat, bat, sat, fat";
var pos = text.search(/at/);
alert(pos); //1
```

为了简化替换子字符串的操作， ECMAScript 提供了 `replace()`方法。这个方法接受两个参数：第一个参数可以是一个 RegExp 对象或者一个字符串（这个字符串不会被转换成正则表达式），第二个参数可以是一个字符串或者一个函数。如果第一个参数是字符串，那么只会替换第一个子字符串。要想替换所有子字符串，唯一的办法就是提供一个正则表达式，而且要指定全局（g）标志。

```js
var text = "cat, bat, sat, fat";
var result = text.replace("at", "ond");
alert(result); //"cond, bat, sat, fat"
result = text.replace(/at/g, "ond");
alert(result); //"cond, bond, sond, fond"
```

`replace()`方法的第二个参数也可以是一个函数。在只有一个匹配项（即与模式匹配的字符串）的情况下，会向这个函数传递 3 个参数：模式的匹配项、模式匹配项在字符串中的位置和原始字符串。在正则表达式中定义了多个捕获组的情况下，传递给函数的参数依次是模式的匹配项、第一个捕获组的匹配项、第二个捕获组的匹配项……，但最后两个参数仍然分别是模式的匹配项在字符串中的位置和原始字符串。这个函数应该返回一个字符串，表示应该被替换的匹配项使用函数作为 `replace()`方法的第二个参数可以实现更加精细的替换操作。

```js
function htmlEscape(text){
  return text.replace(/[<>"&]/g, function(match, pos, originalText){
    switch(match){
      case "<":
      return "&lt;";
      case ">":
      return "&gt;";
      case "&":
      return "&amp;";
      case "\"":
      return "&quot;";
    }
  });
}
alert(htmlEscape("<p class=\"greeting\">Hello world!</p>"));
//&lt;p class=&quot;greeting&quot;&gt;Hello world!&lt;/p&gt;
```

最后一个与模式匹配有关的方法是 `split()`，这个方法可以基于指定的分隔符将一个字符串分割成多个子字符串，并将结果放在一个数组中。分隔符可以是字符串，也可以是一个 RegExp 对象（这个方法不会将字符串看成正则表达式）。 `split()`方法可以接受可选的第二个参数，用于指定数组的大小，以便确保返回的数组不会超过既定大小。

```js
var colorText = "red,blue,green,yellow";
var colors1 = colorText.split(","); //["red", "blue", "green", "yellow"]
var colors2 = colorText.split(",", 2); //["red", "blue"]
var colors3 = colorText.split(/[^\,]+/); //["", ",", ",", ",", ""]
```

#### 5.6.3.7 localeCompare()方法

与操作字符串有关的最后一个方法是 `localeCompare()`，这个方法比较两个字符串，并返回下列值中的一个：
- 如果字符串在字母表中应该排在字符串参数之前，则返回一个负数（大多数情况下是-1，具体的值要视实现而定）；
- 如果字符串等于字符串参数，则返回 0；
- 如果字符串在字母表中应该排在字符串参数之后，则返回一个正数（大多数情况下是 1，具体的值同样要视实现而定）。

#### 5.6.3.8 fromCharCode()方法  

另外， String 构造函数本身还有一个静态方法： `fromCharCode()`。这个方法的任务是接收一或多个字符编码，然后将它们转换成一个字符串。从本质上来看，这个方法与实例方法 `charCodeAt()`执行的是相反的操作。

```js
alert(String.fromCharCode(104, 101, 108, 108, 111)); //"hello"
```

#### 5.6.3.9 HTML()方法  

早期的 Web 浏览器提供商觉察到了使用 JavaScript 动态格式化 HTML 的需求。于是，这些提供商就扩展了标准，实现了一些专门用于简化常见 HTML 格式化任务的方法。不过，需要请读者注意的是，应该尽量不使用这些方法，因为它们创建的标记通常无法表达语义。

## 5.7 单体内置对象　

内置对象是不依赖于宿主环境的对象，除了Object、Array和String这几个内置对象，还有两个单体内置对象：Global和Math。

Global全局对象是最特别的一个对象。不属于任何对象的属性和方法，最终都是它的属性和方法，没有全局变量或全局函数，所有在全局作用域中定义的属性和函数，都是Global对象的属性。Global 对象的 encodeURI () 和  encodeURIComponent () 方法可以对 URI（ Uniform Resource Identifiers ，通用资源标识符）进行编码，以便发送给浏览器。  URL编码方法： encodeURI () 和 encodeURIComponent () 方法可以对URI进行编码，以便发送给浏览器。解码则是 decodeURI () 和 dencodeURIcomponent () 。

eval () 方法就像是一个完整的 ECMAScript 解析器，它只接受一个参数，即要执行的 ECMAScript 字符串。在严格模式下，在外部访问不到 eval () 中创建的任何变量或函数，但是一般在 eval () 创建的任何变量或函数都不会被提升，因为在解析代码的时候，它们被包含在一个字符串中；它们只在eval()执行的时候创建。虽然没有指出如何直接访问Global对象，但Web浏览器都是将这个全局对象作为window对象的一部分加以实现的。因此，在全局作用域中声明的所有变量和函数，就都成为了window对象的属性。

ECMAScript还为保存数学公式和信息提供了一个公共位置，即Math对象。 min () 和 max () 方法用于确定一组数值中的最小值和最大值，这两个方法都可以接收任意多个数值参数。将小数值舍入为整数的几个方法： Math.ceil () 、 Math.floor () 和 Math.round() ，第一个执行向上舍入，第二个向下舍入，第三个四舍五入。 random () 方法返回大于等于0小于1的一个随机数。

## 5.8 小结　

对象在 JavaScript 中被称为引用类型的值，而且有一些内置的引用类型可以用来创建特定的对象，现简要总结如下：
+ 引用类型与传统面向对象程序设计中的类相似，但实现不同；
+ Object 是一个基础类型，其他所有类型都从 Object 继承了基本的行为；
+ Array 类型是一组值的有序列表，同时还提供了操作和转换这些值的功能；
+ Date 类型提供了有关日期和时间的信息，包括当前日期和时间以及相关的计算功能；
+ RegExp 类型是 ECMAScript 支持正则表达式的一个接口，提供了最基本的和一些高级的正则表达式功能。

函数实际上是 Function 类型的实例，因此函数也是对象；而这一点正是 JavaScript 最有特色的地方。由于函数是对象，所以函数也拥有方法，可以用来增强其行为。

因为有了基本包装类型，所以 JavaScript 中的基本类型值可以被当作对象来访问。三种基本包装类型分别是： Boolean、 Number 和 String。以下是它们共同的特征：

+ 每个包装类型都映射到同名的基本类型；
+ 在读取模式下访问基本类型值时，就会创建对应的基本包装类型的一个对象，从而方便了数据操作；
+ 操作基本类型值的语句一经执行完毕，就会立即销毁新创建的包装对象。

在所有代码执行之前，作用域中就已经存在两个内置对象： Global 和 Math。在大多数 ECMAScript 实现中都不能直接访问 Global 对象；不过， Web 浏览器实现了承担该角色的 window 对象。全局变量和函数都是 Global 对象的属性。 Math 对象提供了很多属性和方法，用于辅助完成复杂的数学计算任务

# 第 6 章 面向对象的程序设计　

面向对象（Object-Oriented， OO）的语言有一个标志，那就是他们都有类的概念，而通过类可以创建任意多个具有相同属性和方法的对象。ECMAScript 中没有类的概念，因此它的对象也与基于类的语言中的对象有所不同。

ECMA-262 把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。”严格来讲，这就相当于说对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值。正因为这样（以及其他将要讨论的原因），我们可以把 ECMAScript 的对象想象成散列表：无非就是一组名值对，其中值可以是数据或函数。

每个对象都是基于一个引用类型创建的，这个引用类型可以是第 5 章讨论的原生类型，也可以是开发人员定义的类型。

## 6.1 理解对象

创建自定义对象的最简单方式就是创建一个 Object 的实例，然后再为它添加属性和方法。

```js
var person = new Object();
person.name = "Nicholas";
person.age = 29;
person.job = "Software Engineer";

person.sayName = function () {
  alert(this.name);
};
```

早期的 JavaScript 开发人员经常使用这个模式创建新对象。几年后，对象字面量成为创建这种对象的首选模式。前面的例子用对象字面量语法可以写成这样：

```js
var person = {
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
```

这些属性在创建时都带有一些特征值（characteristic）， JavaScript 通过这些特征值来定义它们的行为。

### 6.1.1 属性类型

ECMA-262 第 5 版在定义只有内部才用的特性（attribute）时，描述了属性（property）的各种特征。ECMA-262 定义这些特性是为了实现 JavaScript 引擎用的，因此在 JavaScript 中不能直接访问它们。为了表示特性是内部值，该规范把它们放在了两对儿方括号中，例如`[[Enumerable]]`。

ECMAScript 中有两种属性：数据属性和访问器属性。

**1.数据属性**

数据属性包含一个数据值的位置，在这个位置可以读取和写入值。数据属性有 4 个描述其行为的特性：

1. `[[Configurable]]`：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
2. `[[Enumerable]]`：表示能否通过 for-in 循环返回属性。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
3. `[[Writable]]`：表示能否修改属性的值。像前面例子中那样直接在对象上定义的属性，它们的这个特性默认值为 true。
4. `[[Value]]`：包含这个属性的数据值。读取属性值的时候，从这个位置读；写入属性值的时候，把新值保存在这个位置。这个特性的默认值为 undefined。

对于像前面例子中那样直接在对象上定义的属性，它们的`[[Configurable]]`、 `[[Enumerable]]`和`[[Writable]]`特性都被设置为 true，而`[[Value]]`特性被设置为指定的值。例如：

```js
var person = {
  name: "Nicholas",
};
```

这里创建了一个名为 name 的属性，为它指定的值是"Nicholas"。也就是说，`[[Value]]`特性将被设置为"Nicholas"，而对这个值的任何修改都将反映在这个位置。

要修改属性默认的特性，必须使用 ECMAScript 5 的 `Object.defineProperty()` 方法，该方法接收三个参数：属性所在的对象、属性的名字和一个描述符对象。其中，描述符（descriptor）对象的属性必须是： configurable、 enumerable、 writable 和 value。设置其中的一或多个值，可以修改对应的特性值。

```js
var person = {};
Object.defineProperty(person, "name", {
  writable: false,
  value: "Nicholas",
});

alert(person.name); //"Nicholas"
person.name = "Greg";
alert(person.name); //"Nicholas"
```

这个例子创建了一个名为 name 的属性，它的值"Nicholas"是只读的。这个属性的值是不可修改的，如果尝试为它指定新值，则在非严格模式下，赋值操作将被忽略；在严格模式下，赋值操作将会导致抛出错误。

类似的规则也适用于不可配置的属性。例如：

```js
var person = {};
Object.defineProperty(person, "name", {
  configurable: false,
  value: "Nicholas",
});
alert(person.name); //"Nicholas"
delete person.name;
alert(person.name); //"Nicholas"
```

把 configurable 设置为 false，表示不能从对象中删除属性。如果对这个属性调用 delete，则在非严格模式下什么也不会发生，而在严格模式下会导致错误。而且，一旦把属性定义为不可配置的，就不能再把它变回可配置了。此时，再调用 `Object.defineProperty()`方法修改除 writable 之外的特性，都会导致错误：

```js
var person = {};
Object.defineProperty(person, "name", {
  configurable: false,
  value: "Nicholas",
});
//抛出错误
Object.defineProperty(person, "name", {
  configurable: true,
  value: "Nicholas",
});
```

也就是说，可以多次调用 `Object.defineProperty()` 方法修改同一个属性，但在把 `[[configurable]]` 特性设置为 false 之后就会有限制了。

在调用 `Object.defineProperty()`方法时，如果不指定，`[[configurable]]`、`[[enumerable]]` 和 `[[writable]]` 特性的默认值都是 false。多数情况下，可能都没有必要利用 `Object.defineProperty()`方法提供的这些高级功能。不过，理解这些概念对理解 JavaScript 对象却非常有用。

> IE8 是第一个实现 `Object.defineProperty()` 方法的浏览器版本。然而，这个版本的实现存在诸多限制：只能在 DOM 对象上使用这个方法，而且只能创建访问器属性。由于实现不彻底，建议读者不要在 IE8 中使用 `Object.defineProperty()` 方法。

**2.访问器属性**

访问器属性不包含数据值：它们包含一对儿 getter 和 setter 函数，不过他们都不是必需的。在读取访问器属性时，会调用 getter 函数，这个函数负责返回有效的值；在写入访问器属性时，会调用 setter 函数并传入新值，这个函数负责决定如何处理数据。访问器属性有如下 4 个特性。

1. `[[Configurable]]`：表示能否通过 delete 删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为数据属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
2. `[[Enumerable]]`：表示能否通过 for-in 循环返回属性。对于直接在对象上定义的属性，这个特性的默认值为 true。
3. `[[Get]]`：在读取属性时调用的函数。默认值为 undefined。
4. `[[Set]]`：在写入属性时调用的函数。默认值为 undefine

访问器属性不能直接定义，必须使用 `Object.defineProperty()` 来定义。

```js
var book = {
  _year: 2004,
  edition: 1,
};
Object.defineProperty(book, "year", {
  get: function () {
    return this._year;
  },
  set: function (newValue) {
    if (newValue > 2004) {
      this._year = newValue;
      this.edition += newValue - 2004;
    }
  },
});
book.year = 2005;
alert(book.edition); //2
```

这是使用访问器属性的常见方式，即设置一个属性的值会导致其他属性发生变化。

不一定非要同时指定 getter 和 setter。只指定 getter 意味着属性是不能写，尝试写入属性会被忽略。在严格模式下，尝试写入只指定了 getter 函数的属性会抛出错误。类似地，只指定 setter 函数的属性也不能读，否则在非严格模式下会返回 undefined，而在严格模式下会抛出错误。

支持 ECMAScript 5 的这个方法的浏览器有 IE9+（IE8 只是部分实现）、 Firefox 4+、 Safari 5+、 Opera 12+ 和 Chrome 。在这个方法之前，要创建访问器属性，一般都使用两个非标准的方法 ：`__defineGetter__()`和`__defineSetter__()`。这两个方法最初是由 Firefox 引入的，后来 Safari 3、 Chrome 1 和 Opera 9.5 也给出了相同的实现。使用这两个遗留的方法，可以像下面这样重写前面的例子。

```js
var book = {
  _year: 2004,
  edition: 1,
};

//定义访问器的旧有方法
book.__defineGetter__("year", function () {
  return this._year;
});
book.__defineSetter__("year", function (newValue) {
  if (newValue > 2004) {
    this._year = newValue;
    this.edition += newValue - 2004;
  }
});

book.year = 2005;
alert(book.edition); //2
```

在不支持`Object.defineProperty()`方法的浏览器中不能修改`[[Configurable]]`和`[[Enumerable]]`。

### 6.1.2 定义多个属性

由于为对象定义多个属性的可能性很大， ECMAScript 5 又定义了一个`Object.defineProperties()`方法。利用这个方法可以通过描述符一次定义多个属性。这个方法接收两个对象参数：第一个对象是要添加和修改其属性的对象，第二个对象的属性与第一个对象中要添加或修改的属性一一对应。

```js
var book = {};
Object.defineProperties(book, {
  _year: {
    value: 2004,
  },
  edition: {
    value: 1,
  },
  year: {
    get: function () {
      return this._year;
    },
    set: function (newValue) {
      if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004;
      }
    },
  },
});
```

以上代码在 book 对象上定义了两个数据属性（`_year` 和 edition）和一个访问器属性（year）。最终的对象与上一节中定义的对象相同。唯一的区别是这里的属性都是在同一时间创建的。

### 6.1.3 读取属性的特性

使用 ECMAScript 5 的 `Object.getOwnPropertyDescriptor()` 方法，可以取得给定属性的描述符。这个方法接收两个参数：属性所在的对象和要读取其描述符的属性名称。返回值是一个对象，如果是访问器属性，这个对象的属性有 configurable、 enumerable、 get 和 set；如果是数据属性，这个对象的属性有 configurable、 enumerable、 writable 和 value。

```js
var book = {};
Object.defineProperties(book, {
  _year: {
    value: 2004,
  },
  edition: {
    value: 1,
  },
  year: {
    get: function () {
      return this._year;
    },
    set: function (newValue) {
      if (newValue > 2004) {
        this._year = newValue;
        this.edition += newValue - 2004;
      }
    },
  },
});
var descriptor = Object.getOwnPropertyDescriptor(book, "_year");
alert(descriptor.value); //2004
alert(descriptor.configurable); //false
alert(typeof descriptor.get); //"undefined"

var descriptor = Object.getOwnPropertyDescriptor(book, "year");
alert(descriptor.value); //undefined
alert(descriptor.enumerable); //false
alert(typeof descriptor.get); //"function"
```

## 6.2 创建对象

虽然 Object 构造函数或对象字面量都可以用来创建单个对象，但这些方式有个明显的缺点：使用同一个接口创建很多对象，会产生大量的重复代码。为解决这个问题，人们开始使用工厂模式的一种变体。

### 6.2.1 工厂模式

工厂模式是软件工程领域一种广为人知的设计模式，这种模式抽象了创建具体对象的过程。考虑到在 ECMAScript 中无法创建类，开发人员就发明了一种函数，用函数来封装以特定接口创建对象的细节，如下面的例子所示。

```js
function createPerson(name, age, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function () {
    alert(this.name);
  };
  return o;
}

var person1 = createPerson("Nicholas", 29, "Software Engineer");
var person2 = createPerson("Greg", 27, "Doctor");
```

函数`createPerson()`能够根据接受的参数来构建一个包含所有必要信息的 Person 对象。可以无数次地调用这个函数，而每次它都会返回一个包含三个属性一个方法的对象。工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别的问题（即怎样知道一个对象的类型）。随着 JavaScript 的发展，又一个新模式出现了。

### 6.2.2 构造函数模式

ECMAScript 中的构造函数可用来创建特定类型的对象。像 Object 和 Array 这样的原生构造函数，在运行时会自动出现在执行环境中。此外，也可以创建自定义的构造函数，从而定义自定义对象类型的属性和方法。例如，可以使用构造函数模式将前面的例子重写如下。

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = function () {
    alert(this.name);
  };
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

在这个例子中，`Person()`函数取代了 `createPerson()`函数。我们注意到，`Person()`中的代码除了与 `createPerson()`中相同的部分外，还存在以下不同之处：

- 没有显式地创建对象；
- 直接将属性和方法赋给了 this 对象；
- 没有 return 语句。

此外，还应该注意到函数名 Person 使用的是大写字母 P。按照惯例，构造函数始终都应该以一个大写字母开头，而非构造函数则应该以一个小写字母开头。这个做法借鉴自其他 OO 语言，主要是为了区别于 ECMAScript 中的其他函数；因为构造函数本身也是函数，只不过可以用来创建对象而已。

要创建 Person 的新实例，必须使用 new 操作符。以这种方式调用构造函数实际上会经历以下 4 个步骤：

1. 创建一个新对象；
2. 分派构造函数中的 this 给新对象（因此 this 就指向了这个新对象）；
3. 执行构造函数中的代码（为这个新对象添加属性）；
4. 返回新对象。

在前面例子的最后， person1 和 person2 分别保存着 Person 的一个不同的实例。这两个对象都有一个 `constructor`（构造函数）属性，该属性指向 Person 。对象的 `constructor` 属性最初是用来标识对象类型的。但是，提到检测对象类型，还是 instanceof 操作符要更可靠一些。

```js
alert(person1.constructor == Person); //true
alert(person2.constructor == Person); //true

alert(person1 instanceof Object); //true
alert(person1 instanceof Person); //true
alert(person2 instanceof Object); //true
alert(person2 instanceof Person); //true
```

创建自定义的构造函数意味着将来可以将它的实例标识为一种特定的类型；而这正是构造函数模式胜过工厂模式的地方。

**1. 将构造函数当作函数**

构造函数与其他函数的唯一区别，就在于调用它们的方式不同。不过，构造函数毕竟也是函数，不存在定义构造函数的特殊语法。任何函数，只要通过 new 操作符来调用，那它就可以作为构造函数；而任何函数，如果不通过 new 操作符来调用，那它跟普通函数也不会有什么两样。例如，前面例子中定义的`Person()`函数可以通过下列任何一种方式来调用。

```js
// 当作构造函数使用
var person = new Person("Nicholas", 29, "Software Engineer");
person.sayName(); //"Nicholas"

// 作为普通函数调用
Person("Greg", 27, "Doctor"); // 添加到 window
window.sayName(); //"Greg"

// 在另一个对象的作用域中调用
var o = new Object();
Person.call(o, "Kristen", 25, "Nurse");
o.sayName(); //"Kristen"
```

**2. 构造函数的问题**

使用构造函数的主要问题，就是每个方法都要在每个实例上重新创建一遍。在前面的例子中， person1 和 person2 都有一个名为`sayName()`的方法，但那两个方法不是同一个 Function 的实例。不要忘了——ECMAScript 中的函数是对象，因此每定义一个函数，也就是实例化了一个对象。从逻辑角度讲，此时的构造函数也可以这样定义。

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = new Function("alert(this.name)"); // 与声明函数在逻辑上是等价的
}
```

从这个角度上来看构造函数，更容易明白每个 Person 实例都包含一个不同的 Function 实例（以显示 name 属性）的本质。说明白些，以这种方式创建函数，会导致不同的作用域链和标识符解析，但创建 Function 新实例的机制仍然是相同的。因此，不同实例上的同名函数是不相等的，以下代码可以证明这一点。

```js
alert(person1.sayName == person2.sayName); //false
```

然而，创建两个完成同样任务的 Function 实例的确没有必要；况且有 this 对象在，根本不用在执行代码前就把函数绑定到特定对象上面。因此，大可像下面这样，通过把函数定义转移到构造函数外部来解决这个问题。

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.sayName = sayName;
}
function sayName() {
  alert(this.name);
}
var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");
```

在这个例子中，我们把`sayName()`函数的定义转移到了构造函数外部。而在构造函数内部，我们将 sayName 属性设置成等于全局的 sayName 函数。这样一来，由于 sayName 包含的是一个指向函数的指针，因此 person1 和 person2 对象就共享了在全局作用域中定义的同一个`sayName()`函数。这样做确实解决了两个函数做同一件事的问题，可是新问题又来了：在全局作用域中定义的函数实际上只能被某个对象调用，这让全局作用域有点名不副实。而更让人无法接受的是：如果对象需要定义很多方法，那么就要定义很多个全局函数，于是我们这个自定义的引用类型就丝毫没有封装性可言了。好在，这些问题可以通过使用原型模式来解决。

### 6.2.3 原型模式

我们创建的每个函数都有一个 prototype（原型）属性，这个属性是一个指针，指向一个对象，而这个对象的用途是包含可以由特定类型的所有实例共享的属性和方法。如果按照字面意思来理解，那么 prototype 就是通过调用构造函数而创建的那个对象实例的原型对象。使用原型对象的好处是可以让所有对象实例共享它所包含的属性和方法。换句话说，不必在构造函数中定义对象实例的信息，而是可以将这些信息直接添加到原型对象中，如下面的例子所示。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};

var person1 = new Person();
person1.sayName(); //"Nicholas"

var person2 = new Person();
person2.sayName(); //"Nicholas"

alert(person1.sayName == person2.sayName); //true
```

即使如此，也仍然可以通过调用构造函数来创建新对象，而且新对象还会具有相同的属性和方法。但与构造函数模式不同的是，新对象的这些属性和方法是由所有实例共享的。换句话说，person1 和 person2 访问的都是同一组属性和同一个`sayName()`函数。要理解原型模式的工作原理，必须先理解 ECMAScript 中原型对象的性质。

**1.理解原型对象**

无论什么时候，只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个 prototype 属性，这个属性指向函数的原型对象。在默认情况下，所有原型对象都会自动获得一个 constructor （构造函数）属性，这个属性包含一个指向 prototype 属性所在函数的指针。就拿前面的例子来说，`Person.prototype.constructor` 指向 Person。而通过这个构造函数，我们还可继续为原型对象添加其他属性和方法。

创建了自定义的构造函数之后，其原型对象默认只会取得 constructor 属性；至于其他方法，则都是从 Object 继承而来的。当调用构造函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象。 ECMA-262 第 5 版中管这个指针叫`[[Prototype]]`。虽然在脚本中没有标准的方式访问`[[Prototype]]`，但 Firefox、 Safari 和 Chrome 在每个对象上都支持一个属性`__proto__`；而在其他实现中，这个属性对脚本则是完全不可见的。不过，要明确的真正重要的一点就是，这个连接存在于实例与构造函数的原型对象之间，而不是存在于实例与构造函数之间。

图 6-1 展示了 Person 构造函数、 Person 的原型属性以及 Person 现有的两个实例之间的关系。在此，`Person.prototype`指向了原型对象，而 `Person.prototype.constructor` 又指回了 Person。原型对象中除了包含 constructor 属性之外，还包括后来添加的其他属性。 Person 的每个实例——person1 和 person2 都包含一个内部属性，该属性仅仅指向了 `Person.prototype`；换句话说，它们与构造函数没有直接的关系。此外，要格外注意的是，虽然这两个实例都不包含属性和方法，但我们却可以调用`person1.sayName()`。这是通过查找对象属性的过程来实现的。

虽然在所有实现中都无法访问到`[[Prototype]]`，但是可以通过 `isPrototypeOf()` 方法来确定对象之间是否存在这种关系，从本质上讲，如果`[[Prototype]]`指向调用`isPrototypeOf()`方法的对象`Person.prototype`，那么这个方法就返回 true。

```js
alert(Person.prototype.isPrototypeOf(person1)); //true
alert(Person.prototype.isPrototypeOf(person2)); //true
```

ECMAScript 5 增加了一个新方法，叫 `Object.getPrototypeOf()`，在所有支持的实现中，这个方法返回`[[Prototype]]`的值。返回的对象实际就是这个对象的原型。

```js
alert(Object.getPrototypeOf(person1) == Person.prototype); //true
alert(Object.getPrototypeOf(person1).name); //"Nicholas"
```

每当代码读取某个对象的某个属性时，都会执行一次搜索，目标是具有给定名字的属性。搜索首先从对象实例本身开始。如果在实例中找到了具有给定名字的属性，则返回该属性的值；如果没有找到，则继续搜索指针指向的原型对象，在原型对象中查找具有给定名字的属性。如果在原型对象中找到了这个属性，则返回该属性的值。也就是说，在我们调用 `person1.sayName()`的时候，会先后执行两次搜索。首先，解析器会问：“实例 person1 有 sayName 属性吗？”答：“没有。”然后，它继续搜索，再问：“person1 的原型有 sayName 属性吗？”答：“有。”于是，它就读取那个保存在原型对象中的函数。当我们调用 `person2.sayName()`时，将会重现相同的搜索过程，得到相同的结果。而这正是多个对象实例共享原型所保存的属性和方法的基本原理。

> 前面提到过，原型最初只包含 constructor 属性，而该属性也是共享的，因此可以通过对象实例访问。

虽然可以通过对象实例访问保存在原型中的值，但却不能通过对象实例重写原型中的值。当为对象实例添加一个属性时，这个属性就会屏蔽原型对象中保存的同名属性。换句话说，添加这个属性只会阻止我们访问原型中的那个属性，但不会修改那个属性。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();

person1.name = "Greg";
alert(person1.name); //"Greg"—— 来自实例
alert(person2.name); //"Nicholas"—— 来自原型
```

即使将这个同名属性设置为 null，也只会在实例中设置这个属性，而不会恢复其指向原型的连接。不过，使用 delete 操作符则可以完全删除实例属性，从而让我们能够重新访问原型中的属性。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();

person1.name = "Greg";
alert(person1.name); //"Greg"—— 来自实例
alert(person2.name); //"Nicholas"—— 来自原型

delete person1.name;
alert(person1.name); //"Nicholas"—— 来自原型
```

使用`hasOwnProperty()`方法可以检测一个属性是存在于实例中，还是存在于原型中。这个方法（不要忘了它是从 Object 继承来的）只在给定属性存在于对象实例中时，才会返回 true。来看下面这个例子。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();

alert(person1.hasOwnProperty("name")); //false

person1.name = "Greg";
alert(person1.name); //"Greg"—— 来自实例
alert(person1.hasOwnProperty("name")); //true

alert(person2.name); //"Nicholas"—— 来自原型
alert(person2.hasOwnProperty("name")); //false

delete person1.name;
alert(person1.name); //"Nicholas"—— 来自原型
alert(person1.hasOwnProperty("name")); //false
```

通过使用`hasOwnProperty()`方法，什么时候访问的是实例属性，什么时候访问的是原型属性就一清二楚了。

> ECMAScript 5 的`Object.getOwnPropertyDescriptor()`方法只能用于实例属性，要取得原型属性的描述符，必须直接在原型对象上调用`Object.getOwnPropertyDescriptor()`方法。

**2.原型与 in 操作符**

有两种方式使用 in 操作符：单独使用和在 for-in 循环中使用。在单独使用时， in 操作符会在通过对象能够访问给定属性时返回 true，无论该属性存在于实例中还是原型中。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};
var person1 = new Person();
var person2 = new Person();

alert(person1.hasOwnProperty("name")); //false
alert("name" in person1); //true

person1.name = "Greg";
alert(person1.name); //"Greg" —— 来自实例
alert(person1.hasOwnProperty("name")); //true
alert("name" in person1); //true

alert(person2.name); //"Nicholas" —— 来自原型
alert(person2.hasOwnProperty("name")); //false
alert("name" in person2); //true

delete person1.name;
alert(person1.name); //"Nicholas" —— 来自原型
alert(person1.hasOwnProperty("name")); //false
alert("name" in person1); //true
```

以上代码执行的整个过程中， name 属性要么是直接在对象上访问到的，要么是通过原型访问到的。因此，调用 `"name" in person1` 始终都返回 true，无论该属性存在于实例中还是存在于原型中。同时使用 `hasOwnProperty()`方法和 in 操作符，就可以确定该属性到底是存在于对象中，还是存在于原型中，如下所示。

```js
function hasPrototypeProperty(object, name) {
  return !object.hasOwnProperty(name) && name in object;
}
```

由于 in 操作符只要通过对象能够访问到属性就返回 true，`hasOwnProperty()`只在属性存在于实例中时才返回 true，因此只要 in 操作符返回 true 而`hasOwnProperty()`返回 false，就可以确定属性是原型中的属性。下面来看一看上面定义的函数`hasPrototypeProperty()`的用法。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};

var person = new Person();
alert(hasPrototypeProperty(person, "name")); //true

person.name = "Greg";
alert(hasPrototypeProperty(person, "name")); //false
```

在使用 for-in 循环时，返回的是所有能够通过对象访问的、可枚举的（enumerated）属性，其中既包括存在于实例中的属性，也包括存在于原型中的属性。屏蔽了原型中不可枚举属性（即将`[[Enumerable]]`标记为 false 的属性）的实例属性也会在 for-in 循环中返回，因为根据规定，所有开发人员定义的属性都是可枚举的——只有在 IE8 及更早版本中例外。

IE 早期版本的实现中存在一个 bug，即屏蔽不可枚举属性的实例属性不会出现在 for-in 循环中。

要取得对象上所有可枚举的实例属性，可以使用 ECMAScript 5 的 `Object.keys()`方法。这个方法接收一个对象作为参数，返回一个包含所有可枚举属性的字符串数组。

```js
function Person() {}
Person.prototype.name = "Nicholas";
Person.prototype.age = 29;
Person.prototype.job = "Software Engineer";
Person.prototype.sayName = function () {
  alert(this.name);
};

var keys = Object.keys(Person.prototype);
alert(keys); //"name,age,job,sayName"

var p1 = new Person();
p1.name = "Rob";
p1.age = 31;
var p1keys = Object.keys(p1);
alert(p1keys); //"name,age"
```

如果你想要得到所有实例属性，无论它是否可枚举，都可以使用 `Object.getOwnPropertyNames()`方法。注意结果中包含了不可枚举的 constructor 属性。`Object.keys()`和 `Object.getOwnPropertyNames()`方法都可以用来替代 for-in 循环。

```js
var keys = Object.getOwnPropertyNames(Person.prototype);
alert(keys); //"constructor,name,age,job,sayName"
```

**3.更简单的原型语法**

前面例子中每添加一个属性和方法就要敲一遍`Person.prototype`。为减少不必要的输入，也为了从视觉上更好地封装原型的功能，更常见的做法是用一个包含所有属性和方法的对象字面量来重写整个原型对象，如下面的例子所示。

```js
function Person() {}
Person.prototype = {
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
```

在上面的代码中，我们将 `Person.prototype` 设置为等于一个以对象字面量形式创建的新对象。最终结果相同，但有一个例外： constructor 属性不再指向 Person 了。前面曾经介绍过，每创建一个函数，就会同时创建它的 prototype 对象，这个对象也会自动获得 constructor 属性。而我们在这里使用的语法，本质上完全重写了默认的 prototype 对象，因此 constructor 属性也就变成了新对象的 constructor 属性（指向 Object 构造函数），不再指向 Person 函数。此时，尽管 instanceof 操作符还能返回正确的结果，但通过 constructor 已经无法确定对象的类型了。

```js
var friend = new Person();

alert(friend instanceof Object); //true
alert(friend instanceof Person); //true
alert(friend.constructor == Person); //false
alert(friend.constructor == Object); //true
```

在此，用 instanceof 操作符测试 Object 和 Person 仍然返回 true，但 constructor 属性则等于 Object 而不等于 Person 了。如果 constructor 的值真的很重要，可以像下面这样特意将它设置回适当的值。

```js
function Person() {}
Person.prototype = {
  constructor: Person,
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
```

注意，以这种方式重设 constructor 属性会导致它的`[[Enumerable]]`特性被设置为 true。默认情况下，原生的 constructor 属性是不可枚举的。因此如果你使用兼容 ECMAScript 5 的 JavaScript 引擎，可以试一试 `Object.defineProperty()`。

```js
function Person() {}
Person.prototype = {
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
//重设构造函数，只适用于 ECMAScript 5 兼容的浏览器
Object.defineProperty(Person.prototype, "constructor", {
  enumerable: false,
  value: Person,
});
```

**4.原型的动态性**

由于在原型中查找值的过程是一次搜索，因此我们对原型对象所做的任何修改都能够立即从实例上反映出来——即使是先创建了实例后修改原型也照样如此。请看下面的例子。

```js
var friend = new Person();
Person.prototype.sayHi = function () {
  alert("hi");
};
friend.sayHi(); //"hi"（没有问题！）
```

即使 person 实例是在添加新方法之前创建的，但它仍然可以访问这个新方法。其原因可以归结为实例与原型之间的松散连接关系。当我们调用`person.sayHi()`时，首先会在实例中搜索名为 sayHi 的属性，在没找到的情况下，会继续搜索原型。因为实例与原型之间的连接只不过是一个指针，而非一个副本，因此就可以在原型中找到新的 sayHi 属性并返回保存在那里的函数。

尽管可以随时为原型添加属性和方法，并且修改能够立即在所有对象实例中反映出来，但如果是重写整个原型对象，那么情况就不一样了。我们知道，调用构造函数时会为实例添加一个指向最初原型的`[[Prototype]]`指针，而把原型修改为另外一个对象就等于切断了构造函数与最初原型之间的联系。请记住：实例中的指针仅指向原型，而不指向构造函数。

```js
function Person() {}
var friend = new Person();
Person.prototype = {
  constructor: Person,
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  sayName: function () {
    alert(this.name);
  },
};
friend.sayName(); //error
```

重写原型对象切断了现有原型与任何之前已经存在的对象实例之间的联系；它们引用的仍然是最初的原型。

**5.原生对象的原型**

原型模式的重要性不仅体现在创建自定义类型方面，就连所有原生的引用类型，都是采用这种模式创建的。所有原生引用类型（Object、 Array、 String，等等）都在其构造函数的原型上定义了方法。例如，在 `Array.prototype` 中可以找到`sort()`方法，而在 `String.prototype` 中可以找到`substring()`方法，如下所示。

```js
alert(typeof Array.prototype.sort); //"function"
alert(typeof String.prototype.substring); //"function"
```

通过原生对象的原型，不仅可以取得所有默认方法的引用，而且也可以定义新方法。可以像修改自定义对象的原型一样修改原生对象的原型，因此可以随时添加方法。下面的代码就给基本包装类型 String 添加了一个名为`startsWith()`的方法。

```js
String.prototype.startsWith = function (text) {
  return this.indexOf(text) == 0;
};
var msg = "Hello world!";
alert(msg.startsWith("Hello")); //true
```

由于 msg 是字符串，而且后台会调用 String 基本包装函数创建这个字符串，因此通过 msg 就可以调用`startsWith()`方法。

> 尽管可以这样做，但我们不推荐在产品化的程序中修改原生对象的原型。如果因某个实现中缺少某个方法，就在原生对象的原型中添加这个方法，那么当在另一个支持该方法的实现中运行代码时，就可能会导致命名冲突。而且，这样做也可能会意外地重写原生方法。

**6.原型对象的问题**

原型模式也不是没有缺点。首先，它省略了为构造函数传递初始化参数这一环节，结果所有实例在默认情况下都将取得相同的属性值。虽然这会在某种程度上带来一些不方便，但还不是原型的最大问题。原型模式的最大问题是由其共享的本性所导致的。

原型中所有属性是被很多实例共享的，这种共享对于函数非常合适。对于那些包含基本值的属性倒也说得过去，毕竟（如前面的例子所示），通过在实例上添加一个同名属性，可以隐藏原型中的对应属性。然而，对于包含引用类型值的属性来说，问题就比较突出了。

```js
function Person() {}
Person.prototype = {
  constructor: Person,
  name: "Nicholas",
  age: 29,
  job: "Software Engineer",
  friends: ["Shelby", "Court"],
  sayName: function () {
    alert(this.name);
  },
};

var person1 = new Person();
var person2 = new Person();

person1.friends.push("Van");

alert(person1.friends); //"Shelby,Court,Van"
alert(person2.friends); //"Shelby,Court,Van"
alert(person1.friends === person2.friends); //true
```

由于 friends 数组存在于`Person.prototype` 而非 person1 中，所以刚刚提到的修改也会通过`person2.friends`（与 `person1.friends` 指向同一个数组）反映出来。假如我们的初衷就是像这样在所有实例中共享一个数组，那么对这个结果我没有话可说。可是，实例一般都是要有属于自己的全部属性的。而这个问题正是我们很少看到有人单独使用原型模式的原因所在。

### 6.2.4 组合使用构造函数模式和原型模式

创建自定义类型的最常见方式，就是组合使用构造函数模式与原型模式。构造函数模式用于定义实例属性，而原型模式用于定义方法和共享的属性。结果，每个实例都会有自己的一份实例属性的副本，但同时又共享着对方法的引用，最大限度地节省了内存。另外，这种混成模式还支持向构造函数传递参数；可谓是集两种模式之长。

```js
function Person(name, age, job) {
  this.name = name;
  this.age = age;
  this.job = job;
  this.friends = ["Shelby", "Court"];
}

Person.prototype = {
  constructor: Person,
  sayName: function () {
    alert(this.name);
  },
};

var person1 = new Person("Nicholas", 29, "Software Engineer");
var person2 = new Person("Greg", 27, "Doctor");

person1.friends.push("Van");

alert(person1.friends); //"Shelby,Court,Van"
alert(person2.friends); //"Shelby,Court"
alert(person1.friends === person2.friends); //false
alert(person1.sayName === person2.sayName); //true
```

这种构造函数与原型混成的模式，是目前在 ECMAScript 中使用最广泛、认同度最高的一种创建自定义类型的方法。可以说，这是用来定义引用类型的一种默认模式。

### 6.2.5 动态原型模式

有其他 OO 语言经验的开发人员在看到独立的构造函数和原型时，很可能会感到非常困惑。动态原型模式正是致力于解决这个问题的一个方案，它把所有信息都封装在了构造函数中，而通过在构造函数中初始化原型（仅在必要的情况下），又保持了同时使用构造函数和原型的优点。换句话说，可以通过检查某个应该存在的方法是否有效，来决定是否需要初始化原型。

```js
function Person(name, age, job) {
  //properties
  this.name = name;
  this.age = age;
  this.job = job;

  //methods
  if (typeof this.sayName != "function") {
    Person.prototype.sayName = function () {
      alert(this.name);
    };
  }
}

var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName();
```

这里只在`sayName()`方法不存在的情况下，才会将它添加到原型中。这段代码只会在初次调用构造函数时才会执行。此后，原型已经完成初始化，不需要再做什么修改了。不过要记住，这里对原型所做的修改，能够立即在所有实例中得到反映。因此，这种方法确实可以说非常完美。其中， if 语句检查的可以是初始化之后应该存在的任何属性或方法——不必用一大堆 if 语句检查每个属性和每个方法；只要检查其中一个即可。对于采用这种模式创建的对象，还可以使用 instanceof 操作符确定它的类型。

> 使用动态原型模式时，不能使用对象字面量重写原型。前面已经解释过了，如果在已经创建了实例的情况下重写原型，那么就会切断现有实例与新原型之间的联系。

### 6.2.6 寄生构造函数模式

通常，在前述的几种模式都不适用的情况下，可以使用寄生（parasitic）构造函数模式。这种模式的基本思想是创建一个函数，该函数的作用仅仅是封装创建对象的代码，然后再返回新创建的对象；但从表面上看，这个函数又很像是典型的构造函数。

```js
function Person(name, age, job) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.job = job;
  o.sayName = function () {
    alert(this.name);
  };
  return o;
}

var friend = new Person("Nicholas", 29, "Software Engineer");
friend.sayName(); //"Nicholas"
```

除了使用 new 操作符并把使用的包装函数叫做构造函数之外，这个模式跟工厂模式其实是一模一样的。构造函数在不返回值的情况下，默认会返回新对象实例。而通过在构造函数的末尾添加一个 return 语句，可以重写调用构造函数时返回的值。

这个模式可以在特殊的情况下用来为对象创建构造函数。假设我们想创建一个具有额外方法的特殊数组。由于不能直接修改 Array 构造函数，因此可以使用这个模式。

```js
function SpecialArray() {
  //创建数组
  var values = new Array();
  //添加值
  values.push.apply(values, arguments);
  //添加方法
  values.toPipedString = function () {
    return this.join("|");
  };
  //返回数组
  return values;
}
var colors = new SpecialArray("red", "blue", "green");
alert(colors.toPipedString()); //"red|blue|green"
```

关于寄生构造函数模式，有一点需要说明：首先，返回的对象与构造函数或者与构造函数的原型属性之间没有关系；也就是说，构造函数返回的对象与在构造函数外部创建的对象没有什么不同。为此，不能依赖 instanceof 操作符来确定对象类型。由于存在上述问题，我们建议在可以使用其他模式的情况下，不要使用这种模式。

### 6.2.7 稳妥构造函数模式

道格拉斯·克罗克福德（Douglas Crockford）发明了 JavaScript 中的稳妥对象（durable objects）这个概念。所谓稳妥对象，指的是没有公共属性，而且其方法也不引用 this 的对象。稳妥对象最适合在一些安全的环境中（这些环境中会禁止使用 this 和 new），或者在防止数据被其他应用程序（如 Mashup 程序）改动时使用。稳妥构造函数遵循与寄生构造函数类似的模式，但有两点不同：一是新创建对象的实例方法不引用 this；二是不使用 new 操作符调用构造函数。按照稳妥构造函数的要求，可以将前面的 Person 构造函数重写如下。

```js
function Person(name, age, job) {
  //创建要返回的对象
  var o = new Object();

  //可以在这里定义私有变量和函数

  //添加方法
  o.sayName = function () {
    alert(name);
  };
  //返回对象
  return o;
}
```

注意，在以这种模式创建的对象中， 除了使用`sayName()`方法之外，没有其他办法访问 name 的值。可以像下面使用稳妥的 Person 构造函数。

```js
var friend = Person("Nicholas", 29, "Software Engineer");
friend.sayName(); //"Nicholas"
```

这样，变量 friend 中保存的是一个稳妥对象，而除了调用`sayName()`方法外，没有别的方式可以访问其数据成员。即使有其他代码会给这个对象添加方法或数据成员，但也不可能有别的办法访问传入到构造函数中的原始数据。稳妥构造函数模式提供的这种安全性，使得它非常适合在某些安全执行环境——例如， [ADsafe](www.adsafe.org)和 [Caja](http://code.google.com/p/google-caja/)提供的环境下使用。

> 与寄生构造函数模式类似，使用稳妥构造函数模式创建的对象与构造函数之间也没有什么关系，因此 instanceof 操作符对这种对象也没有意义。

## 6.3 继承　

继承是 OO 语言中的一个最为人津津乐道的概念。许多 OO 语言都支持两种继承方式：接口继承和实现继承。接口继承只继承方法签名，而实现继承则继承实际的方法。如前所述，由于函数没有签名，在 ECMAScript 中无法实现接口继承。 ECMAScript 只支持实现继承，而且其实现继承主要是依靠原型链来实现的。

### 6.3.1 原型链

ECMAScript 中描述了原型链的概念，并将原型链作为实现继承的主要方法。其基本思想是利用原型让一个引用类型继承另一个引用类型的属性和方法。简单回顾一下构造函数、原型和实例的关系：

1. 每个构造函数都有一个原型对象
2. 原型对象都包含一个指向构造函数的指针
3. 而实例都包含一个指向原型对象的内部指针

那么，假如我们让原型对象等于另一个类型的实例，结果会怎么样呢？显然，此时的原型对象将包含一个指向另一个原型的指针，相应地，另一个原型中也包含着一个指向另一个构造函数的指针。假如另一个原型又是另一个类型的实例，那么上述关系依然成立，如此层层递进，就构成了实例与原型的链条。这就是所谓原型链的基本概念。

实现原型链有一种基本模式，其代码大致如下。

```js
function SuperType() {
  this.property = true;
}

SuperType.prototype.getSuperValue = function () {
  return this.property;
};

function SubType() {
  this.subproperty = false;
}

// 继承了 SuperType
SubType.prototype = new SuperType();

SubType.prototype.getSubValue = function () {
  return this.subproperty;
};

var instance = new SubType();
alert(instance.getSuperValue()); //true

alert(instance instanceof Object); //true
alert(instance instanceof SuperType); //true
alert(instance instanceof SubType); //true

alert(Object.prototype.isPrototypeOf(instance)); //true
alert(SuperType.prototype.isPrototypeOf(instance)); //true
```

以上代码定义了两个类型： SuperType 和 SubType。每个类型分别有一个属性和一个方法。它们的主要区别是 SubType 继承了 SuperType，而继承是通过创建 SuperType 的实例，并将该实例赋给 `SubType.prototype` 实现的。实现的本质是重写原型对象，代之以一个新类型的实例。换句话说，原来存在于 SuperType 的实例中的所有属性和方法，现在也存在于 `SubType.prototype` 中了。在确立了继承关系之后，我们给 `SubType.prototype` 添加了一个方法，这样就在继承了 SuperType 的属性和方法的基础上又添加了一个新方法。这个例子中的实例以及构造函数和原型之间的关系如图 6-4 所示。

通过实现原型链，本质上扩展了本章前面介绍的原型搜索机制。读者大概还记得，当以读取模式访问一个实例属性时，首先会在实例中搜索该属性。如果没有找到该属性，则会继续搜索实例的原型。在通过原型链实现继承的情况下，搜索过程就得以沿着原型链继续向上。就拿上面的例子来说，调用`instance.getSuperValue()`会经历三个搜索步骤：

1. 搜索实例；
2. 搜索 `SubType.prototype`；
3. 搜索 `SuperType.prototype`，最后一步才会找到该方法。

在找不到属性或方法的情况下，搜索过程总是要一环一环地前行到原型链末端才会停下来。

**1. 别忘记默认的原型**

事实上，前面例子中展示的原型链还少一环。我们知道，所有引用类型默认都继承了 Object，而这个继承也是通过原型链实现的。大家要记住，所有函数的默认原型都是 Object 的实例，因此默认原型都会包含一个内部指针，指向 `Object.prototype`。这也正是所有自定义类型都会继承 `toString()`、`valueOf()`等默认方法的根本原因。所以，我们说上面例子展示的原型链中还应该包括另外一个继承层次。图 6-5 为我们展示了该例子中完整的原型链。

一句话，SubType 继承了 SuperType，而 SuperType 继承了 Object。当调用 `instance.toString()`时，实际上调用的是保存在 `Object.prototype` 中的那个方法。

**2. 确定原型和实例的关系**

可以通过两种方式来确定原型和实例之间的关系。第一种方式是使用 instanceof 操作符，只要用这个操作符来测试实例与原型链中出现过的构造函数，结果就会返回 true。以下几行代码就说明了这一点。

```js
alert(instance instanceof Object); //true
alert(instance instanceof SuperType); //true
alert(instance instanceof SubType); //true
```

由于原型链的关系，我们可以说 instance 是 Object、 SuperType 或 SubType 中任何一个类型的实例。因此，测试这三个构造函数的结果都返回了 true。第二种方式是使用`isPrototypeOf()`方法。同样，只要是原型链中出现过的原型，都可以说是该原型链所派生的实例的原型，因此`isPrototypeOf()`方法也会返回 true，如下所示。

```js
alert(Object.prototype.isPrototypeOf(instance)); //true
alert(SuperType.prototype.isPrototypeOf(instance)); //true
alert(SubType.prototype.isPrototypeOf(instance)); //true
```

**3. 谨慎地定义方法**

子类型有时候需要重写超类型中的某个方法，或者需要添加超类型中不存在的某个方法。但不管怎样，给原型添加方法的代码一定要放在替换原型的语句之后。来看下面的例子。

```js
function SuperType() {
  this.property = true;
}
SuperType.prototype.getSuperValue = function () {
  return this.property;
};
function SubType() {
  this.subproperty = false;
}
//继承了 SuperType
SubType.prototype = new SuperType();

//添加新方法
SubType.prototype.getSubValue = function () {
  return this.subproperty;
};
//重写超类型中的方法
SubType.prototype.getSuperValue = function () {
  return false;
};

var instance = new SubType();
alert(instance.getSuperValue()); //false
```

在以上代码中，加粗的部分是两个方法的定义。第一个方法 `getSubValue()`被添加到了 SubType 中。第二个方法 `getSuperValue()`是原型链中已经存在的一个方法，但重写这个方法将会屏蔽原来的那个方法。换句话说，当通过 SubType 的实例调用 `getSuperValue()`时，调用的就是这个重新定义的方法；但通过 SuperType 的实例调用 `getSuperValue()`时，还会继续调用原来的那个方法。这里要格外注意的是，必须在用 SuperType 的实例替换原型之后，再定义这两个方法。还有一点需要提醒读者，即在通过原型链实现继承时，不能使用对象字面量创建原型方法。因为这样做就会重写原型链，如下面的例子所示。

```js
function SuperType() {
  this.property = true;
}
SuperType.prototype.getSuperValue = function () {
  return this.property;
};
function SubType() {
  this.subproperty = false;
}

//继承了 SuperType
SubType.prototype = new SuperType();

//使用字面量添加新方法，会导致上一行代码无效
SubType.prototype = {
  getSubValue: function () {
    return this.subproperty;
  },
  someOtherMethod: function () {
    return false;
  },
};
var instance = new SubType();
alert(instance.getSuperValue()); //error!
```

以上代码展示了刚刚把 SuperType 的实例赋值给原型，紧接着又将原型替换成一个对象字面量而导致的问题。由于现在的原型包含的是一个 Object 的实例，而非 SuperType 的实例，因此我们设想中的原型链已经被切断——SubType 和 SuperType 之间已经没有关系了。

**4. 原型链的问题**

原型链虽然很强大，可以用它来实现继承，但它也存在一些问题。

其中，最主要的问题来自**包含引用类型值的原型**。

想必大家还记得，我们前面介绍过包含引用类型值的原型属性会被所有实例共享；而这也正是为什么要在构造函数中，而不是在原型对象中定义属性的原因。在通过原型来实现继承时，原型实际上会变成另一个类型的实例。于是，原先的实例属性也就顺理成章地变成了现在的原型属性了。下列代码可以用来说明这个问题。

```js
function SuperType() {
  this.colors = ["red", "blue", "green"];
}
function SubType() {}

//继承了 SuperType
SubType.prototype = new SuperType();

var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"

var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green,black"
```

这个例子中的 SuperType 构造函数定义了一个 colors 属性，该属性包含一个数组（引用类型值）。SuperType 的每个实例都会有各自包含自己数组的 colors 属性。当 SubType 通过原型链继承了 SuperType 之后，`SubType.prototype` 就变成了 SuperType 的一个实例，因此它也拥有了一个它自己的 colors 属性——就跟专门创建了一个 `SubType.prototype.colors` 属性一样。但结果是什么呢？结果是 SubType 的所有实例都会共享这一个 colors 属性。 而我们对 `instance1.colors` 的修改能够通过 `instance2.colors` 反映出来，就已经充分证实了这一点。

原型链的第二个问题是：在创建子类型的实例时，**不能向超类型的构造函数中传递参数**。

实际上，应该说是没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。有鉴于此，再加上前面刚刚讨论过的由于原型中包含引用类型值所带来的问题，实践中很少会单独使用原型链。

### 6.3.2 借用构造函数

在解决原型中包含引用类型值所带来问题的过程中，开发人员开始使用一种叫做借用构造函数（constructor stealing）的技术（有时候也叫做伪造对象或经典继承）。这种技术的基本思想相当简单，即在子类型构造函数的内部调用超类型构造函数。别忘了，函数只不过是在特定环境中执行代码的对象，因此通过使用 `apply()`和 `call()`方法也可以在（将来）新创建的对象上执行构造函数，如下所示：

```js
function SuperType() {
  this.colors = ["red", "blue", "green"];
}
function SubType() {
  //继承了 SuperType
  SuperType.call(this);
}

var instance1 = new SubType();
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"

var instance2 = new SubType();
alert(instance2.colors); //"red,blue,green"
```

代码中加粗的那一行代码“借调”了超类型的构造函数。通过使用`call()`方法（或`apply()`方法也可以），我们实际上是在（未来将要）新创建的 SubType 实例的环境下调用了 SuperType 构造函数。这样一来，就会在新 SubType 对象上执行`SuperType()`函数中定义的所有对象初始化代码。结果，SubType 的每个实例就都会具有自己的 colors 属性的副本了。

**1. 传递参数**

相对于原型链而言，借用构造函数有一个很大的优势，即可以在子类型构造函数中向超类型构造函数传递参数。看下面这个例子。

```js
function SuperType(name) {
  this.name = name;
}
function SubType() {
  //继承了 SuperType，同时还传递了参数
  SuperType.call(this, "Nicholas");
  //实例属性
  this.age = 29;
}
var instance = new SubType();
alert(instance.name); //"Nicholas";
alert(instance.age); //29
```

以上代码中的 SuperType 只接受一个参数 name，该参数会直接赋给一个属性。在 SubType 构造函数内部调用 SuperType 构造函数时，实际上是为 SubType 的实例设置了 name 属性。为了确保 SuperType 构造函数不会重写子类型的属性，可以在调用超类型构造函数后，再添加应该在子类型中定义的属性。

**2. 借用构造函数的问题**

如果仅仅是借用构造函数，那么也将无法避免构造函数模式存在的问题。

1. 方法都在构造函数中定义，因此函数复用就无从谈起了
2. 在超类型的原型中定义的方法，对子类型而言也是不可见的，结果所有类型都只能使用构造函数模式

考虑到这些问题，借用构造函数的技术也是很少单独使用的。

### 6.3.3 组合继承

组合继承（combination inheritance），有时候也叫做伪经典继承，指的是将原型链和借用构造函数的技术组合到一块，从而发挥二者之长的一种继承模式。其背后的思路是使用原型链实现对原型属性和方法的继承，而通过借用构造函数来实现对实例属性的继承。这样，既通过在原型上定义方法实现了函数复用，又能够保证每个实例都有它自己的属性。下面来看一个例子。

```js
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function () {
  alert(this.name);
};
function SubType(name, age) {
  //继承属性
  SuperType.call(this, name);
  this.age = age;
}

//继承方法
SubType.prototype = new SuperType();
SubType.prototype.constructor = SubType;

SubType.prototype.sayAge = function () {
  alert(this.age);
};

var instance1 = new SubType("Nicholas", 29);
instance1.colors.push("black");
alert(instance1.colors); //"red,blue,green,black"
instance1.sayName(); //"Nicholas";
instance1.sayAge(); //29

var instance2 = new SubType("Greg", 27);
alert(instance2.colors); //"red,blue,green"
instance2.sayName(); //"Greg";
instance2.sayAge(); //27
```

在这个例子中， SuperType 构造函数定义了两个属性： name 和 colors。 SuperType 的原型定义了一个方法 `sayName()`。 SubType 构造函数在调用 SuperType 构造函数时传入了 name 参数，紧接着又定义了它自己的属性 age。然后，将 SuperType 的实例赋值给 SubType 的原型，然后又在该新原型上定义了方法 `sayAge()`。这样一来，就可以让两个不同的 SubType 实例既分别拥有自己属性——包括 colors 属性，又可以使用相同的方法了。组合继承避免了原型链和借用构造函数的缺陷，融合了它们的优点，成为 JavaScript 中最常用的继承模式。而且， instanceof 和 `isPrototypeOf()` 也能够用于识别基于组合继承创建的对象。

### 6.3.4 原型式继承

道格拉斯·克罗克福德在 2006 年写了一篇文章，题为 Prototypal Inheritance in JavaScript （JavaScript 中的原型式继承）。在这篇文章中，他介绍了一种实现继承的方法，这种方法并没有使用严格意义上的构造函数。他的想法是借助原型可以基于已有的对象创建新对象，同时还不必因此创建自定义类型。为了达到这个目的，他给出了如下函数。

```js
function object(o) {
  function F() {}
  F.prototype = o;
  return new F();
}
```

在`object()`函数内部，先创建了一个临时性的构造函数，然后将传入的对象作为这个构造函数的原型，最后返回了这个临时类型的一个新实例。从本质上讲，`object()`对传入其中的对象执行了一次浅复制。来看下面的例子。

```js
var person = {
  name: "Nicholas",
  friends: ["wesley", "fox"],
};

var anotherPerson = object(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");

var yetAnotherPerson = object(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");

alert(person.friends); //'wesley,fox,Rob,Barbie'
```

克罗克福德主张的这种原型式继承，要求你必须有一个对象可以作为另一个对象的基础。如果有这么一个对象的话，可以把它传递给`object()`函数，然后再根据具体需求对得到的对象加以修改即可。在这个例子中，可以作为另一个对象基础的是 person 对象，于是我们把它传入到`object()`函数中，然后该函数就会返回一个新对象。这个新对象将 person 作为原型，所以它的原型中就包含一个基本类型值属性和一个引用类型值属性。这意味着 `person.friends` 不仅属于 person 所有，而且也会被 anotherPerson 以及 yetAnotherPerson 共享。实际上，这就相当于又创建了 person 对象的两个副本。

ECMAScript 5 通过新增 `Object.create()`方法规范化了原型式继承。这个方法接收两个参数：一个用作新对象原型的对象和（可选的）一个为新对象定义额外属性的对象。在传入一个参数的情况下，`Object.create()`与`object()`方法的行为相同。

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"],
};

var anotherPerson = Object.create(person);
anotherPerson.name = "Greg";
anotherPerson.friends.push("Rob");

var yetAnotherPerson = Object.create(person);
yetAnotherPerson.name = "Linda";
yetAnotherPerson.friends.push("Barbie");

alert(person.friends); //"Shelby,Court,Van,Rob,Barbie"
```

`Object.create()`方法的第二个参数与`Object.defineProperties()`方法的第二个参数格式相同：每个属性都是通过自己的描述符定义的。以这种方式指定的任何属性都会覆盖原型对象上的同名属性。例如：

```js
var person = {
  name: 'Nicholas',
  friends: ['wesley','fox']
};

var anotherPerson = Object.create(person, {
  name：{
    value: 'Greg'
  }
});
```

支持 `Object.create()`方法的浏览器有 IE9+、 Firefox 4+、 Safari 5+、 Opera 12+和 Chrome。

在没有必要兴师动众地创建构造函数，而只想让一个对象与另一个对象保持类似的情况下，原型式继承是完全可以胜任的。不过别忘了，包含引用类型值的属性始终都会共享相应的值，就像使用原型模式一样。

### 6.3.5 寄生式继承

寄生式（parasitic）继承是与原型式继承紧密相关的一种思路，并且同样也是由克罗克福德推而广之的。寄生式继承的思路与寄生构造函数和工厂模式类似，即创建一个仅用于封装继承过程的函数，该函数在内部以某种方式来增强对象，最后再像真地是它做了所有工作一样返回对象。以下代码示范了寄生式继承模式。

```js
function createAnother(original) {
  var clone = object(original); //通过调用函数创建一个新对象
  clone.sayHi = function () {
    //以某种方式来增强这个对象
    console.log("Hi");
  };
  return clone; // 返回这个对象
}
```

在这个例子中，`createAnother()`函数接收了一个参数，也就是将要作为新对象基础的对象。然后，把这个对象（original）传递给`object()`函数，将返回的结果赋值给 clone。再为 clone 对象添加一个新方法`sayHi()`，最后返回 clone 对象。可以像下面这样来使用`createAnother()`函数：

```js
var person = {
  name: "Nicholas",
  friends: ["Shelby", "Court", "Van"],
};
var anotherPerson = createAnother(person);
anotherPerson.sayHi(); //"hi"
```

这个例子中的代码基于 person 返回了一个新对象——anotherPerson。新对象不仅具有 person 的所有属性和方法，而且还有自己的`sayHi()`方法。

在主要考虑对象而不是自定义类型和构造函数的情况下，寄生式继承也是一种有用的模式。前面示范继承模式时使用的`object()`函数不是必需的；任何能够返回新对象的函数都适用于此模式。

> 使用寄生式继承来为对象添加函数，会由于不能做到函数复用而降低效率；这一点与构造函数模式类似。

### 6.3.6 寄生组合式继承

前面说过，组合继承是 JavaScript 最常用的继承模式；不过，它也有自己的不足。组合继承最大的问题就是无论什么情况下，都会调用两次超类型构造函数：一次是在创建子类型原型的时候，另一次是在子类型构造函数内部。没错，子类型最终会包含超类型对象的全部实例属性，但我们不得不在调用子类型构造函数时重写这些属性。再来看一看下面组合继承的例子。

```js
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function () {
  alert(this.name);
};

function SubType(name, age) {
  SuperType.call(this, name); //第二次调用 SuperType()
  this.age = age;
}

SubType.prototype = new SuperType(); //第一次调用 SuperType()
SubType.prototype.constructor = SubType;

SubType.prototype.sayAge = function () {
  alert(this.age);
};
```

加粗字体的行中是调用 SuperType 构造函数的代码。在第一次调用 SuperType 构造函数时， `SubType.prototype` 会得到两个属性： name 和 colors；它们都是 SuperType 的实例属性，只不过现在位于 SubType 的原型中。当调用 SubType 构造函数时，又会调用一次 SuperType 构造函数，这一次又在新对象上创建了实例属性 name 和 colors。于是，这两个属性就屏蔽了原型中的两个同名属性。图 6-6 展示了上述过程。

如图 6-6 所示，有两组 name 和 colors 属性：一组在实例上，一组在 SubType 原型中。这就是调用两次 SuperType 构造函数的结果。好在我们已经找到了解决这个问题方法——寄生组合式继承。所谓寄生组合式继承，即通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。其背后的基本思路是：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型原型的一个副本而已。本质上，就是使用寄生式继承来继承超类型的原型，然后再将结果指定给子类型的原型。寄生组合式继承的基本模式如下所示。

```js
function inheritPrototype(subType, superType) {
  var prototype = object(superType.prototype); //创建对象
  prototype.constructor = subType; //增强对象
  subType.prototype = prototype; //指定对象
}
```

这个示例中的 `inheritPrototype()`函数实现了寄生组合式继承的最简单形式。这个函数接收两个参数：子类型构造函数和超类型构造函数。在函数内部，第一步是创建超类型原型的一个副本。第二步是为创建的副本添加 constructor 属性，从而弥补因重写原型而失去的默认的 constructor 属性。最后一步，将新创建的对象（即副本）赋值给子类型的原型。这样，我们就可以用调用 `inheritPrototype()`函数的语句，去替换前面例子中为子类型原型赋值的语句了，例如：

```js
function SuperType(name) {
  this.name = name;
  this.colors = ["red", "blue", "green"];
}
SuperType.prototype.sayName = function () {
  alert(this.name);
};

function SubType(name, age) {
  SuperType.call(this, name);
  this.age = age;
}

inheritPrototype(SubType, SuperType);

SubType.prototype.sayAge = function () {
  alert(this.age);
};
```

这个例子的高效率体现在它只调用了一次 SuperType 构造函数，并且因此避免了在 `SubType.prototype` 上面创建不必要的、多余的属性。与此同时，原型链还能保持不变；因此，还能够正常使用 instanceof 和 `isPrototypeOf()`。开发人员普遍认为寄生组合式继承是引用类型最理想的继承范式。

> YUI 的`YAHOO.lang.extend()`方法采用了寄生组合继承，从而让这种模式首次出现在了一个应用非常广泛的 JavaScript 库中。要了解有关 YUI 的更多信息，请访问[链接](http://developer.yahoo.com/yui/)。

## 6.4 小结　

ECMAScript 支持面向对象（OO）编程，但不使用类或者接口。对象可以在代码执行过程中创建和增强，因此具有动态性而非严格定义的实体。在没有类的情况下，可以采用下列模式创建对象。

- 工厂模式，使用简单的函数创建对象，为对象添加属性和方法，然后返回对象。这个模式后来被构造函数模式所取代。
- 构造函数模式，可以创建自定义引用类型，可以像创建内置对象实例一样使用 new 操作符。不过，构造函数模式也有缺点，即它的每个成员都无法得到复用，包括函数。由于函数可以不局限于任何对象（即与对象具有松散耦合的特点），因此没有理由不在多个对象间共享函数。
- 原型模式，使用构造函数的 prototype 属性来指定那些应该共享的属性和方法。组合使用构造函数模式和原型模式时，使用构造函数定义实例属性，而使用原型定义共享的属性和方法。

JavaScript 主要通过原型链实现继承。原型链的构建是通过将一个类型的实例赋值给另一个构造函数的原型实现的。这样，子类型就能够访问超类型的所有属性和方法，这一点与基于类的继承很相似。原型链的问题是对象实例共享所有继承的属性和方法，因此不适宜单独使用。解决这个问题的技术是借用构造函数，即在子类型构造函数的内部调用超类型构造函数。这样就可以做到每个实例都具有自己的属性，同时还能保证只使用构造函数模式来定义类型。使用最多的继承模式是组合继承，这种模式使用原型链继承共享的属性和方法，而通过借用构造函数继承实例属性。

此外，还存在下列可供选择的继承模式。

- 原型式继承，可以在不必预先定义构造函数的情况下实现继承，其本质是执行对给定对象的浅复制。而复制得到的副本还可以得到进一步改造。
- 寄生式继承，与原型式继承非常相似，也是基于某个对象或某些信息创建一个对象，然后增强对象，最后返回对象。为了解决组合继承模式由于多次调用超类型构造函数而导致的低效率问题，可以将这个模式与组合继承一起使用。
- 寄生组合式继承，集寄生式继承和组合继承的优点与一身，是实现基于类型继承的最有效方式。

# 第7章 函数表达式

定义函数的方式有两种：一种是函数声明，另一种就是函数表达式。

函数声明是使用 function 关键字，再加上函数的名字，这就是指定函数名的方式。函数声明的重要特征就是函数声明提升，执行代码之前先读取函数声明。这意味着可以把函数声明放在调用它的语句后面。

```js
//  不会抛出错误
sayHi();
function sayHi(){
  alert("Hi!");
}
```

第二种创建函数的方式是使用函数表达式。函数表达式有几种不同的语法形式。

下面形式看起来好像是常规的变量赋值语句，即创建一个函数并将它赋值给变量。这种情况下创建的函数叫做匿名函数（anonymous function），因为 function 关键字后面没有标识符（匿名函数有时候也叫拉姆达函数），匿名函数的 name 属性是空字符串。函数表达式与其他表达式一样，在使用前必须先赋值。

```js
sayHi(); //错误：函数还不存在
var sayHi = function(){
  alert("Hi!");
};
```

理解函数提升的关键，就是理解函数声明与函数表达式之间的区别。例如，执行以下代码的结果可能会让人意想不到。

```js
//不要这样做！
if(condition){
  function sayHi(){
      alert("Hi!");
    }
} else {
  function sayHi(){
      alert("Yo!");
    }
}
```

实际上，以上的代码在 ECMAScript 中属于无效语法， JavaScript 引擎会尝试修正错误，将其转换为合理的状态。但问题是浏览器尝试修正错误的做法并不一致。大多数浏览器会返回第二个声明，忽略condition； Firefox 会在 condition 为 true 时返回第一个声明。因此这种使用方式很危险，不应该出现在你的代码中。不过，如果是使用函数表达式，那就没有什么问题了。

```js
//可以这样做
var sayHi;
if(condition){
  sayHi = function(){
    alert("Hi!");
  };
} else {
  sayHi = function(){
    alert("Yo!");
  };
}
```

能够创建函数再赋值给变量，也就能够把函数作为其他函数的值返回。

```js
function createComparisonFunction(propertyName) {
  return function(object1, object2){
    var value1 = object1[propertyName];
    var value2 = object2[propertyName];
    if (value1 < value2){
     return -1;
    } else if (value1 > value2){
     return 1;
    } else {
     return 0;
    }
  };
}
```

返回的函数可能会被赋值给一个变量，或者以其他方式被调用；不过，在函数内部，它是匿名的。在把函数当成值来使用的情况下都可以使用匿名函数。不过，这并不是匿名函数唯一的用途。

## 7.1 递归 

递归函数是在一个函数通过名字调用自身的情况下构成的。

```js
function factorial(num){
  if (num <= 1){
    return 1;
  } else {
    return num * factorial(num-1);
  }
}
```

这是一个经典的递归阶乘函数。虽然这个函数表面看来没什么问题，但下面的代码却可能导致它出错。

```js
var anotherFactorial = factorial;
factorial = null;
alert(anotherFactorial(4)); //出错！
```

`arguments.callee`是一个指向正在执行的函数的指针，因此可以用它来实现对函数的递归调用。通过使用 `arguments.callee` 代替函数名，可以确保无论怎样调用函数都不会出问题。

```js
function factorial(num){
  if (num <= 1){
    return 1; 
  } else {
    return num * arguments.callee(num-1);
  }
}
```

但在严格模式下，不能通过脚本访问`arguments.callee`，访问这个属性会导致错误。不过，可以使用命名函数表达式来达成相同的结果。

```js
var factorial = (function f(num){
  if (num <= 1){
    return 1;
  } else {
    return num * f(num-1);
  }
});
```

## 7.2 闭包 

闭包是指有权访问另一个函数作用域中的变量的函数。创建闭包的常见方式，就是在一个函数内部创建另一个函数。下面代码即使这个内部函数被返回了，而且是在其他地方被调用了，但它仍然可以访问变量 propertyName 。之所以还能够访问这个变量，是因为内部函数的作用域链中包含`createComparisonFunction()`的作用域。要彻底搞清楚其中的细节，必须从理解函数被调用的时候都会发生什么入手。

```js
function createComparisonFunction(propertyName) {
  return function(object1, object2){
    var value1 = object1[propertyName];
    var value2 = object2[propertyName];
    if (value1 < value2){
      return -1;
    } else if (value1 > value2){
      return 1;
    } else {
      return 0;
    }
  };
}
```

当某个函数被调用时，会创建一个执行环境（execution context）及相应的作用域链。然后，使用 arguments 和其他命名参数的值来初始化函数的活动对象（activation object）。但在作用域链中，外部函数的活动对象始终处于第二位，外部函数的外部函数的活动对象处于第三位，……直至作为作用域链终点的全局执行环境。

在函数执行过程中，为读取和写入变量的值，就需要在作用域链中查找变量。无论什么时候在函数中访问一个变量时，就会从作用域链中搜索具有相应名字的变量。

```js
function compare(value1, value2){
  if (value1 < value2){
    return -1;
  } else if (value1 > value2){
    return 1;
  } else {
    return 0;
  }
}
var result = compare(5, 10);
```

以上代码先定义了 `compare()`函数，然后又在全局作用域中调用了它。当调用 `compare()`时，会创建一个包含 arguments、 value1 和 value2 的活动对象。全局执行环境的变量对象（包含 result和 compare）在 `compare()`执行环境的作用域链中则处于第二位。

后台的每个执行环境都有一个表示变量的对象——变量对象。全局环境的变量对象始终存在，而像`compare()`函数这样的局部环境的变量对象，则只在函数执行的过程中存在。在创建 `compare()`函数时，会创建一个预先包含全局变量对象的作用域链，这个作用域链被保存在内部的`[[Scope]]`属性中。当调用 `compare()`函数时，会为函数创建一个执行环境，然后通过复制函数的`[[Scope]]`属性中的对象构建起执行环境的作用域链。此后，又有一个活动对象（在此作为变量对象使用）被创建并被推入执行环境作用域链的前端。对于这个例子中 `compare()`函数的执行环境而言，其作用域链中包含两个变量对象：本地活动对象和全局变量对象。显然，作用域链本质上是一个指向变量对象的指针列表，它只引用但不实际包含变量对象。

无论什么时候在函数中访问一个变量时，就会从作用域链中搜索具有相应名字的变量。一般来讲，当函数执行完毕后，局部活动对象就会被销毁，内存中仅保存全局作用域（全局执行环境的变量对象）。但是，闭包的情况又有所不同。

在另一个函数内部定义的函数会将包含函数（即外部函数）的活动对象添加到它的作用域链中。因此，在 `createComparisonFunction()`函数内部定义的匿名函数的作用域链中，实际上将会包含外部函数 `createComparisonFunction()`的活动对象。当下列代码执行时，包含函数与内部匿名函数的作用域链。

```js
var compare = createComparisonFunction("name");
var result = compare({ name: "Nicholas" }, { name: "Greg" });
```

在匿名函数从 `createComparisonFunction()`中被返回后，它的作用域链被初始化为包含`createComparisonFunction()`函数的活动对象和全局变量对象。这样，匿名函数就可以访问在`createComparisonFunction()`中定义的所有变量。更为重要的是，`createComparisonFunction()`函数在执行完毕后，其活动对象也不会被销毁，因为匿名函数的作用域链仍然在引用这个活动对象。换句话说，当 `createComparisonFunction()`函数返回后，其执行环境的作用域链会被销毁，但它的活动对象仍然会留在内存中；直到匿名函数被销毁后， `createComparisonFunction()`的活动对象才会被销毁，例如：

```js
//创建函数
var compareNames = createComparisonFunction("name");

//调用函数
var result = compareNames({ name: "Nicholas" }, { name: "Greg" });

//解除对匿名函数的引用（以便释放内存）
compareNames = null;
```

首先，创建的比较函数被保存在变量 compareNames 中。而通过将 compareNames 设置为等于 null 解除该函数的引用，就等于通知垃圾回收例程将其清除。随着匿名函数的作用域链被销毁，其他作用域（除了全局作用域）也都可以安全地销毁了。

> 由于闭包会携带包含它的函数的作用域，因此会比其他函数占用更多的内存。过度使用闭包可能会导致内存占用过多，建议只在绝对必要时再考虑使用闭包。虽然像 V8 等优化后的 JavaScript 引擎会尝试回收被闭包占用的内存，但请大家还是要慎重使用闭包。

### 7.2.1 闭包与变量

作用域链的这种配置机制引出了一个值得注意的副作用，即闭包只能取得包含函数中任何变量的最后一个值。闭包所保存的是整个变量对象，而不是某个特殊的变量。

```js
function createFunctions(){
  var result = new Array();
  for (var i=0; i < 10; i++){
    result[i] = function(){
      return i;
    };
  }
  return result;
}
```

这个函数会返回一个函数数组。表面上看，似乎每个函数都应该返自己的索引值。但实际上，每个函数都返回 10。因为每个函数的作用域链中都保存着`createFunctions()`函数的活动对象，所以它们引用的都是同一个变量i 。 当`createFunctions()`函数返回后，变量 i 的值是 10，此时每个函数都引用着保存变量 i 的同一个变量对象，所以在每个函数内部 i 的值都是 10。

可以通过创建另一个匿名函数强制让闭包的行为符合预期。

```js
function createFunctions(){
  var result = new Array();
  for (var i=0; i < 10; i++){
    result[i] = function(num){
      return function(){
        return num;
      };
    }(i);
  }
  return result;
}
```

在这个版本中，没有直接把闭包赋值给数组，而是定义了一个匿名函数，并将立即执行该匿名函数的结果赋给数组。这里的匿名函数有一个参数 num，也就是最终的函数要返回的值。在调用每个匿名函数时，我们传入了变量 i。由于函数参数是按值传递的，所以就会将变量 i 的当前值复制给参数 num。而在这个匿名函数内部，又创建并返回了一个访问 num 的闭包。这样一来， result 数组中的每个函数都有自己 num 变量的一个副本，因此就可以返回各自不同的数值了。

### 7.2.2 关于this对象

this 对象是在运行时基于函数的执行环境绑定的：在全局函数中，this 等于 window，而当函数被作为某个对象的方法调用时，this 等于那个对象。不过，匿名函数的执行环境具有全局性，因此其 this 对象通常指向 window。但有时候由于编写闭包的方式不同，这一点可能不会那么明显。

```js
var name = "The Window";
var object = {
  name : "My Object",
  getNameFunc : function(){
    return function(){
      return this.name;
    };
  }
};
alert(object.getNameFunc()()); //"The Window"（在非严格模式下）
```

为什么匿名函数没有取得其包含作用域（或外部作用域）的 this 对象呢？前面曾经提到过，每个函数在被调用时都会自动取得两个特殊变量：`this` 和 `arguments`。内部函数在搜索这两个变量时，只会搜索到其活动对象为止，因此永远不可能直接访问外部函数中的这两个变量。不过，把外部作用域中的 this 对象保存在一个闭包能够访问到的变量里，就可以让闭包访问该对象了。

```js
var name = "The Window";
var object = {
  name : "My Object",
  getNameFunc : function(){
    var that = this;
    return function(){
      return that.name;
    };
  }
};
alert(object.getNameFunc()()); //"My Object"
```

> this 和 arguments 也存在同样的问题。如果想访问作用域中的 arguments 对象，必须将对该对象的引用保存到另一个闭包能够访问的变量中。

在下面几种特殊情况下， this 的值可能会意外地改变。

```js
var name = "The Window";
var object = {
  name : "My Object",
  getName: function(){
    return this.name;
  }
};

object.getName(); //"My Object"
(object.getName)(); //"My Object"
(object.getName = object.getName)(); //"The Window"，在非严格模式下
```

第三行代码先执行了一条赋值语句，然后再调用赋值后的结果。因为这个赋值表达式的值是函数本身，所以 this 的值不能得到维持，结果就返回了"The Window"。

### 7.2.3 内存泄漏

由于 IE9 之前的版本对 JScript 对象和 COM 对象使用不同的垃圾收集例程，因此闭包在 IE 的这些版本中会导致一些特殊的问题。具体来说，如果闭包的作用域链中保存着一个 HTML 元素，那么就意味着该元素将无法被销毁。只要匿名函数存在，变量引用 DOM 的引用数至少也是1，因此它所占用的内存就永远不会被回收。

```js
function assignHandler(){
  var element = document.getElementById("someElement");
  element.onclick = function(){
    alert(element.id);
  };
}
```

闭包会引用包含函数的整个活动对象，而其中包含着 element。通过把 `element.id` 的一个副本保存在一个变量中，并且在闭包中引用该变量消除了循环引用。但仅仅做到这一步，还是不能解决内存泄漏的问题。即使闭包不直接引用 element，包含函数的活动对象中也仍然会保存一个引用。因此，有必要把 element 变量设置为 null。这样就能够解除对 DOM 对象的引用，顺利地减少其引用数，确保正常回收其占用的内存。

```js
function assignHandler(){
  var element = document.getElementById("someElement");
  var id = element.id;
  element.onclick = function(){
    alert(id);
  };
  element = null;
}
```

## 7.3 模仿块级作用域

JavaScript 没有块级作用域的概念。这意味着在块语句中定义的变量，实际上是在包含函数中而非语句中创建的。

```js
function outputNumbers(count){
  for (var i=0; i < count; i++){
    alert(i);
  }
  alert(i); //计数
}
```

在 Java、 C++等语言中，变量 i 只会在 for 循环的语句块中有定义，循环一旦结束，变量 i 就会被销毁。可是在 JavaScrip 中，变量 i 是定义在 `ouputNumbers()`的活动对象中的，因此从它有定义开始，就可以在函数内部随处访问它。即使像下面这样错误地重新声明同一个变量，也不会改变它的值。

```js
function outputNumbers(count){
  for (var i=0; i < count; i++){
    alert(i);
  }
  var i; //重新声明变量
  alert(i); //计数
}
```

JavaScript 从来不会告诉你是否多次声明了同一个变量，它只会对后续的声明视而不见（不过，它会执行后续声明中的变量初始化）。匿名函数可以用来模仿块级作用域并避免这个问题。

用作块级作用域（通常称为私有作用域）的匿名函数的语法如下所示。

```js
(function(){
  //这里是块级作用域
})();
```

以上代码定义并立即调用了一个匿名函数。将函数声明包含在一对圆括号中，表示它实际上是一个函数表达式。而紧随其后的另一对圆括号会立即调用这个函数。如果有读者感觉这种语法不太好理解，可以再看看下面这个例子。

```js
var count = 5;
outputNumbers(count);
// 也可以这么做
// outputNumbers(5);
```

这样做之所以可行，是因为变量只不过是值的另一种表现形式，因此用实际的值替换变量没有问题。再看下面的例子。

```js
var someFunction = function(){
  //这里是块级作用域
};
someFunction();
```

通过前面的例子我们知道，可以使用实际的值来取代变量 count，那在这里是不是也可以用函数的值直接取代函数名呢？ 然而，下面的代码却会导致错误。

```js
function(){
  //这里是块级作用域
}(); //出错！
```

这段代码会导致语法错误，是因为 JavaScript 将 function 关键字当作一个函数声明的开始，而函数声明后面不能跟圆括号。然而，函数表达式的后面可以跟圆括号。要将函数声明转换成函数表达式，只要给它加上一对圆括号即可。

无论在什么地方，只要临时需要一些变量，就可以使用私有作用域：

```js
function outputNumbers(count){
  (function () {
    for (var i=0; i < count; i++){
      alert(i);
    }
  })();
  alert(i); //导致一个错误！
}
```

因此，变量 i 只能在循环中使用，使用后即被销毁。而在私有作用域中能够访问变量 count，是因为这个匿名函数是一个闭包，它能够访问包含作用域中的所有变量。

这种技术经常在全局作用域中被用在函数外部，从而限制向全局作用域中添加过多的变量和函数。一般来说，我们都应该尽量少向全局作用域中添加变量和函数。在一个由很多开发人员共同参与的大型应用程序中，过多的全局变量和函数很容易导致命名冲突。而通过创建私有作用域，每个开发人员既可以使用自己的变量，又不必担心搞乱全局作用域。

```js
(function(){
  var now = new Date();
  if (now.getMonth() == 0 && now.getDate() == 1){
    alert("Happy new year!");
  }
})();
```

把上面这段代码放在全局作用域中，可以用来确定哪一天是 1 月 1 日；如果到了这一天，就会向用户显示一条祝贺新年的消息。其中的变量 now 现在是匿名函数中的局部变量，而我们不必在全局作用域中创建它。

> 这种做法可以减少闭包占用的内存问题，因为没有指向匿名函数的引用。只要函数执行完毕，就可以立即销毁其作用域链了。

## 7.4 私有变量

严格来说，JavaScript 中没有私有成员的概念：所有对象属性都是公有的。不过，倒是有一个私有变量的概念。任何函数中定义的变量，都可以认为是私有变量，因为不能在函数的外部访问这些变量。私有变量包括函数的参数、局部变量和在函数内部定义的其他函数。

```js
function add(num1, num2){
  var sum = num1 + num2;
  return sum;
}
```

在这个函数内部，有 3 个私有变量： num1、 num2 和 sum。在函数内部可以访问这几个变量，但在函数外部则不能访问它们。如果在这个函数内部创建一个闭包，那么闭包通过自己的作用域链也可以访问这些变量。而利用这一点，就可以创建用于访问私有变量的公有方法。

我们把有权访问私有变量和私有函数的公有方法称为特权方法。有两种在对象上创建特权方法的方式。第一种是在构造函数中定义特权方法。

```js
function MyObject(){
  // 私有变量
  var privateVariable = 10;
  // 私有函数
  function privateFunction(){
    return false;
  }
  // 特权方法
  this.publicMethod = function (){
    privateVariable++;
    return privateFunction();
  };
}
```

能够在构造函数中定义特权方法，是因为特权方法作为闭包有权访问在构造函数中定义的所有变量和函数。

利用私有和特权成员，可以隐藏那些不应该被直接修改的数据。

```js
function Person(name){
  this.getName = function(){
    return name;
  };
  this.setName = function (value) {
    name = value;
  };
}
var person = new Person("Nicholas");
alert(person.getName()); //"Nicholas"
person.setName("Greg");
alert(person.getName()); //"Greg"
```

不过，在构造函数中定义特权方法也有一个缺点，那就是你必须使用构造函数模式来达到这个目的。第 6 章曾经讨论过，构造函数模式的缺点是针对每个实例都会创建同样一组新方法，而使用静态私有变量来实现特权方法就可以避免这个问题。

### 7.4.1 静态私有变量

通过在私有作用域中定义私有变量或函数，同样也可以创建特权方法，其基本模式如下所示。

```js
(function(){
  //私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){
    return false;
  }
  //构造函数
  MyObject = function(){
  };
  //公有/特权方法
  MyObject.prototype.publicMethod = function(){
    privateVariable++;
    return privateFunction();
  };
})();
```

这个模式创建了一个私有作用域，并在其中封装了一个构造函数及相应的方法。在私有作用域中，首先定义了私有变量和私有函数，然后又定义了构造函数及其公有方法。公有方法是在原型上定义的，这一点体现了典型的原型模式。需要注意的是，这个模式在定义构造函数时并没有使用函数声明，而是使用了函数表达式。函数声明只能创建局部函数，但那并不是我们想要的。出于同样的原因，我们也没有在声明 MyObject 时使用 var 关键字。记住：初始化未经声明的变量，总是会创建一个全局变量。因此， MyObject 就成了一个全局变量，能够在私有作用域之外被访问到。但也要知道，在严格模式下给未经声明的变量赋值会导致错误。

这个模式与在构造函数中定义特权方法的主要区别，就在于私有变量和函数是由实例共享的。由于特权方法是在原型上定义的，因此所有实例都使用同一个函数。而这个特权方法，作为一个闭包，总是保存着对包含作用域的引用。来看一看下面的代码。

```js
(function(){
  var name = "";
  Person = function(value){
    name = value;
  };
  Person.prototype.getName = function(){
    return name;
  };
  Person.prototype.setName = function (value){
    name = value;
  };
})();

var person1 = new Person("Nicholas");
alert(person1.getName()); //"Nicholas"
person1.setName("Greg");
alert(person1.getName()); //"Greg"

var person2 = new Person("Michael");
alert(person1.getName()); //"Michael"
alert(person2.getName()); //"Michael"
```

以这种方式创建静态私有变量会因为使用原型而增进代码复用，但每个实例都没有自己的私有变量。到底是使用实例变量，还是静态私有变量，最终还是要视你的具体需求而定。

### 7.4.2 模块模式

前面的模式是用于为自定义类型创建私有变量和特权方法的。而道格拉斯所说的模块模式（ module pattern）则是为单例创建私有变量和特权方法。所谓单例（ singleton），指的就是只有一个实例的对象。按照惯例， JavaScript 是以对象字面量的方式来创建单例对象的。

```js
var singleton = {
  name : value,
  method : function () {
    //这里是方法的代码
  }
};
```

模块模式通过为单例添加私有变量和特权方法能够使其得到增强，其语法形式如下：

```js
var singleton = function(){
  //私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){
    return false;
  }
  //特权/公有方法和属性
  return {
    publicProperty: true,
    publicMethod : function(){
      privateVariable++;
      return privateFunction();
    }
  };
}();
```

这个模块模式使用了一个返回对象的匿名函数。在这个匿名函数内部，首先定义了私有变量和函数。然后，将一个对象字面量作为函数的值返回。返回的对象字面量中只包含可以公开的属性和方法。由于这个对象是在匿名函数内部定义的，因此它的公有方法有权访问私有变量和函数。从本质上来讲，这个对象字面量定义的是单例的公共接口。这种模式在需要对单例进行某些初始化，同时又需要维护其私有变量时是非常有用的，例如：

```js
var application = function(){
  //私有变量和函数
  var components = new Array();
  //初始化
  components.push(new BaseComponent());
  //公共
  return {
    getComponentCount : function(){
      return components.length;
    },
    registerComponent : function(component){
      if (typeof component == "object"){
        components.push(component);
      }
    }
  };
}();
```

在 Web 应用程序中，经常需要使用一个单例来管理应用程序级的信息。这个简单的例子创建了一个用于管理组件的 application 对象。在创建这个对象的过程中，首先声明了一个私有的 components 数组，并向数组中添加了一个 BaseComponent 的新实例（在这里不需要关心 BaseComponent 的代码，我们只是用它来展示初始化操作）。而返回对象的` getComponentCount()`和 `registerComponent()`方法，都是有权访问数组 components 的特权方法。前者只是返回已注册的组件数目，后者用于注册新组件。

简言之，如果必须创建一个对象并以某些数据对其进行初始化，同时还要公开一些能够访问这些私有数据的方法，那么就可以使用模块模式。以这种模式创建的每个单例都是 Object 的实例，因为最终要通过一个对象字面量来表示它。事实上，这也没有什么；毕竟，单例通常都是作为全局对象存在的，我们不会将它传递给一个函数。因此，也就没有什么必要使用 instanceof 操作符来检查其对象类型了。

### 7.4.3 增强的模块模式

增强的模块模式，即在返回对象之前加入对其增强的代码，这个模式适合那些单例必须是某种类型的实例，同时还必须添加某些属性和（或）方法对其加以增强的情况。

```js
var singleton = function(){
  //私有变量和私有函数
  var privateVariable = 10;
  function privateFunction(){
    return false;
  }
  //创建对象
  var object = new CustomType();
  //添加特权/公有属性和方法
  object.publicProperty = true;
  object.publicMethod = function(){
    privateVariable++;
    return privateFunction();
  };
  //返回这个对象
  return object;
}();
```

如果前面演示模块模式的例子中的 application 对象必须是 BaseComponent 的实例，那么就可以使用以下代码。

```js
var application = function(){
  //私有变量和函数
  var components = new Array();
  //初始化
  components.push(new BaseComponent());
  //创建 application 的一个局部副本
  var app = new BaseComponent();
  //公共接口
  app.getComponentCount = function(){
    return components.length;
  };
  app.registerComponent = function(component){
    if (typeof component == "object"){
    components.push(component);
    }
  };
  //返回这个副本
  return app;
}();
```

在这个重写后的应用程序（ application）单例中，首先也是像前面例子中一样定义了私有变量。主要的不同之处在于命名变量 app 的创建过程，因为它必须是 BaseComponent 的实例。这个实例实际上是 application 对象的局部变量版。此后，我们又为 app 对象添加了能够访问私有变量的公有方法。最后一步是返回 app 对象，结果仍然是将它赋值给全局变量 application。

## 7.5 小结

在 JavaScript 编程中，函数表达式是一种非常有用的技术。使用函数表达式可以无须对函数命名，从而实现动态编程。匿名函数，也称为拉姆达函数，是一种使用 JavaScript 函数的强大方式。以下总结了函数表达式的特点。

+ 函数表达式不同于函数声明。函数声明要求有名字，但函数表达式不需要。没有名字的函数表达式也叫做匿名函数。
+ 在无法确定如何引用函数的情况下，递归函数就会变得比较复杂；
+ 递归函数应该始终使用 arguments.callee 来递归地调用自身，不要使用函数名——函数名可能会发生变化。

当在函数内部定义了其他函数时，就创建了闭包。闭包有权访问包含函数内部的所有变量，原理如下。

+ 在后台执行环境中，闭包的作用域链包含着它自己的作用域、包含函数的作用域和全局作用域。
+ 通常，函数的作用域及其所有变量都会在函数执行结束后被销毁。
+ 但是，当函数返回了一个闭包时，这个函数的作用域将会一直在内存中保存到闭包不存在为止。

使用闭包可以在 JavaScript 中模仿块级作用域（ JavaScript 本身没有块级作用域的概念），要点如下。

+ 创建并立即调用一个函数，这样既可以执行其中的代码，又不会在内存中留下对该函数的引用。
+ 结果就是函数内部的所有变量都会被立即销毁——除非将某些变量赋值给了包含作用域（即外部作用域）中的变量。

闭包还可以用于在对象中创建私有变量，相关概念和要点如下。

+ 即使 JavaScript 中没有正式的私有对象属性的概念，但可以使用闭包来实现公有方法，而通过公有方法可以访问在包含作用域中定义的变量。
+ 有权访问私有变量的公有方法叫做特权方法。
+ 可以使用构造函数模式、原型模式来实现自定义类型的特权方法，也可以使用模块模式、增强的模块模式来实现单例的特权方法。

JavaScript 中的函数表达式和闭包都是极其有用的特性，利用它们可以实现很多功能。不过，因为创建闭包必须维护额外的作用域，所以过度使用它们可能会占用大量内存。

# 第8章 BOM　

ECMAScript 是 JavaScript 的核心，但如果要在 Web 中使用 JavaScript，那么 BOM（浏览器对象模型）则无疑才是真正的核心。 BOM 提供了很多对象，用于访问浏览器的功能，这些功能与任何网页内容无关。多年来，缺少事实上的规范导致 BOM 既有意思又有问题，因为浏览器提供商会按照各自的想法随意去扩展它。于是，浏览器之间共有的对象就成为了事实上的标准。这些对象在浏览器中得以存在，很大程度上是由于它们提供了与浏览器的互操作性。 W3C 为了把浏览器中 JavaScript 最基本的部分标准化，已经将 BOM 的主要方面纳入了 HTML5 的规范中。

## 8.1 window对象 

BOM 的核心对象是 window，它表示浏览器的一个实例。在浏览器中， window 对象有双重角色，它既是通过 JavaScript 访问浏览器窗口的一个接口，又是 ECMAScript 规定的 Global 对象。这意味着在网页中定义的任何一个对象、变量和函数，都以 window 作为其 Global 对象，因此有权访问`parseInt()`等方法。

### 8.1.1 全局作用域

由于 window 对象同时扮演着 ECMAScript 中 Global 对象的角色，因此所有在全局作用域中声明的变量、函数都会变成 window 对象的属性和方法。

```js
var age = 29;
function sayAge(){
  alert(this.age);
}
alert(window.age); //29
sayAge(); //29
window.sayAge(); //29
```

定义全局变量与在 window 对象上直接定义属性还是有一点差别：全局变量不能通过 delete 操作符删除，而直接在 window 对象上的定义的属性可以。使用 var 语句添加的 window 属性有一个名为`[[Configurable]]`的特性，这个特性的值被设置为false，因此这样定义的属性不可以通过delete 操作符删除。

```js
var age = 29;
window.color = "red";
//在 IE < 9 时抛出错误，在其他所有浏览器中都返回 false
delete window.age;
//在 IE < 9 时抛出错误，在其他所有浏览器中都返回 true
delete window.color; //returns true
alert(window.age); //29
alert(window.color); //undefined
```

尝试访问未声明的变量会抛出错误，但是通过查询 window 对象，可以知道某个可能未声明的变量是否存在。

```js
//这里会抛出错误，因为 oldValue 未定义
var newValue = oldValue;
//这里不会抛出错误，因为这是一次属性查询
//newValue 的值是 undefined
var newValue = window.oldValue;
```

### 8.1.2 窗口关系及框架

如果页面中包含框架，则每个框架都拥有自己的 window 对象，并且保存在 frames 集合中。在 frames 集合中，可以通过数值索引（从 0 开始，从左至右，从上到下）或者框架名称来访问相应的 window 对象。每个 window 对象都有一个 name 属性，其中包含框架的名称。

```xml
<html>
  <head>
    <title>Frameset Example</title>
  </head>
  <frameset rows="160,*">
    <frame src="frame.htm" name="topFrame">
    <frameset cols="50%,50%">
      <frame src="anotherframe.htm" name="leftFrame">
      <frame src="yetanotherframe.htm" name="rightFrame">
    </frameset>
  </frameset>
</html>
```

### 8.1.3 窗口位置

用来确定和修改 window 对象位置的属性和方法有很多。 IE、 Safari、 Opera 和 Chrome 都提供了screenLeft 和 screenTop 属性，分别用于表示窗口相对于屏幕左边和上边的位置。 Firefox 则在screenX 和 screenY 属性中提供相同的窗口位置信息， Safari 和 Chrome 也同时支持这两个属性。

```js
var leftPos = (typeof window.screenLeft == "number") ?
  window.screenLeft : window.screenX;
var topPos = (typeof window.screenTop == "number") ?
  window.screenTop : window.screenY;
```

使用 `moveTo ()` 和 `moveBy ()` 方法可能将窗口精确地移动到一个新位置，这两个方法都接收两个参数，其中 `moveTo ()` 接收的新新位置的 x 和 y 坐标值，而 `moveBy ()` 接收的是在水平和垂直方向上移动的像素数。

### 8.1.4 窗口大小

跨浏览器确定一个窗口的大小不是一件简单的事。 IE9+、 Firefox、 Safari、 Opera 和 Chrome 均为此提供了 4 个属性： innerWidth、 innerHeight、 outerWidth 和 outerHeight。

使用 `resizeTo ()` 和 `resizeBy ()` 方法可以调整浏览器窗口的大小，这两个方法都接收两个参数，前者接收浏览器窗口的新宽度和新高度，而后者接收新窗口与原窗口的宽度和高度之差。需要注意的是，这两个方法与移动窗口位置的方法类似，也有可能被浏览器禁用。

```js
//调整到 100× 100
window.resizeTo(100, 100);
//调整到 200× 150
window.resizeBy(100, 50);
//调整到 300× 300
window.resizeTo(300, 300);
```

### 8.1.5 导航和打开窗口

使用 `window.open()`方法既可以导航到一个特定的 URL，也可以打开一个新的浏览器窗口。这个方法可以接收 4 个参数：要加载的 URL、窗口目标、一个特性字符串以及一个表示新页面是否取代浏览器历史记录中当前加载页面的布尔值。通常只须传递第一个参数，最后一个参数只在不打开新窗口的情况下使用。

```js
//等同于< a href="http://www.wrox.com" target="topFrame"></a>
window.open("http://www.wrox.com/", "topFrame");
```

### 8.1.6 间歇调用和超时调用

JavaScript 是单线程语言，但它允许通过设置超时值和间歇时间值来调度代码在特定的时刻执行。前者是在指定的时间过后执行代码，而后者则是每隔指定的时间就执行一次代码。

超时调用需要使用 window 对象的 `setTimeout()`方法，它接受两个参数：要执行的代码和以毫秒表示的时间（即在执行代码前需要等待多少毫秒）。其中，第一个参数可以是一个包含 JavaScript 代码的字符串（就和在 `eval()`函数中使用的字符串一样），也可以是一个函数。例如，下面对 `setTimeout()`的两次调用都会在一秒钟后显示一个警告框。

```js
//不建议传递字符串！
setTimeout("alert('Hello world!') ", 1000);

//推荐的调用方式
setTimeout(function() {
  alert("Hello world!");
}, 1000);
```

第二个参数是一个表示等待多长时间的毫秒数，但经过该时间后指定的代码不一定会执行。JavaScript 是一个单线程序的解释器，因此一定时间内只能执行一段代码。为了控制要执行的代码，就有一个 JavaScript 任务队列。这些任务会按照将它们添加到队列的顺序执行。 `setTimeout()`的第二个参数告诉 JavaScript 再过多长时间把当前任务添加到队列中。如果队列是空的，那么添加的代码会立即执行；如果队列不是空的，那么它就要等前面的代码执行完了以后再执行。

调用 `setTimeout()`之后，该方法会返回一个数值 ID，表示超时调用。这个超时调用 ID 是计划执行代码的唯一标识符，可以通过它来取消超时调用。要取消尚未执行的超时调用计划，可以调用`clearTimeout()`方法并将相应的超时调用 ID 作为参数传递给它

```js
//设置超时调用
var timeoutId = setTimeout(function() {
  alert("Hello world!");
}, 1000);

//注意：把它取消
clearTimeout(timeoutId);
```

间歇调用与超时调用类似，只不过它会按照指定的时间间隔重复执行代码，直至间歇调用被取消或者页面被卸载。设置间歇调用的方法是 `setInterval()`，它接受的参数与 `setTimeout()`相同：要执行的代码（字符串或函数）和每次执行之前需要等待的毫秒数。

```js
//不建议传递字符串！
setInterval ("alert('Hello world!') ", 10000);
//推荐的调用方式
setInterval (function() {
  alert("Hello world!");
}, 10000);
```

调用 setInterval()方法同样也会返回一个间歇调用 ID，该 ID 可用于在将来某个时刻取消间歇调用。要取消尚未执行的间歇调用，可以使用 clearInterval()方法并传入相应的间歇调用 ID。取消间歇调用的重要性要远远高于取消超时调用，因为在不加干涉的情况下，间歇调用将会一直执行到页面卸载。

```js
var num = 0;
var max = 10;
var intervalId = null;
function incrementNumber() {
  num++;
  //如果执行次数达到了 max 设定的值，则取消后续尚未执行的调用
  if (num == max) {
    clearInterval(intervalId);
    alert("Done");
  }
}
intervalId = setInterval(incrementNumber, 500);
```

在使用超时调用时，没有必要跟踪超时调用 ID，因为每次执行代码之后，如果不再设置另一次超时调用，调用就会自行停止。一般认为，使用超时调用来模拟间歇调用的是一种最佳模式。在开发环境下，很少使用真正的间歇调用，原因是后一个间歇调用可能会在前一个间歇调用结束之前启动。而像前面示例中那样使用超时调用，则完全可以避免这一点。所以，最好不要使用间歇调用。

```js
var num = 0;
var max = 10;
function incrementNumber() {
  num++;
  //如果执行次数未达到 max 设定的值，则设置另一次超时调用
  if (num < max) {
    setTimeout(incrementNumber, 500);
  } else {
    alert("Done");
  }
}
  setTimeout(incrementNumber, 500);
```

### 8.1.7 系统对话框

浏览器通过 `alert()`、 `confirm()`和 `prompt()`方法可以调用系统对话框向用户显示消息。系统对话框与在浏览器中显示的网页没有关系，也不包含 HTML。它们的外观由操作系统及（或）浏览器设置决定，而不是由 CSS 决定。此外，通过这几个方法打开的对话框都是同步和模态的。也就是说，显示这些对话框的时候代码会停止执行，而关掉这些对话框后代码又会恢复执行。

```js
if (confirm("Are you sure?")) {
  alert("I'm so glad you're sure! ");
} else {
  alert("I'm sorry to hear you're not sure. ");
}
```

最后一种对话框是通过调用 `prompt()`方法生成的，这是一个“提示”框，用于提示用户输入一些文本。提示框中除了显示 OK 和 Cancel 按钮之外，还会显示一个文本输入域，以供用户在其中输入内容。`prompt()`方法接受两个参数：要显示给用户的文本提示和文本输入域的默认值（可以是一个空字符串）。

```js
var result = prompt("What is your name? ", "");
if (result !== null) {
  alert("Welcome, " + result);
}
```

综上所述，这些系统对话框很适合向用户显示消息并请用户作出决定。由于不涉及 HTML、 CSS 或JavaScript，因此它们是增强 Web 应用程序的一种便捷方式。

还有两个可以通过 JavaScript 打开的对话框，即“查找”和“打印”。这两个对话框都是异步显示的，能够将控制权立即交还给脚本。这两个对话框与用户通过浏览器菜单的“查找”和“打印”命令打开的对话框相同。而在 JavaScript 中则可以像下面这样通过 window 对象的 `find()`和 `print()`方法打开它们。

```js
//显示“打印”对话框
window.print();
//显示“查找”对话框
window.find();
```

## 8.2 location对象 

location 是最有用的 BOM 对象之一，它提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能。事实上， location 对象是很特别的一个对象，因为它既是 window 对象的属性，也是document 对象的属性；换句话说， `window.location` 和 `document.location` 引用的是同一个对象。location 对象的用处不只表现在它保存着当前文档的信息，还表现在它将 URL 解析为独立的片段，让开发人员可以通过不同的属性访问这些片段。

下表列出了 location 对象的所有属性（注：省略了每个属性前面的 location 前缀）。

|  属性名  |         例子         |                                    说明                                     |
| -------- | -------------------- | --------------------------------------------------------------------------- |
| hash     | "#contents"          | 返回URL中的hash（#号后跟零或多个字符），如果URL中不包含散列，则返回空字符串 |
| host     | "www.wrox.com:80"    | 返回服务器名称和端口号（如果有）                                            |
| hostname | "www.wrox.com"       | 返回不带端口号的服务器名称                                                  |
| href     | "http:/www.wrox.com" | 返回当前加载页面的完整URL。而location对象的`toString()`方法也返回这个值     |
| pathname | "/WileyCDA/"         | 返回URL中的目录和（或）文件名                                               |
| port     | "8080"               | 返回URL中指定的端口号。如果URL中不包含端口号，则这个属性返回空字符串        |
| protocol | "http:"              | 返回页面使用的协议。通常是http:或https:                                     |
| search   | "?q=javascript"      | 返回URL的查询字符串。这个字符串以问号开头                                   |

### 8.2.1 查询字符串参数

尽管 `location.search` 返回从问号到 URL 末尾的所有内容，但却没有办法逐个访问其中的每个查询字符串参数。为此，可以像下面这样创建一个函数，用以解析查询字符串，然后返回包含所有参数的一个对象。

```js
function getQueryStringArgs(){
  //取得查询字符串并去掉开头的问号
  var qs = (location.search.length > 0 ? location.search.substring(1) : ""),
  //保存数据的对象
  args = {},
  //取得每一项
  items = qs.length ? qs.split("&") : [],
  item = null,
  name = null,
  value = null,
  //在 for 循环中使用
  i = 0,
  len = items.length;
  //逐个将每一项添加到 args 对象中
  for (i=0; i < len; i++){
  item = items[i].split("=");
  name = decodeURIComponent(item[0]);
  value = decodeURIComponent(item[1]);
  if (name.length) {
  args[name] = value;
  }
  }
  return args;
}
```

### 8.2.2 位置操作

使用 location 对象可以通过很多方式来改变浏览器的位置。首先，也是最常用的方式，就是使用`assign()`方法并为其传递一个 URL。这样，就可以立即打开新 URL 并在浏览器的历史记录中生成一条记录。如果是将 `location.href` 或 `window.location` 设置为一个 URL 值，也会以该值调用 `assign()`方法。

```js
location.assign("http://www.wrox.com");
// 等价于
window.location = "http://www.wrox.com";
location.href = "http://www.wrox.com";
```

另外，修改location 对象的其他属性也可以改变当前加载的页面。每次修改 location 的属性（hash 除外），页面都会以新 URL 重新加载。

```js
//假设初始 URL 为 http://www.wrox.com/WileyCDA/
//将 URL 修改为"http://www.wrox.com/WileyCDA/#section1"
location.hash = "#section1";
//将 URL 修改为"http://www.wrox.com/WileyCDA/?q=javascript"
location.search = "?q=javascript";
//将 URL 修改为"http://www.yahoo.com/WileyCDA/"
location.hostname = "www.yahoo.com";
//将 URL 修改为"http://www.yahoo.com/mydir/"
location.pathname = "mydir";
//将 URL 修改为"http://www.yahoo.com:8080/WileyCDA/"
location.port = 8080;
```

当通过上述任何一种方式修改 URL 之后，浏览器的历史记录中就会生成一条新记录，因此用户通过单击“后退”按钮都会导航到前一个页面。要禁用这种行为，可以使用 `replace()`方法。这个方法只接受一个参数，即要导航到的 URL；结果虽然会导致浏览器位置改变，但不会在历史记录中生成新记录。在调用 `replace()`方法之后，用户不能回到前一个页面。

```js
<!DOCTYPE html>
<html>
  <head>
    <title>You won't be able to get back here</title>
  </head>
  <body>
    <p>Enjoy this page for a second, because you won't be coming back here.</p>
    <script type="text/javascript">
      setTimeout(function () {
        location.replace("http://www.wrox.com/");
      }, 1000);
    </script>
  </body>
</html>
```

与位置有关的最后一个方法是 `reload()`，作用是重新加载当前显示的页面。如果调用 `reload()`时不传递任何参数，页面就会以最有效的方式重新加载。也就是说，如果页面自上次请求以来并没有改变过，页面就会从浏览器缓存中重新加载。如果要强制从服务器重新加载，则需要像下面这样为该方法传递参数 true。

```js
location.reload(); //重新加载（有可能从缓存中加载）
location.reload(true); //重新加载（从服务器重新加载）
```

## 8.3 navigator对象

检测浏览器中是否安装了特定的插件是一种最常见的检测例程。可以使用 plugins 数组来达到目标，一般来说 name 属性会包含检测插件所需的信息，但有时候需要循环迭代并比较。典型的做法是针对每个插件分别创建检测函数，而不是使用前面通用的检测方法。

两个方法，可以让一个站点指明它可以处理特定类型的信息，它们是 registerContentHandler () 和 registerProtoolHandel ()。

## 8.4 screen对象 

screen 对象基本上只用来表明客户端的能力，其中包括浏览器窗口外部的显示器的信息，如像素宽度和高度等。

## 8.5 history对象

History 对象保存着用户上网的历史记录，从窗口被打开的那一刻算起，每个特定的 window 对象都与自己的 History 对象关联，开发人员无法得知用户浏览过的 URL 但是可以实现后退前进功能。使用 go () 方法可以在用户的历史记录中任意跳转，可以向后也可以向前，这个方法接受一个参数，表示向后或向前跳转的页面数的一个整数值。也可以使用 go () 方法传递一个字符串参数，此时浏览器会跳转到历史记录中包含该字符串的第一个位置——可能后退，也可能前进，具体要看哪个位置最近。还可以使用两个简写方法 back () 和 forward () 来代替 go () 代替后退和前进。除了上述几个方法外，history 对象还有一个l ength 属性，保存着历史记录的数量。如果等于 0，那么就是加载到窗口、标签页或框架中的第一个页面。

8.6　小结

# 第9章 客户端检测

每一种浏览器都有着各自的缺点，开发人员要么采取迁就各方的“最小公分母”策略，要么就得利用各种客户端检测方法，来突破或者规避种种局限性。

## 9.1 能力检测 

最常用也是最为人们广泛接受的客户端检测形式是能力检测，又称特性检测。先检测达成目的的最常用的特性，然后测试实际要用到的特性。

## 9.2 怪癖检测

怪癖检测的目标是识别浏览器的特殊行为，想要知道浏览器存在什么缺陷（bug）。

## 9.3 用户代理检测

用户代理检测通过检测用户代理字符串来确定实际使用的浏览器，在服务端通过用户代理字符串来确定用户使用的浏览器是常见并且广为接受的做法，但是在客户端它的优先级在能力检测和（或）怪癖检测之后。识别呈现引擎、识别JavaScript 引擎、识别平台、识别 windows 操作系统、识别移动设备，构成了用户代理字符串检测脚本的内容。这种方法对用户代理字符串具有很强的依赖性，是客户端检测的最后一种方案。

9.4 小结

# 第10章 DOM　

DOM（文档对象模型）是针对 HTML 和 XML 文档的一个 API（应用程序编程接口）。 DOM 描绘了一个层次化的节点树，允许开发人员添加、移除和修改页面的某一部分。 DOM 脱胎于 Netscape 及微软公司创始的 DHTML（动态 HTML），但现在它已经成为表现和操作页面标记的真正的跨平台、语言中立的方式。

1998 年 10 月 DOM1 级规范成为 W3C 的推荐标准，为基本的文档结构及查询提供了接口。本章主要讨论与浏览器中的 HTML 页面相关的 DOM1 级的特性和应用，以及 JavaScript 对 DOM1 级的实现。IE、 Firefox、 Safari、 Chrome 和 Opera 都非常完善地实现了 DOM。

> 注意， IE 中的所有 DOM 对象都是以 COM 对象的形式实现的。这意味着 IE 中的 DOM 对象与原生 JavaScript 对象的行为或活动特点并不一致。本章将较多地谈及这些差异。

## 10.1 节点层次 

DOM 可以将任何 HTML 或 XML 文档描绘成一个由多层节点构成的结构。节点分为几种不同的类型，每种类型分别表示文档中不同的信息及（或）标记。每个节点都拥有各自的特点、数据和方法，另外也与其他节点存在某种关系。节点之间的关系构成了层次，而所有页面标记则表现为一个以特定节点为根节点的树形结构。以下面的 HTML 为例：

```html
<html>
  <head>
    <title>Sample Page</title>
  </head>
  <body>
    <p>Hello World!</p>
  </body>
</html>
```

文档节点是每个文档的根节点。在这个例子中，文档节点只有一个子节点，即`<html>`元素，我们称之为文档元素。文档元素是文档的最外层元素，文档中的其他所有元素都包含在文档元素中。每个文档只能有一个文档元素。在 HTML 页面中，文档元素始终都是`<html>`元素。在 XML 中，没有预定义的元素，因此任何元素都可能成为文档元素。

每一段标记都可以通过树中的一个节点来表示： HTML 元素通过元素节点表示，特性（attribute）通过特性节点表示，文档类型通过文档类型节点表示，而注释则通过注释节点表示。总共有 12 种节点类型，这些类型都继承自一个基类型。

### 10.1.1 Node类型

DOM1 级定义的一个 Node 接口，该接口将由 DOM 中的所有节点类型实现，这个接口在 JavaScript 中是作为 Node 类型实现的。JavaScript中的所有节点类型都继承自 Node 类型，因此所有节点类型都共享者相同的基本属性和方法。

每个节点都有一个 nodeType 属性，用于表明节点的类型。节点类型由在 Node 类型中定义的下列 12 个数值常量来表示，任何节点类型必居其一：

- Node.ELEMENT_NODE(1)；
- Node.ATTRIBUTE_NODE(2)；
- Node.TEXT_NODE(3)；
- Node.CDATA_SECTION_NODE(4)；
- Node.ENTITY_REFERENCE_NODE(5)；
- Node.ENTITY_NODE(6)；
- Node.PROCESSING_INSTRUCTION_NODE(7)；
- Node.COMMENT_NODE(8)；
- Node.DOCUMENT_NODE(9)；
- Node.DOCUMENT_TYPE_NODE(10)；
- Node.DOCUMENT_FRAGMENT_NODE(11)；
- Node.NOTATION_NODE(12)。

通过比较上面这些常量，可以很容易地确定节点的类型，例如：

```js
if (someNode.nodeType == Node.ELEMENT_NODE){ //在 IE 中无效
  alert("Node is an element.");
}
```

由于 IE 没有公开 Node 类型的构造函数，因此上面的代码在 IE 中会导致错误。为了确保跨浏览器兼容，最好还是将 nodeType 属性与数字值进行比较，如下所示：

```js
if (someNode.nodeType == 1){ //适用于所有浏览器
  alert("Node is an element.");
}
```

并不是所有节点类型都受到 Web 浏览器的支持。开发人员最常用的就是元素和文本节点。本章后面将详细讨论每个节点类型的受支持情况及使用方法。

**1. nodeName 和 nodeValue 属性**

要了解节点的具体信息，可以使用 nodeName 和 nodeValue 这两个属性。这两个属性的值完全取决于节点的类型。在使用这两个值以前，最好是像下面这样先检测一下节点的类型。

```js
if (someNode.nodeType == 1){
  value = someNode.nodeName; //nodeName 的值是元素的标签名
}
```

在这个例子中，首先检查节点类型，看它是不是一个元素。如果是，则取得并保存 nodeName 的值。对于元素节点， nodeName 中保存的始终都是元素的标签名，而 nodeValue 的值则始终为 null。

**2. 节点关系**

文档中所有的节点之间都存在这样或那样的关系。节点间的各种关系可以用传统的家族关系来描述，相当于把文档树比喻成家谱。在 HTML 中，可以将`<body>`元素看成是`<html>`元素的子元素；相应地，也就可以将`<html>`元素看成是`<body>`元素的父元素。而`<head>`元素，则可以看成是`<body>`元素的同胞元素，因为它们都是同一个父元素`<html>`的直接子元素。

每个节点都有一个 childNodes 属性，其中保存着一个 NodeList 对象。 NodeList 是一种类数组对象，用于保存一组有序的节点，可以通过位置来访问这些节点。请注意，虽然可以通过方括号语法来访问 NodeList 的值，而且这个对象也有 length 属性，但它并不是 Array 的实例。 NodeList 对象的独特之处在于，它实际上是基于 DOM 结构动态执行查询的结果，因此 DOM 结构的变化能够自动反映在 NodeList 对象中。我们常说， NodeList 是有生命、有呼吸的对象，而不是在我们第一次访问它们的某个瞬间拍摄下来的一张快照。

下面的例子展示了如何访问保存在 NodeList 中的节点——可以通过方括号，也可以使用`item()`方法。

```js
var firstChild = someNode.childNodes[0];
var secondChild = someNode.childNodes.item(1);
var count = someNode.childNodes.length;
```

无论使用方括号还是使用`item()`方法都没有问题，但使用方括号语法看起来与访问数组相似，因此颇受一些开发人员的青睐。另外，要注意 length 属性表示的是访问 NodeList 的那一刻，其中包含的节点数量。我们在本书前面介绍过，对 arguments 对象使用`Array.prototype.slice()`方法可以将其转换为数组。而采用同样的方法，也可以将 NodeList 对象转换为数组。来看下面的例子：

```js
//在 IE8 及之前版本中无效
var arrayOfNodes = Array.prototype.slice.call(someNode.childNodes, 0);
```

除 IE8 及更早版本之外，这行代码能在任何浏览器中运行。由于 IE8 及更早版本将 NodeList 实现为一个 COM 对象，而我们不能像使用 JScript 对象那样使用这种对象，因此上面的代码会导致错误。要想在 IE 中将 NodeList 转换为数组，必须手动枚举所有成员。下列代码在所有浏览器中都可以运行：

```js
function convertToArray(nodes){
  var array = null;
  try { 
    array = Array.prototype.slice.call(nodes, 0); //针对非 IE 浏览器
  } catch (ex) {
    array = new Array();
    for (var i = 0, len = nodes.length; i < len; i++){
      array.push(nodes[i]);
    }
  }
  return array;
}
```

每个节点都有一个 parentNode 属性，该属性指向文档树中的父节点。包含在 childNodes 列表中的所有节点都具有相同的父节点，因此它们的 parentNode 属性都指向同一个节点。此外，包含在 childNodes 列表中的每个节点相互之间都是同胞节点。通过使用列表中每个节点的 previousSibling 和 nextSibling 属性，可以访问同一列表中的其他节点。列表中第一个节点的 previousSibling 属性值为 null，而列表中最后一个节点的 nextSibling 属性的值同样也为 null，如下面的例子所示：

```js
if (someNode.nextSibling === null){
  alert("Last node in the parent’s childNodes list.");
} else if (someNode.previousSibling === null){
  alert("First node in the parent’s childNodes list.");
}
```

当然，如果列表中只有一个节点，那么该节点的 nextSibling 和 previousSibling 都为 null。

父节点与其第一个和最后一个子节点之间也存在特殊关系。父节点的 firstChild 和  lastChild 属性分别指向其 childNodes 列表中的第一个和最后一个节点。其中，`someNode.firstChild` 的值始终等于`someNode.childNodes[0]`，而`someNode.lastChild`的值始终等于`someNode.childNodes[someNode.childNodes.length-1]`。在只有一个子节点的情况下， firstChild 和lastChild 指向同一个节点。如果没有子节点，那么 firstChild 和 lastChild 的值均为 null。明确这些关系能够对我们查找和访问文档结构中的节点提供极大的便利。图 10-2 形象地展示了上述关系。

在反映这些关系的所有属性当中， childNodes 属性与其他属性相比更方便一些，因为只须使用简单的关系指针，就可以通过它访问文档树中的任何节点。另外，`hasChildNodes()`也是一个非常有用的方法，这个方法在节点包含一或多个子节点的情况下返回 true；应该说，这是比查询 childNodes 列表的 length 属性更简单的方法。

所有节点都有的最后一个属性是 ownerDocument ，该属性指向表示整个文档的文档节点。这种关系表示的是任何节点都属于它所在的文档，任何节点都不能同时存在于两个或更多个文档中。通过这个属性，我们可以不必在节点层次中通过层层回溯到达顶端，而是可以直接访问文档节点。

> 虽然所有节点类型都继承自 Node，但并不是每种节点都有子节点。本章后面将会讨论不同节点类型之间的差异。

**3. 操作节点**

因为关系指针都是只读的，所以 DOM 提供了一些操作节点的方法。其中，最常用的方法是`appendChild()`，用于向 childNodes 列表的末尾添加一个节点。添加节点后， childNodes 的新增节点、父节点及以前的最后一个子节点的关系指针都会相应地得到更新。更新完成后， `appendChild()`返回新增的节点。来看下面的例子：

```js
var returnedNode = someNode.appendChild(newNode);
alert(returnedNode == newNode); //true
alert(someNode.lastChild == newNode); //true
```

如果传入到 `appendChild()`中的节点已经是文档的一部分了，那结果就是将该节点从原来的位置转移到新位置。即使可以将 DOM 树看成是由一系列指针连接起来的，但任何 DOM 节点也不能同时出现在文档中的多个位置上。因此，如果在调用 `appendChild()`时传入了父节点的第一个子节点，那么该节点就会成为父节点的最后一个子节点，如下面的例子所示。

```js
// someNode 有多个子节点
var returnedNode = someNode.appendChild(someNode.firstChild);
alert(returnedNode == someNode.firstChild); // false
alert(returnedNode == someNode.lastChild); // true
```

如果需要把节点放在 childNodes 列表中某个特定的位置上，而不是放在末尾，那么可以使用`insertBefore()`方法。这个方法接受两个参数：要插入的节点和作为参照的节点。插入节点后，被插入的节点会变成参照节点的前一个同胞节点（previousSibling），同时被方法返回。如果参照节点是null，则 `insertBefore()`与 `appendChild()`执行相同的操作，如下面的例子所示。

```js
// 插入后成为最后一个子节点
returnedNode = someNode.insertBefore(newNode, null);
alert(newNode == someNode.lastChild); //true

// 插入后成为第一个子节点
var returnedNode = someNode.insertBefore(newNode, someNode.firstChild);
alert(returnedNode == newNode); //true
alert(newNode == someNode.firstChild); //true

// 插入到最后一个子节点前面
returnedNode = someNode.insertBefore(newNode, someNode.lastChild);
alert(newNode == someNode.childNodes[someNode.childNodes.length-2]); //true
```

前面介绍的 `appendChild()`和 `insertBefore()`方法都只插入节点，不会移除节点。而下面要介绍的 `replaceChild()`方法接受的两个参数是：要插入的节点和要替换的节点。要替换的节点将由这个方法返回并从文档树中被移除，同时由要插入的节点占据其位置。来看下面的例子。

```js
//替换第一个子节点
var returnedNode = someNode.replaceChild(newNode, someNode.firstChild);

//替换最后一个子节点
returnedNode = someNode.replaceChild(newNode, someNode.lastChild);
```

在使用`replaceChild()`插入一个节点时，该节点的所有关系指针都会从被它替换的节点复制过来。尽管从技术上讲，被替换的节点仍然还在文档中，但它在文档中已经没有了自己的位置。

如果只想移除而非替换节点，可以使用`removeChild()`方法。这个方法接受一个参数，即要移除的节点。被移除的节点将成为方法的返回值，如下面的例子所示。

```js
// 移除第一个子节点
var formerFirstChild = someNode.removeChild(someNode.firstChild);

// 移除最后一个子节点
var formerLastChild = someNode.removeChild(someNode.lastChild);
```

与使用`replaceChild()`方法一样，通过`removeChild()`移除的节点仍然为文档所有，只不过在文档中已经没有了自己的位置。

前面介绍的四个方法操作的都是某个节点的子节点，也就是说，要使用这几个方法必须先取得父节点（使用 parentNode 属性）。另外，并不是所有类型的节点都有子节点，如果在不支持子节点的节点上调用了这些方法，将会导致错误发生。

**4. 其他方法**

有两个方法是所有类型的节点都有的。第一个就是`cloneNode()`，用于创建调用这个方法的节点的一个完全相同的副本。`cloneNode()`方法接受一个布尔值参数，表示是否执行深复制。在参数为 true 的情况下，执行深复制，也就是复制节点及其整个子节点树；在参数为 false 的情况下，执行浅复制，即只复制节点本身。复制后返回的节点副本属于文档所有，但并没有为它指定父节点。因此，这个节点副本就成为了一个“孤儿”，除非通过 `appendChild()`、 `insertBefore()`或 `replaceChild()`将它添加到文档中。例如，假设有下面的 HTML 代码。

```html
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
```

如果我们已经将`<ul>`元素的引用保存在了变量 myList 中，那么通常下列代码就可以看出使用`cloneNode()`方法的两种模式。

```js
var deepList = myList.cloneNode(true);
alert(deepList.childNodes.length); // 3（ IE < 9）或 7（其他浏览器）

var shallowList = myList.cloneNode(false);
alert(shallowList.childNodes.length); // 0
```

在这个例子中， deepList 中保存着一个对 myList 执行深复制得到的副本。因此， deepList 中包含 3 个列表项，每个列表项中都包含文本。而变量 shallowList 中保存着对 myList 执行浅复制得到的副本，因此它不包含子节点。` deepList.childNodes.length` 中的差异主要是因为 IE8 及更早版本与其他浏览器处理空白字符的方式不一样。 IE9 之前的版本不会为空白符创建节点。

> `cloneNode()`方法不会复制添加到 DOM 节点中的 JavaScript 属性，例如事件处理程序等。这个方法只复制特性、（在明确指定的情况下也复制）子节点，其他一切都不会复制。 IE 在此存在一个 bug，即它会复制事件处理程序，所以我们建议在复制之前最好先移除事件处理程序。

我们要介绍的最后一个方法是`normalize()`，这个方法唯一的作用就是处理文档树中的文本节点。由于解析器的实现或 DOM 操作等原因，可能会出现文本节点不包含文本，或者接连出现两个文本节点的情况。当在某个节点上调用这个方法时，就会在该节点的后代节点中查找上述两种情况。如果找到了空文本节点，则删除它；如果找到相邻的文本节点，则将它们合并为一个文本节点。本章后面还将进一步讨论这个方法。

### 10.1.2 Document类型

JavaScript 通过 Document 类型表示文档。在浏览器中， document 对象是 HTMLDocument（继承自 Document 类型）的一个实例，表示整个 HTML 页面。而且， document 对象是 window 对象的一个属性，因此可以将其作为全局对象来访问。 Document 节点具有下列特征：

- nodeType 的值为 9；
- nodeName 的值为"#document"；
- nodeValue 的值为 null；
- parentNode 的值为 null；
- ownerDocument 的值为 null；
- 其子节点可能是一个 DocumentType（最多一个）、 Element（最多一个）、 ProcessingInstruction 或 Comment。

Document 类型可以表示 HTML 页面或者其他基于 XML 的文档。不过，最常见的应用还是作为 HTMLDocument 实例的 document 对象。通过这个文档对象，不仅可以取得与页面有关的信息，而且还能操作页面的外观及其底层结构。

> 在 Firefox、 Safari、 Chrome 和 Opera 中，可以通过脚本访问 Document 类型的构造函数和原型。 但在所有浏览器中都可以访问 HTMLDocument 类型的构造函数和原型，包括 IE8 及后续版本。

**1. 文档的子节点**

虽然 DOM 标准规定 Document 节点的子节点可以是 DocumentType、 Element、 ProcessingInstruction 或 Comment，但还有两个内置的访问其子节点的快捷方式。 第一个就是 documentElement 属性，该属性始终指向 HTML 页面中的`<html>`元素。另一个就是通过 childNodes 列表访问文档元素，但通过 documentElement 属性则能更快捷、更直接地访问该元素。以下面这个简单的页面为例。

```js
<html>
  <body>
  </body>
</html>
```

这个页面在经过浏览器解析后，其文档中只包含一个子节点，即`<html>`元素。可以通过 documentElement 或 childNodes 列表来访问这个元素，如下所示。

```js
var html = document.documentElement; // 取得对<html>的引用
alert(html === document.childNodes[0]); // true
alert(html === document.firstChild); // true
```

这个例子说明， documentElement、 firstChild 和 childNodes[0]的值相同，都指向`<html>`元素。

作为 HTMLDocument 的实例， document 对象还有一个 body 属性，直接指向`<body>`元素。因为开发人员经常要使用这个元素，所以`document.body`在 JavaScript 代码中出现的频率非常高，其用法如下。

```js
var body = document.body; //取得对<body>的引用
```

所有浏览器都支持 `document.documentElement` 和 `document.body` 属性。

Document 另一个可能的子节点是 DocumentType 。通常将`<!DOCTYPE>`标签看成一个与文档其他部分不同的实体，可以通过 doctype 属性（在浏览器中是 document.doctype）来访问它的信息。

```js
var doctype = document.doctype; //取得对<!DOCTYPE>的引用
```

浏览器对 document.doctype 的支持差别很大，可以给出如下总结。

- IE8 及之前版本：如果存在文档类型声明，会将其错误地解释为一个注释并把它当作 Comment 节点；而`document.doctype` 的值始终为 null。
- IE9+及 Firefox：如果存在文档类型声明，则将其作为文档的第一个子节点；`document.doctype`是一个 DocumentType 节点，也可以通过`document.firstChild` 或 `document.childNodes[0]`访问同一个节点。
- Safari、 Chrome 和 Opera：如果存在文档类型声明，则将其解析，但不作为文档的子节点。`document.doctype` 是一个 DocumentType 节点，但该节点不会出现在 document.childNodes 中。

由于浏览器对`document.doctype` 的支持不一致，因此这个属性的用处很有限。

从技术上说，出现在`<html>`元素外部的注释应该算是文档的子节点。然而，不同的浏览器在是否解析这些注释以及能否正确处理它们等方面，也存在很大差异。以下面简单的 HTML 页面为例。

```html
<!--第一条注释 -->
<html>
  <body>
  </body>
</html>
<!--第二条注释 -->
```

看起来这个页面应该有 3 个子节点：注释、`<html>`元素、注释。从逻辑上讲，我们会认为`document.childNodes`中应该包含与这 3 个节点对应的 3 项。但是，现实中的浏览器在处理位于`<html>`外部的注释方面存在如下差异。

- IE8 及之前版本、 Safari 3.1 及更高版本、 Opera 和 Chrome 只为第一条注释创建节点，不为第二条注释创建节点。结果，第一条注释就会成为`document.childNodes`中的第一个子节点。
- IE9 及更高版本会将第一条注释创建为`document.childNodes`中的一个注释节点，也会将第二条注释创建为`document.childNodes`中的注释子节点。
- Firefox 以及 Safari 3.1 之前的版本会完全忽略这两条注释。

同样，浏览器间的这种不一致性也导致了位于`<html>`元素外部的注释没有什么用处。

多数情况下，我们都用不着在 document 对象上调用`appendChild()`、`removeChild()`和`replaceChild()`方法，因为文档类型（如果存在的话）是只读的，而且它只能有一个元素子节点（该节点通常早就已经存在了）。

**2. 文档信息**

作为 HTMLDocument 的一个实例， document 对象还有一些标准的 Document 对象所没有的属性。这些属性提供了 document 对象所表现的网页的一些信息。其中第一个属性就是 title，包含着`<title>`元素中的文本——显示在浏览器窗口的标题栏或标签页上。通过这个属性可以取得当前页面的标题，也可以修改当前页面的标题并反映在浏览器的标题栏中。修改 title 属性的值不会改变`<title>`元素。来看下面的例子。

```js
//取得文档标题
var originalTitle = document.title;
//设置文档标题
document.title = "New page title";
```

接下来要介绍的 3 个属性都与对网页的请求有关，它们是 URL、 domain 和 referrer。 URL 属性中包含页面完整的 URL（即地址栏中显示的 URL）， domain 属性中只包含页面的域名，而 referrer 属性中则保存着链接到当前页面的那个页面的 URL。在没有来源页面的情况下， referrer 属性中可能会包含空字符串。所有这些信息都存在于请求的 HTTP 头部，只不过是通过这些属性让我们能够在JavaScrip 中访问它们而已，如下面的例子所示。

```js
//取得完整的 URL
var url = document.URL;
//取得域名
var domain = document.domain;
//取得来源页面的 URL
var referrer = document.referrer;
```

URL 与 domain 属性是相互关联的。例如，如果 document.URL 等于`http://www.wrox.com/WileyCDA/`，那么 document.domain 就等于`www.wrox.com`。

在这 3 个属性中，只有 domain 是可以设置的。但由于安全方面的限制，也并非可以给 domain 设置任何值。 如果 URL 中包含一个子域名，例如 `p2p.wrox.com`，那么就只能将 domain 设置为"wrox.com"（ URL 中包含"www"，如 www.wrox.com 时，也是如此）。不能将这个属性设置为 URL 中不包含的域，如下面的例子所示。

```js
// 假设页面来自 p2p.wrox.com 域
document.domain = "wrox.com"; // 成功
document.domain = "nczonline.net"; // 出错！
```

当页面中包含来自其他子域的框架或内嵌框架时，能够设置 `document.domain` 就非常方便了。由于跨域安全限制，来自不同子域的页面无法通过 JavaScript 通信 。 而通过将每个页面的`document.domain`设置为相同的值，这些页面就可以互相访问对方包含的 JavaScript 对象了。例如，假设有一个页面加载自 www.wrox.com，其中包含一个内嵌框架，框架内的页面加载自 p2p.wrox.com。由于 `document.domain` 字符串不一样，内外两个页面之间无法相互访问对方的 JavaScript 对象。但如果将这两个页面的 `document.domain` 值都设置为"wrox.com"，它们之间就可以通信了。

浏览器对 domain 属性还有一个限制，即如果域名一开始是“松散的”（ loose），那么不能将它再设置为“紧绷的”（ tight）。换句话说，在将 `document.domain` 设置为"wrox.com"之后，就不能再将其设置回"p2p.wrox.com"，否则将会导致错误，如下面的例子所示。

```js
// 假设页面来自于 p2p.wrox.com 域
document.domain = "wrox.com"; // 松散的（成功）
document.domain = "p2p.wrox.com"; // 紧绷的（出错！）
```

所有浏览器中都存在这个限制，但 IE8 是实现这一限制的最早的 IE 版本。

**3. 查找元素**

说到最常见的 DOM 应用， 恐怕就要数取得特定的某个或某组元素的引用，然后再执行一些操作了。取得元素的操作可以使用 document 对象的几个方法来完成。其中， Document 类型为此提供了两个方法： `getElementById()`和 `getElementsByTagName()`。

第一个方法， `getElementById()`，接收一个参数：要取得的元素的 ID。如果找到相应的元素则返回该元素，如果不存在带有相应 ID 的元素，则返回 null。注意，这里的 ID 必须与页面中元素的 id 特性（attribute）严格匹配，包括大小写。以下面的元素为例。

```html
<div id="myDiv">Some text</div>
```

可以使用下面的代码取得这个元素：

```js
var div = document.getElementById("myDiv"); //取得<div>元素的引用
```

但是，下面的代码在除 IE7 及更早版本之外的所有浏览器中都将返回 null。

```js
var div = document.getElementById("mydiv"); //无效的 ID（在 IE7 及更早版本中可以）
```

IE8 及较低版本不区分 ID 的大小写，因此"myDiv"和"mydiv"会被当作相同的元素 ID。

如果页面中多个元素的 ID 值相同，`getElementById()`只返回文档中第一次出现的元素。 IE7 及较低版本还为此方法添加了一个有意思的“怪癖”： name 特性与给定 ID 匹配的表单元素（`<input>`、`<textarea>`、 `<button>`及`<select>`）也会被该方法返回。如果有哪个表单元素的 name 特性等于指定的 ID，而且该元素在文档中位于带有给定 ID 的元素前面，那么 IE 就会返回那个表单元素。来看下面的例子。

```js
<input type="text" name="myElement" value="Text field">
<div id="myElement">A div</div>
```

基于这段 HTML 代码，在 IE7 中调用 `document.getElementById("myElement")`，结果会返回`<input>`元素；而在其他所有浏览器中，都会返回对`<div>`元素的引用。为了避免 IE 中存在的这个问题，最好的办法是不让表单字段的 name 特性与其他元素的 ID 相同。

另一个常用于取得元素引用的方法是 `getElementsByTagName()`。这个方法接受一个参数，即要取得元素的标签名，而返回的是包含零或多个元素的 NodeList。在 HTML 文档中，这个方法会返回一个 HTMLCollection 对象，作为一个“动态”集合，该对象与 NodeList 非常类似。例如，下列代码会取得页面中所有的`<img>`元素，并返回一个 HTMLCollection。

```js
var images = document.getElementsByTagName("img");
```

这行代码会将一个 HTMLCollection 对象保存在 images 变量中。与 NodeList 对象类似，可以使用方括号语法或`item()`方法来访问 HTMLCollection 对象中的项。而这个对象中元素的数量则可以通过其 length 属性取得，如下面的例子所示。

```js
alert(images.length); //输出图像的数量
alert(images[0].src); //输出第一个图像元素的 src 特性
alert(images.item(0).src); //输出第一个图像元素的 src 特性
```

HTMLCollection 对象还有一个方法，叫做`namedItem()`，使用这个方法可以通过元素的 name 特性取得集合中的项。例如，假设上面提到的页面中包含如下`<img>`元素：

```js
<img src="myimage.gif" name="myImage">
```

那么就可以通过如下方式从 images 变量中取得这个`<img>`元素：

```js
var myImage = images.namedItem("myImage");
```

在提供按索引访问项的基础上， HTMLCollection 还支持按名称访问项，这就为我们取得实际想要的元素提供了便利。而且，对命名的项也可以使用方括号语法来访问，如下所示：

```js
var myImage = images["myImage"];
```

对 HTMLCollection 而言，我们可以向方括号中传入数值或字符串形式的索引值。在后台，对数值索引就会调用 `item()`，而对字符串索引就会调用 `namedItem()`。要想取得文档中的所有元素，可以向 `getElementsByTagName()`中传入"*"。在 JavaScript 及 CSS中，星号（`*`）通常表示“全部”。下面看一个例子。

```js
var allElements = document.getElementsByTagName("*");
```

仅此一行代码返回的 HTMLCollection 中，就包含了整个页面中的所有元素——按照它们出现的先后顺序。换句话说，第一项是`<html>`元素， 第二项是`<head>`元素，以此类推。由于 IE 将注释（ Comment）实现为元素（ Element），因此在 IE 中调用 `getElementsByTagName("*")`将会返回所有注释节点。

虽然标准规定标签名需要区分大小写，但为了最大限度地与既有 HTML 页面兼容，传给 `getElementsByTagName()`的标签名是不需要区分大小写的。但对于 XML 页面而言（包括 XHTML）， `getElementsByTagName()`方法就会区分大小写。

第三个方法，也是只有 HTMLDocument 类型才有的方法，是 `getElementsByName()`。顾名思义，这个方法会返回带有给定 name 特性的所有元素。最常使用`getElementsByName()`方法的情况是取得单选按钮；为了确保发送给浏览器的值正确无误，所有单选按钮必须具有相同的 name 特性，如下面的例子所示。

```html
<fieldset>
  <legend>Which color do you prefer?</legend>
  <ul>
    <li><input type="radio" value="red" name="color" id="colorRed">
      <label for="colorRed">Red</label></li>
    <li><input type="radio" value="green" name="color" id="colorGreen">
      <label for="colorGreen">Green</label></li>
    <li><input type="radio" value="blue" name="color" id="colorBlue">
      <label for="colorBlue">Blue</label></li>
  </ul>
</fieldset>
```

如这个例子所示，其中所有单选按钮的 name 特性值都是"color"，但它们的 ID 可以不同。 ID 的作用在于将`<label>`元素应用到每个单选按钮，而 name 特性则用以确保三个值中只有一个被发送给浏览器。这样，我们就可以使用如下代码取得所有单选按钮：

```js
var radios = document.getElementsByName("color");
```

与 `getElementsByTagName()`类似， `getElementsByName()`方法也会返回一个 HTMLCollectioin。但是，对于这里的单选按钮来说， `namedItem()`方法则只会取得第一项（因为每一项的 name 特性都相同）。

**4. 特殊集合**

除了属性和方法， document 对象还有一些特殊的集合。这些集合都是 HTMLCollection 对象，为访问文档常用的部分提供了快捷方式，包括：

- document.anchors，包含文档中所有带 name 特性的`<a>`元素；
- document.applets，包含文档中所有的`<applet>`元素，因为不再推荐使用`<applet>`元素，所以这个集合已经不建议使用了；
- document.forms， 包含文档中所有的`<form>`元素， 与 `document.getElementsByTagName("form")`得到的结果相同；
- document.images，包含文档中所有的`<img>`元素，与 `document.getElementsByTagName("img")`得到的结果相同；
- document.links，包含文档中所有带 href 特性的`<a>`元素。

这个特殊集合始终都可以通过 HTMLDocument 对象访问到， 而且， 与 HTMLCollection 对象类似，集合中的项也会随着当前文档内容的更新而更新。

**5. DOM 一致性检测**

由于 DOM 分为多个级别，也包含多个部分，因此检测浏览器实现了 DOM 的哪些部分就十分必要了。`document.implementation` 属性就是为此提供相应信息和功能的对象，与浏览器对 DOM 的实现直接对应。 DOM1 级只为 `document.implementation` 规定了一个方法，即`hasFeature()`。这个方法接受两个参数：要检测的 DOM 功能的名称及版本号。如果浏览器支持给定名称和版本的功能，则该方法返回 true，如下面的例子所示：

```js
var hasXmlDom = document.implementation.hasFeature("XML", "1.0");
```

下表列出了可以检测的不同的值及版本号。

尽管使用`hasFeature()`确实方便，但也有缺点。因为实现者可以自行决定是否与 DOM 规范的不同部分保持一致。事实上，要想让` hasFearture()`方法针对所有值都返回 true 很容易，但返回 true 有时候也不意味着实现与规范一致。例如， Safari 2.x 及更早版本会在没有完全实现某些 DOM 功能的情况下也返回 true。为此，我们建议多数情况下，在使用 DOM 的某些特殊的功能之前，最好除了检测`hasFeature()`之外，还同时使用能力检测。

**6. 文档写入**

有一个 document 对象的功能已经存在很多年了，那就是将输出流写入到网页中的能力。这个能力体现在下列 4 个方法中： `write()`、 `writeln()`、 `open()`和 `close()`。其中， `write()`和 `writeln()`方法都接受一个字符串参数，即要写入到输出流中的文本。 `write()`会原样写入，而`writeln()`则会在字符串的末尾添加一个换行符（`\n`）。在页面被加载的过程中，可以使用这两个方法向页面中动态地加入内容，如下面的例子所示。

```html
<html>
<head>
  <title>document.write() Example</title>
</head>
<body>
  <p>The current date and time is:
  <script type="text/javascript">
    document.write("<strong>" + (new Date()).toString() + "</strong>");
  </script>
  </p>
</body>
</html
```

这个例子展示了在页面加载过程中输出当前日期和时间的代码。其中，日期被包含在一个`<strong>`元素中，就像在 HTML 页面中包含普通的文本一样。这样做会创建一个 DOM 元素，而且可以在将来访问该元素。通过 `write()`和 `writeln()`输出的任何 HTML 代码都将如此处理。

此外，还可以使用 `write()`和 `writeln()`方法动态地包含外部资源，例如 JavaScript 文件等。在包含 JavaScript 文件时，必须注意不能像下面的例子那样直接包含字符串`</script>`，因为这会导致该字符串被解释为脚本块的结束，它后面的代码将无法执行。

```html
<html>
<head>
  <title>document.write() Example 2</title>
</head>
<body>
  <script type="text/javascript">
    document.write("<script type=\"text/javascript\" src=\"file.js\">" +
      "</script>");
  </script>
</body>
</html>
```

即使这个文件看起来没错，但字符串`</script>`将被解释为与外部的`<script>`标签匹配，结果文本`);`将会出现在页面中。为避免这个问题，只需加入转义字符`\`即可；第 2 章也曾经提及这个问题，解决方案如下。

```html
<html>
<head>
  <title>document.write() Example 3</title>
</head>
<body>
  <script type="text/javascript">
    document.write("<script type=\"text/javascript\" src=\"file.js\">" +
      "<\/script>");
  </script>
</body>
</html>
```

字符串`<\/script>`不会被当作外部`<script>`标签的关闭标签，因而页面中也就不会出现多余的内容了。

前面的例子使用`document.write()`在页面被呈现的过程中直接向其中输出了内容。如果在文档加载结束后再调用`document.write()`，那么输出的内容将会重写整个页面，如下面的例子所示：

```html
<html>
<head>
  <title>document.write() Example 4</title>
</head>
<body>
  <p>This is some content that you won't get to see because it will be overwritten.</p>
  <script type="text/javascript">
    window.onload = function(){
      document.write("Hello world!");
    };
  </script>
</body>
</html>
```

在这个例子中，我们使用了 `window.onload` 事件处理程序（事件将在第 13 章讨论），等到页面完全加载之后延迟执行函数。函数执行之后，字符串"Hello world!"会重写整个页面内容。

方法 `open()`和 `close()`分别用于打开和关闭网页的输出流。如果是在页面加载期间使用 `write()`或 `writeln()`方法，则不需要用到这两个方法。

> 严格型 XHTML 文档不支持文档写入。对于那些按照 application/xml+xhtml 内容类型提供的页面，这两个方法也同样无效。

### 10.1.3 Element类型

除了 Document 类型之外， Element 类型就要算是 Web 编程中最常用的类型了。 Element 类型用于表现 XML 或 HTML 元素，提供了对元素标签名、子节点及特性的访问。 Element 节点具有以下特征：

- nodeType 的值为 1；
- nodeName 的值为元素的标签名；
- nodeValue 的值为 null；
- parentNode 可能是 Document 或 Element；
- 其子节点可能是 Element、 Text、 Comment、 ProcessingInstruction、 CDATASection 或EntityReference。

要访问元素的标签名，可以使用 nodeName 属性，也可以使用 tagName 属性；这两个属性会返回相同的值（使用后者主要是为了清晰起见）。以下面的元素为例：

```js
<div id="myDiv"></div>
```

可以像下面这样取得这个元素及其标签名：

```js
var div = document.getElementById("myDiv");
alert(div.tagName); // "DIV"
alert(div.tagName == div.nodeName); // true
```

这里的元素标签名是 div，它拥有一个值为"myDiv"的 ID。可是， `div.tagName` 实际上输出的是"DIV"而非"div"。在 HTML 中，标签名始终都以全部大写表示；而在 XML（有时候也包括 XHTML）中，标签名则始终会与源代码中的保持一致。假如你不确定自己的脚本将会在 HTML 还是 XML 文档中执行，最好是在比较之前将标签名转换为相同的大小写形式，如下面的例子所示：

```js
if (element.tagName == "div"){ //不能这样比较，很容易出错！
//在此执行某些操作
}
if (element.tagName.toLowerCase() == "div"){ //这样最好（适用于任何文档）
//在此执行某些操作
}
```

这个例子展示了围绕 tagName 属性的两次比较操作。第一次比较非常容易出错，因为其代码在 HTML 文档中不管用。第二次比较将标签名转换成了全部小写，是我们推荐的做法，因为这种做法适用于 HTML 文档，也适用于 XML 文档。

> 可以在任何浏览器中通过脚本访问 Element 类型的构造函数及原型，包括 IE8 及之前版本。在 Safari 2 之前版本和 Opera 8 之前的版本中，不能访问 Element 类型的构造函数。

**2. 取得特性**

每个元素都有一或多个特性，这些特性的用途是给出相应元素或其内容的附加信息。操作特性的DOM 方法主要有三个，分别是`getAttribute()`、 `setAttribute()`和 `removeAttribute()`。这三个方法可以针对任何特性使用，包括那些以 HTMLElement 类型属性的形式定义的特性。来看下面的例子：

```js
var div = document.getElementById("myDiv");
alert(div.getAttribute("id")); //"myDiv"
alert(div.getAttribute("class")); //"bd"
alert(div.getAttribute("title")); //"Body text"
alert(div.getAttribute("lang")); //"en"
alert(div.getAttribute("dir")); //"ltr"
```

注意，传递给`getAttribute()`的特性名与实际的特性名相同。因此要想得到 class 特性值，应该传入"class"而不是"className"，后者只有在通过对象属性访问特性时才用。如果给定名称的特性不存在， `getAttribute()`返回 null。通过 `getAttribute()`方法也可以取得自定义特性（即标准 HTML 语言中没有的特性）的值，以下面的元素为例：

```html
<div id="myDiv" my_special_attribute="hello!"></div>
```

这个元素包含一个名为 my_special_attribute 的自定义特性，它的值是"hello!"。可以像取得其他特性一样取得这个值，如下所示：

```js
var value = div.getAttribute("my_special_attribute");
```

不过，特性的名称是不区分大小写的，即"ID"和"id"代表的都是同一个特性。另外也要注意，根据 HTML5 规范，自定义特性应该加上 data-前缀以便验证。任何元素的所有特性，也都可以通过 DOM 元素本身的属性来访问。当然， HTMLElement 也会有 5 个属性与相应的特性一一对应。不过，只有公认的（非自定义的）特性才会以属性的形式添加到 DOM 对象中。以下面的元素为例：

```js
<div id="myDiv" align="left" my_special_attribute="hello!"></div>
```

因为 id 和 align 在 HTML 中是`<div>`的公认特性，因此该元素的 DOM 对象中也将存在对应的属性。不过，自定义特性 my_special_attribute 在 Safari、 Opera、 Chrome 及 Firefox 中是不存在的；但 IE 却会为自定义特性也创建属性，如下面的例子所示：

```js
alert(div.id); //"myDiv"
alert(div.my_special_attribute); //undefined（ IE 除外）
alert(div.align); //"left"
```

有两类特殊的特性，它们虽然有对应的属性名，但属性的值与通过`getAttribute()`返回的值并不相同。第一类特性就是 style，用于通过 CSS 为元素指定样式。在通过`getAttribute()`访问时，返回的 style 特性值中包含的是 CSS 文本，而通过属性来访问它则会返回一个对象。由于 style 属性是用于以编程方式访问元素样式的（本章后面讨论），因此并没有直接映射到 style 特性。

第二类与众不同的特性是 onclick 这样的事件处理程序。当在元素上使用时， onclick 特性中包含的是 JavaScript 代码，如果通过`getAttribute()`访问，则会返回相应代码的字符串。而在访问 onclick 属性时，则会返回一个 JavaScript 函数（如果未在元素中指定相应特性，则返回 null）。这是因为 onclick 及其他事件处理程序属性本身就应该被赋予函数值。

由于存在这些差别，在通过 JavaScript 以编程方式操作 DOM 时，开发人员经常不使用`getAttribute()`，而是只使用对象的属性。只有在取得自定义特性值的情况下，才会使用`getAttribute()`方法。在 IE7 及以前版本中，通过`getAttribute()`方法访问 style 特性或 onclick 这样的事件处理特性时，返回的值与属性的值相同。换句话说， `getAttribute("style")`返回一个对象，而` getAttribute("onclick")`返回一个函数。虽然 IE8 已经修复了这个bug，但不同IE版本间的不一致性，也是导致开发人员不使`getAttribute()`访问HTML特性的一个原因。

**3. 设置特性**

与 `getAttribute()`对应的方法是 `setAttribute()`，这个方法接受两个参数：要设置的特性名和值。如果特性已经存在，`setAttribute()`会以指定的值替换现有的值；如果特性不存在，`setAttribute()`则创建该属性并设置相应的值。来看下面的例子：

```js
div.setAttribute("id", "someOtherId");
div.setAttribute("class", "ft");
div.setAttribute("title", "Some other text");
div.setAttribute("lang","fr");
div.setAttribute("dir", "rtl");
```

通过 `setAttribute()`方法既可以操作 HTML 特性也可以操作自定义特性。通过这个方法设置的特性名会被统一转换为小写形式，即"ID"最终会变成"id"。

因为所有特性都是属性，所以直接给属性赋值可以设置特性的值，如下所示。

```js
div.id = "someOtherId";
div.align = "left";
```

不过，像下面这样为 DOM 元素添加一个自定义的属性，该属性不会自动成为元素的特性。

```js
div.mycolor = "red";
alert(div.getAttribute("mycolor")); //null（ IE 除外）
```

这个例子添加了一个名为 mycolor 的属性并将它的值设置为"red"。在大多数浏览器中，这个属性都不会自动变成元素的特性，因此想通过 `getAttribute()`取得同名特性的值，结果会返回 null。可是，自定义属性在 IE 中会被当作元素的特性，反之亦然。

> 在 IE7 及以前版本中，`setAttribute()`存在一些异常行为。通过这个方法设置 class 和 style 特性，没有任何效果，而使用这个方法设置事件处理程序特性时也一样。尽管到了 IE8 才解决这些问题，但我们还是推荐通过属性来设置特性。

要介绍的最后一个方法是 `removeAttribute()`，这个方法用于彻底删除元素的特性。调用这个方法不仅会清除特性的值，而且也会从元素中完全删除特性，如下所示：

```js
div.removeAttribute("class");
```

这个方法并不常用，但在序列化 DOM 元素时，可以通过它来确切地指定要包含哪些特性。

> IE6 及以前版本不支持 `removeAttribute()`。

**4. attributes 属性**

Element 类型是使用 attributes 属性的唯一一个 DOM 节点类型。attributes 属性中包含一个 NamedNodeMap ，与 NodeList 类似，也是一个“动态”的集合。元素的每一个特性都由一个 Attr 节点表示，每个节点都保存在 NamedNodeMap 对象中。 NamedNodeMap 对象拥有下列方法。

- getNamedItem(name)：返回 nodeName 属性等于 name 的节点；
- removeNamedItem(name)：从列表中移除 nodeName 属性等于 name 的节点；
- setNamedItem(node)：向列表中添加节点，以节点的 nodeName 属性为索引；
- item(pos)：返回位于数字 pos 位置处的节点。

attributes 属性中包含一系列节点，每个节点的 nodeName 就是特性的名称， 而节点的 nodeValue 就是特性的值。要取得元素的 id 特性，可以使用以下代码。

```js
var id = element.attributes.getNamedItem("id").nodeValue;
```

以下是使用方括号语法通过特性名称访问节点的简写方式。

```js
var id = element.attributes["id"].nodeValue;
```

也可以使用这种语法来设置特性的值，即先取得特性节点，然后再将其 nodeValue 设置为新值，如下所示。

```js
element.attributes["id"].nodeValue = "someOtherId";
```

调用 `removeNamedItem()`方法与在元素上调用 `removeAttribute()`方法的效果相同——直接删除具有给定名称的特性。下面的例子展示了两个方法间唯一的区别，即 `removeNamedItem()`返回表示被删除特性的 Attr 节点。

```js
var oldAttr = element.attributes.removeNamedItem("id");
```

最后， `setNamedItem()`是一个很不常用的方法，通过这个方法可以为元素添加一个新特性，为此需要为它传入一个特性节点，如下所示。

```js
element.attributes.setNamedItem(newAttr);
```

一般来说，由于前面介绍的 attributes 的方法不够方便，因此开发人员更多的会使用`getAttribute()`、`removeAttribute()`和`setAttribute()`方法。

不过，如果想要遍历元素的特性， attributes 属性倒是可以派上用场。在需要将 DOM 结构序列化为 XML 或 HTML 字符串时，多数都会涉及遍历元素特性。以下代码展示了如何迭代元素的每一个特性，然后将它们构造成`name="value" name="value"`这样的字符串格式。

```js
function outputAttributes(element){
  var pairs = new Array(),
  attrName,
  attrValue,
  i,
  len;
  for (i=0, len=element.attributes.length; i < len; i++){
    attrName = element.attributes[i].nodeName;
    attrValue = element.attributes[i].nodeValue;
    pairs.push(attrName + "=\"" + attrValue + "\"");
  }
  return pairs.join(" ");
}
```

这个函数使用了一个数组来保存名值对，最后再以空格为分隔符将它们拼接起来（这是序列化长字符串时的一种常用技巧）。通过` attributes.length` 属性， for 循环会遍历每个特性，将特性的名称和值输出为字符串。关于以上代码的运行结果，以下是两点必要的说明。

- 针对 attributes 对象中的特性，不同浏览器返回的顺序不同。这些特性在 XML 或 HTML 代码中出现的先后顺序，不一定与它们出现在 attributes 对象中的顺序一致。
- IE7 及更早的版本会返回 HTML 元素中所有可能的特性，包括没有指定的特性。换句话说，返回 100 多个特性的情况会很常见。

针对 IE7 及更早版本中存在的问题，可以对上面的函数加以改进，让它只返回指定的特性。每个特性节点都有一个名为 specified 的属性，这个属性的值如果为 true，则意味着要么是在 HTML 中指定了相应特性，要么是通过`setAttribute()`方法设置了该特性。在 IE 中，所有未设置过的特性的该属性值都为 false，而在其他浏览器中根本不会为这类特性生成对应的特性节点（因此，在这些浏览器中，任何特性节点的 specified 值始终为 true）。改进后的代码如下所示。

```js
function outputAttributes(element){
  var pairs = new Array(),
  attrName,
  attrValue,
  i,
  len;
  for (i=0, len=element.attributes.length; i < len; i++){
    attrName = element.attributes[i].nodeName;
    attrValue = element.attributes[i].nodeValue;
    if (element.attributes[i].specified) {
      pairs.push(attrName + "=\"" + attrValue + "\"");
    }
  }
  return pairs.join(" ");
}
```

这个经过改进的函数可以确保即使在 IE7 及更早的版本中，也会只返回指定的特性。

**5. 创建元素**

使用`document.createElement()`方法可以创建新元素。这个方法只接受一个参数，即要创建元素的标签名。这个标签名在 HTML 文档中不区分大小写，而在 XML（包括 XHTML）文档中，则是区分大小写的。例如，使用下面的代码可以创建一个`<div>`元素。

```js
var div = document.createElement("div");
```

在使用`createElement()`方法创建新元素的同时，也为新元素设置了 ownerDocuemnt 属性。此时，还可以操作元素的特性，为它添加更多子节点，以及执行其他操作。来看下面的例子。

```js
div.id = "myNewDiv";
div.className = "box";
```

在新元素上设置这些特性只是给它们赋予了相应的信息。由于新元素尚未被添加到文档树中，因此设置这些特性不会影响浏览器的显示。要把新元素添加到文档树，可以使用`appendChild()`、`insertBefore()`或`replaceChild()`方法。下面的代码会把新创建的元素添加到文档的`<body>`元素中。

```js
document.body.appendChild(div);
```

一旦将元素添加到文档树中，浏览器就会立即呈现该元素。此后，对这个元素所作的任何修改都会实时反映在浏览器中。

在 IE 中可以以另一种方式使用`createElement()`，即为这个方法传入完整的元素标签，也可以包含属性，如下面的例子所示。

```js
var div = document.createElement("<div id=\"myNewDiv\" class=\"box\"></div >");
```

这种方式有助于避开在 IE7 及更早版本中动态创建元素的某些问题。下面是已知的一些这类问题。

- 不能设置动态创建的`<iframe>`元素的 name 特性。
- 不能通过表单的`reset()`方法重设动态创建的`<input>`元素（第 13 章将讨论`reset()`方法）
- 动态创建的 type 特性值为"reset"的`<buttou>`元素重设不了表单。
- 动态创建的一批 name 相同的单选按钮彼此毫无关系。 name 值相同的一组单选按钮本来应该用于表示同一选项的不同值，但动态创建的一批这种单选按钮之间却没有这种关系。

上述所有问题都可以通过在`createElement()`中指定完整的 HTML 标签来解决，如下面的例子所示。

```js
if (client.browser.ie && client.browser.ie <=7){
  //创建一个带 name 特性的 iframe 元素
  var iframe = document.createElement("<iframe name=\"myframe\"></iframe>");

  //创建 input 元素
  var input = document.createElement("<input type=\"checkbox\">");

  //创建 button 元素
  var button = document.createElement("<button type=\"reset\"></button>");

  //创建单选按钮
  var radio1 = document.createElement("<input type=\"radio\" name=\"choice\" "＋
  "value=\"1\">");
  var radio2 = document.createElement("<input type=\"radio\" name=\"choice\" "＋
  "value=\"2\">");
}
```

与使用`createElement()`的惯常方式一样，这样的用法也会返回一个 DOM 元素的引用。可以将这个引用添加到文档中，也可以对其加以增强。但是，由于这样的用法要求使用浏览器检测，因此我们建议只在需要避开 IE 及更早版本中上述某个问题的情况下使用。其他浏览器都不支持这种用法。

**6. 元素的子节点**

元素可以有任意数目的子节点和后代节点，因为元素可以是其他元素的子节点。元素的 childNodes 属性中包含了它的所有子节点，这些子节点有可能是元素、文本节点、注释或处理指令。

不同浏览器在看待这些节点方面存在显著的不同，以下面的代码为例。

```html
<ul id="myList">
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

如果是 IE 来解析这些代码，那么`<ul>`元素会有 3 个子节点，分别是 3 个`<li>`元素。但如果是在其他浏览器中， `<ul>`元素都会有 7 个元素，包括 3 个`<li>`元素和 4 个文本节点（表示`<li>`元素之间的空白符）。如果像下面这样将元素间的空白符删除，那么所有浏览器都会返回相同数目的子节点。

```js
<ul id="myList"><li>Item 1</li><li>Item 2</li><li>Item 3</li></ul>
```

对于这段代码，`<ul>`元素在任何浏览器中都会包含 3 个子节点。如果需要通过 childNodes 属性遍历子节点，那么一定不要忘记浏览器间的这一差别。这意味着在执行某项操作以前，通常都要先检查一下 nodeTpye 属性，如下面的例子所示。

```js
for (var i=0, len=element.childNodes.length; i < len; i++){
  if (element.childNodes[i].nodeType == 1){
    //执行某些操作
  }
}
```

这个例子会循环遍历特定元素的每一个子节点，然后只在子节点的 nodeType 等于 1（表示是元素节点）的情况下，才会执行某些操作。

如果想通过某个特定的标签名取得子节点或后代节点该怎么办呢？实际上，元素也支持`getElementsByTagName()`方法。在通过元素调用这个方法时，除了搜索起点是当前元素之外，其他方面都跟通过 document 调用这个方法相同，因此结果只会返回当前元素的后代。例如，要想取得前面`<ul>`元素中包含的所有`<li>`元素，可以使用下列代码。

```js
var ul = document.getElementById("myList");
var items = ul.getElementsByTagName("li");
```

要注意的是，这里`<ul>`的后代中只包含直接子元素。不过，如果它包含更多层次的后代元素，那么各个层次中包含的`<li>`元素也都会返回。

### 10.1.4 Text类型

文本节点由 Text 类型表示，包含的是可以照字面解释的纯文本内容。纯文本中可以包含转义后的 HTML 字符，但不能包含 HTML 代码。 Text 节点具有以下特征：

- nodeType 的值为 3；
- nodeName 的值为"#text"；
- nodeValue 的值为节点所包含的文本；
- parentNode 是一个 Element；
- 不支持（没有）子节点。

可以通过 nodeValue 属性或 data 属性访问 Text 节点中包含的文本，这两个属性中包含的值相同。对 nodeValue 的修改也会通过 data 反映出来，反之亦然。使用下列方法可以操作节点中的文本。

- `appendData(text)`：将 text 添加到节点的末尾。
- `deleteData(offset, count)`：从 offset 指定的位置开始删除 count 个字符。
- `insertData(offset, text)`：在 offset 指定的位置插入 text。
- `replaceData(offset, count, text)`：用 text 替换从 offset 指定的位置开始到 offset+count 为止处的文本。
- `splitText(offset)`：从 offset 指定的位置将当前文本节点分成两个文本节点。
- `substringData(offset, count)`：提取从 offset 指定的位置开始到 offset+count 为止处的字符串。

除了这些方法之外，文本节点还有一个 length 属性，保存着节点中字符的数目。而且，`nodeValue.length` 和 `data.length` 中也保存着同样的值。

在默认情况下，每个可以包含内容的元素最多只能有一个文本节点，而且必须确实有内容存在。来看几个例子。

```html
<!-- 没有内容，也就没有文本节点 -->
<div></div>
<!-- 有空格，因而有一个文本节点 -->
<div> </div>
<!-- 有内容，因而有一个文本节点 -->
<div>Hello World!</div>
```

上面代码给出的第一个`<div>`元素没有内容，因此也就不存在文本节点。开始与结束标签之间只要存在内容，就会创建一个文本节点。因此，第二个`<div>`元素中虽然只包含一个空格，但仍然有一个文本子节点；文本节点的 nodeValue 值是一个空格。第三个`<div>`也有一个文本节点，其 nodeValue 的值为"Hello World!"。可以使用以下代码来访问这些文本子节点。

```js
var textNode = div.firstChild; //或者 div.childNodes[0]
```

在取得了文本节点的引用后，就可以像下面这样来修改它了。

```js
div.firstChild.nodeValue = "Some other message";
```

如果这个文本节点当前存在于文档树中，那么修改文本节点的结果就会立即得到反映。另外，在修改文本节点时还要注意，此时的字符串会经过 HTML（或 XML，取决于文档类型）编码。换句话说，小于号、大于号或引号都会像下面的例子一样被转义。

```js
//输出结果是"Some &lt;strong&gt;other&lt;/strong&gt; message"
div.firstChild.nodeValue = "Some <strong>other</strong> message";
```

应该说，这是在向 DOM 文档中插入文本之前，先对其进行 HTML 编码的一种有效方式。

> 在 IE8、 Firefox、 Safari、 Chrome 和 Opera 中，可以通过脚本访问 Text 类型的构造函数和原型。

**1. 创建文本节点**

可以使用 `document.createTextNode()`创建新文本节点，这个方法接受一个参数——要插入节点中的文本。与设置已有文本节点的值一样，作为参数的文本也将按照 HTML 或 XML 的格式进行编码。

```js
var textNode = document.createTextNode("<strong>Hello</strong> world!");
```

在创建新文本节点的同时，也会为其设置 ownerDocument 属性。不过，除非把新节点添加到文档树中已经存在的节点中，否则我们不会在浏览器窗口中看到新节点。下面的代码会创建一个`<div>`元素并向其中添加一条消息。

```js
var element = document.createElement("div");
element.className = "message";
var textNode = document.createTextNode("Hello world!");
element.appendChild(textNode);
document.body.appendChild(element);
```

这个例子创建了一个新`<div>`元素并为它指定了值为"message"的 class 特性。然后，又创建了一个文本节点，并将其添加到前面创建的元素中。最后一步，就是将这个元素添加到了文档的`<body>`元素中，这样就可以在浏览器中看到新创建的元素和文本节点了。

一般情况下，每个元素只有一个文本子节点。不过，在某些情况下也可能包含多个文本子节点，如下面的例子所示。

```js
var element = document.createElement("div");
element.className = "message";
var textNode = document.createTextNode("Hello world!");
element.appendChild(textNode);
var anotherTextNode = document.createTextNode("Yippee!");
element.appendChild(anotherTextNode);
document.body.appendChild(element);
```

如果两个文本节点是相邻的同胞节点，那么这两个节点中的文本就会连起来显示，中间不会有空格。

**2. 规范化文本节点**

DOM 文档中存在相邻的同胞文本节点很容易导致混乱，因为分不清哪个文本节点表示哪个字符串。另外， DOM 文档中出现相邻文本节点的情况也不在少数，于是就催生了一个能够将相邻文本节点合并的方法。这个方法是由 Node 类型定义的（因而在所有节点类型中都存在），名叫 `normalize()`。如果在一个包含两个或多个文本节点的父元素上调用 `normalize()`方法，则会将所有文本节点合并成一个节点，结果节点的 nodeValue 等于将合并前每个文本节点的 nodeValue 值拼接起来的值。来看一个
例子。

```js
var element = document.createElement("div");
element.className = "message";
var textNode = document.createTextNode("Hello world!");
element.appendChild(textNode);
var anotherTextNode = document.createTextNode("Yippee!");
element.appendChild(anotherTextNode);
document.body.appendChild(element);
alert(element.childNodes.length); //2
element.normalize();
alert(element.childNodes.length); //1
alert(element.firstChild.nodeValue); // "Hello world!Yippee!"
```

浏览器在解析文档时永远不会创建相邻的文本节点。这种情况只会作为执行 DOM 操作的结果出现。

> 在某些情况下，执行 `normalize()`方法会导致 IE6 崩溃。不过，在 IE6 后来的补丁中，可能已经修复了这个问题（未经证实）。 IE7 及更高版本中不存在这个问题。

**3. 分割文本节点**

Text 类型提供了一个作用与 `normalize()`相反的方法：`splitText()`。这个方法会将一个文本节点分成两个文本节点，即按照指定的位置分割 nodeValue 值。原来的文本节点将包含从开始到指定位置之前的内容，新文本节点将包含剩下的文本。这个方法会返回一个新文本节点，该节点与原节点的 parentNode 相同。来看下面的例子。

```js
var element = document.createElement("div");
element.className = "message";
var textNode = document.createTextNode("Hello world!");
element.appendChild(textNode);
document.body.appendChild(element);

var newNode = element.firstChild.splitText(5);
alert(element.firstChild.nodeValue); //"Hello"
alert(newNode.nodeValue); //" world!"
alert(element.childNodes.length); //2
```

在这个例子中，包含"Hello world!"的文本节点被分割为两个文本节点，从位置 5 开始。位置 5是"Hello"和"world!"之间的空格，因此原来的文本节点将包含字符串"Hello"，而新文本节点将包含文本"world!"（包含空格）。

分割文本节点是从文本节点中提取数据的一种常用 DOM 解析技术。

### 10.1.5 Comment类型

注释在 DOM 中是通过 Comment 类型来表示的。 Comment 节点具有下列特征：

- nodeType 的值为 8；
- nodeName 的值为"#comment"；
- nodeValue 的值是注释的内容；
- parentNode 可能是 Document 或 Element；
- 不支持（没有）子节点。

Comment 类型与 Text 类型继承自相同的基类，因此它拥有除`splitText()`之外的所有字符串操作方法。与 Text 类型相似，也可以通过 nodeValue 或 data 属性来取得注释的内容。

注释节点可以通过其父节点来访问，以下面的代码为例。

```html
<div id="myDiv"><!--A comment --></div>
```

在此，注释节点是`<div>`元素的一个子节点，因此可以通过下面的代码来访问它。

```js
var div = document.getElementById("myDiv");
var comment = div.firstChild;
alert(comment.data); //"A comment"
```

另外，使用 `document.createComment()`并为其传递注释文本也可以创建注释节点，如下面的例子所示。

```js
var comment = document.createComment("A comment ");
```

显然，开发人员很少会创建和访问注释节点，因为注释节点对算法鲜有影响。此外，浏览器也不会识别位于`</html>`标签后面的注释。如果要访问注释节点，一定要保证它们是`<html>`元素的后代（即位于`<html>`和`</html>`之间）。

> 在 Firefox、 Safari、 Chrome 和 Opera 中，可以访问 Comment 类型的构造函数和原型。在 IE8 中，注释节点被视作标签名为"!"的元素。也就是说，使用`getElementsByTagName()`可以取得注释节点。尽管 IE9 没有把注释当成元素，但它仍然通过一个名为 HTMLCommentElement 的构造函数来表示注释。

### 10.1.6 CDATASection类型

CDATASection 类型只针对基于 XML 的文档，表示的是 CDATA 区域。与 Comment 类似， CDATASection 类型继承自 Text 类型，因此拥有除`splitText()`之外的所有字符串操作方法。CDATASection 节点具有下列特征：

- nodeType 的值为 4；
- nodeName 的值为"#cdata-section"；
- nodeValue 的值是 CDATA 区域中的内容；
- parentNode 可能是 Document 或 Element；
- 不支持（没有）子节点。

CDATA 区域只会出现在 XML 文档中，因此多数浏览器都会把 CDATA 区域错误地解析为 Comment 或 Element。以下面的代码为例：

```html
<div id="myDiv"><![CDATA[This is some content.]]></div>
```

这个例子中的`<div>`元素应该包含一个 CDATASection 节点。可是，四大主流浏览器无一能够这样解析它。即使对于有效的 XHTML 页面，浏览器也没有正确地支持嵌入的 CDATA 区域。

在真正的 XML 文档中，可以使用`document.createCDataSection()`来创建 CDATA 区域，只需为其传入节点的内容即可。

> 在 Firefox、 Safari、 Chrome 和 Opera 中，可以访问 CDATASection 类型的构造函数和原型。 IE9 及之前版本不支持这个类型。

### 10.1.7 DocumentType类型

DocumentType 类型在 Web 浏览器中并不常用，仅有 Firefox、 Safari 和 Opera 支持它。 DocumentType 包含着与文档的 doctype 有关的所有信息，它具有下列特征：

- nodeType 的值为 10；
- nodeName 的值为 doctype 的名称；
- nodeValue 的值为 null；
- parentNode 是 Document；
- 不支持（没有）子节点。

在 DOM1 级中， DocumentType 对象不能动态创建，而只能通过解析文档代码的方式来创建。支持它的浏览器会把 DocumentType 对象保存在 `document.doctype` 中 。 DOM1 级描述了DocumentType 对象的 3 个属性： name、 entities 和 notations。其中， name 表示文档类型的名称；entities 是由文档类型描述的实体的 NamedNodeMap 对象； notations 是由文档类型描述的符号的NamedNodeMap 对象。通常，浏览器中的文档使用的都是 HTML 或 XHTML 文档类型，因而 entities和 notations 都是空列表（列表中的项来自行内文档类型声明）。但不管怎样，只有 name 属性是有用的。这个属性中保存的是文档类型的名称，也就是出现在`<!DOCTYPE`之后的文本。以下面严格型 HTML 4.01 的文档类型声明为例：

```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">
```

DocumentType 的 name 属性中保存的就是"HTML"：

```js
alert(document.doctype.name); //"HTML"
```

IE 及更早版本不支持 DocumentType，因此 `document.doctype` 的值始终都等于 null。可是，这些浏览器会把文档类型声明错误地解释为注释，并且为它创建一个注释节点。 IE9 会给`document.doctype`赋正确的对象，但仍然不支持访问 DocumentType 类型。

### 10.1.8 DocumentFragment类型

在所有节点类型中，只有 DocumentFragment 在文档中没有对应的标记。 DOM 规定文档片段（document fragment）是一种“轻量级”的文档，可以包含和控制节点，但不会像完整的文档那样占用额外的资源。 DocumentFragment 节点具有下列特征：

- nodeType 的值为 11；
- nodeName 的值为"#document-fragment"；
- nodeValue 的值为 null；
- parentNode 的值为 null；
- 子节点可以是 Element、 ProcessingInstruction、 Comment、 Text、 CDATASection 或 EntityReference。

虽然不能把文档片段直接添加到文档中，但可以将它作为一个“仓库”来使用，即可以在里面保存将来可能会添加到文档中的节点。要创建文档片段，可以使用 `document.createDocumentFragment()`方法，如下所示：

```js
var fragment = document.createDocumentFragment();
```

文档片段继承了 Node 的所有方法，通常用于执行那些针对文档的 DOM 操作。如果将文档中的节点添加到文档片段中，就会从文档树中移除该节点，也不会从浏览器中再看到该节点。添加到文档片段中的新节点同样也不属于文档树。可以通过 `appendChild()`或 `insertBefore()`将文档片段中内容添加到文档中。在将文档片段作为参数传递给这两个方法时，实际上只会将文档片段的所有子节点添加到相应位置上；文档片段本身永远不会成为文档树的一部分。来看下面的 HTML 示例代码：

```js
<ul id="myList"></ul>
```

假设我们想为这个`<ul>`元素添加 3 个列表项。如果逐个地添加列表项，将会导致浏览器反复渲染（呈现）新信息。为避免这个问题，可以像下面这样使用一个文档片段来保存创建的列表项，然后再一次性将它们添加到文档中。

```js
var fragment = document.createDocumentFragment();
var ul = document.getElementById("myList");
var li = null;
for (var i=0; i < 3; i++){
  li = document.createElement("li");
  li.appendChild(document.createTextNode("Item " + (i+1)));
  fragment.appendChild(li);
}
ul.appendChild(fragment);
```

在这个例子中，我们先创建一个文档片段并取得了对`<ul>`元素的引用。然后，通过 for 循环创建 3 个列表项，并通过文本表示它们的顺序。为此，需要分别创建`<li>`元素、创建文本节点，再把文本节点添加到`<li>`元素。接着使用`appendChild()`将`<li>`元素添加到文档片段中。循环结束后，再调用`appendChild()`并传入文档片段，将所有列表项添加到`<ul>`元素中。此时，文档片段的所有子节点都被删除并转移到了`<ul>`元素中。

### 10.1.9 Attr类型

元素的特性在 DOM 中以 Attr 类型来表示。在所有浏览器中（包括 IE8），都可以访问 Attr 类型的构造函数和原型。从技术角度讲，特性就是存在于元素的 attributes 属性中的节点。特性节点具有下列特征：

- nodeType 的值为 2；
- nodeName 的值是特性的名称；
- nodeValue 的值是特性的值；
- parentNode 的值为 null；
- 在 HTML 中不支持（没有）子节点；
- 在 XML 中子节点可以是 Text 或 EntityReference。

尽管它们也是节点，但特性却不被认为是 DOM 文档树的一部分。开发人员最常使用的是 `getAttribute()`、 `setAttribute()`和 `remveAttribute()`方法，很少直接引用特性节点。

Attr 对象有 3 个属性： name、 value 和 specified。其中， name 是特性名称（与 nodeName 的值相同）， value 是特性的值（与 nodeValue 的值相同），而 specified 是一个布尔值，用以区别特
性是在代码中指定的，还是默认的。使用 `document.createAttribute()`并传入特性的名称可以创建新的特性节点。例如，要为元素添加 align 特性，可以使用下列代码：

```js
var attr = document.createAttribute("align");
attr.value = "left";
element.setAttributeNode(attr);
alert(element.attributes["align"].value); //"left"
alert(element.getAttributeNode("align").value); //"left"
alert(element.getAttribute("align")); //"left"
```

这个例子创建了一个新的特性节点。由于在调用 `createAttribute()`时已经为 name 属性赋了值，所以后面就不必给它赋值了。之后，又把 value 属性的值设置为"left"。为了将新创建的特性添加到元素中，必须使用元素的 `setAttributeNode()`方法。添加特性之后，可以通过下列任何方式访问该特性： attributes 属性、 `getAttributeNode()`方法以及 `getAttribute()`方法。其中， attributes和` getAttributeNode()`都会返回对应特性的 Attr 节点，而 `getAttribute()`则只返回特性的值。我们并不建议直接访问特性节点。实际上，使用 `getAttribute()`、`setAttribute()`和 `removeAttribute()`方法远比操作特性节点更为方便。

## 10.2 DOM操作技术 

很多时候， DOM 操作都比较简明，因此用 JavaScript 生成那些通常原本是用 HTML 代码生成的内容并不麻烦。不过，也有一些时候，操作 DOM 并不像表面上看起来那么简单。由于浏览器中充斥着隐藏的陷阱和不兼容问题，用 JavaScript 代码处理 DOM 的某些部分要比处理其他部分更复杂一些。

### 10.2.1 动态脚本

使用`<script>`元素可以向页面中插入 JavaScript 代码，一种方式是通过其 src 特性包含外部文件，另一种方式就是用这个元素本身来包含代码。而这一节要讨论的动态脚本，指的是在页面加载时不存在，但将来的某一时刻通过修改 DOM 动态添加的脚本。跟操作 HTML 元素一样，创建动态脚本也有两种方式：插入外部文件和直接插入 JavaScript 代码。

动态加载的外部 JavaScript 文件能够立即运行，比如下面的`<script>`元素：

```js
<script type="text/javascript" src="client.js"></script>
```

这个`<script>`元素包含了第 9 章的客户端检测脚本。而创建这个节点的 DOM 代码如下所示：

```js
var script = document.createElement("script");
script.type = "text/javascrip";
script.src = "client.js";
document.body.appendChild(script);
```

显然，这里的 DOM 代码如实反映了相应的 HTML 代码。不过，在执行最后一行代码把`<script>`元素添加到页面中之前，是不会下载外部文件的。也可以把这个元素添加到`<head>`元素中，效果相同。整个过程可以使用下面的函数来封装：

```js
function loadScript(url){
  var script = document.createElement("script");
  script.type = "text/javascript";
  script.src = url;
  document.body.appendChild(script);
}
```

然后，就可以通过调用这个函数来加载外部的 JavaScript 文件了：

```js
loadScript("client.js");
```

加载完成后，就可以在页面中的其他地方使用这个脚本了。问题只有一个：怎么知道脚本加载完成呢？遗憾的是，并没有什么标准方式来探知这一点。不过，与此相关的一些事件倒是可以派上用场，但要取决于所用的浏览器，详细讨论请见第 13 章。

另一种指定 JavaScript 代码的方式是行内方式，如下面的例子所示：

```js
<script type="text/javascript">
  function sayHi(){
    alert("hi");
  }
</script>
```

从逻辑上讲，下面的 DOM 代码是有效的：

```js
var script = document.createElement("script");
script.type = "text/javascript";
script.appendChild(document.createTextNode("function sayHi(){alert('hi');}"));
document.body.appendChild(script);
```

在 Firefox、 Safari、 Chrome 和 Opera 中，这些 DOM 代码可以正常运行。但在 IE 中，则会导致错误。IE 将`<script>`视为一个特殊的元素，不允许 DOM 访问其子节点。不过，可以使用`<script>`元素的 text 属性来指定 JavaScript 代码，像下面的例子这样：

```js
var script = document.createElement("script");
script.type = "text/javascript";
script.text = "function sayHi(){alert('hi');}";
document.body.appendChild(script);
```

经过这样修改之后的代码可以在 IE、 Firefox、 Opera 和 Safari 3 及之后版本中运行。 Safari 3.0 之前的版本虽然不能正确地支持 text 属性，但却允许使用文本节点技术来指定代码。如果需要兼容早期版本的 Safari，可以使用下列代码：

```js
var script = document.createElement("script");
script.type = "text/javascript";
var code = "function sayHi(){alert('hi');}";
try {
  script.appendChild(document.createTextNode("code"));
} catch (ex){
  script.text = "code";
}
document.body.appendChild(script);
```

这里，首先尝试标准的 DOM 文本节点方法，因为除了 IE（在 IE 中会导致抛出错误），所有浏览器都支持这种方式。如果这行代码抛出了错误，那么说明是 IE，于是就必须使用 text 属性了。整个过程可以用以下函数来表示：

```js
function loadScriptString(code){
  var script = document.createElement("script");
  script.type = "text/javascript";
  try {
    script.appendChild(document.createTextNode(code));
  } catch (ex){
    script.text = code;
  }
  document.body.appendChild(script);
}
```

下面是调用这个函数的示例：

```js
loadScriptString("function sayHi(){alert('hi');}");
```

以这种方式加载的代码会在全局作用域中执行，而且当脚本执行后将立即可用。实际上，这样执行代码与在全局作用域中把相同的字符串传递给 `eval()`是一样的。

### 10.2.2 动态样式

能够把 CSS 样式包含到 HTML 页面中的元素有两个。其中，`<link>`元素用于包含来自外部的文件，而`<style>`元素用于指定嵌入的样式。与动态脚本类似，所谓动态样式是指在页面刚加载时不存在的样式；动态样式是在页面加载完成后动态添加到页面中的。

我们以下面这个典型的`<link>`元素为例：

```html
<link rel="stylesheet" type="text/css" href="styles.css">
```

使用 DOM 代码可以很容易地动态创建出这个元素：

```js
var link = document.createElement("link");
link.rel = "stylesheet";
link.type = "text/css";
link.href = "style.css";
var head = document.getElementsByTagName("head")[0];
head.appendChild(link);
```

以上代码在所有主流浏览器中都可以正常运行。需要注意的是，必须将`<link>`元素添加到`<head>`而不是`<body>`元素，才能保证在所有浏览器中的行为一致。整个过程可以用以下函数来表示：

```js
function loadStyles(url){
  var link = document.createElement("link");
  link.rel = "stylesheet";
  link.type = "text/css";
  link.href = url;
  var head = document.getElementsByTagName("head")[0];
  head.appendChild(link);
}
```

调用`loadStyles()`函数的代码如下所示：

```js
loadStyles("styles.css");
```

加载外部样式文件的过程是异步的，也就是加载样式与执行 JavaScript 代码的过程没有固定的次序。一般来说，知不知道样式已经加载完成并不重要；不过，也存在几种利用事件来检测这个过程是否完成的技术，这些技术将在第 13 章讨论。

另一种定义样式的方式是使用`<style>`元素来包含嵌入式 CSS，如下所示：

```html
<style type="text/css">
body {
  background-color: red;
}
</style>
```

按照相同的逻辑，下列 DOM 代码应该是有效的：

```js
var style = document.createElement("style");
style.type = "text/css";
style.appendChild(document.createTextNode("body{background-color:red}"));
var head = document.getElementsByTagName("head")[0];
head.appendChild(style);
```

以上代码可以在 Firefox、 Safari、 Chrome 和 Opera 中运行，在 IE 中则会报错。 IE 将`<style>`视为一个特殊的、与`<script>`类似的节点，不允许访问其子节点。事实上， IE 此时抛出的错误与向`<script>`元素添加子节点时抛出的错误相同。解决 IE 中这个问题的办法，就是访问元素的 styleSheet 属性，该属性又有一个 cssText 属性，可以接受 CSS 代码（第 13 章将进一步讨论这两个属性），如下面的例子所示。

```js
var style = document.createElement("style");
style.type = "text/css";
try{
  style.appendChild(document.createTextNode("body{background-color:red}"));
} catch (ex){
  style.styleSheet.cssText = "body{background-color:red}";
}
var head = document.getElementsByTagName("head")[0];
head.appendChild(style);
```

与动态添加嵌入式脚本类似，重写后的代码使用了 try-catch 语句来捕获 IE 抛出的错误，然后再使用针对 IE 的特殊方式来设置样式。因此，通用的解决方案如下。

```js
function loadStyleString(css){
  var style = document.createElement("style");
  style.type = "text/css";
  try{
    style.appendChild(document.createTextNode(css));
  } catch (ex){
    style.styleSheet.cssText = css;
  }
  var head = document.getElementsByTagName("head")[0];
  head.appendChild(style);
}
```

调用这个函数的示例如下：

```js
loadStyleString("body{background-color:red}");
```

这种方式会实时地向页面中添加样式，因此能够马上看到变化。

> 如果专门针对 IE 编写代码，务必小心使用 `styleSheet.cssText` 属性。在重用同一个`<style>`元素并再次设置这个属性时，有可能会导致浏览器崩溃。同样，将cssText 属性设置为空字符串也可能导致浏览器崩溃。我们希望 IE 中的这个 bug 能够在将来被修复。

### 10.2.3 操作表格

`<table>`元素是 HTML 中最复杂的结构之一。要想创建表格，一般都必须涉及表示表格行、 单元格、表头等方面的标签。由于涉及的标签多，因而使用核心 DOM 方法创建和修改表格往往都免不了要编写大量的代码。假设我们要使用 DOM 来创建下面的 HTML 表格。

```html
<table border="1" width="100%">
  <tbody>
    <tr>
      <td>Cell 1,1</td>
      <td>Cell 2,1</td>
    </tr>
    <tr>
      <td>Cell 1,2</td>
      <td>Cell 2,2</td>
    </tr>
  </tbody>
</table>
```

要使用核心 DOM 方法创建这些元素，得需要像下面这么多的代码：

```js
//创建 table
var table = document.createElement("table");
table.border = 1;
table.width = "100%";

//创建 tbody
var tbody = document.createElement("tbody");
table.appendChild(tbody);

//创建第一行
var row1 = document.createElement("tr");
tbody.appendChild(row1);
var cell1_1 = document.createElement("td");
cell1_1.appendChild(document.createTextNode("Cell 1,1"));
row1.appendChild(cell1_1);
var cell2_1 = document.createElement("td");
cell2_1.appendChild(document.createTextNode("Cell 2,1"));
row1.appendChild(cell2_1);

//创建第二行
var row2 = document.createElement("tr");
tbody.appendChild(row2);
var cell1_2 = document.createElement("td");
cell1_2.appendChild(document.createTextNode("Cell 1,2"));
row2.appendChild(cell1_2);
var cell2_2= document.createElement("td");
cell2_2.appendChild(document.createTextNode("Cell 2,2"));
row2.appendChild(cell2_2);

//将表格添加到文档主体中
document.body.appendChild(table);
```

显然， DOM 代码很长，还有点不太好懂。为了方便构建表格， HTML DOM 还为`<table>`、 `<tbody>`和`<tr>`元素添加了一些属性和方法。为`<table>`元素添加的属性和方法如下。

- caption：保存着对`<caption>`元素（如果有）的指针。
- tBodies：是一个`<tbody>`元素的 HTMLCollection。
- tFoot：保存着对`<tfoot>`元素（如果有）的指针。
- tHead：保存着对`<thead>`元素（如果有）的指针。
- rows：是一个表格中所有行的 HTMLCollection。
- createTHead()：创建`<thead>`元素，将其放到表格中，返回引用。
- createTFoot()：创建`<tfoot>`元素，将其放到表格中，返回引用。
- createCaption()：创建`<caption>`元素，将其放到表格中，返回引用。
- deleteTHead()：删除`<thead>`元素。
- deleteTFoot()：删除`<tfoot>`元素。
- deleteCaption()：删除`<caption>`元素。
- deleteRow(pos)：删除指定位置的行。
- insertRow(pos)：向 rows 集合中的指定位置插入一行。

为`<tbody>`元素添加的属性和方法如下。

- rows：保存着`<tbody>`元素中行的 HTMLCollection。
- deleteRow(pos)：删除指定位置的行。
- insertRow(pos)：向 rows 集合中的指定位置插入一行，返回对新插入行的引用。

为`<tr>`元素添加的属性和方法如下。

- cells：保存着`<tr>`元素中单元格的 HTMLCollection。
- deleteCell(pos)：删除指定位置的单元格。
- insertCell(pos)：向 cells 集合中的指定位置插入一个单元格，返回对新插入单元格的引用。

使用这些属性和方法，可以极大地减少创建表格所需的代码数量。例如，使用这些属性和方法可以将前面的代码重写如下（加阴影的部分是重写后的代码）。

```js
//创建 table
var table = document.createElement("table");
table.border = 1;
table.width = "100%";

//创建 tbody
var tbody = document.createElement("tbody");
table.appendChild(tbody);

//创建第一行
tbody.insertRow(0);
tbody.rows[0].insertCell(0);
tbody.rows[0].cells[0].appendChild(document.createTextNode("Cell 1,1"));
tbody.rows[0].insertCell(1);
tbody.rows[0].cells[1].appendChild(document.createTextNode("Cell 2,1"));

//创建第二行
tbody.insertRow(1);
tbody.rows[1].insertCell(0);
tbody.rows[1].cells[0].appendChild(document.createTextNode("Cell 1,2"));
tbody.rows[1].insertCell(1);
tbody.rows[1].cells[1].appendChild(document.createTextNode("Cell 2,2"));

//将表格添加到文档主体中
document.body.appendChild(table);
```

在这次的代码中，创建`<table>`和`<tbody>`的代码没有变化。不同的是创建两行的部分，其中使用了 HTML DOM 定义的表格属性和方法。在创建第一行时，通过`<tbody>`元素调用了`insertRow()`方法，传入了参数 0——表示应该将插入的行放在什么位置上。执行这一行代码后，就会自动创建一行并将其插入到`<tbody>`元素的位置 0 上，因此就可以马上通过`tbody.rows[0]`来引用新插入的行。

创建单元格的方式也十分相似，即通过`<tr>`元素调用`insertCell()`方法并传入放置单元格的位置。然后，就可以通过`tbody.rows[0].cells[0]`来引用新插入的单元格，因为新创建的单元格被插入到了这一行的位置 0 上。

总之，使用这些属性和方法创建表格的逻辑性更强，也更容易看懂，尽管技术上这两套代码都是正确的。

### 10.2.4 使用NodeList

理解 NodeList 及其“近亲” NamedNodeMap 和 HTMLCollection ，是从整体上透彻理解 DOM 的关键所在。这三个集合都是“动态的”；换句话说，每当文档结构发生变化时，它们都会得到更新。因此，它们始终都会保存着最新、最准确的信息。从本质上说，所有 NodeList 对象都是在访问 DOM 文档时实时运行的查询。例如，下列代码会导致无限循环：

```js
var divs = document.getElementsByTagName("div"),
  i,
  div;
for (i=0; i < divs.length; i++){
  div = document.createElement("div");
  document.body.appendChild(div);
}
```

第一行代码会取得文档中所有`<div>`元素的 HTMLCollection。由于这个集合是“动态的”，因此只要有新`<div>`元素被添加到页面中，这个元素也会被添加到该集合中。浏览器不会将创建的所有集合都保存在一个列表中，而是在下一次访问集合时再更新集合。结果，在遇到上例中所示的循环代码时，就会导致一个有趣的问题。每次循环都要对条件 `i < divs.length` 求值，意味着会运行取得所有`<div>`元素的查询。考虑到循环体每次都会创建一个新`<div>`元素并将其添加到文档中，因此`divs.length` 的值在每次循环后都会递增。既然 i 和 `divs.length` 每次都会同时递增，结果它们的值永远也不会相等。

如果想要迭代一个 NodeList，最好是使用 length 属性初始化第二个变量，然后将迭代器与该变量进行比较，如下面的例子所示：

```js
var divs = document.getElementsByTagName("div"),
  i,
  len,
  div;
for (i=0, len=divs.length; i < len; i++){
  div = document.createElement("div");
  document.body.appendChild(div);
}
```

这个例子中初始化了第二个变量 len。由于 len 中保存着对 `divs.length` 在循环开始时的一个快照，因此就会避免上一个例子中出现的无限循环问题。在本章演示迭代 NodeList 对象的例子中，使用的都是这种更为保险的方式。

一般来说，应该尽量减少访问 NodeList 的次数。因为每次访问 NodeList，都会运行一次基于文档的查询。所以，可以考虑将从 NodeList 中取得的值缓存起来。

## 10.3 小结　

DOM 是语言中立的 API，用于访问和操作 HTML 和 XML 文档。 DOM1 级将 HTML 和 XML 文档形象地看作一个层次化的节点树，可以使用 JavaScript 来操作这个节点树，进而改变底层文档的外观和
结构。

DOM 由各种节点构成，简要总结如下。

- 最基本的节点类型是 Node，用于抽象地表示文档中一个独立的部分；所有其他类型都继承自 Node。
- Document 类型表示整个文档，是一组分层节点的根节点。在 JavaScript 中， document 对象是 Document 的一个实例。使用 document 对象，有很多种方式可以查询和取得节点。
- Element 节点表示文档中的所有 HTML 或 XML 元素，可以用来操作这些元素的内容和特性。
- 另外还有一些节点类型，分别表示文本内容、注释、文档类型、 CDATA 区域和文档片段。

访问 DOM 的操作在多数情况下都很直观，不过在处理`<script>`和`<style>`元素时还是存在一些复杂性。由于这两个元素分别包含脚本和样式信息，因此浏览器通常会将它们与其他元素区别对待。这些区别导致了在针对这些元素使用 innerHTML 时，以及在创建新元素时的一些问题。

理解 DOM 的关键，就是理解 DOM 对性能的影响。 DOM 操作往往是 JavaScript 程序中开销最大的部分，而因访问 NodeList 导致的问题为最多。 NodeList 对象都是“动态的”，这就意味着每次访问 NodeList 对象，都会运行一次查询。有鉴于此，最好的办法就是尽量减少 DOM 操作。

# 第11章 DOM扩展

尽管 DOM 作为 API 已经非常完善了，但为了实现更多的功能，仍然会有一些标准或专有的扩展。 2008 年之前，浏览器中几乎所有的 DOM 扩展都是专有的。此后， W3C 着手将一些已经成为事实标准的专有扩展标准化并写入规范当中。

对 DOM 的两个主要的扩展是 Selectors API（选择符 API）和 HTML5。这两个扩展都源自开发社区，而将某些常见做法及 API 标准化一直是众望所归。此外，还有一个不那么引人瞩目的 Element Traversal（元素遍历）规范，为 DOM 添加了一些属性。虽然前述两个主要规范（特别是 HTML5）已经涵盖了大量的 DOM 扩展，但专有扩展依然存在。本章也会介绍专有的 DOM 扩展。

## 11.1 选择符API 

众多 JavaScript 库中最常用的一项功能，就是根据 CSS 选择符选择与某个模式匹配的 DOM 元素。实际上， [jQuery](www.jquery.com)的核心就是通过 CSS 选择符查询 DOM 文档取得元素的引用，从而抛开了`getElementById()`和`getElementsByTagName()`。

[Selectors API](www.w3.org/TR/selectors-api/)是由 W3C 发起制定的一个标准，致力于让浏览器原生支持 CSS 查询。所有实现这一功能的 JavaScript 库都会写一个基础的 CSS 解析器，然后再使用已有的 DOM 方法查询文档并找到匹配的节点。尽管库开发人员在不知疲倦地改进这一过程的性能，但到头来都只能通过运行 JavaScript 代码来完成查询操作。而把这个功能变成原生 API 之后，解析和树查询操作可以在浏览器内部通过编译后的代码来完成，极大地改善了性能。

Selectors API Level 1 的核心是两个方法：`querySelector()`和`querySelectorAll()`。在兼容的浏览器中，可以通过 Document 及 Element 类型的实例调用它们。目前已完全支持 Selectors API Level 1 的浏览器有 IE 8+、 Firefox 3.5+、 Safari 3.1+、 Chrome 和 Opera 10+。

### 11.1.1 querySelector()方法

`querySelector()`方法接收一个 CSS 选择符，返回与该模式匹配的第一个元素，如果没有找到匹配的元素，返回 null。请看下面的例子。

```js
//取得 body 元素
var body = document.querySelector("body");
//取得 ID 为"myDiv"的元素
var myDiv = document.querySelector("#myDiv");
//取得类为"selected"的第一个元素
var selected = document.querySelector(".selected");
//取得类为"button"的第一个图像元素
var img = document.body.querySelector("img.button");
```

通过 Document 类型调用 `querySelector()`方法时，会在文档元素的范围内查找匹配的元素。而通过 Element 类型调用 `querySelector()`方法时，只会在该元素后代元素的范围内查找匹配的元素。

CSS 选择符可以简单也可以复杂，视情况而定。如果传入了不被支持的选择符， `querySelector()`会抛出错误。

### 11.1.2 querySelectorAll()方法

`querySelectorAll()`方法接收的参数与 `querySelector()`方法一样，都是一个 CSS 选择符，但返回的是所有匹配的元素而不仅仅是一个元素。这个方法返回的是一个 NodeList 的实例。

具体来说，返回的值实际上是带有所有属性和方法的 NodeList，而其底层实现则类似于一组元素的快照，而非不断对文档进行搜索的动态查询。这样实现可以避免使用 NodeList 对象通常会引起的大多数性能问题。

只要传给 `querySelectorAll()`方法的 CSS 选择符有效，该方法都会返回一个 NodeList 对象，而不管找到多少匹配的元素。如果没有找到匹配的元素， NodeList 就是空的。

与 `querySelector()`类似，能够调用 `querySelectorAll()`方法的类型包括 Document、DocumentFragment 和 Element。下面是几个例子。

```js
//取得某<div>中的所有<em>元素（类似于 getElementsByTagName("em")）
var ems = document.getElementById("myDiv").querySelectorAll("em");

//取得类为"selected"的所有元素
var selecteds = document.querySelectorAll(".selected");

//取得所有<p>元素中的所有<strong>元素
var strongs = document.querySelectorAll("p strong");
```

要取得返回的 NodeList 中的每一个元素，可以使用`item()`方法，也可以使用方括号语法，比如：

```js
var i, len, strong;
for (i = 0, len = strongs.length; i < len; i++){
  strong = strongs[i]; //或者 strongs.item(i)
  strong.className = "important";
}
```

同样与 `querySelector()`类似，如果传入了浏览器不支持的选择符或者选择符中有语法错误，`querySelectorAll()`会抛出错误。

### 11.1.3 matchesSelector()方法

Selectors API Level 2 规范为 Element 类型新增了一个方法`matchesSelector()`。这个方法接收一个参数，即 CSS 选择符，如果调用元素与该选择符匹配，返回 true；否则，返回 false。看例子。

```js
if (document.body.matchesSelector("body.page1")){
  //true
}
```

在取得某个元素引用的情况下，使用这个方法能够方便地检测它是否会被 `querySelector()`或`querySelectorAll()`方法返回。

截至 2011 年年中，还没有浏览器支持`matchesSelector()`方法；不过，也有一些实验性的实现。IE 9+通过`msMatchesSelector()`支持该方法，Firefox 3.6+通过 `mozMatchesSelector()`支持该方法，Safari 5+和 Chrome 通过 `webkitMatchesSelector()`支持该方法。因此，如果你想使用这个方法，最好是编写一个包装函数。

```js
function matchesSelector(element, selector){
  if (element.matchesSelector){
    return element.matchesSelector(selector);
  } else if (element.msMatchesSelector){
    return element.msMatchesSelector(selector);
  } else if (element.mozMatchesSelector){
    return element.mozMatchesSelector(selector);
  } else if (element.webkitMatchesSelector){
    return element.webkitMatchesSelector(selector);
  } else {
    throw new Error("Not supported.");
  }
}
if (matchesSelector(document.body, "body.page1")){
  //执行操作
}
```

## 11.2 元素遍历 

对于元素间的空格， IE9 及之前版本不会返回文本节点，而其他所有浏览器都会返回文本节点。这样，就导致了在使用 childNodes 和 firstChild 等属性时的行为不一致。为了弥补这一差异，而同时又保持 DOM 规范不变， [Element Traversal 规范](www.w3.org/TR/ElementTraversal/)新定义了一组属性。Element Traversal API 为 DOM 元素添加了以下 5 个属性。

- childElementCount：返回子元素（不包括文本节点和注释）的个数。
- firstElementChild：指向第一个子元素； firstChild 的元素版。
- lastElementChild：指向最后一个子元素； lastChild 的元素版。
- previousElementSibling：指向前一个同辈元素； previousSibling 的元素版。
- nextElementSibling：指向后一个同辈元素； nextSibling 的元素版。

支持的浏览器为 DOM 元素添加了这些属性，利用这些元素不必担心空白文本节点，从而可以更方便地查找 DOM 元素了。

下面来看一个例子。过去，要跨浏览器遍历某元素的所有子元素，需要像下面这样写代码。

```js
var i,
  len,
child = element.firstChild;
while(child != element.lastChild){
  if (child.nodeType == 1){ //检查是不是元素
    processChild(child);
  }
  child = child.nextSibling;
}
```

而使用 Element Traversal 新增的元素，代码会更简洁。

```js
var i,
  len,
child = element.firstElementChild;
while(child != element.lastElementChild){
  processChild(child); //已知其是元素
  child = child.nextElementSibling;
}
```

支持 Element Traversal 规范的浏览器有 IE 9+、 Firefox 3.5+、 Safari 4+、 Chrome 和 Opera 10+。

## 11.3 HTML5 

对于传统 HTML 而言， HTML5 是一个叛逆。所有之前的版本对 JavaScript 接口的描述都不过三言两语，主要篇幅都用于定义标记，与 JavaScript 相关的内容一概交由 DOM 规范去定义。

而 HTML5 规范则围绕如何使用新增标记定义了大量 JavaScript API。其中一些 API 与 DOM 重叠，定义了浏览器应该支持的 DOM 扩展。

> 因为 HTML5 涉及的面非常广，本节只讨论与 DOM 节点相关的内容。 HTML5 的其他相关内容将在本书其他章节中穿插介绍。

### 11.3.1 与类相关的扩充

HTML4 在 Web 开发领域得到广泛采用后导致了一个很大的变化，即 class 属性用得越来越多，一方面可以通过它为元素添加样式，另一方面还可以用它表示元素的语义。于是，自然就有很多 JavaScript 代码会来操作 CSS 类，比如动态修改类或者搜索文档中具有给定类或给定的一组类的元素，等等。为了让开发人员适应并增加对 class 属性的新认识， HTML5 新增了很多 API，致力于简化 CSS 类的用法。

**1. getElementsByClassName()方法**

HTML5 添加的`getElementsByClassName()`方法是最受人欢迎的一个方法，可以通过 document 对象及所有 HTML 元素调用该方法。这个方法最早出现在 JavaScript 库中，是通过既有的 DOM 功能实现的，而原生的实现具有极大的性能优势。

`getElementsByClassName()`方法接收一个参数，即一个包含一或多个类名的字符串，返回带有指定类的所有元素的 NodeList。传入多个类名时，类名的先后顺序不重要。来看下面的例子。

```js
//取得所有类中包含"username"和"current"的元素，类名的先后顺序无所谓
var allCurrentUsernames = document.getElementsByClassName("username current");

//取得 ID 为"myDiv"的元素中带有类名"selected"的所有元素
var selected = document.getElementById("myDiv").getElementsByClassName("selected");
```

调用这个方法时，只有位于调用元素子树中的元素才会返回。在 document 对象上调用`getElementsByClassName()`始终会返回与类名匹配的所有元素，在元素上调用该方法就只会返回后代元素中匹配的元素。

使用这个方法可以更方便地为带有某些类的元素添加事件处理程序，从而不必再局限于使用 ID 或标签名。 不过别忘了，因为返回的对象是 NodeList， 所以使用这个方法与使用 `getElementsByTagName()`以及其他返回 NodeList 的 DOM 方法都具有同样的性能问题。支持`getElementsByClassName()`方法的浏览器有 IE 9+、 Firefox 3+、 Safari 3.1+、 Chrome 和 Opera 9.5+。

**2. classList 属性**

在操作类名时，需要通过 className 属性添加、删除和替换类名。因为 className 中是一个字符串，所以即使只修改字符串一部分，也必须每次都设置整个字符串的值。比如，以下面的 HTML 代码为例。

```js
<div class="bd user disabled">...</div>
```

这个`<div>`元素一共有三个类名。要从中删除一个类名，需要把这三个类名拆开，删除不想要的那
个，然后再把其他类名拼成一个新字符串。请看下面的例子。

```js
// 删除"user"类
// 首先，取得类名字符串并拆分成数组
var classNames = div.className.split(/\s+/);
// 找到要删的类名
var pos = -1,
  i,
  len;
for (i=0, len=classNames.length; i < len; i++){
  if (classNames[i] == "user"){
    pos = i;
    break;
  }
}
// 删除类名
classNames.splice(i,1);
// 把剩下的类名拼成字符串并重新设置
div.className = classNames.join(" ");
```

为了从`<div>`元素的 class 属性中删除"user"，以上这些代码都是必需的。必须得通过类似的算法替换类名并确认元素中是否包含该类名。添加类名可以通过拼接字符串完成，但必须要通过检测确定不会多次添加相同的类名。很多 JavaScript 库都实现了这个方法，以简化这些操作。

HTML5 新增了一种操作类名的方式，可以让操作更简单也更安全，那就是为所有元素添加 classList 属性。这个 classList 属性是新集合类型 DOMTokenList 的实例。与其他 DOM 集合类似， DOMTokenList 有一个表示自己包含多少元素的 length 属性，而要取得每个元素可以使用`item()`方法，也可以使用方括号语法。此外，这个新类型还定义如下方法。

- add(value)：将给定的字符串值添加到列表中。如果值已经存在，就不添加了。
- contains(value)：表示列表中是否存在给定的值，如果存在则返回 true，否则返回 false。
- remove(value)：从列表中删除给定的字符串。
- toggle(value)：如果列表中已经存在给定的值，删除它；如果列表中没有给定的值，添加它。

这样，前面那么多行代码用下面这一行代码就可以代替了：

```js
div.classList.remove("user");
```

以上代码能够确保其他类名不受此次修改的影响。其他方法也能极大地减少类似基本操作的复杂性，如下面的例子所示。

```js
// 删除"disabled"类
div.classList.remove("disabled");

// 添加"current"类
div.classList.add("current");

// 切换"user"类
div.classList.toggle("user");

// 确定元素中是否包含既定的类名
if (div.classList.contains("bd") && !div.classList.contains("disabled")){
  // 执行操作
}

// 迭代类名
for (var i=0, len=div.classList.length; i < len; i++){
  doSomething(div.classList[i]);
}
```

有了 classList 属性，除非你需要全部删除所有类名，或者完全重写元素的 class 属性，否则也就用不到 className 属性了。

支持 classList 属性的浏览器有 Firefox 3.6+和 Chrome。

### 11.3.2 焦点管理

HTML5 也添加了辅助管理 DOM 焦点的功能。首先就是 `document.activeElement` 属性，这个属性始终会引用 DOM 中当前获得了焦点的元素。元素获得焦点的方式有页面加载、用户输入（通常是通过按 Tab 键）和在代码中调用 `focus()`方法。来看几个例子。

```js
var button = document.getElementById("myButton");
button.focus();
alert(document.activeElement === button); //true
```

默认情况下，文档刚刚加载完成时， `document.activeElement` 中保存的是 document.body 元素的引用。文档加载期间， `document.activeElement` 的值为 null。

另外就是新增了 `document.hasFocus()`方法，这个方法用于确定文档是否获得了焦点。

```js
var button = document.getElementById("myButton");
button.focus();
alert(document.hasFocus()); //true
```

通过检测文档是否获得了焦点，可以知道用户是不是正在与页面交互。

查询文档获知哪个元素获得了焦点，以及确定文档是否获得了焦点，这两个功能最重要的用途是提高 Web 应用的无障碍性。无障碍 Web 应用的一个主要标志就是恰当的焦点管理，而确切地知道哪个元素获得了焦点是一个极大的进步，至少我们不用再像过去那样靠猜测了。

实现了这两个属性的浏览器的包括 IE 4+、 Firefox 3+、 Safari 4+、 Chrome 和 Opera 8+。

### 11.3.3 HTMLDocument的变化

HTML5 扩展了 HTMLDocument，增加了新的功能。与 HTML5 中新增的其他 DOM 扩展类似，这些变化同样基于那些已经得到很多浏览器完美支持的专有扩展。所以，尽管这些扩展被写入标准的时间相对不长，但很多浏览器很早就已经支持这些功能了。

**1. readyState 属性**

IE4 最早为 document 对象引入了 readyState 属性。然后，其他浏览器也都陆续添加这个属性，最终 HTML5 把这个属性纳入了标准当中。 Document 的 readyState 属性有两个可能的值：

- loading，正在加载文档；
- complete，已经加载完文档。

使用 `document.readyState` 的最恰当方式，就是通过它来实现一个指示文档已经加载完成的指示器。在这个属性得到广泛支持之前，要实现这样一个指示器，必须借助 onload 事件处理程序设置一个标签，表明文档已经加载完毕。 `document.readyState` 属性的基本用法如下。

```js
if (document.readyState == "complete"){
  //执行操作
}
```

支持 readyState 属性的浏览器有 IE4+、 Firefox 3.6+、 Safari、 Chrome 和 Opera 9+。

**2. 兼容模式**

自从 IE6 开始区分渲染页面的模式是标准的还是混杂的，检测页面的兼容模式就成为浏览器的必要功能。 IE 为此给 document 添加了一个名为 compatMode 的属性，这个属性就是为了告诉开发人员浏览器采用了哪种渲染模式。就像下面例子中所展示的那样，在标准模式下， `document.compatMode` 的值等于"CSS1Compat"，而在混杂模式下， `document.compatMode` 的值等于"BackCompat"。

```js
if (document.compatMode == "CSS1Compat"){
  alert("Standards mode");
} else {
  alert("Quirks mode");
}
```

后来，陆续实现这个属性的浏览器有 Firefox、 Safari 3.1+、 Opera 和 Chrome。最终， HTML5 也把这个属性纳入标准，对其实现做出了明确规定。

**3. head 属性**

作为对 `document.body` 引用文档的`<body>`元素的补充， HTML5 新增了`document.head`属性，引用文档的`<head>`元素。要引用文档的`<head>`元素，可以结合使用这个属性和另一种后备方法。

```js
var head = document.head || document.getElementsByTagName("head")[0];
```

如果可用，就使用 `document.head`，否则仍然使用 `getElementsByTagName()`方法。

实现 `document.head` 属性的浏览器包括 Chrome 和 Safari 5。

### 11.3.4 字符集属性

HTML5 新增了几个与文档字符集有关的属性。其中， charset 属性表示文档中实际使用的字符集，也可以用来指定新字符集。默认情况下，这个属性的值为"UTF-16"，但可以通过`<meta>`元素、响应头部或直接设置 charset 属性修改这个值。来看一个例子。

```js
alert(document.charset); //"UTF-16"
document.charset = "UTF-8";
```

另一个属性是 defaultCharset，表示根据默认浏览器及操作系统的设置，当前文档默认的字符集应该是什么。如果文档没有使用默认的字符集，那 charset 和 defaultCharset 属性的值可能会不一样，例如：

```js
if (document.charset != document.defaultCharset){
  alert("Custom character set being used.");
}
```

通过这两个属性可以得到文档使用的字符编码的具体信息，也能对字符编码进行准确地控制。运行适当的情况下，可以保证用户正常查看页面或使用应用。

支持 `document.charset` 属性的浏览器有 IE、 Firefox、 Safari、 Opera 和 Chrome。支持 `document.defaultCharset` 属性的浏览器有 IE、 Safari 和 Chrome。

### 11.3.5 自定义数据属性

HTML5 规定可以为元素添加非标准的属性，但要添加前缀 data-，目的是为元素提供与渲染无关的信息，或者提供语义信息。这些属性可以任意添加、随便命名，只要以`data-`开头即可。来看一个例子。

```js
<div id="myDiv" data-appId="12345" data-myname="Nicholas"></div>
```

添加了自定义属性之后，可以通过元素的 dataset 属性来访问自定义属性的值。 dataset 属性的值是 DOMStringMap 的一个实例，也就是一个名值对儿的映射。在这个映射中，每个 data-name 形式的属性都会有一个对应的属性，只不过属性名没有 data-前缀（比如，自定义属性是 data-myname，那映射中对应的属性就是 myname）。还是看一个例子吧。

```js
//本例中使用的方法仅用于演示
var div = document.getElementById("myDiv");
//取得自定义属性的值
var appId = div.dataset.appId;
var myName = div.dataset.myname;
//设置值
div.dataset.appId = 23456;
div.dataset.myname = "Michael";
//有没有"myname"值呢？
if (div.dataset.myname){
  alert("Hello, " + div.dataset.myname);
}
```

如果需要给元素添加一些不可见的数据以便进行其他处理，那就要用到自定义数据属性。在跟踪链接或混搭应用中，通过自定义数据属性能方便地知道点击来自页面中的哪个部分。

在编写本书时，支持自定义数据属性的浏览器有 Firefox 6+和 Chrome。

### 11.3.6 插入标记

虽然 DOM 为操作节点提供了细致入微的控制手段，但在需要给文档插入大量新 HTML 标记的情况下，通过 DOM 操作仍然非常麻烦，因为不仅要创建一系列 DOM 节点，而且还要小心地按照正确的顺序把它们连接起来。相对而言，使用插入标记的技术，直接插入 HTML 字符串不仅更简单，速度也更快。以下与插入标记相关的 DOM 扩展已经纳入了 HTML5 规范。

**1. innerHTML 属性**

在读模式下， innerHTML 属性返回与调用元素的所有子节点（包括元素、注释和文本节点）对应的 HTML 标记。在写模式下， innerHTML 会根据指定的值创建新的 DOM 树，然后用这个 DOM 树完全替换调用元素原先的所有子节点。下面是一个例子。

```html
<div id="content">
  <p>This is a <strong>paragraph</strong> with a list following it.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
</div>
```

对于上面的`<div>`元素来说，它的 innerHTML 属性会返回如下字符串。

```html
<p>This is a <strong>paragraph</strong> with a list following it.</p>
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
  <li>Item 3</li>
</ul>
```

但是，不同浏览器返回的文本格式会有所不同。IE 和 Opera 会将所有标签转换为大写形式，而 Safari、 Chrome 和 Firefox 则会原原本本地按照原先文档中（或指定这些标签时）的格式返回 HTML，包括空格和缩进。不要指望所有浏览器返回的 innerHTML 值完全相同。

在写模式下， innerHTML 的值会被解析为 DOM 子树，替换调用元素原来的所有子节点。因为它的值被认为是 HTML，所以其中的所有标签都会按照浏览器处理 HTML 的标准方式转换为元素（同样，这里的转换结果也因浏览器而异）。如果设置的值仅是文本而没有 HTML 标签，那么结果就是设置纯文本，如下所示。

```js
div.innerHTML = "Hello world!";
```

为 innerHTML 设置的包含 HTML 的字符串值与解析后 innerHTML 的值大不相同。来看下面的
例子。

```js
div.innerHTML = "Hello & welcome, <b>\"reader\"!</b>";
```

以上操作得到的结果如下：

```html
<div id="content">Hello &amp; welcome, <b>&quot;reader&quot;!</b></div>
```

设置了 innerHTML 之后，可以像访问文档中的其他节点一样访问新创建的节点。

> 为 innerHTML 设置 HTML 字符串后，浏览器会将这个字符串解析为相应的 DOM 树。因此设置了 innerHTML 之后，再从中读取 HTML 字符串，会得到与设置时不一样的结果。原因在于返回的字符串是根据原始 HTML 字符串创建的 DOM 树经过序列化之后的结果。

使用 innerHTML 属性也有一些限制。比如，在大多数浏览器中，通过 innerHTML 插入`<script>`元素并不会执行其中的脚本。 IE8 及更早版本是唯一能在这种情况下执行脚本的浏览器，但必须满足一些条件。一是必须为`<script>`元素指定 defer 属性，二是`<script>`元素必须位于（微软所谓的）“有作用域的元素”（ scoped element）之后。 `<script>`元素被认为是“无作用域的元素”（ NoScope element），也就是在页面中看不到的元素，与`<style>`元素或注释类似。如果通过 innerHTML 插入的字符串开头就是一个“无作用域的元素”，那么 IE 会在解析这个字符串前先删除该元素。换句话说，以下代码达不到目的：

```js
div.innerHTML = "<script defer>alert('hi');<\/script>"; //无效
```

此时， innerHTML 字符串一开始（而且整个）就是一个“无作用域的元素”，所以这个字符串会变成空字符串。如果想插入这段脚本，必须在前面添加一个“有作用域的元素”，可以是一个文本节点，也可以是一个没有结束标签的元素如`<input>`。例如，下面这几行代码都可以正常执行：

```js
div.innerHTML = "_<script defer>alert('hi');<\/script>";
div.innerHTML = "<div>&nbsp;</div><script defer>alert('hi');<\/script>";
div.innerHTML = "<input type=\"hidden\"><script defer>alert('hi');<\/script>";
```

第一行代码会在`<script>`元素前插入一个文本节点。事后，为了不影响页面显示，你可能需要移除这个文本节点。第二行代码采用的方法类似，只不过使用的是一个包含非换行空格的`<div>`元素。如果仅仅插入一个空的`<div>`元素，还是不行；必须要包含一点儿内容，浏览器才会创建文本节点。同样，为了不影响页面布局，恐怕还得移除这个节点。第三行代码使用的是一个隐藏的`<input>`域，也能达到相同的效果。不过，由于隐藏的`<input>`域不影响页面布局，因此这种方式在大多数情况下都是首选。大多数浏览器都支持以直观的方式通过 innerHTML 插入`<style>`元素，例如：

```js
div.innerHTML = "<style type=\"text/css\">body {background-color: red; }</style>";
```

但在 IE8 及更早版本中， `<style>`也是一个“没有作用域的元素”，因此必须像下面这样给它前置一个“有作用域的元素”：

```js
div.innerHTML = "_<style type=\"text/css\">body {background-color: red; }</style>";
div.removeChild(div.firstChild);
```

并不是所有元素都支持 innerHTML 属性。不支持 innerHTML 的元素有： `<col>`、 `<colgroup>`、`<frameset>`、 `<head>`、 `<html>`、 `<style>`、 `<table>`、 `<tbody>`、 `<thead>`、 `<tfoot>`和`<tr>`。此外，在 IE8 及更早版本中，` <title>`元素也没有 innerHTML 属性。

> Firefox 对在内容类型为 application/xhtml+xml 的 XHTML 文档中设置 innerHTML有严格的限制。在 XHTML 文档中使用 innerHTML 时， XHTML 代码必须完全符合要求。如果代码格式不正确，设置 innerHTML 将会静默地失败。

无论什么时候，只要使用 innerHTML 从外部插入 HTML，都应该首先以可靠的方式处理 HTML。IE8 为此提供了 `window.toStaticHTML()`方法，这个方法接收一个参数，即一个 HTML 字符串；返回
一个经过无害处理后的版本——从源 HTML 中删除所有脚本节点和事件处理程序属性。下面就是一个例子：

```js
var text = "<a href=\"#\" onclick=\"alert('hi')\">Click Me</a>";
var sanitized = window.toStaticHTML(text); //Internet Explorer 8 only
alert(sanitized); //"<a href=\"#\">Click Me</a>"
```

这个例子将一个 HTML 链接字符串传给了`toStaticHTML()`方法，得到的无害版本中去掉了 onclick 属性。虽然目前只有 IE8 原生支持这个方法，但我们还是建议读者在通过 innerHTML 插入代码之前，尽可能先手工检查一下其中的文本内容。

**2. outerHTML 属性**

在读模式下， outerHTML 返回调用它的元素及所有子节点的 HTML 标签。 在写模式下， outerHTML 会根据指定的 HTML 字符串创建新的 DOM 子树，然后用这个 DOM 子树完全替换调用元素。下面是一个例子。

```html
<div id="content">
  <p>This is a <strong>paragraph</strong> with a list following it.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
</div>
```

如果在`<div>`元素上调用 outerHTML，会返回与上面相同的代码，包括`<div>`本身。不过，由于浏览器解析和解释 HTML 标记的不同，结果也可能会有所不同。（这里的不同与使用 innerHTML 属性时存在的差异性质是一样的。）

使用 outerHTML 属性以下面这种方式设置值：

```js
div.outerHTML = "<p>This is a paragraph.</p>";
```

这行代码完成的操作与下面这些 DOM 脚本代码一样：

```js
var p = document.createElement("p");
p.appendChild(document.createTextNode("This is a paragraph."));
div.parentNode.replaceChild(p, div);
```

结果，就是新创建的`<p>`元素会取代 DOM 树中的`<div>`元素。

支持 outerHTML 属性的浏览器有 IE4+、 Safari 4+、 Chrome 和 Opera 8+。 Firefox 7 及之前版本都不支持 outerHTML 属性。

**3. insertAdjacentHTML()方法**

插入标记的最后一个新增方式是 `insertAdjacentHTML()`方法。这个方法最早也是在IE中出现的，它接收两个参数：插入位置和要插入的 HTML 文本。第一个参数必须是下列值之一：

- "beforebegin"，在当前元素之前插入一个紧邻的同辈元素；
- "afterbegin"， 在当前元素之下插入一个新的子元素或在第一个子元素之前再插入新的子元素；
- "beforeend"， 在当前元素之下插入一个新的子元素或在最后一个子元素之后再插入新的子元素；
- "afterend"，在当前元素之后插入一个紧邻的同辈元素。

注意，这些值都必须是小写形式。第二个参数是一个 HTML 字符串（与 innerHTML 和 outerHTML 的值相同），如果浏览器无法解析该字符串，就会抛出错误。以下是这个方法的基本用法示例。

```js
//作为前一个同辈元素插入
element.insertAdjacentHTML("beforebegin", "<p>Hello world!</p>");

//作为第一个子元素插入
element.insertAdjacentHTML("afterbegin", "<p>Hello world!</p>");

//作为最后一个子元素插入
element.insertAdjacentHTML("beforeend", "<p>Hello world!</p>");

//作为后一个同辈元素插入
element.insertAdjacentHTML("afterend", "<p>Hello world!</p>");
```

支持`insertAdjacentHTML()`方法的浏览器有 IE、 Firefox 8+、 Safari、 Opera 和 Chrome。

**4. 内存与性能问题**

使用本节介绍的方法替换子节点可能会导致浏览器的内存占用问题，尤其是在 IE 中，问题更加明显。在删除带有事件处理程序或引用了其他 JavaScript 对象子树时，就有可能导致内存占用问题。假设某个元素有一个事件处理程序（或者引用了一个 JavaScript 对象作为属性），在使用前述某个属性将该元素从文档树中删除后，元素与事件处理程序（或 JavaScript 对象）之间的绑定关系在内存中并没有一并删除。如果这种情况频繁出现，页面占用的内存数量就会明显增加。因此，在使用 innerHTML、 outerHTML 属性和 `insertAdjacentHTML()`方法时，最好先手工删除要被替换的元素的所有事件处理程序和 JavaScript 对象属性（第 13 章将进一步讨论事件处理程序）。

不过，使用这几个属性——特别是使用 innerHTML，仍然还是可以为我们提供很多便利的。一般来说，在插入大量新 HTML 标记时，使用 innerHTML 属性与通过多次 DOM 操作先创建节点再指定它们之间的关系相比，效率要高得多。这是因为在设置 innerHTML 或 outerHTML 时，就会创建一个 HTML 解析器。这个解析器是在浏览器级别的代码（通常是 C++编写的）基础上运行的，因此比执行 JavaScript 快得多。不可避免地，创建和销毁 HTML 解析器也会带来性能损失，所以最好能够将设置 innerHTML 或 outerHTML 的次数控制在合理的范围内。例如，下列代码使用 innerHTML 创建了很多列表项：

```js
for (var i=0, len=values.length; i < len; i++){
  ul.innerHTML += "<li>" + values[i] + "</li>"; //要避免这种频繁操作！！
}
```

这种每次循环都设置一次 innerHTML 的做法效率很低。而且，每次循环还要从 innerHTML 中读取一次信息，就意味着每次循环要访问两次 innerHTML。最好的做法是单独构建字符串，然后再一次性地将结果字符串赋值给 innerHTML，像下面这样：

```js
var itemsHtml = "";
for (var i=0, len=values.length; i < len; i++){
  itemsHtml += "<li>" + values[i] + "</li>";
}
ul.innerHTML = itemsHtml;
```

这个例子的效率要高得多，因为它只对 innerHTML 执行了一次赋值操作。

### 11.3.7 scrollIntoView()方法

如何滚动页面也是 DOM 规范没有解决的一个问题。为了解决这个问题，浏览器实现了一些方法，以方便开发人员更好地控制页面滚动。在各种专有方法中， HTML5 最终选择了 `scrollIntoView()`作为标准方法。

`scrollIntoView()`可以在所有 HTML 元素上调用，通过滚动浏览器窗口或某个容器元素，调用元素就可以出现在视口中。如果给这个方法传入 true 作为参数，或者不传入任何参数，那么窗口滚动之后会让调用元素的顶部与视口顶部尽可能平齐。如果传入 false 作为参数，调用元素会尽可能全部出现在视口中，（可能的话，调用元素的底部会与视口顶部平齐。）不过顶部不一定平齐，例如：

```js
//让元素可见
document.forms[0].scrollIntoView();
```

当页面发生变化时，一般会用这个方法来吸引用户的注意力。实际上，为某个元素设置焦点也会导致浏览器滚动并显示出获得焦点的元素。

支持 `scrollIntoView()`方法的浏览器有 IE、 Firefox、 Safari 和 Opera。

## 11.4 专有扩展 

虽然所有浏览器开发商都知晓坚持标准的重要性，但在发现某项功能缺失时，这些开发商都会一如既往地向 DOM 中添加专有扩展，以弥补功能上的不足。表面上看，这种各行其事的做法似乎不太好，但实际上专有扩展为 Web 开发领域提供了很多重要的功能，这些功能最终都在 HTML5 规范中得到了标准化。

即便如此，仍然还有大量专有的 DOM 扩展没有成为标准。但这并不是说它们将来不会被写进标准，而只是说在编写本书的时候，它们还是专有功能，而且只得到了少数浏览器的支持。

### 11.4.1 文档模式

IE8 引入了一个新的概念叫“文档模式”（document mode）。页面的文档模式决定了可以使用什么功能。换句话说，文档模式决定了你可以使用哪个级别的 CSS，可以在 JavaScript 中使用哪些 API，以及如何对待文档类型（doctype）。到了 IE9，总共有以下 4 种文档模式。

- IE5：以混杂模式渲染页面（IE5 的默认模式就是混杂模式）。 IE8 及更高版本中的新功能都无法使用。
- IE7：以 IE7 标准模式渲染页面。 IE8 及更高版本中的新功能都无法使用。
- IE8：以 IE8 标准模式渲染页面。 IE8 中的新功能都可以使用，因此可以使用 Selectors API、更多CSS2 级选择符和某些 CSS3 功能，还有一些 HTML5 的功能。不过 IE9 中的新功能无法使用。
- IE9：以 IE9 标准模式渲染页面。 IE9 中的新功能都可以使用，比如 ECMAScript 5、完整的 CSS3 以及更多 HTML5 功能。这个文档模式是最高级的模式。

要理解 IE8 及更高版本的工作原理，必须理解文档模式。

要强制浏览器以某种模式渲染页面，可以使用 HTTP 头部信息 X-UA-Compatible，或通过等价的`<meta>`标签来设置：

```js
<meta http-equiv="X-UA-Compatible" content="IE=IEVersion">
```

注意，这里 IE 的版本（IEVersion）有以下一些不同的值，而且这些值并不一定与上述 4 种文档模式对应。

- Edge：始终以最新的文档模式来渲染页面。忽略文档类型声明。对于 IE8，始终保持以 IE8 标准模式渲染页面。对于 IE9，则以 IE9 标准模式渲染页面。
- EmulateIE9：如果有文档类型声明，则以 IE9 标准模式渲染页面，否则将文档模式设置为 IE5。
- EmulateIE8：如果有文档类型声明，则以 IE8 标准模式渲染页面，否则将文档模式设置为 IE5。
- EmulateIE7：如果有文档类型声明，则以 IE7 标准模式渲染页面，否则将文档模式设置为 IE5。
- 9：强制以 IE9 标准模式渲染页面，忽略文档类型声明。
- 8：强制以 IE8 标准模式渲染页面，忽略文档类型声明。
- 7：强制以 IE7 标准模式渲染页面，忽略文档类型声明。
- 5：强制将文档模式设置为 IE5，忽略文档类型声明。

比如，要想让文档模式像在 IE7 中一样，可以使用下面这行代码：

```js
<meta http-equiv="X-UA-Compatible" content="IE=EmulateIE7">
```

如果不打算考虑文档类型声明，而直接使用 IE7 标准模式，那么可以使用下面这行代码：

```js
<meta http-equiv="X-UA-Compatible" content="IE=7">
```

没有规定说必须在页面中设置 X-UA-Compatible。默认情况下，浏览器会通过文档类型声明来确定是使用最佳的可用文档模式，还是使用混杂模式。

通过 document.documentMode 属性可以知道给定页面使用的是什么文档模式。这个属性是 IE8 中新增的，它会返回使用的文档模式的版本号（在 IE9 中，可能返回的版本号为 5、 7、 8、 9）：

```js
var mode = document.documentMode;
```

知道页面采用的是什么文档模式，有助于理解页面的行为方式。无论在什么文档模式下，都可以访问这个属性。

### 11.4.2 children属性

由于 IE9 之前的版本与其他浏览器在处理文本节点中的空白符时有差异，因此就出现了 children 属性。这个属性是 HTMLCollection 的实例，只包含元素中同样还是元素的子节点。除此之外，children 属性与 childNodes 没有什么区别，即在元素只包含元素子节点时，这两个属性的值相同。

下面是访问 children 属性的示例代码：

```js
var childCount = element.children.length;
var firstChild = element.children[0];
```

支持 children 属性的浏览器有 IE5、 Firefox 3.5、 Safari 2（但有 bug）、 Safari 3（完全支持）、 Opera8 和 Chrome（所有版本）。 IE8 及更早版本的 children 属性中也会包含注释节点，但 IE9 之后的版本则只返回元素节点。

### 11.4.3 contains()方法

在实际开发中，经常需要知道某个节点是不是另一个节点的后代。 IE 为此率先引入了 `contains()` 方法，以便不通过在 DOM 文档树中查找即可获得这个信息。调用 `contains()`方法的应该是祖先节点，
也就是搜索开始的节点，这个方法接收一个参数，即要检测的后代节点。如果被检测的节点是后代节点，该方法返回 true；否则，返回 false。以下是一个例子：

```js
alert(document.documentElement.contains(document.body)); //true
```

这个例子测试了`<body>`元素是不是`<html>`元素的后代，在格式正确的 HTML 页面中，以上代码返回 true。支持 `contains()`方法的浏览器有 IE、 Firefox 9+、 Safari、 Opera 和 Chrome。

使用 DOM Level 3 `compareDocumentPosition()`也能够确定节点间的关系。支持这个方法的浏览器有 IE9+、 Firefox、 Safari、 Opera 9.5+和 Chrome。如前所述，这个方法用于确定两个节点间的关系，返回一个表示该关系的位掩码（bitmask）。下表列出了这个位掩码的值。

| 掩码 | 节点关系 |
|---|---|
| 1 | 无关（给定的节点不在当前文档中） |
| 2 | 居前（给定的节点在DOM树中位于参考节点之前） |
| 4 | 居后（给定的节点在DOM树中位于参考节点之后） |
| 8 | 包含（给定的节点是参考节点的祖先） |
| 16 | 被包含（给定的节点是参考节点的后代） |

为模仿 `contains()`方法，应该关注的是掩码 16。可以对 `compareDocumentPosition()`的结果执行按位与，以确定参考节点（调用 `compareDocumentPosition()`方法的当前节点）是否包含给定的节点（传入的节点）。来看下面的例子：

```js
var result = document.documentElement.compareDocumentPosition(document.body);
alert(!!(result & 16));
```

执行上面的代码后，结果会变成 20（表示“居后”的 4 加上表示“被包含”的 16）。对掩码 16 执行按位操作会返回一个非零数值，而两个逻辑非操作符会将该数值转换成布尔值。

使用一些浏览器及能力检测，就可以写出如下所示的一个通用的 contains 函数：

```js
function contains(refNode, otherNode){
  if (typeof refNode.contains == "function" &&
  (!client.engine.webkit || client.engine.webkit >= 522)){
    return refNode.contains(otherNode);
  } else if (typeof refNode.compareDocumentPosition == "function"){
    return !!(refNode.compareDocumentPosition(otherNode) & 16);
  } else {
    var node = otherNode.parentNode;
    do {
      if (node === refNode){
        return true;
      } else {
        node = node.parentNode;
      }
    } while (node !== null);
    return false;
  }
}
```

这个函数组合使用了三种方式来确定一个节点是不是另一个节点的后代。函数的第一个参数是参考节点，第二个参数是要检查的节点。在函数体内，首先检测 refNode 中是否存在 `contains()`方法（能力检测）。这一部分代码还检查了当前浏览器所用的 WebKit 版本号。如果方法存在而且不是 WebKit（!client.engine.webkit），则继续执行代码。 否则， 如果浏览器是 WebKit 且至少是 Safari 3（WebKit 版本号为 522 或更高），那么也可以继续执行代码。在 WebKit 版本号小于 522 的 Safari 浏览器中，`contains()`方法不能正常使用。

接下来检查是否存在 `compareDocumentPosition()`方法，而函数的最后一步则是自 otherNode 开始向上遍历 DOM 结构，以递归方式取得 parentNode，并检查其是否与 refNode 相等。在文档树的顶端， parentNode 的值等于 null，于是循环结束。这是针对旧版本 Safari 设计的一个后备策略。

### 11.4.4 插入文本

前面介绍过， IE 原来专有的插入标记的属性 innerHTML 和 outerHTML 已经被 HTML5 纳入规范。但另外两个插入文本的专有属性则没有这么好的运气。这两个没有被 HTML5 看中的属性是 innerText 和 outerText。

**1. innerText 属性**

通过 innertText 属性可以操作元素中包含的所有文本内容，包括子文档树中的文本。在通过 innerText 读取值时，它会按照由浅入深的顺序，将子文档树中的所有文本拼接起来。在通过 innerText 写入值时，结果会删除元素的所有子节点，插入包含相应文本值的文本节点。来看下面这个 HTML 代码示例。

```html
<div id="content">
  <p>This is a <strong>paragraph</strong> with a list following it.</p>
  <ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
</div>
```

对于这个例子中的`<div>`元素而言，其 innerText 属性会返回下列字符串：

```
This is a paragraph with a list following it.
Item 1
Item 2
Item 3
```

由于不同浏览器处理空白符的方式不同，因此输出的文本可能会也可能不会包含原始 HTML 代码中的缩进。

使用 innerText 属性设置这个`<div>`元素的内容，则只需一行代码：

```js
div.innerText = "Hello world!";
```

执行这行代码后，页面的 HTML 代码就会变成如下所示。

```html
<div id="content">Hello world!</div>
```

设置innerText属性移除了先前存在的所有子节点，完全改变了 DOM子树。此外，设置innerText 属性的同时，也对文本中存在的 HTML 语法字符（小于号、大于号、引号及和号）进行了编码。再看一个例子。

```js
div.innerText = "Hello & welcome, <b>\"reader\"!</b>";
```

运行以上代码之后，会得到如下所示的结果。

```js
<div id="content">Hello &amp; welcome, &lt;b&gt;&quot;reader&quot;!&lt;/b&gt;</div>
```

设置 innerText 永远只会生成当前节点的一个子文本节点，而为了确保只生成一个子文本节点，就必须要对文本进行 HTML 编码。利用这一点，可以通过 innerText 属性过滤掉 HTML 标签。方法是将 innerText 设置为等于 innerText，这样就可以去掉所有 HTML 标签，比如：

```js
div.innerText = div.innerText;
```

执行这行代码后，就用原来的文本内容替换了容器元素中的所有内容（包括子节点，因而也就去掉了 HTML 标签）。

支持 innerText 属性的浏览器包括 IE4+、 Safari 3+、 Opera 8+和 Chrome。 Firefox 虽然不支持innerText，但支持作用类似的 textContent 属性。 textContent 是 DOM Level 3 规定的一个属性，其他支持 textContent 属性的浏览器还有 IE9+、 Safari 3+、 Opera 10+和 Chrome。为了确保跨浏览器兼容，有必要编写一个类似于下面的函数来检测可以使用哪个属性。

```js
function getInnerText(element){
  return (typeof element.textContent == "string") ?
  element.textContent : element.innerText;
}
function setInnerText(element, text){
  if (typeof element.textContent == "string"){
    element.textContent = text;
  } else {
    element.innerText = text;
  }
}
```

这两个函数都接收一个元素作为参数，然后检查这个元素是不是有 textContent 属性。如果有，那么 typeof element.textContent 应该是"string"；如果没有，那么这两个函数就会改为使用 innerText。可以像下面这样调用这两个函数。

```js
setInnerText(div, "Hello world!");
alert(getInnerText(div)); //"Hello world!"
```

使用这两个函数可以确保在不同的浏览器中使用正确的属性。

> 实际上， innerText 与 textContent 返回的内容并不完全一样。比如，innerText 会忽略行内的样式和脚本，而 textContent 则会像返回其他文本一样返回行内的样式和脚本代码。避免跨浏览器兼容问题的最佳途径，就是从不包含行内样式或行内脚本的 DOM 子树副本或 DOM 片段中读取文本。

**2. outerText 属性**

除了作用范围扩大到了包含调用它的节点之外， outerText 与 innerText 基本上没有多大区别。在读取文本值时， outerText 与 innerText 的结果完全一样。但在写模式下， outerText 就完全不同了： outerText 不只是替换调用它的元素的子节点，而是会替换整个元素（包括子节点）。比如：

```js
div.outerText = "Hello world!";
```

这行代码实际上相当于如下两行代码：

```js
var text = document.createTextNode("Hello world!");
div.parentNode.replaceChild(text, div);
```

本质上，新的文本节点会完全取代调用 outerText 的元素。此后，该元素就从文档中被删除，无法访问。

支持 outerText 属性的浏览器有 IE4+、 Safari 3+、 Opera 8+和 Chrome。由于这个属性会导致调用它的元素不存在，因此并不常用。我们也建议读者尽可能不要使用这个属性。

### 11.4.5 滚动

如前所述， HTML5 之前的规范并没有就与页面滚动相关的 API 做出任何规定。但 HTML5 在将`scrollIntoView()`纳入规范之后，仍然还有其他几个专有方法可以在不同的浏览器中使用。下面列出的几个方法都是对 HTMLElement 类型的扩展，因此在所有元素中都可以调用。

- `scrollIntoViewIfNeeded(alignCenter)`：只在当前元素在视口中不可见的情况下，才滚动浏览器窗口或容器元素，最终让它可见。如果当前元素在视口中可见，这个方法什么也不做。如果将可选的 alignCenter 参数设置为 true，则表示尽量将元素显示在视口中部（垂直方向）。Safari 和 Chrome 实现了这个方法。
- `scrollByLines(lineCount)`：将元素的内容滚动指定的行高， lineCount 值可以是正值，也可以是负值。 Safari 和 Chrome 实现了这个方法。
- `scrollByPages(pageCount)`：将元素的内容滚动指定的页面高度，具体高度由元素的高度决定。 Safari 和 Chrome 实现了这个方法。

希望大家要注意的是， `scrollIntoView()`和 `scrollIntoViewIfNeeded()`的作用对象是元素的容器，而 `scrollByLines()`和 `scrollByPages()`影响的则是元素自身。下面还是来看几个示例吧。

```js
//将页面主体滚动 5 行
document.body.scrollByLines(5);
//在当前元素不可见的时候，让它进入浏览器的视口
document.images[0].scrollIntoViewIfNeeded();
//将页面主体往回滚动 1 页
document.body.scrollByPages(-1);
```

由于 `scrollIntoView()`是唯一一个所有浏览器都支持的方法，因此还是这个方法最常用。

## 11.5 小结　

虽然 DOM 为与 XML 及 HTML 文档交互制定了一系列核心 API，但仍然有几个规范对标准的 DOM进行了扩展。这些扩展中有很多原来是浏览器专有的，但后来成为了事实标准，于是其他浏览器也都提供了相同的实现。本章介绍的三个这方面的规范如下。

- Selectors API，定义了两个方法，让开发人员能够基于 CSS 选择符从 DOM 中取得元素，这两个方法是`querySelector()`和`querySelectorAll()`。
- Element Traversal，为 DOM 元素定义了额外的属性，让开发人员能够更方便地从一个元素跳到另一个元素。之所以会出现这个扩展，是因为浏览器处理 DOM 元素间空白符的方式不一样。
- HTML5，为标准的 DOM 定义了很多扩展功能。其中包括在 innerHTML 属性这样的事实标准基础上提供的标准定义，以及为管理焦点、设置字符集、滚动页面而规定的扩展 API。

虽然目前 DOM 扩展的数量还不多，但随着 Web 技术的发展，相信一定还会涌现出更多扩展来。很多浏览器都在试验专有的扩展，而这些扩展一旦获得认可，就能成为“伪”标准，甚至会被收录到规范的更新版本中。

# 第12章 DOM2和DOM3　

DOM1 级主要定义的是 HTML 和 XML 文档的底层结构。 DOM2 和 DOM3 级则在这个结构的基础上引入了更多的交互能力，也支持了更高级的 XML 特性。为此， DOM2 和 DOM3 级分为许多模块（模块之间具有某种关联），分别描述了 DOM 的某个非常具体的子集。这些模块如下。

- DOM2 级核心（ DOM Level 2 Core）：在 1 级核心基础上构建，为节点添加了更多方法和属性。
- DOM2 级视图（ DOM Level 2 Views）：为文档定义了基于样式信息的不同视图。
- DOM2 级事件（ DOM Level 2 Events）：说明了如何使用事件与 DOM 文档交互。
- DOM2 级样式（ DOM Level 2 Style）：定义了如何以编程方式来访问和改变 CSS 样式信息。
- DOM2 级遍历和范围（ DOM Level 2 Traversal and Range）：引入了遍历 DOM 文档和选择其特定部分的新接口。
- DOM2 级 HTML（ DOM Level 2 HTML）：在 1 级 HTML 基础上构建，添加了更多属性、方法和
新接口。

本章探讨除“DOM2 级事件”之外的所有模块，“DOM2 级事件”模块将在第 13 章进行全面讲解。

> DOM3 级又增加了“XPath”模块和“加载与保存”（ Load and Save）模块。这些模块将在第 18 章讨论。

## 12.1 DOM变化 

DOM2 级和 3 级的目的在于扩展 DOM API，以满足操作 XML 的所有需求，同时提供更好的错误处理及特性检测能力。从某种意义上讲，实现这一目的很大程度意味着对命名空间的支持。“DOM2 级核心”没有引入新类型，它只是在 DOM1 级的基础上通过增加新方法和新属性来增强了既有类型。“DOM3级核心”同样增强了既有类型，但也引入了一些新类型。

类似地，“DOM2 级视图”和“DOM2 级 HTML”模块也增强了 DOM 接口，提供了新的属性和方法。由于这两个模块很小，因此我们将把它们与“DOM2 级核心”放在一起，讨论基本 JavaScript 对象的变化。可以通过下列代码来确定浏览器是否支持这些 DOM 模块。

```js
var supportsDOM2Core = document.implementation.hasFeature("Core", "2.0");
var supportsDOM3Core = document.implementation.hasFeature("Core", "3.0");
var supportsDOM2HTML = document.implementation.hasFeature("HTML", "2.0");
var supportsDOM2Views = document.implementation.hasFeature("Views", "2.0");
var supportsDOM2XML = document.implementation.hasFeature("XML", "2.0");
```

本章只讨论那些已经有浏览器实现的部分，任何浏览器都没有实现的部分将不作讨论。

### 12.1.1 针对XML命名空间的变化

有了 XML 命名空间，不同 XML 文档的元素就可以混合在一起，共同构成格式良好的文档，而不
必担心发生命名冲突。从技术上说， HTML 不支持 XML 命名空间，但 XHTML 支持 XML 命名空间。
因此，本节给出的都是 XHTML 的示例。

命名空间要使用 xmlns 特性来指定。 XHTML 的命名空间是 http://www.w3.org/1999/xhtml，在任何格式良好 XHTML 页面中，都应该将其包含在<html>元素中，如下面的例子所示。

```js
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>Example XHTML page</title>
  </head>
  <body>
    Hello world!
  </body>
</html>
```

对这个例子而言，其中的所有元素默认都被视为 XHTML 命名空间中的元素。要想明确地为 XML
命名空间创建前缀，可以使用 xmlns 后跟冒号，再后跟前缀，如下所示。

```js
<xhtml:html xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <xhtml:head>
  <xhtml:title>Example XHTML page</xhtml:title>
  </xhtml:head>
  <xhtml:body>
  Hello world!
  </xhtml:body>
</xhtml:html>
```

这里为 XHTML 的命名空间定义了一个名为 xhtml 的前缀，并要求所有 XHTML 元素都以该前缀
开头。有时候为了避免不同语言间的冲突，也需要使用命名空间来限定特性，如下面的例子所示。

```js
<xhtml:html xmlns:xhtml="http://www.w3.org/1999/xhtml">
  <xhtml:head>
    <xhtml:title>Example XHTML page</xhtml:title>
  </xhtml:head>
  <xhtml:body xhtml:class="home">
    Hello world!
  </xhtml:body>
</xhtml:html>
```

这个例子中的特性 class 带有一个 xhtml 前缀。在只基于一种语言编写 XML 文档的情况下，命
名空间实际上也没有什么用。不过，在混合使用两种语言的情况下，命名空间的用处就非常大了。来看
一看下面这个混合了 XHTML 和 SVG 语言的文档：

```js
<html xmlns="http://www.w3.org/1999/xhtml">
  <head>
    <title>Example XHTML page</title>
  </head>
  <body>
    <svg xmlns="http://www.w3.org/2000/svg" version="1.1"
      viewBox="0 0 100 100" style="width:100%; height:100%">
    <rect x="0" y="0" width="100" height="100" style="fill:red"/>
    </svg>
  </body>
</html>
```

在这个例子中，通过设置命名空间，将`<svg>`标识为了与包含文档无关的元素。此时， `<svg>`元素的所有子元素，以及这些元素的所有特性，都被认为属于 http://www.w3.org/2000/svg 命名空间。即使这个文档从技术上说是一个 XHTML 文档，但因为有了命名空间，其中的 SVG 代码也仍然是有效的。

对于类似这样的文档来说，最有意思的事发生在调用方法操作文档节点的情况下。例如，在创建一
个元素时，这个元素属于哪个命名空间呢？在查询一个特殊标签名时，应该将结果包含在哪个命名空间
中呢？“DOM2 级核心”通过为大多数 DOM1 级方法提供特定于命名空间的版本解决了这个问题。

......

### 12.1.2 其他方面的变化

DOM 的其他部分在“DOM2 级核心”中也发生了一些变化。这些变化与 XML 命名空间无关，而是
更倾向于确保 API 的可靠性及完整性。

**1. DocumentType 类型的变化**

DocumentType 类型新增了 3 个属性： publicId、 systemId 和 internalSubset。其中，前两个属性表示的是文档类型声明中的两个信息段，这两个信息段在 DOM1 级中是没有办法访问到的。以下面的 HTML 文档类型声明为例。

```js
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
"http://www.w3.org/TR/html4/strict.dtd">
```

对这个文档类型声明而言， publicId 是"-//W3C//DTD HTML 4.01//EN"，而 systemId 是"http://www.w3.org/TR/html4/strict.dtd"。在支持 DOM2 级的浏览器中，应该可以运行下列代码。

```js
alert(document.doctype.publicId);
alert(document.doctype.systemId);
```

实际上，很少需要在网页中访问此类信息。

最后一个属性 internalSubset，用于访问包含在文档类型声明中的额外定义，以下面的代码为例。

```js
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"
[<!ELEMENT name (#PCDATA)>] >
```

访问 `document.doctype.internalSubset` 将得到"<!ELEMENT name (#PCDATA)>"。这种内部子集（ internal subset）在 HTML 中极少用到，在 XML 中可能会更常见一些。

**2. Document 类型的变化**

Document 类型的变化中唯一与命名空间无关的方法是 `importNode()`。这个方法的用途是从一个文档中取得一个节点，然后将其导入到另一个文档，使其成为这个文档结构的一部分。需要注意的是，每个节点都有一个 ownerDocument 属性，表示所属的文档。如果调用 `appendChild()`时传入的节点属于不同的文档（ ownerDocument 属性的值不一样），则会导致错误。但在调用 `importNode()`时传入不同文档的节点则会返回一个新节点，这个新节点的所有权归当前文档所有。

说起来， `importNode()`方法与 Element 的 `cloneNode()`方法非常相似，它接受两个参数：要复制的节点和一个表示是否复制子节点的布尔值。返回的结果是原来节点的副本，但能够在当前文档中使用。来看下面的例子：

```js
var newNode = document.importNode(oldNode, true); //导入节点及其所有子节点
document.body.appendChild(newNode);
```

这个方法在 HTML 文档中并不常用，在 XML 文档中用得比较多（更多讨论请参见第 18 章）。

“DOM2 级视图”模块添加了一个名为 defaultView 的属性，其中保存着一个指针，指向拥有给定文档的窗口（或框架）。除此之外，“视图”规范没有提供什么时候其他视图可用的信息，因而这是唯一一个新增的属性。除 IE 之外的所有浏览器都支持 defaultView 属性。在 IE 中有一个等价的属性名叫 parentWindow（ Opera 也支持这个属性）。因此，要确定文档的归属窗口，可以使用以下代码。

```js
var parentWindow = document.defaultView || document.parentWindow;
```

除了上述一个方法和一个属性之外， “DOM2 级核心” 还为 `document.implementation` 对象规定了两个新方法： `createDocumentType()`和 `createDocument()`。 前者用于创建一个新的 DocumentType 节点，接受 3 个参数：文档类型名称、 publicId、 systemId。例如，下列代码会创建一个新的 HTML 4.01 Strict 文档类型。

```js
var doctype = document.implementation.createDocumentType("html",
"-//W3C//DTD HTML 4.01//EN",
"http://www.w3.org/TR/html4/strict.dtd");
```

由于既有文档的文档类型不能改变，因此 `createDocumentType()`只在创建新文档时有用；创建新文档时需要用到 `createDocument()`方法。这个方法接受 3 个参数：针对文档中元素的 namespaceURI、文档元素的标签名、新文档的文档类型。下面这行代码将会创建一个空的新 XML 文档。

```js
var doc = document.implementation.createDocument("", "root", null);
```

这行代码会创建一个没有命名空间的新文档，文档元素为`<root>`，而且没有指定文档类型。要想创建一个 XHTML 文档，可以使用以下代码。

```js
var doctype = document.implementation.createDocumentType("html",
" -//W3C//DTD XHTML 1.0 Strict//EN",
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd");
var doc = document.implementation.createDocument("http://www.w3.org/1999/xhtml",
"html", doctype);
```

这样，就创建了一个带有适当命名空间和文档类型的新 XHTML 文档。不过，新文档当前只有文档元素`<html>`，剩下的所有元素都需要继续添加。

“DOM2 级 HTML”模块也为 document.implementation 新增了一个方法，名叫 `createHTMLDocument()`。这个方法的用途是创建一个完整的 HTML 文档，包括`<html>`、 `<head>`、 `<title>`和`<body>`元素。这个方法只接受一个参数，即新创建文档的标题（放在`<title>`元素中的字符串），返回新的 HTML 文档，如下所示：

```js
var htmldoc = document.implementation.createHTMLDocument("New Doc");
alert(htmldoc.title); //"New Doc"
alert(typeof htmldoc.body); //"object"
```

通过调用 `createHTMLDocument()`创建的这个文档，是 HTMLDocument 类型的实例，因而具有该类型的所有属性和方法，包括 title 和 body 属性。只有 Opera 和 Safari 支持这个方法。

**3. Node 类型的变化**

Node 类型中唯一与命名空间无关的变化，就是添加了 `isSupported()`方法。与 DOM1 级为 document.implementation 引入的 `hasFeature()`方法类似， `isSupported()`方法用于确定当前节点具有什么能力。这个方法也接受相同的两个参数：特性名和特性版本号。如果浏览器实现了相应特性，而且能够基于给定节点执行该特性， `isSupported()`就返回 true。来看一个例子：

```js
if (document.body.isSupported("HTML", "2.0")){
  //执行只有"DOM2 级 HTML"才支持的操作
}
```

由于不同实现在决定对什么特性返回 true 或 false 时并不一致，这个方法同样也存在与 `hasFeature()`方法相同的问题。为此，我们建议在确定某个特性是否可用时，最好还是使用能力检测。

DOM3 级引入了两个辅助比较节点的方法： `isSameNode()`和 `isEqualNode()`。这两个方法都接受一个节点参数，并在传入节点与引用的节点相同或相等时返回 true。所谓相同，指的是两个节点引用的是同一个对象。所谓相等，指的是两个节点是相同的类型，具有相等的属性（ nodeName、 nodeValue，等等），而且它们的 attributes 和 childNodes 属性也相等（相同位置包含相同的值）。来看一个例子。

```js
var div1 = document.createElement("div");
div1.setAttribute("class", "box");
var div2 = document.createElement("div");
div2.setAttribute("class", "box");
alert(div1.isSameNode(div1)); //true
alert(div1.isEqualNode(div2)); //true
alert(div1.isSameNode(div2)); //false
```

这里创建了两个具有相同特性的`<div>`元素。这两个元素相等，但不相同。

DOM3 级还针对为 DOM 节点添加额外数据引入了新方法。其中， `setUserData()`方法会将数据指定给节点，它接受 3 个参数：要设置的键、实际的数据（可以是任何数据类型）和处理函数。以下代码可以将数据指定给一个节点。

```js
document.body.setUserData("name", "Nicholas", function(){});
```

然后，使用 `getUserData()`并传入相同的键，就可以取得该数据，如下所示：

```js
var value = document.body.getUserData("name");
```

传入 `setUserData()`中的处理函数会在带有数据的节点被复制、删除、重命名或引入一个文档时调用，因而你可以事先决定在上述操作发生时如何处理用户数据。处理函数接受 5 个参数：表示操作类型的数值（ 1 表示复制， 2 表示导入， 3 表示删除， 4 表示重命名）、数据键、数据值、源节点和目标节点。在删除节点时，源节点是 null；除在复制节点时，目标节点均为 null。在函数内部，你可以决定如何存储数据。来看下面的例子。

```js
var div = document.createElement("div");
div.setUserData("name", "Nicholas", function(operation, key, value, src, dest){
if (operation == 1){
dest.setUserData(key, value, function(){}); }
});
var newDiv = div.cloneNode(true);
alert(newDiv.getUserData("name")); //"Nicholas"
```

这里，先创建了一个`<div>`元素，然后又为它添加了一些数据（用户数据）。在使用 `cloneNode()`复制这个元素时，就会调用处理函数，从而将数据自动复制到了副本节点。结果在通过副本节点调用`getUserData()`时，就会返回与原始节点中包含的相同的值。

**4. 框架的变化**

框架和内嵌框架分别用 HTMLFrameElement 和 HTMLIFrameElement 表示， 它们在 DOM2 级中都有了一个新属性，名叫 contentDocument。这个属性包含一个指针，指向表示框架内容的文档对象。在此之前，无法直接通过元素取得这个文档对象（只能使用 frames 集合）。可以像下面这样使用这个属性。

```js
var iframe = document.getElementById("myIframe");
var iframeDoc = iframe.contentDocument; //在 IE8 以前的版本中无效
```

由于 contentDocument 属性是 Document 类型的实例，因此可以像使用其他 HTML 文档一样使用它，包括所有属性和方法。 Opera、 Firefox、 Safari 和 Chrome 支持这个属性。 IE8 之前不支持框架中的 contentDocument 属性，但支持一个名叫 contentWindow 的属性，该属性返回框架的 window 对象，而这个 window 对象又有一个 document 属性。因此，要想在上述所有浏览器中访问内嵌框架的文档对象，可以使用下列代码。

```js
var iframe = document.getElementById("myIframe");
var iframeDoc = iframe.contentDocument || iframe.contentWindow.document;
```

所有浏览器都支持 contentWindow 属性。

> 访问框架或内嵌框架的文档对象要受到跨域安全策略的限制。如果某个框架中的页面来自其他域或不同子域，或者使用了不同的协议，那么要访问这个框架的文档对象就会导致错误。

## 12.2 样式 

在 HTML 中定义样式的方式有 3 种：通过`<link/>`元素包含外部样式表文件、使用`<style/>`元素定义嵌入式样式，以及使用 style 特性定义针对特定元素的样式。“DOM2 级样式”模块围绕这 3 种应用样式的机制提供了一套 API。要确定浏览器是否支持 DOM2 级定义的 CSS 能力，可以使用下列代码。

```js
var supportsDOM2CSS = document.implementation.hasFeature("CSS", "2.0");
var supportsDOM2CSS2 = document.implementation.hasFeature("CSS2", "2.0");
```

### 12.2.1 访问元素的样式

任何支持 style 特性的 HTML 元素在 JavaScript 中都有一个对应的 style 属性。 这个 style 对象是 CSSStyleDeclaration 的实例，包含着通过 HTML 的 style 特性指定的所有样式信息，但不包含与外部样式表或嵌入样式表经层叠而来的样式。在 style 特性中指定的任何 CSS 属性都将表现为这个style 对象的相应属性。对于使用短划线（分隔不同的词汇，例如 background-image）的 CSS 属性名，必须将其转换成驼峰大小写形式，才能通过 JavaScript 来访问。下表列出了几个常见的 CSS 属性及其在 style 对象中对应的属性名。

| CSS属性 | JavaScript属性 |
|---|---|
| background-image | style.backgroundImage |
| color | style.color |
| display | style.display |
| font-family | style.fontFamily |

多数情况下，都可以通过简单地转换属性名的格式来实现转换。其中一个不能直接转换的 CSS 属性就是 float。由于 float 是 JavaScript 中的保留字，因此不能用作属性名。“DOM2 级样式”规范规定样式对象上相应的属性名应该是 cssFloat； Firefox、 Safari、 Opera 和 Chrome 都支持这个属性，而 IE 支持的则是 styleFloat。

只要取得一个有效的 DOM 元素的引用，就可以随时使用 JavaScript 为其设置样式。以下是几个例子。

```js
var myDiv = document.getElementById("myDiv");
//设置背景颜色
myDiv.style.backgroundColor = "red";
//改变大小
myDiv.style.width = "100px";
myDiv.style.height = "200px";
//指定边框
myDiv.style.border = "1px solid black";
```

在以这种方式改变样式时，元素的外观会自动被更新。

> 在标准模式下，所有度量值都必须指定一个度量单位。在混杂模式下，可以将style.width 设置为"20"，浏览器会假设它是"20px"；但在标准模式下，将style.width 设置为"20"会导致被忽略—— 因为没有度量单位。在实践中，最好始终都指定度量单位。

通过 style 对象同样可以取得在 style 特性中指定的样式。以下面的 HTML 代码为例。

```js
<div id="myDiv" style="background-color:blue; width:10px; height:25px"></div>
```

在 style 特性中指定的样式信息可以通过下列代码取得。

```js
alert(myDiv.style.backgroundColor); //"blue"
alert(myDiv.style.width); //"10px"
alert(myDiv.style.height); //"25px"
```

如果没有为元素设置 style 特性，那么 style 对象中可能会包含一些默认的值，但这些值并不能准确地反映该元素的样式信息。

**1. DOM 样式属性和方法**

“DOM2 级样式”规范还为 style 对象定义了一些属性和方法。这些属性和方法在提供元素的 style 特性值的同时，也可以修改样式。下面列出了这些属性和方法。

- cssText：如前所述，通过它能够访问到 style 特性中的 CSS 代码。
- length：应用给元素的 CSS 属性的数量。
- parentRule：表示 CSS 信息的 CSSRule 对象。本节后面将讨论 CSSRule 类型。
- `getPropertyCSSValue(propertyName)`：返回包含给定属性值的 CSSValue 对象。
- `getPropertyPriority(propertyName)`：如果给定的属性使用了!important 设置，则返回"important"；否则，返回空字符串。
- `getPropertyValue(propertyName)`：返回给定属性的字符串值。
- `item(index)`：返回给定位置的 CSS 属性的名称。
- `removeProperty(propertyName)`：从样式中删除给定属性。
- `setProperty(propertyName,value,priority)`：将给定属性设置为相应的值，并加上优先权标志（ "important"或者一个空字符串）。

通过 cssText 属性可以访问 style 特性中的 CSS 代码。在读取模式下， cssText 返回浏览器对 style 特性中 CSS 代码的内部表示。在写入模式下，赋给 cssText 的值会重写整个 style 特性的值；也就是说，以前通过 style 特性指定的样式信息都将丢失。例如，如果通过 style 特性为元素设置了边框，然后再以不包含边框的规则重写 cssText，那么就会抹去元素上的边框。下面是使用 cssText 属性的一个例子。

```js
myDiv.style.cssText = "width: 25px; height: 100px; background-color: green";
alert(myDiv.style.cssText);
```

设置 cssText 是为元素应用多项变化最快捷的方式，因为可以一次性地应用所有变化。

设计 length 属性的目的，就是将其与 `item()`方法配套使用，以便迭代在元素中定义的 CSS 属性。在使用 length 和 `item()`时， style 对象实际上就相当于一个集合，都可以使用方括号语法来代替`item()`来取得给定位置的 CSS 属性，如下面的例子所示。

```js
for (var i=0, len=myDiv.style.length; i < len; i++){
  alert(myDiv.style[i]); //或者 myDiv.style.item(i)
}
```

无论是使用方括号语法还是使用 `item()`方法，都可以取得 CSS 属性名（ "background-color"，不是"backgroundColor"）。然后，就可以在 ``getPropertyValue()``中使用取得的属性名进一步取得属性的值，如下所示。

```js
var prop, value, i, len;
for (i=0, len=myDiv.style.length; i < len; i++){
prop = myDiv.style[i]; //或者 myDiv.style.item(i)
value = myDiv.style.getPropertyValue(prop);
alert(prop + " : " + value);
}
```

`getPropertyValue()`方法取得的始终都是 CSS 属性值的字符串表示。如果你需要更多信息，可以使用 `getPropertyCSSValue()`方法，它返回一个包含两个属性的 CSSValue 对象，这两个属性分别是： cssText 和 cssValueType。其中， cssText 属性的值与 `getPropertyValue()`返回的值相同，而 cssValueType 属性则是一个数值常量，表示值的类型： 0 表示继承的值， 1 表示基本的值， 2 表示值列表， 3 表示自定义的值。以下代码既输出 CSS 属性值，也输出值的类型。

```js
var prop, value, i, len;
for (i=0, len=myDiv.style.length; i < len; i++){
  prop = myDiv.style[i]; //或者 myDiv.style.item(i)
  value = myDiv.style.getPropertyCSSValue(prop);
  alert(prop + " : " + value.cssText + " (" + value.cssValueType + ")");
}
```

在实际开发中， `getPropertyCSSValue()`使用得比 `getPropertyValue()`少得多。 IE9+、 Safarie3+以及 Chrome 支持这个方法。 Firefox 7 及之前版本也提供这个访问，但调用总返回 null。要从元素的样式中移除某个 CSS 属性，需要使用` removeProperty()`方法。使用这个方法移除一个属性，意味着将会为该属性应用默认的样式（从其他样式表经层叠而来）。例如，要移除通过 style 特性设置的 border 属性，可以使用下面的代码。

```js
myDiv.style.removeProperty("border");
```

在不确定某个给定的 CSS 属性拥有什么默认值的情况下，就可以使用这个方法。只要移除相应的属性，就可以为元素应用默认值。

> 除非另有说明，本节讨论的属性和方法都得到了 IE9+、 Firefox、 Safari、 Opera 9+ 以及 Chrome 的支持。

**2. 计算的样式**

虽然 style 对象能够提供支持 style 特性的任何元素的样式信息，但它不包含那些从其他样式表层叠而来并影响到当前元素的样式信息。 “DOM2 级样式”增强了 document.defaultView，提供了`getComputedStyle()`方法。这个方法接受两个参数：要取得计算样式的元素和一个伪元素字符串（例如":after"）。如果不需要伪元素信息，第二个参数可以是 null。 `getComputedStyle()`方法返回一个 CSSStyleDeclaration 对象（与 style 属性的类型相同），其中包含当前元素的所有计算的样式。以下面这个 HTML 页面为例。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Computed Styles Example</title>
  <style type="text/css">
    #myDiv {
      background-color: blue;
      width: 100px;
      height: 200px;
    }
  </style>
</head>
<body>
  <div id="myDiv" style="background-color: red; border: 1px solid black"></div>
</body>
</html>
```

应用给这个例子中`<div>`元素的样式一方面来自嵌入式样式表（ `<style>`元素中的样式），另一方面来自其 style 特性。但是， style 特性中设置了 backgroundColor 和 border，没有设置 width 和 height，后者是通过样式表规则应用的。以下代码可以取得这个元素计算后的样式。

```js
var myDiv = document.getElementById("myDiv");
var computedStyle = document.defaultView.getComputedStyle(myDiv, null);
alert(computedStyle.backgroundColor); // "red"
alert(computedStyle.width); // "100px"
alert(computedStyle.height); // "200px"
alert(computedStyle.border); // 在某些浏览器中是"1px solid black"
```

在这个元素计算后的样式中，背景颜色的值是"red"，宽度值是"100px"，高度值是"200px"。我们注意到，背景颜色不是"blue"，因为这个样式在自身的 style 特性中已经被覆盖了。边框属性可能会也可能不会返回样式表中实际的 border 规则（ Opera 会返回，但其他浏览器不会）。存在这个差别的原因是不同浏览器解释综合（ rollup）属性（如 border）的方式不同，因为设置这种属性实际上会涉及很多其他属性。在设置 border 时，实际上是设置了四个边的边框宽度、颜色、样式属性（ border-left-width 、 border-top-color 、 border-bottom-style ，等等）。因此，即使 computedStyle.border 不会在所有浏览器中都返回值，但 `computedStyle.borderLeftWidth` 会返回值。

>　需要注意的是，即使有些浏览器支持这种功能，但表示值的方式可能会有所区别。例如， Firefox 和 Safari 会将所有颜色转换成 RGB 格式（例如红色是 `rgb(255,0,0)`）。因此，在使用 `getComputedStyle()`方法时，最好多在几种浏览器中测试一下。

IE 不支持 `getComputedStyle()`方法，但它有一种类似的概念。在 IE 中，每个具有 style 属性的元素还有一个 currentStyle 属性。这个属性是 CSSStyleDeclaration 的实例，包含当前元素全部计算后的样式。取得这些样式的方式也差不多，如下面的例子所示。

```js
var myDiv = document.getElementById("myDiv");
var computedStyle = myDiv.currentStyle;
alert(computedStyle.backgroundColor); //"red"
alert(computedStyle.width); //"100px"
alert(computedStyle.height); //"200px"
alert(computedStyle.border); //undefined
```

与 DOM 版本的方式一样， IE 也没有返回 border 样式，因为这是一个综合属性。

无论在哪个浏览器中，最重要的一条是要记住所有计算的样式都是只读的；不能修改计算后样式对象中的 CSS 属性。此外，计算后的样式也包含属于浏览器内部样式表的样式信息，因此任何具有默认值的 CSS 属性都会表现在计算后的样式中。例如，所有浏览器中的 visibility 属性都有一个默认值，但这个值会因实现而异。在默认情况下，有的浏览器将 visibility 属性设置为"visible"，而有的浏览器则将其设置为"inherit"。换句话说，不能指望某个 CSS 属性的默认值在不同浏览器中是相同的。如果你需要元素具有某个特定的默认值，应该手工在样式表中指定该值。

### 12.2.2 操作样式表

CSSStyleSheet 类型表示的是样式表，包括通过`<link>`元素包含的样式表和在`<style>`元素中定义的样式表。有读者可能记得，这两个元素本身分别是由 HTMLLinkElement 和 HTMLStyleElement 类型表示的。但是， CSSStyleSheet 类型相对更加通用一些，它只表示样式表，而不管这些样式表在 HTML 中是如何定义的。此外，上述两个针对元素的类型允许修改 HTML 特性，但 CSSStyleSheet 对象则是一套只读的接口（有一个属性例外）。使用下面的代码可以确定浏览器是否支持 DOM2 级样式表。

```js
var supportsDOM2StyleSheets =
document.implementation.hasFeature("StyleSheets", "2.0");
```

CSSStyleSheet 继承自 StyleSheet，后者可以作为一个基础接口来定义非 CSS 样式表。从StyleSheet 接口继承而来的属性如下。

- disabled：表示样式表是否被禁用的布尔值。这个属性是可读/写的，将这个值设置为 true 可以禁用样式表。
- href：如果样式表是通过`<link>`包含的，则是样式表的 URL；否则，是 null。
- media：当前样式表支持的所有媒体类型的集合。与所有 DOM 集合一样，这个集合也有一个length 属性和一个 `item()`方法。也可以使用方括号语法取得集合中特定的项。如果集合是空列表，表示样式表适用于所有媒体。在 IE 中， media 是一个反映`<link>`和`<style>`元素 media特性值的字符串。
- ownerNode：指向拥有当前样式表的节点的指针，样式表可能是在 HTML 中通过`<link>`或`<style/>`引入的（在 XML 中可能是通过处理指令引入的）。如果当前样式表是其他样式表通过@import 导入的，则这个属性值为 null。 IE 不支持这个属性。
- parentStyleSheet：在当前样式表是通过@import 导入的情况下，这个属性是一个指向导入它的样式表的指针。
- title： ownerNode 中 title 属性的值。
- type：表示样式表类型的字符串。对 CSS 样式表而言，这个字符串是"type/css"。除 了 disabled 属 性 之 外， 其 他 属 性都 是 只 读 的 。 在 支 持 以上 所 有 这 些属 性 的 基 础上 ，CSSStyleSheet 类型还支持下列属性和方法：
- cssRules：样式表中包含的样式规则的集合。 IE 不支持这个属性，但有一个类似的 rules 属性。
- ownerRule：如果样式表是通过@import 导入的，这个属性就是一个指针，指向表示导入的规则；否则，值为 null。 IE 不支持这个属性。
- `deleteRule(index)`：删除 cssRules 集合中指定位置的规则。 IE 不支持这个方法，但支持一个类似的 `removeRule()`方法。
- `insertRule(rule,index)`：向 cssRules 集合中指定的位置插入 rule 字符串。 IE 不支持这个方法，但支持一个类似的 `addRule()`方法。

应用于文档的所有样式表是通过 `document.styleSheets` 集合来表示的。通过这个集合的 length 属性可以获知文档中样式表的数量，而通过方括号语法或 `item()`方法可以访问每一个样式表。来看一个例子。

```js
var sheet = null;
for (var i=0, len=document.styleSheets.length; i < len; i++){
  sheet = document.styleSheets[i];
  alert(sheet.href);
}
```

以上代码可以输出文档中使用的每一个样式表的 href 属性（ `<style>`元素包含的样式表没有href 属性）。

不同浏览器的 document.styleSheets 返回的样式表也不同。所有浏览器都会包含`<style>`元素和 rel 特性被设置为"stylesheet"的`<link>`元素引入的样式表。 IE 和 Opera 也包含 rel 特性被设置为"alternate stylesheet"的`<link>`元素引入的样式表。

也可以直接通过`<link>`或`<style>`元素取得 CSSStyleSheet 对象。 DOM 规定了一个包含 CSSStyleSheet 对象的属性，名叫 sheet；除了 IE，其他浏览器都支持这个属性。 IE 支持的是 styleSheet 属性。要想在不同浏览器中都能取得样式表对象，可以使用下列代码。

```js
function getStyleSheet(element){
return element.sheet || element.styleSheet;
}
//取得第一个<link/>元素引入的样式表
var link = document.getElementsByTagName("link")[0];
var sheet = getStylesheet(link);
StyleSheetsExample2.htm
```

这里的 `getStyleSheet()`返回的样式表对象与 document.styleSheets 集合中的样式表对象相同。

**1. CSS 规则**

CSSRule 对象表示样式表中的每一条规则。实际上， CSSRule 是一个供其他多种类型继承的基类型，其中最常见的就是 CSSStyleRule 类型，表示样式信息（其他规则还有@import、 @font-face、@page 和@charset，但这些规则很少有必要通过脚本来访问）。 CSSStyleRule 对象包含下列属性。

- cssText：返回整条规则对应的文本。由于浏览器对样式表的内部处理方式不同，返回的文本可能会与样式表中实际的文本不一样； Safari 始终都会将文本转换成全部小写。 IE 不支持这个属性。
- parentRule：如果当前规则是导入的规则，这个属性引用的就是导入规则；否则，这个值为null。 IE 不支持这个属性。
- parentStyleSheet：当前规则所属的样式表。 IE 不支持这个属性。
- selectorText：返回当前规则的选择符文本。由于浏览器对样式表的内部处理方式不同，返回的文本可能会与样式表中实际的文本不一样（例如， Safari 3 之前的版本始终会将文本转换成全部小写）。在 Firefox、 Safari、 Chrome 和 IE 中这个属性是只读的。 Opera 允许修改 selectorText。
- style：一个 CSSStyleDeclaration 对象，可以通过它设置和取得规则中特定的样式值。
- type：表示规则类型的常量值。对于样式规则，这个值是 1。 IE 不支持这个属性。

其中三个最常用的属性是 cssText、 selectorText 和 style。 cssText 属性与 style.cssText属性类似，但并不相同。前者包含选择符文本和围绕样式信息的花括号，后者只包含样式信息（类似于元素的 style.cssText）。此外， cssText 是只读的，而 style.cssText 也可以被重写。大多数情况下，仅使用 style 属性就可以满足所有操作样式规则的需求了。这个对象就像每个元素上的 style 属性一样，可以通过它读取和修改规则中的样式信息。以下面的 CSS 规则为例。

```css
div.box {
  background-color: blue;
  width: 100px;
  height: 200px;
}
```

假设这条规则位于页面中的第一个样式表中，而且这个样式表中只有这一条样式规则，那么通过下列代码可以取得这条规则的各种信息。

```js
var sheet = document.styleSheets[0];
var rules = sheet.cssRules || sheet.rules; //取得规则列表
var rule = rules[0]; //取得第一条规则
alert(rule.selectorText); //"div.box"
alert(rule.style.cssText); //完整的 CSS 代码
alert(rule.style.backgroundColor); //"blue"
alert(rule.style.width); //"100px"
alert(rule.style.height); //"200px"
```

使用这种方式，可以像确定元素的行内样式信息一样，确定与规则相关的样式信息。与使用元素的方式一样，在这种方式下也可以修改样式信息，如下面的例子所示。

```js
var sheet = document.styleSheets[0];
var rules = sheet.cssRules || sheet.rules; //取得规则列表
var rule = rules[0]; //取得第一条规则
rule.style.backgroundColor = "red"
```

必须要注意的是，以这种方式修改规则会影响页面中适用于该规则的所有元素。换句话说，如果有两个带有 box 类的`<div>`元素，那么这两个元素都会应用修改后的样式。

**2. 创建规则**

DOM 规定，要向现有样式表中添加新规则，需要使用 `insertRule()`方法。这个方法接受两个参数：规则文本和表示在哪里插入规则的索引。下面是一个例子。

```js
sheet.insertRule("body { background-color: silver }", 0); //DOM 方法
```

这个例子插入的规则会改变元素的背景颜色。插入的规则将成为样式表中的第一条规则（插入到了位置 0）——规则的次序在确定层叠之后应用到文档的规则时至关重要。 Firefox、 Safari、 Opera 和 Chrome 都支持 `insertRule()`方法。

IE8 及更早版本支持一个类似的方法，名叫 `addRule()`，也接收两必选参数：选择符文本和 CSS 样式信息；一个可选参数：插入规则的位置。在 IE 中插入与前面例子相同的规则，可使用如下代码。

```js
sheet.addRule("body", "background-color: silver", 0); //仅对 IE 有效
```

有关这个方法的规定中说，最多可以使用 `addRule()`添加 4 095 条样式规则。超出这个上限的调用将会导致错误。

要以跨浏览器的方式向样式表中插入规则，可以使用下面的函数。这个函数接受 4 个参数：要向其中添加规则的样式表以及与 `addRule()`相同的 3 个参数，如下所示。

```js
function insertRule(sheet, selectorText, cssText, position){
  if (sheet.insertRule){
    sheet.insertRule(selectorText + "{" + cssText + "}", position);
  } else if (sheet.addRule){
    sheet.addRule(selectorText, cssText, position);
  }
}
```

下面是调用这个函数的示例代码。

```js
insertRule(document.styleSheets[0], "body", "background-color: silver", 0);
```

虽然可以像这样来添加规则，但随着要添加规则的增多，这种方法就会变得非常繁琐。因此，如果要添加的规则非常多，我们建议还是采用第 10 章介绍过的动态加载样式表的技术。

**3. 删除规则**

从样式表中删除规则的方法是 `deleteRule()`，这个方法接受一个参数：要删除的规则的位置。例如，要删除样式表中的第一条规则，可以使用以下代码。

```js
sheet.deleteRule(0); //DOM 方法
```

IE 支持的类似方法叫 removeRule()，使用方法相同，如下所示：

```js
sheet.removeRule(0); //仅对 IE 有效
```

下面是一个能够跨浏览器删除规则的函数。第一个参数是要操作的样式表，第二个参数是要删除的规则的索引。

```js
function deleteRule(sheet, index){
if (sheet.deleteRule){
sheet.deleteRule(index);
} else if (sheet.removeRule){
sheet.removeRule(index);
}
}
```

调用这个函数的方式如下。

```js
deleteRule(document.styleSheets[0], 0);
```

与添加规则相似，删除规则也不是实际 Web 开发中常见的做法。考虑到删除规则可能会影响 CSS 层叠的效果，因此请大家慎重使用。

### 12.2.3 元素大小

本节介绍的属性和方法并不属于“DOM2 级样式”规范，但却与 HTML 元素的样式息息相关。 DOM 中没有规定如何确定页面中元素的大小。 IE 为此率先引入了一些属性，以便开发人员使用。目前，所有主要的浏览器都已经支持这些属性。

**1. 偏移量**

首先要介绍的属性涉及偏移量（ offset dimension ），包括元素在屏幕上占用的所有可见的空间。元素的可见大小由其高度、宽度决定，包括所有内边距、滚动条和边框大小（注意，不包括外边距）。通过下列 4 个属性可以取得元素的偏移量。

- offsetHeight：元素在垂直方向上占用的空间大小，以像素计。包括元素的高度、（可见的）水平滚动条的高度、上边框高度和下边框高度。
- offsetWidth：元素在水平方向上占用的空间大小，以像素计。包括元素的宽度、（可见的）垂直滚动条的宽度、左边框宽度和右边框宽度。
- offsetLeft：元素的左外边框至包含元素的左内边框之间的像素距离。
- offsetTop：元素的上外边框至包含元素的上内边框之间的像素距离。

其中， offsetLeft 和 offsetTop 属性与包含元素有关，包含元素的引用保存在 offsetParent 属性中。 offsetParent 属性不一定与 parentNode 的值相等。例如， `<td>`元素的 offsetParent 是作为其祖先元素的`<table>`元素，因为`<table>`是在 DOM 层次中距`<td>`最近的一个具有大小的元素。图 12-1 形象地展示了上面几个属性表示的不同大小。

要想知道某个元素在页面上的偏移量，将这个元素的 offsetLeft 和 offsetTop 与其 offsetParent 的相同属性相加，如此循环直至根元素，就可以得到一个基本准确的值。以下两个函数就可以用于分别取得元素的左和上偏移量。

```js
function getElementLeft(element){
  var actualLeft = element.offsetLeft;
  var current = element.offsetParent;
  while (current !== null){
    actualLeft += current.offsetLeft;
    current = current.offsetParent;
  }
  return actualLeft;
}

function getElementTop(element){
  var actualTop = element.offsetTop;
  var current = element.offsetParent;
  while (current !== null){
    actualTop += current. offsetTop;
    current = current.offsetParent;
  }
  return actualTop;
}
```

这两个函数利用 offsetParent 属性在 DOM 层次中逐级向上回溯，将每个层次中的偏移量属性合计到一块。对于简单的 CSS 布局的页面，这两函数可以得到非常精确的结果。对于使用表格和内嵌框架布局的页面，由于不同浏览器实现这些元素的方式不同，因此得到的值就不太精确了。一般来说，页面中的所有元素都会被包含在几个`<div>`元素中，而这些`<div>`元素的 offsetParent 又是`<body>`元素，所以 `getElementLeft()`与 `getElementTop()`会返回与 offsetLeft 和 offsetTop相同的值。

> 所有这些偏移量属性都是只读的，而且每次访问它们都需要重新计算。因此，应该尽量避免重复访问这些属性；如果需要重复使用其中某些属性的值，可以将它们保存在局部变量中，以提高性能。

**2. 客户区大小**

元素的客户区大小（ client dimension），指的是元素内容及其内边距所占据的空间大小。有关客户区大小的属性有两个： clientWidth 和 clientHeight。其中， clientWidth 属性是元素内容区宽度加上左右内边距宽度； clientHeight 属性是元素内容区高度加上上下内边距高度。图 12-2 形象地说明了这些属性表示的大小。

从字面上看，客户区大小就是元素内部的空间大小，因此滚动条占用的空间不计算在内。最常用到这些属性的情况，就是像第 8 章讨论的确定浏览器视口大小的时候。如下面的例子所示，要确定浏览器视口大小，可以使用 `document.documentElement` 或 `document.body`（在 IE7 之前的版本中）的 clientWidth 和 clientHeight。

```js
function getViewport(){
  if (document.compatMode == "BackCompat"){
    return {
      width: document.body.clientWidth,
      height: document.body.clientHeight
    };
  } else {
    return {
      width: document.documentElement.clientWidth,
      height: document.documentElement.clientHeight
    };
  }
}
```

这个函数首先检查 `document.compatMode` 属性，以确定浏览器是否运行在混杂模式。 Safari 3.1 之前的版本不支持这个属性，因此就会自动执行 else 语句。 Chrome、 Opera 和 Firefox 大多数情况下都运行在标准模式下，因此它们也会前进到 else 语句。这个函数会返回一个对象，包含两个属性： width 和 height；表示浏览器视口（ `<html>`或`<body>`元素）的大小。

> 与偏移量相似，客户区大小也是只读的，也是每次访问都要重新计算的。

**3. 滚动大小**

最后要介绍的是滚动大小（ scroll dimension），指的是包含滚动内容的元素的大小。有些元素（例如`<html>`元素），即使没有执行任何代码也能自动地添加滚动条；但另外一些元素，则需要通过 CSS 的 overflow 属性进行设置才能滚动。以下是 4 个与滚动大小相关的属性。

- scrollHeight：在没有滚动条的情况下，元素内容的总高度。
- scrollWidth：在没有滚动条的情况下，元素内容的总宽度。
- scrollLeft：被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置。
- scrollTop：被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置。

图 12-3 展示了这些属性代表的大小。

scrollWidth 和 scrollHeight 主要用于确定元素内容的实际大小。例如，通常认为`<html>`元素是在 Web 浏览器的视口中滚动的元素（ IE6 之前版本运行在混杂模式下时是`<body>`元素）。因此，带有垂直滚动条的页面总高度就是`document.documentElement.scrollHeight`。

对于不包含滚动条的页面而言 ， scrollWidth 和 scrollHeight 与 clientWidth 和 clientHeight 之间的关系并不十分清晰。在这种情况下，基于 `document.documentElement` 查看这些属性会在不同浏览器间发现一些不一致性问题，如下所述。

- Firefox 中这两组属性始终都是相等的，但大小代表的是文档内容区域的实际尺寸，而非视口的尺寸。
- Opera、 Safari 3.1 及更高版本、 Chrome 中的这两组属性是有差别的，其中 scrollWidth 和 scrollHeight 等于视口大小，而 clientWidth 和 clientHeight 等于文档内容区域的大小。
- IE（在标准模式）中的这两组属性不相等，其中 scrollWidth 和 scrollHeight 等于文档内容区域的大小，而 clientWidth 和 clientHeight 等于视口大小。

在确定文档的总高度时（包括基于视口的最小高度时），必须取得 scrollWidth/clientWidth 和scrollHeight/clientHeight 中的最大值，才能保证在跨浏览器的环境下得到精确的结果。下面就是这样一个例子。

```js
var docHeight = Math.max(document.documentElement.scrollHeight, document.documentElement.clientHeight);
var docWidth = Math.max(document.documentElement.scrollWidth, document.documentElement.clientWidth);
```

注意，对于运行在混杂模式下的 IE，则需要用 `document.body` 代替 `document.documentElement`。通过 scrollLeft 和 scrollTop 属性既可以确定元素当前滚动的状态，也可以设置元素的滚动位置。在元素尚未被滚动时，这两个属性的值都等于 0。如果元素被垂直滚动了，那么 scrollTop 的值会大于 0，且表示元素上方不可见内容的像素高度。如果元素被水平滚动了，那么 scrollLeft 的值会大于 0，且表示元素左侧不可见内容的像素宽度。这两个属性都是可以设置的，因此将元素的 scrollLeft 和 scrollTop 设置为 0，就可以重置元素的滚动位置。下面这个函数会检测元素是否位于顶部，如果不是就将其回滚到顶部。

```js
function scrollToTop(element){
  if (element.scrollTop != 0){
    element.scrollTop = 0;
  }
}
```

这个函数既取得了 scrollTop 的值，也设置了它的值。

**4. 确定元素大小**

IE、 Firefox 3+、 Safari 4+、 Opera 9.5 及 Chrome 为每个元素都提供了一个`getBoundingClientRect()`方法。这个方法返回会一个矩形对象，包含 4 个属性： left、 top、 right 和 bottom。这些属性给出了元素在页面中相对于视口的位置。但是，浏览器的实现稍有不同。 IE8 及更早版本认为文档的左上角坐标是`(2, 2)`，而其他浏览器包括 IE9 则将传统的`(0, 0)`作为起点坐标。因此，就需要在一开始检查一下位于`(0, 0)`处的元素的位置，在 IE8 及更早版本中，会返回`(2, 2)`，而在其他浏览器中会返回`(0, 0)`。来看下面的函数：

```js
function getBoundingClientRect(element){
  if (typeof arguments.callee.offset != "number"){
    var scrollTop = document.documentElement.scrollTop;
    var temp = document.createElement("div");
      temp.style.cssText = "position: absolute; left: 0; top: 0;";
      document.body.appendChild(temp);
      arguments.callee.offset = -temp.getBoundingClientRect().top - scrollTop;
      document.body.removeChild(temp);
      temp = null;
  }
  var rect = element.getBoundingClientRect();
  var offset = arguments.callee.offset;
  return {
    left: rect.left + offset,
    right: rect.right + offset,
    top: rect.top + offset,
    bottom: rect.bottom + offset
  };
}
```

这个函数使用了它自身的属性来确定是否要对坐标进行调整。第一步是检测属性是否有定义，如果没有就定义一个。最终的 offset 会被设置为新元素上坐标的负值，实际上就是在 IE 中设置为-2，在Firefox 和 Opera 中设置为-0。为此，需要创建一个临时的元素，将其位置设置在`(0,0)`，然后再调用其`getBoundingClientRect()`。而之所以要减去视口的 scrollTop，是为了防止调用这个函数时窗口被滚动了。这样编写代码，就无需每次调用这个函数都执行两次 `getBoundingClientRect()`了。接下来，再在传入的元素上调用这个方法并基于新的计算公式创建一个对象。

对于不支持 `getBoundingClientRect()`的浏览器，可以通过其他手段取得相同的信息。一般来说， right 和 left 的差值与 offsetWidth 的值相等，而 bottom 和 top 的差值与 offsetHeight 相等。而且， left 和 top 属性大致等于使用本章前面定义的 `getElementLeft()`和 `getElementTop()` 函数取得的值。综合上述，就可以创建出下面这个跨浏览器的函数：

```js
function getBoundingClientRect(element){
  var scrollTop = document.documentElement.scrollTop;
  var scrollLeft = document.documentElement.scrollLeft;
    if (element.getBoundingClientRect){
      if (typeof arguments.callee.offset != "number"){
        var temp = document.createElement("div");
        temp.style.cssText = "position:absolute;left:0;top:0;";
        document.body.appendChild(temp);
        arguments.callee.offset = -temp.getBoundingClientRect().top - scrollTop;
        document.body.removeChild(temp);
        temp = null;
      }
      var rect = element.getBoundingClientRect();
      var offset = arguments.callee.offset;
      return {
        left: rect.left + offset,
        right: rect.right + offset,
        top: rect.top + offset,
        bottom: rect.bottom + offset
      };
    } else {
      var actualLeft = getElementLeft(element);
      var actualTop = getElementTop(element);
      return {  
        left: actualLeft - scrollLeft,
        right: actualLeft + element.offsetWidth - scrollLeft,
        top: actualTop - scrollTop,
        bottom: actualTop + element.offsetHeight - scrollTop
      }
    }
}
```

这个函数在`getBoundingClientRect()`有效时，就使用这个原生方法，而在这个方法无效时则使用默认的计算公式。在某些情况下，这个函数返回的值可能会有所不同，例如使用表格布局或使用滚动元素的情况下。

> 由于这里使用了 arguments.callee，所以这个方法不能在严格模式下使用。

## 12.3 遍历 

“DOM2 级遍历和范围”模块定义了两个用于辅助完成顺序遍历 DOM 结构的类型： NodeIterator 和 TreeWalker。这两个类型能够基于给定的起点对 DOM 结构执行深度优先（depth-first）的遍历操作。在与 DOM 兼容的浏览器中（Firefox 1 及更高版本、 Safari 1.3 及更高版本、 Opera 7.6 及更高版本、 Chrome0.2 及更高版本），都可以访问到这些类型的对象。 IE 不支持 DOM 遍历。使用下列代码可以检测浏览器对 DOM2 级遍历能力的支持情况。

```js
var supportsTraversals = document.implementation.hasFeature("Traversal", "2.0");
var supportsNodeIterator = (typeof document.createNodeIterator == "function");
var supportsTreeWalker = (typeof document.createTreeWalker == "function");
```

如前所述， DOM 遍历是深度优先的 DOM 结构遍历，也就是说，移动的方向至少有两个（取决于使用的遍历类型）。遍历以给定节点为根，不可能向上超出 DOM 树的根节点。以下面的 HTML 页面为例。

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Example</title>
  </head>
  <body>
    <p><b>Hello</b> world!</p>
  </body>
</html>
```

任何节点都可以作为遍历的根节点。如果假设`<body>`元素为根节点，那么遍历的第一步就是访问`<p>`元素，然后再访问同为`<body>`元素后代的两个文本节点。不过，这次遍历永远不会到达`<html>`、 `<head>`元素，也不会到达不属于`<body>`元素子树的任何节点。而以 document 为根节点的遍历则可以访问到文档中的全部节点。图 12-5 展示了对以 document 为根节点的 DOM 树进行深度优先遍历的先后顺序。

从 document 开始依序向前，访问的第一个节点是 document，访问的最后一个节点是包含"world!"的文本节点。从文档最后的文本节点开始，遍历可以反向移动到 DOM 树的顶端。此时，访问的第一个节点是包含"Hello"的文本节点，访问的最后一个节点是 document 节点。 NodeIterator 和 TreeWalker 都以这种方式执行遍历。

### 12.3.1 NodeIterator

NodeIterator 类型是两者中比较简单的一个，可以使用 `document.createNodeIterator()`方法创建它的新实例。这个方法接受下列 4 个参数。

- root：想要作为搜索起点的树中的节点。
- whatToShow：表示要访问哪些节点的数字代码。
- filter：是一个 NodeFilter 对象，或者一个表示应该接受还是拒绝某种特定节点的函数。
- entityReferenceExpansion：布尔值，表示是否要扩展实体引用。这个参数在 HTML 页面中没有用，因为其中的实体引用不能扩展。

whatToShow 参数是一个位掩码，通过应用一或多个过滤器（ filter）来确定要访问哪些节点。这个参数的值以常量形式在 NodeFilter 类型中定义，如下所示。

- NodeFilter.SHOW_ALL：显示所有类型的节点。
- NodeFilter.SHOW_ELEMENT：显示元素节点。
- NodeFilter.SHOW_ATTRIBUTE：显示特性节点。由于 DOM 结构原因，实际上不能使用这个值。
- NodeFilter.SHOW_TEXT：显示文本节点。
- NodeFilter.SHOW_CDATA_SECTION：显示 CDATA 节点。对 HTML 页面没有用。
- NodeFilter.SHOW_ENTITY_REFERENCE：显示实体引用节点。对 HTML 页面没有用。
- NodeFilter.SHOW_ENTITYE：显示实体节点。对 HTML 页面没有用。
- NodeFilter.SHOW_PROCESSING_INSTRUCTION：显示处理指令节点。对 HTML 页面没有用。
- NodeFilter.SHOW_COMMENT：显示注释节点。
- NodeFilter.SHOW_DOCUMENT：显示文档节点。
- NodeFilter.SHOW_DOCUMENT_TYPE：显示文档类型节点。
- NodeFilter.SHOW_DOCUMENT_FRAGMENT：显示文档片段节点。对 HTML 页面没有用。
- NodeFilter.SHOW_NOTATION：显示符号节点。对 HTML 页面没有用。

除了 NodeFilter.SHOW_ALL 之外，可以使用按位或操作符来组合多个选项，如下面的例子所示：

```js
var whatToShow = NodeFilter.SHOW_ELEMENT | NodeFilter.SHOW_TEXT;
```

可以通过 `createNodeIterator()`方法的 filter 参数来指定自定义的 NodeFilter 对象，或者指定一个功能类似节点过滤器（ node filter）的函数。每个 NodeFilter 对象只有一个方法，即 `acceptNode()`；如果应该访问给定的节点，该方法返回 NodeFilter.FILTER_ACCEPT，如果不应该访问给定的节点，该方法返回 NodeFilter.FILTER_SKIP。由于 NodeFilter 是一个抽象的类型，因此不能直接创建它的实例。在必要时，只要创建一个包含 `acceptNode()`方法的对象，然后将这个对象传入`createNodeIterator()`中即可。例如，下列代码展示了如何创建一个只显示`<p>`元素的节点迭代器。

```js
var filter = {
  acceptNode: function(node){
    return node.tagName.toLowerCase() == "p" ?
    NodeFilter.FILTER_ACCEPT :
    NodeFilter.FILTER_SKIP;
  }
};
var iterator = document.createNodeIterator(root, NodeFilter.SHOW_ELEMENT,
filter, false);
```

第三个参数也可以是一个与 `acceptNode()`方法类似的函数，如下所示。

```js
var filter = function(node){
  return node.tagName.toLowerCase() == "p" ?
  NodeFilter.FILTER_ACCEPT :
  NodeFilter.FILTER_SKIP;
};
var iterator = document.createNodeIterator(root, NodeFilter.SHOW_ELEMENT,
filter, false);
```

一般来说，这就是在 JavaScript 中使用这个方法的形式，这种形式比较简单，而且也跟其他的 JavaScript 代码很相似。如果不指定过滤器，那么应该在第三个参数的位置上传入 null。下面的代码创建了一个能够访问所有类型节点的简单的 NodeIterator。

```js
var iterator = document.createNodeIterator(document, NodeFilter.SHOW_ALL,
null, false);
```

NodeIterator 类型的两个主要方法是 `nextNode()`和 `previousNode()`。顾名思义，在深度优先的 DOM 子树遍历中， `nextNode()`方法用于向前前进一步，而 `previousNode()`用于向后后退一步。在刚刚创建的 NodeIterator 对象中，有一个内部指针指向根节点，因此第一次调用 `nextNode()`会返回根节点。当遍历到 DOM 子树的最后一个节点时， `nextNode()`返回 null。 `previousNode()`方法的工作机制类似。当遍历到 DOM 子树的最后一个节点，且 `previousNode()`返回根节点之后，再次调用它就会返回 null。

以下面的 HTML 片段为例。

```html
<div id="div1">
  <p><b>Hello</b> world!</p>
  <ul>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
  </ul>
</div>
```

假设我们想要遍历`<div>`元素中的所有元素，那么可以使用下列代码。

```js
var div = document.getElementById("div1");
var iterator = document.createNodeIterator(div, NodeFilter.SHOW_ELEMENT,
null, false);
var node = iterator.nextNode();
while (node !== null) {
  alert(node.tagName); //输出标签名
  node = iterator.nextNode();
}
```

在这个例子中，第一次调用 `nextNode()`返回`<p>`元素。因为在到达 DOM 子树末端时 `nextNode()`返回 null，所以这里使用了 while 语句在每次循环时检查对 `nextNode()`的调用是否返回了 null。执行上面的代码会显示如下标签名：

```js
DIV
P
B
UL
LI
LI
LI
```

也许用不着显示那么多信息，你只想返回遍历中遇到的`<li>`元素。很简单，只要使用一个过滤器即可，如下面的例子所示。

```js
var div = document.getElementById("div1");
var filter = function(node){
  return node.tagName.toLowerCase() == "li" ?
  NodeFilter.FILTER_ACCEPT :
  NodeFilter.FILTER_SKIP;
};
var iterator = document.createNodeIterator(div, NodeFilter.SHOW_ELEMENT,
filter, false);
var node = iterator.nextNode();
while (node !== null) {
  alert(node.tagName); //输出标签名
  node = iterator.nextNode();
}
```

在这个例子中，迭代器只会返回`<li>`元素。

由于 `nextNode()`和` previousNode()`方法都基于 NodeIterator 在 DOM 结构中的内部指针工作，所以 DOM 结构的变化会反映在遍历的结果中。

> Firefox 3.5 之前的版本没有实现 `createNodeIterator()`方法，但却支持下一节要讨论的 `createTreeWalker()`方法。

### 12.3.2 TreeWalker

TreeWalker 是 NodeIterator 的一个更高级的版本。除了包括 `nextNode()`和 `previousNode()`在内的相同的功能之外，这个类型还提供了下列用于在不同方向上遍历 DOM 结构的方法。

- parentNode()：遍历到当前节点的父节点；
- firstChild()：遍历到当前节点的第一个子节点；
- lastChild()：遍历到当前节点的最后一个子节点；
- nextSibling()：遍历到当前节点的下一个同辈节点；
- previousSibling()：遍历到当前节点的上一个同辈节点。

创建 TreeWalker 对象要使用 `document.createTreeWalker()`方法，这个方法接受的 4 个参数与 `document.createNodeIterator()`方法相同：作为遍历起点的根节点、要显示的节点类型、过滤器和一个表示是否扩展实体引用的布尔值。由于这两个创建方法很相似，所以很容易用 TreeWalker 来代替 NodeIterator，如下面的例子所示。

```js
var div = document.getElementById("div1");
var filter = function(node){
  return node.tagName.toLowerCase() == "li"?
  NodeFilter.FILTER_ACCEPT :
  NodeFilter.FILTER_SKIP;
};
var walker= document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT,
filter, false);
var node = iterator.nextNode();
while (node !== null) {
  alert(node.tagName); //输出标签名
  node = iterator.nextNode();
}
```

在这里， filter 可以返回的值有所不同。除了 NodeFilter.FILTER_ACCEPT 和 NodeFilter.FILTER_SKIP 之外，还可以使用 NodeFilter.FILTER_REJECT。在使用 NodeIterator 对象时，NodeFilter.FILTER_SKIP 与 NodeFilter.FILTER_REJECT 的作用相同：跳过指定的节点。但在使用 TreeWalker 对象时， NodeFilter.FILTER_SKIP 会跳过相应节点继续前进到子树中的下一个节点，而 NodeFilter.FILTER_REJECT 则会跳过相应节点及该节点的整个子树。例如，将前面例子中的 NodeFilter.FILTER_SKIP 修改成 NodeFilter.FILTER_REJECT，结果就是不会访问任何节点。这是因为第一个返回的节点是`<div>`，它的标签名不是"li"，于是就会返回 NodeFilter.FILTER_REJECT，这意味着遍历会跳过整个子树。在这个例子中， `<div>`元素是遍历的根节点，于是结果就会停止遍历。

当然， TreeWalker 真正强大的地方在于能够在 DOM 结构中沿任何方向移动。使用 TreeWalker 遍历 DOM 树，即使不定义过滤器，也可以取得所有`<li>`元素，如下面的代码所示。

```js
var div = document.getElementById("div1");
var walker = document.createTreeWalker(div, NodeFilter.SHOW_ELEMENT, null, false);
walker.firstChild(); //转到<p>
walker.nextSibling(); //转到<ul>
var node = walker.firstChild(); //转到第一个<li>
while (node !== null) {
  alert(node.tagName);
  node = walker.nextSibling();
}
```

因为我们知道`<li>`元素在文档结构中的位置，所以可以直接定位到那里，即使用 `firstChild()`转到`<p>`元素，使用 `nextSibling()`转到`<ul>`元素，然后再使用 `firstChild()`转到第一个`<li>`元素。注意，此处 TreeWalker 只返回元素（由传入到 `createTreeWalker()`的第二个参数决定）。因此，可以放心地使用 `nextSibling()`访问每一个`<li>`元素，直至这个方法最后返回 null。

TreeWalker 类型还有一个属性，名叫 currentNode，表示任何遍历方法在上一次遍历中返回的节点。通过设置这个属性也可以修改遍历继续进行的起点，如下面的例子所示。

```js
var node = walker.nextNode();
alert(node === walker.currentNode); //true
walker.currentNode = document.body; //修改起点
```

与 NodeIterator 相比， TreeWalker 类型在遍历 DOM 时拥有更大的灵活性。由于 IE 中没有对应的类型和方法，所以使用遍历的跨浏览器解决方案非常少见。

## 12.4 范围

为了让开发人员更方便地控制页面，“DOM2 级遍历和范围”模块定义了“范围”（range）接口。通过范围可以选择文档中的一个区域，而不必考虑节点的界限（选择在后台完成，对用户是不可见的）。在常规的 DOM 操作不能更有效地修改文档时，使用范围往往可以达到目的。 Firefox、 Opera、 Safari 和Chrome 都支持 DOM 范围。 IE 以专有方式实现了自己的范围特性。

### 12.4.1 DOM中的范围

DOM2 级在 Document 类型中定义了 `createRange()`方法。在兼容 DOM 的浏览器中，这个方法属于 document 对象。使用 `hasFeature()`或者直接检测该方法，都可以确定浏览器是否支持范围。

```js
var supportsRange = document.implementation.hasFeature("Range", "2.0");
var alsoSupportsRange = (typeof document.createRange == "function");
```

如果浏览器支持范围，那么就可以使用 `createRange()`来创建 DOM 范围，如下所示：

```js
var range = document.createRange();
```

与节点类似，新创建的范围也直接与创建它的文档关联在一起，不能用于其他文档。创建了范围之后，接下来就可以使用它在后台选择文档中的特定部分。而创建范围并设置了其位置之后，还可以针对范围的内容执行很多种操作，从而实现对底层 DOM 树的更精细的控制。

每个范围由一个 Range 类型的实例表示，这个实例拥有很多属性和方法。下列属性提供了当前范围在文档中的位置信息。

- startContainer：包含范围起点的节点（即选区中第一个节点的父节点）。
- startOffset：范围在 startContainer 中起点的偏移量。如果 startContainer 是文本节点、注释节点或 CDATA 节点，那么 startOffset 就是范围起点之前跳过的字符数量。否则，startOffset 就是范围中第一个子节点的索引。
- endContainer：包含范围终点的节点（即选区中最后一个节点的父节点）。
- endOffset：范围在 endContainer 中终点的偏移量（与 startOffset 遵循相同的取值规则）。
- commonAncestorContainer： startContainer 和 endContainer 共同的祖先节点在文档树中位置最深的那个。

在把范围放到文档中特定的位置时，这些属性都会被赋值。

**1. 用 DOM 范围实现简单选择**

要使用范围来选择文档中的一部分，最简的方式就是使用 `selectNode()`或 `selectNodeContents()`。这两个方法都接受一个参数，即一个 DOM 节点，然后使用该节点中的信息来填充范围。其中，`selectNode()`方法选择整个节点，包括其子节点；而 `selectNodeContents()`方法则只选择节点的子节点。以下面的 HTML 代码为例。

```html
<!DOCTYPE html>
<html>
  <body>
    <p id="p1"><b>Hello</b> world!</p>
  </body>
</html>
```

我们可以使用下列代码来创建范围：

```js
var range1 = document.createRange();
range2 = document.createRange();
p1 = document.getElementById("p1");
range1.selectNode(p1);
range2.selectNodeContents(p1);
```

这里创建的两个范围包含文档中不同的部分： rang1 包含`<p/>`元素及其所有子元素，而 rang2 包含`<b/>`元素、文本节点"Hello"和文本节点"world!"（如图 12-6 所示）。

在调用 `selectNode()`时， startContainer、 endContainer 和 commonAncestorContainer 都等于传入节点的父节点，也就是这个例子中的 document.body。而 startOffset 属性等于给定节点在其父节点的 childNodes 集合中的索引（在这个例子中是 1——因为兼容 DOM 的浏览器将空格算作一个文本节点）， endOffset 等于 startOffset 加 1（因为只选择了一个节点）。

在调用 `selectNodeContents()`时， startContainer、endContainer 和 commonAncestorContainer 等于传入的节点，即这个例子中的`<p>`元素。而 startOffset 属性始终等于 0，因为范围从给定节点的第一个子节点开始。最后， endOffset 等于子节点的数量（ node.childNodes.length），在这个例子中是 2。

此外，为了更精细地控制将哪些节点包含在范围中，还可以使用下列方法。

- setStartBefore(refNode)：将范围的起点设置在 refNode 之前，因此 refNode 也就是范围选区中的第一个子节点。同时会将 startContainer 属性设置为 refNode.parentNode，将startOffset 属性设置为 refNode 在其父节点的 childNodes 集合中的索引。
- setStartAfter(refNode)：将范围的起点设置在 refNode 之后，因此 refNode 也就不在范围之内了，其下一个同辈节点才是范围选区中的第一个子节点。同时会将 startContainer 属性设置为 refNode.parentNode，将 startOffset 属性设置为 refNode 在其父节点的childNodes 集合中的索引加 1。
- setEndBefore(refNode)：将范围的终点设置在 refNode 之前，因此 refNode 也就不在范围之内了，其上一个同辈节点才是范围选区中的最后一个子节点。同时会将 endContainer 属性设置为 refNode.parentNode，将 endOffset 属性设置为 refNode 在其父节点的 childNodes 集合中的索引。
- setEndAfter(refNode)：将范围的终点设置在 refNode 之后，因此 refNode 也就是范围选区中的最后一个子节点。同时会将 endContainer 属性设置为 refNode.parentNode，将 endOffset 属性设置为 refNode 在其父节点的 childNodes 集合中的索引加 1。

在调用这些方法时，所有属性都会自动为你设置好。不过，要想创建复杂的范围选区，也可以直接指定这些属性的值。

**2. 用 DOM 范围实现复杂选择**

要创建复杂的范围就得使用 `setStart()`和 `setEnd()`方法。这两个方法都接受两个参数：一个参照节点和一个偏移量值。对 `setStart()`来说，参照节点会变成 startContainer，而偏移量值会变成startOffset。对于 `setEnd()`来说，参照节点会变成 endContainer，而偏移量值会变成 endOffset。

可以使用这两个方法来模仿 `selectNode()`和 `selectNodeContents()`。来看下面的例子：

```js
var range1 = document.createRange();
range2 = document.createRange();
p1 = document.getElementById("p1");
p1Index = -1;
i, len;
for (i=0, len=p1.parentNode.childNodes.length; i < len; i++) {
  if (p1.parentNode.childNodes[i] == p1) {
    p1Index = i;
    break;
  }
}
range1.setStart(p1.parentNode, p1Index);
range1.setEnd(p1.parentNode, p1Index + 1);
range2.setStart(p1, 0);
range2.setEnd(p1, p1.childNodes.length);
```

显然，要选择这个节点（使用 range1），就必须确定当前节点（ p1）在其父节点的 childNodes 集合中的索引。而要选择这个节点的内容（使用 range2），也不必计算什么；只要通过 `setStart()`和 `setEnd()`设置默认值即可。模仿 `selectNode()`和 `selectNodeContents()`并不是 `setStart()`和 `setEnd()`的主要用途，它们更胜一筹的地方在于能够选择节点的一部分。

假设你只想选择前面 HTML 示例代码中从"Hello"的"llo"到"world!"的"o"——很容易做到。第一步是取得所有节点的引用，如下面的例子所示：

```js
var p1 = document.getElementById("p1");
helloNode = p1.firstChild.firstChild;
worldNode = p1.lastChild;
```

实际上， "Hello"文本节点是`<p>`元素的孙子节点，因为它本身是`<b>`元素的一个子节点。因此，p1.firstChild 取得的是`<b>`，而 p1.firstChild.firstChild 取得的才是这个文本节点。"world!"文本节点是`<p>`元素的第二个子节点（也是最后一个子节点），因此可以使用 p1.lastChild 取得该节点。然后，必须在创建范围时指定相应的起点和终点，如下面的例子所示。

```js
var range = document.createRange();
range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
```

因为这个范围的选区应该从"Hello"中"e"的后面开始，所以在 `setStart()`中传入 helloNode 的同时，传入了偏移量 2（即"e"的下一个位置； "H"的位置是 0）。设置选区的终点时，在 `setEnd()`中传入 worldNode 的同时传入了偏移量 3，表示选区之外的第一个字符的位置，这个字符是"r"，它的位置是 3（位置 0 上还有一个空格）。如图 12-7 所示。

由于 helloNode 和 worldNode 都是文本节点，因此它们分别变成了新建范围的 startContainer 和 endContainer。此时 startOffset 和 endOffset 分别用以确定两个节点所包含的文本中的位置，而不是用以确定子节点的位置（就像传入的参数为元素节点时那样）。此时的 commonAncestorContainer 是`<p>`元素，也就是同时包含这两个节点的第一个祖先元素。

当然，仅仅是选择了文档中的某一部分用处并不大。但重要的是，选择之后才可以对选区进行操作。

**3. 操作 DOM 范围中的内容**

在创建范围时 ，内部会为这个范围创建一个文档片段，范围所属的全部节点都被添加到了这个文档片段中。为了创建这个文档片段，范围内容的格式必须正确有效。在前面的例子中，我们创建的选区分别开始和结束于两个文本节点的内部，因此不能算是格式良好的 DOM 结构，也就无法通过 DOM 来表示。但是，范围知道自身缺少哪些开标签和闭标签，它能够重新构建有效的 DOM 结构以便我们对其进行操作。

对于前面的例子而言，范围经过计算知道选区中缺少一个开始的`<b>`标签，因此就会在后台动态加入一个该标签，同时还会在前面加入一个表示结束的`</b>`标签以结束"He"。于是，修改后的 DOM 就变成了如下所示。

```js
<p><b>He</b><b>llo</b> world!</p>
```

另外，文本节点"world!"也被拆分为两个文本节点，一个包含"wo"，另一个包含"rld!"。最终的DOM 树如图 12-8 所示，右侧是表示范围的文档片段的内容。

像这样创建了范围之后，就可以使用各种方法对范围的内容进行操作了（注意，表示范围的内部文档片段中的所有节点，都只是指向文档中相应节点的指针）。

第一个方法，也是最容易理解的方法，就是 `deleteContents()`。这个方法能够从文档中删除范围所包含的内容。例如：

```js
var p1 = document.getElementById("p1");
helloNode = p1.firstChild.firstChild;
worldNode = p1.lastChild;
range = document.createRange();
range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
range.deleteContents();
```

执行以上代码后，页面中会显示如下 HTML 代码：

```html
<p><b>He</b>rld!</p>
```

由于范围选区在修改底层 DOM 结构时能够保证格式良好，因此即使内容被删除了，最终的 DOM 结构依旧是格式良好的。

与 `deleteContents()`方法相似， `extractContents()`也会从文档中移除范围选区。但这两个方法的区别在于， `extractContents()`会返回范围的文档片段。利用这个返回的值，可以将范围的内容插入到文档中的其他地方。如下面的例子所示：

```js
var p1 = document.getElementById("p1");
helloNode = p1.firstChild.firstChild;
worldNode = p1.lastChild;
range = document.createRange();
range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
var fragment = range.extractContents();
p1.parentNode.appendChild(fragment);
```

在这个例子中，我们将提取出来的文档片段添加到了文档`<body>`元素的末尾。（记住，在将文档片段传入`appendChild()`方法中时，添加到文档中的只是片段的子节点，而非片段本身。）结果得到如下HTML 代码：

```html
<p><b>He</b>rld!</p>
<b>llo</b> wo
```

还一种做法，即使用 `cloneContents()`创建范围对象的一个副本，然后在文档的其他地方插入该副本。如下面的例子所示：

```js
var p1 = document.getElementById("p1"),
helloNode = p1.firstChild.firstChild,
worldNode = p1.lastChild,
range = document.createRange();
range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
var fragment = range.cloneContents();
p1.parentNode.appendChild(fragment);
```

这个方法与 `extractContents()`非常类似，因为它们都返回文档片段。它们的主要区别在于，`cloneContents()`返回的文档片段包含的是范围中节点的副本，而不是实际的节点。执行上面的操作后，页面中的 HTML 代码应该如下所示：

```html
<p><b>Hello</b> world!</p>
<b>llo</b> wo
```

有一点请读者注意，那就是在调用上面介绍的方法之前，拆分的节点并不会产生格式良好的文档片段。换句话说，原始的 HTML 在 DOM 被修改之前会始终保持不变。

**4. 插入 DOM 范围中的内容**

利用范围，可以删除或复制内容，还可以像前面介绍的那样操作范围中的内容。 使用 `insertNode()`方法可以向范围选区的开始处插入一个节点。假设我们想在前面例子中的 HTML 前面插入以下 HTML
代码：

```html
<span style="color: red">Inserted text</span>
```

那么，就可以使用下列代码：

```js
var p1 = document.getElementById("p1");
helloNode = p1.firstChild.firstChild;
worldNode = p1.lastChild;
range = document.createRange();
range.setStart(helloNode, 2);
range.setEnd(worldNode, 3);
var span = document.createElement("span");
span.style.color = "red";
span.appendChild(document.createTextNode("Inserted text"));
range.insertNode(span);
```

运行以上 JavaScript 代码，就会得到如下 HTML 代码：

```html
<p id="p1"><b>He<span style="color: red">Inserted text</span>llo</b> world</p>
```

注意， `<span>`正好被插入到了"Hello"中的"llo"前面，而该位置就是范围选区的开始位置。还要注意的是，由于这里没有使用上一节介绍的方法，结果原始的 HTML 并没有添加或删除`<b>`元素。使用这种技术可以插入一些帮助提示信息，例如在打开新窗口的链接旁边插入一幅图像。

除了向范围内部插入内容之外，还可以环绕范围插入内容，此时就要使用 `surroundContents()`方法。这个方法接受一个参数，即环绕范围内容的节点。在环绕范围插入内容时，后台会执行下列步骤。

(1) 提取出范围中的内容（类似执行 `extractContent()`）；
(2) 将给定节点插入到文档中原来范围所在的位置上；
(3) 将文档片段的内容添加到给定节点中。

可以使用这种技术来突出显示网页中的某些词句，例如下列代码：

```js
var p1 = document.getElementById("p1");
helloNode = p1.firstChild.firstChild;
worldNode = p1.lastChild;
range = document.createRange();
range.selectNode(helloNode);
var span = document.createElement("span");
span.style.backgroundColor = "yellow";
range.surroundContents(span);
```

会给范围选区加上一个黄色的背景。得到的 HTML 代码如下所示：

```html
<p><b><span style="background-color:yellow">Hello</span></b> world!</p>
```

为了插入`<span>`，范围必须包含整个 DOM 选区（不能仅仅包含选中的 DOM 节点）。

**5. 折叠 DOM 范围**

所谓折叠范围，就是指范围中未选择文档的任何部分。可以用文本框来描述折叠范围的过程。假设文本框中有一行文本，你用鼠标选择了其中一个完整的单词。然后，你单击鼠标左键，选区消失，而光标则落在了其中两个字母之间。同样，在折叠范围时，其位置会落在文档中的两个部分之间，可能是范围选区的开始位置，也可能是结束位置。图 12-9 展示了折叠范围时发生的情形。

使用`collapse()`方法来折叠范围，这个方法接受一个参数，一个布尔值，表示要折叠到范围的哪一端。参数 true 表示折叠到范围的起点，参数 false 表示折叠到范围的终点。要确定范围已经折叠完毕，可以检查 collapsed 属性，如下所示：

```js
range.collapse(true); //折叠到起点
alert(range.collapsed); //输出 true
```

检测某个范围是否处于折叠状态，可以帮我们确定范围中的两个节点是否紧密相邻。例如，对于下面的 HTML 代码：

```html
<p id="p1">Paragraph 1</p><p id="p2">Paragraph 2</p>
```

如果我们不知道其实际构成（比如说，这行代码是动态生成的）， 那么可以像下面这样创建一个范围。

```js
var p1 = document.getElementById("p1"),
p2 = document.getElementById("p2"),
range = document.createRange();
range.setStartAfter(p1);
range.setStartBefore(p2);
alert(range.collapsed); //输出 true
```

在这个例子中，新创建的范围是折叠的，因为 p1 的后面和 p2 的前面什么也没有。

**6. 比较 DOM 范围**

在有多个范围的情况下，可以使用 `compareBoundaryPoints()`方法来确定这些范围是否有公共的边界（起点或终点）。这个方法接受两个参数：表示比较方式的常量值和要比较的范围。表示比较方式的常量值如下所示。

- Range.START_TO_START(0)：比较第一个范围和第二个范围的起点；
- Range.START_TO_END(1)：比较第一个范围的起点和第二个范围的终点；
- Range.END_TO_END(2)：比较第一个范围和第二个范围的终点；
- Range.END_TO_START(3)：比较第一个范围的终点和第一个范围的起点。

`compareBoundaryPoints()`方法可能的返回值如下：如果第一个范围中的点位于第二个范围中的点之前，返回-1；如果两个点相等，返回 0；如果第一个范围中的点位于第二个范围中的点之后，返回1。来看下面的例子。

```js
var range1 = document.createRange();
var range2 = document.createRange();
var p1 = document.getElementById("p1");
range1.selectNodeContents(p1);
range2.selectNodeContents(p1);
range2.setEndBefore(p1.lastChild);
alert(range1.compareBoundaryPoints(Range.START_TO_START, range2)); //0
alert(range1.compareBoundaryPoints(Range.END_TO_END, range2)); //1
```

在这个例子中，两个范围的起点实际上是相同的，因为它们的起点都是由 `selectNodeContents()`方法设置的默认值来指定的。因此，第一次比较返回 0。但是， range2 的终点由于调用 setEndBefore()经改变了，结果是 range1 的终点位于 range2 的终点后面（见图 12-10），因此第二次比较返回 1。

**7. 复制 DOM 范围**

可以使用 `cloneRange()`方法复制范围。这个方法会创建调用它的范围的一个副本。

```js
var newRange = range.cloneRange();
```

新创建的范围与原来的范围包含相同的属性，而修改它的端点不会影响原来的范围。

**8. 清理 DOM 范围**

在使用完范围之后，最好是调用 `detach()`方法，以便从创建范围的文档中分离出该范围。调用`detach()`之后，就可以放心地解除对范围的引用，从而让垃圾回收机制回收其内存了。来看下面的例子。

```js
range.detach(); //从文档中分离
range = null; //解除引用
```

在使用范围的最后再执行这两个步骤是我们推荐的方式。一旦分离范围，就不能再恢复使用了。

### 12.4.2 IE8 及更早版本中的范围

虽然 IE9 支持 DOM 范围，但 IE8 及之前版本不支持 DOM 范围。不过， IE8 及早期版本支持一种类似的概念，即文本范围（ text range）。文本范围是 IE 专有的特性，其他浏览器都不支持。顾名思义，文本范围处理的主要是文本（不一定是 DOM 节点）。通过`<body>`、 `<button>`、 `<input>`和`<textarea>`等这几个元素，可以调用 `createTextRange()`方法来创建文本范围。以下是一个例子：

```js
var range = document.body.createTextRange();
```

像这样通过 document 创建的范围可以在页面中的任何地方使用（通过其他元素创建的范围则只能在相应的元素中使用）。与 DOM 范围类似，使用 IE 文本范围的方式也有很多种。

**1. 用 IE 范围实现简单的选择**

选择页面中某一区域的最简单方式，就是使用范围的 `findText()`方法。这个方法会找到第一次出现的给定文本，并将范围移过来以环绕该文本。如果没有找到文本，这个方法返回 false；否则返回true。同样，仍然以下面的 HTML 代码为例。

```html
<p id="p1"><b>Hello</b> world!</p>
```

要选择"Hello"，可以使用下列代码。

```js
var range = document.body.createTextRange();
var found = range.findText("Hello");
```

在执行完第二行代码之后，文本"Hello"就被包围在范围之内了。为此，可以检查范围的 text 属性来确认（这个属性返回范围中包含的文本），或者也可以检查 `findText()`的返回值——在找到了文本的情况下返回值为 true。例如：

```js
alert(found); //true
alert(range.text); //"Hello"
```

还可以为 `findText()`传入另一个参数，即一个表示向哪个方向继续搜索的数值。负值表示应该从当前位置向后搜索，而正值表示应该从当前位置向前搜索。因此，要查找文档中前两个"Hello"的实例，应该使用下列代码。

```js
var found = range.findText("Hello");
var foundAgain = range.findText("Hello", 1);
```

IE 中与 DOM 中的 `selectNode()`方法最接近的方法是 `moveToElementText()`，这个方法接受一个 DOM 元素，并选择该元素的所有文本，包括 HTML 标签。下面是一个例子。

```js
var range = document.body.createTextRange();
var p1 = document.getElementById("p1");
range.moveToElementText(p1);
```

在文本范围中包含 HTML 的情况下，可以使用 htmlText 属性取得范围的全部内容，包括 HTML 和文本，如下面的例子所示。

```js
alert(range.htmlText);
```

IE 的范围没有任何属性可以随着范围选区的变化而动态更新。不过，其 `parentElement()`方法倒是与 DOM 的 commonAncestorContainer 属性类似。

```js
var ancestor = range.parentElement();
```

这样得到的父元素始终都可以反映文本选区的父节点。

**2. 使用 IE 范围实现复杂的选择**

在 IE 中创建复杂范围的方法，就是以特定的增量向四周移动范围。为此， IE 提供了 4 个方法：`move()`、 `moveStart()`、 `moveEnd()`和 `expand()`。这些方法都接受两个参数：移动单位和移动单位的数量。其中，移动单位是下列一种字符串值。

- "character"：逐个字符地移动。
- "word"：逐个单词（一系列非空格字符）地移动。
- "sentence"：逐个句子（一系列以句号、问号或叹号结尾的字符）地移动。
- "textedit"：移动到当前范围选区的开始或结束位置。

通过 `moveStart()`方法可以移动范围的起点，通过 `moveEnd()`方法可以移动范围的终点，移动的幅度由单位数量指定，如下面的例子所示。

```js
range.moveStart("word", 2); //起点移动 2 个单词
range.moveEnd("character", 1); //终点移动 1 个字符
```

使用 `expand()`方法可以将范围规范化。换句话说， `expand()`方法的作用是将任何部分选择的文本全部选中。例如，当前选择的是一个单词中间的两个字符，调用 `expand("word")`可以将整个单词都包含在范围之内。

而 `move()`方法则首先会折叠当前范围（让起点和终点相等），然后再将范围移动指定的单位数量，如下面的例子所示。

```js
range.move("character", 5); //移动 5 个字符
```

调用 `move()`之后，范围的起点和终点相同，因此必须再使用 `moveStart()`或 `moveEnd()`创建新的选区。

**3. 操作 IE 范围中的内容**

在 IE 中操作范围中的内容可以使用 text 属性或 `pasteHTML()`方法。如前所述，通过 text 属性可以取得范围中的内容文本；但是，也可以通过这个属性设置范围中的内容文本。来看一个例子。

```js
var range = document.body.createTextRange();
range.findText("Hello");
range.text = "Howdy";
```

如果仍以前面的 Hello World 代码为例，执行以上代码后的 HTML 代码如下。

```html
<p id="p1"><b>Howdy</b> world!</p>
```

注意，在设置 text 属性的情况下， HTML 标签保持不变。

要向范围中插入 HTML 代码，就得使用 `pasteHTML()`方法，如下面的例子所示。

```js
var range = document.body.createTextRange();
range.findText("Hello");
range.pasteHTML("<em>Howdy</em>");
```

执行这些代码后，会得到如下 HTML。

```html
<p id="p1"><b><em>Howdy</em></b> world!</p>
```

不过，在范围中包含 HTML 代码时，不应该使用 `pasteHTML()`，因为这样很容易导致不可预料的结果——很可能是格式不正确的 HTML。

**4. 折叠 IE 范围**

IE 为范围提供的`collapse()`方法与相应的 DOM 方法用法一样：传入 true 把范围折叠到起点，传入 false 把范围折叠到终点。例如：

```js
range.collapse(true); //折叠到起点
```

可惜的是，没有对应的 collapsed 属性让我们知道范围是否已经折叠完毕。为此，必须使用boundingWidth 属性，该属性返回范围的宽度（以像素为单位）。如果 boundingWidth 属性等于 0，就说明范围已经折叠了：

```js
var isCollapsed = (range.boundingWidth == 0);
```

此外，还有 boundingHeight、 boundingLeft 和 boundingTop 等属性，虽然它们都不像boundingWidth 那么有用，但也可以提供一些有关范围位置的信息。

**5. 比较 IE 范围**

IE 中的 `compareEndPoints()`方法与 DOM 范围的 `compareBoundaryPoints()`方法类似。这个方法接受两个参数：比较的类型和要比较的范围。比较类型的取值范围是下列几个字符串值："StartToStart"、 "StartToEnd"、 "EndToEnd"和"EndToStart"。这几种比较类型与比较 DOM 范围时使用的几个值是相同的。

同样与 DOM 类似的是， `compareEndPoints()`方法也会按照相同的规则返回值，即如果第一个范围的边界位于第二个范围的边界前面，返回-1；如果二者边界相同，返回 0；如果第一个范围的边界位于第二个范围的边界后面，返回 1。仍以前面的 Hello World 代码为例，下列代码将创建两个范围，一个选择"Hello world!"（包括`<b>`标签），另一个选择"Hello"。

```js
var range1 = document.body.createTextRange();
var range2 = document.body.createTextRange();
range1.findText("Hello world!");
range2.findText("Hello");
alert(range1.compareEndPoints("StartToStart", range2)); //0
alert(range1.compareEndPoints("EndToEnd", range2)); //1
```

由于这两个范围共享同一个起点，所以使用 `compareEndPoints()`比较起点返回 0。而 range1 的终点在 range2 的终点后面，所以 `compareEndPoints()`返回 1。

IE 中还有两个方法，也是用于比较范围的： `isEqual()`用于确定两个范围是否相等， `inRange()`用于确定一个范围是否包含另一个范围。下面是相应的示例。

```js
var range1 = document.body.createTextRange();
var range2 = document.body.createTextRange();
range1.findText("Hello World");
range2.findText("Hello");
alert("range1.isEqual(range2): " + range1.isEqual(range2)); //false
alert("range1.inRange(range2):" + range1.inRange(range2)); //true
```

这个例子使用了与前面相同的范围来示范这两个方法。由于这两个范围的终点不同，所以它们不相等，调用 `isEqual()`返回 false。由于 range2 实际位于 range1 内部，它的终点位于后者的终点之前、起点之后，所以 range2 被包含在 range1 内部，调用 `inRange()`返回 true。

**6. 复制 IE 范围**

在 IE 中使用` duplicate()`方法可以复制文本范围，结果会创建原范围的一个副本，如下面的例子所示。

```js
var newRange = range.duplicate();
```

新创建的范围会带有与原范围完全相同的属性。

## 12.5 小结　

DOM2 级规范定义了一些模块，用于增强 DOM1 级。“DOM2 级核心”为不同的 DOM 类型引入了一些与 XML 命名空间有关的方法。这些变化只在使用 XML 或 XHTML 文档时才有用；对于 HTML 文档没有实际意义。除了与 XML 命名空间有关的方法外，“DOM2 级核心”还定义了以编程方式创建Document 实例的方法，也支持了创建 DocumentType 对象。

“DOM2 级样式”模块主要针对操作元素的样式信息而开发，其特性简要总结如下。

+ 每个元素都有一个关联的 style 对象，可以用来确定和修改行内的样式。
+ 要确定某个元素的计算样式（包括应用给它的所有 CSS 规则），可以使用`getComputedStyle()`方法。
+ IE 不支持`getComputedStyle()`方法，但为所有元素都提供了能够返回相同信息 currentStyle属性。
+ 可以通过 document.styleSheets 集合访问样式表。
+ 除 IE 之外的所有浏览器都支持针对样式表的这个接口， IE 也为几乎所有相应的 DOM 功能提供了自己的一套属性和方法。

“DOM2 级遍历和范围”模块提供了与 DOM 结构交互的不同方式，简要总结如下。

+ 遍历即使用 NodeIterator 或 TreeWalker 对 DOM 执行深度优先的遍历。
+ NodeIterator 是一个简单的接口，只允许以一个节点的步幅前后移动。而 TreeWalker 在提供相同功能的同时，还支持在 DOM 结构的各个方向上移动，包括父节点、同辈节点和子节点等方向。
+ 范围是选择 DOM 结构中特定部分，然后再执行相应操作的一种手段。
+ 使用范围选区可以在删除文档中某些部分的同时，保持文档结构的格式良好，或者复制文档中的相应部分。
+ IE8 及更早版本不支持“DOM2 级遍历和范围”模块，但它提供了一个专有的文本范围对象，可以用来完成简单的基于文本的范围操作。 IE9 完全支持 DOM 遍历。

# 第13章 事件　

JavaScript 与 HTML 之间的交互是通过事件实现的。事件，就是文档或浏览器窗口中发生的一些特定的交互瞬间。可以使用侦听器（或处理程序）来预订事件，以便事件发生时执行相应的代码。这种在传统软件工程中被称为观察员模式的模型，支持页面的行为（JavaScript 代码）与页面的外观（HTML 和 CSS 代码）之间的松散耦合。

事件最早是在 IE3 和 Netscape Navigator 2 中出现的，当时是作为分担服务器运算负载的一种手段。在 IE4 和 Navigator 4 发布时，这两种浏览器都提供了相似但不相同的 API，这些 API 并存经过了好几个主要版本。 DOM2 级规范开始尝试以一种符合逻辑的方式来标准化 DOM 事件。 IE9、 Firefox、 Opera、 Safari 和 Chrome 全都已经实现了“DOM2 级事件”模块的核心部分。 IE8 是最后一个仍然使用其专有事件系统的主要浏览器。

浏览器的事件系统相对比较复杂。尽管所有主要浏览器已经实现了“DOM2 级事件”，但这个规范本身并没有涵盖所有事件类型。浏览器对象模型（BOM）也支持一些事件，这些事件与文档对象模型（DOM）事件之间的关系并不十分清晰，因为 BOM 事件长期没有规范可以遵循（HTML5 后来给出了详细的说明）。随着 DOM3 级的出现，增强后的 DOM 事件 API 变得更加繁琐。使用事件有时相对简单，有时则非常复杂，难易程度会因你的需求而不同。不过，有关事件的一些核心概念是一定要理解的。

## 13.1 事件流 

当浏览器发展到第四代时（IE4 及 Netscape Communicator 4），浏览器开发团队遇到了一个很有意思的问题：页面的哪一部分会拥有某个特定的事件？要明白这个问题问的是什么，可以想象画在一张纸上的一组同心圆。如果你把手指放在圆心上，那么你的手指指向的不是一个圆，而是纸上的所有圆。两家公司的浏览器开发团队在看待浏览器事件方面还是一致的。如果你单击了某个按钮，他们都认为单击事件不仅仅发生在按钮上。换句话说，在单击按钮的同时，你也单击了按钮的容器元素，甚至也单击了整个页面。

事件流描述的是从页面中接收事件的顺序。但有意思的是， IE 和 Netscape 开发团队居然提出了差不多是完全相反的事件流的概念。 IE 的事件流是事件冒泡流，而 Netscape Communicator 的事件流是事件捕获流。

### 13.1.1 事件冒泡

IE 的事件流叫做事件冒泡（event bubbling），即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）。以下面的 HTML 页面为例：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Event Bubbling Example</title>
  </head>
  <body>
    <div id="myDiv">Click Me</div>
  </body>
</html>
```

如果你单击了页面中的`<div>`元素，那么这个 click 事件会按照如下顺序传播：

1. `<div>`
2. `<body>`
3. `<html>`
4. document

也就是说， click 事件首先在`<div>`元素上发生，而这个元素就是我们单击的元素。然后， click 事件沿 DOM 树向上传播，在每一级节点上都会发生，直至传播到 document 对象。图 13-1 展示了事件冒泡的过程。

所有现代浏览器都支持事件冒泡，但在具体实现上还是有一些差别。 IE5.5 及更早版本中的事件冒泡会跳过`<html>`元素（从`<body>`直接跳到 document）。 IE9、 Firefox、 Chrome 和 Safari 则将事件一直冒泡到 window 对象。

### 13.1.2 事件捕获

Netscape Communicator 团队提出的另一种事件流叫做事件捕获（event capturing）。事件捕获的思想是不太具体的节点应该更早接收到事件，而最具体的节点应该最后接收到事件。事件捕获的用意在于在事件到达预定目标之前捕获它。如果仍以前面的 HTML 页面作为演示事件捕获的例子，那么单击`<div>`元素就会以下列顺序触发 click 事件。

1. document
2. `<html>`
3. `<body>`
4. `<div>`

在事件捕获过程中， document 对象首先接收到 click 事件，然后事件沿 DOM 树依次向下，一直传播到事件的实际目标，即`<div>`元素。图 13-2 展示了事件捕获的过程。

虽然事件捕获是 Netscape Communicator 唯一支持的事件流模型，但 IE9、 Safari、 Chrome、 Opera 和 Firefox 目前也都支持这种事件流模型。尽管“DOM2 级事件”规范要求事件应该从 document 对象开始传播，但这些浏览器都是从 window 对象开始捕获事件的。

由于老版本的浏览器不支持，因此很少有人使用事件捕获。我们也建议读者放心地使用事件冒泡，在有特殊需要时再使用事件捕获。

### 13.1.3 DOM事件流

“DOM2级事件”规定的事件流包括三个阶段：事件捕获阶段、处于目标阶段和事件冒泡阶段。首先发生的是事件捕获，为截获事件提供了机会。然后是实际的目标接收到事件。最后一个阶段是冒泡阶段，可以在这个阶段对事件做出响应。以前面简单的 HTML 页面为例，单击`<div>`元素会按照图13-3所示顺序触发事件。

1. document
2. `<html>`
3. `<body>`
4. `<div>`
5. `<body>`
6. `<html>`
7. document

在 DOM 事件流中，实际的目标（`<div>`元素）在捕获阶段不会接收到事件。这意味着在捕获阶段，事件从 document 到`<html>`再到`<body>`后就停止了。下一个阶段是“处于目标”阶段，于是事件在`<div>`上发生，并在事件处理（后面将会讨论这个概念）中被看成冒泡阶段的一部分。然后，冒泡阶段发生，事件又传播回文档。

多数支持 DOM 事件流的浏览器都实现了一种特定的行为；即使“DOM2 级事件”规范明确要求捕获阶段不会涉及事件目标，但 IE9、 Safari、 Chrome、 Firefox 和 Opera 9.5 及更高版本都会在捕获阶段触发事件对象上的事件。结果，就是有两个机会在目标对象上面操作事件。

> IE9、 Opera、 Firefox、 Chrome 和 Safari 都支持 DOM 事件流； IE8 及更早版本不支持 DOM 事件流。

## 13.2 事件处理程序

事件就是用户或浏览器自身执行的某种动作。诸如 click、 load 和 mouseover，都是事件的名字。而响应某个事件的函数就叫做事件处理程序（或事件侦听器）。事件处理程序的名字以"on"开头，因此click 事件的事件处理程序就是 onclick， load 事件的事件处理程序就是 onload。为事件指定处理程序的方式有好几种。

### 13.2.1 HTML事件处理程序

某个元素支持的每种事件，都可以使用一个与相应事件处理程序同名的 HTML 特性来指定。这个特性的值应该是能够执行的 JavaScript 代码。例如，要在按钮被单击时执行一些 JavaScript，可以像下面这样编写代码：

```html
<input type="button" value="Click Me" onclick="alert('Clicked')" />
```

当单击这个按钮时，就会显示一个警告框。这个操作是通过指定 onclick 特性并将一些 JavaScript 代码作为它的值来定义的。由于这个值是 JavaScript，因此不能在其中使用未经转义的 HTML 语法字符，例如和号（&）、双引号（""）、小于号（<）或大于号（>）。为了避免使用 HTML 实体，这里使用了单引号。如果想要使用双引号，那么就要将代码改写成如下所示：

```html
<input type="button" value="Click Me" onclick="alert(&quot;Clicked&quot;)" />
```

在 HTML 中定义的事件处理程序可以包含要执行的具体动作，也可以调用在页面其他地方定义的脚本，如下面的例子所示：

```html
<script type="text/javascript">
  function showMessage(){
    alert("Hello world!");
  }
</script>
<input type="button" value="Click Me" onclick="showMessage()" />
```

在这个例子中，单击按钮就会调用 `showMessage()`函数。这个函数是在一个独立的`<script>`元素中定义的，当然也可以被包含在一个外部文件中。事件处理程序中的代码在执行时，有权访问全局作用域中的任何代码。

这样指定事件处理程序具有一些独到之处。首先，这样会创建一个封装着元素属性值的函数。这个函数中有一个局部变量 event，也就是事件对象（本章稍后讨论）：

```html
<!-- 输出 "click" -->
<input type="button" value="Click Me" onclick="alert(event.type)">
```

通过 event 变量，可以直接访问事件对象，你不用自己定义它，也不用从函数的参数列表中读取。在这个函数内部， this 值等于事件的目标元素，例如：

```html
<!-- 输出 "Click Me" -->
<input type="button" value="Click Me" onclick="alert(this.value)">
```

关于这个动态创建的函数，另一个有意思的地方是它扩展作用域的方式。在这个函数内部，可以像访问局部变量一样访问 document 及该元素本身的成员。这个函数使用 with 像下面这样扩展作用域：

```js
function(){
  with(document){
    with(this){
      //元素属性值
    }
  }
}
```

如此一来，事件处理程序要访问自己的属性就简单多了。下面这行代码与前面的例子效果相同：

```html
<!-- 输出 "Click Me" -->
<input type="button" value="Click Me" onclick="alert(value)">
```

如果当前元素是一个表单输入元素，则作用域中还会包含访问表单元素（父元素）的入口，这个函数就变成了如下所示：

```js
function(){
  with(document){
    with(this.form){
      with(this){
        //元素属性值
      }
    }
  }
}
```

实际上，这样扩展作用域的方式，无非就是想让事件处理程序无需引用表单元素就能访问其他表单字段。例如：

```html
<form method="post">
  <input type="text" name="username" value="">
  <input type="button" value="Echo Username" onclick="alert(username.value)">
</form>
```

在这个例子中，单击按钮会显示文本框中的文本。值得注意的是，这里直接引用了 username 元素。

不过，在 HTML 中指定事件处理程序有两个缺点。首先，存在一个时差问题。因为用户可能会在 HTML 元素一出现在页面上就触发相应的事件，但当时的事件处理程序有可能尚不具备执行条件。以前面的例子来说明，假设 `showMessage()`函数是在按钮下方、页面的最底部定义的。如果用户在页面解析 `showMessage()`函数之前就单击了按钮，就会引发错误。为此，很多 HTML 事件处理程序都会被封装在一个 try-catch 块中，以便错误不会浮出水面，如下面的例子所示：

```html
<input type="button" value="Click Me" onclick="try{showMessage();}catch(ex){}">
```

这样，如果在 `showMessage()`函数有定义之前单击了按钮，用户将不会看到 JavaScript 错误，因为在浏览器有机会处理错误之前，错误就被捕获了。

另一个缺点是，这样扩展事件处理程序的作用域链在不同浏览器中会导致不同结果。不同 JavaScript 引擎遵循的标识符解析规则略有差异，很可能会在访问非限定对象成员时出错。

通过 HTML 指定事件处理程序的最后一个缺点是 HTML 与 JavaScript 代码紧密耦合。如果要更换事件处理程序，就要改动两个地方： HTML 代码和 JavaScript 代码。而这正是许多开发人员摒弃 HTML 事件处理程序，转而使用 JavaScript 指定事件处理程序的原因所在。

> 要了解关于 HTML 事件处理程序缺点的更多信息，请参考 Garrett Smith 的文章“[Event Handler Scope](www.jibbering.com/faq/names/event_handler.html)”。

### 13.2.2 DOM0级事件处理程序

通过 JavaScript 指定事件处理程序的传统方式，就是将一个函数赋值给一个事件处理程序属性。这种为事件处理程序赋值的方法是在第四代 Web 浏览器中出现的，而且至今仍然为所有现代浏览器所支持。原因一是简单，二是具有跨浏览器的优势。要使用 JavaScript 指定事件处理程序，首先必须取得一个要操作的对象的引用。

每个元素（包括 window 和 document）都有自己的事件处理程序属性，这些属性通常全部小写，例如 onclick。将这种属性的值设置为一个函数，就可以指定事件处理程序，如下所示：

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  alert("Clicked");
};
```

在此，我们通过文档对象取得了一个按钮的引用，然后为它指定了 onclick 事件处理程序。但要注意，在这些代码运行以前不会指定事件处理程序，因此如果这些代码在页面中位于按钮后面，就有可能在一段时间内怎么单击都没有反应。

使用 DOM0 级方法指定的事件处理程序被认为是元素的方法。因此，这时候的事件处理程序是在元素的作用域中运行；换句话说，程序中的 this 引用当前元素。来看一个例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  alert(this.id); //"myBtn"
};
```

单击按钮显示的是元素的 ID，这个 ID 是通过 this.id 取得的。不仅仅是 ID，实际上可以在事件处理程序中通过 this 访问元素的任何属性和方法。以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理。

也可以删除通过 DOM0 级方法指定的事件处理程序，只要像下面这样将事件处理程序属性的值设置为 null 即可：

```js
btn.onclick = null; //删除事件处理程序
```

将事件处理程序设置为 null 之后，再单击按钮将不会有任何动作发生。

> 如果你使用 HTML 指定事件处理程序，那么 onclick 属性的值就是一个包含着在同名 HTML 特性中指定的代码的函数。而将相应的属性设置为 null，也可以删除以这种方式指定的事件处理程序。

### 13.2.3 DOM2级事件处理程序

“DOM2 级事件” 定义了两个方法，用于处理指定和删除事件处理程序的操作： `addEventListener()`和 `removeEventListener()`。所有 DOM 节点中都包含这两个方法，并且它们都接受 3 个参数：要处理的事件名、作为事件处理程序的函数和一个布尔值。最后这个布尔值参数如果是 true，表示在捕获阶段调用事件处理程序；如果是 false，表示在冒泡阶段调用事件处理程序。

要在按钮上为 click 事件添加事件处理程序，可以使用下列代码：

```js
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
  alert(this.id);
}, false);
```

上面的代码为一个按钮添加了 onclick 事件处理程序，而且该事件会在冒泡阶段被触发（因为最后一个参数是 false）。与 DOM0 级方法一样，这里添加的事件处理程序也是在其依附的元素的作用域中运行。使用 DOM2 级方法添加事件处理程序的主要好处是可以添加多个事件处理程序。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
  alert(this.id);
}, false);
btn.addEventListener("click", function(){
  alert("Hello world!");
}, false);
```

这里为按钮添加了两个事件处理程序。这两个事件处理程序会按照添加它们的顺序触发，因此首先会显示元素的 ID，其次会显示"Hello world!"消息。

通过 `addEventListener()`添加的事件处理程序只能使用 `removeEventListener()`来移除；移除时传入的参数与添加处理程序时使用的参数相同。这也意味着通过 `addEventListener()`添加的匿名函数将无法移除，如下面的例子所示。

```js
var btn = document.getElementById("myBtn");
btn.addEventListener("click", function(){
  alert(this.id);
}, false);

//这里省略了其他代码
btn.removeEventListener("click", function(){ //没有用！
  alert(this.id);
}, false);
```

在这个例子中，我们使用 `addEventListener()`添加了一个事件处理程序。虽然调用 `removeEventListener()`时看似使用了相同的参数，但实际上，第二个参数与传入 `addEventListener()`中的那一个是完全不同的函数。而传入 `removeEventListener()`中的事件处理程序函数必须与传入`addEventListener()`中的相同，如下面的例子所示。

```js
var btn = document.getElementById("myBtn");
var handler = function(){
  alert(this.id);
};
btn.addEventListener("click", handler, false);
//这里省略了其他代码
btn.removeEventListener("click", handler, false); //有效！
```

重写后的这个例子没有问题，是因为在 `addEventListener()`和 `removeEventListener()`中使用了相同的函数。

大多数情况下，都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度地兼容各种浏览器。最好只在需要在事件到达目标之前截获它的时候将事件处理程序添加到捕获阶段。如果不是特别需要，我们不建议在事件捕获阶段注册事件处理程序。

> IE9、 Firefox、 Safari、 Chrome 和 Opera 支持 DOM2 级事件处理程序。

### 13.2.4 IE事件处理程序

IE 实现了与 DOM 中类似的两个方法： `attachEvent()`和 `detachEvent()`。这两个方法接受相同的两个参数：事件处理程序名称与事件处理程序函数。由于 IE8 及更早版本只支持事件冒泡，所以通过`attachEvent()`添加的事件处理程序都会被添加到冒泡阶段。

要使用 `attachEvent()`为按钮添加一个事件处理程序，可以使用以下代码。

```js
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
  alert("Clicked");
});
```

注意， `attachEvent()`的第一个参数是"onclick"，而非 DOM 的 `addEventListener()`方法中
的"click"。

在 IE 中使用 `attachEvent()`与使用 DOM0 级方法的主要区别在于事件处理程序的作用域。在使用 DOM0 级方法的情况下，事件处理程序会在其所属元素的作用域内运行；在使用 `attachEvent()`方法的情况下，事件处理程序会在全局作用域中运行，因此 this 等于 window。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
  alert(this === window); //true
});
```

在编写跨浏览器的代码时，牢记这一区别非常重要。

与 `addEventListener()`类似， `attachEvent()`方法也可以用来为一个元素添加多个事件处理程序。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(){
  alert("Clicked");
});
btn.attachEvent("onclick", function(){
  alert("Hello world!");
});
```

这里调用了两次 `attachEvent()`，为同一个按钮添加了两个不同的事件处理程序。不过，与 DOM 方法不同的是，这些事件处理程序不是以添加它们的顺序执行，而是以相反的顺序被触发。单击这个例子中的按钮，首先看到的是"Hello world!"，然后才是"Clicked"。

使用 `attachEvent()`添加的事件可以通过 `detachEvent()`来移除，条件是必须提供相同的参数。与 DOM 方法一样，这也意味着添加的匿名函数将不能被移除。不过，只要能够将对相同函数的引用传给 `detachEvent()`，就可以移除相应的事件处理程序。例如：

```js
var btn = document.getElementById("myBtn");
var handler = function(){
  alert("Clicked");
};
btn.attachEvent("onclick", handler);

//这里省略了其他代码
btn.detachEvent("onclick", handler);
```

这个例子将保存在变量 handler 中的函数作为事件处理程序。因此，后面的 `detachEvent()`可以使用相同的函数来移除事件处理程序。

> 支持 IE 事件处理程序的浏览器有 IE 和 Opera。

### 13.2.5 跨浏览器的事件处理程序

为了以跨浏览器的方式处理事件，不少开发人员会使用能够隔离浏览器差异的 JavaScript 库，还有一些开发人员会自己开发最合适的事件处理的方法。自己编写代码其实也不难，只要恰当地使用能力检测即可（能力检测在第 9 章介绍过）。要保证处理事件的代码能在大多数浏览器下一致地运行，只需关注冒泡阶段。

第一个要创建的方法是 `addHandler()`，它的职责是视情况分别使用 DOM0 级方法、 DOM2 级方法或 IE 方法来添加事件。这个方法属于一个名叫 EventUtil 的对象，本书将使用这个对象来处理浏览器间的差异。 `addHandler()`方法接受 3 个参数：要操作的元素、事件名称和事件处理程序函数。

与 `addHandler()`对应的方法是 `removeHandler()`，它也接受相同的参数。这个方法的职责是移除之前添加的事件处理程序——无论该事件处理程序是采取什么方式添加到元素中的，如果其他方法无效，默认采用 DOM0 级方法。

EventUtil 的用法如下所示。

```js
var EventUtil = {
  addHandler: function(element, type, handler){
    if (element.addEventListener){
      element.addEventListener(type, handler, false);
    } else if (element.attachEvent){
      element.attachEvent("on" + type, handler);
    } else {
    element["on" + type] = handler;
    }
  },
  removeHandler: function(element, type, handler){
    if (element.removeEventListener){
      element.removeEventListener(type, handler, false);
    } else if (element.detachEvent){
      element.detachEvent("on" + type, handler);
    } else {
      element["on" + type] = null;
    }
  }
};
```

这两个方法首先都会检测传入的元素中是否存在 DOM2 级方法。如果存在 DOM2 级方法，则使用该方法：传入事件类型、事件处理程序函数和第三个参数 false（表示冒泡阶段）。如果存在的是 IE 的方法，则采取第二种方案。注意，为了在 IE8 及更早版本中运行，此时的事件类型必须加上"on"前缀。最后一种可能就是使用 DOM0 级方法（在现代浏览器中，应该不会执行这里的代码）。此时，我们使用的是方括号语法来将属性名指定为事件处理程序，或者将属性设置为 null。

可以像下面这样使用 EventUtil 对象：

```js
var btn = document.getElementById("myBtn");
var handler = function(){
  alert("Clicked");
};
EventUtil.addHandler(btn, "click", handler);
//这里省略了其他代码
EventUtil.removeHandler(btn, "click", handler);
```

`addHandler()`和 `removeHandler()`没有考虑到所有的浏览器问题，例如在 IE 中的作用域问题。不过，使用它们添加和移除事件处理程序还是足够了。此外还要注意， DOM0 级对每个事件只支持一个事件处理程序。好在，只支持 DOM0 级的浏览器已经没有那么多了，因此这对你而言应该不是什么问题。:

## 13.3 事件对象 

在触发 DOM 上的某个事件时，会产生一个事件对象 event，这个对象中包含着所有与事件有关的信息。包括导致事件的元素、事件的类型以及其他与特定事件相关的信息。例如，鼠标操作导致的事件对象中，会包含鼠标位置的信息，而键盘操作导致的事件对象中，会包含与按下的键有关的信息。所有浏览器都支持 event 对象，但支持方式不同。

### 13.3.1 DOM中的事件对象

兼容 DOM 的浏览器会将一个 event 对象传入到事件处理程序中。无论指定事件处理程序时使用什么方法（ DOM0 级或 DOM2 级），都会传入 event 对象。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
  alert(event.type); //"click"
};
btn.addEventListener("click", function(event){
  alert(event.type); //"click"
}, false);
```

这个例子中的两个事件处理程序都会弹出一个警告框，显示由 `event.type` 属性表示的事件类型。这个属性始终都会包含被触发的事件类型，例如 "click" （与传入 `ddEventListener()` 和`removeEventListener()`中的事件类型一致）。

在通过 HTML 特性指定事件处理程序时，变量 event 中保存着 event 对象。请看下面的例子。

```js
<input type="button" value="Click Me" onclick="alert(event.type)"/>
```

以这种方式提供 event 对象，可以让 HTML 特性事件处理程序与 JavaScript 函数执行相同的操作。

event 对象包含与创建它的特定事件有关的属性和方法。触发的事件类型不一样，可用的属性和方法也不一样。不过，所有事件都会有下表列出的成员。

| 属性/方法 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| bubbles | Boolean | 只读 | 表明事件是否冒泡 |
| cancelable | Boolean | 只读 | 表明是否可以取消事件的默认行为 |
| currentTarget | Element | 只读 | 其事件处理程序当前正在处理事件的那个元素 |
| defaultPrevented | Boolean | 只读 | 为 true 表示已经调用了 preventDefault( ) （DOM3 新增） |
| detail | Integer | 只读 | 与事件相关的细节信息 |
| eventPhase | Integer | 只读 | 调用事件处理程序的阶段：1 表示捕获阶段，2 表示“处于目标”，3 表示冒泡阶段 |
| preventDefault( ) | Function | 只读 | 取消事件的默认行为。如果 cancelable 是 true，则可以使用这个方法 |
| stopImmediatePropagation( ) | Function | 只读 | 取消事件的进一步捕获或冒泡，同时阻止任何事件处理程序被调用（DOM3 新增） |
| stopPropagation( ) | Function | 只读 | 取消事件的进一步捕获或冒泡。如果 bubbles 为 true，则可以使用这个方法 |
| target | Element | 只读 | 事件的目标 |
| trusted | Boolean | 只读 | 为 true 表示事件是浏览器生成的。false 表示事件是由开发人员通过 JavaScript 创建的（DOM3 新增） |
| type | String | 只读 | 被触发的事件的类型 |
| view | AbstractView | 只读 | 与事件关联的抽象试图。等同于发生时间的 window 对象 |

在事件处理程序内部，对象 this 始终等于 currentTarget 的值，而 target 则只包含事件的实际目标。如果直接将事件处理程序指定给了目标元素，则 this、 currentTarget 和 target 包含相同的值。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
  alert(event.currentTarget === this); //true
  alert(event.target === this); //true
};
```

这个例子检测了 currentTarget 和 target 与 this 的值。由于 click 事件的目标是按钮，因此这三个值是相等的。如果事件处理程序存在于按钮的父节点中（例如 document.body），那么这些值是不相同的。再看下面的例子。

```js
document.body.onclick = function(event){
  alert(event.currentTarget === document.body); //true
  alert(this === document.body); //true
  alert(event.target === document.getElementById("myBtn")); //true
};
```

当单击这个例子中的按钮时， this 和 currentTarget 都等于 `document.body`，因为事件处理程序是注册到这个元素上的。然而， target 元素却等于按钮元素，因为它是 click 事件真正的目标。由于按钮上并没有注册事件处理程序，结果 click 事件就冒泡到了 `document.body`，在那里事件才得到了处理。

在需要通过一个函数处理多个事件时，可以使用 type 属性。例如：

```js
var btn = document.getElementById("myBtn");
var handler = function(event){
  switch(event.type){
    case "click":
      alert("Clicked");
    break;
      case "mouseover":
      event.target.style.backgroundColor = "red";
      break;
    case "mouseout":
      event.target.style.backgroundColor = "";
      break;
  }
};
btn.onclick = handler;
btn.onmouseover = handler;
btn.onmouseout = handler;
```

这个例子定义了一个名为 handler 的函数，用于处理 3 种事件： click、 mouseover 和 mouseout。当单击按钮时，会出现一个与前面例子中一样的警告框。当按钮移动到按钮上面时，背景颜色应该会变成红色，而当鼠标移动出按钮的范围时，背景颜色应该会恢复为默认值。这里通过检测 event.type 属性，让函数能够确定发生了什么事件，并执行相应的操作。

要阻止特定事件的默认行为，可以使用 `preventDefault()`方法。例如，链接的默认行为就是在被单击时会导航到其 href 特性指定的 URL。如果你想阻止链接导航这一默认行为，那么通过链接的onclick 事件处理程序可以取消它，如下面的例子所示。

```js
var link = document.getElementById("myLink");
link.onclick = function(event){
  event.preventDefault();
};
```

只有 cancelable 属性设置为 true 的事件，才可以使用 preventDefault()来取消其默认行为。

另外， stopPropagation()方法用于立即停止事件在 DOM 层次中的传播，即取消进一步的事件捕获或冒泡。例如，直接添加到一个按钮的事件处理程序可以调用 stopPropagation()，从而避免触发注册在 document.body 上面的事件处理程序，如下面的例子所示。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
  alert("Clicked");
  event.stopPropagation();
};
document.body.onclick = function(event){
  alert("Body clicked");
};
```

对于这个例子而言，如果不调用 stopPropagation()，就会在单击按钮时出现两个警告框。可是，由于 click 事件根本不会传播到 document.body，因此就不会触发注册在这个元素上的 onclick 事件处理程序。

事件对象的 eventPhase 属性，可以用来确定事件当前正位于事件流的哪个阶段。如果是在捕获阶段调用的事件处理程序，那么 eventPhase 等于 1；如果事件处理程序处于目标对象上，则 eventPhase 等于 2；如果是在冒泡阶段调用的事件处理程序， eventPhase 等于 3。这里要注意的是，尽管“处于目标”发生在冒泡阶段，但 eventPhase 仍然一直等于 2。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
  alert(event.eventPhase); //2
};
document.body.addEventListener("click", function(event){
  alert(event.eventPhase); //1
}, true);
document.body.onclick = function(event){
  alert(event.eventPhase); //3
};
```

当单击这个例子中的按钮时，首先执行的事件处理程序是在捕获阶段触发的添加到 document.body 中的那一个，结果会弹出一个警告框显示表示 eventPhase 的 1。接着，会触发在按钮上注册的事件处理程序，此时的 eventPhase 值为 2。最后一个被触发的事件处理程序，是在冒泡阶段执行的添加到document.body 上的那一个，显示 eventPhase 的值为 3。而当 eventPhase 等于 2 时， this、 target 和 currentTarget 始终都是相等的。

> 只有在事件处理程序执行期间， event 对象才会存在；一旦事件处理程序执行完成， event 对象就会被销毁。

### 13.3.2 IE中的事件对象

与访问 DOM 中的 event 对象不同，要访问 IE 中的 event 对象有几种不同的方式，取决于指定事件处理程序的方法。在使用 DOM0 级方法添加事件处理程序时， event 对象作为 window 对象的一个属性存在。来看下面的例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  var event = window.event;
  alert(event.type); //"click"
};
```

在此，我们通过 window.event 取得了 event 对象，并检测了被触发事件的类型（IE 中的 type 属性与 DOM 中的 type 属性是相同的）。可是，如果事件处理程序是使用 `attachEvent()`添加的，那么就会有一个 event 对象作为参数被传入事件处理程序函数中，如下所示。

```js
var btn = document.getElementById("myBtn");
btn.attachEvent("onclick", function(event){
  alert(event.type); //"click"
});
```

在像这样使用 `attachEvent()`的情况下，也可以通过 window 对象来访问 event 对象，就像使用DOM0 级方法时一样。不过为方便起见，同一个对象也会作为参数传递。

如果是通过 HTML 特性指定的事件处理程序，那么还可以通过一个名叫 event 的变量来访问 event 对象（与 DOM 中的事件模型相同）。再看一个例子。

```js
<input type="button" value="Click Me" onclick="alert(event.type)">
```

IE 的 event 对象同样也包含与创建它的事件相关的属性和方法。其中很多属性和方法都有对应的或者相关的 DOM 属性和方法。与 DOM 的 event 对象一样，这些属性和方法也会因为事件类型的不同而不同，但所有事件对象都会包含下表所列的属性和方法。

| 属性/方法 | 类型 | 读/写 | 说明 |
|---|---|---|---|
| cancelBubble | Boolean | 读/写 | 默认值为false，但将其设置为true就可以取消事件冒泡(与DOM中的stopPropagation()方法的作用相同) |
| returnValue | Boolean | 读/写 | 默认值为true，但将其设置为false就可以事件的默认行为(与DOM中的preventDefault()方法的作用相同) |
| srcElement | Element | 只读 | 事件的目标(与DOm中的target属性相同) |
| type | String | 只读 | 被触发的事件的类型 |

因为事件处理程序的作用域是根据指定它的方式来确定的，所以不能认为 this 会始终等于事件目标。故而，最好还是使用 `event.srcElement` 比较保险。例如：

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  alert(window.event.srcElement === this); //true
};
btn.attachEvent("onclick", function(event){
  alert(event.srcElement === this); //false
});
```

在第一个事件处理程序中（使用 DOM0 级方法指定的）， srcElement 属性等于 this，但在第二个事件处理程序中，这两者的值不相同。

如前所述， returnValue 属性相当于 DOM 中的 `preventDefault()`方法，它们的作用都是取消给定事件的默认行为。只要将 returnValue 设置为 false，就可以阻止默认行为。来看下面的例子。

```js
var link = document.getElementById("myLink");
link.onclick = function(){
  window.event.returnValue = false;
};
```

这个例子在 onclick 事件处理程序中使用 returnValue 达到了阻止链接默认行为的目的。与 DOM 不同的是，在此没有办法确定事件是否能被取消。

相应地， cancelBubble 属性与 DOM 中的 `stopPropagation()`方法作用相同，都是用来停止事件冒泡的。由于 IE 不支持事件捕获，因而只能取消事件冒泡；但 `stopPropagatioin()`可以同时取消事件捕获和冒泡。例如：

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  alert("Clicked");
  window.event.cancelBubble = true;
};
document.body.onclick = function(){
  alert("Body clicked");
};
```

通过在 onclick 事件处理程序中将 cancelBubble 设置为 true，就可阻止事件通过冒泡而触发 document.body 中注册的事件处理程序。结果，在单击按钮之后，只会显示一个警告框。

### 13.3.3 跨浏览器的事件对象

虽然 DOM 和 IE 中的 event 对象不同，但基于它们之间的相似性依旧可以拿出跨浏览器的方案来。IE 中 event 对象的全部信息和方法 DOM 对象中都有，只不过实现方式不一样。不过，这种对应关系让实现两种事件模型之间的映射非常容易。可以对前面介绍的 EventUtil 对象加以增强，添加如下方法以求同存异。

```js
var EventUtil = {
  addHandler: function(element, type, handler){
    //省略的代码
  },
  getEvent: function(event){
    return event ? event : window.event;
  },
  getTarget: function(event){
    return event.target || event.srcElement;
  },
  preventDefault: function(event){
    if (event.preventDefault){
      event.preventDefault();
    } else {
      event.returnValue = false;
    }
  },
  removeHandler: function(element, type, handler){
    //省略的代码
  },
  stopPropagation: function(event){
    if (event.stopPropagation){
      event.stopPropagation();
    } else {
      event.cancelBubble = true;
    }
  }
};
```

以上代码显示，我们为 EventUtil 添加了 4 个新方法。第一个是 `getEvent()`，它返回对 event 对象的引用。考虑到 IE 中事件对象的位置不同，可以使用这个方法来取得 event 对象，而不必担心指定事件处理程序的方式。在使用这个方法时，必须假设有一个事件对象传入到事件处理程序中，而且要把该变量传给这个方法，如下所示。

```js
btn.onclick = function(event){
  event = EventUtil.getEvent(event);
};
```

在兼容 DOM 的浏览器中， event 变量只是简单地传入和返回。而在 IE 中， event 参数是未定义的（undefined），因此就会返回 window.event。将这一行代码添加到事件处理程序的开头，就可以确保随时都能使用 event 对象，而不必担心用户使用的是什么浏览器。

第二个方法是 `getTarget()`，它返回事件的目标。在这个方法内部，会检测 event 对象的 target 属性，如果存在则返回该属性的值；否则，返回 srcElement 属性的值。可以像下面这样使用这个方法。

```js
btn.onclick = function(event){
  event = EventUtil.getEvent(event);
  var target = EventUtil.getTarget(event);
};
```

第三个方法是 `preventDefault()`，用于取消事件的默认行为。在传入 event 对象后，这个方法
会检查是否存在 `preventDefault()`方法，如果存在则调用该方法。如果 `preventDefault()`方法不
存在，则将 returnValue 设置为 false。下面是使用这个方法的例子。

```js
var link = document.getElementById("myLink");
link.onclick = function(event){
  event = EventUtil.getEvent(event);
  EventUtil.preventDefault(event);
};
```

以上代码可以确保在所有浏览器中单击该链接都不会打开另一个页面。首先，使用 `EventUtil.getEvent()`取得 event 对象，然后将其传入到 EventUtil.`preventDefault()`以取消默认行为。

第四个方法是 `stopPropagation()`，其实现方式类似。首先尝试使用 DOM 方法阻止事件流，否则就使用 cancelBubble 属性。下面看一个例子。

```js
var btn = document.getElementById("myBtn");
btn.onclick = function(event){
alert("Clicked");
event = EventUtil.getEvent(event);
EventUtil.stopPropagation(event);
};
document.body.onclick = function(event){
alert("Body clicked");
};
```

在此，首先使用 EventUtil.`getEvent()`取得了 event 对象，然后又将其传入到 `EventUtil.stopPropagation()`。别忘了由于 IE 不支持事件捕获，因此这个方法在跨浏览器的情况下，也只能用来阻止事件冒泡。

## 13.4 事件类型

Web 浏览器中可能发生的事件有很多类型。如前所述，不同的事件类型具有不同的信息，而“DOM3级事件”规定了以下几类事件。

- UI（User Interface，用户界面）事件，当用户与页面上的元素交互时触发；
- 焦点事件，当元素获得或失去焦点时触发；
- 鼠标事件，当用户通过鼠标在页面上执行操作时触发；
- 滚轮事件，当使用鼠标滚轮（或类似设备）时触发；
- 文本事件，当在文档中输入文本时触发；
- 键盘事件，当用户通过键盘在页面上执行操作时触发；
- 合成事件，当为 IME（Input Method Editor，输入法编辑器）输入字符时触发；
- 变动（mutation）事件，当底层 DOM 结构发生变化时触发。
- 变动名称事件，当元素或属性名变动时触发。此类事件已经被废弃，没有任何浏览器实现它们，因此本章不做介绍。

除了这几类事件之外， HTML5 也定义了一组事件，而有些浏览器还会在 DOM 和 BOM 中实现其他专有事件。这些专有的事件一般都是根据开发人员需求定制的，没有什么规范，因此不同浏览器的实现有可能不一致。

DOM3 级事件模块在 DOM2 级事件模块基础上重新定义了这些事件，也添加了一些新事件。包括IE9 在内的所有主流浏览器都支持 DOM2 级事件。 IE9 也支持 DOM3 级事件。

### 13.4.1 UI事件

UI 事件指的是那些不一定与用户操作有关的事件。这些事件在 DOM 规范出现之前，都是以这种或那种形式存在的，而在 DOM 规范中保留是为了向后兼容。现有的 UI 事件如下。

- DOMActivate：表示元素已经被用户操作（通过鼠标或键盘）激活。这个事件在 DOM3 级事件中被废弃，但 Firefox 2+ 和 Chrome 支持它。考虑到不同浏览器实现的差异，不建议使用这个事件。
- load：当页面完全加载后在 window 上面触发，当所有框架都加载完毕时在框架集上面触发，当图像加载完毕时在`<img>`元素上面触发，或者当嵌入的内容加载完毕时在`<object>`元素上面触发。
- unload：当页面完全卸载后在 window 上面触发，当所有框架都卸载后在框架集上面触发，或者当嵌入的内容卸载完毕后在`<object>`元素上面触发。
- abort：在用户停止下载过程时，如果嵌入的内容没有加载完，则在`<object>`元素上面触发。
- error：当发生 JavaScript 错误时在 window 上面触发，当无法加载图像时在`<img>`元素上面触发，当无法加载嵌入内容时在`<object>`元素上面触发，或者当有一或多个框架无法加载时在框架集上面触发。第 17 章将继续讨论这个事件。
- select：当用户选择文本框（ `<input>`或`<texterea>`）中的一或多个字符时触发。第 14 章将继续讨论这个事件。
- resize：当窗口或框架的大小变化时在 window 或框架上面触发。
- scroll：当用户滚动带滚动条的元素中的内容时，在该元素上面触发。 `<body>`元素中包含所加载页面的滚动条。

多数这些事件都与 window 对象或表单控件相关。

除了 DOMActivate 之外，其他事件在 DOM2 级事件中都归为 HTML 事件（ DOMActivate 在 DOM2级中仍然属于 UI 事件）。要确定浏览器是否支持 DOM2 级事件规定的 HTML 事件，可以使用如下代码：

```js
var isSupported = document.implementation.hasFeature("HTMLEvents", "2.0");
```

注意，只有根据“DOM2 级事件”实现这些事件的浏览器才会返回 true。而以非标准方式支持这些事件的浏览器则会返回 false。要确定浏览器是否支持“DOM3 级事件”定义的事件，可以使用如下代码：

```js
var isSupported = document.implementation.hasFeature("UIEvent", "3.0");
```

**1. load 事件**

JavaScript 中最常用的一个事件就是 load。当页面完全加载后（包括所有图像、 JavaScript 文件、CSS 文件等外部资源），就会触发 window 上面的 load 事件。有两种定义 onload 事件处理程序的方式。

第一种方式是使用如下所示的 JavaScript 代码：

```js
EventUtil.addHandler(window, "load", function(event){
  alert("Loaded!");
});
```

这是通过 JavaScript 来指定事件处理程序的方式，使用了本章前面定义的跨浏览器的 EventUtil 对象。与添加其他事件一样，这里也给事件处理程序传入了一个 event 对象。这个 event 对象中不包含有关这个事件的任何附加信息，但在兼容 DOM 的浏览器中， event.target 属性的值会被设置为document，而 IE 并不会为这个事件设置 srcElement 属性。

第二种指定 onload 事件处理程序的方式是为`<body>`元素添加一个 onload 特性，如下面的例子所示：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Load Event Example</title>
  </head>
  <body onload="alert('Loaded!')">
  </body>
</html>
```

一般来说，在 window 上面发生的任何事件都可以在`<body>`元素中通过相应的特性来指定，因为在 HTML 中无法访问 window 元素。实际上，这只是为了保证向后兼容的一种权宜之计，但所有浏览器都能很好地支持这种方式。我们建议读者尽可能使用 JavaScript 方式。

> 根据“DOM2 级事件”规范，应该在 document 而非 window 上面触发 load 事件。但是，所有浏览器都在 window 上面实现了该事件，以确保向后兼容。

图像上面也可以触发 load 事件，无论是在 DOM 中的图像元素还是 HTML 中的图像元素。因此，可以在 HTML 中为任何图像指定 onload 事件处理程序，例如：

```js
<img src="smile.gif" onload="alert('Image loaded.')">
```

这样，当例子中的图像加载完毕后就会显示一个警告框。同样的功能也可以使用 JavaScript 来实现，例如：

```js
var image = document.getElementById("myImage");
EventUtil.addHandler(image, "load", function(event){
  event = EventUtil.getEvent(event);
  alert(EventUtil.getTarget(event).src);
});
```

这里，使用 JavaScript 指定了 onload 事件处理程序。同时也传入了 event 对象，尽管它也不包含什么有用的信息。不过，事件的目标是`<img>`元素，因此可以通过 src 属性访问并显示该信息。

在创建新的`<img>`元素时，可以为其指定一个事件处理程序，以便图像加载完毕后给出提示。此时，最重要的是要在指定 src 属性之前先指定事件，如下面的例子所示。

```js
EventUtil.addHandler(window, "load", function(){
  var image = document.createElement("img");
  EventUtil.addHandler(image, "load", function(event){
    event = EventUtil.getEvent(event);
    alert(EventUtil.getTarget(event).src);
  });
  document.body.appendChild(image);
  image.src = "smile.gif";
});
```

在这个例子中，首先为 window 指定了 onload 事件处理程序。原因在于，我们是想向 DOM 中添加一个新元素，所以必须确定页面已经加载完毕——如果在页面加载前操作 document.body 会导致错误。然后，创建了一个新的图像元素，并设置了其 onload 事件处理程序。最后又将这个图像添加到页面中，还设置了它的 src 属性。这里有一点需要格外注意：新图像元素不一定要从添加到文档后才开始下载，只要设置了 src 属性就会开始下载。

同样的功能也可以通过使用 DOM0 级的 Image 对象实现。在 DOM 出现之前，开发人员经常使用Image 对象在客户端预先加载图像。可以像使用`<img>`元素一样使用 Image 对象，只不过无法将其添加到 DOM 树中。下面来看一个例子。

```js
EventUtil.addHandler(window, "load", function(){
  var image = new Image();
  EventUtil.addHandler(image, "load", function(event){
    alert("Image loaded!");
  });
  image.src = "smile.gif";
});
```

在此，我们使用 Image 构造函数创建了一个新图像的实例，然后又为它指定了事件处理程序。有的浏览器将 Image 对象实现为`<img>`元素，但并非所有浏览器都如此，所以最好将它们区别对待。

> 在不属于 DOM 文档的图像（包括未添加到文档的`<img>`元素和 Image 对象）上触发 load 事件时， IE8 及之前版本不会生成 event 对象。 IE9 修复了这个问题。

还有一些元素也以非标准的方式支持 load 事件。在 IE9+、 Firefox、 Opera、 Chrome 和 Safari 3+及更高版本中，`<script>`元素也会触发 load 事件，以便开发人员确定动态加载的 JavaScript 文件是否加载完毕。与图像不同，只有在设置了`<script>`元素的 src 属性并将该元素添加到文档后，才会开始下载 JavaScript 文件。换句话说，对于`<script>`元素而言，指定 src 属性和指定事件处理程序的先后顺序就不重要了。以下代码展示了怎样为`<script>`元素指定事件处理程序。

```js
EventUtil.addHandler(window, "load", function(){
  var script = document.createElement("script");
  EventUtil.addHandler(script, "load", function(event){
    alert("Loaded");
  });
  script.src = "example.js";
  document.body.appendChild(script);
});
```

这个例子使用了跨浏览器的 EventUtil 对象为新创建的`<script>`元素指定了 onload 事件处理程序。此时，大多数浏览器中 event 对象的 target 属性引用的都是`<script>`节点，而在 Firefox 3 之前的版本中，引用的则是 document。 IE8 及更早版本不支持`<script>`元素上的 load 事件。

IE 和 Opera 还支持`<link>`元素上的 load 事件，以便开发人员确定样式表是否加载完毕。例如：

```js
EventUtil.addHandler(window, "load", function(){
  var link = document.createElement("link");
  link.type = "text/css";
  link.rel= "stylesheet";
  EventUtil.addHandler(link, "load", function(event){
    alert("css loaded");
  });
  link.href = "example.css";
  document.getElementsByTagName("head")[0].appendChild(link);
});
```

与`<script>`节点类似，在未指定 href 属性并将`<link>`元素添加到文档之前也不会开始下载样式表。

**2. unload 事件**

与 load 事件对应的是 unload 事件，这个事件在文档被完全卸载后触发。只要用户从一个页面切换到另一个页面，就会发生 unload 事件。而利用这个事件最多的情况是清除引用，以避免内存泄漏。

与 load 事件类似，也有两种指定 onunload 事件处理程序的方式。第一种方式是使用 JavaScript ，如下所示：

```js
EventUtil.addHandler(window, "unload", function(event){
  alert("Unloaded");
});
```

此时生成的 event 对象在兼容 DOM 的浏览器中只包含 target 属性（值为 document）。 IE8 及之前版本则为这个事件对象提供了 srcElement 属性。

指定事件处理程序的第二种方式，也是为`<body>`元素添加一个特性（与 load 事件相似），如下面的例子所示：

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Unload Event Example</title>
  </head>
  <body onunload="alert('Unloaded!')">
  </body>
</html>
```

无论使用哪种方式，都要小心编写 onunload 事件处理程序中的代码。既然 unload 事件是在一切都被卸载之后才触发，那么在页面加载后存在的那些对象，此时就不一定存在了。此时，操作 DOM 节点或者元素的样式就会导致错误。

> 根据“DOM2 级事件”，应该在`<body>`元素而非 window 对象上面触发 unload 事件。不过，所有浏览器都在 window 上实现了 unload 事件，以确保向后兼容。

**3. resize 事件**

当浏览器窗口被调整到一个新的高度或宽度时，就会触发 resize 事件。这个事件在 window（窗口）上面触发，因此可以通过 JavaScript 或者`<body>`元素中的 onresize 特性来指定事件处理程序。如前所述，我们还是推荐使用如下所示的 JavaScript 方式：

```js
EventUtil.addHandler(window, "resize", function(event){
  alert("Resized");
});
```

与其他发生在 window 上的事件类似，在兼容 DOM 的浏览器中，传入事件处理程序中的 event 对象有一个 target 属性，值为 document；而 IE8 及之前版本则未提供任何属性。

关于何时会触发 resize 事件，不同浏览器有不同的机制。 IE、 Safari、 Chrome 和 Opera 会在浏览器窗口变化了 1 像素时就触发 resize 事件，然后随着变化不断重复触发。 Firefox 则只会在用户停止调整窗口大小时才会触发 resize 事件。由于存在这个差别，应该注意不要在这个事件的处理程序中加入大计算量的代码，因为这些代码有可能被频繁执行，从而导致浏览器反应明显变慢。

> 浏览器窗口最小化或最大化时也会触发 resize 事件。

**4. scroll 事件**

虽然 scroll 事件是在 window 对象上发生的，但它实际表示的则是页面中相应元素的变化。在混杂模式下，可以通过`<body>`元素的 scrollLeft 和 scrollTop 来监控到这一变化；而在标准模式下，除 Safari 之外的所有浏览器都会通过`<html>`元素来反映这一变化（ Safari 仍然基于`<body>`跟踪滚动位置），如下面的例子所示：

```js
EventUtil.addHandler(window, "scroll", function(event){
  if (document.compatMode == "CSS1Compat"){
    alert(document.documentElement.scrollTop);
  } else {
    alert(document.body.scrollTop);
  }
});
```

以上代码指定的事件处理程序会输出页面的垂直滚动位置——根据呈现模式不同使用了不同的元素。由于 Safari 3.1 之前的版本不支持`document.compatMode`，因此旧版本的浏览器就会满足第二个条件。

与 resize 事件类似， scroll 事件也会在文档被滚动期间重复被触发，所以有必要尽量保持事件处理程序的代码简单。

### 13.4.2 焦点事件

焦点事件会在页面元素获得或失去焦点时触发。利用这些事件并与`document.hasFocus()`方法及 `document.activeElement` 属性配合，可以知晓用户在页面上的行踪。有以下 6 个焦点事件。

- blur：在元素失去焦点时触发。这个事件不会冒泡；所有浏览器都支持它。
- DOMFocusIn：在元素获得焦点时触发。这个事件与 HTML 事件 focus 等价，但它冒泡。只有Opera 支持这个事件。 DOM3 级事件废弃了 DOMFocusIn，选择了 focusin。
- DOMFocusOut：在元素失去焦点时触发。这个事件是 HTML 事件 blur 的通用版本。只有 Opera 支持这个事件。 DOM3 级事件废弃了 DOMFocusOut，选择了 focusout。
- focus：在元素获得焦点时触发。这个事件不会冒泡；所有浏览器都支持它。
- focusin：在元素获得焦点时触发。这个事件与 HTML 事件 focus 等价，但它冒泡。支持这个事件的浏览器有 IE5.5+、 Safari 5.1+、 Opera 11.5+和 Chrome。
- focusout：在元素失去焦点时触发。这个事件是 HTML 事件 blur 的通用版本。支持这个事件的浏览器有 IE5.5+、 Safari 5.1+、 Opera 11.5+和 Chrome。

这一类事件中最主要的两个是 focus 和 blur，它们都是 JavaScript 早期就得到所有浏览器支持的事件。这些事件的最大问题是它们不冒泡。因此， IE 的 focusin 和 focusout 与 Opera 的 DOMFocusIn和 DOMFocusOut 才会发生重叠。 IE 的方式最后被 DOM3 级事件采纳为标准方式。

当焦点从页面中的一个元素移动到另一个元素，会依次触发下列事件：

1. focusout 在失去焦点的元素上触发；
2. focusin 在获得焦点的元素上触发；
3. blur 在失去焦点的元素上触发；
4. DOMFocusOut 在失去焦点的元素上触发；
5. focus 在获得焦点的元素上触发；
6. DOMFocusIn 在获得焦点的元素上触发。

其中， blur、 DOMFocusOut 和 focusout 的事件目标是失去焦点的元素；而 focus、 DOMFocusIn 和 focusin 的事件目标是获得焦点的元素。

要确定浏览器是否支持这些事件，可以使用如下代码：

```js
var isSupported = document.implementation.hasFeature("FocusEvent", "3.0");
```

> 即使 focus 和 blur 不冒泡，也可以在捕获阶段侦听到它们。 Peter-Paul Koch 就此写过一篇非常棒的[文章](www.quirksmode.org/blog/archives/2008/04/delegating_the.html)。

### 13.4.3 鼠标与滚轮事件

鼠标事件是 Web 开发中最常用的一类事件，毕竟鼠标还是最主要的定位设备。 DOM3 级事件中定义了 9 个鼠标事件，简介如下。

- click：在用户单击主鼠标按钮（一般是左边的按钮）或者按下回车键时触发。这一点对确保易访问性很重要，意味着 onclick 事件处理程序既可以通过键盘也可以通过鼠标执行。
- dblclick：在用户双击主鼠标按钮（一般是左边的按钮）时触发。从技术上说，这个事件并不是 DOM2 级事件规范中规定的，但鉴于它得到了广泛支持，所以 DOM3 级事件将其纳入了标准。
- mousedown：在用户按下了任意鼠标按钮时触发。不能通过键盘触发这个事件。
- mouseenter：在鼠标光标从元素外部首次移动到元素范围之内时触发。这个事件不冒泡，而且在光标移动到后代元素上不会触发。 DOM2 级事件并没有定义这个事件，但 DOM3 级事件将它纳入了规范。 IE、 Firefox 9+和 Opera 支持这个事件。
- mouseleave：在位于元素上方的鼠标光标移动到元素范围之外时触发。这个事件不冒泡，而且在光标移动到后代元素上不会触发。 DOM2 级事件并没有定义这个事件，但 DOM3 级事件将它纳入了规范。 IE、 Firefox 9+和 Opera 支持这个事件。
- mousemove：当鼠标指针在元素内部移动时重复地触发。不能通过键盘触发这个事件。
- mouseout：在鼠标指针位于一个元素上方，然后用户将其移入另一个元素时触发。又移入的另一个元素可能位于前一个元素的外部，也可能是这个元素的子元素。不能通过键盘触发这个事件。
- mouseover：在鼠标指针位于一个元素外部，然后用户将其首次移入另一个元素边界之内时触发。不能通过键盘触发这个事件。
- mouseup：在用户释放鼠标按钮时触发。不能通过键盘触发这个事件。

页面上的所有元素都支持鼠标事件。除了 mouseenter 和 mouseleave，所有鼠标事件都会冒泡，也可以被取消，而取消鼠标事件将会影响浏览器的默认行为。取消鼠标事件的默认行为还会影响其他事件，因为鼠标事件与其他事件是密不可分的关系。

只有在同一个元素上相继触发 mousedown 和 mouseup 事件，才会触发 click 事件；如果mousedown 或 mouseup 中的一个被取消，就不会触发 click 事件。类似地，只有触发两次 click 事件， 才会触发一次 dblclick 事件。如果有代码阻止了连续两次触发 click 事件（可能是直接取消 click事件，也可能通过取消 mousedown 或 mouseup 间接实现），那么就不会触发 dblclick 事件了。这 4个事件触发的顺序始终如下：

1. mousedown
2. mouseup
3. click
4. mousedown
5. mouseup
6. click
7. dblclick

显然， click 和 dblclick 事件都会依赖于其他先行事件的触发；而 mousedown 和 mouseup 则不受其他事件的影响。

IE8 及之前版本中的实现有一个小 bug，因此在双击事件中，会跳过第二个 mousedown 和 click事件，其顺序如下：

1. mousedown
2. mouseup
3. click
4. mouseup
5. dblclick

IE9 修复了这个 bug，之后顺序就正确了。

使用以下代码可以检测浏览器是否支持以上 DOM2 级事件（除 dbclick、 mouseenter 和 mouseleave 之外）：

```js
var isSupported = document.implementation.hasFeature("MouseEvents", "2.0");
```

要检测浏览器是否支持上面的所有事件，可以使用以下代码：

```js
var isSupported = document.implementation.hasFeature("MouseEvent", "3.0")
```

注意， DOM3 级事件的 feature 名是"MouseEvent"，而非"MouseEvents"。

鼠标事件中还有一类滚轮事件。而说是一类事件，其实就是一个 mousewheel 事件。这个事件跟踪鼠标滚轮，类似于 Mac 的触控板。

**1. 客户区坐标位置**

鼠标事件都是在浏览器视口中的特定位置上发生的。这个位置信息保存在事件对象的 clientX 和clientY 属性中。所有浏览器都支持这两个属性，它们的值表示事件发生时鼠标指针在视口中的水平和垂直坐标。图 13-4 展示了视口中客户区坐标位置的含义。

可以使用类似下列代码取得鼠标事件的客户端坐标信息：

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
  event = EventUtil.getEvent(event);
  alert("Client coordinates: " + event.clientX + "," + event.clientY);
});
```

这里为一个`<div>`元素指定了 onclick 事件处理程序。当用户单击这个元素时，就会看到事件的客户端坐标信息。注意，这些值中不包括页面滚动的距离，因此这个位置并不表示鼠标在页面上的位置。

**2. 页面坐标位置**

通过客户区坐标能够知道鼠标是在视口中什么位置发生的，而页面坐标通过事件对象的 pageX 和 pageY 属性，能告诉你事件是在页面中的什么位置发生的。换句话说，这两个属性表示鼠标光标在页面中的位置，因此坐标是从页面本身而非视口的左边和顶边计算的。

以下代码可以取得鼠标事件在页面中的坐标：

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
  event = EventUtil.getEvent(event);
  alert("Page coordinates: " + event.pageX + "," + event.pageY);
});
```

在页面没有滚动的情况下， pageX 和 pageY 的值与 clientX 和 clientY 的值相等。

IE8 及更早版本不支持事件对象上的页面坐标，不过使用客户区坐标和滚动信息可以计算出来。这时候需要用到 `document.body`（混杂模式）或 `document.documentElement`（标准模式）中的 scrollLeft 和 scrollTop 属性。计算过程如下所示：

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
  event = EventUtil.getEvent(event);
  var pageX = event.pageX,
  pageY = event.pageY;
  if (pageX === undefined){
    pageX = event.clientX + (document.body.scrollLeft ||
    document.documentElement.scrollLeft);
  }
  if (pageY === undefined){
    pageY = event.clientY + (document.body.scrollTop ||
    document.documentElement.scrollTop);
  }
  alert("Page coordinates: " + pageX + "," + pageY);
});
```

**3. 屏幕坐标位置**

鼠标事件发生时，不仅会有相对于浏览器窗口的位置，还有一个相对于整个电脑屏幕的位置。而通过 screenX 和 screenY 属性就可以确定鼠标事件发生时鼠标指针相对于整个屏幕的坐标信息。图 13-5展示了浏览器中屏幕坐标的含义。

可以使用类似下面的代码取得鼠标事件的屏幕坐标：

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
  event = EventUtil.getEvent(event);
  alert("Screen coordinates: " + event.screenX + "," + event.screenY);
});
```

与前一个例子类似，这里也是为`<div>`元素指定了一个 onclick 事件处理程序。当这个元素被单击时，就会显示出事件的屏幕坐标信息了。

**4. 修改键**

虽然鼠标事件主要是使用鼠标来触发的，但在按下鼠标时键盘上的某些键的状态也可以影响到所要采取的操作。这些修改键就是 Shift、 Ctrl、 Alt 和 Meta（在 Windows 键盘中是 Windows 键，在苹果机中是 Cmd 键），它们经常被用来修改鼠标事件的行为。 DOM 为此规定了 4 个属性，表示这些修改键的状态： shiftKey、 ctrlKey、 altKey 和 metaKey。这些属性中包含的都是布尔值，如果相应的键被按下了，则值为 true，否则值为 false。当某个鼠标事件发生时，通过检测这几个属性就可以确定用户是否同时按下了其中的键。来看下面的例子。

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "click", function(event){
  event = EventUtil.getEvent(event);
  var keys = new Array();
  if (event.shiftKey){
    keys.push("shift");
  }
  if (event.ctrlKey){
    keys.push("ctrl");
  }
  if (event.altKey){
    keys.push("alt");
  }
  if (event.metaKey){
    keys.push("meta");
  }
  alert("Keys: " + keys.join(","));
});
```

在这个例子中，我们通过一个 onclick 事件处理程序检测了不同修改键的状态。数组 keys 中包含着被按下的修改键的名称。换句话说，如果有属性值为 true，就会将对应修改键的名称添加到 keys数组中。在事件处理程序的最后，有一个警告框将检测到的键的信息显示给用户。

> IE9、 Firefox、 Safari、 Chrome 和 Opera 都支持这 4 个键。 IE8 及之前版本不支持 metaKey 属性。

**5. 相关元素**

在发生 mouseover 和 mouserout 事件时，还会涉及更多的元素。这两个事件都会涉及把鼠标指针从一个元素的边界之内移动到另一个元素的边界之内。对 mouseover 事件而言，事件的主目标是获得光标的元素，而相关元素就是那个失去光标的元素。类似地，对 mouseout 事件而言，事件的主目标是失去光标的元素，而相关元素则是获得光标的元素。来看下面的例子。

```html
<!DOCTYPE html>
<html>
<head>
  <title>Related Elements Example</title>
</head>
<body>
  <div id="myDiv" style="background-color:red;height:100px;width:100px;"></div>
</body>
</html>
```

这个例子会在页面上显示一个`<div>`元素。如果鼠标指针一开始位于这个`<div>`元素上，然后移出了这个元素，那么就会在`<div>`元素上触发 mouseout 事件，相关元素就是`<body>`元素。与此同时，`<body>`元素上面会触发 mouseover 事件，而相关元素变成了`<div>`。

DOM 通过 event 对象的 relatedTarget 属性提供了相关元素的信息。这个属性只对于 mouseover和 mouseout 事件才包含值；对于其他事件，这个属性的值是 null。IE8及之前版本不支持 relatedTarget属性，但提供了保存着同样信息的不同属性。在 mouseover 事件触发时， IE 的 fromElement 属性中保存了相关元素；在 mouseout 事件触发时， IE 的 toElement 属性中保存着相关元素。（ IE9 支持所有这些属性。）可以把下面这个跨浏览器取得相关元素的方法添加到 EventUtil 对象中。

```js
var EventUtil = {
//省略了其他代码
  getRelatedTarget: function(event){
    if (event.relatedTarget){
      return event.relatedTarget;
    } else if (event.toElement){
      return event.toElement;
    } else if (event.fromElement){
      return event.fromElement;
    } else {
      return null;
    }
  },
  //省略了其他代码
};
```

与以前添加的跨浏览器方法一样，这个方法也使用了特性检测来确定返回哪个值。可以像下面这样

使用 `EventUtil.getRelatedTarget()`方法：

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "mouseout", function(event){
  event = EventUtil.getEvent(event);
  var target = EventUtil.getTarget(event);
  var relatedTarget = EventUtil.getRelatedTarget(event);
  alert("Moused out of " + target.tagName + " to " + relatedTarget.tagName);
});
```

这个例子为`<div>`元素的 mouseout 事件注册了一个事件处理程序。当事件触发时，会有一个警告框显示鼠标移出和移入的元素信息。

**6. 鼠标按钮**

只有在主鼠标按钮被单击（或键盘回车键被按下）时才会触发 click 事件，因此检测按钮的信息并不是必要的。但对于 mousedown 和 mouseup 事件来说，则在其 event 对象存在一个 button 属性，表示按下或释放的按钮。 DOM 的 button 属性可能有如下 3 个值： 0 表示主鼠标按钮， 1 表示中间的鼠标按钮（鼠标滚轮按钮）， 2 表示次鼠标按钮。在常规的设置中，主鼠标按钮就是鼠标左键，而次鼠标按钮就是鼠标右键。

IE8 及之前版本也提供了 button 属性，但这个属性的值与 DOM 的 button 属性有很大差异。

- 0：表示没有按下按钮。
- 1：表示按下了主鼠标按钮。
- 2：表示按下了次鼠标按钮。
- 3：表示同时按下了主、次鼠标按钮。
- 4：表示按下了中间的鼠标按钮。
- 5：表示同时按下了主鼠标按钮和中间的鼠标按钮。
- 6：表示同时按下了次鼠标按钮和中间的鼠标按钮。
- 7：表示同时按下了三个鼠标按钮。

不难想见， DOM 模型下的 button 属性比 IE 模型下的 button 属性更简单也更为实用，因为同时按下多个鼠标按钮的情形十分罕见。最常见的做法就是将 IE 模型规范化为 DOM 方式，毕竟除 IE8 及更早版本之外的其他浏览器都原生支持 DOM 模型。而对主、中、次按钮的映射并不困难，只要将 IE 的其他选项分别转换成如同按下这三个按键中的一个即可（同时将主按钮作为优先选取的对象）。换句话说，IE 中返回的 5 和 7 会被转换成 DOM 模型中的 0。

由于单独使用能力检测无法确定差异（两种模型有同名的 button 属性），因此必须另辟蹊径。我们知道，支持 DOM 版鼠标事件的浏览器可以通过 `hasFearture()`方法来检测，所以可以再为 EventUtil 对象添加如下 `getButton()`方法。

```js
var EventUtil = {
  //省略了其他代码
  getButton: function(event){
    if (document.implementation.hasFeature("MouseEvents", "2.0")){
      return event.button;
    } else {
      switch(event.button){
        case 0:
        case 1:
        case 3:
        case 5:
        case 7:
          return 0;
        case 2:
        case 6:
          return 2;
        case 4:
          return 1;
      }
    }
  },
  //省略了其他代码
};
```

通过检测"MouseEvents"这个特性，就可以确定 event 对象中存在的 button 属性中是否包含正确的值。如果测试失败，说明是 IE，就必须对相应的值进行规范化。以下是使用该方法的示例。

```js
var div = document.getElementById("myDiv");
EventUtil.addHandler(div, "mousedown", function(event){
  event = EventUtil.getEvent(event);
  alert(EventUtil.getButton(event));
});
```

在这个例子中，我们为一个`<div>`元素添加了一个 onmousedown 事件处理程序。当在这个元素上按下鼠标按钮时，会有警告框显示按钮的代码。

> 在使用 onmouseup 事件处理程序时， button 的值表示释放的是哪个按钮。此外，如果不是按下或释放了主鼠标按钮， Opera 不会触发 mouseup 或 mousedown事件。

**7. 更多的事件信息**

“DOM2 级事件”规范在 event 对象中还提供了 detail 属性，用于给出有关事件的更多信息。对于鼠标事件来说， detail 中包含了一个数值，表示在给定位置上发生了多少次单击。在同一个元素上相继地发生一次 mousedown 和一次 mouseup 事件算作一次单击。 detail 属性从 1 开始计数，每次单击发生后都会递增。如果鼠标在 mousedown 和 mouseup 之间移动了位置，则 detail 会被重置为 0。

IE 也通过下列属性为鼠标事件提供了更多信息。

- altLeft： 布尔值，表示是否按下了 Alt 键。 如果 altLeft 的值为 true，则 altKey 的值也为 true。
- ctrlLeft：布尔值，表示是否按下了 Ctrl 键。如果 ctrlLeft 的值为 true，则 ctrlKey 的值也为 true。
- offsetX：光标相对于目标元素边界的 x 坐标。
- offsetY：光标相对于目标元素边界的 y 坐标。
- shiftLeft：布尔值，表示是否按下了 Shift 键。如果 shiftLeft 的值为 true，则 shiftKey 的值也为 true。

这些属性的用处并不大，原因一方面是只有 IE 支持它们，另一方是它们提供的信息要么没有什么价值，要么可以通过其他方式计算得来。

**8. 鼠标滚轮事件**

IE 6.0 首先实现了 mousewheel 事件。此后， Opera、 Chrome 和 Safari 也都实现了这个事件。当用户通过鼠标滚轮与页面交互、在垂直方向上滚动页面时（无论向上还是向下），就会触发 mousewheel事件。这个事件可以在任何元素上面触发，最终会冒泡到 document（ IE8）或 window（ IE9、 Opera、Chrome 及 Safari）对象。与 mousewheel 事件对应的 event 对象除包含鼠标事件的所有标准信息外，还包含一个特殊的 wheelDelta 属性。当用户向前滚动鼠标滚轮时， wheelDelta 是 120 的倍数；当用户向后滚动鼠标滚轮时， wheelDelta 是 120 的倍数。图 13-6 展示了这个属性。

将 mousewheel 事件处理程序指定给页面中的任何元素或 document 对象，即可处理鼠标滚轮的交互操作。来看下面的例子。

```js
EventUtil.addHandler(document, "mousewheel", function(event){
  event = EventUtil.getEvent(event);
  alert(event.wheelDelta);
});
```

这个例子会在发生 mousewheel 事件时显示 wheelDelta 的值。多数情况下，只要知道鼠标滚轮滚动的方向就够了，而这通过检测 wheelDelta 的正负号就可以确定。

有一点要注意：在 Opera 9.5 之前的版本中， wheelDelta 值的正负号是颠倒的。如果你打算支持早期的 Opera 版本，就需要使用浏览器检测技术来确定实际的值，如下面的例子所示。

```js
EventUtil.addHandler(document, "mousewheel", function(event){
  event = EventUtil.getEvent(event);
  var delta = (client.engine.opera && client.engine.opera < 9.5 ?
    -event.wheelDelta : event.wheelDelta);
  alert(delta);
});
```

> 以上代码使用第 9 章创建的 client 对象检测了浏览器是不是早期版本的 Opera。由于 mousewheel 事件非常流行，而且所有浏览器都支持它，所以 HTML 5 也加入了该事件。

Firefox 支持一个名为 DOMMouseScroll 的类似事件，也是在鼠标滚轮滚动时触发。与 mousewheel事件一样， DOMMouseScroll 也被视为鼠标事件，因而包含与鼠标事件有关的所有属性。而有关鼠标滚轮的信息则保存在 detail 属性中，当向前滚动鼠标滚轮时，这个属性的值是-3 的倍数，当向后滚动鼠标滚轮时，这个属性的值是 3 的倍数。图 13-7 展示了这个属性。

可以将 DOMMouseScroll 事件添加到页面中的任何元素，而且该事件会冒泡到 window 对象。因此，可以像下面这样针对这个事件来添加事件处理程序。

```js
EventUtil.addHandler(window, "DOMMouseScroll", function(event){
  event = EventUtil.getEvent(event);
  alert(event.detail);
});
```

这个简单的事件处理程序会在鼠标滚轮滚动时显示 detail 属性的值。

若要给出跨浏览器环境下的解决方案，第一步就是创建一个能够取得鼠标滚轮增量值（ delta）的方法。下面是我们添加到 EventUtil 对象中的这个方法。

```js
var EventUtil = {
  //省略了其他代码
  getWheelDelta: function(event){
    if (event.wheelDelta){
      return (client.engine.opera && client.engine.opera < 9.5 ?
      -event.wheelDelta : event.wheelDelta);
    } else {
      return -event.detail * 40;
    }
  },
  //省略了其他代码
};
```

这里， `getWheelDelta()`方法首先检测了事件对象是否包含 wheelDelta 属性，如果是则通过浏览器检测代码确定正确的值。如果 wheelDelta 不存在，则假设相应的值保存在 detail 属性中。由于Firefox 的值有所不同，因此首先要将这个值的符号反向，然后再乘以 40，就可以保证与其他浏览器的值相同了。有了这个方法之后，就可以将相同的事件处理程序指定给 mousewheel 和 DOMMouseScroll 事件了，例如：

```js
(function(){
  function handleMouseWheel(event){
    event = EventUtil.getEvent(event);
    var delta = EventUtil.getWheelDelta(event);
    alert(delta);
  }
  EventUtil.addHandler(document, "mousewheel", handleMouseWheel);
  EventUtil.addHandler(document, "DOMMouseScroll", handleMouseWheel);
})();
```

我们将相关代码放在了一个私有作用域中，从而不会让新定义的函数干扰全局作用域。这里定义的`handleMouseWheel()`函数可以用作两个事件的处理程序（如果指定的事件不存在，则为该事件指定处理程序的代码就会静默地失败）。由于使用了 `EventUtil.getWheelDelta()`方法，我们定义的这个事件处理程序函数可以适用于任何一种情况。

**9. 触摸设备**

iOS 和 Android 设备的实现非常特别，因为这些设备没有鼠标。在面向 iPhone 和 iPod 中的 Safari开发时，要记住以下几点。

- 不支持 dblclick 事件。双击浏览器窗口会放大画面，而且没有办法改变该行为。
- 轻击可单击元素会触发 mousemove 事件。如果此操作会导致内容变化，将不再有其他事件发生；如果屏幕没有因此变化，那么会依次发生 mousedown、 mouseup 和 click 事件。轻击不可单击的元素不会触发任何事件。可单击的元素是指那些单击可产生默认操作的元素（如链接），或者那些已经被指定了 onclick 事件处理程序的元素。
- mousemove 事件也会触发 mouseover 和 mouseout 事件。
- 两个手指放在屏幕上且页面随手指移动而滚动时会触发 mousewheel 和 scroll 事件。

**10. 无障碍性问题**

如果你的 Web 应用程序或网站要确保残疾人特别是那些使用屏幕阅读器的人都能访问，那么在使用鼠标事件时就要格外小心。前面提到过，可以通过键盘上的回车键来触发 click 事件，但其他鼠标事件却无法通过键盘来触发。为此，我们不建议使用 click 之外的其他鼠标事件来展示功能或引发代码执行。因为这样会给盲人或视障用户造成极大不便。以下是在使用鼠标事件时应当注意的几个易访问性问题。

- 使用 click 事件执行代码。有人指出通过 onmousedown 执行代码会让人觉得速度更快，对视力正常的人来说这是没错的。但是，在屏幕阅读器中，由于无法触发 mousedown 事件，结果就会造成代码无法执行。
- 不要使用 onmouseover 向用户显示新的选项。原因同上，屏幕阅读器无法触发这个事件。如果确实非要通过这种方式来显示新选项，可以考虑添加显示相同信息的键盘快捷方式。
- 不要使用 dblclick 执行重要的操作。键盘无法触发这个事件。

遵照以上提示可以极大地提升残疾人在访问你的 Web 应用程序或网站时的易访问性。

> 要了解如何在网页中实现无障碍访问的内容，请访问 www.webaim.org 和http://yaccessibilityblog.com/。

### 13.4.4 键盘与文本事件

用户在使用键盘时会触发键盘事件。“DOM2 级事件”最初规定了键盘事件，但在最终定稿之前又删除了相应的内容。结果，对键盘事件的支持主要遵循的是 DOM0 级。

“DOM3 级事件”为键盘事件制定了规范， IE9 率先完全实现了该规范。其他浏览器也在着手实现这一标准，但仍然有很多遗留的问题。

有 3 个键盘事件，简述如下。

- keydown：当用户按下键盘上的任意键时触发，而且如果按住不放的话，会重复触发此事件。
- keypress：当用户按下键盘上的字符键时触发，而且如果按住不放的话，会重复触发此事件。按下 Esc 键也会触发这个事件。 Safari 3.1 之前的版本也会在用户按下非字符键时触发 keypress事件。
- keyup：当用户释放键盘上的键时触发。

虽然所有元素都支持以上 3 个事件，但只有在用户通过文本框输入文本时才最常用到。只有一个文本事件： textInput。这个事件是对 keypress 的补充，用意是在将文本显示给用户之前更容易拦截文本。在文本插入文本框之前会触发 textInput 事件。

在用户按了一下键盘上的字符键时，首先会触发 keydown 事件，然后紧跟着是 keypress 事件，最后会触发 keyup 事件。 其中， keydown 和 keypress 都是在文本框发生变化之前被触发的；而 keyup事件则是在文本框已经发生变化之后被触发的。如果用户按下了一个字符键不放，就会重复触发keydown 和 keypress 事件，直到用户松开该键为止。

如果用户按下的是一个非字符键，那么首先会触发 keydown 事件，然后就是 keyup 事件。如果按住这个非字符键不放，那么就会一直重复触发 keydown 事件，直到用户松开这个键，此时会触发 keyup事件。

> 键盘事件与鼠标事件一样，都支持相同的修改键。而且，键盘事件的事件对象中也有 shiftKey、 ctrlKey、 altKey 和 metaKey 属性。 IE 不支持 metaKey。

**1. 键码**

在发生 keydown 和 keyup 事件时， event 对象的 keyCode 属性中会包含一个代码，与键盘上一个特定的键对应。对数字字母字符键， keyCode 属性的值与 ASCII 码中对应小写字母或数字的编码相同。因此，数字键 7 的 keyCode 值为 55，而字母 A 键的 keyCode 值为 65——与 Shift 键的状态无关。DOM 和 IE 的 event 对象都支持 keyCode 属性。请看下面这个例子：

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keyup", function(event){
  event = EventUtil.getEvent(event);
  alert(event.keyCode);
});
```

在这个例子中，用户每次在文本框中按键触发 keyup 事件时，都会显示 keyCode 的值。下表列出了所有非字符键的键码。


无论 keydown 或 keyup 事件都会存在的一些特殊情况。在 Firefox 和 Opera 中， 按分号键时 keyCode值为 59，也就是 ASCII 中分号的编码；但 IE 和 Safari 返回 186，即键盘中按键的键码。

**2. 字符编码**

发生 keypress 事件意味着按下的键会影响到屏幕中文本的显示。在所有浏览器中，按下能够插入或删除字符的键都会触发 keypress 事件；按下其他键能否触发此事件因浏览器而异。由于截止到 2008年，尚无浏览器实现“DOM3 级事件”规范，所以浏览器之间的键盘事件并没有多大的差异。

IE9、 Firefox、 Chrome 和 Safari 的 event 对象都支持一个 charCode 属性，这个属性只有在发生 keypress 事件时才包含值，而且这个值是按下的那个键所代表字符的 ASCII 编码。此时的 keyCode通常等于 0 或者也可能等于所按键的键码。IE8 及之前版本和 Opera 则是在 keyCode 中保存字符的 ASCII编码。要想以跨浏览器的方式取得字符编码，必须首先检测 charCode 属性是否可用，如果不可用则使用 keyCode，如下面的例子所示。

```js
var EventUtil = {
  //省略的代码
  getCharCode: function(event){
    if (typeof event.charCode == "number"){
      return event.charCode;
    } else {
      return event.keyCode;
    }
  },
  //省略的代码
};
```

这个方法首先检测 charCode 属性是否包含数值（在不支持这个属性的浏览器中，值为 undefined），如果是，则返回该值。否则，就返回 keyCode 属性值。下面是使用这个方法的示例。

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keypress", function(event){
  event = EventUtil.getEvent(event);
  alert(EventUtil.getCharCode(event));
});
```

在取得了字符编码之后，就可以使用 `String.fromCharCode()`将其转换成实际的字符。

**3. DOM3 级变化**

尽管所有浏览器都实现了某种形式的键盘事件， DOM3 级事件还是做出了一些改变。比如， DOM3级事件中的键盘事件，不再包含 charCode 属性，而是包含两个新属性： key 和 char。

其中， key 属性是为了取代 keyCode 而新增的，它的值是一个字符串。在按下某个字符键时， key的值就是相应的文本字符（如“k”或“M”）；在按下非字符键时， key 的值是相应键的名（如“Shift”或“Down”）。而 char 属性在按下字符键时的行为与 key 相同，但在按下非字符键时值为 null。

IE9 支持 key 属性，但不支持 char 属性。 Safari 5 和 Chrome 支持名为 keyIdentifier 的属性，在按下非字符键（例如 Shift）的情况下与 key 的值相同。对于字符键， keyIdentifier 返回一个格式类似“U+0000”的字符串，表示 Unicode 值。

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keypress", function(event){
  event = EventUtil.getEvent(event);
  var identifier = event.key || event.keyIdentifier;
  if (identifier){
    alert(identifi er);
  }
});
```

由于存在跨浏览器问题，因此本书不推荐使用 key、 keyIdentifier 或 char。

DOM3 级事件还添加了一个名为 location 的属性，这是一个数值，表示按下了什么位置上的键：0 表示默认键盘， 1 表示左侧位置（例如左位的 Alt 键）， 2 表示右侧位置（例如右侧的 Shift 键）， 3 表示数字小键盘， 4 表示移动设备键盘（也就是虚拟键盘）， 5 表示手柄（如任天堂 Wii 控制器）。 IE9 支持这个属性。 Safari 和 Chrome 支持名为 keyLocation 的等价属性，但即有 bug——值始终是 0，除非按下了数字键盘（此时，值 为 3）；否则，不会是 1、 2、 4、 5。

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keypress", function(event){
  event = EventUtil.getEvent(event);
  var loc = event.location || event.keyLocation;
  if (loc){
    alert(loc);
  }
});
```

与 key 属性一样，支持 location 的浏览器也不多，所以在跨浏览器开发中不推荐使用。

最后是给 event 对象添加了 `getModifierState()`方法。这个方法接收一个参数，即等于 Shift、Control、 AltGraph 或 Meta 的字符串，表示要检测的修改键。如果指定的修改键是活动的（也就是处于被按下的状态），这个方法返回 true，否则返回 false。

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "keypress", function(event){
  event = EventUtil.getEvent(event);
  if (event.getModifierState){
    alert(event.getModifierState("Shift"));
  }
});
```

实际上，通过 event 对象的 shiftKey、 altKey、 ctrlKey 和 metaKey 属性已经可以取得类似的属性了。 IE9 是唯一支持 `getModifierState()`方法的浏览器。

**4. textInput 事件**

“DOM3 级事件”规范中引入了一个新事件，名叫 textInput。根据规范，当用户在可编辑区域中输入字符时，就会触发这个事件。这个用于替代 keypress 的 textInput 事件的行为稍有不同。区别之一就是任何可以获得焦点的元素都可以触发 keypress 事件，但只有可编辑区域才能触发 textInput事件。区别之二是 textInput 事件只会在用户按下能够输入实际字符的键时才会被触发，而 keypress事件则在按下那些能够影响文本显示的键时也会触发（例如退格键）。

由于 textInput 事件主要考虑的是字符，因此它的 event 对象中还包含一个 data 属性，这个属性的值就是用户输入的字符（而非字符编码）。换句话说，用户在没有按上档键的情况下按下了 S 键，data 的值就是"s"，而如果在按住上档键时按下该键， data 的值就是"S"。

以下是一个使用 textInput 事件的例子：

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "textInput", function(event){
  event = EventUtil.getEvent(event);
  alert(event.data);
});
```

在这个例子中，插入到文本框中的字符会通过一个警告框显示出来。

另外， event 对象上还有一个属性，叫 inputMethod，表示把文本输入到文本框中的方式。

- 0，表示浏览器不确定是怎么输入的。
- 1，表示是使用键盘输入的。
- 2，表示文本是粘贴进来的。
- 3，表示文本是拖放进来的。
- 4，表示文本是使用 IME 输入的。
- 5，表示文本是通过在表单中选择某一项输入的。
- 6，表示文本是通过手写输入的（比如使用手写笔）。
- 7，表示文本是通过语音输入的。
- 8，表示文本是通过几种方法组合输入的。
- 9，表示文本是通过脚本输入的。

使用这个属性可以确定文本是如何输入到控件中的，从而可以验证其有效性。支持 textInput 属性的浏览器有 IE9+、 Safari 和 Chrome。只有 IE 支持 inputMethod 属性。

**5. 设备中的键盘事件**

任天堂 Wii 会在用户按下 Wii 遥控器上的按键时触发键盘事件。尽管没有办法访问 Wii 遥控器中的所有按键，但还是有一些键可以触发键盘事件。图 13-6 展示了一些键的键码，通过这些键码可以知道用户按下了哪个键。

当用户按下十字键盘（键码为 175～ 178）、减号（ 170）、加号（ 174）、 1（ 172）或 2（ 173）键时就会触发键盘事件。但没有办法得知用户是否按下了电源开关、 A、 B 或主页键。

iOS 版 Safari 和 Android 版 WebKit 在使用屏幕键盘时会触发键盘事件。

### 13.4.5 复合事件

复合事件（ composition event）是 DOM3 级事件中新添加的一类事件，用于处理 IME 的输入序列。IME（ Input Method Editor，输入法编辑器）可以让用户输入在物理键盘上找不到的字符。例如，使用拉丁文键盘的用户通过 IME 照样能输入日文字符。 IME 通常需要同时按住多个键，但最终只输入一个字符。复合事件就是针对检测和处理这种输入而设计的。有以下三种复合事件。

- compositionstart：在 IME 的文本复合系统打开时触发，表示要开始输入了。
- compositionupdate：在向输入字段中插入新字符时触发。
- compositionend：在 IME 的文本复合系统关闭时触发，表示返回正常键盘输入状态。

复合事件与文本事件在很多方面都很相似。在触发复合事件时，目标是接收文本的输入字段。但它比文本事件的事件对象多一个属性 data，其中包含以下几个值中的一个：

- 如果在 compositionstart 事件发生时访问，包含正在编辑的文本（例如，已经选中的需要马上替换的文本）；
- 如果在 compositionupdate 事件发生时访问，包含正插入的新字符；
- 如果在 compositionend 事件发生时访问，包含此次输入会话中插入的所有字符。

与文本事件一样，必要时可以利用复合事件来筛选输入。可以像下面这样使用它们：

```js
var textbox = document.getElementById("myText");
EventUtil.addHandler(textbox, "compositionstart", function(event){
  event = EventUtil.getEvent(event);
  alert(event.data);
});
EventUtil.addHandler(textbox, "compositionupdate", function(event){
  event = EventUtil.getEvent(event);
  alert(event.data);
});
EventUtil.addHandler(textbox, "compositionend", function(event){
  event = EventUtil.getEvent(event);
  alert(event.data);
});
```

IE9+是到 2011 年唯一支持复合事件的浏览器。由于缺少支持，对于需要开发跨浏览器应用的开发人员，它的用处不大。要确定浏览器是否支持复合事件，可以使用以下代码：

```js
var isSupported = document.implementation.hasFeature("CompositionEvent", "3.0");
```

### 13.4.6 变动事件

DOM2 级的变动（ mutation）事件能在 DOM 中的某一部分发生变化时给出提示。变动事件是为 XML或 HTML DOM 设计的，并不特定于某种语言。 DOM2 级定义了如下变动事件。

- DOMSubtreeModified：在 DOM 结构中发生任何变化时触发。这个事件在其他任何事件触发后都会触发。
- DOMNodeInserted：在一个节点作为子节点被插入到另一个节点中时触发。
- DOMNodeRemoved：在节点从其父节点中被移除时触发。
- DOMNodeInsertedIntoDocument：在一个节点被直接插入文档或通过子树间接插入文档之后触发。这个事件在 DOMNodeInserted 之后触发。除之前触发。这个事件在 DOMNodeRemoved 之后触发。
- DOMAttrModified：在特性被修改之后触发。
- DOMCharacterDataModified：在文本节点的值发生变化时触发。

使用下列代码可以检测出浏览器是否支持变动事件：

```js
var isSupported = document.implementation.hasFeature("MutationEvents", "2.0");
```

IE8 及更早版本不支持任何变动事件。下表列出了不同浏览器对不同变动事件的支持情况。

由于 DOM3 级事件模块作废了很多变动事件，所以本节只介绍那些将来仍然会得到支持的事件。

**1. 删除节点**

在使用`removeChild()`或`replaceChild()`从 DOM中删除节点时，首先会触发 DOMNodeRemoved 事件。这个事件的目标（ event.target）是被删除的节点，而 event.relatedNode 属性中包含着对
目标节点父节点的引用。在这个事件触发时，节点尚未从其父节点删除，因此其 parentNode 属性仍然指向父节点（与 event.relatedNode 相同）。这个事件会冒泡，因而可以在 DOM 的任何层次上面处理它。

如果被移除的节点包含子节点，那么在其所有子节点以及这个被移除的节点上会相继触发DOMNodeRemovedFromDocument 事件。但这个事件不会冒泡，所以只有直接指定给其中一个子节点的事件处理程序才会被调用。这个事件的目标是相应的子节点或者那个被移除的节点，除此之外 event 对象中不包含其他信息。

紧随其后触发的是 DOMSubtreeModified 事件。这个事件的目标是被移除节点的父节点；此时的event 对象也不会提供与事件相关的其他信息。

为了理解上述事件的触发过程，下面我们就以一个简单的 HTML 页面为例。

```js
<! DOCTYPE html>
<html>
<head>
  <title>Node Removal Events Example</title>
</head>
<body>
  <ul id="myList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
  </ul>
</body>
</html>
```

在这个例子中，我们假设要移除`<ul>`元素。此时，就会依次触发以下事件。

1. 在`<ul>`元素上触发 DOMNodeRemoved 事件。 relatedNode 属性等于 document.body。
2. 在`<ul>`元素上触发 DOMNodeRemovedFromDocument 事件。
3. 在身为`<ul>`元素子节点的每个`<li>`元素及文本节点上触发 DOMNodeRemovedFromDocument 事件。
4. 在 document.body 上触发 DOMSubtreeModified 事件，因为`<ul>`元素是 document.body 的直接子元素。

运行下列代码可以验证以上事件发生的顺序。

```js
EventUtil.addHandler(window, "load", function(event){
  var list = document.getElementById("myList");
  EventUtil.addHandler(document, "DOMSubtreeModified", function(event){
    alert(event.type);
    alert(event.target);
  });
  EventUtil.addHandler(document, "DOMNodeRemoved", function(event){
    alert(event.type);
    alert(event.target);
    alert(event.relatedNode);
  });
  EventUtil.addHandler(list.firstChild, "DOMNodeRemovedFromDocument", function(event){
    alert(event.type);
    alert(event.target);
  });
  list.parentNode.removeChild(list);
});
```

以上代码为 document 添加了针对 DOMSubtreeModified 和 DOMNodeRemoved 事件的处理程序，以便在页面上处理这些事件。由于 DOMNodeRemovedFromDocument 不会冒泡，所以我们将针对它的事件处理程序直接添加给了`<ul>`元素的第一个子节点（在兼容 DOM 的浏览器中是一个文本节点）。在设置了以上事件处理程序后，代码从文档中移除了`<ul>`元素。

**2. 插入节点**

在使用 `appendChild()`、 `replaceChild()`或 `insertBefore()`向 DOM 中插入节点时，首先会触发 DOMNodeInserted 事件。这个事件的目标是被插入的节点，而 event.relatedNode 属性中包含一个对父节点的引用。在这个事件触发时，节点已经被插入到了新的父节点中。这个事件是冒泡的，因此可以在 DOM 的各个层次上处理它。

紧接着，会在新插入的节点上面触发 DOMNodeInsertedIntoDocument 事件。这个事件不冒泡，因此必须在插入节点之前为它添加这个事件处理程序。这个事件的目标是被插入的节点，除此之外event 对象中不包含其他信息。

最后一个触发的事件是 DOMSubtreeModified，触发于新插入节点的父节点。

我们仍以前面的 HTML 文档为例，可以通过下列 JavaScript 代码来验证上述事件的触发顺序。

```js
EventUtil.addHandler(window, "load", function(event){
  var list = document.getElementById("myList");
  var item = document.createElement("li");
  item.appendChild(document.createTextNode("Item 4"));
  EventUtil.addHandler(document, "DOMSubtreeModified", function(event){
    alert(event.type);
    alert(event.target);
  });
  EventUtil.addHandler(document, "DOMNodeInserted", function(event){
    alert(event.type);
    alert(event.target);
    alert(event.relatedNode);
  });
  EventUtil.addHandler(item, "DOMNodeInsertedIntoDocument", function(event){
    alert(event.type);
    alert(event.target);
  });
  list.appendChild(item);
});
```

以上代码首先创建了一个包含文本"Item 4"的新`<li>`元素。由于 DOMSubtreeModified 和DOMNodeInserted 事件是冒泡的，所以把它们的事件处理程序添加到了文档中。在将列表项插入到其父节点之前，先将 DOMNodeInsertedIntoDocument 事件的事件处理程序添加给它。最后一步就是使用 appendChild()来添加这个列表项；此时，事件开始依次被触发。首先是在新`<li>`元素项上触发DOMNodeInserted 事件，其 relatedNode 是`<ul>`元素。然后是触发新`<li>`元素上的 DOMNodeInsertedIntoDocument 事件，最后触发的是`<ul>`元素上的 DOMSubtreeModified 事件。

### 13.4.7 HTML5 事件

DOM 规范没有涵盖所有浏览器支持的所有事件。很多浏览器出于不同的目的——满足用户需求或解决特殊问题，还实现了一些自定义的事件。 HTML5 详尽列出了浏览器应该支持的所有事件。本节只讨论其中得到浏览器完善支持的事件，但并非全部事件。（其他事件会在本书其他章节讨论。）

**1. contextmenu 事件**

Windows 95 在 PC 中引入了上下文菜单的概念，即通过单击鼠标右键可以调出上下文菜单。不久，这个概念也被引入了 Web 领域。为了实现上下文菜单，开发人员面临的主要问题是如何确定应该显示上下文菜单（在 Windows 中，是右键单击；在 Mac 中，是 Ctrl+单击），以及如何屏蔽与该操作关联的默认上下文菜单。为解决这个问题，就出现了 contextmenu 这个事件，用以表示何时应该显示上下文菜单，以便开发人员取消默认的上下文菜单而提供自定义的菜单。

由于 contextmenu 事件是冒泡的，因此可以为 document 指定一个事件处理程序，用以处理页面中发生的所有此类事件。这个事件的目标是发生用户操作的元素。在所有浏览器中都可以取消这个事件：在兼容 DOM 的浏览器中，使用 `event.preventDefalut()`；在 IE 中，将 event.returnValue 的值设置为 false。因为 contextmenu 事件属于鼠标事件，所以其事件对象中包含与光标位置有关的所有属性。通常使用 contextmenu 事件来显示自定义的上下文菜单，而使用 onclick 事件处理程序来隐藏该菜单。以下面的 HTML 页面为例。

```js
<!DOCTYPE html>
<html>
<head>
  <title>ContextMenu Event Example</title>
</head>
<body>
  <div id="myDiv">Right click or Ctrl+click me to get a custom context menu.
    Click anywhere else to get the default context menu.</div>
  <ul id="myMenu" style="position:absolute;visibility:hidden;background-color:
  silver">
    <li><a href="http://www.nczonline.net">Nicholas’ site</a></li>
    <li><a href="http://www.wrox.com">Wrox site</a></li>
    <li><a href="http://www.yahoo.com">Yahoo!</a></li>
  </ul>
</body>
</html>
```

这里的`<div>`元素包含一个自定义的上下文菜单。其中， `<ul>`元素作为自定义上下文菜单，并且在初始时是隐藏的。实现这个例子的 JavaScript 代码如下所示。

```js
EventUtil.addHandler(window, "load", function(event){
  var div = document.getElementById("myDiv");
  EventUtil.addHandler(div, "contextmenu", function(event){
    event = EventUtil.getEvent(event);
    EventUtil.preventDefault(event);
    var menu = document.getElementById("myMenu");
    menu.style.left = event.clientX + "px";
    menu.style.top = event.clientY + "px";
    menu.style.visibility = "visible";
  });
  EventUtil.addHandler(document, "click", function(event){
    document.getElementById("myMenu").style.visibility = "hidden";
  });
});
```

在这个例子中，我们为`<div>`元素添加了 oncontextmenu 事件的处理程序。这个事件处理程序首先会取消默认行为，以保证不显示浏览器默认的上下文菜单。然后，再根据 event 对象 clientX 和clientY 属性的值，来确定放置`<ul>`元素的位置。最后一步就是通过将 visibility 属性设置为"visible"来显示自定义上下文菜单。另外，还为 document 添加了一个 onclick 事件处理程序，以便用户能够通过鼠标单击来隐藏菜单（单击也是隐藏系统上下文菜单的默认操作）。

虽然这个例子很简单，但它却展示了 Web 上所有自定义上下文菜单的基本结构。只需为这个例子中的上下文菜单添加一些 CSS 样式，就可以得到非常棒的效果。

支持 contextmenu 事件的浏览器有 IE、 Firefox、 Safari、 Chrome 和 Opera 11+。

**2. beforeunload 事件**

之所以有发生在 window 对象上的 beforeunload 事件，是为了让开发人员有可能在页面卸载前阻止这一操作。这个事件会在浏览器卸载页面之前触发，可以通过它来取消卸载并继续使用原有页面。但是，不能彻底取消这个事件，因为那就相当于让用户无法离开当前页面了。为此，这个事件的意图是将控制权交给用户。显示的消息会告知用户页面行将被卸载（正因为如此才会显示这个消息），询问用户是否真的要关闭页面，还是希望继续留下来（见图 13-9）。

为了显示这个弹出对话框，必须将 event.returnValue 的值设置为要显示给用户的字符串（对IE 及 Fiefox 而言），同时作为函数的值返回（对 Safari 和 Chrome 而言），如下面的例子所示。

```js
EventUtil.addHandler(window, "beforeunload", function(event){
  event = EventUtil.getEvent(event);
  var message = "I'm really going to miss you if you go.";
  event.returnValue = message;
  return message;
});
```

IE 和 Firefox、 Safari 和 Chrome 都支持 beforeunload 事件，也都会弹出这个对话框询问用户是否真想离开。 Opera 11 及之前的版本不支持 beforeunload 事件。

**3. DOMContentLoaded 事件**

如前所述， window 的 load 事件会在页面中的一切都加载完毕时触发，但这个过程可能会因为要加载的外部资源过多而颇费周折。而 DOMContentLoaded 事件则在形成完整的 DOM 树之后就会触发，不理会图像、 JavaScript 文件、 CSS 文件或其他资源是否已经下载完毕。与 load 事件不同，DOMContentLoaded 支持在页面下载的早期添加事件处理程序，这也就意味着用户能够尽早地与页面进行交互。

要处理 DOMContentLoaded 事件，可以为 document 或 window 添加相应的事件处理程序（尽管这个事件会冒泡到 window，但它的目标实际上是 document）。来看下面的例子。

```js
EventUtil.addHandler(document, "DOMContentLoaded", function(event){
  alert("Content loaded");
});
```

DOMContentLoaded 事件对象不会提供任何额外的信息（其 target 属性是 document）。

IE9+、 Firefox、 Chrome、 Safari 3.1+和 Opera 9+都支持 DOMContentLoaded 事件，通常这个事件既可以添加事件处理程序，也可以执行其他 DOM 操作。这个事件始终都会在 load 事件之前触发。

对于不支持 DOMContentLoaded 的浏览器，我们建议在页面加载期间设置一个时间为 0 毫秒的超时调用，如下面的例子所示。

```js
setTimeout(function(){
  //在此添加事件处理程序
}, 0);
```

这段代码的实际意思就是：“在当前 JavaScript 处理完成后立即运行这个函数。”在页面下载和构建期间，只有一个 JavaScript 处理过程，因此超时调用会在该过程结束时立即触发。至于这个时间与DOMContentLoaded 被触发的时间能否同步，主要还是取决于用户使用的浏览器和页面中的其他代码。为了确保这个方法有效，必须将其作为页面中的第一个超时调用；即便如此，也还是无法保证在所有环境中该超时调用一定会早于 load 事件被触发。

**4. readystatechange 事件**

IE 为 DOM 文档中的某些部分提供了 readystatechange 事件。这个事件的目的是提供与文档或元素的加载状态有关的信息，但这个事件的行为有时候也很难预料。支持 readystatechange 事件的每个对象都有一个 readyState 属性，可能包含下列 5 个值中的一个。

- uninitialized（未初始化）：对象存在但尚未初始化。
- loading（正在加载）：对象正在加载数据。
- loaded（加载完毕）：对象加载数据完成。
- interactive（交互）：可以操作对象了，但还没有完全加载。
- complete（完成）：对象已经加载完毕。

这些状态看起来很直观，但并非所有对象都会经历 readyState 的这几个阶段。换句话说，如果某个阶段不适用某个对象，则该对象完全可能跳过该阶段；并没有规定哪个阶段适用于哪个对象。显然，这意味着 readystatechange 事件经常会少于 4 次，而 readyState 属性的值也不总是连续的。

对于 document 而言，值为"interactive"的 readyState 会在与 DOMContentLoaded 大致相同的时刻触发 readystatechange 事件。此时， DOM 树已经加载完毕，可以安全地操作它了，因此就会进入交互（ interactive）阶段。但与此同时，图像及其他外部文件不一定可用。下面来看一段处理readystatechange 事件的代码。

```js
EventUtil.addHandler(document, "readystatechange", function(event){
  if (document.readyState == "interactive"){
    alert("Content loaded");
  }
});
```

这个事件的 event 对象不会提供任何信息，也没有目标对象。

在与 load 事件一起使用时，无法预测两个事件触发的先后顺序。在包含较多或较大的外部资源的页面中，会在 load 事件触发之前先进入交互阶段；而在包含较少或较小的外部资源的页面中，则很难说 readystatechange 事件会发生在 load 事件前面。

让问题变得更复杂的是，交互阶段可能会早于也可能会晚于完成阶段出现，无法确保顺序。在包含较多外部资源的页面中，交互阶段更有可能早于完成阶段出现；而在页面中包含较少外部资源的情况下，完成阶段先于交互阶段出现的可能性更大。因此，为了尽可能抢到先机，有必要同时检测交互和完成阶段，如下面的例子所示。

```js
EventUtil.addHandler(document, "readystatechange", function(event){
  if (document.readyState == "interactive" || document.readyState == "complete"){
    EventUtil.removeHandler(document, "readystatechange", arguments.callee);
    alert("Content loaded");
  }
});
```

对于上面的代码来说，当 readystatechange 事件触发时， 会检测 document.readyState 的值，看当前是否已经进入交互阶段或完成阶段。如果是，则移除相应的事件处理程序以免在其他阶段再执行。注意，由于事件处理程序使用的是匿名函数，因此这里使用了 arguments.callee 来引用该函数。然后，会显示一个警告框，说明内容已经加载完毕。这样编写代码可以达到与使用 DOMContentLoaded 十分相近的效果。

支持 readystatechange 事件的浏览器有 IE、 Firfox 4+和 Opera。

> 虽然使用 readystatechange 可以十分近似地模拟 DOMContentLoaded 事件，但它们本质上还是不同的。在不同页面中， load 事件与 readystatechange 事件并不能保证以相同的顺序触发。

另外，` <script>`（在 IE 和 Opera 中）和`<link>`（仅 IE 中）元素也会触发 readystatechange 事件，可以用来确定外部的 JavaScript 和 CSS 文件是否已经加载完成。与在其他浏览器中一样，除非把动态创建的元素添加到页面中，否则浏览器不会开始下载外部资源。基于元素触发的readystatechange 事件也存在同样的问题，即 readyState 属性无论等于 "loaded" 还是"complete"都可以表示资源已经可用。有时候， readyState 会停在"loaded"阶段而永远不会“完成”；有时候，又会跳过"loaded"阶段而直接“完成”。于是，还需要像对待 document 一样采取相同的编码
方式。例如，下面展示了一段加载外部 JavaScript 文件的代码。

```js
EventUtil.addHandler(window, "load", function(){
  var script = document.createElement("script");
  EventUtil.addHandler(script, "readystatechange", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
  if (target.readyState == "loaded" || target.readyState == "complete"){
    EventUtil.removeHandler(target, "readystatechange", arguments. callee);
    alert("Script Loaded");
  }
  });
  script.src = "example.js";
  document.body.appendChild(script);
});
```

这个例子为新创建的`<script>`节点指定了一个事件处理程序。事件的目标是该节点本身，因此当触 发 readystatechange 事 件 时 ， 要 检 测 目 标 的 readyState 属 性 是 不 是 等 于 "loaded" 或"complete"。如果进入了其中任何一个阶段，则移除事件处理程序（以防止被执行两次），并显示一个警告框。与此同时，就可以执行已经加载完毕的外部文件中的函数了。

同样的编码方式也适用于通过`<link>`元素加载 CSS 文件的情况，如下面的例子所示。

```js
EventUtil.addHandler(window, "load", function(){
  var link = document.createElement("link");
  link.type = "text/css";
  link.rel= "stylesheet";
  EventUtil.addHandler(script, "readystatechange", function(event){
    event = EventUtil.getEvent(event);
    var target = EventUtil.getTarget(event);
  if (target.readyState == "loaded" || target.readyState == "complete"){
    EventUtil.removeHandler(target, "readystatechange", arguments. callee);
    alert("CSS Loaded");
  }
  });
  link.href = "example.css";
  document.getElementsByTagName("head")[0].appendChild(link);
});
```

同样，最重要的是要一并检测 readyState 的两个状态，并在调用了一次事件处理程序后就将其移除。

**5. pageshow 和 pagehide 事件**

Firefox 和 Opera 有一个特性，名叫“往返缓存”（ back-forward cache，或 bfcache），可以在用户使用浏览器的“后退”和“前进”按钮时加快页面的转换速度。这个缓存中不仅保存着页面数据，还保存了 DOM 和 JavaScript 的状态；实际上是将整个页面都保存在了内存里。如果页面位于 bfcache 中，那么再次打开该页面时就不会触发 load 事件。尽管由于内存中保存了整个页面的状态，不触发 load 事件也不应该会导致什么问题，但为了更形象地说明 bfcache 的行为， Firefox 还是提供了一些新事件。

第一个事件就是 pageshow，这个事件在页面显示时触发，无论该页面是否来自 bfcache。在重新加载的页面中， pageshow 会在 load 事件触发后触发；而对于 bfcache 中的页面， pageshow 会在页面状态完全恢复的那一刻触发。另外要注意的是，虽然这个事件的目标是 document，但必须将其事件处理程序添加到 window。来看下面的例子。

```js
(function(){
  var showCount = 0;
  EventUtil.addHandler(window, "load", function(){
    alert("Load fired");
  });
  EventUtil.addHandler(window, "pageshow", function(){
    showCount++;
    alert("Show has been fired " + showCount + " times.");
  });
})();
```

这个例子使用了私有作用域，以防止变量 showCount 进入全局作用域。当页面首次加载完成时，showCount 的值为 0。此后，每当触发 pageshow 事件， showCount 的值就会递增并通过警告框显示出来。如果你在离开包含以上代码的页面之后，又单击“后退”按钮返回该页面，就会看到 showCount 每次递增的值。这是因为该变量的状态，乃至整个页面的状态，都被保存在了内存中，当你返回这个页面时，它们的状态得到了恢复。如果你单击了浏览器的“刷新”按钮，那么 showCount 的值就会被重置为 0，因为页面已经完全重新加载了。

除了通常的属性之外， pageshow 事件的 event 对象还包含一个名为 persisted 的布尔值属性。如果页面被保存在了 bfcache 中，则这个属性的值为 true；否则，这个属性的值为 false。可以像下面这样在事件处理程序中检测这个属性。

```js
(function(){
  var showCount = 0;
  EventUtil.addHandler(window, "load", function(){
    alert("Load fired");
  });
  EventUtil.addHandler(window, "pageshow", function(){
    showCount++;
    alert("Show has been fired " + showCount +
    " times. Persisted? " + event.persisted);
  });
})();
```

通过检测 persisted 属性，就可以根据页面在 bfcache 中的状态来确定是否需要采取其他操作。

与 pageshow 事件对应的是 pagehide 事件，该事件会在浏览器卸载页面的时候触发，而且是在unload 事件之前触发。与 pageshow 事件一样， pagehide 在 document 上面触发，但其事件处理程序必须要添加到 window 对象。 这个事件的 event 对象也包含 persisted 属性，不过其用途稍有不同。来看下面的例子。

```js
EventUtil.addHandler(window, "pagehide", function(event){
  alert("Hiding. Persisted? " + event.persisted);
});
```

有时候，可能需要在 pagehide 事件触发时根据 persisted 的值采取不同的操作。对于 pageshow 事件，如果页面是从 bfcache 中加载的，那么 persisted 的值就是 true；对于 pagehide 事件，如果页面在卸载之后会被保存在 bfcache 中，那么 persisted 的值也会被设置为 true。因此，当第一次触发 pageshow 时， persisted 的值一定是 false，而在第一次触发 pagehide 时， persisted 就会变成 true（除非页面不会被保存在 bfcache 中）。

支持 pageshow 和 pagehide 事件的浏览器有 Firefox、 Safari 5+、 Chrome 和 Opera。 IE9 及之前版本不支持这两个事件。

> 指定了 onunload 事件处理程序的页面会被自动排除在 bfcache 之外，即使事件处理程序是空的。原因在于， onunload 最常用于撤销在 onload 中所执行的操作，而跳过 onload 后再次显示页面很可能就会导致页面不正常。

**6. hashchange 事件**

HTML5 新增了 hashchange 事件，以便在 URL 的参数列表（及 URL 中“#”号后面的所有字符串）发生变化时通知开发人员。之所以新增这个事件，是因为在 Ajax 应用中，开发人员经常要利用 URL 参数列表来保存状态或导航信息。

必须要把 hashchange 事件处理程序添加给 window 对象，然后 URL 参数列表只要变化就会调用它。此时的 event 对象应该额外包含两个属性： oldURL 和 newURL。这两个属性分别保存着参数列表变化前后的完整 URL。例如：

```js
EventUtil.addHandler(window, "hashchange", function(event){
  alert("Old URL: " + event.oldURL + "\nNew URL: " + event.newURL);
});
```

支持 hashchange 事件的浏览器有 IE8+、 Firefox 3.6+、 Safari 5+、 Chrome 和 Opera 10.6+。在这些浏览器中， 只有 Firefox 6+、 Chrome 和 Opera 支持 oldURL 和 newURL 属性。为此，最好是使用 location 对象来确定当前的参数列表。

```js
EventUtil.addHandler(window, "hashchange", function(event){
  alert("Current hash: " + location.hash);
});
```

使用以下代码可以检测浏览器是否支持 hashchange 事件：

```js
var isSupported = ("onhashchange" in window); //这里有 bug
```

如果 IE8 是在 IE7 文档模式下运行，即使功能无效它也会返回 true。为解决这个问题，可以使用以下这个更稳妥的检测方式：

```js
var isSupported = ("onhashchange" in window) && (document.documentMode ===
  undefined || document.documentMode > 7);
```

### 13.4.8 设备事件

智能手机和平板电脑的普及，为用户与浏览器交互引入了一种新的方式，而一类新事件也应运而生。设备事件（ device event）可以让开发人员确定用户在怎样使用设备。 W3C 从 2011 年开始着手制定一份关于设备事件的[新草案](http://dev.w3.org/geo/api/spec-source-orientation.html)，以涵盖不断增长的设备类型并为它们定义相关的事件。本节会同时讨论这份草案中涉及的 API 和特定于浏览器开发商的事件。

**1. orientationchange 事件**

苹果公司为移动 Safari 中添加了 orientationchange 事件，以便开发人员能够确定用户何时将设备由横向查看模式切换为纵向查看模式。移动 Safari 的 window.orientation 属性中可能包含 3 个值：0 表示肖像模式， 90 表示向左旋转的横向模式（“主屏幕”按钮在右侧）， -90 表示向右旋转的横向模式（“主屏幕”按钮在左侧）。相关文档中还提到一个值，即 180 表示 iPhone 头朝下；但这种模式至今尚未得到支持。图 13-10 展示了 window.orientation 的每个值的含义。

只要用户改变了设备的查看模式，就会触发 orientationchange 事件。此时的 event 对象不包含任何有价值的信息，因为唯一相关的信息可以通过 window.orientation 访问到。下面是使用这个事件的典型示例。

```js
EventUtil.addHandler(window, "load", function(event){
  var div = document.getElementById("myDiv");
  div.innerHTML = "Current orientation is " + window.orientation;
  EventUtil.addHandler(window, "orientationchange", function(event){
    div.innerHTML = "Current orientation is " + window.orientation;
  });
});
```

在这个例子中，当触发 load 事件时会显示最初的方向信息。然后，添加了处理 orientationchange 事件的处理程序。只要发生这个事件，就会有表示新方向的信息更新页面中的消息。

所有 iOS 设备都支持 orientationchange 事件和 window.orientation 属性。由于可以将 orientationchange 看成 window 事件，所以也可以通过指定`<body>`元素的 onorientationchange 特性来指定事件处理程序。

**2. MozOrientation 事件**

Firefox 3.6 为检测设备的方向引入了一个名为 MozOrientation 的新事件。（前缀 Moz 表示这是特定于浏览器开发商的事件，不是标准事件。）当设备的加速计检测到设备方向改变时，就会触发这个事件。但这个事件与 iOS 中的 orientationchange 事件不同，该事件只能提供一个平面的方向变化。由于 MozOrientation 事件是在 window 对象上触发的，所以可以使用以下代码来处理。

```js
EventUtil.addHandler(window, "MozOrientation", function(event){
  //响应事件
});
```

此时的 event 对象包含三个属性： x、 y 和 z。这几个属性的值都介于 1 到-1 之间，表示不同坐标轴上的方向。在静止状态下， x 值为 0， y 值为 0， z 值为 1（表示设备处于竖直状态）。如果设备向右倾斜， x 值会减小；反之，向左倾斜， x 值会增大。类似地，如果设备向远离用户的方向倾斜， y 值会减小，向接近用户的方向倾斜， y 值会增大。 z 轴检测垂直加速度度， 1 表示静止不动，在设备移动时值会减小。（失重状态下值为 0。）以下是输出这三个值的一个简单的例子。

```js
EventUtil.addHandler(window, "MozOrientation", function(event){
  var output = document.getElementById("output");
  output.innerHTML = "X=" + event.x + ", Y=" + event.y + ", Z=" + event.z +"<br>";
});
```

只有带加速计的设备才支持 MozOrientation 事件，包括 Macbook、 Lenovo Thinkpad、 Windows Mobile 和 Android 设备。请大家注意，这是一个实验性 API，将来可能会变（可能会被其他事件取代）。

**3. deviceorientation 事件**

本质上， DeviceOrientation Event 规范定义的 deviceorientation 事件与 MozOrientation 事件类似。它也是在加速计检测到设备方向变化时在 window 对象上触发，而且具有与 MozOrientation 事件相同的支持限制。不过， deviceorientation 事件的意图是告诉开发人员设备在空间中朝向哪儿，而不是如何移动。

设备在三维空间中是靠 x、 y 和 z 轴来定位的。当设备静止放在水平表面上时，这三个值都是 0。 x 轴方向是从左往右， y 轴方向是从下往上， z 轴方向是从后往前（参见图 13-11）。

触发 deviceorientation 事件时，事件对象中包含着每个轴相对于设备静止状态下发生变化的信息。事件对象包含以下 5 个属性。

- alpha：在围绕 z 轴旋转时（即左右旋转时）， y 轴的度数差；是一个介于 0 到 360 之间的浮点数。
- beta：在围绕 x 轴旋转时（即前后旋转时）， z 轴的度数差；是一个介于180 到 180 之间的浮点数。
- gamma：在围绕 y 轴旋转时（即扭转设备时）， z 轴的度数差；是一个介于90 到 90 之间的浮点数。
- absolute：布尔值，表示设备是否返回一个绝对值。
- compassCalibrated：布尔值，表示设备的指南针是否校准过。

图 13-12 是 alpha、 beta 和 gamma 值含义的示意图。

```js
下面是一个输出 alpha、 beta 和 gamma 值的例子。
EventUtil.addHandler(window, "deviceorientation", function(event){
  var output = document.getElementById("output");
  output.innerHTML = "Alpha=" + event.alpha + ", Beta=" + event.beta +
  ", Gamma=" + event.gamma + "<br>";
});
```

通过这些信息，可以响应设备的方向，重新排列或修改屏幕上的元素。要响应设备方向的改变而旋转元素，可以参考如下代码。

```js
EventUtil.addHandler(window, "deviceorientation", function(event){
  var arrow = document.getElementById("arrow");
  arrow.style.webkitTransform = "rotate(" + Math.round(event.alpha) + "deg)";
});
```

这个例子只能在移动 WebKit 浏览器中运行，因为它使用了专有的 webkitTransform 属性（即 CSS 标准属性 transform 的临时版）。元素“arrow”会随着 event.alpha 值的变化而旋转，给人一种指南
针的感觉。为了保证旋转平滑，这里的 CSS3 变换使用了舍入之后的值。

到 2011 年，支持 deviceorientation 事件的浏览器有 iOS 4.2+中的 Safari、 Chrome 和 Android 版 WebKit。

**4. devicemotion 事件**

DeviceOrientation Event 规范还定义了一个 devicemotion 事件。这个事件是要告诉开发人员设备什么时候移动，而不仅仅是设备方向如何改变。例如，通过 devicemotion 能够检测到设备是不是正在
往下掉，或者是不是被走着的人拿在手里。

触发 devicemotion 事件时，事件对象包含以下属性。

- acceleration：一个包含 x、 y 和 z 属性的对象，在不考虑重力的情况下，告诉你在每个方向上的加速度。
- accelerationIncludingGravity：一个包含 x、 y 和 z 属性的对象，在考虑 z 轴自然重力加速度的情况下，告诉你在每个方向上的加速度。
- interval：以毫秒表示的时间值，必须在另一个 devicemotion 事件触发前传入。这个值在每个事件中应该是一个常量。
- rotationRate：一个包含表示方向的 alpha、 beta 和 gamma 属性的对象。

如果读取不到 acceleration、 accelerationIncludingGravity 和 rotationRate 值，则它们的值为 null。因此，在使用这三个属性之前，应该先检测确定它们的值不是 null。例如：

```js
EventUtil.addHandler(window, "devicemotion", function(event){
  var output = document.getElementById("output");
  if (event.rotationRate !== null){
    output.innerHTML += "Alpha=" + event.rotationRate.alpha + ", Beta=" +
    event.rotationRate.beta + ", Gamma=" +
    event.rotationRate.gamma;
  }
});
```

与 deviceorientation 事件类似，只有 iOS 4.2+中的 Safari、 Chrome 和 Android 版 WebKit 实现了devicemotion 事件。

### 13.4.9 触摸与手势事件

iOS 版 Safari 为了向开发人员传达一些特殊信息，新增了一些专有事件。因为 iOS 设备既没有鼠标也没有键盘，所以在为移动 Safari 开发交互性网页时，常规的鼠标和键盘事件根本不够用。随着 Android 中的 WebKit 的加入，很多这样的专有事件变成了事实标准，导致 W3C 开始制定 Touch Events 规范（参见 https://dvcs.w3.org/hg/webevents/raw-file/tip/touchevents.html）。以下介绍的事件只针对触摸设备。

**1. 触摸事件**

包含 iOS 2.0 软件的 iPhone 3G 发布时，也包含了一个新版本的 Safari 浏览器。这款新的移动 Safari 提供了一些与触摸（ touch）操作相关的新事件。后来， Android 上的浏览器也实现了相同的事件。触摸事件会在用户手指放在屏幕上面时、在屏幕上滑动时或从屏幕上移开时触发。具体来说，有以下几个触摸事件。

- touchstart：当手指触摸屏幕时触发；即使已经有一个手指放在了屏幕上也会触发。
- touchmove： 当手指在屏幕上滑动时连续地触发。在这个事件发生期间，调用 `preventDefault()`可以阻止滚动。
- touchend：当手指从屏幕上移开时触发。
- touchcancel：当系统停止跟踪触摸时触发。关于此事件的确切触发时间，文档中没有明确说明。

上面这几个事件都会冒泡，也都可以取消。虽然这些触摸事件没有在 DOM 规范中定义，但它们却是以兼容 DOM 的方式实现的。因此，每个触摸事件的 event 对象都提供了在鼠标事件中常见的属性：bubbles、 cancelable、 view、 clientX、 clientY、 screenX、 screenY、 detail、 altKey、 shiftKey、 ctrlKey 和 metaKey。

除了常见的 DOM 属性外，触摸事件还包含下列三个用于跟踪触摸的属性。

- touches：表示当前跟踪的触摸操作的 Touch 对象的数组。
- targetTouchs：特定于事件目标的 Touch 对象的数组。
- changeTouches：表示自上次触摸以来发生了什么改变的 Touch 对象的数组。

每个 Touch 对象包含下列属性。

- clientX：触摸目标在视口中的 x 坐标。
- clientY：触摸目标在视口中的 y 坐标。
- identifier：标识触摸的唯一 ID。
- pageX：触摸目标在页面中的 x 坐标。
- pageY：触摸目标在页面中的 y 坐标。
- screenX：触摸目标在屏幕中的 x 坐标。
- screenY：触摸目标在屏幕中的 y 坐标。
- target：触摸的 DOM 节点目标。

使用这些属性可以跟踪用户对屏幕的触摸操作。来看下面的例子。

```js
function handleTouchEvent(event){
  //只跟踪一次触摸
  if (event.touches.length == 1){
    var output = document.getElementById("output");
    switch(event.type){
    case "touchstart":
    output.innerHTML = "Touch started (" + event.touches[0].clientX +
    "," + event.touches[0].clientY + ")";
    break;
    case "touchend":
    output.innerHTML += "<br>Touch ended (" +
    event.changedTouches[0].clientX + "," +
    event.changedTouches[0].clientY + ")";
    break;
    case "touchmove":
    event.preventDefault(); //阻止滚动
    output.innerHTML += "<br>Touch moved (" +
    event.changedTouches[0].clientX + "," +
    event.changedTouches[0].clientY + ")";
    break;
    }
  }
}
EventUtil.addHandler(document, "touchstart", handleTouchEvent);
EventUtil.addHandler(document, "touchend", handleTouchEvent);
EventUtil.addHandler(document, "touchmove", handleTouchEvent);
```

以上代码会跟踪屏幕上发生的一次触摸操作。为简单起见，只会在有一次活动触摸操作的情况下输出信息。当 touchstart 事件发生时，会将触摸的位置信息输出到`<div>`元素中。当 touchmove 事件发生时，会取消其默认行为，阻止滚动（触摸移动的默认行为是滚动页面），然后输出触摸操作的变化信息。而 touchend 事件则会输出有关触摸操作的最终信息。注意，在 touchend 事件发生时， touches 集合中就没有任何 Touch 对象了，因为不存在活动的触摸操作；此时，就必须转而使用 changeTouchs 集合。

这些事件会在文档的所有元素上面触发，因而可以分别操作页面的不同部分。在触摸屏幕上的元素时，这些事件（包括鼠标事件）发生的顺序如下：

1. touchstart
2. mouseover
3. mousemove（一次）
4. mousedown
5. mouseup
6. click
7. touchend

支持触摸事件的浏览器包括 iOS 版 Safari、 Android 版 WebKit、 bada 版 Dolfin、 OS6+中的 BlackBerry WebKit、 Opera Mobile 10.1+和 LG 专有 OS 中的 Phantom 浏览器。目前只有 iOS 版 Safari 支持多点触摸。

桌面版 Firefox 6+和 Chrome 也支持触摸事件。

**2. 手势事件**

iOS 2.0 中的 Safari 还引入了一组手势事件。当两个手指触摸屏幕时就会产生手势，手势通常会改变显示项的大小，或者旋转显示项。有三个手势事件，分别介绍如下。

- gesturestart：当一个手指已经按在屏幕上而另一个手指又触摸屏幕时触发。
- gesturechange：当触摸屏幕的任何一个手指的位置发生变化时触发。
- gestureend：当任何一个手指从屏幕上面移开时触发。

只有两个手指都触摸到事件的接收容器时才会触发这些事件。在一个元素上设置事件处理程序，意味着两个手指必须同时位于该元素的范围之内，才能触发手势事件（这个元素就是目标）。由于这些事
件冒泡，所以将事件处理程序放在文档上也可以处理所有手势事件。此时，事件的目标就是两个手指都位于其范围内的那个元素。

触摸事件和手势事件之间存在某种关系。当一个手指放在屏幕上时，会触发 touchstart 事件。如果另一个手指又放在了屏幕上，则会先触发 gesturestart 事件，随后触发基于该手指的 touchstart 事件。如果一个或两个手指在屏幕上滑动，将会触发 gesturechange 事件。但只要有一个手指移开，就会触发 gestureend 事件，紧接着又会触发基于该手指的 touchend 事件。

与触摸事件一样，每个手势事件的 event 对象都包含着标准的鼠标事件属性： bubbles、 cancelable、 view、 clientX、 clientY、 screenX、 screenY、 detail、 altKey、 shiftKey、 ctrlKey 和 metaKey。此外，还包含两个额外的属性： rotation 和 scale。其中， rotation 属性表示手指变化引起的旋转角度，负值表示逆时针旋转，正值表示顺时针旋转（该值从 0 开始）。而 scale 属性表示两个手指间距离的变化情况（例如向内收缩会缩短距离）；这个值从 1 开始，并随距离拉大而增长，随距离缩短而减小。

下面是使用手势事件的一个示例。

```js
function handleGestureEvent(event){
  var output = document.getElementById("output");
  switch(event.type){
    case "gesturestart":
    output.innerHTML = "Gesture started (rotation=" + event.rotation +
    ",scale=" + event.scale + ")";
    break;
    case "gestureend":
    output.innerHTML += "<br>Gesture ended (rotation=" + event.rotation +
    ",scale=" + event.scale + ")";
    break;
    case "gesturechange":
    output.innerHTML += "<br>Gesture changed (rotation=" + event.rotation +
    ",scale=" + event.scale + ")";
    break;
  }
}
document.addEventListener("gesturestart", handleGestureEvent, false);
document.addEventListener("gestureend", handleGestureEvent, false);
document.addEventListener("gesturechange", handleGestureEvent, false);
```

与前面演示触摸事件的例子一样，这里的代码只是将每个事件都关联到同一个函数中，然后通过该函数输出每个事件的相关信息。

> 触摸事件也会返回 rotation 和 scale 属性，但这两个属性只会在两个手指与屏幕保持接触时才会发生变化。一般来说，使用基于两个手指的手势事件，要比管理触摸事件中的所有交互要容易得多。

## 13.5 内存和性能 

由于事件处理程序可以为现代 Web 应用程序提供交互能力，因此许多开发人员会不分青红皂白地向页面中添加大量的处理程序。在创建 GUI 的语言（如 C#）中，为 GUI 中的每个按钮添加一个 onclick 事件处理程序是司空见惯的事，而且这样做也不会导致什么问题。可是在 JavaScript 中，添加到页面上的事件处理程序数量将直接关系到页面的整体运行性能。导致这一问题的原因是多方面的。首先，每个函数都是对象，都会占用内存；内存中的对象越多，性能就越差。其次，必须事先指定所有事件处理程序而导致的 DOM 访问次数，会延迟整个页面的交互就绪时间。事实上，从如何利用好事件处理程序的角度出发，还是有一些方法能够提升性能的。

### 13.5.1 事件委托

对“事件处理程序过多”问题的解决方案就是事件委托。事件委托利用了事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。例如， click 事件会一直冒泡到 document 层次。也就是说，我们可以为整个页面指定一个 onclick 事件处理程序，而不必给每个可单击的元素分别添加事件处理程序。以下面的 HTML 代码为例。

```html
<ul id="myLinks">
  <li id="goSomewhere">Go somewhere</li>
  <li id="doSomething">Do something</li>
  <li id="sayHi">Say hi</li>
</ul>
```

其中包含 3 个被单击后会执行操作的列表项。按照传统的做法，需要像下面这样为它们添加 3 个事件处理程序。

```js
var item1 = document.getElementById("goSomewhere");
var item2 = document.getElementById("doSomething");
var item3 = document.getElementById("sayHi");

EventUtil.addHandler(item1, "click", function(event){
  n.href = "http://www.wrox.com";
});
EventUtil.addHandler(item2, "click", function(event){
  document.title = "I changed the document's title";
});
EventUtil.addHandler(item3, "click", function(event){
  alert("hi");
});
```

如果在一个复杂的 Web 应用程序中，对所有可单击的元素都采用这种方式，那么结果就会有数不清的代码用于添加事件处理程序。此时，可以利用事件委托技术解决这个问题。使用事件委托，只需在 DOM 树中尽量最高的层次上添加一个事件处理程序，如下面的例子所示。

```js
var list = document.getElementById("myLinks");
EventUtil.addHandler(list, "click", function(event){
  event = EventUtil.getEvent(event);
  var target = EventUtil.getTarget(event);
  switch(target.id){
    case "doSomething":
      document.title = "I changed the document's title";
      break;
    case "goSomewhere":
      location.href = "http://www.wrox.com";
      break;
    case "sayHi":
      alert("hi");
      break;
  }
});
```

在这段代码里，我们使用事件委托只为`<ul>`元素添加了一个 onclick 事件处理程序。由于所有列表项都是这个元素的子节点，而且它们的事件会冒泡，所以单击事件最终会被这个函数处理。我们知道，事件目标是被单击的列表项，故而可以通过检测 id 属性来决定采取适当的操作。与前面未使用事件委托的代码比一比，会发现这段代码的事前消耗更低，因为只取得了一个 DOM 元素，只添加了一个事件处理程序。虽然对用户来说最终的结果相同，但这种技术需要占用的内存更少。所有用到按钮的事件（多数鼠标事件和键盘事件）都适合采用事件委托技术。

如果可行的话，也可以考虑为 document 对象添加一个事件处理程序，用以处理页面上发生的某种特定类型的事件。这样做与采取传统的做法相比具有如下优点。

- document 对象很快就可以访问，而且可以在页面生命周期的任何时点上为它添加事件处理程序（无需等待 DOMContentLoaded 或 load 事件）。换句话说，只要可单击的元素呈现在页面上，就可以立即具备适当的功能。
- 在页面中设置事件处理程序所需的时间更少。只添加一个事件处理程序所需的 DOM 引用更少，所花的时间也更少。
- 整个页面占用的内存空间更少，能够提升整体性能。

最适合采用事件委托技术的事件包括 click、mousedown、mouseup、keydown、keyup 和 keypress。虽然 mouseover 和 mouseout 事件也冒泡，但要适当处理它们并不容易，而且经常需要计算元素的位置。（因为当鼠标从一个元素移到其子节点时，或者当鼠标移出该元素时，都会触发 mouseout 事件。）

### 13.5.2 移除事件处理程序

每当将事件处理程序指定给元素时，运行中的浏览器代码与支持页面交互的 JavaScript 代码之间就会建立一个连接。这种连接越多，页面执行起来就越慢。如前所述，可以采用事件委托技术，限制建立的连接数量。另外，在不需要的时候移除事件处理程序，也是解决这个问题的一种方案。内存中留有那些过时不用的“空事件处理程序”（ dangling event handler），也是造成 Web 应用程序内存与性能问题的主要原因。

在两种情况下，可能会造成上述问题。第一种情况就是从文档中移除带有事件处理程序的元素时。这可能是通过纯粹的 DOM 操作，例如使用 `removeChild()`和 `replaceChild()`方法，但更多地是发生在使用 innerHTML 替换页面中某一部分的时候。如果带有事件处理程序的元素被 innerHTML 删除了，那么原来添加到元素中的事件处理程序极有可能无法被当作垃圾回收。来看下面的例子。

```html
<div id="myDiv">
  <input type="button" value="Click Me" id="myBtn">
</div>
<script type="text/javascript">
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  //先执行某些操作
  document.getElementById("myDiv").innerHTML = "Processing..."; //麻烦了！
};
</script>
```

这里，有一个按钮被包含在`<div>`元素中。为避免双击，单击这个按钮时就将按钮移除并替换成一条消息；这是网站设计中非常流行的一种做法。但问题在于，当按钮被从页面中移除时，它还带着一个事件处理程序呢。在`<div>`元素上设置 innerHTML 可以把按钮移走，但事件处理程序仍然与按钮保持着引用关系。有的浏览器（尤其是 IE）在这种情况下不会作出恰当地处理，它们很有可能会将对元素和对事件处理程序的引用都保存在内存中。如果你知道某个元素即将被移除，那么最好手工移除事件处理程序，如下面的例子所示。

```html
<div id="myDiv">
  <input type="button" value="Click Me" id="myBtn">
</div>
<script type="text/javascript">
var btn = document.getElementById("myBtn");
btn.onclick = function(){
  //先执行某些操作
  btn.onclick = null; //移除事件处理程序
  document.getElementById("myDiv").innerHTML = "Processing...";
};
</script>
```

在此，我们在设置`<div>`的 innerHTML 属性之前，先移除了按钮的事件处理程序。这样就确保了内存可以被再次利用，而从 DOM 中移除按钮也做到了干净利索。

注意，在事件处理程序中删除按钮也能阻止事件冒泡。目标元素在文档中是事件冒泡的前提。

> 采用事件委托也有助于解决这个问题。如果事先知道将来有可能使用 innerHTML 替换掉页面中的某一部分，那么就可以不直接把事件处理程序添加到该部分的元素中。而通过把事件处理程序指定给较高层次的元素，同样能够处理该区域中的事件。

导致“空事件处理程序”的另一种情况，就是卸载页面的时候。毫不奇怪， IE8 及更早版本在这种情况下依然是问题最多的浏览器，尽管其他浏览器或多或少也有类似的问题。如果在页面被卸载之前没有清理干净事件处理程序，那它们就会滞留在内存中。每次加载完页面再卸载页面时（可能是在两个页面间来回切换，也可以是单击了“刷新”按钮），内存中滞留的对象数目就会增加，因为事件处理程序占用的内存并没有被释放。

一般来说，最好的做法是在页面卸载之前，先通过 onunload 事件处理程序移除所有事件处理程序。在此，事件委托技术再次表现出它的优势——需要跟踪的事件处理程序越少，移除它们就越容易。对这种类似撤销的操作，我们可以把它想象成：只要是通过 onload 事件处理程序添加的东西，最后都要通过 onunload 事件处理程序将它们移除。

> 不要忘了，使用 onunload 事件处理程序意味着页面不会被缓存在 bfcache 中。如果你在意这个问题，那么就只能在 IE 中通过 onunload 来移除事件处理程序了。

## 13.6 模拟事件

事件，就是网页中某个特别值得关注的瞬间。事件经常由用户操作或通过其他浏览器功能来触发。但很少有人知道，也可以使用 JavaScript 在任意时刻来触发特定的事件，而此时的事件就如同浏览器创建的事件一样。也就是说，这些事件该冒泡还会冒泡，而且照样能够导致浏览器执行已经指定的处理它们的事件处理程序。在测试 Web 应用程序，模拟触发事件是一种极其有用的技术。 DOM2 级规范为此规定了模拟特定事件的方式， IE9、 Opera、 Firefox、 Chrome 和 Safari 都支持这种方式。 IE 有它自己模拟事件的方式。

### 13.6.1 DOM中的事件模拟

可以在 document 对象上使用 `createEvent()`方法创建 event 对象。这个方法接收一个参数，即表示要创建的事件类型的字符串。在 DOM2 级中，所有这些字符串都使用英文复数形式，而在 DOM3 级中都变成了单数。这个字符串可以是下列几字符串之一。

- UIEvents：一般化的 UI 事件。 鼠标事件和键盘事件都继承自 UI 事件。 DOM3 级中是 UIEvent。
- MouseEvents：一般化的鼠标事件。 DOM3 级中是 MouseEvent。
- MutationEvents：一般化的 DOM 变动事件。 DOM3 级中是 MutationEvent。
- HTMLEvents：一般化的 HTML 事件。没有对应的 DOM3 级事件（ HTML 事件被分散到其他类别中）。

要注意的是，“DOM2 级事件”并没有专门规定键盘事件，后来的“DOM3 级事件”中才正式将其作为一种事件给出规定。 IE9 是目前唯一支持 DOM3 级键盘事件的浏览器。不过，在其他浏览器中，在现有方法的基础上，可以通过几种方式来模拟键盘事件。

在创建了 event 对象之后，还需要使用与事件有关的信息对其进行初始化。每种类型的 event 对象都有一个特殊的方法，为它传入适当的数据就可以初始化该 event 对象。不同类型的这个方法的名字也不相同，具体要取决于 `createEvent()`中使用的参数。

模拟事件的最后一步就是触发事件。这一步需要使用 `dispatchEvent()`方法，所有支持事件的DOM 节点都支持这个方法。调用 `dispatchEvent()`方法时，需要传入一个参数，即表示要触发事件的 event 对象。触发事件之后，该事件就跻身“官方事件”之列了，因而能够照样冒泡并引发相应事件处理程序的执行。

**1. 模拟鼠标事件**

创建新的鼠标事件对象并为其指定必要的信息，就可以模拟鼠标事件。创建鼠标事件对象的方法是为 createEvent()传入字符串"MouseEvents"。返回的对象有一个名为 initMouseEvent()方法，用于指定与该鼠标事件有关的信息。这个方法接收 15 个参数，分别与鼠标事件中每个典型的属性一一对应；这些参数的含义如下。

- type（字符串）：表示要触发的事件类型，例如"click"。
- bubbles（布尔值）：表示事件是否应该冒泡。为精确地模拟鼠标事件，应该把这个参数设置为true。
- cancelable（布尔值）：表示事件是否可以取消。为精确地模拟鼠标事件，应该把这个参数设置为 true。
- view（ AbstractView）：与事件关联的视图。这个参数几乎总是要设置为 document.defaultView。
- detail（整数）： 与事件有关的详细信息。这个值一般只有事件处理程序使用，但通常都设置为 0。
- screenX（整数）：事件相对于屏幕的 X 坐标。
- screenY（整数）：事件相对于屏幕的 Y 坐标。
- clientX（整数）：事件相对于视口的 X 坐标。
- clientY（整数）：事件想对于视口的 Y 坐标。
- ctrlKey（布尔值）：表示是否按下了 Ctrl 键。默认值为 false。
- altKey（布尔值）：表示是否按下了 Alt 键。默认值为 false。
- shiftKey（布尔值）：表示是否按下了 Shift 键。默认值为 false。
- metaKey（布尔值）：表示是否按下了 Meta 键。默认值为 false。
- button（整数）：表示按下了哪一个鼠标键。默认值为 0。
- relatedTarget（对象）： 表示与事件相关的对象。这个参数只在模拟 mouseover 或 mouseout 时使用。

显而易见， initMouseEvent()方法的这些参数是与鼠标事件的 event 对象所包含的属性一一对应的。其中，前 4 个参数对正确地激发事件至关重要，因为浏览器要用到这些参数；而剩下的所有参数只有在事件处理程序中才会用到。当把 event 对象传给 dispatchEvent()方法时，这个对象的 target 属性会自动设置。下面，我们就通过一个例子来了解如何模拟对按钮的单击事件。

```js
var btn = document.getElementById("myBtn");
//创建事件对象
var event = document.createEvent("MouseEvents");
//初始化事件对象
event.initMouseEvent("click", true, true, document.defaultView, 0, 0, 0, 0, 0,
false, false, false, false, 0, null);
//触发事件
btn.dispatchEvent(event);
```

在兼容 DOM 的浏览器中，也可以通过相同的方式来模拟其他鼠标事件（例如 dblclick）。

**2. 模拟键盘事件**

前面曾经提到过，“DOM2 级事件”中没有就键盘事件作出规定，因此模拟键盘事件并没有现成的思路可循。“DOM2 级事件”的草案中本来包含了键盘事件，但在定稿之前又被删除了； Firefox 根据其草案实现了键盘事件。需要提请大家注意的是，“DOM3 级事件”中的键盘事件与曾包含在“DOM2 级事件”草案中的键盘事件有很大区别。

DOM3 级规定，调用 createEvent()并传入"KeyboardEvent"就可以创建一个键盘事件。返回的事件对象会包含一个 initKeyEvent()方法，这个方法接收下列参数。

- type（字符串）：表示要触发的事件类型，如"keydown"。
- bubbles（布尔值）：表示事件是否应该冒泡。为精确模拟鼠标事件，应该设置为 true。
- cancelable（布尔值）：表示事件是否可以取消。为精确模拟鼠标事件，应该设置为 true。
- view （ AbstractView ）：与事件关联的视图。这个参数几乎总是要设置为 document.defaultView。
- key（布尔值）：表示按下的键的键码。
- location（整数）：表示按下了哪里的键。 0 表示默认的主键盘， 1 表示左， 2 表示右， 3 表示数字键盘， 4 表示移动设备（即虚拟键盘）， 5 表示手柄。
- modifiers（字符串）：空格分隔的修改键列表，如"Shift"。
- repeat（整数）：在一行中按了这个键多少次。

由于 DOM3 级不提倡使用 keypress 事件，因此只能利用这种技术来模拟 keydown 和 keyup 事件。

```js
var textbox = document.getElementById("myTextbox"),
event;
//以 DOM3 级方式创建事件对象
if (document.implementation.hasFeature("KeyboardEvents", "3.0")){
  event = document.createEvent("KeyboardEvent");
  //初始化事件对象
  event.initKeyboardEvent("keydown", true, true, document.defaultView, "a",
  0, "Shift", 0);
}
//触发事件
textbox.dispatchEvent(event);
```

这个例子模拟的是按住Shift的同时又按下A键。在使用 `document.createEvent("KeyboardEvent")`之前，应该先检测浏览器是否支持 DOM3 级事件；其他浏览器返回一个非标准的 KeyboardEvent 对象。

在 Firefox 中，调用 createEvent()并传入"KeyEvents"就可以创建一个键盘事件。返回的事件对象会包含一个 initKeyEvent()方法，这个方法接受下列 10 个参数。

- type（字符串）：表示要触发的事件类型，如"keydown"。
- bubbles（布尔值）：表示事件是否应该冒泡。为精确模拟鼠标事件，应该设置为 true。
- cancelable（布尔值）：表示事件是否可以取消。为精确模拟鼠标事件，应该设置为 true。
- view（ AbstractView）：与事件关联的视图。这个参数几乎总是要设置为 document.defaultView。
- ctrlKey（布尔值）：表示是否按下了 Ctrl 键。默认值为 false。
- altKey（布尔值）：表示是否按下了 Alt 键。默认值为 false。
- shiftKey（布尔值）：表示是否按下了 Shift 键。默认值为 false。
- metaKey（布尔值）：表示是否按下了 Meta 键。默认值为 false。
- keyCode（整数）：被按下或释放的键的键码。这个参数对 keydown 和 keyup 事件有用，默认值为 0。
- charCode（整数）：通过按键生成的字符的 ASCII 编码。这个参数对 keypress 事件有用，默认值为 0。

将创建的 event 对象传入到 dispatchEvent()方法就可以触发键盘事件，如下面的例子所示。

```js
//只适用于 Firefox
var textbox = document.getElementById("myTextbox")
//创建事件对象
var event = document.createEvent("KeyEvents");
//初始化事件对象
event.initKeyEvent("keypress", true, true, document.defaultView, false, false,
false, false, 65, 65);
//触发事件
textbox.dispatchEvent(event);
```

在 Firefox 中运行上面的代码，会在指定的文本框中输入字母 A。同样，也可以依此模拟 keyup 和 keydown 事件。

在其他浏览器中，则需要创建一个通用的事件，然后再向事件对象中添加键盘事件特有的信息。例如：

```js
var textbox = document.getElementById("myTextbox");
//创建事件对象
var event = document.createEvent("Events");
//初始化事件对象
event.initEvent(type, bubbles, cancelable);
event.view = document.defaultView;
event.altKey = false;
event.ctrlKey = false;
event.shiftKey = false;
event.metaKey = false;
event.keyCode = 65;
event.charCode = 65;
//触发事件
textbox.dispatchEvent(event);
```

以上代码首先创建了一个通用事件，然后调用 initEvent()对其进行初始化，最后又为其添加了键盘事件的具体信息。在此必须要使用通用事件，而不能使用 UI 事件，因为 UI 事件不允许向 event 对象中再添加新属性（ Safari 除外）。像这样模拟事件虽然会触发键盘事件，但却不会向文本框中写入文本，这是由于无法精确模拟键盘事件所造成的。

**3. 模拟其他事件**

虽然鼠标事件和键盘事件是在浏览器中最经常模拟的事件，但有时候同样需要模拟变动事件和 HTML 事件。要模拟变动事件，可以使用 createEvent("MutationEvents") 创建一个包含initMutationEvent()方法的变动事件对象。这个方法接受的参数包括： type、 bubbles 、 cancelable、 relatedNode、 preValue、 newValue、 attrName 和 attrChange。下面来看一个模拟变动事件的例子。

```js
var event = document.createEvent("MutationEvents");
event.initMutationEvent("DOMNodeInserted", true, false, someNode, "","","",0);
target.dispatchEvent(event);
```

以上代码模拟了 DOMNodeInserted 事件。其他变动事件也都可以照这个样子来模拟，只要改一改参数就可以了。

要模拟 HTML 事件，同样需要先创建一个 event 对象——通过 createEvent("HTMLEvents")，然后再使用这个对象的 initEvent()方法来初始化它即可，如下面的例子所示。

```js
var event = document.createEvent("HTMLEvents");
event.initEvent("focus", true, false);
target.dispatchEvent(event);
```

这个例子展示了如何在给定目标上模拟 focus 事件。模拟其他 HTML 事件的方法也是这样。

> 浏览器中很少使用变动事件和 HTML 事件，因为使用它们会受到一些限制。

**4. 自定义 DOM 事件**

DOM3 级还定义了“自定义事件”。自定义事件不是由 DOM 原生触发的，它的目的是让开发人员创建自己的事件。要创建新的自定义事件，可以调用 createEvent("CustomEvent")。返回的对象有一个名为 initCustomEvent()的方法，接收如下 4 个参数。

- type（字符串）：触发的事件类型，例如"keydown"。
- bubbles（布尔值）：表示事件是否应该冒泡。
- cancelable（布尔值）：表示事件是否可以取消。
- detail（对象）：任意值，保存在 event 对象的 detail 属性中。

可以像分派其他事件一样在 DOM 中分派创建的自定义事件对象。例如：

```js
var div = document.getElementById("myDiv"),
event;
EventUtil.addHandler(div, "myevent", function(event){
  alert("DIV: " + event.detail);
});
EventUtil.addHandler(document, "myevent", function(event){
  alert("DOCUMENT: " + event.detail);
});
if (document.implementation.hasFeature("CustomEvents", "3.0")){
  event = document.createEvent("CustomEvent");
  event.initCustomEvent("myevent", true, false, "Hello world!");
  div.dispatchEvent(event);
}
```

这个例子创建了一个冒泡事件"myevent"。而 event.detail 的值被设置成了一个简单的字符串，然后在`<div>`元素和 document 上侦听这个事件。因为 initCustomEvent()方法已经指定这个事件应该冒泡，所以浏览器会负责将事件向上冒泡到 document。

支持自定义 DOM 事件的浏览器有 IE9+和 Firefox 6+。

### 13.6.2 IE中的事件模拟

在 IE8 及之前版本中模拟事件与在 DOM 中模拟事件的思路相似：先创建 event 对象，然后为其指定相应的信息，然后再使用该对象来触发事件。当然， IE 在实现每个步骤时都采用了不一样的方式。调用 document.createEventObject()方法可以在 IE 中创建 event 对象。但与 DOM 方式不同的是，这个方法不接受参数，结果会返回一个通用的 event 对象。然后，你必须手工为这个对象添加所有必要的信息（没有方法来辅助完成这一步骤）。最后一步就是在目标上调用 fireEvent()方法，这个方法接受两个参数：事件处理程序的名称和 event 对象。在调用 fireEvent()方法时，会自动为event 对象添加 srcElement 和 type 属性；其他属性则都是必须通过手工添加的。换句话说，模拟任何 IE 支持的事件都采用相同的模式。例如，下面的代码模拟了在一个按钮上触发 click 事件过程。

```js
var btn = document.getElementById("myBtn");
//创建事件对象
var event = document.createEventObject();
//初始化事件对象
event.screenX = 100;
event.screenY = 0;
event.clientX = 0;
event.clientY = 0;
event.ctrlKey = false;
event.altKey = false;
event.shiftKey = false;
event.button = 0;
//触发事件
btn.fireEvent("onclick", event);
```

这个例子先创建了一个 event 对象，然后又用一些信息对其进行了初始化。注意，这里可以为对象随意添加属性，不会有任何限制——即使添加的属性 IE8 及更早版本并不支持也无所谓。在此添加的属性对事件没有什么影响，因为只有事件处理程序才会用到它们。

采用相同的模式也可以模拟触发 keypress 事件，如下面的例子所示。

```js
var textbox = document.getElementById("myTextbox");
//创建事件对象
var event = document.createEventObject();
//初始化事件对象
event.altKey = false;
event.ctrlKey = false;
event.shiftKey = false;
event.keyCode = 65;
//触发事件
textbox.fireEvent("onkeypress", event);
```

由于鼠标事件、键盘事件以及其他事件的 event 对象并没有什么不同，所以可以使用通用对象来触发任何类型的事件。不过， 正如在 DOM中模拟键盘事件一样，运行这个例子也不会因模拟了 keypress 而在文本框中看到任何字符，即使触发了事件处理程序也没有用。

## 13.7 小结

事件是将 JavaScript 与网页联系在一起的主要方式。“DOM3 级事件”规范和 HTML5 定义了常见的大多数事件。即使有规范定义了基本事件，但很多浏览器仍然在规范之外实现了自己的专有事件，从而为开发人员提供更多掌握用户交互的手段。有些专有事件与特定设备关联，例如移动 Safari 中的 orientationchange 事件就是特定关联 iOS 设备的。

在使用事件时，需要考虑如下一些内存与性能方面的问题。

- 有必要限制一个页面中事件处理程序的数量，数量太多会导致占用大量内存，而且也会让用户感觉页面反应不够灵敏。
- 建立在事件冒泡机制之上的事件委托技术，可以有效地减少事件处理程序的数量。
- 建议在浏览器卸载页面之前移除页面中的所有事件处理程序。

可以使用 JavaScript 在浏览器中模拟事件。“DOM2 级事件”和“DOM3 级事件”规范规定了模拟事件的方法，为模拟各种有定义的事件提供了方便。此外，通过组合使用一些技术，还可以在某种程度上模拟键盘事件。 IE8 及之前版本同样支持事件模拟，只不过模拟的过程有些差异。

事件是 JavaScript 中最重要的主题之一，深入理解事件的工作机制以及它们对性能的影响至关重要。

# 第14章 表单脚本　

## 14.1 表单的基础知识

在HTML中，表单是由`<form>`元素来表示的，而在JavaScript中，表单对应的则是HTMLFormElement类型，继承了HTMLElement，有相同的默认属性，也有独特的属性和方法。取得`<form>`元素引用的方式有好几种。通过getElementById()方法获取，通过document.forms获取所有表单然后以数值索引或者name值来取得特定的表单。在较早的浏览器或者支持向后兼容的浏览器中，也会把每个设置了name特性的表单作为属性保存在document对象中。

提交表单。使用`<input>`或`<button>`都可以定义提交按钮，只要将其type特性的值设置为"submit"即可，而图像按钮则是通过将`<input>`的type特性值设置为"image"来定义，src表示图像位置。拥有焦点的表单控件，按下回车键触发提交，除了textarea，同时在浏览器发送请求给服务器之前触发submit，这样就有机会验证表单数据。在JavaScript中，还可以以编程的方式调用submit()方法提交表单，这种方式无需表单包含提交按钮。提交表单时可能出现的最大问题，就是重复提交表单，解决这个问题的办法有两个：在第一次提交表单后旧禁用表单按钮，或者利用onsubmit事件处理程序取消后续的表单提交操作。

重置表单。使用type特性值为"reset"的`<input>`或`<button>`都可以创建重置按钮。在重置表单时，所有表单字段都会恢复到页面刚加载完毕时的初始值。用户单击重置按钮重置表单时，会触发reset事件，因此可以取消重置操作，同时也能调用reset()方法触发reset事件。

表单字段。每个表单都有elements属性，该属性时表单中所有表单元素（字段）的集合，这个集合是一个有序列表，可以按照位置和name特性来访问，如果多个表单控件都在使用一个name，就会返回以该name命名的一个NodeList。公有的表单字段属性。除了form属性之外，可以通过JavaScript动态去修改其他任何属性，包括disable、name、readOnly、tabIndex、type、value。公有的表单字段方法。每个表单字段都有两个方法：focus()和blur()，HTML5为表单字段新增了一个autofocus属性，只要设置这个属性，不用JavaScript就能自动把焦点移动到相应的字段。共有的表单字段事件。基本上表单字段都支持blur、change和focus事件。change事件在不同表单控件中触发的次数会有所不同。

## 14.2 文本框脚本 

在HTML中，有两种方式表现文本框，`<input>`单行文本框和`<textarea>`多行文本框。选择文本。无论这两种文本框在标记中有什么区别，但它们都会把用户输入的内容保存在value属性中，通过使用value属性或设置文本框的值修改，不建议使用标准的DOM方法。

选择文本。调用select()方法，大多数浏览器都会将焦点设置到文本框中，这个方法不接受参数。在选择了文本框的文本或者调用slect()方法时，就会触发select事件。有两个属性：selectStionart和selectionEnd，这两个属性保存的是基于0的数值，表示所选择文本的范围（即文本选取开头和结尾的偏移量）。IE8及更早的版本不支持，可以通过document.selection对象，对象保存着用户在整个文档范围内选择的文本信息，即可通过document.selection。createRange().text取得焦点所在文本。选择部分文本。除了select()方法，所有文本框还有setSelectionRange()方法，这个方法接收两个参数：要选择的第一个字符的索引和要选择的最后一个字符之后的字符的索引。如果IE是老版本，则需要先用createRange()方法创建一个范围，然后使用collapse()将范围折叠到文本框的开始位置，接着调用那个moveStart()和moveEnd()这两个方法，最后使用范围的select()方法选择文本。

过滤输入。屏蔽字符，响应向文本框中插入字符操作的是keypress事件，先取得字符编码，然后将字符编码转换成字符串，再使用正则表达式来测试该字符串，从而确定用户输入的是不是数值，如果测试失败，可以通过阻止这个事件的默认行为来屏蔽此类字符。

操作剪贴板，剪贴板事件有六个：beforecopy、copy、beforecut、cut、beforepaste、paste，在实际的事件发生之前before+事件可以向剪贴板发送数据，或者从剪贴板取得数据之前修改数据，但是取消操作只能用事件copy、cut和paste。要访问剪贴板中的数据，可以使用clipboardData对象，一般在了确保跨浏览器兼容性，最好只在发生剪贴板事件期间使用这个对象，这个对象有三个方法：getData()、setData()和clearData()，第一个方法接受一个参数，即要取得的数据的格式，第二个方法第一个参数也是数据类型，第二个参数是要放在剪贴板中的文本。自动切换焦点。通过函数比较用户输入的值与文本框的maxlength特性，如果值相等，则需要查找表单字段集合，直至找到下一个文本框，找到之后将焦点奇幻到该文本框。然后，我们把这个函数指定为每个文本框的onkeyup事件处理程序。

HTML5约束验证API。第一种情况是在表单字段中指定了required属性。HTML5为`<input>`元素的type属性又增加了几个值，这些新的类型不仅能反映数据类型的信息，而且还能提供一些默认的验证功能。例如"email"类型要求输入的文本必须符合电子邮件地址的模式，而"url"类型要求输入的文本必须符合URL的模式，这些设置特定的输入类型不能阻止用户输入无效的值，只能应用某些默认的验证。HTML5还定义了另外几种输入元素，这几个元素都要求填写某种基于数字的值："number"、"range"、"datetime"、"datetime-local"、"date""mouth"、"week""tiem"。对于这些数值类型的输入元素，可以指定min属性、max属性和step属性。以上属性在JavaScript中都能通过对应的元素访问或修改，此外还有两个方法：stepUp()和stepDown()，都接收一个可选的参数，要在当前值基础上加上或减去的数值。输入模式。HTML5为文本字段新增了pattern属性，这个属性的值是一个正则表达式，用于匹配文本框中的值，模式的开头和末尾不用加^和$符号表示输入的值必须从头到尾都与模式匹配。检测有效性。使用checkValidity()方法可以检测表单中的某个字段是否有效，使用validity属性则显示字段为什么有效或无效。这个对象中包含一系列属性，每个属性会返回一个布尔值，如果判断不匹配，则返回true。禁用验证。通过设置novalidate属性，可以告诉表单不进行验证。在JavaScript中使用noValidate属性可以取得或设置这个值，如果这个属性存在，值为true，否则为false。

## 14.3 选择框脚本 

选择框是通过`<select>`和`<option>`元素创建的，为了方便与这个控件交互，除了所有表单字段公有的属性和方法外，HTMLSelectElement类型还提供了下列属性和方法，add、multiple、options、remove(index)、selectedIndex、size，选择框的type属性不是"select-one"，就是"select-multiple"，这取决于HTML代码中有没有multiple特性。选择框的value属性由当前选中项决定，如果没有选中项，则value属性保存空字符串，如果如果有选中项但value值未指定，则value属性等于该项的文本。在DOM中，每个`<option>`元素都有一个HTMLOptionElement对象表示，对象有着indx、label、selected、text、value属性。同时，选择框的change事件与其他表单字段的change事件触发的条件不一样，选择框的change事件只要选中了选项就会触发，其它表单字段则是在值被修改且焦点离开当前字段时触发。

选择选项。对于只允许选择某一项的选择框，访问选中项的最简单方式，就是使用选择框的selectedIndex属性。对于可以选择多项的选择框，selectedIndex属性就好像只允许选择一项一样。设置selectedIndex会导致取消以前的所有选项并选择指定的那一项，而读取selectedIndex则只会返回选中项中第一项的索引。另一种选择选项的方式，就是取得对某一项的引用，然后将其selected属性设置为true，要取得所有选中的项，可以循环遍历选项集合，然后测试每个选项的selected属性，从而确定选中的数组。

添加选项。可以使用JavaScript动态创建选项，并将它们添加到选择框中。第一种方法是使先创建元素，再添加文本节点和value特性，最后使用`appendChild()`方法将元素对象添加到选择框中。第二种方法是使用Option构造函数来创建新选项，这个构造函数接收两个参数：文本和值，第二参数可选。第三种添加新选项的方式是使用选择框的add()方法。这个方法接收两个参数：要添加的新选项和将位于新选项之后的选项。如果想在列表的最后添加一个选项，应该将第二个参数设置为null值。

移除选项。移除选项可以使用DOM的removeChild()方法，为其传入要移除的选项。其次，可以使用选择框的remove()方法。最后一种方法，就是将相应选项设置为null值，移除选项后，所有后续选项都会自动向上移动一个位置。

移动和重排选项。使用DOM的appendChild()方法，就可以将第一个选择框中的选项直接移动到第二个选择框汇总。如果该方法传入一个文档中已有的元素，那么就会先从该元素的父节点中移除它，再把它添加到指定的位置，移动选项与移除选项有一个共通之处，就是会重置每一个选项的index属性。

## 14.4 表单序列化 

在JavaScript中，可以利用表单字段的type属性，连同name和value属性一起实现对表单的序列化。

表单提交期间，浏览器通过发送给服务器的数据是有

- 对表单字段的名称和值进行 URL 编码，使用和号（&）分隔。
- 不发送禁用的表单字段。
- 只发送勾选的复选框和单选按钮。
- 不发送 type 为"reset"和"button"的按钮。
- 多选选择框中的每个选中的值单独一个条目。
- 在单击提交按钮提交表单的情况下，也会发送提交按钮；否则，不发送提交按钮。也包括 type
为"image"的`<input>`元素。
- `<select>`元素的值，就是选中的`<option>`元素的 value 特性的值。如果`<option>`元素没有 value 特性，则是`<option>`元素的文本值。

在表单序列化过程中，一般不包含任何按钮字段，因为结果字符串很可能是通过其他方式提交的。

```JavaScript
function serialize(form) {
  var parts = [],
    field = null,
    i,
    len,
    j,
    optLen,
    option,
    optValue;
  for (i = 0, len = form.elements.length; i < len; i++) {
    field = form.elements[i];
    switch (field.type) {
      case "select-one":
      case "select-multiple":
        if (field.name.length) {
          for (j = 0, optLen = field.options.length; j < optLen; j++) {
            option = field.options[j];
            if (option.selected) {
              optValue = "";
              if (option.hasAttribute) {
                optValue = option.hasAttribute("value")
                  ? option.value
                  : option.text;
              } else {
                optValue = option.attributes["value"].specified
                  ? option.value
                  : option.text;
              }
              parts.push(
                encodeURIComponent(field.name) +
                  "=" +
                  encodeURIComponent(optValue)
              );
            }
          }
        }
        break;
      case undefined: //字段集
      case "file": //文件输入
      case "submit": //提交按钮
      case "reset": //重置按钮
      case "button": //自定义按钮
        break;
      case "radio": //单选按钮
      case "checkbox": //复选框
        if (!field.checked) {
          break;
        }
      /* 执行默认操作 */
      default:
        //不包含没有名字的表单字段
        if (field.name.length) {
          parts.push(
            encodeURIComponent(field.name) +
              "=" +
              encodeURIComponent(field.value)
          );
        }
    }
  }
  return parts.join("&");
}
```

## 14.5 富文本编辑 

富文本编辑器，又称为WYSIWYG，所见即多得。这一技术的本质，就是在页面中嵌入一个包含空HTML页面的iframe，通过设置designMode属性，这个空白的HTML页面可以被编辑，而编辑对象则是该页面`<body>`元素的HTML代码。designMode属性有两个可能的值："off"和"on"。在包含页面中，必须使用onload事件处理程序来在适当的时刻设置designMode。

另一种编辑富文本内容的方式是使用名为contentedditable的特殊属性。通过设置该属性，这个元素好像变成了`<textarea>`元素一样，这个属性有三个可能的值："true"表示打开、"false"表示关闭、"inherit"表示从父元素那里继承。

操作富文本。使用document.execCommand()方法可以对文档执行预定义的命令，而且可以应用大多数格式，这个方法有三个参数：要执行的命令名称、表示浏览器是否应该为当前命令提供用户界面的一个布尔值和执行命令必须的一个值（如果不需要值，则传递null）。除了命令外，还有一些与命令相关的方法，第一个方法就是queryCommandEnabled()，可以用它来检测是否可以针对当前选择的文本，或者当前插入字符所在位置执行命令，这个方式接收一个表示检测的命令的参数。如果当前编辑区域允许执行传入的命令，这个方法返回true，否则返回false。最后一个方法是queryCommandValue()，用于取得执行命令时传入的值。

富文本选取。使用iframe的getSelection()方法，可以确定实际选择的文本，这个方法是window对象和document对象的属性，调用它会返回一个表示当前选择文本的Selection对象，每个Selection对象都有多个属性和方法，同时也可以访问DOM范围对富文本编辑器进行更加细化的控制。

表单与富文本。由于富文本编辑是使用iframe而非表单控件实现的，因此从技术上说富文本编辑器并不属于表单，需要我们手动来提取并提交HTML给服务器。可以通过文档主体的innerHTML属性取得了iframe中的HTML，然后将其插入到了表单字段中。

14.6　小结　

# 第15章 使用Canvas绘图　

## 15.1 基本用法 

使用`<canvas>`元素，必须先设置其width和Height属性，指定可以绘图的区域大小，出现在开始和结束中的内容是后备信息，如果浏览器不支持该元素，就会显示这些信息。调用getContext()方法并传入上下文的名字，可以取得绘图上下文对象的引用。传入"2D"，就可以取得2D上下文对象。使用toDataURL()方法，可以导出在`<canvas>`元素上绘制的图像，这个方法接受一个参数，即图像的MIME类型格式，而且适合用于创建图像的任何上下文。

## 15.2 2D上下文 

2D上下文的坐标开始于`<canvas>`元素的左上角。2D上下文的两种基本绘图操作是填充和描边。填充，就是用指定的样式填充图形；描边，就是在图形的边缘划线，操作的结果取决于两个属性：fillStyle和strokeStyle，这两个属性的值可以是字符串、渐变对象或模式对象。

矩形是唯一一种可以直接在2D上下文中绘制的形状，与矩形有关的方法包括fillRect()、strokeRect()和clearRect()。这三个方法都能接收4个参数：矩形的x坐标、矩形的y坐标、矩形宽度和矩形高度，这些参数的单位都是像素。fillRect()方法在画布上绘制使用指定的颜色填充，填充颜色通过fillStyle属性指定；strokeRect()在画布上绘制使用指定的颜色描边，描边颜色通过strokeStyle属性指定，描边线条的宽度由lineWidth属性控制。

绘制路径首先必须调用beginPath()方法，表示要开始绘制新路径。然后，arc()创建弧/曲线（用于创建圆形或部分圆），arcTo()创建两切线之间的弧/曲线，lineTo()添加一个新点，然后在画布中创建从该点到最后指定点的线条，moveTo()把路径移动到画布中的指定点，不创建线条，quadraticCurveTo()创建二次贝塞尔曲线，bezierCurveTo()创建三次方贝塞尔曲线，rect()创建矩形路径。创建了路径后，调用closePath()方法可以绘制一条连接到路径起点的线条，使用fill()方法可以填充该路径，使用stroke()方法可以对路径描边，使用slip()放可以在路径上创建一个剪切区域。使用isPointInPath()方法，可以在路径被关闭之前确定画布上的某一点是否位于路径上，这个方法接收需要确定的点的x和y坐标作为参数。

绘制文本主要有两个方法：fillText()和strokeText()。这两个方法都可以接收4个参数：要绘制的文本字符串、x坐标、y坐标和可选的最大像素宽度。这两个方法都以font、textAlign和textBaseline属性为基础。2D上下文提供了服务确定文本大小的方法measureText()方法，这个方法接收一个参数，即要绘制的文本，返回一个TextMetrics对象。

通过上下文的变换，可以把处理后的图像绘制到画布上。方法有rotate()旋转，scale()缩放，translate()重新映射画布上的(0,0)位置，transform()替换绘图的当前转换矩阵，setTransform()将当前转换重置为单位矩阵。然后运行transform()。使用save()方法可以保存某组属性与变换的组合，通过restore()方法可以在设置的栈结构中向前返回一级，回复之前的状态。

2D绘图上下文内置了对图像的支持，可以使用drawImage()方法将一幅图像绘制到画布上。总共可以传入9个参数：要绘制的图像、源图像的x坐标、源图像的y坐标、源图像的宽度、源图像的高度、目标图像的x坐标、目标图像的y坐标、目标图像的宽度、目标图像的高度。除了给drawImage()方法传入HTML`<img>`元素外，还可以传入另一个`<canvas>`元素作为其第一个参数。

2D上下文会根据以下几个属性的值，自动为形状或路径绘制出阴影。shadowColor用CSS颜色格式表示的阴影颜色，shadowOffsetX和shadowOffsetY表示阴影偏移量，shadowBlur模糊的像素数。

渐变由CanvasGradient实例表示，createLineGradient()方法可以创建一个新的线性渐变，接收的四个参数是起点的坐标和终点的坐标，这样就可以有一个指定大小的渐变并返回CanvasGradient对象的实例。使用addColorStop()方法来指定色标，接收的两个参数是色标位置和CSS颜色值，为了让渐变覆盖整个矩形，而不是仅应用到矩形的一部分，矩形和渐变对象的坐标必须匹配才行。课使用createRadialGradient()方法，这个方法接收5个参数，对应两个圆的圆心和半径。
模式。调用createPattern()方法并传入两个参数：一个HTML`<img>`元素和一个表示如何重复图像的字符串，就可以用来填充或描边图形。

使用图像数据。通过使用getImageData()方法取得原始图像数据，这个方法接收4个参数：要取得其数据的画面区域的x和y坐标以及该区域的像素宽度和高度。返回的对象是ImageData的实例，每个ImageData对象都有三个属性：width、height和data，其中data属性是一个数组，保存着图像中每个像素的数据。在打他数组中，每个像素用四个元素来保存，分别表示红绿蓝和透明度值。调用putImageData()方法把图像数据绘制到画布上。

合成。属性globalAlpha是一个介于0和1之间的值（包括0和1），用于指定所有绘制的透明度，默认值为0。globalCompositionOperate属性表示后绘制的图形怎么样与先绘制的图形结合，属性值是特定的字符串。

## 15.3 WebGL 

WebGL是针对Canvas的3D上下文，WebGL并不是W3C制订的标准。类型化数组的元素被设置为特定类型的值，核心是名为ArrayBuffer的类型，表示内存中指定的字节数。使用ArrayBuffer的一种特别的方式就是用它来创建数组缓冲器视图，最常见的视图是DataView，通过它可以选择ArrayBuffer中一小段字节。类型化视图一般也被陈伟类型化数组，因为他们除了元素必须是某种特定的数据类型外，与常会的数组无异，类型化视图也分几种，而且它们都继承了DataView，类型化视图的目的在于简化对二进制数据的操作。WebGL上下文，一般都把WebGL上下文对象命名为gl，通过给getContext()传递第二个参数，可以为WebGL上下文设置一些选项。在WebGL中，保存在上下文对象中的这些常量都没有GL_前缀，方法都试图通过名字传递有关数据类型的信息。在实际操作WebGL上下文之前，一般都要使用某种实色清除`<canvas>`，为绘图做好准备。默认情况下，WebGL视口可以使用整个`<canvas>`区域，吐过要改变大小可以调用viewport()方法并传入4个参数。顶点信息保存在JavaScript的类型化数组中，使用之前必须转换到WebGL的缓冲区，要创建缓冲区，可以调用gl.createBuffer()，然后使用gl.bindBuffer()绑定到WebGL上下文。JavaScript与WebGL之间的最大的区别在于，WebGL操作一般不会抛出错误，为了知道是否有错误发生，必须在调用某个可能出错的方法后，手工调用gl.getError()方法，这个方法返回一个表示错误类型的常量。WebGL中有两种着色器：顶点着色器和片段着色器，顶点着色器用于将3D顶点转换为需要渲染的2D点，片段着色器用于准确计算要绘制的每个像素的颜色。着色器是使用GLSL编写的类C语言，每个着色器都有一个main()方法，该方法在绘图期间会重复执行，为着色器传递数据的方式有两种：Attribute和Uniform。浏览器不能理解GLSL程序，因此必须准备好字符串形式的GLSL程序，以便编译并链接到着色器程序。取得了GLSL字符串之后，接下来就是创建着色器对象。为着色器传值，Uniform变量可以使用gl.getUniformcation()方法，该方法返回一个对象，表示Uniform变量在内存中的位置，然后可以基于变量的位置来赋值。着色器操作也可能会失败，而且是静默失败，如果想知道着色器或程序执行中是否发生了错误，必须亲自询问WebGL上下文。WebGL只能绘制三种形状：点、线和三角，其它所有形状都是由这三种基本形状合成之后，再绘制到三维空间中的，执行绘图操作要调用gl.drawArrays()或gl.drawElements()方法，前者用于数组缓冲区，后者用于元素数组缓冲区。WebGL的纹理可以使用DOM中的图像，要创建一个新纹理，可以调用gl.createTexture()，然后再将一幅图像绑定到该纹理。与2D上下文类似，通过WebGL上下文也能读取像素值。读取像素值的方法readPixels()与OpenGL中的同名方法只有一点不同，即最后一个参数必须是类型化数组。

15.4 小结　

# 第16章 HTML5脚本编程　

## 16.1 跨文档消息传递 

跨文档消息传达，有时候简称为XDM，指的是在来自不同域的页面间传递消息。XDM的核心是postMessage()方法，接收两个参数：一条消息和一个表示消息接收方来自哪个域的字符串。第二个参数对保障安全通信非常重要，可以防止浏览器把小心发送到不安全的地方。接收到XDM消息时，会触发window对象的message事件，事件触发是异步的，触发后传递给onmessage处理程序的事件对象包含以下三方面的重要信息：data字符串数据、origin文档所在域和source对象的代理。event.source大多数情况下只是window对象的代理，并非实际的window对象，一般只通过调用postMessage()方法发送回执。

## 16.2 原生拖放 

按下鼠标键并开始移动鼠标时，会在被拖放的元素上出发dragstart事件，此时光标变成“不能放”符号，表示不能把元素放到自己上面。触发dragstart事件后，随即会触发drag事件，而且在元素被拖动期间会持续触发该事件，与鼠标过程中mousemove事件类似。当拖动停止时，会触发dragend事件。同理，当某个元素被拖动到一个有效的放置目标上时，下列事件会在放置目标的元素依次发生，dragenter、dragover（在放置目标内移动）、dragleave或drop。其中dragleave是元素被拖出了放置目标才触发，类似mouseout事件，而drop事件时元素被放到了放置目标中才会触发。

自定义放置目标。在拖动元素经过某些无效放置目标时，可以看到一种特殊的光标（圆环中有一条反斜线），表示不能放置。可以把任何元素变成有效的放置目标，方法是重写dragenter和dragover事件的默认行为。

dataTransfer对象，它是事件对象的一个属性，用于从被拖动元素向放置目标传递字符串格式的数据。该对象有两个主要方法：getData()和setData()。前者只有一个参数，即用来表示保存的数据类型的一个字符串，取值为"text"或"URL"。后者的第二个参数是字符串数据。实际上，dataTransfer对象可以为每种MIME类型都保存一个值。将数据保存为文本和保存为URL是由区别的，后者会跳转到另一个浏览器窗口。

dropEffect与effectAllowed。在dataTransfer对象中，dropEffect属性可以知道被拖动的元素能够执行哪种放置行为，属性值有none、move、copy和link，在把元素拖动到放置目标上时，以上每个值都会导致光标显示为不同的符号。dropEffect属性只有搭配effectAllowed属性才有用，effectAllowed属性表示允许拖动元素的哪种dropEffect。

HTML5为所有HTML元素规定了一个draggable属性，表示元素是否可以拖动。图像和链接的draggable属性自动被设置成了true，而其它元素这个属性的默认值都是false。

## 16.3 媒体元素 

使用`<audio>`和`<video>`标签元素，至少要在标签中包含src属性，指向要加载的媒体文件，还可以设置width和height属性以指定视频播放器的大小，而为poster属性指定图像的URI可以在加载视频内容期间显示一幅图像。另外，如果标签中有controls属性，则意味着浏览器应该显示UI控件，以便用户直接操作媒体。位于开始和结束标签之间的任何内容都将作为后备内容，在浏览器不支持这两个媒体元素的情况下显示。通过使用一个或多个`<source>`元素，可以指定多个不同的媒体俩元。这两个媒体元素有大量属性和可以触发很多事件，这些事件监控者不同的属性的变化，这些变化是媒体播放的结果，也可能是用户操作播放器的结果。

检测编解码器的支持情况。这两个媒体元素都有一个canPlayType()方法，该方法接收一种格式/编解码器字符串，返回"probably"、"maybe"或""，空字符串是假值。

`<audio>`元素还有一个原生的JavaScript构造函数Audio，可以在任何时候播放音频。创建新的的Audio实例即可开始下载指定的文件。下载完成后，调用play()就可以播放音频。

## 16.4 历史状态管理 

HTML5通过更新history对象为管理历史状态提供了方便。通过hashchange事件，可以知道URL的参数什么时候发生了变化，即什么时候有所反应。通过状态管理API，能够在不加载新页面的情况下改变浏览器的URL。为此，需要使用history.pushState()方法，该方法接收三个参数：状态对象、新状态的标签和可选的相对URL。执行pushState()方法后，新的状态信息就会被加入历史状态栈，而浏览器地址栏也会变成新的相对URL。按下“后退”按钮，会触发window对象的popstate事件，它有一个包含当初以第一个参数传递给pushState()的状态对象的state属性。得到这个状态对象后，必须把页面重置为状态对象中的数据表示的状态。需要更新当前状态，可以调用replaceState()，传入的参数与pushState()的前两个参数相同。调用这个方法不会再历史状态栈中创建新状态，只会重写当前状态。

16.5　小结　

# 第17章 错误处理与调试　

## 17.1 浏览器报告的错误 

IE是唯一一个在浏览器的界面窗体中显示JavaScript错误信息的浏览器。

## 17.2 错误处理

ECMA-262 第 3 版引入了 try-catch 语句，作为 JavaScript 中处理异常的一种标准方式。只要代码中还包含 finally 子句，则无论 try 或 catch 语句块中包含什么代码，甚至 return 语句，都不会阻止 finally 子句的执行。

错误类型 Error 是基类型，其它错误类型都继承自该类型。EvalError 类型的错误会在使用 `eval()` 函数而发生异常时被抛出。RangeError 类型的错误会在数值超出相应范围时触发。ReferenceError 类型在找不到对象的情况下触发，这种情况下会直接导致人所共知的"object expected"浏览器错误，通常，在访问不存在的变量时，就会发生这种错误。SyntaxError 类型是在把语法错误的 JavaScript 字符串传入 `eval()` 函数时触发。TypeError 类型在 JavaScript 中经常用到，在变量中保存着意外的类型时，或者在访问不存在的方法时，都会导致这种错误。在使用 `encodeURI()` 或 `decodeURI()` ，而 URI 格式不正确时，就会导致 URIError 错误。

当 try-catch 语句中发生错误时，浏览器会认为错误已经被处理了，而不会出现机制记录或报告错误。使用 try-catch 最适合处理那些我们无法控制的错误。与这个语句相配的还有一个 throw 操作符，用于随时抛出自定义错误。抛出错误时，必须要给 throw 操作符指定一个值，值的类型没要求。在遇到 throw 操作符时，代码会立刻停止执行，仅当有 try-catch 语句捕获到被抛出的值时，代码才会继续执行。通过使用某种内置错误类型，可以更真实地模拟浏览器错误，每种错误类型的构造函数接收一个参数，即实际的错误消息。另外，利用原型链还可以通过继承 Error 来创建自定义错误类型。要针对函数为什么会执行失败给出更多信息，抛出自定义错误是一种很方便的方式。

任何没有通过 try-catch 处理的错误都会触发 window 对象的 error 事件。在任何 Web 浏览器中，onerror 事件处理程序都不会创建 event 对象，但它可以接收三个参数：错误消息、错误所在的 URL 和行号。要指定 onerrror 事件处理程序，必须使用 DOM0 级技术，它没有遵循“DOM2 级事件”的标准格式。如果触发 error 事件并执行事件处理程序时，通过返回 false，这个函数实际上就充当了整个文档中的 try-catch 语句，可以捕获所有无代码处理的运行时错误。

常见的错误类型。类型转换错误发生在使用某个操作符，或者使用其他可能会自动转换值的数据类型的语言结构时。数据类型错误，JavaScript 是松散类型的，也就是说，在使用变量和函数参数之前，不会对它们进行比较以确保它们的数据类型正确。大体上来说，基本类型的值应该使用 typeof 来检测，而对象的值则应该使用 instanceof 来检测。通信错误，第一种通讯错误与格式不正确的 URL 或发送的数据有关，最常见的问题是在将数据发送给服务器之前没有使用 `encodeURIComponent()` 对数据进行编码，另外在服务器响应的数据不正确时也会发生通信错误。

区分志明错误和非致命错误。区分两者的依据，就是看它们对用户的影响。开发 Web 应用程序过程中的一种常见的做法，就是集中保存错误日记，一边查找重要错误的原因。要建立这样一种 JavaScript 错误记录系统，首先需要在服务器上创建一个页面（或者一个服务器入口点），用于处理错误数据。

## 17.3 调试技术

将消息记录到控制台。一般都可以通过 console 对象向 JavaScript 控制台中写入消息，这个对象具有下列方法：将错误消息记录到控制台 `error()` 、将信息性消息记录到控制台 `info()` 、将一般消息记录到控制台 `log()` 、将警告信息记录到控制台 `warn()` 。将消息记录到当前页面。就是在页面中开辟一小块区域，在这个区域通常是一个元素，而该元素可以总是出现在页面中，但仅用于调试目的。抛出错误。对于大型应用程序来说，自定义的错误通常都是用 `assert()` 函数抛出。

## 17.4 常见的 IE 错误

操作终止。在修改尚未加载完成的页面时，就会发生操作终止错误，此时出现一个模态对话框，提示“操作终止”。无效字符。在 JavaScript 文件中存在无效字符时，IE 会抛出无效字符错误，即 JavaScript 语法中未定义的字符。为找到成员。具体来说，如果在对象被销毁之后，又给对象赋值，就会导致未找到成员错误。未知运行时错误。当使用 innerHTML 或 outerHTML 以下列方式指定 HTML 时，就会发生未知运行时错误：一是把块元素插入到行内元素时，二是访问表格任意部分的任意属性时。语法错误。原因可能是代码中少了一个分号，或者花括号前后不对应，或者引用的外部 JavaScript 文件没有返回代码。系统无法找到指定资源。IE 有对 URL 最长不能超过 2083 个字符的限制。

17.5　小结　

第18章　JavaScript与XML　
18.1　浏览器对XML DOM的支持　
18.2　浏览器对XPath的支持　
18.3　浏览器对XSLT的支持  
18.4　小结　

# 第19章 E4X　

E4X是以ECMA-357标准的形式发布的对ECMAScript的一个扩展，目的是为了操作XML数据提供与标准ECMAScript更相近的语法。

19.2 一般用法 

19.3 其他变化 

19.4 全面启用E4X

19.5 小结

# 第20章 JSON　

JSON 是 JavaScript 的一个严格的子集，利用了 JavaScript 中的一些模式来表示结构化数据。

## 20.1 语法 

JSON 的语法可以表示以下三种类型的值。  

- 简单值。最简单的 JSON 数据形式就是简单值。可以在 JSON 中表示字符串、数值、布尔值和 null 。与 JavaScript 不同的是，JSON 字符串必须使用双引号。在实际应用中， JSON 更多地用来表示更复杂的数据结构，而简单值只是整个数据结构中的一部分。

- 对象。对象作为一种复杂数据类型，表示的是一组无序的键值对儿。而每个键值对儿中的值可以是简单值，也可以是复杂数据类型的值。JSON 中的对象要求给属性加引号。JSON 对象有两个地方不一样。首先，没有声明变量（ JSON 中没有变量的概念）。其次，没有末尾的分号（因为这不是 JavaScript 语句，所以不需要分号）。  

- 数组。数组也是一种复杂数据类型，表示一组有序的值的列表。可以通过索引来访问其中的值。数组的值也可以是任意类型——简单值、对象或数组。JSON数组也没有变量和分号。把数组和对象结合起来，可以构成更复杂的数据集合。

JSON 不支持变量、函数或对象实例，它就是一种表示结构化数据的格式，虽然与 JavaScript 中表示数据的某些语法相同，但它并不局限于 JavaScript 的范畴。  

## 20.2 解析与序列化

JSON 之所以流行，除了拥有与JavaScript类似的语法，更重要的原因是，可以把 JSON 数据结构解析为有用的 Javascript 对象，而 XML 数据结构要解析成 DOM 文档而且从中提取数据。

`eval()`函数。早期的 JSON 解析器基本上就是使用 JavaScript 的`eval()`函数。由于 JSON 是 JavaScript 语法的子集，因此`eval()`函数可以解析、解释并返回 JavaScript 对象和数组。ES5 对解析 JSON 的行为进行规范，定义了全局对象 JSON。

JSON对象有两个方法：`stringify()`和`parse()`，在最简单的情况下，`stringify()`方法把 JavaScript 对象序列化为 JSON 字符串；`parse()`方法把 JSON 字符串解析为原生 JavaScript 值。

在序列化 JavaScript 对象时，所有函数及原型成员都会被有意忽略，不体现在结果中，值为 undefined 的任何属性也都会被跳过，结果中最终都是值为有效 JSON 数据类型的实例属性。

`JSON.stringify()`序列化选项。除了要序列化的 JavaScript 对象外，还可以接收另外两个参数，这两个参数用于指定以不同的方式序列化 JavaScript 对象。第一个参数是个过滤器（数组或函数），第二个参数是一个选项，表示是否在 JSON 字符串中保留缩进。

- 过滤结果，如果过滤器是数组，那么`JSON.Stringify()`的结果中将只包含数组中列出的属性。
- 如果过滤器是函数，那么传入的函数接收两个参数：属性名和属性值。为了改变序列化对象的结果，函数返回的值就是相应键的值。

```JavaScript
var book={
	title:"Professional JavaScript",
	authors:[
		"Nicholas C. Zakas"
	],
	edition:3,
	year:2011
};
var jsonText=JSON.stringify(book,function(key,value){
	switch(key){
		case "authors":
			return value.join(",");
		case "year":
			return 5000;
		case "edition":
			return undefined;
		default:
			return value;
	}
});

/*序列化后的JSON字符串如下所示*/
{"title":"Professional JavaScript","authors":"Nicholas C.Zakas","year":5000}
```

- 字符串缩进，如果这个参数是一个数值，那它表示的是每个级别缩进的空格数，同时插入换行符以提高可读性。
- 如果缩进参数是一个字符串而非数值，则这个字符串将在JSON字符串中被用作缩进字符。

```JavaScript
var book={
	title:"Professional JavaScript",
	authors:[
		"Nicholas C. Zakas"
	],
	edition:3,
	year:2011
};
var jsonText=JSON.stringify(book,null,4);

//保存在jsonText中的字符串如下所示：
{
	"title":"Professional JavaScript",
	"authors":[
		"Nicholas C. Zakas"
	],
	"edition":3,
	"year":2011
}
```

`toJSON()`方法。有时候，`JSON.Stringify()`还是不能满足对某些对象进行自定义序列化的需求，在这个情况下，可以给对象定义`toJSON()`方法。该返回其自身的 JSON 数据格式。对象将被序列化为一个简单的字符串而非对象，可以让`toJSON()`方法返回任何值，它都能正常工作。`toJSON()`可以作为函数过滤器的补充。

```JavaScript
var book={
	title:"Professional JavaScript",
	authors:[
		"Nicholas C. Zakas"
	],
	edition:3,
	year:2011，
	toJSON:function(){
		return this.title;
	}
};
var jsonText=JSON.stringify(book);  // "Professional JavaScript" 
```

`JSON.parse()`解析方法也可以接收另一个参数，该参数是一个函数，将在每个键值对儿上调用，这个函数被称为还原函数，与序列化方法中的过滤函数的签名相同，都接收两个参数，一个键和一个值，而且都需要返回一个值。如果还原函数返回 undefined，则表示要从结果中删除相应的键；如果返回其他值，则将该值插入到结果中。  

```JavaScript
var book = {
  "title": "Professional JavaScript",
  "authors": [
    "Nicholas C. Zakas"
  ],
  edition: 3,
  year: 2011,
  releaseDate: new Date(2011, 11, 1)
};
var jsonText = JSON.stringify(book);
var bookCopy = JSON.parse(jsonText, function(key, value){
  if (key == "releaseDate"){
    return new Date(value);
  } else {
    return value;
  }
});
alert(bookCopy.releaseDate.getFullYear());
```

20.3　小结　

# 第21章 Ajax与Comet

Ajax，是对 Asynchronous Javascript+XML 的简写，这个技术能够向服务器请求额外的数据而无需卸载页面，会带来更好的用户体验。

Ajax 技术的核心是 XMLHttpRequest 对象，简称 XHR ，它为向服务器发送请求和解析服务器响应提供了流畅的接口，能够以异步方式从服务器取得更多信息。但 Ajax 通信与数据格式无关，这种技术就是无需刷新页面即可从服务器取得数据，但不一定是 XML 数据。

## 21.1 XMLHttpRequest对象　

在一般的浏览器中创建 XHR 对象，直接使用 XMLHttpRequest 构造函数，这便是原生的XHR实现。如果还要支持 IE 的早期版本，那么则可以在这个`createXHR()`函数中加入对原生 XHR 对象的支持。

```JavaScript
function createXHR() {
  if (typeof XMLHttpRequest != "undefined") {
    return new XMLHttpRequest();
  } else if (typeof ActiveXObject != "undefined") {
    if (typeof arguments.callee.activeXString != "string") {
      var versions = [
          "MSXML2.XMLHttp.6.0",
          "MSXML2.XMLHttp.3.0",
          "MSXML2.XMLHttp"
        ],
        i,
        len;

      for (i = 0, len = versions.length; i < len; i++) {
        try {
          new ActiveXObject(versions[i]);
          arguments.callee.activeXString = versions[i];
          break;
        } catch (ex) {
          //跳过
        }
      }
    }

    return new ActiveXObject(arguments.callee.activeXString);
  } else {
    throw new Error("No XHR object available.");
  }
}
var xhr = createXHR();
```

XHR 的用法。在使用 XHR 对象时，要调用的第一个方法是`open()`，它接受3个参数：要发送的请求类型（ "get"、"post" 等）、请求的URL和表示是否异步发送请求的布尔值。其中 URL 相对于执行代码的当前页面（当然也可以使用绝对路径），调用`open ()`方法并不会真正发送请求，而只是启动一个请求以备发送。

```javascript
xhr.open("get", "example.php", false);
```

调用XHR对象的`send()`方法，该方法接收一个参数，即要作为请求主题发送的数据。如果不需要通过请求主题发送数据，则必须传入 null，因为这个参数对有些浏览器来说是必须的，通过调用，请求就会被分派到服务器。

```javascript
xhr.send(null);
```

收到响应后，响应的数据会自动填充XHR对象的属性，相关的属性简介如下。 

- responseText：作为响应主体被返回的文本。 
- responseXML：如果响应的内容类型是 "text/xml" 或 "application/xml" ，这个属性中将保存包含着响应数据的 XML DOM 文档。 
- status：响应的 HTTP 状态。 
- statusText： HTTP 状态的说明。  

在收到响应后，第一步是检查 status 属性（HTTP状态代码200为成功的标志），以确定响应已经成功返回。状态代码为304表示请求的资源并没有被修改，可以直接使用浏览器中缓存的版本。如果 responseText 属性的内容已经就绪，而且在内容类型正确的情况下，responseXML 也应该能够访问了。

```javascript
xhr.open("get", "example.txt", false);
xhr.send(null);
if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
  alert(xhr.responseText);
} else {
  alert("Request was unsuccessful: " + xhr.status);
}
```

发送异步请求，可以检测 XHR 对象的 readyState 属性，该属性表示请求/响应过程的当前活动阶段，属性值0代表未初始化，1代表启动，2代表发送，3代表接收，4代表完成。只要该属性值变化，都会触发一次 readyStatechange 事件。

另外，在接收到响应之前还可以调用`abort()`方法取消异步请求。调用这个方法后， XHR 对象会停止触发事件，而且也不再允许访问任何与响应有关的对象属性。  

```javascript
var xhr = createXHR();	// createXHR () 是兼容性创建 XMLHttpRequest 的方法
xhr.onreadystatechange = function(){
	if (xhr.readyState == 4){
		if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
			alert(xhr.responseText);
		} else {
		alert("Request was unsuccessful: " + xhr.status);
		}
	}
};
xhr.open("get", "example.txt", true);
xhr.send(null);

xhr.abort();
```

HTTP 头部信息。每个 HTTP 请求和响应都会带有相应的头部信息，XHR 对象也提供了操作这两种头部（即请求头部和响应头部）信息的方法。默认情况下，在发送 XHR 请求的同时，还会发送下列头部信息。

- Accept：浏览器能够处理的内容类型。
- Accept-Charset：浏览器能够显示的字符集。
- Accept-Encoding：浏览器能够处理的压缩编码。
- Accept-Language：浏览器当前设置的语言。
- Connection：浏览器与服务器之间连接的类型。
- Cookie：当前页面设置的任何 Cookie。
- Host：发出请求的页面所在的域 。
- Referer：发出请求的页面的 URI。注意， HTTP 规范将这个头部字段拼写错了，而为保证与规范一致，也只能将错就错了。（这个英文单词的正确拼法应该是 referrer。）
- User-Agent：浏览器的用户代理字符串。

XHR 对象提供了操作每个 HTTP 请求和响应的这两种头部信息的方法。使用`setRequestHeader()` 方法可以设置自定义的请求头部，这个方法接收两个参数：头部字段的名称和头部字段的值。要成功发送请求头部信息，必须在调用`open()`方法和`send()`方法之间调用`setRequestHeader()`方法。调用 XHR 对象的`getResponseHeader()`方法并传入头部字段名称，可以取得相应的响应头部信息，而调用`getAllResponseHeaders()`方法可以取得一个包含所有头部信息的长字符串。在服务器端，也可以利用头部信息向浏览器发送额外的、结构化的数据。

GET 是最常见的请求类型，最常用于向服务器查询某些信息。必要时，可以将查询字符串参数追加到URL的末尾，以便将信息发送给服务器。对 XHR 而言，位于传入`open()`方法的 URL 末尾的查询字符串必须经过正确的编码才行。使用`encodeURIComponent()`进行编码，而且所有名-值对儿都必须由和号`（&）`分隔。

POST 请求。使用频率仅次于 GET 的是 POST 请求，通常用于向服务器发送应该被保存的数据。POST请求应该把数据作为请求的主题提交，而 GET 请求请求传统上不是这样。POST请求的主体可以包含非常多的数据，而且格式不限。在`open()`方法第一个参数的位置传入 "post" ，就可以初始化一个 POST 请求 。发送 POST 请求的第二步就是向`send()`方法中传入某些数据，数据可以是 XML DOM 文档，也可以是字符串，经序列化之后将作为请求主体被提交到服务器。如果需要像 HTML 表单那样 POST 数据，需要使用`setRequestHeader()`来添加 HTTP 头。然后在`send()`方法中规定发送的数据： 

```javascript
function submitData() {
  var xhr = createXHR();
  xhr.onreadystatechange = function() {
    if (xhr.readyState == 4) {
      if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
        alert(xhr.responseText);
      } else {
        alert("Request was unsuccessful: " + xhr.status);
      }
    }
  };
  xhr.open("post", "postexample.php", true);
  xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
  var form = document.getElementById("user-info");
  xhr.send(serialize(form));  // serialize() 为定义表单序列化方法
}
```

如果不设置 Content-Type 头部信息，那么发送给服务器的数据就不会出现在`$_POST`超级全局变量中。这时候，要访问同样的数据，就必须借助`$HTTP_RAW-POST-DATA`。

## 21.2 XMLHttpRequest 2级

FormData实例。FormData 类型为序列化表单以及创建与表单格式相同的数据（用于通过 XHR 传输）提供了便利。其中 FormData 的实例对象有 `append()` 方法，接收两个参数：键和值，分别对应表单字段的名字和字段中包含的值。

```JavaScript
var data = new FormData();
data.append("name", "Nicholas");
```

而通过向 FormData 构造函数中传入表单元素，也可以用表单元素的数据预先向其中填入键值对儿。因此，创建了 FormDate 的实例后，可以将它直接传给 XHR 的`send()`方法。使用 FormData 的方便之处体现在不必明确地在 XHR 对象上设置请求头部。XHR 对象能够识别传入的数据类型是 FormData 的实例，并配置适当的头部信息。

```javascript
var xhr = createXHR();
xhr.onreadystatechange = function(event) {
  if (xhr.readyState == 4) {
    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
      alert(xhr.responseText);
    } else {
      alert("Request was unsuccessful: " + xhr.status);
    }
  }
};

xhr.open("post", "postexample.php", true);
var form = document.getElementById("user-info");
xhr.send(new FormData(form));
```

超时设置。timeout 属性表示请求在等待响应多少毫秒之后就停止，如果在规定时间内浏览器没有接收到响应，那么就会触发 timeout 时间，进而调用 ontimeout 时间处理程序。`overrideMimeType()`方法用于重写 XHR 响应的 MIME 类型。

```javascript
// timeout
xhr.open("get", "timeout.php", true);
xhr.timeout = 1000; //将超时设置为 1 秒钟（仅适用于 IE8+）
xhr.ontimeout = function(){
	alert("Request did not return in a second.");
};
xhr.send(null);	
```

请求终止时，会调用 ontimeout 事件处理程序。但此时 redyState 可能已经变成4了，这意味着会调用 onreadystatechange 事件处理程序。可是，如果在超时终止请求之后再访问 status 属性，就会导致错误。为了避免浏览器报告错误，可以将检查 status 属性的语句封装在一个 try-catch 语句当中。

`overrideMimeType()`方法。该方法用于重写 XHR 响应的 MIME 类型。因为返回响应的 MIME 类型决定了 XHR 对象如何处理它，所以提供一种方法能够重写服务器返回的 MIME 类型是很有用的。

比如，服务器返回的 MIME 类型是 text/plain，但数据中实际包含的是 XML。根据 MIME 类型，即使数据是 XML，responseXML 属性中仍然是 null，通过调用`overrideMimeType()`方法就可以保证把响应头当做 XML 而非纯文本来处理。调用该方法必须在`send()`方法之前，才能保证重写相应的 MIME 类型。

```JavaScript
var xhr = createXHR();
xhr.open("get", "text.php", true);
xhr.overrideMimeType("text/xml");
xhr.send(null);
```

## 21.3 进度事件　

Progress Events 规范定义了与客户端服务器通信有关的事件。有以下 6 个进度事件。 

- loadstart：在接收到响应数据的第一个字节时触发。 
- progress：在接收响应期间持续不断地触发。 
- error：在请求发生错误时触发。 
- abort：在因为调用`abort()`方法而终止连接时触发。 
- load：在接收到完整的响应数据时触发。 
- loadend：在通信完成或者触发 error、 abort 或 load 事件后触发。  

每个请求都从触发 loadstart 事件开始，接下来是一或多个 progress 事件，然后触发 error 、 abort 或 load 事件中的一个，最后以触发 loadend 事件结束。

load 事件。Firefox 实现中引入了 load 事件，用以替代 readystatechange 事件。响应接收完毕后将触发 load 事件，因此也就没有必要去检查 readyState 属性了。而 onload 事件处理程序会接收到一个 event 对象，其 target 属性就指向 XHR 对象实例，因而可以访问到 XHR 对象的所有方法和属性。如果遇到不支持的浏览器，还是要使用 XHR 对象变量。

只要浏览器接收到服务器的响应，不管其状态如何，都会触发 load 事件。而这意味着你必须要检查 status 属性，才能确定数据是否真的已经可用了。

progress 事件。progress 事件会在浏览器接收新数据期间周期性地触发，而 onprogress 事件处理程序会接收到一个 event 对象，其 target 属性时 XHR 对象，但包含着三个额外的属性：表示进度信息是否可用的布尔值 lengthComputable 、表示已经接收的字节数 position 和表示根据 content-Length 响应头部确定的预期字节数的 totalSize 。

```JavaScript
// 进度指示器
var xhr = createXHR();
xhr.onload = function(event) {
  if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
    alert(xhr.responseText);
  } else {
    alert("Request was unsuccessful: " + xhr.status);
  }
};
xhr.onprogress = function(event) {
  var divStatus = document.getElementById("status");
  if (event.lengthComputable) {
    divStatus.innerHTML =
      "Received " + event.position + " of " + event.totalSize + " bytes";
  }
};
xhr.open("get", "altevents.php", true);
xhr.send(null);

```

为确保正常执行，必须在调用 `open()` 方法之前添加 onprogress 事件处理程序。在上面代码中，每次触发 progress 事件，都会以新的状态信息更新 HTML 元素的内容。如果响应头部中包含 Content-Length 字段，那么也可以利用此信息来计算从响应中已经接收到的数据的百分比。

## 21.4 跨源资源共享　

通过 XHR 实现 Ajax 通信的一个主要限制，来源于跨域安全策略。默认情况下，XHR 对象只能访问与包含它的页面位于同一个域中的资源。这种安全策略可以预防某些恶意 行为。但是，实现合理的跨域请求对开发某些浏览器应用程序也是至关重要的。

CORS 跨资源共享定义了在必须访问跨资源时，浏览器与服务器应该如何沟通。CORS 背后的基本思想，就是使用自定义的 HTTP 头部让浏览器与服务器进行沟通，从而决定请求或响应是应该成功，还是应该失败。  

比如一个简单的使用 GET 或 POST 发送的请求，它没有自定义的头部，而主体内容是 text/plain。在发送该请求时，需要给它附加一个额外的 Origin 头部，其中包含请求页面的源信息（协议、域名和端口），以便服务器根据这个头部信息来决定是否给予响应。下面是 Origin 头部的一个示例： 

```
Origin: http://www.nczonline.net
```

如果服务器认为这个请求可以接受，就在 Access-Control-Allow-Origin 头部中回发相同的源信息（如果是公共资源，可以回发"*"）。例如： 

```
Access-Control-Allow-Origin: http://www.nczonline.net 
```

如果没有这个头部，或者有这个头部但源信息不匹配，浏览器就会驳回请求。正常情况下，浏览器会处理请求。注意，请求和响应都不包含 cookie 信息。  

IE 对 CORS 的实现。IE8 引入了XDR 类型，这个对象与 XHR 类似，但能实现安全可靠的跨域通信。XDR 对象的使用方法与 XHR 对象非常相似，也是创建一个 XDomainRequest 的实例，调用`open()`，再调用`send()`方法进行异步请求。

其他浏览器对 CORS 的实现。它们可以**通过 XMLHttpRequest 对象实现了对 CORS 的原生支持**。在尝试打开不同来源的资源时，无需额外编写代码就可以触发这个行为。要请求位于另一个域中的资源，使用标准的 XHR 对象并在`open()`方法中传入绝对 URL 即可。

```JavaScript
var xhr = createXHR();
xhr.onreadystatechange = function() {
  if (xhr.readyState == 4) {
    if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304) {
      alert(xhr.responseText);
    } else {
      alert("Request was unsuccessful: " + xhr.status);
    }
  }
};
xhr.open("get", "http://www.somewhere-else.com/page/", true);
xhr.send(null);
```

与 IE 中的 XDR 对象不同，通过跨域 XHR 对象可以访问 status 和 statusText 属性，而且还支持同步请求。但是跨域 XHR 对象也有一些限制，但为了安全这些限制是必须的

- 不能使用 `setRequestHeader()`设置自定义头部。
- 不能发送和接收 cookie。
- 调用 `getAllResponseHeaders()`方法总会返回空字符串。

由于无论同源请求还是跨源请求都使用相同的接口，因此对于本地资源，最好使用相对 URL，在访问远程资源时再使用绝对 URL。这样做能消除歧义，避免出现限制访问头部或本地 cookie 信息等问题。

Preflighted Requests。CORS 通过一种叫做 Preflighted Requests 透明服务器验证机制**支持开发人员使用自定义的头部、GET或POST之外的方法**，以及不同类型的主题内容。在使用高级选项来发送请求时，就会向服务器发送一个 Preflight 请求，这种请求使用 OPTIONS 方法，发送下列头部。

- Origin：与简单的请求相同。
- Access-Control-Request-Method：请求自身使用的方法。
- Access-Control-Request-Headers：（可选）自定义的头部信息，多个头部以逗号分隔。

以下是一个带有自定义头部 NCZ 的使用 POST 方法发送的请求。

```
Origin: http://www.nczonline.net
Access-Control-Request-Method: POST
Access-Control-Request-Headers: NCZ
```

发送这个请求后，服务器可以决定是否允许这种类型的请求。服务器通过在相应中发送如下头部与浏览器进行沟通。

- Access-Control-Allow-Origin：与简单的请求相同。
- Access-Control-Allow-Methods：允许的方法，多个方法以逗号分隔。
- Access-Control-Allow-Headers：允许的头部，多个头部以逗号分隔。
- Access-Control-Max-Age：应该将这个 Preflight 请求缓存多长时间（以秒表示）。

Preflight 请求结束后，结果将按照响应中指定的时间缓存起来。而为此付出的代码知识第一次发送这种请求时会多一次 HTTP 请求。

带凭借的请求。默认情况下，跨域请求不提供凭据，包括 cookie 、 HTTP 认证及客户端 SSL 证明等，但通过将 withCredentials 属性设置为 true ，可以指定某个请求应该发送凭据。如果服务器接受带凭据的请求，会用下面的 HTTP 头部来响应。

```
Access-Control-Allow-Credentials: true
```

如果发送的是带凭据的请求，但服务器的响应中没有包含这个头部，那么浏览器就不会把响应交给 JavaScript。另外，服务器还可以在 Preflight 响应中发送这个 HTTP 头部，表示允许源发哦送带凭据的请求。

跨浏览器的 CORS。即使浏览器对 CORS 的支持程度并不都一样，但所有浏览器都支持简单的（非 Preflight 和不带凭据的）请求。但有必要实现一个跨浏览器的方案，检测 XHR 是否支持 CORS 的最简单方式，就是检查是否存在 withCredentials 属性，再结合检测 XDomainRequest 对象是否存在，就可以兼顾所有浏览器了。

## 21.5 其他跨域技术　

在 CORS 出现以前，开发人员想出一些办法，利用 DOM 中能够执行跨域请求的功能，在不依赖 XHR 对象的情况下也能发送某种请求。虽然 CORS 技术已经无处不在，但这些办法仍然被广泛使用，毕竟这样不要修改服务器端代码。

图像 Ping。这种跨域请求技术是使用`<img>`标签。动态创建图像经常用于图像Ping，它是与服务器进行简单、单向的跨域通信的一种方式。请求的数据是通过查询字符串形式发送的，而响应可以是任意内容，但通常是像素图或 204 响应。通过图像Ping，浏览器得不到任何具体的数据，但通过侦听 load 和 error 事件，它能知道响应是什么时候接收到的。图像 Ping 最常用于跟踪用户点击页面或动态广告曝光次数。图像 Ping 有两个主要的缺点，一是只能发送 GET 请求，二是无法访问服务器的响应文本。  

```javascript
var img = new Image();
img.onload = img.onerror = function(){
	alert("Done!");
};
img.src = "http://www.example.com/test?name=Nicholas";
```

JSONP 是 JSON with padding 的简写，是应用 JSON 的一种新方法。JSONP 由两部分组成：回调函数和数据。回调函数是当响应到来时应该在页面中调用的函数，回调函数的名字一般都是在请求中指定的，而数据就是传入回调函数中的 JSON 数据。JSONP 是通过动态`<script>`元素来使用的，使用时可以为 src 属性指定一个跨域 URL。这里的`<script>`元素与`<img>`元素类似，都有能力不受限制地从其他域加载资源。因为 JSONP 是有效的 JavaScript 代码，所以在请求完成后，即在 JSONP 响应加载到页面中以后，就会立即执行。

```javascript
function handleResponse(response){
	alert("You’ re at IP address " + response.ip + ", which is in " +
		response.city + ", " + response.region_name);
}
var script = document.createElement("script");
script.src = "http://freegeoip.net/json/?callback=handleResponse";
document.body.insertBefore(script, document.body.firstChild);	
```

JSONP 之所以在开发人员中极为流行。主要原因是它非常简单易用。与图像 Ping 相比，它的优点在于能够直接访问响应文本，支持在浏览器与服务器之间双向通信。不过，JSONP 也有两点不足。

- JSONP 从其他域中加载代码执行，如果其他域不安全，很可能会在响应中带一些恶意代码。
- 要确定 JSONP 请求是否失败并不容易，虽然 HTML5 给`<script>`元素新增了一个 onerror 事件处理程序。但 HTML5 得到浏览器支持是缓慢的。

Comet 指的是一种更高级的 Ajax 技术，经常也有人称为服务器推送。Ajax 是一种从页面向服务器请求数据的技术，而 Comet 则是一种服务器向页面推送数据的技术。有两种实现 Comet 的方式：长轮询和流。长轮询是传统轮询（短轮询）的一个翻版，浏览器都要在接收数据之前，先发起对服务器的连接，短轮询是服务器立刻发送响应，而长轮询是等待发送响应。HTTP 流在页面的整个生命周期内只使用一个 HTTP 连接，服务器保持连接打开，周期性地向浏览器发送数据。

SSE 服务器发送事件是围绕只读 Comet 交互退出的 API 或者模式。SSE API 用于创建到服务器的单向链接，服务器通过这个连接可以发送任意数量的数据。要预订新的事件流，首先要创建一个新的 EventSource 对象，并传进一个入口点。EventSource 的实例有一个 readyStatus 属性，值为0表示正连接到服务器，值为1表示打开了连接，值为2表示关闭了连接。另外还有三个事件，在建立连接时触发的 open 事件、在从服务器接收到新事件时触发的 message 事件、在无法建立连接时触发的 error 事件。服务器发回的数据以字符串形式保存在 event.data 中。默认情况下， EventSource 对象会保持与服务器的活动连接。事件流。所谓的服务器事件会通过一个持久的 HTTP 响应发送，这个响应的 MIME 类型是 text/eventstream。响应的格式是纯文本。

Web Sockets 的目标是在一个单独的持久连接上提供全双工、双向通信。Web Sockets 使用了自定义的协议，好处是在客户端和服务器之间发送非常少量的数据，而不必担心 HTTP 那样字节级的开销。要创建 Web Socket ，先实例一个WebSocket 对象并传入要连接的 URL ，如果要关闭连接，可以在任意时候调用`close()`方法。如果要向服务器发送数据，使用`send()`方法并传入任意字符串，因为只能通过连接发送纯文本数据，所以对于复杂的数据结构，在通过连接发送之前必须进行序列化。当服务器向客户端发来小心时，WebSocket 对象就会触发 message 事件，返回的数据保存在 event.data 属性中。

## 21.6 安全

首先，可以通过 XHR 访问的任何 URL 也可以通过浏览器或服务器访问。对于未被授权系统有权访问某个资源的情况，我们称之为 XSRF 跨站点请求伪造。为确保通过XHR访问的URL安全，通行的做法就是验证发送请求者是否有权限访问相应的资源。

XHR 对象也提供了一些安全机制，虽然表面上看可以保证安全，但实际上却相当不可靠。实际上，前面介绍的 `open()` 还能再接收两个参数：要随请求一起发送的用户名和密码。带有这两个参数的请求可以通过 SSL 发送给服务器上的页面。

21.7　小结　

第22章 高级技巧　

22.1　高级函数　

22.2　防篡改对象　

22.3　高级定时器　

22.4　自定义事件　

22.5　拖放　

22.6　小结　

# 第23章 离线应用与客户端存储　

## 23.1 离线检测 

HTML5定义了一个navigator.onLine属性来确定设备是在线还是离线，属性值为true则表示设备能够上网。为了更好地确定网络是否可用，还定义了两个事件：online和offline，当网络从离线变为在线或者从在线变为离线时，分别触发这两个事件，这两个事件在window对象上触发。

## 23.2 应用缓存 

HTML5的应用缓存，简称为appcache，是专门为开发离线Web应用而设计的。要向在浏览器的缓存中分出一块缓存区，然后保存数据，可以使用一个描述文件，列出要下载和缓存的资源。要将描述文件与页面关联起来，可以在`<html>`中的mainfest属性中指定这个文件的路径。虽然应用缓存的意图是确保离线时资源可用，但也有相应的JavaScript API让你知道它都在做什么，这个API的核心是applicationCache对象，这个对象有一个status属性、属性的值是常量，表示应用缓存的如下状态：无缓存0、闲置1、检查中2、下载中3、更新完成4、废弃5。应用缓存还有很多相关的事件，表示其状态的改变。一般来说，这些事件会随着页面加载按上述顺序触发，不过调用update()方法也可以手工干预，让应用缓存为检查更新而出发上述事件。如果触发了updateready事件，则说明新版本的应用缓存已经可用，而此时你需要调用swapCache()来启用新应用缓存。

## 23.3 数据存储 

HTTP Cookie，通常直接叫做cookie，最初是在客户端用于存储会话信息的。cookie在性质上是绑定在特定的域名下的。每个域的cookie总数是有限的，不过浏览器之间各不同。当超过单个域名限制之后还要再设置cookie，浏览器就会清除以前设置的cookie。浏览器中对于cookie的尺寸也有限制。最好将整个cookie长度限制不超过4095。cookie由浏览器保存的名称、值、域、路径、失效时间和安全标志这几块信息构成。BOM的document.cookie属性的独特之处在于它会因为使用它的方式不同而变现出不同的行为。当用来获取属性值时，它返回当前页面可用的所有cookie的字符串，一系列由分号隔开的名值对儿。当用于设置值的时候，它可以设置为一个新的cookie字符串，并被解释和添加到现有的cookie集合中。设置cookie的格式与Set-Cookie头中使用的格式一样，多个参数中只有cookie的名字和值是必须的。字cookie是存在在单个cookie中的更小段的数据，使用cookie值来存储多个名称值对儿。获取子cookie的方法有两个：get()和getAll()，get()方法获取单个子cookie的值，接收两个参数：cookie的名字和子cookie的名字。而SubCookieUtil.getAll()方法和COokieUtil.get()在解析cookie值的方式上非常相似，区别在于cookie的值并非立即解码。删除子cookie的方法是获取包含在某个cookie中的所有子cookie，然后仅删除需要删除的那个子cookie，然后再将余下的子cookie的值保存在cookie的值。

IE用户数据。微软通过一个自定义行为引入了持久化用户数据的概念，用户数据允许每个文档最多128KB数据，每个域名最多1MB数据。具体操作，使用CSS在某个元素上指定userData行为，接着使用setAttributes()方法在上面保存数据，还可以调用save()方法指定数据空间的名称，在下一次页面载入之后就可以使用load()方法指定同样的数据空间名称来获取数据。

Web Storage主要目的有两个：提供一种在cookie之外存储会话数据的途径，提供一种存储大量可以跨会话存在的数据的机制。Storage类型提供最大的存储空间（因浏览器而异）来存储明值对儿。sessionStorage对象来存储特定于某个会话的数据。globalStorage对象的目的是跨越会话存储数据，但也有特定的访问限制，要使用这个对象，首先要指定哪个域中可以访问该数据，然后通过方括号标记使用属性来实现。localStorage对象在HTML5规范中取代了globalStorage，但是不能给localhostStorage指定任何访问规则，规则事先就要设定好。对Storage对象进行任何修改，都会在文档上出发Storage事件。这个事件的event对象有domain、key、newValue和oldValue属性。

IndexedDB全称是Indexed Database API，是在浏览器中保存结构化数据的一种数据库。IndexedDB设计的操作完全是异步进行的。在得到完整支持的情况下，IndexedDB将是一个uzoweiAPI宿主的全局对象。它的最大特色是使用对象保存数据，而不是使用表来保存数据。调用IndexedDB.open()会返回一个IDBRequest对象，在这个对象上可以添加到onerror和onsuccess事件处理程序。默认情况下，IndexedDB数据库是没有版本号的，可以调用setVersion()方法传入以字符串形式表示的版本号进行指定，同样这个方法也会返回一个请求对象，需要你再指定事件处理程序。使用createObjectStore()方法来构建对象存储空间，第一个参数是全局唯一的键，第二个参数中中的keyPath属性时对象的一个属性，即存储空间的键，另外还有属性值。可以使用add()或put()方法来向其中添加数据。如果添加已经包含键值相同的对象时，add()会返回错误，put()则会重写原有对象。操作数据都是通过事务来完成的，在数据库对象上调用transaction()方法可以创建事务。如果没有参数，就只能通过事务来读取数据库中保存的对象。第一个参数表示访问的一个或多个对象，第二个参数表示访问方式。取得了事务的索引后，使用objectStore()方法并传入存储空间的名称，就可以访问特定的存储空间。使用事务可以直接通过以至的键检索单个对象，而需要检索多个对象则需要在事务内部创建游标。游标就是一指向结果集的指针。与传统数据库查询不同，游标并不提前收集结果。游标指针会先指向结果中的第一项，在接到查找下一项的指令时，才会指向下一项。调用openCursor()方法可以创建游标。使用游标也可以更新个别的记录，调用update()可以用指定的对象更新当前游标的value。对于某些数据，可能需要为一个对象存储空间指定多个键。可以考虑创建索引，首先引用对象存储空间，然后调用createIndex()方法。并发问题。只有当浏览器中仅有一个标签页使用数据库的情况下，调用setVersion()才能完成操作。每次成功打开数据库，都应该指定onversionchange事件处理程序。IndexedDB数据库只能由同源页面操作，占用的磁盘空间也有限制。

23.4 小结 

第24章 最佳实践 

24.1 可维护性

24.2 性能

24.3 部署

24.4 小结

第25章 新兴的API

25.1 requestAnimationFrame() 

25.2 Page Visibility API 

25.3 Geolocation API 

25.4 File API 

25.5 Web计时 

25.6 Web Workers 

25.7 小结

附录A ECMAScript Harmony 

附录B 严格模式

附录C JavaScript库

附录D JavaScript工具
​	
​	
​	

