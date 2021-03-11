[niubility-coding-js](https://github.com/LinDaiDai/niubility-coding-js)

# 函数关键字 this

引用 `this` 的 5 种绑定方式：

1. 默认绑定。非严格模式下`this`指向全局对象, 严格模式下会绑定到`undefined`
2. 隐式绑定。当函数引用有上下文对象时, 如 `obj.foo()`的调用方式, `foo`内的`this`指向`obj`
3. 显示绑定。可通过`call()`等方法直接指定`this`的绑定对象
4. 关键字 new 绑定。当一个函数用作构造函数时，它的`this`被绑定到正在构造的新对象
5. 箭头函数绑定。`this`的指向由外层作用域决定的

## 1. 默认绑定

默认绑定也就是我们常说的：在非严格模式下`this`指向的是全局对象`window`，而在严格模式下会绑定到`undefined`。

**1.1 题目一**

老规矩，来看个最基本的案例：

```javascript
var a = 10;
function foo() {
  console.log(this.a);
}
foo();
```

我们知道在使用`var`创建变量的时候（不在函数里），会把创建的变量绑定到`window`上，所以此时`a`是`window`下的属性。

而函数`foo`也是`window`下的属性。

因此上面的代码其实就相当于是这样:

```javascript
window.a = 10;
function foo() {
  console.log(this.a);
}
window.foo();
```

在这里，调用`foo()`函数的是`window`对象，且又是在非严格模式下，所以`foo()`中`this`的指向是`window`对象，因此`this.a`会输出`10`。

答案：

```
10
```

**1.2 题目二**

改造下题目一，看看在严格模式下。

```javascript
'use strict';
var a = 10;
function foo() {
  console.log('this1', this);
  console.log(window.a);
  console.log(this.a);
}
console.log(window.foo);
console.log('this2', this);
foo();
```

需要注意的点：

- 开启了严格模式，只是说使得函数内的`this`指向`undefined`，它并不会改变全局中`this`的指向。因此`this1`中打印的是`undefined`，而`this2`还是`window`对象。
- 另外，它也不会阻止`a`被绑定到`window`对象上。

所以最后的执行结果：

```
f foo() {...}
'this2' Window{...}
'this1' undefined
10
Uncaught TypeError: Cannot read property 'a' of undefined
```

**1.3 题目三**

```javascript
let a = 10;
const b = 20;

function foo() {
  console.log(this.a);
  console.log(this.b);
}
foo();
console.log(window.a);
```

如果把`var`改成了`let` 或者 `const`，变量是不会被绑定到`window`上的，所以此时会打印出三个`undefined`。

答案：

```
undefined
undefined
undefined
```

**1.4 题目四**

```javascript
var a = 1;
function foo() {
  var a = 2;
  console.log(this);
  console.log(this.a);
}

foo();
```

这里我们很容易就知道，`foo()`函数内的`this`指向的是`window`，因为是`window`调用的`foo`。

但是打印出的`this.a`呢？注意，是`this.a`，不是`a`，因此是`window`下的`a`。

并且由于函数作用域的原因我们知道`window`下的`a`还是`1`。

因此答案为：

```
Window{...}
1
```

**1.5 题目五**

把题目`1.4`改造一下。

```javascript
var a = 1;
function foo() {
  var a = 2;
  function inner() {
    console.log(this.a);
  }
  inner();
}

foo();
```

其实这里和`1.4`很像，不过一看到函数内的函数，就很容易让人联想到闭包，然后... 然后就脱口而出，答案是`2`啊，这还不简单。

小伙伴们，审题可得仔细啊，这里问你的是`this.a`，而在`inner`中，`this`指向的还是`window`。

答案：

```
1
```

## 2. 隐式绑定

隐式绑定，this 永远指向最后调用它的那个对象。谁最后调用的函数，函数内的`this`指向的就是谁（不考虑箭头函数）。这与上下文对象以及作用域有关。

下面你可以用这个规则来做题啦。

**2.1 题目一**

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1, foo };
var a = 2;
obj.foo();
```

在这道题中，函数`foo()`虽然是定义在`window`下，但是我在`obj`对象中引用了它，并将它重新赋值到`obj.foo`上。

且调用它的是`obj`对象，因此打印出来的`this.a`应该是`obj`中的`a`。

换个角度想，上面这段代码是不是就相当于是这样：

```javascript
var obj = {
  a: 1,
  foo: function () {
    console.log(this.a);
  },
};
var a = 2;
obj.foo();
```

在这里`foo`函数内的`this`指向的就是`obj`，和题目效果一样。

答案都是：

```
1
```

有小伙伴就会有有疑问了，`obj.foo()`不就相当于是`window.obj.foo()`吗？

那`foo()`内的`this`到底是算`window`呢，还是`obj`呢？

请注意我前面说的，是最后调用函数的对象，显然，`obj`要比`window`更后面一点。

## 3. 隐式绑定的隐式丢失问题

隐式丢失其实就是被隐式绑定的函数在特定的情况下会丢失绑定对象。有两种情况容易发生隐式丢失问题：

- 使用另一个变量来给函数取别名
- 将函数作为参数传递时会被隐式赋值，回调函数丢失 this 绑定

**3.1 题目一**

使用另一个变量来给函数取别名会发生隐式丢失。

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1, foo };
var a = 2;
var foo2 = obj.foo;

obj.foo();
foo2();
```

在这里我们已经知道了，`obj.foo()`中`this`的指向是为`obj`的，所以`obj.foo()`执行的时候，打印出来的是`obj`对象中的`a`，也就是`1`。

但是`foo2`它不也是`obj.foo`吗？我只不过是用了一个变量`foo2`来盛放了它而已。所以你是不是认为它打印的也是`1`呢？

额，其实这里不是的，它打印出的是`window`下的`a`。

答案：

```
1
2
```

这是因为虽然`foo2`指向的是`obj.foo`函数，不过调用它的却是`window`对象，所以它里面`this`的指向是为`window`。

其实也就相当于是`window.foo2()`，如果你不相信的话，可以看下面一题。

**3.2 题目二**

让我们在一个新的变量`obj2`中也定义一个`foo2`看看：

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1, foo };
var a = 2;
var foo2 = obj.foo;
var obj2 = { a: 3, foo2: obj.foo };

obj.foo();
foo2();
obj2.foo2();
```

这三种不同的`foo()`打印出来的分别是什么呢？

答案：

```
1
2
3
```

- `obj.foo()`中的`this`指向调用者`obj`
- `foo2()`发生了隐式丢失，调用者是`window`，使得`foo()`中的`this`指向`window`
- `foo3()`发生了隐式丢失，调用者是`obj2`，使得`foo()`中的`this`指向`obj2`

**3.3 题目三**

再就是如果你把一个函数当成参数传递时，也会被隐式赋值，发生意想不到的问题。

来看看这道题目：

```javascript
function foo() {
  console.log(this.a);
}
function doFoo(fn) {
  console.log(this);
  fn();
}
var obj = { a: 1, foo };
var a = 2;
doFoo(obj.foo);
```

这里我们将`obj.foo`当成参数传递到`doFoo`函数中，在传递的过程中，`obj.foo()`函数内的`this`发生了改变，指向了`window`。

因此结果为：

```
Window{...}
2
```

注意，我这里说的是`obj.foo()`函数，而不是说`doFoo()`。`doFoo()`函数内的`this`本来就是指向`window`的，因为这里是`window`调用的它。

但是你不要以为是`doFoo()`函数内的`this`影响了`obj.foo()`，不信你看下一题。

**3.4 题目四**

现在我们不用`window`调用`doFoo`，而是放在对象`obj2`里，用`obj2`调用：

```javascript
function foo() {
  console.log(this.a);
}
function doFoo(fn) {
  console.log(this);
  fn();
}
var obj = { a: 1, foo };
var a = 2;
var obj2 = { a: 3, doFoo };

obj2.doFoo(obj.foo);
```

现在调用`obj2.doFoo()`函数，里面的`this`指向的应该是`obj2`，因为是`obj2`调用的它。

但是`obj.foo()`打印出来的`a`依然是`2`，也就是`window`下的。

执行结果为：

```
{ a:3, doFoo: f }
2
```

所以说，如果你把一个函数当成参数传递到另一个函数的时候，也会发生隐式丢失的问题，且与包裹着它的函数的 this 指向无关。在非严格模式下，会把该函数的 this 绑定到 window 上，严格模式下绑定到 undefined。

一样的代码，试试严格模式下：

```javascript
'use strict';
function foo() {
  console.log(this.a);
}
function doFoo(fn) {
  console.log(this);
  fn();
}
var obj = { a: 1, foo };
var a = 2;
var obj2 = { a: 3, doFoo };

obj2.doFoo(obj.foo);
```

执行结果：

```
{ a:3, doFoo: f }
Uncaught TypeError: Cannot read property 'a' of undefined
```

## 4. 显式绑定

功能如其名，就是强行使用某些方法，改变函数内`this`的指向。

通过`call()、apply()`或者`bind()`方法直接指定`this`的绑定对象, 如`foo.call(obj)`。

这里有几个知识点需要注意：

- 使用`call()`或者`apply()`的函数是会直接执行的
- `bind()`是创建一个新的函数，需要手动调用才会执行
- `call()`和`apply()`用法基本类似，不过`call`接收若干个参数，而`apply`接收的是一个数组

来看看题目一。

**4.1 题目一**

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1 };
var a = 2;

foo();
foo.call(obj);
foo.apply(obj);
foo.bind(obj);
```

第一个`foo()` 都很好理解，这不就是默认绑定吗？

而第二个和第三个`foo`都使用了`call`或`apply`来改变`this`的指向，并且是立即执行的。

第四个`foo`，仅仅是使用`bind`创建了一个新的函数，且这个新函数也没用别的变量接收并调用，因此并不会执行。

答案：

```
2
1
1
```

这里想要提一嘴，如果`call、apply、bind`接收到的第一个参数是空或者`null、undefined`的话，则会忽略这个参数。

例如：

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
foo.call();
foo.call(null);
foo.call(undefined);
```

输出的是：

```
2
2
2
```

**4.2 题目二**

了解了显式绑定的基本使用之后，让我们来看看它的妙用。

首先，是这个例子：

```javascript
var obj1 = {
  a: 1,
};
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    setTimeout(function () {
      console.log(this);
      console.log(this.a);
    }, 0);
  },
};
var a = 3;

obj2.foo1();
obj2.foo2();
```

对于`obj2.foo1()`，我们很清楚，它就是打印出`2`。

但是对于`obj2.foo2`呢？在这个函数里，设置了一个定时器，并要求我们打印出`this`和`this.a`。

想想我前面说过的话，谁调用的函数，函数内的`this`指向的就是谁。

而对于匿名函数，它里面的`this`在非严格模式下始终指向的都是`window`。

所以最终的结果是：

```
2
Window{...}
3
```

**4.3 题目三**

面对上面这种情况我们就可以使用`call、apply` 或者`bind`来改变函数中`this`的指向，使它绑定到`obj1`上，从而打印出`1`。

```javascript
var obj1 = {
  a: 1,
};
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    setTimeout(
      function () {
        console.log(this);
        console.log(this.a);
      }.call(obj1),
      0
    );
  },
};
var a = 3;
obj2.foo1();
obj2.foo2();
```

现在的执行结果就是：

```
2
{ a: 1 }
1
```

但是看看我这里的写法，我是将`.call`运用到`setTimeout`里的回调函数上，并不是运用到`obj2.foo2()`上。

所以有小伙伴就会问了，我下面的这种写法不可以吗？

```javascript
obj2.foo2.call(obj1);
```

注意：如果是这种写法的话，我改变的就是`foo2`函数内的`this`的指向了，但是我们知道，`foo2`函数内`this`的指向和`setTimeout`里函数的`this`是没有关系的，因为调用定时器的始终是`window`。

并且这里使用`.bind()`也是可以的，因为定时器里的函数在时间到了之后本就是会自动执行的。

**4.4 题目四**

OK，我们不用定时器，把它干掉，换成一个函数：

```javascript
var obj1 = {
  a: 1,
};
var obj2 = {
  a: 2,
  foo1: function () {
    console.log(this.a);
  },
  foo2: function () {
    function inner() {
      console.log(this);
      console.log(this.a);
    }
    inner();
  },
};
var a = 3;
obj2.foo1();
obj2.foo2();
```

其实这里有点像题目`1.5`有木有，都是函数内包裹着函数。

调用`inner`函数的依然是`window`，所以结果为：

```
2
Window{...}
3
```

如果给`inner()`函数显式绑定的话：

```javascript
inner.call(obj1);
```

结果为

```
2
{ a: 1 }
1
```

**4.5 题目五**

其实在实际面试中，面试官喜欢以这样的方式考你：

看看这道题，会输出什么呢 ？

```javascript
function foo() {
  console.log(this.a);
}
var obj = { a: 1 };
var a = 2;

