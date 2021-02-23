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

# DOM和BOM
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