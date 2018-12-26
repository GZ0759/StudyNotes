# 第一章 初识Vue.js

## 1.1 Vue.js是什么

Vue.js 的官方文档中是这样介绍它的。 简单小巧的核心，渐进式技术栈，足以应付任何规模的应用。 简单小巧是指 Vue.js 压缩后大小仅有17KB。所谓渐进式（Progressive），就是你可以一步一 步、有阶段性地来使用 Vue.js，不必一开始就使用所有的东西。

使用 Vue.js 可以让 Web 开发变得简单，同时也颠覆了传统前端开发模式。它提供了现代 Web 开发中常见的高级功能，比如 ：

- 解耦视图与数据
- 可复用的组件
- 前端路由
- 状态管理 
- 虚拟 DOM ( Virtual DOM) 

MVVM（Model-VIew-ViewModel）模式是由经典的软件架构 MVC 衍生来的 。当 View （视图层）变化时，会自动更新到 ViewModel （视图模型），反之亦然。 View 和 ViewModel 之间通过双向绑定（tdata-binding）建立联系。Vue.js 通过 MVVM 的模式拆分为视图与数据两部分，并将其分离。因此，你只需要关心你的数据即可， DOM 的事情 Vue 会帮你自动搞定。

## 1.2 如何使用Vue.js

Vue.js 是一个渐进式的 JavaScript 框架，根据项目需求，可以选择从不同的维度来使用它。如果只是简单开发， 可以直接通过 script 加载 CDN 文件。引入 Vue.js 框架后，在 body 底部使用 new Vue() 的方式创建一个实例，这就是 Vue.js 最基本的开发模式。

```html
`<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>`
```

# 第二章 数据绑定和第一个Vue应用

## 2.1 Vue实例与数据绑定

Vue.js 应用的创建很简单，通过构造函数 Vue 就可以创建一个 Vue 的根实例，并启动 Vue 应用。变量 app 就代表了这个 Vue 实例，基本上所以的代码都是一个对象，写入 Vue 实例的选项内。

```javascript
var app = new Vue({
  // 选项
})
```



Vue 实例对象的一个必不可少的选项就是 el ，用于指定一个页面中已存在的 DOM 元素来挂载 Vue 实例，它可以是 HTMLElement ，也可以是 CSS 选择器。挂载成功后，我们可以通过 app.$el 来访问该元素。Vue 提供了很多常见的实例属性和方法，都以`$`开头。

```javascript
// <div id='app'></div>
var app = new Vue({
    el:"#app" /* 或者是 document.getElementById('app') */
}）
```



通过 Vue 实例的 data 选项，可以声明应用内需要双向绑定的数据。建议所有会用到的数据都预先在 data 内声明，这样不至于将数据散落在业务逻辑中，难以维护。Vue 实例本身也代理了 data 对象里的所有属性。

```javascript
var data = { a: 1 }

// 直接创建一个实例
var vm = new Vue({
  data: data
})
vm.a // => 1
vm.$data === data // => true
```



每个 Vue 实例创建时，都会经历一系列的初始化过程，同时也会调用相应的生命周期钩子， 我们可以利用这些钩子，在合适的时机执行我们的业务逻辑。这些钩子与 el 和 data 类似，也是作为选项写入 Vue 实例内，并且钩子的 this 指向的是调用它的 Vue 实例。

```javascript
new Vue({
  el: '#app',
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  },
    mounted: function () {
    console.log(this.$el); // <div id="app"><div>    
  }
})
```



比较常用的生命周期钩子有，created（实例创建完成后调用）、mounted（el挂载到实例上后调用）、beforeDestroy（实例销毁之前调用）。这些钩子与 el 和 data 类似，也是作为选项写入 Vue 实例内，并且钩子的 this 指向的是调用它的 Vue 实例。

使用双大括号（Mustache语法）`"{{}}"`是最基本的文本插值方法，它会自动将我们双向绑定的数值实时显示出来，可以 v-text 代替。通过任何方法修改数据，大括号的内容都会被实时替换。

```html
<span v-text="msg"></span>
<!-- 和下面的一样 -->
<span>{{msg}}</span>
```



```html
<p>Using mustaches: {{ rawHtml }}</p>   
<!-- 显示 rawHtml 表示的内容，文本形式 -->

<p>Using v-html directive: <span v-html="rawHtml"></span></p>
<!-- 显示rawHtml 表示的内容，如是 html 则解析再显示 -->

<span v-pre>{{ this will not be compiled }}</span>
<!-- 跳过这个元素及子元素的编译过程。可用来显示原始 Mustache 标签 -->
```



