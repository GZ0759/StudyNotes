> JavaScript 设计模式  
> 张容铭著  
> 2015 年 8 月第一版  

# 第一篇 面向对象编程

面向对象编程（Object-oriented programming, OOP）是一种程序设计范型。它将对象作为程序的基本单元，将程序和数据封装其中，以提高程序的重用性、灵活性和扩展性。

## 第1章 灵活的语言——JavaScript

### 1.3 用对象收编变量。

对象有属性和方法，如果想要访问它的属性或方法时，可以通过点语法向下遍历查询得到。因此可以创建一个检测对象，然后把方法放在里面。可以将全局变量统一放在一个变量里保存，这样就可减少覆盖或被覆盖的风险。

```JavaScript
var CheckObject = {
  checkName : function () {
    // 验证姓名
  },
  checkEmail : function () {
    // 验证邮箱
  },
  checkPassword : function () {
    // 验证密码
  }
}
```

### 1.4 对象的另一种形式

首先要声明一个对象，然后给它添加方法，当然在 JavaScript 中函数也是对象，所以可以这么做。

```JavaScript
var CheckObject = function(){};
CheckObject.checkName = function () {
  // 验证姓名
},
CheckObject.checkEmail = function () {
  // 验证邮箱
},
CheckObject.checkPassword = function () {
  // 验证密码
}
```

### 1.5 真假对象

但是上面这个对象不能复制一份，或者说这个对象类在用 new 关键字创建新的对象时，新创建的对象时不能继承这些方法的。如果想要简单地复制一下对象，可以将这些方法放在一个函数对象中。

```JavaScript
var CheckObject = function() {
  return {
    checkName : function () {
      // 验证姓名
    },
    checkEmail : function () {
      // 验证邮箱
    },
    checkPassword : function () {
      // 验证密码
    }
  }
}

var a = CheckObject();
a.checkEmail();
```

### 1.6 类也可以。

虽然创建了新对象完成了需求，但是它不是一个真正意义上类的创建方式，创建的对象与对象 CheckObject 没有任何关系。如下，把所有的方法放在函数内部，通过 this 定义，每一次通过 new 关键字创建新对象的时候，新创建的对象都会对类的 this 上的属性进行复制，所以这些新创建的对象都会有自己的一套方法。

```JavaScript
var CheckObjectThree = function () {
    this.checkName = function () {
        console.log("验证姓名");
    };
    this.checkEmail = function () {
        console.log("验证邮箱");
    };
    this.checkPassword = function () {
        console.log("验证密码");
    }
};

var a = new CheckObjectThree();
a.checkName();
a.checkEmail();
a.checkPassword();
```

### 1.7 一个检测类。

但是有时候这么做造成的消耗是很奢侈的，因为这些新创建的对象都有自己的一套方法，需要处理一下。如下，创建出来的对象所拥有的方法就都是一个，因为它们都要依赖 prototype 原型依次寻找，而找到的方法都是同一个，它们都绑定在 CheckObject 对象类的原型上。

```JavaScript
var CheckObjectFive = function () {
};
CheckObjectFive.prototype = {
    checkName: function () {
        console.log("验证姓名");
    },
    checkEmail: function () {
        console.log("验证邮箱");
    },
    checkPassword: function () {
        console.log("验证密码");
    }
};

var a = new CheckObjectFive();
a.checkName();
a.checkEmail();
a.checkPassword();
```

### 1.8 方法还可以这样用。

使用该类多次调用了对象，这是可以避免的。可以在声明的每一个方法的末尾处将当前对象返回，在JavaScript 中 this 指向的就是当前对象。当然也可以放到类的原型对象中。

```JavaScript
var CheckObjectSix = function () {
};
CheckObjectSix.prototype = {
    checkName: function () {
        console.log("验证姓名");
        return this;
    },
    checkEmail: function () {
        console.log("验证邮箱");
        return this;
    },
    checkPassword: function () {
        console.log("验证密码");
        return this;
    }
};
var a = new CheckObjectSix();
a.checkName().checkEmail().checkPassword();
```

### 1.9 函数的祖先。

