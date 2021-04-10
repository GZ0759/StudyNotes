# JavaScript

## 前端性能优化

加载时优化，主要解决的就是让一个网站加载过程更快，比如压缩文件大小、使用CDN加速等方式可以优化加载性能。检查加载性能的指标一般看以下两点，其中主要的脚本代码为 `new Date().getTime() - performance.timing.navigationStart`。

1. 白屏时间。指的是从输入网址，到页面开始显示内容的时间。将代码脚本放在 `</head>` 前面就能获取白屏时间。
2. 首屏时间。指从输入网址，到首屏页面内容渲染完毕的时间。在 `window.onload` 事件中执行脚本代码，可以获取首屏时间。

运行时性能，是指页面运行时的性能表现，而不是页面加载时的性能。可以通过chrome开发者工具中的 Performance 面板来分析页面的运行时性能。

接下来就从加载时性能和运行时性能两个方面来讨论网站优化具体应该怎么做。

### 加载时性能优化
1. DNS 预解析
2. 使用HTTP2
3. 减少HTTP请求数量
4. 压缩、合并文件
5. 采用svg图片或者字体图标
6. 按需加载代码，减少冗余代码
7. 服务器端渲染
8. 使用 Defer 加载JS
9. 静态资源使用 CDN
10. 图片优化

### 运行时性能优化

1. 减少重绘与重排
2. 避免页面卡顿
3. 长列表优化
4. 滚动事件性能优化
5. 使用 Web Workers
6. 写代码时的优化点
  1. 使用事件委托
  2. if-else 对比 switch
  3. 布局上使用flexbox


加载页面和静态资源

- 静态资源的压缩合并，减小资源的大小，减少 http 请求
- 静态资源缓存，
- 使用 CDN 让资源加载更快
- 使用 SSR（服务端渲染）后端渲染，数据直接输出到 HTML 中

页面渲染优化

- CSS 放前面，JS 放后面
- 懒加载（图片懒加载，下拉加载更多）
- 减少 DOM 查询，对 DOM 查询做缓存
- 减少 DOM 操作，多个 DOM 操作尽量合并在一起执行
- 事件节流
- 尽早执行操作（如使用 DOMCotentLoaded）

## typeof 返回数据类型

Undefined、Boolean、Number、String、Function、Object、Symbol

## 异步 ajax 优缺点

优点：不会造成 UI 卡死，用户体验好；局部刷新页面，省流量。

缺点：后退按钮无效，多个请求回调时间不确定，对搜索引擎不友好、数据安全。

## src 与 href

href 表示超文本引用（hypertext reference），在 `<link>` 和 `<a>` 等元素上使用。src 表示来源地址，是指外部资源的位置，指向的内容将会嵌入到文档中当前标签 所在的位置，在 img、script、iframe 等元素上。

## js 垃圾回收方法

标记清除（mark and sweep）

这是 JavaScript 最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了。

引用计数(reference counting)

在低版本 IE 中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个 变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加 1，如果该变量的值变成了另外一个，则这个值得引用次数减 1，当这个值的引用次数变为 0 的时 候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为 0 的值占用的空间。

在 IE 中虽然 JavaScript 对象通过标记清除的方式进行垃圾回收，但 BOM 与 DOM 对象却是通过引用计数回收垃圾的， 也就是说只要涉及 BOM 及 DOM 就会出现循环引用问题。

## 创建 Ajax 的步骤

1. 创建 XMLHttpRequest 对象，也就是创建一个异步调用对象；
2. 创建一个新的 HTTP 请求，并指定改 HTTP 请求的方法、URL 以及验证信息；
3. 设置响应 HTTP 状态变化的函数；
4. 发送 HTTP 请求；
5. 获取异步调用返回的数据；
6. 使用 JavaScript 和 DOM 实现局部刷新；

```js
var xhr;
if (window.XMLHttpRequest) {
  // 标准浏览器
  xhr = new XMLHttpRequest();
} else {
  // IE浏览器
  xhr = ActiveXObject('Microsoft.XMLHTTP');
}

xhr.open('get', 'api/ajax.php', true); // 创建HTTP连接

xhr.oreadystatechange = function () {
  // 响应HTTP状态变化
  if (xhr.readyState == 4) {
    if (xhr.status == 200) {
      var data = xhr.responseText;
    }
  }
};

xhr.send(); // 向服务器发送请求
```

## TypeScript 语法

简单笼统地说，TypeScript 是 JavaScript 的超集，是微软开发的一种脚本语言。和 JavaScript 一样，是现在项目开发中热门的脚本语言。

