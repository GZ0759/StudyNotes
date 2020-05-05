> CSS权威指南第四版  
> CSS:The Definitive Guide(4th Edition)
> 2019年4月第一版
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

#### 置换元素

置换元素（replaced element）指用来置换元素内容的部分不由文档内容直接表示。在 HTML 中，最常见的置换元素要数 img ，它的内容由文档之外的图像文件替换。其实，通过下面这个简单的例子可以看出， img 元素没有内容。

```html
<img src="howdy.gif" />
```

如果指向的图像文件存在，文档会把那个图像显示出来，否则，浏览器什么也不显示，或者显示“图像损坏”占位图。

input 元素类似，根据类型的不同，会替换成单选按钮、复选框或文本输入框。

#### 非置换元素

HTML 元素大部分是非置换元素（nonreplaced element），即元素的内容由用户代理（通常为浏览器）在元素自身生成的框中显示。例如，`<span>hi there</span>`是非置换元素，用户代理会显示“hi there”文本。段落、标题、单元格、列表，以及 HTML 中其他几乎所有元素都是非置换元素。

### 1.2.2 元素的显示方式

除了置换元素和非置换元素，CSS还把元素分为块级和行内两种基本类型。（这两种最常见，除此之外还有其他的显示类型）。

#### 块级元素

块级元素默认生成一个填满父级元素内容区域的框，旁边不能有其他元素。也就是说，块级元素在元素框前后都有断行。 HTML 中最常见的块级元素有p和div。置换元素可以是块级元素，但往往不是。

列表项目是一种特殊的块级元素，它会在元素框旁边生成一个记号（无序列表通常是圆点，有序列表通常是数字），除此之外列表项目和其他块级元素并没有什么不同。

#### 行内元素

行内元素在一行文本内生成元素框，不打断所在的行。最常见的行内元素是a，此外还有 strong 和 em 。这类元素不在自身所在的元素框欠火候“断行”，因此可以出现在另一个元素的内容中，且不影响所在的元素。

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

开始与结束style标签之间的样式表称为文档样式表（document stylesheet）或嵌入样式表（embedded stylesheet）。style元素可以直接包含应用到文档上的样式，也可以通过@import 指令引入外部样式表。

### 1.3.3 @import 指令

与link标签一样，Web浏览器遇到@import 指令时会加载外部样式表。但是**@import 指令必须写在样式表的开头**，否则不起作用。

一个文档中可以有多个@import 指令，但是无法指定候选样式表，可以指定媒体描述符。

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
	...
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

	| 重要性（从低到高) | 来源     | 重要程度     |
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
```json
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
第 11 章 定位

# 第 12 章 弹性盒布局

CSS Flexible Box Module Level 1（简称 [Flexbox](https://www.w3.org/TR/css-flexbox-1/)，弹性盒）把以往间距的布局人物变得极为简单，例如很多类型的页面、小组件、应用和图库。

## 12.1 弹性盒基础

弹性盒是一种简单而强大的布局方式，我们通过弹性盒指明空间的分布方式、内容的对齐方式和元素的视觉顺序，把不同的组件放置在页面中。内容可以轻易横向或纵向排布，还可以沿一个轴布局，或者折断成多行。

使用弹性盒，内容的呈现顺序不再受源码顺序的限制。然而，这只是视觉上的调整，弹性盒相关的属性不会改变屏幕阅读器对内容的读取顺序。

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
- 主轴尺寸：主轴方向上内容的总长度。
- 主轴起边：主轴上内容开始流动的那一端。
- 主轴终边：主轴上内容流向的那一端，与主轴起边相对。
- 垂轴：块级元素沿此轴堆叠。在弹性盒中，指放置新弹性元素行的方向（前提是允许换行）。
- 垂轴尺寸：垂轴方向上内容的总长度。
- 垂轴起边：垂轴上块级元素开始堆叠的那一边。
- 垂轴终边：垂轴上与起边相对的那一边。

这些要素的位置取决于弹性方向、换行方式和书写模式。图解每种书写模式有点难，下面仅以从左至右书写的语言为例。各种情况见表12-1。

### 12.2.5. flex-wrap续谈

默认值nowrap禁止换行，因此前文讨论的垂轴方向没有任何意义，毕竟根本不会出现第二行。如果可能出现额外的行（flex-wrap设为wrap或wrap-reverse时）,那些将沿垂轴方向添加。第一行放在垂轴的起边，额外的行则向垂轴终边排开。

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

对弹性容器中的文本子节点来说，如果文本节点不是空的（内容不是空白）,将放在一个匿名弹性元素中，其行为与其他同辈弹性元素一样。虽然匿名弹性元素与同辈DOM节点一样，将继承在弹性容器上设置的相关弹性属性，但是不能直接使用CSS装饰。因此，不能直接在匿名弹性元素上设置针对弹性元素的属性。

### 12.9.2. 弹性元素的特性

弹性元素的外边距不折叠。float 和 clear 属性对弹性元素不起作用，不会把弹性元素移出文档流。其实，应用到弹性元素的 float 和 clear 将被忽略（然而，float属性对框体的生成仍有影响，因为 display 属性的计算值受它影响）。

**绝对定位**

我们知道float不会浮动弹性元素，但是`position:absolute`则不一样。如果绝对定位弹性容器的子元素，与绝对定位普通元素一样，将从文档流中移除。

除此之外，绝对定位的弹性元素不再参与弹性布局，因为它们已经不在文档流中。然而，这些元素将受应用在弹性容器上的样式影响，就像子元素受普通父元素（非弹性容器）的样式影响一样。除了可继承的属性被继承之外，应用到弹性容器上的属性可能还会影响定位原点。

绝对定位的弹性容器的子元素既受弹性容器的justify-content值影响，也受自身align-self值（如果设定了）的影响。例如，如果在绝对定位的子元素上设定`align-self:center`,元素将相对弹性容器的垂轴居中，然后再使用top、bottom、外边距等属性移动其位置。

order属性对弹性容器中绝对定位的子元素的位置没有影响，但是对同辈元素的绘制顺序有影响。

### 12.9.3. 最小宽度

在图12-40中可以看到，设为默认值nowrap的弹性元素行从弹性容器中溢出了。这是因为对弹性元素来说，未设定min-width时，默认为auto,而不是0。最初，规范规定，如果弹性元素在唯一的主轴上放不下，其尺寸将缩减。然而，出现弹性元素后，min-width的规范改了（以前，min-width的默认值是0。参见https://drafts.csswg.org/css2/visudet.html#min-max-widths)。

## 12.10 适用于弹性元素的属性

虽然弹性元素的对齐方式、顺序和弹性（flexibility)在一定程度上受在弹性容器上设置的属性控制，但是有些属性可以应用到单个弹性元素上，以便进行更细致地控制。
简写属性flex,以及构成它的flex-grow、flex-shrink和flex-basis属性用于控制弹性元素的弹性。这里所说的弹性是指弹性元素在主轴方向上可以增加或缩减多少尺寸。

## 12.11 flex属性 

弹性布局最突出的一点是能把弹性元素变得具有“弹性”，即在主轴方向上调整弹性元素的宽度或高度，占满可用空间。弹性容器根据弹性增长因子（flex grow factor)按比例分配额外的空间，或者根据弹性缩减因子（flex shrink factor)按比例缩小弹性元素，以防溢出（稍后探讨这些概念）。

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
第 16 章 转换
第 17 章 跃迁
第 18 章 动画
第 19 章 过滤器，混合，剪切和掩蔽
第 20 章 Media-Dependent 风格