prototype.js 是一款 JavaScript 框架，里面为我们方便的封装了很多方法，最大的特点是对原生对象（JavaScript语言为们提供的对象类，如Function、Array、Object等等）的拓展。例如我们想给每一个函数都添加一个检测邮箱的方法可以这么做。

```js
Function.prototype.checkEmail = function() {
    // 验证邮箱
};

// 这时候调用就比较方便了
var f = function() {};
f.checkEmail();

// 如果你习惯类的形式，也可以这么用
var f = new Function();
f.checkEmail();
```

但是这样做会无缘原生对象Function，所以别人创建的函数也会被你创建的函数所污染，造成不必要的开销，但是你可以抽象出一个统一添加方法的功能方法。

```js
Function.prototype.addMethod = function(name, fn) {
    this[name] = fn;
};

var methods = function() {};
// 或者 var methods = new Function();
methods.addMethod("checkName", function() {
    // 验证姓名
});
methods.addMethod("checkEmail", function() {
    // 验证邮箱
});

// 调用
methods.checkEmail();
methods.checkName();
```

### 1.10 可以链式添加吗

链式添加。分别对 addMethod 和里面的方法进行链式调用。

```js
Function.prototype.addMethod = function(name, fn) {
    this[name] = fn;
    return this;
};

var methods = function() {};
// 链式添加的添加方法
methods.addMethod("checkName", function() {
  // 验证姓名
  return this;
}).addMethod("checkEmail", function() {
  // 验证邮箱
  return this;
});

// 链接添加的方法调用
methods.checkEmail().checkName();
```

### 1.11 换一种方式使用方法。

上面在测试的时候，采用的是函数式调用方式，因此也可以采用类式调用的方法。

```js
Function.prototype.addMethod = function(name, fn) {
    this.prototype[name] = fn;
    return this;
};

var Methods = function() {};
Methods.addMethod("checkName", function() {
  // 验证姓名
}).addMethod("checkEmail", function() {
  // 验证邮箱
});

var m = new Methods()
m.checkName();
m.checkEmail();
```

### 我问你答。

- 真假对象一节中如何实现方法的链式调用呢？

只需在类中的每个方法中通过`this`关键字返回对象实例的引用。每次函数调用都会返回一个新对象，表面上是CheckObject对象，实际是返回的新对象，这样每次调用就不会相互影响了。

- 试着定义一个可以为函数添加多个方法的 addMethod 方法。
- 试着定义一个既可为函数原型添加方法又可唯器自身添加方法的 addMethod 方法


## 第2章 写的都是看到的——面向对象编程

### 2.1 两种编程风格——面向过程与面向对象

面向对象编程就是将需求抽象成一个对象，然后针对这个对象分析器特征（属性）与动作（方法）。这个对象我们称之为类。面向对象编程思想有一个特点就是封装，就是说把你需要的功能放在一个对象里。

遗憾的是对于 JavaScript 这种解释性的弱类型语言没有经典强类型语言中那种通过 class 等关键字实现的类的封装方式，JavaScript 中都是通过一些特性模仿实现的，但这也带来了极高的灵活性，让编写的代码更自由。

### 2.2 包装明星——封装

#### 2.2.1 创建一个类

在 javascript 中创建一个类很容易，首先声明一个函数保存在一个变量里。按编程习惯一般将这个代表类的变量名字母大写。然后在这个函数（类）的内部通过对 this 变量添加属性或者方法来实现对类添加属性或者方法。 this 是函数内部自带的一个变量，用于指向当前这个对象。

```js
var Book = function(id, bookname, price) {
    this.id = id;
    this.name = bookname;
    this.price = price;
};

var book = new Book(10, "JavaScript设计模式", 50);
console.log(book.bookname);
```

也可以通过在类的原型上添加属性和方法，有两种方式，一种是一一为原型对象属性赋值，另一种则是将一个对象赋值给类的原型对象，但这两种不要混用。

```js
Book.prototype.display = function() {
    // 展示这本书
};

// 或者
Book.prototype = {
    display: function() {}
};
```

两者的不同。通过类创建一个新对象时，this 指向的属性和方法都会得到相应的创建，而通过 prototype 继承的属性或者方法是每个对象通过 prototype 访问到，所以每次通过类创建一个新对象时这些属性和方法不会再次创建。

