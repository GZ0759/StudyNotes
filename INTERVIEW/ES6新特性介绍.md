# 变量声明 let 和 const

- 块级作用域
- 不存在变量提升
- 暂时性死区
- 不允许重复声明/常量的值不能修改

# 变量的解构复制

- 数组、对象、字符串和函数参数
- 数值和布尔值

# 字符串扩展和新增方法

- 模板字符串
- replaceAll 方法

# 函数扩展

- 箭头函数

  - this 是定义时所在的对象
  - 不可以当做构造函数
  - 不可以使用 arguments 对象
  - 不可以使用 yield 命令

- 函数参数默认值和 rest 参数

# 对象的扩展和新增方法

- 对象简洁表示法
- 链判断运算符 `?.`
- Null 判断运算符 `??`
- 对象合并 Object.assgin
- Object.values 和 Object.entires
- 对象原型相关方法

# Symbol 数据类型

Set 和 Map 数据结构

- Set 类似数组，成员的值是唯一的
- Map 本质上是键值对的集合（Hash 结构）

# Proxy 元编程

- Proxy 支持的拦截操作一览，一共 13 种
- get(target, propKey, receiver)：拦截对象属性的读取
- set(target, propKey, value, receiver)：拦截对象属性的设置

# Promise 对象

- 实例方法 then/catch/finally
- 静态方法 all/race/allSettled/any 和 resolve/reject

# 生成器和迭代器

- Generator
- Iterator 和 for...of 循环

# Async 异步函数

- Generator 函数的语法糖
- 正常情况下，await 命令后面是一个 Promise 对象，返回该对象的结果

# Class 类

- 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到
- constructor()方法是类的默认方法，通过 new 命令生成对象实例时，自动调用该方法。
- 引入了一个 `new.target` 属性，该属性一般用在构造函数之中，返回 new 命令作用于的那个构造函数

# Module 模块

- CommonJS 模块输出的是一个值的拷贝，ES6 模块输出的是值的引用。
- CommonJS 模块是运行时加载，ES6 模块是编译时输出接口。
- CommonJS 模块的 require()是同步加载模块，ES6 模块的 import 命令是异步加载，有一个独立的模块依赖的解析阶段。
