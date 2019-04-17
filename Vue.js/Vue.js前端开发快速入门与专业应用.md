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
  bind: function() {
    console.log('~~~~~~~~~~~bind~~~~~~~~~~~~~');
    console.log('el', this.el); // el <div></div>
    console.log('name', this.name); // name my-msg
    console.log('vm', this.vm); // vm
    console.log('expression', this.expression); // expression content
    console.log('arg', this.arg); // arg console
    console.log('modifiers', this.modifiers); // modifiers Object {log: true}
    console.log('descriptor', this.descriptor); 
  },
  update: function(newValue, oldValue) {
    var keys = Object.keys(this.modifiers);
    window[this.arg][keys[0]](newValue);
  },
  unbind: function() {
  }
});
var vm = new Vue({
el: '#app',
data: {
  content: 'there is the content'
}
});
```

元素指令。元素指令是 Vue.js 的一种特殊指令，普通指令需要绑定在某个具体的 DOM 元素上，但元素指令可以单独存在，从使用方式上看更像是一个组件，但本身内部的实例属性和钩子函数是和指令一致的。Vue.js 2.0 中取消了这个特性，推荐使用组件来实现需要的业务。

```JavaScript
<div v-my-directive></div> // -> 普通指令使用方式
<my-directive></my-directive> // -> 元素指令使用方式
```

## 3.3 指令的高级选项

Vue.js 指令定义对象中除了钩子函数外，还有一些其他的选项。

params。定义对象中可以接受一个 params 数组，Vue.js 编译器将自动提取自定义指令绑定元素上的这些属性。除了直接传入数值外， params 支持绑定动态数据，并且可以设定一个 watcher 监听，当数据变化时，会调用这个回调函数。

```JavaScript
<div v-my-advance-directive a="paramA"></div>
Vue.directive('my-advance-directive', {
  params : ['a'],
  bind : function() {
   console.log('params', this.params);
  }
});
```

deep。当自定义指令作用域一个对象上时，可以使用 deep 选项来监听对象内部发生的变化。Vue.js 2.0 中废弃了该选项。 

twoWay。在自定义指令中，如果需要向 Vue 实例写回数据，就需要在定义对象中使用 `twoWay:true`，这样可以在指令中使用 this.set(value) 来写回数据。

acceptStatement。选项`acceptStatement: true`可以允许自定义指令接受内敛语句，同时 update 函数接收的值是一个函数，在调用该函数时，它将在所属实例作用域内运行。

terminal。选项 terminal 的作用是阻止 Vue.js 遍历这个元素及其内部元素，并由该指令本身去编译绑定元素及其内部元素，内置的指令 v-if 和 v-for 都是 terminal 指令。

priority。选项 priority 即为指定指令的优先级，普通指令默认是 1000，terminal 指令默认为 2000。同一元素上优先级高的指令会比其他指令处理得早一I些，相同优先级则按出现顺序依次处理。

## 3.4 指令在Vue.js2.0中的变化

在 Vue.js 2.0 中取消了指令实例这一概念，即在钩子函数中的 this 并不能指向指令的相关属性。指令的相关属性均通过参数的形式传递给钩子函数。

# 第四章 过滤器

Vue.js 允许在表达式后面添加可选的过滤器，以管道符表示。过滤器的本质是一个函数，接受管道符前面的值作为初始值，同时也能接受额外的参数，返回值为经过处理后的输出值。多个过滤器可以进行串联。

```JavaScript
{{ message | filterA 'arg1' 'arg2' }}
{{ message | filterA | filterB}}
```

## 4.1 过滤器注册

Vue.js 提供了全局方法 Vue.filter() 注册一个自定义过滤器，接受过滤器 ID 和过滤器函数两个参数。除了初始值之外，过滤器也能接受任意数量的参数。

```JavaScript
Vue.filter('date', function(value) {
  if(!value instanceof Date) return value;
  return value.toLocaleDateString();
})
```

## 4.2 双向过滤器

之前提及的过滤器都是在数据输出到视图之前，对数据进行转化显示，但不影响数据本身。Vue.js 也提供了在改变视图中数据的值，写回 data 绑定属性中的过滤器，称为双向过滤器。

```JavaScript
<input type="text" v-model="price | cents" >
Vue.filter('cents', {
  // 该过滤器的作用是处理价钱的转化，一般数据库中保存的单位都为分，避免浮点运算
  read : function(value) {
   return (value / 100).toFixed(2);
  },
  write : function(value) {
   return value * 100;
  }
  });
  var vm = new Vue({
  el : '#app',
  data: {
    price : 150
  }
});
```

从使用场景和功能来看，双向过滤器和第 2 章中提到的计算属性有点雷同。而 Vue.js 2.0 中也取消了过滤器对 v-model、 v-on 这些指令的支持，认为会导致更多复杂的情况，而且使用起来并不方便。所以 Vue.js 2.0 中只允许开发者在 {{}} 标签中使用过滤器，像上述对写操作有转化要求的数据，建议使用计算属性这一特性来实现。

## 4.3 动态参数

过滤器除了能接受单引号（""）括起来的参数外，也支持接受在 vm 实例中绑定的数据，称之为动态参数。使用区别就在于不需要用单引号将参数括起来。

```JavaScript
<input type="text" v-model="price" />
<span>{{ date | dynamic price }}</span>