constructor 是一个属性，当创建一个函数或者对象时都会为其创建一个原型对象 prototype，在prototype 对象中又会像函数中创建 this 一样创建一个 constructor 属性，那么 constructor 属性指向的就是拥有整个原型对象的函数或对象。

#### 2.2.2 属性与方法封装。

由于 JavaScript 的函数级作用域，声明在函数内部的变量以及方法在外界是访问不到的，通过此特性即可创建类的私有变量以及私有方法。

然而在函数内部通过 this 创建的属性和方法，在类创建对象时，每个对象自身都拥有一份并且可以在外部访问到。因此通过 this 创建的属性可看作是对象共有属性和对象共有方法。

通过 this 创建的方法，不但可以访问这些对象的共有属性与共有方法，而且还能访问到类（创建时）或对象自身的私有属性和私有方法，由于这些方法权利比较大，所以又可看成特权方法。

在对象创建时通过使用这些特权方法可以初始化实例对象的一些属性，因此这些在创建对象时调用的特权方法还可以看作是类的构造器。


```js
// 私有属性与私有方法，对象公有属性和对象公有方法，构造器
var Book = function(id, name, price) {
    // 私有属性
    var num = 1;
    // 私有方法
    function checkId() {}
    // 特权方法
    this.getName = function() {};
    this.getPrice = function() {};
    this.setName = function() {};
    this.setPrice = function() {};
    // 对象公有属性
    this.id = id;
    this.copy = function() {};
    // 构造器
    this.setName(name);
    this.setPrice(price);
};
```

通过 new 关键字创建新对象时，由于类外面通过点语法添加的属性和方法没有执行到，所以新创建的对象中无法获取他们，但是可以通过类来使用。因此在类外面通过点语法定义的属性以及方法被称为静态共有属性和类的静态共有方法。而类通过 prototype 创建的属性或者方法在类实例的对象中是可以通过 this 访问到的，所以将 prototype 对象中的属性和方法称为共有属性和共有方法。

```js
// 类静态公有属性（对象不能访问）
Book.isChinese = true;
// 类静态公有方法（对象不能访问）
Book.resetTime = function() {
    console.log("new Time");
};
Book.prototype = {
    // 公有属性
    isJSBook: false,
    // 公有方法
    display: function() {}
};

var b = new Book(11, "JavaScript设计模式", 50);
console.log(b.num); // undefined
console.log(b.isJSBook);  // false
console.log(b.id);  // 11
console.log(b.isChinese); // undefined

console.log(Book.isChinese);  // true
Book.resetTime(); // new Time
```

#### 2.2.3 闭包实现。

闭包是有权访问另外一个函数作用域中变量的函数，即在一个函数内部创建另外一个函数。我们把这个闭包作为创建对象的构造函数，这样它既是闭包又是可实例对象的函数，即可访问到类函数作用域中的变量。有时候在闭包内部实现一个完整的类然后将其返回。

```js
var Book = (function() {
    // 静态私有变量
    var bookNum = 0;
    // 静态私有方法
    function checkBook(name) {}
    // 创建类
    function _book(newId, newName, newPrice) {
        // 私有变量
        var name, price;
        // 私有方法
        function checkID(id) {}
        // 特权方法
        this.getName = function() {};
        this.getPrice = function() {};
        this.setName = function() {};
        this.setPrice = function() {};
        // 公有属性
        this.id = newId;
        // 公有方法
        this.copy = function() {};
        bookNum++;
        if (bookNum > 100) {
            throw new Error("我们仅出版100本书。");
        }
        // 构造器
        this.setName(name);
        this.setPrice(price);
    }
    // 构造原型
    _book.prototype = {
        // 静态公有属性
        isJSBook: false,
        display: function() {}
    };
    // 返回类
    return _book;
})();
```

#### 2.2.4 创建对象的安全模式。

对于初学者来说，在创建对象上由于不适应这种写法，所以经常容易忘记使用 new 而犯错误。

```js
var Book = function(title, time, type) {
    this.title = title;
    this.time = time;
    this.type = type;
};
var book = Book("JavaScript", "2014", "js");
console.log(book); // undefined
console.log(window.title); // JavaScript
console.log(window.time); // 2014
console.log(window.type); // js
```

