> 自己总结的 JavaScript 面试题
> [参考-冴羽博客](https://github.com/mqyqingfeng/Blog/tree/master/articles) > [参考-后盾人](http://houdunren.gitee.io/note/js/1%20%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86.html)

# 深浅拷贝

浅拷贝

如果是数组，我们可以利用数组的一些方法比如：slice、concat 返回一个新数组的特性来实现拷贝。如果数组元素是基本类型，就会拷贝一份，互不影响，而如果是对象或者数组，就会只拷贝对象和数组的引用，这样我们无论在新旧数组进行了修改，两者都会发生变化。我们把这种复制引用的拷贝方法称之为浅拷贝，与之对应的就是深拷贝，深拷贝就是指完全的拷贝一个对象，即使嵌套了对象，两者也相互分离，修改一个对象的属性，也不会影响另一个。所以我们可以看出使用 concat 和 slice 是一种浅拷贝。

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

那如何深拷贝一个数组呢？这里介绍一个技巧，不仅适用于数组还适用于对象！这是一个简单粗暴的好方法，就是有一个问题，不能拷贝函数。因为在序列化 JavaScript 对象时，所有函数和原型成员会被有意忽略。

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

# 函数节流和防抖

节流（`throttle`）:不管事件触发频率多高，只在单位时间内执行一次。有两种方式可以实现节流，使用时间戳和定时器。

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

防抖（`debounce`）：不管事件触发频率多高，一定在事件触发`n`秒后才执行，如果你在一个事件触发的 `n` 秒内又触发了这个事件，就以新的事件的时间为准，`n`秒后才执行，总之，触发完事件 `n` 秒内不再触发事件，`n`秒后再执行。

应用场景

1. 窗口大小变化，调整样式`window.addEventListener('resize', debounce(handleResize, 200));`

2. 搜索框，输入后 300 毫秒搜索`debounce(fetchSelectData, 300);`

3. 表单验证，输入 1000 毫秒后验证`debounce(validator, 1000);`

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

# 函数柯里化