foo();
foo.call(obj);
foo().call(obj);
```

也就是使用`.call()`方法位置的不同。

结果：

```
2
1
2
Uncaught TypeError: Cannot read property 'call' of undefined
```

- `foo()`会正常打印出`window`下的`a`，也就是`2`
- `foo.call(obj)`由于显式绑定了`this`，所以会打印出`obj`下的`a`，也就是`1`
- `foo().call(obj)`开始会执行`foo()`函数，打印出`2`，但是会对`foo()`函数的返回值执行`.call(obj)`操作，可是我们可以看到`foo()`函数的返回值是`undefined`，因此就会报错了。

所以我们可以看到`foo.call()`和`foo().call()`的区别了，一个是针对于函数，一个是针对于函数的返回值。

下面我会用更多的例题来帮助大家了解这类题目的解法。

**4.6 题目六**

OK，既然刚刚`4.5`是因为函数没有返回值才报的错，那我现在给它加上返回值看看：

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = { a: 1 };
var a = 2;

foo();
foo.call(obj);
foo().call(obj);
```

结果是：

```
2
1
2
1
```

- 第一个数字`2`自然是`foo()`输出的，虽然`foo()`函数也返回了一个匿名函数，但是并没有调用它呀，只有写成`foo()()`，这样才算是调用匿名函数。
- 第二个数字`1`是`foo.call(obj)`输出的，由于`.call()`是紧跟着`foo`的，所以改变的是`foo()`内`this`的指向，并且`.call()`是会使函数立即执行的，因此打印出`1`，同理，它也没有调用返回的函数。
- 第三个数字`2`是`foo().call(obj)`先执行`foo()`时打印出来的，此时`foo()`内`this`还是指向`window`。
- 在执行完`foo()`之后，会返回一个匿名函数，并且后面使用了`.call(obj)`来改变这个匿名函数的`this`指向并调用了它，所以输出了`1`。

咦～好像从这道题开始，变得越来越有意思了哈

**4.7 题目七**

想想我们把`call`换成`bind`会怎么样呢？

先来回忆一下它们的区别：`call`是会直接执行函数的，`bind`是返回一个新函数，但不会执行。

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = { a: 1 };
var a = 2;

foo();
foo.bind(obj);
foo().bind(obj);
```

结果自然就是：

```
2
2
```

- `foo()`会执行没错，打印出了`2`。
- 但是`foo.bind(obj)`却不会执行，它返回的是一个新函数。
- `foo().bind(obj)`只会执行前面的`foo()`函数，打印出`2`，`.bind(obj)`只是将`foo()`返回的匿名函数显式绑定`this`而已，并没有调用。

**4.8 题目八**

说实话，做上面这类题目，会让我有一种疑惑。

这种函数内返回的函数，它的`this`会和它外层的函数有关吗？

也就是内层函数它的`this`到底是谁呢？

还是那句话，谁最后调用的它，`this`就指向谁。

```javascript
function foo() {
  console.log(this.a);
  return function () {
    console.log(this.a);
  };
}
var obj = { a: 1 };
var a = 2;

foo.call(obj)();
```

就像是这道题，`foo()`函数内的`this`虽然指定了是为`obj`，但是调用最后调用匿名函数的却是`window`。

所以结果为：

```
1
2
```

（请注意这个例子，后面它会与箭头函数做对比）

**4.9 题目九**

一直都在做函数返回函数的题目，让我们来看看把它们加到对象里，会有哪些有趣的题目吧。

```javascript
var obj = {
  a: 'obj',
  foo: function () {
    console.log('foo:', this.a);
    return function () {
      console.log('inner:', this.a);
    };
  },
};
var a = 'window';
var obj2 = { a: 'obj2' };

obj.foo()();
obj.foo.call(obj2)();
obj.foo().call(obj2);
```

现在，没和你玩文字游戏了，每个`foo`返回的函数我都调用了，但是你能知道每次调用，打印出的都是什么吗？

```
foo: obj
inner: window
foo: obj2
inner: window
foo: obj
inner: obj2
```

**4.10 题目十**

一直做这种题目是不是没意思，让我们加几个参数来玩玩。

```javascript
var obj = {
  a: 1,
  foo: function (b) {
    b = b || this.a;
    return function (c) {
      console.log(this.a + b + c);
    };
  },
};
var a = 2;
var obj2 = { a: 3 };

obj.foo(a).call(obj2, 1);
obj.foo.call(obj2)(1);
```

执行结果：

```
6
6
```

- 开始调用`obj.foo(a)`将`2`传入`foo`函数并赋值给型参`b`，并且由于闭包的原因，使得匿名函数内能访问到`b`，之后调用匿名函数的时候，用`call()`改变了`this`的指向，使得匿名函数内`this.a`为`3`，并传入最后一个参数`1`，所以第一行输出的应该是`3 + 2 + 1`，也就是`6`。
- 而第二行，`obj.foo.call(obj2)`这里是将`foo`函数内的`this`指向了`obj2`，同时并没有传递任何参数，所以`b`开始是`undefined`的，但是又因为有一句`b = b || this.a`，使得`b`变为了`3`；同时最后一段代码`(1)`，是在调用匿名函数，且和这个匿名函数内的`this`应该是指向`window`的，因此输出也为`3+2+1`，为`6`。

## 5. 显式绑定的其它用法

除了上面那几道题的用法之外，我们还可以有一些其它的用法。

例如，我们可以在一个函数内使用`call`来显式绑定某个对象，这样无论怎样调用它，其内部的`this`总是指向这个对象。(可见题目`5.1`)

**5.1 题目一**

```javascript
function foo1() {
  console.log(this.a);
}
var a = 1;
var obj = {
  a: 2,
};

var foo2 = function () {
  foo1.call(obj);
};

foo2();
foo2.call(window);
```

这里`foo2`函数内部的函数`foo1`我们使用`call`来显式绑定`obj`，就算后面再用`call`来绑定`window`也没有用了。

结果为：

```
2
2
```

**5.2 题目二**

```javascript
function foo1(b) {
  console.log(`${this.a} + ${b}`);
  return this.a + b;
}
var a = 1;
var obj = {
  a: 2,
};

var foo2 = function () {
  return foo1.call(obj, ...arguments);
};

var num = foo2(3);
console.log(num);
```

答案：

```
'2 + 3'
5
```

**5.3 题目三**

接下我想要介绍一个比较冷门的知识。

相信大家对`forEach、map、filter`都不陌生吧，它们是`JS`内置的一些函数，但是你知道它们的第二个参数也是能绑定`this`的吗？

来看看下面的题目：

```javascript
function foo(item) {
  console.log(item, this.a);
}
var obj = {
  a: 'obj',
};
var a = 'window';
var arr = [1, 2, 3];

// arr.forEach(foo, obj)
// arr.map(foo, obj)
arr.filter(function (i) {
  console.log(i, this.a);
  return i > 2;
}, obj);
```

这里的答案为：

```
1 "obj"
2 "obj"
3 "obj"
```

如果我们没有传递第二个参数`obj`的话，`this.a`打印出来的肯定就是`window`下的`a`了，但是传入了之后将`obj`显示绑定到第一个参数函数上。

关于`arr.filter`为什么也会打印出`1, 2, 3`，那是因为虽然我们使用了`return i > 2`，不过在执行阶段`filter`还是把每一项都打印出来。

**总结**

总结一下这部分的知识点好了：

- `this` 永远指向最后调用它的那个对象
- 匿名函数的`this`永远指向`window`
- 使用`.call()`或者`.apply()`的函数是会直接执行的
- `bind()`是创建一个新的函数，需要手动调用才会执行
- 如果`call、apply、bind`接收到的第一个参数是空或者`null、undefined`的话，则会忽略这个参数
- `forEach、map、filter`函数的第二个参数也是能显式绑定`this`的

## 6. new 绑定

好滴，让我们来看看另一种`this`的绑定形式，也就是`new`绑定。

使用`new`来调用一个函数，会构造一个新对象并把这个新对象绑定到调用函数中的`this`。

例如第一题。

**6.1 题目一**

使用`new`来调用`Person`，构造了一个新对象`person1`并把它绑定到`Person`调用中的`this`。

```javascript
function Person(name) {
  this.name = name;
}
var name = 'window';
var persion1 = new Person('LinDaiDai');
console.log(person1.name);
```

答案：

```
'LinDaiDai'
```

**6.2 题目二**

构造函数中不仅可以加属性，也可以加方法：

```javascript
function Person(name) {
  this.name = name;
  this.foo1 = function () {
    console.log(this.name);
  };
  this.foo2 = function () {
    return function () {
      console.log(this.name);
    };
  };
}
var person1 = new Person('person1');
person1.foo1();
person1.foo2()();
```

这道题的写法不得不让我想到题目`4.9`：

```javascript
var obj = {
  a: 'obj',
  foo: function () {
    console.log('foo:', this.a);
    return function () {
      console.log('inner:', this.a);
    };
  },
};
```

好像都是函数包裹着函数，没错，其实它们的解法都差不多。

所以这道题的结果为：

```
'person1'
''
```

- 第一个`this.name`打印的肯定是`person1`对象中的`name`，也就是构造`person1`对象时传递进去的`person1`字符串。
- 第二个`this.name`打印的应该就是`window`下的`name`了，但是这里`window`对象中并不存在`name`属性，所以打印出的是空。

在做这道题时，我发现了一个有意思的现象。

我将这道题用浏览器打开，控制台输出的竟然是:

```
'person1'
'window'
```

咦 ？`window`下明明没有`name`这个属性啊，它怎么会打印出`window`，别和我说我电脑的浏览器这么吊...给`window`对象自动加了一个属性值为`window`的`name`属性...

思考了一会，我想起来了，之前我在代码里确实定义了一个变量`name`，`var name = 'window'`。

可是这段代码我已经删掉了啊，并且强制刷新了浏览器，难道它还是存在于`window`中吗？

为了验证我的想法，我又重新定义了一个变量`var name = 'LinDaiDai'`，然后打开浏览器刷新，之后再删除这段代码再刷新。

果然，`window.name`打印出来还是`LinDaiDai`。它会记住这个`name`属性不被回收，直到你关闭此页签。

但是如果把`name`属性名换成别的（比如`dd`），它就不会有这种情况。

有兴趣的小伙伴可以去尝试一下哈，这里我就不深究了...

**6.3 题目三**

使用`new`函数创建的对象和字面量形式创建出来的对象好像没什么大的区别，如果对象中有属性是函数类型的话，并且不是箭头函数，那么解法都一样。在后面说到箭头函数的时候就有区别了，不过我们一步一步来。

先看看下面这道题：

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  this.foo = function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
}
var person2 = {
  name: 'person2',
  foo: function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};

var person1 = new Person('person1');
person1.foo()();
person2.foo()();
```

在这道题中，`person1.foo`和`person2`就没有什么区别。

打印出来的结果为：

```
'person1'
'window'
'person2'
'window'
```

**6.4 题目四**

当`new`绑定结合显示绑定，例如`call`函数的话，解起来其实也不难。

来看看下面的题目。

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  this.foo = function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
}
var person1 = new Person('person1');
var person2 = new Person('person2');

person1.foo.call(person2)();
person1.foo().call(person2);
```

在做这类题的时候，你就把`Person`生成的`person1`脑补成：

```javascript
var person1 = {
  name: 'person1',
  foo: function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};
