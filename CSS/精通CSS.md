> CSS Mastery: Advanced Web Standards Solutions, Third Edition
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

# 第一章 奠定基础

# 第二章 让你的样式达到目标

# 第三章 可视化格式模型概述

# 第四章 Web 印刷样式

# 第五章 完美盒模型

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
  - flex-direction 主轴方向（flex-direction: row|row-reverse|column|column-reverse）
  - flex-wrap 换行处理（flex-wrap: nowrap | wrap | wrap-reverse）
- justify-content 主轴对齐（justify-content: flex-start|flex-end|center|space-between|space-around）
- align-items 辅轴对齐（align-items: stretch|center|flex-start|flex-end|baseline）
- align-content 多行对齐（align-content: stretch|center|flex-start|flex-end|space-between|space-around）

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

Flexbox 对子项的排列有多种方式，沿主轴的排列叫排布（justification），沿辅轴的排列则叫对齐（alignment）。 用于指定排布方式的属性是 justify-content，其默认值是 flex-start，表示按照当前文本方向排布，关键词还有 flex-end、center、space-between、space-around。

Flexbox 不允许通过以上这些关键字指定个别项的排布方式。然而，如果指定某一项的外边距值为 auto，而且在容器里哪一侧还有空间，那么该外边距就会扩展占据可用空间。

辅轴对齐。如果增加 Flex 容器自身或其中一项的高度，会发现子项自动就等高了。实际上，控制辅轴对齐的属性 align-items，其默认值就是 stretch，其它关键字时 flex-start、center 和 flex-end。最后，后可以使用 baseline 关键字，将子项中文本的基线与容器基线对齐，效果与行内块元素的默认行为类似。

除了同时对其所有项，还可以在辅轴上指定个别项的对齐方式。使用的是 align-self 属性。align-self 属性重写了容器的 align-items 属性。

Flexbox 中的垂直对齐。在容器里只有一个元素时，只要将容器设置为 flex，再将需要居中的元素的外边距设置为 auto 就行了，因为 Flexbox 中各项的自动外边距会扩展“填充”相应方向的空间。如果 Flex 容器有多个元素，那么就可以使用对齐属性将它们聚拢到水平和垂直中心上，只需要把排布和对齐都设置为 center。

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
  min-height: 0; /* [1] */
  order: -1;
}
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

# 第八章 响应式 Web 设计和 CSS

# 第九章 样式表和数据表

# 第十章 让它动起来：Transforms，Transitions 和 Animations

# 第十一章 前沿视觉效果

# 第十二章 代码质量和工作流
