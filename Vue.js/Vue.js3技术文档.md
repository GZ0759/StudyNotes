# 组合式 API

## 介绍

### 什么是组合式 API？

通过创建 Vue 组件，我们可以将界面中重复的部分连同其功能一起提取为可重用的代码段。仅此一项就可以使我们的应用在可维护性和灵活性方面走得相当远。然而，我们的经验已经证明，光靠这一点可能并不够，尤其是当你的应用变得非常大的时候——想想几百个组件。处理这样的大型应用时，共享和重用代码变得尤为重要。

假设我们的应用中有一个显示某个用户的仓库列表的视图。此外，我们还希望有搜索和筛选功能。实现此视图组件的代码可能如下所示：

```js
// src/components/UserRepositories.vue

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      repositories: [], // 1
      filters: { ... }, // 3
      searchQuery: '' // 2
    }
  },
  computed: {
    filteredRepositories () { ... }, // 3
    repositoriesMatchingSearchQuery () { ... }, // 2
  },
  watch: {
    user: 'getUserRepositories' // 1
  },
  methods: {
    getUserRepositories () {
      // 使用 `this.user` 获取用户仓库
    }, // 1
    updateFilters () { ... }, // 3
  },
  mounted () {
    this.getUserRepositories() // 1
  }
}
```

该组件有以下几个职责：

1. 从假定的外部 API 获取该用户的仓库，并在用户有任何更改时进行刷新
2. 使用 searchQuery 字符串搜索仓库
3. 使用 filters 对象筛选仓库

使用 (data、computed、methods、watch) 组件选项来组织逻辑通常都很有效。然而，当我们的组件开始变得更大时，逻辑关注点的列表也会增长。尤其对于那些一开始没有编写这些组件的人来说，这会导致组件难以阅读和理解。

Vue 选项式 API: 按选项类型分组的代码

这是一个大型组件的示例，其中逻辑关注点按颜色进行分组。

这种碎片化使得理解和维护复杂组件变得困难。选项的分离掩盖了潜在的逻辑问题。此外，在处理单个逻辑关注点时，我们必须不断地“跳转”相关代码的选项块。

如果能够将同一个逻辑关注点相关代码收集在一起会更好。而这正是组合式 API 使我们能够做到的。

### 组合式 API 基础

既然我们知道了为什么，我们就可以知道怎么做。为了开始使用组合式 API，我们首先需要一个可以实际使用它的地方。在 Vue 组件中，我们将此位置称为 setup。

#### setup 组件选项

新的 setup 选项在组件创建之前执行，一旦 props 被解析，就将作为组合式 API 的入口。

WARNING

在 setup 中你应该避免使用 this，因为它不会找到组件实例。setup 的调用发生在 data property、computed property 或 methods 被解析之前，所以它们无法在 setup 中被获取。

setup 选项是一个接收 props 和 context 的函数，我们将在之后进行讨论。此外，我们将 setup 返回的所有内容都暴露给组件的其余部分 (计算属性、方法、生命周期钩子等等) 以及组件的模板。

让我们把 setup 添加到组件中：

```js
// src/components/UserRepositories.vue

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    console.log(props); // { user: '' }

    return {}; // 这里返回的任何内容都可以用于组件的其余部分
  },
  // 组件的“其余部分”
};
```

现在让我们从提取第一个逻辑关注点开始 (在原始代码段中标记为“1”)。

从假定的外部 API 获取该用户的仓库，并在用户有任何更改时进行刷新
我们将从最明显的部分开始：

- 仓库列表
- 更新仓库列表的函数
- 返回列表和函数，以便其他组件选项可以对它们进行访问

```js
// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'

// 在我们的组件内
setup (props) {
  let repositories = []
  const getUserRepositories = async () => {
    repositories = await fetchUserRepositories(props.user)
  }

  return {
    repositories,
    getUserRepositories // 返回的函数与方法的行为相同
  }
}
```

这是我们的出发点，但它还无法生效，因为 repositories 变量是非响应式的。这意味着从用户的角度来看，仓库列表将始终为空。让我们来解决这个问题！

#### 带 ref 的响应式变量

在 Vue 3.0 中，我们可以通过一个新的 ref 函数使任何响应式变量在任何地方起作用，如下所示：

```js
import { ref } from 'vue';

const counter = ref(0);
```

ref 接收参数并将其包裹在一个带有 value property 的对象中返回，然后可以使用该 property 访问或更改响应式变量的值：

```js
import { ref } from 'vue';

const counter = ref(0);

console.log(counter); // { value: 0 }
console.log(counter.value); // 0

counter.value++;
console.log(counter.value); // 1
```

将值封装在一个对象中，看似没有必要，但为了保持 JavaScript 中不同数据类型的行为统一，这是必须的。这是因为在 JavaScript 中，Number 或 String 等基本类型是通过值而非引用传递的：

在任何值周围都有一个封装对象，这样我们就可以在整个应用中安全地传递它，而不必担心在某个地方失去它的响应性。

提示

换句话说，ref 为我们的值创建了一个响应式引用。在整个组合式 API 中会经常使用引用的概念。

回到我们的例子，让我们创建一个响应式的 repositories 变量：

```js
// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'
import { ref } from 'vue'

// 在我们的组件中
setup (props) {
  const repositories = ref([])
  const getUserRepositories = async () => {
    repositories.value = await fetchUserRepositories(props.user)
  }

  return {
    repositories,
    getUserRepositories
  }
}
```

完成！现在，每当我们调用 getUserRepositories 时，repositories 都将发生变化，视图也会更新以反映变化。我们的组件现在应该如下所示：