```

所以答案很容易就出来了：

```
'person2'
'window'
'person1'
'person2'
```

解题分析：

- `person1.foo.call(person2)()`将`foo()`函数内的`this`指向了`person2`，所以打印出`person2`，而内部返回的匿名函数是由`window`调用的，所以打印出`window`。(类似题目`4.9`)
- `person1.foo().call(person2)`是将匿名函数的`this`显式绑定到了`person2`上，所以打印出来的会是`person2`。

## 7. 箭头函数绑定

在上面，我们有学到一个诀窍：this 永远指向最后调用它的那个对象。

但是对于箭头函数就不是这样咯，它里面的`this`是由外层作用域来决定的，且指向函数定义时的 this 而非执行时。

`它里面的this是由外层作用域来决定的`啥意思呢？来看看这句话：

> 箭头函数中没有 this 绑定，必须通过查找作用域链来决定其值，如果箭头函数被非箭头函数包含，则 this 绑定的是最近一层非箭头函数的 this，否则，this 为 undefined。

而`且指向函数定义时的this而非执行时`这句话可以等会看题目`7.4`。

读了这句话相信你已经能解决 80%的题目了，让我们看完了第一题`7.1`之后，再来看看箭头函数可以分为哪几类题目来说吧，这是目录：

- 字面量对象中普通函数与箭头函数的区别: 只有一层函数的题目
- 字面量对象中普通函数与箭头函数的区别：函数嵌套的题目
- 构造函数对象中普通函数和箭头函数的区别：只有一层函数的题目
- 构造函数对象中普通函数和箭头函数的区别：函数嵌套的题目
- 箭头函数结合`.call`的题目

**7.1 题目一**

```javascript
var obj = {
  name: 'obj',
  foo1: () => {
    console.log(this.name);
  },
  foo2: function () {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  },
};
var name = 'window';
obj.foo1();
obj.foo2()();
```

这道题就非常有代表性，它明确了箭头函数内的`this`是由外层作用域决定的。

- 对于`obj.foo1()`函数的调用，它的外层作用域是`window`，对象`obj`当然不属于作用域了（我们知道作用域只有全局作用域`window`和局部作用域函数）。所以会打印出`window`
- `obj.foo2()()`，首先会执行`obj.foo2()`，这不是个箭头函数，所以它里面的`this`是调用它的`obj`对象，因此打印出`obj`，而返回的匿名函数是一个箭头函数，它的`this`由外层作用域决定，那也就是函数`foo2`咯，那也就是它的`this`会和`foo2`函数里的`this`一样，就也打印出了`obj`。

```
window
obj
obj
```

做完了这道题心里是不是有点谱了，感觉也不是那么难嘛...

让我们来拆分一下看看区别。

**7.2 题目二**

**字面量对象中普通函数与箭头函数的区别: 只有一层函数的题目**

```javascript
var name = 'window';
var obj1 = {
  name: 'obj1',
  foo: function () {
    console.log(this.name);
  },
};

var obj2 = {
  name: 'obj2',
  foo: () => {
    console.log(this.name);
  },
};

obj1.foo();
obj2.foo();
```

解题分析：

- 不使用箭头函数的`obj1.foo()`是由`obj1`调用的，所以`this.name`为`obj1`。
- 使用箭头函数的`obj2.foo()`的外层作用域是`window`，所以`this.name`为`window`。

答案：

```
'obj1'
'window'
```

**7.3 题目三**

**字面量对象中普通函数与箭头函数的区别：函数嵌套的题目**

如果用普通函数和箭头函数来做一层嵌套关系的话，一共有四种情况，让我们把每种情况都考虑一遍：

```javascript
var name = 'window';
var obj1 = {
  name: 'obj1',
  foo: function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};
var obj2 = {
  name: 'obj2',
  foo: function () {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  },
};
var obj3 = {
  name: 'obj3',
  foo: () => {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};
var obj4 = {
  name: 'obj4',
  foo: () => {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  },
};

obj1.foo()();
obj2.foo()();
obj3.foo()();
obj4.foo()();
```

解题分析：

- `obj1.foo()()`两层都是普通函数，类似于题目`4.6`，分别打印出`obj1`和`window`。
- `obj2.foo()()`外层为普通函数，内层为箭头，类似于题目`7.1`，都是打印出`obj2`。
- `obj3.foo()()`外层为箭头函数，内层为普通函数，箭头函数的`this`由外层作用域决定，因此为`window`，内层普通函数由调用者决定，调用它的是`window`，因此也为`window`。
- `obj4.foo()()`两层都是箭头函数，第一个箭头函数的`this`由外层作用域决定，因此为`window`，第二个箭头函数的`this`也由外层作用域决定，它的外层作用域是第一个箭头函数，而第一个箭头函数的`this`是`window`，因此内层的`this`也是`window`。

答案：

```
'obj1' 'window'
'obj2' 'obj2'
'window' 'window'
'window' 'window'
```

**7.4 题目四**

**构造函数对象中普通函数和箭头函数的区别：一层函数的题目**

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  this.foo1 = function () {
    console.log(this.name);
  };
  this.foo2 = () => {
    console.log(this.name);
  };
}
var person2 = {
  name: 'person2',
  foo2: () => {
    console.log(this.name);
  },
};
var person1 = new Person('person1');
person1.foo1();
person1.foo2();
person2.foo2();
```

解题思路：

- `person1.foo1()`是个普通函数，this 由最后调用它的对象决定，即`person1`。
- `person1.foo2()`为箭头函数，this 由外层作用域决定，且指向函数定义时的 this 而非执行时，在这里它的外层作用域是函数`Person`，且这个是构造函数，并且使用了`new`来生成了对象`person1`，所以此时`this`的指向是为`person1`。
- `person2.foo2()`字面量创建的的对象`person2`中的`foo2`是个箭头函数，由于`person2`是直接在`window`下创建的，你可以理解为它所在的作用域就是在`window`下，因此`person2.foo2()`内的`this`应该是`window`。

答案：

```
'person1'
'person1'
'window'
```

**7.5 题目五**

**构造函数对象中普通函数和箭头函数的区别：函数嵌套的题目**

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  this.foo1 = function () {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
  this.foo2 = function () {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  };
  this.foo3 = () => {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  };
  this.foo4 = () => {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  };
}
var person1 = new Person('person1');
person1.foo1()();
person1.foo2()();
person1.foo3()();
person1.foo4()();
```

解题分析：

- `person1.foo1()()`两层都是普通函数，这个不再重复说了，打印出`person1`和`window`。(类似题目`6.2`)
- `person1.foo2()()`第一层普通函数，它的`this`是由最后调用它的对象决定也就是`person1`，第二层为箭头函数，它的`this`由外层作用域决定，也就是`foo2`这个函数，因此也为`person1`。
- `person1.foo3()()`第一层为箭头函数，`this`由外层作用域决定，因此为`person1`，第二层为普通函数，由最后调用者决定，因此为`window`。
- `person1.foo4()()`两层都是箭头函数，`this`由外层作用域决定，所以都是`person1`。

答案：

```
'person1' 'window'
'person1' 'person1'
'person1' 'window'
'person1' 'person1'
```

**7.6 题目六**

**箭头函数结合`.call`的题目**

箭头函数的`this`无法通过`bind、call、apply`来直接修改，但是可以通过改变作用域中`this`的指向来间接修改。

```javascript
var name = 'window';
var obj1 = {
  name: 'obj1',
  foo1: function () {
    console.log(this.name);
    return () => {
      console.log(this.name);
    };
  },
  foo2: () => {
    console.log(this.name);
    return function () {
      console.log(this.name);
    };
  },
};
var obj2 = {
  name: 'obj2',
};
obj1.foo1.call(obj2)();
obj1.foo1().call(obj2);
obj1.foo2.call(obj2)();
obj1.foo2().call(obj2);
```

解题分析：

- `obj1.foo1.call(obj2)()`第一层为普通函数，并且通过`.call`改变了`this`指向为`obj2`，所以会打印出`obj2`，第二层为箭头函数，它的`this`和外层作用域中的`this`相同，因此也是`obj2`。
- `obj1.foo().call(obj2)`第一层打印出`obj1`，第二层为箭头函数，使用了`.call`想要修改`this`的指向，但是并不能成功，因此`.call(obj2)`对箭头函数无效，还是打印出`obj1`。
- `obj1.foo2.call(obj2)()`第一层为箭头函数，并且想要通过`.call(obj2)`改变`this`指向，但是无效，且它的外层作用域是`window`，所以会打印出`window`，第二层为普通函数，`this`是最后调用者`window`，所以也会打印出`window`。
- `obj1.foo2().call(obj2)`第一层为箭头函数，外层作用域是`window`，打印出`window`，第二层为普通函数，且使用了`.call(obj2)`来改变`this`指向，所以打印出了`obj2`。

答案：

```
'obj2' 'obj2'
'obj1' 'obj1'
'window' 'window'
'window' 'obj2'
```

在这道题中，`obj1.foo1.call(obj2)()`就相当于是通过改变作用域间接改变箭头函数内`this`的指向。

**总结**

OK，来总结一下箭头函数需要注意的点吧：

- 它里面的`this`是由外层作用域来决定的，且指向函数定义时的`this`而非执行时
- 字面量创建的对象，作用域是`window`，如果里面有箭头函数属性的话，`this`指向的是`window`
- 构造函数创建的对象，作用域是可以理解为是这个构造函数，且这个构造函数的`this`是指向新建的对象的，因此`this`指向这个对象。
- 箭头函数的`this`是无法通过`bind、call、apply`来直接修改，但是可以通过改变作用域中`this`的指向来间接修改。

## 8. 综合题

哈哈哈～

`this`大法已练成，接下来到了我们最喜欢的综合题环节。

让我们来做些难点的题巩固巩固吧！

**8.1 题目一**

字面量对象中的各种场景

```javascript
var name = 'window';
var person1 = {
  name: 'person1',
  foo1: function () {
    console.log(this.name);
  },
  foo2: () => console.log(this.name),
  foo3: function () {
    return function () {
      console.log(this.name);
    };
  },
  foo4: function () {
    return () => {
      console.log(this.name);
    };
  },
};
var person2 = { name: 'person2' };

person1.foo1();
person1.foo1.call(person2);

person1.foo2();
person1.foo2.call(person2);

person1.foo3()();
person1.foo3.call(person2)();
person1.foo3().call(person2);

person1.foo4()();
person1.foo4.call(person2)();
person1.foo4().call(person2);
```

这里我就不写题解了，因为如果你认真看了前面的题目的话，我相信一定能做的来，其实就是将原本分散的知识点汇总在一起。

- `person1.foo1()`类似题目`4.5`
- `person1.foo2()`类似题目`7.1`
- `person1.foo3()`类似题目`7.3`
- `person1.foo4()`类似题目`7.3`

答案：

```
'person1'
'person2'

'window'
'window'

'window'
'window'
'person2'

'person1'
'person2'
'person1'
```

**8.2 题目二**

构造函数中的各种场景

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  (this.foo1 = function () {
    console.log(this.name);
  }),
    (this.foo2 = () => console.log(this.name)),
    (this.foo3 = function () {
      return function () {
        console.log(this.name);
      };
    }),
    (this.foo4 = function () {
      return () => {
        console.log(this.name);
      };
    });
}
var person1 = new Person('person1');
var person2 = new Person('person2');

person1.foo1();
person1.foo1.call(person2);

person1.foo2();
person1.foo2.call(person2);

person1.foo3()();
person1.foo3.call(person2)();
person1.foo3().call(person2);

person1.foo4()();
person1.foo4.call(person2)();
person1.foo4().call(person2);
```

- `person1.foo1()`类似题目`7.4`
- `person1.foo2()`类似题目`7.4`
- `person1.foo3()`类似题目`7.5`
- `person1.foo4()`类似题目`7.5`

答案：

```
'person1'
'person2'

'person1'
'person1'

'window'
'window'
'person2'

'person1'
'person2'
'person1'
```

**8.3 题目三**

```javascript
var name = 'window';
function Person(name) {
  this.name = name;
  this.obj = {
    name: 'obj',
    foo1: function () {
      return function () {
        console.log(this.name);
      };
    },
    foo2: function () {
      return () => {
        console.log(this.name);
      };
    },
  };
}
var person1 = new Person('person1');
var person2 = new Person('person2');

person1.obj.foo1()();
person1.obj.foo1.call(person2)();
person1.obj.foo1().call(person2);

person1.obj.foo2()();
person1.obj.foo2.call(person2)();
person1.obj.foo2().call(person2);
```

这道题还是蛮有意思的，可以仔细说下。

首先是定义了一个构造函数`Person`，不过它与前面几题的区别就是，函数是放在其中的一个叫`obj`的对象里面。

**在这里我提醒一句：this 永远指向最后调用它的那个对象**。

解题分析：

- `person1.obj.foo1()()`返回的是一个普通的匿名函数，调用它的是`window`，所以打印出`window`。
- `person1.obj.foo1.call(person2)()`中是使用`.call(person2)`改变第一层函数中的`this`，匿名函数和它没关系，依旧是`window`调用的，所以打印出`window`。
- `person1.obj.foo1().call(person2)`是通过`.call(person2)`改变匿名函数内的`this`，所以绑定有效，因此打印出`person2`。
- `person1.obj.foo2()()`第一层为普通函数，第二层为匿名箭头函数。首先让我们明确匿名箭头函数内的`this`是由第一层普通函数决定的，所以我们只要知道第一层函数内的`this`是谁就可以了。而这里，第一层函数最后是由谁调用的呢 ？是由`obj`这个对象，所以打印出`obj`。
- `person1.obj.foo2.call(person2)()`中使用`.call(person2)`改变了第一层函数中的`this`指向，所以第二层的箭头函数会打印出`person2`。
- `person1.obj.foo2().call(person2)`中使用`.call(person2)`想要改变内层箭头函数的`this`指向，但是失败了，所以还是为外层作用域里的`this`，打印出`obj`。

答案

```
'window'
'window'
'person2'

'obj'
'person2'
'obj'
```

**9.4 题目四**

来看看这里会打印出什么呢？

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
(function () {
  'use strict';
  foo();
})();
```

答案并不是`undefined`，也不会报错，而是打印出了`2`。

哈哈 ，其实这里是有一个迷惑点的，那就是`"use strict"`。

我们知道，使用了`"use strict"`开启严格模式会使得`"use strict"`以下代码的`this`为`undefined`，也就是这里的立即执行函数中的`this`是`undefined`。

但是调用`foo()`函数的依然是`window`，所以`foo()`中的`this`依旧是`window`，所以会打印出`2`。

如果你是使用`this.foo()`调用的话，就会报错了，因为现在立即执行函数中的`this`是`undefined`。

或者将`"use strict"`放到`foo()`函数里面，也会报错。

# 对象 Promise

## 1. 基础题目

**1.1 题目一**

```javascript
const promise1 = new Promise((resolve, reject) => {
  console.log('promise1');
});
console.log('1', promise1);
```

过程分析：

- 从上至下，先遇到`new Promise`，执行该构造函数中的代码`promise1`
- 然后执行同步代码`1`，此时`promise1`没有被`resolve`或者`reject`，因此状态还是`pending`

结果：

```
'promise1'
'1' Promise{<pending>}
```

**1.2 题目二**

```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1);
  resolve('success');
  console.log(2);
});
promise.then(() => {
  console.log(3);
});
console.log(4);
```

过程分析：

- 从上至下，先遇到`new Promise`，执行其中的同步代码`1`
- 再遇到`resolve('success')`， 将`promise`的状态改为了`resolved`并且将值保存下来
- 继续执行同步代码`2`
- 跳出`promise`，往下执行，碰到`promise.then`这个微任务，将其加入微任务队列
- 执行同步代码`4`
- 本轮宏任务全部执行完毕，检查微任务队列，发现`promise.then`这个微任务且状态为`resolved`，执行它。

结果：

```
1 2 4 3
```

**1.3 题目三**

```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1);
  console.log(2);
});
promise.then(() => {
  console.log(3);
});
console.log(4);
```

过程分析

- 和题目二相似，只不过在`promise`中并没有`resolve`或者`reject`
- 因此`promise.then`并不会执行，它只有在被改变了状态之后才会执行。

结果：

```
1 2 4
```

**1.4 题目四**

```javascript
const promise1 = new Promise((resolve, reject) => {
  console.log('promise1');
  resolve('resolve1');
});
const promise2 = promise1.then((res) => {
  console.log(res);
});
console.log('1', promise1);
console.log('2', promise2);
```

过程分析：

- 从上至下，先遇到`new Promise`，执行该构造函数中的代码`promise1`
- 碰到`resolve`函数, 将`promise1`的状态改变为`resolved`, 并将结果保存下来
- 碰到`promise1.then`这个微任务，将它放入微任务队列
- `promise2`是一个新的状态为`pending`的`Promise`
- 执行同步代码`1`， 同时打印出`promise1`的状态是`resolved`
- 执行同步代码`2`，同时打印出`promise2`的状态是`pending`
- 宏任务执行完毕，查找微任务队列，发现`promise1.then`这个微任务且状态为`resolved`，执行它。

结果：

```
'promise1'
'1' Promise{<resolved>: 'resolve1'}
'2' Promise{<pending>}
'resolve1'
```

**1.5 题目五**

接下来看看这道题：

```javascript
const fn = () =>
  new Promise((resolve, reject) => {
    console.log(1);
    resolve('success');
  });