在`{{}}`中，除了简单的绑定属性值外，还可以使用 JavaScript 表达式进行简单的运算 、三元运算等。Vue.js只支持单个表达式，不支持语句和流控制。另外在表达式中，不能使用用户自定义的全局变量，只能使用 Vue 白名单内的全局变量，例如 Math 和 Date。

Vue.js 支持在`{{}}`插值的尾部添加一个管道符 “ | ” 对数据进行过滤，经常用于格式化文本。过滤的规则是自定义的，通过给 Vue 实例添加选项 filters 来设置，过滤器可以串联，也可以接受参数。过滤器可以用在两个地方：双花括号插值和 v-bind 表达式。

```html
<!-- 在双花括号中 -->
{{ message | capitalize }}

<!-- 在 `v-bind` 中 -->
<div v-bind:id="rawId | formatId"></div>
```



## 2.2 指令与事件

指令是 Vue.js 模板中最常用的一项功能，它带有前缀 v-，指令的主要职责就是当起表达式的值改变时，相应地将某些行为应用到 DOM 上。

数据驱动 DOM 是Vue.js 的核心理念，所以不到万不得已时不要主动操作 DOM，只需要维护好数据，DOM 的事 Vue 会帮忙优雅处理。

Vue.js 内置了很多指令，帮助快速完成常见的 DOM 操作，比如循环渲染、显示与隐藏等，其中有两个比较重要的指令是 v-bind 和 v-on。

v-bind 的基本用途是动态更新HTML元素上的属性，比如 id、class 等。

v-on 指令用来绑定事件监听器。在普通元素上，v-on 可以监听原生的 DOM 事件，表达式可以是一个方法名，这些方法都写在 Vue 实例的 methods 属性内，并且是函数的形式，函数内的 this 指向的是当前 Vue 实例本身，因此可以直接使用 this.xxx 的形式来访问或修改数据。表达式除了方法名，也可以直接是一个内联语句。

## 2.3 语法糖

语法糖是指在不影响功能的情况下，添加某种方法实现同样的效果，从而方便程序开发。

Vue.js 的 v-bind 和 v-on 指令都提供了语法糖，也可以说是缩写，比如 v-bind 可以省略，直接写一个冒号”:”；v-on 可以直接用"@"来缩写。

# 第三章 计算属性

## 3.1 什么是计算属性

模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。

所有的计算属性都以函数的形式写在 Vue 实例内的 computed 选项内，最终返回计算后的结果。

## 3.2 计算属性用法

在一个计算属性里可以完成各种复杂的逻辑，包括运算、函数调用等，只要最终返回一个结果就可以。除了简单的用法，计算属性还可以依赖多个 Vue 实例的数据，只要其中任一数据变化，计算属性就会重新执行，视图也会更新。  

每一个计算属性都包含一个 getter 和一个 setter，默认只是利用了 getter 来读取。在需要时，也可以提供一个 setter 函数 ， 当手动修改计算属性的值就像修改一个普通数据那样时，就会触发 setter 函数，执行一些自定义的操作。

```javascript
computed: {
  fullName: {
    // getter
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
vm.fullName = 'John Doe'
```



计算属性除了简单的文本插值外，还经常用于动态地设置元素的样式名称 class 和内联样式 style 。当使用组件时，计算属性也经常用来动态传递 props 。

计算属性还有两个很实用的小技巧，一是计算属性可以依赖其他计算属性，二是计算属性不仅可以依赖当前Vue实例的数据，还可以依赖其它实例的数据。

## 3.3 计算属性缓存

调用 methods 里的方法也可以与计算属性起到同样的作用。

```html
<p>Reversed message: "{{ reversedMessage() }}"</p>
```



```javascript
// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```



计算属性是基于它的依赖缓存的。 一个计算属性所依赖的数据发生变化时，它才会重新取值，所以依赖数据只要不改变，计算属性也就不更新。但是 methods 则不同，只要重新渲染，它就会被调用，因此函数也会被执行 。

使用计算属性还是 methods 取决于你是否需要缓存，当遍历大数组和做大量计算时，应当使用计算属性，除非你不希望得到缓存。  

# 第四章 v-bind及class与style绑定

## 4.1 了解b-bind指令

v-bind 的的主要用法是动态更新 HTML 元素上的属性。