TypeScript 是一种强类型语言，可编译成 JavaScript，包含了 JavaScript 的所有元素，可以载入 JavaScript 代码运行，扩展了 JavaScript 的语法。相比 JavaScript，TypeScript 是真面向对象，增加了静态类型，类，模块，接口和类型注解。

TypeScript 的编译器很智能，会进行冲突检测，举个例子，一个 enum 的数据，你初始化一个数据，再用一个 switch 语句，编译器会判定其他选项为无效的，会编译错误，直接指出错误原因，这在 JavaScript 是不会指出错误的。

## Web 客户端

主流浏览器的内核。

- IE 浏览器是 Trident
- Mozilla 浏览器是 Gecko
- Safari 浏览器是 Webkit
- Chrome 浏览器是 Blink
- Opera 浏览器现在也是 Blink。

同源策略是对 XHR 的一个主要约束，它为通信设置了“相同的域、相同的端口、相同的协议”这一限制。试图访问上述限制之外的资源，都会引发安全错误，除非采用被认可的跨域解决方案。这个解决方案叫做 CORS（ Cross-Origin Resource Sharing，跨源资源共享）， IE8 通过 XDomainRequest 对象支持 CORS，其他浏览器通过 XHR 对象原生支持 CORS。图像 Ping 和 JSONP 是另外两种跨域通信的技术，但不如 CORS 稳妥。

## 遍历

1. 普通的 for 循环。最简单的一种，正常用的话也不会出现什么问题，想中断也可以中断，性能上也还可以。

```js
var arr = [1, 2, 3];
for (var i = 0; i < arr.length; i++) {
  // 这里的i是代表数组的下标
  console.log(i); // 0, 1, 2
}
```

2. `for in`遍历。这个更多是用来遍历对象，很少用来遍历数组，不过 item 对应与数组的 key 值，建议不要用该方法来遍历数组，因为它的效率是最低的。遍历对象时，可以遍历到 myObject 的原型方法 method,如果不想遍历原型方法和属性的话，可以在循环内部判断一下，hasOwnPropery 方法可以判断某属性是否是该对象的实例属性

```js
// 遍历对象
for (var key in myObject) {
  if (myObject.hasOwnProperty(key)) {
    console.log(key);
  }
}

// 遍历数组
var arr = [1, 2, 3];
for (var item in arr) {
  // item遍历数组时为数组的下标，遍历对象时为对象的key值
  console.log(item); // 0, 1, 2
}
```

`for in`遍历数组的毛病

- index 索引为字符串型数字，不能直接进行几何运算
- 遍历顺序有可能不是按照实际数组的内部顺序
- 使用`for in`会遍历数组所有的可枚举属性，包括原型。例如原型方法 method 和 name 属性

3. ES5 具有遍历数组方法。但是使用 foreach 遍历数组的话，使用 break 不能中断循环，使用 return 也不能返回到外层函数。

方法有`forEach`、`map`、`filter`、`some`、`every`、`reduce`、`reduceRight`等，只不过他们的返回结果不一样。

4. ES6 中的`for of`。这个遍历的是数组元素（键值），不包括数组的原型属性 method 和索引 name 。`for of`适用遍历数、数组对象、字符串、`map`、`set`等拥有迭代器对象的集合.但是不能遍历对象,因为没有迭代器对象。与`forEach()`不同的是，它可以正确响应 break、continue 和 return 语句。

```js
Array.prototype.method = function () {
  console.log(this.length);
};
var myArray = [1, 2, 4, 5, 6, 7];
myArray.name = '数组';
// 1 2 4 5 6 7
for (var value of myArray) {
  console.log(value);
}
```

同样可以通过 ES5 的`Object.keys(myObject)`获取对象的实例属性组成的数组，不包括原型方法和属性。ES2017 引入了跟`Object.keys`配套的`Object.values`和`Object.entries`，作为遍历一个对象的补充手段，供`for of`循环使用。

```js
// Object.keys()
for (var key of Object.keys(someObject)) {
  console.log(key + ': ' + someObject[key]);
}

// 遍历map对象时适合用解构
for (var [key, value] of phoneBookMap) {
  console.log(key + "'s phone number is: " + value);
}
```

`for of`的步骤。`for of`循环首先调用集合的`Symbol.iterator`方法，紧接着返回一个新的迭代器对象。迭代器对象可以是任意具有`.next()`方法的对象；`for of`循环将重复调用这个方法，每次循环调用一次。举个例子，这段代码是能想出来的最简单的迭代器：

```js
var zeroesForeverIterator = {
  [Symbol.iterator]: function () {
    return this;
  },
  next: function () {
    return { done: false, value: 0 };
  },
};
```

## 搜索引擎优化 SEO