```js
// src/components/UserRepositories.vue
import { fetchUserRepositories } from '@/api/repositories'
import { ref } from 'vue'

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true
    }
  },
  setup (props) {
    const repositories = ref([])
    const getUserRepositories = async () => {
      repositories.value = await fetchUserRepositories(props.user)
    }

    return {
      repositories,
      getUserRepositories
    }
  },
  data () {
    return {
      filters: { ... }, // 3
      searchQuery: '' // 2
    }
  },
  computed: {
    filteredRepositories () { ... }, // 3
    repositoriesMatchingSearchQuery () { ... }, // 2
  },
  watch: {
    user: 'getUserRepositories' // 1
  },
  methods: {
    updateFilters () { ... }, // 3
  },
  mounted () {
    this.getUserRepositories() // 1
  }
}
```

我们已经将第一个逻辑关注点中的几个部分移到了 setup 方法中，它们彼此非常接近。剩下的就是在 mounted 钩子中调用 getUserRepositories，并设置一个监听器，以便在 user prop 发生变化时执行此操作。

我们将从生命周期钩子开始。

#### 在 setup 内注册生命周期钩子

为了使组合式 API 的功能和选项式 API 一样完整，我们还需要一种在 setup 中注册生命周期钩子的方法。这要归功于 Vue 导出的几个新函数。组合式 API 上的生命周期钩子与选项式 API 的名称相同，但前缀为 on：即 mounted 看起来会像 onMounted。

这些函数接受一个回调，当钩子被组件调用时，该回调将被执行。

让我们将其添加到 setup 函数中：

```js
// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'
import { ref, onMounted } from 'vue'

// 在我们的组件中
setup (props) {
  const repositories = ref([])
  const getUserRepositories = async () => {
    repositories.value = await fetchUserRepositories(props.user)
  }

  onMounted(getUserRepositories) // 在 `mounted` 时调用 `getUserRepositories`

  return {
    repositories,
    getUserRepositories
  }
}
```

现在我们需要对 user prop 的变化做出反应。为此，我们将使用独立的 watch 函数。

#### watch 响应式更改

就像我们在组件中使用 watch 选项并在 user property 上设置侦听器一样，我们也可以使用从 Vue 导入的 watch 函数执行相同的操作。它接受 3 个参数：

- 一个想要侦听的响应式引用或 getter 函数
- 一个回调
- 可选的配置选项

下面让我们快速了解一下它是如何工作的

```js
import { ref, watch } from 'vue';

const counter = ref(0);
watch(counter, (newValue, oldValue) => {
  console.log('The new counter value is: ' + counter.value);
});
```

每当 counter 被修改时，例如 `counter.value=5`，侦听将触发并执行回调 (第二个参数)，在本例中，它将把 'The new counter value is:5' 记录到控制台中。

以下是等效的选项式 API：

```js
export default {
  data() {
    return {
      counter: 0,
    };
  },
  watch: {
    counter(newValue, oldValue) {
      console.log('The new counter value is: ' + this.counter);
    },
  },
};
```

有关 watch 的详细信息，请参阅我们的深入指南。

现在我们将其应用到我们的示例中：

```js
// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'
import { ref, onMounted, watch, toRefs } from 'vue'

// 在我们组件中
setup (props) {
  // 使用 `toRefs` 创建对 `props` 中的 `user` property 的响应式引用
  const { user } = toRefs(props)

  const repositories = ref([])
  const getUserRepositories = async () => {
    // 更新 `prop.user` 到 `user.value` 访问引用值
    repositories.value = await fetchUserRepositories(user.value)
  }

  onMounted(getUserRepositories)

  // 在 user prop 的响应式引用上设置一个侦听器
  watch(user, getUserRepositories)

  return {
    repositories,
    getUserRepositories
  }
}
```

你可能已经注意到在我们的 setup 的顶部使用了 toRefs。这是为了确保我们的侦听器能够根据 user prop 的变化做出反应。

有了这些变化，我们就把第一个逻辑关注点移到了一个地方。我们现在可以对第二个关注点执行相同的操作——基于 searchQuery 进行过滤，这次是使用计算属性。

#### 独立的 computed 属性

与 ref 和 watch 类似，也可以使用从 Vue 导入的 computed 函数在 Vue 组件外部创建计算属性。让我们回到 counter 的例子：

```js
import { ref, computed } from 'vue';

const counter = ref(0);
const twiceTheCounter = computed(() => counter.value * 2);

counter.value++;
console.log(counter.value); // 1
console.log(twiceTheCounter.value); // 2
```

这里我们给 computed 函数传递了第一个参数，它是一个类似 getter 的回调函数，输出的是一个只读的响应式引用。为了访问新创建的计算变量的 value，我们需要像 ref 一样使用 `.value property`。

让我们将搜索功能移到 setup 中：

```js
// src/components/UserRepositories.vue `setup` function
import { fetchUserRepositories } from '@/api/repositories'
import { ref, onMounted, watch, toRefs, computed } from 'vue'

// 在我们的组件中
setup (props) {
  // 使用 `toRefs` 创建对 props 中的 `user` property 的响应式引用
  const { user } = toRefs(props)

  const repositories = ref([])
  const getUserRepositories = async () => {
    // 更新 `props.user ` 到 `user.value` 访问引用值
    repositories.value = await fetchUserRepositories(user.value)
  }

  onMounted(getUserRepositories)

  // 在 user prop 的响应式引用上设置一个侦听器
  watch(user, getUserRepositories)

  const searchQuery = ref('')
  const repositoriesMatchingSearchQuery = computed(() => {
    return repositories.value.filter(
      repository => repository.name.includes(searchQuery.value)
    )
  })

  return {
    repositories,
    getUserRepositories,
    searchQuery,
    repositoriesMatchingSearchQuery
  }
}
```