在 JavaScript 创建对象时有一种安全模式就可以安全解决忘记使用 new 关键字而引发的错误。

```js
/** 图书安全类 */
var Book = function(title, time, type) {
    // 判断执行过程中this是否是当前这个对象（如果是用new创建的）
    if (this instanceof Book) {
        this.title = title;
        this.time = time;
        this.type = type;
    } else {
        // 否则重新创建这个对象
        return new Book(title, time, type);
    }
};

var book = Book("javaScript", "2014", "js");

// 测试
console.log(book); // Book
console.log(book.title); // JavaScript
console.log(book.time); // 2014
console.log(book.type); // js
console.log(window.title); // undefined
console.log(window.type); // undefined
console.log(window.time); // undefined
```

### 3.3 传宗接代——继承

每个类都有3个部分。
- 构造函数内，供实例对象赋值用
- 构造函数外，直接通过点语法添加，供类使用
- 类的原型中，实例化对象可以通过其原型链间接访问到，也是为供所有实例化对象所共用。

类式继承。类的原型对象的作用就是为类的原型添加共有方法，但类不能直接访问这些属性和方法，必须通过原型 prototype 来访问。而实例化一个父类的时候，新创建的对象复制了父类的构造函数内的属性和方法并且将原型 `_proto_` 指向了父类的原型对象，这样就拥有了父类的原型对象上的属性与方法，并且这个新创建的对象可直接访问到父类原型对象上的属性和方法，也可以访问从父类构造函数中赋值的属性和方法。将这个对象赋值给子类的原型，那么这个子类的原型同样可以访问父类原型上的属性和方法与父类构造函数中复制的属性和方法。

```js
// 声明父类
function SuperClass() {
    this.superValue = true;
}
// 为父类添加公有方法
SuperClass.prototype.getSuperValue = function() {
    return this.superValue;
};
// 声明子类
function SubClass() {
    this.SubValue = false;
}

// 继承父类
SubClass.prototype = new SuperClass();
// 为子类添加公有方法
SubClass.prototype.getSubValue = function() {
    return this.SubValue;
};

var instance = new SubClass();
console.log(instance.getSuperValue()); // true
console.log(instance.getSubValue()); // false

console.log(instance instanceof SuperClass); // true
console.log(instance instanceof SubClass); // true
console.log(SubClass instanceof SuperClass); // false
console.log(SubClass.prototype instanceof SuperClass); // true
```

这种类式继承有两个缺点。
- 由于子类通过其原型 prototype 对父类实例化，继承了父类。所以说父类中的共有属性要是引用类型，就会在子类中被所有实例公用，因此一个子类的实例更改子类原型从父类构造器函数中继承来的共有属性就会直接影响到其他子类。
- 由于子类实现的继承是靠其原型 prototype 对父类的实例化实现的，因此在创建父类的时候，是无法向父类传递参数的，因而在实例化父类的时候也无法对父类构造函数内的属性进行初始化。

```js
function SuperClass() {
    this.books = ["JavaScript", "html", "css"];
}

function SubClass() {}
SubClass.prototype = new SuperClass();
var instance1 = new SubClass();
var instance2 = new SubClass();
console.log(instance2.books); // ["JavaScript", "html", "css"]
instance1.books.push("设计模式");
console.log(instance2.books); // ["JavaScript", "html", "css", "设计模式"]
```

创建即继承——构造函数继承。由于这类继承没有涉及原型prototype，所以父类的原型的方法自然不会被子类继承。`SuperClass.call(this, id);`这条语句是构造函数式继承的精华，由于 call 这个方法可以更改函数的作用环境，因此在子类中，对 superClass 调用这个方法就是将子类中的变量在父类中执行一遍，由于父类中是给 this 绑定属性的，因此子类自然也就继承了父类的共有属性。

由于这种类型的继承没有涉及原型 prototype，所以父类的原型方法自然不会被子类继承，而如果要想被子类继承就必须要放在构造函数中，这样创建出来的每个实例都会单独拥有一份而不能共用。

