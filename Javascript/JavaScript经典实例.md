> JavaScript经典实例（第2版）
> JavaScript Cookbook, 2nd Ed.
> 2015年 12 月第一次出版

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

| 字符  | 匹配                                       | 例子                                               |
| ----- | ------------------------------------------ | -------------------------------------------------- |
| ^     | 匹配输入的开头                             | /^This/ 匹配 This is…                              |
| $     | 匹配输入的末尾                             | /end$/ 匹配 This is the end                        |
| *     | 匹配0次或多次                              | /se*/ 匹配 seeee 和 se                             |
| ?     | 匹配0次或1次                               | /ap?/ 匹配 apple 和 and                            |
| +     | 匹配1次或多次                              | /ap+/ 匹配 apple 但没 and                          |
| {n}   | 严格匹配n次                                | /ap{2}/ 匹配 apple 但没 apie                       |
| {n,}  | 匹配n次或多次                              | /ap{2,}/ 匹配在 apple 和 appple 里的所有p但没 apie |
| {n,m} | 至少匹配n次，最多匹配m次                   | /ap{2,4}/ 匹配在 apppppple 里的四个p               |
| .     | 除换行以外的任何字符                       | /a.e/ 匹配 ape 和 axe                              |
| […]   | 方括号中的任何字符                         | /a[px]e/ 匹配 ape 和 axe 但没 ale                  |
| [^…]  | 除方括号中的字符以外的任何字符             | `/a[^px]/` 匹配 ale 但没 axe 或 ape                |
| \b    | 匹配单词边界                               | /\bno/ 匹配在 nono 里第1个no                       |
| \B    | 匹配非单词边界                             | /\Bno/ 匹配在 nono 里第2个no                       |
| \d    | 数字0到9                                   | /\d{3}/ 匹配在 Now in 123 里 123                   |
| \D    | 匹配任何非数字字符                         | /\D{2,4}/ 匹配在 Now in 123 里的 Now in            |
| \w    | 匹配任何单词字符（字母、数组和下划线）     | /\w/ 匹配在javascript里的 j                        |
| \W    | 匹配任何非单词字符（非字母、数组和下划线） | \/W/  匹配在 100% 里的 %                           |
| \n    | 匹配一个换行                               |                                                    |
| \s    | 一个单个的空白字符                         |                                                    |
| \S    | 一个单个的非空白字符                       |                                                    |
| \t    | 一个制表符                                 |                                                    |
| (x)   | 捕获括号                                   | 记住匹配的字符                                     |



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

## 2.1 在数组中搜索

You want to search an array for a specific value and get the array element index if found.  

使用数组方法indexOf()和lastIndexOf()，两个方法都接受一个搜索值，再将数组中的每个元素比较，如果找到则返回表示该数组元素的一个索引，没有找到则返回-1，前者返回找到的第一个元素，后者返回找到的最后一个元素。两个方法都接受一个开始索引，表示在哪里开始搜索。

```javascript

```



findIndex()方法，测试每个数组值并且当测试成功的时候返回数组元素的索引，find()方法则是返回通过测试的元素的值，这两个方法都接受一个回调函数，以及另一个可选的参数，它在函数中的作用就像this。

## 2.2 用concat()和apply()将一个二维数组扁平化

You want to flatten a two-dimensional array.  

使用Array对象concat()方法，把多维数组合并为一个单维数组。apply()方法传递一个空的数组作为第一个参数，因为concat()通过该数组连接到一个已有的数组上面工作。

```javascript
var fruitarray = [];
fruitarray[0] = ['strawberry','orange'];
fruitarray[1] = ['lime','peach','banana'];
fruitarray[2] = ['tangerine','apricot'];
fruitarray[3] = ['raspberry','kiwi'];
// flatten array
var newArray = fruitarray.concat.apply([],fruitarray);
console.log(newArray[5]); // tangerine
```



## 2.3 删除或替换数组元素

You want to find occurrences of a given value in an array, and either remove the element or replace with another value. 

使用Array的indexOf()和splice()方法，找到并删除/替换数组元素。 

```javascript
var animals = new Array("dog","cat","seal","walrus","lion", "cat");
// remove the element from array
animals.splice(animals.indexOf("walrus"),1); // dog,cat,seal,lion,cat
// splice in new element
animals.splice(animals.lastIndexOf("cat"),1,"monkey");
// dog,cat,seal,lion,monkey
console.log(animals.toString());
```



splice()方法可接受3个参数，第一个参数是进行拼接处的索引，第二个参数是删除元素的数目，第三个参数是替换元素。如果索引是负数，那么将从数组末尾开始拼接该元素。

## 2.4 提取一个数组的一部分

You want to extract out a portion of an array but keep the original array intact.  

使用Array对象的slice()方法，来提取一个已有数组的一部分的一个浅拷贝。

```javascript
var animals = ['elephant','tiger','lion','zebra','cat','dog','rabbit','goose'];
var domestic = animals.slice(4,7);
console.log(domestic); // ['cat','dog','rabbit'];
```



## 2.5 对每个数组元素应用一个函数