对于其他的逻辑关注点我们也可以这样做，但是你可能已经在问这个问题了——这不就是把代码移到 setup 选项并使它变得非常大吗？嗯，确实是这样的。这就是为什么我们要在继续其他任务之前，我们首先要将上述代码提取到一个独立的组合式函数中。让我们从创建 useUserRepositories 函数开始：

```js
// src/composables/useUserRepositories.js

import { fetchUserRepositories } from '@/api/repositories';
import { ref, onMounted, watch } from 'vue';

export default function useUserRepositories(user) {
  const repositories = ref([]);
  const getUserRepositories = async () => {
    repositories.value = await fetchUserRepositories(user.value);
  };

  onMounted(getUserRepositories);
  watch(user, getUserRepositories);

  return {
    repositories,
    getUserRepositories,
  };
}
```

然后是搜索功能：

```js
// src/composables/useRepositoryNameSearch.js

import { ref, computed } from 'vue';

export default function useRepositoryNameSearch(repositories) {
  const searchQuery = ref('');
  const repositoriesMatchingSearchQuery = computed(() => {
    return repositories.value.filter((repository) => {
      return repository.name.includes(searchQuery.value);
    });
  });

  return {
    searchQuery,
    repositoriesMatchingSearchQuery,
  };
}
```

现在我们有了两个单独的功能模块，接下来就可以开始在组件中使用它们了。以下是如何做到这一点：

```js
// src/components/UserRepositories.vue
import useUserRepositories from '@/composables/useUserRepositories'
import useRepositoryNameSearch from '@/composables/useRepositoryNameSearch'
import { toRefs } from 'vue'

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true
    }
  },
  setup (props) {
    const { user } = toRefs(props)

    const { repositories, getUserRepositories } = useUserRepositories(user)

    const {
      searchQuery,
      repositoriesMatchingSearchQuery
    } = useRepositoryNameSearch(repositories)

    return {
      // 因为我们并不关心未经过滤的仓库
      // 我们可以在 `repositories` 名称下暴露过滤后的结果
      repositories: repositoriesMatchingSearchQuery,
      getUserRepositories,
      searchQuery,
    }
  },
  data () {
    return {
      filters: { ... }, // 3
    }
  },
  computed: {
    filteredRepositories () { ... }, // 3
  },
  methods: {
    updateFilters () { ... }, // 3
  }
}
```

此时，你可能已经知道了其中的奥妙，所以让我们跳到最后，迁移剩余的过滤功能。我们不需要深入了解实现细节，因为这并不是本指南的重点。

```js
// src/components/UserRepositories.vue
import { toRefs } from 'vue';
import useUserRepositories from '@/composables/useUserRepositories';
import useRepositoryNameSearch from '@/composables/useRepositoryNameSearch';
import useRepositoryFilters from '@/composables/useRepositoryFilters';

export default {
  components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
  props: {
    user: {
      type: String,
      required: true,
    },
  },
  setup(props) {
    const { user } = toRefs(props);

    const { repositories, getUserRepositories } = useUserRepositories(user);

    const { searchQuery, repositoriesMatchingSearchQuery } =
      useRepositoryNameSearch(repositories);

    const { filters, updateFilters, filteredRepositories } =
      useRepositoryFilters(repositoriesMatchingSearchQuery);

    return {
      // 因为我们并不关心未经过滤的仓库
      // 我们可以在 `repositories` 名称下暴露过滤后的结果
      repositories: filteredRepositories,
      getUserRepositories,
      searchQuery,
      filters,
      updateFilters,
    };
  },
};
```

我们完成了！

请记住，我们只触及了组合式 API 的表面以及它允许我们做什么。要了解更多信息，请参阅深入指南。

## Setup

本节使用单文件组件代码示例的语法

本指南假定你已经阅读了组合式 API 简介和响应性原理。如果你不熟悉组合式 API，请先阅读这两篇文章。

### 参数

使用 setup 函数时，它将接收两个参数：

- props
- context

让我们更深入地研究如何使用每个参数。

### Props

setup 函数中的第一个参数是 props。正如在一个标准组件中所期望的那样，setup 函数中的 props 是响应式的，当传入新的 prop 时，它将被更新。

```js
// MyBook.vue

export default {
  props: {
    title: String,
  },
  setup(props) {
    console.log(props.title);
  },
};
```

WARNING

但是，因为 props 是响应式的，你不能使用 ES6 解构，它会消除 prop 的响应性。

如果需要解构 prop，可以在 setup 函数中使用 toRefs 函数来完成此操作：

```js
// MyBook.vue

import { toRefs } from 'vue'

setup(props) {
  const { title } = toRefs(props)

  console.log(title.value)
}
```

如果 title 是可选的 prop，则传入的 props 中可能没有 title 。在这种情况下，toRefs 将不会为 title 创建一个 ref 。你需要使用 toRef 替代它：

```js
// MyBook.vue
import { toRef } from 'vue'
setup(props) {
  const title = toRef(props, 'title')
  console.log(title.value)
}
```

### Context

传递给 setup 函数的第二个参数是 context。context 是一个普通 JavaScript 对象，暴露了其它可能在 setup 中有用的值：

```js
// MyBook.vue

export default {
  setup(props, context) {
    // Attribute (非响应式对象，等同于 $attrs)
    console.log(context.attrs);

    // 插槽 (非响应式对象，等同于 $slots)
    console.log(context.slots);

    // 触发事件 (方法，等同于 $emit)
    console.log(context.emit);

    // 暴露公共 property (函数)
    console.log(context.expose);
  },
};
```

context 是一个普通的 JavaScript 对象，也就是说，它不是响应式的，这意味着你可以安全地对 context 使用 ES6 解构。

```js
// MyBook.vue
export default {
  setup(props, { attrs, slots, emit, expose }) {
    ...
  }
}
```