Vue.filter('dynamic', function(date, price) {
  return date.toLocaleDateString() + ' : ' + price;
});
var vm = new Vue({
  el : '#app',
  data: {
    date : new Date(),
    price : 150
  }
});
```

## 4.4 过滤器在Vue.js2.0中的变化

过滤器在 Vue.js 2.0 中也发生了一些变化，大致说明如下：
- 取消了所有内置过滤器，即 capitalize, uppercase, json 等。作者建议尽量使用单独的插件来按需加入你所需要的过滤器。不过如果你觉得仍然想使用这些 Vue.js 1.0 中的内置过
滤器，也不是什么难办的事。 1.0 源码 filters/ 目录下的 index.js 和 array-filter.js 中就是所有内置过滤器的源码，你可以挑选你想用的手动加到 2.0 中。
- 取消了对 v-model 和 v-on 的支持，过滤器只能使用在 {{}} 标签中。
- 修改了过滤器参数的使用方式，采用函数的形式而不是空格来标记参数。例如： {{date | date('yyyy-MM-dd') }}。


# 第五章 过渡

过渡系统是 Vue.js 为 DOM 动画效果提供的一个特性，它能在元素从 DOM 中插入或移除时触发 CSS 过渡（transition）和动画（animation），也就是说在 DOM 元素发生变化时为其添加特定的 class 类名，从而产生过度效果。除了 CSS 过渡外， Vue.js 的过渡系统也支持 javascript 的过渡，通过暴露过渡系统的钩子函数。

## 5.1 CSS过渡

在模板中用 transition 绑定一个 DOM 元素，并且使用 v-if 指令使元素先处于未被编译状态。然后在控制台内手动调用 vm.show = true, 就可以看到在 DOM 元素完成编译后，过渡系统自动给元素添加了一个 my-startup-transition 的 class 类名。

```JavaScript
<div v-if="show" transition="my-startup"></div>
var vm = new Vue({
  el : '#app',
  data: {
   show : false
  }
});

<div class="my-startup-transition"></div>

```

Vue.js 的过渡系统给元素插入及移除时分别添加了 2 个类名： *-enter 和 *-leave， * 即为 transition 绑定的字符串.需要注意的是，这两个类名的优先级需要高于 `.my-startup-transition`，不然被 my-startup-transition 覆盖后就失效了。

```css
.my-startup-enter, .my-startup-leave{
  height: 0px;
  opacity: 0;
}
```

同样，我们也可以通过 CSS 的 animation 属性来实现过渡的效果。

CSS 过渡钩子函数。Vue.js 提供了在插入或 DOM 元素时类名变化的钩子函数，可以通过 Vue.transition('name', {})的方式来执行具体的函数操作。

```JavaScript
Vue.transition('my-startup', {
  beforeEnter: function (el) {
    console.log('beforeEnter', el.className);
  },
  enter: function (el) {
    console.log('enter', el.className);
  },
  afterEnter: function (el) {
    console.log('afterEnter', el.className);
  },
  enterCancelled: function (el) {
    console.log('enterCancelled', el.className);
  },
  beforeLeave: function (el) {
    console.log('beforeLeave', el.className);
  },
  leave: function (el) {
    console.log('leave', el.className);
  },
  afterLeave: function (el) {
    console.log('afterLeave', el.className);
  },
  leaveCancelled: function (el) {
    console.log('leaveCancelled', el.className);
  }
})
```

显示声明过渡类型。Vue.js 可以指定过渡元素监听的结束事件的类型。

```JavaScript
Vue.transition('done-type', {
  type: 'animation'
})
```

此时 Vue.js 就只监听元素的 animationend 事件，避免元素上还存在 transition 时导致的结束事件触发不一致。

自定义过渡类名。除了使用默认的类名`*-enter`、`*-leave`外，Vue.js 也允许我们自定义过渡类名。

```JavaScript
Vue.transition('my-startup', {
  enterClass: 'fadeIn',
  leaveClass: 'fadeOut'
})
```

Vue.js 官方推荐了一个 CSS 动画库， animate.css，配合自定义过渡类名使用，可以达
到非常不错的效果。只需要引入一个 CSS 文件， `http://cdn.bootcss.com/animate.css/3.5.2/animate.min.css`，就可以使用里面的预设动画。

