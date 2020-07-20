> 深入理解 ES6  
> Understanding ES6  
> 2017 年 7 月第一版  
> [开源图书地址](https://github.com/nzakas/understandinges6)

# 第 1 章 块级作用域绑定

## 1.1 var 声明及变量提升机制

在函数作用域或全局作用域中通过关键宇 var 声明的变量，无论实际上是在哪里声明的，都会被当成在当前作用域顶部声明的变量，这就是我们常说的提升（Hoisting）机制。

```javascript
function getValue(condition) {
  if (condition) {
    var value = "blue";
    // other code
    return value;
  } else {
    // value exists here with a value of undefined
    return null;
  }
  // value exists here with a value of undefined
}

// 相当于
function getValue(condition) {
  var value;
  if (condition) {
    value = "blue";
    // other code
    return value;
  } else {
    return null;
  }
}
```

## 1.2 块级声明

块级声明用于声明在指定块的作用域之外无法访问的变量。块级作用域（也被称为词法作用域）存在于：函数内部、块中（字符 `{` 和 `}` 之间的区域）。很多类 C 语言都有块级作用域，而 ECMAScript 6 引入块级作用域就是为了让 JavaScript 更灵活也更普适。

let 声明。let 声明的用法与 var 相同。使用 let 来代替声明变量，就可以把变量的作用域限制在当前代码块中。由于 let 声明不会被提升，因此开发者通常将 let 声明语句放在封闭代码块的顶部，以便整个代码块都可以访问。

禁止重声明。假设作用域中已经存在某个标识符，此时再使用 let 关键字声明它机会抛出错误。但如果当前作用域内嵌另一个作用域，便可在内嵌的作用域中用 let 声明同名变量。

const 声明。使用 cons 声明的是常量，其值一旦被设定后不可更改。因此，每个通过 const 声明的变量必须进行初始化。

const 和 let 声明的都是块级标识符，所以常量也只在当前代码块内有效，一旦执行到块外立即被销毁。常量同样也不会被提升至作用域顶部。

与 let 相似，在同一作用域用 const 声明已经存在的标识符也会导致语法错误，无论该标识符是使用 var，还是 let 声明的。

const 声明与 let 声明有一处很大的不同，即无论在严格模式还是在非严格模式下，都不可以为 const 定义的常量再赋值，否则会抛出错误。但是，JavaScript 中的常量如果是对象，则对象中的值可以修改。

```javascript
const person = {
  name: "Nicholas",
};

// works
person.name = "Greg";

// throws an error
person = {
  name: "Greg",
};
```

临时死区 TDZ。与 var 不同，let 和 const 声明的变量不会被提升到作用域顶部，如果在声明之前访问这些变量，即使是相对安全的 typeof 操作符也会触发引用错误。但在 let 声明的作用域外对该变量使用 typeof 则不会报错。

JavaScript 引擎在扫描代码发现变量声明时，要么将它们提升至作用域顶部（遇到 var 声明），要么将声明放到 TDZ 中（遇到 let 和 const 声明）。访问 TDZ 中的变量会触发运行时错误。只有执行过变量声明语句后，变量才会从 TDZ 中移出，然后方可正常访问。

## 1.3 循环中的块作用域绑定

开发者可能最希望实现 for 循环的块级作用域了，因为可以把随意声明的计算器变量限制在循环内部。在 JavaScript 中，由于 var 声明得到了提升，变量在循环结束后仍可访问。如果换用 let 声明变量就能得到想要的结果。

```javascript
for (let i = 0; i < 10; i++) {
  process(items[i]);
}

// i is not accessible here - throws an error
console.log(i);
```

循环中的函数。长久以来，var 声明让开发者在循环中创建函数变得异常困难，因为变量到了循环之外仍能访问。

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
  funcs.push(function () {
    console.log(i);
  });
}

funcs.forEach(function (func) {
  func(); // outputs the number "10" ten times
});
```

为了解决这个问题，开发者们在循环中使用立即调用函数表达式（IIFE），以强制生成计算器变量的副本。在循环内部，IIFE 表达式为接受的每一个变量 i 都创建了一个副本并存储为变量 value。这个变量的值就是相应迭代创建的函数所使用的值。

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
  funcs.push(
    (function (value) {
      return function () {
        console.log(value);
      };
    })(i)
  );
}

funcs.forEach(function (func) {
  func(); // outputs 0, then 1, then 2, up to 9
});
```

循环中的 let 声明。let 声明模仿上述实例中 IIFE 所做的一切来简化循环过程，每次迭代循环都会创建一个新变量，并以之前迭代中的同名变量的值将其初始化。这意味着彻底删除 IIFE 之后仍可得到预期中的结果。每次循环的时候 let 声明都会创建一个新变量 i，并将其初始化为 i 的当前值，每次循环内部创建的每隔函数都能得到属于它们自己的 i 的副本。对于 for-in 循环和 for-of 循环来说也是一样的。

```javascript
var funcs = [];

for (let i = 0; i < 10; i++) {
  funcs.push(function () {
    console.log(i);
  });
}

funcs.forEach(function (func) {
  func(); // outputs 0, then 1, then 2, up to 9
});
```

循环中的 const 声明。对于普通的 for 循环来说，可以在初始化变量时使用 const，但是更改这个变量的值就会抛出错误。在 for-in 或 for-of 循环中使用 const 时的行为与使用 let 一致，唯一的区别是在循环内不能改变变量的值，每次迭代不会修改已有的绑定，而是会创建一个新绑定。

## 1.4 全局块作用域绑定

let 和 const 相比 var，另外一个区别是它们在全局作用域中的行为。当 var 被用于全局作用域时，它会创建一个新的全局变量作为全局对象（浏览器环境中的 window 对象）的属性。这意味着用 var 很可能会无意中覆盖一个已经存在的全局变量。

如果在全局作用域中使用 let 或 const，会在全局作用域下创建一个新的绑定，但该绑定不会添加为全局对象的属性。换句话说，用 let 或 const 不能覆盖全局变量，而只能屏蔽它。

```javascript
// in a browser
let RegExp = "Hello!";
console.log(RegExp); // "Hello!"
console.log(window.RegExp === RegExp); // false

const ncz = "Hi!";
console.log(ncz); // "Hi!"
console.log("ncz" in window); // false
```

## 1.5 块级绑定最佳实践的进化

当更多的开发者迁移到 ECMAScript 6 后，一种做法日益普及：默认使用 const，只有确实需要改变变量的值时使用 let 。因为大部分变量的值在初始化后不应再改变，而预料外的变量值的改变是很多 bug 的源头。

# 第 2 章 字符串和正则表达式

字符串可以说是编程时最重要的数据类型之一，几乎在每一门高级语言中都有它的存在，只有熟练掌握字符串的操作才能创建有用的程序。

## 2.1 更好的 Unicode 支持

在 ES6 出现以前，JavaScript 字符串一直基于 16 位字符编码（UTF-16）进行构建。每 16 位的序列是一个编码单元，代表一个字符。length、`charAt()` 等字符串属性和方法都是基于这种编码单元构造的。

ES6 新增加了完全支持 UTF-16 的`codePointAt()` 方法，这个方法接受编码单元的位置而非字符位置作为参数，返回与字符串中给定位置对应的码位，即一个整数值。

## 2.2 其他字符串变更

JavaScript 字符串特性的更新总是延后于其他语言中的相同特性，例如，直到 ES5 才为字符串添加了`trim()`方法，而在 ES6 中继续扩展了 JavaScript 解析字符串的能力。

字符串中的子串识别。自 JavaScript 首次被使用以来，开发者就开始使用`indexOf()`方法来在一段字符串中检测另一段子字符串，在 ES6 中，提供了一下 3 个类似的方法可以达到相同效果。

- `includes()`方法。如果在字符串中检测到指定文本则返回 true，否则返回 false。
- `startsWith()`方法。如果在字符串的起始部分检测到指定文本则返回 true，否则返回 false。
- `endsWith()`方法。如果在字符串的结束部分检测到指定文本则返回 true，否则返回 false。

以上的 3 个方法都接受两个参数：第一个参数指定要搜索的文本；第二个参数时可选的，指定一个开始搜索的位置的索引值。实际上，指定第二个参数会大大减少字符串被搜索的范围。

```JavaScript
var msg = "Hello world!";

console.log(msg.startsWith("Hello"));       // true
console.log(msg.endsWith("!"));             // true
console.log(msg.includes("o"));             // true

console.log(msg.startsWith("o"));           // false
console.log(msg.endsWith("world!"));        // true
console.log(msg.includes("x"));             // false

console.log(msg.startsWith("o", 4));        // true
console.log(msg.endsWith("o", 8));          // true
console.log(msg.includes("o", 8));          // false
```

尽管这 3 个方法执行后返回的都是布尔值，也极大地简化了子串匹配的方法，但是如果需要在一个字符串中寻找另一个字符串的实际位置，还需使用`index()`方法或`lastIndexOf()`方法

`repeat()`方法。ES6 还为字符串增添了一个`repeat()`方法，其接受一个 number 类型的参数，表示该字符串的重复次数，返回值是当前字符串重复一定次数后的新字符串。

```JavaScript
console.log("x".repeat(3));         // "xxx"
console.log("hello".repeat(2));     // "hellohello"
console.log("abc".repeat(4));       // "abcabcabcabc"

// indent using a specified number of spaces
var indent = " ".repeat(4),
    indentLevel = 0;

// whenever you increase the indent
var newIndent = indent.repeat(++indentLevel);
```

## 2.3 其他正则表达式语法变更

正则表达式 y 修饰符。它会影响正则表达式搜索过程中的 sticky 属性，当在字符串中开始字符匹配时，它会通知搜索从正则表达式的 lastIndex 属性开始进行，如果在指定位置没能成功匹配，则停止继续匹配。

正则表达式的赋值。在 ES5 中，可以通过给 RegExp 构造函数传递正则表达式作为参数来复制这个正则表达式。如果在 ES5 环境中给 RegExp 构造函数提供第二个参数，为正则表达式指定一个修饰符，则代码无法运行。ES6 修改了这个行为，即使第一个参数为正则表达式，也可以通过第二个参数修改其修饰符。

```JavaScript
var re1 = /ab/i,

    // throws an error in ES5, okay in ES6
    re2 = new RegExp(re1, "g");


console.log(re1.toString());            // "/ab/i"
console.log(re2.toString());            // "/ab/g"

console.log(re1.test("ab"));            // true
console.log(re2.test("ab"));            // true

console.log(re1.test("AB"));            // true
console.log(re2.test("AB"));            // false
```

flags 属性。为了使获取修饰符的过程更加简单，ES6 新增了 flags 属性，它与 source 属性都是只读的原型属性访问器，对其只定义了`getter()`方法，这极大地简化了调试和编写继承代码的复杂度。

```JavaScript
function getFlags(re) {
    var text = re.toString();
    return text.substring(text.lastIndexOf("/") + 1, text.length);
}

// toString() is "/ab/g"
var re = /ab/g;

console.log(getFlags(re));          // "g"


// ES6
var re = /ab/g;

console.log(re.source);     // "ab"
console.log(re.flags);      // "g"
```

## 2.4 模板字面量

事实上，ES5 中一直缺少许多特性，而 ES6 通过模板字面量的方式进行了填补。

- 多行字符串。一个正式的多行字符串的概念。
- 基本的字符串格式化。将变量的值嵌入字符串的能力。
- HTML 转义。向 HTML 插入经过安全转换后的字符串的能力。

基础语法。模板字面量最简单的用法，看起来好像只是用反撇号（`）替换了单、双引号。在模板字面量中，不需要转义单、双引号，单需要转义反撇号。

```JavaScript
let message = `Hello world!`;

console.log(message);               // "Hello world!"
console.log(typeof message);        // "string"
console.log(message.length);        // 12
```

多行字符串。自 JavaScript 诞生起，开发者们一直在寻找一种创建多行字符串的方式。但如果使用单、双引号，字符串一定要在同一行才行。但一直存在一个语法 bug，在一个新行最前方添加反斜杠（\）可以承接上一行的代码，因此可以利用这个 bug 来创造多行字符串。

```JavaScript
var message = "Multiline \
string";

console.log(message);       // "Multiline string"
```

当通过这种方式把字符串打印到控制台时其并未按照跨行方式显示，因为反斜杠在此处代表行的延续，而非真正代表新的一行。如果想输出为新的一行，需要手动加入换行符。在所有主流的 JavaScript 引擎中，变量 message 的内容被打印在两个独立的行中，不过这个行为被视为引擎实现的 bug，很多开发者建议避免使用这种方法。

```JavaScript
var message = "Multiline \n\
string";

console.log(message);       // "Multiline
                            //  string"
```

在 ES6 之前的版本中，通常都依靠数组或字符串拼接的方法来创建多行字符串。

```JavaScript
var message = [
    "Multiline ",
    "string"
].join("\n");

let message = "Multiline \n" +
    "string";
```

ES 6 的模板字面量的语法简单，如果想要在字符串中添加新的一行，只需在代码中直接换行，此处的换行将同步出现在结果中。同时，在反撇号中的所有空白符都属于字符串的一部分，所以千万要小心缩进。

```JavaScript
let message = `Multiline
string`;

console.log(message);           // "Multiline
                                //  string"
console.log(message.length);    // 16
```

如果一定要通过适当的缩进来对齐文本，则可以考虑在多行模板字面量的第一行留白，并在后面的几行中缩进。HTML 标签缩进正确，且可以通过调用`trim()`方法移除最初的空行。

```JavaScript
let html = `
<div>
    <h1>Title</h1>
</div>`.trim();
```

字符串占位符。模板字面量和字符串的真正区别在于模板字面量中的占位符功能。在一个模板字面量中，可以把任何合法的 JavaScript 表达式嵌入到占位符中并将其作为字符串的一部分输出到结果中。占位符由一个左侧的`$(`和右侧的`)`符号组成，中间可以包含任意的 JavaScript 表达式。

```JavaScript
let count = 10,
    price = 0.25,
    message = `${count} items cost $${(count * price).toFixed(2)}.`;

console.log(message);       // "10 items cost $2.50."
```

同时，模板字面量本身也是 JavaScript 表达式，所以可以在一个模板字面量里嵌入另外一个。

```JavaScript
let name = "Nicholas",
    message = `Hello, ${
        `my name is ${ name }`
    }.`;

console.log(message);        // "Hello, my name is Nicholas."
```

标签模板。每个模板标签都可以执行模板字面量上的转换并返回最终的字符串值。标签指的是在模板字面量第一个反撇号前方标注的字符串。

```JavaScript
let message = tag`Hello world`;
```

定义标签。标签可以是一个函数，调用时传入加工过的模板字面量各部分数据，但必须结合每个部分来创建结果。第一个参数是数组，包含 JavaScript 解释过后的字面量字符串，它之后的所有参数都是每一个占位符的解释值。标签函数通常使用不定参数特性来定义占位符，从而简化数据处理的过程。

```JavaScript
function passthru(literals, ...substitutions) {
    let result = "";

    // run the loop only for the substitution count
    for (let i = 0; i < substitutions.length; i++) {
        result += literals[i];
        result += substitutions[i];
    }

    // add the last literal
    result += literals[literals.length - 1];

    return result;
}

let count = 10,
    price = 0.25,
    message = passthru`${count} items cost $${(count * price).toFixed(2)}.`;

console.log(message);       // "10 items cost $2.50."
```

在模板字面量中使用原始值。模板标签同样可以访问原生字符串信息，也就是说通过模板标签可以访问到字符转义被转换成等价字符前的原生字符串。最简单的例子是使用内建的`String.raw()`标签。原生字符串信息同样被传入模板标签，标签函数的第一个参数是一个数组，它有一个额外的属性 raw，是一个包含每一个字面值的原生等价信息的数组。

```Javascript
let message1 = `Multiline\nstring`,
    message2 = String.raw`Multiline\nstring`;

console.log(message1);          // "Multiline
                                //  string"
console.log(message2);          // "Multiline\\nstring"
```

# 第 3 章 函数

## 3.1 函数形参的默认值

JavaScript 函数有一个特别的地方，无论在函数定义中声明了多少形参，都可以传入任意数量的参数。这可以在定义函数时添加针对不同参数的处理逻辑，当已定义的形参无对应的传入参数时为其指定一个默认值。

在 ES5 中模拟默认参数。对于函数的命名参数，如果不显式传值，则其默认值为 undefined。因此我们经常使用逻辑或操作符为缺失的参数提供默认值。在 ECMAScript 5 和早期版本中，可以通过以下模式创建函数并未参数赋予默认值。然而这种方法也有缺陷，如果我们想给函数的形参传入值 0，即使这个值是合法的，也会被视为一个 false 值。在这种情况下，更安全的选择是通过 typeof 检查参数类型。

```javascript
function makeRequest(url, timeout, callback) {
  timeout = timeout || 2000;
  callback = callback || function () {};
  // the rest of the function
}

function makeRequest(url, timeout, callback) {
  timeout = typeof timeout !== "undefined" ? timeout : 2000;
  callback = typeof callback !== "undefined" ? callback : function () {};
  // the rest of the function
}
```

ECMAScript 6 中的默认参数值。ES6 简化了为形参提供默认值的过程，如果没为参数传入值则为其提供一个初始值，而且不需要添加任何校验值是否缺失的代码，所以函数体会更加地小。对于默认参数值，null 是一个合法值，而如果是 undefined 则会使用默认值。

```javascript
function makeRequest(url, timeout = 2000, callback = function () {}) {
  // the rest of the function
}
```

默认参数值对 arguments 对象的影响。在 ECMAScript 5 非严格模式下，函数命名参数的变化会体现在 arguments 对象中，而在严格模式下，无论参数如何变化，arguments 对象不再随之改变。在 ES6 中，如果一个函数使用了默认参数值，则无论是否显式定义了严格模式，arguments 对象的行为都将与 ES5 严格模式下保持一致。默认参数值的存在使得 arguments 对象保持与命名参数分离。

```javascript
// not in strict mode
function mixArgs(first, second = "b") {
  console.log(arguments.length);
  console.log(first === arguments[0]);
  console.log(second === arguments[1]);
  first = "c";
  second = "d";
  console.log(first === arguments[0]);
  console.log(second === arguments[1]);
}

mixArgs("a");
// 1
// true
// false
// false
// false
```

默认参数表达式。可以通过函数执行来得到默认参数的值，如果不主动传入参数，那么就会调用方法（表达式）来得到正确的默认值。初次解析函数声明时不会调用该方法，只有当调用函数且不传入参数时才会调用。

```javascript
let value = 5;

function getValue() {
  return value++;
}

function add(first, second = getValue()) {
  return first + second;
}

console.log(add(1, 1)); // 2
console.log(add(1)); // 6
console.log(add(1)); // 7
```

正因为默认参数时在函数调用时求值，所以可以使用自定义的参数作为后定义参数的默认值。更进一步，可以将前面的参数传入一个函数来获得后面参数的默认值。但是，在引用参数默认值的时候，只允许引用前面参数的值，即先定义的参数不能访问后定义的参数。

```javascript
function add(first, second = first) {
  return first + second;
}
console.log(add(1, 1)); // 2
console.log(add(1)); // 2

function getValue(value) {
  return value + 5;
}
function add(first, second = getValue(first)) {
  return first + second;
}
console.log(add(1, 1)); // 2
console.log(add(1)); // 7
```

默认参数的临时死区。默认参数也同样有临死死区，在这里的参数不可访问。与 let 声明类似，定义参数时会为每个参数创建一个新的标识符绑定，该绑定在初始化之前不可被引用，如果试图访问会导致程序抛出错误。当调用函数时，会通过传入的值或参数的默认值初始化该参数。

```javascript
function add(first = second, second) {
  return first + second;
}

console.log(add(1, 1)); // 2
console.log(add(undefined, 1)); // throws error

// JavaScript representation of call to add(1, 1)
let first = 1;
let second = 1;

// JavaScript representation of call to add(undefined, 1)
let first = second;
let second = 1;
```

## 3.2 处理无命名参数

JavaScript 的函数语法规定，无论函数已定义的命名参数有多少，都不限制调用时传入的实际参数数量，调用时总是可以传入任意数量的参数。当传入更少的数量的参数时，默认参数值的特性可以有效简化函数声明的代码；当传入更多数量的参数时，ES6 同样也提供了更好的方案。

ES5 中的无命名参数。早先，JavaScript 提供 arguments 对象来检查函数的所有参数，从而不必定义每一个要用的参数。但实际使用起来该对象缺有些笨重。下面的函数返回一个给定对象的副本，包含原始对象属性的特定子集。该函数只定义了一个参数，作为被复制属性的源对象，其他参数为被复制属性的名称。出现的情况，不容易发现这个函数可以接受任意数量的参数，需要从索引 1 而不是索引 0 开始遍历 arguments 对象。

```javascript
function pick(object) {
  let result = Object.create(null);

  // start at the second parameter
  for (let i = 1, len = arguments.length; i < len; i++) {
    result[arguments[i]] = object[arguments[i]];
  }

  return result;
}