在数据绑定中，最常见的两个需求就是元素的样式名称 class 和内联样式 style 的动态绑定，它们也是 HTML 的属性，因此可以使用 v-bind 指令。我们只需要用 v-bind 计算出表达式最终的字符串就可以，不过有时候表达式的逻辑较复杂，使用字符串拼接方法较难阅读和维护，所以 Vue.js 增强了对 class 和 style 的绑定。

## 4.2 绑定class的几种方式

绑定 class 的几种方式，包括对象语法、数组语法和在组件上使用。

给 v-bind:class 设置一个对象，可以动态地切换 class。对象中也可以传入多个属性，来动态切换 class，表达式中项为真时对应的类名就会加载。另外，该设置能够与普通 class 共存。

当 :class 的表达式过长或逻辑复杂时，还可以绑定一个计算属性。

```html
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
```



当需要应用多个 class 时， 可以使用数组语法，给 :class 绑定一个数组，应用一个 class 列表。也可以使用三元表达式来根据条件切换 class。如果 class 有多个条件时，可以在数组语法中使用对象语法。

```html
<div v-bind:class="[activeClass, errorClass]"></div>
<!--  
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
} 
-->

<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>

```



如果直接在自定义组件上使用 class 或 :class，样式规则会直接应用到这个组件的根元素上。但只适合于自定义组件的最外层是一个根元素。当不满足这种条件或需要给具体的子元素设置类名时，应当使用组件的 props 来传递。

```html
<my-component class="baz boo"></my-component>
<!--  
渲染后的结果为
<p class="foo bar baz boo">Hi</p>  
-->
<script>
  Vue.component('my-component', {
    template: '<p class="foo bar">Hi</p>'
  })
</script>
```



## 4.3 绑定内联样式

绑定内联样式，使用v-bind:style可以给元素绑定内联样式，方法与:class类似，也有对象语法和数组语法，看起来很像直接在元素上写CSS。

CSS属性名称使用驼峰命名或短横分割命名。大多数情况下直接写一长串的样式不便于阅读和维护，一般以对象写在data或computed，也可以使用数组语法。大多数情况下 ， 直接写一长串的样式不便于阅读和维护，所以一般写在 data 或 computed 里。

```html
<div v-bind:style="styleObject"></div>

<script>
    var app = new Vue({
      el: '#app',
      data: {
        styleObject: {
          color: 'red',
          fontSize: '13px'
        }
      }
    })
</script>
```



另外，Vue.js会自动给特殊的CSS属性名称增加前缀，比如 transform。

# 第五章 内置指令

## 5.1 基本指令

v-cloak 不需要表达式，在 Vue 实例结束编译时从从绑定的HTML元素上移除，经常和 CSS 的 display:none 配合使用。在一般情况下，v-cloak 是一个解决初始化慢导致页面闪动的最佳实践。对于简单的项目很实用，但是在具有工程化的项目里，剩下的内容都是由路由去挂载不同组件完成的，所以不再需要 v-cloak。

```html
<div v-cloak>
  {{ message }}
</div>
```



```css
[v-cloak] {
  display: none;
}
```



v-once 也是一个不需要表达式的指令，作用是定义它的元素或组件只渲染一次，包括元素或组件的所有子节点。首次渲染后，不再随数据的变化重新渲染，将被视为静态内容。v-once 在业务中很少使用，只有需要进一步优化性能时才会用得上。

## 5.2 条件渲染指令

与 JavaScript 的条件语句 if、else、else if 类似，Vue.js 的条件指令可以根据表达式的值在 DOM 中渲染或销毁元素/组件。可以在 Vue.js 内置的`<template>`元素上使用条件指令，最终渲染的结果不会包含该元素。

Vue 在渲染元素时，出于效率考虑，会尽可能地复用已有的元素而非重新渲染。v-if、v-else-if、v-else 是条件渲染指令，利用 key 属性，可以决定是否要复用元素，key 的值必须是唯一的。

v-show 改变元素的 CSS 属性 display，当 v-show 表达式的值为 false 时，元素会隐藏，查看 DOM 结构会看到元素上加载了内联样式`display: none;`。但该指令不能在`<template>`上使用。

v-if 是真正的条件渲染，它会根据表达式适当地销毁或重建元素及绑定的事件或子组件，如果表达式的初始值为 false，则一开始元素/组件并不会渲染，只有当条件第一次变为真时才开始变异。而 v-show 只是简单的 CSS 属性切换，无论条件真与否，都会被编译。相比之下，v-if 更适合条件不经常改变的场景，因为它切换开销相对较大，而 v-show 适用于频繁切换条件。