```js
// 声明父类
function SuperClass(id) {
    // 引用类型公有属性
    this.books = ["JavaScript", "html", "css"];
    // 值类型公有属性
    this.id = id;
}

// 父类声明原型方法
SuperClass.prototype.showBooks = function() {
    console.log(this.books);
};

// 声明子类
function SubClass(id) {
    // 继承父类
    SuperClass.call(this, id);
}

// 创建第一个子类的示例
var instance1 = new SubClass(10);
var instance2 = new SubClass(11);

instance1.books.push("设计模式");
console.log(instance1.books); // ["JavaScript", "html", "css", "设计模式"];
console.log(instance1.id); // 10
console.log(instance2.books); // ["JavaScript", "html", "css"]
console.log(instance2.id); // 11

instance1.showBooks(); // TypeError
```

将优点为我所用——组合继承。类式继承是通过子类的原型prototype对父类实例化来实现的，构造函数式继承是通过在子类的构造函数作用环境中执行一次父类的构造函数来实现的，组合继承只要同时做到两点即可。  
这种继承方式在使用构造函数继承时执行了一遍父类的构造函数，而在实现子类原型的类式继承时又调用了一遍父类构造函数，因此父类构造函数调用了两遍，所以这种继承方式并不是最完美的方式。

```js
/** 组合式继承 */
// 声明父类
function SuperClass() {
    // 值类型公有属性
    this.name = name;
    // 引用类型公有属性
    this.books = ["html", "css", "JavaScript"];
}

// 父类原型公有方法
SuperClass.prototype.getName = function() {
    console.log(this.name);
};

// 声明子类
function SubClass(name, time) {
    // 构造函数式继承父类属性
    SuperClass.call(this, name);
    // 子类中新增公有属性
    this.time = time;
}

// 类式继承 子类原型继承父类
SubClass.prototype = new SuperClass();
// 子类原型方法
SubClass.prototype.getTime = function() {
    console.log(this.time);
};

// 测试
var instance1 = new SubClass("js book", 2014);
instance1.books.push("设计模式");
console.log(instance1.books); // ["html", "css", "JavaScript", "设计模式"]
instance1.getName();  // js book;
instance1.getTime();  // 2014

var instance2 = new SubClass("css book", 2013);
console.log(instance2.books); // ["html", "css", "JavaScript"]
instance1.getName();  // css book;
instance1.getTime();  // 2013
```

洁净的继承者——原型式继承。它是类式继承的一个封装，其中的过渡对象就相当于类式集成中的子类，只不过在原型式中作为一个过渡对象出现的，目的是为了创建要返回的新的实例化对象。

```js
/** 原型式继承 */
function inheritObject(o) {
    // 声明一个过渡函数对象
    function F() {}
    // 过渡对象的原型继承符对象
    F.prototype = o;
    // 返回过渡对象的一个实例，该实例的原型继承了父对象
    return new F();
}

// 测试用例
var book = {
    name: "js book",
    alikeBook: ["css book", "html book"]
};

var newBook = inheritObject(book);
newBook.name = "ajax book";
newBook.alikeBook.push("xml book");

var otherBook = inheritObject(book);
otherBook.name = "flash book";
otherBook.alikeBook.push("as book");

console.log(newBook.name); // ajax book
console.log(newBook.alikeBook); // ["css book", "html book", "xml book", "as book"]
console.log(otherBook.name); // flash book
console.log(otherBook.alikeBook); // ["css book", "html book", "xml book", "as book"]
console.log(book.name); // js book
console.log(book.alikeBook); // ["css book", "html book", "xml book", "as book"]

/** 跟类式继承一样，引用类型的属性被共用 */
```

如虎添翼——寄生式继承。其实寄生式继承就是对原型继承的第二次封装，并且在第二次封装过程中对继承的对象进行了拓展，这样新创建的对象不仅仅有父类中的属性和方法而且还添加新的属性和方法。

```js
/** 寄生式继承 */
function inheritObject(o) {
    // 声明一个过渡函数对象
    function F() {}
    // 过渡对象的原型继承父对象
    F.prototype = o;
    // 返回过渡对象的一个实例，该实例的原型继承了父对象
    return new F();
}

// 声明基对象
var book = {
    name: "js book",
    alikeBook: ["css book", "html book"]
};

function createBook(obj) {
    // 通过原型继承方式创建新对象
    var o = new inheritObject(obj);
    // 拓展新对象
    o.getName = function(){
        console.log(name);
    };
    // 返回拓展后的新对象
    return o;
}
```

