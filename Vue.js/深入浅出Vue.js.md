> 深入浅出 Vue.js  
> 作者: 刘博文  
> 2019 年 3 月第 1 版  
> [图灵社区](https://www.ituring.com.cn/book/2675)

# 第 1 章 Vue.js 简介

## 1.1 什么是 Vue.js

Vue.js，通常被称为 Vue，是一款友好的、多用途且高性能的 JavaScript 框架。

## 1.2 Vue.js 简史

到 2015 年 10 月 26 日这天，Vue.js 终于迎来了 1.0.0 版本的发布。

2016年 10 月 1 日，也是 Vue.js 2.0 发布的日子。

# 第一篇 变化侦测

> Vue.js 最独特的特性之一是看起来并不显眼的响应式系统。数据模型仅仅是普通的 JavaScript 对象。而当你修改它们时，视图会进行更新。这使得状态管理非常简单、直接。不过理解其工作原理同样重要，这样你可以回避一些常见的问题。——官方文档

从状态生成 DOM，再输出到用户界面显示的一整套流程叫作渲染，应用在运行时会不断地进行重新渲染。而响应式系统赋予框架重新渲染的能力，其重要组成部分是变化侦测。变化侦测是响应式系统的核心，没有它，就没有重新渲染。框架在运行时，视图也就无法随着状态的变化而变化。

简单来说，变化侦测的作用是侦测数据的变化。当数据变化时，会通知视图进行相应的更新。

正如文档中所说，深入理解变化侦测的工作原理，既可以帮助我们在开发应用时回避一些很常见的问题，也可以在应用程序出问题时，快速调试并修复问题。

本篇中，我们将针对变化侦测的实现原理做一个详细介绍，并且会带着你一步一步从 0 到 1 实现一个变化侦测的逻辑。学完本篇，你将可以自己实现一个变化侦测的功能。

# 第 2 章 Object 的变化侦测

大部分人不会想到 Object 和 Array 的变化侦测采用不同的处理方式。事实上，它们的侦测方式确实不一样。在这一章中，我们将详细介绍 Object 的变化侦测。

## 2.1 什么是变化侦测

Vue.js 会自动通过状态生成 DOM，并将其输出到页面上显示出来，这个过程叫渲染。Vue.js 的渲染过程是声明式的，我们通过模板来描述状态与 DOM 之间的映射关系。

通常，在运行时应用内部的状态会不断发生变化，此时需要不停地重新渲染。这时如何确定状态中发生了什么变化？

变化侦测就是用来解决这个问题的，它分为两种类型：一种是“推”（push），另一种是“拉”（pull）。

Angular 和 React 中的变化侦测都属于“拉”，这就是说当状态发生变化时，它不知道哪个状态变了，只知道状态有可能变了，然后会发送一个信号告诉框架，框架内部收到信号后，会进行一个暴力比对来找出哪些 DOM 节点需要重新渲染。这在 Angular 中是脏检查的流程，在 React 中使用的是虚拟 DOM。

而 Vue.js 的变化侦测属于“推”。当状态发生变化时，Vue.js 立刻就知道了，而且在一定程度上知道哪些状态变了。因此，它知道的信息更多，也就可以进行更细粒度的更新。

所谓更细粒度的更新，就是说：假如有一个状态绑定着好多个依赖，每个依赖表示一个具体的 DOM 节点，那么当这个状态发生变化时，向这个状态的所有依赖发送通知，让它们进行 DOM 更新操作。相比较而言，“拉”的粒度是最粗的。

但是它也有一定的代价，因为粒度越细，每个状态所绑定的依赖就越多，依赖追踪在内存上的开销就会越大。因此，从 Vue.js 2.0 开始，它引入了虚拟 DOM，将粒度调整为中等粒度，即一个状态所绑定的依赖不再是具体的 DOM 节点，而是一个组件。这样状态变化后，会通知到组件，组件内部再使用虚拟 DOM 进行比对。这可以大大降低依赖数量，从而降低依赖追踪所消耗的内存。

Vue.js 之所以能随意调整粒度，本质上还要归功于变化侦测。因为“推”类型的变化侦测可以随意调整粒度。

## 2.2 如何追踪变化

关于变化侦测，首先要问一个问题，在 JavaScript（简称 JS）中，如何侦测一个对象的变化？

其实这个问题还是比较简单的。学过 JavaScript 的人都知道，有两种方法可以侦测到变化：

1. 使用 `Object.defineProperty`
2. ES6 的 Proxy

由于 ES6 在浏览器中的支持度并不理想，到目前为止 Vue.js 还是使用 `Object.defineProperty` 来实现的，所以书中也会使用它来介绍变化侦测的原理。

> 由于使用 `Object.defineProperty` 来侦测变化会有很多缺陷，所以 Vue.js 的作者尤雨溪说日后会使用 Proxy 重写这部分代码。好在本章讲的是原理和思想，所以即便以后用 Proxy 重写了这部分代码，书中介绍的原理也不会变。

知道了 `Object.defineProperty` 可以侦测到对象的变化，那么我们可以写出这样的代码：

```js
function defineReactive(data, key, val) {
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }
      val = newVal;
    },
  });
}
```

这里的函数 defineReactive 用来对 `Object.defineProperty` 进行封装。从函数的名字可以看出，其作用是定义一个响应式数据。也就是在这个函数中进行变化追踪，封装后只需要传递 data、key 和 val 就行了。

封装好之后，每当从 data 的 key 中读取数据时，get 函数被触发；每当往 data 的 key 中设置数据时，set 函数被触发。

## 2.3 如何收集依赖

如果只是把 `Object.defineProperty` 进行封装，那其实并没什么实际用处，真正有用的是收集依赖。

思考一下，我们之所以要观察数据，其目的是当数据的属性发生变化时，可以通知那些曾经使用了该数据的地方。

举个例子：

```html
<template>
  <h1>{{ name }}</h1>
</template>
```

该模板中使用了数据 name，所以当它发生变化时，要向使用了它的地方发送通知。

> 注意　在 Vue.js 2.0 中，模板使用数据等同于组件使用数据，所以当数据发生变化时，会将通知发送到组件，然后组件内部再通过虚拟 DOM 重新渲染。

回答是，先收集依赖，即把用到数据 name 的地方收集起来，然后等属性发生变化时，把之前收集好的依赖循环触发一遍就好了。

总结起来，其实就一句话，在 getter 中收集依赖，在 setter 中触发依赖。

## 2.4 依赖收集在哪里

现在我们已经有了很明确的目标，就是要在 getter 中收集依赖，那么要把依赖收集到哪里去呢？

思考一下，首先想到的是每个 key 都有一个数组，用来存储当前 key 的依赖。假设依赖是一个函数，保存在 `window.target` 上，现在就可以把 defineReactive 函数稍微改造一下：

```js
function defineReactive(data, key, val) {
  let dep = []; // 新增
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.push(window.target); // 新增
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }
      // 新增
      for (let i = 0; i < dep.length; i++) {
        dep[i](newVal, val);
      }
      val = newVal;
    },
  });
}
```

这里我们新增了数组 dep，用来存储被收集的依赖。

然后在 set 被触发时，循环 dep 以触发收集到的依赖。

但是这样写有点耦合，我们把依赖收集的代码封装成一个 Dep 类，它专门帮助我们管理依赖。使用这个类，我们可以收集依赖、删除依赖或者向依赖发送通知等。其代码如下：

```js
export default class Dep {
  constructor() {
    this.subs = [];
  }
  addSub(sub) {
    this.subs.push(sub);
  }
  removeSub(sub) {
    remove(this.subs, sub);
  }
  depend() {
    if (window.target) {
      this.addSub(window.target);
    }
  }
  notify() {
    const subs = this.subs.slice();
    for (let i = 0, l = subs.length; i < l; i++) {
      subs[i].update();
    }
  }
}
function remove(arr, item) {
  if (arr.length) {
    const index = arr.indexOf(item);
    if (index > -1) {
      return arr.splice(index, 1);
    }
  }
}
```

之后再改造一下 defineReactive：

```js
function defineReactive(data, key, val) {
  let dep = new Dep(); // 修改
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.depend(); // 修改
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }
      val = newVal;
      dep.notify(); // 新增
    },
  });
}
```

此时代码看起来清晰多了，这也顺便回答了上面的问题，依赖收集到哪儿？收集到 Dep 中。

## 2.5 依赖是谁

在上面的代码中，我们收集的依赖是 `window.target`，那么它到底是什么？我们究竟要收集谁呢？

收集谁，换句话说，就是当属性发生变化后，通知谁。

我们要通知用到数据的地方，而使用这个数据的地方有很多，而且类型还不一样，既有可能是模板，也有可能是用户写的一个 watch，这时需要抽象出一个能集中处理这些情况的类。然后，我们在依赖收集阶段只收集这个封装好的类的实例进来，通知也只通知它一个。接着，它再负责通知其他地方。所以，我们要抽象的这个东西需要先起一个好听的名字。嗯，就叫它 Watcher 吧。

现在就可以回答上面的问题了，收集谁？Watcher！

## 2.6 什么是 Watcher

Watcher 是一个中介的角色，数据发生变化时通知它，然后它再通知其他地方。

关于 Watcher，先看一个经典的使用方式：

```js
// keypath
vm.$watch('a.b.c', function (newVal, oldVal) {
  // 做点什么
});
```

这段代码表示当 `data.a.b.c` 属性发生变化时，触发第二个参数中的函数。

思考一下，怎么实现这个功能呢？好像只要把这个 watcher 实例添加到 `data.a.b.c` 属性的 Dep 中就行了。然后，当 `data.a.b.c` 的值发生变化时，通知 Watcher。接着，Watcher 再执行参数中的这个回调函数。

```js
export default class Watcher {
  constructor(vm, expOrFn, cb) {
    this.vm = vm;
    // 执行this.getter()，就可以读取data.a.b.c的内容
    this.getter = parsePath(expOrFn);
    this.cb = cb;
    this.value = this.get();
  }
  get() {
    window.target = this;
    let value = this.getter.call(this.vm, this.vm);
    window.target = undefined;
    return value;
  }
  update() {
    const oldValue = this.value;
    this.value = this.get();
    this.cb.call(this.vm, this.value, oldValue);
  }
}
```

这段代码可以把自己主动添加到 `data.a.b.c` 的 Dep 中去，是不是很神奇？

因为我在 get 方法中先把 `window.target` 设置成了 this，也就是当前 watcher 实例，然后再读一下 `data.a.b.c` 的值，这肯定会触发 getter。

触发了 getter，就会触发收集依赖的逻辑。而关于收集依赖，上面已经介绍了，会从 `window.target` 中读取一个依赖并添加到 Dep 中。

这就导致，只要先在 `window.target` 赋一个 this，然后再读一下值，去触发 getter，就可以把 this 主动添加到 keypath 的 Dep 中。有没有很神奇的感觉啊？

依赖注入到 Dep 中后，每当 `data.a.b.c` 的值发生变化时，就会让依赖列表中所有的依赖循环触发 update 方法，也就是 Watcher 中的 update 方法。而 update 方法会执行参数中的回调函数，将 value 和 oldValue 传到参数中。

所以，其实不管是用户执行的 `vm.$watch('a.b.c', (value, oldValue) => {})`，还是模板中用到的 data，都是通过 Watcher 来通知自己是否需要发生变化。

这里有些小伙伴可能会好奇上面代码中的 parsePath 是怎么读取一个字符串的 keypath 的，下面用一段代码来介绍其实现原理：

```js
/**
 * 解析简单路径
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

可以看到，这其实并不复杂。先将 keypath 用 `.` 分割成数组，然后循环数组一层一层去读数据，最后拿到的 obj 就是 keypath 中想要读的数据。

## 2.7 递归侦测所有 key

现在，其实已经可以实现变化侦测的功能了，但是前面介绍的代码只能侦测数据中的某一个属性，我们希望把数据中的所有属性（包括子属性）都侦测到，所以要封装一个 Observer 类。这个类的作用是将一个数据内的所有属性（包括子属性）都转换成 getter/setter 的形式，然后去追踪它们的变化：

```js
/**
 * Observer类会附加到每一个被侦测的object上。
 * 一旦被附加上，Observer会将object的所有属性转换为getter/setter的形式
 * 来收集属性的依赖，并且当属性发生变化时会通知这些依赖
 */
export class Observer {
  constructor(value) {
    this.value = value;

    if (!Array.isArray(value)) {
      this.walk(value);
    }
  }

  /**
   * walk会将每一个属性都转换成getter/setter的形式来侦测变化
   * 这个方法只有在数据类型为Object时被调用
   */
  walk(obj) {
    const keys = Object.keys(obj);
    for (let i = 0; i < keys.length; i++) {
      defineReactive(obj, keys[i], obj[keys[i]]);
    }
  }
}

function defineReactive(data, key, val) {
  // 新增，递归子属性
  if (typeof val === 'object') {
    new Observer(val);
  }
  let dep = new Dep();
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.depend();
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }

      val = newVal;
      dep.notify();
    },
  });
}
```

在上面的代码中，我们定义了 Observer 类，它用来将一个正常的 object 转换成被侦测的 object。

然后判断数据的类型，只有 Object 类型的数据才会调用 walk 将每一个属性转换成 getter/setter 的形式来侦测变化。

最后，在 defineReactive 中新增 `new Observer(val)`来递归子属性，这样我们就可以把 data 中的所有属性（包括子属性）都转换成 getter/setter 的形式来侦测变化。

当 data 中的属性发生变化时，与这个属性对应的依赖就会接收到通知。

也就是说，只要我们将一个 object 传到 Observer 中，那么这个 object 就会变成响应式的 object。

## 2.8 关于 Object 的问题

前面介绍了 Object 类型数据的变化侦测原理，了解了数据的变化是通过 getter/setter 来追踪的。也正是由于这种追踪方式，有些语法中即便是数据发生了变化，Vue.js 也追踪不到。

比如，向 object 添加属性：

```js
var vm = new Vue({
  el: '#el',
  template: '#demo-template',
  methods: {
    action() {
      this.obj.name = 'berwin';
    },
  },
  data: {
    obj: {},
  },
});
```

在 action 方法中，我们在 obj 上面新增了 name 属性，Vue.js 无法侦测到这个变化，所以不会向依赖发送通知。

再比如，从 obj 中删除一个属性：

```js
var vm = new Vue({
  el: '#el',
  template: '#demo-template',
  methods: {
    action() {
      delete this.obj.name;
    },
  },
  data: {
    obj: {
      name: 'berwin',
    },
  },
});
```

在上面的代码中，我们在 action 方法中删除了 obj 中的 name 属性，而 Vue.js 无法侦测到这个变化，所以不会向依赖发送通知。

Vue.js 通过 `Object.defineProperty` 来将对象的 key 转换成 getter/setter 的形式来追踪变化，但 getter/setter 只能追踪一个数据是否被修改，无法追踪新增属性和删除属性，所以才会导致上面例子中提到的问题。

但这也是没有办法的事，因为在 ES6 之前，JavaScript 没有提供元编程的能力，无法侦测到一个新属性被添加到了对象中，也无法侦测到一个属性从对象中删除了。为了解决这个问题，Vue.js 提供了两个 API——`vm.$set`与`vm.$delete`，第 4 章会详细介绍它们。

## 2.9 总结

变化侦测就是侦测数据的变化。当数据发生变化时，要能侦测到并发出通知。

Object 可以通过 `Object.defineProperty` 将属性转换成 getter/setter 的形式来追踪变化。读取数据时会触发 getter，修改数据时会触发 setter。

我们需要在 getter 中收集有哪些依赖使用了数据。当 setter 被触发时，去通知 getter 中收集的依赖数据发生了变化。

收集依赖需要为依赖找一个存储依赖的地方，为此我们创建了 Dep，它用来收集依赖、删除依赖和向依赖发送消息等。

所谓的依赖，其实就是 Watcher。只有 Watcher 触发的 getter 才会收集依赖，哪个 Watcher 触发了 getter，就把哪个 Watcher 收集到 Dep 中。当数据发生变化时，会循环依赖列表，把所有的 Watcher 都通知一遍。

Watcher 的原理是先把自己设置到全局唯一的指定位置（例如 `window.target`），然后读取数据。因为读取了数据，所以会触发这个数据的 getter。接着，在 getter 中就会从全局唯一的那个位置读取当前正在读取数据的 Watcher，并把这个 Watcher 收集到 Dep 中去。通过这样的方式，Watcher 可以主动去订阅任意一个数据的变化。

此外，我们创建了 Observer 类，它的作用是把一个 object 中的所有数据（包括子数据）都转换成响应式的，也就是它会侦测 object 中所有数据（包括子数据）的变化。

由于在 ES6 之前 JavaScript 并没有提供元编程的能力，所以在对象上新增属性和删除属性都无法被追踪到。

图 2-1 给出了 Data、Observer、Dep 和 Watcher 之间的关系。

图 2-1 Data、Observer、Dep 和 Watcher 之间的关系

Data 通过 Observer 转换成了 getter/setter 的形式来追踪变化。

当外界通过 Watcher 读取数据时，会触发 getter 从而将 Watcher 添加到依赖中。

当数据发生了变化时，会触发 setter，从而向 Dep 中的依赖（Watcher）发送通知。

Watcher 接收到通知后，会向外界发送通知，变化通知到外界后可能会触发视图更新，也有可能触发用户的某个回调函数等。

# 第 3 章 Array 的变化侦测

上一章介绍了 Object 的侦测方式，本章介绍 Array 的侦测方式。

可能很多人不太理解为什么 Array 的侦测方式和 Object 的不同，下面我们举例说明一下：

```js
this.list.push(1);
```

在上面的代码中，我们使用 push 方法向 list 中新增了数字 1。

前面介绍 Object 的时候，我们说过其侦测方式是通过 getter/setter 实现的，但上面这个例子使用了 push 方法来改变数组，并不会触发 getter/setter。

正因为我们可以通过 Array 原型上的方法来改变数组的内容，所以 Object 那种通过 getter/setter 的实现方式就行不通了。

## 3.1 如何追踪变化

Object 的变化是靠 setter 来追踪的，只要一个数据发生了变化，一定会触发 setter。

同理，前面例子中使用 push 来改变数组的内容，那么我们只要能在用户使用 push 操作数组的时候得到通知，就能实现同样目的。

可惜的是，在 ES6 之前，JavaScript 并没有提供元编程的能力，也就是没有提供可以拦截原型方法的能力，但是这难不倒聪明的程序员们。我们可以用自定义的方法去覆盖原生的原型方法。

如图 3-1 所示，我们可以用一个拦截器覆盖 `Array.prototype`。之后，每当使用 Array 原型上的方法操作数组时，其实执行的都是拦截器中提供的方法，比如 push 方法。然后，在拦截器中使用原生 Array 的原型方法去操作数组。

图 3-1 　使用拦截器覆盖原生的原型方法

这样通过拦截器，我们就可以追踪到 Array 的变化。

## 3.2 拦截器

上一节中，我们已经介绍了拦截器的作用，这一节介绍如何实现它。

拦截器其实就是一个和 `Array.prototype` 一样的 Object，里面包含的属性一模一样，只不过这个 Object 中某些可以改变数组自身内容的方法是我们处理过的。

经过整理，我们发现 Array 原型中可以改变数组自身内容的方法有 7 个，分别是 push、pop、shift、unshift、splice、sort 和 reverse。

下面我们写出代码：

```js
const arrayProto = Array.prototype;
export const arrayMethods = Object.create(arrayProto);
['push', 'pop', 'shift', 'unshift', 'splice', 'sort', 'reverse'].forEach(
  function (method) {
    // 缓存原始方法
    const original = arrayProto[method];
    Object.defineProperty(arrayMethods, method, {
      value: function mutator(...args) {
        return original.apply(this, args);
      },
      enumerable: false,
      writable: true,
      configurable: true,
    });
  }
);
```

在上面的代码中，我们创建了变量 arrayMethods，它继承自 `Array.prototype`，具备其所有功能。未来，我们要使用 arrayMethods 去覆盖 `Array.prototype`。

接下来，在 arrayMethods 上使用 `Object.defineProperty` 方法将那些可以改变数组自身内容的方法（push、pop、shift、unshift、splice、sort 和 reverse）进行封装。

所以，当使用 push 方法的时候，其实调用的是 `arrayMethods.push`，而 `arrayMethods.push` 是函数 mutator，也就是说，实际上执行的是 mutator 函数。

最后，在 mutator 中执行 original（它是原生 `Array.prototype` 上的方法，例如 `Array.prototype.push`）来做它应该做的事，比如 push 的功能。

因此，我们就可以在 mutator 函数中做一些其他的事，比如说发送变化通知。

## 3.3 使用拦截器覆盖 Array 原型

有了拦截器之后，想要让它生效，就需要使用它去覆盖 `Array.prototype`。但是我们又不能直接覆盖，因为这样会污染全局的 Array，这并不是我们希望看到的结果。我们希望拦截操作只针对那些被侦测了变化的数据生效，也就是说希望拦截器只覆盖那些响应式数组的原型。

而将一个数据转换成响应式的，需要通过 Observer，所以我们只需要在 Observer 中使用拦截器覆盖那些即将被转换成响应式 Array 类型数据的原型就好了：

```js
export class Observer {
  constructor(value) {
    this.value = value;

    if (Array.isArray(value)) {
      value.__proto__ = arrayMethods; // 新增
    } else {
      this.walk(value);
    }
  }
}
```

在上面的代码中，我们新增了一行代码：

```js
value.__proto__ = arrayMethods;
```

它的作用是将拦截器（加工后具备拦截功能的 arrayMethods）赋值给`value.__proto__`，通过`__proto__`可以很巧妙地实现覆盖 value 原型的功能，如图 3-2 所示。

图 3-2 　使用`__proto__`覆盖原型

`__proto__` 其实是 `Object.getPrototypeOf` 和 `Object.setPrototypeOf` 的早期实现，所以使用 ES6 的 `Object.setPrototypeOf` 来代替`__proto__`完全可以实现同样的效果。只是到目前为止，ES6 在浏览器中的支持度并不理想。

## 3.4 将拦截器方法挂载到数组的属性上

虽然绝大多数浏览器都支持这种非标准的属性（在 ES6 之前并不是标准）来访问原型，但并不是所有浏览器都支持！因此，我们需要处理不能使用`__proto__`的情况。

Vue 的做法非常粗暴，如果不能使用 `__proto__`，就直接将 arrayMethods 身上的这些方法设置到被侦测的数组上：

```js
import { arrayMethods } from './array';