## 5.2 JavaScript过渡

Vue.js 也可以和一些 JavaScript 动画库配合使用，这里只需要调用 JavaScript 钩子函数，而不需要定义 CSS 样式。 transition 接受选项 css:false，将直接跳过 CSS 检测，避免 CSS 规则干扰过渡，而且需要在 enter 和 leave 钩子函数中调用 done 函数，明确过渡结束时间。此处将引入 Velocity.js 来配合使用 JavaScript 过渡。

```JavaScript
<style>
.my-velocity-transition {
  position: absolute; top:0px;
  width: 100px; height: 100px;
  background: black;
}
</style>
<div v-if="velocity" transition="my-velocity"></div>
Vue.transition('my-velocity', {
  css : false,
  enter: function (el, done) {
    Velocity(el, { left : '100px' }, 500, 'swing', done);
  },
  enterCancelled: function (el) {
    Velocity(el, 'stop');
  },
  leave: function (el, done) {
    Velocity(el, { left : '0px' }, 500, 'swing', done);
  },
  leaveCancelled: function (el) {
    Velocity(el, 'stop');
  }
})
```

## 5.3 过渡系统在Vue.js2.0中的变化

- 用法变化。新的过渡系统中取消了 v-transition 这个指令，新增了名为 transition 的内置标签。transition 标签为一个抽象组件，并不会额外渲染一个 DOM 元素，仅仅是用于包裹过渡元素及触发过渡行为。 v-if、 v-show 等指令仍旧标记在内容元素上，并不会作用于transition 标签上。

- 钩子函数。enterClass, leaveClass, enterActiveClass, leaveActiveClass, appearClass,appearActiveClass，可以分别自定义各阶段的 class 类名。总得来说，在 Vue.js 2.0 中我们可以直接使用 transition 标签并设定其属性来定义一个过渡效果，而不需要像在 Vue.js 1.0 中通过 Vue.transition() 语句来定义。

-类名变化。Vue.js 2.0 中新增了两个类名 enter-active 和 leave-active，用于分离元素本身样式和过渡样式。我们可以把过渡样式放到 *-enter-active、 *-leave-active 中， *-enter， *-leave 中则定义元素过渡前的样式，而元素原本的样
式则由自己的类名去控制，不和过渡系统自动添加的类名样式混合起来。

- 钩子函数变化。Vue.js 2.0 中添加了三个新的钩子函数， before-appear, appear 和 after-appear。appear 主要是用于元素的首次渲染，如果同时声明了 enter 和 appear 的相关钩子函数，元素首次渲染的时候会使用 appear 系钩子函数，再次渲染的时候才使用 enter 系钩子函数。

- transition-group。除了内置的 transition 标签外， Vue.js 2.0 提供了 transition-group 标签，方便作用到多个 DOM 元素上。

```HTML
<div id="list-demo" class="demo">
  <button v-on:click="add">Add</button>
  <button v-on:click="remove">Remove</button>
  <transition-group name="list" tag="p">
    <span v-for="item in items" v-bind:key="item" class="list-item">
      {{ item }}
    </span>
  </transition-group>
</div>
```

```JavaScript
new Vue({
  el: '#list-demo',
  data: {
    items: [1,2,3,4,5,6,7,8,9],
    nextNum: 10
  },
  methods: {
    randomIndex: function () {
      return Math.floor(Math.random() * this.items.length)
    },
    add: function () {
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    remove: function () {
      this.items.splice(this.randomIndex(), 1)
    },
  }
})
```

```css
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to
/* .list-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
```

# 第六章 组件

