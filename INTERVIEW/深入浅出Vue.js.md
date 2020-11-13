[从源码解读 - Vue常考面试题](https://mp.weixin.qq.com/s/5YR2pgxgB5K-_B6QpN0uSw)
[30 道 Vue 面试题，内含详细讲解（涵盖入门到精通，自测 Vue 掌握程度）](https://juejin.im/post/6844903918753808398)

# Vue

## 基础点

### 单页面 SPA

说说对 SPA 单⻚⾯的理解，它的优缺点分别是什么？

SPA（ single-page application ）仅在 Web ⻚⾯初始化时加载相应的 HTML、JavaScript 和 CSS。⼀旦⻚⾯加载完成，SPA 不会因为⽤户的操作⽽进⾏⻚⾯的重新加载或跳转；取⽽代之的是利⽤路由机制实现 HTML 内容的变换，UI 与⽤户的交互，避免⻚⾯的重新加载。

- 优点：

  1. ⽤户体验好、快，内容的改变不需要重新加载整个⻚⾯，避免了不必要的跳转和重复渲染；
  2. 基于上面一点，SPA 相对对服务器压⼒⼩；
  3. 前后端职责分离，架构清晰，前端进⾏交互逻辑，后端负责数据处理；

- 缺点：
  1. 初次加载耗时多：为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
  2. 前进后退路由管理：由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理；
  3. SEO 难度较大：由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势。

### Vue 初始化

new Vue() 发生了什么？

结论：new Vue()是创建 Vue 实例，它内部执行了根实例的初始化过程。

具体包括以下操作：

- 选项合并
- $children，$refs，$slots，$createElement 等实例属性的方法初始化
- 自定义事件处理
- 数据响应式处理
- 生命周期钩子调用 （beforecreate created）
- 可能的挂载

总结：new Vue()创建了根实例并准备好数据和方法，未来执行挂载时，此过程还会递归的应用于它的子组件上，最终形成一个有紧密关系的组件实例树。

源码地址：src/core/instance/init.js

### Vue.use 是干什么的？原理是什么？

vue.use 是用来使用插件的，我们可以在插件中扩展全局组件、指令、原型方法等。

过程

1. 检查插件是否注册，若已注册，则直接跳出；
2. 处理入参，将第一个参数之后的参数归集，并在首部塞入 this 上下文；
3. 执行注册方法，调用定义好的 install 方法，传入处理的参数，若没有 install 方法并且插件本身为 function 则直接进行注册；

应用

1. 插件不能重复的加载。install 方法的第一个参数是 vue 的构造函数，其他参数是 Vue.set 中除了第一个参数的其他参数； 代码：`args.unshift(this)`
2. 调用插件的 install 方法 代码：`typeof plugin.install === 'function'`
3. 插件本身是一个函数，直接让函数执行。 代码：`plugin.apply(null, args)`
4. 缓存插件。 代码：`installedPlugins.push(plugin)`

源码地址：src/core/global-api/use.js

### 响应式数据

请说一下响应式数据的理解？

根据数据类型来做不同处理，数组和对象类型当值变化时如何劫持。

1. 对象内部通过 defineReactive 方法，使用 Object.defineProperty() 监听数据属性的 get 来进行数据依赖收集，再通过 set 来完成数据更新的派发；

2. 数组则通过重写数组方法来实现的。扩展它的 7 个变更⽅法，通过监听这些方法可以做到依赖收集和派发更新；( push/pop/shift/unshift/splice/reverse/sort )

这里在回答时可以带出一些相关知识点 （比如多层对象是通过递归来实现劫持，顺带提出 vue3 中是使用 proxy 来实现响应式数据）

补充回答：
内部依赖收集是怎么做到的，每个属性都拥有自己的 dep 属性，存放他所依赖的 watcher，当属性变化后会通知自己对应的 watcher 去更新。

响应式流程：

1. defineReactive 把数据定义成响应式的；
2. 给属性增加一个 dep，用来收集对应的那些 watcher；
3. 等数据变化进行更新

```js
dep.depend(); // get 取值：进行依赖收集
dep.notify(); // set 设置时：通知视图更新
```

这里可以引出性能优化相关的内容：1)对象层级过深，性能就会差。2)不需要响应数据的内容不要放在 data 中。3)object.freeze() 可以冻结数据。

