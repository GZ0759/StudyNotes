> JavaScript权威指南第6版  
> David Flanagan 著  
> 淘宝前端团队 译  
> 2012 年 4 月第 1 版  
> [试读章节](https://book.2cto.com/201210/7006.html)
> [博客园](https://www.cnblogs.com/ahthw/category/652668.html)

# 前言
# 第1章 JavaScript概述

JavaScript 是面向 Web 的编程语言。绝大多数网站都适用了 JavaScript ，并且所有的现代 Web 浏览器——基于桌面系统、游戏机、平板电脑和智能手机的浏览器——均包含了 JavaScript 解释器。这使得 JavaScript 能够称得上史上使用最广泛的编程语言。JavaScript 也是前端开发工程师必须掌握的三种技能之一：描述网页内容的 HTML 、描述网页样式的 CSS 以及描述网页行为的 JavaScript 。

## 1.1 JavaScript语言核心

本节是 JavaScript 语言的一个快速概览，也是本书第一部分的快速概览。将关注 JavaScript 的基础知识，第二章讲解 JavaScript 注释、分号和 Unicode 字符集，第三章讲解 JavaScript 变量和赋值。

```js
// 变量是表示值的一个符号名字
// 变量是通过var关键字声明的
var x;    // 声明一个变量x

// 值可以通过等号赋值给变量
x = 0;    // 现在变量x的值为0
x     // => 0:通过变量获取其值

// JavaScript支持多种数据类型
x = 1;    // 数字
x = 0.01;   // 整数和实数共用一种数据类型
x = "hello world";  // 由双引号内的文本构成的字符串
x = 'JavaScript';  // 单引号内的文本同样构成字符串
x = true;   // 布尔值
x = false;   // 另一个布尔值
x = null;   // null是一个特殊的值，意思是"空"
x = undefined;  // undefined和null非常类似
```

JavaScript 中两个非常重要的数据类型是对象和数组。第六章介绍对象，第七章介绍数组，对象和数组在 JavaScript 中是很重要的。

```js
//JavaScript中的最重要的类型就是对象
//对象是名/值对的集合，或字符串到值映射的集合
var book = {    // 对象是由花括号括起来的
    topic: "JavaScript", // 属性"topic"的值是"JavaScript"
    fat: true   // 属性"fat"的值是true
};      // 右花括号标记了对象的结束

// 通过"."或" []"来访问对象属性
book.topic    // => "JavaScript"
book["fat"]    // => true:另外一种获取属性的方式
book.author = "Flanagan";  // 通过赋值创建一个新属性
book.contents = {};   // {} 是一个空对象，它没有属性

// JavaScript同样支持数组（以数字为索引的列表）
var primes = [2, 3, 5, 7];  // 拥有4个值的数组，由"["和"]"划定边界
primes[0]    // => 2: 数组中的第一个元素（索引为0）
primes.length   // => 4: 数组中的元素个数
primes[primes.length - 1]  // => 7:数组的最后一个元素
primes[4] = 9;   // 通过赋值来添加新元素
primes[4] = 11;   // 或通过赋值来改变已有的元素
var empty = [];   // [] 是空数组，它具有0个元素
empty.length    // => 0

// 数组和对象中都可以包含另一个数组或对象:
var points = [   // 具有两个元素的数组
 {x: 0, y: 0},  // 每个元素都是一个对象
 {x: 1, y: 1}
];
var data = {    // 一个包含两个属性的对象
    trial1: [[1, 2],[3, 4]], // 每一个属性都是数组
    trial2: [[2, 3],[4, 5]]  // 数组的元素也是数组
};
```

上段代码中通过方括号定义数组元素和通过花括号定义对象属性名和属性值之间的映射关系的语法称为初始化表达式（initalizer expression），第四章有专门的介绍。表达式是 JavaScript 中的一个短语，这个短语可以通过运算得出一个值。通过 “.” 和 “[]” 来引用对象属性或数组元素的值就构成一个表达式。

JavaScript 中最常见的表达式写法是想下面代码这样使用运算符（operator）。

```js
// 运算符作用于操作数，生成一个新的值
// 最常见的是算术运算符
3 + 2     // => 5: 加法
3 - 2     // => 1: 减法
3 * 2     // => 6: 乘法
3 / 2     // => 1.5: 除法
points[1].x - points[0].x  // => 1: 更复杂的操作数也能照常工作
"3" + "2"    // => "32": + 可以完成加法运算也可以作字符串连接

// JavaScript定义了一些算术运算符的简写形式
var count = 0;   // 定义一个变量
count++;    // 自增1
count--;    // 自减1
count += 2;    // 自增2：和"count = count + 2;"写法一样
count *= 3;    // 自乘3：和"count = count * 3;"写法一样
count     // => 6: 变量名本身也是一个表达式

// 相等关系运算符用来判断两值是否相等
// 不等、大于、小于运算符的运算结果是true或false
var x = 2, y = 3;   // 这里的 = 等号是赋值的意思，不是比较相等
x == y     // => false: 相等
x != y     // => true: 不等
x < y     // => true: 小于
x <= y     // => true: 小于等于
x > y     // => false: 大于等于
x >= y     // => false: 大于等于
"two" == "three"   // => false: 两个字符串不相等
"two" > "three"   // => true: "tw"在字母表中的索引大于"th"
false == (x > y)   // => true: false和false相等

// 逻辑运算符是对布尔值的合并或求反
(x == 2) && (y == 3)   // => true: 两个比较都是true，&&表示"与"
(x > 3) || (y < 3)   // => false: 两个比较不都是true，||表示"或"
!(x == y)    // => true: ! 求反
```

如果 JavaScript 中的“短语”是表达式的话，那么整个句子就称作语句（statement），第五章会详细讲解。在上述代码中，以分号结束的行均是一条语句（下面的代码中，会看到省略分号的多行语句）。实际上，语句和表达式之间有很多共同之处，粗略地将，表达式仅仅计算出一个值但并不作任何操作，它并不改变程序的运行状态。而语句并不包含一个值（或者说它包含的值我们并不关心），但它们改变程序的运算状态。在上文中已经见过变量声明语句和赋值语句。另一类是“控制结构”（control structure），比如条件判断和循环。

函数是带有名称（named）和参数的 JavaScript 代码段，可以一次定义多次调用。第八章会正式详细地讲解函数。

```js
// 函数是一段带有参数的JavaScript代码端，可以多次调用
function plus1(x) {   // 定义了名为plus1的一个函数，带有参数x
    return x+1;   // 返回一个比传入的参数大的值
}      // 函数的代码块是由花括号包裹起来的部分
plus1(y)      // => 4: y为3，调用函数的结果为 3+1

var square = function(x) {    // 函数是一种值，可以赋值给变量
    return x*x;     // 计算函数的值
};        // 分号标识了赋值语句的结束

square(plus1(y))     // => 16: 在一个表达式中调用两个函数
```

当将函数和对象合写在一起时，函数就变成了“方法”（method）：

```js
// 当函数赋值给对象的属性，我们称为
//  "方法"，所有的JavaScript对象都含有方法
var a = [];     // 创建一个空数组
a.push(1, 2, 3);    // push()方法向数组中添加元素
a.reverse();     // 另一个方法：将数组元素的次序反转

// 我们也可以定义自己的方法，"this"关键字是对定义方法
// 的对象的引用：这里的例子是上文中提到的包含两个点位置信息的数组
points.dist = function() {   // 定义一个方法用来计算两点之间的距离
    var p1 = this[0];   // 通过this获得对当前数组的引用
    var p2 = this[1];   // 并取得调用的数组前两个元素
    var a = p2.x - p1.x;   // X坐标轴上的距离
    var b = p2.y - p1.y;   // Y坐标轴上的距离
    return Math.sqrt(a * a +   // 勾股定理
    b * b);    // 用Math.sqrt()来计算平方根
};
points.dist()    // => 1.414: 求得两个点之间的距离
```

现在，给出一些控制语句的例子。

```js
// 这些JavaScript语句使用该语法包含条件判断和循环
// 使用了类似C、C++、Java和其他语言的语法
function abs(x) {    // 求绝对值的函数
    if (x >= 0) {    // if语句...
        return x;    // 如果比较结果为true则执行这里的代码.
    }      // 子句的结束.
    else {     // 当if条件不满足时执行else子句
        return - x;
    }      // 如果分支中只有一条语句，花括号是可以省略的
}       // 注意if/else中嵌套的return语句
function factorial(n) {   // 计算阶乘的函数
    var product = 1;    // 给product赋值为1
    while (n > 1) {    // 当()内的表达式为true时循环执行{}内的代码
        product *= n;   // "product = product * n; "的简写形式
        n--;     //  "n = n - 1; "的简写形式
    }      // 循环结束
    return product;    // 返回product
}
factorial(4)     // => 24: 1*4*3*2
function factorial2(n) {   // 实现循环的另一种写法
    var i, product = 1;   // 给product赋值为1
    for (i = 2; i <= n; i++)   // 将i从2自增至n
      product *= i;   // 循环体，当循环体中只有一句代码，可以省略{}
    return product;    // 返回计算好的阶乘
}
factorial2(5)    // => 120: 1*2*3*4*5
```

JavaScript 是一种面向对象的编程语言，但和传统的面向对象又有很大区别。第九章将详细讲解 JavaScript 中的面向对象编程。下面的代码展示了如何在 JavaScript 中定义一个类来表示 2D 平面几何中的点。这个类实例化的对象拥有一个名为 `r()` 的方法，用来计算点到原点的距离。

```js
// 定义一个构造函数以初始化一个新的Point对象
function Point(x, y) {   // 按照惯例，构造函数均以大写字母开始
    this.x = x;    // 关键字this指代初始化的实例
    this.y = y;    // 将函数参数存储为对象的属性
}       // 不需要return

// 使用new关键字和构造函数来创建一个实例
var p = new Point(1, 1); // 平面几何中的点 (1,1)

// 通过给构造函数的prototye对象赋值
// 来给Point对象定义方法
Point.prototype.r = function() {
    return Math.sqrt(   // 返回 x2 + y2 的平方根
    this.x * this.x +   // this指代调用这个方法的对象
    this.y * this.y);
};

// Point的实例对象p（以及所有的Point实例对象）继承了方法 r()
p.r()      // => 1.414...
```

第九章是第一部分的精华所在，后续的各章做了一些零星的延伸，将我们对 JavaScript 语言核心的探索带向尾声。第十章主要讲解了正则表达式的语法，并演示了如何使用这些“正则表达式”进行文本的模式匹配。第十一章介绍 JavaScript 语言核心的子集和超集。最后，在进入客户端 JavaScript 的内容之前，第十二章介绍两种在 Web 浏览器之外的两种 JavaScript 运行环境。

## 1.1 客户端JavaScript

第十三章是第二部分的第一章，该章介绍如何让 JavaScript 在 Web 浏览器中运行起来。从该章学到的最重要的内容是， JavaScript 代码可以通过`<script>`标签来嵌入到 HTML 文件中。

```html
<html>
<head>
<script src="library.js"></script> <!-- 引入一个JavaScript库-->
</head>
<body>
<p>This is a paragraph of HTML</p>
<script>
// 在这里编写嵌入到HTML文件中的JavaScript代码
</script>
<p>Here is more HTML.</P>
</body>
</html>
```

第十四章讲解 Web 浏览器脚本技术，并涵盖客户端 JavaScript 中的一些重要全局函数。

```html
<script>
function moveon() {
    // 通过弹出一个对话框来询问用户一个问题
    var answer = confirm("准备好了吗?");
    // 单击"确定"按钮，浏览器会加载一个新页面
    if (answer) window.location = "http://taobao.com";
}
// 在1分钟（6万毫秒）后执行定义的这个函数
setTimeout(moveon, 60000);
</script>
```

第十五章的内容更加务实——通过脚本来操纵 HTML 文档内容。它将展示如何选取特定的 HTML 元素、如何给 HTML 元素设置属性、如何修改元素内容，以及如何给文档添加新节点。

```js
// 在document中的一个指定的区域输出调试消息
// 如果document不存在这样一个区域，则创建一个
function debug(msg) {
    // 通过查看HTML元素id属性来查找文档的调试部分
    var log = document.getElementById("debuglog");

    // 如果这个元素不存在，则创建一个
    if (!log) {
        log = document.createElement("div");  // 创建一个新的<div>元素
        log.id = "debuglog";    // 给这个元素的HTML id赋值
        log.innerHTML = "<h1>Debug Log</h1>";  // 定义初始内容
        document.body.appendChild(log);  // 将其添加到文档的末尾
    }

    // 将消息包装在<pre>中，并添加至log中
    var pre = document.createElement("pre");  // 创建<pre>标签
    var text = document.createTextNode(msg);  // 将msg包装在一个文本节点中
    pre.appendChild(text);    // 将文本添加至<pre>
    log.appendChild(pre);    // 将<pre>添加至log
}
```

第十五章讲述 JavaScript 如何操纵 HTML 中定义 Web 内容的元素。第十六章讲诉如何使用 JavaScript 来进行 CSS 样式操作， CSS 样式定义了内容的展示方式。这通常会使用到 HTML 元素的 style 和 class 属性。

```js
function hide(e, reflow) {   // 通过JavaScript操纵样式来隐藏元素e
    if (reflow) {    // 如果第二个参数是true
        e.style.display = "none"  // 隐藏这个元素，其所占的空间也随之消失
    }
    else {     // 否则
        e.style.visibility = "hidden"; // 将e隐藏，但是保留其所占的空间
    }
}
function highlight(e) {   // 通过设置CSS类来高亮显示e
    // 简单地定义或追加HTML类属性
    // 这里假设CSS样式表中已经有"hilite"类的定义
    if (!e.className) e.className = "hilite";
    else e.className += " hilite";
}
```

可以通过 JavaScript 来操控 Web 浏览器中的HTML内容和文档的CSS样式，同样，也可以通过事件处理程序（event handler）来定义文档的行为。事件处理程序是一个在浏览器中注册的 JavaScript 函数，当特定类型的事件发生时浏览器便调用这个函数。通常我们关心的事件类型是鼠标点击事件和键盘按键事件（在智能手机中则是各种触碰事件）。或者说，当浏览器完成了文档的加载，当用户改变窗口大小或当用户向 HTML表单元素中输入数据时便会触发一个事件。第17章详细描述如何定义、注册事件处理程序，以及在事件发生时浏览器是如何调用它们的。

定义事件处理程序最简单的方法是，给 HTML 的以“on”为前缀的属性绑定一个回调。当写一些简单的测试程序时，最实用的方法就是给“onclick”处理程序绑定回调。假定已经将上文中的`debug()`和`hide()`两个函数保存至名为debug.js和hide.js的文件中，那么就可以写一个简单的HTML测试文件，来给`<button>`元素的onclick属性指定一个事件处理程序：

```html
<script src="debug.js"></script>
<script src="hide.js"></script>
<button onclick="hide(this,true); debug('hide button 1');">Hide1</button>
<button onclick="hide(this); debug('hide button 2');">Hide2</button>
```

下面这些客户端 JavaScript 代码用到了事件，它给一个很重要的事件——“load”事件注册了一个事件处理程序。同时，也展示了注册“click”事件处理函数更高级的一种方法。

```js
// "load"事件只有在文档加载完成后才会触发
//通常需要等待load事件发生后才开始执行JavaScript代码
window.onload = function() { // 当文档加载完成时执行这里的代码
    // 找到文档中所有的<img>标签
    var images = document.getElementsByTagName("img");

    // 遍历 images，给每个节点的"click"事件添加事件处理程序
    // 在点击图片的时候将图片隐藏
    for(var i = 0; i < images.length; i++) {
        var image = images[i];
        if (image.addEventListener)  // 注册事件处理程序的另一种方法
            image.addEventListener("click", hide, false);
        else     // 兼容IE8及以前的版本
            image.attachEvent("onclick", hide);
    }

    // 这便是上面注册的事件处理函数
    function hide(event) { event.target.style.visibility = "hidden"; }
};
```

第十五章到十七章讲诉了如何使用 JavaScript 来操控网页的内容（HTML）、样式（CSS）以及行为（事件处理）。这些章所讨论得 API 多少有些复杂，且至今仍具有糟糕的浏览器兼容性。也正是由于这个原因，很多客户端 JavaScript 程序员选择使用“库”或“框架”来简化他们的编码工作。最流行的库非 jQuery 莫属。第19章将会详细介绍 jQuery 库。 jQuery 定义了一套灵巧易用的 API ，用来操控文档内容、样式和行为。 jQuery 经过了完整的测试，在所有现代主流浏览器，甚至在 IE6 这种早期浏览器中都可以照常运行。

jQuery代码非常易于识别，因为它充分利用了一个名为`$()`的函数。这里用 jQuery 重写了上文中提到的`debug()`函数：

```js
function debug(msg) {
    var log = $("#debuglog");   // 找到要显示msg的元素.
    if (log.length == 0) {   // 如果不存在则创建之
        log = $("<div id='debuglog'><h1>Debug Log</h1></div>");
        log.appendTo(document.body);  // 并将其追加到body里
    }
    log.append($("<pre/>").text(msg)); // 将msg包装在<pre>中，再追加到log里
}
```

目前我们所提到的第二部分的四章都是围绕网页展开讨论的。后续的四章将着眼点转向 Web 应用。这几章的内容并不是讨论如何通过编写操控内容、样式和行为的脚本使用 Web 浏览器来渲染文档；而是讲解如何将 Web 浏览器当做应用平台，并描述了用以支持更复杂精细的客户端 Web 应用的现代浏览器 API 。第十八掌章讲解如何使用 JavaScript 来发起 HTTP 请求。第二十章描述数据存储的机制以及客户端应用中的会话状态的保持。第二十一章涵盖基于 HTML 的`<canvas>`标签的客户端 API ，用来进行任意形状图形的绘制。最后，第二十二章讲解 HTML5 所提供的新一代 Web 应用 API 。网络、存储、图形：这些都是 Web 浏览器提供的操作系统级的服务，它们定义了全新的跨平台的应用环境。如果你正在进行基于那些支持这些新 API 的浏览器的开发，这将是你作为客户端 JavaScript 程序员最激动人心的时刻。最后四章并没有太多示例代码，但下面的例子使用了这些新的API。

## 示例：一个 JavaScript 贷款计算器

这里的例子展示了诸多JavaScript语言核心特性，同样展示了重要的客户端JavaScript技术：

- 如何在文档中查找元素
- 如何通过表单 input 元素来获取用户的输入数据
- 如何通过文档元素来设置 HTML 内容
- 如何将数据存储在浏览器中
- 如何使用脚本发起HTTP请求
- 如何利用`<canvas>`元素绘图

# 第一部分 JavaScript语言核心

# 第2章 词法结构

编程语言的词法结构是一套基础性规则，用来描述如何使用这门语言来编写程序。作为语法的基础，它规定了诸如变量名是什么样的，怎么写注释，以及程序语句之间如何分割等规则。

## 2.1 字符集

JavaScript 程序是用 Unicode 字符集编写的。 Unicode 是 ASCALL 和 Latin-1 的超集，并支持地球上几乎所有在用的语言。

### 2.1.1 区别大小写

JavaScript 是区分大小写的语言。也就是说，关键字、变量、函数名和所有的标识符（identifier）都必须采用一致的大小写规则。

但需要注意的是， HTML 并不区分大小写（尽管 XHTML 区分大小写）。许多客户端 JavaScript 对象和属性与它们所表示的 HTML 标签和属性同名。在 HTML中，这些标签和属性名可以使用大写也可以是小写，而在 JavaScript 中则必须是小写。例如，在 HTML 中设置事件处理程序时， onclick 属性可以写成 onClick ，但在 JavaScript 代码（或者 XHTML 文档）中，必须使用小写的 onclick 。 

### 2.1.2 空格、换行符和格式控制符

JavaScript 会忽略程序中的标识（token）之间的空格，多数情况下， JavaScript 同样会忽略换行符。由于可以在代码中随意使用空格和换行符，一次可以采用整齐和一致的缩进来形成统一的编码风格，提高代码的可读性。

JavaScript 除了识别空格符(\u0020)。 JavaScript 还可以识别如下标示空格的字符：水平制表符（\u0009）、垂直制表符(\u000B)、换页符(\u000C)、不中断空白符(\u00A0)、字节序标记(\uFEFF)，以及在Unicode中所有Zs类别的字符。

JavaScript 将如下字符识别为结束符：换行符(\u000A)，回车符号(\u000D)，行分隔符(\u2028)，段分隔符号(\u2029)。回车符加换行符在一起呗解析为一个单行的结束符。

Unicode格式控制字符(Cf类)，比如“从右至左书写标记”(\u200F)和从“从左至右书写标记”(\u200E)，控制着文本的视觉显示。这对一些非英语文本的正确显示来说是至关重要的，这些字符可以在 JavaScript 的注释，字符串直接量和正则表达式直接量中，但不能用在标示符（比如，变量名）中，但有个例外零宽连接符(\u200D)和零宽非连接符(\uFEFF)是可以出现在标示符中，但不能作为标识符的手字符。上文也提到了，字节序标记格式控制符(\uFEFF)被当成了空格来对待。

### 2.1.3 Unicode转义序列

在有些计算机硬件和软件里，无法显示或输入 Unicode 字符全集。为了支持那些使用老旧技术的程序员， JavaScript 定义了一种特殊序列，使用六个 ASCLL 字符来代表任意 16 位 Unicode 内码。这些 Unicode 转义序列均以`\u`为前缀，其后跟随 4 个十六进制数（使用数字以及大写或小写的字符A-F表示）。这种 Unicode转义写法可以用在 JavaScript 字符串直接量、正则表达式直接量和标识符中（关键字除外）。例如，下面两个 JavaScript 字符串是完全一样的。

```js
"café" === "caf\u00e9" => true 
```

Unicode 转义写法也可以出现在注释中，但由于 JavaScript 会将注释忽略，它们只是被当成上下文中的 ASCLL 字符处理，而且不会被解析为其对应的 Unicode 字符。

### 2.1.4 标准化

Unicode 允许使用多种方法对同一个字符进行编码。比如字符é可以使用 Unicode 字符\u00E9,也可以使用普通的 ASCLL 字符e跟随一个语调符号\u0301 ,在文本编辑器中，这两个编码显示的结果是一摸一样的，但是它们的二进制编码表示是不一样的，在计算机里也不相等。 Unicode 标准为索引字符定义了一个首选的代码格式，并给出了一个标准化的处理方式将文本转化为一种适合比较的标准格式，不会再对其它表示、字符串或者正则表达式做标准化处理。

## 2.2 注释

JavaScript 支持两种格式的注释。在行尾`//`之后的文本都会被 JavaScript 当作注释忽略掉的。此外，`/*`和`*/`之间的文本也会当作注释，这种注释可以跨行书写，但不能有嵌套的注释。

```js
// 这里是单行注释
/* 这里是一段注释 */  // 这里是另一段注释
/*
* 这又是一段注释
* 这里的注释可以连续写多行
*/
```

## 2.3 直接量

所谓直接量（literal），就是程序中直接使用的数据值。

```js
12 //数字
1.2 //小数
"Hllo World" //字符串文本
'hi' //另一个字符串
true //布尔值
false //另一个布尔值
/javascript/gi //正则表达式直接量（用做模式匹配）
null //空
```

更多复杂的表达方式可以写成数组或对象直接量。

```js
{ x:1, y:2 } //对象
[ 1,2, 3,4,5 ] //数组
```

## 2.4 标识符和保留字

标识符就是一个名字。在 JavaScript 中，标识符用来对变量和函数进行命名，或者用作 JavaScript 代码中某些循环语句中的跳转位置的标记。 JavaScript 标识符必须以字符、下划线（_）或美元符（$）开始。后续的字符可以是字母、数字、下划线或美元符（数字是不允许作为首字符出现的，以便 JavaScript 可以轻易区分开标识符和数字）。下面是合法的标识符：

- my_variable_name
- b13
- _dummy
- $str

处于可移植性和易于书写的考虑，通常我们只使用 ASCII 字符和数字来书写标识符。然而需要注意的是， JavaScript 允许标识符中出现 Unicode 字符全集中的字母和数字。此外，程序员也可以使用非英语语言或数字符号来书写标识符。

```js
var sá = true;
var π = 3.14;
```

和其他任何编程语言一样，JavaScript 保留了一些标识符为自己所用。这些“保留字”不能用作普通的标识符。

**保留字**

JavaScript 把一些标识符拿出来用作自己的关键字。因此，就不能再在程序中把这些关键字用作标识符了：

- break
- case
- catch
- continue
- default
- delete
- do
- else
- finally
- for
- function
- if
- in
- instanceof
- new
- return
- switch
- this
- throw
- try
- typeof
- var
- void
- while
- with

javascript 同样保留了一些关键字，这些关键字在当前的语言版本并没有使用，但在未来版本中可能会用到。ECMAScript 5 保留了这些关键字。

class const enum export
export extends import super

## 2.5 可选的分号

和很多编程语言一样， JavaScript 使用分号`;`将语句分隔开。这对增强代码的可读性和整洁性是非常重要的。缺少分隔符，一条语句结束就成了下一条语句的开始，反之亦然。

在 JavaScript 中，各自语句独占一行，通常可以省略语句之间的分号（程序结尾处使用`}`花括弧之前的分号也可以省略）。

很多 JavaScript 程序员（包括本书的代码示例）都是使用分号来明确标记语句的结束，即使在并不完全需要分号的时候也是如此，另一种风格是在任何可以省略分号时都将其省略，只有在不得不使用的时候才使用分号，不管哪种编程风格，关于 JavaScript 有几个细节需要注意。

```js
// 如下代码,第一个分号是可以省略的
a=3;
b=4;

// 但如果按照如下格式书写，第一个分号则不能省略。
a=3;b=4;
```

需要注意的是， JavaScript 并不是在所有的换行处都填补分号：只有在缺少了分号就无法正常解析代码的时候， JavaScript 才会填补分号，换句话说（类似下面代码中的两处异常），如果当前的语句和随后的的非空格字符不能当成一个整体解析的话， JavaScript 就在当前语句的结束处来填补分号，看下如下代码

```js
var a
a
=
3
console.log(a)

// javascript将其解析为
var a;a=3;console.log(a); 
```

有些语句的分隔规则会导致一些想不到的情形，这段代码写成了两行，看起来是两条独立的语句。

```js
var y = x + f
(a+b).toString()

// 实际上
var y = x+f(a+b).toString();
```

通常来讲，如果一条语句以 `(`、`[`、`/` `+` 或 `-` 开始，那么它极有可能和前条语句组合在一起解析，以 `/`、`+` 和 `-` 开始的语句不很常见，但以 `(` 和 `[` 开始的语句则非常常见。至少在一些javascript编码符风格中是很常见的。有点程序员喜欢保守的在语句前边加上一个分号，这样，哪怕之前的语句被修稿了，分号被误删了，当前语句还是会正确的解析；

```js
// 这里省略了分号
var x = 0 
// 前面的分号保证了正确地语句解析
;[x, x+1, x+2].forEach(console.log)  
```

如果当前语句和下一行语句无法合并解析。javascript 则在第一行后填补分号，这是通用规则，但有两个例外。第一个例外是涉及到 `returnm`、`birak` 和 `continue` 语句，如果这三个关键字后紧跟着换行。javascript则会在换行处填补分号。例如

```js
return
true;

// 而 javascript解析成
return;ture;

// 而代码的本意是
return ture;
```
也就是说`return`、`break` 和 `contuine` 好的随后的表达式之间不能有换行，如果添加了换行，程序则在极有特殊情况才能报错。而且程序的调试很不方便。

第二个例子是涉及到 `++` 和 `--` 运算符时，这些表达式符号可以代表标识符表达式的前缀和后缀。如果将其又再后表达式，如果的将其用做后缀表达式。它和表达式应该看做一行。否则行尾将填补分号。

```js
x
++
yy

// 以上代码解析为
x;
++y
```

# 第3章 类型、值和变量

计算机程序的运行需要对值（value）进行操作。在编程语言中，能够表示并操作的值的类型称作数据类型（type），编程语言最基本的特性就是能够支持多种数据类型。当程序需要将值保存起来以备将来使用时，便将其复制给（将值“保存”到）一个变量（variable）。变量是一个值的符号名称，可以通过名称来获得对值的引用。变量的工作机制是变成语言的另一个基本特性。

JavaScript 的数据类型分为两类：原始类型(primitive type)和对象类型(object type)。 JavaScript 中的原始类包括数字、字符串和布尔值，

JavaScript 还有两个特殊的原始值，`null`(空)和`Undefined`(未定义)，他们不是数字、字符串、布尔值。它们分别代表了各自特殊类型的唯一成员。

javascript除了数字、字符串、布尔值、`null`、`undefined`之外就是对象了。对象 (object)是属性(property)的集合。每个属性都由"名/值对"(值可以是原始值，比如数字，字符串，也可以是对象)构成。其中一个比较特殊的对象(全局对象(global object)。

普通的 JavaScript 对象是“命名值”的无需集合。 JavaScript 同样定义了一种特殊对象——数组(array)，表示带编号的值的有序集合。 JavaScript 为数组定义了专用的语法。使数组拥有一些和普通对象不同的特有的行为属性。

JavaScript 还定义了一种特殊的对象——函数。函数是具有与它相关联的可执行代码的对象，通过调用函数来运行可执行代码，并返回运算结果。和数组一样，函数行为特征和其它对象都不一样。 JavaScript 为使用函数定义了专用语法。对 JavaScript 函数来讲。最重要的是，他们都是真值，并且 JavaScript 可以将他们当做普通对象来对待。

如果函数初始化（使用`new`运算符）一个新建对象，我们称之为构造函数(constructor)。每个构造函数定义了一类（class）对象——由构造函数初始化对象组成的集合。类可以看做对象类型的子类型。除了数组（Array）类和函数(Function)类之外，JavaScript 还定义了其它三种有用的类。日期（Date）类定义了代表日期的对象。正则（RegExp）类定义了正则表达式的对象。错误（error）类定义了那行表示JavaScript 程序中运行时错误和语法错误对象。可以通过定义自己的构造函数来定义需要的类。

JavaScript 解释器有自己的内存管理机制，可以自动对内存进行垃圾回收（garbage collection）。这意味着程序程序可以按需创建对象，程序员则不必担心这些对象的销毁和内存回收。当不再有任何引用指向一个对象，解释器就知道这个对象没有用了，然后会自动回收它所占用的内存资源。

JavaScript 是一种面向对象的语言。不严格的讲，这意味着我们不用全局的定义函数去操作不同类型的值，数据类型本身可以定义方法(method)来使用值。例如数组的方法可以使用`[].sort()`来排序。

从技术上来将，只有 JavaScript 对象才能拥有方法。然而，数字，字符串，布尔值也拥有自己的方法。在 JavaScript 中，只有`null`和`undefined`是无法拥有方法的值。

JavaScript 的类型可以分为原始类型和对象类型，也可分为可以拥有方法的类型和不能拥有方法的类型。同样可分为可变（mutable）乐行和不可变(immutable)类型。可变类型的值是可以修改的，对象和数组属于可变类型； JavaScript 程序可以改变对象的属性值和数组元素的值。数字、布尔值、`null`和`undefined`属于不可改变的类型。

比如，修改一个数组的内容本身就说不通。字符串可以看做是字符组成的数组，你可以认为它是可以变的。然而在 JavaScript 中，字符串是不可变的。可以访问字符串任意位置的文本，但 JavaScript 并未提供修改已知字符串文本内容的方法。

JavaScript 可以自由地进行数据类型转换。比如，如果在程序期望使用字符串的地方使用了数字，JavaScript 会自动将数字转换为字符串。如果期望在使用布尔值的地方使用了非布尔值，JavaScript 也会相应的转换。JavaScript 中对灵活的类型转换规则对“判断相等”（equality）的定义亦有影响。

JavaScript 的变量是无类型的（untyped），变量可以被赋予任何类型的值，同样一个变量也可以重新赋予不同类型的值。使用`var`关键字来声明（declare）变量。JavaScript 采用语法作用域。不在任何函数内声明的变量称为全局变量（global variable），它在 JavaScript 的程序中任何地方都是可见的。在函数内声明的变量具有函数作用域（function scope），并且只在函数内可见。

## 3.1 数字
## 3.2 文本
## 3.3 布尔值
## 3.4 null和undefined
## 3.5 全局对象
## 3.6 包装对象
## 3.7 不可变的原始值和可变的对象引用
## 3.8 类型转换
## 3.9 变量声明
## 3.10 变量作用域

# 第4章 表达式和运算符
# 第5章 语句
# 第6章 对象
# 第7章 数组
# 第8章 函数

函数是这样的一段 JavaScript 代码，它只定义一次，但可能被执行或调用任意次。

JavaScript函数是参数化的：函数的定义会包括一个称为形参（parameter）的标识符列表，这些参数在函数体中像局部变量一样工作。函数调用会为形参提供实参的值。函数使用它们实参的值来计算返回值，成为该函数调用表达式的值。

除了实参之外，每次调用还会拥有另一个值——本次调用的上下文——这就是this关键字的值。

如果函数挂载在一个对象上，作为对象的一个属性，就称它为对象的方法。当通过这个对象来调用函数时，该对象就是此次调用的上下文（context），也就是该函数的this的值。

用于初始化一个新创建的对象的函数称为构造函数（constructor）。

在JavaScript里，函数即对象，程序可以随意操控它们。比如，JavaScript可以把函数赋值给变量，或者作为参数传递给其他函数。因为函数就是对象，所以可以给它们设置属性，甚至调用它们的方法。

JavaScript 的函数可以嵌套在其他函数中定义，这样它们就可以访问它们被定义时所处的作用域中的任何变量。这意味着 JavaScript 函数构成了一个闭包（closure），它给 JavaScript 带来了非常强劲的编程能力。

## 8.1 函数定义 

函数使用 function 关键字来定义，它可以用在函数定义表达式或者函数声明语句里。在两种形式中，函数定义都从 function 关键字开始，其后跟随这些组成部分：

* 函数名称标识符。函数名称是函数声明语句必需的部分。它的用途就像变量的名字，新定义的函数对象会赋值给这个变量。对函数定义表达式来说，这个名字是可选的：如果存在，该名字只存在于函数体中，并指代该函数对象本身。
* 一对圆括号，其中包含由0个或者多个用逗号隔开的标识符组成的列表。这些标识符是函数的参数名称，它们就像函数体中的局部变量一样。
* 一对花括号，其中包含0条或多条 JavaScript 语句。这些语句构成了函数体：一旦调用函数，就会执行这些语句。

注意，以表达式来定义函数只适用于它作为一个大的表达式的一部分，比如在赋值和调用过程中定义函数：

```js
//定义javascript函数
//输出o的每个属性的名称和值，返回undefined
function printprops(o) {
    for (p in o)
        console.log(p + ":" + o[p] + "\n")
}

//计算两个迪卡尔坐标（x1,y1）和(x2,y2)之间的距离
function distance(x1, y1, x2, y2) {
    var dx = x2 - x1;
    var dy = y2 - y1;
    return Math.sqrt(dx * dx + dy * dy)
}

//计算递归函数（调用自身的函数）
//x!的值是从x到x递减（步长为1）的值的累乘
function factorial(x) {
    if (x <= 1) return 1;
    return x * factorial(x - 1);
}

//这个函数表达式定义了一个函数用来求传入参数的平方
//注意我们把它赋值了给一个变量
var square = function(x) {
    return x * x
}

//函数表达式可以包含名称，这在递归时很有用
var f = function fact(x) {
    if (x <= 1) return 1;
    else return x * fact(x - 1);
};
//f(7)=>5040

//函数表达式也可以作为参数传给其它函数
data.sort(function(a, b) {
    return a - b;
});

//函数表达式有时定义后立即使用
var tensquared = (function(x) {
    return x * x;
}(10))
```

注意，以表达式方式定义的函数，函数的名称是可选的。一条函数声明语句实际上声明了一个变量，并把一个函数对象赋值给它。相对而言，定义函数表达式并没有声明一个变量。实际上，函数的名称将成为函数内部的一个局部变量。

通常而言，以表示方式定义函数时都不需要名称，这会让定义它们的代码更为紧凑。函数定义表达式特别适合用来定义那些只会用到一次得函数。

函数名称通常是动词或以动词为前缀的词组。通常函数名的第一个字符为小写，这是一种编程约定。在一些编程风格中，或者编程框架里，通常为那些经常调用的函数指定短名称，比如客户端 JavaScript 框架 jQuery 就将最常用的方法重命名为`$()`（一个美元符号）（美元符号和下划线是除了字母和数字之外的两个合法的 JavaScript 标识符）。

函数声明语句“被提前”到外部脚本或外部函数作用域的顶部，所以以这种方式声明的函数，可以被在它定义之前出现的代码所调用。不过，以表达式定义的函数就另当别论了，为了调用一个函数，必须要能引用它，而要使用一个以表达式方式定义的函数之前，必须把它赋值给一个变量。变量的声明提前了，但给变量赋值是不会提前的，所以，以表达式方式定义的函数在定义之前无法调用）。

大多数函数（但不是全部）包含一条 return 语句。 return 语句导致函数停止执行，并返回它的表达式（如果有的话）的值给调用者。如果 return 语句没有一个与之相关的表达式，则它返回 undefined 值。如果一个函数不包含 return 语句，那它就只执行函数体中的每条语句，并返回 undefined 值给调用者。

**嵌套函数**

在 JavaScript 里，函数可以嵌套在其他函数里。

```js
function hyuse(a, b) {
    function square(x) {
        return x * x
    }
    return Math.sqrt(square(a) + square(b));
}
```

嵌套函数的有趣之处在于它的变量作用域规则，它们可以访问嵌套它们（或多重嵌套）的函数的参数和变量。

函数声明语句并非真正的语句， ECMAScript 规范只是允许它们作为顶级语句。它们可以出现在全局代码里，或者内嵌在其他函数中，但它们不能出现在循环、条件判断，或者`try/catch/finally`以及`with`语句中。注意，此限制仅用于以语句声明形式定义的函数。函数定义表达式可以出现在 JavaScript 代码的任何地方。

## 8.2 函数调用 

构成函数主体的 JavaScript 代码在定义之时并不会执行，只有调用该函数时，它们才会执行。有4种方式来调用JavaScript函数：

1. 作为函数
2. 作为方法
3. 作为构造函数
4. 通过它们的`call()`和`apply()`方法间接调用

### 8.2.1 函数调用

使用调用表达式可以进行普通的函数调用也可进行方法调用。一个调用表达式由多个函数表达式组成，每个函数表达式都是由一个函数对象和左圆括号、参数列表和右圆括号组成，参数列表是由逗号分隔的零个或多个参数表达式组成。如果函数表达式是一个属性访问表达式，即该函数是一个对象的属性或数组中的一个元素，那么它就是一个方法调用表达式。

```js
printprops({x: 1});
var total = distance(0,0,2,1) + distance(2,2,3,5);
var probality = factorial(5) / factorial(13);
```

在一个调用中，每个参数表达式（圆括号之间的部分）都会计算出一个值，计算的结果作为参数传递给另外一个函数。这些值作为实参传递给声明函数时定义的形参。

对于普通的函数调用，函数的返回值称为调用表达式的值。如果该函数返回时因为解释器达到结尾，返回值就是 undefined 。如果函数返回时因为解释器执行到一条 return 语句，返回值就是 return 之后的表达式的值。如果 return 语句没有值，则返回 undefined 。

根据ECMAScript 3和非严格的ECMAScript 5对函数调用的规定，调用上下文（this的值）是全局对象。然而，在严格模式下，调用上下文则是 undefined 。以函数形式调用的函数通常不使用 this 关键字。不过，“this”可以用来判断当前是否是严格模式。

```js
var strict= (function(){return !this;}());
```

### 8.2.2 方法调用

一个方法无非是个保存在一个对象的属性里的 JavaScript 函数。如果有一个函数 f 和一个对象 o ，则可以用下面的代码给 o 定义一个名为 m() 的方法。

```js
o.m = f;
```

给对象 o 定义了方法 m() 调用它时就像这样：

```js
o.m();

// 需要实参的调用
o.m(x, y);
```

上面的代码是一个调用表达式：它包括一个函数表达式 o.m ，以及两个实参表达式 x 和 y ，函数表达式本身就是一个属性访问表达式，这意味着该函数被当作一个方法，而不是作为一个普通函数来调用。

对方法调用的参数和返回值的处理，和上面所描述的普通函数调用完全一致。但是，方法调用和函数调用有一个重要的区别，就是调用上下文。属性访问表达式由两部分组成，一个对象（本例中的 o ）和属性名称（m）。在像这样的方法调用表达式里，对象 o 成为调用上下文，函数体可以使用关键字 this 引用该对象。

```js
var calcul = { //对象直接量
    oprand1: 1,
    oprand2: 1,
    add: function() {
        //注意this关键字的用法，this指带当前对象
        return this.result = this.oprand1 + this.oprand2;
    }
};
calcul.add(); //这个方法调用计算1+1的结果
calcul.result; //=>2
```

大多数方法调用使用点符号来访问属性，使用方括号也可以进行属性访问操作。

```js
o["m"](x,y) //o.m(x,y)的另外一种写法
a[0](z)//同样是一个方法调用(这里假设a[0]是一个函数)
```

方法调用可能包括更复杂的属性访问表达式

```js
customer.surname.toUpperCase(); //调用customer.surname方法
f().m(); //在f()调用结束后继续调用返回值中的方法m()
```

方法和 this 关键字是面向对象编程范例的核心。任何函数只要作为方法调用实际上都会传入一个隐式的实参——这个实参是一个对象，方法调用的母体就是这个对象。通常来讲，基于那个对象的方法可以执行多种操作，方法调用的语法已经很清晰地表明了函数将基于一个对象进行操作

```js
rect.setSize(windth, height);
setrectSize(rect, width, heigth);
```

当方法的返回值是一个对象，这个对象还可以再调用它的方法。这种方法调用序列中（通常称为“链”或者“级联”）每次的调用结果都是另外一个表达式的组成部分。比如，基于jQuery库，我们常常会这样写代码：

```js
//找到所有的header，取得他们的id的映射，转换为数组并给它们进行排序
$(":header").map(function(){return this.id}).get().sort();
```

需要注意的是， this 是一个关键字，不是变量，也不是属性名。 JavaScript 的语法不允许给 this 赋值。

和变量不同，关键字this没有作用域的限制，嵌套的函数不会从调用它的函数中继承this。如果嵌套函数作为方法调用，其this的值指向调用它的对象。如果嵌套函数作为函数调用，其this值不是全局对象（非严格模式下）就是undefined（严格模式下）。很多人误以为调用嵌套函数时this会指向调用外层函数的上下文。如果你想访问这个外部函数的this值，需要将this的值保存在一个变量里，这个变量和内部函数都同在一个作用域内。通常使用变量self来保存this，比如：

```js
var o = { //对象o
    m: function() { //对象中的方法m()
        var self = this; //将this的值保存在一个变量中
        console.log(this === o); //输出true，this就是这个对象o
        f(); //调用辅助函数f()

        function f() { //定义一个嵌套函数f()
            console.log(this === o); //"false":this的值是全局对象undefied
            console.log(self === o); //"true": slef指外部函数this的值
        }
    }
};
o.m();//调用对象o的方法m
```

### 8.2.3 构造函数调用

如果函数或者方法调用之前带有关键字 new ，它就构成构造函数调用。构造函数调用和普通的函数调用以及方法调用在实参处理、调用上下文和返回值方面有所不同。

如果构造函数调用在圆括号内包含一组实参列表，先计算这些实参表达式，然后传入函数内，这和函数调用和方法调用是一致的。但如果构造函数没有形参， JavaScript 构造函数的语法是允许省略实参列表和圆括号的。凡事没有形参的构造函数调用都可以省略括号。

```js
var o = Object();
// 等价
var o = Object;
```

构造函数调用创建一个新的空对象，这个对象继承来自构造函数的 prototype 属性。构造函数视图初始化这个新创建的对象，并将这个对象用作其调用上下文，因此构造函数可以使用 this 关键字来引用这个新创建的对象。注意，尽管构造函数看起来像一个方法调用，它仍然会使用这个新对象作为调用上下文，也就是说，在表达式`new o.m()`中，调用上下文并不是 o 。

构造函数通常不使用 return 关键字，它们通常初始化新对象，当构造函数的函数体执行完毕时，它会显式返回。在这种情况下，构造函数调用表达式的计算结果就是这个新对象的值。然而如果构造函数显式地使用 return 语句返回一个对象，那么调用表达式的值就是这个对象。如果构造函数使用 return 语句但没有指定返回值，或者返回一个原始值，那么这时将忽略返回值，同时使用这个新对象作为调用结果。

### 8.2.4 间接调用

JavaScript 中的函数也是对象，和其他 JavaScript 对象没什么两样，函数对象也可以包含方法。其中的两个方法`call()`和`apply()`可以用来间接地调用函数。两个方法都允许显式指定调用所需的 this 值，也就是说，任何函数可以作为任何对象的方法来调用，哪怕这个函数不是那个对象的方法。两个方法都可以指定调用的实参。`call()`方法使用它自有的实参列表作为函数的实参，`apply()`方法则要求以数组的形式传入参数。

## 8.3 函数的实参和形参 

JavaScript 中的函数定义并未指定函数形参的类型，函数调用也未对传入的实参值做任何类型检查。实际上， JavaScript 函数调用甚至不检查形参的个数。

### 8.3.1 可选形参

当调用函数的时候传入的实参比函数声明指定的形参个数要少，剩下的形参都将设置为 undefined 值。因此在调用函数时形参是否可选以及是否可以省略应当保持好的适应性。为了做到这一点，应当给省略的参数赋一个合理的默认值。

```js
//将对象o中的可枚举属性名追加到数组a中，并返回这个数组a
//如果省略a，则创建一个新数组并返回这个新数组
function getPropertyNames(o, /*optional*/ a) {
    if (a === undefined) a = []; //如果a未定义，则使用新数组
    for (var property in o) a.push(property);
    return a;
}

//这个函数调用时可以使用两个实参
getPropertyNames(xx); //将o的属性存储到一个新的数组中
getPropertyNames(xx, zz); //将p的属性追加到数组a中
```

如果在第一行代码中不使用 if 语句，可以使用“||”运算符，这是一个钟习惯用法。

```js
a = a || [];
```

需要注意的是，当用这种可选实参来实现函数时，需要将可选实参放在实参列表的最后，那些调用你的函数的程序员是没办法省略第一个实参并传入第二个实参的，它必须将 undefined 作为第一个实参显式传入。

### 8.3.2 可变长的实参列表：实参对象

当调用函数的时候传入的实参个数超过函数定义时，没有办法直接获得未命名值的引用。参数对象解决了这个问题。在函数体内，标识符 arguments 是指向实参对象的引用，实参对象是一个类数组对象，这样可以通过数字下标就能访问传入函数的实参值，而不用非要通过名字来得到实参。

此外，和真正的数组一样， arguments 也包含一个 length 属性，用以标识其所包含元素的个数。

实参对象在很多地方都非常有用，下面的例子展示了使用它来验证实参的个数。需要注意的是，通常不必像这样检查实参个数。大多数情况下 JavaScript 的默认行为是可以满足需要的：省略的实参都是 undefined ，多出的参数会自动省略。

```js
function f(x, y, z) {
    //首先验证传入实参的个数是否正确
    if (arguments.leng != 3) {
        throw new Error("function f() called with" + arguments.length + "arguments,but it ecxpects 3 arguments");
    }
    //再执行函数的其它逻辑
}
```

实参对象有一个重要的用处，就是让函数可以操作任意数量的实参。下面的函数就可以接收任意数量的实参，并返回传入实参的最大值（内置函数`Math.max()`的功能与之类似）。类似这种函数可以接收任意个数的实参，这种函数也称为“不定实参函数”（varargs function）。

```js
function max( /*...*/ ) {
    var max = Number.NEGATIVE_INFINITY;
    //遍历实参，查找并记住最大值
    for (var i = 0; i < arguments.length; i++)
        if (arguments[i] > max) max = arguments[i];
        //返回最大值
    return max;
}
max(1, 10, 222, 100); //=>222
```

注意，不定实参函数的实参个数不能为零，`arguments[]`对象最适合的应用场景是在这样一类函数中，这种函数包含固定个数的命名和必须参数，以及随后个数不定的可选实参。

数组对象包含一个非同寻常的特性。在非严格 模式下，当一个函数包含若干形参，实参对象的数组元素时函数形参所对应实参的别名，实参对象中以数字索引，并且形参名称可以认为是相同变量的不同命名。通过实参名字来修改参数值的话，通过`arguments[]`数组也可以获取到更改后的值。

```js
function f(x) {
    console.log(x); //输出实参的初始值
    arguments[0] = null; //修改实参组的元素同样会修改x的内容
    console.log(x); //输“null”
}
f(11);
```

在 ECMAScript 5 中移除了实参对象的这个特殊特性。再严格模式中，它变成了一个保留字。严格模式中的函数无法使用 arguments 作为形参名或局部变量名，也不能给 arguments 赋值。

**callee和caller属性**

除了数组元素，实参对象还定义了 callee和 caller属性。在 ECMAScript 5 严格模式中，对这两个属性的读写操作都会产生一个类型错误。而在非严格模式下， ECMAScript标准规定 callee 属性指代当前正在执行的函数。 caller是非标准的，但大多数浏览器实现了这个属性，它指代调用当前正在执行的函数的函数。通过 caller 属性可以访问调用栈。callee 属性在某些时候会非常有用，比如在匿名函数中通过 callee 来递归地调用自身。

```js
var factorial = function(x) {
    if (x <= 1) return 1;
    return x * arguments.callee(x - 1);
}
```

### 8.3.3 将对象属性用作实参

当一个函数包含超过三个形参时，要记住调用函数中实参的正确顺序比较困难，最好通过名/值对的形式来传入参数。为了实现这种风格的方法调用，定义函数的时候，传入的实参都写入一个单独的对象之中，在调用的时候传入一个对象，对象中的名/值是真正需要的实参数据。

```js
//将原始值数组的length元素复制至目标数组
//开始复制原始数组的from_start元素
//并且将其复制到目标数组to_start中
//要记住实现的顺序并不容易
function arrayCopy( /*array*/ from, /*index*/ from_start, 
                    /*array*/ to, /*index*/ to_start, 
                    /*integer*/ length) {
    //逻辑代码
}
//这个版本的实现效率有些低，但你不必再记住实参的顺序
//并且from_start和to_start都默认为0
function easyCopy(args) {
    arrayCopy(args.form,
        args.form_start || 0, //注意，这里设置了默认值
        args.to,
        args.to_start || 0, args.length);
}
//来看如何调用easyCopy
var a = [1, 2, 3, 4],
    b = [];
easyCopy({
    from: a,
    to: b,
    length: 4
});
```

### 8.3.4 实参类型

JavaScript 方法的形参并未声明类型，在形参传入函数体之前也未做任何类型检查。

应当添加类似的实参类型检查逻辑，宁愿程序在传入非法值时报错，也不愿非法值导致程序在执行时报错。

```js
//判定o是否是一个类数组对象
//字符串和函数都length属性，但是他们可以有typeOf检测将其排除
//在客户端javascript中，DOM文本节点也有length属性，需要用额外的o.nodetype != 3将其排除
function isArrayLike(o) {
    if (o && //o非null、undefined等
        typeof o === "object" && //o是对象
        isFinite(o.length) && //o.length是有限数
        o.length >= o && //o.length是非负数
        o.length === Math.floor(o.length) && //o.length是整数
        o.length < 4294967296) //o.length < 2^32
        return true;
    else
        return fasle; //否则它不是
}

//返回数组（或类数组对象）a的元素累加和
//数组a中必须为数字/ null undefined的元素都将忽略
function sum(a) {
    if (isArrayLike(a)) {
        var total = 0;
        for (var i = 0; i < a.length; i++) { //遍历所有元素
            var element = a[i];
            if (element == null) continue; //跳过null和undefiend
            if (isFinite(element)) total += element;
            else throw new Error("sum():elements must be a finte numbers");
        }
        return total;
    } else throw new Error("sun():arguments mustbe array-like")
};

a = [1,2,4,5,3,6,7];
sum(a)
```

JavaScript 是一种非常灵活的弱类型语言，有时适合编写实参类型和实参个数的不确定性的函数。接下来的`flexisum()`方法就是这样。它可以接收任意数量的实参，并可以递归地处理实参是数组的情况。

```js
function flexisum(a) {
    var total = 0;
    for (var i = 0; i < arguments.length; i++) {
        var element = arguments[i],
            n;
        if (element == null) continue; //忽略null和undefined
        if (isArray(element)) //如果实参是数组
            n = flexisum.apply(this, element); //递归的计算累加和
        else if (typeof element === "function") //否则，如果是函数...
            n = Number(element()); //调用它并做类型抓换
        else
            n = Number(element); //直接做类型抓换
        if (isNaN(n)) //如果无法转换为数字，则抛出异常
            throw Error("flexisum():can nont convent" + element + "to number");
        total += n; //否则，将n累加到total
    }
    return total;
}
```

## 8.4 作为值的函数 

函数可以定义，也可以调用，这是函数最重要的特性。在 JavaScript 中，函数不仅是一种语法，也是值，也就是说，可以将函数赋值给变量，存储在对象的属性或数组的元素中，作为参数传入另外一个函数等。

```js
function square(x) {
    return x * x
}
var s = square; //现在s和sqare指代同一个函数
square(4); //=>16
s(4); //=>16
```

除了可以将函数赋值给变量，同样可以将函数赋值给对象的属性。当函数作为对象的属性调用时，函数就成为方法。

```js
var o = {
        square: function(x) {
            return x * x
        }
    }; //对象直接量
var y = o.square(16);
```

函数甚至不需要名字，当把它们赋值给数组元素时。

```js
var a = [
    function(x) {return x * x},
    20];
console.log(a[0](a[1])) //=>400
```

**自定义函数属性**

JavaScript 中的函数并不是原始值，而是一种特殊的对象，也就是说，函数可以拥有属性。

比如，想写一个返回一个唯一整数的函数，不管在哪里调用函数都会返回这个整数。而函数不能两次返回同一个值。因为这个信息仅仅是函数本身用到的。最好将这个信息保存到函数对象的一个属性中。

```js
//初始化函数对象的计数器属性
//由于函数声明被提前了，因此这个是可以在函数声明
//之前给它的成员赋值的
unInterger.counter = 0;

//每次调用这个函数都会返回一个不同的整数
//它使用一个属性来记住下一次将要返回的值
function unInterger() {
        unInterger.counter++  ; //先返回计数器的值，然后计数器自增1
}
```

下面这个函数`factorrial()`使用了自身的属性（将自身当作数组来对象）来缓存上一次的计算结果。

```js
//计算阶乘，并将结果缓存在函数的属性中
function factorrial(n) {
    if (isFinite(n) && n > 0 && n == Math.round(n)) { //有限的正整数
        if (!(n in factorrial)) //如果没有缓存结果
            factorrial[n] = n * factorrial(n - 1); //计算并缓存之
        return factorrial[n];
    } else return NaN; //如果输入有误
}
factorrial[1] = 1; //初始化缓存以保存这种基本情况
console.log(factorrial())
```

## 8.5 作为命名空间的函数 

在函数中声明的变量在整个函数体内都是可见的（包括在嵌套的函数中），在函数的外部是不可见的。不再任何函数内声明的变量是全局变量，在整个 JavaScript 程序中都是可见的。在 JavaScript 中是无法声明在一个代码块内可见的变量的，基于这个原因，可以简单地定义一个函数用作临时的命名空间，在这个命名空间内定义的变量都不会污染到全局命名空间。

```js
function mymodule() {
    //模块代码
    //这个模块所有使用的所有变量是局部变量
    //而不是污染全局命名空间
}
mymodule(); //不要忘了还要调用的这个函数
```

这段代码仅仅定义了一个单独的全局变量：名为“mymodule”的函数。这样还是太麻烦，可以直接定义一个匿名函数，并在某个表达式中调用它。

```js
(function() { //mymodule函数重写为匿名函数表达式
    //模块代码
}()); //结束函数定义并立即调用它
```

## 8.6 闭包 

和其他大多数现代编程语言一样， JavaScript 也采用词法作用域（lexical scoping），也就是说，函数的执行依赖于变量作用域，这个作用域是在函数定义时决定的，而不是函数调用时决定的。为了实现这种词语作用域， JavaScript 函数对象的内部状态不仅包含函数的代码逻辑，还必须引用当前的作用域链。函数对象可以通过作用域链相互关联起来，函数体内部的变量都可以保存在函数作用域内，这种特性在计算机科学文献中被称为“闭包”。

从技术的角度讲，所有的 JavaScript 函数都是闭包，它们都是对象，它们都关联到作用域链。定义大多数函数时的作用域链在调用函数时依然有效，但这并不影响闭包。当一个函数嵌套了另一个函数，外部函数将嵌套的函数对象作为返回值返回的时候，往往会发生这种事情:调用函数时闭包所指向的作用域链和定义函数时的作用域链不是同一个作用域链。有很多强大的编程技术都利用到了这类嵌套的函数闭包，以至于这种编程模式在 JavaScript 中非常常见。

理解闭包首先要了解嵌套函数的词法作用域规则。

```js
var scope = "global scope"; //全局变量
function checkscope() {
    var scope = "local scope"; //局部变量
    function f() {
            return console.log(scope);
        } //在作用域中返回这个值
    return f();
}
checkscope(); // local scope
```

将函数体内的一对圆括号移动到了`checkscope()`之后。`checkscope()`现在仅仅返回函数体内嵌套的一个函数对象，而不是直接返回结果。

回顾一下词法作用域链的基本规则： JavaScript 函数的执行涉及到作用域链，这个作用域链是函数定义的时候创建的。嵌套的函数`f()`定义在这个作用域链里，其中的变量 scope 一定是局部变量，不管在何时何地执行函数`f()`，这种绑定在执行`f()`时依然有效，因此最后一行代码返回“local scope”。简言之，闭包的这个特性强大到让人吃惊：它们可以捕捉到局部变量（和参数），并一直保存下来，看起来像这些变量绑定到了在其中定义它们的外部函数。

```js
var scope = "global scope"; //全局变量
function checkscope() {
    var scope = "local scope"; //局部变量
    function f() {
            return console.log(scope);
        } //在作用域中返回这个值
    return f;
}
checkscope()(); // local scope
```

> 实现闭包。函数定义时的作用域链到函数执行时依然有效。往往我们觉得在外部函数中定义的局部变量在函数返回后就不存在了，那么嵌套的函数如何能调用不存在的作用域链呢？但其实这是错的。

> 我们将作用域链描述为一个对象列表，不是绑定的栈。每次调用 JavaScript 函数的时候，都会为之创建一个新的对象用来保存局部变量，把这个对象添加至作用域链中。当函数返回的时候，就从作用域链中将这个绑定变量的对象删除。如果不存在嵌套的函数，也没有其他引用指向这个绑定对象，它就会被当作垃圾回收掉。如果定义了嵌套的函数，每个嵌套函数都各自对应一个作用域链，并且这个作用域链指向一个变量绑定对象。如果这些嵌套的函数对象在外部函数中保存下来，那么它们也会和所指向的变量绑定对象一样当作垃圾回收。但是，如果这个函数定义了嵌套的函数，并将它作为返回值返回或者存储在某处的属性里，这时就会有一个外部引用指向这个嵌套的函数。它就不会被当作垃圾回收，并且它所指向的变量绑定对象也不会被当作垃圾回收。

在 8.4.1 节中定义了`uniqueInteger()`函数，这个函数使用自身的一个属性来保存每次返回的值，以便每次调用都能跟踪上次的返回值。但这种做法有一个问题，就是恶意代码可能将计数器重置或者把一个非整数赋值给它，导致该函数不一定能产生唯一的整数。而闭包可以捕捉到单个函数调用的局部变量，并将这些局部变量用作私有状态。

```js
var uniqueInteger = (function() { //定义函数并立即调用
    var counter = 0; //函数的私有状态
    return function() {return counter++;};
}());
```

像 counter 一样的私有变量不是只能用在一个单独的闭包内，在同一个外部函数内定义的多个嵌套函数也可以访问它，这多个嵌套函数都共享一个作用域链。

```js
function counter(){
    var n =0;
    return{
        count: function(){ return n++; },
        reset: function(){ n = 0; }
    };
}
var c = counter(), d = counter(); //创建两个计数器
console.log(c.count())  // =>0
console.log(d.count())  // =>0

c.reset()  // reset()和count方法共享状态
console.log(c.count())  // =>0 因为我们重置了c
console.log(d.count())  // =>1 我们没有重置d
console.log(d.count())  // =>2
```

从技术角度看，其实可以将这个闭包合并为属性存取器方法 getter 和 seter 。

```js
function counter(n) { //函数参数n是一个私有变量
    return {
        //属性getter方法返回并给私有计数器var递增1
        get count() {
            return n++;
        },
        //属性setter方法不允许n递减
        set count(m) {
            if (m >= n) n = m;
            else throw Error("count can only be set to a larger value");
        }
    };
}
var c = counter(1000);
console.log(c.count) //=>1000
console.log(c.count) //=>1001

c.count = 2000
console.log(c.count) //=>2000
console.log(c.count) //=>2001

c.count = 2000 //Error
```

在同一个作用域链中定义两个闭包，这两个闭包共享同样的私有变量或变量。这是一种非常重要的技术，但还是要特别小心那些不希望共享的变量往往不经意间共享给了其他的闭包。

```js
//这个函数返回一个总是返回v的函数
function constfunc(v) {
    return function() { return v; }
};

//创建一个数组用来常数函数
var funcs = [];
for (var i = 0; i < 10; i++) funcs[i] = constfunc(i);

//在第5个位置的元素所表示的函数返回值为5
funcs[5]() //=>5
```

这段代码利用循环创建了很多个闭包，当写类似这种代码的时候往往会犯一个错误，那就是试图将循环代码移入定义这个闭包的函数之内。

```js
//返回一个函数组成的数组，它们的返回值是0-9
function constfuncs() {
    var funcs = [];
    for (var i = 0; i < 10; i++)
        funcs[i] = function() {
            return i;
        };
    return funcs;
}
var funcs = constfuncs();
console.log(funcs[5]()) //10
```

书写闭包的时候还需要注意一件事情， this 是 JavaScript 的关键字，而不是变量。正如之前讨论得，每个函数调用都包含一个 this 值，如果闭包在外部函数里是无法访问 this 的，除非外部函数将 this 转存为一个变量。

```js
var self = this; //将this保存到一个变量中，以便嵌套的函数能够访问它
```

绑定 arguments 的问题与之类似， arguments 并不是一个关键字，但在调用每个函数时都会自动声明它，由于闭包具有自己所绑定的 arguments ，因此闭包内无法直接访问外部函数的参数数组，除非外部函数将参数数组保存到另外一个变量中。

```js
var outerArguments = arguments; //保存起来以便嵌套的函数能使用它
```

## 8.7 函数属性、方法和构造函数 
## 8.8 函数式编程 

# 第9章 类和模块
# 第10章 正则表达式的模式匹配
# 第11章 JavaScript的子集和扩展
# 第12章 服务端JavaScript
# 第二部分 客户端JavaScript
# 第13章 Web浏览器中的JavaScript
# 第14章 Window对象
# 第15章 脚本化文档
# 第16章 脚本化CSS
# 第17章 事件处理
# 第18章 脚本化HTTP
# 第19章 jQuery类库
# 第20章 客户端存储
# 第21章 多媒体和图形编程
# 第22章 HTML5 API
# 第三部分 JavaScript核心参考
# JavaScript核心参考
# 第四部分 客户端JavaScript参考
# 客户端JavaScript参考