终极继承者——寄生组合式继承。寄生是寄生式继承，另外一种继承模式是构造函数继承。但是这里的寄生式继承有些特别，这里它处理的不是对象，而是类的原型。
```js
/**
 * 寄生式继承 继承原型
 * 传递参数 subClass  子类
 * 传递参数 superClass  父类
 **/

function inheritObject(o) {
    // 声明一个过渡函数对象
    function F() {}
    // 过渡对象的原型继承父对象
    F.prototype = o;
    // 返回过渡对象的一个实例，该实例的原型继承了父对象
    return new F();
}

function inheritPrototype(subClass, superClass) {
    // 复制一份父类的原型保存在变量中
    var p = inheritObject(superClass.prototype);
    p.constructor = subClass;
    subClass.prototype = p;
}

/** 测试用例 */
// 定义父类
function SuperClass(name) {
    this.name = name;
    this.colors = ["red", "blue", "green"];
}

//定义父类原型方法
SuperClass.prototype.getName = function() {
    console.log(this.name);
};

// 定义子类
function SubClass(name, time) {
    // 构造函数式继承
    SuperClass.call(this,name);
    // 子类增强属性
    this.time = time;
}

// 寄生式继承父类原型
inheritPrototype(SubClass,SuperClass);
// 子类新增原型方法
SubClass.prototype.getTime = function(){
    console.log(this.time);
};
// 创建两个测试方法
var instance1 = new SubClass("js book", 2014);
var instance2 = new SubClass("css book", 2013);

instance1.colors.push("black");
console.log(instance1.colors);  // ["red", "blue", "green", "black"]
console.log(instance2.colors);  // ["red", "blue", "green"]
instance2.getName();  // css book
instance2.getTime();  // 2013
```

### 2.4 老师不止一位——多继承

在 javascript 中继承是依赖于原型 prototype 链实现的，只有一条原型链，所以理论上是不能继承多个父类的。然而 javascript 是灵活的，通过一些技巧方法却可以继承多个对象的属性来实现类似的多继承。

extend 方法是一个浅复制过程，只能复制值类型的属性，对于引用类型的属性无能为力。而在 jquery 等一些框架中实现了深复制，就是将源对象中的引用类型的属性再执行一遍 extend 方法而实现的。

```js
/** 单继承 属性复制 */
var extend = function(target, source) {
    for (var property in source) {
        // 将对象中的属性复制到目标对象中
        target[property] = source[property];
    }
    // 返回目标对象
    return target;
};

// 测试用例
var book = {
    name: "JavaScript设计模式",
    alike: ["css", "html", "JavaScript"]
};
var anotherBook = {
    color: "blue"
};
extend(anotherBook, book);
console.log(anotherBook.name); // JavaScript设计模式
console.log(anotherBook.alike); // ["css", "html", "JavaScript"]

anotherBook.alike.push("ajax");
anotherBook.name = "设计模式";
console.log(anotherBook.name);  // 设计模式
console.log(anotherBook.alike); // ["css", "html", "JavaScript", "ajax"]
console.log(book.name); // JavaScript设计模式
console.log(book.alike);  // ["css", "html", "JavaScript", "ajax"]
```

mix 方法的作用就是将传入的多个对象的属性复制到源对象中，这样既可实现多个对象的属性的继承。也可以将他绑定到原生对象Object上，这样所有的对象就可以拥有这个方法了。

```js
/** 多继承 属性复制 */
var mix = function() {
    var i = 1, // 从第二个参数开始为被继承的对象
        leng = arguments.length, // 获取参数长度
        target = arguments[0], // 第一个参数为目标对象
        arg; // 缓存参数对象
    // 遍历被继承的对象
    for (; i < len; i++) {
        // 缓存当前对象
        arg = arguments[i];
        // 遍历被继承对象中的属性
        for (var variable in arg) {
            // 将被继承对象中的属性复制到目标对象中
            target[variable] = arg[variable];
        }
    }

    // 返回目标对象
    return target;
};

otherBook.mix(book1, book2);
console.log(otherBook);
```

### 2.5 多种调用方式——多态