let book = {
  title: "Understanding ECMAScript 6",
  author: "Nicholas C. Zakas",
  year: 2015,
};

let bookData = pick(book, "author", "year");

console.log(bookData.author); // "Nicholas C. Zakas"
console.log(bookData.year); // 2015
```

不定参数。在 ES6 中，通过引入不定参数的特性可以解决这些问题。在函数的命名参数前添加三个点（...）就表明这是一个不定参数，该参数为一个数组，包含着自它之后传入的所有参数，通过这个数组名即可逐一访问里面的参数。

```javascript
function pick(object, ...keys) {
  let result = Object.create(null);

  for (let i = 0, len = keys.length; i < len; i++) {
    result[keys[i]] = object[keys[i]];
  }

  return result;
}
```

不定参数有两条使用限制。首先，每个函数最多只能声明一个不定参数，而且一定要放在所有参数的末尾。其次，不定参数不能用于对象字面量 setter 之中。之所以存在这条限制，是因为对象字面量 setter 的参数有且只能有一个，所以在当前上下文不允许使用不定参数。

## 3.3 增强的 Function 构造函数

Function 构造函数时 JavaScript 语法中很少被用到的一部分，通常我们由它来动态创建新的函数。这种构造函数接受字符串形式的参数，分别为函数的参数及函数体。

ES6 增强了 Function 构造函数的功能，支持在创建函数时定义默认参数和不定参数。唯一需要做的是在参数名后添加一个等号及一个默认值。对于 Function 构造函数，新增的默认参数和不定参数这两个特性使其具备了与声明式创建函数相同的能力。

## 3.4 展开运算符

展开运算符可以让你指定一个数组，将它们打算后作为各自独立的参数传入函数。

JavaScript 内建的 Math.max() 方法可以接受任意数量的参数并返回值最大的哪一个，如果希望从数组中挑选出最大的值则不能直接用该方法，需要手动遍历数组或使用 apply() 方法。

```javascript
let values = [25, 50, 75, 100];

console.log(Math.max.apply(Math, values)); // 100
```

使用 ES6 的展开运算符可以简化上述示例，向 Math.max() 方法传入一个数组，再在数组前添加不定参数中使用`...`符号，就无须再调用 apply() 方法了。JavaScript 引擎读取这段程序后悔将参数数组分割为各自独立的参数并依次传入。

```javascript
let values = [25, 50, 75, 100];

// equivalent to
// console.log(Math.max(25, 50, 75, 100));
console.log(Math.max(...values)); // 100
```

可以将展开运算符与其他正常传入的参数混合使用。假设想限定返回的最小值为 0，防止负数偷偷溜进数组中，可以单独传入限定值。

```javascript
let values = [-25, -50, -75, -100];

console.log(Math.max(...values, 0)); // 0
```

## 3.5 name 属性

ES6 程序中所有的函数的 name 属性都有一个合适的值，一般对应着生命是的函数名称或该匿名函数的变量的名称。

```javascript
function doSomething() {
  // ...
}

var doAnotherThing = function () {
  // ...
};

console.log(doSomething.name); // "doSomething"
console.log(doAnotherThing.name); // "doAnotherThing"
```

ES6 做了更多的改进来确保所有函数都有适合的名称。另外还有两个有关函数名称的特例，通过 `bind()` 函数创建的函数，其名称将带有“bound”前缀，通过 Function 构造函数创建的函数，其名称将带有前缀“anonymous”。

```javascript
var doSomething = function doSomethingElse() {
  // ...
};

var person = {
  get firstName() {
    return "Nicholas";
  },
  sayName: function () {
    console.log(this.name);
  },
};

console.log(doSomething.name); // "doSomethingElse"
console.log(person.sayName.name); // "sayName"

var descriptor = Object.getOwnPropertyDescriptor(person, "firstName");
console.log(descriptor.get.name); // "get firstName"
```

切记，函数 name 属性的值不一定引用同名变量，它只是协助调试用的额外信息，所以不能使用 name 属性的值来获取对于函数的引用。

## 3.6 明确函数的多重用途

ES5 及早期版本中的函数具有多重功能，可以结合 new 使用，函数内的 this 值将指向一个新对象，函数最终会返回这个新对象。

```java
function Person(name) {
    this.name = name;
}

var person = new Person("Nicholas");
var notAPerson = Person("Nicholas");

console.log(person);        // "[Object object]"
console.log(notAPerson);    // "undefined"
```

JavaScript 函数有两个不同的内部方法：`[[Call]]`和`[[Construct]]`。当通过 new 关键字调用函数时，执行的是`[[Construct]]`函数，它负责创建一个通常被称作实例的新对象，然后再执行函数体，将 this 绑定到实例上；如果不通过 new 关键字调用函数，则执行`[[Call]]`函数，从而直接执行代码中的函数体。具有`[[Construct]]`方法的函数被统称为构造函数。

切记，不说所有函数都有`[[Construct]]`方法，因此不是所有函数都可以通过 new 来调用，比如箭头函数就没有这个方法。

在 ES5 中，如果想确定一个函数是否通过 new 关键字被调用，或者是判断该函数是否作为构造函数被调用，最流行的方式时使用 instanceof。

```javascript
function Person(name) {
  if (this instanceof Person) {
    this.name = name; // using new
  } else {
    throw new Error("You must use new with Person.");
  }
}

var person = new Person("Nicholas");
var notAPerson = Person("Nicholas"); // throws error

var notAPerson = Person.call(person, "Michael"); // works!
```

为了解决判断函数是否通过 new 关键字调用的问题，ES6 引入了 new.target 这个元属性。元属性是指非对象的属性，其可以提供非对象目标的补充信息。当调用函数的`[[Construct]]`方法时，new.target 被赋值为 new 操作符的目标，通常是新创建对象实例，也就是函数体内的 this 的构造函数；如果调用`[[Call]]`方法，则 new.target 的值为 undefined。

有了这个元属性，可以通过检查 new.target 是否被定义过来安全第检测一个函数是否通过 new 关键字调用。

```javascript
function Person(name) {
  if (typeof new.target !== "undefined") {
    this.name = name; // using new
  } else {
    throw new Error("You must use new with Person.");
  }
}

var person = new Person("Nicholas");
var notAPerson = Person.call(person, "Michael"); // error!
```

## 3.7 块级函数

在 ES3 和早期版本中，在代码块中声明一个块级函数严格来说是一个语法错误，但是所有的浏览器仍然支持这个特性，但兼容程度不一样。为了遏制这种互相不兼容的行为，ES5 的严格模式引入一个错误提示，当在代码块内部声明函数时程序会抛出错误。

```javascript
"use strict";

if (true) {
  // Throws a syntax error in ES5, not so in ES6
  function doSomething() {
    // ...
  }
}
```

在 ES6 中，会将函数视为一个块级声明，从而可以在定义该函数的代码块内访问和调用它。

```javascript
"use strict";

if (true) {
  console.log(typeof doSomething); // "function"

  function doSomething() {
    // ...
  }

  doSomething();
}

console.log(typeof doSomething); // "undefined"
```

块级函数与 let 函数表达式类似，一旦执行过程流出了代码块，函数定义立即被移除。二者的却别是，在该代码块中，块级函数会被提升至块的顶部，而用 let 定义的函数表达式不会被提升。

```javascript
"use strict";

if (true) {
  console.log(typeof doSomething); // throws error

  let doSomething = function () {
    // ...
  };

  doSomething();
}

console.log(typeof doSomething); // undefined
```

非严格模式下的块级函数。在 ES6 中，即使处于非严格模式下，也可以声明块级函数，但其行为与严格模式下稍有不同。这些函数不再提升至代码块的顶部，而是提升至外围函数或全局作用域的顶部。

```javascript
// ECMAScript 6 behavior
if (true) {
  console.log(typeof doSomething); // "function"

  function doSomething() {
    // ...
  }

  doSomething();
}

console.log(typeof doSomething); // "function"
```

## 3.8 箭头函数

箭头函数时一种使用箭头（=>）定义函数的新语法，它与传统的 JavaScript 函数有些许不同，主要集中在以下方面：

- 没有 this、super、argumetns 和 new.target 绑定
- 不能通过 new 关键字调用
- 没有原型，即不存在 prototype 这个属性
- 不可以改变 this 的绑定
- 不支持 arguments 对象
- 不支持重复的命名参数

箭头函数的语法多变，根据实际的使用场景有多重形式。所有变种都由函数参数、箭头、函数体组成，根据使用的需要，参数和函数体可以分别采取多种不同的形式。

当箭头函数只有一个参数时，可以直接写参数名，箭头紧随其后，箭头右侧的表达式被求值后便立即返回。即使没有显式的返回语句，这个箭头函数也可以返回传入的第一个参数，不需要更多的语法铺垫。

```javascript
var reflect = (value) => value;

// effectively equivalent to:

var reflect = function (value) {
  return value;
};
```

如果要传入两个或两个以上的参数，要在参数的两侧添加一堆小括号。

```javascript
var sum = (num1, num2) => num1 + num2;

// effectively equivalent to:

var sum = function (num1, num2) {
  return num1 + num2;
};
```

如果函数没有参数，也要在声明的时候写一组没有内容的小括号。

```javascript
var getName = () => "Nicholas";

// effectively equivalent to:

var getName = function () {
  return "Nicholas";
};
```

如果希望为函数编写由多个表达式组成的更传统的函数体，那么需要用花括号包括函数体，并显式定义一个返回值。

```javascript
var sum = (num1, num2) => {
  return num1 + num2;
};

// effectively equivalent to:

var sum = function (num1, num2) {
  return num1 + num2;
};
```

如果想要创建一个空函数，需要写一堆没有内容的花括号。或括号代表函数体的部分。

```javascript
var doNothing = () => {};

// effectively equivalent to:

var doNothing = function () {};
```

如果想要在箭头函数外返回一个对象字面量，则需要将该字面量包括在小括号里。

```javascript
var getTempItem = (id) => ({ id: id, name: "Temp" });

// effectively equivalent to:

var getTempItem = function (id) {
  return {
    id: id,
    name: "Temp",
  };
};
```

创建立即执行函数表达式。JavaScript 函数的一个流行的使用方式时创建立即执行函数表达式（IIFE），可以定义一个匿名函数并立即调用，自始至终不保存对该函数的引用。当希望创建一个与其他程序隔离的作用域时，这种模式非常方便。

```javascript
let person = (function (name) {
  return {
    getName: function () {
      return name;
    },
  };
})("Nicholas");

console.log(person.getName()); // "Nicholas"
```

在代码中立即执行函数表达式通过 `getName()` 方法创建了一个新对象，将参数 name 作为该对象的一个私有成员返回给函数的调用者。只要将箭头函数包裹在小括号里，就可以用它实现相同的功能。注意，小括号只包括箭头函数定义，没有包含（“Nicholas”），这一点与正常函数有所不同，由正产函数定义的立即执行函数表达式既可以用小括号包括函数体，也可以额外包裹函数调用的部分。

```javascript
let person = ((name) => {
  return {
    getName: function () {
      return name;
    },
  };
})("Nicholas");

console.log(person.getName()); // "Nicholas"
```

箭头函数没有 this 绑定。函数内的 this 绑定时 JavaScript 中最常出现错误的因素，函数内的 this 值可以根据函数调用上下文而改变，这有可能错误地影响其他对象。

```javascript
var PageHandler = {
  id: "123456",

  init: function () {
    document.addEventListener(
      "click",
      function (event) {
        this.doSomething(event.type); // error
      },
      false
    );
  },

  doSomething: function (type) {
    console.log("Handling " + type + " for " + this.id);
  },
};
```

可以使用 `bind()` 方法显式地将 this 绑定到 PageHandler 函数上来修正这个问题。

```javascript
var PageHandler = {
  id: "123456",

  init: function () {
    document.addEventListener(
      "click",
      function (event) {
        this.doSomething(event.type); // no error
      }.bind(this),
      false
    );
  },

  doSomething: function (type) {
    console.log("Handling " + type + " for " + this.id);
  },
};
```

但是调用 `bind(this)` 后事实上创建了一个额外的函数，可以通过一个更好的方式来修正这段代码，使用箭头函数。箭头函数没有 this 绑定，必须通过查找作用域链来决定其值。如果箭头函数被非箭头函数包含，则 this 绑定的是最近一层非箭头函数的 this；否则，this 的值会被设置为 undefined。

```javascript
var PageHandler = {
  id: "123456",

  init: function () {
    document.addEventListener(
      "click",
      (event) => this.doSomething(event.type),
      false
    );
  },

  doSomething: function (type) {
    console.log("Handling " + type + " for " + this.id);
  },
};
```

箭头函数缺少正常函数所拥有的 prototype 属性，它的设计初衷是“即用即弃”，所以不能用它来定义新的类型。如果尝试通过 new 关键字调用一个箭头函数，会导致程序抛出错误。同时，箭头函数中的 this 值取决于该函数外部非箭头函数的 this 值，且不能通过 call()、apply() 或 bind() 方法来改变 this 的值。

箭头函数和数组。箭头函数的语法简洁，非常适用于数组处理。

```javascript
var result = values.sort(function (a, b) {
  return a - b;
});

var result = values.sort((a, b) => a - b);
```

箭头函数没有 arguments 绑定。箭头函数没有自己的 arguments 对象，且未来无论函数在哪个上下文中执行，箭头函数始终可以访问外围函数的 arguments 对象。

```javascript
function createArrowFunctionReturningFirstArg() {
  return () => arguments[0];
}

var arrowFunction = createArrowFunctionReturningFirstArg(5);

console.log(arrowFunction()); // 5
```

箭头函数的辨识方法。尽管箭头函数与传统函数的语法不同，但它同样可以被识别出来。

```javascript
var comparator = (a, b) => a - b;

console.log(typeof comparator); // "function"
console.log(comparator instanceof Function); // true
```

同样，仍然可以在箭头函数上调用 call()、apply() 及 bind() 方法，但与其他函数不同的是，箭头函数的 this 值不会受这些方法的影响。

## 3.9 尾调用优化

尾调用指的是函数作为另一个函数的最后一条语句被调用。在 ES5 的引擎中，尾调用的实现与其他函数调用的实现类似：创建一个新的栈帧，将其推入栈来表示函数调用。也就是说，在循环调用中，每一个未用完的栈帧都会被保存在内存中，当调用栈变得过大时会造成程序问题。

ES6 缩减了严格模式下尾调用栈的大小，在非严格模式下不受影响，如果满足以下条件，尾调用不再创建新的栈帧，而是清除并重用当前栈帧。

- 尾调用不访问当前栈帧的变量，也就是说函数不是一个闭包
- 在函数内部，尾调用是最后一条语句
- 尾调用的结果作为函数值返回

实际上，尾调用的优化发生在引擎背后，除非尝试优化一个函数，否则无需思考此类问题。递归函数时其最主要的应用场景，此时尾调用优化的结果最显著。

```javascript
function factorial(n) {
  if (n <= 1) {
    return 1;
  } else {
    // not optimized - must multiply after returning
    return n * factorial(n - 1);
  }
}
```

```javascript
function factorial(n, p = 1) {
  if (n <= 1) {
    return 1 * p;
  } else {
    let result = n * p;

    // optimized
    return factorial(n - 1, result);
  }
}
```

# 第 4 章 扩展对象的功能性

ECMAScript 6 通过多种方式来加强对象的使用，通过简单的语法扩展，提供了更多操作对象及对象交互的方法。

## 4.1 对象类别

ES 6 规范清晰定义了每一个类别的对象。

- 普通对象：具有 JavaScript 对象所有的默认内部行为。
- 特异对象：具有某些与默认行为不符的内部行为。
- 标准对象：ES6 规范中定义的对象，例如 Array、Data 等。标准对象既可以是普通对象，也可以是特异对象。
- 内建对象：脚本开始执行时存在于 JavaScript 执行环境中的对象，所有标准对象都是内建对象。

## 4.2 对象字面量语法扩展

对象字面量让我们创建对象不再需要编写冗余的代码，直接通过它简洁的语法就可以实现。而在 ES6 中，通过下面的几种语法，让对象字面量变得更强大、更简洁。

### 4.2.1 属性初始值的简写。

在 ECMAScript 5 及更早版本中，对象字面量只是简单的键值对集合，这意味着初始化属性值时会有一些重复。在 ES6 中，通过使用属性初始化的简写语法，可以消除属性名称与局部变量之间的重复书写。当一个对象的属性与本地变量同名时，不必再写冒号和值，简单地只写属性名即可。这种简写方法有助于消除命名错误。

```javascript
function createPerson(name, age) {
  return {
    name, // name: name,
    age, // age: age
  };
}
```

### 4.2.2 对象方法的简写语法。

在 ES5 及早期版本中，如果为对象添加方法，必须通过指定名称并完整定义函数来实现。而在 ES6 中，消除了冒号和 function 关键字。在对象中创建一个方法，该属性被赋值为一个匿名函数表达式，它拥有在 ES5 中定义的对象方法所具有的的全部特性。二者唯一的区别是，简写方法可以使用 super 关键字。

通过对象方法简写语法创建的方法有一个 name 属性，其值为小括号前的名称，在上述示例中，person.sayName() 方法的 name 属性的值为“sayName”。

```javascript
var person = {
  name: "Nicholas",
  // sayName: function() {
  //     console.log(this.name);
  // }
  sayName() {
    console.log(this.name);
  },
};
```

### 4.2.3 可计算属性名。

在 ES5 及早期版本的对象实例中，如果想要通过计算得到属性名，就需要用方括号代替点记法。方括号允许使用变量或包含字符串的字面量来指定属性名，虽然如果字面量作为标识符有语法错误。

```javascript
var person = {},
  lastName = "last name";

person["first name"] = "Nicholas"; // 字符串
person[lastName] = "Zakas"; // 变量

console.log(person["first name"]); // "Nicholas"
console.log(person[lastName]); // "Zakas"
```

此外，在对象字面量中，可以直接使用字符串字面量作为属性名称。这种模式适用于属性名提前已知或可被字符串字面量表示的情况。  
如果属性名称被包含在一个变量中，或者需要通过计算才能得到该变量的值，那么在 ECMAScript 5 中是无法为一个对象字面量定义该属性的。而在 ES6 中，可在对象字面量中使用可计算属性名称，其语法与引用对象实例的可计算属性名称相同，也是使用方括号。

```javascript
var person = {
  "first name": "Nicholas",
};

console.log(person["first name"]); // "Nicholas"

// ES6 新增
var suffix = " name";
var person = {
  ["first" + suffix]: "Nicholas",
  ["last" + suffix]: "Zakas",
};
console.log(person["first name"]); // "Nicholas"
console.log(person["last name"]); // "Zakas"
```

## 4.3 新增方法

从 ES5 开始，避免创建新的全局方法和在 Object.prototype 上创建新的方法。当开发者想向标准添加新方法时，他们会找一个适当的现有对象，让这些方法可用。结果，当没有其他合适的对象时，全局 Object 对象会收到越来越多的对象方法。而在 ES6 中，为了使某些任务更易完成，在全局 Object 对象上引入了一些新方法。

### 4.3.1 Object.is()方法

ES 6 引入了 Object.is() 方法来弥补全等运算符的不准确运算。这个方法接受两个参数，如果这两个参数类型相同且具有相同的值，则返回 true。

```js
console.log(+0 == -0); // true
console.log(+0 === -0); // true
console.log(Object.is(+0, -0)); // false

console.log(NaN == NaN); // false
console.log(NaN === NaN); // false
console.log(Object.is(NaN, NaN)); // true