代码复用一直是软件开发中长期存在的一个问题，每个开发者都想再次使用之前写好的代码，又担心引入这段代码后对现有的程序产生影响。从 jQuery 开始，就开始通过插件的形式复用代码，到 Requirejs 开始将 js 文件模块化，按需加载。这两种方式都提供了比较
方便的复用方式，但往往还需要自己手动加入所需的 CSS 文件和 HTML 模块。现在， Web Components 的出现提供了一种新的思路，可以自定义 tag 标签，并拥有自身的模板、样式和交互。 Angularjs 的指令， Reactjs 的组件化都在往这方面做尝试。同样， Vue.js 也提供了自己的组件系统，支持自定义 tag 和原生 HTML 元素的扩展。

## 6.1 组件注册

Vue.js 提供了两种注册方式，分别是全局注册和局部注册。

全局注册需要确保在根实例初始化之前注册，这样才能使组件在任意实例中被使用，注
册方式如下。这条语句需要写在 var vm = new Vue({…}) 之前，注册成功之后，就可以在模块中以自定义元素 `<my-component>` 的形式使用组件。

```JavaScript
<div id="app">
  <my-component></my-component>
</div>
var MyComponent = Vue.extend({
  template : '<p>This is a component</p>'
})
Vue.component('my-component', MyComponent)
var vm = new Vue({
  el : '#app'
});
```

局部注册则限定了组件只能在被注册的组件中使用，而无法在其他组件中使用，注册方式如下。

```JavaScript
var Child = Vue.extend({
  template : '<p>This is a child component</p>'
});
var Parent = Vue.extend({
  template: '<div> \
    <p>This is a parent component</p> \
    <my-child></my-child> \
    </div>',
  components: {
    'my-child': Child
  }
});
<div>
  <p>This is a parent component</p>
  <p>This is a child component</p>
</div>
```

注册语法糖。Vue.js 对于上述两种注册方式也提供了简化的方法，我们可以直接在注册的时候定义组件构造器选项。

```JavaScript
// 全局注册
Vue.component('my-component', {
  template : '<p>This is a component</p>'
})
// 局部注册
var Parent = Vue.extend({
  template: '<div> \
    <p>This is a parent component</p> \
    <my-child></my-child> \
    </div>',
  components: {
    'my-child': {
       template : '<p>This is a child component</p>'
  }
  }
});
```

## 6.2 组件选项

组件选项中与Vue选项的区别。组件选项中的 el 和 data 与 Vue 构造器选项中这两个属性的赋值会稍微有些不同。在 Vue 构造器中是直接赋值。而在组件中需要通过函数来返回一个新对象。

组件 Props。选项 props 是组件中非常重要的一个选项，起到了父子组件间桥梁的作用。

```JavaScript
Vue.component('my-child', {
  props : ['parent'],
  template: '<p>{{ parent }} is from parent'
})
<my-child parent="This data"></my-child> 
//-> <p>This data is from parent </p>
```

驼峰命名。同指令等情况相同，HTML 中的特性名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名)。

```JavaScript
Vue.component('blog-post', {
  // 在 JavaScript 中是 camelCase 的
  props: ['postTitle'],
  template: '<h3>{{ postTitle }}</h3>'
})
```

```html
<!-- 在 HTML 中是 kebab-case 的 -->
<blog-post post-title="hello!"></blog-post>
```

动态 Pros。可以通过 v-bind 的方式将父组件的 data 数据传递给子组件。需要注意的是，如果直接传递一个数值给子组件，就必须借助动态 Props。

```html
<!-- 即便 `42` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:likes="42"></blog-post>

<!-- 用一个变量进行动态赋值。-->
<blog-post v-bind:likes="post.likes"></blog-post>
```

绑定类型。在动态绑定中，v-bind 指令也提供了几种修饰符来进行不同方式的绑定。Props 绑定默认是单向绑定，即当父组件的数据发生变化时，子组件的数据随之变化，但在子组件中修改数据并不影响父组件。修饰符`.sync`和`.once`显示的声明绑定为双向绑定或单词绑定。

Props验证。组件可以指定 props 验证要求，这对开发第三方组件来说，可以让使用者更加准确地使用组件。使用验证的时候，props 接受的参数为 json 对象，而不是上述例子中的数组。

```JavaScript
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})

```

## 6.3 组件间通信

