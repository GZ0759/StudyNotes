> Vue.js 组件精讲  
> Aresn iView 的作者 《Vue.js实战》的作者  

# 0 开篇：Vue.js 的精髓——组件

## 0.1 组件的分类

一般来说，Vue.js 组件主要分成三类：

1. 由 `vue-router` 产生的每个页面，它本质上也是一个组件（.vue），主要承载当前页面的 HTML 结构，会包含数据获取、数据整理、数据可视化等常规业务。整个文件相对较大，但一般不会有 `props` 选项和 `自定义事件`，因为它作为路由的渲染，不会被复用，因此也不会对外提供接口。

2. 不包含业务，独立、具体功能的基础组件，比如日期选择器、模态框等。这类组件作为项目的基础控件，会被大量使用，因此组件的 API 进行过高强度的抽象，可以通过不同配置实现不同的功能。比如笔者开源的 iView，就是包含了 50 多个这样基础组件的 UI 组件库。

3. 业务组件。它不像第二类独立组件只包含某个功能，而是在业务中被多个页面复用的，它与独立组件的区别是，业务组件只在当前项目中会用到，不具有通用性，而且会包含一些业务，比如数据请求；而独立组件不含业务，在任何项目中都可以使用，功能单一，比如一个具有数据校验功能的输入框。

## 0.2 小册的内容

因为本小册是围绕 Vue.js 组件展开的，所以第二节会讲解 Vue.js 组件的三个 API：`prop`、`event`、`slot`。

- 3 - 7 小节会介绍组件间通信的一些方法和黑科技，一部分是 Vue.js 内置的，一部分是自行实现的，在实际开发中，会非常实用。例如具有数据校验功能的表单组件（Form）和组合多选框组件（CheckboxGroup & Checkbox）。

- 8 - 10 小节介绍 Vue 的构造器 extend 和手动挂载组件 $mount 的用法及案例。Vue.js 除了我们正常 `new Vue()` 外，还可以手动挂载的，例如动态渲染 .vue 文件的组件（Display）和全局通知组件（$Alert）。

- 11 - 12 小节介绍 Render 函数与 Functional Render，并完成一个能够渲染自定义列的 Table 组件。Render 函数也是 Vue.js 组件重要的一部分，只不过在大多数业务中不常使用。本小节会介绍它的使用场景。

- 13 小节介绍作用域 slot（slot-scope），并基于这种方法同样实现 Table 组件。slot 用的很多，但 slot-scope  在业务中并不常用，但在一些特定场景下，比如组件内部有循环体时，会非常实用。

- 14 - 15 小节介绍递归组件，并完成树形控件（Tree）。

- 16 - 19 小节是综合拓展，会着重讲解 Vue.js 容易忽略却很重要的 API，以及对 Vue.js 面试题的详细分析。除此之外，还会总结笔者在两年的 iView 开源经历中的经验，除了技术细节外，还包括开源项目的持续性发展、推广等。

# 1 基础：Vue.js 组件的三个 API：prop、event、slot

## 1.1 组件的构成

一个再复杂的组件，都是由三部分组成的：prop、event、slot，它们构成了 Vue.js 组件的 API。如果开发的是一个通用组件，那一定要事先设计好这三部分，因为组件一旦发布，后面再修改 API 就很困难了，使用者都是希望不断新增功能，修复 bug，而不是经常变更接口。

### 1.1.1 属性 prop 

`prop` 定义了这个组件有哪些可配置的属性，组件的核心功能也都是它来确定的。写通用组件时，props 最好用对象的写法，这样可以针对每个属性设置类型、默认值或自定义校验属性的值，这点在组件开发中很重要，然而很多人却忽视，直接使用 props 的数组用法，这样的组件往往是不严谨的。比如我们封装一个按钮组件 `<i-button>`：

```html
<template>
  <button :class="'i-button-size' + size" :disabled="disabled"></button>
</template>
<script>
  // 判断参数是否是其中之一
  function oneOf (value, validList) {
    for (let i = 0; i < validList.length; i++) {
      if (value === validList[i]) {
        return true;
      }
    }
    return false;
  }

  export default {
    props: {
      size: {
        validator (value) {
          return oneOf(value, ['small', 'large', 'default']);
        },
        default: 'default'
      },
      disabled: {
        type: Boolean,
        default: false
      }
    }
  }
</script>
```

使用组件：

```html
<i-button size="large"></i-button>
<i-button disabled></i-button>
```

组件中定义了两个属性：尺寸 size 和 是否禁用 disabled。其中 size 使用 `validator` 进行了值的自定义验证，也就是说，从父级传入的 size，它的值必须是指定的 small、large、default 中的一个，默认值是 default，如果传入这三个以外的值，都会抛出一条警告。

要注意的是，组件里定义的 props，都是单向数据流，也就是只能通过父级修改，组件自己不能修改 props 的值，只能修改定义在 data 里的数据，非要修改，也是通过后面介绍的自定义事件通知父级，由父级来修改。

在使用组件时，也可以传入一些标准的 html 特性，比如 id、class：

```html
<i-button id="btn1" class="btn-submit"></i-button>
```

这样的 html 特性，在组件内的 `<button>` 元素上会继承，并不需要在 props 里再定义一遍。这个特性是默认支持的，如果不期望开启，在组件选项里配置 `inheritAttrs: false` 就可以禁用了。

### 1.1.2 插槽 slot

如果要给上面的按钮组件 `<i-button>` 添加一些文字内容，就要用到组件的第二个 API：插槽 slot，它可以分发组件的内容，比如在上面的按钮组件中定义一个插槽：

```html
<template>
  <button :class="'i-button-size' + size" :disabled="disabled">
    <slot></slot>
  </button>
</template>
```

这里的 `<slot>` 节点就是指定的一个插槽的位置，这样在组件内部就可以扩展内容了：

```html
<i-button>按钮 1</i-button>
<i-button>
  <strong>按钮 2</strong>
</i-button>
```

当需要多个插槽时，会用到具名 slot，比如上面的组件我们再增加一个 slot，用于设置另一个图标组件：