attrs 和 slots 是有状态的对象，它们总是会随组件本身的更新而更新。这意味着你应该避免对它们进行解构，并始终以 `attrs.x` 或 `slots.x` 的方式引用 property。请注意，与 props 不同，attrs 和 slots 的 property 是非响应式的。如果你打算根据 attrs 或 slots 的更改应用副作用，那么应该在 onBeforeUpdate 生命周期钩子中执行此操作。

我们将在稍后解释 expose 所扮演的角色。

### 访问组件的 property

执行 setup 时，你只能访问以下 property：

- props
- attrs
- slots
- emit

换句话说，你将无法访问以下组件选项：

- data
- computed
- methods
- refs (模板 ref)

### 结合模板使用

如果 setup 返回一个对象，那么该对象的 property 以及传递给 setup 的 props 参数中的 property 就都可以在模板中访问到：

```html
<!-- MyBook.vue -->
<template>
  <div>{{ collectionName }}: {{ readersNumber }} {{ book.title }}</div>
</template>

<script>
  import { ref, reactive } from 'vue';

  export default {
    props: {
      collectionName: String,
    },
    setup(props) {
      const readersNumber = ref(0);
      const book = reactive({ title: 'Vue 3 Guide' });

      // 暴露给 template
      return {
        readersNumber,
        book,
      };
    },
  };
</script>
```

注意，从 setup 返回的 refs 在模板中访问时是被自动浅解包的，因此不应在模板中使用 `.value`。

### 使用渲染函数

setup 还可以返回一个渲染函数，该函数可以直接使用在同一作用域中声明的响应式状态：

```js
// MyBook.vue

import { h, ref, reactive } from 'vue';

export default {
  setup() {
    const readersNumber = ref(0);
    const book = reactive({ title: 'Vue 3 Guide' });
    // 请注意这里我们需要显式使用 ref 的 value
    return () => h('div', [readersNumber.value, book.title]);
  },
};
```

返回一个渲染函数将阻止我们返回任何其它的东西。从内部来说这不应该成为一个问题，但当我们想要将这个组件的方法通过模板 ref 暴露给父组件时就不一样了。

我们可以通过调用 expose 来解决这个问题，给它传递一个对象，其中定义的 property 将可以被外部组件实例访问：

```js
import { h, ref } from 'vue';
export default {
  setup(props, { expose }) {
    const count = ref(0);
    const increment = () => ++count.value;

    expose({
      increment,
    });

    return () => h('div', count.value);
  },
};
```

这个 increment 方法现在将可以通过父组件的模板 ref 访问。

### 使用 this

在 `setup()` 内部，this 不是该活跃实例的引用，因为 `setup()` 是在解析其它组件选项之前被调用的，所以 `setup()` 内部的 this 的行为与其它选项中的 this 完全不同。这使得 `setup()` 在和其它选项式 API 一起使用时可能会导致混淆。

# 响应性

## 深入响应性原理

现在是时候深入了！Vue 最独特的特性之一，是其非侵入性的响应性系统。数据模型是被代理的 JavaScript 对象。而当你修改它们时，视图会进行更新。这让状态管理非常简单直观，不过理解其工作原理同样重要，这样你可以避开一些常见的问题。在这个章节，我们将研究一下 Vue 响应性系统的底层的细节。

### 什么是响应性

这个术语在程序设计中经常被提及，但这是什么意思呢？响应性是一种允许我们以声明式的方式去适应变化的编程范例。人们通常展示的典型例子，是一份 excel 电子表格 (一个非常好的例子)。

如果将数字 2 放在第一个单元格中，将数字 3 放在第二个单元格中并要求提供 SUM，则电子表格会将其计算出来给你。不要惊奇，同时，如果你更新第一个数字，SUM 也会自动更新。

JavaScript 通常不是这样工作的——如果我们想用 JavaScript 编写类似的内容：

```js
let val1 = 2;
let val2 = 3;
let sum = val1 + val2;

console.log(sum); // 5

val1 = 3;

console.log(sum); // 仍然是 5
```

如果我们更新第一个值，sum 不会被修改。

那么我们如何用 JavaScript 实现这一点呢？

作为一个高阶的概述，我们需要做到以下几点：

1. 当一个值被读取时进行追踪，例如 val1 + val2 会同时读取 val1 和 val2。
2. 当某个值改变时进行检测，例如，当我们赋值 val1 = 3。
3. 重新运行代码来读取原始值，例如，再次运行 sum = val1 + val2 来更新 sum 的值。

我们不能直接用前面的例子中的代码来继续，但是我们后面会再来看看这个例子，以及如何调整它来兼容 Vue 的响应性系统。

首先，让我们深入了解一下 Vue 是如何实现上述核心响应性要求的。

### Vue 如何知道哪些代码在执行

为了能够在数值变化时，随时运行我们的总和，我们首先要做的是将其包裹在一个函数中。

```js
const updateSum = () => {
  sum = val1 + val2;
};
```

但我们如何告知 Vue 这个函数呢？

Vue 通过一个副作用 (effect) 来跟踪当前正在运行的函数。副作用是一个函数的包裹器，在函数被调用之前就启动跟踪。Vue 知道哪个副作用在何时运行，并能在需要时再次执行它。

为了更好地理解这一点，让我们尝试脱离 Vue 实现类似的东西，以看看它如何工作。

我们需要的是能够包裹总和的东西，像这样：

```js
createEffect(() => {
  sum = val1 + val2;
});
```

我们需要 createEffect 来跟踪和执行。我们的实现如下：

```js
// 维持一个执行副作用的栈
const runningEffects = [];

const createEffect = (fn) => {
  // 将传来的 fn 包裹在一个副作用函数中
  const effect = () => {
    runningEffects.push(effect);
    fn();
    runningEffects.pop();
  };

  // 立即自动执行副作用
  effect();
};
```