搜索引擎优化（Search engine optimization，简称 SEO），指为了提升网页在搜索引擎自然搜索结果中（非商业性推广结果）的收录数量以及排序位置而做的优化行为，是为了从搜索引擎中获得更多的免费流量，以及更好的展现形象。SEM（Search engine marketing，搜索引擎营销），则既包括了 SEO，也包括了付费的商业推广优化。

[原文](https://juejin.im/post/6844903892967227400#heading-15)

### 搜索引擎工作原理

1. 爬虫抓取网页内容。一般爬虫抓取页面内容是先从一个页面出发，从中提取出其他页面的链接，然后当作下一个请求的对象，一直重复这个过程。所以要有良好的 SEO，需要你在各大网站上拥有外链，这样会提高你的网站被搜索引擎爬虫的几率。
2. 分析网页内容。爬虫拿到 HTML 之后，就会对其内容进行分析。一般需要进行去杂、分词、建立索引数据库。什么是索引数据库呢？简单地说就是记录一个词在哪些文档中出现、出现次数、出现的位置等等。为什么要建立索引数据库呢？是为了快速查找。
3. 搜索和排序。搜索会根据你输入的关键词，分别查询其对应的索引数据库，并对结果进行处理和排序。

### 编码阶段 SEO

网站结构要清晰和扁平。结构层数越少越好，一般不要超过三层。

页面应该要有简明的导航。导航可以让搜索引擎知道网站的结构，也可以让搜索引擎知道当前页面在网站结构所在的层次。

同一个页面，只对应一个 url 。多个 url 可以采用 301 进行重定向。

提交 Sitemap。Sitemap 可通知搜索引擎他们网站上有哪些可供抓取的网页，以便搜索引擎可以更加智能地抓取网站。

搜索引擎爬行网站第一个访问的文件就是 robots.txt。在这个文件中声明该网站中不想被蜘蛛访问的部分，这样，该网站的部分或全部内容就可以不被搜索引擎访问和收录了，或者可以通过 robots.txt 指定使搜索引擎只收录指定的内容。

合理的 HTTP 返回码。不同的返回码，搜索引擎的处理逻辑是不一样的。

合适的 title。title 是告诉搜索引擎网页的主要内容。

每个网页应该有一个独一无二的标题，切忌所有的页面都使用默认标题。

description 是对网页内容的精练概括。这个标签存在与否不影响网页权值，只会用做搜索结果摘要的一个选择目标。

HTML 语义化是用标签和属性来描述内容。所以 HTML 语义化是 SEO 的基石。一般建议：

- HTML 结构要清晰和简洁
- 跳转使用`<a>`标签，不要使用 js 跳转
- 图片加 alt 说明
- 文章用`<article>`标签承载

### 单⻚⾯ SEO

目前，对于 SEO 支持比较好的项目方案是采用服务端渲染。所以如果项目有 SEO 需求，那么比较好的方案是服务端渲染。

如果你已经采用了前后分离的单页项目，而你的网站内容不需要 AJAX 去获取内容和展示内容，那么可以试试 prerender-spa-plugin 这个插件，这个插件是一个 webpack 插件，可以帮助你在打包过程中通过无头浏览器去渲染你的页面，并生成对应的 HTML。当然这个方案适合你的路由是静态的，并且路由数量非海量。

如果你的内容是 AJAX 动态获取的，那么 vue 单页项目可以试试 prerender ,这个是一个预渲染服务，可以帮你通过无头浏览器渲染页面，并返回 HTML。这个方案和 prerender-spa-plugin 很相似，都是通过无头浏览器去渲染页面，不同的是渲染的时机，prerender-spa-plugin 是在打包过程中渲染，注定了其只能渲染静态路由，而 prerender 是在请求时渲染，所以可以渲染动态的路由。下面我重点介绍一下 prerender 方案。

首先服务端接收到一个页面的请求，然后判断这个请求是否来自搜索引擎的爬虫，如果不是，则直接返回单页项目的 HTML，按照普通单页项目的工作模式（客户端渲染），如果是，则把请求转发给 prerender 服务，prerender 服务会通过无头浏览器进行预渲染，渲染完成把内容返回，这样爬虫就可以拿到有内容的 HTML 了。prerender 中间件就是用来判断请求是否来自搜索引擎爬虫和转发请求的。

那么 prerender 服务是怎么知道页面渲染已经完成的呢？ Prerender 服务通过计算未完成的请求数量，来确定页面何时完成加载。一旦未完成的请求数达到零，服务会等待一段时间（默认 500ms），然后保存 HTML。

经过实践，请求一个经过 prerender 渲染的页面是时间，快的时候约 2s，慢的时候会长达 8s。一般来说，请求时间在 3s 以内是最好的。所以我从以下几个方面入手，探索 prerender 的优化方法。

减少资源请求的时间
影响 prerender 渲染时间的资源主要有 js 请求资源和 api 请求资源，api 请求时间一般由后端决定，所以我考虑的是如何减少 js 资源请求时间。一般 prerender 服务渲染的资源请求地址是由页面请求 URL 决定的，所以一般是线上的地址，如果我们把 prerender 服务部署在网站的服务器上，让 prerender 服务请求资源走本地，那么就可以缩短资源的请求时间了。

优化 prerender 选项

- pageDoneCheckInterval 检查页面请求是否完成的定时器时间
- waitAfterLastRequest 这个参数是最后一个请求完成之后等待的时间

prerender 插件

- httpHeaders —— 返回合理的 HTTP 状态码
- blockResources —— 无需等待图片资源

自定义渲染结束时间。如果你想更细粒化地控制 prerender 的返回时机，提前结束或者延后结束，那么可以使用这个标志 window.prerenderReady。

开启缓存。缓存这里有两个方面，一方面是 HTTP 缓存（浏览器缓存），另一方面是渲染结果缓存。

统计和监控。统计和监控可以放在中间件的 afterRender 中进行。

## DOM 元素尺寸

### 基本知识

1. 偏移尺寸（offset dimensions）

- offsetHeight ，元素在垂直方向上占用的像素尺寸，包括它的高度、水平滚动条高度（如果可见）和上、下边框的高度。
- offsetLeft ，元素左边框外侧距离包含元素左边框内侧的像素数。
- offsetTop ，元素上边框外侧距离包含元素上边框内侧的像素数。
- offsetWidth ，元素在水平方向上占用的像素尺寸，包括它的宽度、垂直滚动条宽度（如果可见）和左、右边框的宽度。

2. 客户端尺寸（client dimensions）

包含元素内容及其内边距所占用的空间。客户端尺寸只有两个相关属性： clientWidth 和 clientHeight 。其中， clientWidth 是内容区宽度加左、右内边距宽度， clientHeight 是内容区高度加上、下内边距高度。

Element.clientLeft

表示一个元素的左边框的宽度，以像素表示。如果元素的文本方向是从右向左（RTL, right-to-left），并且由于内容溢出导致左边出现了一个垂直滚动条，则该属性包括滚动条的宽度。clientLeft 不包括左外边距和左内边距。clientLeft 是只读的。

Element.clientTop

一个元素顶部边框的宽度（以像素表示）。不包括顶部外边距或内边距。clientTop 是只读的。

3. 滚动尺寸（scroll dimensions）

- scrollHeight ，没有滚动条出现时，元素内容的总高度。
- scrollLeft ，内容区左侧隐藏的像素数，设置这个属性可以改变元素的滚动位置。
- scrollTop ，内容区顶部隐藏的像素数，设置这个属性可以改变元素的滚动位置。
- scrollWidth ，没有滚动条出现时，元素内容的总宽度。

4. 确定元素尺寸

浏览器在每个元素上都暴露了 `getBoundingClientRect()`方法，返回一个 DOMRect 对象，包含 6 个属性： left 、 top 、 right 、 bottom 、 height 和 width 。这些属性给出了元素在页面中相对于视口的位置。

### 常用实例

根据 tab 滚动至相应相应位置

```
i = tab;
scrollTo(0, eles[i].offsetTop)
```

根据滚动位置响应相应 tab

```
eles[i].offsetTop < scrollTop < eles[i+1].offsetTop
tab = i;
```

滚动到底部

```
scrollHeight - scrollTop = clientHeight
```

元素在文档坐标中的位置

```
x = box.getBoundingClientRect().left + document.documentElement.scrollLeft
y = box.getBoundingClientRect().top + document.documentElement.scrollTop
```

元素在文档坐标中的位置（兼容性较强）

```
while(e != null) {
 x += e.offsetLeft;
 y += e.offsetTop;
 e = e.offsetParent;
}
```

元素在文档坐标中的位置（存在滚动和溢出内容）

```
let e1 = e2 = e;
while(e1 != null) {
 x += e1.offsetLeft;
 y += e1.offsetTop;
 e1 = e1.offsetParent;
}

e2 = e2.parentNode;
while(e2 != null && e2.nodeType == 1) {
 x -= e2.scrollLeft;
 y -= e2.scrollTop;
 e2 = e2.offsetParent;
}
```

页面没有滚动条

```
scrollWidth === clientWidth；
scrollHeight === clientHeight；
```

页面存在滚动条

```
scrollWidth > clientWidth；
scrollHeight > clientHeight；
```

确定浏览器视口尺寸

```
document.documentElement.clientWidth
document.documentElement.clientHeight
```