组件间通信是组件开发时非常重要的一环，既希望组件的独立性，数据能互不干涉，又不可避免组件间会有联系和交互。Vue.js 在组件间这一部分即提供了直接访问组件实例的方法，也提供了自定义事件机制，通过广播、派发、监听等形式进行跨组件的函数调用。

直接访问。在组件实例中，Vue.js 提供了以下三个属性对其父子组件及根实例进行直接访问。这三个属性都挂载在组件的 this 上，虽然 Vue.js 提供了直接访问这种方式，但并不提倡这么操作。这会导致父组件和子组件紧密耦合，且自身状态难以理解，锁机尽量使用 props 在组件间传递数据。

- $parent: 父组件实例。
- $children: 包含所有子组件实例。
- $root: 组件所在的根实例。

自定义事件监听。在 Vue 实例中，系统提供了一套自定义事件接口，用于组件间通信，方便修改组件状态。

可以在初始化实例或注册子组件的时候，直接传给选项 events 一个对象。也可以在某些特定情况或方法内采用 $on 方法来监听事件。

自定义事件触发机制。设置完成事件监听后，接下来是 Vue.js 的触发机制。

`$emit`。可以在实例本身触发事件。

```JavaScript
events : {
  'add' : function(msg) {
   this.todo.push(msg);
  }
}
methods: {
  onClick : function() {
    this.$emit('add', 'there is a message');// 即可触发 events 中的 add 函数
  }
}
```

`$dispatch`。派发事件，事件沿着父链冒泡，并在在第一次触发回调之后自动停止冒泡，除非触发函数明确返回 true ，才会继续向上冒泡。

```JavaScript
// 父组件：
events : {
'add' : function(msg) {
  this.todo.push(msg);
  // return true　明确返回 true 后，事件会继续向上冒泡
}
}

// 子组件：
methods: {
  toParent : function() {
  this.$dispatch('add', 'message from child');
  }
}
```

`$broadcast`。广播事件，事件会向下传递给所有的后代。

```JavaScript
methods: {
  toChild : function() {
    this.$dispatch('msg', 'message from parent');
  }
}
// 子组件：
events : {
  'msg' : function(msg) {
   alert(msg);
  }
}
```

子组件索引。虽然不建议组件直接访问各自的实例，但有时不可避免，Vue.js 也提供了直接访问子组件的方式。除了之前的 this.children 外，还可以给子组件绑定一个 v-ref 指令，指定一个索引 ID。这样就能在父组件中就可以通过 this.$refs 的方式获取子组件实例。另外，如果 v-ref 作用在 v-for 绑定的元素上，那么父组件获取的则为一个数组，包含相应的子组件实例。

## 6.4 内容分发

在实际的一些情况中，子组件往往并不知道需要展示的内容， 而知提供基础的交互功能，内容及事件由父组件来提供。对此 Vue.js 提供了一种混合父组件与子组件自己模板的方式，这种方式称之为内容分发。Vue.js 参照了当前 web component 规范草稿，使用 `<slot>` 元素为原始内容的插槽。

```JavaScript
<div id="app">
  // 使用包含 slot 标签属性的子组件
  <my-slot>
    // 属性 slot 值需要与子组件中 slot 的 name 值匹配
    <p slot="title">{{ title }}</p>
    <div slot="content">{{ content }}</div>
  </my-slot>
</div>
// 注册 my-slot 组件，包含 <slot> 标签，且设定唯一标识 name
Vue.component('my-slot', {
  template : '<div>\
  <div class="title"> \
  <slot name="title"></slot> \
  </div> \
  <div class="content"> \
  <slot name="content"></slot> \
  </div> \
  </div>',
});
var vm = new Vue({
  el : '#app',
  data : {
    title : 'This is a title',
    content : 'This is the content'
  }
});
// 最后输出结果
<div>
  <div class="title">
    <p slot="title">This is a title</p>
  </div>
  <div class="content">
    <div slot="content">This is the content</div>
  </div>
</div>
```

在模板下，`<slot>` 绑定的是父组件的数据。父组件模板的内容在父组件作用域内编译，子组件模板的内容在子组件作用域内编译。

`<slot>`标签允许有一个匿名 slot，不需要有 name 值，作为找不到匹配的内容片段的回退插槽，如果没有默认的 slot，这些找不到匹配的内容片段将被忽略。

在父组件中，可以定义多个相同的 slot 属性的 DOM 标签，这样会依次插入到对应的子组件的 slot 便签中，以兄弟节点的方式呈现。

## 6.5 动态组件