源码地址：src/core/observer/index.js 158

### 数组检测

Vue 如何检测数组变化？

数组考虑性能原因没有用 defineProperty 对数组的每一项进行拦截，而是选择重写数组 方法以进行重写。当数组调用到这 7 个方法的时候，执行 ob.dep.notify() 进行派发通知 Watcher 更新；

- 重写数组方法：push/pop/shift/unshift/splice/reverse/sort

补充回答：
在 Vue 中修改数组的索引和长度是无法监控到的。需要通过以下 7 种变异方法修改数组才会触发数组对应的 wacther 进行更新。数组中如果是对象数据类型也会进行递归劫持。
说明：那如果想要改索引更新数据怎么办？
可以通过 Vue.set()来进行处理 =》 核心内部用的是 splice 方法。

```js
// 取出原型方法；
const arrayProto = Array.prototype
// 拷贝原型方法；
export const arrayMethods = Object.create(arrayProto)
// 重写数组方法；
def(arrayMethods, method, function mutator (...args) { }

ob.dep.notify()  // 调用方法时更新视图；
```

源码地址：src/core/observer/array.js 15

### Vue set 方式实现

Vue.set 方法是如何实现的？

我们给对象和数组本身都增加了 dep 属性，当给对象新增不存在的属性则触发对象依赖的 watcher 去更新，当修改数组索引时我们调用数组本身的 splice 方法去更新数组。

补充回答：
官方定义 `Vue.set(object, key, value)`

1. 如果是数组，调用重写的 splice 方法 （这样可以更新视图 ） 代码：`target.splice(key, 1, val)`
2. 如果不是响应式的也不需要将其定义成响应式属性。
3. 如果是对象，将属性定义成响应式的 `defineReactive(ob.value, key, val)`，通知视图更新 `ob.dep.notify()`

源码地址：src/core/observer/index.js 202

### Vue 模板编译原理

Vue 中模板编译原理？

如何将 template 转换成 render 函数（这里要注意的是我们在开发时尽量不要使用 template，因为将 template 转化成 render 方法需要在运行时进行编译操作会有性能损耗，同时引用带有 complier 包的 vue 体积也会变大） 默认.vue 文件中的 template 处理是通过 vue-loader 来进行处理的并不是通过运行时的编译。

1. 将 template 模板转换成 ast 语法树 - parserHTML
2. 对静态语法做静态标记 - markUp
3. 重新生成代码 - codeGen

补充回答：
模板引擎的实现原理就是 new Function + with 来进行实现的。
vue-loader 中处理 template 属性主要靠的是 vue-template-compiler
vue-loader

```js
// template => ast => codegen => with+function 实现生成render方法
let { ast, render } = VueTemplateCompiler.compile(`<div>{{aaa}}</div>`);
console.log(ast, render);

// 模板引擎的实现原理 with + new Function
console.log(new Function(render).tostring());
// render方法执行完毕后生成的是虚拟 dom
// with(this){return _c('div',[_s(aaa)])}
// 代码生成
```

源码设置：

```js
const ast = parse(template.trim(), options); // 将代码解析成ast语法树
if (options.optimize !== false) {
  optimize(ast, options); // 优化代码 标记静态点 标记树
}
const code = generate(ast, options); // 生成代码
```

源码地址：src/compiler/index.js

### 响应式方法

Proxy 与 Object.defineProperty 优劣对比

Proxy 的优势如下:

1. 可以直接监听对象而非属性；
2. 可以直接监听数组的变化；
3. 有多达 13 种拦截方法,不限于 apply、ownKeys、deleteProperty、has 等等是 Object.defineProperty 不具备的；
4. 返回的是一个新对象,我们可以只操作新的对象达到目的,而 Object.defineProperty 只能遍历对象属性直接修改；
5. 作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利；

Object.defineProperty 的优势如下:
兼容性好，支持 IE9，而 Proxy 的存在浏览器兼容性问题，而且无法用 polyfill 磨平，因此 Vue 的作者才声明需要等到下个大版本( 3.0 )才能用 Proxy 重写。

### Vue3.x 响应式数据原理

Vue3.x 改用 Proxy 替代 Object.defineProperty。因为 Proxy 可以直接监听对象和数组的变化，并且有多达 13 种拦截方法。并且作为新标准将受到浏览器厂商重点持续的性能优化。

