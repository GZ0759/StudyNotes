> Vue 3 入门指南与实战案例  
> [原文地址](https://github.com/chengpeiquan/learning-vue3)

# 快速上手 TypeScript

## 常用的 TS 类型定义

### 原始数据类型

[原始数据类型](https://developer.mozilla.org/zh-CN/docs/Glossary/Primitive) 是一种既非对象也无方法的数据。

除了 String ，另外还有数值 Number 、布尔值 Boolean 等等，它们在 TypeScript 都有统一的表达方式，我们列个表格对比，能够更直观的了解：

| 原始数据类型 | JavaScript | TypeScript |
| :----------: | :--------: | :--------: |
|    字符串    |   String   |   string   |
|     数值     |   Number   |   number   |
|    布尔值    |  Boolean   |  boolean   |
|    大整数    |   BigInt   |   bigint   |
|     符号     |   Symbol   |   symbol   |
|    不存在    |    Null    |    null    |
|    未定义    | Undefined  | undefined  |

### 数组

除了原始数据类型之外， JavaScript 还有引用类型，数组 Array 就是其中的一种。

| 数组里的数据 | 类型写法 1  |     类型写法 2     |
| :----------: | :---------: | :----------------: |
|    字符串    |  string[]   |  Array\<string\>   |
|     数值     |  number[]   |  Array\<number\>   |
|    布尔值    |  boolean[]  |  Array\<boolean\>  |
|    大整数    |  bigint[]   |  Array\<bigint\>   |
|     符号     |  symbol[]   |  Array\<symbol\>   |
|    不存在    |   null[]    |   Array\<null\>    |
|    未定义    | undefined[] | Array\<undefined\> |

### 对象（接口）

如果你熟悉 JavaScript ，那么就知道对象的 “键值对” 里面的值，可能是由原始数据、数组、对象组成的，所以在 TypeScript ，类型定义也是需要根据值的类型来确定它的类型，因此定义对象的类型应该是第一个比较有门槛的地方。

#### 如何定义对象的类型

对象的类型定义有两个语法支持： `type` 和 `interface` 。

先看看 `type` 的写法：

```ts
type UserItem = {
  // ...
}
```

再看看 `interface` 的写法：

```ts
interface UserItem {
  // ...
}
```

可以看到它们表面上的区别是一个有 `=` 号，一个没有，事实上在一般的情况下也确实如此，两者非常接近，但是在特殊的时候也有一定的区别。

#### 了解接口的使用

为了降低学习门槛，我们统一使用 `interface` 来做入门教学，它的写法与 Object 更为接近，事实上它也被用的更多。

对象的类型 `interface` 也叫做接口，用来描述对象的结构。

我们以这个用户信息为例子，比如你要描述 Petter 这个用户，他的最基础信息就是姓名和年龄，那么定义为接口就是这么写：

```ts
// 定义用户对象的类型
interface UserItem {
  name: string
  age: number
}

// 在声明变量的时候将其关联到类型上
const petter: UserItem = {
  name: 'Petter',
  age: 20,
}
```

如果你需要添加数组、对象等类型到属性里，按照这样继续追加即可。

#### 可选的接口属性

注意，上面这样定义的接口类型，表示 `name` 和 `age` 都是必选的属性，不可以缺少，一旦缺少，代码运行起来就会报错！

在实际的业务中，有可能会出现一些属性并不是必须的，就像这个年龄，你可以将其设置为可选属性，通过添加 `?` 来定义。

请注意下面代码的第三行， `age` 后面紧跟了一个 `?` 号再接 `:` 号，这是 TypeScript 对象对于可选属性的一个定义方式，这一次这段代码是可以成功运行的！

```ts{3-4}
interface UserItem {
  name: string
  // 这个属性变成了可选
  age?: number
}

const petter: UserItem = {
  name: 'Petter',
}
```

#### 调用自身接口的属性

如果一些属性的结构跟本身一致，也可以直接引用，比如下面例子里的 `friendList` 属性，用户的好友列表，它就可以继续使用 `UserItem` 这个接口作为数组的类型：

```ts{5-6,13-26}
interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  // 这个属性引用了本身的类型
  friendList: UserItem[]
}

const petter: UserItem = {
  name: 'Petter',
  age: 18,
  enjoyFoods: ['rice', 'noodle', 'pizza'],
  friendList: [
    {
      name: 'Marry',
      age: 16,
      enjoyFoods: ['pizza', 'ice cream'],
      friendList: [],
    },
    {
      name: 'Tom',
      age: 20,
      enjoyFoods: ['chicken', 'cake'],
      friendList: [],
    }
  ],
}
```

#### 接口的继承

接口还可以继承，比如你要对用户设置管理员，管理员信息也是一个对象，但要比普通用户多一个权限级别的属性，那么就可以使用继承，它通过 `extends` 来实现：

```ts{8-11,31}
interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  friendList: UserItem[]
}

// 这里继承了 UserItem 的所有属性类型，并追加了一个权限等级属性
interface Admin extends UserItem {
  permissionLevel: number
}

const admin: Admin = {
  name: 'Petter',
  age: 18,
  enjoyFoods: ['rice', 'noodle', 'pizza'],
  friendList: [
    {
      name: 'Marry',
      age: 16,
      enjoyFoods: ['pizza', 'ice cream'],
      friendList: [],
    },
    {
      name: 'Tom',
      age: 20,
      enjoyFoods: ['chicken', 'cake'],
      friendList: [],
    }
  ],
  permissionLevel: 1,
}
```

如果你觉得这个 `Admin` 类型不需要记录这么多属性，也可以在继承的过程中舍弃某些属性，通过 `Omit` 帮助类型来实现，`Omit` 的类型如下：

```ts
type Omit<T, K extends string | number | symbol>
```

其中 `T` 代表已有的一个对象类型， `K` 代表要删除的属性名，如果只有一个属性就直接是一个字符串，如果有多个属性，用 `|` 来分隔开，下面的例子就是删除了两个不需要的属性：

```ts{8-11}
interface UserItem {
  name: string
  age: number
  enjoyFoods: string[]
  friendList?: UserItem[]
}

// 这里在继承 UserItem 类型的时候，删除了两个多余的属性
interface Admin extends Omit<UserItem, 'enjoyFoods' | 'friendList'> {
  permissionLevel: number
}

// 现在的 admin 就非常精简了
const admin: Admin = {
  name: 'Petter',
  age: 18,
  permissionLevel: 1,
}
```

看到这里并实际体验过的话，在业务中常见的类型定义已经难不倒你了！

### 类

类是 JavaScript ES6 推出的一个概念，通过 `class` 关键字，你可以定义一个对象的模板，如果你对类还比较陌生的话，可以先阅读一下阮一峰老师的 ES6 文章：[Class 的基本语法](https://es6.ruanyifeng.com/#docs/class) 。

在 TypeScript ，通过类得到的变量，它的类型就是这个类，可能这句话看起来有点难以理解，我们来看个例子，你可以在 demo 里运行它：

```ts
// 定义一个类
class User {
  // constructor 上的数据需要先这样定好类型
  name: string

  // 入参也要定义类型
  constructor(userName: string) {
    this.name = userName
  }

  getName() {
    console.log(this.name)
  }
}

// 通过 new 这个类得到的变量，它的类型就是这个类
const petter: User = new User('Petter')
petter.getName() // Petter
```

类与类之间可以继承：

```ts
// 这是一个基础类
class UserBase {
  name: string
  constructor(userName: string) {
    this.name = userName
  }
}

// 这是另外一个类，继承自基础类
class User extends UserBase {
  getName() {
    console.log(this.name)
  }
}

// 这个变量拥有上面两个类的所有属性和方法
const petter: User = new User('Petter')
petter.getName()
```

类也可以提供给接口去继承：

```ts
// 这是一个类
class UserBase {
  name: string
  constructor(userName: string) {
    this.name = userName
  }
}

// 这是一个接口，可以继承自类
interface User extends UserBase {
  age: number
}

// 这样这个变量就必须同时存在两个属性
const petter: User = {
  name: 'Petter',
  age: 18,
}
```

如果类上面本身有方法存在，接口在继承的时候也要相应的实现，当然也可以借助在 [对象（接口）](#对象-接口) 提到的 `Omit` 帮助类型来去掉这些方法。

```ts{6-9,12-15}
class UserBase {
  name: string
  constructor(userName: string) {
    this.name = userName
  }
  // 这是一个方法
  getName() {
    console.log(this.name)
  }
}

// 接口继承类的时候也可以去掉类上面的方法
interface User extends Omit<UserBase, 'getName'> {
  age: number
}

// 最终只保留数据属性，不带有方法
const petter: User = {
  name: 'Petter',
  age: 18,
}
```

### 联合类型

当一个变量可能出现多种类型的值的时候，你可以使用联合类型来定义它，类型之间用 `|` 符号分隔。

举一个简单的例子，下面这个函数接收一个代表 “计数” 的入参，并拼接成一句话打印到控制台，因为最终打印出来的句子是字符串，所以参数没有必要非得是数值，传字符串也是可以的，所以我们就可以使用联合类型：

```ts{2}
// 你可以在 demo 里运行这段代码
function counter(count: number | string) {
  console.log(`The current count is: ${count}.`)
}

// 不论传数值还是字符串，都可以达到我们的目的
counter(1)  // The current count is: 1.
counter('2')  // The current count is: 2.
```

在实际的业务场景中，例如 Vue 的路由在不同的数据结构里也有不同的类型，有时候我们需要通过路由实例来判断是否符合要求的页面，也需要用到这种联合类型：

```ts{5}
// 注意：这不是完整的代码，只是一个使用场景示例
import type { RouteRecordRaw, RouteLocationNormalizedLoaded } from 'vue-router'

function isArticle(
  route: RouteRecordRaw | RouteLocationNormalizedLoaded
): boolean {
  // ...
}

```

再举个例子，我们是用 Vue 做页面，你会涉及到子组件或者 DOM 的操作，当它们还没有渲染出来时，你获取到的是 null ，渲染后你才能拿到组件或者 DOM 结构，这种场景我们也可以使用联合类型：

```ts
// querySelector 拿不到 DOM 的时候返回 null
const ele: HTMLElement | null = document.querySelector('.main')
```

### 函数

函数是 JavaScript 里最重要的成员之一，我们所有的功能实现都是基于函数。

#### 函数的基本的写法

在 JavaScript ，函数有很多种写法：

```js
// 注意：这是 JavaScript 代码

// 写法一：函数声明
function sum1(x, y) {
  return x + y
}

// 写法二：函数表达式
const sum2 = function (x, y) {
  return x + y
}

// 写法三：箭头函数
const sum3 = (x, y) => x + y

// 写法四：对象上的方法
const obj = {
  sum4(x, y) {
    return x + y
  },
}

// 还有很多……
```

但其实离不开两个最核心的操作：输入与输出，也就是对应函数的 “入参” 和 “返回值” ，在 TypeScript ，函数本身和 TS 类型有关系的也是在这两个地方。

函数的入参是把类型写在参数后面，返回值是写在圆括号后面，我们把上面在 JavaScript 的这几个写法，转换成 TypeScript 看看区别在哪里：

```ts{4,9,14,18}
// 注意：这是 TypeScript 代码

// 写法一：函数声明
function sum1(x: number, y: number): number {
  return x + y
}

// 写法二：函数表达式
const sum2 = function(x: number, y: number): number {
  return x + y
}

// 写法三：箭头函数
const sum3 = (x: number, y: number): number => x + y

// 写法四：对象上的方法
const obj = {
  sum4(x: number, y: number): number {
    return x + y
  }
}

// 还有很多……
```

是不是一下子 Get 到了技巧！函数的类型定义也是非常的简单，掌握这个技巧可以让你解决大部分常见的函数。

#### 函数的可选参数

实际业务中会遇到有一些函数入参是可选，可以用和 [对象（接口）](#对象-接口) 一样，用 `?` 来定义：

```ts
// 注意 isDouble 这个入参后面有个 ? 号，表示可选
function sum(x: number, y: number, isDouble?: boolean): number {
  return isDouble ? (x + y) * 2 : x + y
}

// 这样传参都不会报错，因为第三个参数是可选的
sum(1, 2) // 3
sum(1, 2, true) // 6
```

#### 无返回值的函数

除了有返回值的函数，我们更多时候是不带返回值的，例如下面这个例子，这种函数我们用 `void` 来定义它的返回，也就是空。

```ts{2}
// 注意这里的返回值类型
function sayHi(name: string): void {
  console.log(`Hi, ${name}!`)
}

sayHi('Petter') // Hi, Petter!
```

需要注意的是， `void` 和 `null` 、 `undefined` 不可以混用，如果你的函数返回值类型是 `null` ，那么你是真的需要 `return` 一个 `null` 值：

```ts{2,4}
// 只有返回 null 值才能定义返回类型为 null
function sayHi(name: string): null {
  console.log(`Hi, ${name}!`)
  return null
}
```

有时候你要判断参数是否合法，不符合要求时需要提前终止执行（比如在做一些表单校验的时候），这种情况下你也可以用 `void` ：

```ts{2-3}
function sayHi(name: string): void {
  // 这里判断参数不符合要求则提前终止运行，但它没有返回值
  if (!name) return

  // 否则正常运行
  console.log(`Hi, ${name}!`)
}
```

#### 异步函数的返回值

对于异步函数，你需要用 `Promise<T>` 类型来定义它的返回值，这里的 `T` 是泛型，取决于你的函数最终返回一个什么样的值（ `async / await` 也适用这个类型）。

例如这个例子，这是一个异步函数，会 `resolve` 一个字符串，所以它的返回类型是 `Promise<string>` （假如你没有 `resolve` 数据，那么就是 `Promise<void>` ）。

```ts{2,5}
// 注意这里的返回值类型
function queryData(): Promise<string> {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('Hello World')
    }, 3000)
  })
}

queryData().then((data) => console.log(data))
```

#### 函数本身的类型

细心的同学可能会有个疑问，通过函数表达式或者箭头函数声明的函数，这样写好像只对函数体的类型进行了定义，而左边的变量并没有指定。

没错，我们确实是没有为这个变量指定类型：

```ts
// 这里的 sum ，我们确实是没有指定类型
const sum = (x: number, y: number): number => x + y
```

这是因为，通常 TypeScript 会根据函数体帮我们自动推导，所以可以省略这里的定义。

如果确实有必要，你可以这样来定义等号左边的类型：

```ts
const sum: (x: number, y: number) => number = (x: number, y: number): number =>
  x + y
```

这里出现了 2 个箭头 `=>` ，注意第一个箭头是 TypeScript 的，第二个箭头是 JavaScript ES6 的。

实际上上面这句代码是分成了三部分：

1. `const sum: (x: number, y: number) => number` 是这个函数的名称和类型
2. `= (x: number, y: number)` 这里是指明了函数的入参和类型
3. `: number => x + y` 这里是函数的返回值和类型

第 2 和 3 点相信你从上面的例子已经能够理解了，所以我们注意力放在第一点：

TypeScript 的函数类型是以 `() => void` 这样的形式来写的：左侧圆括号是函数的入参类型，如果没有参数，就只有一个圆括号，如果有参数，就按照参数的类型写进去；右侧则是函数的返回值。

事实上由于 TypeScript 会帮你推导函数类型，所以我们很少会显式的去写出来，除非你在给对象定义方法：

```ts{3-4,9-11}
// 对象的接口
interface Obj {
  // 上面的方法就需要你显式的定义出来
  sum: (x: number, y: number) => number
}

// 声明一个对象
const obj: Obj = {
  sum(x: number, y: number): number {
    return x + y
  }
}
```

#### 函数的重载

在未来的实际开发中，你可能会接触到一个 API 有多个 TS 类型的情况，比如 Vue 的 [watch API](component.md#api-的-ts-类型) 。

Vue 的这个 watch API 在被调用时，需要接收一个数据源参数，当监听单个数据源时，它匹配了类型 1 ，当传入一个数组监听多个数据源时，它匹配了类型 2 。

这个知识点其实就是 TypeScript 里的函数重载。

我们先来看下不用重载的时候，我们的代码应该怎么写：

```ts
// 对单人或者多人打招呼
function greet(name: string | string[]): string | string[] {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

// 单个问候语
const greeting = greet('Petter')
console.log(greeting) // Welcome, Petter!

// 多个问候语
const greetings = greet(['Petter', 'Tom', 'Jimmy'])
console.log(greetings)
// [ 'Welcome, Petter!', 'Welcome, Tom!', 'Welcome, Jimmy!' ]
```

虽然代码逻辑部分还是比较清晰的，区分了入参的数组类型和字符串类型，返回不同的结果，但是，在入参和返回值的类型这里，却显得非常乱。

并且这样子写，下面在调用函数时，定义的变量也无法准确的获得它们的类型：

```ts
// 此时这个变量依然可能有多个类型
const greeting: string | string[]
```

如果你要强制确认类型，需要使用 TS 的 [类型断言](#类型断言) （留意后面的 `as` 关键字）：

```ts
const greeting = greet('Petter') as string
const greetings = greet(['Petter', 'Tom', 'Jimmy']) as string[]
```

这无形的增加了编码时的心智负担。

此时，利用 TypeScript 的函数重载就非常有用！我们来看一下具体如何实现：

```ts{2-4}
// 这一次用了函数重载
function greet(name: string): string  // TS 类型
function greet(name: string[]): string[]  // TS 类型
function greet(name: string | string[]) {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

// 单个问候语，此时只有一个类型 string
const greeting = greet('Petter')
console.log(greeting) // Welcome, Petter!

// 多个问候语，此时只有一个类型 string[]
const greetings = greet(['Petter', 'Tom', 'Jimmy'])
console.log(greetings)
// [ 'Welcome, Petter!', 'Welcome, Tom!', 'Welcome, Jimmy!' ]
```

上面是利用函数重载优化后的代码，可以看到我一共写了 3 行 `function greet …` ，区别如下：

第 1 行是函数的 TS 类型，告知 TypeScript ，当入参为 `string` 类型时，返回值也是 `string` ;

第 2 行也是函数的 TS 类型，告知 TypeScript ，当入参为 `string[]` 类型时，返回值也是 `string[]` ;

第 3 行开始才是真正的函数体，这里的函数入参需要把可能涉及到的类型都写出来，用以匹配前两行的类型，并且这种情况下，函数的返回值类型可以省略，因为在第 1 、 2 行里已经定义过返回类型了。

### 任意值

如果你实在不知道应该如何定义一个变量的类型， TypeScript 也允许你使用任意值。

还记得我们在 [为什么需要类型系统](#为什么需要类型系统) 的用的那个例子吗？我们再次放到 `src/ts/index.ts` 里：

```ts
// 这段代码在 TS 里运行会报错
function getFirstWord(msg) {
  console.log(msg.split(' ')[0])
}

getFirstWord('Hello World')

getFirstWord(123)
```

运行 `npm run dev:ts` 的时候，会得到一句报错 `Parameter 'msg' implicitly has an 'any' type.` ，意思是这个参数带有隐式 any 类型。

这里的 any 类型，就是 TypeScript 任意值。

既然报错是 “隐式” ，那我们 “显式” 的指定就可以了，当然，为了程序能够正常运行，我们还提高一下函数体内的代码健壮性：

```ts{2,4}
// 这里的入参显式指定了 any
function getFirstWord(msg: any) {
  // 这里使用了 String 来避免程序报错
  console.log(String(msg).split(' ')[0])
}

getFirstWord('Hello World')

getFirstWord(123)
```

这次就不会报错了，不论是传 `string` 还是 `number` 还是其他类型，都可以正常运行。

### npm 包

虽然现在从 npm 安装的包都基本自带 TS 类型了，不过也存在一些包没有默认支持 TypeScript ，比如我们前面提到的 [md5](https://www.npmjs.com/package/md5) 。

你在 TS 文件里导入并使用这个包的时候，会编译失败，比如在我们前面的 [Hello TypeScript](#hello-typescript) demo 里敲入以下代码：

```ts
// src/ts/index.ts
import md5 from 'md5'
console.log(md5('Hello World'))
```

在命令行执行 `npm run dev:ts` 之后，你会得到一段报错信息：

```bash
src/ts/index.ts:1:17 - error TS7016:
Could not find a declaration file for module 'md5'.
'D:/Project/demo/node-demo/node_modules/md5/md5.js' implicitly has an 'any' type.
  Try `npm i --save-dev @types/md5` if it exists
  or add a new declaration (.d.ts) file
  containing `declare module 'md5';`

1 import md5 from 'md5'
                  ~~~~~
```

这是因为缺少 md5 这个包的类型定义，我们根据命令行的提示，安装 `@types/md5` 这个包。

这是因为这些包是很早期用 JavaScript 编写的，因为功能够用作者也没有进行维护更新，所以缺少相应的 TS 类型，因此开源社区推出了一套 @types 类型包，专门处理这样的情况。

@types 类型包的命名格式为 `@types/<package-name>` ，也就是在原有的包名前面拼接 `@types` ，日常开发要用到的知名 npm 包都会有响应的类型包，只需要将其安装到 package.json 的 `devDependencies` 里即可解决该问题。

我们来安装一下 md5 的类型包：

```bash
npm install -D @types/md5
```

再次运行就不会报错了！

```bash
npm run dev:ts

> demo@1.0.0 dev:ts
> ts-node src/ts/index.ts

b10a8db164e0754105b7a99be72e3fe5
```

### 类型断言

在讲解 [函数的重载](#函数的重载) 的时候，我提到了一个用法：

```ts
const greeting = greet('Petter') as string
```

这里的 `值 as 类型` 就是 TypeScript 类型断言的语法，它还有另外一个语法是 `<类型>值` 。

当一个变量应用了 [联合类型](#联合类型) 时，在某些时候如果不显式的指明其中的一种类型，可能会导致后续的代码运行报错。

这个时候你就可以通过类型断言强制指定其中一种类型，以便程序顺利运行下去。

#### 常见的使用场景

我们把函数重载时最开始用到的那个例子，也就是下面的代码放到 `src/ts/index.ts` 里：

```ts{9-11}
// 对单人或者多人打招呼
function greet(name: string | string[]): string | string[] {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

// 虽然已知此时应该是 string[]
// 但 TypeScript 还是会认为这是 string | string[]
const greetings = greet(['Petter', 'Tom', 'Jimmy'])

// 会导致无法使用 join 方法
const greetingSentence = greetings.join(' ')
console.log(greetingSentence)
```

执行 `npm run dev:ts` ，可以清楚的看到报错原因，因为 `string` 类型不具备 `join` 方法。

```bash
src/ts/index.ts:11:31 - error TS2339:
Property 'join' does not exist on type 'string | string[]'.
  Property 'join' does not exist on type 'string'.

11 const greetingStr = greetings.join(' ')
                                 ~~~~
```

此时利用类型断言就可以达到目的：

```ts{9-10}
// 对单人或者多人打招呼
function greet(name: string | string[]): string | string[] {
  if (Array.isArray(name)) {
    return name.map((n) => `Welcome, ${n}!`)
  }
  return `Welcome, ${name}!`
}

// 已知此时应该是 string[] ，所以用类型断言将其指定为 string[]
const greetings = greet(['Petter', 'Tom', 'Jimmy']) as string[]

// 现在可以正常使用 join 方法
const greetingSentence = greetings.join(' ')
console.log(greetingSentence)
```

#### 需要注意的事情

但是，请不要滥用类型断言，只在你能够确保代码正确的情况下去使用它，我们来看一个反例：

```ts
// 原本要求 age 也是必须的属性之一
interface User {
  name: string
  age: number
}

// 但是类型断言过程中，你遗漏了
const petter = {} as User
petter.name = 'Petter'

// TypeScript 依然可以运行下去，但实际上你的数据是不完整的
console.log(petter) // { name: 'Petter' }
```

### 类型推论

还记得我在讲 [原始数据类型](#原始数据类型) 的时候，最后提到的：

> 不过在实际的编程过程中，原始数据类型的类型定义是可以省略的，因为 TypeScript 会根据你声明变量时赋值的类型，自动帮你推导变量类型

这其实是 TypeScript 的类型推论功能，当你在声明变量的时候可以确认它的值，那么 TypeScript 也可以在这个时候帮你推导它的类型，这种情况下你就可以省略一些代码量。

下面这个变量这样声明是 OK 的，因为 TypeScript 会帮你推导 `msg` 是 `string` 类型。

```ts
// 相当于 msg: string
let msg = 'Hello World'

// 所以要赋值为 number 类型时会报错
msg = 3 // Type 'number' is not assignable to type 'string'
```

下面这段代码也是可以正常运行的，因为 TypeScript 会根据 `return` 的结果推导 `getRandomNumber` 的返回值是 `number` 类型，从而推导变量 `num` 也是 `number` 类型。

```ts
// 相当于 getRandomNumber(): number
function getRandomNumber() {
  return Math.round(Math.random() * 10)
}

// 相当于 num: number
const num = getRandomNumber()
```

类型推论的前提是变量在声明时有明确的值，如果一开始没有赋值，那么会被默认为 `any` 类型。

```ts
// 此时相当于 foo: any
let foo

// 所以可以任意改变类型
foo = 1 // 1
foo = true // true
```

类型推论可以帮你节约很多书写工作量，在确保变量初始化有明确的值的时候，你可以省略其类型，但必要的时候，该写上的还是要写上。

# 单组件的编写

项目搭好了，第一个要了解的肯定是组件的变化。

## 两个基本函数

在开始编写组件之前，我们需要了解两个全新的前置知识点：`setup` 与 `defineComponent`。

### setup 函数

Vue 3.x 的 `composition api` 系列里，推出了一个全新的 `setup` 函数，它是一个组件选项，在创建组件之前执行，一旦 props 被解析，并作为组合式 API 的入口点。

基本语法：

```ts
import { defineComponent } from 'vue'

export default defineComponent({
  setup (props, context) {
    // 业务代码写这里...
    
    return {
      // 需要给template用的数据、函数放这里return出去...
    }
  }
})
```

`setup` 函数包含了两个入参：

参数|类型|含义|是否必传
:--|:--|:--|:--
props|object|由父组件传递下来的数据|否
context|object|组件的执行上下文|否

1. 参数 `props` ：它是响应式的（只要你不解构它，或者使用 toRef/toRefs 进行响应式解构），当传入新的 prop 时，它将被更新。

2. 参数 `context` ：只是一个普通的对象，它暴露三个组件的 property：

属性|类型|作用
:--|:--|:--
attrs|非响应式对象|props 未定义的属性都将变成 attrs
slots|非响应式对象|插槽
emit|方法|触发事件

因为 `context` 只是一个普通对象，所以你可以直接使用 ES6 解构。但是 `attrs` 和 `slots` 请保持 `attrs.xxx`、`slots.xxx` 来使用他们数据，不要解构这两个属性，因为他们虽然不是响应式对象，但会随组件本身的更新而更新。

### defineComponent 函数

这是 Vue 3.x 推出的一个全新 API ，`defineComponent` 可以用于 `TypeScript` 的类型推导，帮你简化掉很多编写过程中的类型定义。

比如，你原本需要这样才可以使用 `setup`：

```ts
import { Slots } from 'vue'

// 声明props和return的数据类型
interface Data {
  [key: string]: unknown
}

// 声明context的类型
interface SetupContext {
  attrs: Data
  slots: Slots
  emit: (event: string, ...args: unknown[]) => void
}

// 使用的时候入参要加上声明，return也要加上声明
export default {
  setup(props: Data, context: SetupContext): Data {
    // ...

    return {
      // ...
    }
  }
}
```

使用了 `defineComponent` 之后，你就可以省略这些类型定义：

```ts
import { defineComponent } from 'vue'

export default defineComponent({
  setup (props, context) {
    // ...
    
    return {
      // ...
    }
  }
})
```

而且不只适用于 `setup`，只要是 Vue 本身的 API ，`defineComponent` 都可以自动帮你推导。

在编写组件的过程中，你只需要维护自己定义的数据类型就可以了，专注于业务。

## 组件的生命周期

我们还需要先了解组件的生命周期，才能够灵活的把控好每一处代码的执行结果达到你的预期。

### 升级变化

从 2.x 升级到 3.x，在保留对 2.x 的生命周期支持的同时，3.x 也带来了一定的调整。

生命周期的变化，可以直观的从下表了解：

2.x 生命周期|3.x 生命周期|执行时间说明
:-:|:-:|:-:
beforeCreate|setup|组件创建前执行
created|setup|组件创建后执行
beforeMount|onBeforeMount|组件挂载到节点上之前执行
mounted|onMounted|组件挂载完成后执行
beforeUpdate|onBeforeUpdate|组件更新之前执行
updated|onUpdated|组件更新完成之后执行
beforeDestroy|onBeforeUnmount|组件卸载之前执行
destroyed|onUnmounted|组件卸载完成后执行
errorCaptured|onErrorCaptured|当捕获一个来自子孙组件的异常时激活钩子函数

其中，在3.x，`setup` 的执行时机比 2.x 的 `beforeCreate` 和 `created` 还早，可以完全代替原来的这 2 个钩子函数。

另外，被包含在 `<keep-alive>` 中的组件，会多出两个生命周期钩子函数：

2.x 生命周期|3.x 生命周期|执行时间说明
:-:|:-:|:-:
activated|onActivated|被激活时执行
deactivated|onDeactivated|切换组件后，原组件消失前执行

### 使用 3.x 的生命周期

在 3.x ，每个生命周期函数都要先导入才可以使用，并且所有生命周期函数统一放在 `setup` 里运行。

如果你需要在达到 2.x 的 `beforeCreate` 和 `created` 目的的话，直接把函数执行在 `setup` 里即可。

比如：

```ts
import { defineComponent, onBeforeMount, onMounted } from 'vue'

export default defineComponent({
  setup () {

    console.log(1);
    
    onBeforeMount( () => {
      console.log(2);
    });
    
    onMounted( () => {
      console.log(3);
    });

    console.log(4);

    return {}
  }
})
```

最终将按照生命周期的顺序输出：

```js
// 1
// 4
// 2
// 3
```

## 组件的基本写法

如果你是从 2.x 就开始写 TS 的话，应该知道在 2.x 的时候就已经有了 `extend` 和 `class component` 的基础写法；3.x 在保留 class 写法的同时，还推出了 `defineComponent` + `composition api`的新写法。

加上视图部分又有 `template` 和 `tsx` 的写法、以及 3.x 对不同版本的生命周期兼容，累计下来，在 Vue 里写 TS ，至少有 9 种不同的组合方式。

我们先来回顾一下这些写法组合分别是什么，了解一下 3.x 最好使用哪种写法：

### 回顾 2.x 组件写法

在 2.x ，为了更好的 TS 推导，用的最多的还是 `class component` 的写法。

适用版本|基本写法|视图写法
:-:|:-:|:-:
2.x|Vue.extend|template
2.x|class component|template
2.x|class component|tsx

### 了解 3.x 组件写法

目前 3.x 从官方对版本升级的态度来看， `defineComponent` 就是为了解决之前 2.x 对 TS 推导不完善等问题而推出的，尤大也是更希望大家习惯 `defineComponent` 的使用。

适用版本|基本写法|视图写法|生命周期版本|官方是否推荐
:-:|:-:|:-:|:-:|:-:
3.x|class component|template|2.x|×
3.x|defineComponent|template|2.x|×
3.x|defineComponent|template|3.x|√
3.x|class component|tsx|2.x|×
3.x|defineComponent|tsx|2.x|×
3.x|defineComponent|tsx|3.x|√

所以从接下来开始，都会以 `defineComponent` + `composition api` + `template` 的写法，并且按照 3.x 的生命周期来作为示范案例。

接下来，使用 `composition api` 来编写组件，先来实现一个最简单的 `Hello World!`。

在 3.x ，只要你的数据要在 `template` 中使用，就必须在 `setup` 里 return 出来。当然，只在函数中调用到，而不需要渲染到模板里的，则无需 return 。

```vue
<template>
  <p class="msg">{{ msg }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const msg = 'Hello World!';

    return {
      msg
    }
  }
})
</script>

<style lang="stylus" scoped>
.msg
  font-size 14px
</style>
```

`template` 和 2.x 可以说是完全一样（会有一些不同，比如 `router-link` 移除了 `tag` 属性等等，后面讲到了会说明）

`style` 则是根据你熟悉的预处理器或者原生 CSS 来写的，完全没有变化。

变化最大的就是 `script` 部分了。

## 响应式数据的变化 

响应式数据是 MVVM 数据驱动编程的特色，相信大部分人当初入坑 MVVM 框架，都是因为响应式数据编程比传统的操作 DOM 要来得方便，而选择 Vue ，则是方便中的方便。

相对于 2.x 在 `data` 里定义后即可通过 `this.xxx` 来调用响应式数据，3.x 的生命周期里取消了 Vue 实例的 `this`，你要用到的比如 `ref` 、`reactive` 等响应式 API ，都必须通过导入才能使用，然后在 `setup` 里定义。

```ts
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const msg = ref<string>('Hello World!');

    return {
      msg
    }
  }
})
```

## 响应式 API 之 ref

`ref` 是最常用的一个响应式 API，它可以用来定义所有类型的数据，包括 Node 节点。

没错，在 2.x 常用的 `this.$refs.xxx` 来取代 `document.querySelector('.xxx')` 获取 Node 节点的方式，也是用这个 API 来取代。

### 类型声明

在开始使用 API 之前，要先了解一下在 `TypeScript` 中，`ref` 需要如何进行类型声明。

1. 变量声明

平时我们在定义变量的时候，都是这样给他们进行类型声明的：

```ts
// 单类型
const msg: string = 'Hello World!';

// 多类型
const phoneNumber: number | string = 13800138000;
```

2. ref 声明

但是在使用 `ref` 时，不能这样子声明，会报错，正确的声明方式应该是使用 `<>` 来包裹类型定义，紧跟在 `ref` API 之后：

```ts
// 单类型
const msg = ref<string>('Hello World!');

// 多类型
const phoneNumber = ref<number | string>(13800138000);
```

### 变量的定义

了解了如何进行类型声明之后，对变量的定义就没什么问题了，前面说了它可以用来定义所有类型的数据，包括 Node 节点，但不同类型的值之间还是有少许差异和注意事项，具体可以参考如下。

1. 基本类型

```ts
// 字符串
const msg = ref<string>('Hello World!');

// 数值
const count = ref<number>(1);

// 布尔值
const isVip = ref<boolean>(false);
```

2. 引用类型

对于对象、数组等引用类型也适用，比如要定义一个对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo = ref<Member>({
  id: 1,
  name: 'Tom'
});
```

定义一个普通数组：

```ts
// 数字数组
const uids = ref<number[]>([ 1, 2, 3 ]);

// 字符串数组
const names = ref<string[]>([ 'Tom', 'Petter', 'Andy' ]);
```

定义一个对象数组：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员组
const memberList = ref<Member[]>([
  {
    id: 1,
    name: 'Tom'
  },
  {
    id: 2,
    name: 'Petter'
  }
]);
```

### DOM 元素与子组件

除了可以定义数据，`ref` 也有我们熟悉的用途，就是用来挂载节点，也可以挂在子组件上。

模板部分依然是熟悉的用法，直接把 ref 挂到你要引用的 DOM 元素或者子组件上。

但是 `script` 部分有三个最基本的注意事项：

1. 定义挂载节点后，也是必须通过 `xxx.value` 才能正确操作到挂载的 DOM 元素或组件
2. 请保证视图渲染完毕后再执行 DOM 或组件的相关操作
3. 该变量必须 `return` 出去才可以给到 `template` 使用

配合上面的 `template` ，来看看 `script` 部分的具体例子：

```ts
import { defineComponent, onMounted, ref } from 'vue'
import Child from '@cp/Child.vue'

export default defineComponent({
  components: {
    Child
  },
  setup () {
    // 定义挂载节点，声明的类型详见下方附表
    const msg = ref<HTMLElement | null>(null);
    const child = ref<typeof Child | null>(null);

    // 请保证视图渲染完毕后再执行节点操作 e.g. onMounted / nextTick
    onMounted( () => {
      // 比如获取DOM的文本
      console.log(msg.value.innerText);

      // 或者操作子组件里的数据
      child.value.isShowDialog = true;
    });

    // 必须return出去才可以给到template使用
    return {
      msg,
      child
    }
  }
})
```

关于 DOM 和子组件的 TS 类型声明，可参考以下规则：

节点类型|声明类型|参考文档
:--|:--|:--
DOM 元素|使用 HTML 元素接口|[HTML 元素接口](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model#html_%E5%85%83%E7%B4%A0%E6%8E%A5%E5%8F%A3)
子组件|使用 typeof 获取子组件的类型|[typeof 操作符](https://zhuanlan.zhihu.com/p/311150643)

另外，关于这一小节，有一个可能会引起 TS 编译报错的情况是，新版本的脚手架创建出来的项目会默认启用 `--strictNullChecks` 选项，会导致案例中的代码无法正常运行（报错 `TS2531: Object is possibly 'null'.` ）。

原因是：默认情况下 `null` 和 `undefined` 是所有类型的子类型，但开启了 `strictNullChecks` 选项之后，会使 `null` 和 `undefined` 只能赋值给 `void` 和它们各自，这虽然是个更为严谨的选项，但因此也会带来一些影响赶工期的额外操作。

**有以下几种解决方案可以参考：**

1. 在涉及到相关操作的时候，对节点变量增加一个判断：

```ts
if ( child.value ) {
  // 读取子组件的数据
  console.log(child.value.num);

  // 执行子组件的方法
  child.value.sayHi('use if in onMounted');
}
```

2. 通过 TS 的可选符 `?` 来将目标设置为可选，避免出现错误（这个方式不能直接修改子组件数据的值）

```ts
// 读取子组件的数据
console.log(child.value?.num);

// 执行子组件的方法
child.value?.sayHi('use ? in onMounted');
```

3. 在项目根目录下的 `tsconfig.json` 文件里，显式的关闭 `strictNullChecks` 选项，关闭后，由自己来决定是否需要对 `null` 进行判断：

```json
{
  "compilerOptions": {
    // ...
    "strictNullChecks": false
  },
  // ...
}
```

4. 使用 any 类型来代替，但是写 TS 还是尽量不要使用 any ，满屏的 AnyScript 不如写回 JS 。

### 变量的读取与赋值

被 `ref` 包裹的变量会全部变成对象，不管你定义的是什么类型的值，都会转化为一个 ref 对象，其中 ref 对象具有指向内部值的单个属性 `value`。

对于普通变量的值，读取的时候直接读变量名即可：

```ts
// 读取一个字符串
const msg: string = 'Hello World!';
console.log('msg的值', msg);

// 读取一个数组
const uids: number[] = [ 1, 2, 3 ];
console.log('第二个uid', uids[1]);
```

对 ref 对象的值的读取，切记！必须通过 value ！

```ts
// 读取一个字符串
const msg = ref<string>('Hello World!');
console.log('msg的值', msg.value);

// 读取一个数组
const uids = ref<number[]>([ 1, 2, 3 ]);
console.log('第二个uid', uids.value[1]);
```

普通变量都必须使用 `let` 才可以修改值，由于 ref 对象是个引用类型，所以可以在 `const` 定义的时候，直接通过 `.value` 来修改。

```ts
// 定义一个字符串变量
const msg = ref<string>('Hi!');

// 1s后修改它的值
setTimeout(() => {
  msg.value = 'Hello!'
}, 1000);
```

因此你在对接接口数据的时候，可以自由的使用 `forEach`、`map`、`filter` 等遍历函数来操作你的 ref 数组，或者直接重置它。

```ts
const data = ref<string[]>([]);

// 提取接口的数据
data.value = api.data.map( (item: any) => item.text );

// 重置数组
data.value = [];
```

问我为什么突然要说这个？因为涉及到下一部分的知识，关于 `reactive` 的。

## 响应式 API 之 reactive

`reactive` 是继 `ref` 之后最常用的一个响应式 API 了，相对于 `ref`，它的局限性在于只适合对象、数组。

### 类型声明与定义

`reactive` 的声明方式，以及定义方式，没有 `ref` 的变化那么大，就是和普通变量一样。

reactive 对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo: Member = reactive({
  id: 1,
  name: 'Tom'
});
```

reactive 数组：

```ts
// 普通数组
const uids: number[] = [ 1, 2, 3];

// 对象数组
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象数组
const userList: Member[] = reactive([
  {
    id: 1,
    name: 'Tom'
  },
  {
    id: 2,
    name: 'Petter'
  },
  {
    id: 3,
    name: 'Andy'
  }
]);
```

### 变量的读取与赋值

reactive 对象在读取字段的值，或者修改值的时候，与普通对象是一样的。

reactive 对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo: Member = reactive({
  id: 1,
  name: 'Tom'
});

// 读取用户名
console.log(userInfo.name);

// 修改用户名
userInfo.name = 'Petter';
```

但是对于 reactive 数组，和普通数组会有一些区别。

先看看普通数组，重置，或者改变值，都是可以直接轻松的进行操作：

```ts
// 定义一个普通数组
let uids: number[] = [ 1, 2, 3 ];

// 从另外一个对象数组里提取数据过来
uids = api.data.map( item => item.id );

// 合并另外一个数组
let newUids: number[] = [ 4, 5, 6 ];
uids = [...uids, ...newUids];

// 重置数组
uids = [];
```

在 2.x 的时候，你在操作数组时，完全可以和普通数组那样随意的处理数据的变化，依然能够保持响应性。

但在 3.x ，如果你使用 `reactive` 定义数组，则不能这么搞了，必须只使用那些不会改变引用地址的操作。

举个例子，比如你要从接口读取翻页数据的时候，通常要先重置数组，再异步添加数据：

如果你使用常规的重置，会导致这个变量失去响应性：

```ts
/** 
 * 不推荐使用这种方式
 * 异步添加数据后，模板不会响应更新
 */
let uids: number[] = reactive([ 1, 2, 3 ]);

// 丢失响应性的步骤
uids = [];

// 异步获取数据后，模板依然是空数组
setTimeout( () => {
  uids.push(1);
}, 1000);
```

要让模板那边依然能够保持响应性，则必须在关键操作时，不破坏响应性 API 的存在。

```ts
let uids: number[] = reactive([ 1, 2, 3 ]);

// 不会破坏响应性
uids.length = 0;

// 异步获取数据后，模板可以正确的展示
setTimeout( () => {
  uids.push(1);
}, 1000);
```

### 特别注意

不要对通过 `reactive` 定义的对象进行解构，解构后得到的变量会失去响应性。

比如这些情况，在 2s 后都得不到新的 name 信息：

```ts
import { defineComponent, reactive } from 'vue'

interface Member {
  id: number,
  name: string
};

export default defineComponent({
  setup () {

    // 定义一个带有响应性的成员对象
    const userInfo: Member = reactive({
      id: 1,
      name: 'Petter'
    });

    // 2s后更新userInfo
    setTimeout( () => {
      userInfo.name = 'Tom';
    }, 2000);

    // 这个变量在2s后不会同步更新
    const newUserInfo: Member = {...userInfo};

    // 这个变量在2s后不会再同步更新
    const { name } = userInfo;

    // 这样return出去给模板用，在2s后也不会同步更新
    return {
      ...userInfo
    }
  }
})
```

## 响应式 API 之 toRef/toRefs

为了方便开发者，Vue 3.x 还推出了 2 个相关的 API ，用于 `reactive` 向 `ref` 转换。

两个 API 的拼写非常接近，顾名思义，一个是只转换一个字段，一个是转换所有字段。

API|作用
:--|:--
toRef|创建一个新的ref变量，转换 reactive 对象的某个字段为ref变量
toRefs|创建一个新的对象，它的每个字段都是 reactive 对象各个字段的ref变量

我们先定义好一个 `reactive` 变量：

```ts
interface Member {
  id: number,
  name: string
};

const userInfo: Member = reactive({
  id: 1,
  name: 'Petter'
});
```

1. toRef

`toRef` 接收 2 个参数，第一个是 `reactive` 对象, 第二个是要转换的 `key` 。在这里我们只想转换 `userInfo` 里的 `name` ，只需要这样操作：

```ts
const name: string = toRef(userInfo, 'name');
```

这样就成功创建了一个 `ref` 变量。之后读取和赋值就使用 `name.value`，它会同时更新 `name` 和 `userInfo.name`。 

在 `toRef` 的过程中，如果使用了原对象上面不存在的 `key` ，那么定义出来的变量的 `value` 将会是 `undefined` 。如果你对这个不存在的 `key` 的 `ref` 变量，进行了 `value` 赋值，那么原来的对象也会同步增加这个 `key`，其值也会同步更新。

2. toRefs

`toRefs` 接收 1 个参数，是一个 `reactive` 对象。

```ts
const userInfoRefs: Member = toRefs(userInfo);
```

这个新的 `userInfoRefs` ，本身是个普通对象，但是它的每个字段，都是与原来关联的 `ref` 变量。

### 为什么要进行转换

`ref` 和 `reactive` 这两者的好处就不重复了，但是在使用的过程中，各自都有各自不方便的地方：

1. `ref` 虽然在 `template` 里使用起来方便，但比较烦的一点是在 `script` 里进行读取/赋值的时候，要一直记得加上 `.value` 属性
2. `reactive` 虽然在使用的时候，因为你知道它本身是一个 `Object` 类型，所以你不会忘记 `foo.bar` 这样的格式去操作，但是在 `template` 渲染的时候，你又因此不得不每次都使用 `foo.bar` 的格式去渲染

### 使用场景

从便利性和可维护性来说，最好只在功能单一、代码量少的组件里使用，比如一个表单组件，通常表单的数据都放在一个对象里。

当然你也可以更猛一点就是把所有的数据都定义到一个 `data` 里，然后你再去 `data` 里面取…但是没有必要为了转换而转换。

### 在业务中的具体运用

这一部分我一直用 `userInfo` 来当案例，那就继续以一个用户信息表的小 demo 来做这个的演示吧。

**在 script 部分：**

1. 先用 `reactive` 定义一个源数据，所有的数据更新，都是修改这个对象对应的值，按照对象的写法去维护你的数据
2. 再通过 `toRefs` 定义一个给 `template` 用的对象，它本身不具备响应性，但是它的字段全部是 `ref` 变量
3. 在 `return` 的时候，对 `toRefs` 对象进行解构，这样导出去就是各个字段对应的 `ref` 变量，而不是一整个对象

```ts
import { defineComponent, reactive, toRefs } from 'vue'

interface Member {
  id: number,
  name: string,
  age: number,
  gender: string
};

export default defineComponent({
  setup () {
    // 定义一个reactive对象
    const userInfo = reactive({
      id: 1,
      name: 'Petter',
      age: 18,
      gender: 'male'
    })

    // 定义一个新的对象，它本身不具备响应性，但是它的字段全部是ref变量
    const userInfoRefs = toRefs(userInfo);

    // 2s后更新userInfo
    setTimeout( () => {
      userInfo.id = 2;
      userInfo.name = 'Tom';
      userInfo.age = 20;
    }, 2000);

    // 在这里结构toRefs对象才能继续保持响应式
    return {
      ...userInfoRefs
    }
  }
})
```

**在 template 部分：**

由于 `return` 出来的都是 `ref` 变量，所以你在模板里直接使用 `userInfo` 各个字段的 `key` 即可。

```vue
<template>
  <ul class="user-info">

    <li class="item">
      <span class="key">ID:</span>
      <span class="value">{{ id }}</span>
    </li>

    <li class="item">
      <span class="key">name:</span>
      <span class="value">{{ name }}</span>
    </li>

    <li class="item">
      <span class="key">age:</span>
      <span class="value">{{ age }}</span>
    </li>

    <li class="item">
      <span class="key">gender:</span>
      <span class="value">{{ gender }}</span>
    </li>

  </ul>
</template>
```

## 函数的定义和使用

在 2.x，函数都是放在 `methods` 对象里定义，然后再在 `mounted` 等生命周期或者模板里通过 `click` 使用。

但在 3.x 的生命周期里，和数据的定义一样，都是通过 `setup` 来完成。

1. 你可以在 `setup` 里定义任意类型的函数（普通函数、class 类、箭头函数、匿名函数等等）
2. 需要自动执行的函数，执行时机需要遵循生命周期
3. 需要暴露给模板去通过 `click`、`change` 等行为来触发的函数，需要把函数名在 `setup` 里进行 `return` 才可以在模板里使用

简单写一下例子：

```vue
<template>
  <p>{{ msg }}</p>

  <!-- 在这里点击执行return出来的方法 -->
  <button @click="changeMsg">修改MSG</button>
  <!-- 在这里点击执行return出来的方法 -->
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue'

export default defineComponent({
  setup () {
    const msg = ref<string>('Hello World!');

    // 这个要暴露给模板使用，必须return才可以使用
    function changeMsg () {
      msg.value = 'Hi World!';
    }

    // 这个要在页面载入时执行，无需return出去
    const init = () => {
      console.log('init');
    }

    // 在这里执行init
    onMounted( () => {
      init();
    });

    return {
      // 数据
      msg,

      // 方法
      changeMsg
    }
  }
})
</script>
```

## 数据的监听

监听数据变化也是组件里的一项重要工作，比如监听路由变化、监听参数变化等等。

Vue 3.x 在保留原来的 `watch` 功能之外，还新增了一个 `watchEffect` 帮助我们更简单的进行监听。

### watch

但是新版的 `watch` 和旧版对比，在使用方式上变化非常大！旧版是这样用的，和 `data` 、 `methods` 都在同级配置：

```ts
// 旧版的写法：
export default {
  watch: {
    // ...
  },
  data () {
    return {
      // ...
    }
  },
  methods: {
    // ...
  }
}
```

新版的 `watch` 需要在 `setup` 里使用，在使用之前，还需要先导入该组件。

```ts
import { defineComponent, ref, watch } from 'vue'

export default defineComponent({
  setup () {
    const name = ref<string>('Petter');

    // 2s后改变数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 你可以监听一个响应式对象
    watch( name, () => {
      console.log('监听整个 ref ', name.value);
    })

    // 也可以监听对象里面的某个值（此时需要写成 getter 函数）
    watch( () => name.value, () => {
      console.log('只监听 value ', name.value);
    })
  }
})
```

需要注意的是，你只能监听响应式数据，如果通过 `let` 定义一个普通的字符串变量，然后去改变字符串内容，这样是无法监听的。

另外，默认情况下，`watch` 是惰性的，即只有当被侦听的源发生变化时才执行回调。

> 新的 `watch` 默认是深度监听，无需再手动指定 `deep` 。

另外， `watch` 可以接受两个参数：

参数|类型|作用
:--|:--|:--
newVal|any|变化后的新值
oldVal|any|变化前的旧值

这里返回的参数类型并没有特定限制，取决于你监听的数据类型变化。

```ts
export default defineComponent({
  setup () {
    const name = ref<string>('Petter');

    // 2s后改变数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 你可以监听一个响应式对象
    watch( name, (newVal, oldVal) => {
      console.log('打印变化前后的值', { oldVal, newVal });
    })

    return {
      name
    }
  }
})
```

注意：第一个参数是新值，第二个才是原来的旧值！

### watchEffect

如果一个函数里包含了多个需要监听的数据，一个一个数据去监听太麻烦了，在 3.x ，你可以直接使用 `watchEffect` 来简化你的操作。

它立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。

```ts
import { defineComponent, ref, watchEffect } from 'vue'

export default defineComponent({
  setup () {
    // 单独定义两个数据，后面用来分开改变数值
    const name = ref<string>('Petter');
    const age = ref<number>(18);

    // 定义一个调用这两个数据的函数
    const getUserInfo = (): void => {
      console.log({
        name: name.value,
        age: age.value
      });
    }

    // 2s后改变第一个数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 4s后改变第二个数据
    setTimeout(() => {
      age.value = 20;
    }, 4000);

    // 直接监听调用函数，在每个数据产生变化的时候，它都会自动执行
    watchEffect(getUserInfo);
  }
})
```

虽然理论上 `watchEffect` 是 `watch` 的一个简化操作，但他们也有一定的区别：

1. `watch` 可以访问侦听状态变化前后的值，而 `watchEffect` 没有。
2. `watch` 是在属性改变的时候才执行，而 `watchEffect` 则默认会执行一次，然后在属性改变的时候也会执行。

## 数据的计算

和 Vue 2.0 一样，数据的计算也是使用 `computed` API ，它可以通过现有的响应式数据，去通过计算得到新的响应式变量。

这里的响应式数据，可以简单理解为通过 ref API 、 reactive API 定义出来的数据，当然 Vuex 、Vue Router 等 Vue 数据也都具备响应式。

在 Vue 2.0 ，`computed` 和 `data` 在同级配置，并且不可以和 `data` 里的数据同名重复定义：

```ts
// 在 Vue 2 的写法：
export default {
  data() {
    return {
      firstName: 'Bill',
      lastName: 'Gates',
    }
  },
  // 注意这里定义的变量，都要通过函数的形式来返回它的值
  computed: {
    // 普通函数可以直接通过熟悉的 this 来拿到 data 里的数据
    fullName() {
      return `${this.firstName} ${this.lastName}`
    },
    // 箭头函数则需要通过参数来拿到实例上的数据
    fullName2: (vm) => `${vm.firstName} ${vm.lastName}`,
  }
}
```

这样你在需要用到全名的地方，只需要通过 `this.fullName` 就可以得到 `Bill Gates` 。

在 Vue 3.0 ，跟其他 API 的用法一样，需要先导入 `computed` 才能使用：

```ts
// 在 Vue 3 的写法：
import { defineComponent, ref, computed } from 'vue'

export default defineComponent({
  setup() {
    // 定义基本的数据
    const firstName = ref<string>('Bill')
    const lastName = ref<string>('Gates')

    // 定义需要计算拼接结果的数据
    const fullName = computed(() => `${firstName.value} ${lastName.value}`)

    // 2s 后改变某个数据的值
    setTimeout(() => {
      firstName.value = 'Petter'
    }, 2000)

    // template 那边在 2s 后也会显示为 Petter Gates
    return {
      fullName,
    }
  },
})
```

你可以把这个用法简单的理解为，传入一个回调函数，并 `return` 一个值，对，它需要有明确的返回值。

需要注意的是：

1. 定义出来的 `computed` 变量，和 `ref` 变量的用法一样，也是需要通过 `.value` 才能拿到它的值
2. 但是区别在于， `computed` 的 `value` 是只读的

### 类型定义

我们之前说过，在 defineComponent 里，会自动帮我们推导 Vue API 的类型，所以一般情况下，你是不需要显式的去定义 `computed` 出来的变量类型的。

在确实需要手动指定的情况下，你也可以导入它的类型然后定义：

```ts
import { computed } from 'vue'
import type { ComputedRef } from 'vue'

// 注意这里添加了类型定义
const fullName: ComputedRef<string> = computed(
  () => `${firstName.value} ${lastName.value}`
)
```

你要返回一个字符串，你就写 `ComputedRef<string>` ；返回布尔值，就写 `ComputedRef<boolean>` ；返回一些复杂对象信息，你可以先定义好你的类型，再诸如 `ComputedRef<UserInfo>` 去写。

```ts
// 这是 ComputedRef 的类型定义：
export declare interface ComputedRef<T = any> extends WritableComputedRef<T> {
  readonly value: T;
  [ComoutedRefSymbol]: true;
}
```

### 优势对比和注意事项

在继续往下看之前，我们先来了解一下这个 API 的一些优势和注意事项。

#### 优势对比

看到这里，相信刚接触的同学可能会有疑问，既然 `computed` 也是通过一个函数来返回值，那么和普通的 `function` 有什么区别，或者说优势？

1. 性能优势

数据的计算是基于它们的响应依赖关系缓存的，只在相关响应式依赖发生改变时它们才会重新求值。

也就是说，只要原始数据没有发生改变，多次访问 `computed` ，都是会立即返回之前的计算结果，而不是再次执行函数；而普通的 `function` 调用多少次就执行多少次，每调用一次就计算一次。

至于为何要如此设计，官网文档也给出了原因：

> 我们为什么需要缓存？假设我们有一个性能开销比较大的计算数据 list，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算数据依赖于 list。如果没有缓存，我们将不可避免的多次执行 list 的 getter！如果你不希望有缓存，请用 function 来替代。

2. 书写统一

我们假定 foo1 是 `ref` 变量， foo2 是 `computed` 变量， foo3 是普通函数返回值。

看到这里的同学应该都已经清楚 Vue 3 的 `ref` 变量是通过 `foo1.value` 来拿到值的，而 `computed` 也是通过 `foo2.value` ，并且在 template 里都可以省略 `.value` ，在读取方面，他们是有一致的风格和简洁性。

而 foo3 不管是在 script 还是 template ，都需要通过 `foo3()` 才能拿到结果，相对来说会有那么一丢丢别扭。

当然，关于这一点，如果涉及到的数据不是响应式数据，那么还是老老实实的用函数返回值吧 。

#### 注意事项

有优势当然也就有一定的 “劣势” ，当然这也是 Vue 框架的有意为之，所以在使用上也需要注意一些问题：

1. 只会更新响应式数据的计算

假设你要获取当前的时间信息，因为不是响应式数据，所以这种情况下你就需要用普通的函数去获取返回值，才能拿到最新的时间。

```ts
const nowTime = computed(() => new Date())
console.log(nowTime.value)
// 输出 Sun Nov 14 2021 21:07:00 GMT+0800 (GMT+08:00)

// 2s 后依然是跟上面一样的结果
setTimeout(() => {
  console.log(nowTime.value)
  // 还是输出 Sun Nov 14 2021 21:07:00 GMT+0800 (GMT+08:00)
}, 2000)
```

2. 数据是只读的

通过 computed 定义的数据，它是只读的。

如果你直接赋值，不仅无法变更数据，而且会收获一个报错。

```bash
TS2540: Cannot assign to 'value' because it is a read-only property.
```

虽然无法直接赋值，但是在必要的情况下，你依然可以通过 `computed` 的 `setter` 来更新数据。

### setter 的使用

通过 computed 定义的变量默认都是只读的形式（只有一个 getter ），但是在必要的情况下，你也可以使用其 setter 属性来更新数据。

#### 基本格式

当你需要用到 setter 的时候， `computed` 就不再是一个传入 callback 的形式了，而是传入一个带有 2 个方法的对象。

```ts
// 注意这里computed接收的入参已经不再是函数
const foo = computed({
  // 这里需要明确的返回一个值
  get() {
    // ...
  },
  // 这里接收一个参数，代表修改 foo 时，赋值下来的新值
  set(newValue) {
    // ...
  },
})
```

这里的 `get` 就是 `computed` 的 getter ，跟原来传入 callback 的形式一样，是用于 `foo.value` 的读取，所以这里你必须有明确的返回值。

这里的 `set` 就是 `computed` 的 setter ，它会接收一个参数，代表新的值，当你通过 `foo.value = xxx` 赋值的时候，赋入的这个值，就会通过这个入参来传递进来，你可以根据你的业务需要，把这个值，赋给相关的数据源。

在了解了基本格式后，可以查看下面的例子来了解具体的用法。

#### 使用示范

使用 Composition API 的写法来演示：

```ts
// 还是这2个数据源
const firstName = ref<string>('Bill')
const lastName = ref<string>('Gates')

// 这里我们配合setter的需要，改成了另外一种写法
const fullName = computed({
  // getter我们还是返回一个拼接起来的全名
  get() {
    return `${firstName.value} ${lastName.value}`
  },
  // setter这里我们改成只更新firstName，注意参数也定义TS类型
  set(newFirstName: string) {
    firstName.value = newFirstName
  },
})
console.log(fullName.value) // 输出 Bill Gates

// 2s后更新一下数据
setTimeout(() => {
  // 对fullName的赋值，其实更新的是firstName
  fullName.value = 'Petter'

  // 此时firstName已经得到了更新
  console.log(firstName.value) // 会输出 Petter

  // 当然，由于firstName变化了，所以fullName的getter也会得到更新
  console.log(fullName.value) // 会输出 Petter Gates
}, 2000)
```

### 应用场景

1. 数据的拼接和计算

如上面的案例，与其每个用到的地方都要用到 `firstName + ' ' + lastName` 这样的多变量拼接，不如用一个 `fullName` 来的简单。

当然，不止是字符串拼接，数据的求和等操作更是合适，比如说你做一个购物车，购物车里有商品列表，同时还要显示购物车内的商品总金额，这种情况就非常适合用计算数据。

2. 复用组件的动态数据

在一个项目里，很多时候组件会涉及到复用，比如说：“首页的文章列表 vs 列表页的文章列表 vs 作者详情页的文章列表” ，特别常见于新闻网站等内容资讯站点，这种情况下，往往并不需要每次都重新写 UI 、数据渲染等代码，仅仅是接口 URL 的区别。

这种情况你就可以通过路由名称来动态获取你要调用哪个列表接口：

```ts
const route = useRoute()

// 定义一个根据路由名称来获取接口URL的计算数据
const apiUrl = computed(() => {
  switch (route.name) {
    // 首页
    case 'home':
      return '/api/list1'
    // 列表页
    case 'list':
      return '/api/list2'
    // 作者页
    case 'author':
      return '/api/list3'
    // 默认是随机列表
    default:
      return '/api/random'
  }
})

// 请求列表
const getArticleList = async (): Promise<void> => {
  // ...
  articleList.value = await axios({
    method: 'get',
    url: apiUrl.value,
    // ...
  })
  // ...
}
```

3. 获取多级对象的值

你应该很经常的遇到要在 template 显示一些多级对象的字段，但是有时候又可能存在某些字段不一定有，需要做一些判断的情况，虽然有 `v-if` ，但是嵌套层级一多，你的模板会难以维护。

如果你把这些工作量转移给计算数据，结合 `try / catch` ，这样就无需在 template 里处理很多判断了。

```ts
// 例子比较极端，但在 Vuex 这种大型数据树上，也不是完全不可能存在
const foo = computed(() => {
  // 正常情况下返回需要的数据
  try {
    return store.state.foo3.foo2.foo1.foo
  }
  // 处理失败则返回一个默认值
  catch (e) {
    return ''
  }
})
```

4. 不同类型的数据转换

有时候你会遇到一些需求类似于，让用户在输入框里，按一定的格式填写文本，比如用英文逗号 `,` 隔开每个词，然后保存的时候，是用数组的格式提交给接口。

这个时候 `computed` 的 setter 就可以妙用了，只需要一个简单的 `computed` ，就可以代替 `input` 的 `change` 事件或者 `watch` 监听，可以减少很多业务代码的编写。

```vue
<template>
  <input
    type="text"
    v-model="tagsStr"
    placeholder="请输入标签，多个标签用英文逗号隔开"
  />
</template>

<script lang="ts">
import { defineComponent, computed, ref } from 'vue'

export default defineComponent({
  setup() {
    // 这个是最终要用到的数组
    const tags = ref<string[]>([])

    // 因为input必须绑定一个字符串
    const tagsStr = computed({
      // 所以通过getter来转成字符串
      get() {
        return tags.value.join(',')
      },
      // 然后在用户输入的时候，切割字符串转换回数组
      set(newValue: string) {
        tags.value = newValue.split(',')
      },
    })

    return {
      tagsStr,
    }
  },
})
</script>
```

## CSS 样式与预处理器

Vue 组件的 CSS 样式部分，3.x 保留着和 2.x 完全一样的写法。 

### 编写组件样式表

最基础的写法，就是在 Vue 文件里创建一个 `style` 标签，即可在里面写 CSS 代码了。

```vue
<style>
.msg {
  width: 100%;
}
.msg p {
  color: #333;
  font-size: 14px;
}
</style>
```

### 动态绑定 CSS

动态绑定 CSS ，在 Vue 2.x 就已经存在了，在此之前常用的是 `:class` 和 `:style` ，现在在 Vue 3.x ，还可以通过 `v-bind` 来动态修改了。

我们先来看看基本的用法：

```vue
<template>
  <p class="msg">Hello World!</p>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const fontColor = ref<string>('#ff0000')

    return {
      fontColor,
    }
  }
})
</script>

<style scoped>
.msg {
  color: v-bind(fontColor);
}
</style>
```

如上面的代码，你将渲染出一句红色文本的 `Hello World!`

这其实是利用了现代浏览器支持的 CSS 变量来实现的一个功能。

它渲染到 DOM 上，其实也是通过绑定 `style` 来实现，我们可以看到渲染出来的样式是：

```html
<p
  class="msg"
  data-v-7eb2bc79=""
  style="--7eb2bc79-fontColor:#ff0000;"
>
  Hello World!
</p>
```

对应的 CSS 变成了：

```css
.msg[data-v-7eb2bc79] {
  color: var(--7eb2bc79-fontColor);
}
```

理论上 `v-bind` 函数可以在 Vue 内部支持任意的 JS 表达式，但由于可能包含在 CSS 标识符中无效的字符，因此官方是建议在大多数情况下，用引号括起来，如：

```css
.text {
  font-size: v-bind('theme.font.size');
}
```

由于 CSS 变量的特性，因此对 CSS 响应式属性的更改不会触发模板的重新渲染（这也是和 `:class` 与 `:style` 的最大不同）。

不管你有没有开启 [\<style scoped\>](#style-scoped) ，使用 `v-bind` 渲染出来的 CSS 变量，都会带上 `scoped` 的随机 hash 前缀，避免样式污染（永远不会意外泄漏到子组件中），所以请放心使用！

### 样式表的组件作用域

CSS 不像 JS ，是没有作用域的概念的，一旦写了某个样式，直接就是全局污染。所以 [BEM 命名法](https://www.bemcss.com/) 等规范才应运而生。

但在 Vue 组件里，有两种方案可以避免出现这种污染问题。

一个是 Vue 2.x 就有的 `<style scoped>` ，一个是 Vue 3.x 新推出的 `<style module>` 。

1. style scoped

Vue 组件在设计的时候，就想到了一个很优秀的解决方案，通过 `scoped` 来支持创建一个 CSS 作用域，使这部分代码只运行在这个组件渲染出来的虚拟 DOM 上。

使用方式很简单，只需要在 `style` 后面带上 `scoped` 属性。

```vue
<style scoped>
.msg {
  width: 100%;
}
.msg p {
  color: #333;
  font-size: 14px;
}
</style>
```

编译后，虚拟 DOM 都会带有一个 `data-v-xxxxx` 这样的属性，其中 `xxxxx` 是一个随机生成的 hash ，同一个组件的 hash 是相同并且唯一的：

```html
<div class="msg" data-v-7eb2bc79>
  <p data-v-7eb2bc79>Hello World!</p>
</div>
```

而 CSS 则也会带上与 HTML 相同的属性，从而达到样式作用域的目的。

```css
.msg[data-v-7eb2bc79] {
  width: 100%;
}
.msg p[data-v-7eb2bc79] {
  color: #333;
  font-size: 14px;
}
```

使用 `scoped` 可以有效的避免全局样式污染，你可以在不同的组件里面都使用相同的 className，而不必担心会相互覆盖，不必再定义很长很长的样式名来防止冲突了。

2. style module

这是在 Vue 3.x 才推出的一个新方案，和 `<style scoped>` 不同，scoped 是通过给 DOM 元素添加自定义属性的方式来避免冲突，而 `<style module>` 则更为激进，将会编译成 [CSS Modules](https://github.com/css-modules/css-modules) 。

对于 CSS Modules 的处理方式，我们也可以通过一个小例子来更直观的了解它：

```css
/* 编译前 */
.title {
  color: red;
}

/* 编译后 */
._3zyde4l1yATCOkgn-DBWEL {
  color: red;
}
```

可以看出，是通过比较 “暴力” 的方式，把我们编写的 “好看的” 样式名，直接改写成一个随机 hash 样式名，来避免样式互相污染。 

所以我们回到 Vue 这边，看看 `<style module>` 是怎么操作的。

```vue
<template>
  <p :class="$style.msg">Hello World!</p>
</template>

<style module>
.msg {
  color: #ff0000;
}
</style>
```

于是，你将渲染出一句红色文本的 `Hello World!` 。

- 如果单纯只使用 `<style module>` ，那么在绑定样式的时候，是默认使用 `$style` 对象来操作的
- 必须显示的指定绑定到某个样式，比如 `$style.msg` ，才能生效
- 如果单纯的绑定 `$style` ，并不能得到 “把全部样式名直接绑定” 的期望结果
- 如果你指定的 className 是短横杆命名，比如 `.user-name` ，那么需要通过 `$style['user-name']` 去绑定

你也可以给 `module` 进行命名，然后就可以通过你命名的 “变量名” 来操作：

```vue
<template>
  <p :class="classes.msg">Hello World!</p>
</template>

<style module="classes">
.msg {
  color: #ff0000;
}
</style>
```

需要注意的一点是，一旦开启 `<style module>` ，那么在 `<style module>` 里所编写的样式，都必须手动绑定才能生效，没有被绑定的样式，会被编译，但不会主动生效到你的 DOM 上。

原因是编译出来的样式名已经变化，而你的 DOM 未指定对应的样式名，或者指定的是编译前的命名，所以并不能匹配到正确的样式。

#### useCssModule

这是一个全新的 API ，面向在 script 部分操作 CSS Modules 。

在上面的 [CSS Modules](#style-module-new) 部分可以知道，你可以在 `style` 定义好样式，然后在 `template` 部分通过变量名来绑定样式。

那么如果有一天有个需求，你需要通过 `v-html` 来渲染 HTML 代码，那这里的样式岂不是凉凉了？当然不会！

Vue 3.x 提供了一个 Composition API `useCssModule` 来帮助你在 `setup` 函数里操作你的 CSS Modules 。

**基本用法：**

我们绑定多几个样式，再来操作：

```vue
<template>
  <p :class="$style.msg">
    <span :class="$style.text">Hello World!</span>
  </p>
</template>

<script lang="ts">
import { defineComponent, useCssModule } from 'vue'

export default defineComponent({
  setup () {
    const style = useCssModule()
    console.log(style)
  }
})
</script>

<style module>
.msg {
  color: #ff0000;
}
.text {
  font-size: 14px;
}
</style>
```

可以看到打印出来的 `style` 是一个对象：

- `key` 是你在 `<style modules>` 里定义的原始样式名
- `value` 则是编译后的新样式名

```js
{
  msg: 'home_msg_37Xmr',
  text: 'home_text_2woQJ'
}
```

所以我们来配合 [模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Template_literals) 的使用，看看刚刚说的，要通过 `v-html` 渲染出来的内容应该如何绑定样式：

```vue
<template>
  <div v-html="content"></div>
</template>

<script lang="ts">
import { defineComponent, useCssModule } from 'vue'

export default defineComponent({
  setup () {
    // 获取样式
    const style = useCssModule()

    // 编写模板内容
    const content = `<p class="${style.msg}">
      <span class="${style.text}">Hello World! —— from v-html</span>
    </p>`

    return {
      content,
    }
  }
})
</script>

<style module>
.msg {
  color: #ff0000;
}
.text {
  font-size: 14px;
}
</style>
```

是不是也非常简单？可能刚开始不太习惯，但写多几次其实也蛮好玩的这个功能！

另外，需要注意的是，如果你是指定了 modules 的名称，那么必须传入对应的名称作为入参才可以正确拿到这些样式：

比如指定了一个 classes 作为名称：

```vue
<style module="classes">
/* ... */
</style>
```

那么需要通过传入 classes 这个名称才能拿到样式，否则会是一个空对象：

```ts
const style = useCssModule('classes')
```

### 深度操作符

在 [样式表的组件作用域](#样式表的组件作用域) 部分我们了解到，使用 scoped 后，父组件的样式将不会渗透到子组件中，但也不能直接修改子组件的样式。

如果确实需要进行修改子组件的样式，必须通过 `::v-deep`（完整写法） 或者 `:deep`（快捷写法） 操作符来实现。

1. 旧版的深度操作符是 `>>>` 、 `/deep/` 和 `::v-deep`，现在 `>>>` 和 `/deep/` 已进入弃用阶段（虽然暂时还没完全移除）
2. 同时需要注意的是，旧版 `::v-deep` 的写法是作为组合器的方式，写在样式或者元素前面，如：`::v-deep .class-name { /* ... */ }`，现在这种写法也废弃了。
:::

现在不论是 `::v-deep` 还是 `:deep` ，使用方法非常统一，我们来假设 `.b` 是子组件的样式名：

```vue
<style scoped>
.a :deep(.b) {
  /* ... */
}
</style>
```

编译后：

```css
.a[data-v-f3f3eg9] .b {
  /* ... */
}
```

同理，如果你使用 Less 或者 Stylus 这种支持嵌套写法的预处理器，也是可以这样去深度操作的：

```less
.a {
  :deep(.b) {
    /* ... */
  }
}
```

另外，除了操作子组件的样式，那些通过 `v-html` 创建的 DOM 内容，也不受作用域内的样式影响，也可以通过深度操作符来实现样式修改。

# 组件之间的通信

## 父子组件通信

父子组件通信是指，B 组件引入到 A 组件里渲染，此时 A 是 B 的父级；B 组件的一些数据需要从A组件拿，B 组件有时也要告知 A 组件一些数据变化情况。

他们之间的关系如下，`Child.vue` 是直接挂载在 `Father.vue` 下面：

```
Father.vue
└─Child.vue
```

常用的方法有：

方案|父组件向子组件|子组件向父组件
:--|:--|:--
props / emits|props|emits
v-model / emits|v-model|emits
ref / emits|ref|emits
provide / inject|provide|inject
EventBus|emit / on|emit / on
Vuex|-|-

在 2.x，有的同学可能喜欢用 `$attrs / $listeners` 来进行通信，但该方案在 3.x 已经移除了，详见 [移除 $listeners](https://v3.cn.vuejs.org/guide/migration/listeners-removed.html)

## props / emits

这是 Vue 跨组件通信最常用，也是基础的一个方案，它的通信过程是：

1. `Father.vue` 通过 `prop` 向 `Child.vue` 传值（可包含父级定义好的函数）
2. `Child.vue` 通过 `emit` 向 `Father.vue` 触发父组件的事件执行

### 下发 props

下发的过程是在 `Father.vue` 里完成的，父组件在向子组件下发 `props` 之前，需要导入子组件并启用它作为自身的模板，然后在 `setup` 里处理好数据，return 给 `template` 用。

在 `Father.vue` 的 `script` 里：

```ts
import { defineComponent } from 'vue'
import Child from '@cp/Child.vue'

interface Member {
  id: number,
  name: string
};

export default defineComponent({
  // 需要启用子组件作为模板
  components: {
    Child
  },

  // 定义一些数据并return给template用
  setup () {
    const userInfo: Member = {
      id: 1,
      name: 'Petter'
    }

    // 不要忘记return，否则template拿不到数据
    return {
      userInfo
    }
  }
})
```

然后在 `Father.vue` 的 `template` 这边拿到 return 出来的数据，把要传递的数据通过属性的方式绑定在 `template` 的组件标签上。

```vue
<template>
  <Child
    title="用户信息"
    :index="1"
    :uid="userInfo.id"
    :user-name="userInfo.name"
  />
</template>
```

这样就完成了 `props` 数据的下发。

### 接收 props

接收的过程是在 `Child.vue` 里完成的，在 `script` 部分，子组件通过与 `setup` 同级的 `props` 来接收数据。

它可以是一个数组，每个 `item` 都是 `String` 类型，把你要接受的变量名放到这个数组里，直接放进来作为数组的 `item`：

```ts
export default defineComponent({
  props: [
    'title',
    'index',
    'userName',
    'uid'
  ]
})
```

但这种情况下，使用者不知道这些属性到底是什么类型的值，是否必传。

### 带有类型限制的 props

注意，和 TS 的类型定义不同， `props` 这里的类型，首字母需要大写。

支持的类型有：

类型|含义
:--|:--
String|字符串
Number|数值
Boolean|布尔值
Array|数组
Object|对象
Date|日期数据，e.g. new Date()
Function|函数，e.g. 普通函数、箭头函数、构造函数
Promise|Promise 类型的函数
Symbol|Symbol 类型的值

于是我们把 `props` 再改一下，加上类型限制：

```ts
export default defineComponent({
  props: {
    title: String,
    index: Number,
    userName: String,
    uid: Number
  }
})
```

这样我们如果传入不正确的类型，程序就会抛出警告信息，告知开发者必须正确传值。

如果你需要对某个 `prop` 允许多类型，比如这个 `uid` 字段，它可能是数值，也可能是字符串，那么可以在类型这里，使用一个数组，把允许的类型都加进去。

```ts
export default defineComponent({
  props: {
    // 单类型
    title: String,
    index: Number,
    userName: String,

    // 这里使用了多种类型
    uid: [ Number, String ]
  }
})
```

### 可选以及带有默认值的 props

有时候我们想对一些 `prop` 设置为可选，然后提供一些默认值，还可以再将 `prop` 再进一步设置为对象，支持的字段有：

字段|类型|含义|
:--|:--|:--
type|string|prop 的类型
required|boolean|是否必传，true=必传，false=可选
default|any|与 type 字段的类型相对应的默认值，如果 required 是 false ，但这里不设置默认值，则会默认为 `undefined`
validator|function|自定义验证函数，需要 return 一个布尔值，true=校验通过，false=校验不通过，当校验不通过时，控制台会抛出警告信息

我们现在再对 `props` 改造一下，对部分字段设置为可选，并提供默认值：

```ts
export default defineComponent({
  props: {
    // 可选，并提供默认值
    title: {
      type: String,
      required: false,
      default: '默认标题'
    },

    // 默认可选，单类型
    index: Number,

    // 添加一些自定义校验
    userName: {
      type: String,

      // 在这里校验用户名必须至少3个字
      validator: v => v.length >= 3
    },

    // 默认可选，但允许多种类型
    uid: [ Number, String ]
  }
})
```

### 使用 props

> 注：这一小节的步骤是在 `Child.vue` 里操作。

在 `template` 部分，3.x 的使用方法和 2.x 是一样的，比如要渲染我们上面传入的 `props` ：

```vue
<template>
  <p>标题：{{ title }}</p>
  <p>索引：{{ index }}</p>
  <p>用户id：{{ uid }}</p>
  <p>用户名：{{ userName }}</p>
</template>
```

**但是 `script` 部分，变化非常大！**

在 2.x ，只需要通过 `this.uid`、`this.userName` 就可以使用父组件传下来的 `prop` 。

但是 3.x 没有了 `this`， 需要给 `setup` 添加一个入参才可以去操作。

```ts
export default defineComponent({
  props: {
    title: String,
    index: Number,
    userName: String,
    uid: Number
  },

  // 在这里需要添加一个入参
  setup (props) {

    // 该入参包含了我们定义的所有props
    console.log(props);

  }
})
```

1. `prop` 是只读，不允许修改
2. `setup` 的第一个入参，包含了我们定义的所有props（如果在 `Child.vue` 里未定义，但 父组件 `Father.vue` 那边非要传过来的，不会拿到，且控制台会有警告信息）

### 传递非 Prop 的 Attribute

上面的提示里有提到一句：

> 如果在 `Child.vue` 里未定义，但 父组件 `Father.vue` 那边非要传过来的，不会拿到，且控制台会有警告信息

但并不意味着你不能传递任何未定义的属性数据，在父组件，除了可以给子组件绑定 props，你还可以根据实际需要去绑定一些特殊的属性。

比如给子组件设置 `class`、`id`，或者 `data-xxx` 之类的一些自定义属性，如果 `Child.vue` 组件的 `template` 只有一个根节点，这些属性默认自动继承，并渲染在 node 节点上。

在 `Father.vue` 里，对 `Child.vue` 传递了 `class`、`id` 和 `data-hash`：

```vue
<template>
  <Child
    class="child"
    keys="aaaa"
    data-hash="afJasdHGUHa87d688723kjaghdhja"
  />
</template>
```

渲染后（2个 `data-v-xxx` 是父子组件各自的 `css scoped` 标记）：

```html
<div
  class="child"
  keys="aaaa"
  data-hash="afJasdHGUHa87d688723kjaghdhja"
  data-v-2dcc19c8=""
  data-v-7eb2bc79=""
>
  <!-- Child的内容 -->
</div>
```

你可以在 `Child.vue` 配置 `inheritAttrs` 为 `false`，来屏蔽这些自定义属性的渲染。

```ts
export default defineComponent({
  inheritAttrs: false,
  setup () {
    // ...    
  }
})
```

### 获取非 Prop 的 Attribute

想要拿到这些属性，原生操作需要通过 `element.getAttribute` ，但 Vue 也提供了相关的 API ：

在 `Child.vue` 里，可以通过 `setup` 的第二个参数 `context` 里的 `attrs` 来获取到这些属性。

```ts
export default defineComponent({
  setup (props, { attrs }) {
    // attrs 是个对象，每个 Attribute 都是它的 key
    console.log(attrs.class);

    // 如果传下来的 Attribute 带有短横线，需要通过这种方式获取
    console.log(attrs['data-hash']);
  }
})
```

1. `attr` 和 `prop` 一样，都是只读的
2. 不管 `inheritAttrs` 是否设置，都可以通过 `attrs` 拿到这些数据，但是 `element.getAttribute` 则只有 `inheritAttrs` 为 `true` 的时候才可以。

Vue 3.x 的 `template` 还允许多个根节点，多个根节点的情况下，无法直接继承这些属性，需要在 `Child.vue` 指定继承在哪个节点上，否则会有警告信息。

```vue
<template>
  <!-- 指定继承 -->
  <p v-bind="attrs"></p>
  <!-- 指定继承 -->
  
  <!-- 这些不会自动继承 -->
  <p></p>
  <p></p>
  <p></p>
  <!-- 这些不会自动继承 -->
</template>
```

当然，前提依然是，`setup` 里要把 `attrs` 给 `return` 出来。

查看详情：[多个根节点上的 Attribute 继承](https://v3.cn.vuejs.org/guide/component-attrs.html#%E5%A4%9A%E4%B8%AA%E6%A0%B9%E8%8A%82%E7%82%B9%E4%B8%8A%E7%9A%84-attribute-%E7%BB%A7%E6%89%BF)

### 绑定 emits

最开始有介绍到，子组件如果需要向父组件告知数据更新，或者执行某些函数时，是通过 emits 来进行的。

每个 `emit` 都是事件，所以需要先由父组件先给子组件绑定，子组件才能知道应该怎么去调用。

:::tip
当然，父组件也是需要先在 `setup` 里进行定义并 `return`，才能够在 `template` 里绑定给子组件。
:::

比如要给 `Child.vue` 绑定一个更新用户年龄的方法，那么在 `Father.vue` 里需要这么处理：

先看 `script` 部分（留意注释部分）：

```ts
import { defineComponent, reactive } from 'vue'
import Child from '@cp/Child.vue'

interface Member {
  id: number,
  name: string,
  age: number
};

export default defineComponent({
  components: {
    Child
  },
  setup () {
    const userInfo: Member = reactive({
      id: 1,
      name: 'Petter',
      age: 0
    })

    // 定义一个更新年龄的方法
    const updateAge = (age: number): void => {
      userInfo.age = age;
    }

    return {
      userInfo,

      // return给template用
      updateAge
    }
  }
})
```

再看 `template` 部分（为了方便阅读，我把之前绑定的 props 先去掉了）：

```vue
<template>
  <Child
    @update-age="updateAge"
  />
</template>
```

### 接收 emits

> 注：这一小节的步骤是在 `Child.vue` 里操作。

和 `props` 一样，你可以指定是一个数组，把要接收的 `emit` 名称写进去：

```ts
export default defineComponent({
  emits: [
    'update-age'
  ]
})
```

其实日常这样配置就足够用了。

:::tip
1. 这里的 `emit` 名称指 `Father.vue` 在给 `Child.vue` 绑定事件时，`template` 里面给子组件指定的 `@aaaaa="bbbbb"` 里的 `aaaaa`

2. 当在 emits 选项中定义了原生事件 (如 `click` ) 时，将使用组件中的事件替代原生事件侦听器
:::

### 接收 emits 时做一些校验

当然你也可以对这些事件做一些验证，配置为对象，然后把这个 `emit` 名称作为 `key`， `value` 则配置为一个方法。

比如上面的更新年龄，只允许达到成年人的年龄才会去更新父组件的数据：

```ts
export default defineComponent({
  emits: {
    // 需要校验
    'update-age': (age: number) => {
      // 写一些条件拦截，记得返回false
      if ( age < 18 ) {
        console.log('未成年人不允许参与');
        return false;
      }

      // 通过则返回true
      return true;
    },

    // 一些无需校验的，设置为null即可
    'update-name': null
  }
})
```

### 调用 emits

> 注：这一小节的步骤是在 `Child.vue` 里操作。

和 `props` 一样，也需要在 `setup` 的入参里引入 `emit` ，才允许操作。

`setup` 的第二个入参 `expose` 是一个对象，你可以完整导入 `expose` 然后通过 `expose.emit` 去操作，也可以按需导入 `{ emit }` （推荐这种方式）：

```ts
export default defineComponent({
  emits: [
    'update-age'
  ],
  setup (props, { emit }) {
    
    // 2s 后更新年龄
    setTimeout( () => {
      emit('update-age', 22);
    }, 2000);

  }
})
```

:::tip
`emit` 的第二个参数开始是父组件那边要接收的自定义数据，为了开发上的便利，建议如果需要传多个数据的情况下，直接将第二个参数设置为一个对象，把所有数据都放到对象里，传递和接收起来都会方便很多。
:::

## v-model / emits

对比 `props / emits` ，这个方式更为简单：

1. 在 `Father.vue` ，通过 `v-model` 向 `Child.vue` 传值

2. `Child.vue` 通过自身设定的 emits 向 `Father.vue` 通知数据更新

`v-model` 的用法和 `props` 非常相似，但是很多操作上更为简化，但操作简单带来的 “副作用” ，就是功能上也没有 `props` 那么多。

### 绑定 v-model

它的和下发 props 的方式类似，都是在子组件上绑定 `Father.vue` 定义好并 `return` 出来的数据。

:::tip
1. 和 2.x 不同， 3.x 可以直接绑定 `v-model` ，而无需在子组件指定 `model` 选项。

2. 另外，3.x 的 `v-model` 需要使用 `:` 来指定你要绑定的属性名，同时也开始支持绑定多个 `v-model`
:::

我们来看看具体的操作：

```vue
<template>
  <Child
    v-model:user-name="userInfo.name"
  />
</template>
```

如果你要绑定多个数据，写多个 `v-model` 即可

```vue
<template>
  <Child
    v-model:user-name="userInfo.name"
    v-model:uid="userInfo.id"
  />
</template>
```

看到这里应该能明白了，一个 `v-model` 其实就是一个 `prop`，它支持的数据类型，和 `prop` 是一样的。

所以，子组件在接收数据的时候，完全按照 `props` 去定义就可以了。

点击回顾：[接收 props](#接收-props) ，了解在 `Child.vue` 如何接收 `props`，以及相关的 `props` 类型限制等部分内容。

### 配置 emits

> 注：这一小节的步骤是在 `Child.vue` 里操作。

虽然 `v-model` 的配置和 `prop` 相似，但是为什么出这么两个相似的东西？自然是为了简化一些开发上的操作。

使用 props / emits，如果要更新父组件的数据，还需要在父组件定义好方法，然后 `return` 给 `template` 去绑定事件给子组件，才能够更新。

而使用 `v-model / emits` ，无需如此，可以在 `Child.vue` 直接通过 “update:属性名” 的格式，直接定义一个更新事件：

```ts
export default defineComponent({
  props: {
    userName: String,
    uid: Number
  },
  emits: [
    'update:userName',
    'update:uid'
  ]
})
```

btw: 这里的 update 后面的属性名，支持驼峰写法，这一部分和 2.x 的使用是相同的。

这里也可以对数据更新做一些校验，配置方式和 [接收 emits 时做一些校验](#接收-emits-时做一些校验) 是一样的。

### 调用自身的 emits

> 注：这一小节的步骤是在 `Child.vue` 里操作。

在 `Child.vue` 配置好 emits 之后，就可以在 `setup` 里直接操作数据的更新了：

```ts
export default defineComponent({
  // ...
  setup (props, { emit }) {

    // 2s 后更新用户名
    setTimeout(() => {
      emit('update:userName', 'Tom')
    }, 2000);

  }
})
```

在使用上，和 [调用 emits](#调用-emits-new) 是一样的。

## ref / emits

在学习 [响应式 API 之 ref](component.md#响应式-api-之-ref-new) 的时候，我们了解到 `ref` 是可以用在 [DOM 元素与子组件](component.md#dom-元素与子组件) 上面。

### 父组件操作子组件

所以，父组件也可以直接通过对子组件绑定 `ref` 属性，然后通过 ref 变量去操作子组件的数据或者调用里面的方法。

比如导入了一个 `Child.vue` 作为子组件，需要在 `template` 处给子组件标签绑定 `ref`：

```vue
<template>
  <Child ref="child" />
</template>
```

然后在 `script` 部分定义好对应的变量名称（记得要 `return` 出来）：

```ts
import { defineComponent, onMounted, ref } from 'vue'
import Child from '@cp/Child.vue'

export default defineComponent({
  components: {
    Child
  },
  setup () {
    // 给子组件定义一个ref变量
    const child = ref<HTMLElement>(null);

    // 请保证视图渲染完毕后再执行操作
    onMounted( () => {
      // 执行子组件里面的ajax函数
      child.value.getList();

      // 打开子组件里面的弹窗
      child.value.isShowDialog = true;
    });

    // 必须return出去才可以给到template使用
    return {
      child
    }
  }
})
```

### 子组件通知父组件

子组件如果想主动向父组件通讯，也需要使用 `emit`，详细的配置方法可见：[绑定 emits](#绑定-emits-new)

## 爷孙组件通信

顾名思义，爷孙组件是比 [父子组件通信](#父子组件通信) 要更深层次的引用关系（也有称之为 “隔代组件”）：

C组件引入到B组件里，B组件引入到A组件里渲染，此时A是C的爷爷级别（可能还有更多层级关系），如果你用 `props` ，只能一级一级传递下去，那就太繁琐了，因此我们需要更直接的通信方式。

他们之间的关系如下，`Grandson.vue` 并非直接挂载在 `Grandfather.vue` 下面，他们之间还隔着至少一个 `Son.vue` （可能有多个）：

```
Grandfather.vue
└─Son.vue
  └─Grandson.vue
```

这一 Part 就是讲一讲 C 和 A 之间的数据传递，常用的方法有：

方案|爷组件向孙组件|孙组件向爷组件
:--|:--|:--
provide / inject|provide|inject
EventBus|emit / on|emit / on
Vuex|-|-

为了方便阅读，下面的父组件统一叫 `Grandfather.vue`，子组件统一叫 `Grandson.vue`，但实际上他们之间可以隔无数代…

:::tip
因为上下级的关系的一致性，爷孙组件通信的方案也适用于 [父子组件通信](#父子组件通信) ，只需要把爷孙关系换成父子关系即可。
:::

## provide / inject

这个特性有两个部分：`Grandfather.vue` 有一个 `provide` 选项来提供数据，`Grandson.vue` 有一个 `inject` 选项来开始使用这些数据。

1. `Grandfather.vue` 通过 `provide` 向 `Grandson.vue` 传值（可包含定义好的函数）

2. `Grandson.vue` 通过 `inject` 向 `Grandfather.vue` 触发爷爷组件的事件执行

无论组件层次结构有多深，发起 `provide` 的组件都可以作为其所有下级组件的依赖提供者。

:::tip
这一部分的内容变化都特别大，但使用起来其实也很简单，不用慌，也有相同的地方：

1. 父组件不需要知道哪些子组件使用它 provide 的 property
2. 子组件不需要知道 inject property 来自哪里

另外，要切记一点就是：provide 和 inject 绑定并不是可响应的。这是刻意为之的，但如果传入了一个可监听的对象，那么其对象的 property 还是可响应的。
:::

### 发起 provide

我们先来回顾一下 2.x 的用法：

```ts
export default {
  // 定义好数据
  data () {
    return {
      tags: [ '中餐', '粤菜', '烧腊' ]
    }
  },
  // provide出去
  provide () {
    return {
      tags: this.tags
    }
  }
}
```

旧版的 `provide` 用法和 `data` 类似，都是配置为一个返回对象的函数。

3.x 的新版 `provide`， 和 2.x 的用法区别比较大。

:::tip
在 3.x ， `provide` 需要导入并在 `setup` 里启用，并且现在是一个全新的方法。

每次要 `provide` 一个数据的时候，就要单独调用一次。
:::

每次调用的时候，都需要传入 2 个参数：

参数|类型|说明
:--|:--|:--
key|string|数据的名称
value|any|数据的值

来看一下如何创建一个 `provide`：

```ts
// 记得导入provide
import { defineComponent, provide } from 'vue'

export default defineComponent({
  // ...
  setup () {
    // 定义好数据
    const msg: string = 'Hello World!';

    // provide出去
    provide('msg', msg);
  }
})
```

操作非常简单对吧哈哈哈，但需要注意的是，`provide` 不是响应式的，如果你要使其具备响应性，你需要传入响应式数据，详见：[响应性数据的传递与接收](#响应性数据的传递与接收-new)

### 接收 inject

也是先来回顾一下 2.x 的用法：

```ts
export default {
  inject: [
    'tags'
  ],
  mounted () {
    console.log(this.tags);
  }
}
```

旧版的 `inject` 用法和 `props` 类似，3.x 的新版 `inject`， 和 2.x 的用法区别也是比较大。

:::tip
在 3.x， `inject` 和 `provide` 一样，也是需要先导入然后在 `setup` 里启用，也是一个全新的方法。

每次要 `inject` 一个数据的时候，就要单独调用一次。
:::

每次调用的时候，只需要传入 1 个参数：

参数|类型|说明
:--|:--|:--
key|string|与 `provide` 相对应的数据名称

来看一下如何创建一个 `inject`：

```ts
// 记得导入inject
import { defineComponent, inject } from 'vue'

export default defineComponent({
  // ...
  setup () {
    const msg: string = inject('msg') || '';
  }
})
```

也是很简单（写 TS 的话，由于 `inject` 到的值可能是 `undefined`，所以要么加个 `undefined` 类型，要么给变量设置一个空的默认值）。

### 响应性数据的传递与接收

之所以要单独拿出来说， 是因为变化真的很大 - -

在前面我们已经知道，provide 和 inject 本身不可响应，但是并非完全不能够拿到响应的结果，只需要我们传入的数据具备响应性，它依然能够提供响应支持。

我们以 `ref` 和 `reactive` 为例，来看看应该怎么发起 `provide` 和接收 `inject`。

对这 2 个 API 还不熟悉的同学，建议先阅读一下 [响应式 API 之 ref](component.md#响应式-api-之-ref-new) 和 [响应式 API 之 reactive](component.md#响应式-api-之-reactive-new) 。 

先在 `Grandfather.vue` 里 `provide` 数据：

```ts
export default defineComponent({
  // ...
  setup () {
    // provide一个ref
    const msg = ref<string>('Hello World!');
    provide('msg', msg);

    // provide一个reactive
    const userInfo: Member = reactive({
      id: 1,
      name: 'Petter'
    });
    provide('userInfo', userInfo);

    // 2s 后更新数据
    setTimeout(() => {
      // 修改消息内容
      msg.value = 'Hi World!';

      // 修改用户名
      userInfo.name = 'Tom';
    }, 2000);
  }
})
```

在 `Grandsun.vue` 里 `inject` 拿到数据：

```ts
export default defineComponent({
  setup () {
    // 获取数据
    const msg = inject('msg');
    const userInfo = inject('userInfo');

    // 打印刚刚拿到的数据
    console.log(msg);
    console.log(userInfo);

    // 因为 2s 后数据会变，我们 3s 后再看下，可以争取拿到新的数据
    setTimeout(() => {
      console.log(msg);
      console.log(userInfo);
    }, 3000);

    // 响应式数据还可以直接给 template 使用，会实时更新
    return {
      msg,
      userInfo
    }
  }
})
```

非常简单，非常方便！！！

:::tip
响应式的数据 `provide` 出去，在子孙组件拿到的也是响应式的，并且可以如同自身定义的响应式变量一样，直接 `return` 给 `template` 使用，一旦数据有变化，视图也会立即更新。

但上面这句话有效的前提是，不破坏数据的响应性，比如 ref 变量，你需要完整的传入，而不能只传入它的 `value`，对于 `reactive` 也是同理，不能直接解构去破坏原本的响应性。

切记！切记！！！
:::

### 引用类型的传递与接收

> 这里是针对非响应性数据的处理

provide 和 inject 并不是可响应的，这是官方的故意设计，但是由于引用类型的特殊性，在子孙组件拿到了数据之后，他们的属性还是可以正常的响应变化。

先在 `Grandfather.vue` 里 `provide` 数据：

```ts
export default defineComponent({
  // ...
  setup () {
    // provide 一个数组
    const tags: string[] = [ '中餐', '粤菜', '烧腊' ];
    provide('tags', tags);

    // provide 一个对象
    const userInfo: Member = {
      id: 1,
      name: 'Petter'
    };
    provide('userInfo', userInfo);

    // 2s 后更新数据
    setTimeout(() => {
      // 增加tags的长度
      tags.push('叉烧');

      // 修改userInfo的属性值
      userInfo.name = 'Tom';
    }, 2000);
  }
})
```

在 `Grandsun.vue` 里 `inject` 拿到数据：

```ts
export default defineComponent({
  setup () {
    // 获取数据
    const tags: string[] = inject('tags') || [];
    const userInfo: Member = inject('userInfo') || {
      id: 0,
      name: ''
    };

    // 打印刚刚拿到的数据
    console.log(tags);
    console.log(tags.length);
    console.log(userInfo);

    // 因为 2s 后数据会变，我们 3s 后再看下，能够看到已经是更新后的数据了
    setTimeout(() => {
      console.log(tags);
      console.log(tags.length);
      console.log(userInfo);
    }, 3000);
  }
})
```

引用类型的数据，拿到后可以直接用，属性的值更新后，子孙组件也会被更新。

:::warning
由于不具备真正的响应性，`return` 给模板使用依然不会更新视图，如果涉及到视图的数据，请依然使用 [响应式 API](component.md#响应式数据的变化-new) 。
:::

### 基本类型的传递与接收

> 这里是针对非响应性数据的处理

基本数据类型被直接 `provide` 出去后，再怎么修改，都无法更新下去，子孙组件拿到的永远是第一次的那个值。

先在 `Grandfather.vue` 里 `provide` 数据：

```ts
export default defineComponent({
  // ...
  setup () {
    // provide 一个数组的长度
    const tags: string[] = [ '中餐', '粤菜', '烧腊' ];
    provide('tagsCount', tags.length);

    // provide 一个字符串
    let name: string = 'Petter';
    provide('name', name);

    // 2s 后更新数据
    setTimeout(() => {
      // tagsCount 在 Grandson 那边依然是 3
      tags.push('叉烧');

      // name 在 Grandson 那边依然是 Petter
      name = 'Tom';
    }, 2000);
  }
})
```

在 `Grandsun.vue` 里 `inject` 拿到数据：

```ts
export default defineComponent({
  setup () {
    // 获取数据
    const name: string = inject('name') || '';
    const tagsCount: number = inject('tagsCount') || 0;

    // 打印刚刚拿到的数据
    console.log(name);
    console.log(tagsCount);

    // 因为 2s 后数据会变，我们 3s 后再看下
    setTimeout(() => {
      // 依然是 Petter
      console.log(name);

      // 依然是 3
      console.log(tagsCount);
    }, 3000);
  }
})
```

很失望，并没有变化。

:::tip
那么是否一定要定义成响应式数据或者引用类型数据呢？

当然不是，我们在 `provide` 的时候，也可以稍作修改，让它能够同步更新下去。
:::

我们再来一次，依然是先在 `Grandfather.vue` 里 `provide` 数据：

```ts
export default defineComponent({
  // ...
  setup () {
    // provide 一个数组的长度
    const tags: string[] = [ '中餐', '粤菜', '烧腊' ];
    provide('tagsCount', (): number => {
      return tags.length;
    });

    // provide 字符串
    let name: string = 'Petter';
    provide('name', (): string => {
      return name;
    });

    // 2s 后更新数据
    setTimeout(() => {
      // tagsCount 现在可以正常拿到 4 了
      tags.push('叉烧');

      // name 现在可以正常拿到 Tom 了
      name = 'Tom';
    }, 2000);
  }
})
```

再来 `Grandsun.vue` 里修改一下 `inject` 的方式，看看这次拿到的数据：

```ts
export default defineComponent({
  setup () {
    // 获取数据
    const tagsCount: any = inject('tagsCount');
    const name: any = inject('name');

    // 打印刚刚拿到的数据
    console.log(tagsCount());
    console.log(name());

    // 因为 2s 后数据会变，我们 3s 后再看下
    setTimeout(() => {
      // 现在可以正确得到 4
      console.log(tagsCount());

      // 现在可以正确得到 Tom
      console.log(name());
    }, 3000);
  }
})
```

这次可以正确拿到数据了，看出这2次的写法有什么区别了吗？

:::tip
基本数据类型，需要 `provide` 一个函数，将其 `return` 出去给子孙组件用，这样子孙组件每次拿到的数据才会是新的。

但由于不具备响应性，所以子孙组件每次都需要重新通过执行 `inject` 得到的函数才能拿到最新的数据。
:::

按我个人习惯来说，使用起来挺别扭的，能不用就不用……

:::warning
由于不具备真正的响应性，`return` 给模板使用依然不会更新视图，如果涉及到视图的数据，请依然使用 [响应式 API](component.md#响应式数据的变化-new) 。
:::

## 兄弟组件通信

兄弟组件是指两个组件都挂载在同一个 `Father.vue` 下，但两个组件之间并没有什么直接的关联，先看看他们的关系：

```
Father.vue
├─Brother.vue
└─LittleBrother.vue
```

既然没有什么直接关联， ╮(╯▽╰)╭ 所以也没有什么专属于他们的通信方式。

如果他们之间要交流，目前大概有这两类选择：

1. 【不推荐】先把数据传给 `Father.vue`，再通过 [父子组件通信](#父子组件通信) 的方案去交流

2. 【推荐】借助 [全局组件通信](#全局组件通信) 的方案才能达到目的。

## 全局组件通信

全局组件通信是指，两个任意的组件，不管是否有关联（e.g. 父子、爷孙）的组件，都可以直接进行交流的通信方案。

举个例子，像下面这样，`B2.vue` 可以采用全局通信方案，直接向 `D2.vue` 发起交流，而无需经过他们的父组件。

```
A.vue
├─B1.vue
├───C1.vue
├─────D1.vue
├─────D2.vue
├───C2.vue
├─────D3.vue
└─B2.vue
```

常用的方法有：

方案|发起方|接收方|对应章节传送门
:--|:--|:--|:--
EventBus|emit|on|[点击查看](#eventbus-new)
Vuex|-|-|[点击查看](#vuex-new)

## EventBus

`EventBus` 通常被称之为 “全局事件总线” ，它是用来在全局范围内通信的一个常用方案，它的特点就是： “简单” 、 “灵活” 、“轻量级”。

:::tip
在中小型项目，全局通信推荐优先采用该方案，事件总线在打包压缩后不到 200 个字节， API 也非常简单和灵活。
:::

### 回顾 2.x

在 2.x，使用 EventBus 无需导入第三方插件，直接在自己的 `libs` 文件夹下创建一个 `bus.ts` 文件，暴露一个新的 Vue 实例即可。
 
```ts
import Vue from 'vue';
export default new Vue();
```

然后就可以在组件里引入 bus ，通过 `$emit` 去发起交流，通过 `$on` 去监听接收交流。

旧版方案的完整案例代码可以查看官方的 [2.x 语法 - 事件 API](https://v3.cn.vuejs.org/guide/migration/events-api.html#_2-x-%E8%AF%AD%E6%B3%95)

### 了解 3.x

Vue 3.x 移除了 `$on` 、 `$off` 和 `$once` 这几个事件 API ，应用实例不再实现事件触发接口。

根据官方文档在 [迁移策略 - 事件 API](https://v3.cn.vuejs.org/guide/migration/events-api.html#%E8%BF%81%E7%A7%BB%E7%AD%96%E7%95%A5) 的推荐，我们可以用 [mitt](https://github.com/developit/mitt) 或者 [tiny-emitter](https://github.com/scottcorgan/tiny-emitter) 等第三方插件来实现 `EventBus` 。

### 创建 3.x 的 EventBus

这里以 `mitt` 为例，示范如何创建一个 Vue 3.x 的 `EventBus` 。

首先，需要安装 `mitt` ：

```
npm install --save mitt
```

然后在 `libs` 文件夹下，创建一个 `bus.ts` 文件，内容和旧版写法其实是一样的，只不过是把 Vue 实例，换成了 mitt 实例。

```ts
import mitt from 'mitt';
export default mitt();
```

然后就可以定义发起和接收的相关事件了，常用的 API 和参数如下：

方法名称|作用
:--|:--
on|注册一个监听事件，用于接收数据
emit|调用方法发起数据传递
off|用来移除监听事件

`on` 的参数：

参数|类型|作用
:--|:--|:--
type|string \| symbol|方法名
handler|function|接收到数据之后要做什么处理的回调函数

这里的 `handler` 建议使用具名函数，因为匿名函数无法销毁。

`emit` 的参数：

参数|类型|作用
:--|:--|:--
type|string \| symbol|与 on 对应的方法名
data|any|与 on 对应的，允许接收的数据

`off` 的参数：

参数|类型|作用
:--|:--|:--
type|string \| symbol|与 on 对应的方法名
handler|function|要删除的，与 on 对应的 handler 函数名

更多的 API 可以查阅 [插件的官方文档](https://github.com/developit/mitt) ，在了解了最基本的用法之后，我们来开始配置一对交流。

:::tip
如果你需要把 `bus` 配置为全局 API ，不想在每个组件里分别 import 的话，可以参考之前的章节内容： [全局 API 挂载](plugin.md#全局-api-挂载) 。
:::

### 创建和移除监听事件

在需要暴露交流事件的组件里，通过 `on` 配置好接收方法，同时为了避免路由切换过程中造成事件多次被绑定，多次触发，需要在适当的时机 `off` 掉：

```ts
import { defineComponent, onBeforeUnmount } from 'vue'
import bus from '@libs/bus'

export default defineComponent({
  setup () {
    // 定义一个打招呼的方法
    const sayHi = (msg: string = 'Hello World!'): void => {
      console.log(msg);
    }

    // 启用监听
    bus.on('sayHi', sayHi);

    // 在组件卸载之前移除监听
    onBeforeUnmount( () => {
      bus.off('sayHi', sayHi);
    })
  }
})
```

btw: 关于销毁的时机，可以参考 [组件的生命周期](component.md#组件的生命周期-new) 。

### 调用监听事件

在需要调用交流事件的组件里，通过 `emit` 进行调用：

```ts
import { defineComponent } from 'vue'
import bus from '@libs/bus'

export default defineComponent({
  setup () {
    // 调用打招呼事件，传入消息内容
    bus.emit('sayHi', '哈哈哈哈哈哈哈哈哈哈哈哈哈哈');
  }
})
```

### 旧项目升级 EventBus

在 [Vue 3.x 的 EventBus](#创建-3-x-的-eventbus-new)，我们可以看到它的 API 和旧版是非常接近的，只是去掉了 `$` 符号。

如果你要对旧的项目进行升级改造，因为原来都是使用了 `$on` 、 `$emit` 等旧的 API ，一个一个组件去修改成新的 API 肯定不现实。

我们可以在创建 `bus.ts` 的时候，通过自定义一个 `bus` 对象，来挂载 `mitt` 的 API 。

在 `bus.ts` 里，改成以下代码：

```ts
import mitt from 'mitt';

// 初始化一个 mitt 实例
const emitter = mitt();

// 定义一个空对象用来承载我们的自定义方法
const bus: any = {};

// 把你要用到的方法添加到 bus 对象上
bus.$on = emitter.on;
bus.$emit = emitter.emit;

// 最终是暴露自己定义的 bus
export default bus;
```

这样我们在组件里就可以继续使用 `bus.$on` 、`bus.$emit` 等以前的老 API 了，不影响我们旧项目的升级使用。

## Vuex

Vuex 是 Vue 生态里面非常重要的一个成员，运用于状态管理模式。

它也是一个全局的通信方案，对比 [EventBus](#eventbus-new)，Vuex 的功能更多，更灵活，但对应的，学习成本和体积也相对较大，通常大型项目才会用上 Vuex。

摘取一段官网的介绍，官方也只建议在大型项目里才用它：

>**什么情况下我应该使用 Vuex？**<br>
>Vuex 可以帮助我们管理共享状态，并附带了更多的概念和框架。这需要对短期和长期效益进行权衡。<br>
>如果您不打算开发大型单页应用，使用 Vuex 可能是繁琐冗余的。

### 在了解之前

在对 Vue 3.x 里是否需要使用 Vuex 的问题上，带有一定的争议，大部分开发者在社区发表的评论都认为通过 [EventBus](#eventbus-new) 和 [provide / inject](#provide-inject) ，甚至 export 一个 [reactive](component.md#响应式-api-之-reactive-new) 对象也足以满足大部分业务需求。

见仁见智，请根据自己的实际需要去看是否需要启用它。

好在新版 Vuex 和旧版几乎没什么区别，大家可以了解一下大概的变化之后，按照之前的官网文档去配置，使用其他应该没有太大的问题。

### Vuex 的目录结构

如果你在创建 Vue 项目的时候选择了带上 Vuex ，那么 `src` 文件夹下会自动生成 Vuex 的相关文件，如果创建时没有选择，你也可以自己按照下面解构去创建对应的目录与文件。

```
src
├─store
├───index.ts
└─main.ts
```

一般情况下一个 `index.ts` 足矣，它是 Vuex 的入口文件，如果你的项目比较庞大，你可以在 `store` 下创建一个 `modules` 文件夹，用 Vuex Modules 的方式导入到 `index.ts` 里去注册。

### 回顾 2.x

在 2.x ，你需要先分别导入 `Vue` 和 `Vuex`，`use` 后通过 `new Vuex.Store(...)` 的方式去初始化

```ts
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
```

### 了解 3.x

而 3.x 简化了很多，只需要从 `vuex` 里导入 `createStore`，直接通过 `createStore` 去创建即可。

```ts
import { createStore } from 'vuex'

export default createStore({
  state: {
  },
  mutations: {
  },
  actions: {
  },
  modules: {
  }
})
```

### Vuex 的配置

除了初始化方式有一定的改变，Vuex 的其他的配置和原来是一样的，具体可以查看 [使用指南 - Vuex](https://next.vuex.vuejs.org/zh/guide/)

### 在组件里使用 Vuex

和 2.x 不同的是，3.x 在组件里使用 Vuex，更像新路由那样，需要通过 `useStore` 去启用。

```ts
import { defineComponent } from 'vue'
import { useStore } from 'vuex';

export default defineComponent({
  setup () {
    // 需要创建一个 store 变量
    const store = useStore();

    // 再使用 store 去操作 Vuex 的 API
    // ...
  }
})
```

其他的用法，都是跟原来一样的。

## Pinia (WIP)

由于 Vuex 4.x 版本只是个过渡版，Vuex 4 对 TypeScript 和 Composition API 都不是很友好，虽然官方团队在 GitHub 已有讨论 [Vuex 5](https://github.com/vuejs/rfcs/discussions/270) 的开发提案，但从 2022-02-07 Vue 3 被设置为默认版本开始， Pinia 也正式被官方推荐作为全局状态管理的工具。

点击访问：[Pinia 官网](https://pinia.vuejs.org/)

:::tip
这部分的内容稍后完善，目前我需要找个时间实践体验一下 Pinia 。
:::

# 单组件组件

## script-setup

这是一个比较有争议的新特性，作为 setup 函数的语法糖，褒贬不一，不过经历了几次迭代之后，目前在体验上来说，感受还是非常棒的。

### 新特性的产生背景

在了解它怎么用之前，可以先了解一下它被推出的一些背景，可以帮助你对比开发体验上的异同点，以及了解为什么会有这一章节里面的新东西。

在 Vue 3.0 的 `.vue` 组件里，遵循 SFC 规范要求（注：SFC，即 Single-File Component，`.vue` 单组件），标准的 setup 用法是，在 setup 里面定义的数据如果需要在 template 使用，都需要 return 出来。

如果你使用的是 TypeScript ，还需要借助 [defineComponent](component.md#了解-definecomponent) 来帮助你对类型的自动推导。

```vue
<!-- 标准组件格式 -->
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    // ...

    return {
      // ...
    }
  }
})
</script>
```

script-setup 的推出是为了让熟悉 3.0 的用户可以更高效率的开发组件，减少一些心智负担，只需要给 script 标签添加一个 setup 属性，那么整个 script 就直接会变成 setup 函数，所有顶级变量、函数，均会自动暴露给模板使用（无需再一个个 return 了）。

Vue 会通过单组件编译器，在编译的时候将其处理回标准组件，所以目前这个方案只适合用 `.vue` 文件写的工程化项目。

```vue
<!-- 使用 script-setup 格式 -->
<script setup lang="ts">
  // ...
</script>
```

### 全局编译器宏

在 script-setup 模式下，新增了 4 个全局编译器宏，他们无需 import 就可以直接使用。

但是默认的情况下直接使用，项目的 eslint 会提示你没有导入，但你导入后，控制台的 Vue 编译助手又会提示你不需要导入，就很尴尬…

哈哈哈哈不过不用着急，可以配置一下 lint ，把这几个编译助手写进全局规则里，就可以了，不需要导入也不会报错了。

```js
// 项目根目录下的 .eslintrc.js
module.exports = {
  // 原来的lint规则，补充下面的globals...
  globals: {
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly',
  },
}
```

下面我们继续了解 script-setup 的变化。

### template 操作简化

如果使用 JSX / TSX 写法，这一点没有太大影响，但对于习惯使用 `<template />` 的开发者来说，这是一个非常爽的体验。

主要体现在这两点：

#### 变量无需进行 return

标准组件模式下，setup 里定义的变量，需要 return 后，在 template 部分才可以正确拿到：

```vue
<!-- 标准组件格式 -->
<template>
  <p>{{ msg }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const msg: string = 'Hello World!';
    
    // 要给 template 用的数据需要 return 出来才可以
    return {
      msg
    }
  }
})
</script>
```

在 script-setup 模式下，你定义了就可以直接使用。

```vue
<!-- 使用 script-setup 格式 -->
<template>
  <p>{{ msg }}</p>
</template>

<script setup lang="ts">
const msg: string = 'Hello World!';
</script>
```

#### 子组件无需手动注册

子组件的挂载，在标准组件里的写法是需要 import 后再放到 components 里才能够启用：

```vue
<!-- 标准组件格式 -->
<template>
  <Child />
</template>

<script lang="ts">
import { defineComponent } from 'vue'

// 导入子组件
import Child from '@cp/Child.vue'

export default defineComponent({
  // 需要启用子组件作为模板
  components: {
    Child
  },

  // 组件里的业务代码
  setup () {
    // ...
  }
})
</script>
```

在 script-setup 模式下，只需要导入组件即可，编译器会自动识别并启用。

```vue
<!-- 使用 script-setup 格式 -->
<template>
  <Child />
</template>

<script setup lang="ts">
import Child from '@cp/Child.vue'
</script>
```

### props 的接收方式变化

由于整个 script 都变成了一个大的 setup function ，没有了组件选项，也没有了 setup 入参，所以没办法和标准写法一样去接收 props 了。

这里需要使用一个全新的 API ：`defineProps` 。

`defineProps` 是一个方法，内部返回一个对象，也就是挂载到这个组件上的所有 props ，它和普通的 props 用法一样，如果不指定为 prop， 则传下来的属性会被放到 attrs 那边去。

#### defineProps 的基础用法

所以，如果只是单纯在 template 里使用，那么其实就这么简单定义就可以了：

```ts
defineProps([
  'name',
  'userInfo',
  'tags'
])
```

使用 `string[]` 数组作为入参，把 prop 的名称作为数组的 item 传给 `defineProps` 就可以了。

如果 script 里的方法要拿到 props 的值，你也可以使用字面量定义：

```ts
const props = defineProps([
  'name',
  'userInfo',
  'tags'
])

console.log(props.name);
```

但在作为一个 Vue 老玩家，都清楚不显性的指定 prop 类型的话，很容易在协作中引起程序报错，那么应该如何对每个 prop 进行类型检查呢？

有两种方式来处理类型定义。

#### 通过构造函数检查 prop

这是第一种方式：使用 JavaScript 原生构造函数进行类型规定。

也就是跟我们平时定义 prop 类型时一样， Vue 会通过 `instanceof` 来进行 [类型检查](https://v3.cn.vuejs.org/guide/component-props.html#%E7%B1%BB%E5%9E%8B%E6%A3%80%E6%9F%A5) 。

使用这种方法，需要通过一个 “对象” 入参来传递给 `defineProps` ，比如：

```ts
defineProps({
  name: String,
  userInfo: Object,
  tags: Array
});
```

所有原来 props 具备的校验机制，都可以适用，比如你除了要限制类型外，还想指定 `name` 是可选，并且带有一个默认值：

```ts
defineProps({
  name: {
    type: String,
    required: false,
    default: 'Petter'
  },
  userInfo: Object,
  tags: Array
});
```

#### 使用类型注解检查 prop

这是第二种方式：使用 TypeScript 的类型注解。

和 ref 等 API 的用法一样，`defineProps` 也是可以使用尖括号 <> 来包裹类型定义，紧跟在 API 后面，另外，由于 `defineProps` 返回的是一个对象（因为 props 本身是一个对象），所以尖括号里面的类型还要用大括号包裹，通过 `key: value` 的键值对形式表示，如：

```ts
defineProps<{ name: string }>();
```

注意到了吗？这里使用的类型，和第一种方法提到的指定类型时是不一样的。

在这里，不再使用构造函数校验，而是需要遵循使用 TypeScript 的类型。比如字符串是 `string`，而不是 `String` 。

如果有多个 prop ，就跟写 interface 一样：

```ts
defineProps<{
  name: string;
  phoneNumber: number;
  userInfo: object;
  tags: string[];
}>();
```

其中，举例里的 `userInfo` 是一个对象，你可以简单的指定为 object，也可以先定义好它对应的类型，再进行指定：

```ts
interface UserInfo {
  id: number;
  age: number;
}

defineProps<{
  name: string;
  userInfo: UserInfo;
}>();
```

如果你想对某个数据设置为可选，也是遵循 TS 规范，通过英文问号 `?` 来允许可选：

```ts
// name 是可选
defineProps<{
  name?: string;
  tags: string[];
}>();
```

如果你想设置可选参数的默认值，需要借助 withDefaults API。

#### withDefaults 的基础用法

这个新的 withDefaults API 可以让你在使用 TS 类型系统时，也可以指定 props 的默认值。

它接收两个入参：

参数|类型|含义
:--|:--|:--
props|object|通过 defineProps 传入的 props
defaultValues|object|根据 props 的 key 传入默认值

可能缺乏一些官方描述，还是看参考用法可能更直观：

```ts
withDefaults(defineProps<{
  size?: number
  labels?: string[]
}>(), {
  size: 3,
  labels: () => ['default label']
})
```

如果你要在 TS / JS 再对 props 进行获取，也可以通过字面量来拿到这些默认值：

```ts
// 如果不习惯上面的写法，你也可以跟平时一样先通过interface定义一个类型接口
interface Props {
  msg?: string
}

// 再作为入参传入
const props = withDefaults(defineProps<Props>(), {
  msg: 'hello'
})

// 这样就可以通过props变量拿到需要的prop值了
console.log(props.msg)
```

### emits 的接收方式变化

和 props 一样，emits 的接收也是需要使用一个全新的 API 来操作，这个 API 就是 `defineEmits` 。

和 `defineProps` 一样， `defineEmits` 也是一个方法，它接受的入参格式和标准组件的要求是一致的。

#### defineEmits 的基础用法

由于 emit 并非提供给模板直接读取，所以需要通过字面量来定义 emits。

最基础的用法也是传递一个 `string[]` 数组进来，把每个 emit 的名称作为数组的 item 。

```ts
// 获取 emit
const emit = defineEmits(['chang-name']);

// 调用 emit
emit('chang-name', 'Tom');
```

由于 `defineEmits` 的用法和原来的 emits 选项差别不大，这里也不重复说明更多的诸如校验之类的用法了。

### attrs 的接收方式变化

`attrs` 和 `props` 很相似，也是基于父子通信的数据，如果父组件绑定下来的数据没有被指定为 `props` ，那么就会被挂到 `attrs` 这边来。

在标准组件里， `attrs` 的数据是通过 `setup` 的第二个入参 `context` 里的 `attrs` API 获取的。

```ts
// 标准组件的写法
export default defineComponent({
  setup (props, { attrs }) {
    // attrs 是个对象，每个 Attribute 都是它的 key
    console.log(attrs.class);

    // 如果传下来的 Attribute 带有短横线，需要通过这种方式获取
    console.log(attrs['data-hash']);
  }
})
```

但和 `props` 一样，由于没有了 `context` 参数，需要使用一个新的 API 来拿到 `attrs` 数据。

这个 API 就是 `useAttrs` 。

#### useAttrs 的基础用法

顾名思义， useAttrs 可以是用来获取 attrs 数据的，它的用法非常简单：

```ts
// 导入 useAttrs 组件
import { useAttrs } from 'vue'

// 获取 attrs
const attrs = useAttrs()

// attrs是个对象，和 props 一样，需要通过 key 来得到对应的单个 attr
console.log(attrs.msg);
```

### slots 的接收方式变化

`slots` 是 Vue 组件的插槽数据，也是在父子通信里的一个重要成员。

对于使用 template 的开发者来说，在 script-setup 里获取插槽数据并不困难，因为跟标准组件的写法是完全一样的，可以直接在 template 里使用 `<slot />` 标签渲染。

```vue
<template>
  <div>
    <!-- 插槽数据 -->
    <slot />
    <!-- 插槽数据 -->
  </div>
</template>
```

但对使用 JSX / TSX 的开发者来说，就影响比较大了，在标准组件里，想在 script 里获取插槽数据，也是需要在 `setup` 的第二个入参里拿到 `slots` API 。

```ts
// 标准组件的写法
export default defineComponent({
  // 这里的 slots 就是插槽
  setup (props, { slots }) {
    // ...
  }
})
```

新版本的 Vue 也提供了一个全新的 `useSlots` API 来帮助 script-setup 用户获取插槽。

#### useSlots 的基础用法

先来看看父组件，父组件先为子组件传入插槽数据，支持 “默认插槽” 和 “命名插槽” ：

```vue
<template>
  <!-- 子组件 -->
  <ChildTSX>
    <!-- 默认插槽 -->
    <p>I am a default slot from TSX.</p>
    <!-- 默认插槽 -->

    <!-- 命名插槽 -->
    <template #msg>
      <p>I am a msg slot from TSX.</p>
    </template>
    <!-- 命名插槽 -->
  </ChildTSX>
  <!-- 子组件 -->
</template>

<script setup lang="ts">
import ChildTSX from '@cp/context/Child.tsx'
</script>
```

在使用 JSX / TSX 编写的子组件里，就可以通过 `useSlots` 来获取父组件传进来的 `slots` 数据进行渲染：

```tsx
// 注意：这是一个 .tsx 文件
import { defineComponent, useSlots } from 'vue'

const ChildTSX = defineComponent({
  setup() {
    // 获取插槽数据
    const slots = useSlots()

    // 渲染组件
    return () => (
      <div>
        {/* 渲染默认插槽 */}
        <p>{ slots.default ? slots.default() : '' }</p>

        {/* 渲染命名插槽 */}
        <p>{ slots.msg ? slots.msg() : '' }</p>
      </div>
    )
  },
})

export default ChildTSX
```

### ref 的通信方式变化

在标准组件写法里，子组件的数据都是默认隐式暴露给父组件的，也就是父组件可以通过 `childComponent.value.foo` 这样的方式直接操作子组件的数据。

但在 script-setup 模式下，所有数据只是默认隐式 return 给 template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。

在 script-setup 模式下，如果要调用子组件的数据，需要先在子组件显示的暴露出来，才能够正确的拿到，这个操作，就是由 `defineExpose` 来完成。

#### defineExpose 的基础用法

`defineExpose` 的用法非常简单，它本身是一个函数，可以接受一个对象参数。

在子组件里，像这样把需要暴露出去的数据通过 `key: value` 的形式作为入参（下面的例子是用到了 ES6 的属性的简洁表示法：

```vue
<script setup lang="ts">
// 定义一个想提供给父组件拿到的数据
const msg: string = 'Hello World!';

// 显示暴露的数据，才可以在父组件拿到
defineExpose({
  msg
});
</script>
```

然后你在父组件就可以通过挂载在子组件上的 ref 变量，去拿到暴露出来的数据了。

### 顶级 await 的支持

在 script-setup 模式下，不必再配合 async 就可以直接使用 await 了，这种情况下，组件的 setup 会自动变成 async setup 。

```vue
<script setup lang="ts">
const post = await fetch(`/api/post/1`).then((r) => r.json())
</script>
```

它转换成标准组件的写法就是：

```vue
<script lang="ts">
import { defineComponent, withAsyncContext } from 'vue'

export default defineComponent({
  async setup() {
    const post = await withAsyncContext(
      fetch(`/api/post/1`).then((r) => r.json())
    )

    return {
      post
    }
  }
})
</script>
```