// __proto__ 是否可用
const hasProto = '__proto__' in {};
const arrayKeys = Object.getOwnPropertyNames(arrayMethods);

export class Observer {
  constructor(value) {
    this.value = value;

    if (Array.isArray(value)) {
      // 修改
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
    } else {
      this.walk(value);
    }
  }

  // ……
}

function protoAugment(target, src, keys) {
  target.__proto__ = src;
}

function copyAugment(target, src, keys) {
  for (let i = 0, l = keys.length; i < l; i++) {
    const key = keys[i];
    def(target, key, src[key]);
  }
}
```

在上面的代码中，我们新增了 hasProto 来判断当前浏览器是否支持 `__proto__`。还新增了 copyAugment 函数，用来将已经加工了拦截操作的原型方法直接添加到 value 的属性中。

此外，还使用 hasProto 判断浏览器是否支持 `__proto__`：如果支持，则使用 protoAugment 函数来覆盖原型；如果不支持，则调用 copyAugment 函数将拦截器中的方法挂载到 value 上。

如图 3-3 所示，在浏览器不支持 `__proto__` 的情况下，会在数组上挂载一些方法。当用户使用这些方法时，其实执行的并不是浏览器原生提供的 `Array.prototype` 上的方法，而是拦截器中提供的方法。

图 3-3 　将拦截器方法挂载到数组属性上

因为当访问一个对象的方法时，只有其自身不存在这个方法，才会去它的原型上找这个方法。

## 3.5 如何收集依赖

上一节中，我们介绍并且创建了拦截器。

可能你也发现了，如果只有一个拦截器，其实还是什么事都做不了。为什么会这样呢？因为我们之所以创建拦截器，本质上是为了得到一种能力，一种当数组的内容发生变化时得到通知的能力。

而现在我们虽然具备了这样的能力，但是通知谁呢？前面我们介绍 Object 时说过，答案肯定是通知 Dep 中的依赖（Watcher），但是依赖怎么收集呢？这就是本节要介绍的内容，如何收集数组的依赖！

在这之前，我们先简单回顾一下 Object 的依赖是如何收集的。

Object 的依赖前面介绍过，是在 defineReactive 中的 getter 里使用 Dep 收集的，每个 key 都会有一个对应的 Dep 列表来存储依赖。

简单来说，就是在 getter 中收集依赖，依赖被存储在 Dep 里。

那么，数组在哪里收集依赖呢？其实数组也是在 getter 中收集依赖的。

有些同学可能不明白了，没关系，我们举例说明一下：

```js
{
  list: [1, 2, 3, 4, 5];
}
```

如果是上面这样的数据，那么想得到 list 数组，肯定是要访问 list 这个 key，对吧？

也就是说，其实不管 value 是什么，要想在一个 Object 中得到某个属性的数据，肯定要通过 key 来读取 value。

因此，在读取 list 的时候，肯定会先触发这个名字叫作 list 的属性的 getter，举个例子：

```js
this.list;
```

上面这行代码从 this 上读取 list，所以肯定会触发 list 这个属性的 getter。

而 Array 的依赖和 Object 一样，也在 defineReactive 中收集：

```js
function defineReactive(data, key, val) {
  if (typeof val === 'object') new Observer(val);
  let dep = new Dep();
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.depend();
      // 这里收集Array的依赖
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }

      dep.notify();
      val = newVal;
    },
  });
}
```

上面的代码新增了一段注释，接下来要在这个位置去收集 Array 的依赖。

所以，Array 在 getter 中收集依赖，在拦截器中触发依赖。

## 3.6 依赖列表存在哪儿

知道了如何收集依赖后，下一个要面对的问题是这些依赖列表存在哪儿。Vue.js 把 Array 的依赖存放在 Observer 中：

```js
export class Observer {
  constructor(value) {
    this.value = value;
    this.dep = new Dep(); // 新增dep

    if (Array.isArray(value)) {
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
    } else {
      this.walk(value);
    }
  }

  // ……
}
```

这个地方有些同学可能会有疑问，为什么数组的 dep（依赖）要保存在 Observer 实例上呢？

上一节中我们介绍了数组在 getter 中收集依赖，在拦截器中触发依赖，所以这个依赖保存的位置就很关键，它必须在 getter 和拦截器中都可以访问到。

我们之所以将依赖保存在 Observer 实例上，是因为在 getter 中可以访问到 Observer 实例，同时在 Array 拦截器中也可以访问到 Observer 实例。

后面会介绍如何在 getter 中访问 Dep 开始收集依赖，以及在拦截器中如何访问 Observer 实例。

## 3.7 收集依赖

把 Dep 实例保存在 Observer 的属性上之后，我们可以在 getter 中像下面这样访问并收集依赖：

```js
function defineReactive(data, key, val) {
  let childOb = observe(val); // 修改
  let dep = new Dep();
  Object.defineProperty(data, key, {
    enumerable: true,
    configurable: true,
    get: function () {
      dep.depend();

      // 新增
      if (childOb) {
        childOb.dep.depend();
      }
      return val;
    },
    set: function (newVal) {
      if (val === newVal) {
        return;
      }

      dep.notify();
      val = newVal;
    },
  });
}

/**
 * 尝试为value创建一个Observer实例，
 * 如果创建成功，直接返回新创建的Observer实例。
 * 如果value已经存在一个Observer实例，则直接返回它
 */
