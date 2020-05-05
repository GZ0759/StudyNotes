> 你不知道的JavaScript（中卷）  
> You Don’t Know JavaScript: Scope & Closures this & Object Prototypes  
> 2016年 8 月第1版    
> [开源图书地址](https://github.com/getify/You-Dont-Know-JS)

# 目录

<!-- TOC -->

- [第一部分 类型和语法](#第一部分-类型和语法)
  - [第1章 类型](#第1章-类型)
  - [第2章 值](#第2章-值)
  - [第3章 原生函数](#第3章-原生函数)
  - [第4章 强制类型转换](#第4章-强制类型转换)
  - [第5章 语法](#第5章-语法)
  - [附录A 混合环境 JavaScript](#附录a-混合环境-javascript)
- [第二部分 异步和性能](#第二部分-异步和性能)
  - [第1章 异步：现在与将来](#第1章-异步现在与将来)
  - [第2章 回调](#第2章-回调)
  - [第3章 Promise](#第3章-promise)
    - [3.1 什么是Promise](#31-什么是promise)
    - [3.2 具有 then 方法的鸭子类型](#32-具有-then-方法的鸭子类型)
    - [3.4  链式流](#34--链式流)
    - [3.5 错误处理](#35-错误处理)
    - [3.6 Promise 模式](#36-promise-模式)
    - [3.7 Promise API 概述](#37-promise-api-概述)
    - [3.8 Promise 局限性](#38-promise-局限性)
  - [第4章 生成器](#第4章-生成器)
    - [4.1 打破完整运行](#41-打破完整运行)
    - [4.2 生成器产生值](#42-生成器产生值)
    - [4.3 异步迭代生成器](#43-异步迭代生成器)
    - [4.4 生成器 +Promise](#44-生成器-promise)
    - [4.5 生成器委托](#45-生成器委托)
    - [4.6 生成器并发](#46-生成器并发)
    - [4.7 形实转换程序](#47-形实转换程序)
    - [4.8 ES6之前的生成器](#48-es6之前的生成器)
  - [第5章 程序性能](#第5章-程序性能)
    - [5.1 Web Worker](#51-Web-Worker)
    - [5.2 SIMD](#52-SIMD)
    - [5.3 asm.js](#53-asm.js)
  - [第6章 性能测试与调优](#第6章-性能测试与调优)
  - [附录A asynquence 库](#附录a-asynquence-库)
  - [附录B 高级异步模式](#附录b-高级异步模式)

<!-- /TOC -->

# 第一部分 类型和语法
## 第1章 类型

对语言引擎和开发人员来说，类型是值的内部特征，它定义了值的行为，以使其区别于其他值。

换句话说，如果语言引擎和开发人员对 42（数字）和 "42"（字符串）采取不同的处理方式，那就说明它们是不同的类型，一个是 number，一个是 string。通常我们对数字 42 进行数学运算，而对字符串 "42" 进行字符串操作，比如输出到页面。它们是不同的类型。

### 1.1 类型

要正确合理地进行类型转换，必须掌握 JavaScript 中的各个类型及其内在行为。几乎所有的 JavaScript 程序都会涉及某种形式的强制类型转换。

### 1.2 内置类型

JavaScript 有七种内置类型： 

- 空值（null） 
- 未定义（undefined）
- 布尔值（ boolean） 
- 数字（number） 
- 字符串（string） 
- 对象（object） 
- 符号（symbol， ES6 中新增） 

除对象之外，其他统称为“基本类型”。

可以用 typeof 运算符来查看值的类型，它返回的是类型的字符串值。有意思的是，这七种类型和它们的字符串值并不一一对应。

```javascript
typeof undefined     === "undefined"; // true
typeof true          === "boolean";   // true
typeof 42            === "number";    // true
typeof "42"          === "string";    // true
typeof { life: 42 }  === "object";    // true

// added in ES6!
typeof Symbol()      === "symbol";    // true
```

另外，null 是基本类型中唯一的一个“假值”类型， typeof 对它的返回值为 "object"。

```javascript
typeof null === "object"; // true

var a = null;
(!a && typeof a === "object"); // true
```

function（函数）也是 JavaScript 的一个内置类型。它实际上是 object 的一个“子类型”。具体来说，函数是“可调用对象”，它有一个内部属性`[[Call]]`，该属性使其可以被调用。函数对象的 length 属性是其声明的参数的个数。

数组也是对象。确切地说，它也是 object 的一个“子类型”，数组的元素按数字顺序来进行索引（而非普通像对象那样通过字符串键值），其 length 属性是元素的个数。

```javascript
typeof function a(){ /* .. */ } === "function"; // true

typeof [1,2,3] === "object"; // true
```

### 1.3 值和类型

JavaScript 中的变量是没有类型的，只有值才有。变量可以随时持有任何类型的值。也就是说，语言引擎不要求变量总是持有与其初始值同类型的值。一个变量可以现在被赋值为字符串类型值，随后又被赋值为数字类型值。

在对变量执行 typeof 操作时，得到的结果并不是该变量的类型，而是该变量持有的值的类型，因为 JavaScript 中的变量没有类型。typeof 运算符总是会返回一个字符串。

```js
var a = 42;
typeof a; // "number"

a = true;
typeof a; // "boolean"
```

#### 1.3.1 undefined 和 undeclared

已在作用域中声明但还没有赋值的变量，是 undefined 的。相反，还没有在作用域中声明过的变量，是 undeclared 的。对于 undeclared（或者 not defined）变量， typeof 照样返回 "undefined"。  

```javascript
var a;

a; // undefined
b; // ReferenceError: b is not defined

typeof a; // "undefined"
typeof b; // "undefined"
```

#### 1.3.2 typeof Undeclared

该安全防范机制对在浏览器中运行的 JavaScript 代码来说还是很有帮助的，因为多个脚本文件会在共享的全局命名空间中加载变量。  

如何在程序中检查全局变量 DEBUG 才不会出现 ReferenceError 错误。这时 typeof 的安全防范机制就成了我们的好帮手。

```js
// 这样会抛出错误
if (DEBUG) {
	console.log( "Debugging is starting" );
}
// 这样是安全的
if (typeof DEBUG !== "undefined") {
	console.log( "Debugging is starting" );
}
```

还有一种不用通过 typeof 的安全防范机制的方法，就是检查所有全局变量是否是全局对象的属性，浏览器中的全局对象是 window。与 undeclared 变量不同，访问不存在的对象属性（甚至是在全局对象 window 上）不会产生 ReferenceError 错误。

```js
if (window.DEBUG) {
	// ..
}
```

还有一些人喜欢使用“依赖注入”（dependency injection）设计模式，就是将依赖通过参数显式地传递到函数中。

```js
function doSomethingCool(FeatureXYZ) {
	var helper = FeatureXYZ ||
	  function() { /*.. default feature ..*/ };
	var val = helper();
	// ..
}
```

## 第2章 值	

### 2.1 数组

和其他强类型语言不同，在 JavaScript 中，数组可以容纳任何类型的值，可以是字符串、 数字、对象（object），甚至是其他数组（多维数组就是通过这种方式来实现的）。对数组声明后即可向其中加入值，不需要预先设定大小。

在创建“稀疏”数组（sparse array，即含有空白或空缺单元的数组）时要特别注意。

```js
var a = [ ];
a[0] = 1;
// 此处没有设置a[1]单元
a[2] = [ 3 ];

a[1]; // undefined
a.length; // 3
```

数组通过数字进行索引，但有趣的是它们也是对象，所以也可以包含字符串键值和属性 （但这些并不计算在数组长度内）。

```js
var a = [ ];
a[0] = 1;
a["foobar"] = 2;

a.length; // 1
a["foobar"]; // 2
a.foobar; // 2
```

这里有个问题需要特别注意，如果字符串键值能够被强制类型转换为十进制数字的话，它就会被当作数字索引来处理。在数组中加入字符串键值或属性并不是一个好主意。建议使用对象来存放键值或属性值，用数组来存放数字索引值。

```js
var a = [ ];
a["13"] = 42;
a.length; // 14
```

**类数组**。有时需要将类数组（一组通过数字索引的值）转换为真正的数组，这一般通过数组工具函数（如 `indexOf(..)`、 `concat(..)`、 `forEach(..)` 等）来实现。

例如，一些 DOM 查询操作会返回 DOM 元素列表，它们并非真正意义上的数组，但十分类似。另一个例子是通过 arguments 对象（类数组）将函数的参数当作列表来访问。

工具函数 `slice(..)` 经常被用于这类转换。

```js
function foo() {
	var arr = Array.prototype.slice.call( arguments );
	arr.push( "bam" );
	console.log( arr );
}
foo( "bar", "baz" ); // ["bar","baz","bam"]
```

用 ES6 中的内置工具函数 `Array.from(..) `也能实现同样的功能。

```js
var arr = Array.from( arguments );
```

### 2.2 字符串

字符串和数组的确很相似，它们都是类数组，都有 length 属性以及 `indexOf(..)`（从 ES5 开始数组支持此方法）和 `concat(..)` 方法。

```js
var a = "foo";
var b = ["f","o","o"];

a.length; // 3
b.length; // 3

a.indexOf( "o" ); // 1
b.indexOf( "o" ); // 1

var c = a.concat( "bar" ); // "foobar"
var d = b.concat( ["b","a","r"] ); // ["f","o","o","b","a","r"]

a === c; // false
b === d; // false

a; // "foo"
b; // ["f","o","o"]
```

JavaScript 中字符串是不可变的，而数组是可变的。字符串不可变是指字符串的成员函数不会改变其原始值，而是创建并返回一个新的字符串。而数组的成员函数都是在其原始值上进行操作。 

许多数组函数用来处理字符串很方便。虽然字符串没有这些函数，但可以通过“借用”数组的非变更方法来处理字符串。

```js
a.join; // undefined
a.map; // undefined
var c = Array.prototype.join.call( a, "-" );
var d = Array.prototype.map.call( a, function(v){
	return v.toUpperCase() + ".";
} ).join( "" );
c; // "f-o-o"
d; // "F.O.O."
```

另一个不同点在于字符串反转（JavaScript 面试常见问题）。数组有一个字符串没有的可变更成员函数 `reverse()`。可惜我们无法“借用”数组的可变更成员函数，因为字符串是不可变的。

```js
a.reverse; // undefined
b.reverse(); // ["!","o","O","f"]
b; // ["f","O","o","!"]
```

一个变通（破解）的办法是先将字符串转换为数组，待处理完后再将结果转换回字符串。

```js
var c = a
// 将a的值转换为字符数组
.split( "" )

// 将数组中的字符进行倒转
.reverse()

// 将数组中的字符拼接回字符串
.join( "" );

c; // "oof"
```

### 2.3 数字

JavaScript 只有一种数值类型： number（数字），包括“整数”和带小数的十进制数。此处 “整数”之所以加引号是因为和其他语言不同， JavaScript 没有真正意义上的整数。JavaScript 中的“整数”就是没有小数的十进制数。所以 42.0 即等同于“整数” 42。

与大部分现代编程语言（包括几乎所有的脚本语言）一样， JavaScript 中的数字类型是基于 IEEE 754 标准来实现的，该标准通常也被称为“浮点数”。 JavaScript 使用的是“双精度”格式（即 64 位二进制）。  

特别大和特别小的数字默认用指数格式显示，与 `toExponential()` 函数的输出结果相同。

```js
var a = 5E10;
a; // 50000000000
a.toExponential(); // "5e+10"
var b = a * a;
b; // 2.5e+21
var c = 1 / a;
c; // 2e-11
```

由于数字值可以使用Number对象进行封装，因此数字值可以调用Number.prototype中的方法。例如， `tofixed(..)` 方法可指定小数部分的显示位数。输出结果实际上是给定数字的字符串形式，如果指定的小数部分的显示位数多于实际位数就用 0 补齐。

```js
var a = 42.59;
a.toFixed( 0 ); // "43"
a.toFixed( 1 ); // "42.6"
a.toFixed( 2 ); // "42.59"
a.toFixed( 3 ); // "42.590"
a.toFixed( 4 ); // "42.5900"
```

`toPrecision(..)` 方法用来指定有效数位的显示位数：

```js
var a = 42.59;
a.toPrecision( 1 ); // "4e+1"
a.toPrecision( 2 ); // "43"
a.toPrecision( 3 ); // "42.6"
a.toPrecision( 4 ); // "42.59"
a.toPrecision( 5 ); // "42.590"
a.toPrecision( 6 ); // "42.5900"
```

方法不仅适用于数字变量，也适用于数字常量。不过对于 . 运算符需要给予特别注意，因为它是一个有效的数字字符，会被优先识别为数字常量的一部分，然后才是对象属性访问运算符。

```js
// 无效语法：
42.toFixed( 3 ); // SyntaxError
// 下面的语法都有效：
(42).toFixed( 3 ); // "42.000"
0.42.toFixed( 3 ); // "0.420"
42..toFixed( 3 ); // "42.000"
```

一些工具库扩展了 Number.prototype 的内置方法以提供更多的数值操作，比如用 `10..makeItRain()` 方法来实现十秒钟金钱雨动画等效果。

数字常量还可以用其他格式来表示，如二进制、八进制和十六进制。当前的 JavaScript 版本都支持这些格式：

```js
0xf3; // 243的十六进制
0Xf3; // 同上
0363; // 243的八进制
```

二进制浮点数最大的问题，二进制浮点数中的 0.1 和 0.2 并不是十分精确，它们相加的结果并非刚好等于0.3，而是一个比较接近的数字 0.30000000000000004，所以条件判断结果为 false。

```js
0.1 + 0.2 === 0.3; // false
```

判断 0.1 + 0.2 和 0.3 是都相等最常见的方法是设置一个误差范围值，通常称为“机器精度”（machine epsilon）。

从 ES6 开始，该值定义在 `Number.EPSILON` 中，我们可以直接拿来用，也可以为 ES6 之前的版本写 polyfill：

```js
if (!Number.EPSILON) {
	Number.EPSILON = Math.pow(2,-52);
}
```

可以使用 `Number.EPSILON` 来比较两个数字是否相等（在指定的误差范围内）：

```js
function numbersCloseEnoughToEqual(n1,n2) {
	return Math.abs( n1 - n2 ) < Number.EPSILON;
}
var a = 0.1 + 0.2;
var b = 0.3;
numbersCloseEnoughToEqual( a, b ); // true
numbersCloseEnoughToEqual( 0.0000001, 0.0000002 ); // false
```

要检测一个值是否是整数，可以使用 ES6 中的 `Number.isInteger(..)` 方法。

```js
Number.isInteger( 42 ); // true
Number.isInteger( 42.000 ); // true
Number.isInteger( 42.3 ); // false
```

也可以为 ES6 之前的版本 polyfill `Number.isInteger(..)` 方法：

```js
if (!Number.isInteger) {
	Number.isInteger = function(num) {
		return typeof num == "number" && num % 1 == 0;
	};
}
```

要检测一个值是否是安全的整数，可以使用 ES6 中的 Number.isSafeInteger(..) 方法：

```js
Number.isSafeInteger( Number.MAX_SAFE_INTEGER ); // true
Number.isSafeInteger( Math.pow( 2, 53 ) ); // false
Number.isSafeInteger( Math.pow( 2, 53 ) - 1 ); // true
```

可以为 ES6 之前的版本 polyfill Number.isSafeInteger(..) 方法：

```js
if (!Number.isSafeInteger) {
	Number.isSafeInteger = function(num) {
		return Number.isInteger( num ) &&
		Math.abs( num ) <= Number.MAX_SAFE_INTEGER;
	};
}
```

### 2.4 特殊数值

#### 2.4.1 不是值的值

undefined 类型只有一个值，即 undefined。 null 类型也只有一个值，即 null。它们的名称既是类型也是值。

undefined 和 null 常被用来表示“空的”值或“不是值”的值。二者之间有一些细微的差别。

- null 指空值（empty value）
- undefined 指没有值（missing value）

或者：

- undefined 指从未赋值
- null 指曾赋过值，但是目前没有值

null 是一个特殊关键字，不是标识符，我们不能将其当作变量来使用和赋值。然而 undefined 却是一个标识符，可以被当作变量来使用和赋值。

#### 2.4.2 undefined

在非严格模式下，我们可以为全局标识符 undefined 赋值（这样的设计实在是欠考虑！）：

```js
function foo() {
	undefined = 2; // 非常糟糕的做法！
}
foo();

function foo() {
	"use strict";
	undefined = 2; // TypeError!
}
foo();
```

undefined 是一个内置标识符，它的值为 undefined，通过 void 运算符即可得到该值。

表达式 `void ___` 没有返回值，因此返回结果是 undefined。 void 并不改变表达式的结果，只是让表达式不返回值。按惯例我们用 `void 0` 来获得 undefined（这主要源自 C 语言，当然使用 void true 或其他 void 表达式也是可以的）。 `void 0`、 `void 1` 和 undefined 之间并没有实质上的区别。

```js
var a = 42;
console.log( void a, a ); // undefined 42
```

void 运算符在其他地方也能派上用场，比如不让表达式返回任何结果（即使其有副作用）。

```js
function doSomething() {
	// 注： APP.ready 由程序自己定义
	if (!APP.ready) {
		// 稍后再试
		return void setTimeout( doSomething,100 );
	}
	var result;
	// 其他
	return result;
}
// 现在可以了吗？
if (doSomething()) {
	// 立即执行下一个任务
}
```

很多开发人员喜欢分开操作，效果都一样，只是没有使用 void 运算符：

```js
if (!APP.ready) {
	// 稍后再试
	setTimeout( doSomething,100 );
	return;
}
```

#### 2.4.3 特殊的数字

不是数字的数字。如果数学运算的操作数不是数字类型（或者无法解析为常规的十进制或十六进制数字），就无法返回一个有效的数字，这种情况下返回值为 NaN。换句话说，“不是数字的数字”仍然是数字类型。NaN 是一个“警戒值”（sentinel value，有特殊用途的常规值），用于指出数字类型中的错误情况，即“执行数学运算没有成功，这是失败后返回的结果”。

```js
var a = 2 / "foo"; // NaN
typeof a === "number"; // true
```

有人也许认为如果要检查变量的值是否为 NaN，可以直接和 NaN 进行比较，就像比较 null 和 undefined 那样。实则不然。NaN 是一个特殊值，它和自身不相等，是唯一一个非自反的值。

```js
var a = 2 / "foo";
a == NaN; // false
a === NaN; // false
```

可以使用内建的全局工具函数 `isNaN(..)` 来判断一个值是否是 NaN。然而操作起来并非这么容易。 `isNaN(..)` 有一个严重的缺陷，它的检查方式过于死板，就是“检查参数是否不是 NaN，也不是数字”。

```js
var a = 2 / "foo";
var b = "foo";
a; // NaN
b; "foo"
window.isNaN( a ); // true
window.isNaN( b ); // true——晕！
```

从 ES6 开始我们可以使用工具函数 `Number.isNaN(..)`。 ES6 之前的浏览器的 polyfill 如下：

```js
if (!Number.isNaN) {
	Number.isNaN = function(n) {
	return (
		typeof n === "number" &&
		  window.isNaN( n )
		);
	};
}
var a = 2 / "foo";
var b = "foo";
Number.isNaN( a ); // true
Number.isNaN( b ); // false——好！
```

实际上还有一个更简单的方法，即利用 NaN 不等于自身这个特点。 NaN 是 JavaScript 中唯一一个不等于自身的值。

```js
if (!Number.isNaN) {
	Number.isNaN = function(n) {
		return n !== n;
	};
}
```

无穷数。熟悉传统编译型语言（如 C）的开发人员可能都遇到过编译错误（compiler error）或者运行时错误（runtime exception），例如“除以 0”。

```js
var a = 1 / 0; // Infinity
var b = -1 / 0; // -Infinity
```

JavaScript 使用有限数字表示法（finite numeric representation，即之前介绍过的 IEEE 754浮点数），所以和纯粹的数学运算不同， JavaScript 的运算结果有可能溢出，此时结果为Infinity 或者 -Infinity。

```js
var a = Number.MAX_VALUE; // 1.7976931348623157e+308
a + a; // Infinity
a + Math.pow( 2, 970 ); // Infinity
a + Math.pow( 2, 969 ); // 1.7976931348623157e+308
```

零值。-0 除了可以用作常量以外，也可以是某些数学运算的返回值。加法和减法运算不会得到负零（negative zero）。

```js
var a = 0 / -3; // -0
var b = 0 * -3; // -0
```

要区分 -0 和 0，不能仅仅依赖开发调试窗口的显示结果，还需要做一些特殊处理：

```js
function isNegZero(n) {
n = Number( n );
return (n === 0) && (1 / n === -Infinity);
}
isNegZero( -0 ); // true
isNegZero( 0 / -3 ); // true
isNegZero( 0 ); // false
```

#### 2.4.4 特殊等式

特殊等式。ES6 中新加入了一个工具方法` Object.is(..)` 来判断两个值是否绝对相等。

```js
var a = 2 / "foo";
var b = -3 * 0;
Object.is( a, NaN ); // true
Object.is( b, -0 ); // true
Object.is( b, 0 ); // false
```

对于 ES6 之前的版本， Object.is(..) 有一个简单的 polyfill。

```js
if (!Object.is) {
	Object.is = function(v1, v2) {
	// 判断是否是-0
	if (v1 === 0 && v2 === 0) {
		return 1 / v1 === 1 / v2;
	}
	// 判断是否是NaN
	if (v1 !== v1) {
		return v2 !== v2;
	}
	// 其他情况
	return v1 === v2;
	};
}
```

能使用 == 和 === 时就尽量不要使用` Object.is(..)`，因为前者效率更高、 更为通用。` Object.is(..)` 主要用来处理那些特殊的相等比较。

### 2.5 值和引用

JavaScript 中没有指针，引用的工作机制也不尽相同。在 JavaScript 中变量不可能成为指向另一个变量的引用。JavaScript 引用指向的是值。如果一个值有 10 个引用，这些引用指向的都是同一个值， 它们相互之间没有引用 / 指向关系。JavaScript 对值和引用的赋值 / 传递在语法上没有区别，完全根据值的类型来决定。

简单值（即标量基本类型值， scalar primitive） 总是通过值复制的方式来赋值 / 传递，包括 null 、 undefined、字符串、数字、布尔和 ES6 中的 symbol。

复合值（compound value）——对象（包括数组和封装对象）和函数，则总是通过引用复制的方式来赋值 / 传递。由于引用指向的是值本身而非变量，所以一个引用无法更改另一个引用的指向。  

由于引用指向的是值本身而非变量，所以一个引用无法更改另一个引用的指向。

```js
var a = [1,2,3];
var b = a;
a; // [1,2,3]
b; // [1,2,3]

// 然后
b = [4,5,6];
a; // [1,2,3]
b; // [4,5,6]
```

函数参数就经常让人产生这样的困惑。

```js
function foo(x) {
x.push( 4 );
x; // [1,2,3,4]
// 然后
x = [4,5,6];
x.push( 7 );
x; // [4,5,6,7]
}
var a = [1,2,3];
foo( a );
a; // 是[1,2,3,4]，不是[4,5,6,7]
```

我们不能通过引用 x 来更改引用 a 的指向，只能更改 a 和 x 共同指向的值。

```js
function foo(x) {
x.push( 4 );
x; // [1,2,3,4]
// 然后
x.length = 0; // 清空数组
x.push( 4, 5, 6, 7 );
x; // [4,5,6,7]
}
var a = [1,2,3];
foo( a );
a; // 是[4,5,6,7]，不是[1,2,3,4]
```

我们无法自行决定使用值复制还是引用复制，一切由值的类型来决定。

如果通过值复制的方式来传递复合值（如数组），就需要为其创建一个复本，这样传递的就不再是原始值。 

```js
foo( a.slice() );
```

如果要将标量基本类型值传递到函数内并进行更改，就需要将该值封装到一个复合值（对象、数组等）中，然后通过引用复制的方式传递。

```js
function foo(wrapper) {
	wrapper.a = 42;
}
var obj = {
	a: 2
};
foo( obj );
obj.a; // 42
```

与预期不同的是，虽然传递的是指向数字对象的引用复本，但我们并不能通过它来更改其中的基本类型值。

```js
function foo(x) {
	x = x + 1;
	x; // 3
}
var a = 2;
var b = new Number( a ); // Object(a)也一样
foo( b );
console.log( b ); // 是2，不是3
```

## 第3章 原生函数	

常见的原生函数有：  
- String() 
- Number() 
- Boolean() 
- Array() 
- Object() 
- Function() 
- RegExp() 
- Date() 
- Error() 
- Symbol()。

实际上，它们就是内建函数，内建函数可以被当作构造函数来使用，但是通过构造函数创建出来的是封装了基本类型值的封装对象。

```javascript
var a = new String( "abc" );
typeof a; // 是"object"，不是"String"
a instanceof String; // true
Object.prototype.toString.call( a ); // "[object String]"
```



内部属性[[Class]] 。所有typeof返回值为“object”的对象都包含一个内部属性[[Class]] ，这个属性无法直接访问，一般通过Object.prototype.toString()来查看。数组的内部[[Class]] 属性值是Array，正则表达式的值是RegExp，一般都是与该对象的内建原生函数相对应。但是Null()和Undefined()这样的原生构造函数并不存在，但是内部[[Class]] 属性值依然是Null和Undefined。

封装对象包装。字符串、数字和布尔这几种基本类型值，通常称为“包装”，一般这几种基本类型值会被各自的封装对象自动包装。如果想要自行封装基本类型值，可以使用Object(..)函数，不带new关键字。

拆封。如果想要得到封装对象中的基本类型值，可以使用valueOf()函数。在需要用到封装对象中的基本类型值的地方会发生隐式拆封。

原生函数作为构造函数。构造函数 Array(..) 不要求必须带 new 关键字。不带时，它会被自动补上。因此 Array(1,2,3) 和 new Array(1,2,3) 的效果是一样的。Array 构造函数只带一个数字参数的时候，该参数会被作为数组的预设长度（length），而非只充当数组中的一个元素。同样，除非万不得已，否则尽量不要使用 Object(..)/Function(..)/RegExp(..)。相较于其他原生构造函数， Date(..) 和 Error(..) 的用处要大很多，因为没有对应的常量形式来作为它们的替代。

ES6 中新加入了一个基本数据类型 ——符号（Symbol）。符号是具有唯一性的特殊值（并 非绝对），用它来命名对象属性不容易导致重名。ES6 中有一些预定义符号，以 Symbol 的静态属性形式出现，如 Symbol.create、 Symbol. iterator 等。我们可以使用 Symbol(..) 原生构造函数来自定义符号。但它比较特殊，不能带 new 关键字，否则会出错。

## 第4章 强制类型转换	

值类型转换。将值从一种类型转换为另一种类型通常称为类型转换（type casting），这是显式的情况；隐式的情况称为强制类型转换（coercion）。  JavaScript 中的强制类型转换总是返回标量基本类型值（参见第 2 章），如字 符串、数字和布尔值，不会返回对象和函数。  

抽象值操作。

抽象操作 ToString。它负责处理非字符串到字符串的强制类型转换。 对大多数简单值来说， JSON 字符串化和 toString() 的效果基本相同，只不过序列化的结果总是字符串。如果对象中定义了 toJSON() 方法， JSON 字符串化时会首先调用该方法，然后用它的返回值来进行序列化。  

> 基本类型值的字符串化规则为： null 转换为 "null"， undefined 转换为 "undefined"， true 转换为 "true"。
>
> 数字的字符串化则遵循通用规则。
>
> 对普通对象来说，除非自行定义，否则 toString()（Object.prototype.toString()）返回内部属性 [[Class]] 的值，如 "[object Object]"。  
>
> 数组的默认 toString() 方法经过了重新定义，将所有单元字符串化以后再用 "," 连接起来。

抽象操作 ToNumber。ToNumber 对字符串的处理基本遵循数字常量的相关规则 / 语法。处理失败时返回 NaN（处理数字常量失败时会产生语法错误）。对象（包括数组）会首先被转换为相应的基本类型值，如果返回的是非数字的基本类型值，则再遵循以上规则将其强制转换为数字。  

为了将值转换为相应的基本类型值，抽象操作 ToPrimitive 会首先检查该值是否有 valueOf() 方法。 如果有并且返回基本类型值，就使用该值进行强制类型转换。如果没有就使用 toString() 的返回值（如果存在）来进行强制类型转换。 如果 valueOf() 和 toString() 均不返回基本类型值，会产生 TypeError 错误。  

抽象操作ToBoolean。从逻辑上说，假值列表以外的都应该是真值（truthy）。浏览器在某些特定情况下，在常规 JavaScript 语法基础上自己创建了一些外来（exotic）值，这些就是“假值对象”。所有字符串都是真值。不过 "" 除外，因为它是假值列表中唯一的字符串。[]、 {} 和 function(){} 都不在假值列表中，因此它们都是真值。  

显式强制类型转换。字符串和数字之间的转换时通过String()和Number()这两个内建函数来实现的，分别遵循前面的TOString()和ToNumber()规则。它们前面没有new关键字，并不创建封装对象。

一元运算符+的另一个常见用途是将日期（Date）对象强制类型转换为数字。`~`运算符首先将值强制类型转换为32位数字，然后执行字位操作“非”（对每一个字位进行反转）。`~`和 indexOf() 一起可以将结果强制类型转换（实际 上仅仅是转换）为真 / 假值。

解析字符串中的数字和将字符串强制类型转换为数字的返回结果都是数字。解析允许字符串中含有非数字字符，解析按从左到右的顺序，如果遇到非数字字符就停止。而转换不允许出现非数字字符，否则会失败并返回 NaN。解析字符串中的浮点数可以使用parseFloat()函数，parseInt(..) 先将参数强制类型转换为字符串再进行解析。

与前面的 String(..) 和 Number(..) 一样， Boolean(..)（不带 new）是显式的 ToBoolean 强 制类型转换。在 if(..).. 这样的布尔值上下文中，如果没有使用 Boolean(..) 和 !!，就会自动隐式地进行 ToBoolean 转换。建议使用 Boolean(..) 和 !! 来进行显式转换以便让代码更清晰易读。  

隐式强制类型转换，指的是那些隐蔽的强制类型转换。

如果某个操作数是字符串或者能够通过以下步骤转换为字符串的话， + 将进行拼接操作。如果其中一个操作数是对象（包括数组），则首先对其调用 ToPrimitive 抽象操作，该抽象操作再调用[[DefaultValue]]，以数字作为上下文。

我们可以将数字和空字符串 "" 相 + 来将其转换为字符串。a + "" 会对 a 调用 valueOf() 方法，然后通过 ToString 抽象操作将返回值转换为字符串。而 String(a) 则是直接调用 ToString()。  

`-` 是数字减法运算符，因此 a - 0 会将 a 强制类型转换为数字。也可以使用 a * 1 和 a / 1，因为这两个运算符也只适用于数字。  

相对布尔值，数字和字符串操作中的隐式强制类型转换还算比较明显。下面的情况会发生布尔值隐式强制类型转换。  

1. if (..) 语句中的条件判断表达式。 
2. for ( .. ; .. ; .. ) 语句中的条件判断表达式（第二个）。
3. while (..) 和 do..while(..) 循环中的条件判断表达式。 
4. ? : 中的条件判断表达式。
5. 逻辑运算符 ||（逻辑或）和 &&（逻辑与）左边的操作数（作为条件判断表达式）。  

逻辑运算符 ||（或）和 &&（与）的返回值是两个操作数中的一个（且仅一个）。即选择两个操作数中的一个，然后返回它的值。

|| 和 && 首先会对第一个操作数（a 和 c）执行条件判断，如果其不是布尔值（如上例）就先进行 ToBoolean 强制类型转换，然后再执行条件判断。 对于 || 来说，如果条件判断结果为 true 就返回第一个操作数的值，如果为 false 就返回第二个操作数的值。 && 则相反，如果条件判断结果为 true 就返回第二个操作数的值，如果为 false 就返 回第一个操作数的值。  

a = a || "hello"（又称为 C# 的“空值合并运算符”的 JavaScript 版本）检查变量 a，如果还未赋值（或者为假值），就赋予它一个默认值（"hello"）。这种用法很常见，但是其中不能有假值，除非加上更明确的条件判断，或者转而使用 ? : 三元表达式。  

a && foo()  就是如果第一个操作数为真值，则 && 运算符“选择”第二个操作数作为返回值，这也叫作“守护运算符” ，即前面的表达式为后面的表达式“把关” 。开发人员通常使用 if (a) { foo(); }。但 JavaScript 代码压缩工具用的是 a && foo()，因为更简洁。  

ES6 允许从符号到字符串的显式强制类型转换，然而隐式强制类型转换会产生错误。符号不能够被强制类型转换为数字（显式和隐式都会产生错误），但可以被强制类型转换为布尔值（显式和隐式结果都是 true）。  

宽松相等（loose equals） == 和严格相等（strict equals） === 都用来判断两个值是否“相 等”，但是它们之间有一个很重要的区别，特别是在判断条件上。== 允许在相等比较中进行强制类型转换，而 === 不允许。宽松不相等（loose not-equality） != 就是 == 的相反值， !== 同理。  

字符串和数字的例子来解释 == 中的强制类型转换。(1) 如果 Type(x) 是数字， Type(y) 是字符串，则返回 x == ToNumber(y) 的结果。 (2) 如果 Type(x) 是字符串， Type(y) 是数字，则返回 ToNumber(x) == y 的结果。  

其他类型和布尔类型之间的相等比较。 (1) 如果 Type(x) 是布尔类型，则返回 ToNumber(x) == y 的结果； (2) 如果 Type(y) 是布尔类型，则返回 x == ToNumber(y) 的结果。  

null 和 undefined 之间的相等比较。(1) 如果 x 为 null， y 为 undefined，则结果为 true。 (2) 如果 x 为 undefined， y 为 null，则结果为 true。在 == 中 null 和 undefined 相等（它们也与其自身相等），除此之外其他值都不存在这种情况。条件判断 a == null 仅在 a 为非 null 和 undefined 时才成立，除此之外其他值都不成立，包括 0、 false 和 "" 这样的假值。  

对象和非对象之间的相等比较。(1) 如果 Type(x) 是字符串或数字， Type(y) 是对象，则返回 x == ToPrimitive(y) 的结果； (2) 如果 Type(x) 是对象， Type(y) 是字符串或数字，则返回 ToPromitive(x) == y 的结果。  

与 == 和 === 的完整性检查一样，我们应该在必要和安全的情况下使用抽象关系的强制类型转换，如： 42 < "43"。换句话说就是为了保证安全，应该对关系比较中的值进行显式强制类型转换  

## 第5章 语法	

语句和表达式。语句都有一个结果值。获得结果值最直接的方法是在浏览器开发控制台中输入语句，默认情况下控制台会显示所 执行的最后一条语句的结果值。规范定义 var 的结果值是 undefined。语法不允许我们获得语句的结果值并将其赋值给另一个变量（至少目前不行），但可以使用万恶的 eval(..)（又读作“evil”）来获得结果值，ES7 规范有一项“do 表达式”（do expression）提案与之相似。

最常见的有副作用（也可能没有）的表达式是函数调用，表达式副作用也可能与++ 运算符有关。其它表达式，例如delete ，如果操作成功， delete 返回 true，否则返回 false。其副作用是属性被从对象中删除（或 者单元从 array 中删除）。a = 42 中的 = 运算符看起来没有副作用，实际上它的结果值是 42，适用于多个赋值语句串联时。

上下文。用大括号定义对象常量。{ .. } 和 for/while 循环以及 if 条件语句中代码块的作用基本相同。大括号也可以是代码块，在`{} + []; // 0`  中 {} 被当作一个独立的空代码块（不执行任何操作）。从 ES6 开始， { .. } 也可用于“解构赋值” ，特别是对象的解构。{ .. } 还可以用作函数命名参数的对象解构，方便隐式地用对象属性赋值。JavaScript 没有 else if，但 if 和 else 只包含单条语句的时候可以省略代码块的 { }，所以 else if (){} 等于 else { if (){} }的结果。

运算符优先级。对 && 和 || 来说，如果从左边的操作数能够得出结果，就可以忽略右边的操作数。我们将 这种现象称为“短路”（即执行最短路径）。一般说来，运算符的关联（associativity）不是从左到右就是从右到左，这取决于组合 （grouping）是从左开始还是从右开始。

自动分号。有时 JavaScript 会自动为代码行补上缺失的分号，即自动分号插入（Automatic Semicolon Insertion， ASI）  。请注意， ASI 只在换行符处起作用，而不会在代码行的中间插入分号。语句代码块结尾不用带 ;，所以不需要用到 ASI  。

错误。JavaScript 不仅有各种类型的运行时错误（TypeError、 ReferenceError、 SyntaxError 等），它的语法中也定义了一些编译时错误。在编译阶段发现的代码错误叫作“早期错误”（early error）。语法错误是早期错误的一种 （如 a = ,）。另外，语法正确但不符合语法规则的情况也存在。  ES6 规范定义了一个新概念，叫作 TDZ（Temporal Dead Zone，暂时性死区）。 TDZ 指的是由于代码中的变量还没有初始化而不能被引用的情况。  

在 ES6 之前，获得函数所有参数的唯一途径就是 arguments 数组。此外，即使将命名参数和 arguments 数组混用也不会出错，只需遵守一个原则，即不要同时访问命名参数和其对应的 arguments 数组单元。  

finally 中的代码总是会在 try 之后执行，如果有 catch 的话则在 catch 之后执行。也可以 将 finally 中的代码看作一个回调函数，即无论出现什么情况最后一定会被调用。如果 finally 中抛出异常（无论是有意还是无意），函数就会在此处终止。如果此前 try 中 已经有 return 设置了返回值，则该值会被丢弃。finally 中的 return 会覆盖 try 和 catch 中 return 的返回值。

## 附录A 混合环境 JavaScript	

JavaScript 语言的官方名称是 ECMAScript（指的是管理它的 ECMA 标准），avaScript 是该语言的通用称谓，更确切地说，它 是该规范在浏览器上的实现。  

由ECMAScript实现的宿主环境提供的对象，可以理解为：浏览器提供的对象。所有的BOM和DOM都是宿主对象。 

声明一个全局变量（使用 var 或者不使用）的结果并不仅仅是创建一个全局变量，而且还会在 global 对象（在浏览器中为 window）中创建一个同名属性。  由于浏览器演进的历史遗留问题，在创建带有 id 属性的 DOM 元素时也会创建同名的全局变量。  

一个广为人知的 JavaScript 的最佳实践是：不要扩展原生原型。  

如果能够预见哪些方法会在将来成为新的标准，如 Array.prototype.foobar，那么就可以 完全放心地使用当前的扩展版本。这种情况一般称为 polyfill（或者 shim）。polyfill 能有效地为不符合最新规范的老版本浏览器填补缺失的功能，让你能够通过可靠的 代码来支持所有你想要支持的运行环境。  

`<script> .. </script> `加载的文件或者包含内联代码，像是互相独立的JavaScript程序，但其实它们共享 global 对象（在浏览器中则是 window），也就是说这些文件中的代码在共享的命名空间中运行，并相互交互。  但是全局变量作用域的提升机制在这些边界中不适用。

```javascript
// The following code would not work (because foo()'s declaration isn't yet declared)
<script>foo();</script>
<script>
  function foo() { .. }
</script>

// But either of these would work instead:
<script>
  foo();
  function foo() { .. }
</script>

// Or:
<script>
  function foo() { .. }
</script>
<script>foo();</script>
```



在 ES5 之前，保留字也不能用来作为对象常量中的属性名称或者键值，但是现在已经没有这个限制。 需要注意的是，在一些版本较老的浏览器中（主要是 IE），这些规则并不完全适用，有时候将保留字作为对象属性还是会出错。所以需要在所有要支持的浏览器中仔细测试。   

# 第二部分 异步和性能	

# 第1章 异步：现在与将来	

所有重要的程序（特别是 JavaScript 程序）都需要通过这样或那样的方法来管理这段时间间隙，这时可能是在等待用户输入、从数据库或文件系统中请求数据、通过网络发送数据并等待响应，或者是在以固定时间间隔执行重复任务（比如动画）。在诸如此类的场景中，程序都需要管理这段时间间隙的状态。

程序中现在运行的部分和将来运行的部分之间的关系就是异步编程的核心。  

## 1.1 分块的程序

可以把 JavaScript 程序写在单个 `.js` 文件中，但是这个程序几乎一定是由多个块构成的。这些块中只有一个是现在执行，其余的则会在将来执行。最常见的块单位是函数。

现在无法完成的任务将会异步完成，因此并不会出现人们本能地认为会出现的或希望出现的阻塞行为。  

```js
// ajax(..)是某个库中提供的某个Ajax函数
var data = ajax( "http://some.url.1" );
console.log( data );
// 啊哦！ data通常不会包含Ajax结果
```

从现在到将来的“等待”，最简单的方法（但绝对不是唯一的，甚至也不是最好的！）是使用一个通常称为回调函数的函数。

```js
// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", function myCallbackFunction(data){
	console.log( data ); // 耶！这里得到了一些数据！
} );
```

你有不同的意见？我知道，但为了避免回调函数引起的混乱并不足以成为使用阻塞式同步Ajax 的理由。

举例来说，考虑一下下面这段代码：

```js
function now() {
	return 21;
}
function later() {
	answer = answer * 2;
	console.log( "Meaning of life:", answer );
}
var answer = now();
setTimeout( later, 1000 ); // Meaning of life: 42
```

这个程序有两个块： 现在执行的部分，以及将来执行的部分。这两块的内容很明显，但这里我们还是要明确指出来。

现在：

```js
function now() {
	return 21;
}
function later() { .. }

var answer = now();
setTimeout( later, 1000 );
```

将来：

```js
answer = answer * 2;
console.log( "Meaning of life:", answer );
```

现在这一块在程序运行之后就会立即执行。但是， setTimeout(..) 还设置了一个事件（定时）在将来执行，所以函数 later() 的内容会在之后的某个时间（从现在起 1000 毫秒之后）执行。

任何时候，只要把一段代码包装成一个函数，并指定它在响应某个事件（定时器、鼠标点击、 Ajax 响应等）时执行，你就是在代码中创建了一个将来执行的块，也由此在这个程序中引入了异步机制。

**异步控制台**

并没有什么规范或一组需求指定 `console.*` 方法族如何工作——它们并不是 JavaScript 正式的一部分，而是由宿主环境添加到 JavaScript 中的。，在某些条件下，某些浏览器的 `console.log(..)` 并不会把传入的内容立即输出。出现这种情况的主要原因是，在许多程序（不只是 JavaScript）中， I/O 是非常低速的阻塞部分。所以，浏览器在后台异步处理控制台 I/O 能够提高性能，这时用户甚至可能根本意识不到其发生。

下面这种情景不是很常见，但也可能发生，从中（不是从代码本身而是从外部）可以观察到这种情况：

```js
var a = {
	index: 1
};
// 然后
console.log( a ); // ??
// 再然后
a.index++;
```

我们通常认为恰好在执行到 `console.log(..)` 语句的时候会看到 a 对象的快照，打印出类似于 `{ index: 1 }` 这样的内容，然后在下一条语句 a.index++ 执行时将其修改，这句的执行会严格在 a 的输出之后。

多数情况下，前述代码在开发者工具的控制台中输出的对象表示与期望是一致的。但是，这段代码运行的时候，浏览器可能会认为需要把控制台 I/O 延迟到后台，在这种情况下，等到浏览器控制台输出对象内容时， `a.index++` 可能已经执行，因此会显示 `{ index: 2 }`。

到底什么时候控制台 I/O 会延迟，甚至是否能够被观察到，这都是游移不定的。如果在调试的过程中遇到对象在 `console.log(..)` 语句之后被修改，可你却看到了意料之外的结果，要意识到这可能是这种 I/O 的异步化造成的。

## 1.2 事件循环

虽然能够编写异步 JavaScript 代码（就像前面我们看到的定时代码），但直到最近（ES6）， JavaScript 才真正内建有直接的异步概念。

JavaScript 引擎并不是独立运行的，它运行在宿主环境中，对多数开发者来说通常就是 Web 浏览器。所有的环境都有一个共同“点”（thread，也指线程），即它们都提供了一种机制来处理程序中多个块的执行，且执行每块时调用 JavaScript 引擎，这种机制被称为事件循环。

换句话说， JavaScript 引擎本身并没有时间的概念，只是一个按需执行 JavaScript 任意代码片段的环境。“事件”（JavaScript 代码执行）调度总是由包含它的环境进行。  

所以，举例来说，如果你的 JavaScript 程序发出一个 Ajax 请求，从服务器获取一些数据，那你就在一个函数（通常称为回调函数）中设置好响应代码，然后 JavaScript 引擎会通知宿主环境：“嘿，现在我要暂停执行，你一旦完成网络请求，拿到了数据，就请调用这个函数。”

然后浏览器就会设置侦听来自网络的响应，拿到要给你的数据之后，就会把回调函数插入到事件循环，以此实现对这个回调的调度执行。

先通过一段伪代码了解一下这个概念 :

```js
// eventLoop是一个用作队列的数组
//（先进，先出）
var eventLoop = [ ];
var event;
//“永远”执行
while (true) {
	// 一次tick
	if (eventLoop.length > 0) {
		// 拿到队列中的下一个事件
		event = eventLoop.shift();
		// 现在，执行下一个事件
		try {
			event();
		}
		catch (err) {
			reportError(err);
		}
	}
}
```

可以看到，有一个用 while 循环实现的持续运行的循环，循环的每一轮称为一个 tick。对每个 tick 而言，如果在队列中有等待事件，那么就会从队列中摘下一个事件并执行。这些事件就是你的回调函数。

一定要清楚， `setTimeout(..)` 并没有把你的回调函数挂在事件循环队列中。它所做的是设定一个定时器。当定时器到时后，环境会把你的回调函数放在事件循环中，这样，在未来某个时刻的 tick 会摘下并执行这个回调。

如果这时候事件循环中已经有 20 个项目了会怎样呢？你的回调就会等待。它得排在其他项目后面——通常没有抢占式的方式支持直接将其排到队首。这也解释了为什么`setTimeout(..)` 定时器的精度可能不高。大体说来，只能确保你的回调函数不会在指定的时间间隔之前运行，但可能会在那个时刻运行，也可能在那之后运行，要根据事件队列的状态而定。

所以换句话说就是，程序通常分成了很多小块，在事件循环队列中一个接一个地执行。严格地说，和你的程序不直接相关的其他事件也可能会插入到队列中。

## 1.3 并行线程

异步是关于现在和将来的时间间隙，而并行是关于能够同时发生的事情。  

并行计算最常见的工具就是进程和线程。进程和线程独立运行，并可能同时运行：在不同的处理器，甚至不同的计算机上，但多个线程能够共享单个进程的内存。  

与之相对的是，事件循环把自身的工作分成一个个任务并顺序执行，不允许对共享内存的并行访问和修改。通过分立线程中彼此合作的事件循环，并行和顺序执行可以共存。  

并行线程的交替执行和异步事件的交替调度，其粒度是完全不同的。

举例来说：

```js
function later() {
	answer = answer * 2;
	console.log( "Meaning of life:", answer );
}
```

尽管 `later()` 的所有内容被看作单独的一个事件循环队列表项，但如果考虑到这段代码是运行在一个线程中，实际上可能有很多个不同的底层运算。比如， `answer = answer * 2` 需要先加载 answer 的当前值，然后把 2 放到某处并执行乘法，取得结果之后保存回 answer 中。

在单线程环境中，线程队列中的这些项目是底层运算确实是无所谓的，因为线程本身不会被中断。但如果是在并行系统中，同一个程序中可能有两个不同的线程在运转，这时很可能就会得到不确定的结果。

考虑：

```js
var a = 20;

function foo() {
	a = a + 1;
}
function bar() {
	a = a * 2;
}

// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

根据 JavaScript 的单线程运行特性，如果 `foo()` 运行在 `bar()` 之前， a 的结果是 42，而如果`bar()` 运行在 `foo()` 之前的话， a 的结果就是 41。

如果共享同一数据的 JavaScript 事件并行执行的话，那么问题就变得更加微妙了。考虑`foo()` 和 `bar()` 中代码运行的线程分别执行的是以下两段伪代码任务，然后思考一下如果它们恰好同时运行的话会出现什么情况。

所以，多线程编程是非常复杂的。因为如果不通过特殊的步骤来防止这种中断和交错运行的话，可能会得到出乎意料的、不确定的行为，通常这很让人头疼。

JavaScript 从不跨线程共享数据，这意味着不需要考虑这一层次的不确定性。但是这并不意味着 JavaScript 总是确定性的。回忆一下前面提到的， `foo()` 和 `bar()` 的相对顺序改变可能会导致不同结果（41 或 42）。

**完整运行**

由于 JavaScript 的单线程特性， `foo()`（以及 `bar()`）中的代码具有原子性。也就是说，一旦 `foo()` 开始运行，它的所有代码都会在 `bar()` 中的任意代码运行之前完成，或者相反。这称为完整运行（run-to-completion）特性。  

实际上，如果 `foo()` 和 `bar()` 中的代码更长，完整运行的语义就会更加清晰，比如：

```js
var a = 1;
var b = 2;

function foo() {
	a++;
	b = b * a;
	a = b + 3;
}
function bar() {
	b--;
	a = 8 + b;
	b = a * 2;
}

// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

由于 `foo()` 不会被 `bar()` 中断， `bar()` 也不会被 `foo()` 中断，所以这个程序只有两个可能的输出，取决于这两个函数哪个先运行——如果存在多线程，且 `foo()` 和 `bar()` 中的语句可以交替运行的话，可能输出的数目将会增加不少！

同一段代码有两个可能输出意味着还是存在不确定性！但是，这种不确定性是在函数（事件）顺序级别上，而不是多线程情况下的语句顺序级别（或者说，表达式运算顺序级别）。换句话说，这一确定性要高于多线程情况。

在 JavaScript 的特性中，这种函数顺序的不确定性就是通常所说的竞态条件（race condition）， `foo()` 和 `bar()` 相互竞争，看谁先运行。具体来说，因为无法可靠预测 a 和 b 的最终结果，所以才是竞态条件。  

## 1.4 并发

现在让我们来设想一个展示状态更新列表（比如社交网络新闻种子）的网站，其随着用户向下滚动列表而逐渐加载更多内容。要正确地实现这一特性，需要（至少）两个独立的“进程”同时运行（也就是说，是在同一段时间内，并不需要在同一时刻）。

这里的“进程”之所以打上引号，是因为这并不是计算机科学意义上的真正操作系统级进程。这是虚拟进程，或者任务，表示一个逻辑上相关的运算序列。之所以使用“进程”而不是“任务”，是因为从概念上来讲，“进程”的定义更符合这里我们使用的意义。

第一个“进程”在用户向下滚动页面触发 onscroll 事件时响应这些事件（发起 Ajax 请求要求新的内容）。第二个“进程”接收 Ajax 响应（把内容展示到页面）。

显然，如果用户滚动页面足够快的话，在等待第一个响应返回并处理的时候可能会看到两个或更多 onscroll 事件被触发，因此将得到快速触发彼此交替的 onscroll 事件和 Ajax 响应事件。

两个或多个“进程”同时执行就出现了并发，不管组成它们的单个运算是否并行执行（在独立的处理器或处理器核心上同时运行）。可以把并发看作“进程”级（或者任务级）的并行，与运算级的并行（不同处理器上的线程）相对。

并发也引出了这些“进程”之间可能的彼此交互的概念。我们会在后面介绍。

在给定的时间窗口内（用户滚动页面的几秒钟内），我们看看把各个独立的“进程”表示为一系列事件 / 运算是什么样的：

```
“进程” 1（onscroll 事件）：

onscroll, 请求1
onscroll, 请求2
onscroll, 请求3
onscroll, 请求4
onscroll, 请求5
onscroll, 请求6
onscroll, 请求7

进程” 2（Ajax 响应事件）：

响应1
响应2
响应3
响应4
响应5
响应6
响应7
```

很可能某个 onscroll 事件和某个 Ajax 响应事件恰好同时可以处理。举例来说，假设这些事件的时间线是这样的：

```
onscroll, 请求1
onscroll, 请求2 响应1
onscroll, 请求3 响应2
响应3
onscroll, 请求4
onscroll, 请求5
onscroll, 请求6 响应4
onscroll, 请求7

响应6
响应5
响应7
```

但是，本章前面介绍过事件循环的概念， JavaScript 一次只能处理一个事件，所以要么是onscroll，请求 2 先发生，要么是响应 1 先发生，但是不会严格地同时发生。这就像学校食堂的孩子们，不管在门外多么拥挤，最终他们都得站成一队才能拿到自己的午饭！

下面列出了事件循环队列中所有这些交替的事件：

```
onscroll, 请求1 <--- 进程1启动
onscroll, 请求2
响应1 <--- 进程2启动
onscroll, 请求3
响应2
响应3
onscroll, 请求4
onscroll, 请求5
onscroll, 请求6
响应4
onscroll, 请求7 <--- 进程1结束
响应6
响应5
响应7 <--- 进程2结束
```

“进程” 1 和“进程” 2 并发运行（任务级并行），但是它们的各个事件是在事件循环队列中依次运行的。

另外，注意到响应 6 和响应 5 的返回是乱序的了吗？

单线程事件循环是并发的一种形式（当然还有其他形式，后面会介绍）。

#### 1.4.1 非交互

两个或多个“进程”在同一个程序内并发地交替运行它们的步骤 / 事件时，如果这些任务彼此不相关，就不一定需要交互。 如果进程间没有相互影响的话，不确定性是完全可以接受的。

举例来说：

```js
var res = {};

function foo(results) {
  res.foo = results;
}
function bar(results) {
  res.bar = results;
}

// ajax(..)是某个库提供的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

`foo()` 和 `bar()` 是两个并发执行的“进程”，按照什么顺序执行是不确定的。但是，我们构建程序的方式使得无论按哪种顺序执行都无所谓，因为它们是独立运行的，不会相互影响。

这并不是竞态条件 bug，因为不管顺序如何，代码总会正常工作。

#### 1.4.2 交互

更常见的情况是，并发的“进程”需要相互交流，通过作用域或 DOM 间接交互。正如前面介绍的，如果出现这样的交互，就需要对它们的交互进行协调以避免竞态的出现。

下面是一个简单的例子，两个并发的“进程”通过隐含的顺序相互影响，这个顺序有时会被破坏：

```js
var res = [];
function response(data) {
  res.push( data );
}
// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

这里的并发“进程”是这两个用来处理 Ajax 响应的 `response()` 调用。它们可能以任意顺序运行。

我们假定期望的行为是 `res[0]` 中放调用 `http://some.url.1` 的结果， `res[1]` 中放调用`http://some.url.2` 的结果。有时候可能是这样，但有时候却恰好相反，这要视哪个调用先完成而定。

这种不确定性很有可能就是一个竞态条件 bug。

所以，可以协调交互顺序来处理这样的竞态条件：

```js
var res = [];

function response(data) {
  if (data.url == "http://some.url.1") {
    res[0] = data;
  } else if (data.url == "http://some.url.2") {
    res[1] = data;
  }
}

// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

不管哪一个 Ajax 响应先返回，我们都要通过查看 `data.url`（当然，假定从服务器总会返回一个！）判断应该把响应数据放在 res 数组中的什么位置上。 `res[0]` 总是包含 `http://some.url.1` 的结果， `res[1]` 总是包含 `http://some.url.2` 的结果。通过简单的协调，就避免了竞态条件引起的不确定性。

从这个场景推出的方法也可以应用于多个并发函数调用通过共享 DOM 彼此之间交互的情况，比如一个函数调用更新某个` <div>` 的内容，另外一个更新这个` <div>` 的风格或属性（比如使这个 DOM 元素一有内容就显示出来）。可能你并不想在这个 DOM 元素在拿到内容之前显示出来，所以这种协调必须要保证正确的交互顺序。

有些并发场景如果不做协调，就总是（并非偶尔）会出错。考虑：

```js
var a, b;

function foo(x) {
  a = x * 2;
  baz();
}
function bar(y) {
  b = y * 2;
  baz();
}
function baz() {
  console.log(a + b);
}

// ajax(..)是某个库中的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

在这个例子中，无论 `foo()` 和 `bar()` 哪一个先被触发，总会使 `baz()` 过早运行（a 或者 b 仍处于未定义状态）；但对 `baz()` 的第二次调用就没有问题，因为这时候 a 和 b 都已经可用了。

要解决这个问题有多种方法。这里给出了一种简单方法：

```js
var a, b;
function foo(x) {
  a = x * 2;
  if (a && b) {
    baz();
  }
}
function bar(y) {
  b = y * 2;
  if (a && b) {
    baz();
  }
}
function baz() {
  console.log( a + b );
}
// ajax(..)是某个库中的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

包裹 `baz()` 调用的条件判断 `if (a && b)` 传统上称为门（gate），我们虽然不能确定 a 和 b到达的顺序，但是会等到它们两个都准备好再进一步打开门（调用 `baz()`）。

另一种可能遇到的并发交互条件有时称为竞态（race），但是更精确的叫法是门闩（latch）。它的特性可以描述为“只有第一名取胜”。在这里，不确定性是可以接受的，因为它明确指出了这一点是可以接受的：需要“竞争”到终点，且只有唯一的胜利者。

请思考下面这段有问题的代码：

```js
var a;

function foo(x) {
  a = x * 2;
  baz();
}
function bar(x) {
  a = x / 2;
  baz();
}
function baz() {
  console.log( a );
}

// ajax(..)是某个库中的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

不管哪一个（`foo()` 或 `bar()`）后被触发，都不仅会覆盖另外一个给 a 赋的值，也会重复调用 `baz()`（很可能并不是想要的结果）。

所以，可以通过一个简单的门闩协调这个交互过程，只让第一个通过：

```js
var a;

function foo(x) {
  if (!a) {
    a = x * 2;
    baz();
  }
}
function bar(x) {
  if (!a) {
    a = x / 2;
    baz();
  }
}
function baz() {
  console.log( a );
}

// ajax(..)是某个库中的某个Ajax函数
ajax( "http://some.url.1", foo );
ajax( "http://some.url.2", bar );
```

条件判断 `if (!a)` 使得只有 `foo()` 和 `bar()` 中的第一个可以通过，第二个（实际上是任何后续的）调用会被忽略。也就是说，第二名没有任何意义！

#### 1.4.3 协作

还有一种并发合作方式，称为并发协作（cooperative concurrency）。这里的重点不再是通过共享作用域中的值进行交互（尽管显然这也是允许的！）。这里的目标是取到一个长期运行的“进程”，并将其分割成多个步骤或多批任务，使得其他并发“进程”有机会将自己的运算插入到事件循环队列中交替运行。

举例来说，考虑一个需要遍历很长的结果列表进行值转换的 Ajax 响应处理函数。我们会使用` Array#map(..)` 让代码更简洁：

```js
var res = [];

// response(..)从Ajax调用中取得结果数组
function response(data) {
  // 添加到已有的res数组
  res = res.concat(
    // 创建一个新的变换数组把所有data值加倍
    data.map( function(val){
      return val * 2;
    } )
  );
}

// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

如果 `http://some.url.1` 首先取得结果，那么整个列表会立刻映射到 res 中。如果记录有几千条或更少，这不算什么。但是如果有像 1000 万条记录的话，就可能需要运行相当一段时间了（在高性能笔记本上需要几秒钟，在移动设备上需要更长时间，等等）。

这样的“进程”运行时，页面上的其他代码都不能运行，包括不能有其他的 `response(..)`调用或 UI 刷新，甚至是像滚动、输入、按钮点击这样的用户事件。这是相当痛苦的。

所以，要创建一个协作性更强更友好且不会霸占事件循环队列的并发系统，你可以异步地批处理这些结果。每次处理之后返回事件循环，让其他等待事件有机会运行。

这里给出一种非常简单的方法：

```js
var res = [];

// response(..)从Ajax调用中取得结果数组
function response(data) {
  // 一次处理1000个
  var chunk = data.splice( 0, 1000 );
  // 添加到已有的res组
  res = res.concat(
    // 创建一个新的数组把chunk中所有值加倍
    chunk.map( function(val){
    return val * 2;
    } )
  );
  // 还有剩下的需要处理吗？
  if (data.length > 0) {
    // 异步调度下一次批处理
    setTimeout( function(){
      response( data );
    }, 0 );
  }
}

// ajax(..)是某个库中提供的某个Ajax函数
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```

我们把数据集合放在最多包含 1000 条项目的块中。这样，我们就确保了“进程”运行时间会很短，即使这意味着需要更多的后续“进程”，因为事件循环队列的交替运行会提高站点 /App 的响应（性能）。

当然，我们并没有协调这些“进程”的顺序，所以结果的顺序是不可预测的。如果需要排序的话，就要使用和前面提到类似的交互技术，或者本书后面章节将要介绍的技术。

这里使用 `setTimeout(..0)`（hack）进行异步调度，基本上它的意思就是“把这个函数插入到当前事件循环队列的结尾处”。

> 严格说来， `setTimeout(..0)` 并不直接把项目插入到事件循环队列。定时器会在有机会的时候插入事件。举例来说，两个连续的 `setTimeout(..0)` 调用不能保证会严格按照调用顺序处理，所以各种情况都有可能出现，比如定时器漂移，在这种情况下，这些事件的顺序就不可预测。在 Node.js 中， 类似的方法是 `process.nextTick(..)`。尽管它们使用方便（通常性能也更高），但并没有（至少到目前为止）直接的方法可以适应所有环境来确保异步事件的顺序。下一小节我们会深入讨论这个话题异步：

## 1.5 任务

在 ES6 中，有一个新的概念建立在事件循环队列之上，叫作任务队列（job queue）。这个概念给大家带来的最大影响可能是 Promise 的异步特性（参见第 3 章）。

遗憾的是，目前为止，这是一个没有公开 API 的机制，因此要展示清楚有些困难。所以我们目前只从概念上进行描述，等到第 3 章讨论 Promise 的异步特性时，你就会理解这些动作是如何协调和处理的。

因此， 我认为对于任务队列最好的理解方式就是，它是挂在事件循环队列的每个 tick 之后的一个队列。在事件循环的每个 tick 中，可能出现的异步动作不会导致一个完整的新事件添加到事件循环队列中，而会在当前 tick 的任务队列末尾添加一个项目（一个任务）。这就像是在说： “哦，这里还有一件事将来要做，但要确保在其他任何事情发生之前就完成它。”

事件循环队列类似于一个游乐园游戏：玩过了一个游戏之后，你需要重新到队尾排队才能再玩一次。而任务队列类似于玩过了游戏之后，插队接着继续玩。

一个任务可能引起更多任务被添加到同一个队列末尾。所以，理论上说， 任务循环（job loop）可能无限循环（一个任务总是添加另一个任务，以此类推），进而导致程序的饿死，无法转移到下一个事件循环 tick。从概念上看，这和代码中的无限循环（就像`while(true)`..）的体验几乎是一样的。

任务和 `setTimeout(..0)` hack 的思路类似，但是其实现方式的定义更加良好，对顺序的保证性更强：尽可能早的将来。

设想一个调度任务（直接地，不要 hack）的 API，称其为 `schedule(..)`。考虑：

```js
console.log( "A" );
setTimeout( function(){
  console.log( "B" );
}, 0 );

// 理论上的"任务API"
schedule( function(){
  console.log( "C" );
  schedule( function(){
    console.log( "D" );
  } );
} );
```

可能你认为这里会打印出 A B C D，但实际打印的结果是 A C D B。因为任务处理是在当前事件循环 tick 结尾处，且定时器触发是为了调度下一个事件循环 tick（如果可用的话！）。在第 3 章中，我们将会看到， Promise 的异步特性是基于任务的，所以一定要清楚它和事件循环特性的关系。

## 1.6 语句顺序

代码中语句的顺序和 JavaScript 引擎执行语句的顺序并不一定要一致。这个陈述可能看起来似乎会很奇怪，所以我们要简单解释一下。

考虑：

```js
var a, b;
a = 10;
b = 30;
a = a + 1;
b = b + 1;
console.log( a + b ); // 42
```

这段代码中没有显式的异步（除了前面介绍过的很少见的异步 I/O ！），所以很可能它的执行过程是从上到下一行行进行的。

但是， JavaScript 引擎在编译这段代码之后可能会发现通过（安全地）重新安排这些语句的顺序有可能提高执行速度。重点是，只要这个重新排序是不可见的，一切都没问题。

比如，引擎可能会发现，其实这样执行会更快：

```js
var a, b;
a = 10;
a++;
b = 30;
b++;
console.log( a + b ); // 42
```

或者这样：

```js
var a, b;
a = 11;
b = 31;
console.log( a + b ); // 42
```

或者甚至这样：

```js
// 因为a和b不会被再次使用
// 我们可以inline，从而完全不需要它们！
console.log( 42 ); // 42
```

前面的所有情况中， JavaScript 引擎在编译期间执行的都是安全的优化，最后可见的结果都是一样的。

但是这里有一种场景，其中特定的优化是不安全的，因此也是不允许的（当然，不用说这其实也根本不能称为优化）：

```js
var a, b;
a = 10;
b = 30;

// 我们需要a和b处于递增之前的状态！
console.log( a * b ); // 300

a = a + 1;
b = b + 1;
console.log( a + b ); // 42
```

还有其他一些例子，其中编译器重新排序会产生可见的副作用（因此必须禁止），比如会产生副作用的函数调用（特别是 getter 函数），或 ES6 代理对象（参考本系列的《你不知道的 JavaScript（下卷）》的“ES6 & Beyond”部分）。

考虑：

```js
function foo() {
  console.log( b );
  return 1;
}
var a, b, c;
// ES5.1 getter字面量语法
c = {
  get bar() {
    console.log( a );
    return 1;
  }
};
a = 10;
b = 30;
a += foo(); // 30
b += c.bar; // 11
console.log( a + b ); // 42
```

如果不是因为代码片段中的语句 `console.log(..)`（只是作为一种方便的形式说明可见的副作用）， JavaScript 引擎如果愿意的话，本来可以自由地把代码重新排序如下：

```js
// ...
a = 10 + foo();
b = 30 + c.bar;
// ...
```

尽管 JavaScript 语义让我们不会见到编译器语句重排序可能导致的噩梦，这是一种幸运，但是代码编写的方式（从上到下的模式）和编译后执行的方式之间的联系非常脆弱，理解这一点也非常重要。

编译器语句重排序几乎就是并发和交互的微型隐喻。作为一个一般性的概念，清楚这一点能够使你更好地理解异步 JavaScript 代码流问题。

## 1.7 小结

实际上， JavaScript 程序总是至少分为两个块：第一块现在运行；下一块将来运行，以响应某个事件。尽管程序是一块一块执行的，但是所有这些块共享对程序作用域和状态的访问，所以对状态的修改都是在之前累积的修改之上进行的。

一旦有事件需要运行，事件循环就会运行，直到队列清空。事件循环的每一轮称为一个tick。用户交互、 IO 和定时器会向事件队列中加入事件。

任意时刻，一次只能从队列中处理一个事件。执行事件的时候，可能直接或间接地引发一个或多个后续事件。

并发是指两个或多个事件链随时间发展交替执行，以至于从更高的层次来看，就像是同时在运行（尽管在任意时刻只处理一个事件）。

通常需要对这些并发执行的“进程”（有别于操作系统中的进程概念）进行某种形式的交互协调，比如需要确保执行顺序或者需要防止竞态出现。这些“进程”也可以通过把自身分割为更小的块，以便其他“进程”插入进来。

## 第2章 回调	

第 1 章的所有例子都是把函数当作独立不可分割的运作单元来使用的。在函数内部，语句以可预测的顺序执行（在编译器以上的层级！），但是在函数顺序这一层级，事件（也就是异步函数调用）的运行顺序可以有多种可能。

在所有这些示例中，函数都是作为回调（callback）使用的，因为它是事件循环“回头调用”到程序中的目标，队列处理到这个项目的时候会运行它。

无数 JavaScript 程序，甚至包括一些最为高深和复杂的，所依赖的异步基础也仅限于回调（当然，它们使用了第 1 章介绍的各种并发交互模式）。回调函数是 JavaScript 的异步主力军，并且它们不辱使命地完成了自己的任务。

## 2.1 continuation

回调函数包裹或者说封装了程序的延续（continuation）。  

## 2.2 顺序的大脑

### 2.2.1 执行与计划

代码（通过回调）表达异步的方式并不能很好地映射到同步的大脑计划行为。

### 2.2.2 嵌套回调与链式回调

下面的代码常常被称为回调地狱（callback hell），有时也被称为毁灭金字塔（pyramid of doom，得名于嵌套缩进产生的横向三角形状）。  

```javascript
listen( "click", function handler(evt){
	setTimeout( function request(){
		ajax( "http://some.url.1", function response(text){
			if (text == "hello") {
				handler();
			}
			else if (text == "world") {
				request();
			}
		} );
	}, 500) ;
} );
```

我们的顺序阻塞式的大脑计划行为无法很好地映射到面向回调的异步代码。这就是回调方式最主要的缺陷：对于它们在代码中表达异步的方式，我们的大脑需要努力才能同步得上。

## 2.3 信任问题

有时候 `ajax(..)`（也就是你交付回调 continuation 的第三方）不是你编写的代码，也不在你的直接控制下。多数情况下，它是某个第三方提供的工具。 

我们把这称为控制反转（inversion of control）， 也就是把自己程序一部分的执行控制交给某个第三方。在你的代码和第三方工具（一组你希望有人维护的东西）之间有一份并没有明确表达的契约。回调最大的问题是控制反转，它会导致信任链的完全断裂。  

### 2.3.1 五个回调的故事

假设你是一名开发人员，为某个销售昂贵电视的网站建立商务结账系统。你已经做好了结账系统的各个界面。在最后一页，当用户点击“确定”就可以购买电视时，你需要调用（假设由某个分析追踪公司提供的）第三方函数以便跟踪这个交易。

你注意到，可能是为了提高性能，他们提供了一个看似用于异步追踪的工具，这意味着你需要传入一个回调函数。在传入的这个 continuation 中，你需要提供向客户收费和展示感谢页面的最终代码。

```js
analytics.trackPurchase( purchaseData, function(){
  chargeCreditCard();
  displayThankyouPage();
} );
```

到了办公室，你得知你们的一位高级客户购买了一台电视，信用卡却被刷了五次。通过分析日志，你得出一个结论：唯一的解释就是那个分析工具出于某种原因把你的回调调用了五次而不是一次。他们的文档中完全没有提到这种情况。

显然，分析公司的开发者开发了一些实验性的代码，在某种情况下，会在五秒钟内每秒重试一次传入的回调函数，然后才会因超时而失败。此你也只能无奈接受，并且你需要找到某种方法来保护结账代码，保证不再出问题。

```js
var tracked = false;
analytics.trackPurchase( purchaseData, function(){
	if (!tracked) {
		tracked = true;
		chargeCreditCard();
		displayThankyouPage();
	}
} );
```

考虑着他们调用你的回调时所有可能的出错情况。这里粗略列出了你能想到的分析工具可能出错的情况：

- 调用回调过早（在追踪之前）；
- 调用回调过晚（或没有调用）；
- 调用回调的次数太少或太多（就像你遇到过的问题！）；
- 没有把所需的环境 / 参数成功传给你的回调函数；
- 吞掉可能出现的错误或异常；
- ……

这感觉就像是一个麻烦列表，实际上它就是。你可能已经开始慢慢意识到，对于被传给你无法信任的工具的每个回调，你都将不得不创建大量的混乱逻辑。

### 2.3.2 不只是别人的代码

多数人都同意，至少在某种程度上我们应该在内部函数中构建一些防御性的输入参数检查，以便减少或阻止无法预料的问题。

过分信任输入：

```js
function addNumbers(x,y) {
  // +是可以重载的，通过类型转换，也可以是字符串连接
  // 所以根据传入参数的不同，这个运算并不是严格安全的
  return x + y;
}
addNumbers( 21, 21 ); // 42
addNumbers( 21, "21" ); // "2121"
```

针对不信任输入的防御性代码：

```js
function addNumbers(x,y) {
  // 确保输入为数字
  if (typeof x != "number" || typeof y != "number") {
    throw Error( "Bad parameters" );
  }
  // 如果到达这里，可以通过+安全的进行数字相加
  return x + y;
}
addNumbers( 21, 21 ); // 42
addNumbers( 21, "21" ); // Error: "Bad parameters"
```

依旧安全但更友好一些的：

```js
function addNumbers(x,y) {
  // 确保输入为数字
  x = Number( x );
  y = Number( y );
  // +安全进行数字相加
  return x + y;
}
addNumbers( 21, 21 ); // 42
addNumbers( 21, "21" ); // 42
```

回调最大的问题是控制反转，它会导致信任链的完全断裂。

## 2.4 省点回调

回调设计存在几个变体，意在解决前面讨论的一些信任问题（不是全部！）。这种试图从回调模式内部挽救它的意图是勇敢的，但却注定要失败。

为了更优雅地处理错误，有些 API 设计提供了分离回调（一个用于成功通知， 一个用于出错通知）  。

```js
function success(data) {
  console.log( data );
}
function failure(err) {
  console.error( err );
}
ajax( "http://some.url.1", success, failure );
```

在这种设计下， API 的出错处理函数 `failure()` 常常是可选的，如果没有提供的话，就是假定这个错误可以吞掉。

> ES6 Promise API 使用的就是这种分离回调设计。第 3 章会介绍 ES6 Promise 的更多细节。

还有一种常见的回调模式叫作“error-first 风格”（有时候也称为“Node 风格”，因为几乎所有 Node.js API 都采用这种风格），其中回调的第一个参数保留用作错误对象（如果有的话）。如果成功的话，这个参数就会被清空 / 置假（后续的参数就是成功数据）。不过，如果产生了错误结果，那么第一个参数就会被置起 / 置真（通常就不会再传递其他结果）。

```js
function response(err,data) {
  // 出错？
  if (err) {
    console.error( err );
  }
  // 否则认为成功
  else {
    console.log( data );
  }
}
ajax( "http://some.url.1", response );
```

在这两种情况下，都应该注意到以下几点。

首先，这并没有像表面看上去那样真正解决主要的信任问题。这并没有涉及阻止或过滤不想要的重复调用回调的问题。现在事情更糟了，因为现在你可能同时得到成功或者失败的结果，或者都没有，并且你还是不得不编码处理所有这些情况。

另外，不要忽略这个事实：尽管这是一种你可以采用的标准模式，但是它肯定更加冗长和模式化，可复用性不高，所以你还得不厌其烦地给应用中的每个回调添加这样的代码。

那么完全不调用这个信任问题又会怎样呢？ 可能需要设置一个超时来取消事件。可以构造一个工具（这里展示的只是一个“验证概念”版本）来帮助实现这一点。

```javascript
function timeoutify(fn, delay) {
	var intv = setTimeout( function(){
			intv = null;
			fn( new Error( "Timeout!" ) );
		}, delay );

	return function() {
		// 还没有超时？
		if (intv) {
			clearTimeout( intv );
			fn.apply( this, [ null ].concat( [].slice.call( arguments ) ) );
		}
	};
}
```

以下是使用方式：

```js
// 使用"error-first 风格" 回调设计
function foo(err,data) {
	if (err) {
		console.error( err );
	}
	else {
		console.log( data );
	}
}

ajax( "http://some.url.1", timeoutify( foo, 500 ) );
```

还有一个信任问题是调用过早。在特定应用的术语中，这可能实际上是指在某个关键任务完成之前调用回调。但是更通用地来说，对于既可能在现在（同步）也可能在将来（异步）调用你的回调的工具来说，这个问题是明显的。

这种由同步或异步行为引起的不确定性几乎总会带来极大的 bug 追踪难度。在某些圈子里，人们用虚构的十分疯狂的恶魔 Zalgo 来描述这种同步 / 异步噩梦。常常会有“不要放出 Zalgo”这样的呼喊，而这也引出了一条非常有效的建议：永远异步调用回调，即使就在事件循环的下一轮，这样，所有回调就都是可预测的异步调用了。

如果你不确定关注的 API 会不会永远异步执行怎么办呢？可以创建一个类似于这个“验证概念”版本的 `asyncify(..)` 工具。

```javascript
function asyncify(fn) {
	var orig_fn = fn,
		intv = setTimeout( function(){
			intv = null;
			if (fn) fn();
		}, 0 );

	fn = null;

	return function() {
		// 触发太快，在定时器intv触发指示异步转换发生之前？
		if (intv) {
			fn = orig_fn.bind.apply(
				orig_fn,
				// 把封装器的this添加到bind(..)调用的参数中，
				// 以及克里化（currying）所有传入参数
				[this].concat( [].slice.call( arguments ) )
			);
		}
		// 已经是异步
		else {
			// 调用原来的函数
			orig_fn.apply( this, arguments );
		}
	};
}
```

可以像这样使用 `asyncify(..)`：

```js
function result(data) {
	console.log( a );
}

var a = 0;

ajax( "..pre-cached-url..", asyncify( result ) );
a++;
```

不管这个 Ajax 请求已经在缓存中并试图对回调立即调用，还是要从网络上取得，进而在将来异步完成，这段代码总是会输出 1，而不是 0——result(..) 只能异步调用，这意味着 a++ 有机会在 result(..) 之前运行。

## 第3章 Promise	

在第 2 章里，我们确定了通过回调表达程序异步和管理并发的两个主要缺陷：缺乏顺序性和可信任性。

回忆一下，我们用回调函数来封装程序中的 continuation，然后把回调交给第三方（甚至可能是外部代码），接着期待其能够调用回调，实现正确的功能。

通过这种形式，我们要表达的意思是：“这是将来要做的事情，要在当前的步骤完成之后发生。”

但是，如果我们能够把控制反转再反转回来，会怎样呢？如果我们不把自己程序的continuation 传给第三方，而是希望第三方给我们提供了解其任务何时结束的能力，然后由我们自己的代码来决定下一步做什么，那将会怎样呢？

这种范式就称为 Promise 。

实际上，绝大多数 JavaScript/DOM 平台新增的异步 API 都是基于 Promise 构建的。

### 3.1 什么是Promise

通过 Promise，调用 `then(..)` 实际上可以接受两个函数，第一个用于完成情况，第二个用于拒绝情况。

```js
add( fetchX(), fetchY() )  
.then(      
	// 完成处理函数      
	function(sum) {          
		console.log( sum );      
	},      
	// 拒绝处理函数     
	function(err) {          
		console.error( err ); // 烦！      
	}  
); 
```

从外部看，由于 Promise 封装了依赖于时间的状态——等待底层值的完成或拒绝，所以 Promise 本身是与时间无关的。因此， Promise 可以按照可预测的方式组成（组合），而不用关心时序或底层的结果。  

另外，一旦 Promise 决议，它就永远保持在这个状态。此时它就成为了不变值（immutable value），可以根据需求多次查看。  

Promise 是一种封装和组合未来值的易于复用的机制。  

单独的 Promise 展示了未来值的特性。但是，也可以从另外一个角度看待 Promise 的决议：一种在异步任务中作为两个或更多步骤的流程控制机制，时序上的 this-then-that。  

在基于 Promise 的方法中，前面的代码片段会让 foo(..) 创建并返回一个 Promise 实例，而且这个 Promise 会被传递到 bar(..) 和 baz(..)。  

```javascript
function foo(x) {
	// start doing something that could take a while

	// construct and return a promise
	return new Promise( function(resolve,reject){
		// eventually, call `resolve(..)` or `reject(..)`,
		// which are the resolution callbacks for
		// the promise.
	} );
}

var p = foo( 42 );

bar( p );

baz( p );

```



bar(..) 和 baz(..) 的内部实现或许如下 

```javascript
function bar(fooPromise) {
	// listen for `foo(..)` to complete
	fooPromise.then(
		function(){
			// `foo(..)` has now finished, so
			// do `bar(..)`'s task
		},
		function(){
			// oops, something went wrong in `foo(..)`
		}
	);
}

// ditto for `baz(..)`
```



Promise 决议并不一定要像前面将 Promise 作为未来值查看时一样会涉及发送消息。它也可以只作为一种流程控制信号。另外一种实现方式是：  

```javascript
function bar() {
	// `foo(..)` has definitely finished, so
	// do `bar(..)`'s task
}

function oopsBar() {
	// oops, something went wrong in `foo(..)`,
	// so `bar(..)` didn't run
}

// ditto for `baz()` and `oopsBaz()`

var p = foo( 42 );

p.then( bar, oopsBar );

p.then( baz, oopsBaz );
```



这里没有把 promise p 传给 bar(..) 和 baz(..)，而是使用 promise 控制 bar(..) 和 baz(..) 何时执行，如果执行的话。最主要的区别在于错误处理部分。  

### 3.2 具有 then 方法的鸭子类型

不能通过 p instanceof Promise 来检查Promise值，因为Promise 值可能是从其他浏览器窗口（iframe 等）接收到的。识别 Promise（或者行为类似于 Promise 的东西）就是定义某种称为 thenable 的东西，将其定义为任何具有 then(..) 方法的对象和函数。我们认为，任何这样的值就是 Promise 一致的 thenable。  

Promise 的定义方式使得它只能被决议一次。如果出于某种原因， Promise 创建代码试图调用 resolve(..) 或 reject(..) 多次，或者试图两者都调用， 那么这个 Promise 将只会接受第一次决议，并默默地忽略任何后续调用。

Promise 至多只能有一个决议值（完成或拒绝）。 如果你没有用任何值显式决议，那么这个值就是 undefined，这是 JavaScript 常见的处理方式。但不管这个值是什么，无论当前或未来，它都会被传给所有注册的（且适当的完成或拒绝）回调。如果使用多个参数调用 resovle(..) 或者 reject(..)，第一个参数之 后的所有参数都会被默默忽略。如果要传递多个值，就必须要把它们封装在单个值中传递，比如通过一个数组或对象。  

如果拒绝一个 Promise 并给出一个理由（也就是一个出错消息），这个值就会被传给拒绝回调。如果在 Promise 的创建过程中或在查看其决议 结果过程中的任何时间点上出现了一个 JavaScript 异常错误，比如一个 TypeError 或 ReferenceError，那这个异常就会被捕捉，并且会使这个 Promise 被拒绝。  

如果向 Promise.resolve(..) 传递一个非 Promise、非 thenable 的立即值，就会得到一个用 这个值填充的 promise。

```javascript
var p1 = new Promise( function(resolve,reject){
	resolve( 42 );
} );

var p2 = Promise.resolve( 42 ); // p2等价于p1
```



而如果向 Promise.resolve(..) 传递一个真正的 Promise，就只会返回同一个 promise 。

```javascript
var p1 = Promise.resolve( 42 );

var p2 = Promise.resolve( p1 );

p1 === p2; // true
```



如果向 Promise.resolve(..) 传递了一个非 Promise 的 thenable 值，前者就会试图展开这个值，而且展开过程会持续到提取出一个具体的非类 Promise 的最终值。    

Promise.resolve(..) 可以接受任何 thenable，将其解封为它的非 thenable 值。从 Promise. resolve(..) 得到的是一个真正的 Promise，是一个可以信任的值。如果你传入的已经是真 正的 Promise，那么你得到的就是它本身，所以通过 Promise.resolve(..) 过滤来获得可信任性完全没有坏处。    

### 3.4  链式流

两个 Promise 固有行为特性： 

- 每次你对 Promise 调用 then(..)，它都会创建并返回一个新的 Promise，我们可以将其 链接起来； 
- 不管从 then(..) 调用的完成回调（第一个参数）返回的值是什么，它都会被自动设置 为被链接 Promise（第一点中的）的完成。    

```javascript
var p = Promise.resolve( 21 );

p
.then( function(v){
	console.log( v );	// 21

	// fulfill the chained promise with value `42`
	return v * 2;
} )
// here's the chained promise
.then( function(v){
	console.log( v );	// 42
} );
```



在这些例子中，一步步传递的值是可选的。如果不显式返回一个值，就会隐式返回 undefined，并且这些 promise 仍然会以同样的方式链接在一起。这样，每个 Promise 的决 议就成了继续下一个步骤的信号。我们构建的这个 Promise 链不仅是一个表达多步异步序列的流程控制，还是一个从一个步骤到下一个步骤传递消息的消息通道。    

如果Promise链中的某个步骤出错了，因为错误和异常是基于每个 Promise 的， 这意味着可能在链的任意位置捕捉到这样的错误，而这个捕捉动作在某种程度上就相当于在这一位置将整条链“重置”回了正常运作 。如果你调用 promise 的 then(..)，并且只传入一个完成处理函数，一个默认拒绝处理函数就会顶替上来。从本质上说，这使得错误可以继续沿着 Promise 链传播下去，直到遇到显式定义的拒绝处理函数。    

Promise(..) 构造器的第一个回调参数的恰当称谓是 resolve(..) ，它实际上的结果可能是完成或拒绝。第二个参数名称很容易决定，几乎所有的文献都将其命名为 reject(..)。

在then(..)的回调中，建议使用fulfilled(..) 和 rejected(..)，第一个参数表示除磷完成的情况，所以不需要使用标识两种状态的术语“resolve”。

### 3.5 错误处理

对多数开发者来说，错误处理最自然的形式就是同步的 try..catch 结构。遗憾的是，它只 能是同步的，无法用于异步代码模式。在回调中，一些模式化的错误处理方式已经出现，最值得一提的是 error-first 回调风格 。Promise 没有采用流行的 error-first 回调设计风格，而是使用了分离回调（split-callback）风格。一个回调用于完成情况，一个回调用于拒绝情况。

Promise 错误处理就是一个“绝望的陷阱”设计。默认情况下，它假定你想要 Promise 状态吞掉所有的错误。如果你忘了查看这个状态，这个错误就会默默地（通常是绝望地）在暗处凋零死掉。为了避免丢失被忽略和抛弃的 Promise 错误，一些开发者表示， Promise 链的一个最佳实践就是最后总以一个 catch(..) 结束。

### 3.6 Promise 模式

在经典的编程术语中，门（gate）是这样一种机制要等待两个或更多并行 / 并发的任务都 完成才能继续。它们的完成顺序并不重要，但是必须都要完成，门才能打开并让流程控制 继续。在 Promise API 中，这种模式被称为 all([ .. ])。    

Promise.all([ .. ]) 需要一个参数，是一个数组，通常由 Promise 实例组成。如果所有成员promise都完成，从 Promise. all([ .. ]) 调用返回的 promise 会收到一个完成消息。这是一个由所有传入 promise 的完成消息组成的数组，与指定的顺序一致，与完成顺序无关。    

Promise.race([ .. ]) 也接受单个数组参数。这个数组由一个或多个 Promise、 thenable 或 立即值组成。与 Promise.all([ .. ]) 类似，一旦有任何一个 Promise 决议为完成， Promise.race([ .. ]) 就会完成；一旦有任何一个 Promise 决议为拒绝，它就会拒绝。   

有些时候会需要在一列 Promise 中迭代，并对所有 Promise 都执行某个任务，非常类似于 对同步数组可以做的那样（比如 forEach(..)、 map(..)、 some(..) 和 every(..)）。如果要对每个 Promise 执行的任务本身是同步的，那这些工具就可以工作。例如异步的 map(..) 工具。它接收一个数组的值（可以是 Promise 或其他任何值），外加要在每个值上运行一个函数（任务）作为参数。 map(..) 本 身返回一个 promise，其完成值是一个数组，该数组（保持映射顺序）保存任务执行之后 的异步完成值 。

### 3.7 Promise API 概述

有启示性的构造器 Promise(..) 必须和 new 一起使用，并且必须提供一个函数回调。这个 回调是同步的或立即调用的。这个函数接受两个函数回调，用以支持 promise 的决议。通 常我们把这两个函数称为 resolve(..) 和 reject(..)  。

```javascript
var p = new Promise( function(resolve,reject){
	// `resolve(..)` to resolve/fulfill the promise
	// `reject(..)` to reject the promise
} );
```



reject(..) 就是拒绝这个 promise；但 resolve(..) 既可能完成 promise，也可能拒绝，要根据传入参数而定。如果传给 resolve(..) 的是一个非 Promise、非 thenable 的立即值，这 个 promise 就会用这个值完成。但是，如果传给 resolve(..) 的是一个真正的 Promise 或 thenable 值，这个值就会被递归展开，并且（要构造的） promise 将取用其最终决议值或状态。    

创建一个已被拒绝的 Promise 的快捷方式是使用 Promise.reject(..)，Promise.resolve(..) 常用于创建一个已完成的 Promise 。但是， Promise.resolve(..) 也会展开 thenable ，返回的 Promise 采用传入的这个 thenable 的最终决议值，可能是完成，也可能是拒绝。

每个 Promise 实例（不是 Promise API 命名空间）都有 then(..) 和 catch(..) 方法，通过这两个方法可以为这个 Promise 注册完成和拒绝处理函数。 Promise 决议之后，立即会调用 这两个处理函数之一，但不会两个都调用，而且总是异步调用。

then(..) 接受一个或两个参数：第一个用于完成回调，第二个用于拒绝回调。如果两者中 的任何一个被省略或者作为非函数值传入的话，就会替换为相应的默认回调。默认完成回 调只是把消息传递下去，而默认拒绝回调则只是重新抛出（传播）其接收到的出错原因。

catch(..) 只接受一个拒绝回调作为参数，并自动替换默认完成回调。换句话说，它等价于 then(null,..)。

then(..) 和 catch(..) 也会创建并返回一个新的 promise，这个 promise 可以用于实现Promise 链式流程控制。如果完成或拒绝回调中抛出异常，返回的 promise 是被拒绝的。如果任意一个回调返回非 Promise、非 thenable 的立即值，这个值会被用作返回 promise 的完成值。如果完成处理函数返回一个 promise 或 thenable，那么这个值会被展开，并作为返回 promise 的决议值。    

ES6 Promise API 静态辅助函数 Promise.all([ .. ]) 和 Promise.race([ .. ]) 都会创建一个 Promise 作为它们的返回值。这个 promise 的决议完全由传入的 promise 数组控制。 

对 Promise.all([ .. ]) 来说，只有传入的所有 promise 都完成，返回 promise 才能完成。 如果有任何 promise 被拒绝，返回的主 promise 就立即会被拒绝（抛弃任何其他 promise 的 结果）。如果完成的话，你会得到一个数组，其中包含传入的所有 promise 的完成值。对于 拒绝的情况，你只会得到第一个拒绝 promise 的拒绝理由值。这种模式传统上被称为门： 所有人都到齐了才开门。       

对 Promise.race([ .. ]) 来说，只有第一个决议的 promise（完成或拒绝）取胜，并且其 决议结果成为返回 promise 的决议。这种模式传统上称为门闩：第一个到达者打开门闩通 过。    

### 3.8 Promise 局限性

如果构建了一个没有错误处理函数的 Promise 链，链中任何地方的任何错误都会在链中一 直传播下去，直到被查看（通过在某个步骤注册拒绝处理函数）。

根据定义， Promise 只能有一个完成值或一个拒绝理由。一般的建议是构造一个值封装（比如一个对象或数组）来保持这样的多个信息。有时候你可以把这一点当作提示你可以 / 应该把问题分解为两个或更多 Promise 的信号。    

Promise 最本质的一个特征是： Promise 只能被决议一次（完成或拒绝）。如果不在 Promise 之上构建显著的抽象， Promise 肯定完全无法支持多值决议处理。

Promise 提供了一种不同的范式，因此，编码方式的改变程度从某处的个别差异到某种情 况下的截然不同都有可能。你需要刻意的改变，因为 Promise 不会从目前的编码方式中自 然而然地衍生出来。    

一旦创建了一个 Promise 并为其注册了完成和 / 或拒绝处理函数，如果出现某种情况使得这个任务悬而未决的话，你也没有办法从外部停止它的进程。单独的 Promise 不应该可取消，但是取消一个可序列是合理的，因为你不会像对待 Promise 那样把序列作为一个单独的不变值来传送。    

如果说 Promise 确实有一个真正的性能局限的话，那就是它们没有真正提供可信任性保护 支持的列表以供选择（你总是得到全部）。Promise 稍慢一些，但是作为交换，可得到的是大量内建的可信任性、对 Zalgo 的避免以及可组合性。    

# 第4章 生成器	

在第 2 章里，我们确定了用回调表达异步控制流程的两个关键缺陷：

- 基于回调的异步不符合大脑对任务步骤的规划方式；
- 由于控制反转，回调并不是可信任或可组合的。

在第 3 章里，我们详细介绍了 Promise 如何把回调的控制反转反转回来，恢复了可信任性 / 可组合性。

现在我们把注意力转移到一种顺序、看似同步的异步流程控制表达风格。使这种风格成为可能的“魔法”就是 ES6 生成器（generator）。

## 4.1 打破完整运行

在第 1 章中，我们解释了 JavaScript 开发者在代码中几乎普遍依赖的一个假定：一个函数一旦开始执行，就会运行到结束，期间不会有其他代码能够打断它并插入其间。

可能看起来似乎有点奇怪，不过 ES6 引入了一个新的函数类型，它并不符合这种运行到结束的特性。这类新的函数被称为生成器。

下面是实现这样的合作式并发的 ES6 代码：

```JS
var x = 1;
function * foo() {
  x++;
  yield; // 暂停！
  console.log("x:", x);
}
function bar() {
  x++;
}
```

> 生成器声明格式为`function* foo() { .. }`或 `function *foo() { .. }`都可以。唯一区别是 * 位置的风格不同。这两种形式在功能和语法上都是等同的，还有一种是 `function*foo(){ .. }`（没有空格）也一样。两种风格，各有优缺，但总体上我比较喜欢 `function *foo..` 的形式，因为这样在使用 `*foo()`来引用生成器的时候就会比较一致。如果只用 `foo()` 的形式，你就不会清楚知道我指的是生成器还是常规函数。这完全是一个风格偏好问题。

现在，我们要如何运行前面的代码片段，使得 bar() 在 `*foo()` 内部的 yield 处执行呢？

```JS
// 构造一个迭代器it来控制这个生成器
var it = foo();
// 这里启动foo()！
it.next();
x; // 2
bar();
x; // 3
it.next(); // x: 3
```

在解释 ES6 生成器的不同机制和语法之前，我们先来看看运行过程。

1. `it = foo()` 运算并没有执行生成器 `*foo()`，而只是构造了一个迭代器（iterator），这个迭代器会控制它的执行。
2. 第一个 `it.next()` 启动了生成器 `*foo()`，并运行了 `*foo()` 第一行的 x++。  
3. `*foo()` 在 yield 语句处暂停，在这一点上第一个 `it.next()` 调用结束。此时 `*foo()` 仍在运行并且是活跃的，但处于暂停状态。  
4. 我们查看 x 的值，此时为 2。  
5. 我们调用 bar()，它通过 x++ 再次递增 x。  
6. 我们再次查看 x 的值，此时为 3。  
7. 最后的 `it.next()` 调用从暂停处恢复了生成器 `*foo()` 的执行，并运行 `console.log(..)`语句，这条语句使用当前 x 的值 3。  

显然， `foo()` 启动了，但是没有完整运行，它在 yield 处暂停了。后面恢复了 `foo()` 并让它运行到结束，但这不是必需的。

因此，生成器就是一类特殊的函数，可以一次或多次启动和停止，并不一定非得要完成。尽管现在还不是特别清楚它的强大之处，但随着对本章后续内容的深入学习，我们会看到它将成为用于构建以生成器作为异步流程控制的代码模式的基础构件之一。

### 4.1.1 输入和输出

生成器函数是一个特殊的函数，具有前面我们展示的新的执行模式。但是，它仍然是一个函数，这意味着它仍然有一些基本的特性没有改变。比如，它仍然可以接受参数（即输入），也能够返回值（即输出）。

```JS
function * foo(x, y) {
  return x * y;
}
var it = foo(6, 7);
var res = it.next();
res.value; // 42
```

我们向` *foo(..)` 传入实参 6 和 7 分别作为参数 x 和 y。` *foo(..)` 向调用代码返回 42。

现在我们可以看到生成器和普通函数在调用上的一个区别。显然 `foo(6,7)` 看起来很熟悉。但难以理解的是，生成器` *foo(..)` 并没有像普通函数一样实际运行。

事实上，我们只是创建了一个迭代器对象，把它赋给了一个变量 it，用于控制生成器`*foo(..)`。然后调用 `it.next()`，指示生成器` *foo(..)` 从当前位置开始继续运行，停在下一个 yield 处或者直到生成器结束。

这个 `next(..)` 调用的结果是一个对象，它有一个 value 属性，持有从` *foo(..)` 返回的值（如果有的话）。换句话说， yield 会导致生成器在执行过程中发送出一个值，这有点类似于中间的 return。

1. 迭代消息传递

除了能够接受参数并提供返回值之外，生成器甚至提供了更强大更引人注目的内建消息输入输出能力，通过 yield 和 `next(..)` 实现。

考虑：
```JS
function * foo(x) {
  var y = x * (yield);
  return y;
}
var it = foo(6);
// 启动foo(..)
it.next();
var res = it.next(7);
res.value; // 42
```

在` *foo(..)` 内部，开始执行语句 `var y = x ..`，但随后就遇到了一个 yield 表达式。它就会在这一点上暂停`*foo(..)`（在赋值语句中间！），并在本质上要求调用代码为 yield表达式提供一个结果值。接下来，调用 `it.next(7)`，这一句把值 7 传回作为被暂停的 yield 表达式的结果。

所以，这时赋值语句实际上就是 `var y = 6 * 7`。现在， return y 返回值 42 作为调用`it.next(7)` 的结果。

注意，这里有一点非常重要，但即使对于有经验的 JavaScript 开发者也很有迷惑性：根据你的视角不同， yield 和` next(..)` 调用有一个不匹配。一般来说，需要的` next(..)` 调用要比 yield 语句多一个，前面的代码片段有一个 yield 和两个` next(..)` 调用。

为什么会有这个不匹配？

因为第一个` next(..)` 总是启动一个生成器，并运行到第一个 yield 处。不过，是第二个`next(..)` 调用完成第一个被暂停的 yield 表达式，第三个` next(..)` 调用完成第二个 yield，以此类推。

2. 两个问题的故事

实际上，你首先考虑的是哪一部分代码将会影响这个不匹配是否被察觉到。

只考虑生成器代码：

```js
var y = x * (yield);
return y;
```

第一个 yield 基本上是提出了一个问题：“这里我应该插入什么值？”

谁来回答这个问题呢？第一个 `next()` 已经运行，使得生成器启动并运行到此处，所以显然它无法回答这个问题。因此必须由第二个 `next(..)` 调用回答第一个 yield 提出的这个问题。

看到不匹配了吗——第二个对第一个？

把视角转化一下：不从生成器的视角看这个问题，而是从迭代器的角度。

为了恰当阐述这个视角，我们还需要解释一下：消息是双向传递的——yield.. 作为一个表达式可以发出消息响应 `next(..)` 调用， `next(..)` 也可以向暂停的 yield 表达式发送值。考虑下面这段稍稍调整过的代码：

```js
function * foo(x) {
  var y = x * (yield "Hello"); // <-- yield一个值！
  return y;
}
var it = foo(6);
var res = it.next(); // 第一个next()，并不传入任何东西
res.value; // "Hello"
res = it.next(7); // 向等待的yield传入7
res.value; // 42
```

yield .. 和 `next(..)` 这一对组合起来， 在生成器的执行过程中构成了一个双向消息传递系统。

> 我们并没有向第一个 `next()` 调用发送值，这是有意为之。只有暂停的 yield 才能接受这样一个通过 `next(..)` 传递的值，而在生成器的起始处我们调用第一个 `next()` 时，还没有暂停的 yield 来接受这样一个值。规范和所有兼容浏览器都会默默丢弃传递给第一个 `next()` 的任何东西。传值过去仍然不是一个好思路，因为你创建了沉默的无效代码，这会让人迷惑。因此，启动生成器时一定要用不带参数的 `next()`。

第一个 `next()` 调用（没有参数的）基本上就是在提出一个问题：“生成器` *foo(..)` 要给我的下一个值是什么”。谁来回答这个问题呢？第一个 yield "hello" 表达式。

看见了吗？这里没有不匹配。

根据你认为提出问题的是谁， yield 和 `next(..)` 调用之间要么有不匹配，要么没有。

但是，稍等！与 yield 语句的数量相比，还是多出了一个额外的 next()。所以，最后一个it.next(7) 调用再次提出了这样的问题：生成器将要产生的下一个值是什么。但是，再没有 yield 语句来回答这个问题了，是不是？那么谁来回答呢？

return 语句回答这个问题！

如果你的生成器中没有 return 的话——在生成器中和在普通函数中一样， return 当然不是必需的——总有一个假定的 / 隐式的 return;（也就是 return undefined;），它会在默认情况下回答最后的 it.next(7) 调用提出的问题。

这样的提问和回答是非常强大的：通过 yield 和 `next(..)` 建立的双向消息传递。

### 4.1.2 多个迭代器

从语法使用的方面来看，通过一个迭代器控制生成器的时候，似乎是在控制声明的生成器
函数本身。但有一个细微之处很容易忽略：每次构建一个迭代器，实际上就隐式构建了生
成器的一个实例，通过这个迭代器来控制的是这个生成器实例。

同一个生成器的多个实例可以同时运行，它们甚至可以彼此交互：

```js
function * foo() {
  var x = yield 2;
  z++;
  var y = yield(x * z);
  console.log(x, y, z);
}
var z = 1;

var it1 = foo();
var it2 = foo();

var val1 = it1.next().value; // 2 <-- yield 2
var val2 = it2.next().value; // 2 <-- yield 2

val1 = it1.next(val2 * 10).value; // 40 <-- x:20, z:2
val2 = it2.next(val1 * 5).value; // 600 <-- x:200, z:3

it1.next(val2 / 2); // y:300
// 20 300 3

it2.next(val1 / 4); // y:10
// 200 10 3
```

> 同一个生成器的多个实例并发运行的最常用处并不是这样的交互，而是生成器在没有输入的情况下，可能从某个独立连接的资源产生自己的值。下一节中我们会详细介绍值产生。

我们简单梳理一下执行流程。

1. `*foo()` 的两个实例同时启动，两个 `next()` 分别从 `yield 2` 语句得到值 2。  
2. `val2 * 10` 也就是 `2 * 10`，发送到第一个生成器实例 it1，因此 x 得到值 20。 z 从 1 增加到 2，然后 `20 * 2` 通过 yield 发出，将 val1 设置为 40。  
3. `val1 * 5` 也就是 `40 * 5`，发送到第二个生成器实例 it2，因此 x 得到值 200。 z 再次从 2 递增到 3，然后 `200 * 3` 通过 yield 发出，将 val2 设置为 600。  
4. `val2 / 2` 也就是 `600 / 2`，发送到第一个生成器实例 it1，因此 y 得到值 300，然后打印出 x y z 的值分别是 20 300 3。  
5. `val1 / 4` 也就是 `40 / 4`，发送到第二个生成器实例 it2，因此 y 得到值 10，然后打印出x y z 的值分别为 200 10 3。  

**交替执行**

回想一下 1.3 节中关于完整运行的这个场景：

```js
var a = 1;
var b = 2;

function foo() {
  a++;
  b = b * a;
  a = b + 3;
}

function bar() {
  b--;
  a = 8 + b;
  b = a * 2;
}
```

如果是普通的 JavaScript 函数的话，显然，要么是 `foo()` 首先运行完毕，要么是 `bar()` 首
先运行完毕，但 `foo()` 和 `bar()` 的语句不能交替执行。所以，前面的程序只有两种可能的
输出。

但是，使用生成器的话，交替执行（甚至在语句当中！）显然是可能的：

```js
var a = 1;
var b = 2;

function * foo() {
  a++;
  yield;
  b = b * a;
  a = (yield b) + 3;
}

function * bar() {
  b--;
  yield;
  a = (yield 8) + b;
  b = a * (yield 2);
}
```

根据迭代器控制的 `*foo()` 和 `*bar()` 调用的相对顺序不同，前面的程序可能会产生多种不
同的结果。换句话说，通过两个生成器在共享的相同变量上的迭代交替执行，我们实际上
可以（以某种模拟的方式）印证第 1 章讨论的理论上的多线程竞态条件环境。

首先，来构建一个名为 `step(..)` 的辅助函数，用于控制迭代器：

```js
function step(gen) {
  var it = gen();
  var last;
  return function () {
    // 不管yield出来的是什么，下一次都把它原样传回去！
    last = it.next(last).value;
  };
}
```

`step(..)` 初始化了一个生成器来创建迭代器 it，然后返回一个函数，这个函数被调用的时
候会将迭代器向前迭代一步。另外，前面的 yield 发出的值会在下一步发送回去。于是，
yield 8 就是 8，而 yield b 就是 b（yield 发出时的值）。

现在，只是为了好玩，我们来试验一下交替运行 `*foo()` 和 `*bar()` 代码块的效果。我们从
乏味的基本情况开始，确保 `*foo()` 在 `*bar()` 之前完全结束（和第 1 章中做的一样）：

```js
// 确保重新设置a和b
a = 1;
b = 2;
var s1 = step(foo);
var s2 = step(bar);
// 首次运行*foo()
s1();
s1();
s1();
// 现在运行*bar()
s2();
s2();
s2();
s2();
console.log(a, b); // 11 22
```

最后的结果是 11 和 22，和第 1 章中的版本一样。现在交替执行顺序，看看 a 和 b 的值是
如何改变的：

```js
// 确保重新设置a和b
a = 1;
b = 2;
var s1 = step(foo);
var s2 = step(bar);
s2(); // b--;
s2(); // yield 8
s1(); // a++;
s2(); // a = 8 + b;
// yield 2
s1(); // b = b * a;
// yield b
s1(); // a = b + 3;
s2(); // b = a * 2;
```

在告诉你结果之前，你能推断出前面的程序运行后 a 和 b 的值吗？不要作弊！

```js
console.log( a, b ); // 12 18
```

> 作为留给大家的练习，请试着重新安排 s1() 和 s2() 的调用顺序，看看还能
够得到多少种结果组合。不要忘了，你总是需要 3 次 s1() 调用和 4 次 s2()
调用。回忆一下前面关于 next() 和 yield 匹配的讨论，想想为什么。

当然，你基本不可能故意创建让人迷惑到这种程度的交替运行实际代码，因为这给理解代
码带来了极大的难度。但这个练习很有趣，对于理解多个生成器如何在共享的作用域上并
发运行也有指导意义，因为这个功能有很多用武之地。

## 4.2 生成器产生值 

在前面一节中，我们提到生成器的一种有趣用法是作为一种产生值的方式。这并不是本章
的重点，但是如果不介绍一些基础的话，就会缺乏完整性了，特别是因为这正是“生成
器”这个名称最初的使用场景。

下面要偏一下题，先介绍一点迭代器，不过我们还会回来介绍它们与生成器的关系以及如
何使用生成器来生成值。

### 4.2.1　生产者与迭代器

假定你要产生一系列值，其中每个值都与前面一个有特定的关系。要实现这一点，需要一
个有状态的生产者能够记住其生成的最后一个值。

可以实现一个直接使用函数闭包的版本，类似如下：

```js
var gimmeSomething = (function () {
  var nextVal;
  return function () {
    if (nextVal === undefined) {
      nextVal = 1;
    } else {
      nextVal = (3 * nextVal) + 6;
    }
    return nextVal;
  };
})();
gimmeSomething(); // 1
gimmeSomething(); // 9
gimmeSomething(); // 33
gimmeSomething(); // 105
```

> 这里 nextVal 的计算逻辑已经简化了，但是从概念上说，我们希望直到下一
次 `gimmeSomething()` 调用发生时才计算下一个值（即 nextVal）。否则，一
般来说，对更持久化或比起简单数字资源更受限的生产者来说，这可能就是
资源泄漏的设计。

生成任意数字序列并不是一个很实际的例子。但如果是想要从数据源生成记录呢？可以采
用基本相同的代码。

实际上，这个任务是一个非常通用的设计模式，通常通过迭代器来解决。 迭代器是一个定
义良好的接口，用于从一个生产者一步步得到一系列值。 JavaScript 迭代器的接口，与多
数语言类似，就是每次想要从生产者得到下一个值的时候调用 `next()`。

可以为我们的数字序列生成器实现标准的迭代器接口：

```js
var something = (function () {
  var nextVal;
  return {
    // for..of循环需要
    [Symbol.iterator]: function () {
        return this;
      },
      // 标准迭代器接口方法
      next: function () {
        if (nextVal === undefined) {
          nextVal = 1;
        } else {
          nextVal = (3 * nextVal) + 6;
        }
        return {
          done: false,
          value: nextVal
        };
      }
  };
})();
something.next().value; // 1
something.next().value; // 9
something.next().value; // 33
something.next().value; // 105
```

> 我们将在 4.2.2 节解释为什么在这段代码中需要 `[Symbol.iterator]: ..` 这
一部分。从语法上说，这涉及了两个 ES6 特性。首先， [ .. ] 语法被称为
计算属性名。这在对象术语定义中是指，指定一个表达式并用这个表
达式的结果作为属性的名称。另外， Symbol.iterator 是 ES6 预定义的特殊
Symbol 值之一。

`next()` 调用返回一个对象。这个对象有两个属性： done 是一个 boolean 值，标识迭代器的
完成状态； value 中放置迭代值。

ES6 还新增了一个 for..of 循环，这意味着可以通过原生循环语法自动迭代标准迭代器：

```js
for (var v of something) {
  console.log(v);
  // 不要死循环！
  if (v > 500) {
    break;
  }
}
// 1 9 33 105 321 969
```

> 因为我们的迭代器 something 总是返回 done:false，因此这个 for..of 循环
将永远运行下去，这也就是为什么我们要在里面放一个 break 条件。迭代器
永不结束是完全没问题的，但是也有一些情况下， 迭代器会在有限的值集合
上运行，并最终返回 done:true。

for..of 循环在每次迭代中自动调用 next()，它不会向 next() 传入任何值，并且会在接收
到 done:true 之后自动停止。这对于在一组数据上循环很方便。

当然，也可以手工在迭代器上循环，调用 next() 并检查 done:true 条件来确定何时停止循
环：

```js
for (var ret;
  (ret = something.next()) && !ret.done;
) {
  console.log(ret.value);
  // 不要死循环！
  if (ret.value > 500) {
    break;
  }
}
// 1 9 33 105 321 969
```

这种手工 for 方法当然要比 ES6 的 for..of 循环语法丑陋，但其优点是，这
样就可以在需要时向 next() 传递值。

除了构造自己的迭代器，许多 JavaScript 的内建数据结构（从 ES6 开始），比如 array，也
有默认的迭代器：

```js
var a = [1,3,5,7,9];
for (var v of a) {
console.log( v );
}
// 1 3 5 7 9
```

for..of 循环向 a 请求它的迭代器，并自动使用这个迭代器迭代遍历 a 的值。
这里可能看起来像是 ES6 一个奇怪的缺失，不过一般的 object 是故意不
像 array 一样有默认的迭代器。这里我们并不会深入探讨其中的缘由。如
果你只是想要迭代一个对象的所有属性的话（不需要保证特定的顺序），可
以通过 Object.keys(..) 返回一个 array，类似于 for (var k of Object.
keys(obj)) { .. 这样使用。这样在一个对象的键值上使用 for..of 循环与
for..in 循环类似，除了 Object.keys(..) 并不包含来自于 [[Prototype]] 链
上的属性，而 for..in 则包含（参见本系列的《你不知道的 JavaScript（上
卷）》的“this 和对象原型”部分）。

### 4.2.2 iterable

前面例子中的 something 对象叫作迭代器，因为它的接口中有一个 next() 方法。而与其紧
密相关的一个术语是 iterable（可迭代），即指一个包含可以在其值上迭代的迭代器的对象。
从 ES6 开始，从一个 iterable 中提取迭代器的方法是： iterable 必须支持一个函数，其名称
是专门的 ES6 符号值 Symbol.iterator。调用这个函数时，它会返回一个迭代器。通常每
次调用会返回一个全新的迭代器，虽然这一点并不是必须的。

前面代码片段中的 a 就是一个 iterable。 for..of 循环自动调用它的 Symbol.iterator 函数来
构建一个迭代器。我们当然也可以手工调用这个函数，然后使用它返回的迭代器：

```js
var a = [1,3,5,7,9];
var it = a[Symbol.iterator]();
it.next().value; // 1
it.next().value; // 3
it.next().value; // 5
..
```

前面的代码中列出了定义的 something，你可能已经注意到了这一行：

```js
[Symbol.iterator]: function(){ return this; }
```

这段有点令人疑惑的代码是在将 something 的值（迭代器 something 的接口）也构建成为一
个 iterable。现在它既是 iterable， 也是迭代器。然后我们把 something 传给 for..of 循环：生成器 ｜ 247

```js
for (var v of something) {
..
}
```

for..of 循环期望 something 是 iterable，于是它寻找并调用它的 Symbol.iterator 函数。
我们将这个函数定义为就是简单的 return this，也就是把自身返回，而 for..of 循环并
不知情。

### 4.2.3　生成器迭代器

了解了迭代器的背景，让我们把注意力转回生成器上。可以把生成器看作一个值的生产
者，我们通过迭代器接口的 next() 调用一次提取出一个值。

所以，严格说来，生成器本身并不是 iterable，尽管非常类似——当你执行一个生成器，就
得到了一个迭代器：

```js
function *foo(){ .. }
var it = foo();
```

可以通过生成器实现前面的这个 something 无限数字序列生产者，类似这样：

```js
function *something() {
var nextVal;
while (true) {
if (nextVal === undefined) {
nextVal = 1;
}
else {
nextVal = (3 * nextVal) + 6;
}
yield nextVal;
}
}
```

通常在实际的 JavaScript 程序中使用 while..true 循环是非常糟糕的主意，至
少如果其中没有 break 或 return 的话是这样，因为它有可能会同步地无限循
环，并阻塞和锁住浏览器 UI。但是，如果在生成器中有 yield 的话，使用这
样的循环就完全没有问题。因为生成器会在每次迭代中暂停，通过 yield 返
回到主程序或事件循环队列中。简单地说就是：“生成器把 while..true 带回
了 JavaScript 编程的世界！”

这样就简单明确多了，是不是？因为生成器会在每个 yield 处暂停，函数 *something() 的
状态（作用域）会被保持，即意味着不需要闭包在调用之间保持变量状态。

这段代码不仅更简洁，我们不需要构造自己的迭代器接口，实际上也更合理，因为它更清
晰地表达了意图。比如， while..true 循环告诉我们这个生成器就是要永远运行：只要我
们一直索要，它就会一直生成值。

现在，可以通过 for..of 循环使用我们雕琢过的新的 *something() 生成器。你可以看到，
其工作方式基本是相同的：

```js
for (var v of something()) {
console.log( v );
// 不要死循环！
if (v > 500) {
break;
}
}
// 1 9 33 105 321 969
```

但是，不要忽略了这段 for (var v of something()) .. ！我们并不是像前面的例子那样把
something 当作一个值来引用，而是调用了 *something() 生成器以得到它的迭代器供 for..
of 循环使用。

如果认真思考的话，你也许会从这段生成器与循环的交互中提出两个问题。

- 为什么不能用 for (var v of something) .. ？因为这里的 something 是生成器，并不是
iterable。我们需要调用 something() 来构造一个生产者供 for..of 循环迭代。
- something() 调用产生一个迭代器，但 for..of 循环需要的是一个 iterable，对吧？是
的。生成器的迭代器也有一个 Symbol.iterator 函数，基本上这个函数做的就是 return
this，和我们前面定义的 iterable something 一样。换句话说，生成器的迭代器也是一个
iterable ！

停止生成器

在前面的例子中，看起来似乎 *something() 生成器的迭代器实例在循环中的 break 调用之
后就永远留在了挂起状态。

其实有一个隐藏的特性会帮助你管理此事。 for..of 循环的“异常结束”（也就是“提前终
止”），通常由 break、 return 或者未捕获异常引起，会向生成器的迭代器发送一个信号使
其终止。

严格地说，在循环正常结束之后， for..of 循环也会向迭代器发送这个信号。
对于生成器来说，这本质上是没有意义的操作，因为生成器的迭代器需要先
完成 for..of 循环才能结束。但是，自定义的迭代器可能会需要从 for..of
循环的消费者那里接收这个额外的信号。

尽管 for..of 循环会自动发送这个信号，但你可能会希望向一个迭代器手工发送这个信号。
可以通过调用 return(..) 实现这一点。

如果在生成器内有 try..finally 语句，它将总是运行，即使生成器已经外部结束。如果需
要清理资源的话（数据库连接等），这一点非常有用：

```js
function *something() {
try {
var nextVal;
while (true) {
if (nextVal === undefined) {
nextVal = 1;
}
else {
nextVal = (3 * nextVal) + 6;
}
yield nextVal;
}
}
// 清理子句
finally {
console.log( "cleaning up!" );
}
}
```
之前的例子中， for..of 循环内的 break 会触发 finally 语句。但是，也可以在外部通过
return(..) 手工终止生成器的迭代器实例：

```js
var it = something();
for (var v of it) {
console.log( v );
// 不要死循环！
if (v > 500) {
console.log(
// 完成生成器的迭代器
it.return( "Hello World" ).value
);
// 这里不需要break
}
}
// 1 9 33 105 321 969
// 清理！
// Hello World
```

调用 it.return(..) 之后，它会立即终止生成器，这当然会运行 finally 语句。另外，它
还会把返回的 value 设置为传入 return(..) 的内容，这也就是 "Hello World" 被传出
去的过程。现在我们也不需要包含 break 语句了，因为生成器的迭代器已经被设置为
done:true，所以 for..of 循环会在下一个迭代终止。

生成器的名字大多来自这种消费生产值（consuming produced values）的用例。但是，这里
要再次申明，这只是生成器的用法之一，坦白地说，甚至不是这本书重点关注的用途。
既然对生成器的工作机制有了更完整的理解，那接下来就可以把关注转向如何把生成器应
用于异步并发了。

## 4.3 异步迭代生成器

生成器与异步编码模式及解决回调问题等，有什么关系呢？让我们来回答这个重要的
问题。

我们应该重新讨论第 3 章中的一个场景。回想一下回调方法：

```js
function foo(x,y,cb) {
ajax(
"http://some.url.1/?x=" + x + "&y=" + y,
cb
);
}
foo( 11, 31, function(err,text) {
if (err) {
console.error( err );
}
else {
console.log( text );
}
} );
```

如果想要通过生成器来表达同样的任务流程控制，可以这样实现：

```js
function foo(x,y) {
ajax(
"http://some.url.1/?x=" + x + "&y=" + y,
function(err,data){
if (err) {
// 向*main()抛出一个错误
it.throw( err );
}
else {
// 用收到的data恢复*main()
it.next( data );
}
}
);
}
function *main() {
try {
var text = yield foo( 11, 31 );生成器 ｜ 251
console.log( text );
}
catch (err) {
console.error( err );
}
}
var it = main();
// 这里启动！
it.next();
```

第一眼看上去，与之前的回调代码对比起来，这段代码更长一些，可能也更复杂一些。
但是，不要被表面现象欺骗了！生成器代码实际上要好得多！不过要解释这一点还是比
较复杂的。

首先，让我们查看一下最重要的这段代码：

```js
var text = yield foo( 11, 31 );
console.log( text );
```

请先花点时间思考一下这段代码是如何工作的。我们调用了一个普通函数 foo(..)，而且
显然能够从 Ajax 调用中得到 text，即使它是异步的。

这怎么可能呢？如果你回想一下第 1 章的开始部分的话，我们给出了几乎相同的代码：

```js
var data = ajax( "..url 1.." );
console.log( data );
```

但是，这段代码不能工作！你能指出其中的区别吗？区别就在于生成器中使用的 yield。
这就是奥秘所在！正是这一点使得我们看似阻塞同步的代码，实际上并不会阻塞整个程
序，它只是暂停或阻塞了生成器本身的代码。

在 yield foo(11,31) 中，首先调用 foo(11,31)，它没有返回值（即返回 undefined），所以
我们发出了一个调用来请求数据，但实际上之后做的是 yield undefined。这没问题，因
为这段代码当前并不依赖 yield 出来的值来做任何事情。本章后面会再次讨论这一点。
这里并不是在消息传递的意义上使用 yield，而只是将其用于流程控制实现暂停 / 阻塞。实
际上，它还是会有消息传递，但只是生成器恢复运行之后的单向消息传递。

所以，生成器在 yield 处暂停，本质上是在提出一个问题：“我应该返回什么值来赋给变量
text ？”谁来回答这个问题呢？

看一下 foo(..)。如果这个 Ajax 请求成功，我们调用：

```js
it.next( data );
```

这会用响应数据恢复生成器，意味着我们暂停的 yield 表达式直接接收到了这个值。然后
随着生成器代码继续运行，这个值被赋给局部变量 text。

很酷吧？
回头往前看一步，思考一下这意味着什么。我们在生成器内部有了看似完全同步的代码
（除了 yield 关键字本身），但隐藏在背后的是，在 foo(..) 内的运行可以完全异步。
这是巨大的改进！对于我们前面陈述的回调无法以顺序同步的、符合我们大脑思考模式的
方式表达异步这个问题，这是一个近乎完美的解决方案。

从本质上而言，我们把异步作为实现细节抽象了出去，使得我们可以以同步顺序的形式追
踪流程控制：“发出一个 Ajax 请求，等它完成之后打印出响应结果。”并且，当然，我们
只在这个流程控制中表达了两个步骤，而这种表达能力是可以无限扩展的，以便我们无论
需要多少步骤都可以表达。

这是一个很重要的领悟，回过头去把上面三段重读一遍，让它融入你的思
想吧！

同步错误处理

前面的生成器代码甚至还给我们带来了更多其他的好处。让我们把注意力转移到生成器内
部的 try..catch：

```js
try {
var text = yield foo( 11, 31 );
console.log( text );
}
catch (err) {
console.error( err );
}
```

这是如何工作的呢？调用 foo(..) 是异步完成的，难道 try..catch 不是无法捕获异步错
误，就像我们在第 3 章中看到的一样吗？

我们已经看到 yield 是如何让赋值语句暂停来等待 foo(..) 完成，使得响应完成后可以被
赋给 text。精彩的部分在于 yield 暂停也使得生成器能够捕获错误。通过这段前面列出的
代码把错误抛出到生成器中：

```js
if (err) {
// 向*main()抛出一个错误生成器 ｜ 253
it.throw( err );
}
```

生成器 yield 暂停的特性意味着我们不仅能够从异步函数调用得到看似同步的返回值，还
可以同步捕获来自这些异步函数调用的错误！

所以我们已经知道，我们可以把错误抛入生成器中，不过如果是从生成器向外抛出错误
呢？正如你所料 :

```js
function *main() {
var x = yield "Hello World";
yield x.toLowerCase(); // 引发一个异常！
}
var it = main();
it.next().value; // Hello World
try {
it.next( 42 );
}
catch (err) {
console.error( err ); // TypeError
}
```

当然，也可以通过 throw .. 手工抛出一个错误，而不是通过触发异常。

甚至可以捕获通过 throw(..) 抛入生成器的同一个错误，基本上也就是给生成器一个处理
它的机会；如果没有处理的话，迭代器代码就必须处理：

```js
function *main() {
var x = yield "Hello World";
// 永远不会到达这里
console.log( x );
}
var it = main();
it.next();
try {
// *main()会处理这个错误吗？看看吧！
it.throw( "Oops" );
}
catch (err) {
// 不行，没有处理！
console.error( err ); // Oops
}
```

在异步代码中实现看似同步的错误处理（通过 try..catch）在可读性和合理性方面都是一
个巨大的进步。

## 4.4 生成器 +Promise
在前面的讨论中，我们展示了如何异步迭代生成器，这是一团乱麻似的回调在顺序性和合
理性方面的巨大进步。但我们错失了很重要的两点： Promise 的可信任性和可组合性（参
见第 3 章）！

别担心，我们还会重获这些。 ES6 中最完美的世界就是生成器（看似同步的异步代码）和
Promise（可信任可组合）的结合。

但如何实现呢？
回想一下第 3 章里在运行 Ajax 例子中基于 Promise 的实现方法：

```js
function foo(x,y) {
return request(
"http://some.url.1/?x=" + x + "&y=" + y
);
}
foo( 11, 31 )
.then(
function(text){
console.log( text );
},
function(err){
console.error( err );
}
);
```

在前面的运行 Ajax 例子的生成器代码中， foo(..) 没有返回值（undefined），并且我们的
迭代器控制代码并不关心 yield 出来的值。

而这里支持 Promise 的 foo(..) 在发出 Ajax 调用之后返回了一个 promise。这暗示我们可
以通过 foo(..) 构造一个 promise，然后通过生成器把它 yield 出来，然后迭代器控制代码
就可以接收到这个 promise 了。

但迭代器应该对这个 promise 做些什么呢？
它应该侦听这个 promise 的决议（完成或拒绝），然后要么使用完成消息恢复生成器运行，
要么向生成器抛出一个带有拒绝原因的错误。

我再重复一遍，因为这一点非常重要。获得 Promise 和生成器最大效用的最自然的方法就
是 yield 出来一个 Promise，然后通过这个 Promise 来控制生成器的迭代器。生成器 ｜ 255

让我们来试一下！首先，把支持 Promise 的 foo(..) 和生成器 *main() 放在一起：

```js
function foo(x,y) {
return request(
"http://some.url.1/?x=" + x + "&y=" + y
);
}
function *main() {
try {
var text = yield foo( 11, 31 );
console.log( text );
}
catch (err) {
console.error( err );
}
}
```

这次重构代码中最有力的发现是， *main() 之中的代码完全不需要改变！在生成器内部，
不管什么值 yield 出来，都只是一个透明的实现细节，所以我们甚至没有意识到其发生，
也不需要关心。

但现在如何运行 *main() 呢？还有一些实现细节需要补充，来实现接收和连接 yield 出来
的 promise，使它能够在决议之后恢复生成器。先从手工实现开始：

```js
var it = main();
var p = it.next().value;
// 等待promise p决议
p.then(
function(text){
it.next( text );
},
function(err){
it.throw( err );
}
);
```

实际上，这并没有那么令人痛苦，对吧？

这段代码看起来应该和我们前面手工组合通过 error-first 回调控制的生成器非常类似。除了
没有 if (err) { it.throw..， promise 已经为我们分离了完成（成功）和拒绝（失败），否
则的话，迭代器控制是完全一样的。

现在，我们已经隐藏了一些重要的细节。

最重要的是，我们利用了已知 *main() 中只有一个需要支持 Promise 的步骤这一事实。如
果想要能够实现 Promise 驱动的生成器，不管其内部有多少个步骤呢？我们当然不希望每256 ｜ 第 4 章
个生成器手工编写不同的 Promise 链！如果有一种方法可以实现重复（即循环）迭代控制，
每次会生成一个 Promise，等其决议后再继续，那该多好啊。

还有，如果在 it.next(..) 调用过程中生成器（有意或无意）抛出一个错误会怎样呢？是
应该退出呢，还是应该捕获这个错误并发送回去呢？类似地，如果通过 it.throw(..) 把一
个 Promise 拒绝抛入生成器中，但它却没有受到处理就被直接抛回了呢？

### 4.4.1　支持 Promise 的 Generator Runner

随着对这条道路的深入探索，你越来越会意识到：“哇，如果有某个工具为我实现这些就
好了。”关于这一点，你绝对没错。这是如此重要的一个模式，你绝对不希望搞错（或精
疲力竭地一次又一次重复实现），所以最好是使用专门设计用来以我们前面展示的方式运
行 Promise-yielding 生成器的工具。

有几个 Promise 抽象库提供了这样的工具，包括我的 asynquence 库及其 runner(..)，本部
分的附录 A 中会介绍。

但是，为了学习和展示的目的，我们还是自己定义一个独立工具，叫作 run(..)：

```js
// 在此感谢Benjamin Gruenbaum（@benjamingr on GitHub）的巨大改进！
function run(gen) {
var args = [].slice.call( arguments, 1), it;
// 在当前上下文中初始化生成器
it = gen.apply( this, args );
// 返回一个promise用于生成器完成
return Promise.resolve()
.then( function handleNext(value){
// 对下一个yield出的值运行
var next = it.next( value );
return (function handleResult(next){
// 生成器运行完毕了吗？
if (next.done) {
return next.value;
}
// 否则继续运行
else {
return Promise.resolve( next.value )
.then(
// 成功就恢复异步循环，把决议的值发回生成器
handleNext,
// 如果value是被拒绝的 promise，
// 就把错误传回生成器进行出错处理
function handleErr(err) {
return Promise.resolve(
it.throw( err )生成器 ｜ 257
)
.then( handleResult );
}
);
}
})(next);
} );
}
```

诚如所见，你可能并不愿意编写这么复杂的工具，并且也会特别不希望为每个使用的生成
器都重复这段代码。所以，一个工具或库中的辅助函数绝对是必要的。尽管如此，我还是
建议你花费几分钟时间学习这段代码，以更好地理解生成器 +Promise 协同运作模式。
如何在运行 Ajax 的例子中使用 run(..) 和 *main() 呢？

```js
function *main() {
// ..
}
run( main );
```

就是这样！这种运行 run(..) 的方式，它会自动异步运行你传给它的生成器，直到结束。
我们定义的 run(..) 返回一个 promise，一旦生成器完成，这个 promise 就
会决议，或收到一个生成器没有处理的未捕获异常。这里并没有展示这种功
能，但我们会在本章后面部分再介绍这一点。

ES7： async 与 await?
前面的模式——生成器 yield 出 Promise，然后其控制生成器的迭代器来执行它，直到结
束——是非常强大有用的一种方法。如果我们能够无需库工具辅助函数（即 run(..)）就
能够实现就好了。

关于这一点，可能有一些好消息。在编写本书的时候，对于后 ES6、 ES7 的时间框架，在
这一方面增加语法支持的提案已经有了一些初期但很强势的支持。显然，现在确定细节还
太早，但其形式很可能会类似如下：

```js
function foo(x,y) {
return request(
"http://some.url.1/?x=" + x + "&y=" + y
);
}
async function main() {
try {
var text = await foo( 11, 31 );
console.log( text );
}258 ｜ 第 4 章
catch (err) {
console.error( err );
}
}
main();
```

可以看到，这里没有通过 run(..) 调用（意味着不需要库工具！）来触发和驱动 main()，
它只是被当作一个普通函数调用。另外， main() 也不再被声明为生成器函数了，它现在是
一类新的函数： async 函数。最后，我们不再 yield 出 Promise，而是用 await 等待它决议。
如果你 await 了一个 Promise， async 函数就会自动获知要做什么，它会暂停这个函数（就
像生成器一样），直到 Promise 决议。 我们并没有在这段代码中展示这一点，但是调用一个
像 main() 这样的 async 函数会自动返回一个 promise。在函数完全结束之后，这个 promise
会决议。

有 C# 经验的人可能很熟悉 async/await 语法，因为它们基本上是相同的。
从本质上说，这个提案就是把前面我们已经推导出来的模式写进规范，使其进入语法机
制：组合 Promise 和看似同步的流程控制代码。这是两个最好的世界的结合，有效地实际
解决了我们列出的回调方案的主要问题。

这样的 ES7 提案已经存在，并有了初期的支持和热情，仅仅是这个事实就极大增加了这个
异步模式对其未来重要性的信心。

### 4.4.2　生成器中的 Promise 并发

到目前为止，我们已经展示的都是 Promise+ 生成器下的单步异步流程。但是，现实世界中
的代码常常会有多个异步步骤。

如果不认真对待的话，生成器的这种看似同步的风格可能会让你陷入对自己异步并发组
织方式的自满中，进而导致并不理想的性能模式。所以我们打算花点时间来研究一下各
种方案。

想象这样一个场景：你需要从两个不同的来源获取数据，然后把响应组合在一起以形成第
三个请求，最终把最后一条响应打印出来。第 3 章已经用 Promise 研究过一个类似的场景，
但是让我们在生成器的环境下重新考虑一下这个问题吧。

你的第一直觉可能类似如下：生成器 ｜ 259

```js
function *foo() {
var r1 = yield request( "http://some.url.1" );
var r2 = yield request( "http://some.url.2" );
var r3 = yield request(
"http://some.url.3/?v=" + r1 + "," + r2
);
console.log( r3 );
}
// 使用前面定义的工具run(..)
run( foo );
```

这段代码可以工作，但是针对我们特定的场景而言，它并不是最优的。你能指出原因吗？
因为请求 r1 和 r2 能够——出于性能考虑也应该——并发执行，但是在这段代码中，
它 们 是 依 次 执 行 的； 直 到 请 求 URL"http://some.url.1" 完 成 后 才 会 通 过 Ajax 获 取
URL"http://some.url.2"。这两个请求是相互独立的，所以性能更高的方案应该是让它们
同时运行。

但是，到底如何通过生成器和 yield 实现这一点呢？我们知道 yield 只是代码中一个单独
的暂停点，并不可能同时在两个点上暂停。

最自然有效的答案就是让异步流程基于 Promise，特别是基于它们以时间无关的方式管理
状态的能力（参见 3.1.1 节）。

最简单的方法：
```js
function *foo() {
// 让两个请求"并行"
var p1 = request( "http://some.url.1" );
var p2 = request( "http://some.url.2" );
// 等待两个promise都决议
var r1 = yield p1;
var r2 = yield p2;
var r3 = yield request(
"http://some.url.3/?v=" + r1 + "," + r2
);
console.log( r3 );
}
// 使用前面定义的工具run(..)
run( foo );
```
为什么这和前面的代码片段不同呢？观察一下 yield 的位置。 p1 和 p2 是并发执行（即260 ｜ 第 4 章
“并行”）的用于 Ajax 请求的 promise。哪一个先完成都无所谓，因为 promise 会按照需要
在决议状态保持任意长时间。

然后我们使用接下来的两个 yield 语句等待并取得 promise 的决议（分别写入 r1 和 r2）。
如果 p1 先决议，那么 yield p1 就会先恢复执行，然后等待 yield p2 恢复。如果 p2 先决
议，它就会耐心保持其决议值等待请求，但是 yield p1 将会先等待，直到 p1 决议。
不管哪种情况， p1 和 p2 都会并发执行，无论完成顺序如何，两者都要全部完成，然后才
会发出 r3 = yield request..Ajax 请求。

这种流程控制模型如果听起来有点熟悉的话，是因为这基本上和我们在第 3 章中通过
Promise.all([ .. ]) 工具实现的 gate 模式相同。因此，也可以这样表达这种流程控制：

```js
function *foo() {
// 让两个请求"并行"，并等待两个promise都决议
var results = yield Promise.all( [
request( "http://some.url.1" ),
request( "http://some.url.2" )
] );
var r1 = results[0];
var r2 = results[1];
var r3 = yield request(
"http://some.url.3/?v=" + r1 + "," + r2
);
console.log( r3 );
}
// 使用前面定义的工具run(..)
run( foo );
```

就像我们在第 3 章中讨论过的，我们甚至可以通过 ES6 解构赋值，把 var
r1 = .. var r2 = .. 赋值语句简化为 var [r1,r2] = results。

换句话说， Promise 所有的并发能力在生成器 +Promise 方法中都可以使用。所以无论在
什么地方你的需求超过了顺序的 this-then-that 异步流程控制， Promise 很可能都是最好的
选择。

隐藏的 Promise
作为一个风格方面的提醒：要注意你的生成器内部包含了多少 Promise 逻辑。我们介绍的
使用生成器实现异步的方法的全部要点在于创建简单、顺序、看似同步的代码，将异步的
细节尽可能隐藏起来。生成器 ｜ 261

比如，这可能是一个更简洁的方案：

```js
// 注：普通函数，不是生成器
function bar(url1,url2) {
return Promise.all( [
request( url1 ),
request( url2 )
] );
}
function *foo() {
// 隐藏bar(..)内部基于Promise的并发细节
var results = yield bar(
"http://some.url.1",
"http://some.url.2"
);
var r1 = results[0];
var r2 = results[1];
var r3 = yield request(
"http://some.url.3/?v=" + r1 + "," + r2
);
console.log( r3 );
}
// 使用前面定义的工具run(..)
run( foo );
```

在 *foo() 内部，我们所做的一切就是要求 bar(..) 给我们一些 results，并通过 yield
来等待结果，这样更简洁也更清晰。我们不需要关心在底层是用 Promise.all([ .. ])
Promise 组合来实现这一切。

我们把异步，实际上是 Promise，作为一个实现细节看待。
如果想要实现一系列高级流程控制的话，那么非常有用的做法是：把你的 Promise 逻辑隐
藏在一个只从生成器代码中调用的函数内部。比如：

```js
function bar() {
Promise.all( [
baz( .. )
.then( .. ),
Promise.race( [ .. ] )
] )
.then( .. )
}
```

有时候会需要这种逻辑，而如果把它直接放在生成器内部的话，那你就失去了几乎所有一
开始使用生成器的理由。应该有意将这样的细节从生成器代码中抽象出来，以避免它把高
层次的任务表达变得杂乱。262 ｜ 第 4 章

创建代码除了要实现功能和保持性能之外，你还应该尽可能使代码易于理解和维护。
对编程来说，抽象并不总是好事，很多时候它会增加复杂度以换取简洁性。
但是在这个例子里，我相信，对生成器 +Promise 异步代码来说，相比于其他
实现，这种抽象更加健康。尽管如此，还是建议大家要注意具体情况具体分
析，为你和你的团队作出正确的决定。

## 4.5 生成器委托

在前面一节中，我们展示了从生成器内部调用常规函数，以及这如何对于把实现细节（就
像异步 Promise 流）抽象出去还是一种有用的技术。但是，用普通函数实现这个任务的主
要缺点是它必须遵守普通函数的规则，也就意味着它不能像生成器一样用 yield 暂停自己。
可能出现的情况是，你可能会从一个生成器调用另一个生成器，使用辅助函数 run(..)，就
像这样：

```js
function *foo() {
var r2 = yield request( "http://some.url.2" );
var r3 = yield request( "http://some.url.3/?v=" + r2 );
return r3;
}
function *bar() {
var r1 = yield request( "http://some.url.1" );
// 通过 run(..) "委托"给*foo()
var r3 = yield run( foo );
console.log( r3 );
}
run( bar );
```

我们再次通过 run(..) 工具从 *bar() 内部运行 *foo()。这里我们利用了如下事实：我们前
面定义的 run(..) 返回一个 promise，这个 promise 在生成器运行结束时（或出错退出时）
决议。因此，如果从一个 run(..) 调用中 yield 出来一个 promise 到另一个 run(..) 实例
中，它会自动暂停 *bar()，直到 *foo() 结束。

但其实还有一个更好的方法可以实现从 *bar() 调用 *foo()，称为 yield 委托。 yield 委托
的具体语法是： yield * __（注意多出来的 *）。在我们弄清它在前面的例子中的使用之前，
先来看一个简单点的场景：

```js
function *foo() {
console.log( "*foo() starting" );生成器 ｜ 263
yield 3;
yield 4;
console.log( "*foo() finished" );
}
function *bar() {
yield 1;
yield 2;
yield *foo(); // yield委托！
yield 5;
}
var it = bar();
it.next().value; // 1
it.next().value; // 2
it.next().value; // *foo()启动
// 3
it.next().value; // 4
it.next().value; // *foo()完成
// 5
```

在本章前面的一条提示中，我解释了为什么我更喜欢 function *foo() ..，
而不是 function* foo() ..。类似地，我也更喜欢——与这个主题的多数其
他文档不同——使用 yield *foo() 而不是 yield* foo()。 * 的位置仅关乎风
格，由你自己来决定使用哪种。不过我发现保持风格一致是很吸引人的。
这里的 yield *foo() 委托是如何工作的呢？

首先，和我们以前看到的完全一样，调用 foo() 创建一个迭代器。然后 yield * 把迭代器
实例控制（当前 *bar() 生成器的）委托给 / 转移到了这另一个 *foo() 迭代器。

所以，前面两个 it.next() 调用控制的是 *bar()。但当我们发出第三个 it.next() 调用时，
*foo() 现在启动了，我们现在控制的是 *foo() 而不是 *bar()。这也是为什么这被称为委
托： *bar() 把自己的迭代控制委托给了 *foo()。

一旦 it 迭代器控制消耗了整个 *foo() 迭代器， it 就会自动转回控制 *bar()。
现在回到前面使用三个顺序 Ajax 请求的例子：

```js
function *foo() {
var r2 = yield request( "http://some.url.2" );
var r3 = yield request( "http://some.url.3/?v=" + r2 );
return r3;
}
function *bar() {
var r1 = yield request( "http://some.url.1" );264 ｜ 第 4 章
// 通过 yeild* "委托"给*foo()
var r3 = yield *foo();
console.log( r3 );
}
run( bar );
```

这段代码和前面版本的唯一区别就在于使用了 yield *foo()， 而不是前面的 yield run(foo)。
yield * 暂停了迭代控制，而不是生成器控制。当你调用 *foo() 生成器
时，现在 yield 委托到了它的迭代器。但实际上，你可以 yield 委托到任意
iterable， yield *[1,2,3] 会消耗数组值 [1,2,3] 的默认迭代器。

### 4.5.1　为什么用委托

yield 委托的主要目的是代码组织，以达到与普通函数调用的对称。

想像一下有两个模块分别提供了方法 foo() 和 bar()，其中 bar() 调用了 foo()。一般来
说，把两者分开实现的原因是该程序的适当的代码组织要求它们位于不同的函数中。比
如，可能有些情况下是单独调用 foo()，另外一些地方则由 bar() 调用 foo()。
同样是出于这些原因，保持生成器分离有助于程序的可读性、可维护性和可调试性。在这
一方面， yield * 是一个语法上的缩写，用于代替手工在 *foo() 的步骤上迭代，不过是在
*bar() 内部。

如果 *foo() 内的步骤是异步的话，这样的手工方法将会特别复杂，这也是你可能需要使用
run(..) 工具来做某些事情的原因。就像我们已经展示的， yield *foo() 消除了对 run(..)
工具的需要（就像 run(foo)）。

### 4.5.2　消息委托

你可能会疑惑，这个 yield 委托是如何不只用于迭代器控制工作，也用于双向消息传递工
作的呢。认真跟踪下面的通过 yield 委托实现的消息流出入：

```js
function *foo() {
console.log( "inside *foo():", yield "B" );
console.log( "inside *foo():", yield "C" );
return "D";
}
function *bar() {生成器 ｜ 265
console.log( "inside *bar():", yield "A" );
// yield委托！
console.log( "inside *bar():", yield *foo() );
console.log( "inside *bar():", yield "E" );
return "F";
}
var it = bar();
console.log( "outside:", it.next().value );
// outside: A
console.log( "outside:", it.next( 1 ).value );
// inside *bar(): 1
// outside: B
console.log( "outside:", it.next( 2 ).value );
// inside *foo(): 2
// outside: C
console.log( "outside:", it.next( 3 ).value );
// inside *foo(): 3
// inside *bar(): D
// outside: E
console.log( "outside:", it.next( 4 ).value );
// inside *bar(): 4
// outside: F
```

要特别注意 it.next(3) 调用之后的执行步骤。
(1) 值 3（通过 *bar() 内部的 yield 委托）传入等待的 *foo() 内部的 yield "C" 表达式。
(2) 然后 *foo() 调用 return "D"，但是这个值并没有一直返回到外部的 it.next(3) 调用。
(3) 取而代之的是，值 "D" 作为 *bar() 内部等待的 yield*foo() 表达式的结果发出——这个
yield 委托本质上在所有的 *foo() 完成之前是暂停的。所以 "D" 成为 *bar() 内部的最
后结果，并被打印出来。
(4) yield "E" 在 *bar() 内部调用，值 "E" 作为 it.next(3) 调用的结果被 yield 发出。
从外层的迭代器（it）角度来说，是控制最开始的生成器还是控制委托的那个，没有任何
区别。

实际上， yield 委托甚至并不要求必须转到另一个生成器，它可以转到一个非生成器的一
般 iterable。比如：

```js
function *bar() {
console.log( "inside *bar():", yield "A" );266 ｜ 第 4 章
// yield委托给非生成器！
console.log( "inside *bar():", yield *[ "B", "C", "D" ] );
console.log( "inside *bar():", yield "E" );
return "F";
}
var it = bar();
console.log( "outside:", it.next().value );
// outside: A
console.log( "outside:", it.next( 1 ).value );
// inside *bar(): 1
// outside: B
console.log( "outside:", it.next( 2 ).value );
// outside: C
console.log( "outside:", it.next( 3 ).value );
// outside: D
console.log( "outside:", it.next( 4 ).value );
// inside *bar(): undefined
// outside: E
console.log( "outside:", it.next( 5 ).value );
// inside *bar(): 5
// outside: F
```

注意这个例子和之前那个例子在消息接收位置和报告位置上的区别。

最显著的是，默认的数组迭代器并不关心通过 next(..) 调用发送的任何消息，所以值 2、
3 和 4 根本就被忽略了。还有，因为迭代器没有显式的返回值（和前面使用的 *foo() 不
同），所以 yield * 表达式完成后得到的是一个 undefined。

异常也被委托！

和 yield 委托透明地双向传递消息的方式一样，错误和异常也是双向传递的：

```js
function *foo() {
try {
yield "B";
}
catch (err) {
console.log( "error caught inside *foo():", err );
}
yield "C";
throw "D";
}生成器 ｜ 267
function *bar() {
yield "A";
try {
yield *foo();
}
catch (err) {
console.log( "error caught inside *bar():", err );
}
yield "E";
yield *baz();
// 注：不会到达这里！
yield "G";
}
function *baz() {
throw "F";
}
var it = bar();
console.log( "outside:", it.next().value );
// outside: A
console.log( "outside:", it.next( 1 ).value );
// outside: B
console.log( "outside:", it.throw( 2 ).value );
// error caught inside *foo(): 2
// outside: C
console.log( "outside:", it.next( 3 ).value );
// error caught inside *bar(): D
// outside: E
try {
console.log( "outside:", it.next( 4 ).value );
}
catch (err) {
console.log( "error caught outside:", err );
}
// error caught outside: F
```

这段代码中需要注意以下几点。
(1) 调用 it.throw(2) 时，它会发送错误消息 2 到 *bar()，它又将其委托给 *foo()，后者捕
获并处理它。然后， yield "C" 把 "C" 发送回去作为 it.throw(2) 调用返回的 value。
(2) 接下来从 *foo() 内 throw 出来的值 "D" 传播到 *bar()，这个函数捕获并处理它。然后
yield "E" 把 "E" 发送回去作为 it.next(3) 调用返回的 value。268 ｜ 第 4 章
(3) 然后，从 *baz() throw 出来的异常并没有在 *bar() 内被捕获——所以 *baz() 和 *bar()
都被设置为完成状态。这段代码之后，就再也无法通过任何后续的 next(..) 调用得到
值 "G"， next(..) 调用只会给 value 返回 undefined。

### 4.5.3　异步委托

我们终于回到前面的多个顺序 Ajax 请求的 yield 委托例子：

```js
function *foo() {
var r2 = yield request( "http://some.url.2" );
var r3 = yield request( "http://some.url.3/?v=" + r2 );
return r3;
}
function *bar() {
var r1 = yield request( "http://some.url.1" );
var r3 = yield *foo();
console.log( r3 );
}
run( bar );
```

这里我们在 *bar() 内部没有调用 yield run(foo)，而是调用 yield *foo()。

在这个例子之前的版本中，使用了 Promise 机制（通过 run(..) 控制）把值从 *foo() 内的
return r3 传递给 *bar() 中的局部变量 r3。现在，这个值通过 yield * 机制直接返回。
除此之外的行为非常相似。

### 4.5.4　递归委托

当然， yield 委托可以跟踪任意多委托步骤，只要你把它们连在一起。甚至可以使用 yield
委托实现异步的生成器递归，即一个 yield 委托到它自身的生成器：

```js
function *foo(val) {
if (val > 1) {
// 生成器递归
val = yield *foo( val - 1 );
}
return yield request( "http://some.url/?v=" + val );
}
function *bar() {
var r1 = yield *foo( 3 );
console.log( r1 );生成器 ｜ 269
}
run( bar );
```

run(..) 工具可以通过 run( foo, 3 ) 调用，因为它支持额外的参数和生成
器一起传入。但是，这里使用了没有参数的 *bar()，以展示 yield * 的灵
活性。

这段代码后面的处理步骤是怎样的呢？坚持一下，接下来的细节描述可能会非常复杂。
(1) run(bar) 启动生成器 *bar()。
(2) foo(3) 创建了一个 *foo(..) 的迭代器，并传入 3 作为其参数 val。
(3) 因为 3 > 1，所以 foo(2) 创建了另一个迭代器，并传入 2 作为其参数 val。
(4) 因为 2 > 1，所以 foo(1) 又创建了一个新的迭代器，并传入 1 作为其参数 val。
(5) 因为 1 > 1 不成立，所以接下来以值 1 调用 request(..)，并从这第一个 Ajax 调用得到
一个 promise。
(6) 这个 promise 通过 yield 传出，回到 *foo(2) 生成器实例。
(7) yield * 把这个 promise 传出回到 *foo(3) 生成器实例。另一个 yield * 把这个 promise
传出回到 *bar() 生成器实例。再有一个 yield * 把这个 promise 传出回到 run(..) 工
具，这个工具会等待这个 promsie（第一个 Ajax 请求）的处理。
(8) 这个 promise 决议后，它的完成消息会发送出来恢复 *bar()；后者通过 yield * 转入
*foo(3) 实例；后者接着通过 yield * 转入 *foo(2) 生成器实例；后者再接着通过 yield *
转入 *foo(3) 生成器实例内部的等待着的普通 yield。
(9) 第一个调用的 Ajax 响应现在立即从 *foo(3) 生成器实例中返回。这个实例把值作为
*foo(2) 实例中 yield * 表达式的结果返回，赋给它的局部变量 val。
(10) 在 *foo(2) 中，通过 request(..) 发送了第二个 Ajax 请求。它的 promise 通过 yield
发回给 *foo(1) 实例，然后通过 yield * 一路传递到 run(..)（再次进行步骤 7）。这个
promise 决议后，第二个 Ajax 响应一路传播回到 *foo(2) 生成器实例，赋给它的局部
变量 val。
(11) 最后，通过 request(..) 发出第三个 Ajax 请求，它的 promise 传出到 run(..)，然后它
的决议值一路返回，然后 return 返回到 *bar() 中等待的 yield * 表达式。
噫！这么多疯狂的脑力杂耍，是不是？这一部分你可能需要多读几次，然后吃点零食让大
脑保持清醒！

## 4.6 生成器并发

就像我们在第 1 章和本章前面都讨论过的一样，两个同时运行的进程可以合作式地交替运
作，而很多时候这可以产生（双关，原文为 yield：既指产生又指 yield 关键字）非常强大270 ｜ 第 4 章
的异步表示。

坦白地说，本部分前面的多个生成器并发交替执行的例子已经展示了如何使其看起来令人
迷惑。但是，我们已经暗示过了，在一些场景中这个功能会很有用武之地的。
回想一下第 1 章给出的一个场景：其中两个不同并发 Ajax 响应处理函数需要彼此协调，
以确保数据交流不会出现竞态条件。我们把响应插入到 res 数组中，就像这样：

```js
function response(data) {
if (data.url == "http://some.url.1") {
res[0] = data;
}
else if (data.url == "http://some.url.2") {
res[1] = data;
}
}
但是这种场景下如何使用多个并发生成器呢？
// request(..)是一个支持Promise的Ajax工具
var res = [];
function *reqData(url) {
res.push(
yield request( url )
);
}
```

这里我们将使用生成器 *reqData(..) 的两个实例，但运行两个不同生成器的
实例也没有任何区别。两种方法的过程几乎一样。稍后将会介绍两个不同生
成器的彼此协调。

这里不需要手工为 res[0] 和 res[1] 赋值排序，而是使用合作式的排序，使得 res.
push(..) 把值按照预期以可预测的顺序正确安置。这样，表达的逻辑给人感觉应该更清晰
一点。

但是，实践中我们如何安排这些交互呢？首先，使用 Promise 手工实现：

```js
var it1 = reqData( "http://some.url.1" );
var it2 = reqData( "http://some.url.2" );
var p1 = it1.next();
var p2 = it2.next();
p1
.then( function(data){
it1.next( data );
return p2;生成器 ｜ 271
} )
.then( function(data){
it2.next( data );
} );
```

*reqData(..) 的两个实例都被启动来发送它们的 Ajax 请求，然后通过 yield 暂停。然后我
们选择在 p1 决议时恢复第一个实例，然后 p2 的决议会重启第二个实例。通过这种方式，
我们使用 Promise 配置确保 res[0] 中会放置第一个响应，而 res[1] 中会放置第二个响应。
但是，坦白地说，这种方式的手工程度非常高，并且它也不能真正地让生成器自己来协
调，而那才是真正的威力所在。让我们换一种方法试试：

```js
// request(..)是一个支持Promise的Ajax工具
var res = [];
function *reqData(url) {
var data = yield request( url );
// 控制转移
yield;
res.push( data );
}
var it1 = reqData( "http://some.url.1" );
var it2 = reqData( "http://some.url.2" );
var p1 = it.next();
var p2 = it.next();
p1.then( function(data){
it1.next( data );
} );
p2.then( function(data){
it2.next( data );
} );
Promise.all( [p1,p2] )
.then( function(){
it1.next();
it2.next();
} );
```

好吧，这看起来好一点（尽管仍然是手工的！），因为现在 *reqData(..) 的两个实例确实
是并发运行了，而且（至少对于前一部分来说）是相互独立的。

在前面的代码中，第二个实例直到第一个实例完全结束才得到数据。但在这里，两个实例
都是各自的响应一回来就取得了数据，然后每个实例再次 yield，用于控制传递的目的。
然后我们在 Promise.all([ .. ]) 处理函数中选择它们的恢复顺序。272 ｜ 第 4 章

可能不那么明显的是，因为对称性，这种方法以更简单的形式暗示了一种可重用的工具。
还可以做得更好。来设想一下使用一个称为 runAll(..) 的工具：

```js
// request(..)是一个支持Promise的Ajax工具
var res = [];
runAll(
function*(){
var p1 = request( "http://some.url.1" );
// 控制转移
yield;
res.push( yield p1 );
},
function*(){
var p2 = request( "http://some.url.2" );
// 控制转移
yield;
res.push( yield p2 );
}
);
```

我们不准备列出 runAll(..) 的代码，不仅是因为其可能因太长而使文本混乱，
也因为它是我们在前面 run(..) 中实现的逻辑的一个扩展。所以，我们把它
作为一个很好的扩展练习，请试着从 run(..) 的代码演进实现我们设想的
runAll(..) 的功能。我的 asynquence 库也提供了一个前面提过的 runner(..)
工具，其中已经内建了对类功能的支持，这将在本部分的附录 A 中讨论。

以下是 runAll(..) 内部运行的过程。
(1) 第一个生成器从第一个来自于 "http://some.url.1" 的 Ajax 响应得到一个 promise，然
后把控制 yield 回 runAll(..) 工具。
(2) 第二个生成器运行，对于 "http://some.url.2" 实现同样的操作，把控制 yield 回
runAll(..) 工具。
(3) 第一个生成器恢复运行，通过 yield 传出其 promise p1。在这种情况下， runAll(..) 工
具所做的和我们之前的 run(..) 一样，因为它会等待这个 promise 决议，然后恢复同一
个生成器（没有控制转移！）。 p1 决议后， runAll(..) 使用这个决议值再次恢复第一个
生成器，然后 res[0] 得到了自己的值。接着，在第一个生成器完成的时候，有一个隐
式的控制转移。
(4) 第二个生成器恢复运行，通过 yield 传出其 promise p2，并等待其决议。一旦决议，
runAll(..) 就用这个值恢复第二个生成器，设置 res[1]。生成器 ｜ 273
在这个例子的运行中，我们使用了一个名为 res 的外层变量来保存两个不同的 Ajax 响应结
果，我们的并发协调使其成为可能。
但是，如果继续扩展 runAll(..) 来提供一个内层的变量空间，以使多个生成器实例可以共
享，将是非常有帮助的，比如下面这个称为 data 的空对象。还有，它可以接受 yield 的非
Promise 值，并把它们传递到下一个生成器。
考虑：

```js
// request(..)是一个支持Promise的Ajax工具
runAll(
function*(data){
data.res = [];
// 控制转移（以及消息传递）
var url1 = yield "http://some.url.2";
var p1 = request( url1 ); // "http://some.url.1"
// 控制转移
yield;
data.res.push( yield p1 );
},
function*(data){
// 控制转移（以及消息传递）
var url2 = yield "http://some.url.1";
var p2 = request( url2 ); // "http://some.url.2"
// 控制转移
yield;
data.res.push( yield p2 );
}
);
```

在这一方案中，实际上两个生成器不只是协调控制转移，还彼此通信，通过 data.res 和
yield 的消息来交换 url1 和 url2 的值。真是极其强大！

这样的实现也为被称作通信顺序进程（Communicating Sequential Processes， CSP）的更高
级异步技术提供了一个概念基础。对此，我们将在本部分的附录 B 中详细讨论。

## 4.7 形实转换程序

目前为止，我们已经假定从生成器 yield 出一个 Promise，并且让这个 Promise 通过一个像
run(..) 这样的辅助函数恢复这个生成器，这是通过生成器管理异步的最好方法。要知道，
事实的确如此。274 ｜ 第 4 章

但是，我们忽略了另一种广泛使用的模式。为了完整性，我们来简要介绍一下这种模式。
在通用计算机科学领域，有一个早期的前 JavaScript 概念，称为形实转换程序（thunk）。
我们这里将不再陷入历史考据的泥沼，而是直接给出形实转换程序的一个狭义表述：
JavaScript 中的 thunk 是指一个用于调用另外一个函数的函数，没有任何参数。
换句话说，你用一个函数定义封装函数调用，包括需要的任何参数，来定义这个调用的执
行，那么这个封装函数就是一个形实转换程序。之后在执行这个 thunk 时，最终就是调用
了原始的函数。
举例来说：

```js
function foo(x,y) {
return x + y;
}
function fooThunk() {
return foo( 3, 4 );
}
// 将来
console.log( fooThunk() ); // 7
```

所以，同步的 thunk 是非常简单的。但如果是异步的 thunk 呢？我们可以把这个狭窄的
thunk 定义扩展到包含让它接收一个回调。
考虑：

```js
function foo(x,y,cb) {
setTimeout( function(){
cb( x + y );
}, 1000 );
}
function fooThunk(cb) {
foo( 3, 4, cb );
}
// 将来
fooThunk( function(sum){
console.log( sum ); // 7
} );
```

正如所见， fooThunk(..) 只需要一个参数 cb(..)，因为它已经有预先指定的值 3 和 4（分
别作为 x 和 y）可以传给 foo(..)。 thunk 就耐心地等待它完成工作所需的最后一部分：那
个回调。生成器 ｜ 275

但是，你并不会想手工编写 thunk。所以，我们发明一个工具来做这部分封装工作。
考虑：

```js
function thunkify(fn) {
var args = [].slice.call( arguments, 1 );
return function(cb) {
args.push( cb );
return fn.apply( null, args );
};
}
var fooThunk = thunkify( foo, 3, 4 );
// 将来
fooThunk( function(sum) {
console.log( sum ); // 7
} );
```

这里我们假定原始（foo(..)）函数原型需要的回调放在最后的位置，其他
参数都在它之前。对异步 JavaScript 函数标准来说，这可以说是一个普遍成
立的标准。你可以称之为“callback-last 风格”。如果出于某种原因需要处理
“callback-first 风格”原型，你可以构建一个使用 args.unshift(..) 而不是
args.push(..) 的工具。

前面 thunkify(..) 的实现接收 foo(..) 函数引用以及它需要的任意参数，并返回 thunk 本
身（fooThunk(..)）。但是，这并不是 JavaScript 中使用 thunk 的典型方案。
典型的方法——如果不令人迷惑的话——并不是 thunkify(..) 构造 thunk 本身，而是
thunkify(..) 工具产生一个生成 thunk 的函数。

考虑：
```js
function thunkify(fn) {
return function() {
var args = [].slice.call( arguments );
return function(cb) {
args.push( cb );
return fn.apply( null, args );
};
};
}
```

此处主要的区别在于多出来的 return function() { .. } 这一层。以下是用法上的区别：

```js
var whatIsThis = thunkify( foo );
var fooThunk = whatIsThis( 3, 4 );276 ｜ 第 4 章
// 将来
fooThunk( function(sum) {
console.log( sum ); // 7
} );
```

显然，这段代码暗藏的一个大问题是： whatIsThis 调用的是什么。并不是这个 thunk，而
是某个从 foo(..) 调用产生 thunk 的东西。这有点类似于 thunk 的“工厂”。似乎还没有任
何标准约定可以给这样的东西命名。

所以我的建议是 thunkory（thunk+factory）。于是就有， thunkify(..) 生成一个 thunkory，
然后 thunkory 生成 thunk。这和第 3 章中我提议 promisory 出于同样的原因：

```js
var fooThunkory = thunkify( foo );
var fooThunk1 = fooThunkory( 3, 4 );
var fooThunk2 = fooThunkory( 5, 6 );
// 将来
fooThunk1( function(sum) {
console.log( sum ); // 7
} );
fooThunk2( function(sum) {
console.log( sum ); // 11
} );
```

foo(..) 例子要求回调的风格不是 error-first 风格。当然， error-first 风格要常
见得多。如果 foo(..) 需要满足一些正统的错误生成期望，可以把它按照期
望改造，使用一个 error-first 回调。后面的 thunkify(..) 机制都不关心回调
的风格。使用上唯一的区别将会是 fooThunk1(function(err,sum){..。
暴露 thunkory 方法——而不是像前面的 thunkify(..) 那样把这个中间步骤隐藏——似乎是
不必要的复杂性。但是，一般来说，在程序开头构造 thunkory 来封装已有的 API 方法，并
在需要 thunk 时可以传递和调用这些 thunkory，是很有用的。两个独立的步骤保留了一个
更清晰的功能分离。

以下代码可说明这一点：
```js
// 更简洁：
var fooThunkory = thunkify( foo );
var fooThunk1 = fooThunkory( 3, 4 );
var fooThunk2 = fooThunkory( 5, 6 );
// 而不是：生成器 ｜ 277
var fooThunk1 = thunkify( foo, 3, 4 );
var fooThunk2 = thunkify( foo, 5, 6 );
```

不管你是否愿意显式地与 thunkory 打交道， thunk fooThunk1(..) 和 fooThunk2(..) 的用法
都是一样的。

s/promise/thunk/

那么所有这些关于 thunk 的内容与生成器有什么关系呢？

可以把 thunk 和 promise 大体上对比一下：它们的特性并不相同，所以并不能直接互换。
Promise 要比裸 thunk 功能更强、更值得信任。

但从另外一个角度来说，它们都可以被看作是对一个值的请求，回答可能是异步的。
回忆一下，在第 3 章里我们定义了一个工具用于 promise 化一个函数，我们称之为
Promise.wrap(..)，也可以将其称为 promisify(..) ！这个 Promise 封装工具并不产生
Promise，它生成的是 promisory，而 promisory 则接着产生 Promise。这和现在讨论的
thunkory 和 thunk 是完全对称的。

为了说明这种对称性，我们要首先把前面的 foo(..) 例子修改一下，改成使用 error-first 风
格的回调：

```js
function foo(x,y,cb) {
setTimeout( function(){
// 假定cb(..)是error-first风格的
cb( null, x + y );
}, 1000 );
}
```

现在我们对比一下 thunkify(..) 和 promisify(..)（即第 3 章中的 Promise.wrap(..)）的
使用：

```js
// 对称：构造问题提问者
var fooThunkory = thunkify( foo );
var fooPromisory = promisify( foo );
// 对称：提问
var fooThunk = fooThunkory( 3, 4 );
var fooPromise = fooPromisory( 3, 4 );
// 得到答案
fooThunk( function(err,sum){
if (err) {
console.error( err );
}
else {
console.log( sum ); // 7278 ｜ 第 4 章
}
} );
// 得到promise答案
fooPromise
.then(
function(sum){
console.log( sum ); // 7
},
function(err){
console.error( err );
}
);
```

thunkory 和 promisory 本质上都是在提出一个请求（要求一个值），分别由 thunk fooThunk
和 promise fooPromise 表示对这个请求的未来的答复。这样考虑的话，这种对称性就很清
晰了。

了解了这个视角之后，就可以看出， yield 出 Promise 以获得异步性的生成器，也可以为
异步性而 yield thunk。我们所需要的只是一个更智能的 run(..) 工具（就像前面的一样），
不但能够寻找和链接 yield 出来的 Promise，还能够向 yield 出来的 thunk 提供回调。

考虑：
```js
function *foo() {
var val = yield request( "http://some.url.1" );
console.log( val );
}
run( foo );
```

在这个例子中， request(..) 可能是一个返回 promise 的 promisory，也可能是一个返回
thunk 的 thunkory。从生成器内部的代码逻辑的角度来说，我们并不关心这个实现细节，这
一点是非常强大的！

于是， request(..) 可能是以下两者之一：

```js
// promisory request(..)（参见第3章）
var request = Promise.wrap( ajax );
// vs.
// thunkory request(..)
var request = thunkify( ajax );
最后，作为前面 run(..) 工具的一个支持 thunk 的补丁，我们还需要这样的逻辑：
// ..
// 我们收到返回的thunk了吗？
else if (typeof next.value == "function") {
return new Promise( function(resolve,reject){生成器 ｜ 279
// 用error-first回调调用这个thunk
next.value( function(err,msg) {
if (err) {
reject( err );
}
else {
resolve( msg );
}
} );
} )
.then(
handleNext,
function handleErr(err) {
return Promise.resolve(
it.throw( err )
)
.then( handleResult );
}
);
}
```

现在，我们的生成器可以调用 promisory 来 yield Promise，也可以调用 thunkory 来 yield
thunk。不管哪种情况， run(..) 都能够处理这个值，并等待它的完成来恢复生成器运行。
从对称性来说，这两种方案看起来是一样的。但应该指出，这只是从代表生成器的未来值
continuation 的 Promise 或 thunk 的角度说才是正确的。

从更大的角度来说， thunk 本身基本上没有任何可信任性和可组合性保证，而这些是
Promise 的设计目标所在。单独使用 thunk 作为 Pormise 的替代在这个特定的生成器异步模
式里是可行的，但是与 Promise 具备的优势（参见第 3 章）相比，这应该并不是一种理想
方案。

如果可以选择的话，你应该使用 yield pr 而不是 yield th。但对 run(..) 工具来说，对两
种值类型都能提供支持则是完全正确的。

我的 asynquence 库（详见附录 A）中的 runner(..) 工具可以处理 Promise、
thunk 和 asynquence 序列的 yield。

## 4.8 ES6 之前的生成器

现在，希望你已经相信，生成器是异步编程工具箱中新增的一种非常重要的工具。但是，
这是 ES6 中新增的语法，这意味着你没法像对待 Promise（这只是一种新的 API）那样使
用生成器。所以如果不能忽略 ES6 前的浏览器的话，怎么才能把生成器引入到我们的浏览280 ｜ 第 4 章
器 JavaScript 中呢？

对 ES6 中所有的语法扩展来说，都有工具（最常见的术语是 transpiler，指 trans-compiler，
翻译编译器）用于接收 ES6 语法并将其翻译为等价（但是显然要丑陋一些！ ）的前 ES6 代
码。因此，生成器可以被翻译为具有同样功能但可以工作于 ES5 及之前的代码。
可怎么实现呢？显然 yield 的“魔法”看起来并不那么容易翻译。实际上，我们之前在讨
论基于闭包的迭代器时已经暗示了一种解决方案。

### 4.8.1　手工变换

在讨论 transpiler 之前，先来推导一下对生成器来说手工变换是如何实现的。这不只是一个
理论上的练习，因为这个练习实际上可以帮助我们更深入理解其工作原理。

考虑：
```js
// request(..)是一个支持Promise的Ajax工具
function *foo(url) {
try {
console.log( "requesting:", url );
var val = yield request( url );
console.log( val );
}
catch (err) {
console.log( "Oops:", err );
return false;
}
}
var it = foo( "http://some.url.1" );
```

首先要观察到的是，我们仍然需要一个可以调用的普通函数 foo()，它仍然需要返回一个
迭代器。因此，先把非生成器变换的轮廓刻画出来：

```js
function foo(url) {
// ..
// 构造并返回一个迭代器
return {
next: function(v) {
// ..
},
throw: function(e) {
// ..
}
};
}
var it = foo( "http://some.url.1" );
```

接下来要观察到的是，生成器是通过暂停自己的作用域 / 状态实现它的“魔法”的。可以
通过函数闭包（参见本系列的《你不知道的 JavaScript（上卷）》 的“作用域和闭包”部分）
来模拟这一点。为了理解这样的代码是如何编写的，我们先给生成器的各个部分标注上状
态值：

```js
// request(..)是一个支持Promise的Ajax工具
function *foo(url) {
// 状态1
try {
console.log( "requesting:", url );
var TMP1 = request( url );
// 状态2
var val = yield TMP1;
console.log( val );
}
catch (err) {
// 状态3
console.log( "Oops:", err );
return false;
}
}
```

为了更精确地展示，我们使用临时变量 TMP1 把 val = yield request.. 语句
分成了两个部分。 request(..) 在状态 1 发生，其完成值赋给 val 发生在状态
2。当我们把代码转换成其非生成器等价时，会去掉这个中间变量 TMP1。

换句话说， 1 是起始状态， 2 是 request(..) 成功后的状态， 3 是 request(..) 失败的状态。
你大概能够想象出如何把任何额外的 yield 步骤编码为更多的状态。

回到我们翻译的生成器，让我们在闭包中定义一个变量 state 用于跟踪状态：

```js
function foo(url) {
// 管理生成器状态
var state;
// ..
}
现在在闭包内定义一个内层函数，称为 process(..)，使用 switch 语句处理每个状态：
// request(..)是一个支持Promise的Ajax工具
function foo(url) {
// 管理生成器状态282 ｜ 第 4 章
var state;
// 生成器范围变量声明
var val;
function process(v) {
switch (state) {
case 1:
console.log( "requesting:", url );
return request( url );
case 2:
val = v;
console.log( val );
return;
case 3:
var err = v;
console.log( "Oops:", err );
return false;
}
}
// ..
}
```

我们生成器的每个状态都在 switch 语句中由自己的 case 表示。每次需要处理一个新状态
的时候就会调用 process(..)。稍后我们将会回来介绍这是如何工作的。

对于每个生成器级的变量声明（val），我们都把它移动为 process(..) 外的一个 val 声明，
这样它们就可以在多个 process(..) 调用之间存活。不过块作用域的变量 err 只在状态 3
中需要使用，所以把它留在原来的位置。

在状态 1，没有了 yield resolve(..)，我们所做的是 return resolve(..)。在终止状态 2，
没有显式的 return，所以我们只做一个 return，这等价于 return undefined。在终止状态
3，有一个 return false，因此就保留这一句。

现在需要定义迭代器函数的代码，使这些函数正确调用 process(..)：

```js
function foo(url) {
// 管理生成器状态
var state;
// 生成器变量范围声明
var val;
function process(v) {
switch (state) {
case 1:
console.log( "requesting:", url );
return request( url );
case 2:
val = v;
console.log( val );生成器 ｜ 283
return;
case 3:
var err = v;
console.log( "Oops:", err );
return false;
}
}
// 构造并返回一个生成器
return {
next: function(v) {
// 初始状态
if (!state) {
state = 1;
return {
done: false,
value: process()
};
}
// yield成功恢复
else if (state == 1) {
state = 2;
return {
done: true,
value: process( v )
};
}
// 生成器已经完成
else {
return {
done: true,
value: undefined
};
}
},
"throw": function(e) {
// 唯一的显式错误处理在状态1
if (state == 1) {
state = 3;
return {
done: true,
value: process( e )
};
}
// 否则错误就不会处理，所以只把它抛回
else {
throw e;
}
}
};
}
```

这段代码是如何工作的呢？
(1) 对迭代器的 next() 的第一个调用会把生成器从未初始化状态转移到状态 1，然后调用
process() 来处理这个状态。 request(..) 的返回值是对应 Ajax 响应的 promise，作为
value 属性从 next() 调用返回。
(2) 如果 Ajax 请求成功，第二个 next(..) 调用应该发送 Ajax 响应值进来，这会把状态转
移到状态 2。再次调用 process(..)（这次包括传入的 Ajax 响应值），从 next(..) 返回
的 value 属性将是 undefined。
(3) 然而， 如果 Ajax 请求失败的话，就会使用错误调用 throw(..)，这会把状态从 1 转移到
3（而非 2）。再次调用 process(..)，这一次包含错误值。这个 case 返回 false，被作
为 throw(..) 调用返回的 value 属性。
从外部来看（也就是说，只与迭代器交互），这个普通函数 foo(..) 与生成器 *foo(..) 的
工作几乎完全一样。所以我们已经成功地把 ES6 生成器转为了前 ES6 兼容代码！
然后就可以手工实例化生成器并控制它的迭代器了，调用 var it = foo("..") 和
it.next(..) 等。甚至更好的是，我们可以把它传给前面定义的工具 run(..)，就像
run(foo,"..")。

### 4.8.2　自动转换

前面的 ES6 生成器到前 ES6 等价代码的手工推导练习，向我们教授了概念上生成器是如何
工作的。但是，这个变换非常复杂，并且对于代码中的其他生成器而言也是不可移植的。
这部分工作通过手工实现十分不实际，会完全抵消生成器的一切优势。

但幸运的是，已经有一些工具可以自动把 ES6 生成器转化为前面小节中我们推导出来的
结果那样的代码。它们不仅会为我们完成这些笨重的工作，还会处理我们忽略的几个枝节
问题。

regenerator 就是这样的一个工具（http://facebook.github.io/regenerator/），出自 Facebook 的
几个聪明人。

如果使用 regenerator 来转换前面的生成器的话，以下是产生的代码（本书写作之时）：

```js
// request(..)是一个支持Promise的Ajax工具
var foo = regeneratorRuntime.mark(function foo(url) {
var val;
return regeneratorRuntime.wrap(function foo$(context$1$0) {
while (1) switch (context$1$0.prev = context$1$0.next) {
case 0:
context$1$0.prev = 0;
console.log( "requesting:", url );生成器 ｜ 285
context$1$0.next = 4;
return request( url );
case 4:
val = context$1$0.sent;
console.log( val );
context$1$0.next = 12;
break;
case 8:
context$1$0.prev = 8;
context$1$0.t0 = context$1$0.catch(0);
console.log("Oops:", context$1$0.t0);
return context$1$0.abrupt("return", false);
case 12:
case "end":
return context$1$0.stop();
}
}, foo, this, [[0, 8]]);
});
```

这与我们手工推导的结果有一些明显的相似之处，比如那些 switch/case 语句，而且我们
甚至看到了移出闭包的 val，就像我们做的一样。

当然，一个不同之处是， regenerator 的变换需要一个辅助库 regeneratorRuntime，其中包
含了管理通用生成器和迭代器的所有可复用逻辑。这些重复代码中有很多和我们的版本不
同，但即使这样，很多概念还是可以看到的，比如 context$1$0.next = 4 记录生成器的下
一个状态。

主要的收获是，生成器不再局限于只能在 ES6+ 环境中使用。一旦理解了这些概念，就可
以在代码中使用，然后使用工具将其变换为与旧环境兼容的代码。

这比仅仅将修改后的 Promise API 用作前 ES6 Promise 所做的工作要多得多，但是，付出的
代价是值得的，因为在实现以合理的、明智的、看似同步的、顺序的方式表达异步流程方
面，生成器的优势太多了。

一旦迷上了生成器，就再也不会想回到那一团乱麻的异步回调地狱中了。

## 4.9 小结

生成器是 ES6 的一个新的函数类型，它并不像普通函数那样总是运行到结束。取而代之的是，生成器可以在运行当中（完全保持其状态）暂停，并且将来再从暂停的地方恢复运行。

这种交替的暂停和恢复是合作性的而不是抢占式的，这意味着生成器具有独一无二的能力来暂停自身，这是通过关键字 yield 实现的。不过，只有控制生成器的迭代器具有恢复生成器的能力（通过 next(..)）。

`yield/next(..)` 这一对不只是一种控制机制，实际上也是一种双向消息传递机制。 `yield ..` 表
达式本质上是暂停下来等待某个值，接下来的 `next(..)` 调用会向被暂停的 yield 表达式传回
一个值（或者是隐式的 undefined）。

在异步控制流程方面，生成器的关键优点是：生成器内部的代码是以自然的同步 / 顺序方式表达任务的一系列步骤。其技巧在于，我们把可能的异步隐藏在了关键字 yield 的后面，把异步移动到控制生成器的迭代器的代码部分。

换句话说，生成器为异步代码保持了顺序、同步、阻塞的代码模式，这使得大脑可以更自然地追踪代码，解决了基于回调的异步的两个关键缺陷之一。

## 第5章 程序性能	

### 5.1 Web Worker

JavaScript 当前并没有任何支持多线程执行的功能，但是浏览器环境很容易提供多个 JavaScript 引擎实例，各自运行在自己的线程上，这样就可以在每个线程上运行不同的程序。程序中每一个这样的独立的多线程部分被称为一个（Web）Worker。这种类型的并行化被称为任务并行，因为其重点在于把程序划分为多个块来并行运行。

从 JavaScript 主程序（或另一个Worker）中，可以这样实例化一个 Worker。这个 URL 应该指向一个 JavaScript 文件的位置，这个文件将被加载到一个 Worker 中。然后浏览器启动一个独立的线程，让这个文件在这个线程中作为独立的程序运行。Worker 之间以及它们和主程序之间，不会共享任何作用域或资源，那会把所有多线程编程的噩梦带到前端领域，而是通过一个基本的事件消息机制互相联系。

```JavaScript
var w1 = new Worker( "http://some.url.1/mycoolworker.js" );
```

Worker w1 对象是一个事件侦听者和触发者，可以通过订阅它来获得这个 Worker 发出的事件以及发送事件给这个 Worker。侦听事件，其实就是固定的“message”事件，也可以发送“message”事件给这个 Worker。在这个 Worker 内部，收发消息时完全对称的。

```JavaScript
// 侦听事件
w1.addEventListener( "message", function(evt){
	// evt.data
} );

// 发送事件
w1.postMessage( "something cool to say" );

```

通常由主页面应用程序创建 Worker，但若是需要的话，Worker 也可以实例化它自己的子 Worker，称为 subworker。有时候，把这样的细节委托给一个“主” Worker，由它来创建其他 Worker 处理部分任务，这样很有用。

要在创建 Worker 的程序中终止 Worker，可以调用 Worker 对象。突然终止 Worker 线程不会给它任何机会完成它的工作或者清理任何资源。这就类似于通过关闭浏览器标签页来关闭页面。

Worker 环境。在 Worker 内部是无法访问主程序的任何资源的。这意味着不能访问它的任何全局变量，也不能访问页面的 DOM 或者其他资源。这是一个完全独立的线程。但是，可以执行网络操作（Ajax、WebSockets）以及设定定时器。还有，Worker 可以访问几个重要的全局变量和功能的本地复本，包括 navigator、location、JSON 和 applicationCache。还可以通过`importScripts(..)`向 Worker 加载额外的 JavaScript 脚本，这些脚本加载时同步的，调用会阻塞余下 Worker 的执行。

```JavaScript
// inside the Worker
importScripts( "foo.js", "bar.js" );
```

Web Worker 通常应用于下面几个方面。

- 处理密集型数学计算
- 大数据集排序
- 数据处理（压缩、音频分析、图像处理等）
- 高流量网络通信

数据传递。这些应用中的大多数都有一个共性，那就是需要在线程之间通过事件机制传递大量的信息，可能是双向的。

在早期的 Worker 中，唯一的选择就是把所有数据序列化到一个字符串值中。除了双向序列化导致的速度损失之外，另一个主要的负面因素是数据需要被赋值，这意味着两倍的内存使用（以及引起的垃圾收集方面的波动）

现在已经有了更好的选择。如果要传递一个对象，可以使用结构化克隆算范把这个对象复制到另一边。这个算法非常高级，甚至可以处理要复制的对象有循环引用的情况。这样就不用付出 to-string 和 from-string 的性能损失了，但是这种方案还是要使用双倍的内存。

还有一个更好的选择，特别是对于大数据而言，就是使用 Transferable 对象。这时发生的是对象所有权的转移，数据本身并没有移动。一旦把对象传递到一个 Worker 中，在原来的位置上，它就编程空的或者是不可访问的，这样就消除了多线程编程作用域共享带来的混乱。当然，所有权传递是可以双向进行的。

如果选择 Transferable 对象的话，其实不需要做什么。任何实现了 Transferable 接口）的数据结构就自动按照这种方式传输。举例来说，像 Uint8Array 这样的带类型的数组就是 Transferable。下面是如何使用`postMessage(..)`发送一个 Transferable 对象。第一个参数是一个原始缓冲区，第二个是一个要传输的内容的列表。

```JavaScript
// `foo` is a `Uint8Array` for instance
postMessage( foo.buffer, [ foo.buffer ] );
```

不支持 Transferable 对象的浏览器就降级到结构化克隆，这会带来性能下降而不是彻底的功能失效。

共享 Worker。如果站点或 app 允许加载同一个页面的多个 tab，那可能非常希望通过专用 Worker 来降低系统的资源使用。在这一方面最常见的有限资源就是 socket 网络连接，因为浏览器限制了到同一个主机的同时连接数目。当然，限制来自于同一客户端的连接数也减轻了资源压力。在这种情况下，创建一个整个站点或 app 的所有页面实例都可以共享的中心 Worker 就非常有用了。这称为 shareWorker，可通过下面的方式创建。

```JavaScript
var w1 = new SharedWorker( "http://some.url.1/mycoolworker.js" );
```

因为共享 Worker 可以与站点的多个程序实例或多个页面连接，所以这个 Worker 需要通过某种方式来得知消息来自于哪个程序。这个唯一标识符称为端口（port），可以类比网络 socket 的端口。因此，调用程序必须使用 Worker 的 port 对象用于通信。还有，端口连接必须要初始化。

```JavaScript
w1.port.addEventListener( "message", handleMessages );

// ..

w1.port.postMessage( "something cool" );

w1.port.start();
```

在共享 Worker 内部，必须要处理额外的一个事件： "connect"。这个事件为这个特定的连接提供了端口对象。保持多个连接独立的最简单办法就是使用 port 上的闭包，就像下面的代码一样，把这个链接上的事件侦听和传递定义在 "connect" 事件的处理函数内部：

```JavaScript
// inside the shared Worker
addEventListener( "connect", function(evt){
	// the assigned port for this connection
	var port = evt.ports[0];

	port.addEventListener( "message", function(evt){
		// ..

		port.postMessage( .. );

		// ..
	} );

	// initialize the port connection
	port.start();
} );
```

模拟 Web Worker。从性能的角度来说，将 Web Worker 用于并行运行 JavaScript程序时非常有吸引力的方案。但是，由于环境所限，可能需要在缺乏对此支持的更老的浏览器中运行代码。因为 Worker 是一种 API 而不是语法，所以可以作为扩展来模拟它。

如果浏览器不支持 Worker，那么从性能的角度来说是没法模拟多线程的。通常认为 Iframe 提供了并行环境，但是在所有的现代浏览器中，它们实际上都是和主页面运行在同一个线程中的，所以并不足以模拟并发。

### 5.2 SIMD

单指令多数据（SIMD）是一种数据并行（data parallelism）方式，与 Web Worker 的任务并行（task parallelism）相对，因为这里的重点实际上不再是把程序逻辑分成并行的块，而是并行处理数据的多个位。

SIMD JavaScript 计划向 JavaScript 代码暴露短向量类型和 API。在支持 SIMD 的那些系统中，这些运算将会直接映射到等价的 CPU 指令，而在非 SIMD 系统中就会退化回非并行化的运算。


### 5.3 asm.js

asm.js 这个标签是指 JavaScript 语言中可以高度优化的一个子集。通过小心避免某些难以优化的机制和模式（垃圾收集、类型强制转换，等等），asm.js 风格的代码可以被 JavaScript 引擎识别并进行特别激进的底层优化。

如何使用 asm.js 优化。关于 asm.js 优化，首先要理解的是类型和强制类型转换。如果 JavaScript 引擎需要跟踪一个变量在各种各样的运算之间的多个不同类型的值，才能按需处理类型之间的强制类型转换，那么这大量的额外工作会使得程序优化无法达到最优。

还有一些技巧可以用来向支持 asm.js 的 JavaScript 引擎暗示变量和运算想要的类型是什么，使它可以省略这些类型转换跟踪步骤。

asm.js 模块。对 JavaScript 性能影响最大的因素是内存分配、垃圾收集和作用域访问。asm.js 对这些问题提出的一个解决方案就是，声明一个更正式的 asm.js“模块”，不要和 ES6 模块混淆。

显然，使 asm.js 代码如此高度可优化的那些限制的特性显著降低了这类代码的使用范围。asm.js 并不是对任意程序都适用的通用优化手段。它的目标是对特定的任务处理提供一种优化方法，比如数学运算（如游戏中的图形处理）。

## 第6章 性能测试与调优	



## 附录A asynquence 库	



## 附录B 高级异步模式