```html
<template>
  <button :class="'i-button-size' + size" :disabled="disabled">
    <slot name="icon"></slot>
    <slot></slot>
  </button>
</template>
```

```html
<i-button>
  <i-icon slot="icon" type="checkmark"></i-icon>
  按钮 1
</i-button>
```

这样，父级内定义的内容，就会出现在组件对应的 slot 里，没有写名字的，就是默认的 slot。

在组件的 `<slot>` 里也可以写一些默认的内容，这样在父级没有写任何 slot 时，它们就会出现，比如：

```html
<slot>提交</slot>
```

### 1.1.3 自定义事件 event

现在我们给组件 `<i-button>` 加一个点击事件，目前有两种写法，我们先看自定义事件 event（部分代码省略）：

```html
<template>
  <button @click="handleClick">
    <slot></slot>
  </button>
</template>
<script>
  export default {
    methods: {
      handleClick (event) {
        this.$emit('on-click', event);
      }
    }
  }
</script>
```

通过 `$emit`，就可以触发自定义的事件 `on-click` ，在父级通过 `@on-click` 来监听：

```html
<i-button @on-click="handleClick"></i-button>
```

上面的 click 事件，是在组件内部的 `<button>` 元素上声明的，这里还有另一种方法，直接在父级声明，但为了区分原生事件和自定义事件，要用到事件修饰符 `.native`，所以上面的示例也可以这样写：

```html
<i-button @click.native="handleClick"></i-button>
```

如果不写 `.native` 修饰符，那上面的 `@click` 就是自定义事件 click，而非原生事件 click，但我们在组件内只触发了 `on-click` 事件，而不是 `click`，所以直接写 `@click` 会监听不到。

## 1.2 组件的通信

一般来说，组件可以有以下几种关系：

