> CSS 世界  
> 2017 年 12 第一次出版

<!-- TOC -->

- [第 1 章 概述](#第1章-概述)
- [第 2 章 需提前了解的术语和概念](#第2章-需提前了解的术语和概念)
- [第 3 章 第 3 章　流、元素与基本尺寸](#第3章-流、元素与基本尺寸)
- [第 4 章 盒尺寸大家族](#第4章-盒尺寸大家族)
  - [4.1 深入理解 content](#41-深入理解content)
  - [4.2 温和的 padding 属性](#42-温和的padding属性)
  - [4.3 激进的 margin 属性](#43-激进的margin属性)
  - [4.4 功勋卓越的 border 属性](#44-功勋卓越的border属性)
- [第 5 章 内联元素与流](#第5章-内联元素与流)
  - [5.1 字母 x—CSS 世界中隐匿的举足轻重的角色](#51-字母xcss世界中隐匿的举足轻重的角色)
  - [5.2 内联元素的基石 line-height](#52-内联元素的基石line-height)
  - [5.3 line-height 的好朋友 vertical-align](#53-line-height的好朋友vertical-align)
- [第 6 章 流的破坏与保护](#第6章-流的破坏与保护)
  - [6.1 魔鬼属性 float](#61-魔鬼属性-float)
  - [6.2 float 的天然克星 clear](#62-float-的天然克星-clear)
  - [6.3 CSS 世界的结界——BFC](#63-css-世界的结界bfc)
  - [6.4 最佳结界 overflow](#64-最佳结界-overflow)
  - [6.5 float 的兄弟 position:absolute](#65-float-的兄弟-positionabsolute)
  - [6.6 absolute 与 overflow](#66-absolute-与-overflow)
  - [6.7 absolute 与 clip](#67-absolute-与-clip)
  - [6.8 absolute 的流体特性](#68-absolute-的流体特性)
  - [6.9 position:relative 才是大哥](#69-positionrelative-才是大哥)
  - [6.10 强悍的 position:fixed 固定定位](#610-强悍的-positionfixed-固定定位)
- [第 7 章 CSS 世界的层叠规则](#第7章-css世界的层叠规则)
  - [7.1 z-index 只是 CSS 层叠规则中的一叶小舟](#71-z-index-只是-css-层叠规则中的一叶小舟)
  - [7.2 理解 CSS 世界的层叠上下文和层叠水平](#72-理解-css-世界的层叠上下文和层叠水平)
  - [7.3 理解元素的层叠顺序](#73-理解元素的层叠顺序)
  - [7.4 务必牢记的层叠准则](#74-务必牢记的层叠准则)
  - [7.5 深入了解层叠上下文](#75-深入了解层叠上下文)
  - [7.6 z-index 负值深入理解](#76-z-index-负值深入理解)
  - [7.7 z-index“不犯二”准则](#77-z-index不犯二准则)
- [第 8 章 强大的文本处理能力](#第8章-强大的文本处理能力)
  - [8.1 line-height 的另外一个朋友 font-size](#81-line-height-的另外一个朋友-font-size)
  - [8.2 字体属性家族的大家长 font-family](#82-字体属性家族的大家长-font-family)
  - [8.3 字体家族其他成员](#83-字体家族其他成员)
  - [8.4 font 属性](#84-font-属性)
  - [8.5 真正了解@font face 规则](#85-真正了解font-face-规则)
  - [8.6 文本的控制](#86-文本的控制)
  - [8.7 了解:first-letter/:first-line 伪元素](#87-了解first-letterfirst-line-伪元素)
- [第 9 章 元素的装饰与美化](#第9章-元素的装饰与美化)
  - [9.1 CSS 世界的 color 很单调](#91-css-世界的-color-很单调)
  - [9.2 CSS 世界的 background 很单调](#92-css-世界的-background-很单调)
- [第 10 章 元素的显示与隐藏](#第10章-元素的显示与隐藏)
  - [10.1 display 与元素的显隐](#101-display-与元素的显隐)
  - [10.2 visibility 与元素的显隐](#102-visibility-与元素的显隐)
- [第 11 章 用户界面样式](#第11章-用户界面样式)
  - [11.1 和 border 形似的 outline 属性](#111-和-border-形似的-outline-属性)
  - [11.2 光标属性 cursor](#112-光标属性-cursor)
- [第 12 章 流向的改变](#第12章-流向的改变)
  - [12.1 改变水平流向的 direction](#121-改变水平流向的-direction)
  - [12.2 改变 CSS 世界纵横规则的 writing-mode](#122-改变-css-世界纵横规则的-writing-mode)

<!-- /TOC -->

# 第 1 章 概述

典型的计算机开发语言着重逻辑思维和抽象能力，但是 CSS 这门语言本身并无逻辑可言，着重的是特性间的相互联系和具象能力。

CSS 世界中的“流”实际上是 CSS 世界中的一种基本的定位和布局机制，可以理解为现实世界的一套物理规则，“流”跟现实世界的“水流”有异曲同工的表现。

CSS 世界构建的基石是 HTML，而 HTML 最具代表的两个基石`<div>`和`<span>`正好是 CSS 世界中块级元素和内联级元素的代表。

所谓“流体布局”，指的是利用元素“流”的特性实现的各类布局效果。因为“流”本身具有自适应特性，所以“流体布局”往往都是具有自适应性的。但是，“流体布局”并不等同于“自适应布局”。“自适应布局”是对凡是具有自适应特性的一类布局的统称，“流体布局”要狭窄得多。例如，表格布局也可以设置为 100%自适应，但表格和“流”不是一路的，并不属于“流体布局”。 曾经风靡的“div+CSS 布局”，实际上指的就是这里的“流体布局”。

CSS 新世界，CSS 3 主要有两个大的改变，布局更为丰富（CSS3 媒介查询、弹性盒子布局、格珊布局）、视觉表现更进步（圆角、阴影和渐变、transform 变换、filter 滤镜和混合模式、animation 动画）。

# 第 2 章 需提前了解的术语和概念

属性。属性对应的是平常我们书面或交谈时对 CSS 的中文称谓。例如 CSS 代码中的 height 和 color 就是属性。

值。值大多数与数字挂钩。类型包括整数值、数值、百分比值、长度值、颜色值。

关键字。关键字指的是 CSS 里面很关键的单词，例如 CSS 代码中的 transparent 就是典型的关键字，还有常见的 solid、inherit 等都是关键字，其中 inherit 也称作泛关键字。

变量。CSS 中目前可以成为变量的比较有限，CSS3 中的 currentColor 就是变量。

长度单位。CSS 中的单位有时间单位（如 s、ms），还有角度单位（如 deg、rad 等），但最常见的自然还是长度单位（如 ps、em 等）。需要注意的是，诸如 2%后面的百分号%不是长度单位。如果继续细分，长度单位又可以分为相对字体长度单位和绝对长度单位。

- 相对长度单位。相对长度单位又分为相对长度单位（em、ex、rem、ch）和相对视区长度单位（vh、vw、vmin、vmax）。

- 绝对长度单位。最常见的就是 px，还有 pt、cm、mm、pc 等。

功能符。值以函数的形式指定（就是被括号括起来的那种），主要用来表示颜色（rgba 和 hsla）、背景图片地址（url）、元素属性值、计算（calc）和过渡效果等，如 rgba(0,0,0,.5)、url('css-world.png')、 attr('href')和 scale(-1)。

属性值。属性冒号后面的所有内容统一称为属性值。例如，1px solid rgb(0,0,0) 就可以称为属性值，它是由“值+关键字+功能符”构成的。属性值也可以由单一内容构成。例如，`z-index:1` 的 1 也是属性值。

声明。属性名加上属性值就是声明。

声明块。声明块是花括号`（{}）`包裹的一系列声明。

规则或规则集。出现了选择器，而且后面还跟着声明块。

选择器。选择器是用来瞄准目标元素的东西，例如，`.vocabulary`就是一个选择器。

- 类选择器：指以“.”这个点号开头的选择器。很多元素可以应用同一个类选择器。“类”，天生就是被公用的命。

- ID 选择器：“#”打头，权重相当高。ID 一般指向唯一元素。但是，在 CSS 中，ID 样式出现在多个不同的元素上并不会只渲染第一个，而是雨露均沾。但显然不推荐这么做。

- 属性选择器：指含有`[]`的选择器，形如`[title]{}`、`[title= "css-world"]{}`、`[title~="css-world"]{}`、`[title^= "css-world"]{}`和`[title$="cssworld"]{}`等。

- 伪类选择器： 一般指前面有个英文冒号（:）的选择器，如`:first-child`或`:lastchild`等。

- 伪元素选择器：就是有连续两个冒号的选择器，如`::first-line`、`::first-letter`、`::before`和`::after`。

关系选择器。关系选择器是指根据与其他元素的关系选择元素的选择器，常见的符号有后代选择器（空格）、相邻后代选择器（“>”）、兄弟选择器（“~”），还有相邻兄弟选择器（“+”）等，这些都是非常常用的选择器。

`@`规则。`@`规则指的是以`@`字符开始的一些规则，像`@media`、`@font-size`、`@page`或者`@support`，诸如此类。

当某个浏览器中出现与其他浏览器不一样的行为或样式表现得时候，此时遇到的表现差异并不是浏览器的 bug，用计算机领域的专业术语描述应该是“未定义行为”。

# 第 3 章　流、元素与基本尺寸

## 3.1 块级元素

虽然标签种类繁多，但通常把它们分为两类:块级元素和内联元素。

“块级元素”对应的英文是 block-level element，常见的块级元素有`<div>`、`<li>`和`<table>`等，它们都符合块级元素的基本特征，也就是一个水平流上只能单独显示一个元素，多个块级元素则换行显示。

由于“块级元素”具有换行特性，因此理论上它都可以配合 clear 属性来清除浮动带来的影响。实际开发时，我们要么使用 block，要么使用 table，并不会使用 list-item。

```css
.clear:after {
  content: "";
  display: "block";
  clear: both;
}
```

## 3.2 width/height 作用的具体细节

display:inline-table 的盒子是怎样组成的。外面是“内联盒子”，里面是“table 盒子”。得到的就是一个可以和文字在一行中显示的表格。

width/height 作用在哪个盒子上。width 的默认值是 auto，它至少包含了以下 4 种不同的宽度表现。

- 充分利用可用空间。元素宽度默认是 100%于父级容器。
- 收缩与包裹。典型代表就是浮动、绝对定位、inline-block 元素或 table 元素。
- 收缩到最小。这个最容易出现在 table-layout 为 auto 的表格中，单独一个文字占一行。
- 超出容器限制。除非有明确的 width 相关设置，否则上面 3 种情况尺寸都不会主动超过父级容器宽度限制的，但是存在一些特殊情况。

```css
.father {
  width: 150px;
  background-color: #cd0000;
  white-space: nowrap;
}
.child {
  display: inline-block;
  background-color: #f0f3f9;
}
```

多年前总结过一套“鑫三无准则”，即“无宽度，无图片，无浮动”。为何要“无宽度”？原因很简单，表现为“外部尺寸”的块级元素一旦设置了宽度，流动性就丢失了。

```css
.nav {
  width: 240px;
}
.nav-a {
  display: block;
  /* 200px = 240px - 10px*2 - 10px*2 */
  width: 200px;
  margin: 0 10px;
  padding: 9px 10px;
  ...;
}
```

格式化宽度仅出现在“绝对定位模型”中，也就是出现在 position 属性值 为 absolute 或 fixed 的元素中。在默认情况下，绝对定位元素的宽度表现是“包裹性”，宽度由内部尺寸决定，但是对于非替换元素，当 left/right 或 top/bottom 对立方位的属性值同时存在的时候，元素的宽度表现为“格式化宽度”，其宽度大小相对于最近的具有定位特性的祖先元素计算。

```css
div {
  position: absolute;
  left: 20px;
  right: 20px;
  /* 该祖先元素宽度是1000px，则该元素宽度是960px */
}
```

包裹性。除了 inline-block 元素，浮动元素以及绝对定位元素都具有包裹性，均由类似的智能宽度行为。按钮就是 CSS 世界中极具代表性的 inline-block 元素，可谓是展示“包裹性”最好的例子，具体表现为：按钮文字阅读宽度越宽（内部尺寸特性），但如果文字足够多，则会在容器宽度处自动换行（自适应特性）。"包裹性"对实际开发有什么作用呢？

```css
/* 文字少时居中显示，超过一行居左显示 */
.box {
  text-align: center;
}
.content {
  display: inline-block;
  text-align: left;
}
```

首选最小宽度。所谓“首选最小宽度”，指的是元素最适合的最小宽度。在 CSS 世界中，图片和文字的权重要远大于布局，因此，CSS 的设计者显然不会让图文在 width:auto 时宽度变成 0 的，此时所表现的宽度就是“首选最小宽度"。具体表现规则如下：

- 东亚文字最小宽度为每个汉字的宽度。
- 西方文字最小宽度由特定的连续的英文字符单元决定。
- 类似图片这样的替换元素的最小宽度就是该元素内容本身的宽度。

最大宽度。最大宽度就是元素可以有的最大宽度。如果内部没有块级元素或者块级元素没有设定宽度值，则“最大宽度”实际上是最大的连续内联盒子的宽度。连续内联盒子指的是 display 为 inline、inline-block、inline-table 等元素一个或一堆元素，中间没有任何的换行标签或者其它块级元素。

最大宽度对我们实际开发有什么作用呢？大部分需要使用“最大宽度”的场景都可以通过设置一个“很大宽度”来实现。设置“很大宽度”，可以保证图片不会因为容器宽度不足而不在一行内显示。两者都能实现几张图片左右滑来滑去的效果。

width 值作用的细节。宽度设定和表现并不合理，主要是流动性丢失、与现实世界表现不一致，包含 padding 或 border 会让元素宽度变大的这种 CSS 表现往往会让 CSS 使用者困惑。

所谓“宽度分离原则”，就是 CSS 中的 width 属性不与影响宽度的 padding/border（有时候包括 margin）属性共存。

分离，width 独立占用一层标签，而 padding、 border、 margin 利用流动性在内部自适应呈现。在前端领域，一提到分离，作用一定是便于维护。由于盒尺寸中的 4 个盒子都能影响宽度，自然页面元素的最终宽度就很容易发生变化而导致意想不到的布局发生。width、padding、border 混用的时候，任何修改都需要实时去计算现在的 width 应该设置多大才能和之前的占用的宽度一样，而使用下列代码进行分离，不用计算，而且页面结构反而更稳固。

```css
.father {
  width: 180px;
}
.son {
  margin: 0 20px;
  padding: 20px;
  border: 1px solid;
}
```

height 和 width 还有一个比较明显的区别就是对百分比单位的支持。 对于 width 属性， 就算父元素 width 为 auto，其百分比值也是支持的；但是，对于 height 属性，如果父元素 height 为 auto，只要子元素在文档流中，其百分比值完全就被忽略了。百分比高度值要想起作用，其父级必须有一个可以生效的高度值。如果包含块的高度没有显式指定（即高度由内容决定），并且该元素不是绝对定位，则计算值为 auto。

如何让元素支持`height: 100%`效果？第一是设定显式的高度值。第二是使用绝对定位。需要注意的是，绝对定位元素的百分比计算和非绝对定位元素的百分比计算是有区别的，区别在于绝对定位的宽高百分比计算是相对于 padding box 的，也就是说会把 padding 大小值计算在内，但是，非绝对定位元素则是相对于 content box 计算的。

改变 width/height 作用细节的 box-sizing。该属性虽然是 CSS3 属性，但是 IE8 可以在添加-ms-私有前缀后支持，IE9 浏览器开始就不需要私有前缀。box-sizing 属性的作用是改变 width 的作用细节。默认情况下，width 是作用在 content box 上，而该属性的作用就是可以把 width 作用的盒子变成其他几个。box-sizing 被发明出来最大的初衷应该是解决替换元素宽度自适应问题。

相对简单而单纯的 height:auto。CSS 的默认流是水平方向的，宽度是稀缺的，高度是无限的。因此，宽度的分配规则就比较复杂，高度就显得比较随意，叠加就是最终的高度值，当然如果存在于绝对定位模型中，也具有格式化高度特性。

关于 height:100%。height 和 width 还有一个比较明显的区别就是对百分比单位的支持。对于 width 属性，就算父元素 width 为 auto，其百分比也是支持的。但是，对于 height 属性，如果父元素 height 为 auto ，只要子元素在文档流中，其百分比值完全就被忽略了。

如何让元素支持 height:100% 效果。

- 设定显式的高度值。
- 使用绝对定位。但绝对定位的宽高百分比是相对于 padding box 的。

## 3.3 CSS min-width/max-width 和 min-height/max-height 二三事

在 CSS 世界中，min-width/max-width 出现的场景一定是自适应布局或则流体布局中。IE 7 浏览器就支持 min/max-width。

在公众号的热门文章中，经常会有图片，这些图片都是用户上传产生的，因此尺寸会有大有小，为了避免图片在移动端展示过大影响体验，常常会有下面的 max-width 限制：

```css
img {
  max-width: 100%;
  height: auto !important;
}
```

height:auto 是必需的，否则，如果原始图片有设定 height， max-width 生效的时候，图片就会被水平压缩。强制 height 为 auto 可以确保宽度不超出的同时使图片保持原来的比例。但这样也会有体验上的问题，那就是在加载时图片占据高度会从 0 变成计算高度，图文会有明显的瀑布式下落。

min-width/min-height 的初始值是 auto，max-width/max-height 的初始值是 none。 max-width 会覆盖 width，包裹覆盖 !important；min-width 覆盖 max-width，此规则发生在 min-width 和 max-width 冲突的时候。

任意高度元素的展开收起动画技术。如果使用 height+overflow:hidden 实现，height 使用的值假设是 auto，则从 0 到 auto 是无法计算的，因此无法形成过渡效果。

```css
.element {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.25s;
}
.element.active {
  max-height: 666px; /* 一个足够大的最大高度值 */
}
```

## 3.4 内联元素

从作用上来讲，块级负责结构，内联负责内容。 CSS 世界是为图文展示而设计的。所谓图文，指图片和文字，是最典型的内联元素。所以，在 CSS 世界中，内联元素是最为重要的，涉及的 CSS 属性也非常之多。

从定义看，“内联盒子”的“内联”特指“外在盒子”，和“display 为inline 的元素”不是一个概念。inline-block 和 inline-table 都是“内联元素”，因为它们的“外在盒子”都是内联盒子。从表现看，“内联元素”的典型特征就是可以和文字在一行显示。

内联世界深入的基础——内联盒模型。
- 内容区域（content area），内容区域指一种围绕文字看不见的盒子，其大小仅受字符本身特性控制，本质上是一个字符盒子。
- 内联盒子（inline box），“内联盒子”不会让内容成块显示，而是排成一行，该盒子又可以细分为“内联盒子”和“匿名内联盒子”两类。
  - 如果外部含内联标签则属于“内联盒子”；
  - 如果是个光秃秃的文字，则属于“匿名内联盒子”。
- 行框盒子（line box），每一行就是一个“行框盒子”，每个“行框盒子”又是由一个一个“内联盒子”组成的。
- 包含盒子（containing box），此盒子由一行一行的“行框盒子”组成。注意的事，更准确的称呼应该是“包含块”（containing block）。

幽灵空白节点。在 HTML5 文档声明中，内联元素的所有解析和渲染比哦先就如同每个行框盒子前面有一个“空白节点”一样。这个“空白节点”永远透明，不占据任何宽度，看不见也无法通过脚本获取。

# 第 4 章 盒尺寸大家族

盒尺寸中的 4 个盒子 content box、 padding box、 border box 和 margin box 分别对应 CSS 世界中的 content、 padding、 border 和 margin 属性，作者把这 4 个属性称为“盒尺寸四大家族” 。

## 4.1 深入理解 content

通过修改某个属性值呈现的内容就可以被替换的元素就称为“替换元素”。替换元素除了内容可替换这一特性以外，还有以下一些特性。

1. 内容的外观不受页面上的 CSS 的影响。
2. 有自己的尺寸。
3. 在很多 CSS 属性上有自己的一套表现规则。

可以将替换元素的尺寸从内而外分为 3 类：固有尺寸、HTML 尺寸和 CSS 尺寸，这三层结构的计算规律具体如下。

1. 如果没有 CSS 尺寸和 HTML 尺寸，则使用固有尺寸作为最终的宽高。
2. 如果没有 CSS 尺寸，则使用 HTML 尺寸作为最终的宽高 。
3. 如果有 CSS 尺寸，则最终尺寸由 CSS 属性决定。
4. 如果“固有尺寸”含有固有的宽高比例，同时仅设置了宽度或仅设置了高度，则元素依然按照固有的宽高比例显示。
5. 如果上面的条件都不符合，则最终宽度表现为 300 像素，高度为 150 像素，宽高比 2:1。这条规则对`<video>`、`<canvas>`和`<iframe>`这些元素都适用，但是图片元素例外。
6. 内联替换元素和块级替换元素使用上面同一套尺寸计算规则。

在 CSS 世界中，图片资源的固有尺寸是无法改变的。尺寸变化的本质并不是改变固有尺寸，而是采用了填充（fill）作为适配 HTML 尺寸和 CSS 尺寸的方式，且在 CSS3 之前，此适配方式是不能修改的。在 CSS3 新世界中，`<img>`和其他一些替换原宿的替换内容的适配方式可以通过 object-fit 属性修改。

实际上，在 CSS 世界中，我们把 content 属性生成的对象称为“匿名替换元素”。content 与替换元素的关系包含以下几点。

1. 使用 content 生成的文本是无法选中、无法复制的，好像设置了`user-select: none`声明一般，但是普通元素的文本却可以被轻松选中。
2. 不能左右`:empty`伪类。也就是说添加 content 的空内容还是会被这个伪类选择到。
3. content 动态生成值无法获取。

content内容生成技术。在实际项目中，content 属性几乎都是用在`::before`/`::after`这两个伪元素中，因此，content 内容生成技术有时候也称为`::before`/`::after`伪元素技术。

1. content 辅助元素生成。通常，我们会把 content 的属性值设置为空字符串。然后，利用其他 CSS 代码来生成辅助元素，或实现图形效果，或实现特定布局。与使用显式的 HTML 标签元素相比，这样做的好处是 HTML 代码会显得更加干净和精简。
```css
.clear:after {
  content: '';
  display: table; /* 也可以是'block' */
  clear: both;
}
```
2. content 字符内容生成。content 字符内容生成就是直接写入字符内容，中英文都可以，比较常见的应用就是配合 @font-face 规则实现图标字体效果。除常规字符之外，我们还可以插入 Unicode 字符，比较经典 的就是插入换行符来实现某些布局或者效果。
3. content 图片生成，指的是直接用 url 功能符显示图片。url 功能符中的图片地址不仅可以是常见的 png、 jpg 格式，还可以是 ico 图片、svg 文件以及 base64URL 地址，但不支持 CSS3 渐变背景图。虽然支持的图片格式多种多样，但是实际项目中，content 图片生成用得并不多，主要原因在于图片的尺寸不好控制，我们设置宽高无法改变图片的固有尺寸。所以，伪元素中的图片更多的是使用 background-image 模拟。
4. 了解 content 开启闭合符号生成。content 支持的属性值中有一对不常用的 open-quote 和 close-quote 关键字，顾名思义，就是“开启的引号”和“闭合的引号”，使用纯正的中文解释就是“上引号”和“下引号”。CSS 中还有 no-open-quote 和 no-close-quote 关键字 。
5. content attr 属性值内容生成。除了原生的 HTML 属性，自定义的 HTML 属性也是可以生成的。需要注意的是，attr 功能符中的属性值名称千万不要自以为是地在外面加个引号。
6. 深入理解 content 计数器。使用 CSS 计数器之前，必须重置一个值，默认是 0。使用`counter()`函数来给元素增加计数器。下面的 CSS 给每个 h3 元素的前面增加了"Section <计算器值>:"。CSS 计数器对创建有序列表特别有用，因为在子元素中会自动创建一个 CSS 计数器的实例。使用 `counters()` 函数，在不同级别的嵌套计数器之间可以插入字符串。比如这个 CSS 例子：

```css
/* 单个计算器 */
body {
  counter-reset: section; /* 重置计数器成0 */
}
h3:before {
  counter-increment: section; /* 增加计数器值 */
  content: "Section " counter(section) ": "; /* 显示计数器 */
}

/* 计算器嵌套 */
ol {
  counter-reset: section; /* 为每个ol元素创建新的计数器实例 */
  list-style-type: none;
}
li:before {
  counter-increment: section; /* 只增加计数器的当前实例 */
  content: counters(section, ".") " "; /* 为所有计数器实例增加以“.”分隔的值 */
}
```

7. content 内容生成的混合特性。所谓“content 内容生成的混合特性”指的是各种 content 内容生成语法是可以混合在一起使用的。

## 4.2 温和的 padding 属性

padding 指盒子的内补间。因为 CSS 中默认的 box-sizing 是 content-box，所以使用 padding 会增加元素的尺寸。内联元素 padding 对视觉层和布局层具有双重影响。实际上，对于非替换元素的内联元素，不仅 padding 不会加入行盒高度的计算，margin 和 border 也都是如此，都是不计算高度，但实际上在内联盒周围发生了渲染。

内联元素可以在不影响当前布局的情况下，优雅地增加链接或按钮的点击区域大小。利用内联元素的 padding 还可以实现高度可控的分割线。

```css
a + a:before {
  content: "";
  font-size: 0;
  padding: 10px 3px 1px;
  margin-left: 6px;
  border-left: 1px solid gray;
}
```

和 margin 属性不同，padding 属性是不支持负值的；其二，padding 支持百分比值，padding 百分比值无论是水平方向还是垂直方向均是相对于宽度计算的。利用这一特性可以实现一些有意思的布局效果，例如轻松实现自适应的等比例矩形效果。

```css
.box {
  padding: 10% 50%;
  position: relative;
}
.box > img {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
}
```

百分比值是应用在具有块状特性的元素上的。如果是内联元素，同样相对于宽度计算，默认的高度和宽度细节有差异，最特别的就是 padding 会断行。原因很简单，内联元素的垂直 padding 会让“幽灵空白节点”显现，也就是规范中的“strut”出现。

标签元素内置的 padding。ol/ul 列表内置 padding-left，但是单位是 px 不是 em，Chrome 浏览器下是 40px。很多表单元素都内置 padding 。例如`<input>`、`<button>`等等。

padding 属性和 background-clip 属性配合，可以在有限的标签下实现一些 CSS 图形绘制效果 。

## 4.3 激进的 margin 属性

margin 与元素尺寸以及相关布局。

margin 与元素的内部尺寸。对于 padding，元素设定了 width 或者保持“包裹性”的时候，会改变元素可视尺寸；但是对于 margin 则相反，元素设定了 width 值或者保持“包裹性”的时候，margin 对尺寸没有影响，只有元素是“充分利用可用空间”状态的时候，margin 才可以改变元素的可视尺寸。例如下面的代码，子元素的宽度就是 340 像素了，尺寸通过负值设置变大了。

```CSS
.box {
  width: 300px;
}
.son {
  margin: 0 -20px;
}
```

对于普通流体元素， margin 只能改变元素水平方向尺寸；但是，对于具有拉伸特性的绝对定位元素，则水平或垂直方向都可以，因为此时的尺寸表现符合“充分利用可用空间”。

由于 margin 具有这种流体特性下的改变尺寸特性，因此，margin 可以很方便地实现很多流体布局效果。例如列表块两端对齐，有三个列表，中间有 2 个 20 像素的间隙，浮动之后右侧有个 20 像素的间隙从而无法完美实现。通过给父容器添加`magin-right: -20px`就可以解决问题。

```css
ul {
  margin-right: -20px;
}
ul > li {
  float: left;
  width: 100px;
  margin-right: 20px;
}
```

margin 与元素的外部尺寸。对于外部尺寸，margin 属性的影响则更为广泛，只要元素具有块状特性，无论有没有设置 width/height，无论是水平方向还是垂直方向，即使发生了 margin 合并，margin 对外部尺寸都着着实实发生了影响。

通过设置内边距 padding 和外边距 margin 正负抵消，还可以在视觉多出一块可以使用的背景色，从而实现使用 margin 负值产生等高布局的效果。这个是针对具有块状特性的元素而言的，对于纯内联元素则不适用。

```css
.column-box {
  overflow: hidden;
}
.column-left,
.column-right {
  margin-bottom: -9999px;
  padding-bottom: 9999px;
}
```

上述 margin 对尺寸的影响是针对具有块状特性的元素而言的，对于纯内联元素则不适用。和 padding 不同，内联元素垂直方向的 margin 是没有任何影响的，既不会影响外部尺寸， 也不会影响内部尺寸，有种石沉大海的感觉。

margin 的百分比值。和 padding 属性一样， margin 的百分比值无论是水平方向还是垂直方向都是相对于宽度计算的。

块级元素的上外边距（ margin-top）与下外边距（margin-bottom）有时会合并为单个外边距，这样的现象称为“margin 合并”。合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。行内框、浮动框或绝对定位之间的外边距不会合并。同时，这种说法在不考虑 writing-mode 的情况下才是正确的。

margin 合并的 3 种场景。

- 相邻兄弟元素 margin 合并。对于兄弟元素的 margin 合并其作用和 em 类似，都是让图文信息的排版更加舒服自然。
- 父级和第一个/最后一个子元素。父子 margin 合并的意义在于：在页面中任何地方嵌套或直接放入任何裸`<div>`，都不会影响原来的块状布局。
- 空块级元素的 margin 合并。自身 margin 合并的意义在于可以避免不小心遗落或者生成的空标签影响排版和布局。

margin 合并的计算规则总结为“正正取大值”“正负值相加”“负负最负值” 3 句话。

深入理解 CSS 中的`margin: auto`。

`margin: auto`的填充规则是：如果一侧定值，一侧 auto，则 auto 为剩余空间大小；如果两侧均是 auto，则平分剩余空间。居中对齐左右同时 auto 计算即可。触发 margin:auto 计算有一个前提条件，就是 width 或 height 为 auto 时，元素是具有对应方向的自动填充特性的，因为在垂直上 height 是不符合条件的，所以不能运用这个方法进行垂直居中。

如果要进行垂直居中，可以使用两种方法。第一种方法是使用 writing-mode 改变文档流的方向。第二种方法是让绝对定位元素的 margin:auto 居中。

```css
.son {
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  width: 200px; height: 100px;
  margin: auto;
}
```

margin 无效情形解析。

- display 计算值 inline 的非替换元素的垂直 margin 是无效的，对于内联替换元素，垂直 margin 有效，并且没有 margin 合并的问题，所以图片永远不会发生 margin 合并。
- 表格中的`<tr>`和`<td>`元素或者设置 display 计算值是 table-cell 或 table-row 的元素的 margin 都是无效的。
- margin 合并的时候，更改 margin 值可能是没有效果的。
- 绝对定位元素非定位方位的 margin 值“无效”。主要是因为绝对定位元素的渲染是独立的。
- 定高容器的子元素的 margin-bottom 或者宽度定死的子元素的 margin-right 的定位“失效”。
- 鞭长莫及导致的 margin 无效。
- 内联特性导致的 margin 无效。因为有“幽灵空白节点” ，它们基于基线对齐。

## 4.4 功勋卓越的 border 属性

注意， border-style 的默认值是 none，有一部分人可能会误以为是 solid。这也是单纯设置 border-width 或 border-color 没有边框显示的原因 。

平常使用 border-width 几乎全是固定的数值，如 border-width:1px 之类，但是，可能有些人并不知道 border-width 还支持若干关键字，包括 thin、 medium（默认值）和 thick，

border-color 有一个很重要也很实用的特性，就是“border-color 默认颜色就是 color 色值”。具体来讲，就是当没有指定 border-color 颜色值的时候，会使用当前元素的 color 计算值作为边框色。

border 与透明边框技巧。虽然`color: transparent`在 IE9 以上版本的浏览器才支持，但是`border-color: transparent`在 IE7 浏览器就开始支持了，于是，我们解决一些棘手问题的思路就更加开阔了。

- 右下方 background 定位的技巧。
- 优雅地增加点击区域大小。比 padding 更加友好。
- 三角等图形绘制。border 属性可以轻松实现兼容性非常好的三角图形效果，其底层原因受 inset/outset 等看上去没有实用价值的 border-style 属性影响。

margin+padding 可以实现等高布局，同样，border 属性也可以实现等高布局。此方法要想生效，有一点需要注意，父级容器不能使用`overflow: hidden`清除浮动影响，因为溢出隐藏是基于 padding box 的，如果设置了`overflow: hidden`，则左浮动的导航列表元素就会被隐藏掉，这显然不是我们想要的效果。

```css
/* 导航背景区border创建 */
.box {
  border-left: 150px solid #333;
  background-color: #f0f3f9;
}
/* 布局主结构 */
.box > nav {
  width: 150px;
  margin-left: -150px;
  float: left;
}
.box > section {
  overflow: hidden;
}
```

# 第 5 章 内联元素与流

块级元素负责结构，内联元素接管内容，而 CSS 世界是面向图文混排，也就是内联元素设计的。

## 5.1 字母 x—CSS 世界中隐匿的举足轻重的角色

字母 x 与 CSS 世界的基线。在各种内联相关模型中，凡是涉及垂直方向的排版或者对齐的，都离不开最基本的基线（ baseline）。例如， line-height 行高的定义就是两基线的间距， vertical-align 的默认值就是基线。字母 x 的下边缘（线）就是我们的基线。

字母 x 与 CSS 中的 x-height。通俗地讲，x-height 指的就是小写字母 x 的高度，术语描述就是基线和等分线（mean line）（也称作中线 midline）之间的距离。在 CSS 世界中，middle 指的是基线往上 1/2 x-height 高度。我们可以近似理解为字母 x 交叉点那个位置。由此可见，`vertical-align: middle`并不是绝对的垂直居中对齐，我们平常看到的 middle 效果只是一种近似效果。原因很简单，因为不同的字体在行内盒子中的位置是不一样的。

字母 x 与 CSS 中的 ex。ex 是 CSS 中的一个相对单位，指的是小写字母 x 的高度，没错，就是指 x-height。ex 的价值就在其副业上——不受字体和字号影响的内联元素的垂直居中对齐效果。内联元素默认是基线对齐的，而基线就是 x 的底部，而 1ex 就是一个 x 的高度，通过使该元素（如图标）高度为 1ex ，同时背景图片居中，从而让其与文字垂直居中。

```css
.icon-arrow {
  display: inline-block;
  width: 20px;
  height: 1ex;
  background: url(arrow.png) no-repeat center;
}
```

## 5.2 内联元素的基石 line-height

`<div>`的高度是由行高 line-height 决定的，而非文字大小 font-size。对于非替换元素的纯内联元素，其可视高度完全由 line-height 决定,什么 padding、 border 属性对可视高度是没有任何影响的，这也是我们平常口中的“盒模型”约定俗成是块级元素的原因。

内联替换元素和内联非替换元素在一起时，由于同属内联元素，因此会共同形成一个“行框盒子”。在 HTML5 文档模式下，每一个“行框盒子”的前面都有一个宽度为 0 的“幽灵空白节点”，其内联特性表现和普通字符一模一样，所以，容器高度会等于 line-height 设置的属性值。

对于块级元素，line-height 对其本身是没有任何作用的，我们平时改变 line-height，块级元素的高度跟着变化，原因是改变了块级元素里面内联级别元素占据的高度。

```html
<style>
.box {
  line-height: 256px;
}
</style>
<div class="box">
  <img src="1.jpg" height="128">
</div>
```

line-height 在这个混合元素的“行框盒子”中扮演的角色是决定这个行盒的最小高度。原因有两个，一是替换元素的高度不受 line-height 影响，二是 vertical-align 属性在背后作祟。

因为 line-height 几乎无处不在的继承特性，并且 CSS 世界是为了更好地图文展示，所以 line-height 不仅是内联元素高度的基石，而且还是整个 CSS 世界高度体系的基石。

要让单行文字垂直居中，只需要 line-height 这一个属性就可以，与 height 一点儿关系都没有。其实，line-height 可以让单行或多行元素近似垂直居中。

```css
.title {
  line-height: 24px;
}
```

单行文本可以垂直居中的原因是 CSS 中“行距的上下等分机制”，但如果行距的添加规则是在文字的上方或者下方，则行高是无法让文字垂直居中的。说“近似”是因为文字字形的垂直中线位置，普遍要比真正的“行框盒子”的垂直中线位置低。

多行文本或者替换元素的垂直居中实现原理和单行文本就不一样了，需要 line-height 属性的好朋友 vertical-align 属性帮助才可以。

```html
<style>
.box {
  line-height: 120px;
}
.content {
  display: inline-block;
  vertical-align: middle;
}
</style>

<div class="box">
  <div class="content">基于行高实现的多行文字垂直居中效果，需要vertical-align属性帮助。</div>
</div>
```

实现的原理大致是有两点。

- 多行文本使用一个标签包裹，然后设置 display 为 inline-block。好处在于既重置外部的 line-height 为正常的大小，又能保持内联元素特性，从而可以设置 vertical-align 属性，以及产生非常关键的"行框盒子"，这样就能在`.content`元素前面撑起了一个高度为 120px 的宽度为0 的内联元素。
- 因为内联元素默认都是基线对齐的，所以通过对`.content`元素`vertical-align: middle`来调整多行文本的垂直位置，从而实现想要的垂直居中效果。如果是要借助 line-height 实现图片垂直居中效果，也是类似的原理和做法。

深入line-height 的各类属性值。line-height 的默认值是 normal，还支持数值、百分比值以及长度值。 乍一看，似乎`line-height: 1.5`、`line-height: 150%`和`line-height: 1.5em`这 3 种用法是一模一样的，最终的行高大小都是和 font-size 计算的值，但是实际上，`line-height: 1.5`和另外两个有一点儿不同，那就是继承细节有所差别。如果使用数值（1.5）作为 line-height 的属性值，那么所有的子元素继承的都是这个已计算的数值；但是，如果使用百分比值（150%）或者长度值（1,5em）作为属性值，那么所有的子元素继承未计算前的值。

```css
.box   { font-size: 14px; }

/* 当h3字体为32px时，子元素继承结果值48px */
.box-1 { line-height: 1.5; }

/* 当h3字体为32px时，子元素继承结果值21px */
.box-2 { line-height: 150%; }
.box-3 { line-height: 1.5em; }

h3 { font-size: 32px; }
p  { font-size: 20px; }
```

内联元素 line-height 的“大值特性”。无论内联元素 line-height 如何设置，最终父级元素的高度都是由数值大的那个 line-height 决定的，称之为“内联元素 line-height 的大值特性”。因为“幽灵空白节点”的干扰会让内联元素的行高增大，而行框盒子的高度是由高度最高的那个“内联盒子”决定的。所以，通过设置子元素`display: inline-block`，创建一个独立的“行框盒子”，这样元素设置的 line-height 才可以生效了,这也是多行文本垂直居中设置的原因。

## 5.3 line-height 的好朋友 vertical-align

抛开 inherit 这类全局属性值不谈，vertical-align 属性值分为以下 4 类：

- 线类，如 baseline（默认值）、 top、 middle、 bottom；
- 文本类，如 text-top、 text-bottom；
- 上标下标类，如 sub、 super；
- 数值百分比类，如 20px、 2em、 20%等。

由于 vertical-align 的默认值是 baseline，即基线对齐，而基线的定义是字母 x 的下边缘。因此，内联元素默认都是沿着字母 x 的下边缘对齐的。对于图片等替换元素，往往使用元素本身的下边缘作为基线，所以默认值为 baseline 的内联文字通常与图片对齐。由于是相对字母 x 的下边缘对齐，而中文和部分英文字形的下边缘要低于字母 x 的下边缘，因此，会给人感觉文字是明显偏下的，一般都会进行调整。

根据计算值的不同，相对于基线往上或往下偏移。如果 vertical-align 的计算值是正值则往上偏移，如果是负值则往下偏移。这里的 vertical-align 属性的百分比值则是相对于 line-height 的计算值计算的。

vertical-align 起作用是有前提条件的，这个前提条件就是：只能应用于内联元素以及 display 值为 table-cell 的元素。换句话说，vertical-align 属性只能作用在 display 计算值为 inline、 inline-block、inline-table 或 table-cell 的元素上。在 CSS 世界中，有一些 CSS 属性值会在背后默默地改变元素 display 属性的计算值，从而导致 vertical-align 不起作用，例如浮动和绝对定位会让元素块状化。

```css
.example {
  float: left;
  vertical-align: middle; /* 没有作用 */
}
.example {
  position: absolute;
  vertical-align: middle; /* 没有作用 */
}
```

有时候只设置 height 而没有设置 line-height 也会让 vertical-align 不生效，因为行框盒子前面的“幽灵空白节点”高度太小，只有设置一个足够大的行高给“幽灵空白节点”才能让它起作用。

```html
<style>
.box {
  height: 128px;
  line-height: 128px; /* 关键 CSS 属性 */
}
.box > img {
  height: 96px;
  vertical-align: middle;
}

</style>
<div class="box">
  <img src="1.jpg">
</div>
```

对 table-cell 元素而言， vertical-align 起作用的是 table-cell 元素自身。

```css
.cell {
  height: 128px;
  display: table-cell;
  vertical-align: middle;
}
.cell > img {
  height: 96px;
}
```

vertical-align 和 line-height 之间的关系。第一点是，前者的百分比值时相对于后者计算的。

同时容器与行高不相等也是这两个的问题。

```html
<style>
.box { line-height: 32px; }
.box > span { font-size: 24px; }
</style>

<div class="box">
  <span>文字</span>
</div>
```

`<span>`标签前面实际上有一个看不见的类似字符的“幽灵空白节点”。对字符而言， font-size 越大字符的基线位置越往下，因为文字默认全部都是基线对齐，所以当字号大小不一样的两个文字在一起的时候，彼此就会发生上下位移，如果位移距离足够大，就会超过行高的限制，而导致出现意料之外的高度。让“幽灵空白节点”和后面`<span>`元素字号一样大。或者改变垂直对齐方式，如顶部对齐，这样就不会有参差位移了。

图片底部留有间隙的问题也是“幽灵空白节点”、line-height 和 vertical-align 属性这三个属性作怪。字母 x 往下的行高产生的多余的间隙就嫁祸到图片下面，让人以为是图片产生的间隙。解决办法是，使图片块状化、或让容器 line-height 足够小、或让容器 font-size 足够小，或将图片设置其他 vertical-align 属性值。

```css
.box {
  width: 280px;
  outline: 1px solid #aaa;
}
.box img {
  height: 96px;
}
/* 间隙清除方法 */
.box-1 img {
  display: block;
  margin: auto;
}
.box-2 {
  line-height: 0;
}
.box-3 {
  font-size: 0;
}
.box-4 img {
  vertical-align: bottom;
}
```

vertical-align 属性的默认值 baseline 在文本之类的内联元素那里就是字符 x 的下边缘，对于替换元素则是替换元素的下边缘。但是，如果是 inline-block 元素，则规则要复杂了：一个 inline-block 元素，如果里面没有内联元素，或者 overflow 不是 visible， 则该元素的基线就是其 margin 底边缘；否则其基线就是元素里面最后一行内联元素的基线。

最佳图标实践 CSS。小图标和文字对齐完全不受 font-size 大小的影响。

```html
<div class="box">
  <h4>1. 空标签后面跟随文本</h4>
  <p><i class="icon icon-delete"></i>删除</p>
  <h4>2. 标签里面有“删除”文本</h4>
  <p><i class="icon icon-delete">删除</i>随便什么文字</p>
</div>
```

```css
.box {
  line-height: 20px;
}
.icon {
  display: inline-block;
  width: 20px;
  height: 20px;
  white-space: nowrap;
  letter-spacing: -1em;
  text-indent: -999em;
}
.icon:before {
  content: "\3000";
}
.icon-delete {
  background: url(delete.png) no-repeat center;
}
```

`vertial-align: top`和`vertial-align: bottom`基本表现类似，只是一个“上”一 个“下”，因此合在一起讲。顾名思义，`vertial-align:top`就是垂直上边缘对齐，具体定义如下。内联元素：元素底部和当前行框盒子的顶部对齐。table-cell 元素：元素底 padding 边缘和表格行的顶部对齐。  
`vertial-align: middle`近似垂直居中的原因与定义有关。内联元素：元素的垂直中心点和行框盒子基线往上 1/2 x-height 处对齐。table-cell 元素：单元格填充盒子相对于外面的表格行居中对齐。

深入理解 vertical-align 文本类属性值。`vertical-align: text-top`：盒子的顶部和父级内容区域的顶部对齐。`vertical-align: text-bottom`：盒子的底部和父级内容区域的底部对齐。

简单了解 vertical-align 上标下标属性值。vertical-align 上标下标类属性值指的就是 sub 和 super 两个值，分别表示下标和上标。在 HTML 代码中，有两个标签语义就是下标和上标，分别是上标`<sup>`和下标`<sub>`。

基于 vertical-align 属性的水平垂直居中弹框。

```css
.container {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
  text-align: center;
  font-size: 0;
  white-space: nowrap;
  overflow: auto;
}
.container:after {
  content: "";
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
.dialog {
  display: inline-block;
  vertical-align: middle;
  text-align: left;
  font-size: 14px;
  white-space: normal;
}
```

# 第 6 章 流的破坏与保护

CSS 世界中正常的流内容或者流布局虽然也足够强大，但是实现的总是方方正正、规规矩矩的效果，有时候我们希望有一些特殊的布局表现，例如，文字环绕效果，或者元素固定在某些位置。因此，CSS 中有一类属性，专门通过破坏正常的“流”来实现一些特殊的样式表现。

## 6.1 魔鬼属性 float

浮动的本质就是为了实现文字环绕效果。 而这种文字环绕，主要指的就是文字环绕图片显示的效果。

float 好像也像流一样满足我们布局页面的需求，但是实际上，这种布局方案缺少弹性。举个例子，一旦某个列表高度变高了，则下面的列表就可能发生不愿看到的布局错位，布局的容错性很糟糕。

float 属性的种种归根结底还是由于自身各种特性导致的。 float 特性具体如下：

- 包裹性
- 块状化并格式化上下文
- 破坏文档流
- 没有任何 margin 合并

包裹性。所谓“包裹性”，由“包裹”和“自适应性”两部分组成。假设浮动元素父元素宽度 200px，浮动元素子元素是一个 128px 宽度的图片，则此时浮动元素宽度表现为“包裹”，就是里面图片的宽度 128px；自适应就是，如果浮动元素的子元素不只是一张 128px 宽度的图片，还有一大波普通的文字。则此时浮动元素宽度就自适应父元素的 200px 宽度，最终的宽度表现也是 200px。

块状化并格式化上下文。元素一旦 float 的属性值不为 none，则其 display 计算值就是 block 或者 table，所以浮动后的元素可以设置宽度和高度等。同时浮动会触发块级格式化上下文（BFC）。

破坏文档流。为了实现文字环绕的效果而进行破坏文档流，而“文字环绕效果” 是由两个特性（即“父级高度塌陷”和“行框盒子区域限制”）共同作用的结果。行框盒子如果和浮动元素的垂直高度有重叠，则行框盒子在正常定位状态下只会跟随浮动元素，而不会发生重叠。注意，这里说的是“行框盒子”，也就是每行内联元素所在的那个盒子，而非外部的块状盒子。实际上，由于浮动元素的塌陷，块状盒子是和图片完全重叠的。

没有任何 margin 合并；如果一个元素具有 BFC，内部子元素再怎么翻江倒海、翻云覆雨，都不会影响外部的元素。所以， BFC 元素是不可能发生 margin 重叠的，因为 margin 重叠是会影响外面的元素的。

我们需要了解两个和 float 相关的术语， 一是“浮动锚点”（float anchor），二是“浮动参考”（float reference）。

- 浮动锚点是 float 元素所在的“流”中的一个点，这个点本身并不浮动，就表现而言更像一个没有 margin、 border 和 padding 的空的内联元素。
- 浮动参考指的是浮动元素对齐参考的实体。

在 CSS 世界中，float 元素的“浮动参考”是“行框盒子”，也就是 float 元素在当前 “行框盒子”内定位。如果 float 元素前后全是块元素，那就要靠浮动锚点进行对齐。

我们可以利用 float 破坏 CSS 正常流的特性，实现两栏或多栏的自适应布局。一边元素没有浮动，也没有设置宽度，因此，流动性保持得很好。同时设置 margin、border 或者 padding 都可以自动改变 content box 的尺寸， 继而实现了宽度自适应布局效果。如果是百分比宽度，则也是可以的。

```
<div class="father">
    <img src="zxx.jpg">
    <p class="girl">美女1，美女2，美女3，美女4，美女5，美女6，后宫1，后宫2，后宫36</p>
</div>

.father {
    border: 1px solid #444;
    overflow: hidden;
}
.father > img {
    width: 60px; height: 64px;
    float: left;
}
.girl {
    /* 环绕和自适应的区别所在 */
    margin-left: 70px;
}
```

## 6.2 float 的天然克星 clear

官方对 clear 属性的解释是：“元素盒子的边不能和前面的浮动元素相邻。” clear 属性指定一个元素是否可以在它之前的浮动元素旁边，或者必须向下移动(清除浮动) 到这些浮动元素的下面。clear 属性适用于浮动和非浮动元素。

clear 属性时让自身不能和前面的浮动元素相邻。考虑到 float 属性要么就 left 要么就 right，不可能同时存在，同时由于 clear 属性对“后面的”浮动元素时不闻不问的。所以当`clear: left`有效的时候，`clear: right`必定无效，也就是此时`clear: left`等同于设置`clear both`；同样的，`clear: right`如果有效也是等同于设置`clear: both`。由此可见，`clear:left`和`clear:right`这两个声明就没有任何使用的价值，至少在 CSS 世界中是如此，直接使用`clear:both`就行（针对一个浮动相邻元素）。

clear 属性只有块级元素才有效的，而::after 等伪元素默认都是内联水平，这就是借助伪元素清除浮动影响时需要设置 display 属性值的原因。

由于`clear: both`的作用本质是让自己不和 float 元素在一行显示，并不是真正意义上的清除浮动，因此 float 元素的一些不好的特性依然存在，于是，会有类似下面的现象。

- 如果`clear:both`元素前面的元素就是 float 元素，则`margin-top`负值即使设成-9999px，也不见任何效果。
- `clear:both`后面的元素依旧可能会发生文字环绕的现象。

当应用于非浮动块时，它将非浮动块的边框边界移动到所有相关浮动元素外边界的下方。这个非浮动块的垂直外边距会折叠。另一方面，两个浮动元素的垂直外边距将不会折叠。当应用于浮动元素时，它将元素的外边界移动到所有相关的浮动元素外边界的下方。这会影响后面浮动元素的布局，后面的浮动元素的位置无法高于它之前的元素。

注释:如果你想要一个元素将所有浮动元素包含在内（解决浮动元素 float 使其父元素高度塌陷），你既可以将这个容器设置为浮动，又可以通过 `::after` 伪元素设置 clear 属性作为替代。还有三种方法是，给父元素一个固定高度；添加一个块级元素，并给此元素设置`clear:both`清除浮动；给父元素添加 `overflow：hidden；`。

## 6.3 CSS 世界的结界——BFC

BFC 全称为 block formatting context，中文为“块级格式化上下文”。相对应的还有 IFC， 也就是 inline formatting context，中文为“内联格式化上下文”。

如果一个元素具有 BFC，内部子元素再怎么翻江倒海、翻云覆雨，都不会影响外部的元素。所以， BFC 元素是不可能发生 margin 重叠的，因为 margin 重叠是会影响外面的元素的； BFC 元素也可以用来清除浮动的影响，因为如果不清除，子元素浮动则父元素高度塌陷，必然会影响后面元素布局和定位，这显然有违 BFC 元素的子元素不会影响外部元素的设定。

触发 BFC 的常见情况如下：

- `<html>`根元素；
- float 的值不为 none；
- overflow 的值为 auto、 scroll 或 hidden；
- display 的值为 table-cell、 table-caption 和 inline-block 中的任何一个；
- position 的值不为 relative 和 static。

换言之，只要元素符合上面任意一个条件，就无须使用`clear: both`属性去清除浮动的影响了。因此，不用见到一个`<div>`元素就加个`.clearfix`的类名。

BFC 的结界特性最重要的用途其实不是去 margin 重叠或者是清除 float 影响，而是实现更健壮、更智能的自适应布局。普通流体元素在设置了`overflow: hidden`后，会自动填满容器中除了浮动元素以外的剩余空间，形成自适应布局效果，而且这种自适应布局要比纯流体自适应更加智能。

如果想要让浮动元素与旁边的 BFC 结界保持合适的间距，那也很简单，如果元素是左浮动，则浮动元素可以设置 margin-right 或透明 border-right 或 padding-right；又或者右侧 BFC 元素设置成透明 border-left 或者 padding-left，但不包括 margin-left，因为如果想要使用 margin-left，则其值必须是浮动元素的宽度加间隙的大小，就变成动态不可控的了，无法大规模复用。

```css
img {
  margin-right: 10px;
}
img {
  border-right: 10px solid transparent;
}
img {
  padding-right: 10px;
}
.animal {
  border-left: 10px solid transparent;
}
.animal {
  padding-right: 10px;
}
```

和基于纯流体特性实现的两栏或多栏自适应布局相比，基于 BFC 特性的自适应布局有如下优点。

- 自适应内容由于封闭而更健壮，容错性更强。比方说，内部设置 clear:both 不会与 float 元素相互干扰而导致错位。
- 自适应内容自动填满浮动以外区域，无须关心浮动元素宽度，可以整站大规模应用。

但是，由于绝大多数的触发 BFC 的属性自身有一些古怪的特性，所以，实际操作的时候，能兼顾流体特性和 BFC 特性来实现无敌自适应布局的属性并不多。下面是常见的 CSS 属性说明。

- `float: left`。浮动元素本身 BFC 化，然而浮动元素有破坏性和包裹性，失去了元素本身的流体自适应性，因此，无法用来实现自动填满容器的自适应布局。

- `position: absolute`。脱离文档流严重，与非定位元素没有配合。

- `overflow: hidden`。块状元素的流体特性保存得相当完好，不仅有着 BFC 的独立区域特性，而且 overflow:hidden 的 BFC 特性从 IE7 浏览器开始就支持， 兼容性也很不错。唯一的问题就是容器盒子外的元素可能会被隐藏掉，一定程度上限制了这种特性的大规模使用。

- `display: inline-block`。其会让元素尺寸包裹收缩，完全不是想要的 block 水平的流动特性。但是在 IE6 和 IE7 浏览器下， block 水平的元素设置`display: inline-block`元素还是 block 水平，也就是还是会自适应容器的可用宽度显示。 当然， `*zoom: 1` 也是类似效果，不过只适用于低级的 IE 浏览器，如 IE7 。

- `display: table-cell`。其让元素表现得像单元格一样， IE8 及以上版本浏览器才支持。它会跟随内部元素的宽度显示，但是，宽度值设置得再大，实际宽度也不会超过表格容器的宽度。如果我们把`display: table-cell`这个 BFC 元素宽度设置得很大，那其实就跟 block 水平元素自动适应容器空间效果一模一样了。

## 6.4 最佳结界 overflow

要想彻底清除浮动的影响，最适合的属性不是 clear 而是 overflow。一般使用`overflow: hidden`，利用 BFC 的“结界”特性彻底解决浮动对外部或兄弟元素的影响。虽然有许多其他 CSS 声明也能清除浮动，但是基本上都会让元素的宽度表现为“包裹性”，也就是会影响原来的样式布局。

一个设置了 overflow:hidden 声明的元素，当其子元素内容超出容器宽度高度限制的时候，剪裁的边界是 border box 的内边缘，而非 padding box 的内边缘。所以我们在实际项目开发的时候，要尽量避免滚动容器设置 padding-bottom 值。

自 IE8 以上版本的浏览器开始， overflow 属性家族增加了两个属性，就是这里的 overflow-x 和 overflow-y，分别表示单独控制水平或垂直方向上的剪裁规则。支持的属性值和 overflow 属性一模一样。

- visible：默认值。
- hidden：剪裁。
- scroll：滚动条区域一直在。
- auto：不足以滚动时没有滚动条，可以滚动时滚动条出现。

但是，除非 overflow-x 和 overflow-y 的属性值都是 visible，否则 visible 会当成 auto 来解析。换句话说，永远不可能实现一个方向溢出剪裁或滚动，另一方向内容溢出显示的效果。

HTML 中有两个标签是默认可以产生滚动条的，一个是根元素`<html>`，另一个是文本域 `<textarea>`。之所以可以出现滚动条，是因为这两个标签默认的 overflow 属性值不是 visible，从 IE8 浏览器开始，都使用 auto 作为默认的属性值。 在 PC 端，无论是什么浏览器，默认滚动条均来自`<html>`，而不是`<body>`标签。同时，滚动条会占用容器的可用宽度或高度。

在 CSS 世界中，很多属性要想生效都必须要有其他 CSS 属性配合，其中有一种效果就离不开`overflow: hidden`声明，即单行文字溢出点点点效果。虽然效果的核心是`text-overflow: ellipsis`，效果实现必需的 3 个声明如下：

```css
.ell {
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
```

目前，对`-webkit-`私有前缀保持良好的浏览器还可以实现多行文本打点效果，但是却无需依赖`overflow: hidden`。比方说，最多显示 2 行内容，再多就打点的核心 CSS 代码时：

```css
.ell-row-2 {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
}
```

锚点，通俗点的解释就是可以让页面定位到某个位置的点。其在高度较高的页面中经常见到，如百度百科页面中标题条目的快速定位效果。

基于 URL 地址的锚链（如上面的`#1`，可以使用 location.hash 获取）实现锚点跳转的方法有两种，一种是`<a>`标签以及 name 属性，还有一种就是使用标签的 id 属性。

锚点定位行为的触发条件，一是 URL 地址中的锚链与锚点元素对应并有交互行为。二是 可 focus 的锚点元素处于 focus 状态。

锚点定位作用的本质。锚点定位行为的发生，本质上是通过改变容器滚动高度或者宽度来实现的。首先，锚点定位也可以发生在普通的容器元素上，而且定位行为的发生是由内而外的。“由内而外”指的是，普通元素和窗体同时可滚动的时候，会由内而外触发所有可滚 动窗体的锚点定位行为。其次就是设置了`overflow: hidden`的元素也是可滚动的，因为锚点定位本质上是改变了 scrollTop 或 scrollLeft 值。

知道`overflow:hidden`元素依然可以滚动，可以帮助我们实现无 JavaScript 的选项卡效果。但却有不少不足之处：其一，容器高度需要固定；第二，也是最麻烦的，就是“由内而外”的锚点定位会触发窗体的重定位，也就是说，如果页面也是可以滚动的，则点击选项卡按钮后页面发生跳动。

```
<div class="box">
  <div class="list" id="one">1</div>
  <div class="list" id="two">2</div>
  <div class="list" id="three">3</div>
  <div class="list" id="four">4</div>
</div>
<div class="link">
  <a href="#one">1</a>
  <a href="#two">2</a>
  <a href="#three">3</a>
  <a href="#four">4</a>
</div>

.box {
  height: 10em;
  border: 1px solid #ddd;
  overflow: hidden;
}
.list {
  line-height: 10em;
  background: #ddd;
}
```

知道`overflow:hidden`元素依然可以滚动，还可以帮助我们理解一些现象发生的原因。例如，之前提到过的使用 margin-bottom 负值加 padding-bottom 正值以及父元素 overflow:hidden 配合实现的等高布局，在大多数情况下，这种布局使用是没有任何问题的，但是如果使用`dom.scrollIntoView()`或者触发窗体视区范围之外的内部元素的锚点定位行为，布局就会飞掉，没错，布局就像长了翅膀一样飞掉了。

## 6.5 float 的兄弟 position:absolute

当 absolute 和 float 同时存在的时候，float 属性是无任何效果的。因此，没有任何理由 absolute 和 float 同时使用。但是两者都具有很多相似的属性。

- “块状化”和浮动类似，元素一旦 position 属性值为 absolute 或 fixed，其 display 计算值就是 block 或者 table。
- “破坏性”，指的是破坏正常的流特性。和 float 类似，虽然 absolute 破坏正常的流来实现自己的特性表现，但本身还是受普通的流体元素布局、位置甚至一些内联相关的 CSS 属性影响的。
- 两者都能“块状格式化上下文”， 也就是 BFC。
- 两者都具有“包裹性”，也就是尺寸收缩包裹，同时具有自适应性。和 float 或其他“包裹性”声明带来的“自适应性”相比，absolute 有一个平时不太被人注意的差异，那就是 absolute 的自适应性最大宽度往往不是由父元素决定的，本质上说，这个差异是由“包含块”的差异决定的。换句话说， absolute 元素具有与众不同的“包含块”。

absolute 的包含块。包含块（containing block）这个就是元素用来计算和定位的一个框。根元素（很多场景下可以看成是`<html>`）被称为“初始包含块”，其尺寸等同于浏览器可视窗口的大小。对于其他元素，如果该元素的 position 是 relative 或者 static，则“包含块” 由其最近的块容器祖先盒的 content box 边界形成。如果元素`position: fixed`，则“包含块”是“初始包含块”。如果元素`position: absolute`，则“包含块”由最近的 position 不为 static 的祖先元素建立，具体方式如下。

如果该祖先元素是纯 inline 元素，则规则略复杂：假设给内联元素的前后各生成一个宽度为 0 的内联盒子（ inline box），则这两个内联盒子的 padding box 外面的包围盒就是内联元素的“包含块”；如果该内联元素被跨行分割了，那么“包含块”是未定义的，也就是 CSS2.1 规范并没有明确定义，浏览器自行发挥。 否则，“包含块”由该祖先的 padding box 边界形成。如果没有符合条件的祖先元素，则“包含块”是“初始包含块”。

和常规元素相比， absolute 绝对定位元素的“包含块”有以下 3 个明显差异：

- 内联元素也可以作为“包含块”所在的元素。
- “包含块”所在的元素不是父块级元素，而是最近的 position 不为 static 的祖先元素或根元素。
- 边界是 padding box 而不是 content box。

具有相对特性的无依赖 absolute 绝对定位。absolute 是非常独立的 CSS 属性值，其样式和行为表现不依赖其他任何 CSS 属性就可以完成。定位效果实现完全不需要父元素设置 position 为 relative 和子元素设置 left/top/ right/bottom 属性值，这种绝对定位称为“无依赖绝对定位”。“无依赖绝对定位”本质上就是“相对定位”，仅仅是不占据 CSS 流的尺寸空间而已。一个简简单单的`position: absolute`，然后通过 margin 属性进行定位，效果即达成。

要实现导航文字右上方的定位很简单，直接对加图标这个元素进行样式设定就可以了了，原来纯文字导航时的样式完全不需要有一丁点儿的修改。实际上，即使是普通的水平对齐的图标也可以使用“无依赖绝对定位”实现。此方法兼容性很好，与 inline-block 对齐相比的好处在于，inline-block 对齐的最终行框并不是 20px，因为中文下沉，图标居中，要想视觉上水平，图标 vertical-align 对齐要比实际低一点，这就会导致最终整个航诳的高度是 21px 或者更大。

```
<span class="icon-x">
  <i class="icon-warn"></i>邮箱格式不准确
</span>
.icon-x {
  line-height: 20px;
  padding-left: 20px;
}
.icon-warn {
  position: absolute;
  margin-left: -20px;
  width: 20px; height: 20px;
  background: url(warn.png) no-repeat center;
}
```

超越常见布局的排版。为了保证视觉舒适，往往会让表单水平居中对齐，如果提示信息出现在输入框后面，为了让默认状态下表单水平居中，就会有宽度不够的问题，但使用“无依赖绝对定位”就不存在这个问题了。表单标签名字前面的星号也是典型的“无依赖绝对定位”，自身绝对定位，然后通过 margin-left 负值偏移实现。不过虽然“无依赖绝对定位”好处多，但是一般只用在静态交互效果上，如果是动态呈现的列表，建议还是使用 JavaScript 来计算和定位。

进一步深入“无依赖绝对定位”。虽然说元素`position: absolute`后的 display 计算值都是块状的，但是其定位的位置和没有设置时候的位置有关。

按道理讲，absolute 和 float 一样，都可以让元素块状化，应该不会受控制内联元素对齐的 text-align 属性影响，但是 text-align 居然可以改变 absolute 元素的位置。这里之所以产生了位置变化，本质上是“幽灵空白节点”和“无依赖绝对定位”共同作用的结果。需要注意的是，只有原本是内联水平的元素绝对定位后可以受 text-align 属性影响。

这是非常简约的定位表现。此时，只要 margin-left 一半图片宽度负值大小，就可以实现图片的水平居中效果了，与元素`position: relative`然后定位元素设置`left: 50%`的方法相比，其优势在于不需要改变父元素的定位属性，避免可能不希望出现的层级问题等。如果不兼容，还可以通过插入显式的内联字符，而非借助缥缈的“幽灵空白节点”实现所有浏览器下的一致表现。

```
<p><img src="1.jpg"></p>

p {
  text-align: center;
}
img {
  position: absolute;
}
```

利用 text-align 控制 absolute 元素的定位最适合的使用场景就是主窗体右侧的“返回顶部”以及“反馈”等小布局的实现。使用`:before`伪元素在前面插入一个空格，此时设置`.alignright`为`text-align: right`，则此空格对齐主结构的右边缘显示，后面的固定定位元素（同绝对定位元素）由于“无依赖定位”特性，左边缘正好就是主结构的右边缘，天然跑到主结构的外面显示了。设置`height：0; overflow: hidden`可以让空格不占据位置，从而让元素不影响主结构的布局。

```
<div class="alignright">
  <span class="follow"></span>
</div>

.alignright {
  height: 0;
  text-align: right;
  overflow: hidden;
}
.alignright:before {
  content: "\2002";
}
.follow {
  position: fixed;
  bottom: 100px;
  z-index: 1;
}
```

## 6.6 absolute 与 overflow

如果 overflow 容器不是定位元素，同时绝对定位元素和 overflow 容器之间也没有定位元素， 则 overflow 容器无法对 absolute 元素进行剪裁。但是，虽然绝对定位元素不能让滚动条出现，非绝对定位元素可以，因此可能当容器滚动时，绝对定位元素纹丝不动，不跟着滚动，表现类似 fixed 固定定位。

最后，非常有必要补充一点，那就是由于`position: fixed`固定定位元素的包含块是根元素，因此，除非是窗体滚动，否则上面讨论的所有 overflow 剪裁规则对固定定位都不适用。

但是，随着 CSS3 新世界到来的冲击，规则在不经意间发生了一些变化，其中最明显的就是 transform 属性对 overflow 剪裁规则的影响。transform 同时对层叠上下文以及`position: fixed`的渲染都有影响。

## 6.7 absolute 与 clip

CSS 世界中有些属性或者特性必须和其他属性一起使用才有效，比方说剪裁属性 clip。clip 属性要想起作用，元素必须是绝对定位或者固定定位，也就是 position 属性值必须是 absolute 或者 fixed。

对于普通元素或者绝对定位元素，想要对其进行剪裁，我们可以利用语义更明显的 overflow 属性，但是对于`position: fixed`元素，overflow 属性往往就力不能及了，因为 fixed 固定定位元素的包含块是根元素。此时就要用 clip 属性。

```css
.fixed-clip {
  position: fixed;
  clip: rect(30px 200px 200px 20px);
}
```

所谓“可访问性隐藏”，指的是虽然内容肉眼看不见，但是其他辅助设备却能够进行识别和访问的隐藏。clip 剪裁被为“最佳可访问性隐藏”的另外一个原因就是，它具有更强的普遍适应性，任何元素、任何场景都可以无障碍使用。

许多网站都有包含自己网站名称的标识 logo，而这些标识一般都是图片，为了更好地 SEO 以及无障碍识别，一般会使用`<h1>`标签写上网站的名称，那么隐藏文字通常有以下一些技术选型。

- 下策是`display: none`或者`visibility: hidden`隐藏，因为屏幕阅读设备会忽略这里的文字。
- text-indent 缩进是中策，但文字如果缩进过大，大到屏幕之外，屏幕阅读设备也是不会读取的。
- `color:transparent`是移动端上策，但却是桌面端中策，因为原生 IE8 浏览器并不支持它`color:transparent`声明，很难用简单的方式阻止文本被框选。
- clip 剪裁隐藏是上策，既满足视觉上的隐藏，屏幕阅读设备等辅助设备也支持得很好。

clip 裁剪称为“最佳可访问性隐藏”的另外一个原因就是，它具有更强的普遍应用性，任何元素、任何场景都可以无障碍使用。

clip 隐藏仅仅是决定了哪部分是可见的，非可见部分无法响应点击事件等；然后，虽然视觉上隐藏，但是元素的尺寸依然是原本的尺寸，在 IE 浏览器和 Firefox 浏览器下抹掉了不可见区域尺寸对布局的影响，Chrome 浏览器却保留了。

## 6.8 absolute 的流体特性

当 absolute 遇到 left/top/right/bottom 属性的时候，absolute 元素才真正变成绝对定位元素。`left: 0; top: 0;` 表示相对于绝对定位元素包含块的左上角对齐，此时原本的相对特性丢失。如果我们仅设置了一个方向的绝对定位，例如`left: 0`，此时，水平方向绝对定位，但垂直方向的定位依然保持了相对特性。

当一个绝对定位元素，其对立定位方向属性同时有具体定位数值的时候，流体特性就发生了。假设`.box`元素的包含块是根元素，则下面的代码可以让`.box`元素正好完全覆盖浏览器的可视窗口，并且如果改变浏览器窗口大小，`.box`会自动跟着一起变化：

```css
.box {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
}
```

如果再将`.box`元素设定宽高都是 100% ，就完全丧失了流动性。所以设置了对立属性的绝对定位元素的表现神似普通`<div>`元素，无论设置 padding 还是 margin，占据的空间一直不变，变化的就是 content box 的尺寸，这就是典型的流体表现特性。

所以，如果想让绝对定位元素宽高自适应于包含块，没有理由不使用流体特性写法，除非是替换元素的拉伸。而绝对定位元素的这种流体特性比普通元素要更强大，普通元素流体特性只有一个方向，默认是水平方向，但是绝对定位元素可以让垂直方向和水平方向同时保持流动性。

当绝对定位元素处于流体状态的时候，各个盒模型相关属性的解析和普通流体元素都是一模一样的， margin 负值可以让元素的尺寸更大，并且可以使用`margin: auto`让绝对定位元素保持居中。

绝对定位元素的`margin: auto`的填充规则和普通流体元素的一模一样。唯一的区别在于，绝对定位元素`margin: auto`居中从 IE8 浏览器开始支持，而普通元素的`margin: auto`居中很早就支持了。

```css
/*如果项目不需要管 IE7 浏览器的话，
下面这种绝对定位元素水平垂直居中用法就可以直接淘汰了：*/
.element {
  width: 300px;
  height: 200px;
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -150px;
  margin-top: -100px;
}

/*如果绝对定位元素的尺寸是已知的，也没有必要使用下面这种用法，因为按照我的经验，
在有些场景下，百分比 transform 会让 iOS 微信闪退，还是尽量避免的好。*/
.element {
  width: 300px;
  height: 200px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}

/*首推的方法就是利用绝对定位元素的流体特性和 margin:auto 的自动分配特性实现居中，例如：*/
.element {
  width: 300px;
  height: 200px;
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  margin: auto;
}
```

## 6.9 position:relative 才是大哥

虽然说 relative/absolute/fixed 都能对 absolute 的“包裹性”以及“定位”产生限制，但只有 relative 可以让元素依然保持在正常的文档流中。relative 的定位有两大特性：一是相对自身；二是无侵入。使用 relative 定位的元素，其相对的是自身进行偏移。 “无侵入”的意思是，当 relative 进行定位偏移的时候，一般情况下不会影响周围元素的布局。

relative 的定位还有另外两点值得一提：相对定位元素的 left/top/right/bottom 的百分比值是相对于包含块计算的，而不是自身。注意，虽然定位位移是相对自身，但是百分比值的计算值不是。

top 和 bottom 这两个垂直方向的百分比值计算跟 height 的百分比值是一样的，都是相对高度计算的。同时，如果包含块的高度是 auto，那么计算值是 0，偏移无效，也就是说，如果父元素没有设定高度或者不是“格式化高度”，那么 relative 类似`top: 20%`的代码等同于`top: 0`。

当 top/bottom 和 left/right 同时使用的时候，绝对定位是尺寸拉伸，保持流体特性，但是相对定位却是根据文档流的顺序来表现，只有一个方向的定位属性会起作用。

“relative 的最小化影响原则”是总结的一套更好地布局实践的原则，主要分为以下两部分：尽量不使用 relative，如果想定位某些元素，看看能否使用“无依赖的绝对定位”；如果场景受限，一定要使用 relative，则该 relative 务必最小化。

因为一个普通元素变成相对定位元素，实际上元素的层叠顺序提高了，甚至在 IE6 和 IE7 浏览器下无须设置 z-index 就直接创建了新的层叠上下文，会导致一些绝对定位浮层无论怎么设置 z-index 都会被其他元素覆盖。“relative 的最小化影响原则”规避了复杂场景可能出现样式问题的隐患，从日后的维护角度讲也更方便。

## 6.10 强悍的 position:fixed 固定定位

`position: fixed`固定定位元素的“包含块”是根元素，我们可以将其近似看成`<html>`元素。

和“无依赖的绝对定位”类似，就是“无依赖的固定定位”，利用 absolute/fixed 元素没有设置 left/top/right/bottom 的相对定位特性，可以将目标元素定位到我们想要的位置。

```
<div class="father">
  <div class="right">
    &nbsp;<div class="son"></div>
  </div>
</div>

.father {
  width: 300px; height: 200px;
  position: relative;
}
  .right {
  height: 0;
  text-align: right;
  overflow: hidden;
}
.son {
  display: inline;
  width: 40px; height: 40px;
  position: fixed;
  margin-left: -40px;
}
```

有时候我们希望元素既有不跟随滚动的固定定位效果，又能被定位元素限制和精准定位。我们可以使用`position: absolute`进行模拟，原理其实很简单：页面的滚动使用普通元素替代，此时滚动元素之外的其他元素自然就有了“固定定位”的效果了。这个其它元素虽然是绝对定位，但是并不在滚动元素内部，自然滚动时不会跟随，如同固定定位效果，同时本身绝对定位。因此，可以使用 relative 进行限制或者 overflow 进行裁剪等。

蒙层弹窗是网页中常见的交互，其中黑色半透明全屏覆盖的蒙层基本上都是使用`position: fixed`定位实现的。但是，如果细致一点儿就会发现蒙层无法覆盖浏览器右侧的滚动栏，并且鼠标滚动的时候后面的背景内容依然可以被滚动，并没有被锁定，体验略打折扣。

如果是移动端项目，阻止 touchmove 事件的默认行为可以防止滚动；如果是桌面端项目，可以让根元素直接`overflow: hidden`。但是，Windows 操作系统下的浏览器的滚动条都是占据一定宽度的，滚动条的消失必然会导致页面的可用宽度变化，页面会产生体验更糟糕的晃动问题，那怎么办呢？很简单，我们只需要找个东西填补消失的滚动条就好了。那该找什么东西充呢？这时候就轮到功勋卓越的 border 属性出马了——消失的滚动条使用同等宽度的透明边框填充！

# 第 7 章 CSS 世界的层叠规则

所谓“层叠规则”，指的是当网页中的元素发生层叠时的表现规则。默认情况下，网页内容是没有偏移角的垂直视觉呈现，当内容发生层叠的时候，一定会有一个前后的层叠顺序产生，有点儿类似于真实世界中“论资排辈”的感觉。

## 7.1 z-index 只是 CSS 层叠规则中的一叶小舟

在 CSS 世界中，z-index 属性只有和定位元素（position 不为 static 的元素）在一起的时候才有作用，可以是正数也可以是负数。理论上说，数值越大层级越高，但实际上其规则要复杂很多。但随着 CSS3 新世界的到来，z-index 已经并非只对定位元素有效，flex 盒子的子元素也可以设置 z-index 属性。

## 7.2 理解 CSS 世界的层叠上下文和层叠水平

层叠上下文，英文称作 stacking context，是 HTML 中的一个三维的概念。如果一个元素含有层叠上下文，我们可以理解为这个元素在 z 轴上就“高人一等”。我们可以把层叠上下文理解为一种“层叠结界”，自成一个小世界。这个小世界中可能有其他的“层叠结界”，而自身也可能处于其他“层叠结界”中。

层叠水平，英文称作 stacking level，决定了同一个层叠上下文中元素在 z 轴上的显示顺序。显而易见，所有的元素都有层叠水平，包括层叠上下文元素，也包括普通元素。然而，对普通元素的层叠水平探讨只局限在当前层叠上下文元素中。

某些情况下 z-index 确实可以影响层叠水平，但是只限于定位元素以及 flex 盒子的孩子元素；而层叠水平所有的元素都存在。

## 7.3 理解元素的层叠顺序

层叠顺序，英文称作 stacking order，表示元素发生层叠时有着特定的垂直显示顺序。

在 CSS 2.1 的年代，在 CSS3 新世界还没有到来的时候（注意这里的前提），层叠顺序规则是。

> 层叠上下文（background/bordr），负 z-index，block 块状水平盒子，float 浮动盒子，inline/inline-block 水平盒子，z-index:auto 或看成 z-index:0，正 z-index
>
> - 位于最下面的 background/border 特指层叠上下文元素的边框和背景色。每一个层叠顺序规则仅适用于当前层叠上下文元素的小世界。
> - inline 水平盒子指的是包括 inline/inline-block/inline-table 元素的“层叠顺序”，它们都是同等级别的。
> - 单纯从层叠水平上看，实际上 z-index:0 和 z-index:auto 是可以看成是一样的。注意这里的措辞—“单纯从层叠水平上看”，实际上，两者在层叠上下文领域有着根本性的差异。

background/border 为装饰属性，浮动和块状元素一般用作布局，而内联元素都是内容。内容的层叠顺序相当高，这样当发生层叠时，重要的文字、图片内容才可以优先显示在屏幕上。

## 7.4 务必牢记的层叠准则

下面这两条是层叠领域的黄金准则。当元素发生层叠的时候，其覆盖关系遵循下面两条准则：

- 谁大谁上： 当具有明显的层叠水平标识的时候，如生效的 z-index 属性值，在同一个层叠上下文领域，层叠水平值大的那一个覆盖小的那一个。
- 后来居上： 当元素的层叠水平一致、层叠顺序相同的时候，在 DOM 流中处于后面的元素会覆盖前面的元素。

在 CSS 和 HTML 领域，只要元素发生了重叠，都离不开上面这两条黄金准则。

## 7.5 深入了解层叠上下文

层叠上下文元素有如下特性。

- 层叠上下文的层叠水平要比普通元素高。
- 层叠上下文可以阻断元素的混合模式。
- 层叠上下文可以嵌套，内部层叠上下文及其所有子元素均受制于外部的“层叠上下文”。
- 每个层叠上下文和兄弟元素独立，也就是说，当进行层叠变化或渲染的时候，只需要考虑后代元素。
- 每个层叠上下文是自成体系的，当元素发生层叠的时候，整个元素被认为是在父层叠上下文的层叠顺序中。

和块状格式化上下文一样，层叠上下文也基本上是由一些特定的 CSS 属性创建的。将其总结为 3 个流派。

- 天生派：页面根元素天生具有层叠上下文，称为根层叠上下文。
- 正统派： z-index 值为数值的定位元素的传统“层叠上下文”。
- 扩招派：其他 CSS3 属性。

根层叠上下文指的是页面根元素，可以看成是`<html>`元素。因此，页面中所有的元素一定处于至少一个“层叠结界”中。

对于 position 值为 relative/absolute 以及 Firefox/IE 浏览器（不包括 Chrome 浏览器）下含有`position: fixed`声明的定位元素，当其 z-index 值不是 auto 的时候，会创建层叠上下文。`z-index: auto`所在的元素是一个普通定位元素，而 z-index 一旦变成数值，哪怕是 0，就会创建一个层叠上下文。此时，层叠规则就可能发生了变化。层叠上下文的特性里面最后一条是自成体系。有时候，我们在网页重构的时候会发现 z-index 嵌套错乱，这时要看看是不是受父级的层叠上下文元素干扰了，可能就豁然开朗了。

CSS3 新世界的出现除了带来了新属性，还对过去的很多规则发出了挑战，其中对层叠上下文规则的影响显得特别突出。

- 元素为 flex 布局元素（父元素 display:flex|inline-flex），同时 z-index 值不是 auto。
- 元素的 opacity 值不是 1。
- 元素的 transform 值不是 none。
- 元素 mix-blend-mode 值不是 normal。
- 元素的 filter 值不是 none。
- 元素的 isolation 值是 isolate。
- 元素的 will-change 属性值为上面 2 ～ 6 的任意一个（如 will-change:opacity、 will-chang:transform 等）。
- 元素的-webkit-overflow-scrolling 设为 touch。

定位元素会层叠在普通元素的上面，其根本原因就是：元素一旦成为定位元素，其 z-index 就会自动生效，此时其 z-index 就是默认的 auto，也就是 0 级别，根据上面的层叠顺序表，就会覆盖 inline 或 block 或 float 元素。而不支持 z-index 的层叠上下文元素天然是`z-index: auto`级别，也就意味着，层叠上下文元素和定位元素是一个层叠顺序的，于是当它们发生层叠的时候，遵循的是“后来居上”准则。

## 7.6 z-index 负值深入理解

z-index 负值的最终表现并不是单一的，而是与“层叠上下文”和“层叠顺序”密切相关。z-index 负值元素的层级是在层叠上下文元素上面、 block 元素的下面，也就是 z-index 虽然名为负数层级，但依然无法突破当前层叠上下文所包裹的小世界。可以这么说， z-index 负值渲染的过程就是一个寻找第一个层叠上下文元素的过程，然后层叠顺序止步于这个层叠上下文元素。

- 可访问性隐藏。z-index 负值可以隐藏元素，只需要层叠上下文内的某一个父元素加个背景色就可以。它与 clip 隐藏相比的一个优势是，元素无须绝对定位。
- IE8 下的多背景模拟。
- 定位在元素的后面。

## 7.7 z-index“不犯二”准则

定位元素一旦设置了 z-index 值，就从普通定位元素变成了层叠上下文元素，相互间的层叠顺序就发生了根本的变化，很容易出现设置了巨大的 z-index 值也无法覆盖其他元素的问题。

避免 z-index“一山比一山高”的样式混乱问题。

页面上主体元素遵循 z-index “不犯二”准则，浮层元素使用 z-index “层级计数器” 。

# 第 8 章 强大的文本处理能力

## 8.1 line-height 的另外一个朋友 font-size

line-height 的部分类别属性值是相对于 font-size 计算的， vertical-align 百分比值属性值又是相对于 line-height 计算的，于是 font-size 和 vertical-align 也有着关系。

通过`vertical-align: 25%`声明让图片的下边缘和中文汉字的中心线对齐。其居中原理本质上和绝对定位元素 50%定位加偏移自身 1/2 尺寸实现居中是一样的，只不过这里的偏移使用的是 vertical-align 百分比值。将前面例子中的`vertical-align: 25%`改成 `vertical-align: .6ex`，效果基本上就是一样的，并且还多了一个优点，就是使用`vertical-align: .6ex`实现的垂直居中效果不会受 line-height 变化影响。

ex 是字符 x 高度，显然和 font-size 关系密切， font-size 值越大，自然 ex 对应的大小也就大。

em 在传统排版中指一个字模的高度，注意是字模的高度，不是字符的高度。其一般由'M'的宽度决定（因为宽高相同），所以叫 em 。在 CSS 中， 1em 的计算值等同于当前元素所在的 font-size 计算值，可以将其想象成当前元素中（如果有）汉字的高度。

rem，即 root em，就是根元素 em 大小。 em 相对于当前元素，rem 相对于根元素，本质差别在于当前元素是多变的，根元素是固定的。如果使用 rem，我们的计算值不会受当前元素 font-size 大小的影响。因此，要想实现带有缩放性质的弹性布局，使用 rem 是最佳策略，但 rem 是 CSS3 单位，IE9 以上浏览器才支持。

em 实际上更适用于图文内容展示的场景，对此进行弹性布局。例如，`<h1>`～`<h6>`以及`<p>`等与文本内容展示的元素的 margin 都是用 em 作为单位，这样，当用户把浏览器默认字号从“中”设置成“大”或改成“小”的时候，上下间距也能根据字号大小自动调整，使阅读更舒服。

font-size 的关键字属性值分以下两类。

相对尺寸关键字。指相对于当前元素 font-size 计算，包括：

- larger：大一点，是`<big>`元素的默认 font-size 属性值。
- smaller：小一点，是`<small>`元素的默认 font-size 属性值。

绝对尺寸关键字。与当前元素 font-size 无关，仅受浏览器设置的字号影响。注意这里的措辞，是“浏览器设置”，而非“根元素”，两者是有区别的。

- xx-large：好大好大，和<h1>元素计算值一样。
- x-large：好大，和<h2>元素计算值一样。
- large：大，和<h3>元素计算值近似（“近似”指计算值偏差在 1 像素以内，下同）。
- medium：不上不下，是 font-size 的初始值。
- small：小，和<h5>元素计算值近似。
- x-small：好小，和<h6>元素计算值近似。
- xx-small：好小好小，无对应的 HTML 元素。

桌面 Chrome 浏览器下有个 12px 的字号限制，就是文字的 font-size 计算值不能小于 12px 。如果`font-size: 0`的字号表现就是 0，那么文字会直接被隐藏掉，并且只能是`font-size: 0`，哪怕设置成`font-size: 0.0000001px`， 都还是会被当作 12px 处理的。

## 8.2 字体属性家族的大家长 font-family

CSS 世界中的有很多属性都是以 font- 开头的，如 font-style、 font-weight 和这里要介绍的 font-family，把所有这些以 font- 开头的 CSS 属性统称为“字体属性家族”。顾名思义， font-family 就是“字体家族”的意思。font-family 默认值由操作系统和浏览器共同决定。

font-family 支持两类属性值，一类是“字体名”，一类是“字体族”。

> 字体名”就是使用的对应字体的名称。 如果字体名包含空格，需要使用引号包起来。 根据实践，可以不用区分大小写。如果有多个字体设定，从左往右依次寻找本地是否有对应的字体即可。
>
> “字体族”分为很多类， MDN 上文档分类如下：
>
> - font-family: serif（衬线字体）
> - font-family: sans-serif（无衬线字体）
> - font-family: monospace（等宽字体）
> - font-family: cursive（手写字体）
> - font-family: fantasy（奇幻字体）
> - font-family: system-ui（系统 UI 字体）

字体分衬线字体和无衬线字体。所谓衬线字体，通俗讲就是笔画开始、结束的地方有额外装饰而且笔画的粗细会有所不同的字体。网页中常用中文衬线字体是“宋体”，常用英文衬线字体有 Times New Roman、 Georgia 等。无衬线字体没有这些额外的装饰，而且笔画的粗细差不多，如中文的“雅黑”字体，英文包括 Arial、 Verdana、 Tahoma、 Helivetica、Calibri 等。

以前人们排正文喜欢使用衬线字体，但是如今，不知是审美疲劳还是人们更加追求简洁干净的缘故，更喜欢使用无衬线字体，如“微软雅黑”或者“苹方”之类的字体。

serif 和 sans-serif 还可以和具体的字体名称写在一起，但是需要注意的是，serif 和 sans-serif 一定要写在最后，因为在大多数浏览器下， 写在 serif 和 sans-serif 后面的所有字体都会被忽略。

所谓等宽字体，一般是针对英文字体而言的。据我所知，东亚字体应该都是等宽的，就是每个字符在同等 font-size 下占据的宽度是一样的。等宽字体利于代码呈现。

ch 和 em、 rem、 ex 一样，是 CSS 中和字符相关的相对单位。和 ch 相关的字符是 0，即阿拉伯数字 0。 1ch 表示一个 0 字符的宽度，所以 6 个 0 所占据的宽度就是 6ch。ch 是个 CSS3 单位，可以通过等宽字体对数字进行一些巧妙设计，例如电话号码的输入，一眼可以看出有没有足够十一位数字。

虽然一些常见中文字体，如宋体、微软雅黑等，直接使用中文名称作为 CSS font-family 的属性值也能生效，但我们一般都不使用中文名称，而是使用英文名称，主要是为了规避乱码的风险。

微软正黑体是一款全面支持 ClearType 技术的 TrueType 无衬线字体，用于繁体中文系统。相对应地，中国大陆地区用的是微软雅黑。我们平常所说的“宋体”，指的都是“中易宋体”，英文名称 SimSun，“黑体”类似的是“中易黑体”。所有英文名称大小写都经过一定的考量，并不是随便设定的，虽然说 CSS font-family 对名称的大小写不怎么敏感，但是根据经验，最好至少首字母要大写，否则在使用 CSS unicode-range 的时候可能会遇到一些麻烦。

## 8.3 字体家族其他成员

font-weight 表示“字重”，通俗点讲，就是表示文字的粗细程度。

> normal 默认值。定义标准的字符。
> bold 定义粗体字符。
> bolder 定义更粗的字符。
> lighter 定义更细的字符。
> 100 ～ 900 的整百数 定义由粗到细的字符。400 等同于 normal，而 700 等同于 bold。
> inherit 规定应该从父元素继承字体的粗细。

font-style 表示文字造型是斜还是正，与 font-weight 相比，其属性值就要少很多。其中， normal 是默认值。浏览器显示一个标准的字体样式。italic 和 oblique 这两个关键字都表示“斜体”的意思。区别在于：italic 是使用当前字体的斜体字体，而 oblique 只是单纯地让文字倾斜。 如果当前字体没有对应的斜体字体，则退而求其次，解析为 oblique，也就是单纯形状倾斜。

font-variant 是一个从 IE6 时代就过来的 CSS 属性，对于我们大中华用户，其支持的属性值和作用让我们这些汉字用户觉得有些头疼，实现小体型大写字母，两个属性值要么 normal， 要么 small-caps，font-variant:small-caps 就是可以让英文字符表现为小体型大写字母。

## 8.4 font 属性

可以缩写在 font 属性中的属性非常多，包括 font-style、 font-variant、 font-weight、 font-size、 line-height、 font-family 等。完整语法为：

> [ [ font-style || font-variant || font-weight ]? font-size [ / line-height ]? font-family ]
>
> ||表示或， ?和正则表达式中的?的含义一致，表示 0 个或 1 个。仔细观察上面的语法，会发现 font-size 和 font-family 后面没有问号，也就是说是必需的，是不可以省略的。这和 background 属性不一样， background 属性虽然也支持缩写，但是并没有需要两个属性值同时存在的限制。
>
> font 缩写必须要带上 font-family，然而， 原本真实继承的 font-family 属性值可能会很长，每次 font 缩写后面都挂一个长长的字体列表。解决方法有两个，随便找一个系统根本不存在的字体名占位，或者利用@font face 规则将我们的字体列表重定义为一个字体，这是兼容性很好、 效益很高的一种解决方法。

font 属性除了缩写用法，还支持关键字属性值，其语法如下。需要注意的是，使用关键字作为属性值的时候必须是独立的，不能添加 font-family 或 者 font-size 之类的，这和 font 属性缩写不是一个路子。如果混用则此时的关键字是作为自定义的字体名称存在的，而不是表示系统的关键字对应的菜单字体。

> font:caption | icon | menu | message-box | small-caption | status-bar
>
> 如果将 font 属性设置为上面的一个值，就等同于设置 font 为操作系统该部件对应的 font，也就是说直接使用系统字体。
>
> - caption：活动窗口标题栏使用的字体。
> - icon：包含图标内容所使用的字体，如所有文件夹名称、文件名称、磁盘名称，甚至浏览器窗口标题所使用的字体。
> - menu：菜单使用的字体，如文件夹菜单。
> - message-box：消息盒里面使用的字体。
> - small-caption：调色板标题所使用的字体。
> - status-bar：窗体状态栏使用的字体。

## 8.5 真正了解@font face 规则

@font face 本质上就是一个定义字体或字体集的变量，这个变量不仅仅是简单地自定义字体，还包括字体重命名、默认字体样式设置等。@font face 规则支持的 CSS 属性有 font-family、 src、 font-style、 font-weigh、 unicode-range、 font-variant、 font-stretch 和 font-feature-settings。

这里的 font-family 可以看成是一个字体变量，名称可以非常随意，如直接用一个美元符号'\$'。非 IE 浏览器下甚至可以直接使用纯空格' '。不过有一点需要注意，就是使用这些稀奇古怪的字符或者空格的时候，一定要加引号。

src 表示引入的字体资源可以是系统字体，也可以是外链字体。如果是使用系统安装字体， 则使用 local()功能符；如果是使用外链字体，则使用 url() 功能符。而 local() 功能符 IE9 及其以上版本浏览器才支持。

在 Chrome 浏览器下， @font face 规则设置`font-style: italic`可以让文字倾斜。因为有些字体可能会有专门的斜体字体，注意这个斜体字体并不 是让文字的形状倾斜，而是专门设计的倾斜的字体，所以很多细节会跟物理上的请求不一样。 于是，可以在 CSS 代码中使用`font-style: italic`的时候，通过方法会调用这个对应字体。

font-weight 和 font-style 类似，只不过它定义了不同字重、使用不同字体。对中文而言，这个要比 font-style 适用性强很多。

unicode-range 的作用是可以让特定的字符或者特定范围的字符使用指定的字体。例如， “微软雅黑”字体的引号左右间隙不均，方向不明，实在是看着不舒服，此时我们就专门指定这两个引号使用其他字体。

从面向未来的角度讲，字体图标技术的使用会越来越边缘化，因为和 SVG 图标技术相比，其唯一的优势就是兼容一些老的 IE 浏览器。SVG 图标同样是矢量的，同样颜色可控，但资源占用更少，加载体验更好，呈现效果更佳，更加符合语义。

## 8.6 文本的控制

CSS 有很多属性专门用来对文本进行控制，由于这些属性的作用机制往往是基于内联盒模型的，因此对于内联块状元素同样也是有效果的，这就使得这些 CSS 属性作用范围更广了，甚至可以影响布局。

text-indent 就是对文本进行缩进控制，用得比较多的是 text-indent 负值隐藏文本内容。另外， text-indent 负值缩进在部分浏览器下会影响元素的 outline 区域，通常需要再设置 `overflow: hidden`。 与文本控制相关的 CSS 属性支持百分比值的并不多，text-indent 支持百分比值其实算是比较“有个性的”，但设置百分比值会有隐患。从理论上讲，我们可以使用 text-indent 与百分值实现宽度已知内联元素的居中效果。

- text-indent 仅对第一行内联盒子内容有效。
- 非替换元素以外的 display 计算值为 inline 的内联元素设置 text-indent 值无效，如果计算值是 inline-block/inline-table 则会生效。因此，如果父级块状元素设置 了 text-indent 属性值，子 inline-block/inline-table 需要设置 text-indent:0 重置。
- `<input>`标签按钮 text-indent 值无效。
- `<button>`标签按钮 text-indent 值有效，但是存在兼容性差异， IE 浏览器理解为单标签，百分比值按照容器计算，而 Chrome 和 Firefox 浏览器标签内还有其他 Shadow DOM 元 素，因此百分比值是按照自身的尺寸计算的。
- `<input>`和`<textarea>`输入框的 text-indent 在低版本 IE 浏览器下有兼容问题。

letter-spacing 可以用来控制字符之间的间距，这里说的“字符”包括英文字母、汉字以及空格等，letter-spocing 具有以下一些特性。

- 继承性。
- 默认值是 normal 而不是 0。虽然说正常情况下， normal 的计算值就是 0 。
- 支持负值，且值足够大的时候，会让字符形成重叠，甚至反向排列（非 IE 浏览器）。
- 和 text-indent 属性一样，无论值多大或多小，第一行一定会保留至少一个字符。 letter-spacing 还有一个非常有意思的特性就是，在默认的左对齐情况下，无论值如何设 置，第一个字符的位置一定是纹丝不动的。
- 支持小数值，即使 0.1px 也是支持的，但并不总能看到效果，这与屏幕的密度有关。
- 暂不支持百分比值。

word-spacing 和 letter-spacing 名称类似，其特性也有很多共通之处：都具有继承性；默认值都是 normal 而不是 0。通常情况下，两者表现并无差异；都支持负值，都可以让字符重叠；都支持小数值，如 `word-spacing: 0.5px`；在目前的 CSS2.1 规范中，并不支持百分比值，但新的草案中新增了对百分值的支持，这是是根据相对于字符的“步进宽度”（ advance width）计算的；间隔算法都会受到 `text-align: justify` 两端对齐的影响。

当然也有差异。letter-spacing 作用于所有字符，但 word-spacing 仅作用于空格字符。注意，是作用在“空格” 上，而不是字面意义上的“单词”。换句话说，word-spacing 的作用就是增加空格的间隙宽度。有空格就有效。在命名上，word-spacing 之所以称为 word-spacing 而不是 blank-spacing 之类的，主要原因是此属性当初主要为英文类排版设计， 而英文单词和单词之间是以空格分隔的，要想控制单词之间的间距，自然就向“空格”开刀了。

word-break 属性规定自动换行的处理方法。语法如下：

- word-break: normal 使用默认的换行规则。
- word-break: break-all 允许任意非 CJK（ Chinese/Japanese/Korean）文本间的单词断行，这个值所有浏览器都支持。
- word-break: keep-all 不允许 CJK 文本中的单词换行，只能在半角空格或连字符处换行。非 CJK 文本的行为实际上和 normal 一致。目前移动端还不适合使用 word-break:keep-all。

word-wrap 属性允许长单词或 URL 地址换行到下一行。在 CSS3 规范里，这个属性的名称被修改了，叫作 overflow-wrap。

- word-wrap: normal 就是大家平常见得最多的正常的换行规则。
- word-wrap: break-word 一行单词中实在没有其他靠谱的换行点的时候换行。

顾名思义，`word-break: break-all` 的作用是所有的都换行，毫不留情，一点儿空隙都不放过，而 `word-wrap: break-word` 则带有怜悯之心，如果这一行文字有可以换行的点，如空格或 CJK（中文/日文/韩文）之类的，就不打英文单词或字符的主意了，在这些换行点换行，至于对不对齐、好不好看则不关心，因此，很容易出现一片一片空白区域的情况。

white-space 属性声明了如何处理元素内的空白字符，这类空白字符包括 Space（空格） 键、 Enter（回车）键、 Tab（制表符）键产生的空白。因此， white-space 可以决定图文内容是否在一行显示（回车空格是否生效），是否显示大段连续空白（空格是否生效）等。 其属性值包括下面这些。

- normal：合并空白字符和换行符。
- pre：空白字符不合并，并且内容只在有换行符的地方换行。
- nowrap：该值和 normal 一样会合并空白字符，但不允许文本环绕。
- pre-wrap：空白字符不合并，并且内容只在有换行符的地方换行，同时允许文本环绕。
- pre-line：合并空白字符，但只在有换行符的地方换行，允许文本环绕。

当 white-space 设置为 nowrap 的时候，元素的宽度此时表现为“最大可用宽度”，换行符和一些空格全部合并，文本一行显示。

- “包含块”尺寸过小处理。绝对定位以及 inline-block 元素都具有包裹性，当文本内容宽度超过包含块宽度的时候，就会发生文本环绕现象。可以对其使用`white-space: nowrap`声明让其如预期的那样一行显示。
- 单行文字溢出点点点效果。`text-overflow: ellipsis`文字内容超出打点效果离不开`white-space: nowrap`声明。
- 水平列表切换效果。 水平列表切换是网页中常见的交互效果，如果列表的数目是不固定的，使用`white-space: nowrap`使列表一行显示会是个非常不错的处理。

IE 浏览器（至少 到 IE11）到目前为止使用`text-align: justify`都无法让中文两端对齐，而 Chrome、 Firefox 和 Safari 等浏览器都是可以的。不过，好在 IE 有一个私有的 CSS 属性 text-justify（目前也写入规范草案了）可以实 现中文两端对齐的。`text-align: justify`除了实现文本的两端对齐，还可以实现容错性更强的两端对齐布局效果。 在默认设置下，`text-align:justify`要想有两端对齐的效果，需要满足两点：一是有分隔点，如空格；二是要超过一行，此时非最后一行内容会两端对齐。

CSS 的 `text-decoration: underline` 可以给内联文本增加下划线，但是，如果对细节要求较高，就会发现，下划线经常会和中文文字的下边缘粘连在一起，英 文的话甚至直接穿过。最好的处理方法就是使用看似普通却功勋卓越的 border 属性。对于纯内联元素，垂直方向的 padding 属性和 border 属性对原来的布局定位等没有任何影响。 也就是说， 就算 border-bottom 宽度设为 100px，上下行文字的垂直位置依旧纹丝不动。 再加上 border 兼容性很好，天然使用 color 颜色作为边框色，可谓下划线重叠问题解决办法 的不二之选。另外，配合 padding，我们就可以很有效地调节下边框和文字下边缘的距离，实现我们最想要的效果。

text-transform 也是为英文字符设计的，要么全大写`text-transform: uppercase`，要么全小写`text-transform: lowercase`。

## 8.7 了解:first-letter/:first-line 伪元素

很多年前，Chrome 浏览器和 IE9 浏览器还未出现， 那时候 first-letter 叫伪类选择器， 写法是前面加一个冒号，如`:first-letter`。那时候的语义要更直白一些，选择第一个字符， 然后设置一些样式。后来，伪类和伪元素被划分得更加明确和规范了，`::after`、`::before`、`::backdrop`、`::first-letter`、`::first-line`、`::selection`等是伪元素，`:active`、`:focus`、`:checked`等被称为伪类，这就导致`::first-letter`的语义发生了一些变化——首字符作为元素的假想子元素。

要想让::first-letter(:first-letter)伪元素生效，是需要满足一定条件的。

- 元素的 display 计算值必须是 block、 inline-block、 list-item、 table-cell 或者 table-caption，其他所有 display 计算值都没有用，包括 display:table 和 display:flex 等。
- 此外，不是所有的字符都能单独作为::first-letter 伪元素存在的。常见的标点符号、各类括号和引号 在::first-letter 伪元素眼中全部都是“辅助类”字符。正常情况下可以直接作为伪元素的字符就是数字、英文字母、中文、 \$、一些运算符，以 及非常容易被忽视的空格等。
- 字符前面不能有图片或者 inline-block/inline-table 之类的元素存在。
- 一般来讲， ::before 伪元素和普通元素之间没有多少瓜葛，例如:first-child 和:empty 之类的选择器都不受影响。但是::before 伪元素也参 与::first-letter 伪元素
- 如果字符被选作了::first-letter 伪元素，并不是像::before 伪元素那样，几乎所 有 CSS 都有效，只是一部分有效。

支持部分 display 属性值标签嵌套。 ::first-letter 伪元素获取可以跨标签，也 就是不仅能选择匿名内联盒子，还能透过层层标签进行选择，但是也有一些限制，并不是所有标签嵌套都是有用的。 ::first-letter 伪元素的另外一个重要特性—颜色等权重总是多了一层。

:first-line 选择器用于选取指定选择器的首行。利用了::first-line 伪元素，于是标签上的颜色实际上是设置给 background-color 的，而按钮真正呈现的颜色已经被::first-line 伪元素牢牢设置好了， 就完全不用担心文字颜色和背景色混在一起了。

- :first-line 和:first-letter 伪元素一样， IE9 及以上版本浏览器支持双冒号::first-line{}写法， IE8 浏览器只认识单冒号写法。

- :first-line 和:first-letter 伪元素一样，只能作用在块级元素上，也就是 display 为 block、 inline-block、 list-item、 table-cell 或者 tablecaption 的元素设置:first-line 才有效， table、 flex 之类都是无效的。

- :first-line 和:first-letter 伪元素一样，仅支持部分 CSS 属性，例如： • 所有字体相关属性； • color 属性； • 所有背景相关属性； • text-decoration、 text-transfor、 letter-spacing、 word-spacing、 line-height 和 vertical-align 等属性。

- :first-line 和:first-letter 伪元素一样， color 等继承属性的权重总是多了 一层，毕竟称为“伪元素”，就好像里面还有个子元素。如果:first-line 和:first-letter 同时设置颜色， :first-letter 级别比:first-line 高，即使:first-line 写在后面，甚至加!important（如果浏览器支持）也是如此。

- :first-line 和:first-letter 伪元素一样，也支持标签嵌套，但是具体细则 和:first-letter 出入较大，例如，它不支持 table 相关属性等。

# 第 9 章 元素的装饰与美化

## 9.1 CSS 世界的 color 很单调

CSS1 的时候只支持 16 个基本颜色关键字，如 black、 white。 CSS2 只加入了一个颜色—橙色 orange。CSS3 一下子增加了 100 多个颜色关键字，甚至连 mediumturquoise 这样的复杂得看不懂也记不住的关 键字都出现了。这些扩展的 CSS 颜色关键字是有专门的名称的，称为“X11 颜色名”，这里 的“X11”不是 11 区的意思，而是指用来显示位图的 X Window System，常见于类 UNIX 计算机系统上。CSS4 仅增加了一个颜色关键字— rebeccapurple。

传统 HTML 的部分属性可以直接支持 color 属性，同时，我们也可以通过 style 属性书写 color 声明。如果浏览器认识这些颜色关键字，则该什么颜色就显示什么颜色；但是，如果浏览器无法 识别这些颜色关键字，则两种书写的最终表现会有差异。在 HTML 中，会使用其他算法将非识别颜色关键字转换成另外一个完全不同的颜色值；而 在 CSS 中则是直接使用默认颜色值。

transparent 关键字是一个很有意思的关键字，让相应属性值作为透明出现， background-color:transparent 包括 IE6 浏览器都支持， border-color:transparent 从 IE7 浏览器开始支持， 但是 color: transparent 却从 IE9 浏览器才开始支持。

currentColor 可以使用当前 color 计算值，即所谓颜色值。但是同样地， IE9+浏览器才支持它。实际上， CSS 中很多属性值默认就是 currentColor 的表现，我们一般（除了部分浏览器 animation 需要）无须画蛇添足地再声明这个关键字。如 border、 text-shadow、 box-shadow 等，尤其 border，包括 IE7 在内的浏览器都是如此特性。

CSS 世界的 color 属性支持十六进制颜色、 rgb 颜色。十六进制颜色指的是长得像 #000000 或#000 这样的颜色，我们在 CSS 中用得最频繁的就是这种格式的颜色。为什么呢？ 因为字符数目最少，书写更快，渲染性能更高。 rgb 颜色实际上和十六进制颜色是近亲，都归属于 rgb 颜色，只是进制有差异。 除了支持数值颜色，如 rgb(255, 0, 51)，还支持百分比 rgb 颜色，如 rgb(100%, 0%, 20%) 。rgb 数值格式只能是整数，不能是小数，否则，包括各 IE 以及 Chrome 在内的浏览器都会 无视它。 但 color 属性并不支持 hsl 颜色、 rgba 颜色和 hsla 颜色。

hsl 颜色是 CSS3 才出现的颜色表现格式， IE9+浏览器才支持。和 rgb 分别表示 red、 green、 blue 一样， hsl 颜色的 3 个字母也有自己的含义。其中， h 表示 hue，是色调的意思，取值 0 ～ 360，大致按照数值红、橙、黄、绿、青、蓝、紫变化节奏； s 表示 saturation（饱和度），用 0 ～ 100%表示，值越大饱和度越高，颜色越亮，通常我们评价某设计“亮瞎我们的眼”，就是“这 个设计颜色饱和度太高”的另一种说法； l 表示 lightness（亮度），也用 0 ～ 100%表示，值越高 颜色越亮， 100%就是白色， 50%则是正常亮度， 0%就是黑色。

最后，CSS3 中的颜色支持 Alpha 透明通道，于是就有了 rgba 颜色和 hsla 颜色， a 表示 透明度，取值在 0 ～ 1， 0 表示完全透明， 1 表示实色无透明。如果使用小数，前面的 0 可以省 略，能节约一个字符大小。

## 9.2 CSS 世界的 background 很单调

CSS 世界中的 background 大部分有意思的内容都是在 CSS3 新世界中才出现的，如 Multiple backgrounds（多背景）、 background-size（背景尺寸）、 background-origin （背景初始定位盒子）、 background-clip（背景剪切盒子）等。

当我们使用 background 属性的时候，实际上使用的是一系列 background 相关属性的集合，包括：

- `background-image: none`
  规定要使用的背景图像。一个元素如果 display 计算值为 none，在 IE 浏览器下（ IE8 ～ IE11，更 高版本不确定）依然会发送图片请求， Firefox 浏览器不会，至于 Chrome 和 Safari 浏览器如果隐藏元素同时又设置了 background-image，则图片依然会去加载； 如果是父元素的 display 计算值为 none，则背景图不会请求，此时浏览器或许放心地认为这个背景图暂时是不会使用的。
- `background-position: 0% 0%`
  规定背景图像的位置。CSS 中有一类属性值被称作`<position>`值，表示一种 CSS 数据类型、二维坐标空间，用于设置相对盒子的坐标。`<position>`值支持 1 ～ 4 个值，可以是具体数值，也可以是百分比值，还可以是 left、top、right、center 和 bottom 等关键字。 如果缺省偏移关键字，则会认为是 center，因此 background-position:top center 可以直接写成 background-position:top。`<position>`值也支持百分比值，不过其表现与 CSS 中其他的百分比单位表现都不一样。 第一个值是水平位置，第二个值是垂直位置。左上角是 0% 0%。右下角是 100% 100%。如果您仅规定了一个值，另一个值将是 50%。
- `background-repeat: repeat`
  规定如何重复背景图像。background-repeat 支持 repeat、 repeat-x、 repeat-y 这几个值，语义清晰，兼容性好。
- `background-attachment: scroll`
  CSS 世界中， background-attachment 支持 scroll 和 fixed 两个属性值，其中 scroll 是默认值，就是平常使用背景图的效果表现； fixed 表示背景相对于 当前文档视区定位，也就是页面再怎么滚动背景图片位置依旧纹丝 不动，稳若泰山。
- `background-color: transparent`
  规定要使用的背景颜色。background 无论是单背景图还是多背景图，背景色一定是在最底下的位置。

如果是 IE9+浏览器，则还包括：

- `background-size: auto auto`

- `background-origin: padding-box`

- `background-clip: border-box`

# 第 10 章 元素的显示与隐藏

如果希望元素不可见，同时不占据空间，辅助设备无法访问，同时不渲染，可以使用`<script>`标签隐藏。`<script>`标签是不支持嵌套的，因此，如果希望在`<script>`标签中再放置其他不渲染的模板内容，可以试试使用`<textarea>`元素。另外，`<script>`标签隐藏内容获取使用 script.innerHTML，`<textarea>`使用 textarea.value。

如果希望元素不可见，同时不占据空间，辅助设备无法访问，但资源有加载，DOM 可访问，则可以直接使用`display: none`隐藏。

如果希望元素不可见，同时不占据空间，辅助设备无法访问，但显隐的时候可以有 transition 淡入淡出效果，则可以使用：`.hidden { position: absolute; visibility: hidden; }`

如果希望元素不可见，不能点击，辅助设备无法访问，但占据空间保留，则可以使用`visibility: hidden`隐藏。

如果希望元素不可见，不能点击，不占据空间，但键盘可访问，则可以使用 clip 剪裁隐藏。

如果希望元素不可见，不能点击，但占据空间，且键盘可访问，则可以试试 relative 隐藏。例如，如果条件允许，也就是和层叠上下文之间存在设置了背景色的父元素， 则也可以使用更友好的 z-index 负值隐藏。

如果希望元素不可见，但可以点击，而且不占据空间，则可以使用透明度。

如果单纯希望元素看不见，但位置保留，依然可以点可以选，则直接让透明度为 0。

## 10.1 display 与元素的显隐

对一个元素而言，如果 display 计算值是 none 则该元素以及所有后代元素都隐藏，如果是其他 display 计算值则显示。

在 Firefox 浏览器下， display:none 的元素的 background-image 图片是不加载的， 包括父元素 display:none 也是如此；如果是 Chrome 和 Safari 浏览器，则要分情况，若父元 素 display:none，图片不加载，若本身背景图所在元素隐藏，则图片依旧会去加载；对 IE 浏览器而言，无论怎样都会请求图片资源。

## 10.2 visibility 与元素的显隐

父元素设置 visibility:hidden，子元素也会看不见，究其原因是继承性，子元素继承了 visibility:hidden，但是，如果子元素设置了 visibility:visible，则子元素又会显示出来。这个和 display 隐藏有着质的区别。

visibility:hidden 不会影响计数器的计数，这和 display:none 完全不一样。

因为 CSS3 transition 支持的 CSS 属性中有 visibility，transition 可以延时执行，因此，和 visibility 配合可以使用纯 CSS 实现 hover 延时显示效果，由此提升我们的交互体验。

# 第 11 章 用户界面样式

用户界面样式指的是 CSS 世界中用来帮助用户进行界面交互的一些 CSS 样式，主要有 outline 和 cursor 等属性。

## 11.1 和 border 形似的 outline 属性

outline 表示元素的轮廓，语法和 border 属性非常类似，分宽度、类型和颜色，支持 的关键字和属性值与 border 属性一模一样。

不可在全局设置 `outline:0 none` 这样的错误会造成部分场景下的部分用户产生使用障碍！

outline 是本书介绍到现在出现的第一个真正意义上的不占据任何空间的属性。例如，内联元素的上下 padding 值似乎不占据任何空间，但是一旦祖先元素 overflow 计算值不是 visible， 同时 padding 值足够大，滚动条就会出现，暴露出“不占据空间”其实是一个假象。但是 outline 属性确实不占据任何空间，轮廓宽度设置得再宽广，也不会影响任何元素的任何布局，并且 outline 轮廓是可穿透的。

## 11.2 光标属性 cursor

cursor 属性值几乎可以认为是当下支持的关键字属性值最多的 CSS 属性，没有之一。下面就是按照功能特性对其进行的分类以及具体解释描述。

常规

- cursor:auto： cursor 默认值。 auto 表示光标形状根据内容类别浏览器自动进行处理。
- cursor:default：系统默认光标形状。虽然有“默认”之意，但却不是 cursor 属 性的默认值。
- cursor:none：这个声明非常有意思，可以让光标隐藏不见。

链接和状态

- cursor:pointer：光标表现为一只伸出食指的手。
- cursor:help：帮助，通常是光标头上带了个问号。
- cursor:progress：表示进行中的意思。
- cursor:wait：我们先看看光标形状，可能是转圈圈，或者是沙漏或者是表， 总之和电脑死机时候的光标是一样的。
- cursor:context-menu：context-menu 的字面意思是“上下文菜单”，就 是右键点击我们的桌面或者网页显示的那个菜单列表。

选择

- cursor:text：潜台词是文字可被选中 。默认文本字符或者可输入的单复选框的光标就表现成这样，因为文字可以被选中；反过来，如果文字是不能被选中的，光标就不应该是 cursor:text。
- cursor:vertical-text：潜台词是文字可以垂直选中 。当我们使用 writing-mode 把文字排版从水平改为垂直的时候，文字的光标就自动表现为 cursor:vertical-text。
- cursor:crosshair：十字光标 。它通常用在像素级的框选或点选场合， 比方说自定义的取色工具。
- cursor:cell： cursor:cell 中的 cell 和 display:table-cell 中的 cell 其 实可以看成是同一个东西，也就是单元格。换句话说， cursor:cell 用来表示单元 格是可以框选的。

拖曳

- cursor:move：光标变成 cursor:move，往往就意味着当前元素是可以移动的。
- cursor:copy：光标变成 cursor:copy，往往就意味着当前元素是可以被复制的。
- cursor:alias：光标变成 cursor:alias，往往就意味着当前元素是可以创建别名或 者快捷方式的。
- cursor:no-drop：光标变成 cursor: no-drop，往往就意味着当前元素放开到当 前位置是不允许的。
- cursor:not-allowed：光标变成 cursor:not-allowed，往往就意味着当前行 为是禁止的。

滚动

- cursor:all-scroll：表示上下左右都可以滚动。

拉伸

- cursor:col-resize：它适用于移动垂直线条，如垂直参考线。
- cursor:row-resize：它适用于移动水平线条，如水平参考线。
- 单向拉伸： 总共 8 个方位 8 个不同的关键字属性值。
- 双向拉伸： 总共 4 个对立方位组合。

缩放

- cursor:zoom-in：光标形似放大镜 。
- cursor:zoom-out：光标形似缩小镜 。

抓取

- cursor:grab：光标是一个五指张开的手。
- cursor:grabbing：光标是一个五指收起的手

从 IE6 开始，我们就可以自定义网页中的光标样式，因此，对于 cursor 属性，兼容性都 不是问题。对于 Chrome 等浏览器，可以直接使用 PNG 图片作为光标，但是 IE 浏览器不行。 IE 仅支 持专门的.cur 格式的光标文件，需要使用工具进行格式转换。

# 第 12 章 流向的改变

## 12.1 改变水平流向的 direction

direction 主要有两个属性。ltr 是初始值，表示 left-to-right，就是从左往右的意思。目前东亚以及欧美文字书写就 是从左往右的； rtl 表示 right-to-left，就是从右往左的意思。阿拉伯语（Arabic）、希伯来语 （Hebrew）等的书写就是从右往左的，也就是说， direction 设计的本意其实是为了兼顾这类语言。

direction 属性似乎只能改变图片或者按钮的呈现顺序，但 对纯字符内容（尤其中文）好像并没有什么效果，但实际上，我们也是可以指定中文每个字符都反向呈现的，方法就是借助 direction 的搭档属性 unicode-bidi。

- normal：正常排列。假设设置了 direction:rtl，则图片、按钮以及问号、加号之类的字符会从右往左显示，但是中文、英文字符还是从左往右显示。
- embed： embed 属性值要想起作用，只能作用在内联元素上。在通常情况下， embed 属性值的表现和 normal 是一样的，导致很多人不明白 embed 到底和 normal 有什么区别。 其实它们的区别很简单， embed 属性值的字符排序是独立内嵌的，不受外部影响。
- bidi-override： 顾名思义， bidi-override 就是“重写双向排序规则”，通常样式表现为所有的字符都按照统一的 direction 顺序排列，例如，若设置 direction:rtl， 则所有字符都会从右往左反向排列，效果强烈。

## 12.2 改变 CSS 世界纵横规则的 writing-mode

和 float 属性有些类似，writing-mode 原本是为控制内联元素的显示而设计的（即所谓的文本布局）。因为在亚洲，尤其像中国这样的东亚国家，存在文字的排版不是水平而是垂直的情况，如中国的古诗文。因此，writing-mode 就是用来实现文字竖向呈现的。

writing-mode 的语法学习要求比其他 CSS 属性要高一些，因为我们需要记住两套不同的语法：一个是 IE 私有属性，一个是 CSS3 规范属性。

- 默认值 horizontal-tb 表 示文本流是水平方向（horizontal）的，元素是从上往下（top-bottom）堆叠的。
- vertical-rl 表示文本是垂直方向（ vertical）展示，然后阅读的顺序是从右往左 （right-left），和我们阅读古诗的顺序一致。
- vertical-lr 表示文本是垂直方向（vertical）展示，然后阅读的顺序还是默认的从左往右（left-right），即仅仅是水平变垂直。
- IE 浏览器下的关键字值多达 11 个。如果项目需要兼容 IE7，则只要关注两个就可以了，即初始值 lr-tb 和 tb-rl，对应于 CSS3 规范中的 horizontal-tb 和 vertical-rl。如果项目只需要兼容 IE8 及以上版本浏览器，恭喜你，你可以和 CSS3 规范属性完全对应上了，而且 IE8 下的 writing-mode 要比 IE7 强大得多。我们需要关注初始值 lr-tb、 tb-rl 和 tb-lr，分别对应于 CSS3 中的 horizontal-tb、 vertical-rl 和 vertical-lr。

相同的 writing-mode 属性值并不会累加。例如，如果父子元素均设置了`writing-mode: tb-rl`，只会渲染一次，子元素并不会两次“旋转”。

在 IE 浏览器下， 如果一个自身具有布局的元素（不是纯文本之类元素）writing-mode 属性值和父元素不同，那么当子元素的布局流变化的时候，其父元素坐标系统的可用空间会被充分利用。

虽然 Chrome 和 Opera 认识 tb-rl 等老的 IE 属性值，但也仅仅是认识而已，并没有任何实际效果！

在 CSS3 中，由于 writing-mode 的存在，对垂直流方向的 margin 值会发生合并。换句话说，如果元素是默认的水平流，则垂直 margin 会合并；如果元素是垂直流，则水平 margin 会合并。 普通块元素可以使用 margin:auto 实现垂直居中。可以使用 text-align:center 实现图片垂直居中。可以使用 text-indent 实现文字下沉效果。可以实现全兼容的 icon fonts 图标的旋转效果。充分利用高度的高度自适应布局。

writing-mode、 direction 和 unicode-bidi 是 CSS 世界中三大可以改变文本布局流向的属性，其中 direction 和 unicode-bidi 属于近亲，经常一起使用，也是仅有的两个不受 CSS3 的 all 属性影响的 CSS 属性，基本上就是和内联元素一起使用。它貌似是为阿拉伯文字设计的。