You want to use a function to check an array value, and replace it if it matches a given criterion.  

使用Array的forEach()方法，来针对每个数组元素应用一个回调函数。

```javascript
var charSets = ["ab","bb","cd","ab","cc","ab","dd","ab"];
function replaceElement(element,index,array) {
if (element == "ab") array[index] = "**";
}
// apply function to each array element
charSets.forEach(replaceElement);
console.log(charSets); // ["**", "bb", "cd", "**", "cc", "**", "dd", "**"]
```



forEach()方法接受一个参数，即回调函数，该函数有三个参数：数组元素、元素的索引和数组。同时可以使用以下语句代替上面的条件语句：`(element == "ab") && (array[index] = "**");`  

## 2.6 使用foreach()和call()遍历querySelectorAll()结果

You want to use forEach() on the nodeList returned from a call to querySelector All().  

为了让forEach()和NodeList一起使用，我们在一个空的数组上调用该方法，然后再该对象上使用call()，从而在NodeLists上模拟了一个Array效果。

```javascript
// use querySelector to find all second table cells
var cells = document.querySelectorAll("td + td");
[].forEach.call(cells,function(cell) {
sum+=parseFloat(cell.firstChild.data);
});
```



## 2.7 对数组中的每个元素执行一个函数并放回一个新数组

You want to convert an array of decimal numbers into a new array with their hexadecimal equivalents.  

使用Array对象的map()方法来创建一个新的数组，该数组中包含了通过传递给map方法的回调函数修改原数组后得到的元素。

```javascript
var decArray = [23, 255, 122, 5, 16, 99];
var hexArray = decArray.map(function(element) {
  return element.toString(16);
});
console.log(hexArray); // ["17", "ff", "7a", "5", "10", "63"]
```



和forEach()方法一样，map()方法也对每一个数组元素应用一个回调函数，但是map()方法的结果是一个新的数组，而不是修改最初的数组。因此，使用forEach()的时候不会返回一个值，但是使用map()的时候必须返回一个值。

## 2.8 创建一个过滤后的数组

You want to filter element values in an array and assign the results to a new array.  

使用Array对象的filter()方法，将一个回调函数应用于每一个数组元素，作为参数传递给filter()方法的函数返回一个布尔值，它根据测试数组元素的结果来返回，这个返回值决定了该数组元素是否添加到一个新的数组中，如果返回true，将会添加；否则将不会添加。

```javascript
var charSet = ["**","bb","cd","**","cc","**","dd","**"];
var newArray = charSet.filter(function(element) {
  return (element !== "**");
});
console.log(newArray); // ["bb", "cd", "cc", "dd"]
```



## 2.9 验证数组内容

You want to ensure that array contents meet certain criteria.  

使用Array every()方法来检查每个元素复合给定的条件，例如下面的代码确保数组的每个元素都由字母字符组成。

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



或者使用Array some()方法来确保至少某些元素符合该条件。every()函数和some()函数不会对所有的数组元素执行，它们只是处理满足自己功能性所必需的那么多的数组元素。使用第一个方法时，如果该函数返回一个false值，处理就会结束，并且该方法也返回false，而第二个方法将继续测试每个数组元素，直到回调函数返回true，此时不再验证其他元素，该方法也返回true。

## 2.10 使用一个关联数组来存储表单元素名和值

You want to store form element names and values for later validation purposes.  

使用关联数组来存储元素，使用元素标识符作为数组索引。不要使用Array对象来创建关联数组，直接使用JavaScript Object即可。keys()对象返回了对象的可枚举属性的一个数组，并且forEach()遍历该数组。

```javascript
var elemArray = new Object(); // notice Object, not Array
var elem = document.forms[0].elements[0];
elemArray[elem.id] = elem.value;

Object.keys(elemArray).forEach(function (key) {
  var value = elemArray[key];
  console.log(value);
});
```



dict模式，创建拥有一个空的原型的对象，以避免已有的属性可能会搞乱应用程序，而不是创建一个标准的对象。

## 2.11 使用解构赋值简化代码

You want to assign array element values to several variables, but you really don’t want to have assign each, individually.  

使用ES 6的解构赋值来简化数组赋值，生命了变量并且用一个数组中的值来实例化它们，从位置为0的数组索引开始。

```javascript
var stateValues = [459, 144, 96, 34, 0, 14];
var [Arizona, Missouri, Idaho, Nebraska, Texas, Minnesota] = stateValues;
console.log(Missouri); // 144
```



Google开发的Traceur是接受ES6代码并将其解释编译的一款应用。

# 第3章 函数：JavaScript的构建块

有3种基本的方式可以创建函数：声明式函数、匿名函数或函数构造函数、函数字面值或函数表达式。

> 声明式函数是通过使用function关键字触发的一条语句，并且当JavaScript应用程序初次载入的时候解析。
>
> 匿名函数是使用new运算符构造的，并且引用Function对象。和声明式函数不同，每次访问匿名函数的时候解析它。
>
> 字面值函数是一个函数表达式，包括参数和函数体，用于在另一个函数的参数中作为回调函数。

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