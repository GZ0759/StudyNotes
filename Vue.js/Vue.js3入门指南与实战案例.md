> Vue 3 入门指南与实战案例  
> [原文地址](https://github.com/chengpeiquan/learning-vue3)

# 单组件的编写

项目搭好了，第一个要了解的肯定是组件的变化。

## 前置知识点

在开始编写组件之前，我们需要了解两个全新的前置知识点：`setup` 与 `defineComponent`。

### setup 函数

Vue 3.x 的 `composition api` 系列里，推出了一个全新的 `setup` 函数，它是一个组件选项，在创建组件之前执行，一旦 props 被解析，并作为组合式 API 的入口点。

基本语法：

```ts
import { defineComponent } from 'vue'

export default defineComponent({
  setup (props, context) {
    // 业务代码写这里...
    
    return {
      // 需要给template用的数据、函数放这里return出去...
    }
  }
})
```

### setup 参数

`setup` 函数包含了两个入参：

参数|类型|含义|是否必传
:--|:--|:--|:--
props|object|由父组件传递下来的数据|否
context|object|组件的执行上下文|否

**第一个参数 `props` ：**

它是响应式的（只要你不解构它，或者使用 [toRef / toRefs](#响应式-api-之-toref-与-torefs-new) 进行响应式解构），当传入新的 prop 时，它将被更新。

**第二个参数 `context` ：**

`context` 只是一个普通的对象，它暴露三个组件的 property：

属性|类型|作用
:--|:--|:--
attrs|非响应式对象|props 未定义的属性都将变成 attrs
slots|非响应式对象|插槽
emit|方法|触发事件

因为 `context` 只是一个普通对象，所以你可以直接使用 ES6 解构。也就是说，可用 `emit('xxx')` 来代替使用 `context.emit('xxx')`，另外两个功能也是如此。

但是 `attrs` 和 `slots` 请保持 `attrs.xxx`、`slots.xxx` 来使用他们数据，不要解构这两个属性，因为他们虽然不是响应式对象，但会随组件本身的更新而更新。

### defineComponent 函数

这是 Vue 3.x 推出的一个全新 API ，`defineComponent` 可以用于 `TypeScript` 的类型推导，帮你简化掉很多编写过程中的类型定义。

比如，你原本需要这样才可以使用 `setup`：

```ts
import { Slots } from 'vue'

// 声明props和return的数据类型
interface Data {
  [key: string]: unknown
}

// 声明context的类型
interface SetupContext {
  attrs: Data
  slots: Slots
  emit: (event: string, ...args: unknown[]) => void
}

// 使用的时候入参要加上声明，return也要加上声明
export default {
  setup(props: Data, context: SetupContext): Data {
    // ...

    return {
      // ...
    }
  }
}
```

是不是很繁琐？（肯定是啊！不用否定……

使用了 `defineComponent` 之后，你就可以省略这些类型定义：

```ts
import { defineComponent } from 'vue'

export default defineComponent({
  setup (props, context) {
    // ...
    
    return {
      // ...
    }
  }
})
```

而且不只适用于 `setup`，只要是 Vue 本身的 API ，`defineComponent` 都可以自动帮你推导。

在编写组件的过程中，你只需要维护自己定义的数据类型就可以了，专注于业务。

## 组件的生命周期

我们还需要先了解组件的生命周期，才能够灵活的把控好每一处代码的执行结果达到你的预期。

### 升级变化

从 2.x 升级到 3.x，在保留对 2.x 的生命周期支持的同时，3.x 也带来了一定的调整。

生命周期的变化，可以直观的从下表了解：

2.x 生命周期|3.x 生命周期|执行时间说明
:-:|:-:|:-:
beforeCreate|setup|组件创建前执行
created|setup|组件创建后执行
beforeMount|onBeforeMount|组件挂载到节点上之前执行
mounted|onMounted|组件挂载完成后执行
beforeUpdate|onBeforeUpdate|组件更新之前执行
updated|onUpdated|组件更新完成之后执行
beforeDestroy|onBeforeUnmount|组件卸载之前执行
destroyed|onUnmounted|组件卸载完成后执行
errorCaptured|onErrorCaptured|当捕获一个来自子孙组件的异常时激活钩子函数

其中，在3.x，`setup` 的执行时机比 2.x 的 `beforeCreate` 和 `created` 还早，可以完全代替原来的这 2 个钩子函数。

另外，被包含在 `<keep-alive>` 中的组件，会多出两个生命周期钩子函数：

2.x 生命周期|3.x 生命周期|执行时间说明
:-:|:-:|:-:
activated|onActivated|被激活时执行
deactivated|onDeactivated|切换组件后，原组件消失前执行

### 使用 3.x 的生命周期

在 3.x ，**每个生命周期函数都要先导入才可以使用**，并且所有生命周期函数统一放在 `setup` 里运行。

如果你需要在达到 2.x 的 `beforeCreate` 和 `created` 目的的话，直接把函数执行在 `setup` 里即可。

比如：

```ts
import { defineComponent, onBeforeMount, onMounted } from 'vue'

export default defineComponent({
  setup () {

    console.log(1);
    
    onBeforeMount( () => {
      console.log(2);
    });
    
    onMounted( () => {
      console.log(3);
    });

    console.log(4);

    return {}
  }
})
```

最终将按照生命周期的顺序输出：

```js
// 1
// 4
// 2
// 3
```

## 组件的基本写法

如果你是从 2.x 就开始写 TS 的话，应该知道在 2.x 的时候就已经有了 `extend` 和 `class component` 的基础写法；3.x 在保留 class 写法的同时，还推出了 `defineComponent` + `composition api`的新写法。

加上视图部分又有 `template` 和 `tsx` 的写法、以及 3.x 对不同版本的生命周期兼容，累计下来，在 Vue 里写 TS ，至少有 9 种不同的组合方式（我的认知内，未有更多的尝试），堪比孔乙己的回字（甚至吊打回字……

我们先来回顾一下这些写法组合分别是什么，了解一下 3.x 最好使用哪种写法：

### 回顾 2.x

在 2.x ，为了更好的 TS 推导，用的最多的还是 `class component` 的写法。

适用版本|基本写法|视图写法
:-:|:-:|:-:
2.x|Vue.extend|template
2.x|class component|template
2.x|class component|tsx

### 了解 3.x

目前 3.x 从官方对版本升级的态度来看， `defineComponent` 就是为了解决之前 2.x 对 TS 推导不完善等问题而推出的，尤大也是更希望大家习惯 `defineComponent` 的使用。

适用版本|基本写法|视图写法|生命周期版本|官方是否推荐
:-:|:-:|:-:|:-:|:-:
3.x|class component|template|2.x|×
3.x|defineComponent|template|2.x|×
3.x|defineComponent|template|3.x|√
3.x|class component|tsx|2.x|×
3.x|defineComponent|tsx|2.x|×
3.x|defineComponent|tsx|3.x|√

所以从接下来开始，都会以 `defineComponent` + `composition api` + `template` 的写法，并且按照 3.x 的生命周期来作为示范案例。

接下来，使用 `composition api` 来编写组件，先来实现一个最简单的 `Hello World!`。

在 3.x ，只要你的数据要在 `template` 中使用，就必须在 `setup` 里return出来。当然，只在函数中调用到，而不需要渲染到模板里的，则无需 return 。

```vue
<template>
  <p class="msg">{{ msg }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const msg = 'Hello World!';

    return {
      msg
    }
  }
})
</script>

<style lang="stylus" scoped>
.msg
  font-size 14px
</style>
```

和 2.x 一样，都是 `template` + `script` + `style` 三段式组合，上手非常简单。

`template` 和 2.x 可以说是完全一样（会有一些不同，比如 `router-link` 移除了 `tag` 属性等等，后面讲到了会说明）

`style` 则是根据你熟悉的预处理器或者原生 CSS 来写的，完全没有变化。

变化最大的就是 `script` 部分了。

## 响应式数据的变化 

响应式数据是 MVVM 数据驱动编程的特色，相信大部分人当初入坑 MVVM 框架，都是因为响应式数据编程比传统的操作 DOM 要来得方便，而选择 Vue ，则是方便中的方便。

在 3.x，响应式数据当然还是得到了保留，但是对比 2.x 的写法， 3.x 的步伐迈的有点大。

相对于 2.x 在 `data` 里定义后即可通过 `this.xxx` 来调用响应式数据，3.x 的生命周期里取消了 Vue 实例的 `this`，你要用到的比如 `ref` 、`reactive` 等响应式 API ，都必须通过导入才能使用，然后在 `setup` 里定义。

```ts
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const msg = ref<string>('Hello World!');

    return {
      msg
    }
  }
})
```

由于新的 API 非常多，但有些使用场景却不多，所以当前暂时只对常用的几个 API 做使用和踩坑说明，更多的 API 可以在官网查阅。

先放上官方文档：[响应性 API | Vue.js](https://v3.cn.vuejs.org/api/reactivity-api)

## 响应式 API 之 ref

`ref` 是最常用的一个响应式 API，它可以用来定义所有类型的数据，包括 Node 节点。

没错，在 2.x 常用的 `this.$refs.xxx` 来取代 `document.querySelector('.xxx')` 获取 Node 节点的方式，也是用这个 API 来取代。

### 类型声明

在开始使用 API 之前，要先了解一下在 `TypeScript` 中，`ref` 需要如何进行类型声明。

平时我们在定义变量的时候，都是这样给他们进行类型声明的：

```ts
// 单类型
const msg: string = 'Hello World!';

// 多类型
const phoneNumber: number | string = 13800138000;
```

但是在使用 `ref` 时，不能这样子声明，会报错，正确的声明方式应该是使用 `<>` 来包裹类型定义，紧跟在 `ref` API 之后：

```ts
// 单类型
const msg = ref<string>('Hello World!');

// 多类型
const phoneNumber = ref<number | string>(13800138000);
```

### 变量的定义

了解了如何进行类型声明之后，对变量的定义就没什么问题了，前面说了它可以用来定义所有类型的数据，包括 Node 节点，但不同类型的值之间还是有少许差异和注意事项，具体可以参考如下。

#### 基本类型

对字符串、布尔值等基本类型的定义方式，比较简单：

```ts
// 字符串
const msg = ref<string>('Hello World!');

// 数值
const count = ref<number>(1);

// 布尔值
const isVip = ref<boolean>(false);
```

#### 引用类型

对于对象、数组等引用类型也适用，比如要定义一个对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo = ref<Member>({
  id: 1,
  name: 'Tom'
});
```

定义一个普通数组：

```ts
// 数字数组
const uids = ref<number[]>([ 1, 2, 3 ]);

// 字符串数组
const names = ref<string[]>([ 'Tom', 'Petter', 'Andy' ]);
```

定义一个对象数组：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员组
const memberList = ref<Member[]>([
  {
    id: 1,
    name: 'Tom'
  },
  {
    id: 2,
    name: 'Petter'
  }
]);
```

### DOM 元素与子组件

除了可以定义数据，`ref` 也有我们熟悉的用途，就是用来挂载节点，也可以挂在子组件上。

对于 2.x 常用的 `this.$refs.xxx` 来获取 DOM 元素信息，该 API 的使用方式也是同样：

模板部分依然是熟悉的用法，把 ref 挂到你要引用的 DOM 上。

```vue
<template>
  <!-- 挂载DOM元素 -->
  <p ref="msg">
    留意该节点，有一个ref属性
  </p>
  <!-- 挂载DOM元素 -->

  <!-- 挂载子组件 -->
  <Child ref="child" />
  <!-- 挂载子组件 -->
</template>
```

`script` 部分有三个最基本的注意事项：

1. 定义挂载节点后，也是必须通过 `xxx.value` 才能正确操作到挂载的 DOM 元素或组件
2. 请保证视图渲染完毕后再执行 DOM 或组件的相关操作（需要放到生命周期的 `onMounted` 或者 `nextTick` 函数里，这一点在 2.x 也是一样）；
3. 该变量必须 `return` 出去才可以给到 `template` 使用（这一点是 3.x 生命周期的硬性要求，子组件的数据和方法如果要给父组件操作，也要 `return` 出来才可以）。

配合上面的 `template` ，来看看 `script` 部分的具体例子：

```ts
import { defineComponent, onMounted, ref } from 'vue'
import Child from '@cp/Child.vue'

export default defineComponent({
  components: {
    Child
  },
  setup () {
    // 定义挂载节点，声明的类型详见下方附表
    const msg = ref<HTMLElement | null>(null);
    const child = ref<typeof Child | null>(null);

    // 请保证视图渲染完毕后再执行节点操作 e.g. onMounted / nextTick
    onMounted( () => {
      // 比如获取DOM的文本
      console.log(msg.value.innerText);

      // 或者操作子组件里的数据
      child.value.isShowDialog = true;
    });

    // 必须return出去才可以给到template使用
    return {
      msg,
      child
    }
  }
})
```

关于 DOM 和子组件的 TS 类型声明，可参考以下规则：

节点类型|声明类型|参考文档
:--|:--|:--
DOM 元素|使用 HTML 元素接口|[HTML 元素接口](https://developer.mozilla.org/zh-CN/docs/Web/API/Document_Object_Model#html_%E5%85%83%E7%B4%A0%E6%8E%A5%E5%8F%A3)
子组件|使用 typeof 获取子组件的类型|[typeof 操作符](https://zhuanlan.zhihu.com/p/311150643)

另外，关于这一小节，有一个可能会引起 TS 编译报错的情况是，新版本的脚手架创建出来的项目会默认启用 `--strictNullChecks` 选项，会导致案例中的代码无法正常运行（报错 `TS2531: Object is possibly 'null'.` ）。

原因是：默认情况下 `null` 和 `undefined` 是所有类型的子类型，但开启了 `strictNullChecks` 选项之后，会使 `null` 和 `undefined` 只能赋值给 `void` 和它们各自，这虽然是个更为严谨的选项，但因此也会带来一些影响赶工期的额外操作。

**有以下几种解决方案可以参考：**

1. 在涉及到相关操作的时候，对节点变量增加一个判断：

```ts
if ( child.value ) {
  // 读取子组件的数据
  console.log(child.value.num);

  // 执行子组件的方法
  child.value.sayHi('use if in onMounted');
}
```

2. 通过 TS 的可选符 `?` 来将目标设置为可选，避免出现错误（这个方式不能直接修改子组件数据的值）

```ts
// 读取子组件的数据
console.log(child.value?.num);

// 执行子组件的方法
child.value?.sayHi('use ? in onMounted');
```

3. 在项目根目录下的 `tsconfig.json` 文件里，显式的关闭 `strictNullChecks` 选项，关闭后，由自己来决定是否需要对 `null` 进行判断：

```json
{
  "compilerOptions": {
    // ...
    "strictNullChecks": false
  },
  // ...
}
```

4. 使用 any 类型来代替，但是写 TS 还是尽量不要使用 any ，满屏的 AnyScript 不如写回 JS 。

### 变量的读取与赋值

被 `ref` 包裹的变量会全部变成对象，不管你定义的是什么类型的值，都会转化为一个 ref 对象，其中 ref 对象具有指向内部值的单个 property `.value`。

对于普通变量的值，读取的时候直接读变量名即可：

```ts
// 读取一个字符串
const msg: string = 'Hello World!';
console.log('msg的值', msg);

// 读取一个数组
const uids: number[] = [ 1, 2, 3 ];
console.log('第二个uid', uids[1]);
```

对 ref 对象的值的读取，切记！必须通过 value ！

```ts
// 读取一个字符串
const msg = ref<string>('Hello World!');
console.log('msg的值', msg.value);

// 读取一个数组
const uids = ref<number[]>([ 1, 2, 3 ]);
console.log('第二个uid', uids.value[1]);
```

普通变量都必须使用 `let` 才可以修改值，由于 ref 对象是个引用类型，所以可以在 `const` 定义的时候，直接通过 `.value` 来修改。

```ts
// 定义一个字符串变量
const msg = ref<string>('Hi!');

// 1s后修改它的值
setTimeout(() => {
  msg.value = 'Hello!'
}, 1000);
```

因此你在对接接口数据的时候，可以自由的使用 `forEach`、`map`、`filter` 等遍历函数来操作你的 ref 数组，或者直接重置它。

```ts
const data = ref<string[]>([]);

// 提取接口的数据
data.value = api.data.map( (item: any) => item.text );

// 重置数组
data.value = [];
```

问我为什么突然要说这个？因为涉及到下一部分的知识，关于 `reactive` 的。

## 响应式 API 之 reactive

`reactive` 是继 `ref` 之后最常用的一个响应式 API 了，相对于 `ref`，它的局限性在于只适合对象、数组。

### 类型声明与定义

`reactive` 的声明方式，以及定义方式，没有 `ref` 的变化那么大，就是和普通变量一样。

reactive 对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo: Member = reactive({
  id: 1,
  name: 'Tom'
});
```

reactive 数组：

```ts
// 普通数组
const uids: number[] = [ 1, 2, 3];

// 对象数组
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象数组
const userList: Member[] = reactive([
  {
    id: 1,
    name: 'Tom'
  },
  {
    id: 2,
    name: 'Petter'
  },
  {
    id: 3,
    name: 'Andy'
  }
]);
```

### 变量的读取与赋值

reactive 对象在读取字段的值，或者修改值的时候，与普通对象是一样的。

reactive 对象：

```ts
// 声明对象的格式
interface Member {
  id: number,
  name: string
};

// 定义一个成员对象
const userInfo: Member = reactive({
  id: 1,
  name: 'Tom'
});

// 读取用户名
console.log(userInfo.name);

// 修改用户名
userInfo.name = 'Petter';
```

但是对于 reactive 数组，和普通数组会有一些区别。

先看看普通数组，重置，或者改变值，都是可以直接轻松的进行操作：

```ts
// 定义一个普通数组
let uids: number[] = [ 1, 2, 3 ];

// 从另外一个对象数组里提取数据过来
uids = api.data.map( item => item.id );

// 合并另外一个数组
let newUids: number[] = [ 4, 5, 6 ];
uids = [...uids, ...newUids];

// 重置数组
uids = [];
```

在 2.x 的时候，你在操作数组时，完全可以和普通数组那样随意的处理数据的变化，依然能够保持响应性。

但在 3.x ，如果你使用 `reactive` 定义数组，则不能这么搞了，必须只使用那些不会改变引用地址的操作。

举个例子，比如你要从接口读取翻页数据的时候，通常要先重置数组，再异步添加数据：

如果你使用常规的重置，会导致这个变量失去响应性：

```ts
/** 
 * 不推荐使用这种方式
 * 异步添加数据后，模板不会响应更新
 */
let uids: number[] = reactive([ 1, 2, 3 ]);

// 丢失响应性的步骤
uids = [];

// 异步获取数据后，模板依然是空数组
setTimeout( () => {
  uids.push(1);
}, 1000);
```

要让模板那边依然能够保持响应性，则必须在关键操作时，不破坏响应性 API 的存在。

```ts
let uids: number[] = reactive([ 1, 2, 3 ]);

// 不会破坏响应性
uids.length = 0;

// 异步获取数据后，模板可以正确的展示
setTimeout( () => {
  uids.push(1);
}, 1000);
```

### 特别注意

不要对通过 `reactive` 定义的对象进行解构，解构后得到的变量会失去响应性。

比如这些情况，在 2s 后都得不到新的 name 信息：

```ts
import { defineComponent, reactive } from 'vue'

interface Member {
  id: number,
  name: string
};

export default defineComponent({
  setup () {

    // 定义一个带有响应性的成员对象
    const userInfo: Member = reactive({
      id: 1,
      name: 'Petter'
    });

    // 2s后更新userInfo
    setTimeout( () => {
      userInfo.name = 'Tom';
    }, 2000);

    // 这个变量在2s后不会同步更新
    const newUserInfo: Member = {...userInfo};

    // 这个变量在2s后不会再同步更新
    const { name } = userInfo;

    // 这样return出去给模板用，在2s后也不会同步更新
    return {
      ...userInfo
    }
  }
})
```

## 响应式 API 之 toRef 与 toRefs

为了方便开发者，Vue 3.x 还推出了 2 个相关的 API ，用于 `reactive` 向 `ref` 转换。

### 各自的作用

两个 API 的拼写非常接近，顾名思义，一个是只转换一个字段，一个是转换所有字段。

API|作用
:--|:--
toRef|创建一个新的ref变量，转换 reactive 对象的某个字段为ref变量
toRefs|创建一个新的对象，它的每个字段都是 reactive 对象各个字段的ref变量

我们先定义好一个 `reactive` 变量：

```ts
interface Member {
  id: number,
  name: string
};

const userInfo: Member = reactive({
  id: 1,
  name: 'Petter'
});
```

然后来看看这 2 个 API 应该怎么使用。

### 使用 toRef

`toRef` 接收 2 个参数，第一个是 `reactive` 对象, 第二个是要转换的 `key` 。

在这里我们只想转换 `userInfo` 里的 `name` ，只需要这样操作：

```ts
const name: string = toRef(userInfo, 'name');
```

这样就成功创建了一个 `ref` 变量。

之后读取和赋值就使用 `name.value`，它会同时更新 `name` 和 `userInfo.name`。 

在 `toRef` 的过程中，如果使用了原对象上面不存在的 `key` ，那么定义出来的变量的 `value` 将会是 `undefined` 。如果你对这个不存在的 `key` 的 `ref` 变量，进行了 `value` 赋值，那么原来的对象也会同步增加这个 `key`，其值也会同步更新。

### 使用 toRefs

`toRefs` 接收 1 个参数，是一个 `reactive` 对象。

```ts
const userInfoRefs: Member = toRefs(userInfo);
```

这个新的 `userInfoRefs` ，本身是个普通对象，但是它的每个字段，都是与原来关联的 `ref` 变量。

### 为什么要进行转换

关于为什么要出这么 2 个 API ，官方文档没有特别说明，不过经过自己的一些实际使用。

`ref` 和 `reactive` 这两者的好处就不重复了，但是在使用的过程中，各自都有各自不方便的地方：

1. `ref` 虽然在 `template` 里使用起来方便，但比较烦的一点是在 `script` 里进行读取/赋值的时候，要一直记得加上 `.value` 属性
2. `reactive` 虽然在使用的时候，因为你知道它本身是一个 `Object` 类型，所以你不会忘记 `foo.bar` 这样的格式去操作，但是在 `template` 渲染的时候，你又因此不得不每次都使用 `foo.bar` 的格式去渲染

那么有没有办法，既可以在编写 `script` 的时候不容易出错，在写 `template` 的时候又比较简单呢？

于是， `toRef` 和 `toRefs` 因此诞生。

### 什么场景下比较适合使用它们

从便利性和可维护性来说，最好只在功能单一、代码量少的组件里使用，比如一个表单组件，通常表单的数据都放在一个对象里。

当然你也可以更猛一点就是把所有的数据都定义到一个 `data` 里，然后你再去 `data` 里面取…但是没有必要为了转换而转换。

### 在业务中的具体运用

这一部分我一直用 `userInfo` 来当案例，那就继续以一个用户信息表的小 demo 来做这个的演示吧。

**在 `script` 部分：**

1. 先用 `reactive` 定义一个源数据，所有的数据更新，都是修改这个对象对应的值，按照对象的写法去维护你的数据
2. 再通过 `toRefs` 定义一个给 `template` 用的对象，它本身不具备响应性，但是它的字段全部是 `ref` 变量
3. 在 `return` 的时候，对 `toRefs` 对象进行解构，这样导出去就是各个字段对应的 `ref` 变量，而不是一整个对象

```ts
import { defineComponent, reactive, toRefs } from 'vue'

interface Member {
  id: number,
  name: string,
  age: number,
  gender: string
};

export default defineComponent({
  setup () {
    // 定义一个reactive对象
    const userInfo = reactive({
      id: 1,
      name: 'Petter',
      age: 18,
      gender: 'male'
    })

    // 定义一个新的对象，它本身不具备响应性，但是它的字段全部是ref变量
    const userInfoRefs = toRefs(userInfo);

    // 2s后更新userInfo
    setTimeout( () => {
      userInfo.id = 2;
      userInfo.name = 'Tom';
      userInfo.age = 20;
    }, 2000);

    // 在这里结构toRefs对象才能继续保持响应式
    return {
      ...userInfoRefs
    }
  }
})
```

**在 `template` 部分：**

由于 `return` 出来的都是 `ref` 变量，所以你在模板里直接使用 `userInfo` 各个字段的 `key` 即可。

```vue
<template>
  <ul class="user-info">

    <li class="item">
      <span class="key">ID:</span>
      <span class="value">{{ id }}</span>
    </li>

    <li class="item">
      <span class="key">name:</span>
      <span class="value">{{ name }}</span>
    </li>

    <li class="item">
      <span class="key">age:</span>
      <span class="value">{{ age }}</span>
    </li>

    <li class="item">
      <span class="key">gender:</span>
      <span class="value">{{ gender }}</span>
    </li>

  </ul>
</template>
```

### 需要注意的问题

请注意是否有相同命名的变量存在，比如上面在 `return` 给 `template` 使用时，解构 `userInfoRefs` 的时候已经包含了一个 `name` 字段，此时如果还有一个单独的变量也叫 `name`。

这种情况下，会以单独定义的 `name` 为渲染数据。

```ts
return {
  ...userInfoRefs,
  name
}
```

这种情况下，则是以 `userInfoRefs` 里的 `name` 为渲染数据。

```ts
return {
  name,
  ...userInfoRefs
}
```

所以当你决定使用 `toRef` 和 `toRefs` 的时候，请注意这个特殊情况！

## 函数的定义和使用

在了解了响应式数据如何使用之后，接下来就要开始了解函数了。

在 2.x，函数都是放在 `methods` 对象里定义，然后再在 `mounted` 等生命周期或者模板里通过 `click` 使用。

但在 3.x 的生命周期里，和数据的定义一样，都是通过 `setup` 来完成。

1. 你可以在 `setup` 里定义任意类型的函数（普通函数、class 类、箭头函数、匿名函数等等）
2. 需要自动执行的函数，执行时机需要遵循生命周期
3. 需要暴露给模板去通过 `click`、`change` 等行为来触发的函数，需要把函数名在 `setup` 里进行 `return` 才可以在模板里使用

简单写一下例子：

```vue
<template>
  <p>{{ msg }}</p>

  <!-- 在这里点击执行return出来的方法 -->
  <button @click="changeMsg">修改MSG</button>
  <!-- 在这里点击执行return出来的方法 -->
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue'

export default defineComponent({
  setup () {
    const msg = ref<string>('Hello World!');

    // 这个要暴露给模板使用，必须return才可以使用
    function changeMsg () {
      msg.value = 'Hi World!';
    }

    // 这个要在页面载入时执行，无需return出去
    const init = () => {
      console.log('init');
    }

    // 在这里执行init
    onMounted( () => {
      init();
    });

    return {
      // 数据
      msg,

      // 方法
      changeMsg
    }
  }
})
</script>
```

## 数据的监听

监听数据变化也是组件里的一项重要工作，比如监听路由变化、监听参数变化等等。

Vue 3.x 在保留原来的 `watch` 功能之外，还新增了一个 `watchEffect` 帮助我们更简单的进行监听。

### watch

但是新版的 `watch` 和旧版对比，在使用方式上变化非常大！旧版是这样用的，和 `data` 、 `methods` 都在同级配置：

```ts
// 旧版的写法：
export default {
  watch: {
    // ...
  },
  data () {
    return {
      // ...
    }
  },
  methods: {
    // ...
  }
}
```

新版的 `watch` 需要在 `setup` 里使用，在使用之前，**还需要先导入该组件**。

```ts
import { defineComponent, ref, watch } from 'vue'

export default defineComponent({
  setup () {
    const name = ref<string>('Petter');

    // 2s后改变数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 你可以监听一个响应式对象
    watch( name, () => {
      console.log('监听整个 ref ', name.value);
    })

    // 也可以监听对象里面的某个值（此时需要写成 getter 函数）
    watch( () => name.value, () => {
      console.log('只监听 value ', name.value);
    })
  }
})
```

需要注意的是，你只能监听响应式数据，如果通过 `let` 定义一个普通的字符串变量，然后去改变字符串内容，这样是无法监听的。

另外，默认情况下，`watch` 是惰性的，即只有当被侦听的源发生变化时才执行回调。

> 新的 `watch` 默认是深度监听，无需再手动指定 `deep` 。

另外， `watch` 可以接受两个参数：

参数|类型|作用
:--|:--|:--
newVal|any|变化后的新值
oldVal|any|变化前的旧值

这里返回的参数类型并没有特定限制，取决于你监听的数据类型变化。

```ts
export default defineComponent({
  setup () {
    const name = ref<string>('Petter');

    // 2s后改变数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 你可以监听一个响应式对象
    watch( name, (newVal, oldVal) => {
      console.log('打印变化前后的值', { oldVal, newVal });
    })

    return {
      name
    }
  }
})
```

注意：第一个参数是新值，第二个才是原来的旧值！

### watchEffect

如果一个函数里包含了多个需要监听的数据，一个一个数据去监听太麻烦了，在 3.x ，你可以直接使用 `watchEffect` 来简化你的操作。

它立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。

```ts
import { defineComponent, ref, watchEffect } from 'vue'

export default defineComponent({
  setup () {
    // 单独定义两个数据，后面用来分开改变数值
    const name = ref<string>('Petter');
    const age = ref<number>(18);

    // 定义一个调用这两个数据的函数
    const getUserInfo = (): void => {
      console.log({
        name: name.value,
        age: age.value
      });
    }

    // 2s后改变第一个数据
    setTimeout(() => {
      name.value = 'Tom';
    }, 2000);

    // 4s后改变第二个数据
    setTimeout(() => {
      age.value = 20;
    }, 4000);

    // 直接监听调用函数，在每个数据产生变化的时候，它都会自动执行
    watchEffect(getUserInfo);
  }
})
```

虽然理论上 `watchEffect` 是 `watch` 的一个简化操作，但他们也有一定的区别：

1. `watch` 可以访问侦听状态变化前后的值，而 `watchEffect` 没有。
2. `watch` 是在属性改变的时候才执行，而 `watchEffect` 则默认会执行一次，然后在属性改变的时候也会执行。

## 数据的计算

和 Vue 2.0 一样，数据的计算也是使用 `computed` API ，它可以通过现有的响应式数据，去通过计算得到新的响应式变量，用过 Vue 2.0 的同学应该不会太陌生，但是在 Vue 3.0 ，在使用方式上也是变化非常大！

这里的响应式数据，可以简单理解为通过 ref API 、 reactive API 定义出来的数据，当然 Vuex 、Vue Router 等 Vue 数据也都具备响应式。

### 用法变化

我们先从一个简单的用例来看看在 Vue 新旧版本的用法区别：

假设你定义了两个分开的数据 `firstName` 名字和 `lastName` 姓氏，但是在 template 展示时，需要展示完整的姓名，那么你就可以通过 `computed` 来计算一个新的数据：

#### 回顾 2.x

在 Vue 2.0 ，`computed` 和 `data` 在同级配置，并且不可以和 `data` 里的数据同名重复定义：

```ts
// 在 Vue 2 的写法：
export default {
  data() {
    return {
      firstName: 'Bill',
      lastName: 'Gates',
    }
  },
  // 注意这里定义的变量，都要通过函数的形式来返回它的值
  computed: {
    // 普通函数可以直接通过熟悉的 this 来拿到 data 里的数据
    fullName() {
      return `${this.firstName} ${this.lastName}`
    },
    // 箭头函数则需要通过参数来拿到实例上的数据
    fullName2: (vm) => `${vm.firstName} ${vm.lastName}`,
  }
}
```

这样你在需要用到全名的地方，只需要通过 `this.fullName` 就可以得到 `Bill Gates` 。

#### 了解 3.x

在 Vue 3.0 ，跟其他 API 的用法一样，需要先导入 `computed` 才能使用：

```ts
// 在 Vue 3 的写法：
import { defineComponent, ref, computed } from 'vue'

export default defineComponent({
  setup() {
    // 定义基本的数据
    const firstName = ref<string>('Bill')
    const lastName = ref<string>('Gates')

    // 定义需要计算拼接结果的数据
    const fullName = computed(() => `${firstName.value} ${lastName.value}`)

    // 2s 后改变某个数据的值
    setTimeout(() => {
      firstName.value = 'Petter'
    }, 2000)

    // template 那边在 2s 后也会显示为 Petter Gates
    return {
      fullName,
    }
  },
})
```

你可以把这个用法简单的理解为，传入一个回调函数，并 `return` 一个值，对，它需要有明确的返回值。

需要注意的是：

1. 定义出来的 `computed` 变量，和 `ref` 变量的用法一样，也是需要通过 `.value` 才能拿到它的值

2. 但是区别在于， `computed` 的 `value` 是只读的

原因详见下方的 [类型定义](#类型定义) 。

### 类型定义

我们之前说过，在 defineComponent 里，会自动帮我们推导 Vue API 的类型，所以一般情况下，你是不需要显式的去定义 `computed` 出来的变量类型的。

在确实需要手动指定的情况下，你也可以导入它的类型然后定义：

```ts
import { computed } from 'vue'
import type { ComputedRef } from 'vue'

// 注意这里添加了类型定义
const fullName: ComputedRef<string> = computed(
  () => `${firstName.value} ${lastName.value}`
)
```

你要返回一个字符串，你就写 `ComputedRef<string>` ；返回布尔值，就写 `ComputedRef<boolean>` ；返回一些复杂对象信息，你可以先定义好你的类型，再诸如 `ComputedRef<UserInfo>` 去写。

```ts
// 这是 ComputedRef 的类型定义：
export declare interface ComputedRef<T = any> extends WritableComputedRef<T> {
  readonly value: T;
  [ComoutedRefSymbol]: true;
}
```

### 优势对比和注意事项

在继续往下看之前，我们先来了解一下这个 API 的一些优势和注意事项。

#### 优势对比

看到这里，相信刚接触的同学可能会有疑问，既然 `computed` 也是通过一个函数来返回值，那么和普通的 `function` 有什么区别，或者说优势？

1. 性能优势

数据的计算是基于它们的响应依赖关系缓存的，只在相关响应式依赖发生改变时它们才会重新求值。

也就是说，只要原始数据没有发生改变，多次访问 `computed` ，都是会立即返回之前的计算结果，而不是再次执行函数；而普通的 `function` 调用多少次就执行多少次，每调用一次就计算一次。

至于为何要如此设计，官网文档也给出了原因：

> 我们为什么需要缓存？假设我们有一个性能开销比较大的计算数据 list，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算数据依赖于 list。如果没有缓存，我们将不可避免的多次执行 list 的 getter！如果你不希望有缓存，请用 function 来替代。

2. 书写统一

我们假定 foo1 是 `ref` 变量， foo2 是 `computed` 变量， foo3 是普通函数返回值。

看到这里的同学应该都已经清楚 Vue 3 的 `ref` 变量是通过 `foo1.value` 来拿到值的，而 `computed` 也是通过 `foo2.value` ，并且在 template 里都可以省略 `.value` ，在读取方面，他们是有一致的风格和简洁性。

而 foo3 不管是在 script 还是 template ，都需要通过 `foo3()` 才能拿到结果，相对来说会有那么一丢丢别扭。

当然，关于这一点，如果涉及到的数据不是响应式数据，那么还是老老实实的用函数返回值吧 。

#### 注意事项

有优势当然也就有一定的 “劣势” ，当然这也是 Vue 框架的有意为之，所以在使用上也需要注意一些问题：

1. 只会更新响应式数据的计算

假设你要获取当前的时间信息，因为不是响应式数据，所以这种情况下你就需要用普通的函数去获取返回值，才能拿到最新的时间。

```ts
const nowTime = computed(() => new Date())
console.log(nowTime.value)
// 输出 Sun Nov 14 2021 21:07:00 GMT+0800 (GMT+08:00)

// 2s 后依然是跟上面一样的结果
setTimeout(() => {
  console.log(nowTime.value)
  // 还是输出 Sun Nov 14 2021 21:07:00 GMT+0800 (GMT+08:00)
}, 2000)
```

2. 数据是只读的

通过 computed 定义的数据，它是只读的。

如果你直接赋值，不仅无法变更数据，而且会收获一个报错。

```bash
TS2540: Cannot assign to 'value' because it is a read-only property.
```

虽然无法直接赋值，但是在必要的情况下，你依然可以通过 `computed` 的 `setter` 来更新数据。

### setter 的使用

通过 computed 定义的变量默认都是只读的形式（只有一个 getter ），但是在必要的情况下，你也可以使用其 setter 属性来更新数据。

#### 基本格式

当你需要用到 setter 的时候， `computed` 就不再是一个传入 callback 的形式了，而是传入一个带有 2 个方法的对象。

```ts
// 注意这里computed接收的入参已经不再是函数
const foo = computed({
  // 这里需要明确的返回一个值
  get() {
    // ...
  },
  // 这里接收一个参数，代表修改 foo 时，赋值下来的新值
  set(newValue) {
    // ...
  },
})
```

这里的 `get` 就是 `computed` 的 getter ，跟原来传入 callback 的形式一样，是用于 `foo.value` 的读取，所以这里你必须有明确的返回值。

这里的 `set` 就是 `computed` 的 setter ，它会接收一个参数，代表新的值，当你通过 `foo.value = xxx` 赋值的时候，赋入的这个值，就会通过这个入参来传递进来，你可以根据你的业务需要，把这个值，赋给相关的数据源。

在了解了基本格式后，可以查看下面的例子来了解具体的用法。

#### 使用示范

官网的 [例子](https://v3.cn.vuejs.org/guide/computed.html#%E8%AE%A1%E7%AE%97%E5%B1%9E%E6%80%A7%E7%9A%84-setter) 是一个 Options API 的案例，这里我们改成 Composition API 的写法来演示：

```ts
// 还是这2个数据源
const firstName = ref<string>('Bill')
const lastName = ref<string>('Gates')

// 这里我们配合setter的需要，改成了另外一种写法
const fullName = computed({
  // getter我们还是返回一个拼接起来的全名
  get() {
    return `${firstName.value} ${lastName.value}`
  },
  // setter这里我们改成只更新firstName，注意参数也定义TS类型
  set(newFirstName: string) {
    firstName.value = newFirstName
  },
})
console.log(fullName.value) // 输出 Bill Gates

// 2s后更新一下数据
setTimeout(() => {
  // 对fullName的赋值，其实更新的是firstName
  fullName.value = 'Petter'

  // 此时firstName已经得到了更新
  console.log(firstName.value) // 会输出 Petter

  // 当然，由于firstName变化了，所以fullName的getter也会得到更新
  console.log(fullName.value) // 会输出 Petter Gates
}, 2000)
```

### 应用场景

计算 API 的作用，官网文档只举了一个非常简单的例子，那么在实际项目中，什么情况下用它会让我们更方便呢？

简单举几个比较常见的例子吧，加深一下对 `computed` 的理解。

#### 数据的拼接和计算

如上面的案例，与其每个用到的地方都要用到 `firstName + ' ' + lastName` 这样的多变量拼接，不如用一个 `fullName` 来的简单。

当然，不止是字符串拼接，数据的求和等操作更是合适，比如说你做一个购物车，购物车里有商品列表，同时还要显示购物车内的商品总金额，这种情况就非常适合用计算数据。

#### 复用组件的动态数据

在一个项目里，很多时候组件会涉及到复用，比如说：“首页的文章列表 vs 列表页的文章列表 vs 作者详情页的文章列表” ，特别常见于新闻网站等内容资讯站点，这种情况下，往往并不需要每次都重新写 UI 、数据渲染等代码，仅仅是接口 URL 的区别。

这种情况你就可以通过路由名称来动态获取你要调用哪个列表接口：

```ts
const route = useRoute()

// 定义一个根据路由名称来获取接口URL的计算数据
const apiUrl = computed(() => {
  switch (route.name) {
    // 首页
    case 'home':
      return '/api/list1'
    // 列表页
    case 'list':
      return '/api/list2'
    // 作者页
    case 'author':
      return '/api/list3'
    // 默认是随机列表
    default:
      return '/api/random'
  }
})

// 请求列表
const getArticleList = async (): Promise<void> => {
  // ...
  articleList.value = await axios({
    method: 'get',
    url: apiUrl.value,
    // ...
  })
  // ...
}
```

当然，这种情况你也可以在父组件通过 `props` 传递接口 URL ，如果你已经学到了 [组件通讯](communication.md) 一章的话。

#### 获取多级对象的值

你应该很经常的遇到要在 template 显示一些多级对象的字段，但是有时候又可能存在某些字段不一定有，需要做一些判断的情况，虽然有 `v-if` ，但是嵌套层级一多，你的模板会难以维护。

如果你把这些工作量转移给计算数据，结合 `try / catch` ，这样就无需在 template 里处理很多判断了。

```ts
// 例子比较极端，但在 Vuex 这种大型数据树上，也不是完全不可能存在
const foo = computed(() => {
  // 正常情况下返回需要的数据
  try {
    return store.state.foo3.foo2.foo1.foo
  }
  // 处理失败则返回一个默认值
  catch (e) {
    return ''
  }
})
```

这样你在 template 里要拿到 foo 的值，完全不需要关心中间一级又一级的字段是否存在，只需要区分是不是默认值。

#### 不同类型的数据转换

有时候你会遇到一些需求类似于，让用户在输入框里，按一定的格式填写文本，比如用英文逗号 `,` 隔开每个词，然后保存的时候，是用数组的格式提交给接口。

这个时候 `computed` 的 setter 就可以妙用了，只需要一个简单的 `computed` ，就可以代替 `input` 的 `change` 事件或者 `watch` 监听，可以减少很多业务代码的编写。

```vue
<template>
  <input
    type="text"
    v-model="tagsStr"
    placeholder="请输入标签，多个标签用英文逗号隔开"
  />
</template>

<script lang="ts">
import { defineComponent, computed, ref } from 'vue'

export default defineComponent({
  setup() {
    // 这个是最终要用到的数组
    const tags = ref<string[]>([])

    // 因为input必须绑定一个字符串
    const tagsStr = computed({
      // 所以通过getter来转成字符串
      get() {
        return tags.value.join(',')
      },
      // 然后在用户输入的时候，切割字符串转换回数组
      set(newValue: string) {
        tags.value = newValue.split(',')
      },
    })

    return {
      tagsStr,
    }
  },
})
</script>
```

## CSS 样式与预处理器

Vue 组件的 CSS 样式部分，3.x 保留着和 2.x 完全一样的写法。 

### 编写组件样式表

最基础的写法，就是在 Vue 文件里创建一个 `style` 标签，即可在里面写 CSS 代码了。

```vue
<style>
.msg {
  width: 100%;
}
.msg p {
  color: #333;
  font-size: 14px;
}
</style>
```

### 动态绑定 CSS

动态绑定 CSS ，在 Vue 2.x 就已经存在了，在此之前常用的是 `:class` 和 `:style` ，现在在 Vue 3.x ，还可以通过 `v-bind` 来动态修改了。

其实这一部分主要是想说一下 3.x 新增的 `<style> v-bind` 功能，不过既然写到这里，就把另外两个动态绑定方式也一起提一下。

#### 使用 :class 动态修改样式名

它是绑定在 DOM 元素上面的一个属性，跟 `class` 同级别，它非常灵活！

假设我们已经提前定义好了这几个变量：

```vue
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const activeClass = 'active-class'
    const activeClass1 = 'active-class1'
    const activeClass2 = 'active-class2'
    const isActive = true

    return {
      activeClass,
      activeClass1,
      activeClass2,
      isActive,
    }
  }
})
</script>
```

如果只想绑定一个单独的动态样式，你可以传入一个字符串：

```vue
<template>
  <p :class="activeClass">Hello World!</p>
</template>
```

如果有多个动态样式，也可以传入一个数组：

```vue
<template>
  <p :class="[activeClass1, activeClass2]">Hello World!</p>
</template>
```

你还可以对动态样式做一些判断，这个时候传入一个对象：

```vue
<template>
  <p :class="{ 'active-class': isActive }">Hello World!</p>
</template>
```

多个判断的情况下，记得也用数组套起来：

```vue
<template>
  <p
    :class="[
      { activeClass1: isActive },
      { activeClass2: !isActive }
    ]"
  >
    Hello World!
  </p>
</template>
```

那么什么情况下会用到 `:class` 呢？

最常见的场景，应该就是导航、选项卡了，比如你要给一个当前选中的选项卡做一个突出高亮的状态，那么就可以使用 `:class` 来动态绑定一个样式。

```vue
<template>
  <ul class="list">
    <li
      class="item"
      :class="{ cur: index === curIndex }"
      v-for="(item, index) in 5"
      :key="index"
      @click="curIndex = index"
    >
      {{ item }}
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const curIndex = ref<number>(0)

    return {
      curIndex,
    }
  }
})
</script>