多态，就是同一个方法多种调用方式。在 javascript 中也是可以实现的，只不过要对传入的参数做判断以实现多种调用方式吧。

```js
function add() {
    // 获取参数
    var arg = arguments,
        len = arg.length;
    switch (len) {
        // 如果没有参数
        case 0:
            return 10;
        case 1:
            return 10 + arg[0];
        case 2:
            return arg[0] + arg[1];
    }
}

// 测试用例
console.log(add()); // 10
console.log(add(5)); // 15
console.log(add(6, 7)); // 13
```

### 我问你答

多继承中通过对对象与方法浅复制实现继承，想一想如何才能实现深复制呢？（浅复制中复制对象的方法对象实质是一种指向引用，所以在深复制中要把对象中的引用类型属性细化成值类型拷贝到目标对象中）

# 第二篇 创建型设计模式

## 第3章 神奇的魔术师——简单工厂模式

简单工厂模式（Simple Factory）：又叫静态工厂方法，由一个工厂对象决定创建某一种产品对象类的实例。主要用来创建同一类对象。

用户输入的内容不符合规范时出现警示框。

```js
var LoginAlert = function(text) {
    this.content = text;
};
LoginAlert.prototype.show = function() {
    // 显示警示框
};
var userNameAlert = new LoginAlert('用户名不能多于16个字母或数字');
userNameAlert.show();

var passwordAlert = new LoginAlert();
passwordAlert.show('输入的密码不正确');

// 还有LoginConfirm、LoginPrompt类
```

将所有类封装在一个函数里，不用再关注这些对象依赖于哪个基类，这个函数通常也被称为工厂函数，这种模式叫简单工厂模式。

```js
var PopFactory = function(name) {
    switch (name) {
        case 'alert': 
            return new LoginAlert();
        case 'confirm': 
            return new LoginConfirm();
        case 'prompt': 
            return new LoginPrompt();
    }
}
```

简单工厂模式的理念就是创建对象，上面的方式是对不同的类实例化，不过除此之外简单工厂模式还可以用来创建相似对象。

```js
function createPop(type, text) {
    var o = new Object();
    o.content = text;
    o.show = function() {
        // 显示方法
    };
    if(type === 'alert') {
        // 警示框差异部分
    }
    if(type === 'prompt') {
        // 提示框差异部分
    }
    if(type === 'confirm') {
        // 确定框差异部分
    }
    return o;
}

var userNameAlert = createPop("alert", "用户名只能是26个字母和数字");
```

第一种是通过类实例化对象创建的，第二种是通过创建一个新对象然后包装增强其属性和功能来实现的。后面寄生方式创建的对象都是一个新的个体，所以他们的方法就不能公用了。

### 我问你答

谈谈简单工厂模式与类的异同点。

## 第4章 给我一张名片——工厂方法模式

工厂方法模式（Factory Method）：通过对产品类的抽象使其创建业务主要负责用于创建多类产品的实例。

工厂方法模式本意是说将实际创建对象工作推迟到子类当中。这样核心类就成了抽象类，在 javascript 中实现工厂方法模式只需要参考它的核心思想即可。所以可以将工厂方法看作是一个实例化对象的工厂类。为了安全起见，我们采用安全模式类，将创建对象的基类放在工厂方法类的原型中即可。

```js
/** 使用安全模式类可以屏蔽创建类的实例时，忽略使用new关键字造成的错误 */
var Demo = function() {
    if (!(this instanceof Demo)) {
        return new Demo();
    }
};

var d = Demo();
d.show(); // 成功获取！
```

安全的工厂方法。

```js
// 安全模式创建的工厂类
var Factory = function(type, content) {
    if (this instanceof Factory) {
        var s = new this[type](content);
        return s;
    } else {
        return new Factory(type, content);
    }
};

// 工厂原型中设置创建所有类型数据对象的基类
Factory.prototype = {
    Java: function(content) {
        // 将内容保存在content里面以备以后使用
        this.content = content;
        // 创建对象时，通过闭包，直接执行，将内容按需求的样式插入到页面内
        (function(content) {
            var div = document.createElement("div");
            div.innerHTML = content;
            div.style.color = "green";
            document.getElementById('container').appendChild(div);
        })(content);
    },
    Php: function(content) {
        // ......
    },
    JavaScript: function(content) {
        // ......
    }
};

var data = [{
    type: "JavaScript",
    content: "JavaScript哪家强"
}, {
    type: "Java",
    content: "Java哪家强"
}, {
    type: "php",
    content: "php哪家强"
}];

for (var i = 0; i < data.length; i++) {
    Factory(data[i].type, data[i].content);
}
```

