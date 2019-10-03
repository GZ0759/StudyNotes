> 精通CSS：高级Web标准解决方案 第三版   
> [源码](https://github.com/GZ0759/css-mastery-16)

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

匿名盒子。HTML 元素可以嵌套，元素盒子当然也可以嵌套。多数盒子都是基于明确定义的元素生成的，不过有一种情况，就算不明确定义也会生成块级盒子。比如下面例子中在 section 这个块级元素的开头加入一些文本。此时，“some text”就算没有定义为块级元素，也会被当成块级元素。这种情况下，这个盒子被称为`匿名块盒子`，因为这个盒子并不与任何特定的元素相关。类似的情况还存在于块级元素内部的文本级行盒子。假设有一个段落中包含三行文本（three lines of text），这三行文本的每一行都构成了一个`匿名行盒子`。除了使用`:first-line`伪元素来添加有限的排班和颜色相关的样式之外，不能直接给`匿名块盒子`或`匿名行盒子`应用样式。

```html
<section>
  <!-- 匿名块盒子 -->
  some text
  <p>Some more text</p>
</section>
```

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

CSS 变换用于在空间中移动物体，而 CSS 过渡和 CSS 关键帧动画用于控制元素随时间推移而变化。在实战中人们通常把它们当成互补的技术来用，加个动画就意味着每秒要改变其外观 60 次，变换可以让浏览器根据对变化的描述进行非常高效的计算。过渡和关键帧动画可以让我们以巧妙的方式把这些变化转换成动画效果。

关于浏览器支持。变换、过渡和关键帧动画的规范仍然在制定中，但是大多数特性已经在常用浏览器中实现了，除了 IE8 和 Opera Mini。IE9 只支持变换的二维子集，而且要使用 -ms 前缀，并不支持关键帧动画和过渡。在 Webkit 和 Blink 系的浏览器中，变换、过渡和关键帧动画相关的属性都要加 -webkit- 前缀，旧版本的 FIrefox 还需要加 -moz- 前缀。

## 10.2 二维变换

CSS 变换支持在页面中平移、旋转、变形和缩放元素。此外，还可以增加第三维。

从技术角度说，变换改变的是元素所在的坐标系统。给元素应用变换，会为元素最初所在的空间创建所谓的局部坐标系统。局部坐标系统就是畸变场，用于转换元素的像素。

```css
.box {
  transform: rotate(45deg);
}
```

如上，页面上元素原来的位置仍然保留了像素空间，但元素上的所有点都被畸变场给变换到了新位置。如果给变换后的元素再应用一个外边距，那么因为元素所在的整个据表坐标都会被旋转，不会出现跟未旋转时一样的效果。旋转后的元素也不会妨碍页面其他部分的布局，就好像根本没有变换过一样。

注意，变换会影响页面的溢出。如果变换后的元素超出设置了 overflow 属性的元素，导致出现了滚动条，则变换后的元素会影响可滚动区域。

变换原点。默认情况下，变换是以元素边框盒子的中心作为原点的。控制原点的属性叫transform-origin。可以给transform-origin设1~3个值，分别代表x、y和z轴坐标。如果只给了一个值，则第二个默认是关键字center，与background- position类似。

注意，给SVG元素应用变换，有些地方不一样。比如，transform-origin属性的默认值是元素左上角，而不是元素中心点。

平移。平移就是元素移动到新位置。可以沿一个轴平移，使用`translateX()`或者`translateY()`；也可以同时沿两个轴平移，使用`translate()`。使用`translate()`函数时，要给它传入两个坐标值，分别代表x轴和y轴平移的距离。这两个值可以是任何长度值，像素、em或百分比都可以。但要注意，百分比这时候是相对于元素自身大小，而不是包含块的大小。

```css
.box {
  /* equivalent to transform: translateX(100%); */
  transform: translate(100%, 0);
}
```

多重变换。可以同时应用多重变换。多重变换的值以空格分隔的列表形式提供给transform属性，按照声明的顺序依次应用。

```css
.rules li {
  counter-increment: rulecount;
  position: relative;
}

.rules li:before {
  content: '§ ' counter(rulecount);
  position: absolute;
  transform-origin: 100% 100%;
  transform: translate(-100%, -100%) rotate(-90deg);
}
```

修改变换。声明多个变换以后，如果想增加新变换，不能直接在原来的基础上添加，而要重新声明整套变换。

```css
.thing {
  transform: translate(0, 100px);
}

.thing:hover {
  /* 警告：这条声明会删除平移效果 */
  /* transform: rotate(45deg); */
  /* 先平移，再旋转 */
  transform: translate(0, 100px) rotate(45deg);
}
```

缩放和变形。现在已经介绍了`translate()`和`rotate()`这两个二维变换函数，剩下的两个是`scale()`和`skew()`。这两个函数都有对应x轴和y轴的变体：scaleX()、scaleY()、skewX()和skewY()。

`scale()`函数很简单，它的参数是没有单位的数值，可以是一个，也可以是两个。如果只传给它一个数值，就表示同时在x轴和y轴上缩放。比如传入数值2，就会同时沿x轴和y轴放大一倍。传入数值1则意味着不会发生任何改变。

```css
.doubled {
  transform: scale(2);
  /* 等于transform: scale(2, 2); */
  /* 也等于transform: scaleX(2) scaleY(2); */
}
/* 只沿一个方向缩放，会导致元素被压扁或拉长。 */
.squashed-text {
  transform: scaleX(0.5);
  /* 等于transform: scale(0.5, 1); */
}
```

变形是指水平或垂直方向平行的边发生相对位移，或偏移一定角度。很多人分不清x轴变形和y轴变形。x轴变形可以理解为水平线在元素变形后仍然保持水平，而垂直线则会发生倾斜。关键在于你想让哪个轴向的边发生相对位移。

```css
.rules li {
  transform: skewX(15deg);
}

.rules li:nth-child(even) {
  transform: skewX(-15deg);
}
```

二维矩阵变换。对浏览器而言，所有这些变换都归于一个数学结构：变换矩阵。我们可以通过`matrix()`这个低级函数直接操纵变换矩阵的值，值一共有6个。

```css
.box {
  width: 100px;
  height: 100px;
  transform: matrix(1.41, 1.41, -1.16, 1.66, 70.7, 70.7);
  /* 等于 transform: rotate(45deg) translate(100px, 0) scale(2) skewX(10deg); */
}
```

变换与性能。浏览器在计算CSS效果时，会在某些情况下多花一些时间。比如，如果修改文本大小，那么生成的行盒子可能会随着文本折行而变化，而元素本身也会变高。元素变高会把下方的元素向页面下方推挤，这样一来又会迫使浏览器进一步重新计算布局。

在使用CSS变换时，相应的计算只会影响相关元素的坐标系统，既不会改变元素内部的布局，又不会影响外部的其他元素。而且，这时的计算基本上可以独立于页面上的其他计算（比如运行脚本或布局其他元素），因为变换不会影响它们。多数浏览器也都会尽量安排图形处理器（如果有的话）来做这些计算，毕竟图形处理器是专门设计来做这种数学计算的。换句话说，变换从性能角度讲是很好的。如果你想实现的效果可以用变换来做，那么变换的性能一定更好。连续多重变换的性能更佳，比如实现某个元素的动画或过渡效果。

变换也有一些副作用。
- 有些浏览器会为变换的元素切换抗锯齿方法，渲染模式会在最终变换应用前完成切换。
- 应用给元素的任何变换都会创建一个堆叠上下文。这意味着在使用变换时，要注意z-index。这是因为变换后的元素有自己的堆叠上下文。换句话说，子元素上的z-index值再大，也不会出现在父元素上方。
- 对于固定定位，变换后的元素也会创建一个新的包含块。如果发生变换的元素中有一个元素使用了`positon: fixed`，那么它会将发生变换的元素当成自己的视口。

## 10.3 过渡

过渡是一种动画，可以从一种状态过渡到另一种状态，比如按钮从常规状态变成被按下的状态。正常情况下，这种变化是瞬间完成的，至少浏览器会尽快实现这种状态变换。在点击或按下按钮时，浏览器会计算页面的新外观，然后在几毫秒之内完成重绘。而应用过渡时，我们要告诉浏览器完成类似变换要花多长时间，然后浏览器再计算在此期间屏幕上该显示哪些过渡状态。

过渡会自动双向运行，因此只要状态一反转，反向动画就会运行。

```css
button {
  transition: all 150ms;
}
button:active {
  transform: translateY(.25em);
}
```

transition 属性是一个简写形式，可以一次设置多个属性。设置过渡的持续时间，以及告诉浏览器在两个状态间切换时动画所有属性。

- transition-property 过渡效果的 CSS 属性的名称
- transition-duration 完成过渡效果需要的时间
- transition-timing-function 速度效果的速度曲线
- transition-delay 过渡效果何时开始

```css
button {
  transition-property: all;
  transition-duration: .15s;
}

/* 如果是特定属性变化而不是全部 */
button {
  transition: box-shadow .15s, transform .15s;
}

/* 另一种方式 */
button {
  transition-property: transform, box-shadow;
  transition-duration: .15s;
}
```

过渡计时函数。默认情况下，过渡变化的速度并不是每一帧都相同，这种速度的变化在动画属于中叫缓动，能让动画效果更自然和流畅。CSS 通过相应的数学函数控制这些变化，而这些函数由 `transition-timing-function`属性来指定。还有一些关键字代表不同类型的缓动函数。
- ease
- liner
- ease-in
- ease-out
- ease-in-out

```css
button {
transition: all .25 ease-in;
/* ...or we could set transition-timing-function: ease-in; */
}
```

在底层，控制速度变化的数学函数基于三次贝塞尔函数生成，每个关键字都是这些函数带特定参数的简写形式，在 CSS 变换中可以使用`cubic-bezier()`函数作为缓动值。同时，还可以指定过渡中每一步的状态，这非常适合创建订个动画。这里的`tiansition-timing-function`指定为`steps(6, start)`意思就是把过渡过程切分为六个步骤，在么跑一次开始时改变属性。默认情况下，`steps(6)`会在每一步结束时改变属性，但也可以通过传入`start`或`end`作为第二个参数来明确指定。

```css
.hello-box {
  width: 200px;
  height: 200px;
  transition: background-position 1s steps(6, start);
  background: url(steps-animation.png) no-repeat 0 -1200px;
}
.hello-box:hover {
  background-position: 0 0;
}
```

使用不同的正向和反向过渡。有时候，会希望某个方向的过渡快一些，而反方向的过渡慢一些，为此可以定义不同的过渡属性集合：一个针对非悬停状态，另一个针对悬停状态。

```css
.hello {
  transition: background-position 0s steps(6);
}
.hello:hover {
  transition-duration: .6s;
}
```

“黏着”过渡。另一个方法是根本不让过渡方向，为了“黏着”过渡，可以指定一个非常大的持续时间。

```css
.hello {
  transition: background-position 9999999999s steps(6);
}
.hello:hover {
  transition-duration: 0.6s;
}
```

延迟过渡。通常，过渡会随状态变化立即发生，比如类名被 JavaScript 修改或按钮被按下。但是可以通过 `transition-delay` 属性来推迟过渡的发生。延迟时间也可以是负值，可以一开始就直接跳到过渡的中段。

过渡的能与不能。多数情况下，涉及长度和颜色的都是可以的，这取决于是否有计算值的中间状态。比如100px到200px，红到蓝，但 display 属性的两个值 block 和 none 就没有中间状态。当然，这个规则本身其实也有例外的。

- 可插值。有些属性虽然没有明确的中间值，却可以实现动画。比如 z-index 和 column-count 只接受整数值，浏览器会自动插入整数值。visibility 属性也可以实现过渡动画，浏览器在过渡经过中点后突变为两个终点值中的一个。
- 过渡到内容高度。对于有些可以实现动画的属性比如 height，只能在数值之间过渡，不能使用像 auto 这样的关键字。

```css
.js .expando-list {
  overflow: hidden;
  transition: all .25s ease-in-out;
  max-height: 0;
  opacity: 0;
}
.js .is-expanded .expando-list {
  max-height: 24em;
  opacity: 1;
}
```

## 10.4 CSS关键帧动画

CSS过渡是一种隐式动画。换句话说，我们给浏览器指定两个状态，让浏览器在元素从一个状态过渡到另一个状态的过程中，给指定的属性添加动画效果。有时候，动画的范围不仅限于两个状态，或者要实现动画的属性一开始也不一定存在。CSS Animations规范引入了关键帧的概念来帮我们实现这一类动画。此外，关键帧动画还支持对动画时间及方式的控制。

## 10.5 三维变换

三维空间中，概念与二维变化一样，只不过要多考虑一个维度，也就是z轴。三维变换允许我们控制坐标系统，旋转、变形、缩放元素，以及向前或向后移动元素。想要实现这些效果，那就要先了解透视的概念。

# 第十一章 高级特效

# 第十二章 品控与流程
