> Vue.js 组件精讲  
> Aresn iView 的作者 《Vue.js实战》的作者  

# 1 开篇：Vue.js 的精髓——组件

## 组件的分类

一般来说，Vue.js 组件主要分成三类：

1. 由 `vue-router` 产生的每个页面，它本质上也是一个组件（.vue），主要承载当前页面的 HTML 结构，会包含数据获取、数据整理、数据可视化等常规业务。整个文件相对较大，但一般不会有 `props` 选项和 `自定义事件`，因为它作为路由的渲染，不会被复用，因此也不会对外提供接口。

2. 不包含业务，独立、具体功能的基础组件，比如日期选择器、模态框等。这类组件作为项目的基础控件，会被大量使用，因此组件的 API 进行过高强度的抽象，可以通过不同配置实现不同的功能。比如笔者开源的 iView，就是包含了 50 多个这样基础组件的 UI 组件库。

3. 业务组件。它不像第二类独立组件只包含某个功能，而是在业务中被多个页面复用的，它与独立组件的区别是，业务组件只在当前项目中会用到，不具有通用性，而且会包含一些业务，比如数据请求；而独立组件不含业务，在任何项目中都可以使用，功能单一，比如一个具有数据校验功能的输入框。

## 小册的内容

因为本小册是围绕 Vue.js 组件展开的，所以第二节会讲解 Vue.js 组件的三个 API：`prop`、`event`、`slot`。

- 3 - 7 小节会介绍组件间通信的一些方法和黑科技，一部分是 Vue.js 内置的，一部分是自行实现的，在实际开发中，会非常实用。例如具有数据校验功能的表单组件（Form）和组合多选框组件（CheckboxGroup & Checkbox）。

- 8 - 10 小节介绍 Vue 的构造器 extend 和手动挂载组件 $mount 的用法及案例。Vue.js 除了我们正常 `new Vue()` 外，还可以手动挂载的，例如动态渲染 .vue 文件的组件（Display）和全局通知组件（$Alert）。

- 11 - 12 小节介绍 Render 函数与 Functional Render，并完成一个能够渲染自定义列的 Table 组件。Render 函数也是 Vue.js 组件重要的一部分，只不过在大多数业务中不常使用。本小节会介绍它的使用场景。

- 13 小节介绍作用域 slot（slot-scope），并基于这种方法同样实现 Table 组件。slot 用的很多，但 slot-scope  在业务中并不常用，但在一些特定场景下，比如组件内部有循环体时，会非常实用。

- 14 - 15 小节介绍递归组件，并完成树形控件（Tree）。

- 16 - 19 小节是综合拓展，会着重讲解 Vue.js 容易忽略却很重要的 API，以及对 Vue.js 面试题的详细分析。除此之外，还会总结笔者在两年的 iView 开源经历中的经验，除了技术细节外，还包括开源项目的持续性发展、推广等。

# 2 基础：Vue.js 组件的三个 API：prop、event、slot

## 组件的构成

一个再复杂的组件，都是由三部分组成的：prop、event、slot，它们构成了 Vue.js 组件的 API。如果开发的是一个通用组件，那一定要事先设计好这三部分，因为组件一旦发布，后面再修改 API 就很困难了，使用者都是希望不断新增功能，修复 bug，而不是经常变更接口。

属性 prop 。`prop` 定义了这个组件有哪些可配置的属性，组件的核心功能也都是它来确定的。写通用组件时，props 最好用**对象**的写法，这样可以针对每个属性设置类型、默认值或自定义校验属性的值，这点在组件开发中很重要。

插槽 slot 。如果要给按钮组件 `<i-button>` 添加一些文字内容，就要用到组件的第二个 API：插槽 slot，它可以分发组件的内容。

自定义事件 event。现在我们给组件 `<i-button>` 加一个点击事件，目前有两种写法，先看自定义事件 event。通过 `$emit`，就可以触发自定义的事件 `on-click` ，在父级通过 `@on-click` 来监听。这里还有另一种方法，直接在父级声明，但为了区分原生事件和自定义事件，要用到事件修饰符 `.native`。

```html
<i-button @click.native="handleClick"></i-button>
```

## 组件的通信

一般来说，组件可以有以下几种关系：

A 和 B、B 和 C、B 和 D 都是父子关系，C 和 D 是兄弟关系，A 和 C 是隔代关系（可能隔多代）。组件间经常会通信，Vue.js 内置的通信手段一般有两种：

- `ref`：给元素或组件注册引用信息；
- `$parent` / `$children`：访问父 / 子实例。

这两种都是直接得到组件实例，使用后可以直接调用组件的方法或访问数据。

这两种方法的弊端是，无法在**跨级**或**兄弟**间通信。那这种情况下，就得配置额外的插件或工具了，比如 Vuex 和 Bus 的解决方案，本小册不再做它们的介绍，读者可以自行阅读相关内容。不过，它们都是依赖第三方插件的存在，这在开发独立组件时是不可取的，而在小册的后续章节，会陆续介绍一些黑科技，它们完全不依赖任何三方插件，就可以轻松得到任意的组件实例，或在任意组件间进行通信，且适用于任意场景。

# 3 组件的通信 1：provide / inject

## 什么是 provide / inject

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

值得注意的是，provide 和 inject 绑定并**不是可响应**的。然而，如果传入了一个可监听的对象，那么其对象的属性还是可响应的。

## 替代 Vuex

状态管理 Vuex 是一个专为 Vue.js 开发的**状态管理模式**，用于集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

使用 Vuex，最主要的目的是跨组件通信、全局数据维护、多人协同开发。需求比如有：用户的登录信息维护、通知信息维护等全局的状态和数据。

将 app.vue 理解为一个最外层的根组件，用来存储所有需要的全局数据和状态，甚至是计算属性（computed）、方法（methods）等。因为你的项目中所有的组件（包含路由），它的父组件（或根组件）都是 app.vue，所以我们**把整个 app.vue 实例通过 `provide` 对外提供**。

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

## 进阶技巧

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

## 独立组件中使用

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

# 4 组件的通信 2：派发与广播——自行实现 dispatch 和 broadcast 方法
# 5 实战 1：具有数据校验功能的表单组件——Form
# 6 组件的通信 3：找到任意组件实例——findComponents 系列方法
# 7 实战 2：组合多选框组件——CheckboxGroup & Checkbox
# 8 Vue 的构造器——extend 与手动挂载——$mount
# 9 实战 3：动态渲染 .vue 文件的组件—— Display
# 10 实战 4：全局提示组件——$Alert
# 11 更灵活的组件：Render 函数与 Functional Render
# 12 实战 5：可用 Render 自定义列的表格组件——Table
# 13 实战 6：可用 slot-scope 自定义列的表格组件——Table
# 14 递归组件与动态组件
# 15 实战 7：树形控件——Tree
# 16 拓展：Vue.js 容易忽略的 API 详解
# 17 拓展：Vue.js 面试、常见问题答疑
# 18 拓展：如何做好一个开源项目（上篇）
# 19 拓展：如何做好一个开源项目（下篇）
# 20 写在最后