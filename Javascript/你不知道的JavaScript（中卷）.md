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

## 第1章 异步：现在与将来	

程序中现在运行的部分和将来运行的部分之间的关系就是异步编程的核心。  

可以把 JavaScript 程序写在单个 .js 文件中，但是这个程序几乎一定是由多个块构成的。这些块中只有一个是现在执行，其余的则会在将来执行。最常见的块单位是函数。换句话说， 现在无法完成的任务将会异步完成，因此 并不会出现人们本能地认为会出现的或希望出现的阻塞行为。  

从现在到将来的“等待”，最简单的方法（但绝对不是唯一的，甚至也不是最好的！）是使用一个通常称为回调函数的函数。任何时候，只要把一段代码包装成一个函数，并指定它在响应某个事件（定时器、鼠标点 击、 Ajax 响应等）时执行，你就是在代码中创建了一个将来执行的块，也由此在这个程序中引入了异步机制。 

并没有什么规范或一组需求指定 console.* 方法族如何工作——它们并不是 JavaScript 正式的一部分，而是由宿主环境添加到 JavaScript 中的。，在某些条件下，某些浏览器的 console.log(..) 并不会把传入的内容立即输出。出现这种情况的主要原因是，在许多程序（不只是 JavaScript）中， I/O 是非常低速的阻塞部分。所以，浏览器在后台异步处理控制台 I/O 能够提高性能，这时用户甚至可能根本意识不到其发生。  

JavaScript 引擎并不是独立运行的，它运行在宿主环境中，对多数开发者来说通常就是 Web 浏览器。所有的环境都有一个共同点，即它们都提供了一种机制来处理程序中多个块的执行，且执行每块时调用 JavaScript 引擎，这种机制被称为事件循环。换句话说， JavaScript 引擎本身并没有时间的概念，只是一个按需执行 JavaScript 任意代码片段的环境。“事件”（JavaScript 代码执行）调度总是由包含它的环境进行。  

setTimeout(..) 定时器的精度可能不高。大体说来，只能确保你的回调函数不会在指定的时间间隔之前运行，但可能会在那个时刻运行，也可能在那之后运行，要根据事件队列的状态而定。

异步是关于现在和将来的时间间隙，而并行是关于能够同时发生的事情。  

并行计算最常见的工具就是进程和线程。进程和线程独立运行，并可能同时运行：在不同的处理器，甚至不同的计算机上，但多个线程能够共享单个进程的内存。  

与之相对的是，事件循环把自身的工作分成一个个任务并顺序执行，不允许对共享内存的并行访问和修改。通过分立线程中彼此合作的事件循环，并行和顺序执行可以共存。  

由于 JavaScript 的单线程特性， foo()（以及 bar()）中的代码具有原子性。也就是说，一 旦 foo() 开始运行，它的所有代码都会在 bar() 中的任意代码运行之前完成，或者相反。 这称为完整运行（run-to-completion）特性。  

在 JavaScript 的特性中，这种函数顺序的不确定性就是通常所说的竞态条件（race condition）， foo() 和 bar() 相互竞争，看谁先运行。具体来说，因为无法可靠预测 a 和 b 的最终结果，所以才是竞态条件。  

两个或多个“进程”同时执行就出现了并发，不管组成它们的单个运算是否并行执行（在独立的处理器或处理器核心上同时运行）。单线程事件循环是并发的一种形式。

两个或多个“进程”在同一个程序内并发地交替运行它们的步骤 / 事件时，如果这些任务 彼此不相关，就不一定需要交互。 如果进程间没有相互影响的话，不确定性是完全可以接受的。  

更常见的情况是，并发的“进程”需要相互交流，通过作用域或 DOM 间接交互。如果出现这样的交互，就需要对它们的交互进行协调以避免竞态的出现。  

还有一种并发合作方式，称为并发协作（cooperative concurrency）。这里的目标是取到一个长期运行的“进程”，并将其分割成多个步骤或多批任务，使得其他并发“进程”有机会将自己的运算插入到事件循环队列中交替运行。  

```javascript
var res = [];

// `response(..)` receives array of results from the Ajax call
function response(data) {
	// let's just do 1000 at a time
	var chunk = data.splice( 0, 1000 );

	// add onto existing `res` array
	res = res.concat(
		// make a new transformed array with all `chunk` values doubled
		chunk.map( function(val){
			return val * 2;
		} )
	);

	// anything left to process?
	if (data.length > 0) {
		// async schedule next batch
		setTimeout( function(){
			response( data );
		}, 0 );
	}
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax( "http://some.url.1", response );
ajax( "http://some.url.2", response );
```



