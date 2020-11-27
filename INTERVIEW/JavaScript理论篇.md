# JavaScript

## 前端优化

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

## GET 请求和 POST 请求。

1. 使用 Get 请求时,参数在 URL 中显示,而使用 Post 请求,则不会显示出来；
2. Post 传输的数据量大，可以达到 2M，而 Get 方法由于受到 URL 长度的限制,只能传递大约 1024 字节.
3. Get 请求请求需注意缓存问题，Post 请求不需担心这个问题；
4. Post 请求必须设置 Content-Type 值为 application/x-form-www-urlencoded；
5. 发送请求时,因为 Get 请求的参数都在 url 里,所以 send 函数发送的参数为 null,而 Post 请求在使用 send 方法时,却需赋予其参数；
6. GET 方式请求的数据会被浏览器缓存起来，因此其他人就可以从浏览器的历史记录中读取到这些数据，例如账号和密码等。在某种情况下，GET 方式会带来严重的安全问题。而 POST 方式相对来说就可以避免这些问题。

## TypeScript 语法

简单笼统地说，TypeScript 是 JavaScript 的超集，是微软开发的一种脚本语言。和 JavaScript 一样，是现在项目开发中热门的脚本语言。

TypeScript 是一种强类型语言，可编译成 JavaScript，包含了 JavaScript 的所有元素，可以载入 JavaScript 代码运行，扩展了 JavaScript 的语法。相比 JavaScript，TypeScript 是真面向对象，增加了静态类型，类，模块，接口和类型注解。

TypeScript 的编译器很智能，会进行冲突检测，举个例子，一个 enum 的数据，你初始化一个数据，再用一个 switch 语句，编译器会判定其他选项为无效的，会编译错误，直接指出错误原因，这在 JavaScript 是不会指出错误的。

## Web 客户端

主流浏览器的内核。IE 浏览器是 Trident，Mozilla 浏览器是 Gecko，Safari 浏览器是 Webkit，Chrome 浏览器是 Blink，Opera 浏览器现在也是 Blink。

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

# 浏览器

## 跨域

跨域是指一个域下的文档或脚本试图去请求另一个域下的资源，这里跨域是广义的。

