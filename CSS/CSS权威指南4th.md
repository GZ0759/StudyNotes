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

置换元素（replaced element）指用来置换元素内容的部分不由文档内容直接表示。在 HTML 中，最常见的置换元素要数 img ，它的内容由文档之外的图像文件替换。其实，通过下面这个简单的例子可以看出， img 元素没有内容。

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

CSS有些内容的前面有个标注，例如-o-border-image，这就叫做厂商前缀，浏览器通过它标记实验性或专属的属性、值或其他内容。
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

`:empty`伪类可以匹配html的空元素，比如img和input，但是它还可以匹配没有内容的textarea元素。

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

在MDN的介绍里，CSS变量可以自定义属性，[点击链接查看相关信息](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Using_CSS_custom_properties#什么是CSS变量)。

第 5 章 字体
第 6 章 文本属性

# 第 7 章 基本的视觉格式化

本章全面阐述 CSS 视觉渲染的理论。为什么要了解这些知识呢？因为 CSS 是如此开放、如此强大的一个系统，任何书都不可能涵盖属性的所有组合方式及其效果。在实践中，你肯定会发现使用 CSS 的新方式。而且在探索 CSS 的过程中，你可能会在某些用户代理中遇到看似奇怪的行为。掌握视觉渲染模型的工作原理之后，你便能判断所遇到的怪异行为（尽管出乎意料）就是 CSS 渲染引擎定义的正确方式，还是确有异常。

## 7.1 元素框基础

不管是什么元素，CSS 都假定每个元素都生成一个或多个矩形框，我们称之为元素框（element box）（以后的规范可能会允许元素生成非矩形框，而其实现在就有这方面的提议，不过目前生成的框还都是矩形的）。各元素框的中心是内容区域（conten area）,四周有可选的内边距、边框、轮廓和外边距。之所以说这些区域是可选的，是因为它们的宽度都可以设为零，即把它们从元素框上删除。图 7-1 展示了一个内容区域，四周围绕着内边距、边框和外边距。

外边距、边框和内边距都有分别针对每一边的属性，例如 margin-left 或 border-bottom,也有简写属性，例如 padding。而轮廓没有针对各边的属性。默认情况下，内容区的背景（例如颜色或平铺的图像）出现在内边距范围内。外边距区域始终是透明的，因此透过它能看到父元素。内边距不能为负值，但是外边距可以。稍后会说明把外边距设为负值的效果。

<!-- <Figures figure="7-1">The content area and its surroundings</Figures> -->

边框的线型由样式定义，例如设为 solid 或 inset,边框的颜色由 border-color 属性设定。如未设定颜色，边框的颜色与元素中内容的前景色相同。比如说，段落中的文本是白色，如果创作人员没有明确声明使用其他颜色，那么段落四周的边框也是白色的。如果边框的线型有间隙，那么默认情况下，从间隙中能看到元素的背景。最后，边框的宽度不能为负数。

元素框各组成部分受很多属性的影响，例如 width 或 border-right。本书将使用其中多数属性，但是不会深入讨论。

### 7.1.1 重要概念概览

下面简要说明一下我们将讨论的不同框体，以及后文将用到的重要术语：

1. 常规流动 Normal flow

即渲染西方语言时从左至右、从上到下的顺序，以及传统的 HTML 文档采用的文本布局方式。注意，对非西方语言来说，流动方向可能会变。多数元素都采用常规的流动方式，除非元素浮动了、定位了，放入弹性盒或采用栅格布局了。不过本章只讨论常规流动方式下的元素。

2. 非置换元素 Nonreplaced element

内容包含在文档中的元素。例如，段落（p）是非置换元素，因为段落中的文本内容在元素自身中。

3. 置换元素 Replaced element

为其他内容占位的元素。典型的置换元素是 img,它指向一个图像文件，那个图像就插在 img 元素在文档流中的位置上，多数表单元素也是置换元素（例如`<input type="radio">`）.

4. 根元素 Root element

位于文档树顶端的元素。在 HTML 文档中，根元素是 html。在 XML 文档中，根元素可以是语言允许的任何元素，例如，RSS 文件的根元素是 rss。

5. 块级框 Block box

段落、标题或 div 等元素生成的框。在常规流动模式下，块级框在框体前后都“换行，因此块级框是纵向堆叠的。`display: block` 声明能把任何元素生成的框体变级框。

6. 行内框 Inline box

strong 或 span 等元素生成的框体。行内框前后不“换行”。`display: inline` 声明能把任何元素生成的框体变成行内框。

7. 行内块级框 Inline-block box

内部特征像块级框，外部特征像行内框。行内块级框的行为与置换元素相似，但不完全相同。比如说把一个 div 元素像行内图像那样插入一行文本，这样一想你就明白了。

除此之外还有其他框体，例如单元格框，但是基于各种各样的原因（那些框体太过复杂一本书也讲不完，而且没有多少作者能驾驭，只这一点就够了），本书不做讨论。

### 7.1.2 容纳块

还有一种框体要深入说明，因为涉及的知识够多，所以单开一节。这种框体是容纳块（containing block）.

每个元素的框体都相对容纳块放置，说得简单点就是，容纳块是元素框体的“布局上下文”。为了确定框体的容纳块，CSS 定义了一系列规则。不过我们只会说明与本书内有关的那些规则，以免话题展开太多。

在使用常规流动方式渲染的西文文本中，容纳块由离元素最近的那个生成列表项目或级框（包含所有与表格有关的框体，例如单元格生成的框体）的祖辈元素的边界构成。以下述标记为例：

```html
<body>
  <div>
    <p>This is a paragraph.</p>
  </div>
</body>
```

在这段十分简单的标记中，p 元素的块级框的容纳块是 div 元素的块级框，因为这是祖辈元素的框体中离 p 元素最近的，而且生成的是块级框或列表项目（这里，div 元素生成的是块级框）。类似地，div 元素的容纳块是 body 元素的框体，因此，p 元素的布局依赖 div 元素的布局，而 div 元素的布局又依赖 body 元素的布局。

继续下去，body 元素的布局依赖 html 元素的布局。html 元素对应的是初始容纳块（initial coataining block）,它的独特之处是，其尺寸由视区（屏幕媒体中的浏览器窗口，印刷媒体中的可打印区域）决定，而非根元素中内容的尺寸。初始容纳块与其他容纳块的差异极小，而且通常并不重要，但是你要知道有这么一种容纳块。

## 7.2 调整元素的显示方式

为 display 属性设值可以影响用户代理显示元素的方式。既然我们开始深入讲解视觉格式化了，那就用前文学过的概念多讨论 display 属性的两个值。

<!-- <Cards cards="display" /> -->

我们将忽略旁注（ruby）和表格相关的值，因为对本章的内容来说，它们太过复杂；我们还将忽略 list-item 这个值，因为它与块级框特别相似。我们将用大量时间讨论块级框和行内框，不过在此之前先讨论调整元素显示方式对布局的影响，随后再说明 inline-block 这个值。

### 7.2.1 改变显示方式

装饰文档时，若能改变元素生成的框体类型显然很方便。例如，假设 nav 元素中有一系列链接，我们想纵向布局，显示为侧边栏：

```html
<nav>
  <a href="index.html">WidgetCo Home</a>
  <a href="products.html">Products</a>
  <a href="services.html">Services</a>
  <a href="fun.html">Widgety Fun!</a>
  <a href="support.html">Support</a>
  <a href="about.html" id="current">About Us</a>
  <a href="contact.html">Contact</a>
</nav>
```

为此，可以把链接分别放在单元格中，也可以把每一个链接都放在一个 nav 元素中，家者直接把各个链接变成块级元素，像下面这样：

```css
nav a {
  display: block;
}
```

这个规则把 nav 元素中的每个 a 元素变成块级元素。如果再添加一些样式，可以得到似图 7-2 所示的结果。

<!-- <Figures figure="7-2">Changing the display role from inline to block</Figures> -->

这样修改元素的显示方式之后，在不支持 CSS 的浏览器中，导航链接将显示为行内元素，而在支持 CSS 的浏览器中，导航链接将显示为块级元素。把链接变成块级元素之后，可以像 div 或 p 元素那样装饰，整个元素框都变成链接的了。因此，用户把鼠标指针悬停在元素框上的任何位置都能单击链接。

此外，你可能还想把元素变成行内显示方式。假设有这么一个显示人名的无序列表：

```html
<ul id="rollcall">
  <li>Bob C.</li>
  <li>Marcio G.</li>
  <li>Eric M.</li>
  <li>Kat M.</li>
  <li>Tristan N.</li>
  <li>Arun R.</li>
  <li>Doron R.</li>
  <li>Susie W.</li>
</ul>
```

现在我们想把这些人名显示为行内元素，而且在人名之间（以及整个列表的前后）加上竖线，为此，只能改变显示方式。下述规则的效果如图 7-3 所示。

```css
#rollcall li {
  display: inline;
  border-right: 1px solid;
  padding: 0 0.33em;
}
#rollcall li:first-child {
  border-left: 1px solid;
}
```

<!-- <Figures figure="7-3">Changing the display role from list-item to inline</Figures> -->

你可以根据设计需要灵活使用不同的显示方式，只有想不到，没有做不到。

热而，要注意，我们改变的是元素的显示方式，而不是元素的本性。也就是说，把段落生或的框体变成行内框并不会把段落变成行内元素。例如，HTML 元素有些是块级元素，有些则是行内元素（其实还有些是“流动”元素，不过暂且不提）。行内元素可以作为块级元素的后代，但是反过来一般不行。比如说，span 元素可以放在一个段落中，但是却不能把段落放在 span 元素中。

不论怎样装饰元素，这一点都成立。以下述标记为例：

```html
<span style="display: block;">
  <p style="display: inline;">this is wrong!</p>
</span>
```

这段标记是不对的，因为块级元素（p）嵌套在行内元素（span）中。虽然改变了显示方式，但这一点是变不了的。display 属性的名称就表明，它是影响元素显示方式的，而不能改变元素的种类。

了解这些知识之后，下面深入讨论不同的框体：块级框、行内框、行内块级框和列表项目框。

### 7.2.2 块级框

块级框的行为有时可以预测，有时又让人捉摸不透。例如，框体位置在横轴和纵轴上的处理方式就有所不同。为了充分理解块级框的处理方式，必须知道一些界线和区域，如图 7-4 所示。

默认情况下，块级框的宽度（width）等于左内边界到右内边界的距离，高度（height）等于上内边界到下内边界的距离。这两个属性可用于生成块级框的元素。

<!-- <Figures figure="7-4">The complete box model</Figures> -->

这些属性的处理方式可以使用 box-sizing 属性调整。

<!-- <Cards cards="box-sizing" /> -->

这个属性用于改变 width 和 height 值的具体意义。如果声明 `width: 400px`,而且不为 box-sizing 设值，那么元素的内容框将为 400 像素宽，内边距和边框等都在此基础上增加，如果声明 `box-sizing: border-box`,那么元素框从左边框的外边界到右边框的外边界相距 400 像素：边框或内边距都在这个尺寸之内计算，即内容区的宽度相应减少。这两种情况如图 7-5 所示。

<!-- <Figures figure="7-5">The effects of box-sizing</Figures> -->

这里提到 box-sizing 属性，是因为它作用于“能设定 width 或 height 的所有元素”，通常，这是指生成块级框的元素，不过也能用于行内置换元素（如图像）,以及行内块级框。

这些宽度、高度，以及内边距和外边距在一起，决定着文档的布局方式。多数情况下，文档的高度和宽度由浏览器自动确定，而且是根据可用显示区域确定的，此外还受一些其他因素的影响。通过 CSS,可以直接控制元素的尺寸和显示方式。

### 7.2.3 横向格式化

横向格式化往往比你想的复杂。之所以复杂，部分是由于 box-sizing 的默认行为，使用默认值 content-box 时，为 width 设定的值是内容区的宽度，而不是整个元素柜的可见宽度。以下述标记为例：

```html
<p style="width: 200px;">wideness?</p>
```

这个段落中的内容为 200 像素宽。如果有背景，看的就相当清楚了。此时，如果有内边距，边框或外边距的话，将增加到这个宽度之上。假设我们是这样设定的：

```html
<p style="width: 200px; padding: 10px; margin: 20px;">wideness?</p>
```

那么，元素框的可见区域将是 220 像素宽，因为我们在内容区的左右各添加了 10 像素宽的内边距。外边距又在元素的两侧添加 20 像素，因此这个元素框的总体宽度为 260 像素。结果如图 7-6 所示。

<!-- <Figures figure="7-6">Additive padding and margin</Figures> -->

如果修改样式，把 box-sizing 设为 border-box,那么结果就不同了。此时，元素柜的可见区域为 200 像素宽，内容区域为 180 像素宽。因为两侧的外边距共 40 像素，所以元素框的总体宽度为 240 像素，如图 7-7 所示。

<!-- <Figures figure="7-7">Subtracted padding</Figures> -->

在这两种情况下，常规流动方式下块级框各组成部分的横向尺寸始终等于容纳块的宽度。假设一个 div 元素中有两个段落，div 元素的外边距为 1em,box-sizing 属性使用默认值。那么，每个段落的内容区宽度（即 width 的值）,加上左右内边距，边框和外边距，得到的和始终等于 div 元素内容区的宽度。

假设 div 元素的宽度为 30em。那么，段落的内容区宽度，加上内边距，边框和外边距之和为 30em。图 7-8 中段落四周的“空白”其实是段落的外边距。如果 div 元素有内边距，空白区域更大，不过这里没有。

<!-- <Figures figure="7-8">Element boxes are as wide as the width of their containing block</Figures> -->

### 7.2.4 横向格式化属性

横向格式化属性有七个，分别为 margin-left、border-left、padding-left、width、padding-right、border-right 和 margin-right。这七个属性影响块级框的横向布局，如图 7-9 所示。

这七个属性的值加在一起要等于元素容纳块的宽度，而这一宽度通常为块级元素的父元素的 width 值（因为块级元素的父元素几乎都是块级元素）。

在这七个属性中，只有三个属性的值能设为 auto（元素内容区的宽度、左外边距和右外边距）。余下的几个属性，要么设为具体的值，也么使用默认值（零）。图 7-10 展示了元素框的哪些部分能设为 auto,而哪些部分不能。

<!-- <Figures figure="7-9">The seven properties of horizontal formatting</Figures> -->

<!-- <Figures figure="7-10">Horizontal properties that can be set to auto</Figures> -->

width 属性的值要么设为 auto,要么设为某种类型的非负值。在横向格式化中使用 auto,可能得到不同的结果。

### 7.2.5 使用 auto

在 width、margin-left 和 margin-right 三个属性中，如果把其中一个设为 auto,另两个设为具体的值，那么设为 auto 的那个属性的具体长度要能满足元素框的宽度等于父元素的宽度，假如七个属性的值之和必须等于 500 像素，右外边距的宽度设为 100px,左外边距设为 auto,而且没有设定内边距或边框，那么左外边距的宽度将是 300 像素。

```css
div {
  width: 500px;
}
p {
  margin-left: auto;
  margin-right: 100px;
  width: 100px;
} /* 'auto' left margin evaluates to 300px */
```

从某种意义上说，auto 可用于补全总和所缺的尺寸。然而，如果把这三个属性的值都设为 100px,没有一个设为 auto,情况又如何呢？

如果把这三个属性都设为 auto 之外的值，用 css 术语来说就是过约束了，那么 margin-right 将被强制设为 auto,也就是说，如果左右外边距和宽度都设为 100px 的话，用户代理会把右外边距重置为 auto,此时，右外边距的宽度自动设定，不过要满足元素的总宽度等于容纳块的宽度。下述样式的结果如图 7-11 所示：

```css
div {
  width: 500px;
}
p {
  margin-left: 100px;
  margin-right: 100px;
  width: 100px;
} /* right margin forced to be 300px */
```

<!-- <Figures figure="7-11">Overriding the margin-right setting</Figures> -->

如果左右外边距都明确设为 auto,那么 width 的值是满足总宽度（即父元素的内容区宽度）所需的任何值。下述样式的结果如图 7-12 所示：

```css
p {
  margin-left: 100px;
  margin-right: 100px;
  width: auto;
}
```

图 7-12 所示的情况是最常见的，即设定左右外边距而不设定 width。下述样式的结果与图 7-12 完全一样：

```css
p {
  margin-left: 100px;
  margin-right: 100px;
} /* same as before */
```

<!-- <Figures figure="7-12">Automatic width</Figures> -->

你可能想知道把 box-sizing 设为其他值（例如 padding-box）会怎样。前面所讲的内容假定用的是 content-box,不过换成其他值后依然成立；正是因为这样，本节才只讨论 width 和两侧的外边距，而没有涉及内边距或边框。不管把 box-sizing 设为什么值，本节及下一节讨论的 `width: auto` 处理方式不变。box-sizing 定义的框体包含哪些区域，设为不同的值时有所不同，但是对 auto 值的处理方式不变，因为 box-sizing 决定的是 width 从何处算起，而不是它与外边距的关系。

### 7.2.6 多个 auto

下面来看这三个属性（width、margin-left 和 margin-right）中有两个设为 auto 的情况。如果两侧的外边距都设为 auto,如下述代码所示，那么外边距的长度相等，元素在父元素内居中显示，如图 7-13 所示

```css
div {
  width: 500px;
}
p {
  width: 300px;
  margin-left: auto;
  margin-right: auto;
}
/* each margin is 100 pixels wide, because (500-300)/2 = 100 */
```

<!-- <Figures figure="7-13">Setting an explicit width</Figures> -->

在常规流动方式下，若想让元素在块级框中居中显示，止明的方式走把网侧的外边距设为同样的宽度（弹性盒和概格布局中还有其他方法，不过这不在本节的讨论范围之内）。

此外，还可以把某一边的外边距和 width 设为 auto。此时，设为 auto 的那个外边距等于零。

```css
div {
  width: 500px;
}
p {
  margin-left: auto;
  margin-right: 100px;
  width: auto;
} /* left margin evaluates to 0; width becomes 400px */
```

width 则被设为填满容纳块所需的值。对上例来说，width 的值为 400 像素，如图 7-14 所示。

<!-- <Figures figure="7-14">What happens when both the width and right margin are auto</Figures> -->

最后，如果这三个属性都设为 auto 呢？答案是，两侧的外边距被设为零，而 width 则要多宽有多宽。这跟默认情况是一样的，即两侧的外边距和宽度都不明确声明值；此时，外边距默认为零，而 width 默认为 auto。

注意，因为横向外边距不折叠，所以父元素的内边距、边框和外边距可能会影响子代。这影响不太直接，例如元素的外边距（等）可能导致子元素有偏移。下述样式的结果如图 7-15 所示。

```css
div {
  padding: 50px;
  background: silver;
}
p {
  margin: 30px;
  padding: 0;
  background: white;
}
```

<!-- <Figures figure="7-15">Offset is implicit in the parent’s margins and padding</Figures> -->

### 7.2.7 负外边距

目前来看，一切都相当简单，但是为何我之前说有些地方是复杂的呢？这是因为外边距还有一种取值，即负值。是的，外边距可以设为负值。设为负值能实现一些有趣的效果。

还记得吗，七个横向属性之和始终等于父元素的 width。只要这几个属性的值都大于或等于零，元素就不可能比父元素的内容区宽。然而，下述样式便出现意外了，如图 7-16 所示：

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: auto;
  margin-right: -50px;
}
```

<!-- <Figures figure="7-16">Wider children through negative margins</Figures> -->

你没看错，子元素比父元素宽了！用算式计算，结果是对的：

```
10px + 0 + 0 + 540px + 0 + 0 − 50px = 500px
```

其中，540px 对应于 `width: auto`,即满足算式左右两边所需的值。尽管子元素超出了父素，但是这里并没有违背规范，因为七个属性的值加在一起等于总宽度。这是语义上的技俩，但却是正确的行为。

下面，加上边框：

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: auto;
  margin-right: -50px;
  border: 3px solid gray;
}
```

此时，变化发生在 width 的计算结果上

```
10px + 3px + 0 + 534px + 0 + 3px − 50px = 500px
```

如果再加上内边距，width 的值还会变小。

反过来，设为 auto 的右外边距也可能得到负值。比如其他属性设为特定的值时，为了满足元素不能比容纳块宽的要求，右外边距就有可能为负值。以下述样式为例：

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: 10px;
  width: 600px;
  margin-right: auto;
  border: 3px solid gray;
}
```

此时，算式要这样列：

```
10px + 3px + 0 + 600px + 0 + 3px − 116px = 500px
```

右外边距的计算结果为-116px。即便明确声明为其他具体的值，右外边距也会被强制设为-116px,因为规则就是这样制定的：倘若元素的尺寸出现过约束，右外边距要被重置为满足算式所需的任何值（如果是从右至左书写的语言，重置的将是左外边距）。

再看一个例子，结果如图 7-17 所示，这里把左外边距设为负值：

```css
div {
  width: 500px;
  border: 3px solid black;
}
p.wide {
  margin-left: -50px;
  width: auto;
  margin-right: 10px;
  border: 3px solid gray;
}
```

<!-- <Figures figure="7-17">Setting a negative left margin</Figures> -->

左外边距为负值时，段落不仅从 div 元素的边框溢出了，还从浏览器窗口的左边溢出了。

注意，内边距、边框和内容宽度（及高度）不能为负值。只有外边距的值可以小于零。

### 7.2.8 百分数

宽度、内边距和外边距设为百分数时，基本的规则依然适用。其实，这些属性的值设为长度值还是百分数并没什么关系。

百分数有时很有用，假设我们想把元素的内容区宽度设为容纳块的三分之二，左右内边距各为 5%,左外边距为 5%,余下的空间都留给右外边距。此时，可以这样声明：

```html
<p
  style="width: 67%; padding-right: 5%; padding-left: 5%; margin-right: auto;
 margin-left: 5%;"
>
  playing percentages
</p>
```

这里的右外边距将是容纳块宽度的 18% = (100%-67%-5%-5%-5%).

然而，百分数和长度单位混在一起使用就不那么容易理清了，以下述标记为例：

```html
<p
  style="width: 67%; padding-right: 2em; padding-left: 2em; margin-right: auto;
 margin-left: 5em;"
>
  mixed lengths
</p>
```

此时，元素框可以这样定义：

```
5em + 0 + 2em + 67% + 2em + 0 + auto = containing block width
```

为了确保右外边距的计算结果为零，元素的容纳块必须是 27.272727em 宽（元素的内容区是 18.272727em 宽）。假使容纳块比这宽，右外边距的计算结果会变成正值，客纳块比这窄的话，右外边距的计算结果则为负值。

如果混用不同的长度单位，情况更复杂。例如：

```html
<p
  style="width: 67%; padding-right: 15px; padding-left: 10px;
 margin-right: auto;
 margin-left: 5em;"
>
  more mixed lengths
</p>
```

为了避免情况一直复杂下去，边框不接受百分数，只能设为长度值。这样限制的基本原因是，只使用百分数其实无法创建完全弹性的元素，除非不添加边框，或者使用某种实验性的方案，例如弹性盒布局。

### 7.2.9 置换元素

目前，我们所讲的都是常规流动模式下非置换块级框的横向格式化，块级置换元素的处理方式要简单些，前面针对非置换块级框的规则都成立，不过有个例外 width 为 auto 时，置换元素的 width 等于内容自身的宽度。如果图像自身的宽度为 20 像素，下述示例中的图像将为 20 像素宽：

```html
<img src="smile.svg" style="display: block; width: auto; margin: 0;" />
```

如果图像自身的宽度为 100 像素，那么它就占 100 像素宽。

明确为 width 提供一个值可以覆盖这个规则。比如说，修改前例，同一个图像显示三次。每次设定的宽度都不同：

```html
<img src="smile.svg" style="display: block; width: 25px; margin: 0;" />
<img src="smile.svg" style="display: block; width: 50px; margin: 0;" />
<img src="smile.svg" style="display: block; width: 100px; margin: 0;" />
```

如图 7-18 所示。

注意，元素的高度随之增加了。如果置换元素的 width 与自身宽度不同，height 的值会按比例变化，除非明确设定 height 的值。反过来亦然，如果设定了 height,而把 widt 设为 auto,那么宽度会随着高度按比例变化。

<!-- <Figures figure="7-18">Changing replaced element widths</Figures> -->

既然提到高度了，下面就来讨论常规流动模式下块级框的纵向格式化。

### 7.2.10 纵向格式化

块级框的纵向格式化与横向格式化类似，也有一些有趣的行为。元素的内容决定元素的默认高度。内容的宽度对高度也有影响，例如，段落越窄，为了包含内部的所有内容，高度就越高。

通过 CSS 可以为任何块级元素设定具体的高度。这么做得到的结果取决于多个因素。假设指定的高度大于显示内容所需的高度：

```html
<p style="height: 10em;"></p>
```

此时，多出的高度看起来像是内边距。再假设指定的高度小于显示内容所需的高度：

```html
<p style="height: 3.33em;"></p>
```

那么，浏览器要提供查看全部内容的方式，而且前提是不增加元素框的高度。如果元的内容比框体高，用户代理的具体行为取决于 overflow 属性。这种情况下的两种显示方式如图 7-19 所示。

在 CSS1 中，对置换元素来说（例如图像）,用户代理可以忽略 auto 之外的任何高度值在 CSS2 及以上版本中，height 的值不再允许忽略，唯一的例外是涉及百分数的特殊情况。这一点稍后讨论。

与 width 一样，height 默认定义内容区的高度，而不是元素框可见区域的高度。元素框的上下内边距，边框和外边距在高度的基础上增加，除非 box-sizing 属性的值不是 content-box.

<!-- <Figures figure="7-19">Heights that don’t match the element’s content height</Figures> -->

### 7.2.11 纵向格式化属性

与横向格式化一样，纵向格式化也涉及七个属性：margin-top、border-top、padding-top、height、padding-bottom、border-bottom 和 margin-bottom。这些属性作用的区域见图 7-20.

这七个属性的值加在一起必须等于块级框的容纳块的高度。通常，这是块级框父元素的 height 值（因为块级元素的父元素几乎都是块级元素）。

这七个属性中只有三个可以设为 auto（元素的高度和上下外边距）。上下内边距和边框必须设为具体的值，否则取默认值零（假设未声明边框式样）。如果设定了边框式（border-style）,那么边框的宽度默认为不具体的 medium,图 7-21 展示了元素框的哪些部分可以设为 auto,而哪些部分不能。

奇怪的是，在常规流动模式下，如果把块级框的 margin-top 或 margin-bottom 设为 auto,二者都自动计算为 0。如此看来，常规流动模式下的元素无法轻易在容纳块中向居中。这也意味着，如果把元素的上下外边距设为 auto,最终会被重置为 0,不会体现在元素框上。

定位元素和弹性盒元素对设为 auto 的上下外边距的处理方式有所不同。

<!-- <Figures figure="7-20">The seven properties of vertical formatting</Figures> -->

height 属性要么设为 auto,要么设为某种类型的非负值，决不能小于零。

### 7.2.12 百分比高度

我们已经知道如何处理值为具体长度的高度，下面花点时间讨论百分数高度。在常规流动模式下，如果把块级框的高度设为百分数，百分数是相对框体的容纳块的高度而言的。对下述标记来说，段落的高度将是 3em:

```html
<div style="height: 6em;">
  <p style="height: 50%;">Half as tall</p>
</div>
```

既然把上下外边距设为 auto 得到的外边距为零，那么针对这个例子，若想纵向居中元素，只能把上下外边距都设为 25%。不过，这样只能把框体居中，里面的内容不居中。

<!-- <Figures figure="7-21">Vertical properties that can be set to auto</Figures> -->

然而，如果未明确声明容纳块的高度，那么百分数高度将被重置为 auto。在上例中，如果把 div 的 height 改为 auto,那么段落的高度将与 div 一样：

```html
<div style="height: auto;">
  <p style="height: 50%;">NOT half as tall; height reset to auto</p>
</div>
```

这两种情况如图 7-22 所示（段落边框和 div 边框之间的空白是段落的上下外边距）。

<!-- <Figures figure="7-22">Percentage heights in different circumstances</Figures> -->

继续讨论之前，仔细看一下图 7.22 中的第一个示例，即那个占据一半高度的段落。看起来，那个侵露占据一半高度，但是并没有以同居中。这是因为容纳块 div 的高度为 6em,占据一半高度的段落是 3em 高。但是，段落的上下外边距均为 1em,所以整个概体的高度是 5em。这意味着，段落可见框体底部到 div 底边的距离是 2em,而不是 1em,初看起来，这可能有点奇怪，但是了解细节之后你便会知道这是合理的。

### 7.2.13 自动调整高度

在常规流动模式下，声明 `height: auto` 的块级框是最简单的，此时，框体的高度恰好能放得下里面的内容，常规流动模式下的块级框如果高度是自动调整的，而且子代都是块级元素，那么默认的高度是从最上边那个块级子代元素的上边框外侧到最下边那个块级子代元素的下边框外侧之间的距离。因此，子元素的外边距“游离”在所属元素的外部（这个行为在下一节说明）。

然而，如果块级元素有上内边距或下内边距，或者有上边框或下边框，那么其高度是从最上边那个子元素的上外边距的外边界到最下边那个子元素的下外边距的外边界之间的距离。

```html
<div
  style="height: auto;
 background: silver;"
>
  <p style="margin-top: 2em; margin-bottom: 2em;">A paragraph!</p>
</div>
<div
  style="height: auto; border-top: 1px solid; border-bottom: 1px solid;
 background: silver;"
>
  <p style="margin-top: 2em; margin-bottom: 2em;">Another paragraph!</p>
</div>
```

这两种情况如图 7-23 所示。

如果把前例中的边框改为内边距，div 元素的高度不变，外边距依然算在其中。

<!-- <Figures figure="7-23">Auto heights with block-level children</Figures> -->

### 7.2.14 折叠纵向外边距

纵向格式化的另一个重要特征是，相邻的纵向外边距会折叠，只有外边距有这种折叠行为。内边距和边框（如果有的话）,绝不与任何区域折叠。

通过纵向罗列的无序列表最易说明外边距折叠行为。假设把下述声明应用到一个有五个项目的列表上：

```css
li {
  margin-top: 10px;
  margin-bottom: 15px;
}
```

每个列表项目都有 10 像素的上外边距和 15 像素的下外边距，然而，渲染时，相邻的两个列表项目之间的距离是 15 像素，而不是 25 像素。这是因为，相邻的外边距在纵轴上折叠了。换句话说就是，较小的外边距被较大的外边距消去了。图 7-24 展示了折叠和未折叠外边距之间的差别。

目前实现的用户代理都会折叠相邻的纵向外边距，如图 7-24 中的第一个列表所示，因此列表项目之间的空白是 15 像素。第二个列表展示的是用户代理不折叠外边距时的情况，此时列表项目之间的空白是 25 像素。

如果你不喜欢“折叠”这个词，可以换成“重叠”，虽然外边距并不真的会重叠，但是你可以借助下述比拟想象一下这其中到底发生了什么。

假设每个元素（例如段落）是一小片纸，元素中的内容写在纸上，纸片四周有一些透明复料，表示外边距。先把第一片纸（假如表示 h1 元素）放在画布上，然后在下面再放一片纸（一个段落）,向上移动，直到其中一片纸的边缘与另一片纸的边缘接触为止。如果第一片纸的下部有半英寸塑料，第二片纸的上部有三分之一英寸型料，那么两片纸移到一起时，第一片纸的塑料将碰到第二片纸的上边缘。两片纸平稳放到画布上之后，纸四周的塑料就重叠了。

<!-- <Figures figure="7-24">Collapsed versus uncollapsed margins</Figures> -->

多个外边距同时出现时也会折叠，例如在列表的末尾。假设把下述规则应用到前例上：

```css
ul {
  margin-bottom: 15px;
}
li {
  margin-top: 10px;
  margin-bottom: 20px;
}
h1 {
  margin-top: 28px;
}
```

列表中最后一个项目的下外边距为 20 像素，u1 元素的下外边距为 15 像素，而后面的 h1 元素的上外边距为 28 像素。因此，折叠外边距之后，最后一个 1i 元素的底部与 h1 元素的顶部之间的距离为 28 像素，如图 7-25 所示。

<!-- <Figures figure="7-25">Collapsing in detail</Figures> -->

你可能还记得前一节的示例，为容纳块添加边框或内边距之后，子元素的外边距便包含其中，现在我们在前述规则的基础上为 u1 元素添加边框，看一下效果：

```css
ul {
  margin-bottom: 15px;
  border: 1px solid;
}
li {
  margin-top: 10px;
  margin-bottom: 20px;
}
h1 {
  margin-top: 28px;
}
```

这样修改之后，11 元素的下外边距在父元素（ul）的范围内。此时，只有 ul 和 h1 之间的外边距会出现折叠，如图 7-26 所示。

<!-- <Figures figure="7-26">Collapsing (or not) with borders added to the mix</Figures> -->

### 7.2.15 负外边距和折叠

负外边距对纵向格式化有一定影响，比如会影响外边距的折叠。如果两个相邻的外边距都是负值，浏览器取其中绝对值较大的那个，然后从正外边距中减去它的绝对值。也是说，把负值与正值相加，得到的结果为两个元素之间的距离。图 7-27 给出了两个具体的例子。

<!-- <Figures figure="7-27">Examples of negative vertical margins</Figures> -->

注意上下外边距为负时出现的“上移”现象。这与横向外边距为负时从父元素中溢出没什么区别。以下述规则和标记为例：

```css
p.neg {
  margin-top: -50px;
  margin-right: 10px;
  margin-left: 10px;
  margin-bottom: 0;
  border: 3px solid gray;
}
```

```html
<div
  style="width: 420px; background-color: silver; padding: 10px;
 margin-top: 50px; border: 1px solid;"
>
  <p class="neg">
    A paragraph.
  </p>
  A div.
</div>
```

从图 7-28 中可以看出，由于上外边距为负，那个段落上移了，注意，div 元素中那个段落后面的内容也向上移了 50 像素。其实，那个段落后面常规流动模式下的每个元素会向上移 50 像素。

<!-- <Figures figure="7-28">The effects of a negative top margin</Figures> -->

对比一下下述标记与图 7-29 中显示的效果：

```css
p.neg {
  margin-bottom: -50px;
  margin-right: 10px;
  margin-left: 10px;
  margin-top: 0;
  border: 3px solid gray;
}
```

```html
<div style="width: 420px; margin-top: 50px;">
  <p class="neg">
    A paragraph.
  </p>
</div>
<p>
  The next paragraph.
</p>
```

<!-- <Figures figure="7-29">The effects of a negative bottom margin</Figures> -->

出现图 7-29 中这种情况的原因是，div 后面的元素是参照 div 的底边放置的。可以想像，div 的底边其实在内部那个段落视觉上的底边上部，而 div 后面的元素是从这一位置计算与 div 底边的距离的。对上述规则来说，这个结果是正确的。

下面再看一个例子，这里列表项目、无序列表和段落的外边距都会折叠。无序列表和段落的外边距均为负值，如下所示：

```css
li {
  margin-bottom: 20px;
}
ul {
  margin-bottom: -15px;
}
h1 {
  margin-top: -18px;
}
```

两个负外边距中绝对值较大的那个（-18px）与最大的正外边距（20px）相加，得到 20px-18px=2px。因此，列表项目内容区的底边到 h1 元素内容区的顶边之间只像素，如图 7-30 所示。

如果负外边距导致元素重叠，很难分请哪个元素在上边。你可能注意到了，本节所举的例子都没有使用背景色。如果这么做了，后续元素的背景色可能会遮盖前面元素的内容。这是可以预见的，因为测览器是从头到尾按顺序演染元素的，在常规流动模式下，如果文档中位于后面的元素与前面的元素重叠了，理应意盖元素的内容。

<!-- <Figures figure="7-30">Collapsing margins and negative margins, in detail</Figures> -->

### 7.2.16 列表项目

到表项目有些独特的规则。列表项目前通常有个记号，例如小圆点或数字，但这个记号其实不在列表项目的内容区中，如图 7-31 所示。

<!-- <Figures figure="7-31">The content of list items</Figures> -->

在文档的布局方便，CSS1 没有详细规定记号的位置和效果。鉴于此，CSS2 引入了专门解决这个问题的属性，例如 marker-offset。然而，由于没有多少浏览器实现，以及想法的变化，CSS2.1 又移除了这个属性；不过，已经有了新的想法（可能还没确定具体的句法）。因此，记号的位置远非创作人员能控制的，至少目前是这样。

记号可以放在列表项目内容区的外部，也可以作为行间内容，放在内容区的开头，这取决于 list-style-position 属性的值。如果把记号放在内部，列表项目与周围元素之间的关系就跟块级元素一模一样，如图 7-32 所示。

<!-- <Figures figure="7-32">Markers inside and outside the list</Figures> -->

如果把记号放在内容区外部，记号与内容区的左边（假设是由左至右书写的语言）有一定的距离。不管如何调整列表的样式，记号与内容区边界之间的距离始终不变。有时，记号甚至可能超出列表元素本身，如图 7-32 所示。

注意，与常规的块级框一样，列表项目框为其后代定义容纳块。

## 7.3 行内元素

除块级元素之外，行内元素是最为常见的。行内元素的相关属性能实现更有趣的效果。常见的行内元素有`em`和`a`等非置换元素，以及置换元素——图像。

注意，本节所述的行为均不适用于表格元素。表格及其内容的行为与块级元素和行内元案有极大的差异，因此 CSS2 引入了专门的新属性和行为。本书不讨论表格装饰，因为这是一个全新的领域，而且异常繁琐。

行内的非置换元素和置换元素有些许差异，在讲解行内元素构成的过程中将逐一说明。

### 7.3.1 行布局

首先要明白行内内容是如何布局的，块级元素相对简单，生成的块级框通常不与其他内容共处一行，行内元素就没这么简单了，不信的话，你可以看一下块级元素（例如一个段落）的内部，你可能会有这样的疑问：这些文本行是如何显示出来的呢？为什么要这样排列呢？可以采用何种方式控制呢？

为了弄请文本行是如何生成的，下面以一个文本行特别长的元素为例，如图 7-33 所示。注意，我们把整行文本放在一个 span 元素中，并为其设定了边框：

```css
span {
  border: 1px dashed black;
}
```

<!-- <Figures figure="7-33">A single-line inline element</Figures> -->

图 7.33 所示的情况非常简单，就是放在块级元素中的一个行内元素，说自了，这与只有两个单词的段落设什么大的区别。这里唯一的区别是，图 7-33 中的单词数量多了些，而且放在一个行内元素（span）中。

先从我们熟悉的概念入手，定义元素的宽度。有了宽度的限制，这行文本将分成几行显示，如图 7-34 所示。

<!-- <Figures figure="7-34">A multiple-line inline element</Figures> -->

其实我们没做什么，只是把单行文本分成了多行，从上到下排列着显示。

在图 7-34 中，各行的边框恰巧与上下边重合，这种情况仅当行内文本没有内边距才会发生。注意，边框稍微有点重合。例如，第一行的下边框正好位于第二行上边框的下方。这是因为边框在各行外部的下一像素（假设你用的是显示器）处绘制，既然行与行之间是相互接触的，那么边框肯定会像图 7-34 中那样重叠。

如果调整 span 元素的样式，为其设定背景色，那么各行的位置就比较明晰了，如图 7.35 所示，图中有四个段落，每个段落的 text-align 值有所不同，而且段落中的各行都有背景色。

图中的灰色虚线是段落内容区的边界，可以看出，不是每一行都能延伸到段落的边界。对左对齐那一段来说，每一行都靠左边界显示，而行尾在断行处结束。右对齐那段情况正好相反。对居中对齐那段而言，每一行的中线与段落的中线对齐。

最后一段的 text-align 属性值为 justify,因此每一行的宽度与段落的内容区相等，而且都到达了边界处。然而，由于每一行自身的宽度与段落的宽度是不同的，所以要调整字母及单词之间的距离。鉴于此，两端对齐的文本，其 word-spacing 属性的值可能会被覆盖（如果 letter-spacing 属性的值是一个长度，那就无法被覆盖）。

以上就是文本行排列的最简单情况。然而，你即将发现，行内格式化模型比这复杂得多。

<!-- <Figures figure="7-35">Showing lines in different alignments</Figures> -->

### 7.3.2 基本属于和概念

深入讨论之前，先学习有关行内布局的一些基本术语。这对理解后续章节的内容尤为重要。

1. 匿名文本`Anonymous text`

不在任何行内元素中的字符串。例如，在`<p>I'm<em>so</em>happy!</p>`标记中，`I'm`和`happy!`是匿名文本。注意，空格也是匿名文本的一部分，因为空格也是一种字符。

2. 字体框`Em box`

由字体具体定义，也叫字符框。字形可能比字体框高或矮。CSS 中的 font-size 属性控制字体框的高度。

3. 内容区`Content area`

对非置换元素而言，内容区有两种定义，CSS 规范允许用户代理选择其中一个实现。内容区可以是各字符的字体框连在一起构成的方框，也可以是元素中各字符的字形合在一起构成的方框。简单起见，本书采用前者。对置换元素来说，内容区是元素自身的高度加上内外边距和边框。

4. 行距`Leading`

行距是 font-size 和 line-height 之差。二者之间的差值除以 2 之后分别添加到内容区的上部和下部。内容区多出来的这部分空间叫半行距（显然的）。只有非置换元素有行距。

5. 行内框`Inline box`

内容区加行距后得到的方框。对非置换元素来说，行内框的高度正好等于 line-height 属性的值。对置换元素而言，行内框的高度等于内容区的高度，因为置换元素没有行距。

6. 行框`Line box`

过一行中各行内框最高点和最低点的方框。也就是说，行框的顶边过最高那个行内框的顶边，行框的底边过最低那个行内框的底边。

此外，CSS 还定义了一些行为和有用的概念：

- 内容区相当于块级框的内容框。
- 行内元素的背景填充在内容区加内边距所在的区域里。
- 行内元素的边框在内容区外的内边距外侧。
- 非置换行内元素的内边距、边框和外边距在对应的方框上没有纵向效果，即对行内框（及元素所在的行框）的高度没有影响。
- 然而，置换元素的外边距和边框对行内框的高度有影响，进而对元素所在的行框的高度也有影响。

还要注意一点：行内框在一行中纵向对齐的方式由 vertical-align 属性决定。

在继续之前，先来看一下构建行框的具体步骤。这一过程能让你了解一行中的各部分是如何决定行高的。

一行中各元素的行内框高度是这样确定的：

1. 确定行内各非置换元素和置名文本的 font-size 和 line-height 值，后者减去前者，得到行距。行距除以 2,分别添加到字体框的上部和下部。
2. 确定各置换元素的 height、margin-top、margin-bottom、padding-top、padding-bottom、border-top-width 和 border-ttom-width 值，各值相加。
3. 确定各内容区在一行的基线上方和下方分别超出多少，这不是件简单的事，你要知道各元素和置名文本的基线在何处，以及一行的基线在何处，然后把它们对齐。另外，要把置换元素的底边与一行的基线对齐。
4. 确定设定了 vertical-align 属性的元素纵向偏移有多少。这是为了查明元素的行内框向上或向下移动多少，因为纵向对齐改变了元素与基线之间的距离。
5. 知道所有行内框的位置之后，计算行框的高度：基线与最高那个行内框顶边之间的距离加上基线与最低那个行内框底边之间的距离。

下面详细分析整个过程。这是正确装饰行内内容的关键。

### 7.3.3 行内格式化

首先要知道，不管有没有显式声明，所有元素都有 line-height 值。这个值在很大程度上影响着行内元素的显示，因此要特别注意。

那么，一行的高度是如何确定的呢？一行的高度（即行框的高度）由其内部的元素及其他内容（例如文本）的高度决定。注意，line-height 影响行内元素和其他行内内容，但不影响块级元素，至少没有直接影响。块级元素可以设定 line-height 值，但是只对块级元素中的行内内容有视觉影响。以下面这个没有内容的段落为例：

```html
<p style="line-height: 0.25em;"></p>
```

因为这个段落没有内容，没什么可显示的，所以我们看不到任何内容。不管这个段落的 line-height 值是多少，是 0.25em 也好，是 25in 也好，没有任何区别，没有内容就没有行框。

块级元素当然可以有 line-height 值，但是这个值将应用于块级元素内部的内容上（不管在不在行内元素中）。从某种程度上讲，块级元素中的各文本行本身就是行内元素，不论是否真的在行内标签中都是如此。如果愿意，可以想象成有个虚构的标签，如下所示：

```html
<p>
  <line>This is a paragraph with a number of</line>
  <line>lines of text which make up the</line>
  <line>contents.</line>
</p>
```

尽管 line 标签并不存在，但是段落的行为就像有这些标签一样，每行文本都从段落上能承样式。为了避免麻烦，你可以为块级元素设定 line-height 值，这样就无需为每个行内元素（虚构的或真实的）设定 line-height 值了。

通过虚构的 line 标签，我们明确了为块级元素设定 line-height 值的效果。根据 css 规范，为块级元素设定 line-height 值的作用是为块级元素中的内容设定行框的最小高度。例如，`p.spacious {line-height: 24pt;}`的作用是把各行框的最小高度设为 24 点。理论上讲，只有行内元素能继承行高时，其中的内容才会继承。但是，多数文本不在行内元素中。如果你假设各行都在虚构的 line 元素中，这就说得通了。

### 7.3.4 行内非置换元素

在现有的格式化知识基础上，下面我们来讨论只含非置换元素（或置名文本）的行。了解这一点之后，你便能更好地理解行布局中非置换元素和置换元素之间的区别了。

**行框的构成**

首先，对非置换元素或匿名文本来说，font-size 值决定内容区的高度。如果行内元素的 font-size 为 15px,那么其内容区的高度就是 15 像素，因为元素中的所有字体框高度都是 15 像素，如图 7-36 所示。

<!-- <Figures figure="7-36">Em boxes determine content area height</Figures> -->

接下来要考虑的是元素的 line-height 值，以及它与 font-size 值之差。如果行内非置换元素的 font-size 为 15px、line-height 为 21px,那么二者之差为 6 像素。用户代理把这 6 像素一分为二，一半添加到内容区上部，一半添加到内容区下部，得到行内框。

<!-- <Figures figure="7-37">Content area plus leading equals inline box</Figures> -->

假设有下述标记：

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  which is <strong style="font-size: 24px;">strongly emphasized</strong> and
  which is<br />
  larger than the surrounding text.
</p>
```

在这个示例中，多数文本的 font-size 为 12px,但是有个行内非置换元素的字号为 24px。然而，所有文本的 line-height 都是 12px,因为 line-height 是会被继承的属性。因此，strong 元素的 line-height 仍是 12px。

鉴于此，对那些 font-size 和 line-height 都为 12px 的文本来说，内容高度不变（因为 12px 减 12px 等于零）,所以行内框的高度为 12 像素。然而，对加粗文本而言，line-height 和 font-size 之差为-12px。除以 2 之后得到半行距（-6px）,然后分别添加到内容区的上部和下部，得到行内框。因为添加的是负值，所以行内框的最终高度为 12 像素。这个 12 像素高的行内框在 24 像素高的内容区里纵向居中显示，因此行内框比内容区小一点。

目前来看，我们对每段文本的分析方式是一样的，而且最终得到的行内框高度相同，但事实要比这复杂。第二行里的各行内框虽然高度相等，但是由于文本都是与基线对齐的，各部分文本并不是平齐的（见图 7-38）。

因为行内框决定着行框的总体高度，所以各行内框的位置特别重要。我们知道，行框的高度是指从最高那个行内框的顶边到最低那个行内框的底边之间的距离，而行框的顶边与前一行的底边是紧挨在一起的，图 7-38 中的文本所在的段落如图 7-39 所示。

<!-- <Figures figure="7-38">Inline boxes within a line</Figures> -->

<!-- <Figures figure="7-39">Line boxes within a paragraph</Figures> -->

从图 7.39 可以看出，中间那一行比其他两行要高，但是还不足以包含全部文本。置名文本所在的行内框决定行框的底边位置，而加粗元素所在的行内框定位行框的顶边，因为那个行内框的顶边在元素的内容区内部，所以加粗元素的内容超出了行框，叠加到其他行框上了。最终的结果是，那部分文本显得不太协调。

> 稍后将说明应对这种行为的方法，以及实现相同基线间距的方法。

**纵向对齐**

改变行内框的纵向对齐方式后，仍以相同的过程确定高度，假设我们把 strong 元素的纵向对齐设为 4px:

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  which is
  <strong style="font-size: 24px; vertical-align: 4px;"
    >strongly emphasized</strong
  >
  and that is<br />
  larger than the surrounding text.
</p>
```

这个小小的改动把 strong 元素向上抬升了 4 像素，而且是内容区与行内框一起移动。现在，strong 元素所在的行内框的顶边是一行中最高的，因此此次修改纵向对齐还把行框的顶边向上移了 4 像素，如图 7-40 所示。

<!-- <Figures figure="7-40">Vertical alignment affects line box height</Figures> -->

再来看一种情况。这里，我们在加粗文本那一行里又添加了一个行内元素，而且不是与基线对齐的：

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>,<br />
  plus other text that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top;">tall</span> and is<br />
  larger than the surrounding text.
</p>
```

结果与之前一样，中间那一行的行框比其他行框要高。然而，请注意“tall”的对齐方式，如图 7-41 所示。

<!-- <Figures figure="7-41">Aligning an inline element to the line box</Figures> -->

这里，“tall”文本所在的行内框的顶边与行框的顶边对齐。因为“tall”文本的 font-size 和 line-height 值相等，所以内容区与行内框的高度相等。然而，再看下面这种情况：

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>,<br />
  plus other text that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top; line-height: 2px;">tall</span> and is<br />
  larger than the surrounding text.
</p>
```

现在，“ul”文本的 line-height 比 font-size 小，因此其行内框的高度比内容区小。到的精果如图 7-42 所示，这处细险的变化将改变文本的位置，因为其行内框的顶边要与行框的顶边对齐。此时得到的结果如图 7-42 所示。

此外，还有可能把“tall”文本的 line-height 设定的比 font-size 大。例如

```html
<p style="font-size: 12px; line-height: 12px;">
  This is text, <em>some of which is emphasized</em>, plus other text<br />
  that is <strong style="font-size: 24px;">strong</strong> and
  <span style="vertical-align: top; line-height: 18px;">tall</span> and that
  is<br />
  larger than the surrounding text.
</p>
```

<!-- <Figures figure="7-42">Text protruding from the line box (again)</Figures> -->

我们把“tall”文本的 line-height 设为 18px,因此 line-height 和 font-size 之差为 6 像素。半行距（3 像素）添加到内容区上之后，得到的行内框为 18 像素高。这个行内的顶边与行框的顶边对齐。类似地，如果 vertical-align 的值为 bottom,那么行内元素的行内框的底边将与行框的底边对齐。

下面使用本章采用的术语描述 vertical-align 各个关键字值的效果：

- top：元素行内框的顶边与所在行框的顶边对齐。
- bottom：元素行内框的底边与所在行框的底边对齐。
- text-top：元素行内框的顶边与父元素内容区的顶边对齐。
- text-bottom：元素行内框的底边与父元素内容区的底边对齐。
- middle：元素行内框的纵向中点与父元素基线以上 0.5ex 处的点对齐。
- super：向上移动元素的内容区和行内框。无法指定移动距离，不同的用户代理之间可能有区别。
- sub：与 super 类似，只不过是向下移动。
- `<percentage>`：向上或向下移动元素，移动的距离等于声明的百分数乘以元素的 line-height 值。

**控制行高**

读过前面几小节我们知道，修改行内元素的 line-height 值可能会导致一行中的文本控制行高与另一行重叠。但是，之前都是修改单个元素的行高。那么有没有一般性的方法，能让 line-height 的值不导致行之间有重叠呢？

一种方法是为字号有变化的元素设定单位为 em 的行高。例如：

```css
p {
  line-height: 1em;
}
big {
  font-size: 250%;
  line-height: 1em;
}
```

```html
<p>
  Not only does this paragraph have "normal" text, but it also<br />
  contains a line in which <big>some big text</big> is found.<br />
  This large text helps illustrate our point.
</p>
```

这里为 big 元素设定的 line-height 值增加了行框的整体高度，为显示 big 元素提供了足够的空间，不会再出现文本重叠，而且也没有改变段落中其他几行的行高。我们把 big 元素的 line-height 值设为 1em,因此 big 元素的行高将与字号相等。还记得吗，line-height 相对元素自身的 font-size 而言，跟父元素没关系。结果如图 7-43 所示。

<!-- <Figures figure="7-43">Assigning the line-height property to inline elements</Figures> -->

前几小节的内容一定要理解，添加边框后情况将变得更加复杂。假如我们想为超链接直接添加 5 像素宽的边框：

```css
a:link {
  border: 5px solid blue;
}
```

如果不把 line-height 设为足够大的值，边框将遮盖其他行。为了避免这种情况发生，我们可以通过 line-height 增加未访向链接的行内框尺寸，这与之前处理 big 元素的方式差不多。这里，我们只需让 line-height 的值比链接的字号大 10 像素即可。然而，假若我们不知道链接的字号为多少像素，就很难保证这一点，不仅仅是段落中带边框的超链接。

另一种方法是增加整个段落的 line-height 值。这样整个段落中的每一行都受影响，而不仅仅是段落中带边框的超链接。

```css
p {
  line-height: 1.8em;
}
a:link {
  border: 5px solid blue;
}
```

因为每一行上下都增加了一定的空白，所以超链接四周的边框不会与其他行出现重叠，如图 7-44 所示。

这里之所以可以使用这种方法，是因为所有文本的字号都相同。如果行内某个元素改变了行框的高度，那么边框情况可能也会发生变化。请看下述规则：

```css
p {
  font-size: 14px;
  line-height: 24px;
}
a:link {
  border: 5px solid blue;
}
big {
  font-size: 150%;
  line-height: 1.5em;
}
```

根据上述规则，段落中 big 元素的行内框高为 31.5 像素（14×1.5×1.5）,这也是行框的高度。为了确保基线是对齐的，p 元素的 line-height 必须等于或大于 32px。

<!-- <Figures figure="7-44">Increasing line-height to leave room for inline borders</Figures> -->

**基线与行高**

行框的具体高度取决于行中各部分之间是如何对齐的。而这又在很大程度上取决于基线落在元素（或匿名文本）的什么位置，因为这个位置决定着行内框是如何摆放的，字体框中基线的位置在每个字体中不尽相同。这个信息内置在字体文件中，除了直接编辑字体文件之外，无法修改。

保持基线对齐更像是一种技艺，而非科学。如果使用相同的单位（例如 em）声明字号和行高，得到的基线很有可能是对齐的。然而，如果混用不同的单位，就困难得多，甚至是不可能的。写作本书时，为了让创作人员能够强制对齐基线，而不管行内有什么内容。相关人员已经提出提案，增加部分属性。如果提案获得通过，网络排版在某些方面将得到极大的简化。不过，提议的属性还都没有实现，离实际使用还远得很。

**按比例设定行高**

实践证明，设定 line-height 值的最佳方式是使用纯数字。这是因为纯数字相当于比例因子，而这个因子能被继承，而不计算为具体的值。假设我们想把文档中所有元素的 line-height 设为 font-size 的 1.5 倍，可以这么做：

```css
body {
  line-height: 1.5;
}
```

这个比例因子将沿着元素继承关系一层一层向下传递，作为各元素 font-size 值的乘数。因此，下述标记和规则得到的结果如图 7-45 所示。

```css
p {
  font-size: 15px;
  line-height: 1.5;
}
small {
  font-size: 66%;
}
big {
  font-size: 200%;
}
```

```html
<p>
  This paragraph has a line-height of 1.5 times its font-size. In addition, any
  elements within it
  <small>such as this small element</small> also have line-heights 1.5 times
  their font-size...and that includes <big>this big element right here</big>. By
  using a scaling factor, line-heights scale to match the font-size of any
  element.
</p>
```

在这个示例中，small 元素的行高为 15 像素，big 元素的行高为 45 像素（行高看起来有些大，不过却与页面的整体设计协调一致）。当然，如果不想让 big 元素中的文本占这么大的行距，可以为其设定 line-height 值，覆盖继承的比例因子：

```css
p {
  font-size: 15px;
  line-height: 1.5;
}
small {
  font-size: 66%;
}
big {
  font-size: 200%;
  line-height: 1em;
}
```

<!-- <Figures figure="7-45">Using a scaling factor for line-height</Figures> -->

还有一种方法（可能是最简单的方法）,即适当地设置样式，使行高恰好能包含行中的内容，没有多余的空间，此时可以把 line-height 设为 1.0,这样乘以 font-size 值之后得到的值与字号一样。因此，每个元素的行内框高度与内容区高度相同，而这正好是内容区的最小高度。

多数字体的字形之间都留有一定的空白，因为字符通常比字体框要小一些。但手写体（草书字体）例外，这种字体的字形往往比字体框大。

**加上盒模型属性**

从前面的讨论可以了解到，内边距、外边距和边框也都可以应用到行内非置换元素上。但是行内元素的这些属性并不影响行框的总体高度。如果为 span 元素设定边框，但不设定外边距或内边距，得到的结果如图 7-46 所示。

边框的边界由 font-size 控制，而不受 line-height 影响。也就是说，如果 span 元素的 font-size 值为 12px、line-height 值为 36px,那么内容区的高度为 12px,而边框出现在内容区的四周。

当然，我们可以为行内元素设定内边距，在边框和文本之间添加一些间距：

```css
span {
  padding: 4px;
}
```

注意，内边距并不影响内容区的高度，因此也不影响元素行内框的高度。类似地，行内元素的边框也不影响行框的生成和布局方式，如图 7-47 所示。

<!-- <Figures figure="7-46">Inline borders and line-box layout</Figures> -->

<!-- <Figures figure="7-47">Padding and borders do not alter line-height</Figures> -->

而外边距实际上不会添加到行内非置换元素的上部和下部，因此也就不影响行框的高度。不过行内元素的两端确受外边距的影响。

你应该还记得，行内元素基本上是按一行放置的，然后再分成多个部分。因此，行内元素的外边程会出现在元素的开头和结尾，即左外边距和右外边距。内边距也会出现在两端。因此，虽然内外边距（和边框）不影响行高，但是对元素内容的布局确有影响，们会在横向上把文本推开。其实，负的左右外边距能让文本靠的更近，甚至出现重叠，如图 7-48 所示。

行内元素可以想象成外国有一圈塑料的纸片。行内元素分成多行显示就相当于把一个大纸片剪成多个小纸片。然而，每个小纸片不再有额外的塑料边。小纸片上的塑料边还最初那个大纸片上的塑料边，所以看上去只是大纸片（行内元素）的开头和末尾有塑料边。至少，这是默认的行为。稍后你将发现，还有另一种行为。

<!-- <Figures figure="7-48">Padding and margins on the ends of an inline element</Figures> -->

如果行内元素有背景色和足量的内边距，导致行的背景出现重叠，那情况又如何呢？以下述规则为例：

```css
p {
  font-size: 15px;
  line-height: 1em;
}
p span {
  background: #faa;
  padding-top: 10px;
  padding-bottom: 10px;
}
```

span 元素的内容区高度为 15 像素，而且我们在内容区的上下各添加了 10 像素的内边距。额外增加的内边距没有改变行框的高度，原本这也没什么，但是有了背景色之后就不同了，此时得到的结果如图 7-49 所示。

CSS2.1 明确指出，行根是按文本出现在文档中的顺序绘制的：“这会导致后面行的边根出现在前面行的边框上，“背景色也是这个道理，如图 7-49 所示。而 CSS2 允许用于用户代理“修剪（即不渲染）边框和内边距区域”。因此，具体结果在很大程度上取决代理遵守的是哪个规范。

<!-- <Figures figure="7-49">Overlapping inline backgrounds</Figures> -->

**改变断行行为**

前一小节讲到，把一个行内非置换元素分成多行显示时，用户代理将其视为断成多块的一长行，每换一行就多一块，这其实是默认行为，可以通过 box-decoration-break 属性改变。

<!-- <Cards cards="box-decoration-break" /> -->

默认值 slice 的行为参见前一小节。另一个值 clone 把元素各片段视作单独的框。这意味着什么呢？请比较图 7-50 中的两个示例，除了 box-decoration-break 属性的值不同之外，标记和其他样式都一样。

二者之间有很多明显的区别，但也有一些不是那么显而易见，比如，后一个示例中每个片段都有内边距，包括断行处，而且，每个片段四周都有自成一体的边框，而没有被切断。

<!-- <Figures figure="7-50">Sliced and cloned inline fragments</Figures> -->

有一处不太显眼的区别，即二者之间背景图的位置是不同的，在切断版本中，背景图随其他内容一起被切断，因此源图只在其中一个片段里，而在克隆版本中，每个片段中都有一个源图。这意味着，如果背景图不重复，那么每个片段中都将出现一次，而不会只在一个片段中出现。

box-decoration-break 属性最常用于行内框，不过只要存在换行的情况都适用，例如在分页媒体中由于换页面打断的元素。此时，每个片段都是独立的一块。如果设定 box-decoration-break:等，多栏布局一样，如果因为换栏而把元素打断了，box-decoration-break 的值将影响渲染方式。

**字形与内容区**

你可能会尽量避免行内非置换元素的背景重叠，尽管如此，这种情况还是有可能发生，这取决于你所用的字体，根源在于字体的字体框和字形之间可能存在差异。事实是，多数字体的字体框高度与字形高度是不一致的。

所起来十分抽象，但这一点却有实际影响。CSS2.1 规范是这么说的：“内容区的高度应该由字体确定，但本规范并不规定具体细则。用户代理可以……使用字体框，也可以使用字体的最大上伸和下沿值（后一种方式能保证超出字体框上部或下部的字形仍然落在内容区中，但是不同的字体得到的行内框是不同的）。”

也就是说，行内非置换元素的“绘制区”由用户代理确定。如果用户代理把字体框的高度当作内容区的高度，那么行内非置换元素的背景高度等于字体框的高度（即 font-size 的值）,如果用户代理使用字体的最大上伸和下沿值，那么背景的高度可能比字体基高或量，此时，如果把行内非置换元素的行高设为 1em,背景依然会与其他行重叠。

### 7.3.5 行内置换元素

行内置换元素（例如图像）自身是有高度和宽度的。例如，一张图像有确定的高度和宽度值。因此，自身有高度的置换元素可能导致行框比正常情况下高。但这不影响行中任间元素的行高，包括置换元素自身。行框的高度将正好容纳置换元素及其盒模型属性设定的值。也就是说，置换元素的行内框包含整个元素，包括内容、外边距、边框和内边距。下述规则就是这种情况，结果如图 7-51 所示。

```css
p {
  font-size: 15px;
  line-height: 18px;
}
img {
  height: 30px;
  margin: 0;
  padding: 0;
  border: none;
}
```

尽管多出了一些空白，但是 line-height 的值并没有变，段落和图像自身都是如此。line-height 对图像的行内框没有影响。因为图 7-51 中的图像没有内边距、外边距和边框，所以它的行内框的高度与内容区相等，即 30 像素。

尽管如此，行内置换元素的 line-height 属性仍有值。这是为什么呢？因为纵向对齐时有这个值才能正确定位元素的位置。例如，vertical-align 属性的百分数值就是相对元素的 line-height 计算的。

```css
p {
  font-size: 15px;
  line-height: 18px;
}
img {
  vertical-align: 50%;
}
```

```html
<p>
  the image in this sentence <img src="test.gif" alt="test image" /> will be
  raised 9 pixels.
</p>
```

<!-- <Figures figure="7-51">Replaced elements can increase the height of the line box but not the value of line-height</Figures> -->

在这个示例中，图像继承的 line-height 值导致图像向上抬升 9 像素。可见，如果 line-height 没有值，那就不能把纵向对齐的值设为百分数了，在纵向对齐中，图像自身的高度没有任何意义，一切都由 line-height 的值决定。

然而，其他置换元素可能需要设定 line-height 值，让后代元素继承，SVG 图像就是这样，因为图中的文本通过 CSS 装饰。

**加上盒模型属性**

有前面的知识打底，在行内置换元素上应用外边距，边框和内边距的行为就好理解了。

应用在置换元素上的内边距和边框跟之前一样，内边距在内容四周添加空白，边框围绕在内边距四周。但也有与之前不一样的地方：内边距和边框会影响行框的高度，因为它们是行内置换元素行内框的一部分（这一点与非置换元素不同）。图 7-52 中的结果由下述样式得到：

```css
img {
  height: 50px;
  width: 50px;
}
img.one {
  margin: 0;
  padding: 0;
  border: 3px dotted;
}
img.two {
  margin: 10px;
  padding: 10px;
  border: 3px solid;
}
```

注意，第一行的行框高度足够容纳图像，而第二行的行框高度足够容纳图像及其内边距和边框。

<!-- <Figures figure="7-52">Adding padding, borders, and margins to an inline replaced element increases its inline box</Figures> -->

外边距也在行框中，但它自身也有问题要面对。正外边距没什么可讲的，就是增加置换元素行内框的高度。与之相反，负外边距减少置换元素行内框的高度。如图 7-53 所示，负的上外边距把图像上面那行向下拉了一点：

```css
img.two {
  margin-top: -10px;
}
```

显然，块级元素上的负外边距也是这种效果。这里，负外边距导致置换元素行内框的高度比常规情况下矮，只有通过负外边距才能让行内置换元素叠加到其他行上，正是因为这样，行内置换元素生成的行内框通常才假定为行内块。

<!-- <Figures figure="7-53">The effect of negative margins on inline replaced elements</Figures> -->

**置换元素与基线**

通过前面的示例你可能注意到了，行内置换元素默认与基线对齐。如果为置换元素设定下内边距、外边距或边框，那么内容区将上移（假设 box-sizing:content-box).置换元素自身没有基线，退而求其次，把置换元素的行内框底边与基线对齐。因此，与基线对齐的其实是外边距的边界，如图 7-54 所示。

<!-- <Figures figure="7-54">Inline replaced elements sit on the baseline</Figures> -->

这种对齐方式有个意想不到（而且不受待见）的后果：只有图像的单元格，其高度要够容纳图像所在的行框。即使单元格中没有文本，甚至没有空白，单元格中的图像还是会被调整尺寸。因此，以往常用的图像分割和空白填充图设计在现代的浏览器中显示效果将惨不忍睹（我知道你已经告别那个时代，但是借此说明这一行为还是不错的）。下面是最简单的情况：

```css
td {
  font-size: 12px;
}
```

```html
<td><img src="spacer.gif" height="1" width="10" /></td>
```

根据 CSS 行内格式化模型，这个单元格的高度为 12 像素，其中的图像与单元格的基线对齐。因此，图像下部可能有 3 像素空白，图像上部可能有 8 像素空白。不过，具体的空白量取决于所用的字体族和基线的位置。

这种行为并不局限于单元格中的图像，只要行内置换元素是块级元素或单元格元素的唯一后代，就会发生。例如，div 元素中的图像也与基线对齐。

这种情况最常用的解决方法是把单元格中的图像设为块级元素，不让它生成行内框。例如：

```css
td {
  font-size: 12px;
}
img.block {
  display: block;
}
```

```html
<td><img src="spacer.gif" height="1" width="10" class="block" /></td>
```

另一种方法是把图像所在的单元格的 font-size 和 line-height 都设为 1px,让行框的高度等于单元格中 1 像素高的图像。

写作本书时，很多浏览器都能忽略此种情况下的 CSS 行内格式化模型。详情参见[Images, Tables, and Mysterious Gaps 一文](https://developer.mozilla.org/zh-CN/docs/Archive/Misc_top_level/Images,_Tables,_and_Mysterious_Gaps).

与基线对齐的行内置换元素还有一个有趣的效果：如果把下外边距设为负值，元素将下移，因为此时行内框的底边比内容区的底边高。因此，下述规则将得到如图 7-55 所示的结果：

```css
p img {
  margin-bottom: -10px;
}
```

<!-- <Figures figure="7-55">Pulling inline replaced elements down with a negative bottom margin</Figures> -->

从图 7.55 中可以看出，这样很容易导致置换元素与下一行重叠。

**行内格式化模型的历史溯源**

CSS 行内格式化模型有点过于复杂，让人提摸不透，有时甚至与创作人员的预期相违，之所以变成这个样子，是因为在制定 CSS 规范时要考虑向后兼容性，兼顾那些在 CSS 之前就已存在的 Web 浏览器，而且还要为将来的发展留有余地。这门样式语言接余着过去与现在。此外还有一个原因：为了避免不良后果而做的合理决策。可能会导致其他不良后果。

例如、有图像和纵向对齐的文本行会“散开”，完其原因，这要归结于 Mosaic 1.0 的做法：留出足够的空间容纳图像。这种做法很好，因为可以避免图像与其他行中的文本重量。所以，为 CSS 制定文本和行内元素的样式化方法时，规范起草人员满尽全力想创建一个（默认情况下）不会导致行内图像与其他文本行重金的模型。然而，这样的模型也存在一些问题，例如上标元素（sup)会导致行之间的距离变大。

这种效果使一些创作人员很恼火，他们希望基线之间的距离是固定不变的。不过，这又会导致一系列问题。如果通过 line-height 让基线之间的距离固定不变，行内置换元素和纵向位置有变动的元素就会与其他行中的文本重叠，这也会让创作人不消意。幸运的是，CSS 总是为你想要的效果提供了某种实现方式，而且 CSS 还在发展，未来潜力无限。

这样的影响惹恼了一些作者，他们希望基线之间有一个精确的距离，而且不能再远了，但是考虑另一种选择。如果“行高”要求基线之间的距离必须精确到指定的距离，那么我们很容易就会得到内联替换和垂直移动的元素，这些元素会覆盖文本的其他行，这也会惹恼作者。幸运的是，CSS 提供了足够的能力来以这样或那样的方式创建您想要的效果，而且 CSS 的未来具有更大的潜力。

### 7.3.6 行内块级元素

inline-block 这个值从字面上看是两个词的结合，其意义也是如此，是块级元素和行元素的混合产物。这种显示方式在 CSS2.1 中引入。

行内块级元素与其他元素和内容的关系按照行内框处理。也就是说，它在一行中的布局方式跟图像一样。实际上，行内块级元素是当做置换元素进行格式化的。这意味着，内块级元素的底边默认是与文本行的基线对齐的，而且内部不会断行。

行内块级元素中的内容视作块级元素进行格式化，width 和 height 属性可以应用到行块级元素上（box-sizing 属性也可以）,因为这些属性都可以应用到块级元素或行内置换元素上，而且如果行内块级元素比周围的内容高，行的高度也会随之增加。

下面通过实例说明：

```html
<div id="one">
  This text is the content of a block-level level element. Within this
  block-level element is another block-level element.
  <p>Look, it's a block-level paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
<div id="two">
  This text is the content of a block-level level element. Within this
  block-level element is an inline element.
  <p>Look, it's an inline paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
<div id="three">
  This text is the content of a block-level level element. Within this
  block-level element is an inline-block element.
  <p>Look, it's an inline-block paragraph.</p>
  Here's the rest of the DIV, which is still block-level.
</div>
```

我们把下述规则应用到这段标记上：

```css
div {
  margin: 1em 0;
  border: 1px solid;
}
p {
  border: 1px dotted;
}
div#one p {
  display: block;
  width: 6em;
  text-align: center;
}
div#two p {
  display: inline;
  width: 6em;
  text-align: center;
}
div#three p {
  display: inline-block;
  width: 6em;
  text-align: center;
}
```

得到的结果如图 7-56 所示。

<!-- <Figures figure="7-56">The behavior of an inline-block element</Figures> -->

注意，第二个 div 元素中的行内段落按照常规的行内内容进行格式化，因此 width 和 text-align 将被忽略（因为这两个属性不能应用到行内元素上）。而在第三个 div 元素中，行内块级段落将应用那两个属性，因为这个段落是按照行内块级元素进行格式化的。这个段落有外边距，从而导致文本行变高，这是因为它相当于置换元素。

如果没有为行内块级元素设定 width,或者显式声明为 auto,那么元素框将根据内容自行调整宽度，即元素框的宽度恰好能容纳其中的内容，不宽不窄。行内框也是如此，不过可以断成多行，而行内块级元素则不断行。因此，如果把下述规则应用到上述标记上：

```css
div#three p {
  display: inline-block;
  height: 4em;
}
```

那么得到的元素框宽度将恰好容纳其中的内容，而且高度更大，如图 7-57 所示。

<!-- <Figures figure="7-57">Autosizing of an inline-block element</Figures> -->

行内块级元素有很多用途，例如在工具栏中放置 5 个宽度相等的超链接。如果想让每个链接占父元素宽度的 20%,而且都放在一行内，可以声明下述规则：

```css
nav a {
  display: inline-block;
  width: 20%;
}
```

弹性盒布局也能实现这种效果，而且多数情况下可能更合适。

### 7.3.7 流动显示方式

Flow 和 flow-root 需要单独说明。声明为 `display: flow` 的元素常规情况下使用块级布局，如果再加上 inline,则生成行内框。

对下述规则来说，前两个得到的是块级框，而第三个得到的是行内框。

```css
#first {
  display: flow;
}
#second {
  display: block flow;
}
#third {
  display: inline flow;
}
```

出现这种形式的原因是，CSS 正在向一种新布局系统发展，在这个系统中有两种显示类型：外部显示类型和内部显示类型。block 和 inline 等关键字表示外部显示类型，指明显示框与周围元素的关系。flow 关键字表示内部显示类型，指明元素内部的布局情况。

利用这种形式可以声明 display:inline table 这样的规则，指明元素内部按照表格布局，而处理与周围内容的关系时则作为行内元素（以前的 inline-table 值具有同等效果）。

display:flow-root 有所不同，它始终生成块级框，而且内部会生成新的块级格式化上下文。这个值可以应用到文档的根元素上，例如 html,其作用是指明“这是格式化的根基所在”，

你可能熟悉的那些 display 属性的旧值依然可用。表 7-1 列出了旧值与新值的对应关系。

表 7-1:display 属性的新旧值对照（续）

截至 2017 年底，Firefox 和 Chrome 支持“flow”和“flow-root”，但其他浏览器不支持。

截至 2017 年年末，只有 Firefox 和 Chrome 支持 flow 和 flow-root,其他浏览器都不支持。

### 7.3.8 Contents 显示方式

display 还新增了一个稍带魔法的值，contents。把`display:contents`应用到元素上之后，那个元素不再参与页面的格式化，相当于把它的子元素提升到当前的层级。以下述简单的 CSS 和 HTML 为例：

```css
ul {
  border: 1px solid red;
}
li {
  border: 1px solid silver;
}
```

```html
<ul>
  <li>The first list item.</li>
  <li>List Item II: The Listening.</li>
  <li>List item the third.</li>
</ul>
```

得到的无序列表将有一个红色边框，而且三个列表元素都有银色边框。

如果把 `display: contents` 应用到 u1 元素上，用户代理会按照文档中没有`<ul>`和`</ul>`那两行进行渲染。正常情况和使用 contents 显示方式得到的结果对比如图 7-58 所示。

<!-- <Figures figure="7-58">A regular unordered list, and one with display: contents</Figures> -->

现在，列表元素还是列表元素，而且表现也像列表元素，但是 u1 没有了，就像从未出现过一样，注意，不仅边框不见了，通常出现在列表内容四周的上下外边距也没了，正因为如此，图 7.58 中的第二个列表才量得比第一个列表的位置高。

> 戴至 2017 年年末，只有 Firefox 支持 `display: contents`。Chrome/Blink 系列浏览器目前正在实现。

### 7.3.9 display 的其它值

display 还有很多值，本章不再讨论。与表格相关的各值在后面讲解表格布局的章节讨论，列表项目在讨论计数器和生成的内容时还会谈及。

与旁注（ruby）相关的值本书完全不涉及，因为讲起来一本书也不够，而且截至 2017 年年末支持有限，还有从未流行开的 run-in,本书也不做讨论，这个值有可能会从 css 规范中删除，或者重新定义。

### 7.3.10 计算值

如果元素是浮动或定位的，其 display 值可能会变。应用到根元素上也可能会变。其实，display,position 和 float 的值之间关系错综复杂。

如果元素是绝对定位的，float 的值为 none,对浮动或绝对定位的元素来说，display 的计算值由声明的值确定，详见表 7.2.

对根元素而言，不管声明为 inline-table,还是 table,得到的计算值均为 table;而声明为 none 时，得到的就是 none,其他值得到的计算值均为 block。

## 7.4 小结

CSS 格式化模型的某些方面初看起来不太直观，不过用得多了也就会慢慢发现确实有一定的道理。很多情况下，看起来没有道理甚至荒谬的规则都是事出有因的，为的是防止文档显示得乱七八精，不符合我们的预期。块级元素相对容易理解一些，不用费什么力气就能控制它们的布局。而行内元素有时却让人捉摸不透，因为要考虑的因素太多，不是区分置换元素和非置换元素就能解决的。

# 第 8 章 内边距、边框、轮廓和外边距

前一章讨论了元素显示方面的基础知识，本将将介绍用于改变元素具体外观的CSS属性和值，包括元素四周的内边距、边框和外边距，以及可能出现的轮廓。

## 8.1 基本元素框

您可能已经注意到，所有文档元素都会生成一个名为 element box 的矩形框，它描述了一个元素在文档布局中所占的空间量。因此，每个盒子都会影响其他元素盒子的位置和大小。例如，如果文档中的第一个元素框是一英寸高，那么下一个框将在文档顶部以下至少一英寸处开始。如果将第一个元素框更改为 2 英寸高，那么下面的每个元素框将向下移动 1 英寸，而第二个元素框将从文档顶部以下至少 2 英寸处开始。

默认情况下，可视化呈现的文档是由一些矩形框组成的，这些矩形框分布在不同的地方，这样它们就不会重叠。此外，在某些约束条件下，这些框占用尽可能少的空间，同时仍然保持分离，以便明确哪些内容属于哪些元素。

如果手动定位方框，它们可能会重叠;如果在正常流元素上使用负边距，则可能出现视觉重叠。

为了理解如何处理边距、填充和边框，您必须理解 box 模型，如图 8-1 所示。

<!-- <Figures figure="8-1">The CSS box model</Figures> -->

<Tips tips="blue">The diagram in Figure 8-1 intentionally omits outlines, for reasons that will hopefully be clear once we discuss outlines.</Tips>

### Width and Height

显式定义元素的宽度相当常见，而在历史上显式定义元素的高度则少见得多。默认情况下，元素的宽度定义为从左内边缘到右内边缘的距离，而高度定义为从内顶部到内底部的距离。毫不奇怪，影响这些距离的属性被称为“高度”和“宽度”。

关于这两个属性有一点需要注意:它们不应用于内联的不可替换元素。例如，如果您试图为正常流中的超链接声明高度和宽度并生成内联框，符合 css 的浏览器必须忽略这些声明。假设以下规则适用:

```css
a:link {
  color: red;
  background: silver;
  height: 15px;
  width: 60px;
}
```

你会在银色背景上得到一个红色的未访问链接，它的高度和宽度是由链接的内容决定的。他们将“不”有 15 像素高 60 像素宽的内容区域。另一方面，如果您添加了一个“显示”值，例如“内联块”或“块”，那么“高度”和“宽度”将设置链接内容区域的高度和宽度。

<!-- <Cards cards="width" /> -->

<!-- <Cards cards="height" /> -->

<Tips tips="blue">As of late 2017, there were a few new values being considered for <code>height</code> and <code>width</code>. These are <code>stretch</code>, <code>min-content</code>, <code>max-content</code>, and <code>fit-content</code> (in two forms). Support for these values was limited, and it’s not clear whether these values will be applied to <code>height</code> and <code>width</code> any time soon.</Tips>

在本章的过程中，我们通常通过假设元素的高度总是自动计算来简化讨论。如果一个元素有 8 行，每一行都是 1/8 英寸高，那么元素的高度就是 1 英寸。如果是 10 行，那么高度是 1.25 英寸。在这两种情况下，高度是由元素的内容决定的，而不是由作者决定的。正常流中的元素很少有固定的高度。

<Tips tips="blue">It’s possible to change the meaning of <code>height</code> and <code>width</code> using the property <code>box-sizing</code>. This is not covered in this chapter, but in short, you can use either the content box or the border box as the area of measure. For the purposes of this chapter, we’ll assume the default situation holds: that <code>height</code> and <code>width</code> refer to the height and width of the content area (<code>box-sizing: content-box</code>).</Tips>

## 8.2 内边距

Just beyond the content area of an element, we find its `padding`, nestled between the content and any borders. The simplest way to set padding is by using the property `padding`.

<!-- <Cards cards="padding" /> -->

As you can see, this property accepts any length value, or a percentage value. So if you want all h2 elements to have 1 em of padding on all sides, it’s this easy (see Figure 8-2):

```css
h2 {
  padding: 2em;
  background-color: silver;
}
```

<!-- <Figures figure="8-2">Adding padding to elements</Figures> -->

如图 8-2 所示，默认情况下，元素的背景扩展到填充中。如果背景是透明的，这将在元素的内容周围创建一些额外的透明空间，但是任何可见的背景都将扩展到填充区域(以及其他区域，我们将在后面的小节中看到)。

<Tips tips="blue">Visible backgrounds can be prevented from extending into the padding by using the property <code>background-clip</code>.</Tips>

默认情况下，元素没有填充。例如，传统上，段落之间的分隔仅靠边距执行（我们将在后面介绍）。在没有填充的情况下，元素的边框也会非常接近元素本身的内容。因此，在元素上加上边框时，通常最好还添加一些填充，如图 8-3 所示。

<!-- <Figures figure="8-3">The effect of padding on bordered block-level elements</Figures> -->

Any length value is permitted, from ems to inches. The simplest way to set padding is with a single length value, which is applied equally to all four padding sides. At times, however, you might desire a different amount of padding on each side of an element. If you want all h1 elements to have a top padding of 10 pixels, a right padding of 20 pixels, a bottom padding of 15 pixels, and a left padding of 5 pixels, here’s all you need:

```css
h1 {
  padding: 10px 20px 15px 5px;
}
```

The order of the values is important, and follows this pattern:

```css
padding: top right bottom left;
```

A good way to remember this pattern is to keep in mind that the four values go clock‐wise around the element, starting from the top. The padding values are always applied in this order, so to get the effect you want, you have to arrange the values correctly.

An easy way to remember the order in which sides must be declared, other than thinking of it as being clockwise from the top, is to keep in mind that getting the sides in the correct order helps you avoid “TRouBLe”—that is, TRBL, for “Top Right Bottom Left.”

It’s also possible to mix up the types of length value you use. You aren’t restricted to using a single length type in a given rule, but can use whatever makes sense for a given side of the element, as shown here:

```css
h2 {
  padding: 14px 5em 0.1in 3ex;
} /* value variety! */
```

Figure 8-4 shows you, with a little extra annotation, the results of this declaration.

<!-- <Figures figure="8-4">Mixed-value padding</Figures> -->

### 8.2.1 复值

Sometimes, the values you enter can get a little repetitive:

```css
p {
  padding: 0.25em 1em 0.25em 1em;
} /* TRBL - Top Right Bottom Left */
```

You don’t have to keep typing in pairs of numbers like this, though. Instead of the preceding rule, try this:

```css
p {
  padding: 0.25em 1em;
}
```

These two values are enough to take the place of four. But how? CSS defines a few rules to accommodate fewer than four values for padding (and many other shorthand properties). These are:

- If the value for left is missing, use the value provided for right.
- If the value for bottom is missing, use the value provided for top.
- If the value for right is missing, use the value provided for top.

If you prefer a more visual approach, take a look at the diagram shown in Figure 8-5.

<!-- <Figures figure="8-5">Value-replication pattern</Figures> -->

In other words, if three values are given for padding, the fourth (left) is copied from the second (right). If two values are given, the fourth is copied from the second, and the third (bottom) from the first (top). Finally, if only one value is given, all the other sides copy that value.

This mechanism allows authors to supply only as many values as necessary, as shown here:

```css
h1 {
  padding: 0.25em 0 0.5em;
} /* same as '0.25em 0 0.5em 0' */
h2 {
  padding: 0.15em 0.2em;
} /* same as '0.15em 0.2em 0.15em 0.2em' */
p {
  padding: 0.5em 10px;
} /* same as '0.5em 10px 0.5em 10px' */
p.close {
  padding: 0.1em;
} /* same as '0.1em 0.1em 0.1em 0.1em' */
```

The method presents a small drawback, which you’re bound to eventually encounter. Suppose you want to set the top and left padding for h1 elements to be 10 pixels, and the bottom and right padding to be 20 pixels. In that case, you have to write the following:

```css
h1 {
  padding: 10px 20px 20px 10px;
} /* can't be any shorter */
```

You get what you want, but it takes a while to get it all in. Unfortunately, there is no way to cut down on the number of values needed in such a circumstance. Let’s take another example, one where you want all of the padding to be zero—except for the left padding, which should be 3 em:

```css
h2 {
  padding: 0 0 0 3em;
}
```

Using padding to separate the content areas of elements can be trickier than using the traditional margins, although it’s not without its rewards. For example, to keep paragraphs the traditional “one blank line” apart with padding, you’d have to write:

```css
p {
  margin: 0;
  padding: 0.5em 0;
}
```

The half-em top and bottom padding of each paragraph butt up against each other and total an em of separation. Why would you bother to do this? Because then you could insert separation borders between the paragraphs, should you so choose, and side borders will touch to form the appearance of a solid line. Both these effects are illustrated in Figure 8-6:

```css
p {
  margin: 0;
  padding: 0.5em 0;
  border-bottom: 1px solid gray;
  border-left: 3px double black;
}
```

<!-- <Figures figure="8-6">Using padding instead of margins</Figures> -->

### 8.2.2 单边内边距

Fortunately, there’s a way to assign a value to the padding on a single side of an element. Four ways, actually. Let’s say you only want to set the left padding of h2 elements to be 3em. Rather than writing out padding: 0 0 0 3em, you can take this approach:

```css
h2 {
  padding-left: 3em;
}
```

padding-left is one of four properties devoted to setting the padding on each of the four sides of an element box. Their names will come as little surprise.

<!-- <Cards cards="padding-top_padding-right_padding-bottom_padding-left" /> -->

These properties operate in a manner consistent with their names. For example, the following two rules will yield the same amount of padding:

```css
h1 {
  padding: 0 0 0 0.25in;
}
h2 {
  padding-left: 0.25in;
}
```

Similarly, these rules are will create equal padding:

```css
h1 {
  padding: 0.25in 0 0;
} /* left padding is copied from right padding */
h2 {
  padding-top: 0.25in;
}
```

For that matter, so will these rules:

```css
h1 {
  padding: 0 0.25in;
}
h2 {
  padding-right: 0.25in;
  padding-left: 0.25in;
}
```

It’s possible to use more than one of these single-side properties in a single rule; for example:

```css
h2 {
  padding-left: 3em;
  padding-bottom: 2em;
  padding-right: 0;
  padding-top: 0;
  background: silver;
}
```

As you can see in Figure 8-7, the padding is set as we wanted. In this case, it might have been easier to use padding after all, like so:

```css
h2 {
  padding: 0 0 2em 3em;
}
```

<!-- <Figures figure="8-7">More than one single-side padding</Figures> -->

In general, once you’re trying to set padding for more than one side, it’s easier to use the shorthand padding. From the standpoint of your document’s display, however, it doesn’t really matter which approach you use, so choose whichever is easiest for you.

### 8.2.3 内边距的百分数值

It’s possible to set percentage values for the padding of an element. Percentages are computed in relation to the width of the parent element’s content area, so they change if the parent element’s width changes in some way. For example, assume the following, which is illustrated in Figure 8-8:

```css
p {
  padding: 10%;
  background-color: silver;
}
```

```html
<div style="width: 600px;">
  <p>
    This paragraph is contained within a DIV that has a width of 600 pixels, so
    its padding will be 10% of the width of the paragraph's parent element.
    Given the declared width of 600 pixels, the padding will be 60 pixels on all
    sides.
  </p>
</div>
<div style="width: 300px;">
  <p>
    This paragraph is contained within a DIV with a width of 300 pixels, so its
    padding will still be 10% of the width of the paragraph's parent. There
    will, therefore, be half as much padding on this paragraph as that on the
    first paragraph.
  </p>
</div>
```

<!-- <Figures figure="8-8">Padding, percentages, and the widths of parent elements</Figures> -->

You may have noticed something odd about the paragraphs in Figure 8-8. Not only did their side padding change according to the width of their parent elements, but so did their top and bottom padding. That’s the desired behavior in CSS. Refer back to the property definition, and you’ll see that percentage values are defined to be relative to the width of the parent element. This applies to the top and bottom padding as well as to the left and right. Thus, given the following styles and markup, the top padding of the paragraph will be 50 px:

```css
div p {
  padding-top: 10%;
}
```

```html
<div style="width: 500px;">
  <p>
    This is a paragraph, and its top margin is 10% the width of its parent
    element.
  </p>
</div>
```

If all this seems strange, consider that most elements in the normal flow are (as we are assuming) as tall as necessary to contain their descendant elements, including padding. If an element’s top and bottom padding were a percentage of the parent’s height, an infinite loop could result where the parent’s height was increased to accommodate the top and bottom padding, which would then have to increase to match the new height, and so on. Rather than ignore percentages for top and bottom padding, the specification authors decided to make it relate to the width of the parent’s content area, which does not change based on the width of its descendants.

By contrast, consider the case of elements without a declared width. In such cases, the overall width of the element box (including padding) is dependent on the width of the parent element. This leads to the possibility of fluid pages, where the padding on elements enlarges or reduces to match the actual size of the parent element. If you style a document so that its elements use percentage padding, then as the user changes the width of a browser window, the padding will expand or shrink to fit. The design choice is up to you.

<Tips tips="blue">The treatment of percentage values for top and bottom padding is different for most positioned elements, flex items, and grid items, where they are calculated with respect to the height of their formatting context.</Tips>

It’s also possible to mix percentages with length values. Thus, to set h2 elements to have top and bottom padding of one-half em, and side padding of 10% the width of their parent elements, you can declare the following, illustrated in Figure 8-9:

```css
h2 {
  padding: 0.5em 10%;
}
```

<!-- <Figures figure="8-9">Mixed padding</Figures> -->

Here, although the top and bottom padding will stay constant in any situation, the side padding will change based on the width of the parent element.

### 8.2.4 行内元素的内边距

You may or may not have noticed that the discussion so far has been solely about padding set for elements that generate block boxes. When padding is applied to inline nonreplaced elements, things can get a little different.

Let’s say you want to set top and bottom padding on strongly emphasized text:

```css
strong {
  padding-top: 25px;
  padding-bottom: 50px;
}
```

This is allowed in the specification, but since you’re applying the padding to an inline nonreplaced element, it will have absolutely no effect on the line height. Since padding is transparent when there’s no visible background, the preceding declaration will have no visual effect whatsoever. This happens because padding on inline nonreplaced elements doesn’t change the line height of an element.

Be careful: an inline nonreplaced element with a background color and padding can have a background that extends above and below the element, like this:

```css
strong {
  padding-top: 0.5em;
  background-color: silver;
}
```

Figure 8-10 gives you an idea of what this might look like.

<!-- <Figures figure="8-10">Top padding on an inline nonreplaced element</Figures> -->

The line height isn’t changed, but since the background color does extend into the padding, each line’s background ends up overlapping the lines that come before it. That’s the expected result.

The preceding behaviors are true only for the top and bottom sides of inline nonreplaced elements; the left and right sides are a different story. We’ll start by considering the case of a small, inline nonreplaced element within a single line. Here, if you set values for the left or right padding, they will be visible, as Figure 8-11 makes clear (so to speak):

```css
strong {
  padding-left: 25px;
  background: silver;
}
```

<!-- <Figures figure="8-11">An inline nonreplaced element with left padding</Figures> -->

Note the extra space between the end of the word just before the inline nonreplaced element and the edge of the inline element’s background. You can add that extra space to both ends of the inline if you want:

```css
strong {
  padding-left: 25px;
  padding-right: 25px;
  background: silver;
}
```

As expected, Figure 8-12 shows a little extra space on the right and left sides of the inline element, and no extra space above or below it.

<!-- <Figures figure="8-12">An inline nonreplaced element with 25-pixel side padding</Figures> -->

Now, when an inline nonreplaced element stretches across multiple lines, the situation changes a bit. Figure 8-13 shows what happens when an inline nonreplaced element with a padding is displayed across multiple lines:

```css
strong {
  padding: 0 25px;
  background: silver;
}
```

The left padding is applied to the beginning of the element and the right padding to the end of it. By default, padding is not applied to the right and left side of each line. Also, you can see that, if not for the padding, the line may have broken after “background.” instead of where it did. padding only affects line breaking by changing the point at which the element’s content begins within a line.

<!-- <Figures figure="8-13">An inline nonreplaced element with 25-pixel side padding displayed across two lines of text</Figures> -->

<Tips tips="blue">The way padding is (or isn’t) applied to the ends of each line box can be altered with the property box-decoration-break. See Chapter 7 for more details.</Tips>

### 8.2.5 置换元素的内边距

This may come as a surprise, but it is possible to apply padding to replaced elements. The most surprising case is that you can apply padding to an image, like this:

```css
img {
  background: silver;
  padding: 1em;
}
```

Regardless of whether the replaced element is block-level or inline, the padding will surround its content, and the background color will fill into that padding, as shown in Figure 8-14. You can also see in Figure 8-14 that padding will push a replaced element’s border (dashed, in this case) away from its content.

<!-- <Figures figure="8-14">Padding replaced elements</Figures> -->

Now, remember all that stuff about how padding on inline nonreplaced elements doesn’t affect the height of the lines of text? You can throw it all out for replaced elements, because they have a different set of rules. As you can see in Figure 8-15, the padding of an inline replaced element very much affects the height of the line.

<!-- <Figures figure="8-15">Padding replaced elements</Figures> -->

The same goes for borders and margins, as we’ll soon see.

<Tips tips="orange">As of late 2017, there was still uncertainty over what to do about styling form elements such as <code>input</code>, which are replaced elements. It is not entirely clear where the padding of a checkbox resides, for example. Therefore, as of this writing, some browsers ignore padding (and other forms of styling) for form elements, while others apply the styles as best they can.</Tips>

## 8.3 边框

Beyond the padding of an element are its borders. The border of an element is just one or more lines that surround the content and padding of an element. By default, the background of the element will stop at the outer border edge, since the background does not extend into the margins, and the border is just inside the margin.

Every border has three aspects: its width, or thickness; its style, or appearance; and its color. The default value for the width of a border is medium, which is not an explicitly defined distance, but usually works out to be two pixels. Despite this, the reason you don’t usually see borders is that the default style is none, which prevents them from existing at all. (This lack of existence can also reset the border-width value, but we’ll get to that in a little while.)

Finally, the default border color is the foreground color of the element itself. If no color has been declared for the border, then it will be the same color as the text of the element. If, on the other hand, an element has no text—let’s say it has a table that contains only images—the border color for that table will be the text color of its parent element (thanks to the fact that color is inherited). That element is likely to be body, div, or another table. Thus, if a table has a border, and the body is its parent, given this rule:

```css
body {
  color: purple;
}
```

then, by default, the border around the table will be purple (assuming the user agent doesn’t set a color for tables).

The CSS specification defines the background area of an element to extend to the outside edge of the border, at least by default. This is important because some borders are intermittent—for example, dotted and dashed borders—so the element’s background should appear in the spaces between the visible portions of the border.

<Tips tips="blue">Visible backgrounds can be prevented from extending into the border area by using the property background-clip. See Chapter 9 for details.</Tips>

### 8.3.1 边框的式样

We’ll start with border styles, which are the most important aspect of a border—not because they control the appearance of the border (although they certainly do that) but because without a style, there wouldn’t be any border at all.

<!-- <Cards cards="border-style" /> -->

CSS defines 10 distinct non-inherit styles for the property border-style, including the default value of none. The styles are demonstrated in Figure 8-16.

The style value hidden is equivalent to none, except when applied to tables, where it has a slightly different effect on border-conflict resolution.

<!-- <Figures figure="8-16">Border styles</Figures> -->

The most unpredictable border style is double. It’s defined such that the width of the two lines it creates, plus the width of the space between them, is equal to the value of border-width (discussed in the next section). However, the CSS specification doesn’t say whether one of the lines should be thicker than the other, or if they should always be the same width, or if the space should be thicker or thinner than the lines. All of these things are left up to the user agent to decide, and the author has no reliable way to influence the final result.

All the borders shown in Figure 8-16 are based on a color value of gray, which makes all of the visual effects easier to see. The look of a border style is always based in some way on the color of the border, although the exact method may vary between user agents. The way browsers treat colors in the border styles inset, outset, groove, and ridge can and does vary. For example, Figure 8-17 illustrates two different ways of rendering an inset border.

<!-- <Figures figure="8-17">Two valid ways of rendering inset</Figures> -->

Note how one browser takes the gray value for the bottom and right sides, and a darker gray for the top and left; the other makes the bottom and right lighter than gray and the top and left darker, but not as dark as the first browser.

Now let’s define a border style for images that are inside any unvisited hyperlink. We might make them outset, so they have a “raised button” look, as depicted in Figure 8-18:

```css
a:link img {
  border-style: outset;
}
```

<!-- <Figures figure="8-18">Applying an outset border to a hyperlinked image</Figures> -->

By default, the color of the border is based on the element’s value for color, which in this circumstance is likely to be blue. This is because the image is contained with a hyperlink, and the foreground color of hyperlinks is usually blue. If you so desired, you could change that color to silver, like this:

```css
a:link img {
  border-style: outset;
  color: silver;
}
```

The border will now be based on the light grayish silver, since that’s now the foreground color of the image—even though the image doesn’t actually use it, it’s still passed on to the border. We’ll talk about another way to change border colors in the section “Border Colors”.

Remember, though, that the color-shifting in borders is up to the user agent. Let’s go back to the blue outset border and compare it in two different browsers, as shown in Figure 8-19.

Again, notice how one browser shifts the colors to the lighter and darker, while another just shifts the “shadowed” sides to be darker than blue. This is why, if a specific set of colors is desired, authors usually set the exact colors they want instead of using a border style like outset and leaving the result up to the browser. We’ll soon see just how to do that.

<!-- <Figures figure="8-19">Two outset borders</Figures> -->

#### MULTIPLE STYLES

It’s possible to define more than one style for a given border. For example:

```css
p.aside {
  border-style: solid dashed dotted solid;
}
```

The result is a paragraph with a solid top border, a dashed right border, a dotted bottom border, and a solid left border.

Again we see the top-right-bottom-left order of values, just as we saw in our discussion of setting padding with multiple values. All the same rules about value replication apply to border styles, just as they did with padding. Thus, the following two statements would have the same effect, as depicted in Figure 8-20:

```css
p.new1 {
  border-style: solid none dashed;
}
p.new2 {
  border-style: solid none dashed none;
}
```

<!-- <Figures figure="8-20">Equivalent style rules</Figures> -->

#### SINGLE-SIDE STYLES

There may be times when you want to set border styles for just one side of an element box, rather than all four. That’s where the single-side border style properties come in.

<!-- <Cards cards="border-top-style_border-right-style_border-bottom-style_border-left-style" /> -->

Single-side border style properties are fairly self-explanatory. If you want to change the style for the bottom border, for example, you use border-bottom-style.

It’s not uncommon to see border used in conjunction with a single-side property. Suppose you want to set a solid border on three sides of a heading, but not have a left border, as shown in Figure 8-21.

<!-- <Figures figure="8-21">Removing the left border</Figures> -->

There are two ways to accomplish this, each one equivalent to the other:

```css
h1 {
  border-style: solid solid solid none;
}
/* the above is the same as the below */
h1 {
  border-style: solid;
  border-left-style: none;
}
```

What’s important to remember is that if you’re going to use the second approach, you have to place the single-side property after the shorthand, as is usually the case with shorthands. This is because border-style: solid is actually a declaration of border-style: solid solid solid solid. If you put border-style-left: none before the border-style declaration, the shorthand’s value will override the single-side value of none.

### 8.3.2 边框宽度

Once you’ve assigned a border a style, the next step is to give it some width, most easily by using the property border-width or one of its cousin properties.

<!-- <Cards cards="border-width" /> -->

Each of these properties is used to set the width on a specific border side, just as with the margin properties.

<Tips tips="blue">As of late 2017, border widths still cannot be given percentage values, which is rather a shame.</Tips>

There are four ways to assign width to a border: you can give it a length value such as 4px or 0.1em, or use one of three keywords. These keywords are thin, medium (the default value), and thick. These keywords don’t necessarily correspond to any particular width, but are defined in relation to one another. According to the specification, thick is always wider than medium, which is in turn always wider than thin. Which makes sense.

However, the exact widths are not defined, so one user agent could set them to be equivalent to 5px, 3px, and 2px, while another sets them to be 3px, 2px, and 1px. No matter what width the user agent uses for each keyword, it will be the same throughout the document, regardless of where the border occurs. So if medium is the same as 2px, then a medium-width border will always be two pixels wide, whether the border surrounds an h1 or a p element. Figure 8-22 illustrates one way to handle these three keywords, as well as how they relate to each other and to the content they surround.

<!-- <Figures figure="8-22">The relation of border-width keywords to each other</Figures> -->

Let’s suppose a paragraph has a background color and a border style set:

```css
p {
  background-color: silver;
  border-style: solid;
}
```

The border’s width is, by default, medium. We can change that easily enough:

```css
p {
  background-color: silver;
  border-style: solid;
  border-width: thick;
}
```

Of course, border widths can be taken to fairly ridiculous extremes, such as setting 50-pixel borders, as depicted in Figure 8-23:

```
p {background-color: silver; padding: 0.5em;
    border-style: solid; border-width: 50px;}
```

<!-- <Figures figure="8-23">Really wide borders</Figures> -->

It’s also possible to set widths for individual sides, using two familiar methods. The first is to use any of the specific properties mentioned at the beginning of the section, such as border-bottom-width. The other way is to use value replication in border-width, which is illustrated in Figure 8-24:

```css
h1 {
  border-style: dotted;
  border-width: thin 0;
}
p {
  border-style: solid;
  border-width: 15px 2px 8px 5px;
}
```

<!-- <Figures figure="8-24">Value replication and uneven border widths</Figures> -->

#### NO BORDER AT ALL

So far, we’ve talked only about using a visible border style such as solid or outset. Let’s consider what happens when you set border-style to none:

```css
p {
  border-style: none;
  border-width: 20px;
}
```

Even though the border’s width is 20px, the style is set to none. In this case, not only does the border’s style vanish, so does its width. The border just ceases to be. Why?

If you’ll remember, the terminology used earlier in the chapter was that a border with a style of none does not exist. Those words were chosen very carefully, because they help explain what’s going on here. Since the border doesn’t exist, it can’t have any width, so the width is automatically set to 0 (zero), no matter what you try to define. After all, if a drinking glass is empty, you can’t really describe it as being half-full of nothing. You can discuss the depth of a glass’s contents only if it has actual contents. In the same way, talking about the width of a border makes sense only in the context of a border that exists.

This is important to keep in mind because it’s a common mistake to forget to declare a border style. This leads to all kinds of author frustration because, at first glance, the styles appear correct. Given the following rule, though, no h1 element will have a border of any kind, let alone one that’s 20 pixels wide:

```css
h1 {
  border-width: 20px;
}
```

Since the default value of border-style is none, failure to declare a style is exactly the same as declaring border-style: none. Therefore, if you want a border to appear, you need to declare a border style.

### 8.3.3 边框颜色

Compared to the other aspects of borders, setting the color is pretty easy. CSS uses the single property border-color, which can accept up to four color values at one time.

<!-- <Cards cards="border-color" /> -->

If there are fewer than four values, value replication takes effect as usual. So if you want h1 elements to have thin gray top and bottom borders with thick green side borders, and medium gray borders around p elements, the following styles will suffice, with the result shown in Figure 8-25:

```css
h1 {
  border-style: solid;
  border-width: thin thick;
  border-color: gray green;
}
p {
  border-style: solid;
  border-color: gray;
}
```

<!-- <Figures figure="8-25">Borders have many aspects</Figures> -->

A single color value will be applied to all four sides, as with the paragraph in the previous example. On the other hand, if you supply four color values, you can get a different color on each side. Any type of color value can be used, from named colors to hexadecimal and RGBA values:

```css
p {
  border-style: solid;
  border-width: thick;
  border-color: black rgba(25%, 25%, 25%, 0.5) #808080 silver;
}
```

As mentioned earlier, if you don’t declare a color, the default color is the foreground color of the element. Thus, the following declaration will be displayed as shown in Figure 8-26:

```css
p.shade1 {
  border-style: solid;
  border-width: thick;
  color: gray;
}
p.shade2 {
  border-style: solid;
  border-width: thick;
  color: gray;
  border-color: black;
}
```

<!-- <Figures figure="8-26">Border colors based on the element’s foreground and the value of the border-color property</Figures> -->

The result is that the first paragraph has a gray border, having taken the value gray from the foreground color of the paragraph. The second paragraph, however, has a black border because that color was explicitly assigned using border-color.

There are single-side border color properties as well. They work in much the same way as the single-side properties for style and width. One way to give headings a solid black border with a solid gray right border is as follows:

```css
h1 {
  border-style: solid;
  border-color: black;
  border-right-color: gray;
}
```

<!-- <Cards cards="border-top-color_border-right-color_border-bottom-color_border-left-color" /> -->

#### TRANSPARENT BORDERS

As you may recall, if a border has no style, then it has no width. There are, however, situations where you’ll want to create an invisible border that still has width. This is where the border color value transparent (introduced in CSS2) comes in.

Let’s say we want a set of three links to have borders that are invisible by default, but look inset when the link is hovered. We can accomplish this by making the borders transparent in the nonhovered case:

```css
a:link,
a:visited {
  border-style: inset;
  border-width: 5px;
  border-color: transparent;
}
a:hover {
  border-color: gray;
}
```

This will have the effect shown in Figure 8-27.

In a sense, transparent lets you use borders as if they were extra padding, with the additional benefit of being able to make them visible should you so choose. They act as padding because the background of the element extends into the border area by default, assuming there is a visible background.

<!-- <Figures figure="8-27">Using transparent borders</Figures> -->

### 8.3.4 简写的边框属性

Unfortunately, shorthand properties such as border-color and border-style aren’t always as helpful as you’d think. For example, you might want to apply a thick, gray, solid border to all h1 elements, but only along the bottom. If you limit yourself to the properties we’ve discussed so far, you’ll have a hard time applying such a border. Here are two examples:

```css
h1 {
  border-bottom-width: thick; /* option #1 */
  border-bottom-style: solid;
  border-bottom-color: gray;
}
h1 {
  border-width: 0 0 thick; /* option #2 */
  border-style: none none solid;
  border-color: gray;
}
```

Neither is really convenient, given all the typing involved. Fortunately, a better solution is available:

```css
h1 {
  border-bottom: thick solid rgb(50%, 40%, 75%);
}
```

This will apply the values to the bottom border alone, as shown in Figure 8-28, leaving the others to their defaults. Since the default border style is none, no borders appear on the other three sides of the element.

<!-- <Figures figure="8-28">Setting a bottom border with a shorthand property</Figures> -->

As you may have already guessed, there are a total of four such shorthand properties.

<!-- <Cards cards="border-top_border-right_border-bottom_border-left" /> -->

It’s possible to use these properties to create some complex borders, such as those shown in Figure 8-29:

```css
h1 {
  border-left: 3px solid gray;
  border-right: green 0.25em dotted;
  border-top: thick goldenrod inset;
  border-bottom: double rgb(13%, 33%, 53%) 10px;
}
```

<!-- <Figures figure="8-29">Very complex borders</Figures> -->

As you can see, the order of the actual values doesn’t really matter. The following three rules will yield exactly the same border effect:

```css
h1 {
  border-bottom: 3px solid gray;
}
h2 {
  border-bottom: solid gray 3px;
}
h3 {
  border-bottom: 3px gray solid;
}
```

You can also leave out some values and let their defaults kick in, like this:

```css
h3 {
  color: gray;
  border-bottom: 3px solid;
}
```

Since no border color is declared, the default value (the element’s foreground) is applied instead. Just remember that if you leave out a border style, the default value of none will prevent your border from existing.

By contrast, if you set only a style, you will still get a border. Let’s say you want a top border style of dashed and you’re willing to let the width default to medium and the color be the same as the text of the element itself. All you need in such a case is the following markup (shown in Figure 8-30):

```css
p.roof {
  border-top: dashed;
}
```

<!-- <Figures figure="8-30">Dashing across the top of an element</Figures> -->

Also note that since each of these border-side properties applies only to a specific side, there isn’t any possibility of value replication—it wouldn’t make any sense. There can be only one of each type of value: that is, only one width value, only one color value, and only one border style. So don’t try to declare more than one value type:

```css
h3 {
  border-top: thin thick solid purple;
} /* two width values--WRONG */
```

In such a case, the entire statement will be invalid and a user agent would ignore it altogether.

### 8.3.5 整个边框

Now, we come to the shortest shorthand border property of all: border.

<!-- <Cards cards="border" /> -->

This property has the advantage of being very compact, although that brevity introduces a few limitations. Before we worry about that, let’s see how border works. If you want all h1 elements to have a thick silver border, the following declaration would be displayed as shown in Figure 8-31:

```css
h1 {
  border: thick silver solid;
}
```

The values are applied to all four sides. This is certainly preferable to the next-best alternative, which would be:

```css
h1 {
  border-top: thick silver solid;
  border-bottom: thick silver solid;
  border-right: thick silver solid;
  border-left: thick silver solid;
} /* same result as previous example */
```

<!-- <Figures figure="8-31">A really short border declaration</Figures> -->

The drawback with border is that you can define only global styles, widths, and colors. In other words, the values you supply for border will apply to all four sides equally. If you want the borders to be different for a single element, you’ll need to use some of the other border properties. Then again, it’s possible to turn the cascade to your advantage:

```css
h1 {
  border: thick goldenrod solid;
  border-left-width: 20px;
}
```

The second rule overrides the width value for the left border assigned by the first rule, thus replacing thick with 20px, as you can see in Figure 8-32.

<!-- <Figures figure="8-32">Using the cascade to one’s advantage</Figures> -->

You still need to take the usual precautions with shorthand properties: if you omit a value, the default will be filled in automatically. This can have unintended effects. Consider the following:

```css
h4 {
  border-style: dashed solid double;
}
h4 {
  border: medium green;
}
```

Here, we’ve failed to assign a border-style in the second rule, which means that the default value of none will be used, and no h4 elements will have any border at all.

### 8.3.6 行内元素的边框

Dealing with borders and inline elements should sound pretty familiar, since the rules are largely the same as those that cover padding and inline elements, as we discussed earlier. Still, I’ll briefly touch on the topic again.

First, no matter how thick you make your borders on inline elements, the line height of the element won’t change. Let’s set top and bottom borders on boldfaced text:

```css
strong {
  border-top: 10px solid hsl(216, 50%, 50%);
  border-bottom: 5px solid #aea010;
}
```

Once more, this syntax is allowed in the specification, but it will have absolutely no effect on the line height. However, since borders are visible, they’ll be drawn—as you can see for yourself in Figure 8-33.

<!-- <Figures figure="8-33">Borders on inline nonreplaced elements</Figures> -->

The borders have to go somewhere. That’s where they went.

Again, all of this is true only for the top and bottom sides of inline elements; the left and right sides are a different story. If you apply a left or right border, not only will they be visible, but they’ll displace the text around them, as you can see in Figure 8-34:

```css
strong {
  border-left: 25px double hsl(216, 50%, 50%);
  background: silver;
}
```

With borders, just as with padding, the browser’s calculations for line breaking are not directly affected by any box properties set for inline nonreplaced elements. The only effect is that the space taken up by the borders may shift portions of the line over a bit, which may in turn change which word is at the end of the line.

<!-- <Figures figure="8-34">Inline nonreplaced elements with left borders</Figures> -->

<Tips tips="blue">The way borders are (or aren’t) drawn at the ends of each line box can be altered with the property <code>box-decoration-break</code>. See Chapter 7 for more details.</Tips>

With replaced elements such as images, on the other hand, the effects are very much like those we saw with padding: a border will affect the height of the lines of text, in addition to shifting text around to the sides. Thus, assuming the following styles, we get a result like that seen in Figure 8-35.

```css
img {
  border: 1em solid rgb(216, 108, 54);
}
```

<!-- <Figures figure="8-35">Borders on inline replaced elements</Figures> -->

### 8.3.7 圆角边框

It’s possible to soften the harsh corners of element borders by using the property border-radius to define a rounding distance (or two). In this particular case, we’re actually going to start with the shorthand property and then mention the individual properties at the end of the section.

<!-- <Cards cards="border-radius" /> -->

The radius of a border is the radius of a circle or ellipse, one quarter of which is used to define the path of the border’s rounding. We’ll start with circles, because they’re a little easier to understand.

Suppose we want to round the corner of an element so that each corner has pretty obviously rounded. Here’s one way to do that:

```css
#example {
  border-radius: 2em;
}
```

That will have the result shown in Figure 8-36, where circle diagrams have been added to two of the corners. (The same rounding is done in all four corners.)

<!-- <Figures figure="8-36">How border radii are calculated</Figures> -->

Focus on the top left corner. There, the border begins to curve 2 em below the top of the border, and 2 em to the right of the left side of the border. The curve follows along the outside of the 2-em-radius circle.

If we were to draw a box that just contained the part of the top left corner that was curved, that box would be 2em wide and 2em tall. The same thing would happen in the bottom right corner.

With single length values, we get circular corner rounding shapes. If a single percentage is used, the results are far more oval. For example, consider the following, illustrated in Figure 8-37.

```css
#example {
  border-radius: 33%;
}
```

<!-- <Figures figure="8-37">How percentage border radii are calculated</Figures> -->

Again, let’s focus on the top left corner. On the left edge, the border curve begins at the point 33% of the element box’s height down from the top. In other words, if the element box is 100 pixels tall from top border edge to bottom border edge, the curve begins 33 pixels from the top of the element box.

Similarly, on the top edge, the curve begins at the point 33% of the element box’s width from the left edge. So if the box is (say) 600 pixels wide, the curve begins 198 pixels from the left edge, because 600 \* 0.33 = 198.

The shape of the curve between those two points is identical to the top left edge of an ellipse whose horizontal radius is 198 pixels long, and whose vertical radius is 33 pixels long. (This is the same as an ellipse with a horizontal axis of 396 pixels and a vertical axis of 66 pixels.)

The same thing is done in each corner, leading to a set of corner shapes that mirror each other, rather than being identical.

Supplying a single length or percentage value for border-radius means all four corners will have the same rounding shape. As you may have spotted in the syntax definnition, similar to padding or some other shorthands like border-style, you can supply border-radius with up to four values. They go in clockwise order from top left to bottom left, like so:

```css
#example {
  border-radius: 1em /* Top Left */ 2em /* Top Right */ 3em /* Bottom Right */
    4em; /* Bottom Left */
}
```

This TL-TR-BR-BL can be remembered with the mnemonic “TiLTeR BuRBLe,” if you’re inclined to such things. The important thing is that the rounding starts in the top left, and works its way clockwise from there.

If a value is left off, then the missing values are filled in using a pattern like that used for padding and so on. If there are three values, the fourth is copied from the second. If there are two, the third is copied from the first and the fourth from the second. Just one, and the missing three are copied from the first. Thus, the following two rules are identical, and will have the result shown in Figure 8-38.

```css
#example {
  border-radius: 1em 2em 3em 2em;
}
#example {
  border-radius: 1em 2em 3em; /* BL copied from TR */
}
```

<!-- <Figures figure="8-38">A variety of rounded corners</Figures> -->

There’s an important aspect to Figure 8-38: the rounding of the content area’s background along with the rest of the background. See how the silver curves, and the period sits outside it? That’s the expected behavior in a situation where the content area’s background is different than the padding background (we’ll see how to do that in the next chapter) and the curving of a corner is large enough to affect the boundary between content and padding.

This is because while border-radius changes how the border and background(s) of an element are drawn, it does not change the shape of the element box. Consider the situation depicted in Figure 8-39.

<!-- <Figures figure="8-39">Elements with rounded corners are still boxes</Figures> -->

There, we can see an element that’s been floated to the left, and other text flowing past it. The border corners have been completely rounded off using border-radius: 50%, and some of its text is sticking out past the rounded corners. Beyond the rounded corners, we can also see the page background visible where the corners would have been, were they not rounded.

So at a glance, you might assume that the element has been reshaped from box to circle (technically ellipse), and the text just happens to stick out of it. But look at the text flowing past the float. It doesn’t flow into the area the rounded corners “left behind.” That’s because the corners of the floated element are still there. They’re just not visibly filled by border and background, thanks to border-radius.

And what happens if a radius value is so large that it would spill into other corners? For example, what happens with border-radius: 100%? Or border-radius: 9999px on an element that’s nowhere near ten thousand pixels tall or wide?

In any such case, the rounding is “clamped” to the maximum it can be for a given quadrant of the element. Making sure that buttons always look little medical lozenges can be done like so:

```css
.button {
  border-radius: 9999em;
}
```

That will just cap off the shortest ends of the element (usually the left and right sides, but no guarantees) to be smooth semicircular caps.

#### MORE COMPLEX CORNER SHAPING

Now that we’ve seen how assigning a single radius value to a corner shapes it, let’s talk about what happens when corners get two values—and, more importantly, how they get those values.

For example, suppose we want corners to be rounded by 3 character units horizontally, and 1 character unit vertically. We can’t just say border-radius: 3ch 1ch because that will round the top left and bottom right corners by 3ch, and the other two corners by 1ch each. Inserting a forward slash will get us what we’re after:

```css
#example {
  border-radius: 3ch / 1ch;
}
```

This is functionally equivalent to saying:

```css
#example {
  border-radius: 3ch 3ch 3ch 3ch / 1ch 1ch 1ch 1ch;
}
```

The way this syntax works, the horizontal radius of each corner’s rounding ellipse is given, and then after the slash, the vertical radius of each corner is given. In both cases, the values are in “TiLTeR BuRBLe” order.

Here’s a simpler example, illustrated in Figure 8-40:

```css
#example {
  border-radius: 1em / 2em;
}
```

<!-- <Figures figure="8-40">Elliptical corner rounding</Figures> -->

Each corner is rounded by 1em along the horizontal axis, and 2em along the vertical axis, in the manner we saw in detail in the previous section.

Here’s a slightly more complex version, providing two lengths to either side of the slash, as depicted in Figure 8-41:

```css
#example {
  border-radius: 1em 2em / 2em 3em;
}
```

<!-- <Figures figure="8-41">Different elliptical rounding calculations</Figures> -->

In this case, the top left and bottom right corners are curved 1em along the horizontal axis, and 2em along the vertical axis. The top right and bottom left corners, on the other hand, are curved 2em along the horizontal and 3 along the vertical.

However! Don’t think the 1em 2em to the left of the slash defines the first corner set, and the 2em 3em to the right of the slash defines the second. Remember, it’s horizontal values before the slash, and vertical after. If we’d wanted to make the top left and bottom right corners be rounded 1em horizontally and 1em vertically (a circular rounding), the values would have been written like so:

```css
#example {
  border-radius: 1em 2em / 1em 3em;
}
```

Percentages are also fair game here. If we want to round the corners of an element so that the sides are fully rounded but only extend 2 character units into the element horizontally, we’d write it like so:

```css
#example {
  border-radius: 2ch / 50%;
}
```

#### CORNER BLENDING

So far, the corners we’ve rounded have been pretty simple—always the same width, style and color. That won’t always be the case, though. What happens if a tick red solid border is rounded into a thin dashed green border?

The specification directs that the rounding cause as smooth a blend as possible when it comes to the width. In other words, when rounding from a thicker border to a thinner border, the width of the border should gradually shrink throughout the curve of the rounded corner.

When it comes to differing styles and colors, the specification is less clear about how this should be accomplished. Consider the various samples shown in Figure 8-42.

<!-- <Figures figure="8-42">Rounded corners up close</Figures> -->

The first is a simple rounded corner, with no variation in color, width, or style. The second shows rounding from one thickness to another. You can visualize this second case as a shape defined by a circular shape on the outer edge and en elliptical shape on the inner edge.

In the third case, the color and thickness stay the same, but the corner curves from a solid style on the left to a double-line style on top. The transition between styles is abrupt, and occurs at the halfway point in the curve.

The fourth example shows a transition from a thick solid to a thinner double border. Note the placement of the transition, which is not at the halfway point. It is instead determined by taking the ratio of the two borders’ thicknesses, and using that to find the transition point. Let’s assume the left border is 10px thick and the top border 5px thick. By summing the two to get 15px, the left border gets 2/3 (10/15) and the top border 1/3 (5/15). Thus, the left border’s style is used in two-thirds of the curve, and the top border‘s style in one-third the curve. The width is still smoothly changed over the length of the curve.

The fifth and sixth examples show what happens with color added to the mix. Effectively, the color stays linked to the style. This hard transition between colors is common behavior amongst browsers as of late 2017, but it may not always be so. The specification explicitly states that user agents may blend from one border color to another by using a linear gradient. Perhaps one day they will, but for now, the changeover is instantaneous.

The seventh example in Figure 8-42 shows a case we haven’t really discussed which is: “What happens if the borders are equal to or thicker than the value of border-radius?” In the case, the outside of the corner is rounded, but the inside is not, as shown. This would occur in a case like the following:

```css
#example {
  border-style: solid;
  border-color: tan red;
  border-width: 20px;
  border-radius: 20px;
}
```

#### INDIVIDUAL ROUNDING PROPERTIES

After that tour of border-radius, you might be wondering if maybe you could just round one corner at a time. Yes, you can!

<!-- <Cards cards="border-top-left-radius_border-top-right-radius_border-bottomright-radius_border-bottom-left-radius" /> -->

Each property sets the curve shape for its corner, and doesn’t affect the others. The fun part is that if you supply two values, one for the horizontal radius and one for the vertical radius, there is not a slash separating them. Really. This means that the following two rules are functionally equivalent:

```css
#example {
  border-radius: 1.5em 2vw 20% 0.67ch / 2rem 1.2vmin 1cm 10%;
}
#example {
  border-top-left-radius: 1.5em 2rem;
  border-top-right-radius: 2vw 1.2vmin;
  border-bottom-right-radius: 20% 1cm;
  border-bottom-left-radius: 0.67ch 10%;
}
```

The individual corner border radius properties are mostly useful for scripting, or for setting a common corner rounding and then overriding just one. Thus, a right-hand-tab shape could be done as follows:

```css
.tabs {
  border-radius: 2em;
  border-bottom-left-radius: 0;
}
```

One thing to keep in mind that, as we’ve seen, corner shaping affects the background and (potentially) the padding and content areas of the element, but not any image borders. Wait a minute, image borders? What are those? Glad you asked!

### 8.3.8 图像边框

The various border styles are nice enough, but are still fairly limited. What if you want to create a really complicated, visually rich border around some of your elements? Back in the day, we’d create complex multirow tables to achieve that sort of effect, but thanks to the image borders added to CSS in the recent past, there’s almost no limit to the kinds of borders you can create.

LOADING AND SLICING A BORDER IMAGE
If you’re going to use an image to create the borders of an image, you’ll need to fetch it from somewhere. border-image-source is how you tell the browser where to look for it.

<!-- <Cards cards="border-image-source" /> -->

Let’s load an image of a single circle to be used as the border image, using the following styles, whose result is shown in Figure 8-43:

```css
border: 25px solid;
border-image-source: url(i/circle.png);
```

<!-- <Figures figure="8-43">Defining a border image’s source</Figures> -->

There are a number of things to note here. First, without the border: 25px solid declaration, there would have been no border at all. Remember, if the value of border-style is none, then the width of the border is zero. So in order to make a border image appear, you need to declare a border-style value other than none. It doesn’t have to be solid. Second, the value of border-width determines the actual width of the border images. Without a declared value, it will default to medium, which is in the vicinity of 3 pixels. (Actual value may vary.)

OK, so we set up a border area 25 pixels wide, and then applied an image to it. That gave us the same circle in each of the four corners. But why did it only appear there, and not along the sides? The answer to that is found in the way border-image-slice is defined.

<!-- <Cards cards="border-image-slice" /> -->

What border-image-slice does is set up a set of four slice-lines that are laid over the image, and where they fall determines how the image will be sliced up for use in an image border. It takes up to four values, defining (in order) offsets from the top, right, bottom, and left edges. Yep, there’s that TRBL pattern again! And value replication is also in effect here, so one value is used for all four offsets. Figure 8-44 shows a small sampling of offset patterns, all based on percentages.

<!-- <Figures figure="8-44">Various slicing patterns</Figures> -->

Now let’s take an image that has a 3 × 3 grid of circles, each a different color, and slice it up for use in an image border. Figure 8-45 shows a single copy of this image and the resulting image border:

```css
border: 25px solid;
border-image-source: url(i/circles.png);
border-image-slice: 33.33%;
```

<!-- <Figures figure="8-45">An all-around image border</Figures> -->

Yikes! That’s…interesting. The stretchiness of the sides is actually the default behavior, and it makes a fair amount of sense, as we’ll see (and find out how to change) in the upcoming section, “Altering the repeat pattern”. Beyond that effect, you can see in Figure 8-45 that the slice-lines fall right between the circles, because the circles are all the same size and so one-third offsets place the slice-lines right between them. The corner circles go into the corners of the border, and each side’s circle is stretched out to fill its side.

(Wait, what happened to the gray circle in the middle? you may wonder. It’s an interesting question! For now, just accept it as one of life’s little mysteries, albeit a mystery that will be explained later in this section.)

All right, so why did our first border image example, back at the beginning of the section, only place images in the corners of the border area instead of all the way around it? Because there’s an interesting wrinkle in the way border-image-slice is defined. Here’s how the relevant bits of the specification read:

if the sum of the right and left [border-image-slice] widths is equal to or greater than the width of the image, the images for the top and bottom edge and the middle part are empty…Analogously for the top and bottom values.

In other words, any time the slice-lines meet or go past each other, the corner images are created but the side images are made empty. This is easiest to visualize with border-image-slice: 50%. In that case, the image is sliced into four quadrants, one for each corner, with nothing remaining for the sides. However, any value above 50% has the same basic result, even though the image isn’t sliced into neat quadrants anymore. Thus, for border-image-slice: 100%—which is the default value—each corner gets the entire image, and the sides are left empty. A few examples of this effect are shown in Figure 8-46.

<!-- <Figures figure="8-46">Various patterns that prevent side slices</Figures> -->

That’s why we had to have a 3 × 3 grid of circles when we wanted to go all the way around the border area, corners, and sides.

In addition to percentage offsets, it’s also possible to define the offsets using a number. Not a length, as you might assume, but a bare number. In raster images like PNGs or JPEGs, the number corresponds to pixels in the image on a 1:1 basis. If you have a raster image where you want to define 25-pixel offsets for the slice-lines, this is how to do that, as illustrated in Figure 8-47:

```css
border: 25px solid;
border-image-source: url(i/circles.png);
border-image-slice: 25;
```

Yikes again! What happened there is that the raster image is 150 × 150 pixels, so each circle is 50 × 50 pixels. Our offsets, though, were only 25, as in 25 pixels. So the slice-lines were placed on the image as shown in Figure 8-48.

This begins to give an idea of why the default behavior for the side images is to stretch them. Note how the corners flow into the sides, visually speaking.

Number offsets don’t scale when changes are made to an image and its size, whereas percentages do. The interesting thing about number offsets is that they work just as well on non-raster images, like SVGs, as they do on rasters. So do percentages. In general, it’s probably best to use percentages for your slicing offsets whenever possible, even if means doing a little math to get exactly the right percentages.

<!-- <Figures figure="8-47">Number slicing</Figures> -->

<!-- <Figures figure="8-48">Slice-lines at 25 pixels</Figures> -->

Now let’s address the curious case of the image’s center. In the previous examples, there’s a circle at the center of the 3 × 3 grid of circles, but it disappears when the image is applied to the border. In the last example, in fact, it wasn’t just the middle circle that was missing, but the entire center slice. This dropping of the center slice is the default behavior for image-slicing, but you can override it by adding a fill keyword to the end of your border-image-slice value. If we add fill to the previous example, as shown here, we’ll get the result shown in Figure 8-49:

```css
border: 25px solid;
border-image-source: url(i/circles.png);
border-image-slice: 25 fill;
```

<!-- <Figures figure="8-49">Using the fill slice</Figures> -->

There’s the center slice, filling up the element’s background area. In fact, it’s drawn over top of whatever background the element might have, so you can use it as a substitute for the background, or as an addition to it.

You may have noticed that all our border areas have been a consistent width (usually 25px). This doesn’t have to be the case, regardless of how the border image is actually sliced up. Suppose we take the circles border image we’ve been using, slice it by thirds as we have, but make the border widths different. That would have a result like that shown in Figure 8-50:

```css
border-style: solid;
border-width: 20px 40px 60px 80px;
border-image-source: url(i/circles.png);
border-image-slice: 50;
```

Even though the slice-lines are intrinsically set to 50 pixels (via 50), the resulting slices are resized to fit into the border areas they occupy.

<!-- <Figures figure="8-50">Uneven border image widths</Figures> -->

ALTERING THE IMAGE WIDTHS
Thus far, all our image borders have depended on a border-width value to set the sizes of the border areas, which the border images have filled out precisely. That is, if the top border side is 25 pixels tall, the border image that fills it will be 25 pixels tall. In cases where you want to make the images a different size than the area defined by border-width, there’s border-image-width.

<!-- <Cards cards="border-image-width" /> -->

The basic thing to understand about border-image-width is that it’s very similar to border-image-slice, except what border-image-width slices up is the border box itself.

To understand what this means, let’s start with length values. We’ll set up 1 em border widths like so:

```css
border-image-width: 1em;
```

What that does is push slice-lines 1 em inward from each of the border area’s sides, as shown in Figure 8-51.

<!-- <Figures figure="8-51">Placing slice-lines for the border image’s width</Figures> -->

So the top and bottom border areas are 1 em tall, the right and left border areas are 1 em wide, and the corners are each 1 em tall and wide. Given that, the border images created with border-image-slice are filled into those border areas in the manner prescribed by border-image-repeat (which we’ll get to shortly). Thus, the following styles give the result shown in Figure 8-52:

```css
border-image-width: 1em;
border-image-slice: 33.3333%;
```

Note that these areas are sized independently from the value of border-width. Thus, in Figure 8-52, we could have had a border-width of zero and still made the border images show up, by using border-image-width. This is useful if you want to have a solid border as a fallback in case the border image doesn’t load, but don’t want to make it as thick as the image border would be. Something like this:

```css
border: 2px solid;
border-image-source: url(stars.gif);
border-image-width: 12px;
border-image-slice: 33.3333%;
```

<!-- <Figures figure="8-52">Filling in the border areas</Figures> -->

This allows for a 12-pixel star border to be replaced with a 2-pixel solid border if border images aren’t available. Remember that if the image border does load, you’ll need to leave enough space for it to show up without overlapping the content! (By default, that is. We’ll see how to mitigate this problem in the next section.)

Now that we’ve established how the width slice-lines are placed, the way percentage values are handled should make sense, as long as you keep in mind that the offsets are with respect to the overall border box, not each border side. For example, consider the following declaration, illustrated in Figure 8-53:

```css
border-image-width: 33%;
```

<!-- <Figures figure="8-53">Placement of percentage slice-lines</Figures> -->

As with length units, the lines are offset from their respective sides of the border box. The distance they travel is with respect to the border box. A common mistake is to assume that a percentage value is with respect to the border area defined by border-width; that is, given a border-width value of 30px, the result of border-image-width: 33.333%; will be 10 pixels. But no! It’s one-third the overall border box along that axis.

One way in which the behavior of border-image-width differs from border-image-slice is in how it handles situations where the slices pass each other, such as in this situation:

```css
border-image-width: 75%;
```

If you recall, for border-image-slice, if the slices passed each other, then the side areas (top, right, bottom, and/or left) are made empty. With border-image-width, the values are proportionally reduced until they don’t. So, given the preceding value of 75%, the browser will treat that as if it were 50%. Similarly, the following two declarations will have equivalent results:

```css
border-image-width: 25% 80% 25% 40%;
border-image-width: 25% 66.6667% 25% 33.3333%;
```

Note how in both declarations, the right offset is twice the left value. That’s what’s meant by proportionally reducing the values until they don’t overlap: in other words, until they no longer add up to more than 100%. The same would be done with top and bottom, were they to overlap.

When it comes to number values for border-image-width, things get even more interesting. If you set border-image-width: 1, then the border image areas will be determined by the value of border-width. That’s the default behavior. Thus, the following two declarations will have the same result:

```css
border-width: 1em 2em;
border-image-width: 1em 2em;
border-width: 1em 2em;
border-image-width: 1;
```

You can increase or reduce the number values in order to get some multiple of the border area that border-width defines. A few examples of this can be seen in Figure 8-54.

In each case, the number has been multipled by the border area’s width or height, and the resulting value is how far in the offset is placed from the relevant side. Thus, for an element where border-top-width is 3 pixels, border-image-width: 10 will create a 30-pixel offset from the top of the element. Change border-image-width to 0.333, and the top offset will be a lone pixel.

<!-- <Figures figure="8-54">Various numeric border image widths</Figures> -->

The last value, auto, is interesting in that its resulting values depend on the state of two other properties. If border-image-slice is defined, then border-image-width: auto uses the values that result from border-image-slice. Otherwise, it uses the values that result from border-width. These two declarations will have the same result:

```css
border-width: 1em 2em;
border-image-width: auto;
border-image-slice: 1em 2em;
border-image-width: auto;
```

This differs from border-image-width: 1 because number values like 1 always relate to the value of border-width, regardless of what border-image-slice might say.

Note that you can mix up the value types for border-image-width. The following are all valid, and would be quite interesting to try out in live web pages:

```css
border-image-width: auto 10px;
border-image-width: 5 15% auto;
border-image-width: 0.42em 13% 3.14 auto;
```

#### CREATING A BORDER OVERHANG

Well, now that we can define these great big image slices and widths, what do we do to keep them from overlapping the content? We could add lots of padding, but that would leave huge amounts of space if the image fails to load, or if the browser doesn’t support border images. Handling such scenarios is what border-image-outset is built to manage.

<!-- <Cards cards="border-image-outset" /> -->

Regardless of whether you use a length or a number, border-image-outset pushes the border image area outward, beyond the border box, in a manner similar to how slice-lines are offset. The difference is that here, the offsets are outward, not inward. Just as with border-image-width, number values for border-image-outset are a multiple of the width defined by border-width—not border-image-width.

To see how this could be helpful, imagine a scenario where we want to use a border image, but have a fallback of a thin solid border if the image isn’t available. We might start out like this:

```css
border: 2px solid;
padding: 0.5em;
border-image-slice: 10;
border-image-width: 1;
```

In this case, there’s half an em of padding; at default browser settings, that will be about eight pixels. That plus the 2-pixel solid border make a distance of 10 pixels from the content edge to the outer border edge. So if the border image is available and rendered, it will fill not only the border area, but also the padding, bringing it right up against the content.

We could increase the padding to account for this, but then if the image doesn’t appear, we’ll have a lot of excess padding between the content and the thin solid border. Instead, let’s push the border image outward, like so:

```css
border: 2px solid;
padding: 0.5em;
border-image-slice: 10;
border-image-width: 1;
border-image-outset: 8px;
```

This is illustrated in Figure 8-55, and compared to situation where there’s no outset and no border image.

<!-- <Figures figure="8-55">Creating an image border overhang</Figures> -->

In the first case, the image border has been pushed out far enough that rather than overlapping the padding area, the images actually overlap the margin area! We can also split the difference so that the image border is roughly centered on the border area, like this:

```css
border: 2px solid;
padding: 0.5em;
border-image-slice: 10;
border-image-width: 1;
border-image-outset: 2; /* twice the `border-width` value */
```

What you have to watch out for is pulling the image border too far outward, to the point that it overlaps other content or gets clipped off by the edges of the browser window (or both).

ALTERING THE REPEAT PATTERN
So far, we’ve seen a lot of stretched-out images along the sides of our examples. The stretching can be very handy in some situations, but a real eyesore in others. With border-image-repeat, you can change how those sides are handled.

<!-- <Cards cards="border-image-repeat" /> -->

Let’s see these values in action and then discuss each in turn.

We’ve already seen stretch, so the effect is familiar. Each side gets a single image, stretched to match the height and width of the border side area the image is filling.

repeat has the image tile until it fills up all the space in its border side area. The exact arrangement is to center the image in its side box, and then tile copies of the image outward from that point, until the border side area is filled. This can lead to some of the repeated images being clipped at the sides of the border area, as seen in Figure 8-56.

<!-- <Figures figure="8-56">Various image-repeat patterns</Figures> -->

round is a little different. With this value, the browser divides the length of the border side area by the size of the image being repeated inside it. It then rounds to the nearest whole number and repeats that number of images. In addition, it stretches or squashes the images so that they just touch each other as they repeat.

As an example, suppose the top border side area is 420 pixels wide, and the image being tiled is 50 pixels wide. 420 divided by 50 is 8.4, so that’s rounded to 8. Thus, 8 images are tiled. However, each is stretched to be 52.5 pixels wide (420 ÷ 8 = 52.5). Similarly, if the right border side area is 280 pixels tall, a 50-pixel-tall image will be tiled 6 times (280 ÷ 50 = 5.6, rounded to 6) and each image will be squashed to be 46.6667 pixels tall (280 ÷ 6 = 46.6667). If you look closely at Figure 8-56, you can see the top and bottom circles are a stretched a bit, whereas the right and left circles show some squashing.

The last value, space, starts out similar to round, in that the border side area’s length is divided by the size of the tiled image and then rounded. The differences are that the resulting number is always rounded down, and images are not distorted, but instead distributed evenly throughout the border area.

Thus, given a top border side area 420 pixels wide and a 50-pixel-wide image to be tiled, there will still be 8 images to repeat (8.4 rounded down is 8). The images will take up 400 pixels of space, leaving 20 pixels. That 20 pixels is divided by 8, which is 2.5 pixels. Half of that is put to each side of each image, meaning each image gets 1.25 pixels of space to either side. That puts 2.5 pixels of space between each image, and 1.25 pixels of space before the first and after the last image. Figure 8-57 shows a few examples of space repeating.

<!-- <Figures figure="8-57">A variety of space repetitions</Figures> -->

<Tips tips="orange">As of late 2017, Chrome and Opera did not support space on border images.</Tips>

#### SHORTHAND BORDER IMAGE

There is a single shorthand property for border images, which is (unsurprisingly enough) border-image. It’s a little unusual in how it’s written, but it offers a lot of power without a lot of typing.

<!-- <Cards cards="border-image" /> -->

This property has, it must be admitted, a somewhat unusual value syntax. In order to get all the various properties for slices and widths and offsets, and be able to tell which was which, the decision was made to separate them by solidus symbols (/) and require them to be listed in a specific order: slice, then width, then offset. The image source and repeat values can go anywhere outside of that three-value chain. Therefore, the following rules are equivalent:

```css
.example {
  border-image-source: url(eagles.png);
  border-image-slice: 40% 30% 20% fill;
  border-image-width: 10px 7px;
  border-image-outset: 5px;
  border-image-repeat: space;
}
.example {
  border-image: url(eagles.png) 40% 30% 20% fill / 10px 7px / 5px space;
}
.example {
  border-image: url(eagles.png) space 40% 30% 20% fill / 10px 7px / 5px;
}
.example {
  border-image: space 40% 30% 20% fill / 10px 7px / 5px url(eagles.png);
}
```

The shorthand clearly means less typing, but also less clarity at a glance.

As is usually the case with shorthand properties, leaving out any of the individual pieces means that the defaults will be supplied. For example, if we just supply an image source, the rest of the properties will get their default values. Thus, the following two declarations will have exactly the same effect:

```css
border-image: url(orbit.svg);
border-image: url(orbit.svg) stretch 100% / 1 / 0;
```

SOME EXAMPLES
Border images can be tricky to internalize, conceptually speaking, so it’s worth looking at some examples of ways to use them.

First, let’s look at how to set up a border with scooped-out corners and a raised appearance, like a plaque, with a fallback to a simple outset border of similar colors. We might use something like these styles and an image, which is shown in Figure 8-58, along with both the final result and the fallback result:

```css
#plaque {
  padding: 10px;
  border: 3px outset goldenrod;
  background: goldenrod;
  border-image-source: url(i/plaque.png);
  border-image-repeat: stretch;
  border-image-slice: 20 fill;
  border-image-width: 12px;
  border-image-outset: 9px;
}
```

<!-- <Figures figure="8-58">A simple plaque effect and its older-browser fallback</Figures> -->

Notice how the side slices are perfectly set up to be stretched—everything about them is just repeated strips of color along the axis of stretching. They could also be repeated or rounded, of course, if not rounded, but stretching works just fine. And since that’s the default value, we could have omitted the border-image-repeat declaration altogether.

Next, let’s try to create something oceanic: an image border that has waves marching all the way around the border. Since we don’t know how wide or tall the element will be ahead of time, and we want the waves to flow from one to another, we’ll use round to take advantage of its scaling behavior while getting in as many waves as will reasonably fit. You can see the result in Figure 8-59, along with the image that’s used to create the effect:

```css
#oceanic {
  border: 2px solid blue;
  border-image: url(waves.png) 50 fill / 20px / 10px round;
}
```

<!-- <Figures figure="8-59">A wavy border</Figures> -->

There is one thing to be wary of here, which is what happens if you add in an element background. Just to make the situation clear, we’ll add a red background to this element, with the result shown in Figure 8-60:

```css
#oceanic {
  background: red;
  border: 2px solid blue;
  border-image: url(waves.png) 50 fill / 20px / 10px round;
}
```

See how the red is visible between the waves? That’s because the wave image is a PNG with transparent bits, and because of the combination of image-slice widths and outset, some of the background area is visible through the transparent parts of the border. This can be a problem, because there will be cases where you want to use a background color in addition to an image border—for the fallback case where the image fails to appear, if nothing else. Generally, this is a problem best addressed by either not needing a background for the fallback case, or else using border-image-outset to pull the image out far enough that no part of the background area is visible.

As you can see, there is a lot of power in border images. Be sure to use them wisely.

<!-- <Figures figure="8-60">The background area, visible through the image border</Figures> -->

## 8.4 轮廓

CSS defines a special sort of element decoration called an outline. In practice, outlines are often drawn just beyond the borders, though (as we’ll see) this is not the whole story. As the specification puts it, outlines differ from borders in three basic ways:

Outlines do not take up space.

Outlines may be nonrectangular.

User agents often render outlines on elements in the :focus state.

To which I’ll add a fourth:

Outlines are an all-or-nothing proposition: you can’t style one side of a border independently from the others.

Let’s start finding out exactly what all that means. First, we’ll run through the various properties, comparing them to their border-related counterparts.

### 8.4.1 轮廓式样

Much as with border-style, you can set a style for your outlines. In fact, the values will seem very familiar to anyone who’s styled a border before.

<!-- <Cards cards="outline-style" /> -->

The two major differences are that outlines cannot have a hidden style, as borders can; and outlines can have auto style. This style allows the user agent to get extra-fancy with the appearance of the outline, as explained in the CSS specification:

The auto value permits the user agent to render a custom outline style, typically a style which is either a user interface default for the platform, or perhaps a style that is richer than can be described in detail in CSS, e.g. a rounded edge outline with semi-translucent outer pixels that appears to glow.

Beyond those two differences, outlines have all the same styles that borders have, as illustrated in Figure 8-61.

<!-- <Figures figure="8-61">Various outline styles</Figures> -->

The less obvious difference is that unlike border-style, outline-style is not a shorthand property. You can’t use it to set a different outline style for each side of the outline, because outlines can’t be styled that way. There is no outline-top-style. This is true for all the rest of the outline properties, with the exception of outline, which we’ll get to in a bit.

### 8.4.2 轮廓宽度

Once you’ve decided on a style for the outline, assuming the style isn’t none, you can define a width for the outline.

<!-- <Cards cards="outline-width" /> -->

There’s very little to say about outline width that we didn’t already say about border width. If the outline style is none, then the outline’s width is set to 0. thick is wider than medium, which is wider than thin, but the specification doesn’t define exact widths for these keywords. Figure 8-62 shows a few different outline widths.

<!-- <Figures figure="8-62">Various outline widths</Figures> -->

As before, the real difference here is that outline-width is not a shorthand property. You can only set one width for the whole outline, and cannot set different widths for different sides. (The reasons for this will soon become clear.)

### 8.4.3 轮廓颜色

Does your outline have a style and a width? Great! Let’s give it some color!

<!-- <Cards cards="outline-color" /> -->

This is pretty much the same as border-color, with the caveat that it’s an all-or-nothing proposition—for example, there’s no outline-left-color.

The one major difference is the default value, invert. What invert does is perform a “color conversion” on all pixels within the visible parts of the outline. This is easier to show than explain, so see Figure 8-63 for the expected results of this style:

```css
h1 {
  outline-style: dashed;
  outline-width: 10px;
  outline-color: invert;
}
```

<!-- <Figures figure="8-63">Color inversion</Figures> -->

The advantage to color inversion is that it can make the outline stand out in a wide variety of situations, regardless of what’s behind it. There is an exception: if you invert the color gray (or rgb(50%,50%,50%) or hsl(0,0%,50%) or any of their equivalents), you get exactly the same color back. Thus, outline-color: invert will make the outline invisible on a gray background. The same will be true for background colors that are very close to gray.

<Tips tips="orange">As of late 2017, <code>invert</code> was only supported by Microsoft Edge and IE11. Most other browsers treated it as an error and thus used the default color (the value of <code>color</code> for the element).</Tips>

#### THE ONLY OUTLINE SHORTHAND

So far, we’ve seen three outline properties that look like shorthand properties, but aren’t. Time for the one outline property that is a shorthand: outline.

<!-- <Cards cards="outline" /> -->

It probably comes as little surprise that, like border, this is a convenient way to set the overall style, width, and color of an outline. Figure 8-64 illustrates a variety of outlines.

<!-- <Figures figure="8-64">Various outlines</Figures> -->

Thus far, outlines seem very much like borders. So how are they different?

### 8.4.4 轮廓与边框的区别

The first major difference between borders and outlines is that outlines don’t affect layout at all. In any way. They’re very purely presentational.

To understand what this means, consider the following styles, illustrated in Figure 8-65:

```css
h1 {
  padding: 10px;
  border: 10px solid green;
  outline: 10px dashed #9ab;
  margin: 10px;
}
```

<!-- <Figures figure="8-65">Outline over margin</Figures> -->

Looks normal, right? What you can’t see is that the outline is completely covering up the margin. If we put in a dotted line to show the margin edges, they’d run right along the outside edge of the outline. (We’ll deal with margins in the next section.)

This is what’s meant by outlines not affecting layout. Let’s consider another example, this time with two span elements that are given outlines. You can see the results in Figure 8-66:

```css
span {
  outline: 1em solid rgba(0, 128, 0, 0.5);
}
span + span {
  outline: 0.5em double purple;
}
```

<!-- <Figures figure="8-66">Overlapping outlines</Figures> -->

The outlines don’t affect the height of the lines, but they also don’t shove the spans to one side or another. The text is laid out as if the outlines aren’t even there.

This raises an even more interesting feature of outlines: they are not always rectangular, nor are they always contiguous. Consider this outline applied to a strong element that breaks across two lines, as illustrated in two different scenarios in Figure 8-67:

```css
strong {
  outline: 2px dotted gray;
}
```

<!-- <Figures figure="8-67">Discontinuous and nonrectangular outlines</Figures> -->

In the first case, there are two complete outline boxes, one for each fragment of the strong element. In the second case, with the longer strong element causing the two fragments to be stacked together, the outline is “fused” into a single polygon that encloses the fragments. You won’t find a border doing that.

This is why there are no side-specific outline properties like outline-right-style: if an outline becomes nonrectangular, which sides are the right sides?

<Tips tips="orange">As of late 2017, not every browser combined the inline fragments into a single contiguous polygon. In those which did not support this behavior, each fragment was still a self-contained rectangle, as in the first example in Figure 8-67.</Tips>

## 8.5 外边距

a margin creates extra blank space around an element. Blank space generally refers to an area in which other elements cannot also exist and in which the parent element’s background is visible. Figure 8-68 shows the difference between two paragraphs without any margins and the same two paragraphs with some margins.

<!-- <Figures figure="8-68">Paragraphs with, and without, margins</Figures> -->

The simplest way to set a margin is by using the property margin.

<!-- <Cards cards="margin" /> -->

Suppose you want to set a quarter-inch margin on h1 elements, as illustrated in Figure 8-69 (a background color has been added so you can clearly see the edges of the content area):

```css
h1 {
  margin: 0.25in;
  background-color: silver;
}
```

This sets a quarter-inch of blank space on each side of an h1 element. In Figure 8-69, dashed lines represent the blank space, but the lines are purely illustrative and would not actually appear in a web browser.

<!-- <Figures figure="8-69">Setting a margin for h1 elements</Figures> -->

margin can accept any length of measure, whether in pixels, inches, millimeters, or ems. However, the default value for margin is effectively 0 (zero), so if you don’t declare a value, by default, no margin should appear.

In practice, however, browsers come with preassigned styles for many elements, and margins are no exception. For example, in CSS-enabled browsers, margins generate the “blank line” above and below each paragraph element. Therefore, if you don’t declare margins for the p element, the browser may apply some margins on its own. Whatever you declare will override the default styles.

Finally, it’s possible to set a percentage value for margin. The details of this value type will be discussed in “Percentages and Margins”.

### 8.5.1 外边距的长度值

Any length value can be used in setting the margins of an element. It’s easy enough, for example, to apply a 10-pixel whitespace around paragraph elements. The following rule gives paragraphs a silver background, 10 pixels of padding, and a 10-pixel margin:

```css
p {
  background-color: silver;
  padding: 10px;
  margin: 10px;
}
```

In this case, 10 pixels of space have been added to each side of every paragraph, just beyond the outer border edge. You can just as easily use margin to set extra space around an image. Let’s say you want 1 em of space surrounding all images:

```css
img {
  margin: 1em;
}
```

That’s all it takes.

At times, you might desire a different amount of space on each side of an element. That’s easy as well, thanks to the value replication behavior we’ve used before. If you want all h1 elements to have a top margin of 10 pixels, a right margin of 20 pixels, a bottom margin of 15 pixels, and a left margin of 5 pixels, here’s all you need:

```css
h1 {
  margin: 10px 20px 15px 5px;
}
```

It’s also possible to mix up the types of length value you use. You aren’t restricted to using a single length type in a given rule, as shown here:

```css
h2 {
  margin: 14px 5em 0.1in 3ex;
} /* value variety! */
```

Figure 8-70 shows you, with a little extra annotation, the results of this declaration.

<!-- <Figures figure="8-70">Mixed-value margins</Figures> -->

### 8.5.2 外边距的百分数值

It’s possible to set percentage values for the margins of an element. As with padding, percentage margins values are computed in relation to the width of the parent element’s content area, so they can change if the parent element’s width changes in some way. For example, assume the following, which is illustrated in Figure 8-71:

```css
p {
  margin: 10%;
}
```

```html
<div style="width: 200px; border: 1px dotted;">
  <p>
    This paragraph is contained within a DIV that has a width of 200 pixels, so
    its margin will be 10% of the width of the paragraph's parent (the DIV).
    Given the declared width of 200 pixels, the margin will be 20 pixels on all
    sides.
  </p>
</div>
<div style="width: 100px; border: 1px dotted;">
  <p>
    This paragraph is contained within a DIV with a width of 100 pixels, so its
    margin will still be 10% of the width of the paragraph's parent. There will,
    therefore, be half as much margin on this paragraph as that on the first
    paragraph.
  </p>
</div>
```

Note that the top and bottom margins are consistent with the right and left margins; in other words, the percentage of top and bottom margins is calculated with respect to the element’s width, not its height. We’ve seen this before—in “Padding”, in case you don’t remember—but it’s worth reviewing again, just to see how it operates.

<!-- <Figures figure="8-71">Parent widths and percentages</Figures> -->

<Tips tips="blue">As with padding, the treatment of percentage values for top and bottom margins is different for most positioned elements, flex items, and grid items, where they are calculated with respect to the height of their formatting context.</Tips>

### 8.5.3 单边外边距属性

You guessed it: there are properties that let you set the margin on a single side of the box, without affecting the others.

<!-- <Cards cards="margin-top_margin-right_margin-bottom_margin-left" /> -->

These properties operate as you’d expect. For example, the following two rules will give the same amount of margin:

```css
h1 {
  margin: 0 0 0 0.25in;
}
h2 {
  margin-left: 0.25in;
}
```

### 8.5.4 外边距折叠

An interesting and often overlooked aspect of the top and bottom margins on block boxes is that they collapse. This is the process by which two (or more) margins that interact collapse to the largest of the interacting margins.

The canonical example of this is the space between paragraphs. Generally, that space is set using a rule like this:

```css
p {
  margin: 1em 0;
}
```

So that sets every paragraph to have top and bottom margins of 1em. If margins didn’t collapse, then whenever one paragraph followed another, there would be two ems of space between them. Instead, there’s only one; the two margins collapse together.

To illustrate this a little more clearly, let’s return to the percentage-margin example, only this time, we’ll add dashed lines to indicate where the margins fall. This is seen in Figure 8-72.

<!-- <Figures figure="8-72">Collapsing margins</Figures> -->

The example shows the separation distance between the contents of the two paragraphs. It’s 60 pixels, because that’s the larger of the two margins that are interacting. The 30-pixel top margin of the second paragraph is collapsed, leaving the first paragraph’s top margin in charge.

So in a sense, Figure 8-72 is lying: if you take the CSS specification strictly at its word, the top margin of the second paragraph is actually reset to zero. It doesn’t stick into the bottom margin of the first paragraph because when it collapses, it isn’t there anymore. The end result is the same, though.

Margin collapsing also explains some oddities that arise when one element is inside another. Consider the following styles and markup:

```css
header {
  background: goldenrod;
}
h1 {
  margin: 1em;
}
```

```html
<header>
  <h1>Welcome to ConHugeCo</h1>
</header>
```

The margin on the h1 will push the edges of the header away from the content of the h1, right? Well, not entirely. See Figure 8-73.

What happened? The side margins took effect—we can see that from the way the text is moved over—but the top and bottom margins are gone!

Only they aren’t gone. They’re just sticking out of the header element, having interacted with the (zero-width) top margin of the header element. The magic of dashed lines in Figure 8-74 show us what’s happening.

<!-- <Figures figure="8-73">Margins collapsing with parents</Figures> -->

<!-- <Figures figure="8-74">Margins collapsing with parents, revealed</Figures> -->

There they are—pushing away any content that might come before or after the header element, but not pushing away the edges of the header itself. This is the intended result, even if it’s often not the desired result. As for why it’s intended, imagine happens if you put a paragraph in a list item. Without the specified margin-collapsing behavior, the paragraph’s top margin would shove it downward, where it would be far out of alignment with the list item’s bullet (or number).

<Tips tips="blue">Margin collapsing can be interrupted by factors such as padding and borders on parent elements. For more details, see the discussion in the section “Collapsing Vertical Margins” in Chapter 7 of Basic Visual Formatting (O’Reilly).</Tips>

### 8.5.5 负外边距

It’s possible to set negative margins for an element. This can cause the element’s box to stick out of its parent or to overlap other elements. Consider these rules, which are illustrated in Figure 8-75:

```css
div {
  border: 1px solid gray;
  margin: 1em;
}
p {
  margin: 1em;
  border: 1px dashed silver;
}
p.one {
  margin: 0 -1em;
}
p.two {
  margin: -1em 0;
}
```

<!-- <Figures figure="8-75">Negative margins in action</Figures> -->

In the first case, the math works out such that the paragraph’s computed width plus its right and left margins are exactly equal to the width of the parent div. So the paragraph ends up two ems wider than the parent element without actually being “wider” (from a mathematical point of view). In the second case, the negative top and bottom margins effectively reduce the computed height of the element and move its top and bottom outer edges inward, which is how it ends up overlapping the paragraphs before and after it.

Combining negative and positive margins is actually very useful. For example, you can make a paragraph “punch out” of a parent element by being creative with positive and negative margins, or you can create a Mondrian effect with several overlapping or randomly placed boxes, as shown in Figure 8-76:

```css
div {
  background: hsl(42, 80%, 80%);
  border: 1px solid;
}
p {
  margin: 1em;
}
p.punch {
  background: white;
  margin: 1em -1px 1em 25%;
  border: 1px solid;
  border-right: none;
  text-align: center;
}
p.mond {
  background: rgba(5, 5, 5, 0.5);
  color: white;
  margin: 1em 3em -3em -3em;
}
```

Thanks to the negative bottom margin for the “mond” paragraph, the bottom of its parent element is pulled upward, allowing the paragraph to stick out of the bottom of its parent.

<!-- <Figures figure="8-76">Punching out of a parent</Figures> -->

### 8.5.6 行内元素的外边距

Margins can also be applied to inline elements. Let’s say you want to set top and bottom margins on strongly emphasized text:

```css
strong {
  margin-top: 25px;
  margin-bottom: 50px;
}
```

This is allowed in the specification, but since you’re applying the margins to an inline nonreplaced element, and margins are always transparent, they will have absolutely no effect on the line height. In effect, they’ll have no effect at all.

As with padding, things change a bit when you apply margins to the left and right sides of an inline nonreplaced element, as illustrated in Figure 8-77:

```css
strong {
  margin-left: 25px;
  background: silver;
}
```

<!-- <Figures figure="8-77">An inline nonreplaced element with a left margin</Figures> -->

Note the extra space between the end of the word just before the inline nonreplaced element and the edge of the inline element’s background. You can add that extra space to both ends of the inline element if you want:

```css
strong {
  margin: 25px;
  background: silver;
}
```

As expected, Figure 8-78 shows a little extra space on the right and left sides of the inline element, and no extra space above or below it.

<!-- <Figures figure="8-78">An inline nonreplaced element with 25-pixel side margins</Figures> -->

Now, when an inline nonreplaced element stretches across multiple lines, the situation changes. Figure 8-79 shows what happens when an inline nonreplaced element with a margin is displayed across multiple lines:

```css
strong {
  margin: 25px;
  background: silver;
}
```

<!-- <Figures figure="8-79">An inline nonreplaced element with 25-pixel side margin displayed across two lines of text</Figures> -->

The left margin is applied to the beginning of the element and the right margin to the end of it. Margins are not applied to the right and left side of each line fragment. Also, you can see that, if not for the margins, the line may have broken after “text” instead of after “strongly emphasized.” Margins only affect line breaking by changing the point at which the element’s content begins within a line.

<Tips tips="blue">The way margins are (or aren’t) applied to the ends of each line box can be altered with the property box-decoration-break. See Chapter 7 for more details.</Tips>

The situation gets even more interesting when we apply negative margins to inline nonreplaced elements. The top and bottom of the element aren’t affected, and neither are the heights of lines, but the left and right ends of the element can overlap other content, as depicted in Figure 8-80:

```css
strong {
  margin: -25px;
  background: silver;
}
```

<!-- <Figures figure="8-80">An inline nonreplaced element with a negative margin</Figures> -->

Replaced inline elements represent yet another story: margins set for them do affect the height of a line, either increasing or reducing it, depending on the value for the top and bottom margin. The left and right margins of an inline replaced element act the same as for a nonreplaced element. Figure 8-81 shows a series of different effects on layout from margins set on inline replaced elements.

<!-- <Figures figure="8-81">Inline replaced elements with differing margin values</Figures> -->

## 8.6 小结

The ability to apply margins, borders, and padding to any element is one of the things that sets CSS so far above traditional web markup. In the past, enclosing a heading in a colored, bordered box meant wrapping the heading in a table, which is a really bloated and awful way to create so simple an effect. It is this sort of power that makes CSS so compelling.

第 9 章 颜色、背景和渐变

# 下册

第 10 章 浮动和形状

# 第 11 章 定位

定位的原理相当简单。你可以相对元素框的常规位置定义元素的具体位置，可以相对父元素或另一个元素定位元素的位置，甚至还可以相对视区（例如浏览器窗口）定位元素的位置。

## 11.1 基本概念

在我们深入研究各种定位之前，最好先看看存在哪些类型以及它们之间的区别。我们还需要定义一些基本的概念，这些概念对于理解定位是如何工作的是非常重要的。

### 11.1.1 定位的类型

您可以使用 position 属性从五种不同的定位类型中选择一种，这将影响元素框的生成方式。

<!-- <Cards cards="position" /> -->

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

两个段落中的 b 元素都是绝对定位的，只是所用的容纳块不同。第一个段落中的 b 元素相对初始容纳块定位，因为它的所有祖辈元素的 position 值都是 static。第二个段落设置了 `position: relative`,因此它变成后代元素的容纳块。

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

> （元素的）“静态位置”基本上指的是元素在常规文档流中的位置。更准确地说是，静态位置的 top 值是容纳块的顶边距一个假想框体上外边距边界的距离。这个假想的框体是元素的第一个框体，而且它的 postion 值为 static、float 的值为 none,clear 的值为 none……如果假想的框体在容纳块上方，值为负。

因此，得到的结果如图 11-12 所示。

<!-- <Figures figure="11-12">Absolutely positioning an element consistently with its “static” top edge</Figures> -->

“[4]”在段落内容的外部，这是因为初始容纳块的左边界在段落左边界的左侧。

left 和 right 设为 auto 时也是如此，定位元素的左（或右）边界与元素未定位时左（或右）边界所在的位置对齐。下面在前例的基础上，把 top 和 left 的值都设为 auto:

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

首先，如果 left、width 和 right 都设为 auto,得到的结果与前一节见到的一样：在从左至右的书写语言中，左边界放在静态位置；在从右至左的书写语言中，右边界放在静态位置。元素的宽度设为“自动缩放”，因此元素内容区的宽度将恰好能放得下内容。非静态定位属性（从左至右语言中的 right,从右至左语言中的 left）设为 auto 的意思是占据余下的距离。例如：

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

问题出现了。我们定位的 span 元素，各个属性的值加在一起只有 14em,而容纳块的宽度是 25em,二者相差 11em,这是我们要找补的。

根据规则，在这种情况下，用户代理将忽略为 right 属性（针对从左向右书写的语言；反之忽略的是 left 属性）声明的值，补上差值。也就是说，结果与下述声明是一样的：

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

在第一种情况下，元素的高度正好放得下内容。在第二种情况下，未指定的属性（bottom）占据定位元素底边与容纳块底边之间的距离。在第三种情况下，top 未指定，因此用补足差值。

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

置换元素（例如图像）的定位规则与非置换元素不同。这是因为置换元素有内在的高度和宽度，除非由创作人员人为修改，否则不会变。因此，对定位的置换元素来说，没有动缩放”这一说。

置换元素的位置和尺寸由下述规则按顺序确定。

1. 如果把 Midth 设为 auto,width 的具体值由元素内容的内在宽度确定。因此，如果图像自身的宽度是 50 像素，那么计算得到的值是 sopx。如果明确声明了 width（所如 100px 或 50%）,那就使用设定的值。
2. 在从左至右书写的语言中，如果 1eft 的值是 auto,auto 将替换为静态位置。在从右至左书写的语言中，right 属性的 auto 值将被者换为静态位置。
3. 如果 left 或 right 的值仍是 auto（也就是说，在前一步中没有被替换）,把 margin-left 或 margin-right 的 auto 值替换为 0.
4. 如果此时 margin-left 和 margin-right 的值仍为 auto,把二者设为相等的值，即让元素居中显示在容纳块中。
5. 最后，如果还有一个属性的值为 auto,修改为满足等式所需的值。

这与明确为非置换元素设置 width 属性的行为基本一样。因此，假如图像自身的宽度是 100 像素，那么下述两个元素的宽度和位置都是一样的（见图 11-20）:

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

与非置换元素一样，如果导致过约束，用户代理将忽略 right（从左至右书写的语言）或 left（从右至左书写的语言）的值。因此，在下述示例中，为 right 声明的值将被计算得到的 50px 覆盖：

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

1. 如果把 height 设为 auto,height 的具体值由元素内容的内在高度确定。因此，如果图像自身的高度是 50 像素，那么计算得到的值是 50px。如果明确声明了 height（例如 100px 或 50%）,那就使用设定的值。
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

在这个坐标系统中，z-index 的值越大，元素离读者的距离越近。因此，值大的元素可能会遮盖其他元素，如图 11-23 所示（这是图 11-22 的正视图）。叠放的优先级称为堆叠次序（stacking）.

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

这几个元素根据相应的样式定位，但是常规的堆叠次序被 z-index 的值调整了。假设各段落是按顺序排列的，正常情况下，从下到上的顺序应该是 `p#first`、`p#second`、`p#third`,`p#fourth`,即 `p#first` 在其他三个元素后面，而 `p#fourth` 在其他元素前面。有了 z-index,我们便能自由掌控堆叠次序。

<!-- <Figures figure="11-24">Stacked elements can overlap</Figures> -->

如前例所示，z-index 的值无需连续，想使用多大的整数都可以。如果想确保某个元素一般都显示在其他内容前面，可以在规则中加上 z-index:100000。多数情况下，这样做能得到预期的结果。但是如果你把另一个元素的 z-index 声明为 100001（或更大的数）,那么它将显示在最前面。

为元素设定 z-index 后（值不为 auto）,元素便确立了自己的局部堆叠上下文。这意味着，所有后代元素的堆叠次序都相对祖辈元素而言。这与元素确立新的容纳块十分相似。下述样式将得到如图 11-25 所示的结果：

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

注意各 em 元素的堆叠次序，它们都相对父元素确定自己在布局中的位置。不管 em 元来的 z-index 值是正是负，都显示在父元素前面。父元素和子元素是组合在一起的，像图像编辑程序中的图层一样（根据规范，使用 z-index 设置堆叠次序时，子元素不能在父元素背后绘制，因此在 `p#three` 中，虽然 em 的 z-index 值为-343,但是依然在 `p#one` 之上给制）。元素的 z-index 值相对局部堆叠上下文，即容纳块。而容纳块也 z-index,也在局部堆叠上下文中处理。

z-index 还有一个值需要说明。CSS 规范是这样规定默认值 auto 的：

> 生成的框体在当前堆叠上下文中的堆叠次序是 0。如果不是根元素，不确立新的堆叠上下文。

因此，z-index:auto 可以视作 z-index:0。

> 尽管弹性布局和栅格布局中的元素不使用 position 属性定位，但是它们也受 z-index 的控制，相关的规则本质上是一样的。

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

此时，可以为 body 元素添加平铺的背景图。背景图透过外边距创建的间隙能看到，如果创作人员觉得合适，当然还可以增大间隙。

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

> 除了始终可见的元素之外，其他很多通过固定定位实现的效果都能使用栅格布局（译情参见第 13 章）实现，而且有时可能更方便。

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

因此，strong 元素将向下移动 10 像素，规范还考虑到了书写方向。对相对定位来说，在从左至右书写的语言中，right 始终等于`-left`;在从右至左书写的语言中，反过来 left 始终等于`-right`.

## 11.9 粘滞定位

css 新增了一种定位方式：粘滞定位。如果你在移动设备上用过优秀的音乐应用，或许记得这样的操作：滚动浏览按字母顺序排列的艺人时，当前字母始终停留在窗口的顶部直到进入一个新的字母，新字母取而代之，显示在窗口顶部。在纸上很难展示这种效果，不过图 11-30 展示了滚动过程中的三个瞬间，希望能让你明白。

<!-- <Figures figure="11-30">Sticky positioning</Figures> -->

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

注意，图 11.31 中的加元素其实在矩形的中间。这是常规文本流中 h2 在包含内容的位置。若想把 h2 粘滞在顶部，要滚动内容，让 h2 的顶边接触粘滞定位矩形的顶边，h2 就粘滞在哪里。这个过程如图 11-32 所示。

<!-- <Figures figure="11-32">Sticking to the top of the sticky-positioning rectangle</Figures> -->

也就是说，在 h2 的粘滞边界与矩形的粘滞边界接触之前，h2 一直在常规文档流中。当两个边界接触时，h2 粘滞在那里，就像是绝对定位了一样，不过 h2 在常规文档流中占据的空间会保留下来。

你可能注意到了，scrollbox 元素没有声明 position 属性。而且我们也没做什么其他设置，只是使用 overflow:scroll 为粘滞定位的 h2 元素创建一个容纳块。这是不使用 position 创建容纳块的一例。

如果向相反的方向滚动，把 h2 在常规文档流中的位置移到矩形顶边以下，h2 将与矩形分离，回到原本在常规文档流中的位置。这个过程如图 11-33 所示。

<!-- <Figures figure="11-33">Detaching from the top of the sticky-positioning rectangle</Figures> -->

注意，h2 之所以粘滞在矩形的顶部，是因为我们把 h2（即粘滞定位的元素）的 top 性设为了 auto 以外的其他值。你可以使用任何一个偏移边。例如，可以在向下滚动内容的过程中把元素粘滞在矩形的底部，如图 11-34 所示。

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

CSS Flexible Box Module Level 1（简称 [Flexbox](https://www.w3.org/TR/css-flexbox-1/)，弹性盒）把以往艰巨的布局任务变得极为简单，例如很多类型的页面、小组件、应用和图库。有了弹性盒，通常不再需要使用 CSS 框架。

## 12.1 弹性盒基础

弹性盒是一种简单而强大的布局方式，我们通过弹性盒指明空间的分布方式、内容的对齐方式和元素的视觉顺序，把不同的组件放置在页面中。内容可以轻易横向或纵向排布，还可以沿一个轴布局，或者折断成多行。

使用弹性盒，内容的呈现顺序不再受源码顺序的限制。然而，这只是视觉上的调整，弹性盒相关的属性不会改变屏幕阅读器对内容的读取顺序。

弹性盒模型布局最突出的一个特点可能是，能让元素对不同的屏幕尺寸和不同的显示设备做好适应准备。弹性盒在响应式网站中表现极好，因为内容能根据可用空间的大小增减尺寸。

弹性盒依赖父子关系。在元素上生命`display: flex`或`display: inline-flex`便激活弹性盒布局，而这个元素随之成为弹性容器（flex-container），负责在所占的空间内布置子元素，控制子元素的布局。弹性容器的子元素称为弹性元素（flex-item）

注意，div 的每个子元素都变成一个弹性元素，而且是以相同方式布局的。不管是段落还是 span 元素，都变成弹性元素（如果不把段落的外边距去掉，会有一些区别）。

上面两个弹性容器之间唯一的区别是，一个使用`display: flex`得到，另一个使用`display: inline-flex`得到。第一个 div 元素生成的是块级框，弹性元素在其中布局。而第二个 div 元素生成的是行内块级框，弹性元素在其中布局。

记住，把一个元素设为弹性容器之后，例如图 12-1 中那两个 div 元素，只有直接子元素使用弹性盒布局，其他后代元素不受影响，这一点十分重要。然而，你也可以把后代元素也设为弹性容器，实现特别复杂的布局。

在弹性容器中，各元素在主轴上排列。主轴可以是横向的，也可以是纵向的，因此可以把元素布置为列或行。主轴采用书写模式设置的方向，深入讨论见本章后面“深入理解各种轴”一节。

如图 12-1 中的第一个 div 元素所示，如果弹性元素没有占满容器的整个主轴（这里指宽子无素可以全部靠后，这些空自的具体处理方式可由几个属性控制，详情参见后文。子元素可以全部靠左、全部靠右、全部居中，也可以均匀分布，把多出的空间平均分配在子元素之间或四周。

除了均匀分布空白之外，还可以增加部分弹性元素的尺寸，把多出的空间分给一个，多个或全部弹性元素，如果容器的空间不足以放下所有弹性元素，可以通过相关属性指明缩减弹性元素的尺寸，或者允许换行。

此外，子元素可以相对容器或其他子元素对齐，可以靠容器底部对齐，可以靠容器顶部对齐，也可以在容器中居中对齐；此外还可以拉伸，占满整个容器。不管同辈元素之间的内容相差多少，使用一个声明就可以让所有同辈元素具有相同的尺寸。

### 12.1.1 一个简单的例子

在阅读本章的过程中谨记一点：弹性盒的目的是实现一种特定的布局，即一维内容分布。也就是说，弹性盒最适合沿一个方向（或轴）布置内容。虽然可以使用弹性盒实现栅格式的布局（二维布局），但这不是弹性盒的最初目的。如果需要的是二维布局，请阅读第 13 章。

## 12.2 弹性容器

首先要完全理解的概念是弹性容器，也叫容器框。`display: flex`或`display: inline-flex`声明的目标元素变成弹性容器，为其子元素生成弹性格式化上下文。

这些子元素无论是 DOM 元素、文本节点，还是生成的内容，都称为弹性元素。弹性容器中的绝对定位子元素也是弹性元素，不过确定其尺寸和位置时，将其视作弹性容器中唯一的弹性元素。

有时只有一个弹性元素，有时却有很多个。有时我们知道一个节点有多少子元素，有时子元素的数量却不在我们的掌控之中。即便知道元素的数量，可能也不知道容器的宽度。我们需要适应性强的 css,即便不知道有多少弹性元素，不知道弹性容器有多宽（比如响应式布局）,也能正确处理布局。这些问题看起来棘手，但是使用弹性盒都能轻易解决，只需使用一些新属性。

### 12.2.1 flex-direction 属性

如果你想要的布局是从上到下、从左至右、从右至左，抑或是从下到上，可以使用 flex-direction 属性控制排布弹性元素的主轴。

flex-direction
取值 row|row-reverse|column|column-reverse
初始值 row
适用于弹性容器
计算值指定的值
继承性否
动画性否

flex-direction 属性指定在弹性容器中如何摆放弹性元素，即定义弹性容器的主轴，弹性元素就沿这个轴排布（详情参见本章后面“深入理解各种轴”一节）。

### 12.2.2 其他书写方向

如果你的网站使用的是英语等从左至右书写的语言，可能希望弹性元素从左至右、从上到下排布。此时，使用默认值或者设为 row 即可。然而，如果使用的是阿拉伯语等从右至左书写的语言，可能想从右至左、从上到下排布弹性元素。此时，也是使用默认值或者设为 row 即可。

`flex-direction: row`按照文本方向（即书写模式）布置弹性元素，不管语言是从左至右书写的，还是从右至左书写的。多数网站用的是从左至右书写的语言，不过也有一些网站使用从右至左书写的语言，甚至还有的网站使用从上到下书写的语言。弹性盒定义的是单向布局。修改书写模式后，弹性盒能自动转换弹性方向。

书写模式由 writing-mode、direction 和 text-orientation 属性设定，也可以使用 HTML 的 dir 属性设置（详情参见第 6 章）。如果书写模式是从右至左，flex-direction 的值为 row 时，主轴（以及弹性容器中的弹性元素）将从右指向左，如图 12-9 所示。

世界上还有纵向书写的语言，例如汉语拼音字母、埃及象形文字、平假名、片假名、汉语、韩语、麦罗埃草书和象形文字、蒙古语、欧甘文字、古土耳其语、八思巴语、鼻语及部分日语，这些语言仅在指定纵向书写模式时才纵向排列。否则，这些语言都模向排列，如果指定纵向的书写模式，所有内容都是纵向的，不管是上面列举的某种竖写语言，还是英语。

好的，我们已经讲了弹性方向与书写模式之间的关系。但是目前所举的例子都只有一行或一列弹性元素，如果弹性元素的主维度（row 时的宽度之和，column 时的高度之和）在弹性容器中放不下将怎样呢？我们可以让放不下的元素溢出，也可以换行。后文还会说明如何缩减弹性元素的尺寸，以便放得下。

### 12.2.3 换行

如果弹性元素在弹性容器的主轴上放不下，默认情况下弹性元素不会换行，也不会自动调整尺寸。如果通过 flex 属性来设定允许弹性元素缩减尺寸，那就缩减尺寸。否则，弹性元素将从容器框的边界溢出。

这个行为受我们的控制，我们可以在容器上设置 flex-wrap 属性，允许弹性元素换行，变成多行或多列，而不让弹性元素从容器中溢出，或者缩减尺寸，挤在同一行。

flex-wrap
取值 nowrap/wrap/wrap-reverse
初始值 nowrap
适用于弹性容器
计算值指定的值
继承性否
动画性否

flex-wrap 属性的作用是限制弹性容器只能显示一行，或者允许弹性元素在必要时显示多行。允许换行时，wrap 和 wrap-reverse 决定多出的行显示在第一行之前还是之后。默认情况下，不管有多少弹性元素，全部在一行里绘制。这往往不是我们想要的效果。遇到这种情况就要请出 flex-wrap 属性了。设为 wrap 或 wrap-reverse 时，如果弹性元素超出了弹性容器的边界，将换行显示放不下的弹性元素。

一般情况下，换行时，对 row 和 row-reverse 来说垂轴从上指向下方；对 column 和 column-reverse 来说，垂轴与语言的横排方向一样。wrap-reverse 值的作用与 wrap 类似，不过额外的行添加在第一行前面，而不是后面。

设为 wrap-reverse 时，垂轴的方向相反：对 row 和 row-reverse 来说，后续的行在上方绘制：对 column 和 column-reverse 来说，后续的行在前一列的左侧绘制。类似地在从右至左书写的语言中，设为 row wrap-reverse 和 row-reverse wrap-reverse 时新行也添加到上方，但是设为 column wrap-reverse 和 column-reverse wrap-reverst 时，新行添加到右侧，即与语言的书写方向和垂轴的方向相反。

### 12.2.4 定义弹性流

flex-flow 属性用于定义主轴和垂轴的方向，以及是否允许弹性元素换行。

flex-flow
取值<flex-direction>||<flex-wrap>
初始值 row nowrap
适用于弹性容器
计算值指定的值
继承性否
动画性否

flex-flow 属性是 flex-direction 和 flex-wrap 两个属性的简写形式，用于定义弹性容器的换行方式及主轴和垂轴的方向。

把 display 属性设为 flex 或 inline-flex 后，省略 flex-flow 、 flex-direction 和 flex-wrap 相当于声明下述三个规则中的任何一个，结果如图 12-12 所示：

```css
flex-flow: row;
flex-flow: norow;
flex-flow: row nowrap;
```

在从左至右的书写模式下，声明前面给出的任何一个值，或者完全省略 flex-flow 属性，得到的弹性容器的主轴是横向的，而且不换行，图 12-12 中的弹性元素在横轴上均匀分布，而且显示在同一行，超过 500 像素宽的容器后溢出。

如果想要的是反向纵排且允许换行的弹性流，使用下述声明中的任何一个都可以：

```css
flex-flow: column-reverse wrap;
flex-flow: wrap column-reverse;
```

**深入理解各种轴**

首先，弹性元素沿主轴排布。各行弹性元素沿垂轴的方向添加。

在介绍 flex-wrap 属性之前，所有示例都只有一行弹性元素。那一行弹性元素在主轴上排布，沿主方向，从主轴起边指向主轴终边。根据所设的 flex-direction 属性，弹性元素可能并排着排布，也可能从上到下或从下到上排布，沿主轴的方向显示为一行或一列。如图 12-13 所示。

可以看出，图 12-13 中有大量术语，其中很多是新的，要说明一下。下面对各术语做个简单的定义。

- 主轴：内容沿此轴流动。在弹性盒中，指弹性元素流动的方向。
- 主轴尺寸：主轴方向上内容的总长度。
- 主轴起边：主轴上内容开始流动的那一端。
- 主轴终边：主轴上内容流向的那一端，与主轴起边相对。
- 垂轴：块级元素沿此轴堆叠。在弹性盒中，指放置新弹性元素行的方向（前提是允许换行）。
- 垂轴尺寸：垂轴方向上内容的总长度。
- 垂轴起边：垂轴上块级元素开始堆叠的那一边。
- 垂轴终边：垂轴上与起边相对的那一边。

这些要素的位置取决于弹性方向、换行方式和书写模式。图解每种书写模式有点难，下面仅以从左至右书写的语言为例。各种情况见表 12-1。

### 12.2.5 flex-wrap 续谈

默认值 nowrap 禁止换行，因此前文讨论的垂轴方向没有任何意义，毕竟根本不会出现第二行。如果可能出现额外的行（flex-wrap 设为 wrap 或 wrap-reverse 时），那些将沿垂轴方向添加。第一行放在垂轴的起边，额外的行则向垂轴终边排开。

可以看出，flex-direction 和 flex-wrap 对布局有很大的影响，而且二者之间也有不小的影响。如果想设置其中某一个属性，最好两个都设置，此时可以使用规范强烈推荐的 flex-flow 属性。

## 12.3 布置弹性元素

目前所举的例子都没有涉及每一行中弹性元素的具体位置，我们不知道如何确定弹性元素的位置。横排的弹性元素横向展开似乎是理所当然的，但是为什么所有元素都靠主轴起边一侧紧挨在一起呢？为什么不增加弹性元素的尺寸，填满全部可用空间呢？为什么不让弹性元素在一行里均匀分布呢？

## 12.4 弹性容器

在目前所举的例子中，如果弹性元素不能填满整个弹性容器，弹性元素将统一向主轴起边靠紧。不过，弹性元素也可以紧靠主轴终边，或者在弹性容器中居中，甚至可以在主轴上均匀分布。

弹性布局规范提供的一些属性能控制空间的分布情况，除了 display 和 flex-flow 之外，CSS Flexible Box Layout Module Level 1 还提供了一些能应用到弹性容器上的属性，包括 justify-content、align-content 和 align-items。

justify-content 属性控制一行里的弹性元素在主轴上如何分布。align-content 属性定义各弹性元素行在弹性容器的垂轴上如何分布。align-items 属性定义各行里的弹性元素在垂轴上如何分布。先看一行里的弹性元素是如何布置的。

## 12.5 调整内容

justify-content 属性指明在弹性容器的主轴上如何分布各行里的弹性元素。这个属性应用于弹性容器上，不能用到单个弹性元素上。

## 12.6 对齐元素

justify-content 定义弹性元素在弹性容器主轴方向上的对齐方式，而 align-items 属性定义的是弹性元素在垂轴方向上的对齐方式。与 justify-content 一样，align-items 应用在弹性容器上，而不能应用到单个弹性元素上。

使用 align-items 属性，可以把所有弹性元素都向垂轴的起边、终边或中线对齐。align-items 属性的作用与 justify-content 类似，不过影响的是垂向，设置所有弹性元素（包括匿名弹性元素）在垂轴上的对齐方式。

使用 align-items 属性，可以把所有元素都向垂轴起边或终边靠拢，也可以拉伸元素，同时靠拢起边和终边。此外，还可以把所有弹性元素都居中显示在垂向上。这个属性有五个可选值，包括 flex-start、flex-end、center、baseline 和默认的 stretch,如图 12-29 所示。

### 12.6.1 起边、缘边和居中对齐

起边、终边和剧中对齐所用的值及其效果相对简单，因此放在一起讲。

### 12.6.2 基线对齐

baseline 值有点复杂。设为 baseline 时，一行中的弹性元素向第一条基线对齐。弹性元素行中，基线与垂轴起边那一侧外边距边界之间距离最远的弹性元素，其外边距的外边界与弹性元素行垂轴起边那一侧的边对齐，其他弹性元素的基线则与那个弹性元素的基线对齐。

### 12.6.3 补充说明

如果想要改变某个或某些弹性元素的对齐方式，而不是全部修改，为响应的元素设置 align-self 属性。这个属性的取值与 align-items 一样，参见 12.9 节。

## 12.7 align-self 属性

看着有点早，但现在是讨论 align-self 属性的最佳时刻。这个属性在单个弹性元素上覆盖 align-items 属性的值。

align-items 属性在弹性容器上设置，定义弹性容器中所有弹性元素的对齐方式。但是，单个弹性元素的对齐方式可以使用 align-self 属性覆盖。align-items 的默认值是 stretch,因此在图 12-34 中的五个示例里，除第二个弹性元素之外，其他弹性元素的高度都与所在的行一样高。

对所有 align-self 属性为默认值 auto 的弹性元素来说，其对齐方式继承自容器的 align-items 属性。但是每个示例中的第二个弹性元素例外，它的 align-self 值标在每个示例的下方。

## 12.8 对齐内容

align-content 属性定义弹性容器有额外的空间时在垂轴方向上如何对齐各弹性元素行，以及空间不足以放下所有弹性元素行时从哪个方向溢出。

align-content 属性指定弹性容器中垂轴方向上的额外空间如何分配到弹性元素行之间和周围，虽然 align-content 与前面讨论的 align-items 属性在取值和相关概念上是一样的，但是二者的作用不同，后者指定的是每一行中弹性元素的定位方式。

align-content 的作用与 justify-content 类似，后者在弹性容器的主轴方向上对齐各个弹性元素，而前者在弹性容器的垂轴方向上对齐各弹性元素行。align-content 属性只适用于分为多行显示的弹性容器，对禁止换行及只有一行的弹性容器没有影响。

## 12.9 弹性元素

前面几节介绍了如何通过弹性容器的样式整体排布弹性元素。此外，弹性盒布局规范还提供了几个直接应用于弹性元素的属性。利用这些专门针对弹性元素的属性，可以更加细致地控制弹性容器中的单个子元素。

### 12.9.1 弹性元素是什么

为有子节点的元素声明`display: flex`或`display: inline-flex`即可创建弹性容器。弹性容器的子代称为弹性元素，不管是子元素，还是元素之间非空的文本节点，或是生成的内容。

对弹性容器中的文本子节点来说，如果文本节点不是空的（内容不是空白），将放在一个匿名弹性元素中，其行为与其他同辈弹性元素一样。虽然匿名弹性元素与同辈 DOM 节点一样，将继承在弹性容器上设置的相关弹性属性，但是不能直接使用 CSS 装饰。因此，不能直接在匿名弹性元素上设置针对弹性元素的属性。

### 12.9.2 弹性元素的特性

弹性元素的外边距不折叠。float 和 clear 属性对弹性元素不起作用，不会把弹性元素移出文档流。其实，应用到弹性元素的 float 和 clear 将被忽略（然而，float 属性对框体的生成仍有影响，因为 display 属性的计算值受它影响）。

**绝对定位**

我们知道 float 不会浮动弹性元素，但是`position: absolute`则不一样。如果绝对定位弹性容器的子元素，与绝对定位普通元素一样，将从文档流中移除。

除此之外，绝对定位的弹性元素不再参与弹性布局，因为它们已经不在文档流中。然而，这些元素将受应用在弹性容器上的样式影响，就像子元素受普通父元素（非弹性容器）的样式影响一样。除了可继承的属性被继承之外，应用到弹性容器上的属性可能还会影响定位原点。

绝对定位的弹性容器的子元素既受弹性容器的 justify-content 值影响，也受自身 align-self 值（如果设定了）的影响。例如，如果在绝对定位的子元素上设定`align-self: center`,元素将相对弹性容器的垂轴居中，然后再使用 top、bottom、外边距等属性移动其位置。

order 属性对弹性容器中绝对定位的子元素的位置没有影响，但是对同辈元素的绘制顺序有影响。

### 12.9.3 最小宽度

在图 12-40 中可以看到，设为默认值 nowrap 的弹性元素行从弹性容器中溢出了。这是因为对弹性元素来说，未设定 min-width 时，默认为 auto,而不是 0。最初，规范规定，如果弹性元素在唯一的主轴上放不下，其尺寸将缩减。然而，出现弹性元素后，min-width 的规范改了（以前，min-width 的默认值是 0。参见https://drafts.csswg.org/css2/visudet.html#min-max-widths）。

## 12.10 适用于弹性元素的属性

虽然弹性元素的对齐方式、顺序和弹性（flexibility）在一定程度上受在弹性容器上设置的属性控制，但是有些属性可以应用到单个弹性元素上，以便进行更细致地控制。

简写属性 flex,以及构成它的 flex-grow、flex-shrink 和 flex-basis 属性用于控制弹性元素的弹性。这里所说的弹性是指弹性元素在主轴方向上可以增加或缩减多少尺寸。

## 12.11 flex 属性

弹性布局最突出的一点是能把弹性元素变得具有“弹性”，即在主轴方向上调整弹性元素的宽度或高度，占满可用空间。弹性容器根据弹性增长因子（flex grow factor）按比例分配额外的空间，或者根据弹性缩减因子（flex shrink factor）按比例缩小弹性元素，以防溢出（稍后探讨这些概念）。

增长因子和缩减因子由弹性元素的 flex 简写属性声明，或者由构成简写属性的单个属性定义。如果空间过多，可以增加弹性元素的尺寸，占满多出的空间。当然也可以不这如果指定的尺寸或默认的尺寸导致弹性元素在弹性容器中放不下，可以按比例缩减以便放得下。当然，此时也可以不这么做。

这一切都由 flex 属性控制，它是 flex-grow、flex-shrink 和 flex-basis 的简写形然三个子属性可以单独使用，但是强烈建议始终使用简写的 flex,原因稍后说明。

## 12.12 flex-grow 属性

flex-grow 属性定义有多余的空间时是否允许弹性元素增大，以及允许增大且有多余的空间时，相对其他同辈弹性元素以什么比例增大。

### 12.12.1 在 flex 属性中设定增长因子

flex 属性有三个值：增长因子，缩减因子和基准。第一个有效的正数设定的是增长因子（即 flex-grow 的值）。如果 flex 属性没有设定增长因子和缩减因子，增长因子默认为 1。然而，如果 flex 和 flex-grow 都没有声明，增长因子默认为 0。是的，你没看错。

## 12.13 flex-shrink 属性

flex 简写属性的`<flex-shrink>`部分指定弹性缩减因子。缩减因子也可以通过 flex-shrink 属性设定。

### 12.13.1 根据宽度和缩减因子按比例缩小

上述示例比较简单，因为各弹性元素的宽度一开始是相同的。如果宽度不等呢？如果第一个和最后一个弹性元素的宽度为 250 像素，而中间那个弹性元素的宽度为 500 像素呢？如图 12-48 所示。

### 12.13.2 不同的基准

如果宽度和弹性基准的值都是 auto，缩减因子为零时，弹性元素中的内容不换行。这与所想的有点出入。其实，缩减因子为任何正数都会导致内容换行。由于缩小的量是与缩减因子成比例的，如果所有弹性元素的缩减因子差不多，内容换行的次数也差不多。

### 12.13.3 响应式弹性布局

利用这种按比例缩小弹性元素尺寸的行为可以实现响应式布局。

## 12.14 flex-basis 属性

我们知道，弹性元素的尺寸受内容及盒模型属性的影响，而且可以通过 flex 属性的三个要素重置。flex 属性中的`<flex-basis>`要素定义弹性元素的初始或默认尺寸，即根据增长因子和缩减因子分配多余或缺少的空间之前，弹性元素的大小。这个要素也可以使用 flex-basis 属性设定。

### 12.14.1 content 关键字

### 12.14.2 自动确定弹性基准

设为 auto 时，不管是显式声明的还是取默认值，flex-basis 等于元素在主轴方向上的尺寸，就像没把元素变成弹性元素一样。如果 width 或 height 的值是长度，弹性基准就等于那个长度，而如果 width 或 height 也是 auto，那么弹性基准回落为 content。

### 12.14.3 默认值

### 12.14.4 长度单位

### 12.14.5 零基准

## 12.15 flex 简写属性

至此，我们对 flex 简写属性的各要素做了全面的了解。记住，始终使用 flex 简写属性。这个属性接受常规的全局属性值，包括 initial、auto 和 none;只要是整数，通常为 1,就表示弹性元素可以增大。下面简要说明一下。

**常见的弹性值**

常见的弹性值有四个，涵盖了最常需要的效果：

1. `flex: initial` 这个值根据 width 或 height 属性（由主轴方向决定）确定弹性元素的尺寸，而且允许缩小。
2. `flex: auto` 这个值也根据 width 或 height 属性确定弹性元素的尺寸，但是元素是完全弹性的，既可以缩小也可以增大。
3. `flex: none` 这个值还是据 width 或 height 属性确定弹性元素的尺寸，但是元素完全没有弹性，不能缩小也不能增大。
4. `flex: <number>` 这个值把弹性元素的增长因子设为`<number>`指定的数，同时把缩减因子设为 0,把基准也设为 0。这意味着，width 或 height 属性的值相当于最小尺寸，弹性元素在有多余的空间时将增大。

**initial 值**

initial 是 CSS 中的全局关键字，任何属性都能使用这个关键字表示属性的初始值，即规范定义的默认值。因此，下面两个声明是等效的：

```
flex: initial;
flex: 0 1 auto;
```

**auto 值**

`flex: auto`的效果与`flex: initial`类似，不过弹性元素的弹性变形是双向的：如果容器的空间放不下全部弹性元素，元素将缩小；如果有额外的空间，弹性元素将增大。主轴方向上的任何多余空间都能分给弹性元素。下面两个声明是等效的：

```
flex: auto;
fle: 1 1 auto;
```

**使用 none 禁止弹性变形**

声明了`flex: none`的弹性元素不具有弹性。下面两个 CSS 声明是等效的：

```
flex: none;
flex: 0 0 auto;
```

**数字值**

如果 flex 属性只有一个值，而且是正数，那个值将用作增长因子，而缩减因子默认为 0，基准也默认为 0.下面两个 CSS 声明是等效的：

```
flex: 3;
flex: 3 0 3;
```

## 12.16 order 属性

默认情况下，弹性元素的显示和排布顺序与在源码中的顺序一致。弹性元素和弹性元素行的顺序可以使用 flex-direction 属性反转，但是有时你可能需要更细致的重排方式。order 属性用于修改单个弹性元素的显示顺序。

默认情况下，所有弹性元素的顺序都是 0,归在同一个排序组中，以出现在源码中的顺序沿主轴方向显示（本章目前所举的例子都是如此）。

若想修改弹性元素的视觉顺序，把 order 属性设为一个非零整数。如果 order 属性的目标元素不是弹性容器的子元素，元素不受影响。

order 属性的值指定一个排序组，把目标弹性元素归在其中。在页面中绘制弹性元素时，order 属性为负数的弹性元素显示在采用默认值 0 的弹性元素前面，而 order 属性为正数的弹性元素显示在采用默认值 0 的弹性元素后面。虽然弹性元素的视觉顺序变了，但是在源码中的顺序没变。屏幕阅读器的阅读顺序和 Tab 键的索引顺序都由 HTML 源码顺序定义。

# 第 13 章 网格布局

css 出现这些年来（你可能不信，已经 20 年了）,布局一直是其最为重要的功能。我们已经讨论过其他布局方式，例如 float 和 clear,不过这并不是它们的恰当用法。弹性盒布局填补了一些空白，但只适用于特定的情况，例如导航栏

与之相比，栅格布局是普适的布局系统。由于栅格布局依赖行和列，初一看似乎倒退到表格布局了（在某些方面二者之间的差异并不明显）,但是栅格布局比表格布局强大得多得多，使用栅格设计布局，无需顾虑各部分在源文档中的顺序，如果愿意，不同的部分还可以重叠在一起。有很多灵活的方法能为栅格线定义重复模式，以及把元素依附到栅格线上等。栅格之内可以联套栅格，而且还可以在栅格中使用表格或弹性容器。这只是举些例子，栅格布局的功能还有很多很多。

总之，栅格布局是我们翘首以盼的布局系统。要学的东西很多，要抛诸脑后的东西可能更多，是时候告别过去 20 年自作聪明的小技巧和变通方法了。

## 13.1 创建栅格容器

创建栅格的第一步是定义栅格容器（grid container)。这与定位所用的容纳块和弹性盒布局中的弹性容器的作用很像：栅格容器为其中的内容定义一个栅格格式化上下文（grid formatting context).

从这一点上看，栅格布局从弹性盒布局上沿袭了相当多的概念。例如，栅格容器的子元素是栅格元素（grid item),就像弹性容器的子元素是弹性元素一样。子元素的子元素不是栅格元素，不过栅格元素自身也可以变作栅格容器，因此它的子元素将变成嵌套栅格的栅格元素。栅格之中可以酸套栅格，而且层级不限（栅格布局还有子栅格这个概念，它与嵌套的栅格容器不是一回事，稍后讨论）。

栅格有两种：常规栅格和行内栅格。这两种栅格使用 display 属性的特殊值创建：grid 和 inline-grid,前者生成块级框，后者生成行内框。二者之间的区别如图 13-1 所示。

<!-- <Figures figure="13-1">Grids and inline grids</Figures> -->

这与 display 属性的 block 和 inline-block 值十分相似。多数栅格都是块级的，不过你要知道也有创建行内栅格这一选择。

虽然`display: grid`创建的是块级栅格，但是严谨的规范明确指出，“栅格容器不是块级容器”，意思就是，栅格框在布局中的行为与块级容器很像，但是二者之间仍有诸多区别。

首先，浮动的元素不会打乱栅格容器，这意味着，栅格不会移到浮动元素的下方，而块级容器会。这一差异如图 13-2 所示。

<!-- <Figures figure="13-2">Floats interact differently with blocks and grids</Figures> -->

其次，栅格容器的外边距不与其后代的外边距折叠。而块级框的外边距（默认）与其后代的外边距折叠，这是栅格容器与块级框的又一区别，例如，有序列表的第一个列表项日可能有上外边距，但这个外边距将与列表元素的上外边距折叠。然而，栅格元素的上外边距绝不会与栅格容器的上外边距折叠。这一差异如图 13-3 所示。

<!-- <Figures figure="13-3">Margin collapsing and the lack thereof</Figures> -->

有些 CSS 属性和功能不能用在栅格容器和栅格元素上，如下：

- 栅格容器上的所有 column 属性（例如 column-count、columns 等）都被忽略。
- 栅格容器没有`::first-line`和`::first-letter`伪元素，如果使用，将被忽略。
- 栅格元素（而非栅格容器）上的 float 和 clear 属性将被忽略。尽管如此，float 属性对栅格容器中子元素的 display 属性的计算值是有影响的，因为栅格元素的 display 值在变成栅格元素之前计算。
- vertical-align 属性对想格元素不起作用，不过可能会影响栅格元素中的内容（别担心，对齐栅格元素有其他更强大的方式）。

最后，如果为栅格容器声明的 display 值是 inline-grid,而目标元素是浮动的或绝对定位的，那么 display 的计算值将变为 grid(取代 inline-grid)。

定义好栅格容器后，接下来要在容器中设置栅格。讨论具体方式之前，有必要说明几个术语。

## 13.2 基本的栅格术语

前面已经讨论过栅格容器和栅格元素，下面为其做个更准确的定义。如前所述，栅格容器是确立栅格格式化上下文的框体，即定义一个栅格区域，其中的元素根据栅格布局（而非块级布局）规则排布。这一点可以与通过`display: table`创建表格格式化上下文类比。表格自身就是一种栅格系统，因此这样类比还是相当合适的，但是不要以为栅格只是另一种形式的表格。栅格比表格强大得多。

栅格元素是在栅格格式化上下文中参与栅格布局的东西。这通常是栅格容器的子元素，但也可以是元素内容中的匿名文本（即不在元素中的文本）。来看下述代码，得到的结果如图 13-4 所示：

```css
#warning {
  display: grid;
  background: #fcc;
  padding: 0.5em;
  grid-template-rows: 1fr;
  grid-template-columns: repeat(7, 1fr);
}
```

```html
<p id="warning">
  <img src="warning.svg" /><strong>Note:</strong> This element is a
  <em>grid container</em> with several <em>grid items</em> inside it.
</p>
```

<!-- <Figures figure="13-4">Grid items</Figures> -->

注意，各元素及元素之间的文本都变成栅格元素了。图像是栅格元素，其他元素和文本块也是栅格元素，一共有 7 个。这些栅格元素都参与栅格布局，然而匿名文本块难以（或无法）使用下文将讨论的栅格属性控制。

在使用栅格属性的过程中，可能会创建或引用栅格布局的多个核心组件，如图 13-5 所示。

<!-- <Figures figure="13-5">Grid components</Figures> -->

最重要的组件是栅格线。栅格线的位置定义好之后，其他栅格组件也就随之而现了：

- 横格轨道（grid track）指两条相邻的栅格线之间夹住的整个区域，从栅格容器的一边延伸到对边，即栅格列或栅格行。栅格轨道的尺寸由栅格线的位置决定。可以对比表格中的列和行理解。用适用性更广的语言来说，可以称之为块级轴和行内轴轨道，（对西方语言来说）列轨道在块级轴上，行轨道在行内轴上。
- 栅格单元（grid cell）指四条栅格线限定的区域，内部没有其他栅格线贯穿，类似于单元格。这是横格布局中区域的最小单位。栅格单元不能直接使用 CSS 栅格属性处理，即没有属性能把一个栅格元素放在指定的栅格单元里（详情参见下一点）。
- 栅格区域（grid area）指任何四条栅格线限定的矩形区域，由一个或多个栅格单元构成。最小的栅格区域是一个栅格单元，最大的栅格区域是栅格中所有的栅格单元。栅格区域能使用 CSS 栅格属性直接处理，定义好栅格区域后即可在其中放置栅格元素。

特别注意，栅格轨道、栅格单元和栅格区域都完全由栅格线建构，不一定非要有相应的栅格元素存在。栅格区域中不一定充满栅格元素，完全可以让部分甚至多数栅格单元空着。此外，栅格元素还可以重叠，方法是定义重叠的栅格区域，或者把栅格线重叠起来。

另外要注意的一点是，栅格线的数量不限，想定义多少就可以定义多少。你可以只定义一系列纵向的栅格线，创建一行多列布局。你也可以反过来，创建多个行轨道但不创建列轨道（当然还是会有一个列轨道，从栅格容器的一边延伸到对边）。

然而，如果栅格元素无法放入你定义的列或行轨道中，或者你明确指定把栅格元素放在轨道的外部，那么栅格系统将自动添加栅格线和轨道。

## 13.3 放置栅格线

It turns out that placing grid lines can get fairly complex. That’s not so much because the concept is difficult; there are just so many different ways to get it done, and each uses its own subtly different syntax.

> 事实证明，放置网格线会变得相当复杂。这并不是因为这个概念很难;有许多不同的方法可以完成它，每种方法都使用自己的语法。

We’ll get started by looking at two closely related properties.

> 我们将从两个密切相关的属性开始。

<!-- <Cards cards="grid-template-rows_grid-template-columns" /> -->

With these properties, you can define the grid lines in your overall grid template, or what the CSS specification calls the `explicit grid`. Everything depends on these grid lines; fail to place them properly, and the whole layout can very easily fall apart.

> 使用这些属性，您可以在整个网格模板中定义网格线，或者 CSS 规范所称的“显式网格”。一切都取决于这些网格线;如果放置不当，整个布局就会很容易崩溃。

<Tips tips="blue">When you’re starting out with CSS grid layout, it’s probably a very good idea to sketch out where the grid lines need to be on paper first, or in some close digital analogue. Having a visual reference for where lines should be, and how they should behave, will make writing your grid CSS a lot easier.</Tips>

The exact syntax patterns for `<track-list>` and `<auto-track-list>` are complex and nest a few layers deep, and unpacking them would take a lot of time and space that’s better devoted to just exploring how things work. There are a lot of ways to specify your grid lines’ placement, so before we get started on learning those patterns, there are some basic things to establish.

> `<track-list>` 和 `<auto-track-list>` 的确切语法模式很复杂，并且嵌套了几层，将它们拆解将花费大量的时间和空间，最好将这些时间和空间用于探索事物是如何工作的。有很多方法可以指定网格线的位置，所以在我们开始学习这些模式之前，需要建立一些基本的东西。

First, grid lines can always be referred to by number, and can also be named by the author. Take the grid shown in Figure 13-6, for example. From your CSS, you can use any of the numbers to refer to a grid line, or you can use the defined names, or you can mix them together. Thus, you could say that a grid item stretches from column line `3` to line `steve`, and from row line `skylight` to line `2`.

> 首先，网格线总是可以通过编号来引用，也可以由作者来命名。以图 13-6 所示的网格为例。在 CSS 中，可以使用任何数字来引用网格线，也可以使用定义的名称，或者将它们混合在一起。因此，您可以说一个网格项从列' 3 '延伸到行' steve '，从行' skylight '延伸到行' 2 '。

Note that a grid line can have more than one name. You can use any of them to refer to a given grid line, though you can’t combine them the way you can multiple class names. You might think that means it’s a good idea to avoid repeating grid-line names, but that’s not always the case, as we’ll soon see.

> 请注意，网格线可以有多个名称。您可以使用它们中的任何一个来引用给定的网格线，尽管您不能像组合多个类名那样组合它们。您可能认为这意味着避免重复网格线名称是一个好主意，但情况并不总是如此，我们很快就会看到。

<Figures figure="13-6">Grid-line numbers and names</Figures>

I used intentionally silly grid-line names in Figure 13-6 to illustrate that you can pick any name you like, and also to avoid the implication that there are “default” names. If you’d seen `start` for the first line, you might have assumed that the first line is always called that. Nope. If you want to stretch an element from `start` to `end`, you’ll need to define those names yourself. Fortunately, that’s simple to do.

> 我在图 13-6 中故意使用了一些愚蠢的网格线名称来说明您可以选择任何喜欢的名称，同时也避免了“默认”名称的含义。如果您看到第一行的“start”，您可能会认为第一行总是被称为“start”。不。如果您想将一个元素从' start '扩展到' end '，您需要自己定义这些名称。幸运的是，这很容易做到。

As I’ve said, many value patterns can be used to define the grid template. We’ll start with the simpler ones and work our way toward the more complex.

> 如前所述，可以使用许多值模式来定义网格模板。我们将从简单的开始，然后逐步向复杂的方向发展。

### 13.3.1 宽度固定的栅格轨道

Our first step is to create a grid whose grid tracks are a fixed width. We don’t necessarily mean a fixed length like pixels or ems; percentages also count as fixed-width here. In this context, “fixed-width” means the grid lines are placed such that the distance between them does not change due to changes of content within the grid tracks.

> 我们的第一步是创建一个网格，其网格轨迹的宽度是固定的。我们不需要像像素或 ems 那样的固定长度;百分比在这里也算作固定宽度。在这种情况下，“固定宽度”是指网格线的位置，使它们之间的距离不会因为网格轨道内内容的变化而改变。

So, as an example, this counts as a definition of three fixed-width grid columns:

> 因此，作为一个例子，这可以看作是三个固定宽度的网格列的定义:

```css
#grid {
  display: grid;
  grid-template-columns: 200px 50% 100px;
}
```

That will place a line 200 pixels from the start of the grid container (by default, the left side); a second grid line half the width of the grid container away from the first; and a third line 100 pixels away from the second. This is illustrated in Figure 13-7.

> 它将从网格容器的开始位置开始放置 200 像素的行(默认情况下是左侧);第二网格线距第一网格容器宽度的一半;第三行距离第二行 100 像素。如图 13-7 所示。

<Figures figure="13-7">Grid-line placement</Figures>

While it’s true that the second column can change in size if the grid container’s size changes, it will `not` change based on the content of the grid items. However wide or narrow the content placed in that second column, the column’s width will always be half the width of the grid container.

> 虽然如果网格容器的大小发生变化，第二列的大小也会发生变化，但是它不会根据网格项的内容发生变化。无论第二列中的内容有多宽或多窄，列的宽度总是网格容器宽度的一半。

It’s also true that the last grid line doesn’t reach the right edge of the grid container. That’s fine; it doesn’t have to. If you want it to—and you probably will—we’ll see vari‐ ous ways to deal with that in just a bit.

> 最后一条网格线没有到达网格容器的右边缘也是事实。这很好;不需要。如果你想这样做——你可能会这样做——我们很快就会看到各种各样的方法来解决这个问题。

This is all lovely, but what if you want to name your grid lines? Just place any gridline name you want, and as many as you want, in the appropriate place in the value, surrounded by square brackets. That’s all! Let’s add some names to our previous example, with the result shown in Figure 13-8:

> 这些都很好，但是如果你想给网格线命名呢?只需将您想要的任何 gridline 名称，以及您想要的任意多的 gridline 名称，放置在值中由方括号包围的适当位置。这是所有!让我们在前面的示例中添加一些名称，结果如图 13-8 所示:

```css
#grid {
  display: grid;
  grid-template-columns: [start col-a] 200px [col-b] 50% [col-c] 100px [stop end last];
}
```

<Figures figure="13-8">Grid-line name</Figures>

What’s nice is that adding the names makes clear that each value is actually specifying a grid track’s width, which means there is always a grid line to either side of a width value. Thus, for the three widths we have, there are actually four grid lines created. Row grid lines are placed in exactly the same way as columns, as Figure 13-9 shows:

> 添加名称的好处是，可以清楚地看到每个值实际上指定了网格轨道的宽度，这意味着在宽度值的两侧始终有一条网格线。因此，对于我们所拥有的三个宽度，实际上创建了四条网格线。行网格线与列的放置方式完全相同，如图 13-9 所示:

```css
#grid {
  display: grid;
  grid-template-columns: [start col-a] 200px [col-b] 50% [col-c] 100px [stop end last];
  grid-template-rows: [start masthead] 3em [content] 80% [footer] 2em [stop end];
}
```

<Figures figure="13-9">Creating a grid</Figures>

There are a couple of things to point out here. First, there are both column and row lines with the names `start` and `end`. This is perfectly OK. Rows and columns don’t share the same namespace, so you can reuse names like these in the two contexts.

> 这里有几点需要指出。首先，有“开始”和“结束”名称的行和列。这完全没问题。行和列不共享相同的名称空间，因此可以在这两个上下文中重用这样的名称。

Second is the percentage value for the `content` row track. This is calculated with respect to the height of the grid container; thus, a container 500 pixels tall would yield a `content` row that’s 400 pixels tall. This requires that you know ahead of time how tall the grid container will be, which won’t always be the case.

> 第二个是“content”行轨道的百分比值。这是根据网格容器的高度计算的;因此，一个 500 像素高的容器将产生 400 像素高的“内容”行。这要求您提前知道网格容器的高度，但实际情况并非总是如此。

You might think we could just say `100%` and have it fill out the space, but that doesn’t work, as Figure 13-10 illustrates: the `content` row track will be as tall as the grid container itself, thus pushing the `footer` row track out of the container altogether:

> 您可能认为我们可以只说' 100% '，并让它填充空间，但这并不工作，如图 13-10 所示:' content '行轨道将与网格容器本身一样高，从而将' footer '行轨道完全挤出容器:

```css
#grid {
  display: grid;
  grid-template-columns: [start col-a] 200px [col-b] 50% [col-c] 100px [stop end last];
  grid-template-rows: [start masthead] 3em [content] 100% [footer] 2em [stop end];
}
```

<Figures figure="13-10">Exceeding the grid container</Figures>

One way (not necessarily the best way) to handle this scenario is to `minmax` the row’s value, telling the browser that you want the row no shorter than one amount and no taller than another, leaving the browser to fill in the exact value. This is done with the `minmax(a,b)` pattern, where `a` is the minimum size and `b` is the maximum size:

> 处理这种情况的一种方法(不一定是最好的方法)是“minmax”行值，告诉浏览器您希望行不小于一个值，也不高于另一个值，让浏览器填写准确的值。这是通过“minmax(a,b)”模式完成的，其中“a”是最小尺寸，“b”是最大尺寸:

```css
#grid {
  display: grid;
  grid-template-columns: [start col-a] 200px [col-b] 50% [col-c] 100px [stop end last];
  grid-template-rows:
    [start masthead] 3em [content] minmax(3em, 100%)
    [footer] 2em [stop end];
}
```

What we’ve said there is to make the `content` row never shorter than 3 ems tall, and never taller than the grid container itself. This allows the browser to bring up the size until it’s tall enough to fit the space left over from the `masthead` and `footer` tracks, and no more. It also allows the browser to make it shorter than that, as long as it’s not shorter than `3em`, so this is not a guaranteed result. Figure 13-11 shows one possible outcome of this approach.

> 我们所说的是让“content”行不低于 3ems 高，也不高于网格容器本身。这允许浏览器调出大小，直到它足够高，以适应“报头”和“页脚”轨道留下的空间，仅此而已。它还允许浏览器使它更短，只要它不短于' 3em '，所以这不是一个保证的结果。图 13-11 显示了这种方法的一个可能结果。

<Figures figure="13-11">Adapting to the grid container</Figures>

In like fashion, with the same caveats, `minmax()` could have been used to help the `col-b` column fill out the space across the grid container. The thing to remember with `minmax()` is that if the `max` is smaller than the `min`, then the `max` value is thrown out and the `min` value is used as a fixed-width track length. Thus, `minmax(100px, 2em)` would resolve to `100px` for any font-size value smaller than `50px`.

> 以类似的方式，使用相同的警告，“minmax()”可以用来帮助“col-b”列填充网格容器中的空间。' minmax() '需要记住的是，如果' max '小于' min '，那么' max '值将被抛出，' min '值将用作固定宽度的磁道长度。因此，' minmax(100px, 2em) '将解析为' 100px '对于任何小于' 50px '的字体大小值。

If the vagueness of `minmax()`’s behavior unsettles you, there are alternatives to this scenario. We could also have used the `calc()` value pattern to come up with a track’s height (or width). For example:

> 如果“minmax()”行为的模糊性让您感到不安，那么可以使用其他替代方案。我们也可以使用' calc() '值模式来得到轨道的高度(或宽度)。例如:

```css
grid-template-rows:
  [start masthead] 3em [content] calc(100%-5em)
  [footer] 2em [stop end];
```

That would yield a `content` row exactly as tall as the grid container minus the sum of the `masthead` and `footer` heights, as we saw in the previous figure.

> 这将生成与网格容器一样高的' content '行，减去' masthead '和' footer '的高度之和，就像我们在前面的图中看到的那样。

That works as far as it goes, but is a somewhat fragile solution, since any changes to the `masthead` or `footer` heights will also require an adjustment of the calculation. It also becomes a lot more difficult (or impossible) if you want more than one column to flex in this fashion. As it happens, there are much more robust ways to deal with this sort of situation, as we’ll soon see.

> 目前为止，这是可行的，但这是一个有点脆弱的解决方案，因为任何改变“报头”或“页脚”的高度也需要调整计算。如果您希望以这种方式伸缩多个列，那么它也会变得更加困难(或者不可能)。实际上，我们很快就会看到，有很多更有效的方法来处理这种情况。

### 13.3.2 弹性栅格轨道

Thus far, all our grid tracks have been `inflexible`—their size determined by a length measure or the grid container’s dimensions, but unaffected by any other considerations. `Flexible` grid tracks, by contrast, can be based on the amount of space in the grid container not consumed by inflexible tracks, or alternatively, can be based on the actual content of the entire track.

> 到目前为止，我们所有的网格轨道都是“不灵活的”——它们的大小由长度度量或网格容器的尺寸决定，但是不受任何其他考虑的影响。相比之下，“灵活的”网格轨道可以基于网格容器中不被灵活轨道占用的空间量，也可以基于整个轨道的实际内容。

#### Fractional units

If you want to divide up whatever space is available by some fraction and distribute the fractions to various columns, the `fr` unit is here for you.

> 如果你想把任何可用的空间除以某个分数，并把分数分配到不同的列，“fr”单位就在这里。

In the simplest case, you can divide up the whole container by equal fractions. For example, if you want four columns, you could say:

> 在最简单的情况下，你可以把整个容器除以相等的分数。例如，如果你想要四列，你可以说:

```css
grid-template-columns: 1fr 1fr 1fr 1fr;
```

In this very limited case, that’s equivalent to saying:

> 在这种非常有限的情况下，这相当于说:

```css
grid-template-columns: 25% 25% 25% 25%;
```

The result either way is shown in Figure 13-12.

> 两种方法的结果如图 13-12 所示。

<Figures figure="13-12">Dividing the container into four columns</Figures>

Now suppose we want to add a fifth column, and redistribute the column size so they’re all still equal. With percentages, we’d have to rewrite the entire value to be five instances of `20%`. With `fr`, though, we can just add another `1fr` to the value and have everything done for us automatically:

> 现在假设我们要添加第五列，重新分配列的大小，使它们仍然相等。对于百分比，我们必须将整个值重写为 5 个“20%”实例。不过，有了“fr”，我们可以只添加另一个“1fr”的价值，并有一切为我们自动:

```css
grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
```

The way `fr` units work is that all of the `fr` values are added together, with the available space divided by that total. Then each track gets the number of those fractions indicated by its number.

> “fr”单元的工作方式是将所有“fr”值加在一起，用可用空间除以总数。然后每条轨迹得到由它的数量表示的分数的数量。

What that meant for the first of the previous examples is that when there were four `fr` values, their numbers were added together to get a total of four. The available space was thus divided by four, and each column got one of those fourths. When we added a fifth `1fr`, the space was divided by five, and each column got one of those fifths.

> 对于前面的第一个示例，这意味着当有四个“fr”值时，将它们的数字相加得到四个值。可用空间因此被除以 4，每一列得到四分之一。当我们添加第五个 1fr 时，空间被 5 除去，每一列都是 5 分之 1。

You are not required to always use `1` with your `fr` units! Suppose you want to divide up a space such that there are three columns, with the middle column twice as wide as the other two. That would look like this:

> 你不需要总是使用' 1 '与你的' fr '单位!假设你想把一个空间分成三列，中间一列的宽度是其他两列的两倍。它是这样的:

```css
grid-template-columns: 1fr 2fr 1fr;
```

Again, these are added up and then 1 is divided by that total, so the base `fr` in this case is `0.25`. The first and third tracks are thus 25% the width of the container, whereas the middle column is half the container’s width, because it’s `2fr`, which is twice `0.25`, or `0.5`.

> 同样地，这些加起来，然后 1 除以总数，所以在这种情况下底数 fr 是 0。25。因此，第一个和第三个轨道是容器宽度的 25%，而中间一列是容器宽度的一半，因为它是' 2fr '，是' 0.25 '或' 0.5 '的两倍。

You aren’t limited to integers, either. A recipe card for apple pie could be laid out using these columns:

> 你也不局限于整数。苹果派的食谱卡可以用以下这些列出来:

```css
grid-template-columns: 1fr 3.14159fr 1fr;
```

I’ll leave the math on that one as an exercise for the reader. (Lucky you! Just remember to start with `1 + 3.14159 + 1`, and you’ll have a good head start.)

> 我把那个问题留给读者作为练习。(你真幸运!只要记住从“1 + 3.14159 + 1”开始，你就会有一个好的开始。

This is a convenient way to slice up a container, but there’s more here than just replacing percentages with something more intuitive. Fractional units really come into their own when there are some fixed columns and some flexible space. Consider, for example, the following, which is illustrated in Figure 13-13:

> 这是分割容器的一种方便的方法，但是这里不仅仅是用更直观的东西替换百分比。当有一些固定的列和一些灵活的空间时，分数单位才真正发挥作用。例如，考虑如下图 13-13 所示:

```css
grid-template-columns: 15em 1fr 10%;
```

<Figures figure="13-13">Giving the center column whatever’s available</Figures>

What happened there is the browser assigned the first and third tracks to their inflexible widths, and then gave whatever was left in the grid container to the center track. This means that for a 1,000-pixel-wide grid container whose `font-size` is the usual browser default of `16px`, the first column will be 240 pixels wide and the third will be 100 pixels wide. That totals 340 pixels, leaving 660 pixels that weren’t assigned to the fixed tracks. The fractional units total one, so 660 is divided by one, yielding 660 pixels, all of which are given to the single `1fr` track. If the grid container’s width is increased to 1,400 pixels, the third column will be 140 pixels wide and the center column 1,020 pixels wide.

> 这里的情况是，浏览器将第一个和第三个轨道分配到它们的固定宽度，然后将网格容器中剩下的所有内容分配给中心轨道。这意味着对于一个 1,000 像素宽的网格容器，它的“字体大小”通常是浏览器默认的“16px”，第一列将是 240 像素宽，第三列将是 100 像素宽。总计 340 像素，剩下 660 像素没有分配到固定轨道。分数单位总数为 1，所以 660 除以 1，得到 660 个像素，所有这些都被分配给单一的“1fr”轨道。如果将网格容器的宽度增加到 1400 像素，则第三列宽 140 像素，中间列宽 1020 像素。

Just like that, we have a mixture of fixed and flexible columns. We can keep this going, splitting up any flexible space into as many fractions as we like. Consider this:

> 就像这样，我们有一个固定和灵活的列的混合物。我们可以继续这样做，把任意的弹性空间分割成任意多的分数。考虑一下:

```css
width: 100em;
grid-template-columns: 15em 4.5fr 3fr 10%;
```

In this case, the columns will be sized as shown in Figure 13-14.

<Figures figure="13-14">Flexible column sizing</Figures>

The widths of the columns will be, from left to right: `15em`, `45em`, `30em`, and `10em`. The first column gets its fixed width of `15em`. The last column is `10%` of 100 em, which is 10 em. That leaves 75 em to distribute among the flexible columns. The two added together total 7.5 fr. For the wider column, 4.5 ÷ 7.5 equals 0.6, and that times 75 em equals 45 em. Similarly, 3 ÷ 7.5 = 0.4, and that times 75 em equals 30 em.

> 各柱的宽度从左至右为:' 15em '， ' 45em '， ' 30em '， ' 10em '。第一列的宽度固定为' 15em '。最后一列是 100 em 的“10%”，即 10 em，剩下 75 em 分布在灵活的列中。两者加起来是 7.5 fr。对于更宽的列，4.5÷7.5 = 0.6，乘以 75 em 等于 45 em，同样，3÷7.5 = 0.4，乘以 75 em 等于 30 em。

Yes, admittedly, I put a thumb on the scales for that example: the `fr` total and `width` value were engineered to yield nice, round numbers for the various columns. This was done purely to aid understanding. If you want to work through the process with less tidy numbers, consider using `92.5em` or `1234px` for the `width` value in the previous example.

> 是的，无可否认，我把一个拇指放在秤上的例子:“fr”的总和“宽度”的价值是工程，以产生漂亮的，各种列的整数。这样做纯粹是为了帮助理解。如果您希望使用不太整齐的数字来完成这个过程，可以考虑在前面的示例中使用' 92.5em '或' 1234px '作为' width '值。

In cases where you want to define a minimum or maximum size for a given track, `minxmax()` can be quite useful. To extend the previous example, suppose the third column should never be less than `5em` wide, no matter what. The CSS would then be:

> 在需要为给定音轨定义最小或最大大小的情况下，' minxmax() '可能非常有用。为了扩展前面的示例，假设第三列的宽度永远不应小于' 5em '，无论如何。CSS 将是:

```css
grid-template-columns: 15em 4.5fr minmax(5em, 3fr) 10%;
```

Now the layout will have two flexible columns at its middle, down to the point that the third column reaches `5em` wide. Below that point, the layout will have three inflexible columns (`15em`, `5em`, and `10%` wide, respectively) and a single flexible column that will get all the leftover space, if there is any. Once you run the math, it turns out that up to `30.5556em` wide, the grid will have one flexible column. Above that width, there will be two such columns.

> 现在布局将在中间有两个灵活的列，直到第三列达到' 5em '宽。在这一点以下，布局将有三个不灵活的列(分别为' 15em '、' 5em '和' 10% '宽)和一个灵活的列(如果有剩余空间的话)。一旦您运行数学运算，结果是在' 30.5556em '宽的范围内，网格将有一个灵活的列。在这个宽度之上，将有两个这样的列。

You might think that this works the other way—for example, if you wanted to make a column track flexible up to a certain point, and then become fixed after, you would declare a minimum `fr` value. This won’t work, sadly, because `fr` units are not allowed in the `min` position of a `minmax()` expression. So any `fr` value provided as a minimum will invalidate the declaration.

> 您可能认为这是另一种工作方式-例如，如果您想使一个列跟踪灵活到某个特定的点，然后成为固定后，你会声明一个最小' fr '值。遗憾的是，这将不起作用，因为“fr”单元不允许在“minmax()”表达式的“min”位置。因此，任何最低“fr”值将使声明无效。

Speaking of setting to zero, let’s look at a situation where the minimum value is explicitly set to `0`, like this:

> 说到设置为 0，让我们看看最小值被显式设置为' 0 '的情况，就像这样:

```css
grid-template-columns: 15em 1fr minmax(0, 500px) 10%;
```

Figure 13-15 illustrates the narrowest grid width at which the third column can remain 500 pixels wide. Any narrower, and the minmaxed column will be narrower than 500 pixels. Any wider, and the second column, the `fr` column, will grow beyond zero width while the third column stays at 500 pixels wide.

> 图 13-15 显示了第三列保持 500 像素宽的最窄网格宽度。任何变窄，则最小的列将小于 500 像素。再宽一点，第二列，也就是“fr”列的宽度就会超过零，而第三列的宽度会保持在 500 像素。

<Figures figure="13-15">Minmaxed column sizing</Figures>

If you look closely, you’ll see the `1fr` label next to the boundary between the `15em` and `minmax(0,500px)` columns. That’s there because the `1fr` is placed with its left edge on the second column grid line, and has no width, because there is no space left to flex. Similarly, the `minmax` is placed on the third column grid line. It’s just that, in this specific situation, the second and third column grid lines are in the same place (which is why the `1fr` column has zero width).

> 如果你仔细看，你会看到“1fr”标签在“15em”和“minmax(0,500px)”栏的边界附近。这是因为“1fr”的左边缘位于第二列网格线上，没有宽度，因为没有空间可以弯曲。类似地，“minmax”被放置在第三列网格线上。只是在这个特定的情况下，第二列和第三列网格线在相同的位置(这就是为什么“1fr”列的宽度为零)。

If you ever run into a case where the minimum value is greater than the maximum value, then the whole thing is replaced with the minimum value. Thus, `minmax(500px,200px)` would be treated as a simple `500px`. You probably wouldn’t do this so obviously, but this feature is useful when mixing things like percentages and fractions. Thus, you could have a column that’s `minmax(10%,1fr)` that would be flexible down to the point where the flexible column was less than 10% of the grid container’s width, at which point it would stick at `10%`.

> 如果遇到最小值大于最大值的情况，整个式子就会被替换成最小值。因此，“minmax(500px,200px)”将被视为一个简单的“500px”。您可能不会这么明显地这样做，但是这个特性在混合百分比和分数时非常有用。因此，您可以有一个' minmax(10%，1fr) '的列，该列将具有挠性，直到挠性列小于网格容器宽度的 10%，在这一点上它将保持在' 10% '。

Fractional units and minmaxes are usable on rows just as easily as columns; it’s just that rows are rarely sized in this way. You could easily imagine setting up a layout where the masthead and footer are fixed tracks, while the content is flexible down to a certain point. That might look something like this:

> 分数单位和最小值在行上和在列上一样容易使用;只是行的大小很少是这样的。你可以很容易地想象建立一个布局，其中的报头和页脚是固定的轨道，而内容是灵活的到一定程度。大概是这样的:

```css
grid-template-rows: 3em minmax(5em, 1fr) 2em;
```

That works OK, but it’s a lot more likely that you’ll want to size that row by the height of its content, not some fraction of the grid container’s height. The next section shows exactly how to make that happen.

> 这样做没问题，但是更可能的情况是，您希望根据内容的高度来调整该行的大小，而不是根据网格容器的高度来调整。下一节将详细说明如何实现这一点。

#### Content-aware tracks

It’s one thing to set up grid tracks that take up fractions of the space available to them, or that occupy fixed amounts of space. But what if you want to line up a bunch of pieces of a page and you can’t guarantee how wide or tall they might get? This is where `min-content` and `max-content` come in.

> 设置网格轨道是一回事，它占用了他们可用空间的一部分，或者占用了固定的空间。但是，如果你想把一页纸的许多部分排成一行，却不能保证它们有多宽或多高，那该怎么办呢?这就是“min-content”和“max-content”的用用之处。

What these keywords mean is simple to state, but not necessarily simple to describe in full. `max-content` means, in effect, “take up the maximum amount of space needed for this content.” For large blocks of text (like a blog post), this would generally mean taking as much room as is available, to maximize the space for that content. It can also mean “as wide as necessary to avoid any line-wrapping,” which can be very wide,
given normal paragraphs of text.

> 这些关键字的意思很容易表述，但不一定很容易完整地描述。“max-content”实际上是指“占用该内容所需的最大空间”。对于大段文字(比如一篇博客文章)，这通常意味着要尽可能多地留出空间，以最大化内容的空间。它还可以表示“尽可能宽以避免任何换行”，换行可以非常宽，给出正常的段落。

`min-content`, by contrast, means “take up the bare minimum space needed for this content.” With text, that means squeezing the width down to the point that the longest word (or widest inline element, if there are things like images or form inputs) sits on a line by itself. That would lead to a lot of line breaks in a very skinny, very tall grid element.

> 相比之下，“min-content”的意思是“占用该内容所需的最小空间”。对于文本，这意味着将宽度压缩到最长的单词(或最宽的行内元素，如果有图像或表单输入的话)单独位于一行上。这将导致在一个非常细、非常高的网格元素中出现很多换行。

What’s so powerful about these sizing keywords is that they apply to the entire grid track they define. For example, if you size a column to be `max-content`, then the entire column track will be as wide as the widest content within it. This is easiest to illustrate with a grid of images (12 in this case) with the grid declared as follows and shown in Figure 13-16:

> 这些分级关键字的强大之处在于它们适用于它们定义的整个网格轨迹。例如，如果您将一个列的大小设置为“max-content”，那么整个列跟踪的宽度将与其中最宽的内容相同。这最容易用图像网格(本例中为 12)进行说明，网格声明如下，如图 13-16 所示:

```css
#gallery {
  display: grid;
  grid-template-columns: max-content max-content max-content max-content;
  grid-template-rows: max-content max-content max-content;
}
```

Looking at the columns, we can see that each column track is as wide as the widest image within that track. Where a bunch of portrait images happened to line up, the column is more narrow; where a landscape image showed up, the column was made wide enough to fit it. The same thing happened with the rows. Each row is as tall as the tallest image within it, so wherever a row happened to have all short images, the row is also short.

> 看看这些列，我们可以看到每个列轨道的宽度与该轨道内最宽的图像一样宽。当一堆人像图像碰巧排成一行时，列就更窄了;在显示景观图像的地方，柱子被做得足够宽以适应它。同样的事情也发生在这些行上。每一行的高度与其中最高的图像一样高，所以无论哪一行碰巧有所有的短图像，该行也都是短的。

The advantage here is that this works for any sort of content, no matter what’s in there. So let’s say we add captions to the photos. All of the columns and rows will resize themselves as needed to handle both text and images, as shown in Figure 13-17.

> 这样做的好处是，它适用于任何类型的内容，不管里面有什么。假设我们给照片添加了标题。所有的列和行都将根据需要调整大小以处理文本和图像，如图 13-17 所示。

This isn’t a full-fledged design—the images are out of place, and there’s no attempt to constrain the caption widths. In fact, that’s exactly what we should expect from `max-content` values for the column widths. Since it means “make this column wide enough to hold all its content,” that’s what we got.

> 这不是一个成熟的设计-图像是不合适的地方，并没有试图限制标题宽度。事实上，这正是我们应该期望从列宽度的“max-content”值中得到的结果。因为它的意思是“让这个栏目足够宽，容纳所有内容”，所以我们得到了这个结果。

<Figures figure="13-16">Sizing grid tracks by content</Figures>

<Figures figure="13-17">Sizing grid tracks around mixed content</Figures>

What’s important to realize is that this will hold even if the grid tracks have to spill out of the grid container. That means that even if we’d assigned something like `width: 250px` to the grid container, the images and captions would be laid out just the same. That’s why things like `max-content` tend to appear in `minmax()` statements. Consider the following, where grids with and without `minmax()` appear side by side. In both cases, the grid container is represented by an orange background (see Figure 13-18):

> 重要的是要认识到，即使网格轨道必须溢出网格容器，这种方法也适用。这意味着，即使我们为网格容器分配了类似于“宽度:250px”这样的内容，图像和标题的布局也是一样的。这就是为什么“max-content”这样的语句常常出现在“minmax()”语句中。考虑下面的情况，其中包含和不包含“minmax()”的网格并排出现。在这两种情况下，网格容器都用橙色背景表示(参见图 13-18):

```css
#g1 {
  display: grid;
  grid-template-columns: max-content max-content max-content max-content;
}
#g2 {
  display: grid;
  grid-template-columns:
    minmax(0, max-content) minmax(0, max-content)
    minmax(0, max-content) minmax(0, max-content);
}
```

<Figures figure="13-18">Sizing grid tracks with and without minmax()</Figures>

In the first instance, the grid items completely contain their contents, but they spill out of the grid container. In the second, the `minmax()` directs the browser to keep the columns within the range of `0` and `max-content`, so they’ll all be fitted into the grid container if possible. A variant on this would be to declare `minmax(mincontent, max-content)`, which can lead to a slightly different result than the `0`, `max-content` approach.

> 在第一个实例中，网格项完全包含它们的内容，但是它们溢出了网格容器。在第二个示例中，“minmax()”指示浏览器将列保持在“0”和“max-content”的范围内，以便尽可能地将它们都安装到网格容器中。另一种变体是声明“minmax(mincontent, max-content)”，这可能导致与“0”、“max-content”方法略有不同的结果。

The reason that some images are overflowing their cells in the second example is that the tracks have been fitted into the grid container according to `minmax(0,maxcontent)`. They can’t reach `max-content` in every track, but they can get as close as possible while all still fitting into the grid container. Where the contents are wider than the track, they just stick out of it, overlapping other tracks. This is standard grid behavior.

> 在第二个例子中，一些图像溢出它们的单元格的原因是轨道已经根据“minmax(0,maxcontent)”被安装到网格容器中。他们不可能在每首歌中都达到“最大内容”，但他们可以尽可能地接近，同时所有的歌都能融入网格容器中。当内容比轨道宽时，它们就会突出来，与其他轨道重叠。这是标准网格的行为。

If you’re wondering what happens if you `min-content` both the columns and the rows, it’s pretty much the same as applying `min-content` to the columns and leaving the rows alone. This happens because the grid specification directs browsers to resolve column sizing first, and row sizing after that.

> 如果您想知道如果对列和行都使用“min-content”会发生什么，那么这与对列应用“min-content”而不使用行几乎是一样的。这是因为网格规范要求浏览器首先解析列大小，然后解析行大小。

There’s one more keyword you can use with grid track sizing, which is `auto`. As a minimum, it’s treated as the minimum size for the grid item, as defined by `min-width` or `min-height`. As a maximum, it’s treated the same as `max-content`. You might think this means it can be used only in `minmax()` statements, but this is not the case. You can use it anywhere, and it will take on either a minimum or maximum role. Which one it takes on depends on the other track values around it, in ways that are frankly too complicated to get into here. As with so many other aspects of CSS, using `auto` is essentially letting the browser do what it wants. Sometimes that’s fine, but in general you’ll probably want to avoid it.

> 还有一个可以用于网格轨道大小调整的关键字，即“自动”。作为最小值，它被视为网格项的最小大小，由“最小宽度”或“最小高度”定义。作为一个最大值，它与“max-content”一样。您可能认为这意味着它只能在' minmax() '语句中使用，但事实并非如此。您可以在任何地方使用它，它将承担最小或最大的角色。哪一个取决于它周围的轨道值，以一种非常复杂的方式进入这里。与 CSS 的许多其他方面一样，使用“auto”实际上是让浏览器做它想做的事情。有时这是可以的，但通常你可能会想要避免它。

<Tips tips="blue">There is a caveat to that last statement: <code>auto</code> values allow grid items to be resized by the <code>align-content</code> and <code>justify-content</code> properties, a topic we’ll discuss in a later section, “Aligning and Grids” on page 721. Since <code>auto</code> values are the only track-sizing values that permit this, there may be very good reasons to use <code>auto</code> after all.</Tips>

### 13.3.3 根据栅格中附加元素

In addition to the `min-content` and `max-content` keywords, there’s a `fit-content()` function that allows you to more compactly express certain types of sizing patterns. It’s a bit complicated to decipher, but the effort is worth it:

> 除了“min-content”和“max-content”关键字之外，还有一个“fit-content()”函数，它允许您更简洁地表达某些类型的分级模式。这是一个有点复杂的破译，但努力是值得的:

`fit-content()` accepts a `<length>` or a `<percentage>` as its argument, like this:

> `fit-content()` 接受 `<length>` 或 `<percentage>` 作为其参数，如下所示:

```css
#grid {
  display: grid;
  grid-template-columns: 1fr fit-content(150px) 2fr;
}
#grid2 {
  display: grid;
  grid-template-columns: 2fr fit-content(50%) 1fr;
}
```

Before we explore what that means, let’s ponder the pseudo-formula given by the specification:

> 在我们探索这意味着什么之前，让我们思考一下规范给出的伪公式:

```css
fit-content(argument) => min(max-content, max(min-content, argument))
```

which means, essentially, “figure out which is greater, the `min-content` sizing or the supplied argument, and then take that result and choose whichever is smaller, that result or the `max-content` size.” Which is probably confusing! It certainly was to me, the first 17 times I worked through it.

> 这意味着，本质上，“找出‘最小内容’大小和提供的参数哪个更大，然后选择那个结果，然后选择那个更小的结果或‘最大内容’大小。“这可能让人困惑!”对我来说，前 17 次我都是如此。

I feel like a better way of phrasing it is: “`fit-content(argument)` is equivalent to `minmax(min-content,max-content)`, except that the value given as an argument sets an upper limit, similar to `max-width` or `max-height`.” Let’s consider this example:

> 我觉得更好的表达方式是:“‘fit-content(参数)’相当于‘minmax(min-content,max-content)’，只是作为参数给出的值设置了一个上限，类似于‘max-width’或‘max-height’。”让我们来看看这个例子:

```css
#example {
  display: grid;
  grid-template-columns: fit-content(50ch);
}
```

The argument here is `50ch`, or about 50 characters wide. So we’re setting up a single column that’s having its content fit to that measure.

> 这里的参数是“50ch”，即大约 50 个字符宽。我们设置了一个单独的列让它的内容符合这个标准。

For the initial case, assume the content is only 29 characters long, measuring 29ch (due to it being in a monospace font). That means the value of `max-content` is `29ch`, and the column will be only that wide, because it minimizes to that measure—`29ch` is smaller than whatever the maximum of `50ch` and `min-content` turns out to be.

> 对于初始情况，假设内容只有 29 个字符长，度量为 29ch(因为它是 monospace 字体)。这意味着“max-content”的值是“29ch”，而列的宽度将只有那么宽，因为它最小化了这个度量——“29ch”比“50ch”和“min-content”的最大值还要小。

Now, let’s assume a bunch of text content is added so that there are 256 characters measuring `256ch` in width. That means `max-content` evaluates to `256ch`. This is well beyond the `50ch` argument, so the column is constrained to be the larger of `min-content` and `50ch`, which is `50ch`.

> 现在，让我们假设添加了一些文本内容，因此有 256 个字符，宽度为“256ch”。这意味着“max-content”的计算结果是“256ch”。这远远超出了' 50ch '参数的范围，因此该列被限制为' min-content '和' 50ch '中较大的一个，即' 50ch '。

As further illustration, consider the results of the following, as shown in Figure 13-19:

> 为了进一步说明，考虑下面的结果，如图 13-19 所示:

```css
#thefollowing {
  display: grid;
  grid-template-columns: fit-content(50ch) fit-content(50ch) fit-content(50ch);
  font-family: monospace;
}
```

<Figures figure="13-19">Sizing grid tracks with fit-content()</Figures>

Notice the first column is narrower than the other two. Its `29ch` content minimizes to that size. The other two columns have more content than will fit into `50ch`, so they line-wrap, because their width has been limited to `50ch`.

> 注意第一列比其他两列窄。它的“29ch”内容最小化到这个大小。另外两列的内容比‘50ch’中包含的内容更多，所以它们是换行的，因为它们的宽度被限制为‘50ch’。

Now let’s consider what happens if an image is added to the second column. We’ll make it 500px wide, which is wider than `50ch` in this instance. For that column, the maximum of `min-content` and `50ch` is determined. As we said, the larger value there is `min-content`, which is to say `500px` (the width of the image). Then the `minimum` of `500px` and `max-content` is determined. The text, rendered as a single line, would go on past `500px`, so the minimum is `500px`. Thus, the second column is now 500 pixels wide. This is depicted in Figure 13-20.

> 现在，让我们考虑如果将一个图像添加到第二列会发生什么。我们将它的宽度设为 500px，在本例中宽度大于 50ch。对于该列，确定“min-content”和“50ch”的最大值。如前所述，最大的值是“min-content”，即“500px”(图像的宽度)。然后确定“最小”为“500px”和“max-content”。文本，作为一个单一的行，将继续过去' 500px '，所以最低是' 500px '。因此，第二列现在是 500 像素宽。如图 13-20 所示。

<Figures figure="13-20">Fitting to wide content</Figures>

If you compare Figure 13-19 to Figure 13-20, you’ll see that the text in the second column wraps at a different point, due to the change in column width. But also compare the text in the the third column. It, too, has different line-wraps.

> 如果比较图 13-19 和图 13-20，您将看到由于列宽度的变化，第二列中的文本包装在不同的位置。还要比较第三栏的文字。它也有不同的行包装。

That happened because after the first and second columns were sized, the third column had a bit less than `50ch` of space in which to be sized. `fit-content(50ch)` still did its thing, but here, it did so within the space available to it. Remember, the `50ch` argument is an upper bound, not a fixed size.

> 这是因为在调整了第一列和第二列的大小之后，第三列的大小空间略小于' 50ch '。“fit-content(50ch)”仍然发挥着它的作用，但在这里，它是在可用空间内发挥作用的。请记住，' 50ch '参数是一个上限，而不是一个固定的大小。

This is one of the great advantages of `fit-content()` over the less flexible `minmax()`. It allows you to shrink tracks down to their minimum content-size when there isn’t much content, while still setting an upper bound on the track size when there’s a lot of content.

> 这是“fit-content()”相对于不太灵活的“minmax()”的一大优点。它允许您在没有太多内容时将音轨缩小到最小的内容大小，而在有大量内容时仍然设置音轨大小的上限。

You’ve probably been wondering about the repetitive grid template values in previous examples, and what happens if you need more than three or four grid tracks. Will you have to write out every single track width individually? Indeed not, as we’ll see in the next section.

> 您可能想知道在前面的示例中重复的网格模板值，以及如果需要超过 3 或 4 个网格轨道会发生什么。你要把每条轨道的宽度单独写出来吗?确实不是，我们将在下一节看到。

### 13.3.4 重复栅格线

If you have a situation where you want to set up a bunch of grid tracks of the same size, you probably don’t want to have to type out every single one of them. Fortunately, `repeat()` is here to make sure you don’t have to.

> 如果您想要设置一组相同大小的网格轨迹，您可能不希望必须键入它们中的每一个。幸运的是，“repeat()”可以确保您不必这样做。

Let’s say we want to set up a column grid line every 5 ems, and have 10 column tracks. Here’s how to do that:

> 假设我们想要每隔 5 ems 建立一个列网格线，并且有 10 个列轨迹。以下是如何做到这一点:

```css
#grid {
  display: grid;
  grid-template-columns: repeat(10, 5em);
}
```

That’s it. Done. Ten column tracks, each one `5em` wide, for a total of 50 ems of column tracks. It sure beats typing `5em` 10 times!

> 就是这样。做。十列轨道，每' 5em '宽，共 50 ems 列轨道。它肯定比打字‘5em’10 次强多了!

Any track-sizing value can be used in a repeat, from `min-content` and `max-content` to `fr` values to `auto`, and so on, and you can put together more than one sizing value. Suppose we want to define a column structure such that there’s a `2em` track, then a `1fr` track, and then another `1fr` track—and, furthermore, we want to repeat that pattern three times. Here’s how to do that, with the result shown in Figure 13-21:

> 任何跟踪大小值都可以重复使用，从“min-content”和“max-content”到“fr”值再到“auto”，等等，您可以组合多个大小值。假设我们要定义一个列结构，其中有一个' 2em '轨道，然后是一个' 1fr '轨道，然后是另一个' 1fr '轨道，而且，我们希望重复该模式三次。下面是如何做到这一点，结果如图 13-21 所示:

```css
#grid {
  display: grid;
  grid-template-columns: repeat(3, 2em 1fr 1fr);
}
```

<Figures figure="13-21">Repeating a track pattern</Figures>

Notice how the last column track is a `1fr` track, whereas the first column track is `2em` wide. This is an effect of the way the `repeat()` was written. It’s easy to add another `2em` track at the end, in order to balance things out, just by making this change:

> 注意最后一列磁道是“1fr”磁道，而第一列磁道是“2em”宽。这是' repeat() '的书写方式的结果。很容易添加另一个' 2em '轨道在年底，以平衡的东西，只需做这样的变化:

```css
#grid {
  display: grid;
  grid-template-columns: repeat(3, 2em 1fr 1fr) 2em;
}
```

See that extra `2em` at the end of the value? That adds one more column track after the three repeated patterns. This highlights the fact that `repeat` can be combined with any other track-sizing values—even other repeats—in the construction of a grid. The one thing you `can’t` do is nest a repeat inside another repeat.

> 看到值末尾的那个额外的“2em”了吗?这在三个重复模式之后又添加了一个列跟踪。这突出了这样一个事实:在网格的构建过程中，“repeat”可以与任何其他跟踪大小值(甚至是其他 repeat)相结合。你“不能”做的一件事是把一个重复嵌套在另一个重复中。

Other than that, just about anything goes within a `repeat()` value. Here’s an example taken straight from the grid specification:

> 除此之外，几乎所有内容都位于' repeat() '值内。下面是一个直接取自网格规范的例子:

```css
#grid {
  display: grid;
  grid-template-columns: repeat(4, 10px [col-start] 250px [col-end]) 10px;
}
```

In this case, there are four repetitions of a 10-pixel track, a named grid line, a 250-pixel track, and then another named grid line. Then, after the four repetitions, a final 10-pixel column track. Yes, that means there will be four column grid lines named `col-start`, and another four named `col-end`, as shown in Figure 13-22. This is acceptable; grid-line names are not required to be unique.

> 在本例中，一个 10 像素的轨迹重复 4 次，一个指定的网格线重复 4 次，一个 250 像素的轨迹重复 4 次，然后是另一个指定的网格线重复 4 次。然后，经过 4 次重复，最后得到一个 10 像素的列轨迹。是的，这意味着将有四个列网格线命名为“coll -start”，另外四个列网格线命名为“coll -end”，如图 13-22 所示。这是可以接受的;网格线名称不需要是唯一的。

<Figures figure="13-22">Repeated columns with named grid lines</Figures>

One thing to remember, if you’re going to repeat named lines, is that if you place two named lines next to each other, they’ll be merged into a single, double-named grid line. In other words, the following two declarations are equivalent:

> 需要记住的一点是，如果你要重复命名的线，如果你把两个命名的线放在一起，它们会合并成一个，双命名的网格线。换句话说，以下两种声明是等价的:

```css
grid-template-rows: repeat(3, [top] 5em [bottom]);
grid-template-rows: [top] 5em [bottom top] 5em [top bottom] 5em [bottom];
```

<Tips tips="blue">If you’re concerned about having the same name applied to multiple grid lines, don’t be: there’s nothing preventing it, and it can even be helpful in some cases. We’ll explore ways to handle such situations in an upcoming section, “Using Column and Row Lines” on page 687.</Tips>

#### Auto-filling tracks

There’s even a way to set up a simple pattern and repeat it until the grid container is filled. This doesn’t have quite the same complexity as regular `repeat()`—at least not yet—but it can still be pretty handy.

> 甚至可以创建一个简单的模式并重复它，直到网格容器被填满。它没有常规的“repeat()”那么复杂——至少现在还没有——但它仍然非常方便。

For example, suppose we want to have the previous row pattern repeat as many times as the grid container will comfortably accept:

> 例如，假设我们想让前面的行模式重复多少次网格容器就可以接受多少次:

```css
grid-template-rows: repeat(auto-fill, [top] 5em [bottom]);
```

That will define a row line every 5 ems until there’s no more room. Thus, for a grid container that’s 11 ems tall, the following is equivalent:

> 每隔 5 ems 就会定义一行，直到没有空间。因此，对于一个 11 ems 高的网格容器，以下内容是等价的:

```css
grid-template-rows: [top] 5em [bottom top] 5em [bottom];
```

If the grid container’s height is increased past 15 ems, but is less than 20 ems, then this is an equivalent declaration:

> 如果网格容器的高度增加了超过 15 ems，但是小于 20 ems，那么这是一个等价的声明:

```css
grid-template-rows: [top] 5em [bottom top] 5em [top bottom] 5em [bottom];
```

See Figure 13-23 for examples of the auto-filled rows at three different grid container heights.

> 图 13-23 给出了三个不同网格容器高度的自动填充行示例。

<Figures figure="13-23">Auto-filling rows at three different heights</Figures>

The limitation with auto-repeating is that it can take only an optional grid-line name, a fixed track size, and another optional grid-line name. So `[top] 5em [bottom]` represents about the maximum value pattern. You can drop the named lines and just repeat `5em`, or just drop one of the names. It’s not possible to repeat multiple fixed track sizes, nor can you repeat flexible track sizes. (Which makes sense: how many times would a browser repeat `1fr` to fill out a grid container? Once.)

> 自动重复的限制是它只能使用一个可选的网格线名称、一个固定的磁道大小和另一个可选的网格线名称。所以“[顶]5em[底]”代表了最大值模式。您可以删除已命名的行，然后重复“5em”，或者删除其中一个名称。不可能重复多个固定轨道尺寸，也不能重复灵活轨道尺寸。(这是有道理的:浏览器会重复多少次“1fr”来填充一个网格容器?一次。)

<Tips tips="blue">You might wish you could auto-repeat multiple track sizes in order to define “gutters” around your content columns. This is usually unnecessary because grids have a concept of (and properties to define) track gutters, which we’ll cover in an upcoming section, “Opening Grid Spaces” on page 714.</Tips>

Furthermore, you can have only one auto-repeat in a given track template. Thus, the following would `not` be permissible:

> 此外，在给定的跟踪模板中只能有一个自动重复。因此，以下内容是不允许的:

```css
grid-template-columns: repeat(auto-fill, 4em) repeat(auto-fill, 100px);
```

However, you `can` combine fixed-repeat tracks with auto-fill tracks. For example, you could start with three wide columns, and then fill the rest of the grid container with narrow tracks (assuming there’s space for them). That would look something like this:

> 但是，您可以将固定重复音轨与自动填充音轨相结合。例如，您可以从三个宽列开始，然后用窄轨填充网格容器的其余部分(假设有空间)。大概是这样的:

```css
grid-template-columns: repeat(3, 20em) repeat(auto-fill, 2em);
```

You can flip that around, too:

> 你也可以反过来看:

```css
grid-template-columns: repeat(auto-fill, 2em) repeat(3, 20em);
```

That works because the grid layout algorithm assigns space to the fixed tracks first, and then fills up whatever space is left with auto-repeated tracks. The end result of that example is to have one or more auto-filled 2-em tracks, and then three 20-em tracks. Two examples of this are shown in Figure 13-24.

> 这是可行的，因为网格布局算法首先将空间分配给固定轨道，然后用自动重复轨道填充剩余的空间。该示例的最终结果是拥有一个或多个自动填充的 2-em 音轨，以及三个 20-em 音轨。图 13-24 中显示了两个这样的例子。

<Figures figure="13-24">Auto-filling columns next to fixed columns</Figures>

With `auto-fill`, you will always get at least one repetition of the track template, even if it won’t fit into the grid container for some reason. You’ll also get as many tracks as will fit, even if some of the tracks don’t have content in them. As an example, suppose you set up an auto-fill that placed five columns, but only the first three of them actually ended up with grid items in them. The other two would remain in place, holding open layout space.

> 使用“自动填充”，您将始终得到至少一个重复的轨道模板，即使它不适合网格容器的某些原因。你也会得到尽可能多的音轨，即使有些音轨没有内容。例如，假设您设置了一个放置了五列的自动填充，但实际上只有前三列中包含网格项。另外两个将保留在原地，保持开放的布局空间。

If you use `auto-fit`, on the other hand, then tracks that don’t contain any grid items will be dropped. Otherwise, `auto-fit` acts the same as `auto-fill`. Suppose the following:

> 另一方面，如果你使用“自动适应”，那么不包含任何网格项目的轨道将被删除。否则，' auto-fit '的作用与' auto-fill '相同。假设如下:

```css
grid-template-columns: repeat(auto-fit, 20em);
```

If there’s room for five column tracks in the grid container (i.e., it’s more than 100 ems wide), but two tracks don’t have any grid items to go into them, those empty grid tracks will be dropped, leaving the three column tracks that `do` contain grid items. The leftover space is handled in accordance with the values of `align-content` and `justify-content` (discussed in the upcoming section, “Aligning and Grids” on page 721). A simple comparison of `auto-fill` and `auto-fit` is shown in Figure 13-25, where the numbers in the colored boxes indicate the grid-column number to which they’ve been attached.

> 如果网格容器中有五个列轨道的空间(即，它超过 100 ems 宽)，但两个轨道没有任何网格项目进入他们，那些空的网格轨道将被删除，留下三列轨道'做'包含网格项目。剩下的空间是按照“对齐内容”和“对齐内容”的值来处理的(在接下来的章节中讨论，“对齐和网格”在 721 页)。图 13-25 显示了“auto-fill”和“auto-fit”的简单比较，其中彩色框中的数字表示它们所附加的网格列号。

<Figures figure="13-25">Auto-fill versus auto-fit</Figures>

### 13.3.5 栅格区域

Sometimes, you’d rather just draw a picture of your grid—both because it’s fun to do, and because the picture can serve as self-documenting code. It turns out you can more or less do exactly that with the `grid-template-areas` property.

> 有时，您宁愿只绘制网格的图片—因为这样做很有趣，而且图片可以作为自文档化代码。事实证明，使用' grid-template-area '属性可以或多或少地做到这一点。

<!-- <Cards cards="grid-template-areas" /> -->

We could go through a wordy description of how this works, but it’s a lot more fun to just show it. The following rule has the result shown in Figure 13-26:

> 我们可以详细地描述一下它是如何工作的，但是展示它要有趣得多。以下规则的结果如图 13-26 所示:

```css
#grid {
  display: grid;
  grid-template-areas:
    "h h h h"
    "l c c r"
    "l f f f";
}
```

<Figures figure="13-26">A simple set of grid areas</Figures>

That’s right: the letters in the string values are used to define how areas of the grid are shaped. Really! And you aren’t even restricted to single letters! For example, we could expand the previous example like so:

> 这是正确的:字符串值中的字母用于定义网格区域的形状。真的!你甚至不受限于单个字母!例如，我们可以像这样展开前面的例子:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "leftside content content rightside"
    "leftside footer footer footer";
}
```

The grid layout is the same as that shown in Figure 13-26, though the name of each area would be different (e.g., `footer` instead of f).

> 网格布局与图 13-26 所示相同，但是每个区域的名称不同(例如，“footer”而不是 f)。

In defining template areas, the whitespace is collapsed, so you can use it (as I did in the previous example) to visually line up columns of names in the value of `grid-template-areas`. You can line them up with spaces or tabs, whichever will annoy your coworkers the most. Or you can just use a single space to separate each identifier, and not worry about the names lining up with each other. You don’t even have to line break between strings; the following works just as well as a pretty-printed version:

> 在定义模板区域时，空格是折叠的，所以您可以使用它(就像我在前面的示例中所做的那样)来在“网格模板区域”的值中可视化地排列名称列。你可以用空格或制表符把它们排起来，无论哪种最让你的同事讨厌。或者，您可以只使用一个空格来分隔每个标识符，而不必担心名称之间的排列。你甚至不需要在字符串之间换行;下面的作品，以及一个漂亮的印刷版本:

```css
grid-template-areas: "h h h h" "l c c r" "l f f f";
```

What you can’t do is merge those separate strings into a single string and have it mean the same thing. Every new string (as delimited by the double quote marks) defines a new row in the grid. So the previous example, like the examples before it, defines three rows. If we merged them all into a single string, like so:

> 你不能做的是把这些单独的字符串合并成一个单独的字符串，让它的意思相同。每个新字符串(由双引号分隔)在网格中定义一个新行。前面的例子，和前面的例子一样，定义了三行。如果我们把它们合并成一个字符串，就像这样:

```css
grid-template-areas: "h h h h
 l c c r
 l f f f";
```

then we’d have a single row of 12 columns, starting with the 4-column area `h` and ending with the 3-column area `f`. The line breaks aren’t significant in any way, except as whitespace that separates one identifier from another.

> 然后我们会有一个 12 列的单行，从 4 列的区域“h”开始，以 3 列的区域“f”结束。换行符在任何方面都不重要，除了作为分隔一个标识符与另一个标识符的空白。

If you look at these values closely, you may come to realize that each individual identifier represents a grid cell. Let’s bring back our first example from this section, and consider the result shown in Figure 13-27:

> 如果仔细查看这些值，您可能会发现每个标识符都代表一个网格单元。让我们回到本节的第一个示例，并考虑图 13-27 所示的结果:

```css
#grid {
  display: grid;
  grid-template-areas:
    "h h h h"
    "l c c r"
    "l f f f";
}
```

<Figures figure="13-27">Grid cells with identifiers</Figures>

This is exactly the same layout result, but here, we’ve shown how each grid identifier in the `grid-template-areas` value corresponds to a grid cell. Once all the cells are identified, the browser merges any adjacent cells with the same name into a single area that encloses all of them—as long as they describe a rectangular shape! If you try to set up more complicated areas, the entire template is invalid. Thus, the following would result in no grid areas being defined:

> 这是完全相同的布局结果，但是在这里，我们已经展示了' grid-template-areas '值中的每个网格标识符如何对应于一个网格单元格。一旦所有的单元格都被识别出来，浏览器就会将所有具有相同名称的相邻单元格合并到一个单独的区域中，只要它们描述的是一个矩形!如果试图设置更复杂的区域，则整个模板无效。因此，以下结果将导致没有定义网格区域:

```css
#grid {
  display: grid;
  grid-template-areas:
    "h h h h"
    "l c c r"
    "l l f f";
}
```

See how `l` outlines an “L” shape? That humble change causes the entire `grid-template-areas` value to be dropped as invalid. A future version of grid layout may allow for nonrectangular shapes, but for now, this is what we have.

> 看到“l”是如何勾勒出“l”形状的吗?这个微小的更改将导致整个“网格模板区域”值作为无效值删除。网格布局的未来版本可能允许非矩形的形状，但现在，这是我们所拥有的。

If you have a situation where you want to only define some grid cells to be part of grid areas, but leave others unlabeled, you can use one or more `.` characters to fill in for those unnamed cells. Let’s say you just want to define some header, footer, and sidebar areas, and leave the rest unnamed. That would look something like this, with the result shown in Figure 13-28:

> 如果你有一个情况，你只想定义一些网格单元格是网格区域的一部分，但不标记其他，你可以使用一个或多个'。来填充那些未命名的细胞。假设您只想定义一些页眉、页脚和边栏区域，其余部分未命名。结果如图 13-28 所示:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "left ... ... right"
    "footer footer footer footer";
}
```

<Figures figure="13-28">A grid with some unnamed grid cells</Figures>

The two grid cells in the center of the grid are not part of a named area, having been represented in the template by `null cell tokens` (the `.` identifiers). Where each of those `...` sequences appears, we could have used one or more null tokens—so `left . . right` or `left ..... ..... right` would work just as well.

> 网格中心的两个网格单元不属于指定区域的一部分，在模板中表示为“空单元标记”(即“”)。的标识符)。每一个。序列出现时，我们可以使用一个或多个空标记—所以' left . .“右”或“左……”“对”也行。

You can be as simple or creative with your cell names as you like. If you want to call your header `ronaldo` and your footer `podiatrist`, go for it. You can even use any Unicode character above codepoint U+0080, so `ConHugeCo©®™` and `åwësømë` are completely valid area identifiers…as are emoji!

> 您可以简单或有创意地使用您喜欢的细胞名称。如果你想称你的头球为 `ronaldo`，称你的脚部为 `podiatrist`，那就去做吧。你甚至可以使用任何 Unicode 字符 codepoint U + 0080 以上,所以`ConHugeCo©®™` 和 `åwësømë`是完全有效的区域标识符…emoji 也一样!

Now, to size the grid tracks created by these areas, we bring in our old friends `grid-template-columns` and `grid-template-rows`. Let’s add both to the previous example, with the result shown in Figure 13-29:

> 现在，为了调整这些区域创建的网格轨迹的大小，我们引入了老朋友 `grid-template-columns` 和 `grid-template-rows`。让我们将它们都添加到前面的示例中，结果如图 13-29 所示:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "left ... ... right"
    "footer footer footer footer";
  grid-template-columns: 1fr 20em 20em 1fr;
  grid-template-rows: 40px 10em 3em;
}
```

<Figures figure="13-29">Named areas and sized tracks</Figures>

Thus, the columns and rows created by naming the grid areas are given track sizes. If we give more track sizes than there are area tracks, that will add more tracks past the named areas. Therefore, the following CSS will lead to the result shown in Figure 13-30:

> 因此，通过命名网格区域创建的列和行被赋予轨道大小。如果我们给出的轨道大小比区域轨道的大小多，那么将会在命名区域之后添加更多的轨道。因此，下面的 CSS 将得到如图 13-30 所示的结果:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "left ... ... right"
    "footer footer footer footer";
  grid-template-columns: 1fr 20em 20em 1fr 1fr;
  grid-template-rows: 40px 10em 3em 20px;
}
```

<Figures figure="13-30">Adding more tracks beyond the named areas</Figures>

So, given that we’re naming areas, how about mixing in some named grid lines? As it happens, we already have: naming a grid area automatically adds names to the grid lines at its start and end. For the `header` area, there’s an implicit `header-start` name on its first column-grid line `and` its first row-grid line, and `header-end` for its second column- and row-grid lines. For the `footer` area, the `footer-start` and `footer-end` names were automatically assigned to its grid lines.

> 既然我们已经命名了区域，那么混合一些命名的网格线呢?实际上，我们已经有了:为网格区域命名会自动将名称添加到网格线的开始和结束处。对于“header”区域，它的第一个列-网格线和第一个行-网格线上有一个隐含的“head -start”名称，而第二个列-网格线和行-网格线上有“head -end”名称。对于“footer”区域，“footer-start”和“footer-end”名称被自动分配到网格线上。

Grid lines extend throughout the whole grid area, so a lot of these names are coincident. Figure 13-31 shows the naming of the lines created by the following template:

> 网格线延伸到整个网格区域，因此许多名称是重合的。图 13-31 显示了以下模板创建的行名称:

```css
grid-template-areas:
  "header header header header"
  "left ... ... right"
  "footer footer footer footer";
```

<Figures figure="13-31">Implicit grid-line names made explicit</Figures>

Now let’s mix it up even more by adding a couple of explicit grid-line names to our CSS. Given the following rules, the first column-grid line in the grid would add the name begin, and the second row-grid line in the grid would add the name `content`:

> 现在，让我们通过向 CSS 添加一些显式网格线名称来进一步混合它。根据以下规则，网格中的第一个列-网格线将添加名称 begin，而网格中的第二个行-网格线将添加名称“content”:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "left ... ... right"
    "footer footer footer footer";
  grid-template-columns: [begin] 1fr 20em 20em 1fr 1fr;
  grid-template-rows: 40px [content] 1fr 3em 20px;
}
```

Again: those grid-line names are `added` to the implicit grid-line names created by the named areas. Interestingly enough, grid-line names never replace other grid-line names. Instead, they just keep piling up.

> 同样:这些网格线名称被“添加”到由命名区域创建的隐式网格线名称中。有趣的是，网格线名称永远不会取代其他网格线名称。相反，它们只会越积越多。

Even more interesting, this implicit-name mechanism runs in reverse. Suppose you don’t use `grid-template-areas` at all, but instead set up some named grid lines like so, as illustrated in Figure 13-32:

> 更有趣的是，这种隐名机制是反向运行的。假设您根本不使用“网格模板-区域”，而是像这样设置一些命名的网格线，如图 13-32 所示:

```css
grid-template-columns:
  [header-start footer-start] 1fr
  [content-start] 1fr [content-end] 1fr
  [header-end footer-end];
grid-template-rows:
  [header-start] 3em
  [header-end content-start] 1fr
  [content-end footer-start] 3em
  [footer-end];
```

<Figures figure="13-32">Implicit grid-area names made explicit</Figures>

Because the grid lines use the form of `name-start`/`name-end`, the grid areas they define are implicitly named. To be frank, it’s clumsier than doing it the other way, but the capability is there in case you ever want it.

> 因为网格线使用 `name-start`/`name-end` 的形式，所以它们定义的网格区域是隐式命名的。坦率地说，它比另一种方法更笨拙，但是在你需要的时候，它是有能力的。

Bear in mind that you don’t need all four grid lines to be named in order to create a named grid area, though you probably do need them all to create a named grid area where you want it to be. Consider the following example:

> 请记住，您不需要为了创建一个指定的网格区域而对所有的 4 条网格线进行命名，尽管您可能确实需要将它们全部用于在您希望的位置创建一个指定的网格区域。考虑下面的例子:

```css
grid-template-columns: 1fr [content-start] 1fr [content-end] 1fr;
grid-template-rows: 3em 1fr 3em;
```

This will still create a grid area named `content`. It’s just that the named area will be placed into a new row after all the defined rows. What’s odd is that an extra, empty row will appear after the defined rows but before the row containing `content`. This has been confirmed to be the intended behavior. Thus, if you try to create a named area by naming the grid lines and miss one or more of them, then your named area will effectively hang off to one side of the grid instead of being a part of the overall grid structure.

> 这仍然会创建一个名为“content”的网格区域。只是在所有已定义的行之后，命名区域将被放置到新行中。奇怪的是，一个额外的空行会出现在定义的行之后，但在包含“content”的行之前。这已被证实是有意为之的行为。因此，如果您试图通过命名网格线来创建一个命名区域，而遗漏了一个或多个网格线，那么您的命名区域将有效地挂在网格的一侧，而不是整个网格结构的一部分。

So, again, you should probably stick to explicitly naming grid areas and let the `start-` and `end-` grid-line names be created implicitly, as opposed to the other way around.

> 因此，再次强调，您可能应该坚持显式地命名网格区域，并允许隐式地创建“开始”和“结束”网格线名称，而不是相反。

## 13.4 在栅格中附加元素

Believe it or not, we’ve gotten this far without talking about how grid items are actually attached to a grid, once it’s been defined.

> 信不信由你，我们已经讲了这么多，但还没有讨论网格项是如何被实际附加到一个网格的，一旦它被定义。

### 13.4.1 使用列线和行线

There are a couple of ways to go about this, depending on whether you want to refer to grid lines or grid areas. We’ll start with four simple properties that attach an element to grid lines.

> 有几种方法可以做到这一点，这取决于您是要引用网格线还是网格区域。我们将从四个将元素附加到网格线的简单属性开始。

<!-- <Cards cards="grid-row-start_grid-row-end_grid-column-start_grid-column-end" /> -->

What these properties do is let you say, “I want the edge of the element to be attached to grid line such-and-so.” As with so much of grid layout, it’s a lot easier to show than to describe, so ponder the following styles and their result (see Figure 13-33):

> 这些属性的作用是让你说，“我想让元素的边缘连接到网格线上，诸如此类。由于有这么多的网格布局，它更容易显示而不是描述，所以考虑以下样式和它们的结果(参见图 13-33):

```css
.grid {
  display: grid;
  width: 50em;
  grid-template-rows: repeat(5, 5em);
  grid-template-columns: repeat(10, 5em);
}
.one {
  grid-row-start: 2;
  grid-row-end: 4;
  grid-column-start: 2;
  grid-column-end: 4;
}
.two {
  grid-row-start: 1;
  grid-row-end: 3;
  grid-column-start: 5;
  grid-column-end: 10;
}
.three {
  grid-row-start: 4;
  grid-column-start: 6;
}
```

Here, we’re using grid-line numbers to say where and how the elements should be placed within the grid. Column numbers count from left to right, and row numbers from top to bottom. Note that if you omit ending grid lines, as was the case for `.three`, then the next grid lines in sequence are used for the end lines.

> 在这里，我们使用网格线编号来表示元素在网格中的位置和方式。列号从左到右计数，行号从上到下计数。注意，如果您省略了结束网格线，就像'的情况一样。三'，然后依次使用下一个网格线作为结束线。

Thus, the rule for `.three` in the previous example is exactly equivalent to the following:

> 因此，'的规则。在前面的例子中，‘three’完全等价于以下内容:

```css
.three {
  grid-row-start: 4;
  grid-row-end: 5;
  grid-column-start: 6;
  grid-column-end: 7;
}
```

<Figures figure="13-33">Attaching elements to grid lines</Figures>

There’s another way to say that same thing, as it happens: you could replace the ending values with `span 1`, or even just plain `span`, like this:

> 还有另一种方式来表达同样的事情:你可以用‘span 1’来替换结束值，或者甚至是简单的‘span’，就像这样:

```css
.three {
  grid-row-start: 4;
  grid-row-end: span 1;
  grid-column-start: 6;
  grid-column-end: span;
}
```

If you supply `span` with a number, you’re saying, “span across this many grid tracks.” So we can rewrite our earlier example like this, and get exactly the same result:

> 如果你给‘span’加上一个数字，你是在说，“跨越这么多网格轨道的 span。所以我们可以像这样重写之前的例子，得到完全相同的结果:

```css
#grid {
  display: grid;
  grid-template-rows: repeat(5, 5em);
  grid-template-columns: repeat(10, 5em);
}
.one {
  grid-row-start: 2;
  grid-row-end: span 2;
  grid-column-start: 2;
  grid-column-end: span 2;
}
.two {
  grid-row-start: 1;
  grid-row-end: span 2;
  grid-column-start: 5;
  grid-column-end: span 5;
}
.three {
  grid-row-start: 4;
  grid-row-end: span 1;
  grid-column-start: 6;
  grid-column-end: span;
}
```

If you leave out a number for `span`, it’s set to be `1`. You can’t use zero or negative numbers for `span`; only positive integers.

> 如果你省略了数字‘span’，它就会被设置为‘1’。你不能用 0 或负数来表示“张成的空间”;唯一的正整数。

An interesting feature of `span` is that you can use it for both ending `and` starting grid lines. The precise behavior of `span` is that it counts grid lines in the direction “away” from the grid line where it starts. In other words, if you define a start grid line and set the ending grid line to be a `span` value, it will search toward the end of the grid.

> “span”的一个有趣的特性是，你可以将它用于结束网格线和开始网格线。“span”的准确行为是它计算网格线的方向“远离”它开始的网格线。换句话说，如果您定义了一个起始网格线，并将结束网格线设置为‘span’值，那么它将搜索网格的末端。

Conversely, if you define an ending grid line and make the start line a `span` value, then it will search toward the start of the grid.

> 相反，如果您定义了一个结束网格线，并将起始网格线设置为‘span’值，那么它将搜索网格的起始部分。

That means the following rules will have the result shown in Figure 13-34:

> 这意味着以下规则的结果如图 13-34 所示:

```css
#grid {
  display: grid;
  grid-rows: repeat(4, 2em);
  grid-columns: repeat(5, 5em);
}
.box01 {
  grid-row-start: 1;
  grid-column-start: 3;
  grid-column-end: span 2;
}
.box02 {
  grid-row-start: 2;
  grid-column-start: span 2;
  grid-column-end: 3;
}
.box03 {
  grid-row-start: 3;
  grid-column-start: 1;
  grid-column-end: span 5;
}
.box04 {
  grid-row-start: 4;
  grid-column-start: span 1;
  grid-column-end: 5;
}
```

<Figures figure="13-34">Spanning grid lines</Figures>

In contrast to `span` numbering, you aren’t restricted to positive integers for your actual grid-line values. Negative numbers will count backward from the end of explicitly defined grid lines. Thus, to place an element into the bottom-right grid cell of a defined grid, regardless of how many columns or rows it might have, you can just say this:

> 与“span”编号不同，您的实际网格线值不局限于正整数。负数将从显式定义的网格线的末尾开始向后计数。因此，要将一个元素放入已定义网格的右下角网格单元中，不管它可能有多少列或行，您只需这样说:

```css
grid-column-start: -1;
grid-row-start: -1;
```

Note that this doesn’t apply to any implicit grid tracks, a concept we’ll get to in a bit, but only to the grid lines you explicitly define via one of the `grid-template-*` properties (e.g., `grid-template-rows`).

> 注意，这并不适用于任何隐含的网格轨迹，我们稍后将讨论这个概念，但只适用于通过' grid-template-\* '属性(例如，' grid-template-rows ')显式定义的网格线。

We aren’t restricted to grid-line numbers, as it happens. If there are named grid lines, we can refer to those instead of (or in conjunction with) numbers. If you have multiple instances of a grid-line name, then you can use numbers to identify which instance of the grid-line name you’re talking about. Thus, to start from the fourth instance of a row grid named `mast-slice`, you can say `mast-slice 4`. Take a look at the following, illustrated in Figure 13-35, for an idea of how this works:

> 事实上，我们并不局限于网格线编号。如果有指定的网格线，我们可以引用它们而不是(或与它们一起)数字。如果您有一个网格线名称的多个实例，那么您可以使用数字来确定您所谈论的网格线名称的实例。因此，要从名为“mast-slice”的行网格的第四个实例开始，您可以说“mast-slice 4”。请看下面的图 13-35，了解一下它是如何工作的:

```css
#grid {
  display: grid;
  grid-template-rows: repeat(5, [R] 4em);
  grid-template-columns: 2em repeat(5, [col-A] 5em [col-B] 5em) 2em;
}
.one {
  grid-row-start: R 2;
  grid-row-end: 5;
  grid-column-start: col-B;
  grid-column-end: span 2;
}
.two {
  grid-row-start: R;
  grid-row-end: span R 2;
  grid-column-start: col-A 3;
  grid-column-end: span 2 col-A;
}
.three {
  grid-row-start: 9;
  grid-column-start: col-A -2;
}
```

<Figures figure="13-35">Attaching elements to named grid lines</Figures>

Notice how `span` changes when we add a name: where we said `span 2 col-A`, that caused the grid item to span from its starting point (the third `col-A`) across another `col-A` and end at the `col-A` after that. This means the grid item actually spans four column tracks, since `col-A` appears on every other column grid line.

> 注意，当我们添加一个名称时，' span '是如何变化的:在这里我们说' span 2 ' - a '，这导致网格项从它的起点(第三个' - a ')跨越另一个' - a '，然后在' - a '结束。这意味着网格项目实际上跨越了四个列轨道，因为‘col-A’出现在每隔一个列网格线上。

Again, negative numbers count backward from the end of a sequence, so `col-A -2` gets us the second-from-last instance of a grid line named `col-A`. Because there are no end-line values declared for `.three`, they’re both set to `span 1`. That means the following is exactly equivalent to the `.three` in the previous example:

> 同样，负数从序列的末尾开始倒数，因此“cola -2”为我们提供了名为“cola”的网格线的倒数第二个实例。因为没有为'声明结束行值。3 '它们都被设置成'张成空间 1 '这意味着下面的式子与'完全等价。在前面的例子中:

```css
.three {
  grid-row-start: 9;
  grid-row-end: span 1;
  grid-column-start: col-A -2;
  grid-row-end: span 1;
}
```

There’s an alternative way to use names with named grid lines—specifically, the named grid lines that are implicitly created by grid areas. For example, consider the following styles, illustrated in Figure 13-36:

> 有一种方法可以将名称与指定的网格线一起使用——具体来说，就是由网格区域隐式创建的指定网格线。例如，考虑下面的样式，如图 13-36 所示:

```css
grid-template-areas:
  "header header header header"
  "leftside content content rightside"
  "leftside footer footer footer";
#masthead {
  grid-row-start: header;
  grid-column-start: header;
  grid-row-end: header;
}
#sidebar {
  grid-row-start: 2;
  grid-row-end: 4;
  grid-column-start: leftside / span 1;
}
#main {
  grid-row-start: content;
  grid-row-end: content;
  grid-column-start: content;
}
#navbar {
  grid-row-start: rightside;
  grd-row-end: 3;
  grid-column-start: rightside;
}
#footer {
  grid-row-start: 3;
  grid-row-end: span 1;
  grid-column-start: footer;
  grid-row-end: footer;
}
```

<Figures figure="13-36">Another way of attaching elements to named grid lines</Figures>

What happens if you supply a custom identifier (i.e., a name you defined) is that the browser looks for a grid line with that name `plus` either `-start` or `-end` added on, depending on whether you’re assigning a start line or an end line. Thus, the following are equivalent:

> 如果你提供一个自定义标识符会发生什么?，您定义的名称)是浏览器查找名称为“+”或“-start”或“-end”的网格线，取决于您是分配起始线还是结束线。因此，以下是等价的:

```css
grid-column-start: header;
grid-column-end: header;
grid-column-start: header-start;
grid-column-end: header-end;
```

This works because, as was mentioned with `grid-template-areas`, explicitly creating a grid area implicitly creates the named `-start` and `-end` grid lines that surround it.

> 这是因为，正如“网格模板-区域”中提到的，显式地创建一个网格区域将隐式地创建包围它的命名为“-start”和“-end”的网格线。

The final value possibility, `auto`, is kind of interesting. According to the Grid Layout specification, if one of the grid-line start/end properties is set to `auto`, that indicates “auto-placement, an automatic span, or a default span of one.” In practice, what this tends to mean is that the grid line that gets picked is governed by the `grid flow`, a concept we have yet to cover (but will soon!). For a start line, `auto` usually means that the next available column or row line will be used. For an end line, `auto` usually means a one-cell span. In both cases, the word “usually” is used intentionally: as with any automatic mechanism, there are no absolutes.

> 最后一个值，auto，很有趣。根据网格布局规范，如果其中一个网格线开始/结束属性设置为“auto”，表示“自动放置、自动跨度或默认跨度为 1”。“在实践中，这往往意味着被选中的网格线是由‘网格流’控制的，这个概念我们还没有涉及(但很快就会涉及!)对于起始行，“auto”通常意味着将使用下一个可用的列或行行。对于结束行，“auto”通常表示一个单元格。在这两种情况下，“通常”这个词都是有意使用的:就像任何自动机制一样，没有绝对原则。

### 13.4.2 行和列的简写属性

There are two shorthand properties that allow you to more compactly attach an element to grid lines.

> 有两个简写属性允许您更紧密地将元素附加到网格线。

<!-- <Cards cards="grid-row_grid-column" /> -->

The primary benefit of these properties is that they make it a lot simpler to declare the start and end grid lines to be used for laying out a grid item. For example:

> 这些属性的主要好处是，它们使声明用于布局网格项的起始和结束网格线变得简单得多。例如:

```css
#grid {
  display: grid;
  grid-template-rows: repeat(10, [R] 1.5em);
  grid-template-columns: 2em repeat(5, [col-A] 5em [col-B] 5em) 2em;
}
.one {
  grid-row: R 3 / 7;
  grid-column: col-B / span 2;
}
.two {
  grid-row: R / span R 2;
  grid-column: col-A 3 / span 2 col-A;
}
.three {
  grid-row: 9;
  grid-column: col-A -2;
}
```

That’s a whole lot easier to read than having each start and end value in its own property, honestly. Other than being more compact, the behavior of these properties is more or less what you’d expect. If you have two bits separated by a solidus, the first part defines the starting grid line, and the second part defines the ending grid line. If you have only one value with no solidus, it defines the starting grid line. The ending grid line depends on what you said for the starting line. If you supply a name for the starting grid line, then the ending grid line is given that same name. Thus, the following are equivalent:

> 坦白地说，这比将每个开始值和结束值放在自己的属性中要容易得多。除了更紧凑之外，这些属性的行为或多或少是您所期望的。如果有两个位由一个 solidus 分隔，第一部分定义起始网格线，第二部分定义结束网格线。如果只有一个没有 solidus 的值，它将定义起始网格线。结束的网格线取决于你说的起始线。如果您为起始网格线提供一个名称，那么结束网格线将被赋予相同的名称。因此，以下是等价的:

```css
grid-column: col-B;
grid-column: col-B / col-B;
```

That will span from one instance of that grid-line name to the next, regardless of how many grid cells are spanned.

> 它将从网格线名称的一个实例跨越到下一个实例，而不管跨越了多少网格单元格。

If a single number is given, then the second number (the end line) is set to `auto`. That means the following pairs are equivalent:

> 如果给定一个数字，那么第二个数字(结束行)被设置为“auto”。这意味着下列配对是等价的:

```css
grid-row: 2;
grid-row: 2 / auto;
grid-column: header;
grid-column: header / header;
```

There’s a subtle behavior built into the handling of grid-line names in `grid-row` and `grid-column` that pertains to implicitly named grid lines. If you recall, defining a named grid area creates `-start` and `-end` grid lines. That is, given a grid area with a name of `footer`, there are implicitly created `footer-start` grid lines to its top and left, and `footer-end` grid lines to its bottom and right.

> 在处理“网格行”和“网格列”中的网格行名称时，内置了一个微妙的行为，它属于隐式命名的网格行。如果您还记得，定义一个命名的网格区域会创建“-start”和“-end”网格线。也就是说，给定一个名为“footer”的网格区域，它的顶部和左侧会隐式地创建“footer-start”网格线，底部和右侧会创建“footer-end”网格线。

In that case, if you refer to those grid lines by the area’s name, the element will still be placed properly. Thus, the following styles have the result shown in Figure 13-37:

> 在这种情况下，如果您通过区域的名称引用这些网格线，元素仍然会被正确放置。因此，以下样式的结果如图 13-37 所示:

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
  grid-template-rows: auto 1fr auto;
  grid-template-columns: 25% 75%;
}
#header {
  grid-row: header / header;
  grid-column: header;
}
#footer {
  grid-row: footer;
  grid-column: footer-start / footer-end;
}
```

<Figures figure="13-37">Attaching to implicit grid lines via grid-area names</Figures>

You can always explicitly refer to the implicitly named grid lines, but if you just refer to the grid area’s name, things still work out. If you refer to a grid-line name that doesn’t correspond to a grid area, then it falls back to the behavior discussed previously. In detail, it’s the same as saying `line-name 1`, so the following two are equivalent:

> 您总是可以显式地引用隐式命名的网格线，但是如果只引用网格区域的名称，那么仍然可以解决问题。如果您引用的网格线名称与网格区域不对应，那么它将返回到前面讨论的行为。在细节上，它相当于说`line-name 1`，所以下面两个是等价的:

```css
grid-column: jane / doe;
grid-column: jane 1 / doe 1;
```

This is why it’s risky to name grid lines the same as grid areas. Consider the following:

```css
grid-template-areas:
  "header header"
  "sidebar content"
  "footer footer"
  "legal legal";
grid-template-rows: auto 1fr [footer] auto [footer];
grid-template-columns: 25% 75%;
```

This explicitly sets grid lines named `footer` above the “footer” row and below the “legal” row…and now there’s trouble ahead. Suppose we add this:

> 它显式地将名为“footer”的网格线设置在“footer”行之上、“legal”行之下……现在前面有麻烦了。假设我们加上这个:

```css
#footer {
  grid-column: footer;
  grid-row: footer;
}
```

For the column lines, there’s no problem. `footer` gets expanded to `footer / footer`. The browser looks for a grid area with that name and finds it, so it translates `footer / footer` to `footer-start / footer-end`. The `#footer` element is attached to those implicit grid lines.

> 对于列行，没有问题。' footer '被扩展为' footer / footer '。浏览器会查找具有该名称的网格区域并找到它，因此它将“footer / footer”转换为“footer-start / footer-end”。' #footer '元素附加到这些隐式网格线。

For `grid-row`, everything starts out the same. `footer` becomes `footer / footer`, which is translated to `footer-start / footer-end`. But that means the `#footer` will only be as tall as the “footer” row. It will `not` stretch to the second explicitly named `footer` grid line below the “legal” row, because the translation of `footer` to `footer-end` (due to the match between the grid-line name and the grid-area name) takes precedence.

> 对于“grid-row”来说，所有东西一开始都是一样的。“footer”变成了“footer / footer”，翻译成“footer-start / footer-end”。但这意味着“#footer”将只与“footer”行一样高。它将“不”延伸到“合法”行下面的第二个显式命名为“footer”的网格线，因为将“footer”转换为“footer-end”(由于网格线名称和网格区域名称之间的匹配)优先。

The upshot of all this: it’s generally a bad idea to use the same name for grid areas and grid lines. You might be able to get away with it in some scenarios, but you’re almost always better off keeping your line and area names distinct, so as to avoid tripping over name-resolution conflicts.

> 所有这些的结果是:对网格区域和网格线使用相同的名称通常是一个坏主意。在某些情况下，您可能不需要这样做，但是最好保持行名和区域名是不同的，这样可以避免出现名称解析冲突。

### 13.4.3 隐式栅格

Up to this point, we’ve concerned ourselves solely with explicitly defined grids: we’ve talked about the row and column tracks we define via properties like `grid-template-columns`, and how to attach grid items to the cells in those tracks.

> 到目前为止，我们只关心显式定义的网格:我们讨论了通过诸如“网格模板-列”之类的属性定义的行和列轨迹，以及如何将网格项附加到这些轨迹中的单元格。

But what happens if we try to place a grid item, or even just part of a grid item, beyond that explicitly created grid? For example, consider the following grid:

> 但是，如果我们试图在显式创建的网格之外放置一个网格项，甚至只是网格项的一部分，会发生什么?例如，考虑以下网格:

```css
#grid {
  display: grid;
  grid-template-rows: 2em 2em;
  grid-template-columns: repeat(6, 4em);
}
```

Two rows, six columns. Simple enough. But suppose we define a grid item to sit in the first column and go from the first grid line to the fourth:

> 两行，六列。很简单。但是假设我们定义了一个网格项，它位于第一列，并从第一个网格线移动到第四个网格线:

```css
.box01 {
  grid-column: 1;
  grid-row: 1 / 4;
}
```

Now what? There are only two rows bounded by three grid lines, and we’ve told the browser to go beyond that, from row line 1 to row line 4.

> 现在怎么办呢?只有两行以三条网格线为界，我们已经告诉浏览器超出这一范围，从行 1 到行 4。

What happens is that another row line is created to handle the situation. This grid line, and the new row track it creates, are both part of the implicit grid. Here are a few examples of grid items that create implicit grid lines (and tracks) and how they’re laid out (see Figure 13-38):

> 所发生的是创建另一行来处理这种情况。此网格线及其创建的新行跟踪都是隐式网格的一部分。以下是一些创建隐式网格线(和轨迹)的网格项示例，以及它们的布局方式(参见图 13-38):

```css
.box01 {
  grid-column: 1;
  grid-row: 1 / 4;
}
.box02 {
  grid-column: 2;
  grid-row: 3 / span 2;
}
.box03 {
  grid-column: 3;
  grid-row: span 2 / 3;
}
.box04 {
  grid-column: 4;
  grid-row: span 2 / 5;
}
.box05 {
  grid-column: 5;
  grid-row: span 4 / 5;
}
.box06 {
  grid-column: 6;
  grid-row: -1 / span 3;
}
.box07 {
  grid-column: 7;
  grid-row: span 3 / -1;
}
```

<Figures figure="13-38">Creating implicit grid lines and tracks</Figures>

There’s a lot going on there, so let’s break it down. First off, the explicit grid is represented by the light-gray box behind the various numbered boxes; all the dashed lines represent the implicit grid.

> 这里有很多东西，让我们把它分解一下。首先，显式网格由各种编号的方框后面的浅灰色方框表示;所有虚线表示隐式网格。

So, what about those numbered boxes? `box1` adds an extra grid line after the end of the explicit grid, as we discussed before. `box2` starts on the last line of the explicit grid, and spans forward two lines, so it adds yet another implicit grid line. `box3` ends on the last explicit grid line (line 3) and spans `back` two lines, thus starting on the first explicit grid line.

> 那么，那些编号的盒子呢?如前所述，“box1”在显式网格结束后添加了一条额外的网格线。“box2”从显式网格的最后一行开始，向前跨越两行，因此它又添加了一条隐式网格线。“box3”以最后一个显式网格线结束(第 3 行)，跨越“back”两行，因此从第一个显式网格线开始。

`box4` is where things really get interesting. It ends on the fifth row line, which is to say the second implicit grid line. It spans back three lines—and yet, it still starts on the same grid line as `box3`. This happens because spans have to start counting within the explicit grid. Once they start, they can continue on into the implicit grid (as happened with `box2`), but they `cannot` start counting within the implicit grid.

> “box4”是真正让事情变得有趣的地方。它在第 5 行结束，也就是第二个隐式网格线。它跨越了三条线——但它仍然从与《box3》相同的网格线开始。这是因为 span 必须在显式网格中开始计算。一旦开始，它们可以继续进入隐式网格(就像“box2”那样)，但是它们“不能”在隐式网格中开始计数。

Thus, `box4` ends on row-line 5, but its span starts with grid-line 3 and counts back two lines (`span 2`) to arrive at line 1. Similarly, `box5` ends on line 5, and spans back four lines, which means it starts on row-line –2. Remember: span counting must `start` in the explicit grid. It doesn’t have to end there.

> 因此，“box4”在第 5 行结束，但是它的 span 从第 3 行开始，并返回两行(“span 2”)，到达第 1 行。类似地，“box5”在第 5 行结束，向后跨越 4 行，这意味着它从第 2 行开始。请记住:span 计数必须在显式网格中“开始”。事情不必到此为止。

After those, `box6` starts on the last explicit row line (line 3), and spans out to the sixth row line—adding yet another implicit row line. The point of having it here is to show that negative grid-line references are with respect to the explicit grid, and count back from its end. They do `not` refer to negatively indexed implicit lines that are placed before the start of the explicit grid.

> 之后，“box6”从最后一个显式行行(第 3 行)开始，扩展到第六行行——添加另一个隐式行行。在这里使用它的目的是为了显示负网格线引用是相对于显式网格的，并从其末端开始计数。它们“不”指的是放在显式网格开始之前的带负索引的隐式行。

If you want to start an element on an implicit grid line before the explicit grid’s start, then the way to do that is shown by `box7`: put its end line somewhere in the explicit grid, and span back past the beginning of the explicit grid. And you may have noticed: `box7` occupies an implicit column track. The original grid was set up to create six columns, which means seven column lines, the seventh being the end of the explicit grid. When `box7` was given `grid-column: 7`, that was equivalent to `grid-column: 7 / span 1` (since a missing end line is always assumed to be `span 1`). That necessitated the creation of an implicit column line in order to hold the grid item in the implicit seventh column.

> 如果您想要在显式网格开始之前在隐式网格线上开始一个元素，那么方法是' box7 ':将它的结束线放在显式网格的某个地方，并跨越回显式网格的开始。您可能已经注意到:“box7”占用了一个隐式的列跟踪。最初的网格被设置为创建 6 个列，这意味着 7 个列行，第七行是显式网格的结束。当' box7 '被赋予' grid-column: 7 '时，它等价于' grid-column: 7 / span 1 '(因为丢失的结束行总是被假定为' span 1 ')。这就需要创建一个隐式的列行，以便在隐式的第七列中保存网格项。

Now let’s take those principles and add named grid lines to the mix. Consider the following, illustrated in Figure 13-39:

> 现在让我们采用这些原则并将命名网格线添加到混合中。考虑如下图 13-39 所示:

```css
#grid {
  display: grid;
  grid-template-rows: [begin] 2em [middle] 2em [end];
  grid-template-columns: repeat(5, 5em);
}
.box01 {
  grid-column: 1;
  grid-row: 2 / span end 2;
}
.box02 {
  grid-column: 2;
  grid-row: 2 / span final;
}
.box03 {
  grid-column: 3;
  grid-row: 1 / span 3 middle;
}
.box04 {
  grid-column: 4;
  grid-row: span begin 2 / end;
}
.box05 {
  grid-column: 5;
  grid-row: span 2 middle / begin;
}
```

What you can see at work there, in several of the examples, is what happens with grid-line names in the implicit grid: every implicitly created line has the name that’s being hunted. Take `box2`, for example. It’s given an end line of `final`, but there is no line with that name. Thus the span-search goes to the end of the explicit grid and, having not found the name it’s looking for, creates a new grid line, to which it attaches the name `final`. (In Figure 13-39, the implicitly-created line names are italicized and faded out a bit.)

> 在一些示例中，您可以看到隐式网格中的网格行名称:每个隐式创建的行都有被搜索的名称。以“box2”为例。它有一个“final”的结束行，但是没有与这个名字相关的行。因此，span-search 将转到显式网格的末尾，在没有找到要查找的名称之后，创建一个新的网格线，并将名称“final”附加到其中。(在图 13-39 中，隐式创建的行名称用斜体显示，并略为淡出。)

<Figures figure="13-39">Named implicit grid lines and tracks</Figures>

Similarly, `box3` starts on the first explicit row line, and then needs to span three `middle` named lines. It searches forward and finds one, then goes looking for the other two. Not finding any, it attaches the name `middle` to the first implicit grid line, and then does the same for the second implicit grid line. Thus, it ends two implicit grid lines past the end of the explicit grid.

> 类似地，“box3”从第一个显式行开始，然后需要跨越三个“中间”命名行。它向前搜索，找到一个，然后去寻找另外两个。没有找到任何，它将名称“middle”附加到第一个隐式网格线，然后对第二个隐式网格线执行相同的操作。因此，它结束了两个隐式网格线，超过了显式网格的结束。

The same sort of thing happens with `box4` and `box5`, except working backward from endpoints. `box4` ends with the end line (line 3), then spans back to the second `begin` line it can find. This causes an implicit line to be created before the first line, named `begin`. `box 5` spans back from `begin` (the explicitly labeled `begin`) to the second `middle` it can find. Since it can’t find any, it labels two implcit lines `middle` and ends at the one furthest from where it started looking.

> 类似的事情也会发生在“box4”和“box5”上，除了从端点反向工作。“box4”以结束行(第 3 行)结束，然后跨越回它能找到的第二个“开始”行。这将导致在第一行之前创建一个隐式行，名为“begin”。“box 5”从“begin”(明确标记为“begin”)一直延伸到它能找到的第二个“middle”。由于找不到任何线索，它将两条线索标为“中间”，并在离它开始寻找的地方最远的地方结束。

When you get right down to it, the implicit grid is a delightfully baroque fallback mechanism. It’s generally best practice to stick to the explicit grid, and to make sure the explicit grid covers everything you want to do. If you find you need another row, don’t just run off the edge of the grid—adjust your grid template’s values instead!

> 当你开始着手时，隐含的网格是一种令人愉快的巴洛克式后退机制。通常，最好的实践是坚持使用显式网格，并确保显式网格涵盖您想要做的所有事情。如果您发现您需要另一行，不要仅仅从网格边缘运行—而是调整您的网格模板的值!

### 13.4.4 错误处理

There are a few cases that need to be covered, as they fall under the general umbrella of “what grids do when things go pear-shaped.”

> 有一些情况是需要覆盖的，因为它们属于“当事情变得梨形时网格会做什么”的一般范畴。

First, what if you accidentally put the start line after the end line? Say, something like this:

> 首先，如果你不小心把起始线放在了结束线之后怎么办?比如说:

```css
grid-row-start: 5;
grid-row-end: 2;
```

All that happens is probably what was meant in the first place: the values are swapped. Thus, you end up with this:

> 所发生的一切可能就是最初的含义:交换值。因此，您最终得到以下结果:

```css
grid-row-start: 2;
grid-row-end: 5;
```

Second, what if both the start and the end lines are declared to be spans of some variety? For example:

> 其次，如果起始线和结束线都被声明为某种类型的跨度，该怎么办?例如:

```css
grid-column-start: span;
grid-column-end: span 3;
```

If this happens, the end value is dropped and replaced with auto. That means you’d end up with this:

> 如果发生这种情况，则将结束值删除并替换为 auto。这意味着你最终会得到这个:

```css
grid-column-start: span; /* 'span' is equal to 'span 1' */
grid-column-end: auto;
```

That would cause the grid item to have its ending edge placed automatically, according to the current grid flow (a subject we’ll soon explore), and the starting edge to be placed one grid line earlier. Third, what if the only thing directing placement of the grid item is a named span? In other words:

> 这将导致根据当前网格流(我们将很快讨论的主题)自动放置网格项的结束边缘，并将开始边缘放置在更早的网格线上。第三，如果指导网格项目放置的惟一东西是一个名为 span 的空间，该怎么办?换句话说:

```css
grid-row-start: span footer;
grid-row-end: auto;
```

This is not permitted, so the `span footer` in this case is replaced with `span 1`.

> 这是不允许的，所以本例中的 `span footer` 被替换为 `span 1`。

### 13.4.5 使用区域

Attaching by row lines and column lines is great, but what if you could refer to a grid area with a single property? Behold: `grid-area`.

<!-- <Cards cards="grid-area" /> -->

Let’s start with the easier use of `grid-area`: assigning an element to a previously defined grid area. Makes sense, right? Let’s bring back our old friend `grid-template-areas`, put it together with `grid-area` and some markup, and see what magic results (as shown in Figure 13-40):

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header header header"
    "leftside content content rightside"
    "leftside footer footer footer";
}
#masthead {
  grid-area: header;
}
#sidebar {
  grid-area: leftside;
}
#main {
  grid-area: content;
}
#navbar {
  grid-area: rightside;
}
#footer {
  grid-area: footer;
}
```

```html
<div id="grid">
  <div id="masthead">…</div>
  <div id="main">…</div>
  <div id="navbar">…</div>
  <div id="sidebar">…</div>
  <div id="footer">…</div>
</div>
```

<Figures figure="13-40">Assigning elements to grid areas</Figures>

That’s all it takes: set up some named grid areas to define your layout, and then drop grid items into them with `grid-area`. So simple, and yet so powerful.

As you might have noticed, the sizing of the column and row tracks was omitted from that CSS. This was done entirely for clarity’s sake. In an actual design, the rule probably would look more like this:

```css
grid-template-areas:
  "header header header header"
  "leftside content content rightside"
  "leftside footer footer footer";
grid-template-rows: 200px 1fr 3em;
grid-template-columns: 20em 1fr 1fr 10em;
```

There is another way to use `grid-area` that refers to grid lines instead of grid areas. Fair warning: it’s likely to be confusing at first, for a couple of reasons.

Here’s an example of a grid template that defines some grid lines, and some `grid-area` rules that reference the lines, as illustrated in Figure 13-41:

```css
#grid {
  display: grid;
  grid-template-rows: [r1-start] 1fr [r1-end r2-start] 2fr [r2-end];
  grid-template-columns: [col-start] 1fr [col-end main-start] 1fr [main-end];
}
.box01 {
  grid-area: r1 / main / r1 / main;
}
.box02 {
  grid-area: r2-start / col-start / r2-end / main-end;
}
.box03 {
  grid-area: 1 / 1 / 2 / 2;
}
```

<Figures figure="13-41">Assigning elements to grid lines</Figures>

As you can see, the elements were placed as directed. Note the ordering of the gridline values, however. They’re listed in the order `row-start`, `column-start`, `row-end`, `column-end`. If you diagram that in your head, you’ll quickly realize that the values go anticlockwise around the grid item—the exact opposite of the TRBL (Top, Right, Bottom, Left) pattern we’re used to from margins, padding, borders, and so on. Further more, this means the column and row references are not grouped together, but are instead split up.

Yes, this is intentional. No, I don’t know why.

If you supply fewer than four values, the missing values are taken from those you do supply. If there are only three values, then the missing `grid-column-end` is the same as `grid-column-start` if it’s a name; if the start line is a number, the end line is set to `auto`. The same holds true if you give only two values, except that the now-missing `grid-row-end` is copied from `grid-row-start` if it’s a name; otherwise, it’s set to `auto`.

From that, you can probably guess what happens if only one value is supplied: if it’s a name, use it for all four values; if it’s a number, the rest are set to `auto`.

This one-to-four replication pattern is actually how giving a single grid-area name translates into having the grid item fill that area. The following are equivalent:

```css
grid-area: footer;
grid-area: footer / footer / footer / footer;
```

Now recall the behavior discussed in the previous section about `grid-column` and `grid-row`: if a grid line’s name matches the name of a grid area, then it’s translated into a `-start` or `-end` variant, as appropriate. That means the previous example is translated to the following:

```css
grid-area: footer-start / footer-start / footer-end / footer-end;
```

And that’s how a single grid-area name causes an element to be placed into the corresponding grid area.

### 13.4.6 栅格元素重叠

One thing we’ve been very careful to do in our grid layouts thus far is to avoid overlap. Rather like positioning, it’s absolutely (get it?) possible to make grid items overlap each other. Let’s take a simple case, illustrated in Figure 13-42:

```css
#grid {
  display: grid;
  grid-template-rows: 50% 50%;
  grid-template-columns: 50% 50%;
}
.box01 {
  grid-area: 1 / 1 / 2 / 3;
}
.box02 {
  grid-area: 1 / 2 / 3 / 2;
}
```

<Figures figure="13-42">Overlapping grid items</Figures>

Thanks to the grid numbers that were supplied, the two grid items overlap in the upper-right grid cell. Which is on top of the other depends on the layering behavior discussed later, but for now, just take it as given that they do layer when overlapping.

Overlap isn’t restricted to situations involving raw grid numbers. In the following case, the sidebar and the footer will overlap, as shown in Figure 13-43. (Assuming the footer comes later than the sidebar in the markup, then in the absence of other styles, the footer will be on top of the sidebar.)

```css
#grid {
  display: grid;
  grid-template-areas:
    "header header"
    "sidebar content"
    "footer footer";
}
#header {
  grid-area: header;
}
#sidebar {
  grid-area: sidebar / sidebar / footer-end / sidebar;
}
#footer {
  grid-area: footer;
}
```

<Figures figure="13-43">Overlapping sidebar and footer</Figures>

I bring this up in part to warn you about the possibility of overlap, and also to serve as a transition to the next topic. It’s a feature that sets grid layout apart from positioning, in that it can sometimes help avoid overlap: the concept of `grid flow`.

## 13.5 栅格流

For the most part, we’ve been explicitly placing grid items on the grid. If items aren’t explicitly placed, then they’re automatically placed into the grid. Following the grid flow in effect, an item is placed in the first area that will fit it. The simplest case is just filling a grid track in sequence, one grid item after another, but things can get a lot more complex than that, expecially if there is a mixture of explicitly and automatically placed grid items—the latter must work around the former.

There are primarily two grid-flow models, `row-first` and `column-first`, though you can enhance either by specifying a `dense` flow. All this is done with the property `gridauto-flow`.

<!-- <Cards cards="grid-auto-flow" /> -->

To see how these values work, consider the following markup:

```html
<ol id="grid">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
</ol>
```

To that markup, let’s apply the following styles:

```css
#grid {
  display: grid;
  width: 45em;
  height: 8em;
  grid-auto-flow: row;
}
#grid li {
  grid-row: auto;
  grid-column: auto;
}
```

Assuming a grid with a column line every 15 ems and a row line every 4 ems, we get the result shown in Figure 13-44.

<Figures figure="13-44">Row-oriented grid flow</Figures>

This probably seems pretty normal, the same sort of thing you’d get if you floated all the boxes, or if all of them were inline blocks. That’s why `row` is the default value. Now, let’s try switching the `grid-auto-flow` value to `column`, as shown in Figure 13-45:

```css
#grid {
  display: grid;
  width: 45em;
  height: 8em;
  grid-auto-flow: column;
}
#grid li {
  grid-row: auto;
  grid-column: auto;
}
```

So with `grid-auto-flow: row`, each row is filled in before starting on the next row. With `grid-auto-flow: column`, each column is filled first.

<Figures figure="13-45">Column-oriented grid flow</Figures>

What needs to be stressed here is that the list items weren’t explicitly sized. By default, they were resized to attach to the defined grid lines. This can be overridden by assigning explicit sizing to the elements. For example, if we make the list items be 7 ems wide and 1.5 ems tall, we’ll get the result shown in Figure 13-46:

```css
#grid {
  display: grid;
  width: 45em;
  height: 8em;
  grid-auto-flow: column;
}
#grid li {
  grid-row: auto;
  grid-column: auto;
  width: 7em;
  height: 1.5em;
}
```

<Figures figure="13-46">Explicitly sized grid items</Figures>

If you compare that to the previous figure, you’ll see that the corresponding grid items start in the same place in each figure; they just don’t end in the same places. This illustrates that what’s really placed in grid flow is grid areas, to which the grid items are then attached.

This is important to keep in mind if you auto-flow elements that are wider than their assigned column or taller than their assigned row, as can very easily happen when turning images or other intrinsically sized elements into grid items. Let’s say we want to put a bunch of images, each a different size, into a grid that’s set up to have a column line every 50 horizontal pixels, and a row line every 50 vertical pixels. This grid is illustrated in Figure 13-47, along with the results of flowing a series of images into that grid by either row or column:

```css
#grid {
  display: grid;
  grid-template-rows: repeat(3, 50px);
  grid-template-columns: repeat(4, 50px);
  grid-auto-rows: 50px;
  grid-auto-columns: 50px;
}
img {
  grid-row: auto;
  grid-column: auto;
}
```

<Figures figure="13-47">Flowing images in grids</Figures>

Notice how some of the images overlap others? That’s because each image is attached to the next grid line in the flow, without taking into account the presence of other grid items. We didn’t set up images to span more than one grid track when they needed it, so overlap occurred.

This can be managed with class names or other identifiers. We could class images as `tall` or `wide` (or both) and specify that they get more grid tracks. Here’s some CSS to add to the previous example, with the result shown in Figure 13-48:

```css
img.wide {
  grid-column: auto / span 2;
}
img.tall {
  grid-row: auto / span 2;
}
```

<Figures figure="13-48">Giving images more track space</Figures>

This does cause the images to keep spilling down the page, but there’s no overlapping. However, notice how there are gaps in that last grid? That happened because the placement of some grid items across grid lines didn’t leave enough room for other items in the flow. In order to illustrate this, and the two flow patterns, more clearly, let’s try an example with numbered boxes (Figure 13-49).

<Figures figure="13-49">Illustrating flow patterns</Figures>

Follow across the rows of the first grid, counting along with the numbers. In this particular flow, the grid items are laid out almost as if they were leftward floats. Almost, but not quite: notice that grid item 13 is actually to the left of grid item 11. That would never happen with floats, but it can with grid flow. The way row flow (if we may call it that) works is that you go across each row from left to right, and if there’s room for a grid item, you put it there. If a grid cell has been occupied by another grid item, you skip over it. So the cell next to item 10 didn’t get filled, because there wasn’t room for item 11. Item 13 went to the left of item 11 because there was room for it there when the row was reached.

The same basic mechanisms hold true for column flow, except in this case you work from top to bottom. Thus, the cell below item 9 is empty because item 10 wouldn’t fit there. It went into the next column and spanned four grid cells. The items after it, since they were just one grid cell in size, filled in the cells after it in column order.

<Tips tips="blue">Grid flow works left-to-right, top-to-bottom in languages that have that writing pattern. In right-to-left languages, such as Arabic and Hebrew, the row-oriented flow would be right-to-left, not left-toright.</Tips>

If you were just now wishing for a way to pack grid items as densely as possible, regardless of how that affected the ordering, good news: you can! Just add the keyword `dense` to your `grid-auto-flow` value, and that’s exactly what will happen. We can see the result in Figure 13-50, which shows the results of `grid-auto-flow: row dense` and `grid-auto-flow: dense column` side by side.

<Figures figure="13-50">Illustrating dense flow patterns</Figures>

In the first grid, item 12 appears in the row above item 11 because there was a cell that fit it. For the same reason, item 11 appears to the left of item 10 in the second grid.

In effect, what happens with `dense` grid flow is that for each grid item, the browser scans through the `entire` grid in the given flow direction (`row` or `column`), starting from the flow’s starting point (the top-left corner, in LTR—left-to-right—languages), until it finds a place where that grid item will fit. This can make things like photo galleries more compact, and works great as long as you don’t have a specific order in which the images need to appear.

Now that we’ve explored grid flow, I have a confession to make: in order to make the last couple of grid items look right, I included some CSS that I didn’t show you. Without it, the items hanging off the edge of the grid would have looked quite a bit different than the other items—much shorter in row-oriented flow, and much narrower in column-oriented flow. We’ll see why, and the CSS I used, in the next section.

## 13.6 自动增加栅格线

So far, we’ve almost entirely seen grid items placed into a grid that was explicitly defined. But in the last section we had situations where grid items ran off the edge of the explicitly defined grid. What happens when a grid item goes off the edge? Rows or columns are added as needed to satisfy the layout directives of the items in question (see “The Implicit Grid” on page 694). So, if an item with a row span of `3` is added after the end of a row-oriented grid, three new rows are added after the explicit grid.

By default, these automatically added rows are the absolute minimum size needed. If you want to exert a little more control over their sizing, then `grid-auto-rows` and `grid-auto-columns` are for you.

<!-- <Cards cards="grid-auto-rows_grid-auto-columns" /> -->

For any automatically created row or column tracks, you can provide a single track size or a minmaxed pair of track sizes. Let’s take a look at a reduced version of the grid-flow example from the previous section: we’ll set up a 2 × 2 grid, and try to put five items into it. In fact, let’s do it twice: once with `grid-auto-rows`, and once without, as illustrated in Figure 13-51:

```css
.grid {
  display: grid;
  grid-template-rows: 80px 80px;
  grid-template-columns: 80px 80px;
}
#g1 {
  grid-auto-rows: 80px;
}
```

As you can see, without sizing the automatically created row, the grid item is placed in a row that’s exactly as tall as the grid item’s content, and not a pixel more. It’s still just as wide as the column into which it’s placed, because that has a size (`80px`). The row, lacking an explicit height, defaults to `auto`, with the result shown.

<Figures figure="13-51">Grids with and without auto-row sizing</Figures>

If we flip it around to columns, the same basic principles apply (see Figure 13-52):

```css
.grid {
  display: grid;
  grid-auto-flow: column;
  grid-template-rows: 80px 80px;
  grid-template-columns: 80px 80px;
}
#g1 {
  grid-auto-columns: 80px;
}
```

<Figures figure="13-52">Grids with and without auto-column sizing</Figures>

In this case, because the flow is column-oriented, the last grid item is placed into a new column past the end of the explicit grid. In the second grid, where there’s no `grid-auto-columns`, that fifth item is as tall as its row (`80px`), but has an `auto` width, so it’s just as wide as it needs to be and no wider. If a sixth item were added and it had wider content, then the column would be sized to fit that content, thus widening the fifth item.

So now you know what I used in the `grid-auto-flow` figures in the previous section: I silently made the auto-rows and auto-columns the same size as the explicitly sized columns, in order to not have the last couple of items look weird. Let’s bring back one of those figures, only this time the `grid-auto-rows` and `grid-auto-columns` styles will be removed. As you can see in Figure 13-53, the last few items in each grid are shorter or narrower than the rest, due to the lack of auto-track sizing.

<Figures figure="13-53">A previous figure with auto-track sizing removed</Figures>

And now you know…the rest of the story.

## 13.7 grid简写属性

At long last, we’ve come to the shorthand property grid. It might just surprise you, though, because it’s not like other shorthand properties.

<!-- <Cards cards="grid" /> -->

The syntax is a little bit migraine-inducing, I admit, but we’ll step through it a piece at a time.

Let’s get to the elephant in the room right away: `grid` allows you to either define a grid template `or` to set the grid’s flow and auto-track sizing in a compact syntax. You can’t do both at the same time.

Furthermore, whichever you don’t define is reset to its defaults, as is normal for a shorthand property. So if you define the grid template, then the flow and auto tracks will be returned to their default values. This includes grid gutters, a topic we haven’t even covered yet. You can’t set the gutters with `grid`, but it will reset them anyway.

Yes, this is intentional. No, I don’t know why.

So let’s talk about creating a grid template using `grid`. The values can get fiendishly complex, and take on some fascinating patterns, but can be very handy. As an example, the following rule is equivalent to the set of rules that follows it:

```css
grid:
  "header header header header" 3em
  ". content sidebar ." 1fr
  "footer footer footer footer" 5em /
  2em 3fr minmax(10em, 1fr) 2em;
grid-template-areas:
  "header header header header"
  ". content sidebar ."
  "footer footer footer footer";
grid-template-rows: 3em 1fr 5em;
grid-template-columns: 2em 3fr minmax(10em, 1fr) 2em;
```

Notice how the value of `grid-template-rows` is broken up and scattered around the strings of `grid-template-areas`. That’s how row sizing is handled in `grid` when you have grid-area strings present. Take those strings out, and you end up with the following:

```css
grid: 3em 1fr 5em / 2em 3fr minmax(10em, 1fr) 2em;
```

In other words, the row tracks are separated by a solidus (`/`) from the column tracks.

Remember that with `grid`, undeclared shorthands are reset to their defaults. That means the following two rules are equivalent:

```css
#layout {
  display: grid;
  grid: 3em 1fr 5em / 2em 3fr minmax(10em, 1fr) 2em;
}
#layout {
  display: grid;
  grid: 3em 1fr 5em / 2em 3fr minmax(10em, 1fr) 2em;
  grid-auto-rows: auto;
  grid-auto-columns: auto;
  grid-auto-flow: row;
}
```

Therefore, make sure your `grid` declaration comes before anything else related to defining the grid. That means that if we wanted a dense column flow, we’d write something like this:

```css
#layout {
  display: grid;
  grid: 3em 1fr 5em / 2em 3fr minmax(10em, 1fr) 2em;
  grid-auto-flow: dense column;
}
```

Now, let’s bring the named grid areas back, `and` add some extra row grid-line names to the mix. A named grid line that goes above a row track is written `before` the string, and a grid line that goes `below` the row track comes `after` the string and any track sizing. So let’s say we want to add `main-start` and `main-stop` above and below the middle row, and `page-end` at the very bottom:

```css
grid:
  "header header header header" 3em
  [main-start] ". content sidebar ." 1fr [main-stop]
  "footer footer footer footer" 5em [page-end] /
  2em 3fr minmax(10em, 1fr) 2em;
```

That creates the grid shown in Figure 13-54, with the implicitly created named grid lines (e.g., `footer-start`), along with the explicitly named grid lines we wrote into the CSS.

<Figures figure="13-54">Creating a grid with the grid shorthand</Figures>

You can see how `grid` can get very complicated very quickly. It’s a very powerful syntax, and it’s surprisingly easy to get used to once you’ve had just a bit of practice. On the other hand, it’s also easy to get things wrong and have the entire value be invalid, thus preventing the appearance of any grid at all.

For the other use of `grid`, it’s a merging of `grid-auto-flow`, `grid-auto-rows`, and `grid-auto-columns`. The following rules are equivalent:

```css
#layout {
  grid-auto-flow: dense rows;
  grid-auto-rows: 2em;
  grid-auto-columns: minmax(1em, 3em);
}
#layout {
  grid: dense rows 2em / minmax(1em, 3em);
}
```

That’s certainly a lot less typing for the same result! But once again, I have to remind you: if you write this, then all the column and row track properties will be set to their defaults. Thus, the following rules are equivalent:

```css
#layout {
  grid: dense rows 2em / minmax(1em, 3em);
}
#layout {
  grid: dense rows 2em / minmax(1em, 3em);
  grid-template-rows: auto;
  grid-template-columns: auto;
}
```

So once again, it’s important to make sure your shorthand comes before any properties it might otherwise override.

### 13.7.1 Subgrids

There’s another possible value for `grid`, which is `subgrid`. It might be used something like this:

```css
#grid {
  display: grid;
  grid: repeat(auto-fill, 2em) / repeat(10, 1% 8% 1%);
}
.module {
  display: grid;
  grid: subgrid;
}
```

What happens inside each `module` element is that its grid items (i.e., its child elements) use the grid defined by `#grid` to align themselves.

This is potentially really useful, because you can imagine having a module that spans three of its parent’s column patterns and containing child elements that are aligned to and laid out using the “master” grid. This is illustrated in Figure 13-55.

<Figures figure="13-55">Aligning subgridded items</Figures>

The problem is that, as of this writing, `subgrid` is an “at-risk” feature of grid layout, and may be dropped entirely. That’s why it rates just this small section, instead of a more comprehensive examination.

## 13.8 释放栅格空间

So far, we’ve seen a lot of grid items jammed right up against one another, with no space between them. There are a number of ways to mitigate this, as we’ll talk about in this section, starting with gutters.

### 13.8.1 栏距

Simply put, a `gutter` is a space between two grid tracks. It’s created as if by expanding the grid line between them to have actual width. It’s much like `border-spacing` in table styling—both because it creates space between grid cells and because you can set only a single spacing value for each axis, via the properties `grid-row-gap` and `gridcolumn-gap`.

<!-- <Cards cards="grid-row-gap_grid-column-gap" /> -->

Right up front: as the value syntax shows, you can supply only a length for these properties; what it’s less clear about is that the lengths must be non-negative. It’s not possible to supply a percentage, a fractional value via `fr`, nor a minmax of some sort. If you want your columns to be separated by 1 em, then it’s easy enough: `gridcolumn-gap: 1em`. That’s pretty much as fancy as it gets. All the columns in the grid will be pushed apart by 1 em, as illustrated in Figure 13-56:

```css
#grid {
  display: grid;
  grid-template-rows: 5em 5em;
  grid-template-columns: 15% 1fr 1fr;
  grid-column-gap: 1em;
}
```

<Figures figure="13-56">Creating column gutters</Figures>

In terms of sizing the tracks in a grid, gutters are treated as if they’re grid tracks. Thus, given the following styles, the fractional grid rows will each be 140 pixels tall:

```css
#grid {
  display: grid;
  height: 500px;
  grid-template-rows: 100px 1fr 1fr 75px;
  grid-row-gap: 15px;
}
```

We get 140 pixels for each fraction row’s height because there are a total of 500 pixels of height. From that, we subtract the two row tracks (100 and 75) to get 325. From that result, we subtract the three 15-pixel gutters, which totals 45 pixels; this yields 280 pixels. That divided in half (because the fractional rows have equal fractions) gets us 140 pixels each. If the gutter value were increased to `25px`, then the fractional rows would have 250 pixels to divide between them, making each 125 pixels tall.

Track sizing can be much more complicated than this; the example used all pixels because it makes the math simple. You can always mix units however you’d like, including minmaxing your actual grid tracks. This is one of the main strengths of grid layout.

<Tips tips="blue">Grid gutters can be changed from their declared size by the effects of <code>align-content</code> and <code>justify-content</code>. This will be covered in the upcoming section, “Opening Grid Spaces” on page 714.</Tips>

There is, as you might have already suspected, a shorthand that combines row and column gap lengths into a single property.

<!-- <Cards cards="grid-gap" /> -->

Not a lot more to say than that, really: supply two non-negative lengths, and you’ll have defined the row gutters and column gutters, in that order. Here’s an example, as shown in Figure 13-57:

```css
#grid {
  display: grid;
  grid-template-rows: 5em 5em;
  grid-template-columns: 15% 1fr 1fr;
  grid-gap: 12px 2em;
}
```

<Figures figure="13-57">Defining grid gutters</Figures>

### 13.8.2 栅格元素与盒模型

Now we can create a grid, attach items to the grid, and even create gutters between the grid tracks. But what happens if we style the element that’s attached to the grid with, say, margins? Or if it’s absolutely positioned? How do these things interact with the grid?

Let’s take margins first. The basic principle at work is that an element is attached to the grid by its margin edges. That means you can push the visible parts of the element
inward from the grid area it occupies by setting positive margins—and pull it outward with negative margins. For example, these styles will have the result shown in Figure 13-58:

```css
#grid {
  display: grid;
  grid-template-rows: repeat(2, 100px);
  grid-template-columns: repeat(2, 200px);
}
.box02 {
  margin: 25px;
}
.box03 {
  margin: -25px 0;
}
```

<Figures figure="13-58">Grid items with margins</Figures>

This worked as it did because the items had both their `width` and `height` set to `auto`, so they could be stretched as needed to make everything work out. If `width` and/or `height` have non-`auto` values, then they’ll end up overriding margins to make all the math work out. This is much like what happens with right and left margins when element sizing is overconstrained: eventually, one of the margins gets overridden.

Consider an element with the following styles placed into a 200-pixel-wide by 100-pixel-tall grid area:

```css
.exel {
  width: 150px;
  height: 100px;
  padding: 0;
  border: 0;
  margin: 10px;
}
```

Going across the element first, it has 10 pixels of margin to either side, and its `width` is `150px`, giving a total of 170 pixels. Something’s gotta give, and in this case it’s the right margin (in left-to-right languages), which is changed to `40px` to make everything work—10 pixels on the left margin, 150 pixels on the content box, and 40 pixels on the right margin equals the 200 pixels of the grid area’s width.

On the vertical axis, the bottom margin is reset to `-10px`. This compensates for the top margin and content height totalling 110 pixels, when the grid area is only 100 pixels tall.

<Tips tips="blue">Margins on grid items are ignored when calculating grid-track sizes. That means that no matter how big or small you make a grid item’s margins, it won’t change the sizing of a <code>min-content</code> column, for example, nor will increasing the margins on a grid item cause <code>fr</code>-sized grid tracks to change size.</Tips>

As with block layout, you can selectively use `auto` margins to decide which margin will have its value changed to fit. Suppose we wanted the grid item to align to the right of its grid area. By setting the item’s left margin to `auto`, that would happen:

```css
.exel {
  width: 150px;
  height: 100px;
  padding: 0;
  border: 0;
  margin: 10px;
  margin-left: auto;
}
```

Now the element will add up 160 pixels for the right margin and content box, and then give the difference between that and the grid area’s width to the left margin, since it’s been explicitly set to `auto`. This has the result shown in Figure 13-59, where there are 10 pixels of margin on each side of the `exel` item, except the left margin, which is (as we just calculated) 40 pixels.

<Figures figure="13-59">Using auto margins to align items</Figures>

That might seem familiar from block-level layout, where you can use `auto` left and right margins to center an element in its containing block, as long as you’ve given it an explicit `width`. Where grid layout differs is that you can do the same thing on the vertical axis; that is, given an element with an absolute height, you can vertically center it by setting the top and bottom margins to `auto`. Figure 13-60 shows a variety of `auto` margin effects on images, which naturally have explicit heights and widths:

```css
.i01 {
  margin: 10px;
}
.i02 {
  margin: 10px;
  margin-left: auto;
}
.i03 {
  margin: auto 10px auto auto;
}
.i04 {
  margin: auto;
}
.i05 {
  margin: auto auto 0 0;
}
.i06 {
  margin: 0 auto;
}
```

<Figures figure="13-60">Various auto-margin alignments</Figures>

<Tips tips="blue">There are other ways to align grid items, notably with properties like <code>justify-self</code>, which don’t depend on having explicit <code>height</code> and <code>width</code> values. These will be covered in the next section.</Tips>

This is a lot like how margins and element sizes operate when elements are absolutely positioned. Which leads us to the next question: what if a grid item is `also` absolutely positioned? For example:

```css
.exel {
  grid-row: 2 / 4;
  grid-column: 2 / 5;
  position: absolute;
  top: 1em;
  bottom: 15%;
  left: 35px;
  right: 1rem;
}
```

The answer is actually pretty elegant: if you’ve defined grid-line starts and ends, that grid area is used as the containing block and positioning context, and the grid item is positioned `within` that context. That means the offset properties (`top` et al.) are calculated in relation to the declared grid area. Thus, the previous CSS would have the result shown in Figure 13-61.

<Figures figure="13-61">Absolutely positioning a grid item</Figures>

Everything you know about absolutely positioned elements regarding offsets, margins, element sizing, and so on applies within this formatting context. It’s just that in this case, the formatting context is defined by a grid area.

There is a wrinkle that absolute positioning introduces: it changes the behavior of the `auto` value for grid-line properties. If, for example, you set `grid-column-end: auto` for an absolutely positioned grid item, the ending grid line will actually create a new and special grid line that corresponds to the padding edge of the grid container itself.

This is true even if the explicit grid is smaller than the grid container, as can happen. To see this in action, we’ll modify the previous example as follows, with the result
shown in Figure 13-62:

```css
.exel {
  grid-row: 1 / auto;
  grid-column: 2 / auto;
  position: absolute;
  top: 1em;
  bottom: 15%;
  left: 35px;
  right: 1rem;
}
```

<Figures figure="13-62">Auto values and absolute positioning</Figures>

Note how the positioning context now starts at the top of the grid container, and stretches all the way to the right edge of the grid container, even though the grid itself ends well short of that edge.

One implication of this behavior is that if you absolutely position an element that’s a grid item, but you don’t give it any grid-line start or end values, then it will use the inner padding edge of the grid container as its positioning context. It does this without having to set the grid container to `position: relative`, or any of the other usual tricks to establish a positioning context.

Note that absolutely positioned grid items do `not` participate in figuring out grid cell and track sizing. As far as the grid layout is concerned, the positioned grid item doesn’t exist. Once the grid is set up, then the grid item is positioned with respect to the grid lines that define its positioning context.

<Tips tips="orange">As of late 2017, browsers did not support any of this absolute positioning behavior. The only way to recreate it was to relatively position the element establishing the grid area, and absolutely position a child element within it. That’s how the absolute-positioning figures in this section were created. The special <code>auto</code> behavior was also not supported.</Tips>

## 13.9 栅格的对齐方式

If you have any familiarity with flexbox, you’re probably aware of the various alignment properties and their values. Those same properties are also available in grid layout, and have very similar effects.

First, a quick refresher. The properties that are available and what they affect are summarized in Table 13-1.

Table 13-1. Justify and align values

| Property        | Aligns                                               | Applied to     |
| --------------- | ---------------------------------------------------- | -------------- |
| justify-self    | A grid item in the inline (horizontal) direction     | Grid items     |
| justify-items   | All grid items in the inline (horizontal) direction  | Grid container |
| justify-content | The entire grid in the inline (horizontal) direction | Grid container |
| align-self      | A grid item in the block (vertical) direction        | Grid items     |
| align-items     | All grid items in the block (vertical) direction     | Grid container |
| align-content   | The entire grid in the block (vertical) direction    | Grid container |

As Table 13-1 shows, the various `justify-*` properties change alignment along the inline axis—in English, this will be the horizontal direction. The difference is whether a property applies to a single grid item, all the grid items in a grid, or the entire grid. Similarly, the `align-*` properties affect alignment along the block axis; in English, this is the vertical direction.

### 13.9.1 纵向对齐和横向对齐单个元素

It’s easiest to start with the `*-self` properties, because we can have one grid show various `justify-self` property values, while a second grid shows the effects of those same values when used by `align-self`. (See Figure 13-63.)

<Figures figure="13-63">Self alignment in the inline and block directions</Figures>

Each grid item in Figure 13-63 is shown with its grid area (the dashed blue line) and a label identifying the property value that’s applied to it. Each deserves a bit of commentary.

First, though, realize that for all of these values, any element that doesn’t have an explicit `width` or `height` will “shrink-wrap” its content, instead of using the default grid-item behavior of filling out the entire grid area.

`start` and `end` cause the grid item to be aligned to the start or end edge of its grid area, which makes sense. Similarly, `center` centers the grid item within its area along the alignment axis, `without` the need to declare margins or any other properties, including `height` and `width`.

`left` and `right` have the expected results for horizontal alignment, but if they’re applied to elements via `align-self` (which is vertical alignment), they’re treated as `start`.

`self-start` and `self-end` are more interesting. `self-start` aligns a grid item with the grid-area edge that corresponds to the grid `item’s` start edge. So in Figure 13-63, the `self-start` and `self-end` boxes were set to `direction: rtl`. That set them to use right-to-left language direction, meaning their start edges were their right edges, and their end edges their left. You can see in the first grid that this right-aligned `self-start` and left-aligned `self-end`. In the second grid, however, the RTL direction is irrelevant to block-axis alignment. Thus, `self-start` was treated as `start`, and `self-end` was treated as `end`.

The last value, `stretch`, is interesting. To understand it, notice how the other boxes in each grid “shrink-wrap” themselves to their content. `stretch`, on the other hand, directs the element to stretch from edge to edge in the given direction—`align-self: stretch` causes the grid item to stretch vertically, and `justify-self: stretch` causes horizontal stretching. This is as you might expect, but bear in mind that it works only if the element’s size properties are set to `auto`. Thus, given the following styles, the first example will stretch vertically, but the second will not:

```css
.exel01 {
  align-self: stretch;
  height: auto;
}
.exel02 {
  align-self: stretch;
  height: 50%;
}
```

Because the second example sets a `height` value that isn’t `auto` (which is the default value), it cannot be resized by `stretch`. The same holds true for `justify-self` and `width`.

There are two more values that can be used to align grid items, but they are sufficiently interesting to merit their own explanation. These permit the alignment of a grid item’s first or last baseline with the highest or lowest baseline in the grid track.

For example, suppose you wanted a grid item to be aligned so the baseline of its last line was aligned with the last baseline in the tallest grid item sharing its row track. That would look like the following:

```css
.exel {
  align-self: last-baseline;
}
```

Conversely, to align its first baseline with the lowest first baseline in the same row track, you’d say this:

```css
.exel {
  align-self: baseline;
}
```

In a situation where a grid element doesn’t have a baseline, or it’s asked to baselinealign itself in a direction where baselines can’t be compared, then `baseline` is treated as `start` and `last-baseline` is treated as `end`.

<Tips tips="blue">There are two values that were intentionally skipped in this section: <code>flex-start</code> and <code>flex-end</code>. These values are supposed to be used only in flexbox layout, and are defined to be equivalent to <code>start</code> and <code>end</code> in any other layout context, including grid layout.</Tips>

### 13.9.2 纵向对齐和横向对齐全部元素

Now let’s consider `align-items` and `justify-items`. These properties accept all the same values we saw in the previous section, and have the same effect, except they apply to all grid items in a given grid container, and must be applied to a grid container instead of to individual grid items.

Thus, you could set all of the grid items in a grid to be center-aligned within their grid areas as follows, with a result like that depicted in Figure 13-64:

```css
#grid {
  display: grid;
  align-items: center;
  justify-items: center;
}
```

<Figures figure="13-64">Centering all the grid items</Figures>

As you can see, that horizontally `and` vertically centers every grid item within its given grid area. Furthermore, it causes any grid item without an explicit width and height to “shrink-wrap” its content rather than stretch out to fill their grid area. If a grid item has an explicit height and width, then those will be honored, and the item centered within its grid area.

Beyond aligning and justifying every grid item, it’s possible to distribute the grid items, or even to justify or align the entire grid, using `align-content` and `justify-content`. There is a small set of distributive values for these properties. Figure 13-65 illustrates the effects of each value as applied to `justify-content`, with each grid sharing the following styles:

```css
.grid {
  display: grid;
  padding: 0.5em;
  margin: 0.5em 1em;
  width: auto;
  grid-gap: 0.75em 0.5em;
  border: 1px solid;
  grid-template-rows: 4em;
  grid-template-columns: repeat(5, 6em);
}
```

<Figures figure="13-65">Distributing grid items horizontally</Figures>

This works just as well in column tracks as it does in row tracks, as Figure 13-66 illustrates, as long as you switch to `align-content`. This time, the grids all share these styles:

```css
.grid {
  display: grid;
  padding: 0.5em;
  grid-gap: 0.75em 0.5em;
  border: 1px solid;
  grid-template-rows: repeat(4, 3em);
  grid-template-columns: 5em;
}
```

The way this distribution works is that the grid tracks, including any gutters, are all sized as usual. Then, if there is any leftover space within the grid container—that is, if the grid tracks don’t reach all the way from one edge of the grid container to the other—then the remaining space is distributed according to the value of `justify-content` (in the horizontal) or `align-content` (in the vertical).

This space distribution is carried out by resizing the grid gutters. If there are no declared gutters, there will be gutters. If there are already gutters, their sizes are altered as required to distribute the grid tracks.

Note that because space is distributed only when the tracks don’t fill out the grid container, the gutters can only increase in size. If the tracks are larger than the container, which can easily happen, there is no leftover space to distribute (negative space turns out to be indivisible).

There is another distribution value, very new as of this writing, which wasn’t shown in the previous figures. `stretch` takes any leftover space and applies it equally to the grid tracks, not the gutters. So if there are 400 pixels of leftover space and 8 grid tracks, each grid track is increased by 50 pixels. The grid tracks are `not` increased proportionally, but equally. As of late 2017, there was no browser support for this value in terms of grid distribution.

<Figures figure="13-66">Distributing grid items vertically</Figures>

We’ll round out this section with examples of justifying, as opposed to distributing, grid tracks. Figure 13-67 shows the possibilities when justifying horizontally.

<Figures figure="13-67">Justifying the grid horizontally</Figures>

In these cases, the set of grid tracks is taken as a single unit, and justified by the value of `justify-content`. That alignment does not affect the alignment of individual grid items; thus, you could end-justify the whole grid with `justify-content: end` while having individual grid items be left-, center-, or start-justified (among other options) within their grid areas.

As you might expect by now, being able to `justify-content` horizontally means you can `align-content` vertically. Figure 13-68 shows each value in action.

<Figures figure="13-68">Aligning the grid vertically</Figures>

`left` and `right` don’t really make sense in a vertical context, so they’re treated as `start`. The others have the effect you’d expect from their names.

## 13.10 分层和排序

As we saw in a previous section, it’s entirely possible to have grid items overlap each other, whether because negative margins are used to pull a grid item beyond the edges of its grid area, or because the grid areas of two different grid items share grid cells. By default, the grid items will visually overlap in document source order: grid items later in the document source will appear in front of grid items earlier in the document source. Thus we see the following result in what’s depicted in Figure 13-69. (Assume the number in each class name represents the grid item’s source order.)

```css
#grid {
  display: grid;
  width: 80%;
  height: 20em;
  grid-rows: repeat(10, 1fr);
  grid-columns: repeat(10, 1fr);
}
.box01 {
  grid-row: 1 / span 4;
  grid-column: 1 / span 4;
}
.box02 {
  grid-row: 4 / span 4;
  grid-column: 4 / span 4;
}
.box03 {
  grid-row: 7 / span 4;
  grid-column: 7 / span 4;
}
.box04 {
  grid-row: 4 / span 7;
  grid-column: 3 / span 2;
}
.box05 {
  grid-row: 2 / span 3;
  grid-column: 4 / span 5;
}
```

<Figures figure="13-69">Grid items overlapping in source order</Figures>

If you want to assert your own stacking order, then `z-index` is here to help. Just as in positioning, `z-index` places elements relative to each other on the z-axis, which is perpendicular to the display surface. Positive values are closer to you, and negative values further away. So to bring the second box to the “top,” as it were, all you need is to give it a `z-index` value higher than any other (with the result shown in Figure 13-70):

```css
.box02 {
  z-index: 10;
}
```

<Figures figure="13-70">Elevating a grid item</Figures>

Another way you can affect the ordering of grid items is by using the `order` property. Its effect is essentially the same as it is in flexbox—you can change the order of grid items within a grid track by giving them `order` values. This affects not only placement within the track, but also paint order if they should overlap. For example, we could change the previous example from `z-index` to `order`, as shown here, and get the same result shown in Figure 13-70:

```css
.box02 {
  order: 10;
}
```

In this case, `box02` appears “on top of ” the other grid items because its order places it after the rest of them. Thus, it’s drawn last. Similarly, if those grid items were all placed in sequence in a grid track, the `order` value for `box02` would put it at the end of the sequence. This is depicted in Figure 13-71.

<Figures figure="13-71">Changing grid-item order</Figures>

Remember that just because you `can` rearrange the order of grid items this way, it doesn’t necessarily mean you `should`. As the Grid Layout specification says (section 4.2):

As with reordering flex items, the `order` property must only be used when the visual order needs to be `out-of-sync` with the speech and navigation order; otherwise the underlying document source should be reordered instead.

So the only reason to use `order` to rearrange grid item layout is if you need to have the document source in one order and layout in the other. This is already easily possible by assigning grid items to areas that don’t match source order.

This is not to say that `order` is useless and should always be shunned; there may well be times it makes sense. But unless you find yourself nearly forced into using it by specific circumstances, think very hard about whether it’s the best solution.

## 13.11 小结

栅格布局复杂而强大，没有吃透也不要灰心。栅格的运作方式要花点时间才能掌握，毕竟有大量特性是我们以前没见过的。多数特性前所未见，这就注定学习的过程是艰辛而曲折的。笔者在撰写与栅格有关的内容时也有过沮丧和迷惘，在过去二十载没有栅格布局的日子里练就的直觉完全失效了。

希望本章的内容能帮你跨过一些障碍，但是正如尤达大师所说的，“温如而知新。”对栅格布局来说，更应该把以前掌握的知识放一边，从头学起，随着时间地过去，你的耐心和毅力终将得到回报。

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
| 适用于 | 所有元素，以及：before和::after伪元素 |
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