Proxy 只会代理对象的第一层，那么 Vue3 又是怎样处理这个问题的呢？
判断当前 Reflect.get 的返回值是否为 Object，如果是则再通过 reactive 方法做代理， 这样就实现了深度观测。

监测数组的时候可能触发多次 get/set，那么如何防止触发多次呢？
我们可以判断 key 是否为当前被代理对象 target 自身属性，也可以判断旧值与新值是否相等，只有满足以上两个条件之一时，才有可能执行 trigger。

## 生命周期

### Vue 声明周期方法

Vue 的生命周期方法有哪些？一般在哪一步发起请求及原因

总共分为 8 个阶段：创建前/后，载入前/后，更新前/后，销毁前/后。

1. 创建前/后：

- beforeCreate 阶段：vue 实例的挂载元素 el 和数据对象 data 都为 undefined，还未初始化。说明：在当前阶段 data、methods、computed 以及 watch 上的数据和方法都不能被访问。
- created 阶段：vue 实例的数据对象 data 有了，el 还没有。说明：可以做一些初始数据的获取，在当前阶段无法与 Dom 进行交互，如果非要想，可以通过 vm.\$nextTick 来访问 Dom。

2. 载入前/后：

- beforeMount 阶段：vue 实例的\$el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点。说明：当前阶段虚拟 Dom 已经创建完成，即将开始渲染。在此时也可以对数据进行更改，不会触发 updated。
- mounted 阶段：vue 实例挂载完成，data.message 成功渲染。说明：在当前阶段，真实的 Dom 挂载完毕，数据完成双向绑定，可以访问到 Dom 节点，使用\$refs 属性对 Dom 进行操作。

3. 更新前/后：

- beforeUpdate 阶段：响应式数据更新时调用，发生在虚拟 DOM 打补丁之前，适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。说明：可以在当前阶段进行更改数据，不会造成重渲染。
- updated 阶段：虚拟 DOM 重新渲染和打补丁之后调用，组成新的 DOM 已经更新，避免在这个钩子函数中操作数据，防止死循环。说明：当前阶段组件 Dom 已完成更新。要注意的是避免在此期间更改数据，因为这可能会导致无限循环的更新。

4. 销毁前/后：

- beforeDestroy 阶段：实例销毁前调用，实例还可以用，this 能获取到实例，常用于销毁定时器，解绑事件。说明：在当前阶段实例完全可以被使用，我们可以在这时进行善后收尾工作，比如清除计时器。
- destroyed 阶段：实例销毁后调用，调用后所有事件监听器会被移除，所有的子实例都会被销毁。说明：当前阶段组件已被拆解，数据绑定被卸除，监听被移出，子实例也统统被销毁。

补充回答：
第一次页面加载时会触发：beforeCreate, created, beforeMount, mounted。

- created 实例已经创建完成，因为它是最早触发的原因可以进行一些数据，资源的请求。(服务器渲染支持 created 方法)
- mounted 实例已经挂载完成，可以进行一些 DOM 操作。(接口请求)

源码地址：src/core/instance/lifecycle.js

### 声明周期钩子的实现

生命周期钩子是如何实现的？

Vue 的生命周期钩子就是回调函数而已，当创建组件实例的过程中会调用对应的钩子方法。

补充回答：
内部主要是使用 callHook 方法来调用对应的方法。核心是一个发布订阅模式，将钩子订阅好（内部采用数组的方式存储），在对应的阶段进行发布。

源码地址：src/core/util/options.js 146 core/instance/lifecycle.js 336

### 父组件和子组件生命周期钩子执行顺序

第一次页面加载时会触发 beforeCreate, created, beforeMount, mounted 这几个钩子。

1. 渲染过程：

父组件挂载完成一定是等子组件都挂载完成后，才算是父组件挂载完，所以父组件的 mounted 在子组件 mouted 之后

父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted

2. 子组件更新过程：

影响到父组件：父 beforeUpdate -> 子 beforeUpdate->子 updated -> 父 updated
不影响父组件：子 beforeUpdate -> 子 updated

3. 父组件更新过程：

影响到子组件：父 beforeUpdate -> 子 beforeUpdate->子 updated -> 父 updted
不影响子组件：父 beforeUpdate -> 父 updated

4. 销毁过程：

父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
重要：父组件等待子组件完成后，才会执行自己对应完成的钩子。

