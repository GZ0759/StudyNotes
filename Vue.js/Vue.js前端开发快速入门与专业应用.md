> Vue.js前端开发快速入门与专业应用
> 2017年2月第1版

# 第一章 Vue.js简介

## 1.1 VUe.js是什么

Vue.js 被定义成一个用来开发 Web 界面的前端库，是个非常轻量级的工具。Vue.js 本身具有响应式编程和组件化的特点。

所谓响应式编程 , 即为保持状态和视图的同步，这个在大多数前端 MV*（MVC/MVVM/MVW）框架，不管是早期的 backbone.js 还是现在 AngularJS 都对这一特性进行了实现（也称之为数据绑定），但这几者的实现方式和使用方式都不相同。相比而言， Vue.js 使用起来更为简单，也无需引入太多的新概念，声明实例 new Vue({ data : data }) 后自然对 data 里面的数据进行了视图上的绑定。修改 data 的数据，视图中对应数据也会随之更改。

Vue.js 的组件化理念和 ReactJS 异曲同工——“一切都是组件”，可以将任意封装好的代码注册成标签。

## 1.2 为什么要用Vue.js

相比较 Angularjs 和 ReactJS，Vue.js 一直以轻量级，易上手被称道。MVVM 的开发模式也使前端从原先的 DOM 操作中解放出来，我们不再需要在维护视图和数据的统一上花大量
的时间，只需要关注于 data 的变化，代码变得更加容易维护。

作为新兴的前端框架，Vue.js 也抛弃了对 IE8 的支持，在移动端支持到 Android 4.2+ 和 iOS 7+。

理想状态下，我们能直接在前后端分离的新项目中使用 Vue.js 最合适。这能最大程度上发挥 Vue.js 的优势和特性，熟悉后能极大的提升我们的开发效率以及代码的复用率。尤其是移动浏览器上，Vue.js 压缩后只有 18KB，而且没有其他的依赖

## 1.3 Vue.js的Hello world

首先，引入 Vue.js 的方式有很多，你可以采用直接使用 CDN。Vue.js 有两个比较显著的特性。第一个特性是数据绑定，第二个特性是组件化，简单来说我们可以自己定义 HTML 标签，并在模板中使用它。

# 第二章 基础特性

## 2.1 实例及选项

Vue.js 的使用都是通过构造函数 Vue({option}) 创建一个 Vue 的实例。一个 Vue 实例相当于一个 MVVM 模式中的 ViewModel。在实例化的时候，我们可以传入一个选项对象，包含数据、模板、挂载元素、方法、生命周期钩子等选项。

```JavaScript
var vm = new Vue({})
```

选项中主要影响模板或 DOM 的选项有 el 和 template，属性 replace 和 template 需要一起使用。

el ：类型为字符串， DOM 元素或函数。其作用是为实例提供挂载元素。一般来说我们会使用 css 选择符，或者原生的 DOM 元素。例如 el:'#app'。在初始项中指定了 el，实例将立即进入编译过程。

template ：类型为字符串。默认会将 template 值替换挂载元素（即 el 值对应的元素），并合并挂载元素和模板根节点的属性（如果属性具有唯一性，类似 id，则以模板根节点为准）如果 replace 为 false，模板 template 的值将插入挂载元素内。通过 template 插入模板的时候，挂载元素的内容都将被互联，除非使用 slot 进行分发。

在使用 template 时，我们往往不会把所有的 HTML 字符串直接写在 js 里面，这样影响可读性而且也不利于维护。所以经常用 '#tpl' 的方式赋值，并且在 body 内容添加 `<scrip id="tpl" type="x-template">` 为标签包含的 HTML 内容，这样就能将 HTML 从 js 中分离开来，示例
如下

```JavaScript
<div id="app">
  <p>123</p>
</div>
<script id="tpl" type="x-template">
  <div class='tpl'>
    <p>This is a tpl from script tag</p>
  </div>
</script>
<script type="text/javascript">
  var vm = new Vue({
    el : '#app',
    template : '#tpl'
  });
</script>
```

Vue.js 2.0 中废除了 replace 这个参数，并且强制要求每一个 Vue.js 实例需要有一个根元素。

Vue.js 实例中可以通过 data 属性定义数据，这些数据可以在实例对应的模板中进行绑定并使用。需要注意的是，如果传入 data 的是一个对象， Vue 实例会代理起 data 对象里的所有属性，而不会对传入的对象进行深拷贝。另外，我们也可以引用 Vue 实例 vm 中的 $data 来获取声明的数据，

```JavaScript
var data = { a: 1 }
var vm = new Vue({
  data: data
})
vm.$data === data // -> true
vm.a === data.a // -> true
// 设置属性也会影响到原始数据
vm.a = 2
data.a // -> 2
// 反之亦然
data.a = 3
vm.a // -> 3
```

