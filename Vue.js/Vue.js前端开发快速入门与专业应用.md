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

当获取到后端数据后，我们会把它按照一定的规则加载到写好的模板中，输出成在浏览器中显示的 HTML，这个过程就称之为渲染。而 Vue.js 是在前端（即浏览器内）进行的模板渲染。

早期的 Web 项目一般是在服务器端进行渲染，服务器进程从数据库获取数据后，利用后端模板引擎，甚至于直接在 HTML 模板中嵌入后端语言（例如 JSP），将数据加载进来生成HTML，然后通过网络传输到用户的浏览器中，然后被浏览器解析成可见的页面。而前端渲染则是在浏览器里利用 JS 把数据和 HTML 模板进行组合。两种方式各有自己的优缺点，需要更具自己的业务场景来选择技术方案。

前端渲染的优点在于：
- 业务分离，后端只需要提供数据接口，前端在开发时也不需要部署对应的后端环境，通过一些代理服务器工具就能远程获取后端数据进行开发，能够提升开发效率。
- 计算量转移，原本需要后端渲染的任务转移给了前端，减轻了服务器的压力。

而后端渲染的优点在于：
- 对搜索引擎友好。
- 首页加载时间短，后端渲染加载完成后就直接显示 HTML，但前端渲染在加载完成后还需要有段 js 渲染的时间。

Vue.js 2.0 开始支持服务端渲染，从而让开发者在使用上有了更多的选择。

条件渲染。v-if 和 v-else 的作用是根据数据值来判断是否输出该 DOM 元素，以及包含的子元素。需要注意的是， v-else 必须紧跟 v-if，不然该指令不起作用。

除了 v-if， v-show 也是可以根据条件展示元素的一种指令。与 v-if 不同的是， v-show 元素的使用会渲染并保持在 DOM 中。 v-show 只是切换元素的 css 属性 display。v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗，我们需要根据实际的使用场景来选择合适的指令。

v-for 指令主要用于列表渲染，将根据接收到数组重复渲染 v-for 绑定到的 DOM 元素及内部的子元素，并且可以通过设置别名的方式，获取数组内数据渲染到节点中。

需要注意的是 Vue.js 对 data 中数组的原生方法进行了封装，所以在改变数组时能触发视图更新，但以下两种情况是无法触发视图更新的：
- 通过索引直接修改数组元素， 例如 `vm.items[0] = { title : 'title-changed'}`;
- 无法直接修改“修改数组”的长度， 例如： `vm.items.length = 0`

对于第一种情况， Vue.js 提供了 $set 方法，在修改数据的同时进行视图更新，可以写成：
`vm.items.$set(0, { title : 'title-changed'}` 或者 `vm.$set('items[0]', { title : 'titlealso-changed '})`， 这两种方式皆可以达到效果。

在列表渲染的时候，有个性能方面的小技巧，如果数组中有唯一标识 id。通过 trace-by 给数组设定唯一标识，Vue.js 在渲染过程中会尽量复用原有对象的作用域及 DOM 元素。

## 2.4 事件绑定与监听

当模板渲染完成之后，就可以进行事件的绑定与监听了。Vue.js 提供了 v-on 指令用来监听 DOM 事件，通常在模板内直接使用，而不像传统方式在 js 中获取 DOM 元素，然后绑定事件。

方法及内联语句处理器。通过 v-on 可以绑定实例属性 methods 中的方法作为事件的处理器，v-on: 后参数接受所有的原生事件名称。Vue.js 也提供了 v-on 的缩写形式"@"。除了直接绑定 methods 函数外，v-on 也支持内联 JavaScript 语句，但仅限一个语句。在直接绑定函数和内联语句时，都有可能需要获取原生 DOM 事件对象，一下两种方式都可以获取。

```JavaScript
<button v-on:click="showEvent">Event</button>
<button v-on:click="showEvent($event)">showEvent</button>
<button v-on:click="showEvent()">showEvent</button> // 这样写获取不到 event
var vm = new Vue({
  el : '#app',
  methods : {
    showEvent : function(event) {
     console.log(event);
    }
  }
});
```