<style scoped>
.cur {
  color: red;
}
</style>
```

这样就简单实现了一个点击切换选项卡高亮的功能。

#### 使用 :style 动态修改内联样式

如果你觉得使用 `:class` 需要提前先写样式，再去绑定样式名有点繁琐，有时候只想简简单单的修改几个样式，那么你可以通过 `:style` 来处理。

默认的情况下，我们都是传入一个对象去绑定：

- `key` 是符合 CSS 属性名的 “小驼峰式” 写法，或者套上引号的短横线分隔写法（原写法），例如在 CSS 里，定义字号是 `font-size` ，那么你需要写成 `fontSize` 或者 `'font-size'` 作为它的键。
- `value` 是 CSS 属性对应的 “合法值”，比如你要修改字号大小，可以传入 `13px` 、`0.4rem` 这种带合法单位字符串值，但不可以是 `13` 这样的缺少单位的值，无效的 CSS 值会被过滤不渲染。

```vue
<template>
  <p
    :style="{
      fontSize: '13px',
      'line-height': 2,
      color: '#ff0000',
      textAlign: 'center'
    }"
  >
    Hello World!
  </p>
</template>
```

如果有些特殊场景需要绑定多套 `style`，你需要在 `script` 先定义好各自的样式变量（也是符合上面说到的那几个要求的对象），然后通过数组来传入：

```vue
<template>
  <p
    :style="[style1, style2]"
  >
    Hello World!
  </p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const style1 = {
      fontSize: '13px',
      'line-height': 2,
    }
    const style2 = {
      color: '#ff0000',
      textAlign: 'center',
    }

    return {
      style1,
      style2,
    }
  }
})
</script>
```

#### 使用 v-bind 动态修改 style

当然，以上两种形式都是关于 `<script />` 和 `<template />` 部分的相爱相杀，如果你觉得会给你的模板带来一定的维护成本的话，不妨考虑这个新方案，将变量绑定到 `<style />` 部分去。

我们先来看看基本的用法：

```vue
<template>
  <p class="msg">Hello World!</p>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const fontColor = ref<string>('#ff0000')

    return {
      fontColor,
    }
  }
})
</script>