## 5.3 列表渲染指令v-for

v-for 是列表渲染指令，可将一个数组遍历或枚举一个对象循环显示。也支持用 of 来代替 in 作为分隔符，前者是当前数组元素的别名，后者是数组。遍历数组时，v-for 的表达式支持一个可选参数作为当前项的索引。与 v-if 一样，v-for也可以用在内置标签`<template>`上，将多个元素进行渲染。

除了数组外，对象的属性也是可以遍历的。遍历对象属性时，有两个可选参数，分别是键名和索引。v-for 也可以迭代整数和字符串。

```html
<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>
```



数组更新，Vue 包含了一组观察数组变异的方法，使用它们改变数组也会触发视图更新，例如 push()、pop()、shift()、unshift()、splice()、sort()、reverse()。但非变异方法不会更新视图，例如 filter()、concat()、slice()，它们返回的是一个新数组，在使用这些非变异方法时，可以用新数组来替换原数组。Vue 在检测到数组变化时，并不是直接重新渲染整个列表，而是最大化地复用 DOM 元素，因此可以大胆地用新数组来替换旧数组，不用担心性能问题。

需要注意的是，通过索引直接设置项、修改数组长度，也是不会触发视图更新的。解决第一个问题的方法可以使用 Vue内置的 set 方法，如果是在 webpack 中使用组件化的方式，默认是没有导入 Vue 的，这是可以使用`$set`。另一种方法时直接使用 splice 来解决。

```javascript
var vm = new Vue({
  data: {
    items: ['a', 'b', 'c']
  }
})
vm.items[1] = 'x' // 不是响应性的
vm.items.length = 2 // 不是响应性的

// Vue.set
Vue.set(vm.items, indexOfItem, newValue)
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)
```



过滤与排序。当不想改变原数组，想通过一个数组的副本来做过滤或排序的显示时，可以使用计算属性来返回过滤或排序后的数组。

```html
<li v-for="n in evenNumbers">{{ n }}</li>
```



```javascript
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
computed: {
  evenNumbers: function () {
    return this.numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```



在计算属性不适用的情况下 (例如，在嵌套 v-for 循环中) 你可以使用一个 method 方法。

```html
<li v-for="n in even(numbers)">{{ n }}</li>
```



```javascript
data: {
  numbers: [ 1, 2, 3, 4, 5 ]
},
methods: {
  even: function (numbers) {
    return numbers.filter(function (number) {
      return number % 2 === 0
    })
  }
}
```



## 5.4 方法与事件

在事件绑定上，类似原生 JavaScript 的 onclick 等写法，也是在 HTML 上进行监听的。`@click`的表达式可以直接使用 JavaScript语句，也可以是一个在 Vue 实例中 methods 选项内的函数名。

`@click`调用的方法名后可以不跟括号"()"，如果该方法有参数，默认会将原生事件对象 event 传入。

这种在 HTML 元素上监听事件的设计看似将 DOM 与 JavaScript 紧耦合，违背分离的原理，实则刚好相反。因为通过 HTML 就可以知道调用的是哪个方法，将逻辑与 DOM 解耦，便于维护。最重要的是，当 ViewModel 销毁时，所有的事件处理器都会自动删除，无需自己清理。

Vue 提供了一个特殊变量`$event`，用于访问原生 DOM 事件。

事件可以用修饰符来实现特定功能，例如`event.preventDefault()`，可以用 Vue 事件的修饰符来实现。在绑定的事件后加小圆点“.”，再跟一个后缀来使用修饰符。

- `.stop` - 调用 `event.stopPropagation()`。
- `.prevent` - 调用 `event.preventDefault()`。
- `.capture` - 添加事件侦听器时使用 capture 模式。
- `.self` - 只当事件是从侦听器绑定的元素本身触发时才触发回调。
- `.{keyCode | keyAlias}` - 只当事件是从特定键触发时才触发回调。
- `.native` - 监听组件根元素的原生事件。
- `.once` - 只触发一次回调。
- `.left` - (2.2.0) 只当点击鼠标左键时触发。
- `.right` - (2.2.0) 只当点击鼠标右键时触发。
- `.middle` - (2.2.0) 只当点击鼠标中键时触发。
- `.passive` - (2.3.0) 以 `{ passive: true }` 模式添加侦听器