fn().then((res) => {
  console.log(res);
});
console.log('start');
```

这道题里最先执行的是`'start'`吗 ？

请仔细看看哦，`fn`函数它是直接返回了一个`new Promise`的，而且`fn`函数的调用是在`start`之前，所以它里面的内容应该会先执行。

结果：

```
1
'start'
'success'
```

**1.6 题目六**

如果把`fn`的调用放到`start`之后呢？

```javascript
const fn = () =>
  new Promise((resolve, reject) => {
    console.log(1);
    resolve('success');
  });
console.log('start');
fn().then((res) => {
  console.log(res);
});
```

是的，现在`start`就在`1`之前打印出来了，因为`fn`函数是之后执行的。

注意：之前我们很容易就以为看到 `new Promise()` 就执行它的第一个参数函数了，其实这是不对的，就像这两道题中，我们得注意它是不是被包裹在函数当中，如果是的话，只有在函数调用的时候才会执行。

答案：

```
"start"
1
"success"
```

## 2. 配合 setTimeout

**2.1 题目一**

```javascript
console.log('start');
setTimeout(() => {
  console.log('time');
});
Promise.resolve().then(() => {
  console.log('resolve');
});
console.log('end');
```

过程分析：

- 刚开始整个脚本作为一个宏任务来执行，对于同步代码直接压入执行栈进行执行，因此先打印出`start`和`end`。
- `setTimout`作为一个宏任务被放入宏任务队列(下一个)
- `Promise.then`作为一个微任务被放入微任务队列
- 本次宏任务执行完，检查微任务，发现`Promise.then`，执行它
- 接下来进入下一个宏任务，发现`setTimeout`，执行。

结果：

```
'start'
'end'
'resolve'
'time'
```

**2.2 题目二**

```javascript
const promise = new Promise((resolve, reject) => {
  console.log(1);
  setTimeout(() => {
    console.log('timerStart');
    resolve('success');
    console.log('timerEnd');
  }, 0);
  console.log(2);
});
promise.then((res) => {
  console.log(res);
});
console.log(4);
```

过程分析：

和题目`1.2`很像，不过在`resolve`的外层加了一层`setTimeout`定时器。

- 从上至下，先遇到`new Promise`，执行该构造函数中的代码`1`
- 然后碰到了定时器，将这个定时器中的函数放到下一个宏任务的延迟队列中等待执行
- 执行同步代码`2`
- 跳出`promise`函数，遇到`promise.then`，但其状态还是为`pending`，这里理解为先不执行
- 执行同步代码`4`
- 一轮循环过后，进入第二次宏任务，发现延迟队列中有`setTimeout`定时器，执行它
- 首先执行`timerStart`，然后遇到了`resolve`，将`promise`的状态改为`resolved`且保存结果并将之前的`promise.then`推入微任务队列
- 继续执行同步代码`timerEnd`
- 宏任务全部执行完毕，查找微任务队列，发现`promise.then`这个微任务，执行它。

因此执行结果为：

```
1
2
4
"timerStart"
"timerEnd"
"success"
```

**2.3 题目三**

题目三分了两个题目，因为看着都差不多，不过执行的结果却不一样，大家不妨先猜猜下面两个题目分别执行什么：

**(1)**:

```javascript
setTimeout(() => {
  console.log('timer1');
  setTimeout(() => {
    console.log('timer3');
  }, 0);
}, 0);
setTimeout(() => {
  console.log('timer2');
}, 0);
console.log('start');
```

**(2)**:

```javascript
setTimeout(() => {
  console.log('timer1');
  Promise.resolve().then(() => {
    console.log('promise');
  });
}, 0);
setTimeout(() => {
  console.log('timer2');
}, 0);
console.log('start');
```

**执行结果：**

```
'start'
'timer1'
'timer2'
'timer3'
```

```
'start'
'timer1'
'promise'
'timer2'
```

这两个例子，看着好像只是把第一个定时器中的内容换了一下而已。

一个是为定时器`timer3`，一个是为`Promise.then`

但是如果是定时器`timer3`的话，它会在`timer2`后执行，而`Promise.then`却是在`timer2`之前执行。

你可以这样理解，`Promise.then`是微任务，它会被加入到本轮中的微任务列表，而定时器`timer3`是宏任务，它会被加入到下一轮的宏任务中。

理解完这两个案例，可以来看看下面一道比较难的题目了。

**2.3 题目三**

```javascript
Promise.resolve().then(() => {
  console.log('promise1');
  const timer2 = setTimeout(() => {
    console.log('timer2');
  }, 0);
});
const timer1 = setTimeout(() => {
  console.log('timer1');
  Promise.resolve().then(() => {
    console.log('promise2');
  });
}, 0);
console.log('start');
```

这道题稍微的难一些，在`promise`中执行定时器，又在定时器中执行`promise`；

并且要注意的是，这里的`Promise`是直接`resolve`的，而之前的`new Promise`不一样。

因此过程分析为：

- 刚开始整个脚本作为第一次宏任务来执行，我们将它标记为**宏 1**，从上至下执行
- 遇到`Promise.resolve().then`这个微任务，将`then`中的内容加入第一次的微任务队列标记为**微 1**
- 遇到定时器`timer1`，将它加入下一次宏任务的延迟列表，标记为**宏 2**，等待执行(先不管里面是什么内容)
- 执行**宏 1**中的同步代码`start`
- 第一次宏任务(**宏 1**)执行完毕，检查第一次的微任务队列(**微 1**)，发现有一个`promise.then`这个微任务需要执行
- 执行打印出**微 1**中同步代码`promise1`，然后发现定时器`timer2`，将它加入**宏 2**的后面，标记为**宏 3**
- 第一次微任务队列(**微 1**)执行完毕，执行第二次宏任务(**宏 2**)，首先执行同步代码`timer1`
- 然后遇到了`promise2`这个微任务，将它加入此次循环的微任务队列，标记为**微 2**
- **宏 2**中没有同步代码可执行了，查找本次循环的微任务队列(**微 2**)，发现了`promise2`，执行它
- 第二轮执行完毕，执行**宏 3**，打印出`timer2`

所以结果为：

```
'start'
'promise1'
'timer1'
'promise2'
'timer2'
```

**2.4 题目四**

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success');
  }, 1000);
});
const promise2 = promise1.then(() => {
  throw new Error('error!!!');
});
console.log('promise1', promise1);
console.log('promise2', promise2);
setTimeout(() => {
  console.log('promise1', promise1);
  console.log('promise2', promise2);
}, 2000);
```

过程分析：

- 从上至下，先执行第一个`new Promise`中的函数，碰到`setTimeout`将它加入下一个宏任务列表
- 跳出`new Promise`，碰到`promise1.then`这个微任务，但其状态还是为`pending`，这里理解为先不执行
- `promise2`是一个新的状态为`pending`的`Promise`
- 执行同步代码`console.log('promise1')`，且打印出的`promise1`的状态为`pending`
- 执行同步代码`console.log('promise2')`，且打印出的`promise2`的状态为`pending`
- 碰到第二个定时器，将其放入下一个宏任务列表
- 第一轮宏任务执行结束，并且没有微任务需要执行，因此执行第二轮宏任务
- 先执行第一个定时器里的内容，将`promise1`的状态改为`resolved`且保存结果并将之前的`promise1.then`推入微任务队列
- 该定时器中没有其它的同步代码可执行，因此执行本轮的微任务队列，也就是`promise1.then`，它抛出了一个错误，且将`promise2`的状态设置为了`rejected`
- 第一个定时器执行完毕，开始执行第二个定时器中的内容
- 打印出`'promise1'`，且此时`promise1`的状态为`resolved`
- 打印出`'promise2'`，且此时`promise2`的状态为`rejected`