当我们的副作用被调用时，在调用 fn 之前，它会把自己推到 runningEffects 数组中。这个数组可以用来检查当前正在运行的副作用。

副作用是许多关键功能的起点。例如，组件的渲染和计算属性都在内部使用副作用。任何时候，只要有东西对数据变化做出奇妙的回应，你就可以肯定它已经被包裹在一个副作用中了。

虽然 Vue 的公开 API 不包括任何直接创建副作用的方法，但它确实暴露了一个叫做 watchEffect 的函数，它的行为很像我们例子中的 createEffect 函数。我们会在该指南后面的部分详细讨论这个问题。

但知道什么代码在执行只是难题的一部分。Vue 如何知道副作用使用了什么值，以及如何知道它们何时发生变化？

### Vue 如何跟踪变化

我们不能像前面的例子中那样跟踪局部变量的重新分配，在 JavaScript 中没有这样的机制。我们可以跟踪的是对象 property 的变化。

当我们从一个组件的 data 函数中返回一个普通的 JavaScript 对象时，Vue 会将该对象包裹在一个带有 get 和 set 处理程序的 Proxy 中。Proxy 是在 ES6 中引入的，它使 Vue 3 避免了 Vue 早期版本中存在的一些响应性问题。

那看起来灵敏，不过，需要一些 Proxy 的知识才能理解！所以让我们深入了解一下。有很多关于 Proxy 的文档，但你真正需要知道的是，Proxy 是一个对象，它包装了另一个对象，并允许你拦截对该对象的任何交互。

我们这样使用它：new Proxy(target, handler)

```js
const dinner = {
  meal: 'tacos',
};

const handler = {
  get(target, property) {
    console.log('intercepted!');
    return target[property];
  },
};

const proxy = new Proxy(dinner, handler);
console.log(proxy.meal);

// intercepted!
// tacos
```

这里我们截获了读取目标对象 property 的举动。像这样的处理函数也称为一个捕捉器 (trap)。有许多可用的不同类型的捕捉器，每个都处理不同类型的交互。

除了控制台日志，我们可以在这里做任何我们想做的事情。如果我们愿意，我们甚至可以不返回实际值。这就是为什么 Proxy 对于创建 API 如此强大。

使用 Proxy 的一个难点是 this 绑定。我们希望任何方法都绑定到这个 Proxy，而不是目标对象，这样我们也可以拦截它们。值得庆幸的是，ES6 引入了另一个名为 Reflect 的新特性，它允许我们以最小的代价消除了这个问题：

```js
const dinner = {
  meal: 'tacos',
};

const handler = {
  get(target, property, receiver) {
    return Reflect.get(...arguments);
  },
};

const proxy = new Proxy(dinner, handler);
console.log(proxy.meal);

// tacos
```

使用 Proxy 实现响应性的第一步就是跟踪一个 property 何时被读取。我们在一个名为 track 的处理器函数中执行此操作，该函数可以传入 target 和 property 两个参数。

```js
const dinner = {
  meal: 'tacos',
};

const handler = {
  get(target, property, receiver) {
    track(target, property);
    return Reflect.get(...arguments);
  },
};

const proxy = new Proxy(dinner, handler);
console.log(proxy.meal);

// tacos
```

这里没有展示 track 的实现。它将检查当前运行的是哪个副作用，并将其与 target 和 property 记录在一起。这就是 Vue 如何知道这个 property 是该副作用的依赖项。

最后，我们需要在 property 值更改时重新运行这个副作用。为此，我们需要在代理上使用一个 set 处理函数：

```js
const dinner = {
  meal: 'tacos',
};

const handler = {
  get(target, property, receiver) {
    track(target, property);
    return Reflect.get(...arguments);
  },
  set(target, property, value, receiver) {
    trigger(target, property);
    return Reflect.set(...arguments);
  },
};

const proxy = new Proxy(dinner, handler);
console.log(proxy.meal);

// tacos
```

还记得前面的表格吗？现在，我们对 Vue 如何实现这些关键步骤有了答案：

1. 当一个值被读取时进行追踪：proxy 的 get 处理函数中 track 函数记录了该 property 和当前副作用。
2. 当某个值改变时进行检测：在 proxy 上调用 set 处理函数。
3. 重新运行代码来读取原始值：trigger 函数查找哪些副作用依赖于该 property 并执行它们。

该被代理的对象对于用户来说是不可见的，但是在内部，它们使 Vue 能够在 property 的值被访问或修改的情况下进行依赖跟踪和变更通知。有一点需要注意，控制台日志会以不同的方式对 proxy 对象进行格式化，因此你可能需要安装 vue-devtools，以提供一种更易于检查的界面。

如果我们要用一个组件重写我们原来的例子，我们可以这样做：

```js
const vm = createApp({
  data() {
    return {
      val1: 2,
      val2: 3,
    };
  },
  computed: {
    sum() {
      return this.val1 + this.val2;
    },
  },
}).mount('#app');

console.log(vm.sum); // 5

vm.val1 = 3;

console.log(vm.sum); // 6
```

data 返回的对象将被包裹在响应式代理中，并存储为 `this.$data`。Property this.val1 和 this.val2 分别是 `this.$data`.val1 和 `this.$data`.val2 的别名，因此它们通过相同的代理。

Vue 将把 sum 的函数包裹在一个副作用中。当我们试图访问 this.sum 时，它将运行该副作用来计算数值。包裹 `$data` 的响应式代理将会追踪到，当副作用运行时，property val1 和 val2 被读取了。