<style scoped>
.msg {
  color: v-bind(fontColor);
}
</style>
```

如上面的代码，你将渲染出一句红色文本的 `Hello World!`

这其实是利用了现代浏览器支持的 CSS 变量来实现的一个功能（所以如果你打算用它的话，需要提前注意一下兼容性噢，点击查看：[CSS Variables 兼容情况](https://caniuse.com/css-variables)）

它渲染到 DOM 上，其实也是通过绑定 `style` 来实现，我们可以看到渲染出来的样式是：

```html
<p
  class="msg"
  data-v-7eb2bc79=""
  style="--7eb2bc79-fontColor:#ff0000;"
>
  Hello World!
</p>
```

对应的 CSS 变成了：

```css
.msg[data-v-7eb2bc79] {
  color: var(--7eb2bc79-fontColor);
}
```

理论上 `v-bind` 函数可以在 Vue 内部支持任意的 JS 表达式，但由于可能包含在 CSS 标识符中无效的字符，因此官方是建议在大多数情况下，用引号括起来，如：

```css
.text {
  font-size: v-bind('theme.font.size');
}
```

由于 CSS 变量的特性，因此对 CSS 响应式属性的更改不会触发模板的重新渲染（这也是和 `:class` 与 `:style` 的最大不同）。

不管你有没有开启 [\<style scoped\>](#style-scoped) ，使用 `v-bind` 渲染出来的 CSS 变量，都会带上 `scoped` 的随机 hash 前缀，避免样式污染（永远不会意外泄漏到子组件中），所以请放心使用！

如果你对 CSS 变量的使用还不是很了解的话，可以先阅读一下相关的基础知识点。

### 样式表的组件作用域

CSS 不像 JS ，是没有作用域的概念的，一旦写了某个样式，直接就是全局污染。所以 [BEM 命名法](https://www.bemcss.com/) 等规范才应运而生。

但在 Vue 组件里，有两种方案可以避免出现这种污染问题。

一个是 Vue 2.x 就有的 `<style scoped>` ，一个是 Vue 3.x 新推出的 `<style module>` 。

#### style scoped

Vue 组件在设计的时候，就想到了一个很优秀的解决方案，通过 `scoped` 来支持创建一个 CSS 作用域，使这部分代码只运行在这个组件渲染出来的虚拟 DOM 上。

使用方式很简单，只需要在 `style` 后面带上 `scoped` 属性。

```vue
<style scoped>
.msg {
  width: 100%;
}
.msg p {
  color: #333;
  font-size: 14px;
}
</style>
```

编译后，虚拟 DOM 都会带有一个 `data-v-xxxxx` 这样的属性，其中 `xxxxx` 是一个随机生成的 hash ，同一个组件的 hash 是相同并且唯一的：

```html
<div class="msg" data-v-7eb2bc79>
  <p data-v-7eb2bc79>Hello World!</p>