完整的结果为：

```
'promise1' Promise{<pending>}
'promise2' Promise{<pending>}
test5.html:102 Uncaught (in promise) Error: error!!! at test.html:102
'promise1' Promise{<resolved>: "success"}
'promise2' Promise{<rejected>: Error: error!!!}
```

**2.5 题目五**

如果你上面这道题搞懂了之后，我们就可以来做做这道了，你应该能很快就给出答案：

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('success');
    console.log('timer1');
  }, 1000);
  console.log('promise1里的内容');
});
const promise2 = promise1.then(() => {
  throw new Error('error!!!');
});
console.log('promise1', promise1);
console.log('promise2', promise2);
setTimeout(() => {
  console.log('timer2');
  console.log('promise1', promise1);
  console.log('promise2', promise2);
}, 2000);
```

结果：

```
'promise1里的内容'
'promise1' Promise{<pending>}
'promise2' Promise{<pending>}
'timer1'
test5.html:102 Uncaught (in promise) Error: error!!! at test.html:102
'timer2'
'promise1' Promise{<resolved>: "success"}
'promise2' Promise{<rejected>: Error: error!!!}
```

## 3. 原型方法 then、catch 和 finally

总结：

1. `Promise`的状态一经改变就不能再改变。(见 3.1)
2. `.then`和`.catch`都会返回一个新的`Promise`。(上面的1.4 证明了)
3. `catch`不管被连接到哪里，都能捕获上层的错误。(见 3.2)
4. 在`Promise`中，返回任意一个非 `promise` 的值都会被包裹成 `promise` 对象，例如`return 2`会被包装为`return Promise.resolve(2)`。
5. `Promise` 的 `.then` 或者 `.catch` 可以被调用多次, 当如果`Promise`内部的状态一经改变，并且有了一个值，那么后续每次调用`.then`或者`.catch`的时候都会直接拿到该值。(见 3.5)
6. `.then` 或者 `.catch` 中 `return` 一个 `error` 对象并不会抛出错误，所以不会被后续的 `.catch` 捕获。(见 3.6)
7. `.then` 或 `.catch` 返回的值不能是 promise 本身，否则会造成死循环。(见 3.7)
8. `.then` 或者 `.catch` 的参数期望是函数，传入非函数则会发生值透传。(见 3.8)
9. `.then`方法是能接收两个参数的，第一个是处理成功的函数，第二个是处理失败的函数，再某些时候你可以认为`catch`是`.then`第二个参数的简便写法。(见 3.9)
10. `.finally`方法也是返回一个`Promise`，他在`Promise`结束的时候，无论结果为`resolved`还是`rejected`，都会执行里面的回调函数。

**3.1 题目一**

```javascript
const promise = new Promise((resolve, reject) => {
  resolve('success1');
  reject('error');
  resolve('success2');
});
promise
  .then((res) => {
    console.log('then: ', res);
  })
  .catch((err) => {
    console.log('catch: ', err);
  });
```

结果：

```
"then: success1"
```

构造函数中的 `resolve` 或 `reject` 只有第一次执行有效，多次调用没有任何作用 。验证了第一个结论，`Promise`的状态一经改变就不能再改变。

**3.2 题目二**

```javascript
const promise = new Promise((resolve, reject) => {
  reject('error');
  resolve('success2');
});
promise
  .then((res) => {
    console.log('then1: ', res);
  })
  .then((res) => {
    console.log('then2: ', res);
  })
  .catch((err) => {
    console.log('catch: ', err);
  })
  .then((res) => {
    console.log('then3: ', res);
  });
```

结果：

```
"catch: " "error"
"then3: " undefined
```

验证了第三个结论，`catch`不管被连接到哪里，都能捕获上层的错误。

至于`then3`也会被执行，那是因为`catch()`也会返回一个`Promise`，且由于这个`Promise`没有返回值，所以打印出来的是`undefined`。

**3.3 题目三**

```javascript
Promise.resolve(1)
  .then((res) => {
    console.log(res);
    return 2;
  })
  .catch((err) => {
    return 3;
  })
  .then((res) => {
    console.log(res);
  });
```

结果：

```
1
2
```

`Promise`可以链式调用，不过`promise` 每次调用 `.then` 或者 `.catch` 都会返回一个新的 `promise`，从而实现了链式调用, 它并不像一般我们任务的链式调用一样`return this`。

上面的输出结果之所以依次打印出`1`和`2`，那是因为`resolve(1)`之后走的是第一个`then`方法，并没有走`catch`里，所以第二个`then`中的`res`得到的实际上是第一个`then`的返回值。

且`return 2`会被包装成`resolve(2)`。

**3.4 题目四**

如果把`3.3`中的`Promise.resolve(1)`改为`Promise.reject(1)`又会怎么样呢？

```javascript
Promise.reject(1)
  .then((res) => {
    console.log(res);
    return 2;
  })
  .catch((err) => {
    console.log(err);
    return 3;
  })
  .then((res) => {
    console.log(res);
  });
```

结果：

```
1
3
```

结果打印的当然是 `1` 和 `3` 啦，因为`reject(1)`此时走的就是`catch`，且第二个`then`中的`res`得到的就是`catch`中的返回值。

**3.5 题目五**

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log('timer');
    resolve('success');
  }, 1000);
});
const start = Date.now();
promise.then((res) => {
  console.log(res, Date.now() - start);
});
promise.then((res) => {
  console.log(res, Date.now() - start);
});
```

执行结果：

```
'timer'
success 1001
success 1002
```

当然，如果你足够快的话，也可能两个都是`1001`。

`Promise` 的 `.then` 或者 `.catch` 可以被调用多次，但这里 `Promise` 构造函数只执行一次。或者说 `promise` 内部状态一经改变，并且有了一个值，那么后续每次调用 `.then` 或者 `.catch` 都会直接拿到该值。

**3.6 题目六**

```javascript
Promise.resolve()
  .then(() => {
    return new Error('error!!!');
  })
  .then((res) => {
    console.log('then: ', res);
  })
  .catch((err) => {
    console.log('catch: ', err);
  });
```

猜猜这里的结果输出的是什么 ？

你可能想到的是进入`.catch`然后被捕获了错误。

结果并不是这样的，它走的是`.then`里面：

```
"then: " "Error: error!!!"
```

这也验证了第 4 点和第 6 点，返回任意一个非 `promise` 的值都会被包裹成 `promise` 对象，因此这里的`return new Error('error!!!')`也被包裹成了`return Promise.resolve(new Error('error!!!'))`。

当然如果你抛出一个错误的话，可以用下面两的任意一种：

```javascript
return Promise.reject(new Error('error!!!'));
// or
throw new Error('error!!!');
```

**3.7 题目七**

```javascript
const promise = Promise.resolve().then(() => {
  return promise;
});
promise.catch(console.err);
```

`.then` 或 `.catch` 返回的值不能是 promise 本身，否则会造成死循环。

因此结果会报错：

```
Uncaught (in promise) TypeError: Chaining cycle detected for promise #<Promise>
```

**3.8 题目八**

```javascript
Promise.resolve(1).then(2).then(Promise.resolve(3)).then(console.log);
```

这道题看着好像很简单，又感觉很复杂的样子，怎么这么多个`.then`啊...

其实你只要记住**原则 8**：`.then` 或者 `.catch` 的参数期望是函数，传入非函数则会发生值透传。

第一个`then`和第二个`then`中传入的都不是函数，一个是数字类型，一个是对象类型，因此发生了透传，将`resolve(1)` 的值直接传到最后一个`then`里。

所以输出结果为：

```
1
```

**3.9 题目九**

下面来介绍一下`.then`函数中的两个参数。

第一个参数是用来处理`Promise`成功的函数，第二个则是处理失败的函数。

也就是说`Promise.resolve('1')`的值会进入成功的函数，`Promise.reject('2')`的值会进入失败的函数。

让我们来看看这个例子：

```javascript
Promise.reject('err!!!')
  .then(
    (res) => {
      console.log('success', res);
    },
    (err) => {
      console.log('error', err);
    }
  )
  .catch((err) => {
    console.log('catch', err);
  });
```

这里的执行结果是：

```
'error' 'error!!!'
```

它进入的是`then()`中的第二个参数里面，而如果把第二个参数去掉，就进入了`catch()`中：

```javascript
Promise.reject('err!!!')
  .then((res) => {
    console.log('success', res);
  })
  .catch((err) => {
    console.log('catch', err);
  });
```

执行结果：

```
'catch' 'error!!!'
```

但是有一个问题，如果是这个案例呢？

```javascript
Promise.resolve()
  .then(
    function success(res) {
      throw new Error('error!!!');
    },
    function fail1(err) {
      console.log('fail1', err);
    }
  )
  .catch(function fail2(err) {
    console.log('fail2', err);
  });
```

由于`Promise`调用的是`resolve()`，因此`.then()`执行的应该是`success()`函数，可是`success()`函数抛出的是一个错误，它会被后面的`catch()`给捕获到，而不是被`fail1`函数捕获。

因此执行结果为：

```
fail2 Error: error!!!
			at success
```

**3.10 题目十**

接着来看看`.finally()`，这个功能一般不太用在面试中，不过如果碰到了你也应该知道该如何处理。

其实你只要记住它三个很重要的知识点就可以了：

1. `.finally()`方法不管`Promise`对象最后的状态如何都会执行
2. `.finally()`方法的回调函数不接受任何的参数，也就是说你在`.finally()`函数中是没法知道`Promise`最终的状态是`resolved`还是`rejected`的
3. 它最终返回的默认会是一个**上一次的 Promise 对象值**，不过如果抛出的是一个异常则返回异常的`Promise`对象。

来看看这个简单的例子：

```javascript
Promise.resolve('1')
  .then((res) => {
    console.log(res);
  })
  .finally(() => {
    console.log('finally');
  });
Promise.resolve('2')
  .finally(() => {
    console.log('finally2');
    return '我是finally2返回的值';
  })
  .then((res) => {
    console.log('finally2后面的then函数', res);
  });
```

这两个`Promise`的`.finally`都会执行，且就算`finally2`返回了新的值，它后面的`then()`函数接收到的结果却还是`'2'`，因此打印结果为：

```
'1'
'finally2'
'finally'
'finally2后面的then函数' '2'
```

至于为什么`finally2`的打印要在`finally`前面，请看下一个例子中的解析。

不过在此之前让我们再来确认一下，`finally`中要是抛出的是一个异常是怎样的：

```javascript
Promise.resolve('1')
  .finally(() => {
    console.log('finally1');
    throw new Error('我是finally中抛出的异常');
  })
  .then((res) => {
    console.log('finally后面的then函数', res);
  })
  .catch((err) => {
    console.log('捕获错误', err);
  });
```

执行结果为：

```
'finally1'
'捕获错误' Error: 我是finally中抛出的异常
```

但是如果改为`return new Error('我是finally中抛出的异常')`，打印出来的就是`'finally后面的then函数 1'`

OK，，让我们来看一个比较难的例子：

```javascript
function promise1() {
  let p = new Promise((resolve) => {
    console.log('promise1');
    resolve('1');
  });
  return p;
}
function promise2() {
  return new Promise((resolve, reject) => {
    reject('error');
  });
}
promise1()
  .then((res) => console.log(res))
  .catch((err) => console.log(err))
  .finally(() => console.log('finally1'));

promise2()
  .then((res) => console.log(res))
  .catch((err) => console.log(err))
  .finally(() => console.log('finally2'));
```

执行过程：

