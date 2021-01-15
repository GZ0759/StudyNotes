> learn-vue-source-code  
> 作者：NLRX-WJC
> [原文地址](https://github.com/NLRX-WJC/Blog/tree/master/docs/learn-vue-source-code)

# 1. 写在最前面

## 1.1 学习目录

本项目所剖析的`Vue.js`源码版本是目前最新的版本，版本号为 v2.6.11 ，其代码目录如下：

```bash
├─dist                   # 项目构建后的文件
├─scripts                # 与项目构建相关的脚本和配置文件
├─flow                   # flow的类型声明文件
├─src                    # 项目源代码
│    ├─complier          # 与模板编译相关的代码
│    ├─core              # 通用的、与运行平台无关的运行时代码
│    │  ├─observe        # 实现变化侦测的代码
│    │  ├─vdom           # 实现virtual dom的代码
│    │  ├─instance       # Vue.js实例的构造函数和原型方法
│    │  ├─global-api     # 全局api的代码
│    │  └─components     # 内置组件的代码
│    ├─server            # 与服务端渲染相关的代码
│    ├─platforms         # 特定运行平台的代码，如weex
│    ├─sfc               # 单文件组件的解析代码
│    └─shared            # 项目公用的工具代码
└─test                   # 项目测试代码
```

从上面的目录结构可以看出，`Vue`的整个项目包含了类型检测相关、单元测试相关、与平台无关的核心代码以及跨平台运行的相关代码。

由于我们只是学习`Vue.js`的设计思想以及代码实现的相关逻辑，所以我们暂不去关心类型检测、单元测试以及特定平台运行等相关逻辑实现，仅关注它的核心代码，即`src/core`和`src/complier`这两个目录下的代码，并且接下来后续的学习也都是只在这两个目录的范围之内。

## 1.2 学习路线

在学习之前，我们需要先制定一个学习路线，循序渐进的学习，这样不至于一头雾水，无处下手。后面的学习路线如下：

1. 变化侦测篇

   学习`Vue`中如何实现数据的响应式系统，从而达到数据驱动视图。

2. 虚拟 DOM 篇

   学习什么是虚拟 DOM，以及`Vue`中的`DOM-Diff`原理

3. 模板编译篇

   学习`Vue`内部是怎么把`template`模板编译成虚拟`DOM`,从而渲染出真实`DOM`

4. 实例方法篇

   学习`Vue`中所有实例方法（即所有以`$`开头的方法）的实现原理

5. 全局 API 篇

   学习`Vue`中所有全局`API`的实现原理

6. 生命周期篇

   学习`Vue`中组件的生命周期实现原理

7. 指令篇

   学习`Vue`中所有指令的实现原理

8. 过滤器篇

   学习`Vue`中所有过滤器的实现原理

9. 内置组件篇

   学习`Vue`中内置组件的实现原理

# 2. 变化侦测篇

## 2.1 变化侦测篇综述

### 前言

众所周知，`Vue`最大的特点之一就是数据驱动视图，那么什么是数据驱动视图呢？在这里，我们可以把数据理解为状态，而视图就是用户可直观看到页面。页面不可能是一成不变的，它应该是动态变化的，而它的变化也不应该是无迹可寻的，它或者是由用户操作引起的，亦或者是由后端数据变化引起的，不管它是因为什么引起的，我们统称为它的状态变了，它由前一个状态变到了后一个状态，页面也就应该随之而变化，所以我们就可以得到如下一个公式：

```
<font color="red">**UI = render(state)**</font>
```

上述公式中：状态`state`是输入，页面`UI`输出，状态输入一旦变化了，页面输出也随之而变化。我们把这种特性称之为数据驱动视图。

OK，有了基本概念以后，我们再把上述公式拆成三部分：`state`、`render()`以及`UI`。我们知道`state`和`UI`都是用户定的，而不变的是这个`render()`。所以`Vue`就扮演了`render()`这个角色，当`Vue`发现`state`变化之后，经过一系列加工，最终将变化反应在`UI`上。

那么第一个问题来了，`Vue`怎么知道`state`变化了呢？

### 什么是变化侦测

那`Vue`是怎么知道`state`变化了呢？换句话说，数据变化了是怎么通知给`Vue`呢？那么，这就引出了`Vue`中的变化侦测。

变化侦测就是追踪状态，亦或者说是数据的变化，一旦发生了变化，就要去更新视图。

变化侦测可不是个新名词，它在目前的前端三大框架中均有涉及。在`Angular`中是通过脏值检查流程来实现变化侦测；在`React`是通过对比虚拟`DOM`来实现变化侦测，而在`Vue`中也有自己的一套变化侦测实现机制。

那么，接下来我们就通过阅读源码来学习一下`Vue`是怎么实现自己的对数据变化进行侦测的机制。

### 总结

首先，我们知道了什么是数据驱动视图。数据驱动视图简单来说就是数据变化引起视图变化，那么第一步就是先要知道数据什么时候发生变化，也就是说对数据的变化要进行侦测。

其次，数据的变化侦测在三大框架中均有涉及，不同的框架有着自己的一套侦测机制。

最后，我们从源码出发，学习在`Vue`中是如何对数据进行变化侦测的。

## 2.2 Object 的变化侦测

### 前言

在上一篇文章中，我们知道：数据驱动视图的关键点则在于我们如何知道数据发生了变化，只要知道数据在什么时候变了，那么问题就变得迎刃而解，我们只需在数据变化的时候去通知视图更新即可。

要想知道数据什么时候被读取了或数据什么时候被改写了，其实不难，`JS`为我们提供了`Object.defineProperty`方法，通过该方法我们就可以轻松的知道数据在什么时候发生变化。

### 使 Object 数据变得“可观测”

数据的每次读和写能够被我们看的见，即我们能够知道数据什么时候被读取了或数据什么时候被改写了，我们将其称为数据变的‘可观测’。

要将数据变的‘可观测’，我们就要借助前言中提到的`Object.defineProperty`方法了，在本文中，我们就使用这个方法使数据变得“可观测”。

首先，我们定义一个数据对象`car`：

```javascript
let car = {
  brand: 'BMW',
  price: 3000,
};
```

我们定义了这个`car`的品牌`brand`是`BMW`,价格`price`是 3000。现在我们可以通过`car.brand`和`car.price`直接读写这个`car`对应的属性值。但是，当这个`car`的属性被读取或修改时，我们并不知情。那么应该如何做才能够让`car`主动告诉我们，它的属性被修改了呢？

接下来，我们使用`Object.defineProperty() `改写上面的例子：

```javascript
let car = {};
let val = 3000;
Object.defineProperty(car, 'price', {
  enumerable: true,
  configurable: true,
  get() {
    console.log('price属性被读取了');
    return val;
  },
  set(newVal) {
    console.log('price属性被修改了');
    val = newVal;
  },
});
```

通过`Object.defineProperty() `方法给`car`定义了一个`price`属性，并把这个属性的读和写分别使用`get()`和`set()`进行拦截，每当该属性进行读或写操作的时候就会触发`get()`和`set()`。如下图：

![](~@/learn-vue-source-code/reactive/1.png)

可以看到，`car`已经可以主动告诉我们它的属性的读写情况了，这也意味着，这个`car`的数据对象已经是“可观测”的了。

为了把`car`的所有属性都变得可观测，我们可以编写如下代码：

```javascript
// 源码位置：src/core/observer/index.js

/**
 * Observer类会通过递归的方式把一个对象的所有属性都转化成可观测对象
 */
export class Observer {
  constructor(value) {
    this.value = value;
    // 给value新增一个__ob__属性，值为该value的Observer实例
    // 相当于为value打上标记，表示它已经被转化成响应式了，避免重复操作
    def(value, '__ob__', this);
    if (Array.isArray(value)) {
      // 当value为数组时的逻辑
      // ...
    } else {
      this.walk(value);
    }
  }

  walk(obj: Object) {
    const keys = Object.keys(obj);
    for (let i = 0; i < keys.length; i++) {
      defineReactive(obj, keys[i]);
    }
  }
}
/**
 * 使一个对象转化成可观测对象
 * @param { Object } obj 对象
 * @param { String } key 对象的key
 * @param { Any } val 对象的某个key的值
 */
function defineReactive(obj, key, val) {
  // 如果只传了obj和key，那么val = obj[key]
  if (arguments.length === 2) {
    val = obj[key];
  }
  if (typeof val === 'object') {
    new Observer(val);
  }
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get() {
      console.log(`${key}属性被读取了`);
      return val;
    },
    set(newVal) {
      if (val === newVal) {
        return;
      }
      console.log(`${key}属性被修改了`);
      val = newVal;
    },
  });
}
```

在上面的代码中，我们定义了`observer`类，它用来将一个正常的`object`转换成可观测的`object`。

并且给`value`新增一个`__ob__`属性，值为该`value`的`Observer`实例。这个操作相当于为`value`打上标记，表示它已经被转化成响应式了，避免重复操作。

然后判断数据的类型，只有`object`类型的数据才会调用`walk`将每一个属性转换成`getter/setter`的形式来侦测变化。
最后，在`defineReactive`中当传入的属性值还是一个`object`时使用` new observer（val）`来递归子属性，这样我们就可以把`obj`中的所有属性（包括子属性）都转换成`getter/seter`的形式来侦测变化。
也就是说，只要我们将一个`object`传到`observer`中，那么这个`object`就会变成可观测的、响应式的`object`。

`observer`类位于源码的`src/core/observer/index.js`中。

那么现在，我们就可以这样定义`car`:

```javascript
let car = new Observer({
  brand: 'BMW',
  price: 3000,
});
```

这样，`car`的两个属性都变得可观测了。

### 依赖收集

#### 1 什么是依赖收集

在上一章中，我们迈出了第一步：让`object`数据变的可观测。变的可观测以后，我们就能知道数据什么时候发生了变化，那么当数据发生变化时，我们去通知视图更新就好了。那么问题又来了，视图那么大，我们到底该通知谁去变化？总不能一个数据变化了，把整个视图全部更新一遍吧，这样显然是不合理的。此时，你肯定会想到，视图里谁用到了这个数据就更新谁呗。对！你想的没错，就是这样。

视图里谁用到了这个数据就更新谁，我们换个优雅说法：我们把"谁用到了这个数据"称为"谁依赖了这个数据",我们给每个数据都建一个依赖数组（因为一个数据可能被多处使用），谁依赖了这个数据（即谁用到了这个数据）我们就把谁放入这个依赖数组中，那么当这个数据发生变化的时候，我们就去它对应的依赖数组中，把每个依赖都通知一遍，告诉他们："你们依赖的数据变啦，你们该更新啦！"。这个过程就是依赖收集。

#### 2 何时收集依赖？何时通知依赖更新？

明白了什么是依赖收集后，那么我们到底该在何时收集依赖？又该在何时通知依赖更新？

其实这个问题在上一小节中已经回答了，我们说过：谁用到了这个数据，那么当这个数据变化时就通知谁。所谓谁用到了这个数据，其实就是谁获取了这个数据，而可观测的数据被获取时会触发`getter`属性，那么我们就可以在`getter`中收集这个依赖。同样，当这个数据变化时会触发`setter`属性，那么我们就可以在`setter`中通知依赖更新。

总结一句话就是：**在 getter 中收集依赖，在 setter 中通知依赖更新**。

#### 3 把依赖收集到哪里

明白了什么是依赖收集以及何时收集何时通知后，那么我们该把依赖收集到哪里？

在 3.1 小节中也说了，我们给每个数据都建一个依赖数组，谁依赖了这个数据我们就把谁放入这个依赖数组中。单单用一个数组来存放依赖的话，功能好像有点欠缺并且代码过于耦合。我们应该将依赖数组的功能扩展一下，更好的做法是我们应该为每一个数据都建立一个依赖管理器，把这个数据所有的依赖都管理起来。OK，到这里，我们的依赖管理器`Dep`类应运而生，代码如下：

```javascript
// 源码位置：src/core/observer/dep.js
export default class Dep {
  constructor() {
    this.subs = [];
  }

  addSub(sub) {
    this.subs.push(sub);
  }
  // 删除一个依赖
  removeSub(sub) {
    remove(this.subs, sub);
  }
  // 添加一个依赖
  depend() {
    if (window.target) {
      this.addSub(window.target);
    }
  }
  // 通知所有依赖更新
  notify() {
    const subs = this.subs.slice();
    for (let i = 0, l = subs.length; i < l; i++) {
      subs[i].update();
    }
  }
}

/**
 * Remove an item from an array
 */
export function remove(arr, item) {
  if (arr.length) {
    const index = arr.indexOf(item);
    if (index > -1) {
      return arr.splice(index, 1);
    }
  }
}
```

在上面的依赖管理器`Dep`类中，我们先初始化了一个`subs`数组，用来存放依赖，并且定义了几个实例方法用来对依赖进行添加，删除，通知等操作。

有了依赖管理器后，我们就可以在 getter 中收集依赖，在 setter 中通知依赖更新了，代码如下：

```javascript
function defineReactive(obj, key, val) {
  if (arguments.length === 2) {
    val = obj[key];
  }
  if (typeof val === 'object') {
    new Observer(val);
  }
  const dep = new Dep(); //实例化一个依赖管理器，生成一个依赖管理数组dep
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get() {
      dep.depend(); // 在getter中收集依赖
      return val;
    },
    set(newVal) {
      if (val === newVal) {
        return;
      }
      val = newVal;
      dep.notify(); // 在setter中通知依赖更新
    },
  });
}
```

在上述代码中，我们在`getter`中调用了`dep.depend()`方法收集依赖，在`setter`中调用`dep.notify()`方法通知所有依赖更新。

### 依赖到底是谁

通过上一章节，我们明白了什么是依赖？何时收集依赖？以及收集的依赖存放到何处？那么我们收集的依赖到底是谁？

虽然我们一直在说”谁用到了这个数据谁就是依赖“，但是这仅仅是在口语层面上，那么反应在代码上该如何来描述这个”谁“呢？

其实在`Vue`中还实现了一个叫做`Watcher`的类，而`Watcher`类的实例就是我们上面所说的那个"谁"。换句话说就是：谁用到了数据，谁就是依赖，我们就为谁创建一个`Watcher`实例。在之后数据变化时，我们不直接去通知依赖更新，而是通知依赖对应的`Watch`实例，由`Watcher`实例去通知真正的视图。

`Watcher`类的具体实现如下：

```javascript
export default class Watcher {
  constructor(vm, expOrFn, cb) {
    this.vm = vm;
    this.cb = cb;
    this.getter = parsePath(expOrFn);
    this.value = this.get();
  }
  get() {
    window.target = this;
    const vm = this.vm;
    let value = this.getter.call(vm, vm);
    window.target = undefined;
    return value;
  }
  update() {
    const oldValue = this.value;
    this.value = this.get();
    this.cb.call(this.vm, this.value, oldValue);
  }
}

/**
 * Parse simple path.
 * 把一个形如'data.a.b.c'的字符串路径所表示的值，从真实的data对象中取出来
 * 例如：
 * data = {a:{b:{c:2}}}
 * parsePath('a.b.c')(data)  // 2
 */
const bailRE = /[^\w.$]/;
export function parsePath(path) {
  if (bailRE.test(path)) {
    return;
  }
  const segments = path.split('.');
  return function (obj) {
    for (let i = 0; i < segments.length; i++) {
      if (!obj) return;
      obj = obj[segments[i]];
    }
    return obj;
  };
}
```

谁用到了数据，谁就是依赖，我们就为谁创建一个`Watcher`实例，在创建`Watcher`实例的过程中会自动的把自己添加到这个数据对应的依赖管理器中，以后这个`Watcher`实例就代表这个依赖，当数据变化时，我们就通知`Watcher`实例，由`Watcher`实例再去通知真正的依赖。

那么，在创建`Watcher`实例的过程中它是如何的把自己添加到这个数据对应的依赖管理器中呢？

下面我们分析`Watcher`类的代码实现逻辑：

1. 当实例化`Watcher`类时，会先执行其构造函数；
2. 在构造函数中调用了`this.get()`实例方法；
3. 在`get()`方法中，首先通过`window.target = this`把实例自身赋给了全局的一个唯一对象`window.target`上，然后通过`let value = this.getter.call(vm, vm)`获取一下被依赖的数据，获取被依赖数据的目的是触发该数据上面的`getter`，上文我们说过，在`getter`里会调用`dep.depend()`收集依赖，而在`dep.depend()`中取到挂载`window.target`上的值并将其存入依赖数组中，在`get()`方法最后将`window.target`释放掉。
4. 而当数据变化时，会触发数据的`setter`，在`setter`中调用了`dep.notify()`方法，在`dep.notify()`方法中，遍历所有依赖（即 watcher 实例），执行依赖的`update()`方法，也就是`Watcher`类中的`update()`实例方法，在`update()`方法中调用数据变化的更新回调函数，从而更新视图。

简单总结一下就是：`Watcher`先把自己设置到全局唯一的指定位置（`window.target`），然后读取数据。因为读取了数据，所以会触发这个数据的`getter`。接着，在`getter`中就会从全局唯一的那个位置读取当前正在读取数据的`Watcher`，并把这个`watcher`收集到`Dep`中去。收集好之后，当数据发生变化时，会向`Dep`中的每个`Watcher`发送通知。通过这样的方式，`Watcher `可以主动去订阅任意一个数据的变化。为了便于理解，我们画出了其关系流程图，如下图：

![](~@/learn-vue-source-code/reactive/3.jpg)

以上，就彻底完成了对`Object`数据的侦测，依赖收集，依赖的更新等所有操作。

### 不足之处

虽然我们通过`Object.defineProperty`方法实现了对`object`数据的可观测，但是这个方法仅仅只能观测到`object`数据的取值及设置值，当我们向`object`数据里添加一对新的`key/value`或删除一对已有的`key/value`时，它是无法观测到的，导致当我们对`object`数据添加或删除值时，无法通知依赖，无法驱动视图进行响应式更新。

当然，`Vue`也注意到了这一点，为了解决这一问题，`Vue`增加了两个全局 API:`Vue.set`和`Vue.delete`，这两个 API 的实现原理将会在后面学习全局 API 的时候说到。

### 总结

首先，我们通过`Object.defineProperty`方法实现了对`object`数据的可观测，并且封装了`Observer`类，让我们能够方便的把`object`数据中的所有属性（包括子属性）都转换成`getter/seter`的形式来侦测变化。

接着，我们学习了什么是依赖收集？并且知道了在`getter`中收集依赖，在`setter`中通知依赖更新，以及封装了依赖管理器`Dep`，用于存储收集到的依赖。

最后，我们为每一个依赖都创建了一个`Watcher`实例，当数据发生变化时，通知`Watcher`实例，由`Watcher`实例去做真实的更新操作。

其整个流程大致如下：

1. `Data`通过`observer`转换成了`getter/setter`的形式来追踪变化。
2. 当外界通过`Watcher`读取数据时，会触发`getter`从而将`Watcher`添加到依赖中。
3. 当数据发生了变化时，会触发`setter`，从而向`Dep`中的依赖（即 Watcher）发送通知。
4. `Watcher`接收到通知后，会向外界发送通知，变化通知到外界后可能会触发视图更新，也有可能触发用户的某个回调函数等。

## 2.3 Array 的变化侦测

### 前言

上一篇文章中我们介绍了`Object`数据的变化侦测方式，本篇文章我们来看一下对`Array`型数据的变化`Vue`是如何进行侦测的。

为什么`Object`数据和`Array`型数据会有两种不同的变化侦测方式？

这是因为对于`Object`数据我们使用的是`JS`提供的对象原型上的方法`Object.defineProperty`，而这个方法是对象原型上的，所以`Array`无法使用这个方法，所以我们需要对`Array`型数据设计一套另外的变化侦测机制。

万变不离其宗，虽然对`Array`型数据设计了新的变化侦测机制，但是其根本思路还是不变的。那就是：还是在获取数据时收集依赖，数据变化时通知依赖更新。

下面我们就通过源码来看看`Vue`对`Array`型数据到底是如何进行变化侦测的。

### 在哪里收集依赖

首先还是老规矩，我们得先把用到`Array`型数据的地方作为依赖收集起来，那么第一问题就是该在哪里收集呢？

其实`Array`型数据的依赖收集方式和`Object`数据的依赖收集方式相同，都是在`getter`中收集。那么问题就来了，不是说`Array`无法使用`Object.defineProperty`方法吗？无法使用怎么还在`getter`中收集依赖呢？

其实不然，我们回想一下平常在开发的时候，在组件的`data`中是不是都这么写的：

```javascript
data(){
  return {
    arr:[1,2,3]
  }
}
```

想想看，`arr`这个数据始终都存在于一个`object`数据对象中，而且我们也说了，谁用到了数据谁就是依赖，那么要用到`arr`这个数据，是不是得先从`object`数据对象中获取一下`arr`数据，而从`object`数据对象中获取`arr`数据自然就会触发`arr`的`getter`，所以我们就可以在`getter`中收集依赖。

总结一句话就是：**Array 型数据还是在 getter 中收集依赖。**

### 使 Array 型数据可观测

上一章节中我们知道了`Array`型数据还是在`getter`中收集依赖，换句话说就是我们已经知道了`Array`型数据何时被读取了。

回想上一篇文章中介绍`Object`数据变化侦测的时候，我们先让`Object`数据变的可观测，即我们能够知道数据什么时候被读取了、什么时候发生变化了。同理，对于`Array`型数据我们也得让它变的可观测，目前我们已经完成了一半可观测，即我们只知道了`Array`型数据何时被读取了，而何时发生变化我们无法知道，那么接下来我们就来解决这一问题：当`Array`型数据发生变化时我们如何得知？

#### 思路分析

`Object`的变化时通过`setter`来追踪的，只有某个数据发生了变化，就一定会触发这个数据上的`setter`。但是`Array`型数据没有`setter`，怎么办？

我们试想一下，要想让`Array`型数据发生变化，那必然是操作了`Array`，而`JS`中提供的操作数组的方法就那么几种，我们可以把这些方法都重写一遍，在不改变原有功能的前提下，我们为其新增一些其他功能，例如下面这个例子：

```javascript
let arr = [1, 2, 3];
arr.push(4);
Array.prototype.newPush = function (val) {
  console.log('arr被修改了');
  this.push(val);
};
arr.newPush(4);
```

在上面这个例子中，我们针对数组的原生`push`方法定义个一个新的`newPush`方法，这个`newPush`方法内部调用了原生`push`方法，这样就保证了新的`newPush`方法跟原生`push`方法具有相同的功能，而且我们还可以在新的`newPush`方法内部干一些别的事情，比如通知变化。

是不是很巧妙？`Vue`内部就是这么干的。

#### 数组方法拦截器

基于上一小节的思想，在`Vue`中创建了一个数组方法拦截器，它拦截在数组实例与`Array.prototype`之间，在拦截器内重写了操作数组的一些方法，当数组实例使用操作数组方法时，其实使用的是拦截器中重写的方法，而不再使用`Array.prototype`上的原生方法。如下图所示：

![](~@/learn-vue-source-code/reactive/2.png)

经过整理，`Array`原型中可以改变数组自身内容的方法有 7 个，分别是：`push`,`pop`,`shift`,`unshift`,`splice`,`sort`,`reverse`。那么源码中的拦截器代码如下：

```javascript
// 源码位置：/src/core/observer/array.js

const arrayProto = Array.prototype;
// 创建一个对象作为拦截器
export const arrayMethods = Object.create(arrayProto);

// 改变数组自身内容的7个方法
const methodsToPatch = [
  'push',
  'pop',
  'shift',
  'unshift',
  'splice',
  'sort',
  'reverse',
];

/**
 * Intercept mutating methods and emit events
 */
methodsToPatch.forEach(function (method) {
  const original = arrayProto[method]; // 缓存原生方法
  Object.defineProperty(arrayMethods, method, {
    enumerable: false,
    configurable: true,
    writable: true,
    value: function mutator(...args) {
      const result = original.apply(this, args);
      return result;
    },
  });
});
```

在上面的代码中，首先创建了继承自`Array`原型的空对象`arrayMethods`，接着在`arrayMethods`上使用`object.defineProperty`方法将那些可以改变数组自身的 7 个方法遍历逐个进行封装。最后，当我们使用`push`方法的时候，其实用的是`arrayMethods.push`，而`arrayMethods.push`就是封装的新函数`mutator`，也就后说，实标上执行的是函数`mutator`，而`mutator`函数内部执行了`original`函数，这个`original`函数就是`Array.prototype`上对应的原生方法。
那么，接下来我们就可以在`mutato`r 函数中做一些其他的事，比如说发送变化通知。

#### 使用拦截器

在上一小节的图中，我们把拦截器做好还不够，还要把它挂载到数组实例与`Array.prototype`之间，这样拦截器才能够生效。

其实挂载不难，我们只需把数据的`__proto__`属性设置为拦截器`arrayMethods`即可，源码实现如下：

```javascript
// 源码位置：/src/core/observer/index.js
export class Observer {
  constructor(value) {
    this.value = value;
    if (Array.isArray(value)) {
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
    } else {
      this.walk(value);
    }
  }
}
// 能力检测：判断__proto__是否可用，因为有的浏览器不支持该属性
export const hasProto = '__proto__' in {};

const arrayKeys = Object.getOwnPropertyNames(arrayMethods);

/**
 * Augment an target Object or Array by intercepting
 * the prototype chain using __proto__
 */
function protoAugment(target, src: Object, keys: any) {
  target.__proto__ = src;
}

/**
 * Augment an target Object or Array by defining
 * hidden properties.
 */
/* istanbul ignore next */
function copyAugment(target: Object, src: Object, keys: Array<string>) {
  for (let i = 0, l = keys.length; i < l; i++) {
    const key = keys[i];
    def(target, key, src[key]);
  }
}
```

上面代码中首先判断了浏览器是否支持`__proto__`，如果支持，则调用`protoAugment`函数把`value.__proto__ = arrayMethods`；如果不支持，则调用`copyAugment`函数把拦截器中重写的 7 个方法循环加入到`value`上。

拦截器生效以后，当数组数据再发生变化时，我们就可以在拦截器中通知变化了，也就是说现在我们就可以知道数组数据何时发生变化了，OK，以上我们就完成了对`Array`型数据的可观测。

### 再谈依赖收集

#### 把依赖收集到哪里

在第二章中我们说了，数组数据的依赖也在`getter`中收集，而给数组数据添加`getter/setter`都是在`Observer`类中完成的，所以我们也应该在`Observer`类中收集依赖，源码如下：

```javascript
// 源码位置：/src/core/observer/index.js
export class Observer {
  constructor(value) {
    this.value = value;
    this.dep = new Dep(); // 实例化一个依赖管理器，用来收集数组依赖
    if (Array.isArray(value)) {
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
    } else {
      this.walk(value);
    }
  }
}
```

上面代码中，在`Observer`类中实例化了一个依赖管理器，用来收集数组依赖。

#### 如何收集依赖

在第二章中我们说了，数组的依赖也在`getter`中收集，那么在`getter`中到底该如何收集呢？这里有一个需要注意的点，那就是依赖管理器定义在`Observer`类中，而我们需要在`getter`中收集依赖，也就是说我们必须在`getter`中能够访问到`Observer`类中的依赖管理器，才能把依赖存进去。源码是这么做的：

```javascript
function defineReactive(obj, key, val) {
  let childOb = observe(val);
  Object.defineProperty(obj, key, {
    enumerable: true,
    configurable: true,
    get() {
      if (childOb) {
        childOb.dep.depend();
      }
      return val;
    },
    set(newVal) {
      if (val === newVal) {
        return;
      }
      val = newVal;
      dep.notify(); // 在setter中通知依赖更新
    },
  });
}

/**
 * Attempt to create an observer instance for a value,
 * returns the new observer if successfully observed,
 * or the existing observer if the value already has one.
 * 尝试为value创建一个0bserver实例，如果创建成功，直接返回新创建的Observer实例。
 * 如果 Value 已经存在一个Observer实例，则直接返回它
 */
export function observe(value, asRootData) {
  if (!isObject(value) || value instanceof VNode) {
    return;
  }
  let ob;
  if (hasOwn(value, '__ob__') && value.__ob__ instanceof Observer) {
    ob = value.__ob__;
  } else {
    ob = new Observer(value);
  }
  return ob;
}
```

在上面代码中，我们首先通过`observe`函数为被获取的数据`arr`尝试创建一个`Observer`实例，在`observe`函数内部，先判断当前传入的数据上是否有`__ob__`属性，因为在上篇文章中说了，如果数据有`__ob__`属性，表示它已经被转化成响应式的了，如果没有则表示该数据还不是响应式的，那么就调用`new Observer(value)`将其转化成响应式的，并把数据对应的`Observer`实例返回。

而在`defineReactive`函数中，首先获取数据对应的`Observer`实例`childOb`，然后在`getter`中调用`Observer`实例上依赖管理器，从而将依赖收集起来。

#### 如何通知依赖

到现在为止，依赖已经收集好了，并且也已经存放好了，那么我们该如何通知依赖呢？

其实不难，在前文说过，我们应该在拦截器里通知依赖，要想通知依赖，首先要能访问到依赖。要访问到依赖也不难，因为我们只要能访问到被转化成响应式的数据`value`即可，因为`vaule`上的`__ob__`就是其对应的`Observer`类实例，有了`Observer`类实例我们就能访问到它上面的依赖管理器，然后只需调用依赖管理器的`dep.notify()`方法，让它去通知依赖更新即可。源码如下：

```javascript
/**
 * Intercept mutating methods and emit events
 */
methodsToPatch.forEach(function (method) {
  const original = arrayProto[method];
  def(arrayMethods, method, function mutator(...args) {
    const result = original.apply(this, args);
    const ob = this.__ob__;
    // notify change
    ob.dep.notify();
    return result;
  });
});
```

上面代码中，由于我们的拦截器是挂载到数组数据的原型上的，所以拦截器中的`this`就是数据`value`，拿到`value`上的`Observer`类实例，从而你就可以调用`Observer`类实例上面依赖管理器的`dep.notify()`方法，以达到通知依赖的目的。

OK，以上就基本完成了`Array`数据的变化侦测。

### 深度侦测

在前文所有讲的`Array`型数据的变化侦测都仅仅说的是数组自身变化的侦测，比如给数组新增一个元素或删除数组中一个元素，而在`Vue`中，不论是`Object`型数据还是`Array`型数据所实现的数据变化侦测都是深度侦测，所谓深度侦测就是不但要侦测数据自身的变化，还要侦测数据中所有子数据的变化。举个例子：

```javascript
let arr = [
  {
    name:'NLRX'，
    age:'18'
  }
]
```

数组中包含了一个对象，如果该对象的某个属性发生了变化也应该被侦测到，这就是深度侦测。

这个实现起来比较简单，源码如下：

```javascript
export class Observer {
  value: any;
  dep: Dep;

  constructor(value: any) {
    this.value = value;
    this.dep = new Dep();
    def(value, '__ob__', this);
    if (Array.isArray(value)) {
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
      this.observeArray(value); // 将数组中的所有元素都转化为可被侦测的响应式
    } else {
      this.walk(value);
    }
  }

  /**
   * Observe a list of Array items.
   */
  observeArray(items: Array<any>) {
    for (let i = 0, l = items.length; i < l; i++) {
      observe(items[i]);
    }
  }
}

export function observe(value, asRootData) {
  if (!isObject(value) || value instanceof VNode) {
    return;
  }
  let ob;
  if (hasOwn(value, '__ob__') && value.__ob__ instanceof Observer) {
    ob = value.__ob__;
  } else {
    ob = new Observer(value);
  }
  return ob;
}
```

在上面代码中，对于`Array`型数据，调用了`observeArray()`方法，该方法内部会遍历数组中的每一个元素，然后通过调用`observe`函数将每一个元素都转化成可侦测的响应式数据。

而对应`object`数据，在上一篇文章中我们已经在`defineReactive`函数中进行了递归操作。

### 数组新增元素的侦测

对于数组中已有的元素我们已经可以将其全部转化成可侦测的响应式数据了，但是如果向数组里新增一个元素的话，我们也需要将新增的这个元素转化成可侦测的响应式数据。

这个实现起来也很容易，我们只需拿到新增的这个元素，然后调用`observe`函数将其转化即可。我们知道，可以向数组内新增元素的方法有 3 个，分别是：`push`、`unshift`、`splice`。我们只需对这 3 中方法分别处理，拿到新增的元素，再将其转化即可。源码如下：

```javascript
/**
 * Intercept mutating methods and emit events
 */
methodsToPatch.forEach(function (method) {
  // cache original method
  const original = arrayProto[method];
  def(arrayMethods, method, function mutator(...args) {
    const result = original.apply(this, args);
    const ob = this.__ob__;
    let inserted;
    switch (method) {
      case 'push':
      case 'unshift':
        inserted = args; // 如果是push或unshift方法，那么传入参数就是新增的元素
        break;
      case 'splice':
        inserted = args.slice(2); // 如果是splice方法，那么传入参数列表中下标为2的就是新增的元素
        break;
    }
    if (inserted) ob.observeArray(inserted); // 调用observe函数将新增的元素转化成响应式
    // notify change
    ob.dep.notify();
    return result;
  });
});
```

在上面拦截器定义代码中，如果是`push`或`unshift`方法，那么传入参数就是新增的元素；如果是`splice`方法，那么传入参数列表中下标为 2 的就是新增的元素，拿到新增的元素后，就可以调用`observe`函数将新增的元素转化成响应式的了。

### 不足之处

前文中我们说过，对于数组变化侦测是通过拦截器实现的，也就是说只要是通过数组原型上的方法对数组进行操作就都可以侦测到，但是别忘了，我们在日常开发中，还可以通过数组的下标来操作数据，如下：

```javascript
let arr = [1, 2, 3];
arr[0] = 5; // 通过数组下标修改数组中的数据
arr.length = 0; // 通过修改数组长度清空数组
```

而使用上述例子中的操作方式来修改数组是无法侦测到的。
同样，`Vue`也注意到了这个问题， 为了解决这一问题，`Vue`增加了两个全局 API:`Vue.set`和`Vue.delete`，这两个 API 的实现原理将会在后面学习全局 API 的时候说到。

### 总结

在本篇文章中，首先我们分析了对于`Array`型数据也在`getter`中进行依赖收集；其次我们发现，当数组数据被访问时我们轻而易举可以知道，但是被修改时我们却很难知道，为了解决这一问题，我们创建了数组方法拦截器，从而成功的将数组数据变的可观测。接着我们对数组的依赖收集及数据变化如何通知依赖进行了深入分析；最后我们发现`Vue`不但对数组自身进行了变化侦测，还对数组中的每一个元素以及新增的元素都进行了变化侦测，我们也分析了其实现原理。

以上就是对`Array`型数据的变化侦测分析。

# 3. 虚拟 DOM 篇

## 3.1 Vue 中的虚拟 DOM

### 前言

虚拟DOM，这个名词作为当下的前端开发人员你一定不会陌生，至少会略有耳闻，但不会闻所未闻吧。这也是现在求职面试考察中非常高频的一个考点了。因为在当下的前端三大框架中关于虚拟DOM或多或少都有所涉及，那么接下来，我们就从源码角度出发，看看`Vue`中的虚拟DOM时怎样的。

### 虚拟DOM简介

由于本系列文章是针对`Vue`源码深入学习的，所以着重分析在`Vue`中对虚拟DOM是如何实现的，而对于虚拟DOM本身这个概念不做大篇幅的展开讨论，仅从以下几个问题简单介绍：

1. 什么是虚拟DOM？

   所谓虚拟DOM，就是用一个`JS`对象来描述一个`DOM`节点，像如下示例：

   ```javascript
   <div class="a" id="b">我是内容</div>

   {
     tag:'div',        // 元素标签
     attrs:{           // 属性
       class:'a',
       id:'b'
     },
     text:'我是内容',  // 文本内容
     children:[]       // 子元素
   }
   ```

   我们把组成一个`DOM`节点的必要东西通过一个`JS`对象表示出来，那么这个`JS`对象就可以用来描述这个`DOM`节点，我们把这个`JS`对象就称为是这个真实`DOM`节点的虚拟`DOM`节点。

2. 为什么要有虚拟DOM？

    我们知道，`Vue`是数据驱动视图的，数据发生变化视图就要随之更新，在更新视图的时候难免要操作`DOM`,而操作真实`DOM`又是非常耗费性能的，这是因为浏览器的标准就把 `DOM` 设计的非常复杂，所以一个真正的 `DOM` 元素是非常庞大的，如下所示：

   ```javascript
   let div = document.createElement('div')
   let str = ''
   for (const key in div) {
     str += key + ''
   }
   console.log(str)
   ```

  ![真实DOM元素](~@/learn-vue-source-code/virtualDOM/1.png)

   上图中我们打印一个简单的空 `div` 标签，就打印出这么多东西，更不用说复杂的、深嵌套的 `DOM` 节点了。由此可见，真实的 `DOM` 节点数据会占据更大的内存，当我们频繁的去做 `DOM` 更新，会产生一定的性能问题，因为 `DOM` 的更新有可能带来页面的重绘或重排。

   那么有没有什么解决方案呢？当然是有的。我们可以用 `JS` 的计算性能来换取操作 `DOM` 所消耗的性能。

   既然我们逃不掉操作`DOM`这道坎,但是我们可以尽可能少的操作 `DOM` 。那如何在更新视图的时候尽可能少的操作 `DOM` 呢？最直观的思路就是我们不要盲目的去更新视图，而是通过对比数据变化前后的状态，计算出视图中哪些地方需要更新，只更新需要更新的地方，而不需要更新的地方则不需关心，这样我们就可以尽可能少的操作 `DOM` 了。这也就是上面所说的用 `JS` 的计算性能来换取操作 `DOM` 的性能。

   我们可以用 `JS` 模拟出一个 `DOM` 节点，称之为虚拟 `DOM` 节点。当数据发生变化时，我们对比变化前后的虚拟`DOM`节点，通过`DOM-Diff`算法计算出需要更新的地方，然后去更新需要更新的视图。

   这就是虚拟 `DOM` 产生的原因以及最大的用途。

   另外，使用虚拟 `DOM` 也能使得 `Vue` 不再依赖于浏览器环境。我们可以很容易的在 `Broswer` 端或者服务器端操作虚拟 `DOM`, 需要 `render` 时再将虚拟 `DOM` 转换为真实 `DOM` 即可。这也使得 `Vue` 有了实现服务器端渲染的能力。

### Vue中的虚拟DOM

前文我们介绍了虚拟`DOM`的概念以及为什么要有虚拟`DOM`，那么在`Vue`中虚拟`DOM`是怎么实现的呢？接下来，我们从源码出发，深入学习一下。

####  VNode类

我们说了，虚拟`DOM`就是用`JS`来描述一个真实的`DOM`节点。而在`Vue`中就存在了一个`VNode`类，通过这个类，我们就可以实例化出不同类型的虚拟`DOM`节点，源码如下：

```javascript
// 源码位置：src/core/vdom/vnode.js

export default class VNode {
  constructor (
    tag?: string,
    data?: VNodeData,
    children?: ?Array<VNode>,
    text?: string,
    elm?: Node,
    context?: Component,
    componentOptions?: VNodeComponentOptions,
    asyncFactory?: Function
  ) {
    this.tag = tag                                /*当前节点的标签名*/
    this.data = data        /*当前节点对应的对象，包含了具体的一些数据信息，是一个VNodeData类型，可以参考VNodeData类型中的数据信息*/
    this.children = children  /*当前节点的子节点，是一个数组*/
    this.text = text     /*当前节点的文本*/
    this.elm = elm       /*当前虚拟节点对应的真实dom节点*/
    this.ns = undefined            /*当前节点的名字空间*/
    this.context = context          /*当前组件节点对应的Vue实例*/
    this.fnContext = undefined       /*函数式组件对应的Vue实例*/
    this.fnOptions = undefined
    this.fnScopeId = undefined
    this.key = data && data.key           /*节点的key属性，被当作节点的标志，用以优化*/
    this.componentOptions = componentOptions   /*组件的option选项*/
    this.componentInstance = undefined       /*当前节点对应的组件的实例*/
    this.parent = undefined           /*当前节点的父节点*/
    this.raw = false         /*简而言之就是是否为原生HTML或只是普通文本，innerHTML的时候为true，textContent的时候为false*/
    this.isStatic = false         /*静态节点标志*/
    this.isRootInsert = true      /*是否作为跟节点插入*/
    this.isComment = false             /*是否为注释节点*/
    this.isCloned = false           /*是否为克隆节点*/
    this.isOnce = false                /*是否有v-once指令*/
    this.asyncFactory = asyncFactory
    this.asyncMeta = undefined
    this.isAsyncPlaceholder = false
  }

  get child (): Component | void {
    return this.componentInstance
  }
}
```

从上面的代码中可以看出：`VNode`类中包含了描述一个真实`DOM`节点所需要的一系列属性，如`tag`表示节点的标签名，`text`表示节点中包含的文本，`children`表示该节点包含的子节点等。通过属性之间不同的搭配，就可以描述出各种类型的真实`DOM`节点。

####  VNode的类型

上一小节最后我们说了，通过属性之间不同的搭配，`VNode`类可以描述出各种类型的真实`DOM`节点。那么它都可以描述出哪些类型的节点呢？通过阅读源码，可以发现通过不同属性的搭配，可以描述出以下几种类型的节点。

- 注释节点
- 文本节点
- 元素节点
- 组件节点
- 函数式组件节点
- 克隆节点

接下来，我们就把这几种类型的节点描述方式从源码中一一对应起来。

##### .1 注释节点

注释节点描述起来相对就非常简单了，它只需两个属性就够了，源码如下：

```javascript
// 创建注释节点
export const createEmptyVNode = (text: string = '') => {
  const node = new VNode()
  node.text = text
  node.isComment = true
  return node
}
```

从上面代码中可以看到，描述一个注释节点只需两个属性，分别是：`text`和`isComment`。其中`text`属性表示具体的注释信息，`isComment`是一个标志，用来标识一个节点是否是注释节点。

##### .2 文本节点

文本节点描述起来比注释节点更简单，因为它只需要一个属性，那就是`text`属性，用来表示具体的文本信息。源码如下：

```javascript
// 创建文本节点
export function createTextVNode (val: string | number) {
  return new VNode(undefined, undefined, undefined, String(val))
}
```

##### .3 克隆节点

克隆节点就是把一个已经存在的节点复制一份出来，它主要是为了做模板编译优化时使用，这个后面我们会说到。关于克隆节点的描述，源码如下：

```javascript
// 创建克隆节点
export function cloneVNode (vnode: VNode): VNode {
  const cloned = new VNode(
    vnode.tag,
    vnode.data,
    vnode.children,
    vnode.text,
    vnode.elm,
    vnode.context,
    vnode.componentOptions,
    vnode.asyncFactory
  )
  cloned.ns = vnode.ns
  cloned.isStatic = vnode.isStatic
  cloned.key = vnode.key
  cloned.isComment = vnode.isComment
  cloned.fnContext = vnode.fnContext
  cloned.fnOptions = vnode.fnOptions
  cloned.fnScopeId = vnode.fnScopeId
  cloned.asyncMeta = vnode.asyncMeta
  cloned.isCloned = true
  return cloned
}
```

从上面代码中可以看到，克隆节点就是把已有节点的属性全部复制到新节点中，而现有节点和新克隆得到的节点之间唯一的不同就是克隆得到的节点`isCloned`为`true`。

##### .4 元素节点

相比之下，元素节点更贴近于我们通常看到的真实`DOM`节点，它有描述节点标签名词的`tag`属性，描述节点属性如`class`、`attributes`等的`data`属性，有描述包含的子节点信息的`children`属性等。由于元素节点所包含的情况相比而言比较复杂，源码中没有像前三种节点一样直接写死（当然也不可能写死），那就举个简单例子说明一下：

```javascript
// 真实DOM节点
<div id='a'><span>难凉热血</span></div>

// VNode节点
{
  tag:'div',
  data:{},
  children:[
    {
      tag:'span',
      text:'难凉热血'
    }
  ]
}
```

我们可以看到，真实`DOM`节点中:`div`标签里面包含了一个`span`标签，而`span`标签里面有一段文本。反应到`VNode`节点上就如上所示:`tag`表示标签名，`data`表示标签的属性`id`等，`children`表示子节点数组。

##### .5 组件节点

组件节点除了有元素节点具有的属性之外，它还有两个特有的属性：

- componentOptions :组件的option选项，如组件的`props`等
- componentInstance :当前组件节点对应的`Vue`实例

##### .6 函数式组件节点

函数式组件节点相较于组件节点，它又有两个特有的属性：

- fnContext:函数式组件对应的Vue实例
- fnOptions: 组件的option选项

##### .7 小结

以上就是`VNode`可以描述的多种节点类型，它们本质上都是`VNode`类的实例，只是在实例化的时候传入的属性参数不同而已。

####  VNode的作用

说了这么多，那么`VNode`在`Vue`的整个虚拟`DOM`过程起了什么作用呢？

其实`VNode`的作用是相当大的。我们在视图渲染之前，把写好的`template`模板先编译成`VNode`并缓存下来，等到数据发生变化页面需要重新渲染的时候，我们把数据发生变化后生成的`VNode`与前一次缓存下来的`VNode`进行对比，找出差异，然后有差异的`VNode`对应的真实`DOM`节点就是需要重新渲染的节点，最后根据有差异的`VNode`创建出真实的`DOM`节点再插入到视图中，最终完成一次视图更新。

### 总结

本章首先介绍了虚拟`DOM`的一些基本概念和为什么要有虚拟`DOM`，其实说白了就是以`JS`的计算性能来换取操作真实`DOM`所消耗的性能。接着从源码角度我们知道了在`Vue`中是通过`VNode`类来实例化出不同类型的虚拟`DOM`节点，并且学习了不同类型节点生成的属性的不同，所谓不同类型的节点其本质还是一样的，都是`VNode`类的实例，只是在实例化时传入的属性参数不同罢了。最后探究了`VNode`的作用，有了数据变化前后的`VNode`，我们才能进行后续的`DOM-Diff`找出差异，最终做到只更新有差异的视图，从而达到尽可能少的操作真实`DOM`的目的，以节省性能。

## 3.2 Vue 中的 DOM-Diff

### 前言

在上一篇文章介绍`VNode`的时候我们说了，`VNode`最大的用途就是在数据变化前后生成真实`DOM`对应的虚拟`DOM`节点，然后就可以对比新旧两份`VNode`，找出差异所在，然后更新有差异的`DOM`节点，最终达到以最少操作真实`DOM`更新视图的目的。而对比新旧两份`VNode`并找出差异的过程就是所谓的`DOM-Diff`过程。`DOM-Diff`算法是整个虚拟`DOM`的核心所在，那么接下来，我们就以源码出发，深入研究一下`Vue`中的`DOM-Diff`过程是怎样的。

### patch

在`Vue`中，把 `DOM-Diff`过程叫做`patch`过程。patch,意为“补丁”，即指对旧的`VNode`修补，打补丁从而得到新的`VNode`，非常形象哈。那不管叫什么，其本质都是把对比新旧两份`VNode`的过程。我们在下面研究`patch`过程的时候，一定把握住这样一个思想：所谓旧的`VNode`(即`oldVNode`)就是数据变化之前视图所对应的虚拟`DOM`节点，而新的`VNode`是数据变化之后将要渲染的新的视图所对应的虚拟`DOM`节点，所以我们要以生成的新的`VNode`为基准，对比旧的`oldVNode`，如果新的`VNode`上有的节点而旧的`oldVNode`上没有，那么就在旧的`oldVNode`上加上去；如果新的`VNode`上没有的节点而旧的`oldVNode`上有，那么就在旧的`oldVNode`上去掉；如果某些节点在新的`VNode`和旧的`oldVNode`上都有，那么就以新的`VNode`为准，更新旧的`oldVNode`，从而让新旧`VNode`相同。

可能你感觉有点绕，没关系，我们在说的通俗一点，你可以这样理解：假设你电脑上现在有一份旧的电子版文档，此时老板又给了你一份新的纸质板文档，并告诉你这两份文档内容大部分都是一样的，让你以新的纸质版文档为准，把纸质版文档做一份新的电子版文档发给老板。对于这个任务此时，你应该有两种解决方案：一种方案是不管它旧的文档内容是什么样的，统统删掉，然后对着新的纸质版文档一个字一个字的敲进去，这种方案就是不用费脑，就是受点累也能解决问题。而另外一种方案是以新的纸质版文档为基准，对比看旧的电子版文档跟新的纸质版文档有什么差异，如果某些部分在新的文档里有而旧的文档里没有，那就在旧的文档里面把这些部分加上；如果某些部分在新的文档里没有而旧的文档里有，那就在旧的文档里把这些部分删掉；如果某些部分在新旧文档里都有，那就对比看有没有需要更新的，最后在旧的文档里更新一下，最终达到把旧的文档变成跟手里纸质版文档一样，完美解决。

对比以上两种方案，显然你和`Vue`一样聪明，肯定会选择第二种方案。第二种方案里的旧的电子版文档对应就是已经渲染在视图上的`oldVNode`，新的纸质版文档对应的是将要渲染在视图上的新的`VNode`。总之一句话：**以新的VNode为基准，改造旧的oldVNode使之成为跟新的VNode一样，这就是patch过程要干的事**。

说了这么多，听起来感觉好像很复杂的样子，其实不然，我们仔细想想，整个`patch`无非就是干三件事：

- 创建节点：新的`VNode`中有而旧的`oldVNode`中没有，就在旧的`oldVNode`中创建。
- 删除节点：新的`VNode`中没有而旧的`oldVNode`中有，就从旧的`oldVNode`中删除。
- 更新节点：新的`VNode`和旧的`oldVNode`中都有，就以新的`VNode`为准，更新旧的`oldVNode`。

OK，到这里，你就对`Vue`中的`patch`过程理解了一半了，接下来，我们就逐个分析，看`Vue`对于以上三件事都是怎么做的。

### 创建节点

在上篇文章中我们分析了，`VNode`类可以描述6种类型的节点，而实际上只有3种类型的节点能够被创建并插入到`DOM`中，它们分别是：元素节点、文本节点、注释节点。所以`Vue`在创建节点的时候会判断在新的`VNode`中有而旧的`oldVNode`中没有的这个节点是属于哪种类型的节点，从而调用不同的方法创建并插入到`DOM`中。

其实判断起来也不难，因为这三种类型的节点其特点非常明显，在源码中是怎么判断的：

```javascript
// 源码位置: /src/core/vdom/patch.js
function createElm (vnode, parentElm, refElm) {
    const data = vnode.data
    const children = vnode.children
    const tag = vnode.tag
    if (isDef(tag)) {
      vnode.elm = nodeOps.createElement(tag, vnode)   // 创建元素节点
      createChildren(vnode, children, insertedVnodeQueue) // 创建元素节点的子节点
      insert(parentElm, vnode.elm, refElm)       // 插入到DOM中
    } else if (isTrue(vnode.isComment)) {
      vnode.elm = nodeOps.createComment(vnode.text)  // 创建注释节点
      insert(parentElm, vnode.elm, refElm)           // 插入到DOM中
    } else {
      vnode.elm = nodeOps.createTextNode(vnode.text)  // 创建文本节点
      insert(parentElm, vnode.elm, refElm)           // 插入到DOM中
    }
  }

```

从上面代码中，我们可以看出：

- 判断是否为元素节点只需判断该`VNode`节点是否有`tag`标签即可。如果有`tag`属性即认为是元素节点，则调用`createElement`方法创建元素节点，通常元素节点还会有子节点，那就递归遍历创建所有子节点，将所有子节点创建好之后`insert`插入到当前元素节点里面，最后把当前元素节点插入到`DOM`中。
- 判断是否为注释节点，只需判断`VNode`的`isComment`属性是否为`true`即可，若为`true`则为注释节点，则调用`createComment`方法创建注释节点，再插入到`DOM`中。
- 如果既不是元素节点，也不是注释节点，那就认为是文本节点，则调用`createTextNode`方法创建文本节点，再插入到`DOM`中。

> 代码中的`nodeOps`是`Vue`为了跨平台兼容性，对所有节点操作进行了封装，例如`nodeOps.createTextNode()`在浏览器端等同于`document.createTextNode()`

以上就完成了创建节点的操作，其完整流程图如下：
![](~@/learn-vue-source-code/virtualDOM/2.png)

### 删除节点

如果某些节点再新的`VNode`中没有而在旧的`oldVNode`中有，那么就需要把这些节点从旧的`oldVNode`中删除。删除节点非常简单，只需在要删除节点的父元素上调用`removeChild`方法即可。源码如下：

```javascript
function removeNode (el) {
  const parent = nodeOps.parentNode(el)  // 获取父节点
  if (isDef(parent)) {
    nodeOps.removeChild(parent, el)  // 调用父节点的removeChild方法
  }
}
```

### 更新节点

创建节点和删除节点都比较简单，而更新节点就相对较为复杂一点了，其实也不算多复杂，只要理清逻辑就能理解了。

更新节点就是当某些节点在新的`VNode`和旧的`oldVNode`中都有时，我们就需要细致比较一下，找出不一样的地方进行更新。

介绍更新节点之前，我们先介绍一个小的概念，就是什么是静态节点？我们看个例子：

```html
<p>我是不会变化的文字</p>
```

上面这个节点里面只包含了纯文字，没有任何可变的变量，这也就是说，不管数据再怎么变化，只要这个节点第一次渲染了，那么它以后就永远不会发生变化，这是因为它不包含任何变量，所以数据发生任何变化都与它无关。我们把这种节点称之为静态节点。

OK，有了这个概念以后，我们开始更新节点。更新节点的时候我们需要对以下3种情况进行判断并分别处理：

1. 如果`VNode`和`oldVNode`均为静态节点

   我们说了，静态节点无论数据发生任何变化都与它无关，所以都为静态节点的话则直接跳过，无需处理。

2. 如果`VNode`是文本节点

   如果`VNode`是文本节点即表示这个节点内只包含纯文本，那么只需看`oldVNode`是否也是文本节点，如果是，那就比较两个文本是否不同，如果不同则把`oldVNode`里的文本改成跟`VNode`的文本一样。如果`oldVNode`不是文本节点，那么不论它是什么，直接调用`setTextNode`方法把它改成文本节点，并且文本内容跟`VNode`相同。

3. 如果`VNode`是元素节点

   如果`VNode`是元素节点，则又细分以下两种情况：

   - 该节点包含子节点

     如果新的节点内包含了子节点，那么此时要看旧的节点是否包含子节点，如果旧的节点里也包含了子节点，那就需要递归对比更新子节点；如果旧的节点里不包含子节点，那么这个旧节点有可能是空节点或者是文本节点，如果旧的节点是空节点就把新的节点里的子节点创建一份然后插入到旧的节点里面，如果旧的节点是文本节点，则把文本清空，然后把新的节点里的子节点创建一份然后插入到旧的节点里面。

   - 该节点不包含子节点

     如果该节点不包含子节点，同时它又不是文本节点，那就说明该节点是个空节点，那就好办了，不管旧节点之前里面都有啥，直接清空即可。

OK，处理完以上3种情况，更新节点就算基本完成了，接下来我们看下源码中具体是怎么实现的，源码如下：

```javascript
// 更新节点
function patchVnode (oldVnode, vnode, insertedVnodeQueue, removeOnly) {
  // vnode与oldVnode是否完全一样？若是，退出程序
  if (oldVnode === vnode) {
    return
  }
  const elm = vnode.elm = oldVnode.elm

  // vnode与oldVnode是否都是静态节点？若是，退出程序
  if (isTrue(vnode.isStatic) &&
    isTrue(oldVnode.isStatic) &&
    vnode.key === oldVnode.key &&
    (isTrue(vnode.isCloned) || isTrue(vnode.isOnce))
  ) {
    return
  }

  const oldCh = oldVnode.children
  const ch = vnode.children
  // vnode有text属性？若没有：
  if (isUndef(vnode.text)) {
    // vnode的子节点与oldVnode的子节点是否都存在？
    if (isDef(oldCh) && isDef(ch)) {
      // 若都存在，判断子节点是否相同，不同则更新子节点
      if (oldCh !== ch) updateChildren(elm, oldCh, ch, insertedVnodeQueue, removeOnly)
    }
    // 若只有vnode的子节点存在
    else if (isDef(ch)) {
      /**
       * 判断oldVnode是否有文本？
       * 若没有，则把vnode的子节点添加到真实DOM中
       * 若有，则清空Dom中的文本，再把vnode的子节点添加到真实DOM中
       */
      if (isDef(oldVnode.text)) nodeOps.setTextContent(elm, '')
      addVnodes(elm, null, ch, 0, ch.length - 1, insertedVnodeQueue)
    }
    // 若只有oldnode的子节点存在
    else if (isDef(oldCh)) {
      // 清空DOM中的子节点
      removeVnodes(elm, oldCh, 0, oldCh.length - 1)
    }
    // 若vnode和oldnode都没有子节点，但是oldnode中有文本
    else if (isDef(oldVnode.text)) {
      // 清空oldnode文本
      nodeOps.setTextContent(elm, '')
    }
    // 上面两个判断一句话概括就是，如果vnode中既没有text，也没有子节点，那么对应的oldnode中有什么就清空什么
  }
  // 若有，vnode的text属性与oldVnode的text属性是否相同？
  else if (oldVnode.text !== vnode.text) {
    // 若不相同：则用vnode的text替换真实DOM的文本
    nodeOps.setTextContent(elm, vnode.text)
  }
}
```

上面代码里注释已经写得很清晰了，接下来我们画流程图来梳理一下整个过程，流程图如下：
![](~@/learn-vue-source-code/virtualDOM/3.png)

通过对照着流程图以及代码，相信更新节点这部分逻辑你很容易就能理解了。

另外，你可能注意到了，如果新旧`VNode`里都包含了子节点，那么对于子节点的更新在代码里调用了`updateChildren`方法，而这个方法的逻辑到底是怎样的我们放在下一篇文章中展开学习。

### 总结

在本篇文章中我们介绍了`Vue`中的`DOM-Diff`算法：patch过程。我们先介绍了算法的整个思想流程，然后通过梳理算法思想，了解了整个`patch`过程干了三件事，分别是：创建节点，删除节点，更新节点。并且对每件事情都对照源码展开了细致的学习，画出了其逻辑流程图。另外对于更新节点中，如果新旧`VNode`里都包含了子节点，我们就需要细致的去更新子节点，关于更新子节点的过程我们在下一篇文章中展开学习。


## 3.3 更新子节点

### 前言

在上一篇文章中，我们了解了`Vue`中的`patch`过程，即`DOM-Diff`算法。并且知道了在`patch`过程中基本会干三件事，分别是：创建节点，删除节点和更新节点。创建节点和删除节点都比较简单，而更新节点因为要处理各种可能出现的情况所以逻辑略微复杂一些，但是没关系，我们通过分析过程，对照源码，画逻辑流程图来帮助我们理解了其中的过程。最后我们还遗留了一个问题，那就是在更新节点过程中，新旧`VNode`可能都包含有子节点，对于子节点的对比更新会有额外的一些逻辑，那么在本篇文章中我们就来学习在`Vue`中是怎么对比更新子节点的。

### 更新子节点

当新的`VNode`与旧的`oldVNode`都是元素节点并且都包含子节点时，那么这两个节点的`VNode`实例上的`children`属性就是所包含的子节点数组。我们把新的`VNode`上的子节点数组记为`newChildren`，把旧的`oldVNode`上的子节点数组记为`oldChildren`，我们把`newChildren`里面的元素与`oldChildren`里的元素一一进行对比，对比两个子节点数组肯定是要通过循环，外层循环`newChildren`数组，内层循环`oldChildren`数组，每循环外层`newChildren`数组里的一个子节点，就去内层`oldChildren`数组里找看有没有与之相同的子节点，伪代码如下：

```javascript
for (let i = 0; i < newChildren.length; i++) {
  const newChild = newChildren[i];
  for (let j = 0; j < oldChildren.length; j++) {
    const oldChild = oldChildren[j];
    if (newChild === oldChild) {
      // ...
    }
  }
}
```

那么以上这个过程将会存在以下四种情况：

- 创建子节点

  如果`newChildren`里面的某个子节点在`oldChildren`里找不到与之相同的子节点，那么说明`newChildren`里面的这个子节点是之前没有的，是需要此次新增的节点，那么就创建子节点。

- 删除子节点

  如果把`newChildren`里面的每一个子节点都循环完毕后，发现在`oldChildren`还有未处理的子节点，那就说明这些未处理的子节点是需要被废弃的，那么就将这些节点删除。

- 移动子节点

  如果`newChildren`里面的某个子节点在`oldChildren`里找到了与之相同的子节点，但是所处的位置不同，这说明此次变化需要调整该子节点的位置，那就以`newChildren`里子节点的位置为基准，调整`oldChildren`里该节点的位置，使之与在`newChildren`里的位置相同。

- 更新节点

  如果`newChildren`里面的某个子节点在`oldChildren`里找到了与之相同的子节点，并且所处的位置也相同，那么就更新`oldChildren`里该节点，使之与`newChildren`里的该节点相同。

OK，到这里，逻辑就相对清晰了，接下来我们只需分门别类的处理这四种情况就好了。

### 创建子节点

如果`newChildren`里面的某个子节点在`oldChildren`里找不到与之相同的子节点，那么说明`newChildren`里面的这个子节点是之前没有的，是需要此次新增的节点，那么我们就创建这个节点，创建好之后再把它插入到`DOM`中合适的位置。

创建节点这个很容易，我们在上一篇文章的第三章已经介绍过了，这里就不再赘述了。

那么创建好之后如何插入到`DOM`中的合适的位置呢？显然，把节点插入到`DOM`中是很容易的，找到合适的位置是关键。接下来我们分析一下如何找这个合适的位置。我们看下面这个图：
![](~@/learn-vue-source-code/virtualDOM/4.png)

上图中左边是新的`VNode`，右边是旧的`oldVNode`，同时也是真实的`DOM`。这个图意思是当我们循环`newChildren`数组里面的子节点，前两个子节点都在`oldChildren`里找到了与之对应的子节点，那么我们将其处理，处理过后把它们标志为已处理，当循环到`newChildren`数组里第三个子节点时，发现在`oldChildren`里找不到与之对应的子节点，那么我们就需要创建这个节点，创建好之后我们发现这个节点本是`newChildren`数组里左起第三个子节点，那么我们就把创建好的节点插入到真实`DOM`里的第三个节点位置，也就是所有已处理节点之后，OK，此时我们拍手称快，所有已处理节点之后就是我们要找的合适的位置，但是真的是这样吗？我们再来看下面这个图：
![](~@/learn-vue-source-code/virtualDOM/5.png)

假如我们按照上面的方法把第三个节点插入到所有已处理节点之后，此时如果第四个节点也在`oldChildren`里找不到与之对应的节点，也是需要创建的节点，那么当我们把第四个节点也按照上面的说的插入到已处理节点之后，发现怎么插入到第三个位置了，可明明这个节点在`newChildren`数组里是第四个啊！

这就是问题所在，其实，我们应该把新创建的节点插入到所有未处理节点之前，这样以来逻辑才正确。后面不管有多少个新增的节点，每一个都插入到所有未处理节点之前，位置才不会错。

所以，**合适的位置是所有未处理节点之前，而并非所有已处理节点之后**。

### 删除子节点

如果把`newChildren`里面的每一个子节点都循环一遍，能在`oldChildren`数组里找到的就处理它，找不到的就新增，直到把`newChildren`里面所有子节点都过一遍后，发现在`oldChildren`还存在未处理的子节点，那就说明这些未处理的子节点是需要被废弃的，那么就将这些节点删除。

删除节点这个也很容易，我们在上一篇文章的第四章已经介绍过了，这里就不再赘述了。

### 更新子节点

如果`newChildren`里面的某个子节点在`oldChildren`里找到了与之相同的子节点，并且所处的位置也相同，那么就更新`oldChildren`里该节点，使之与`newChildren`里的该节点相同。

关于更新节点，我们在上一篇文章的第五章已经介绍过了，这里就不再赘述了。

### 移动子节点

如果`newChildren`里面的某个子节点在`oldChildren`里找到了与之相同的子节点，但是所处的位置不同，这说明此次变化需要调整该子节点的位置，那就以`newChildren`里子节点的位置为基准，调整`oldChildren`里该节点的位置，使之与在`newChildren`里的位置相同。

同样，移动一个节点不难，关键在于该移动到哪，或者说关键在于移动到哪个位置，这个位置才是关键。我们看下图：
![](~@/learn-vue-source-code/virtualDOM/6.png)

在上图中，绿色的两个节点是相同节点但是所处位置不同，即`newChildren`里面的第三个子节点与真实`DOM`即`oldChildren`里面的第四个子节点相同但是所处位置不同，按照上面所说的，我们应该以`newChildren`里子节点的位置为基准，调整`oldChildren`里该节点的位置，所以我们应该把真实`DOM`即`oldChildren`里面的第四个节点移动到第三个节点的位置，通过上图中的标注我们不难发现，**所有未处理节点之前就是我们要移动的目的位置**。如果此时你说那可不可以移动到所有已处理节点之后呢？那就又回到了更新节点时所遇到的那个问题了：如果前面有新增的节点呢？

### 回到源码

OK，以上就是更新子节点时所要考虑的所有情况了，分析完以后，我们回到源码里看看实际情况是不是我们分析的这样子的，源码如下：

```javascript
// 源码位置： /src/core/vdom/patch.js

if (isUndef(idxInOld)) {    // 如果在oldChildren里找不到当前循环的newChildren里的子节点
    // 新增节点并插入到合适位置
    createElm(newStartVnode, insertedVnodeQueue, parentElm, oldStartVnode.elm, false, newCh, newStartIdx)
} else {
    // 如果在oldChildren里找到了当前循环的newChildren里的子节点
    vnodeToMove = oldCh[idxInOld]
    // 如果两个节点相同
    if (sameVnode(vnodeToMove, newStartVnode)) {
        // 调用patchVnode更新节点
        patchVnode(vnodeToMove, newStartVnode, insertedVnodeQueue)
        oldCh[idxInOld] = undefined
        // canmove表示是否需要移动节点，如果为true表示需要移动，则移动节点，如果为false则不用移动
        canMove && nodeOps.insertBefore(parentElm, vnodeToMove.elm, oldStartVnode.elm)
    }
}
```

以上代码中，首先判断在`oldChildren`里能否找到当前循环的`newChildren`里的子节点，如果找不到，那就是新增节点并插入到合适位置；如果找到了，先对比两个节点是否相同，若相同则先调用`patchVnode`更新节点，更新完之后再看是否需要移动节点，注意，源码里在判断是否需要移动子节点时用了简写的方式，下面这两种写法是等价的：

```javascript
canMove && nodeOps.insertBefore(parentElm, vnodeToMove.elm, oldStartVnode.elm)
// 等同于
if(canMove){
  nodeOps.insertBefore(parentElm, vnodeToMove.elm, oldStartVnode.elm)
}
```

我们看到，源码里的实现跟我们分析的是一样一样的。

### 总结

本篇文章我们分析了`Vue`在更新子节点时是外层循环`newChildren`数组，内层循环`oldChildren`数组，把`newChildren`数组里的每一个元素分别与`oldChildren`数组里的每一个元素匹配，根据不同情况作出创建子节点、删除子节点、更新子节点以及移动子节点的操作。并且我们对不同情况的不同操作都进行了深入分析，分析之后我们回到源码验证我们分析的正确性，发现我们的分析跟源码的实现是一致的。

最后，我们再思考一个问题：这样双层循环虽然能解决问题，但是如果节点数量很多，这样循环算法的时间复杂度会不会很高？有没有什么可以优化的办法？答案当然是有的，并且`Vue`也意识到了这点，也进行了优化，那么下篇文章我们就来分析当节点数量很多时`Vue`是怎么优化算法的。

## 3.4 优化更新子节点

### 前言

在上一篇文章中，我们介绍了当新的`VNode`与旧的`oldVNode`都是元素节点并且都包含子节点时，`Vue`对子节点是

先外层循环`newChildren`数组，再内层循环`oldChildren`数组，每循环外层`newChildren`数组里的一个子节点，就去内层`oldChildren`数组里找看有没有与之相同的子节点，最后根据不同的情况作出不同的操作。

在上一篇文章的结尾我们也说了，这种方法虽然能够解决问题，但是还存在可优化的地方。比如当包含的子节点数量很多时，这样循环算法的时间复杂度就会变的很大，不利于性能提升。当然，`Vue`也意识到了这点，并对此也进行了优化，那么本篇文章，就来学习一下关于子节点更新的优化问题`Vue`是如何做的。

### 优化策略介绍

假如我们现有一份新的`newChildren`数组和旧的`oldChildren`数组，如下所示：

```javascript
newChildren = ['新子节点1','新子节点2','新子节点3','新子节点4']
oldChildren = ['旧子节点1','旧子节点2','旧子节点3','旧子节点4']
```

如果按照优化之前的解决方案，那么我们接下来的操作应该是这样的：先循环`newChildren`数组，拿到第一个新子节点1，然后用第一个新子节点1去跟`oldChildren`数组里的旧子节点逐一对比，如果运气好一点，刚好`oldChildren`数组里的第一个旧子节点1与第一个新子节点1相同，那就皆大欢喜，直接处理，不用再往下循环了。那如果运气坏一点，直到循环到`oldChildren`数组里的第四个旧子节点4才与第一个新子节点1相同，那此时就会多循环了4次。我们不妨把情况再设想的极端一点，如果`newChildren`数组和`oldChildren`数组里前三个节点都没有变化，只是第四个节点发生了变化，那么我们就会循环16次，只有在第16次循环的时候才发现新节点4与旧节点4相同，进行更新，如下图所示：
![](~@/learn-vue-source-code/virtualDOM/7.jpg)

上面例子中只有四个子节点，好像还看不出来有什么缺陷，但是当子节点数量很多的时候，算法的时间复杂度就会非常高，很不利于性能提升。

那么我们该怎么优化呢？其实我们可以这样想，我们不要按顺序去循环`newChildren`和`oldChildren`这两个数组，可以先比较这两个数组里特殊位置的子节点，比如：

- 先把`newChildren`数组里的所有未处理子节点的第一个子节点和`oldChildren`数组里所有未处理子节点的第一个子节点做比对，如果相同，那就直接进入更新节点的操作；
- 如果不同，再把`newChildren`数组里所有未处理子节点的最后一个子节点和`oldChildren`数组里所有未处理子节点的最后一个子节点做比对，如果相同，那就直接进入更新节点的操作；
- 如果不同，再把`newChildren`数组里所有未处理子节点的最后一个子节点和`oldChildren`数组里所有未处理子节点的第一个子节点做比对，如果相同，那就直接进入更新节点的操作，更新完后再将`oldChildren`数组里的该节点移动到与`newChildren`数组里节点相同的位置；
- 如果不同，再把`newChildren`数组里所有未处理子节点的第一个子节点和`oldChildren`数组里所有未处理子节点的最后一个子节点做比对，如果相同，那就直接进入更新节点的操作，更新完后再将`oldChildren`数组里的该节点移动到与`newChildren`数组里节点相同的位置；
- 最后四种情况都试完如果还不同，那就按照之前循环的方式来查找节点。

其过程如下图所示：
![](~@/learn-vue-source-code/virtualDOM/8.png)

在上图中，我们把：

- `newChildren`数组里的所有未处理子节点的第一个子节点称为：新前；
- `newChildren`数组里的所有未处理子节点的最后一个子节点称为：新后；
- `oldChildren`数组里的所有未处理子节点的第一个子节点称为：旧前；
- `oldChildren`数组里的所有未处理子节点的最后一个子节点称为：旧后；

OK，有了以上概念以后，下面我们就来看看其具体是如何实施的。

### 新前与旧前

把`newChildren`数组里的所有未处理子节点的第一个子节点和`oldChildren`数组里所有未处理子节点的第一个子节点做比对，如果相同，那好极了，直接进入之前文章中说的更新节点的操作并且由于新前与旧前两个节点的位置也相同，无需进行节点移动操作；如果不同，没关系，再尝试后面三种情况。
![](~@/learn-vue-source-code/virtualDOM/9.png)

### 新后与旧后

把`newChildren`数组里所有未处理子节点的最后一个子节点和`oldChildren`数组里所有未处理子节点的最后一个子节点做比对，如果相同，那就直接进入更新节点的操作并且由于新后与旧后两个节点的位置也相同，无需进行节点移动操作；如果不同，继续往后尝试。
![](~@/learn-vue-source-code/virtualDOM/10.png)

### 新后与旧前

把`newChildren`数组里所有未处理子节点的最后一个子节点和`oldChildren`数组里所有未处理子节点的第一个子节点做比对，如果相同，那就直接进入更新节点的操作，更新完后再将`oldChildren`数组里的该节点移动到与`newChildren`数组里节点相同的位置；
![](~@/learn-vue-source-code/virtualDOM/11.png)

此时，出现了移动节点的操作，移动节点最关键的地方在于找准要移动的位置。我们一再强调，**更新节点要以新`VNode`为基准，然后操作旧的`oldVNode`，使之最后旧的`oldVNode`与新的`VNode`相同**。那么现在的情况是：`newChildren`数组里的最后一个子节点与`oldChildren`数组里的第一个子节点相同，那么我们就应该在`oldChildren`数组里把第一个子节点移动到最后一个子节点的位置，如下图：

![](~@/learn-vue-source-code/virtualDOM/12.png)

从图中不难看出，我们要把`oldChildren`数组里把第一个子节点移动到数组中**所有未处理节点之后**。

如果对比之后发现这两个节点仍不是同一个节点，那就继续尝试最后一种情况。

### 新前与旧后

把`newChildren`数组里所有未处理子节点的第一个子节点和`oldChildren`数组里所有未处理子节点的最后一个子节点做比对，如果相同，那就直接进入更新节点的操作，更新完后再将`oldChildren`数组里的该节点移动到与`newChildren`数组里节点相同的位置；

![](~@/learn-vue-source-code/virtualDOM/13.png)

同样，这种情况的节点移动位置逻辑与“新后与旧前”的逻辑类似，那就是`newChildren`数组里的第一个子节点与`oldChildren`数组里的最后一个子节点相同，那么我们就应该在`oldChildren`数组里把最后一个子节点移动到第一个子节点的位置，如下图：

![](~@/learn-vue-source-code/virtualDOM/14.png)

从图中不难看出，我们要把`oldChildren`数组里把最后一个子节点移动到数组中**所有未处理节点之前**。

OK，以上就是子节点对比更新优化策略种的4种情况，如果以上4种情况逐个试遍之后要是还没找到相同的节点，那就再通过之前的循环方式查找。

### 回到源码

思路分析完，逻辑理清之后，我们再回到源码里看看，验证一下源码实现的逻辑是否跟我们分析的一样。源码如下：

```javascript
// 循环更新子节点
  function updateChildren (parentElm, oldCh, newCh, insertedVnodeQueue, removeOnly) {
    let oldStartIdx = 0               // oldChildren开始索引
    let oldEndIdx = oldCh.length - 1   // oldChildren结束索引
    let oldStartVnode = oldCh[0]        // oldChildren中所有未处理节点中的第一个
    let oldEndVnode = oldCh[oldEndIdx]   // oldChildren中所有未处理节点中的最后一个

    let newStartIdx = 0               // newChildren开始索引
    let newEndIdx = newCh.length - 1   // newChildren结束索引
    let newStartVnode = newCh[0]        // newChildren中所有未处理节点中的第一个
    let newEndVnode = newCh[newEndIdx]  // newChildren中所有未处理节点中的最后一个

    let oldKeyToIdx, idxInOld, vnodeToMove, refElm

    // removeOnly is a special flag used only by <transition-group>
    // to ensure removed elements stay in correct relative positions
    // during leaving transitions
    const canMove = !removeOnly

    if (process.env.NODE_ENV !== 'production') {
      checkDuplicateKeys(newCh)
    }

    // 以"新前"、"新后"、"旧前"、"旧后"的方式开始比对节点
    while (oldStartIdx <= oldEndIdx && newStartIdx <= newEndIdx) {
      if (isUndef(oldStartVnode)) {
        oldStartVnode = oldCh[++oldStartIdx] // 如果oldStartVnode不存在，则直接跳过，比对下一个
      } else if (isUndef(oldEndVnode)) {
        oldEndVnode = oldCh[--oldEndIdx]
      } else if (sameVnode(oldStartVnode, newStartVnode)) {
        // 如果新前与旧前节点相同，就把两个节点进行patch更新
        patchVnode(oldStartVnode, newStartVnode, insertedVnodeQueue)
        oldStartVnode = oldCh[++oldStartIdx]
        newStartVnode = newCh[++newStartIdx]
      } else if (sameVnode(oldEndVnode, newEndVnode)) {
        // 如果新后与旧后节点相同，就把两个节点进行patch更新
        patchVnode(oldEndVnode, newEndVnode, insertedVnodeQueue)
        oldEndVnode = oldCh[--oldEndIdx]
        newEndVnode = newCh[--newEndIdx]
      } else if (sameVnode(oldStartVnode, newEndVnode)) { // Vnode moved right
        // 如果新后与旧前节点相同，先把两个节点进行patch更新，然后把旧前节点移动到oldChilren中所有未处理节点之后
        patchVnode(oldStartVnode, newEndVnode, insertedVnodeQueue)
        canMove && nodeOps.insertBefore(parentElm, oldStartVnode.elm, nodeOps.nextSibling(oldEndVnode.elm))
        oldStartVnode = oldCh[++oldStartIdx]
        newEndVnode = newCh[--newEndIdx]
      } else if (sameVnode(oldEndVnode, newStartVnode)) { // Vnode moved left
        // 如果新前与旧后节点相同，先把两个节点进行patch更新，然后把旧后节点移动到oldChilren中所有未处理节点之前
        patchVnode(oldEndVnode, newStartVnode, insertedVnodeQueue)
        canMove && nodeOps.insertBefore(parentElm, oldEndVnode.elm, oldStartVnode.elm)
        oldEndVnode = oldCh[--oldEndIdx]
        newStartVnode = newCh[++newStartIdx]
      } else {
        // 如果不属于以上四种情况，就进行常规的循环比对patch
        if (isUndef(oldKeyToIdx)) oldKeyToIdx = createKeyToOldIdx(oldCh, oldStartIdx, oldEndIdx)
        idxInOld = isDef(newStartVnode.key)
          ? oldKeyToIdx[newStartVnode.key]
          : findIdxInOld(newStartVnode, oldCh, oldStartIdx, oldEndIdx)
        // 如果在oldChildren里找不到当前循环的newChildren里的子节点
        if (isUndef(idxInOld)) { // New element
          // 新增节点并插入到合适位置
          createElm(newStartVnode, insertedVnodeQueue, parentElm, oldStartVnode.elm, false, newCh, newStartIdx)
        } else {
          // 如果在oldChildren里找到了当前循环的newChildren里的子节点
          vnodeToMove = oldCh[idxInOld]
          // 如果两个节点相同
          if (sameVnode(vnodeToMove, newStartVnode)) {
            // 调用patchVnode更新节点
            patchVnode(vnodeToMove, newStartVnode, insertedVnodeQueue)
            oldCh[idxInOld] = undefined
            // canmove表示是否需要移动节点，如果为true表示需要移动，则移动节点，如果为false则不用移动
            canMove && nodeOps.insertBefore(parentElm, vnodeToMove.elm, oldStartVnode.elm)
          } else {
            // same key but different element. treat as new element
            createElm(newStartVnode, insertedVnodeQueue, parentElm, oldStartVnode.elm, false, newCh, newStartIdx)
          }
        }
        newStartVnode = newCh[++newStartIdx]
      }
    }
    if (oldStartIdx > oldEndIdx) {
      /**
       * 如果oldChildren比newChildren先循环完毕，
       * 那么newChildren里面剩余的节点都是需要新增的节点，
       * 把[newStartIdx, newEndIdx]之间的所有节点都插入到DOM中
       */
      refElm = isUndef(newCh[newEndIdx + 1]) ? null : newCh[newEndIdx + 1].elm
      addVnodes(parentElm, refElm, newCh, newStartIdx, newEndIdx, insertedVnodeQueue)
    } else if (newStartIdx > newEndIdx) {
      /**
       * 如果newChildren比oldChildren先循环完毕，
       * 那么oldChildren里面剩余的节点都是需要删除的节点，
       * 把[oldStartIdx, oldEndIdx]之间的所有节点都删除
       */
      removeVnodes(parentElm, oldCh, oldStartIdx, oldEndIdx)
    }
  }

```

读源码之前，我们先有这样一个概念：那就是在我们前面所说的优化策略中，节点有可能是从前面对比，也有可能是从后面对比，对比成功就会进行更新处理，也就是说我们有可能处理第一个，也有可能处理最后一个，那么我们在循环的时候就不能简单从前往后或从后往前循环，而是要从两边向中间循环。

那么该如何从两边向中间循环呢？请看下图：
![](~@/learn-vue-source-code/virtualDOM/15.png)

首先，我们先准备4个变量：

- **newStartIdx:**`newChildren`数组里开始位置的下标；
- **newEndIdx:**`newChildren`数组里结束位置的下标；
- **oldStartIdx:**`oldChildren`数组里开始位置的下标；
- **oldEndIdx:**`oldChildren`数组里结束位置的下标；

在循环的时候，每处理一个节点，就将下标向图中箭头所指的方向移动一个位置，开始位置所表示的节点被处理后，就向后移动一个位置；结束位置所表示的节点被处理后，就向前移动一个位置；由于我们的优化策略都是新旧节点两两更新的，所以一次更新将会移动两个节点。说的再直白一点就是：`newStartIdx`和`oldStartIdx`只能往后移动（只会加），`newEndIdx`和`oldEndIdx`只能往前移动（只会减）。

当开始位置大于结束位置时，表示所有节点都已经遍历过了。

OK，有了这个概念后，我们开始读源码：

1. 如果`oldStartVnode`不存在，则直接跳过，将`oldStartIdx`加1，比对下一个

   ```javascript
   // 以"新前"、"新后"、"旧前"、"旧后"的方式开始比对节点
   while (oldStartIdx <= oldEndIdx && newStartIdx <= newEndIdx) {
    if (isUndef(oldStartVnode)) {
      oldStartVnode = oldCh[++oldStartIdx]
    }
   }
   ```

2. 如果`oldEndVnode`不存在，则直接跳过，将`oldEndIdx`减1，比对前一个

   ```javascript
   else if (isUndef(oldEndVnode)) {
       oldEndVnode = oldCh[--oldEndIdx]
   }
   ```

3. 如果新前与旧前节点相同，就把两个节点进行`patch`更新，同时`oldStartIdx`和`newStartIdx`都加1，后移一个位置

   ```javascript
   else if (sameVnode(oldStartVnode, newStartVnode)) {
       patchVnode(oldStartVnode, newStartVnode, insertedVnodeQueue)
       oldStartVnode = oldCh[++oldStartIdx]
       newStartVnode = newCh[++newStartIdx]
   }
   ```

4. 如果新后与旧后节点相同，就把两个节点进行`patch`更新，同时`oldEndIdx`和`newEndIdx`都减1，前移一个位置

   ```javascript
   else if (sameVnode(oldEndVnode, newEndVnode)) {
       patchVnode(oldEndVnode, newEndVnode, insertedVnodeQueue)
       oldEndVnode = oldCh[--oldEndIdx]
       newEndVnode = newCh[--newEndIdx]
   }
   ```

5. 如果新后与旧前节点相同，先把两个节点进行`patch`更新，然后把旧前节点移动到`oldChilren`中所有未处理节点之后，最后把`oldStartIdx`加1，后移一个位置，`newEndIdx`减1，前移一个位置

   ```javascript
   else if (sameVnode(oldStartVnode, newEndVnode)) {
       patchVnode(oldStartVnode, newEndVnode, insertedVnodeQueue)
       canMove && nodeOps.insertBefore(parentElm, oldStartVnode.elm, nodeOps.nextSibling(oldEndVnode.elm))
       oldStartVnode = oldCh[++oldStartIdx]
       newEndVnode = newCh[--newEndIdx]
   }
   ```

6. 如果新前与旧后节点相同，先把两个节点进行`patch`更新，然后把旧后节点移动到`oldChilren`中所有未处理节点之前，最后把`newStartIdx`加1，后移一个位置，`oldEndIdx`减1，前移一个位置

   ```javascript
   else if (sameVnode(oldEndVnode, newStartVnode)) { // Vnode moved left
       patchVnode(oldEndVnode, newStartVnode, insertedVnodeQueue)
       canMove && nodeOps.insertBefore(parentElm, oldEndVnode.elm, oldStartVnode.elm)
       oldEndVnode = oldCh[--oldEndIdx]
       newStartVnode = newCh[++newStartIdx]
   }
   ```

7. 如果不属于以上四种情况，就进行常规的循环比对`patch`

8. 如果在循环中，`oldStartIdx`大于`oldEndIdx`了，那就表示`oldChildren`比`newChildren`先循环完毕，那么`newChildren`里面剩余的节点都是需要新增的节点，把`[newStartIdx, newEndIdx]`之间的所有节点都插入到`DOM`中

   ```javascript
   if (oldStartIdx > oldEndIdx) {
       refElm = isUndef(newCh[newEndIdx + 1]) ? null : newCh[newEndIdx + 1].elm
       addVnodes(parentElm, refElm, newCh, newStartIdx, newEndIdx, insertedVnodeQueue)
   }
   ```

9. 如果在循环中，`newStartIdx`大于`newEndIdx`了，那就表示`newChildren`比`oldChildren`先循环完毕，那么`oldChildren`里面剩余的节点都是需要删除的节点，把`[oldStartIdx, oldEndIdx]`之间的所有节点都删除

   ```javascript
   else if (newStartIdx > newEndIdx) {
       removeVnodes(parentElm, oldCh, oldStartIdx, oldEndIdx)
   }
   ```

OK,处理完毕，可见源码中的处理逻辑跟我们之前分析的逻辑是一样的。

### 总结

本篇文章中，我们介绍了`Vue`中子节点更新的优化策略，发现`Vue`为了避免双重循环数据量大时间复杂度升高带来的性能问题，而选择了从子节点数组中的4个特殊位置互相比对，分别是：新前与旧前，新后与旧后，新后与旧前，新前与旧后。对于每一种情况我们都通过图文的形式对其逻辑进行了分析。最后我们回到源码，通过阅读源码来验证我们分析的是否正确。幸运的是我们之前每一步的分析都在源码中找到了相应的实现，得以验证我们的分析没有错。以上就是`Vue`中的`patch`过程，即`DOM-Diff`算法所有内容了，到这里相信你再读这部分源码的时候就有比较清晰的思路了。

# 4. 模板编译篇

## 4.1 模板编译篇综述

### 前言

在前几篇文章中，我们介绍了`Vue`中的虚拟`DOM`以及虚拟`DOM`的`patch`(DOM-Diff)过程，而虚拟`DOM`存在的必要条件是得先有`VNode`，那么`VNode`又是从哪儿来的呢？这就是接下来几篇文章要说的模板编译。你可以这么理解：把用户写的模板进行编译，就会产生`VNode`。

### 什么是模板编译

我们知道，在日常开发中，我们把写在`<template></template>`标签中的类似于原生`HTML`的内容称之为模板。这时你可能会问了，为什么说是“类似于原生`HTML`的内容”而不是“就是`HTML`的内容”？因为我们在开发中，在`<template></template>`标签中除了写一些原生`HTML`的标签，我们还会写一些变量插值，如{{xxx}}，或者写一些`Vue`指令，如`v-on`、`v-if`等。而这些东西都是在原生`HTML`语法中不存在的，不被接受的。但是事实上我们确实这么写了，也被正确识别了，页面也正常显示了，这又是为什么呢？

这就归功于`Vue`的模板编译了，`Vue`会把用户在`<template></template>`标签中写的类似于原生`HTML`的内容进行编译，把原生`HTML`的内容找出来，再把非原生`HTML`找出来，经过一系列的逻辑处理生成渲染函数，也就是`render`函数，而`render`函数会将模板内容生成对应的`VNode`，而`VNode`再经过前几篇文章介绍的`patch`过程从而得到将要渲染的视图中的`VNode`，最后根据`VNode`创建真实的`DOM`节点并插入到视图中， 最终完成视图的渲染更新。

而把用户在`<template></template>`标签中写的类似于原生`HTML`的内容进行编译，把原生`HTML`的内容找出来，再把非原生`HTML`找出来，经过一系列的逻辑处理生成渲染函数，也就是`render`函数的这一段过程称之为模板编译过程。

### 整体渲染流程

所谓渲染流程，就是把用户写的类似于原生`HTML`的模板经过一系列处理最终反应到视图中称之为整个渲染流程。这个流程在上文中其实已经说到了，下面我们以流程图的形式宏观的了解一下，流程图如下：
![](~@/learn-vue-source-code/complie/1.png)

从图中我们也可以看到，模板编译过程就是把用户写的模板经过一系列处理最终生成`render`函数的过程。

### 模板编译内部流程

那么模板编译内部是怎么把用户写的模板经过处理最终生成`render`函数的呢？这内部的过程是怎样的呢？

####  抽象语法树AST

我们知道，用户在`<template></template>`标签中写的模板对`Vue`来说就是一堆字符串，那么如何解析这一堆字符串并且从中提取出元素的标签、属性、变量插值等有效信息呢？这就需要借助一个叫做抽象语法树的东西。

所谓抽象语法树，在计算机科学中，**抽象语法树**（**A**bstract**S**yntax**T**ree，AST），或简称**语法树**（Syntax tree），是源代码语法结构的一种抽象表示。它以树状的形式表现编程语言的语法结构，树上的每个节点都表示源代码中的一种结构。之所以说语法是“抽象”的，是因为这里的语法并不会表示出真实语法中出现的每个细节。比如，嵌套括号被隐含在树的结构中，并没有以节点的形式呈现；而类似于if-condition-then这样的条件跳转语句，可以使用带有两个分支的节点来表示。——来自百度百科

我就知道，这段话贴出来也是白贴，因为看了也看不懂，哈哈。那么我们就以最直观的例子来理解什么是抽象语法树。请看下图：
![](~@/learn-vue-source-code/complie/2.png)

从图中我们可以看到，一个简单的`HTML`标签的代码被转换成了一个`JS`对象，而这个对象中的属性代表了这个标签中一些关键有效信息。如图中标识。
有兴趣的同学可以在这个网站在线转换试试：https://astexplorer.net/
####  具体流程

将一堆字符串模板解析成抽象语法树`AST`后，我们就可以对其进行各种操作处理了，处理完后用处理后的`AST`来生成`render`函数。其具体流程可大致分为三个阶段：

1. 模板解析阶段：将一堆模板字符串用正则等方式解析成抽象语法树`AST`；
2. 优化阶段：遍历`AST`，找出其中的静态节点，并打上标记；
3. 代码生成阶段：将`AST`转换成渲染函数；

这三个阶段在源码中分别对应三个模块，下面给出三个模块的源代码在源码中的路径：

1. 模板解析阶段——解析器——源码路径：`src/compiler/parser/index.js`;
2. 优化阶段——优化器——源码路径：`src/compiler/optimizer.js`;
3. 代码生成阶段——代码生成器——源码路径：`src/compiler/codegen/index.js`;
其对应的源码如下：

```javascript
// 源码位置: /src/complier/index.js

export const createCompiler = createCompilerCreator(function baseCompile (
  template: string,
  options: CompilerOptions
): CompiledResult {
  // 模板解析阶段：用正则等方式解析 template 模板中的指令、class、style等数据，形成AST
  const ast = parse(template.trim(), options)
  if (options.optimize !== false) {
    // 优化阶段：遍历AST，找出其中的静态节点，并打上标记；
    optimize(ast, options)
  }
  // 代码生成阶段：将AST转换成渲染函数；
  const code = generate(ast, options)
  return {
    ast,
    render: code.render,
    staticRenderFns: code.staticRenderFns
  }
})

```
可以看到 `baseCompile` 的代码非常的简短主要核心代码。

- **const ast =parse(template.trim(), options)**:`parse` 会用正则等方式解析 `template` 模板中的指令、`class`、`style`等数据，形成`AST`。
- **optimize(ast, options)**: `optimize` 的主要作用是标记静态节点，这是 `Vue` 在编译过程中的一处优化，挡在进行`patch` 的过程中， `DOM-Diff` 算法会直接跳过静态节点，从而减少了比较的过程，优化了 `patch` 的性能。
- **const code =generate(ast, options)**: 将 `AST` 转化成 `render`函数字符串的过程，得到结果是 `render`函数 的字符串以及 `staticRenderFns` 字符串。

最终 `baseCompile` 的返回值

```js
{
 	ast: ast,
 	render: code.render,
 	staticRenderFns: code.staticRenderFns
 }
```

最终返回了抽象语法树( ast )，渲染函数( render )，静态渲染函数( staticRenderFns )，且`render` 的值为`code.render `，`staticRenderFns` 的值为`code.staticRenderFns `，也就是说通过 `generate `处理 `ast `之后得到的返回值 `code` 是一个对象。


下面再给出模板编译内部具体流程图，便于理解。流程图如下：
![](~@/learn-vue-source-code/complie/3.png)

### 总结

本篇文章首先引出了为什么会有模板编译，因为有了模板编译，才有了虚拟`DOM`，才有了后续的视图更新。接着介绍了什么是模板编译，以及介绍了把用户所写的模板经过层层处理直到最终渲染的视图中这个整体的渲染流程；最后介绍了模板编译过程中所需要使用的抽象语法树的概念以及分析了模板编译的具体实施流程，其流程大致分为三个阶段，分别是模板解析阶段、优化阶段和代码生成阶段。那么接下来的几篇文章将会把这三个阶段逐一进行分析介绍。

## 4.2 模板解析阶段(整体运行流程)

### 整体流程

上篇文章中我们说了，在模板解析阶段主要做的工作是把用户在`<template></template>`标签内写的模板使用正则等方式解析成抽象语法树（`AST`）。而这一阶段在源码中对应解析器（`parser`）模块。

解析器，顾名思义，就是把用户所写的模板根据一定的解析规则解析出有效的信息，最后用这些信息形成`AST`。我们知道在`<template></template>`模板内，除了有常规的`HTML`标签外，用户还会一些文本信息以及在文本信息中包含过滤器。而这些不同的内容在解析起来肯定需要不同的解析规则，所以解析器不可能只有一个，它应该除了有解析常规`HTML`的HTML解析器，还应该有解析文本的文本解析器以及解析文本中如果包含过滤器的过滤器解析器。

另外，文本信息和标签属性信息却又是存在于HTML标签之内的，所以在解析整个模板的时候它的流程应该是这样子的：HTML解析器是主线，先用HTML解析器进行解析整个模板，在解析过程中如果碰到文本内容，那就调用文本解析器来解析文本，如果碰到文本中包含过滤器那就调用过滤器解析器来解析。如下图所示：

![](~@/learn-vue-source-code/complie/4.png)

### 回到源码

解析器的源码位于`/src/complier/parser`文件夹下，其主线代码如下：

```javascript
// 代码位置：/src/complier/parser/index.js

/**
 * Convert HTML string to AST.
 */
export function parse(template, options) {
   // ...
  parseHTML(template, {
    warn,
    expectHTML: options.expectHTML,
    isUnaryTag: options.isUnaryTag,
    canBeLeftOpenTag: options.canBeLeftOpenTag,
    shouldDecodeNewlines: options.shouldDecodeNewlines,
    shouldDecodeNewlinesForHref: options.shouldDecodeNewlinesForHref,
    shouldKeepComment: options.comments,
    start (tag, attrs, unary) {

    },
    end () {

    },
    chars (text: string) {

    },
    comment (text: string) {

    }
  })
  return root
}
```



从上面代码中可以看到，`parse` 函数就是解析器的主函数，在`parse` 函数内调用了`parseHTML` 函数对模板字符串进行解析，在`parseHTML` 函数解析模板字符串的过程中，如果遇到文本信息，就会调用文本解析器`parseText`函数进行文本解析；如果遇到文本中包含过滤器，就会调用过滤器解析器`parseFilters`函数进行解析。

### 总结

本篇文章主要梳理了模板解析的整体运行流程，模板解析其实就是根据被解析内容的特点使用正则等方式将有效信息解析提取出来，根据解析内容的不同分为HTML解析器，文本解析器和过滤器解析器。而文本信息与过滤器信息又存在于HTML标签中，所以在解析器主线函数`parse`中先调用HTML解析器`parseHTML` 函数对模板字符串进行解析，如果在解析过程中遇到文本或过滤器信息则再调用相应的解析器进行解析，最终完成对整个模板字符串的解析。

了解了模板解析阶段的整体运行流程后，接下来，我们就对流程中所涉及到的三种解析器分别深入分析，逐个击破。

## 4.3 模板解析阶段(HTML解析器)


### 前言

上篇文章中我们说到，在模板解析阶段主线函数`parse`中，根据要解析的内容不同会调用不同的解析器，

而在三个不同的解析器中最主要的当属`HTML`解析器，为什么这么说呢？因为`HTML`解析器主要负责解析出模板字符串中有哪些内容，然后根据不同的内容才能调用其他的解析器以及做相应的处理。那么本篇文章就来介绍一下`HTML`解析器是如何解析出模板字符串中包含的不同的内容的。

### HTML解析器内部运行流程

在源码中，`HTML`解析器就是`parseHTML`函数，在模板解析主线函数`parse`中调用了该函数，并传入两个参数，代码如下：

```javascript
// 代码位置：/src/complier/parser/index.js

/**
 * Convert HTML string to AST.
 * 将HTML模板字符串转化为AST
 */
export function parse(template, options) {
   // ...
  parseHTML(template, {
    warn,
    expectHTML: options.expectHTML,
    isUnaryTag: options.isUnaryTag,
    canBeLeftOpenTag: options.canBeLeftOpenTag,
    shouldDecodeNewlines: options.shouldDecodeNewlines,
    shouldDecodeNewlinesForHref: options.shouldDecodeNewlinesForHref,
    shouldKeepComment: options.comments,
    // 当解析到开始标签时，调用该函数
    start (tag, attrs, unary) {

    },
    // 当解析到结束标签时，调用该函数
    end () {

    },
    // 当解析到文本时，调用该函数
    chars (text) {

    },
    // 当解析到注释时，调用该函数
    comment (text) {

    }
  })
  return root
}
```

从代码中我们可以看到，调用`parseHTML`函数时为其传入的两个参数分别是：

- template:待转换的模板字符串；
- options:转换时所需的选项；

第一个参数是待转换的模板字符串，无需多言；重点看第二个参数，第二个参数提供了一些解析`HTML`模板时的一些参数，同时还定义了4个钩子函数。这4个钩子函数有什么作用呢？我们说了模板编译阶段主线函数`parse`会将`HTML`模板字符串转化成`AST`，而`parseHTML`是用来解析模板字符串的，把模板字符串中不同的内容出来之后，那么谁来把提取出来的内容生成对应的`AST`呢？答案就是这4个钩子函数。

把这4个钩子函数作为参数传给解析器`parseHTML`，当解析器解析出不同的内容时调用不同的钩子函数从而生成不同的`AST`。

- 当解析到开始标签时调用`start`函数生成元素类型的`AST`节点，代码如下；

  ```javascript
  // 当解析到标签的开始位置时，触发start
  start (tag, attrs, unary) {
  	let element = createASTElement(tag, attrs, currentParent)
  }

  export function createASTElement (tag,attrs,parent) {
    return {
      type: 1,
      tag,
      attrsList: attrs,
      attrsMap: makeAttrsMap(attrs),
      parent,
      children: []
    }
  }
  ```

  从上面代码中我们可以看到，`start`函数接收三个参数，分别是标签名`tag`、标签属性`attrs`、标签是否自闭合`unary`。当调用该钩子函数时，内部会调用`createASTElement`函数来创建元素类型的`AST`节点

- 当解析到结束标签时调用`end`函数；

- 当解析到文本时调用`chars`函数生成文本类型的`AST`节点；

  ```javascript
  // 当解析到标签的文本时，触发chars
  chars (text) {
  	if(text是带变量的动态文本){
      let element = {
        type: 2,
        expression: res.expression,
        tokens: res.tokens,
        text
      }
    } else {
      let element = {
        type: 3,
        text
      }
    }
  }
  ```

  当解析到标签的文本时，触发`chars`钩子函数，在该钩子函数内部，首先会判断文本是不是一个带变量的动态文本，如“hello {{name}}”。如果是动态文本，则创建动态文本类型的`AST`节点；如果不是动态文本，则创建纯静态文本类型的`AST`节点。

- 当解析到注释时调用`comment`函数生成注释类型的`AST`节点；

  ```javascript
  // 当解析到标签的注释时，触发comment
  comment (text: string) {
    let element = {
      type: 3,
      text,
      isComment: true
    }
  }
  ```

  当解析到标签的注释时，触发`comment`钩子函数，该钩子函数会创建一个注释类型的`AST`节点。

一边解析不同的内容一边调用对应的钩子函数生成对应的`AST`节点，最终完成将整个模板字符串转化成`AST`,这就是`HTML`解析器所要做的工作。

### 如何解析不同的内容

要从模板字符串中解析出不同的内容，那首先要知道模板字符串中都会包含哪些内容。那么通常我们所写的模板字符串中都会包含哪些内容呢？经过整理，通常模板内会包含如下内容：

- 文本，例如“难凉热血”
- HTML注释，例如\<!-- 我是注释 -->
- 条件注释，例如\<!-- [if !IE]> -->我是注释\<!--< ![endif]  -->
- DOCTYPE，例如\<!DOCTYPE html>
- 开始标签，例如\<div>
- 结束标签，例如\</div>

这几种内容都有其各自独有的特点，也就是说我们要根据不同内容所具有的不同的的特点通过编写不同的正则表达式将这些内容从模板字符串中一一解析出来，然后再把不同的内容做不同的处理。

下面，我们就来分别看一下`HTML`解析器是如何从模板字符串中将以上不同种类的内容进行解析出来。

####  解析HTML注释

解析注释比较简单，我们知道`HTML`注释是以`<!--`开头，以`-->`结尾，这两者中间的内容就是注释内容，那么我们只需用正则判断待解析的模板字符串`html`是否以`<!--`开头，若是，那就继续向后寻找`-->`，如果找到了，OK，注释就被解析出来了。代码如下：

```javascript
const comment = /^<!\--/
if (comment.test(html)) {
  // 若为注释，则继续查找是否存在'-->'
  const commentEnd = html.indexOf('-->')

  if (commentEnd >= 0) {
    // 若存在 '-->',继续判断options中是否保留注释
    if (options.shouldKeepComment) {
      // 若保留注释，则把注释截取出来传给options.comment，创建注释类型的AST节点
      options.comment(html.substring(4, commentEnd))
    }
    // 若不保留注释，则将游标移动到'-->'之后，继续向后解析
    advance(commentEnd + 3)
    continue
  }
}
```

在上面代码中，如果模板字符串`html`符合注释开始的正则，那么就继续向后查找是否存在`-->`，若存在，则把`html`从第4位（"\<!--"长度为4）开始截取，直到`-->`处，截取得到的内容就是注释的真实内容，然后调用4个钩子函数中的`comment`函数，将真实的注释内容传进去，创建注释类型的`AST`节点。

上面代码中有一处值得注意的地方，那就是我们平常在模板中可以在`<template></template>`标签上配置`comments`选项来决定在渲染模板时是否保留注释，对应到上面代码中就是`options.shouldKeepComment`,如果用户配置了`comments`选项为`true`，则`shouldKeepComment`为`true`，则创建注释类型的`AST`节点，如不保留注释，则将游标移动到'-->'之后，继续向后解析。

`advance`函数是用来移动解析游标的，解析完一部分就把游标向后移动一部分，确保不会重复解析，其代码如下：

```javascript
function advance (n) {
  index += n   // index为解析游标
  html = html.substring(n)
}
```
为了更加直观地说明 `advance` 的作用，请看下图：
![](~@/learn-vue-source-code/complie/5.png)

调用 `advance` 函数：

```js
advance(3)
```

得到结果：

![](~@/learn-vue-source-code/complie/6.png)

从图中可以看到，解析游标`index`最开始在模板字符串的位置0处，当调用了`advance(3)`之后，解析游标到了位置3处，每次解析完一段内容就将游标向后移动一段，接着再从解析游标往后解析，这样就保证了解析过的内容不会被重复解析。

####  解析条件注释

解析条件注释也比较简单，其原理跟解析注释相同，都是先用正则判断是否是以条件注释特有的开头标识开始，然后寻找其特有的结束标识，若找到，则说明是条件注释，将其截取出来即可，由于条件注释不存在于真正的`DOM`树中，所以不需要调用钩子函数创建`AST`节点。代码如下：

```javascript
// 解析是否是条件注释
const conditionalComment = /^<!\[/
if (conditionalComment.test(html)) {
  // 若为条件注释，则继续查找是否存在']>'
  const conditionalEnd = html.indexOf(']>')

  if (conditionalEnd >= 0) {
    // 若存在 ']>',则从原本的html字符串中把条件注释截掉，
    // 把剩下的内容重新赋给html，继续向后匹配
    advance(conditionalEnd + 2)
    continue
  }
}
```

####  解析DOCTYPE

解析`DOCTYPE`的原理同解析条件注释完全相同，此处不再赘述，代码如下：

```javascript
const doctype = /^<!DOCTYPE [^>]+>/i
// 解析是否是DOCTYPE
const doctypeMatch = html.match(doctype)
if (doctypeMatch) {
  advance(doctypeMatch[0].length)
  continue
}
```

####  解析开始标签

相较于前三种内容的解析，解析开始标签会稍微复杂一点，但是万变不离其宗，它的原理还是相通的，都是使用正则去匹配提取。

首先使用开始标签的正则去匹配模板字符串，看模板字符串是否具有开始标签的特征，如下：

```javascript
/**
 * 匹配开始标签的正则
 */
const ncname = '[a-zA-Z_][\\w\\-\\.]*'
const qnameCapture = `((?:${ncname}\\:)?${ncname})`
const startTagOpen = new RegExp(`^<${qnameCapture}`)

const start = html.match(startTagOpen)
if (start) {
  const match = {
    tagName: start[1],
    attrs: [],
    start: index
  }
}

// 以开始标签开始的模板：
'<div></div>'.match(startTagOpen)  => ['<div','div',index:0,input:'<div></div>']
// 以结束标签开始的模板：
'</div><div></div>'.match(startTagOpen) => null
// 以文本开始的模板：
'我是文本</p>'.match(startTagOpen) => null
```

在上面代码中，我们用不同类型的内容去匹配开始标签的正则，发现只有`<div></div>`的字符串可以正确匹配，并且返回一个数组。

在前文中我们说到，当解析到开始标签时，会调用4个钩子函数中的`start`函数，而`start`函数需要传递3个参数，分别是标签名`tag`、标签属性`attrs`、标签是否自闭合`unary`。标签名通过正则匹配的结果就可以拿到，即上面代码中的`start[1]`，而标签属性`attrs`以及标签是否自闭合`unary`需要进一步解析。

1. 解析标签属性

   我们知道，标签属性一般是写在开始标签的标签名之后的，如下：

   ```html
   <div class="a" id="b"></div>
   ```

   另外，我们在上面匹配是否是开始标签的正则中已经可以拿到开始标签的标签名，即上面代码中的`start[0]`，那么我们可以将这一部分先从模板字符串中截掉，则剩下的部分如下：

   ```html
    class="a" id="b"></div>
   ```

   那么我们只需用剩下的这部分去匹配标签属性的正则，就可以将标签属性提取出来了，如下：

   ```javascript
   const attribute = /^\s*([^\s"'<>\/=]+)(?:\s*(=)\s*(?:"([^"]*)"+|'([^']*)'+|([^\s"'=<>`]+)))?/
   let html = 'class="a" id="b"></div>'
   let attr = html.match(attribute)
   console.log(attr)
   // ["class="a"", "class", "=", "a", undefined, undefined, index: 0, input: "class="a" id="b"></div>", groups: undefined]
   ```

   可以看到，第一个标签属性`class="a"`已经被拿到了。另外，标签属性有可能有多个也有可能没有，如果没有的话那好办，匹配标签属性的正则就会匹配失败，标签属性就为空数组；而如果标签属性有多个的话，那就需要循环匹配了，匹配出第一个标签属性后，就把该属性截掉，用剩下的字符串继续匹配，直到不再满足正则为止，代码如下：

   ```javascript
   const attribute = /^\s*([^\s"'<>\/=]+)(?:\s*(=)\s*(?:"([^"]*)"+|'([^']*)'+|([^\s"'=<>`]+)))?/
   const startTagClose = /^\s*(\/?)>/
   const match = {
    tagName: start[1],
    attrs: [],
    start: index
   }
   while (!(end = html.match(startTagClose)) && (attr = html.match(attribute))) {
    advance(attr[0].length)
    match.attrs.push(attr)
   }
   ```

   在上面代码的`while`循环中，如果剩下的字符串不符合开始标签的结束特征（startTagClose）并且符合标签属性的特征的话，那就说明还有未提取出的标签属性，那就进入循环，继续提取，直到把所有标签属性都提取完毕。

   所谓不符合开始标签的结束特征是指当前剩下的字符串不是以开始标签结束符开头的，我们知道一个开始标签的结束符有可能是一个`>`（非自闭合标签），也有可能是`/>`（自闭合标签），如果剩下的字符串（如`></div>`）以开始标签的结束符开头，那么就表示标签属性已经被提取完毕了。



2. 解析标签是否是自闭合

   在`HTML`中，有自闭合标签（如`<img src=""/>`）也有非自闭合标签（如`<div></div>`），这两种类型的标签在创建`AST`节点是处理方式是有区别的，所以我们需要解析出当前标签是否是自闭合标签。

   解析的方式很简单，我们知道，经过标签属性提取之后，那么剩下的字符串无非就两种，如下：

   ```html
   <!--非自闭合标签-->
   ></div>
   ```

   或

   ```html
   <!--自闭合标签-->
   />
   ```

   所以我们可以用剩下的字符串去匹配开始标签结束符正则，如下：

   ```javascript
   const startTagClose = /^\s*(\/?)>/
   let end = html.match(startTagClose)
   '></div>'.match(startTagClose) // [">", "", index: 0, input: "></div>", groups: undefined]
   '/>'.match(startTagClose) // ["/>", "/", index: 0, input: "/><div></div>", groups: undefined]
   ```

   可以看到，非自闭合标签匹配结果中的`end[1]`为`""`，而自闭合标签匹配结果中的`end[1]`为`"/"`。所以根据匹配结果的`end[1]`是否是`""`我们即可判断出当前标签是否为自闭合标签，源码如下：

   ```javascript
   const startTagClose = /^\s*(\/?)>/
   let end = html.match(startTagClose)
   if (end) {
    match.unarySlash = end[1]
    advance(end[0].length)
    match.end = index
    return match
   }
   ```

经过以上两步，开始标签就已经解析完毕了，完整源码如下：

```javascript
const ncname = '[a-zA-Z_][\\w\\-\\.]*'
const qnameCapture = `((?:${ncname}\\:)?${ncname})`
const startTagOpen = new RegExp(`^<${qnameCapture}`)
const startTagClose = /^\s*(\/?)>/


function parseStartTag () {
  const start = html.match(startTagOpen)
  // '<div></div>'.match(startTagOpen)  => ['<div','div',index:0,input:'<div></div>']
  if (start) {
    const match = {
      tagName: start[1],
      attrs: [],
      start: index
    }
    advance(start[0].length)
    let end, attr
    /**
     * <div a=1 b=2 c=3></div>
     * 从<div之后到开始标签的结束符号'>'之前，一直匹配属性attrs
     * 所有属性匹配完之后，html字符串还剩下
     * 自闭合标签剩下：'/>'
     * 非自闭合标签剩下：'></div>'
     */
    while (!(end = html.match(startTagClose)) && (attr = html.match(attribute))) {
      advance(attr[0].length)
      match.attrs.push(attr)
    }

    /**
     * 这里判断了该标签是否为自闭合标签
     * 自闭合标签如:<input type='text' />
     * 非自闭合标签如:<div></div>
     * '></div>'.match(startTagClose) => [">", "", index: 0, input: "></div>", groups: undefined]
     * '/><div></div>'.match(startTagClose) => ["/>", "/", index: 0, input: "/><div></div>", groups: undefined]
     * 因此，我们可以通过end[1]是否是"/"来判断该标签是否是自闭合标签
     */
    if (end) {
      match.unarySlash = end[1]
      advance(end[0].length)
      match.end = index
      return match
    }
  }
}
```

通过源码可以看到，调用`parseStartTag`函数，如果模板字符串符合开始标签的特征，则解析开始标签，并将解析结果返回，如果不符合开始标签的特征，则返回`undefined`。

解析完毕后，就可以用解析得到的结果去调用`start`钩子函数去创建元素型的`AST`节点了。

在源码中，`Vue`并没有直接去调`start`钩子函数去创建`AST`节点，而是调用了`handleStartTag`函数，在该函数内部才去调的`start`钩子函数，为什么要这样做呢？这是因为虽然经过`parseStartTag`函数已经把创建`AST`节点必要信息提取出来了，但是提取出来的标签属性数组还是需要处理一下，下面我们就来看一下`handleStartTag`函数都做了些什么事。`handleStartTag`函数源码如下：

```javascript
function handleStartTag (match) {
    const tagName = match.tagName
    const unarySlash = match.unarySlash

    if (expectHTML) {
      // ...
    }

    const unary = isUnaryTag(tagName) || !!unarySlash

    const l = match.attrs.length
    const attrs = new Array(l)
    for (let i = 0; i < l; i++) {
      const args = match.attrs[i]
      const value = args[3] || args[4] || args[5] || ''
      const shouldDecodeNewlines = tagName === 'a' && args[1] === 'href'
        ? options.shouldDecodeNewlinesForHref
        : options.shouldDecodeNewlines
      attrs[i] = {
        name: args[1],
        value: decodeAttr(value, shouldDecodeNewlines)
      }
    }

    if (!unary) {
      stack.push({ tag: tagName, lowerCasedTag: tagName.toLowerCase(), attrs: attrs })
      lastTag = tagName
    }

    if (options.start) {
      options.start(tagName, attrs, unary, match.start, match.end)
    }
  }

```

 `handleStartTag`函数用来对`parseStartTag`函数的解析结果进行进一步处理，它接收`parseStartTag`函数的返回值作为参数。

`handleStartTag`函数的开始定义几个常量：

```javascript
const tagName = match.tagName       // 开始标签的标签名
const unarySlash = match.unarySlash  // 是否为自闭合标签的标志，自闭合为"",非自闭合为"/"
const unary = isUnaryTag(tagName) || !!unarySlash  // 布尔值，标志是否为自闭合标签
const l = match.attrs.length    // match.attrs 数组的长度
const attrs = new Array(l)  // 一个与match.attrs数组长度相等的数组
```

接下来是循环处理提取出来的标签属性数组`match.attrs`，如下：

```javascript
for (let i = 0; i < l; i++) {
    const args = match.attrs[i]
    const value = args[3] || args[4] || args[5] || ''
    const shouldDecodeNewlines = tagName === 'a' && args[1] === 'href'
    ? options.shouldDecodeNewlinesForHref
    : options.shouldDecodeNewlines
    attrs[i] = {
        name: args[1],
        value: decodeAttr(value, shouldDecodeNewlines)
    }
}
```

 上面代码中，首先定义了 `args `常量，它是解析出来的标签属性数组中的每一个属性对象，即`match.attrs` 数组中每个元素对象。 它长这样：

```javascript
const args = ["class="a"", "class", "=", "a", undefined, undefined, index: 0, input: "class="a" id="b"></div>", groups: undefined]
```

接着定义了`value`，用于存储标签属性的属性值，我们可以看到，在代码中尝试取`args`的`args[3]`、`args[4]`、`args[5]`，如果都取不到，则给`value`复制为空

```javascript
const value = args[3] || args[4] || args[5] || ''
```



接着定义了`shouldDecodeNewlines`，这个常量主要是做一些兼容性处理， 如果 `shouldDecodeNewlines` 为 `true`，意味着 `Vue` 在编译模板的时候，要对属性值中的换行符或制表符做兼容处理。而`shouldDecodeNewlinesForHref`为`true` 意味着`Vue`在编译模板的时候，要对`a`标签的 `href `属性值中的换行符或制表符做兼容处理。

```javascript
const shouldDecodeNewlines = tagName === 'a' && args[1] === 'href'
    ? options.shouldDecodeNewlinesForHref
    : options.shouldDecodeNewlinesconst value = args[3] || args[4] || args[5] || ''
```

最后将处理好的结果存入之前定义好的与`match.attrs`数组长度相等的`attrs`数组中，如下：

```javascript
attrs[i] = {
    name: args[1],    // 标签属性的属性名，如class
    value: decodeAttr(value, shouldDecodeNewlines) // 标签属性的属性值，如class对应的a
}
```

最后，如果该标签是非自闭合标签，则将标签推入栈中（关于栈这个概念后面会说到），如下：

```javascript
if (!unary) {
    stack.push({ tag: tagName, lowerCasedTag: tagName.toLowerCase(), attrs: attrs })
    lastTag = tagName
}
```

如果该标签是自闭合标签，现在就可以调用`start`钩子函数并传入处理好的参数来创建`AST`节点了，如下：

```javascript
if (options.start) {
    options.start(tagName, attrs, unary, match.start, match.end)
}
```

以上就是开始标签的解析以及调用`start`钩子函数创建元素型的`AST`节点的所有过程。

####  解析结束标签

结束标签的解析要比解析开始标签容易多了，因为它不需要解析什么属性，只需要判断剩下的模板字符串是否符合结束标签的特征，如果是，就将结束标签名提取出来，再调用4个钩子函数中的`end`函数就好了。

首先判断剩余的模板字符串是否符合结束标签的特征，如下：

```javascript
const ncname = '[a-zA-Z_][\\w\\-\\.]*'
const qnameCapture = `((?:${ncname}\\:)?${ncname})`
const endTag = new RegExp(`^<\\/${qnameCapture}[^>]*>`)
const endTagMatch = html.match(endTag)

'</div>'.match(endTag)  // ["</div>", "div", index: 0, input: "</div>", groups: undefined]
'<div>'.match(endTag)  // null
```

上面代码中，如果模板字符串符合结束标签的特征，则会获得匹配结果数组；如果不合符，则得到null。

接着再调用`end`钩子函数，如下：

```javascript
if (endTagMatch) {
    const curIndex = index
    advance(endTagMatch[0].length)
    parseEndTag(endTagMatch[1], curIndex, index)
    continue
}
```

在上面代码中，没有直接去调用`end`函数，而是调用了`parseEndTag`函数，关于`parseEndTag`函数内部的作用我们后面会介绍到，在这里你暂时可以理解为该函数内部就是去调用了`end`钩子函数。

####  解析文本

```
终于到了解析最后一种文本类型的内容了，为什么要把解析文本类型放在最后一个介绍呢？我们仔细想一下，前面五种类型都是以`<`开头的，只有文本类型的内容不是以`<`开头的，所以我们在解析模板字符串的时候可以先判断一下字符串是不是以`<`开头的，如果是则继续判断是以上五种类型的具体哪一种，而如果不是的话，那它肯定就是文本了。
```

解析文本也比较容易，在解析模板字符串之前，我们先查找一下第一个`<`出现在什么位置，如果第一个`<`在第一个位置，那么说明模板字符串是以其它5种类型开始的；如果第一个`<`不在第一个位置而在模板字符串中间某个位置，那么说明模板字符串是以文本开头的，那么从开头到第一个`<`出现的位置就都是文本内容了；如果在整个模板字符串里没有找到`<`，那说明整个模板字符串都是文本。这就是解析思路，接下来我们对照源码来了解一下实际的解析过程，源码如下：

```javascript
let textEnd = html.indexOf('<')
// '<' 在第一个位置，为其余5种类型
if (textEnd === 0) {
    // ...
}
// '<' 不在第一个位置，文本开头
if (textEnd >= 0) {
    // 如果html字符串不是以'<'开头,说明'<'前面的都是纯文本，无需处理
    // 那就把'<'以后的内容拿出来赋给rest
    rest = html.slice(textEnd)
    while (
        !endTag.test(rest) &&
        !startTagOpen.test(rest) &&
        !comment.test(rest) &&
        !conditionalComment.test(rest)
    ) {
        // < in plain text, be forgiving and treat it as text
        /**
           * 用'<'以后的内容rest去匹配endTag、startTagOpen、comment、conditionalComment
           * 如果都匹配不上，表示'<'是属于文本本身的内容
           */
        // 在'<'之后查找是否还有'<'
        next = rest.indexOf('<', 1)
        // 如果没有了，表示'<'后面也是文本
        if (next < 0) break
        // 如果还有，表示'<'是文本中的一个字符
        textEnd += next
        // 那就把next之后的内容截出来继续下一轮循环匹配
        rest = html.slice(textEnd)
    }
    // '<'是结束标签的开始 ,说明从开始到'<'都是文本，截取出来
    text = html.substring(0, textEnd)
    advance(textEnd)
}
// 整个模板字符串里没有找到`<`,说明整个模板字符串都是文本
if (textEnd < 0) {
    text = html
    html = ''
}
// 把截取出来的text转化成textAST
if (options.chars && text) {
    options.chars(text)
}
```

源码的逻辑很清晰，根据`<`在不在第一个位置以及整个模板字符串里没有`<`都分别进行了处理。

值得深究的是如果`<`不在第一个位置而在模板字符串中间某个位置，那么说明模板字符串是以文本开头的，那么从开头到第一个`<`出现的位置就都是文本内容了，接着我们还要从第一个`<`的位置继续向后判断，因为还存在这样一种情况，那就是如果文本里面本来就包含一个`<`，例如`1<2</div>`。为了处理这种情况，我们把从第一个`<`的位置直到模板字符串结束都截取出来记作`rest`，如下：

```javascript
 let rest = html.slice(textEnd)
```

接着用`rest`去匹配以上5种类型的正则，如果都匹配不上，则表明这个`<`是属于文本本身的内容，如下：

```javascript
while (
    !endTag.test(rest) &&
    !startTagOpen.test(rest) &&
    !comment.test(rest) &&
    !conditionalComment.test(rest)
) {

}
```

如果都匹配不上，则表明这个`<`是属于文本本身的内容，接着以这个`<`的位置继续向后查找，看是否还有`<`，如果没有了，则表示后面的都是文本；如果后面还有下一个`<`，那表明至少在这个`<`到下一个`<`中间的内容都是文本，至于下一个`<`以后的内容是什么，则还需要重复以上的逻辑继续判断。代码如下：

```javascript
while (
    !endTag.test(rest) &&
    !startTagOpen.test(rest) &&
    !comment.test(rest) &&
    !conditionalComment.test(rest)
) {
    // < in plain text, be forgiving and treat it as text
    /**
    * 用'<'以后的内容rest去匹配endTag、startTagOpen、comment、conditionalComment
    * 如果都匹配不上，表示'<'是属于文本本身的内容
    */
    // 在'<'之后查找是否还有'<'
    next = rest.indexOf('<', 1)
    // 如果没有了，表示'<'后面也是文本
    if (next < 0) break
    // 如果还有，表示'<'是文本中的一个字符
    textEnd += next
    // 那就把next之后的内容截出来继续下一轮循环匹配
    rest = html.slice(textEnd)
}
```

最后截取文本内容`text`并调用4个钩子函数中的`chars`函数创建文本型的`AST`节点。

### 如何保证AST节点层级关系

上一章节我们介绍了`HTML`解析器是如何解析各种不同类型的内容并且调用钩子函数创建不同类型的`AST`节点。此时你可能会有个疑问，我们上面创建的`AST`节点都是单独创建且分散的，而真正的`DOM`节点都是有层级关系的，那如何来保证`AST`节点的层级关系与真正的`DOM`节点相同呢？

关于这个问题，`Vue`也注意到了。`Vue`在`HTML`解析器的开头定义了一个栈`stack`，这个栈的作用就是用来维护`AST`节点层级的，那么它是怎么维护的呢？通过前文我们知道，`HTML`解析器在从前向后解析模板字符串时，每当遇到开始标签时就会调用`start`钩子函数，那么在`start`钩子函数内部我们可以将解析得到的开始标签推入栈中，而每当遇到结束标签时就会调用`end`钩子函数，那么我们也可以在`end`钩子函数内部将解析得到的结束标签所对应的开始标签从栈中弹出。请看如下例子：

加入有如下模板字符串：

```html
<div><p><span></span></p></div>
```

当解析到开始标签`<div>`时，就把`div`推入栈中，然后继续解析，当解析到`<p>`时，再把`p`推入栈中，同理，再把`span`推入栈中，当解析到结束标签`</span>`时，此时栈顶的标签刚好是`span`的开始标签，那么就用`span`的开始标签和结束标签构建`AST`节点，并且从栈中把`span`的开始标签弹出，那么此时栈中的栈顶标签`p`就是构建好的`span`的`AST`节点的父节点，如下图：

![](~@/learn-vue-source-code/complie/7.png)


这样我们就找到了当前被构建节点的父节点。这只是栈的一个用途，它还有另外一个用途，我们再看如下模板字符串：

```html
<div><p><span></p></div>
```

按照上面的流程解析这个模板字符串时，当解析到结束标签`</p>`时，此时栈顶的标签应该是`p`才对，而现在是`span`，那么就说明`span`标签没有被正确闭合，此时控制台就会抛出警告：‘tag  has no matching end tag.’相信这个警告你一定不会陌生。这就是栈的第二个用途： 检测模板字符串中是否有未正确闭合的标签。

OK，有了这个栈的概念之后，我们再回看上一章`HTML`解析器解析不同内容的代码。

### 回归源码

####  HTML解析器源码

以上内容都了解了之后，我们回归源码，逐句分析`HTML`解析器`parseHTML`函数，函数定义如下：

```javascript
function parseHTML(html, options) {
	var stack = [];
	var expectHTML = options.expectHTML;
	var isUnaryTag$$1 = options.isUnaryTag || no;
	var canBeLeftOpenTag$$1 = options.canBeLeftOpenTag || no;
	var index = 0;
	var last, lastTag;

	// 开启一个 while 循环，循环结束的条件是 html 为空，即 html 被 parse 完毕
	while (html) {
		last = html;
		// 确保即将 parse 的内容不是在纯文本标签里 (script,style,textarea)
		if (!lastTag || !isPlainTextElement(lastTag)) {
		   let textEnd = html.indexOf('<')
              /**
               * 如果html字符串是以'<'开头,则有以下几种可能
               * 开始标签:<div>
               * 结束标签:</div>
               * 注释:<!-- 我是注释 -->
               * 条件注释:<!-- [if !IE] --> <!-- [endif] -->
               * DOCTYPE:<!DOCTYPE html>
               * 需要一一去匹配尝试
               */
            if (textEnd === 0) {
                // 解析是否是注释
        		if (comment.test(html)) {

                }
                // 解析是否是条件注释
                if (conditionalComment.test(html)) {

                }
                // 解析是否是DOCTYPE
                const doctypeMatch = html.match(doctype)
                if (doctypeMatch) {

                }
                // 解析是否是结束标签
                const endTagMatch = html.match(endTag)
                if (endTagMatch) {

                }
                // 匹配是否是开始标签
                const startTagMatch = parseStartTag()
                if (startTagMatch) {

                }
            }
            // 如果html字符串不是以'<'开头,则解析文本类型
            let text, rest, next
            if (textEnd >= 0) {

            }
            // 如果在html字符串中没有找到'<'，表示这一段html字符串都是纯文本
            if (textEnd < 0) {
                text = html
                html = ''
            }
            // 把截取出来的text转化成textAST
            if (options.chars && text) {
                options.chars(text)
            }
		} else {
			// 父元素为script、style、textarea时，其内部的内容全部当做纯文本处理
		}

		//将整个字符串作为文本对待
		if (html === last) {
			options.chars && options.chars(html);
			if (!stack.length && options.warn) {
				options.warn(("Mal-formatted tag at end of template: \"" + html + "\""));
			}
			break
		}
	}

	// Clean up any remaining tags
	parseEndTag();
	//parse 开始标签
	function parseStartTag() {

	}
	//处理 parseStartTag 的结果
	function handleStartTag(match) {

	}
	//parse 结束标签
	function parseEndTag(tagName, start, end) {

	}
}
```

上述代码中大致可分为三部分：

- 定义的一些常量和变量
- while 循环
- 解析过程中用到的辅助函数

我们一一来分析：

首先定义了几个常量，如下

```javascript
const stack = []       // 维护AST节点层级的栈
const expectHTML = options.expectHTML
const isUnaryTag = options.isUnaryTag || no
const canBeLeftOpenTag = options.canBeLeftOpenTag || no   //用来检测一个标签是否是可以省略闭合标签的非自闭合标签
let index = 0   //解析游标，标识当前从何处开始解析模板字符串
let last,   // 存储剩余还未解析的模板字符串
    lastTag  // 存储着位于 stack 栈顶的元素
```

 接着开启` while` 循环，循环的终止条件是 模板字符串`html `为空，即模板字符串被全部编译完毕。在每次`while`循环中， 先把 ` html `的值赋给变量 `last  `，如下：

```javascript
last = html
```

这样做的目的是，如果经过上述所有处理逻辑处理过后，`html`字符串没有任何变化，即表示`html`字符串没有匹配上任何一条规则，那么就把`html`字符串当作纯文本对待，创建文本类型的`AST`节点并且如果抛出异常：模板字符串中标签格式有误。如下：

```javascript
//将整个字符串作为文本对待
if (html === last) {
    options.chars && options.chars(html);
    if (!stack.length && options.warn) {
        options.warn(("Mal-formatted tag at end of template: \"" + html + "\""));
    }
    break
}
```

接着，我们继续看`while`循环体内的代码：

```javascript
while (html) {
  // 确保即将 parse 的内容不是在纯文本标签里 (script,style,textarea)
  if (!lastTag || !isPlainTextElement(lastTag)) {

  } else {
    // parse 的内容是在纯文本标签里 (script,style,textarea)
  }
}
```

在循环体内，首先判断了待解析的`html`字符串是否在纯文本标签里，如`script`,`style`,`textarea`，因为在这三个标签里的内容肯定不会有`HTML`标签，所以我们可直接当作文本处理，判断条件如下：

```javascript
!lastTag || !isPlainTextElement(lastTag)
```

 前面我们说了，`lastTag`为栈顶元素，`!lastTag`即表示当前`html`字符串没有父节点，而`isPlainTextElement(lastTag)` 是检测 `lastTag` 是否为是那三个纯文本标签之一，是的话返回`true`，不是返回`fasle`。

也就是说当前`html`字符串要么没有父节点要么父节点不是纯文本标签，则接下来就可以依次解析那6种类型的内容了，关于6种类型内容的处理方式前文已经逐个介绍过，此处不再重复。

####  parseEndTag函数源码

接下来我们看一下之前在解析结束标签时遗留的`parseEndTag`函数，该函数定义如下：

```javascript
function parseEndTag (tagName, start, end) {
    let pos, lowerCasedTagName
    if (start == null) start = index
    if (end == null) end = index

    if (tagName) {
      lowerCasedTagName = tagName.toLowerCase()
    }

    // Find the closest opened tag of the same type
    if (tagName) {
      for (pos = stack.length - 1; pos >= 0; pos--) {
        if (stack[pos].lowerCasedTag === lowerCasedTagName) {
          break
        }
      }
    } else {
      // If no tag name is provided, clean shop
      pos = 0
    }

    if (pos >= 0) {
      // Close all the open elements, up the stack
      for (let i = stack.length - 1; i >= pos; i--) {
        if (process.env.NODE_ENV !== 'production' &&
          (i > pos || !tagName) &&
          options.warn
        ) {
          options.warn(
            `tag <${stack[i].tag}> has no matching end tag.`
          )
        }
        if (options.end) {
          options.end(stack[i].tag, start, end)
        }
      }

      // Remove the open elements from the stack
      stack.length = pos
      lastTag = pos && stack[pos - 1].tag
    } else if (lowerCasedTagName === 'br') {
      if (options.start) {
        options.start(tagName, [], true, start, end)
      }
    } else if (lowerCasedTagName === 'p') {
      if (options.start) {
        options.start(tagName, [], false, start, end)
      }
      if (options.end) {
        options.end(tagName, start, end)
      }
    }
  }
}
```

该函数接收三个参数，分别是结束标签名`tagName`、结束标签在`html`字符串中的起始和结束位置`start`和`end`。

这三个参数其实都是可选的，根据传参的不同其功能也不同。

- 第一种是三个参数都传递，用于处理普通的结束标签
- 第二种是只传递`tagName`
- 第三种是三个参数都不传递，用于处理栈中剩余未处理的标签

如果`tagName`存在，那么就从后往前遍历栈，在栈中寻找与`tagName`相同的标签并记录其所在的位置`pos`，如果`tagName`不存在，则将`pos`置为0。如下：

```javascript
if (tagName) {
    for (pos = stack.length - 1; pos >= 0; pos--) {
        if (stack[pos].lowerCasedTag === lowerCasedTagName) {
            break
        }
    }
} else {
    // If no tag name is provided, clean shop
    pos = 0
}
```

接着当`pos>=0`时，开启一个`for`循环，从栈顶位置从后向前遍历直到`pos`处，如果发现`stack`栈中存在索引大于` pos `的元素，那么该元素一定是缺少闭合标签的。这是因为在正常情况下，`stack`栈的栈顶元素应该和当前的结束标签`tagName` 匹配，也就是说正常的`pos`应该是栈顶位置，后面不应该再有元素，如果后面还有元素，那么后面的元素就都缺少闭合标签 那么这个时候如果是在非生产环境会抛出警告，告诉你缺少闭合标签。除此之外，还会调用 `options.end(stack[i].tag, start, end) `立即将其闭合，这是为了保证解析结果的正确性。

```javascript
if (pos >= 0) {
	// Close all the open elements, up the stack
	for (var i = stack.length - 1; i >= pos; i--) {
		if (i > pos || !tagName ) {
			options.warn(
				("tag <" + (stack[i].tag) + "> has no matching end tag.")
			);
		}
		if (options.end) {
			options.end(stack[i].tag, start, end);
		}
	}

	// Remove the open elements from the stack
	stack.length = pos;
	lastTag = pos && stack[pos - 1].tag;
}
```

最后把`pos`位置以后的元素都从`stack`栈中弹出，以及把` lastTag`更新为栈顶元素:

```js
stack.length = pos;
lastTag = pos && stack[pos - 1].tag;
```

接着，如果`pos`没有大于等于0，即当 `tagName` 没有在 `stack` 栈中找到对应的开始标签时，`pos` 为 -1 。那么此时再判断 `tagName` 是否为`br` 或`p`标签，为什么要单独判断这两个标签呢？这是因为在浏览器中如果我们写了如下`HTML`：

```html
<div>
    </br>
    </p>
</div>
```

浏览器会自动把`</br>`标签解析为正常的 \<br>标签，而对于`</p>`浏览器则自动将其补全为`<p></p>`，所以`Vue`为了与浏览器对这两个标签的行为保持一致，故对这两个便签单独判断处理，如下：

```javascript
if (lowerCasedTagName === 'br') {
    if (options.start) {
        options.start(tagName, [], true, start, end)  // 创建<br>AST节点
    }
}
// 补全p标签并创建AST节点
if (lowerCasedTagName === 'p') {
    if (options.start) {
        options.start(tagName, [], false, start, end)
    }
    if (options.end) {
        options.end(tagName, start, end)
    }
}
```

以上就是对结束标签的解析与处理。

另外，在`while`循环后面还有一行代码：

```javascript
parseEndTag()
```

这行代码执行的时机是`html === last`，即`html`字符串中的标签格式有误时会跳出`while`循环，此时就会执行这行代码，这行代码是调用`parseEndTag`函数并不传递任何参数，前面我们说过如果`parseEndTag`函数不传递任何参数是用于处理栈中剩余未处理的标签。这是因为如果不传递任何函数，此时`parseEndTag`函数里的`pos`就为0，那么`pos>=0`就会恒成立，那么就会逐个警告缺少闭合标签，并调用 `options.end `将其闭合。

### 总结

本篇文章主要介绍了`HTML`解析器的工作流程以及工作原理，文章比较长，但是逻辑并不复杂。

首先介绍了`HTML`解析器的工作流程，一句话概括就是：一边解析不同的内容一边调用对应的钩子函数生成对应的`AST`节点，最终完成将整个模板字符串转化成`AST`。

接着介绍了`HTML`解析器是如何解析用户所写的模板字符串中各种类型的内容的，把各种类型的解析方式都分别进行了介绍。

其次，介绍了在解析器内维护了一个栈，用来保证构建的`AST`节点层级与真正`DOM`层级一致。

了解了思想之后，最后回归源码，学习了源码中一些处理细节的地方。

## 4.4 模板解析阶段(文本解析器)

### 前言

在上篇文章中我们说了，当`HTML`解析器解析到文本内容时会调用4个钩子函数中的`chars`函数来创建文本型的`AST`节点，并且也说了在`chars`函数中会根据文本内容是否包含变量再细分为创建含有变量的`AST`节点和不包含变量的`AST`节点，如下：

```javascript
// 当解析到标签的文本时，触发chars
chars (text) {
  if(res = parseText(text)){
       let element = {
           type: 2,
           expression: res.expression,
           tokens: res.tokens,
           text
       }
    } else {
       let element = {
           type: 3,
           text
       }
    }
}
```

从上面代码中可以看到，创建含有变量的`AST`节点时节点的`type`属性为2，并且相较于不包含变量的`AST`节点多了两个属性：`expression`和`tokens`。那么如何来判断文本里面是否包含变量以及多的那两个属性是什么呢？这就涉及到文本解析器了，当`Vue`用`HTML`解析器解析出文本时，再将解析出来的文本内容传给文本解析器，最后由文本解析器解析该段文本里面是否包含变量以及如果包含变量时再解析`expression`和`tokens`。那么接下来，本篇文章就来分析一下文本解析器都干了些什么。

### 结果分析

研究文本解析器内部原理之前，我们先来看一下由`HTML`解析器解析得到的文本内容经过文本解析器后输出的结果是什么样子的，这样对我们后面分析文本解析器内部原理会有很大的帮助。

从上面`chars`函数的代码中可以看到，把`HTML`解析器解析得到的文本内容`text`传给文本解析器`parseText`函数，根据`parseText`函数是否有返回值判断该文本是否包含变量，以及从返回值中取到需要的`expression`和`tokens`。那么我们就先来看一下`parseText`函数如果有返回值，那么它的返回值是什么样子的。

假设现有由`HTML`解析器解析得到的文本内容如下：

```javascript
let text = "我叫{{name}}，我今年{{age}}岁了"
```

经过文本解析器解析后得到：

```javascript
let res = parseText(text)
res = {
    expression:"我叫"+_s(name)+"，我今年"+_s(age)+"岁了",
    tokens:[
        "我叫",
        {'@binding': name },
        "，我今年"
        {'@binding': age },
    	"岁了"
    ]
}
```

  从上面的结果中我们可以看到，`expression`属性就是把文本中的变量和非变量提取出来，然后把变量用`_s()`包裹，最后按照文本里的顺序把它们用`+`连接起来。而`tokens`是个数组，数组内容也是文本中的变量和非变量，不一样的是把变量构造成`{'@binding': xxx}`。

那么这样做有什么用呢？这主要是为了给后面代码生成阶段的生成`render`函数时用的，这个我们在后面介绍代码生成阶段是会详细说明，此处暂可理解为单纯的在构造形式。

OK，现在我们就可以知道文本解析器内部就干了三件事：

- 判断传入的文本是否包含变量
- 构造expression
- 构造tokens

那么接下来我们就通过阅读源码，逐行分析文本解析器内部工作原理。

### 源码分析

 文本解析器的源码位于 `src/compiler/parser/text-parsre.js` 中，代码如下：

```javascript
const defaultTagRE = /\{\{((?:.|\n)+?)\}\}/g
const buildRegex = cached(delimiters => {
  const open = delimiters[0].replace(regexEscapeRE, '\\$&')
  const close = delimiters[1].replace(regexEscapeRE, '\\$&')
  return new RegExp(open + '((?:.|\\n)+?)' + close, 'g')
})
export function parseText (text,delimiters) {
  const tagRE = delimiters ? buildRegex(delimiters) : defaultTagRE
  if (!tagRE.test(text)) {
    return
  }
  const tokens = []
  const rawTokens = []
  /**
   * let lastIndex = tagRE.lastIndex = 0
   * 上面这行代码等同于下面这两行代码:
   * tagRE.lastIndex = 0
   * let lastIndex = tagRE.lastIndex
   */
  let lastIndex = tagRE.lastIndex = 0
  let match, index, tokenValue
  while ((match = tagRE.exec(text))) {
    index = match.index
    // push text token
    if (index > lastIndex) {
      // 先把'{{'前面的文本放入tokens中
      rawTokens.push(tokenValue = text.slice(lastIndex, index))
      tokens.push(JSON.stringify(tokenValue))
    }
    // tag token
    // 取出'{{ }}'中间的变量exp
    const exp = parseFilters(match[1].trim())
    // 把变量exp改成_s(exp)形式也放入tokens中
    tokens.push(`_s(${exp})`)
    rawTokens.push({ '@binding': exp })
    // 设置lastIndex 以保证下一轮循环时，只从'}}'后面再开始匹配正则
    lastIndex = index + match[0].length
  }
  // 当剩下的text不再被正则匹配上时，表示所有变量已经处理完毕
  // 此时如果lastIndex < text.length，表示在最后一个变量后面还有文本
  // 最后将后面的文本再加入到tokens中
  if (lastIndex < text.length) {
    rawTokens.push(tokenValue = text.slice(lastIndex))
    tokens.push(JSON.stringify(tokenValue))
  }

  // 最后把数组tokens中的所有元素用'+'拼接起来
  return {
    expression: tokens.join('+'),
    tokens: rawTokens
  }
}

```

我们看到，除开我们自己加的注释，代码其实不复杂，我们逐行分析。

`parseText`函数接收两个参数，一个是传入的待解析的文本内容`text`，一个包裹变量的符号`delimiters`。第一个参数好理解，那第二个参数是干什么的呢？别急，我们看函数体内第一行代码：

```javascript
const tagRE = delimiters ? buildRegex(delimiters) : defaultTagRE
```

函数体内首先定义了变量`tagRE`，表示一个正则表达式。这个正则表达式是用来检查文本中是否包含变量的。我们知道，通常我们在模板中写变量时是这样写的：hello {{name}}。这里用`{{}}`包裹的内容就是变量。所以我们就知道，`tagRE`是用来检测文本内是否有`{{}}`。而`tagRE`又是可变的，它是根据是否传入了`delimiters`参数从而又不同的值，也就是说如果没有传入`delimiters`参数，则是检测文本是否包含`{{}}`，如果传入了值，就会检测文本是否包含传入的值。换句话说在开发`Vue`项目中，用户可以自定义文本内包含变量所使用的符号，例如你可以使用`%`包裹变量如：hello %name%。

接下来用`tagRE`去匹配传入的文本内容，判断是否包含变量，若不包含，则直接返回，如下：

```javascript
if (!tagRE.test(text)) {
    return
}
```

如果包含变量，那就继续往下看：

```javascript
const tokens = []
const rawTokens = []
let lastIndex = tagRE.lastIndex = 0
let match, index, tokenValue
while ((match = tagRE.exec(text))) {

}
```

接下来会开启一个`while`循环，循环结束条件是`tagRE.exec(text)`的结果`match`是否为`null`，`exec( )`方法是在一个字符串中执行匹配检索，如果它没有找到任何匹配就返回`null`，但如果它找到了一个匹配就返回一个数组。例如：

```javascript
tagRE.exec("hello {{name}}，I am {{age}}")
//返回：["{{name}}", "name", index: 6, input: "hello {{name}}，I am {{age}}", groups: undefined]
tagRE.exec("hello")
//返回：null
```

可以看到，当匹配上时，匹配结果的第一个元素是字符串中第一个完整的带有包裹的变量，第二个元素是第一个被包裹的变量名，第三个元素是第一个变量在字符串中的起始位置。

接着往下看循环体内：

```javascript
while ((match = tagRE.exec(text))) {
    index = match.index
    if (index > lastIndex) {
      // 先把'{{'前面的文本放入tokens中
      rawTokens.push(tokenValue = text.slice(lastIndex, index))
      tokens.push(JSON.stringify(tokenValue))
    }
    // tag token
    // 取出'{{ }}'中间的变量exp
    const exp = match[1].trim()
    // 把变量exp改成_s(exp)形式也放入tokens中
    tokens.push(`_s(${exp})`)
    rawTokens.push({ '@binding': exp })
    // 设置lastIndex 以保证下一轮循环时，只从'}}'后面再开始匹配正则
    lastIndex = index + match[0].length
  }
```

上面代码中，首先取得字符串中第一个变量在字符串中的起始位置赋给`index`，然后比较`index`和`lastIndex`的大小，此时你可能有疑问了，这个`lastIndex`是什么呢？在上面定义变量中，定义了`let lastIndex = tagRE.lastIndex = 0`,所以`lastIndex`就是`tagRE.lastIndex`，而`tagRE.lastIndex`又是什么呢？当调用`exec( )`的正则表达式对象具有修饰符`g`时，它将把当前正则表达式对象的`lastIndex`属性设置为紧挨着匹配子串的字符位置，当同一个正则表达式第二次调用`exec( )`，它会将从`lastIndex`属性所指示的字符串处开始检索，如果`exec( )`没有发现任何匹配结果，它会将`lastIndex`重置为0。示例如下：

```javascript
const tagRE = /\{\{((?:.|\n)+?)\}\}/g
tagRE.exec("hello {{name}}，I am {{age}}")
tagRE.lastIndex   // 14
```

从示例中可以看到，`tagRE.lastIndex`就是第一个包裹变量最后一个`}`所在字符串中的位置。`lastIndex`初始值为0。

那么接下里就好理解了，当`index>lastIndex`时，表示变量前面有纯文本，那么就把这段纯文本截取出来，存入`rawTokens`中，同时再调用`JSON.stringify`给这段文本包裹上双引号，存入`tokens`中，如下：

```javascript
if (index > lastIndex) {
    // 先把'{{'前面的文本放入tokens中
    rawTokens.push(tokenValue = text.slice(lastIndex, index))
    tokens.push(JSON.stringify(tokenValue))
}
```

如果`index`不大于`lastIndex`，那说明`index`也为0，即该文本一开始就是变量，例如：`{{name}}hello`。那么此时变量前面没有纯文本，那就不用截取，直接取出匹配结果的第一个元素变量名，将其用`_s()`包裹存入`tokens`中，同时再把变量名构造成`{'@binding': exp}`存入`rawTokens`中，如下：

```javascript
// 取出'{{ }}'中间的变量exp
const exp = match[1].trim()
// 把变量exp改成_s(exp)形式也放入tokens中
tokens.push(`_s(${exp})`)
rawTokens.push({ '@binding': exp })
```

接着，更新`lastIndex `以保证下一轮循环时，只从`}}`后面再开始匹配正则，如下：

```javascript
lastIndex = index + match[0].length
```

接着，当`while`循环完毕时，表明文本中所有变量已经被解析完毕，如果此时`lastIndex < text.length`，那就说明最后一个变量的后面还有纯文本，那就将其再存入`tokens`和`rawTokens`中，如下：

```javascript
// 当剩下的text不再被正则匹配上时，表示所有变量已经处理完毕
// 此时如果lastIndex < text.length，表示在最后一个变量后面还有文本
// 最后将后面的文本再加入到tokens中
if (lastIndex < text.length) {
    rawTokens.push(tokenValue = text.slice(lastIndex))
    tokens.push(JSON.stringify(tokenValue))
}
```

最后，把`tokens`数组里的元素用`+`连接，和`rawTokens`一并返回，如下：

```javascript
return {
    expression: tokens.join('+'),
    tokens: rawTokens
}
```

以上就是文本解析器`parseText`函数的所有逻辑了。

### 总结

本篇文章介绍了文本解析器的内部工作原理，文本解析器的作用就是将`HTML`解析器解析得到的文本内容进行二次解析，解析文本内容中是否包含变量，如果包含变量，则将变量提取出来进行加工，为后续生产`render`函数做准备。

## 4.5 优化阶段

### 前言

在前几篇文章中，我们介绍了模板编译流程三大阶段中的第一阶段模板解析阶段，在这一阶段主要做的工作是用解析器将用户所写的模板字符串解析成`AST`抽象语法树，理论上来讲，有了`AST`就可直接进入第三阶段生成`render`函数了。其实不然，`Vue`还是很看重性能的，只要有一点可以优化的地方就要将其进行优化。在之前介绍虚拟`DOM`的时候我们说过，有一种节点一旦首次渲染上了之后不管状态再怎么变化它都不会变了，这种节点叫做静态节点，如下：

```html
<ul>
    <li>我是文本信息</li>
    <li>我是文本信息</li>
    <li>我是文本信息</li>
    <li>我是文本信息</li>
    <li>我是文本信息</li>
</ul>
```

在上面代码中，`ul`标签下面有5个`li`标签，每个`li`标签里的内容都是不含任何变量的纯文本，也就是说这种标签一旦第一次被渲染成`DOM`节点以后，之后不管状态再怎么变化它都不会变了，我们把像`li`的这种节点称之为静态节点。而这5个`li`节点的父节点是`ul`节点，也就是说`ul`节点的所有子节点都是静态节点，那么我们把像`ul`的这种节点称之为静态根节点。

OK，有了静态节点和静态根节点这两个概念之后，我们再仔细思考，模板编译的最终目的是用模板生成一个`render`函数，而用`render`函数就可以生成与模板对应的`VNode`，之后再进行`patch`算法，最后完成视图渲染。这中间的`patch`算法又是用来对比新旧`VNode`之间存在的差异。在上面我们还说了，静态节点不管状态怎么变化它是不会变的，基于此，那我们就可以在`patch`过程中不用去对比这些静态节点了，这样不就又可以提高一些性能了吗？

所以我们在模板编译的时候就先找出模板中所有的静态节点和静态根节点，然后给它们打上标记，用于告诉后面`patch`过程打了标记的这些节点是不需要对比的，你只要把它们克隆一份去用就好啦。这就是优化阶段存在的意义。

上面也说了，优化阶段其实就干了两件事：

1. 在`AST`中找出所有静态节点并打上标记；
2. 在`AST`中找出所有静态根节点并打上标记；

优化阶段的源码位于`src/compiler/optimizer.js`中，如下：

```javascript
export function optimize (root: ?ASTElement, options: CompilerOptions) {
  if (!root) return
  isStaticKey = genStaticKeysCached(options.staticKeys || '')
  isPlatformReservedTag = options.isReservedTag || no
  // 标记静态节点
  markStatic(root)
  // 标记静态根节点
  markStaticRoots(root, false)
}
```



接下来，我们就对所干的这两件事逐个分析。

### 标记静态节点

从`AST`中找出所有静态节点并标记其实不难，我们只需从根节点开始，先标记根节点是否为静态节点，然后看根节点如果是元素节点，那么就去向下递归它的子节点，子节点如果还有子节点那就继续向下递归，直到标记完所有节点。代码如下：

```javascript
function markStatic (node: ASTNode) {
  node.static = isStatic(node)
  if (node.type === 1) {
    // do not make component slot content static. this avoids
    // 1. components not able to mutate slot nodes
    // 2. static slot content fails for hot-reloading
    if (
      !isPlatformReservedTag(node.tag) &&
      node.tag !== 'slot' &&
      node.attrsMap['inline-template'] == null
    ) {
      return
    }
    for (let i = 0, l = node.children.length; i < l; i++) {
      const child = node.children[i]
      markStatic(child)
      if (!child.static) {
        node.static = false
      }
    }
    if (node.ifConditions) {
      for (let i = 1, l = node.ifConditions.length; i < l; i++) {
        const block = node.ifConditions[i].block
        markStatic(block)
        if (!block.static) {
          node.static = false
        }
      }
    }
  }
}
```

在上面代码中，首先调用`isStatic`函数标记节点是否为静态节点，该函数若返回`true`表示该节点是静态节点，若返回`false`表示该节点不是静态节点，函数实现如下：

```javascript
function isStatic (node: ASTNode): boolean {
  if (node.type === 2) { // 包含变量的动态文本节点
    return false
  }
  if (node.type === 3) { // 不包含变量的纯文本节点
    return true
  }
  return !!(node.pre || (
    !node.hasBindings && // no dynamic bindings
    !node.if && !node.for && // not v-if or v-for or v-else
    !isBuiltInTag(node.tag) && // not a built-in
    isPlatformReservedTag(node.tag) && // not a component
    !isDirectChildOfTemplateFor(node) &&
    Object.keys(node).every(isStaticKey)
  ))
}
```

该函数的实现过程其实也说明了如何判断一个节点是否为静态节点。还记得在`HTML`解析器在调用钩子函数创建`AST`节点时会根据节点类型的不同为节点加上不同的`type`属性，用`type`属性来标记`AST`节点的节点类型，其对应关系如下：

| type取值 | 对应的AST节点类型      |
| -------- | ---------------------- |
| 1        | 元素节点               |
| 2        | 包含变量的动态文本节点 |
| 3        | 不包含变量的纯文本节点 |

所以在判断一个节点是否为静态节点时首先会根据`type`值判断节点类型，如果`type`值为2，那么该节点是包含变量的动态文本节点，它就肯定不是静态节点，返回`false`；

```javascript
if (node.type === 2) { // 包含变量的动态文本节点
    return false
}
```

如果`type`值为2，那么该节点是不包含变量的纯文本节点，它就肯定是静态节点，返回`true`；

```javascript
if (node.type === 3) { // 不包含变量的纯文本节点
    return true
}
```



如果`type`值为1,说明该节点是元素节点，那就需要进一步判断。

```javascript
node.pre ||
(
    !node.hasBindings && // no dynamic bindings
    !node.if && !node.for && // not v-if or v-for or v-else
    !isBuiltInTag(node.tag) && // not a built-in
    isPlatformReservedTag(node.tag) && // not a component
    !isDirectChildOfTemplateFor(node) &&
    Object.keys(node).every(isStaticKey)
)
```



如果元素节点是静态节点，那就必须满足以下几点要求：

- 如果节点使用了`v-pre`指令，那就断定它是静态节点；
- 如果节点没有使用`v-pre`指令，那它要成为静态节点必须满足：
  - 不能使用动态绑定语法，即标签上不能有`v-`、`@`、`:`开头的属性；
  - 不能使用`v-if`、`v-else`、`v-for`指令；
  - 不能是内置组件，即标签名不能是`slot`和`component`；
  - 标签名必须是平台保留标签，即不能是组件；
  - 当前节点的父节点不能是带有 `v-for` 的 `template` 标签；
  - 节点的所有属性的 `key` 都必须是静态节点才有的 `key`，注：静态节点的`key`是有限的，它只能是`type`,`tag`,`attrsList`,`attrsMap`,`plain`,`parent`,`children`,`attrs`之一；

标记完当前节点是否为静态节点之后，如果该节点是元素节点，那么还要继续去递归判断它的子节点，如下：

```javascript
for (let i = 0, l = node.children.length; i < l; i++) {
    const child = node.children[i]
    markStatic(child)
    if (!child.static) {
        node.static = false
    }
}
```

注意，在上面代码中，新增了一个判断：

```javascript
if (!child.static) {
    node.static = false
}
```

这个判断的意思是如果当前节点的子节点有一个不是静态节点，那就把当前节点也标记为非静态节点。为什么要这么做呢？这是因为我们在判断的时候是从上往下判断的，也就是说先判断当前节点，再判断当前节点的子节点，如果当前节点在一开始被标记为了静态节点，但是通过判断子节点的时候发现有一个子节点却不是静态节点，这就有问题了，我们之前说过一旦标记为静态节点，就说明这个节点首次渲染之后不会再发生任何变化，但是它的一个子节点却又是可以变化的，就出现了自相矛盾，所以我们需要当发现它的子节点中有一个不是静态节点的时候，就得把当前节点重新设置为非静态节点。

循环`node.children`后还不算把所有子节点都遍历完，因为如果当前节点的子节点中有标签带有`v-if`、`v-else-if`、`v-else`等指令时，这些子节点在每次渲染时都只渲染一个，所以其余没有被渲染的肯定不在`node.children`中，而是存在于`node.ifConditions`，所以我们还要把`node.ifConditions`循环一遍，如下：

```javascript
if (node.ifConditions) {
    for (let i = 1, l = node.ifConditions.length; i < l; i++) {
        const block = node.ifConditions[i].block
        markStatic(block)
        if (!block.static) {
            node.static = false
        }
    }
}
```

同理，如果当前节点的`node.ifConditions`中有一个子节点不是静态节点也要将当前节点设置为非静态节点。

以上就是标记静态节点的全部逻辑。

### 标记静态根节点

寻找静态根节点根寻找静态节点的逻辑类似，都是从`AST`根节点递归向下遍历寻找，其代码如下：

```javascript
function markStaticRoots (node: ASTNode, isInFor: boolean) {
  if (node.type === 1) {
    if (node.static || node.once) {
      node.staticInFor = isInFor
    }
    // For a node to qualify as a static root, it should have children that
    // are not just static text. Otherwise the cost of hoisting out will
    // outweigh the benefits and it's better off to just always render it fresh.
    if (node.static && node.children.length && !(
      node.children.length === 1 &&
      node.children[0].type === 3
    )) {
      node.staticRoot = true
      return
    } else {
      node.staticRoot = false
    }
    if (node.children) {
      for (let i = 0, l = node.children.length; i < l; i++) {
        markStaticRoots(node.children[i], isInFor || !!node.for)
      }
    }
    if (node.ifConditions) {
      for (let i = 1, l = node.ifConditions.length; i < l; i++) {
        markStaticRoots(node.ifConditions[i].block, isInFor)
      }
    }
  }
}
```

上面代码中，首先`markStaticRoots` 第二个参数是 `isInFor`，对于已经是 `static` 的节点或者是 `v-once` 指令的节点，`node.staticInFor = isInFor`，如下：

```javascript
if (node.static || node.once) {
    node.staticInFor = isInFor
}
```



接着判断该节点是否为静态根节点，如下：

```javascript
// For a node to qualify as a static root, it should have children that
// are not just static text. Otherwise the cost of hoisting out will
// outweigh the benefits and it's better off to just always render it fresh.
// 为了使节点有资格作为静态根节点，它应具有不只是静态文本的子节点。 否则，优化的成本将超过收益，最好始终将其更新。
if (node.static && node.children.length && !(
    node.children.length === 1 &&
    node.children[0].type === 3
)) {
    node.staticRoot = true
    return
} else {
    node.staticRoot = false
}
```

从代码和注释中我们可以看到，一个节点要想成为静态根节点，它必须满足以下要求：

- 节点本身必须是静态节点；
- 必须拥有子节点 `children`；
- 子节点不能只是只有一个文本节点；

否则的话，对它的优化成本将大于优化后带来的收益。

如果当前节点不是静态根节点，那就继续递归遍历它的子节点`node.children`和`node.ifConditions`，如下：

```javascript
if (node.children) {
    for (let i = 0, l = node.children.length; i < l; i++) {
        markStaticRoots(node.children[i], isInFor || !!node.for)
    }
}
if (node.ifConditions) {
    for (let i = 1, l = node.ifConditions.length; i < l; i++) {
        markStaticRoots(node.ifConditions[i].block, isInFor)
    }
}
```



这里的原理跟寻找静态节点相同，此处就不再重复。

### 总结

本篇文章介绍了模板编译过程三大阶段的第二阶段——优化阶段。

首先，介绍了为什么要有优化阶段，是为了提高虚拟`DOM`中`patch`过程的性能。在优化阶段将所有静态节点都打上标记，这样在`patch`过程中就可以跳过对比这些节点。

接着，介绍了优化阶段主要干了两件事情，分别是从构建出的`AST`中找出并标记所有静态节点和所有静态根节点。

最后，分别通过逐行分析源码的方式分析了这两件事具体的内部工作原理。

## 4.6 代码生成阶段

### 前言

经过前几篇文章，我们把用户所写的模板字符串先经过解析阶段解析生成对应的抽象语法树`AST`，接着再经过优化阶段将`AST`中的静态节点及静态根节点都打上标记，现在终于到了模板编译三大阶段的最后一个阶段了——代码生成阶段。所谓代码生成阶段，到底是要生成什么代码？答：要生成`render`函数字符串。

我们知道，`Vue`实例在挂载的时候会调用其自身的`render`函数来生成实例上的`template`选项所对应的`VNode`，简单的来说就是`Vue`只要调用了`render`函数，就可以把模板转换成对应的虚拟`DOM`。那么`Vue`要想调用`render`函数，那必须要先有这个`render`函数，那这个`render`函数又是从哪来的呢？是用户手写的还是`Vue`自己生成的？答案是都有可能。我们知道，我们在日常开发中是可以在`Vue`组件选项中手写一个`render`选项，其值对应一个函数，那这个函数就是`render`函数，当用户手写了`render`函数时，那么`Vue`在挂载该组件的时候就会调用用户手写的这个`render`函数。那如果用户没有写呢？那这个时候`Vue`就要自己根据模板内容生成一个`render`函数供组件挂载的时候调用。而`Vue`自己根据模板内容生成`render`函数的过程就是本篇文章所要介绍的代码生成阶段。

现在我们知道了，所谓代码生成其实就是根据模板对应的抽象语法树`AST`生成一个函数，通过调用这个函数就可以得到模板对应的虚拟`DOM`。

### 如何根据AST生成render函数

通过上文我们知道了，代码生成阶段主要的工作就是根据已有的`AST`生成对应的`render`函数供组件挂载时调用，组件只要调用的这个`render`函数就可以得到`AST`对应的虚拟`DOM`的`VNode`。那么如何根据`AST`生成`render`函数呢？这其中是怎样一个过程呢？接下来我们就来细细剖析一下。

假设现有如下模板：

```html
<div id="NLRX"><p>Hello {{name}}</p></div>
```

该模板经过解析并优化后对应的`AST`如下：

```javascript
ast = {
    'type': 1,
    'tag': 'div',
    'attrsList': [
        {
            'name':'id',
            'value':'NLRX',
        }
    ],
    'attrsMap': {
      'id': 'NLRX',
    },
    'static':false,
    'parent': undefined,
    'plain': false,
    'children': [{
      'type': 1,
      'tag': 'p',
      'plain': false,
      'static':false,
      'children': [
        {
            'type': 2,
            'expression': '"Hello "+_s(name)',
            'text': 'Hello {{name}}',
            'static':false,
        }
      ]
    }]
  }
```

下面我们就来根据已有的这个`AST`来生成对应的`render`函数。生成`render`函数的过程其实就是一个递归的过程，从顶向下依次递归`AST`中的每一个节点，根据不同的`AST`节点类型创建不同的`VNode`类型。接下来我们就来对照已有的模板和`AST`实际演示一下生成`render`函数的过程。

1. 首先，根节点`div`是一个元素型`AST`节点，那么我们就要创建一个元素型`VNode`，我们把创建元素型`VNode`的方法叫做`_c(tagName,data,children)`。我们暂且不管`_c()`是什么，只需知道调用`_c()`就可以创建一个元素型`VNode`。那么就可以生成如下代码：

   ```javascript
   _c('div',{attrs:{"id":"NLRX"}},[/*子节点列表*/])
   ```

2. 根节点`div`有子节点，那么我们进入子节点列表`children`里遍历子节点，发现子节点`p`也是元素型的，那就继续创建元素型`VNode`并将其放入上述代码中根节点的子节点列表中，如下：

   ```javascript
   _c('div',{attrs:{"id":"NLRX"}},[_c('p',{attrs:{}},[/*子节点列表*/])])
   ```

3. 同理，继续遍历`p`节点的子节点，发现是一个文本型节点，那就创建一个文本型`VNode`并将其插入到`p`节点的子节点列表中，同理，创建文本型`VNode`我们调用`_v()`方法，如下：

   ```javascript
   _c('div',{attrs:{"id":"NLRX"}},[_c('p',{attrs:{}},[_v("Hello "+_s(name))])])
   ```

4. 到此，整个`AST`就遍历完毕了，我们将得到的代码再包装一下，如下：

   ```javascript
    `
    with(this){
      reurn _c(
        'div',
        {
          attrs:{"id":"NLRX"},
        },
        [
          _c(
            'p',
            {
              attrs:{}
            },
            [
              _v("Hello "+_s(name))
            ]
          )
        ]
      )
    }
    `
   ```

5. 最后，我们将上面得到的这个函数字符串传递给`createFunction `函数（关于这个函数在后面会介绍到），`createFunction `函数会帮我们把得到的函数字符串转换成真正的函数，赋给组件中的`render`选项，从而就是`render`函数了。如下：

   ```javascript
   res.render = createFunction(compiled.render, fnGenErrors)

   function createFunction (code, errors) {
     try {
       return new Function(code)
     } catch (err) {
       errors.push({ err, code })
       return noop
     }
   }
   ```

以上就是根据一个简单的模板所对应的`AST`生成`render`函数的过程，理论过程我们已经了解了，那么在源码中实际是如何实现的呢？下面我们就回归源码分析其具体实现过程。

### 回归源码

代码生成阶段的源码位于`src/compiler/codegen/index.js` 中，源码虽然很长，但是逻辑不复杂，核心逻辑如下：

```javascript
export function generate (ast,option) {
  const state = new CodegenState(options)
  const code = ast ? genElement(ast, state) : '_c("div")'
  return {
    render: `with(this){return ${code}}`,
    staticRenderFns: state.staticRenderFns
  }
}
```

```javascript
const code = generate(ast, options)
```

调用`generate`函数并传入优化后得到的`ast`，在`generate`函数内部先判断`ast`是否为空，不为空则调用`genElement(ast, state)`函数创建`VNode`，为空则创建一个空的元素型`div`的`VNode`。然后将得到的结果用`with(this){return ${code}}`包裹返回。可以看出，真正起作用的是`genElement`函数，下面我们继续来看一下`genElement`函数内部是怎样的。

`genElement`函数定义如下：

```javascript
export function genElement (el: ASTElement, state: CodegenState): string {
  if (el.staticRoot && !el.staticProcessed) {
    return genStatic(el, state)
  } else if (el.once && !el.onceProcessed) {
    return genOnce(el, state)
  } else if (el.for && !el.forProcessed) {
    return genFor(el, state)
  } else if (el.if && !el.ifProcessed) {
    return genIf(el, state)
  } else if (el.tag === 'template' && !el.slotTarget) {
    return genChildren(el, state) || 'void 0'
  } else if (el.tag === 'slot') {
    return genSlot(el, state)
  } else {
    // component or element
    let code
    if (el.component) {
      code = genComponent(el.component, el, state)
    } else {
      const data = el.plain ? undefined : genData(el, state)

      const children = el.inlineTemplate ? null : genChildren(el, state, true)
      code = `_c('${el.tag}'${
        data ? `,${data}` : '' // data
      }${
        children ? `,${children}` : '' // children
      })`
    }
    // module transforms
    for (let i = 0; i < state.transforms.length; i++) {
      code = state.transforms[i](el, code)
    }
    return code
  }
}
```

`genElement`函数逻辑很清晰，就是根据当前 `AST` 元素节点属性的不同从而执行不同的代码生成函数。虽然元素节点属性的情况有很多种，但是最后真正创建出来的`VNode`无非就三种，分别是元素节点，文本节点，注释节点。接下来我们就着重分析一下如何生成这三种节点类型的`render`函数的。

####  元素节点

生成元素型节点的`render`函数代码如下：

```javascript
const data = el.plain ? undefined : genData(el, state)

const children = el.inlineTemplate ? null : genChildren(el, state, true)
code = `_c('${el.tag}'${
data ? `,${data}` : '' // data
}${
children ? `,${children}` : '' // children
})`
```

生成元素节点的`render`函数就是生成一个`_c()`函数调用的字符串，上文提到了`_c()`函数接收三个参数，分别是节点的标签名`tagName`，节点属性`data`，节点的子节点列表`children`。那么我们只需将这三部分都填进去即可。

1. 获取节点属性data

   首先判断`plain`属性是否为`true`，若为`true`则表示节点没有属性，将`data`赋值为`undefined`；如果不为`true`则调用`genData`函数获取节点属性`data`数据。`genData`函数定义如下：

   ```javascript
   export function genData (el: ASTElement, state: CodegenState): string {
     let data = '{'
     const dirs = genDirectives(el, state)
     if (dirs) data += dirs + ','

       // key
       if (el.key) {
           data += `key:${el.key},`
       }
       // ref
       if (el.ref) {
           data += `ref:${el.ref},`
       }
       if (el.refInFor) {
           data += `refInFor:true,`
       }
       // pre
       if (el.pre) {
           data += `pre:true,`
       }
       // 篇幅所限，省略其他情况的判断
       data = data.replace(/,$/, '') + '}'
       return data
   }
   ```

   我们看到，源码中`genData`虽然很长，但是其逻辑非常简单，就是在拼接字符串，先给`data`赋值为一个`{`，然后判断存在哪些属性数据，就将这些数据拼接到`data`中，最后再加一个`}`，最终得到节点全部属性`data`。

2. 获取子节点列表children

   获取子节点列表`children`其实就是遍历`AST`的`children`属性中的元素，然后根据元素属性的不同生成不同的`VNode`创建函数调用字符串，如下：

   ```javascript
   export function genChildren (el):  {
       if (children.length) {
           return `[${children.map(c => genNode(c, state)).join(',')}]`
       }
   }
   function genNode (node: ASTNode, state: CodegenState): string {
     if (node.type === 1) {
       return genElement(node, state)
     } if (node.type === 3 && node.isComment) {
       return genComment(node)
     } else {
       return genText(node)
     }
   }
   ```

3. 上面两步完成之后，生成`_c（）`函数调用字符串，如下：

   ```javascript
   code = `_c('${el.tag}'${
           data ? `,${data}` : '' // data
         }${
           children ? `,${children}` : '' // children
         })`
   ```

####  文本节点

文本型的`VNode`可以调用`_v(text)`函数来创建，所以生成文本节点的`render`函数就是生成一个`_v(text)`函数调用的字符串。`_v()`函数接收文本内容作为参数，如果文本是动态文本，则使用动态文本`AST`节点的`expression`属性，如果是纯静态文本，则使用`text`属性。其生成代码如下：

```javascript
export function genText (text: ASTText | ASTExpression): string {
  return `_v(${text.type === 2
    ? text.expression // no need for () because already wrapped in _s()
    : transformSpecialNewlines(JSON.stringify(text.text))
  })`
}
```

####  注释节点

注释型的`VNode`可以调用`_e(text)`函数来创建，所以生成注释节点的`render`函数就是生成一个`_e(text)`函数调用的字符串。`_e()`函数接收注释内容作为参数，其生成代码如下：

```javascript
export function genComment (comment: ASTText): string {
  return `_e(${JSON.stringify(comment.text)})`
}
```

### 总结

本篇文章介绍了模板编译三大阶段的最后一个阶段——代码生成阶段。

首先，介绍了为什么要有代码生成阶段以及代码生成阶段主要干什么。我们知道了，代码生成其实就是根据模板对应的抽象语法树`AST`生成一个函数供组件挂载时调用，通过调用这个函数就可以得到模板对应的虚拟`DOM`。

接着，我们通过一个简单的模板演示了把模板经过递归遍历最后生成`render`函数的过程。

最后，我们回归源码，通过分析源码了解了生成`render`函数的具体实现过程。

## 4.7 模板编译篇总结

### 前言

到现在，模板编译的三大阶段就已经全部介绍完毕了，接下来本篇文章，就以宏观角度回顾并梳理一下模板编译整个流程是怎样的。

首先，我们需要搞清楚模板编译的最终目的是什么，它的最终目的就是：把用户所写的模板转化成供`Vue`实例在挂载时可调用的`render`函数。或者你可以这样简单的理解为：模板编译就是一台机器，给它输入模板字符串，它就输出对应的`render`函数。

我们把模板编译的最终目的只要牢记在心以后，那么模板编译中间的所有的变化都是在为达到这个目的而努力。

接下来我们就以宏观角度来梳理一下模板编译的整个流程。

### 整体流程

上文说了，模板编译就是把模板转化成供`Vue`实例在挂载时可调用的`render`函数。那么我们就从`Vue`实例挂载时入手，一步一步从后往前推。我们知道，`Vue`实例在挂载时会调用全局实例方法——`$mount`方法(关于该方法后面会详细介绍)。那么我们就先看一下`$mount`方法，如下：

```javascript
Vue.prototype.$mount = function(el) {
  const options = this.$options;
  // 如果用户没有手写render函数
  if (!options.render) {
    // 获取模板，先尝试获取内部模板，如果获取不到则获取外部模板
    let template = options.template;
    if (template) {
    } else {
      template = getOuterHTML(el);
    }
    const { render, staticRenderFns } = compileToFunctions(
      template,
      {
        shouldDecodeNewlines,
        shouldDecodeNewlinesForHref,
        delimiters: options.delimiters,
        comments: options.comments
      },
      this
    );
    options.render = render;
    options.staticRenderFns = staticRenderFns;
  }
};
```

从上述代码中可以看到，首先从`Vue`实例的属性选项中获取`render`选项，如果没有获取到，说明用户没有手写`render`函数，那么此时，就像上一篇文章中说的，需要`Vue`自己将模板转化成`render`函数。接着获取模板，先尝试获取内部模板，如果获取不到则获取外部模板。最后，调用`compileToFunctions`函数将模板转化成`render`函数，再将`render`函数赋值给`options.render`。

显然，上面代码中的核心部分是调用`compileToFunctions`函数生成`render`函数的部分，如下：

```javascript
const { render, staticRenderFns } = compileToFunctions(
  template,
  {
    shouldDecodeNewlines,
    shouldDecodeNewlinesForHref,
    delimiters: options.delimiters,
    comments: options.comments
  },
  this
);
```

将模板`template`传给`compileToFunctions`函数就可以得到`render`函数，那这个`compileToFunctions`函数是怎么来的呢？

我们通过代码跳转发现`compileToFunctions`函数的出处如下：

```javascript
const { compile, compileToFunctions } = createCompiler(baseOptions);
```

我们发现，`compileToFunctions`函数是 `createCompiler` 函数的返回值对象中的其中一个，`createCompiler` 函数顾名思义他的作用就是创建一个编译器。那么我们再继续往前推，看看`createCompiler` 函数又是从哪来的。

`createCompiler` 函数出处位于源码的`src/complier/index.js`文件中，如下：

```javascript
export const createCompiler = createCompilerCreator(function baseCompile(
  template: string,
  options: CompilerOptions
): CompiledResult {
  // 模板解析阶段：用正则等方式解析 template 模板中的指令、class、style等数据，形成AST
  const ast = parse(template.trim(), options);
  if (options.optimize !== false) {
    // 优化阶段：遍历AST，找出其中的静态节点，并打上标记；
    optimize(ast, options);
  }
  // 代码生成阶段：将AST转换成渲染函数；
  const code = generate(ast, options);
  return {
    ast,
    render: code.render,
    staticRenderFns: code.staticRenderFns
  };
});
```

可以看到，`createCompiler`函数是又 调用`createCompilerCreator` 函数返回得到的，`createCompilerCreator` 函数接收一个`baseCompile`函数作为参数。我们仔细看这个`baseCompile`函数，这个函数就是我们所说的模板编译三大阶段的主函数。将这个函数传给`createCompilerCreator` 函数就可以得到`createCompiler`函数，那么我们再往前推，看一下`createCompilerCreator` 函数又是怎么定义的。

`createCompilerCreator` 函数的定义位于源码的`src/complier/create-compiler.js`文件中，如下：

```javascript
export function createCompilerCreator(baseCompile) {
  return function createCompiler(baseOptions) {};
}
```

可以看到，调用`createCompilerCreator` 函数会返回`createCompiler`函数，同时我们也可以看到`createCompiler`函数的定义，如下：

```javascript
function createCompiler(baseOptions) {
  function compile() {}
  return {
    compile,
    compileToFunctions: createCompileToFunctionFn(compile)
  };
}
```

在`createCompiler`函数的内部定义了一个子函数`compile`，同时返回一个对象，其中这个对象的第二个属性就是我们在开头看到的`compileToFunctions`，其值对应的是`createCompileToFunctionFn(compile)`函数的返回值，那么我们再往前推，看看`createCompileToFunctionFn(compile)`函数又是怎么样的。

`createCompileToFunctionFn(compile)`函数的出处位于源码的`src/complier/to-function.js`文件中，如下：

```javascript
export function createCompileToFunctionFn(compile) {
  return function compileToFunctions() {
    // compile
    const res = {};
    const compiled = compile(template, options);
    res.render = createFunction(compiled.render, fnGenErrors);
    res.staticRenderFns = compiled.staticRenderFns.map(code => {
      return createFunction(code, fnGenErrors);
    });
    return res;
  };
}

function createFunction(code, errors) {
  try {
    return new Function(code);
  } catch (err) {
    errors.push({ err, code });
    return noop;
  }
}
```

可以看到，调用`createCompileToFunctionFn`函数就可以得到`compileToFunctions`函数了，终于推到头了，原来最开始调用`compileToFunctions`函数是在这里定义的，那么我们就来看一下`compileToFunctions`函数内部都干了些什么。

`compileToFunctions`函数内部会调用传入的`compile`函数，而这个`compile`函数是`createCompiler`函数内部定义的子函数，如下：

```javascript
function compile(template, options) {
  const compiled = baseCompile(template, finalOptions);
  compiled.errors = errors;
  compiled.tips = tips;
  return compiled;
}
```

在`compile`函数内部又会调用传入的`baseCompile`函数，而这个`baseCompile`函数就是我们所说的模板编译三大阶段的主线函数，如下：

```javascript
function baseCompile (
  template: string,
  options: CompilerOptions
): CompiledResult {
  // 模板解析阶段：用正则等方式解析 template 模板中的指令、class、style等数据，形成AST
  const ast = parse(template.trim(), options)
  if (options.optimize !== false) {
    // 优化阶段：遍历AST，找出其中的静态节点，并打上标记；
    optimize(ast, options)
  }
  // 代码生成阶段：将AST转换成渲染函数；
  const code = generate(ast, options)
  return {
    ast,
    render: code.render,
    staticRenderFns: code.staticRenderFns
  }

```

那么现在就清晰了，最开始调用的`compileToFunctions`函数内部调用了`compile`函数，在`compile`函数内部又调用了`baseCompile`函数，而`baseCompile`函数返回的是代码生成阶段生成好的`render`函数字符串。所以在`compileToFunctions`函数内部调用`compile`函数就可以拿到生成好的`render`函数字符串，然后在`compileToFunctions`函数内部将`render`函数字符串传给`createFunction`函数从而变成真正的`render`函数返回出去，最后将其赋值给`options.render`。为了便于更好的理解，我们画出了其上述过程的流程图，如下：

![](~@/learn-vue-source-code/complie/8.jpg)

以上，就是模板编译的整体流程。

### 整体导图

![](~@/learn-vue-source-code/complie/9.png)

# 5. 生命周期篇

## 生命周期篇综述


### 前言

在`Vue`中，每个`Vue`实例从被创建出来到最终被销毁都会经历一个过程，就像人一样，从出生到死亡。在这一过程里会发生许许多多的事，例如设置数据监听，编译模板，组件挂载等。在`Vue`中，把`Vue`实例从被创建出来到最终被销毁的这一过程称为`Vue`实例的生命周期，同时，在`Vue`实例生命周期的不同阶段`Vue`还提供了不同的钩子函数，以方便用户在不同的生命周期阶段做一些额外的事情。那么，接下来的几篇文章我们就从源码角度深入剖析一下一个`Vue`实例在从生到死的生命周期里到底都经历了些什么，每个阶段都做了哪些事情。

### 生命周期流程图

下图是`Vue`官网给出的`Vue`实例的生命周期流程图，如下：

![](~@/learn-vue-source-code/lifecycle/1.jpg)

从图中我们可以看到，`Vue`实例的生命周期大致可分为4个阶段：

- 初始化阶段：为`Vue`实例上初始化一些属性，事件以及响应式数据；
- 模板编译阶段：将模板编译成渲染函数；
- 挂载阶段：将实例挂载到指定的`DOM`上，即将模板渲染到真实`DOM`中；
- 销毁阶段：将实例自身从父组件中删除，并取消依赖追踪及事件监听器；



### 总结

本篇文章是生命周期篇的开篇综述，借用`Vue`官网的生命周期流程图介绍了一个`Vue`实例的生命周期大致可分为四个阶段，分别是初始化阶段、模板编译阶段、挂载阶段、销毁阶段。接下来的几篇文章我们就从这个流程图为基础，自上到下，从每个阶段入手，深入分析在每个阶段里都干了些什么。

## 初始化阶段(new Vue)


### 前言

上篇文章中介绍了`Vue`实例的生命周期大致分为4个阶段，那么首先我们先从第一个阶段——初始化阶段开始入手分析。从生命周期流程图中我们可以看到，初始化阶段所做的工作也可大致分为两部分：第一部分是`new Vue()`，也就是创建一个`Vue`实例；第二部分是为创建好的`Vue`实例初始化一些事件、属性、响应式数据等。接下来我们就从源码角度来深入分析一下初始化阶段所做的工作及其内部原理。

### new Vue()都干了什么

初始化阶段所做的第一件事就是`new Vue()`创建一个`Vue`实例，那么`new Vue()`的内部都干了什么呢？ 我们知道，`new` 关键字在 `JS`中表示从一个类中实例化出一个对象来，由此可见， `Vue` 实际上是一个类。所以`new Vue()`实际上是执行了`Vue`类的构造函数，那么我们来看一下`Vue`类是如何定义的，`Vue`类的定义是在源码的`src/core/instance/index.js` 中，如下：

```javascript
function Vue (options) {
  if (process.env.NODE_ENV !== 'production' &&
    !(this instanceof Vue)
  ) {
    warn('Vue is a constructor and should be called with the `new` keyword')
  }
  this._init(options)
}
```

可以看到，`Vue`类的定义非常简单，其构造函数核心就一行代码：

```javascript
this._init(options)
```

调用原型上的`_init(options)`方法并把用户所写的选项`options`传入。那这个`_init`方法是从哪来的呢？在`Vue`类定义的下面还有几行代码，其中之一就是：

```javascript
initMixin(Vue)
```

这一行代码执行了`initMixin`函数，那`initMixin`函数又是从哪儿来的呢？该函数定义位于源码的`src/core/instance/init.js` 中，如下：

```javascript
export function initMixin (Vue) {
  Vue.prototype._init = function (options) {
    const vm = this
    vm.$options = mergeOptions(
        resolveConstructorOptions(vm.constructor),
        options || {},
        vm
    )
    vm._self = vm
    initLifecycle(vm)
    initEvents(vm)
    initRender(vm)
    callHook(vm, 'beforeCreate')
    initInjections(vm) // resolve injections before data/props
    initState(vm)
    initProvide(vm) // resolve provide after data/props
    callHook(vm, 'created')

    if (vm.$options.el) {
      vm.$mount(vm.$options.el)
    }
  }
}
```

可以看到，在`initMixin`函数内部就只干了一件事，那就是给`Vue`类的原型上绑定`_init`方法，同时`_init`方法的定义也在该函数内部。现在我们知道了，`new Vue()`会执行`Vue`类的构造函数，构造函数内部会执行`_init`方法，所以`new Vue()`所干的事情其实就是`_init`方法所干的事情，那么我们着重来分析下`_init`方法都干了哪些事情。

首先，把`Vue`实例赋值给变量`vm`，并且把用户传递的`options`选项与当前构造函数的`options`属性及其父级构造函数的`options`属性进行合并（关于属性如何合并的问题下面会介绍），得到一个新的`options`选项赋值给`$options`属性，并将`$options`属性挂载到`Vue`实例上，如下：

```javascript
vm.$options = mergeOptions(
    resolveConstructorOptions(vm.constructor),
    options || {},
    vm
)
```

接着，通过调用一些初始化函数来为`Vue`实例初始化一些属性，事件，响应式数据等，如下：

```javascript
initLifecycle(vm)       // 初始化生命周期
initEvents(vm)        // 初始化事件
initRender(vm)         // 初始化渲染
callHook(vm, 'beforeCreate')  // 调用生命周期钩子函数
initInjections(vm)   //初始化injections
initState(vm)    // 初始化props,methods,data,computed,watch
initProvide(vm) // 初始化 provide
callHook(vm, 'created')  // 调用生命周期钩子函数
```

可以看到，除了调用初始化函数来进行相关数据的初始化之外，还在合适的时机调用了`callHook`函数来触发生命周期的钩子，关于`callHook`函数是如何触发生命周期的钩子会在下面介绍，我们先继续往下看：

```javascript
if (vm.$options.el) {
    vm.$mount(vm.$options.el)
}
```

在所有的初始化工作都完成以后，最后，会判断用户是否传入了`el`选项，如果传入了则调用`$mount`函数进入模板编译与挂载阶段，如果没有传入`el`选项，则不进入下一个生命周期阶段，需要用户手动执行`vm.$mount`方法才进入下一个生命周期阶段。

以上就是`new Vue()`所做的所有事情，可以看到，整个初始化阶段都是在`new Vue()`里完成的，关于`new Vue()`里调用的一些初始化函数具体是如何进行初始化的，我们将在接下来的几篇文章里逐一介绍。下面我们先来看看上文中遗留的属性合并及`callHook`函数是如何触发生命周期的钩子的问题。

### 合并属性

在上文中，`_init`方法里首先会调用`mergeOptions`函数来进行属性合并，如下：

```javascript
vm.$options = mergeOptions(
    resolveConstructorOptions(vm.constructor),
    options || {},
    vm
)
```



 它实际上就是把 `resolveConstructorOptions(vm.constructor)` 的返回值和 `options` 做合并，`resolveConstructorOptions` 的实现先不考虑，可简单理解为返回 `vm.constructor.options`，相当于 `Vue.options`，那么这个 `Vue.options`又是什么呢，其实在 `initGlobalAPI(Vue)` 的时候定义了这个值，代码在 `src/core/global-api/index.js` 中：

```javascript
export function initGlobalAPI (Vue: GlobalAPI) {
  // ...
  Vue.options = Object.create(null)
  ASSET_TYPES.forEach(type => {
    Vue.options[type + 's'] = Object.create(null)
  })

  extend(Vue.options.components, builtInComponents)
  // ...
}
```

 首先通过 `Vue.options = Object.create(null)` 创建一个空对象，然后遍历 `ASSET_TYPES`，`ASSET_TYPES` 的定义在 `src/shared/constants.js` 中：

```javascript
export const ASSET_TYPES = [
  'component',
  'directive',
  'filter'
]
```

所以上面遍历 `ASSET_TYPES` 后的代码相当于：

```js
Vue.options.components = {}
Vue.options.directives = {}
Vue.options.filters = {}
```

最后通过 `extend(Vue.options.components, builtInComponents)` 把一些内置组件扩展到 `Vue.options.components` 上，`Vue` 的内置组件目前 有`<keep-alive>`、`<transition>` 和`<transition-group>` 组件，这也就是为什么我们在其它组件中使用这些组件不需要注册的原因。

 那么回到 `mergeOptions` 这个函数，它的定义在 `src/core/util/options.js` 中：

```javascript
/**
 * Merge two option objects into a new one.
 * Core utility used in both instantiation and inheritance.
 */
export function mergeOptions (
  parent: Object,
  child: Object,
  vm?: Component
): Object {

  if (typeof child === 'function') {
    child = child.options
  }
  const extendsFrom = child.extends
  if (extendsFrom) {
    parent = mergeOptions(parent, extendsFrom, vm)
  }
  if (child.mixins) {
    for (let i = 0, l = child.mixins.length; i < l; i++) {
      parent = mergeOptions(parent, child.mixins[i], vm)
    }
  }
  const options = {}
  let key
  for (key in parent) {
    mergeField(key)
  }
  for (key in child) {
    if (!hasOwn(parent, key)) {
      mergeField(key)
    }
  }
  function mergeField (key) {
    const strat = strats[key] || defaultStrat
    options[key] = strat(parent[key], child[key], vm, key)
  }
  return options
}
```

可以看出，`mergeOptions`函数的 主要功能是把 `parent` 和 `child` 这两个对象根据一些合并策略，合并成一个新对象并返回。首先递归把 `extends` 和 `mixins` 合并到 `parent` 上，

```javascript
 const extendsFrom = child.extends
  if (extendsFrom) {
    parent = mergeOptions(parent, extendsFrom, vm)
  }
  if (child.mixins) {
    for (let i = 0, l = child.mixins.length; i < l; i++) {
      parent = mergeOptions(parent, child.mixins[i], vm)
    }
  }
```

然后创建一个空对象`options`，遍历 `parent`，把`parent`中的每一项通过调用 `mergeField`函数合并到空对象`options`里，

```javascript
const options = {}
let key
for (key in parent) {
    mergeField(key)
}
```

接着再遍历 `child`，把存在于`child`里但又不在 `parent`中 的属性继续调用 `mergeField`函数合并到空对象`options`里，

```javascript
for (key in child) {
    if (!hasOwn(parent, key)) {
        mergeField(key)
    }
}
```

最后，`options`就是最终合并后得到的结果，将其返回。

这里值得一提的是 `mergeField` 函数，它不是简单的把属性从一个对象里复制到另外一个对象里，而是根据被合并的不同的选项有着不同的合并策略。例如，对于`data`有`data`的合并策略，即该文件中的`strats.data`函数；对于`watch`有`watch`的合并策略，即该文件中的`strats.watch`函数等等。这就是设计模式中非常典型的**策略模式**。

关于这些合并策略都很简单，我们不一一展开介绍，仅介绍生命周期钩子函数的合并策略，因为我们后面会用到。生命周期钩子函数的合并策略如下：

```javascript
/**
 * Hooks and props are merged as arrays.
 */
function mergeHook (parentVal,childVal):  {
  return childVal
    ? parentVal
      ? parentVal.concat(childVal)
      : Array.isArray(childVal)
        ? childVal
        : [childVal]
    : parentVal
}

LIFECYCLE_HOOKS.forEach(hook => {
  strats[hook] = mergeHook
})
```

 这其中的 `LIFECYCLE_HOOKS` 的定义在 `src/shared/constants.js` 中：

```javascript
export const LIFECYCLE_HOOKS = [
  'beforeCreate',
  'created',
  'beforeMount',
  'mounted',
  'beforeUpdate',
  'updated',
  'beforeDestroy',
  'destroyed',
  'activated',
  'deactivated',
  'errorCaptured'
]
```

 这里定义了所有钩子函数名称，所以对于钩子函数的合并策略都是 `mergeHook` 函数。`mergeHook` 函数的实现用了一个多层嵌套的三元运算符，如果嵌套太深不好理解的话我们可以将其展开，如下：

 ```javascript
function mergeHook (parentVal,childVal):  {
  if (childVal) {
    if (parentVal) {
      return parentVal.concat(childVal)
    } else {
      if (Array.isArray(childVal)) {
        return childVal
      } else {
        return [childVal]
      }
    }
  } else {
    return parentVal
  }
}
 ```

 从展开后的代码中可以看到，它的合并策略是这样子的：如果 `childVal`不存在，就返回 `parentVal`；否则再判断是否存在 `parentVal`，如果存在就把 `childVal` 添加到 `parentVal` 后返回新数组；否则返回 `childVal` 的数组。所以回到 `mergeOptions` 函数，一旦 `parent` 和 `child` 都定义了相同的钩子函数，那么它们会把 2 个钩子函数合并成一个数组。

那么问题来了，为什么要把相同的钩子函数转换成数组呢？这是因为`Vue`允许用户使用`Vue.mixin`方法（关于该方法会在后面章节中介绍）向实例混入自定义行为，`Vue`的一些插件通常都是这么做的。所以当`Vue.mixin`和用户在实例化`Vue`时，如果设置了同一个钩子函数，那么在触发钩子函数时，就需要同时触发这个两个函数，所以转换成数组就是为了能在同一个生命周期钩子列表中保存多个钩子函数。

### callHook函数如何触发钩子函数

关于`callHook`函数如何触发钩子函数的问题，我们只需看一下该函数的实现源码即可，该函数的源码位于`src/core/instance/lifecycle.js` 中，如下：

```javascript
export function callHook (vm: Component, hook: string) {
  const handlers = vm.$options[hook]
  if (handlers) {
    for (let i = 0, j = handlers.length; i < j; i++) {
      try {
        handlers[i].call(vm)
      } catch (e) {
        handleError(e, vm, `${hook} hook`)
      }
    }
  }
}
```

可以看到，`callHook`函数逻辑非常简单。首先从实例的`$options`中获取到需要触发的钩子名称所对应的钩子函数数组`handlers`，我们说过，每个生命周期钩子名称都对应了一个钩子函数数组。然后遍历该数组，将数组中的每个钩子函数都执行一遍。

### 总结

本篇文章介绍了生命周期第一个阶段——初始化阶段中所做的第一件事：`new Vue()`。

首先，分析了`new Vue()`时其内部都干了些什么。其主要逻辑就是：合并配置，调用一些初始化函数，触发生命周期钩子函数，调用`$mount`开启下一个阶段。

接着，就合并属性进行了详细介绍，知道了对于不同的选项有着不同的合并策略，并挑出钩子函数的合并策略进行了分析。

最后，分析了`callHook`函数的源码，知道了`callHook`函数如何触发钩子函数的。

接下来后面几篇文章将对调用的这些初始化函数进行逐个分析。

## 初始化阶段(initLifecycle)


### 前言

在上篇文章中，我们介绍了生命周期初始化阶段的整体工作流程，以及在该阶段都做了哪些事情。我们知道了，在该阶段会调用一些初始化函数，对`Vue`实例的属性、数据等进行初始化工作。那这些初始化函数都初始化了哪些东西以及都怎么初始化的呢？接下来我们就把这些初始化函数一一展开介绍，本篇文章介绍第一个初始化函数`initLifecycle`。

### initLifecycle函数分析

`initLifecycle`函数的定义位于源码的`src/core/instance/lifecycle.js`中，其代码如下：

```javascript
export function initLifecycle (vm: Component) {
  const options = vm.$options

  // locate first non-abstract parent
  let parent = options.parent
  if (parent && !options.abstract) {
    while (parent.$options.abstract && parent.$parent) {
      parent = parent.$parent
    }
    parent.$children.push(vm)
  }

  vm.$parent = parent
  vm.$root = parent ? parent.$root : vm

  vm.$children = []
  vm.$refs = {}

  vm._watcher = null
  vm._inactive = null
  vm._directInactive = false
  vm._isMounted = false
  vm._isDestroyed = false
  vm._isBeingDestroyed = false
}
```

可以看到，`initLifecycle`函数的代码量并不多，逻辑也不复杂。其主要是给`Vue`实例上挂载了一些属性并设置了默认值，值得一提的是挂载`$parent` 属性和`$root`属性， 下面我们就来逐个分析。

首先是给实例上挂载`$parent`属性，这个属性有点意思，我们先来看看代码：

```javascript
let parent = options.parent
if (parent && !options.abstract) {
  while (parent.$options.abstract && parent.$parent) {
    parent = parent.$parent
  }
  parent.$children.push(vm)
}

vm.$parent = parent
```

从代码中可以看到，逻辑是这样子的：如果当前组件不是抽象组件并且存在父级，那么就通过`while`循环来向上循环，如果当前组件的父级是抽象组件并且也存在父级，那就继续向上查找当前组件父级的父级，直到找到第一个不是抽象类型的父级时，将其赋值`vm.$parent`，同时把该实例自身添加进找到的父级的`$children`属性中。这样就确保了在子组件的`$parent`属性上能访问到父组件实例，在父组件的`$children`属性上也能访问子组件的实例。

接着是给实例上挂载`$root`属性，如下：

```javascript
vm.$root = parent ? parent.$root : vm
```

实例的`$root`属性表示当前实例的根实例，挂载该属性时，首先会判断如果当前实例存在父级，那么当前实例的根实例`$root`属性就是其父级的根实例`$root`属性，如果不存在，那么根实例`$root`属性就是它自己。这很好理解，举个例子：假如有一个人，他如果有父亲，那么他父亲的祖先肯定也是他的祖先，同理，他的儿子的祖先也肯定是他的祖先，我们不需要真正的一层一层的向上递归查找到他祖先本人，只需要知道他父亲的祖先是谁然后告诉他即可。如果他没有父亲，那说明他自己就是祖先，那么他后面的儿子、孙子的`$root`属性就是他自己了。

这就是一个自上到下将根实例的`$root`属性依次传递给每一个子实例的过程。

最后，再初始化了一些其它属性，因为都是简单的赋初始值，这里就不再一一介绍，等后面内容涉及到的时候再介绍。

```javascript
vm.$children = []
vm.$refs = {}

vm._watcher = null
vm._inactive = null
vm._directInactive = false
vm._isMounted = false
vm._isDestroyed = false
vm._isBeingDestroyed = false
```

### 总结

本篇文章介绍了初始化阶段调用的第一个初始化函数——`initLifecycle`函数。该函数的逻辑非常简单，就是给实例初始化了一些属性，包括以`$`开头的供用户使用的外部属性，也包括以`_`开头的供内部使用的内部属性。

## 初始化阶段(initEvents)


### 前言

本篇文章介绍生命周期初始化阶段所调用的第二个初始化函数——`initEvents`。从函数名字上来看，这个初始化函数是初始化实例的事件系统。我们知道，在`Vue`中，当我们在父组件中使用子组件时可以给子组件上注册一些事件，这些事件即包括使用`v-on`或`@`注册的自定义事件，也包括注册的浏览器原生事件（需要加 `.native` 修饰符），如下：

```html
<child @select="selectHandler" 	@click.native="clickHandler"></child>
```

不管是什么事件，当子组件（即实例）在初始化的时候都需要进行一定的初始化，那么本篇文章就来看看实例上的事件都是如何进行初始化的。

### 解析事件

我们先从解析事件开始说起，回顾之前的模板编译解析中，当遇到开始标签的时候，除了会解析开始标签，还会调用`processAttrs` 方法解析标签中的属性，`processAttrs` 方法位于源码的 `src/compiler/parser/index.js`中， 如下：

```javascript
export const onRE = /^@|^v-on:/
export const dirRE = /^v-|^@|^:/

function processAttrs (el) {
  const list = el.attrsList
  let i, l, name, value, modifiers
  for (i = 0, l = list.length; i < l; i++) {
    name  = list[i].name
    value = list[i].value
    if (dirRE.test(name)) {
      // 解析修饰符
      modifiers = parseModifiers(name)
      if (modifiers) {
        name = name.replace(modifierRE, '')
      }
      if (onRE.test(name)) { // v-on
        name = name.replace(onRE, '')
        addHandler(el, name, value, modifiers, false, warn)
      }
    }
  }
}
```

从上述代码中可以看到，在对标签属性进行解析时，判断如果属性是指令，首先通过 `parseModifiers` 解析出属性的修饰符，然后判断如果是事件的指令，则执行 `addHandler(el, name, value, modifiers, false, warn)` 方法，  该方法定义在 `src/compiler/helpers.js` 中，如下：

```javascript
export function addHandler (el,name,value,modifiers) {
  modifiers = modifiers || emptyObject

  // check capture modifier 判断是否有capture修饰符
  if (modifiers.capture) {
    delete modifiers.capture
    name = '!' + name // 给事件名前加'!'用以标记capture修饰符
  }
  // 判断是否有once修饰符
  if (modifiers.once) {
    delete modifiers.once
    name = '~' + name // 给事件名前加'~'用以标记once修饰符
  }
  // 判断是否有passive修饰符
  if (modifiers.passive) {
    delete modifiers.passive
    name = '&' + name // 给事件名前加'&'用以标记passive修饰符
  }

  let events
  if (modifiers.native) {
    delete modifiers.native
    events = el.nativeEvents || (el.nativeEvents = {})
  } else {
    events = el.events || (el.events = {})
  }

  const newHandler: any = {
    value: value.trim()
  }
  if (modifiers !== emptyObject) {
    newHandler.modifiers = modifiers
  }

  const handlers = events[name]
  if (Array.isArray(handlers)) {
    handlers.push(newHandler)
  } else if (handlers) {
    events[name] = [handlers, newHandler]
  } else {
    events[name] = newHandler
  }

  el.plain = false
}
```

在`addHandler` 函数里做了 3 件事情，首先根据 `modifier` 修饰符对事件名 `name` 做处理，接着根据 `modifier.native` 判断事件是一个浏览器原生事件还是自定义事件，分别对应 `el.nativeEvents` 和 `el.events`，最后按照 `name` 对事件做归类，并把回调函数的字符串保留到对应的事件中。

 在前言中的例子中，父组件的 `child` 节点生成的 `el.events` 和 `el.nativeEvents` 如下：

```javascript
el.events = {
  select: {
    value: 'selectHandler'
  }
}

el.nativeEvents = {
  click: {
    value: 'clickHandler'
  }
}
```

 然后在模板编译的代码生成阶段，会在 `genData` 函数中根据 `AST` 元素节点上的 `events` 和 `nativeEvents` 生成`_c(tagName,data,children)`函数中所需要的 `data` 数据，它的定义在 `src/compiler/codegen/index.js` 中：

```javascript
export function genData (el state) {
  let data = '{'
  // ...
  if (el.events) {
    data += `${genHandlers(el.events, false,state.warn)},`
  }
  if (el.nativeEvents) {
    data += `${genHandlers(el.nativeEvents, true, state.warn)},`
  }
  // ...
  return data
}
```

生成的`data`数据如下：

```javascript
{
  // ...
  on: {"select": selectHandler},
  nativeOn: {"click": function($event) {
      return clickHandler($event)
    }
  }
  // ...
}
```

可以看到，最开始的模板中标签上注册的事件最终会被解析成用于创建元素型`VNode`的`_c(tagName,data,children)`函数中`data`数据中的两个对象，自定义事件对象`on`，浏览器原生事件`nativeOn`。

在前面的文章中我们说过，模板编译的最终目的是创建`render`函数供挂载的时候调用生成虚拟`DOM`，那么在挂载阶段， 如果被挂载的节点是一个组件节点，则通过 `createComponent` 函数创建一个组件 `vnode`，该函数位于源码的 `src/core/vdom/create-component.js` 中， 如下：

```javascript
export function createComponent (
  Ctor: Class<Component> | Function | Object | void,
  data: ?VNodeData,
  context: Component,
  children: ?Array<VNode>,
  tag?: string
): VNode | Array<VNode> | void {
  // ...
  const listeners = data.on

  data.on = data.nativeOn

  // ...
  const name = Ctor.options.name || tag
  const vnode = new VNode(
    `vue-component-${Ctor.cid}${name ? `-${name}` : ''}`,
    data, undefined, undefined, undefined, context,
    { Ctor, propsData, listeners, tag, children },
    asyncFactory
  )

  return vnode
}
```

可以看到，把 自定义事件`data.on` 赋值给了 `listeners`，把浏览器原生事件 `data.nativeOn` 赋值给了 `data.on`，这说明所有的原生浏览器事件处理是在当前父组件环境中处理的。而对于自定义事件，会把 `listeners` 作为 `vnode` 的 `componentOptions` 传入，放在子组件初始化阶段中处理， 在子组件的初始化的时候，  拿到了父组件传入的 `listeners`，然后在执行 `initEvents` 的过程中，会处理这个 `listeners`。

所以铺垫了这么多，结论来了：**父组件给子组件的注册事件中，把自定义事件传给子组件，在子组件实例化的时候进行初始化；而浏览器原生事件是在父组件中处理。**

换句话说：**实例初始化阶段调用的初始化事件函数`initEvents`实际上初始化的是父组件在模板中使用v-on或@注册的监听子组件内触发的事件。**

###   initEvents函数分析

了解了以上过程之后，我们终于进入了正题，开始分析`initEvents`函数，该函数位于源码的`src/instance/events.js`中，如下：

```javascript
export function initEvents (vm: Component) {
  vm._events = Object.create(null)
  // init parent attached events
  const listeners = vm.$options._parentListeners
  if (listeners) {
    updateComponentListeners(vm, listeners)
  }
}
```

可以看到，`initEvents`函数逻辑非常简单，首先在`vm`上新增`_events`属性并将其赋值为空对象，用来存储事件。

```javascript
vm._events = Object.create(null)
```

接着，获取父组件注册的事件赋给`listeners`，如果`listeners`不为空，则调用`updateComponentListeners`函数，将父组件向子组件注册的事件注册到子组件的实例中，如下：

```javascript
const listeners = vm.$options._parentListeners
if (listeners) {
  updateComponentListeners(vm, listeners)
}
```

这个`updateComponentListeners`函数是什么呢？该函数定义如下：

```javascript
export function updateComponentListeners (
  vm: Component,
  listeners: Object,
  oldListeners: ?Object
) {
  target = vm
  updateListeners(listeners, oldListeners || {}, add, remove, vm)
  target = undefined
}

function add (event, fn, once) {
  if (once) {
    target.$once(event, fn)
  } else {
    target.$on(event, fn)
  }
}

function remove (event, fn) {
  target.$off(event, fn)
}
```

可以看到，`updateComponentListeners`函数其实也没有干什么，只是调用了`updateListeners`函数，并把`listeners`以及`add`和`remove`这两个函数传入。我们继续跟进，看看`updateListeners`函数干了些什么，`updateListeners`函数位于源码的`src/vdom/helpers/update-listeners.js`中，如下：

```javascript
export function updateListeners (
  on: Object,
  oldOn: Object,
  add: Function,
  remove: Function,
  vm: Component
) {
  let name, def, cur, old, event
  for (name in on) {
    def = cur = on[name]
    old = oldOn[name]
    event = normalizeEvent(name)
    if (isUndef(cur)) {
      process.env.NODE_ENV !== 'production' && warn(
        `Invalid handler for event "${event.name}": got ` + String(cur),
        vm
      )
    } else if (isUndef(old)) {
      if (isUndef(cur.fns)) {
        cur = on[name] = createFnInvoker(cur)
      }
      add(event.name, cur, event.once, event.capture, event.passive, event.params)
    } else if (cur !== old) {
      old.fns = cur
      on[name] = old
    }
  }
  for (name in oldOn) {
    if (isUndef(on[name])) {
      event = normalizeEvent(name)
      remove(event.name, oldOn[name], event.capture)
    }
  }
}

```

可以看到，该函数的作用是对比`listeners`和`oldListeners`的不同，并调用参数中提供的`add`和`remove`进行相应的注册事件和卸载事件。其思想是：如果`listeners`对象中存在某个`key`（即事件名）而`oldListeners`中不存在，则说明这个事件是需要新增的；反之，如果`oldListeners`对象中存在某个`key`（即事件名）而`listeners`中不存在，则说明这个事件是需要从事件系统中卸载的；

该函数接收5个参数，分别是`on`、`oldOn`、`add`、`remove`、`vm`，其中`on`对应`listeners`，`oldOn`对应`oldListeners`。

首先对`on`进行遍历， 获得每一个事件名，然后调用 `normalizeEvent` 函数（关于该函数下面会介绍）处理， 处理完事件名后， 判断事件名对应的值是否存在，如果不存在则抛出警告，如下：

```javascript
for (name in on) {
  def = cur = on[name]
  old = oldOn[name]
  event = normalizeEvent(name)
  if (isUndef(cur)) {
    process.env.NODE_ENV !== 'production' && warn(
      `Invalid handler for event "${event.name}": got ` + String(cur),
      vm
    )
  }
}
```

如果存在，则继续判断该事件名在`oldOn`中是否存在，如果不存在，则调用`add`注册事件，如下：

```javascript
if (isUndef(old)) {
  if (isUndef(cur.fns)) {
    cur = on[name] = createFnInvoker(cur)
  }
  add(event.name, cur, event.once, event.capture, event.passive, event.params)
}
```

这里定义了 `createFnInvoker` 方法并返回`invoker`函数:

```javascript
export function createFnInvoker (fns) {
  function invoker () {
    const fns = invoker.fns
    if (Array.isArray(fns)) {
      const cloned = fns.slice()
      for (let i = 0; i < cloned.length; i++) {
        cloned[i].apply(null, arguments)
      }
    } else {
      // return handler return value for single handlers
      return fns.apply(null, arguments)
    }
  }
  invoker.fns = fns
  return invoker
}
```

 由于一个事件可能会对应多个回调函数，所以这里做了数组的判断，多个回调函数就依次调用。注意最后的赋值逻辑， `invoker.fns = fns`，每一次执行 `invoker` 函数都是从 `invoker.fns` 里取执行的回调函数，回到 `updateListeners`，当我们第二次执行该函数的时候，判断如果 `cur !== old`，那么只需要更改 `old.fns = cur` 把之前绑定的 `involer.fns` 赋值为新的回调函数即可，并且 通过 `on[name] = old` 保留引用关系，这样就保证了事件回调只添加一次，之后仅仅去修改它的回调函数的引用。

```javascript
if (cur !== old) {
  old.fns = cur
  on[name] = old
}
```

 最后遍历 `oldOn`， 获得每一个事件名，判断如果事件名在`on`中不存在，则表示该事件是需要从事件系统中卸载的事件，则调用 `remove`方法卸载该事件。

 以上就是`updateListeners`函数的所有逻辑，那么上面还遗留了一个`normalizeEvent` 函数是干什么用的呢？还记得我们在解析事件的时候，当事件上有修饰符的时候，我们会根据不同的修饰符给事件名前面添加不同的符号以作标识，其实这个`normalizeEvent` 函数就是个反向操作，根据事件名前面的不同标识反向解析出该事件所带的何种修饰符，其代码如下：

```javascript
const normalizeEvent = cached((name: string): {
  name: string,
  once: boolean,
  capture: boolean,
  passive: boolean,
  handler?: Function,
  params?: Array<any>
} => {
  const passive = name.charAt(0) === '&'
  name = passive ? name.slice(1) : name
  const once = name.charAt(0) === '~'
  name = once ? name.slice(1) : name
  const capture = name.charAt(0) === '!'
  name = capture ? name.slice(1) : name
  return {
    name,
    once,
    capture,
    passive
  }
})
```

可以看到，就是判断事件名的第一个字符是何种标识进而判断出事件带有何种修饰符，最终将真实事件名及所带的修饰符返回。

### 总结

本篇文章介绍了生命周期初始化阶段所调用的第二个初始化函数——`initEvents`。该函数是用来初始化实例的事件系统的。

我们先从模板编译时对组件标签上的事件解析入手分析，我们知道了，父组件既可以给子组件上绑定自定义事件，也可以绑定浏览器原生事件。这两种事件有着不同的处理时机，浏览器原生事件是由父组件处理，而自定义事件是在子组件初始化的时候由父组件传给子组件，再由子组件注册到实例的事件系统中。

也就是说：**初始化事件函数initEvents实际上初始化的是父组件在模板中使用v-on或@注册的监听子组件内触发的事件。**

最后分析了`initEvents`函数的具体实现过程，该函数内部首先在实例上新增了`_events`属性并将其赋值为空对象，用来存储事件。接着通过调用`updateComponentListeners`函数，将父组件向子组件注册的事件注册到子组件实例中的`_events`对象里。

## 初始化阶段(initInjections)


### 前言

本篇文章介绍生命周期初始化阶段所调用的第四个初始化函数——`initInjections`。从函数名字上来看，该函数是用来初始化实例中的`inject`选项的。说到`inject`选项，那必然离不开`provide`选项，这两个选项都是成对出现的，它们的作用是：允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在起上下游关系成立的时间里始终生效。并且

`provide` 选项应该是一个对象或返回一个对象的函数。该对象包含可注入其子孙的属性。在该对象中你可以使用 ES2015 Symbols 作为 key，但是只在原生支持 `Symbol` 和 `Reflect.ownKeys` 的环境下可工作。

`inject` 选项应该是：

- 一个字符串数组，或
- 一个对象，对象的 key 是本地的绑定名，value 是：
  - 在可用的注入内容中搜索用的 key (字符串或 Symbol)，或
  - 一个对象，该对象的：
    - `from` 属性是在可用的注入内容中搜索用的 key (字符串或 Symbol)
    - `default` 属性是降级情况下使用的 value

这两个选项在我们日常开发中使用的频率不是很高，但是在一些组件库中使用的很频繁，官方文档给出了使用示例，如下：

```javascript
// 父级组件提供 'foo'
var Parent = {
  provide: {
    foo: 'bar'
  },
  // ...
}

// 子组件注入 'foo'
var Child = {
  inject: ['foo'],
  created () {
    console.log(this.foo) // => "bar"
  }
  // ...
}
```

利用 ES2015 Symbols、函数 `provide` 和对象 `inject`：

```javascript
const s = Symbol()

const Provider = {
  provide () {
    return {
      [s]: 'foo'
    }
  }
}

const Child = {
  inject: { s },
  // ...
}
```

> 接下来 2 个例子只工作在 Vue 2.2.1 或更高版本。低于这个版本时，注入的值会在 `props` 和 `data` 初始化之后得到。

使用一个注入的值作为一个属性的默认值：

```javascript
const Child = {
  inject: ['foo'],
  props: {
    bar: {
      default () {
        return this.foo
      }
    }
  }
}
```

使用一个注入的值作为数据入口：

```javascript
const Child = {
  inject: ['foo'],
  data () {
    return {
      bar: this.foo
    }
  }
}
```

> 在 2.5.0+ 的注入可以通过设置默认值使其变成可选项：

```javascript
const Child = {
  inject: {
    foo: { default: 'foo' }
  }
}
```

如果它需要从一个不同名字的属性注入，则使用 `from` 来表示其源属性：

```javascript
const Child = {
  inject: {
    foo: {
      from: 'bar',
      default: 'foo'
    }
  }
}
```

与 prop 的默认值类似，你需要对非原始值使用一个工厂方法：

```javascript
const Child = {
  inject: {
    foo: {
      from: 'bar',
      default: () => [1, 2, 3]
    }
  }
}
```

总结起来一句话就是：父组件可以使用`provide`选项给自己的下游子孙组件内注入一些数据，在下游子孙组件中可以使用`inject`选项来接收这些数据以便为自己所用。

另外，这里有一点需要注意：`provide` 和 `inject` 选项绑定的数据不是响应式的。

了解了他们的作用及使用方法后，我们就来看下`initInjections`函数是如何来初始化`inject`选项的。

### initInjections函数分析

分析之前，我们先说一个问题，细心的同学可能会发现，既然`inject`选项和`provide`选项都是成对出现的，那为什么在初始化的时候不一起初始化呢？为什么在`init`函数中调用`initInjections`函数和`initProvide`函数之间穿插一个`initState`函数呢？

其实不然，在官方文档示例中说了，`provide`选项注入的值作为数据入口，如下：

```javascript
const Child = {
  inject: ['foo'],
  data () {
    return {
      bar: this.foo
    }
  }
}
```

这里所说的数据就是我们通常所写`data`、`props`、`watch`、`computed`及`method`，所以`inject`选项接收到注入的值有可能被以上这些数据所使用到，所以在初始化完`inject`后需要先初始化这些数据，然后才能再初始化`provide`，所以在调用`initInjections`函数对`inject`初始化完之后需要先调用`initState`函数对数据进行初始化，最后再调用`initProvide`函数对`provide`进行初始化。

OK，接下来我们就来分析`initInjections`函数的具体原理，该函数定义位于源码的`src/core/instance/inject.js`中，如下：

```javascript
export function initInjections (vm: Component) {
  const result = resolveInject(vm.$options.inject, vm)
  if (result) {
    toggleObserving(false)
    Object.keys(result).forEach(key => {
      defineReactive(vm, key, result[key])
    }
    toggleObserving(true)
  }
}

export let shouldObserve: boolean = true
export function toggleObserving (value: boolean) {
  shouldObserve = value
}
```

可以看到，`initInjections`函数的逻辑并不复杂，首先调用`resolveInject`把`inject`选项中的数据转化成键值对的形式赋给`result`，如官方文档给出的例子，那么`result`应为如下样子：

```javascript
// 父级组件提供 'foo'
var Parent = {
  provide: {
    foo: 'bar'
  }
}

// 子组件注入 'foo'
var Child = {
  inject: ['foo'],
}

// result
result = {
    'foo':'bar'
}
```

然后遍历`result`中的每一对键值，调用`defineReactive`函数将其添加当前实例上，如下：

```javascript
if (result) {
    toggleObserving(false)
    Object.keys(result).forEach(key => {
        defineReactive(vm, key, result[key])
    }
    toggleObserving(true)
}
```

此处有一个地方需要注意，在把`result`中的键值添加到当前实例上之前，会先调用`toggleObserving(false)`，而这个函数内部是把`shouldObserve = false`，这是为了告诉`defineReactive`函数仅仅是把键值添加到当前实例上而不需要将其转换成响应式，这个就呼应了官方文档在介绍`provide` 和 `inject` 选项用法的时候所提示的：

> `provide` 和 `inject` 绑定并不是可响应的。这是刻意为之的。然而，如果你传入了一个可监听的对象，那么其对象的属性还是可响应的。

`initInjections`函数的逻辑就介绍完了，接下来我们看看`resolveInject`函数内部是如何把`inject` 选项中数据转换成键值对的。

#### olveInject函数分析

我们知道，`inject` 选项中的每一个数据`key`都是由其上游父级组件提供的，所以我们应该把每一个数据`key`从当前组件起，不断的向上游父级组件中查找该数据`key`对应的值，直到找到为止。如果在上游所有父级组件中没找到，那么就看在`inject` 选项是否为该数据`key`设置了默认值，如果设置了就使用默认值，如果没有设置，则抛出异常。

OK，以上是我们的分析，下面我们就来看下`resolveInject`函数的源码，验证我们的分析，源码如下：

```javascript
export function resolveInject (inject: any, vm: Component): ?Object {
  if (inject) {
    const result = Object.create(null)
    const keys =  Object.keys(inject)

    for (let i = 0; i < keys.length; i++) {
      const key = keys[i]
      const provideKey = inject[key].from
      let source = vm
      while (source) {
        if (source._provided && hasOwn(source._provided, provideKey)) {
          result[key] = source._provided[provideKey]
          break
        }
        source = source.$parent
      }
      if (!source) {
        if ('default' in inject[key]) {
          const provideDefault = inject[key].default
          result[key] = typeof provideDefault === 'function'
            ? provideDefault.call(vm)
            : provideDefault
        } else if (process.env.NODE_ENV !== 'production') {
          warn(`Injection "${key}" not found`, vm)
        }
      }
    }
    return result
  }
}
```

在分析函数源码之前，我们对照着官网给出的示例，这样会比较好理解一些。

```javascript
var Parent = {
  provide: {
    foo: 'bar'
  },
  // ...
}
const Child = {
  inject: {
    foo: {
      from: 'bar',
      default: () => [1, 2, 3]
    }
  }
}
```



可以看到，在函数源码中，首先创建一个空对象`result`，用来存储`inject` 选项中的数据`key`及其对应的值，作为最后的返回结果。

然后获取当前`inject` 选项中的所有`key`，然后遍历每一个`key`，拿到每一个`key`的`from`属性记作`provideKey`，`provideKey`就是上游父级组件提供的源属性，然后开启一个`while`循环，从当前组件起，不断的向上游父级组件的`_provided`属性中（父级组件使用`provide`选项注入数据时会将注入的数据存入自己的实例的`_provided`属性中）查找，直到查找到源属性的对应的值，将其存入`result`中，如下：

```javascript
for (let i = 0; i < keys.length; i++) {
  const key = keys[i]
  const provideKey = inject[key].from
  let source = vm
  while (source) {
    if (source._provided && hasOwn(source._provided, provideKey)) {
      result[key] = source._provided[provideKey]
      break
    }
    source = source.$parent
  }
}
```

如果没有找到，那么就看`inject` 选项中当前的数据`key`是否设置了默认值，即是否有`default`属性，如果有的话，则拿到这个默认值，官方文档示例中说了，默认值可以为一个工厂函数，所以当默认值是函数的时候，就去该函数的返回值，否则就取默认值本身。如果没有设置默认值，则抛出异常。如下：

```javascript
if (!source) {
  if ('default' in inject[key]) {
    const provideDefault = inject[key].default
    result[key] = typeof provideDefault === 'function'
        ? provideDefault.call(vm)
    : provideDefault
  } else if (process.env.NODE_ENV !== 'production') {
    warn(`Injection "${key}" not found`, vm)
  }
}
```

最后将`result`返回。这就是`resolveInject`函数的所有逻辑。

此时你可能会有个疑问，官方文档中说`inject` 选项可以是一个字符串数组，也可以是一个对象，在上面的代码中只看见了处理当为对象的情况，那如果是字符串数组呢？怎么没有处理呢？

其实在初始化阶段`_init`函数在合并属性的时候还调用了一个将`inject` 选项数据规范化的函数`normalizeInject`，该函数的作用是将以下这三种写法：

```javascript
// 写法一
var Child = {
  inject: ['foo']
}

// 写法二
const Child = {
  inject: {
    foo: { default: 'xxx' }
  }
}

// 写法三
const Child = {
  inject: {
    foo
  }
}
```

统统转换成以下规范化格式：

```javascript
const Child = {
  inject: {
    foo: {
      from: 'foo',
      default: 'xxx'  //如果有默认的值就有default属性
    }
  }
}
```

这样做的目的是，不管用户使用了何种写法，统统将其转化成一种便于集中处理的写法。

该函数的定义位于源码的`src/core/util/options.js`中，如下：

```javascript
function normalizeInject (options: Object, vm: ?Component) {
  const inject = options.inject
  if (!inject) return
  const normalized = options.inject = {}
  if (Array.isArray(inject)) {
    for (let i = 0; i < inject.length; i++) {
      normalized[inject[i]] = { from: inject[i] }
    }
  } else if (isPlainObject(inject)) {
    for (const key in inject) {
      const val = inject[key]
      normalized[key] = isPlainObject(val)
        ? extend({ from: key }, val)
        : { from: val }
    }
  } else if (process.env.NODE_ENV !== 'production') {
    warn(
      `Invalid value for option "inject": expected an Array or an Object, ` +
      `but got ${toRawType(inject)}.`,
      vm
    )
  }
}
```

该函数的逻辑并不复杂，如果用户给`inject`选项传入的是一个字符串数组（写法一），那么就遍历该数组，把数组的每一项变成

```javascript
inject:{
  foo:{
    from:'foo'
  }
}
```

如果给`inject`选项传入的是一个对象，那就遍历对象中的每一个`key`，给写法二形式的`key`对应的值扩展`{ from: key }`，变成：

```javascript
inject:{
  foo:{
    from: 'foo',
    default: 'xxx'
  }
}
```

将写法三形式的`key`对应的值变成：

```javascript
inject:{
  foo:{
    from: 'foo'
  }
}
```

总之一句话就是把各种写法转换成一种规范化写法，便于集中处理。

### 总结

本篇文章介绍生命周期初始化阶段所调用的第四个初始化函数——`initInjections`。该函数是用来初始化`inject`选项的。

由于`inject`选项在日常开发中使用频率不高，所以首先我们先根据官方文档回顾了该选项的作用及使用方法。

接着，我们分析了`initInjections`函数的内部实现原理，分析了是根据`inject`选项中的数据`key`是如何自底向上查找上游父级组件所注入的对应的值。

另外，对`inject`选项的规范化函数`normalizeInject`也进行了分析，`Vue`为用户提供了自由多种的写法，其内部是将各种写法最后进行统一规范化处理。


## 初始化阶段(initState)


### 前言

 本篇文章介绍生命周期初始化阶段所调用的第五个初始化函数——`initState`。 从函数名字上来看，这个函数是用来初始化实例状态的，那么什么是实例的状态呢？在前面文章中我们略有提及，在我们日常开发中，在`Vue`组件中会写一些如`props`、`data`、`methods`、`computed`、`watch`选项，我们把这些选项称为实例的状态选项。也就是说，`initState`函数就是用来初始化这些状态的，那么接下来我们就来分析该函数是如何初始化这些状态选项的。

### initState函数分析

首先我们先来分析`initState`函数，该函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
export function initState (vm: Component) {
  vm._watchers = []
  const opts = vm.$options
  if (opts.props) initProps(vm, opts.props)
  if (opts.methods) initMethods(vm, opts.methods)
  if (opts.data) {
    initData(vm)
  } else {
    observe(vm._data = {}, true /* asRootData */)
  }
  if (opts.computed) initComputed(vm, opts.computed)
  if (opts.watch && opts.watch !== nativeWatch) {
    initWatch(vm, opts.watch)
  }
}
```

可以看到，该函数的代码并不多，而且逻辑也非常清晰。

首先，给实例上新增了一个属性`_watchers`，用来存储当前实例中所有的`watcher`实例，无论是使用`vm.$watch`注册的`watcher`实例还是使用`watch`选项注册的`watcher`实例，都会被保存到该属性中。

这里我们再额外多说一点，在变化侦测篇中我们介绍了`Vue`中对数据变化的侦测是使用属性拦截的方式实现的，但是`Vue`并不是对所有数据都使用属性拦截的方式侦测变化，这是因为数据越多，数据上所绑定的依赖就会多，从而造成依赖追踪的内存开销就会很大，所以从`Vue 2.0`版本起，`Vue`不再对所有数据都进行侦测，而是将侦测粒度提高到了组件层面，对每个组件进行侦测，所以在每个组件上新增了`vm._watchers`属性，用来存放这个组件内用到的所有状态的依赖，当其中一个状态发生变化时，就会通知到组件，然后由组件内部使用虚拟`DOM`进行数据比对，从而降低内存开销，提高性能。

继续回到源码，接下来就是判断实例中有哪些选项就调用对应的选项初始化子函数进行初始化，如下：

```javascript
if (opts.props) initProps(vm, opts.props)
if (opts.methods) initMethods(vm, opts.methods)
if (opts.data) {
    initData(vm)
} else {
    observe(vm._data = {}, true /* asRootData */)
}
if (opts.computed) initComputed(vm, opts.computed)
if (opts.watch && opts.watch !== nativeWatch) {
    initWatch(vm, opts.watch)
}
```

先判断实例中是否有`props`选项，如果有，就调用`props`选项初始化函数`initProps`去初始化`props`选项；

再判断实例中是否有`methods`选项，如果有，就调用`methods`选项初始化函数`initMethods`去初始化`methods`选项；

接着再判断实例中是否有`data`选项，如果有，就调用`data`选项初始化函数`initData`去初始化`data`选项；如果没有，就把`data`当作空对象并将其转换成响应式；

接着再判断实例中是否有`computed`选项，如果有，就调用`computed`选项初始化函数`initComputed`去初始化`computed`选项；

最后判断实例中是否有`watch`选项，如果有，就调用`watch`选项初始化函数`initWatch`去初始化`watch`选项；

总之一句话就是：有什么选项就调用对应的选项初始化子函数去初始化什么选项。

以上就是`initState`函数的所有逻辑，其实你会发现，在函数内部初始化这5个选项的时候它的顺序是有意安排的，不是毫无章法的。如果你在开发中有注意到我们在`data`中可以使用`props`，在`watch`中可以观察`data`和`props`，之所以可以这样做，就是因为在初始化的时候遵循了这种顺序，先初始化`props`，接着初始化`data`，最后初始化`watch`。

下面我们就针对这5个状态选项对应的5个初始化子函数进行逐一分析，看看其内部分别都是如何进行初始化的。

### 初始化props

`props`选项通常是由当前组件的父级组件传入的，当父组件在调用子组件的时候，通常会把`props`属性值作为标签属性添加在子组件的标签上，如下：

```html
<Child prop1="xxx" prop2="yyy"></Child>
```

在前面文章介绍初始化事件`initEvents`函数的时候我们说了，在模板编译的时候，当解析到组件标签时会将所有的标签属性都解析出来然后在子组件实例化的时候传给子组件，当然这里面就包括`props`数据。

在子组件内部，通过`props`选项来接收父组件传来的数据，在接收的时候可以这样写：

```javascript
// 写法一
props: ['name']

// 写法二
props: {
    name: String, // [String, Number]
}

// 写法三
props: {
    name:{
		type: String
    }
}

```

可以看到，`Vue`给用户提供的`props`选项写法非常自由，根据`Vue`的惯例，写法虽多但是最终处理的时候肯定只处理一种写法，此时你肯定会想到，处理之前先对数据进行规范化，将所有写法都转化成一种写法。对，你没有猜错，同规范化事件一样，在合并属性的时候也进行了`props`数据的规范化。

####  规范化数据

`props`数据规范化函数的定义位于源码的`src/core/util/options.js`中，如下：

```javascript
function normalizeProps (options, vm) {
  const props = options.props
  if (!props) return
  const res = {}
  let i, val, name
  if (Array.isArray(props)) {
    i = props.length
    while (i--) {
      val = props[i]
      if (typeof val === 'string') {
        name = camelize(val)
        res[name] = { type: null }
      } else if (process.env.NODE_ENV !== 'production') {
        warn('props must be strings when using array syntax.')
      }
    }
  } else if (isPlainObject(props)) {
    for (const key in props) {
      val = props[key]
      name = camelize(key)
      res[name] = isPlainObject(val)
        ? val
        : { type: val }
    }
  } else if (process.env.NODE_ENV !== 'production') {
    warn(
      `Invalid value for option "props": expected an Array or an Object, ` +
      `but got ${toRawType(props)}.`,
      vm
    )
  }
  options.props = res
}
```

上面代码中，首先拿到实例中的`props`选项，如果不存在，则直接返回。

```javascript
const props = options.props
if (!props) return
```

如果存在，则定义一个空对象`res`，用来存储最终的结果。接着判断如果`props`选项是一个数组（写法一），则遍历该数组中的每一项元素，如果该元素是字符串，那么先将该元素统一转化成驼峰式命名，然后将该元素作为`key`，将`{type: null}`作为`value`存入`res`中；如果该元素不是字符串，则抛出异常。如下：

```javascript
if (Array.isArray(props)) {
    i = props.length
    while (i--) {
        val = props[i]
        if (typeof val === 'string') {
            name = camelize(val)
            res[name] = { type: null }
        } else if (process.env.NODE_ENV !== 'production') {
            warn('props must be strings when using array syntax.')
        }
    }
}
```

如果`props`选项不是数组那就继续判断是不是一个对象，如果是一个对象，那就遍历对象中的每一对键值，拿到每一对键值后，先将键名统一转化成驼峰式命名，然后判断值是否还是一个对象，如果值是对象（写法三），那么就将该键值对存入`res`中；如果值不是对象（写法二），那么就将键名作为`key`，将`{type: null}`作为`value`存入`res`中。如下：

```javascript
if (isPlainObject(props)) {
    for (const key in props) {
        val = props[key]
        name = camelize(key)
        res[name] = isPlainObject(val)
            ? val
        : { type: val }
    }
}
```

如果`props`选项既不是数组也不是对象，那么如果在非生产环境下就抛出异常，最后将`res`作为规范化后的结果重新赋值给实例的`props`选项。如下：

```javascript
if (process.env.NODE_ENV !== 'production') {
    warn(
        `Invalid value for option "props": expected an Array or an Object, ` +
        `but got ${toRawType(props)}.`,
        vm
    )
}
options.props = res
```

以上就是对`props`数据的规范化处理，可以看到，无论是三种写法的哪一种，最终都会被转化成如下写法：

```javascript
props: {
    name:{
        type: xxx
    }
}
```

####  initProps函数分析

将`props`选项规范化完成之后，接下来我们就可以来真正的初始化`props`选项了，`initProps`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function initProps (vm: Component, propsOptions: Object) {
  const propsData = vm.$options.propsData || {}
  const props = vm._props = {}
  // cache prop keys so that future props updates can iterate using Array
  // instead of dynamic object key enumeration.
  const keys = vm.$options._propKeys = []
  const isRoot = !vm.$parent
  // root instance props should be converted
  if (!isRoot) {
    toggleObserving(false)
  }
  for (const key in propsOptions) {
    keys.push(key)
    const value = validateProp(key, propsOptions, propsData, vm)
    /* istanbul ignore else */
    if (process.env.NODE_ENV !== 'production') {
      const hyphenatedKey = hyphenate(key)
      if (isReservedAttribute(hyphenatedKey) ||
          config.isReservedAttr(hyphenatedKey)) {
        warn(
          `"${hyphenatedKey}" is a reserved attribute and cannot be used as component prop.`,
          vm
        )
      }
      defineReactive(props, key, value, () => {
        if (vm.$parent && !isUpdatingChildComponent) {
          warn(
            `Avoid mutating a prop directly since the value will be ` +
            `overwritten whenever the parent component re-renders. ` +
            `Instead, use a data or computed property based on the prop's ` +
            `value. Prop being mutated: "${key}"`,
            vm
          )
        }
      })
    } else {
      defineReactive(props, key, value)
    }
    // static props are already proxied on the component's prototype
    // during Vue.extend(). We only need to proxy props defined at
    // instantiation here.
    if (!(key in vm)) {
      proxy(vm, `_props`, key)
    }
  }
  toggleObserving(true)
}
```

可以看到，该函数接收两个参数：当前`Vue`实例和当前实例规范化后的`props`选项。

在函数内部首先定义了4个变量，分别是：

```javascript
const propsData = vm.$options.propsData || {}
const props = vm._props = {}
const keys = vm.$options._propKeys = []
const isRoot = !vm.$parent
```

- propsData:父组件传入的真实`props`数据。
- props:指向`vm._props`的指针，所有设置到`props`变量中的属性都会保存到`vm._props`中。
- keys:指向`vm.$options._propKeys`的指针，缓存`props`对象中的`key`，将来更新`props`时只需遍历`vm.$options._propKeys`数组即可得到所有`props`的`key`。
- isRoot:当前组件是否为根组件。

接着，判断当前组件是否为根组件，如果不是，那么不需要将`props`数组转换为响应式的，`toggleObserving(false)`用来控制是否将数据转换成响应式。如下：

```javascript
if (!isRoot) {
    toggleObserving(false)
}
```

接着，遍历`props`选项拿到每一对键值，先将键名添加到`keys`中，然后调用`validateProp`函数（关于该函数下面会介绍）校验父组件传入的`props`数据类型是否匹配并获取到传入的值`value`，然后将键和值通过`defineReactive`函数添加到`props`（即`vm._props`）中，如下：

```javascript
for (const key in propsOptions) {
    keys.push(key)
    const value = validateProp(key, propsOptions, propsData, vm)
    if (process.env.NODE_ENV !== 'production') {
      const hyphenatedKey = hyphenate(key)
      if (isReservedAttribute(hyphenatedKey) ||
          config.isReservedAttr(hyphenatedKey)) {
        warn(
          `"${hyphenatedKey}" is a reserved attribute and cannot be used as component prop.`,
          vm
        )
      }
      defineReactive(props, key, value, () => {
        if (vm.$parent && !isUpdatingChildComponent) {
          warn(
            `Avoid mutating a prop directly since the value will be ` +
            `overwritten whenever the parent component re-renders. ` +
            `Instead, use a data or computed property based on the prop's ` +
            `value. Prop being mutated: "${key}"`,
            vm
          )
        }
      })
    } else {
      defineReactive(props, key, value)
    }
  }
```

添加完之后再判断这个`key`在当前实例`vm`中是否存在，如果不存在，则调用`proxy`函数在`vm`上设置一个以`key`为属性的代码，当使用`vm[key]`访问数据时，其实访问的是`vm._props[key]`。如下：

```javascript
if (!(key in vm)) {
    proxy(vm, `_props`, key)
}
```

以上就是`initProps`函数的所有逻辑，接下来我们再看一下是如何通过`validateProp`函数校验父组件传入的`props`数据类型是否匹配并获取到传入的值的。

####  validateProp函数分析

`validateProp`函数的定义位于源码的`src/core/util/props.js`中，如下：

```javascript
export function validateProp (key,propOptions,propsData,vm) {
  const prop = propOptions[key]
  const absent = !hasOwn(propsData, key)
  let value = propsData[key]
  // boolean casting
  const booleanIndex = getTypeIndex(Boolean, prop.type)
  if (booleanIndex > -1) {
    if (absent && !hasOwn(prop, 'default')) {
      value = false
    } else if (value === '' || value === hyphenate(key)) {
      // only cast empty string / same name to boolean if
      // boolean has higher priority
      const stringIndex = getTypeIndex(String, prop.type)
      if (stringIndex < 0 || booleanIndex < stringIndex) {
        value = true
      }
    }
  }
  // check default value
  if (value === undefined) {
    value = getPropDefaultValue(vm, prop, key)
    // since the default value is a fresh copy,
    // make sure to observe it.
    const prevShouldObserve = shouldObserve
    toggleObserving(true)
    observe(value)
    toggleObserving(prevShouldObserve)
  }
  if (process.env.NODE_ENV !== 'production') {
    assertProp(prop, key, value, vm, absent)
  }
  return value
}
```

可以看到，该函数接收4个参数，分别是：

- key:遍历`propOptions`时拿到的每个属性名。
- propOptions:当前实例规范化后的`props`选项。
- propsData:父组件传入的真实`props`数据。
- vm:当前实例。

在函数内部首先定义了3个变量，分别是：

```javascript
const prop = propOptions[key]
const absent = !hasOwn(propsData, key)
let value = propsData[key]
```

- prop:当前`key`在`propOptions`中对应的值。
- absent:当前`key`是否在`propsData`中存在，即父组件是否传入了该属性。
- value:当前`key`在`propsData`中对应的值，即父组件对于该属性传入的真实值。

接着，判断`prop`的`type`属性是否是布尔类型（Boolean）,`getTypeIndex`函数用于判断`prop`的`type`属性中是否存在某种类型，如果存在，则返回该类型在`type`属性中的索引（因为`type`属性可以是数组），如果不存在则返回-1。

如果是布尔类型的话，那么有两种边界情况需要单独处理：

1. 如果`absent`为`true`，即父组件没有传入该`prop`属性并且该属性也没有默认值的时候，将该属性值设置为`false`，如下：

   ```javascript
   if (absent && !hasOwn(prop, 'default')) {
       value = false
   }
   ```

2. 如果父组件传入了该`prop`属性，那么需要满足以下几点：

   - 该属性值为空字符串或者属性值与属性名相等；
   - `prop`的`type`属性中不存在`String`类型；
   - 如果`prop`的`type`属性中存在`String`类型，那么`Boolean`类型在`type`属性中的索引必须小于`String`类型的索引，即`Boolean`类型的优先级更高;

   则将该属性值设置为`true`，如下：

   ```javascript
   if (value === '' || value === hyphenate(key)) {
       const stringIndex = getTypeIndex(String, prop.type)
       if (stringIndex < 0 || booleanIndex < stringIndex) {
           value = true
       }
   }
   ```

   另外，在判断属性值与属性名相等的时候，是先将属性名由驼峰式转换成用`-`连接的字符串，下面的这几种写法，子组件的`prop`都将被设置为`true`：

   ```html
   <Child name></Child>
   <Child name="name"></Child>
   <Child userName="user-name"></Child>
   ```

   如果不是布尔类型，是其它类型的话，那就只需判断父组件是否传入该属性即可，如果没有传入，则该属性值为`undefined`，此时调用`getPropDefaultValue`函数（关于该函数下面会介绍）获取该属性的默认值，并将其转换成响应式，如下：

   ```javascript
   if (value === undefined) {
       value = getPropDefaultValue(vm, prop, key)
       // since the default value is a fresh copy,
       // make sure to observe it.
       const prevShouldObserve = shouldObserve
       toggleObserving(true)
       observe(value)
       toggleObserving(prevShouldObserve)
   }
   ```

   如果父组件传入了该属性并且也有对应的真实值，那么在非生产环境下会调用`assertProp`函数（关于该函数下面会介绍）校验该属性值是否与要求的类型相匹配。如下：

   ```javascript
   if (process.env.NODE_ENV !== 'production' ) {
       assertProp(prop, key, value, vm, absent)
   }
   ```

   最后将父组件传入的该属性的真实值返回。

####  getPropDefaultValue函数分析

`getPropDefaultValue`函数的定义位于源码的`src/core/util/props.js`中，如下：

```javascript
function getPropDefaultValue (vm, prop, key){
  // no default, return undefined
  if (!hasOwn(prop, 'default')) {
    return undefined
  }
  const def = prop.default
  // warn against non-factory defaults for Object & Array
  if (process.env.NODE_ENV !== 'production' && isObject(def)) {
    warn(
      'Invalid default value for prop "' + key + '": ' +
      'Props with type Object/Array must use a factory function ' +
      'to return the default value.',
      vm
    )
  }
  // the raw prop value was also undefined from previous render,
  // return previous default value to avoid unnecessary watcher trigger
  if (vm && vm.$options.propsData &&
    vm.$options.propsData[key] === undefined &&
    vm._props[key] !== undefined
  ) {
    return vm._props[key]
  }
  // call factory function for non-Function types
  // a value is Function if its prototype is function even across different execution context
  return typeof def === 'function' && getType(prop.type) !== 'Function'
    ? def.call(vm)
    : def
}
```

该函数接收三个参数，分别是：

- vm:当前实例；
- prop:子组件`props`选项中的每个`key`对应的值；
- key:子组件`props`选项中的每个`key`；

其作用是根据子组件`props`选项中的`key`获取其对应的默认值。

首先判断`prop`中是否有`default`属性，如果没有，则表示没有默认值，直接返回。如下：

```javascript
if (!hasOwn(prop, 'default')) {
    return undefined
}
```

如果有则取出`default`属性，赋给变量`def`。接着判断在非生产环境下`def`是否是一个对象，如果是，则抛出警告：对象或数组默认值必须从一个工厂函数获取。如下：

```javascript
const def = prop.default
// warn against non-factory defaults for Object & Array
if (process.env.NODE_ENV !== 'production' && isObject(def)) {
    warn(
        'Invalid default value for prop "' + key + '": ' +
        'Props with type Object/Array must use a factory function ' +
        'to return the default value.',
        vm
    )
}
```

接着，再判断如果父组件没有传入该`props`属性，但是在`vm._props`中有该属性值，这说明`vm._props`中的该属性值就是默认值，如下：

```javascript
if (vm && vm.$options.propsData &&
    vm.$options.propsData[key] === undefined &&
    vm._props[key] !== undefined
   ) {
    return vm._props[key]
}
```

最后，判断`def`是否为函数并且`prop.type`不为`Function`，如果是的话表明`def`是一个返回对象或数组的工厂函数，那么将函数的返回值作为默认值返回；如果`def`不是函数，那么则将`def`作为默认值返回。如下：

```javascript
return typeof def === 'function' && getType(prop.type) !== 'Function'
    ? def.call(vm)
	: def
```

####  assertProp函数分析

`assertProp`函数的定义位于源码的`src/core/util/props.js`中，如下：

```javascript
function assertProp (prop,name,value,vm,absent) {
  if (prop.required && absent) {
    warn(
      'Missing required prop: "' + name + '"',
      vm
    )
    return
  }
  if (value == null && !prop.required) {
    return
  }
  let type = prop.type
  let valid = !type || type === true
  const expectedTypes = []
  if (type) {
    if (!Array.isArray(type)) {
      type = [type]
    }
    for (let i = 0; i < type.length && !valid; i++) {
      const assertedType = assertType(value, type[i])
      expectedTypes.push(assertedType.expectedType || '')
      valid = assertedType.valid
    }
  }
  if (!valid) {
    warn(
      `Invalid prop: type check failed for prop "${name}".` +
      ` Expected ${expectedTypes.map(capitalize).join(', ')}` +
      `, got ${toRawType(value)}.`,
      vm
    )
    return
  }
  const validator = prop.validator
  if (validator) {
    if (!validator(value)) {
      warn(
        'Invalid prop: custom validator check failed for prop "' + name + '".',
        vm
      )
    }
  }
}

```

该函数接收5个参数，分别是：

- prop:`prop`选项;
- name:`props`中`prop`选项的`key`;
- value:父组件传入的`propsData`中`key`对应的真实数据；
- vm:当前实例；
- absent:当前`key`是否在`propsData`中存在，即父组件是否传入了该属性。

其作用是校验父组件传来的真实值是否与`prop`的`type`类型相匹配，如果不匹配则在非生产环境下抛出警告。

函数内部首先判断`prop`中如果设置了必填项（即`prop.required`为`true`）并且父组件又没有传入该属性，此时则抛出警告：提示该项必填。如下：

```javascript
if (prop.required && absent) {
    warn(
        'Missing required prop: "' + name + '"',
        vm
    )
    return
}
```

接着判断如果该项不是必填的并且该项的值`value`不存在，那么此时是合法的，直接返回。如下：

```javascript
if (value == null && !prop.required) {
    return
}
```

接下来定义了3个变量，分别是：

```javascript
let type = prop.type
let valid = !type || type === true
const expectedTypes = []
```



- type:`prop`中的`type`类型；
- valid：校验是否成功；
- expectedTypes：保存期望类型的数组，当校验失败抛出警告时，会提示用户该属性所期望的类型是什么；

通常情况下，`type`可以是一个原生构造函数，也可以是一个包含多种类型的数组，还可以不设置该属性。如果用户设置的是原生构造函数或数组，那么此时`vaild`默认为`false`（`!type`），如果用户没有设置该属性，表示不需要校验，那么此时`vaild`默认为`true`，即校验成功。

另外，当`type`等于`true`时，即出现这样的写法：`props:{name:true}`，这说明`prop`一定会校验成功。所以当出现这种语法的时候，此时`type === true`，所以`vaild`默认为`true`。

接下来开始校验类型，如果用户设置了`type`属性，则判断该属性是不是数组，如果不是，则统一转化为数组，方便后续处理，如下：

```javascript
if (type) {
    if (!Array.isArray(type)) {
        type = [type]
    }
}
```

接下来遍历`type`数组，并调用`assertType`函数校验`value`。`assertType`函数校验后会返回一个对象，如下：

```javascript
{
    vaild:true,       // 表示是否校验成功
    expectedType：'Boolean'   // 表示被校验的类型
}
```

然后将被校验的类型添加到`expectedTypes`中，并将`vaild`变量设置为`assertedType.valid`，如下：

```javascript
for (let i = 0; i < type.length && !valid; i++) {
    const assertedType = assertType(value, type[i])
    expectedTypes.push(assertedType.expectedType || '')
    valid = assertedType.valid
}
```

这里请注意：上面循环中的条件语句有这样一个条件：`!vaild`，即`type`数组中还要有一个校验成功，循环立即结束，表示校验通过。

接下来，如果循环完毕后`vaild`为`false`，即表示校验未通过，则抛出警告。如下：

```javascript
if (!valid) {
    warn(
        `Invalid prop: type check failed for prop "${name}".` +
        ` Expected ${expectedTypes.map(capitalize).join(', ')}` +
        `, got ${toRawType(value)}.`,
        vm
    )
    return
}
```

另外，`prop`选项还支持自定义校验函数，如下：

```javascript
props:{
   // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
}
```

所以还需要使用用户传入的自定义校验函数来校验数据。首先获取到用户传入的校验函数，调用该函数并将待校验的数据传入，如果校验失败，则抛出警告。如下：

```javascript
const validator = prop.validator
if (validator) {
    if (!validator(value)) {
        warn(
            'Invalid prop: custom validator check failed for prop "' + name + '".',
            vm
        )
    }
}
```



### 初始化methods

初始化`methods`相较而言就比较简单了，它的初始化函数定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function initMethods (vm, methods) {
  const props = vm.$options.props
  for (const key in methods) {
    if (process.env.NODE_ENV !== 'production') {
      if (methods[key] == null) {
        warn(
          `Method "${key}" has an undefined value in the component definition. ` +
          `Did you reference the function correctly?`,
          vm
        )
      }
      if (props && hasOwn(props, key)) {
        warn(
          `Method "${key}" has already been defined as a prop.`,
          vm
        )
      }
      if ((key in vm) && isReserved(key)) {
        warn(
          `Method "${key}" conflicts with an existing Vue instance method. ` +
          `Avoid defining component methods that start with _ or $.`
        )
      }
    }
    vm[key] = methods[key] == null ? noop : bind(methods[key], vm)
  }
}
```

从代码中可以看到，初始化`methods`无非就干了三件事：判断`method`有没有？`method`的命名符不符合命名规范？如果`method`既有又符合规范那就把它挂载到`vm`实例上。下面我们就逐行分析源码，来过一遍这三件事。

首先，遍历`methods`选项中的每一个对象，在非生产环境下判断如果`methods`中某个方法只有`key`而没有`value`，即只有方法名没有方法体时，抛出异常：提示用户方法未定义。如下：

```javascript
if (methods[key] == null) {
    warn(
        `Method "${key}" has an undefined value in the component definition. ` +
        `Did you reference the function correctly?`,
        vm
    )
}
```

接着判断如果`methods`中某个方法名与`props`中某个属性名重复了，就抛出异常：提示用户方法名重复了。如下：

```javascript
if (props && hasOwn(props, key)) {
    warn(
        `Method "${key}" has already been defined as a prop.`,
        vm
    )
}
```

接着判断如果`methods`中某个方法名如果在实例`vm`中已经存在并且方法名是以`_`或`$`开头的，就抛出异常：提示用户方法名命名不规范。如下：

```javascript
if ((key in vm) && isReserved(key)) {
    warn(
        `Method "${key}" conflicts with an existing Vue instance method. ` +
        `Avoid defining component methods that start with _ or $.`
    )
}
```

其中，`isReserved`函数是用来判断字符串是否以`_`或`$`开头。

最后，如果上述判断都没问题，那就`method`绑定到实例`vm`上，这样，我们就可以通过`this.xxx`来访问`methods`选项中的`xxx`方法了，如下：

```javascript
vm[key] = methods[key] == null ? noop : bind(methods[key], vm)
```

### 初始化data

初始化`data`也比较简单，它的初始化函数定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function initData (vm) {
    let data = vm.$options.data
    data = vm._data = typeof data === 'function'
        ? getData(data, vm)
    : data || {}
    if (!isPlainObject(data)) {
        data = {}
        process.env.NODE_ENV !== 'production' && warn(
            'data functions should return an object:\n' +
            'https://vuejs.org/v2/guide/components.html##data-Must-Be-a-Function',
            vm
        )
    }
    // proxy data on instance
    const keys = Object.keys(data)
    const props = vm.$options.props
    const methods = vm.$options.methods
    let i = keys.length
    while (i--) {
        const key = keys[i]
        if (process.env.NODE_ENV !== 'production') {
            if (methods && hasOwn(methods, key)) {
                warn(
                    `Method "${key}" has already been defined as a data property.`,
                    vm
                )
            }
        }
        if (props && hasOwn(props, key)) {
            process.env.NODE_ENV !== 'production' && warn(
                `The data property "${key}" is already declared as a prop. ` +
                `Use prop default value instead.`,
                vm
            )
        } else if (!isReserved(key)) {
            proxy(vm, `_data`, key)
        }
    }
    // observe data
    observe(data, true /* asRootData */)
}
```

可以看到，`initData`函数的逻辑并不复杂，跟`initMethods`函数的逻辑有几分相似。就是通过一系列条件判断用户传入的`data`选项是否合法，最后将`data`转换成响应式并绑定到实例`vm`上。下面我们就来仔细看一下代码逻辑。

首先获取到用户传入的`data`选项，赋给变量`data`，同时将变量`data`作为指针指向`vm._data`，然后判断`data`是不是一个函数，如果是就调用`getData`函数获取其返回值，将其保存到`vm._data`中。如果不是，就将其本身保存到`vm._data`中。如下：

```javascript
let data = vm.$options.data
data = vm._data = typeof data === 'function'
    ? getData(data, vm)
	: data || {}
```

我们知道，无论传入的`data`选项是不是一个函数，它最终的值都应该是一个对象，如果不是对象的话，就抛出警告：提示用户`data`应该是一个对象。如下：

```javascript
if (!isPlainObject(data)) {
    data = {}
    process.env.NODE_ENV !== 'production' && warn(
        'data functions should return an object:\n' +
        'https://vuejs.org/v2/guide/components.html##data-Must-Be-a-Function',
        vm
    )
}
```

接下来遍历`data`对象中的每一项，在非生产环境下判断`data`对象中是否存在某一项的`key`与`methods`中某个属性名重复，如果存在重复，就抛出警告：提示用户属性名重复。如下：

```javascript
if (process.env.NODE_ENV !== 'production') {
    if (methods && hasOwn(methods, key)) {
        warn(
            `Method "${key}" has already been defined as a data property.`,
            vm
        )
    }
}
```

接着再判断是否存在某一项的`key`与`prop`中某个属性名重复，如果存在重复，就抛出警告：提示用户属性名重复。如下：

```javascript
if (props && hasOwn(props, key)) {
    process.env.NODE_ENV !== 'production' && warn(
        `The data property "${key}" is already declared as a prop. ` +
        `Use prop default value instead.`,
        vm
    )
}
```

如果都没有重复，则调用`proxy`函数将`data`对象中`key`不以`_`或`$`开头的属性代理到实例`vm`上，这样，我们就可以通过`this.xxx`来访问`data`选项中的`xxx`数据了。如下：

```javascript
if (!isReserved(key)) {
    proxy(vm, `_data`, key)
}
```

最后，调用`observe`函数将`data`中的数据转化成响应式，如下：

```javascript
observe(data, true /* asRootData */)
```



### 初始化computed

计算属性`computed`相信大家一定不会陌生，在日常开发中肯定会经常用到，而且我们知道计算属性有一个很大的特点就是： 计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。 那么接下来我们就来看一下计算属性是如何实现这些功能的的。

####  回顾用法

首先，根据官方文档的使用示例，我们来回顾一下计算属性的用法，如下：

```javascript
var vm = new Vue({
  data: { a: 1 },
  computed: {
    // 仅读取
    aDouble: function () {
      return this.a * 2
    },
    // 读取和设置
    aPlus: {
      get: function () {
        return this.a + 1
      },
      set: function (v) {
        this.a = v - 1
      }
    }
  }
})
vm.aPlus   // => 2
vm.aPlus = 3
vm.a       // => 2
vm.aDouble // => 4
```

可以看到，`computed`选项中的属性值可以是一个函数，那么该函数默认为取值器`getter`，用于仅读取数据；还可以是一个对象，对象里面有取值器`getter`和存值器`setter`，用于读取和设置数据。

####  initComputed函数分析

了解了计算属性的用法之后，下面我们就来分析一下计算属性的初始化函数`initComputed`的内部原理是怎样的。`initComputed`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function initComputed (vm: Component, computed: Object) {
    const watchers = vm._computedWatchers = Object.create(null)
    const isSSR = isServerRendering()

    for (const key in computed) {
        const userDef = computed[key]
        const getter = typeof userDef === 'function' ? userDef : userDef.get
        if (process.env.NODE_ENV !== 'production' && getter == null) {
            warn(
                `Getter is missing for computed property "${key}".`,
                vm
            )
        }

        if (!isSSR) {
            // create internal watcher for the computed property.
            watchers[key] = new Watcher(
                vm,
                getter || noop,
                noop,
                computedWatcherOptions
            )
        }

        if (!(key in vm)) {
            defineComputed(vm, key, userDef)
        } else if (process.env.NODE_ENV !== 'production') {
            if (key in vm.$data) {
                warn(`The computed property "${key}" is already defined in data.`, vm)
            } else if (vm.$options.props && key in vm.$options.props) {
                warn(`The computed property "${key}" is already defined as a prop.`, vm)
            }
        }
    }
}
```

可以看到，在函数内部，首先定义了一个变量`watchers`并将其赋值为空对象，同时将其作为指针指向`vm._computedWatchers`，如下：

```javascript
const watchers = vm._computedWatchers = Object.create(null)
```

接着，遍历`computed`选项中的每一项属性，首先获取到每一项的属性值，记作`userDef`，然后判断`userDef`是不是一个函数，如果是函数，则该函数默认为取值器`getter`，将其赋值给变量`getter`；如果不是函数，则说明是一个对象，则取对象中的`get`属性作为取值器赋给变量`getter`。如下：

```javascript
const userDef = computed[key]
const getter = typeof userDef === 'function' ? userDef : userDef.get
```

接着判断在非生产环境下如果上面两种情况取到的取值器不存在，则抛出警告：提示用户计算属性必须有取值器。如下：

```javascript
if (process.env.NODE_ENV !== 'production' && getter == null) {
    warn(
        `Getter is missing for computed property "${key}".`,
        vm
    )
}
```

接着判断如果不是在服务端渲染环境下，则创建一个`watcher`实例，并将当前循环到的的属性名作为键，创建的`watcher`实例作为值存入`watchers`对象中。如下：

```javascript
if (!isSSR) {
    // create internal watcher for the computed property.
    watchers[key] = new Watcher(
        vm,
        getter || noop,
        noop,
        computedWatcherOptions
    )
}
```

最后，判断当前循环到的的属性名是否存在于当前实例`vm`上，如果存在，则在非生产环境下抛出警告；如果不存在，则调用`defineComputed`函数为实例`vm`上设置计算属性。

以上就是`initComputed`函数的内部逻辑，接下里我们再来看一下`defineComputed`函数是如何为实例`vm`上设置计算属性的。

####  defineComputed函数分析



`defineComputed`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
const sharedPropertyDefinition = {
  enumerable: true,
  configurable: true,
  get: noop,
  set: noop
}

export function defineComputed (target,key,userDef) {
  const shouldCache = !isServerRendering()
  if (typeof userDef === 'function') {
    sharedPropertyDefinition.get = shouldCache
      ? createComputedGetter(key)
      : userDef
    sharedPropertyDefinition.set = noop
  } else {
    sharedPropertyDefinition.get = userDef.get
      ? shouldCache && userDef.cache !== false
        ? createComputedGetter(key)
        : userDef.get
      : noop
    sharedPropertyDefinition.set = userDef.set
      ? userDef.set
      : noop
  }
  if (process.env.NODE_ENV !== 'production' &&
      sharedPropertyDefinition.set === noop) {
    sharedPropertyDefinition.set = function () {
      warn(
        `Computed property "${key}" was assigned to but it has no setter.`,
        this
      )
    }
  }
  Object.defineProperty(target, key, sharedPropertyDefinition)
}


```

该函数接受3个参数，分别是：`target`、`key`和`userDef`。其作用是为`target`上定义一个属性`key`，并且属性`key`的`getter`和`setter`根据`userDef`的值来设置。下面我们就来看一下该函数的具体逻辑。

首先定义了变量`sharedPropertyDefinition`，它是一个默认的属性描述符。

接着，在函数内部定义了变量`shouldCache`，用于标识计算属性是否应该有缓存。该变量的值是当前环境是否为非服务端渲染环境，如果是非服务端渲染环境则该变量为`true`。也就是说，只有在非服务端渲染环境下计算属性才应该有缓存。如下：

```javascript
const shouldCache = !isServerRendering()
```

接着，判断如果`userDef`是一个函数，则该函数默认为取值器`getter`，此处在非服务端渲染环境下并没有直接使用`userDef`作为`getter`，而是调用`createComputedGetter`函数（关于该函数下面会介绍）创建了一个`getter`，这是因为`userDef`只是一个普通的`getter`，它并没有缓存功能，所以我们需要额外创建一个具有缓存功能的`getter`，而在服务端渲染环境下可以直接使用`userDef`作为`getter`，因为在服务端渲染环境下计算属性不需要缓存。由于用户没有设置`setter`函数，所以将`sharedPropertyDefinition.set`设置为`noop`。如下：

```javascript
if (typeof userDef === 'function') {
    sharedPropertyDefinition.get = shouldCache
        ? createComputedGetter(key)
    : userDef
    sharedPropertyDefinition.set = noop
}
```

如果`userDef`不是一个函数，那么就将它当作对象处理。在设置`sharedPropertyDefinition.get`的时候先判断`userDef.get`是否存在，如果不存在，则将其设置为`noop`，如果存在，则同上面一样，在非服务端渲染环境下并且用户没有明确的将`userDef.cache`设置为`false`时调用`createComputedGetter`函数创建一个`getter`赋给`sharedPropertyDefinition.get`。然后设置`sharedPropertyDefinition.set`为`userDef.set`函数。如下：

```javascript
sharedPropertyDefinition.get = userDef.get
      ? shouldCache && userDef.cache !== false
        ? createComputedGetter(key)
        : userDef.get
      : noop
sharedPropertyDefinition.set = userDef.set
    ? userDef.set
	: noop
```

接着，再判断在非生产环境下如果用户没有设置`setter`的话，那么就给`setter`一个默认函数，这是为了防止用户在没有设置`setter`的情况下修改计算属性，从而为其抛出警告，如下：

```javascript
if (process.env.NODE_ENV !== 'production' &&
    sharedPropertyDefinition.set === noop) {
    sharedPropertyDefinition.set = function () {
        warn(
            `Computed property "${key}" was assigned to but it has no setter.`,
            this
        )
    }
}
```

最后调用`Object.defineProperty`方法将属性`key`绑定到`target`上，其中的属性描述符就是上面设置的`sharedPropertyDefinition`。如此以来，就将计算属性绑定到实例`vm`上了。

以上就是`defineComputed`函数的所有逻辑。另外，我们发现，计算属性有没有缓存及其响应式貌似主要在于是否将`getter`设置为`createComputedGetter`函数的返回结果。那么接下来，我们就对这个`createComputedGetter`函数一探究竟。

####  createComputedGetter函数分析

`createComputedGetter`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function createComputedGetter (key) {
    return function computedGetter () {
        const watcher = this._computedWatchers && this._computedWatchers[key]
        if (watcher) {
            watcher.depend()
            return watcher.evaluate()
        }
    }
}
```

可以看到，该函数是一个高阶函数，其内部返回了一个`computedGetter`函数，所以其实是将`computedGetter`函数赋给了`sharedPropertyDefinition.get`。当获取计算属性的值时会执行属性的`getter`，而属性的`getter`就是 `sharedPropertyDefinition.get`，也就是说最终执行的 `computedGetter`函数。

在`computedGetter`函数内部，首先存储在当前实例上`_computedWatchers`属性中`key`所对应的`watcher`实例，如果`watcher`存在，则调用`watcher`实例上的`depend`方法和`evaluate`方法，并且将`evaluate`方法的返回值作为计算属性的计算结果返回。那么`watcher`实例上的`depend`方法和`evaluate`方法又是什么呢？

####  depend和evaluate

回顾上文中创建`watcher`实例的时候：

```javascript
const computedWatcherOptions = { computed: true }
watchers[key] = new Watcher(
    vm,
    getter || noop,
    noop,
    computedWatcherOptions
)
```

传入的参数中第二个参数是`getter`函数，第四个参数是一个对象`computedWatcherOptions`。

我们再回顾`Watcher`类的定义，如下：

```javascript
export default class Watcher {
    constructor (vm,expOrFn,cb,options,isRenderWatcher) {
        if (options) {
            // ...
            this.computed = !!options.computed
            // ...
        } else {
            // ...
        }

        this.dirty = this.computed // for computed watchers
        if (typeof expOrFn === 'function') {
            this.getter = expOrFn
        }

        if (this.computed) {
            this.value = undefined
            this.dep = new Dep()
        }
    }

    evaluate () {
        if (this.dirty) {
            this.value = this.get()
            this.dirty = false
        }
        return this.value
    }

    /**
     * Depend on this watcher. Only for computed property watchers.
     */
    depend () {
        if (this.dep && Dep.target) {
            this.dep.depend()
        }
    }

    update () {
        if (this.computed) {
            if (this.dep.subs.length === 0) {
                this.dirty = true
            } else {
                this.getAndInvoke(() => {
                    this.dep.notify()
                })
            }
        }
    }

    getAndInvoke (cb: Function) {
        const value = this.get()
        if (
            value !== this.value ||
            // Deep watchers and watchers on Object/Arrays should fire even
            // when the value is the same, because the value may
            // have mutated.
            isObject(value) ||
            this.deep
        ) {
            // set new value
            const oldValue = this.value
            this.value = value
            this.dirty = false
            if (this.user) {
                try {
                    cb.call(this.vm, value, oldValue)
                } catch (e) {
                    handleError(e, this.vm, `callback for watcher "${this.expression}"`)
                }
            } else {
                cb.call(this.vm, value, oldValue)
            }
        }
    }
}
```

可以看到，在实例化`Watcher`类的时候，第四个参数传入了一个对象`computedWatcherOptions = { computed: true }`，该对象中的`computed`属性标志着这个`watcher`实例是计算属性的`watcher`实例，即`Watcher`类中的`this.computed`属性，同时类中还定义了`this.dirty`属性用于标志计算属性的返回值是否有变化，计算属性的缓存就是通过这个属性来判断的，每当计算属性依赖的数据发生变化时，会将`this.dirty`属性设置为`true`，这样下一次读取计算属性时，会重新计算结果返回，否则直接返回之前的计算结果。

当调用`watcher.depend()`方法时，会将读取计算属性的那个`watcher`添加到计算属性的`watcher`实例的依赖列表中，当计算属性中用到的数据发生变化时，计算属性的`watcher`实例就会执行`watcher.update()`方法，在`update`方法中会判断当前的`watcher`是不是计算属性的`watcher`，如果是则调用`getAndInvoke`去对比计算属性的返回值是否发生了变化，如果真的发生变化，则执行回调，通知那些读取计算属性的`watcher`重新执行渲染逻辑。

当调用`watcher.evaluate()`方法时，会先判断`this.dirty`是否为`true`，如果为`true`，则表明计算属性所依赖的数据发生了变化，则调用`this.get()`重新获取计算结果最后返回；如果为`false`，则直接返回之前的计算结果。

其内部原理如图所示：

![](~@/learn-vue-source-code/lifecycle/2.png)


### 初始化watch

接下来就是最后一个初始化函数了——初始化`watch`选项。在日常开发中`watch`选项也经常会使用到，它可以用来侦听某个已有的数据，当该数据发生变化时执行对应的回调函数。那么，接下来我们就来看一些`watch`选项是如何被初始化的。

####  回顾用法

首先，根据官方文档的使用示例，我们来回顾一下`watch`选项的用法，如下：

```javascript
var vm = new Vue({
  data: {
    a: 1,
    b: 2,
    c: 3,
    d: 4,
    e: {
      f: {
        g: 5
      }
    }
  },
  watch: {
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    // methods选项中的方法名
    b: 'someMethod',
    // 深度侦听，该回调会在任何被侦听的对象的 property 改变时被调用，不论其被嵌套多深
    c: {
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    },
    // 该回调将会在侦听开始之后被立即调用
    d: {
      handler: 'someMethod',
      immediate: true
    },
    // 调用多个回调
    e: [
      'handle1',
      function handle2 (val, oldVal) { /* ... */ },
      {
        handler: function handle3 (val, oldVal) { /* ... */ },
      }
    ],
    // 侦听表达式
    'e.f': function (val, oldVal) { /* ... */ }
  }
})
vm.a = 2 // => new: 2, old: 1
```

可以看到，`watch`选项的用法非常灵活。首先`watch`选项是一个对象，键是需要观察的表达式，值是对应回调函数。值也可以是方法名，或者包含选项的对象。既然给用户提供的用法灵活，那么在代码中就需要按条件来判断，根据不同的用法做相应的处理。

####  initWatch函数分析

了解了`watch`选项的用法之后，下面我们就来分析一下`watch`选项的初始化函数`initWatch`的内部原理是怎样的。`initWatch`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function initWatch (vm, watch) {
  for (const key in watch) {
    const handler = watch[key]
    if (Array.isArray(handler)) {
      for (let i = 0; i < handler.length; i++) {
        createWatcher(vm, key, handler[i])
      }
    } else {
      createWatcher(vm, key, handler)
    }
  }
}
```



可以看到，在函数内部会遍历`watch`选项，拿到每一项的`key`和对应的值`handler`。然后判断`handler`是否为数组，如果是数组则循环该数组并将数组中的每一项依次调用`createWatcher`函数来创建`watcher`；如果不是数组，则直接调用`createWatcher`函数来创建`watcher`。那么这个`createWatcher`函数是如何创建`watcher`的呢？

####  createWatcher函数分析

`createWatcher`函数的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
function createWatcher (
  vm: Component,
  expOrFn: string | Function,
  handler: any,
  options?: Object
) {
  if (isPlainObject(handler)) {
    options = handler
    handler = handler.handler
  }
  if (typeof handler === 'string') {
    handler = vm[handler]
  }
  return vm.$watch(expOrFn, handler, options)
}
```

可以看到，该函数接收4个参数，分别是：

- vm:当前实例；
- expOrFn:被侦听的属性表达式
- handler:`watch`选项中每一项的值
- options:用于传递给`vm.$watch`的选项对象

在该函数内部，首先会判断传入的`handler`是否为一个对象，如果是一个对象，那么就认为用户使用的是这种写法：

```javascript
watch: {
    c: {
        handler: function (val, oldVal) { /* ... */ },
		deep: true
    }
}
```

即带有侦听选项的写法，此时就将`handler`对象整体记作`options`，把`handler`对象中的`handler`属性作为真正的回调函数记作`handler`，如下：

```javascript
if (isPlainObject(handler)) {
    options = handler
    handler = handler.handler
}
```

接着判断传入的`handler`是否为一个字符串，如果是一个字符串，那么就认为用户使用的是这种写法：

```javascript
watch: {
    // methods选项中的方法名
    b: 'someMethod',
}
```

即回调函数是`methods`选项中的一个方法名，我们知道，在初始化`methods`选项的时候会将选项中的每一个方法都绑定到当前实例上，所以此时我们只需从当前实例上取出该方法作为真正的回调函数记作`handler`，如下：

```javascript
if (typeof handler === 'string') {
    handler = vm[handler]
}
```

如果既不是对象又不是字符串，那么我们就认为它是一个函数，就不做任何处理。

针对不同类型的值处理完毕后，`expOrFn`是被侦听的属性表达式，`handler`变量是回调函数，`options`变量为侦听选项，最后，调用`vm.$watcher`方法（关于该方法在介绍全局实例方法的时候会详细介绍）并传入以上三个参数完成初始化`watch`。

### 总结

本篇文章介绍了生命周期初始化阶段所调用的第五个初始化函数——`initState`。该初始化函数内部总共初始化了5个选项，分别是：`props`、`methods`、`data`、`computed`和`watch`。

这5个选项的初始化顺序不是任意的，而是经过精心安排的。只有按照这种顺序初始化我们才能在开发中在`data`中可以使用`props`，在`watch`中可以观察`data`和`props`。

这5个选项中的所有属性最终都会被绑定到实例上，这也就是我们为什么可以使用`this.xxx`来访问任意属性。同时正是因为这一点，这5个选项中的所有属性名都不应该有所重复，这样会造成属性之间相互覆盖。

最后，我们对这5个选项分别都是如何进行初始化的内部原理进行了逐一分析。

## 模板编译阶段


### 前言

前几篇文章中我们介绍了生命周期的初始化阶段，我们知道，在初始化阶段各项工作做完之后调用了`vm.$mount`方法，该方法的调用标志着初始化阶段的结束和进入下一个阶段，从官方文档给出的生命周期流程图中可以看到，下一个阶段就进入了模板编译阶段，该阶段所做的主要工作是获取到用户传入的模板内容并将其编译成渲染函数。

![](~@/learn-vue-source-code/lifecycle/3.png)


模板编译阶段并不是存在于`Vue`的所有构建版本中，它只存在于完整版（即`vue.js`）中。在只包含运行时版本（即`vue.runtime.js`）中并不存在该阶段，这是因为当使用`vue-loader`或`vueify`时，`*.vue`文件内部的模板会在构建时预编译成渲染函数，所以是不需要编译的，从而不存在模板编译阶段，由上一步的初始化阶段直接进入下一阶段的挂载阶段。

在这里，我们有必要介绍一下什么是完整版和只包含运行时版。

 `vue`基于源码构建的有两个版本，一个是`runtime only`(一个只包含运行时的版本)，另一个是`runtime + compiler`(一个同时包含编译器和运行时的完整版本)。而两个版本的区别仅在于后者包含了一个编译器。

- 完整版本

  一个完整的`Vue`版本是包含编译器的，我们可以使用`template`选项进行模板编写。编译器会自动将`template`选项中的模板字符串编译成渲染函数的代码,源码中就是`render`函数。如果你需要在客户端编译模板 (比如传入一个字符串给 `template` 选项，或挂载到一个元素上并以其 `DOM` 内部的 HTML 作为模板)，就需要一个包含编译器的版本。 如下：

  ```javascript
  // 需要编译器的版本
  new Vue({
    template: '<div>{{ hi }}</div>'
  })
  ```

- 只包含运行时版本

  只包含运行时的版本拥有创建`Vue`实例、渲染并处理`Virtual DOM`等功能，基本上就是除去编译器外的完整代码。该版本的适用场景有两种：

  1.我们在选项中通过手写`render`函数去定义渲染过程，这个时候并不需要包含编译器的版本便可完整执行。

  ```javascript
  // 不需要编译器
  new Vue({
    render (h) {
      return h('div', this.hi)
    }
  })
  ```

   2.借助`vue-loader`这样的编译工具进行编译，当我们利用`webpack`进行`Vue`的工程化开发时，常常会利用`vue-loader`对`*.vue`文件进行编译，尽管我们也是利用`template`模板标签去书写代码，但是此时的`Vue`已经不需要利用编译器去负责模板的编译工作了，这个过程交给了插件去实现。

很明显，编译过程对性能会造成一定的损耗，并且由于加入了编译的流程代码，`Vue`代码的总体积也更加庞大(运行时版本相比完整版体积要小大约 30%)。因此在实际开发中，我们需要借助像`webpack`的`vue-loader`这类工具进行编译，将`Vue`对模板的编译阶段合并到`webpack`的构建流程中，这样不仅减少了生产环境代码的体积，也大大提高了运行时的性能，一举两得。

为了完整的学习源码，本篇文章将会分析完整版中的模板编译阶段到底做了些什么。

### 模板编译阶段分析

上文中说了，完整版和只包含运行时版之间的差异主要在于是否有模板编译阶段，而是否有模板编译阶段主要表现在`vm.$mount`方法的实现上。此时你可能会有疑问：照这么说，`$mount`方法也有两个版本？对的，你可以这么理解，但归根结底来说还是一种。我们分别来看一下。

####  两种$mount方法对比

只包含运行时版本的`$mount`代码如下：

```javascript
Vue.prototype.$mount = function (el,hydrating) {
  el = el && inBrowser ? query(el) : undefined;
  return mountComponent(this, el, hydrating)
};
```

在该版本中的`$mount`方法内部获取到`el`选项对应的`DOM`元素后直接调用`mountComponent`函数进行挂载操作，关于该函数我们会在挂载阶段详细介绍。

而完整版本的`$mount`代码如下：

```javascript
var mount = Vue.prototype.$mount;
Vue.prototype.$mount = function (el,hydrating) {
  // 省略获取模板及编译代码

  return mount.call(this, el, hydrating)
}
```

注意，在完整版本的`$mount`定义之前，先将`Vue`原型上的`$mount`方法先缓存起来，记作变量`mount`。此时你可能会问了，这`$mount`方法还没定义呢，怎么先缓存起来了。

其实在源码中，是先定义只包含运行时版本的`$mount`方法，再定义完整版本的`$mount`方法，所以此时缓存的`mount`变量就是只包含运行时版本的`$mount`方法。

为什么要这么做呢？上文我们说了，完整版本和只包含运行时版本之间的差异主要在于是否有模板编译阶段，只包含运行时版本没有模板编译阶段，初始化阶段完成后直接进入挂载阶段，而完整版本是初始化阶段完成后进入模板编译阶段，然后再进入挂载阶段。也就是说，这两个版本最终都会进入挂载阶段。所以在完整版本的`$mount`方法中将模板编译完成后需要回头去调只包含运行时版本的`$mount`方法以进入挂载阶段。

这也就是在完整版本的`$mount`方法中先把只包含运行时版本的`$mount`方法缓存下来，记作变量`mount`，然后等模板编译完成，再执行`mount`方法（即只包含运行时版本的`$mount`方法）。

所以分析模板编译阶段其实就是分析完整版的`vm.$mount`方法的实现。

####  完整版的vm.$mount方法分析

完整版的`vm.$mount`方法定义位于源码的`src/platforms/web/entry-runtime-with-compiler.js`中，如下：

```javascript
var mount = Vue.prototype.$mount;
Vue.prototype.$mount = function (el,hydrating) {
  el = el && query(el);
  if (el === document.body || el === document.documentElement) {
    warn(
      "Do not mount Vue to <html> or <body> - mount to normal elements instead."
    );
    return this
  }

  var options = this.$options;
  // resolve template/el and convert to render function
  if (!options.render) {
    var template = options.template;
    if (template) {
      if (typeof template === 'string') {
          if (template.charAt(0) === '#') {
            template = idToTemplate(template);
            /* istanbul ignore if */
            if (!template) {
              warn(
                ("Template element not found or is empty: " + (options.template)),
                this
              );
            }
          }
      } else if (template.nodeType) {
        template = template.innerHTML;
      } else {
        {
          warn('invalid template option:' + template, this);
        }
        return this
      }
    } else if (el) {
      template = getOuterHTML(el);
    }
    if (template) {
      if (config.performance && mark) {
        mark('compile');
      }

      var ref = compileToFunctions(template, {
        outputSourceRange: "development" !== 'production',
        shouldDecodeNewlines: shouldDecodeNewlines,
        shouldDecodeNewlinesForHref: shouldDecodeNewlinesForHref,
        delimiters: options.delimiters,
        comments: options.comments
      }, this);
      var render = ref.render;
      var staticRenderFns = ref.staticRenderFns;
      options.render = render;
      options.staticRenderFns = staticRenderFns;

      if (config.performance && mark) {
        mark('compile end');
        measure(("vue " + (this._name) + " compile"), 'compile', 'compile end');
      }
    }
  }
  return mount.call(this, el, hydrating)
};
```

从代码中可以看到，该函数可大致分为三部分：

- 根据传入的`el`参数获取`DOM`元素；
- 在用户没有手写`render`函数的情况下获取传入的模板`template`；
- 将获取到的`template`编译成`render`函数；

接下来我们就逐一分析。

首先，根据传入的`el`参数获取`DOM`元素。如下：

```javascript
el = el && query(el);

function query (el) {
  if (typeof el === 'string') {
    var selected = document.querySelector(el);
    if (!selected) {
      warn(
        'Cannot find element: ' + el
      );
      return document.createElement('div')
    }
    return selected
  } else {
    return el
  }
}
```

由于`el`参数可以是元素，也可以是字符串类型的元素选择器，所以调用`query`函数来获取到`el`对应的`DOM`元素。由于`query`函数比较简单，就是根据传入的`el`参数是否为字符串从而以不同方式获取到对应的`DOM`元素，这里就不逐行展开介绍了。

另外，这里还多了一个判断，就是判断获取到`el`对应的`DOM`元素如果是`body`或`html`元素时，将会抛出警告。这是因为`Vue`会将模板中的内容替换`el`对应的`DOM`元素，如果是`body`或`html`元素时，替换之后将会破坏整个`DOM`文档，所以不允许`el`是`body`或`html`。如下：

```javascript
if (el === document.body || el === document.documentElement) {
  warn(
    "Do not mount Vue to <html> or <body> - mount to normal elements instead."
  );
  return this
}
```



接着，在用户没有手写`render`函数的情况下获取传入的模板`template`；如下：

```javascript
if (!options.render) {
  var template = options.template;
  if (template) {
    if (typeof template === 'string') {
      if (template.charAt(0) === '#') {
        template = idToTemplate(template);
        /* istanbul ignore if */
        if (!template) {
          warn(
            ("Template element not found or is empty: " + (options.template)),
            this
          );
        }
      }
    } else if (template.nodeType) {
        template = template.innerHTML;
    } else {
      {
        warn('invalid template option:' + template, this);
      }
      return this
    }
  } else if (el) {
    template = getOuterHTML(el);
  }
}
```

首先获取用户传入的`template`选项赋给变量`template`，如果变量`template`存在，则接着判断如果`template`是字符串并且以`##`开头，则认为`template`是`id`选择符，则调用`idToTemplate`函数获取到选择符对应的`DOM`元素的`innerHTML`作为模板，如下：

```javascript
if (template) {
  if (typeof template === 'string') {
    if (template.charAt(0) === '#') {
      template = idToTemplate(template);
    }
  }
}

var idToTemplate = cached(function (id) {
  var el = query(id);
  return el && el.innerHTML
});
```

如果`template`不是字符串，那就判断它是不是一个`DOM`元素，如果是，则使用该`DOM`元素的`innerHTML`作为模板，如下：

```javascript
if (template.nodeType) {
  template = template.innerHTML;
}
```

如果既不是字符串，也不是`DOM`元素，此时会抛出警告：提示用户`template`选项无效。如下：

```javascript
else {
  {
    warn('invalid template option:' + template, this);
  }
  return this
}
```

如果变量`template`不存在，表明用户没有传入`template`选项，则根据传入的`el`参数调用`getOuterHTML`函数获取外部模板，如下：

```javascript
if (el) {
  template = getOuterHTML(el);
}

function getOuterHTML (el) {
  if (el.outerHTML) {
    return el.outerHTML
  } else {
    var container = document.createElement('div');
    container.appendChild(el.cloneNode(true));
    return container.innerHTML
  }
}
```

不管是从内部的`template`选项中获取模板，还是从外部获取模板，总之就是要获取到用户传入的模板内容，有了模板内容接下来才能将模板编译成渲染函数。

获取到模板之后，接下来要做的事就是将其编译成渲染函数，如下：

```javascript
if (template) {
  var ref = compileToFunctions(template, {
    outputSourceRange: "development" !== 'production',
    shouldDecodeNewlines: shouldDecodeNewlines,
    shouldDecodeNewlinesForHref: shouldDecodeNewlinesForHref,
    delimiters: options.delimiters,
    comments: options.comments
  }, this);
  var render = ref.render;
  var staticRenderFns = ref.staticRenderFns;
  options.render = render;
  options.staticRenderFns = staticRenderFns;
}
```

关于将模板编译成渲染函数的具体步骤在前面文章模板编译篇中已经做了详细介绍，在这里，我们仅做简单回顾。

把模板编译成渲染函数是在`compileToFunctions`函数中进行的，该函数接收待编译的模板字符串和编译选项作为参数，返回一个对象，对象里面的`render`属性即是编译好的渲染函数，最后将渲染函数设置到`$options`上。

### 总结

本篇文章介绍了生命周期中的第二个阶段——模板编译阶段。

首先介绍了`Vue`源码构建的两种版本：完整版本和只包含运行时版本。并且我们知道了模板编译阶段只存在于完整版中，在只包含运行时版本中不存在该阶段，这是因为在只包含运行时版本中，当使用`vue-loader`或`vueify`时，`*.vue`文件内部的模板会在构建时预编译成渲染函数，所以是不需要编译的，从而不存在模板编译阶段。

然后对比了两种版本`$mount`方法的区别。它们的区别在于在`$mount`方法中是否进行了模板编译。在只包含运行时版本的`$mount`方法中获取到`DOM`元素后直接进入挂载阶段，而在完整版本的`$mount`方法中是先将模板进行编译，然后回过头调只包含运行时版本的`$mount`方法进入挂载阶段。

最后，我们知道了分析模板编译阶段其实就是分析完整版的`vm.$mount`方法的实现，我们将完整版的`vm.$mount`方法源码进行了逐行分析。知道了在该阶段中所做的工作就是：从用户传入的`el`选项和`template`选项中获取到用户传入的内部或外部模板，然后将获取到的模板编译成渲染函数。

## 挂载阶段


### 前言

模板编译阶段完成之后，接下来就进入了挂载阶段，从官方文档给出的生命周期流程图中可以看到，挂载阶段所做的主要工作是创建`Vue`实例并用其替换`el`选项对应的`DOM`元素，同时还要开启对模板中数据（状态）的监控，当数据（状态）发生变化时通知其依赖进行视图更新。

![](~@/learn-vue-source-code/lifecycle/4.png)


### 挂载阶段分析

在上篇文章介绍模板编译阶段中我们说过，在完整版本的`$mount`方法中将模板编译完成之后，会回过头去调只包含运行时版本的`$mount`方法进入挂载阶段，所以要想分析挂载阶段我们必须从只包含运行时版本的`$mount`方法入手。

只包含运行时版本的`$mount`代码如下：

```javascript
Vue.prototype.$mount = function (el,hydrating) {
  el = el && inBrowser ? query(el) : undefined;
  return mountComponent(this, el, hydrating)
};
```

可以看到，在该函数内部首先获取到`el`选项对应的`DOM`元素，然后调用`mountComponent`函数并将`el`选项对应的`DOM`元素传入，进入挂载阶段。那么，下面我们来看下`mountComponent`函数内部都干了些什么。

`mountComponent`函数的定义位于源码的`src/core/instance/lifecycle.js`中，如下：

```javascript
export function mountComponent (vm,el,hydrating) {
    vm.$el = el
    if (!vm.$options.render) {
        vm.$options.render = createEmptyVNode
    }
    callHook(vm, 'beforeMount')

    let updateComponent

    updateComponent = () => {
        vm._update(vm._render(), hydrating)
    }
    new Watcher(vm, updateComponent, noop, {
        before () {
            if (vm._isMounted) {
                callHook(vm, 'beforeUpdate')
            }
        }
    }, true /* isRenderWatcher */)
    hydrating = false

    if (vm.$vnode == null) {
        vm._isMounted = true
        callHook(vm, 'mounted')
    }
    return vm
}
```

可以看到，在该函数中，首先会判断实例上是否存在渲染函数，如果不存在，则设置一个默认的渲染函数`createEmptyVNode`，该渲染函数会创建一个注释类型的`VNode`节点。如下：

```javascript
vm.$el = el
if (!vm.$options.render) {
    vm.$options.render = createEmptyVNode
}
```



然后调用`callHook`函数来触发`beforeMount`生命周期钩子函数，如下：

```javascript
callHook(vm, 'beforeMount')
```



该钩子函数触发后标志着正式开始执行挂载操作。

接下来定义了一个`updateComponent`函数，如下：

```javascript
updateComponent = () => {
    vm._update(vm._render(), hydrating)
}
```

在该函数内部，首先执行渲染函数`vm._render()`得到一份最新的`VNode`节点树，然后执行` vm._update()`方法对最新的`VNode`节点树与上一次渲染的旧`VNode`节点树进行对比并更新`DOM`节点(即`patch`操作)，完成一次渲染。

也就是说，如果调用了`updateComponent`函数，就会将最新的模板内容渲染到视图页面中，这样就完成了挂载操作的一半工作，即图中的上半部分：

![](~@/learn-vue-source-code/lifecycle/5.png)




为什么说是完成了一半操作呢？这是因为在挂载阶段不但要将模板渲染到视图中，同时还要开启对模板中数据（状态）的监控，当数据（状态）发生变化时通知其依赖进行视图更新。即图中的下半部分：

![](~@/learn-vue-source-code/lifecycle/6.png)


继续往下看，接下来创建了一个`Watcher`实例，并将定义好的`updateComponent`函数传入。要想开启对模板中数据（状态）的监控，这一段代码是关键，如下：

```javascript
new Watcher(
    vm,                    // 第一个参数
    updateComponent,       // 第二个参数
    noop,                  // 第三个参数
    {                      // 第四个参数
        before () {
          if (vm._isMounted) {
            callHook(vm, 'beforeUpdate')
          }
        }
	},
    true                    // 第五个参数
)
```

可以看到，在创建`Watcher`实例的时候，传入的第二个参数是`updateComponent`函数。回顾一下我们在数据侦测篇文章中介绍`Watcher`类的时候，`Watcher`类构造函数的第二个参数支持两种类型：函数和数据路径（如`a.b.c`）。如果是数据路径，会根据路径去读取这个数据；如果是函数，会执行这个函数。一旦读取了数据或者执行了函数，就会触发数据或者函数内数据的`getter`方法，而在`getter`方法中会将`watcher`实例添加到该数据的依赖列表中，当该数据发生变化时就会通知依赖列表中所有的依赖，依赖接收到通知后就会调用第四个参数回调函数去更新视图。

换句话说，上面代码中把`updateComponent`函数作为第二个参数传给`Watcher`类从而创建了`watcher`实例，那么`updateComponent`函数中读取的所有数据都将被`watcher`所监控，这些数据中只要有任何一个发生了变化，那么`watcher`都将会得到通知，从而会去调用第四个参数回调函数去更新视图，如此反复，直到实例被销毁。



这样就完成了挂载阶段的另一半工作。

如此之后，挂载阶段才算是全部完成了，接下来调用挂载完成的生命周期钩子函数`mounted`。

### 总结

本篇文章介绍了生命周期中的第三个阶段——挂载阶段。

在该阶段中所做的主要工作是创建`Vue`实例并用其替换`el`选项对应的`DOM`元素，同时还要开启对模板中数据（状态）的监控，当数据（状态）发生变化时通知其依赖进行视图更新。

我们将挂载阶段所做的工作分成两部分进行了分析，第一部分是将模板渲染到视图上，第二部分是开启对模板中数据（状态）的监控。两部分工作都完成以后挂载阶段才算真正的完成了。

## 销毁阶段


### 前言

接下来到了生命周期流程的最后一个阶段——销毁阶段。从官方文档给出的生命周期流程图中可以看到，当调用了`vm.$destroy`方法，`Vue`实例就进入了销毁阶段，该阶段所做的主要工作是将当前的`Vue`实例从其父级实例中删除，取消当前实例上的所有依赖追踪并且移除实例上的所有事件监听器。也就是说，当这个阶段完成之后，当前的`Vue`实例的整个生命流程就全部走完了，最终“寿终正寝”了。

![](~@/learn-vue-source-code/lifecycle/7.png)


本篇文章就来分析一下在销毁阶段都做了哪些工作。

### 销毁阶段分析

上文说了，当调用了实例的`$destroy`方法之后，当前实例就进入了销毁阶段。所以分析销毁阶段就是分析`$destroy`方法的内部实现。该方法的定义位于源码的`src/core/instance.lifecycle.js`中，如下：

```javascript
Vue.prototype.$destroy = function () {
  const vm: Component = this
  if (vm._isBeingDestroyed) {
    return
  }
  callHook(vm, 'beforeDestroy')
  vm._isBeingDestroyed = true
  // remove self from parent
  const parent = vm.$parent
  if (parent && !parent._isBeingDestroyed && !vm.$options.abstract) {
    remove(parent.$children, vm)
  }
  // teardown watchers
  if (vm._watcher) {
    vm._watcher.teardown()
  }
  let i = vm._watchers.length
  while (i--) {
    vm._watchers[i].teardown()
  }
  // remove reference from data ob
  // frozen object may not have observer.
  if (vm._data.__ob__) {
    vm._data.__ob__.vmCount--
  }
  // call the last hook...
  vm._isDestroyed = true
  // invoke destroy hooks on current rendered tree
  vm.__patch__(vm._vnode, null)
  // fire destroyed hook
  callHook(vm, 'destroyed')
  // turn off all instance listeners.
  vm.$off()
  // remove __vue__ reference
  if (vm.$el) {
    vm.$el.__vue__ = null
  }
  // release circular reference (##6759)
  if (vm.$vnode) {
    vm.$vnode.parent = null
  }
}
```

可以看到，在上述代码中，首先判断当前实例的`_isBeingDestroyed`属性是否为`true`，因为该属性标志着当前实例是否处于正在被销毁的状态，如果它为`true`，则直接`return`退出函数，防止反复执行销毁逻辑。如下：

```javascript
const vm: Component = this
if (vm._isBeingDestroyed) {
  return
}
```

接着，触发生命周期钩子函数`beforeDestroy`，该钩子函数的调用标志着当前实例正式开始销毁。如下：

```javascript
callHook(vm, 'beforeDestroy')
```

接下来，就进入了当前实例销毁的真正逻辑。

首先，需要将当前的`Vue`实例从其父级实例中删除，如下：

```javascript
const parent = vm.$parent
if (parent && !parent._isBeingDestroyed && !vm.$options.abstract) {
  remove(parent.$children, vm)
}
```

上面代码表示：如果当前实例有父级实例，同时该父级实例没有被销毁并且不是抽象组件，那么就将当前实例从其父级实例的`$children`属性中删除，即将自己从父级实例的子实例列表中删除。

把自己从父级实例的子实例列表中删除之后，接下来就开始将自己身上的依赖追踪和事件监听移除。

我们知道， 实例身上的依赖包含两部分：一部分是实例自身依赖其他数据，需要将实例自身从其他数据的依赖列表中删除；另一部分是实例内的数据对其他数据的依赖（如用户使用`$watch`创建的依赖），也需要从其他数据的依赖列表中删除实例内数据。所以删除依赖的时候需要将这两部分依赖都删除掉。如下：

```javascript
// teardown watchers
if (vm._watcher) {
  vm._watcher.teardown()
}
let i = vm._watchers.length
while (i--) {
  vm._watchers[i].teardown()
}
```

在上述代码中，首先执行`vm._watcher.teardown()`将实例自身从其他数据的依赖列表中删除，`teardown`方法的作用是从所有依赖向的`Dep`列表中将自己删除。然后，在前面文章介绍`initState`函数时我们知道，所有实例内的数据对其他数据的依赖都会存放在实例的`_watchers`属性中，所以我们只需遍历`_watchers`，将其中的每一个`watcher`都调用`teardown`方法，从而实现移除实例内数据对其他数据的依赖。

接下来移除实例内响应式数据的引用、给当前实例上添加`_isDestroyed`属性来表示当前实例已经被销毁，同时将实例的`VNode`树设置为`null`，如下：

```javascript
if (vm._data.__ob__) {
  vm._data.__ob__.vmCount--
}
vm._isDestroyed = true
vm.__patch__(vm._vnode, null)
```

接着，触发生命周期钩子函数`destroyed`，如下：

```javascript
callHook(vm, 'destroyed')
```

最后，调用实例的`vm.$off`方法（关于该方法在后面介绍实例方法时会详细介绍），移除实例上的所有事件监听器。如下：

```javascript
vm.$off()
```

最后，再移除一些相关属性的引用，至此，当前实例算是销毁完毕。

### 总结

本篇文章介绍了生命周期流程的最后一个阶段——销毁阶段。

我们知道了，当调用了实例上的`vm.$destory`方法后，实例就进入了销毁阶段，在该阶段所做的主要工作是将当前的`Vue`实例从其父级实例中删除，取消当前实例上的所有依赖追踪并且移除实例上的所有事件监听器。并且对照源码将所做的工作都进行了逐行分析。

# 6. 实例方法篇

## 数据相关的方法

###  前言

与数据相关的实例方法有 3 个，分别是`vm.$set`、`vm.$delete`和`vm.$watch`。它们是在`stateMixin`函数中挂载到`Vue`原型上的，代码如下：

```javascript
import { set, del } from "../observer/index";

export function stateMixin(Vue) {
  Vue.prototype.$set = set;
  Vue.prototype.$delete = del;
  Vue.prototype.$watch = function(expOrFn, cb, options) {};
}
```

当执行`stateMixin`函数后，会向`Vue`原型上挂载上述 3 个实例方法。

接下来，我们就来分析这 3 个与数据相关的实例方法其内部的原理都是怎样的。

###  vm.\$watch

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$watch(expOrFn, callback, [options]);
```

- **参数**：

  - `{string | Function} expOrFn`
  - `{Function | Object} callback`
  - `{Object} [options]`
    - `{boolean} deep`
    - `{boolean} immediate`

- **返回值**：`{Function} unwatch`

- **用法**：

  观察 `Vue` 实例变化的一个表达式或计算属性函数。回调函数得到的参数为新值和旧值。表达式只接受监督的键路径。对于更复杂的表达式，用一个函数取代。

  注意：在变异 (不是替换) 对象或数组时，旧值将与新值相同，因为它们的引用指向同一个对象/数组。`Vue` 不会保留变异之前值的副本。

- **示例**：

  ```javascript
  // 键路径
  vm.$watch("a.b.c", function(newVal, oldVal) {
    // 做点什么
  });

  // 函数
  vm.$watch(
    function() {
      // 表达式 `this.a + this.b` 每次得出一个不同的结果时
      // 处理函数都会被调用。
      // 这就像监听一个未被定义的计算属性
      return this.a + this.b;
    },
    function(newVal, oldVal) {
      // 做点什么
    }
  );
  ```

  `vm.$watch` 返回一个取消观察函数，用来停止触发回调：

  ```javascript
  var unwatch = vm.$watch("a", cb);
  // 之后取消观察
  unwatch();
  ```

- **选项：deep**

  为了发现对象内部值的变化，可以在选项参数中指定 `deep: true` 。注意监听数组的变动不需要这么做。

  ```javascript
  vm.$watch("someObject", callback, {
    deep: true
  });
  vm.someObject.nestedValue = 123;
  // callback is fired
  ```

- **选项：immediate**

  在选项参数中指定 `immediate: true` 将立即以表达式的当前值触发回调：

  ```javascript
  vm.$watch("a", callback, {
    immediate: true
  });
  // 立即以 `a` 的当前值触发回调
  ```

  注意在带有 `immediate` 选项时，你不能在第一次回调时取消侦听给定的 property。

  ```javascript
  // 这会导致报错
  var unwatch = vm.$watch(
    "value",
    function() {
      doSomething();
      unwatch();
    },
    { immediate: true }
  );
  ```

  如果你仍然希望在回调内部调用一个取消侦听的函数，你应该先检查其函数的可用性：

  ```javascript
  var unwatch = vm.$watch(
    "value",
    function() {
      doSomething();
      if (unwatch) {
        unwatch();
      }
    },
    { immediate: true }
  );
  ```

#### 2 内部原理

`$watch`的定义位于源码的`src/core/instance/state.js`中，如下：

```javascript
Vue.prototype.$watch = function(expOrFn, cb, options) {
  const vm: Component = this;
  if (isPlainObject(cb)) {
    return createWatcher(vm, expOrFn, cb, options);
  }
  options = options || {};
  options.user = true;
  const watcher = new Watcher(vm, expOrFn, cb, options);
  if (options.immediate) {
    cb.call(vm, watcher.value);
  }
  return function unwatchFn() {
    watcher.teardown();
  };
};
```

可以看到，`$watch`方法的代码并不多，逻辑也不是很复杂。

在函数内部，首先判断传入的回调函数是否为一个对象，就像下面这种形式：

```javascript
vm.$watch("a.b.c", {
  handler: function(val, oldVal) {
    /* ... */
  },
  deep: true
});
```

如果传入的回调函数是个对象，那就表明用户是把第二个参数回调函数`cb`和第三个参数选项`options`合起来传入的，此时调用`createWatcher`函数，该函数定义如下：

```javascript
function createWatcher(vm, expOrFn, handler, options) {
  if (isPlainObject(handler)) {
    options = handler;
    handler = handler.handler;
  }
  if (typeof handler === "string") {
    handler = vm[handler];
  }
  return vm.$watch(expOrFn, handler, options);
}
```

可以看到，该函数内部其实就是从用户合起来传入的对象中把回调函数`cb`和参数`options`剥离出来，然后再以常规的方式调用`$watch`方法并将剥离出来的参数穿进去。

接着获取到用户传入的`options`，如果用户没有传入则将其赋值为一个默认空对象，如下：

```javascript
options = options || {};
```

`$watch`方法内部会创建一个`watcher`实例，由于该实例是用户手动调用`$watch`方法创建而来的，所以给`options`添加`user`属性并赋值为`true`，用于区分用户创建的`watcher`实例和`Vue`内部创建的`watcher`实例，如下：

```javascript
options.user = true;
```

接着，传入参数创建一个`watcher`实例，如下：

```javascript
const watcher = new Watcher(vm, expOrFn, cb, options);
```

接着判断如果用户在选项参数`options`中指定的`immediate`为`true`，则立即用被观察数据当前的值触发回调，如下：

```javascript
if (options.immediate) {
  cb.call(vm, watcher.value);
}
```

最后返回一个取消观察函数`unwatchFn`，用来停止触发回调。如下：

```javascript
return function unwatchFn() {
  watcher.teardown();
};
```

这个取消观察函数`unwatchFn`内部其实是调用了`watcher`实例的`teardown`方法，那么我们来看一下这个`teardown`方法是如何实现的。其代码如下：

```javascript
export default class Watcher {
  constructor(/* ... */) {
    // ...
    this.deps = [];
  }
  teardown() {
    let i = this.deps.length;
    while (i--) {
      this.deps[i].removeSub(this);
    }
  }
}
```

在之前介绍变化侦测篇的文章中我们说过，谁读取了数据，就表示谁依赖了这个数据，那么谁就会存在于这个数据的依赖列表中，当这个数据变化时，就会通知谁。也就是说，如果谁不想依赖这个数据了，那么只需从这个数据的依赖列表中把谁删掉即可。

在上面代码中，创建`watcher`实例的时候会读取被观察的数据，读取了数据就表示依赖了数据，所以`watcher`实例就会存在于数据的依赖列表中，同时`watcher`实例也记录了自己依赖了哪些数据，另外我们还说过，每个数据都有一个自己的依赖管理器`dep`，`watcher`实例记录自己依赖了哪些数据其实就是把这些数据的依赖管理器`dep`存放在`watcher`实例的`this.deps = []`属性中，当取消观察时即`watcher`实例不想依赖这些数据了，那么就遍历自己记录的这些数据的依赖管理器，告诉这些数据可以从你们的依赖列表中把我删除了。

举个例子：

```javascript
vm.$watch(
  function() {
    return this.a + this.b;
  },
  function(newVal, oldVal) {
    // 做点什么
  }
);
```

例如上面`watcher`实例，它观察了数据`a`和数据`b`，那么它就依赖了数据`a`和数据`b`，那么这个`watcher`实例就存在于数据`a`和数据`b`的依赖管理器`depA`和`depB`中，同时`watcher`实例的`deps`属性中也记录了这两个依赖管理器，即`this.deps=[depA,depB]`，

当取消观察时，就遍历`this.deps`，让每个依赖管理器调用其`removeSub`方法将这个`watcher`实例从自己的依赖列表中删除。

下面还有最后一个问题，当选项参数`options`中的`deep`属性为`true`时，如何实现深度观察呢？

首先我们来看看什么是深度观察，假如有如下被观察的数据：

```javascript
obj = {
  a: 2
};
```

所谓深度观察，就是当`obj`对象发生变化时我们会得到通知，通知当`obj.a`属性发生变化时我们也要能得到通知，简单的说就是观察对象内部值的变化。

要实现这个功能也不难，我们知道，要想让数据变化时通知我们，那我们只需成为这个数据的依赖即可，因为数据变化时会通知它所有的依赖，那么如何成为数据的依赖呢，很简单，读取一下数据即可。也就是说我们只需在创建`watcher`实例的时候把`obj`对象内部所有的值都递归的读一遍，那么这个`watcher`实例就会被加入到对象内所有值的依赖列表中，之后当对象内任意某个值发生变化时就能够得到通知了。

有了初步的思想后，接下来我们看看代码中是如何实现的。我们知道，在创建`watcher`实例的时候，会执行`Watcher`类中`get`方法来读取一下被观察的数据，如下：

```javascript
export default class Watcher {
  constructor(/* ... */) {
    // ...
    this.value = this.get();
  }
  get() {
    // ...
    // "touch" every property so they are all tracked as
    // dependencies for deep watching
    if (this.deep) {
      traverse(value);
    }
    return value;
  }
}
```

可以看到，在`get`方法中，如果传入的`deep`为`true`，则会调用`traverse`函数，并且在源码中，对于这一步操作有个很形象的注释：

```text
"touch" every property so they are all tracked as dependencies for deep watching

“触摸”每个属性，以便将它们全部作为深度监视的依赖项进行跟踪
```

所谓“触摸”每个属性，不就是将每个属性都读取一遍么？哈哈

回到代码，`traverse`函数定义如下：

```javascript
const seenObjects = new Set();

export function traverse(val: any) {
  _traverse(val, seenObjects);
  seenObjects.clear();
}

function _traverse(val: any, seen: SimpleSet) {
  let i, keys;
  const isA = Array.isArray(val);
  if (
    (!isA && !isObject(val)) ||
    Object.isFrozen(val) ||
    val instanceof VNode
  ) {
    return;
  }
  if (val.__ob__) {
    const depId = val.__ob__.dep.id;
    if (seen.has(depId)) {
      return;
    }
    seen.add(depId);
  }
  if (isA) {
    i = val.length;
    while (i--) _traverse(val[i], seen);
  } else {
    keys = Object.keys(val);
    i = keys.length;
    while (i--) _traverse(val[keys[i]], seen);
  }
}
```

可以看到，该函数其实就是个递归遍历的过程，把被观察数据的内部值都递归遍历读取一遍。

首先先判断传入的`val`类型，如果它不是`Array`或`object`，再或者已经被冻结，那么直接返回，退出程序。如下：

```javascript
const isA = Array.isArray(val);
if ((!isA && !isObject(val)) || Object.isFrozen(val) || val instanceof VNode) {
  return;
}
```

然后拿到`val`的`dep.id`，存入创建好的集合`seen`中，因为集合相比数据而言它有天然的去重效果，以此来保证存入的`dep.id`没有重复，不会造成重复收集依赖，如下：

```javascript
if (val.__ob__) {
  const depId = val.__ob__.dep.id;
  if (seen.has(depId)) {
    return;
  }
  seen.add(depId);
}
```

接下来判断如果是数组，则循环数组，将数组中每一项递归调用`_traverse`；如果是对象，则取出对象所有的`key`，然后执行读取操作，再递归内部值，如下：

```javascript
if (isA) {
  i = val.length;
  while (i--) _traverse(val[i], seen);
} else {
  keys = Object.keys(val);
  i = keys.length;
  while (i--) _traverse(val[keys[i]], seen);
}
```

这样，把被观察数据内部所有的值都递归的读取一遍后，那么这个`watcher`实例就会被加入到对象内所有值的依赖列表中，之后当对象内任意某个值发生变化时就能够得到通知了。

###  vm.\$set

`vm.$set` 是全局 `Vue.set` 的**别名**，其用法相同。

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$set(target, propertyName / index, value);
```

- **参数**：

  - `{Object | Array} target`
  - `{string | number} propertyName/index`
  - `{any} value`

- **返回值**：设置的值。

- **用法**：

  向响应式对象中添加一个属性，并确保这个新属性同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新属性，因为 `Vue` 无法探测普通的新增属性 (比如 `this.myObject.newProperty = 'hi'`)

- **注意**：对象不能是 `Vue` 实例，或者 `Vue` 实例的根数据对象。

#### 2 内部原理

还记得我们在介绍数据变化侦测的时候说过，对于`object`型数据，当我们向`object`数据里添加一对新的`key/value`或删除一对已有的`key/value`时，`Vue`是无法观测到的；而对于`Array`型数据，当我们通过数组下标修改数组中的数据时，`Vue`也是是无法观测到的；

正是因为存在这个问题，所以`Vue`设计了`set`和`delete`这两个方法来解决这一问题，下面我们就先来看看`set`方法的内部实现原理。

`set`方法的定义位于源码的`src/core/observer/index.js`中，如下：

```javascript
export function set(target, key, val) {
  if (
    process.env.NODE_ENV !== "production" &&
    (isUndef(target) || isPrimitive(target))
  ) {
    warn(
      `Cannot set reactive property on undefined, null, or primitive value: ${(target: any)}`
    );
  }
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.length = Math.max(target.length, key);
    target.splice(key, 1, val);
    return val;
  }
  if (key in target && !(key in Object.prototype)) {
    target[key] = val;
    return val;
  }
  const ob = (target: any).__ob__;
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== "production" &&
      warn(
        "Avoid adding reactive properties to a Vue instance or its root $data " +
          "at runtime - declare it upfront in the data option."
      );
    return val;
  }
  if (!ob) {
    target[key] = val;
    return val;
  }
  defineReactive(ob.value, key, val);
  ob.dep.notify();
  return val;
}
```

可以看到，方法内部的逻辑并不复杂，就是根据不同的情况作出不同的处理。

首先判断在非生产环境下如果传入的`target`是否为`undefined`、`null`或是原始类型，如果是，则抛出警告，如下：

```javascript
if (
  process.env.NODE_ENV !== "production" &&
  (isUndef(target) || isPrimitive(target))
) {
  warn(
    `Cannot set reactive property on undefined, null, or primitive value: ${(target: any)}`
  );
}
```

接着判断如果传入的`target`是数组并且传入的`key`是有效索引的话，那么就取当前数组长度与`key`这两者的最大值作为数组的新长度，然后使用数组的`splice`方法将传入的索引`key`对应的`val`值添加进数组。这里注意一点，为什么要用`splice`方法呢？还记得我们在介绍`Array`类型数据的变化侦测方式时说过，数组的`splice`方法已经被我们创建的拦截器重写了，也就是说，当使用`splice`方法向数组内添加元素时，该元素会自动被变成响应式的。如下：

```javascript
if (Array.isArray(target) && isValidArrayIndex(key)) {
  target.length = Math.max(target.length, key);
  target.splice(key, 1, val);
  return val;
}
```

如果传入的`target`不是数组，那就当做对象来处理。

首先判断传入的`key`是否已经存在于`target`中，如果存在，表明这次操作不是新增属性，而是对已有的属性进行简单的修改值，那么就只修改属性值即可，如下：

```javascript
if (key in target && !(key in Object.prototype)) {
  target[key] = val;
  return val;
}
```

接下来获取到`target`的`__ob__`属性，我们说过，该属性是否为`true`标志着`target`是否为响应式对象，接着判断如果`tragte`是 `Vue` 实例，或者是 `Vue` 实例的根数据对象，则抛出警告并退出程序，如下：

```javascript
const ob = (target: any).__ob__;
if (target._isVue || (ob && ob.vmCount)) {
  process.env.NODE_ENV !== "production" &&
    warn(
      "Avoid adding reactive properties to a Vue instance or its root $data " +
        "at runtime - declare it upfront in the data option."
    );
  return val;
}
```

接着判断如果`ob`属性为`false`，那么表明`target`不是一个响应式对象，那么我们只需简单给它添加上新的属性，不用将新属性转化成响应式，如下：

```javascript
if (!ob) {
  target[key] = val;
  return val;
}
```

最后，如果`target`是对象，并且是响应式，那么就调用`defineReactive`方法将新属性值添加到`target`上，`defineReactive`方会将新属性添加完之后并将其转化成响应式，最后通知依赖更新，如下：

```javascript
defineReactive(ob.value, key, val);
ob.dep.notify();
```

以上，就是`set`方法的内部原理。其逻辑流程图如下：

![](~@/learn-vue-source-code/instanceMethods/1.jpg)

###  vm.\$delete

`vm.$delete` 是全局 `Vue.delete`的**别名**，其用法相同。

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$delete(target, propertyName / index);
```

- **参数**：

  - `{Object | Array} target`
  - `{string | number} propertyName/index`

  > 仅在 2.2.0+ 版本中支持 Array + index 用法。

- **用法**：

  删除对象的属性。如果对象是响应式的，确保删除能触发更新视图。这个方法主要用于避开 `Vue` 不能检测到属性被删除的限制，但是你应该很少会使用它。

  > 在 2.2.0+ 中同样支持在数组上工作。

* **注意**： 目标对象不能是一个 `Vue` 实例或 `Vue` 实例的根数据对象。

#### 2 内部原理

`delete`方法是用来解决 `Vue` 不能检测到属性被删除的限制，该方法的定义位于源码的`src/core.observer/index.js`中，如下：

```javascript
export function del(target, key) {
  if (
    process.env.NODE_ENV !== "production" &&
    (isUndef(target) || isPrimitive(target))
  ) {
    warn(
      `Cannot delete reactive property on undefined, null, or primitive value: ${(target: any)}`
    );
  }
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.splice(key, 1);
    return;
  }
  const ob = (target: any).__ob__;
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== "production" &&
      warn(
        "Avoid deleting properties on a Vue instance or its root $data " +
          "- just set it to null."
      );
    return;
  }
  if (!hasOwn(target, key)) {
    return;
  }
  delete target[key];
  if (!ob) {
    return;
  }
  ob.dep.notify();
}
```

该方法的内部原理与`set`方法有几分相似，都是根据不同情况作出不同处理。

首先判断在非生产环境下如果传入的`target`不存在，或者`target`是原始值，则抛出警告，如下：

```javascript
if (
  process.env.NODE_ENV !== "production" &&
  (isUndef(target) || isPrimitive(target))
) {
  warn(
    `Cannot set reactive property on undefined, null, or primitive value: ${(target: any)}`
  );
}
```

接着判断如果传入的`target`是数组并且传入的`key`是有效索引的话，就使用数组的`splice`方法将索引`key`对应的值删掉，为什么要用`splice`方法上文中也解释了，就是因为数组的`splice`方法已经被我们创建的拦截器重写了，所以使用该方法会自动通知相关依赖。如下：

```javascript
if (Array.isArray(target) && isValidArrayIndex(key)) {
  target.splice(key, 1);
  return;
}
```

如果传入的`target`不是数组，那就当做对象来处理。

接下来获取到`target`的`__ob__`属性，我们说过，该属性是否为`true`标志着`target`是否为响应式对象，接着判断如果`tragte`是 `Vue` 实例，或者是 `Vue` 实例的根数据对象，则抛出警告并退出程序，如下：

```javascript
const ob = (target: any).__ob__;
if (target._isVue || (ob && ob.vmCount)) {
  process.env.NODE_ENV !== "production" &&
    warn(
      "Avoid adding reactive properties to a Vue instance or its root $data " +
        "at runtime - declare it upfront in the data option."
    );
  return val;
}
```

接着判断传入的`key`是否存在于`target`中，如果`key`本来就不存在于`target`中，那就不用删除，直接退出程序即可，如下：

```javascript
if (!hasOwn(target, key)) {
  return;
}
```

最后，如果`target`是对象，并且传入的`key`也存在于`target`中，那么就从`target`中将该属性删除，同时判断当前的`target`是否为响应式对象，如果是响应式对象，则通知依赖更新；如果不是，删除完后直接返回不通知更新，如下：

```javascript
delete target[key];
if (!ob) {
  return;
}
ob.dep.notify();
```

以上，就是`delete`方法的内部原理。

## 事件相关的方法

###  前言

与事件相关的实例方法有4个，分别是`vm.$on`、`vm.$emit`、`vm.$off`和`vm.$once`。它们是在`eventsMixin`函数中挂载到`Vue`原型上的，代码如下：

```javascript
export function eventsMixin (Vue) {
    Vue.prototype.$on = function (event, fn) {}
    Vue.prototype.$once = function (event, fn) {}
    Vue.prototype.$off = function (event, fn) {}
    Vue.prototype.$emit = function (event) {}
}
```

当执行`eventsMixin`函数后，会向`Vue`原型上挂载上述4个实例方法。

 接下来，我们就来分析这4个与事件相关的实例方法其内部的原理都是怎样的。

###  vm.$on

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$on( event, callback )
```

- **参数**：

  - `{string | Array<string>} event` (数组只在 2.2.0+ 中支持)
  - `{Function} callback`

- **作用**：

  监听当前实例上的自定义事件。事件可以由`vm.$emit`触发。回调函数会接收所有传入事件触发函数的额外参数。

- **示例**：

  ```javascript
  vm.$on('test', function (msg) {
    console.log(msg)
  })
  vm.$emit('test', 'hi')
  // => "hi"
  ```

#### 2 内部原理

在介绍内部原理之前，我们先有一个这样的概念：`$on`和`$emit`这两个方法的内部原理是设计模式中最典型的发布订阅模式，首先定义一个事件中心，通过`$on`订阅事件，将事件存储在事件中心里面，然后通过`$emit`触发事件中心里面存储的订阅事件。

OK，有了这个概念之后，接下来，我们就先来看看`$on`方法的内部原理。该方法的定义位于源码的`src/core/instance/event.js`中，如下：

```javascript
Vue.prototype.$on = function (event, fn) {
    const vm: Component = this
    if (Array.isArray(event)) {
        for (let i = 0, l = event.length; i < l; i++) {
            this.$on(event[i], fn)
        }
    } else {
        (vm._events[event] || (vm._events[event] = [])).push(fn)
    }
    return vm
}
```

`$on`方法接收两个参数，第一个参数是订阅的事件名，可以是数组，表示订阅多个事件。第二个参数是回调函数，当触发所订阅的事件时会执行该回调函数。

首先，判断传入的事件名是否是一个数组，如果是数组，就表示需要一次性订阅多个事件，就遍历该数组，将数组中的每一个事件都递归调用`$on`方法将其作为单个事件订阅。如下：

```javascript
if (Array.isArray(event)) {
    for (let i = 0, l = event.length; i < l; i++) {
        this.$on(event[i], fn)
    }
}
```

如果不是数组，那就当做单个事件名来处理，以该事件名作为`key`，先尝试在当前实例的`_events`属性中获取其对应的事件列表，如果获取不到就给其赋空数组为默认值，并将第二个参数回调函数添加进去。如下：

```javascript
else {
    (vm._events[event] || (vm._events[event] = [])).push(fn)
}
```

那么问题来了，当前实例的`_events`属性是干嘛的呢？

还记得我们在介绍生命周期初始化阶段的初始化事件`initEvents`函数中，在该函数中，首先在当前实例上绑定了`_events`属性并给其赋值为空对象，如下：

```javascript
export function initEvents (vm: Component) {
    vm._events = Object.create(null)
    // ...

}
```

这个`_events`属性就是用来作为当前实例的事件中心，所有绑定在这个实例上的事件都会存储在事件中心`_events`属性中。

以上，就是`$on`方法的内部原理。

###  vm.$emit

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$emit( eventName, […args] )
```

- **参数**：
  - `{string} eventName`
  - `[...args]`
- **作用**：
  触发当前实例上的事件。附加参数都会传给监听器回调。

#### 2 内部原理

该方法接收的第一个参数是要触发的事件名，之后的附加参数都会传给被触发事件的回调函数。该方法的定义位于源码的`src/core/instance/event.js`中，如下：

```javascript
Vue.prototype.$emit = function (event: string): Component {
    const vm: Component = this
    let cbs = vm._events[event]
    if (cbs) {
      cbs = cbs.length > 1 ? toArray(cbs) : cbs
      const args = toArray(arguments, 1)
      for (let i = 0, l = cbs.length; i < l; i++) {
        try {
          cbs[i].apply(vm, args)
        } catch (e) {
          handleError(e, vm, `event handler for "${event}"`)
        }
      }
    }
    return vm
  }
}
```

该方法的逻辑很简单，就是根据传入的事件名从当前实例的`_events`属性（即事件中心）中获取到该事件名所对应的回调函数`cbs`，如下：

```javascript
let cbs = vm._events[event]
```

然后再获取传入的附加参数`args`，如下：

```javascript
const args = toArray(arguments, 1)
```

由于`cbs`是一个数组，所以遍历该数组，拿到每一个回调函数，执行回调函数并将附加参数`args`传给该回调。如下：

```javascript
for (let i = 0, l = cbs.length; i < l; i++) {
    try {
        cbs[i].apply(vm, args)
    } catch (e) {
        handleError(e, vm, `event handler for "${event}"`)
    }
}
```

以上，就是`$emit`方法的内部原理。



###  vm.$off

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$off( [event, callback] )
```

- **参数**：

  - `{string | Array<string>} event` (只在 2.2.2+ 支持数组)
  - `{Function} [callback]`

- **作用**：

  移除自定义事件监听器。

  - 如果没有提供参数，则移除所有的事件监听器；
  - 如果只提供了事件，则移除该事件所有的监听器；
  - 如果同时提供了事件与回调，则只移除这个回调的监听器。

#### 2 内部原理

通过用法回顾我们知道，该方法用来移除事件中心里面某个事件的回调函数，根据所传入参数的不同，作出不同的处理。该方法的定义位于源码的`src/core/instance/event.js`中，如下：

```javascript
Vue.prototype.$off = function (event, fn) {
    const vm: Component = this
    // all
    if (!arguments.length) {
        vm._events = Object.create(null)
        return vm
    }
    // array of events
    if (Array.isArray(event)) {
        for (let i = 0, l = event.length; i < l; i++) {
            this.$off(event[i], fn)
        }
        return vm
    }
    // specific event
    const cbs = vm._events[event]
    if (!cbs) {
        return vm
    }
    if (!fn) {
        vm._events[event] = null
        return vm
    }
    if (fn) {
        // specific handler
        let cb
        let i = cbs.length
        while (i--) {
            cb = cbs[i]
            if (cb === fn || cb.fn === fn) {
                cbs.splice(i, 1)
                break
            }
        }
    }
    return vm
}
```

可以看到，在该方法内部就是通过不断判断所传参数的情况进而进行不同的逻辑处理，接下来我们逐行分析。

首先，判断如果没有传入任何参数（即`arguments.length`为0），这就是第一种情况：如果没有提供参数，则移除所有的事件监听器。我们知道，当前实例上的所有事件都存储在事件中心`_events`属性中，要想移除所有的事件，那么只需把`_events`属性重新置为空对象即可。如下：

```javascript
if (!arguments.length) {
    vm._events = Object.create(null)
    return vm
}
```

接着，判断如果传入的需要移除的事件名是一个数组，就表示需要一次性移除多个事件，那么我们只需同订阅多个事件一样，遍历该数组，然后将数组中的每一个事件都递归调用`$off`方法进行移除即可。如下：

```javascript
if (Array.isArray(event)) {
    for (let i = 0, l = event.length; i < l; i++) {
        this.$off(event[i], fn)
    }
    return vm
}
```

接着，获取到需要移除的事件名在事件中心中对应的回调函数`cbs`。如下：

```javascript
const cbs = vm._events[event]
```

接着，判断如果`cbs`不存在，那表明在事件中心从来没有订阅过该事件，那就谈不上移除该事件，直接返回，退出程序即可。如下：

```javascript
if (!cbs) {
    return vm
}
```

接着，如果`cbs`存在，但是没有传入回调函数`fn`，这就是第二种情况：如果只提供了事件，则移除该事件所有的监听器。这个也不难，我们知道，在事件中心里面，一个事件名对应的回调函数是一个数组，要想移除所有的回调函数我们只需把它对应的数组设置为`null`即可。如下：

```javascript
if (!fn) {
    vm._events[event] = null
    return vm
}
```

接着，如果既传入了事件名，又传入了回调函数，`cbs`也存在，那这就是第三种情况：如果同时提供了事件与回调，则只移除这个回调的监听器。那么我们只需遍历所有回调函数数组`cbs`，如果`cbs`中某一项与`fn`相同，或者某一项的`fn`属性与`fn`相同，那么就将其从数组中删除即可。如下：

```javascript
if (fn) {
    // specific handler
    let cb
    let i = cbs.length
    while (i--) {
        cb = cbs[i]
        if (cb === fn || cb.fn === fn) {
            cbs.splice(i, 1)
            break
        }
    }
}
```

以上，就是`$off`方法的内部原理。









###  vm.$once

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$once( event, callback )
```

- **参数**：

  - `{string} event`
  - `{Function} callback`

- **作用**：

  监听一个自定义事件，但是只触发一次。一旦触发之后，监听器就会被移除。

#### 2 内部原理

该方法的作用是先订阅事件，但是该事件只能触发一次，也就是说当该事件被触发后会立即移除。要实现这个功能也不难，我们可以定义一个子函数，用这个子函数来替换原本订阅事件所对应的回调，也就是说当触发订阅事件时，其实执行的是这个子函数，然后再子函数内部先把该订阅移除，再执行原本的回调，以此来达到只触发一次的目的。

下面我们就来看下源码的实现。该方法的定义位于源码的`src/core/instance/event.js`中，如下：

```javascript
Vue.prototype.$once = function (event, fn) {
    const vm: Component = this
    function on () {
        vm.$off(event, on)
        fn.apply(vm, arguments)
    }
    on.fn = fn
    vm.$on(event, on)
    return vm
}
```

可以看到，在上述代码中，被监听的事件是`event`，其原本对应的回调是`fn`，然后定义了一个子函数`on`。

在该函数内部，先通过`$on`方法订阅事件，同时所使用的回调函数并不是原本的`fn`而是子函数`on`，如下：

```javascript
vm.$on(event, on)
```

也就是说，当事件`event`被触发时，会执行子函数`on`。

然后在子函数内部先通过`$off`方法移除订阅的事件，这样确保该事件不会被再次触发，接着执行原本的回调`fn`，如下：

```javascript
function on () {
    vm.$off(event, on)
    fn.apply(vm, arguments)
}
```

另外，还有一行代码`on.fn = fn`是干什么的呢？

上文我们说了，我们用子函数`on`替换了原本的订阅事件所对应的回调`fn`，那么在事件中心`_events`属性中存储的该事件名就会变成如下这个样子：

```javascript
vm._events = {
    'xxx':[on]
}
```

但是用户自己却不知道传入的`fn`被替换了，当用户在触发该事件之前想调用`$off`方法移除该事件时：

```javascript
vm.$off('xxx',fn)
```

此时就会出现问题，因为在`_events`属性中的事件名`xxx`对应的回调函数列表中没有`fn`，那么就会移除失败。这就让用户费解了，用户明明给`xxx`事件传入的回调函数是`fn`，现在反而找不到`fn`导致事件移除不了了。

所以，为了解决这一问题，我们需要给`on`上绑定一个`fn`属性，属性值为用户传入的回调`fn`，这样在使用`$off`移除事件的时候，`$off`内部会判断如果回调函数列表中某一项的`fn`属性与`fn`相同时，就可以成功移除事件了。

以上，就是`$once`方法的内部原理。

## 生命周期相关的方法

###  前言

与生命周期相关的实例方法有4个，分别是`vm.$mount`、`vm.$forceUpdate`、`vm.$nextTick`和`vm.$destory`。其中，`$forceUpdate`和`$destroy`方法是在`lifecycleMixin`函数中挂载到`Vue`原型上的，`$nextTick`方法是在`renderMixin`函数中挂载到`Vue`原型上的，而`$mount`方法是在跨平台的代码中挂载到`Vue`原型上的。代码如下：

```javascript
export function lifecycleMixin (Vue) {
    Vue.prototype.$forceUpdate = function () {}
    Vue.prototype.$destroy = function (fn) {}
}

export function renderMixin (Vue) {
    Vue.prototype.$nextTick = function (fn) {}
}
```

当执行`lifecycleMixin`和`renderMixin`函数后，会向`Vue`原型上挂载相应的实例方法。

接下来，我们就来分析这4个与生命周期相关的实例方法其内部的原理都是怎样的。

###  vm.$mount

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$mount( [elementOrSelector] )
```

- **参数**：

  - `{Element | string} [elementOrSelector]`
  - `{boolean} [hydrating]`

- **返回值**：`vm` - 实例自身

- **作用**：

  如果 `Vue` 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用 `vm.$mount()` 手动地挂载一个未挂载的实例。

  如果没有提供 `elementOrSelector` 参数，模板将被渲染为文档之外的的元素，并且你必须使用原生 `DOM API `把它插入文档中。

  这个方法返回实例自身，因而可以链式调用其它实例方法。

#### 2 内部原理

关于该方法的内部原理在介绍**生命周期篇的模板编译阶段**中已经详细分析过，此处不再重复。

###  vm.$forceUpdate

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$forceUpdate()
```

- **作用**：

  迫使 `Vue` 实例重新渲染。注意它仅仅影响实例本身和插入插槽内容的子组件，而不是所有子组件。

#### 2 内部原理

通过用法回顾我们知道， 该方法是用来迫使`Vue` 实例重新渲染的。也就是说，当调用了该方法，当前实例会立即重新渲染。

在分析原理之前，我们先思考这样一个问题：什么情况下实例会重新渲染？那就是当实例依赖的数据发生变化时，变化的数据会通知其收集的依赖列表中的依赖进行更新，在之前的文章中我们说过，收集依赖就是收集`watcher`，依赖更新就是`watcher`调用`update`方法更新，所以实例依赖的数据发生变化时，就会通知实例`watcher`去执行`update`方法进行更新。

那么我们就知道了，实例的重新渲染其实就是实例`watcher`执行了`update`方法。

OK，有了这个概念之后，接下来我们来分析`$forceUpdate`源码实现，代码如下：

```javascript
Vue.prototype.$forceUpdate = function () {
    const vm: Component = this
    if (vm._watcher) {
        vm._watcher.update()
    }
}
```

可以看到，源码实现的逻辑跟我们上面分析的是一致的。在之前的文章中我们说过，当前实例的`_watcher`属性就是该实例的`watcher`，所以要想让实例重新渲染，我们只需手动的去执行一下实例`watcher`的`update`方法即可。



###  vm.$nextTick

`vm.$nextTick` 是全局 `Vue.nextTick` 的**别名**，其用法相同。

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$nextTick( [callback] )
```

- **参数**：

  - `{Function} [callback]`

- **用法**：

  将回调延迟到下次 DOM 更新循环之后执行。在修改数据之后立即使用它，然后等待 DOM 更新。它跟全局方法 `Vue.nextTick` 一样，不同的是回调的 `this` 自动绑定到调用它的实例上。

  > 2.1.0 起新增：如果没有提供回调且在支持 Promise 的环境中，则返回一个 Promise。请注意 Vue 不自带 Promise 的 polyfill，所以如果你的目标浏览器不是原生支持 Promise (IE：你们都看我干嘛)，你得自行 polyfill。

从上面的官方文档对`$nextTick`方法的介绍中我们似乎还是不能理解该方法的作用，那么我们举个例子看一下，如下：

```vue
<template>
	<div id="example">{{message}}</div>
</template>
<script>
    var vm = new Vue({
      el: '##example',
      data: {
        message: '123'
      }
    })
    vm.message = 'new message' // 更改数据
    console.log(vm.$el.innerHTML) // '123'
    Vue.nextTick(function () {
      console.log(vm.$el.innerHTML) // 'new message'
    })
</script>
```

在上面例子中，当我们更新了`message`的数据后，立即获取`vm.$el.innerHTML`，发现此时获取到的还是更新之前的数据：123。但是当我们使用`nextTick`来获取`vm.$el.innerHTML`时，此时就可以获取到更新后的数据了。这是为什么呢？

这里就涉及到`Vue`中对`DOM`的更新策略了，`Vue` 在更新 `DOM` 时是**异步**执行的。只要侦听到数据变化，`Vue` 将开启一个事件队列，并缓冲在同一事件循环中发生的所有数据变更。如果同一个 `watcher` 被多次触发，只会被推入到事件队列中一次。这种在缓冲时去除重复数据对于避免不必要的计算和 `DOM` 操作是非常重要的。然后，在下一个的事件循环“tick”中，`Vue` 刷新事件队列并执行实际 (已去重的) 工作。

在上面这个例子中，当我们通过 `vm.message = 'new message'`更新数据时，此时该组件不会立即重新渲染。当刷新事件队列时，组件会在下一个事件循环“tick”中重新渲染。所以当我们更新完数据后，此时又想基于更新后的 `DOM` 状态来做点什么，此时我们就需要使用`Vue.nextTick(callback)`，把基于更新后的`DOM` 状态所需要的操作放入回调函数`callback`中，这样回调函数将在 `DOM` 更新完成后被调用。

OK，现在大家应该对`nextTick`是什么、为什么要有`nextTick`以及怎么使用`nextTick`有个大概的了解了。那么问题又来了，`Vue`为什么要这么设计？为什么要异步更新`DOM`？这就涉及到另外一个知识：`JS`的运行机制。

#### 2 JS的运行机制

我们知道 `JS` 执行是单线程的，它是基于事件循环的。事件循环大致分为以下几个步骤：

1. 所有同步任务都在主线程上执行，形成一个执行栈（`execution context stack`）。
2. 主线程之外，还存在一个"任务队列"（`task queue`）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
3. 一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
4. 主线程不断重复上面的第三步。

主线程的执行过程就是一个 `tick`，而所有的异步结果都是通过 “任务队列” 来调度。 任务队列中存放的是一个个的任务（`task`）。 规范中规定 `task` 分为两大类，分别是宏任务(`macro task`) 和微任务(`micro task`），并且每执行完一个个宏任务(`macro task`)后，都要去清空该宏任务所对应的微任务队列中所有的微任务(`micro task`），他们的执行顺序如下所示：

```javascript
for (macroTask of macroTaskQueue) {
    // 1. 处理当前的宏任务
    handleMacroTask();

    // 2. 处理对应的所有微任务
    for (microTask of microTaskQueue) {
        handleMicroTask(microTask);
    }
}
```

在浏览器环境中，常见的

- 宏任务(`macro task`) 有 `setTimeout`、`MessageChannel`、`postMessage`、`setImmediate`；
- 微任务(`micro task`）有`MutationObsever` 和 `Promise.then`。

OK，有了这个概念之后，接下来我们就进入正菜：从`Vue`源码角度来分析`nextTick`的实现原理。

#### 3 内部原理

`nextTick` 的定义位于源码的`src/core/util/next-tick.js`中，其大概可分为两大部分：

1. 能力检测
2. 根据能力检测以不同方式执行回调队列

##### 检测

`Vue` 在内部对异步队列尝试使用原生的 `Promise.then`、`MutationObserver` 和 `setImmediate`，如果执行环境不支持，则会采用 `setTimeout(fn, 0)` 代替。

宏任务耗费的时间是大于微任务的，所以在浏览器支持的情况下，优先使用微任务。如果浏览器不支持微任务，使用宏任务；但是，各种宏任务之间也有效率的不同，需要根据浏览器的支持情况，使用不同的宏任务。

这一部分的源码如下：

```javascript
let microTimerFunc
let macroTimerFunc
let useMacroTask = false

/* 对于宏任务(macro task) */
// 检测是否支持原生 setImmediate(高版本 IE 和 Edge 支持)
if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {
    macroTimerFunc = () => {
        setImmediate(flushCallbacks)
    }
}
// 检测是否支持原生的 MessageChannel
else if (typeof MessageChannel !== 'undefined' && (
    isNative(MessageChannel) ||
    // PhantomJS
    MessageChannel.toString() === '[object MessageChannelConstructor]'
)) {
    const channel = new MessageChannel()
    const port = channel.port2
    channel.port1.onmessage = flushCallbacks
    macroTimerFunc = () => {
        port.postMessage(1)
    }
}
// 都不支持的情况下，使用setTimeout
else {
    macroTimerFunc = () => {
        setTimeout(flushCallbacks, 0)
    }
}

/* 对于微任务(micro task) */
// 检测浏览器是否原生支持 Promise
if (typeof Promise !== 'undefined' && isNative(Promise)) {
    const p = Promise.resolve()
    microTimerFunc = () => {
        p.then(flushCallbacks)
    }
}
// 不支持的话直接指向 macro task 的实现。
else {
    // fallback to macro
    microTimerFunc = macroTimerFunc
}
```

首先声明了两个变量： `microTimerFunc` 和 `macroTimerFunc` ，它们分别对应的是 `micro task` 的函数和 `macro task` 的函数。对于 `macro task` 的实现，优先检测是否支持原生 `setImmediate`，这是一个高版本 `IE` 和`Edge` 才支持的特性，不支持的话再去检测是否支持原生的 `MessageChannel`，如果也不支持的话就会降级为 `setTimeout 0`；而对于 `micro task` 的实现，则检测浏览器是否原生支持 `Promise`，不支持的话直接指向 `macro task` 的实现。

##### 回调队列

接下来就进入了核心函数`nextTick`中，如下：

```javascript
const callbacks = []   // 回调队列
let pending = false    // 异步锁

// 执行队列中的每一个回调
function flushCallbacks () {
    pending = false     // 重置异步锁
    // 防止出现nextTick中包含nextTick时出现问题，在执行回调函数队列前，提前复制备份并清空回调函数队列
    const copies = callbacks.slice(0)
    callbacks.length = 0
    // 执行回调函数队列
    for (let i = 0; i < copies.length; i++) {
        copies[i]()
    }
}

export function nextTick (cb?: Function, ctx?: Object) {
    let _resolve
    // 将回调函数推入回调队列
    callbacks.push(() => {
        if (cb) {
            try {
                cb.call(ctx)
            } catch (e) {
                handleError(e, ctx, 'nextTick')
            }
        } else if (_resolve) {
            _resolve(ctx)
        }
    })
    // 如果异步锁未锁上，锁上异步锁，调用异步函数，准备等同步函数执行完后，就开始执行回调函数队列
    if (!pending) {
        pending = true
        if (useMacroTask) {
            macroTimerFunc()
        } else {
            microTimerFunc()
        }
    }
    // 如果没有提供回调，并且支持Promise，返回一个Promise
    if (!cb && typeof Promise !== 'undefined') {
        return new Promise(resolve => {
            _resolve = resolve
        })
    }
}
```

首先，先来看 `nextTick`函数，该函数的主要逻辑是：先把传入的回调函数 `cb` 推入 回调队列`callbacks` 数组，同时在接收第一个回调函数时，执行能力检测中对应的异步方法（异步方法中调用了回调函数队列）。最后一次性地根据 `useMacroTask` 条件执行 `macroTimerFunc` 或者是 `microTimerFunc`，而它们都会在下一个 tick 执行 `flushCallbacks`，`flushCallbacks` 的逻辑非常简单，对 `callbacks` 遍历，然后执行相应的回调函数。

`nextTick` 函数最后还有一段逻辑：

```javascript
if (!cb && typeof Promise !== 'undefined') {
  return new Promise(resolve => {
    _resolve = resolve
  })
}
```

这是当 `nextTick` 不传 `cb` 参数的时候，提供一个 Promise 化的调用，比如：

```javascript
nextTick().then(() => {})
```

当 `_resolve` 函数执行，就会跳到 `then` 的逻辑中。

这里有两个问题需要注意：

1. 如何保证只在接收第一个回调函数时执行异步方法？

   `nextTick`源码中使用了一个异步锁的概念，即接收第一个回调函数时，先关上锁，执行异步方法。此时，浏览器处于等待执行完同步代码就执行异步代码的情况。

2. 执行 `flushCallbacks` 函数时为什么需要备份回调函数队列？执行的也是备份的回调函数队列？

   因为，会出现这么一种情况：`nextTick` 的回调函数中还使用 `nextTick`。如果 `flushCallbacks` 不做特殊处理，直接循环执行回调函数，会导致里面`nextTick` 中的回调函数会进入回调队列。



以上就是对 `nextTick` 的源码分析，我们了解到数据的变化到 `DOM` 的重新渲染是一个异步过程，发生在下一个 tick。当我们在实际开发中，比如从服务端接口去获取数据的时候，数据做了修改，如果我们的某些方法去依赖了数据修改后的 DOM 变化，我们就必须在 `nextTick` 后执行。



###  vm.$destory

#### 1 用法回顾

在介绍方法的内部原理之前，我们先根据官方文档示例回顾一下它的用法。

```javascript
vm.$destroy()
```

- **用法**：

  完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器。

  触发 `beforeDestroy` 和 `destroyed` 的钩子。

#### 2 内部原理

关于该方法的内部原理在介绍**生命周期篇的销毁阶段**中已经详细分析过，此处不再重复。


# 7. 全局 API 篇

# 8. 过滤器篇

# 9. 指令篇

# 10. 内置组件篇
