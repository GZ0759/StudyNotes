> 深入理解ES6
> Understanding ES6
> 2017年7月第一版

# 第一章 块级作用域绑定

## 1.1 var声明及变量提升（Hoisting）机制

在函数作用域或全局作用域中通过关键宇 var 声明的变量，无论实际上是在哪里声明的，都会被当成在当前作用域顶部声明的变量，这就是我们常说的提升（Hoisting）机制 。 

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
```



## 1.2 块级声明

块级声明用于声明在指定块的作用域之外无法访问的变量。块级作用域（也被称为词法作用域）存在于：函数内部、块中（字符 { 和 } 之间的区域）。很多类C语言都有块级作用域，而ECMAScript 6 引入块级作用域就是为了让 JavaScript 更灵活也更普适。

let 声明。let 声明的用法与 var 相同。使用 let 来代替声明变量，就可以把变量的作用域限制在当前代码块中。由于 let 声明不会被提升，因此开发者通常将 let 声明语句放在封闭代码块的顶部，以便整个代码块都可以访问。

禁止重声明。假设作用域中已经存在某个标识符，此时再使用 let 关键字声明它机会抛出错误。但如果当前作用域内嵌另一个作用域，便可在内嵌的作用域中用 let 声明同名变量。

const 声明。使用 cons 声明的是常量，其值一旦被设定后不可更改。因此，每个通过 const 声明的变量必须进行初始化。

const 和 let 声明的都是块级标识符，所以常量也只在当前代码块内有效，一旦执行到块外立即被销毁。常量同样也不会被提升至作用域顶部。

与 let 相似，在同一作用域用 const 声明已经存在的标识符也会导致语法错误，无论该标识符是使用 var，还是 let 声明的。

const 声明与 let 声明有一处很大的不同，即无论在严格模式还是在非严格模式下，都不可以为 const 定义的常量再赋值，否则会抛出错误。但是，JavaScript 中的常量如果是对象，则对象中的值可以修改。

```javascript
const person = {
    name: "Nicholas"
};

// works
person.name = "Greg";

// throws an error
person = {
    name: "Greg"
};
```



临时死区TDZ。与 var 不同，let 和 const 声明的变量不会被提升到作用域顶部，如果在声明之前访问这些变量，即使是相对安全的 typeof 操作符也会触发引用错误。但在 let 声明的作用域外对该变量使用 typeof 则不会报错。

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
    funcs.push(function() { console.log(i); });
}

funcs.forEach(function(func) {
    func();     // outputs the number "10" ten times
});
```



为了解决这个问题，开发者们在循环中使用立即调用函数表达式（IIFE），以强制生成计算器变量的副本。在循环内部，IIFE 表达式为接受的每一个变量 i 都创建了一个副本并存储为变量 value。这个变量的值就是相应迭代创建的函数所使用的值。

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
    funcs.push((function(value) {
        return function() {
            console.log(value);
        }
    }(i)));
}

funcs.forEach(function(func) {
    func();     // outputs 0, then 1, then 2, up to 9
});
```



循环中的 let 声明。let 声明模仿上述实例中 IIFE 所做的一切来简化循环过程，每次迭代循环都会创建一个新变量，并以之前迭代中的同名变量的值将其初始化。这意味着彻底删除 IIFE 之后仍可得到预期中的结果。每次循环的时候 let 声明都会创建一个新变量 i，并将其初始化为 i 的当前值，每次循环内部创建的每隔函数都能得到属于它们自己的 i 的副本。对于 for-in 循环和 for-of 循环来说也是一样的。

```javascript
var funcs = [];

for (let i = 0; i < 10; i++) {
    funcs.push(function() {
        console.log(i);
    });
}

funcs.forEach(function(func) {
    func();     // outputs 0, then 1, then 2, up to 9
})
```



循环中的 const 声明。对于普通的 for 循环来说，可以在初始化变量时使用 const，但是更改这个变量的值就会抛出错误。在 for-in 或 for-of 循环中使用 const 时的行为与使用 let 一致，唯一的区别是在循环内不能改变变量的值，每次迭代不会修改已有的绑定，而是会创建一个新绑定。

## 1.4 全局块作用域绑定

let 和 const 相比 var，另外一个区别是它们在全局作用域中的行为。当 var 被用于全局作用域时，它会创建一个新的全局变量作为全局对象（浏览器环境中的 window 对象）的属性。这意味着用 var 很可能会无意中覆盖一个已经存在的全局变量。

如果在全局作用域中使用 let 或 const，会在全局作用域下创建一个新的绑定，但该绑定不会添加为全局对象的属性。换句话说，用 let 或 const 不能覆盖全局变量，而只能屏蔽它。

```javascript
// in a browser
let RegExp = "Hello!";
console.log(RegExp);                    // "Hello!"
console.log(window.RegExp === RegExp);  // false

const ncz = "Hi!";
console.log(ncz);                       // "Hi!"
console.log("ncz" in window);           // false
```



## 1.5 块级绑定最佳实践的进化

当更多的开发者迁移到 ECMAScript 6 后，一种做法日益普及：默认使用 const，只有确实需要改变变量的值时使用 let 。因为大部分变量的值在初始化后不应再改变，而预料外的变量值的改变是很多 bug 的源头。

# 第二章 字符串和正则表达式

# 第三章 函数

## 3.1 函数形参的默认值

## 3.2 处理无命名参数

## 3.3 增强的Function构造函数

## 3.4展开运算符

## 3.5 name属性

## 3.6 明确函数的多重用途

## 3.7块级函数

## 3.8 箭头函数

## 3.9 尾调用优化