- 首先定义了两个函数`promise1`和`promise2`，先不管接着往下看。
- `promise1`函数先被调用了，然后执行里面`new Promise`的同步代码打印出`promise1`
- 之后遇到了`resolve(1)`，将`p`的状态改为了`resolved`并将结果保存下来。
- 此时`promise1`内的函数内容已经执行完了，跳出该函数
- 碰到了`promise1().then()`，由于`promise1`的状态已经发生了改变且为`resolved`因此将`promise1().then()`这条微任务加入本轮的微任务列表(**这是第一个微任务**)
- 这时候要注意了，代码并不会接着往链式调用的下面走，也就是不会先将`.finally`加入微任务列表，那是因为`.then`本身就是一个微任务，它链式后面的内容必须得等当前这个微任务执行完才会执行，因此这里我们先不管`.finally()`
- 再往下走碰到了`promise2()`函数，其中返回的`new Promise`中并没有同步代码需要执行，所以执行`reject('error')`的时候将`promise2`函数中的`Promise`的状态变为了`rejected`
- 跳出`promise2`函数，遇到了`promise2().then()`，将其加入当前的微任务队列(**这是第二个微任务**)，且链式调用后面的内容得等该任务执行完后才执行，和`.then()`一样。
- OK， 本轮的宏任务全部执行完了，来看看微任务列表，存在`promise1().then()`，执行它，打印出`1`，然后遇到了`.finally()`这个微任务将它加入微任务列表(**这是第三个微任务**)等待执行
- 再执行`promise2().catch()`打印出`error`，执行完后将`finally2`加入微任务加入微任务列表(**这是第四个微任务**)
- OK， 本轮又全部执行完了，但是微任务列表还有两个新的微任务没有执行完，因此依次执行`finally1`和`finally2`。

结果：

```
'promise1'
'1'
'error'
'finally1'
'finally2'
```

在这道题中其实能拓展的东西挺多的，之前没有提到，那就是你可以理解为**链式调用**后面的内容需要等前一个调用执行完才会执行。

就像是这里的`finally()`会等`promise1().then()`执行完才会将`finally()`加入微任务队列，其实如果这道题中你把`finally()`换成是`then()`也是这样的:

```javascript
function promise1() {
  let p = new Promise((resolve) => {
    console.log('promise1');
    resolve('1');
  });
  return p;
}
function promise2() {
  return new Promise((resolve, reject) => {
    reject('error');
  });
}
promise1()
  .then((res) => console.log(res))
  .catch((err) => console.log(err))
  .then(() => console.log('finally1'));

promise2()
  .then((res) => console.log(res))
  .catch((err) => console.log(err))
  .then(() => console.log('finally2'));
```

## 4. 静态方法 all 和 race

在做下面的题目之前，让我们先来了解一下`Promise.all()`和`Promise.race()`的用法。

通俗来说，`.all()`的作用是接收一组异步任务，然后并行执行异步任务，并且在所有异步操作执行完后才执行回调。

`.race()`的作用也是接收一组异步任务，然后并行执行异步任务，只保留取第一个执行完成的异步操作的结果，其他的方法仍在执行，不过执行结果会被抛弃。

来看看题目一。

**4.1 题目一**

我们知道如果直接在脚本文件中定义一个`Promise`，它构造函数的第一个参数是会立即执行的，就像这样：

```javascript
const p1 = new Promise((r) => console.log('立即打印'));
```

控制台中会立即打印出 “立即打印”。

因此为了控制它什么时候执行，我们可以用一个函数包裹着它，在需要它执行的时候，调用这个函数就可以了：

```javascript
function runP1() {
  const p1 = new Promise((r) => console.log('立即打印'));
  return p1;
}

runP1(); // 调用此函数时才执行
```

OK ， 让我们回归正题。

现在来构建这么一个函数：

```javascript
function runAsync(x) {
  const p = new Promise((r) => setTimeout(() => r(x, console.log(x)), 1000));
  return p;
}
```

该函数传入一个值`x`，然后间隔一秒后打印出这个`x`。

如果我用`.all()`来执行它会怎样呢？

```javascript
function runAsync(x) {
  const p = new Promise((r) => setTimeout(() => r(x, console.log(x)), 1000));
  return p;
}
Promise.all([runAsync(1), runAsync(2), runAsync(3)]).then((res) =>
  console.log(res)
);
```

先来想想此段代码在浏览器中会如何执行？

没错，当你打开页面的时候，在间隔一秒后，控制台会同时打印出`1, 2, 3`，还有一个数组`[1, 2, 3]`。

```
1
2
3
[1, 2, 3]
```

所以你现在能理解这句话的意思了吗：**有了 all，你就可以并行执行多个异步操作，并且在一个回调中处理所有的返回数据。**

`.all()`后面的`.then()`里的回调函数接收的就是所有异步操作的结果。

而且这个结果中数组的顺序和`Promise.all()`接收到的数组顺序一致！！！

> 有一个场景是很适合用这个的，一些游戏类的素材比较多的应用，打开网页时，预先加载需要用到的各种资源如图片、flash 以及各种静态文件。所有的都加载完后，我们再进行页面的初始化。

**4.2 题目二**

我新增了一个`runReject`函数，它用来在`1000 * x`秒后`reject`一个错误。

同时`.catch()`函数能够捕获到`.all()`里最先的那个异常，并且只执行一次。

想想这道题会怎样执行呢 ？

```javascript
function runAsync(x) {
  const p = new Promise((r) => setTimeout(() => r(x, console.log(x)), 1000));
  return p;
}
function runReject(x) {
  const p = new Promise((res, rej) =>
    setTimeout(() => rej(`Error: ${x}`, console.log(x)), 1000 * x)
  );
  return p;
}
Promise.all([runAsync(1), runReject(4), runAsync(3), runReject(2)])
  .then((res) => console.log(res))
  .catch((err) => console.log(err));
```

不卖关子了，让我来公布答案：

```
1
3
// 2s后输出
2
Error: 2
// 4s后输出
4
```

没错，就像我之前说的，`.catch`是会捕获最先的那个异常，在这道题目中最先的异常就是`runReject(2)`的结果。

另外，如果一组异步操作中有一个异常都不会进入`.then()`的第一个回调函数参数中。

注意，为什么不说是不进入`.then()`中呢 ？

哈哈，大家别忘了`.then()`方法的第二个参数也是可以捕获错误的：

```javascript
Promise.all([runAsync(1), runReject(4), runAsync(3), runReject(2)]).then(
  (res) => console.log(res),
  (err) => console.log(err)
);
```

**4.3 题目三**

接下来让我们看看另一个有趣的方法`.race`。

让我看看你们的英语水平如何？

快！一秒钟告诉我`race`是什么意思？

好吧...你们果然很强...

`race`，比赛，赛跑的意思。

所以使用`.race()`方法，它只会获取最先执行完成的那个结果，其它的异步任务虽然也会继续进行下去，不过`race`已经不管那些任务的结果了。

来，改造一下`4.1`这道题：

```javascript
function runAsync(x) {
  const p = new Promise((r) => setTimeout(() => r(x, console.log(x)), 1000));
  return p;
}
Promise.race([runAsync(1), runAsync(2), runAsync(3)])
  .then((res) => console.log('result: ', res))
  .catch((err) => console.log(err));
```

执行结果为：

```
1
'result: ' 1
2
3
```

> 这个 race 有什么用呢？使用场景还是很多的，比如我们可以用 race 给某个异步请求设置超时时间，并且在超时后执行相应的操作

**4.4 题目四**

改造一下题目`4.2`：

```javascript
function runAsync(x) {
  const p = new Promise((r) => setTimeout(() => r(x, console.log(x)), 1000));
  return p;
}
function runReject(x) {
  const p = new Promise((res, rej) =>
    setTimeout(() => rej(`Error: ${x}`, console.log(x)), 1000 * x)
  );
  return p;
}
Promise.race([runReject(0), runAsync(1), runAsync(2), runAsync(3)])
  .then((res) => console.log('result: ', res))
  .catch((err) => console.log(err));
```

遇到错误的话，也是一样的，在这道题中，`runReject(0)`最先执行完，所以进入了`catch()`中：

```
0
'Error: 0'
1
2
3
```

**总结**

好的，让我们来总结一下`.then()`和`.race()`吧，

- `Promise.all()`的作用是接收一组异步任务，然后并行执行异步任务，并且在所有异步操作执行完后才执行回调。
- `.race()`的作用也是接收一组异步任务，然后并行执行异步任务，只保留取第一个执行完成的异步操作的结果，其他的方法仍在执行，不过执行结果会被抛弃。
- `Promise.all().then()`结果中数组的顺序和`Promise.all()`接收到的数组顺序一致。

## 5. 配合 async/await

既然谈到了`Promise`，那就肯定得再说说`async/await`，在很多时候`async`和`Promise`的解法差不多，又有些不一样。不信你来看看题目一。

**5.1 题目一**

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  console.log('async2');
}
async1();
console.log('start');
```

这道基础题输出的是啥？

答案：

```
'async1 start'
'async2'
'start'
'async1 end'
```

过程分析：

- 首先一进来是创建了两个函数的，我们先不看函数的创建位置，而是看它的调用位置
- 发现`async1`函数被调用了，然后去看看调用的内容
- 执行函数中的同步代码`async1 start`，之后碰到了`await`，它会阻塞`async1`后面代码的执行，因此会先去执行`async2`中的同步代码`async2`，然后跳出`async1`
- 跳出`async1`函数后，执行同步代码`start`
- 在一轮宏任务全部执行完之后，再来执行刚刚`await`后面的内容`async1 end`。

在这里，你可以理解为`await`后面的内容就相当于放到了`Promise.then`的里面。

让我们来看看将`await`转换为`Promise.then`的伪代码：

```javascript
async function async1() {
  console.log('async1 start');
  // 原来代码
  // await async2();
  // console.log("async1 end");

  // 转换后代码
  new Promise((resolve) => {
    console.log('async2');
    resolve();
  }).then((res) => console.log('async1 end'));
}
async function async2() {
  console.log('async2');
}
async1();
console.log('start');
```

转换后的伪代码和前面的执行结果是一样的。(感谢评论区[Wing93](https://juejin.im/user/57e0f2738ac2470061745306)小伙伴的指出)

另外关于`await`和`Promise`的区别，如果我们把`await async2()`换成一个`new Promise`呢？

```javascript
async function async1() {
  console.log('async1 start');
  new Promise((resolve) => {
    console.log('promise');
  });
  console.log('async1 end');
}
async1();
console.log('start');
```

此时的执行结果为：

```
'async start'
'promise'
'async1 end'
'start'
```

可以看到`new Promise()`并不会阻塞后面的同步代码`async1 end`的执行。

**5.2 题目二**

现在将`async`结合定时器看看。

给题目一中的 `async2`函数中加上一个定时器：

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}
async function async2() {
  setTimeout(() => {
    console.log('timer');
  }, 0);
  console.log('async2');
}
async1();
console.log('start');
```

没错，定时器始终还是最后执行的，它被放到下一条宏任务的延迟队列中。

答案：

```
'async1 start'
'async2'
'start'
'async1 end'
'timer'
```

**5.3 题目三**

来吧，小伙伴们，让我们多加几个定时器看看。

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
  setTimeout(() => {
    console.log('timer1');
  }, 0);
}
async function async2() {
  setTimeout(() => {
    console.log('timer2');
  }, 0);
  console.log('async2');
}
async1();
setTimeout(() => {
  console.log('timer3');
}, 0);
console.log('start');
```

思考一下 🤔，执行结果会是什么？

其实如果你能做到这里了，说明你前面的那些知识点也都掌握了，我就不需要太过详细的步骤分析了。

直接公布答案吧：

```
'async1 start'
'async2'
'start'
'async1 end'
'timer2'
'timer3'
'timer1'
```

定时器谁先执行，你只需要关注谁先被调用的以及延迟时间是多少，这道题中延迟时间都是`0`，所以只要关注谁先被调用的。。

**5.4 题目四**

正常情况下，`async`中的`await`命令是一个`Promise`对象，返回该对象的结果。

但如果不是`Promise`对象的话，就会直接返回对应的值，相当于`Promise.resolve()`

```javascript
async function fn() {
  // return await 1234
  // 等同于
  return 123;
}
fn().then((res) => console.log(res));
```

结果：

```
123
```

**5.5 题目五**

```javascript
async function async1() {
  console.log('async1 start');
  await new Promise((resolve) => {
    console.log('promise1');
  });
  console.log('async1 success');
  return 'async1 end';
}
console.log('srcipt start');
async1().then((res) => console.log(res));
console.log('srcipt end');
```

这道题目比较有意思，大家要注意了。

在`async1`中`await`后面的`Promise`是没有返回值的，也就是它的状态始终是`pending`状态，因此相当于一直在`await`，`await`，`await`却始终没有响应...

所以在`await`之后的内容是不会执行的，也包括`async1`后面的 `.then`。

答案为：

```
'script start'
'async1 start'
'promise1'
'script end'
```

**5.6 题目六**

让我们给`5.5`中的`Promise`加上`resolve`：

```javascript
async function async1() {
  console.log('async1 start');
  await new Promise((resolve) => {
    console.log('promise1');
    resolve('promise1 resolve');
  }).then((res) => console.log(res));
  console.log('async1 success');
  return 'async1 end';
}
console.log('srcipt start');
async1().then((res) => console.log(res));
console.log('srcipt end');
```

现在`Promise`有了返回值了，因此`await`后面的内容将会被执行：

```
'script start'
'async1 start'
'promise1'
'script end'
'promise1 resolve'
'async1 success'
'async1 end'
```

**5.7 题目七**

```javascript
async function async1() {
  console.log('async1 start');
  await new Promise((resolve) => {
    console.log('promise1');
    resolve('promise resolve');
  });
  console.log('async1 success');
  return 'async1 end';
}
console.log('srcipt start');
async1().then((res) => {
  console.log(res);
});
new Promise((resolve) => {
  console.log('promise2');
  setTimeout(() => {
    console.log('timer');
  });
});
```

这道题应该也不难，不过有一点需要注意的，在`async1`中的`new Promise`它的`resovle`的值和`async1().then()`里的值是没有关系的，很多小伙伴可能看到`resovle('promise resolve')`就会误以为是`async1().then()`中的返回值。

因此这里的执行结果为：

```
'script start'
'async1 start'
'promise1'
'promise2'
'async1 success'
'sync1 end'
'timer'
```

**5.8 题目八**

我们再来看一道头条曾经的面试题：

```javascript
async function async1() {
  console.log('async1 start');
  await async2();
  console.log('async1 end');
}