console.log(5 == 5); // true
console.log(5 == "5"); // true
console.log(5 === 5); // true
console.log(5 === "5"); // false
console.log(Object.is(5, 5)); // true
console.log(Object.is(5, "5")); // false
```

### 4.3.2 Object.assign()方法

混合（Mixin）是 JavaScript 中实现对象组合最流行的一种模式。在一个 mixin 方法中，一个对象接收来自另一个对象的属性和方法，许多 JavaScript 库中都有类似的 mixin 方法。

```js
function mixin(receiver, supplier) {
  Object.keys(supplier).forEach(function (key) {
    receiver[key] = supplier[key];
  });

  return receiver;
}
```

这种混合模式非常流行，因而 ECMAScript 6 添加了 `Object.assign()` 方法来实现相同的功能，这个方法接受一个接收对象和任意数量的源对象，最终返回接收对象。`mixin()` 方法使用赋值操作符（assignment operator） `=`来复制相关属性，却不能复制访问器属性到接收对象中，因此最终添加的方法弃用 mixin 而改用 assign 作为方法名 。

`Object.assign()`方法可以接受任意数量的源对象，并按指定的顺序将属性复制到接收对象中。所以如果多个源对象具有同名属性，则排位靠后的源对象会覆盖排位靠前的。

```js
var receiver = {};

Object.assign(
  receiver,
  {
    type: "js",
    name: "file.js",
  },
  {
    type: "css",
  }
);

console.log(receiver.type); // "css"
console.log(receiver.name); // "file.js"
```

## 4.4 重复的对象字面量属性

ES5 严格模式中加入了对象字面量重复属性的校验，当同时存在多个同名属性时会抛出错误。但是在 ES6 中重复校验检查被移除了，无论是在严格模式还是非严格模式下，代码不再检查重复属性，对于每一组重复属性，都会选取最后一个取值。

```javascript
"use strict";

var person = {
  name: "Nicholas",
  name: "Greg", // no error in ES6 strict mode
};

console.log(person.name); // "Greg"
```

## 4.5 自由属性枚举顺序

ES5 中未定义对象属性的枚举顺序，由 JavaScript 引擎厂商自行决定。然而，ES6 严格规定了对象的自由属性被枚举时的返回顺序，这回影响到 `Object.getOwnPropertyNames()` 方法及 `Reflect.ownKeys` 返回属性的方式，`Object.assign()` 方法处理属性的顺序也将随之改变。

自有属性枚举顺序的基本规则是：

- 所有数字键按升序排序。
- 所有字符串建按照它们被加入对象的顺序排序。
- 所有 symbol 键按照它们被加入对象的顺序排序。

```js
var obj = {
  a: 1,
  0: 1,
  c: 1,
  2: 1,
  b: 1,
  1: 1,
};

obj.d = 1;

console.log(Object.getOwnPropertyNames(obj).join("")); // "012acbd"
```

对于 for-in 循环，由于并非所有厂商都遵循相同的实现方式，因此仍未指定一个明确的枚举顺序；而 `Object. keys()` 方法和 `JSON. stringify()` 方法都指明与 for-in 使用相同的枚举顺序，因此它们的枚举顺序目前也不明晰。

4.6 增强对象原型

4.7 正式的方法定义

# 第 5 章 解构：使数据访问更便捷

对象和数组字面量是 JavaScript 中两种最常用的数据解构，由于 JSON 数据格式的普及，二者已经成为语言中特别重要的一部分。在编码过程中，我们经常定义许多对象和数组，然后有组织第从中提取相关的信息片段。ES6 添加了可以简化这种任务的新特性：解构。解构是一种打破数据解构，将其拆分为更小部分的过程。

## 5.1 为何使用解构功能

在 ES5 及早期版本中，开发者为了从对象和数组中获取特定数据并赋值给变量，编写了很多看起来同质化的代码。想象一下，如果要提取更多变量，则必须依次编写类似的代码来为变量赋值，如果其中还包含嵌套结构，只靠遍历是找不到真实信息的，必须要深入挖掘整个数据解构才能找到所需数据。

```javascript
let options = {
  repeat: true,
  save: false,
};

// extract data from the object
let repeat = options.repeat,
  save = options.save;
```

所以 ES6 为对象和数组都添加了解构功能，将数据解构打散的过程变得更加简单，可以从打散后更小的部分中获取所需信息。许多语言都通过较少量的语法实现了解构功能，以简化获取信息的过程；而 ES6 中的实现实际上利用早已熟悉的语法：对象和数组字面量语法。

## 5.2 对象解构

对象字面量的语法形式是，在一个赋值操作符左边放置一个对象字面量。type、name 都是局部声明的变量，也是用来从 oprions 对象读取相应值的属性名称。

```javascript
let node = {
  type: "Identifier",
  name: "foo",
};

let { type, name } = node;

console.log(type); // "Identifier"
console.log(name); // "foo"
```

如果使用 var、let 或 const 解构声明变量，则必须要提供初始化程序（也就是等号右侧的值），否则会导致程序抛出语法错误。

### 5.2.1 解构赋值

可以将对象解构应用到变量的声明中，也同样可以在给变量赋值时使用解构语法。注意的是，一定要用一对小括号包裹解构赋值语句，JavaScript 引擎将一对开放的花括号视为一个代码块，而语法规定，代码块语句不允许出现在赋值语句左侧，添加小括号后可以将块语句转换为一个表达式，从而实现整个解构赋值的过程。

```javascript
let node = {
    type: "Identifier",
    name: "foo",
  },
  type = "Literal",
  name = 5;

// assign different values using destructuring
({ type, name } = node);

console.log(type); // "Identifier"
console.log(name); // "foo"
```

解构赋值表达式的值与表达式右侧的值相等，如此一来，在任何可以使用值的地方都可以使用解构赋值表达式。但是注意的是，解构赋值表达式如果为 null 或 undefined 会导致程序抛出错误。也就是说，任何尝试读取 null 或 undefined 的属性的行为都会触发运行时错误。

```javascript
let node = {
    type: "Identifier",
    name: "foo",
  },
  type = "Literal",
  name = 5;

function outputInfo(value) {
  console.log(value === node); // true
}

outputInfo(({ type, name } = node));

console.log(type); // "Identifier"
console.log(name); // "foo"
```

### 5.2.2 默认值。

使用解构赋值表达式时，如果指定的局部变量名称在对象中不存在，那么这个局部变量会被赋值为 undefined。但是当指定的属性不存在时，可以随意定义一个默认值，在属性名称或添加一个等号（=）和相应的默认值即可。

```javascript
let node = {
  type: "Identifier",
  name: "foo",
};

let { type, name, value, value1 = true } = node;

console.log(type); // "Identifier"
console.log(name); // "foo"
console.log(value); // undefined
console.log(value1); // true
```

### 5.2.3 为非同名局部变量赋值。

如果希望使用不同命名的局部变量来存储对象属性的值，ES6 中的一个扩展语法可以满足需求，这个语法与完整的对象字面量属性初始化程序很像。这种语法实际上与传统对象字面量的语法相悖，原来的语法名称在冒号左边，值在右边；现在语法名称在冒号右边，而读取的对象值在左边。当使用其他变量名进行赋值时也可以添加默认值，只需在变量名后添加等号和默认值即可。

```javascript
let node = {
  type: "Identifier",
};

let { type: localType, name: localName = "bar" } = node;

console.log(localType); // "Identifier"
console.log(localName); // "bar"
```

### 5.2.4 嵌套对象解构。

解构嵌套对象仍然与对象字面量的语法相似，可以将对象拆解以获取想要的信息。在下面的解构中，所有冒号前的标识符都代表在对象中的检索位置，其右侧为被赋值的变量名；如果冒号后是花括号，则意味着要赋予的最终值嵌套在对象内部更深的层级中。

```javascript
let node = {
  type: "Identifier",
  name: "foo",
  loc: {
    start: {
      line: 1,
      column: 1,
    },
    end: {
      line: 1,
      column: 4,
    },
  },
};

let {
  loc: { start },
} = node;

console.log(start.line); // 1
console.log(start.column); // 1
```

更进一步，也可以使用一个与对象属性名不同的局部变量名。

```javascript
let node = {
  type: "Identifier",
  name: "foo",
  loc: {
    start: {
      line: 1,
      column: 1,
    },
    end: {
      line: 1,
      column: 4,
    },
  },
};

// extract node.loc.start
let {
  loc: { start: localStart },
} = node;

console.log(localStart.line); // 1
console.log(localStart.column); // 1
```

## 5.3 数组解构

与对象解构的语法相比，数组解构就简单多了，它使用的是数组字面量，且解构操作全部在数组内完成，而不是像对象字面量语法一样使用对象的命名属性。在这个过程中，数组本身不会发生任何变化。

```javascript
let colors = ["red", "green", "blue"];

let [firstColor, secondColor] = colors;

console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

在解构模式中，也可以直接省略元素，只为感兴趣的元素提供变量名。

```javascript
let colors = ["red", "green", "blue"];

let [, , thirdColor] = colors;

console.log(thirdColor); // "blue"
```

解构赋值。数组解构也可用于赋值上下文，但不需要用小括号包裹表达式，这一点与数组解构的约定不同。

```javascript
let colors = ["red", "green", "blue"],
  firstColor = "black",
  secondColor = "purple";

[firstColor, secondColor] = colors;

console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

数组解构还有一个独特的用例：交换两个变量的值，并且不需要额外的变量。右侧是一个为交换过程创建的临时数组字面量。代码执行过程中，先解构临时数组，将 b 和 a 的值赋值到左侧数组的前两个位置，最终结果是变量交换了它们的值。

```javascript
// Swapping variables in ECMAScript 6
let a = 1,
  b = 2;

[a, b] = [b, a];

console.log(a); // 2
console.log(b); // 1
```

默认值。也可以在数组解构赋值表达式中为数组中的任意位置添加默认值，当指定位置的属性不存在或其值为 undefined 时使用默认值。

嵌套数组解构。嵌套数组解构与嵌套对象解构的语法类似，在原有的数组模式中插入另一个数组模式，即可将解构过程深入到下一个层级。

```javascript
let colors = ["red", ["green", "lightgreen"], "blue"];

let [firstColor, [secondColor]] = colors;

console.log(firstColor); // "red"
console.log(secondColor); // "green"
```

不定元素。在数组中，通过通过“...”语法将数组中的其余元素赋值给一个特定的变量。

```javascript
let colors = ["red", "green", "blue"];

let [firstColor, ...restColors] = colors;

console.log(firstColor); // "red"
console.log(restColors.length); // 2
console.log(restColors[0]); // "green"
console.log(restColors[1]); // "blue"
```

不定元素语法有助于从数组中提取特定元素并保证其余元素可用，它还有数组复制的功能。concat() 方法的设计初衷是连接两个数组，如果调用时不传递参数就会返回当前函数的副本。在 ES6 中，可以通过不定元素的语法来实现相同的目标。

```javascript
// cloning an array in ECMAScript 6
let colors = ["red", "green", "blue"];
let [...clonedColors] = colors;

console.log(clonedColors); //"[red,green,blue]"
```

## 5.4 混合解构

可以混合使用对象解构和数组解构来创建更多复杂的表达式，如此一来，可以从任何混杂着对象和数组的数据解构中提取想要的信息。

## 5.5 解构参数

当定义一个接受大量可选参数的 JavaScript 函数时，通常会创建一个可选对象，将额外的参数定义为这个对象的属性。

```javascript
// properties on options represent additional parameters
function setCookie(name, value, options) {
  options = options || {};

  let secure = options.secure,
    path = options.path,
    domain = options.domain,
    expires = options.expires;

  // code to set the cookie
}

// 可以简化为这样
function setCookie(name, value, { secure, path, domain, expires }) {
  // code to set the cookie
}

// third argument maps to options
setCookie("type", "js", {
  secure: true,
  expires: 60000,
});
```

必须传值的结构参数。解构参数有一个奇怪的地方，默认情况下，如果调用函数时不提供被解构的参数会导致程序抛出错误。如果解构赋值表达式的右值为 null 或 undefined，则程序也会报错。如果希望将解构参数定义为可选的，那么久必须为其提供默认值来解决这个问题。也可以为解构参数指定默认值，就像在解构赋值语句中做的那样，只需在参数后添加等号并且指定一个默认值即可。

```javascript
function setCookie(name, value, { secure, path, domain, expires } = {}) {
  // ...
}
```

# 第 6 章 Symbol 和 Symbol 属性

## 6.1 创建 Symbol

## 6.2 Symbol 的使用方法

## 6.3 Symbol 共享体系

## 6.4 Symbol 与类型强制转换

## 6.5 Symbol 属性检索

## 6.6 通过 well-known Symbol 暴露内部操作

### 6.6.1 Symbol.hasInstance 方法

### 6.6.1 Symbol.isConcatSpreadable 属性

### 6.6.1 Symbol.match、Symbol.replace、Symbol.search 和 Symbol.split 属性

### 6.6.1 Symbol.toPrimitive 方法

### 6.6.1 Symbol.toStringTag 属性

### 6.6.1 Symbol.unscopables 属性

# 第 7 章 Set 集合与 Map 集合

## 7.1 ECMAScript 5 中的 Set 集合与 Map 集合

## 7.2 该解决方案的一些问题

## 7.3 ECMAScript 6 中的 Set 集合

### 7.3.1 创建 Set 集合并添加元素

### 7.3.2 移除元素

### 7.3.3 Set 集合的 forEach()方法

### 7.3.4 将 Set 集合转换为数组

### 7.3.5 Weak Set 集合

## 7.4 ECMAScript 6 中的 Map 集合

### 7.4.1 Map 集合支持的方法

### 7.4.2 Map 集合的初始化方法

### 7.4.3 Map 集合的 forEach()方法

### 7.4.4 Weak Map 集合

# 第 8 章 迭代器（Iterator）和生成器（Generator）

用循环语句迭代数据时，必须要初始化一个变量来记录每一次迭代在数据集合中的位置，而在许多编程语言中，已经开始通过程序化的方式用迭代器对象返回迭代过程中集合的每一个元素。

迭代器的使用可以极大地简化数据操作，于是 ECMAScript 6 也向 JavaScript 中添加了这个迭代器特性。新的数组方法和新的集合类型（例如 Set 集合与 Map 集合）都依赖迭代器的实现，这个新特性对于高效的数据处理而言是不可或缺的，你也会发现在语言的其他特性中也都有迭代器的身影：新的 for-of 循环、展开运算符`...`，甚至连异步编程都可以使用迭代器。

## 8.1 循环语句的问题

虽然循环语句的语法简单，但是如果将多个循环嵌套则需要追踪多个变量，代码的复杂度会大大增加， 一不小心就错误使用了其他 for 循环的跟踪变量 ，从而导致程序出错。迭代器的出现旨在消除这种复杂性并减少循环中的错误。

```js
var colors = ["red", "green", "blue"];
for (var i = 0, len = colors.length; i < len; i++) {
  console.log(colors[i]);
}
```

## 8.2 什么是迭代器

迭代器是一种特殊对象，它具有一些专门为迭代过程设计的专有接口，所有的迭代器对象都有一个`next()`方法，每次调用都返回一个结果对象。结果对象有两个属性：一个是 value，表示下一个将要返回的值；另一个是 done ，它是一个布尔类型的值， 当没有更多可返回数据时返回 true 。迭代器还会保存一个内部指针，用来指向当前集合中值的位置，每调用一次 `next()`方法，都会返回下一个可用的值 。

如果在最后一个值返回后再调用 `next()`方法，那么返回的对象中属性 done 的值为 true ，属性 value 则包含迭代器最终返回的值，这个返回值不是数据集的一部分，它与函数的返回值类似，是函数调用过程中最后一次给调用者传递信息的方法，如果没有相关数据则返回 undefined 。

用 ECMAScript 5 的语法创建一个迭代器。

```js
function createIterator(items) {
  var i = 0;
  return {
    next: function () {
      var done = i >= items.length;
      var value = !done ? items[i++] : undefined;
      return {
        done: done,
        value: value,
      };
    },
  };
}

var iterator = createIterator([1, 2, 3]);
console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
// 之后所有的调用都会返回相同内容
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在 ECMAScript 6 中， 迭代器的编写规则也同样复杂，但 ECMAScript 6 同时还引入了一个生成器对象，它可以让创建迭代器对象的过程变得更简单。

## 8.3 什么是生成器

生成器是一种返回迭代器的函数，通过 function 关键字后的星号`*`来表示，函数中会用到新的关键宇 yield 。星号可以紧挨着 function 关键字 ，也可以在中间添加一个空格。

```js
// 生成器
function* createIterator() {
  yield 1;
  yield 2;
  yield 3;
}

// 生成器的调用方式与普通函数相同，只不过返回的是一个迭代器
let iterator = createIterator();
console.log(iterator.next().value); // 1
console.log(iterator.next().value); // 2
console.log(iterator.next().value); // 3
```

生成器函数最有趣的部分大概是，每当执行完一条 yield 语句后函数就会自动停止执行。

使用 yield 关键字可以返回任何值或表达式，所以可以通过生成器函数批量地给迭代器添加元素。例如，可以在循环中使用 yield 关键宇。

```js
function* createIterator(items) {
  for (let i = 0; i < items.length; i++) {
    yield items[i];
  }
}

let iterator = createIterator([1, 2, 3]);
console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
// 之后所有的调用都会返回相同内容
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

生成器函数是 ES6 中的一个重要特性，可以将其用于所有支持函数使用的地方。

> yield 的使用限制。  
> yield 关键字只可在生成器内部使用，在其他地方使用会导致程序抛出语法错误，即使在生成器内部的函数里使用也是如此。它与 return 关键字一样，二者都不能穿透函数边界。嵌套函数中的 return 语句不能用作函数的返回语句，而此处嵌套函数中的 yield 语句会导致程序抛出语法错误。

```js
function *createIterator(items) {
  items.forEach(function(item) {
    // 语法错误
    yield item + 1;
  });
}
```

### 8.3.1 生成器函数表达式

也可以通过函数表达式来创建生成器，只需在 function 关键字和小括号中间添加一个星号`*`即可。注意，不能用箭头函数来创建生成器。

```js
let createIterator = function* (items) {
  for (let i = 0; i < items.length; i++) {
    yield items[i];
  }
};

let iterator = createIterator([1, 2, 3]);
```

> 不能用箭头函数来创建生成器

### 8.3.2 生成器对象的方法

由于生成器本身就是函数，因而可以将它们添加到对象中。例如，在 ECMAScript 5 风格的对象字面量中，可以通过函数表达式来创建生成器。

```js
var o = {
  createIterator: function* (items) {
    for (let i = 0; i < items.length; i++) {
      yield items[i];
    }
  },
};

let iterator = o.createIterator([1, 2, 3]);
```

也可以用 ECMAScript 6 的函数方法的简写方式来创建生成器，只需在函数名前添加一个星号`*`。

```js
var o = {
  *createIterator(items) {
    for (let i = 0; i < items.length; i++) {
      yield items[i];
    }
  },
};

let iterator = o.createIterator([1, 2, 3]);
```

## 8.4 可迭代对象和 for-of 循环

可迭代对象具有 `Symbol.iterator` 属性，是一种与迭代器密切相关的对象。`Symbol.iterator` 通过指定的函数可以返回一个作用于附属对象的迭代器。在 ECMAScript 6 中，所有的集合对象（数组、 Set 集合及 Map 集合）和字符串都是可迭代对象，这些对象中都有默认的迭代器。 ECMAScript 中新加入的特性 for-of 循环需要用到可迭代对象的这些功能。

> 由于生成器默认会为 `Symbol.iterator` 属性赋佳，因此所有通过生成器创建的迭代器都是可迭代对象 。

for-of 循环每执行一次都会调用可迭代对象的 `next()` 方法，并将迭代器返回的结果对象的 value 属性存储在一个变量中，循环将持续执行这一过程直到返回对象的 done 属性的值为 true 。

```js
let values = [1, 2, 3];
for (let num of values) {
  console.log(num);
}
```

这段 for-of 循环的代码通过调用 values 数组的 `Symbol.iterator` 方法来获取迭代器，这一过程是在 JavaScript 引擎背后完成的。随后迭代器的 `next()`方法被多次调用，从其返回对象的 value 属性读取值并存储在变量 num 中，依次为 l 、 2 和 3，当结果对象的 done 属性值为 true 时循环退出，所以 num 不会被赋值为 undefined 。

如果只需迭代数组或集合中的值，用 for-of 循环代替 for 循环是个不错的选择。相比传统的 for 循环，for-of 循环的控制条件更简单，不需要追踪复杂的条件，所以更少出错。

> 如果将 for-of 语句用于不可迭代对象、 null 或 undefined 将会导致程序抛出错误。

### 8.4.1 访问默认迭代器

可以通过 `Symbol.iterator` 来访问对象默认的迭代器。

```js
let values = [1, 2, 3];
let iterator = values[Symbol.iterator]();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在这段代码中，通过 `Symbol.iterator` 获取了数组 values 的默认迭代器，并用它遍历数组中的元素。在 JavaScript 引擎中执行 for-of 循环语句时也会有类似的处理过程。

由于具有 `Symbol.iterator` 属性的对象都有默认的迭代器，因此可以用它来检测对象是否为可法代对象：