Vue.js 支持动态组件，即多个组件可以使用同一挂载点，根据条件来切换不同的组件。使用保留标签`<component>`，通过绑定到 is 属性的值来判断挂载哪个组件。这种场景往往运用在路由控制或者 tab 切换中。

```JavaScript
<div id="app">
  // 相当于一级导航栏，点击可切换页面
  <ul>
    <li @click="currentView = 'home'">Home</li>
    <li @click="currentView = 'list'">List</li>
    <li @click="currentView = 'detail'">Detail</li>
  </ul>
  <component :is="currentView"></component>
</div>

var vm = new Vue({
  el : '#app',
  data: {
   currentView: 'home'
  },
  components: {
    home: {
      template : '<div>Home</div>'
    },
    list: {
     template : '<div>List</div>'
    },
    detail: {
      template : '<div>Detail</div>'
    }
  }
});
```

component 标签接受 keep-alive 属性，可以将切换出去的组件保留在内存中，避免重新渲染。可以根据该特性适当地进行页面的性能优化，如果每个组件在激活时并不要求每次都实时请求数据，那使用 keep-alive 可以避免一些不必要的重复渲染，导致用户看到停留时间过长的空白页面。但如果每次激活组件都需要向后端请求数据的话，就不太适合使用 keepalive 属性了。Vue.js 2.0 中 keep-alive 属性被修改为标签。

activate 钩子函数。Vue.js 给组件提供了 activate 钩子函数，作用于动态组件切换或者静态组件初始化的过程中。active 接受了一个回调函数作为参数，使用函数后组件才进行之后的渲染过程。

```JavaScript
home: {
  template : '<div> \
  <p>Home</p> \
  <ul> \
  <li v-for="item in items">{{ item }}</li> \
  </ul> \
  </div>',
  data : function() {
    return {
     items : []
    }
  },
  activate : function(done) {
    var that = this;
    // 此处的 setTimeout 用于模拟正式业务中的 ajax 异步请求数据
    setTimeout(function() {
      that.items = [1, 2, 3, 4, 5];
      done();
    }, 1000);
  }
}
```

## 6.6 Vue.js2.0中的变化

Vue.js 2.0 中废弃了 event 选项，所有的自定义事件都需要通过`$emit`、`$on`、`$off`函数来进行触发、监听和取消监听。另外，废弃了`$dispatch`和`$broadcast`方法。官方认为这两种方法主要依赖于组件的属性结构，而当组件结构越来越复杂后，这种事件流的形式将难以被理解，而且也并不能解决兄弟组件之间的通信。所以官方推荐使用集中式的事件管理机制来处理组件间的通信，而不是依赖于组件本身的结构。

```JavaScript
// 官方建议可以直接使用一个空 Vue 实例来处理简单的事件触发机制：
var bus = new Vue();
bus.$emit('create', { title : 'name'});
bus.$on('create', function(data) {
// 进行对应的操作
})
```

```JavaScript
<div id="app">
  <comp-a></comp-a>
  <comp-b></comp-b>
</div>
var bus = new Vue();
var vm = new Vue({
el : '#app',
components : {
  compA : {
  template : '<div> \
    <input type="text" v-model="name" /> \
    <button @click="create"> 添加 </button> \
    </div>',
  data : function() {
    return {
      name : ''
    }
  },
  methods : {
    create : function() {
      bus.$emit('create', { name : this.name });
      this.name = '';
    }
  }
  },
  compB : {
    template : '<ul> \
      <li v-for="item in items">{{ item.name }} </li> \
      </ul>',
    data : function() {
      return {
      items : []
      }
    },
    // mounted 为 Vue.js 2.0 中新的生命周期函数
    mounted() {
      var that = this;
      bus.$on('create', function(data) {
        that.items.push(data);
      })
    }
  }
  }
});
```

keep-alive 不再是动态组件 component 标签中的属性，而成为了单独的标签。keep-alive 也可以不和 component 配合使用，单独包裹多个子组件，只需要确保所有子组件只激活唯一一个即可。

```JavaScript
<keep-alive>
  <comp-a v-if="active"></comp-a>
  <comp-b v-else></comp-b>
</keep-alive>
```

slot 不再支持多个相同 plot 属性的 DOM 插入到对应的 slot 标签中，一个 slot 只被使用一次。另外，slot 标签不再保存自身的属性及样式，均有父元素或被插入的元素提供样式和属性。