从 Vue 3 开始，我们的响应性现在可以在一个独立包中使用。将 `$data` 包裹在一个代理中的函数被称为 reactive。我们可以自己直接调用这个函数，允许我们在不需要使用组件的情况下将一个对象包裹在一个响应式代理中。

```js
const proxy = reactive({
  val1: 2,
  val2: 3,
});
```

在指南接下来的几页中，我们将探索响应性包所暴露的功能。这包括我们已经见过的 reactive 和 watchEffect 等函数，以及使用其他响应性特性的方法，如不需要创建组件的 computed 和 watch。

### 被代理的对象

Vue 在内部跟踪所有已经被转成响应式的对象，所以它总是为同一个对象返回相同的代理。

当从一个响应式代理中访问一个嵌套对象时，该对象在被返回之前也被转换为一个代理：

```js
const handler = {
  get(target, property, receiver) {
    track(target, property);
    const value = Reflect.get(...arguments);
    if (isObject(value)) {
      // 将嵌套对象包裹在自己的响应式代理中
      return reactive(value);
    } else {
      return value;
    }
  },
  // ...
};
```

### Proxy vs 原始标识

Proxy 的使用确实引入了一个需要注意的新警告：在身份比较方面，被代理对象与原始对象不相等 (===)。例如：

```js
const obj = {};
const wrapped = new Proxy(obj, handlers);

console.log(obj === wrapped); // false
```

其他依赖严格等于比较的操作也会受到影响，例如 .includes() 或 .indexOf()。

这里的最佳实践是永远不要持有对原始对象的引用，而只使用响应式版本。

```js
const obj = reactive({
  count: 0,
}); // 未引用原始
```

这确保了等值的比较和响应性的行为都符合预期。

请注意，Vue 不会在 Proxy 中包裹数字或字符串等原始值，所以你仍然可以对这些值直接使用 === 来比较：

```js
const obj = reactive({
  count: 0,
});

console.log(obj.count === 0); // true
```

### 如何让渲染响应变化

一个组件的模板被编译成一个 render 函数。渲染函数创建 VNodes，描述该组件应该如何被渲染。它被包裹在一个副作用中，允许 Vue 在运行时跟踪被“触达”的 property。

一个 render 函数在概念上与一个 computed property 非常相似。Vue 并不确切地追踪依赖关系是如何被使用的，它只知道在函数运行的某个时间点上使用了这些依赖关系。如果这些 property 中的任何一个随后发生了变化，它将触发副作用再次运行，重新运行 render 函数以生成新的 VNodes。然后这些举动被用来对 DOM 进行必要的修改。

## 响应性基础

### 声明响应式状态

要为 JavaScript 对象创建响应式状态，可以使用 reactive 方法：

```js
import { reactive } from 'vue';

// 响应式状态
const state = reactive({
  count: 0,
});
```

reactive 相当于 Vue 2.x 中的 Vue.observable() API，为避免与 RxJS 中的 observables 混淆因此对其重命名。该 API 返回一个响应式的对象状态。该响应式转换是“深度转换”——它会影响传递对象的所有嵌套 property。

Vue 中响应式状态的基本用例是我们可以在渲染期间使用它。因为依赖跟踪的关系，当响应式状态改变时视图会自动更新。

这就是 Vue 响应性系统的本质。当从组件中的 data() 返回一个对象时，它在内部交由 reactive() 使其成为响应式对象。模板会被编译成能够使用这些响应式 property 的渲染函数。

在响应性基础 API 章节你可以学习更多关于 reactive 的内容。

### 创建独立的响应式值作为 refs

想象一下，我们有一个独立的原始值 (例如，一个字符串)，我们想让它变成响应式的。当然，我们可以创建一个拥有相同字符串 property 的对象，并将其传递给 reactive。Vue 为我们提供了一个可以做相同事情的方法——ref：

```js
import { ref } from 'vue';

const count = ref(0);
```

ref 会返回一个可变的响应式对象，该对象作为一个响应式的引用维护着它内部的值，这就是 ref 名称的来源。该对象只包含一个名为 value 的 property：

```js
import { ref } from 'vue';

const count = ref(0);
console.log(count.value); // 0

count.value++;
console.log(count.value); // 1
```

### Ref 解包

当 ref 作为渲染上下文 (从 setup() 中返回的对象) 上的 property 返回并可以在模板中被访问时，它将自动浅层次解包内部值。只有访问嵌套的 ref 时需要在模板中添加 .value：

```html
<template>
  <div>
    <span>{{ count }}</span>
    <button @click="count ++">Increment count</button>
    <button @click="nested.count.value ++">Nested Increment count</button>
  </div>
</template>

<script>
  import { ref } from 'vue';
  export default {
    setup() {
      const count = ref(0);
      return {
        count,

        nested: {
          count,
        },
      };
    },
  };
</script>
```

TIP

如果你不想要访问实际的对象实例，可将其用 reactive 包裹:

```js
nested: reactive({
  count,
});
```

### 访问响应式对象

当 ref 作为响应式对象的 property 被访问或更改时，为使其行为类似于普通 property，它会自动解包内部值：

```js
const count = ref(0);
const state = reactive({
  count,
});

console.log(state.count); // 0

state.count = 1;
console.log(count.value); // 1
```

如果将新的 ref 赋值给现有 ref 的 property，将会替换旧的 ref：

```js
const otherCount = ref(2);

state.count = otherCount;
console.log(state.count); // 2
console.log(count.value); // 1
```

Ref 解包仅发生在被响应式 Object 嵌套的时候。当从 Array 或原生集合类型如 Map 访问 ref 时，不会进行解包：

```js
const books = reactive([ref('Vue 3 Guide')]);
// 这里需要 .value
console.log(books[0].value);

const map = reactive(new Map([['count', ref(0)]]));
// 这里需要 .value
console.log(map.get('count').value);
```