## 组件通信

### 组件的函数类型 data

Vue 中的组件的 data 为什么是一个函数？而 new Vue 实例里，data 可以直接是一个对象？

每次使用组件时都会对组件进行实例化操作，并且调用 data 函数返回一个对象作为组件的数据源。这样可以保证多个组件间数据互不影响。

如果 data 是对象的话，对象属于引用类型，会影响到所有的实例。所以为了保证组件不同的实例之间 data 不冲突，data 必须是一个函数。而 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题。

源码地址：src/core/util/options 121

### 组件通信方式

Vue 组件间通信有哪几种方式？

Vue 组件间通信只要指以下 3 类通信：父子组件通信、隔代组件通信、兄弟组件通信，下面我们分别介绍每种通信方式且会说明此种方法可适用于哪类组件间通信。

1. props / \$emit 适用 父子组件通信

这种方法是 Vue 组件的基础，相信大部分同学耳闻能详，所以此处就不举例展开介绍。

2. ref 与 $parent / $children 适用 父子组件通信

- ref：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用就指向组件实例
- $parent / $children：访问父 / 子实例

3. EventBus （$emit / $on） 适用于 父子、隔代、兄弟组件通信

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

4. $attrs/$listeners 适用于 隔代组件通信

- $attrs：包含了父作用域中不被 prop 所识别 (且获取) 的特性绑定 ( class 和 style 除外 )。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 ( class 和 style 除外 )，并且可以通过 v-bind="$attrs" 传入内部组件。通常配合 inheritAttrs 选项一起使用。
- $listeners：包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="$listeners" 传入内部组件

5. provide / inject 适用于 隔代组件通信

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

6. Vuex 适用于 父子、隔代、兄弟组件通信

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

- Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
- 改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

### 组件中的 name 选项

组件中写 name 选项有哪些好处及作用？

1. 可以通过名字找到对应的组件 （ 递归组件 ）
2. 可以通过 name 属性实现缓存功能 (keep-alive)
3. 可以通过 name 来识别组件 （跨级组件通信时非常重要）

```js
Vue.extend = function () {
  if (name) {
    Sub.options.componentd[name] = Sub;
  }
};
```

源码地址：src/core/vdom/create-element.js 111

### keep-alive 原理

keep-alive 平时在哪里使用？原理是什么？

keep-alive 主要是组件缓存，采用的是 LRU 算法。最近最久未使用法。
常用的两个属性 include/exclude，允许组件有条件的进行缓存。
两个生命周期 activated/deactivated，用来得知当前组件是否处于活跃状态。

```js
abstract: true, // 抽象组件
props:{
    include: patternTypes,  // 要缓存的有哪些
    exclude: patternTypes, // 要排除的有哪些
    max: [String, Number] //最大缓存数量
}
if(cache[key]) { // 通过key 找到缓存，获取实例
    vnode.componentInstance = cache[key].componentInstance
    remove(keys, key) //将key删除掉
    keys.push(key) // 放到末尾
} else {
    cache[key] = vnode // 没有缓存过
    keys.push(key) //存储key
    if(this.max && keys.length > parseInt(this.max)) { // 如果超过最大缓存数
    // 删除最早缓存的
    pruneCacheEntry(cache, keys[0], keys, this._vnode)
}
}
vnode.data.keepAlive = true // 标记走了缓存
```

### Vue.mixin

Vue.mixin 的使用场景和原理？

Vue.mixin 的作用就是抽离公共的业务逻辑，原理类似“对象的继承”，当组件初始化时会调用 mergeOptions 方法进行合并，采用策略模式针对不同的属性进行合并，如果混入的数据和本身组件中的数据冲突，会采用“就近原则”以组件的数据为准。

补充回答：
mixin 中有很多缺陷“命名冲突问题”，“依赖问题”，“数据来源问题”，这里强调一下 mixin 的数据是不会被共享的。

源码地址：src/core/util/options.js

## 路由

### 路由钩子函数

Vue-router 有几种钩子函数？具体是什么及执行流程是怎样的？

路由钩子的执行流程，钩子函数种类有：全局守卫、路由守卫、组件守卫。

完整的导航解析流程