</div>
```

而 CSS 则也会带上与 HTML 相同的属性，从而达到样式作用域的目的。

```css
.msg[data-v-7eb2bc79] {
  width: 100%;
}
.msg p[data-v-7eb2bc79] {
  color: #333;
  font-size: 14px;
}
```

使用 `scoped` 可以有效的避免全局样式污染，你可以在不同的组件里面都使用相同的 className，而不必担心会相互覆盖，不必再定义很长很长的样式名来防止冲突了。

#### style module

这是在 Vue 3.x 才推出的一个新方案，和 `<style scoped>` 不同，scoped 是通过给 DOM 元素添加自定义属性的方式来避免冲突，而 `<style module>` 则更为激进，将会编译成 [CSS Modules](https://github.com/css-modules/css-modules) 。

对于 CSS Modules 的处理方式，我们也可以通过一个小例子来更直观的了解它：

```css
/* 编译前 */
.title {
  color: red;
}

/* 编译后 */
._3zyde4l1yATCOkgn-DBWEL {
  color: red;
}
```

可以看出，是通过比较 “暴力” 的方式，把我们编写的 “好看的” 样式名，直接改写成一个随机 hash 样式名，来避免样式互相污染。

>上面的案例来自阮老师的博文 [CSS Modules 用法教程](https://www.ruanyifeng.com/blog/2016/06/css_modules.html) 

所以我们回到 Vue 这边，看看 `<style module>` 是怎么操作的。

```vue
<template>
  <p :class="$style.msg">Hello World!</p>
