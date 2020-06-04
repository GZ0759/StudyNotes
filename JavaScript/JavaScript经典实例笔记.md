> JavaScript经典实例（第2版）  
> JavaScript Cookbook, 2nd Ed.  
> 2015年 12 月第一次出版  
 
<!-- TOC -->

- [第1章 JavaScript不只是简单的构建块](#第1章-javascript不只是简单的构建块)
  - [1.1 JavaScript对象、基本类型和字面值之间的区别](#11-javascript对象基本类型和字面值之间的区别)
  - [1.2 从字符串提取一个列表](#12-从字符串提取一个列表)
  - [1.3 检查一个存在的、非空的字符串](#13-检查一个存在的非空的字符串)
  - [1.4 插入特殊字符](#14-插入特殊字符)
  - [1.5 使用新字符串替换模式](#15-使用新字符串替换模式)
  - [1.6 找到并突出显示一个模式的所有实例](#16-找到并突出显示一个模式的所有实例)
  - [1.7 使用捕获圆括号交换一个字符串中的单词](#17-使用捕获圆括号交换一个字符串中的单词)
  - [1.8 使用命名实体来替代html标签](#18-使用命名实体来替代html标签)
  - [1.9 把一个iso 8601格式的日期转换为date对象可接受的一种格式](#19-把一个iso-8601格式的日期转换为date对象可接受的一种格式)
  - [1.10 使用带有定时器的函数闭包](#110-使用带有定时器的函数闭包)
  - [1.11 记录消耗时间](#111-记录消耗时间)
  - [1.12 把十进制数转换为一个十六进制值](#112-把十进制数转换为一个十六进制值)
  - [1.13 把表中一列的所有数字加和](#113-把表中一列的所有数字加和)
  - [1.14 在角度和弧度之间转换](#114-在角度和弧度之间转换)
  - [1.15 找到页面元素可容纳的一个圆的半径和圆心](#115-找到页面元素可容纳的一个圆的半径和圆心)
  - [1.16 计算圆弧的长度](#116-计算圆弧的长度)
  - [1.17 使用ES6字符串新增方法而不会丢弃用户](#117-使用es6字符串新增方法而不会丢弃用户)
- [第2章 JavaScript数组](#第2章-javascript数组)
  - [2.1 在数组中搜索](#21-在数组中搜索)
  - [2.2 用concat()和apply()将一个二维数组扁平化](#22-用concat和apply将一个二维数组扁平化)
  - [2.3 删除或替换数组元素](#23-删除或替换数组元素)
  - [2.4 提取一个数组的一部分](#24-提取一个数组的一部分)
  - [2.5 对每个数组元素应用一个函数](#25-对每个数组元素应用一个函数)
  - [2.6 使用foreach()和call()遍历querySelectorAll()结果](#26-使用foreach和call遍历queryselectorall结果)
  - [2.7 对数组中的每个元素执行一个函数并放回一个新数组](#27-对数组中的每个元素执行一个函数并放回一个新数组)
  - [2.8 创建一个过滤后的数组](#28-创建一个过滤后的数组)
  - [2.9 验证数组内容](#29-验证数组内容)
  - [2.10 使用一个关联数组来存储表单元素名和值](#210-使用一个关联数组来存储表单元素名和值)
  - [2.11 使用解构赋值简化代码](#211-使用解构赋值简化代码)
- [第3章 函数：JavaScript的构建块](#第3章-函数javascript的构建块)
  - [3.1 放置函数并提升](#31-放置函数并提升)
  - [3.2 把一个函数当作参数传递给另一个函数](#32-把一个函数当作参数传递给另一个函数)
  - [3.3 实现递归算法](#33-实现递归算法)
  - [3.4 使用一个定时器和回调防止代码阻塞](#34-使用一个定时器和回调防止代码阻塞)
  - [3.5 创建能够记住其状态的函数](#35-创建能够记住其状态的函数)

<!-- /TOC -->

# 第1章 JavaScript不只是简单的构建块

## 1.1 JavaScript对象、基本类型和字面值之间的区别

People toss around terms like object, primitive, and literal. What is the difference between the three, and how can you tell which is which?  

一个JavaScript字面值表示某种特定类型的一个值。

JavaScript基本类型是特定的数据类型的一个实例。而这样的类型JavaScript有五个，分别是String、Number、Boolean、null和undefined。

在这些基本数据类型中，有3个有对应的构造方法对象：String、Number和Boolean。这些对象提供了对内建属性和方法的访问，允许我们做一些简单赋值和顺序访问之外的事情。

声明变量，可以使用一个字面值表示或者使用该对象而不带new操作符，从而创建基本类型的布尔值、字符串和数字变量。若有意实例化一个对象，使用new操作符。基本类型变量严格地等于（===）字面值，而对象实例则不会。



## 1.2 从字符串提取一个列表

You have a string with several sentences, one of which includes a list of items. The list begins with a colon (:) and ends with a period (.), and each item is separated by a comma. You want to extract just the list. 

Before: `This is a list of items: cherries, limes, oranges, apples.` 

After: `['cherries','limes','oranges','apples']`  

解决方法需要两个操作：提取出包含列表项的字符串，然后将该字符串转换为一个列表。

- 使用String的indexOf()方法来找到冒号，然后再次使用它找到冒号后面的第一个句点。通过这两个位置，利用String的substring()方法来提取字符串。
- 一旦获得了包含列表项的字符串，使用String的split()方法把该字符串分割为一个数组。

```javascript
var sentence = 'This is one sentence. This is a sentence with a list of items:' + 'cherries, oranges, apples, bananas. That was the list of items.'; 
var start = sentence.indexOf(':'); 
var end = sentence.indexOf('.', start+1); 
var listStr = sentence.substring(start+1, end);  

var fruits = listStr.split(',');
console.log(fruits); // ['cherries', ' oranges', ' apples', ' bananas']
```



还有另一个字符串提取方法substr()，但是，它是基于子字符串开始的索引位置的，传入子字符串的长度作为第二个参数。提取字符串的其它方法就是使用正则表达式和RegExp对象。

```javascript
var listStr = sentence.substr(start+1, end-start); 
var fruits = listStr.split(',');  
```



分割所提取的字符串的结果是列表项的一个数组，这些项带有由句子中的空白所产生的部分（开头的空格）。在大部分的应用程序中，我们要清理最终的数组元素。

```javascript
fruits = listStr.split(',');
console.log(fruits); // [' cherries', ' oranges', ' apples', ' bananas']
fruits.forEach(function(elmnt,indx,arry) {
arry[indx] = elmnt.trim();
});
console.log(fruits); // ['cherries', 'oranges', 'apples", "bananas"]
```



另一种简单的方法是，给split()传递一个正则表达式，该方法将修整结果然后再返回。

```javascript
var fruits = listStr.split(/\s*,\s*/);
```



## 1.3 检查一个存在的、非空的字符串

You want to verify that a variable is defined, is a string, and is not empty.  

最简单的方法。如果变量不是一个字符串或者其字符串长度不大于0，测试失败。

```javascript
if (typeof unknownVariable === 'string' && unknownVariable.length > 0)  
```



如果测试一个字符串，不管是一个String对象还是一个字符串字面值，确保该变量不为空。第一个方法测试变量是否已经定义，第二个方法测试该变量不为null，第三个方法是测试变量是否为非空字符串，第四个方法检测变量的基本类型值是否是String类型。

```javascript
if (((typeof unknownVariable != 'undefined' && unknownVariable) &&
unknownVariable.length() > 0) &&
typeof unknownVariable.valueOf() == 'string') ...
```



## 1.4 插入特殊字符

You want to insert a special character, such as a line feed, into a string.  

在字符串中使用转义序列之一。例如，要向添加到页面中的一段文本添加一个版权符号，使用转义序列 \u00A9 。JavaScript中的转义序列都以一个反斜杠开始（ \ ）。

```javascript
var resultString = "<p>This page \u00A9 Shelley Powers </p>";
// print out to page
var blk = document.getElementById("result");
blk.innerHTML = resultString;
```



## 1.5 使用新字符串替换模式

You want to replace all matched substrings with a new substring.

使用 String 对象的 replace 方法和一个正则表达式。

```javascript
var searchString = "Now is the time, this is the tame";
var re = /t\w{2}e/g;
var replacement = searchString.replace(re, "place");
console.log(replacement); // Now is the place, this is the place
```



使用内建的RegExp。与正则表达式相比，外围的斜杠不是必须的，模式中使用的反斜杠必须转义，全局指示符是一个可选参数。

```javascript
var re = new RegExp('t\\w{2}e',"g"); 
var replacement = searchString.replace(re,"place");
console.log(p);
```



正则表达式由单独使用的字符或者与特殊字符组合使用的字符构成。反斜杠（ \ ）有两个作用，和常规字符使用表明其实一个特殊字符，与特殊字符一起使用表明这个字符应该当作字面值对待。

下标是一些常用的特殊字符。

| 字符 | 匹配 | 例子 |
|---|---|---|
| ^ | 匹配输入的开头 | /^This/ 匹配 This is… |
| $ | 匹配输入的末尾 | /end$/ 匹配 This is the end |
| * | 匹配0次或多次 | /se*/ 匹配 seeee 和 se |
| ? | 匹配0次或1次 | /ap?/ 匹配 apple 和 and |
| + | 匹配1次或多次 | /ap+/ 匹配 apple 但没 and |
| {n} | 严格匹配n次 | /ap{2}/ 匹配 apple 但没 apie |
| {n,} | 匹配n次或多次 | /ap{2,}/ 匹配在 apple 和 appple 里的所有p但没 apie |
| {n,m} | 至少匹配n次，最多匹配m次 | /ap{2,4}/ 匹配在 apppppple 里的四个p |
| . | 除换行以外的任何字符 | /a.e/ 匹配 ape 和 axe |
| […] | 方括号中的任何字符 | /a[px]e/ 匹配 ape 和 axe 但没 ale |
| [^…] | 除方括号中的字符以外的任何字符 | `/a[^px]/` 匹配 ale 但没 axe 或 ape |
| \b | 匹配单词边界 | /\bno/ 匹配在 nono 里第1个no |
| \B | 匹配非单词边界 | /\Bno/ 匹配在 nono 里第2个no |
| \d | 数字0到9 | /\d{3}/ 匹配在 Now in 123 里 123 |
| \D | 匹配任何非数字字符 | /\D{2,4}/ 匹配在 Now in 123 里的 Now in |
| \w | 匹配任何单词字符（字母、数组和下划线） | /\w/ 匹配在javascript里的 j |
| \W | 匹配任何非单词字符（非字母、数组和下划线） | \/W/  匹配在 100% 里的 % |
| \n | 匹配一个换行 |  |
| \s | 一个单个的空白字符 |  |
| \S | 一个单个的非空白字符 |  |
|  | 一个制表符 |  |
| (x) | 捕获括号 | 记住匹配的字符 |


## 1.6 找到并突出显示一个模式的所有实例

You want to find all instances of a pattern within a string.  

在一个循环中，使用RegExp exec方法和全局标志（ g ），来找到一个模式的所有实例。例如：任何以t开头并且以e结尾，中间有任意多个字符的单词或其他文本。

```javascript
var searchString = "Now is the time and this is the time and that is the time";
var pattern = /t\w*e/g;
var matchArray;
var str = "";
// check for pattern with regexp exec, if not null, process
while((matchArray = pattern.exec(searchString)) != null) {
str+="at " + matchArray.index + " we found " + matchArray[0] + "\n";
}
console.log(str);
/* 
The results are:
at 7 we found the
at 11 we found time
at 28 we found the
at 32 we found time
at 49 we found the
at 53 we found time 
*/
```



RegExp exec()方法执行该正则表达式，如果没有找到一个匹配，返回null；如果找到一个匹配，返回带有匹配相关信息的一个数组。

使用全局标志（ g ），这触发了RegExp对象去保留每一次匹配的位置，并且从之前找到的匹配的之后开始搜索。当用于循环中的时候，我们可以找到模式匹配字符串的所有实例。

## 1.7 使用捕获圆括号交换一个字符串中的单词

You want to accept an input string with first and last name, and swap the names so the last name is first.  

正则表达式匹配两个单词，这两个单词用空格隔开，这两个单词都应用了捕获括号，因此，使用可以与replace一起使用的特殊字符，使用“$1”访问名字，"$2"访问姓氏。

```javascript
var name = "Abe Lincoln";
var re = /^(\w+)\s(\w+)$/;
var newname = name.replace(re,"$2, $1");
```



String.replace特殊模式

| 字符             | 替换文本                                            |
| ---------------- | --------------------------------------------------- |
| $1、$2、...、$99 | 与 regexp 中的第 1 到第 99 个子表达式相匹配的文本。 |
| $&               | 与 regexp 相匹配的子串。                            |
| $`               | 位于匹配子串左侧的文本。                            |
| $'               | 位于匹配子串右侧的文本。                            |
| $$               | 直接量符号。                                        |

## 1.8 使用命名实体来替代html标签

You want to paste example markup into a web page, and escape the markup (i.e., have the angle brackets print out rather than have the contents parsed)  

使用正则表达式把尖括号（<和>）转换为命名的实体：&lt和&gt。

```javascript
var pieceOfHtml = "<p>This is a <span>paragraph</span></p>";
pieceOfHtml = pieceOfHtml.replace(/</g,"&lt;");
pieceOfHtml = pieceOfHtml.replace(/>/g,"&gt;");
console.log(pieceOfHtml);
```



## 1.9 把一个iso 8601格式的日期转换为date对象可接受的一种格式

You need to convert an ISO 8601 formatted date string into values that can be used to create a new Date object instance.  

使用String split()方法，所有非数字字符都转换为一个特定的字符，由于ISO月份是从1开始的，要在JavaScript Date中使用月份值，月份需要通过减去1来进行调整。最后，创建了新的Date。

```javascript
var dtstr= "2014-3-04T19:35:32Z";
dtstr = dtstr.replace(/\D/g," ");
var dtcomps = dtstr.split(" ");
// modify month between 1 based ISO 8601 and zero based Date
dtcomps[1]--;
var convdt = new Date(Date.UTC.apply(null,dtcomps));
console.log(convdt.toString()); // Tue, 04 Mar 2014 19:35:32 GMT
```



## 1.10 使用带有定时器的函数闭包

You want to provide a function with a timer, but you want to add the function directly into the timer method call.  

当使用setInterval()或setTimerout()方法创建定时器的时候，可以传入一个函数变量作为其第一个参数。解决方案中使用一个匿名函数，只是和定时器一起使用，可以直接嵌入该函数。

```javascript
intervalId=setInterval(
  function() {
    x+=5;
    var left = x + "px";
  document.getElementById("redbox").style.left=left;
 },100);
```



## 1.11 记录消耗时间

You want to track the elapsed time between events.  

在第一个事件发生时，创建一个Date对象，当第二个事件发生的时候，创建一个新的Date对象，并且从第二个对象中减去第一个对象。之间的差是以毫秒表示的。

```javascript
var firstDate = new Date();
setTimeout(function() {
  doEvent(firstDate);
  }, 25000);
function doEvent() {
  var secondDate = new Date();
  var diff = secondDate - firstDate;
  console.log(diff); // approx. 25000
}
```



## 1.12 把十进制数转换为一个十六进制值

You have a decimal value, and need to find its hexadecimal equivalent.  

默认情况下，JavaScript的数字是十进制的，十六进制数字以0x开头，八进制数字总是以0开头。

```javascript
var num = 255;
// displays ff, which is hexadecimal equivalent for 255
console.log(num.toString(16));
```



## 1.13 把表中一列的所有数字加和

You want to sum all numbers in a table column.  

全局函数pareseInt()和parseFloat()都能把字符串转换为数字，后者既能用于整数，也能用于浮点数。querySelectorAll() 方法返回文档中匹配指定 CSS 选择器的所有元素，返回 NodeList 对象。NodeList 对象表示节点的集合。可以通过索引访问，索引值从 0 开始。

```javascript
var sum = 0;
// use querySelector to find all second table cells
var cells = document.querySelectorAll("td:nth-of-type(2)");
for (var i = 0; i < cells.length; i++) {
  sum+=parseFloat(cells[i].firstChild.data);
}
```



## 1.14 在角度和弧度之间转换

You have an angle in degrees. To use the value in the Math object’s trigonometric functions, you need to convert the degrees to radians.  

```javascript
// 将角度转换为弧度
var radians = degrees * (Math.PI / 180);
// 将弧度转换为角度
var degrees = radians * (180 / Math.PI);
```



## 1.15 找到页面元素可容纳的一个圆的半径和圆心

Given the width and height of a page element, you need to find the center and radius of the largest circle that fits within that page element.  

找出宽度和高度中较小的一个，然后得到该圆半径。通过给定页面元素的宽度和高度，找到圆心位置。

```javascript
var circleRadius = Math.min(elementWidth, elementHeight) / 2;
var x = elementWidth / 2;
var y = elementHeight / 2;
```



## 1.16 计算圆弧的长度

Given the radius of a circle, and the angle of an arc in degrees, find the length of the arc.  

使用Math.PI把角度转换为弧度，并在公式中使用该结果来求得圆弧的长度。圆弧的长度通过把圆的半径乘以圆弧的弧度值而求得。

```javascript
// angle of arc is 120 degrees, radius of circle is 2
var radians = degrees * (Math.PI / 180);
var arclength = radians * radius; // value is 4.18879020478...
```



## 1.17 使用ES6字符串新增方法而不会丢弃用户

You want to use new ECMAScript 6 features, such as the string extras like startsWith() and endsWith(), but you don’t want your applications to break for people using browsers that don’t support this newer functionality  

使用一个ECMAScript 6 shim 来提供对浏览器中当前还没有实现的功能的支持。另一种方案是transpiler，它把未来的代码编译到今天的环境中。

# 第2章 JavaScript数组

JavaScript 中没有数组类型。相反，通过 JavaScript 的 Array 对象来支持数组。多年来，Array 对象的支持发生了显著的变化，从简单的数组访问发展为赋予了允许搜索和排序数组的高级功能，以及使用较为高效率的技术来操作数组元素。

## 2.1 在数组中搜索

### 问题

想要在数组中搜索一个特定值，如果找到的话，获取该数组元素的索引。

You want to search an array for a specific value and get the array element index if found.  

### 解决方案

使用 ES5 Array对象方法 `indexOf()` 和 `lastIndexOf()`

```js
var animals = new Array("dog","cat","seal","elephant","walrus","lion");
console.log(animals.indexOf("elephant")); // prints 3
```

### 讨论

使用数组方法`indexOf()`和`lastIndexOf()`，两个方法都接受一个搜索值，再将数组中的每个元素比较，如果找到则返回表示该数组元素的一个索引，没有找到则返回-1，前者返回找到的第一个元素，后者返回找到的最后一个元素。两个方法都接受一个开始索引，表示在哪里开始搜索。

```javascript
var animals = new Array("dog","cat","seal","walrus","lion", "cat");
console.log(animals.indexOf("cat")); // prints 1
console.log(animals.lastIndexOf("cat")); // prints 5

console.log(animals.indexOf("cat",2)); // prints 5
console.log(animals.lastIndexOf("cat",4)); // prints 1
```

还可以使用 ES6 的`findIndex()`方法，测试每个数组值并且当测试成功的时候返回数组元素的索引。

```js
var nums = [2, 4, 19, 15, 183, 6, 7, 1, 1];
var over = nums.findIndex(function(element) {
  return (element >= 100);
});

console.log(nums[over]);
```

一个具有可比性的 ES6 数组方法是`find()`，它执行相同的过程，但是返回成功通过测试的元素的值。

这两个方法都接受一个回调函数，以及另一个可选的参数，它在函数中的作用就像this。该回调函数有3个参数，数组元素、索引和数组自身。但是，只有一个参数是必需的。这些方法都不修改原始的数组。

## 2.2 用concat()和apply()将一个二维数组扁平化

### 问题

想要将一个两维数组扁平化为一个单维数组。

You want to flatten a two-dimensional array.  

### 解决方案

使用Array对象`concat()`方法，把多维数组合并为一个单维数组。

```js
var fruitarray = [];
fruitarray[0] = ['strawberry','orange'];
fruitarray[1] = ['lime','peach','banana'];
fruitarray[2] = ['tangerine','apricot'];
fruitarray[3] = ['raspberry','kiwi'];
// flatten array
var newArray = fruitarray.concat.apply([],fruitarray);
console.log(newArray[5]); // tangerine
```

### 讨论

Array 对象 `concat()`方法接受一个或多个数组，并且将数组元素附加到用来调用该方法的父数组的内容的末尾。合并的数组作为一个新的数组返回。这种功能的用途之一是，返回由一个多维数组中的元素所组成的一个单维数组。

```js
var newArray = fruitarray[0].concat(fruitarray[1],fruitarray[2],fruitarray[3]);
```

`apply()`方法允许针对给定的一个参数的数组，应用将要调用的函数（concat）。在这个示例中，参数的数组就是最初的多维数组。为了使其能够工作，要给`apply()`传递一个空的数组作为第一个参数，因为`concat()`通过将该数组连接到一个已有的数组上面工作。

## 2.3 删除或替换数组元素

想要在数组中找到给定的值的出现，删除掉该元素或者用另一个值替换它。

You want to find occurrences of a given value in an array, and either remove the element or replace with another value. 

### 解决方案

使用Array的`indexOf()`和`splice()`方法，找到并删除/替换数组元素。 

```javascript
var animals = new Array("dog","cat","seal","walrus","lion", "cat");
// remove the element from array
animals.splice(animals.indexOf("walrus"),1); // dog,cat,seal,lion,cat
// splice in new element
animals.splice(animals.lastIndexOf("cat"),1,"monkey");
// dog,cat,seal,lion,monkey
console.log(animals.toString());
```

### 讨论

`splice()`方法可接受3个参数，第一个参数是进行拼接处的索引（必须），第二个参数是删除元素的数目（可选），第三个参数是一组替换元素（可选）。如果索引是负数，那么将从数组末尾开始拼接该元素，而不是从数组开头进行。

```js
var animals = ["cat","walrus","lion", "cat"];
// splice in new element
animals.splice(-1,1,"monkey"); // cat,walrus,lion,monkey
```

如果没有提供要拼接的元素数目，从索引到末尾的所有元素都将删除。

```js
var animals = ["cat","walrus","lion", "cat"];
// remove all elements after second
animals.splice(2); // cat,walrus
```

最后一个参数是替代值，可以是替代元素的一个集合，也可以是用逗号隔开的替代值。

```js
var animals = ["cat","walrus","lion", "cat"];
// replace second element with two
animals.splice(2,1,"zebra","elephant"); // cat,walrus,zebra,elephant,cat
```

删除或替换一个元素很方便，但是，删除或替换一个特定元素的所有实例甚至会更方便。

```js
var charSets = ["ab","bb","cd","ab","cc","ab","dd","ab"];
// replace element
while (charSets.indexOf("ab") != -1) {
charSets.splice(charSets.indexOf("ab"),1,"**");
}
// ["**", "bb", "cd", "**", "cc", "**", "dd", "**"]
console.log(charSets);

// delete new element
while(charSets.indexOf("**") != -1) {
charSets.splice(charSets.indexOf("**"),1);
}
console.log(charSets); // ["bb", "cd", "cc", "dd"]
```

## 2.4 提取一个数组的一部分

### 问题

想要从一个数组提取一部分，但是保持最初的数组的完整性。

You want to extract out a portion of an array but keep the original array intact.  

### 解决方案

使用Array对象的`slice()`方法，来提取一个已有数组的一部分的一个浅拷贝。

```javascript
var animals = ['elephant','tiger','lion','zebra','cat','dog','rabbit','goose'];
var domestic = animals.slice(4,7);
console.log(domestic); // ['cat','dog','rabbit'];
```

### 解决方案

`slice()`方法复制一个已有的数组的一部分，返回一个新的数组。它执行浅拷贝，这意味着，如果数组元素时对象，两个数组都指向相同的对象。对新数组中的对象进行修改，会在旧的数组的相同的对象中反应出来。

```js
var mArray = [];
mArray[0] = ['apple','pear'];
mArray[1] = ['strawberry','lemon'];
mArray[2] = ['lime','peach','berry'];
var nArray = mArray.slice(1,2);
console.log(mArray[1]); // ['strawberry','lemon']
nArray[0][0] = 'raspberry';
console.log(nArray[0]); // ['raspberry','lemon']
console.log(mArray[1]); // ['raspberry','lemon']
```

值是按照引用来复制的。如果数组元素是一个基本数据类型，例如字符串或者数字，它们将按照值来复制，也就是说，对新的数组的修改，不会再旧的数组中反映出来。

## 2.5 对每个数组元素应用一个函数

### 问题

想要使用一个函数来检查一个数组值，如果满足给定的条件，就替换它。

You want to use a function to check an array value, and replace it if it matches a given criterion.  

### 解决方案

使用Array的`forEach()`方法，来针对每个数组元素应用一个回调函数。

```javascript
var charSets = ["ab","bb","cd","ab","cc","ab","dd","ab"];
function replaceElement(element,index,array) {
  if (element == "ab") array[index] = "**";
}
// apply function to each array element
charSets.forEach(replaceElement);
console.log(charSets); // ["**", "bb", "cd", "**", "cc", "**", "dd", "**"]
```

### 讨论

`forEach()`方法接受一个参数，即回调函数。该函数自身有3个参数：数组元素、元素的索引和数组。所以这3个参数都用于该函数中，但是，只有第一个参数是必需的。

警告：不要从传递给`forEach()`的函数中返回一个值，因为该值将会被丢弃。

### 参见

如果想要修改数组的一个副本，而不是替换最初的数组，使用`map()`方法。

### 额外知识：关于条件语句

关于条件语句。在单个一行中使用条件语句，可以不用使用花括号。同时可以更加晦涩一些，虽然这种方法比传统的 if 语句可读性要差一点。

```js
// if (element == "ab") array[index] = "**";
// 等价于
(element == "ab") && (array[index] = "**");
```

## 2.6 使用foreach()和call()遍历querySelectorAll()结果

### 问题

想要对调用`querySelectorAll()`所返回的一个 nodeList，使用`forEach()`。

You want to use forEach() on the nodeList returned from a call to querySelector All().  

### 解决方案

可以将`forEach()`强制地和一个 NodeList 一起使用。

```javascript
// use querySelector to find all second table cells
var cells = document.querySelectorAll("td + td");
[].forEach.call(cells,function(cell) {
  sum += parseFloat(cell.firstChild.data);
});
```

### 讨论

`forEach()`是一个 Array 方法，而 `querySelectorAll()`的结果是一个 NodeList，这是和 Array 不同类型的一种对象。为了让`forEach()`和 NodeList 一起使用，可以在一个空的数组上调用该方法，然后在该对象上使用`call()`，从而在 NodeList 上模拟了一个 Array 的效果。

这种方法简单，但是有缺点。这种强制的方式是一次性的，如果需要再次使用相同的功能的话，必须再次重复它。

## 2.7 对数组中的每个元素执行一个函数并放回一个新数组

### 问题

想要把一个十进制数的数组转换为一个新的数组，其中都是它们等价的十六进制数形式。

You want to convert an array of decimal numbers into a new array with their hexadecimal equivalents.  

### 解决方案

使用Array对象的`map()`方法来创建一个新的数组，该数组中包含了通过传递给map方法的回调函数修改原数组后得到的元素。

```javascript
var decArray = [23, 255, 122, 5, 16, 99];
var hexArray = decArray.map(function(element) {
  return element.toString(16);
});
console.log(hexArray); // ["17", "ff", "7a", "5", "10", "63"]
```

### 讨论

和`forEach()`方法一样，`map()`方法也对每一个数组元素应用一个回调函数，但是`map()`方法的结果是一个新的数组，而不是修改最初的数组。因此，使用`forEach()`的时候不会返回一个值，但是使用`map()`的时候必须返回一个值。

## 2.8 创建一个过滤后的数组

### 问题

想要过滤一个数组中的元素的值，并且把结果赋给一个新的数组。

You want to filter element values in an array and assign the results to a new array.  

### 解决方案

使用Array对象的`filter()`方法。

```javascript
var charSet = ["**","bb","cd","**","cc","**","dd","**"];
var newArray = charSet.filter(function(element) {
  return (element !== "**");
});
console.log(newArray); // ["bb", "cd", "cc", "dd"]
```

### 讨论

`filter()`方法将一个回调函数应用于每一个数组元素，作为参数传递给`filter()`方法的函数返回一个布尔值，它根据测试数组元素的结果来返回。这个返回值决定了该数组元素是否添加到一个新的数组中，如果返回true，将会添加；否则将不会添加。

## 2.9 验证数组内容

### 问题

想要确保数组内容满足某个条件。

You want to ensure that array contents meet certain criteria.  

### 解决方案

使用Array `every()`方法来检查每个元素复合给定的条件，例如下面的代码确保数组的每个元素都由字母字符组成。

```javascript
// testing function
function testValue (element,index,array) {
  var textExp = /^[a-zA-Z]+$/;
  return textExp.test(element);
}
var elemSet = ["**",123,"aaa","abc","-",46,"AAA"];
// run test
var result = elemSet.every(testValue);
console.log(result); // false
var elemSet2 = ["elephant","lion","cat","dog"];
result = elemSet2.every(testValue);
console.log(result); // true
```

或者使用Array `some()`方法来确保至少某些元素符合该条件。

```javascript
var elemSet = new Array["**",123,"aaa","abc","-",46,"AAA"];

function testValue (element) {
  var textExp = /^[a-zA-Z]+$/;
  return textExp.test(element);
}

var result = elemSet.some(testValue);
console.log(result); // true
```

### 讨论

`every()`函数和`some()`函数不会对所有的数组元素执行，它们只是处理满足自己功能性所必需的那么多的数组元素。

使用`every()`方法时，如果该函数返回一个false值，处理就会结束，并且该方法也返回false，而`some()`方法将继续测试每个数组元素，直到回调函数返回true，此时不再验证其他元素，该方法也返回true。

### 额外知识：在数组方法中使用匿名函数

使用命名函数的好处是，当调试代码的时候，它会出现在栈追踪中，而匿名函数则不会这样。当要处理简单的、目标明确的功能的时候，这不是一个问题。

命名函数的另一个优点是，可以在多个地方使用她。再一次，将以一个特定 Array 方法回调函数为目标的函数进行复用。如果是由于具体回调函数之外的任何其他原因的话，这么做是没有什么意义的。使用命名函数的时候，缺点会把全局空间搞得很乱。

使用命名函数的最后一个可能得优点是，在所有的浏览器中，它在 Array 方法回调环境中比匿名函数要执行得更好。

## 2.10 使用一个关联数组来存储表单元素名和值

### 问题

想要存储表单元素的名称和值，以便随后用于验证。

You want to store form element names and values for later validation purposes.  

### 解决方案

使用关联数组来存储元素，使用元素标识符作为数组索引。

```javascript
var elemArray = new Object(); // notice Object, not Array
var elem = document.forms[0].elements[0];
elemArray[elem.id] = elem.value;
```

将`keys()`和`forEach()`组合起来，遍历该数组。

```js
Object.keys(elemArray).forEach(function (key) {
  var value = elemArray[key];
  console.log(value);
});
```

### 讨论

大多数 javascript 数组使用数字索引，如`arr[0] = value;`。然而，可以使用 javascript 创建一个关联数组，其中，数组索引可以是表示关键字的一个字符串，把该字符串映射到一个给定的值。在解决方案中，数组索引是给定的数组元素的标识符，而实际的数组值是表单元素的值。

可以创建一个关联数组，但是，不能使用 Array 对象来做到这一点。使用 Array 对象有风险并且令人沮丧，特别是如果要使用某个采用了 prototype 属性的内建库来扩展对象。

## 2.11 使用解构赋值简化代码

### 问题

想要将数组元素的支赋给几个变量，但是确实不像单独地赋每一个值。

You want to assign array element values to several variables, but you really don’t want to have assign each, individually.  

### 解决方案

使用ES 6的解构赋值来简化数组赋值。

```javascript
var stateValues = [459, 144, 96, 34, 0, 14];
var [Arizona, Missouri, Idaho, Nebraska, Texas, Minnesota] = stateValues;
console.log(Missouri); // 144
```

### 讨论

在解决方案中，声明了变量并且用一个数组中的值来实例化它们，从位置为0的数组索引开始。如果变量的数目少于数组元素的数目，元素值会赋给它们，直到所有的变量都已经复制。如果变量数目比数组元素数目多，未匹配的变量也会创建，但是将它们设置为 undefined。

Google开发的Traceur是接受ES6代码并将其解释编译的一款应用。

# 第3章 函数：JavaScript的构建块

javascript 函数提供了一种方法把一段代码封装起来，以便能够多次复用代码。函数是 javascript 中的第一等对象，这意味着可以把它们当做一个对象及一个表达式或语句一样地对待。

有3种基本的方式可以创建函数：声明式函数、匿名函数或函数构造函数、函数字面值或函数表达式。

- 声明式函数：通过使用 function 关键字触发的一条语句，并且当 JavaScript 应用程序初次载入的时候解析。

- 匿名函数或函数构造函数：匿名函数是使用new运算符构造的，并且引用Function对象。和声明式函数不同，每次访问匿名函数的时候解析它。

- 函数字面值或函数表达式：字面值函数是一个函数表达式，包括参数和函数体，用于在另一个函数的参数中作为回调函数。


## 3.1 放置函数并提升

You’re not sure where to place your function to ensure it’s accessible when needed.  

如果要使用一个声明式的函数，可以将其放置在代码中的任何位置。如果要使用函数表达式，必须将其放置在使用函数的位置之前。

在JavaScript中，所有的变量声明都会移动或提升到当前作用域的顶部。

## 3.2 把一个函数当作参数传递给另一个函数

You want to pass a function as an argument to another function.  

function关键字是一个运算符，也是一条语句，它也可以用来创建作为表达式的一个函数，以这种方式创建的函数称为函数表达式、函数字面值和匿名函数。

```javascript
function otherFunction(x,y,z) {
  x(y,z);
}
var param = function(arg1, arg2) { alert(arg1 + " " + arg2); };
otherFunction(param, "Hello", "World");
// or
otherFunction(function(arg1,arg2) {
alert(arg1 + ' ' + arg2); }, "Hello","World");
```



一个函数接受另一个函数作为参数，或者返回一个函数，或者两个都具备，这称为一个高阶函数。这个概念来自于一种称为函数式编程的编程范围。函数式编程的真正好处是，代码更具有可读性。

## 3.3 实现递归算法

You want to implement a function that will recursively traverse an array and return a string of the array element values, in reverse order.  

递归地使用一个函数字面值，直到达到最终目标。递归符合函数式编程规范，这意味着代码会更具有可读性和一致性，但是递归函数很消耗内存。

```javascript
var reverseArray = function(x,indx,str) {
  return indx == 0 ? str :
    reverseArray(x,--indx,(str+= " " + x[indx]));
}
var arr = ['apple','orange','peach','lime'];
var str = reverseArray(arr,arr.length,"");
console.log(str);
var arr2 = ['car','boat','sun','computer'];
str = reverseArray(arr2,arr2.length,"");
console.log(str);
```



ES 6提出了一项尾调用优化的新JavaScript功能。适当的尾调用优化所做的事情，就是复用相同帧而不是添加一个新的帧。

## 3.4 使用一个定时器和回调防止代码阻塞

You have a piece of code that can be time consuming, and you don’t want to block the rest of the code from processing while waiting for it to finish. But you do need to perform some functionality when the time-consuming function is finished.  

将一个回调函数和setTimeout()结合起来使用，定时器设置为0。调用factorial()两次，一次使用值3，一次使用值4，每次迭代都将参数的值打印到控制台。在noBlock()中，使用一个setTimeout()来调用factorial()，传递给其第一个参数，如果可选的第二个参数是一个函数的话，调用该函数。

```javascript
function factorial(n) {
  console.log(n); // 输出的第四段 3 2 1 
  return n == 1 ? 1 : n * factorial(n -1);
}
function noBlock(n, callback) {
  setTimeout(function() {
    var val = factorial(n);
    if (callback && typeof callback == 'function') {
      callback(val);
    }
  },0);
}
console.log("Top of the morning to you"); // 输出的第一段
noBlock(3, function(n) {
  console.log('first call ends with ' + n); // 输出的第四段
  noBlock(n, function(m) {
    console.log("final result is " + m); // 输出的第六段
  });
});
var tst = 0;
for (i = 0; i < 10; i++) {
  tst+=i;
}
console.log("value of tst is " + tst); // 输出的第二段
noBlock(4, function(n) {
  console.log("end result is " + n); // 输出的第五段
});
console.log("not doing too much"); // 输出的第三段
```



不考虑底层系统或应用的话，JavaScript不是多线程的，所有的进程都是在单个的线程上执行。当JavaScript定时器事件发生的时候，就像JavaScript中任何其他的异步事件一样，它添加到了事件队列的末尾，而不是立即挤入到队列之中。

## 3.5 创建能够记住其状态的函数

You want to create a function that can remember data, but without having to use global variables and without resending the same data with each function call.  

创建一个外围函数，它接受一个或多个参数，然后创建一个内部函数，它也接受一个或多个参数，内部使用自己的参数以及其原函数的参数。从外围函数返回内部函数，并且将其赋值给一个变量。从这一刻起，该变量就被当作一个函数使用。

```javascript
function greetingMaker(greeting) {
   function addName(name) {
      return greeting + " " + name;
   }
   return addName;
}

// Now, create new partial functions
var daytimeGreeting = greetingMaker("Good Day to you");
var nightGreeting = greetingMaker("Good Evening");

var name = 'Reader';

// if daytime
console.log(daytimeGreeting(name));

// if night
console.log(nightGreeting(name));
```



3.6 把函数参数转换到一个数组中

You want to use Array functionality on a function’s arguments, but the arguments object isn’t an array.  

使用Array.prototype.slice()，然后是函数call()方法，将arguments集合转换到一个数组中。

```javascript
function someFunc() {
  var args = Array.prototype.slice.call(arguments);
}
// 另一种方法
function someFunc() {
  var args = [].slice.call(arguments);
}
```



slice()方法返回了对数组的一部分的一个浅拷贝，如果没有给定起始值或结束值的话，就是整个数组的浅拷贝。slice()方法也是一个函数，这意味着诸如call()这样的函数式方法可以与其一起使用。call()方法的第一个参数是this值，通常是调用对象本身，后面跟着任意数目的参数。

3.7 使用一个局部已改用减少冗余性



3.8 使用缓存计算来提高应用程序性能



3.9 使用匿名函数包装全局变量



3.10 提供一个默认的参数

# 第4章 可扩展JavaScript对象
## 4.1 保持对象成员私有
## 4.2 用原型扩展对象
## 4.3 继承一个对象的功能
## 4.4 通过定义一个新的属性来扩展对象
## 4.5 阻止对象可扩展性
## 4.6 阻止对对象的任何修改
## 4.7 为你的javascript对象提供命名空间
## 4.8 用prototype.bind再次发现"this"
## 4.9 将对象方法链化

# 第5章 JavaScript和直接访问用户界面
# 第6章 基本测试和可访问性
# 第7章 创建和使用JavaScript库
# 第8章 简化的客户端-服务器通信和数据
# 第9章 创建富媒体和交互Web效果

# 第二部分 JavaScript全面兴起
# 第10章 新的ECMAScript标准对象
# 第11章 Node：服务器上的JavaScript
# 第12章 模块化和管理JavaScript
# 第13章 API的乐趣
# 第14章 JavaScript框架
# 第15章 高级客户端-服务器通信和流
# 第16章 数据可视化和客户端/服务器图形
# 第17章 数据和持久性
# 第18章 JavaScript迈上移动之路
# 附录A 认识jsBin和jsFiddle