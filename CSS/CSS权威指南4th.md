> CSS权威指南第四版  
> CSS:The Definitive Guide(4th Edition)  
> 2019年4月第一版  
> Revision History for the Fourth Edition
> 2000-05-01: First Release  
> 2004-03-01: Second Release  
> 2006-11-01: Third Release  
> 2017-10-10: Fourth Release   
> [作者博客](https://meyerweb.com/eric/books/css-tdg/)  
> [线上资源](https://github.com/gdut-yy/CSS-The-Definitive-Guide-4th-zh)

# 上册

# 第 1 章 CSS 和文档

层叠样式表（Cascading Style Sheets, CSS）是一个强大的工具，能影响一个或一组文档的表现，CSS 几乎触及 Web 的每个角落，甚至很多非 Web 环境也能见到它的身影。

## 1.1 Web 样式简介

CSS 最初是在 1994 年提出的，当时 web 刚刚开始流行。当时，浏览器为用户提供了各种样式的定制功能。例如，用户在 Mosaic 的表现偏好设置中可以为单个元素设置字体族、字号和颜色。而文档编写人员却做不到这一点。文档编写人员只能把内容标记成一个个段落、一级级标题、一块块预排格式文本，或者一些其他类型的元素。

CSS 就是在这样的背景下诞生的。它的目标是提供一个简单的声明式样式语言，而且具有一定的灵活性。能为文档编写和用户提供等同的样式化功能。层叠样式中的“层叠”是指样式可以结合起来使用，而且具有优先级，文档编写人员和用户都有话语权，不过最终的决策权在用户手中。

单独来看，CSS 的每一部分都很简单，但把各部分放在一起就变得异常复杂，而且早期实现有些先天不足，例如不同浏览器对盒模型（box model）的实现之间有差异尤其为人诟病。

1998年年初CSS2定案。随后CSS工作组开始制定CSS3，以及CSS2的修订工作（制定CSS2.1）。与以往不同的是，CSS3有多个（理论上的）独立的模块构成，而不是单独一个臃肿的规范。

CSS3分成多个模块的根本原因是各模块可以独立演进，尤其是重要的（或是受众广的）模块可以按照W3C的规划向前推进，而不必受其他模块拖累。

但是这样做也有缺点，那就是CSS规范不能涵盖一切。所以我们没有办法指着某些文件说：这就是CSS3，而是应该分模块学习不同的特性。模块的灵活性有时可以弥补由此引起的语义不足。

如果要看单独的完整规范，可以留意CSS工作组每年发布的[Snapshot 文档](https://www.w3.org/Style/CSS/)。

## 1.2 元素

元素（element）是文档结构的根基。在 HTML 中，最常见的元素有 `p`, `table`, `span`, `a`, 和 `div`等。文档中的每个元素都对文档的表现起一定作用。

### 1.2.1 置换元素和非置换元素

虽然 CSS 依赖于元素，但并不是所有的元素都以同样的方式创建的。例如，图像和段落不是同一类型的元素，`span` 和 `div` 也不是。在 CSS 中，元素通常有两种形式:置换元素和非置换。

**置换元素**

置换元素（replaced element）指用来置换元素内容纳部分不由文档内容直接表示。在 HTML 中，最常见的置换元素要数 img ，它的内容由文档之外的图像文件替换。其实，通过下面这个简单的例子可以看出， img 元素没有内容。

```html
<img src="howdy.gif" />
```

如果指向的图像文件存在，文档会把那个图像显示出来，否则，浏览器什么也不显示，或者显示“图像损坏”占位图。

input 元素类似，根据类型的不同，会替换成单选按钮、复选框或文本输入框。

**非置换元素**

HTML 元素大部分是非置换元素（nonreplaced element），即元素的内容由用户代理（通常为浏览器）在元素自身生成的框中显示。例如，`<span>hi there</span>`是非置换元素，用户代理会显示“hi there”文本。段落、标题、单元格、列表，以及 HTML 中其他几乎所有元素都是非置换元素。

### 1.2.2 元素的显示方式

除了置换元素和非置换元素，CSS还把元素分为块级和行内两种基本类型。（这两种最常见，除此之外还有其他的显示类型）。

**块级元素**

块级元素默认生成一个填满父级元素内容区域的框，旁边不能有其他元素。也就是说，块级元素在元素框前后都有断行。 HTML 中最常见的块级元素有p和div。置换元素可以是块级元素，但往往不是。

列表项目是一种特殊的块级元素，它会在元素框旁边生成一个记号（无序列表通常是圆点，有序列表通常是数字），除此之外列表项目和其他块级元素并没有什么不同。

**行内元素**

行内元素在一行文本内生成元素框，不打断所在的行。最常见的行内元素是a，此外还有 strong 和 em 。这类元素不在自身所在的元素框前后“断行”，因此可以出现在另一个元素的内容中，且不影响所在的元素。

注意，HTML中的块级元素和行内元素虽然有诸多共同点，但是它们之间有个重要的区别：在 HTML 中，块级元素不能出现在行内元素中。但是CSS并不限制它们的显示方式，相互之间可以嵌套。

```html
<body>
  <p>This is a paragraph with <em>an inline element</em> within it.</p>
</body>
```

这里有两个块级元素（ body 和 p ）及一个行内元素（ em ）。根据 HTML 规范， em 可以放在 p 里，而反过来却不行。一般地， HTML 层次结构要求，行内元素可以放在块级元素中，反之则不行。

与此不同， CSS 没有这种限制。在不改变标记的前提下，可以像下面一样改变它们的显示方式。

```css
p {
  display: inline;
}
em {
  display: block;
}
```

这会导致行内框中出现一个块级框。这完全是有效的，不违背任何 CSS 规则。然而，如果在 HTML 中调换元素之间的嵌套关系，就会出现问题。

改变元素的显示方式对 HTML 文档来说是有用的，不过对 XML 文档而言的作用更大。 XML 文档的元素没有固定的显示方式，而是完全由编写人员定义。

```xml
<book>
  <maintitle>Cascading Style Sheets: The Definitive Guide</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>November 2006</pubdate>
  <isbn type="print">978-0-596-52733-4</isbn>
</book>
<book>
  <maintitle>CSS Pocket Reference</maintitle>
  <subtitle>Third Edition</subtitle>
  <author>Eric A. Meyer</author>
  <publisher>O'Reilly and Associates</publisher>
  <pubdate>October 2007</pubdate>
  <isbn type="print">978-0-596-51505-8</isbn>
</book>
```

上述内容默认将显示为行内文本，这样显示没有什么用。因此，可以用 display 定义基本布局，还可以在上述规则的基础上再添加一些样式，得到更好的视觉效果。

```css
book,
maintitle,
subtitle,
author,
isbn {
  display: block;
}
publisher,
pubdate {
  display: inline;
}
```

## 1.3 把CSS应用到HTML上

HTML 文档内部有一定的结构。这种结构正式 HTML 与 CSS 之间固有关系的一部分，如若不然，二者之间便是泾渭分明。

### 1.3.1 link标签

link 标签的基本作用是把其他文档与当前文档关联起来。 CSS 通过它链接应用到文档上的样式表。通过 link 链接的样式表不是HTML文档的一部分，但却供文档使用。我们称这样的样式表为外部样式表（external stylesheet）。

```html
<link rel="stylesheet" type="text/css" href="sheet.css" media="all">
```

为了正确的加载样式表， link 标签必须放在 head 元素中，不能放在其他元素中。

**属性**

- rel是relation（关系）的简称，这里指定的是stylesheet。
- type属性的值为text/css，说明通过link标签加载的数据类型。
- href的值是样式表的URL。可以是绝对地址，或者相对地址。
- media属性，它的值是一个或多个媒体描述符（media descriptor），指明媒体的类型和具有的功能。多个媒体描述符以逗号分号。

```html
<link rel="stylesheet" type="text/css" href="visual-sheet.css" 
media="screen, projection">
```

**候选样式表**

候选样式表（alternate stylesheet）的定义方式是把 rel 属性的值设为alternate stylesheet。仅当用户自己选择，文档才会使用候选样式表渲染。

如果浏览器支持候选样式表，会使用link元素title属性的值生成候选样式表列表。

```html
<link rel="stylesheet" type="text/css" href="sheet1.css" title="Default">
<link rel="alternate stylesheet" type="text/css" href="bigtext.css" title="Big Text">
<link rel="alternate stylesheet" type="text/css" href="zany.css" title="Crazy colors!">
```

浏览器默认使用第一个样式表（这里是名为Default的样式表）。此外用户还可以自己选择想使用的样式表（实际上这就是CSS开始崭露头角之时的方式）。此外，还可以为不同的候选样式表设定相同的 title 值，把它们分组放在一起。利用这一点，用户可以为屏幕和印刷媒体选择不同的外观。

下面三个 link 元素声明的都是首选样式表，因为都设定了 title 属性，但是文档只会使用其中一个，另外两个则完全被忽略，并且因为 HTML 没有提供相关的方法，无法确定该忽略哪些首选样式表，又该使用哪个首选样式表。

```html
<link rel="stylesheet" type="text/css"href="sheet1.css" title="Default" media="screen">
<link rel="stylesheet" type="text/css"href="print-sheet1.css" title="Default" media="print">
<link rel="alternate stylesheet" type="text/css"href="bigtext.css" title="Big Text" media="screen">
<link rel="alternate stylesheet" type="text/css"href="print-bigtext.css" title="Big Text" media="print">
```

如果不为样式表设定标题，那它就是永久样式表（persistent stylesheet），始终用于显示文档。这通常是文档编写人员想要的行为。

### 1.3.2 style 元素

style元素也是一种引入样式表的方式，直接写在文档中：

```
<style type="text/css">...</style>
```

开始与结束style标签之间的样式表称为文档样式表（document stylesheet）或嵌入样式表（embedded stylesheet）。style元素可以直接包含应用到文档上的样式，也可以通过`@import` 指令引入外部样式表。

### 1.3.3 @import 指令

与link标签一样，Web浏览器遇到`@import` 指令时会加载外部样式表。但是`@import` 指令必须写在样式表的开头，否则不起作用。

一个文档中可以有多个`@import` 指令，但是无法指定候选样式表，可以指定媒体描述符。

### 1.3.5 行内样式

如果只是为单个元素提供少量样式，可以利用HTML元素的style属性设置行内样式。

```html
<p style="color: red;">这是一段红色的字</p>
```

除了body元素之外的标签，所有的HTML标签都能设置style属性。

style属性中不能使用@import 指令。

### 1.3.4 HTTP链接

为文档关联CSS还有一种鲜为人知的方式：使用HTTP首部。

在支持HTTP链接样式表的浏览器中（比如Firefox系列），可以用此方式将开发版与线上部署版区分开。

## 1.4 样式表中的内容
### 标记
样式表中除了HTML注释外，不能有任何标记。
### 规则的结构
```css
h1 {
    color: red;
    background: yellow;
}
```

一个样式表由一系列规则组成。一个规则由两个基本部分构成：选择符（selector）和声明块（declaration block）。声明块由一个或多个声明组成，而一个声明包含一个属性（property）和对应的值（value）。

如上面的规则所示：选择符为h1。声明块为大括号内的内容。声明块里面有两个声明：字体颜色为红色，背景颜色为黄色。所以整个规则为：对于文档中的所有h1元素，显示为黄底红字。

### 厂商前缀

CSS有些内容纳前面有个标注，例如-o-border-image，这就叫做厂商前缀，浏览器通过它标记实验性或专属的属性、值或其他内容。
下表为一些常见的厂商前缀

|   前缀   |                  厂商                  |
| -------- | -------------------------------------- |
| -epub-   | 国际数字出版论坛制定的ePub格式         |
| -moz-    | 基于Mozilla的浏览器（如Firefox）       |
| -ms-     | 微软IE浏览器                           |
| -o-      | 基于Opera的浏览器                      |
| -webkit- | 基于Webkit的浏览器（如Safari和Chrome） |

厂商前缀的一般格式为一个英文破折号、一个标注和一个英文破折号。不过也有少量前缀开头没有破折号。

### 处理空白

CSS对规则之间的空白基本没有严格要求，而且对规则内部的空白也没有严格要求，不过有些例外。
一般来说，CSS对待空白的方式跟HTML差不多：解析时，连续的空白会被合并为一个空白（不论空白是空格，制表符还是换行符，甚至是他们的组合）。

### CSS注释

CSS支持注释，注释内容放在 /* 和 */之间，可以换行但是注释不能嵌套。

正确的注释：

```css
/*这是一个正确的注释，
注释可以换行。*/
 ```

## 1.5 媒体查询

文档编写人员通过媒体查询（media query）定义浏览器在何种媒体环境中使用指定的样式表。

### 用法

媒体查询可以在下述几个地方使用：

- link元素的media属性
- style属性的media属性
- @import 声明的媒体描述符部分
- @media 声明的媒体描述符部分

媒体查询可以是简单的媒体类型，也可以是复杂的媒体类型和特性的组合。

### 简单的媒体查询

这个例子中，在所以媒体中h1元素都是红褐色，但是在投影媒体中body元素会有一个黄色背景。

```css
h1{
  color: red;
}
@media projection {
  body{
    background: yellow;
  }
}
```

一个样式表中可以有任意多个@media块，而且每个都有自己的一套媒体描述符。

### 媒体类型

媒体查询最基本的形式媒体类型，由CSS2引入。媒体类型就是指明不同媒体的标注：

- all：用于所有展示的媒体。
- print：为有视力的用户打印文档时使用，也在预览打印效果时使用。
- screen：在屏幕媒体（比如电脑的显示器，Web浏览器）上展示文档时使用。

多个媒体类型使用逗号分隔，比如同时应用到屏幕媒体和印刷媒体上：

```css
@media screen, print{
	/* ... */
}
```

### 媒体描述符

一个媒体描述符包含一个媒体类型和一个或多个媒体特征列表，其中特征描述符要放在圆括号中。如果没有媒体类型，那就应用到所有媒体上面。
以下两个语句是等效的：

```css
@media all and (min-resolution: 96dpi){...}
@media (min-resolution: 96dpi){...}
```

 一般情况下，媒体特性描述符的格式类似于CSS中的一对属性和值。两者间最大的区别是特性描述符可以不包含值。因此，任何彩色媒体都符合（color）指定的条件。任何色深为16位的彩色媒体都符合（color：16）指定的条件。其实，不指定值的时候是在做判断。比如说，（color）的意思是：这个媒体是彩色的吗？
媒体查询可用的逻辑关键字有两个：


and：连接的两个或多个媒体特性必须同时满足条件，整个查询结果才为真值。

```css
(color) and (orientation: lamdscape) and (min-device-width: 800px)
/*
    表示当媒体环境是彩色的，横着放的，而且设备宽度至少是800px像素时，才会应用样式表。
*/
```
 

not：对整个查询取反。只能用在媒体查询开头。

```css
(color) and not (min-device-width: 800px)
/*
    错误！
    not只能放在媒体查询开头，这样写会被忽略。
*/
```
 

媒体查询不支持OR关键字。不过，分隔多个媒体查询的逗号相当于OR。
此外还有一个only关键字，专门用来保证向后兼容。
only：在不支持媒体查询的旧浏览器中隐藏样式表。只能用在媒体查询开头。

```css
@import url(new.css) only all;
/*
	在支持媒体查询的浏览器中，only会被忽略。
	在不支持媒体查询的浏览器中，媒体类型为only all，无效，这个媒体查询语句会被忽略。
*/
```

### 媒体特性描述符和值的类型

至2017年年底所有可用的描述符

| width             | max-device-height       | min-color-index |
| min-width         | aspect-ratio            | max-color-index |
| max-width         | min-aspect-ratio        | monochrome      |
| device-width      | max-aspect-ratio        | min-monochrome  |
| min-device-width  | device-aspect-ratio     | max-monochrome  |
| max-device-width  | min-device-aspect-ratio | resolution      |
| height            | max-device-aspect-ratio | min-resolution  |
| min-height        | color                   | max-resolution  |
| max-height        | min-color               | orientation     |
| device-height     | max-color               | scan            |
| min-device-height | color-index             | grid            |


此外，还有两种新增的值：

- ratio
- resolution

## 1.6 特性查询

2015~2016年间，CSS新增了一个功能，根据用户代理是否支持特定的CSS属性及其值来应用一段样式。这个功能被称为特性查询。

```css
@supports (color: blank) {
    body {color: blank;}
    h1 {color:pink;}
}
```

 上述代码的意思是：如果可以识别并处理color： blank这样的属性和值的组合，那么就应用这段样式。否则忽视它。

### 特性查询是渐进增强的完美方式。

与媒体查询一样，特性查询支持使用逻辑运算符and，or，not
特性查询为什么既要写属性也要写值？比如测试是否支持栅格布局：
```css
@supports (display) {
    /* 栅格样式 */
}
```
 
这样写肯定不行，因为支持display属性的不一定支持grid这个值。

注意：特性查询不是正确性查询，无法保证所有支持的浏览器的实现效果一样。


# 第 2 章 选择器

## 2.1 样式的基本规则

### 元素选择器

元素选择器通常是HTML元素。（但也有例外，比如在XML中可能有quote选择器）。

### 声明和关键字

声明块中有一个或多个声明。

声明的格式是固定的：属性 + 冒号 + 值+ 分号。例如：

```css
p {font: medium Helvetica;}
```

## 2.2 群组

把同一个样式应用到多个元素上。

### 群组选择器

选择器之间以`,`（逗号）分隔。

```css
h2, p{color: red;}
```

#### 通配选择器

`*`匹配所有元素。

在配合其他简单选择器的时候,省略掉通配选择器会有同样的效果.比如,`*.warning` 和`.warning` 的效果完全相同.

```css
/*
    文档中所有元素都显示为红色。
*/

*{color: red;}
```

#### 群组声明

一个群组可以有多个选择器，也可以有多个声明。

```css
h1{font: 18px Helvetica;}
h1{color: red;}

/*
    上面的声明和下面的声明效果一样。
*/

h1{
    font: 18px Helvetica;
    color: red;
}
```

#### 在旧浏览器中使用新的元素

有些旧浏览器不支持新加入的元素，解决方法是在DOM中创建元素。

```js
// 例如在IE8中识别main元素
document.createElement("main")
//运行这段代码后，IE8将可以识别main元素
```

## 2.3 类选择符和ID选择符

类选择器和ID选择器以一种独立于元素的方式赋予样式。

### 类选择器

应用样式而不关心所涉及的元素，最常使用类选择器。

为了把类选择器定义的样式应用在元素上，必须为class属性赋予适当的值。

```html
<p class='warning'>
    这是一段警告文本
</p>
```

然后就可以使用`.`（点号）为设定好的class设置样式。

```css
.warning{
    font-weight: bold;
    color: red;
}
```

效果：

![警告图片](https://user-gold-cdn.xitu.io/2019/8/12/16c841418e175435?w=149&h=48&f=png&s=956)

类选择器可以和其他选择器一起使用，比如对于：

```html
<p class='warning'>
    这是一段警告文本
</p>
<p>
    这一段无法被匹配
</p>
```

可以设置：

```css
p.warning{
    font-weight: bold;
    color:red;
}
```

效果：

![和其他选择器一起使用的警告文本](https://user-gold-cdn.xitu.io/2019/8/12/16c8414190ae7a65?w=157&h=94&f=png&s=2154)

#### 多个类

如果HTML中一个元素有多个类，可以把类选择器串联在一起。

```html
<p class='warning urgent'>
    这是一段警告文本
</p>
<p class='warning'>
    这一段class为warning无法被匹配
</p>
```

可以设置：

```css
/*
    串联顺序不影响效果，
    所以下面的声明也可以设置为p.urgent.warning
*/
p.warning.urgent{
    font-weight: bold;
    color:red;
}
```

效果：

![多个类选择器串联](https://user-gold-cdn.xitu.io/2019/8/12/16c841418f185a3d?w=266&h=92&f=png&s=3413)

### ID选择器

ID选择器以`#`（井号）开头，引用id属性的值。

```css
#{
    font-weight: bold;
}
```

### 在类选择器和ID选择器之间选择

一个文档中，类选择器可以使用任意多次，ID选择器只能使用一次。ID选择器不能串联使用，并且ID选择器权重更高。

## 2.4 属性选择符

不管是类选择器还是ID选择器，选择的都是属性的值。

属性选择器分为4类：**简单属性选择器**、**精准属性值选择器**、**部分匹配属性值选择器**和**起始值属性选择器**。

### 简单属性选择器

如果想要选取具有某个属性的元素，而不管这个属性的值是什么，可以使用简单属性选择器。

```css
h1[class] {color: red;}
```

简单属性选择器可以选择多个属性：

```css
/*
    对于以下css设置
*/
p[class][id] {color: red;}
```

当HTML文档为：

```html
<p id='warning' class="urgent">
    这一段文本可以被匹配
</p>
<p class='warning'>
    这一段只有class属性无法被匹配
</p>
```



效果：

![简单属性选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c841419cdf1bde?w=251&h=96&f=png&s=3714)

### 精准属性值选择器

在简单属性选择器的基础上，可以精准选择属性为特定值的元素。

```css
p[class][id='first'] {color: red;}
```

对于文档：

```html
<p id='first' class="urgent">
    这一段文本可以被匹配
</p>
<p id='warning' class="urgent">
    这一段id属性值不匹配，无法被匹配
</p>
```

效果：

![精准属性值选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c84141937d3c3d?w=278&h=101&f=png&s=3824)

### 部分匹配属性值选择器

根据属性值的一部分选择元素，而不是完整的值。

| 形式            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| [foo \|= “bar”] | 选择的元素有foo属性，并且它的值为bar或者以bar和一个英文破折号开头。 |
| [foo ~= “bar”]  | 选择的元素有foo属性，并且它的值是包含bar（用空格隔开）的一组词。 |
| [foo *= “bar”]  | 选择的元素有foo属性，并且它的值包含子串bar。                 |
| [foo ^= “bar”]  | 选择的元素有foo属性，并且它的值以bar开头                     |
| [foo $= “bar”]  | 选择的元素有foo属性，并且它的值以bar结尾。                   |

#### 对于|=：匹配属性值或属性值加-开头的子串

```css
*[lang |= "en"] { color: red;}
```

对于文档

```html
<h1 lang="en">H1标题</h1>
<p lang="en-us">一段文本</p>
<div lang="fr">一个div</div>
```

结果为：

![部分匹配属性值选择器|=](https://user-gold-cdn.xitu.io/2019/8/12/16c84141935721f7?w=145&h=140&f=png&s=3189)

#### 对于~=：匹配以空格分隔的一组词中的一个

```css
span[class ~= "warning"] { color: red;}
```

对于文档

```html
<span class="warning">第一个span</span>
<span class="blue warning">第二个span</span>
<span class="blue-warning">第三个span</span>
```

结果为：

![部分匹配属性值选择器|=](https://user-gold-cdn.xitu.io/2019/8/12/16c84141b5e56df8?w=291&h=36&f=png&s=1601)

#### 对于*=：匹配属性值的子串

```css
span[class *= "warning"] { color: red;}
```

对于文档

```html
<span class="warning">第一个span</span>
<span class="blue warning">第二个span</span>
<span class="blue-warning">第三个span</span>
```

结果为：

![部分匹配属性值选择器|=](https://user-gold-cdn.xitu.io/2019/8/12/16c84141aca8330b?w=290&h=40&f=png&s=1373)

#### 对于^=：匹配属性值开头的子串

```css
a[href ^= "https:"] { color: red;}
```

对于文档

```html
<a href = "https://www.baidu.com">https百度</a>
<a href = "http://www.baidu.com">http百度</a>
<a href = "www.baidu.com">百度</a>
```

结果为：

![部分匹配属性值选择器|=](https://user-gold-cdn.xitu.io/2019/8/12/16c84141b69b4901?w=205&h=53&f=png&s=1804)

#### 对于$=：匹配属性值结尾的子串

```css
a[href $= ".pdf"] { color: red;}
```

对于文档

```html
<a href = "a.pdf">PDF</a>
<a href = "b">any</a>
<a href = "c.txt">TXT</a>
```

结果为：

![部分匹配属性值选择器|=](https://user-gold-cdn.xitu.io/2019/8/12/16c84141b9b5fc53?w=149&h=56&f=png&s=1156)

### 不区分大小写的标识符

在结束方括号前加上`i`，属性选择器不管文档语言的要求，匹配属性值时不区分大小写。

```css
a[href $= ".pdf" i] { color: red;}
a[href $= ".txt"] { color: red;}
```

对于以下文档：

```html
<a href = "a.PDF">大写PDF</a>
<a href = "b.pdf">小写pdf</a>
<a href = "c.Pdf">混合大小写pdf</a>
<a href = "a.TXT">大写TXT</a>
<a href = "b.txt">小写txt</a>
<a href = "c.Txt">混合大小写Txt</a>
```

结果为：

![不区分大小写标识符](https://user-gold-cdn.xitu.io/2019/8/12/16c84141ca611031?w=503&h=43&f=png&s=3337)

## 2.5 根据文档结构选择

### 父子关系

dom树状图：

![dom树状图](https://user-gold-cdn.xitu.io/2019/8/12/16c84141d1f8d13d?w=1060&h=1092&f=png&s=50604)

如上图，以**body的第一个p元素**为例：

p元素是em和strong的**父元素**，em和strong是p元素的**子元素**。

p元素是html的**后代元素**。

p元素是p元素的strong元素的a元素的**祖先元素**。

### 后代选择器

后代选择器（descendant selector），又称为上下文选择器（contextual selector）。

`' '`  (空格) 操作符将选择第一个元素的子代节点。

对于：

```html
<p>
    这是一个
    <em>段落</em>
</p>
```

设置：

```css
p em {color: red;}
```

效果：

![后代选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c84141d21d7e91?w=131&h=52&f=png&s=1047)

**后代选择器的两个元素之间的层级是可以无限的。**

对于：

```html
<ul>
    <li>第一个li元素</li>
    <ol>
        <li>ol里面的li元素</li>
    </ol>
</ul>
```

设置：

```css
ul li {color: red;}
```

结果为：

![后代选择器层级无限](https://user-gold-cdn.xitu.io/2019/8/12/16c84141d5c7face?w=237&h=78&f=png&s=1880)

### 子代选择器

`'>'` 操作符选择第一个元素的直接子节点。选择器两边的空格是可选的。

对于：

```html
<ul>
    <li>第一个li元素</li>
    <ol>
        <li>ol里面的li元素</li>
    </ol>
</ul>
```

设置：

```css
ul > li {color: red;}
```

结果为：

![子元素选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c84141e65f403a?w=210&h=69&f=png&s=1937)

后代选择器和子代选择器可以同时使用，比如

```css
table.warning td > p
```

### 相邻兄弟选择器

`'+'` 操作符选择相邻元素，即第二个节点紧邻着第一个节点，并且拥有共同的父节点。选择器两边的空格是可选的。

对于：

```html
<ul>
  <li>One</li>
  <li>Two!</li>
  <li>Three</li>
</ul>
```

设置：

```css
li + li {
  color: red;
}
```

结果为：

![相邻兄弟选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c84141ebf113a4?w=139&h=89&f=png&s=1416)

两个元素之间的文本不影响相邻兄弟选择器的作用。因为这些文本属于父元素，但是如果把文本放在p元素里面，就会影响到相邻兄弟选择器。

比如：

```html
<ul>
    <li>One</li>
    一些文字
    <li>Two!</li>
    <p>第二段文字</p>
    <li>Three</li>
</ul>
```

结果为：

![相邻兄弟选择器不受文本影响](https://user-gold-cdn.xitu.io/2019/8/12/16c84141efcafe4c?w=170&h=161&f=png&s=2675)

### 兄弟选择器

`'~'` 操作符选择兄弟元素，也就是说，第二个节点在第一个节点后面的任意位置，并且这俩节点的父节点相同。

对于：

```html
<h2>h2标题</h2>
<p>第一段文字</p>
<h3>h3标题</h3>
<p>第二段文字</p>
<p>第三段文字</p>
```

设置：

```css
h2 ~ p {
    color: red;
}
```

结果为：

![兄弟选择器](https://user-gold-cdn.xitu.io/2019/8/12/16c84141f7233c99?w=130&h=236&f=png&s=4748)

## 2.6 伪类选择符

伪类选择器指定要选择的元素的特殊状态，可以为文档中不一定真正存在的结构指定样式。

**伪类始终指代所依附的元素。**

### 拼接伪类

css允许把伪类串联（拼接）在一起，伪类串联的顺序没有什么关系。

```css
a:link:hover{color: red;}
/*
	等价于
*/
a:hover:link{color: red;}
```

但是互斥的伪类不能串联，比如link和visited。

### 结构伪类

伪类大部分是结构上的，即它们指代文档中的标记结构。

#### 选择根元素

`:root`伪类选择根元素，在HTML中，根元素始终是html，这个选择符真正的用途是在XML语言的样式表中。

#### 选择空元素

`:empty`伪类可以选择没有任何子代的元素，甚至连文本和空白都没有。

`:empty`伪类可以匹配html的空元素，比如img和input，但是它还可以匹配没有内容纳textarea元素。

**截止2017年末，`empty`是唯一一个在匹配时考虑文本节点的css选择器，其他选择器只会考虑元素。**

#### 选择唯一子代

##### only-child伪类

`:only-child`伪类匹配的元素是另一个元素唯一的子代。

对于：

```html
<ul>
    <li>第一个li元素</li>
    <li>第二个li元素</li>
    <ol>
        <li>第三个li元素</li>
    </ol>
</ul>
```

设置：

```css
li:only-child {
    color: red;
}
```

效果为：

![唯一子代伪类](https://user-gold-cdn.xitu.io/2019/8/12/16c8414202ef022a?w=193&h=96&f=png&s=1991)

##### only-of-type伪类

`:only-of-type`伪类匹配的元素没有其他相同类型的兄弟元素（唯一的那一种元素）。

对于：

```html
<main>
  <div>I am `div` #1.</div>
  <p>I am the only `p` among my siblings.</p>
  <div>I am `div` #2.</div>
  <div>I am `div` #3.
    <i>I am the only `i` child.</i>
    <em>I am `em` #1.</em>
    <em>I am `em` #2.</em>
  </div>
</main>
```

设置：

```css
/*
	这里使用了后代选择器，所以选取的是main元素的后代里面的相对于父元素唯一的那一种元素。
*/
main :only-of-type {
  color: red;
}
```

效果为：

![only-of-type伪类](https://user-gold-cdn.xitu.io/2019/8/12/16c84141fc05b306?w=510&h=135&f=png&s=5755)

#### 选择第一个和最后一个子代

`:first-child`选择一个元素的第一个元素。

`:last-child`选择一个元素的最后一个元素。

对于：

```html
<div>
    <p>第一个p元素</p>
    <p>第二个p元素</p>
    <p>最后一个p元素</p>
</div>
```

设置：

```css
p:first-child {
  color: red;
}
p:last-child {
  color: blue;
}
```

效果为：

![第一个和最后一个后代](https://user-gold-cdn.xitu.io/2019/8/12/16c84142096aefaf?w=141&h=122&f=png&s=2545)

#### 选择第一个和最后一个某种元素

`:first-of-type`选择一组兄弟元素中某类型的第一个元素。

`:last-of-type`选择一组兄弟元素中某类型的最后一个元素。

对于：

```html
<article>
    <div>这是第一个 `div` </div>
    <div>这个 <span> `span` 是第一个也是最后一个</span>!</div>
    <div>这个 <em> `em` 是第一个</em>, 这个 <em> `em` 是最后一个</em> !</div>
    <div>这个 <span> `span` 是第一个也是最后一个</span>!</div>
    <b>这个 `b` 是第一个也是最后一个</b>
    <div>这个 `div` 是最后一个</div>
</article>
```

设置：

```css
article :first-of-type {
  background-color: pink;
}
article :last-of-type {
  color: red;
}
```

效果为：

![选择第一个和最后一个某种元素](https://user-gold-cdn.xitu.io/2019/8/12/16c841420cfb1bf9?w=419&h=146&f=png&s=11543)

#### 选择每第N个子元素

`:nth-child(an+b)`首先找到所有当前元素的兄弟元素，然后按照位置先后顺序从1开始排序，选择的结果为第（an+b）个元素的集合（n=0，1，2，3..…）。示例：

- `0n+3` 或简单的 `3` 匹配第三个元素。
- `1n+0` 或简单的 `n` 匹配每个元素。
- `2n+0` 或简单的 `2n` 匹配位置为 2、4、6、8..…的元素（n=0时，2n+0=0，第0个元素不存在，因为是从1开始排序)。你可以使用关键字 **even** 来替换此表达式。
- `2n+1` 匹配位置为 1、3、5、7..…的元素。你可以使用关键字 **odd** 来替换此表达式。
- `3n+4` 匹配位置为 4、7、10、13..…的元素。

`a` 和 `b` 都必须为整数，并且元素的第一个子元素的下标为 1。

`:nth-last-child(an+b)`的作用与`:nth-child(an+b)`一样，不过它是从最后一个开始计算。

对于：

```html
<ul>
    <li>第1个li元素</li>
    <li>第2个li元素</li>
    <li>第3个li元素</li>
    <li>第4个li元素</li>
    <li>第5个li元素</li>
    <li>第6个li元素</li>
    <li>第7个li元素</li>
</ul>
```

设置：

```css
li:nth-child(1) {
    background: pink;
}
li:nth-child(2n + 2) {
    background: #5bc49f;
}
li:nth-last-child(3n + 1) {
    color: red;
}
```

效果为：

![选择第每n个子元素](https://user-gold-cdn.xitu.io/2019/8/12/16c84142120a212e?w=373&h=196&f=png&s=8116)

#### 选择每第N个某种元素

`:nth-of-type(an+b)`和`:nth-last-of-type(an+b)`选择每第N个某种元素。

对于：

```html
<div>
    <span>这是 span.</span>
    <span>这是另一个 span.</span>
    <em>这个是 em.</em>
    <span>这是第三个span</span>
    <p>这个是p.</p>
    <span>这是最后一个span.</span>
</div>
```

设置：

```css
span:nth-last-of-type(1) {
    background-color: lime;
}
span:nth-of-type(2) {
    background-color: #5bc49f;
}
p:nth-last-of-type(1) {
    color: white;
}
p:nth-of-type(1) {
    background-color: #5bc49f;
}
```

效果为：

![选择每第N个某种元素](https://user-gold-cdn.xitu.io/2019/8/12/16c8414214952ff3)

### 动态伪类

动态伪类在页面渲染结束后根据页面变化而变化。

#### 超链接伪类

| 伪类     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| :link    | 指代用作超链接的锚记（即具有href属性），而且指向未访问过的地址。 |
| :visited | 指代指向已访问地址的超链接。出于安全考虑，可用的样式十分有限。 |

> 出于隐私考虑，:visited伪类只能设置颜色相关的属性，并且通过DOM查询已访问链接的样式，返回的值和未访问时一样。

#### 用户操作伪类

| 伪类    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| :focus  | 指代当前获得输入焦点的元素，即可以接受键盘输入或以某种方式激活。 |
| :hover  | 指代鼠标指针放置在上面的元素，例如鼠标指针悬停在超链接上。   |
| :active | 指代由用户输入激活的元素，例如用户点击超链接时按下鼠标的那段时间。 |

可以处于`:active`状态的元素有链接，菜单项目，以及可以设定tabindex属性的元素。这些元素，加上其他所有的交互元素，还可以获得焦点。

这些伪类通常用于超链接，推荐使用顺序为：`link - visited - hover - active`

#### 动态样式引起的问题

动态伪类有些耐人寻味的问题和怪异行为。比如：把已访问的链接和未访问的链接设置成相同的字号，同时在悬停时把字号放大，这可能会导致这个链接后面的内容重排（重新绘制文档）。

### UI状态伪类

| 伪类           | 说明                                                         |
| -------------- | ------------------------------------------------------------ |
| :enabled       | 指代启用的用户界面元素（比如表单元素），即接受输入的元素。   |
| :disabled      | 指代禁用的用户界面元素（比如表单元素），即接受输入的元素。   |
| :checked       | 指代由用户或文档默认选中的单选按钮或复选框。                 |
| :indeterminate | 指代既没有选中也没有未选中的单选按钮或复选框，这个状态只能由DOM脚本设定。 |
| :default       | 指代默认选中的单选按钮、复选框或选项。                       |
| :valid         | 指代满足所有数据有效性语义的输入框。                         |
| :invalid       | 指代不满足所有数据有效性语义的输入框。                       |
| :in-range      | 指代输入的值在最大值和最小值之间的输入框。                   |
| :out-of-range  | 指代输入的值不在最大值和最小值之间的输入框。                 |
| :required      | 指代必须输入值的输入框。                                     |
| :optional      | 指代不需要一定输入值的输入框。                               |
| :read-write    | 指代可由用户编辑的输入框。                                   |
| :read-only     | 指代不能由用户编辑的输入框。                                 |

虽然UI元素的状态可由用户操作而改变，但是UI状态伪类不是单纯动态的，因为它们还受文档结构或DOM脚本的影响。

### target伪类

`:target`伪类代表一个唯一的页面元素(目标元素)，其`id` 与当前URL片段匹配 .

对于：

```html
<section id="section2">Example</section>
```

设置：

```css
:target {
    border: 2px solid black;
}
```

当访问页面的#section2时，效果为：

![target伪类](https://user-gold-cdn.xitu.io/2019/8/12/16c8414232608109?w=424&h=119&f=png&s=7545)

`:target`伪类在以下两种情况下不会被使用：

1. 页面的URL中没有片段标识符
2. 页面的URL中有片段标识符，但是文档中没有与之匹配的元素

### :lang 伪类

如果想根据文本使用的语言选择元素，可以使用`:lang`伪类，在匹配方式上，`:lang`伪类和`|=`属性选择器类似。

伪类选择器和属性选择器之间的主要区别是语言信息有多个来源，有可能来自元素自身以外。对于属性选择器来说，元素自身必须有`lang`属性菜能匹配，而`:lang`伪类能匹配设定了语言的元素的后代。

> 在HTML中, 语言是通过`lang` 属性,和 `meta` 元素的组合来决定的, 也可能是通过协议的信息来确定（例如HTTP头）. 对于其他文档类型，也可能存在其他用于确定语言的方法。

### 否定伪类

`:not()`伪类依附在元素上，括号内是简单的选择器。

根据W3C的定义，**简单选择器**指：一个类型选择器，通用选择器，属性选择器，类选择器，ID选择器或伪类。（基本上就是没有祖辈 - 后代关系的选择器）。

`:not()`伪类中只能使用一个选择器，所以不能使用群则选择器，不能使用后代选择器等等。

`:not()`可以在选择器的任何位置使用。

`:not()`伪类不能嵌套。

`:not()`伪类可以串联使用，相当于“也不是”。

对于：

```html
<p class='first' id='txt'>这是一段文本</p>
<p class='second' id='TXT'>这是第二段文本</p>
<p class='three' id='txt-other'>这是第三段文本</p>
```

设置：

```css
p:not(#txt):not(.three) {
    color: red;
}
```

效果为：

![not伪类](https://user-gold-cdn.xitu.io/2019/8/12/16c84142228ec60f?w=149&h=130&f=png&s=2512)

## 2.7 伪元素选择符

伪元素和伪类很像，为了实现特定的效果，它在文档中插入虚拟的元素。

CSS2定义了4个伪元素，CSS2之后又定义了其他伪元素。这里只介绍CSS2定义的4个。

伪类使用一个冒号，伪元素使用两个冒号（为了向后兼容，伪元素也可以使用一个冒号，但是不建议）。

所有的伪元素只能出现在选择器的最后面（所有只能使用一个伪元素）。

### 装饰首字母伪元素

`::first-letter`伪元素用于装饰任何非行内元素的首字母，或者开头的标点符号和首字母。

`::first-letter`伪元素最常用来实现排版效果中的**首字母下沉**或者**首字母大写**。

对于：

```html
<p>这是一段文本</p>
<p>这是第二段文本</p>
```

设置：

```css
p:first-of-type::first-letter {
    color: red;
    font-size: 200%;
}
```

效果为：

![::first-letter伪元素](https://user-gold-cdn.xitu.io/2019/8/12/16c84142231d8ea5?w=153&h=117&f=png&s=2108)

这个规则相当于构建了一个虚拟的元素来包裹首行的第一个文本。比如：

```html
<p>
    <p-first-letter>这</p-first-letter>
    是一段文本
</p>
<p>这是第二段文本</p>
```

`p-first-letter`元素既不出现在文档的源码中，也不出现在DOM树中，而是由用户代理动态构建，也就是说，`p-first-letter`是一个伪元素。

### 装饰首行

`::first-line`用于装饰元素的首行文本。

### 对于::first-letter和::first-line的限制

目前，`::first-letter`和`::first-line`伪元素只能应用到块级元素上，例如标题和段落，不能应用到行内元素上，比如超链接。

另外，对于它们可使用的CSS属性也有限制。

允许伪元素使用的属性：

| ::first-letter   | ::first-line     |
| ---------------- | ---------------- |
| 所有的字体属性   | 所有的字体属性   |
| 所有的背景属性   | 所有的背景属性   |
| 所有文本装饰属性 | 所有文本装饰属性 |
| 所有行内排版属性 | 所有行内排版属性 |
| 所有行内布局属性 | 所有外边距属性   |
| 所有边框属性     | 所有内边距属性   |
| box-shadow       | 所有边框属性     |
| color            | color            |
| opacity          | opacity          |

### 装饰（或创建）前置和后置内容元素

`::before`和`::after`创建一个伪元素，其将成为匹配选中的元素的第一个子元素。常通过 `content`属性来为一个元素添加修饰性的内容。此元素默认为行内元素。

由`::before` 和`::after` 生成的伪元素 包含在元素格式框内， 因此不能应用在替换元素上， 比如`img`或`br` 元素。

生成内容是一个单独的话题，会在15章进行更深入的介绍。

# 第 3 章 特指度和级联

## 3.1 特指度

优先级就是分配给指定的CSS声明的一个权重，由选择器的本身组成决定，一个优先级由4部分构成，例如（0, 0, 0, 0）。

选择器的优先级有以下规则：

1. ID选择器为`0, 1, 0, 0`。
2. 类选择器，属性选择器，伪类为`0, 0, 1, 0`。
3. 每个元素选择器，伪元素为`0, 0, 0, 1`。
4. 连接符和通配选择器不增加优先级（通配选择器的优先级为`0, 0, 0, 0`，而连接符没有优先级）。
5. 行内样式的优先级为`1, 0, 0, 0`。

比如：

```css
h1 {color: red;} /* 优先级 = 0, 0, 0, 1 */
p em {color: red;} /* 优先级 = 0, 0, 0, 2 */
.warning {color: red;} /* 优先级 = 0, 0, 1, 0 */
*.warning.up {color: red;} /* 优先级 = 0, 0, 2, 0 */
div#main {color: red;} /* 优先级 = 0, 1, 0, 1 */
div#main *[href] {color: red;} /* 优先级 = 0, 1, 1, 1 */
```

如果两个或多个属性声明有冲突，那么优先级高的会胜出。

```css
em {color: red;} /* 优先级 = 0, 0, 0, 1 */
p em {color: red;} /* 优先级 = 0, 0, 0, 2 (胜出)*/
```

### 声明和优先级

选择器的优先级确定后，将被赋予关联的每个声明。

比如：

```css
h1 {
    color: red;
    backgroud: black;
}
/* 将被视为： */
h1 {color: red;}
h1 {backgroud: black;}
```

如果多个规则匹配同一个用啥，那么优先级就起作用了。

比如：

```css
h1 + p {color: red;}/* 优先级 = 0, 0, 0, 2 */
.side{color: green;}/* 优先级 = 0, 0, 1, 0 */
p{color: blue;}/* 优先级 = 0, 0, 0, 1 */
```

对于文档：

```html
<h1>这个是h1</h1>
<p class='side'>这是一个段落</p>
```

结果为：

![优先级](https://user-gold-cdn.xitu.io/2019/8/14/16c9091a40c6ae61?w=187&h=135&f=png&s=3854)

### 通配选择器和连接符的优先级

通配选择器优先级为0, 0, 0, 0，连接符不存在优先级。

### ID选择器和属性选择器的ID属性的优先级

ID选择器和属性选择器的ID属性的优先级是不同的，ID选择器的优先级为`0, 1, 0, 0`；而属性选择器的ID属性的优先级为`0, 0, 1, 0`。

### 行内样式的优先级

行内样式的优先级为`1, 0, 0, 0`，所有行内样式具有最高的优先级。

### 例外的 `!important` 规则

当在一个样式声明中使用一个`!important` 规则时，**此声明将覆盖任何其他声明**。虽然技术上`!important`与优先级无关，但它与它直接相关。

比如：

```css
h1 + p {color: red;}/* 优先级 = 0, 0, 0, 2 */
.side{color: green;}/* 优先级 = 0, 0, 1, 0 */
p{color: blue !important;}/* 优先级 = 0, 0, 0, 1 */
```

对于文档：

```html
<h1>这个是h1</h1>
<p class='side'>这是一个段落</p>
```

结果为：

![!important规则](https://user-gold-cdn.xitu.io/2019/8/14/16c9091a40d7f362?w=353&h=154&f=png&s=8246)

## 3.2 继承

继承指某些样式不仅应用到所指的元素，还应用到元素的后代上。

在CSS中，每个**CSS属性定义的概述**都指出了这个属性是默认继承的(“Inherited: Yes”) 还是默认不继承的(“Inherited: no”)。这决定了当你没有为元素的属性指定值时该如何计算值。

继承是CSS的根基之一，哪些属性默认被继承哪些不被继承大部分符合常识，通常无需考虑。但是需要注意的是：

**继承的值没有优先级。**（所以继承属性和通配选择器有冲突时候，通配选择器胜出）。

比如以下CSS设置：

```css
* {color: red;}
h1#title {color: black;}
```

对于文档：

```html
<h1 id="title">
    h1标题<em>倾斜的em</em>
</h1>
```

结果为：

![继承的值没有优先级](https://user-gold-cdn.xitu.io/2019/8/14/16c9091a4131a14a?w=449&h=232&f=png&s=13232)

## 3.3 层叠

层叠是CSS的一个基本特征，它是一个定义了如何合并来自多个源的属性值的算法。它在CSS处于核心地位，CSS的全称层叠样式表正是强调了这一点。

CSS声明可以有不同的来源：

- 浏览器会有一个基本的样式表来给任何网页设置默认样式。这些样式统称**用户代理样式**。
- 网页的作者可以定义文档的样式，这是最常见的样式表。
- 读者，作为浏览器的用户，可以使用自定义样式表定制使用体验。

### 层叠规则

1. 首先过滤来自不同源的全部规则，并保留要应用到指定元素上的那些规则。

2. 依据重要性对这些规则进行排序。即是指，规则后面是否跟随者`!important`以及规则的来源。**层叠是按升序排列的**，这意味着来着用户自定义样式表的`!important`值比用户代理样式表的普通值优先级高：

	| 重要性（从低到高） | 来源     | 重要程度     |
	| :---------------- | :------- | :----------- |
	| 1                 | 用户代理 | 普通         |
	| 2                 | 用户代理 | `!important` |
	| 3                 | 用户     | 普通         |
	| 4                 | 页面作者 | 普通         |
	| 5                 | CSS动画  | 见下节       |
	| 6                 | 页面作者 | `!important` |
	| 7                 | 用户     | `!important` |

3. 假如层叠顺序相等，则使用哪个值取决于优先级。

### CSS动画与层叠

CSS动画，指使用`@keyframes` @规则定义状态间的动画。关键帧不参与层叠，意味着在任何时候CSS都是取单一的`@keyframes`的值而不会是某几个`@keyframe`的混合。

当有多个满足条件的关键帧时，在最重要的文档里面最后定义的关键帧会被选中，而不会是将它们组合在一起。

同时仍应注意用`@keyframes` @规则定义的值会覆盖全部普通值，但会被`!important`的值覆盖。

### 例子

**用户代理CSS：**

```css
li { margin-left: 10px }
```

**网页作者CSS1：**

```css
li { margin-left: 0 } 
```

**网页作者CSS2：**

```css
@media screen {
  li { margin-left: 3px }
}

@media print {
  li { margin-left: 1px }
}
```

**用户CSS：**

```css
.specific { margin-left: 1em }
```

**HTML：**

```html
<ul>
  <li class="specific">1<sup>st</sup></li>
  <li>2<sup>nd</sup></li>
</ul>
```

对于这个情形，应当应用`li`和`.specific`里面的声明。由于没有声明被标记为`!important`，所以优先顺序为页面作者样式优于用户样式，用户代理样式最低。

故是这3条声明的竞争：

```css
margin-left: 0
margin-left: 3px
margin-left: 1px
```

由于是在屏幕显示，所以最后一条舍弃，而前两条的选择器相同，因此优先级也相同，故最终选择的是后者：

```css
margin-left: 3px
```

注意尽管定义在用户CSS里面的声明有更高的优先级，但它并不会被选中，因为层叠算法是先于优先级算法的。

# 第 4 章 值和单位

## 4.1 关键字，字符串和其他文本值

### 关键字

有时，值用一个词表示，这就是关键字。

`none`是一个常见的关键字，如果想要移除链接的下划线，可以这么写

```css
a:link, a:visited{text-decoration: none;}
```

#### 全局关键字

CSS3定义了几个全局关键字，所有的属性都能使用：`inherit`, `initial`和`unset`。

- `inherit`关键字：`inherit`元素把某个属性的值设为和父元素同一属性的值一样。
- `initial`关键字：`initial`把属性设为预定义的值，相当于重置。
- `unset`关键字：`unset`会自动选取`inherit`或`initial`，对于继承的属性来说，使用`inherit`，不继承的属性，使用`initial`。

这三个关键字在所有的属性中都可以使用。

`all`这个特殊的属性只接受这几个全局关键字。

` all` 表示除了 `unicode-bidi` 与 `direction` 之外的所有属性。

### 字符串

字符串指放在单引号或双引号内的任意字符序列。

### URL

URL分为绝对URL和相对URL。

引用URL的格式如下：

```css
url(protocol://server/pathname) /* 绝对URL */
url(pathname) /* 相对URL */
```

### 标识符

有些属性接收标识符，最常见的有生成的列表序号。在取值语法中用`<identifier>`表示。

## 4.2 数字和百分数

| 名称   | 数据类型       | 说明                                                   |
| ------ | -------------- | ------------------------------------------------------ |
| 整数   | `<integer>`    | 由一到多个数组成，前面可以有`+`或`-`，表示正数和负数。 |
| 数字   | `<number>`     | 整数或者实数（小数）。                                 |
| 百分数 | `<percentage>` | 在`number`后加一个`%`。                                |
| 弹性值 | `<flex>`       | 在`number`后加`fr`。                                   |

## 4.3 距离

`<length>`是表示距离尺寸的一种CSS数据格式。`<length>`数据类型包含`number`，后面跟长度单位。 

### 绝对长度单位

| 类型 | 说明                                         |
| ---- | -------------------------------------------- |
| `cm` | 厘米                                         |
| `mm` | 毫米                                         |
| `q`  | 四分之一毫米                                 |
| `in` | 英寸（2.54厘米）。`1in` = `2.54cm` = `96px`. |
| `pt` | 点（1/72 英寸）。`1pt` = 1/12 `pc`.          |
| `pc` | 派卡。`1pc` = `12pt` = 1/6 `in`.             |
| `px` | `1px` = 1/96 `in`.                           |

**如果显示器的像素密度与每英寸96px相差特别大，用户代理应该缩放像素度量，使用参考像素。**

### 分辨率单位

随着媒体查询和响应式设计的出现，为了描述显示器的分辨率，出现了3个新的单位。

| 类型   | 说明                                |
| ------ | ----------------------------------- |
| `dpi`  | 表示每英寸的点数。                  |
| `dpcm` | 表示每`cm`的点数。                  |
| `dppx` | 表示每`px`的点数。`1dppx` = `96dpi` |

### 相对长度单位

相对长度代表着以其它距离为单位的一种尺寸。使用这个单位的，可以是指定字符的大小，行高，或者是[viewport](https://developer.mozilla.org/zh-CN/docs/Glossary/viewport)的大小。

| 类型  | 说明                                                     |
| ----- | -------------------------------------------------------- |
| `em`  | 1em等于**元素**的`font-size`属性值。                     |
| `ex`  | ex指**所用字体**中小写字母x的高度。                      |
| `rem` | 1rem等于**根元素**的`font-size`属性值。                  |
| `ch`  | 这一单位代表元素所用字体 `font`中“0”这一字形的预测尺寸。 |

### 视口相关的单位

视口百分比长度定义相对于[viewport](https://developer.mozilla.org/zh-CN/docs/Glossary/Viewport)的大小的`<length>`值，即文档的可见部分。 

| 类型   | 说明                                 |
| ------ | ------------------------------------ |
| `vw`   | 视口宽度的 1/100。                   |
| `vh`   | 视口高度的 1/100。                   |
| `vmin` | 视口高度和宽度之间的最小值的 1/100。 |
| `vmax` | 视口高度和宽度之间的最大值的 1/100。 |

## 4.4 计算值

`calc()` 函数允许在声明CSS属性值时执行一些计算。

它可以用在如下场合：[`<length>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/length)、[`<frequency>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/frequency), [`<angle>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/angle)、[`<time>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/time)、[`<number>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/number)、或[`<integer>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/integer)。

例如：

```css
/* property: calc(expression) */
width: calc(100% - 80px);
```

`calc()` 函数用一个表达式作为它的参数，用这个表达式的结果作为值。这个表达式可以是`+`, `-`, `*`, `/`（加减乘除）操作符的组合，采用标准操作符处理法则的简单表达式。在需要时，还可以使用小括号来建立计算顺序。

有以下限制：

1. 在 `+` 和 `-` 运算符两边必须使用相同的单位类型。
2. ` * ` 计算的两个值中必须有一个是 `<number>` 。
3. `/` 计算的两个值的右侧的那个必须是 `<number>` 。
4. 任何情况下都不能除以0。
5. **在 `+` 和 `-` 运算符两边必须有空白。**

## 4.5 属性值

在一些CSS属性中，可以使用样式表对应的元素上的HTML属性值，方法是使用`attr()` 表达式。

比如：

```css
p::before {content: "[" attr(id) "]";}
```

对于以下文档：

```html
<p id="text">
    这是一段文本
</p>
```

结果为：

![属性值](https://user-gold-cdn.xitu.io/2019/8/16/16c99ca7bf8a8864?w=372&h=214&f=png&s=9261)

**`attr()` 理论上能用于所有的CSS属性，但目前支持的仅有伪元素的 [`content`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/content) 属性**

## 4.6 颜色

### 色彩关键字

如果只想使用基本的颜色，使用[色彩关键字]([https://developer.mozilla.org/zh-CN/docs/Web/CSS/color_value#%E5%8F%96%E5%80%BC](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color_value#取值))是最简单的办法。

色彩关键字是不区分大小写的标识符，它表示一个具体的颜色，例如 `red, blue, brown, lightseagreen` 。

### RGB 和 RGBa 颜色

颜色可以使用红-绿-蓝（red-green-blue (RGB)）模式被定义。

#### 函数式RGB

`rgb(R,G,B)`，`rgb` 后跟3个 [`<integer>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/integer) 或3个 [`<percentage>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/percentage) 值。整数 255 相当于 100%，和十六进制符号里的 F 或 FF 。

#### 十六进制RGB

`#RRGGBB` 和 `#RGB`

- `#` 后跟6位十六进制字符（0-9, A-F）。
- `#` 后跟3位十六进制字符（0-9, A-F）

三位数的 RGB 符号（`#RGB`）和六位数的形式（`#RRGGBB`）是相等的。例如， `#f03` 和 `#ff0033` 代表同样的颜色。

#### 函数式RGBa

`rgba()` 函数在红-绿-蓝-阿尔法（RGBa）模式下被定义。RGBa 扩展了 RGB 颜色模式，它包含了阿尔法通道，允许设定一个颜色的透明度。
**a** 表示透明度：0=透明；1=不透明；

#### 十六进制RGBa

`#RRGGBBaa` 和 `#RGBa`

与`RGBa`一样，多出来的`a`为alpha通道的值。

### HSL 和 HSLa 颜色

**HSL**即[色相](https://zh.wikipedia.org/wiki/色相)、[饱和度](https://zh.wikipedia.org/wiki/色度_(色彩学))、[亮度](https://zh.wikipedia.org/wiki/亮度)（英语：Hue, Saturation, Lightness）。

**色相（Hue）** 表示色环（即代表彩虹的一个圆环）的一个角度（0~360度）。这个角度作为一个无单位的 [`<numbe>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/number) 被给出。定义 **red=0=360**，其它颜色分散于圆环，所以 **green=120**, **blue=240**，以此类推。作为一个角度，它隐含像 -120=240 和 480=120 这样的回环。

饱和度和明度由百分数来表示。

`100%` 是满**饱和度**，而 `0%` 是一种灰度。

`100%` **亮度**是白色， `0%` 亮度是黑色，而 `50%` 亮度是“一般的”。

#### HSLa

颜色可以使用 `hsla()` 函数符在色相-饱和度-明度-阿尔法（HSLa）模式下被定义。HSLa 扩展自 HSL 颜色模式，包含了阿尔法通道，可以规定一个颜色的透明度。
**a** 表示透明度：0=透明；1=不透明；

### 特殊的颜色关键字

有两个颜色关键字可以在任何允许使用颜色值的地方使用：

- `transparent` 关键字表示一个完全透明的颜色，即该颜色看上去将是背景色。从技术上说，它是带有阿尔法通道为最小值的黑色，是 `rgba(0,0,0,0)` 的简写。
- `currentColor` 关键字代表当前元素的 [`color`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/color) 属性的计算值。

## 4.7 角度

| 类型   | 说明                            |
| ------ | ------------------------------- |
| `deg`  | 度数。完整的圆周是360度。       |
| `grad` | 百分度。完整的圆周是400百分度。 |
| `rad`  | 弧度。完整的圆周是2π。          |
| `turn` | 圈数。一个完整的圆周是一圈。    |

## 4.8 时间和频率

`<time>` 数据类型 表达了以秒（s）或毫秒（ms）为单位的时间的值。于[`animation`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation)、[`transition`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition)及相关属性中使用，用来定义持续时间或延迟时间。它是一个 `<number>` 值后跟一个`s`（秒）或者`ms`（毫秒）。

`<frequency>` 数据类型表示频率维度，像一个说话声音的音调。 它由一个[`<number>`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/number) 值后跟一个 `hz`（赫兹） 或 `khz` （千赫兹）组成。

## 4.9 位置

`<position>` 数据类型表示用于设置相对于框的位置的2D空间中的坐标，用来指定图像在背景区域的位置（`background-position` 属性）。

定义：
```
[
    [ left | center | right | top | bottom | <percentage> | <length> ] |
    [ left | center | right | <percentage> | <length> ]
    [ top | center | bottom | <percentage> | <length> ] |
    [ center | [ left | right ] [ <percentage> | <length> ]? ] && 
    [ center | [ top | bottom ] [ <percentage> | <length> ]? ]
]
```

### 声明一个值

如果只声明一个值，那么第二个值将被设置为 `center` 。

```css
left;
/* 实际上为 */
left center;
```

### 声明两个值

如果声明了两个值（像上面那样隐式或显式），而且第一个值为长度或者百分数，那么前一个值始终是横向值。

```css
25% 35px;/* 25% 是横向距离， 35px是纵向距离。 */
35px 25%;/* 35px 是横向距离， 25% 是纵向距离。 */
```

所以如果写 ` 25% left` 将会无效，因为两个值都是横向距离，没有指定纵向距离。（同理 `left right` 等也无效）。

如果写成 `left 25%` 有效，因为既指定了横向距离，又指定了纵向距离。 

### 声明三个值

三个值的最后一个值被设置为0，然后按照四个值去处理。所以 `right 20px bottom` 和 `right 20px bottom 0` 效果一样。

### 声明四个值

如果声明四个值，必须有两个长度或百分数，而且它们前面都得是关键字。比如 `right 10% top 25px` 。

## 4.10 自定义值

CSS 变量是由CSS作者定义的实体，其中包含要在整个文档中重复使用的特定值。使用自定义属性来设置变量名，并使用特定的 [var() ](https://developer.mozilla.org/zh-CN/docs/Web/CSS/var)来访问。

`var()` 函数可以代替元素中任何属性中的值的任何部分。`var()` 函数不能作为属性名、选择器或者其他除了属性值之外的值。

CSS 变量定义由 `--` 开头，区分大小写。

```css
div {
    --default--color: red;
}
p {color: var(--default--color);}
```

对于文档：

```html
<div>
    <p>一段文本</p>
</div>
```

结果为：

![css变量](https://user-gold-cdn.xitu.io/2019/8/16/16c99ca7bfbcb32c?w=330&h=58&f=png&s=3020)

CSS变量拥有作用域，所以可以在 `:root` 定义全局变量。

**在MDN的介绍里，CSS变量可以自定义属性，[点击链接查看相关信息](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties#什么是CSS变量)。**

第 5 章 字体
第 6 章 文本属性
第 7 章 基本的视觉格式化
第 8 章 Padding, Borders, Outlines 和 Margins
第 9 章 颜色、背景和渐变

# 下册

第 10 章 浮动和形状

# 第 11 章 定位

定位的原理相当简单。你可以相对元素框的常规位置定义元素的具体位置，可以相对父元素或另一个元素定位元素的位置，甚至还可以相对视区（例如浏览器窗口）定位元素的位置。

## 11.1 基本概念

在我们深入研究各种定位之前，最好先看看存在哪些类型以及它们之间的区别。我们还需要定义一些基本的概念，这些概念对于理解定位是如何工作的是非常重要的。

### 11.1.1 定位的类型

您可以使用 position 属性从五种不同的定位类型中选择一种，这将影响元素框的生成方式。

<Cards cards="position" />

position 属性各值得含义如下

1. static：正常生成元素框。块级元素生成矩形框，位于文档流中；行内元素生成一个或多个行框，随父元素流动。
2. relative：元素框偏移一定的距离。元素的形状与未定位时一样，而且元素所占的空间也与正常情况下相同。
3. absolute：元素框完全从文档流中移除，相对容纳块定位。此时，容纳块可能是文档中的另一个元素，也可能是初始容纳块（参见下一节）。正常情况下元素在文档流中占据的空间不复存在，好似元素没有出现过一样。不管元素在常规的文档流中生成什么类型的框体，定位后生成的都是块级框。
4. fixed：元素框的行为类似于 absolute,不过容纳块是视区自身。
5. sticky：元素一开始留在常规的文档流中，达到触发粘滞的条件时，从常规的文档流中移除，不过在常规文档流中占据的空间得以保留。此时，相当于相对容纳块绝对定位，触发粘滞的条件失效后，元素回到常规文档流中最初的位置。

### 11.1.2 容纳块

一般而言，容纳块指包含另一个元素的框体。比如说，在常规文档流中，根元素（HTM 中的 html）是 body 元素的容纳块，body 元素又是其所有子元素的容纳块，以此类推，但是对定位元素来说，容纳块完全取决于定位类型。

对非根元素来说，如果 position 属性的值是 relative 或 static,其容纳块由最近的块级、单元格或行内块级祖辈元素框体的内容边界划定。

对非根元素来说，如果 position 属性的值是 absolute,其容纳块是 position 属性的值不是 static 的最近的祖辈元素（任何类型）。具体规则如下：

- 如果祖辈元素是块级元素，容纳块是那个元素的内边距边界，即由边框限定的区域。
- 如果祖辈元素是行内元素，容纳块是祖辈元素的内容边界。在由左至右书写的语言中，容纳块的顶边和左边是祖辈元素中第一个框体的内容边界的顶边和左边，底边和右边是最后一个框体的内容边界的底边和右边。在从右向左书写的语言中，容纳块的右边界是第一个框体内容区的右边界，左边界是最后一个框体内容区的左边界；顶边和底边与前述情况一样。
- 如果没有祖辈元素，元素的容纳块是初始容纳块。

上述确定容纳块的规则有一个变数：对粘滞定位的元素来说，容纳块的边界由粘滞限定矩形确定。粘滞定位就发生在这个矩形中，详情参见 11.9 节。

注意，定位的元素可能位于容纳块外部。我们知道，浮动元素可以使用负外边距移到父元素的内容区外部，这里的情况与之类似。其实，“容纳块”应该换成“定位上下文”，但是规范用的就是“容纳块”。

## 11.2 偏移属性

前一节介绍的定位方式中有四种，即相对定位、绝对定位、粘滞定位和固定定位，使用四个属性指定定位元素的各边相对容纳块的偏移。这四个属性称为偏移属性（offset property），对定位有极大的影响。

<!-- <Cards cards="top_right_bottom_left" /> -->

这些属性指定距容纳块最近的边的偏移（因此才叫偏移属性）。例如，top 属性指定定位元素的上外边距边界距容纳块的顶边多远。对 top 属性来说，正值把定位元素的上外边距边界向下移动，而负值把上外边距边界移到容纳块的顶边上部。类似地，left 属性指定定位元素左外边距边界在容纳块左边的右侧（正值）或左侧（负值）的什么位置。正值把定位元素的外边距边界向右移动，负值把外边距边界向左移动。

换个说法就是，正值是内向偏移，把边界向容纳块的中心移动，负值则是外向偏移。

定位元素的外边距边界偏移后，元素的一切都随之移动，包括外边距、边框、内边距和内容，因此，定位元素也是可以设置外边距，边框和内边距的。这些区域在定位元素的过程中得以保留，而且都在偏移属性定义的范围内。

注意，偏移属性定义的是距容纳块相应边的偏移距离（例如，left 定义距左边的偏移）而不是距容纳左上角的距离。例如，若想让元素填充容纳块的右下角，要使用这些值：`top: 50%; bottom: 0; left: 50%; right: 0;`

在这个示例中，定位元素的左外边界在容纳块横向一半的位置。这是距容纳块左边界的偏移，然而，定位元素的右外边界与容纳块的右边界之间没有偏移，因此二者重合。这个定位元素的顶边和底边也是如此：上外边界在纵向一半的位置，而下外边界没有移动，结果如图 11-1 所示。

注意定位元素的背景区域。图 11-1 中的定位元素没有外边距，如果有的话，外边距边框和临移的各边之间生成一些空白。这样，定位元素看起来便没有完全填满容纳块的右下象限。事实上，右下象限会被填满，只是看似没有，因此，下面两组样式得到的结果看起来几乎是一样的（假设容纳块的高度为 100em、宽度为 100em）:

```css
#ex1 {
  top: 50%;
  bottom: 0;
  left: 50%;
  right: 0;
  margin: 10em;
}
#ex2 {
  top: 60%;
  bottom: 10%;
  left: 60%;
  right: 10%;
  margin: 0;
}
```

重申一下，只是看起来差不多而已。

使用负的偏移值可以把元素定位到容纳块的外部。例如，下述偏移值得到的结果如图 11-2 所示：

`top: 50%; bottom: -2em; left: 75%; right: -7em;`

<!-- <Figures figure="11-2">Positioning an element outside its containing block</Figures> -->

除了长度和百分数值以外，偏移属性还可以设为 auto,这是默认值。auto 的行为不定，根据定位类型而变。在逐一讲解各种定位类型时会探讨 auto 的具体行为。

## 11.3 宽度和高度

很多情况下，确定把元素定位在何处之后，可能还要声明元素的宽度和高度。有时你想自行限制定位元素的高度或宽度，还有一些情况下则交由浏览器自动计算宽度或高度。

### 11.3.1 设定宽度和高度

如果想为定位元素指定具体的宽度，使用 width 属性。类似地，使用 height 可以为定位元素指定具体的高度。

虽然有时必须为元素设定 width 和 height,但定位元素却不强制要求。例如，如果使 top、right、bottom 和 left 限定了元素四边的位置，height 和 width 的值便能从中推出，假设我们想让绝对定位的元素占满容纳块的左半边，可以使用下述偏移值，结果如图 11-3 所示：

`top: 0; bottom: 0; left: 0; right: 50%;`

<!-- <Figures figure="11-3">Positioning and sizing an element using only the offset properties</Figures> -->

因为 width 和 height 的默认值是 auto,所以图 11-3 与使用下述声明得到的结果是完全一样的：

`top: 0; bottom: 0; left: 0; right: 50%; width: 50%; height: 100%;`

这里添加的 width 和 height 属性对元素的布局没有任何影响。

然而，如果添加了内边距、边框或外边距，height 和 width 属性对结果的影响就大了：

`top: 0; bottom: 0; left: 0; right: 50%; width: 50%; height: 100%; padding: 2em;`

上述声明得到的结果是，定位元素超出容纳块的边界，如图 11-4 所示。

<!-- <Figures figure="11-4">Positioning an element partially outside its containing block</Figures> -->

这是因为，（默认情况下）内边距增加到内容区上，而内容区的尺寸由 height 和 width 属性的值确定。如果想要内边距，而且不让元素超出容纳块，可以删除 height 和 width 声明，或者把二者的值都设为 auto,此外还可以把 box-sizing 属性设为 border-box。

### 11.3.2 限制宽度和高度

如果有必要，或者自己主动想做，可以使用下述属性（以下称为极值属性）限制元素的宽度和高度。元素的内容区尺寸可以使用 min-width 和 min-height 定义最小值。

<!-- <Cards cards="min-width_min-height" /> -->

类似地，元素的尺寸可以使用 max-width 和 max-height 定义最大值。

<!-- <Cards cards="max-width_max-height" /> -->

这几个属性的名称已经表明其作用，无需过多解释。不过有一点不怎么明显，但是细想之后也合理，即这些属性的值都不能为负。

下述样式限制定位元素的宽度至少为 10em，高度至少为 20em，结果如图 11-5 所示。

`top: 10%; bottom: 20%; left: 50%; right: 10%; min-width: 10em; min-height: 20em;`

<!-- <Figures figure="11-5">Setting a minimum width and height for a positioned element</Figures> -->

但是这样限制太死了，不管容纳块有多大，都限制元素至少为一定的尺寸。下面这样声明更好一些:

`top: 10%; bottom: auto; left: 50%; right: 10%; height: auto; min-width: 15em;`

这里，我们把元素的宽度设为容纳块宽度的 40%，但是不能小于 15em。我们还修改了 bottom 和 height，自动确定二者的值。因此，元素的高度将根据内容自动调整，不管元素会变得多窄（当然不能小于 15em）。

我们可以换个方向，使用 max-width 和 max-height 避免元素变得太宽或太高。假如某种情况下，我们想让元素的宽度为容纳块宽度的四分之三，但是达到 400 像素后就不再继续变宽。恰当的样式如下：

`left: 0%; right: auto; width: 75%; max-width: 400px;`

极值属性的一大优势是，相对可以放心混用不同的单位。你可以使用百分数设定尺寸，然后使用长度限定极值，或者反过来。

值得一提的是，极值属性对浮动元素也有很大的用途。例如，可以相对父元素（即容纳块的宽度设定浮动元素的宽度，确保浮动元素的宽度绝不小于 10em。当然，反过来也可以：

```css
p.aside {
  float: left;
  width: 40em;
  max-width: 40%;
}
```

上述样式把浮动元素的宽度设为 40em,当然前提是不能超过容纳块宽度的 40%,因为大只能是容纳块宽度的 40%。

## 11.4 内容溢出和裁剪

如果内容太多，在元素中放不下，可能会从元素中溢出。这样的情况有几种处理方式，通过 CSS 可以选择其中一个。此外，还可以定义一个裁剪区，指明超出元素多大范围算溢出。

### 11.4.1 溢出

假设有个尺寸固定的元素（不深究原因），内容在里面放不下。这种情况使用 overflow 属性处理。

<!-- <Cards cards="overflow" /> -->

默认值 visible 的意思是，超出元素框的内容是可见的。通常，这会导致内容超出所在的元素框，但是对元素框的形状没有影响。下述样式得到的结果如图 11-6 所示。

```css
div#sidebar {
  position: absolute;
  top: 0;
  left: 0;
  width: 25%;
  height: 7em;
  background: #bbb;
  overflow: visible;
}
```

如果把 overflow 的值设为 scroll,元素的内容将在元素框的边界处裁剪（即隐藏），但是被裁减的内容依然有方法呈现给用户。在 Web 浏览器中，可能会出现一个滚动条（或几个滚动条），也可能是其他不改变元素形状的其他方法。其中一种可能如图 11-6 所示。

设为 scroll 时，平移机制（例如滚动条）应该始终渲染。根据规范，这样要求的原因是“避免动态环境下滚动条出现和消失时导致什么问题”。因此，即便元素的尺寸足够显示全部内容，滚动条也可能会出现，占据着一定的空间（不过也可能不会出现）。但是，打印网页时，或者在印刷媒介中显示文档时，可能会像 overflow 的值为 visible 那样显示内容。

如果把 overflow 的值设为 hidden,元素的内容将在元素框的边界处裁剪，而且超出裁剪区的内容无法通过滚动条等界面元素查看。此时，用户看不到被裁剪的内容。

<!-- <Figures figure="11-6">Three methods for handling overflowing content</Figures> -->

最后，还有 `overflow: auto`。这个值让用户代理自己决定使用哪种行为，不过建议在要时提供流动机制，使用 auto 处理溢出也不错，因为用户代理可能把这条建议解读为“在需要时提供滚动条”（可能不提供，但肯定可以提供，而且或许应该提供）。

## 11.5 元素的可见性

除了裁剪和溢出之外，还可以控制整个元素的可见性。

<!-- <Cards cards="visibility" /> -->

这个属性相当简单。如果设定 `visibility: visible`,与你所想的一样，元素是可见的。如果设定 `visibility: hidden`,元素“不可见”（invisible,规范用的就是这个词）。在不可见状态下，元素依然像可见时那样影响文档的布局。也就是说，元素还在那里，只是你看不见，就像声明 `opacity: 0` 一样。

注意这与 `display: none` 之间的区别。后者导致元素不显示，完全从文档中移除，因此对文档的布局不再有任何影响。下述样式和标记把段落中一部分的可见性设为 hidden,得到的结果如图 11-7 所示

```css
em.trans {
  visibility: hidden;
  border: 3px solid gray;
  background: silver;
  margin: 2em;
  padding: 1em;
}
```

```html
<p>
  This is a paragraph which should be visible. Nulla berea consuetudium ohio
  city, mutationem dolore.
  <em class="trans">Humanitatis molly shannon ut lorem.</em> Doug dieken dolor
  possim south euclid.
</p>
```

<!-- <Figures figure="11-7">Making elements invisible without suppressing their element boxes</Figures> -->

隐藏元素的可见部分，例如内容、背景和边框，都变得不可见了。但是占据的空间依然在那里，因为不可见的元素还是文档布局的一部分，只是我们看不到罢了。

可见性为 hidden 的元素，其后代元素可以设为 visible,尽管祖辈元素不可见了，但是后代元素将出现在常规位置。为此，我们要把后代元素的可见性明确声明为 visible 因为 visibility 属性是继承的：

```css
p.clear {
  visibility: hidden;
}
p.clear em {
  visibility: visible;
}
```

`visbility: collapse` 在渲染表格时使用，本节暂不讨论，根据规范，collapse 与非表格元素上的 hidden 具有相同的作用。

## 11.6 绝对定位

前面几节中的示例和插图大都使用绝对定位，我想你应该对此有一定的了解了，尚未提的只是一些细节。

### 11.6.1 绝对定位元素的容纳块

绝对定位的元素完全从文档流中移除，其位置相对容纳块确定，外边距的边界使用偏移属性（top、left 等）划定，绝对定位的元素不围绕其他元素的内容流动，而且其内也不围绕定位元素流动，这表明，绝对定位的元素可能会叠放到其他元素上，或者被其他元素覆盖（稍后说明如何控制叠放顺序）。

绝对定位元素的容纳块是 position 属性的值不是 static 的最近的祖辈元素。通常，创作人员选定用作绝对定位元素的容纳块的元素后，会把 position 的值设为 relative 而且不设置偏移，如下所示：

```css
.contain {
  position: relative;
}
```

考虑图 11-8 中的例子，它演示了以下内容:

```css
p {
  margin: 2em;
}
p.contain {
  position: relative;
} /* establish a containing block*/
b {
  position: absolute;
  top: auto;
  right: 0;
  bottom: 0;
  left: auto;
  width: 8em;
  height: 5em;
  border: 1px solid gray;
}
```

```html
<body>
  <p>
    This paragraph does <em>not</em> establish a containing block for any of its
    descendant elements that are absolutely positioned. Therefore, the
    absolutely positioned <b>boldface</b> element it contains will be positioned
    with respect to the initial containing block.
  </p>
  <p class="contain">
    Thanks to <code>position: relative</code>, this paragraph establishes a
    containing block for any of its descendant elements that are absolutely
    positioned. Since there is such an element--
    <em
      >that is to say,
      <b>a boldfaced element that is absolutely positioned,</b> placed with
      respect to its containing block (the paragraph)</em
    >, it will appear within the element box generated by the paragraph.
  </p>
</body>
```

两个段落中的 b 元素都是绝对定位的，只是所用的容纳块不同。第一个段落中的 b 元素相对初始容纳块定位，因为它的所有祖辈元素的 position 值都是 static。第二个段落设置了 position:relative,因此它变成后代元素的容纳块。

<!-- <Figures figure="11-8">Using relative positioning to define containing blocks</Figures> -->

你可能注意到了，第二段中的定位元素与段落中的文本有些重叠。这是不可避免的，除非把 b 元素定位到段落外部（把 right 或其他偏移属性设为负值）,或者为段落设定是够宽的内边距，留出空间放置定位的元素。此外，因为 b 元素的背景是透明的，所以透过这个定位元素能看到段落中的文本。如果不希望如此，只能为定位元素设置背景，或者完全移到段落外部。

有时你可能想确保 body 元素是所有后代元素的容纳块，而不让用户代理自行选择初始容纳块。这很简单，只需像下面这样声明：

```css
body {
  position: relative;
}
```

在这样的文档中，如果有下面这个绝对定位的段落，得到的结果将是图 11-9 那样。

```html
<p
  style="position: absolute; top: 0; right: 25%; left: 25%; bottom:
 auto; width: 50%; height: auto; background: silver;"
>
  ...
</p>
```

这个段落定位在文档开头，宽度是文档宽度的一半，而且覆盖了其他内容。

<!-- <Figures figure="11-9">Positioning an element whose containing block is the root element</Figures> -->

需要着重说明的一点是，绝对定位的元素是其后代元素的容纳块。例如，我们可以定位一个元素，然后再绝对定位它的子元素。下述样式和标记得到的结果如图 11-10 所示。

```css
div {
  position: relative;
  width: 100%;
  height: 10em;
  border: 1px solid;
  background: #eee;
}
div.a {
  position: absolute;
  top: 0;
  right: 0;
  width: 15em;
  height: 100%;
  margin-left: auto;
  background: #ccc;
}
div.b {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 10em;
  height: 50%;
  margin-top: auto;
  background: #aaa;
}
```

```html
<div>
  <div class="a">
    absolutely positioned element A
    <div class="b">
      absolutely positioned element B
    </div>
  </div>
  containing block
</div>
```

注意，如果文档能滚动，绝对定位的元素将随之滚动。只要绝对定位的元素不是固定定位或粘滞定位元素的后代，都是这样。

之所以如此，是因为元素最终必将相对正常文档流中的某个元素定位。例如，如果绝对定位一个表格，而表格的容纳块是初始容纳块，那么它将滚动，这是因为初始容纳块是正常文档流中的一部分，所以会随之滚动。

如果希望元素相对视区定位，而且不随文档一起滚动，请继续往下读。下一节讨论固定定位时将说明。

<!-- <Figures figure="11-10">Absolutely positioned elements establish containing blocks</Figures> -->

### 11.6.2 绝对定位元素的位置和尺寸

把位置和尺寸放在一起讲看起来有点奇怪，但是对绝对定位的元素来说必须这么做，因为规范就把二者紧密联系在一起。其实，仔细一想，位置和尺寸之间也不是没有联系。试想，如果使用四个偏移属性定位元素，将得到什么结果，如下所示：

```css
#masthead h1 {
  position: absolute;
  top: 1em;
  left: 1em;
  right: 25%;
  bottom: 10px;
  margin: 0;
  padding: 0;
  background: silver;
}
```

这样，h1 元素框的高度和宽度由其外边距边界的位置决定，如图 11-11 所示。

<!-- <Figures figure="11-11">Determining the height of an element based on the offset properties</Figures> -->

如果容纳块更高一些，h1 的高度也会变大；如果容纳块变窄，h1 也会窄一些。如果为 h1 设置了外边距或内边距，h1 的高度和宽度将进一步受到影响。

但如果我们做了所有这些，然后还试图设置一个显式的高度和宽度呢?

```css
#masthead h1 {
  position: absolute;
  top: 0;
  left: 1em;
  right: 10%;
  bottom: 0;
  margin: 0;
  padding: 0;
  height: 1em;
  width: 50%;
  background: silver;
}
```

有些值必然将被忽略，因为不可能每个值都是准确的。其实，如果上述所有值都是准确的，容纳块的宽度必须正好是根据 font-size 计算出的 h1 元素宽度的 2.5 倍。一旦 width 不是这个值，说明至少有一个值是错的，将被忽略。具体忽略哪个值受很多因素的影响，而且对置换元素和非置换元素来说，因素还不一样。

鉴于此，来看下述样式：

```css
#masthead h1 {
  position: absolute;
  top: auto;
  left: auto;
}
```

这将得到怎样的结果呢？可以想见，肯定不是“把值重置为零”这么简单。从下一节开始，我们将讨论具体结果。

### 11.6.3 自顶确定边界的位置

绝对定位一个元素时，如果除 bottom 之外的某个偏移属性被设为 auto,将得到一种特殊的行为。以 top 为例。请看下述代码：

```html
<p>
  When we consider the effect of positioning, it quickly becomes clear that
  authors can do a great deal of damage to layout, just as they can do very
  interesting things.<span
    style="position: absolute; top: auto;
 left: 0;"
    >[4]</span
  >
  This is usually the case with useful technologies: the sword always has at
  least two edges, both of them sharp.
</p>
```

结果如何呢？左边界好确定，将与容纳块（假设为初始容纳块）的左边界重合。然而，顶边的位置却不那么容易确定。这里，定位元素的顶边将与没有定位时的顶边位置对齐。也就是说，要先确定 position 属性的值是 static 时，span 在什么位置（即静态位置）然后据此计算定位后顶边的位置。关于静态位置，CSS2.1 是这么说的：

> (元素的）“静态位置”基本上指的是元素在常规文档流中的位置。更准确地说是，静态位置的 top 值是容纳块的顶边距一个假想框体上外边距边界的距离。这个假想的框体是元素的第一个框体，而且它的 postion 值为 static、float 的值为 none,clear 的值为 none……如果假想的框体在容纳块上方，值为负。

因此，得到的结果如图 11-12 所示。

<!-- <Figures figure="11-12">Absolutely positioning an element consistently with its “static” top edge</Figures> -->

“[4]”在段落内容的外部，这是因为初始容纳块的左边界在段落左边界的左侧。

left 和 right 设为 auto 时也是如此，定位元素的左（或右）边界与元素未定位时左（s)右）边界所在的位置对齐。下面在前例的基础上，把 top 和 left 的值都设为 auto:

```html
<p>
  When we consider the effect of positioning, it quickly becomes clear that
  authors can do a great deal of damage to layout, just as they can do very
  interesting things.<span
    style="position: absolute; top: auto; left:
 auto;"
    >[4]</span
  >
  This is usually the case with useful technologies: the sword always has at
  least two edges, both of them sharp.
</p>
```

得到的结果如图 11-13 所示。

<!-- <Figures figure="11-13">Absolutely positioning an element consistently with its “static” position</Figures> -->

现在“[4]”所处的位置与未定位前一样。注意，因为已经做了定位，所以它在常规文流中的位置被收回了。因而，定位后的元素与常规文档流中的内容有重叠。

这种自动确定位置的机制只在特定情况下才起作用，一般来说只要对定位元素的其他尺寸没有太多限制，都会使用这个机制。前例之所以能自动确定位置，是因为没有限制元素的高度或宽度，也没有限定下边界和右边界的位置。但是，有时会对此作出限制，例如：

```html
<p>
  When we consider the effect of positioning, it quickly becomes clear that
  authors can do a great deal of damage to layout, just as they can do very
  interesting things.<span
    style="position: absolute; top: auto; left: auto;
 right: 0; bottom: 0; height: 2em; width: 5em;"
    >[4]</span
  >
  This is usually the case with useful technologies: the sword always has at
  least two edges, both of them sharp.
</p>
```

这些值不可能同时满足，具体如何处理，参见下一节。

### 11.6.4 非置换元素的位置和尺寸

一般来说，元素的尺寸和位置取决于容纳块。不同的属性（width、right、padding-left 等）对元素的布局会产生一定的影响，但是最根本的影响来自容纳块。

以定位元素的宽度和横向位置为例。二者要满足下述等式：

```
left + margin-left + border-left-width + padding-left + width +
padding-right + border-right-width + margin-right + right =
the width of the containing block
```

这样计算是比较合理的。这个等式基本上与计算常规文档流中块级元素尺寸的等式一样，不过多了 left 和 right。那么，各属性之间是如何互相影响的呢？这涉及一系列规则。

首先，如果 left、width 和 right 都设为 auto,得到的结果与前一节见到的一样：在从左至右的书写语言中，左边界放在静态位置；在从右至左的书写语言中，右边界放在静态位置。元素的宽度设为“自动缩放”，因此元素内容区的宽度将恰好能放得下内容。非静态定位属性（从左至右语言中的 right,从右至左语言中的 left)设为 auto 的意思是占据余下的距离。例如：

```html
<div style="position: relative; width: 25em; border: 1px dotted;">
  An absolutely positioned element can have its content
  <span
    style="position:
Absolute Positioning | 543
 absolute; top: 0; left: 0; right: auto; width: auto; background:
 silver;"
    >shrink-wrapped</span
  >
  thanks to the way positioning rules work.
</div>
```

得到的结果如图 11-14 所示。

<!-- <Figures figure="11-14">The “shrink-to-fit” behavior of absolutely positioned elements</Figures> -->

这里，元素的顶边与容纳块（div 元素）的顶边重合，而元素的宽度正好能放得下内容。元素右边界到容纳块右边界之间的距离都变成 right 的计算值。

现在在只把左右外边更设为 auto,left、width 和 right 都不设为 auto,如下所示；

```html
<div style="position: relative; width: 25em; border: 1px dotted;">
  An absolutely positioned element can have its content
  <span
    style="position:
 absolute; top: 0; left: 1em; right: 1em; width: 10em; margin: 0 auto;
 background: silver;"
    >shrink-wrapped</span
  >
  thanks to the way positioning rules work.
</div>
```

因为左右外边更的值都是 auto,所以二者的计算值相等。这样得到的结果是，元素居体显示，如图 11-15 所示。

<!-- <Figures figure="11-15">Horizontally centering an absolutely positioned element with auto margins</Figures> -->

这与在常规文档流中把外边距设为 auto 居中显示元素的原理基本一样。下面把外边的值由 auto 改为其他值：

```html
<div style="position: relative; width: 25em; border: 1px dotted;">
  An absolutely positioned element can have its content
  <span
    style="position:
 absolute; top: 0; left: 1em; right: 1em; width: 10em; margin-left: 1em;
 margin-right: 1em; background: silver;"
    >shrink-wrapped</span
  >
  thanks to the way positioning rules work.
</div>
```

问题出现了。我们定位的 span 元素，各个属性的值加在一起只有 14em,而容纳块的宽度是 25em,二者相差 1lem,这是我们要找补的。

根据规则，在这种情况下，用户代理将忽略为 right 属性（针对从左向右书写的语言；反之忽略的是 left 属性）声明的值，补上差值。也就是说，结果与下述声明是一样的：(span stylee"position: a

```html
<span
  style="position: absolute; top: 0; left: 1em;
right: 12em; width: 10em; margin-left: 1em; margin-right: 1em;
right: auto; background: silver;"
  >shrink-wrapped</span
>
```

得到的结果如图 11-16 所示。

<!-- <Figures figure="11-16">Ignoring the value for right in an overconstrained situation</Figures> -->

如果其中一边的外边距是 auto,情况就不同了，假如把样式改成下面这样：

```html
<span
  style="position: absolute; top: 0; left: 1em;
right: 1em; width: 10em; margin-left: 1em; margin-right: auto;
background: silver;"
  >shrink-wrapped</span
>
```

此时，得到的结果看起来与图 11-16 一样，只不过计算得到的右外边距是 12em,right 属性的值不再被覆盖。

如果设为 auto 的是左外边距，右外边距的值将被重置，如图 11-17 所示。

```html
<span
  style="position: absolute; top: 0; left: 1em;
right: 1em; width: 10em; margin-left: auto; margin-right: 1em;
background: silver;"
  >shrink-wrapped</span
>
```

<!-- <Figures figure="11-17">Ignoring the value for margin-right in an overconstrained situation</Figures> -->

一般来说，如果只有一个属性的值是 auto,将通过那个属性补足本节前面给出的等式。因此，对下述样式来说，元素的宽度将延伸为所需的大小，而不会“折弯”内容：

```html
<span
  style="position: absolute; top: 0; left: 1em;
right: 1em; width: auto; margin-left: 1em; margin-right: 1em;
background: silver;"
  >not shrink-wrapped</span
>
```

目前讨论的都是横轴上的行为，不过纵轴所用的规则与之十分相似。如果把前面所讲规则旋转 90 度，行为基本上是一样的。例如，下述标记得到的结果如图 11-18 所示：

```html
<div style="position: relative; width: 30em; height: 10em; border: 1px solid;">
  <div
    style="position: absolute; left: 0; width: 30%;
 background: #CCC; top: 0;"
  >
    element A
  </div>
  <div
    style="position: absolute; left: 35%; width: 30%;
 background: #AAA; top: 0; height: 50%;"
  >
    element B
  </div>
  <div
    style="position: absolute; left: 70%; width: 30%;
 background: #CCC; height: 50%; bottom: 0;"
  >
    element C
  </div>
</div>
```

在第一种情况下，元素的高度正好放得下内容。在第二种情况下，未指定的属性（bottom)占据定位元素底边与容纳块底边之间的距离。在第三种情况下，top 未指定，因此用补足差值。

<!-- <Figures figure="11-18">Vertical layout behavior for absolutely positioned elements</Figures> -->

鉴于此，外边距为 auto 时，元素将纵向居中显示。对下述样式来说，绝对定位的 din 元素将在容纳块中纵向居中显示，如图 11-19 所示：

```html
<div style="position: relative; width: 10em; height: 10em; border: 1px solid;">
  <div
    style="position: absolute; left: 0; width: 100%; background: #CCC;
 top: 0; height: 5em; bottom: 0; margin: auto 0;"
  >
    element D
  </div>
</div>
```

有两点细微差别要指出。在横向布局中，如果 right 或 left 的值为 auto,左右边界的位置根据静态位置确定。而在纵向布局中，只有 top 根据静态位置确定：bottom 在任何情况下都不这样确定。

此外，如果绝对定位元素的纵向尺寸过约束了，bottom 的值将被忽略。因此，在下述标记中，bottom 声明的值将被计算得到的 5em 覆盖：

```html
<div style="position: relative; width: 10em; height: 10em; border: 1px solid;">
  <div
    style="position: absolute; left: 0; width: 100%; background: #CCC;
 top: 0; height: 5em; bottom: 0; margin: 0;"
  >
    element D
  </div>
</div>
```

如果属性的值导致过约束，top 永远不会被忽略。

<!-- <Figures figure="11-19">Vertically centering an absolutely positioned element with auto-margins</Figures> -->

### 11.6.5 置换元素的位置和尺寸

置换元素（例如图像）的定位规则与非置换元素不同。这是因为置换元素有内在的高和宽度，除非由创作人员人为修改，否则不会变。因此，对定位的置换元素来说，没有动缩放”这一说。

置换元素的位置和尺寸由下述规则按顺序确定。

1. 如果把 Midth 设为 auto,width 的具体值由元素内容的内在党度明足。因此，如果图像自身的宽度是 50 像素，那么计算得到的值是 sopx。如果明确声明了 width(所如 100px 或 50%),那就使用设定的值。
2. 在从左至右书写的语言中，如果 1eft 的值是 auto,auto 将替换为静态位置。在从右至左书写的语言中，right 属性的 auto 值将被者换为静态位置。
3. 如果 1eft 或 right 的值仍是 auto(也就是说，在前一步中没有被替换）,把 margin-left 或 margin-right 的 auto 值替换为 0.
4. 如果此时 margin-left 和 margin-right 的值仍为 auto,把二者设为相等的值，an 让元素居中显示在容纳块中。
5. 最后，如果还有一个属性的值为 auto,修改为满足等式所需的值。

这与明确为非置换元素设置 width 属性的行为基本一样。因此，假如图像自身的宽度是 100 像素，那么下述两个元素的宽度和位置都是一样的（见图 11-20):

```html
<div>
  <img
    src="frown.gif"
    alt="a frowny face"
    style="position: absolute; top: 0; left: 50px; margin: 0;"
  />
</div>
<div
  style="position: absolute; top: 0; left: 50px;
 width: 100px; height: 100px; margin: 0;"
>
  it's a div!
</div>
```

<!-- <Figures figure="11-20">Absolutely positioning a replaced element</Figures> -->

与非置换元素一样，如果导致过约束，用户代理将忽略 right(从左至右书写的语言）或 left(从右至左书写的语言）的值。因此，在下述示例中，为 right 声明的值将被计算得到的 50px 覆盖：

```html
<div style="position: relative; width: 300px;">
  <img
    src="frown.gif"
    alt="a frowny face"
    style="position: absolute; top: 0;
 left: 50px; right: 125px; width: 200px; margin: 0;"
  />
</div>
```

类似地，纵轴布局由下述规则控制：

1. 如果把 height 设为 auto,height 的具体值由元素内容的内在高度确定。因此，如果图像自身的高度是 50 像素，那么计算得到的值是 50px。如果明确声明了 height(例如 100px 或 50%),那就使用设定的值。
2. 如果 top 的值是 auto,替换为置换元素的静态位置。
3. 如果 bottom 的值是 auto,把值为 auto 的 margin-top 或 margin-bottom 替换为 0.
4. 如果此时 margin-top 和 margin-bottom 的值仍为 auto,把二者设为相等的值，即让元素居中显示在容纳块中。
5. 最后，如果还有一个属性的值为 auto,修改为满足等式所需的值。

与非置换元素一样，如果过约束了，用户代理将忽略 bottom 的值。

因此，下述标记将得到如图 11-21 所示的结果：

```html
<div
  style="position: relative; height: 200px; width: 200px; border: 1px solid;"
>
  <img
    src="one.gif"
    alt="one"
    width="25"
    height="25"
    style="position: absolute; top: 0; left: 0; margin: 0;"
  />
  <img
    src="two.gif"
    alt="two"
    width="25"
    height="25"
    style="position: absolute; top: 0; left: 60px; margin: 10px 0;
 bottom: 4377px;"
  />
  <img
    src="three.gif"
    alt=" three"
    width="25"
    height="25"
    style="position: absolute; left: 0; width: 100px; margin: 10px;
 bottom: 0;"
  />
  <img
    src="four.gif"
    alt=" four"
    width="25"
    height="25"
    style="position: absolute; top: 0; height: 100px; right: 0;
 width: 50px;"
  />
  <img
    src="five.gif"
    alt="five"
    width="25"
    height="25"
    style="position: absolute; top: 0; left: 0; bottom: 0; right: 0;
 margin: auto;"
  />
</div>
```

<!-- <Figures figure="11-21">Stretching replaced elements through positioning</Figures> -->

### 11.6.6 Z 轴上的位置

了解这么多定位知识之后，可以想见的是，终有那么一个时刻，两个元素会出现在相同的位置，当然这指的是视觉上的效果。相同位置上的元素将重叠在一起，那么如何控制哪个元素在“上面”呢？答案是使用 z-index 属性。

z-index 用于调整元素之间重叠的方式。这个属性的名称源自坐标系，其中从左到右是 x 轴，从上到下是 y 轴：第三个轴，即由后到前，像是从你面前的纸张射出来的一样，称为 z 轴。因此，为元素设置的 z-index 值就在这个轴上。这个坐标系如图 11-22 所示。

<!-- <Cards cards="z-index" /> -->

<!-- <Figures figure="11-22">A conceptual view of z-index stacking</Figures> -->

在这个坐标系统中，z-index 的值越大，元素离读者的距离越近。因此，值大的元素可能会遮盖其他元素，如图 11-23 所示（这是图 11-22 的正视图）。叠放的优先级称为堆叠次序（stacking).

<!-- <Figures figure="11-23">How the elements are stacked</Figures> -->

z-index 的值可以设为任何整数，包括负数。z-index 的值为负数时，元素远离读者；在堆叠次序中更靠下。下述样式得到的结果如图 11-24 所示：

```css
p {
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid;
}
p#first {
  position: absolute;
  top: 0;
  left: 0;
  width: 40%;
  height: 10em;
  z-index: 8;
}
p#second {
  position: absolute;
  top: -0.75em;
  left: 15%;
  width: 60%;
  height: 5.5em;
  z-index: 4;
}
p#third {
  position: absolute;
  top: 23%;
  left: 25%;
  width: 30%;
  height: 10em;
  z-index: 1;
}
p#fourth {
  position: absolute;
  top: 10%;
  left: 10%;
  width: 80%;
  height: 10em;
  z-index: 0;
}
```

这几个元素根据相应的样式定位，但是常规的堆叠次序被 z-index 的值调整了。假设各段落是按顺序排列的，正常情况下，从下到上的顺序应该是 p#first、p#second、pethird,pafourth,即，pifirst 在其他三个元素后面，而 p#fourth 在其他元素前面。有了 z-index,我们便能自由掌控堆叠次序。

<Figures figure="11-24">Stacked elements can overlap</Figures>

如前例所示，z-index 的值无需连续，想使用多大的整数都可以。如果想确保某个元素一般都显示在其他内容前面，可以在规则中加上 z-index:100000。多数情况下，这样做能得到预期的结果。但是如果你把另一个元素的 z-index 声明为 100001(或更大的数）,那么它将显示在最前面。

正如前面的示例所演示的，没有必要特别要求' z-index '值是连续的。您可以分配任何大小的任何整数。如果您想确保某个元素始终位于其他元素之前，可以使用“z-index: 100000”这样的规则。在大多数情况下，这将与预期一样工作—尽管如果您曾经将另一个元素的' z-index '声明为' 100001 '(或更高)，它将出现在前面。

为元素设定 z-index 后（值不为 auto),元素便确立了自己的局部堆叠上下文。这意味着，所有后代元素的堆叠次序都相对祖辈元素而言。这与元素确立新的容纳块十分相似。下述样式将得到如图 11-25 所示的结果：

```css
p {
  border: 1px solid;
  background: #ddd;
  margin: 0;
}
#one {
  position: absolute;
  top: 1em;
  left: 0;
  width: 40%;
  height: 10em;
  z-index: 3;
}
#two {
  position: absolute;
  top: -0.75em;
  left: 15%;
  width: 60%;
  height: 5.5em;
  z-index: 10;
}
#three {
  position: absolute;
  top: 10%;
  left: 30%;
  width: 30%;
  height: 10em;
  z-index: 8;
}
p[id] em {
  position: absolute;
  top: -1em;
  left: -1em;
  width: 10em;
  height: 5em;
}
#one em {
  z-index: 100;
  background: hsla(0, 50%, 70%, 0.9);
}
#two em {
  z-index: 10;
  background: hsla(120, 50%, 70%, 0.9);
}
#three em {
  z-index: -343;
  background: hsla(240, 50%, 70%, 0.9);
}
```

<!-- <Figures figure="11-25">Positioned elements establish local stacking contexts</Figures> -->

注意各 em 元素的性量次序，它们都相对父元素确定自己在布局中的位置。不管 em 元来的 z-index 值是正是负，都显示在父元素前面。父元素和子元素是组合在一起的，像图像编辑程序中的图层一样（根据规范，使用 z-index 设置堆叠次序时，子元素不能在父元素背后绘割，因此在 p#three 中，虽然 em 的 z-index 值为-343,但是依然在 pone 之上给制）。元素的 z-index 值相对局部堆叠上下文，即容纳块。而容纳块也 z-index,也在局部堆叠上下文中处理。

z-index 还有一个值需要说明。CSS 规范是这样规定默认值 auto 的：

> 生成的框体在当前堆叠上下文中的堆叠次序是 0。如果不是根元素，不确立新的堆叠上下文。

因此，z-index:auto 可以视作 z-index:0。

> 尽管弹性布局和棚格布局中的元素不使用 position 属性定位，但是它们也受 z-index 的控制，相关的规则本质上是一样的。

## 11.7 固定定位

前一节暗示过，固定定位与绝对定位类似，只不过固定定位元素的容纳块是视区。固定定位的元素完全从文档流中移除，其位置与文档中的任何一部分都没关系。

利用固定定位可以实现很多有趣的效果。首先，可以使用固定定位实现框架式界面。以图 11-26 为例，这是一种十分常见的布局方式。

<!-- <Figures figure="11-26">Emulating frames with fixed positioning</Figures> -->

这个布局可以使用下述样式实现：

```css
div#header {
  position: fixed;
  top: 0;
  bottom: 80%;
  left: 20%;
  right: 0;
  background: gray;
}
div#sidebar {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 80%;
  background: silver;
}
```

这段样式把页头固定在视区顶部，把侧边栏固定在视区一侧，不论如何滚动文档，位始终不变。然而，这样做的后果是，文档的其他部分会被这些固定元素遮盖。因此，余下的内容或许应该放在一个 div 容器中，并应用下述样式：

```css
div#main {
  position: absolute;
  top: 20%;
  bottom: 0;
  left: 20%;
  right: 0;
  overflow: scroll;
  background: white;
}
```

为这三个定位的 div 元素添加适当的外边距可以增加一点间隙，例如：

```css
body {
  background: black;
  color: silver;
} /* colors for safety's sake */
div#header {
  position: fixed;
  top: 0;
  bottom: 80%;
  left: 20%;
  right: 0;
  background: gray;
  margin-bottom: 2px;
  color: yellow;
}
div#sidebar {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 80%;
  background: silver;
  margin-right: 2px;
  color: maroon;
}
div#main {
  position: absolute;
  top: 20%;
  bottom: 0;
  left: 20%;
  right: 0;
  overflow: auto;
  background: white;
  color: black;
}
```

此时，可以为 body 元素添加平铺的背景图。背景图透过外边距创建的间除能看到，如果创作人员觉得合适，当然还可以增大间隙。

利用固定定位还可以在界面中放一个始终可见的元素，例如一个小的链接列表。我们可以像下面这样创建一个始终可见的页脚，显示版权等信息：

```css
footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  height: auto;
}
```

这个样式把 footer 元素放在视区的底部，不管如何滚动文档，始终显示在那里。

> 除了始终可见的元素之外，其他很多通过固定定位实现的效果都能使用研格布局（译情参见第 13 章）实现，而且有时可能更方便。

## 11.8 相对定位

最容易理解的定位方式是相对定位。相对定位使用偏移属性移动元素。然而，这可能带来一些有趣的后果。

表面上看，这种定位方式确实简单。假如我们想把一个图像向上和向左移动一些距离，使用下述样式将得到如图 11-27 所示的结果。

```css
img {
  position: relative;
  top: -20px;
  left: -20px;
}
```

<!-- <Figures figure="11-27">A relatively positioned element</Figures> -->

这里，我们把图像的上边界向上移动 20 像素，把左边界向左移动 20 像素。然而请注意，图像原本所在的位置出现了空白。这是因为，在相对定位中，元素从常规的位置移开了，但是其占据的空间并没有消失。来看下述样式，得到的结果如图 11-28 所示：

```css
em {
  position: relative;
  top: 10em;
  color: red;
}
```

<!-- <Figures figure="11-28">Another relatively positioned element</Figures> -->

可以看到，段落中有一些空白，这是 em 元素原本占据的空间，而且新位置上的 em 元素与原位置的布局方式完全一样。

相对定位的元素还可能与其他元素重叠。例如，下述样式和标记得到的结果如图 11-29 所示

```css
img.slide {
  position: relative;
  left: 30px;
}
```

```html
<p>
  the right. It will therefor
  <img src="star.gif" alt="A ar!" class="slide" /> overlap content nearby,
  assuming that it is not the last element in its line box.
</p>
```

<Figures figure="11-29">Relatively positioned elements can overlap other content</Figures>

相对定位有个有意思的小问题，试想，如果相对定位的元素过约束了会怎样？例如：

```css
strong {
  position: relative;
  top: 10px;
  bottom: 20px;
}
```

这里提供的两个值可能得到差别很大的结果。如果只考虑 top:10px,元素将向下移动 10 像素，但是 botto:20px 是然会应用到元素上，把元素向上移动 20 像素。

CSS2 规范没有明确规定如何处理这种情况。但是 CSS2.1 规定，如果相对定位出现过约来，把其中一个值没为另一个值的相反数。因此，bottom 始终等于-top。这意味着，上例将被视作：

```css
strong {
  position: relative;
  top: 10px;
  bottom: -10px;
}
```

因此，strong 元素将向下移动 10 像素，规范还考虑到了书写方向。对相对定位来说，在从左至右书写的语言中，right 始终等于·left;在从右至左书写的语言中，反过来 left 始终等于-right.

## 11.9 粘滞定位

css 新增了一种定位方式：粘滞定位。如果你在移动设备上用过优秀的音乐应用，或许记得这样的操作：滚动浏览按字母顺序排列的艺人时，当前字母始终停留在窗口的顶部直到进入一个新的字母，新字母取而代之，显示在窗口顶部。在纸上很难展示这种效果，不过图 11-30 展示了滚动过程中的三个瞬间，希望能让你明白。

<Figures figure="11-30">Sticky positioning</Figures>

CSS 通过将一个元素声明为' position: sticky '来实现这种功能，但是(通常)它还有更多的功能。
使用 CSS 便能实现这种效果，为元素声明 position:sticky 即可，但是（一如往常）情况没有这么简单。

首先，偏移属性（top、left 等）用于定义相对容纳块的粘滞定位矩形。以下述样式为例，得到的结果如图 11-31 所示。图中的虚线是粘滞定位矩形。

```css
#scrollbox {
  overflow: scroll;
  width: 15em;
  height: 18em;
}
#scrollbox h2 {
  position: sticky;
  top: 2em;
  bottom: auto;
  left: auto;
  right: auto;
}
```

<!-- <Figures figure="11-31">The sticky-positioning rectangle</Figures> -->

注意，图 11.31 中的加元素其实在更形的中间。这是常规文本流中 h2 在包含内容的位置。若想把 h2 粘滞在顶部，要浪动内容，让 h2 的顶边接触粘滞定位矩形的顶边，h2 就粘滞在哪里。这个过程如图 11-32 所示。

<!-- <Figures figure="11-32">Sticking to the top of the sticky-positioning rectangle</Figures> -->

也就是说，在 h2 的粘游边界与矩形的粘滞边界接触之前，h2 一直在常规文档流中。当两个边界接触时，h2 粘滞在那里，就像是绝对定位了一样，不过 h2 在常规文档流中占据的空间会保留下来。

你可能注意到了，scrollbox 元素没有声明 position 属性。而且我们也没做什么其他设置，只是使用 overflow:scroll 为粘滞定位的 h2 元素创建一个容纳块。这是不使用 position 创建容纳块的一例。

如果向相反的方向滚动，把 h2 在常规文档流中的位置移到矩形顶边以下，h2 将与矩形分离，回到原本在常规文档流中的位置。这个过程如图 11-33 所示。

<!-- <Figures figure="11-33">Detaching from the top of the sticky-positioning rectangle</Figures> -->

注意，h2 之所以粘滞在矩形的顶部，是因为我们把 h2(即粘滞定位的元素）的 top 性设为了 auto 以外的其他值。你可以使用任何一个偏移边。例如，可以在向下滚动内容的过程中把元素粘滞在矩形的底部，如图 11-34 所示。

```css
#scrollbox {
  overflow: scroll;
  position: relative;
  width: 15em;
  height: 10em;
}
#scrollbox h2 {
  position: sticky;
  top: auto;
  bottom: 0;
  left: auto;
  right: auto;
}
```

<!-- <Figures figure="11-34">Sticking to the bottom of the sticky-positioning rectangle</Figures> -->

可以利用这一点显示某个段落的脚注或评论，当流动超过那个段落时，粘滞的脚注或评论将上移。这些规则也适用于左右两边，在横向滚动内容时用得到。

如果定义多个偏移属性，而且值都不是 auto,那么各边都将变成粘滞边界。例如，下述样式把 h2 限制在滚动框中，无论内容如何滚动，都不超出（见图 11-35):

```css
#scrollbox {
  overflow: scroll;
  :15em ;
  height: 10em;
}
#scrollbox h2 {
  position: sticky;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
```

<!-- <Figures figure="11-35">Making every side a sticky side</Figures> -->

你可能会间，如果流动到某一位置触发了多个粘滞定位的元素会得到什么结果？答案是，多个粘滞定位的元素将堆在一起。

```css
#scrollbox {
  overflow: scroll;
  width: 15em;
  height: 18em;
}
#scrollbox h2 {
  position: sticky;
  top: 0;
  width: 40%;
}
h2#h01 {
  margin-right: 60%;
  background: hsla(0, 100%, 50%, 0.75);
}
h2#h02 {
  margin-left: 60%;
  background: hsla(120, 100%, 50%, 0.75);
}
h2#h03 {
  margin-left: auto;
  margin-right: auto;
  background: hsla(240, 100%, 50%, 0.75);
}
```

这几个标题将堆在一起，在源文件中靠后的标题离观看的人更近，不过在图 11-36 这样的静态图像中不那么容易看清楚。这就是 z-index 的常规行为，因此你可以明确设置 2-index,决定哪个粘滞元素显示在其他粘滞元素之上。假如我们想让第一个粘滞元素显示在其他所有粘滞元素之上。此时，声明 z-index:1000,或者其他足够大的值便可以让第一个粘滞元素显示在同一位置上的其他所有粘滞元素之上。得到的效果看起来是其他元素“滑入”最顶层的元素背后一样。

<!-- <Figures figure="11-36">A sticky-header pileup</Figures> -->

## 11.10 小结

借助定位可以随意移动元素，这是常规文档流难以企及的。虽然很多定位技巧终将被栅格布局取代，但是定位仍有大量用途，例如让侧边栏始终显示在视区中，或者粘滞显示列表或长文中的小节标题。通过 z 轴确定叠放次序，加上各种溢出模式，定位依旧有其用武之地。

# 第 12 章 弹性盒布局

CSS Flexible Box Module Level 1（简称 [Flexbox](https://www.w3.org/TR/css-flexbox-1/)，弹性盒）把以往间距的布局人物变得极为简单，例如很多类型的页面、小组件、应用和图库。

## 12.1 弹性盒基础

弹性盒是一种简单而强大的布局方式，我们通过弹性盒指明空间的分布方式、内容纳对齐方式和元素的视觉顺序，把不同的组件放置在页面中。内容可以轻易横向或纵向排布，还可以沿一个轴布局，或者折断成多行。

使用弹性盒，内容纳呈现顺序不再受源码顺序的限制。然而，这只是视觉上的调整，弹性盒相关的属性不会改变屏幕阅读器对内容纳读取顺序。

弹性盒模型布局最突出的一个特点可能是，能让元素对不同的屏幕尺寸和不同的显示设备做好适应准备。弹性盒在响应式网站中表现极好，因为内容能根据可用空间的大小增减尺寸。

弹性盒依赖父子关系。在元素上生命`display: flex`或`display: inline-flex`便激活弹性盒布局，而这个元素随之成为弹性容器（flex-container），负责在所占的空间内布置子元素，控制子元素的布局。弹性容器的子元素称为弹性元素（flex-item）

## 12.2 弹性容器组

首先要完全理解的概念是弹性容器，也叫容器框。`display: flex`或`display: inline-flex`声明的目标元素变成然形容器，为其子元素生成弹性格式化上下文。

这些子元素无论是 DOM 元素、文本节点，还是生成的内容，都称为弹性元素。弹性容器中的绝对定位子元素也是弹性元素，不过确定其尺寸和位置时，将其视作弹性容器中唯一的弹性元素。

### 12.2.1. flex-direction属性

如果你想要的布局是从上到下、从左至右、从右至左，抑或是从下到上，可以使用 flex-direction 属性控制排布弹性元素的主轴。

### 12.2.2. 其他书写方向
### 12.2.3. 换行

如果弹性元素在弹性容器的主轴上放不下，默认情况下弹性元素不会换行，也不会自动调整尺寸。如果通过 flex 属性来设定允许弹性元素缩减尺寸，那就缩减尺寸。否则，弹性元素将从容器框的边界溢出。

这个行为受我们的控制，我们可以在容器上设置 flex-wrap 属性，允许弹性元素换行，变成多行或多列，而不让弹性元素从容器中溢出，或者缩减尺寸，挤在同一行。

### 12.2.4. 定义弹性流

flex-flow 属性用于定义主轴和垂轴的方向，以及是否允许弹性元素换行。

flex-flow 属性是 flex-direction 和 flex-wrap 两个属性的简写形式，用于定义弹性容器的换行方式及主轴和垂轴的方向。

把 display 属性设为 flex 或 inline-flex 后，省略 flex-flow 、 flex-direction 和 flex-wrap 相当于声明下述三个规则中的任何一个，结果如图12-12所示：

```css
flex-flow: row;
flex-flow: norow;
flex-flow: row nowrap;
```

**深入理解各种轴**

首先，弹性元素沿主轴排布。各行弹性元素沿垂轴的方向添加。

在介绍flex-wrap属性之前，所有示例都只有一行弹性元素。那一行弹性元素在主轴上排布，沿主方向，从主轴起边指向主轴终边。根据所设的flex-direction属性，弹性元素可能并排着排布，也可能从上到下或从下到上排布，沿主轴的方向显示为一行或一列。如图12-13所示。

可以看出，图12-13中有大量术语，其中很多是新的，要说明一下。下面对各术语做个简单的定义。

- 主轴：内容沿此轴流动。在弹性盒中，指弹性元素流动的方向。
- 主轴尺寸：主轴方向上内容纳总长度。
- 主轴起边：主轴上内容开始流动的那一端。
- 主轴终边：主轴上内容流向的那一端，与主轴起边相对。
- 垂轴：块级元素沿此轴堆叠。在弹性盒中，指放置新弹性元素行的方向（前提是允许换行）。
- 垂轴尺寸：垂轴方向上内容纳总长度。
- 垂轴起边：垂轴上块级元素开始堆叠的那一边。
- 垂轴终边：垂轴上与起边相对的那一边。

这些要素的位置取决于弹性方向、换行方式和书写模式。图解每种书写模式有点难，下面仅以从左至右书写的语言为例。各种情况见表12-1。

### 12.2.5. flex-wrap续谈

默认值nowrap禁止换行，因此前文讨论的垂轴方向没有任何意义，毕竟根本不会出现第二行。如果可能出现额外的行（flex-wrap设为wrap或wrap-reverse时），那些将沿垂轴方向添加。第一行放在垂轴的起边，额外的行则向垂轴终边排开。

可以看出，flex-direction和flex-wrap对布局有很大的影响，而且二者之间也有不小的影响。如果想设置其中某一个属性，最好两个都设置，此时可以使用规范强烈推荐的flex-flow属性。

## 12.3 布置弹性元素

目前所举的例子都没有涉及每一行中弹性元素的具体位置，我们不知道如何确定弹性元素的位置。横排的弹性元素横向展开似乎是理所当然的，但是为什么所有元素都靠主轴起边一侧紧挨在一起呢？为什么不增加弹性元素的尺寸，填满全部可用空间呢？为什么不让弹性元素在一行里均匀分布呢？

## 12.4 弹性容器

在目前所举的例子中，如果弹性元素不能填满整个弹性容器，弹性元素将统一向主轴起边靠紧。不过，弹性元素也可以紧靠主轴终边，或者在弹性容器中居中，甚至可以在主轴上均匀分布。

弹性布局规范提供的一些属性能控制空间的分布情况，除了display和flex-flow之外，CSS Flexible Box Layout Module Level 1还提供了一些能应用到弹性容器上的属性，包括justify-content、align-content和align-items。

justify-content属性控制一行里的弹性元素在主轴上如何分布。align-content属性定义各弹性元素行在弹性容器的垂轴上如何分布。align-items属性定义各行里的弹性元素在垂轴上如何分布。先看一行里的弹性元素是如何布置的。

## 12.5 调整内容

justify-content属性指明在弹性容器的主轴上如何分布各行里的弹性元素。这个属性应用于弹性容器上，不能用到单个弹性元素上。

## 12.6 对齐元素

justify-content定义弹性元素在弹性容器主轴方向上的对齐方式，而align-items属性定义的是弹性元素在垂轴方向上的对齐方式。与justify-content一样，align-items应用在弹性容器上，而不能应用到单个弹性元素上。

使用align-items属性，可以把所有弹性元素都向垂轴的起边、终边或中线对齐。align-items属性的作用与justify-content类似，不过影响的是垂向，设置所有弹性元素（包括匿名弹性元素）在垂轴上的对齐方式。

使用align-items属性，可以把所有元素都向垂轴起边或终边靠拢，也可以拉伸元素，同时靠拢起边和终边。此外，还可以把所有弹性元素都居中显示在垂向上。这个属性有五个可选值，包括flex-start、flex-end、center、baseline和默认的stretch,如图12-29所示。

### 12.6.1. 起边、缘边和居中对齐
### 12.6.2. 基线对齐
### 12.6.3. 补充说明
## 12.7 align-self属性 

看着有点早，但现在是讨论align-self属性的最佳时刻。这个属性在单个弹性元素上覆盖align-items属性的值。

align-items属性在弹性容器上设置，定义弹性容器中所有弹性元素的对齐方式。但是，单个弹性元素的对齐方式可以使用align-self属性覆盖。align-items的默认值是stretch,因此在图12-34中的五个示例里，除第二个弹性元素之外，其他弹性元素的高度都与所在的行一样高。

对所有align-self属性为默认值auto的弹性元素来说，其对齐方式继承自容器的align-items属性。但是每个示例中的第二个弹性元素例外，它的align-self值标在每个示例的下方。

## 12.8 对齐内容

align-content属性定义弹性容器有额外的空间时在垂轴方向上如何对齐各弹性元素行，以及空间不足以放下所有弹性元素行时从哪个方向溢出。

align-content属性指定弹性容器中垂轴方向上的额外空间如何分配到弹性元素行之间和周围，虽然align-content与前面讨论的align-items属性在取值和相关概念上是一样的，但是二者的作用不同，后者指定的是每一行中弹性元素的定位方式。

align-content的作用与justify-content类似，后者在弹性容器的主轴方向上对齐各个弹性元素，而前者在弹性容器的垂轴方向上对齐各弹性元素行。align-content属性只适用于分为多行显示的弹性容器，对禁止换行及只有一行的弹性容器没有影响。

## 12.9 弹性元素

前面几节介绍了如何通过弹性容器的样式整体排布弹性元素。此外，弹性盒布局规范还提供了几个直接应用于弹性元素的属性。利用这些专门针对弹性元素的属性，可以更加细致地控制弹性容器中的单个子元素。

### 12.9.1. 弹性元素是什么

为有子节点的元素声明`display:flex`或`display:inline-flex`即可创建弹性容器。弹性容器的子代称为弹性元素，不管是子元素，还是元素之间非空的文本节点，或是生成的内容。

对弹性容器中的文本子节点来说，如果文本节点不是空的（内容不是空白），将放在一个匿名弹性元素中，其行为与其他同辈弹性元素一样。虽然匿名弹性元素与同辈DOM节点一样，将继承在弹性容器上设置的相关弹性属性，但是不能直接使用CSS装饰。因此，不能直接在匿名弹性元素上设置针对弹性元素的属性。

### 12.9.2. 弹性元素的特性

弹性元素的外边距不折叠。float 和 clear 属性对弹性元素不起作用，不会把弹性元素移出文档流。其实，应用到弹性元素的 float 和 clear 将被忽略（然而，float属性对框体的生成仍有影响，因为 display 属性的计算值受它影响）。

**绝对定位**

我们知道float不会浮动弹性元素，但是`position:absolute`则不一样。如果绝对定位弹性容器的子元素，与绝对定位普通元素一样，将从文档流中移除。

除此之外，绝对定位的弹性元素不再参与弹性布局，因为它们已经不在文档流中。然而，这些元素将受应用在弹性容器上的样式影响，就像子元素受普通父元素（非弹性容器）的样式影响一样。除了可继承的属性被继承之外，应用到弹性容器上的属性可能还会影响定位原点。

绝对定位的弹性容器的子元素既受弹性容器的justify-content值影响，也受自身align-self值（如果设定了）的影响。例如，如果在绝对定位的子元素上设定`align-self:center`,元素将相对弹性容器的垂轴居中，然后再使用top、bottom、外边距等属性移动其位置。

order属性对弹性容器中绝对定位的子元素的位置没有影响，但是对同辈元素的绘制顺序有影响。

### 12.9.3. 最小宽度

在图12-40中可以看到，设为默认值nowrap的弹性元素行从弹性容器中溢出了。这是因为对弹性元素来说，未设定min-width时，默认为auto,而不是0。最初，规范规定，如果弹性元素在唯一的主轴上放不下，其尺寸将缩减。然而，出现弹性元素后，min-width的规范改了（以前，min-width的默认值是0。参见https://drafts.csswg.org/css2/visudet.html#min-max-widths）。

## 12.10 适用于弹性元素的属性

虽然弹性元素的对齐方式、顺序和弹性（flexibility）在一定程度上受在弹性容器上设置的属性控制，但是有些属性可以应用到单个弹性元素上，以便进行更细致地控制。
简写属性flex,以及构成它的flex-grow、flex-shrink和flex-basis属性用于控制弹性元素的弹性。这里所说的弹性是指弹性元素在主轴方向上可以增加或缩减多少尺寸。

## 12.11 flex属性 

弹性布局最突出的一点是能把弹性元素变得具有“弹性”，即在主轴方向上调整弹性元素的宽度或高度，占满可用空间。弹性容器根据弹性增长因子（flex grow factor）按比例分配额外的空间，或者根据弹性缩减因子（flex shrink factor）按比例缩小弹性元素，以防溢出（稍后探讨这些概念）。

增长因子和缩减因子由弹性元素的flex简写属性声明，或者由构成简写属性的单个属性定义。如果空间过多，可以增加弹性元素的尺寸，占满多出的空间。当然也可以不这如果指定的尺寸或默认的尺寸导致弹性元素在弹性容器中放不下，可以按比例缩减以便放得下。当然，此时也可以不这么做。

这一切都由flex属性控制，它是flex-grow、flex-shrink和flex-basis的简写形然三个子属性可以单独使用，但是强烈建议始终使用简写的flex,原因稍后说明。

## 12.12 flex-grow属性 

flex-grow属性定义有多余的空间时是否允许弹性元素增大，以及允许增大且有多余的空间时，相对其他同辈弹性元素以什么比例增大。

### 12.12.1 在flex属性中设定增长因子

flex属性有三个值：增长因子，缩减因子和基准。第一个有效的正数设定的是增长因子（即flex-grow的值）。如果flex属性没有设定增长因子和缩减因子，增长因子默认为1。然而，如果flex和flex-grow都没有声明，增长因子默认为0。是的，你没看错。

## 12.13 flex-shrink属性 

flex简写属性的`<flex-shrink>`部分指定弹性缩减因子。缩减因子也可以通过flex-shrink属性设定。

### 12.13.1. 根据宽度和缩减银子按比例缩小
### 12.13.2. 不同的基准
### 12.13.3. 响应式弹性布局

利用这种按比例缩小弹性元素尺寸的行为可以实现响应式布局。

## 12.14 flex-basis属性 

我们知道，弹性元素的尺寸受内容及盒模型属性的影响，而且可以通过flex属性的三个要素重置。flex属性中的`<flex-basis>`要素定义弹性元素的初始或默认尺寸，即根据增长因子和缩减因子分配多余或缺少的空间之前，弹性元素的大小。这个要素也可以使用flex-basis属性设定。

### 12.14.1. content关键字
### 12.14.2. 自动确定弹性基准
### 12.14.3. 默认值
### 12.14.4. 长度单位
### 12.14.5. 零基准 
## 12.15 flex简写属性

至此，我们对flex简写属性的各要素做了全面的了解。记住，始终使用flex简写属性。这个属性接受常规的全局属性值，包括initial、auto和none;只要是整数，通常为1,就表示弹性元素可以增大。下面简要说明一下。

**常见的弹性值**

常见的弹性值有四个，涵盖了最常需要的效果：

1. `flex:initial` 这个值根据width或height属性（由主轴方向决定）确定弹性元素的尺寸，而且允许缩小。
2. `flex:auto` 这个值也根据width或height属性确定弹性元素的尺寸，但是元素是完全弹性的，既可以缩小也可以增大。
3. `flex:none` 这个值还是据width或height属性确定弹性元素的尺寸，但是元素完全没有弹性，不能缩小也不能增大。
4. `flex:<number>` 这个值把弹性元素的增长因子设为`<number>`指定的数，同时把缩减因子设为0,把基准也设为0。这意味着，width或height属性的值相当于最小尺寸，弹性元素在有多余的空间时将增大。

## 12.16 order属性 

默认情况下，弹性元素的显示和排布顺序与在源码中的顺序一致。弹性元素和弹性元素行的顺序可以使用flex-direction属性反转，但是有时你可能需要更细致的重排方式。order属性用于修改单个弹性元素的显示顺序。

默认情况下，所有弹性元素的顺序都是0,归在同一个排序组中，以出现在源码中的顺序沿主轴方向显示（本章目前所举的例子都是如此）。

若想修改弹性元素的视觉顺序，把order属性设为一个非零整数。如果order属性的目标元素不是弹性容器的子元素，元素不受影响。

order属性的值指定一个排序组，把目标弹性元素归在其中。在页面中绘制弹性元素时，order属性为负数的弹性元素显示在采用默认值0的弹性元素前面，而order属性为正数的弹性元素显示在采用默认值0的弹性元素后面。虽然弹性元素的视觉顺序变了，但是在源码中的顺序没变。屏幕阅读器的阅读顺序和Tab键的索引顺序都由HTML源码顺序定义。

第 13 章 网格布局
第 14 章 CSS 中的表格布局
第 15 章 列表和生成的内容
# 第 16 章 变形

自层叠样式表（Cascading StyleSheet,CSS）诞生以来，元素始终是矩形的，而且只能沿横轴和纵轴放置。有些技巧能让元素看起来是倾斜的，但是底层的坐标方格并没有变形。时间来到21世纪10年代之前的几年，人们的兴趣日渐高涨，希望打破坐标方格的束缚，能以不同的方式改变对象的形态，而且还不只限于二维。

如果你定位过对象的位置，不管是相对定位还是绝对定位，你就改变过对象的形态。就此而论，使用浮动或负外边距技巧（抑或二者兼具）也算是改变了对象的形态。这些都是平移（translation）的例子，即把元素从原本所在的位置移到其他位置上。利用CSS提供的变形功能，不仅能平移元素，还能做很多其他的事。不论你想旋转照片，让照片看起来更自然，还是让界面元素在翻转后才能看到信息，又或是使用一些技巧，以有趣的视域显示侧边栏，CSS变形功能都能做到。不是我夸大，CSS变形功能甚至能让设计有所改观。

## 16.1 坐标系

旅程开始之前，先花点时间调整一下，变形涉及两种坐标系，最好事先了解一下。

首先是笛卡尔坐标系，也就是通常所说的x/y/z坐标系。这种坐标系使用两个数字（二维）或三个数字（三维）表示一个点在空间中的位置。在CSS中，这个坐标系使用三个轴表示：x轴（横轴）、y轴（纵轴）和z轴（深度轴），如图16-1所示。

2D（二维）变形只需关注x轴和y轴。按约定，x轴上的正值在右侧，负值在左侧。类似地，,轴上的正值沿纵轴向下，负值沿纵轴向上。

如果想在三维空间中改变元素的形态，要加上z轴值。这个轴从显示器上“跃出”，指向你的眼前。理论上，就是这样。z轴上的正值离你较近，负值离你较远。在这方面，z抽与z-index属性是完全一样的。

真正需要注意的是，每个元素都有自己的参照系，各轴都相对自身而动。也就是说，如果旋转了元素，轴也随之旋转，如图16-2所示。旋转之后再变形，是相对旋转后的轴计算的，而不是显示器的轴。

提起旋转，这就引出 CSS 变形功能使用的另一个坐标系——球坐标系，这个坐标系用于描述 3D 空间中的角度。

在2D变形中只需关注全周360度极坐标系，即由x轴和y轴构成的平面。对旋转来说，2D旋转其实是在绕z轴旋转。类似地，如果绕x轴旋转，元素将偏向我们或远离我们，而绕y轴旋转的话，元素将向两侧翻转。这些旋转方式如图16-4所示。

## 16.2 变形

变形其实只有一个属性，不过有几个辅助属性用于控制如何变形。先从主要的属性入手。

如果使用CSS改变可缩放矢量图形（Scalable Vector Graphic,SVG）的形态，其范围框是SVG图形定义的对象范围框。

注意，变形的元素有自己的堆叠上下文。经过缩放的元素可能比变形前小或大，不过元素在页面上所占的空间与变形前保持不变。这一点对所有变形函数都成立。

取值句法中的`<transform-list>`也需要说明一下。这个占位符表示一个或多个变形函数，一个接一个，中间以空格分隔，像下面这样，结果如图16-6所示：

```css
#example {transform: rotate(30deg) skewx(-25deg) scaleY(2);}
```

变形函数一次只处理一个，从第一个（最左边）开始，一直到最后一个（最右边）。从头到尾的处理顺序是很重要的，顺序变了，得到的结果可能就大有不同。请看下面两个规则，结果如图16-7所示：

顺序有影响的情况要比没有影响的情况多得多，因此一般来说，最好假定始终需要考虑顺序，即便严格来说并非总是如此。

注意，有多个变形函数时，每个都要正确设置，确保全部有效。即使有一个函数是无效的，整个值都将失效。例如：

**变形函数**

写作本书时，一共有21个变形函数。不同的变形函数和用不同格式的值实施相应的变形，这些可用的变形函数及其值的格式见表16-1

|               |           |            |         |               |
| ------------- | --------- | ---------- | ------- | ------------- |
| translate()   | scale()   | rotate()   | skew()  | matrix()      |
| translate3d() | scale3d() | rotate3d() | skewX() | matrix3d()    |
| translateX()  | scaleX()  | rotateX()  | skewY() | perspective() |
| translateY()  | scaleY()  | rotateY()  |         |               |
| translateZ()  | scaleZ()  | rotateZ()  |         |               |

transform 属性的值通常由空格分隔的一个或多个函数，各函数从头（左）至尾（右）依次处理，而且每个函数的值都必须是有效的。倘若有一个函数的值是无效的，那么 transform 属性的整个值都将失效，因而也就不做任何改变。

**平移函数**

平移变形指沿一个轴或多个轴移动。例如，translateX()沿元素自身的x轴移动元素，translateY()沿元素自身的y轴移动元素，translateZ()沿元素自身的z轴移动元素。

| 函数 | 可取的值 |
|---|---|
| translateX(),translateY() | `<length>`/`<percentage>` |


这两个通常称为“2D”平移函数，因为它们能上下移动元素，也能左右移动元素，但是不能沿z轴前后移动元素。这两个函数的值都是一个距离值，可以是长度，也可以是百分数。

值为长度时，效果与你预想的差不多。使用translateX(200px)沿x轴移动200像素的结果是元素向右移动200像素。换成translateX(-200px),元素则向左移动200像素。
对translateY()来说，正值向下移动元素，负值向上移动元素，而且都是相对元素自身的轴而言的。因此，如果通过旋转对调上下两边，那么translateY()的正值将在页面上向上移动元素。

如果值是百分数，移动距离相对元素自身的尺寸计算。对宽度为30像素、高度为200像素的元素来说，translateX(50%)把元素向右移动150像素，translateY(-10%)把元素向上移动20像素（相对原位置）

| 函数 | 可取的值 |
|---|---|
| translate() | `[<length>/<percentage>]``[<length>/<percentage>]?` |

如果想同时沿x轴和y轴移动，使用translate()更方便。第一个值是沿x轴的移动量，第二个值是沿y轴的移动量，这与translateX()translateY()结合在一起的作用是一样的。如果省略y值，假定为零。因此，translate(2em)视作translate(2em,0),也等同于translatex(2em)。图16-9是一些2D平移示例。

根据最新版规范，两个2D平移函数的值都可以不带单位。此时，提供的数字采用用户单位，如未设为其他单位，就是像素。CSS规范没有说明如何设定用户单位，但是SVG规范有规定，然而不详细。经测试，写作本书时没有浏览器支持不带单位的平移值，因此目前只是理论上支持这个特性。

| 语数 | 可取的值 |
|---|---|
| translateZ() | <length> |

这个函数沿z轴平移元素，即在第三个维度中移动元素。与2D平移函数不同，translateZ()只接受长度值。translatez()不允许使用百分数值，其实任何有关z轴的值都不可以使用百分数。

| 函数 | 可取的值 |
|---|---|
| translate3d() | [<length>/<percentage>],[<length>/<percentage>],[<length>] |

我们知道translate()能同时设定x轴和y轴平移，类似地，translate3d()这个简写属性能同时设定x轴、y轴和z轴的平移量。如果想一次性把元素向右、向上和向前移动，使用这个函数特别方便。

与translate()不同，如果translate3d()的值少于三个，没有假定的默认值。因此，用户代理应该把translate3d(1em,-50px)视作无效的，而不能假定为translate3d(2em,-50px,0)。

**缩放函数**

缴放变形把元素放大或缩小，具体取决于提供的值。缩放函数的值都是无单位的实数，而且始终为正数。在2D平面中，可以分别在x轴或y轴上缩放，也可以同时在两个轴上缩放。

| 函数 | 可取的值 |
|---|---|
| scalex(),scaleY(),scalez() | `<number>` |

提供给缩放函数的数字是个乘数，因此，scalex(2)将把元素的宽度变为变形前的两倍，而scaleY(0.5)将把元素的高度缩小一半。这样看，你可能以为缩放值也能使用百分数，但其实不然。

| 函数 | 可取的值 |
|---|---|
| scale() | `<number>` `[,<number>]?` |

如果想在两个轴上同时缩放，使用scale()。第一个始终是x值，第二个则是y值，因此scale(2, 0.5)将把元素的宽度放大两倍，把元素的高度缩小一半。如果只提供一个值，用作两个轴的缩放值；因此，scale(2)将把元素的宽度和高度都放大两倍。这与translate()是不同的，在translate()中，省略的第二个值始终被设为零。scale(1)缩放的元素与缩放前的尺寸完全相同，scale(1,1)也是，万一你真想这么做的话。

能在二维空间缩放，也就能在三维空间缩放。CSS提供的scalez()函数仅在z轴上缩放，而scale3d()则能同时在三个轴上缩放。当然，仅当元素有深度时，这两个函数才有效果，而元素在默认情况并没有深度。如果让元素具有一定的深度，例如绕x轴或y轴旋转，那么深度就可以缩放，使用scalez()或scale3d()都可以。

| 函数 | 可取的值 |
|---|---|
| scale3d() | `<number>`,`<number>`,`<number>` |

与translate3d()一样，scale3d()的三个数都必须是有效的。如若不然，无效的scale3d()将导致所属的整个变形值失效。

**旋转函数**

旋转函数绕某个轴旋转元素，或者绕3D空间中的一个向量旋转元素。庭转变形有四个简单的函数，以及一个稍微复杂、专门用于3D旋转的函数。

| 函数 | 可取的值 |
|---|---|
| rotate(),rotatex(),rotateY(),rotatez() | `<angle>` |

四个简单的旋转函数都只接受一个值，即角度。角度值以一个数字（可正可负）和一个有效的角度单位（deg、grad、rad和turn)表示。如果数字超出了相应单位的常规范围，将化为范围内的值。也就是说，437deg与77deg的效果是相同的，与-283deg的效果也是相同的。

然而要注意，仅当没有使用任何形式的动画，这样的换算才是完全等效的。如果以动画的形式旋转1100deg,元素将转动几周，最终停止在-20度（如果喜欢用正数，是340度）的倾斜位置。与之相比，如果以动画的形式旋转-20deg,元素将稍微向左倾斜，而不转动：如果以动画的形式旋转340deg,元素将向右转动几乎一周。这三次动画的最终状态是一样的，但是每一次旋转的过程有明显的差异。

rotate()函数实施的是2D旋转，是我们最常用的旋转方式。它的效果等同于rotateZ(),因为都是绕z轴（从显示器射出来，直指你的眼睛）旋转的。类似地，rotateX()绕x轴旋转，致使元素向你倾斜，或者远离你倾斜；rotateY()绕y轴旋转元素，像门的开合一样。这几个函数的效果如图16-12所示。

| 函数 | 可取的值 |
|---|---|
| rotate3d() | `<number>`,`<number>`,`<number>`,`<angle>` |

如果你了解向量，想在3D空间中旋转元素，使用rotate3d()。前三个值指定3D空间中向量的x、y和z分量，第四个值是角度值，指定绕向量旋转的量。

看个简单的例子：rotate(45deg)用3D旋转表示是rotate3d(0,0,1,45deg)。这个向量在x轴和y轴上的大小是零，在z轴上的大小是1。也就是说，旋转中心是z轴。元将绕指定的向量旋转45度，如图16-13所示。图中还给出了绕x轴和y轴旋转45度时应该提供给rotate3d()函数的值。

**倾斜函数**

倾斜函数沿x轴和（或）y轴倾斜元素。元素不能沿z轴或3D空间中的向量倾斜。

| 函数 | 可取的值 |
|---|---|
| skewx(),skewY() | `<angle>` |

这两个函数使元素倾斜指定的角度。文字表达有点抽象，看几个示例你就明白了。图16-16展示了几个沿x轴和y轴倾斜的例子。

| 函数 | 可取的值 |
|---|---|
| skew() | `<angle>``[<angle>]?` |

skew(a,b)的效果与skewX(a)skewY(b)不同。前者通过矩阵运算[ax,ay]实施2D倾斜。图16-17展示了几个矩阵倾斜的例子，以及与使用两个单轴倾斜变形的结果对比；表面上看结果应该是一样的，事实却不然。

如果提供两个值，第一个始终是x轴的倾斜角度，第二个是y轴的倾斜角度。如未指定y轴倾斜角度，假定为零。

**视域函数**

在3D空间中改变元素的形态时，基本上都要赋予元素一定的视域。视域为元素赋予前后深度，而这深度可以根据需要设定。

| 函数 | 可取的值 |
|---|---|
| perspective() | `<length>` |

通过距离指定视域看起来有点奇怪，毕竟`perspective(200px)`设定的距离无法在z轴上准确衡量。然而，存在即合理。深度幻象就围绕我们指定的值构建。较小的数得到较极端的视角，就像在元素跟前通过鱼眼镜头看元素一样。较大的数得到较温和的视角就像从远处通过变焦镜头看元素一样。特别大的视域值会产生等距效应。

这是有一定道理的。如果把视域想象成金字塔，顶点在视域的原点，基底在离你最近的地方，那么顶点与基底之间的距离越短，金字塔越扁，变形效果越失真，如图16-18所示图中假想的金字塔分别表示200像素、800像素和2000像素的视域距离。

视域值必须是正数，而且不能为零。其他值都将导致perspective()函数被忽略。此外要注意，perspective()函数在变形函数列表中的位置十分重要。

**矩阵函数**

如果你特别喜欢高等数学，或是出自Wachowski姐妹的电影译注1中的老掉牙的笑话，决不能错过本节介绍的函数。

| 函数 | 可取的值 |
|---|---|
| matrix() | `<number>` `[,<number>] (5,5)` |

CSS变形规范对matrix()函数做了严格规定：“以六个值a-f确定的变换矩阵指定2D平面中的变形。”
首先要注意，matrix()函数的有效值是六个以逗号分隔的数字。不能多，也不能少。数字可以为正，也可以为负。其次，matrix()函数的值所用的句法十分复杂，描述的是元素变形后的最终状态，可以涵盖其他所有变形类型（旋转、倾斜等）。最后，极少有人使用这个句法。


## 16.3 其他变形属性

除了基本的 transform 属性之外，还有几个辅助属性，用于定义变形的原点、“场景”使用的视域等。

### 16.3.1 移动原点

目前所见的变形有个共同点，都以元素的绝对中心为变形的原点。例如，旋转元素时，是绕着中心旋转的，而不是绕着某一角旋转的。这是默认行为，不过可以使用 transform-origin 属性修改。

取值句法看起来错综复杂，但实际使用起来还是比较简单的。transform-origin属性的值为两个或三个关键字，用于定义相对哪个点变形：第一个值针对横向，第二个值针对级向，可选的第三个值是z轴上的长度。横轴和纵轴可以使用英语关键字，例如top和right,也可以使用百分数、长度，或者不同类型的关键字搭配。然而z轴不能使用英语关键字或百分数，不过可以使用长度值，其中像素值是目前最常用的。

长度值设定的是距元素左上角的距离。因此，`transform-origin: 5em 22px`定义的变形原点距元素的左边5em、距元素的顶边22像素。类似地，transform-origin:5em22px200px定义的变形原点右移5em、下移22像素、后移200像素（即元素所在位置背后200像素）。

百分数相对对应的轴和元素的尺寸计算，设定的是距元素左上角的偏移量。例如，`transform-origin: 67% 40%`定义的元素距元素左边的距离为宽度的67%,距元素顶边的距离为高度的40%。图16-22展示了几种定义原点的方式。

### 16.3.2 选择3D变形方式

如果在三维空间中改变元素的形态，例如使用translate3d()或rotateY()。或许希望在 3D 空间中呈现元素。然而，这却不是默认的行为。默认情况下，不管怎样变形，得到的结果都是扁平的。幸好，这个行为可以使用transform-style属性修改。

| transform-style |  |
|---|---|
| 取值 | flat / preserve-3d |
| 初始值 | flat |
| 适用于 | 任何可变形的元素计算值指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

### 16.3.3 修改视域

视城其实由两个属性定义：一个定义视域距离，相当于前面讨论过的`perspective()`函数；令一个定义视域的原点。

**定义视域**

先讲perspective属性，这个属性的值是一个长度，定义视域椎体的深度。

先讲perspective属性。这个属性的值是一个长度，定义视域锥体的深度。这么看来，它与前面讨论的`perspective()`函数功能类似，不过二者之间有重要的区别。

| perspective |  |
|---|---|
| 取值 | none / `<length>` |
| 初始值 | none |
| 适用于 | 任何可变形的元素 |
| 计算值 | 绝对长度，或者none |
| 继承性 | 否 |
| 动画性 | 是 |

**移动视域的原点**

如果允许以3D形式呈现，元素在三维空间中的变形将使用视域（参见前文的transform-style和perspective属性）。视域有原点，也称消隐点（vanishing point），这个点的位置可以使用perspective-origin属性修改。

你可能发现了，perspective-origin的取值句法与transform-origin一样，而且最后也有个可选的长度值，定义在z轴上的偏移量。虽然值的表述是一样的，但是效果却截然不同。transform-origin定义的是围绕哪个点变形，而perspective-origin定义的是视线汇聚于哪一点。

### 16.3.4 处理背面

| backface-visibility |  |
|---|---|
| 取值 | visible / hidden |
| 初始值 | visible |
| 适用于 | 任何可变形的元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

这个属性没有前面讨论的属性和函数那么复杂，它的作用只有一个，即决定元素的背面朝向我们时是否渲染背面，仅此而已。

## 16.4 小结

CSS变形功能能在二维和三维空间中改变元素的形态，这为设计师提供了新的呈观信息的方式，使用丰富的 2D 变形可以实现引人注目的效果。利用 3D 变形还能创建交互式界面，变形功能为设计开群了一片新天地，有些属性之间有依赖关系。这对刚接触 CSS 变形的创作人员来说可能有些陌生，但是见得多了也会习惯的。

# 第 17 章 过渡

CSS过渡在一段时间内把CSS属性的初始值变为另一个值。这种状态的转变是对某种提作的响应，通常由用户交互触发，不过也可能由脚本对类、ID或其他状态的改变而引起。

通常， CSS 属性值的变化（发生“样式变化事件”）瞬间完成。属性的新值替换旧值持续的时间是毫秒级的，受影响的内容在这短暂的时间内重新绘制，若有必要，先重排布局再重新绘制。多数情况下，值的变化是瞬间完成的，整个过程不超过16毫秒。即便所用的时间较长，也是从一个值直接变为另一个值。例如，鼠标悬停时改变背景色，背景直接从一个颜色变为另一个颜色，中间没有过渡。

## 17.1 CSS过渡

CSS过渡能控制一段时间内属性的值如何变成另一个值。因此，我们可以让属性的值逐新变化,自然一些,不那么突兀。

## 17.2 定义过渡的属性

在CSS中，过渡使用四个属性定义：`transition-property`、`transition-duration`、`transition-timing-function`和`transition-delay`。此外，还有个简写属性`transition`，可一次声明全部四个属性。

过渡就在应用到元素上的常规样式中声明。当目标属性的值发生变化时，如果为目标属性设置了过渡效果，浏览器将应用过渡效果，逐渐由旧值变成新值。

### 17.2.1 限制受过渡影响的属性

transition-property属性指定想应用过渡效果的CSS属性名称。这样便可以限定只在特定的属性上应用过渡效果，而其他属性值的变化则瞬间完成。

transition-property属性的值是以逗号分隔的属性列表；或者是none,表示不过渡任何属性：还可以是默认值a11,即“过渡所有支持动画的属性”。以逗号分隔的属性列表中也可以包含关键字all。

> 在逗号分隔的一组值中，all必须放在首位。在a11前面声明的属性涵盖在a11之中，这样本想为前面的属性设定的其他过渡属性值将被覆盖。

**禁用过渡效果**

默认情况下没有过渡效果，然而如果设置了过渡，而后又想在特定的情况下撤销过渡效果，可以使用`transition-property: none`覆盖整个过渡声明，禁用所有属性的过渡效果。none关键字只能作为该属性的唯一一个值，不能放在以逗号分隔的一组值中。如果想销部分属性的过渡效果，只能列出仍想过渡的属性。transition-property属性不能排除不想过渡的属性，只能涵盖想过渡的属性。

> 另一种方法是把属性的延迟和持续时间都设为0s。这样，变化瞬间显现，就像没有应用CSS过渡效果一样。

**过渡事件**

在DOM中，不管是哪个方向的过渡，不管过渡持续多久，延迟多长，也不管过渡的属性是单独声明还是覆盖在 all 中，过渡结束后都会触发`transitionend`事件，有时看似单个声明的属性，却会触发多个`transitioned`事件，因为简写属性中每个支持动画的属性有各自的`transitionend`事件。以下述样式为例：

### 17.2.2 设置过渡持续时间

`transition-duration`属性的值是以逼号分隔的时间长度列表，单位为秒（s）或毫秒（ms）。这些值指定从一个状态过渡到另一个状态历时多久。

如果两个状态声明的transition-duration值不一样，过渡的持续时间为目标状态声明的transition-duration值。在上述示例中，如果输入框中的内容无效，变为红色背景的过程持续1秒，而内容有效时，变为绿色背景的过程只持续200毫秒。

transition-duration属性的值是正数，单位为秒（s）或毫秒（ms）。规范要求必须带时间单位，就算设为零秒，也要写成0s。默认情况下，属性值的变化是瞬间完成的看不到动画效果，因此过渡持续时间的默认值为0s。

如果transition-delay属性的值不是正值，而且没有声明transition-duration,那么声明的transition-property不起作用，即不触发transitionend事件。只要设置的过渡总时间大于零秒，可以直接设为0s,也可以不声明transition-duration,默认为0s,过渡效果就会应用，而且过渡结束时会触发transitionend事件。

transition-duration的值不能为负，如果持续时间列表中有一个是负值，整个属性值都将失效。

以前面那个超长的transition-property声明为例，我们可以为所有属性声明统一的持续时间，也可以单独为各属性声明不同的持续时间，还可以让余下的属性使用相同的持续时间。如果想让全部属性使用相同的持续时间，设置过渡时只要声明一个ransition-duration值：

此外，也可以在transition-duration属性中声明一组以逗号分隔的时间值，各值相同，而且与transition-property属性列出的值数量相等。如果想让各属性持续不同的时间，要在一组以逗号分隔的值中设置不同的时长：

如果声明的属性数量与持续时间的数量不一致，根据各浏览器制定的规则处理。如果持续时间的数量比属性多，忽略多出的持续时间。如果属性的数量比持续时间多，重复使用前面的持续时间。在下面的示例中，color、border-radius、opacity和width的持续时间为100毫秒，border、transform、box-shadow和padding的持续时间为200毫秒。

如果恰好声明两个持续时间，奇数位上的属性使用第一个持续时间，偶数位上的属性使用第二个持续时间。

### 17.2.3 调整过渡的内部时序

你是否希望过渡慢速开始，然后逐渐加快？或者快速开始，逐渐减速走向终点？又或者先平稳行进，然后步进甚至弹跳数次？`transition-timing-function`属性用于控制过渡的步调。

`transition-timing-function`可以取的值有ease、linear、ease-in、ease-out、ease-in-out、step-start、step-end、steps（n,start）（n是步进的次数）、steps（n,end）和cubic-bezier（x1,y1,x2,y2）（这些也是`animation-timing-function`属性的有效值，详情参见第18章）。

除步进关键字之外，其他关键字定义的是渐进时序函数，是描述平滑曲线的三次方贝塞尔函数的别名。规范预定义了五个渐进函数，见表17-1。

### 17.2.4 延迟过渡

transition-delay属性在元素上发生触发过渡的变化与开始过渡之间引入一定的延迟。

**负的延迟值**

如果transition-delay的值为负数，而且绝对值比transition-duration的值小，从中间某个位置立即开始过渡。例如：

### 17.2.5 transition简写属性

transition简写属性把目前介绍的四个属性合而为一：transition-property、transition-duration,、transition-timing-function 和 transition-delay。

transition属性的值可以是none,或者任意个以逼号分隔的单次过渡。单次过渡包含：应用过渡效果的一个属性，或者关键字a11,把过渡应用到全部属性上；过渡的持续时间：时序函数：以及延迟。

如果transition简写属性中的单次过渡没有声明要过渡的属性，那么此次过渡默认为all.如果没有声明transition-timing-function值，默认为ease。如果只有一个时间值，设定的是持续时间，而没有延迟，好似把transition-delay设为0s一样。

在单次过渡中，持续时间和延迟值的顺序很重要：解析为时间的第一个值设定的是持续时间。如果在逗号之前或语句末尾还有时间值，那就是延迟。

## 17.3 反向过渡：退回起点

在前面的示例中，我们都只声明了一个过渡。所有过渡都应用在默认状态上，由hover事件触发。这些情况下，当鼠标移开后，各属性通过相同的过渡回到默认状态，延迟相同但时序函数是相反的。

如果只在全局状态中声明过渡，鼠标悬停和移开状态使用相同的transition声明，因为选择符能匹配两个状态。如果不想完全复用整个过渡，覆盖部分过渡的属性，可以在全局状态（而不只是悬停状态）中声明不同的过渡值。

## 17.4 支持动画的属性和值

判断属性是否支持动画的关键是确定其取值能否内插。插值指在两个数据点之间插入一个数据点。判断属性的值是否支持动画的关键准则是计算值能否内插。如果属性的计算值是关键字，不能内插；如果关键字能计算为某种数值，则能内插。简单而言，如果能找到属性的两个值的中间点，那么属性的值可能就支持动画。

## 17.5 过渡是效果增强

浏览器对过渡的支持极好。所有浏览器，包括Safari、Chrome、Opera、Firefox、Edge和Internet Explorer（从IE10开始），都支持CSS过渡。

过渡是对用户界面（user-interface,UI）的效果增强。即使没有得到全面支持，也不妨碍你使用。如果某个浏览器不支持CSS过渡，本想以过渡效果呈现的变化仍会发生，只不过触发样式重新计算事件时，始态将瞬间“过渡”到终态。

用户可能会错过有趣的（也可能是恼人的）效果，但不会错过任何内容。

过渡算是一种渐进增强，因此无需为旧版IE浏览器打腻子脚本（polyfil）。为了支持IE9及之前的版本，是可以使用JavaScript腻子脚本，在Android4.3及之前的版本中也可以使用带前缀的过渡属性，不过这么做没多大意义。

## 17.6 打印过渡

打印网页或Web应用时，使用的是针对印刷媒体的样式表。如果style元素的media属性只匹配screen,那么CSS对打印出来的页面根本没有影响。

通常，我们不设定media属性；这跟设定media="all"一样，也就是默认值。打印有过渡效果的元素时，可能会忽略内插的值，也可能会打印当前状态下属性的值，具体取决于浏览器。

纸张上看不到元素的过渡效果，在某些浏览器中，例如Chrome,纸上打印出来的是调用print 函数时所处的状态（前提是过渡的属性能打印出来）。如果变化的是背景色，那么前后状态中的背景色都不会打印，因为背景色一般不打印。然而，如果是文本颜色从一个值变成另一个值，彩色打印机或PDF打印机将打印color属性的当前值。

在另一些测览器中，例如Firefox,打印过渡开始前还是开始后的值取决于过渡是如何开始的。如果是鼠标悬停触发的，打印的是非悬停状态下的值，因为在打印对话框中操作时鼠标不可能还悬停在那个元素上。如果过渡是通过增加类触发的，打印的是过渡开始后的值，即使过渡尚未结束。打印程序就像忽略过渡属性一样。

偏若有单独的印刷样式表或针对印刷品的@media规则，浏览器将单独计算样式。在印剧样式中，样式没有变化，因此也就没有过渡。在打印程序看来，属性值是瞬间变化的没有耗费一定时间的过渡效果。

# 第 18 章 动画

前一章介绍的CSS过渡算是一种简单的动画。过渡在状态发生变化时把属性的值从一个规则中设定的值变成另一个规则中设定的值，这个变化是在一段时间内完成的，而不是瞬间变化的。在CSS过渡中，属性的始态和终态值由规则中设定的属性值确定，但是对时间段内值的变化方式没有多少控制权。

CSS动画与过渡的相同点是CSS属性的值都在一段时间内发生变化，而不同点是前者对变化的方式有更大的控制权。尤其是，通过关键帧实现的CSS动画能设定是否以及如何重复动画，还能深度控制整个动画的过程等。过渡触发的是属性值的隐式变化，而动画变化过程中用到的属性值要在关键帧中显式声明。

css动画改变的属性值可以不在元素的前后两个状态中。在有动画效果的元素上设置的属性值无需参与动画过程。例如，从黑色到白色的过渡只以动画形式呈现不同的灰度；而使用动画时，在播放动画的过程中，元素可以不是黑色或白色，甚至也无需是位于二者之间的灰度。

当然，可以让颜色在不同的灰度之间过渡，但是我们可以先把元素变成黄色，然后再从黄色变成橙色。此外，还可以在不同的颜色之间变化，从黑色开始，到白色结束，让整个动画过程呈现彩虹式的变化。本章将探讨如何实现关键赖动画。

## 18.1 定义关键帧

若想为元素添加动画效果，要有一个关键赖，而这又要求有一个具名关键赖动画。首先，要使用ekeyframes规则定义可复用的CSS关键帧动画，并为动画起个名称。然后，通过这个名称把对应的动画效果应用到元素或伪元素上。

一个`@keyframes`规则有一个动画标识符（即动画的名称），以及一到多个关键帧块，每个关键帧块有一到多个关键帧选择符，声明属性及其值。整个`@keyframes`规则设置一个动画效果的完整选代过程。动画可以选代零次或多次，这主要取决于animation-iteration-count属性的值（参见18.4.3节）。

每个关键帧块中有一到多个关键帧选择符。关键帧选择符是动画持续时间内的时间点，可以是百分数，也可以是关键字from或to。动画的一般结构如下：

## 18.2 设置关键帧动画

创建动画的第一步是使用`@keyframes`为动画起个名称，并在一对花括号中定义关键赖。载至目前，这跟媒体查询（参见第20章）很像。

在一对花括号中有一系列关键帧选择符，其后有一段CSS,声明想以动画形式改变的属性。定义好关键帧之后，要使用animation-name属性把动画“附加”到元素上。这属性在18.4.1节讨论。

先看@规则声明，其后是动画的名称和一对花括号：

## 18.3 关键帧选择符

关键赖选择符指明声明的属性值应用到动画的哪个时间点，即动画播放到某个时刻希望属性为什么值。如果想设定动画开头的值，在0%记号处声明。如果想让属性在动画结束时变成另一个值，在100%记号处声明属性的值。如果想让属性在动画的三分之一处变成某个值，在33%记号处声明。这些记号就是关键帧选择符。

关键核选择符可以是以逗号分隔的一组百分数，也可以是关键字`from`或`to`。关键字`from`等于0%,关键字end等于100%。关键帧选择符表示目标关键帧在动画持续时间内位于百分之几的位置。关键帧由选择符后的属性值块声明。百分数值必须带上%号；也就是说，0不是有效的关键帧选择符。

### 18.3.1 省略from和to值

如未指定 0% 或 from 关键帧，用户代理（浏览器）将使用要应用动画效果的属性的原始值构建一个 0% 关键帧。这就跟使用没有应用动画效果时属性的值声明 0% 关键赖一样，只不过相应的属性不能受其他动画的影响（详情参见18.4.1节）。类似地，如果没有定义 100% 或 to 关键帧，而且没有应用其他动画，浏览器将使用没有动画效果时属性的值构建一个虚设的 100% 关键帧。

### 18.3.2 重复关键帧属性

在 Webkit 最初实现的实验性动画中（使用`-webkit-`前级），每个关键帧只能声明一次，如果多次声明，只有最后一个声明起作用，之前的关键帧选择符块被忽略。现在则不然。
如今，与CSS中的其他机制一样，具有相同值的关键帧将层叠。在标准的句法中（不用前级），前述W动画可以声明两次to或100%,left属性的值将被覆盖：

```css
@keyframes W {
  from, to {
    top: 0;
    left: 0;
  }
  25%, 75% {
    top: 100%;
  }
  50% {
    top: 50%;
  }
  to {
    left: 100%;
  }
}
```

注意，第一个关键帧选择符中既有from,也有to。因此，那个选择符块会为to关键帧设定top和left。而后，to关键帧的left值在最后一个关键帧块中被覆盖。

### 18.3.3 支持动画的属性

特别注意，不是所有属性都支持动画。在动画的关键帧中列出的不支持动画的属性，直接被忽略（同理，浏览器无法识别的属性和值也将被忽略）。

如果两个属性值没有中间点，得到的动画效果可能与预期不符，可能无法正确以动画形式呈现，或者根本没有动画效果。例如，不应该让元素的高度在`height:auto`和`height:300px`之间以动画形式变化，因为auto和300px之间没有中间点。动画效果可能还有，但是不同浏览器的处理方式不同：Firefox不渲染动画；如果auto等同于0,Safari会渲染动画；目前，Opera和Chrome直接跳到动画前后状态之间一半的位置，这可能并不是50%关键帧选择符，具体情况视animation-timing-function的值而定。也就是说，在没有中间点这个问题上，不同的浏览器对不同的属性有不同的处理方式，无法保证一定能得到预期的结果。

为每个属性都声明位于0%和100%位置上的值基本上能得到符合预期的动画效果。

### 18.3.4 不支持动画但不被忽略的属性

上述中间点规则有两个例外：visibility和animation-timing-function.

虽然`visibility:hidden`和`visibility:visible`之间没有中间点，但是visibility属性支持动画。从hidden变成visible时，可见性的值从一个值直接跳到发生变化的下一个关键帧。

尽管animation-timing-function属性不支持动画，但是如果在关键帧块中声明了，所在块中的属性值将使用它设定的时序函数。动画时序的变化不以动画形式呈现，而是直接变成新值，并且只在转到下一个关键帧时起作用（详情参见18.4.7节）。

### 18.3.5 通过脚本编辑@keyframes动画

关键帧规则在出现的那一刻还会应用可以通过API查找、追加和删除。@keyframes动画中声明的关键帧块可以使用`appendRule(n)`或`deleteRule(n)`修改，其中n是关键的完整选择符。关键帧的内容可通过`findRule(n)`获取。

```css
@keyframes w {
  from, to {
    top: 0;
    left: 0;
  }
  25%, 75% {
    top: 100%;
  }
  50% {
    top: 50%;
  }
  to {
    left: 100%;
  }
}
```

`appendRule()`、`deleteRule()`和`findRule()`三个方法的参数都是完整的关键帧选择符。以W动画为例，如果想获取25%/75%关键帧的内容，传入的参数为25%,75%:

```js
//获取指定关键帧的选择符和内容
var aRule = myAnimation.findRule ('25%, 75%').cssText;
//删除50%关键帧
myAnimation.deleteRule('50%');
//在动画末尾添加53%关键帧
myAnimation.appendRule('53% {top: 50%;}');
```

在`myAnimation.findRule('25%,75%').cssText;`语句中，myAnimation是一个关键帧动画的名称，返回的结果是匹配25%,75%的关键帧。如果只有25%或75%关键赖，匹配不到任何关键帧。如果用的是W动画，这个语句返回`25%,75%{top:100%;}`。

类似地，`myAnimation.deleteRule('50%')`将删除最后一个50%关键帧。因此，如果有多个50%关键帧，排在最后的那个将被删除。反过来，`myAnimation,appendRule('53%{top:50%;})`将在@keyframes块中最后一个关键帧的后面追加53%关键帧。

动画有三个事件，animationstart、animationend和animationiteration,分别在动画的开头和结尾，以及一次选代结束与下一次迭代开始之间触发。只要动画中定义的关键帧规则有效，就会触发animationstart和animationend事件，即使关键帧规则为空也是如此。animationiteration事件仅在动画有多次选代时才会触发，因为animationiteration不能与animationend事件同时触发。

## 18.4 把动画应用到元素上

定义好关键帧动画便可以把动画应用到元素和（或）伪元素上。为了把动画附加到元素上，并控制动画的播放过程，CSS提供了多个相关的属性。若想保证动画效果能显示出来，至少要指明动画的名称，以及持续时间（不然动画瞬间就结束了）。

在元素上声明动画属性的方式有两种：一种是单独声明各个属性，另一种是使用animation简写属性一次性声明全部属性（抑或二者结合）。我们先来学习各个单独的属性，然后再介绍如何把全部声明浓缩在animation简写属性中。

下面逐一介绍各个单独的属性。

### 18.4.1 指定动画的名称

animation-name属性的值为一个逗号分隔的列表，指定想应用的关键帧动画的名称。这里所说的名称是指使用@keyframes规则定义动画时设定的无引号标识符或有引号的字符串（抑或二者混用）。

| animation-name |  |
|---|---|
| 取值 | [`<single-animation-name>` / none]# |
| 初始值 | none |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

默认值为none,表示没有动画效果。根据CSS层叠机制，可以使用none值覆盖其他地方应用的动画（这也是不建议使用none命名动画的原因，除非你疯了）。如果想应用动画，把值设为`@keyframes`的标识符，即动画的名称。

只把动画应用到先系上还不足以让动画呈现出来，动画虽然能播放，但是瞬间就结束。此时，关键帧中的属性都会经历变化，而且animationstart和animationend事件也会触发。若想看到动画效果，至少要让动画持续一定的时间。而这由animation-duration属性设定。

### 18.4.2 定义动画的时长

animation-duration属性定义动画选代一次用时多久，单位为秒（s）或毫秒（ms）。

| animation-duration |  |
|---|---|
| 取值 | `<time>`# |
| 初始值 | 0s |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

### 18.4.3 声明动画的迭代次数

只声明必须的animation-name属性，动画将播放一次，而且只播放一次。如果希望选代的次数不是默认的一次，使用animation-iteration-count属性设定。

| animation-iteration-count |  |
|---|---|
| 取值 | [`<number>` / infinite]# |
| 初始值 | 1 |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

默认情况下，动画播放一次（因为默认值是1）。如果给animation-iteration-count属性提供其他值，可以是任何数字或关键字infinite,而且animation-delay属性的值中没有负值，动画将重复指定的次数。

### 18.4.4 设置动画的播放方向

使用animation-direction属性可以控制动画是从0%关键帧向100%关键帧播放，还是从100%关键帧向0%关键帧播放。可以让所有迭代都按照相同的方向播放，也可以隔一个循环变换一次方向。

| animation-direction |  |
|---|---|
| 取值 | [normal / reverse / alternate / alternate-reverse]# |
| 初始值 | Normal |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

animation-direction属性定义按什么方向播放动画的关键帧。可取的值有四个：

- `normal`：设为normal时（或者省略，默认为norma1），动画的每次选代都从0%关键帧向100%关键帧播放。
- `reverse`：reverse值逆序播放各次选代，即从100%关键帧向0%关键帧播放。逆转动画的方向也就逆转了animation-timing-function（参见18.4.7节）。
- `alternate`：alternate值的意思是第一次选代（以及后续各奇数次选代）从0%向100%播放，第二次选代（以及后续各偶数次选代）方向相反，从100%向0%播放。
- `alternate-reverse`：alternate-reverse值与alternate值类似，只不过是反过来的。第一次选代（以及后续各奇数次选代）从100%向0%播放，第二次选代（以及后续各偶数次迭代）方向相反，从0%向100%播放。

### 18.4.5 延迟播放动画

animation-delay属性定义浏览器把动画附加到元素上之后等待多久开始第一次选代。

| animation-delay |  |
|---|---|
| 取值 | `<time>`# |
| 初始值 | 0s |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

animation-delay属性设定把动画附加到元素上之后隔多久开始播放动画，单位为秒（s）或毫秒（ms）。


### 18.4.6 动画事件

与动画有关的事件有三个：animationstart、animationiteration和animationend。每个事件都有三个只读属性：animationName、elapsedTime和pseudoElement,在所有浏览器中都无需使用前缀。

animationstart 事件在动画开始播放时触发；如有延迟，等animation-delay 设定的时间过后触发；否则，立即触发。如果animation-delay为负值，animationstart事件立即触发，在支持elapsedTime的浏览器中，它的值等于延迟的绝对值。而在仍需使用前缀的浏览器中，elapsedTime等于0。

**动画链**

我们可以利用animation-delay属性把多个动画串在一次，让下一个动画在前一个动画结束后立即开始：

```css
.rainbow {
  animation-name: red, orange, yellow, blue, green;
  animation-duration: 1s, 3s, 5s, 7s, 11s;
  animation-delay: 3s, 4s, 7s, 12s, 19s;
}
```

在这个示例中，red动画延迟三秒、持续一秒，因此animationend事件在四秒后触发。后续各动画都在前一个动画结束后开始。我们称这样的效果为CSS动画链。

### 18.4.7 改变动画的内部时序

好了，编写脚本是很好玩，不过我们还是回到纯CSS上吧。下面讨论时序函数。与transition-timing-function属性类似，animation-timing-function属性指明动画在一次循环（或迭代）中如何演进。

| animation-timing-function |  |
|---|---|
| 取值 | [ ease / linear / ease-in / ease-out / ease-in-out / steps-start / steps-end / steps(`<integer>`, start) / steps(`<integer>`, end) / cubic-bezier(`<number>`, `<number>`, `<number>`, `<number>`)]# |
| 初始值 | ease |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

### 18.4.8 设置动画的播放状态

如果想暂停和继续播放动画，可以使用animation-play-state属性定义动画是播放还是暂停的。

| animation-play-state |  |
|---|---|
| 取值 | [running / paused]# |
| 初始值 | running |
| 适用于 | 所有元素，以及`::before`和`::after`伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

设为默认值running时，动画正常播放。设为paused时，动画暂停。此时，动画依然应用到元素上，只是在暂停前播放到的位置停住。如果在迭代中途停止，已经发生变化的属性停在当前的值。再次设为running,或者回到默认值，动画从停止的位置继续播放，就像控制动画的“时钟”停止后又开始行走了一样。

如果在动画的延迟阶段设置`animation-play-state: paused`,延迟时钟也暂停，把animation-play-state设为running之后继续计时。

### 18.4.9 动画的填充模式

animation-fill-mode属性定义动画播放结束后是否应用原来的属性值。

| animation-fill-mode |  |
|---|---|
| 取值 | [ none / forwards / backwards / both ]# |
| 初始值 | none |
| 适用于 | 所有元素，以及：before和：:after伪元素 |
| 计算值 | 指定的值 |
| 继承性 | 否 |
| 动画性 | 否 |

这个属性的作用体现在，默认情况下动画所做的改动只在动画播放的过程中有效，一旦动画结束，属性将还原为动画之前的值。因此，如果动画把背景由红色变成蓝色，（默认情况下）动画结束后背景将还原为红色。

类似地，如果animation-delay为正值，动画不会立即改变属性的值，而是在延迟结束，触发animationstart事件后才开始改变。

使用animation-fi11-mode属性可以定义触发animationstart事件之前和触发animationend事件之后动画如何影响元素。我们可以设定，让0%关键帧中设定的属性值在延迟期间就应用到元素上，或者在触发animationend事件之后继续应用到元素上。

animation-fill-mode属性的默认值是none,意思是动画不播放就没有效果：0%关键赖（或反向播放动画时的100%关键帧）块中设定的属性值在animation-delay结束、触发animationstart事件之前不应用到元素上。

设为backwards时，0%或from关键帧（如果有的话）中定义的属性值在动画应用到元素上的那一刻就起作用。0%关键帧（animation-direction属性的值为reversed或reversed-alternate时，为100%关键帧）定义的属性值立即应用，而不等待animation-delay时间结束。

forwards值的意思是动画播放结束后，即animation-iteration-count设定的选付次数全部结束，触发了animationend事件，当时的属性值继续应用在元素上。如果animation-iteration-count的值是整数，应用的属性值来自100%关键赖；如果最后一次选代是反向的，则来自0%关键帧。

both值包含backwards和forwards两个值的效果，即把动画附加到元素上之后立即应用属性值，而且触发animationend事件之后，属性的值得以保留。

## 18.5 写为一个属性

使用animation简写属性，无需分别定义8个属性，在一行声明中就能为元素定义全部动画属性。animation属性的值是一个列表，以空格分隔，分别对应各个单独属性。如果要在元素或伪元素上应用多个动画，在列出的各动画之间加上逗号。

## 18.6 动画、特指度和优先顺序

动画在特指度和层叠规则方面有些特殊，确定把哪个属性值应用到元素上时，会错误地覆盖层叠样式中的其他所有值（截至2017年年末）。

### 18.6.1 特指度和!important

一般来说，通过ID选择符应用到元素上的属性，其权重为1-0-0,这应该比元素选择符的0-0-1权重高。然而，如果属性的值是以关键帧动画形式改变的，应用到元素上时，属性及其值好像是通过行内样式添加的一样。

目前，在所有支持动画的浏览器中，关键帧设定的属性值都好像是行内声明的一样，而且加上了！important,例如`<divstyle="keyframe-property:valuelimportant">`.根据规范，这是错误的行为。规范指出，“动画覆盖常规的规则，但是能被带有！important的规则覆盖”。在2017年年末之前实现的浏览器中，这是个bug,最终应该会被修正。或者，规范可能会做修改。

尽管如此，不要在动画声明块中使用!important。这样做是无效的，反而会导致相应的属性和值被忽略。

### 18.6.2 动画顺序

如果有多个动画为同一个属性指定了不同的值，最后一个应用的动画将覆盖之前动画中声明的值：

### 18.6.3 display:none;对动画迭代的影响
### 18.6.4 动画和UI线程
## 18.7 癫痫和前庭功能失调
## 18.8 动画事件及其前缀
### 18.8.1 animationstart
### 18.8.2 animationend
### 18.8.3 animationiteration
## 18.9 打印动画

第 19 章 过滤器，混合，剪切和掩蔽
第 20 章 Media-Dependent 风格