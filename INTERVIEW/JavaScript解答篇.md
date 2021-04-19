[Front-End-Interview-Notebook](https://github.com/CavsZhouyou/Front-End-Interview-Notebook/blob/master/JavaScript/JavaScript.md)

# 数据类型和语法

如何获取安全的 undefined 值？

## JS 数据类型

JavaScript 有哪些数据类型

原始数据类型是直接存储在栈 stack 中的简单数据段，占据空间小、大小固定，属于被频繁使用数据。原始数据类型有 7 种：

- `Boolean`: 布尔表示一个逻辑实体，可以有两个值：`true` 和 `false`
- `Number`: 用于表示数字类型
- `String`: 用于表示文本数据
- `Null`: 该类型只有一个值 `null`，特指对象的值未设置
- `Undefined`: 一个没有被赋值的变量会有个默认值 `undefined`
- `Symbol`: 代表创建后独一无二且不可变的数据类型
- `BigInt`：一种数字类型的数据，它可以表示任意精度格式的整数，使用 BigInt 可以安全地存储和操作大整数

引用数据类型是存储在堆 heap 中的对象，占据空间大、大小不固定。如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释器寻找引用值时，会首先检索其在栈中的地址，取得地址后从堆中获得实体。

引用类型只有 1 种：`Object`

## 类型判断

怎么判断不同的 JS 数据类型

1. `typeof`操作符：返回一个字符串，表示未经计算的操作数的类型
  - 简单数据类型直接返回本身的数据类型由 `Boolean`、`Number`、`String`、`Undefined`、`Symbol`
  - 函数对象返回 `function`，其他对象均返回 `Object`
  - `null` 返回 `Object`
2. `instanceof`: 根据原型链来判断两个对象是否属于实例关系，而不能判断实例具体属于哪种类型
3. `Array.isArray()` 可以确认某个对象本身是否为数组类型
4. `toString`: `Object` 的原型方法，调用该方法，默认返回当前对象的 `[[Class]]` 。这是一个内部属性，其格式为 `[object Xxx]` ，其中 `Xxx` 就是对象的类型

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

## undefined/undeclared

undefined 与 undeclared 的区别？

已在作用域中声明但还没有赋值的变量，是 undefined 的。相反，还没有在作用域中声明过的变量，是 undeclared 的。

对于 undeclared 变量的引用，浏览器会报引用错误，如 `ReferenceError: b is not defined` 。但是我们可以使用 typeof 的安全防范机制来避免报错，因为对于 undeclared（或者 not defined ）变量，typeof 会返回 "undefined"。

## undefined/null

undefined 和 null 有什么区别

首先 Undefined 和 Null 都是基本数据类型，这两个基本数据类型分别都只有一个值，就是 undefined 和 null。

`null`表示"没有对象"，即该处不应该有值。典型用法：

1. 作为函数的参数，表示该函数的参数不是对象
2. 作为对象原型链的终点

`undefined`表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法：

1. 变量被声明了，但没有赋值时，就等于`undefined`
2. 调用函数时，应该提供的参数没有提供，该参数等于`undefined`
3. 对象没有赋值的属性，该属性的值为`undefined`
4. 函数没有返回值时，默认返回`undefined`

当我们对两种类型使用 typeof 进行判断的时候，Null 类型化会返回 “object”，这是一个历史遗留的问题。当我们使用双等号对两种类型的值进行比较时会返回 true，使用三个等号时会返回 false。

#### 安全的 undefined 值

如何获取安全的 undefined 值？

因为 undefined 是一个标识符，所以可以被当作变量来使用和赋值，但是这样会影响 undefined 的正常判断。

表达式 `void ___` 没有返回值，因此返回结果是 undefined。void 并不改变表达式的结果，只是让表达式不返回值。

按惯例我们用 `void 0` 来获得 undefined。

# 内存和作用域

什么是堆？什么是栈？它们之间有什么区别和联系？
Javascript 的作用域链？
eval 是做什么的？
什么是闭包，为什么要用它？
javascript 代码中的 "use strict"; 是什么意思 ? 使用它区别是什么？


## 内存泄露

什么是内存泄漏，哪些操作会造成内存泄漏

内存泄漏：是指一块被分配的内存既不能使用，又不能回收，直到浏览器进程结束。可能造成内存泄漏的操作：

- 意外的全局变量
- 闭包
- 循环引用
- 被遗忘的定时器或者回调函数

## 垃圾回收

JS 内存空间中，栈用来存放变量，堆存放复杂对象，池存放常量。垃圾回收策略分为两种：

- 手动回收：C/C++ 语言可以通过 `free()` 这些代码来决定何时分配内存、何时销毁内存
- 自动回收：JavaScript、Python、Java 等产生的垃圾数据是由垃圾回收器来释放的

V8 中会把堆分为 新生代 和 老生代 两个区域，新生代中存放的是生存时间短的对象，老生代中存放的生存时间久的对象。新生区的容量没有老生区那么大，所以 V8 分别使用 2 个不同的垃圾回收器，来高效实施垃圾回收：

- 副垃圾回收器。主要负责新生代的垃圾回收。
- 主垃圾回收器。主要负责老生代的垃圾回收。

### 垃圾回收方法

1. 标记清除 mark and sweep

这是 JavaScript 最常见的垃圾回收方式，当变量进入执行环境的时候，比如函数中声明一个变量，垃圾回收器将其标记为“进入环境”，当变量离开环境的时候（函数执行结束）将其标记为“离开环境”。

垃圾回收器会在运行的时候给存储在内存中的所有变量加上标记，然后去掉环境中的变量以及被环境中变量所引用的变量（闭包），在这些完成之后仍存在标记的就是要删除的变量了。

2. 引用计数 reference counting 

在低版本 IE 中经常会出现内存泄露，很多时候就是因为其采用引用计数方式进行垃圾回收。引用计数的策略是跟踪记录每个值被使用的次数，当声明了一个变量并将一个引用类型赋值给该变量的时候这个值的引用次数就加 1，如果该变量的值变成了另外一个，则这个值得引用次数减 1，当这个值的引用次数变为 0 的时候，说明没有变量在使用，这个值没法被访问了，因此可以将其占用的空间回收，这样垃圾回收器会在运行的时候清理掉引用次数为 0 的值占用的空间。

在 IE 中虽然 JavaScript 对象通过标记清除的方式进行垃圾回收，但 BOM 与 DOM 对象却是通过引用计数回收垃圾的，也就是说只要涉及 BOM 及 DOM 就会出现循环引用问题。

### 减少 JS 中垃圾回收

- 对象优化
- 数组优化
- 方法优化

# 语言进阶

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

## 数组常用方法

数组对象有哪些常用方法

1. 修改器方法：

- `pop()`: 删除数组的最后一个元素，并返回这个元素
- `push()`：在数组的末尾增加一个或多个元素，并返回数组的新长度
- `reverse()`: 颠倒数组中元素的排列顺序
- `shift()`: 删除数组的第一个元素，并返回这个元素
- `unshift()`: 在数组的开头增加一个或多个元素，并返回数组的新长度
- `sort()`: 对数组元素进行排序，并返回当前数组
- `splice()`: 在任意的位置给数组添加或删除任意个元素

2. 访问方法：

- `concat()`: 返回一个由当前数组和其它若干个数组或者若干个非数组值组合而成的新数组
- `join()`: 连接所有数组元素组成一个字符串
- `slice()`: 抽取当前数组中的一段元素组合成一个新数组
- `indeOf()`: 返回数组中第一个与指定值相等的元素的索引，如果找不到这样的元素，则返回 `-1`
- `lastIndexOf()`: 返回数组中最后一个（从右边数第一个）与指定值相等的元素的索引，如果找不到这样的元素，则返回 `-1`

3. 迭代方法：

- `forEach()`: 为数组中的每个元素执行一次回调函数,最终返回 `undefined`
- `every()`: 如果数组中的每个元素都满足测试函数，则返回 `true`，否则返回 `false`
- `some()`: 如果数组中至少有一个元素满足测试函数，则返回 `true`，否则返回 `false`
- `filter()`: 将所有在过滤函数中返回 `true` 的数组元素放进一个新数组中并返回
- `map()`: 返回一个由回调函数的返回值组成的新数组

## 遍历语法

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

# 最佳实践

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

## AMD/CMD

对 AMD 和 CMD 的理解，它们有什么区别

`AMD`和`CMD`都是为了解决浏览器端模块化问题而产生的，`AMD`规范对应的库函数有 `Require.js`，`CMD`规范是在国内发展起来的，对应的库函数有`Sea.js`

`AMD`和`CMD`最大的区别是对依赖模块的执行时机处理不同

1. `AMD`推崇依赖前置，在定义模块的时候就要声明其依赖的模块
2. `CMD`推崇就近依赖，只有在用到某个模块的时候再去`require`

## TypeScript 语法

简单笼统地说，TypeScript 是 JavaScript 的超集，是微软开发的一种脚本语言。和 JavaScript 一样，是现在项目开发中热门的脚本语言。

TypeScript 是一种强类型语言，可编译成 JavaScript，包含了 JavaScript 的所有元素，可以载入 JavaScript 代码运行，扩展了 JavaScript 的语法。相比 JavaScript，TypeScript 是真面向对象，增加了静态类型，类，模块，接口和类型注解。

TypeScript 的编译器很智能，会进行冲突检测，举个例子，一个 enum 的数据，你初始化一个数据，再用一个 switch 语句，编译器会判定其他选项为无效的，会编译错误，直接指出错误原因，这在 JavaScript 是不会指出错误的。

# 面向对象

JavaScript 原型，原型链？ 有什么特点？
js 获取原型的方法？
javascript 创建对象的几种方式？
JavaScript 继承的几种实现方式？
寄生式组合继承的实现？
谈谈 This 对象的理解。
如何判断一个对象是否属于某个类？

## 实现继承

JavaScript 如何实现继承

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

## 原型和原型链

介绍一下 JavaScript 原型和原型链，它们有何特点

`JavaScript` 是基于原型的。每个构造函数 constructor 都有一个原型对象 prototype ，原型对象都包含一个指向构造函数的指针，而实例 instance 都包含一个指向原型对象的内部指针.

- 每一个构造函数都拥有一个`prototype`属性，这个属性指向一个对象，也就是原型对象
- 原型对象默认拥有一个`constructor`属性，指向指向它的那个构造函数
- 每个对象都拥有一个隐藏的属性`[[prototype]]`，指向它的原型对象

那么什么是原型链：

`JavaScript`中所有的对象都是由它的原型对象继承而来。

- 原型对象自身也是一个对象，它也有自己的原型对象，这样层层上溯，就形成了一个类似链表的结构，这就是原型链
- 所有原型链的终点都是`Object`函数的`prototype`属性。`Objec.prototype`指向的原型对象同样拥有原型，不过它的原型是`null`，而`null`则没有原型

## 创建对象方法

JS 有哪几种创建对象的方式

1. 对象字面量
2. Object 构造函数
3. 工厂模式。每次通过创建对象的时候，所有的方法都是一样的，但是却存储了多次，浪费资源
4. 构造函数模式
5. 原型模式。实现了方法与属性的共享，可以动态添加对象的属性和方法。但是没有办法创建实例自己的属性和方法，也没有办法传递参数

```js
function Person() {}
Person.prototype.name = 'hanmeimei';
Person.prototype.say = function () {
  alert(this.name);
};
Person.prototype.friends = ['lilei'];
var person = new Person();
```

6. 构造函数和原型组合

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

# DOM 和 BOM

documen.write 和 innerHTML 的区别？
什么是 DOM 和 BOM？
innerHTML 与 outerHTML 的区别？
移动端的点击事件的有延迟，时间是多久，为什么会有？ 怎么解决这个延时？
什么是 Polyfill ？

## DOM 常用方法

DOM 增删改查操作有哪些？

- getElementById 返回带有指定 ID 的元素
- getElementsByTagName 返回包含带有指定标签名称的所有元素的节点列表
- getElementsByClassName 返回包含带有指定类名的所有元素的节点列表

- appendChild 把新的子节点添加到指定节点
- removeChild 删除子节点
- replaceChild 替换子节点
- insertBefore 在指定子节点前面插入新的子节点

- createAttribute 创建属性节点。
- createElement 创建元素节点。
- createTextNode 创建文本节点。
- getAttribute 返回指定的属性值。
- setAttribute 把指定属性设置或修改为指定的值。

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

# 事件和事件循环

写一个通用的事件侦听器函数。
事件是什么？IE 与火狐的事件机制有什么区别？ 如何阻止冒泡？
三种事件模型是什么？
事件委托是什么？
js 的事件循环是什么？

## 事件代理

什么是事件代理，它的原理是什么

> 事件代理：通俗来说就是将元素的事件委托给它的父级或者更外级元素处理

> 原理：利用事件冒泡机制实现的

> 优点：只需要将同类元素的事件委托给父级或者更外级的元素，不需要给所有元素都绑定事件，减少内存空间占用，提升性能; 动态新增的元素无需重新绑定事件

# 运行机制

## src 与 href

href 表示超文本引用（hypertext reference），在 `<link>` 和 `<a>` 等元素上使用。src 表示来源地址，是指外部资源的位置，指向的内容将会嵌入到文档中当前标签 所在的位置，在 img、script、iframe 等元素上。

## JS 运行机制

对 JS 引擎执行机制的理解

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


## 异步加载

同步和异步的区别，怎么异步加载 JavaScript

> 同步模式

同步模式，又称阻塞模式。`javascript` 在默认情况下是会阻塞加载的。当前面的 `javascript` 请求没有处理和执行完时，会阻止浏览器的后续处理

> 异步模式

异步加载又叫非阻塞，浏览器在下载执行 `js` 同时，还会继续进行后续页面的处理

> 异步加载 `JavaScript`

- 动态添加 `script` 标签
- `defer`
- `async`

> `defer`属性和`async`都是属于 `script` 标签上面的属性，两者都能实现 `JavaScript` 的异步加载。不同之处在于：`async` 在异步加载完成的时候就马上开始执行了，`defer` 会等到 `html` 加载完毕之后再执行


# 网络与安全

## Web 客户端

主流浏览器的内核。

- IE 浏览器是 Trident
- Mozilla 浏览器是 Gecko
- Safari 浏览器是 Webkit
- Chrome 浏览器是 Blink
- Opera 浏览器现在也是 Blink。

同源策略是对 XHR 的一个主要约束，它为通信设置了“相同的域、相同的端口、相同的协议”这一限制。试图访问上述限制之外的资源，都会引发安全错误，除非采用被认可的跨域解决方案。这个解决方案叫做 CORS（ Cross-Origin Resource Sharing，跨源资源共享）， IE8 通过 XDomainRequest 对象支持 CORS，其他浏览器通过 XHR 对象原生支持 CORS。图像 Ping 和 JSONP 是另外两种跨域通信的技术，但不如 CORS 稳妥。

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

## 异步 ajax 优缺点

优点：不会造成 UI 卡死，用户体验好；局部刷新页面，省流量。

缺点：后退按钮无效，多个请求回调时间不确定，对搜索引擎不友好、数据安全。

# ES6 特性

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

## export/export default

export 与 export default 有什么区别

`export` 与 `export default` 均可用于导出常量、函数、文件、模块等

1. 在一个文件或模块中，`export`、`import` 可以有多个，`export default` 仅有一个
2. 通过 `export` 方式导出，在导入时要加 `{}`，`export default` 则不需要
3. 使用 `export default`命令，为模块指定默认输出，这样就不需要知道所要加载模块的变量名; `export` 加载的时候需要知道加载模块的变量名

`export default` 命令的本质是将后面的值，赋给 `default` 变量，所以可以直接将一个值写在 `export default` 之后

## async/awit

async 函数以及 awit 命令

`async` 函数是什么？一句话，它就是 `Generator` 函数的语法糖。`async` 特点：

1. `async` 函数返回一个 `Promise` 对象，可以使用 `then ` 方法添加回调函数。
2. `async` 函数内部 `return` 语句返回的值，会成为 `then` 方法回调函数的参数
3. `async` 函数返回的 `Promise` 对象，必须等到内部所有 `await` 命令后面的 `Promise` 对象执行完，才会发生状态改变，除非遇到 `return` 语句或者抛出错误
4. `async` 函数内部抛出错误，会导致返回的 `Promise` 对象变为 `reject` 状态。抛出的错误对象会被 `catch` 方法回调函数接收到

`await` 命令: 

1. `await` 命令后面是一个 `Promise` 对象，返回该对象的结果。如果不是 `Promise` 对象，就直接返回对应的值
2. `await` 命令后面是一个`thenable`对象（即定义 then 方法的对象），那么`await`会将其等同于 `Promise` 对象

使用注意点：

- `await` 命令后面的 `Promise` 对象，运行结果可能是 `rejected`，所以最好把 `await` 命令放在 `try...catch` 代码块中
- 多个 `await` 命令后面的异步操作，如果不存在继发关系，最好让它们同时触发
- `await` 命令只能用在 `async` 函数之中，如果用在普通函数，就会报错


# 性能优化

## 雅虎优化列表

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

## 前端性能优化

加载时优化，主要解决的就是让一个网站加载过程更快，比如压缩文件大小、使用CDN加速等方式可以优化加载性能。检查加载性能的指标一般看以下两点，其中主要的脚本代码为 `new Date().getTime() - performance.timing.navigationStart`。

1. 白屏时间。指的是从输入网址，到页面开始显示内容的时间。将代码脚本放在 `</head>` 前面就能获取白屏时间。
2. 首屏时间。指从输入网址，到首屏页面内容渲染完毕的时间。在 `window.onload` 事件中执行脚本代码，可以获取首屏时间。

运行时性能，是指页面运行时的性能表现，而不是页面加载时的性能。可以通过chrome开发者工具中的 Performance 面板来分析页面的运行时性能。

接下来就从加载时性能和运行时性能两个方面来讨论网站优化具体应该怎么做。

### 加载时性能优化

1. DNS 预解析
  - 浏览器缓存 ->系统缓存 ->路由器缓存 ->ISP DNS缓存 ->递归搜索
  - 用 meta 信息来告知浏览器, 当前页面要做 DNS 预解析
  - 在页面 header 中使用 link 标签来强制对 DNS 预解析
2. 优化 HTTP 请求
  - 使用 HTTP2 协议，二进制/多路复用/数据流/首部压缩/服务器推送
  - 静态资源采用 CDN 减少服务器压力，应付不必携带 cookie 的场景
  - 减少请求数量，将资源文件合并，利用 cookie/WebStorage 缓存数据
  - 减少请求大小，压缩资源文件，开启 Gzip 压缩
3. Webpack 优化
  - 按需加载代码，减少冗余代码
  - Tree shaking 减少冗余代码
4. 优化图片资源
  - 采用 SVG 或者字体图标
  - 利用雪碧图合并图片
  - 图片懒加载
5. 按需加载代码，减少冗余代码
  - 结合 import 动态引入组件
  - 减少 ES6 转为 ES5 的冗余代码
6. 服务器端渲染
  - 服务端发送完成的 HTML 文件，浏览器直接加载渲染，减少前后端交互
7. 资源加载顺序调整
  - 将 script 标签放到 body 后面，或添加 defer 属性进行异步下载，避免加载阻塞
  - 将 CSS 放在文件头部 head 位置，减少 HTML 加载完毕需要等待 CSS 加载的问题
  - 优化 CSS 选择器解析问题，减少选择器或优先级较低的选择器，因为 CSS 是从右往左加载的

### 运行时性能优化

1. 减少重绘与重排
  - 避免 table 布局
  - 分离读写操作
  - 样式集中改变，或改变类名而不是修样式
2. 避免页面卡顿
3. 长列表优化
  - 列表懒加载，添加骨架屏
  - 实现虚拟列表，只渲染可见区域附近的列表
4. 滚动事件性能优化
  - 防抖和节流
5. 使用 Web Workers
  - 进行多线程变成，不会阻塞 UI 渲染
6. 日常开发优化点
  1. 使用事件委托
  2. if-else 对比 switch
  3. 布局上使用 flexbox


图片的懒加载和预加载
如何确定页面的可用性时间，什么是 Performance API？
一个列表，假设有 100000 个数据，这个该怎么办？
怎么做 JS 代码 Error 统计？
如何编写高性能的 Javascript ？
为什么使用 setTimeout 实现 setInterval？怎么模拟？
什么是 requestAnimationFrame ？

# 搜索引擎优化

## SEO 工作原理

搜索引擎优化（Search engine optimization，简称 SEO），指为了提升网页在搜索引擎自然搜索结果中（非商业性推广结果）的收录数量以及排序位置而做的优化行为，是为了从搜索引擎中获得更多的免费流量，以及更好的展现形象。SEM（Search engine marketing，搜索引擎营销），则既包括了 SEO，也包括了付费的商业推广优化。

1. 爬虫抓取网页内容。一般爬虫抓取页面内容是先从一个页面出发，从中提取出其他页面的链接，然后当作下一个请求的对象，一直重复这个过程。所以要有良好的 SEO，需要你在各大网站上拥有外链，这样会提高你的网站被搜索引擎爬虫的几率。
2. 分析网页内容。爬虫拿到 HTML 之后，就会对其内容进行分析。一般需要进行去杂、分词、建立索引数据库。什么是索引数据库呢？简单地说就是记录一个词在哪些文档中出现、出现次数、出现的位置等等。为什么要建立索引数据库呢？是为了快速查找。
3. 搜索和排序。搜索会根据你输入的关键词，分别查询其对应的索引数据库，并对结果进行处理和排序。

## 编码阶段 SEO

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