```js
function isIterable(object) {
  return typeof object[Symbol.iterator] === "function";
}

console.log(isIterable([1, 2, 3])); // true
console.log(isIterable("Hello")); // true
console.log(isIterable(new Map())); // true
console.log(isIterable(new Set())); // true
console.log(isIterable(new WeakMap())); // false
console.log(isIterable(new WeakSet())); // false
```

当然，也可以使用 `Symbol.iterator` 来创建属于自己的迭代器。

### 8.4.2 创建可迭代对象

默认情况下，开发者定义的对象都是不可选代对象，但如果给 `Symbol.iterator` 属性添加一个生成器，则可以将其变为可迭代对象。

```js
let collection = {
  items: [],
  *[Symbol.iterator]() {
    for (let item of this.items) {
      yield item;
    }
  },
};

collection.items.push(1);
collection.items.push(2);
collection.items.push(3);

for (let x of collection) {
  console.log(x);
}
// 1
// 2
// 3
```

在这个示例中，先创建一个生成器（注意，型号仍然在属性名前）并将其赋值给对象的 `Symbol.iterator` 属性来创建默认的迭代器；而在生成器中通过 for-of 循环迭代 `this.items` 并用 yield 返回每一个值。collection 对象默认迭代器的返回值由迭代器 `this.items` 自动生成，而非手动遍历来定义返回值。

> 在后面的“委托生成器”中，将会讲解对象迭代器的另一种使用方式。

在 ES6 中还有很多内建迭代器可以简化集合数据的操作。

## 8.5 内建迭代器

迭代器是 ES6 的 一个重要组成部分，在 ECMAScript 6 中，已经默认为许多内建类型提供了内建迭代器，只有当这些内建迭代器无法实现你的目标时才需要自己创建。通常来说当定义自己的对象和类时才会遇到这种情况，否则，完全可以依靠内建的迭代器完成工作，而最常使用的可能是集合的那些迭代器。

### 8.5.1 集合对象迭代器

在 ECMAScript 6 中有 3 种类型的集合对象：数组、 Map 集合与 Set 集合 。为了更好地访问对象中的内容，这 3 种对象都内建了以下三种迭代器：

- `entries()` 返回一个迭代器，其值为多个键值对。
- `values()` 返回一个迭代器，其值为集合的值。
- `keys()` 返回一个迭代器，其值为集合中的所有键名。

调用以上 3 个方法都可以访问集合的迭代器。

**entries()迭代器**

每次调用 `next()`方法时， `entries()`迭代器都会返回一个数组，数组中的两个元素分别表示集合中每个元素的键与值。如果被遍历的对象是数组，则第一个元素是数字类型的索引 ：如果是 Set 集合，则第一个元素与第二个元素都是值（ Set 集合中的值被同时作为键与值使用）；如果是 Map 集合，则第一个元素为键名。

```js
let colors = ["red", "green", "blue"];
let tracking = new Set([1234, 5678, 9012]);
let data = new Map();

data.set("title", "Understanding ECMAScript 6");
data.set("format", "ebook");

for (let entry of colors.entries()) {
  console.log(entry);
}

for (let entry of tracking.entries()) {
  console.log(entry);
}

for (let entry of data.entries()) {
  console.log(entry);
}

// [0, "red"]
// [1, "green"]
// [2, "blue"]
// [1234, 1234]
// [5678, 5678]
// [9012, 9012]
// ["title", "Understanding ECMAScript 6"]
// ["format", "ebook"]
```

**values() 迭代器**

调用 `values()` 迭代器时会返回集合中所存的所有值。调用`values()`迭代器后，返回的是每个集合中所包含的真正的数据，而不会包含数据在集合中的位置信息。

```js
let colors = ["red", "green", "blue"];
let tracking = new Set([1234, 5678, 9012]);
let data = new Map();

data.set("title", "Understanding ECMAScript 6");
data.set("format", "ebook");

for (let value of colors.values()) {
  console.log(value);
}

for (let value of tracking.values()) {
  console.log(value);
}

for (let value of data.values()) {
  console.log(value);
}

// "red"
// "green"
// "blue"
// 1234
// 5678
// 9012
// "Understanding ECMAScript 6"
// "ebook"
```

**keys() 迭代器**

`keys()` 迭代器会返回集合中存在的每一个键。如果遍历的是数组，则会返回数字类型的键，数组本身的其他属性不会被返回；如果是 Set 集合 ， 由于键与值是相同的 ， 因此 `keys()`和 `values()`返回的也是相同的迭代器；如果是 Map 集合，则 `keys()`迭代器会返回每个独立的键。

```js
let colors = ["red", "green", "blue"];
let tracking = new Set([1234, 5678, 9012]);
let data = new Map();

data.set("title", "Understanding ECMAScript 6");
data.set("format", "ebook");

for (let key of colors.keys()) {
  console.log(key);
}

for (let key of tracking.keys()) {
  console.log(key);
}

for (let key of data.keys()) {
  console.log(key);
}

// 0
// 1
// 2
// 1234
// 5678
// 9012
// "title"
// "format"
```

**不同集合类型的默认迭代器**

每个集合类型都有一个默认的迭代器，在 for-of 循环中，如果没有显式指定则使用默认的迭代器。数组和 Set 集合的默认迭代器是 `values()` 方法， Map 集合的默认迭代器是 `entries()`方法。有了这些默认的迭代器，可以更轻松地在 for-of 循环中使用集合对象。

```js
let colors = ["red", "green", "blue"];
let tracking = new Set([1234, 5678, 9012]);
let data = new Map();

data.set("title", "Understanding ECMAScript 6");
data.set("format", "print");

// 与调用colors.values()方法相同
for (let value of colors) {
  console.log(value);
}

// 与调用tracking.values()方法相同
for (let num of tracking) {
  console.log(num);
}

// 与调用data.entries()方法相同
for (let entry of data) {
  console.log(entry);
}
```

默认情况下，如果是数组和 Set 集合，会逐一返回集合中所有的值；如果是 Map 集合，则按照 Map 构造函数参数的格式返回相同的数组内容。而 WeakSet 集合与 WeakMap 集合就没有内建的迭代器，由于要管理弱引用，因而无法确切地知道集合中存在的值，也就无法迭代这些集合了。

> 解构与 for-of 循环。  
> 如果要在 for-of 循环中使用解构语法，则可以利用 Map 集合默认构造函数的行为来简化编码过程，将 Map 集合中每一个条目解构为 key 和 value 两变量。使用这种方法后，便不再需要访问含有键和值的两元素数组，也不需要通过 Map 集合的内建方法取出每一个键和值。 除了 Map 集合外，我们也可将 for-of 循环中的解构方法应用于 Set 集合与数组 。

```js
let data = new Map();
data.set("title", "Understanding ECMAScript 6");
data.set("format", "ebook");
// 与使用data.entries()方法相同
for (let [key, value] of data) {
  console.log(key + "=" + value);
}
```

### 8.5.2 字符串迭代器

自 ECMAScript 5 发布以后， JavaScript 字符串慢慢变得更像数组了，例如，ECMAScript 5 正式规定可以通过方括号访问字符串中的宇符（也就是说，`text[0]`可以获取字符串 text 的第一个字符，并以此类推）。由于方括号操作的是编码单元而非字符，因此无法正确访问双字节字符.

```js
var message = "A 𠮷 B";

for (let i = 0; i < message.length; i++) {
  console.log(message[i]);
}

// A
// (空)
// (空)
// (空)
// (空)
// B
```

由于双字节字符被视作两个独立的编码但愿，从而最终在 A 与 B 之间打印出 4 个空行。

所幸， ECMAScript 6 的目标是全面支持 Unicode ，并且我们可以通过改变字符串的默认迭代器来解决这个问题，使其操作字符而不是编码单元。现在，我们修改前一个示例中字符串的默认迭代器，让 for-of 循环输出正确的内容。

```js
var message = "A 𠮷 B";

for (let c of message) {
  console.log(c);
}

// A
// (blank)
// 𠮷
// (blank)
// B
```

### 8.5.3 NodeList 迭代器

DOM 标准中有一个 NodeList 类型， document 对象中的所有元素都用这个类型来表示。对于编写 Web 浏览器环境中的 JavaScript 的开发者来说，需要花一点儿功夫去理解 NodeList 对象和数组之间的差异。二者都使用 length 属性来表示集合中元素的数量，都可以通过方括号来访问集合中的独立元素：而在内部实现中，二者的表现非常不一致，因而会造成很多困扰。

自从 ECMAScript 6 添加了默认迭代器后， DOM 定义中的 NodeList 类型（定义在 HTML 标准而不是 ECMAScript 6 标准中）也拥有了默认迭代器，其行为与数组的默认迭代器完全一致。所以可以将 NodeList 应用于 for-of 循环及其他支持对象默认迭代器的地方。

```js
var divs = document.getElementsByTagName("div");

for (let div of divs) {
  console.log(div.id);
}
```

## 8.6 展开运算符与非数组可迭代对象

展开运算符可以把 Set 集合的所有值填充到了一个数组字面量里，它可以操作所有可迭代对象，并根据默认迭代器来选取要引用的值，从迭代器读取所有值。然后按照返回顺序将它们依次插入到数组中。

```js
let set = new Set([1, 2, 3, 3, 3, 4, 5]),
  array = [...set];

console.log(array); // [1,2,3,4,5]
```

展开运算符也可以把 Map 集合转换成包含多个数组的数组， Map 集合的默认迭代器返回的是多组键值对，所以结果数组与执行 `new Map()` 时传入的数组看起来一样 。

```js
let map = new Map([
    ["name", "Nicholas"],
    ["age", 25],
  ]),
  array = [...map];

console.log(array); // [ ["name", "Nicholas"], ["age", 25]]
```

在数组字面量中可以多次使用展开运算符，将可迭代对象中的多个元素一次插入新数组中，替换原先展开运算符所在的位置。

```js
let smallNumbers = [1, 2, 3],
  bigNumbers = [100, 101, 102],
  allNumbers = [0, ...smallNumbers, ...bigNumbers];

console.log(allNumbers.length); // 7
console.log(allNumbers); // [0, 1, 2, 3, 100, 101, 102]
```

由于展开运算符可以作用于任意可迭代对象，因此如果想将可迭代对象转换为数组，这是最简单的方法。既可以将字符串中的每一个字符（不是编码单元）存入新数组中，也可以将浏览器中 NodeList 对象中的每一个节点存入新的数组中。

## 8.7 高级迭代器功能

迭代器的基础功能可以辅助我们完成很多任务，通过生成器创建迭代器的过程也很便捷，除了这些简单的集合遍历任务外，迭代器也可以被用于完成一些复杂的任务。

### 8.7.1 给迭代器传递参数

在本章的示例中，已经展示了一些迭代器向外传值的方法，既可以用迭代器的`next()`方法返回值，也可以在生成器内部使用 yield 关键字来生成值。如果给迭代器的`next()`方法传递参数，则这个参数的值就会替代生成器内部上一条 yield 语句的返回值。而如果要实现更多像异步编程这样的高级功能，那么这种给迭代器传值的能力就变得至关重要。请看这个简单的示例：

```js
function* createIterator() {
  let first = yield 1;
  let second = yield first + 2; // 4 + 2
  yield second + 3; // 5 + 3
}

let iterator = createIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next(4)); // "{ value: 6, done: false }"
console.log(iterator.next(5)); // "{ value: 8, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

这里有一个特例，第一次调用`next()`方法时无论传入什么参数都会被丢弃。由于传给`next()`方法的参数会替代上一次 yield 的返回值，而在第一次调用`next()`方法前不会执行任何 yield 语句，因此在第一次调用`next()`方法时传递参数是毫无意义的。

第二次调用`next()`方法传入数值 4 作为参数，它最后被赋值给生成器函数内部的变量 first。在一个含参 yield 语句中，表达式右侧等价于第一次调用`next()`方法后的下一个返回值，表达式左侧等价于第二次调用`next()`方法后，在函数继续执行前得到的返回值。第二次调用`next()`方法传入的值为 4,它会被赋值给变量 first,函数则继续执行。

第二条 yield 语句在第一次 yield 的结果上加了 2,最终的返回值为 6。第三次调用`next()`方法时，传入数值 5,这个值被赋值给 second,最后用于第三条 yield 语句并最终返回数值 8。

如果想理解程序内部的具体细节，想清楚这些会对你很有帮助：在生成器内部，代码每次继续执行前，正在执行的代码是哪一段。图 8-1 通过灰色阴影展示了每次 yield 前正在执行的代码。

在生成器内部，浅灰色高亮的是`next()`方法的第一次调用，中灰色标示了 `next(4)`的调用过程，深灰色标示了 `next(5)`的调用过程，分别返回每一次 yield 生成的值。这里有一个过程很复杂，在执行左侧代码前，右侧的每一个表达式会先执行再停止。比起普通的函数，调试复杂的生成器会花费更多的精力。

给迭代器的`next()`方法传值时，yield 语句可以返回相应计算后的值，而在生成器的内部，还有很多诸如此类的执行技巧可以使用，例如在迭代器中手动抛出错误。

### 8.7.2 在迭代器中抛出错误

除了给迭代器传递数据外，还可以给它传递错误条件。通过`throw()`方法，当迭代器恢复执行时可令其抛出一个错误。这种主动抛出错误的能力对于异步编程而言至关重要，也能为你提供模拟结束函数执行的两种方法（返回值或抛出错误）,从而增强生成器内部的编程弹性。将错误对象传给 `throw()`方法后，在迭代器继续执行时其会被抛出。例如：

```js
function* createIterator() {
  let first = yield 1;
  let second = yield first + 2; // yield 4 + 2, then throw
  yield second + 3; // never is executed
}

let iterator = createIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next(4)); // "{ value: 6, done: false }"
console.log(iterator.throw(new Error("Boom"))); // error thrown from generator
```

在这个示例中，前两个表达式正常求值，而调用 `throw()` 方法后，在继续执行 `let second` 求值前，错误就会被抛出并阻止了代码继续执行。这个过程与直接抛出错误很相似，二者唯一的区别是抛出的时机不同。

知道了这一点，就可以在生成器内部通过 try-catch 代码块来捕获这些错误。

```js
function* createIterator() {
  let first = yield 1;
  let second;

  try {
    second = yield first + 2; // yield 4 + 2, then throw
  } catch (ex) {
    second = 6; // on error, assign a different value
  }
  yield second + 3;
}

let iterator = createIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next(4)); // "{ value: 6, done: false }"
console.log(iterator.throw(new Error("Boom"))); // "{ value: 9, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在此示例中，try-catch 代码块包裹着第二条 yield 语句。尽管这条语句本身没有错误，但在给变量 second 赋值前还是会主动抛出错误，catch 代码块捕获错误后将 second 变量赋值为 6,下一条 yield 语句继续执行后返回 9。

请注意这里有一个有趣的现象：调用`throw()`方法后也会像调用`next()`方法一样返回一个结果对象。由于在生成器内部捕获了这个错误，因而会继续执行下一条 yield 语句，最终返回数值 9。

如此一来，`next()`和`throw()`就像是迭代器的两条指令，调用`next()`方法食令迭代器继续执行（可能提供一个值）,调用`throw()`方法也会命令迭代器继续执行，但同时也抛出一个错误，在此之后的执行过程取决于生成器内部的代码。

在迭代器内部，如果使用了 yield 语句，则可以通过`next()`方法和`throw()`方法控制执行过程，当然，也可以使用 return 语句返回一些与普通函数返回语句不太一样的内容，下一节将讲解这方面的内容。

### 8.7.3 生成器返回语句

由于生成器也是函数，因此可以通过 return 语句提前退出函数执行，对于最后一次`next()`方法调用，可以主动为其指定一个返回值。在本章的绝大多数示例中，最后一次调用返回的都是 undefined,正如在其他函数中那样，你可以通过 return 语句指定一个返回值。而在生成器中，return 表示所有操作已经完成，属性 done 被设置为 true;如果同时提供了相应的值，则属性 value 会被设置为这个值。这里有一个简单的示例：

```js
function* createIterator() {
  yield 1;
  return;
  yield 2;
  yield 3;
}

let iterator = createIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在这段代码中的生成器包含多条 yield 语句和一条 return 语句，其中 return 语句紧随第一条 yield 语句，其后的 yield 语句将不会被执行。

在 return 语句中也可以指定一个返回值，该值将被赋值给返回对象的 value 属性：

```js
function* createIterator() {
  yield 1;
  return 42;
}

let iterator = createIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 42, done: true }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在此示例中，第二次调用 `next()` 方法时返回对象的 value 属性值为 42 ，done 属性首次设为 true；第三次调用 `next()` 方法依然返回一个对象，只是 value 属性的值会变为 undefined 。因此，通过 return 语句指定的返回值，只会在返回对象中出现一次，在后续调用返回的对象中， value 属性会被重置为 undefined。

> 展开运算符与 for-of 循环语句会直接忽略通过 return 语句指定的任何返回值，只要 done 一变为 true 就立即停止读取其他的值。不管怎样，迭代器的返回值依然是一个非常有用的特性，比如即将要讲到的委托生成器。

### 8.7.4 委托生成器

在某些情况下，我们需要将两个迭代器合二为一，这时可以创建一个生成器，再给 yield 语句添加一个星号，就可以将生成数据的过程委托给其他生成器。当定义这些生成器时，只需将星号放置在关键字 yield 和生成器的函数名之间即可，就像这样：

```js
function* createNumberIterator() {
  yield 1;
  yield 2;
}

function* createColorIterator() {
  yield "red";
  yield "green";
}

function* createCombinedIterator() {
  yield* createNumberIterator();
  yield* createColorIterator();
  yield true;
}

var iterator = createCombinedIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: "red", done: false }"
console.log(iterator.next()); // "{ value: "green", done: false }"
console.log(iterator.next()); // "{ value: true, done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

这里的生成器`createCombinedIterator()`先后委托了另外两个生成器`createNumberlterator()`和`createColorlterator()`。仅根据迭代器的返回值来看，它就像是一个完整的迭代器，可以生成所有的值。每一次调用`next()`方法就会委托相应的迭代器生成相应的值，直到最后由`createNumberlterator()`和`createColorlterator()`创建的迭代器无法返回更多的值，此时执行最后一条 yield 语句并返回 true，

有了生成器委托这个新功能，可以进一步利用生成器的返回值来处理复杂任务。

```js
function* createNumberIterator() {
  yield 1;
  yield 2;
  return 3;
}

function* createRepeatingIterator(count) {
  for (let i = 0; i < count; i++) {
    yield "repeat";
  }
}

function* createCombinedIterator() {
  let result = yield* createNumberIterator();
  yield* createRepeatingIterator(result);
}

var iterator = createCombinedIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

在生成器`createCombinedlterator()`中，执行过程先被委托给了生成器`createNumberlterator()`，返回值会被赋值给变量 result，执行到 return 3 时会返回数值 3。这个值随后被传入`createRepeatinglterator()`作为它的参数，因而生成字符串"repeat"的 yield 语句会被执行三次。

无论通过何种方式调用迭代器`next()`方法，数值 3 都不会被返回，它只存在于生成器`createCombinedlterator()`的内部。但如果想输出这个值，则可以额外添加一条 yield 语句。

```js
function* createNumberIterator() {
  yield 1;
  yield 2;
  return 3;
}

function* createRepeatingIterator(count) {
  for (let i = 0; i < count; i++) {
    yield "repeat";
  }
}

function* createCombinedIterator() {
  let result = yield* createNumberIterator();
  yield result;
  yield* createRepeatingIterator(result);
}

var iterator = createCombinedIterator();

console.log(iterator.next()); // "{ value: 1, done: false }"
console.log(iterator.next()); // "{ value: 2, done: false }"
console.log(iterator.next()); // "{ value: 3, done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: "repeat", done: false }"
console.log(iterator.next()); // "{ value: undefined, done: true }"
```

> `yield*`也可直接应用于字符串，例如`yield * "hello"`，此时将使用字符串的默认迭代器。

## 8.8 异步任务执行

生成器令人兴奋的特性多与异步编程有关，JavaScript 中的异步编程有利弊：简单任务的异步化非常容易；而复杂任务的异步化会带来很多管理代码的挑战。由于生成器支持在函数中暂停代码执行，因而可以深入挖掘异步处理的更多用法。

执行异步操作的传统方式一般是调用一个函数并执行相应回调函数。举个例子，我们用 Node.js 编写一段从磁盘读取文件的代码：

```js
let fs = require("fs");

fs.readFile("config.json", function (err, contents) {
  if (err) {
    throw err;
  }

  doSomethingWith(contents);
  console.log("Done");
});
```