在表单元素上监听键盘事件时，还可以使用按键修饰符，比如按下具体某个键时才调用方法。也可以自己配置具体按键，全局定义后即可使用 keycode 和快键名称，甚至组合使用。除了具体的某个 keyCode 外，Vue 还提供了一些快捷名称。这些按键修饰符也可以组合使用，或和鼠标一起配合使用。

## 5.5 实战：利用计算属性、指令等知识开发购物车

购物侧需要展示一个已加入购物车的商品列表，包含商品名称、商品单价、购买数量和操作等信息，还需要实时显示购买的总价。其中购买数量可以增加或减少，每类购买数量还可以从购物车中移除。

注意，将 vue.min.js 和 index.js 文件写在`<body>`的最底部，如果写在`<head>`里，Vue 实例将无法创建，因为此时 DOM 还没有被解析完成，除非通过异步或在事件 DOMContentLoaded（IE是onreadystatechange）触发时再创建 vue 实例，这有点像 jQuery的`$(document).ready()`方法。

练习1：在当前示例基础上扩展商品列表，新增一项是否选中该商品的功能，总价变为只计算选中商品的总价，同时提供一个全选的按钮。

练习2：将商品列表 list 改为一个二维数组来实现商品的分类，比如可分为“电子产品”、“生活用品”和“果蔬”，同类商品聚合在一起。提示，你可能会用到两次 v-for。



# 第六章 表单与v-model

使用v-model后，表单控件显示的值只依赖所绑定的数据，不再关心初始化时的value属性。如果实时更新中文数据，可以用@input来替代v-model。v-model修饰符有lazy转变在change时间中同步数据、number将输入内容转换成Numbe类型、trim可以自动过滤输入的首尾空格

# 第七章 组件详解

## 7.1 组件与复用

Vue.js 的组件就是提高复用性，让代码可复用。那些没见过的自定义标签就是组件，每个标签代表一个组件，在任何使用 Vue 的地方都可以直接使用。

组件注册有全局注册和局部注册两种方式，注册的组件标签名称推荐使用小写加“-”分割的形式。组件中的选项data必须是函数，然后将数据 return 出去。

```javascript
`Vue.component('my-component-name', { /* ... */ })`
```



## 7.2 使用props传递数据

使用选项 props 来声明需要从父级接受的数据，props 的值有字符串数组类型和对象类型。由于HTML特性不区分大小写，当使用DOM模板时，驼峰命名的 prop 名称要转为短横分割命名。

父组件传递初值进来，子组件保存并进行修改渲染。第一种方法，在子组件的data内声明数据，并且引用父组件的 prop 。第二种方法是使用组件内的计算属性。

## 7.3 组件通信

子组件需要向父组件传递数据，则用到自定义事件。子组件用`$emit()`来触发事件，父组件用`$on()`来监听子组件的事件，父组件也可以直接在子组件的自定义标签上使用 v-on 来监听子组件触发的自定义事件。

一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件，但是像单选框、复选框等类型的输入控件可能会将 value 特性用于不同的目的。

在Vue.js 1.x中，除了`$emit()`方法外，还提供`$dispatch()`和`$broadcast()`这两个方法。前者用于向上级派发时间，后者是由上级向下级广播时间。

在Vue.js 2.x中，使用中央事件总线(bus)。首先创建名为bus的空Vue实例，在生命周期mounted钩子函数里监控来自bus事件的方法，在组件中通过bus把事件发送出去。

在子组件中，使用`this.$parent`可以直接访问该组件的父实例或组件，父组件也可以通过`this.$children`访问它所有的子组件。

Vue提供了子组件索引的方法，用特殊的属性ref来为子组件指定一个索引名称。在父组件模板中，子组件标签上使用ref指定一个名称，并在父组件内通过this.$refs来访问指定名称的子组件。

## 7.4 使用slot分发内容

子组件模板内定义`<slot>`元素，并且有`<p>`作为默认内容，如果父组件没有使用 slot 时，默认渲染这段默认内容，否则，父组件的内容进行分发，替换整个`<slot>`插槽。如果没有使用name特性，它将作为默认slot出现，父组件没有使用slot的元素与内容都将出现在这里。如果没有指定默认的匿名slot，父组件内多余的内容片段都将被抛弃，除非父组件的组件标签使用inline-template特性，将它们作为内联模板。

作用域插槽的使用场景就是父组件既可以复用子组件的slot，又可以使slot内容不一致。

`$slots`用来访问被插槽分发的内容。每个具名插槽有其相应的属性 (例如：slot="foo"中的内容将会在`vm.$slots.foo`中被找到)。default属性包括了所有没有被包含在具名插槽中的节点。