1. 导航被触发；
2. 在失活的组件里调用 beforeRouteLeave 守卫；
3. 调用全局 beforeEach 守卫；
4. 在复用组件里调用 beforeRouteUpdate 守卫；
5. 调用路由配置里的 beforeEnter 守卫；
6. 解析异步路由组件；
7. 在被激活的组件里调用 beforeRouteEnter 守卫；
8. 调用全局 beforeResolve 守卫；
9. 导航被确认；
10. 调用全局的 afterEach 钩子；
11. DOM 更新；
12. 用创建好的实例调用 beforeRouteEnter 守卫中传给 next 的回调函数。

### vue-router 模式

vue-router 路由模式有几种？

vue-router 有 3 种路由模式：hash、history、abstract。

1. hash 模式：hash + hashChange

特点：hash 虽然在 URL 中，但不被包括在 HTTP 请求中；用来指导浏览器动作，对服务端安全无用，hash 不会重加载页面。通过监听 hash（#）的变化来执行 js 代码 从而实现 页面的改变。

核心代码：

```js
window.addEventListener(‘hashchange‘,function(){
    self.urlChange()
})
```

2. history 模式：historyApi + popState

HTML5 推出的 history API，由 pushState()记录操作历史，监听 popstate 事件来监听到状态变更；
因为 只要刷新 这个 url（www.ff.ff/jjkj/fdfd/fdf/fd）就会请求服务器，然而服务器上根本没有这个资源，所以就会报404，解决方案就 配置一下服务器端。

说明：

1. hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器；
2. history : 依赖 HTML5 History API 和服务器配置。具体可以查看 HTML5 History 模式；
3. abstract : 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式.

## 属性作用与对比

### nextTick 原理

nextTick 在哪里使用？原理是？

nextTick 的回调是在下次 DOM 更新循环结束之后执行的延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。nextTick 主要使用了宏任务和微任务。原理就是异步方法(promise, mutationObserver, setImmediate, setTimeout)经常与事件循环一起来问。

补充回答：
vue 多次更新数据，最终会进行批处理更新。内部调用的就是 nextTick 实现了延迟更新，用户自定义的 nextTick 中的回调会被延迟到更新完成后调用，从而可以获取更新后的 DOM。
源码地址：src/core/util/next-tick.js 42

### 虚拟 DOM 的优势和劣势

Vue 为什么需要虚拟 DOM？虚拟 DOM 的优劣如何？

Virtual DOM 就是用 js 对象来描述真实 DOM，是对真实 DOM 的抽象，由于直接操作 DOM 性能低但是 js 层的操作效率高，可以将 DOM 操作转化成对象操作，最终通过 diff 算法比对差异进行更新 DOM （减少了对真实 DOM 的操作）。虚拟 DOM 不依赖真实平台环境从而也可以实现跨平台。

优点：

1. 保证性能下限： 框架的虚拟 DOM 需要适配任何上层 API 可能产生的操作，它的一些 DOM 操作的实现必须是普适的，所以它的性能并不是最优的；但是比起粗暴的 DOM 操作性能要好很多，因此框架的虚拟 DOM 至少可以保证在你不需要手动优化的情况下，依然可以提供还不错的性能，即保证性能的下限；
2. 无需手动操作 DOM： 我们不再需要手动去操作 DOM，只需要写好 View-Model 的代码逻辑，框架会根据虚拟 DOM 和 数据双向绑定，帮我们以可预期的方式更新视图，极大提高我们的开发效率；
3. 跨平台： 虚拟 DOM 本质上是 JavaScript 对象,而 DOM 与平台强相关，相比之下虚拟 DOM 可以进行更方便地跨平台操作，例如服务器渲染、weex 开发等等。

缺点:

1. 无法进行极致优化： 虽然虚拟 DOM + 合理的优化，足以应对绝大部分应用的性能需求，但在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化。

补充回答：
虚拟 DOM 的实现就是普通对象包含 tag、data、children 等属性对真实节点的描述。（本质上就是在 JS 和 DOM 之间的一个缓存）
Vue2 的 Virtual DOM 借鉴了开源库 snabbdom 的实现。
VirtualDOM 映射到真实 DOM 要经历 VNode 的 create、diff、patch 等阶段。

源码地址：src/core/vdom/vnode: 3

### Vue 中 key 的作用

Vue 中 key 的作用和工作原理，说说你对它的理解