修饰符。Vue.js 为指令 v-on 提供了多个修饰符，方便处理一些 DOM 事件的细节，并且修饰符可以串联使用。主要的修饰符如下。

- .stop: 等同于调用 event. stopPropagation()。
- .prevent: 等同于调用 event.preventDefault()。
- .capture: 使用 capture 模式添加事件监听器。
- .self: 只当事件是从监听元素本身触发时才触发回调。

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

除了事件修饰符之外，v-on 还提供了按键修饰符，方便我们监听键盘事件中的按键。Vue.js 给一些常用的按键名提供了别称，这样就省去了一些记 keyCode 的事件。全部按键别名为： enter、 tab、 delete、 esc、 space、 up、 down、 left、 right。Vue.js 也允许我们自己定义按键别名。Vue.js 2.0 中可以直接在 Vue.config.keyCodes 里添加自定义按键别名，无需修改 v-on 指令。

```JavaScript
// 可以使用 `v-on:keyup.f1`
Vue.config.keyCodes.f1 = 112
```

与传统事件绑定的区别。Vue.js 事件处理方法和表达式都严格绑定在当前视图的 ViewModel 上，所以并不会维护困难。这么写的好处在于，无需手动管理事件，ViewModel 被校会时所有事件处理器都会自动被删除；方便解耦。在处理 ul、li 这种列表时，往往会把 li 事件代理到 ul 上，而 Vue.js 这类的框架由于不需要手动添加事件，往往会把事件绑定在 li 上，虽然多耗了些性能。但在实际运用中并没有什么特别的性能瓶颈影响，而且也省去代理中处理 e.target 的步骤，让事件和 DOM 元素关系更紧密、简单。

## 2.5 Vue.extend()

组件化开发也是 Vue.js 中非常重要的一个特性，可以将一个页面看成一个大的根组件，里面包含的元素就是不同的子组件，子组件也可以在不同的根组件中被调用。那么，如何可被重复使用的子组件呢？Vue.js 提供了 Vue。extend(options) 方法，创建基础 Vue 构造器的“子类”，参数 options 对象和直接声明 Vue 实例参数对象基本一致，使用方法如下。

```JavaScript
var Child = Vue.extend({
  template : '#child',
  // 不同的是， el 和 data 选项需要通过函数返回值赋值，避免多个组件实例共用一个数据
  data : function() {
    return {
    ….
    }
  }
  ….
})
Vue.component('child', Child) // 全局注册子组件
<child></child> // 子组件在其他组件内的调用方式
```

# 第三章 指令

指令是 Vue.js 中一个重要的特性，主要提供了一种机制将数据的变化映射为 DOM 行为。当数据变化时，指令会依据设定好的操作对 DOM 进行修改，这样就可以只关注数据的变化，而不用去管理 DOM 的变化和状态，使得逻辑更加清晰，可维护性更好。

## 3.1 内置指令

v-bind 主要用于动态绑定 DOM 元素属性，即元素属性实际的值是由 vm 实例中的 data 属性提供的。v-bind 也可以简写为“:”。v-bind 还拥有三种修饰符，分别为 .sync、 .once、 .camel，作用分别如下。

- .sync ：用于组件 props 属性，进行双向绑定，即父组件绑定传递给子组件的值，无论在哪个组件中对其进行了修改，其他组件中的这个值也会随之更新。
- .once ：同 .synce 一样，用于组件 props 属性，但进行的是单次绑定。和双向绑定正好相反，单次绑定是将绑定数据传递给子组件后，子组件单独维护这份数据，和父组件的数据再无关系，父组件的数据发生变化也不会影响子组件中的数据。
- .camel ：将绑定的特性名字转回驼峰命名。只能用于普通 HTML 属性的绑定，通常会用于svg 标签下的属性。

不过在 Vue.js 2.0 中，修饰符 .syce 和 .once 均被废弃，规定组件间仅能单向传递，如果子组件需要修改父组件，则必须使用事件机制来进行处理。