组件在它的模板内可以递归地调用自己，只要给组件设置name的选项就可以。

动态组件component是特殊的元素，使用:is特性可以用来动态的挂载不同的组件。

异步组件，将组件定义为一个工厂函数，动态地解析组件。Vue.js只在组件需要渲染时触发工厂函数，同时将结果缓存起来，用于后面的再次渲染。

`$nextTick`将回调延迟到下次DOM更新循环之后执行。在修改数据之后立即使用它，然后等待DOM更新。

除了内联模板，另一个定义模板的方式是在一个`<script>`元素中，并为其带上text/x-template的类型，然后通过一个id将模板引用过去。

手动挂载实例的方法，Vue.extend创建子类，参数是包含组件选项的对象，如果Vue实例在实例化时没有收到el选项，它就处于“未挂载”状态，没有关联的DOM元素，可以使用`$mount()`手动挂载一个未挂载的实例。

# 第八章 自定义指令

自定义指令的注册方式和组件很像，也分为全局注册和局部注册，一个指令定义对象可以提供如下几个钩子函数 (均为可选)：有blid、inserted、update、componentUpdated、unbind五种。其中钩子函数有四个参数，el、binding、vnode和oldVnode，binding是一个对象，包含的属性有name、value、oldValue、expression、arg、modifiers六个。

如果指令需要多个值，可以传入一个JavaScript对象字面量。记住，指令函数能够接受所有合法的 JavaScript 表达式

# 第九章 Render函数

Vue.js 2.x与Vue.js1.x最大的区别就在于前者使用了Virtual Dom（虚拟DOM）来更新节点，提升渲染性能。虚拟DOM并不是真正意义上的DOM，而是一个轻量级的JavaScript对象，在状态发生变化时，虚拟DOM会进行Diff运算，来更新只需要被替换的DOM，而不是全部重绘，与DOM操作相比，开销会小很多。
vNode对象通过一些特定的选项描述了真实的DOM结构，每个DOM元素或组件都对应一个VNode对象，VNode主要可以分为如下几类，TextVNode文本节点、ElementVnode普通元素节点、ComponentVnode组件节点、EmptyVNode没有内容的注释节点、CLoneVNode克隆节点，可以是以上任意类型的节点，唯一的区别在于isCloned属性为true

Render函数通过createElement参数来创建Virtual Dom，结构精简了很多。slot的使用场景也是在Render函数中的。createElement函数生成模板，它有3个参数。第一个参数是必选的，可以是一个HTML标签字符串，也可以是一个组件或函数；第二个是可选参数，包含模板相关属性的数据对象，在template中使用，第三个是子节点VNodes，由creatElement()构建而成，也是可选参数。

在以往的template里，我们都是在组件的标签上v-bind:class/v-on:click这样的指令，在Render函数都将其写在了数据对象里。

约束，组件树中的所有VNodes必须是唯一的。如果要重复很多次的元素/组件，可以使用工厂函数来实现。对于含有组件的slot，复用就要复杂一点，需要将slot的每个子节点都要克隆一份。

在Render函数中，不再需要Vue内置的指令，比如v-for、v-if，当然，也没有办法使用它们，无论要实现什么功能，都可以用原生JavaScript。解决办法，if、for用在父组件渲染中而不是模板界面，v-model的替代就是用prop：value和event：input组合使用的一个语法糖，也能在父组件渲染中实现逻辑功能。对于事件修饰符和按键修饰符，基本也需要自己实现，但事件修饰符.capture和.once，Vue提供了特殊的前缀，可以直接写在on的配置里。

函数化组件，Vue.js提供了一个functional的布尔值选项，设置为true可以使组件无状态和无实例，也就是data和this上下文，这样用Render函数返回虚拟节点可以更容易渲染，因为函数化组件是一个函数，渲染开销要小很多。使用函数化组件时，Render函数提供了第二个参数context来提供临时上下文，为了弥补缺少的实例。组件需要的东西都是通过这个上下文来传递的。在添加functional:true之后，锚点标题组件的render函数之间简单更新增加context参数，this.$slots.default更新为context.children，之后this.level更新为context.props.level

JSC是简化的模板，让Render函数更好地书写和阅读，Vue.js提供了插件babel-plugin-transform-vue-jsx来支持JSX语法，它看起来像HTML，但实际是JavaScript的语法扩展，用接近DOM结构的形式来描述一个组件的UI和状态信息。

