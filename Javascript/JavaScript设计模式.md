> JavaScript 设计模式  
> 张容铭著  
> 2015 年 8 月第一版  

# 第一篇 面向对象编程

面向对象编程（Object-oriented programming, OOP）是一种程序设计范型。它将对象作为程序的基本单元，将程序和数据封装其中，以提高程序的重用性、灵活性和扩展性。

## 第1章 灵活的语言——JavaScript

### 用对象收编变量。

可以将全局变量统一放在一个变量里保存，这样就可减少覆盖或被覆盖的风险。

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

真假对象。但是上面这个对象不能复制一份，或者说这个对象类在用 new 关键字创建新的对象时，新创建的对象时不能继承这些方法的。如果想要简单地复制一下对象，可以将这些方法放在一个函数对象中。

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

### 类也可以。

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

### 一个检测类。

但是有时候这么做造成的消耗是很奢侈的，因为这些新创建的对象都有自己的一套方法，需要处理一下。如下，创建出来的对象所拥有的方法就都是一个，因为它们都要依赖 prototype 原型依次寻找，而找到的方法都是同一个，它们都绑定在 CheckObject 对象类的原型上。

```JavaScript
var CheckObjectFive = function () {
};
// var CheckObject = function() {};
// CheckObject.prototype.checkName = function() {
//     // 验证姓名
// };
// CheckObject.prototype.checkEmail = function() {
//     // 验证邮箱
// };
// CheckObject.prototype.checkPassword = function() {
//     // 验证密码
// };
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

var c = new CheckObjectFive();
c.checkName();
c.checkEmail();
c.checkPassword();
```

### 方法还可以这样用。

使用该类多次调用了对象，这是可以避免的。可以在声明的每一个方法的末尾处将当前对象返回，在JavaScript 中 this 指向的就是当前对象。

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
var d = new CheckObjectSix();
d.checkName().checkEmail().checkPassword();
```

### 函数的祖先。

prototype.js 是一款 JavaScript 框架，里面为我们方便的封装了很多方法，最大的特点是对原生对象（JavaScript语言为们提供的对象类，如Function、Array、Object等等）的拓展。例如我们想给每一个函数都添加一个检测邮箱的方法可以这么做

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

这样做会无缘原生对象Function，所以别人创建的函数也会被你创建的函数所污染，造成不必要的开销，但是你可以抽象出一个统一添加方法的功能方法。

```js
Function.prototype.addMethod = function(name, fn) {
    this[name] = fn;
};

var methods = function() {};
// 或者 var methods = new Function();
methods.addMethod("checkName", function() {});
methods.addMethod("checkEmail", function() {});

// 调用
methods.checkEmail();
methods.checkName();
```

链式添加。分别对 addMethod 和 里面的方法进行链式调用。

```js
Function.prototype.addMethod = function(name, fn) {
    this[name] = fn;
    return this;
};

var methods = function() {};
methods.addMethod("checkName", function() {
  // 验证姓名
  return this;
}).addMethod("checkEmail", function() {
  // 验证邮箱
  return this;
});
methods.checkEmail().checkName();
```

换一种方式使用方法。采用类式调用的方法。

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

面向对象编程就是将你的需求抽象成一个对象，然后针对这个对象分析器特征（属性）与动作（方法）。这个对象我们称之为类。面向对象编程思想有一个特点就是封装，就是说把你需要的功能放在一个对象里。

### 2.2 包装明星——封装

在 javascript 中创建一个类很容易，首先声明一个函数保存在一个变量里。按编程习惯一般将这个代表类的变量名字母大写。然后在这个函数（类）的内部通过对 this 变量添加属性或者方法来实现对类添加属性或者方法。

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

属性与方法封装。

- 由于 javascript 的函数级作用域，声明在函数内部的变量以及方法在外界是访问不到的，通过此特性即可创建类的私有变量以及私有方法。
- 然而在函数内部通过 this 创建的属性和方法，在类创建对象时，每个对象自身都拥有一份并且可以在外部访问到。因此通过 this 创建的属性可看作是对象共有属性和对象共有方法。
- 通过 this 创建的方法，不但可以访问这些对象的共有属性与共有方法，而且还能访问到类（创建时）或对象自身的私有属性和私有方法，由于这些方法权利比较大，所以又可看成特权方法。
- 在对象创建时通过使用这些特权方法可以初始化实例对象的一些属性，因此这些在创建对象时调用的特权方法还可以看作是类的构造器。


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

闭包实现。闭包是有权访问另外一个函数作用域中变量的函数，即在一个函数内部创建另外一个函数。我们把这个闭包作为创建对象的构造函数，这样它既是闭包又是可实例对象的函数，即可访问到类函数作用域中的变量。有时候在闭包内部实现一个完整的类然后将其返回。

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

创建对象的安全模式。在JavaScript创建对象时有一种安全模式就可以安全解决忘记使用new关键字而引发的错误。

```js
/** 反面示例 */
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

# 第二篇 创建型设计模式

# 第三篇 结构性设计模式

# 第四篇 行为型设计模式

# 第五篇 技巧性设计模式

# 第六篇 架构型设计模式

# 附录 A
