> 自己总结的 JavaScript 面试题  
> [参考-冴羽博客](https://github.com/mqyqingfeng/Blog/tree/master/articles)   
> [参考-后盾人](http://houdunren.gitee.io/note/js/1%20%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86.html)
> [参考-木易杨](https://github.com/yygmind/blog)

# 深浅拷贝

如果数组元素是基本类型，就会拷贝一份，互不影响，而如果是对象或者数组，就会只拷贝对象和数组的引用，这样我们无论在新旧数组进行了修改，两者都会发生变化。我们把这种复制引用的拷贝方法称之为浅拷贝，与之对应的就是深拷贝，深拷贝就是指完全的拷贝一个对象，即使嵌套了对象，两者也相互分离，修改一个对象的属性，也不会影响另一个。

浅拷贝

1. slice、concat
2. for/in
3. Object.assign
4. 展开语法 Spread syntax

如果是数组，我们可以利用数组的一些方法比如：slice、concat 返回一个新数组的特性来实现拷贝。

```js
var arr = ["old", 1, true, null, undefined];
var new_arr = arr.concat();
// 或者
// var new_arr = arr.slice();
new_arr[0] = "new";
console.log(arr); // ["old", 1, true, null, undefined]
console.log(new_arr); // ["new", 1, true, null, undefined]
```

使用 for/in 执行对象拷贝。遍历对象，然后把属性和属性值都放在一个新的对象中。

```js
var shallowCopy = function (obj) {
  if (typeof obj !== "object") return;
  var newObj = obj instanceof Array ? [] : {};
  for (var key in obj) {
    if (obj.hasOwnProperty(key)) {
      newObj[key] = obj[key];
    }
  }
  return newObj;
};
```

Object.assign 函数可简单的实现浅拷贝，它是将两个对象的属性叠加后面对象属性会覆盖前面对象同名属性。

```js
let user = { name: "后盾人" };
let hd = Object.assign({}, user);
hd.name = "hdcms";
console.log(user.name); //后盾人
```

使用展示语法也可以实现浅拷贝。

```js
let obj = { name: "后盾人" };
let hd = { ...obj };
hd.name = "hdcms";
console.log(hd);
console.log(obj);
```

深拷贝

1. JSON序列化和解析
2. 递归for/of

那如何深拷贝一个数组呢？这里介绍一个技巧，不仅适用于数组还适用于对象！但是该方法有以下几个问题。
- 会忽略 undefined
- 会忽略 symbol
- 不能序列化函数
- 不能解决循环引用的对象
- 不能正确处理`new Date()`
- 不能处理正则

```js
var arr = ["old", 1, true, ["old1", "old2"], { old: 1 }];
var new_arr = JSON.parse(JSON.stringify(arr));
console.log(new_arr);
```

在拷贝的时候判断一下属性值的类型，如果是对象，我们递归调用深拷贝函数。

```js
var deepCopy = function (obj) {
  if (typeof obj !== "object") return obj;
  var newObj = obj instanceof Array ? [] : {};
  for (const [k, v] of Object.entries(obj)) {
    newObj[k] = deepCopy(v);
  }
  return newObj;
};
```

尽管使用深拷贝会完全的克隆一个新对象，不会产生副作用，但是深拷贝因为使用递归，性能会不如浅拷贝，在开发中，还是要根据实际情况进行选择。

我们知道 JSON 无法深拷贝循环引用，遇到这种情况会抛出异常。解决方案很简单，其实就是循环检测，我们设置一个数组或者哈希表存储已拷贝过的对象，当检测到当前对象已存在于哈希表中时，取出该值并返回即可。也可以使用了 ES6 中的 WeakMap 来处理。

# 函数节流和防抖

节流（`throttle`）:不管事件触发频率多高，只在单位时间内执行一次。有两种方式可以实现节流，使用时间戳和定时器。防抖（`debounce`）：不管事件触发频率多高，一定在事件触发`n`秒后才执行，如果你在一个事件触发的 `n` 秒内又触发了这个事件，就以新的事件的时间为准，`n`秒后才执行，总之，触发完事件 `n` 秒内不再触发事件，`n`秒后再执行。

节流

1. 时间戳实现
2. 定时器实现
3. 时间戳/定时器结合

时间戳实现。第一次事件肯定触发，最后一次不会触发

```js
function throttle(event, time) {
  let pre = 0;
  return function (...args) {
  if (Date.now() - pre > time) {
    pre = Date.now();
    event.apply(this, args);
  }
  }
```

定时器实现。第一次事件不会触发，最后一次一定触发

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

定时器和时间戳的结合版，也相当于节流和防抖的结合版，第一次和最后一次都会触发

```js
function throttle(event, time) {
  let pre = 0;
  let timer = null;
  return function (...args) {
    if (Date.now() - pre > time) {
      clearTimeout(timer);
      timer = null;
      pre = Date.now();
      event.apply(this, args);
    } else if (!timer) {
      timer = setTimeout(() => {
        event.apply(this, args);
      }, time);
    }
  };
}
```


防抖应用场景  
- 窗口大小变化，调整样式`window.addEventListener('resize', debounce(handleResize, 200));`
- 搜索框，输入后 300 毫秒搜索`debounce(fetchSelectData, 300);`
- 表单验证，输入 1000 毫秒后验证`debounce(validator, 1000);`

```js
function debounce(event, time) {
  let timer = null;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => {
      event.apply(this, args);
    }, time);
  };
}
```

有时候我们需要让函数立即执行一次，再等后面事件触发后等待`n`秒执行，我们给`debounce`函数一个`flag`用于标示是否立即执行。

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

# 数组去重

- 双层循环
- 开辟存储对象
- indexOf + filter
- Set
- 排序
- 去除重复值

最原始的方法的双层循环

```js
function unique(array) {
  var res = [];
  for (var i = 0, arrayLen = array.length; i < arrayLen; i++) {
    // 第二层遍历
    for (var j = 0, resLen = res.length; j < resLen; j++ ) {
      if (array[i] === res[j]) {
          break;
      }
    }
    if (j === resLen) {
      res.push(array[i])
    }
    // 用 indexOf 简化内层的循环
    // var current = array[i];
    // if (res.indexOf(current) === -1) {
    //   res.push(current)
    // }
  }
  return res;
}
```

开辟一个外部存储空间用于标示元素是否出现过。

```js
const unique = (array)=> {
  var container = {};
  return array.filter((item, index) => {
    return container.hasOwnProperty(item) ? false : (container[item] = true)
  });
}
```

indexOf + filter

```js
const unique = arr => arr.filter((e,i) => arr.indexOf(e) === i);
```

Set

```js
const unique = arr => Array.from(new Set(arr));
// 或者
// const unique = arr => [...new Set(arr)];
```

Map

```js
function unique (arr) {
    const seen = new Map()
    return arr.filter((a) => !seen.has(a) && seen.set(a, 1))
}
```

排序后去重。

```js
const unique = (array) => {
  array.sort((a, b) => a - b);
  let pre = 0;
  const result = [];
  for (let i = 0; i < array.length; i++) {
    if (!i || array[i] != array[pre]) {
      result.push(array[i]);
    }
    pre = i;
  }
  return result;
}
```

不同于上面的去重，这里是只要数字出现了重复次，就将其移除掉。

```js
const filterNonUnique = arr => arr.filter(i => 
  arr.indexOf(i) === arr.lastIndexOf(i)
)
```

# 数组扁平化
# 函数柯里化