在 ES6 中，有一个新的概念建立在事件循环队列之上，叫作任务队列（job queue）。这个 概念给大家带来的最大影响可能是 Promise 的异步特性。它是挂在事件循环队列的每个 tick 之后 的一个队列。在事件循环的每个 tick 中，可能出现的异步动作不会导致一个完整的新事件添加到事件循环队列中，而会在当前 tick 的任务队列末尾添加一个项目（一个任务）。  

## 第2章 回调	

在所有这些示例中，函数都是作为回调（callback）使用的，因为它是事件循环“回头调用”到程序中的目标，队列处理到这个项目的时候会运行它。回调函数包裹或者说封装了程序的延续（continuation）。  

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



有时候 ajax(..)（也就是你交付回调 continuation 的第三方）不是你编写的代码，也不在你的直接控制下。多数情况下，它是某个第三方提供的工具。 我们把这称为控制反转（inversion of control）， 也就是把自己程序一部分的执行控制交给某 个第三方。在你的代码和第三方工具（一组你希望有人维护的东西）之间有一份并没有明确表达的契约。回调最大的问题是控制反转，它会导致信任链的完全断裂。  

从回调模式内部进行解决。为了更优雅地处理错误，有些 API 设计提供了分离回调（一个用于成功通知， 一个用于出错通知）  。还有一种常见的回调模式叫作“error-first 风格”（有时候也称为“Node 风格”，因为几乎所有 Node.js API 都采用这种风格），其中回调的第一个参数保留用作错误对象（如果有的 话）。如果成功的话，这个参数就会被清空 / 置假（后续的参数就是成功数据）。不过，如果产生了错误结果，那么第一个参数就会被置起 / 置真（通常就不会再传递其他结果）。

那么完全不调用这个信任问题又会怎样呢？ 可能需要设置一个超时来取消事件。可以构造一个工具（这里展示的只是一个“验证概念”版本）来帮助实现这一点。

```javascript
function timeoutify(fn,delay) {
	var intv = setTimeout( function(){
			intv = null;
			fn( new Error( "Timeout!" ) );
		}, delay )
	;

	return function() {
		// timeout hasn't happened yet?
		if (intv) {
			clearTimeout( intv );
			fn.apply( this, [ null ].concat( [].slice.call( arguments ) ) );
		}
	};
}
// Here's how you use it:
// using "error-first style" callback design
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



如果你不确定关注的 API 会不会永远异步执行怎么办呢？可以创建一个类似于这个“验证概念”版本的 asyncify(..) 工具。

```javascript
function asyncify(fn) {
	var orig_fn = fn,
		intv = setTimeout( function(){
			intv = null;
			if (fn) fn();
		}, 0 )
	;

	fn = null;

	return function() {
		// firing too quickly, before `intv` timer has fired to
		// indicate async turn has passed?
		if (intv) {
			fn = orig_fn.bind.apply(
				orig_fn,
				// add the wrapper's `this` to the `bind(..)`
				// call parameters, as well as currying any
				// passed in parameters
				[this].concat( [].slice.call( arguments ) )
			);
		}
		// already async
		else {
			// invoke original function
			orig_fn.apply( this, arguments );
		}
	};
}
// You use asyncify(..) like this:

function result(data) {
	console.log( a );
}

var a = 0;

ajax( "..pre-cached-url..", asyncify( result ) );
a++;
```



## 第3章 Promise	

### 3.1 什么是Promise

通过 Promise，调用 then(..) 实际上可以接受两个函数，第一个用于完成情况，第二个用于拒绝情况。从外部看，由于 Promise 封装了依赖于时间的状态——等待底层值的完成或拒绝，所以 Promise 本身是与时间无关的。因此， Promise 可以按照可预测的方式组成（组合），而不用关心时序或底层的结果。  另外，一旦 Promise 决议，它就永远保持在这个状态。此时它就成为了不变值（immutable value），可以根据需求多次查看。  

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



## 第4章 生成器	

### 4.1 打破完整运行

ES6 引入了一个新的函数类型，它并不符合一个函数一旦开始就会运行到结束的特性。这类新的函数被称为生成器。生成器就是一类特殊的函数，可以一次或多次启动和停止，并不一定非得要完成。    

除了能够接受参数并提供返回值之外，生成器甚至提供了更强大更引人注目的内建消息输入输出能力，通过 yield 和 next(..) 实现。同一个生成器的多个实例可以同时运行，它们甚至可以彼此交互。

### 4.2 生成器产生值 



### 4.3 异步迭代生成器 



### 4.4 生成器 +Promise



### 4.5 生成器委托



### 4.6 生成器并发



### 4.7 形实转换程序



### 4.8 ES6之前的生成器



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