[参考 1](https://segmentfault.com/a/1190000011145364)  
[参考 1](https://developer.mozilla.org/zh-CN/docs/Web/Security/Same-origin_policy)

1. 资源跳转：`<a>` 链接、重定向、表单提交；
2. 资源嵌入：`<link>`、`<script>`、`<img>`、`<frame>`等 dom 标签，还有样式中 `background:url()`、`@font-face()`等文件外链；
3. 脚本请求：js 发起的 ajax 请求、dom 和 js 对象的跨域操作等；

狭义的跨域：是由浏览器同源策略限制的一类请求场景。

### 同源策略

同源策略（SOP，Same origin policy）是一个重要的安全策略，它用于限制一个 origin 的文档或者它加载的脚本如何能与另一个源的资源进行交互。它能帮助阻隔恶意文档，减少可能被攻击的媒介。

同源策略是一种约定，由 Netscape 公司 1995 年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到 XSS、CSFR 等攻击。所谓同源是指“协议+域名+端口”三者相同，即便两个不同的域名指向同一个 ip 地址，也非同源。

同源策略限制以下几种行为：

1. Cookie、LocalStorage 和 IndexDB 无法读取
2. DOM 和 Js 对象无法获得
3. AJAX 请求不能发送

#### 源的继承

在页面中通过 `about:blank` 或 `javascript:` URL 执行的脚本会继承打开该 URL 的文档的源，因为这些类型的 URLs 没有包含源服务器的相关信息。例如，`about:blank` 通常作为父脚本写入内容的新的空白弹出窗口的 URL（例如，通过 `Window.open()` ）。 如果此弹出窗口也包含 JavaScript，则该脚本将从创建它的脚本那里继承对应的源。

#### IE 中的特例

Internet Explorer 的同源策略有两个主要的差异点：

- 授信范围（Trust Zones）：两个相互之间高度互信的域名，如公司域名（corporate domains），则不受同源策略限制。
- 端口：IE 未将端口号纳入到同源策略的检查中，因此 `https://company.com:81/index.html` 和 `https://company.com/index.html` 属于同源并且不受任何限制。

这些差异点是不规范的，其它浏览器也未做出支持。

### 跨域解决方案

#### JSONP 跨域

Jsonp（JSON with Padding） 是 json 的一种"使用模式"，可以让网页从别的域名（网站）那获取资料，即跨域读取数据。

实现原理：基于两个条件：网页允许资源嵌入，且资源路径不受限制；网页使用 js 有三种方式，HTML 标签上`javascript:xxx`、`<script>`标签内和`<script>`标签外链。JSONP 就是利用这种标签外链，通过请求其他域下的服务，返回一个携带结果数据的 JS 执行函数。

jsonp 缺点：只能实现 get 一种请求。

通常为了减轻 web 服务器的负载，我们把 js、css，img 等静态资源分离到另一台独立域名的服务器上，在 html 页面中再通过相应的标签从不同域名下加载静态资源，而被浏览器允许，基于此原理，我们可以通过动态创建 script，再请求一个带参网址实现跨域通信。这个方法需要客户端和服务端的配合才能完成。

客户端：

```html
<script>
  let script = document.createElement('script');
  script.type = 'text/javascript';
  // 传参一个回调函数名给后端，方便后端返回时执行这个在前端定义的回调函数
  script.src = 'http://127.0.0.1:3000/jsonp?callback=' + handleCallback;
  document.head.appendChild(script);

  // 回调执行函数
  function handleCallback(res) {
    // console.log(JSON.stringify(res));
    console.log(res);
  }
</script>
```

服务端：

```js
let express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('hello world');
});

app.get('/jsonp', (req, res) => {
  let arr = [
    { name: 'andy', age: 18 },
    { name: 'wudi', age: 19 },
    { name: 'akl', age: 20 },
    { name: 'lks', age: 21 },
    { name: 'aike', age: 22 },
    { name: 'jojo', age: 23 },
  ];
  //令客户端执行handleCallback函数
  const request = `handleCallback(${JSON.stringify(arr)})`;
  res.send(request);
});

app.listen(3000, function () {
  console.log('server is running!');
});
```

#### CORS 跨域资源共享

普通跨域请求：只服务端设置 Access-Control-Allow-Origin 即可，前端无须设置，若要带 cookie 请求：前后端都需要设置。

需注意的是：由于同源策略的限制，所读取的 cookie 为跨域请求接口所在域的 cookie，而非当前页。

目前，所有浏览器都支持该功能，IE8/9 需要使用 XDomainRequest 对象来支持，CORS 也已经成为主流的跨域解决方案。

前端设置：

```js
// 原生 ajax
xhr.withCredentials = true; // 前端设置是否带cookie

// jQuery ajax
$.ajax({
  // 前端设置是否带cookie
  xhrFields: { withCredentials: true },
  // 会让请求头中包含跨域的额外信息，但不会含cookie
  crossDomain: true,
});

// axios
axios.defaults.withCredentials = true;
```

服务端设置：

```js
// java
// 允许跨域访问的域名：若有端口需写全（协议+域名+端口），若没有端口末尾不用加'/'
response.setHeader('Access-Control-Allow-Origin', 'http://www.domain1.com');
// 允许前端带认证cookie：启用此项后，上面的域名不能为'*'，必须指定具体的域名，否则浏览器会提示
response.setHeader('Access-Control-Allow-Credentials', 'true');
// 提示OPTIONS预检时，后端需要设置的两个常用自定义头
response.setHeader(
  'Access-Control-Allow-Headers',
  'Content-Type,X-Requested-With'
);

// Nodejs
req.addListener('end', function () {
  postData = qs.parse(postData);
  // 跨域后台设置
  res.writeHead(200, {
    'Access-Control-Allow-Credentials': 'true', // 后端允许发送Cookie
    'Access-Control-Allow-Origin': 'http://www.domain1.com', // 允许访问的域（协议+域名+端口）
    'Set-Cookie': 'l=a123456;Path=/;Domain=www.domain2.com;HttpOnly', // HttpOnly的作用是让js无法读取cookie
  });
  res.write(JSON.stringify(postData));
  res.end();
});
```

#### iframe 嵌套页面

HTML 内联框架元素 `<iframe>` 表示嵌套的 browsing context。它能够将另一个 HTML 页面嵌入到当前页面中。

1. document.domain 和 iframe

此方案仅限主域相同，子域不同的跨域应用场景。实现原理：两个页面都通过 js 强制设置 document.domain 为基础主域，就实现了同域。

```html
<!-- 父窗口：http://www.domain.com/a.html -->
<iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
<script>
  document.domain = 'domain.com';
  var user = 'admin';
</script>
```

```html
<!-- 子窗口：http://child.domain.com/b.html -->
<script>
  document.domain = 'domain.com';
  // 获取父窗口中变量
  alert('get js data from parent ---> ' + window.parent.user);
</script>
```

实际运用，在主站 `www.abc.com` 中打开弹框登录 `login.abc.com` 窗口，这时候两个子域之间沟通可以通过设置 domain 为父域值来实现数据交换。

2. location.hash 和 iframe

实现原理： a 欲与 b 跨域相互通信，通过中间页 c 来实现。 三个页面，不同域之间利用 iframe 的 location.hash 传值，相同域之间直接 js 访问来通信。

具体实现： a 与 b 不同域只能通过 hash 值单向通信，b 与 c 也不同域也只能单向通信，但 c 与 a 同域，所以 c 可通过 parent.parent 访问 a 页面所有对象。

```html
<!-- a.html：http://www.domain1.com/a.html -->
<iframe
  id="iframe"
  src="http://www.domain2.com/b.html"
  style="display:none;"
></iframe>
<script>
  var iframe = document.getElementById('iframe');
  // 向b.html传hash值
  setTimeout(function () {
    iframe.src = iframe.src + '#user=admin';
  }, 1000);
  // 开放给同域c.html的回调方法
  function onCallback(res) {
    alert('data from c.html ---> ' + res);
  }
</script>
```

```html
<!-- b.html：http://www.domain2.com/b.html -->
<iframe
  id="iframe"
  src="http://www.domain1.com/c.html"
  style="display:none;"
></iframe>
<script>
  var iframe = document.getElementById('iframe');
  // 监听a.html传来的hash值，再传给c.html
  window.onhashchange = function () {
    iframe.src = iframe.src + location.hash;
  };
</script>
```

```html
<!-- c.html：http://www.domain1.com/c.html -->
<script>
  // 监听b.html传来的hash值
  window.onhashchange = function () {
    // 再通过操作同域a.html的js回调，将结果传回
    window.parent.parent.onCallback(
      'hello: ' + location.hash.replace('#user=', '')
    );
  };
</script>
```

3. window.name 和 iframe

window.name 属性的独特之处：name 值在不同的页面（甚至不同域名）加载后依旧存在，并且可以支持非常长的 name 值（2MB）。

```js
// a.html：http://www.domain1.com/a.html
var proxy = function (url, callback) {
  var state = 0;
  var iframe = document.createElement('iframe');
  // 加载跨域页面
  iframe.src = url;
  // onload事件会触发2次，第1次加载跨域页，并留存数据于window.name
  iframe.onload = function () {
    if (state === 1) {
      // 第2次onload(同域proxy页)成功后，读取同域window.name中数据
      callback(iframe.contentWindow.name);
      destoryFrame();
    } else if (state === 0) {
      // 第1次onload(跨域页)成功后，切换到同域代理页面
      iframe.contentWindow.location = 'http://www.domain1.com/proxy.html';
      state = 1;
    }
  };
  document.body.appendChild(iframe);
  // 获取数据以后销毁这个iframe，释放内存；这也保证了安全（不被其他域frame js访问）
  function destoryFrame() {
    iframe.contentWindow.document.write('');
    iframe.contentWindow.close();
    document.body.removeChild(iframe);
  }
};
// 请求跨域b页面数据
proxy('http://www.domain2.com/b.html', function (data) {
  alert(data);
});
```

```html
<!-- proxy.html：http://www.domain1.com/proxy.html -->
<!-- 中间代理页，与 a.html 同域，内容为空即可。 -->
```

```html
<!-- b.html：http://www.domain2.com/b.html -->
<script>
  window.name = 'This is domain2 data!';
</script>
```

总结：通过 iframe 的 src 属性由外域转向本地域，跨域数据即由 iframe 的 window.name 从外域传递到本地域。这个就巧妙地绕过了浏览器的跨域访问限制，但同时它又是安全操作。

#### postMessage 跨域

postMessage 是 HTML5 XMLHttpRequest Level 2 中的 API，且是为数不多可以跨域操作的 window 属性之一，它可用于解决以下方面的问题：

1. 页面和其打开的新窗口的数据传递
2. 多窗口之间消息传递
3. 页面与嵌套的 iframe 消息传递
4. 上面三个场景的跨域数据传递

用法：`postMessage()`方法接受两个参数

1. data： html5 规范支持任意基本类型或可复制的对象，但部分浏览器只支持字符串，所以传参时最好用 JSON 序列化。
2. origin： 协议+主机+端口号，也可以设置为"\*"，表示可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。

```html
<!-- a.html：http://www.domain1.com/a.html -->
<iframe
  id="iframe"
  src="http://www.domain2.com/b.html"
  style="display:none;"
></iframe>
<script>
  var iframe = document.getElementById('iframe');
  iframe.onload = function () {
    var data = {
      name: 'aym',
    };
    // 向domain2传送跨域数据
    iframe.contentWindow.postMessage(
      JSON.stringify(data),
      'http://www.domain2.com'
    );
  };
  // 接受domain2返回数据
  window.addEventListener(
    'message',
    function (e) {
      alert('data from domain2 ---> ' + e.data);
    },
    false
  );
</script>
```

```html
<!-- b.html：http://www.domain2.com/b.html -->
<script>
  // 接收domain1的数据
  window.addEventListener(
    'message',
    function (e) {
      alert('data from domain1 ---> ' + e.data);
      var data = JSON.parse(e.data);
      if (data) {
        data.number = 16;
        // 处理后再发回domain1
        window.parent.postMessage(
          JSON.stringify(data),
          'http://www.domain1.com'
        );
      }
    },
    false
  );
</script>
```

实际运用：

域 1 下的 react 项目中：

```js
  componentDidMount() {
    this.getDetailUrl();
    window.addEventListener("message", this.receiveMessage, false);
  }
  ...
  // 向iframe发送数据
  sendPostMessage(data, name) {
    //必须是iframe加载完成后才可以向子域发送数据
    const childFrameObj = document.getElementById('Model');
    childFrameObj.contentWindow.postMessage({data, name}, this.state.postMesUrl);
  };
  ...
  receiveMessage = (event) => {
    if (event !== undefined && event.data && event.data.name) {
      var eventData = event.data;
      ...
    }
  };
```

域 2 下的 jquery 项目中：

```js
var evt = window.event;
var postMessageUrl = 'https://xxx.xxx.com';
//监听message事件 接收react传过来的参数
window.addEventListener('message', receiveMessageFromReact, false);
//向react发送数据
function transmitData(data) {
  parent.postMessage(data, postMessageUrl); //window.postMessage
}
/*search*/
var searchResult = function () {
  var initData = {
    name: 'search',
    data: {
      keyword: $('input[name=keyword]').val(),
    },
  };
  transmitData(initData);
};
$('.J-search-btn').click(function (e) {
  e.preventDefault();
  searchResult();
});
$('input[name=keyword]').on('keyup', function (e) {
  if (e.keyCode === 13) {
    searchResult();
  }
});
```

#### WebSocket 协议跨域

WebSocket protocol 是 HTML5 一种新的协议。它实现了浏览器与服务器全双工通信，同时允许跨域通讯，是 server push 技术的一种很好的实现。

原生 WebSocket API 使用起来不太方便，我们使用 Socket.io，它很好地封装了 webSocket 接口，提供了更简单、灵活的接口，也对不支持 webSocket 的浏览器提供了向下兼容。

前端代码：

```html
<div>user input：<input type="text" /></div>
<script src="https://cdn.bootcss.com/socket.io/2.2.0/socket.io.js"></script>
<script>
  var socket = io('http://www.domain2.com:8080');
  // 连接成功处理
  socket.on('connect', function () {
    // 监听服务端消息
    socket.on('message', function (msg) {
      console.log('data from server: ---> ' + msg);
    });
    // 监听服务端关闭
    socket.on('disconnect', function () {
      console.log('Server socket has closed.');
    });
  });
  document.getElementsByTagName('input')[0].onblur = function () {
    socket.send(this.value);
  };
</script>
```

Nodejs socket 后台：

```js
var http = require('http');
var socket = require('socket.io');
// 启http服务
var server = http.createServer(function(req, res) {
    res.writeHead(200, {
        'Content-type': 'text/html'
    });
    res.end();
});
server.listen('8080');
console.log('Server is running at port 8080...');
// 监听socket连接
socket.listen(server).on('connection', function(client) {
    // 接收信息
    client.on('message', function(msg) {
        client.send('hello：' + msg);
        console.log('data from client: ---> ' + msg);
    });
    // 断开处理
    client.on('disconnect', function() {
        console.log('Client socket has closed.');
    });
```

#### nginx 代理跨域

1. nginx 配置解决 iconfont 跨域

浏览器跨域访问 js、css、img 等常规静态资源被同源策略许可，但 iconfont 字体文件 eot/otf/ttf/woff/svg 例外，此时可在 nginx 的静态资源服务器中加入以下配置。

```xml
location / {
  add_header Access-Control-Allow-Origin *;
}
```

2. nginx 反向代理接口跨域

跨域原理： 同源策略是浏览器的安全策略，不是 HTTP 协议的一部分。服务器端调用 HTTP 接口只是使用 HTTP 协议，不会执行 JS 脚本，不需要同源策略，也就不存在跨越问题。

实现思路：通过 nginx 配置一个代理服务器（域名与 domain1 相同，端口不同）做跳板机，反向代理访问 domain2 接口，并且可以顺便修改 cookie 中 domain 信息，方便当前域 cookie 写入，实现跨域登录。
nginx 具体配置：

```xml
#proxy服务器
server {
    listen       81;
    server_name  www.domain1.com;
    location / {
        proxy_pass   http://www.domain2.com:8080;  #反向代理
        proxy_cookie_domain www.domain2.com www.domain1.com; #修改cookie里域名
        index  index.html index.htm;
        # 当用webpack-dev-server等中间件代理接口访问nignx时，此时无浏览器参与，故没有同源限制，下面的跨域配置可不启用
        add_header Access-Control-Allow-Origin http://www.domain1.com;  #当前端只跨域不带cookie时，可为*
        add_header Access-Control-Allow-Credentials true;
    }
}
```

前端代码示例：

```js
var xhr = new XMLHttpRequest();
// 前端开关：浏览器是否读写cookie
xhr.withCredentials = true;
// 访问nginx中的代理服务器
xhr.open('get', 'http://www.domain1.com:81/?user=admin', true);
xhr.send();
```

Nodejs 后台示例：

```js
var http = require('http');
var server = http.createServer();
var qs = require('querystring');
server.on('request', function (req, res) {
  var params = qs.parse(req.url.substring(2));
  // 向前台写cookie
  res.writeHead(200, {
    'Set-Cookie': 'l=a123456;Path=/;Domain=www.domain2.com;HttpOnly', // HttpOnly:脚本无法读取
  });
  res.write(JSON.stringify(params));
  res.end();
});
server.listen('8080');
console.log('Server is running at port 8080...');
```

#### Nodejs 中间件代理跨域

node 中间件实现跨域代理，原理大致与 nginx 相同，都是通过启一个代理服务器，实现数据的转发，也可以通过设置 cookieDomainRewrite 参数修改响应头中 cookie 中域名，实现当前域的 cookie 写入，方便接口登录认证。

利用 node + express + http-proxy-middleware 搭建一个 proxy 服务器。

前端代码示例：

```js
var xhr = new XMLHttpRequest();
// 前端开关：浏览器是否读写cookie
xhr.withCredentials = true;
// 访问http-proxy-middleware代理服务器
xhr.open('get', 'http://www.domain1.com:3000/login?user=admin', true);
xhr.send();
```

中间件服务器：

```js
var express = require('express');
var proxy = require('http-proxy-middleware');
var app = express();
app.use(
  '/',
  proxy({
    // 代理跨域目标接口
    target: 'http://www.domain2.com:8080',
    changeOrigin: true,
    // 修改响应头信息，实现跨域并允许带cookie
    onProxyRes: function (proxyRes, req, res) {
      res.header('Access-Control-Allow-Origin', 'http://www.domain1.com');
      res.header('Access-Control-Allow-Credentials', 'true');
    },
    // 修改响应信息中的cookie域名
    cookieDomainRewrite: 'www.domain1.com', // 可以为false，表示不修改
  })
);
app.listen(3000);
console.log('Proxy server is listen at port 3000...');
```

Nodejs 后台（同 nginx）

## 浏览器缓存

缓存可以说是性能优化中简单高效的一种优化方式了。一个优秀的缓存策略可以缩短网页请求资源的距离，减少延迟，并且由于缓存文件可以重复利用，还可以减少带宽，降低网络负荷。

对于一个数据请求来说，可以分为发起网络请求、后端处理、浏览器响应三个步骤。浏览器缓存可以帮助我们在第一和第三步骤中优化性能。比如说直接使用缓存而不发起请求，或者发起了请求但后端存储的数据和前端一致，那么就没有必要再将数据回传回来，这样就减少了响应数据。

[参考](https://www.jianshu.com/p/54cc04190252)

### 缓存位置

从缓存位置上来说分为四种，并且各自有优先级，当依次查找缓存且都没有命中的时候，才会去请求网络。

1. Service Worker
2. Memory Cache
3. Disk Cache
4. Push Cache

**Service Worker**

Service Worker 是运行在浏览器背后的独立线程，一般可以用来实现缓存功能。使用 Service Worker 的话，传输协议必须为 HTTPS。因为 Service Worker 中涉及到请求拦截，所以必须使用 HTTPS 协议来保障安全。Service Worker 的缓存与浏览器其他内建的缓存机制不同，它可以让我们自由控制缓存哪些文件、如何匹配缓存、如何读取缓存，并且缓存是持续性的。

Service Worker 实现缓存功能一般分为三个步骤：首先需要先注册 Service Worker，然后监听到 install 事件以后就可以缓存需要的文件，那么在下次用户访问的时候就可以通过拦截请求的方式查询是否存在缓存，存在缓存的话就可以直接读取缓存文件，否则就去请求数据。

当 Service Worker 没有命中缓存的时候，我们需要去调用 fetch 函数获取数据。也就是说，如果我们没有在 Service Worker 命中缓存的话，会根据缓存查找优先级去查找数据。但是不管我们是从 Memory Cache 中还是从网络请求中获取的数据，浏览器都会显示我们是从 Service Worker 中获取的内容。

**Memory Cache**

Memory Cache 也就是内存中的缓存，主要包含的是当前中页面中已经抓取到的资源,例如页面上已经下载的样式、脚本、图片等。读取内存中的数据肯定比磁盘快,内存缓存虽然读取高效，可是缓存持续性很短，会随着进程的释放而释放。 一旦我们关闭 Tab 页面，内存中的缓存也就被释放了。

那么既然内存缓存这么高效，我们是不是能让数据都存放在内存中呢？这是不可能的。计算机中的内存一定比硬盘容量小得多，操作系统需要精打细算内存的使用，所以能让我们使用的内存必然不多。

当我们访问过页面以后，再次刷新页面，可以发现很多数据都来自于内存缓存。

内存缓存中有一块重要的缓存资源是 preloader 相关指令（例如`<link rel="prefetch">`）下载的资源。总所周知 preloader 的相关指令已经是页面优化的常见手段之一，它可以一边解析 js/css 文件，一边网络请求下一个资源。

需要注意的事情是，内存缓存在缓存资源时并不关心返回资源的 HTTP 缓存头 Cache-Control 是什么值，同时资源的匹配也并非仅仅是对 URL 做匹配，还可能会对 Content-Type，CORS 等其他特征做校验。

**Disk Cache**

Disk Cache 也就是存储在硬盘中的缓存，读取速度慢点，但是什么都能存储到磁盘中，比之 Memory Cache 胜在容量和存储时效性上。

在所有浏览器缓存中，Disk Cache 覆盖面基本是最大的。它会根据 HTTP Herder 中的字段判断哪些资源需要缓存，哪些资源可以不请求直接使用，哪些资源已经过期需要重新请求。并且即使在跨站点的情况下，相同地址的资源一旦被硬盘缓存下来，就不会再次去请求数据。绝大部分的缓存都来自 Disk Cache，关于 HTTP 的协议头中的缓存字段，我们会在下文进行详细介绍。

浏览器会把哪些文件丢进内存中？哪些丢进硬盘中？关于这点，网上说法不一，不过以下观点比较靠得住：对于大文件来说，大概率是不存储在内存中的，反之优先；当前系统内存使用率高的话，文件优先存储进硬盘。

**Push Cache**

Push Cache（推送缓存）是 HTTP/2 中的内容，当以上三种缓存都没有命中时，它才会被使用。它只在会话（Session）中存在，一旦会话结束就被释放，并且缓存时间也很短暂，在 Chrome 浏览器中只有 5 分钟左右，同时它也并非严格执行 HTTP 头中的缓存指令。

Push Cache 在国内能够查到的资料很少，也是因为 HTTP/2 在国内不够普及。这里推荐阅读 Jake Archibald 的 HTTP/2 push is tougher than I thought 这篇文章，文章中的几个结论：

- 所有的资源都能被推送，并且能够被缓存,但是 Edge 和 Safari 浏览器支持相对比较差
- 可以推送 no-cache 和 no-store 的资源
- 一旦连接被关闭，Push Cache 就被释放
- 多个页面可以使用同一个 HTTP/2 的连接，也就可以使用同一个 Push Cache。这主要还是依赖浏览器的实现而定，出于对性能的考虑，有的浏览器会对相同域名但不同的 tab 标签使用同一个 HTTP 连接。
- Push Cache 中的缓存只能被使用一次
- 浏览器可以拒绝接受已经存在的资源推送
- 你可以给其他域名推送资源

如果以上四种缓存都没有命中的话，那么只能发起请求来获取资源了。

那么为了性能上的考虑，大部分的接口都应该选择好缓存策略，通常浏览器缓存策略分为两种：强缓存和协商缓存，并且缓存策略都是通过设置 HTTP Header 来实现的。

### 缓存过程分析

浏览器与服务器通信的方式为应答模式，即是：浏览器发起 HTTP 请求 – 服务器响应该请求，那么浏览器怎么确定一个资源该不该缓存，如何去缓存呢？浏览器第一次向服务器发起该请求后拿到请求结果后，将请求结果和缓存标识存入浏览器缓存，浏览器对于缓存的处理是根据第一次请求资源时返回的响应头来确定的。具体过程如下：

1. 浏览器 发起一次 HTTP 请求
2. 浏览器缓存 告诉浏览器这边没有该请求的缓存结果和缓存标识
3. 浏览器 向 服务器 发起 HTTP 请求
4. 服务器 返回该请求结果和缓存规则
5. 浏览器 将该请求结果和缓存标识存入浏览器缓存中

- 浏览器每次发起请求，都会先在浏览器缓存中查找该请求的结果以及缓存标识
- 浏览器每次拿到返回的请求结果都会将该结果和缓存标识存入浏览器缓存中

以上两点结论就是浏览器缓存机制的关键，它确保了每个请求的缓存存入与读取，只要我们再理解浏览器缓存的使用规则，那么所有的问题就迎刃而解了，本文也将围绕着这点进行详细分析。为了方便大家理解，这里我们根据是否需要向服务器重新发起 HTTP 请求将缓存过程分为两个部分，分别是强缓存和协商缓存。

### 强缓存

强缓存：不会向服务器发送请求，直接从缓存中读取资源，在 chrome 控制台的 Network 选项中可以看到该请求返回 200 的状态码，并且 Size 显示 from disk cache 或 from memory cache。强缓存可以通过设置两种 HTTP Header 实现：Expires 和 Cache-Control。

1. Expires

缓存过期时间，用来指定资源到期的时间，是服务器端的具体的时间点。也就是说，Expires=max-age + 请求时间，需要和 Last-modified 结合使用。Expires 是 Web 服务器响应消息头字段，在响应 http 请求时告诉浏览器在过期时间前浏览器可以直接从浏览器缓存取数据，而无需再次请求。

Expires 是 HTTP/1 的产物，受限于本地时间，如果修改了本地时间，可能会造成缓存失效。Expires: Wed, 22 Oct 2018 08:41:00 GMT 表示资源会在 Wed, 22 Oct 2018 08:41:00 GMT 后过期，需要再次请求。

2. Cache-Control

在 HTTP/1.1 中，Cache-Control 是最重要的规则，主要用于控制网页缓存。比如当 Cache-Control:max-age=300 时，则代表在这个请求正确返回时间（浏览器也会记录下来）的 5 分钟内再次加载资源，就会命中强缓存。

Cache-Control 可以在请求头或者响应头中设置，并且可以组合使用多种指令：

public：所有内容都将被缓存（客户端和代理服务器都可缓存）。具体来说响应可被任何中间节点缓存，如 Browser <-- proxy1 <-- proxy2 <-- Server，中间的 proxy 可以缓存资源，比如下次再请求同一资源 proxy1 直接把自己缓存的东西给 Browser 而不再向 proxy2 要。

private：所有内容只有客户端可以缓存，Cache-Control 的默认取值。具体来说，表示中间节点不允许缓存，对于 Browser <-- proxy1 <-- proxy2 <-- Server，proxy 会老老实实把 Server 返回的数据发送给 proxy1,自己不缓存任何数据。当下次 Browser 再次请求时 proxy 会做好请求转发而不是自作主张给自己缓存的数据。

no-cache：客户端缓存内容，是否使用缓存则需要经过协商缓存来验证决定。表示不使用 Cache-Control 的缓存控制方式做前置验证，而是使用 Etag 或者 Last-Modified 字段来控制缓存。需要注意的是，no-cache 这个名字有一点误导。设置了 no-cache 之后，并不是说浏览器就不再缓存数据，只是浏览器在使用缓存数据时，需要先确认一下数据是否还跟服务器保持一致。

no-store：所有内容都不会被缓存，即不使用强制缓存，也不使用协商缓存

max-age：max-age=xxx (xxx is numeric)表示缓存内容将在 xxx 秒后失效

s-maxage（单位为 s）：同 max-age 作用一样，只在代理服务器中生效（比如 CDN 缓存）。比如当 s-maxage=60 时，在这 60 秒中，即使更新了 CDN 的内容，浏览器也不会进行请求。max-age 用于普通缓存，而 s-maxage 用于代理缓存。s-maxage 的优先级高于 max-age。如果存在 s-maxage，则会覆盖掉 max-age 和 Expires header。

max-stale：能容忍的最大过期时间。max-stale 指令标示了客户端愿意接收一个已经过期了的响应。如果指定了 max-stale 的值，则最大容忍时间为对应的秒数。如果没有指定，那么说明浏览器愿意接收任何 age 的响应（age 表示响应由源站生成或确认的时间与当前时间的差值）。

min-fresh：能够容忍的最小新鲜度。min-fresh 标示了客户端不愿意接受新鲜度不多于当前的 age 加上 min-fresh 设定的时间之和的响应。
cache-control

从图中我们可以看到，我们可以将多个指令配合起来一起使用，达到多个目的。比如说我们希望资源能被缓存下来，并且是客户端和代理服务器都能缓存，还能设置缓存失效时间等等。

3. Expires 和 Cache-Control 两者对比

其实这两者差别不大，区别就在于 Expires 是 http1.0 的产物，Cache-Control 是 http1.1 的产物，两者同时存在的话，Cache-Control 优先级高于 Expires；在某些不支持 HTTP1.1 的环境下，Expires 就会发挥用处。所以 Expires 其实是过时的产物，现阶段它的存在只是一种兼容性的写法。

强缓存判断是否缓存的依据来自于是否超出某个时间或者某个时间段，而不关心服务器端文件是否已经更新，这可能会导致加载文件不是服务器端最新的内容，那我们如何获知服务器端内容是否已经发生了更新呢？此时我们需要用到协商缓存策略。

### 协商缓存

协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程，主要有以下两种情况：

1. 协商缓存生效，返回 304 和 Not Modified
2. 协商缓存失效，返回 200 和请求结果

协商缓存可以通过设置两种 HTTP Header 实现：Last-Modified 和 ETag 。

**Last-Modified 和 If-Modified-Since**

浏览器在第一次访问资源时，服务器返回资源的同时，在 response header 中添加 Last-Modified 的 header，值是这个资源在服务器上的最后修改时间，浏览器接收后缓存文件和 header；

Last-Modified: Fri, 22 Jul 2016 01:47:00 GMT
浏览器下一次请求这个资源，浏览器检测到有 Last-Modified 这个 header，于是添加 If-Modified-Since 这个 header，值就是 Last-Modified 中的值；服务器再次收到这个资源请求，会根据 If-Modified-Since 中的值与服务器中这个资源的最后修改时间对比，如果没有变化，返回 304 和空的响应体，直接从缓存读取，如果 If-Modified-Since 的时间小于服务器中这个资源的最后修改时间，说明文件有更新，于是返回新的资源文件和 200

但是 Last-Modified 存在一些弊端：
如果本地打开缓存文件，即使没有对文件进行修改，但还是会造成 Last-Modified 被修改，服务端不能命中缓存导致发送相同的资源
因为 Last-Modified 只能以秒计时，如果在不可感知的时间内修改完成文件，那么服务端会认为资源还是命中了，不会返回正确的资源
既然根据文件修改时间来决定是否缓存尚有不足，能否可以直接根据文件内容是否修改来决定缓存策略？所以在 HTTP / 1.1 出现了 ETag 和 If-None-Match

**ETag 和 If-None-Match**

Etag 是服务器响应请求时，返回当前资源文件的一个唯一标识(由服务器生成)，只要资源有变化，Etag 就会重新生成。浏览器在下一次加载资源向服务器发送请求时，会将上一次返回的 Etag 值放到 request header 里的 If-None-Match 里，服务器只需要比较客户端传来的 If-None-Match 跟自己服务器上该资源的 ETag 是否一致，就能很好地判断资源相对客户端而言是否被修改过了。如果服务器发现 ETag 匹配不上，那么直接以常规 GET 200 回包形式将新的资源（当然也包括了新的 ETag）发给客户端；如果 ETag 是一致的，则直接返回 304 知会客户端直接使用本地缓存即可。

ETag 和 If-None-Match

**两者之间对比：**

首先在精确度上，Etag 要优于 Last-Modified。
Last-Modified 的时间单位是秒，如果某个文件在 1 秒内改变了多次，那么他们的 Last-Modified 其实并没有体现出来修改，但是 Etag 每次都会改变确保了精度；如果是负载均衡的服务器，各个服务器生成的 Last-Modified 也有可能不一致。

第二在性能上，Etag 要逊于 Last-Modified，毕竟 Last-Modified 只需要记录时间，而 Etag 需要服务器通过算法来计算出一个 hash 值。
第三在优先级上，服务器校验优先考虑 Etag

### 缓存机制

强制缓存优先于协商缓存进行，若强制缓存（Expires 和 Cache-Control）生效则直接使用缓存，若不生效则进行协商缓存（Last-Modified / If-Modified-Since 和 Etag / If-None-Match），协商缓存由服务器决定是否使用缓存，若协商缓存失效，那么代表该请求的缓存失效，返回 200，重新返回资源和缓存标识，再存入浏览器缓存中；生效则返回 304，继续使用缓存。具体流程图如下：

缓存的机制

看到这里，不知道你是否存在这样一个疑问:如果什么缓存策略都没设置，那么浏览器会怎么处理？

对于这种情况，浏览器会采用一个启发式的算法，通常会取响应头中的 Date 减去 Last-Modified 值的 10% 作为缓存时间。

### 实际场景应用缓存策略

1. 频繁变动的资源

```
Cache-Control: no-cache
```

对于频繁变动的资源，首先需要使用 Cache-Control: no-cache 使浏览器每次都请求服务器，然后配合 ETag 或者 Last-Modified 来验证资源是否有效。这样的做法虽然不能节省请求数量，但是能显著减少响应数据大小。

2. 不常变化的资源

```
Cache-Control: max-age=31536000
```

通常在处理这类资源时，给它们的 Cache-Control 配置一个很大的 max-age=31536000 (一年)，这样浏览器之后请求相同的 URL 会命中强制缓存。而为了解决更新的问题，就需要在文件名(或者路径)中添加 hash， 版本号等动态字符，之后更改动态字符，从而达到更改引用 URL 的目的，让之前的强制缓存失效 (其实并未立即失效，只是不再使用了而已)。
在线提供的类库 (如 jquery-3.3.1.min.js, lodash.min.js 等) 均采用这个模式。

### 用户行为对浏览器缓存的影响

所谓用户行为对浏览器缓存的影响，指的就是用户在浏览器如何操作时，会触发怎样的缓存策略。主要有 3 种：

1. 打开网页，地址栏输入地址： 查找 disk cache 中是否有匹配。如有则使用；如没有则发送网络请求。
2. 普通刷新 （F5）：因为 TAB 并没有关闭，因此 memory cache 是可用的，会被优先使用（如果匹配的话）。其次才是 disk cache。
3. 强制刷新 （Ctrl + F5）：浏览器不使用缓存，因此发送的请求头部均带有 `Cache-control: no-cache`，为了兼容，还带了 `Pragma: no-cache`,服务器直接返回 200 和最新内容。

## 事件循环 Event Loop

Event Loop 即事件循环，是指浏览器或 Node 的一种解决 JavaScript 单线程运行时不会阻塞的一种机制，也就是我们经常使用异步的原理。

**单线程和多线程**

JavaScript 是一个单线程的语言。单线程在程序执行时，所走的程序路径按照连续顺序排下来，前面的必须处理好，后面的才会执行。

以 Chrome 浏览器中为例，当你打开一个 Tab 页时，其实就是创建了一个进程。一个进程中可以有多个线程，比如渲染线程、JS 引擎线程、HTTP 请求线程等等。

当你发起一个请求时，其实就是创建了一个线程，当请求结束后，该线程可能就会被销毁。

浏览器内核是怎样的？浏览器内核是多线程的，在内核控制下各线程相互配合以保持同步，一个浏览器通常由以下常驻线程组成：

1. GUI 渲染线程：解析 HTML、CSS 等。在 JavaScript 引擎线程运行脚本期间，GUI 渲染线程处于挂起状态，也就是被 “冻结” 了。
2. JavaScript 引擎线程：负责处理 JavaScript 脚本。
3. 定时触发器线程：setTimeout、setInterval 等。事件触发线程会将计数完毕后的事件加入到任务队列的尾部，等待 JS 引擎线程执行。
4. 事件触发线程：负责将准备好的事件交给 JS 引擎执行。
5. 异步 http 请求线程：负责执行异步请求之类函数的线程，例如 `Promise.then()`、ajax 等。

为什么不设计成多线程？假设有个 DOM 节点，现在有线程 A 操作它，删除了这个 DOM；然后线程 B 又操作它，修改了这个 DOM 某部分。那么现在问题来了，咱听谁的？所以干脆设计成一个单线程，安全稳妥不出事。哪怕后期 HTML5 出了个 Web Worker 也是不允许操作 DOM 结构的，可以完成一些分布式的计算。

**为什么需要异步？**

这时候又有问题了，如果调用某个接口（Ajax），或者加载某张图片的时候，我们卡住了，这样页面是不是就一直不能渲染？

然后因为单线程只能先让前面的程序走完，即便这个接口或者图片缓过来了，我下面还有其他任务没做呢，这不就卡死了么？

所以这时候异步来了：

在涉及某些需要等待的操作的时候，我们就选择让程序继续运行。

等待接口或者图片返回过来后，就通知程序我做好了，你可以继续调用了。

### Event Loop

JavaScript 为了协调事件、用户交互、脚本、渲染、网络等，就搞出来一个 事件循环（Event Loop）。JavaScript 从 script 开始读取，然后不断循环，从 “任务队列” 中读取执行事件的过程，就是 事件循环。

4.1 Event Loop 执行过程

Event Loop 执行过程如下：

1. 一开始整个脚本 script 作为一个宏任务执行
2. 执行过程中，同步代码 直接执行，宏任务 进入宏任务队列，微任务 进入微任务队列。
3. 当前宏任务执行完出队，检查微任务列表，有则依次执行，直到全部执行完毕。
4. 执行浏览器 UI 线程的渲染工作。
5. 检查是否有 Web Worker 任务，有则执行。
6. 执行完本轮的宏任务，回到步骤 2，依次循环，直到宏任务和微任务队列为空。

事件循环中的异步队列有两种：宏任务队列（MacroTask）和 微任务队列（MicroTask）。而 Web Worker 是运行在后台的 JS，独立于其他脚本，不会影响页面的性能。

宏任务队列可以有多个，微任务队列只有一个。

宏任务 包括：

- script
- setTimeout
- setInterval
- setImmediate
- I/O
- UI rendering

微任务 包括：

- MutationObserver
- `Promise.then()`/`catch()`
- 以 Promise 为基础开发的其他技术，例如 fetch API
- V8 的垃圾回收过程
- Node 独有的 process.nextTick

  4.2 requestAnimationFrame

  4.2.1 requestAnimationFrame 介绍

`window.requestAnimationFrame()` 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。

该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。

requestAnimationFrame 简称 rAF。

我们看一下它使用情况：

```html
<body>
  <div class="animation">动画元素</div>

  <script>
    window.onload = function () {
      const element = document.querySelector('.animation');
      let start;

      function step(timestamp) {
        if (start === undefined) {
          start = timestamp;
        }
        const elapsed = timestamp - start;

        // 这里使用 Math.min() 确保元素刚好停在 200px 的位置。
        element.style.transform =
          'translateX(' + Math.min(0.1 * elapsed, 200) + 'px)';

        // 在两秒后停止动画
        if (elapsed < 2000) {
          window.requestAnimationFrame(step);
        }
      }

      window.requestAnimationFrame(step);
    };
  </script>
</body>
```

4.2.2 requestAnimationFrame 使用缘由

如果我们使用 setTimeout 来实现动画效果，那么我们会发现在某些低端机上出现卡顿、抖动的现象，它产生的原因是：

- setTimeout 的执行事件并不是确定的。它属于宏任务队列，只有当主线程上的任务执行完毕后，才会调用队列中的任务判断是否开始执行。
- 刷新频率受屏幕分辨率和屏幕尺寸影响，因此不同设备的刷新频率不同，而 setTimeout 只能固定一个时间间隔刷新。

在上面 Event Loop 的过程中，我们知道执行完微任务队列会有一步操作：执行浏览器 UI 线程的渲染工作。

而 requestAnimationFrame 就在这里边执行，就不会等宏任务队列的排队，从而导致卡顿等问题了。

4.3 Web Worker

Web Worker 为 Web 内容在后台线程中运行脚本提供了一种简单的方法。

如我们所知，JavaScript 一直是属于单线程环境，我们无法同时运行两个 JavaScript 脚本。

但是试想一下，如果我们可以同时运行两个（或者多个）JavaScript 脚本，一个来处理 UI 界面（一直以来的用法），一个来处理一些复杂计算，那么性能就会更好。

在 HTML5 的新规范中，实现了 Web Worker 来引入 JavaScript 的 “多线程” 技术，他的能力让我们可以在页面主运行的 JavaScript 线程中加载运行另外单独的一个或者多个 JavaScript 线程。

注意：JavaScript 本质上还是单线程的，Web Worker 只是浏览器（宿主环境）提供的一个得力 API。

4.3.1 Web Worker 使用

调用 Web Worker：
index.js

```js
console.log('index-同步任务');
Promise.resolve().then((res) => {
  console.log('index-Promise');
});
setTimeout(() => {
  console.log('index-setTimeout');
}, 1000);
```

index.html

```html
<script>
  window.onload = function () {
    console.log('本地-同步任务');
    // 微任务之间
    Promise.resolve().then((res) => {
      console.log('本地-微任务 1');
    });
    const worker1 = new Worker('./index.js');
    Promise.resolve().then((res) => {
      console.log('本地-微任务 2');
    });

    // 宏任务之间
    setTimeout(() => {
      console.log('本地-宏任务 1');
    }, 1000);
    const worker2 = new Worker('./index.js');
    setTimeout(() => {
      console.log('本地-宏任务 2');
    }, 1000);
  };
</script>
```

执行的时候打印结果：

本地-同步任务
本地-微任务 1
本地-微任务 2
index-同步任务
index-Promise
index-同步任务
index-Promise
本地-宏任务 1
本地-宏任务 2
index-setTimeout
index-setTimeout
可以看到：

先执行 script 中同步任务
再执行 script 中微任务
然后执行 UI 线程的渲染工作（这里在代码中没有体现，感兴趣的可以试试添加 rAF）
接着才执行 Web Worker 里面内容
再来是 index.html 中的宏任务
最后才是 Web Worker 文件中的宏任务
可以看出它仍符合 Event Loop 流程。

4.3.2 Web Worker 数据通讯

index.js

```js
onmessage = (res) => {
  // Worker 接收数据
  console.log('Worker 收到数据：', res);
  // Worker 收到数据：
  // MessageEvent {isTrusted: true, data: "查房，这里是 index.html！", origin: "", lastEventId: "", source: null, …}

  // Worker 发送数据
  postMessage('开门！这里是 index.js');
};
```

index.html

```html
<script>
  window.onload = function () {
    // 实例化 Worker
    const worker = new Worker('./index.js');

    // index.html 接收数据
    worker.addEventListener('message', (res) => {
      console.log('index.html 收到数据：', res);
      // index.html 收到数据：
      // MessageEvent {isTrusted: true, data: "开门！这里是 index.js", origin: "", lastEventId: "", source: null, …}
    });

    // index.html 发送数据
    worker.postMessage('查房，这里是 index.html！');

    //  终止 Worker
    worker.terminate();
  };
</script>
```

在 index.html 中，通过：

worker.addEventListener('message', callback)。接收 Web Worker 传递的数据。
worker.postMessage('xxx')。发送数据给 Web Worker。
worker.terminate()。终止通讯
在 index.js 中，通过：

```js
onmessage = (res) => {
  console.log(res); // 在 onmessage 方法接受数据
  postMessage('xxx'); // 通过 postMessage 发送数据
};
```

4.3.3 Web Worker 可操作 API

setTimeout()， clearTimeout()， setInterval()， clearInterval()：有了这几个函数，就可以在 Web Worker 线程中执行定时操作了；
XMLHttpRequest 对象：意味着我们可以在 Web Worker 线程中执行 Ajax 请求；
navigator 对象：可以获取到 ppName，appVersion，platform，userAgent 等信息；
location 对象（只读）：可以获取到有关当前 URL 的信息；
如果需要加载其他 JS 脚本：

```js
importScripts('./index2.js', './index3.js');

// 或者

// importScripts('./index2.js');
// importScripts('./index3.js');
```

4.3.4 Web Worker 兼容性

IE：11 版本
Edge：14+ 版本
Firefox：51+ 版本
Chrome：56+ 版本
其他：看 caniuse 链接
4.4 Node 和 浏览器

为啥会有 浏览器 Event Loop 和 Node.js Event Loop？

简单来说：

你的页面放到了浏览器去展示，你的数据放到了后台处理（将 Node.js 看成 PHP、Java 等后端语言），这两者能没有区别么？！
再仔细一点：

Node.js：Node.js 的 Event Loop 是基于 libuv。libuv 已经对 Node.js 的 Event Loop 作出了实现。
浏览器：浏览器的 Event Loop 是基于 HTML5 规范 的。而 HTML5 规范中只是定义了浏览器中的 Event Loop 的模型，具体实现留给了浏览器厂商。
libuv 是一个多平台支持库，主要用于异步 I/O。它最初是为 Node.js 开发的，现在 Luvit、Julia、pyuv 和其他的框架也使用它。Github - libuv 仓库

所以，咱们得将这两个 Event Loop 区分开来，它们是不一样的东东哈~

五 两个环境 Event Loop 对比

浏览器环境下，microtask 的任务队列是每个 macrotask 执行完之后执行。

而在 Node.js 中，microtask 会在事件循环的各个阶段之间执行，也就是一个阶段执行完毕，就会去执行 microtask 队列的任务。

这里没有讲 Node.js 的时间循环机制，第一个是因为 jsliang 对 Node 不熟，怕瞎写误导；第二个是因为面试官问的时候，基本上回答的都是浏览器的事件循环机制，偶尔提一嘴 Event Loop 分为浏览器事件循环和 Node 事件循环算是加点小分了。