export function observe(value, asRootData) {
  if (!isObject(value)) {
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

在上面的代码中，我们新增了函数 observe，它尝试创建一个 Observer 实例。如果 value 已经是响应式数据，不需要再次创建 Observer 实例，直接返回已经创建的 Observer 实例即可，避免了重复侦测 value 变化的问题。

此外，我们在 defineReactive 函数中调用了 observe，它把 val 当作参数传了进去并拿到一个返回值，那就是 Observer 实例。

前面我们介绍过数组为什么在 getter 中收集依赖，而 defineReactive 函数中的 val 很有可能会是一个数组。通过 observe 我们得到了数组的 Observer 实例（childOb），最后通过 childOb 的 dep 执行 depend 方法来收集依赖。

通过这种方式，我们就可以实现在 getter 中将依赖收集到 Observer 实例的 dep 中。更通俗的解释是：通过这样的方式可以为数组收集依赖。

## 3.8 在拦截器中获取 Observer 实例

在本节中，我们将介绍如何在拦截器中访问 Observer 实例。

因为 Array 拦截器是对原型的一种封装，所以可以在拦截器中访问到 this（当前正在被操作的数组）。

而 dep 保存在 Observer 中，所以需要在 this 上读到 Observer 的实例：

```js
// 工具函数
function def(obj, key, val, enumerable) {
  Object.defineProperty(obj, key, {
    value: val,
    enumerable: !!enumerable,
    writable: true,
    configurable: true,
  });
}

export class Observer {
  constructor(value) {
    this.value = value;
    this.dep = new Dep();
    def(value, '__ob__', this); // 新增

    if (Array.isArray(value)) {
      const augment = hasProto ? protoAugment : copyAugment;
      augment(value, arrayMethods, arrayKeys);
    } else {
      this.walk(value);
    }
  }

  // ……
}
```

在上面的代码中，我们在 Observer 中新增了一段代码，它可以在 value 上新增一个不可枚举的属性 `__ob__`，这个属性的值就是当前 Observer 的实例。

这样我们就可以通过数组数据的 `__ob__` 属性拿到 Observer 实例，然后就可以拿到 `__ob__` 上的 dep 啦。

当然，`__ob__` 的作用不仅仅是为了在拦截器中访问 Observer 实例这么简单，还可以用来标记当前 value 是否已经被 Observer 转换成了响应式数据。

也就是说，所有被侦测了变化的数据身上都会有一个 `__ob__` 属性来表示它们是响应式的。上一节中的 observe 函数就是通过 `__ob__` 属性来判断：如果 value 是响应式的，则直接返回 `__ob__`；如果不是响应式的，则使用 new Observer 来将数据转换成响应式数据。

当 value 身上被标记了 `__ob__` 之后，就可以通过 value.`__ob__` 来访问 Observer 实例。如果是 Array 拦截器，因为拦截器是原型方法，所以可以直接通过 `this.__ob__` 来访问 Observer 实例。例如：

```js
['push', 'pop', 'shift', 'unshift', 'splice', 'sort', 'reverse'].forEach(
  function (method) {
    // 缓存原始方法
    const original = arrayProto[method];
    Object.defineProperty(arrayMethods, method, {
      value: function mutator(...args) {
        const ob = this.__ob__; // 新增
        return original.apply(this, args);
      },
      enumerable: false,
      writable: true,
      configurable: true,
    });
  }
);
```

在上面的代码中，我们在 mutator 函数里通过 `this.__ob__` 来获取 Observer 实例。

## 3.9 向数组的依赖发送通知

当侦测到数组发生变化时，会向依赖发送通知。此时，首先要能访问到依赖。前面已经介绍过如何在拦截器中访问 Observer 实例，所以这里只需要在 Observer 实例中拿到 dep 属性，然后直接发送通知就可以了：

```js
['push', 'pop', 'shift', 'unshift', 'splice', 'sort', 'reverse'].forEach(
  function (method) {
    // 缓存原始方法
    const original = arrayProto[method];
    def(arrayMethods, method, function mutator(...args) {
      const result = original.apply(this, args);
      const ob = this.__ob__;
      ob.dep.notify(); // 向依赖发送消息
      return result;
    });
  }
);
```

在上面的代码中，我们调用了 `ob.dep.notify()`去通知依赖（Watcher）数据发生了改变。

## 3.10 侦测数组中元素的变化

前面说过如何侦测数组的变化，指的是数组自身的变化，比如是否新增一个元素，是否删除一个元素等。

其实数组中保存了一些元素，它们的变化也是需要侦测的。比如，当数组中 object 身上某个属性的值发生了变化时，也需要发送通知。

此外，如果用户使用了 push 往数组中新增了元素，这个新增元素的变化也需要侦测。

也就是说，所有响应式数据的子数据都要侦测，不论是 Object 中的数据还是 Array 中的数据。

这里我们先介绍如何侦测所有数据子集的变化，下一节再来介绍如何侦测新增元素的变化。

前面介绍 Observer 时说过，其作用是将 object 的所有属性转换为 getter/setter 的形式来侦测变化。现在 Observer 类不光能处理 Object 类型的数据，还可以处理 Array 类型的数据。

所以，我们要在 Observer 中新增一些处理，让它可以将 Array 也转换成响应式的：

```js
export class Observer {
  constructor(value) {
    this.value = value;
    def(value, '__ob__', this);

    // 新增
    if (Array.isArray(value)) {
      this.observeArray(value);
    } else {
      this.walk(value);
    }
  }

  /**
   * 侦测Array中的每一项
   */
  observeArray(items) {
    for (let i = 0, l = items.length; i < l; i++) {
      observe(items[i]);
    }
  }

  // ……
}
```

在上面的代码中，我们在 Observer 中新增了对 Array 类型数据的处理逻辑。

这里新增了 observeArray 方法，其作用是循环 Array 中的每一项，执行 observe 函数来侦测变化。前面介绍过 observe 函数，其实就是将数组中的每个元素都执行一遍 new Observer，这很明显是一个递归的过程。

现在只要将一个数据丢进去，Observer 就会把这个数据的所有子数据转换成响应式的。接下来，我们介绍如何侦测数组中新增元素的变化。

## 3.11 侦测新增元素的变化

数组中有一些方法是可以新增数组内容的，比如 push，而新增的内容也需要转换成响应式来侦测变化，否则会出现修改数据时无法触发消息等问题。因此，我们必须侦测数组中新增元素的变化。

其实现方式其实并不难，只要能获取新增的元素并使用 Observer 来侦测它们就行。

### 3.11.1 获取新增元素

想要获取新增元素，我们需要在拦截器中对数组方法的类型进行判断。如果操作数组的方法是 push、unshift 和 splice（可以新增数组元素的方法），则把参数中新增的元素拿过来，用 Observer 来侦测：

```js
['push', 'pop', 'shift', 'unshift', 'splice', 'sort', 'reverse'].forEach(
  function (method) {
    // 缓存原始方法
    const original = arrayProto[method];
    def(arrayMethods, method, function mutator(...args) {
      const result = original.apply(this, args);
      const ob = this.__ob__;
      let inserted;
      switch (method) {
        case 'push':
        case 'unshift':
          inserted = args;
          break;
        case 'splice':
          inserted = args.slice(2);
          break;
      }
      ob.dep.notify();
      return result;
    });
  }
);
```

在上面的代码中，我们通过 switch 对 method 进行判断，如果 method 是 push、unshift、splice 这种可以新增数组元素的方法，那么从 args 中将新增元素取出来，暂存在 inserted 中。

接下来，我们要使用 Observer 把 inserted 中的元素转换成响应式的。

### 3.11.2 使用 Observer 侦测新增元素

前面介绍过 Observer 会将自身的实例附加到 value 的 `__ob__` 属性上。所有被侦测了变化的数据都有一个 `__ob__` 属性，数组元素也不例外。

因此，我们可以在拦截器中通过 this 访问到 `__ob__`，然后调用 `__ob__` 上的 observeArray 方法就可以了：

```js
['push', 'pop', 'shift', 'unshift', 'splice', 'sort', 'reverse'].forEach(
  function (method) {
    // 缓存原始方法
    const original = arrayProto[method];
    def(arrayMethods, method, function mutator(...args) {
      const result = original.apply(this, args);
      const ob = this.__ob__;
      let inserted;
      switch (method) {
        case 'push':
        case 'unshift':
          inserted = args;
          break;
        case 'splice':
          inserted = args.slice(2);
          break;
      }
      if (inserted) ob.observeArray(inserted); // 新增
      ob.dep.notify();
      return result;
    });
  }
);
```

在上面的代码中，我们从 `this.__ob__` 上拿到 Observer 实例后，如果有新增元素，则使用 ob.observeArray 来侦测这些新增元素的变化。

## 3.12 关于 Array 的问题

前面介绍过，对 Array 的变化侦测是通过拦截原型的方式实现的。正是因为这种实现方式，其实有些数组操作 Vue.js 是拦截不到的，例如：

```js
this.list[0] = 2;
```

即修改数组中第一个元素的值时，无法侦测到数组的变化，所以并不会触发 re-render 或 watch 等。

例如：

```js
this.list.length = 0;
```

这个清空数组操作也无法侦测到数组的变化，所以也不会触发 re-render 或 watch 等。

因为 Vue.js 的实现方式决定了无法对上面举的两个例子做拦截，也就没有办法响应。在 ES6 之前，无法做到模拟数组的原生行为，所以拦截不到也是没有办法的事情。ES6 提供了元编程的能力，所以有能力拦截，我猜测未来 Vue.js 很有可能会使用 ES6 提供的 Proxy 来实现这部分功能，从而解决这个问题。

## 3.13 总结

Array 追踪变化的方式和 Object 不一样。因为它是通过方法来改变内容的，所以我们通过创建拦截器去覆盖数组原型的方式来追踪变化。

为了不污染全局 `Array.prototype`，我们在 Observer 中只针对那些需要侦测变化的数组使用 `__proto__` 来覆盖原型方法，但 `__proto__` 在 ES6 之前并不是标准属性，不是所有浏览器都支持它。因此，针对不支持 `__proto__` 属性的浏览器，我们直接循环拦截器，把拦截器中的方法直接设置到数组身上来拦截 `Array.prototype` 上的原生方法。

Array 收集依赖的方式和 Object 一样，都是在 getter 中收集。但是由于使用依赖的位置不同，数组要在拦截器中向依赖发消息，所以依赖不能像 Object 那样保存在 defineReactive 中，而是把依赖保存在了 Observer 实例上。

在 Observer 中，我们对每个侦测了变化的数据都标上印记 `__ob__`，并把 this（Observer 实例）保存在 `__ob__` 上。这主要有两个作用，一方面是为了标记数据是否被侦测了变化（保证同一个数据只被侦测一次），另一方面可以很方便地通过数据取到 `__ob__`，从而拿到 Observer 实例上保存的依赖。当拦截到数组发生变化时，向依赖发送通知。

除了侦测数组自身的变化外，数组中元素发生的变化也要侦测。我们在 Observer 中判断如果当前被侦测的数据是数组，则调用 observeArray 方法将数组中的每一个元素都转换成响应式的并侦测变化。

除了侦测已有数据外，当用户使用 push 等方法向数组中新增数据时，新增的数据也要进行变化侦测。我们使用当前操作数组的方法来进行判断，如果是 push、unshift 和 splice 方法，则从参数中将新增数据提取出来，然后使用 observeArray 对新增数据进行变化侦测。

由于在 ES6 之前，JavaScript 并没有提供元编程的能力，所以对于数组类型的数据，一些语法无法追踪到变化，只能拦截原型上的方法，而无法拦截数组特有的语法，例如使用 length 清空数组的操作就无法拦截。

# 第 4 章 变化侦测相关的 API 实现原理

本章将介绍几个与变化侦测相关的常用 API 的内部原理。

## 4.1 vm.\$watch

### 4.1.1 用法

观察 Vue 实例上的一个表达式或者一个函数计算结果的变化。回调函数得到的参数为新值和旧值。表达式只接受简单的键路径。对于更复杂的表达式，用一个函数取代。

```js
vm.$watch(expOrFn, callback, [options]);
```

### 4.1.2 watch 的内部原理

`vm.$watch`其实是对 Watcher 的一种封装，通过 Watcher 完全可以实现`vm.$watch`的功能，但`vm.$watch`中的参数 deep 和 immediate 是 Watcher 中所没有的。下面我们来看一看`vm.$watch`到底是怎么实现的。

```js
Vue.prototype.$watch = function (expOrFn, cb, options) {
  const vm = this;
  options = options || {};
  const watcher = new Watcher(vm, expOrFn, cb, options);
  if (options.immediate) {
    cb.call(vm, watcher.value);
  }
  return function unwatchFn() {
    watcher.teardown();
  };
};
```

先执行 `new Watcher` 来实现`vm.$watch`的基本功能。

这里有一个细节需要注意，expOrFn 是支持函数的，前面未做介绍。这里需要对 Watcher 进行一个简单的修改。

```js
export default class Watcher {
  constructor(vm, expOrFn, cb) {
    this.vm = vm;
    // 执行this.getter()就可以读取data.a.b.c的内容
    if (typeof expOrFn === 'function') {
      this.getter = expOrFn;
    } else {
      this.getter = parsePath(expOrFn);
    }
    this.cb = cb;
    // 保存旧值
    this.value = this.get();
  }
  // ......
}
```

上面的代码新增了判断 expOrFn 类型的逻辑。如果 expOrFn 是函数，则直接将它赋值给 getter；如果不是函数，再使用 parsePath 函数来读取 keypath 中的数据。keypath 指的是属性路径，例如 `a.b.c.d` 就是一个 keypath，说明从 `vm.a.b.c.d` 中读取数据。

当 expOrFn 是函数时，它不只可以动态返回数据，其中读取的所有数据也会被 Watcher 观察。当 expOrFn 是字符串类型的 keypath 时，Watcher 会读取这个 keypath 所指向的数据并观察这个数据的变化。而当 expOrFn 是函数时，Watcher 会同时观察 expOrFn 函数中读取的所有 Vue.js 实例上上的响应式数据。也就是说，如果函数从 Vue.js 实例上读取了两个数据，那么 Watcher 会同时观察这两个数据的变化，当其中任意一个发生变化时，Watcher 都会得到通知。

> 事实上，Vue.js 中计算属性（Computed）的实现原理与 expOrFn 支持函数有很大的关系。

执行 `new Watcher` 后，代码会判断用户是否使用了 immediate 参数，如果使用了，则立即执行一次 cb。

最后，返回一个函数 unwatchFn。其作用是取消观察数据。

当用户执行这个函数时，实例上是执行了`watcher.teardown()`来取消观察数据，其本质是把 watcher 实例从当前正在观察的状态的依赖列表中移除。

实现 Watcher 的 teardown 方法：首先需要在 Watcher 中记录自己订阅了谁，也就是 watcher 实例被收集进了哪些 Dep 里。然后当 Watcher 不想继续订阅这些 Dep 时，循环自己记录的订阅列表来通知它们（Dep）将自己从它们（Dep）的依赖列表中移除掉。

因此，先在 Watcher 中添加 addDep 方法，该方法的作用是在 Watcher 中记录自己都订阅过哪些 Dep。

```js
export default class Watcher {
  constructor(vm, expOrFn, cb) {
    this.vm = vm;
    // 新增
    this.deps = [];
    // 新增
    this.depIds = new Set();
    if (typeof expOrFn === 'function') {
      this.getter = expOrFn;
    } else {
      this.getter = parsePath(expOrFn);
    }
    this.cb = cb;
    this.value = this.get();
  }
  // ......
  addDep(dep) {
    const id = dep.id;
    if (!this.depIds.has(id)) {
      this.depIds.add(id);
      this.deps.push(dep);
      dep.addSub(this);
    }
  }
  // ....
}
```

1. 使用 depIds 来判断如果当前 Watcher 已经订阅了该 Dep，则不会重复订阅。
2. Watcher 读取 value 时，会触发收集依赖的逻辑。当依赖发生变化时，会通知 Watcher 重新读取最新的数据。如果没有这个判断，就会发现每次数据发生了变化，Watcher 都会读取最新的数据。而读数据就会再次收集依赖，这就会导致 Dep 中依赖有重复。这样当数据发生变化时，会同时通知多个 Watcher。为了避免这个问题，只有第一次触发 getter 的时候才会收集依赖。
3. 执行 `this.depIds.add` 来记录当前 Watcher 已经订阅了这个 Dep。
4. 执行 `this.deps.push(dep)`记录自己都订阅了哪些 Dep。
5. 触发 `dep.addSub(this)`，来将自己订阅到 Dep 中。

在 Watcher 中新增 addDep 方法后，Dep 中收集依赖的逻辑也需要有所改变。

```js
// 新增
let uid = 0;
export default class Dep {
  constructor() {
    // 新增
    this.id = uid++;
    this.subs = [];
  }
  // ....
  depend() {
    if (window.target) {
      // 废弃
      // this.addSub(window.target);
      // 新增
      window.target.addDep(this);
    }
  }
  // ...
}
```

此时，Dep 会记录数据发生变化时，需要通知哪些 Watcher，而 Watcher 中也同样记录了自己会被哪些 Dep 通知。（多对多关系）

如果 Watcher 中的 expOrFn 参数是一个表达式，那么肯定只收集一个 Dep，并且大部分都是这样。

但 expOrFn 可以是一个函数，此时如果该函数中使用了多个数据，那么这时 Watcher 就要收集多个 Dep 了

```js
this.$watch(
  function () {
    return this.name + this.age;
  },
  function (newValue, oldValue) {
    console.lognewValue, oldValue();
  }
);
```

上面这个例子，表达式是一个函数，并且在函数中访问了 name 和 age 两个数据。这种情况下，Watcher 内部会收集两个 Dep---name 的 Dep 和 age 的 Dep。同时这两个 Dep 中也会收集 Watcher。这导致 age 和 name 中任意一个数据发生变化时，Watcher 都会收到通知。

言归正传，当我们已经在 Watcher 中记录自己订阅了哪些 Dep 之后，就可以在 Watcher 中新增 teardown 方法来通知订阅的 Dep，让它们把自己从依赖列表中移除掉。

```js
{
  // 从所有依赖项的Dep列表中将自己移除
  teardown(){
    let i = this.deps.length;
    while(1--){
      this.deps[i].removeSub(this);
    }
  }
}
```

上面做的事情很简单，只是循环订阅列表，然后分别执行它们的 removeSub 方法，来把自己从它们的依赖列表中移除掉。接下来，看看 removeSub 中都发生了什么：

```js
export default class Dep {
  // ....
  removeSub(sub) {
    const index = this.subs.indexOf(sub);
    if (index > -1) {
      return this.subs.splice(index, 1);
    }
  }
  // ...
}
```

上面的代码把 Watcher 从 sub 中删除掉，然后当数据发生变化时，将不再通知这个已经删除的 Watcher，这就是 unwatch 的原理。

### 4.1.3 deep 参数的实现原理

Watcher 想监听某个数据，就会触发某个数据收集依赖的逻辑，将自己收集进去，然后当它发生变化时，就会通知 Watcher。

要想实现 deep 的功能，其实就是除了要触发当前这个被监听数据的收集依赖的逻辑之外，还要把当前监听的这个值在内的所有子值都触发一遍收集依赖逻辑。这就可以实现当前这个依赖的所有子数据发生变化时，通知当前 Watcher。

```js
export default class Watcher {
  constructor(vm, expOrFn, cb, options) {
    this.vm = vm;
    // 新增
    if (options) {
      this.deep = !!options.deep;
    } else {
      this.deep = false;
    }
    this.deps = [];
    this.depIds = new Set();
    if (typeof expOrFn === 'function') {
      this.getter = expOrFn;
    } else {
      this.getter = parsePath(expOrFn);
    }
    this.cb = cb;
    this.value = this.get();
  }
  get() {
    // 将this赋值给window.target，用于主动将自己添加到依赖中
    window.target = this;
    // 触发了getter，触发收集依赖，将this主动添加到keypath的Dep中
    let value = this.getter.call(this.vm, this.vm);
    // 新增
    if (this.deep) {
      traverse(value);
    }
    window.target = undefined;
    return value;
  }
  // .....
}
```

在上面的代码中，如果用户使用了 deep 参数，则在 `window.target = undefined` 之前调用 traverse 来处理 deep 的逻辑，这样才能保证子集收集的依赖是当前这个 Watcher。若在其之后，那么其实当前的 Watcher 并不会被收集到子值的依赖列表中，也就无法实现 deep 功能。

接下来，要递归 value 的所有子值来触发它们收集依赖的功能。

```js
const seenObjects = new Set();
export function traverse(val) {
  _traverse(val, seenObjects);
  seenObjects.clear();
}
function _traverse(val, seen) {
  let i, keys;
  const isA = Array.isArray(val);
  if ((!isA && !isObejct(val)) || Object.isFrozen(val)) {
    return;
  }
  if (val._ob_) {
    const depId = val._ob_.dep.id;
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
    while (i--) _traverse(val[(keys[i], seen)]);
  }
}
```

1. 先判 val 类型，如果它不是 Array 和 Object，或者已经被冻结，那么直接返回，什么也不干。
2. 然后拿到 val 的 `dep.id`，用这个 id 来保证不会重复收集依赖。
3. 如果是数组，则循环数组，将数组中每一项递归调用`_traverse`。
4. 如果是 Object 类型的数据，则循环 Object 中所有 key，然后执行一次读取操作，再递归子值

```js
_traverse(val[(keys[i], seen)]);
```

其中 `val[keys[i]` 会触发 getter，也就是说会触发收集依赖的操作，这时 `window.target` 还没有被清空，会将当前 Watcher 收集进去。

而 `_traverse` 函数其实是一个递归操作，所以这个 value 的子值也会触发同样的逻辑，这样就可以实现通过 deep 参数来监听所有子值的变化。

## 4.2 vm.\$set

### 4.2.1 用法

向响应式对象中添加一个 property，并确保这个新 property 同样是响应式的，且触发视图更新。它必须用于向响应式对象上添加新 property，因为 Vue 无法探测普通的新增 property。

```js
Vue.set(target, propertyName / index, value);
```

只有已经存在的属性的变化会被追踪到，新增的属性无法追踪到。因为在 ES6 之前，Javascript 并没有提供元编程的能力，所以根本无法侦测 object 什么时候被添加了一个属性。

而`vm.$set`就是为了解决这个问题而出现的。使用它，可以为 object 新增属性，然后 Vue.js 就可以将这个新增属性转换成响应式的。

举个例子：

```js
var vm = new Vue({
	el:'#el',
	template:'#demo-template',
	methods:{
		action(){
			this.obj.name = 'berwin'
		}
	}
	data:{
		obj:{}
	}
})
```

直接给 obj 设置一个属性，当 action 方法被调用时，会为 obj 新增一个 name 属性，而 Vue.js 并不会得到任何通知，新增的这个属性也不是响应式的，Vue.js 根本不知道这个 obj 新增了属性，就好像 Vue.js 无法知道我们使用 `array.lenght = 0` 清空了数组一样。

`vm.$set`就可以解决这个事情。`vm.$set`实现如下：

```js
import { set } from '../observer/index';
Vue.prototype.$set = set;
```

这里在 Vue.js 的原型上设置`$set`属性。其实我们使用的所有以`vm.$`开头的方法都是在 Vue.js 的原型上设置的。`vm.$set`的具体实现其实是在 observer 中抛出的 set 方法。

所以，先创建一个 set 方法

```js
export function set(target, key, val) {
  //做点什么
}
```

### 4.2.2 Array 的处理

上面创建了 set 方法并且规定它接收 3 个参数，这 3 个参数与 `vm.$set` API 规定的需要传递的参数一致。

接下来，需要对 target 是数组的情况进行处理：

```js
export function set(target, key, val) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.length = Math.max(target.length, key);
    target.splice(key, 1, val);
    return val;
  }
}
```

在上面的代码中，如果 target 是数组并且 key 是一个有效的索引值，就先设置 length 属性。这样如果我们传递的索引值大于当前数组的 length，就需要让 target 的 length 等于索引值。

接下来，通过 splice 方法把 val 设置到 target 中的指定位置（参数中提供的索引值的位置）。当我们使用 splice 方法把 val 设置到 target 中的时候，数组拦截器会侦测到 target 发生了变化，并且会自动帮助我们把这个新增的 val 转换成响应式的。

最后，返回 val 即可。

### 4.2.3 key 已经存在于 target 中

接下来，需要处理参数中的 key 已经存在于 target 中的情况：

```js
export function set(target, key, val) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.length = Math.max(target.length, key);
    target.splice(key, 1, val);
    return val;
  }
  // 新增
  if (key in target && !(key in Object.prototype)) {
    target[key] = val;
    return val;
  }
}
```

由于 key 已经存在于 target 中，所以其实这个 key 已经被侦测了变化。也就是说，这种情况属于修改数据，直接用 key 和 val 改数据就好了。修改数据的动作会被 Vue.js 侦测到，所以数据发生变化后，会自动向依赖发送通知。

### 4.2.4 处理新增的属性

终于到了重头戏，现在来处理在 target 上新增的 key：

```js
export function set(target, key, val) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.length = Math.max(target.length, key);
    target.splice(key, 1, val);
    return val;
  }
  if (key in target && !(key in Object.prototype)) {
    target[key] = val;
    return val;
  }
  // 新增
  const ob = target._ob_;
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' &&
      warn(
        'Avoid adding reactive properties to a Vue instance or its root $data' +
          'at runtime - declare it upfront in the data option'
      );
    return val;
  }
  if (!ob) {
    target[key] = val;
    return val;
  }
  defineReactive(ob.value, key, val);
  ob.dep.notify();
}
```

在上面的代码中，最先做的事情是获取 target 的`__ob__`属性。然后要处理 target 不能是 Vue.js 实例或则 Vue.js 实例的根数据对象的情况。

实现这个功能并不难，只需要使用 `target_isVue` 来判断 target 是不是 Vue.js 实例，使用 ob.vmCount 来判断它是不是根数据对象（`this.$data` 就是根数据）。

接下来，要处理 target 不是响应式的情况。如果 target 身上没有`__ob__`属性，说明它并不是响应式的，并不需要做什么特殊处理，只需要通过 key 和 val 在 target 上设置就行了。

如果前面的所有判断条件都不满足，那么说明用户是在响应式数据上新增了一个属性，这种情况下需要追踪这个新增属性的变化，即使用 defineReactive 将新增属性转换成 getter/setter 的形式即可。

最后，向 target 的依赖发送变化通知，并返回 val。

## 4.3 vm.\$delete

### 4.3.1 用法

主要用于删除对象的 property。如果对象是响应式的，确保删除能触发更新视图。这个方法主要用于避开 Vue 不能检测到 property 被删除的限制，但是你应该很少会使用它。

```js
Vue.delete(target, propertyName / index);
```

### 4.3.2 实现原理

`vm.$delete` 方法也是为了解决变化侦测的缺陷。在 ES6 之前，Javascript 并没有办法侦测到一个属性在 object 中被删除，所以如果使用 delete 来删除一个数据，Vue.js 根本不知道这个属性被删除了。

使用 `vm.$delete` 能帮助我们在删除属性后自动向依赖发送消息，通知 Watcher 数据发生了变化。

其实`vm.$delete`内部的实现原理就是，在删除属性后向依赖发消息。

```js
import { del } from '../observer/index';
Vue.prototype.$delete = del;
```

在 Vue.js 的原型上挂载`$.delete` 方法。而 del 函数的定义如下：

```js
export function del(target, key) {
  const _ob_ = target._ob_;
  delete target[key];
  _ob_.dep.notify();
}
```

这里先从 target 中将属性 key 删除，然后向依赖发送消息。

接下来，要处理数组的情况

```js
export function del(target, key) {
  //新增
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.splice(key, 1);
    return;
  }
  const _ob_ = target._ob_;
  delete target[key];
  _ob_.dep.notify();
}
```

这里只需要使用 splice 将参数 key 所指定的索引位置的元素删除即可。因为使用了 splice 方法，数组拦截器会自动向依赖发送通知。

与 `vm.$set`一样，`vm.$delete` 也不可以在 Vue.js 实例或 Vue.js 实例的跟数据对象上使用。

因此，需要对这种情况进行判断：

```js
export function del(target, key) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.splice(key, 1);
    return;
  }
  const _ob_ = target._ob_;
  //新增
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' &&
      warn(
        'Avoid deleting properties on a Vue instance or its root $data' +
          '- just set it to null'
      );
    return val;
  }
  delete target[key];
  _ob_.dep.notify();
}
```

上面的代码中新增了逻辑判断：如果 target 上有 `_isVue` 属性（target 是 Vue.js 实例）或则 ob.vmCount 数量大于 1（target 是根数据），则直接返回，终止程序继续执行，并且如果是开发环境，会在控制台中发出警告。

如果删除的这个 key 不是 target 自身的属性，就什么都不做，直接退出程序执行。

```js
export function del(target, key) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.splice(key, 1);
    return;
  }
  const _ob_ = target._ob_;
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' &&
      warn(
        'Avoid deleting properties on a Vue instance or its root $data' +
          '- just set it to null'
      );
    return val;
  }
  // 如果key不是target自身的属性,则终止程序继续执行
  if (!hasOwn(target, key)) {
    return;
  }
  delete target[key];
  _ob_.dep.notify();
}
```

如果删除的这个 key 在 target 中根本不存在，那么其实并不需要进行删除操作，也不需要向依赖发送通知。

最后，还要判断 target 是不是一个响应式数据，也就是说要判断 target 身上存不存在`__ob__`属性。只有响应式数据才需要发送通知，非响应式数据只需要执行删除操作即可。

下面这段代码新增了判断条件，如果数据不是响应式的，则使用 return 语句阻止执行发送通知的语句：

```js
export function del(target, key) {
  if (Array.isArray(target) && isValidArrayIndex(key)) {
    target.splice(key, 1);
    return;
  }
  const _ob_ = target._ob_;
  if (target._isVue || (ob && ob.vmCount)) {
    process.env.NODE_ENV !== 'production' &&
      warn(
        'Avoid deleting properties on a Vue instance or its root $data' +
          '- just set it to null'
      );
    return val;
  }
  //如果key不是target自身的属性,则终止程序继续执行
  if (!hasOwn(target, key)) {
    return;
  }
  delete target[key];
  //如果ob不存在,则直接终止程序
  if (!_ob_) {
    return;
  }
  _ob_.dep.notify();
}
```

在上面的代码中，在删除属性后判断 ob 是否存在，如果不存在，则直接终止程序，继续执行下面发送变化通知的代码。

## 4.4 总结

本章中，我们详细介绍了变化侦测相关 API 的内部实现原理。

我们先介绍了`vm.$watch`的内部实现及其相关参数的实现原理，包括 deep、immediate 和 unwatch。

随后介绍了`vm.$set`的内部实现。这里介绍了几种情况，分别为 Array 的处理逻辑，key 已经存在的处理逻辑，以及最红要的新增属性的处理逻辑。

最后，介绍了`vm.$delete`的内部实现原理。

# 第二篇 虚拟 DOM

Vue.js2.0 引入了虚拟 DOM,比 Vue.js1.0 的初始渲染速度提升了 2-4 倍，并大大降低了内存消耗。

虚拟 DOM 也是 React 核心技术之一。它到底有着怎样的魔力，使前端界各大主流框架都纷份使用？

你是否好奇，虚拟 DOM 的原理是什么？

你是否好奇，为什么 Vue.js2.0 开始引入了虚拟 DOM?

你是否好奇，为什么 Vue.js 引入虚拟 DOM 后渲染速度就变快了？

又或者，你根本没听说过虚拟 DOM,那么什么是虚拟 DOM?

这一切的问题，都将在本篇揭晓。

# 第 5 章 虚拟 DOM 简介

## 5.1 什么是虚拟 DOM

我们现在使用的三大主流框架 Vue.js、Angular 和 React 都是声明式操作 DOM。我们通过描述状态和 DOM 之间的映射关系是怎样的，就可以将状态渲染成视图。关于状态到视图的转化过程，框架会帮我们做，不需要我们自己去操作 DOM。

状态可以是 JavaScript 中的任意类型。Object、Array、String、Number、Boolean 等都可以作为状态，这些状态可能最终会以段落、表单、链接或按钮等元素呈现在用户界面上。

本质上，我们将状态作为输入，并生成 DOM 输出在页面上显示出来，这个过程叫做渲染。

然而通常在程序运行时，状态会不断发生改变（状态改变的原因有很多，可能是用户点击了某个按钮，可能是某个 ajax 请求，这些行为都是异步的）每当状态发生变化时，都需要重新渲染。如何确定状态中发生了什么变化以及需要在哪里更新 DOM？

在这种情况下，最简单粗暴的方式是，不需要关心状态发生了什么变化，不需要关心哪里更新 DOM，我们只要把所有 DOM 删除了，然后使用状态重新生成一份 DOM，并将其输出到界面上。

但是访问 DOM 是非常昂贵的，按照上面的方式，会造成相当多的性能浪费。状态变化通常只是有限的几个节点需要重新渲染，所有我们不仅需要找出哪里需要更新，还需要尽可能少的访问 DOM。

如上图所示，当某个状态发生变化时，只更新与这个状态相关联的 DOM 节点。

这个问题有很多种解决方案，目前，各大主流框架都有自己一套解决方案，在 Angular 中就是脏检查的流程，React 中使用虚拟 DOM，vuejs1.0 通过细粒度的绑定。因此，虚拟 DOM 本质上只是众多解决方案中的一种，可以用但并不一定必须用。

虚拟 DOM 的解决方式是通过状态生成一个虚拟节点树，然后使用虚拟节点树进行渲染。在渲染之前，会使用新生成的虚拟节点数和上一次生成的虚拟节点树进行对比，只渲染不同的部分。

虚拟节点数其实是由组件树建立起来的整个虚拟节点（Virtual Node，也简写为 Vnode）树。

## 5.2 为什么要引入虚拟 DOM

事实上，Angular 和 React 的变化侦测有一个共同点，那就是他们都不知道哪些状态变了。因此，就需要进行比较暴力的对比，React 是通过虚拟 DOM 的比对，Angular 是使用脏检查的流程。

Vue.js 的变化侦测不一样，它在一定程度上知道具体哪些状态发生了变化，这样就可以通过更细粒度的绑定来更新视图。也就是说，在 Vue.js 中，当状态发生变化时，它在一定程度上知道哪些节点使用了这个状态，从而对这些节点进行更新操作，不需要对比。事实上，在 vue.js 1.0 中就是这样实现的。

但是这样做也有一定的代价，因为粒度太细，每一个绑定都会有一个对应得 watcher 来观察状态的变化，这样就会有一定的内存开销和追踪依赖的开销。当状态被越多的节点使用时，开销就越大。大型项目来说，这个开销是非常大。

因此，Vue.js 2.0 中选择了中等粒度的解决方案，那就是引入了虚拟 DOM。组件级别是一个 watcher 实例，就是说即便一个组件内有 10 个节点使用了某个状态，但其实也只有一个 watcher 在观察这个状态的变化。所以这个状态发生变化时，只能通知到组件，然后组件内部通过虚拟 DOM 去进行比对和渲染。

## 5.3 Vue.js 中的虚拟 DOM

在 vue.js 中，我们使用模板来描述状态和 DOM 之间的映射关系。Vue.js 通过编译将模板转化为渲染函数 render，执行渲染函数就可以得到一个虚拟节点树，使用这个虚拟节点树就可以渲染页面。

虚拟 DOM 的终极目标是将虚拟节点(vnode)渲染到视图上。但是如果直接使用虚拟节点覆盖旧节点的话，会造成很多不必要的 DOM 操作。

例如一个 ul 标签下有很多 li 标签，其中只有一个 li 变化，这种情况下如果直接用新的 ul 替换旧的 ul，其实除了那个发生了变化的 li 节点之外，其他节点都不需要重新渲染。

由于 DOM 操作比较慢，所以这些 DOM 操作在性能上会有一定的浪费。避免这些不必要的 DOM 操作会提升很大的性能。

为了避免不必要的 DOM 操作，虚拟 DOM 在虚拟节点映射到视图的过程中，将虚拟节点和上一次渲染视图所使用的的旧虚拟节点（oldVnode）进行对比。找出真正需要更新的节点来进行 DOM 操作，可以避免不必要改动的 DOM。

图中给出了虚拟 DOM 的整体运行流程，先将 vnode 和 oldVnode 做对比，然后在更新视图

可以看出虚拟 DOM 在 Vue.js 中所做的事情并没有那么复杂，他主要做了两件事

- 提供与真实 DOM 节点所对应得虚拟节点 vnode
- 将虚拟节点 vnode 和旧虚拟节点 oldvnode 进行对比，然后更新视图。

vnode 是 JavaScript 中一个很普通的对象，这个对象的属性上保存了生成 DOM 节点所需要的一些数据。

对比两个虚拟节点是虚拟 DOM 中最核心的算法（即 patch），他可以判断出哪些节点发生了变化，从而只对发生了变化的节点进行操作。

## 5.4 总结

虚拟 DOM 是讲状态映射成视图的众多解决方案之一，它的运作原理是使用状态生成虚拟节点，然后使用虚拟节点渲染成视图。

之所以需要先使用状态生成虚拟节点，是因为如果直接用状态生成真实的 DOM，会有一定程度上的性能浪费。而先创建虚拟节点再渲染视图，就可以将虚拟节点缓存，然后使用新创建的虚拟节点和上一次缓存的虚拟节点进行对比，然后根据对比结果更新需要更新的 DOM 节点，避免不必要的 DOM 操作。

由于 Vue.js 的变化侦测粒度更细，所以挡状态发生变化时，vue.js 知道的信息更多，一定程度上知道哪些位置使用了窗台。因此，vue.js 可以通过细粒度的绑定来更新视图，vue.js 1.0 就是这样实现的。

但是这么做也有一定的代价。因为粒度太细，就会有很多的 watcher 同时观察这些状态，会有一定的内存开销和依赖追踪依赖的开销，所以 vue.js 2.0 采取了中等粒度的解决方案。状态侦测不再是某个具体节点，而是某个组件，组件内部通过虚拟 DOM 来渲染视图，这样可以大大的缩减依赖数量和 watcher 数量。

Vue.js 中通过模板来描述状态和视图之间的映射关系，所以会将模板编译成渲染函数 render,然后执行渲染函数生成虚拟节点 vnode，最后使用虚拟节点更新视图。

虚拟 DOM 在 vue.js 中所做的事是将虚拟节点 vnode 和旧虚拟节点 oldVnode 进行对比，根据对比结果来进行 DOM 操作来更新视图。

# 第 6 章 VNode

## 6.1 什么是 VNode

在 vue.js 中存在一个 VNode 类，使用它可以实例化不同类型的 vnode 实例，而不同类型的 vnode 实例各自表示不同类型的 DOM 元素。

例如，DOM 元素有元素节点，文本节点，注释节点等，vnode 实例也会对应着有元素节点和文本节点和注释节点。

VNode 类代码如下：

```js
export default class VNode {
  constructor(
    tag,
    data,
    children,
    text,
    elm,
    context,
    componentOptions,
    asyncFactory
  ) {
    this.tag = tag;
    this.data = data;
    this.children = children;
    this.text = text;
    this.elm = elm;
    this.ns = undefined;
    this.context = context;
    this.functionalContext = undefined;
    this.functionalOptions = undefined;
    this.functionalScopeId = undefined;
    this.key = data && data.key;
    this.componentOptions = componentOptions;
    this.componentInstance = undefined;
    this.parent = undefined;
    this.raw = false;
    this.isStatic = false;
    this.isRootInsert = true;
    this.isComment = false;
    this.isCloned = false;
    this.isOnce = false;
    this.asyncFactory = asyncFactory;
    this.asyncMeta = undefined;
    this.isAsyncPlaceholder = false;
  }
  get child() {
    return this.componentInstance;
  }
}
```

从上面的代码可以看出，vnode 只是一个名字，本质上来说就是一个普通的 JavaScript 对象，是从 VNode 类实例化的对象。我们用这个 JavaScript 对象来描述一个真实 DOM 元素的话，那么该 DOM 元素上的所有属性在 VNode 这个对象上都存在对应得属性。

简单来说，vnode 可以理解成节点描述对象，他描述了应该怎样去创建真实的 DOM 节点。

例如，tag 表示一个元素节点的名称，text 表示一个文本节点的文本，children 表示子节点等。vnode 表示一个真实的 DOM 元素，所有真实的 DOM 节点都是用 vnode 创建并插入到页面中。

图中展示了使用 vnode 创建真实的 DOM 并渲染到视图的过程。可以得知，vnode 和视图是一一对应的。我们可以把 vnode 理解成 JavaScript 对象版本的 DOM 元素。

渲染视图的过程是先创建 vnode，然后在使用 vnode 去生成真实的 DOM 元素，最后插入到页面渲染视图。

## 6.2 VNode 的作用

由于每次渲染视图时都是先创建 vnode，然后使用它创建的真实 DOM 插入到页面中，所以可以将上一次渲染视图时先所创建的 vnode 先缓存起来，之后每当需要重新渲染视图时，将新创建的 vnode 和上一次缓存的 vnode 对比，查看他们之间有哪些不一样的地方，找出不一样的地方并基于此去修改真实的 DOM。

Vue.js 目前对状态的侦测策略采用了中等粒度。当状态发生变化时，只通知到组件级别，然后组件内使用虚拟 DOM 来渲染视图。

如图下所示，当某个状态发生变化时，只通知使用了这个状态的组件。也就是说，只要组件使用的众多状态中有一个发生了变化，那么整个组件就要重新渲染。

如果组件只有一个节点发生了变化，那么重新渲染整个组件的所有节点，很明显会造成很大的性能浪费。因此，对 vnode 惊醒缓存，并将上一次的缓存和当前创建的 vnode 对比，只更新有差异的节点就变得很重要。这也是 vnode 最重要的一个作用。

## 6.3 VNode 的类型

vnode 有很多不同的类型，有以下几种：

- 注释节点
- 文本节点
- 元素节点
- 组件节点
- 函数式节点
- 克隆节点

前面介绍了 vnode 是一个 JavaScript 对象，不同类型的 vnode 之间其实属性不同，准确说是有效属性不同。因为当使用 VNode 类创建一个 vnode 时，通过参数为实例设置属性时，无效的属性会默认设置为 undefined 或者 false。对于 vnode 身上的无效属性，直接忽略就好。

### 6.3.1 注释节点

由于创建注释节点的过程非常简单，所以直接通过代码来介绍它有哪些属性：

```js
export const createEmptyVNode = (text) => {
  const node = new VNode();
  node.text = text;
  node.isComment = true;
  return node;
};
```

一个注释节点只有两个有效属性 text 和 isComment。其余属性全是默认 undefined 或者 false。

例如一个真实的注释节点，所对应的 vnode 是下面的样子：

```js
// <!-- 注释节点 -->
{
    text: "注释节点",
    isComment: true
}
```

### 6.3.2 文本节点

文本节点的创建过程也非常简单，代码如下：

```js
export function createTextVNode(val) {
  return new VNode(undefined, undefined, undefined, String(val));
}
```

当文本类型的 vnode 被创建时，它只有一个 text 属性：

```js
{
  text: '文本节点';
}
```

### 6.3.3 克隆节点

克隆节点是将现有节点的属性赋值到新节点中，让新创建的节点和被克隆的节点的属性保持一致，从而实现克隆效果。它的作用是优化静态节点和插槽节点（slot node）。

以静态节点为例，当组件内某个状态发生变化后，当前组件会通过虚拟 DOM 重新渲染视图，静态节点因为它的内容不会改变，所以除了首次渲染需要执行渲染函数获取 vnode 之外，后续更新不需要执行渲染函数重新生成 vnode。因此，这是就会使用创建克隆节点的方法将 vnode 克隆一份，使用克隆节点进行渲染。这样就不需要执行渲染函数生成新的静态节点的 vnode，从而提升一定的性能。

创建克隆节点的代码如下：

```js
export function cloneVNode(vnode, deep) {
  const cloned = new VNode(
    vnode.tag,
    vnode.data,
    vnode.children,
    vnode.text,
    vnode.elm,
    vnode.context,
    vnode.componentOptions,
    vnode.asyncFactory
  );
  cloned.ns = vnode.ns;
  cloned.isStatic = vnode.isStatic;
  cloned.key = vnode.key;
  cloned.isComment = vnode.isComment;
  cloned.isCloned = true;
  if (deep && vnode.children) {
    cloned.children = cloneVNodes(vnode.children);
  }
  return cloned;
}
```

克隆现有节点，只需要将现有节点的属性全部赋值到新节点中。

克隆节点和被克隆节点位移的区别是 isCloned 属性，克隆节点为 true，被克隆的原始节点为 false。

### 6.3.4 元素节点

元素节点通常会存在以下 4 中有效属性。

1. tag：tag 就是一个节点的名称，例如 p、ul、li 和 div 等。
2. data：改属性包含了一些节点上的数据，比如 attrs、class 和 style 等。
3. children：当前节点的子节点列表。
4. context：它是当前组件的 Vue.js 实例

一个真实的元素节点，对应得 vnode 是下面这样：

```js
// <p><span>Hello</span><span>World</span></p>
{
  children: [VNode, VNode],
  context: {...},
  data: {...},
  tag: "p",
  // ...
}
```

### 6.3.5 组件节点

组件节点和元素节点类似，有以下两个独有的属性。

componentOptions：组件节点的选项参数，其中包含了 propsData、tag 和 children 等信息

componentInstance：组件的实例，也就是 Vue.js 的实例。事实上，在 Vue.js 中，每个组件都有一个 Vue.js 实例。

一个组件节点，对应得 vnode 是下面这样：

```js
// <child></child>
{
  componentInstance: {...},
  componentOptions: {...},
  context: {...},
  data: {...},
  tag: "vue-component-1-child",
  ...
}
```

### 6.3.6 函数式组件

函数式节点和组件节点类似，他有两个独有的属性 functionalContext 和 functionalOptions。

通常，一个函数式节点的 vnode 是下面这样：

```js
{
  functionalContext: {...},
  functionalOptions: {...},
  context: {...},
  data: {...},
  tag: "div"
}
```

## 6.4 总结

VNode 是一个类，可以生产不同类型的 vnode 实例，不同类型的实例表示不同类型的真实 DOM。

由于 Vue.js 对组件采用了虚拟 DOM 来更新视图，当属性发生变化时，整个组件都要进行重新渲染的操作，但组件内并不是所有的 DOM 节点都需要更新，所以将 vnode 缓存并将当前新生成的 vnode 和缓存的 vnode 作对比，只对需要更新的部分进行 DOM 操作可以提升很多的性能。

vnode 有很多类型，它们本质上都是 Vnode 实例化出的对象，其唯一区别是属性不同。

# 第 7 章 patch

虚拟 DOM 最核心的部分是 patch,它可以将 vnode 渲染成真实的 DOM。
patch 也可以叫作 pasching 算法，通过它渲染真实 DOM 时，并不是暴力覆盖原有 DOM ，而是比对新旧两个 vnode 之间有哪些不同，然后根据对比结果找出需要更新的节点进行更新。这一点从名字就可以看出，patch 本身就有补丁、修补等意思，其实际作用是在现有 DOM 上进行修改来实现更新视图的目的。
之所以要这么做，主要是因为 DOM 操作的执行速度远不如 JavaScript 的运算速度快，因此，把大量的 DOM 操作搬运到 JavaScript 中，使用 patching 算法来计算出真正需要更新的节点，最大限度地减少 DOM 操作，从而显著提升性能。这本质上其实是使用 JavaScript 的运算成本来替换 DOM 操作的执行成本，而 JavaScript 的运算速度要比 DOM 快很多，这样做很划算，所以才会有虚拟 DOM。

## 7.1 patch 介绍

对比两个 vnode 之间的差异只是 patch 的一部分，这是手段，而不是目的。patch 的目的其实是修改 DOM 节点，也可以理解为渲染视图。上上面说过，patch 不是暴力替换节点，而是在现有 DOM 上进行修改来达到渲染视图的目的。对现有 DOM 进行修改需要做三件事：

1. 创建新增的节点：
2. 删除已经废弃的节点；
3. 修改需要更新的节点。

我们知道 patch 的过程其实就是创建节点、删除节点和修改节点的过程，接下来主要讨论在什么情况下创建新节点，插入到什么位置；在什么情况下删除节点，删除哪个节点；在什么情况下修改节点，修改哪个节点等。

在详细讨论什么情况下需要对节点进行更改之前，我们需要先弄清楚一个问题。
事实上，我一再强闻：之所以需要通过算法来比对两个节点之间的差异，并针对不同的节点进行更新，主要是为了性能考虑。

我们完全可以把整个旧节点从 DOM 中删除，然后使用最新的状态（state）重新生成一份全新的节点并插入到 DOM 中，这种方式完全可以实现功能。

由于我们的最终目的是渲染视图，所以可以发现渲染视图的标准是以 vnode（使用最新状态创建的 vnode）来渲染而不是 oldVnode（上一次渲染 DOM 所创建的 vnode）。

也就是说，当 oldVnode 和 vnode 不一样的时候，以 vnode 为准来渲染视图。

### 7.1.1 新增节点

本节中，我们主要讨论在什么情况下新增节点。之所以讨论什么情况下需要新增节点，本质上是为了使用 JavaScript 的计算成本来换取 DOM 的操作成本。如果一个节点已经存在于 DOM 中，那就不需要重新创建一个同样的节点去替换已经存在的节点。事实上，只有那些因为状态的改变而新增的节点在 DOM 中并不存在时，我们才需要创建一个节点并插入到 DOM 中。

首先，新增节点的一个很明显的场景就是，当 oldVnode 不存在而 vnode 存在时，就需要使用 vnode 生成真实的 DOM 元素并将其插入到视图当中去。

这通常会发生在首次渲染中。因为首次渲染时，DOM 中不存在任何节点，所以 oldVnode 是不存在的。

图 7-1 给出了当 oldVnode 不存在时，直接使用 vnode 创建元素并渲染视图。

图 7-1 使用 vnode 创建元素并渲染视图

图 7-2 给出了首次渲染视图时（页面中没有任何节点，oldVnode 并不存在）,只需要使用 vnode 即可。

图 7-2 首次渲染视图时，使用 vnode 直接渲染

除了上面介绍的情况需要新增节点之外，还有一种情况也需要新增节点。

当 vnode 和 oldVnode 完全不是同一个节点时，需要使用 vnode 生成真实的 DOM 元素并将其插入到视图当中。

前面介绍过，当 oldVnode 和 vnode 不一样的时候，以 vnode 为标准来渲染视图。因此，当 vnode 和 oldVnode 完全不是同一个节点的时候，可以得知 vnode 就是一个全新的节点，而 oldVnode 就是一个被废弃的节点。

这种情况下，我们要做的事情就是使用 vnode 创建一个新 DOM 节点，用它去替换 oldVnode 所对应的真实 DOM 节点，如图 7-3 所示。

图 7.3 使用 vnode 替换 oldVnode

### 7.1.2 删除节点

删除节点的场景上一节略有提及，就是当一个节点只在 oldVode 中存在时，我们需要把它从 DOM 中删除。因为渲染视图时，需要以 vnode 为标准，所以 vnode 中不存在的节点都属于被废弃的节点，而被废弃的节点的需要从 DOM 中删除。
如图 7-3 所示，当 oldVnode 和 voode 完全不是同一个节点时，在 DOM 中需要使用 vnode 创建的新节点替换 oldVnode 所对应的的旧节点，而替换过程是将新创建的 DOM 节点插入到旧节点的旁边，然后再将旧节点删除，从而完成替换过程。

### 7.1.3 更新节点

前面介绍了新增节点和删除节点的场景，我们发现它们之间有一个共同点，那就是两个虚拟节点是完全不同的。由于我们需要以新节点为标准渲染视图，所以这个时候只有两种操作可以执行：将旧节点删除或者创建新增节点。
其实除了前面介绍的场景外，另一个更常见的场景是新旧两个节点是同一个节点。当新旧两个节点是相同的节点时，我们需要对这两个节点进行比较细致的比对，然后对 oldVnode 在视图中所对应的真实节点进行更新。
举个简单的例子，当新旧两个节点是同一个文本节点，但是两个节点的文本不一样时，我们需要重新设置 oldVnode 在视图中所对应的真实 DOM 节点的文本。
图 7-4 给出了用 vnode 中的文字替换 DOM 中文字的过程。视图中的文本节点所包含的文字是“我是文字”，而当状态发生变化时，将文本改成了“我是文字 2”，这时使用改变后的状态生成了新的 vnode,然后将 vnode 与 oldVnode 进行比对，发现它们是同一个节点，再将这两个节点进行更详细的比对，比对结果是文字发生了变化，最后将真实 DOM 节点中的文本改成了 vnode 中的文字“我是文字 2”。

图 7-4 使用 vnode 中的文字替换真实 DOM 中的文字

这里提到对两个相同节点进行更详细的比对，这个比对过程会在 7.4 节中详细介绍。

### 7.1.4 小结

通过前面的介绍，可以发现整个 patch 的过程并不复杂。当 oldVnode 不存在时，直接使用 vnode 渲染视图；当 oldVnode 和 vnode 都存在但并不是同一个节点时，使用 vnode 创建的 DON 元素替换旧的 DOM 元素；当 oldVnode 和 vnode 是同一个节点时，使用更详细的对比操作对真实的 DOM 节点进行更新。

图 7-5 patch 运行流程

## 7.2 创建节点

在 7.1.1 节中，我们介绍了在什么情况下创建元素并将元素渲染到视图。本节中，我们将详细介绍一个元素从创建到渲染的过程。
通过前面的学习，我们知道创建一个真实的 DOM 元素所需的信息都保存在 vnode 中，我们需要通过 Vnode 来创建一个真实的 DOM 元素。而第 6 章又介绍了 vnode 是有类型的，所以在创建 DOM 元素时，最重要的事是根据 vnode 的类型来创建出相同类型的 DOM 元素，然后将 DOM 元素插入到视图中。

事实上，只有三种类型的节点会被创建并插入到 DOM 中：元素节点、注释节点和文本节点。

而要判断 vnode 是否是元素节点，只需要判断它是否具有 tag 属性即可。如果一个 vnode 具有 tag 属性，就认为它是元素属性。接着，我们就可以调用当前环境下的 createElement 方法（在浏览器环境下就是 document.createElement）来创建真实的元素节点。当一个元素节点被创建后，接下来要做的事情就是将它插入到指定的父节点中。
将元素渲染到视图的过程非常简单。只需要调用当前环境下的 appendChild 方法（在浏览器环境下就是调用 parentNode,appendChild）,就可以将一个元素插入到指定的父节点中。如果这个指定的父节点已经被渲染到视图，那么把元素插入到它的下面将会自动将元素渲染到视图。

其实创建元素节点还缺了一个步骤，我们刚刚没有说。元素节点通常都会有子节点 children）,所以当一个元素节点被创建后，我们需要将它的子节点也创建出来并插入到这个刚创建出的节点下面。
创建子节点的过程是一个递归过程。vnode 中的 children 属性保存了当前节点的所有子虚拟节点（child virtual node）,所以只需要将 vnode 中的 children 属性循环一遍，将每个子虚拟节点都执行一遍创建元素的逻辑，就可以实现我们想要的功能。

创建子节点时，子节点的父节点就是当前刚创建出来的这个节点，所以子节点被创建后，会被插入到当前节点的下面。当所有子节点都创建完并插入到当前节点中之后，我们把当前节点插入到指定父节点的下面。如果这个指定的父节点已经被渲染到视图中，那么将当前这个节点插入进去之后，会将当前节点（包括其子节点）渲染到视图中。
图 7-6 给出了从虚拟 DOM 创建真实 DOM,最后渲染到视图的过程。

图 7-6 使用虚拟 DOM 创建真实 DOM 并渲染到视图的过程

图 7-7 给出了一个元素节点从创建到应染视图的过程。
图 7.7 创建元素节点并将其渲染到视图的过程

除了元素节点外，其实还要创建注释节点和文本节点。

在创建节点时，如果 vnode 中不存在 tag 属性，那么它可能会是另外两种节点：注释节点和文本节点。

在第 6 章中介绍 vNode 时，我们介绍过注释节点有一个唯一的标识属性 isComment。在所有类型的 vnode 中，只有注释节点的 isComment 属性是 true,所以通过 isComment 属性就可以判断一个 vnode 是否是注释节点。

当发现一个 vnode 的 tag 属性不存在时，我们可以用 isComment 属性来判断它是注释节点还是文本节点。如果是文本节点，则调用当前环境下的 createTextNode 方法（浏览器环境下调用 document.createTextNode）来创建真实的文本节点并将其插入到指定的父节点中；如果是注释节点，则调用当前环境下的 createComment 方法（浏览器环境下调用 document.createComment 方法）来创建真实的注释节点并将其插入到指定的父节点中。

图 7-8 给出了创建一个节点并将其渲染到视图的全过程。

## 7.3 删除节点

在 7.1.2 节中，我们介绍了在什么情况下需要将元素从视图中删除。本节中，我们将详细介绍一个元素是怎样从视图中删除的。

删除节点的过程非常简单。在 Vue.js 源码中，删除元素的代码并不多，其实现逻辑如下：

```js
function removeVnodes(vnodes, startIdx, endIdx) {
  for (; startIdx <= endIdx; ++startIdx) {
    const ch = vnodes[startIdx];
    if (isDef(ch)) {
      removeVnode(ch.elm);
    }
  }
}
```

简单来说，上面代码实现的功能是删除 vnodes 数组中从 startIdx 指定的位置到 endIdx 指定位置的内容。

removende 用于删除视图中的单个节点，而 removeVnodes 用于删除一组指定的节点。

removeNode 的实现逻辑如下：

```js
const nodeOps = {
  removeChild() {
    nodeOps.removeChild(child);
  },
};

function removeNode(el) {
  const parent = nodeOps.parentNode(el);
  if (isDef(parent)) {
    nodeOps.removeChild(parent, el);
  }
}
```

上面代码的逻辑是将当前元素从它的父节点中删除，其中 nodeOps 是对节点操作的封装。
有同学可能会对 nodeops 感到奇怪，为什么不直接使用`parent.removeChild(child)`删除节点，而是将这个节点操作封装成函数放在 nodeops 里呢？
其实这涉及跨平台渲染的知识，我们知道阿里开发的 Weex 可以让我们使用相同的组件模为 iOS 和 Android 编写原生渲染的应用。也就是说，我们写的 Vue.js 组件可以分别在 iOS 和 Android 环境中进行原生渲染。
而跨平台渲染的本质是在设计框架的时候，要让框架的渲染机制和 DOM 解耦。只要把框架更新 DOM 时的节点操作进行封装，就可以实现跨平台渲染，在不同平台下调用节点的操作。
换言之，如果我们把这些平台下节点操作的封装看成渲染引擎，那么将这些渲染引擎所提供的节点操作的 API 和框架的运行时对接一下，就可以实现将框架中的代码进行原生渲染的目的

这就是将 removeChild 方法封装到 nodeops 中的原因。更多关于跨平台渲染的内容已超出本章的讨论范围，这里不再展开讨论。

## 7.4 更新节点

在 7.13 节中，我们介绍了只有两个节点是同一个节点时，才需要更新元素节点，而更新点并不是很暴力地使用新节点覆盖旧节点，而是通过比对找出新旧两个节点不一样的地方，针对那些不一样的地方进行更新。本节中，我们将介绍节点更新的详细过程。

### 7.4.1 静态节点

在更新节点时，首先需要判断新旧两个虚拟节点是否是静态节点，如果是，就不需要进行更新操作，可以直接跳更新节点的过。

什么是静态节点？

静态节点指的是那些一旦渲染到界面上之后，无论日后状态如何变化，都不会发生任何变化的节点。
例如：

```html
<p>我是静态节点，我不需要发生变化</p>
```

上面这个 HTML 就是一个静态节点，它不会因为状态的变化而发生变化。这个节点一旦被渲染到视图之后，当应用在运行时，无论状态是否发生变化，都不会影响到这个节点，这个节点永远都不需要重新渲染。
了解了静态节点的特点之后，就不难理解为什么需要判断虚拟节点是否是静态节点，从而跳过更新节点的操作过程了。

### 7.4.2 新虚拟节点有文本属性

当新旧两个虚拟节点（vnode 和 oldVnode）不是静态节点，并且有不同的属性时，要以新虚拟节点（vnode）为准来更新视图。根据新节点（vnode）是否有 text 属性，更新节点可以分为两种不同的情况。
如果新生成的虚拟节点（vnode）有 text 属性，那么不论之前旧节点的子节点是什么，直接调用 setTextcontent 方法（在浏览器环境下是 node.textContent 方法）来将视图中 DOM 节点的内容改为虚拟节点（vnode）的 text 属性所保存的文字。
因为更新是以新创建的虚拟节点（vnode）为准的，所以如果新创建的虚拟节点有文本，那么根本就不需要关心之前旧节点中所包含的内容是什么，无论是文本还是元素节点，这都不重要。唯一需要关心的是，如果之前的旧节点也是文本，并且和新节点的文本相同，那么就不需要执行 setTextContent 方法来重复设置相同的文本。

简单来说，就是当新虚拟节点有文本属性，并且和旧虚拟节点的文本属性不一样时，我们可以直接把视图中的真实 DOM 节点的内容改成新虚拟节点的文本。

### 7.4.3 新虚拟节点无文本属性

如果新创建的虚拟节点没有 text 属性，那么它就是一个元素节点。元素节点通常会有子节点，也就是 children 属性，但也有可能没有子节点，所以存在两种不同的情况。

1. 有 children 的情况
   当新创建的虚拟节点有 children 属性时，其实还会有两种情况，那就是要看旧虚拟节点（oldVnode）是否有 children 属性。
   如果旧虚拟节点也有 children 属性，那么我们要对新旧两个虚拟节点的 children 进行一个更详细的对比并更新。更新 children 可能会移动某个子节点的位置，也有可能会删除或新增某个子节点，具体更新 children 的过程我们会在 7.5 节中详细介绍。

如果旧虚拟节点没有 children 属性，那么说明旧虚拟节点要么是一个空标签，要么是有文本的文本节点。如果是文本节点，那么先把文本清空让它变成空标签，然后将新虚拟节点（vnode 中的 children 挨个创建成真实的 DOM 元素节点并将其插入到视图中的 DOM 节点下面。 2. 无 children 的情况
当新创建的虚拟节点既没有 text 属性也没有 children 属性时，这说明这个新创建的节点是一个空节点，它下面既没有文本也没有子节点，这时如果旧虚拟节点（oldVnode）中有子节点就删除子节点，有文本就删除文本。有什么删什么，最后达到视图中是空标签的目的。

### 7.4.4 小结

本节重点讨论了更新节点的详细过程以及处理逻辑，讨论的内容包括新虚拟节点有文本时如何处理，有 children 属性时如何处理，以及没有 children 属性时怎么处理等。图 7-9 给出了更新节点的整体逻辑。

## 7.5 更新子节点

在 7.4 节中，我们详细讨论了更新节点的过程，其中讨论了当新节点的子节点和旧节点的子节点都存在并且不相同时，会进行子节点的更新操作。但我们并没有详细讨论子节点是如何更新的，本节将详细讨论如何更新子节点。
事实上，更新子节点大概可以分为 4 种操作：更新节点、新增节点、删除节点、移动节点位置。因此，更新子节点更多的是在讨论什么情况下需要更新节点，什么情况下新增节点等。
更新子节点首先要对比两个子节点都有哪些不同，然后针对不同的情况做不同的处理。
例如，newChildren（新子节点列表）中有一个节点在 o1dChildren（旧子节点列表）中不到相同的节点，这说明这个节点是因本次状态更改而新增的节点，此时就需要进行新增节点的操作。
再例如，newChildren 中的某个节点和 oldChildren 中的某个节点是同一个节点，但位置不同，这说明这个节点是由于状态变化而位置发生了移动的节点，这时需要进行节点移动的操作。对比两个子节点列表（children）,首先需要做的事情是循环。循环 newChildren（新子节点列表）,每循环到一个新子节点，就去 oldChildren（旧子节点列表）中找到和当前节点相同的那个旧子节点。如果在 oldChildren 中找不到，说明当前子节点是由于状态变化而新增的节点，我们要进行创建节点并插入视图的操作；如果找到了，就做更新操作；如果找到的旧子节的位置和新子节点不同，则需要移动节点等。

### 7.5.1 更新策略

本节主要针对新增节点、更新节点、移动节点、删除节点等操作进行讨论。

1. 创建子节点
   关于新增节点，我们主要讨论什么情况下需要创建节点，以及把创建的节点插入到真实 DOM 子节点中哪个位置的问题。
   前面提到过，新旧两个子节点列表是通过循环进行比对的，所以创建节点的操作是在循环体内执行的，其具体实现是在 oldChildren（旧子节点列表）中寻找本次循环所指向的新子节点。

如果在 oldchildren 中没有找到与本次循环所指向的新子节点相同的节点，那么说明本次循环所指向的新子节点是一个新增节点。对于新增节点，我们需要执行创建节点的操作，并将新创建的节点插入到 oldChildren 中所有未处理节点（未处理就是没有进行任何更新操作的节点）的前面。当节点成功插入 DOM 后，这一轮的循环就结束了。关于创建节点，我们在 7.2 节细介绍过。
你可能会对为什么插入到 oldchildren 中所有未处理节点的前面感到很困惑，没关系，下面我们举例说明一下。
我们先看图 7-11 所示的例子，最上面的 DOM 节点是视图中的真实 DOM 节点。左下角的节点是新创建的虚拟节点，右下角的节点是旧的虚拟节点。
图 7-11 更新子节点的一个小例子
图 7-11 表示已经对前两个子节点进行了更新，当前正在处理第三个子节点。当在右下角的虚拟子节点中找不到与左下角的第三个节点相同的节点时，证明它是新增节点，这时候需要创节点并插入到真实 DOM 中，插入的位置是所有未处理节点的前面，也就是虚线所指定的位置。你可能会说，插入到所有已处理节点的后面不也行吗？不是的，如果这个新节点后面也是一个新增节点呢？
图 7-12 是我们希望插入到真实 DOM 中的位置。而如果以插入到已处理节点后面这样的逻辑插入节点，则会出现如图 7-13 所示的问题。

从图 7-13 中我们会发现，节点插入的位置不是我们希望插入的位置，因为顺序反了，这个节点的位置应该是第四位，而不是第三位。你可能会问，为什么？
因为我们是使用虚拟节点进行对比，而不是真实 DOM 节点做对比，所以是左下角的虚拟节点和右下角的旧虚拟节点进行对比，而右下角的虚拟节点表示已处理的节点只有两个，不包括我们新插入的节点，所以用插入到已处理节点后面这样的逻辑来插入节点，就会插入一个错误的可能你现在又有疑问了，节点插入进真实 DOM 中后，真实 DOM 中的节点越来越多，为什么没看见删除节点的逻辑？
关于删除节点的逻辑，我们将在后面详细介绍。 2. 更新子节点
更新节点本质上是当一个节点同时存在于 newChildren 和 oldChildren 中时需要执行的操作

如图 7-14 所示，两个节点是同一个节点并且位置相同，这种情况下只需要进行更新节点的操作即可。关于更新节点，我们在 7.4 节中已详细介绍过。

但如果 oldChildren 中子节点的位置和本次循环所指向的新子节点的位置不一致时，除了对真实 DOM 节点进行更新操作外，我们还需要对这个真实 DOM 节点进行移动节点的操作。 3. 移动子节点
移动节点通常发生在 newChildren 中的某个节点和 oldChildren 中的某个节点是同一个节点，但是位置不同，所以在真实的 DOM 中需要将这个节点的位置以新虚拟节点的位置为基准进行移动。
如图 7-15 所示，当 oldchildren 中找到的节点和 newchildren 中的节点位置不同时，视图中真实 DOM 节点就会移动到 newChildren 中节点所在的位置。
图 7-15 移动子节点的位置
通过`Node.insertBefore()`方法，我们可以成功地将一个已有节点移动到一个指定的位置。

但怎么得知新虚拟节点的位置是哪里呢？换句话说，怎么知道应该把节点移动到哪里呢？

其实得到这个位置并不难。对比两个子节点列表是通过从左到右循环 newChildren 这个列表，然后每循环一个节点，就去 oldChildren 中寻找与这个节点相同的节点进行处理。也就是说，newChildren 中当前被循环到的这个节点的左边都是被处理过的。那就不难发现，这个节点的位置是所有未处理节点的第一个节点。
所以，只要把需要移动的节点移动到所有未处理节点的最前面，就能实现我们的目的，如图 7-16 所示。

图 7-16 表示正在处理第三个节点，这时在 oldchildren 中找到的相同节点是第四个节点。由于位置不同，所以需要移动节点，移动节点的位置是所有未处理节点的最前面。本例中，将第四个节点移动到所有未处理节点的最前面，就是将节点从第四个变成了第三个。

节点更新并且移动完位置后，开始进行下一轮循环，也就是开始处理 newChildren 中的第四个节点。

关于怎么分辨哪些节点是处理过的，哪些节点是未处理的，我们将在 7.5.3 节中详细讨论。

4. 删除子节点
   删除子节点，本质上是删除那些 oldChildren 中存在但 newChildren 中不存在的节点。
   用图 7-12 来举例，左下角的 newChildren 和右下角的 oldChildren 中前两个节点是相同的。在 newChildren 中，右面两个节点是新增节点；在 oldChildren 中，右边两个节点是废弃的需要被删除的节点。
   可以得出结论，当 newChildren 中的所有节点都被循环了一遍后，也就是循环结束后，如果 oldchildren 中还有剩余的没有被处理的节点，那么这些节点就是被废弃、需要删除的节点。

在图 7-12 中，真实 DOM 节点中有 6 个节点，其中最右面的两个节点是需要删除的节点，当这些废弃的节点被删除后，你会发现真实 DOM 中的子节点和 newChildren 变成一样的了。这不正是我们想要的效果吗？

### 7.5.2 优化策略

通常情况下，并不是所有子节点的位置都会发生移动，一个列表中总有几个节点的位置是不变的。针对这些位置不变的或者说位置可以预测的节点，我们不需要循环来查找，因为我们有一个更快捷的查找方式。
假设有一个场景，我们只是修改了列表中某个数据的内容，而没有新增数据或者删除数据等这种情况下 newChildren 和 oldChildren 中所有节点的位置都是相同的，这时节点的位置就是可以预测的，不需要循环也可以知道 oldchildren 中的哪个节点和被寻找的新子节点是同一个节点。

只需要尝试使用相同位置的两个节点来比对是否是同一个节点：如果恰巧是同一个节点，直接就可以进入更新节点的操作；如果尝试失败了，再用循环的方式来查找节点。
这样做可以很大程度地避免循环 oldChildren 来查找节点，从而使执行速度得到很大的提升如果我们把这种很快速的查找节点的方式称为快捷查找，那么它共有 4 种查找方式，分别是：

- 新前与旧前
- 新后与旧后
- 新后与旧前
- 新前与旧后
  你可能会对“新前”“旧前”这些名词感到困惑，没关系，因为这是我自己起的名字。接下来，我将详细介绍这些名词都是什么意思。
  从图 7-17 中可以看出“新前”“新后”“旧前”“旧后”这 4 个名词分别对应 4 个节点，图有两个虚拟节点，左边那个虚拟节点是由于状态的变化而新生成的虚拟节点，右边那个虚拟节点是上一次渲染 DOM 时用的旧的虚拟节点。
- 新前：newChildren 中所有未处理的第一个节点。
- 新后：newChildren 中所有未处理的最后一个节点
- 旧前：oldChildren 中所有未处理的第一个节点。
- 旧后：oldChildren 中所有未处理的最后一个节点。
  图 7-17“新前”“新后”“旧前”“旧后”所代表的节点
  现在我们已经清楚了这些名词的意思，前文中提到比较快捷的查找方式有 4 种，接下来我们详细介绍这 4 种方式。

1. 新前与旧前
   顾名思义，“新前”与“旧前”的意思就是尝试使用“新前”这个节点与“旧前”这个节点对比，对比它们俩是不是同一个节点。如果是同一个节点，则说明我们不费吹灰之力就在 oldchildrer 中找到了这个虚拟节点，然后使用 7.4 节中介绍的更新节点操作将它们俩进行对比并更新视图，如图
   7-18 所示。

图 7-18 尝试对比“新前”与“旧前”这两个节点是否是同一个节点

由于“新前”与“旧前”的位置相同，所以并不需要执行移动节点的操作，只需要更新节点即可。
如果不是同一个节点，没关系，一共有 4 种快捷查找方式，挨个试一遍即可。如果都不行，最后再使用循环来查找节点。 2. 新后与旧后
当“新前”与“旧前”对比后发现不是同一个节点，这时可以尝试用“新后”与“旧后”的方式来比对它们俩是否是同一个节点。
“新后”与“旧后”的意思是使用“新后”这个节点和“旧后”这个节点对比，对比它们俩是不是同一个节点。如果是同一个节点，就将这两个节点进行对比并更新视图，如图 7-19 所示。
图 7-19 会试对比“新后”与“旧后”这两个节点是否是同一个节点
由于“新后“与“旧后”这两个节点的位置相同，所以只需要执行更新节点的操作即可，不需要执行移动节点的操作。

如果对比之后发现“新后”和“旧后”也不是同一个节点，则继续尝试对比“新后”与“旧前”是否是同一个节点。 3. 新后与旧前
“新后”与“旧前”的意思是使用“新后”这个节点与“旧前”这个节点进行对比，通过对比来分辨它们俩是不是同一个节点。如果是同一个节点，就对比它们俩并更新视图，如图 7-20 所示。
图 7-20 尝试对比“新后”与“旧前”这两个节点是否是同一个节点

如果“新后”与“旧前”是同一个节点，那么由于它们的位置不同，所以除了更新节点外，还需要执行移动节点的操作，如图 7-21 所示。
图 7-21 移动节点操作
从图 7-21 中可以看出，当“新后”与“旧前”是同一个节点时，在真实 DOM 中除了做更新操作外，还需要将节点移动到 oldChildren 中所有未处理节点的最后面。
你可能对为什么移动到 oldChildren 中所有未处理节点的最后面感到困惑，接下来我们会详细介绍为什么移动到这个位置。
更新节点是以新虚拟节点为基准，子节点也不例外，所以在图 7-21 中，因为“新后”这个节点是最后一个节点，所以真实 DOM 中将节点移动到最后不难理解，让我们感到困惑的是为什么移动到 oldchildren 中所有未处理节点的最后面。

这里我们举个例子，如图 7-22 所示。
移动到所有来处理节点的最后面
图 7-22 移动到所有未处理节点的最后面
如图 7-22 所示，当真实 DOM 子节点左右两侧已经有节点被更新，只有中间这部分节点未处理时，“新后”这个节点是未处理节点中的最后一个节点，所以真实 DOM 节点移动位置时，需要移动到 oldchildren 中所有未处理节点的最后面。只有移动到未处理节点的最后面，它的位置才与“新后”这个节点的位置相同。
如果对比之后发现这两个节点也不是同一个节点，则继续尝试对比“新前”与“旧后”是否是同一个节点。 4. 新前与旧后
“新前”与“旧后”的意思是使用“新前”与“旧后”这两个节点进行对比，对比它们是否是同一个节点，如果是同一个节点，则进行更新节点的操作，如图 7-23 所示。

图 7-23 尝试对比“新前”与“旧后”这两个节点是否是同一个节点

由于“新前”与“旧后”这两个节点的位置不同，所以除了更新节点的操作外，还需要进行移动节点的操作，如图 7-24 所示。
图 7-24 移动节点操作
从图 7-24 中可以看出，当“新前”与“旧后”是同一个节点时，在真实 DOM 中除了做更新操作外，还需要将节点移动到 oldChildren 中所有未处理节点的最前面。
将节点移动到 oldChildren 中所有未处理节点的最前面的原因，与前面介绍的“新后”与“旧前”的逻辑是一样的，如图 7-25 所示。
图 7-25 移动到所有未处理节点的最前面
如图 7-25 所示，当真实的 DOM 节点中已经有节点被更新，并且更新到第二个节点时，我们发现 oldchidren 中对应的节点在第三个的位置上，这时需要将“旧后”这个节点更新并移动到第二个的位置上，所以只需要将节点移动到所有未处理节点的最前面，就能实现移动到第二个位置的目的

也就是说，已更新过的节点都不用管。因为更新过的节点无论是节点的内容或者节点的位置，都是正确的，更新完后面就不需要再进行更改了。所以，我们只需要在所有未更新的节点区间内进行移动和更新操作即可。

如果前面这 4 种方式对比之后都没找到相同的节点，这时再通过循环的方式去 oldChildren 中详细找一圈，看看能否找到。
大部分情况下，通过前面这 4 种方式就可以找到相同的节点，所以节省了很多次循环操作。

### 7.5.3 哪些节点是未处理过的

你可能会发现，所有的对比都是针对未处理的节点的，已处理过的节点忽略不计。那么，怎么分辨哪些节点是处理过的，哪些节点是未处理过的呢？
这个问题就要从循环说起了，因为我们的逻辑都是在循环体内处理的，所以只要让循环保证只有未处理过的节点才能进入循环体内，就能达到忽略已处理过的节点从而只对未处理节点进行对比和更新等操作。
事实上，这个功能不难实现，随便一个正常的循环都能实现这个效果，从前往后循环，循环一个处理一个，能被循环到的都是未处理过的节点，处理到最后所有的节点都处理过了。
但由于前面我们的优化策略，节点是有可能会从后面对比的，对比成功就会进行更新处理，也就是说，我们的循环体内的逻辑由于优化策略，不再是只处理所有未处理过的节点的第一个，而是有可能会处理最后一个，这种情况下就不能从前向后循环，而应该是从两边向中间循环

那么，怎样实现从两边向中间循环呢？
首先，我们先准备 4 个变量：oldstartIdx、oldEndIdx、newStartIdx 和 newEndIdx。

这 4 个变量分别表示 oldChildren 的开始位置的下标（oldstartIdx）和结束位置的下标 oldEndIdx）,以及 newChildren 的开始位置的下标（newstartIdx）和结束位置的下标 newEndIdx）。
在循环体内，每处理一个节点，就将下标向指定的方向移动一个位置，通常情况下是对新旧两个节点进行更新操作，就相当于一次性处理两个节点，将新旧两个节点的下标都向指定方向移移动一个位置。

开始位置所表示的节点被处理后，就向后移动一个位置；结束位置的节点被处理后，则向前移动一个位置。

也就是说，oldstartldx 和 newstartldx 只能向后移动，而 oldEndIdx 和 newEndIdx 只能向前移动。

当开始位置大于等于结束位置时，说明所有节点都遍历过了，则结束循环：

```js
while (oldstartIdx <= oldEndIdx && newstartIdx <= newEndIdx) {
  // 做点什么
}
```

通过上面的循环条件，就可以保证循环体内的节点都是未处理的。
你可能会发现，这个循环条件是无论 newChildren 或者 oldChildren,只要它们两个中有一个循环完毕，就会退出循环。那么，当新子节点和旧子节点的节点数量不一致时，会导致循环结束后仍然有未处理的节点，也就是说这个循环将无法覆盖所有节点。

确实是无法覆盖所有节点，但正是因为这样，才会少循环几次，提升一些性能。你可能会觉得惊讶，为什么？
因为循环的目的是找出差异，针对差异来做对应的操作，但现在直接就可以判断出差异，所以就不需要再循环对比差异了。

你可能更惊讶了，为什么？
因为如果是 oldChildren 先循环完毕，这个时候如果 newChildren 中还有剩余的节点，那么说明什么问题？说明这些节点都是需要新增的节点，直接把这些节点插入到 DOM 中就行了，不需要循环比对了。

如果是 newChildren 先循环完毕，这时如果 oldchildren 还有剩余的节点，又说明了什么问题？这说明 oldChildren 中剩余的节点都是被废弃的节点，是应该被删除的节点。这时不需要循环对比就可以知道需要将这些节点从 DOM 中移除。

找到 newChildren 中所有剩余的节点并不难，由于 oldChildren 先被循环完，所以此时 newStartIdx 肯定是小于 newEndIdx 的，那么在 newChildren 中，下标在 newstartIdx 和 newEndIdx 之间的所有节点都是未处理的节点。

同理，找到 oldchildren 中所有剩余的节点也很简单。由于 newChildren 先被循环完，所以 oldstartIdx 小于 oldEndIdx,那么在 oldChildren 中，下标在 oldstartIdx 和 oldEndId 之间的所有节点都是未处理的节点。

### 7.5.4 小结

本节重点讨论了更新子节点的详细过程以及处理逻辑。
在本节中，我们学习了更新子节点可以分为 4 种操作，分别是：新增子节点、更新子节点、移动子节点和删除子节点。
在新增子节点中，我们详细讨论了什么情况下需要创建子节点，以及把创建的子节点插入到什么位置。

接下来，我们又讨论了更新子节点的过程。如果在 oldChildren 中可以找到与新子节点相同的节点，就需要更新它们。

如果在 oldchildren 中找到的节点的位置和新子节点的位置不一样，需要将 DOM 中的节点移动到新子节点所在的位置。

删除节点的操作发生在循环结束后。当循环结束后，oldChildren 中所有未处理的节点都是需要被删除的节点。

随后我们还讨论了优化策略，通过优化策略可以避免很多循环操作。

最后，我们讨论了怎么分辨哪些子节点是未处理过的节点。

图 7-26 给出了更新子节点的整体流程。

在图 7-26 中，有些名词前面并没有提到过，这里给出解释。

- oldstartVnode:oldChildren 中所有未处理的第一个节点，与前文中提到的“旧前”是同一个节点。
- oldEndVnode:oldChildren 中所有未处理的最后一个节点，与前文中提到的“旧后”是同一个节点。
- newstartmode:newchidren 中所有未处理的第一个节点，与前文中提到的“新前”是同一个节点。
- newEndvnode:neqchildren 中所有未处理的最后一个节点，与前文中提到的“新后”是同一个节点。

在图 7-26 中，我们看到在循环的一开始先判断 oldstartvnode 和 oldEndVnode 是否存在如果不存在，则直接跳，本次循环，进行下一轮循环（也就是说，如果这个节点不存在，则直接跳过这个节点，处理下一个节点）。

之所以有这么一个判断，主要是为了处理旧节点已经被移动到其他位置的情况。移动节点日真正移动的是真实 DOM 节点。移动真实 DOM 节点后，为了防止后续重复处理同一个节点，旧的虚拟子节点就会被设置为 undefined,用来标记这个节点已经被处理并且移动到其他位置。

在图 7-26 中，有一部分逻辑是建立 key 与 index 索引的对应关系。这部分内容前面并没有提到。在 Vuejs 的模板中，渲染列表时可以为节点设置一个属性 key,这个属性可以标示一个点的唯一 ID.Vuejs 官方非常推荐在渲染列表时使用这个属性，我也非常推荐使用它，为什么呢？

前面提到过，在更新子节点时，需要在 oldChildren 中循环去找一个节点。但是如果我们在模板中谊染列表时，为子节点设置了属性 key,那么在图 7-26 中建立 key 与 index 索引的对应关系时，就生成了一个 key 对应着一个节点下标这样一个对象。也就是说，如果在节点上了属性 key,那么在 oldChildren 中找相同节点时，可以直接通过 key 拿到下标，从而获取节点。这样，我们根本不需要通过循环来查找节点。

## 7.6 总结

本章中，我们介绍了虚拟 DOM 中最关键的部分：patch。
通过 patch 可以对比新旧两个虚拟 DOM,从而只针对发生了变化的节点进行更新视图的操作。本章详细介绍了如何对比新旧两个节点以及更新视图的过程。
在本章开始，我们主要讨论了在什么情况下创建新节点，将新节点插入到什么位置。还了在什么情况下删除节点，删除哪个节点，以及在什么情况下修改节点，修改哪个节点等问题。

随后，我们介绍了从虚拟节点创建真实节点并渲染到视图的详细过程。
接下来，我们又介绍了一个元素是怎样从视图中删除的。
然后，详细介绍了更新节点的详细过程。
最后，详细讨论了更新子节点的过程，其中包括创建新增的子节点、删除废弃的子节点、新发生变化的子节点以及移动位置发生了变化的子节点等。

# 第三篇 模板编译原理

在 Vue.js 内部，模板编译是一项比较重要的技术。我们平时使用 Vue.js 进行开发时，会经常使用模板。模板赋予我们很多强大的能力，例如可以在模板中访问变量。

但在 Vue.js 中创建 HTML 并不是只有模板这一种途径，我们既可以手动写渲染函数来创建 HTML,也可以在 Vue.js 中使用 JSX 来创建 HTML。

渲染函数是创建 HTML 最原始的方法。模板最终会通过编译转换成渲染函数，渲染函数执行后，会得到一份 vnode 用于虚拟 DOM 渲染。所以模板编译其实是配合虚拟 DOM 进行渲染，这也是本书先介绍虚拟 DOM 后介绍模板编译的原因。

本篇中，我们将会详细介绍模板转换成渲染函数的详细过程。

# 第 8 章 模板编译

8.1 概念
8.2 将模板编译成渲染函数
8.2.1 解析器
8.2.2 优化器
8.2.3 代码生成器
8.3 总结

# 第 9 章 解析器

9.1 解析器的作用
9.2 解析器内部运行原理
9.3 HTML 解析器
9.3.1 运行原理
9.3.2 截取开始标签
9.3.3 截取结束标签
9.3.4 截取注释
9.3.5 截取条件注释
9.3.6 截取 DOCTYPE
9.3.7 截取文本
9.3.8 纯文本内容元素的处理
9.3.9 使用栈维护 DOM 层级
9.3.10 整体逻辑
9.4 文本解析器
9.5 总结

# 第 10 章 优化器

10.1 找出所有静态节点并标记
10.2 找出所有静态根节点并标记
10.3 总结

# 第 11 章 代码生成器

11.1 通过 AST 生成代码字符串
11.2 代码生成器的原理
11.2.1 元素节点
11.2.2 文本节点
11.2.3 注释节点
11.3 总结

# 第四篇 整体流程

前几篇介绍的是 Vue.js 在实现一些功能时所要用到的技术，其内容偏底层。

在本篇中，我们更多的是介绍距离用户比较近的内容，例如使用 Vue.js 开发项目时常用的 P1、模板中的各种指令、组件里经常使用的生命周期钩子以及使用事件进行父子组件间的通信。此外，我们还会定义一些 Vue.js 插件和过滤器。

本篇中，我们主要讲解常用功能的内部原理，同时还会介绍 Vue.js 的架构设计和代码结构，也会讨论如何组建 Vue.js 这样的开源项目的代码等内容。

在开发一些很复杂的功能时，在某些特定的场景下，本篇所介绍的内容一定会对我们有帮助。

如果熟悉所使用功能的内部实现，那么当业务功能出现 bug 时，我们就可以快速、精准地定位问题所在，知道问题是由 Vue.js 的某些特性导致的，还是代码逻辑有问题，并且在开发复杂功能时，我们可以清楚地知道 Vue.js 能提供的能力的边界在哪里，这样就可以最大限度地发挥它的价值。

# 第 12 章 架构设计与项目结构

12.1 目录结构
12.2 架构设计
12.3 总结

# 第 13 章 实例方法与全局 API 的实现原理

13.1 数据相关的实例方法
13.2 事件相关的实例方法
13.2.1 vm.$on
13.2.2 vm.$off
13.2.3 vm.$once
13.2.4 vm.$emit
13.3 生命周期相关的实例方法
13.3.1 vm.$forceUpdate
13.3.2 vm.$destroy
13.3.3 vm.$nextTick
13.3.4 vm.$mount
13.4 全局 API 的实现原理
13.4.1 Vue.extend
13.4.2 Vue.nextTick
13.4.3 Vue.set
13.4.4 Vue.delete
13.4.5 Vue.directive
13.4.6 Vue.filter
13.4.7 Vue.component
13.4.8 Vue.use
13.4.9 Vue.mixin
13.4.10 Vue.compile
13.4.11 Vue.version
13.5 总结

# 第 14 章 生命周期

14.1 生命周期图示
14.1.1 初始化阶段
14.1.2 模板编译阶段
14.1.3 挂载阶段
14.1.4 卸载阶段
14.1.5 小结
14.2 从源码角度了解生命周期
14.3 errorCaptured 与错误处理
14.4 初始化实例属性
14.5 初始化事件
14.6 初始化 inject
14.6.1 provide/inject 的使用方式
14.6.2 inject 的内部原理
14.7 初始化状态
14.7.1 初始化 props
14.7.2 初始化 methods
14.7.3 初始化 data
14.7.4 初始化 computed
14.7.5 初始化 watch
14.8 初始化 provide
14.9 总结

# 第 15 章 指令的奥秘

15.1 指令原理概述
15.1.1 v-if 指令的原理概述
15.1.2 v-for 指令的原理概述
15.1.3 v-on 指令
15.2 自定义指令的内部原理
15.3 虚拟 DOM 钩子函数
15.4 总结

# 第 16 章 过滤器的奥秘

16.1 过滤器原理概述
16.1.1 串联过滤器
16.1.2 滤器接收参数
16.1.3 resolveFilter 的内部原理
16.2 解析过滤器
16.3 总结

# 第 17 章 最佳实践

17.1 为列表渲染设置属性 key
17.2 在 v-if/v-if-else/v-else 中使用 key
17.3 路由切换组件不变
17.3.1 路由导航守卫 beforeRouteUpdate
17.3.2 观察 \$route 对象的变化
17.3.3 为 router-view 组件添加属性 key
17.4 为所有路由统一添加 query
17.4.1 使用全局守卫 beforeEach
17.4.2 使用函数劫持
17.5 区分 Vuex 与 props 的使用边界
17.6 避免 v-if 和 v-for 一起使用
17.7 为组件样式设置作用域
17.8 避免在 scoped 中使用元素选择器
17.9 避免隐性的父子组件通信
17.10 单文件组件如何命名
17.10.1 单文件组件的文件名的大小写
17.10.2 基础组件名
17.10.3 单例组件名
17.10.4 紧密耦合的组件名
17.10.5 组件名中的单词顺序
17.10.6 完整单词的组件名
17.10.7 组件名为多个单词
17.10.8 模板中的组件名大小写
17.10.9 JS/JSX 中的组件名大小写
17.11 自闭合组件
17.12 prop 名的大小写
17.13 多个特性的元素
17.14 模板中简单的表达式
17.15 简单的计算属性
17.16 指令缩写
17.17 良好的代码顺序
17.17.1 组件/实例的选项的顺序
17.17.2 元素特性的顺序
17.17.3 单文件组件顶级元素的顺序
17.18 总结