# 第十章 使用webpack

webpack的主要使用场景是单页面富应用，将图片/CSS/字体打包成模块，从而处理模块间的依赖关系。export 和 import 是用来导出和导入模块的，一个模块就是一个 js 文件，拥有独立的作用域。导入的模块名称都是在 export 的文件中设置的，用户必须预先知道这个名称，如果想自定义名称，则使用 export default 来输出默认的模块。

webpack 配置中最重要也是必选的两项就是入口 Enrty 和出口 Output，入门的作用是告诉 webpack 从哪里开始寻找依赖，并且编译，出口则用来配置编译后的文件存储位置和文件名。entry 中的 js 文件就是我们配置的单入口，webpack 会从这个文件开始工作。output 中的 path 用来存放打包后文件的输出目录，是必填项，publicPath 指定资源文件引用的目录，flename 用于指定输出文件的名称。

对于不同的模块，需要用不同的加载器 Loaders 来处理，而加载器就是 webpack 的最重要的功能，通过安装不同的加载器可以对各种后缀名的文件进行处理，比如说要写 CSS 样式，就要用到 style-load 和 css-loader。在 module 对象的 rules 属性中可以指定一系列的 loads，其包含 test 和 use 两个选项，从而让 webpack 在编译过程中遇到 require () 和import 语句导入一个后缀名为 css 的文件时，先转换。use 选项的值可以是数字或字符串，如果是数字，编译顺序就是从后往前。CSS 是通过 JavaScript 动态创建 (style) 标签来写入的，意味着代码已经编译在了 mian.js 里。

webpack 最后一个重要的概念就是插件 Plugins。比如，通过很强大且可以定制的插件，可以把散落在各地的 css 或提取出来，并生成一个 main.css 文件。

.vue 单文件组件就是一个后缀名为 .vue 的文件，是一种新的构建模式，在 webpack 中使用 vue-loader 就可以对 .vue 格式的文件进行处理，该文件一般包含三个部分，即<template>、<script>、<style>。分别是 HTML/CSS/JS/ 模板，如果在 style 标签上使用 scoped 属性则代表只在这个组件有效。也可以使用 CSS 预编译。使用 .vue 文件需要先安装 vue-loader、vue-style-loader 等加载器并做配置，因为要使用 ES6 语法，还需要安装 babel 和 babel-loader 等加载器。在 demo 目录下有一个 .babelrc 的文件，是写入 babel 的配置，webpack 会依赖此配置文件来使用 babel 编译 ES6 代码。这样，每个 .vue 就代表一个组件，组件之间可以互相依赖。

ES6语法提示
data(){}等同于data:function(){}

.vue 的组件时没有名称的，在父组件使用时可以对它自定义，写好了就可以在入口 main.js 中使用它了。

ES6语法提示
=>是箭头函数，`render:h=>h(App)`等同于`render:function(h){return h(App)}`也等同于`render:h=>{return h(App)}`。但是，箭头函数里面的this指向与普通函数是不一样的，箭头函数体内的this对象就是定义时所在的对象，而不是使用时所在的对象。

ES6语法提示
`components:{vTitle,vButton}`等同于`component:{vTitle:vTitle,vButton:vButton}`。总结来说就是对象字面量缩写，当对象的 key 和 value 名称一致时，可以缩写成一个。

安装 url-loader 和 file-loader 来支持图片、字体等文件，其中“?limit=1024”是指如果这个文件小于 1kb，就以 base64 的形式加载，不会生出一个文件。

单页面富应用技术，意味着最终只有一个 html 文件，其余都是静态资源，实际部署到生产环境时，一般都会将 html 挂在后端程序下，由后端路由渲染这个页面，将所有静态资源单独部署到CDN，当然也可以和够短程序部署在一起，这样就实现了前后端完全分离。静态资源在大部分场景都有缓存。

# 第十一章 插件

注册插件需要一个公开的方法install，它的第一个参数是Vue构造器，第二个参数是一个可选的选项对象。然后通过Vue.use()来使用插件。

目前大多数的网站都是这种后端路由，也就是多页面的，这样可以让页面在服务器渲染好直接返回给浏览器，不用等待前端加载任何js和css就可以直接显示网页内容，再比如对SEO友好，缺点是后端必须维护和改写模板。

前后端分离的开发模式，后端只提供API返回数据，前端通过Ajax获取数据后，再用一定的方式渲染到页面里。缺点是首屏渲染需要时间来加载css和js。SPA就是在前后端分离的基础上，加一层前端路由。