需要注意的是，只有初始化时传入的对象才是响应式的，即在声明完实例后，再加上一句 vm.$data.b = '2'，并在模板中使用 {{b}}，这时是不会输出字符串 '2' 的。如果需要在实例化之后加入响应式变量，需要调用实例方法 $set。不过 Vue.js 并不推荐这么做，这样会抛出一个异常。所以，我们应尽量在初始化的时候，把所有的变量都设定好，如果没有值，也可以用undefined 或 null 占位。

另外，组件类型的实例可以通过 props 获取数据，同 data 一样，也需要在初始化时预设好。

也可以在上述组件类型实例中同时使用 data，但有两个地方需要注意：第一，data 的值必须是一个函数，并且返回值是原始对象。如果传给组件的 data 是一个原始对象的话，则在建立多个组件实例时它们就会共用这个 data 对象，修改其中一个组件实例的数据就会影响到其他组件实例的数据。第二，data 中的属性和 props 中的不能重名。这两者均会抛出异常。

可以通过选项属性 methods 对象来定义方法，并且使用 v-on 指令来监听 DOM 事件。

另外， Vue.js 实例也支持自定义事件，可以在初始化时传入 events 对象，通过实例的$emit 方法进行触发。这套通信机制常用在组件间相互通信的情况中，例如子组件冒泡触发父组件事件方法，或者父组件广播某个事件，子组件对其进行监听等。而 Vue.js 2.0 中废弃了 events 选项属性，不再支持事件广播这类特性，推荐直接使用Vue 实例的全局方法 $on()/$emit()，或者使用插件 Vuex 来处理。

```JavaScript
var vm = new Vue({
  el : '#app',
  data : data,
  events : {
    'event.alert' : function() {
    alert('this is event alert :' + this.a);
    }
  }
});
vm.$emit('event.alert');
```

Vue.js 实例在创建时有一系列的初始化步骤，例如建立数据观察，编译模板，创建数据绑定等。在此过程中，我们可以通过一些定义好的生命周期钩子函数来运行业务逻辑。

通过写一个简单的 demo 来更清楚地了解内部的运行机制.

```JavaScript
var vm = new Vue({
  el : '#app',
  init: function() {
    console.log('init');
  },
  created: function() {
    console.log('created');
  },
  beforeCompile: function() {
    console.log('beforeCompile');
  },
  compiled: function() {
    console.log('compiled');
  },
  attached: function() {
    console.log('attached');
  },
  dettached: function() {
    console.log('dettached');
  },
  beforeDestroy: function() {
    console.log('beforeDestroy');
  },
  destroyed: function() {
    console.log('destroyed');
  },
  ready: function() {
    console.log('ready');
  // 组件完成后调用 $destory() 函数，进行销毁
  this.$destroy();
  }
});
```

## 2.2 数据绑定

Vue.js 的核心是一个响应式的数据绑定系统，建立绑定后， DOM 将和数据保持同步，这样就无需手动维护 DOM，使代码能够更加简洁易懂、提升效率。

- 文本插值。数据绑定最基础的形式就是文本插值，使用的是双大括号标签 {{}}，为“Mustache” 语
法。模板语法同时也支持单次插值，即首次赋值后再更改 vm 实例属性值不会引起 DOM 变化。Vue.js 2.0 去除了 {{*}} 这种写法，采用 v-once 代替这种单词插值。

- HTML属性。Mustache 标签也同样适用于 HTML 属性中，但是Vue.js 2.0 中废弃了这种写法，用 v-bind 指令代替。

- 绑定表达式。放在 Mustache 标签内的文本内容称为绑定表达式。除了直接输出属性值之外，一段绑定表达式可以由一个简单的 JavaScript 表达式和可选的一个或多个过滤器构成。每个绑定中只能包含单个表达式，并不支持 JavaScript 语句，否则 Vue.js 就会抛出warning 异常。并且绑定表达式里不支持正则表达式，如果需要进行复杂的转换，可以使用过滤器或者计算属性来进行处理。

```JavaScript
{{ var a = 1 }} // 无效
{{ if (ok) { return name } }} // 无效，但可以写成 ok ? name : '' 或者 ok && name 这
样的写法
```

- 过滤器。Vue.js 允许在表达式后添加可选的过滤器，以管道符“|” 指示。同时也允许多个过滤器链式使用，也允许传入多个参数。需要注意的是， Vue.js 2.0 中已经去除了内置的过滤器。

- 指令。指令通常会直接书写在模板的 HTML 元素中，而为了有别于普通的属性， Vue.js 指令是带有前缀的 v- 的属性。可以理解为当表达式的值发生改变时，会有些特殊行为作用到绑定的 DOM 上。

简单介绍指令绑定数据和事件的语法。

参数

```JavaScript
<img v-bind:src="avatar" />
```
指令 v-bind 可以在后面带一个参数，用冒号（:）隔开， src 即为参数。此时 img 标签
中的 src 会与 vm 实例中的 avatar 绑定，等同于 :
```JavaScript
<img src="{{avatar}}" />
```

修饰符

修饰符（Modifiers）是以半角句号 . 开始的特殊后缀，用于表示指令应该以特殊方式绑定。
```JavaScript
<button v-on:click.stop=""doClick></button>
```
v-on 的作用是在对应的 DOM 元素上绑定事件监听器， doClick 为函数名，而 stop 即为
修饰符，作用是停止冒泡，相当于调用了 e. stopPropagation()。