</template>

<style module>
.msg {
  color: #ff0000;
}
</style>
```

于是，你将渲染出一句红色文本的 `Hello World!` 。

- 如果单纯只使用 `<style module>` ，那么在绑定样式的时候，是默认使用 `$style` 对象来操作的
- 必须显示的指定绑定到某个样式，比如 `$style.msg` ，才能生效
- 如果单纯的绑定 `$style` ，并不能得到 “把全部样式名直接绑定” 的期望结果
- 如果你指定的 className 是短横杆命名，比如 `.user-name` ，那么需要通过 `$style['user-name']` 去绑定

你也可以给 `module` 进行命名，然后就可以通过你命名的 “变量名” 来操作：

```vue
<template>
  <p :class="classes.msg">Hello World!</p>
</template>

<style module="classes">
.msg {
  color: #ff0000;
}
</style>
```

需要注意的一点是，一旦开启 `<style module>` ，那么在 `<style module>` 里所编写的样式，都必须手动绑定才能生效，没有被绑定的样式，会被编译，但不会主动生效到你的 DOM 上。

原因是编译出来的样式名已经变化，而你的 DOM 未指定对应的样式名，或者指定的是编译前的命名，所以并不能匹配到正确的样式。

#### useCssModule

这是一个全新的 API ，面向在 script 部分操作 CSS Modules 。

在上面的 [CSS Modules](#style-module-new) 部分可以知道，你可以在 `style` 定义好样式，然后在 `template` 部分通过变量名来绑定样式。

那么如果有一天有个需求，你需要通过 `v-html` 来渲染 HTML 代码，那这里的样式岂不是凉凉了？当然不会！

Vue 3.x 提供了一个 Composition API `useCssModule` 来帮助你在 `setup` 函数里操作你的 CSS Modules 。

**基本用法：**

我们绑定多几个样式，再来操作：

```vue
<template>
  <p :class="$style.msg">
    <span :class="$style.text">Hello World!</span>
  </p>
