> 个人总结的 JavaScript 面试题  
> [参考-awesome-coding-js](https://github.com/ConardLi/awesome-coding-js)   
> [参考-冴羽博客](https://github.com/mqyqingfeng/Blog/tree/master/articles)   
> [参考-后盾人](http://houdunren.gitee.io/note/js/1%20%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86.html)  
> [参考-木易杨](https://github.com/yygmind/blog)  

# 函数闭包

函数和对其周围状态（lexical environment，词法环境）的引用捆绑在一起构成闭包（closure）。也就是说，闭包可以让你从内部函数访问外部函数作用域。在 JavaScript 中，每当函数被创建，就会在函数生成时生成闭包。

## 闭包的实用性

闭包很有用，因为它允许将函数与其所操作的某些数据（环境）关联起来。这显然类似于面向对象编程。在面向对象编程中，对象允许我们将某些数据（对象的属性）与一个或者多个方法相关联。

```js
function makeSizer(size) {
  return function () {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```

## 模拟私有方法

编程语言中，比如 Java，是支持将方法声明为私有的，即它们只能被同一个类中的其它方法所调用。而 JavaScript 没有这种原生支持，但我们可以使用闭包来模拟私有方法。私有方法不仅仅有利于限制对代码的访问：还提供了管理全局命名空间的强大能力，避免非核心的方法弄乱了代码的公共接口部分。

```js
var Counter = (function () {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function () {
      changeBy(1);
    },
    decrement: function () {
      changeBy(-1);
    },
    value: function () {
      return privateCounter;
    },
  };
})();
```

## 在循环中创建闭包

在 ECMAScript 2015 引入 let 关键字之前，在循环中有一个常见的闭包创建问题。

```js
// DOM 事件回调
function setupHelp() {
  var helpText = [
    { id: 'email', help: 'Your e-mail address' },
    { id: 'name', help: 'Your full name' },
    { id: 'age', help: 'Your age (you must be over 16)' },
  ];

  for (var i = 0; i < helpText.length; i++) {
    var item = helpText[i];
    document.getElementById(item.id).onfocus = function () {
      showHelp(item.help);
    };
  }
}

// 打印页面元素序号
var nodeList = document.getElementsByTagName('li');
for (var i = 0; i < nodeList.length; i++) {
    nodeList[i].addEventListener("click", function() {
        window.alert(i);
    });
}

// 定时器回调
for (var i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    console.log(i);
  }, i * 1000);
}
```

## 循环闭包的解决办法

### 闭包方法

使用更多的闭包来解决问题。

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

### 非闭包方法

通过其他针对性方法来解决问题。

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
var deepCopy = function (obj) {
  if (typeof obj !== 'object') return obj;
  var newObj = obj instanceof Array ? [] : {};
  for (const [k, v] of Object.entries(obj)) {
    newObj[k] = deepCopy(v);
  }
  return newObj;
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

防抖和节流是前端开发中经常使用的一种优化手段，它们都被用来控制一段时间内方法执行的次数，可以为我们节省大量不必要的开销。

## 防抖（debounce）

防抖的功效，它把一组连续的调用变为了一个，最大程度地优化了效率。防抖非常适于只关心结果，不关心过程如何的情况，它能很好地将大量连续事件转为单个我们需要的事件。

不管事件触发频率多高，一定在事件触发 n 秒后才执行，如果你在一个事件触发的 n 秒内又触发了这个事件，就以新的事件的时间为准，n 秒后才执行，总之，触发完事件 n 秒内不再触发事件，n 秒后再执行。

应用场景

1. 窗口大小变化，只关心最后结果
2. 搜索栏，只关心完成结果
3. 表单验证，延迟后进行验证

为了更好理解，下面提供了最简单的 debounce 实现：返回一个 function，第一次执行这个 function 会启动一个定时器，下一次执行会清除上一次的定时器并重起一个定时器，直到这个 function 不再被调用，定时器成功跑完，执行回调函数。

```js
const debounce = function (func, wait) {
  let timer;
  return function () {
    !!timer && clearTimeout(timer);
    timer = setTimeout(func, wait);
  };
};
```

有时候我们需要让函数立即执行一次，再等后面事件触发后等待 n 秒执行，我们给`debounce`函数一个`flag`用于标示是否立即执行。同时保留上下文和参数。

```js
function debounce(event, time, flag) {
  let timer = null;
  return function (...args) {
    clearTimeout(timer);
    if (flag && !timer) {
      event.apply(this, args);
    }
    timer = setTimeout(() => {
      event.apply(this, args);
    }, time);
  };
}
```

## 节流（throttle）

节流让指定函数在规定的时间里执行次数不会超过一次，也就是说，在连续高频执行中，动作会被定期执行。节流的主要目的是将原本操作的频率降低。

不管事件触发频率多高，只在单位时间内执行一次。有两种方式可以实现节流，使用时间戳和定时器。

1. 时间戳实现。第一次事件肯定触发，最后一次不会触发。

```js
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

2. 定时器实现。第一次事件不会触发，最后一次一定触发。

```js
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

3. 定时器和时间戳的结合版，也相当于节流和防抖的结合版，第一次和最后一次都会触发。

```js
function throttle(event, time) {
  let pre = 0;
  let timer = null;
  return function (...args) {
    if (Date.now() - pre > time) {
      // 时间戳 首次执行
      clearTimeout(timer);
      timer = null;
      pre = Date.now();
      event.apply(this, args);
    } else if (!timer) {
      // 定时器 最后一次执行
      timer = setTimeout(() => {
        event.apply(this, args);
      }, time);
    }
  };
}
```

## requestAnimationFrame（rAF）

rAF 在一定程度上和 `throttle(func, 16)` 的作用相似，但它是浏览器自带的 api，所以，它比 throttle 函数执行得更加平滑。调用 `window.requestAnimationFrame()`，浏览器会在下次刷新的时候执行指定回调函数。通常，屏幕的刷新频率是 60hz，所以，这个函数也就是大约 16.7ms 执行一次。如果你想让你的动画更加平滑，用 rAF 就再好不过了，因为它是跟着屏幕的刷新频率来的。

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

- 循环递归的基本实现
- 使用reduce简化循环
- ES6扩展运算符循环
- 字符串toString方法
- 字符串JSON过滤

基本实现。循环数组元素，如果还是一个数组，就递归调用该方法。

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
}
```

使用reduce简化

```js
function flatten(array) {
  return array.reduce(
    (target, current) =>
      Array.isArray(current) ?
        target.concat(flatten(current)) :
        target.concat(current)
    , [])
}
```

ES6 增加了扩展运算符，用于取出参数对象的所有可遍历属性，拷贝到当前对象之中。

```js
function flatten(arr) {
  while (arr.some(item => Array.isArray(item))) {
    arr = [].concat(...arr);
  }
  return arr;
}
```

如果数组的元素都是数字或都是字符串，那么我们可以考虑使用 toString 方法，因为：调用 toString 方法，返回了一个逗号分隔的扁平的字符串。然而这种方法使用的场景却非常有限，如果数组是 [1, '1', 2, '2'] 的话，这种方法就会产生错误的结果。

```js
function flatten(arr) {
  return arr.toString().split(',').map(() => +item)
}
```

字符串过滤。将输入数组转换为字符串并删除所有括号（[]）并将输出解析为数组。

```js
const flatten = arr => {
  let re = /\[|\]/g;
  let str = JSON.stringify(arr).replace(re, '');
  return JSON.parse(`[${str}]`);
}
```

# 数组最值

- 直接循环求最值
- 使用reduce简化
- Math.max接收合适参数
- 数组排序方法sort

最最原始的方法，莫过于循环遍历一遍：

```js
var result = arr[0];
for (var i = 1; i < arr.length; i++) {
    result =  Math.max(result, arr[i]);
}
```

既然是通过遍历数组求出一个最终值，那么我们就可以使用 reduce 方法。

```js
array.reduce((c, n) => Math.max(c, n))
```

`Math.max`参数原本是一组数字，只需要让他可以接收数组即可。

```js
const array = [3,2,1,4,5];
Math.max.apply(null, array);
// 或者
// Math.max(...array);
```

如果我们先对数组进行一次排序，那么最大值就是最后一个值：

```js
arr.sort(function (a, b) {
  return a - b;
});
arr[arr.length - 1]
```

# 函数柯里化

在数学和计算机科学中，柯里化是一种将使用多个参数的一个函数转换成一系列使用一个参数的函数的技术。通俗易懂的解释：用闭包把参数保存起来，当参数的数量足够执行函数了，就开始执行函数。

判断当前函数传入的参数是否大于或等于`fn`需要参数的数量，如果是，直接执行`fn`。如果传入参数数量不够，返回一个闭包，暂存传入的参数，并重新返回`currying`函数。

实际应用
- 延迟计算：部分求和、bind 函数
- 动态创建函数：添加监听 addEvent、惰性函数
- 参数复用

```js
function currying(fn, length) {
  length = length || fn.length; 	
  return function (...args) {			
    return args.length >= length	
    	? fn.apply(this, args)			
      : currying(fn.bind(this, ...args), length - args.length) 
  }
}
```

ES6 极简写法，更加简洁也更加易懂。

```js
function currying(fn, ...args) {
  if (args.length >= fn.length) {
    return fn(...args);
  } else {
    return (...args2) => currying(fn, ...args, ...args2);
  }
}
```

# 模拟实现call

`call()` 方法使用一个指定的 this 值和单独给出的一个或多个参数来调用一个函数。

- 允许为不同的对象分配和调用属于一个对象的函数/方法。
- 提供新的 this 值给当前调用的函数/方法。可以使用 call 来实现继承。

处理步骤：
1. 判断当前`this`是否为函数，防止` Function.prototype.myCall()` 直接调用
2. `context` 为可选参数，如果不传的话默认上下文为 `window`
3. 为`context` 创建一个 `Symbol`（保证不会重名）属性，将当前函数赋值给这个属性
4. 处理参数，传入第一个参数后的其余参数
4. 调用函数后即删除该`Symbol`属性

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
}
```

call 是 ES3 的方法，展开运算符是 ES6 的功能。所以用 eval 方法拼成一个函数。这里 args 会自动调用 `Array.toString()` 这个方法。

```js
var args = [];
  for(var i = 1, len = arguments.length; i < len; i++) {
      args.push('arguments[' + i + ']');
  }
  var result = eval('context.fn(' + args +')');
```

# 模拟实现apply

`apply`实现类似`call`，参数为数组

```js
Function.prototype.myApply = function (context = window, args) {
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
}
```

# 模拟实现bind

bind() 方法会创建一个新函数，当这个新函数被调用时，它的 this 值是传递给 bind() 的第一个参数，传入bind方法的第二个以及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数。bind返回的绑定函数也能使用 new 操作符创建对象：这种行为就像把原函数当成构造器，提供的 this 值被忽略，同时调用时的参数被提供给模拟函数。

处理步骤：
1. 处理参数，返回一个闭包
2. 判断是否为构造函数调用，如果是则使用`new`调用当前函数
3. 如果不是，使用`apply`，将`context`和处理好的参数传入

```js
Function.prototype.myBind = function (context, ...args1) {
  if (this === Function.prototype) {
    throw new TypeError('Error')
  }
  const _this = this
  return function F(...args2) {
    // 判断是否用于构造函数
    if (this instanceof F) {
      return new _this(...args1, ...args2)
    }
    return _this.apply(context, args1.concat(args2))
  }
}
```

兼容到ES5版本。

```js
Function.prototype.bind2 = function (context) {

    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    // 用一个空对象作为中介
    // 把 fBound.prototype 赋值为空对象的实例
    // 原型式继承
    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
}
```

# 模拟实现instanceof

instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上。

原型与原型链（prototype chain）关系
- 函数的`prototype`属性指向了一个对象，这个对象正是调用该构造函数而创建的实例的原型
- 每一个JavaScript对象（除了 null ）都具有的一个属性，叫`__proto__`，这个属性会指向该对象的原型
- 每个原型都有一个`constructor`属性指向关联的构造函数，实例也可以继承该属性

```js
function Car(make, model, year) {
  this.make = make; 
  this.model = model;
  this.year = year;
}
const auto = new Car('Honda', 'Accord', 1998);

console.log(auto instanceof Car);  // true
console.log(auto instanceof Object);  // true
```

实现

```js
function myInstanceof(target, origin) {
  const proto = target.__proto__;
  if (proto) {
    if (origin.prototype === proto) {
      return true;
    } else {
      return myInstanceof(proto, origin)
    }
  } else {
    return false;
  }
}
```

# 模拟实现new

new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。new 关键字会进行如下的操作：

- 创建一个空的简单JavaScript对象（即{}）；
- 链接该对象（即设置该对象的构造函数）到另一个对象 ；
- 将步骤1新创建的对象作为this的上下文 ；
- 如果该函数没有返回对象，则返回this。

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
};
```

```js
function create(Con, ...args) {
  let obj = {}
  Object.setPrototypeOf(obj, Con.prototype)
  let result = Con.apply(obj, args)
  return result instanceof Object ? result : obj
}
```

# 模拟实现Promise

## 基础版本

- 设定三个状态 `PENDING、FULFILLED、REJECTED` ，只能由`PENDING`改变为`FULFILLED、REJECTED`，并且只能改变一次
- `MyPromise`接收一个函数`executor`，`executor`有两个参数`resolve`方法和`reject`方法
- `resolve`将`PENDING`改变为`FULFILLED`
- `reject`将`PENDING`改变为`FULFILLED`
- `promise`变为`FULFILLED`状态后具有一个唯一的`value`
- `promise`变为`REJECTED`状态后具有一个唯一的`reason`

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
  }

  const reject = (reason) => {
    if (this.state === PENDING) {
      this.state = REJECTED;
      this.reason = reason;
    }
  }

  try {
    executor(resolve, reject);
  } catch (reason) {
    reject(reason);
  }
}
```

## then方法

- `then`方法接受两个参数`onFulfilled、onRejected`，它们分别在状态由`PENDING`改变为`FULFILLED、REJECTED`后调用
- 一个`promise`可绑定多个`then`方法
- `then`方法可以同步调用也可以异步调用
- 同步调用：状态已经改变，直接调用`onFulfilled`方法
- 异步调用：状态还是`PENDING`，将`onFulfilled、onRejected`分别加入两个函数数组`onFulfilledCallbacks、onRejectedCallbacks`，当异步调用`resolve`和`reject`时，将两个数组中绑定的事件循环执行。

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
      this.onFulfilledCallbacks.forEach(fun => {
        fun();
      });
    }
  }

  const reject = (reason) => {
    if (this.state === PENDING) {
      this.state = REJECTED;
      this.reason = reason;
      this.onRejectedCallbacks.forEach(fun => {
        fun();
      });
    }
  }

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
      })
      this.onRejectedCallbacks.push(() => {
        onRejected(this.reason);
      })
      break;
  }
}
```

### then方法异步调用

如下面的代码：输入顺序是：`1、2、ConardLi`

```js
console.log(1);