### 响应式状态解构

当我们想使用大型响应式对象的一些 property 时，可能很想使用 ES6 解构来获取我们想要的 property：

```js
import { reactive } from 'vue';

const book = reactive({
  author: 'Vue Team',
  year: '2020',
  title: 'Vue 3 Guide',
  description: 'You are reading this book right now ;)',
  price: 'free',
});

let { author, title } = book;
```

遗憾的是，使用解构的两个 property 的响应性都会丢失。对于这种情况，我们需要将我们的响应式对象转换为一组 ref。这些 ref 将保留与源对象的响应式关联：

```js
import { reactive, toRefs } from 'vue';

const book = reactive({
  author: 'Vue Team',
  year: '2020',
  title: 'Vue 3 Guide',
  description: 'You are reading this book right now ;)',
  price: 'free',
});

let { author, title } = toRefs(book);

title.value = 'Vue 3 Detailed Guide'; // 我们需要使用 .value 作为标题，现在是 ref
console.log(book.title); // 'Vue 3 Detailed Guide'
```

你可以在 Refs API 部分中了解更多有关 refs 的信息

### 使用 readonly 防止更改响应式对象

有时我们想跟踪响应式对象 (ref 或 reactive) 的变化，但我们也希望防止在应用程序的某个位置更改它。例如，当我们有一个被 provide 的响应式对象时，我们不想让它在注入之后被改变。为此，我们可以基于原始对象创建一个只读的 proxy 对象：

```js
import { reactive, readonly } from 'vue';

const original = reactive({ count: 0 });

const copy = readonly(original);

// 通过 original 修改 count，将会触发依赖 copy 的侦听器

original.count++;

// 通过 copy 修改 count，将导致失败并出现警告
copy.count++; // 警告: "Set operation on key 'count' failed: target is readonly."
```

## 响应式计算和侦听

### 计算值

有时我们需要依赖于其他状态的状态——在 Vue 中，这是用组件计算属性处理的，以直接创建计算值，我们可以使用 computed 函数：它接受 getter 函数并为 getter 返回的值返回一个不可变的响应式 ref 对象。

```js
const count = ref(1);
const plusOne = computed(() => count.value + 1);

console.log(plusOne.value); // 2

plusOne.value++; // error
```

或者，它可以使用一个带有 get 和 set 函数的对象来创建一个可写的 ref 对象。

```js
const count = ref(1);
const plusOne = computed({
  get: () => count.value + 1,
  set: (val) => {
    count.value = val - 1;
  },
});

plusOne.value = 1;
console.log(count.value); // 0
```

#### 调试 Computed

computed 可接受一个带有 onTrack 和 onTrigger 选项的对象作为第二个参数：

onTrack 会在某个响应式 property 或 ref 作为依赖被追踪时调用。
onTrigger 会在侦听回调被某个依赖的修改触发时调用。
所有回调都会收到一个 debugger 事件，其中包含了一些依赖相关的信息。推荐在这些回调内放置一个 debugger 语句以调试依赖。

```js
const plusOne = computed(() => count.value + 1, {
  onTrack(e) {
    // 当 count.value 作为依赖被追踪时触发
    debugger
  },
  onTrigger(e) {
    // 当 count.value 被修改时触发
    debugger
  }
})
// 访问 plusOne，应该触发 onTrack
console.log(plusOne.value)
// 修改 count.value，应该触发 onTrigger
count.value++
onTrack 和 onTrigger 仅在开发模式下生效。
```

### watchEffect

为了根据响应式状态自动应用和重新应用副作用，我们可以使用 watchEffect 函数。它立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。

```js
const count = ref(0);

watchEffect(() => console.log(count.value));
// -> logs 0

setTimeout(() => {
  count.value++;
  // -> logs 1
}, 100);
```

#### 停止侦听

当 watchEffect 在组件的 setup() 函数或生命周期钩子被调用时，侦听器会被链接到该组件的生命周期，并在组件卸载时自动停止。

在一些情况下，也可以显式调用返回值以停止侦听：

```js
const stop = watchEffect(() => {
  /* ... */
});

// later
stop();
```

#### 清除副作用

有时副作用函数会执行一些异步的副作用，这些响应需要在其失效时清除 (即完成之前状态已改变了) 。所以侦听副作用传入的函数可以接收一个 onInvalidate 函数作入参，用来注册清理失效时的回调。当以下情况发生时，这个失效回调会被触发：

副作用即将重新执行时
侦听器被停止 (如果在 setup() 或生命周期钩子函数中使用了 watchEffect，则在组件卸载时)

```js
watchEffect((onInvalidate) => {
  const token = performAsyncOperation(id.value);
  onInvalidate(() => {
    // id has changed or watcher is stopped.
    // invalidate previously pending async operation
    token.cancel();
  });
});
```

我们之所以是通过传入一个函数去注册失效回调，而不是从回调返回它，是因为返回值对于异步错误处理很重要。

在执行数据请求时，副作用函数往往是一个异步函数：

```js
const data = ref(null);
watchEffect(async (onInvalidate) => {
  onInvalidate(() => {
    /* ... */
  }); // 我们在Promise解析之前注册清除函数
  data.value = await fetchData(props.id);
});
```

我们知道异步函数都会隐式地返回一个 Promise，但是清理函数必须要在 Promise 被 resolve 之前被注册。另外，Vue 依赖这个返回的 Promise 来自动处理 Promise 链上的潜在错误。

#### 副作用刷新时机

Vue 的响应性系统会缓存副作用函数，并异步地刷新它们，这样可以避免同一个“tick” 中多个状态改变导致的不必要的重复调用。在核心的具体实现中，组件的 update 函数也是一个被侦听的副作用。当一个用户定义的副作用函数进入队列时，默认情况下，会在所有的组件 update 前执行：