</template>

<script lang="ts">
import { defineComponent, useCssModule } from 'vue'

export default defineComponent({
  setup () {
    const style = useCssModule()
    console.log(style)
  }
})
</script>

<style module>
.msg {
  color: #ff0000;
}
.text {
  font-size: 14px;
}
</style>
```

可以看到打印出来的 `style` 是一个对象：

- `key` 是你在 `<style modules>` 里定义的原始样式名
- `value` 则是编译后的新样式名

```js
{
  msg: 'home_msg_37Xmr',
  text: 'home_text_2woQJ'
}
```

所以我们来配合 [模板字符串](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Template_literals) 的使用，看看刚刚说的，要通过 `v-html` 渲染出来的内容应该如何绑定样式：

```vue
<template>
  <div v-html="content"></div>
</template>

<script lang="ts">
import { defineComponent, useCssModule } from 'vue'

export default defineComponent({
  setup () {
    // 获取样式
    const style = useCssModule()

    // 编写模板内容
    const content = `<p class="${style.msg}">
      <span class="${style.text}">Hello World! —— from v-html</span>
    </p>`

    return {
      content,
    }
  }
})
</script>

<style module>
.msg {
  color: #ff0000;
}
.text {
  font-size: 14px;
}
</style>
```

是不是也非常简单？可能刚开始不太习惯，但写多几次其实也蛮好玩的这个功能！

**另外，需要注意的是，如果你是指定了 modules 的名称，那么必须传入对应的名称作为入参才可以正确拿到这些样式：**

比如指定了一个 classes 作为名称：

```vue
<style module="classes">
/* ... */
</style>
```

那么需要通过传入 classes 这个名称才能拿到样式，否则会是一个空对象：

```ts
const style = useCssModule('classes')
```

### 深度操作符

在 [样式表的组件作用域](#样式表的组件作用域) 部分我们了解到，使用 scoped 后，父组件的样式将不会渗透到子组件中，但也不能直接修改子组件的样式。

如果确实需要进行修改子组件的样式，必须通过 `::v-deep`（完整写法） 或者 `:deep`（快捷写法） 操作符来实现。

1. 旧版的深度操作符是 `>>>` 、 `/deep/` 和 `::v-deep`，现在 `>>>` 和 `/deep/` 已进入弃用阶段（虽然暂时还没完全移除）
2. 同时需要注意的是，旧版 `::v-deep` 的写法是作为组合器的方式，写在样式或者元素前面，如：`::v-deep .class-name { /* ... */ }`，现在这种写法也废弃了。
:::

现在不论是 `::v-deep` 还是 `:deep` ，使用方法非常统一，我们来假设 `.b` 是子组件的样式名：

```vue
<style scoped>
.a :deep(.b) {
  /* ... */
}
</style>
```

编译后：

```css
.a[data-v-f3f3eg9] .b {
  /* ... */
}
```

同理，如果你使用 Less 或者 Stylus 这种支持嵌套写法的预处理器，也是可以这样去深度操作的：

```less
.a {
  :deep(.b) {
    /* ... */
  }
}
```

另外，除了操作子组件的样式，那些通过 `v-html` 创建的 DOM 内容，也不受作用域内的样式影响，也可以通过深度操作符来实现样式修改。

# 高效开发

## script-setup

这是一个比较有争议的新特性，作为 setup 函数的语法糖，褒贬不一，不过经历了几次迭代之后，目前在体验上来说，感受还是非常棒的。

### 新特性的产生背景

在了解它怎么用之前，可以先了解一下它被推出的一些背景，可以帮助你对比开发体验上的异同点，以及了解为什么会有这一章节里面的新东西。

在 Vue 3.0 的 .vue 组件里，遵循 SFC 规范要求（注：SFC，即 Single-File Component，.vue 单组件），标准的 setup 用法是，在 setup 里面定义的数据如果需要在 template 使用，都需要 return 出来。

如果你使用的是 TypeScript ，还需要借助 [defineComponent](component.md#了解-definecomponent) 来帮助你对类型的自动推导。

```vue
<!-- 标准组件格式 -->
<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    // ...

    return {
      // ...
    }
  }
})
</script>
```

关于标准 setup 和 defineComponent 的说明和用法，可以查阅 [全新的 setup 函数](component.md#全新的-setup-函数-new) 一节。

script-setup 的推出是为了让熟悉 3.0 的用户可以更高效率的开发组件，减少一些心智负担，只需要给 script 标签添加一个 setup 属性，那么整个 script 就直接会变成 setup 函数，所有顶级变量、函数，均会自动暴露给模板使用（无需再一个个 return 了）。

Vue 会通过单组件编译器，在编译的时候将其处理回标准组件，所以目前这个方案只适合用 .vue 文件写的工程化项目。

```vue
<!-- 使用 script-setup 格式 -->
<script setup lang="ts">
  // ...
