[Front-End-Interview-Notebook](https://github.com/CavsZhouyou/Front-End-Interview-Notebook/blob/master/JavaScript/JavaScript.md)

# 语言基础

介绍 js 的基本数据类型。
JavaScript 有几种类型的值？你能画一下他们的内存图吗？
介绍 js 有哪些内置对象？
内部属性 [[Class]] 是什么？
undefined 与 undeclared 的区别？
null 和 undefined 的区别？
如何获取安全的 undefined 值？

# 内存和作用域

什么是堆？什么是栈？它们之间有什么区别和联系？
Javascript 的作用域链？
eval 是做什么的？
什么是闭包，为什么要用它？
javascript 代码中的 "use strict"; 是什么意思 ? 使用它区别是什么？

## 语言进阶

在 js 中不同进制数字的表示方式
js 中整数的安全范围是多少？
typeof NaN 的结果是什么？
isNaN 和 Number.isNaN 函数的区别？
Array 构造函数只有一个参数值时的表现？
其他值到字符串的转换规则？
其他值到数字值的转换规则？
其他值到布尔类型的值的转换规则？
{} 和 [] 的 valueOf 和 toString 的结果是什么？
什么是假值对象？
~ 操作符的作用？
解析字符串中的数字和将字符串强制类型转换为数字的返回结果都是数字，它们之间的区别是什么？
操作符什么时候用于字符串的拼接？
什么情况下会发生布尔值的隐式强制类型转换？
|| 和 &amp;&amp; 操作符的返回值？
Symbol 值的强制类型转换？
== 操作符的强制类型转换规则？
如何将字符串转化为数字，例如 '12.3b'?
如何将浮点数点左边的数每三位添加一个逗号，如 12000000.11 转化为『12,000,000.11』?
常用正则表达式
生成随机数的各种方法？
如何实现数组的随机排序？
["1", "2", "3"].map(parseInt) 答案是多少？
如何封装一个 javascript 的类型判断函数？
如何判断一个对象是否为空对象？
使用闭包实现每隔一秒打印 1,2,3,4
Math.ceil 和 Math.floor
instanceof 的作用？
.call() 和 .apply() 的区别？
JavaScript 类数组对象的定义？
Object.is() 与原来的比较操作符 “===”、“==” 的区别？
escape,encodeURI,encodeURIComponent 有什么区别？
Unicode 和 UTF-8 之间的关系？
原码、反码和补码的介绍
toPrecision 和 toFixed 和 Math.round 的区别？

# 实践操作

说几条写 JavaScript 的基本规范？
模块化开发怎么做？
js 的几种模块规范？
AMD 和 CMD 规范的区别？
ES6 模块与 CommonJS 模块、AMD、CMD 的差异。
requireJS 的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何 缓存的？）
JS 模块加载器的轮子怎么造，也就是如何实现一个模块加载器？
js 中的命名规则
js 语句末尾分号是否可以省略？
如何查找一篇英文文章中出现频率最高的单词？
谈一谈你理解的函数式编程？
Js 动画与 CSS 动画区别及相应实现
mouseover 和 mouseenter 的区别？
js 拖拽功能的实现
js 中倒计时的纠偏实现？
js 中的深浅拷贝实现？
手写 call、apply 及 bind 函数
函数柯里化的实现
为什么 0.1 0.2 != 0.3？如何解决这个问题？
如何测试前端代码么？ 知道 BDD, TDD, Unit Test 么？ 知道怎么测试你的前端工程么(mocha, sinon, jasmin, qUnit..)？
介绍一下 js 的节流与防抖？
使用 JS 实现获取文件扩展名？
Javascript 中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？
js 延迟加载的方式有哪些？
同步和异步的区别？
对于 JSON 的了解？

# 面向对象

new 操作符具体干了什么呢？如何实现？
JavaScript 原型，原型链？ 有什么特点？
js 获取原型的方法？
javascript 创建对象的几种方式？
JavaScript 继承的几种实现方式？
寄生式组合继承的实现？
谈谈 This 对象的理解。
如何判断一个对象是否属于某个类？

# DOM 和 BOM

documen.write 和 innerHTML 的区别？
什么是 DOM 和 BOM？
innerHTML 与 outerHTML 的区别？
移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？
什么是 Polyfill ？

# 事件

写一个通用的事件侦听器函数。
事件是什么？IE 与火狐的事件机制有什么区别？ 如何阻止冒泡？
三种事件模型是什么？
事件委托是什么？
js 的事件循环是什么？

# 网络请求

开发中常用的几种 Content-Type ？
get 请求传参长度的误区
URL 和 URI 的区别？
get 和 post 请求在缓存方面的区别
手写一个 jsonp
Ajax 是什么? 如何创建一个 Ajax？

# 网络安全

什么是 XSS 攻击？如何防范 XSS 攻击？
什么是 CSP？
什么是 CSRF 攻击？如何防范 CSRF 攻击？
什么是 Samesite Cookie 属性？
什么是点击劫持？如何防范点击劫持？
SQL 注入攻击？

# ECMAScript 6

数组的 fill 方法？
ECMAScript6 怎么写 class，为什么会出现 class 这种东西?
什么是 Proxy ？
异步编程的实现方式？
什么是 Promise 对象，什么是 Promises/A 规范？
手写一个 Promise
let 和 const 的注意点？
什么是 rest 参数？
什么是尾调用，使用尾调用有什么好处？
Symbol 类型的注意点？
Set 和 WeakSet 结构？
Map 和 WeakMap 结构？
Object.assign()
require 模块引入的查找方式？
Reflect 对象创建目的？

# 性能优化

图片的懒加载和预加载
如何确定页面的可用性时间，什么是 Performance API？
一个列表，假设有 100000 个数据，这个该怎么办？
怎么做 JS 代码 Error 统计？
如何编写高性能的 Javascript ？
为什么使用 setTimeout 实现 setInterval？怎么模拟？
什么是 requestAnimationFrame ？

# 更多
## JavaScript 有哪些数据类型

6 种原始数据类型：

- `Boolean`: 布尔表示一个逻辑实体，可以有两个值：`true` 和 `false`
- `Number`: 用于表示数字类型
- `String`: 用于表示文本数据
- `Null`: `Null` 类型只有一个值： `null`,特指对象的值未设置
- `Undefined`: 一个没有被赋值的变量会有个默认值 `undefined`
- `Symbol`: 符号`(Symbols)`是`ECMAScript`第 6 版新定义的。符号类型是唯一的并且是不可修改的

引用类型：`Object`

## 怎么判断不同的 JS 数据类型

- `typeof`操作符：返回一个字符串，表示未经计算的操作数的类型

> `typeof` 操作符对于简单数据类型，返回其本身的数据类型，函数对象返回 `function` ，其他对象均返回 `Object`

> `null` 返回 `Object`

- `instanceof`: 用来判断 `A` 是否是 `B` 的实例，表达式为 `A instanceof B`，返回一个`Boolean`类型的值

> `instanceof` 检测的是**原型**,只能用来判断两个对象是否属于实例关系， 而不能判断一个对象实例具体属于哪种类型

```js
let a = [];
a instanceof Array; // true
a instanceof Object; // true
```

> 变量 `a` 的 `__proto__` 直接指向`Array.prototype`，间接指向 `Object.prototype`，所以按照 `instanceof` 的判断规则，`a` 就是`Object`的实例.针对数组的这个问题，`ES5` 提供了 `Array.isArray()` 方法 。该方法用以确认某个对象本身是否为 `Array` 类型

- `constructor`: 当一个函数被定义时，`JS` 引擎会为其添加`prototype`原型，然后再在 `prototype`上添加一个 `constructor` 属性，并让其指向该函数的引用

> `null`和`undefined`是无效的对象，因此是不会有`constructor`存在的，这两种类型的数据需要通过其他方式来判断

> 函数的`constructor`是不稳定的，这个主要体现在自定义对象上，当开发者重写`prototype`后，原有的`constructor`引用会丢失，`constructor`会默认为 `Object`

```js
function F() {}
var f = new F();
f.constructor == F; // true

F.prototype = { a: 1 };
var f = new F();
f.constructor == F; // false
```

> 在构造函数 `F.prototype` 没有被重写之前，构造函数 `F` 就是新创建的对象 `f` 的数据类型。当 `F.prototype` 被重写之后，原有的 `constructor` 引用丢失, 默认为 `Object`

> 因此，为了规范开发，在重写对象原型时一般都需要重新给 `constructor` 赋值，以保证对象实例的类型不被篡改

- `toString`: `Object` 的原型方法，调用该方法，默认返回当前对象的 `[[Class]]` 。这是一个内部属性，其格式为 `[object Xxx]` ，其中 `Xxx` 就是对象的类型

```js
Object.prototype.toString.call(''); // [object String]
Object.prototype.toString.call(11); // [object Number]
Object.prototype.toString.call(true); // [object Boolean]
Object.prototype.toString.call(Symbol()); //[object Symbol]
Object.prototype.toString.call(undefined); // [object Undefined]
Object.prototype.toString.call(null); // [object Null]
Object.prototype.toString.call(new Function()); // [object Function]
Object.prototype.toString.call([]); // [object Array]
```

## undefined 和 null 有什么区别

> `null`表示"没有对象"，即该处不应该有值

典型用法：

1. 作为函数的参数，表示该函数的参数不是对象
2. 作为对象原型链的终点

> `undefined`表示"缺少值"，就是此处应该有一个值，但是还没有定义

典型用法：

1. 变量被声明了，但没有赋值时，就等于`undefined`
2. 调用函数时，应该提供的参数没有提供，该参数等于`undefined`
3. 对象没有赋值的属性，该属性的值为`undefined`
4. 函数没有返回值时，默认返回`undefined`

详见： [undefined 和 null 的区别-阮一峰](http://www.ruanyifeng.com/blog/2014/03/undefined-vs-null.html)

## 数组对象有哪些常用方法

> 修改器方法：

- `pop()`: 删除数组的最后一个元素，并返回这个元素
- `push()`：在数组的末尾增加一个或多个元素，并返回数组的新长度
- `reverse()`: 颠倒数组中元素的排列顺序
- `shift()`: 删除数组的第一个元素，并返回这个元素
- `unshift()`: 在数组的开头增加一个或多个元素，并返回数组的新长度
- `sort()`: 对数组元素进行排序，并返回当前数组
- `splice()`: 在任意的位置给数组添加或删除任意个元素

> 访问方法：

- `concat()`: 返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组
- `join()`: 连接所有数组元素组成一个字符串
- `slice()`: 抽取当前数组中的一段元素组合成一个新数组
- `indeOf()`: 返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 `-1`
- `lastIndexOf()`: 返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 `-1`

> 迭代方法：

- `forEach()`: 为数组中的每个元素执行一次回调函数,最终返回 `undefined`
- `every()`: 如果数组中的每个元素都满足测试函数，则返回 `true`，否则返回 `false`
- `some()`: 如果数组中至少有一个元素满足测试函数，则返回 `true`，否则返回 `false`
- `filter()`: 将所有在过滤函数中返回 `true` 的数组元素放进一个新数组中并返回
- `map()`: 返回一个由回调函数的返回值组成的新数组

## Js 有哪几种创建对象的方式

> 对象字面量

```js
var obj = {};
```

> Object 构造函数

```js
var obj = new Object();
```

> 工厂模式

```js
function Person(name, age) {
  var o = new Object();
  o.name = name;
  o.age = age;
  o.say = function () {
    console.log(name);
  };
  return o;
}
```

缺点： 每次通过`Person`创建对象的时候，所有的`say`方法都是一样的，但是却存储了多次，浪费资源

> 构造函数模式

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.say = function () {
    console.log(name);
  };
}
var person = new Person('hello', 18);
```

构造函数模式隐试的在最后返回`return this` 所以在缺少`new`的情况下，会将属性和方法添加给全局对象，浏览器端就会添加给`window`对象,可以根据`return this` 的特性调用`call`或者`apply`指定`this`

> 原型模式

```js
function Person() {}
Person.prototype.name = 'hanmeimei';
Person.prototype.say = function () {
  alert(this.name);
};
Person.prototype.friends = ['lilei'];
var person = new Person();
```

实现了方法与属性的共享，可以动态添加对象的属性和方法。但是没有办法创建实例自己的属性和方法，也没有办法传递参数

> 构造函数和原型组合

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.say = function () {
  console.log(this.name);
};
var person = new Person('hello');
```

还有好几种模式，感兴趣的小伙伴可以参考 **红宝书**，你们肯定知道的了！

## 怎么实现对对象的拷贝(浅拷贝与深拷贝)

> 浅拷贝

- 拷贝原对象引用
- 可以使用`Array.prototype.slice()`也可以完成对一个数组或者对象的浅拷贝
- `Object.assign()`方法

> 深拷贝

- 最常用的方式就是 `JSON.parse(JSON.stringify(目标对象)`，缺点就是只能拷贝符合`JSON`数据标准类型的对象

## 什么是闭包，为什么要用它

> 简单来说，闭包就是能够读取其他函数内部变量的函数

```js
function Person() {
  var name = 'hello';
  function say() {
    console.log(name);
  }
  return say();
}
Person(); // hello
```

> 由于 `JavaScript` 特殊的作用域，函数外部无法直接读取内部的变量，内部可以直接读取外部的变量，从而就产生了闭包的概念

用途：

> 最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中

注意点：

> 由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在 IE 中可能导致内存泄露

## 介绍一下 JavaScript 原型，原型链，它们有何特点

首先明确一点，**`JavaScript` 是基于原型的**

> 每个构造函数`(constructor)`都有一个原型对象`(prototype)`,原型对象都包含一个指向构造函数的指针,而实例`(instance)`都包含一个指向原型对象的内部指针.

![image](https://raw.githubusercontent.com/ltadpoles/web-document/master/JavaScript/images/%E5%8E%9F%E5%9E%8B%E5%9B%BE%E7%A4%BA.jpg)

图解：

- 每一个构造函数都拥有一个`prototype`属性，这个属性指向一个对象，也就是原型对象
- 原型对象默认拥有一个`constructor`属性，指向指向它的那个构造函数
- 每个对象都拥有一个隐藏的属性`[[prototype]]`，指向它的原型对象

那么什么是原型链：

> `JavaScript`中所有的对象都是由它的原型对象继承而来。而原型对象自身也是一个对象，它也有自己的原型对象，这样层层上溯，就形成了一个类似链表的结构，这就是原型链

> 所有原型链的终点都是`Object`函数的`prototype`属性。`Objec.prototype`指向的原型对象同样拥有原型，不过它的原型是`null`，而`null`则没有原型

![image](https://raw.githubusercontent.com/ltadpoles/web-document/master/JavaScript/images/%E5%8E%9F%E5%9E%8B%E9%93%BE.png)

## JavaScript 如何实现继承

- 原型链继承

```js
function Animal() {}
Animal.prototype.name = 'cat';
Animal.prototype.age = 1;
Animal.prototype.say = function () {
  console.log('hello');
};

var cat = new Animal();

cat.name; // cat
cat.age; // 1
cat.say(); // hello
```

> 最简单的继承实现方式，但是也有其缺点

1. 来自原型对象的所有属性被所有实例共享
2. 创建子类实例时，无法向父类构造函数传参
3. 要想为子类新增属性和方法，必须要在`new`语句之后执行，不能放到构造器中

- 构造继承

```js
function Animal() {
  this.species = '动物';
}
function Cat(name, age) {
  Animal.call(this);
  this.name = name;
  this.age = age;
}

var cat = new Cat('豆豆', 2);

cat.name; // 豆豆
cat.age; // 2
cat.species; // 动物
```

> 使用 `call` 或 `apply` 方法，将父对象的构造函数绑定在子对象上.

- 组合继承

```js
function Animal() {
  this.species = '动物';
}

function Cat(name) {
  Animal.call(this);
  this.name = name;
}

Cat.prototype = new Animal(); // 重写原型
Cat.prototype.constructor = Cat;
```

> 如果没有`Cat.prototype = new Animal()`这一行，`Cat.prototype.constructor`是指向`Cat`的；加了这一行以后，`Cat.prototype.constructor`指向`Animal`.这显然会导致继承链的紊乱(`cat1` 明明是用构造函数`Cat`生成的），因此我们必须手动纠正，将`Cat.prototype`对象的`constructor`值改为`Cat`

- `extends` 继承
  `ES6` 新增继承方式，`Class` 可以通过 `extends` 关键字实现继承

```js
class Animal {}

class Cat extends Animal {
  constructor() {
    super();
  }
}
```

> 使用 `extends` 实现继承，必须添加 `super` 关键字定义子类的 `constructor`，这里的`super()` 就相当于 `Animal.prototype.constructor.call(this)`

当然，还有很多种实现继承的方式，这里就不多说了。然后，再推荐一波 **红宝书**

## new 操作符具体干了什么

- 创建一个空对象，并且 `this` 变量引用该对象，同时还继承了该函数的原型
- 属性和方法被加入到 `this` 引用的对象中
- 新创建的对象由 `this` 所引用，并且最后隐式的返回 `this`

## 同步和异步的区别，怎么异步加载 JavaScript

> 同步模式

同步模式，又称阻塞模式。`javascript` 在默认情况下是会阻塞加载的。当前面的 `javascript` 请求没有处理和执行完时，会阻止浏览器的后续处理

> 异步模式

异步加载又叫非阻塞，浏览器在下载执行 `js` 同时，还会继续进行后续页面的处理

> 异步加载 `JavaScript`

- 动态添加 `script` 标签
- `defer`
- `async`

> `defer`属性和`async`都是属于 `script` 标签上面的属性，两者都能实现 `JavaScript` 的异步加载。不同之处在于：`async` 在异步加载完成的时候就马上开始执行了，`defer` 会等到 `html` 加载完毕之后再执行

## 跨域问题的产生，怎么解决它

> 由于浏览器的 [同源策略](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)，在出现 域名、端口、协议有一种不一致时，就会出现跨域，属于浏览器的一种安全限制。

解决跨域问题有很多种方式，常用的就是以下几种：

- `jsonp` 跨域：动态创建`script`，再请求一个带参网址实现跨域通信.缺点就是只能实现 `get` 一种请求
- `document.domain + iframe`跨域：两个页面都通过 js 强制设置`document.domain`为基础主域，就实现了同域.但是仅限主域相同，子域不同的跨域应用场景
- 跨域资源共享`CORS`：只服务端设置`Access-Control-Allow-Origin`即可，前端无须设置，若要带`cookie`请求：前后端都需要设置
- `nginx`反向代理接口跨域：同源策略是浏览器的安全策略，不是`HTTP`协议的一部分。服务器端调用`HTTP`接口只是使用`HTTP`协议，不会执行`JS`脚本，不需要同源策略，也就不存在跨越问题
- `WebSocket`协议跨域

## 对 this 的理解

在 `JavaScript` 中，研究 `this` 一般都是 `this` 的指向问题，核心就是 **`this` 永远指向最终调用它的那个对象**，除非改变 `this` 指向或者箭头函数那种特殊情况

```js
function test() {
  console.log(this);
}

test(); // window

var obj = {
  foo: function () {
    console.log(this.bar);
  },
  bar: 1,
};

var foo = obj.foo;
var bar = 2;

obj.foo(); // 1
foo(); // 2

// 函数调用的环境不同，所得到的结果也是不一样的
```

## apply()、call()和 bind() 是做什么的，它们有什么区别

相同点：三者都可以**改变 `this` 的指向**

不同点：

- `apply` 方法传入两个参数：一个是作为函数上下文的对象，另外一个是作为函数参数所组成的数组

```js
var obj = {
  name: 'sss',
};

function func(firstName, lastName) {
  console.log(firstName + ' ' + this.name + ' ' + lastName);
}

func.apply(obj, ['A', 'B']); // A sss B
```

- `call` 方法第一个参数也是作为函数上下文的对象，但是后面传入的是一个参数列表，而不是单个数组

```js
var obj = {
  name: 'sss',
};

function func(firstName, lastName) {
  console.log(firstName + ' ' + this.name + ' ' + lastName);
}

func.call(obj, 'C', 'D'); // C sss D
```

- `bind` 接受的参数有两部分，第一个参数是是作为函数上下文的对象，第二部分参数是个列表，可以接受多个参数

```js
var obj = {
  name: 'sss',
};

function func() {
  console.log(this.name);
}

var func1 = func.bind(null, 'xixi');
func1();
```

> `apply`、`call` 方法都会使函数立即执行，因此它们也可以用来调用函数

> `bind` 方法不会立即执行，而是返回一个改变了上下文 `this` 后的函数。而原函数 `func` 中的 `this` 并没有被改变，依旧指向全局对象 `window`

> `bind` 在传递参数的时候会将自己带过去的参数排在原函数参数之前

```js
function func(a, b, c) {
  console.log(a, b, c);
}
var func1 = func.bind(this, 'xixi');
func1(1, 2); // xixi 1 2
```

## 什么是内存泄漏，哪些操作会造成内存泄漏

> 内存泄漏：是指一块被分配的内存既不能使用，又不能回收，直到浏览器进程结束

可能造成内存泄漏的操作：

- 意外的全局变量
- 闭包
- 循环引用
- 被遗忘的定时器或者回调函数

你可能还需要知道 [垃圾回收机制](http://www.ruanyifeng.com/blog/2017/04/memory-leak.html) 此外，高程上面对垃圾回收机制的介绍也很全面，有兴趣的小伙伴可以看看

## 什么是事件代理，它的原理是什么

> 事件代理：通俗来说就是将元素的事件委托给它的父级或者更外级元素处理

> 原理：利用事件冒泡机制实现的

> 优点：只需要将同类元素的事件委托给父级或者更外级的元素，不需要给所有元素都绑定事件，减少内存空间占用，提升性能; 动态新增的元素无需重新绑定事件

## 对 AMD 和 CMD 的理解，它们有什么区别

> `AMD`和`CMD`都是为了解决浏览器端模块化问题而产生的，`AMD`规范对应的库函数有 `Require.js`，`CMD`规范是在国内发展起来的，对应的库函数有`Sea.js`

**`AMD`和`CMD`最大的区别是对依赖模块的执行时机处理不同**

> 1、`AMD`推崇依赖前置，在定义模块的时候就要声明其依赖的模块

> 2、`CMD`推崇就近依赖，只有在用到某个模块的时候再去`require`

参考：[AMD-中文版](https://github.com/amdjs/amdjs-api/wiki/AMD-%28%E4%B8%AD%E6%96%87%E7%89%88%29) [CMD-规范](https://github.com/seajs/seajs/issues/242)

## 对 ES6 的了解

> `ECMAScript 6.0` 是 `JavaScript` 语言的下一代标准

新增的特性：

- 声明变量的方式 `let` `const`
- 变量解构赋值
- 字符串新增方法 `includes()` `startsWith()` `endsWith()` 等
- 数组新增方法 `Array.from()` `Array.of()` `entries()` `keys()` `values()` 等
- 对象简洁写法以及新增方法 `Object.is()` `Object.assign()` `entries()` `keys()` `values()`等
- 箭头函数、`rest` 参数、函数参数默认值等
- 新的数据结构： `Set` 和 `Map`
- `Proxy`
- `Promise`对象
- `async`函数 `await`命令
- `Class`类
- `Module` 体系 模块的加载和输出方式

## 箭头函数有什么特点

> `ES6` 允许使用箭头`=>` 定义函数

```js
var f = (v) => v;

// 等同于
var f = function (v) {
  return v;
};
```

注意点：

- 函数体内的 `this` 对象，就是定义时所在的对象，而不是使用时所在的对象
- 不可以当作构造函数，也就是说，不可以使用 `new` 命令，否则会抛出一个错误
- 不可以使用 `arguments` 对象，该对象在函数体内不存在。如果要用，可以用 `rest` 参数代替

## Promise 对象的了解

> `Promise` 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大.所谓 `Promise` ，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果 -- `ES6` 入门-阮一峰

> `Promise` 对象代表一个异步操作，有三种状态：`pending`（进行中）、`fulfilled`（已成功）和 `rejected`（已失败）。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态

特点：

- 对象的状态不受外界影响
- 一旦状态改变，就不会再变，任何时候都可以得到这个结果
- `Promise` 新建后就会立即执行

```js
const promise = new Promise(function(resolve, reject) {
  // ... some code

  if (/* 异步操作成功 */){
    resolve(value);
  } else {
    reject(error);
  }
})
```

> `Promise` 实例生成以后，可以用 `then` 方法分别指定 `resolved `状态和 `rejected` 状态的回调函数

```js
promise.then(
  function (value) {
    // success
  },
  function (error) {
    // failure
  }
);
```

> `then` 方法返回的是一个新的 Promise 实例

> `Promise.prototype.catch` 用于指定发生错误时的回调函数,具有`冒泡`性质，会一直向后传递，直到被捕获为止。也就是说，错误总是会被下一个`catch`语句捕获

```js
getJSON('/post/1.json')
  .then(function (post) {
    return getJSON(post.commentURL);
  })
  .then(function (comments) {
    // some code
  })
  .catch(function (error) {
    // 处理前面三个Promise产生的错误
  });
```

> `catch` 方法返回的还是一个 `Promise` 对象，因此后面还可以接着调用 `then` 方法

出去上述方法，`Promise` 还有其他用法，小伙伴们可以在这里查看大佬写的文章 [ES6 入门-阮一峰](http://es6.ruanyifeng.com/#README)

## async 函数以及 awit 命令

> `async` 函数是什么？一句话，它就是 `Generator` 函数的语法糖

了解 `Generator` 函数的小伙伴，这里 [传送门](http://es6.ruanyifeng.com/#docs/generator)

`async` 特点：

> `async` 函数返回一个 `Promise` 对象，可以使用 `then ` 方法添加回调函数。当函数执行的时候，一旦遇到 `await` 就会先返回，等到异步操作完成，再接着执行函数体内后面的语句

> `async` 函数内部 `return` 语句返回的值，会成为 `then` 方法回调函数的参数

> `async` 函数返回的 `Promise` 对象，必须等到内部所有 `await` 命令后面的 `Promise` 对象执行完，才会发生状态改变，除非遇到 `return` 语句或者抛出错误

> `async` 函数内部抛出错误，会导致返回的 `Promise` 对象变为 `reject` 状态。抛出的错误对象会被 `catch` 方法回调函数接收到

```js
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint('hello world', 50);
```

> `await` 命令: `await` 命令后面是一个 `Promise` 对象，返回该对象的结果。如果不是 `Promise` 对象，就直接返回对应的值

```js
async function f() {
  // 等同于
  // return 123;
  return await 123;
}

f().then((v) => console.log(v));
// 123
```

> `await` 命令后面是一个`thenable`对象（即定义 then 方法的对象），那么`await`会将其等同于 `Promise` 对象.也就是说就算一个对象不是`Promise`对象，但是只要它有`then`这个方法， `await` 也会将它等同于`Promise`对象

使用注意点：

- `await` 命令后面的 `Promise` 对象，运行结果可能是 `rejected`，所以最好把 `await` 命令放在 `try...catch` 代码块中
- 多个 `await` 命令后面的异步操作，如果不存在继发关系，最好让它们同时触发
- `await` 命令只能用在 `async` 函数之中，如果用在普通函数，就会报错

了解更多，请点击 [这里](http://es6.ruanyifeng.com/#docs/async)

## export 与 export default 有什么区别

> `export` 与 `export default` 均可用于导出常量、函数、文件、模块等

> 在一个文件或模块中，`export`、`import` 可以有多个，`export default` 仅有一个

> 通过 `export` 方式导出，在导入时要加 `{ }`，`export default` 则不需要

> 使用 `export default`命令，为模块指定默认输出，这样就不需要知道所要加载模块的变量名; `export` 加载的时候需要知道加载模块的变量名

> `export default` 命令的本质是将后面的值，赋给 `default` 变量，所以可以直接将一个值写在 `export default` 之后

## 前端性能优化

| 内容 | 类型 |
|---|---|
| 1. 尽可能的减少 HTTP 的请求数 | content |
| 2. 使用 CDN（Content Delivery Network） | server |
| 3. 添加 Expires 头(或者 Cache-control ) | server |
| 4. Gzip 组件 | server |
| 5. 将 CSS 样式放在页面的上方 | css |
| 6. 将脚本移动到底部（包括内联的） | javascript |
| 7. 避免使用 CSS 中的 Expressions | css |
| 8. 将 JavaScript 和 CSS 独立成外部文件 | javascript css |
| 9. 减少 DNS 查询 | content |
| 10. 压缩 JavaScript 和 CSS (包括内联的) | javascript css |
| 11. 避免重定向 | server |
| 12. 移除重复的脚本 | javascript |
| 13. 配置实体标签（ETags） | css |
| 14. 使 AJAX 缓存 |

参见 [雅虎 14 条前端性能优化](https://blog.csdn.net/qfkfw/article/details/7272961)

## 对 JS 引擎执行机制的理解

首选明确两点：

> `JavaScript` 是单线程语言

> `JavaScript` 的 `Event Loop` 是 `JS` 的执行机制, 也就是事件循环

```js
console.log(1);

setTimeout(function () {
  console.log(2);
}, 0);

console.log(3);

// 1 3 2
```

> `JavaScript` 将任务分为同步任务和异步任务，执行机制就是先执行同步任务，将同步任务加入到主线程，遇到异步任务就先加入到 `event table` ，当所有的同步任务执行完毕，如果有可执行的异步任务，再将其加入到主线程中执行

视频详解，移步 [这里](https://vimeo.com/96425312)

```js
setTimeout(function () {
  console.log(1);
}, 0);
new Promise(function (resolve) {
  console.log(2);
  for (var i = 0; i < 10000; i++) {
    i == 99 && resolve();
  }
}).then(function () {
  console.log(3);
});

console.log(4);

// 2 4 3 1
```

在异步任务中，定时器也属于特殊的存在。有人将其称之为 宏任务、微任务，定时器就属于宏任务的范畴。

参考 [JS 引擎的执行机制](https://segmentfault.com/a/1190000012806637)
