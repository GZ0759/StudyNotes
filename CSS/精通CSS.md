> 精通CSS：高级Web标准解决方案 第三版   
> [源码](https://github.com/GZ0759/css-mastery-16)

# 目录

- [第一章 奠定基础](#第一章-奠定基础)
- [第二章 让你的样式达到目标](#第二章-让你的样式达到目标)
- [第三章 可视化格式模型概述](#第三章-可视化格式模型概述)
- [第四章 Web 印刷样式](#第四章-Web印刷样式)
- [第五章 完美盒模型](#第五章-完美盒模型)
- [第六章 内容布局](#第六章-内容布局)
  - [6.1 使用定位](#6.1-使用定位)
  - [6.2 水平布局](#6.2-水平布局)
  - [6.3 弹性布局](#6.3-弹性布局)
- [第七章 页面布局和网格](#第七章-页面布局和网格)
- [第八章 响应式 Web 设计和 CSS](#第八章-响应式Web设计和CSS)
- [第九章 样式表和数据表](#第九章-样式表和数据表)
- [第十章 让它动起来：Transforms，Transitions 和 Animations](#第十章-让它动起来：Transforms，Transitions和Animations)
- [第十一章 前沿视觉效果](#第十一章-前沿视觉效果)
- [第十二章 代码质量和工作流](#第十二章-代码质量和工作流)

# 第一章 基础知识

# 第二章 添加样式

## 2.1 CSS选择符

类型与后代选择符是最基本的选择符。类型应用于选择特定类型的元素，只要写出想要添加样式的元素名即可。类型选择符有时候也被称为元素选择符。后代选择符用于选择某个或某组元素的后代。后代选择符的写法是在两个选择符之间添加空格。

```css
p {
color: black;
}

blockquote p {
padding-left: 2em;
}
```

要想更精准地选择目标元素，可以使用 ID 选择符和类选择符。顾名思义，这两个选择符通过对应 ID 和 class 属性的值来选择元素。ID 选择符由井号（#）开通，类选择符由句点（.）开通。

```css
#intro {
font-weight: bold;
}

.date-posted {
color: #ccc;
}
```

子选择符与同辈选择符。CSS 提供了高级选择符。第一个高级选择符叫子选择符。与后代选择符会选择一个元素的所有后代不同，子选择符只选择一个元素的直接后代，也就是子元素。有时候可能需要为某个元素相邻的元素添加样式。使用相邻同辈选择符，可以选择位于某个元素后面，并与该元素拥有共同父元素的元素。“>”、“+”在这里被称为组合子，还有一个类似的组合子，那就是一般同辈组合子：`~`，使用一般同辈组合子可以选择指定元素后面的所有相同元素。

注意：相邻同辈选择符和一般同辈选择符都不会选择前面的同辈元素，这主要是跟网页渲染性能有关。通常情况下，浏览器会按照元素在页面中出现的先后顺序给它们应用样式。如果有向前同辈组合子，浏览器就必须先记住相应的选择符，然后对文档进行多轮处理才能彻底应用样式。

```css
#nav > li {
background: url(folder.png) no-repeat left top;
padding-left: 20px;
}

h2 + p {
font-size: 1.4em;
font-weight: bold;
color: #777;
}
```

通用选择符。通用选择符可以匹配任何元素，与其他语言中的通配符类似，通用选择符也使用星号（*）表示，以表示可以匹配页面中的所有元素。

```css
* {
padding: 0;
margin: 0;
}
```

属性选择符。属性选择符基于元素是否有某个属性或者属性是否有某个值来选择元素。有时候，关心的是属性值是否匹配某个模式，而非某个特定值，通过给属性选择符中的等号前面加上特殊字符，就可以表达出想要匹配的值的形式了。

```css
/* 匹配是否存在某个属性 */
abbr[title] {
border-bottom: 1px dotted #999;
}
 
 /* 匹配特定的属性值 */
input[type="submit"] {
cursor: pointer;
}

/* 匹配以字符开头的属性值 */
a[href^="http:"] 

/* 匹配以字符结尾的属性值 */
img[src$=".jpg"]

/* 匹配包含字符的属性值 */
a[href*="/about/"]

/* 匹配空格分隔的字符串中的属性值 */
a[rel~=next]

/* 匹配开头是特定值或指定值后连着一个短划线 */
a[hreflang|=en]

```

伪元素。有时候想选择的页面区域不是通过元素来表示的，而我们也不想为此给页面添加额外的标记。CSS 为这种情况提供了一些特殊选择符，叫做伪元素。伪元素一般使用双冒号语法，但是一些旧版本浏览器在实现伪元素时支持的是但冒号语法。

```css
.chapter::before {
content: '”';
font-size: 15em;
}
```

伪类。有时候想基于文档结构以外的情形来为页面添加样式，比如基于超链接或表单元素的状态。这时候可以使用伪类选择符。伪类选择符的语法是以一个冒号开头，用于选择元素的特定状态或关系。

```css
/* makes all unvisited links blue */
a:link {
color: blue;
}
/* makes all visited links green */
a:visited {
color: green;
}
/* makes links red on mouse hover, keyboard focus */
a:hover,
a:focus {
color: red;
}
/*...and purple when activated. */
a:active {
color: purple;
}
```

结构化伪类。使用结构化伪类能够做很多事，因为在文档中基于相对位置精确选择元素时，它们提供了方便。CSS3 新增了一大批与文档结构有关的伪类。其中最常用的是 nth-child 选择符，可以用来交替地为表格应用样式。nth-last-child 选择符与 nth-child 选择符类似，只不过是从最后一个元素倒序计算。CSS2.1 中有一个选择第一个子元素的伪元素，叫`:first-child`，相当于直观版的`:nth-child(1)`。CSS3 选择符规范又添加了一个选择最后一个子元素的伪类`:last-child`，对应于`nth-last-child(1)`。此外，还有`:only-child`和选择特定类型的唯一子元素`only-of-type`。

表单伪类。还有很多伪类专门用于选择表单元素，这些伪类根据用户与表单控件交互的方式，来反映表单控件的某种状态。

## 2.2 层叠

稍微复杂的样式表中都可能存在两条甚至多条规则同时选择一个元素的情况。CSS 通过一种叫层叠的机制来处理这种冲突。层叠机制的原理是为规则赋予不同的重要程度。同时允许用户使用`!important`标注来覆盖规则，主要是处于无障碍交互的需要。

```css
p {
font-size: 1.5em !important;
color: #666 !important;
}
```

归纳起来，层叠机制的重要性级别从高到低如下所示。

- 标注为`!important`的用户样式
- 标注为`!important`的作者样式
- 作者样式
- 用户样式
- 浏览器或用户代码的默认样式
- 选择符的特殊性

## 2.3 特殊性

为量化规则的特殊性，每种选择符都对应着一个数值。这样，一条规则的特殊性就表示为其每个选择符的累加数值。累加计算是基于位置累加，避免出现高特殊性选择符被一堆低特殊性选择符的累加值所覆盖。

注意：通用选择符（*）的特殊性为0，无论它在规则声明中出现多少次。

利用层叠次序。如果两条规则的特殊性相等，则优先应用后定义的规则。

控制特殊性。理解特殊性是写好 CSS 的关键，而控制特殊性则是大型网站开发总最难处理的问题。利用特殊性，可以先为公用元素设置默认样式，然后再更特殊的元素上覆盖这些样式。

特殊性与调试。任何一款现代浏览器都有内置的开发者工具，都非常清楚地显示应用给特殊元素的样式来自哪条规则。

## 2.4 继承

有些属性，像颜色或字体大小，会被应用它们的元素的后代所继承。继承是很有用的机制，有了它就可以避免给一个元素的所有后代重复应用相同的样式。但是继承的属性值时没有任何特殊性的，连0都说不上，这意味着使用特殊性为0的通用选择符设置的样式都可以覆盖继承的样式。合理利用继承有助于减少选择符的数量，降低复杂度，不同如果有大量的元素继承了各种不同的样式，那么查找样式的来源也会比较麻烦。

## 2.5 为文档应用样式

首先可以把样式放在 style 元素中，直接放在文档的 head 部分。如果样式不多，不愿意因为浏览器额外下载文件而耽误时间，那么就可以使用这种方法。如果样式在外部样式表中，那么有两种方法把它们挂接到网页上，最常用的方式是使用 link 元素，还有一种方法是使用`@import`指令加载外部 CSS 文件。

```html
<!-- 直接放置style -->
<style>
body {
font-family: Avenir Next, SegoeUI, sans-serif;
color: grey;
}
</style>

<!-- 使用link加载 -->
<link href="/c/base.css" rel="stylesheet" />


<!-- 使用@import加载 -->
<style>
@import url("/c/modules.css");
</style>
```

性能。选择以什么方式把 CSS 加载到页面中，决定了浏览器显示页面的速度。度量 Web 性能的一个重要指标就是网页内容实际显示在屏幕上需要多久。这个指标有时候也叫“渲染时间”或“上屏时间”。

- 减少 HTTP 请求

线上网页最好把需要加载的 CSS 文件数量控制在1或2个。只用一个 link 元素加载 CSS 文件，然后在其中使用`@import`，并不鞥呢把请求控制为1个，因为这意味着先需要1个请求下载链接的文件，此外还要发送额外的请求取得所有导入的文件。因此，在线上网页中尽量不要使用`@import`。

- 压缩和缓存内容

使用 GZIP 压缩线上资源也非常重要。CSS 压缩的比率很高，因为它的很多属性和值都是重复的。类似的，让 Web 服务器帮助设置一定的 CSS 文件缓存时间也很重要。

- 不让浏览器渲染阻塞 JavaScript

如果在 HTML 文档的`<head>`元素加入了`<script>`元素，浏览器必须先把链接的内容下载下来，然后再向用户显示网页内容。这种情况下的 HTML 和 CSS 解析完全被下载以及执行脚本阻断了，也就是所谓的“渲染阻塞”。渲染阻塞明显会拖慢网站加载速度。为此，主流的做法是在 HTML 页面底部的结束标签`</body>`之前加载 JavaScript。比较现代的做法是在`<head>`中使用`<script>`标签时添加 async 或 defer 属性。

```html
<head>
  <!-- will load asynchronously, but execute immediately when downloaded -->
  <script src="/scripts/core.js" async></script>
  <!-- will load asynchronously, but execute after HTML is done-->
  <script src="/scripts/deferred.js" defer></script>
</head>
```

# 第三章 可视化格式模型

## 3.1 盒模型

盒模型是 CSS 的核心概念，描述了元素如何显示，以及（在一定程度上）如何相互作用、相互影响。页面中的所有元素都被看作一个矩形盒子，这个盒子包含元素的内容、内边距、边框和外边距。

内边距（padding）是内容区周围的控件。给元素应用的背景会作用于元素内容和内边距。因此，内边距通常用于分割内容，使其不致于散布到背景的边界。   
边框（border）会在内边距外侧增加一条框线，这条框线可以是实线、虚线或点划线。   
外框的外侧是外边距（margin）。外边距是围绕在盒子可见部分之外的透明区域，用于在页面中控制元素之间的距离。   

有一个与边框类似的属性，即轮廓线（outline）。这个属性可以在边框盒子外围画出一条线，但这条线不影响盒子的布局，也就是不会影响盒子的宽度和高度。因此，outline 常用于调试复杂布局，或者演示布局效果。

盒子大小。默认情况下，元素盒子的 width 和 height 属性指的是内容盒子，也就是元素可渲染内容区的宽度和高度。这时候添加边距和内边距并不会影响内容盒子的大小，但会导致整个元素盒子变大。通过修改 box-sizing 属性可以改变计算盒子大小的方式。box-sizing 的默认值为 content-box，即内容区。

最大值和最小值。给元素应用 min-height 和 max-height 值很有用。因为这样一来，块级盒子就可以默认自动填充父元素的宽度，但不会收缩到比 min-width 指定的值更窄，或者扩展到比 max-width 指定的值更宽。

## 3.2 可见格式化模型

p、h1 和 article 这些元素是块级元素，作为元素显示为内容块或块级盒子的形式，相对而言，strong、span 和 time 被称为行内元素，因为它们的内容会以行内盒子的形式显示在行内。可以使用 display 属性改变生成的盒子类型。例如通过把 display 属性设置为 block，让 span 变得跟块级元素一样。如果把 display 属性设置为 none，还可以让浏览器不为相应的元素生成盒子。如果不生成盒子，那么元素及其包含的内容就不会显示出来，也不会占用文档中的空间。

CSS 中有几种不同的定位模型，包括浮动、绝对定位和相对定位，除非特别指定，否则所有元素盒子都会在常规文档流中生成，即 position 属性的默认值为 static。常规文档流中元素盒子的位置，由元素在 HTML 中的位置决定。但行内盒子的高度不受其垂直方向上的内边距、边框和外边距的影响。因此，给行内盒子明确设置高度和宽度也不会起作用。

行内盒子是指沿文本流水平排列，也会随文本换行而换行。它们之间的水平间距可以通过水平方向的内边距、边框和外边距来调节。

由一行文本形成的水平盒子叫行盒子（line-box），而行盒子的高度由所包含的行内盒子决定。修改行盒子大小的唯一途径就是修改行高（line-height），或者给它内部的行内盒子设置水平方向的边框、内边距和外边距。

当然，也可以把元素的 display 属性设置为 inline-block。这样设置之后，该元素就会像一个行内盒子一样水平排列。但这个盒子的内部仍然像块级元素一样，能够设置宽度、高度、垂直外边距和内边距。

匿名盒子。HTML 元素可以嵌套，元素盒子当然也可以嵌套。多数盒子都是基于明确定义的元素生成的，不过有一种情况，就算不明确定义也会生成块级盒子。比如在 section 这个块级元素的开头加入“sone text”。此时，“some text”就算没有定义为块级元素，也会被当成块级元素。这种情况下，这个盒子被称为匿名块盒子，因为这个盒子并不与任何特定的元素相关。类似的情况还存在于块级元素内部的文本级行盒子。假设有一个段落中包含三行文本，这三行文本的每一行都构成了一个匿名行盒子。除了使用`:first-line`伪元素来添加有限的排班和颜色相关的样式之外，不能直接给匿名块盒子或匿名行盒子应用样式。

## 3.3 其他CSS布局模块

# 第四章 网页排版

# 第五章 漂亮的盒子

# 第六章 内容布局

## 6.1 使用定位

绝对定位使用案例。绝对定位一般用于遮盖、工具栏和对话盒子等放置在内容上面，这些定位元素可以配合 top、right、bottom、left 属性使用。

使用初始定位。对于下面的例子，每个评论是一个设置在每个提及的段落后面的旁边元素，为了让评论展示在段落最后的左边，需要使用绝对定位。当定位上下文中的偏移量未定义时，绝对定位元素将保留其作为静态元素的位置。如果将位置偏移用 top、right、left、bottom 来定位，那么需要考虑父位置上下文和附近元素的具体数值，不过，可以使用负值 margin 来移动元素。

```css
.comment {
  position: absolute;
  width: 7em;
  margin-left: -9.5em;
  margin-top: -2.5em;
}
```

额外惊喜：用 CSS 创建三角形。

```css
.comment:after {
  position: absolute;
  content: "";
  display: block;
  width: 0;
  height: 0;
  border: 0.5em solid #dcf0ff;
  border-bottom-color: transparent;
  border-right-color: transparent;
  position: absolute;
  right: -1em;
  top: 0.5em;
}
```

使用偏移自动适应尺寸。如果绝对元素没有明确的尺寸，那么它就会变回内容需要的尺寸，当声明位置上下文的相反方向的两个偏移，元素机会伸展到可容纳的尺寸以便适应规则。

```css
.photo-header {
  position: relative;
}
.photo-header-plate {
  position: absolute;
  right: 4em;
  bottom: 4em;
  left: 4em;
  background-color: #fff;
  background-color: rgba(255, 255, 255, 0.7);
  padding: 2em;
}
```

## 6.2 水平布局

## 6.3 Flexbox

Flexbox，也就是 Flexible Box Layout 模块，是 CSS 提供的用于布局的一套新属性。这套属性包括针对容器（弹性容器，flex container）和针对其直接子元素（弹性香，flex item）的两类属性。Flexbox 可以控制弹性项的如下方面：

- 大小，基于内容及空间；
- 流动方向，水平还是垂直，正向还是方向；
- 两个轴向上的对齐与分布；
- 顺序，与源代码中的顺序无关。

容器属性

- flex-flow
  - flex-direction 主轴方向`（flex-direction: row|row-reverse|column|column-reverse）`
  - flex-wrap 换行处理`（flex-wrap: nowrap | wrap | wrap-reverse）`
- justify-content 主轴对齐`（justify-content: flex-start|flex-end|center|space-between|space-around）`
- align-items 辅轴对齐`（align-items: stretch|center|flex-start|flex-end|baseline）`
- align-content 多行对齐`（align-content: stretch|center|flex-start|flex-end|space-between|space-around）`

元素属性

- order 调整顺序
- flex
  - flex-grow 放大比例
  - flex-shrink 缩小比例
  - flex-basis 原始尺寸
- align-self 单独对齐方式

### 6.3.1 浏览器支持与语法

Flexbox 已经得到主流浏览器较新版本的广泛支持。如果要支持 IE10 及更早版本的 Webkit 浏览器，需要在本章标准代码基础上补充提供商前缀属性和一些不同的属性。IE9 及更早版本的 IE 不支持 Flexbox。

### 6.3.2 理解 Flex 方向：主轴和辅轴

区域内的盒子可以沿两个方向排列：默认水平排列（成一行），也可以垂直排列（成一列），这个排列方向成为主轴（main axis）。与主轴垂直的方向为辅轴（cross axis），区域内的盒子可以沿辅轴发生位移或伸缩。

通常，Flexbox 布局中最重要的尺寸就是主轴方向的尺寸：水平布局时的宽度或垂直布局时的高度，这个主轴方向的尺寸叫做主尺寸（main size）。

所有项集中在左侧，是从左到右书写的语言环境下的默认行为。如果把 flex-direction 改成 row-reverse，那么所有项就会集中到右侧，而且变成从右向左排列。

如果不指定大小，Flex 容器内的项目会自动收缩，也就是说，一行中的各项会收缩到各自的最小宽度，或者一列中各项会收缩到各自的最小高度，以恰好可以容纳自身内容为限。

### 6.3.3 对齐与空间

Flexbox 对子项的排列有多种方式，沿主轴的排列叫排布（justification），沿辅轴的排列则叫对齐（alignment）。 

排布对齐。用于指定排布方式的属性是 justify-content，其默认值是 flex-start，表示按照当前文本方向排布，关键词还有 flex-end、center、space-between、space-around。

Flexbox 不允许通过以上这些关键字指定个别项的排布方式。然而，如果指定某一项的外边距值为 auto，而且在容器里哪一侧还有空间，那么该外边距就会扩展占据可用空间。

辅轴对齐。如果增加 Flex 容器自身或其中一项的高度，会发现子项自动就等高了。实际上，控制辅轴对齐的属性 align-items，其默认值就是 stretch，其它关键字时 flex-start、center 和 flex-end。最后，后可以使用 baseline 关键字，将子项中文本的基线与容器基线对齐，效果与行内块元素的默认行为类似。

除了同时对其所有项，还可以在辅轴上指定个别项的对齐方式。使用的是 align-self 属性。align-self 属性重写了容器的 align-items 属性。

垂直和水平居中。Flexbox 中的垂直对齐。在容器里只有一个元素时，只要将容器设置为 flex，再将需要居中的元素的外边距设置为 auto 就行了，因为 Flexbox 中各项的自动外边距会扩展“填充”相应方向的空间。如果 Flex 容器有多个元素，那么就可以使用对齐属性将它们聚拢到水平和垂直中心上，只需要把排布和对齐都设置为 center。

### 6.3.4 可伸缩的尺寸

Flexbox 支持对元素大小的灵活控制。体现在以下三个属性中：flex-basis、flex-grow 和 flex-shrink。这三个属性应用给每个可伸缩项，而不是容器。

- flex-basis。控制项目在主轴方向上，经过修正之前的“首选”大小，可以是长度值、百分比，也可以是关键字 auto。
- flex-grow。一个弹性系数。其值是一个数值，表示剩余空间的一个比值。默认值是 0，表示从 flex-basis 取得尺寸后旧不再扩展。
- flex-shrink。也是一个弹性系数。默认值是 1，表示如果空间不够，所有项都会以自己的首选尺寸为基准等比例收缩。

扩展。只有两个 li，第一部分分得剩余空间的四分之三，第二部分分得四分之一。

```css
.navbar li:first-child {
  flex-grow: 3;
}
.navbar li:last-child {
  flex-grow: 1;
}
```

纯粹按伸缩系数计算大小。假设上面的代码中 flex-basis 的值是 0，那么这一步就不会给项目分配空间。这种情况下，容器内部的全部空间都会留到第二步再分配，就是根据伸缩系数切分，然后将最终尺寸指定给具体的项目。下面两个项目恰好各自占据可分配空间的一半。

```css
.navbar li:first-child {
  flex-basis: 0;
  flex-grow: 1;
}
.navbar li:last-child {
  flex-basis: 0;
  flex-grow: 1;
}
```

接下来可以使用 flex 这个简写属性一次性设置 flex-grow、flex-shrink 和 flex-basis 属性，值以空格分隔`flex: 1 0 0%`。

收缩项目。当项目宽度总和超过容器宽度时，Flexbox 会按照 flex-shrink 属性来决定如何收缩它们。

### 6.3.5 Flexbox 布局

与行内块和浮动类似，Flexbox 也支持内容排布到多行或多列，但具有更强的可控性。

折行与方向。可以将 flex-direction 的值改为 row-reverse，那么所有项就会变成从右上角起从右往左排布，每一项都变成了右对齐。也可以反转垂直排布的方向，让第一行从底部开头，然后向上折行，只要将 flex-wrap 设置成了 wrap-reverse。

多行布局中可伸缩的大小。Flexbox 对多行布局的另一个好处就是，可以利用可伸缩的大小均匀填充每一行。但是如果最后一个项换行了，就会独自占据所有一行，所以可以设置一个 max-width 来限制可伸缩的范围。

对齐所有行。Flexbox 允许相对于一行的 flex-start、center、baseline 和 flex-end 这几个点来对齐项目。而在多行布局中，则可以相对于容器来对齐行或列。align-content 的默认值是 stretch，意思是每一行都会拉伸以填充自己应占的容器高度。align-content 对容器中多行的作用，与 justify-content 对主轴内容排布的作用非常相似。通过 align-content 骇客把多行排布到 flex-start（容器顶部）、flex-end（容器底部）、center（容器中部）、还可以通过 space-between 或 space-around 让多行隔开。

### 6.3.6 列布局与个别排序

使用 Flexbox 的 order 属性，可以完全摆脱项目在源代码中顺序的约束。只要告诉浏览器这个项目排第几就行了。默认情况下，每个项目的 order 值都为 0，意味着按照它们在源代码中的顺序出现。order 的值不一定要连续，而且正、负值都可以，只要是可以比较大小的数值，相应的项就会调整次序。

### 6.3.7 嵌套的 Flexbox 布局

两个文章导读组件及时 Flexbox 行的可伸缩项，也是嵌套的 Flexbox 列。只要在“阅读详情”元素上设置 `margin-top: auto`，就可以把它推到列的底部，让两个组件的元素在视觉上对齐。

```css
.article-teaser-group {
  display: flex;
}

.article-teaser {
  display: flex;
  flex-direction: column;
  max-width: 20em;
}
.article-teaser img {
  width: 100%;
  min-height: 0; 
  order: -1;
}
/* 底部查看更多按钮 */
.article-teaser-more {
  margin-top: auto;
}

```

### 6.3.8 Flexbox 不可用怎么办

首先，因为 Flexbox 只是一种显示模式，所以不理解 flex 关键字的浏览器会忽略它。也就是说，不支持 Flexbox 的浏览器仍然会按照一个常规块元素来显示原来的容器。

其次，给可伸缩项加上 float 声明，或者将其设置为`display: inline-block`，都不会影响 Flexbox 布局。

### 6.3.9 Flexbox 的 bug 与提示

order 属性的值决定了可伸缩项的绘制次序，但这个值可能会影响这些项的叠加次序，与 z-index 类似。

# 第七章 页面布局和网格

# 第八章 响应式 Web 设计与 CSS

# 第九章 表单和数据表

# 第十章 变换、过渡与动画

## 10.1 概述

CSS 变换用于在空间中移动物体，而 CSS 过渡和 CSS 关键帧动画用于控制元素随时间推移而变化。在实战中人们通常把它们当成互补的技术来用，加个动画就意味着每秒要改变其外观 60 次，变换可以让卢兰奇根据对变化的描述进行非常高效的计算。过渡和关键帧动画可以让我们以巧妙的方式把这些变化转换成动画效果。

关于浏览器支持。变换、过渡和关键帧动画的规范仍然在制定中，但是大多数特性已经在常用浏览器中实现了，除了 IE8 和 Opera Mini。IE9 只支持变换的二维子集，而且要使用 -ms 前缀，并不支持关键帧动画和过渡。在 Webkit 和 Blink 系的浏览器中，变换、过渡和关键帧动画相关的属性都要加 -webkit- 前缀，旧版本的 FIrefox 还需要加 -moz- 前缀。

## 10.2 二维变换
## 10.3 过渡
## 10.4 CSS关键帧动画
## 10.5 三维变换

# 第十一章 高级特效

# 第十二章 品控与流程