![组件关系](https://user-gold-cdn.xitu.io/2018/10/18/166864d066bbcf69?w=790&h=632&f=png&s=36436)

A 和 B、B 和 C、B 和 D 都是父子关系，C 和 D 是兄弟关系，A 和 C 是隔代关系（可能隔多代）。组件间经常会通信，Vue.js 内置的通信手段一般有两种：

- `ref`：给元素或组件注册引用信息；
- `$parent` / `$children`：访问父 / 子实例。

这两种都是直接得到组件实例，使用后可以直接调用组件的方法或访问数据，比如下面的示例中，用 ref 来访问组件（部分代码省略）：

```js
// component-a
export default {
  data () {
    return {
      title: 'Vue.js'
    }
  },
  methods: {
    sayHello () {
      window.alert('Hello');
    }
  }
}
```

```html
<template>
  <component-a ref="comA"></component-a>
</template>
<script>
  export default {
    mounted () {
      const comA = this.$refs.comA;
      console.log(comA.title);  // Vue.js
      comA.sayHello();  // 弹窗
    }
  }
</script>
```

`$parent` 和 `$children` 类似，也是基于当前上下文访问父组件或全部子组件的。

这两种方法的弊端是，无法在跨级或兄弟间通信，比如下面的结构：

```js
// parent.vue
<component-a></component-a>
<component-b></component-b>
<component-b></component-b>
```

我们想在 component-a 中，访问到引用它的页面中（这里就是 parent.vue）的两个 component-b 组件，那这种情况下，就得配置额外的插件或工具了，比如 Vuex 和 Bus 的解决方案，本小册不再做它们的介绍，读者可以自行阅读相关内容。不过，它们都是依赖第三方插件的存在，这在开发独立组件时是不可取的，而在小册的后续章节，会陆续介绍一些黑科技，它们完全不依赖任何三方插件，就可以轻松得到任意的组件实例，或在任意组件间进行通信，且适用于任意场景。

# 2 组件的通信 1：provide / inject

## 2.1 什么是 provide / inject

这对选项需要一起使用，以允许一个祖先组件向其所有子孙后代注入一个依赖，不论组件层次有多深，并在起上下游关系成立的时间里始终生效。如果熟悉 React，这与 React 的上下文特性很相似。provide 和 inject 主要为高阶插件/组件库提供用例。并不推荐直接用于应用程序代码中。

```js
// A.vue
export default {
  provide: {
    name: 'Aresn'
  }
}

// B.vue
// B为A的子组件
export default {
  inject: ['name'],
  mounted () {
    console.log(this.name);  // Aresn
  }
}
```

值得注意的是，provide 和 inject 绑定并不是可响应的。然而，如果传入了一个可监听的对象，那么其对象的属性还是可响应的。

## 2.2 替代 Vuex

状态管理 Vuex 是一个专为 Vue.js 开发的状态管理模式，用于集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

使用 Vuex，最主要的目的是跨组件通信、全局数据维护、多人协同开发。需求比如有：用户的登录信息维护、通知信息维护等全局的状态和数据。

将 app.vue 理解为一个最外层的根组件，用来存储所有需要的全局数据和状态，甚至是计算属性（computed）、方法（methods）等。因为你的项目中所有的组件（包含路由），它的父组件（或根组件）都是 app.vue，所以我们把整个 app.vue 实例通过 `provide` 对外提供。

```html
<!-- app.vue -->
<script>
  export default {
    provide () {
      return {
        app: this
      }
    },
    data () {
      return {
        userInfo: null
      }
    },
    methods: {
      getUserInfo () {
        // 这里通过 ajax 获取用户信息后，赋值给 this.userInfo，以下为伪代码
        $.ajax('/user/info', (data) => {
          this.userInfo = data;
        });
      }
    },
    mounted () {
      this.getUserInfo();
    }
  }
</script>
```

```html
<!-- 子组件 -->
<template>
  <div>
    {{ app.userInfo }}
  </div>
</template>
<script>
  export default {
    inject: ['app'],
    methods: {
      changeUserInfo () {
        // 这里修改完用户数据后，通知 app.vue 更新，以下为伪代码
        $.ajax('/user/update', () => {
          // 直接通过 this.app 就可以调用 app.vue 里的方法
          this.app.getUserInfo();
        })
      }
    }
  }
</script>
```

## 3.3 进阶技巧

如果项目足够复杂，或需要多人协同开发时，在 `app.vue` 里会写非常多的代码，多到结构复杂难以维护。这时可以使用 Vue.js 的混合 `mixins`，将不同的逻辑分开到不同的 js 文件里。

```js
// user.js
export default {
  data () {
    return {
      userInfo: null
    }
  },
  methods: {
    getUserInfo () {
      // 这里通过 ajax 获取用户信息后，赋值给 this.userInfo，以下为伪代码
      $.ajax('/user/info', (data) => {
        this.userInfo = data;
      });
    }
  },
  mounted () {
    this.getUserInfo();
  }
}
```

```html
<!-- app.vue -->
<script>
  import mixins_user from '../mixins/user.js';

  export default {
    mixins: [mixins_user],
    data () {
      return {

      }
    }
  }
</script>
```

## 3.4 独立组件中使用

只要一个组件使用了 `provide` 向下提供数据，那其下所有的子组件都可以通过 `inject` 来注入，不管中间隔了多少代，而且可以注入多个来自不同父级提供的数据。需要注意的是，一旦注入了某个数据，比如上面示例中的 `app`，那这个组件中就不能再声明 `app` 这个数据了，因为它已经被父级占有。

独立组件使用 provide / inject 的场景，主要是具有联动关系的组件，比如接下来很快会介绍的第一个实战：具有数据校验功能的表单组件 Form。它其实是两个组件，一个是 Form，一个是 FormItem，FormItem 是 Form 的子组件，它会依赖 Form 组件上的一些特性（props），所以就需要得到父组件 Form，这在 Vue.js 2.2.0 版本以前，是没有 provide / inject 这对 API 的，而 Form 和 FormItem 不一定是父子关系，中间很可能间隔了其它组件，所以不能单纯使用 `$parent` 来向上获取实例。在 Vue.js 2.2.0 之前，一种比较可行的方案是用计算属性动态获取：

```js
computed: {
  form () {
    let parent = this.$parent;
    while (parent.$options.name !== 'Form') {
      parent = parent.$parent;
    }
    return parent;
  }
}
```

每个组件都可以设置 `name` 选项，作为组件名的标识，利用这个特点，通过向上遍历，直到找到需要的组件。这个方法可行，但相比一个 `inject` 来说，太费劲了，而且不那么优雅和 native。如果用 inject，可能只需要一行代码：

```js
export default {
  inject: ['form']
}
```

# 3 组件的通信 2：派发与广播——自行实现 dispatch 和 broadcast 方法

上一讲的 provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。然后有两种场景它不能很好的解决：

- 父组件向子组件（支持跨级）传递数据；
- 子组件向父组件（支持跨级）传递数据。

这种父子（含跨级）传递数据的通信方式，Vue.js 并没有提供原生的 API 来支持，而是推荐使用大型数据状态管理工具 Vuex，而我们之前已经介绍过 Vuex 的场景与在独立组件（或库）中使用的限制。本小节则介绍一种在父子组件间通信的方法 `dispatch` 和 `broadcast`。

## \$on 与 \$emit

如果您使用过较早的 Vue.js 1.x 版本，肯定对 `$dispatch` 和 `$broadcast` 这两个内置的方法很熟悉，不过它们都在 Vue.js 2.x 里废弃了。在正式介绍主角前，我们先看看 `$on` 与 `$emit` 这两个 API，因为它们是本节内容的基础。

`$emit` 会在**当前组件**实例上触发自定义事件，并传递一些参数给监听器的回调，一般来说，都是在父级调用这个组件时，使用 `@on` 的方式来监听自定义事件的，比如在子组件中触发事件：

```js
// child.vue，部分代码省略
export default {
  methods: {
    handleEmitEvent () {
      this.$emit('test', 'Hello Vue.js');
    }
  }
}
```

在父组件中监听由 *child.vue* 触发的自定义事件 **test**：

```html
<!-- parent.vue，部分代码省略-->
<template>
  <child-component @test="handleEvent">
</template>
<script>
  export default {
    methods: {
      handleEvent (text) {
      	console.log(text);  // Hello Vue.js
      }
    }
  }
</script>
```

这里看似是在父组件 *parent.vue* 中绑定的自定义事件 **test** 的处理句柄，然而事件 test 并不是在父组件上触发的，而是在子组件 *child.vue* 里触发的，只是通过 `v-on` 在父组件中监听。既然是子组件自己触发的，那它自己也可以监听到，这就要使用 `$on` 来监听实例上的事件，换言之，组件使用 `$emit` 在自己实例上触发事件，并用 `$on` 监听它。

听起来这种神（sāo）操作有点多此一举，我们不妨先来看个示例：

（也可通过在线链接 [https://run.iviewui.com/ggsomfHM](https://run.iviewui.com/ggsomfHM) 直接运行该示例）

```html
<template>
  <div>
    <button @click="handleEmitEvent">触发自定义事件</button>
  </div>
</template>
<script>
  export default {
    methods: {
      handleEmitEvent () {
        // 在当前组件上触发自定义事件 test，并传值
        this.$emit('test', 'Hello Vue.js')
      }
    },
    mounted () {
      // 监听自定义事件 test
      this.$on('test', (text) => {
        window.alert(text);
      });
    }
  }
</script>
```

`$on` 监听了自己触发的自定义事件 test，因为有时不确定何时会触发事件，一般会在 `mounted` 或 `created` 钩子中来监听。

仅上面的示例，的确是多此一举的，因为大可在 handleEmitEvent 里直接写 `window.alert(text)`，没必要绕一圈。

之所以多此一举，是因为 handleEmitEvent 是当前组件内的 `<button>` 调用的，如果这个方法不是它自己调用，而是其它组件调用的，那这个用法就大有可为了。

了解了 `$on` 和 `$emit` 的用法后，我们再来看两个“过时的” API。

## Vue.js 1.x 的 \$dispatch 与 \$broadcast

虽然 Vue.js 1.x 已经成为过去时，但为了充分理解本节通信方法的使用场景，还是有必要来了解一点它的历史。

在 Vue.js 1.x 中，提供了两个方法：`$dispatch` 和 `$broadcast` ，前者用于向上级派发事件，只要是它的父级（一级或多级以上），都可以在组件内通过 `$on` （或 events，2.x 已废弃）监听到，后者相反，是由上级向下级广播事件的。

来看一个简单的示例：

```html
<!-- 注意：该示例为 Vue.js 1.x 版本 -->
<!-- 子组件 -->
<template>
  <button @click="handleDispatch">派发事件</button>
</template>
<script>
export default {
  methods: {
    handleDispatch () {
      this.$dispatch('test', 'Hello, Vue.js');
    }
  }
}
</script>
```

```html
<!-- 父组件，部分代码省略 -->
<template>
  <child-component></child-component>
</template>
<script>
  export default {
    mounted () {
      this.$on('test', (text) => {
        console.log(text);  // Hello, Vue.js
      });
    }
  }
</script>
```

`$broadcast` 类似，只不过方向相反。这两种方法一旦发出事件后，任何组件都是可以接收到的，就近原则，而且会在第一次接收到后停止冒泡，除非返回 true。

这两个方法虽然看起来很好用，但是在 Vue.js 2.x 中都废弃了，官方给出的解释是：

> 因为基于组件树结构的事件流方式有时让人难以理解，并且在组件结构扩展的过程中会变得越来越脆弱。

虽然在业务开发中，它没有 Vuex 这样专门管理状态的插件清晰好用，但对独立组件（库）的开发，绝对是福音。因为独立组件一般层级并不会很复杂，并且剥离了业务，不会变的难以维护。

知道了 `$dispatch` 和 `$broadcast` 的前世今生，接下来我们就在 Vue.js 2.x 中自行实现这两个方法。

## 自行实现 dispatch 和 broadcast 方法

自行实现的 dispatch 和 broadcast 方法，不能保证跟 Vue.js 1.x 的  `$dispatch` 和 `$broadcast` 具有完全相同的体验，但基本功能是一样的，都是解决父子组件（含跨级）间的通信问题。

通过目前已知的信息，我们要实现的 dispatch 和 broadcast 方法，将具有以下功能：

- 在子组件调用 dispatch 方法，向上级指定的组件实例（最近的）上触发自定义事件，并传递数据，且该上级组件已预先通过 `$on` 监听了这个事件；
- 相反，在父组件调用 broadcast 方法，向下级指定的组件实例（最近的）上触发自定义事件，并传递数据，且该下级组件已预先通过 `$on` 监听了这个事件。

实现这对方法的关键点在于，如何正确地向上或向下找到对应的组件实例，并在它上面触发方法。在设计一个新功能（features）时，可以先确定这个功能的 API 是什么，也就是说方法名、参数、使用样例，确定好 API，再来写具体的代码。

因为 Vue.js 内置的方法，才是以 `$` 开头的，比如 `$nextTick`、`$emit` 等，为了避免不必要的冲突并遵循规范，这里的 dispatch 和 broadcast 方法名前不加 `$`。并且该方法可能在很多组件中都会使用，复用起见，我们封装在混合（mixins）里。那它的使用样例可能是这样的：

```js
// 部分代码省略
import Emitter from '../mixins/emitter.js'

export default {
  mixins: [ Emitter ],
  methods: {
    handleDispatch () {
      this.dispatch();  // ①
    },
    handleBroadcast () {
      this.broadcast();  // ②
    }
  }
}
```

上例中行 ① 和行 ② 的两个方法就是在导入的混合 **emitter.js** 中定义的，这个稍后我们再讲，先来分析这两个方法应该传入什么参数。一般来说，为了跟 Vue.js 1.x 的方法一致，第一个参数应当是自定义事件名，比如 “test”，第二个参数是传递的数据，比如 “Hello, Vue.js”，但在这里，有什么问题呢？只通过这两个参数，我们没办法知道要在哪个组件上触发事件，因为自行实现的这对方法，与 Vue.js 1.x 的原生方法机理上是有区别的。上文说到，实现这对方法的关键点在于准确地**找到组件实例**。那在寻找组件实例上，我们的“惯用伎俩”就是通过遍历来匹配组件的 `name` 选项，在独立组件（库）里，每个组件的 `name` 值应当是唯一的，name 主要用于递归组件，在后面小节会单独介绍。

先来看下 **emitter.js** 的代码：

```js
function broadcast(componentName, eventName, params) {
  this.$children.forEach(child => {
    const name = child.$options.name;

    if (name === componentName) {
      child.$emit.apply(child, [eventName].concat(params));
    } else {
      broadcast.apply(child, [componentName, eventName].concat([params]));
    }
  });
}
export default {
  methods: {
    dispatch(componentName, eventName, params) {
      let parent = this.$parent || this.$root;
      let name = parent.$options.name;

      while (parent && (!name || name !== componentName)) {
        parent = parent.$parent;

        if (parent) {
          name = parent.$options.name;
        }
      }
      if (parent) {
        parent.$emit.apply(parent, [eventName].concat(params));
      }
    },
    broadcast(componentName, eventName, params) {
      broadcast.call(this, componentName, eventName, params);
    }
  }
};
```

因为是用作 mixins 导入，所以在 methods 里定义的 dispatch 和 broadcast 方法会被混合到组件里，自然就可以用 `this.dispatch` 和 `this.broadcast` 来使用。

这两个方法都接收了三个参数，第一个是组件的 `name` 值，用于向上或向下递归遍历来寻找对应的组件，第二个和第三个就是上文分析的自定义事件名称和要传递的数据。

可以看到，在 dispatch 里，通过 *while* 语句，不断向上遍历更新当前组件（即上下文为当前调用该方法的组件）的父组件实例（变量 parent 即为父组件实例），直到匹配到定义的 `componentName` 与某个上级组件的 `name` 选项一致时，结束循环，并在找到的组件实例上，调用 `$emit` 方法来触发自定义事件 `eventName`。broadcast 方法与之类似，只不过是向下遍历寻找。

来看一下具体的使用方法。有 **A.vue** 和 **B.vue** 两个组件，其中 B 是 A 的子组件，中间可能跨多级，在 A 中向 B 通信：

```html
<!-- A.vue -->
<template>
	<button @click="handleClick">触发事件</button>
</template>
<script>
  import Emitter from '../mixins/emitter.js';
  
  export default {
    name: 'componentA',
    mixins: [ Emitter ],
    methods: {
      handleClick () {
        this.broadcast('componentB', 'on-message', 'Hello Vue.js');
      }
    }
  }
</script>
```

```js
// B.vue
export default {
  name: 'componentB',
  created () {
    this.$on('on-message', this.showMessage);
  },
  methods: {
    showMessage (text) {
      window.alert(text);
    }
  }
}
```

同理，如果是 B 向 A 通信，在 B 中调用 dispatch 方法，在 A 中使用 `$on` 监听事件即可。

以上就是自行实现的 dispatch 和 broadcast 方法，相比 Vue.js 1.x，有以下不同：

- 需要额外传入组件的 name 作为第一个参数；
- 无冒泡机制；
- 第三个参数传递的数据，只能是一个（较多时可以传入一个对象），而 Vue.js 1.x 可以传入多个参数，当然，你对 emitter.js 稍作修改，也能支持传入多个参数，只是一般场景传入一个对象足以。

## 结语

Vue.js 的组件通信到此还没完全结束，如果你想“趁热打铁”一口气看完，可以先阅读第 6 节组件的通信 3。亦或按顺序看下一节的实战，来进一步加深理解 provide / inject 和 dispatch / broadcast 这两对通信方法的使用场景。

注：本节部分代码参考 [iView](https://github.com/iview/iview/blob/2.0/src/mixins/emitter.js)。

# 4 实战 1：具有数据校验功能的表单组件——Form

在第 3 节和第 4 节中，我们介绍了组件间的两种通信方法：provide / inject 和 dispatch / broadcast，前者是 Vue.js 内置的，主要用于子组件获取父组件（包括跨级）的状态；后者是自行实现的一种混合，用于父子组件（包括跨级）间通过自定义事件通信。本小节则基于这两种通信方法，来实现一个具有数据校验功能的表单组件——Form。

## Form 组件概览

表单类组件在项目中会大量使用，比如输入框（Input）、单选（Radio）、多选（Checkbox）、下拉选择器（Select）等。在使用表单类组件时，也会经常用到数据校验，如果每次都写校验程序来对每一个表单控件校验，会很低效，因此需要一个能够校验基础表单控件的组件，也就是本节要完成的 Form 组件。一般的组件库都提供了这个组件，比如 iView，它能够校验内置的 15 种控件，且支持校验自定义组件，如下图所示：

（也可以在线访问本示例体验：[https://run.iviewui.com/jwrqnFss](https://run.iviewui.com/jwrqnFss)）


![](https://user-gold-cdn.xitu.io/2018/10/30/166c3b75c37ef9a8?w=900&h=958&f=gif&s=1820338)

Form 组件分为两个部分，一个是外层的 `Form` 表单域组件，一组表单控件只有一个 Form，而内部包含了多个 `FormItem` 组件，每一个表单控件都被一个 FormItem 包裹。基本的结构看起来像：

```html
<i-form>
  <i-form-item>
    <i-input v-model="form.name"></i-input>
  </i-form-item>
  <i-form-item>
    <i-input v-model="form.mail"></i-input>
  </i-form-item>
</i-form>
```

Form 要用到数据校验，并在对应的 FormItem 中给出校验失败的提示，校验我们会用到一个开源库：[async-validator](https://github.com/yiminghe/async-validator)，基本主流的组件库都是基于它做的校验。使用它很简单，只需按要求写好一个校验规则就好，比如：

```js
[
  { required: true, message: '邮箱不能为空', trigger: 'blur' },
  { type: 'email', message: '邮箱格式不正确', trigger: 'blur' }
]
```

这个代表要校验的数据先判断是否为空（required: true），如果为空，则提示“邮箱不能为空”，触发校验的事件为失焦（trigger: 'blur'），如果第一条满足要求，再进行第二条的验证，判断是否为邮箱格式（type: 'email'）等等，还支持自定义校验规则。更详细的用法可以参看它的文档。

## 接口设计

我们先使用最新的 Vue CLI 3 创建一个空白的项目（如果你还不清楚 Vue CLI 3 的用法，需要先补习一下了，可以阅读文末的扩展阅读 1），并使用 `vue-router` 插件，同时安装好 `async-validator` 库。

在 `src/components` 下新建一个 `form` 文件夹，并初始化两个组件 `form.vue` 和 `form-item.vue`，然后初始化项目，配置路由，创建一个页面能够被访问到。

> 本节所有代码可以在 [https://github.com/icarusion/vue-component-book](https://github.com/icarusion/vue-component-book) 中查看，你可以一边看源码，一边阅读本节；也可以边阅读，边动手实现一遍，遇到问题再参考完整的源码。

第 2 节我们介绍到，编写一个 Vue.js 组件，最重要的是设计好它的接口，一个 Vue.js 组件的接口来自三个部分：props、slots、events。而 Form 和 FormItem 两个组件主要做数据校验，用不到 events。Form 的 slot 就是一系列的 FormItem，FormItem 的 slot 就是具体的表单控件，比如输入框 `<i-input>` 。那主要设计的就是 props 了。

在 `Form` 组件中，定义两个 props：

- model：表单控件绑定的数据对象，在校验或重置时会访问该数据对象下对应的表单数据，类型为 Object。
- rules：表单验证规则，即上面介绍的 async-validator 所使用的校验规则，类型为 Object。

在 `FormItem` 组件中，也定义两个 props：

- label：单个表单组件的标签文本，类似原生的 `<label>` 元素，类型为 String。
- prop：对应表单域 Form 组件 model 里的字段，用于在校验或重置时访问表单组件绑定的数据，类型为 String。

定义好 props，就可以写出大概的用例了：

```html
<template>
  <div>
    <i-form :model="formValidate" :rules="ruleValidate">
      <i-form-item label="用户名" prop="name">
        <i-input v-model="formValidate.name"></i-input>
      </i-form-item>
      <i-form-item label="邮箱" prop="mail">
        <i-input v-model="formValidate.mail"></i-input>
      </i-form-item>
    </i-form>
  </div>
</template>
<script>
  import iForm from '../components/form/form.vue';
  import iFormItem from '../components/form/form-item.vue';
  import iInput from '../components/input/input.vue';

  export default {
    components: { iForm, iFormItem, iInput },
    data () {
      return {
        formValidate: {
          name: '',
          mail: ''
        },
        ruleValidate: {
          name: [
            { required: true, message: '用户名不能为空', trigger: 'blur' }
          ],
          mail: [
            { required: true, message: '邮箱不能为空', trigger: 'blur' },
            { type: 'email', message: '邮箱格式不正确', trigger: 'blur' }
          ],
        }
      }
    }
  }
</script>
```

有两点需要注意的是：

1. 这里的 `<i-input>` 并不是原生的 `<input>` 输入框，而是一个特制的输入框组件，之后会介讲解的功能和代码；
2. `<i-form-item>` 的属性 `prop` 是字符串，所以它前面没有冒号（即不是 `:prop="name"`）。

当前的两个组件只是个框框，还没有实现任何功能，不过万事开头难，定义好接口，剩下的就是补全组件的逻辑，而对于使用者，知道了 props、events、slots，就已经能写出上例的使用代码了。

到此，Form 和 FormItem 的代码如下：

```html
<!-- form.vue -->
<template>
  <form>
    <slot></slot>
  </form>
</template>
<script>
  export default {
    name: 'iForm',
    props: {
      model: {
        type: Object
      },
      rules: {
        type: Object
      }
    }
  }
</script>
```

```html
<!-- form-item.vue -->
<template>
  <div>
    <label v-if="label">{{ label }}</label>
    <div>
      <slot></slot>
    </div>
  </div>
</template>
<script>
  export default {
    name: 'iFormItem',
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: {
        type: String
      }
    }
  }
</script>
```

## 在 Form 中缓存 FormItem 实例

`Form` 组件的核心功能是数据校验，一个 Form 中包含了多个 FormItem，当点击提交按钮时，要逐一对每个 FormItem 内的表单组件校验，而校验是由使用者发起，并通过 `Form` 来调用每一个 `FormItem` 的验证方法，再将校验结果汇总后，通过 `Form` 返回出去。大致的流程如下图所示：


![](https://user-gold-cdn.xitu.io/2018/10/30/166c3b7f124cb84a?w=1046&h=610&f=png&s=42610)

因为要在 Form 中逐一调用 FormItem 的验证方法，而 Form 和 FormItem 是独立的，需要预先将 FormItem 的每个实例缓存在 Form 中，这个操作就需要用到第 4 节的组件通信方法。当每个 FormItem 渲染时，将其自身（this）作为参数通过 `dispatch` 派发到 Form 组件中，然后通过一个数组缓存起来；同理当 FormItem 销毁时，将其从 Form 缓存的数组中移除。相关代码如下：

```js
// form-item.vue，部分代码省略

import Emitter from '../../mixins/emitter.js';

export default {
  name: 'iFormItem',
  mixins: [ Emitter ],
  // 组件渲染时，将实例缓存在 Form 中
  mounted () {
    // 如果没有传入 prop，则无需校验，也就无需缓存
    if (this.prop) {
      this.dispatch('iForm', 'on-form-item-add', this);
    }
  },
  // 组件销毁前，将实例从 Form 的缓存中移除
  beforeDestroy () {
    this.dispatch('iForm', 'on-form-item-remove', this);
  }
}
```

注意，Vue.js 的组件渲染顺序是由内而外的，所以 FormItem 要先于 Form 渲染，在 FormItem 的 mounted 触发时，我们向 Form 派发了事件 `on-form-item-add`，并将当前 FormItem 的实例（this）传递给了 Form，而此时，Form 的 mounted 尚未触发，因为 Form 在最外层，如果在 Form 的 mounted 里监听事件，是不可以的，所以要在其 created 内监听自定义事件，Form 的 created 要先于 FormItem 的 mounted。所以 Form 的相关代码为：

```js
// form.vue，部分代码省略
export default {
  name: 'iForm',
  data () {
    return {
      fields: []
    };
  },
  created () {
    this.$on('on-form-item-add', (field) => {
      if (field) this.fields.push(field);
    });
    this.$on('on-form-item-remove', (field) => {
      if (field.prop) this.fields.splice(this.fields.indexOf(field), 1);
    });
  }
}
```

定义的数据 `fields` 就是用来缓存所有 FormItem 实例的。

## 触发校验

Form 支持两种事件来触发校验：

- **blur**：失去焦点时触发，常见的有输入框失去焦点时触发校验；
- **change**：实时输入时触发或选择时触发，常见的有输入框实时输入时触发校验、下拉选择器选择项目时触发校验等。

以上两个事件，都是有具体的表单组件来触发的，我们先来编写一个简单的输入框组件 `i-input`。在 `components` 下新建目录 `input`，并创建文件 `input.vue`：

```html
<!-- input.vue -->
<template>
  <input
    type="text"
    :value="currentValue"
    @input="handleInput"
    @blur="handleBlur"
    />
</template>
<script>
  import Emitter from '../../mixins/emitter.js';

  export default {
    name: 'iInput',
    mixins: [ Emitter ],
    props: {
      value: {
        type: String,
        default: ''
      },
    },
    data () {
      return {
        currentValue: this.value
      }
    },
    watch: {
      value (val) {
        this.currentValue = val;
      }
    },
    methods: {
      handleInput (event) {
        const value = event.target.value;
        this.currentValue = value;
        this.$emit('input', value);
        this.dispatch('iFormItem', 'on-form-change', value);
      },
      handleBlur () {
        this.dispatch('iFormItem', 'on-form-blur', this.currentValue);
      }
    }
  }
</script>
```

Input 组件中，绑定在 `<input>` 元素上的原生事件 `@input`，每当输入一个字符，都会调用句柄 `handleInput`，并通过 `dispatch` 方法向上级的 FormItem 组件派发自定义事件 `on-form-change`；同理，绑定的原生事件 `@blur`  会在 input 失焦时触发，并传递事件 `on-form-blur`。

基础组件有了，接下来要做的，是在 FormItem 中监听来自 Input 组件派发的自定义事件。这里可以在 mounted 中监听，因为你的手速远赶不上组件渲染的速度，不过在 created 中监听也是没任何问题的。相关代码如下：

```js
// form-item.vue，部分代码省略
export default {
  methods: {
    setRules () {
      this.$on('on-form-blur', this.onFieldBlur);
      this.$on('on-form-change', this.onFieldChange);
    },
  },
  mounted () {
    if (this.prop) {
      this.dispatch('iForm', 'on-form-item-add', this);
      this.setRules();
    }
  }
}
```

通过调用 `setRules` 方法，监听表单组件的两个事件，并绑定了句柄函数 `onFieldBlur` 和 `onFieldChange`，分别对应 blur 和 change 两种事件类型。当 onFieldBlur 或 onFieldChange 函数触发时，就意味着 FormItem 要对**当前的数据**进行一次校验。当前的数据，指的就是通过表单域 Form 中定义的 props：model，结合当前 FormItem 定义的 `props：prop` 来确定的数据，可以回顾上文写过的用例。

因为 FormItem 中只定义了数据源的某个 key 名称（即属性 prop），要拿到 Form 中 model 里的数据，需要用到第 3 节的通信方法 provide / inject。所以在 Form 中，把整个实例（this）向下提供，并在 FormItem 中注入：

```js
// form.vue，部分代码省略
export default {
  provide() {
    return {
      form : this
    };
  }
}
```

```js
// form-item.vue，部分代码省略
export default {
  inject: ['form']
}
```

准备好这些，接着就是最核心的校验功能了。blur 和 change 事件都会触发校验，它们调用同一个方法，只是参数不同。相关代码如下：

```js
// form-item.vue，部分代码省略
import AsyncValidator from 'async-validator';

export default {
  inject: ['form'],
  props: {
    prop: {
      type: String
    },
  },
  data () {
    return {
      validateState: '',  // 校验状态
      validateMessage: '',  // 校验不通过时的提示信息
    }
  },
  computed: {
    // 从 Form 的 model 中动态得到当前表单组件的数据
    fieldValue () {
      return this.form.model[this.prop];
    }
  },
  methods: {
    // 从 Form 的 rules 属性中，获取当前 FormItem 的校验规则
    getRules () {
      let formRules = this.form.rules;

      formRules = formRules ? formRules[this.prop] : [];

      return [].concat(formRules || []);
    },
    // 只支持 blur 和 change，所以过滤出符合要求的 rule 规则
    getFilteredRule (trigger) {
      const rules = this.getRules();
      return rules.filter(rule => !rule.trigger || rule.trigger.indexOf(trigger) !== -1);
    },
    /**
     * 校验数据
     * @param trigger 校验类型
     * @param callback 回调函数
     */
    validate(trigger, callback = function () {}) {
      let rules = this.getFilteredRule(trigger);

      if (!rules || rules.length === 0) {
        return true;
      }

      // 设置状态为校验中
      this.validateState = 'validating';

      // 以下为 async-validator 库的调用方法
      let descriptor = {};
      descriptor[this.prop] = rules;

      const validator = new AsyncValidator(descriptor);
      let model = {};

      model[this.prop] = this.fieldValue;

      validator.validate(model, { firstFields: true }, errors => {
        this.validateState = !errors ? 'success' : 'error';
        this.validateMessage = errors ? errors[0].message : '';

        callback(this.validateMessage);
      });
    },
    onFieldBlur() {
      this.validate('blur');
    },
    onFieldChange() {
      this.validate('change');
    }
  }
}
```

在 FormItem 的 `validate()` 方法中，最终做了两件事：

1. 设置了当前的校验状态 `validateState` 和校验不通过提示信息 `validateMessage`（通过值为空）；
2. 将 validateMessage 通过回调 callback 传递给调用者，这里的调用者是 onFieldBlur 和 onFieldChange，它们只传入了第一个参数 `trigger`，callback 并未传入，因此也不会触发回调，而这个回调主要是给 Form 用的，因为 Form 中可以通过提交按钮一次性校验所有的 FormItem（后文会介绍）这里只是表单组件触发事件时，对当前 FormItem 做校验。

除了校验，还可以对当前数据进行重置。重置是指将表单组件的数据还原到最初绑定的值，而不是清空，因此需要预先缓存一份初始值。同时我们将校验信息也显示在模板中，并加一些样式。相关代码如下：

```html
<!-- form-item.vue，部分代码省略 -->
<template>
  <div>
    <label v-if="label" :class="{ 'i-form-item-label-required': isRequired }">{{ label }}</label>
    <div>
      <slot></slot>
      <div v-if="validateState === 'error'" class="i-form-item-message">{{ validateMessage }}</div>
    </div>
  </div>
</template>
<script>
  export default {
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: {
        type: String
      },
    },
    data () {
      return {
        isRequired: false,  // 是否为必填
        validateState: '',  // 校验状态
        validateMessage: '',  // 校验不通过时的提示信息
      }
    },
    mounted () {
      // 如果没有传入 prop，则无需校验，也就无需缓存
      if (this.prop) {
        this.dispatch('iForm', 'on-form-item-add', this);

        // 设置初始值，以便在重置时恢复默认值
        this.initialValue = this.fieldValue;

        this.setRules();
      }
    },
    methods: {
      setRules () {
        let rules = this.getRules();
        if (rules.length) {
          rules.every((rule) => {
            // 如果当前校验规则中有必填项，则标记出来
            this.isRequired = rule.required;
          });
        }

        this.$on('on-form-blur', this.onFieldBlur);
        this.$on('on-form-change', this.onFieldChange);
      },
      // 从 Form 的 rules 属性中，获取当前 FormItem 的校验规则
      getRules () {
        let formRules = this.form.rules;

        formRules = formRules ? formRules[this.prop] : [];

        return [].concat(formRules || []);
      },
      // 重置数据
      resetField () {
        this.validateState = '';
        this.validateMessage = '';

        this.form.model[this.prop] = this.initialValue;
      },
    }
  }
</script>
<style>
  .i-form-item-label-required:before {
    content: '*';
    color: red;
  }
  .i-form-item-message {
    color: red;
  }
</style>
```

至此，FormItem 代码已经完成，不过它只具有单独校验的功能，也就是说，只能对自己的一个表单组件验证，不能对一个表单域里的所有组件一次性全部校验。而实现全部校验和全部重置的功能，要在 Form 中完成。

上文已经介绍到，在 `Form` 组件中，预先缓存了全部的 FormItem 实例，自然也能在 Form 中调用它们。通过点击提交按钮全部校验，或点击重置按钮全部重置数据，只需要在 Form 中，逐一调用缓存的 FormItem 实例中的 `validate` 或 `resetField` 方法。相关代码如下：

```js
// form.vue，部分代码省略
export default {
  data () {
    return {
      fields: []
    };
  },
  methods: {
    // 公开方法：全部重置数据
    resetFields() {
      this.fields.forEach(field => {
        field.resetField();
      });
    },
    // 公开方法：全部校验数据，支持 Promise
    validate(callback) {
      return new Promise(resolve => {
        let valid = true;
        let count = 0;
        this.fields.forEach(field => {
          field.validate('', errors => {
            if (errors) {
              valid = false;
            }
            if (++count === this.fields.length) {
              // 全部完成
              resolve(valid);
              if (typeof callback === 'function') {
                callback(valid);
              }
            }
          });
        });
      });
    }
  },
}
```

虽然说 Vue.js 的 API 只来自 prop、event、slot 这三个部分，但一些场景下，需要通过 `ref` 来访问这个组件，调用它的一些内置方法，比如上面的 `validate` 和 `resetFields` 方法，就需要使用者来主动调用。

resetFields 很简单，就是通过循环逐一调用 FormItem 的 resetField 方法来重置数据。validate 稍显复杂，它支持两种使用方法，一种是普通的回调，比如：

```html
<template>
  <div>
    <i-form ref="form"></i-form>
    <button @click="handleSubmit">提交</button>
  </div>
</template>
<script>
  export default {
    methods: {
      handleSubmit () {
        this.$refs.form.validate((valid) => {
          if (valid) {
            window.alert('提交成功');
          } else {
            window.alert('表单校验失败');
          }
        })
      }
    }
  }
</script>
```

同时也支持 Promise，例如：

```js
handleSubmit () {
  const validate = this.$refs.form.validate();
  
  validate.then((valid) => {
    if (valid) {
      window.alert('提交成功');
    } else {
      window.alert('表单校验失败');
    }
  })
}
```

在 Form 组件定义的 Promise 中，只调用了 `resolve(valid)`，没有调用 `reject()`，因此不能直接使用 `.catch()` ，不过聪明的你稍作修改，肯定能够支持到！

完整的用例如下：

```html
<template>
  <div>
    <h3>具有数据校验功能的表单组件——Form</h3>
    <i-form ref="form" :model="formValidate" :rules="ruleValidate">
      <i-form-item label="用户名" prop="name">
        <i-input v-model="formValidate.name"></i-input>
      </i-form-item>
      <i-form-item label="邮箱" prop="mail">
        <i-input v-model="formValidate.mail"></i-input>
      </i-form-item>
    </i-form>
    <button @click="handleSubmit">提交</button>
    <button @click="handleReset">重置</button>
  </div>
</template>
<script>
  import iForm from '../components/form/form.vue';
  import iFormItem from '../components/form/form-item.vue';
  import iInput from '../components/input/input.vue';

  export default {
    components: { iForm, iFormItem, iInput },
    data () {
      return {
        formValidate: {
          name: '',
          mail: ''
        },
        ruleValidate: {
          name: [
            { required: true, message: '用户名不能为空', trigger: 'blur' }
          ],
          mail: [
            { required: true, message: '邮箱不能为空', trigger: 'blur' },
            { type: 'email', message: '邮箱格式不正确', trigger: 'blur' }
          ],
        }
      }
    },
    methods: {
      handleSubmit () {
        this.$refs.form.validate((valid) => {
          if (valid) {
            window.alert('提交成功');
          } else {
            window.alert('表单校验失败');
          }
        })
      },
      handleReset () {
        this.$refs.form.resetFields();
      }
    }
  }
</script>
```

运行效果：


![](https://user-gold-cdn.xitu.io/2018/10/30/166c3b8a77e382ec?w=1417&h=550&f=png&s=60805)

完整的示例源码可通过 GitHub 查看：

[https://github.com/icarusion/vue-component-book](https://github.com/icarusion/vue-component-book)

> 项目基于 Vue CLI 3 构建，下载安装依赖后，通过 npm run serve 可访问。

## 结语

组件最终的效果看起来有点 “low”，但它实现的功能却不简单。通过这个实战，你或许已经感受到本小册一开始说的，组件写到最后，都是在拼 JavaScript 功底。的确，Vue.js 组件为我们提供了一种新的代码组织形式，但归根到底，是离不开 JS 的。

这个实战，你应该对独立组件间的通信用法有进一步的认知了吧，不过，这还不是组件通信的终极方案，下一节，我们就来看看适用于任何场景的组件通信方案。

注：本节部分代码参考 [iView](https://github.com/iview/iview/tree/2.0/src/components/form)。

## 扩展阅读

- [一份超级详细的Vue-cli3.0使用教程](https://juejin.im/post/5bdec6e8e51d4505327a8952)

# 5 组件的通信 3：找到任意组件实例——findComponents 系列方法
# 6 实战 2：组合多选框组件——CheckboxGroup & Checkbox
# 7 Vue 的构造器——extend 与手动挂载——$mount
# 8 实战 3：动态渲染 .vue 文件的组件—— Display
# 9 实战 4：全局提示组件——$Alert
# 10 更灵活的组件：Render 函数与 Functional Render
# 11 实战 5：可用 Render 自定义列的表格组件——Table
# 12 实战 6：可用 slot-scope 自定义列的表格组件——Table
# 13 递归组件与动态组件
# 14 实战 7：树形控件——Tree
# 15 拓展：Vue.js 容易忽略的 API 详解
# 16 拓展：Vue.js 面试、常见问题答疑
# 17 拓展：如何做好一个开源项目（上篇）
# 18 拓展：如何做好一个开源项目（下篇）
# 19 写在最后