### 我问你答

通过工厂方法模式为页面创建不同功能的按钮。

## 第5章 出现的都是幻觉——抽象工厂模式

抽象工厂模式（Abstract Factory）：通过对类的工厂抽象使其业务用于对产品类簇的创建，而不负责创建某一类产品的实例。

抽象类是一种声明但不能使用的类，使用的话就会报错。但是 javascript 是灵活的，所以可以在类的方法中手动地抛出错误来模拟抽象类。产品簇中声明一些必备的方法，如果子类中没有去重写就会抛出错误。

抽象类中定义的方法只是显性的定义一些功能。但没有具体的实现，而一个对象是要具有一套完整的功能的，所以用抽象类创建的对象当然也是“抽象”的了，所以我们不能使用它来创建一个真实的对象，一般用来它作为父类来创建一些子类。

## 第6章 分即是合——建造者模式

建造者模式 将一个复杂对象的构建层与其表示层相互分离，同样的构建过程可采用不同的表示。

建造者模式与工厂模式的区别。工厂模式主要是为了创建对象实例或者类簇（抽象工厂），关心的是最终产出（创建）的是什么。不关心你创建的整个过程，仅仅需要知道你最终创建的结果。所以通过工厂模式我们得到的都是对象实例或者族类。然而建造者模式在创建对象是要更为复杂一些，虽然其目的也是为了创建对象，但是他更多关心的是穿件这个对象的整个过程，甚至于创建对象的每一个细节。

以前工厂模式创建出来的是一个对象，他追求的是创建的结果，别无他求，所以那仅仅是一个实实在在的创建过程，而建造者模式就有所不同，他不仅仅可以得到创建的结果，而且也参与了创建的具体过程，对于创建的具体实现的细节也参与了干涉，所以说创建的对象更复杂，或者说这种模式创建的对象是一个复合对象。

## 第7章 语言之魂——原型模式

原型模式。用原型实例指向创建对象的类，适用于创建新的对象的类共享原型对象的属性基方法。

## 第8章 一个人的寂寞——单例模式

单例模式，又被称为单体模式，是只允许实例化一次的对象类。有时候我们也用一个对象来规划一个命名空间，并井井有条的管理对象的属性与方法。

# 第三篇 结构性设计模式

## 第9章 套餐服务——外观模式
## 第10章 水管弯弯——适配器模式
## 第11章 牛郎织女——代理模式
## 第12章 房子装修——装饰者模式
## 第13章 城市间的公路——桥接模式
## 第14章 超值午餐——组合模式
## 第15章 城市公交车——享元模式

# 第四篇 行为型设计模式

## 第16章 照猫画虎——模板方法模式
## 第17章 通信卫星——观察者模式
## 第18章 超级玛丽——状态模式
## 第19章 活诸葛——策略模式
## 第20章 有序车站——职责链模式
## 第21章 命令模式
## 第22章 驻华大使——访问者模式
## 第23章 媒婆——中介者模式
## 第24章 做好笔录——备忘录模式
## 第25章 点钞机——迭代器模式
## 第26章 翻译语言——解释器模式

# 第五篇 技巧性设计模式

## 第27章 永无尽头——链模式
## 第28章 未来预言家——委托模式
## 第29章 数据管理器——数据访问对象模式
## 第30章 执行控制——节流模式
## 第31章 卡片拼图——简单模板模式
## 第32章 机器学习——惰性模式
## 第33章 异国战场——参与者模式
## 第34章 入场仪式——等待者模式

# 第六篇 架构型设计模式

## 第35章 死心眼——同步模块模式
## 第36章 大心脏——异步模块模式
## 第37章 分而治之——Widget模式
## 第38章 三人行——MVC模式
## 第39章 三军统帅——MVP模式
## 第40章 视图的逆袭——MVVM模式

# 附录 A