子组件索引 v-ref 的声明方式产生了变化，不再是一个指令了，而替换成一个子组件的一个特殊属性。调用方式没有发生变化，仍采用 `vm.$refs` 的方式直接访问子组件实例。

# 第七章 Vue.js常用插件

Vue.js 本身只提供了数据与视图绑定及组件化等功能，如果想要开发一个完整的 SPA 应用，还需要使用一些 Vue.js 插件。

## 7.1 Vue-router

Vue-router 是给 Vue.js 提供路由管理的插件，利用 hash 的变化控制动态组件的切换。

以往页面间跳转都由后端 MVC 中的 Controller 层控制，通过 `<a>` 标签的 href 或者直接修改 location.href，我们会向服务端发起一个请求，服务端响应后根据所接收到的信息去获取数据和指派对应的模板，渲染成 HTML 再返回给浏览器，解析成我们可见的页面。 Vue.js + Vue-router 的组合将这一套逻辑放在了前端去执行，切换到对应的组件后再向后端请求数据，填充进模板来，在浏览器端完成 HTML 的渲染。这样也有助于前后端分离，前端不用依赖于后端的逻辑，只需要后端提供数据接口即可。

vue-router 的基本作用就是将每个路径映射到对应的组件，并通过修改路由进行组件间的切换。常规路径规则为在当前 url 路径后面加上 #!/path， path 即为设定的前端路由路径。

一般应用中的路由方式不会那么简单，往往会出现二级导航这种情况。这时就需要使用嵌套路由这种写法。

```JavaScript
var Biz = Vue.extend({
  template : '<div> \
    <h1>This is the some business channel</h1> \
    <div class="container"> \
    <ul class="nav navbar-nav"> \
    <li> \
    <a v-link="{ path : \'/biz/list\'}">List</a> \
    </li> \
    <li> \
    <a v-link="{ path : \'/biz/detail\'}">Detail</a> \
    </li> \
    </ul> \
    </div> \
    <router-view></router-view> \
    </div>'
});

// 路由配置修改如下
router.map({
  '/home': {
    component: Home
  },
  '/biz': {
    component : Biz,
    subRoutes : {
      '/list' : {
        component : {
        template : '<h2>This is the business list page</h2>'
      }
      },
      '/detail' : {
        component : {
        template : '<h2>This is the business detail page</h2>'
      }
      }
    }
  }
})
```

路由匹配。vue-route 在设置路由规则的时候，支持以冒号开头的动态片段。

```JavaScript
router.map({
  '/list/:page': {
    component : {
      template: '<h1>This is the No.{{ $route.params.page }} page</h1>'
    }
  }
})
```

一条路有规则中支持包含多个动态片段。除了冒号: 开头的动态片段：page 外，Vue-router 还提供了以 * 号开头的全匹配片段。全匹配片段会包含所有符合的路径，而且不以“/”为间隔。

具名路由。在设置路由规则时，可以给路径名设置一个别名，方便进行路由跳转，而不需要去记住过长的全路径。

路由对象。在使用 Vue-router 启动应用时，每个匹配的自荐实例中都会被注入 router 的想，称之为路由对象。在组件内部可以通过 `this.$route` 的方式进行调用。
路由对象共包含了一下几个属性。
- $route.path
- $route.params
- $route.query
- $route.router
- $route.matched
- $route.name

v-link 是 vue-router 应用中用于路径间跳转的指令，其本质是调用路径实例 route 本身的 go 函数进行跳转。该指令接受一个 JavaScript 表达式，而且可以直接使用组件内绑定数据。

常见的使用方式包含以下两种：
- 直接使用字面路径
- 使用具名路径，并可以通过 params 或 query 设置路径中的动态片段或查询变量。

v-link包含其他参数选项。
- activeClass
- exact
- replace
- append

路径配置项。在创建路由器实例的时候，Vue-router 提供了以下参数供配置。
- hashbang
- history
- abstract
- root
- linkActiveClass
- saveScrollPosition
- transitionOnLoad
- suppressTransitionError

route钩子函数。在使用 Vue-router 的应用中，每个路由匹配到的组件中会多出一个 route 选项。在这个选项中可以使用路由切换的钩子函数来进行一定的业务逻辑操作。route 提供了 6 个钩子函数，分别如下。
- canActivate(): 在组件创建之前被调用，验证组件是否可被创建。
- activate(): 在组件创建且将要加载时被调用。
- data(): 在 activate 之后被调用，用于加载和设置当前组件的数据。
- canDeactivate(): 在组件被移出前被调用，验证是否可被移出。
- deactivate(): 在组件移出时调用。