let promise = new Promise((resolve, reject) => {
  resolve('ConardLi');
});

promise.then((value) => {
  console.log(value);
});

console.log(2);
```

虽然`resolve`是同步执行的，我们必须保证`then`是异步调用的，我们用`setTimeout`来模拟异步调用（并不能实现微任务和宏任务的执行机制，只是保证异步调用）

```js
MyPromise.prototype.then = function (onFulfilled, onRejected) {
  if (typeof onFulfilled != 'function') {
    onFulfilled = function (value) {
      return value;
    }
  }
  if (typeof onRejected != 'function') {
    onRejected = function (reason) {
      throw reason;
    }
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
      })
      this.onRejectedCallbacks.push(() => {
        setTimeout(() => {
          onRejected(this.reason);
        }, 0);
      })
      break;
  }
}
```

### then方法链式调用

保证链式调用，即`then`方法中要返回一个新的`promise`，并将`then`方法的返回值进行`resolve`。

> 注意：这种实现并不能保证`then`方法中返回一个新的`promise`，只能保证链式调用。

```js
MyPromise.prototype.then = function (onFulfilled, onRejected) {
  if (typeof onFulfilled != 'function') {
    onFulfilled = function (value) {
      return value;
    }
  }
  if (typeof onRejected != 'function') {
    onRejected = function (reason) {
      throw reason;
    }
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
        })
        this.onRejectedCallbacks.push(() => {
          setTimeout(() => {
            try {
              const x = onRejected(this.reason);
              resolve(x);
            } catch (reason) {
              reject(reason);
            }
          }, 0);
        })
        break;
    }
  })
  return promise2;
}
```

## catch方法

若上面没有定义`reject`方法，所有的异常会走向`catch`方法：

```js
MyPromise.prototype.catch = function(onRejected) {
  return this.then(null, onRejected);
};
```

## finally方法

不管是`resolve`还是`reject`都会调用`finally`。

```js
MyPromise.prototype.finally = function(fn) {
  return this.then(value => {
      fn();
      return value;
  }, reason => {
      fn();
      throw reason;
  });
};
```

## Promise.resolve

`Promise.resolve`用来生成一个直接处于`FULFILLED`状态的Promise。

```js
MyPromise.reject = function(value) {
  return new MyPromise((resolve, reject) => {
    resolve(value);
  });
};
```

## Promise.reject

`Promise.reject`用来生成一个直接处于`REJECTED`状态的Promise。

```js
MyPromise.reject = function(reason) {
  return new MyPromise((resolve, reject) => {
    reject(reason);
  });
};
```

## all方法

接受一个`promise`数组，当所有`promise`状态`resolve`后，执行`resolve`

```js
MyPromise.all = function (promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      resolve([]);
    } else {
      let result = [];
      let index = 0;
      for (let i = 0; i < promises.length; i++) {
        promises[i].then(data => {
          result[i] = data;
          if (++index === promises.length) {
            resolve(result);
          }
        }, err => {
          reject(err);
          return;
        });
      }
    }
  });
}
```

## race方法

接受一个`promise`数组，当有一个`promise`状态`resolve`后，执行`resolve`

```js
MyPromise.race = function (promises) {
  return new Promise((resolve, reject) => {
    if (promises.length === 0) {
      resolve();
    } else {
      let index = 0;
      for (let i = 0; i < promises.length; i++) {
        promises[i].then(data => {
          resolve(data);
        }, err => {
          reject(err);
          return;
        });
      }
    }
  });
}
```


# 手动实现JSONP

1. 将传入的data数据转化为url字符串形式
2. 处理url中的回调函数
3. 创建一个script标签并插入到页面中 
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