</script>
```

对，就是这样，代码量瞬间大幅度减少……

:::tip
因为 script-setup 的大部分功能在书写上和标准版是一致的，这里只提及一些差异化的表现。
:::

### 全局编译器宏

在 script-setup 模式下，新增了 4 个全局编译器宏，他们无需 import 就可以直接使用。

但是默认的情况下直接使用，项目的 eslint 会提示你没有导入，但你导入后，控制台的 Vue 编译助手又会提示你不需要导入，就很尴尬…

哈哈哈哈不过不用着急，可以配置一下 lint ，把这几个编译助手写进全局规则里，就可以了，不需要导入也不会报错了。

```js
// 项目根目录下的 .eslintrc.js
module.exports = {
  // 原来的lint规则，补充下面的globals...
  globals: {
    defineProps: 'readonly',
    defineEmits: 'readonly',
    defineExpose: 'readonly',
    withDefaults: 'readonly',
  },
}
```

关于几个宏的说明都在下面的文档部分有说明，你也可以从这里导航过去直接查看。

宏|说明
:-:|:-:
defineProps|[点击查看](#defineprops-的基础用法)
defineEmits|[点击查看](#defineemits-的基础用法)
defineExpose|[点击查看](#defineexpose-的基础用法)
withDefaults|[点击查看](#withdefaults-的基础用法)

下面我们继续了解 script-setup 的变化。

### template 操作简化

如果使用 JSX / TSX 写法，这一点没有太大影响，但对于习惯使用 `<template />` 的开发者来说，这是一个非常爽的体验。

主要体现在这两点：

#### 变量无需进行 return

标准组件模式下，setup 里定义的变量，需要 return 后，在 template 部分才可以正确拿到：

```vue
<!-- 标准组件格式 -->
<template>
  <p>{{ msg }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  setup () {
    const msg: string = 'Hello World!';
    
    // 要给 template 用的数据需要 return 出来才可以
    return {
      msg
    }
  }
})
</script>
```

在 script-setup 模式下，你定义了就可以直接使用。

```vue
<!-- 使用 script-setup 格式 -->
<template>
  <p>{{ msg }}</p>
</template>

<script setup lang="ts">
const msg: string = 'Hello World!';
</script>
```

#### 子组件无需手动注册

子组件的挂载，在标准组件里的写法是需要 import 后再放到 components 里才能够启用：

```vue
<!-- 标准组件格式 -->
<template>
  <Child />
</template>

<script lang="ts">
import { defineComponent } from 'vue'

// 导入子组件
import Child from '@cp/Child.vue'

export default defineComponent({
  // 需要启用子组件作为模板
  components: {
    Child
  },

  // 组件里的业务代码
  setup () {
    // ...
  }
})
</script>
```

在 script-setup 模式下，只需要导入组件即可，编译器会自动识别并启用。

```vue
<!-- 使用 script-setup 格式 -->
<template>
  <Child />
</template>

<script setup lang="ts">
import Child from '@cp/Child.vue'
</script>
```

### props 的接收方式变化

由于整个 script 都变成了一个大的 setup function ，没有了组件选项，也没有了 setup 入参，所以没办法和标准写法一样去接收 props 了。

这里需要使用一个全新的 API ：`defineProps` 。

`defineProps` 是一个方法，内部返回一个对象，也就是挂载到这个组件上的所有 props ，它和普通的 props 用法一样，如果不指定为 prop， 则传下来的属性会被放到 attrs 那边去。

:::tip
前置知识点：[接收 props - 组件之间的通信](communication.md#接收-props)。
:::

#### defineProps 的基础用法

所以，如果只是单纯在 template 里使用，那么其实就这么简单定义就可以了：

```ts
defineProps([
  'name',
  'userInfo',
  'tags'
])
```

使用 `string[]` 数组作为入参，把 prop 的名称作为数组的 item 传给 `defineProps` 就可以了。

如果 script 里的方法要拿到 props 的值，你也可以使用字面量定义：

```ts
const props = defineProps([
  'name',
  'userInfo',
  'tags'
])

console.log(props.name);
```

但在作为一个 Vue 老玩家，都清楚不显性的指定 prop 类型的话，很容易在协作中引起程序报错，那么应该如何对每个 prop 进行类型检查呢？

有两种方式来处理类型定义。

#### 通过构造函数检查 prop

这是第一种方式：使用 JavaScript 原生构造函数进行类型规定。

也就是跟我们平时定义 prop 类型时一样， Vue 会通过 `instanceof` 来进行 [类型检查](https://v3.cn.vuejs.org/guide/component-props.html#%E7%B1%BB%E5%9E%8B%E6%A3%80%E6%9F%A5) 。

使用这种方法，需要通过一个 “对象” 入参来传递给 `defineProps` ，比如：

```ts
defineProps({
  name: String,
  userInfo: Object,
  tags: Array
});
```

所有原来 props 具备的校验机制，都可以适用，比如你除了要限制类型外，还想指定 `name` 是可选，并且带有一个默认值：

```ts
defineProps({
  name: {
    type: String,
    required: false,
    default: 'Petter'
  },
  userInfo: Object,
  tags: Array
});
```

更多的 props 校验机制，可以点击 [带有类型限制的 props](communication.md#%E5%B8%A6%E6%9C%89%E7%B1%BB%E5%9E%8B%E9%99%90%E5%88%B6%E7%9A%84-props) 和 [可选以及带有默认值的 props](communication.md#%E5%8F%AF%E9%80%89%E4%BB%A5%E5%8F%8A%E5%B8%A6%E6%9C%89%E9%BB%98%E8%AE%A4%E5%80%BC%E7%9A%84-props) 了解更多。

#### 使用类型注解检查 prop

这是第二种方式：使用 TypeScript 的类型注解。

和 ref 等 API 的用法一样，`defineProps` 也是可以使用尖括号 <> 来包裹类型定义，紧跟在 API 后面，另外，由于 `defineProps` 返回的是一个对象（因为 props 本身是一个对象），所以尖括号里面的类型还要用大括号包裹，通过 `key: value` 的键值对形式表示，如：

```ts
defineProps<{ name: string }>();
```

注意到了吗？这里使用的类型，和第一种方法提到的指定类型时是不一样的。

:::tip
在这里，不再使用构造函数校验，而是需要遵循使用 TypeScript 的类型。

比如字符串是 `string`，而不是 `String` 。
:::

如果有多个 prop ，就跟写 interface 一样：

```ts
defineProps<{
  name: string;
  phoneNumber: number;
  userInfo: object;
  tags: string[];
}>();
```

其中，举例里的 `userInfo` 是一个对象，你可以简单的指定为 object，也可以先定义好它对应的类型，再进行指定：

```ts
interface UserInfo {
  id: number;
  age: number;
}