async function async2() {
  console.log('async2');
}

console.log('script start');

setTimeout(function () {
  console.log('setTimeout');
}, 0);

async1();

new Promise(function (resolve) {
  console.log('promise1');
  resolve();
}).then(function () {
  console.log('promise2');
});
console.log('script end');
```

有了上面几题做基础，相信你很快也能答上来了。

自信的写下你们的答案吧。

```
'script start'
'async1 start'
'async2'
'promise1'
'script end'
'async1 end'
'promise2'
'setTimeout'
```

(这道题最后`async1 end`和`promise2`的顺序其实在网上饱受争议，我这里使用浏览器`Chrome V80`，`Node v12.16.1`的执行结果都是上面这个答案)

**5.9 题目九**

好的 ，`async/await`大法已练成，咱们继续：

```javascript
async function testSometing() {
  console.log('执行testSometing');
  return 'testSometing';
}

async function testAsync() {
  console.log('执行testAsync');
  return Promise.resolve('hello async');
}

async function test() {
  console.log('test start...');
  const v1 = await testSometing();
  console.log(v1);
  const v2 = await testAsync();
  console.log(v2);
  console.log(v1, v2);
}

test();

var promise = new Promise((resolve) => {
  console.log('promise start...');
  resolve('promise');
});
promise.then((val) => console.log(val));

console.log('test end...');
```

答案：

```
'test start...'
'执行testSometing'
'promise start...'
'test end...'
'testSometing'
'执行testAsync'
'promise'
'hello async'
'testSometing' 'hello async'
```

## 6. async 处理错误

**6.1 题目一**

在`async`中，如果 `await`后面的内容是一个异常或者错误的话，会怎样呢？

```javascript
async function async1() {
  await async2();
  console.log('async1');
  return 'async1 success';
}
async function async2() {
  return new Promise((resolve, reject) => {
    console.log('async2');
    reject('error');
  });
}
async1().then((res) => console.log(res));
```

例如这道题中，`await`后面跟着的是一个状态为`rejected`的`promise`。

**如果在 async 函数中抛出了错误，则终止错误结果，不会继续向下执行。**

所以答案为：

```
'async2'
Uncaught (in promise) error
```

如果改为`throw new Error`也是一样的：

```javascript
async function async1() {
  console.log('async1');
  throw new Error('error!!!');
  return 'async1 success';
}
async1().then((res) => console.log(res));
```

结果为：

```
'async1'
Uncaught (in promise) Error: error!!!
```

**6.2 题目二**

如果想要使得错误的地方不影响`async`函数后续的执行的话，可以使用`try catch`

```javascript
async function async1() {
  try {
    await Promise.reject('error!!!');
  } catch (e) {
    console.log(e);
  }
  console.log('async1');
  return Promise.resolve('async1 success');
}
async1().then((res) => console.log(res));
console.log('script start');
```

这里的结果为：

```
'script start'
'error!!!'
'async1'
'async1 success'
```

或者你可以直接在`Promise.reject`后面跟着一个`catch()`方法：

```javascript
async function async1() {
  // try {
  //   await Promise.reject('error!!!')
  // } catch(e) {
  //   console.log(e)
  // }
  await Promise.reject('error!!!').catch((e) => console.log(e));
  console.log('async1');
  return Promise.resolve('async1 success');
}
async1().then((res) => console.log(res));
console.log('script start');
```

运行结果是一样的。

## 7. 综合题

上面的题目都是被我拆分着说一些功能点，现在让我们来做一些比较难的综合题吧。

**7.1 题目一**

```javascript
const first = () =>
  new Promise((resolve, reject) => {
    console.log(3);
    let p = new Promise((resolve, reject) => {
      console.log(7);
      setTimeout(() => {
        console.log(5);
        resolve(6);
        console.log(p);
      }, 0);
      resolve(1);
    });
    resolve(2);
    p.then((arg) => {
      console.log(arg);
    });
  });
first().then((arg) => {
  console.log(arg);
});
console.log(4);
```

过程分析：

- 第一段代码定义的是一个函数，所以我们得看看它是在哪执行的，发现它在`4`之前，所以可以来看看`first`函数里面的内容了。(这一步有点类似于题目`1.5`)
- 函数`first`返回的是一个`new Promise()`，因此先执行里面的同步代码`3`
- 接着又遇到了一个`new Promise()`，直接执行里面的同步代码`7`
- 执行完`7`之后，在`p`中，遇到了一个定时器，先将它放到下一个宏任务队列里不管它，接着向下走
- 碰到了`resolve(1)`，这里就把`p`的状态改为了`resolved`，且返回值为`1`，不过这里也先不执行
- 跳出`p`，碰到了`resolve(2)`，这里的`resolve(2)`，表示的是把`first`函数返回的那个`Promise`的状态改了，也先不管它。
- 然后碰到了`p.then`，将它加入本次循环的微任务列表，等待执行
- 跳出`first`函数，遇到了`first().then()`，将它加入本次循环的微任务列表(`p.then`的后面执行)
- 然后执行同步代码`4`
- 本轮的同步代码全部执行完毕，查找微任务列表，发现`p.then`和`first().then()`，依次执行，打印出`1和2`
- 本轮任务执行完毕了，发现还有一个定时器没有跑完，接着执行这个定时器里的内容，执行同步代码`5`
- 然后又遇到了一个`resolve(6)`，它是放在`p`里的，但是`p`的状态在之前已经发生过改变了，因此这里就不会再改变，也就是说`resolve(6)`相当于没任何用处，因此打印出来的`p`为`Promise{<resolved>: 1}`。(这一步类似于题目`3.1`)

结果：

```
3
7
4
1
2
5
Promise{<resolved>: 1}
```

做对了的小伙伴奖励自己一朵小`(大)`红`(嘴)`花`(巴)`吧，

**7.2 题目二**

```javascript
const async1 = async () => {
  console.log('async1');
  setTimeout(() => {
    console.log('timer1');
  }, 2000);
  await new Promise((resolve) => {
    console.log('promise1');
  });
  console.log('async1 end');
  return 'async1 success';
};
console.log('script start');
async1().then((res) => console.log(res));
console.log('script end');
Promise.resolve(1)
  .then(2)
  .then(Promise.resolve(3))
  .catch(4)
  .then((res) => console.log(res));
setTimeout(() => {
  console.log('timer2');
}, 1000);
```

注意的知识点：

- `async`函数中`await`的`new Promise`要是没有返回值的话则不执行后面的内容(类似题`5.5`)
- `.then`函数中的参数期待的是函数，如果不是函数的话会发生透传(类似题`3.8` )
- 注意定时器的延迟时间

因此本题答案为：

```
'script start'
'async1'
'promise1'
'script end'
1
'timer2'
'timer1'
```

**7.3 题目三**

```javascript
const p1 = new Promise((resolve) => {
  setTimeout(() => {
    resolve('resolve3');
    console.log('timer1');
  }, 0);
  resolve('resovle1');
  resolve('resolve2');
})
  .then((res) => {
    console.log(res);
    setTimeout(() => {
      console.log(p1);
    }, 1000);
  })
  .finally((res) => {
    console.log('finally', res);
  });
```

注意的知识点：

- `Promise`的状态一旦改变就无法改变(类似题目`3.5`)
- `finally`不管`Promise`的状态是`resolved`还是`rejected`都会执行，且它的回调函数是接收不到`Promise`的结果的，所以`finally()`中的`res`是一个迷惑项(类似`3.10`)。
- 最后一个定时器打印出的`p1`其实是`.finally`的返回值，我们知道`.finally`的返回值如果在没有抛出错误的情况下默认会是上一个`Promise`的返回值(`3.10`中也有提到), 而这道题中`.finally`上一个`Promise`是`.then()`，但是这个`.then()`并没有返回值，所以`p1`打印出来的`Promise`的值会是`undefined`，如果你在定时器的**下面**加上一个`return 1`，则值就会变成`1`(感谢掘友[JS 丛中过](https://juejin.im/user/5b1487eee51d4506e1748613)的指出)。

答案：

```
'resolve1'
'finally' undefined
'timer1'
Promise{<resolved>: undefined}
```

## 8. 几道大厂的面试题

**8.1 使用 Promise 实现每隔 1 秒输出 1,2,3**

这道题比较简单的一种做法是可以用`Promise`配合着`reduce`不停的在`promise`后面叠加`.then`，请看下面的代码：

```javascript
const arr = [1, 2, 3];
arr.reduce((p, x) => {
  return p.then(() => {
    return new Promise((r) => {
      setTimeout(() => r(console.log(x)), 1000);
    });
  });
}, Promise.resolve());
```

或者你可以更简单一点写：

```javascript
const arr = [1, 2, 3];
arr.reduce(
  (p, x) =>
    p.then(() => new Promise((r) => setTimeout(() => r(console.log(x)), 1000))),
  Promise.resolve()
);
```

参考链接：[如何让异步操作顺序执行](https://segmentfault.com/q/1010000010748967)

**拓展题**

这道拓展题来自于“万物皆可爱的[LINGLONG](https://juejin.im/user/5cd2341ce51d456e5c5baba3) ”小姐姐，炒鸡棒 👍。

题目是这样的，她把我上面写的箭头函数版本改造了一下：

```javascript
const arr = [1, 2, 3];
const result = arr.reduce(
  (p, x) =>
    p.then(new Promise((r) => setTimeout(() => r(console.log(x)), 1000))),
  Promise.resolve()
);
```

眼尖的小伙伴看出区别了吗？

`p.then`里的代码由`() => new Promise(...)`变成了`new Promise(...)`。

现在执行结果就大不相同了。

**在一秒后按顺序同时打印出`1、2、3`:**

```
1
2
3
```

咦 ？为什么会这样呢 ？

只是一个小小的改变却有大大的区别。

其实刚开始看到的时候霖呆呆我也愣了那么几秒。不过等我们一步一步拆分并对想不通的地方写了几个案例来看就理解了。

评论区和小姐姐扯了一大堆，结果把她越弄越糊。后来我改变了一种思路来描述，觉得应该直接上伪代码：

```javascript
const arr = [1, 2, 3];
arr.reduce(
  (p, x) =>
    p.then(() => new Promise((r) => setTimeout(() => r(console.log(x)), 1000))),
  Promise.resolve()
);
```

转换为伪代码就是这样：

(相当于是用`reduce`不停的往后面叠加`.then`)

```javascript
Promise.resolve()
  .then(() => {
    return new Promise((r) => {
      setTimeout(() => {
        r(console.log(1));
      }, 1000);
    });
  })
  .then((r) => {
    return new Promise((r) => {
      setTimeout(() => {
        r(console.log(2));
      }, 1000);
    });
  })
  .then((r) => {
    return new Promise((r) => {
      setTimeout(() => {
        r(console.log(3));
      }, 1000);
    });
  });