v-model指令主要用于 input、select、textarea 标签中，具有 lazy、number、debounce（2.0废除）、trim（2.0新增）这些修饰符。

v-if/v-else/v-show 这三个指令主要用于根据条件展示对应的模板内容。v-if 和 v-show 的主要区别在于，v-if 在条件为false 的情况下并不进行模板的搬移，而 v-show 则会在模板编译好之后将元素隐藏掉。v-if 的切换消耗要比 v-show 高，但初始条件为 false 的情况下，v-if 的初始渲染要稍快。

v-for 也是用于模板渲染的指令，v-for 指令在 Vue.js 2.0 中做了些细微的调整。大致包含一下几个方面。

- 参数顺序变化。当包含参数 index 或 key 时，对象参数修改为 (item, index) 或 (value, key)，这样与 JS Array 对象的新方法 forEach 和 map，以及一些对象迭代器（例如lodash）的参数能保持一致。
- 属性 track-by 被 v-bind: key 代替。
- v-for="n in 10" 中的 n 由原来的 0 ～ 9 迭代变成 1 ～ 10 迭代。

在 Vue.js 2.0 中，在组件上使用 v-on 指令只监听自定义事件，即使用 $emit 触发的
事件；如果要监听原生事件，需要使用修饰符 .native，例如 `<my-component v-on:click.native="onClick"></my-component>`

v-text，参数类型为 String，作用是更新元素的 textContent。 {{}} 文本插值本身也会被编译成 textNode 的一个 v-text 指令。而与直接使用 {{}} 不同的是， v-text 需要绑定在某个元素上，能避免未编译前的闪现问题。

如果直接使用 `<span>{{msg}}</span>`，在生命周期 beforeCompile 期间，此刻 msg 数据尚未编译至 {{msg}} 中，用户能看到一瞬间的 {{msg}}，然后闪现为 There is a message，而用 v-text 的话则不会有这个问题。

v-HTML, 参数类型为 String， 作用为更新元素的 innerHTML，接受的字符串不会进行编译等操作，按普通 HTML 处理。同 v-text 类似， {{{}}} 插值也会编译为节点的 v-HTML 指令， v-HTML 也需要绑定在某个元素上且能避免编译前闪现问题。

v-el 指令为 DOM 元素注册了一个索引，使得可以直接访问 DOM 元素。语法上说，可以通过所属实例的 $els 属性调用。或者在 vm 内部通过 this 进行调用。另外，由于 HTML 不区分大小写，在 v-el 中如果使用了驼峰命名方式，系统会自动转成小写。但可以使用“-”来连接期望的大写字符。

v-ref 指令与 v-el 类似，只不过 v-ref 作用于子组件上，实例可以通过 $refs 访问子组件。命名方式也类似，想使用驼峰式命名的话用“-” 来做连接。

```JavaScript
<message v-ref:title content="title"></message>
<message v-ref:sub-title content="subTitle"></message>

var Message = Vue.extend({
  props : ['content'],
  template : '<h1>{{content}}</h1>'
});
Vue.component('message', Message);
```

最终将 vm.$refs.title 和 vm.$refs.subTitle 用 console.log 的方式打印到控制台中，结果为输出了两个子组件的实例。从理论上来说，我们可以通过父组件对子组件进行任意的操作，但实际上尽量还是会采用props 数据绑定，用组件间通信的方式去进行逻辑上的交互，尽量让组件只操作自己内部的数据和状态，如果组件间有通信，也通过调用组件暴露出来的接口进行通信，而不是直接跨组件修改数据。

v-pre 指令相对简单，就是跳过编译这个元素和子元素，显示原始的 {{}}Mustache 标
签，用来减少编译时间。

```html
<span v-pre>{{ this will not be compiled }}</span>
```

v-cloak 指令相当于在元素上添加了一个 `[v-cloak]` 的属性，直到关联的实例结束编译。官方推荐可以和 css 规则 `[v-cloak]{ display :none }` 一起使用，可以隐藏未编译的 Mustache 标签直到实例准备完毕。