调用 `fs.readFile()`方法时要求传入要读取的文件名和一个回调函数，操作结束后会调用该回调函数并检查是否存在错误，如果没有就可以处理返回的内容。如果要执行的任务很少，那么这样的方式可以很好地完成任务；如若需要嵌套回调或序列化一系列的异步操作，事情会变得非常复杂。此时，生成器和 yield 语句就派上用场了。

### 8.8.1 简单任务执行器

由于执行 yield 语句会暂停当前函数的执行过程并等待下一次调用`next()`方法，因此你可以创建一个函数，在函数中调用生成器生成相应的迭代器，从而在不用回调函数的基础上实现异步调用`next()`方法，就像这样：

```js
function run(taskDef) {
  // 创建一个无使用限制的迭代器
  let task = taskDef();
  // 开始执行任务
  let result = task.next();
  // 循环调用 next() 的函数
  function step() {
    // 如果任务未完成，则继续执行
    if (!result.done) {
      result = task.next();
      step();
    }
  }
  // 开始迭代执行
  step();
}
```

函数 `run()`接受一个生成器函数作为参数，这个函数定义了后续要执行的任务，生成一个迭代器并将它储存在变量 task 中。首次调用迭代器的`next()`方法时，返回的结果被储存起来稍后继续使用。`step()`函数会检查 `result.done` 的值，如果为 false 则执行迭代器的`next()`方法，并再次执行 `step()`操作。每次调用`next()`方法时，返回的最新信息总会覆写变量 result。在代码的最后，初始化执行 `step()`函数并开始整个的迭代过程，每次通过检查 `result.done` 来确定是否有更多任务需要执行。

借助这个 `run()`函数，可以像这样执行一个包含多条 yield 语句的生成器：

```js
run(function* () {
  console.log(1);
  yield;
  console.log(2);
  yield;
  console.log(3);
});
```

这个示例最终会向控制台输出多次调用`next()`方法的结果，分别为数值 1、2 和 3。当然，简单输出迭代次数不足以展示迭代器高级功能的实用之处，下一步将在迭代器与调用者之间互相传值。

### 8.8.2 向任务执行器传递数据

给任务执行器传递数据的最简单办法是，将值通过迭代器的`next()`方法传入作为 yield 的生成值供下次调用。在这段代码中，只需将`result.value`传入`next()`方法即可。

```js
function run(taskDef) {
  // 创建一个无使用限制的迭代器
  let task = taskDef();
  // 开始执行任务
  let result = task.next();
  // 循环调用 next() 的函数
  function step() {
    // 如果任务未完成，则继续执行
    if (!result.done) {
      result = task.next(result.value);
      step();
    }
  }
  // 开始迭代执行
  step();
}
```

现在`result.value`作为`next()`方法的参数被传入，这样就可以在 yield 调用之间传递数据了。

```js
run(function* () {
  let value = yield 1;
  console.log(value); // 1
  value = yield value + 3;
  console.log(value); // 4
});
```

此示例会向控制台输出两个数值 1 和 4。其中，数值 1 取自`yield 1`语句中回传给变量 value 的值；而 4 取自给变量 value 加 3 后回传给 value 的值。现在数据已经能够在 yield 调用间互相传递了，只需一个小小改变便能支持异步调用。

### 8.8.3 异步任务执行器

之前的示例只是在多个 yield 调用间来回传递静态数据，而等待一个异步过程有些不同。任务执行器需要知晓回调函数是什么以及如何使用它。由于 yield 表达式会将值返回给任务执行器，所有的函数调用都会返回一个值，因而在某种程度上这也是一个异步操作，任务执行器会一直等待直到操作完成。

下面定义一个异步操作。

```js
function fetchData() {
  return function (callback) {
    callback(null, "Hi!");
  };
}
```

本示例的原意是让任务执行器调用的所有函数都返回一个可以执行回调过程的函数，此处`fetchData()`函数的返回值是一个可接受回调函数作为参数的函数，当调用它时会传入一个字符串"Hi!"作为回调函数的参数并执行。参数 callback 需要通过任务执行器指定，以确保回调函数执行时可以与底层迭代器正确交互。尽管`fetchData()`是同步函数，但简单添加一个延迟方法即可将其变为异步函数。

```js
function fetchData() {
  return function (callback) {
    setTimeout(function () {
      callback(null, "Hi!");
    }, 50);
  };
}
```

在这个版本的`fetchData()`函数中，让回调函数延迟了 50ms 再被调用，所以这种模式在同步和异步状态下都运行良好。只需保证每个要通过 yield 关键字调用的函数都按照与之相同的模式编写。

理解了函数中异步过程的运作方式，可以将任务执行器稍作修改。当`result.value`是一个函数时，任务执行器会先执行这个函数再将结果传入`next()`方法。

```js
function run(taskDef) {
  // 创建迭代器，让它在别处可用
  let task = taskDef();
  // 启动任务
  let result = task.next();
  // 递归使用函数来保持对 next() 的调用
  function step() {
    // 如果还有更多要做的
    if (!result.done) {
      if (typeof result.value === "function") {
        result.value(function (err, data) {
          if (err) {
            result = task.throw(err);
            return;
          }
          result = task.next(data);
          step();
        });
      } else {
        result = task.next(result.value);
        step();
      }
    }
  }
  // 开始处理过程
  step();
}
```

通过`===`操作符检査后，如果`result.value`是一个函数，会传入一个回调函数作为参数调用它，回调函数遵循 Node.js 有关执行错误的约定：所有可能的错误放在第一个参数(err)中，结果放在第二个参数中。如果传入了 err，意味着执行过程中产生了错误，这时通过`task.throw()`正确输出错误对象；如果没有错误产生，data 被传入`task.next()`作为结果储存起来，并继续执行 step()。如果`result.value`不是一个函数，则直接将其传入 next()方法。

现在，这个新版的任务执行器已经可以用于所有的异步任务了。在 Node.js 环境中，如果要从文件中读取一些数据，需要在`fs.readFile()`外围创建一个包装器(wrapper)，并返回一个与`fetchData()`类似的函数。

```js
let fs = require("fs");
function readFile(filename) {
  return function (callback) {
    fs.readFile(filename, callback);
  };
}
```

`readFile()`接受一个文件名作为参数，返回一个可以执行回调函数的函数。回调函数被直接传入`fs.readFile()`方法，读取完成后会执行它。

```js
run(function* () {
  let contents = yield readFile("config.json");
  doSomethingWith(contents);
  console.log("Done");
});
```

在这段代码中没有任何回调变量，异步的`readFile()`操作却正常执行，除了 yield 关键字外，其他代码与同步代码完全一样，只不过函数执行的是异步操作。所以遵循相同的接口，可以编写一些读起来像是同步代码的异步逻辑。

当然，这些示例中使用的模式也有缺点，也就是不能百分百确认函数中返回的其他函数一定是异步的。着眼当下，最重要的是能理解任务执行过程背后的理论知识。ES6 中的新特性 Promise 可以提供一种更灵活的方式来调度异步任务，将在第 11 章 深入讲解这个功能。

## 8.9 小结

迭代器是 ECMAScript6 的一个重要组成部分，它是语言中某些关键语言元素的依赖。尽管迭代器看起来好像只是一种通过几个简单 API 返回一系列值的新特性，但在 ECMAScript6 中，它还能被应用于许多更复杂的场景中。

`Symbol.iterator`被用来定义对象的默认迭代器，内建对象和开发者定义的对象都支持这个特性，通过这个 Symbol 定义的方法可以返回一个迭代器。如果对象中有`Symbol.iterator`这个属性，则此对象为可迭代对象。

for-of 循环可以持续获取可选代对象中的值，与传统的 for 循环迭代相比，for-of 循环不需要追踪值在集合中的位置，也不需要控制循环结束的时机，使用起来非常方便，它会自动地从迭代器中读取所有值，如果没有更多可返回的值就自动退出循环。

为了降低 for-of 的使用成本，ECMAScript6 中的许多值都有默认迭代器。所有的集合类型（例如数组、Map 集合与 Set 集合）都有默认迭代器，字符串同样也有默认迭代器，其可以直接迭代字符串中的子符，避免了遍历编码单元带来的诸多问题。

展开运算符也可以作用于可选代对象，通过迭代器从对象中读取相应的值并插入到一个数组中。

生成器是一类特殊函数，在定义时需要额外添加一个星号`*`,被调用时会自动创建一个迭代器，并通过关键字 yield 来标识每次调用迭代器的`next()`方法时的返回值。

借助生成器委托这个新特性，便可重用已有生成器来创建新的生成器，从而进一步封装更复杂的迭代器行为。新语法使用`yield *`来标识生成的值，新迭代器的返回值便可取自己有的多个迭代器。

在生成器和迭代器的所有应用场景中，最有趣且最令人兴奋的可能是用来创建更简洁的异步代码。这种方式无须在所有地方定义回调函数，其代码看起来像是同步代码，但实际上使用了 yield 生成的特性来等待异步操作最终完成。

# 第 9 章 JavaScript 中的类

## 9.1 ECMAScript 5 中的近类结构

## 9.2 类的声明

### 9.2.1 基本的类声明语法

### 9.2.2 为何使用类语法

## 9.3 类表达式

### 9.3.1 基本的类表达式语法

### 9.3.2 命名类表达式

## 9.4 作为一等公民的类

## 9.5 访问器属性

## 9.6 可计算成员名称

## 9.7 生成器方法

## 9.8 静态成员

## 9.9 继承与派生类

### 9.9.1 类方法遮蔽

### 9.9.2 静态成员继承

### 9.9.3 派生自表达式的类

### 9.9.4 内建对象的继承

### 9.9.5 Symbol.species 属性

## 9.10 在类的构造函数中使用 new.target

# 第 10 章 改进的数组功能

数组是一种基础的 JavaScript 对象，随着时间推进，JavaScript 中的其他部分一直在演进，而直到 ECMAScript5 标准才为数组对象引入一些新方法来简化使用。ECMAScript6 标准继续改进数组，添加了很多新功能。

## 10.1 创建数组

在 ECMAScript6 以前，创建数组的方式主要有两种，一种是调用 Array 构造函数，另一种是用数组字面量语法，这两种方法均需列举数组中的元素，功能非常受限。如果想将一个类数组对象（具有数值型索引和 length 属性的对象）转换为数组，可选的方法也十分有限，经常需要编写额外的代码。为了进一步简化 JavaScript 数组的创建过程，ECMAScript6 新增了 `Array.of()` 和 `Array.from()` 两个方法 。

### 10.1.1 Array.of()方法

如果给 Array 构造函数传入一个数值型的值，那么数组的 length 属性会被设为该值；如果传入多个值，此时无论这些值是不是数值型的，都会变为数组的元素。这个特性令人感到困惑，所以存在一定的风险。

```JavaScript
let items = new Array(2);
console.log(items.length);          // 2
console.log(items[0]);              // undefined
console.log(items[1]);              // undefined

items = new Array("2");
console.log(items.length);          // 1
console.log(items[0]);              // "2"

items = new Array(1, 2);
console.log(items.length);          // 2
console.log(items[0]);              // 1
console.log(items[1]);              // 2

items = new Array(3, "2");
console.log(items.length);          // 2
console.log(items[0]);              // 3
console.log(items[1]);              // "2"
```

ECMAScript6 通过引入 `Array.of()` 方法来解决这个问题。无论有多少个参数，无论参数时什么类型的，`Array.of()` 总会创建一个包含所有参数的数组。

```js
let items = Array.of(1, 2);
console.log(items.length); // 2
console.log(items[0]); // 1
console.log(items[1]); // 2

items = Array.of(2);
console.log(items.length); // 1
console.log(items[0]); // 2

items = Array.of("2");
console.log(items.length); // 1
console.log(items[0]); // "2"
```

这与数组字面量的使用方法很相似，在大多数情况，可以用数组字面量来创建原生数组，但如果需要给一个函数传入 Array 的构造函数，则可能更希望传入 `Array.of()` 来确保行为一致。

```JavaScript
function createArray(arrayCreator, value) {
    return arrayCreator(value);
}

let items = createArray(Array.of, value);
```

### 10.1.2 Array.from()方法

`Array.from()` 方法。JavaScript 不支持直接将非数组对象转换为真实数组，arguments 就是一种类数组对象，如果要把它当做数组使用则必须先转换该对象的类型。在 ECMAScript5 中，可能需要编写如下函数来把类数组对象转换为数组。

```JavaScript
function makeArray(arrayLike) {
    var result = [];

    for (var i = 0, len = arrayLike.length; i < len; i++) {
        result.push(arrayLike[i]);
    }

    return result;
}

function doSomething() {
    var args = makeArray(arguments);

    // use args
}
```

另外，开发者发现了一种只需编写极少代码的新方法，调用数组原生的 `slice()` 方法可以将非数组对象转换为数组。

```JavaScript
function makeArray(arrayLike) {
    return Array.prototype.slice.call(arrayLike);
}

function doSomething() {
    var args = makeArray(arguments);
    // use args
}
```

ECMAScript6 添加了一个语义清晰、语法简洁的新方法 `Array.from()` 来将对象转化为数组。`Array.from()` 方法可以接受可迭代对象或类数组对象作为第一个参数，最终返回一个数组。`Array.from()` 方法也是通过 this 来确定返回数组的类型的。

```js
function doSomething() {
  var args = Array.from(arguments);
  // use args
}
```

映射转换。如果想要进一步转化数组，可以提供一个映射函数作为 `Array.from()` 第二个参数，这个函数用来将类数组对象中的每一个值转换成其他形式，最后将这些结果储存在结果数组的相应索引中。

```JavaScript
function translate() {
    return Array.from(arguments, (value) => value + 1);
}

let numbers = translate(1, 2, 3);

console.log(numbers);               // 2,3,4
```

如果用映射函数处理对象，也可以给 `Array.from()` 传入第三个参数来表示映射函数的 this 值，从而无需通过调用 `bind()` 方法或其他方法来指定 this 的值了。

```JavaScript
let helper = {
    diff: 1,

    add(value) {
        return value + this.diff;
    }
};

function translate() {
    return Array.from(arguments, helper.add, helper);
}

let numbers = translate(1, 2, 3);

console.log(numbers);               // 2,3,4
```

用 `Array.from()` 转换可迭代对象。`Array.from()` 方法可以处理类数组对象和可迭代对象，也就是说该方法能够将所有含有 Symbol.iterator 属性的对象转换为数组。

```JavaScript
let numbers = {
    *[Symbol.iterator]() {
        yield 1;
        yield 2;
        yield 3;
    }
};

let numbers2 = Array.from(numbers, (value) => value + 1);

console.log(numbers2);              // 2,3,4
```

## 10.2 为所有数组添加的新方法

ECMAScript6 延续了 ECMAScript5 的一贯风格，也为数组添加了几个新的方法。`find()` 方法和 `findIndex()` 方法可以协助开发者在数组中查找任意值；`fill()` 方法和 `copyWithin()` 方法的灵感来自于定型数组的使用过程。

### 10.2.1 find()方法和 findIndex()方法

在 ECMAScript5 以前的版本中，由于没有内建的数组搜索方法，因此想在数组中查找元素会比较麻烦，于是 ECMAScript5 正式添加了 `indexOf()` 和 `lastlndexOf()` 两个方法，可以用它们在数组中查找特定的值。虽然这是一个巨大的进步，但这两种方法仍有局限之处，即每次只能查找一个值，如果想在一系列数字中查找第一个偶数，则必须自己编写代码来实现。于是 ECMAScript6 引入了 `find()` 方法和 `findlndex()` 方法来解决这个问题。

`find()` 方法和 `findIndex()` 方法都接受两个参数：一个是回调函数；另一个是可选参数，用来指定回调函数中 this 的值。

执行回调函数时，传入的参数分别为：数组中的某个元素和该元素在数组中的索引以及数组本身，与传入 `map()` 和 `foreach()` 方法的参数相同。

如果给定的值满足定义的标准，回调函数应返回 true，一旦回调函数返回 true，`find()` 方法和 `findIndex()` 方法都会立即停止搜索数组剩余的部分。

二者间的唯一的区别是，`find()` 方法返回查找到的值，`findIndex()` 方法返回查找倒的索引。

```JavaScript
let numbers = [25, 30, 35, 40, 45];

console.log(numbers.find(n => n > 33));         // 35
console.log(numbers.findIndex(n => n > 33));    // 2
```

如果要在数组中根据某个条件查找匹配的元素，那么 `find()` 方法和 `findIndex()` 方法可以很好地完成任务；如果只想查找与某个值匹配的元素，则 `indexOf()` 方法和 `lastIndexOf()` 方法时更好的选择。

### 10.2.2 fill() 方法。

`fill()` 方法可以用指定的值填充一至多个数组元素。当传入一个值时，`fill()` 方法会用这个值重写数组中的所有值。

```js
let numbers = [1, 2, 3, 4];

numbers.fill(1);
console.log(numbers.toString()); // 1,1,1,1
```

如果只想改变数组某一部分的值，可以传入开始索引和结束索引（不包含结束索引当前值）这两个可选参数。如果索引为负值，则这些值会与数组的 length 属性相加作为最终位置。

```JavaScript
let numbers = [1, 2, 3, 4];

numbers.fill(1, 2);
console.log(numbers.toString());    // 1,2,1,1

numbers.fill(0, 1, 3);
console.log(numbers.toString());    // 1,0,0,1
```

### 10.2.3 copyWithin()方法。

`copyWithin()` 方法与 `fill()` 方法相似，其也可以同时改变数组中的多个元素。`fill()` 方法是将数组元素赋值为一个指定的值，而 `copyWithin()` 方法则是从数组中复制元素的值。调用 `copyWithin()` 方法时需要传入两个参数：一个是该方法开始填充值的索引位置，另一个是开始复制值得索引位置。

```JavaScript
let numbers = [1, 2, 3, 4];

// paste values into array starting at index 2
// copy values from array starting at index 0
numbers.copyWithin(2, 0);

console.log(numbers.toString());    // 1,2,1,2
```

默认情况下，`copyWithin()` 方法会一直复制直到数组末尾的值，但是可以提供可选的第三个参数来限制被重写元素的数量。第三个参数时不包含结束索引，用于指定停止复制值的位置。

```JavaScript
let numbers = [1, 2, 3, 4];

// paste values into array starting at index 2
// copy values from array starting at index 0
// stop copying values when you hit index 1
numbers.copyWithin(2, 0, 1);

console.log(numbers.toString());    // 1,2,1,4
```

## 10.3 完型数组

定型数组是一种用于处理数值类型数据的专用数组，最早是在 WebGL 中使用的，WebGL ES 2.0 的移植版，在 Web 页面中通过`<canvas>`元素来呈现它。定型数组也被一同移植而来，其可为 JavaScript 提供快速的按位运算。

在 JavaScript 中，数字是以 64 位浮点格式存储的，并按需转换为 32 位整数，所以算术运算非常慢，无法满足 WebGL 的需求。因此在 ECMAScript 6 中引入定型数组来解决这个问题，井提供更高性能的算术运算。所谓定型数组，就是将任何数字转换为一个包含数字比特的数组，随后就可以通过我们熟悉的 JavaScript 数组方法来进一步处理 。

ECMAScript 6 采用定型数组作为语言的正式格式来确保更好的跨 JavaScript 引擎兼容性以及与 JavaScript 数组的互操作性。尽管 ECMAScript 6 版本的定型数组与 WebGL 中的不一样，但是仍保留了足够的相似之处，这使得 ECMAScript 6 版本可以基于 WebGL 版本演化而不至于走向完全分化。

### 10.3.1 数值数据类型。

JavaScript 数组按照 IEEE 754 标准定义的格式存储，也就是用 64 个比特来存储一个浮点形式的数字。这个格式用于表示 JavaScript 中的证书及浮点数，两种格式间经常伴随着数字改变发生相互转换。定型数组支持存储和操作以下 8 种不同的数值类型。

- 有符号 8 位 整数 (int8)
- 无符号 8 位 整数 (uint8)
- 有符号 16 位 整数 (int16)
- 无符号 16 位 整数 (uint16)
- 有符号 32 位 整数 (int32)
- 无符号 32 位 整数 (uint32)
- 32 位 浮点数 (float32)
- 64 位 浮点数 (float64)

如果用普通的 JavaScript 数字来存储 8 位整数，会浪费整整 56 个比特，这些比特原本可以存储其他 8 位整数或小于 56 比特的数字。这也正是定型数组的一个实际用例，即更有效地利用比特。所有与定型数组有关的操作和对象都集中在这 8 个数据类型上，但是在使用它们之前，需要创建一个数组缓冲区存储这些数据。