key 的作用主要是为了高效的更新虚拟 DOM，其原理是 vue 在 patch 过程中通过 key 可以精准判断两个节点是否是同一个，从而避免频繁更新不同元素，使得整个 patch 过程更加高效，减少 DOM 操作量，提高性能。

补充回答：

1. 若不设置 key 还可能在列表更新时引发一些隐蔽的 bug
2. vue 中在使用相同标签名元素的过渡切换时，也会使用到 key 属性，其目的也是为了让 vue 可以区分它们，否则 vue 只会替换其内部属性而不会触发过渡效果。

源码地址：src\core\vdom\patch.js - updateChildren

### Vue 中的 diff 原理

vue 的 diff 算法是平级比较，不考虑跨级比较的情况。内部采用深度递归的方式 + 双指针的方式进行比较。

补充回答：

1. 先比较是否是相同节点
2. 相同节点比较属性，并复用老节点
3. 比较儿子节点，考虑老节点和新节点儿子的情况
4. 优化比较：头头、尾尾、头尾、尾头
5. 比对查找进行复用

Vue2 与 Vue3.x 的 diff 算法：
Vue2 的核心 Diff 算法采用了双端比较的算法，同时从新旧 children 的两端开始进行比较，借助 key 值找到可复用的节点，再进行相关操作。
Vue3.x 借鉴了 ivi 算法和 inferno 算法，该算法中还运用了动态规划的思想求解最长递归子序列。(实际的实现可以结合 Vue3.x 源码看。)

源码地址：src/core/vdom/patch.js 501

### v-if 与 v-for 的优先级

1、v-for 优先于 v-if 被解析
2、如果同时出现，每次渲染都会先执行循环再判断条件，无论如何循环都不可避免，浪费了性能
3、要避免出现这种情况，则在外层嵌套 template，在这一层进行 v-if 判断，然后在内部进行 v-for 循环
4、如果条件出现在循环内部，可通过计算属性提前过滤掉那些不需要显示的项
源码地址：compiler/codegen/index.js

### v-if 与 v-show 的区别

v-if 是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 “display” 属性进行切换。

所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。

### computed 和 watch 的区别

computed 和 watch 的区别和运用的场景？

computed： 计算属性。依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值；
watch： 监听数据的变化。更多的是「观察」的作用，类似于某些数据的监听回调 ，每当监听的数据变化时都会执行回调进行后续操作；

运用场景：

1. 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
2. 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作 ( 访问一个 API )，限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

### 自定义指令的理解

如何理解自定义指令？

指令的实现原理，可以从编译原理 =>代码生成=> 指令钩子实现进行概述

1. 在生成 ast 语法树时，遇到指令会给当前元素添加 directives 属性
2. 通过 genDirectives 生成指令代码
3. 在 patch 前将指令的钩子提取到 cbs 中，在 patch 过程中调用对应的钩子。
4. 当执行指令对应钩子函数时，调用对应指令定义的方法

## v-modal 原理

V-model 的原理是什么？

v-model 本质就是一个语法糖，可以看成是 value + input 方法的语法糖。可以通过 model 属性的 prop 和 event 属性来进行自定义。原生的 v-model，会根据标签的不同生成不同的事件和属性。
v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

1. text 和 textarea 元素使用 value 属性和 input 事件；
2. checkbox 和 radio 使用 checked 属性和 change 事件；
3. select 字段将 value 作为 prop 并将 change 作为事件。

## 常考-性能优化

你都做过哪些 Vue 的性能优化？（ 统计后的结果 ）

### 编码阶段

尽量减少 data 中的数据，data 中的数据都会增加 getter 和 setter，会收集对应的 watcher；
如果需要使用 v-for 给每项元素绑定事件时使用事件代理；
SPA 页面采用 keep-alive 缓存组件；
在更多的情况下，使用 v-if 替代 v-show；
key 保证唯一；
使用路由懒加载、异步组件；
防抖、节流；
第三方模块按需导入；
长列表滚动到可视区域动态加载；
图片懒加载；

### 用户体验：

骨架屏；
PWA；
还可以使用缓存(客户端缓存、服务端缓存)优化、服务端开启 gzip 压缩等。

### SEO 优化

预渲染；
服务端渲染 SSR；

### 打包优化

压缩代码；
Tree Shaking/Scope Hoisting；
使用 cdn 加载第三方模块；
多线程打包 happypack；
splitChunks 抽离公共文件；
sourceMap 优化；