计算属性。在项目开发中，展示的数据往往需要经过一些处理。除了在模板中绑定表达式或者利用过滤器外， Vue.js 还提供了计算属性这种方法，避免在模板中加入过重的业务逻辑，保证模板的结构清晰和可维护性。

```JavaScript
var vm = new Vue({
  el : '#app,
  data: {
    firstName : 'Gavin'，
    lastName: 'CLY'
  }
  computed : {
    fullName : function() {
    // this 指向 vm 实例
    return this.firstName + ' ' + this.lastName
    }
  }
});
<p>{{ firstName }}</p> // Gavin
<p>{{ lastName }}</p> // CLY
<p>{{ fullName }}</p> // Gavin CLY
```

如果说上面那个例子并没有体现出来计算属性的优势的话，那计算属性的 Setter 方法，则在更新属性时给我们带来了便利。

```JavaScript
var vm = new Vue({
  el : '#el',
  data: {
    //  vm.cents 设置为后端所存的数据
    cents : 100，
  }
  computed : {
    // 计算属性 price 为前端展示和更新的数据
    price : {
      set : function(newValue) {
        this.cents = newValue * 100;
      },
      get : function() {
       return (this.cents / 100).toFixed(2);
      }
    }
  }
});
```

表单控件。Vue.js 中提供 v-model 的指令对表单元素进行双向数据绑定，在修改表单元素值的
同时，实例 vm 中对应的属性值也同时更新，反之亦然。Vue.js 为表单控件提供了一些参数，方便处理某些常规操作。

- lazy。默认情况下， v-model 在 input 事件中同步输入框值与数据，加 lazy 属性后从会改到在
change 事件中同步。

- number。会自动将用户输入转为 Number 类型，如果原值转换结果为 NaN 则返回原值。

- debounce。设置最小延时，单位为 ms，即为单位时间内仅执行一次数据更新。该参数往往应用在高耗操作上，例如在更新时发出 ajax 请求返回提示信息。

不过 Vue.js 2.0 中取消了 lazy 和 number 作为参数，用修饰符（modifier）来代替。新增了 trim 修饰符，去掉输入值首尾空格。去除了 debounce 这个参数，原因是无法监测到输入新数据，但尚未同步到 vm 实例属性时这个状态。

Class与Style绑定。在开发过程中，经常会遇到动态添加类名或直接修改内联样式。class 和 style 都是 DOM 元素的 attribute ，可以直接使用 v-bind 对这两个属性进行数据绑定。例如 `<p v-bind:style='style'><p>`，然后通过修改 vm.style 的值对元素样式进行修改。但这样未免过于繁琐而且容易出错，所以 Vue.js 为这两个属性单独做了增强处理，表达式的结果类型除了字符串之外，还可以是对象和数组。

Class绑定。绑定的数据可以是对象和数组，具体的语法如下：
- 对象语法： v-bind:class 接受参数是一个对象，而且可以与普通的 class 属性共存。
- 数组语法： v-bind:class 也接受数组作为参数。也可以使用三元表达式切换数组中的 class 。

内联样式绑定。style 属性绑定的数据即为内联样式，同样具有对象和数组两种形式。

- 对象语法。直接绑定符合样式格式的对象。除了直接绑定对象外，也可以绑定单个属性或直接使用字符串。
- 数组语法：v-bind:style 允许将多个样式对象绑定到统一元素上。

自动添加前缀。在使用 transform 这类属性时，v-bind:style 会根据需要自动添加厂商前缀。 :style 在运行时进行前缀探测，如果浏览器版本本身就支持不加前缀的 css 属性，那就不会添加。

## 2.3 模板渲染

## 2.4 事件绑定与监听

第三章 指令
3.1 内置指令
3.2 自定义指令基础
3.3 指令的高级选项
3.4 指令在Vue.js2.0中的变化

第四章 过滤器
4.1 过滤器注册
4.2 双向过滤器
4.3 动态参数
4.4 过滤器在Vue.js2.0中的变化

第五章 过渡
5.1 CSS过渡
5.2 JavaScript过渡
5.3 过渡系统在Vue.js2.0中的变化

第六章 组件
6.1 组件注册
6.2 组件选项
6.3 组件间通信
6.4 内容分发
6.5 动态组件
6.6 Vue.js2.0中的变化

第七章 Vue.js常用插件
7.1 Vue-router
7.2 Vue-resource
7.3 Vue-devtools

第八章 Vue.js工程实例
8.1 准备工作
8.2 目录结构
8.3 前端开发
8.4 后端联调
8.5 部署上线

第九章 状态管理：Vuex
9.1 概述
9.2 简单实例
9.3 严格模式
9.4 中间件
9.5 表单处理
9.6 目录结构
9.7 实例
9.8 Vue.js2.0的变化

第十章 跨平台开发：Weex

第十一章 Vue.js2.0新特性