前端路由，即由前端来维护一个路由规则，实现有两种，一是利用url的hash，就是常说的描点，java通过hashChange事件来监听url的改变。另一种就是HTML5的History模式，这种模式需要服务端支持。

vue-router路由不同的页面事实上就是动态加载不同的组件。每个页面对应一个组件，也就是对应一个.vue文件。在main.js里完成路由的剩下配置，创建一个数组来制定路由匹配列表，每个路由映射一个组件，component是映射的路由。

ES6语法提示
使用let和const命令来声明变量，代替了var。他们的作用域就是块。const声明后不能再修改，let则可以修改。

使用了异步路由后，编译出的每个页面的js都叫作块。，课通过设置里chunkFilename字段修改chunk命名。

vue-router有两种跳转页面的方法，第一种是使用内置的<router-link>组件，它会被渲染为一个<a>标签，to选项就是一个prop，指定需要跳转的路径，tag可以指定渲染成什么标签，使用replace不会留下History记录，active-class是跳转成功后给元素增加伪元素。

第二种跳转方法，通过JavaScript进行，使用router实例的方法。通过点击事件触发$router.push方法。$router还有replace和go等方法。

vue-router提供了导航钩子beforeEach和afterEach，它们会在路由即将改变前和改变后触发。导航钩子有三个参数，to表示进入的路由对象，from表示即将离开的路由对象，next表示调用该方法才能进入下一个钩子。

Vuex所解决的问题与bus类似，它作为Vue的一个插件来使用，可以更好地管理和维护整个项目的组件问题。使用Vuex会有一定的门槛和复杂度，它的主要使用场景是大型单页应用。它的用法与vue-router类似，在main.js里，通过Vue.use()使用Vuex。仓库store包含了应用的数据（状态）和操作过程，任何组件使用同一store的数据发生变化时，对应的组件也会立刻更新。可以通过$store.state.变量名进行读取。在组件内，来自store的数据只能读取，不能手动改变，改变store中数据的唯一途径就是显式地提交mutations。mutations是Vuex的第二个选项，用来直接修改state里的数据。在组件内，通过this.$store.commite方法来执行mutations。第二种方法是直接使用包含type属性的对象。mutation里尽量不要异步操作数据。

ES6语法提示
increment(state,n=1)等同于increment(state,n){n=n||1}

Vuex还有其他三个选项可以使用，getters、actions、modules。第一个就是用来依赖组件的计算属性；第二个是异步操作业务逻辑，在组件内通过$store.dispatch触发；最后一个可以将store分割到不同模块，每个module拥有自己的state、getters、mutations、actions，而且可以多层嵌套，在actions和getters中还可以接受一个参数rootState来访问根节点的状态。

ES6语法提示
Promise是一种异步方案，它有三种状态：Pending（进行中）、Resolve（已完成）、Rejected（已失败）

ES6语法提示
emit(event,...args)中的...args是函数参数的结构，使用它可以从当前参数（这里是第二个）到最后的参数都获取到。

# 第十二章 iView经典组件解剖

IView是一套基于Vue.js2的开源UI组件库，主要服务于PC界面的中后台产品，深度封装了40多个常用业务组件，比如Input、Checkbox、Select、Table；同时也是一整套的前端解决方案，包括设计规范、基础样式，支持服务端渲染（SSR），同时提供了可视化脚手架，方便快速构建项目工程。

级联选择组件Cascader。接受一个prop:data作为选择面板的数据源，使用v-model可以双向绑定当前选择的项。data中的label是面板显示的内容，value是它对应的值，children是它的子集，可递归。v-model绑定一个数组，每一项对应data里的value。Cascader的核心是用到了组件·递归，使用组件递归必不可少的两个条件是由name选项和在适当的时候结束递归。iView作为独立组件，无法使用bus和vuex，为了实现跨组件通信，iView摸你了Vue1的dispatch和boradcast方法。

折叠面板组件Collapse。组件分为两部分：collapse.vue和panel.vue，前者作为组件容器，接收一个整体的slot，而slot就是由后者组成，并且可以进行折叠面板的嵌套。collage支持v-model来双向绑定当前激活的面板，判断激活的依据是panel的prop：name。

iView内置工具函数。findComponentUpward方法以当前实例为参照点，向上寻找出指定name或几个name中的一个组件实例，找到后立即返回该实例。除了实用的工具函数外，iView内置的自定义指令、混合也可以直接使用。