defineProps<{
  name: string;
  userInfo: UserInfo;
}>();
```

如果你想对某个数据设置为可选，也是遵循 TS 规范，通过英文问号 `?` 来允许可选：

```ts
// name 是可选
defineProps<{
  name?: string;
  tags: string[];
}>();
```

如果你想设置可选参数的默认值，需要借助 [withDefaults](#withdefaults-的基础用法) API。

:::warning
需要强调的一点是：在 [构造函数](#通过构造函数检查-prop) 和 [类型注解](#使用类型注解检查-prop) 这两种校验方式只能二选一，不能同时使用，否则会引起程序报错
:::

#### withDefaults 的基础用法

这个新的 withDefaults API 可以让你在使用 TS 类型系统时，也可以指定 props 的默认值。

它接收两个入参：

参数|类型|含义
:--|:--|:--
props|object|通过 defineProps 传入的 props
defaultValues|object|根据 props 的 key 传入默认值

可能缺乏一些官方描述，还是看参考用法可能更直观：

```ts
withDefaults(defineProps<{
  size?: number
  labels?: string[]
}>(), {
  size: 3,
  labels: () => ['default label']
})
```

如果你要在 TS / JS 再对 props 进行获取，也可以通过字面量来拿到这些默认值：

```ts
// 如果不习惯上面的写法，你也可以跟平时一样先通过interface定义一个类型接口
interface Props {
  msg?: string
}

// 再作为入参传入
const props = withDefaults(defineProps<Props>(), {
  msg: 'hello'
})

// 这样就可以通过props变量拿到需要的prop值了
console.log(props.msg)
```

### emits 的接收方式变化

和 props 一样，emits 的接收也是需要使用一个全新的 API 来操作，这个 API 就是 `defineEmits` 。

和 `defineProps` 一样， `defineEmits` 也是一个方法，它接受的入参格式和标准组件的要求是一致的。

:::tip
注意：从 `3.1.3` 版本开始，该 API 已被改名，加上了复数结尾，带有 s，在此版本之前是没有 s 结尾！

前置知识点：[接收 emits - 组件之间的通信](communication.md#接收-emits)。
:::

#### defineEmits 的基础用法

由于 emit 并非提供给模板直接读取，所以需要通过字面量来定义 emits。

最基础的用法也是传递一个 `string[]` 数组进来，把每个 emit 的名称作为数组的 item 。

```ts
// 获取 emit
const emit = defineEmits(['chang-name']);

// 调用 emit
emit('chang-name', 'Tom');
```

由于 `defineEmits` 的用法和原来的 emits 选项差别不大，这里也不重复说明更多的诸如校验之类的用法了，可以查看 [接收 emits](communication.md#接收-emits) 一节了解更多。

### attrs 的接收方式变化

`attrs` 和 `props` 很相似，也是基于父子通信的数据，如果父组件绑定下来的数据没有被指定为 `props` ，那么就会被挂到 `attrs` 这边来。

在标准组件里， `attrs` 的数据是通过 `setup` 的第二个入参 `context` 里的 `attrs` API 获取的。

```ts
// 标准组件的写法
export default defineComponent({
  setup (props, { attrs }) {
    // attrs 是个对象，每个 Attribute 都是它的 key
    console.log(attrs.class);

    // 如果传下来的 Attribute 带有短横线，需要通过这种方式获取
    console.log(attrs['data-hash']);
  }
})
```

但和 `props` 一样，由于没有了 `context` 参数，需要使用一个新的 API 来拿到 `attrs` 数据。

这个 API 就是 `useAttrs` 。

:::tip
请注意，`useAttrs` API 需要 Vue `3.1.4` 或更高版本才可以使用。
:::

#### useAttrs 的基础用法

顾名思义， useAttrs 可以是用来获取 attrs 数据的，它的用法非常简单：

```ts
// 导入 useAttrs 组件
import { useAttrs } from 'vue'

// 获取 attrs
const attrs = useAttrs()

// attrs是个对象，和 props 一样，需要通过 key 来得到对应的单个 attr
console.log(attrs.msg);
```

对 `attrs` 不太了解的话，可以查阅 [获取非 Prop 的 Attribute](communication.md#%E8%8E%B7%E5%8F%96%E9%9D%9E-prop-%E7%9A%84-attribute-new)

### slots 的接收方式变化

`slots` 是 Vue 组件的插槽数据，也是在父子通信里的一个重要成员。

对于使用 template 的开发者来说，在 script-setup 里获取插槽数据并不困难，因为跟标准组件的写法是完全一样的，可以直接在 template 里使用 `<slot />` 标签渲染。

```vue
<template>
  <div>
    <!-- 插槽数据 -->
    <slot />
    <!-- 插槽数据 -->
  </div>
</template>
```

但对使用 JSX / TSX 的开发者来说，就影响比较大了，在标准组件里，想在 script 里获取插槽数据，也是需要在 `setup` 的第二个入参里拿到 `slots` API 。

```ts
// 标准组件的写法
export default defineComponent({
  // 这里的 slots 就是插槽
  setup (props, { slots }) {
    // ...
  }
})
```

新版本的 Vue 也提供了一个全新的 `useSlots` API 来帮助 script-setup 用户获取插槽。

:::tip
请注意，`useSlots` API 需要 Vue `3.1.4` 或更高版本才可以使用。
:::

#### useSlots 的基础用法

先来看看父组件，父组件先为子组件传入插槽数据，支持 “默认插槽” 和 “命名插槽” ：

```vue
<template>
  <!-- 子组件 -->
  <ChildTSX>
    <!-- 默认插槽 -->
    <p>I am a default slot from TSX.</p>
    <!-- 默认插槽 -->

    <!-- 命名插槽 -->
    <template #msg>
      <p>I am a msg slot from TSX.</p>
    </template>
    <!-- 命名插槽 -->
  </ChildTSX>
  <!-- 子组件 -->
</template>

<script setup lang="ts">
import ChildTSX from '@cp/context/Child.tsx'
</script>
```

在使用 JSX / TSX 编写的子组件里，就可以通过 `useSlots` 来获取父组件传进来的 `slots` 数据进行渲染：

```tsx
// 注意：这是一个 .tsx 文件
import { defineComponent, useSlots } from 'vue'

const ChildTSX = defineComponent({
  setup() {
    // 获取插槽数据
    const slots = useSlots()

    // 渲染组件
    return () => (
      <div>
        {/* 渲染默认插槽 */}
        <p>{ slots.default ? slots.default() : '' }</p>

        {/* 渲染命名插槽 */}
        <p>{ slots.msg ? slots.msg() : '' }</p>
      </div>
    )
  },
})

export default ChildTSX
```

### ref 的通信方式变化

在标准组件写法里，子组件的数据都是默认隐式暴露给父组件的，也就是父组件可以通过 `childComponent.value.foo` 这样的方式直接操作子组件的数据（参见：[DOM 元素与子组件 - 响应式 API 之 ref](component.md#dom-元素与子组件)）。

但在 script-setup 模式下，所有数据只是默认隐式 return 给 template 使用，不会暴露到组件外，所以父组件是无法直接通过挂载 ref 变量获取子组件的数据。

在 script-setup 模式下，如果要调用子组件的数据，需要先在子组件显示的暴露出来，才能够正确的拿到，这个操作，就是由 `defineExpose` 来完成。

#### defineExpose 的基础用法

`defineExpose` 的用法非常简单，它本身是一个函数，可以接受一个对象参数。

在子组件里，像这样把需要暴露出去的数据通过 `key: value` 的形式作为入参（下面的例子是用到了 ES6 的 [属性的简洁表示法](https://es6.ruanyifeng.com/#docs/object#%E5%B1%9E%E6%80%A7%E7%9A%84%E7%AE%80%E6%B4%81%E8%A1%A8%E7%A4%BA%E6%B3%95)）：

```vue
<script setup lang="ts">
// 定义一个想提供给父组件拿到的数据
const msg: string = 'Hello World!';

// 显示暴露的数据，才可以在父组件拿到
defineExpose({
  msg
});
</script>
```

然后你在父组件就可以通过挂载在子组件上的 ref 变量，去拿到暴露出来的数据了。

### 顶级 await 的支持

在 script-setup 模式下，不必再配合 async 就可以直接使用 await 了，这种情况下，组件的 setup 会自动变成 async setup 。

```vue
<script setup lang="ts">
const post = await fetch(`/api/post/1`).then((r) => r.json())
</script>
```

它转换成标准组件的写法就是：

```vue
<script lang="ts">
import { defineComponent, withAsyncContext } from 'vue'

export default defineComponent({
  async setup() {
    const post = await withAsyncContext(
      fetch(`/api/post/1`).then((r) => r.json())
    )

    return {
      post
    }
  }
})
</script>
```