### 10.3.2 数组缓冲区

数组缓冲区是所有定型数组的根基，它是一段可以包含特定数量字节的内存地址。创建数组缓冲区的过程类似于在 C 语言中调用 `malloc()` 来分配内存，知识不需指明内存块所包含的数据类型。可以通过 ArrayBuffer 构造函数来创建数组缓冲区。创建完成后，可以通过 byteLength 属性查看缓冲区中的比特数量。

```JavaScript
let buffer = new ArrayBuffer(10);   // allocate 10 bytes
console.log(buffer.byteLength);     // 10
```

也可以通过 `slice()` 方法分割已有数组缓冲区来创建一个新的，这个 `slice()` 方法与数组上的 `slice()` 方法很像：传入开始索引和结束索引为参数，然后返回一个新的 ArrayBuffer 实例，新实例由原始数组缓冲区的切片组成。

### 10.3.3 通过视图操作数组缓冲区

数组缓冲区是内存中的一段地址，视图是用来操作内存的接口。视图可以操作数组缓冲区或缓冲区字节的子集，并按照其中一种数值型数据类型来读取和写入数据。DataView 类型是一种通用的数组缓冲区视图，其支持所有 8 种数值型数据类型。要使用 DataView，首先要创建一个 ArrayBuffer 实例，然后用这个实例来创建新的 DataView。

如果提供了一个表示比特偏移量的数值，那么可以基于缓冲区的其中一部分来创建视图，DataView 将默认选取从偏移值开始到缓冲区末尾的所有比特。如果额外提供一个表示选取比特数量的可选参数，DataView 则从偏移位置后选取该数量的比特。

```JavaScript
let buffer = new ArrayBuffer(10),
    view = new DataView(buffer);

let buffer = new ArrayBuffer(10),
    view = new DataView(buffer, 5, 2);      // cover bytes 5 and 6
```

获取视图信息。可以通过以下几种只读属性来获取视图的信息。

- buffer - The array buffer that the view is tied to
- byteOffset - The second argument to the DataView constructor, if provided (0 by default)
- byteLength - The third argument to the DataView constructor, if provided (the buffer's byteLength by default)

```JavaScript
let buffer = new ArrayBuffer(10),
    view1 = new DataView(buffer),           // cover all bytes
    view2 = new DataView(buffer, 5, 2);     // cover bytes 5 and 6

console.log(view1.buffer === buffer);       // true
console.log(view2.buffer === buffer);       // true
console.log(view1.byteOffset);              // 0
console.log(view2.byteOffset);              // 5
console.log(view1.byteLength);              // 10
console.log(view2.byteLength);              // 2
```

读取和写入数据。JavaScript 有 8 种数值型数据类型，对于其中的每一种，都能在 DataView 的原型上找到相应的在数组缓冲区中写入数据和读取数据的方法。这些方法都以 set 或 get 开头，紧跟着的是每一种数据类型的缩写。例如，以下这个列表时用于读取和写入 init8 和 unit8 类型数据的方法。

- getInt8(byteOffset, littleEndian) - Read an int8 starting at byteOffset
- setInt8(byteOffset, value, littleEndian) - Write an int8 starting at byteOffset
- getUint8(byteOffset, littleEndian) - Read an uint8 starting at byteOffset
- setUint8(byteOffset, value, littleEndian) - Write an uint8 starting at byteOffset

get 方法接受两个参数：读取数据时偏移的字节数量和一个可选的布尔值，表示是否按照小端序进行读取（小端序是指最低有效字节位于字节 0 的字节顺序）。set 方法接受三个参数：写入数据时偏移的比特数量、写入的值和一个可选的布尔值，表示是否按照小端序格式存储。

定型数组是视图。ECMAScript 6 定型数组实际上是用于数组缓冲区的特定类型的视图，可以强制使用特定的数据类型，而不是使用通用的 DataView 对象来操作数组缓冲区。8 个特定类型的视图对应于 8 种数值型数据类型，uint8 的值还有其他选择。

创建特定类型的视图。定型数组构造函数可以接受多种类型的参数，所以可以通过多种方法来创建定型数组。首先，可以传入 DataView 构造函数可接受的参数来创建新的定型数组，分别是数组缓冲区、可选的比特偏移量、可选的长度值。

创建定型数组的第二种方法是：调用构造函数时传入一个数字。这个数字表示分配给数组的元素数量（不是比特数量），构造函数将创建一个新的缓冲区，并按照数组元素的数量来分配合理的比特数量，通过 length 属性可以访问数组中的元素数量。

第三种创建定型数组的方法是调用构造函数时，将以下任一对象作为唯一的参数传入。

- A Typed Array - Each element is copied into a new element on the new typed array. For example, if you pass an int8 to the Int16Array constructor, the int8 values would be copied into an int16 array. The new typed array has a different array buffer than the one that was passed in.
- An Iterable - The object's iterator is called to retrieve the items to insert into the typed array. The constructor will throw an error if any elements are invalid for the view type.
- An Array - The elements of the array are copied into a new typed array. The constructor will throw an error if any elements are invalid for the type.
- An Array-Like Object - Behaves the same as an array.

## 10.4 定型数组与普通数组的相似之处

定型数组和普通数组有几个相似之处，在许多情况下可以按照普通数组的使用方式去使用定型数组。举个例子，通过 length 属性可以查看定型数组中含有的元素数量，通过数值型索引可以直接访问定型数组中的元素。

```JavaScript
let ints = new Int16Array([25, 50]);

console.log(ints.length);          // 2
console.log(ints[0]);              // 25
console.log(ints[1]);              // 50

ints[0] = 1;
ints[1] = 2;

console.log(ints[0]);              // 1
console.log(ints[1]);              // 2
```

通用方法。定型数组也包括许多在功能上与普通数组方法等效的方法，以下方法均可用于定型数组。

- copyWithin()
- entries()
- fill()
- filter()
- find()
- findIndex()
- forEach()
- indexOf()
- join()
- keys()
- lastIndexOf()
- map()
- reduce()
- reduceRight()
- reverse()
- slice()
- some()
- sort()
- values()

相同的迭代器。定型数据与普通数组有 3 个相同的迭代器，分别是 entries() 方法、keys() 方法和 values() 方法，这意味着可以把定型数组当作普通数组一样来使用展开运算符、for-of 循环。

of() 方法和 from() 方法。此外，所有定型数组都含有静态 of() 方法和 from() 方法，运行效果分别与 Array.of() 方法和 Array.from() 方法相似，区别是定型数组的方法返回定型数组，而普通数组的方法返回普通数组。

## 10.5 定型数组与普通数组的差别

定型数组与普通数组的最重要的差别是：定型数组不是普通数组。它不继承自 Array，通过 Array.isArray() 方法检查定型数组返回的是 false。

行为差异。当操作普通数组时，其可以变大变小，但定型数组却始终保持相同的尺寸。给定型数组中不存在的数值索引赋值会被忽略，而在普通数组中就可以。

缺失的方法。尽管定型数组包含许多与普通数组相同的方法，但也缺失了几个。以下几个方法在定型数组中不可使用：concat()、shift()、pop()、splice()、push()、unshift()。

附加方法。最后，定型数组还有两个没出现在普通数组中的方法：set() 和 subarray()。这两个方法的功能相反，set() 方法将其他数组复制到己有的定型数组，subarray() 提取己有定型数组的一部分作为一个新的定型数组。

# 第 11 章 Promise 与异步编程

JavaScript 有很多强大的功能，其中一个是它可以轻松地搞定异步编程。作为一门为 Web 而生的语言 ，它从一开始就需要能够响应异步的用户交互，如点击和按键操作等。 Node.js 用回调函数代替了事件，使异步编程在 JavaScript 领域更加流行。

Promise 可以实现其他语言中类似 Future 和 Deferred 一样的功能，是另一种异步编程的选择，它既可以像事件和回调函数一样指定稍后执行的代码，也可以明确指示代码是否成功执行。基于这些成功或失败的状态，为了让代码更容易理解和调试，可以链式地编写 Promise。

## 11.1 异步编程的背景知识

JavaScript 引擎是基于单线程（Single-threaded）事件循环的概念构建的，同一时刻只允许一个代码块在执行，与之相反的是像 Java 和 C＋＋ 一样的语言，它们允许多个不同的代码块同时执行。对于基于线程的软件而言，当多个代码块同时访问并改变状态时，程序很难维护并保证状态不会出错。

JavaScript 引擎同一时刻只能执行一个代码块，所以需要跟踪即将运行的代码，那些代码被放在一个任务队列（job queue）中，每当一段代码准备执行时，都会被添加到任务队列。每当 JavaScript 引擎中的一段代码结束执行，事件循环（event loop）会执行队列中的下一个任务，它是 JavaScript 引擎中的一段程序，负责监控代码执行井管理任务队列。请记住，队列中的任务会从第一个一直执行到最后一个。

### 11.1.1 事件模型

用户点击按钮或按下键盘上的按键会触发类似 onclick 这样的事件，它会向任务队列添加一个新任务来响应用户的操作，这是 JavaScript 中最基础的异步编程形式，直到事件触发时才执行事件处理程序，且执行时上下文与定义时的相同。

```js
let button = document.getElementById("my-btn");
button.onclick = function (event) {
  console.log("Clicked");
};
```

在这段代码中，单击 button 后会执行 `console.log("Clicked")`，赋值给 onclick 的函数被添加到任务队列中，只有当前面的任务都完成后它才会被执行。

事件模型适用于处理简单的交互，然而将多个独立的异步调用连接在一起会使程序更加复杂，因为必须跟踪每个事件的事件目标（如示例中的 button ）。此外，必须要保证事件在添加事件处理程序之后才被触发。举个例子，如果先单击 button 再给 onclick 赋值，则任何事情都不会发生。

### 11.1.2 回调模式

Node.js 通过普及回调函数来改进异步编程模型，回调模式与事件模型类似，异步代码都会在未来的某个时间点执行， 二者的区别是回调模式中被调用的函数是作为参数传入的。

```js
readFile("example.txt", function (err, contents) {
  if (err) {
    throw err;
  }

  console.log(contents);
});
console.log("Hi!");
```

此示例使用 Node.js 传统的错误优先（error-first）回调风格。调用 `readFile()` 函数后，`console.log("Hi")`语句立即执行并输出“Hi” ；当 `readFile()` 结束执行时，会向任务队列的末尾添加一个新任务，该任务包含回调函数及相应的参数，当队列前面所有的任务完成后才执行该任务，并最终执行 `console.log(contents)` 输出所有内容 。

回调模式比事件模型更灵活，因为相比之下，通过回调模式链接多个调用更容易。

```js
readFile("example.txt", function (err, contents) {
  if (err) {
    throw err;
  }

  writeFile("example.txt", function (err) {
    if (err) {
      throw err;
    }

    console.log("File was written!");
  });
});
```

虽然这个模式运行效果很不错，但由于嵌套了太多的回调函数，使自己陷入了回调地狱。如果想要实现更复杂的功能，回调函数的局限性同样也会显现出来。

```js
method1(function (err, result) {
  if (err) {
    throw err;
  }

  method2(function (err, result) {
    if (err) {
      throw err;
    }

    method3(function (err, result) {
      if (err) {
        throw err;
      }

      method4(function (err, result) {
        if (err) {
          throw err;
        }

        method5(result);
      });
    });
  });
});
```

像示例中这样嵌套多个方法调用，会创建一堆难以理解和调试的代码。如果想实现更复杂的功能，回调函数的局限性同样也会显现出来，例如，并行执行两个异步操作，当两个操作都结束时才通知；或者同时进行两个异步操作，只取优先完成的操作结果。在这种情况下，需要跟踪多个回调函数并清理这些操作，而 Promise 就能非常好地改进这样的情况。

## 11.2 Promise 的基础知识

Promise 相当于异步操作结果的占位符，它不会去订阅一个事件，也不会传递一个回调函数给目标函数，而是让函数返回一个 Promise 对象，未来对这个对象的操作完全取决于 Promise 的生命周期。

```js
// readFile承诺在未来的某个时刻完成
let promise = readFile("example.txt");
```

### 11.2.1 Promise 的声明周期

每个 Promise 都会经历一个短暂的声明周期：先是处于进行中（pending）的状态，此时操作尚未完成，所以它也是未处理（unsettled）的；一旦异步操作执行结束，Promise 则变成已处理（settled）的状态。操作结束后，Promise 可能会进入到以下两种状态中的其中一个：

- Fulfilled: Promise 异步操作成功完成。
- Rejected: 由于程序错误或一些其他原因，Promise 异步操作未能成功完成。

内部属性`[[PromiseState]]`被用来表示 Promise 的 3 种状态："pending", "fulfilled", 和 "rejected"。这个属性不暴露在 Promise 对象上，所以不能以编程的方式检测 Promise 的状态，只有当 Promise 的状态改变时，通过`then()`方法来采取特定的行动。

所有 Promise 都有`then()`方法，它接受两个参数：第一个是当 Promise 的状态变为 fulfilled 时要调用的函数，与异步操作相关的附加数据都会传递给这个完成函数（fulfillment function）；第二个是当 Promise 的状态变为 rejected 时要调用的函数，其与完成时调用的函数类似，所有与失败状态相关的附加数据都会传递给这个拒绝函数（rejection function）。

> 如果一个对象实现了上诉的 `then()` 方法，那这个对象我们称之为 thenable 对象。所有的 Promise 都是 thenable 对象，但并非所有的 thenable 对象都是 Promise。

`then()`的两个参数都是可选的，所以可以按照任意组合的方式来监听 Promise，执行完成或被拒绝都会被响应。

```js
let promise = readFile("example.txt");

promise.then(
  function (contents) {
    // fulfillment
    console.log(contents);
  },
  function (err) {
    // rejection
    console.error(err.message);
  }
);

promise.then(function (contents) {
  // fulfillment
  console.log(contents);
});

promise.then(null, function (err) {
  // rejection
  console.error(err.message);
});
```

Promise 还有一个 `catch()` 方法，相当于只给其传入拒绝处理程序的 `then()` 方法。例如，下面这个`catch()`方法和`then()`方法实现的功能是等价的：

```js
promise.catch(function (err) {
  // rejection
  console.error(err.message);
});

// 以以下调用相同
promise.then(null, function (err) {
  // rejection
  console.error(err.message);
});
```

`then()`方法和 `catch()`方法一起使用才能更好地处理异步操作结果。这套体系能够清楚地指明操作结果是成功还是失败，比事件和回调函数更好用。如果使用事件，在遇到错误时不会主动触发；如果使用回调函数，则必须要记得每次都检查错误参数。你要知道，如果不给 Promise 添加拒绝处理程序，那所有失败就自动被忽略了，所以一定要添加拒绝处理程序，即使只在函数内部记录失败的结果也行。

如果一个 Promise 处于己处理状态，在这之后添加到任务队列中的处理程序仍将执行。所以无论何时你都可以添加新的完成处理程序或拒绝处理程序，同时也可以保证这些处理程序能被调用。举个例子：

```js
let promise = readFile("example.txt");

// 最初的完成处理程序
promise.then(function(contents) {
  console.log(contents);

  // 现在又添加一个
  promise.then(function(contents) {
    console.log(contents);
  });
});
```

在这段代码中，一个完成处理程序被调用时向同一个 Promise 添加了另一个完成处理程序，此时这个 Promise 已经完成，所以新的处理程序会被添加到任务队列中，当前面的任务完成后其才被调用。这对拒绝处理程序也同样使用。

> 每次调用 `then()` 方法或 `catch()` 方法都会创建一个新任务，当 Promise 被解决（resolved）时执行。这些任务最终会被加入到一个为 Promise 量身定制的独立队列中，这个任务队列的具体细节对于理解如何使用 Promise 而言不重要，通常只要理解任务队列是如何运行的就可以了。

### 11.2.2 创建未完成的 Promise

用 Promise 构造函数可以创建新的 Promise，构造函数只接受一个参数：包含初始化 Promise 代码的执行器（executor）函数。执行器接受两个参数，分别是 `resolve()` 函数和 `reject()` 函数。执行器成功完成时调用 `resolve()` 函数，反之，失败时则调用 `reject()` 函数。

```js
// Node.js 示例
let fs = require("fs");
function readFile(filename) {
  return new Promise(function (resolve, reject) {
    // 触发异步函数
    fs.readFile(filename, { encoding: "utf8" }, function (err, contents) {
      // 检查是否有错误
      if (err) {
        reject(err);
        return;
      }
      // 成功读取文件
      resolve(contents);
    });
  });
}

let promise = readFile("example.txt");

// 同时监听执行完成和执行被拒
promise.then(
  function (contents) {
    // fulfillment
    console.log(contents);
  },
  function (err) {
    // rejection
    console.error(err.message);
  }
);
```

在这个示例中，用 Promise 包裹了一个原生 Node.js 的 `fs.readFile()` 异步调用。如果失败，执行器向 `reject()` 函数传递错误对象；如果成功，执行器想 `resolve()` 函数传递文件内容。

要记住，`readFile()`方法被调用时执行器会立刻执行，在执行器中，无论是调用 `resolve()` 还是`reject()`，都会向任务队列中添加一个任务来解决这个 Promise。像`setTimeout()`或`setInterval()`函数一样，这种是名为任务编排（job scheduling）的过程。当编排任务时，会向任务队列中添加一个新任务，并明确指定将任务延后执行。例如，使用 `setTimeout()` 函数可以指定将任务添加到队列前的延时。

```js
// 500ms 之后将这个函数添加到任务队列
setTimeout(function () {
  console.log("Timeout");
}, 500);
console.log("Hi!");

// Hi!
// Timeout
```

这段代码编排了一个 500ms 后才被添加到任务队列的任务，两次 `console.log()` 调用分别输入内容顺序如上。

Promise 具有类似的工作原理， Promise 的执行器会立即执行，然后才执行后续流程中的代码。

```js
let promise = new Promise(function (resolve, reject) {
  console.log("Promise");
  resolve();
});

promise.then(function () {
  console.log("Resolved.");
});

console.log("Hi!");

// Promise
// Hi!
// Resolved
```

调用 `resolve()` 后回触发一个异步操作，传入`then()`和`catch()`方法的函数会被添加到任务队列中并异步执行。请注意，即使在代码中`then()`调用位于`console.log()`之前，但其与执行器不同，它并没有立即执行。这是因为，完成处理程序和拒绝程序总是在执行器完成后被添加到任务队列的末尾。

### 11.2.3 创建已处理的 Promise

创建未处理 Promise 的最好方法是使用 Promise 的构造函数，这是由于 Promise 执行器具有动态性。但如果你想用 Promise 来表示一个己知值，则编排一个只是简单地给 `resolve()` 函数传值的任务并无实际意义，反倒是可以用以下两种方法根据特定的值来创建己解决 Promise。

**使用Promise.resolve()**

`Promise.resolve()` 方法只接受一个参数并返回一个完成态的 Promise，也就是说不会有任务编排的过程，而且需要向 Promise 添加一至多个完成处理程序来获取值。

```js
let promise = Promise.resolve(42);

promise.then(function (value) {
  console.log(value); // 42
});
```

这段代码创建了一个已完成 Promise，完成处理程序的形参 value 接受了传入值 42，由于该 Promise 永远不会存在拒绝状态，因而该 Promise 的拒绝处理程序永远不会被调用。

**使用Promise.reject()**

也可以使用 `Promise.reject()` 方法来创建已拒绝的 Promise，它与`Promise.resolve()`很像，唯一的区别是创建出来的是拒绝态的 Promise。

```js
let promise = Promise.reject(42);

promise.catch(function (value) {
  console.log(value); // 42
});
```

任何附加到这个 Promise 的拒绝处理程序都将被调用，但却不会调用完成处理程序。

> 如果向 `Promise.resolve()` 或 `Promise.reject()` 方法传递了一个 promise，那么该 promise 不会做任何修改而直接返回。

**非 promise 的 thenable 对象**

`Promise.resolve()` 和 `Promise.reject()` 都可以接收非 promise 的 thenable 对象作为参数。在传递它之后，这些方法在调用`then()`之后创建一个新的 promise ，并在`then()`函数中被调用。

拥有`then()`方法且接受 resolve 和 reject 这两个参数的普通对象就是非 Promise 的 Thenable 对象。

```js
let thenable = {
  then: function (resolve, reject) {
    resolve(42);
  },
};
```

在此示例中，Thenable 对象和 Promise 之间只有`then()`方法这一个相似之处，可以调用`Promise.resolve()`方法将 thenable 对象转换成一个已完成 Promise：

```js
let thenable = {
  then: function (resolve, reject) {
    resolve(42);
  },
};

let p1 = Promise.resolve(thenable);
p1.then(function (value) {
  console.log(value); // 42
});
```

在此示例中，`Promise.resolve()`调用的是 `thenable.then()`，所以 Promise 的状态可以被检测到。由于是在 `then()` 方法内部调用了 `resolve(42)`，因此 Thenable 对象的 Promise 状态是已完成。新创建的已完成状态 Promise p1 从 Thenable 对象接受传入的值（也就是42），p1 的完成处理程序将 42 赋值给形参 value。

可以使用与`Promise.resolve()`相同的过程创建基于 Thenable 对象的己拒绝 Promise。

```js
let thenable = {
  then: function (resolve, reject) {
    reject(42);
  },
};

let p1 = Promise.resolve(thenable);
p1.catch(function (value) {
  console.log(value); // 42
});
```

有了`Proimse.resolve()` 和 `Promise.reject()` 方法，可以更轻松地处理非 promise 的 thenable 对象。很多库都在 promise 被引入 ECMAScript 6 之前就使用了 thenable，所以将 thenable 转化为正式 promise 的向后兼容特性对于这些已存在的库来讲至关重要。如果不确定一个对象是否是 promise，最好的办法就是将该对象传入 `Promise.resolve()` 或 `Promise.reject()`，因为 promise 在这些函数中不会发生任何改变。

### 11.2.4 执行器错误

如果执行器内部抛出一个错误，则 Promise 的拒绝处理程序就会被调用。

```js
let promise = new Promise(function (resolve, reject) {
  throw new Error("Explosion!");
});

promise.catch(function (error) {
  console.log(error.message); // "Explosion!"
});
```

该段代码中，执行函数故意抛出了一个错误。实际上每个执行函数内部都包含一个隐式的 try-catch，因此内部的错误会被捕捉并传入拒绝处理程序。该例等效如下：

```js
let promise = new Promise(function (resolve, reject) {
  try {
    throw new Error("Explosion!");
  } catch (ex) {
    reject(ex);
  }
});

promise.catch(function (error) {
  console.log(error.message); // "Explosion!"
});
```

为了简化这种常见的用例，执行器会捕获所有抛出的错误，但只有当拒绝处理程序时才会记录执行器中抛出的错误，否则错误会被忽略掉。在早期的时候，开发人员使用 Promise 会遇到这种问题，后来 JavaScript 环境提供了一些捕获已拒绝 Promise 的钩子函数来解决这个问题。

## 11.3 全局的 Promise 拒绝处理

有关 Promise 的其中一个最争议的问题是，如果没有拒绝处理程序的情况下拒绝一个 Promise，那么不会提示失败信息。这是 JavaScript 语言中唯一一处没有强制报错的地方，一些人认为这是标准中最大的缺陷。

Promise 的特性决定了很难检测一个 Promise 是否被处理过。

```js
// Promise被立即拒绝
let rejected = Promise.reject(42);

// 在当前，rejected 未被处理

// 一段时间过后...
rejected.catch(function (value) {
  // 现在 rejected 已被处理
  console.log(value);
});
```

任何时候都可以调用`then()`或`catch()`方法，无论 Promise 是否已解决这两个方法都可以正常运行，但这样就很难知道一个 Promise 何时被处理。在此示例中 ，Promise 被立即拒绝，但是稍后才被处理。

尽管这个问题在未来版本的 ECMAScript 中可能会被解决，但是 Node.js 和浏览器环境都已分别做出了一些改变来解决开发者的这个痛点，这些改变不是 ECMAScript6 标准的一部分，不过当使用 Promise 的时候它们确实是非常有价值的工具。

### 11.3.1 Node.js 环境的拒绝处理

在 Node.js 中，处理 Promise 拒绝时会触发 Process 对象中的两个事件：

1. unhandledRejection 在一个事件循环中，当 Promise 被拒绝，并且没有提供拒绝处理程序时被调用。
2. rejectionHandled 在一个事件循环后，当 Promise 被拒绝，并且拥有提供拒绝处理程序时被调用。

设计这些事件是用来识别那些被拒绝却又没被处理过的 Promise 的。

拒绝原因（通常是一个错误对象）及被拒绝的 Promise 作为参数被传入 unhandledRejection 事件处理程序中。

```js
let rejected;

process.on("unhandledRejection", function (reason, promise) {
  console.log(reason.message); // "Explosion!"
  console.log(rejected === promise); // true
});

rejected = Promise.reject(new Error("Explosion!"));
```

rejectionHandled 事件处理程序只有一个参数，就是被拒绝的 Promise。

```js
let rejected;

process.on("rejectionHandled", function (promise) {
  console.log(rejected === promise); // true
});

rejected = Promise.reject(new Error("Explosion!"));

// 等待 rejection 处理的添加
setTimeout(function () {
  rejected.catch(function (value) {
    console.log(value.message); // "Explosion!"
  });
}, 1000);
```

这里的 rejectionHandled 事件在拒绝处理程序最后被调用时触发，如果在创建 rejected 之后直接添加拒绝处理程序，那么该事件不会被触发，因为 rejected 创建的过程与拒绝处理程序的调用在同一个事件循环中，此时 rejectionHandled 事件尚未生效。

通过事件 rejectionHandled 和事件 unhandledRejection 将潜在未处理的拒绝存储为一个列表，等待一段时间后检查列表便能够正确地跟踪潜在的未处理拒绝。例如下面这个简单的未处理拒绝跟踪器。

```js
let possiblyUnhandledRejections = new Map();

// 当 rejection 未处理时，将其添加到 map 中
process.on("unhandledRejection", function (reason, promise) {
  possiblyUnhandledRejections.set(promise, reason);
});

process.on("rejectionHandled", function (promise) {
  possiblyUnhandledRejections.delete(promise);
});

setInterval(function () {
  possiblyUnhandledRejections.forEach(function (reason, promise) {
    console.log(reason.message ? reason.message : reason);

    // 做一些什么来处理这些拒绝
    handleRejection(promise, reason);
  });

  possiblyUnhandledRejections.clear();
}, 60000);
```

这段代码使用 Map 集合来存储 Promise 及其拒绝原因，每个 Promise 键都有一个拒绝原因的相关值。每当触发 unhandledRejection 事件时，会向 Map 集合中添加一组 Promise 及拒绝原因；每当触发 rejectionHandled 事件时，已处理的 Promise 会从 Map 集合中移除。结果是，possiblyUnhandledRejections 会随着事件调用不断扩充或收缩。`setInterval()`调用会定期检查列表，将可能未处理的拒绝输出到控制台(实际上会通过其他方式记录或者直接处理掉这个拒绝)。在这个示例中使用的是 Map 集合而不是 WeakMap 集合，这是因为需要定期检查 Map 集合来确认一个 Promise 是否存在，而这是 WeakMap 无法实现的。

尽管这个示例针对 Node.js 设计，但是浏览器也实现了一套类似的机制来提示开发者哪些拒绝还没有被处理。

### 11.3.2 浏览器环境的拒绝处理

浏览器也是通过触发两个事件来识别未处理的拒绝的，虽然这些事件实在 window 对象上出发的，但实际上与 Node.js 中的完全等效。

1. unhandledrejection 在一个事件循环中，当 Promise 被拒绝，并且没有提供拒绝处理程序时被调用。
2. rejectionHandled 在一个事件循环后，当 Promise 被拒绝，并且拥有提供拒绝处理程序时被调用。

在 Node.js 实现中，事件处理程序接受多个独立参数：而在浏览器中，事件处理程序接受一个有以下属性的事件对象作为参数：

- type 事件名称（“unhandledrejection”或“rejectionHandled”）
- promise 被拒绝的 Promise 对象
- reason 来自 Promise 的拒绝值

浏览器实现中的另一处不同是，在两个事件中都可以使用拒绝值（reason）。

```js
let rejected;

// 也可以使用addEventListener('unhandledrejection')
window.onunhandledrejection = function (event) {
  console.log(event.type); // "unhandledrejection"
  console.log(event.reason.message); // "Explosion!"
  console.log(rejected === event.promise); // true
};

// 也可以使用addEventListener('rejectionhandled')
window.onrejectionhandled = function (event) {
  console.log(event.type); // "rejectionhandled"
  console.log(event.reason.message); // "Explosion!"
  console.log(rejected === event.promise); // true
};

rejected = Promise.reject(new Error("Explosion!"));
```

在浏览器中，跟踪未处理的代码也与 Node.js 中的非常相似。二者都是用同样的方法将 Promise 及其处理值存储在 Map 集合中，然后再进行检索。唯一的区别是，在事件处理程序中检索信息的位置不同。

## 11.4 串联 Promise

每次调用`then()`或`catch()`方法时实际上创建并返回了另一个 Promise，只有当第一个 Promise 完成或被拒绝后，第二个才会被解决。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

p1.then(function (value) {
  console.log(value);
}).then(function () {
  console.log("Finished");
});
```

调用`p1.then()`后返回第二个Promise，紧接着又调用了它的`then()`方法，只有当第一个Promise被解决之后才会调用第二个`then()`方法的完成处理程序。如果将这个示例拆解开，看起来是这样的

```js
let p1 = new Promise(function(resolve, reject) {
  resolve(42);
});
let p2 = p1.then(function(value) {
  console.log(value);
})
p2.then(function() {
  console.log("Finished");
});
```

### 14.1 捕获错误

完成处理程序或拒绝处理程序中可能发生错误，而 Promise 链可以用来捕获这些错误。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

p1.then(function (value) {
  throw new Error("Boom!");
}).catch(function (error) {
  console.log(error.message); // "Boom!"
});
```

在这段代码中，p1的完成处理程序抛出了一个错误，链式调用第二个Promise的`catch()`方法后，可以通过它的拒绝处理程序接收这个错误。如果拒绝处理程序抛出错误，也可以通过相同的方式接收到这个错误：

```js
let p1 = new Promise(function(resolve, reject) {
  throw new Error("Explosion!");
});
p1.catch(function(error) {
  console.log(error.message); // "Explosion!"
  throw new Error("Boom!");
}).catch(function(error) {
  console.log(error.message); // "Boom!"
});
```

> 务必在 Promise 链的末尾留有一个拒绝处理程序以确保能够正确处理所有可能发生的错误。

### 14.2 Promise 链的返回值

Promise 链的另一个重要特性是可以给下游 Promise 传递数据，从执行器`resolve()`处理程序到 Promise 完成处理程序的数据传递，如果在完成处理程序中指定一个返回值，则可以沿着这条链继续传递数据。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

p1.then(function (value) {
  console.log(value); // "42"
  return value + 1;
}).then(function (value) {
  console.log(value); // "43"
});
```

在拒绝处理程序中也可以做相同的事情。在必要时，即使其中一个 Promise 失败也能恢复整条链的执行。

### 14.3 在 Promise 链中返回 Promise

在 Promise 间可以通过完成和拒绝程序中返回的原始值来传递数据。但是如果返回的是 Promise 对象，会通过一个额外的步骤来确定下一步怎么走。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

let p2 = new Promise(function (resolve, reject) {
  resolve(43);
});

p1.then(function (value) {
  // 首个完成处理程序
  console.log(value); // 42
  return p2;
}).then(function (value) {
  // 第二个完成处理程序
  console.log(value); // 43
});
```

在这段代码中，p1编排的任务解决并传入42，然后p1的完成处理程序返回一个已解决状态的Promise p2，由于p2已经被完成，因此第二个完成处理程序被调用。如果p2被拒绝，则调用拒绝处理程序

关于这个模式，最需要注意的是，第二个完成处理程序被添加到了第三个Promise而不是p2，所以之前的示例等价于：

```js
let p1 = new Promise(function(resolve, reject) {
  resolve(42);
});
let p2 = new Promise(function(resolve, reject) {
  resolve(43);
});
let p3 = p1.then(function(value) {
  // 第一个完成处理函数
  console.log(value); // 42
  return p2;
});
p3.then(function(value) {
  // 第二个完成处理函数
  console.log(value); // 43
});
```

很明显的是，此处第二个完成处理程序被添加到p3而非p2，这个差异虽小但非常重要，如果p2被拒绝那么第二个完成处理程序将不会被调用。

在完成或拒绝处理程序中返回 Thenable 对象不会改变 Promise 执行器的执行时机，先定义的 Promise 的执行器先执行，后定义的后执行，以此类推。返回Thenable对象仅允许为这些promise结果定义额外的响应。在完成处理程序中创建新的Promise可以推迟完成处理程序的执行。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

p1.then(function (value) {
  console.log(value); // 42

  // 创建一个新的 Promise
  let p2 = new Promise(function (resolve, reject) {
    resolve(43);
  });

  return p2;
}).then(function (value) {
  console.log(value); // 43
});
```

## 11.5 响应多个 Promise

如果想通过监听多个 Promise 来决定下一步的操作，则可以使用 ES6 提供的`Promise.all()`和`Promise.race()`方法来监听多个 Promise。

### 11.5.1 Promise.all()方法

`Promise.all()`方法只接受一个参数并返回一个 Promise，该参数是一个含有多个受监视 Promise 的可迭代对象（如数组），只有当可迭代对象中所有 Promise 都被解决后返回的 Promise 才会被解决，只有当可迭代对象中所有 Promise 都被完成后返回的 Promise 才会被完成。

```js
et p1 = new Promise(function(resolve, reject) {
    resolve(42);
});

let p2 = new Promise(function(resolve, reject) {
    resolve(43);
});

let p3 = new Promise(function(resolve, reject) {
    resolve(44);
});

let p4 = Promise.all([p1, p2, p3]);

p4.then(function(value) {
    console.log(Array.isArray(value));  // true
    console.log(value[0]);              // 42
    console.log(value[1]);              // 43
    console.log(value[2]);              // 44
});
```

在这段代码中，每个Promise解决时都传入一个数字，调用`Promise.all()`方法创建Promise p4，最终当Promise p1、p2和p3都处于完成状态后p4才被完成。传入p4完成处理程序的结果是一个包含每个解决值(42、43和44)的数组，这些值按照Promise被解决的顺序存储，所以可以根据每个结果来匹配对应的Promise。

所有传入`Promise.all()`方法的 Promise 只要有一个被拒绝，那么返回的 Promise 没等所有 Promise 都完成就立即被拒绝了。

```js
let p1 = new Promise(function (resolve, reject) {
  resolve(42);
});

let p2 = new Promise(function (resolve, reject) {
  reject(43);
});

let p3 = new Promise(function (resolve, reject) {
  resolve(44);
});

let p4 = Promise.all([p1, p2, p3]);

p4.catch(function (value) {
  console.log(Array.isArray(value)); // false
  console.log(value); // 43
});
```

在这个示例中，p2被拒绝并传入值43，没等p1或p3结束执行，p4的拒绝处理程序就立即被调用。(p1和p3的执行过程会结束，只是p4并未等待)。

拒绝处理程序总是接受一个值而非数组，该值来自被拒绝Promise的拒绝值。在本示例中，传入拒绝处理程序的43表示该拒绝来自p2。

### 11.5.2 Promise.race()方法

`Promise.race()`方法监听多个 Promise 的方法稍有不同，它也接受多个受监视 Promise 的可迭代对象作为唯一参数并返回一个 Promise，但只要有一个 Promise 被解决返回的 Promise 就被解决，无须等到所有 Promise 都被完成。一旦数组中的某个 Promise 被完成，`Promise.race()`方法也会像`Promise.all()`方法一样返回一个特定的 Promise。

```js
let p1 = Promise.resolve(42);

let p2 = new Promise(function (resolve, reject) {
  resolve(43);
});

let p3 = new Promise(function (resolve, reject) {
  resolve(44);
});

let p4 = Promise.race([p1, p2, p3]);

p4.then(function (value) {
  console.log(value); // 42
});
```

在这段代码中，p1创建时便处于已完成状态，其他Promise用于编排任务。随后，p4的完成处理程序被调用并传入值42，其他Promise则被忽略。实际上，传给`Promise.race()`方法的Promise会进行竞选，以决出哪一个先被解决，如果先解决的是已完成Promise，则返回己完成Promise；如果先解决的是已拒绝Promise，则返回已拒绝Promise。

```js
let p1 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve(42);
  }, 100);
});

