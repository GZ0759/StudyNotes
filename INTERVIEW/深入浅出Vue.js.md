[从源码解读 - Vue 常考面试题](https://mp.weixin.qq.com/s/5YR2pgxgB5K-_B6QpN0uSw)  
[30 道 Vue 面试题，内含详细讲解（涵盖入门到精通，自测 Vue 掌握程度）](https://juejin.im/post/6844903918753808398)  
[「面试题」20+Vue 面试题整理](https://juejin.im/post/6844904084374290446)

# Vue

## 基础知识

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

### MVVM 模式

什么是 MVVM？

Model–View–ViewModel （MVVM） 是一个软件架构设计模式，由微软 WPF 和 Silverlight 的架构师 Ken Cooper 和 Ted Peters 开发，是一种简化用户界面的事件驱动编程方式。由 John Gossman（同样也是 WPF 和 Silverlight 的架构师）于 2005 年在他的博客上发表。

MVVM 源自于经典的 Model–View–Controller（MVC）模式 ，MVVM 的出现促进了前端开发与后端业务逻辑的分离，极大地提高了前端开发效率，MVVM 的核心是 ViewModel 层，它就像是一个中转站（value converter），负责转换 Model 中的数据对象来让数据变得更容易管理和使用，该层向上与视图层进行双向数据绑定，向下与 Model 层通过接口请求进行数据交互，起呈上启下作用。如下图所示：

1. View 是视图层，也就是用户界面。前端主要由 HTML 和 CSS 来构建 。
2. Model 是指数据模型，泛指后端进行的各种业务逻辑处理和数据操控，对于前端来说就是后端提供的 api 接口。
3. ViewModel 是由前端开发人员组织生成和维护的视图数据层。

在 ViewModel 层，前端开发者对从后端获取的 Model 数据进行转换处理，做二次封装，以生成符合 View 层使用预期的视图数据模型。需要注意的是 ViewModel 所封装出来的数据模型包括视图的状态和行为两部分，而 Model 层的数据模型是只包含状态的，比如页面的这一块展示什么，而页面加载进来时发生什么，点击这一块发生什么，这一块滚动时发生什么这些都属于视图行为（交互），视图状态和行为都封装在了 ViewModel 里。这样的封装使得 ViewModel 可以完整地去描述 View 层。

MVVM 框架实现了双向绑定，这样 ViewModel 的内容会实时展现在 View 层，前端开发者再也不必低效又麻烦地通过操纵 DOM 去更新视图，MVVM 框架已经把最脏最累的一块做好了，我们开发者只需要处理和维护 ViewModel，更新数据视图就会自动得到相应更新。这样 View 层展现的不是 Model 层的数据，而是 ViewModel 的数据，由 ViewModel 负责与 Model 层交互，这就完全解耦了 View 层和 Model 层，这个解耦是至关重要的，它是前后端分离方案实施的重要一环。

### 数据双向绑定

Vue 数据双向绑定主要是指：数据变化更新视图，视图变化更新数据。主要通过一下四个步骤来实现。

1. 实现一个监听器 Observer：对数据对象进行遍历，包括子属性对象的属性，利用 `Object.defineProperty()` 监听属性。
2. 实现一个解析器 Compile：解析 Vue 模板指令，将模板中的变量都替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，调用更新函数进行数据更新。
3. 实现一个订阅者 Watcher：Watcher 订阅者是 Observer 和 Compile 之间通信的桥梁 ，主要的任务是订阅 Observer 中的属性值变化的消息，当收到属性值变化的消息时，触发解析器 Compile 中对应的更新函数。
4. 实现一个订阅器 Dep：订阅器采用 发布-订阅 设计模式，用来收集订阅者 Watcher，对监听器 Observer 和 订阅者 Watcher 进行统一管理。

### Vue 初始化

`new Vue()` 发生了什么？

每个 Vue 应用都是通过用 Vue 函数创建一个新的 Vue 实例开始的：虽然没有完全遵循 MVVM 模型，但是 Vue 的设计也受到了它的启发。因此在文档中经常会使用 vm （ViewModel 的缩写） 这个变量名表示 Vue 实例。当创建一个 Vue 实例时，你可以传入一个选项对象，使用这些选项来创建想要的行为。

- 数据与方法
  - 将 data 对象中的所有的 property 加入到 Vue 的响应式系统中
  - 暴露了一些有用的实例 property 与方法。它们都有前缀 `$`，以便与用户定义的 property 区分开来
- 实例生命周期钩子

`new Vue()`是创建 Vue 实例，它内部执行了根实例的初始化过程。创建了根实例并准备好数据和方法，未来执行挂载时，此过程还会递归的应用于它的子组件上，最终形成一个有紧密关系的组件实例树。具体包括以下操作：

- 选项合并
- 实例的方法初始化
- 自定义事件处理
- 数据响应式处理
- 生命周期钩子调用
- 可能的挂载

源码地址：src/core/instance/init.js

### Vue.use 是干什么的？原理是什么？

vue.use 是用来使用插件的，我们可以在插件中扩展全局组件、指令、原型方法等。如果插件是一个对象，必须提供 install 方法。如果插件是一个函数，它会被作为 install 方法。该方法需要在调用 `new Vue()` 之前被调用。当 install 方法被同一个插件多次调用，插件将只会被安装一次。

1. 首先判断这个插件是否被注册过，不允许重复注册
2. 将传入的参数整理成数组，将 Vue 对象替换成第一个参数
3. 调用插件的 install 方法或者插件本身
4. 将插件添加到已添加的插件数组中，缓存插件。

源码地址：src/core/global-api/use.js

### 响应式数据的实现

请说一下响应式数据的理解？

Vue 最独特的特性之一，就是其非侵入性的响应式系统。数据模型仅仅是普通的 JavaScript 对象。当修改它们时，视图会更新。这使得状态管理非常简单直接。

当把一个普通的 JavaScript 对象传入 Vue 实例作为 data 选项，Vue 将遍历此对象所有的 property，并使用 `Object.defineProperty` 把这些 property 全部转为 getter/setter。`Object.defineProperty` 是 ES5 中一个无法 shim 的特性，这也就是 Vue 不支持 IE8 以及更低版本浏览器的原因。

对于对象来说，依赖是在 getter 中收集，在 setter 中触发执行。使用一个 Dep 类来管理依赖。Vue 无法检测 property 的添加或移除，所以 property 必须在 data 对象上存在才能让 Vue 将它转换为响应式的，而中途新增属性或者使用 delete 方法也不会成功。

对于数组来说，Vue 用来改变数组的方法都是通过内部的拦截器提供的，数组的依赖也是在 getter 中收集，依赖存放在 Observer 中，然后拦截器便可以访问这些依赖。但利用索引直接设置一个数组项或直接修改数组长度的时候，就无法追踪。这时可以可以使用 `vm.$set` 方法或者数组变异方法。

这里可以引出性能优化相关的内容：

1. 对象层级过深，性能就会差。
2. 不需要响应数据的内容不要放在 data 中。
3. `object.freeze()` 可以冻结数据。

源码地址：src/core/observer/index.js 158

### 检测数组变化

Vue 如何检测数组变化？

数组考虑性能原因没有用 defineProperty 对数组的每一项进行拦截，而是选择重写数组方法以进行重写。当数组调用到这 7 个方法 push/pop/shift/unshift/splice/reverse/sort 的时候，进行派发更新

补充回答：
在 Vue 中修改数组的索引和长度是无法监控到的。需要通过 7 种变异方法修改数组才会触发数组对应的 wacther 进行更新。数组中如果是对象数据类型也会进行递归劫持。
如果想要改变索引更新数据，可以通过 `Vue.set()` 来进行处理，其核心内部用的是 splice 方法。

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

1. 如果是数组，调用重写的 splice 方法 （这样可以更新视图 ）
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

Proxy 与 `Object.defineProperty` 优劣对比

Proxy 的优势如下:

1. 可以直接监听对象而非属性
2. 可以直接监听数组的变化
3. 有多达 13 种拦截方法,不限于 apply、ownKeys、deleteProperty、has 等等
4. 返回的是一个新对象，我们可以只操作新的对象达到目的，而 `Object.defineProperty` 只能遍历对象属性直接修改
5. 作为新标准将受到浏览器厂商重点持续的性能优化，也就是传说中的新标准的性能红利

`Object.defineProperty` 的优势是兼容性好，支持 IE9，而 Proxy 的存在浏览器兼容性问题，而且无法用 polyfill 磨平，因此 Vue 的作者才声明需要等到下个大版本才能用 Proxy 重写。

### Vue3.x 响应式数据原理

Vue3.x 改用 Proxy 替代 Object.defineProperty。因为 Proxy 可以直接监听对象和数组的变化，并且有多达 13 种拦截方法。并且作为新标准将受到浏览器厂商重点持续的性能优化。

Proxy 只会代理对象的第一层，那么 Vue3 又是怎样处理这个问题的呢？
判断当前 Reflect.get 的返回值是否为 Object，如果是则再通过 reactive 方法做代理，这样就实现了深度观测。

监测数组的时候可能触发多次 get/set，那么如何防止触发多次呢？
我们可以判断 key 是否为当前被代理对象 target 自身属性，也可以判断旧值与新值是否相等，只有满足以上两个条件之一时，才有可能执行 trigger。

## 生命周期

### 所有的钩子方法

Vue 的生命周期方法有哪些？

每个 Vue 实例在被创建时都要经过一系列的初始化过程，在这个过程中也会运行一些叫做生命周期钩子的函数，这给用户在不同阶段添加自己代码的机会。生命周期总共分为 8 个阶段：创建前/后，载入前/后，更新前/后，销毁前/后。

1. 创建前/后：

- beforeCreate：初始化 Vue 空的实例对象，只有一些默认的生命周期函数和默认的事件。在当前阶段 data、methods、computed 以及 watch 都不能被访问。
- created：实例的数据对象 data 和方法 methods 都已经初始化，可以做一些初始数据的获取，不可以在当前阶段无法与 Dom 进行交互，但可以通过 `vm.$nextTick` 来访问 Dom。

2. 载入前/后：

- beforeMount：模板已经在内存中编译完成，还是在挂载之前为虚拟的 DOM 节点。在此时也可以对数据进行更改，不会触发 updated。
- mounted：实例挂载 el 完成，代表整个 Vue 实例 已经初始化完成，进行运行阶段。真实的 Dom 挂载完毕，数据完成双向绑定，可以访问到 DOM 节点，可以使用 `$refs` 属性对 DOM 进行操作。

3. 更新前/后：

组件运行阶段的声明周期函数，响应式数据更新时调用，有选择性的触发，可能是零次或者多次。

- beforeUpdate：发生在虚拟 DOM 打补丁之前，适合在更新之前访问现有的 DOM，比如手动移除已添加的事件监听器。可以在当前阶段进行更改数据，不会造成重渲染。
- updated：虚拟 DOM 重新渲染和打补丁之后调用，组成新的 DOM 已经更新，避免在这个钩子函数中操作数据，防止死循环。要注意的是避免在此期间更改数据，因为这可能会导致无限循环的更新。

4. 销毁前/后：

实例从运行阶段进入销毁阶段。

- beforeDestroy：实例销毁前调用，实例还可以用，this 能获取到实例，常用于销毁定时器，解绑事件。
- destroyed：实例销毁后调用，调用后所有事件监听器会被移除，所有的子实例都会被销毁。说明：当前阶段组件已被拆解，数据绑定被卸除，监听被移出，子实例也统统被销毁。

源码地址：src/core/instance/lifecycle.js

### 钩子的实现

生命周期钩子是如何实现的？

Vue 的生命周期钩子就是回调函数而已，当创建组件实例的过程中会调用对应的钩子方法。

补充回答：
内部主要是使用 callHook 方法来调用对应的方法。核心是一个发布订阅模式，将钩子订阅好（内部采用数组的方式存储），在对应的阶段进行发布。

源码地址：src/core/util/options.js 146 core/instance/lifecycle.js 336

### 钩子执行顺序

父组件和子组件生命周期钩子函数执行顺序可以归类为以下四部分。其中最重要的是，父组件等待子组件完成后，才会执行自己对应完成的钩子。

1. 加载渲染过程：

父组件挂载完成一定是等子组件都挂载完成后，才算是父组件挂载完，所以父组件的 mounted 在子组件 mouted 之后

```
父 beforeCreate/created/beforeMount
子 beforeCreate/created/beforeMount/mounted
父 mounted
```

2. 子组件更新过程：

影响到父组件

```
父 beforeUpdate
子 beforeUpdate/updated
父 updated
```

不影响父组件

```
子 beforeUpdate/updated
```

3. 父组件更新过程：

影响到子组件

```
父 beforeUpdate
子 beforeUpdate/updated
父 updted
```

不影响子组件

```
父 beforeUpdate/updated
```

4. 销毁过程：

```
父 beforeDestroy
子 beforeDestroy/destroyed
父 destroyed
```

第一次页面加载时会触发 beforeCreate/created/beforeMount/mounted，可以在后三个阶段进行异步请求，因为能在服务端返回的数据进行赋值。

推荐在 created 钩子函数中调用，因为可以更快获取数据，减少页面等待时间。在挂载后可以进行一些 DOM 操作，但 SSR 不支持 beforeMount/mounted，因此放在 created 中有助于一致性。

### 钩子事件 hookEvent

父组件可以监听到子组件的生命周期吗？

比如有父组件 Parent 和子组件 Child，如果父组件监听到子组件挂载 mounted 就做一些逻辑处理，可以通过以下写法实现：

```
// Parent.vue
<Child @mounted="doSomething"/>

// Child.vue
mounted() {
  this.$emit("mounted");
}
```

以上需要手动通过 `$emit` 触发父组件的事件，更简单的方式可以在父组件引用子组件时通过 `@hook` 来监听即可，如下所示：

```
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
  console.log('父组件监听到 mounted 钩子函数 ...');
},

//  Child.vue
mounted(){
  console.log('子组件触发 mounted 钩子函数 ...');
},
```

如果想给一个 Vue 组件添加生命周期函数有 3 个办法：

1. 在 Vue 组件选项中添加；
2. 在模板中通过 `@hooks:created` 这种形式；
3. `vm.$once('hooks:created', cb)`。

## 组件通信

### 组件的数据 data 选项

Vue 中的组件的 data 为什么是一个函数？而 new Vue 实例里，data 可以直接是一个对象？

每次使用组件时都会对组件进行实例化操作，并且调用 data 函数返回一个对象作为组件的数据源。这样可以保证多个组件间数据互不影响。如果 data 是对象的话，对象属于引用类型，会影响到所有的实例。

但是 new Vue 的实例，是不会被复用的，因此不存在引用对象的问题。

源码地址：src/core/util/options 121

### 单向数据流

怎样理解 Vue 的单向数据流？

所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。这样会防止从子组件意外改变父级组件的状态，从而导致你的应用的数据流向难以理解。

额外的，每次父级组件发生更新时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。如果你这样做了，Vue 会在浏览器的控制台中发出警告。

子组件想修改时，只能通过 `$emit` 派发一个自定义事件，父组件接收到后，由父组件修改。

有两种常见的试图改变一个 prop 的情形 :

1. 定义一个本地的 data 属性并将这个 prop 用作其初始值
2. 使用这个 prop 的值来定义一个计算属性

### 组件通信方式

Vue 组件间通信有哪几种方式？

Vue 组件间通信只要指以下 3 类通信：父子组件通信、隔代组件通信、兄弟组件通信

1. `props` 和 `$emit` 适用 父子组件通信

2. `ref` 与 `$parent`/`$children` 适用 父子组件通信

- `ref`：指向 DOM 元素或组件实例
- `$parent`或`$children`：访问父或子实例

3. EventBus （`$emit`/`$on`） 适用于 父子、隔代、兄弟组件通信

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

4. `$attrs`/`$listeners` 适用于 隔代组件通信

`$attrs`：包含了父作用域中不被 prop 所识别且获取的特性绑定，class 和 style 除外。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定，并且可以通过 `v-bind="$attrs"` 传入内部组件。通常配合 inheritAttrs 选项一起使用。

`$listeners`：包含了父作用域中的 v-on 事件监听器，不含 native 修饰器的。它可以通过 `v-on="$listeners"` 传入内部组件。

5. `provide`/`inject` 适用于 隔代组件通信

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。provide/inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

6. `Vuex` 适用于 父子、隔代、兄弟组件通信

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态（state）。

Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。改变 store 中的状态的唯一途径就是显式地提交 mutation。这样使得我们可以方便地跟踪每一个状态的变化。

主要包括以下几个模块

- State：定义了应用状态的数据结构，可以在这里设置默认的初始状态。
- Getter：允许组件从 Store 中获取数据，mapGetters 辅助函数仅仅是将 store 中的 getter 映射到局部计算属性。
- Mutation：是唯一更改 store 中状态的方法，且必须是同步函数。
- Action：用于提交 mutation，而不是直接变更状态，可以包含任意异步操作。
- Module：允许将单一的 Store 拆分为多个 store 且同时保存在单一的状态树中。

### 组件中的 name 选项

组件中写 name 选项有哪些好处及作用？

1. 可以通过名字找到对应的组件 （ 递归组件 ）
2. 可以实现 keep-alive 缓存功能
3. 可以识别组件，跨级组件通信时非常重要

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

keep-alive 是 Vue 内置的一个组件，能够将不活动的组件实例保存在内存中，而不是直接将其销毁，这是一个抽象组件。因此，可以使被包含的组件保留状态，避免重新渲染，其有以下特性

- 一般结合路由和动态组件一起使用，用于缓存组件
- 提供 include 和 exclude 属性，include 表示只有名称匹配的组件会被缓存，exclude 表示任何名称匹配的组件都不会被缓存
- 提供 max 属性最多可以缓存多少组件实例。一旦这个数字达到了，在新实例被创建之前，已缓存组件中最久没有被访问的实例会被销毁掉
- 对应两个钩子函数 activated 和 deactivated ，在组件激活和销毁时触发。

LRU 缓存算法

LRU（Least recently used）算法根据数据的历史访问记录来进行淘汰数据，其核心思想是“如果数据最近被访问过，那么将来被访问的几率也更高”。

1. 最常见的实现是使用一个链表保存缓存数据，详细算法实现如下：

- 新数据插入到链表头部；
- 每当缓存命中（即缓存数据被访问），则将数据移到链表头部；
- 当链表满的时候，将链表尾部的数据丢弃。

2. 还可以使用 es6 中的 map 来实现：map 中插入数据有顺序的。

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

### 混入 mixin

Vue.mixin 的使用场景和原理？

混入提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。Vue.mixin 的作用就是抽离公共的业务逻辑，原理类似“对象的继承”。

当组件初始化时会调用 mergeOptions 方法进行合并，采用策略模式针对不同的属性进行合并，如果混入的数据和本身组件中的数据冲突，会采用“就近原则”，以组件的数据为准。

补充回答：
mixin 中有很多缺陷“命名冲突问题”，“依赖问题”，“数据来源问题”，这里强调一下 mixin 的数据是不会被共享的。

源码地址：src/core/util/options.js

## 路由

### 路由钩子函数

Vue-router 有几种钩子函数？具体是什么及执行流程是怎样的？

路由钩子的执行流程，钩子函数种类有：全局守卫、路由守卫、组件守卫。

- 全局前置守卫 beforeEach
- 全局解析守卫 beforeResolve
- 全局后置守卫 afterEach
- 路由独享守卫 beforeEnter
- 组件守卫 beforeRouterEnter
- 组件守卫 beforeRouterUpdate
- 组件守卫 beforeRouterLeave

完整的导航解析流程

1. 导航被触发。
2. 在失活的组件里调用 beforeRouteLeave 守卫。
3. 调用全局的 beforeEach 守卫。
4. 在重用的组件里调用 beforeRouteUpdate 守卫
5. 在路由配置里调用 beforeEnter。
6. 解析异步路由组件。
7. 在被激活的组件里调用 beforeRouteEnter。
8. 调用全局的 beforeResolve 守卫
9. 导航被确认。
10. 调用全局的 afterEach 钩子。
11. 触发 DOM 更新。
12. 调用 beforeRouteEnter 守卫中传给 next 的回调函数，创建好的组件实例会作为回调函数的参数传入。

### vue-router 模式

vue-router 路由模式有几种？

vue-router 有 3 种路由模式：hash、history、abstract。

1. hash: 使用 URL hash 值来作路由。支持所有浏览器，包括不支持 HTML5 History Api 的浏览器；
2. history : 依赖 HTML5 History API 和服务器配置。
3. abstract : 支持所有 JavaScript 运行环境，如 Node.js 服务器端。如果发现没有浏览器的 API，路由会自动强制进入这个模式。

**hash 模式的实现原理**

vue-router 默认 hash 模式。早期的前端路由的实现就是基于 location.hash 来实现的。其实现原理很简单，location.hash 的值就是 URL 中 `#` 后面的内容。比如下面这个`https://www.word.com#search`网站，它的 location.hash 的值为 '#search'。

hash 路由模式的实现主要是基于下面几个特性：

- URL 中 hash 值只是客户端的一种状态，也就是说当向服务器端发出请求时，hash 部分不会被发送；
- hash 值的改变，都会在浏览器的访问历史中增加一个记录。因此我们能通过浏览器的回退、前进按钮控制 hash 的切换；
- 可以通过  a  标签，并设置  href  属性，当用户点击这个标签后，URL  的 hash 值会发生改变；或者使用  JavaScript 来对  loaction.hash  进行赋值，改变 URL 的 hash 值；
- 可以使用 hashchange 事件来监听 hash 值的变化，从而对页面进行跳转（渲染）。

**history 模式的实现原理**

HTML5 提供了 History API 来实现 URL 的变化。其中做最主要的 API 有以下两个：`history.pushState()` 和 `history.repalceState()`。这两个 API 可以在不进行刷新的情况下，操作浏览器的历史纪录。唯一不同的是，前者是新增一个历史记录，后者是直接替换当前的历史记录。这个模式还需要还需要后台配置支持。

history 路由模式的实现主要基于存在下面几个特性：

- pushState 和 repalceState 两个 API 来操作实现 URL 的变化 ；
- 可以使用 popstate 事件来监听 url 的变化，从而对页面进行跳转（渲染）；
- pushState 方法或 replaceState 方法不会触发 popstate 事件，这时我们需要手动触发页面跳转（渲染）。

## 属性作用与对比

### nextTick 原理

nextTick 在哪里使用？原理是？

nextTick 的回调是在下次 DOM 更新循环结束之后执行的延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。nextTick 主要使用了宏任务和微任务。原理就是异步方法 promise/mutationObserver/setImmediate/setTimeout 经常与事件循环一起来问。

补充回答：
vue 多次更新数据，最终会进行批处理更新。内部调用的就是 nextTick 实现了延迟更新，用户自定义的 nextTick 中的回调会被延迟到更新完成后调用，从而可以获取更新后的 DOM。

源码地址：src/core/util/next-tick.js 42

### 虚拟 DOM 的优势和劣势

Vue 为什么需要虚拟 DOM？虚拟 DOM 的优劣如何？

Virtual DOM 就是用 js 对象来描述真实 DOM，是对真实 DOM 的抽象，由于直接操作 DOM 性能低但是 js 层的操作效率高，可以将 DOM 操作转化成对象操作，最终通过 diff 算法比对差异进行更新 DOM （减少了对真实 DOM 的操作）。虚拟 DOM 不依赖真实平台环境从而也可以实现跨平台。

优点：

1. 保证性能下限。框架的虚拟 DOM 需要适配任何上层 API 可能产生的操作，它的一些 DOM 操作的实现必须是普适的，所以它的性能并不是最优的；但是比起粗暴的 DOM 操作性能要好很多，因此框架的虚拟 DOM 至少可以保证在你不需要手动优化的情况下，依然可以提供还不错的性能，即保证性能的下限；
2. 无需手动操作 DOM。我们不再需要手动去操作 DOM，只需要写好 View-Model 的代码逻辑，框架会根据虚拟 DOM 和 数据双向绑定，帮我们以可预期的方式更新视图，极大提高我们的开发效率；
3. 跨平台。虚拟 DOM 本质上是 JavaScript 对象,而 DOM 与平台强相关，相比之下虚拟 DOM 可以进行更方便地跨平台操作，例如服务器渲染、weex 开发等等。

缺点:

1. 无法进行极致优化。虽然虚拟 DOM + 合理的优化，足以应对绝大部分应用的性能需求，但在一些性能要求极高的应用中虚拟 DOM 无法进行针对性的极致优化。

补充回答：
虚拟 DOM 的实现就是普通对象包含 tag、data、children 等属性对真实节点的描述。（本质上就是在 JS 和 DOM 之间的一个缓存）
Vue2 的 Virtual DOM 借鉴了开源库 snabbdom 的实现。
VirtualDOM 映射到真实 DOM 要经历 VNode 的 create、diff、patch 等阶段。

源码地址：src/core/vdom/vnode: 3

### 虚拟 DOM 实现原理

虚拟 DOM 的实现原理主要包括以下 3 部分：

1. 用 JavaScript 对象模拟真实 DOM 树，对真实 DOM 进行抽象；
1. diff 算法 — 比较两棵虚拟 DOM 树的差异；
1. pach 算法 — 将两个虚拟 DOM 对象的差异应用到真正的 DOM 树。

### Vue 中 key 的作用

Vue 中 key 的作用和工作原理，说说你对它的理解

key 的特殊 attribute 主要用在 Vue 虚拟 DOM 算法，在新旧 nodes 对比时辨识 VNodes。如果不使用 key，Vue 会使用一种最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。而使用 key 时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。最常见的用例是用于 for 遍历。

key 的作用主要是为了高效的更新虚拟 DOM，其原理是 vue 在 patch 过程中通过 key 可以精准判断两个节点是否是同一个，从而避免频繁更新不同元素，使得整个 patch 过程更加高效，减少 DOM 操作量，提高性能。

- 更准确
- 更快速

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

v-for 优先于 v-if 被解析。如果同时出现，每次渲染都会先执行循环再判断条件，无论如何循环都不可避免，浪费了性能。

要避免出现这种情况，则在外层嵌套 template，在这一层进行 v-if 判断，然后在内部进行 v-for 循环。如果条件出现在循环内部，可通过计算属性提前过滤掉那些不需要显示的项。

源码地址：compiler/codegen/index.js

### v-if 与 v-show 的区别

v-if 是真正的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建；也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。

v-show 就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 的 display 属性进行切换。

所以，v-if 适用于在运行时很少改变条件，不需要频繁切换条件的场景；v-show 则适用于需要非常频繁切换条件的场景。

### 计算属性和侦听器的区别

computed 和 watch 的区别和运用的场景？

computed 是计算属性。依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值。

watch 是监听数据的变化。更多的是观察的作用，类似于某些数据的监听回调，每当监听的数据变化时都会执行回调进行后续操作；

1. 当我们需要进行数值计算，并且依赖于其它数据时，应该使用 computed，因为可以利用 computed 的缓存特性，避免每次获取值时，都要重新计算；
2. 当我们需要在数据变化时执行异步或开销较大的操作时，应该使用 watch，使用 watch 选项允许我们执行异步操作（访问一个 API），限制我们执行该操作的频率，并在我们得到最终结果前，设置中间状态。这些都是计算属性无法做到的。

### 自定义指令的理解

如何理解自定义指令？

指令的实现原理，可以从编译原理 =>代码生成=> 指令钩子实现进行概述

1. 在生成 ast 语法树时，遇到指令会给当前元素添加 directives 属性
2. 通过 genDirectives 生成指令代码
3. 在 patch 前将指令的钩子提取到 cbs 中，在 patch 过程中调用对应的钩子。
4. 当执行指令对应钩子函数时，调用对应指令定义的方法

### v-modal 原理

V-model 的原理是什么？

在项目中主要使用 v-model 指令在表单 input、textarea、select 等元素上创建双向数据绑定，我们知道 v-model 本质上不过是语法糖，v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

v-model 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

1. text 和 textarea 元素使用 value 属性和 input 事件；
2. checkbox 和 radio 使用 checked 属性和 change 事件；
3. select 字段将 value 作为 prop 并将 change 作为事件。

如果在自定义组件中，v-model 默认会利用名为 value 的 prop 和名为 input 的事件。

## 服务端渲染

### Vue SSR

使用过 Vue SSR 吗？说说 SSR？

Vue.js 是构建客户端应用程序的框架。默认情况下，可以在浏览器中输出 Vue 组件，进行生成 DOM 和操作 DOM。然而，也可以将同一个组件渲染为服务端的 HTML 字符串，将它们直接发送到浏览器，最后将这些静态标记"激活"为客户端上完全可交互的应用程序。

服务端渲染 SSR 的优缺点如下：

服务端渲染的优点：

- 更好的 SEO： 因为 SPA 页面的内容是通过 Ajax 获取，而搜索引擎爬取工具并不会等待 Ajax 异步完成后再抓取页面内容，所以在 SPA 中是抓取不到页面通过 Ajax 获取到的内容；而 SSR 是直接由服务端返回已经渲染好的页面（数据已经包含在页面中），所以搜索引擎爬取工具可以抓取渲染好的页面；
- 更快的内容到达时间（首屏加载更快）： SPA 会等待所有 Vue 编译后的 js 文件都下载完成后，才开始进行页面的渲染，文件下载等需要一定的时间等，所以首屏渲染需要一定的时间；SSR 直接由服务端渲染好页面直接返回显示，无需等待下载 js 文件及再去渲染等，所以 SSR 有更快的内容到达时间；

服务端渲染的缺点：

- 更多的开发条件限制： 例如服务端渲染只支持 beforCreate 和 created 两个钩子函数，这会导致一些外部扩展库需要特殊处理，才能在服务端渲染应用程序中运行；并且与可以部署在任何静态文件服务器上的完全静态单页面应用程序 SPA 不同，服务端渲染应用程序，需要处于 Node.js server 运行环境；
- 更多的服务器负载：在 Node.js 中渲染完整的应用程序，显然会比仅仅提供静态文件的 server 更加大量占用 CPU 资源（CPU-intensive - CPU 密集），因此如果你预料在高流量环境（ high traffic）下使用，请准备相应的服务器负载，并明智地采用缓存策略。

## 性能优化

你都做过哪些 Vue 的性能优化？（ 统计后的结果 ）

### 编码阶段

1. v-if/v-show 和 computed/watch 区分各自使用场景
2. 减少 data 选项中不必要的数据
3. v-for 遍历添加 key，准确使用 v-if，适当添加事件代理
4. SPA 页面采用 keep-alive 缓存组件
5. 长列表/无限列表性能优化
6. 事件的销毁
7. 路由懒加载/异步组件
8. 防抖、节流
9. 第三方插件按需引入
10. 图片懒加载
11. 骨架屏

### Webpack 层面

1. Webpack 对图片/代码进行压缩
2. 减少 ES6 转为 ES5 的冗余代码
3. 提取公共代码
4. 模板预编译
5. 提取组件的 CSS
6. 优化 SourceMap
7. 构建结果输出分析
8. Vue 项目的编译优化

### Web 技术的优化

1. 开启 gzip 压缩
2. 浏览器缓存
3. CDN 的使用
4. 使用 Chrome Performance 查找性能瓶颈
5. 服务端渲染/预渲染
