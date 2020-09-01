> 深入浅出 Vue.js  
> 作者: 刘博文  
> 2019 年 3 月第 1 版  
> [图灵社区](https://www.ituring.com.cn/book/2675)

# 第 1 章 Vue.js 简介

1.1 什么是 Vue.js
1.2 Vue.js 简史

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

其实这个问题还是比较简单的。学过 JavaScript 的人都知道，有两种方法可以侦测到变化：使用 `Object.defineProperty` 和 ES6 的 Proxy。

由于 ES6 在浏览器中的支持度并不理想，到目前为止 Vue.js 还是使用 `Object.defineProperty` 来实现的，所以书中也会使用它来介绍变化侦测的原理。

由于使用 `Object.defineProperty` 来侦测变化会有很多缺陷，所以 Vue.js 的作者尤雨溪说日后会使用 Proxy 重写这部分代码。好在本章讲的是原理和思想，所以即便以后用 Proxy 重写了这部分代码，书中介绍的原理也不会变。

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

当 value 身上被标记了 `__ob__` 之后，就可以通过 value.`__ob__` 来访问 Observer 实例。如果是 Array 拦截器，因为拦截器是原型方法，所以可以直接通过 this.`__ob__` 来访问 Observer 实例。例如：

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

在上面的代码中，我们在 mutator 函数里通过 this.`__ob__` 来获取 Observer 实例。

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

在上面的代码中，我们从 this.`__ob__` 上拿到 Observer 实例后，如果有新增元素，则使用 ob.observeArray 来侦测这些新增元素的变化。

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

为了不污染全局 Array.prototype，我们在 Observer 中只针对那些需要侦测变化的数组使用 `__proto__` 来覆盖原型方法，但 `__proto__` 在 ES6 之前并不是标准属性，不是所有浏览器都支持它。因此，针对不支持 `__proto__` 属性的浏览器，我们直接循环拦截器，把拦截器中的方法直接设置到数组身上来拦截 Array.prototype 上的原生方法。

Array 收集依赖的方式和 Object 一样，都是在 getter 中收集。但是由于使用依赖的位置不同，数组要在拦截器中向依赖发消息，所以依赖不能像 Object 那样保存在 defineReactive 中，而是把依赖保存在了 Observer 实例上。

在 Observer 中，我们对每个侦测了变化的数据都标上印记 `__ob__`，并把 this（Observer 实例）保存在 `__ob__` 上。这主要有两个作用，一方面是为了标记数据是否被侦测了变化（保证同一个数据只被侦测一次），另一方面可以很方便地通过数据取到 `__ob__`，从而拿到 Observer 实例上保存的依赖。当拦截到数组发生变化时，向依赖发送通知。

除了侦测数组自身的变化外，数组中元素发生的变化也要侦测。我们在 Observer 中判断如果当前被侦测的数据是数组，则调用 observeArray 方法将数组中的每一个元素都转换成响应式的并侦测变化。

除了侦测已有数据外，当用户使用 push 等方法向数组中新增数据时，新增的数据也要进行变化侦测。我们使用当前操作数组的方法来进行判断，如果是 push、unshift 和 splice 方法，则从参数中将新增数据提取出来，然后使用 observeArray 对新增数据进行变化侦测。

由于在 ES6 之前，JavaScript 并没有提供元编程的能力，所以对于数组类型的数据，一些语法无法追踪到变化，只能拦截原型上的方法，而无法拦截数组特有的语法，例如使用 length 清空数组的操作就无法拦截。

# 第 4 章 变化侦测相关的 API 实现原理

4.1 vm.\$watch
4.1.1 用法
4.1.2 watch的内部原理
4.1.3 deep参数的实现原理
4.2 vm.\$set
4.2.1 用法
4.2.2 Array 的处理
4.2.3 key 已经存在于 target 中
4.2.4 处理新增的属性
4.3 vm.\$delete
4.3.1 用法
4.3.2 实现原理
4.4 总结

# 第二篇 虚拟 DOM

Vue.js2.0 引入了虚拟 DOM,比 Vue.js1.0 的初始渲染速度提升了 2-4 倍，并大大降低了内存消耗。

虚拟 DOM 也是 React 核心技术之一。它到底有着怎样的魔力，使前端界各大主流框架都纷份使用？

你是否好奇，虚拟 DOM 的原理是什么？

你是否好奇，为什么 Vue.js2.0 开始引入了虚拟 DOM?

你是否好奇，为什么 Vue.js 引入虚拟 DOM 后渲染速度就变快了？

又或者，你根本没听说过虚拟 DOM,那么什么是虚拟 DOM?

这一切的问题，都将在本篇揭晓。

# 第 5 章 虚拟 DOM 简介

5.1 什么是虚拟 DOM
5.2 为什么要引入虚拟 DOM
5.3 Vue.js 中的虚拟 DOM
5.4 总结

# 第 6 章 VNode

6.1 什么是 VNode
6.2 VNode 的作用
6.3 VNode 的类型
6.3.1 注释节点
6.3.2 文本节点
6.3.3 克隆节点
6.3.4 元素节点
6.3.5 组件节点
6.3.6 函数式组件
6.4 总结

# 第 7 章 patch

7.1 patch 介绍
7.1.1 新增节点
7.1.2 删除节点
7.1.3 更新节点
7.1.4 小结
7.2 创建节点
7.3 删除节点
7.4 更新节点
7.4.1 静态节点
7.4.2 新虚拟节点有文本属性
7.4.3 新虚拟节点无文本属性
7.4.4 小结
7.5 更新子节点
7.5.1 更新策略
7.5.2 优化策略
7.5.3 哪些节点是未处理过的
7.5.4 小结
7.6 总结

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