let p2 = new Promise(function (resolve, reject) {
  reject(43);
});

let p3 = new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve(44);
  }, 50);
});

let p4 = Promise.race([p1, p2, p3]);

p4.catch(function (value) {
  console.log(value); // 43
});
```

## 11.6 自 Promise 继承

Promise与其他内建类型一样，也可以作为基类派生其他类，所以可以定义自己的Promise变量来扩展内建Promise的功能。例如，假设创建一个既支持`then()`方法和`catch()`方法又支持`success()`方法和`failure()`方法的Promise，则可以这样创建该Promise类型：


```js
class MyPromise extends Promise {
  // 使用默认的构造函数
  success(resolve, reject) {
    return this.then(resolve, reject);
  }
  failure(reject) {
    return this.catch(reject);
  }
}

let promise = new MyPromise(function (resolve, reject) {
  resolve(42);
});

promise
  .success(function (value) {
    console.log(value); // 42
  })
  .failure(function (value) {
    console.log(value);
  });
```

在这个示例中，派生自Promise的MyPromise扩展了另外两个方法模仿`resolve()`的`success()`方法以及模仿`reject()`的`failure()`方法。

这两个新增方法都通过this来调用它模仿的方法，派生Promise与内建Promise的功能一样，只不过多了`success()`和`failure()`这两个可以调用的方法。

由于静态方法会被继承，因此派生的Promise也拥有`MyPromise.resolve()`、`MyPromise.reject()`、`MyPromise.race()`和`MyPromise.all()` 这 4 个方法，后二者与内建方法完全一致，而前二者却稍有不同。

由于`MyPromise.resolve()`方法和`MyPromise.reject()`方法通过`Symbol.species`属性来决定返回Promise的类型，故调用这两个方法时无论传入什么值都会返回一个MyPromise的实例。如果将内建Promise作为参数传入其他方法，则这个Promise将被解决或拒绝，然后该方法将会返回一个新的MyPromise，于是就可以给它的成功处理程序及失败处理程序赋值。例如：

```js
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});
let p2 = MyPromise.resolve(p1);
p2.success(function(value) {
    console.log(value); // 42
});
console.log(p2 instanceof MyPromise); // true
```

这里的p1是一个内建Promise，被传入`MyPromise.resolve()`方法后得到结果p2，它是MyPromise的一个实例，来自p1的解决值被传入完成处理程序。

传入`MyPromise.resolve()`方法或`MyPromise.reject()`方法的MyPromise实例未经解决便直接返回。在其他方面，这两个方法的行为与`Promise.resolve()`和`Promise.reject()`很像。

## 11.7 基于 Promise 的异步任务执行

在异步任务执行中可以使用生成器。

```js
let fs = require("fs");

function run(taskDef) {
  // 创建迭代器，使其在作用域其它部分可用。
  let task = taskDef();
  // 任务开始
  let result = task.next();
  // 递归函数并持续调用 next()
  function step() {
    // 如果还有工作要做
    if (!result.done) {
      if (typeof result.value === "function") {
        result.value(function (err, data) {
          if (err) {
            result = task.throw(err);
            return;
          }

          result = task.next(data);
          step();
        });
      } else {
        result = task.next(result.value);
        step();
      }
    }
  }
  // 开始递归
  step();
}

// 定义任务运行器需要的函数
function readFile(filename) {
  return function (callback) {
    fs.readFile(filename, callback);
  };
}

// 运行一个任务
run(function* () {
  let contents = yield readFile("config.json");
  doSomethingWith(contents);
  console.log("Done");
});
```

这个实现会导致一些问题。首先，在返回值是函数的函数中包裹每一个函数会令人感到困惑。其次，无法区分用作任务执行器回调函数的返回值和一个不是回调函数的返回值。

只要每个异步操作都返回Promise，就可以极大地简化并通用化这个过程。以Promise作为通用接口用于所有异步代码可以简化任务执行器。

```js
let fs = require("fs");

function run(taskDef) {
  // 创建迭代器
  let task = taskDef();
  // 开始任务
  let result = task.next();
  // 使用函数递归进行迭代
  (function step() {
    // 如果还有工作要做
    if (!result.done) {
      // 使用 resolve() 来简化 promise 的处理
      let promise = Promise.resolve(result.value);
      promise
        .then(function (value) {
          result = task.next(value);
          step();
        })
        .catch(function (error) {
          result = task.throw(error);
          step();
        });
    }
  })();
}