```

可以看到，每一个`.then`都是依赖于上一个`new Promise`何时被`resolve`了才会执行的，例如第二个`.then()`，它要等`r(console.log(1)`这段代码执行了，才会执行。

那么`r(console.log(1))`什么时候执行呢？就是在第一个定时器(也就是一秒后)触发的时候才执行。这样就保证了后面接着的`.then()`要等前一个定时器执行完才能执行，也就是隔一秒输出。

而如果是这样写的话：

```javascript
const arr = [1, 2, 3];
const result = arr.reduce(
  (p, x) =>
    p.then(new Promise((r) => setTimeout(() => r(console.log(x)), 1000))),
  Promise.resolve()
);
```

它的伪代码就是这样：

(每个`then`里面的第一个参数不是一个函数)

```javascript
Promise.resolve()
  .then(
    new Promise((r) => {
      setTimeout(() => {
        r(console.log(1));
      }, 1000);
    })
  )
  .then(
    new Promise((r) => {
      setTimeout(() => {
        r(console.log(2));
      }, 1000);
    })
  )
  .then(
    new Promise((r) => {
      setTimeout(() => {
        r(console.log(3));
      }, 1000);
    })
  );
```

`p.then()`里面的参数如果不是函数的话，会发生透传，这个在`3.8`中已经提过了。但是发生透传，`.then()`里的代码就不执行了吗？

并不是的，我们来看这个例子：

```javascript
const p = Promise.resolve(1).then(console.log('我不关心结果'));
console.log(p);
p.then((res) => console.log(res));
```

很明显这里也发生了透传，但是`'我不关心结果'`也还是被打印出来了，并且由于透传，`p.then()`里获取到的`res`就是`1`，因此会打印出：

```
'我不关心结果'
Promise{
[[PromiseStatus]]: "resolved"
[[PromiseValue]]: 1
}
1
```

(第二行打印出`Promise{<pending>}`的小伙伴请把这个对象展开来看)

这个例子表明，就算发生了透传，`p.then()`中的代码依据也是会执行的。

所以回到

```javascript
.then(new Promise(r => {
    setTimeout(() => {
      r(console.log(1))
    }, 1000)
  }))
```

中，现在`.then()`中就相当于是执行一段同步代码：

```javascript
new Promise((r) => {
  setTimeout(() => {
    r(console.log(1));
  }, 1000);
});
```

而这段代码的作用是向延迟队列中`push`一个一秒后执行的定时器任务。

并且在`push`完定时器之后，代码就马上进入了下一个`.then`(因为既然第一个`.then`已经是透传的了就没有必要等它的执行结果了)

下一个`.then`竟然也是一个透传，OK，那我继续`push`这个定时器，然后再执行第三个`.then`。

三个`.then`已经执行完成了，现在我们的延迟队列中已经有了三个定时器等待执行，**并且三个定时器的延迟时间都是 1000ms!!!**。

所以等到了时间之后，就会同时打印出来了`1、2、3`。（其实准确来说，不是同时打印的，不过中间相差的时间非常非常短，大可忽略它）

现在你是否理解了其中的区别呢 😝。

**8.2 使用 Promise 实现红绿灯交替重复亮**

红灯 3 秒亮一次，黄灯 2 秒亮一次，绿灯 1 秒亮一次；如何让三个灯不断交替重复亮灯？（用 Promise 实现）三个亮灯函数已经存在：

```javascript
function red() {
  console.log('red');
}
function green() {
  console.log('green');
}
function yellow() {
  console.log('yellow');
}
```

答案：

```javascript
function red() {
  console.log('red');
}
function green() {
  console.log('green');
}
function yellow() {
  console.log('yellow');
}
const light = function (timer, cb) {
  return new Promise((resolve) => {
    setTimeout(() => {
      cb();
      resolve();
    }, timer);
  });
};
const step = function () {
  Promise.resolve()
    .then(() => {
      return light(3000, red);
    })
    .then(() => {
      return light(2000, green);
    })
    .then(() => {
      return light(1000, yellow);
    })
    .then(() => {
      return step();
    });
};

step();
```

**8.3 实现 mergePromise 函数**

实现 mergePromise 函数，把传进去的数组按顺序先后执行，并且把返回的数据先后放到数组 data 中。

```javascript
const time = (timer) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve();
    }, timer);
  });
};
const ajax1 = () =>
  time(2000).then(() => {
    console.log(1);
    return 1;
  });
const ajax2 = () =>
  time(1000).then(() => {
    console.log(2);
    return 2;
  });
const ajax3 = () =>
  time(1000).then(() => {
    console.log(3);
    return 3;
  });

function mergePromise() {
  // 在这里写代码
}

mergePromise([ajax1, ajax2, ajax3]).then((data) => {
  console.log('done');
  console.log(data); // data 为 [1, 2, 3]
});

// 要求分别输出
// 1
// 2
// 3
// done
// [1, 2, 3]
```

这道题有点类似于`Promise.all()`，不过`.all()`不需要管执行顺序，只需要并发执行就行了。但是这里需要等上一个执行完毕之后才能执行下一个。

解题思路：

- 定义一个数组`data`用于保存所有异步操作的结果
- 初始化一个`const promise = Promise.resolve()`，然后循环遍历数组，在`promise`后面添加执行`ajax`任务，同时要将添加的结果重新赋值到`promise`上。

答案：

```
function mergePromise (ajaxArray) {
  // 存放每个ajax的结果
  const data = [];
  let promise = Promise.resolve();
  ajaxArray.forEach(ajax => {
  	// 第一次的then为了用来调用ajax
  	// 第二次的then是为了获取ajax的结果
    promise = promise.then(ajax).then(res => {
      data.push(res);
      return data; // 把每次的结果返回
    })
  })
  // 最后得到的promise它的值就是data
  return promise;
}
```

**8.4 根据 promiseA+实现一个自己的 promise**

说真的，这道题被问到的概率还是挺高的，而且要说的内容也很多...

霖呆呆这里偷个懒，不想细说了...

不过哈，我保证，下下题我一定仔细说 😼.

来吧，给你们一些好的宝典：

- [《Promise 不会？？看这里！！！史上最通俗易懂的 Promise！！！》](https://juejin.im/post/5afe6d3bf265da0b9e654c4b#heading-7)
- [《写一个符合 Promises/A+ 规范并可配合 ES7 async/await 使用的 Promise》](https://zhuanlan.zhihu.com/p/23312442)

**8.5 封装一个异步加载图片的方法**

这个相对简单一些，只需要在图片的`onload`函数中，使用`resolve`返回一下就可以了。

来看看具体代码：

```javascript
function loadImg(url) {
  return new Promise((resolve, reject) => {
    const img = new Image();
    img.onload = function() {
      console.log("一张图片加载完成");
      resolve(img);
    };
    img.onerror = function() {
    	reject(new Error('Could not load image at' + url));
    };
    img.src = url;
  });
```

**8.6 限制异步操作的并发个数并尽可能快的完成全部**

有 8 个图片资源的 url，已经存储在数组`urls`中。

`urls`类似于`['https://image1.png', 'https://image2.png', ....]`

而且已经有一个函数`function loadImg`，输入一个`url`链接，返回一个`Promise`，该`Promise`在图片下载完成的时候`resolve`，下载失败则`reject`。

但有一个要求，任何时刻同时下载的链接**数量不可以超过 3 个**。

请写一段代码实现这个需求，要求**尽可能快速**地将所有图片下载完成。

```javascript
var urls = [
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/AboutMe-painting1.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/AboutMe-painting2.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/AboutMe-painting3.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/AboutMe-painting4.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/AboutMe-painting5.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/bpmn6.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/bpmn7.png",
  "https://hexo-blog-1256114407.cos.ap-shenzhen-fsi.myqcloud.com/bpmn8.png",
];
function loadImg(url) {
  return new Promise((resolve, reject) => {
    const img = new Image();
    img.onload = function() {
      console.log("一张图片加载完成");
      resolve(img);
    };
    img.onerror = function() {
    	reject(new Error('Could not load image at' + url));
    };
    img.src = url;
  });
```

看到这道题时，我最开始的想法是：

- 拿到`urls`，然后将这个数组每 3 个`url`一组创建成一个二维数组
- 然后用`Promise.all()`每次加载一组`url`（也就是并发 3 个），这一组加载完再加载下一组。

这个想法从技术上说并不难实现，有点类似于第三题。不过缺点也明显，那就是每次都要等到上一组全部加载完之后，才加载下一组，那如果上一组有`2`个已经加载完了，还有`1`个特别慢，还在加载，要等这个慢的也加载完才能进入下一组。这明显会照常卡顿，影响加载效率。

但是开始没有考虑这么多，因此有了第一个版本。

**如果你有兴趣可以看看想法一的代码，虽然对你没什么帮助，想直接知道比较好的做法的小伙伴请跳到想法二**

**想法一**💡：

```javascript
function limitLoad(urls, handler, limit) {
  const data = []; // 存储所有的加载结果
  let p = Promise.resolve();
  const handleUrls = (urls) => {
    // 这个函数是为了生成3个url为一组的二维数组
    const doubleDim = [];
    const len = Math.ceil(urls.length / limit); // Math.ceil(8 / 3) = 3
    console.log(len); // 3, 表示二维数组的长度为3
    for (let i = 0; i < len; i++) {
      doubleDim.push(urls.slice(i * limit, (i + 1) * limit));
    }
    return doubleDim;
  };
  const ajaxImage = (urlCollect) => {
    // 将一组字符串url 转换为一个加载图片的数组
    console.log(urlCollect);
    return urlCollect.map((url) => handler(url));
  };
  const doubleDim = handleUrls(urls); // 得到3个url为一组的二维数组
  doubleDim.forEach((urlCollect) => {
    p = p
      .then(() => Promise.all(ajaxImage(urlCollect)))
      .then((res) => {
        data.push(...res); // 将每次的结果展开，并存储到data中 (res为：[img, img, img])
        return data;
      });
  });
  return p;
}
limitLoad(urls, loadImg, 3).then((res) => {
  console.log(res); // 最终得到的是长度为8的img数组: [img, img, img, ...]
  res.forEach((img) => {
    document.body.appendChild(img);
  });
});
```

**想法二**💡：

参考[LHH 大翰仔仔-Promise 面试题](https://www.jianshu.com/p/4bb1521343ba)

既然题目的要求是保证每次并发请求的数量为 3，那么我们可以先请求`urls`中的前面三个(下标为`0,1,2`)，并且请求的时候使用`Promise.race()`来同时请求，三个中有一个先完成了(例如下标为`1`的图片)，我们就把这个当前数组中已经完成的那一项(第`1`项)换成还没有请求的那一项(`urls`中下标为`3`)。

直到`urls`已经遍历完了，然后将最后三个没有完成的请求(也就是状态没有改变的`Promise`)用`Promise.all()`来加载它们。

不多说，流程图都给你画好了，你可以结合流程图再来看代码。

为了方便你查看，我截了个图，不过代码在后面也有

(说真的，要我看这一大长串代码我也不愿意...)

代码：

```javascript
function limitLoad(urls, handler, limit) {
  let sequence = [].concat(urls); // 复制urls
  // 这一步是为了初始化 promises 这个"容器"
  let promises = sequence.splice(0, limit).map((url, index) => {
    return handler(url).then(() => {
      // 返回下标是为了知道数组中是哪一项最先完成
      return index;
    });
  });
  // 注意这里要将整个变量过程返回，这样得到的就是一个Promise，可以在外面链式调用
  return sequence
    .reduce((pCollect, url) => {
      return pCollect
        .then(() => {
          return Promise.race(promises); // 返回已经完成的下标
        })
        .then((fastestIndex) => {
          // 获取到已经完成的下标
          // 将"容器"内已经完成的那一项替换
          promises[fastestIndex] = handler(url).then(() => {
            return fastestIndex; // 要继续将这个下标返回，以便下一次变量
          });
        })
        .catch((err) => {
          console.error(err);
        });
    }, Promise.resolve()) // 初始化传入
    .then(() => {
      // 最后三个用.all来调用
      return Promise.all(promises);
    });
}
limitLoad(urls, loadImg, 3)
  .then((res) => {
    console.log('图片全部加载完毕');
    console.log(res);
  })
  .catch((err) => {
    console.error(err);
  });
```
