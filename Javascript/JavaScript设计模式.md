> JavaScript 设计模式  
> 张容铭著  
> 2015 年 8 月第一版  

# 第一篇 面向对象编程

面向对象编程（Object-oriented programming, OOP）是一种程序设计范型。它将对象作为程序的基本单元，将程序和数据封装其中，以提高程序的重用性、灵活性和扩展性。

## 第1章 灵活的语言——JavaScript

用对象收编变量。但是这个对象不能复制一份，或者说这个对象类在用 new 关键字创建新的对象时，新创建的对象时不能继承这些方法的。

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

真假对象。如果想要简单地复制一下对象，可以将这些方法放在一个函数对象中。

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

类也可以。虽然创建了新对象完成了需求，但是它不是一个真正意义上类的创建方式，创建的对象与对象 CheckObject 没有任何关系。如下，把所有的方法放在函数内部，通过 this 定义，每一次通过 new 关键字创建新对象的时候，新创建的对象都会对类的 this 上的属性进行复制，所以这些新创建的对象都会有自己的一套方法。

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

一个检测类。但是有时候这么做造成的消耗是很奢侈的，需要处理一下。如下，创建出来的对象所拥有的方法就都是一个，因为它们都要依赖 prototype 原型依次寻找，而找到的方法都是同一个，它们都绑定在 CheckObject 对象类的原型上。

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

var c = new CheckObjectFive();
c.checkName();
c.checkEmail();
c.checkPassword();
```

方法还可以这样用。使用该类多次调用了对象，这是可以避免的。可以在声明的每一个方法的末尾处将当前对象返回，在JavaScript 中 this 指向的就是当前对象。

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


## 第2章 写的都是看到的——面向对象编程

# 第二篇 创建型设计模式

# 第三篇 结构性设计模式

# 第四篇 行为型设计模式

# 第五篇 技巧性设计模式

# 第六篇 架构型设计模式

# 附录 A
