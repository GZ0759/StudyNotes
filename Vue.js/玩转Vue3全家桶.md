> 玩转 Vue 3 全家桶  
> 大圣 前百度前端架构师  
> [课程地址](https://time.geekbang.org/column/intro/100094401)

# 玩转 Vue3 全家桶

## 建构前端知识体系

### 为什么要学 Vue3

在目前的前端开发中，流行的框架相信你并不陌生。它们的目标都是为了帮助开发者高效地开发 Web 应用，只不过走的路线略显不同，比如 React 注重数据不可变、虚拟 DOM 和运行时；而 Svelte 运行时都非常轻量级，侧重在于编译时的优化；Angular 则在抽象这个维度又走向一个极致，生来就是为了复杂项目。
每个流行框架的内部，都有一大堆的最佳实践。而相比之下，Vue 就简单多了，简单到大部分前端开发者都能学得会。Vue 在每个维度之间，做了非常好的权衡和取舍，算是一个非常中庸且优雅的框架，兼顾响应式、虚拟 DOM、运行时和编译优化。
而且 Vue 3 作为 Vue 框架最新的版本，有很多优秀的设计相信你会非常喜欢，例如 Composition 组合 API、基于 Proxy 的响应式系统、自定义渲染器等。
这些设计可以让我们以很轻松的方式，从最熟悉的框架逐渐深入底层。学习 Vue 3 的同时，我们就可以去回顾 Vue 1 和 Vue 2，直观地感受 Vue 框架发展的过程。在此基础上，我们再去横向对比 Angular、React、Svelte 等框架，最终是可以把学到的知识点串成一个网络的。这不仅是加强记忆那么简单，还能大大开阔你的前端视野。

### 如何学习 Vue3

既然我们已经锚定了 Vue 3 这个出发点，那么该如何学习它呢？
Vue 3 已经是上手最简单的框架了，如果你没有 Vue 2 的经验，可以直接走 Vite+Option 先熟悉模板的语法，把官网的入门教程先走一遍，然后再去研究 Vue 3 的新特性。
不过，如果你没有 Vue 2 的经验，或者 Vue 基础比较薄弱，也不用害怕，你可以跟着我的脚步，往下学《上手：一个清单应用帮你入门 Vue.js》这一讲。在这里，即便你不熟悉 Vue，也能先体验一把 Vue。
而如果你已经是 Vue 2 的开发者，那么上手 Vue 3 就更简单了，直接去熟悉 Composition API 的新语法就可以了，我们专栏中的项目也会主要用 Composition API 来组织。
入门以后，我们就可以正式探索冰山了。但进阶之路还是要慢慢走，我们会逐步补齐要学习的下面这些版块的内容，从而帮你构建出一个完整的前端知识体系。

## 什么是好的项目?

### 文件上传的场景

比如，在我们上传一个 2GB 大小的视频文件的时候，如果直接使用 axios.post 上传，那么中途一旦出现网络卡顿，就需要重新上传这个视频文件。这就会对用户的体验造成不好的影响，所以在这种数据量极大的场景下，我们需要采用断点续传的解决方案。

把文件切成数据块依次上传，如果上传的过程中，出现了网络错误，那么再次上传的时候，就会把已经存在的切片列表过滤掉，只上传其他的切片。

完成上述断点续传的功能之后，我们就完成了项目的初步优化，在文件上传之前，我们需要在前端计算出一个文件的 Hash 值作为唯一标识，用来向后端询问切片的列表。

对于卡顿问题，我们可以通过 web-workder 去解决，这有点像孙悟空可以用猴毛变出一个分身，我们这里的 hash.js，就相当于浏览器主进程的分身，用分身就可以去计算 Hash 值，不耽误主进程的任务。

### 列表渲染的场景

使用虚拟列表就意味着，我们只需要渲染视图中可见的 DOM 元素，就可以实现性能优化了。看下面的示意图，我们只渲染窗口中的绿色元素，然后浏览器滚动的过程中我们维护这些 DOM，就可以避免因为页面中 DOM 元素过多，而引起的卡顿问题。

### 给项目骨干开发者的优化建议

1. 团队脚手架项目，把项目中的代码规范、Vite 配置，log 等等都集成在脚手架内部，通过这样的方式，可以提高项目的启动效率。
2. 基础组件库的项目，做出一个类似 Element3 的基础组件库，并且发布在公司的 npm 服务之上，提供给全公司前端使用。给组件库实现完备的文档系统以及超过 90% 的单测覆盖率。
3. CI/CD 项目，利用 GitHub 的 action 机制，可以把整个发布过程自动化，并且还可以一键回滚。解决需求频繁变更的问题，以及版本迭代的需求。

作为项目负责人来说，你要能够在整体上推动项目向前，提高团队整体的研发效率就是你做的项目最大的亮点。

其实面试官问你做过什么项目，目的就是想通过你做的项目，挖掘出你的技术亮点，所以不要一句“我做过 XXX 项目”一闪而过，我们可以尝试使用 STAR 原则去描述项目。所谓 STAR 原则，即 Situation（情景）、Task（任务）、Action（行动）和 Result（结果）四个英文单词的首字母组合，也就是你在什么情景下、遇见了什么任务、做了什么动作，拿到了怎样的结果，结果中最好还能带上数字展示，这样你的项目的描述就会很饱满。

2020-2021 在极客时间负责官网开发和后台管理系统。对此，我们可以用 STAR 原则来对你的项目描述加以优化，对比之下不难发现，下面的描述明显比上面的描述更能突出你的技术特点和个人能力。

2020-2021 在极客时间带领 3 个同事开发和维护极客时间官网的前端项目，作为核心开发者，参与了组件库的设计，XX 个组件测试覆盖率达到 80%，性能优化了 XX%。

2021 年 6 月至今，在极客时间负责开发极客时间后台管理系统，作为团队负责人，负责代码开发和 5 人团队的搭建，项目由 XX 和 XX 核心模块构成，通过引入 XX，提高了 XX% 的性能。

## 深入 TypeScript

### TypeScript 入门

- TypeScript 可以在 JavaScript 的基础上，对变量的数据类型加以限制。
- 当你不确定某个变量是什么类型时，你可以使用 any 作为这个变量的类型。
- 可以使用 enum 去定义枚举类型，这样可以把类型限制在指定的场景之内。
- 通过组合的方式组合出新的类型，最常见的组合方式就是使用 `|` 实现类型联合。
- 通过 interface 接口可以定义对象的类型限制。
- 函数的定义，参数和返回值本质上也是变量的概念，都可以进行类型的定义。
- 变量的方式去定义函数，直接使用 (参数类型) => 返回值类型的语法去定义 add1 的变量类型，但是这样写出来的代码可读性稍差一些，我更建议你使用 type 或者 interface 关键字去定义函数的类型

如果你的函数本来就支持多个类型的参数，下面的代码中 reverse 函数既支持数字也支持字符串。我们的要求是如果参数是数字，返回值也要是数字，参数是字符串返回值也只能是字符串，所以参数和返回值都用 number|string 就没法精确地限制这个需求。我们需要使用函数重载的方式，定义多个函数的输入值和返回值类型，更精确地限制函数的类型。

关于宿主环境里的类型，TypeScript 全部都给我们提供了，我们可以直接在代码中书写：Window 是 window 的类型，HTMLElement 是 dom 元素类型，NodeList 是节点列表类型，MouseEvent 是鼠标点击事件的类型……

除了浏览器的 API，我们还会用到很多第三方框架，比如 Vue、Element3 等等，这些框架现在都提供了完美的类型可以直接使用。在第 18 讲中我们使用下面的代码 Vue 导出的 Ref 来限定数据是 ref 包裹的响应式数据：

### 泛型

TypeScript 可以进行类型编程，这会极大提高 TypeScript 在复杂场景下的应用场景。

- keyof 可以帮助我们拆解已有类型
- extends 相当于 TypeScript 世界中的条件语句，然后 in 关键字可以理解为 TypeScript 世界中的遍历。
- `<T>` 让我们拥有了给函数的参数定义类型变量的能力，infer 则是可以在 extends 之后的变量设置类型变量，更加细致地控制类型。

## 一、课程导读篇

### 01. 宏观视角:从前端框架发展史聊聊为什么要学 Vue 3 ?

#### 前端三大框架

在前端 MVVM 模式下，不同框架的目标都是一致的，就是利用数据驱动页面，但是怎么处理数据的变化，各个框架走出了不同的路线。

这些框架要回答的核心问题就是，数据发生变化后，我们怎么去通知页面更新。各大框架在这个步骤上，各显神通：
Angular 1 就是最老套的脏检查。所谓的脏检查，指的是 Angular 1 在对数据变化的检查上，遵循每次用户交互时都检查一次数据是否变化，有变化就去更新 DOM 这一方法。这个方法看似简单粗暴，但算是数据驱动页面早期的实现，所以一经推出，就迅速占领了 MVVM 市场。
后面 Angular 团队自断双臂，完全抛弃 Angular 1，搞了一个全新的框架还叫 Angular，引入了 TypeScript、RxJS 等新内容，虽然这些设计很优秀，但是不支持向前兼容，抛弃了老用户。这样做也伤了一大批 Angular 1 用户的心，包括我。这也是 Angular 这个优秀的框架现在在国内没有大面积推广的原因。
而 Vue 1 的解决方案，就是使用响应式，初始化的时候，Watcher 监听了数据的每个属性，这样数据发生变化的时候，我们就能精确地知道数据的哪个 key 变了，去针对性修改对应的 DOM 即可，这一过程可以按如下方式解构：

在上图中，左边是实际的网页内容，我们在网页中使用`{{}}`渲染一个变量，Vue 1 就会在内容里保存一个监听器监控这个变量，我们称之为 Watcher，数据有变化，watcher 会收到通知去更新网页。
通俗来说，如果把网页数据看成你管理的员工，普通数据就是那种每次你都需要找到他，告诉他要怎么做的人，响应式数据就是他本身有任何变化，都会主动给你发日报告诉你的积极员工。
此外，Facebook 的 React 团队提出了不同于上面的 Angular、Vue 的的解决方案，他们设计了 React 框架，在页面初始化的时候，在浏览器 DOM 之上，搞了一个叫虚拟 DOM 的东西，也就是用一个 JavaScript 对象来描述整个 DOM 树。我们可以很方便的通过虚拟 DOM 计算出变化的数据，去进行精确的修改。
我们先看 React 中的一段代码：

```js
<div id="app">
  <p class="item">Item1</p>
  <div class="item">Item2</div>
</div>
```

在 React 中，这样一段 HTML 会被映射成一个 JavaScript 的对象进行描述。这个对象就像数据和实际 DOM 的一个缓存层，通过管理这个对象的变化，来减少对实际 DOM 的操作。
这种形式不仅让性能有个很好的保障，我们还多了一个用 JSON 来描述网页的工具，并且让虚拟 DOM 这个技术脱离了 Web 的限制。因为积累了这么多优势，虚拟 DOM 在小程序，客户端等跨端领域大放异彩。
虚拟 DOM 在运行的时候就是这么一个对象：

```js
{
  tag: "div",
  attrs: {
    id: "app"
  },
  children: [
    {
      tag: "p",
      attrs: { className: "item" },
      children: ["Item1"]
    },
    {
      tag: "div",
      attrs: { className: "item" },
      children: ["Item2"]
    }
  ]
}
```

这个对象完整地描述了 DOM 的树形结构，这样数据有变化的时候，我们生成一份新的虚拟 DOM 数据，然后再对之前的虚拟 DOM 进行计算，算出需要修改的 DOM，再去页面进行操作。
浏览器操作 DOM 一直都是性能杀手，而虚拟 DOM 的 Diff 的逻辑，又能够确保尽可能少的操作 DOM，这也是虚拟 DOM 驱动的框架性能一直比较优秀的原因之一。

#### Vue 与 React 框架的对比

通过上面对前端三大框架的介绍，我们不难发现 Vue 和 React 在数据发生变化后，在通知页面更新的方式上有明显的不同，通俗的来说，就是：在 Vue 框架下，如果数据变了，那框架会主动告诉你修改了哪些数据；而 React 的数据变化后，我们只能通过新老数据的计算 Diff 来得知数据的变化。
这两个解决方案都解决了数据变化后，如何通知页面更新的问题，并且迅速地获得了很高的占有率，但是他们都碰到了性能的瓶颈：

1. 对于 Vue 来说，它的一个核心就是“响应式”，也就是数据变化后，会主动通知我们。响应式数据新建 Watcher 监听，本身就比较损耗性能，项目大了之后每个数据都有一个 watcher 会影响性能。
2. 对于 React 的虚拟 DOM 的 Diff 计算逻辑来说，如果虚拟 DOM 树过于庞大，使得计算时间大于 16.6ms，那么就可能会造成性能的卡顿。
   为了解决这种性能瓶颈， Vue 和 React 走了不同的道路。
   React 为了突破性能瓶颈，借鉴了操作系统时间分片的概念，引入了 Fiber 架构。通俗来说，就是把整个虚拟 DOM 树微观化，变成链表，然后我们利用浏览器的空闲时间计算 Diff。一旦浏览器有需求，我们可以把没计算完的任务放在一旁，把主进程控制权还给浏览器，等待浏览器下次空闲。
   这种架构虽然没有减少运算量，但是巧妙地利用空闲实现计算，解决了卡顿的问题。你可以看一下我画的图解：

在上图中，左侧是一个树形结构，树形结构的 Diff 很难中断；右侧是把树形结构改造成了链表，遍历严格地按照子元素 -> 兄弟元素 -> 父元素的逻辑，随时可以中断和恢复 Diff 的计算过程。
为了方便你对计算 Diff 的理解，我们来看下面这张图：

这个图里两个虚线之间是浏览器的一帧，高性能的动画要求是 60fps，也就是 1 秒要渲染 60 次，每一帧的时间就是 16.6 毫秒，在这 16.6 毫秒里，浏览器自己的渲染更新任务执行后，会有一部分的空闲时间，这段时间我们就用来计算 Diff。
等到下一帧任务来了，我们就把控制权还给浏览器，让它继续去更新和渲染，等待空闲时间再继续计算，这样就不会导致卡顿。

Vue 1 的问题在于响应式数据过多，这样会带来内存占用过多的问题。所以 Vue 2 大胆引入虚拟 DOM 来解决响应式数据过多的问题。
这个解决方案使用虚拟 DOM 解决了响应式数据过多的内存占用问题，又良好地规避了 React 中虚拟 DOM 的问题， 还通过虚拟 DOM 给 Vue 带来了跨端的能力。看到这个解决方案的时候，我真是一拍大腿，直呼“真牛！”。
响应式数据是主动推送变化，虚拟 DOM 是被动计算数据的 Diff，一个推一个拉，它们看起来是两个方向的技术，但被 Vue 2 很好地融合在一起，采用的方式就是组件级别的划分。
对于 Vue 2 来说，组件之间的变化，可以通过响应式来通知更新。组件内部的数据变化，则通过虚拟 DOM 去更新页面。这样就把响应式的监听器，控制在了组件级别，而虚拟 DOM 的量级，也控制在了组件的大小。
这个方案也体现了 Vue 一直以来坚持的中庸的设计思想。
下图左边就是一个个的组件，组件内部是没有 Watcher 监听器的，而是通过虚拟 DOM 来更新，每个组件对应一个监听器，大大减小了监听器的数量。

除了响应式和虚拟 DOM 这个维度，Vue 和 React 还有一些理念和路线的不同，在模板的书写上，也走出了 template 和 JSX 两个路线。

React 的世界里只有 JSX，最终 JSX 都会在 Compiler 那一层，也就是工程化那里编译成 JS 来执行，所以 React 最终拥有了全部 JS 的动态性，这也导致了 React 的 API 一直很少，只有 state、hooks、Component 几个概念，主要都是 JavaScript 本身的语法和特性。
而 Vue 的世界默认是 template，也就是语法是限定死的，比如 v-if 和 v-for 等语法。有了这些写法的规矩后，我们可以在上线前做很多优化。Vue 3 很优秀的一个点，就是在虚拟 DOM 的静态标记上做到了极致，让静态的部分越过虚拟 DOM 的计算，真正做到了按需更新，很好的提高了性能。

在模板的书写上，除了 Vue 和 React 走出的 template 和 JSX 两个路线，还出现了 Svelte 这种框架，没有虚拟 DOM 的库，直接把模板编译成原生 DOM，几乎没有 Runtime，所有的逻辑都在 Compiler 层优化，算是另外一个极致。

### 02. 上手: 一个清单应用带你入门 Vue.js

计算属性全选框功能

```html
<div>
  全选<input type="checkbox" v-model="allDone" />
  <span> {{active}} / {{all}} </span>
</div>
<script>
  computed:{
    active(){
      return this.todos.filter(v=>!v.done).length
    },
    all(){
      return this.todos.length
    },
    allDone: {
        get: function () {
          return this.active === 0
        },
        set: function (val) {
          this.todos.forEach(todo=>{
            todo.done = val
          });
        }
    }
  }
</script>
```

### 03. 新特性:初探 Vue 3 新特性

Vue 2 的核心模块和历史遗留问题

1. 开发维护，使用停止维护的 Flow.js 来做类型校验；
2. 社区二次维护困难，内部运行时执行浏览器 API 导致跨端方案出现问题；
3. 响应式不是真正意义上的代理，知识利用 defineProperty 进行属性拦截；
4. Option API 在组织代码中不易维护，对 TS 的类型推导不友好；

从七个方面了解 Vue 3 新特性

1. Vue 团队开发的工作方式：RFC 机制；
2. 响应式机制使用 Proxy 代理代替 define Property 拦截；
3. 自定义渲染器，使用 monorepo 管理方式，渲染的逻辑也拆成了平台无关渲染逻辑和浏览器渲染 API 两部分；
4. 全部模块使用 TypeScript 重构，给系统带来更方便的提示和让代码更健壮；
5. Composition API 组合语法，对 Tree- shaking 友好，代码方便复用；
6. 内置了 Fragment/Teleport/Suspense 新组建；
7. 新一代工程化工具 Vite；

### 04. 升级:Vue2 项目如何升级到 Vue3?

Vue 3 的 Composition API 带来的代码组织方式更利于封装代码，维护起来也不会上下横跳。

Vue 3 也不是没有问题，由于新的响应式系统用了 Proxy，会存在兼容性问题。

## 二、基础入门篇

### 05. 项目启动:搭建 Vue 3 工程化项目第一步

```
Vue 3 项目
VS Code编辑器   Chrome浏览器
Volar语法提示   Devtools调试工具
CSS 预处理  网络请求    Element3 组件库
Vuex 管理数据   Vue 3   vue-router 路由
Vite 工程化     代码规范/研发规范
Node.js
单元测试   发布部署
```

### 06. 新的代码组织方式: Composition API + script setup 到底好在哪里?

开发上手

1. 使用单文件组件 vue 文件，支持将组件的 HTML、CSS 和 JavaScript 写在单个文件内容中；
2. 对于 ref 返回的响应式数据，我们需要修改 `.value` 才能生效，而在 `<script setup>` 标签内定义的变量和函数，都可以在模板中直接使用；
3. script setup 自动把 import 引入的组件注册到当前组件中；
4. 计算属性和生命周期等功能，都可以脱离 Vue 的组件机制单独使用；
5. script setup 可以让代码变得更加精简和高效；

style 样式的特性

1. 添加 scoped 属性避免样式冲突问题；
2. 全局的样式可以使用 `:global` 来标记；
3. 通过 v-bind 函数直接在 CSS 中使用 JavaScript 中的变量；

### 07. 巧妙的响应式:深入理解 Vue 3 的响应式机制

JavaScript 里面的变量是没有响应式的概念的，代码自上而下执行。

#### 响应式原理

Vue 中用过三种响应式解决方案：defineProperty/Proxy/value setter。

defineProperty 在对象的属性中实现了拦截，读取属性的时候执行 get 函数，修改属性时执行 set 函数。单语法也有一些缺陷，删除属性并不会触发 set 函数。

Proxy 是针对对象来监听，而不是针对某个具体属性，所以不仅可以代理那些定义时不存在的属性，还可以代理更丰富的数据结构，比如 Map/Set 等。Vue 3 的 reactive 函数可以把一个对象变成响应式数据，而 reactive 就是基于 Proxy 实现的，还可以通过 watchEffect 执行代理的副作用。

Vue3 中还有另外一个响应式实现的逻辑，就是利用对象的 get 和 set 函数来进行监听。这种响应式的实现方式，只能拦截某一个属性的修改，这也是 Vue3 中 ref 这个 API 的实现。

| 实现原理       | 实际场景       | 优势                      | 劣势                     | 实际应用           |
| -------------- | -------------- | ------------------------- | ------------------------ | ------------------ |
| defineProperty | Vue 2 响应式   | 兼容性                    | 数组和属性删除等拦截不了 | Vue 2              |
| Proxy          | Vue 3 reactive | 基于 Proxy 实现真正的拦截 | 兼容不了 IE11            | Vue 3 复杂数据结构 |
| value setter   | Vue 3 ref      | 实现简单                  | 只拦截了 value 属性      | Vue 3 简单数据结构 |

定制响应式数据

watchEffect 函数可以在数据变化之后执行指定的函数。

Vueuse 工具包

封装更多的类似 useStorage 函数的其他 use 类型的函数，把实际开发中你用到的任何数据或者浏览器属性，都封装成响应式数据，这样就可以极大地提高我们的开发效率。Vue 社区中其实已经有一个类似的工具集合，也就是 [VueUse](https://vueuse.org/)，它把开发中常见的属性都封装成为响应式函数。

### 08. 组件化:如何像搭积木一样开发网页?

除了浏览器自带的组件外，Vue 还允许我们自定义组件，把一个功能的模板（template）封装在一个.vue 文件中。例如在下图中，我们把每个组件的逻辑和样式，也就是把 JavaScript 和 CSS 封装在一起，方便在项目中复用整个组件的代码。

Vue 已经把组件化的机制实现得很好了，你只需要在这个基础之上，去掌握和学习组件化在使用上的设计理念。这样做的目的是实现高效的代码复用，在后续的项目开发中，我们会把组件分成两个类型，一个是通用型组件，一个是业务型组件。

组件的开发由于要考虑代码的复用性，会比通常的业务开发要求更高，需要有更好的可维护性和稳定性的要求。

在 Vue 中，我们使用 emit 来对外传递事件，这样父元素就可以监听组件内部的变化。

对于自定义组件来说，v-model 是传递属性和接收组件事件两个写法的简写。

在 Vue 中直接使用 slot 组件来显示组件的子元素，也就是所谓的插槽。

### 09. 动画: Vue 中如何实现动画效果?

#### 前端过渡和动效

1. 通过一个 CSS 的属性 transition 来实现过渡；
2. 可以通过 animation 和 keyframe 的组合实现动画；

#### Vue 3 动画入门

Vue 3 中提供了一些动画的封装，使用内置的 transition 组件来控制组件的动画。

标签在进入和离开的时候，会有 fade-enter-active 和 fade-leave-active 的 class，进入的开始和结束会有 fade-enter-from 和 face-enter-to 两个 class。

#### 列表动画

在 Vue 中，我们把这种需求称之为列表过渡。因为 transition 组件会把子元素作为一个整体同时去过渡，所以我们需要一个新的内置组件 transition-group。在 v-for 渲染列表的场景之下，我们使用 transition-group 组件去包裹元素，通过 tag 属性去指定渲染一个元素。

#### 页面切换动画

如果要在路由组件上使用转场，并且对导航进行动画处理，你就需要使用 v-slot API。我们来到 src/App.vue 组件中，因为之前 router-view 没有子元素，所以我们要对代码进行修改。

#### JavaScript 动画

具体怎么做呢？ 在 Vue 的 transition 组件里，我们可以分别设置 before-enter，enter 和 after-enter 三个函数来更精确地控制动画。
在下面的代码中，我们首先定义了 animate 响应式对象来控制动画元素的显示和隐藏，并且用 transition 标签包裹动画元素。在 beforeEnter 函数中，通过 getBoundingClientRect 函数获取鼠标的点击位置，让动画元素通过 translate 属性移动到鼠标所在位置；并且在 enter 钩子中，把动画元素移动到初始位置，在 afterEnter 中，也就是动画结束后，把动画元素再隐藏起来，这样就实现了类似购物车的飞入效果。

## 三、全家桶实战篇

### 10. 数据流:如何使用 Vuex 设计你的数据流

使用 createStore 来创建一个数据存储，我们称之为 store。
store 内部除了数据，还需要一个 mutation 配置去修改数据，你可以把这个 mutation 理解为数据更新的申请单，mutation 内部的函数会把 state 作为参数，我们直接操作 state.count 就可以完成数据的修改。

对于一个数据，如果只是组件内部使用就是用 ref 管理；如果我们需要跨组件，跨页面共享的时候，我们就需要把数据从 Vue 的组件内部抽离出来，放在 Vuex 中去管理。

Vuex 就是一个公用版本的 ref，提供响应式数据给整个项目使用。

在 Vuex 中，mutation 的设计就是用来实现同步地修改数据。如果数据是异步修改的，我们需要一个新的配置 action。

#### 下一代 Vuex

Vuex 由于在 API 的设计上，对 TypeScript 的类型推导的支持比较复杂，用起来很是痛苦。因为我们的项目一直用的都是 JavaScript，你可能感触并不深，但对于使用 TypeScript 的用户来说，Vuex 的这种问题是很明显的。
为了解决 Vuex 的这个问题，Vuex 的作者最近发布了一个新的作品叫 Pinia，并将其称之为下一代的 Vuex。Pinia 的 API 的设计非常接近 Vuex5 的提案，首先，Pinia 不需要 Vuex 自定义复杂的类型去支持 TypeScript，天生对类型推断就非常友好，并且对 Vue Devtool 的支持也非常好，是一个很有潜力的状态管理框架。

### 11. 路由:新一代 vue-router 带来什么变化?

#### 前后端开发模式的演变

在 jQuery 时代，对于大部分 Web 项目而言，前端都是不能控制路由的，而是需要依赖后端项目的路由系统。通常，前端项目也会部署在后端项目的模板里，整个项目执行的示意图如下：

前端依赖后端，并且前端不需要负责路由的这种开发方式，有很多的优点，比如开发速度会很快、后端也可以承担部分前端任务等，所以到现在还有很多公司的内部管理系统是这样的架构。当然，这种开发方式也有很多缺点，比如前后端项目无法分离、页面跳转由于需要重新刷新整个页面、等待时间较长等等，所以也会让交互体验下降。

用户访问路由后，无论是什么 URL 地址，都直接渲染一个前端的入口文件 index.html，然后就会在 index.html 文件中加载 JS 和 CSS。之后，JavaScript 获取当前的页面地址，以及当前路由匹配的组件，再去动态渲染当前页面即可。用户在页面上进行点击操作时，也不需要刷新页面，而是直接通过 JS 重新计算出匹配的路由渲染即可。

通过 JavaScript 动态控制数据去提高用户体验的方式并不新奇，Ajax 让数据的获取不需要刷新页面，SPA 应用让路由跳转也不需要刷新页面。这种开发的模式在 jQuery 时代就出来了，浏览器路由的变化可以通过 pushState 来操作，这种纯前端开发应用的方式，以前称之为 Pjax （pushState+ Ajax）。之后，这种开发模式在 MVVM 框架的时代大放异彩，现在大部分使用 Vue/React/Angular 的应用都是这种架构。
SPA 应用相比于模板的开发方式，对前端更加友好，比如：前端对项目的控制权更大了、交互体验也更加丝滑，更重要的是，前端项目终于可以独立出来单独部署了。

#### 前端路由的实现原理

在讲完前端路由的执行逻辑之后，我们深入探索一下前端控制路由的实现原理。
现在，通过 URL 区分路由的机制上，有两种实现方式，一种是 hash 模式，通过 URL 中 # 后面的内容做区分，我们称之为 hash-router；另外一个方式就是 history 模式，在这种方式下，路由看起来和正常的 URL 完全一致。
这两个不同的原理，在 vue-router 中对应两个函数，分别是 createWebHashHistory 和 createWebHistory。

hash 模式

类似于服务端路由，前端路由实现起来其实也很简单，就是匹配不同的 URL 路径，进行解析，然后动态地渲染出区域 HTML 内容。但是这样存在一个问题，就是 URL 每次变化的时候，都会造成页面的刷新。解决这一问题的思路便是在改变 URL 的情况下，保证页面的不刷新。

之后，在进行页面跳转的操作时，hash 值的变化并不会导致浏览器页面的刷新，只是会触发 hashchange 事件。在下面的代码中，通过对 hashchange 事件的监听，我们就可以在 fn 函数内部进行动态地页面切换。

history 模式

2014 年之后，因为 HTML5 标准发布，浏览器多了两个 API：pushState 和 replaceState。通过这两个 API ，我们可以改变 URL 地址，并且浏览器不会向后端发送请求，我们就能用另外一种方式实现前端路由。
在下面的代码中，我们监听了 popstate 事件，可以监听到通过 pushState 修改路由的变化。并且在 fn 函数中，我们实现了页面的更新操作。

#### 手写迷你 vue-router

在代码中，我们首先实现了用 Router 类去管理路由，并且，我们使用 createWebHashHistory 来返回 hash 模式相关的监听代码，以及返回当前 URL 和监听 hashchange 事件的方法；然后，我们通过 Router 类的 install 方法注册了 Router 的实例，并对外暴露 createRouter 方法去创建 Router 实例；最后，我们还暴露了 useRouter 方法，去获取路由实例。

下一步，我们需要注册两个内置组件 router-view 和 router-link。在 createRouter 创建的 Router 实例上，current 返回当前的路由地址，并且使用 ref 包裹成响应式的数据。router-view 组件的功能，就是 current 发生变化的时候，去匹配 current 地址对应的组件，然后动态渲染到 router-view 就可以了。

### 12. 调试:提高开发效率必备的 Vue Devtools

Vue Devtools 可以算是一个 Elements 页面的 Vue 定制版本，调试页面左侧的显示内容并不是 HTML，而是 Vue 的组件嵌套关系。我们可以从中清晰地看到整个项目中最外层的 App 组件，也能看到 App 组件内部的 RouterView 下面的 Todo 组件。

并且，在调试页面的左侧中，当我们点击组件的时候，我们所调试的前端页面中也会高亮清单组件的覆盖范围。调试页面的右侧则显示着 todo 组件内部所有的数据和方法。我们可以清晰地看到 setup 配置下，有 todos、animate、active 等诸多变量，并且这些变量也是和页面实时同步的数据，我们在页面中输入新的清单后，可以看到 active 和 all 的数据也随之发生了变化。

同时，我们也可以直接修改调试窗口里面的数据，这样，正在调试的前端页面也会同步数据的显示效果。有了 Vue 的调试页面，当我们碰到页面中的数据和标签不同步的情况时，就可以很轻松地定位出是哪里出现了问题。
然后在 Component 的下拉框那里，我们还可以选择 Vuex 和 Router 页面，分别用来调试 Vuex 和 vue-router。

这里还有一个小技巧，你可以了解一下：在 Components 页面下，你选中一个组件后，调试窗口的右侧就会出现 4 个小工具。
如下图所示，在我用红框标记的四个工具中，最右边的那个工具可以让你直接在编辑器里打开这个代码。这样，调试组件的时候就不用根据路径再去 VS Code 里搜索代码文件了，这算是一个非常好用的小功能。

### 13. JSX:如何利用 JSX 应对更灵活的开发场景?

实际上，Vue 中不仅有 JSX，而且 Vue 还借助 JSX 发挥了 Javascript 动态化的优势。此外，Vue 中的 JSX 在组件库、路由库这类开发场景中，也发挥着重要的作用。

#### h 函数

在 Vue 3 的项目开发中，template 是 Vue 3 默认的写法。虽然 template 长得很像 HTML，但 Vue 其实会把 template 解析为 render 函数，之后，组件运行的时候通过 render 函数去返回虚拟 DOM，你可以在 Vue Devtools 中看到组件编译之后的结果。

调试窗口右侧代码中的 `_sfc_render_` 函数就是清单应用的 template 解析成 JavaScript 之后的结果。所以除了 template 之外，在某些场景下，我们可以直接写 render 函数来实现组件。

我们使用 defineComponent 定义一个组件，组件内部配置了 props 和 setup。这里的 setup 函数返回值是一个函数，就是我们所说的 render 函数。render 函数返回 h 函数的执行结果，h 函数的第一个参数就是标签名，我们可以很方便地使用字符串拼接的方式，实现和上面代码一样的需求。像这种连标签名都需要动态处理的场景，就需要通过手写 h 函数来实现。

手写的 h 函数，可以处理动态性更高的场景。但是如果是复杂的场景，h 函数写起来就显得非常繁琐，需要自己把所有的属性都转变成对象。并且组件嵌套的时候，对象也会变得非常复杂。不过，因为 h 函数也是返回虚拟 DOM 的，所以有没有更方便的方式去写 h 函数呢？答案是肯定的，这个方式就是 JSX。

#### JSX 是什么

在 JavaScript 里面写 HTML 的语法，就叫做 JSX，算是对 JavaScript 语法的一个扩展。上面的代码直接在 JavaScript 环境中运行时，会报错。JSX 的本质就是下面代码的语法糖，h 函数内部也是调用 createVnode 来返回虚拟 DOM。

#### JSX 和 Template

而 JSX 只是 h 函数的一个语法糖，本质就是 JavaScript，想实现条件渲染可以用 if else，也可以用三元表达式，还可以用任意合法的 JavaScript 语法。也就是说，JSX 可以支持更动态的需求。而 template 则因为语法限制原因，不能够像 JSX 那样可以支持更动态的需求。这是 JSX 相比于 template 的一个优势。

JSX 相比于 template 还有一个优势，是可以在一个文件内返回多个组件。

相比于我们自己去写 h 函数，在 template 解析的结果中，有以下几个性能优化的方面。

首先，静态的标签和属性会放在 \_hoisted 变量中，并且放在 render 函数之外。这样，重复执行 render 的时候，代码里的 h1 这个纯静态的标签，就不需要进行额外地计算，并且静态标签在虚拟 DOM 计算的时候，会直接越过 Diff 过程。

然后是 @click 函数增加了一个 cache 缓存层，这样实现出来的效果也是和静态提升类似，尽可能高效地利用缓存。最后是，由于在下面代码中的属性里，那些带冒号的属性是动态属性，因而存在使用一个数字去标记标签的动态情况。

template 由于语法固定，可以在编译层面做的优化较多，比如静态标记就真正做到了按需更新；而 JSX 由于动态性太强，只能在有限的场景下做优化，虽然性能不如 template 好，但在某些动态性要求较高的场景下，JSX 成了标配，这也是诸多组件库会使用 JSX 的主要原因。

### 14. TypeScript: Vue 3 中如何使用 TypeScript

TypeScript 是微软开发的 JavaScript 的超集，这里说的超集，意思就是 TypeScript 在语法上完全包含 JavaScript。TypeScript 的主要作用是给 JavaScript 赋予强类型的语言环境。现在大部分的开源项目都是用 TypeScript 构建的，并且 Vue 3 本身 TS 的覆盖率也超过了 95%。

只要是不符合接口规定的类型的变量，就会直接在变量下方给出红色波浪线的报错提示。鼠标移到报错的变量那里，就会有提示信息弹出，直接通知你哪里出问题了。这也是为什么现在大部分前端开源项目都使用 TypeScript 构建的原因，因为每个函数的参数、返回值的类型和属性都清晰可见，这就可以极大地提高我们代码的可维护性和开发效率。

#### 进阶用法

1. 泛型。在函数名的后面用尖括号包裹一个类型占位符；
2. 递归类型。可以书写更复杂的类型组合；

#### Vue3 中的 TypeScript

Vue 2 中全部属性都挂载在 this 之上，而 this 可以说是一个黑盒子，我们完全没办法预先知道 this 上会有什么数据，这也是为什么 Vue 2 对 TypeScript 的支持一直不太好的原因。

使用 Composition API 的过程中，可以针对 ref 或者 reactive 进行类型推导。如果 ref 包裹的是数字，那么在对 `count.value` 进行 split 函数操作的时候，TypeScript 就可以预先判断 `count.value` 是一个数字，并且进行报错提示。

可以显式地去规定 ref、reactive 和 computed 输入的属性，ref、reactive 和 computed 限制类型的写法，每个函数都可以使用默认的参数推导，也可以显式地通过泛型去限制。

在 Vue 中，除了组件内部数据的类型限制，还需要对传递的属性 Props 声明类型。而在 `<script setup>` 语法中，只需要在 defineProps 和 defineEmits 声明参数类型就可以了。

#### TypeScript 和 JavaScript 的平衡

TypeScript 是 JavaScript 的一个超集，这两者并不是完全对立的关系。所以，学习 TypeScript 和学习 JavaScript 不是二选一的关系，你需要做的，是打好坚实的 JavaScript 的基础，在维护复杂项目和基础库的时候选择 TypeScript。

TypeScript 最终还是要编译成为 JavaScript，并在浏览器里执行。对于浏览器厂商来说，引入类型系统的收益并不太高，毕竟编译需要时间。而过多的编译时间，会影响运行时的性能，所以未来 TypeScript 很难成为浏览器的语言标准。

### 15. 实战痛点 1:复杂 Vue 项目的规范和基础库封装

在项目开发中，我们首先需要一个组件库帮助我们快速搭建项目，组件库提供了各式各样的封装完备的组件。现在社区可选择的组件库有 element-plus、antd-vue，Naive-UI、Element3 等。

完成页面基本结构的搭建后，在我们获取后端数据时，需要使用 axios 发起网络请求。

在项目里集成 CSS 预编译器，CSS 预编译器可以帮我们更快、更高效地管理和编写 CSS 代码。

由于个人习惯的不同，每个人写代码的风格也略有不同。比如在写 JavaScript 代码中，有些人习惯在每行代码之后都写分号，有些人习惯不写分号。但是团队产出的项目就需要有一致的风格，这样代码在团队之间阅读起来时，也会更加流畅。ESLint 就是专门用来做规范团队代码的一个库。

### 16. 实战痛点 2:项目开发中的权限系统

#### 登录权限

HTTP 的 Request Headers 里就有 Cookie 这个数据，这是浏览器自动管理和发送的，也算是权限认证的最佳方案之一。

在现在这种前后端分离的场景下，通常前后端项目都会部署在不同的机器和服务器之上，Cookie 在跨域上有诸多的限制。所以在这种场景下，我们更愿意手动地去管理权限，于是就诞生了现在流行的基于 token 的权限解决方案，你也可以把 token 理解为我们手动管理的 cookie。

权限系统中还有一个常见的问题，就是登录是有时间限制的。token 的过期时间认证是由后端来实现和完成的。如果登录状态过期，那么会有一个单独的报错信息，我们需要在接口拦截函数中，统一对接口的响应结果进行拦截。如果报错信息显示的是登录过期，我们需要清理所有的 token 和页面权限数据，并且跳转到登录页面。

#### 角色权限

我们通常使用的权限解决方案就是 RBAC 权限管理机制。每个用户有不同的角色，每个角色对应不同的页面权限，这个数据结构的关系设计主要是由后端来实现。

关于这部分动态路由的内容，官网的文档中有详细的 API 介绍。在下面的代码中，我们在 Vuex 中注册 addRoute 这个 action，通过后端返回的权限页面数据，调用 router.addRoute 新增路由。

与新增路由对应，在页面重新设置权限的时候，我们需要用 router.removeRoute 来删除注册的路由，这也是上面的代码中我们还有一个 remoteRoutes 来管理动态路由的原因。

然后，我们需要把动态路由的状态存储在本地存储里，否则刷新页面之后，动态的路由部分就会被清空，页面就会显示 404 报错。我们需要在 localStorage 中把静态路由和动态路由分开对待，在页面刷新的时候，通过 src/router/index.js 入口文件中的 routes 配置，从 localStorage 中获取完整的路由信息，并且新增到 vue-router 中，才能加载完整的路由。

### 17. 实战痛点 3: Vue 3 中如何集成第三方框架

1. 独立的第三方库

axios 这种相对独立的工具对于我们项目来说，引入的难度非常低。通常来说，使用这种独立的框架需要以下两步。

第一步是，我们先进入到项目根目录下，使用下面的命令去安装。

第二步，就是在需要使用的地方进行 import 的相关操作，比如在页面跳转的时候。

2. 组件的封装

template 设置了一个普通的 div 作为容器，通过 mount 和 onUnmounted 生命周期内部去初始化图表，实现 ECharts 框架中图表的渲染和清理，然后 initChart 内部使用 echart 的 API 进行渲染，这样就实现了图表的渲染。

3. 指令的封装

指令的生命周期和组件类似，首先我们要让指令能够支持 Vue 的插件机制，所以我们需要在 install 函数内注册 lazy 指令。这种实现 Vue 插件的方式，在 vuex 和 vue-router 两讲中已经带你学习过了，这里的代码里我们使用 install 方法，在 install 方法的内部去注册 lazy 指令，并且实现了 mounted、updated、unmounted 三个钩子函数。

### 18. 实战痛点 4:Vue3 项目中的性能优化

下面，我们会先从 Vue 项目在整体上的执行流程谈起，然后详细介绍性能优化的两个重要方面：网络请求优化和代码效率优化。不过，在性能优化之外，用户体验才是性能优化的目的，所以我也会简单谈一下用户体验方面的优化项。最后，我还会通过性能监测报告，为你指引出性能优化的方向。

#### 用户输入 URL 到页面显示的过程

简单来说，就是用户在输入 URL 并且敲击回车之后，浏览器会去查询当前域名对应的 IP 地址。对于 IP 地址来说，它就相当于域名后面的服务器在互联网世界的门牌号。然后，浏览器会向服务器发起一个网络请求，服务器会把浏览器请求的 HTML 代码返回给浏览器。

之后，浏览器会解析这段 HTML 代码，并且加载 HTML 代码中需要加载的 CSS 和 JavaScript，然后开始执行 JavaScript 代码。进入到项目的代码逻辑中，可以看到 Vue 中通过 vue-router 计算出当前路由匹配的组件，并且把这些组件显示到页面中，这样我们的页面就完全显示出来了。而我们性能优化的主要目的，就是让页面显示过程的时间再缩短一些。

#### 网络请求优化

对于前端来说，可以优化的点，首先就是在首页的标签中，使用标签去通知浏览器对页面中出现的其他域名去做 DNS 的预解析，比如页面中的图片通常都是放置在独立的 CDN 域名下，这样页面加载首页的时候就能预先解析域名并把结果缓存起来 。

项目在整体流程中，会通过 HTTP 请求加载很多的 CSS、JavaScript，以及图片等静态资源。为了让这些文件在网络加载中更快，我们可以从后面这几方面入手进行优化。

首先，浏览器在获取网络文件时，需要通过 HTTP 请求，HTTP 协议底层的 TCP 协议每次创建链接的时候，都需要三次握手，而三次握手会造成额外的网络损耗。如果浏览器需要获取的文件较多，那就会因为三次握手次数过多，而带来过多网络损耗的问题。

所以，首先我们需要的是让文件尽可能地少，这就诞生出一些常见的优化策略，比如先给文件打包，之后再上线；使用 CSS 雪碧图来进行图片打包等等。文件打包这条策略在 HTTP2 全面普及之前还是有效的，但是在 HTTP2 普及之后，多路复用可以优化三次握手带来的网络损耗。关于 HTTP2 的更多内容，你可以去搜索相关文章自行学习。

其次，除了让文件尽可能少，我们还可以想办法让这些文件尽可能地小一些，因为如果能减少文件的体积，那文件的加载速度自然也就会变快。这一环节也诞生出一些性能优化策略，比如 CSS 和 JavaScript 代码会在上线之前进行压缩；在图片格式的选择上，对于大部分图片来说，需要使用 JPG 格式，精细度要求高的图片才使用 PNG 格式；优先使用 WebP 等等。也就是说，尽可能在同等像素下，选择体积更小的图片格式。

在性能优化中，懒加载的方式也被广泛使用。图片懒加载的意思是，我们可以动态计算图片的位置，只需要正常加载首屏出现的图片，其他暂时没出现的图片只显示一个占位符，等到页面滚动到对应图片位置的时候，再去加载完整图片。

除了图片，项目中也会做路由懒加载，现在项目打包后，所有路由的代码都在首页一起加载。但是，我们也可以把不常用的路由单独打包，在用户访问到这个路由的时候再去加载代码。下面的代码中，vue-router 也提供了懒加载的使用方式，只有用户访问了 `/course/:id` 这个页面后，对应页面的代码才会加载执行。

这些文件如何才能高效复用呢？我们需要做的，就是尽可能高效地利用浏览器的缓存机制，在文件内容没有发生变化的时候，做到一次加载多次使用，项目中如果成功复用一个几百 KB 的文件，对于性能优化来说是一个巨大的提升。

浏览器的缓存机制有好几个 Headers 可以实现，Expires、Cache-control，last-modify、etag 这些缓存相关的 Header 可以让浏览器高效地利用文件缓存。我们需要做的是，只有当文件的内容修改了，我们才会重新加载文件。这也是为什么我们的项目执行 npm run build 命令之后，静态资源都会带上一串 Hash 值，因为这样确保了只有文件内容发生变化的时候，文件名才会发生变化，其他情况都会复用缓存。

#### 代码效率优化

在浏览器加载网络请求结束后，页面开始执行 JavaScript，因为 Vue 已经对项目做了很多内部的优化，所以在代码层面，我们需要做的优化并不多。很多 Vue 2 中的性能优化策略，在 Vue 3 时代已经不需要了，我们需要做的就是遵循 Vue 官方的最佳实践，其余的交给 Vue 自身来优化就可以了。

比如 computed 内置有缓存机制，比使用 watch 函数好一些；组件里也优先使用 template 去激活 Vue 内置的静态标记，也就是能够对代码执行效率进行优化；v-for 循环渲染一定要有 key，从而能够在虚拟 DOM 计算 Diff 的时候更高效复用标签等等。然后就是 JavaScript 本身的性能优化，或者说某些实现场景算法的选择了，这里需要具体问题具体分析，在通过性能监测工具发现代码运行的瓶颈后，我们依次对耗时过长的函数进行优化即可。

#### 用户体验优化

性能优化的主要目的，还是为了能让用户在浏览网页的时候感觉更舒服，所有有些场景我们不能只考虑单纯的性能指标，还要结合用户的交互体验进行设计，必要的时候，我们可以损失一些性能去换取交互体验的提升。

比如用户加载大量图片的同时，如果本身图片清晰度较高，那直接加载的话，页面会有很多图一直是白框。所以我们也可以预先解析出图片的一个模糊版本，加载图片的时候，先加载这个模糊的图作为占位符，然后再去加载清晰的版本。虽然额外加载了图片文件，但是用户在体验上得到了提升。

类似的场景还有很多，比如用户上传文件的时候，如果文件过大，那么上传可能就会很耗时。而且一旦上传的过程中发生了网络中断，那上传就前功尽弃了。

为了提高用户的体验，我们可以选择断点续传，也就是把文件切分成小块后，挨个上传。这样即使中间上传中断，但下次再上传时，只上传缺失的那些部分就可以了。可以看到，断点上传虽然在性能上，会造成网络请求变多的问题，但也极大地提高了用户上传的体验。

还有很多组件库也会提供骨架图的组件，能够在页面还没有解析完成之前，先渲染一个页面的骨架和 loading 的状态，这样用户在页面加载的等待期就不至于一直白屏，下图所示就是 antd-vue 组件库骨架图渲染的结果。

#### 性能监测报告

在第 12 讲学习 Vue Devtools 的时候，我们已经使用 Chrome 的性能监测工具 Lighthouse 对极客时间的官网做了一次性能的评估，我们可以在这里看到评测报告。并且，我们也对如何在调试窗口的 Performance 页面中进行性能监控，给出了演示。为了方便你理解，我们在这里也解释一下 FCP、TTI 和 LCP 这几个关键指标的含义。

首先是 First Contentful Paint，通常简写为 FCP，它表示的是页面上呈现第一个 DOM 元素的时间。在此之前，页面都是白屏的状态；然后是 Time to interactive，通常简写为 TTI，也就是页面可以开始交互的时间；还有和用户体验相关的 Largest Contentful Paint，通常简写为 LCP，这是页面视口上最大的图片或者文本块渲染的时间，在这个时间，用户能看到渲染基本完成后的首页，这也是用户体验里非常重要的一个指标。

我们还可以通过代码中的 performance 对象去动态获取性能指标数据，并且统一发送给后端，实现网页性能的监控。性能监控也是大型项目必备的监控系统之一，可以获取到用户电脑上项目运行的状态。

### 19. 实战痛点 5:如何打包发布你的 Vue 3 应用?

代码部署难点

现在前端所处的时代，我们主要会面临后面这些代码部署难点：首先是，如何高效地利用项目中的文件缓存；然后是，如何能够让整个项目的上线部署过程自动化，尽可能避免人力的介入，从而提高上线的稳定性；最后，项目上线之后，如果发现有重大 Bug，我们就要考虑如何尽快回滚代码。

项目上线前的自动化部署

首先，我们需要一台独立的机器去进行打包和构建的操作，这台机器需要独立于所有开发环境，这样做是为了保证打包环境的稳定；之后，在部署任务启动的时候，我们需要拉取远程的代码，并且切换到需要部署的分支，然后锁定 Node 版本进行依赖安装、单元测试、ESLint 等代码检查工作；最后，在这台机器上，执行经过编译产出的打包后的代码，并打包上传代码到 CDN 和静态服务器。当然了，完成这些操作之后，还要能通过脚本自动通过内部沟通软件通知团队项目构建的结果。

项目上线后的自动化部署

为了解决上面说到的这些问题，我们需要一种机制，能够让我们在发现问题之后，尽快地将版本进行回滚，并且在回滚的操作过程中，尽可能不需要人力的介入。所以，我们需要静态资源的版本管理，具体来说，就是让每个历史版本的资源都能保留下来，并且有一个唯一的版本号，如果发生了故障，能够瞬间切换版本。这个过程由具体的代码实现之后，我们只需要点击回滚的版本号，系统就会自动恢复到上线前的版本。

在这种机制下，如果你的业务流量特别大，每秒都有大量用户访问和使用，那么直接全量上线的操作就会被禁止。为了减少上线时，部署操作对用户造成的影响，我们需要先选择一部分用户去做灰度测试，也就是说，上线后的项目的访问权限，暂时只对这些用户开放。或者，你也可以做一些 AB 测试，比如给北京的同学推送 Vue 课，给上海的同学推荐 React 课等等。我们需要做的，就是把不同版本的代码分开打包，互不干涉。之后，我们再设计部署的机器和机房去适配不同的用户。

## 四、Vue 3 进阶开发篇

### 20. 组件库:如何设计你自己的通用组件库?

首先安装和初始化了 husky，然后我们使用 npx husky add 命令新增了 commit-msg 钩子，husky 会在我们执行 git commit 提交代码的时候执行 node scripts/verifyCommit 命令来校验 commit 信息格式。

开发组件库的时候，我们要确保每个组件都有自己的名字，script setup 中没法返回组件的名字，所以我们需要一个单独的标签，使用 options 的语法设置组件的 name 属性。

使用插件机制对外暴露安装的接口，对外暴露了一个对象，对象的 install 方法中，使用 `app.component` 注册这五个组件。

### 21. 单元测试:如何使用 TDD 开发一个组件?

单元测试（Unit Testing），是指对软件中的最小可测试单元进行检查和验证，这是百度百科对单元测试的定义。而我的理解是，在我们日常代码开发中，会经常写 Console 来确认代码执行效果是否符合预期，这其实就算是测试的雏形了，我们把代码中的某个函数或者功能，传入参数后，校验输出是否符合预期。

我们选择 Facebook 出品的 Jest 作为我们组件库的测试代码，Jest 是现在做测试的最佳选择了，因为它内置了断言、测试覆盖率等功能。

然后，我们还需要新建 `jest.config.js`，用来配置 jest 的测试行为。不同格式的文件需要使用不同命令来配置，对于 `.vue` 文件我们使用 vue-jest，对于 `.js` 或者 `.jsx` 结果的文件，我们就要使用 babel-jest，而对于 `.ts` 结尾的文件我们使用 ts-jest，然后匹配文件名是 `xx.spect.js`。这里请注意，Jest 只会执行 `.spec.js` 结尾的文件。

### 22. 表单:如何设计一个表单组件?

表单组件
在 Element 表单组件的页面里，我们能看到表单种类的组件类型有很多，我们常见的输入框、单选框和评分组件等都算是表单组件系列的。
下面这段代码是 Element3 官方演示表单的 Template，整体表单页面分三层：
el-form 组件负责最外层的表单容器；
el-form-item 组件负责每一个输入项的 label 和校验管理；
内部的 el-input 或者 el-switch 负责具体的输入组件。

```html
<el-form
  :model="ruleForm"
  :rules="rules"
  ref="form"
  label-width="100px"
  class="demo-ruleForm"
>
  <el-form-item label="活动名称" prop="name">
    <el-input v-model="ruleForm.name"></el-input>
  </el-form-item>
  <el-form-item label="活动区域" prop="region">
    <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
      <el-option label="区域一" value="shanghai"></el-option>
      <el-option label="区域二" value="beijing"></el-option>
    </el-select>
  </el-form-item>
  <el-form-item label="即时配送" prop="delivery">
    <el-switch v-model="ruleForm.delivery"></el-switch>
  </el-form-item>
  <el-form-item label="活动性质" prop="type">
    <el-checkbox-group v-model="ruleForm.type">
      <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
      <el-checkbox label="地推活动" name="type"></el-checkbox>
      <el-checkbox label="线下主题活动" name="type"></el-checkbox>
      <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
    </el-checkbox-group>
  </el-form-item>
  <el-form-item label="特殊资源" prop="resource">
    <el-radio-group v-model="ruleForm.resource">
      <el-radio label="线上品牌商赞助"></el-radio>
      <el-radio label="线下场地免费"></el-radio>
    </el-radio-group>
  </el-form-item>
  <el-form-item label="活动形式" prop="desc">
    <el-input type="textarea" v-model="ruleForm.desc"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm('ruleForm')"
      >立即创建</el-button
    >
    <el-button @click="resetForm('ruleForm')">重置</el-button>
  </el-form-item>
</el-form>
```

现在我们把上面的代码简化为最简单的形式，只留下 el-input 作为输入项，就可以清晰地看到表单组件工作的模式：el-form 组件使用:model 提供数据绑定；使用 rules 提供输入校验规则，可以规范用户的输入内容；使用 el-form-item 作为输入项的容器，对输入进行校验，显示错误信息。

```html
<el-form :model="ruleForm" :rules="rules" ref="form">
  <el-form-item label="用户名" prop="username">
    <el-input v-model="ruleForm.username"></el-input>
    <!-- <el-input :model-value="" @update:model-value=""></el-input> -->
  </el-form-item>
  <el-form-item label="密码" prop="passwd">
    <el-input type="textarea" v-model="ruleForm.passwd"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="submitForm()">登录</el-button>
  </el-form-item>
</el-form>
```

然后我们看下 rules 和 model 是如何工作的。
这里使用 reactive 返回用户输入的数据，username 和 passwd 输入项对应，然后 rules 使用 reactive 包裹用户输入项校验的配置。
具体的校验规则，现在主流组件库使用的都是 async-validator 这个库，详细的校验规则你可以访问 async-validator 的官网查看。而表单 Ref 上我们额外新增了一个 validate 方法，这个方法会执行所有的校验逻辑来显示用户的报错信息，下图就是用户输入不符合 rules 配置后，页面的报错提示效果。

```js
const ruleForm =
  reactive <
  UserForm >
  {
    username: '',
    passwd: '',
  };
const rules = reactive({
  rules: {
    username: {
      required: true,
      min: 1,
      max: 20,
      message: '长度在 1 到 20 个字符',
      trigger: 'blur',
    },
    passwd: [{ required: true, message: '密码', trigger: 'blur' }],
  },
});
function submitForm() {
  form.value.validate((valid) => {
    if (valid) {
      alert('submit!');
    } else {
      console.log('error submit!!');
      return false;
    }
  });
}
```

表单组件实现
那么接下来我们就要实现组件了。我们进入到 src/components 目录下新建 Form.vue 去实现 el-form 组件，该组件是整个表单组件的容器，负责管理每一个 el-form-item 组件的校验方法，并且自身还提供一个检查所有输入项的 validate 方法。
在下面的代码中，我们注册了传递的属性的格式，并且注册了 validate 方法使其对外暴露使用。

```js
interface Props {
  label?: string
  prop?: string
}
const props = withDefaults(defineProps<Props>(), {
  label: "",
  prop: ""
})
const formData = inject(key)
const o: FormItem = {
  validate,
}
defineExpose(o)
```

那么在 el-form 组件中如何管理 el-form-item 组件呢？我们先要新建 FormItem.vue 文件，这个组件加载完毕之后去通知 el-form 组件自己加载完毕了，这样在 el-form 中我们就可以很方便地使用数组来管理所有内部的 form-item 组件。

```js
import { emitter } from "../../emitter"
const items = ref<FormItem[]>([])
emitter.on("addFormItem", (item) => {
  items.value.push(item)
})
```

然后 el-form-item 还要负责管理内部的 input 输入标签，并且从 form 组件中获得配置的 rules，通过 rules 的逻辑，来判断用户的输入值是否合法。另外，el-form 还要管理当前输入框的 label，看看输入状态是否报错，以及报错的信息显示，这是一个承上启下的组件。

```js
onMounted(() => {
  if (props.prop) {
    emitter.on('validate', () => {
      validate();
    });
    emitter.emit('addFormItem', o);
  }
});
function validate() {
  if (formData?.rules === undefined) {
    return Promise.resolve({ result: true });
  }
  const rules = formData.rules[props.prop];
  const value = formData.model[props.prop];
  const schema = new Schema({ [props.prop]: rules });
  return schema.validate({ [props.prop]: value }, (errors) => {
    if (errors) {
      error.value = errors[0].message || '校验错误';
    } else {
      error.value = '';
    }
  });
}
```

这里我们可以看到，form、form-item 和 input 这三个组件之间是嵌套使用的关系：
form 提供了所有的数据对象和配置规则；
input 负责具体的输入交互；
form-item 负责中间的数据和规则管理，以及显示具体的报错信息。
这就需要一个强有力的组件通信机制，在 Vue 中组件之间的通信机制有这么几种。
首先是父子组件通信，通过 props 和 emits 来通信。这个我们在全家桶实战篇和评级组件那一讲都有讲过，父元素通过 props 把需要的数据传递给子元素，子元素通过 emits 通知父元素内部的变化，并且还可以通过 defineDepose 的方式暴露给父元素方法，可以让父元素调用自己的方法。
那么 form 和 input 组件如何通信呢？这种祖先元素和后代元素，中间可能嵌套了很多层的关系，Vue 则提供了 provide 和 inject 两个 API 来实现这个功能。
在组件中我们可以使用 provide 函数向所有子组件提供数据，子组件内部通过 inject 函数注入使用。注意这里 provide 提供的只是普通的数据，并没有做响应式的处理，如果子组件内部需要响应式的数据，那么需要在 provide 函数内部使用 ref 或者 reative 包裹才可以。
关于 prvide 和 inject 的类型系统，我们可以使用 Vue 提供的 InjectiveKey 来声明。我们在 form 目录下新建 type.ts 专门管理表单组件用到的相关类型，在下面的代码中，我们定义了表单 form 和表单管理 form-item 的上下文，并且通过 InjectionKey 管理提供的类型。

```js
import { InjectionKey } from "vue"
import { Rules, Values } from "async-validator"
export type FormData = {
  model: Record<string, unknown>
  rules?: Rules
}
export type FormItem = {
  validate: () => Promise<Values>
}
export type FormType = {
  validate: (cb: (isValid: boolean) => void) => void
}
export const key: InjectionKey<FormData> = Symbol("form-data")
```

而下面的代码，我们则通过 provide 向所有子元素提供 form 组件的上下文。子组件内部通过 inject 获取，很多组件都是嵌套成对出现的，provide 和 inject 这种通信机制后面我们还会不停地用到，做好准备。

```
provide(key, {
  model: props.model,
  rules?: props.rules,
})
# 子组件
const formData = inject(key);
```

然后就是具体的 input 实现逻辑，在下面的代码中，input 的核心逻辑就是对 v-model 的支持，这个内容我们在评级组件那一讲已经实现过了。
v-mode 其实是:mode-value="x"和 @update:modelValute 两个写法的简写，组件内部获取对应的属性和 modelValue 方法即可。这里需要关注的代码是我们输入完成之后的事件，输入的结果校验是由父组件 el-form-item 来实现的，我们只需要通过 emit 对外广播出去即可。

```html
<template>
  <div
    class="el-form-item"
  >
    <label
      v-if="label"
    >{{ label }}</label>
    <slot />
    <p
      v-if="error"
      class="error"
    >
      {{ error }}
    </p>
  </div>
</template>
<script lang="ts">
export default{
  name:'ElFormItem'
}
</script>
<script setup lang="ts">
import Schema from "async-validator"
import { onMounted, ref, inject } from "vue"
import { FormItem, key } from "./type"
import { emitter } from "../../emitter"
interface Props {
  label?: string
  prop?: string
}
const props = withDefaults(defineProps<Props>(), { label: "", prop: "" })
// 错误
const error = ref("")
const formData = inject(key)
const o: FormItem = {
  validate,
}
defineExpose(o)
onMounted(() => {
  if (props.prop) {
    emitter.on("validate", () => {
      validate()
    })
    emitter.emit("addFormItem", o)
  }
})
function validate() {
  if (formData?.rules === undefined) {
    return Promise.resolve({ result: true })
  }
  const rules = formData.rules[props.prop]
  const value = formData.model[props.prop]
  const schema = new Schema({ [props.prop]: rules })
  return schema.validate({ [props.prop]: value }, (errors) => {
    if (errors) {
      error.value = errors[0].message || "校验错误"
    } else {
      error.value = ""
    }
  })
}
</script>
<style lang="scss">
@import '../styles/mixin';
@include b(form-item) {
  margin-bottom: 22px;
  label{
    line-height:1.2;
    margin-bottom:5px;
    display: inline-block;
  }
  & .el-form-item {
    margin-bottom: 0;
  }
}
.error{
  color:red;
}
</style>
```

最后我们点击按钮的时候，在最外层的 form 标签内部会对所有的输入项进行校验。由于我们管理着所有的 form-item，只需要遍历所有的 form-item，依次执行即可。
下面的代码就是表单注册的 validate 方法，我们遍历全部的表单输入项，调用表单输入项的 validate 方法，有任何一个输入项有报错信息，整体的校验就会是失败状态。

```js
function validate(cb: (isValid: boolean) => void) {
  const tasks = items.value.map((item) => item.validate());
  Promise.all(tasks)
    .then(() => {
      cb(true);
    })
    .catch(() => {
      cb(false);
    });
}
```

上面代码实际执行的是每个表单输入项内部的 validate 方法，这里我们使用的就是 async-validate 的校验函数。在 validate 函数内部，我们会获取表单所有的 ruls，并且过滤出当前输入项匹配的输入校验规则，然后通过 AsyncValidator 对输入项进行校验，把所有的校验结果放在 model 对象中。如果 `errors[0].message` 非空，就说明校验失败，需要显示对应的错误消息，页面输入框显示红色状态。

```js
import Schema from 'async-validator';
function validate() {
  if (formData?.rules === undefined) {
    return Promise.resolve({ result: true });
  }
  const rules = formData.rules[props.prop];
  const value = formData.model[props.prop];
  const schema = new Schema({ [props.prop]: rules });
  return schema.validate({ [props.prop]: value }, (errors) => {
    if (errors) {
      error.value = errors[0].message || '校验错误';
    } else {
      error.value = '';
    }
  });
}
```

### 23. 弹窗:如何设计一个弹窗组件?

上一讲我们剖析了表单组件的实现模式，相信学完之后，你已经掌握了表单类型组件设计的细节，表单组件的主要功能就是在页面上获取用户的输入。
不过，用户在交互完成之后，还需要知道交互的结果状态，这就需要我们提供专门用来反馈操作状态的组件。这类组件根据反馈的级别不同，也分成了很多种类型，比如全屏灰色遮罩、居中显示的对话框 Dialog，在交互按钮侧面显示、用来做简单提示的 tooltip，以及右上角显示信息的通知组件 Notification 等，这类组件的交互体验你都可以在Element3 官网感受。
今天的代码也会用 Element3 的 Dialog 组件和 Notification 进行举例，在动手写代码实现之前，我们先从这个弹窗组件的需求开始说起。
组件需求分析
我们先来设计一下要做的组件，通过这部分内容，还可以帮你继续加深一下对单元测试 Jest 框架的使用熟练度。我建议你在设计一个新的组件的时候，也试试采用这种方式，先把组件所有的功能都罗列出来，分析清楚需求再具体实现，这样能够让你后面的工作事半功倍。
首先无论是对话框 Dialog，还是消息弹窗 Notification，它们都由一个弹窗的标题，以及具体的弹窗的内容组成的。我们希望弹窗有一个关闭的按钮，点击之后就可以关闭弹窗，弹窗关闭之后还可以设置回调函数。
下面这段代码演示了 dialog 组件的使用方法，通过 title 显示标题，通过 slot 显示文本内容和交互按钮，而通过 v-model 就能控制显示状态。
```html
<el-dialog
  title="提示"
  :visible.sync="dialogVisible"
  width="30%"
  v-model:visible="dialogVisible"
>
  <span>这是一段信息</span>
  <template #footer>
    <span class="dialog-footer">
      <el-button @click="dialogVisible = false">取 消</el-button>
      <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
    </span>
  </template>
</el-dialog>
```
这类组件实现起来和表单类组件区别不是特别大，我们首先需要做的就是控制好组件的数据传递，并且使用 Teleport 渲染到页面顶层的 body 标签。
像 Dialog 和 Notification 类的组件，我们只是单纯想显示一个提示或者报错信息，过几秒就删除，如果在每个组件内部都需要写一个 <Dialog v-if>，并且使用 v-if 绑定变量的方式控制显示就会显得很冗余。
所以，这里就要用到一种调用 Vue 组件的新方式：我们可以使用 JavaScript 的 API 动态地创建和渲染 Vue 的组件。具体如何实现呢？我们以 Notification 组件为例一起看一下。
下面的代码是 Element3 的 Notification 演示代码。组件内部只有两个 button，我们不需要书写额外的组件标签，只需要在 <script setup> 中使用 Notification.success函数，就会在页面动态创建 Notification 组件，并且显示在页面右上角。
```html
<template>
  <el-button plain @click="open1"> 成功 </el-button>
  <el-button plain @click="open2"> 警告 </el-button>
</template>
<script setup>
  import { Notification } from 'element3'
  function open1() {
    Notification.success({
      title: '成功',
      message: '这是一条成功的提示消息',
      type: 'success'
    })
  }
  function open2() {
    Notification.warning({
      title: '警告',
      message: '这是一条警告的提示消息',
      type: 'warning'
    })
  }
</script>
```
弹窗组件实现
分析完需求之后，我们借助单元测试的方法来实现这个弹窗组件（单元测试的内容如果记不清了，你可以回顾第 20 讲）。
我们依次来分析 Notification 的代码，相比于写 Demo 逻辑的代码，这次我们体验一下实际的组件和演示组件的区别。我们来到 element3 下面的 src/components/Notification/notifucation.vue 代码中，下面的代码构成了组件的主体框架，我们不去直接写组件的逻辑，而是先从测试代码来梳理组件的功能。
```html
<template>
  <div class="el-nofication">
    <slot />
  </div>
</template>
<script>
</script>
<style lang="scss">
@import '../styles/mixin';
</style>
```
结合下面的代码可以看到，我们进入到了内部文件 Notification.spec.js 中。下面的测试代码中，我们期待 Notification 组件能够渲染 el-notification样式类，并且内部能够通过属性 title 渲染标题；message 属性用来渲染消息主体；position 用来渲染组件的位置，让我们的弹窗组件可以显示在浏览器四个角。
```html
import Notification from "./Notification.vue"
import { mount } from "@vue/test-utils"
describe("Notification", () => { 
  
  it('渲染标题title', () => {
    const title = 'this is a title'
    const wrapper = mount(Notification, {
      props: {
        title
      }
    })
    expect(wrapper.get('.el-notification__title').text()).toContain(title)
  })
  it('信息message渲染', () => {
    const message = 'this is a message'
    const wrapper = mount(Notification, {
      props: {
        message
      }
    })
    expect(wrapper.get('.el-notification__content').text()).toContain(message)
  })
  it('位置渲染', () => {
    const position = 'bottom-right'
    const wrapper = mount(Notification, {
      props: {
        position
      }
    })
    expect(wrapper.find('.el-notification').classes()).toContain('right')
    expect(wrapper.vm.verticalProperty).toBe('bottom')
    expect(wrapper.find('.el-notification').element.style.bottom).toBe('0px')
  })
  it('位置偏移', () => {
    const verticalOffset = 50
    const wrapper = mount(Notification, {
      props: {
        verticalOffset
      }
    })
    expect(wrapper.vm.verticalProperty).toBe('top')
    expect(wrapper.find('.el-notification').element.style.top).toBe(
      `${verticalOffset}px`
    )
  })
})
```
这时候毫无疑问，测试窗口会报错。我们需要进入 notificatin.vue 中实现代码逻辑。
下面的代码中，我们在代码中接收 title、message 和 position，使用 notification__title 和 notification__message 渲染标题和消息。
```html
<template>
  <div class="el-notification" :style="positionStyle" @click="onClickHandler">
    <div class="el-notification__title">
      {{ title }}
    </div>
    <div class="el-notification__message">
      {{ message }}
    </div>
    <button
      v-if="showClose"
      class="el-notification__close-button"
      @click="onCloseHandler"
    ></button>
  </div>
</template>
<script setup>
const instance = getCurrentInstance()
const visible = ref(true)
const verticalOffsetVal = ref(props.verticalOffset)
const typeClass = computed(() => {
  return props.type ? `el-icon-${props.type}` : ''
})
const horizontalClass = computed(() => {
  return props.position.endsWith('right') ? 'right' : 'left'
})
const verticalProperty = computed(() => {
  return props.position.startsWith('top') ? 'top' : 'bottom'
})
const positionStyle = computed(() => {
  return {
    [verticalProperty.value]: `${verticalOffsetVal.value}px`
  }
})
</script>
<style lang="scss">
.el-notification {
  position: fixed;
  right: 10px;
  top: 50px;
  width: 330px;
  padding: 14px 26px 14px 13px;
  border-radius: 8px;
  border: 1px solid #ebeef5;
  background-color: #fff;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  overflow: hidden;
}
</style>
```
然后我们新增测试代码，设置弹窗是否显示关闭按钮以及关闭弹窗之后的回调函数。我们希望点击关闭按钮之后，就能够正确执行传入的 onClose 函数。
```html
it('set the showClose ', () => {
    const showClose = true
    const wrapper = mount(Notification, {
      props: {
        showClose
      }
    })
    expect(wrapper.find('.el-notification__closeBtn').exists()).toBe(true)
    expect(wrapper.find('.el-icon-close').exists()).toBe(true)
  })
  it('点击关闭按钮', async () => {
    const showClose = true
    const wrapper = mount(Notification, {
      props: {
        showClose
      }
    })
    const closeBtn = wrapper.get('.el-notification__closeBtn')
    await closeBtn.trigger('click')
    expect(wrapper.get('.el-notification').isVisible()).toBe(false)
  })
  it('持续时间之后自动管理', async () => {
    jest.useFakeTimers()
    const wrapper = mount(Notification, {
      props: {
        duration: 1000
      }
    })
    jest.runTimersToTime(1000)
    await flushPromises()
    expect(wrapper.get('.el-notification').isVisible()).toBe(false)
     })
```
到这里，Notification 组件测试的主体逻辑就实现完毕了，我们拥有了一个能够显示在右上角的组件，具体效果你可以参考后面这张截图。

进行到这里，距离完成整体设计我们还差两个步骤。
首先，弹窗类的组件都需要直接渲染在 body 标签下面，弹窗类组件由于布局都是绝对定位，如果在组件内部渲染，组件的 css 属性（比如 Transform）会影响弹窗组件的渲染样式，为了避免这种问题重复出现，弹窗组件 Dialog、Notification 都需要渲染在 body 内部。
Dialog 组件可以直接使用 Vue3 自带的 Teleport，很方便地渲染到 body 之上。在下面的代码中, 我们用 teleport 组件把 dialog 组件包裹之后，通过 to 属性把 dialog 渲染到 body 标签内部。
```html
  <teleport
    :disabled="!appendToBody"
    to="body"
  >
    <div class="el-dialog">
      <div class="el-dialog__content">
        <slot />
      </div>
    </div>
  </teleport>
```
这时我们使用浏览器调试窗口，就可以看到 Dialog 标签已经从当前组件移动到了 body 标签内部，如下图所示。

但是 Notification 组件并不会在当前组件以组件的形式直接调用，我们需要像 Element3 一样，能够使用 js 函数动态创建 Notification 组件，给 Vue 的组件提供 Javascript 的动态渲染方法，这是弹窗类组件的特殊需求。
组件渲染优化
我们先把测试代码写好，具体如下。代码中分别测试函数创建组件，以及不同配置和样式的通知组件。
```html
it('函数会创建组件', () => {
  const instanceProxy = Notification('foo')
  expect(instanceProxy.close).toBeTruthy()
})
it('默认配置 ', () => {
  const instanceProxy = Notification('foo')
  expect(instanceProxy.$props.position).toBe('top-right')
  expect(instanceProxy.$props.message).toBe('foo')
  expect(instanceProxy.$props.duration).toBe(4500)
  expect(instanceProxy.$props.verticalOffset).toBe(16)
})
test('字符串信息', () => {
  const instanceProxy = Notification.info('foo')
  expect(instanceProxy.$props.type).toBe('info')
  expect(instanceProxy.$props.message).toBe('foo')
})
test('成功信息', () => {
  const instanceProxy = Notification.success('foo')
  expect(instanceProxy.$props.type).toBe('success')
  expect(instanceProxy.$props.message).toBe('foo')
})
```
现在测试写完后还是会报错，因为现在 Notification 函数还没有定义，我们要能通过 Notification 函数动态地创建 Vue 的组件，而不是在 template 中使用组件。
在JSX 那一讲中我们讲过，template 的本质就是使用 h 函数创建虚拟 Dom，如果我们自己想动态创建组件时，使用相同的方式即可。
在下面的代码中我们使用 Notification 函数去执行 createComponent 函数，使用 h 函数动态创建组件，实现了动态组件的创建。
```html
function createComponent(Component, props, children) {
  const vnode = h(Component, { ...props, ref: MOUNT_COMPONENT_REF }, children)
  const container = document.createElement('div')
  vnode[COMPONENT_CONTAINER_SYMBOL] = container
  render(vnode, container)
  return vnode.component
}
export function Notification(options) {
  return createNotification(mergeProps(options))
}
function createNotification(options) {
  const instance = createNotificationByOpts(options)
  setZIndex(instance)
  addToBody(instance)
  return instance.proxy
}
```
创建组件后，由于 Notification 组件同时可能会出现多个弹窗，所以我们需要使用数组来管理通知组件的每一个实例，每一个弹窗的实例都存储在数组中进行管理。
下面的代码里，我演示了怎样用数组管理弹窗的实例。Notification 函数最终会暴露给用户使用，在 Notification 函数内部我们通过 createComponent 函数创建渲染的容器，然后通过 createNotification 创建弹窗组件的实例，并且维护在 instanceList 中。
```html
const instanceList = []
function createNotification(options) {
  ...
  addInstance(instance)
  return instance.proxy
}  
function addInstance(instance) {
  instanceList.push(instance)
}
;['success', 'warning', 'info', 'error'].forEach((type) => {
  Notification[type] = (options) => {
    if (typeof options === 'string' || isVNode(options)) {
      options = {
        message: options
      }
    }
    options.type = type
    return Notification(options)
  }
})
// 有了instanceList， 可以很方便的关闭所有信息弹窗
Notification.closeAll = () => {
  instanceList.forEach((instance) => {
    instance.proxy.close()
    removeInstance(instance)
  })
}
```
最后，我带你简单回顾下我们都做了什么。在正式动手实现弹窗组件前，我们分析了弹窗类组件的风格。弹窗类组件主要负责用户交互的反馈。根据显示的级别不同，它可以划分成不同的种类：既有覆盖全屏的弹窗 Dialog，也有负责提示消息的 Notification。
这些组件除了负责渲染传递的数据和方法之外，还需要能够脱离当前组件进行渲染，防止当前组件的 css 样式影响布局。因此 Notification 组件需要渲染到 body 标签内部，而 Vue 提供了 Teleport 组件来完成这个任务，我们通过 Teleport 组件就能把内部的组件渲染到指定的 dom 标签。
之后，我们需要给组件提供 JavaScript 调用的方法。我们可以使用 Notification()的方式动态创建组件，利用 createNotification 即可动态创建 Vue 组件的实例。
对于弹窗组件来说可以这样操作：首先通过 createNotification 函数创建弹窗的实例，并且给每个弹窗设置好唯一的 id 属性，然后存储在数组中进行管理。接着，我们通过对 createNotification 函数返回值的管理，即可实现弹窗动态的渲染、更新和删除功能。
总结
正文里已经详细讲解和演示了弹窗组件的设计，所以今天的总结我想变个花样，再给你说说 TDD 的事儿。
很多同学会觉得写测试代码要花一定成本，有畏难心理，觉得自己不太会写测试，这些“假想”给我们造成了“TDD 很难实施”的错觉。实际上入门 TDD 并没有这么难。按照我的实践经验来看，先学会怎么写测试，再学习怎么重构，基本上就可以入门写 TDD 了。
就拿我们这讲的实践来说，我们再次应用了测试驱动开发这个方式来实现弹窗组件，把整体需求拆分成一个个子任务，逐个击破。根据设计的需求写好测试代码之后，测试代码就会检查我们的业务逻辑有没有实现，指导我们做相应的修改。
咱们的实践过程抽象出来，一共包括四个步骤：写测试 -> 运行测试 (报错) -> 写代码让测试通过 -> 重构的方式。这样的开发模式，今后你在设计组件库时也可以借鉴，不但有助于提高代码的质量和可维护性，还能让代码有比较高的代码测试覆盖率。
思考题
最后留一个思考题，现在我们设计的 Notification 组件的 message 只能支持文本消息，如果想支持传入其他组件，应该如何实现？
欢迎你在评论去分享你的答案，也欢迎你把这一讲的内容分享给你的同事和朋友们，我们下一讲再见。

### 24. 树:如何设计一个树形组件?

上一讲，我们一起学习了弹窗组件的设计与实现，这类组件的主要特点是需要渲染在最外层 body 标签之内，并且还需要支持 JavaScript 动态创建和调用组件。相信学完上一讲，你不但会对弹窗类组件的实现加深理解，也会对 TDD 模式更有心得。
除了弹窗组件，树形组件我们在前端开发中经常用到，所以今天我就跟你聊一下树形组件的设计思路跟实现细节。
组件功能分析
我们进入Element3 的 Tree 组件文档页面，现在我们对 Vue 的组件如何设计和实现已经很熟悉了，我重点挑跟之前组件设计不同的地方为你讲解。
在设计新组件的时候，我们需要重点考虑的就是树形组件和之前我们之前的 Container、Button、Notification 有什么区别。树形组件的主要特点是可以无限层级、这种需求在日常工作和生活中其实很常见，比如后台管理系统的菜单管理、文件夹管理、生物分类、思维导图等等。

根据上图所示，我们可以先拆解出树形组件的功能需求。
首先，树形组件的节点可以无限展开，父节点可以展开和收起节点，并且每一个节点有一个复选框，可以切换当前节点和所有子节点的选择状态。另外，同一级所有节点选中的时候，父节点也能自动选中。
下面的代码是 Element3 的 Tree 组件使用方式，所有的节点配置都是一个 data 对象实现的。每个节点里的 label 用来显示文本；expaned 显示是否展开；checked 用来决定复选框选中列表，data 数据内部的 children 属性用来配置子节点数组，子节点的数据结构和父节点相同，可以递归实现。
```html
<el-tree
  :data="data"
  show-checkbox
  v-model:expanded="expandedList"
  v-model:checked="checkedList"
  :defaultNodeKey="defaultNodeKey"
>
</el-tree>
<script>
  export default {
    data() {
      return {
        expandedList: [4, 5],
        checkedList: [5],
        data: [
          {
            id: 1,
            label: '一级 1',
            children: [
              {
                id: 4,
                label: '二级 1-1',
                children: [
                  {
                    id: 9,
                    label: '三级 1-1-1'
                  },
                  {
                    id: 10,
                    label: '三级 1-1-2'
                  }
                ]
              }
            ]
          },
          {
            id: 2,
            label: '一级 2',
            children: [
              {
                id: 5,
                label: '二级 2-1'
              },
              {
                id: 6,
                label: '二级 2-2'
              }
            ]
          }
        ],
        defaultNodeKey: {
          childNodes: 'children',
          label: 'label'
        }
      }
    }
  }
  
</script>
```
递归组件
这里父节点和子节点的样式操作完全一致，并且可以无限嵌套，这种需求需要组件递归来实现，也就是组件内部渲染自己渲染自己。
想要搞定递归组件，我们需要先明确什么是递归，递归的概念也是我们前端进阶过程中必须要掌握的知识点。
前端的场景中，树这个数据结构出现的频率非常高，浏览器渲染的页面是 Dom 树，我们内部管理的是虚拟 Dom 树，树形结构是一种天然适合递归的数据结构。
我们先来做一个算法题感受一下，我们来到leetcode 第 226 题反转二叉树，题目的描述很简单，就是把属性结构反转，下面是题目的描述：
每一个节点的 val 属性代表显示的数字，left 指向左节点，right 指向右节点，如何实现 invertTree 去反转这一个二叉树，也就是所有节点的 left 和 right 互换位置呢？
输入     
```html
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
输出
```html
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
节点的构造函数
```html
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
```
输入的左右位置正好相反，而且每个节点的结构都相同，这就是非常适合递归的场景。递归的时候，我们首先需要思考递归的核心逻辑如何实现，这里就是两个节点如何交换，然后就是递归的终止条件，否则递归函数就会进入死循环。
下面的代码中，设置 invertTree 函数的终止条件是 root 是 null 的时候，也就是如果节点不存在的时候不需要反转。这里我们只用了一行解构赋值的代码就实现了，值得注意的是右边的代码中我们递归调用了 inverTree 去递归执行，最终实现了整棵树的反转。
```html
var invertTree = function(root) {
  // 递归 终止条件
  if(root==null) {
    return root
  }
  // 递归的逻辑
  [root.left, root.right] = [invertTree(root.right), invertTree(root.left)]
  return root
}
```
树形组件的数据结构内部的 children 可以无限嵌套，处理这种数据结构，就需要使用递归的算法思想。有了上面这个算法题的基础后，我们后面再学习树形组件如何实现就能更加顺畅了。
组件实现
首先我们进入到 Element3 的 tree 文件夹内部，然后找到 tree.vue 文件。tree.vue 是组件的入口容器，用于接收和处理数据，并将数据传递给 TreeNode.vue；TreeNode.vue 负责渲染树形组件的选择框、标题和递归渲染子元素。
在下面的代码中，我们提供了 el-tree 的容器，还导入了 el-tree-node 进行渲染。tree.vue 通过 provide 向所有子元素提供 tree 的数据，通过 useExpand 判断树形结构的展开状态，并且用到了 watchEffect 去向组件外部通知 update:expanded 事件。
```html
<template>
  <div class="el-tree">
    <el-tree-node v-for="child in tree.root.childNodes" :node="child" :key="child.id"></el-tree-node>
  </div>
</template>
<script>
import ElTreeNode from './TreeNode.vue'
const instance = getCurrentInstance()
const tree = new Tree(props.data, props.defaultNodeKey, {
  asyncLoadFn: props.asyncLoadFn,
  isAsync: props.async
})
const state = reactive({
  tree
})
provide('elTree', instance)
useTab()
useExpand(props, state)
function useExpand(props, state) {
  const instance = getCurrentInstance()
  const { emit } = instance
  if (props.defaultExpandAll) {
    state.tree.expandAll()
  }
  watchEffect(() => {
    emit('update:expanded', state.tree.expanded)
  })
  watchEffect(() => {
    state.tree.setExpandedByIdList(props.expanded, true)
  })
  onMounted(() => {
    state.tree.root.expand(true)
  })
}
  
</script>
```
然后我们进入到 Tree.Node.vue 文件中，tree-node 组件是树组件的核心，一个 TreeNode 组件包含四个部分：展开按钮、文本的多选框、每个节点的标题和递归的 children 子节点。
我们先来看 TreeNode.vue 的模板基本结构，可以把下面的 div 标签分成四个部分：el-tree-node__content 负责每个树节点的渲染，第一个 span 就是渲染展开符；el-checkbox 组件负责显示复选框，并且绑定了 node.isChecked 属性；el-node__contentn 负责渲染树节点的标题；el-tree__children 负责递归渲染 el-tree-node 节点，组件内部渲染自己，这就是组件递归的写法。
```html
<div
    v-show="node.isVisable"
    class="el-tree-node"
    :class="{
      'is-expanded': node.isExpanded,
      'is-current': elTree.proxy.dragState.current === node,
      'is-checked': node.isChecked,
    }"
    role="TreeNode"
    ref="TreeNode"
    :id="'TreeNode' + node.id"
    @click.stop="onClickNode"
  >
    <div class="el-tree-node__content"> 
      <span
        :class="[
          { expanded: node.isExpanded, 'is-leaf': node.isLeaf },
          'el-tree-node__expand-icon',
          elTree.props.iconClass
        ]"
        @click.stop="
          node.isLeaf ||
            (elTree.props.accordion ? node.collapse() : node.expand())
        ">
      </span>
      <el-checkbox
        v-if="elTree.props.showCheckbox"
        :modelValue="node.isChecked"
        @update:modelValue="onChangeCheckbox"
        @click="elTree.emit('check', node, node.isChecked, $event)"
      >
      </el-checkbox>
      <el-node-content
        class="el-tree-node__label"
        :node="node"
      ></el-node-content>
    </div>
      <div
        class="el-tree-node__children"
        v-show="node.isExpanded"
        v-if="!elTree.props.renderAfterExpand || node.isRendered"
        role="group"
        :aria-expanded="node.isExpanded"
      >
        <el-tree-node
          v-for="child in node.childNodes"
          :key="child.id"
          :node="child"
        >
        </el-tree-node>
      </div>
  </div>
```
然后我们看下 tree-node 中我们需要处理的数据有哪些。下面的代码中，我们先通过 inject 注入 tree 组件最完成的配置。然后在点击节点的时候，通过判断 elTree 的全局配置，去决定点击之后的切换功能，并且在展开和 checkbox 切换的同时，通过 emit 对父组件触发事件。
```html
const elTree = inject('elTree')
const onClickNode = (e) => {
  !elTree.props.expandOnClickNode ||
    props.node.isLeaf ||
    (elTree.props.accordion ? props.node.collapse() : props.node.expand())
  !elTree.props.checkOnClickNode ||
    props.node.setChecked(undefined, elTree.props.checkStrictly)
  elTree.emit('node-click', props.node, e)
  elTree.emit('current-change', props.node, e)
  props.node.isExpanded
    ? elTree.emit('node-expand', props.node, e)
    : elTree.emit('node-collapse', props.node, e)
}
const onChangeCheckbox = (e) => {
  props.node.setChecked(undefined, elTree.props.checkStrictly)
  elTree.emit('check-change', props.node, e)
}
```

到这里，树结构的渲染其实就结束了。
但是有些场景我们需要对树节点的渲染内容进行自定。比如后面这段代码，我们在节点的右侧加上 append 和 delete 操作按钮，这种需求在菜单树的管理中很常见。
这个时候我们节点需要支持内容的自定义，然后我们注册了 el-node-content 组件。这个组件使用起来非常简单，由于我们还需要支持节点的自定义渲染，所以要把这部分抽离成组件。当 slots.default 为函数的时候，返回函数的执行内容；或者传递的 renderContent 是函数的话，也要返回函数执行的结果。
```html
import { TreeNode } from './entity/TreeNode'
import { inject, h } from 'vue'
render(ctx) {
  const elTree = inject('elTree')
  if (typeof elTree.slots.default === 'function') {
    return elTree.slots.default({ node: ctx.node, data: ctx.node.data.raw })
  } else if (typeof elTree.props.renderContent === 'function') {
    return elTree.props.renderContent({
      node: ctx.node,
      data: ctx.node.data.raw
    })
  }
  return h('span', ctx.node.label)
}
```
这样，用户就可以利用 render-content 属性传递一个函数的方式，去实现内容的自定义渲染。
我们还是结合代码例子做理解，下面的代码中用了 render-content 的方式返回树形结构的渲染结果，render-content 传递的函数内部会根据 node 和 data 数据，返回对应的标题，并且新增了两个 el-button 组件。
```html
<div class="custom-tree-container">
  <div class="block">
    <p>使用 render-content</p>
    <el-tree
      :data="data1"
      show-checkbox
      default-expand-all
      :expand-on-click-node="false"
      :render-content="renderContent"
    >
    </el-tree>
  </div>
</div>
<script>
function renderContent({ node, data }) {
  return (
    <span class="custom-tree-node">
      <span>{data.label}</span>
      <span>
        <el-button
          size="mini"
          type="text"
          onClick={() => this.append(node, data)}
        >
          Append
        </el-button>
        <el-button
          size="mini"
          type="text"
          onClick={() => this.remove(node, data)}
        >
          Delete
        </el-button>
      </span>
    </span>
  )
}
</script>
```
上面的代码会渲染出下面的示意图的效果。

最后，我们还可以对树实现更多操作方式的支持。
比如我们可以支持树形结构的拖拽修改、可以把任何任意节点拖拽到其他树形内部、修改整个树形结构的内容。想要实现这些功能，我们就需要监听节点的 drag-over、drag-leave 等拖拽事件，在 drop 事件执行的时候，把拖拽的节点数据，复制给拖拽的节点中完成修改即可。这部分代码，同学们可以自行去 Element3 拓展学习。
总结
今天的主要内容就讲完啦，我们来总结一下今天学到的内容吧。
首先我们分析了树形组件的设计需求、我们需要递归组件的形式去实现树形节点的无限嵌套，然后我们通过算法题的形式掌握了递归的概念，这个概念在 Vue 组件中也是一样的，每个组件返回 name 后，可以通过这个 name 在组件内部来调用自己，这样就可以很轻松地实现 Tree 组件。
tree 组件具体要分成三个组件进行实现。最外层的 tree 组件负责整个树组件的容器，内部会通过 provide 方法为子元素提供全局的配置和操作方法。每个 tree 的配置中的 title、expanded、checked 树形作为树组件显示的主体内容。children 是一个深层嵌套的数组，我们需要用递归组件的方式渲染出完成的树，tree 内部的 tree-node 组件就负责递归渲染出完成的树形结构。
最后，我们想支持树节点的自定义渲染，这就需要在 teree-node 内部定制 tree-node-content 组件，用来渲染用户传递的 render-content 或者默认的插槽函数。
树形数据在我们日常开发项目中也很常见，菜单、城市选择、权限等数据都很适合树形结构，学会树形结构的处理，能很好地帮助我们在日常开发中应对更复杂的需求。
思考题
最后留一个思考题吧。我们的树形组件现在是全部节点的渲染，如果我们有 1000 个节点要渲染，如何对这个树形节点做性能优化呢？
欢迎你在评论区分享你的答案，也欢迎你把这一讲的内容分享给你的同事和朋友们，我们下一讲再见。

### 25. 表格:如何设计一个表格组件?

上一讲我们实现了树形组件，树形组件的主要难点就是对无限嵌套数据的处理。今天我们来介绍组件库中最复杂的表格组件，表格组件在项目中负责列表数据的展示，尤其是在管理系统中，比如用户信息、课程订单信息的展示，都需要使用表格组件进行渲染。
关于表单的具体交互形式和复杂程度，你可以访问ElementPlus、NaiveUi、 AntDesignVue这三个主流组件库中的表格组件去体验，并且社区还提供了单独的复杂表格组件，这一讲我就给你详细说说一个复杂表格组件如何去实现。
表格组件
大部分组件库都会内置表格组件，这是总后台最常用的组件之一，用于展示大量的结构化的数据。html 也提供了内置的表格标签，由  <table> 、<thead> 、<tbody> 、<tr> 、<th> 、<td>  这些标签来组成一个最简单的表格标签。
我们先研究一下 html 的 table 标签。下面的代码中，table 标签负责表格的容器，thead 负责表头信息的容器，tbody 负责表格的主体，tr 标签负责表格的每一行，th 和 td 分别负责表头和主体的单元格。
其实标准的表格系列标签，跟 div+css 实现是有很大区别的。比如表格在做单元格合并时，要提供原生属性，这时候用 div 就很麻烦了。另外，它们的渲染原理上也有一定的区别，每一列的宽度会保持一致。
```html
<table>
  <thead>
    <tr>
      <th>课程</th>
      <th>价格</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>重学前端</td>
      <td>129</td>
    </tr>
    <tr>
      <td>玩转Vue3全家桶</td>
      <td>129</td>
    </tr>
  </tbody>
</table>
```
简单的表格数据渲染并不需要组件，我们直接使用标准的 table 系列标签就可以。但有的时候，除了呈现数据，也会带有一些额外的功能要求，比如嵌套列、性能优化等。这时候组件的好处就很明显了，它能帮我们省去这些基础的工作。
表格组件的使用风格，从设计上说也分为了两个方向。一个方向是完全由数据驱动，这里我们可以参考 Naive Ui 的使用方式，n-data-table 标签负责容器，直接通过 data 属性传递数据，通过 columns 传递表格的表头配置。
下面的代码中，我们在 colums 中去配置每行需要显示的属性，通过 render 函数可以返回定制化的结果，再使用 h 函数返回 Button，渲染出对应的按钮。
```html
<template>
  <n-data-table :columns="columns" :data="data" :pagination="pagination" />
</template>
<script>
import { h, defineComponent } from 'vue'
import { NTag, NButton, useMessage } from 'naive-ui'
const createColumns = ({ sendMail }) => {
  return [
    {
      title: 'Name',
      key: 'name',
      align: 'center'
    },
    {
      title: 'Age',
      key: 'age'
    },
    {
      title: 'Action',
      key: 'actions',
      render (row) {
        return h(
          NButton,
          {
            size: 'small',
            onClick: () => sendMail(row)
          },
          { default: () => 'Send Email' }
        )
      }
    }
  ]
}
const createData = () => [
  {
    key: 0,
    name: 'John Brown',
    age: 32,
    tags: ['nice', 'developer']
  },
  {
    key: 1,
    name: 'Jim Green',
    age: 42,
  },
  {
    key: 2,
    name: 'Joe Black',
    age: 32
  }
]
export default defineComponent({
  setup () {
    const message = useMessage()
    return {
      data: createData(),
      columns: createColumns({
        sendMail (rowData) {
          message.info('send mail to ' + rowData.name)
        }
      }),
      pagination: {
        pageSize: 10
      }
    }
  }
})
</script>
```
还有一种是 Element3 现在使用的风格，配置数据之后，具体数据的展现形式交给子元素来决定，把 columns 当成组件去使用，我们仍然通过例子来加深理解。
下面的代码中，我们配置完 data 后，使用 el-table-colum 组件去渲染组件的每一列，通过 slot 的方式去实现定制化的渲染。这两种风格各有优缺点，我们后面还会结合 Elemnt3 的源码进行讲解.
```html
<el-table :data="tableData" border style="width: 100%">
  <el-table-column fixed prop="date" label="日期" width="150">
  </el-table-column>
  <el-table-column prop="name" label="姓名" width="120"> </el-table-column>
  <el-table-column prop="province" label="省份" width="120"> </el-table-column>
  <el-table-column prop="city" label="市区" width="120"> </el-table-column>
  <el-table-column prop="address" label="地址" width="300"> </el-table-column>
  <el-table-column prop="zip" label="邮编" width="120"> </el-table-column>
  <el-table-column fixed="right" label="操作" width="100">
    <template v-slot="scope">
      <el-button @click="handleClick(scope.row)" type="text" size="small"
        >查看</el-button
      >
      <el-button type="text" size="small">编辑</el-button>
    </template>
  </el-table-column>
</el-table>
<script>
  export default {
    methods: {
      handleClick(row) {
        console.log(row)
      }
    },
    data() {
      return {
        tableData: [
          {
            date: '2016-05-02',
            name: '王小虎',
            province: '上海',
            city: '普陀区',
            address: '上海市普陀区金沙江路 1518 弄',
            zip: 200333
          },
          {
            date: '2016-05-04',
            name: '王小虎',
            province: '上海',
            city: '普陀区',
            address: '上海市普陀区金沙江路 1517 弄',
            zip: 200333
          },
          {
            date: '2016-05-01',
            name: '王小虎',
            province: '上海',
            city: '普陀区',
            address: '上海市普陀区金沙江路 1519 弄',
            zip: 200333
          },
          {
            date: '2016-05-03',
            name: '王小虎',
            province: '上海',
            city: '普陀区',
            address: '上海市普陀区金沙江路 1516 弄',
            zip: 200333
          }
        ]
      }
    }
  }
</script>
```
表格组件的扩展
复杂的表格组件需要对表格的显示和操作进行扩展。
首先是从表格的显示上扩展，我们可以支持表头或者某一列的锁定，在滚动的时候锁定列不受影响。一个 table 标签很难实现这个效果，这时候我们就需要分为 table-head 和 table-body 两个组件进行维护，通过 colgroup 组件限制每一列的宽度实现表格的效果，而且表头还需要支持表头嵌套。
下面的示意图中，表头就是被分组显示的。

我们还是先分析一下需求。对于表格的操作来说，首先要和树组件一样，每一样支持复选框进行选中，方便进行批量的操作。另外，表头还需要支持点击事件，点击后对当前这一列实现排序的效果，同时每一列还可能会有详情数据的展开，甚至表格内部还会有树形组件的嵌套、底部的数据显示等等。
把这些需求组合在一起，表格就成了组件库中最复杂的组件。我们需要先分解需求，把组件内部拆分成 table、table-column、table-body、table-header 组件，我们挨个来看一下。
首先，在 table 组件的内部，我们使用 table-body 和 table-header 构成组件。table 提供了整个表格的标签容器；hidden-columns 负责隐藏列的显示，并且通过 table-store 进行表格内部的状态管理。每当 table 中的 table-store 被修改后，table-header、table-body 都需要重新渲染。
```html
<template>
  <div class="el-table">
    <div class="hidden-columns" ref="hiddenColumns">
      <slot></slot>
    </div>
    <div class="el-table__header-wrapper"
         ref="headerWrapper">
      <table-header ref="tableHeader"
                    :store="store">
      </table-header>
    </div>
    <div class="el-table__body-wrapper"
         ref="bodyWrapper">
      <table-body :context="context"
                  :store="store">                  
      </table-body>
    </div>
  </div>
</template>
```
然后在 table 组件的初始化过程中，我们首先使用 createStore 创建表格的 store 数据管理，并且通过 TableLayout 创建表格的布局，然后把 store 通过属性的方式传递给 table-header 和 table-body。
```html
et table = getCurrentInstance()
    const store = createStore(table, {
      rowKey: props.rowKey,
      defaultExpandAll: props.defaultExpandAll,
      selectOnIndeterminate: props.selectOnIndeterminate,
      // TreeTable 的相关配置
      indent: props.indent,
      lazy: props.lazy,
      lazyColumnIdentifier: props.treeProps.hasChildren || 'hasChildren',
      childrenColumnName: props.treeProps.children || 'children',
      data: props.data
    })
    table.store = store
    const layout = new TableLayout({
      store: table.store,
      table,
      fit: props.fit,
      showHeader: props.showHeader
    })
    table.layout = layout
```
再接着，table-header 组件内部会接收传递的 store，并且提供监听的事件，包括 click，mousedown 等鼠标操作后，计算出当前表头的宽高等数据进行显示。
```html
const instance = getCurrentInstance()
    const parent = instance.parent
    const storeData = parent.store.states
    const filterPanels = ref({})
    const {
      tableLayout,
      onColumnsChange,
      onScrollableChange
    } = useLayoutObserver(parent)
    const hasGutter = computed(() => {
      return !props.fixed && tableLayout.gutterWidth
    })
    onMounted(() => {
      nextTick(() => {
        const { prop, order } = props.defaultSort
        const init = true
        parent.store.commit('sort', { prop, order, init })
      })
    })
    const {
      handleHeaderClick,
      handleHeaderContextMenu,
      handleMouseDown,
      handleMouseMove,
      handleMouseOut,
      handleSortClick,
      handleFilterClick
    } = useEvent(props, emit)
    const {
      getHeaderRowStyle,
      getHeaderRowClass,
      getHeaderCellStyle,
      getHeaderCellClass
    } = useStyle(props)
    const { isGroup, toggleAllSelection, columnRows } = useUtils(props)
    instance.state = {
      onColumnsChange,
      onScrollableChange
    }
    // eslint-disable-next-line
    instance.filterPanels = filterPanels
```
在 table-body 中，也是类似的实现方式和效果。不过 table-body 和 table-header 中的定制需求较多，我们需要用 render 函数来实现定制化的需求。
下面的代码中，我们利用 h 函数返回 el-table__body 的渲染，通过 state 中读取的 columns 数据依次进行数据的显示。
```html
render() {
    return h(
      'table',
      {
        class: 'el-table__body',
        cellspacing: '0',
        cellpadding: '0',
        border: '0'
      },
      [
        hColgroup(this.store.states.columns.value),
        h('tbody', {}, [
          data.reduce((acc, row) => {
            return acc.concat(this.wrappedRowRender(row, acc.length))
          }, []),
          h(
            ElTooltip,
            {
              modelValue: this.tooltipVisible,
              content: this.tooltipContent,
              manual: true,
              effect: this.$parent.tooltipEffect,
              placement: 'top'
            },
            {
              default: () => this.tooltipTrigger
            }
          )
        ])
      ]
    )
  }
```
  
整体表格组件的渲染逻辑和过程比较复杂。为了帮你抽丝剥茧，这节课我重点给你说说 Element3 中 table 标签的渲染过程，至于具体的表格实现代码，你可以课后参考 Element3 的源码。
表格组件除了显示的效果非常复杂、交互非常复杂之外，还有一个非常棘手的性能问题。由于表格是二维渲染，而且表格组件如果想支持表头或者某一列锁定的定制效果，内部需要渲染不止一个 table 标签。一旦数据量庞大之后，表格就成了最容易导致性能瓶颈的组件，那这种场景如何去做优化呢？
这里我们要快速回顾一下性能优化那一讲的思路：性能优化主要的思路就是如何能够减少计算量。比如我们的表格如果有 1000 行要显示，但是我们浏览器最多只能显示 100 条，其他的需要通过滚动条的方式进行滚动显示，屏幕之外，成千上万个 dom 元素就成了性能消耗的主要原因。
针对这种情况，我们可以考虑类似图片懒加载的方案，对屏幕之外的 dom 元素做懒渲染，也就是非常常见的虚拟列表解决方案。
在虚拟列表解决方案中，我们首先要获取窗口的高度、元素的高度以及当前滚动的距离，通过这些数据计算出当前屏幕显示出来的数据。然后创建这些元素标签，设置元素的 transform 属性模拟滚动效果。这样表面看是 1000 条数据在表格里显示，实际只渲染了屏幕中间的这 100 行数据，当我们滚动鼠标的同时，去维护这 100 个数据列表，这样就完成了标签过多的性能问题。
如果表格内部每一行的高度不同的话，我们就需要对每一个元素的高度进行估计。具体操作时，先进行渲染，然后等待渲染完毕之后获取高度并且缓存下来，即可实现虚拟列表元素高度的自适应。
总结
今天要我们学习了表格组件如何实现，我给你做个总结吧。
表格组件是组件库中最复杂的组件，核心的难点除了数据的嵌套渲染和复杂的交互之外，复杂的 dom 节点也是表格的特点之一。我们通过对 table-header、table-body 和 table-footer 的组件分析，掌握了表格组件设计思路的实现细节。
除此之外，表格也是最容易导致页面卡顿的组件，所以我们除了数据驱动渲染之外，还需要考虑通过虚拟滚动的方式进行渲染的优化，这也是列表数据常见的优化策略，属于懒渲染的解决方案。
无论数据有多少行，我们只渲染用户可视窗口之内的，控制 top 的属性来模拟滚动效果，通过 computed 计算出需要渲染的数据。最后，我还想提醒你注意，虚拟滚动也是面试的热门解决方案，你一定要手敲一遍才能加深理解。
思考题
最后留个思考题吧，你现在基础的复杂项目或者组件库中，有哪些组件适合用虚拟滚动做性能优化呢？欢迎你在评论区分享你的答案，也欢迎你把这一讲分享给你的同事和朋友们，我们下一讲再见

### 26. 文档:如何给你的组件库设计一个可交互式文档?

文档页面主要包含组件的描述，组件 Demo 示例的展示、描述和代码，并且每个组件都应该有详细的参数文档。

VuePress。它是 Vue 官网团队维护的在线技术文档工具，样式和 Vue 的官方文档保持一致。

Element3 中使用 Markdown-it 进行 Markdown 语法的解析和扩展。Markdown-it 导出一个函数，这个函数可以把 Markdown 语法解析为 HTML 标签。这里我们需要做的就是解析出 Markdown 中的 demo 语法，渲染其中的 Vue 组件，并且同时能把源码也显示在组件下方，这样就完成了扩展任务。

### 27. 自定义渲染器:如何实现 Vue 的跨端渲染?

#### 什么是渲染器

渲染器是围绕虚拟 Dom 存在的。在浏览器中，我们把虚拟 Dom 渲染成真实的 Dom 对象，Vue 源码内部把一个框架里所有和平台相关的操作，抽离成了独立的方法。

在 Vue 3 中的 runtime-core 模块，就对外暴露了这些接口，runtime-core 内部基于这些函数实现了整个 Vue 内部的所有操作，然后在 runtime-dom 中传入以上所有方法。

#### 自定义渲染

自定义渲染器让 Vue 脱离了浏览器的限制，我们只需要实现平台内部的增删改查函数后，就可以直接对接 Vue 3。比方说，我们可以把 Vue 渲染到小程序平台，实现 Vue 3-minipp；也可以渲染到 Canvas，实现 vue 3-canvas，把虚拟 dom 渲染成 Canvas；甚至还可以尝试把 Vue 3 渲染到 threee.js 中，在 3D 世界使用响应式开发。

## 五、Vue 3 生态源码篇

### 28. 响应式:万能面试题，怎么手写响应式系统

Vue3 的组件之间是通过响应式机制来通知的，响应式机制可以自动收集系统中数据的依赖，并且在修改数据之后自动执行更新，极大提高开发的效率。

根据响应式组件通知效果可以知道，响应式机制的主要功能就是，可以把普通的 JavaScript 对象封装成为响应式对象，拦截数据的获取和修改操作，实现依赖数据的自动化更新。

所以，一个最简单的响应式模型，我们可以通过 reactive 或者 ref 函数，把数据包裹成响应式对象，并且通过 effect 函数注册回调函数，然后在数据修改之后，响应式地通知 effect 去执行回调函数即可。


### 29. 运行时: Vue 在浏览器里是怎么跑起来的?

#### 首次渲染

想要启动一个 Vue 项目，只需要从 Vue 中引入 createApp，传入 App 组件，并且调用 createApp 返回的 App 实例的 mount 方法，就实现了项目的启动。

#### patch 函数

patch 传递的是 container._vnode，也就是上一次渲染缓存的 vnode、本次渲染组件的 vnode，以及容器 container。

通过 patch 实现组件的渲染，patch 函数内部根据节点的不同类型，去分别执行 processElement、processComponent、processText 等方法去递归处理不同类型的节点，最终通过 setupComponent 执行组件的 setup 函数，setupRenderEffect 中使用响应式的 effect 函数监听数据的变化。

##### processComponent 方法

那我们继续进入到 processComponent 代码内部，看下面的代码。首次渲染的时候，n1 就是 null，所以会执行 mountComponent；如果是更新组件的时候，n1 就是上次渲染的 vdom，需要执行 updateComponent。

#### setupComponent

首先看 setupComponent，要完成的就是执行我们写的 setup 函数。

内部先初始化了 props 和 slots，并且执行 setupStatefulComponent 创建组件，而这个函数内部从 component 中获取 setup 属性，也就是 script setup 内部实现的函数，就进入到我们组件内部的 reactive、ref 等函数实现的逻辑了。

#### setupRenderEffect

另一个 setupRenderEffect 函数，就是为了后续数据修改注册的函数，我们先梳理一下核心的实现逻辑。

组件首次加载会调用 patch 函数去初始化子组件，注意 setupRenderEffect 本身就是在 patch 函数内部执行的，所以这里就会递归整个虚拟 DOM 树，然后触发生命周期 mounted，完成这个组件的初始化。

页面首次更新结束后，setupRenderEffect 不仅实现了组件的递归渲染，还注册了组件的更新机制。

### 30. 虚拟 DOM(上):如何通过虚拟 DOM 更新页面?

#### Vue 虚拟 DOM 执行流程

在 Vue 中，我们使用虚拟 DOM 来描述页面的组件，比如 template 虽然格式和 HTML 很像，但是在 Vue 的内部会解析成 JavaScript 函数，这个函数就是用来返回虚拟 DOM：

####  DOM 的创建

createVNode 负责创建 Vue 中的虚拟 DOM。

我们给组件注册了 update 方法，这个方法使用 effect 包裹后，当组件内的 ref、reactive 包裹的响应式数据变化的时候就会执行 update 方法，触发组件内部的更新机制。

#### patch 函数

在 patch 函数中，会针对不同的组件类型执行不同的函数，组件我们会执行 processComponent，HTML 标签我们会执行 processElement：

由于更新之后不是首次渲染了，patch 函数内部会执行 updateComponent，看下面的 updateComponent 函数内部，shouldUpdateComponent 会判断组件是否需要更新，实际执行的是 instance.update：

#### patchElement 函数

在函数 patchElement 中我们主要就做两件事，更新节点自己的属性和更新子元素。

#### patchChildren

最后就剩下 patchChildren 的实现了，这也是各类虚拟 DOM 框架中最难实现的函数，我们需要实现一个高效的更新算法，能够使用尽可能少的更新次数，来实现从老的子元素到新的子元素的更新。

### 31. 虚拟 DOM(下):想看懂虚拟 DOM 算法，先刷个算法题

我们将讲到如何使用位运算来实现 Vue 中的按需更新，让静态的节点可以越过虚拟 DOM 的计算逻辑，并且使用计算最长递增子序列的方式，来实现队伍的高效排序。

#### 位运算

方法就是使用 & 操作符来判断操作的类型，比如 `patchFlag & PatchFlags.CLASS` 来判断当前元素的 class 是否需要计算 `diff；shapeFlag & ShapeFlags.ELEMENT` 来判断当前虚拟 DOM 是 HTML 元素还是 Component 组件。这个“&”其实就是位运算的按位与。

这些都是在二进制上的计算，运算的性能通常会比字符串和数字的计算性能要好，这也是很多框架内部使用位运算的原因。

#### 最长递增子系列

贪心算法和二分查找

### 32. 编译原理(上):手写一个迷你 Vue 3 Compiler 的入门原理

首先，代码会被解析成一个对象，这个对象有点像虚拟 DOM 的概念，用来描述 template 的代码关系，这个对象就是抽象语法树（简称 AST，后面我们细讲）。然后通过 transform 模块对代码进行优化，比如识别 Vue 中的语法，静态标记、最后通过 generate 模块生成最终的 render 函数。

理清了流程，我们动手完成具体代码实现。用下面的代码就能实现上述的流程图里的内容。其中 parse 函数负责生成抽象语法树 AST，transform 函数负责语义转换，generate 函数负责最终的代码生成。

我们先来看下 parse 函数如何实现。template 转成 render 函数是两种语法的转换，这种代码转换的需求其实计算机的世界中非常常见。比如我们常用的 Babel，就是把 ES6 的语法转成低版本浏览器可以执行的代码。

#### tokenizer 的迷你实现

首先，我们要对 template 进行词法分析，把模板中的 `<div>`,  `@click`, `{{}}`等语法识别出来，转换成一个个的 token。你可以理解为把 template 的语法进行了分类，这一步我们叫 tokenizer。

下面的代码就是 tokenizer 的迷你实现。我们使用 tokens 数组存储解析的结果，然后对模板字符串进行循环，在 template 中，`<` `>` `/` 和空格都是关键的分隔符，如果碰见 `<` 字符，我们需要判断下一个字符的状态。如果是字符串我们就标记 tagstart；如果是 /，我们就知道是结束标签，标记为 tagend，最终通过 push 方法把分割之后的 token 存储在数组 tokens 中返回。

#### 生成抽象语法树

下面的数组中，我们分别用 tagstart、props tagend 和 text 标记，用它们标记了全部内容。然后下一步我们需要把这个数组按照标签的嵌套关系转换成树形结构，这样才能完整地描述 template 标签的关系。

#### 语义分析和优化

有了抽象语法树之后，我们还要进行语义的分析和优化，也就是说，我们要在这个阶段理解语句要做的事。

### 33. 编译原理(中): Vue Compiler 模块全解析

#### Vue compiler 入口分析

Vue 3 内部有 4 个和 compiler 相关的包。compiler-dom 和 compiler-core 负责实现浏览器端的编译，这两个包是我们需要深入研究的，compiler-ssr 负责服务器端渲染。

#### Vue 浏览器端编译的核心流程

然后，我们进入到 baseCompile 函数中，这就是 Vue 浏览器端编译的核心流程。
下面的代码中可以很清楚地看到，我们先通过 baseParse 把传递的 template 解析成 AST，然后通过 transform 函数对 AST 进行语义化分析，最后通过 generate 函数生成代码。

#### AST 的语义化分析

下一步我们要对 AST 进行语义化的分析。transform 函数的执行流程分支很多，核心的逻辑就是识别一个个的 Vue 的语法，并且进行编译器的优化，我们经常提到的静态标记就是这一步完成的。

#### template 到 render 函数的转化

结合下面的代码我们可以看到，generate 首先通过 createCodegenContext 创建上下文对象，然后通过 genModulePreamble 生成预先定义好的代码模板，然后生成 render 函数，最后生成创建虚拟 DOM 的表达式。

### 34. 编译原理(下):编译原理给我们带来了什么?

#### vite 插件

首先我们在项目中使用了 script setup 来组织我们的代码，虽然组件引入之后有了自动注册的功能，但是每一个组件内部都肯定要用到 ref、computed 等 Vue 提供的 API。我们还想要多一步，项目大了只引入 ref 的语句就写了几百行，就会非常地繁琐，这时候就可以使用编译的思想来解决这个问题。

#### Babel

我们在项目中异步的任务有很多，经常使用 async+ await 的语法执行异步任务，比如网络数据的获取。但 await 是异步任务，如果报错，我们需要使用 try catch 语句进行错误处理，每个 catch 语句都是一个打印语句会让代码变得冗余，但我们有了代码转化的思路后，这一步就能用编译的思路自动来完成。

### 35. Vite 原理:写一个迷你的 Vite

### 36. 数据流原理: Vuex & Pinia 源码剖析

### 37. 前端路由原理: vue- -router 源码剖析

### 38. 服务端渲染原理: Vue 3 中的 SSR 是如何实现的?

## Vue 3 生态源码到底给我们带来了什么?
