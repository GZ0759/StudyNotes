> JavaScript设计模式  
> Addy Osmani 著  
> 徐涛 译  
> 2013年 06 月 第一版  
> [开源图书原文地址](https://addyosmani.com/resources/essentialjsdesignpatterns/book/index.html)  
> [译文地址](https://www.oschina.net/translate/learning-javascript-design-patterns)  
> [W3Cschool](https://www.w3cschool.cn/zobyhd/)  

# 第1章 介绍

编写易于维护的代码，其中一个最重要方面是能够找到代码中重复出现的主题并优化它们。这也是设计模式有价值的地方。

# 第2章 什么是模式

模式是一种可复用的解决方案，可用于解决软件设计中遇到的常见问题，如在我们编写的 JavaScript 应用程序的实例中。另一种模式的方式是将解决问题的方法制作成模板，并且这些模板可应用于多种不同的情况。

设计模式有三大好处。

- 模式是已经验证的解决之道
- 模式很容易被复用
- 模式富有表达力

模式的一些其他优点。

- 复用模式有助于防止开发过程中，小问题引发的大问题。可以在结构上少花时间，从而有更多时间专注于整体解决方案的质量。
- 模式可以提供通用的解决方案，并且其记录方式不需要与某个特定问题挂钩。
- 某些模式确实能够通过避免代码复用来减少代码的总体资源占用量。
- 模式添加到开发人员的词汇中，会使沟通更快速。
- 经常使用的模式可以逐步改进，因为其他开发人员使用这些模式后总结出的共同经验又贡献给了设计模式社区。

**我们每天都在使用模式**

为页面上每个具有“foo”类的class属性的DOM元素增加一个计数器，查询列表最有效的方法？

1. 在页面上选择所有元素并存储，接着过滤该集合并使用正则表达式（或另一种方式）来存储那些具有“foo”类的元素
2. 使用浏览器原生的`querySelectorAll()`等功能来选择所有具有“foo”类的元素
3. 使用原生特性`getElementsByClassName()`等功能来重新获得所需的集合。

最快的实际是第三种，他比其他方法快8至10倍。但在实际应用中，IE9一下的版本不支持第三种方法，因此必须使用第一种方法，其他方法行不通。

使用jQuery的开发人员不必担心这个问题，因为通过使用Facade(外观)模式，它已经被抽象出来了，该模式为若干更复杂的底层代码体提供了一套简单的抽象接口(例如`$el.css()`和`$el. animate()`)正如我们看到的，这意味着在实现级细节上花费更少的时间。根据现有浏览器的支持范围，jQuery会在幕后选择最佳的元素选择方式，我们只需要使用抽象层即可。

# 第3章 模式状态测试、Proto模式及三法则

在学习设计模式时,我们不时会碰到“原始模式(proto-pattern)”这个词：一种尚未通“模式”测试的设计模式。原始模式是值得与社区分享的特殊解决方案，来自社区编程人员的心血，但因为产生的时间短，还没有机会对它们进行严格的审查。

如果模式可以执行以下操作，就被认为是“优秀”的模式

- 解决特殊问题
- 没有显而易见的解决方案
- 描述业经验证的概念
- 描述一种关系

成为有效模式的其中一个附加要求是,它们展示一些反复出现的现象。这通常可以限定在至少三个关键领域中,被称为三法则。使用该规则重现,则必须证明如下:

- 适合性
- 实用性
- 适用性

# 第4章 设计模式的结构

模式是最初提出的一种在两者之间建立关系的规则：

- 上下文
- 上下文里产生的元件系统
- 解决元件在上下文中自身问题的配置

一种设计模式应该具有：

- 模式名称和相应的描述
- 上下文大纲。模式在上下文中有效，以满足用户的需求
- 问题概述。问题的陈述已解决，因此可以理解模式的意图
- 解决方案。以可理解的步骤和看法解决用户问题的描述
- 设计。模式设计的描述，特别是与它交互的用户行为
- 实现。有关如何实现模式的指导
- 插图。模式中类的可视表示（如图表）
- 示例。最小形式的模式实现
- 辅助条件。需要那些其他模式来支持所描述模式的使用？
- 关系。这种模式像哪些模式？它是否极力模仿其他模式呢？
- 已知的用法。是广泛使用的模式？如果是这样，在哪里使用？如何使用？
- 讨论。团队或者作者对该模式所带来巨大好处的想法。

在一个组织或团队中，当在同一页面上创建和维护的解决方案时，对所有涉及到的开发者来说，设计模式能帮上大忙。如果考虑到你自己的工作模式，记住，虽然他们可能在制定计划和编写阶段，有一个较大的初期成本投入，但从投资方返回的值是值得的。然而，新的模式工作前，务必深入研究，你会发现它比起重新开始，更有利于使用或建立比现有的行之有效的模式之上。

# 第5章 编写设计模式

如果有兴趣创建新的设计模式，以下是一些建议：

- 模式的实用性：确保该模式描述了针对反复出现的问题的经过验证的解决方案，而不仅仅是描述了尚未经过验证的推测性解决方案。
- 牢记最佳实践：我们所做的设计决策应基于我们从对最佳实践的理解中得出的原则。
- 设计模式对用户应该透明：设计模式对任何类型的用户体验都应该完全透明。它们主要是用来为使用它们的开发人员提供服务的，不应强迫用户体验中的行为发生变化，而这些行为如果不使用模式就不会发生。
- 独创性在模式设计中不是重点：编写模式时，我们不必是记录在案的解决方案的原始发现者，也不必担心我们的设计会与其他模式的次要部分重叠。如果该方法足够强大以具有广泛的有用适用性，则有可能被认为是有效模式。
- 模式需要一批有说服力的示例：良好的模式描述之后必须要有一组同样强大的示例，以证明我们的模式已成功应用。为了显示广泛的用途，具有良好设计原则的示例是理想的。

模式编写是在创建通用、具体及有用的设计方面找到一种细致的平衡，要努力确保所编写的模式能够覆盖最广发的应用领域。

# 第6章 反模式

提出了两种反模式概念。

- 描述特定问题的不良解决方案，该方案会导致糟糕的情况发生
- 描述如何摆脱前述的糟糕情况以及如何创造好的解决方案

关于这个主题，Alexander撰写了在良好的设计结构和良好的上下文之间取得良好平衡的困难：

“这些说明是关于设计过程的；为了响应功能而发明的物理事物显示新的物理顺序，组织，形式的过程。每个设计问题都始于努力实现两个实体之间的适应性：所讨论的形式及其上下文。表格是解决问题的方法。上下文定义了问题”。

反模式是一个值得记录的不良设计。JavaScript中的反模式示例如下：

- 通过在全局上下文中定义大量变量来污染全局名称空间
- 将字符串而不是函数传递给`setTimeout`或`setInterval`，因为这会触发`eval()`内部使用。
- 修改Object类原型（这是一个非常糟糕的反模式）
- 以内联形式使用JavaScript，因为这不灵活
- 在更适合使用原生DOM方法（例如`document.createElement`）的地方使用`document.write`。

# 第7章 设计模式类别

著名设计书《域驱动术语》中的词汇表正确地指出：

“设计模式可以命名，抽象和标识通用设计结构的关键方面，从而使它对于创建可重用的面向对象设计很有用。设计模式标识参与的类及其实例，它们的角色和协作以及职责分配。

每个设计模式都针对特定的面向对象设计问题。它描述了何时应用，是否可以根据其他设计约束来应用，使用的后果和取舍。由于我们最终必须实现设计，因此设计模式还提供了示例代码来说明实现。

尽管设计模式描述了面向对象的设计，但它们基于已在主流面向对象编程语言中实现的实用解决方案……。”

设计模式可以分为许多不同的类别。

**创建型设计模式**

创建性设计模式着重于处理对象创建机制，其中以适合我们所处情况的方式创建对象。否则，对象创建的基本方法可能会导致项目增加复杂性，而这些模式旨在通过以下方式解决此问题：控制创建过程。属于此类别的一些模式是：构造函数，工厂，抽象，原型，单例和构建器。

**结构型设计模式**

结构模式与对象组成有关，通常会识别实现不同对象之间关系的简单方法。它们有助于确保当系统的一部分发生更改时，系统的整个结构都不需要这样做。它们还有助于将系统中不适合特定用途的部分重铸到适合的部分。属于此类别的模式包括：装饰器，外观，Flyweight，适配器和代理。

**行为设计模式**

行为模式集中于改善或简化系统中不同对象之间的通信。一些行为模式包括：迭代器，中介器，观察者和访客。

# 第8章 设计模式分类

## 8.1 有关类的要点

此表中将有一些引用“类”概念的模式。在ES5中，JavaScript是一种无类语言，但是可以使用函数来模拟类。

实现此目的最常见的方法是定义一个JavaScript函数，然后在其中使用new关键字创建一个对象。this可用于帮助定义对象的新属性和方法，如下所示：

```js
// A car "class"
function Car( model ) {
 
  this.model = model;
  this.color = "silver";
  this.year = "2012";
 
  this.getInfo = function () {
    return this.model + " " + this.year;
  };
 
}
```

然后，我们可以使用上面定义的Car构造函数实例化对象。

```js
var myCar = new Car("ford");
 
myCar.year = "2010";
 
console.log( myCar.getInfo() );
```

## 8.2 创建型模式

创建型模式Creational，是基于创建对象的概念。

- Class
  - Factory Method（工厂方法）。基于接口数据或事件生成几个派生类的一个实例。
- Object
  - Abstract Factory（抽象工厂）。创建若干类系列的一个实例，无需详述具体的类。
  - Builder （生成器）。从表示中分离对象构建，而总是创建相同类型的对象。
  - Prototype（原型）。用于赋值或克隆完全初始化的实例。
  - Singleton（单例）。一个类在全局访问点只有唯一一个实例。

## 8.3 结构型模式

结构型模式Structural，是根据构建对象块的思想。

- Class
  - Adapter（适配器）。匹配不同类的接口，因此类可以在不兼容接口的情况下共同工作。
- Object
  - Adapter（适配器）。匹配不同类的接口，因此类可以在不兼容接口的情况下共同工作。
  - Bridge（桥接）。将对象接口从其实现中，因此它们可以独立进行变化。
  - Composite（组合）。简单和复合对象的结构，使对象的总和不只是它各部分的总和。
  - Decorator（装饰器）。向对象动态的添加备选的处理。
  - Facada（外观）。隐藏整个子系统复杂性的唯一一个类。
  - Flyweight（享元）。 一个用于实现包含在别处信息的高效共享的细粒度实例。
  - Proxy（代理）。占位符对象代表真正的对象。

## 8.4 行为模式

行为模式Behavioral，是基于对象在一起配合工作的方式。

- Class
  - Interpreter（解释器）。将语言元素包含在应用程序中的方法，以匹配预期语言的语法。
  - Template Method（模板方法）。在一个方法中为某个算法建立一层外壳，将算法的具体步骤交付给子类去做。
- Object
  - Chain of Responsibility（响应链）。在对象链之间传递请求的方法，以找到能够处理请求的对象。
  - Command（命令）。将命令执行从其调用程序中分离的方法。
  - Iterator（迭代器）。顺序访问一个集合中的元素，无需了解该集合的内部工作原理。
  - Mediator（中介者模式）。在类之间定义简化的通信，以防止一组类显示引用彼此。
  - Memento（备忘录）。捕获对象的内部状态，以能够在以后恢复它。
  - Observer（观察者模式）。向多个类通知改变的方式，以确保类之间的一致性。
  - State（状态）。状态改变时，更改对象行为。
  - Strategy（策略）。在一个类中封装算法，将选择与实现分离。
  - Visitor（访问者）。向类添加一个新的操作，无需改变类。

# 第9章 JavaScript设计模式

## 9.1 构造器模式

在经典面向对象编程语言中，Constructor（构造器）是一种在内存已分配给该对象的情况下，用来初始化新创建对象的特殊方法。在JavaScript中，几乎所有的东西都是对象，我们通常最感兴趣的是 object 构造器。

Object 构造器用于创建特定类型的对象——准备好对象以备使用，同时接收构造器可以使用的参数，以在第一次创建对象时，设置成员属性和方法的值。

### 9.1.1 对象创建

下面是我们创建对象的三种基本方式。最后一个例子中"Object"构造器创建了一个针对特殊值的对象包装，只不过这里没有传值给它，所以它将会返回一个空对象。

```js
var newObject = {};
// or
var newObject = Object.create( null );
// or
var newObject = new Object();
```

有四种方式可以将一个键值对赋给一个对象:   
ECMAScript 3 兼容形式。包括点语法（Dot syntax）和中括号语法（Square bracket syntax）。

```js
newObject.someKey = "Hello World";
var key = newObject.someKey;

newObject["someKey"] = "Hello World";
var key = newObject["someKey"];
```

只适用 ECMAScript 5 的方式。包括`Object.defineProperty`和 `Object.defineProperties`。

```js
Object.defineProperty( newObject, "someKey", {
    value: "for more control of the property's behavior",
    writable: true,
    enumerable: true,
    configurable: true
});
// 简写
var defineProp = function ( obj, key, value ){
  config.value = value;
  Object.defineProperty( obj, key, config );
};
// 为了使用它，我们要创建一个“person”对象
var person = Object.create( null );
// 用属性构造对象
defineProp( person, "car",  "Delorean" );
defineProp( person, "dateOfBirth", "1981" );
defineProp( person, "hasBeard", false );

// 设置属性
Object.defineProperties( newObject, {
  "someKey": { 
    value: "Hello World", 
    writable: true 
  },
  "anotherKey": { 
    value: "Foo bar", 
    writable: false 
  } 

});
```

在这本书的后面一点，这些方法会被用于继承，如下：

```js
// 创建一个继承与Person的赛车司机
var driver = Object.create( person );

// 设置司机的属性
defineProp(driver, "topSpeed", "100mph");

// 获取继承的属性 (1981)
console.log( driver.dateOfBirth );

// 获取我们设置的属性 (100mph)
console.log( driver.topSpeed );
```

### 9.1.2 基本构造器

正如我们先前所看到的，Javascript不支持类的概念，但它确实支持与对象一起用的 constructor（构造器）函数。使用new关键字来调用该函数，使Javascript像使用构造器一样实例化一个新对象，并且对象成员由该函数定义。

在构造器中，关键字this引用新创建的对象。一个基本的构造器看起来是这个样子:

```js
function Car( model, year, miles ) {

  this.model = model;
  this.year = year;
  this.miles = miles;

  this.toString = function () {
    return this.model + " has done " + this.miles + " miles";
  };
}

// 使用:

// 我们可以示例化一个Car
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );

// 打开浏览器控制台查看这些对象toString()方法的输出值
// output of the toString() method being called on
// these objects
console.log( civic.toString() );
console.log( mondeo.toString() );
```

上面这是个简单版本的构造器模式，但它还是有些问题。一个是难以继承，另一个是每个Car构造函数创建的对象中，`toString()`之类的函数都被重新定义。这不是非常好，理想的情况是所有Car类型的对象都应该引用同一个函数。 值得庆幸的是，因为有很多 ES3 和ES5 兼容替代方法能够用于创建对象，所以很容易解决这个限制问题。

### 9.1.3 使用“原型”的构造器

在Javascript中函数有一个prototype的属性。调用JavaScript 构造器创建一个对象后，新对象就会具有构造器原型的所有属性。通过这种方式，就可以创建多个访问相同prototype的Car对象了。注意这里我们使用 `Object.prototype.newMethod` 而不是 `Object.prototype` ，以避免我们重新定义原型对象。
```js
function Car( model, year, miles ) {

  this.model = model;
  this.year = year;
  this.miles = miles;

}

Car.prototype.toString = function () {
  return this.model + " has done " + this.miles + " miles";
};

// 使用:

var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );

console.log( civic.toString() );
console.log( mondeo.toString() );
```

通过上面代码，单个`toString()`实例被所有的Car对象所共享了。

## 9.2 模块模式

Module（模块）是任何健壮的应用程序架构中不可或缺的一部分，它通常能够帮助我们清晰地分析和组织项目中的代码单元。

在JavaScript中，有几种用于实现模块的方法。

- 对象字面量表示法
- Module 模式
- AMD模块
- CommonJS 模块
- ECMAScript Harmony 模块

我们在书中后面的现代模块化JavaScript设计模式章节中将探讨这些选项中的最后三个。Module模式在某种程度上时基于对象字面量的，因此首先重新认识对象字面量是由意义的。

### 9.2.1 对象字面量

在对象字面量表示法中，一个对象被描述为一组包含在大括号`{}`中、以逗号分隔的 name/value 对。对象内的名称可以是字符串或标识符，后面跟着一个冒号。对象中最后的一个 name/value 对的后面不用加逗号，如果加将会导致出错。

```js
var myObjectLiteral = {
    variableKey: variableValue,
    functionKey: function () {
      // ...
    };
};
```

对象字面量不需要使用new运算符进行实例化，但不能用在一个语句的开头，因为开始的可能被解读为一个块的开始。在对象的外部，新成员可以使用如下赋值语句添加到对象字面量中，如`myModule.property="someValue"`。

```js
var myModule = {

  myProperty: "someValue",

  myConfig: {
    useCaching: true,
    language: "en"
  },

  myMethod: function () {
    console.log( "Where in the world is Paul Irish today?" );
  },

  myMethod2: function () {
    console.log( "Caching is:" + ( this.myConfig.useCaching ) ? "enabled" : "disabled" );
  },

  myMethod3: function( newConfig ) {

    if ( typeof newConfig === "object" ) {
      this.myConfig = newConfig;
      console.log( this.myConfig.language );
    }
  }
};

// 输出: Where in the world is Paul Irish today?
myModule.myMethod();

// 输出: Caching is:enabled
myModule.myMethod2();

// 输出: fr
myModule.myMethod3({
  language: "fr",
  useCaching: false
});
```

使用对象字面量有助于封装和组织代码。如果你想近一步了解对象字面量可以阅读 Rebecca Murphey 写过的关于此类话题的更深入的[文章](http://rmurphey.com/blog/2009/10/15/using-objects-to-organize-your-code)。

也就是说，如果我们选择了这种技术，我们可能对模块模式有同样的兴趣。它仍然使用对象字面量，但只是作为一个作用域函数的返回值。

### 9.2.2 模块化模式

模块模式最初被定义为一种在传统软件工程中为类提供私有和公有封装的方法。在JavaScript中，模块化模式用来进一步模拟类的概念，通过这种方式，能够使一个单独的对象拥有公有/私有方法和变量，从而屏蔽来自全局作用域的特殊部分。产生的结果是：函数与页面上其它脚本定义的函数冲突的可能性降低。

**私有**
模块模式使用闭包封装“私有”状态和组织。它提供一种包装混合公有或私有方法、变量的方式，防止其泄露至全局作用域，或者与别的开发人员的接口发生冲突。通过该模式，只需返回一个公有API，而其他的一切则都维持在私有闭包里。

这为我们提供了一个屏蔽处理底层事件逻辑的整洁解决方案，同时只暴露一个接口供应用程序的其他部分使用。该模式除了返回一个对象而并不是函数之外，非常类似于一个立即调用的函数表达式。

应该指出的是，在js中没有正真意义上的“私有”，因为js没有访问修饰符，因此我们使用函数作用域来模拟这个概念。在Module模式内：闭包声明的变量和方法只在该模式内部可用。但在返回对象上定义的变量和方法，则对外部使用者都是可用的。

**历史**
从历史角度来看，模块模式最初是在2003年由一群人共同发展出来的，这其中包括Richard Cornford。后来通过Douglas Crockford的演讲，逐渐变得流行起来。另外一件事情是，如果你曾经用过雅虎的YUI库，你会看到其中的一些特性和模块模式非常类似，而这种情况的原因是在创建YUI框架的时候，模块模式极大的影响了YUI的设计。

**例子**
下面这个例子通过创建一个自包含的模块实现了模块模式。

```js
var testModule = (function () {
  var counter = 0;
  return {
    incrementCounter: function () {
      return counter++;
    },
    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };
})();

// 增加计数器
testModule.incrementCounter();

// 检查计数器值并重置
testModule.resetCounter();
```

在这里我们看到，其它部分的代码不能直接访问我们的`incrementCounter()` 或者 `resetCounter()`的值。counter变量被完全从全局域中隔离起来了，因此其表现的就像一个私有变量一样，它的存在只局限于模块的闭包内部，因此只有两个函数可以访问counter。我们的方法是有名字空间限制的，因此在我们代码的测试部分，所有的调用都需要加上前缀(例如"testModule")。

使用模块模式时，可能会觉得它可以用来定义一个简单的模板来入门。下面是一个包含命名空间、公有和私有变量的模块模式。

```js
var myNamespace = (function () {

  var myPrivateVar, myPrivateMethod;

  // 私有计数器变量
  myPrivateVar = 0;

  // 记录所有参数的私有函数
  myPrivateMethod = function( foo ) {
      console.log( foo );
  };

  return {

    // 公有变量
    myPublicVar: "foo",

    // 调用私有变量和方法的公有函数
    myPublicFunction: function( bar ) {

      // 增加私有计数器值
      myPrivateVar++;

      // 传入 bar 调用私有方法
      myPrivateMethod( bar );

    }
  };

})();
```

看一下另外一个例子，下面我们看到一个使用这种模式实现的购物车。这个模块完全自包含在一个叫做basketModule 全局变量中。模块中的购物车数组是私有的，应用的其它部分不能直接读取。它只与模块的闭包一起存在，因此只有可以访问其域的方法可以访问这个变量。

```js
var basketModule = (function () {
  var basket = [];
  function doSomethingPrivate() {
    //...
  }
  function doSomethingElsePrivate() {
    //...
  }
  // 返回一个暴露出的公有对象
  return {
    // 添加item到购物车
    addItem: function( values ) {
      basket.push(values);
    },
    // 获取购物车里的item数目
    getItemCount: function () {
      return basket.length;
    },
    // 私有函数的公有形式别名
    doSomething: doSomethingPrivate,

    // 获取购物车里所有item的价格总值
    getTotal: function () {
      var q = this.getItemCount(),
          p = 0;
      while (q--) {
        p += basket[q].price;
      }
      return p;
    }
  };
}());
```

在这个模块中，可能已经注意到返回了一个对象。它被自动赋值给 basketModule ，以便我们可以与它交互。

```js
basketModule.addItem({
  item: "bread",
  price: 0.5
});

basketModule.addItem({
  item: "butter",
  price: 0.3
});

// Outputs: 2
console.log( basketModule.getItemCount() );

// Outputs: 0.8
console.log( basketModule.getTotal() );

// Outputs: undefined
console.log( basketModule.basket );

// Uncaught ReferenceError: basket is not defined
console.log( basket );
```

上面的方法都处于basketModule 的名字空间中。

请注意在上面的basket模块中域函数是如何在我们所有的函数中被封装起来的，以及我们如何立即调用这个域函数，并且将返回值保存下来。这种方式有以下的优势：

- 只有模块自身才能享有拥有私有函数的自由，因为它只会暴露我们输出的API。
- 鉴于函数往往已声明并命名，在试图找到哪些函数抛出异常时，这将使得在调试器中显示调用堆栈变得更容易。
- 根据环境，还可以让我们返回不同的函数。

### 9.2.3 模块模式变化

**引入混合**

模式的这种变化展示了全局变量（如jQuery、Underscore）如何作为参数传递给模块的匿名函数。这允许我们引入它们，并按照我们所希望的为它们取个本地别名。

```js
// 全局模块
var myModule = (function (jQ, _) {
  function privateMethod1() {
    jQ(".container").html("test");
  }
  function privateMethod2() {
    console.log(_.min([10, 5, 100, 2, 1000]));
  }
  return {
    publicMethod: function () {
      privateMethod1();
    }
  };
// 引入jQuery和Underscore
})(jQuery, _));
myModule.publicMethod();
```

**引出**

下一个变化允许我们声明全局变量，而不需实现它们，并可以同样地支持上一个示例中的全局引入的概念。

```js
// 全局模块
var myModule = (function () {
  // 模块对象
  var module = {},
    privateVariable = "Hello World";
  function privateMethod() {
    // ...
  }
  module.publicProperty = "Foobar";
  module.publicMethod = function () {
    console.log( privateVariable );
  };

  return module;
}());
```

### 9.2.4 工具包和特定框架的模块模式实现。

**Dojo**

Dojo 提供了一种和对象一起用的便利方法`dojo.setObject()`。其第一个参数是用点号分割的字符串，如`myObj.parent.child`，它在parent对象中引用一个称为child的属性，parent对象是在myObj内部定义。我们可以使用`setObject()`设置子级的值（比如属性等），如果中间对象不存在的话，也可以通过点号分割将中间的字符作为中间对象进行创建。

例如，如果我们声明商店命名空间的对象basket.coreas，可以实现使用传统的方式如下：

```js
var store = window.store || {};

if ( !store["basket"] ) {
  store.basket = {};
}

if ( !store.basket["core"] ) {
  store.basket.core = {};
}

store.basket.core = {
  // ...rest of our logic
};
```

或使用Dojo1.7（AMD兼容的版本）及以上如下：

```js
require(["dojo/_base/customStore"], function (store) {
  // 使用 dojo.setObject()
  store.setObject("basket.core", (function () {
    var basket = [];
    function privateMethod() {
      console.log(basket);
    }
    return {
      publicMethod: function (){
          privateMethod();
      }
    };
  })());
});
```

**ExtJS**

对比那些使用Sencha ExtJS的人，你的运气会好一点，因为官方文档包含了一些示例，演示了EXTJS框架下如何正确使用Module模式。

在这里，我们可以看到这样的一个示例：如何定义一个名称空间，然后填充一个包含私有和公有 API 的模块。除了一些语义差异，它与如何在纯JavaScript中实现Module模式十分相近。

```js
// 创建命名空间
Ext.namespace("myNameSpace");
// 创建应用
myNameSpace.app = function () {
  // 私有变量
  var btn1,
      privVar1 = 11;
  // 私有函数
  var btn1Handler = function ( button, event ) {
      console.log( "privVar1=" + privVar1 );
      console.log( "this.btn1Text=" + this.btn1Text );
    };
  return {
    // 公有属性
    btn1Text: "Button 1",
    // 公有该方法
    init: function () {
      if ( Ext.Ext2 ) {
        btn1 = new Ext.Button({
          renderTo: "btn1-ct",
          text: this.btn1Text,
          handler: btn1Handler
        });
      } else {
        btn1 = new Ext.Button( "btn1-ct", {
          text: this.btn1Text,
          handler: btn1Handler
        });
      }
    }
  };
}();
```

**YUI**

同样，在使用 YUI3 构建应用程序时，我们也可以实现Module模式。下面的示例在很大程度上基于由Eric Miraglia提出的原始YUI Module模式实现，但它又与纯JavaScript版本截然不同。

```js
Y.namespace( "store.basket" ) = (function () {
    var myPrivateVar, myPrivateMethod;
    // 私有变量
    myPrivateVar = "I can be accessed only within Y.store.basket.";
    // 私有方法
    myPrivateMethod = function () {
        Y.log( "I can be accessed only from within YAHOO.store.basket" );
    }
    return {
        myPublicProperty: "I'm a public property.",
        myPublicMethod: function () {
            Y.log( "I'm a public method." );
            // 在basket里，可以访问到私有变量和方法
            Y.log( myPrivateVar );
            Y.log( myPrivateMethod() );
            // myPublicMethod 的原始作用域是store，所以可以使用this来访问公有成员
            Y.log( this.myPublicProperty );
        }
    };

})();
```

**jQuery**

有许多方式可以将非jQuery插件代码包装在Module模式中。如果模块之间有多个共性，Ben Cherry之前建议过一种实现，在模块模式内部模块定义附件使用函数包装器。

在下面的示例中，定义了library函数，它声明一个新库，并在创建新库（即模块）时将init函数自动绑定到document.ready。

```js
function library( module ) {
  $( function() {
    if ( module.init ) {
      module.init();
    }
  });
  return module;
}

var myLibrary = library(function () {
  return {
    init: function () {
      // 模块实现
    }
  };
}());
```

### 9.2.5 优势

首先，相比真正封装的思想，它对于很多拥有面向对象背景的开发人员来说更加整洁，至少是从JavaScript的角度。

其次，它支持私有数据，因此，在Module模式中，代码的公有（public）部分能够接触私有部分，然而外界无法接触类的私有部分。

### 9.2.6 缺点

Module模式的缺点是：由于我们访问公有和私有成员的方式不同，当我们想改变可见性时，实际上我们必须要修改每一个曾经使用过该成员的地方。

我们也无法访问那些之后在方法里添加的私有成员。也就是说，在很多情况下，如果正确使用，Module模式仍然是相当有用的，肯定可以改进应用程序的结构。

其他缺点包括：无法为私有成员创建自动化单元测试，bug需要修正补丁时会增加额外的复杂性。为私有方法打补丁是不可能的。相反，我们必须覆盖所有与有bug的私有方法进行交互的公有方法。另外开发人员也无法轻易地扩展私有方法，所以要记住，私有方法并不像它们最初显现出来的那么灵活。

想要了解更深入的信息，可以阅读 Ben Cherry 这篇[精彩的文章](http://www.adequatelygood.com/JavaScript-Module-Pattern-In-Depth.html)。

## 9.3 揭示模块模式

揭示模块（Revealing Module）模式来自于，当Heilmann对这样一个现状的不满，即当我们想要在一个公有方法中调用另外一个公有方法，或者访问公有变量的时候，我们不得不重复主对象的名称。他也不喜欢模块模式中，当想要将某个成员变成公共成员时，修改文字标记的做法。

因此他工作的结果就是一个更新的模式，在这个模式中，我们可以简单地在私有域中定义我们所有的函数和变量，并且返回一个匿名对象，这个对象包含有一些指针，这些指针指向我们想要暴露出来的私有成员，使这些私有成员公有化。

下面给出一个如何使用暴露式模块模式的例子:

```js
var myRevealingModule = function () {

  var privateVar = "Ben Cherry",
      publicVar  = "Hey there!";

  function privateFunction() {
      console.log( "Name:" + privateVar );
  }

  function publicSetName( strName ) {
      privateVar = strName;
  }

  function publicGetName() {
      privateFunction();
  }

  // Reveal public pointers to 
  // private functions and properties

  return {
      setName: publicSetName,
      greeting: publicVar,
      getName: publicGetName
  };

}();
myRevealingModule.setName( "Paul Kinlan" );
```

这个模式可以用于将私有函数和属性以更加规范的命名方式展现出来。

```js
var myRevealingModule = function () {

  var privateCounter = 0;

  function privateFunction() {
      privateCounter++;
  }

  function publicFunction() {
      publicIncrement();
  }

  function publicIncrement() {
      privateFunction();
  }

  function publicGetCount(){
    return privateCounter;
  }

  // Reveal public pointers to
  // private functions and properties       

  return {
      start: publicFunction,
      increment: publicIncrement,
      count: publicGetCount
  };

}();

myRevealingModule.start();
```

### 9.3.1 优势

这个模式是我们脚本的语法更加一致。同样在模块的最后关于那些函数和变量可以被公共访问也变得更加清晰，增强了可读性。

### 9.3.2 缺点

这个模式的一个缺点是如果私有函数需要使用公有函数，那么这个公有函数在需要打补丁的时候就不能被重载。因为私有函数仍然使用的是私有的实现，并且这个模式不能用于公有成员，只用于函数。

公有成员使用私有成员也遵循上面不能打补丁的规则。

因为上面的原因，使用暴露式模块模式创建的模块相对于原始的模块模式更容易出问题，因此在使用的时候需要小心。

## 9.4 单例模式

单例（Singleton）模式之所以这么叫，是因为它限制一个类只能有一个实例化对象。经典的实现方式是，创建一个类，这个类包含一个方法，这个方法在没有对象存在的情况下，将会创建一个新的实例对象。如果对象存在，这个方法只是返回这个对象的引用。

单例和静态类不同，因为我们可以退出单例的初始化时间。通常这样做是因为，在初始化的时候需要一些额外的信息，而这些信息在声明的时候无法得知。对于并不知晓对单例模式引用的代码来讲，单例模式没有为它们提供一种方式可以简单的获取单例模式。这是因为，单例模式既不返回对象也不返回类，它只返回一种结构。可以类比闭包中的变量不是闭包-提供闭包的函数域是闭包（绕进去了）。

在JavaScript语言中, 单例服务作为一个从全局空间的代码实现中隔离出来共享的资源空间是为了提供一个单独的函数访问指针。

我们能像这样实现一个单例:

```js
var mySingleton = (function () {

  // Instance stores a reference to the Singleton
  var instance;

  function init() {

    // 单例

    // 私有方法和变量
    function privateMethod(){
        console.log( "I am private" );
    }

    var privateVariable = "Im also private";

    var privateRandomNumber = Math.random();

    return {

      // 共有方法和变量
      publicMethod: function () {
        console.log( "The public can see me!" );
      },

      publicProperty: "I am also public",

      getRandomNumber: function() {
        return privateRandomNumber;
      }

    };

  };

  return {

    // 如果存在获取此单例实例，如果不存在创建一个单例实例
    getInstance: function () {

      if ( !instance ) {
        instance = init();
      }

      return instance;
    }

  };

})();

var myBadSingleton = (function () {

  // 存储单例实例的引用
  var instance;

  function init() {

    // 单例

    var privateRandomNumber = Math.random();

    return {

      getRandomNumber: function() {
        return privateRandomNumber;
      }

    };

  };

  return {

    // 总是创建一个新的实例
    getInstance: function () {

      instance = init();

      return instance;
    }

  };

})();

// 使用:

var singleA = mySingleton.getInstance();
var singleB = mySingleton.getInstance();
console.log( singleA.getRandomNumber() === singleB.getRandomNumber() ); // true

var badSingleA = myBadSingleton.getInstance();
var badSingleB = myBadSingleton.getInstance();
console.log( badSingleA.getRandomNumber() !== badSingleB.getRandomNumber() ); // true
```

创建一个全局访问的单例实例 (通常通过 MySingleton.getInstance()) 因为我们不能(至少在静态语言中) 直接调用 new MySingleton() 创建实例. 这在JavaScript语言中是不可能的。

在四人帮(GoF)的书里面，单例模式的应用描述如下：

每个类只有一个实例，这个实例必须通过一个广为人知的接口，来被客户访问。
子类如果要扩展这个唯一的实例，客户可以不用修改代码就能使用这个扩展后的实例。
关于第二点，可以参考如下的实例，我们需要这样编码:

```js
mySingleton.getInstance = function(){
  if ( this._instance == null ) {
    if ( isFoo() ) {
       this._instance = new FooSingleton();
    } else {
       this._instance = new BasicSingleton();
    }
  }
  return this._instance;
};
```

在这里，getInstance 有点类似于工厂方法，我们不需要去更新每个访问单例的代码。FooSingleton可以是BasicSinglton的子类，并且实现了相同的接口。

为什么对于单例模式来讲，延迟执行执行这么重要？

在c++代码中，单例模式将不可预知的动态初始化顺序问题隔离掉，将控制权返回给程序员。

区分类的静态实例和单例模式很重要：尽管单例模式可以被实现成一个静态实例，但是单例可以懒构造，在真正用到之前，单例模式不需要分配资源或者内存。

如果我们有个静态对象可以被直接初始化，我们需要保证代码总是以同样的顺序执行（例如 汽车需要轮胎先初始化）当你有很多源文件的时候，这种方式没有可扩展性。

单例模式和静态对象都很有用，但是不能滥用-同样的我们也不能滥用其它模式。

在实践中，当一个对象需要和另外的对象进行跨系统协作的时候，单例模式很有用。下面是一个单例模式在这种情况下使用的例子：

```js
var SingletonTester = (function () {

  // options: an object containing configuration options for the singleton
  // e.g var options = { name: "test", pointX: 5}; 
  function Singleton( options )  {

    // set options to the options supplied
    // or an empty object if none are provided
    options = options || {};

    // set some properties for our singleton
    this.name = "SingletonTester";

    this.pointX = options.pointX || 6;

    this.pointY = options.pointY || 10; 

  }

  // our instance holder 
  var instance;

  // an emulation of static variables and methods
  var _static  = {  

    name:  "SingletonTester",

    // Method for getting an instance. It returns
    // a singleton instance of a singleton object
    getInstance:  function( options ) {   
      if( instance  ===  undefined )  {    
        instance = new Singleton( options );   
      }   

      return  instance; 

    } 
  }; 

  return  _static;

})();

var singletonTest  =  SingletonTester.getInstance({
  pointX:  5
});

// Log the output of pointX just to verify it is correct
// Outputs: 5
console.log( singletonTest.pointX );
```

尽管单例模式有着合理的使用需求，但是通常当我们发现自己需要在javascript使用它的时候，这是一种信号，表明我们可能需要去重新评估自己的设计。

这通常表明系统中的模块要么紧耦合要么逻辑过于分散在代码库的多个部分。单例模式更难测试，因为可能有多种多样的问题出现，例如隐藏的依赖关系，很难去创建多个实例，很难清理依赖关系，等等。

要想进一步了解关于单例的信息，可以读读 Miller Medeiros 推荐的这篇非常棒的关于单例模式以及单例模式各种各样问题的[文章](https://www.ibm.com/developerworks/webservices/library/co-single/index.html)，也可以看看这篇[文章](http://misko.hevery.com/2008/09/10/where-have-all-the-new-operators-gone/)的评论，这些评论讨论了单例模式是怎样增加了模块间的紧耦合。我很乐意去支持这些推荐，因为这两篇文章提出了很多关于单例模式重要的观点，而这些观点是很值得重视的。

## 9.5 观察者模式

观察者（Observer）模式是这样一种设计模式。一个被称作被观察者的对象，维护一组被称为观察者的对象，这些对象依赖于被观察者，被观察者自动将自身的状态的任何变化通知给它们。

当一个被观察者需要将一些变化通知给观察者的时候，它将采用广播的方式，这条广播可能包含特定于这条通知的一些数据。

当特定的观察者不再需要接受来自于它所注册的被观察者的通知的时候，被观察者可以将其从所维护的组中删除。 在这里提及一下设计模式现有的定义很有必要。这个定义是与所使用的语言无关的。通过这个定义，最终我们可以更深层次地了解到设计模式如何使用以及其优势。在四人帮的《设计模式:可重用的面向对象软件的元素》这本书中，是这样定义观察者模式的:

一个或者更多的观察者对一个被观察者的状态感兴趣，将自身的这种兴趣通过附着自身的方式注册在被观察者身上。当被观察者发生变化，而这种便可也是观察者所关心的，就会产生一个通知，这个通知将会被送出去，最后将会调用每个观察者的更新方法。当观察者不在对被观察者的状态感兴趣的时候，它们只需要简单的将自身剥离即可。

我们现在可以通过实现一个观察者模式来进一步扩展我们刚才所学到的东西。这个实现包含一下组件：

- 被观察者：维护一组观察者， 提供用于增加和移除观察者的方法。
- 观察者：提供一个更新接口，用于当被观察者状态变化时，得到通知。
- 具体的被观察者：状态变化时广播通知给观察者，保持具体的观察者的信息。
- 具体的观察者：保持一个指向具体被观察者的引用，实现一个更新接口，用于观察，以便保证自身状态总是和被观察者状态一致的。

首先，让我们对被观察者可能有的一组依赖其的观察者进行建模：
```js
function ObserverList(){
  this.observerList = [];
}

ObserverList.prototype.Add = function( obj ){
  return this.observerList.push( obj );
};

ObserverList.prototype.Empty = function(){
  this.observerList = [];
};

ObserverList.prototype.Count = function(){
  return this.observerList.length;
};

ObserverList.prototype.Get = function( index ){
  if( index > -1 && index < this.observerList.length ){
    return this.observerList[ index ];
  }
};

ObserverList.prototype.Insert = function( obj, index ){
  var pointer = -1;

  if( index === 0 ){
    this.observerList.unshift( obj );
    pointer = index;
  }else if( index === this.observerList.length ){
    this.observerList.push( obj );
    pointer = index;
  }

  return pointer;
};

ObserverList.prototype.IndexOf = function( obj, startIndex ){
  var i = startIndex, pointer = -1;

  while( i < this.observerList.length ){
    if( this.observerList[i] === obj ){
      pointer = i;
    }
    i++;
  }

  return pointer;
};

ObserverList.prototype.RemoveAt = function( index ){
  if( index === 0 ){
    this.observerList.shift();
  }else if( index === this.observerList.length -1 ){
    this.observerList.pop();
  }
};

// Extend an object with an extension
function extend( extension, obj ){
  for ( var key in extension ){
    obj[key] = extension[key];
  }
}
```
接着，我们对被观察者以及其增加，删除，通知在观察者列表中的观察者的能力进行建模：
```js
function Subject(){
  this.observers = new ObserverList();
}

Subject.prototype.AddObserver = function( observer ){
  this.observers.Add( observer );
}; 

Subject.prototype.RemoveObserver = function( observer ){
  this.observers.RemoveAt( this.observers.IndexOf( observer, 0 ) );
}; 

Subject.prototype.Notify = function( context ){
  var observerCount = this.observers.Count();
  for(var i=0; i < observerCount; i++){
    this.observers.Get(i).Update( context );
  }
};
```
我们接着定义建立新的观察者的一个框架。这里的update 函数之后会被具体的行为覆盖。
```js
// The Observer
function Observer(){
  this.Update = function(){
    // ...
  };
}
```
在我们的样例应用里面，我们使用上面的观察者组件，现在我们定义：

一个按钮，这个按钮用于增加新的充当观察者的选择框到页面上
一个控制用的选择框 , 充当一个被观察者，通知其它选择框是否应该被选中
一个容器，用于放置新的选择框
我们接着定义具体被观察者和具体观察者，用于给页面增加新的观察者，以及实现更新接口。通过查看下面的内联的注释，搞清楚在我们样例中的这些组件是如何工作的。

```HTML
<button id="addNewObserver">Add New Observer checkbox</button>
<input id="mainCheckbox" type="checkbox"/>
<div id="observersContainer"></div>
```
Sample script
```js
// 我们DOM 元素的引用

var controlCheckbox = document.getElementById( "mainCheckbox" ),
  addBtn = document.getElementById( "addNewObserver" ),
  container = document.getElementById( "observersContainer" );

// 具体的被观察者

//Subject 类扩展controlCheckbox 类
extend( new Subject(), controlCheckbox );

//点击checkbox 将会触发对观察者的通知
controlCheckbox["onclick"] = new Function( "controlCheckbox.Notify(controlCheckbox.checked)" );

addBtn["onclick"] = AddNewObserver;

// 具体的观察者

function AddNewObserver(){

  //建立一个新的用于增加的checkbox
  var check  = document.createElement( "input" );
  check.type = "checkbox";

  // 使用Observer 类扩展checkbox
  extend( new Observer(), check );

  // 使用定制的Update函数重载
  check.Update = function( value ){
    this.checked = value;
  };

  // 增加新的观察者到我们主要的被观察者的观察者列表中
  controlCheckbox.AddObserver( check );

  // 将元素添加到容器的最后
  container.appendChild( check );
}
```
在这个例子里面，我们看到了如何实现和配置观察者模式，了解了被观察者，观察者，具体被观察者，具体观察者的概念。

### 9.5.1 观察者模式和发布/订阅模式的不同
观察者模式确实很有用，但是在javascript时间里面，通常我们使用一种叫做发布/订阅模式的变体来实现观察者模式。这两种模式很相似，但是也有一些值得注意的不同。

观察者模式要求想要接受相关通知的观察者必须到发起这个事件的被观察者上注册这个事件。

发布/订阅模式使用一个主题/事件频道，这个频道处于想要获取通知的订阅者和发起事件的发布者之间。这个事件系统允许代码定义应用相关的事件，这个事件可以传递特殊的参数，参数中包含有订阅者所需要的值。这种想法是为了避免订阅者和发布者之间的依赖性。

这种和观察者模式之间的不同，使订阅者可以实现一个合适的事件处理函数，用于注册和接受由发布者广播的相关通知。

这里给出一个关于如何使用发布者/订阅者模式的例子，这个例子中完整地实现了功能强大的`publish()`,` subscribe()` 和 `unsubscribe()`。
```js
// 一个非常简单的邮件处理器

// 接受的消息的计数器
var mailCounter = 0;

// 初始化一个订阅者，这个订阅者监听名叫"inbox/newMessage" 的频道

// 渲染新消息的粗略信息
var subscriber1 = subscribe( "inbox/newMessage", function( topic, data ) {

  // 日志记录主题，用于调试
  console.log( "A new message was received: ", topic );

  // 使用来自于被观察者的数据，用于给用户展示一个消息的粗略信息
  $( ".messageSender" ).html( data.sender );
  $( ".messagePreview" ).html( data.body );

});

// 这是另外一个订阅者，使用相同的数据执行不同的任务

// 更细计数器，显示当前来自于发布者的新信息的数量
var subscriber2 = subscribe( "inbox/newMessage", function( topic, data ) {

  $('.newMessageCounter').html( mailCounter++ );

});

publish( "inbox/newMessage", [{
  sender:"hello@google.com",
  body: "Hey there! How are you doing today?"
}]);

// 在之后，我们可以让我们的订阅者通过下面的方式取消订阅来自于新主题的通知
// unsubscribe( subscriber1,  );
// unsubscribe( subscriber2 );
```
这个例子的更广的意义是对松耦合的原则的一种推崇。不是一个对象直接调用另外一个对象的方法，而是通过订阅另外一个对象的一个特定的任务或者活动，从而在这个任务或者活动出现的时候的得到通知。

### 9.5.2 优势
观察者和发布/订阅模式鼓励人们认真考虑应用不同部分之间的关系，同时帮助我们找出这样的层，该层中包含有直接的关系，这些关系可以通过一些列的观察者和被观察者来替换掉。这中方式可以有效地将一个应用程序切割成小块，这些小块耦合度低，从而改善代码的管理，以及用于潜在的代码复用。

使用观察者模式更深层次的动机是，当我们需要维护相关对象的一致性的时候，我们可以避免对象之间的紧密耦合。例如，一个对象可以通知另外一个对象，而不需要知道这个对象的信息。

两种模式下，观察者和被观察者之间都可以存在动态关系。这提供很好的灵活性，而当我们的应用中不同的部分之间紧密耦合的时候，是很难实现这种灵活性的。

尽管这些模式并不是万能的灵丹妙药，这些模式仍然是作为最好的设计松耦合系统的工具之一，因此在任何的JavaScript 开发者的工具箱里面，都应该有这样一个重要的工具。

### 9.5.3 缺点
事实上，这些模式的一些问题实际上正是来自于它们所带来的一些好处。在发布/订阅模式中，将发布者共订阅者上解耦，将会在一些情况下，导致很难确保我们应用中的特定部分按照我们预期的那样正常工作。

例如，发布者可以假设有一个或者多个订阅者正在监听它们。比如我们基于这样的假设，在某些应用处理过程中来记录或者输出错误日志。如果订阅者执行日志功能崩溃了（或者因为某些原因不能正常工作），因为系统本身的解耦本质，发布者没有办法感知到这些事情。

另外一个这种模式的缺点是，订阅者对彼此之间存在没有感知，对切换发布者的代价无从得知。因为订阅者和发布者之间的动态关系，更新依赖也很能去追踪。

### 9.5.4 发布/订阅实现
发布/订阅在JavaScript的生态系统中非常合适，主要是因为作为核心的ECMAScript 实现是事件驱动的。尤其是在浏览器环境下更是如此，因为DOM使用事件作为其主要的用于脚本的交互API。

也就是说，无论是ECMAScript 还是DOM都没有在实现代码中提供核心对象或者方法用于创建定制的事件系统（DOM3 的CustomEvent是一个例外，这个事件绑定在DOM上，因此通常用处不大）。

幸运的是，流行的JavaScript库例如dojo, jQuery(定制事件)以及YUI已经有相关的工具，可以帮助我们方便的实现一个发布/订阅者系统。下面我们看一些例子。

// 发布

// jQuery: $(obj).trigger("channel", [arg1, arg2, arg3]);
$( el ).trigger( "/login", [{username:"test", userData:"test"}] );

// Dojo: dojo.publish("channel", [arg1, arg2, arg3] );
dojo.publish( "/login", [{username:"test", userData:"test"}] );

// YUI: el.publish("channel", [arg1, arg2, arg3]);
el.publish( "/login", {username:"test", userData:"test"} );

// 订阅

// jQuery: $(obj).on( "channel", [data], fn );
$( el ).on( "/login", function( event ){...} );

// Dojo: dojo.subscribe( "channel", fn);
var handle = dojo.subscribe( "/login", function(data){..} );

// YUI: el.on("channel", handler);
el.on( "/login", function( data ){...} );

// 取消订阅

// jQuery: $(obj).off( "channel" );
$( el ).off( "/login" );

// Dojo: dojo.unsubscribe( handle );
dojo.unsubscribe( handle );

// YUI: el.detach("channel");
el.detach( "/login" );
对于想要在vanilla Javascript(或者其它库)中使用发布/订阅模式的人来讲， AmplifyJS 包含了一个干净的，库无关的实现，可以和任何库或者工具箱一起使用。Radio.js, PubSubJS 或者 Pure JS PubSub 来自于 Peter Higgins 都有类似的替代品值得研究。

尤其对于jQuery 开发者来讲，他们拥有很多其它的选择，可以选择大量的良好实现的代码，从Peter Higgins 的jQuery插件到Ben Alman 在GitHub 上的（优化的）发布/订阅 jQuery gist。下面给出了这些代码的链接。

Ben Alman的发布/订阅 gist(推荐)
Rick Waldron 在上面基础上修改的 jQuery-core 风格的实现
Peter Higgins 的插件
AppendTo 在AmplifyJS中的 发布/订阅实现
Ben Truyman的 gist
从上面我们可以看到在javascript中有这么多种观察者模式的实现，让我们看一下最小的一个版本的发布/订阅模式实现，这个实现我放在github 上，叫做pubsubz。这个实现展示了发布，订阅的核心概念，以及如何取消订阅。

我之所以选择这个代码作为我们例子的基础，是因为这个代码紧密贴合了方法签名和实现方式，这种实现方式正是我想看到的javascript版本的经典的观察者模式所应该有的样子。

发布/订阅实例
```js
var pubsub = {};

(function(q) {

    var topics = {},
        subUid = -1;

    // Publish or broadcast events of interest
    // with a specific topic name and arguments
    // such as the data to pass along
    q.publish = function( topic, args ) {

        if ( !topics[topic] ) {
            return false;
        }

        var subscribers = topics[topic],
            len = subscribers ? subscribers.length : 0;

        while (len--) {
            subscribers[len].func( topic, args );
        }

        return this;
    };

    // Subscribe to events of interest
    // with a specific topic name and a
    // callback function, to be executed
    // when the topic/event is observed
    q.subscribe = function( topic, func ) {

        if (!topics[topic]) {
            topics[topic] = [];
        }

        var token = ( ++subUid ).toString();
        topics[topic].push({
            token: token,
            func: func
        });
        return token;
    };

    // Unsubscribe from a specific
    // topic, based on a tokenized reference
    // to the subscription
    q.unsubscribe = function( token ) {
        for ( var m in topics ) {
            if ( topics[m] ) {
                for ( var i = 0, j = topics[m].length; i < j; i++ ) {
                    if ( topics[m][i].token === token) {
                        topics[m].splice( i, 1 );
                        return token;
                    }
                }
            }
        }
        return this;
    };
}( pubsub ));
```
示例:使用我们的实现
我们现在可以使用发布实例和订阅感兴趣的事件，例如:
```js
// Another simple message handler

// A simple message logger that logs any topics and data received through our
// subscriber
var messageLogger = function ( topics, data ) {
    console.log( "Logging: " + topics + ": " + data );
};

// Subscribers listen for topics they have subscribed to and
// invoke a callback function (e.g messageLogger) once a new
// notification is broadcast on that topic
var subscription = pubsub.subscribe( "inbox/newMessage", messageLogger );

// Publishers are in charge of publishing topics or notifications of
// interest to the application. e.g:

pubsub.publish( "inbox/newMessage", "hello world!" );

// or
pubsub.publish( "inbox/newMessage", ["test", "a", "b", "c"] );

// or
pubsub.publish( "inbox/newMessage", {
  sender: "hello@google.com",
  body: "Hey again!"
});

// We cab also unsubscribe if we no longer wish for our subscribers
// to be notified
// pubsub.unsubscribe( subscription );

// Once unsubscribed, this for example won't result in our
// messageLogger being executed as the subscriber is
// no longer listening
pubsub.publish( "inbox/newMessage", "Hello! are you still there?" );
```
例如：用户界面通知
接下来，让我们想象一下，我们有一个Web应用程序，负责显示实时股票信息。

应用程序可能有一个表格显示股票统计数据和一个计数器显示的最后更新点。当数据模型发生变化时，应用程序将需要更新表格和计数器。在这种情况下，我们的主题（这将发布主题/通知）是数据模型以及我们的订阅者是表格和计数器。

当我们的订阅者收到通知：该模型本身已经改变，他们自己可以进行相应的更新。

在我们的实现中，如果发现新的股票信息是可用的，我们的订阅者将收听到的主题“新数据可用”。如果一个新的通知发布到该主题，那将触发表格去添加一个包含此信息的新行。它也将更新最后更新计数器，记录最后一次添加的数据
```js
// Return the current local time to be used in our UI later
getCurrentTime = function (){

   var date = new Date(),
         m = date.getMonth() + 1,
         d = date.getDate(),
         y = date.getFullYear(),
         t = date.toLocaleTimeString().toLowerCase();

        return (m + "/" + d + "/" + y + " " + t);
};

// Add a new row of data to our fictional grid component
function addGridRow( data ) {

   // ui.grid.addRow( data );
   console.log( "updated grid component with:" + data );

}

// Update our fictional grid to show the time it was last
// updated
function updateCounter( data ) {

   // ui.grid.updateLastChanged( getCurrentTime() );  
   console.log( "data last updated at: " + getCurrentTime() + " with " + data);

}

// Update the grid using the data passed to our subscribers
gridUpdate = function( topic, data ){

  if ( data !== "undefined" ) {
     addGridRow( data );
     updateCounter( data );
   }

};

// Create a subscription to the newDataAvailable topic
var subscriber = pubsub.subscribe( "newDataAvailable", gridUpdate );

// The following represents updates to our data layer. This could be
// powered by ajax requests which broadcast that new data is available
// to the rest of the application.

// Publish changes to the gridUpdated topic representing new entries
pubsub.publish( "newDataAvailable", {
  summary: "Apple made $5 billion",
  identifier: "APPL",
  stockPrice: 570.91
});

pubsub.publish( "newDataAvailable", {
  summary: "Microsoft made $20 million",
  identifier: "MSFT",
  stockPrice: 30.85
});
```
样例：在下面这个电影评分的例子里面，我们使用Ben Alman的发布/订阅实现来解耦应用程序。我们使用Ben Alman的jQuery实现，来展示如何解耦用户界面。请注意，我们如何做到提交一个评分，来产生一个发布信息，这个信息表明了当前新的用户和评分数据可用。

剩余的工作留给订阅者，由订阅者来代理这些主题中的数据发生的变化。在我们的例子中，我们将新的数据压入到现存的数组中，接着使用Underscore库的template()方法来渲染模板。

HTML/模板
```html
<script id="userTemplate" type="text/html">
   <li><%= name %></li>
</script>

<script id="ratingsTemplate" type="text/html">
   <li><strong><%= title %></strong> was rated <%= rating %>/5</li>
</script>

<div id="container">

   <div class="sampleForm">
       <p>
           <label for="twitter_handle">Twitter handle:</label>
           <input type="text" id="twitter_handle" />
       </p>
       <p>
           <label for="movie_seen">Name a movie you've seen this year:</label>
           <input type="text" id="movie_seen" />
       </p>
       <p>

           <label for="movie_rating">Rate the movie you saw:</label>
           <select id="movie_rating">
                 <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                  <option value="5" selected>5</option>

          </select>
        </p>
        <p>

            <button id="add">Submit rating</button>
        </p>
    </div>

    <div class="summaryTable">
        <div id="users"><h3>Recent users</h3></div>
        <div id="ratings"><h3>Recent movies rated</h3></div>
    </div>

 </div>
 ```
JavaScript
```js
;(function( $ ) {

  // Pre-compile templates and "cache" them using closure
  var
    userTemplate = _.template($( "#userTemplate" ).html()),
    ratingsTemplate = _.template($( "#ratingsTemplate" ).html());

  // Subscribe to the new user topic, which adds a user
  // to a list of users who have submitted reviews
  $.subscribe( "/new/user", function( e, data ){

    if( data ){

      $('#users').append( userTemplate( data ));

    }

  });

  // Subscribe to the new rating topic. This is composed of a title and
  // rating. New ratings are appended to a running list of added user
  // ratings.
  $.subscribe( "/new/rating", function( e, data ){

    var compiledTemplate;

    if( data ){

      $( "#ratings" ).append( ratingsTemplate( data );

    }

  });

  // Handler for adding a new user
  $("#add").on("click", function( e ) {

    e.preventDefault();

    var strUser = $("#twitter_handle").val(),
       strMovie = $("#movie_seen").val(),
       strRating = $("#movie_rating").val();

    // Inform the application a new user is available
    $.publish( "/new/user",  { name: strUser } );

    // Inform the app a new rating is available
    $.publish( "/new/rating",  { title: strMovie, rating: strRating} );

    });

})( jQuery );
```
样例：解耦一个基于Ajax的jQuery应用。

在我们最后的例子中，我们将从实用的角度来看一下如何在开发早起使用发布/订阅模式来解耦代码，这样可以帮助我们避免之后痛苦的重构过程。

在Ajax重度依赖的应用里面，我们常会见到这种情况，当我们收到一个请求的响应之后，我们希望能够完成不仅仅一个特定的操作。我们可以简单的将所有请求后的逻辑加入到成功的回调函数里面，但是这样做有一些问题。

高度耦合的应用优势会增加重用功能的代价，因为高度耦合增加了内部函数/代码的依赖性。这意味着如果我们只是希望获取一次性获取结果集，可以将请求后 的逻辑代码 硬编码在回调函数里面，这种方式可以正常工作，但是当我们想要对相同的数据源(不同的最终行为)做更多的Ajax调用的时候，这种方式就不适合了，我们必须要多次重写部分代码。与其回溯调用相同数据源的每一层，然后在将它们泛化，不如一开始就使用发布/订阅模式来节约时间。

使用观察者，我们可以简单的将整个应用范围的通知进行隔离，针对不同的事件，我们可以把这种隔离做到我们想要的粒度上，如果使用其它模式，则可能不会有这么优雅的实现。

注意我们下面的例子中，当用户表明他们想要做一次搜索查询的时候，一个话题通知就会生成，而当请求返回，并且实际的数据可用的时候，又会生成另外一个通知。而如何使用这些事件（或者返回的数据），都是由订阅者自己决定的。这样做的好处是，如果我们想要，我们可以有10个不同的订阅者，以不同的方式使用返回的数据，而对于Ajax层来讲，它不会关心你如何处理数据。它唯一的责任就是请求和返回数据，接着将数据发送给所有想要使用数据的地方。这种相关性上的隔离可以是我们整个代码设计更为清晰。

HTML/Templates
```html
<form id="flickrSearch">

   <input type="text" name="tag" id="query"/>

   <input type="submit" name="submit" value="submit"/>

</form>

<div id="lastQuery"></div>

<div id="searchResults"></div>

<script id="resultTemplate" type="text/html">
    <% _.each(items, function( item ){  %>
            <li><p><img src="<%= item.media.m %>"/></p></li>
    <% });%>
</script>
```
JavaScript
```js
;(function( $ ) {

   // Pre-compile template and "cache" it using closure
   var resultTemplate = _.template($( "#resultTemplate" ).html());

   // Subscribe to the new search tags topic
   $.subscribe( "/search/tags" , function( tags ) {
       $( "#searchResults" )
                .html("
<p>
    Searched for:<strong>" + tags + "</strong>
</p>
");
   });

   // Subscribe to the new results topic
   $.subscribe( "/search/resultSet" , function( results ){

       $( "#searchResults" ).append(resultTemplate( results ));

   });

   // Submit a search query and publish tags on the /search/tags topic
   $( "#flickrSearch" ).submit( function( e ) {

       e.preventDefault();
       var tags = $(this).find( "#query").val();

       if ( !tags ){
        return;
       }

       $.publish( "/search/tags" , [ $.trim(tags) ]);

   });

   // Subscribe to new tags being published and perform
   // a search query using them. Once data has returned
   // publish this data for the rest of the application
   // to consume

   $.subscribe("/search/tags", function( tags ) {

       $.getJSON( "http://api.flickr.com/services/feeds/photos_public.gne?jsoncallback=?" ,{
              tags: tags,
              tagmode: "any",
              format: "json"
            },

          function( data ){

              if( !data.items.length ) {
                return;
              }

              $.publish( "/search/resultSet" , data.items  );
       });

   });

})();
```

观察者模式在应用设计中，解耦一系列不同的场景上非常有用，如果你没有用过它，我推荐你尝试一下今天提到的之前写到的某个实现。这个模式是一个易于学习的模式，同时也是一个威力巨大的模式。

## 9.6 Mediator（中介者）模式

### 中介者模式
字典中中介者的定义是，一个中立方，在谈判和冲突解决过程中起辅助作用。在我们的世界，一个中介者是一个行为设计模式，使我们可以导出统一的接口，这样系统不同部分就可以彼此通信。

如果系统组件之间存在大量的直接关系，就可能是时候，使用一个中心的控制点，来让不同的组件通过它来通信。中介者通过将组件之间显式的直接的引用替换成通过中心点来交互的方式，来做到松耦合。这样可以帮助我们解耦，和改善组件的重用性。

在现实世界中，类似的系统就是，飞行控制系统。一个航站塔（中介者）处理哪个飞机可以起飞，哪个可以着陆，因为所有的通信（监听的通知或者广播的通知）都是飞机和控制塔之间进行的，而不是飞机和飞机之间进行的。一个中央集权的控制中心是这个系统成功的关键，也正是中介者在软件设计领域中所扮演的角色。

从实现角度来讲，中介者模式是观察者模式中的共享被观察者对象。在这个系统中的对象之间直接的发布/订阅关系被牺牲掉了，取而代之的是维护一个通信的中心节点。

也可以认为是一种补充-用于应用级别的通知，例如不同子系统之间的通信，子系统本身很复杂，可能需要使用发布/订阅模式来做内部组件之间的解耦。

另外一个类似的例子是DOM的事件冒泡机制，以及事件代理机制。如果系统中所有的订阅者都是对文档订阅，而不是对独立的节点订阅，那么文档就充当一个中介者的角色。DOM的这种做法，不是将事件绑定到独立节点上，而是用一个更高级别的对象负责通知订阅者关于交互事件的信息。

### 基础的实现
中间人模式的一种简单的实现可以在下面找到,`publish()`和`subscribe()`方法都被暴露出来使用:
```js
var mediator = (function(){

    // Storage for topics that can be broadcast or listened to
    var topics = {};

    // Subscribe to a topic, supply a callback to be executed
    // when that topic is broadcast to
    var subscribe = function( topic, fn ){

        if ( !topics[topic] ){
          topics[topic] = [];
        }

        topics[topic].push( { context: this, callback: fn } );

        return this;
    };

    // Publish/broadcast an event to the rest of the application
    var publish = function( topic ){

        var args;

        if ( !topics[topic] ){
          return false;
        }

        args = Array.prototype.slice.call( arguments, 1 );
        for ( var i = 0, l = topics[topic].length; i < l; i++ ) {

            var subscription = topics[topic][i];
            subscription.callback.apply( subscription.context, args );
        }
        return this;
    };

    return {
        publish: publish,
        subscribe: subscribe,
        installTo: function( obj ){
            obj.subscribe = subscribe;
            obj.publish = publish;
        }
    };

}());
```
### 高级的实现
对于那些对更加高级实现感兴趣的人,以走读的方式看一看以下我对Jack Lawson优秀的Mediator.js重写的一个缩略版本.在其它方面的改进当中,为我们的中间人支持主题命名空间,用户拆卸和一个更加稳定的发布/订阅系统。但是如果你想跳过这个走读，你可以直接进入到下一个例子继续阅读。

得感谢Jack优秀的代码注释对这部分内容的协助。

首先，让我们实现认购的概念，我们可以考虑一个中间人主题的注册。

通过生成对象实体,我们稍后能够简单的更新认购,而不需要去取消注册然后重新注册它们.认购可以写成一个使用被称作一个选项对象或者一个上下文环境的函数
```js
// Pass in a context to attach our Mediator to.
// By default this will be the window object
(function( root ){

  function guidGenerator() { /*..*/}

  // Our Subscriber constructor
  function Subscriber( fn, options, context ){

    if ( !(this instanceof Subscriber) ) {

      return new Subscriber( fn, context, options );

    }else{

      // guidGenerator() is a function that generates
      // GUIDs for instances of our Mediators Subscribers so
      // we can easily reference them later on. We're going
      // to skip its implementation for brevity

      this.id = guidGenerator();
      this.fn = fn;
      this.options = options;
      this.context = context;
      this.topic = null;

    }
  }
})();
```
在我们的中间人主题中包涵了一长串的回调和子主题,当中间人发布在我们中间人实体上被调用的时候被启动.它也包含操作数据列表的方法
```js
// Let's model the Topic.
// JavaScript lets us use a Function object as a
// conjunction of a prototype for use with the new
// object and a constructor function to be invoked.
function Topic( namespace ){

  if ( !(this instanceof Topic) ) {
    return new Topic( namespace );
  }else{

    this.namespace = namespace || "";
    this._callbacks = [];
    this._topics = [];
    this.stopped = false;

  }
}

// Define the prototype for our topic, including ways to
// add new subscribers or retrieve existing ones.
Topic.prototype = {

  // Add a new subscriber
  AddSubscriber: function( fn, options, context ){

    var callback = new Subscriber( fn, options, context );

    this._callbacks.push( callback );

    callback.topic = this;

    return callback;
  },
...
```
我们的主题实体被当做中间人调用的一个参数被传递.使用一个方便实用的calledStopPropagation()方法,回调就可以进一步被传播开来:
```js
StopPropagation: function(){
  this.stopped = true;
},
```
我们也能够使得当提供一个GUID的标识符的时候检索订购用户更加容易:
```js
GetSubscriber: function( identifier ){

  for(var x = 0, y = this._callbacks.length; x < y; x++ ){
    if( this._callbacks[x].id == identifier || this._callbacks[x].fn == identifier ){
      return this._callbacks[x];
    }
  }

  for( var z in this._topics ){
    if( this._topics.hasOwnProperty( z ) ){
      var sub = this._topics[z].GetSubscriber( identifier );
      if( sub !== undefined ){
        return sub;
      }
    }
  }

},
```
接着,在我们需要它们的情况下,我们也能够提供添加新主题,检查现有的主题或者检索主题的简单方法:
```js
AddTopic: function( topic ){
  this._topics[topic] = new Topic( (this.namespace ? this.namespace + ":" : "") + topic );
},

HasTopic: function( topic ){
  return this._topics.hasOwnProperty( topic );
},

ReturnTopic: function( topic ){
  return this._topics[topic];
},
```
如果我们觉得不再需要它们了,我们也可以明确的删除这些订购用户.下面就是通过它的其子主题递归删除订购用户的代码:
```js
RemoveSubscriber: function( identifier ){

  if( !identifier ){
    this._callbacks = [];

    for( var z in this._topics ){
      if( this._topics.hasOwnProperty(z) ){
        this._topics[z].RemoveSubscriber( identifier );
      }
    }
  }

  for( var y = 0, x = this._callbacks.length; y < x; y++ ) {
    if( this._callbacks[y].fn == identifier || this._callbacks[y].id == identifier ){
      this._callbacks[y].topic = null;
      this._callbacks.splice( y,1 );
      x--; y--;
    }
  }

},
```
接着我们通过递归子主题将发布任意参数的能够包含到订购服务对象中:
```js
Publish: function( data ){

    for( var y = 0, x = this._callbacks.length; y < x; y++ ) {

        var callback = this._callbacks[y], l;
          callback.fn.apply( callback.context, data );

      l = this._callbacks.length;

      if( l < x ){
        y--;
        x = l;
      }
    }

    for( var x in this._topics ){
      if( !this.stopped ){
        if( this._topics.hasOwnProperty( x ) ){
          this._topics[x].Publish( data );
        }
      }
    }

    this.stopped = false;
  }
};
```
接着我们暴露我们将主要交互的调节实体.这里它是通过注册的并且从主题中删除的事件来实现的
```js
function Mediator() {

  if ( !(this instanceof Mediator) ) {
    return new Mediator();
  }else{
    this._topics = new Topic( "" );
  }

};
```
想要更多先进的用例,我们可以看看调解支持的主题命名空间,下面这样的asinbox:messages:new:read.GetTopic 返回基于一个命名空间的主题实体。
```js
Mediator.prototype = {

  GetTopic: function( namespace ){
    var topic = this._topics,
        namespaceHierarchy = namespace.split( ":" );

    if( namespace === "" ){
      return topic;
    }

    if( namespaceHierarchy.length > 0 ){
      for( var i = 0, j = namespaceHierarchy.length; i < j; i++ ){

        if( !topic.HasTopic( namespaceHierarchy[i]) ){
          topic.AddTopic( namespaceHierarchy[i] );
        }

        topic = topic.ReturnTopic( namespaceHierarchy[i] );
      }
    }

    return topic;
  },
  ```
这一节我们定义了一个Mediator.Subscribe方法，它接受一个主题命名空间,一个将要被执行的函数,选项和又一个在订阅中调用函数的上下文环境.这样就创建了一个主题,如果这样的一个主题存在的话
```js
Subscribe: function( topiclName, fn, options, context ){
  var options = options || {},
      context = context || {},
      topic = this.GetTopic( topicName ),
      sub = topic.AddSubscriber( fn, options, context );

  return sub;
},
```
根据这一点,我们可以进一步定义能够访问特定订阅用户,或者将他们从主题中递归删除的工具
```js
// Returns a subscriber for a given subscriber id / named function and topic namespace

GetSubscriber: function( identifier, topic ){
  return this.GetTopic( topic || "" ).GetSubscriber( identifier );
},

// Remove a subscriber from a given topic namespace recursively based on
// a provided subscriber id or named function.

Remove: function( topicName, identifier ){
  this.GetTopic( topicName ).RemoveSubscriber( identifier );
},
```
我们主要的发布方式可以让我们随意发布数据到选定的主题命名空间，这可以在下面的代码中看到。

主题可以被向下递归.例如,一条对inbox:message的post将发送到inbox:message:new和inbox:message:new:read.它将像接下来这样被使用:Mediator.Publish( "inbox:messages:new", [args] );
```js
Publish: function( topicName ){
    var args = Array.prototype.slice.call( arguments, 1),
        topic = this.GetTopic( topicName );

    args.push( topic );

    this.GetTopic( topicName ).Publish( args );
  }
};
最后，我们可以很容易的暴露我们的中间人，将它附着在传递到根中的对象上：

 root.Mediator = Mediator;
  Mediator.Topic = Topic;
  Mediator.Subscriber = Subscriber;

// Remember we can pass anything in here. I've passed inwindowto
// attach the Mediator to, but we can just as easily attach it to another
// object if desired.
})( window );
```
示例
无论是使用来自上面的实现（简单的选项和更加先进的选项都是），我们能够像下面这样将一个简单的聊天记录系统整到一起:

HTML
```html
<h1>Chat</h1>
<form id="chatForm">
    <label for="fromBox">Your Name:</label>
    <input id="fromBox" type="text"/>
    <br />
    <label for="toBox">Send to:</label>
    <input id="toBox" type="text"/>
    <br />
    <label for="chatBox">Message:</label>
    <input id="chatBox" type="text"/>
    <button type="submit">Chat</button>
</form>

<div id="chatResult"></div>
```

Javascript
```js
$( "#chatForm" ).on( "submit", function(e) {
    e.preventDefault();

    // Collect the details of the chat from our UI
    var text = $( "#chatBox" ).val(),
        from = $( "#fromBox" ).val(),
        to = $( "#toBox" ).val();

    // Publish data from the chat to the newMessage topic
    mediator.publish( "newMessage" , { message: text, from: from, to: to } );
});

// Append new messages as they come through
function displayChat( data ) {
    var date = new Date(),
        msg = data.from + " said \"" + data.message + "\" to " + data.to;

    $( "#chatResult" )
        .prepend("
<p>
    " + msg + " (" + date.toLocaleTimeString() + ")
</p>
");
}

// Log messages
function logChat( data ) {
    if ( window.console ) {
        console.log( data );
    }
}

// Subscribe to new chat messages being submitted
// via the mediator
mediator.subscribe( "newMessage", displayChat );
mediator.subscribe( "newMessage", logChat );

// The following will however only work with the more advanced implementation:

function amITalkingToMyself( data ) {
    return data.from === data.to;
}

function iAmClearlyCrazy( data ) {
    $( "#chatResult" ).prepend("
<p>
    " + data.from + " is talking to himself.
</p>
");
}

 mediator.Subscribe( amITalkingToMyself, iAmClearlyCrazy );
 ```
### 优点&缺点
中间人模式最大的好处就是，它节约了对象或者组件之间的通信信道，这些对象或者组件存在于从多对多到多对一的系统之中。由于解耦合水平的因素，添加新的发布或者订阅者是相对容易的。

也许使用这个模式最大的缺点是它可以引入一个单点故障。在模块之间放置一个中间人也可能会造成性能损失，因为它们经常是间接地的进行通信的。由于松耦合的特性，仅仅盯着广播很难去确认系统是如何做出反应的。

这就是说，提醒我们自己解耦合的系统拥有许多其它的好处，是很有用的——如果我们的模块互相之间直接的进行通信，对于模块的改变（例如：另一个模块抛出了异常）可以很容易的对我们系统的其它部分产生多米诺连锁效应。这个问题在解耦合的系统中很少需要被考虑到。

在一天结束的时候，紧耦合会导致各种头痛，这仅仅只是另外一种可选的解决方案，但是如果得到正确实现的话也能够工作得很好。

### 中间人VS观察者
开发人员往往不知道中间人模式和观察者模式之间的区别。不可否认，这两种模式之间有一点点重叠，但让我们回过头来重新寻求GoF的一种解释：

“在观察者模式中，没有封装约束的单一对象”。取而代之，观察者和主题必须合作来维护约束。通信的模式决定于观察者和主题相互关联的方式：一个单独的主题经常有许多的观察者，而有时候一个主题的观察者是另外一个观察者的主题。“

中间人和观察者都提倡松耦合，然而，中间人默认使用让对象严格通过中间人进行通信的方式实现松耦合。观察者模式则创建了观察者对象，这些观察者对象会发布触发对象认购的感兴趣的事件。

### 中间人VS外观
不久我们的描述就将涵盖外观模式，但作为参考之用，一些开发者也想知道中间人和外观模式之间有哪些相似之处。它们都对模块的功能进行抽象，但有一些细微的差别。

中间人模式让模块之间集中进行通信，它会被这些模块明确的引用。外观模式却只是为模块或者系统定义一个更加简单的接口，但不添加任何额外的功能。系统中其他的模块并不直接意识到外观的概念，而可以被认为是单向的。

## 9.7 Prototype（原型）模式

### 原型模式
GoF将原型模式引用为通过克隆的方式基于一个现有对象的模板创建对象的模式。

我们能够将原型模式认作是基于原型的继承中,我们创建作为其它对象原型的对象.原型对象自身被当做构造器创建的每一个对象的蓝本高效的使用着.如果构造器函数使用的原型包含例如叫做name的属性,那么每一个通过同一个构造器创建的对象都将拥有这个相同的属性。

在现存的(非Javascript的)语法中重新看一看对这个模式的定义,我们也许可以再一次发现对类的引用.真实的情况是那种原型继承避免了完全使用类.理论上既不是一个"定义的“对象，也不是一个核心对象。我们可以简单的创建现存函数型对象的拷贝。

使用原型模式的好处之一就是,我们在JavaScript提供的原生能力之上工作的,而不是JavaScript试图模仿的其它语言的特性.而对于其它的模式来说,情况并非如此。

这一模式不仅仅是实现继承的一种简单方式,它顺便还能够带来一点性能上的提升:当定义对象的一个方法时,它们都是使用引用创建的(因此所有的子对象都指向同一个函数),而不是创建属于它们的单独的拷贝。

对于那些有趣的,真正原型的集成,像ECMAScript 5标准中所定义的那样,需要使用 `Object.create`(如我们在本节的前面部分所见到的).为了提醒我们自己,`Object.create`创建了一个拥有特定原型的对象,并且也包含选项式的特定属性.(例如,`Object.create(prototype,optionalDescriptorObject)`)。

我们可以在下面的示例中看到对这个的展示:
```js
var myCar = {

  name: "Ford Escort",

  drive: function () {
    console.log( "Weeee. I'm driving!" );
  },

  panic: function () {
    console.log( "Wait. How do you stop this thing?" );
  }

};

// Use Object.create to instantiate a new car
var yourCar = Object.create( myCar );

// Now we can see that one is a prototype of the other
console.log( yourCar.name );
Object.create也允许我们简单的继承先进的概念,比如对象能够直接继承自其它对象,这种不同的继承.我们早先也看到Object.create允许我们使用 供应的第二个参数来初始化对象属性。例如：

var vehicle = {
  getModel: function () {
    console.log( "The model of this vehicle is.." + this.model );
  }
};

var car = Object.create(vehicle, {

  "id": {
    value: MY_GLOBAL.nextId(),
    // writable:false, configurable:false by default
    enumerable: true
  },

  "model": {
    value: "Ford",
    enumerable: true
  }

});
```
这里的属性可以被Object.create的第二个参数来初始化,使用一种类似于我们前面看到的Object.defineProperties和Object.defineProperties方法所使用语法的对象字面值。

在枚举对象的属性,和(如Crockford所提醒的那样)在一个hasOwnProperty()检查中封装循环的内容时,原型关系会造成麻烦,这一事实是值得我们关注的。

如果我们希望在不直接使用Object.create的前提下实现原型模式,我们可以像下面这样,按照上面的示例,模拟这一模式:
```js
var vehiclePrototype = {

  init: function ( carModel ) {
    this.model = carModel;
  },

  getModel: function () {
    console.log( "The model of this vehicle is.." + this.model);
  }
};

function vehicle( model ) {

  function F() {};
  F.prototype = vehiclePrototype;

  var f = new F();

  f.init( model );
  return f;

}

var car = vehicle( "Ford Escort" );
car.getModel();
```
注意:这种可选的方式不允许用户使用相同的方式定义只读的属性(因为如果不小心的话vehicle原型可能会被改变)。

原型模式的最后一种可选实现可以像下面这样:
```js
var beget = (function () {

    function F() {}

    return function ( proto ) {
        F.prototype = proto;
        return new F();
    };
})();
```
一个人可以从vehicle函数引用这个方法,注意,这里的那个vehicle正是在模拟着构造器,因为原型模式在将一个对象链接到一个原型之外没有任何初始化的概念。

## 9.8 Command（命令）模式

### 命令模式
命名模式的目标是将方法的调用,请求或者操作封装到一个单独的对象中,给我们酌情执行同时参数化和传递方法调用的能力.另外,它使得我们能将对象从实现了行为的对象对这些行为的调用进行解耦,为我们带来了换出具体的对象这一更深程度的整体灵活性。

具体类是对基于类的编程语言的最好解释,并且同抽象类的理念联系紧密.抽象类定义了一个接口,但并不需要提供对它的所有成员函数的实现.它扮演着驱动其它类的基类角色.被驱动类实现了缺失的函数而被称为具体类. 命令模式背后的一般理念是为我们提供了从任何执行中的命令中分离出发出命令的责任,取而代之将这一责任委托给其它的对象。

实现明智简单的命令对象,将一个行为和对象对调用这个行为的需求都绑定到了一起.它们始终都包含一个执行操作(比如run()或者execute()).所有带有相同接口的命令对象能够被简单地根据需要调换,这被认为是命令模式的更大的好处之一。

为了展示命令模式,我们创建一个简单的汽车购买服务:
```js
(function(){

  var CarManager = {

      // request information
      requestInfo: function( model, id ){
        return "The information for " + model + " with ID " + id + " is foobar";
      },

      // purchase the car
      buyVehicle: function( model, id ){
        return "You have successfully purchased Item " + id + ", a " + model;
      },

      // arrange a viewing
      arrangeViewing: function( model, id ){
        return "You have successfully booked a viewing of " + model + " ( " + id + " ) ";
      }

    };

})();
```
看一看上面的这段代码,它也许是通过直接访问对象来琐碎的调用我们CarManager的方法。在技术上我们也许都会都会对这个没有任何失误达成谅解.它是完全有效的Javascript然而也会有情况不利的情况。

例如,想象如果CarManager的核心API会发生改变的这种情况.这可能需要所有直接访问这些方法的对象也跟着被修改.这可以被看成是一种耦合,明显违背了OOP方法学尽量实现松耦合的理念.取而代之,我们可以通过更深入的抽象这些API来解决这个问题。

现在让我们来扩展我们的CarManager,以便我们这个命令模式的应用程序得到接下来的这种效果:接受任何可以在CarManager对象上面执行的方法,传送任何可以被使用到的数据,如Car模型和ID。

这里是我们希望能够实现的样子:
```js
CarManager.execute( "buyVehicle", "Ford Escort", "453543" );
```
按照这种结构,我们现在应该像下面这样,添加一个对于"CarManager.execute()"方法的定义：
```js
CarManager.execute = function ( name ) {
    return CarManager[name] && CarManager[name].apply( CarManager, [].slice.call(arguments, 1) );
};
```
最终我们的调用如下所示:
```js
CarManager.execute( "arrangeViewing", "Ferrari", "14523" );
CarManager.execute( "requestInfo", "Ford Mondeo", "54323" );
CarManager.execute( "requestInfo", "Ford Escort", "34232" );
CarManager.execute( "buyVehicle", "Ford Escort", "34232" );
```
## 9.9 Facade（外观）模式

外观模式
当我们提出一个门面，我们要向这个世界展现的是一个外观，这一外观可能藏匿着一种非常与众不同的真实。这就是我们即将要回顾的模式背后的灵感——门面模式。这一模式提供了面向一种更大型的代码体提供了一个的更高级别的舒适的接口，隐藏了其真正的潜在复杂性。把这一模式想象成要是呈现给开发者简化的API，一些总是会提升使用性能的东西。

门面是一种经常可以在Javascript库中看到的结构性模式，像在jQuery中，尽管一种实现可能支持带有广泛行为的方法，但仅仅只有这些方法的“门面”或者说被限制住的抽象才会公开展现出来供人们所使用。

这允许我们直接同门面，而不是同幕后的子系统交互。不论何时我们使用jQuery的$(el).css或者$(el).animate()方法，我们实际上都是在使用一个门面——更加简单的公共接口让我们避免为了使得行为工作起来而不得不去手动调用jQuery核心的内置方法。这也避免了手动同DOM API交互和维护状态变量的需要。

应该考虑对jQuery的核心方法做一层中间抽象。对于开发者来说更直接的负担是DOM API，而门面使得jQuery使用起来如此的容易。

为了在我们所学的基础上进行构建，门面模式同时需要简化一个类的接口，和把类同使用它的代码解耦。这给予了我们使用一种方式直接同子系统交互的能力，这一方式有时候会比直接访问子系统更加不容易出错。门面的优势包括易用，还有常常实现起这个模式来只是一小段路，不费力。

让我们通过实践来看看这个模式。这是一个没有经过优化的代码示例，但是这里我们使用了一个门面来简化跨浏览器事件监听的接口。我们创建了一个公共的方法来实现，此方法 能够被用在检查特性的存在的代码中，以便这段代码能够提供一种安全和跨浏览器兼容方案。
```js
var addMyEvent = function( el,ev,fn ){

   if( el.addEventListener ){
            el.addEventListener( ev,fn, false );
      }else if(el.attachEvent){
            el.attachEvent( "on" + ev, fn );
      } else{
           el["on" + ev] = fn;
    }

};
```
我们都熟知jQuery的$(document).ready(..)，使 用了一种类似的方式。在内部，这实际上是考一个叫做bindReady()的方法来驱动的，它做了一些这样的事：
```js
bindReady: function() {
    ...
    if ( document.addEventListener ) {
      // Use the handy event callback
      document.addEventListener( "DOMContentLoaded", DOMContentLoaded, false );

      // A fallback to window.onload, that will always work
      window.addEventListener( "load", jQuery.ready, false );

    // If IE event model is used
    } else if ( document.attachEvent ) {

      document.attachEvent( "onreadystatechange", DOMContentLoaded );

      // A fallback to window.onload, that will always work
      window.attachEvent( "onload", jQuery.ready );
```
这是门面的另外一个例子，其它人只需要使用被$(document).ready(...)有限暴露的简单接口，而更加复杂的实现被从视野中隐藏了。

门面不仅仅只被用在它们自己身上，它们也能够被用来同其它的模式诸如模块模式进行集成。如我们在下面所看到的，我们模块模式的实体包含许多被定义为私有的方法。门面则被用来提供访问这些方法的更加简单的API：
```js
var module = (function() {

    var _private = {
        i:5,
        get : function() {
            console.log( "current value:" + this.i);
        },
        set : function( val ) {
            this.i = val;
        },
        run : function() {
            console.log( "running" );
        },
        jump: function(){
            console.log( "jumping" );
        }
    };

    return {

        facade : function( args ) {
            _private.set(args.val);
            _private.get();
            if ( args.run ) {
                _private.run();
            }
        }
    };
}());
// Outputs: "current value: 10" and "running"
module.facade( {run: true, val:10} );
```
在这个示例中，调用module.facade()将会触发一堆模块中的私有方法。但再一次，用户并不需要关心这些。我们已经使得对用户而言不需要担心实现级别的细节就能消受一种特性。

关于抽象的注意事项
门面一般没有多少缺陷，但是性能是值得注意的问题。也就是说，需要确定门面在为我们提供实现的同时是否为我们带来了隐性的消耗，如果是这样的话，那么这种消耗是否合理。回到jQuery库，我们都知道`getElementById('identifier')`和`$("#identifier")`都能够被用来借助ID查找页面上的一个元素。

然而你是否知道getElementById()拥有更高数量级的速度呢？来瞧瞧这个jsPerf的测试，看一看在每一个浏览器级别的结果：http://jsperf.com/getelementbyid-vs-jquery-id。当然现在，我们应该牢记在心的是jQuery（和Sizzle-它的的选择器引擎）在幕后对我们的查询（而这返回的是一个jQuery对象，并不是一个DOM节点）做了更大量的优化。

这个特定的门面模式所面临的挑战就是，为了提供一种优雅的接受和转换多种查询类型的选择器功能，就会有在抽象上的隐性成本。用户并不需要访问`jQuery.getById("identifier")`或者`jQuery.getbyClass("identifier")`等等方法。那就是说，在性能上权衡已经通过了多年的实践考量，并且带了jQuery的成功，一个实际上为团队工作得很好的门面。

当使用这个模式的时候，尝试了解任何有关性能上面的消耗，要知道它们是否值得以抽象的级别被提供出来调用。

## 9.10 Factory（工厂）模式

工厂模式
工厂模式是另外一种关注对象创建概念的创建模式。它的领域中同其它模式的不同之处在于它并没有明确要求我们使用一个构造器。取而代之，一个工厂能提供一个创建对象的公共接口，我们可以在其中指定我们希望被创建的工厂对象的类型。

试想一下，在我们被要求创建一种类型的UI组件时，我们就有一个UI工厂。并不是通过直接使用new操作符或者通过另外一个构造器来创建这个组件，我们取而代之的向一个工厂对象索要一个新的组件。我们告知工厂我们需要什么类型的组件（例如：“按钮”，“面板”），而它会将其初始化，然后返回供我们使用。

如果创建过程相当复杂的话，那这会特别的有用，例如：如果它强烈依赖于动态因素或者应用程序配置的话。

这个模式的一些例子可以在UI库里面找到，例如ExtJS, 用于创建对象或者组件的方法可以被做更深层次的子类。 下面使用用我们之前的那些代码来做的一个例子，通过使用构造器模式逻辑来定义汽车。这个例子展示了Vehicle 工厂可以使用工厂模式来实现。
```js
// Types.js - Constructors used behind the scenes

// A constructor for defining new cars
function Car( options ) {

  // some defaults
  this.doors = options.doors || 4;
  this.state = options.state || "brand new";
  this.color = options.color || "silver";

}

// A constructor for defining new trucks
function Truck( options){

  this.state = options.state || "used";
  this.wheelSize = options.wheelSize || "large";
  this.color = options.color || "blue";
}

// FactoryExample.js

// Define a skeleton vehicle factory
function VehicleFactory() {}

// Define the prototypes and utilities for this factory

// Our default vehicleClass is Car
VehicleFactory.prototype.vehicleClass = Car;

// Our Factory method for creating new Vehicle instances
VehicleFactory.prototype.createVehicle = function ( options ) {

  if( options.vehicleType === "car" ){
    this.vehicleClass = Car;
  }else{
    this.vehicleClass = Truck;
  }

  return new this.vehicleClass( options );

};

// Create an instance of our factory that makes cars
var carFactory = new VehicleFactory();
var car = carFactory.createVehicle( {
            vehicleType: "car",
            color: "yellow",
            doors: 6 } );

// Test to confirm our car was created using the vehicleClass/prototype Car

// Outputs: true
console.log( car instanceof Car );

// Outputs: Car object of color "yellow", doors: 6 in a "brand new" state
console.log( car );
```
方法1: 修改 VehicleFactory 实例使用 Truck 类
```js
var movingTruck = carFactory.createVehicle( {
                      vehicleType: "truck",
                      state: "like new",
                      color: "red",
                      wheelSize: "small" } );

// Test to confirm our truck was created with the vehicleClass/prototype Truck

// Outputs: true
console.log( movingTruck instanceof Truck );

// Outputs: Truck object of color "red", a "like new" state
// and a "small" wheelSize
console.log( movingTruck );
```
方法2: 做 VehicleFactory 的子类用于创建一个工厂类生产 Trucks
```js
function TruckFactory () {}
TruckFactory.prototype = new VehicleFactory();
TruckFactory.prototype.vehicleClass = Truck;

var truckFactory = new TruckFactory();
var myBigTruck = truckFactory.createVehicle( {
                    state: "omg..so bad.",
                    color: "pink",
                    wheelSize: "so big" } );

// Confirms that myBigTruck was created with the prototype Truck
// Outputs: true
console.log( myBigTruck instanceof Truck );

// Outputs: Truck object with the color "pink", wheelSize "so big"
// and state "omg. so bad"
console.log( myBigTruck );
```
何时使用工厂模式
当被应用到下面的场景中时，工厂模式特别有用：

当我们的对象或者组件设置涉及到高程度级别的复杂度时。
当我们需要根据我们所在的环境方便的生成不同对象的实体时。
当我们在许多共享同一个属性的许多小型对象或组件上工作时。
当带有其它仅仅需要满足一种API约定(又名鸭式类型)的对象的组合对象工作时.这对于解耦来说是有用的。
何时不要去使用工厂模式
当被应用到错误的问题类型上时,这一模式会给应用程序引入大量不必要的复杂性.除非为创建对象提供一个接口是我们编写的库或者框架的一个设计上目标,否则我会建议使用明确的构造器,以避免不必要的开销。

由于对象的创建过程被高效的抽象在一个接口后面的事实,这也会给依赖于这个过程可能会有多复杂的单元测试带来问题。

抽象工厂
了解抽象工厂模式也是非常实用的,它的目标是以一个通用的目标将一组独立的工厂进行封装.它将一堆对象的实现细节从它们的一般用例中分离。

抽象工厂应该被用在一种必须从其创建或生成对象的方式处独立,或者需要同多种类型的对象一起工作,这样的系统中。

简单且容易理解的例子就是一个发动机工厂,它定义了获取或者注册发动机类型的方式.抽象工厂会被命名为AbstractVehicleFactory.抽象工厂将允许像"car"或者"truck"的发动机类型的定义,并且构造工厂将仅实现满足发动机合同的类.(例如:Vehicle.prototype.driven和Vehicle.prototype.breakDown)。
```js
var AbstractVehicleFactory = (function () {

    // Storage for our vehicle types
    var types = {};

    return {
        getVehicle: function ( type, customizations ) {
            var Vehicle = types[type];

            return (Vehicle ? new Vehicle(customizations) : null);
        },

        registerVehicle: function ( type, Vehicle ) {
            var proto = Vehicle.prototype;

            // only register classes that fulfill the vehicle contract
            if ( proto.drive && proto.breakDown ) {
                types[type] = Vehicle;
            }

            return AbstractVehicleFactory;
        }
    };
})();

// Usage:

AbstractVehicleFactory.registerVehicle( "car", Car );
AbstractVehicleFactory.registerVehicle( "truck", Truck );

// Instantiate a new car based on the abstract vehicle type
var car = AbstractVehicleFactory.getVehicle( "car" , {
            color: "lime green",
            state: "like new" } );

// Instantiate a new truck in a similar manner
var truck = AbstractVehicleFactory.getVehicle( "truck" , {
            wheelSize: "medium",
            color: "neon yellow" } );
```
## 9.11 Mixin模式

Mixin 模式
在诸如C++或者List着这样的传统语言中,织入模式就是一些提供能够被一个或者一组子类简单继承功能的类,意在重用其功能。

子类划分
对于不熟悉子类划分的开发者,在深入织入模式和装饰器模式之前,我们将对他们进行一个简短的初学者入门指引。

子类划分是一个参考了为一个新对象继承来自一个基类或者超类对象的属性的术语.在传统的面向对象编程中,类B能够从另外一个类A处扩展.这里我们将A看做是超类,而将B看做是A的子类.如此,所有B的实体都从A处继承了其A的方法.然而B仍然能够定义它自己的方法,包括那些重载的原本在A中的定义的方法。

B是否应该调用已经被重载的A中的方法,我们将这个引述为方法链.B是否应该调用A(超类)的构造器,我们将这称为构造器链。

为了演示子类划分,首先我们需要一个能够创建自身新实体的基对象。
```js
var Person =  function( firstName , lastName ){

  this.firstName = firstName;
  this.lastName =  lastName;
  this.gender = "male";

};
```
接下来,我们将制定一个新的类(对象),它是一个现有的Person对象的子类.让我们想象我们想要加入一个不同属性用来分辨一个Person和一个继承了Person"超类"属性的Superhero.由于超级英雄分享了一般人类许多共有的特征(例如:name,gender),因此这应该很有希望充分展示出子类划分是如何工作的。
```js
// a new instance of Person can then easily be created as follows:
var clark = new Person( "Clark" , "Kent" );

// Define a subclass constructor for for "Superhero":
var Superhero = function( firstName, lastName , powers ){

    // Invoke the superclass constructor on the new object
    // then use .call() to invoke the constructor as a method of
    // the object to be initialized.

    Person.call( this, firstName, lastName );

    // Finally, store their powers, a new array of traits not found in a normal "Person"
    this.powers = powers;
};

SuperHero.prototype = Object.create( Person.prototype );
var superman = new Superhero( "Clark" ,"Kent" , ["flight","heat-vision"] );
console.log( superman );

// Outputs Person attributes as well as powers
```
Superhero构造器创建了一个自Peroson下降的对象。这种类型的对象拥有链中位于它之上的对象的属性,而且如果我们在Person对象中设置了默认的值,Superhero能够使用特定于它的对象的值覆盖任何继承的值。

Mixin(织入目标类)
在Javascript中,我们会将从Mixin继承看作是通过扩展收集功能的一种途径.我们定义的每一个新的对象都有一个原型,从其中它可以继承更多的属性.原型可以从其他对象继承而来,但是更重要的是,能够为任意数量的对象定义属性.我们可以利用这一事实来促进功能重用。

Mix允许对象以最小量的复杂性从它们那里借用(或者说继承)功能.作为一种利用Javascript对象原型工作得很好的模式,它为我们提供了从不止一个Mix处分享功能的相当灵活,但比多继承有效得多得多的方式。

它们可以被看做是其属性和方法可以很容易的在其它大量对象原型共享的对象.想象一下我们定义了一个在一个标准对象字面量中含有实用功能的Mixin,如下所示:
```js
var myMixins = {

  moveUp: function(){
    console.log( "move up" );
  },

  moveDown: function(){
    console.log( "move down" );
  },

  stop: function(){
    console.log( "stop! in the name of love!" );
  }

};
```
然后我们可以方便的扩展现有构造器功能的原型,使其包含这种使用一个 如下面的score.js_.extends()方法辅助器的行为:
```js
// A skeleton carAnimator constructor
function carAnimator(){
  this.moveLeft = function(){
    console.log( "move left" );
  };
}

// A skeleton personAnimator constructor
function personAnimator(){
  this.moveRandomly = function(){ /*..*/ };
}

// Extend both constructors with our Mixin
_.extend( carAnimator.prototype, myMixins );
_.extend( personAnimator.prototype, myMixins );

// Create a new instance of carAnimator
var myAnimator = new carAnimator();
myAnimator.moveLeft();
myAnimator.moveDown();
myAnimator.stop();

// Outputs:
// move left
// move down
// stop! in the name of love!
```
如我们所见,这允许我们将通用的行为轻易的"混"入相当普通对象构造器中。

在接下来的示例中,我们有两个构造器:一个Car和一个Mixin.我们将要做的是静Car参数化(另外一种说法是扩展),以便它能够继承Mixin中的特定方法,名叫driveForwar()和driveBackward().这一次我们不会使用Underscore.js。

取而代之，这个示例将演示如何将一个构造器参数化，以便在无需重复每一个构造器函数过程的前提下包含其功能。
```js
// Define a simple Car constructor
var Car = function ( settings ) {

        this.model = settings.model || "no model provided";
        this.color = settings.color || "no colour provided";

    };

// Mixin
var Mixin = function () {};

Mixin.prototype = {

    driveForward: function () {
        console.log( "drive forward" );
    },

    driveBackward: function () {
        console.log( "drive backward" );
    },

    driveSideways: function () {
        console.log( "drive sideways" );
    }

};

// Extend an existing object with a method from another
function augment( receivingClass, givingClass ) {

    // only provide certain methods
    if ( arguments[2] ) {
        for ( var i = 2, len = arguments.length; i < len; i++ ) {
            receivingClass.prototype[arguments[i]] = givingClass.prototype[arguments[i]];
        }
    }
    // provide all methods
    else {
        for ( var methodName in givingClass.prototype ) {

            // check to make sure the receiving class doesn't
            // have a method of the same name as the one currently
            // being processed
            if ( !Object.hasOwnProperty(receivingClass.prototype, methodName) ) {
                receivingClass.prototype[methodName] = givingClass.prototype[methodName];
            }

            // Alternatively:
            // if ( !receivingClass.prototype[methodName] ) {
            //  receivingClass.prototype[methodName] = givingClass.prototype[methodName];
            // }
        }
    }
}

// Augment the Car constructor to include "driveForward" and "driveBackward"
augment( Car, Mixin, "driveForward", "driveBackward" );

// Create a new Car
var myCar = new Car({
    model: "Ford Escort",
    color: "blue"
});

// Test to make sure we now have access to the methods
myCar.driveForward();
myCar.driveBackward();

// Outputs:
// drive forward
// drive backward

// We can also augment Car to include all functions from our mixin
// by not explicitly listing a selection of them
augment( Car, Mixin );

var mySportsCar = new Car({
    model: "Porsche",
    color: "red"
});

mySportsCar.driveSideways();

// Outputs:
// drive sideways
```
优点&缺点
Mixin支持在一个系统中降解功能的重复性,增加功能的重用性.在一些应用程序也许需要在所有的对象实体共享行为的地方,我们能够通过在一个Mixin中维护这个共享的功能,来很容易的避免任何重复,而因此专注于只实现我们系统中真正彼此不同的功能。

也就是说,对Mixin的副作用是值得商榷的.一些开发者感觉将功能注入到对象的原型中是一个坏点子,因为它会同时导致原型污染和一定程度上的对我们原有功能的不确定性.在大型的系统中,很可能是有这种情况的。

我认为,强大的文档对最大限度的减少对待功能中的混入源的迷惑是有帮助的,而且对于每一种模式而言,如果在实现过程中小心行事,我们应该是没多大问题的。

## 9.12 Decorator（装饰者）模式

装饰模式
装饰器是旨在提升重用性能的一种结构性设计模式。同Mixin类似，它可以被看作是应用子类划分的另外一种有价值的可选方案。

典型的装饰器提供了向一个系统中现有的类动态添加行为的能力。其创意是装饰本身并不关心类的基础功能，而只是将它自身拷贝到超类之中。

它们能够被用来在不需要深度改变使用它们的对象的依赖代码的前提下，变更我们希望向其中附加功能的现有系统之中。开发者使用它们的一个通常的理由是，它们的应用程序也许包含了需要大量彼此不相干类型对象的特性。想象一下不得不要去定义上百个不同对象的构造器，比方说，一个Javascript游戏。

对象构造器可以代表不同播放器类型，每一种类型具有不同的功能。一种叫做领主戒指的游戏会需要霍比特人、巫术师，兽人，巨兽，精灵，山岭巨人，乱世陆地等对象的构造器，而这些的数量很容易过百。而我们还要考虑为每一个类型的能力组合创建子类。

例如，带指环的霍比特人，带剑的霍比特人和插满宝剑的陆地等等。这并不是非常的实用，当我们考虑到不同能力的数量在不断增长这一因素时，最后肯定是不可控的。

装饰器模式并不去深入依赖于对象是如何创建的，而是专注于扩展它们的功能这一问题上。不同于只依赖于原型继承，我们在一个简单的基础对象上面逐步添加能够提供附加功能的装饰对象。它的想法是，不同于子类划分，我们向一个基础对象添加（装饰）属性或者方法，因此它会是更加轻巧的。

向Javascript中的对象添加新的属性是一个非常直接了当的过程，因此将这一特定牢记于心，一个非常简单的装饰器可以实现如下：

示例1：带有新功能的装饰构造器
```js
// A vehicle constructor
function vehicle( vehicleType ){

    // some sane defaults
    this.vehicleType = vehicleType || "car";
    this.model = "default";
    this.license = "00000-000";

}

// Test instance for a basic vehicle
var testInstance = new vehicle( "car" );
console.log( testInstance );

// Outputs:
// vehicle: car, model:default, license: 00000-000

// Lets create a new instance of vehicle, to be decorated
var truck = new vehicle( "truck" );

// New functionality we're decorating vehicle with
truck.setModel = function( modelName ){
    this.model = modelName;
};

truck.setColor = function( color ){
    this.color = color;
};

// Test the value setters and value assignment works correctly
truck.setModel( "CAT" );
truck.setColor( "blue" );

console.log( truck );

// Outputs:
// vehicle:truck, model:CAT, color: blue

// Demonstrate "vehicle" is still unaltered
var secondInstance = new vehicle( "car" );
console.log( secondInstance );

// Outputs:
// vehicle: car, model:default, license: 00000-000
```
这种类型的简单实现是实用的，但它没有真正展示出装饰能够贡献出来的全部潜能。为这个，我们首先区分一下我的Coffee示例和Freeman，Sierra和Bates所著Head First Design Patterns这一本优秀的书中围绕Mackbook商店建立的模型，这两个之间的不同。

示例2：带有多个装饰器的装饰对象
```js
// The constructor to decorate
function MacBook() {

  this.cost = function () { return 997; };
  this.screenSize = function () { return 11.6; };

}

// Decorator 1
function Memory( macbook ) {

  var v = macbook.cost();
  macbook.cost = function() {
    return v + 75;
  };

}

// Decorator 2
function Engraving( macbook ){

  var v = macbook.cost();
  macbook.cost = function(){
    return  v + 200;
  };

}

// Decorator 3
function Insurance( macbook ){

  var v = macbook.cost();
  macbook.cost = function(){
     return  v + 250;
  };

}

var mb = new MacBook();
Memory( mb );
Engraving( mb );
Insurance( mb );

// Outputs: 1522
console.log( mb.cost() );

// Outputs: 11.6
console.log( mb.screenSize() );
```
在上面的示例中，我们的装饰器重载了超类对象MacBook()的 object.cost()函数，使其返回的Macbook的当前价格加上了被定制后升级的价格。

这被看做是对原来的Macbook对象构造器方法的装饰，它并没有将其重写（例如，screenSize())，我们所定义的Macbook的其它属性也保持不变，完好无缺。

上面的示例并没有真正定义什么接口，而且我们也转移了从创造者到接受者移动时确保一个对象对应一个接口的责任。

伪古典装饰器
我们现在要来试试首见于Dustin Diaz与Ross Harmes合著的Pro Javascript Design Patterns（PJDP）中一种装饰器的变体。

不像早些时候的一些实例，Diaz和Harms坚持更加近似于其他编程语言（如Java或者C++)如何使用一种“接口”的概念来实现装饰器，我们不久就将对此进行详细的定义。

注意：装饰模式的这一特殊变体是提供出来做参考用的。如果发现它过于复杂，建议你选择前面更加简单的实现。

接口
PJDP所描述的装饰器是一种被用于将具备相同接口的对象进行透明封装的对象，这样一种模式。接口是一种定义一个对象应该具有哪些方法的途径，然而，它实际上并不指定那些方法应该如何实现。

它们也可以声明方法应该有些什么参数，但这被看做是可选项。

因此，为什么我们要在Javascript中使用接口呢？这个想法意在让它们具有自说明文档特性，并促进其重用性。在理论上，接口通过确保了其被改变的同时也要让其对象实现这些改变，从而使得代码更加的稳定。

下面是一个在Javascript中使用鸭式类型来实现接口的示例，鸭式类型是一种基于所实现的方法来帮助判定一个对象是否是一种构造器/对象的实体的方法。

```js
// Create interfaces using a pre-defined Interface
// constructor that accepts an interface name and
// skeleton methods to expose.

// In our reminder example summary() and placeOrder()
// represent functionality the interface should
// support
var reminder = new Interface( "List", ["summary", "placeOrder"] );

var properties = {
  name: "Remember to buy the milk",
  date: "05/06/2016",
  actions:{
    summary: function (){
      return "Remember to buy the milk, we are almost out!";
   },
    placeOrder: function (){
      return "Ordering milk from your local grocery store";
    }
  }
};

// Now create a constructor implementing the above properties
// and methods

function Todo( config ){

  // State the methods we expect to be supported
  // as well as the Interface instance being checked
  // against

  Interface.ensureImplements( config.actions, reminder );

  this.name = config.name;
  this.methods = config.actions;

}

// Create a new instance of our Todo constructor

var todoItem = Todo( properties );

// Finally test to make sure these function correctly

console.log( todoItem.methods.summary() );
console.log( todoItem.methods.placeOrder() );

// Outputs:
// Remember to buy the milk, we are almost out!
// Ordering milk from your local grocery store
```
在上面的代码中，接口确保了实现提供严格的功能检查，而这个和接口构造器的接口代码能在这里找到。

使用接口最大的问题是，由于这并不是Javascript内置的对它们的支持，对我们而言就会存在尝试去模仿另外一种语言的特性，但看着并不完全合适，这样一种风险。然而对于没有太大性能消耗的轻量级接口是可以被使用的，并且下面我们将要看到的抽象装饰器同样使用了这个概念。

抽象装饰者
为了阐明这个版本的装饰者模式的结构，我们想象有一个超级类，还是一个Macbook模型，以及一个store，使我们可以用耗费额外费用的许多种增强来“装饰”Macbook。

增强可以包括升级到4GB或8GB的Ram，雕刻，或相似案例。如果现在我们要针对每一种增强选项的组合，使用单独的子类进行建模，可能看起来是这样的：

```js
var Macbook = function(){
        //...
};

var  MacbookWith4GBRam =  function(){},
     MacbookWith8GBRam = function(){},
     MacbookWith4GBRamAndEngraving = function(){},
     MacbookWith8GBRamAndEngraving = function(){},
     MacbookWith8GBRamAndParallels = function(){},
     MacbookWith4GBRamAndParallels = function(){},
     MacbookWith8GBRamAndParallelsAndCase = function(){},
     MacbookWith4GBRamAndParallelsAndCase = function(){},
     MacbookWith8GBRamAndParallelsAndCaseAndInsurance = function(){},
     MacbookWith4GBRamAndParallelsAndCaseAndInsurance = function(){};
```
等等。

这不是一个实际的解决方案，因为一个新的子类可能需要具有每一种可能的增强组合。由于我们倾向于保持事物简单，不想维持一个巨大的子类集合，我们来看看怎样用装饰者更好的解决这个问题。

不需要我们前面看到的所有组合，我们只需要简单的创建五个新的装饰者类。对这些增强类的方法调用，将会传递给Macbook类。

在我们下一个例子中，装饰者透明的包装了它们的组件，而且有趣的是，可以在相同的接口互换。

这里是我们给Macbook定义的接口：

```js
var Macbook = new Interface( "Macbook",
  ["addEngraving",
  "addParallels",
  "add4GBRam",
  "add8GBRam",
  "addCase"]);

// A Macbook Pro might thus be represented as follows:
var MacbookPro = function(){
    // implements Macbook
};

MacbookPro.prototype = {
    addEngraving: function(){
    },
    addParallels: function(){
    },
    add4GBRam: function(){
    },
    add8GBRam:function(){
    },
    addCase: function(){
    },
    getPrice: function(){
      // Base price
      return 900.00;        
    }
};
```
为了使得我们稍后更加容易的添加所需的更多选项，一种带有被用来实现Mackbook接口的默认方法的抽象装饰器方法被定义了出来，其剩余的选项将会进行子类划分。抽象装饰器确保了我们能够独立于尽可能多的在不同的组合中所需的装饰器，去装饰一个基础类（记得早先的那个示例么？），而不需要去为了每一种可能的组合而去驱动一个类。

```js
// Macbook decorator abstract decorator class

var MacbookDecorator = function( macbook ){

    Interface.ensureImplements( macbook, Macbook );
    this.macbook = macbook; 

};

MacbookDecorator.prototype = {
    addEngraving: function(){
        return this.macbook.addEngraving();
    },
    addParallels: function(){
        return this.macbook.addParallels();
    },
    add4GBRam: function(){
        return this.macbook.add4GBRam();
    },
    add8GBRam:function(){
        return this.macbook.add8GBRam();
    },
    addCase: function(){
        return this.macbook.addCase();
    },
    getPrice: function(){
        return this.macbook.getPrice();
    }       
};
```
上述示例中所发生的是Macbook装饰器在像组件一样的使用一个对象。它使用了我们早先定义的Macbook接口，对于每一个方法都调用了组件上相同的方法。我们现在就能够只使用Macbook装饰器来创建我们的选项类了——通过简单调用超类的构造器和根据需要可以被重载的方法。

```js
var CaseDecorator = function( macbook ){

   // call the superclass's constructor next
   this.superclass.constructor( macbook );  

};

// Let's now extend the superclass
extend( CaseDecorator, MacbookDecorator );

CaseDecorator.prototype.addCase = function(){
    return this.macbook.addCase() + "Adding case to macbook";  
};

CaseDecorator.prototype.getPrice = function(){
    return this.macbook.getPrice() + 45.00; 
};
```
如我们所见，大多数都是相对应的直接实现。我们所做的是重载需要被装饰的addCase()和getPrise()方法，而我们通过首先执行组件的方法然后将其添加到它里面，来达到目的。

鉴于到目前为止本节所介绍的信息一斤相当的多了，让我们试试将其全部放到一个单独的实例中，以期突出我们所学。

```js
// Instantiation of the macbook
var myMacbookPro = new MacbookPro(); 

// Outputs: 900.00
console.log( myMacbookPro.getPrice() );

// Decorate the macbook
myMacbookPro = new CaseDecorator( myMacbookPro );

// This will return 945.00
console.log( myMacbookPro.getPrice() );
```
由于装饰器能够动态的修改对象，它们就是改变现有系统的理想模式。有时候，它只是简单的围绕一个对象及其维护针对每一个对象类型单独的子类划分所产生的麻烦，来创建装饰器的。这使得维护起可能需要大量子类划分对象的应用程序来更加显著的直接。

装饰器和jQuery
同我们所涵盖的其它模式一起，也有许多装饰器模式的示例能够使用jQuery来实现。jQuery.extend()允许我们将两个或者更多个对象（以及它们的属性）扩展（或者混合）到一个对象中，不论是在运行时或者动态的在一个稍后的时点上。

在这一场景中，目标对象没必要打断或者重载源/超类中现有的方法（尽管这可以被做到）就能够使用新的功能装饰起来。 在接下来的示例中，我们定义了三个对象：默认，选项和设置。任务的目标是用在选项中找到的附加功能来装饰默认对象。

将“默认”放置在一个不可触及的状态之中，在这里我们不会失去访问稍后会在其中发现的属性和方法的能力
赢得了使用在“选项”中找到被装饰起来的属性和函数的能力。
```js
var decoratorApp = decoratorApp || {};

// define the objects we're going to use
decoratorApp = {

    defaults: {
        validate: false,
        limit: 5,
        name: "foo",
        welcome: function () {
            console.log( "welcome!" );
        }
    },

    options: {
        validate: true,
        name: "bar",
        helloWorld: function () {
            console.log( "hello world" );
        }
    },

    settings: {},

    printObj: function ( obj ) {
        var arr = [],
            next;
        $.each( obj, function ( key, val ) {
            next = key + ": ";
            next += $.isPlainObject(val) ? printObj( val ) : val;
            arr.push( next );
        } );

        return "{ " + arr.join(", ") + " }";
    }

};

// merge defaults and options, without modifying defaults explicitly
decoratorApp.settings = $.extend({}, decoratorApp.defaults, decoratorApp.options);

// what we have done here is decorated defaults in a way that provides
// access to the properties and functionality it has to offer (as well as
// that of the decorator "options"). defaults itself is left unchanged

$("#log")
    .append( decoratorApp.printObj(decoratorApp.settings) + 
          + decoratorApp.printObj(decoratorApp.options) +
          + decoratorApp.printObj(decoratorApp.defaults));

// settings -- { validate: true, limit: 5, name: bar, welcome: function (){ console.log( "welcome!" ); },
// helloWorld: function (){ console.log("hello!"); } }
// options -- { validate: true, name: bar, helloWorld: function (){ console.log("hello!"); } }
// defaults -- { validate: false, limit: 5, name: foo, welcome: function (){ console.log("welcome!"); } }
```
优点 & 缺点
因为它可以被透明的使用，并且也相当的灵活，因此开发者都挺乐意去使用这个模式——如我们所见，对象可以用新的行为封装或者“装饰”起来，而后继续使用，并不用去担心基础的对象被改变。在一个更加广泛的范围内，这一模式也避免了我们去依赖大量子类来实现同样的效果。

然而在实现这个模式时，也存在我们应该意识到的缺点。如果穷于管理，它也会由于引入了许多微小但是相似的对象到我们的命名空间中，从而显著的使得我们的应用程序架构变得复杂起来。这里所担忧的是，除了渐渐变得难于管理，其他不能熟练使用这个模式的开发者也可能会有一段要掌握它被使用的理由的艰难时期。

足够的注释或者对模式的研究，对此应该有助益，而只要我们对在我们的应程序中的多大范围内使用这一模式有所掌控的话，我们就能让两方面都得到改善。

## 9.13 Flyweight（享元）模式

亨元模式
享元模式是一个优化重复、缓慢和低效数据共享代码的经典结构化解决方案。它的目标是以相关对象尽可能多的共享数据，来减少应用程序中内存的使用(例如：应用程序的配置、状态等)。

此模式最先由Paul Calder 和 Mark Linton在1990提出，并用拳击等级中少于112磅体重的等级名称来命名。享元(“Flyweight”英语中的轻量级)的名称本身是从以帮以助我们完成减少重量(内存标记)为目标的重量等级推导出的。

实际应用中，轻量级的数据共享采集被多个对象使用的相似对象或数据结构，并将这些数据放置于单个的扩展对象中。我们可以把它传递给依靠这些数据的对象，而不是在他们每个上面都存储一次。

使用享元
有两种方法来使用享元。第一种是数据层，基于存储在内存中的大量相同对象的数据共享的概念。第二种是DOM层，享元模式被作为事件管理中心，以避免将事件处理程序关联到我们需要相同行为父容器的所有子节点上。 享元模式通常被更多的用于数据层，我们先来看看它。

享元和数据共享
对于这个应用程序而言，围绕经典的享元模式有更多需要我们意识到的概念。享元模式中有一个两种状态的概念——内在和外在。内在信息可能会被我们的对象中的内部方法所需要，它们绝对不可以作为功能被带出。外在信息则可以被移除或者放在外部存储。

带有相同内在数据的对象可以被一个单独的共享对象所代替，它通过一个工厂方法被创建出来。这允许我们去显著降低隐式数据的存储数量。

个中的好处是我们能够留心于已经被初始化的对象，让只有不同于我们已经拥有的对象的内在状态时，新的拷贝才会被创建。

我们使用一个管理器来处理外在状态。如何实现可以有所不同，但针对此的一种方法就是让管理器对象包含一个存储外在状态以及它们所属的享元对象的中心数据库。

经典的享元实现
近几年享元模式已经在Javascript中得到了深入的应用，我们会用到的许多实现方式其灵感来自于Java和C++的世界。

我们第一个要来看的关于享元模式的代码是我的对来自维基百科的针对享元模式的 Java 示例的 Javascript 实现。

在这个实现中我们将要使用如下所列的三种类型的享元组件：

享元对应的是一个接口，通过此接口能够接受和控制外在状态。
构造享元来实际的实际的实现接口，并存储内在状态。构造享元须是能够被共享的，并且具有操作外在状态的能力。
享元工厂负责管理享元对象，并且也创建它们。它确保了我们的享元对象是共享的，并且可以对其作为一组对象进行管理，这一组对象可以在我们需要的时候查询其中的单个实体。如果一个对象已经在一个组里面创建好了，那它就会返回该对象，否则它会在对象池中新创建一个，并且返回之。
这些对应于我们实现中的如下定义：

CoffeeOrder：享元
CoffeeFlavor：构造享元
CoffeeOrderContext：辅助器
CoffeeFlavorFactory：享元工厂
testFlyweight：对我们享元的使用
鸭式冲减的 “implements”
鸭式冲减允许我们扩展一种语言或者解决方法的能力，而不需要变更运行时的源。由于接下的方案需要使用一个Java关键字“implements”来实现接口，而在Javascript本地看不到这种方案，那就让我们首先来对它进行鸭式冲减。

Function.prototype.implementsFor 在一个对象构造器上面起作用，并且将接受一个父类（函数—）或者对象，而从继承于普通的继承（对于函数而言）或者虚拟继承（对于对象而言）都可以。

```js
// Simulate pure virtual inheritance/"implement" keyword for JS
Function.prototype.implementsFor = function( parentClassOrObject ){
    if ( parentClassOrObject.constructor === Function )
    {
        // Normal Inheritance
        this.prototype = new parentClassOrObject();
        this.prototype.constructor = this;
        this.prototype.parent = parentClassOrObject.prototype;
    }
    else
    {
        // Pure Virtual Inheritance
        this.prototype = parentClassOrObject;
        this.prototype.constructor = this;
        this.prototype.parent = parentClassOrObject;
    }
    return this;
};
```

我们可以通过让一个函数明确的继承自一个接口来弥补implements关键字的缺失。下面，为了使我们得以去分配支持一个对象的这些实现的功能，CoffeeFlavor实现了CoffeeOrder接口，并且必须包含其接口的方法。

```js
// Flyweight object
var CoffeeOrder = {

  // Interfaces
  serveCoffee:function(context){},
    getFlavor:function(){}

};

// ConcreteFlyweight object that creates ConcreteFlyweight
// Implements CoffeeOrder
function CoffeeFlavor( newFlavor ){

    var flavor = newFlavor;

    // If an interface has been defined for a feature
    // implement the feature
    if( typeof this.getFlavor === "function" ){
      this.getFlavor = function() {
          return flavor;
      };
    }

    if( typeof this.serveCoffee === "function" ){
      this.serveCoffee = function( context ) {
        console.log("Serving Coffee flavor "
          + flavor
          + " to table number "
          + context.getTable());
    };     
    }

}

// Implement interface for CoffeeOrder
CoffeeFlavor.implementsFor( CoffeeOrder );

// Handle table numbers for a coffee order
function CoffeeOrderContext( tableNumber ) {
   return{
      getTable: function() {
         return tableNumber;
     }
   };
}

function CoffeeFlavorFactory() {
    var flavors = {},
    length = 0;

    return {
        getCoffeeFlavor: function (flavorName) {

            var flavor = flavors[flavorName];
            if (flavor === undefined) {
                flavor = new CoffeeFlavor(flavorName);
                flavors[flavorName] = flavor;
                length++;
            }
            return flavor;
        },

        getTotalCoffeeFlavorsMade: function () {
            return length;
        }
    };
}

// Sample usage:
// testFlyweight()

function testFlyweight(){

  // The flavors ordered.
  var flavors = new CoffeeFlavor(),

  // The tables for the orders.
    tables = new CoffeeOrderContext(),

  // Number of orders made
    ordersMade = 0,

  // The CoffeeFlavorFactory instance
    flavorFactory;

  function takeOrders( flavorIn, table) {
     flavors[ordersMade] = flavorFactory.getCoffeeFlavor( flavorIn );
     tables[ordersMade++] = new CoffeeOrderContext( table );
  }

   flavorFactory = new CoffeeFlavorFactory();

   takeOrders("Cappuccino", 2);
   takeOrders("Cappuccino", 2);
   takeOrders("Frappe", 1);
   takeOrders("Frappe", 1);
   takeOrders("Xpresso", 1);
   takeOrders("Frappe", 897);
   takeOrders("Cappuccino", 97);
   takeOrders("Cappuccino", 97);
   takeOrders("Frappe", 3);
   takeOrders("Xpresso", 3);
   takeOrders("Cappuccino", 3);
   takeOrders("Xpresso", 96);
   takeOrders("Frappe", 552);
   takeOrders("Cappuccino", 121);
   takeOrders("Xpresso", 121);

   for (var i = 0; i < ordersMade; ++i) {
       flavors[i].serveCoffee(tables[i]);
   }
   console.log(" ");
   console.log("total CoffeeFlavor objects made: " +  flavorFactory.getTotalCoffeeFlavorsMade());
} 
```
转换代码为使用享元模式
接下来，让我们通过实现一个管理一个图书馆中所有书籍的系统来继续观察享元。分析得知每一本书的重要元数据如下：

ID
标题
作者
类型
总页数
出版商ID
ISBN
我们也将需要下面一些属性，来跟踪哪一个成员是被借出的一本特定的书，借出它们的日期，还有预计的归还日期。

借出日期
借出的成员
规定归还时间
可用性
```js
var Book = function( id, title, author, genre, pageCount,publisherID, ISBN, checkoutDate, checkoutMember, dueReturnDate,availability ){

   this.id = id;
   this.title = title;
   this.author = author;
   this.genre = genre;
   this.pageCount = pageCount;
   this.publisherID = publisherID;
   this.ISBN = ISBN;
   this.checkoutDate = checkoutDate;
   this.checkoutMember = checkoutMember;
   this.dueReturnDate = dueReturnDate;
   this.availability = availability;

};

Book.prototype = {

  getTitle: function () {
     return this.title;
  },

  getAuthor: function () {
     return this.author;
  },

  getISBN: function (){
     return this.ISBN;
  },

  // For brevity, other getters are not shown
  updateCheckoutStatus: function( bookID, newStatus, checkoutDate , checkoutMember, newReturnDate ){

     this.id  = bookID;
     this.availability = newStatus;
     this.checkoutDate = checkoutDate;
     this.checkoutMember = checkoutMember;
     this.dueReturnDate = newReturnDate;

  },

  extendCheckoutPeriod: function( bookID, newReturnDate ){

      this.id =  bookID;
      this.dueReturnDate = newReturnDate;

  },

  isPastDue: function(bookID){

     var currentDate = new Date();
     return currentDate.getTime() > Date.parse( this.dueReturnDate );

   }
};
```
这对于最初小规模的藏书可能工作得还好，然而当图书馆扩充至每一本书的多个版本和可用的备份，这样一个大型的库存，我们会发现管理系统的运行随着时间的推移会越来越慢。使用成千上万的书籍对象可能会压倒内存，而我们可以通过享元模式的提升来优化我们的系统。

现在我们可以像下面这样将我们的数据分离成为内在和外在的状态：同书籍对象（标题，版权归属）相关的数据是内在的，而借出数据（借出成员，规定归还日期）则被看做是外在的。这实际上意味着对于每一种书籍属性的组合仅需要一个书籍对象。这仍然具有相当大的数量，但相比之前已经得到大大的缩减了。

下面的书籍元数据组合的单一实体将在所有带有一个特定标题的书籍拷贝中共享。

```js
// Flyweight optimized version
var Book = function ( title, author, genre, pageCount, publisherID, ISBN ) {

    this.title = title;
    this.author = author;
    this.genre = genre;
    this.pageCount = pageCount;
    this.publisherID = publisherID;
    this.ISBN = ISBN;

};
```
如我们所见，外在状态已经被移除了。从图书馆借出所要做的一切都被转移到一个管理器中，由于对象数据现在是分段的，工厂可以被用来做实例化。

一个基本工厂
现在让我们定义一个非常基本的工厂。我们用它做的工作是，执行一个检查来看看一本给定标题的书是不是之前已经在系统内创建过了；如果创建过了，我们就返回它 - 如果没有，一本新书就会被创建并保存，使得以后可以访问它。这确保了为每一条本质上唯一的数据，我们只创建了一份单一的拷贝:

```js
// Book Factory singleton
var BookFactory = (function () {
  var existingBooks = {}, existingBook;

  return {
    createBook: function ( title, author, genre, pageCount, publisherID, ISBN ) {

      // Find out if a particular book meta-data combination has been created before
      // !! or (bang bang) forces a boolean to be returned
      existingBook = existingBooks[ISBN];
      if ( !!existingBook ) {
        return existingBook;
      } else {

        // if not, let's create a new instance of the book and store it
        var book = new Book( title, author, genre, pageCount, publisherID, ISBN );
        existingBooks[ISBN] = book;
        return book;

      }
    }
  };

});
```
管理外在状态
下一步，我们需要将那些从Book对象中移除的状态存储到某一个地方——幸运的是一个管理器（我们会将其定义成一个单例）可以被用来封装它们。书籍对象和借出这些书籍的图书馆成员的组合将被称作书籍借出记录。这些我们的管理器都将会存储，并且也包含我们在对Book类进行享元优化期间剥离的同借出相关的逻辑。

```js
// BookRecordManager singleton
var BookRecordManager = (function () {

  var bookRecordDatabase = {};

  return {
    // add a new book into the library system
    addBookRecord: function ( id, title, author, genre, pageCount, publisherID, ISBN, checkoutDate, checkoutMember, dueReturnDate, availability ) {

      var book = bookFactory.createBook( title, author, genre, pageCount, publisherID, ISBN );

      bookRecordDatabase[id] = {
        checkoutMember: checkoutMember,
        checkoutDate: checkoutDate,
        dueReturnDate: dueReturnDate,
        availability: availability,
        book: book
      };
    },
    updateCheckoutStatus: function ( bookID, newStatus, checkoutDate, checkoutMember, newReturnDate ) {

      var record = bookRecordDatabase[bookID];
      record.availability = newStatus;
      record.checkoutDate = checkoutDate;
      record.checkoutMember = checkoutMember;
      record.dueReturnDate = newReturnDate;
    },

    extendCheckoutPeriod: function ( bookID, newReturnDate ) {
      bookRecordDatabase[bookID].dueReturnDate = newReturnDate;
    },

    isPastDue: function ( bookID ) {
      var currentDate = new Date();
      return currentDate.getTime() > Date.parse( bookRecordDatabase[bookID].dueReturnDate );
    }
  };

});
```
这些改变的结果是所有从Book类中撷取的数据现在被存储到了BookManager单例（BookDatabase）的一个属性之中——与我们以前使用大量对象相比可以被认为是更加高效的东西。同书籍借出相关的方法也被设置在这里，因为它们处理的数据是外在的而不内在的。

这个过程确实给我们最终的解决方法增加了一点点复杂性，然而同已经明智解决的数据性能问题相比，这只是一个小担忧，如果我们有同一本书的30份拷贝，现在我们只需要存储它一次就够了。每一个函数也会占用内存。使用享元模式这些函数只在一个地方存在（就是在管理器上），并且不是在每一个对象上面，这节约了内存上的使用。

享元模式和DOM
DOM（文档对象模型）支持两种允许对象侦听事件的方法——自顶向下（事件捕获）或者自底向下（时间冒泡）。 在事件捕获中，事件一开始会被最外面的元素捕获，并且传播到最里面的元素。在事件冒泡中，事件被捕获并且被赋给了最里面的元素，然后传播到最外面的元素。

在此背景下描述享元模式的最好隐喻来自Gary Chisholm写的文章，这里摘录了一点点：

尝试用一种池塘的方式思考享元模式。一只鱼张开了它的嘴巴（事件发生了），泡泡一直要上升到表面（冒泡），当泡泡到达表面时，停泊在顶部的一直苍蝇飞走了（动作执行）。在这个示例中我们能够很容易的将鱼张开嘴巴转换为按钮被点击了一下，将泡泡转换为冒泡效果，而苍蝇飞走了表示一些需要运行的函数。

冒泡被引入用来处理单个事件（比如：一次点击）可能会由在DOM层级中的不同级别的多个事件处理器处理，这样的场景。这在哪里发生了，事件冒泡就会为在尽可能最低的级别定义的事件处理器执行。从那里开始，事件向上冒泡，一直到包含比应该包含的更高层级的元素。

享元模式可用来进一步调整事件冒泡过程，这我们很快就将会看到。

例子1：集中式事件处理
一起来看看我们第一例子，当用户有个动作(如点击或是鼠标移动)时我们将有很多相似的文档对象以及相似的行为要处理。一般情况下，当我们构建手风琴式控件，菜单以及其它列表控件时，就会在每一个超链接元素父容器里绑定点击事件(如，$('ul li a').on(..)(jQuery代码,译者注))。我们可以方便的在可以监听事件容器里添加Flyweight，而不是在很多元素里绑定点击事件。这样就可处理或是简单或是复杂的需求。

提到组件的类型，经常会涉及到很多部分都有同样重复的标签(如，手风琴式控件)，这是个好机会，每个元素都有可能被点击的行为，而且基本上用相同的类。我们可以用Flyweight来构建一个基本的手风琴控件。

这里我们使用一个stateManager命名空间来封装我们的享元逻辑，同时使用jQuery来把初始点击事件绑定到一个div容器上。为了确保页面上没有其他程序逻辑把类似的处理器绑定到该容器上，首先使用了一个unbind事件。

现在明确的确立一下容器中的那个子元素会被点击，我们使用一次对target的检查来提供对被点击元素的引用，而不管它的父元素是谁。然后我们利用该信息来处理点击事件，而实际上不需要在页面装载时把该事件绑定到具体的子元素上。

HTML
```html
<div id="container">
   <div class="toggle" href="#">More Info (Address)
       <span class="info">
           This is more information
       </span></div>
   <div class="toggle" href="#">Even More Info (Map)
       <span class="info">
          <iframe src="https://atts.w3cschool.cn/attachments/image/cimg/extmap.php?name=London&address=london%2C%20england&amp;width=500...gt;"</iframe>
       </span>
   </div>
</div>
JavaScript
var stateManager = {

  fly: function () {

    var self = this;

    $( "#container" ).unbind().on( "click" , function ( e ) {
      var target = $( e.originalTarget || e.srcElement );
        if ( target.is( "div.toggle") ) {
          self.handleClick( target );
        }
    });
  },

  handleClick: function ( elem ) {
    elem.find( "span" ).toggle( "slow" );
  }
};
```
这样做的好处是，我们把许多不相关的动作转换为一个可以共享的动作(也许会保存在内存中)。

示例2：使用享元进行性能优化
在我们的第二个示例中，我们将会引述通过使用jQuery的享元可以获得的一些更多的性能上的收获。

Jame Padolsey 以前写过一篇叫做76比特的文章，讲述更快的jQuery，在其中他提醒我们每一次jQuery触发了一个回调，不管是什么类型（过滤器，每一个，事件处理器），我们都能够通过this关键字访问函数的上下文（与它相关的DOM元素）。

不幸的是，我们中的许多人已经习惯将this封装到$()或者jQuery()中的想法，这意味着新的jQuery实体没必要每次都被构造出来，而是简单的这样做：

```js
$("div").on( "click", function () {
  console.log( "You clicked: " + $( this ).attr( "id" ));
});

// we should avoid using the DOM element to create a
// jQuery object (with the overhead that comes with it)
// and just use the DOM element itself like this:

$( "div" ).on( "click", function () {
  console.log( "You clicked:"  + this.id );
});
James想要下面的场景中使用jQuery的jQuery.text，然而他不能苟同一个新的jQuery对象必须在每次迭代中创建的概念。

$( "a" ).map( function () {
  return $( this ).text();
});
```
现在就使用jQuery的工具方法进行多余的包装而言，使用jQuery.methodName(如，jQuery.text）比jQuery.fn.methodName（如，jQuery.fn.text）更好，这里methodName代表了一种使用的工具，如each()或者text。这避免了调用更深远级别的抽象，或者每一次当我们的函数被调用时就构造一个新的jQuery对象，因为定义了jQuery.methodName的库本身在更底层使用jQuery.fn.methodName驱动的。

然而由于并不是所有jQuery的方法都有相应的单节点功能，Padolsey根据这个创意设计了jQuery.single工具。 这里的创意是一个单独的jQuery对象会被被创建出来并且用于每一次对jQuery.single的调用（有意义的是仅有一个jQuery对象会被创建出来）。对于此的实现可以在下面看到，而且由于我们将来自多个可能的对象的数据整合到一个更加集中的单一结构中，技术上讲，它也是一个享元。

```js
jQuery.single = (function( o ){

   var collection = jQuery([1]);
   return function( element ) {

       // Give collection the element:
       collection[0] = element;

        // Return the collection:
       return collection;

   };
});
```
对于这个的带有调用链的动作的示例如下：

```js
$( "div" ).on( "click", function () {

   var html = jQuery.single( this ).next().html();
   console.log( html );

});
```
注意：尽管我们可能相信通过简单的缓存我们的jQuery代码会提供出同等良好的性能收获，但Padolsey声称`$.single()`仍然值得使用，且表现更好。那并不是说不使用任何的缓存，只要对这种方法的助益做到心里有数就行。想要对`$.single`有更加详细的了解，建议你读一读Padolsey完整的文章。

# 第10章 JavaScript MV*模式
10.1 MVC
10.2 为JavaScript开发人员提供的MVC
10.3 MVC为我们提供了什么
10.4 JavaScript中的Smalltalk-80 MVC
10.5 MVP
10.6 MVVM
10.7 利与弊
10.8 使用更松散数据绑定的MVVM
10.9 MVC、MVP与MVVM
10.10 Backbone.js与KnockoutJS
# 第11章 模块化的JavaScript设计模式
11.1 脚本加载器要点
11.2 AMD
11.3 CommonJS
11.4 AMD和CommonJS：互相竞争，标准同效
11.5 ES Harmony
11.6 总结
# 第12章 jQuery中的设计模式
12.1 Composite（组合）模式
12.2 Adapter（适配器）模式
12.3 Facade（外观）模式
12.4 Observer（观察者）模式
12.5 Iterator（迭代器）模式
12.6 延迟初始化
12.7 Proxy（代理）模式
12.8 Builder（生成器）模式
# 第13章 jQuery插件设计模式
13.1 模式
13.2 Lightweight Start模式
13.3 完整的Widget Factory模式
13.4 嵌套命名空间插件模式
13.5 自定义事件插件模式（使用Widget Factory）
13.6 使用DOM-to-Object Bridge模式的原型继承
13.7 jQuery UI Widget Factory Bridge模式
13.8 使用Widget Factory的 jQuery Mobile Widget
13.9 RequireJS和 jQuery UI Widget Factory
13.10 全局选项和单次调用可重写选项（最佳选项模式）
13.11 高可配和高可变的插件模式
13.12 是什么使插件超越模式
13.13 总结
13.14 命名空间模式
13.15 命名空间基础
13.16 高级命名空间模式
# 第14章 总结