路由实例属性及方法。在 Vue-router 启动的应用中，每个组件会被注入 router 实例，可以在组件内通过this.$router（或者使用路由对象 $route.router）进行访问。这个 router 实例主要包含了一些全局的钩子函数，以及配置路由规则，进行路由切换等 api。
- router.app
- router.mode
- router.start(App, el)
- router.stop()
- router.map()
- router.on()
- router.go(path)

vue-router 2.0 的变化。

使用方式。VueRouter 的初始化方式、路由规则配置和启动方式均发生了变化。嵌套路由的配置方法也发生了变化，改用 children 属性来进行标记，而且其中的 path 路径不需要以“/”开头，否则会认为从根路径开头。
```JavaScript
const router = new VueRouter({
  // 路由规则在实例化 VueRouter 的时候就直接传入，而不是调用 map 方法再进行传递
  routes : [
  { path : '/home', component: Home}
  ]
})
// 启动方法也发生了变化， router 实例直接传入 Vue.js 实例中，并调用 $mount 方法挂载到DOM 元素中
const app = new Vue({
  router : router
}).$mount('#app')
```

跳转方式。路由跳转的方式也发生了变化，首先是废弃了 v-link 指令，采用`<router-link>`标签来创建 a 标签来定义链接。其中的 to 属性和 v-link 所能接受的属性相同。其次是用 router 实例方法进行跳转的 api 也修改成了 push()，接受的选项参数基本没有变化。router.go() 方法不再表示跳转，而是接受一个整型参数，作用是在 history 记录中向前或者后退多少步，类似 window.history.go(n)。router 实例的 api 方法 push()、 replace()、 go() 主要是模拟 window.history 下的 pushState()、replaceState() 和 go() 的使用方法来实现的，并且确保 router 在不同模式下（ hash、 history）表现的一致性。

钩子函数。Vue-router 基本重新定义了自身的钩子函数。主要可分为三个方面。
- 全局钩子。在初始化 VueRouter 后直接使用 router 实例进行注册，包含 beforeEach和 afterEach 两个钩子，在每个路由切换前 / 后调用。
- 单个路由钩子。这个需要在路由配置的时候直接定义
- 组件内钩子。在组件内定义

获取数据。由于钩子函数的变化，在 Vue.js 2.0 中也就不存在使用 data 钩子来处理请求数据的逻辑了，可以通过监听动态路由的变化来获取数据。

```JavaScript
const List = {
  template: '...',
  watch: {
  '$route' (to, from) {
    // 对路由变化作出响应，在此处理业务逻辑
  }
  }
}
```

而且在 Vue.js 2.0 中，既可以在导航完成之前获取数据，也可以在导航完成之后获取数据。在导航完成之后获取数据，是为了在获取数据期间展示一个 loading 状态。可以在组件的 create() 钩子函数和 watch : { route : ' '} 中调用获取数据的函数。

在导航获取之前完成数据，我们可以在 beforeRouteEnter 钩子中获取数据，并且只有当数据获取成功或确定有权限后才进行组件的渲染，否则就回退到路由变化前的组件状态。

```JavaScript
import pageSrv from './api/pages' // 此处先模拟一个获取数据的模块
export default {
  data () {
    return {
      list : []
    }
  },
  beforeRouteEnter (to, from, next) {
    pageSrv.get(to.params.page, (err, data) => {
      if (err) {
        next(false); // 中断当前导航
      } else {
        next(vm => {
          vm.list = data;
        })
      }
    })
  },
  watch: {
    $route () {
      this.list = null;
      pageSrv.get(this.$route.params.id, (err, data) => {
        if (err) {
        // 处理展示错误的逻辑
        } else {
          this.list = data;
        }
      })
    }
  }
}
```

命名视图。Vue-router 2.0 中允许同级展示多个视图，而不是嵌套展示，可以通过给`<router-view>`添加 name 属性的方式匹配不同的组件，如果没有设置 name，默认为 default。

```JavaScript
<router-view></router-view>
<router-view name='main'></router-view>
const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: { // 要注意这里的属性是 components，而不是 component
        default: Nav,
        main: Main
      }
    }
  ]
})
```

## 7.2 Vue-resource
## 7.3 Vue-devtools

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