v-once 指令是 Vue.js 2.0 中新增的内置指令，用于标明元素或组件只渲染一次，即使随后发生绑定数据的变化或更新，该元素或组件及包含的子元素都不会再次被编译和渲染。这样就相当于我们明确标注了这些元素不需要被更新，所以 v-once 的作用是最大程度地提升了更新行为中页面的性能，可以略过一些明确不需要变化的步骤。

## 3.2 自定义指令基础

除了内置指令外，Vue.js 也提供了方法可以注册自定义指令，以便封装对 DOM 元素的处理方式，提高代码复用率。

指令的注册。通过`Vue.directive(id, definition)`方法注册一个全局自定义指令，接收参数 id 和定义对象。id 是指令的唯一标识，定义对象则是指令的相关属性及钩子函数。`Vue.directive(‘global-directive’, definition); `全局注册指令，也可以通过组建的 directive 选项注册一个局部的自定义指令。

```JavaScript
var comp = Vue.extend({
directives : {
  'localDirective' : {} // 可以采用驼峰式命名
}
});
```

指令的定义对象。在注册指令的同时，可以传入 definition 对象，对指令赋予一些特殊的功能。这个定义对象主要包含三个钩子函数，bind、update 和 unbind。
- bind: 只被调用一次，在指令第一次绑定到元素上时调用。
- update: 指令在 bind 之后以初始值在参数进行第一次调用，之后每次当绑定值发生变化时调用，update 接收到的参数为 newValue 和 oldValue。
- unbind: 指令从元素上解绑时调用，只调用一次。

```JavaScript
<div v-if="isExist" v-my-directive="param"></div>
Vue.directive('my-directive', {
  bind : function() {
   console.log('bind', arguments);
  },
  update : function(newValue, oldValue) {
    console.log('update', newValue, oldValue)
  },
  unbind : function() {
    console.log('unbind', arguments);
  }
})
var vm = new Vue({
  el : '#app',
  data : {
    param : 'first',
    isExist : true
  }
});
```

另外，如果我们只需要使用 update 函数时，可以直接传入一个函数代替定义对象。

```JavaScript
Vue.directive('my-directive', function(value) {
// 该函数即为 update 函数
});
```

上述例子中，可以使用 my-directive 指令绑定的值是 data 中的 param 属性。也可以直接绑定字符串常量，或使用字面修饰符，但这样的话需要注意 update 方法将只调用一次，因为普通字符串不能响应数据变化。除了字符串外，指令也能接受对象字面量或任意合法的 JavaScript 表达式。

指令实例属性。除了了解指令的生命周期外，还需要知道指令中能调用的相关属性，一边对相关 DOM 进行操作。在指令的钩子函数内，可以通过 this 来调用指令实例。

- el ：指令绑定的元素。
- vm ：该指令的上下文 ViewModel，可以为 new Vue() 的实例，也可以为组件实例。
- expression ：指令的表达式，不包括参数和过滤器。
- arg ：指令的参数。
- name ：指令的名字，不包括 v- 前缀。
- modifiers ：一个对象，包含指令的修饰符。
- descriptor ：一个对象，包含指令的解析结果。

```html
<div v-my-msg:console.log="content"></div>
```

```JavaScript
Vue.directive('my-msg', {
  bind : function() {
    console.log('~~~~~~~~~~~bind~~~~~~~~~~~~~');
    console.log('el', this.el);
    console.log('name', this.name);
    console.log('vm', this.vm);
    console.log('expression', this.expression);
    console.log('arg', this.arg);
    console.log('modifiers', this.modifiers);
    console.log('descriptor', this.descriptor);
  },
  update : function(newValue, oldValue) {
    var keys = Object.keys(this.modifiers);
    window[this.arg][keys[0]](newValue);
  },
  unbind : function() {
  }
});
var vm = new Vue({
  el : '#app',
  data : {
    content : 'there is the content'
  }
});
```

## 3.3 指令的高级选项
## 3.4 指令在Vue.js2.0中的变化

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