```html
<template>
  <div>{{ count }}</div>
</template>

<script>
  export default {
    setup() {
      const count = ref(0);

      watchEffect(() => {
        console.log(count.value);
      });

      return {
        count,
      };
    },
  };
</script>
```

在这个例子中：

count 会在初始运行时同步打印出来
更改 count 时，将在组件更新前执行副作用。
如果需要在组件更新(例如：当与模板引用一起)后重新运行侦听器副作用，我们可以传递带有 flush 选项的附加 options 对象 (默认为 'pre')：

```js
// 在组件更新后触发，这样你就可以访问更新的 DOM。
// 注意：这也将推迟副作用的初始运行，直到组件的首次渲染完成。
watchEffect(
  () => {
    /* ... */
  },
  {
    flush: 'post',
  }
);
```

flush 选项还接受 sync，这将强制效果始终同步触发。然而，这是低效的，应该很少需要。

从 Vue 3.2.0 开始，watchPostEffect 和 watchSyncEffect 别名也可以用来让代码意图更加明显。

#### 侦听器调试

onTrack 和 onTrigger 选项可用于调试侦听器的行为。

onTrack 将在响应式 property 或 ref 作为依赖项被追踪时被调用。
onTrigger 将在依赖项变更导致副作用被触发时被调用。
这两个回调都将接收到一个包含有关所依赖项信息的调试器事件。建议在以下回调中编写 debugger 语句来检查依赖关系：

```js
watchEffect(
  () => {
    /* 副作用 */
  },
  {
    onTrigger(e) {
      debugger;
    },
  }
);
```

onTrack 和 onTrigger 只能在开发模式下工作。

### watch

watch API 完全等同于组件侦听器 property。watch 需要侦听特定的数据源，并在回调函数中执行副作用。默认情况下，它也是惰性的，即只有当被侦听的源发生变化时才执行回调。

与 watchEffect 比较，watch 允许我们：

懒执行副作用；
更具体地说明什么状态应该触发侦听器重新运行；
访问侦听状态变化前后的值。

#### 侦听单个数据源

侦听器数据源可以是返回值的 getter 函数，也可以直接是 ref：

```js
// 侦听一个 getter
const state = reactive({ count: 0 });
watch(
  () => state.count,
  (count, prevCount) => {
    /* ... */
  }
);

// 直接侦听ref
const count = ref(0);
watch(count, (count, prevCount) => {
  /* ... */
});
```

#### 侦听多个数据源

侦听器还可以使用数组同时侦听多个源：

```js
const firstName = ref('');
const lastName = ref('');

watch([firstName, lastName], (newValues, prevValues) => {
  console.log(newValues, prevValues);
});

firstName.value = 'John'; // logs: ["John", ""] ["", ""]
lastName.value = 'Smith'; // logs: ["John", "Smith"] ["John", ""]
```

尽管如此，如果你在同一个函数里同时改变这些被侦听的来源，侦听器仍只会执行一次：

```js
setup() {
  const firstName = ref('')
  const lastName = ref('')

  watch([firstName, lastName], (newValues, prevValues) => {
    console.log(newValues, prevValues)
  })

  const changeValues = () => {
    firstName.value = 'John'
    lastName.value = 'Smith'
    // 打印 ["John", "Smith"] ["", ""]
  }

  return { changeValues }
}
```

注意多个同步更改只会触发一次侦听器。

通过更改设置 flush: 'sync'，我们可以为每个更改都强制触发侦听器，尽管这通常是不推荐的。或者，可以用 nextTick 等待侦听器在下一步改变之前运行。例如：

```js
const changeValues = async () => {
  firstName.value = 'John'; // 打印 ["John", ""] ["", ""]
  await nextTick();
  lastName.value = 'Smith'; // 打印 ["John", "Smith"] ["John", ""]
};
```

#### 侦听响应式对象

使用侦听器来比较一个数组或对象的值，这些值是响应式的，要求它有一个由值构成的副本。

```js
const numbers = reactive([1, 2, 3, 4]);

watch(
  () => [...numbers],
  (numbers, prevNumbers) => {
    console.log(numbers, prevNumbers);
  }
);

numbers.push(5); // logs: [1,2,3,4,5] [1,2,3,4]
```

尝试检查深度嵌套对象或数组中的 property 变化时，仍然需要 deep 选项设置为 true。

```js
const state = reactive({
  id: 1,
  attributes: {
    name: '',
  },
});

watch(
  () => state,
  (state, prevState) => {
    console.log('not deep', state.attributes.name, prevState.attributes.name);
  }
);

watch(
  () => state,
  (state, prevState) => {
    console.log('deep', state.attributes.name, prevState.attributes.name);
  },
  { deep: true }
);

state.attributes.name = 'Alex'; // 日志: "deep" "Alex" "Alex"
```

然而，侦听一个响应式对象或数组将始终返回该对象的当前值和上一个状态值的引用。为了完全侦听深度嵌套的对象和数组，可能需要对值进行深拷贝。这可以通过诸如 lodash.cloneDeep 这样的实用工具来实现。

```js
import _ from 'lodash';

const state = reactive({
  id: 1,
  attributes: {
    name: '',
  },
});

watch(
  () => _.cloneDeep(state),
  (state, prevState) => {
    console.log(state.attributes.name, prevState.attributes.name);
  }
);

state.attributes.name = 'Alex'; // 日志: "Alex" ""
```

### 与 watchEffect 共享的行为

watch 与 watchEffect 共享停止侦听，清除副作用 (相应地 onInvalidate 会作为回调的第三个参数传入)、副作用刷新时机和侦听器调试行为。
