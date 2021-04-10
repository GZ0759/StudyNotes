> 个人总结的 JavaScript 面试题  
> [参考-awesome-coding-js](https://github.com/ConardLi/awesome-coding-js)  
> [参考-冴羽博客](https://github.com/mqyqingfeng/Blog/tree/master/articles)  
> [参考-后盾人](http://houdunren.gitee.io/note/js/1%20%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86.html)  
> [参考-木易杨](https://github.com/yygmind/blog)

# 函数闭包

## 闭包的概念

函数和对其周围状态（lexical environment，词法环境）的引用捆绑在一起构成闭包（closure）。也就是说，闭包可以让你从内部函数访问外部函数作用域。在 JavaScript 中，每当函数被创建，就会在函数生成时生成闭包。

使用闭包主要是为了设计私有的方法和变量。闭包的优点是可以避免全局变量的污染，缺点是闭包会常驻内存，会增大内存使用量，使用不当很容易造成内存泄露。闭包有三个特性：

1. 函数嵌套函数
2. 函数内部可以引用外部的参数和变量
3. 参数和变量不会被垃圾回收机制回收

**闭包的实用性**。闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来。这显然类似于面向对象编程。在面向对象编程中，对象允许我们将某些数据（对象的属性）与一个或者多个方法相关联。

**模拟私有方法**。编程语言中，比如 Java，是支持将方法声明为私有的，即它们只能被同一个类中的其它方法所调用。而 JavaScript 没有这种原生支持，但我们可以使用闭包来模拟私有方法。私有方法不仅仅有利于限制对代码的访问：还提供了管理全局命名空间的强大能力，避免非核心的方法弄乱了代码的公共接口部分。

**在循环中创建闭包**。在 ECMAScript 2015 引入 let 关键字之前，在循环中有一个常见的闭包创建问题。例如，这三个闭包在循环中被创建，但他们共享了同一个词法作用域，在这个作用域中存在一个变量 item。这是因为变量 item 使用 var 进行声明，由于变量提升，所以具有函数作用域。由于循环在事件触发之前早已执行完毕，变量对象 item（被三个闭包所共享）已经指向了目标内容的最后一项。

## 解决循环闭包问题

1. 闭包方法。使用更多的闭包、let 块级作用域或者 `Array.prototype.forEach()` 来解决问题。

```js
// 工厂函数
function makeHelpCallback(help) {
  return function () {
    showHelp(help);
  };
}
for (var i = 0; i < helpText.length; i++) {
  var item = helpText[i];
  document.getElementById(item.id).onfocus = makeHelpCallback(item.help);
}

// 匿名闭包
for (var i = 0; i < helpText.length; i++) {
  (function () {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function () {
      showHelp(item.help);
    };
  })();
}

// let关键字
for (var i = 0; i < helpText.length; i++) {
  let item = helpText[i];
  document.getElementById(item.id).onfocus = function () {
    showHelp(item.help);
  };
}

// 数组forEach方法
helpText.forEach(function (text) {
  document.getElementById(text.id).onfocus = function () {
    showHelp(text.help);
  };
});
```

2. 非闭包方法。通过其他针对性方法来解决问题。

```js
// 对象属性保存
for (var i = 0; i < lis.length; i++) {
  var li = lis[i];
  li.index = i;
  li.onclick = function (e) {
    window.alert(this.index);
  };
}

// 事件委派
let ul = document.querySelector('ul');
ul.addEventListener('click', function (e) {
  window.alert(lis.indexOf(e.srcElement));
});

// 使用setTimeout的第三个参数
for (var i = 1; i <= 5; i++) {
  setTimeout(
    function timer(j) {
      console.log(j);
    },
    i * 1000,
    i
  );
}
```

# 深浅拷贝

如果数组元素是基本类型，就会拷贝一份，互不影响，而如果是对象或者数组，就会只拷贝对象和数组的引用，这样我们无论在新旧数组进行了修改，两者都会发生变化。我们把这种复制引用的拷贝方法称之为浅拷贝，与之对应的就是深拷贝，深拷贝就是指完全的拷贝一个对象，即使嵌套了对象，两者也相互分离，修改一个对象的属性，也不会影响另一个。

## 浅拷贝

1. 利用数组本身的 slice 或 concat 方法

```js
var arr = ['old', 1, true, null, undefined];
var new_arr = arr.concat();
// 或者
var new_arr = arr.slice();
```

2. 使用 for...in 遍历对象进行拷贝

```js
var shallowCopy = function (obj) {
  if (typeof obj !== 'object') return;
  var newObj = obj instanceof Array ? [] : {};
  for (var key in obj) {
    if (obj.hasOwnProperty(key)) {
      newObj[key] = obj[key];
    }
  }
  return newObj;
};
```

3. 利用 ES6 的 `Object.assign` 函数进行拷贝或覆盖

```js
let user = { name: '后盾人' };
let hd = Object.assign({}, user);
```

4. 利用 ES6 的展开语法

```js
let obj = { name: '后盾人' };
let hd = { ...obj };
```

## 深拷贝

1. JSON 序列化和解析，可用于数组和对象

```js
var arr = ['old', 1, true, ['old1', 'old2'], { old: 1 }];
var new_arr = JSON.parse(JSON.stringify(arr));
console.log(new_arr);
```

但是该方法有以下几个问题。

- 会忽略 undefined
- 会忽略 symbol
- 不能序列化函数
- 不能解决循环引用的对象
- 不能正确处理`new Date()`
- 不能处理正则

2. 递归遍历。拷贝时判断类型，如果是对象则递归调用

```js
var deepCopy = function (target) {
  if (typeof target !== 'object') return target;
  if (target === null) return null;

  var obj = target instanceof Array ? [] : {};
  for (const [k, v] of Object.entries(target)) {
    obj[k] = deepCopy(v);
  }
  return obj;
};
```

尽管使用深拷贝会完全的克隆一个新对象，不会产生副作用，但是深拷贝因为使用递归，性能会不如浅拷贝，在开发中，还是要根据实际情况进行选择。

## 循环引用

我们知道 JSON 无法深拷贝循环引用，遇到这种情况会抛出异常。

```js
let a = {};
a.circleRef = a;

JSON.parse(JSON.stringify(a));
// TypeError: Converting circular structure to JSON
```

1. 使用哈希表

解决方案很简单，其实就是循环检测，我们设置一个数组或者哈希表存储已拷贝过的对象，当检测到当前对象已存在于哈希表中时，取出该值并返回即可。也可以使用了 ES6 中的 WeakMap 来处理。

```js
function cloneDeep3(source, hash = new WeakMap()) {
  if (!isObject(source)) return source;
  if (hash.has(source)) return hash.get(source); // 新增代码，查哈希表

  var target = Array.isArray(source) ? [] : {};
  hash.set(source, target); // 新增代码，哈希表设值

  for (var key in source) {
    if (Object.prototype.hasOwnProperty.call(source, key)) {
      if (isObject(source[key])) {
        target[key] = cloneDeep3(source[key], hash); // 新增代码，传入哈希表
      } else {
        target[key] = source[key];
      }
    }
  }
  return target;
}

function isObject(obj) {
  return typeof obj === 'object' && obj != null;
}
```

2. 使用数组

这里使用了 ES6 中的 WeakMap 来处理，那在 ES5 下应该如何处理呢？也很简单，使用数组来处理就好啦，代码如下。

```js
// 木易杨
function cloneDeep3(source, uniqueList) {
  if (!isObject(source)) return source;
  if (!uniqueList) uniqueList = []; // 初始化数组

  var target = Array.isArray(source) ? [] : {};

  // 数据已经存在，返回保存的数据
  var uniqueData = find(uniqueList, source);
  if (uniqueData) {
    return uniqueData.target;
  }

  // 数据不存在，保存源数据，以及对应的引用
  uniqueList.push({
    source: source,
    target: target,
  });

  for (var key in source) {
    if (Object.prototype.hasOwnProperty.call(source, key)) {
      if (isObject(source[key])) {
        target[key] = cloneDeep3(source[key], uniqueList); // 新增代码，传入数组
      } else {
        target[key] = source[key];
      }
    }
  }
  return target;
}

// 新增方法，用于查找
function find(arr, item) {
  for (var i = 0; i < arr.length; i++) {
    if (arr[i].source === item) {
      return arr[i];
    }
  }
  return null;
}
```

4. 拷贝 Symbol

这个时候可能要搞事情了，那我们能不能拷贝 Symol 类型呢？

当然可以，不过 Symbol 在 ES6 下才有，我们需要一些方法来检测出 Symble 类型。

- Object.getOwnPropertySymbols(...)
- Reflect.ownKeys(...)

对于方法一可以查找一个给定对象的符号属性时返回一个 ?symbol 类型的数组。注意，每个初始化的对象都是没有自己的 symbol 属性的，因此这个数组可能为空，除非你已经在对象上设置了 symbol 属性。（来自 MDN）

```js
var obj = {};
var a = Symbol('a'); // 创建新的symbol类型
var b = Symbol.for('b'); // 从全局的symbol注册?表设置和取得symbol

obj[a] = 'localSymbol';
obj[b] = 'globalSymbol';

var objectSymbols = Object.getOwnPropertySymbols(obj);

console.log(objectSymbols.length); // 2
console.log(objectSymbols); // [Symbol(a), Symbol(b)]
console.log(objectSymbols[0]); // Symbol(a)
```

对于方法二返回一个由目标对象自身的属性键组成的数组。它的返回值等同于 Object.getOwnPropertyNames(target).concat(Object.getOwnPropertySymbols(target))。(来自 MDN)

```js
Reflect.ownKeys({ z: 3, y: 2, x: 1 }); // [ "z", "y", "x" ]
Reflect.ownKeys([]); // ["length"]

var sym = Symbol.for('comet');
var sym2 = Symbol.for('meteor');
var obj = {
  [sym]: 0,
  str: 0,
  773: 0,
  0: 0,
  [sym2]: 0,
  '-1': 0,
  8: 0,
  'second str': 0,
};
Reflect.ownKeys(obj);
// [ "0", "8", "773", "str", "-1", "second str", Symbol(comet), Symbol(meteor) ]
// 注意顺序
// Indexes in numeric order,
// strings in insertion order,
// symbols in insertion order
```

方法一
思路就是先查找有没有 Symbol 属性，如果查找到则先遍历处理 Symbol 情况，然后再处理正常情况，多出来的逻辑就是下面的新增代码。

```js
// 木易杨
function cloneDeep4(source, hash = new WeakMap()) {
  if (!isObject(source)) return source;
  if (hash.has(source)) return hash.get(source);

  let target = Array.isArray(source) ? [] : {};
  hash.set(source, target);

  // ============= 新增代码
  let symKeys = Object.getOwnPropertySymbols(source); // 查找
  if (symKeys.length) {
    // 查找成功
    symKeys.forEach((symKey) => {
      if (isObject(source[symKey])) {
        target[symKey] = cloneDeep4(source[symKey], hash);
      } else {
        target[symKey] = source[symKey];
      }
    });
  }
  // =============

  for (let key in source) {
    if (Object.prototype.hasOwnProperty.call(source, key)) {
      if (isObject(source[key])) {
        target[key] = cloneDeep4(source[key], hash);
      } else {
        target[key] = source[key];
      }
    }
  }
  return target;
}
```

5. 破解递归爆栈

上面四步使用的都是递归方法，但是有一个问题在于会爆栈，错误提示如下。

```js
// RangeError: Maximum call stack size exceeded
```

那应该如何解决呢？其实我们使用循环就可以了，代码如下。

```js
function cloneDeep5(x) {
  const root = {};

  // 栈
  const loopList = [
    {
      parent: root,
      key: undefined,
      data: x,
    },
  ];

  while (loopList.length) {
    // 广度优先
    const node = loopList.pop();
    const parent = node.parent;
    const key = node.key;
    const data = node.data;

    // 初始化赋值目标，key为undefined则拷贝到父元素，否则拷贝到子元素
    let res = parent;
    if (typeof key !== 'undefined') {
      res = parent[key] = {};
    }

    for (let k in data) {
      if (data.hasOwnProperty(k)) {
        if (typeof data[k] === 'object') {
          // 下一次循环
          loopList.push({
            parent: res,
            key: k,
            data: data[k],
          });
        } else {
          res[k] = data[k];
        }
      }
    }
  }

  return root;
}
```

# 函数节流和防抖

防抖 debounce 和节流 throttle 是前端开发中经常使用的一种优化手段，它们都被用来控制一段时间内方法执行的次数，可以为我们节省大量不必要的开销。

## 防抖

防抖的功效，它把一组连续的调用变为了一个，最大程度地优化了效率。防抖非常适于只关心结果，不关心过程如何的情况，它能很好地将大量连续事件转为单个我们需要的事件。

应用场景

1. 窗口大小变化，只关心最后结果
2. 搜索栏，只关心完成结果
3. 表单验证，延迟后进行验证

为了更好理解，下面提供了最简单的 debounce 实现：

```js
const debounce = function (func, wait) {
  let timer;
  return function () {
    !!timer && clearTimeout(timer);
    timer = setTimeout(func, wait);
  };
};
```

给`debounce`函数一个`flag`用于标示是否立即执行。同时保留上下文和参数。

```js
function debounce(func, wait, flag = false) {
  let timer;
  return function (...args) {
    !!timer && clearTimeout(timer);
    if (flag && !timer) {
      func.apply(this, args);
    }
    timer = setTimeout(() => {
      func.apply(this, args);
    }, wait);
  };
}
```

> 不管事件触发频率多高，一定在事件触发 n 秒后才执行，如果你在一个事件触发的 n 秒内又触发了这个事件，就以新的事件的时间为准，n 秒后才执行，总之，触发完事件 n 秒内不再触发事件，n 秒后再执行。

## 节流

节流让指定函数在规定的时间里执行次数不会超过一次，也就是说，在连续高频执行中，动作会被定期执行。节流的主要目的是将原本操作的频率降低。

1. 时间戳实现。

```js
// 时间段开始触发
function throttle(event, time) {
  let pre = 0;
  return function (...args) {
    if (Date.now() - pre > time) {
      pre = Date.now();
      event.apply(this, args);
    }
  };
}
```

2. 定时器实现。

```js
// 时间段结束触发
function throttle(event, time) {
  let timer = null;
  return function (...args) {
    if (!timer) {
      timer = setTimeout(() => {
        timer = null;
        event.apply(this, args);
      }, time);
    }
  };
}
```

> 不管事件触发频率多高，只在单位时间内执行一次。

## 结合版本

现在考虑一种情况，如果用户的操作非常频繁，不等设置的延迟时间结束就进行下次操作，会频繁的清除计时器并重新生成，所以函数 fn 一直都没办法执行，导致用户操作迟迟得不到响应。有一种思想是将节流和防抖合二为一，变成加强版的节流函数，关键点在于「wait 时间内，可以重新生成定时器，但只要 wait 的时间到了，必须给用户一个响应」。这种合体思路恰好可以解决上面提出的问题。

```js
function throttle(fn, wait) {
  let previous = 0,
    timer = null;
  return function (...args) {
    let now = +new Date();
    if (now - previous < wait) {
      // 没到时间重新生成定时器
      if (timer) clearTimeout(timer);
      timer = setTimeout(() => {
        previous = now;
        fn.apply(this, args);
      }, wait);
    } else {
      // 时间到必须触发
      previous = now;
      fn.apply(this, args);
    }
  };
}
```

## rAF

requestAnimationFrame（rAF） 在一定程度上和 `throttle(func, 16)` 的作用相似，但它是浏览器自带的 api，所以，它比 throttle 函数执行得更加平滑。调用 `window.requestAnimationFrame()`，浏览器会在下次刷新的时候执行指定回调函数。通常，屏幕的刷新频率是 60hz，所以，这个函数也就是大约 16.7ms 执行一次。如果你想让你的动画更加平滑，用 rAF 就再好不过了，因为它是跟着屏幕的刷新频率来的。

rAF 的写法与 debounce 和 throttle 不同，如果你想用它绘制动画，需要不停地在回调函数里调用自身，具体写法可以参考[MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame)。

rAF 支持 ie10 及以上浏览器，不过因为是浏览器自带的 api，我们也就无法在 node 中使用它了。

# 数组去重

1. 最原始的方法的使用双重循环，其中第二重遍历可以使用 indexOf 方法或 includes 方法简化。

```js
function unique(array) {
  let res = [];
  for (let i = 0; i < array.length; i++) {
    for (let j = 0; j < res.length; j++) {
      if (array[i] === res[j]) {
        break;
      }
    }
    if (j === res.length) {
      res.push(array[i]);
    }
  }
  return res;
}
```

2. 通过 `filter()` 方法创建一个符合测试的新数组。

```js
const unique = (arr) =>
  arr.filter((item, index) => {
    return arr.indexOf(item) === index;
  });

// 如果是重复数字则删除
const filterNonUnique = (arr) =>
  arr.filter((i) => {
    return arr.indexOf(i) === arr.lastIndexOf(i);
  });
```

3. 通过 `sort()` 方法进行排序，然后判断是否有重复。

```js
const unique = (array) => {
  array.sort((a, b) => a - b);
  let pre = 0;
  const result = [];
  // 第一个元素或者相邻的元素不相同
  for (let i = 0; i < array.length; i++) {
    if (!i || array[i] != array[pre]) {
      result.push(array[i]);
    }
    pre = i;
  }
  return result;
};
```

4. 使用 ES6 提供了新的数据结构 Set。

```js
const unique = (arr) => Array.from(new Set(arr));
// 或者
const unique = (arr) => [...new Set(arr)];
```

5. 使用 ES6 提供了 Map 数据结构。

```js
function unique(arr) {
  const seen = new Map();
  return arr.filter((a) => !seen.has(a) && seen.set(a, 1));
}
```

# 数组扁平化

1. 循环递归的基本实现

```js
const flat = (array) => {
  let result = [];
  for (let i = 0; i < array.length; i++) {
    if (Array.isArray(array[i])) {
      result = result.concat(flat(array[i]));
    } else {
      result.push(array[i]);
    }
  }
  return result;
};
```

2. 使用`reduce()`简化递归遍历

```js
function flatten(array) {
  return array.reduce(
    (target, current) =>
      Array.isArray(current)
        ? target.concat(flatten(current))
        : target.concat(current),
    []
  );
}
```

3. 数组 `some()` 方法和 ES6 扩展运算符

```js
function flatten(arr) {
  while (arr.some(Array.isArray)) {
    arr = [].concat(...arr)
  }
  // while (arr.some((item) => Array.isArray(item))) {
  //   arr = [].concat(...arr);
  // }
  return arr;
}
```

4. 字符串`toString()`方法

如果数组的元素都是数字或都是字符串，那么我们可以考虑使用 toString 方法，因为：调用 toString 方法，返回了一个逗号分隔的扁平的字符串。然而这种方法使用的场景却非常有限，如果数组是 `[1, '1', 2, '2']` 的话，这种方法就会产生错误的结果。

```js
function flatten(arr) {
  return arr
    .toString()
    .split(',')
    .map(item => +item);
}
```

5. 字符串过滤

将输入数组转换为字符串并删除所有括号`[]`并将输出解析为数组。

```js
const flatten = (arr) => {
  let re = /\[|\]/g;
  let str = JSON.stringify(arr).replace(re, '');
  return JSON.parse(`[${str}]`);
};
```

6. ES6 的 `Array.prototype.flat()` 方法

`flat()`默认只会“拉平”一层，如果想要“拉平”多层的嵌套数组，可以将`flat()`方法的参数写成一个整数，表示想要拉平的层数，默认为 1。如果不管有多少层嵌套，都要转成一维数组，可以用`Infinity`关键字作为参数。

```js
function flatten(arr) {
  return arr.flat(Infinity);
}
```

# 数组最值

1. 直接循环

```js
var result = arr[0];
for (var i = 1; i < arr.length; i++) {
  result = Math.max(result, arr[i]);
}
```

2. 使用 `reduce()` 方法简化循环

```js
array.reduce((c, n) => Math.max(c, n));
```

3. 调用原生方法 `Math.max()`。

```js
const array = [3, 2, 1, 4, 5];
Math.max.apply(null, array);
// 或者
// Math.max(...array);
```

4. 使用 `sort()` 方法排序

```js
arr.sort(function (a, b) {
  return a - b;
});
arr[arr.length - 1];
```

# 函数柯里化

在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。通俗易懂的解释：用闭包把参数保存起来，当参数的数量足够执行函数了，就开始执行函数。

判断当前函数传入的参数是否大于或等于`fn`需要参数的数量，如果是，直接执行`fn`。如果传入参数数量不够，返回一个闭包，暂存传入的参数，并重新返回`currying`函数。

## 实际应用

1. 参数复用，需要输入多个参数，最终只需输入一个。
2. 延迟运行，例如部分求和，而 bind 函数的模拟实现和柯理化函数的实现，其核心代码都是一致的。
3. 提前确定，例如只计算一次的函数或者惰性函数。

```js
// 添加监听 addEvent 函数
const addEvent = (function () {
  // 闭包和立即调用函数表达式（IIFE）
  if (window.addEventListener) {
    return function (type, el, fn, capture) {
      el.addEventListener(type, fn, capture);
    };
  } else if (window.attachEvent) {
    return function (type, el, fn) {
      el.attachEvent('on' + type, fn);
    };
  }
})();
```

```js
// 惰性函数
function addEvent(type, el, fn, capture = false) {
  // 重写函数
  if (window.addEventListener) {
    addEvent = function (type, el, fn, capture) {
      el.addEventListener(type, fn, capture);
    };
  } else if (window.attachEvent) {
    addEvent = function (type, el, fn) {
      el.attachEvent('on' + type, fn);
    };
  }
  // 执行函数，有循环爆栈风险
  addEvent(type, el, fn, capture);
}
```

## 实现方法

1. 使用 ES6 极简写法，更加简洁也更加易懂。

```js
function currying(fn, ...args) {
  if (args.length >= fn.length) {
    return fn(...args);
  } else {
    return (...args2) => currying(fn, ...args, ...args2);
  }
}
```

2. 使用兼容语法。

```js
function progressCurrying(fn, args) {
  var _this = this;
  var len = fn.length;
  var args = args || [];
  return function () {
    var _args = Array.prototype.slice.call(arguments);
    Array.prototype.push.apply(args, _args);

    if (_args.length < len) {
      return progressCurrying.call(_this, fn, _args);
    }

    return fn.apply(this, _args);
  };
}
```

# 模拟实现 call

`call()` 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。

实现步骤：

1. 判断当前 this 是否为函数，防止 `Function.prototype.myCall()` 直接调用
2. context 为可选参数，如果不传的话默认上下文为 window
3. 为 context 创建一个 Symbol（保证不会重名）属性，将当前函数赋值给这个属性
4. 处理参数，传入第一个参数后的其余参数
5. 调用函数后即删除该 Symbol 属性

```js
Function.prototype.myCall = function (context, ...args) {
  if (this === Function.prototype) {
    return undefined;
  }
  context = Object(context) || window;
  const fn = Symbol();
  context[fn] = this;

  const result = context[fn](...args);
  delete context[fn];
  return result;
};
```

call 是 ES3 的方法，展开运算符是 ES6 的功能。所以用 eval 方法拼成一个函数。这里 args 会自动调用 `Array.toString()` 这个方法。

```js
var args = [];
for (var i = 1, len = arguments.length; i < len; i++) {
  args.push('arguments[' + i + ']');
}
var result = eval('context.fn(' + args + ')');
```

# 模拟实现 apply

`apply`实现类似`call`，该方法调用一个具有给定 this 值的函数，以及以一个数组（或类数组对象）的形式提供的参数。

```js
Function.prototype.myApply = function (context, args) {
  if (this === Function.prototype) {
    return undefined;
  }
  context = Object(context) || window;
  const fn = Symbol();
  context[fn] = this;
  let result;
  if (Array.isArray(args)) {
    result = context[fn](...args);
  } else {
    result = context[fn]();
  }
  delete context[fn];
  return result;
};
```

# 模拟实现 bind

`bind()` 方法创建一个新的函数，在 `bind()` 被调用时，这个新函数的 this 被指定为 `bind()` 的第一个参数，而其余参数将作为新函数的参数，供调用时使用。绑定函数也可以使用 new 运算符构造，它会表现为目标函数已经被构建完毕了似的。提供的 this 值会被忽略，但前置参数仍会提供给模拟函数。

实现步骤：

1. 处理参数，返回一个闭包
2. 判断是否为构造函数调用，如果是则使用`new`调用当前函数
3. 如果不是，使用`apply`，将`context`和处理好的参数传入

```js
Function.prototype.myBind = function (context, ...args1) {
  if (this === Function.prototype) {
    throw new TypeError('Error');
  }
  const _this = this;
  return function F(...args2) {
    // 判断是否用于构造函数
    if (this instanceof F) {
      return new _this(...args1, ...args2);
    }
    return _this.apply(context, [...args1, ...args2]);
  };
};
```

兼容到 ES5 版本。

```js
Function.prototype.bind2 = function (context) {
  if (typeof this !== 'function') {
    throw new Error(
      'Function.prototype.bind - what is trying to be bound is not callable'
    );
  }
  var self = this;
  var args = Array.prototype.slice.call(arguments, 1);

  var fNOP = function () {};
  var fBound = function () {
    var bindArgs = Array.prototype.slice.call(arguments);
    return self.apply(
      this instanceof fNOP ? this : context,
      args.concat(bindArgs)
    );
  };

  fNOP.prototype = this.prototype;
  fBound.prototype = new fNOP();
  return fBound;
};
```

# 模拟实现 instanceof

instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

原型与原型链（prototype chain）关系

- 函数的`prototype`属性指向了一个对象，这个对象正是调用该构造函数而创建的实例的原型
- 每一个 JavaScript 对象（除了 null ）都具有的一个属性，叫`__proto__`，这个属性会指向该对象的原型
- 每个原型都有一个`constructor`属性指向关联的构造函数，实例也可以继承该属性

```js
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
const auto = new Car('Honda', 'Accord', 1998);

console.log(auto instanceof Car); // true
console.log(auto instanceof Object); // true
```

实现

```js
function myInstanceof(target, origin) {
  const proto = target.__proto__;
  if (proto) {
    if (origin.prototype === proto) {
      return true;
    } else {
      return myInstanceof(proto, origin);
    }
  } else {
    return false;
  }
}
```

# 模拟实现 new

new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。new 关键字会进行如下的操作：

1. 创建一个空的简单 JavaScript 对象；
2. 链接该对象（设置该对象的 constructor）到另一个对象；
3. 将步骤 1 新创建的对象作为 this 的上下文；
4. 如果该函数没有返回对象，则返回 this。

```js
function create(Con, ...args) {
  let obj = {};
  Object.setPrototypeOf(obj, Con.prototype);
  let result = Con.apply(obj, args);
  return result instanceof Object ? result : obj;
}
```

```js
function create() {
  // 1、获得构造函数，同时删除 arguments 中第一个参数
  Con = [].shift.call(arguments);
  // 2、创建一个空的对象并链接到原型，obj 可以访问构造函数原型中的属性
  var obj = Object.create(Con.prototype);
  // 3、绑定 this 实现继承，obj 可以访问到构造函数中的属性
  var ret = Con.apply(obj, arguments);
  // 4、优先返回构造函数返回的对象
  return ret instanceof Object ? ret : obj;
}
```

# 模拟实现 Promise

## 基本结构 Promise

- 设定三个状态 PENDING/FULFILLED/REJECTED ，只能由 PENDING 改变为 FULFILLED/REJECTED ，并且只能改变一次
- MyPromise 构造函数接收一个双参函数 executor，参数是 resolve/reject，它们是函数类型
  1. resolve 函数被调用时将 PENDING 改变为 FULFILLED，此时 MyPromise 具有唯一的 value 值
  2. reject 函数被调用时将 PENDING 改变为 REJECTED，此时 MyPromise 具有唯一的 reason 值

```js
const PENDING = 'pending';
const FULFILLED = 'fulfilled';
const REJECTED = 'rejected';

function MyPromise(executor) {
  this.state = PENDING;
  this.value = null;
  this.reason = null;

  const resolve = (value) => {
    if (this.state === PENDING) {
      this.state = FULFILLED;
      this.value = value;
    }
  };

  const reject = (reason) => {
    if (this.state === PENDING) {
      this.state = REJECTED;
      this.reason = reason;
    }
  };

  try {
    executor(resolve, reject);
  } catch (reason) {
    reject(reason);
  }
}
```

## 原型方法 then

- then 方法接受两个回调函数 onFulfilled/onRejected 作为参数 ，它们分别在状态由 PENDING 改变为 FULFILLED/REJECTED 后被调用
- 一个 promise 可绑定多个 then 方法，可将 onFulfilled/onRejected 分别加入两个函数数组 onFulfilledCallbacks/onRejectedCallbacks
- then 方法可以同步调用也可以异步调用，也可以进行链式调用。
  1. 同步调用：状态已经改变，直接调用 onFulfilled 方法
  2. 异步调用：状态还是 PENDING ，加入函数数组，当异步调用 resolve/reject 时，将两个数组中绑定的事件循环执行
  3. 链式调用：返回一个 Promise 对象

```js
function MyPromise(executor) {
  this.state = PENDING;
  this.value = null;
  this.reason = null;
  this.onFulfilledCallbacks = [];
  this.onRejectedCallbacks = [];

  const resolve = (value) => {
    if (this.state === PENDING) {
      this.state = FULFILLED;
      this.value = value;
      this.onFulfilledCallbacks.forEach((fun) => {
        fun();
      });
    }
  };

  const reject = (reason) => {
    if (this.state === PENDING) {
      this.state = REJECTED;
      this.reason = reason;
      this.onRejectedCallbacks.forEach((fun) => {
        fun();
      });
    }
  };

  try {
    executor(resolve, reject);
  } catch (reason) {
    reject(reason);
  }
}

MyPromise.prototype.then = function (onFulfilled, onRejected) {
  switch (this.state) {
    case FULFILLED:
      onFulfilled(this.value);
      break;
    case REJECTED:
      onFulfilled(this.value);
      break;
    case PENDING:
      this.onFulfilledCallbacks.push(() => {
        onFulfilled(this.value);
      });
      this.onRejectedCallbacks.push(() => {
        onRejected(this.reason);
      });
      break;
  }
};
```

### then 方法异步调用

虽然 resolve 是同步执行的，我们必须保证 then 是异步调用的，我们用 setTimeout 来模拟异步调用（并不能实现微任务和宏任务的执行机制，只是保证异步调用）。

```js
MyPromise.prototype.then = function (onFulfilled, onRejected) {
  if (typeof onFulfilled != 'function') {
    onFulfilled = function (value) {
      return value;
    };
  }
  if (typeof onRejected != 'function') {
    onRejected = function (reason) {
      throw reason;
    };
  }
  switch (this.state) {
    case FULFILLED:
      setTimeout(() => {
        onFulfilled(this.value);
      }, 0);
      break;
    case REJECTED:
      setTimeout(() => {
        onRejected(this.reason);
      }, 0);
      break;
    case PENDING:
      this.onFulfilledCallbacks.push(() => {
        setTimeout(() => {
          onFulfilled(this.value);
        }, 0);
      });
      this.onRejectedCallbacks.push(() => {
        setTimeout(() => {
          onRejected(this.reason);
        }, 0);
      });
      break;
  }
};
```

### then 方法链式调用

then 可以采用链式写法，即 then 方法中要返回一个新的 promise ，并将 then 方法的返回值进行 resolve 。注意：这种实现并不能保证 then 方法中返回一个新的 promise ，只能保证链式调用。

```js
MyPromise.prototype.then = function (onFulfilled, onRejected) {
  if (typeof onFulfilled != 'function') {
    onFulfilled = function (value) {
      return value;
    };
  }
  if (typeof onRejected != 'function') {
    onRejected = function (reason) {
      throw reason;
    };
  }
  const promise2 = new MyPromise((resolve, reject) => {
    switch (this.state) {
      case FULFILLED:
        setTimeout(() => {
          try {
            const x = onFulfilled(this.value);
            resolve(x);
          } catch (reason) {
            reject(reason);
          }
        }, 0);
        break;
      case REJECTED:
        setTimeout(() => {
          try {
            const x = onRejected(this.reason);
            resolve(x);
          } catch (reason) {
            reject(reason);
          }
        }, 0);
        break;
      case PENDING:
        this.onFulfilledCallbacks.push(() => {
          setTimeout(() => {
            try {
              const x = onFulfilled(this.value);
              resolve(x);
            } catch (reason) {
              reject(reason);
            }
          }, 0);
        });
        this.onRejectedCallbacks.push(() => {
          setTimeout(() => {
            try {
              const x = onRejected(this.reason);
              resolve(x);
            } catch (reason) {
              reject(reason);
            }
          }, 0);
        });
        break;
    }
  });
  return promise2;
};
```

## 原型方法 catch

若上面没有定义 reject 方法，所有的异常会走向 catch 方法：

```js
MyPromise.prototype.catch = function (onRejected) {
  return this.then(null, onRejected);
};
```

## 原型方法 finally

不管是 resolve 还是 reject 都会调用 finally 。

```js
MyPromise.prototype.finally = function (fn) {
  return this.then(
    (value) => {
      fn();
      return value;
    },
    (reason) => {
      fn();
      throw reason;
    }
  );
};
```

## 静态方法 Promise.resolve

Promise.resolve 用来生成一个直接处于 FULFILLED 状态的 Promise。

```js
MyPromise.reject = function (value) {
  return new MyPromise((resolve, reject) => {
    resolve(value);
  });
};
```

## 静态方法 Promise.reject

Promise.reject 用来生成一个直接处于 REJECTED 状态的 Promise。

```js
MyPromise.reject = function (reason) {
  return new MyPromise((resolve, reject) => {
    reject(reason);
  });
};
```

## 静态方法 Promise.all

接受一个 promise 数组，当所有 promise 状态 resolve 后，执行 resolve 。

```js
MyPromise.all = function (promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      resolve([]);
    } else {
      let result = [];
      let index = 0;
      for (let i = 0; i < promises.length; i++) {
        promises[i].then(
          (data) => {
            result[i] = data;
            if (++index === promises.length) {
              resolve(result);
            }
          },
          (err) => {
            reject(err);
            return;
          }
        );
      }
    }
  });
};
```

## 静态方法 Promise.race

接受一个 promise 数组，当有一个 promise 状态 resolve 后，执行 resolve 。

```js
MyPromise.race = function (promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      resolve();
    } else {
      let index = 0;
      for (let i = 0; i < promises.length; i++) {
        promises[i].then(
          (data) => {
            resolve(data);
          },
          (err) => {
            reject(err);
            return;
          }
        );
      }
    }
  });
};
```

## 不足之处

1. 如果 excutor 的 resolve 方法接受的参数是一个 Promise 对象会怎么样？

[研究：当 resolve 函数参数里是另外一个 Promise 实例](https://segmentfault.com/a/1190000023409765)

一个 Promise 实例 的 resolve 函数的参数除了正常的值以外，还可能是另一个 Promise 实例，后者的状态决定了前者的状态。应该是新添加的 Promise A+规范。

2. Promise.then 返回的是一个 Promise 实例

[从零开始手写Promise](https://zhuanlan.zhihu.com/p/144058361)

Promise 解决过程 The Promise Resolution Procedure

Promise 解决过程是一个抽象的操作，其需输入一个 promise 和一个值，我们表示为 `[[Resolve]](promise, x)`，如果 x 有 then 方法且看上去像一个 Promise ，解决程序即尝试使 promise 接受 x 的状态；否则其用 x 的值来执行 promise 。

[MDN Promise.prototype.then](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)

当一个 Promise 完成（fulfilled）或者失败（rejected）时，返回函数将被异步调用（由当前的线程循环来调度完成）。具体的返回值依据以下规则返回。如果 then 中的回调函数：

- 返回了一个值，那么 then 返回的 Promise 将会成为接受状态，并且将返回的值作为接受状态的回调函数的参数值。
- 没有返回任何值，那么 then 返回的 Promise 将会成为接受状态，并且该接受状态的回调函数的参数值为 undefined。
- 抛出一个错误，那么 then 返回的 Promise 将会成为拒绝状态，并且将抛出的错误作为拒绝状态的回调函数的参数值。
- 返回一个已经是接受状态的 Promise，那么 then 返回的 Promise 也会成为接受状态，并且将那个 Promise 的接受状态的回调函数的参数值作为该被返回的 Promise 的接受状态回调函数的参数值。
- 返回一个已经是拒绝状态的 Promise，那么 then 返回的 Promise 也会成为拒绝状态，并且将那个 Promise 的拒绝状态的回调函数的参数值作为该被返回的 Promise 的拒绝状态回调函数的参数值。
- 返回一个未定状态（pending）的 Promise，那么 then 返回 Promise 的状态也是未定的，并且它的终态与那个 Promise 的终态相同；同时，它变为终态时调用的回调函数参数与那个 Promise 变为终态时的回调函数的参数是相同的。

# 手动实现 JSONP

1. 将传入的 data 数据转化为 url 字符串形式
2. 处理 url 中的回调函数
3. 创建一个 script 标签并插入到页面中
4. 挂载回调函数

```js
(function (window, document) {
  'use strict';
  var jsonp = function (url, data, callback) {
    var dataString = url.indexof('?') === -1 ? '?' : '&';
    for (var key in data) {
      dataString += key + '=' + data[key] + '&';
    }

    // cbFuncName回调函数的名字 ：my_json_cb_名字的前缀 + 随机数（把小数点去掉）
    var cbFuncName = 'my_json_cb_' + Math.random().toString().replace('.', '');
    dataString += 'callback=' + cbFuncName;

    var scriptEle = document.createElement('script');
    scriptEle.src = url + dataString;

    window[cbFuncName] = function (data) {
      callback(data);
      document.body.removeChild(scriptEle);
    };

    document.body.appendChild(scriptEle);
  };

  window.$jsonp = jsonp;
})(window, document);
```