// 定义任务运行器需要的函数
function readFile(filename) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filename, function (err, contents) {
      if (err) {
        reject(err);
      } else {
        resolve(contents);
      }
    });
  });
}

// 运行一个任务
run(function* () {
  let contents = yield readFile("config.json");
  doSomethingWith(contents);
  console.log("Done");
});
```

在这个版本的代码中，一个通用的run()函数执行生成器创建了一个迭代器，它调用task.next()方法来启动任务并递归调用step()方法直到迭代器完成

在step()函数中，如果有更多任务，那么result.done的值为false，此时的result.value应该是一个Promise，调用Promise.resolve()是为了防止函数不返回Promise。(传入Promise.resolve()的Promise直接通过，传入的非Promise会被包裹成一个Promise)接下来，添加完成处理程序提取Promise的值并将其传回迭代器。然后在step()函数调用自身之前结果会被赋值给下一个生成的结果

拒绝处理程序将所有拒绝结果存储到一个错误对象中，然后通过task.throw()方法将错误对象传回迭代器，如果在任务中捕获到错误，结果会被赋值给下一个生成结果。最后继续在catch()内部调用step()函数

这个run()函数可以运行所有使用yield实现异步代码的生成器，而且不会将Promise或回调函数暴露给开发者。事实上，由于函数调用的返回值总会被转换成一个Promise，因此可以返回一些非Promise的值，也就是说，用yield调用同步或异步方法都可以正常运行，永远不需要检查返回值是否为Promise

唯一需要关注的是像readFile()这样的异步函数，其返回的是一个能被正确识别状态的Promise，所以调用Node.js的内建方法时不能使用回调函数，须将其转换为返回Promise的函数

> 未来的异步任务执行  
> JavaScript 正在引入一种用于执行异步任务的更简单的语法，例如，await语法致力于替代基于Promise的示例。其基本思想是用async标记的函数代替生成器，用await代替yield来调用函数

```js
(async function() {
    let contents = await readFile("config.json");
    doSomethingWith(contents);
    console.log("Done");
});
```

> 在函数前添加关键字async表示该函数以异步模式运行，await关键字表示调用readFile("config.json")的函数应该返回一个Promise，否则，响应应该被包裹在Promise中。如果Promise被拒绝则await应该抛出错误，否则通过Promise来返回值。最后的结果是，可以按照同步方式编写异步代码，唯一的开销是一个基于迭代器的状态机

## 11.8 小结

Promise 的设计目标是改进 JavaScript 中的异步变成，它能够让你更好地掌握并组合多个同步操作，比事件系统和回调更使用。Promise 编排的任务会被添加到 JavaScript 引擎任务队列并在未来之星，还有一个任务队列用于跟踪 Promise 的完成处理程序和拒绝处理程序并确保正确执行。

Promise 有3个状态：进行中（pending）、已完成（fulfilled）和已拒绝（rejected）。Promise 的起始状态是进行中，执行成功会变为已完成，失败则变为已拒绝。在后两种情况下都可以添加处理程序，以便当 Promise 被解决（settled）时做出相应操作，通过`then()`方法可以添加完成处理程序或拒绝处理程序，通过`catch()`方法只能添加拒绝处理程序。

有多种方法可将 Promise 链接在一起并在它们之间传递信息，每次调用`then()`方法会创建并返回一个新的 Promise，它会随前面 Promise 被解决而解决。这样的链条可用于触发一系列同步事件的相应，也可通过`Promise.race()`方法和`Promise.all()`方法来监控多个 Promise 的进程并作出相应响应。

由于 Promise 可以提供异步操作能返回的通用接口，因而将生成器和 Promise 结合后会进一步简化异步任务执行的过程，随后可用生成器和 yield 运算符来等待异步响应并做出相应反应。

大多数新的 Web API 都基于 Promise 构建，可以预期在未来会有更多的效仿者出现。

# 第 12 章 代理（Proxy）和反射（Reflection）API

## 12.1 数组问题

## 12.2 代理和反射

## 12.3 创建一个简单的代理

## 12.4 使用 set 陷阱验证属性

## 12.5 用 get 陷阱验证对象结构（Object Shape）

## 12.6 使用 has 陷阱隐藏已有属性

## 12.7 用 deleteProperty 陷阱防止删除属性

## 12.8 原型代理陷阱

-- 原型代理陷阱的运行机制
-- 为什么有两组方法

## 12.9 对象可扩展性陷阱

-- 两个基础示例
-- 重复的可扩展性方法

## 12.10 属性描述符陷阱

-- 给 Object.defineProperty()添加限制
-- 描述符对象限制
-- 重复的描述符方法

## 12.11 ownKeys 陷阱

## 12.12 函数代理中的 apply 和 construct 陷阱

-- 验证函数参数
-- 不用 new 调用构造函数
-- 覆写抽象基类构造函数
-- 可调用的类构造函数

## 12.13 可撤销代理

## 12.14 解决数组问题

-- 检测数组索引
-- 添加新元素时增加 length 的值
-- 减少 length 的值来删除元素
-- 实现 MyArray 类

## 12.15 将代理用作原型

-- 在原型上使用 get 陷阱
-- 在原型上使用 set 陷阱
-- 在原型上使用 has 陷阱
-- 将代理用作类的原型

# 第 13 章 用模块封装代码

在 ECMAScript 6 以前，在应用程序的每一个 JavaScript 中定义的一切都共享一个全局作用域。JavaScript 用“共享一切”的方法加载代码，这是该语言中最容易出错且令人感到困惑的地方。

## 13.1 什么是模块

模块是自动运行在严格模式下并且没有办法退出运行的 JavaScript 代码。与共享一切框架相反的是，在模块顶部创建变量不会自动被添加到全局共享作用域，这个变量仅在模块的顶级作用域中存在，而且模块必须导出一些外部代码可以访问的元素，如变量或函数。模块也可以从其他模块导入绑定。

另外两个模块的特性与作用域关系不大，但也很重要。

- 在模块的顶部， this 的值是 undefined
- 模块不支持 HTML 风格的代码注释

脚本，也就是任何不是模块的 JavaScript 代码，则缺少这些特性。模块和其他 JavaScript 代码之间的差异可能乍一看不起眼，但是它们代表了 JavaScript 代码加载和求值的一个重要变化。模块真正的魔力所在是仅导出和导入需要的绑定，而不是将所用东西都放到一个文件。只有很好地理解了导出和导入才能理解模块与脚本的区别。

## 13.2 导出的基本语法

可以用 export 关键字将一部分己发布的代码暴露给其他模块，在最简单的用例中，可以将 export 放在任何变量、函数或类声明的前面，以将它们从模块导出。

```js
// 导出数据
export var color = "red";
export let name = "Nicholas";
export const magicNumber = 7;

// 导出函数
export function sum(num1, num2) {
    return num1 + num1;
}

// 导出类
export class Rectangle {
    constructor(length, width) {
        this.length = length;
        this.width = width;
    }
}

// 该函数是模块私有的
function subtract(num1, num2) {
    return num1 - num2;
}

// 定义一个函数...
function multiply(num1, num2) {
    return num1 * num2;
}

// ...并在之后导出它
export multiply;
```

除了 export 关键字外，每一个声明与脚本中的一模一样。因为导出的函数和类声明需要有一个名称，所以代码中的每一个函数或类也确实有这个名称。除非用 default 关键字，否则不能用这个语法导出匿名函数或类。

另外，`multiply()`函数在定义时没有马上导出。由于不必总是导出声明，可以导出引用，因此这段代码可以运行。但是，这个示例并未导出`subtract()`函数，任何未显式导出的变量、函数或类都是模块私有的，无法从模块外部访问。

## 13.3 导入的基本语法

从模块中导出的功能可以通过 import 关键字在另一个模块中访问，import 语句的两个部分分别是：要导入的标识符和应当从哪个模块导入。

```js
import { identifier1, identifier2 } from "./example.js";
```

import 后面的大括号表示从给定模块导入的绑定（binding），关键字 from 表示从哪个模块导入给定的绑定，该模块由表示模块路径的字符串指定（被称作模块说明符）。浏览器使用的路径格式与传给`<script>`元素的相同，也就是说，必须把文件扩展名也加上。另一方面，Node.js 则遵循基于文件系统前缀区分本地文件和包的惯例。例如，`example` 是一个包而`.／example.js`是一个本地文件 。

导入绑定的列表看起来与解构对象很相似，但它不是。当从模块中导入一个绑定时，它就好像使用 const 定义的一样，无法定义另一个同名变量 （包括导入另一个同名绑定），也无法在 import 时语句前使用标识符或改变绑定的值。

### 13.3.1 导入单个绑定

可以导入并以多种方式使用这个模块中的绑定。例如，可以只导入一个标识符。但是如果尝试赋新值，结果是抛出一个错误，因为不能给导入的绑定重新赋值。

为了最好地兼容多个浏览器和 Node.js 环境，一定要在字符串之前包含`/`、`./`或`../`来表示要导入的文件。

```js
// 只引入单个标识符
import { sum } from "./example.js";

console.log(sum(1, 2)); // 3

sum = 1; // 错误
```

### 13.3.2 导入多个绑定

如果想从模块中导入多个绑定，则可以明确地将它们列出来。

```js
// 引入多个绑定
import { sum, multiply, magicNumber } from "./example.js";
console.log(sum(1, magicNumber)); // 8
console.log(multiply(1, 2)); // 2
```

### 13.3.3 导入整个模块

特殊情况下，可以导入整个模块作为一个单一的对象，然后所有的导出都可以作为对象的属性使用。

```js
// 导入一些
import * as example from "./example.js";
console.log(example.sum(1, example.magicNumber)); // 8
console.log(example.multiply(1, 2)); // 2
```

但是无论在 import 语句中把一个模块写了多少次，该模块将只执行一次。导入模块的代码执行后，在实例化的模块被保存在内存中，只要另一个 import 语句引用它就可以重复使用，这些模块将使用相同的模块实例。

模块语法的限制。export 和 import 的一种重要的限制是，它们必须在其他语句和函数之外使用。同样，只能在顶部使用。出于同样的原因，不能动态地导入或导出模块。export 和 import 关键字被设计成静态的。

### 13.3.4 导入绑定的一个微妙怪异之处

ECMAScript 6 的 import 语句为变量、函数和类创建的是只读绑定，而不是像正常变量一样简单地引用原始绑定。标识符只有在被导出的模块中可以修改，即使是导入绑定的模块也无法更改绑定的值。

```js
export var name = "Nicholas";
export function setName(newName) {
  name = newName;
}
```

```js
import { name, setName } from "./example.js";

console.log(name); // "Nicholas"
setName("Greg");
console.log(name); // "Greg"

name = "Nicholas"; // 错误
```

## 13.4 导出和导入时重命名

有时候，从一个模块导入变量、函数或者类时，我们可能不希望使用它们的原始名称。幸运的是，可以在导出过程和导入过程中改变导出元素的名称。

假设要使用不同的名称导出一个函数，则可以用 as 关键字来指定函数在模块外应该被称为什么名称。

```js
function sum(num1, num2) {
  return num1 + num2;
}

export { sum as add };
```

如果模块想使用不同的名称来导入函数。

```js
import { add as sum } from "./example.js";
console.log(typeof add); // "undefined"
console.log(sum(1, 2)); // 3
```

## 13.5 模块的默认值

由于在诸如 CommonJS （浏览器外的另一个 JavaScript 使用规范）的其他模块系统中，从模块中导出和导入默认值是一个常见的做法，该语法被进行了优化。模块的默认值指的是通过 default 关键宇指定的单个变量、函数或类，只能为每个模块设置一个默认的导出值，导出时多次使用 default 关键字是一个语法错误。

### 13.5.1 导出默认值

在重命名导出时标识符 default 具有特殊含义，用来指示模块的默认值。由于 default 是 JavaScript 中的默认关键字，因此不能将其用于变量、函数或类的名称：但是，可以将其用作属性名称。所以用 default 来重命名模块是为了尽可能与非默认导出的定义一致。如果想在一条导出语句中同时指定多个导出（包括默认导出），这个语法非常有用。

```js
// 函数被模块所代表，不需要名称
export default function (num1, num2) {
  return num1 + num2;
}
```

```js
// 添加默认导出值得标识符
function sum(num1, num2) {
  return num1 + num2;
}
export default sum;
```

```js
// 使用重命名语法
function sum(num1, num2) {
  return num1 + num2;
}
export { sum as default };
```

### 13.5.2 导入默认值

本地名称 sum 用于表示模块导出的任何默认函数，这种语法是最纯净的，ECMAScript 6 的创建者希望它能够成为 Web 上主流的模块导入形式，并且可以使用己有的对象。

```js
// 引入默认值
import sum from "./example.js";

console.log(sum(1, 2)); // 3
```

对于导出默认值和一或多个非默认绑定的模块，可以用一条语句导入所有导出的绑定。

```js
export let color = "red";

export default function (num1, num2) {
  return num1 + num2;
}
```

可以使用下面的 import 语句同时引入 color 和 默认输出的函数。用逗号将默认的本地名称与大括号包裹的非默认值分隔开，请记住 ， 在 import 语句中，默认值必须排在非默认值之前。

```js
import sum, { color } from "./example.js";

console.log(sum(1, 2)); // 3
console.log(color); // "red"
```

与导出默认值一样， 也可以在导入默认值时使用重命名语法。

```js
import { default as sum, color } from "example";

console.log(sum(1, 2)); // 3
console.log(color); // "red"
```

## 13.6 重新导出一个绑定

最终，可能需要重新导出模块己经导入的内容。例如，你正在用几个小模块创建一个库， 则可以用本章己经讨论的模式重新导出己经导入的值。这种形式的 export 在指定的模块中查找声明，然后将其导出。当然，对于同样的值也可以以不同的名称导出。注意的是，如果导出一切时，原模块有默认的导出值，则使用该语句将无法重新定义一个新的默认导出。

```js
import { sum } from "./example.js";
export { sum };

// 单条语句完成任务
export { sum } from "./example.js";

// sum从example.js导入，再将add这个名字导出
export { sum as add } from "./example.js";

// 导出一个模块汇总的所有值
export * from "./example.js";
```

## 13.7 无绑定导入

某些模块可能不导出任何东西，相反，它们可能只修改全局作用域中的对象。尽管模块中的顶层变量、函数和类不会自动地出现在全局作用域中，但这并不意味着模块无法访问全局作用域。内建对象（如 Array 和 Object ）的共事定义可以在模块中访问，对这些对象所做的更改将反映在其他模块中。

```js
// module code without exports or imports
Array.prototype.pushAll = function (items) {
  // items must be an array
  if (!Array.isArray(items)) {
    throw new TypeError("Argument must be an array.");
  }

  // use built-in push() and spread operator
  return this.push(...items);
};
```

即使没有任何导出或导入的操作，这也是一个有效的模块。这段代码既可以用作模块也可以用作脚本。由于它不导出任何东西，因而可以使用简化的导入操作来执行模块代码，而且不导入任何的绑定。

```js
import "./example.js";

let colors = ["red", "green", "blue"];
let items = [];

items.pushAll(colors);
```

无绑定导入最有可能被应用于创建 Polyfill 和 Shim。polyfill 是一段代码（或者插件），提供了那些开发者们希望浏览器原生提供支持的功能。Shim 指的是在一个旧的环境中模拟出一个新 API ，而且仅靠旧环境中已有的手段实现，以便所有的浏览器具有相同的行为。

## 13.8 加载模块

虽然 ECMAScript 6 定义了模块的语法，但它并没有定义如何加载这些模块。这正是规范复杂性的一个体现，应由不同的实现环境来决定。

### 13.8.1 在 Web 浏览器中使用模块

即使在 ECMAScript 6 出现以前， Web 浏览器也有多种方式可 以将 JavaScript 包含在 Web 应用程序中 ， 这些脚本加载的方法分别是：

- 在`<script>`元素中通过 src 属性指定一个加载代码的地址来加载 JavaScript 代码文件 。
- 将 JavaScript 代码内嵌到没有 src 属性的`<script>`元素中。
- 通过 Web Worker 或 Service Worker 的方法加载并执行 JavaScript 代码文件。

在`<script>`中使用模块。主要有两种方式，元素以可以执行内联代码或加载 src 中指定的文件，同时 type 属性的值为“module”时即可支持加载模块。 此外，当无法识别 type 的值时，浏览器会忽略`<script>`元素 ，因此不支持模块的浏览器将自动忽略`<script type="module">`未提供良好的向后兼容性 。

```html
<!-- 加载一个 JavaScript 模块文件 -->
<script type="module" src="module.js"></script>

<!-- 包含一个模块内联代码 -->
<script type="module">
  import { sum } from "./example.js";

  let result = sum(1, 2);
</script>
```

Web 浏览器中的模块加载顺序。模块与脚本不同，它是独一无二的，可以通过 import 关键字来指明其所依赖的其他文件，并且这些文件必须被加载进该模块才能正确执行。为了支持该功能 ，`<script type="module">`执行时自动应用 defer 属性。模块文件便开始下载，直到文档被完全解析模块才会执行。模块按照它们出现在 HTML 文件中的顺序执行。

```html
<!-- 最先执行 -->
<script type="module" src="module1.js"></script>

<!-- 第二个执行 -->
<script type="module">
  import { sum } from "./example.js";

  let result = sum(1, 2);
</script>

<!-- 第三个执行 -->
<script type="module" src="module2.js"></script>
```

每个模块都可以从一个或多个其他的模块导入，这会使问题复杂化。因此，首先解析模块以识别所有导入语句：然后，每个导入语句都触发一次获取过程（从网络或从缓存），并且在所有导入资源都被加载和执行后才会执行当前模块。

Web 浏览器中的异步模块加载。当`<script>`元素的 async 属性应用于脚本时，脚本文件将在文件完全下载并解析后执行。文档中 async 脚本的顺序不会影响脚本执行的顺序，脚本在下载完成后立即执行，而不必等待包含的文档完成解析。

async 属性也可以应用在模块上，在`<script type="module">`元素上应用 async 属性会让模块以类似于脚本的方式执行，唯一的区别是，在模块执行前，模块中所有的导入资源都必须下载下来。这可以确保只有当模块执行所需的所有资源都下载完成后才执行模块 ，但不能保证的是模块的执行时机。

```html
<!-- 无法确定哪个模块会首先运行 -->
<script type="module" async src="module1.js"></script>
<script type="module" async src="module2.js"></script>
```

将模块作为 Woker 加载。Worker，例如 Web Worker 和 Service Woker，可以在网页上下文之外执行 JavaScript 代码。创建新 Worker 的步骤包括：创建一个新的 Worker 实例（或其他的类），传入 JavaScript 文件的地址。默认的加载机制是按照脚本的方式加载文件。

```js
// 以 script 的方式加载 script.js
let worker = new Worker("script.js");
```

为了支持加载模块，HTML 标准的开发者向这些构造函数添加了第二个参数，第二个参数是一个对象，其 type 属性的默认值为“script”。可以将 type 设置为“module”来加载模块文件。

```js
// 以模块的方式加载 module.js
let worker = new Worker("module.js", { type: "module" });
```

Worker 模块通常与 Worker 脚本一起使用，但也有一些例外。首先，Worker 脚本只能从与引用的网页相同的源加载，但是 Worker 模块不会完全受限，虽然 Worker 模块具有相同的默认限制，但它们还是可以加载并访问具有适当的跨域资源共享（CORS）头的文件；其次，尽管 Worker 脚本可以使用 `self.importScripts()` 方法将其他脚本加载到 Worker 中，但`self.importScripts()`却始终无法加载 Worker 模块，因为应该使用 import 来导入。

### 13.8.2 浏览器模块说明符解析

模块说明符（module specifier）使用的都是相对路径（例如，字符串 “./example.js”），浏览器要求模块说明符具有以下几种格式之一。

- 以`/`开头的解析为从根目录开始。
- 以`./`开头的解析为从当前目录开始。
- 以`../`开头的解析为从父目录开始。
- URL 格式。

故此，一些看起来正常的模块说明符在浏览器中实际上是无效的，井且会导致错误。

```js
// 无效的 开头未使用 /，./，或 ../
import { first } from "example.js";

// 无效的 开头未使用 /，./，或 ../
import { second } from "example/index.js";
```

由于这两个模块说明符的格式不正确（缺少正确的起始字符），因此它们无法被浏览器加载，即使在`<script>`标签中用作 src 的值时二者都可以正常工作。`<script>`标签和 import 之间的这种行为差异是有意为之。

# 附录 A ECMAScript 6 中较小的改动

# 附录 B 了解 ECMAScript 7（2016）
