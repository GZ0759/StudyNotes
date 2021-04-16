> [50 道 CSS 基础面试题（附答案）](https://segmentfault.com/a/1190000013325778)

# 盒模型

## 标准盒模型和 IE 盒模型

介绍一下标准的 CSS 的盒子模型？与低版本 IE 的盒子模型有什么不同的？

完整的 CSS 盒模型应用于块级盒子，内联盒子只使用盒模型中定义的部分内容。模型定义了盒的每个部分 margin/border/padding/content，这些合在一起就可以创建我们在页面上看到的内容。为了增加一些额外的复杂性，有一个标准的和替代（IE）的盒模型。

1. 标准盒模型 Standards Mode。在标准盒模型中，如果给盒设置 width 和 height，实际设置的是 content box , 也就是说 padding 和 border 再加上设置的宽高一起决定整个盒子的大小。
2. 替代盒模型 Quirks Mode。可能有人会认为盒子的大小本身要算上边框和内边距，因此，CSS 还有一个替代盒模型，也叫怪异盒子。使用这个模型，所有宽度都是可见宽度，所以内容宽度 content 是该宽度减去边框和内边距部分。

> margin 不计入实际大小。它会影响盒子在页面所占空间，但是影响的是盒子外部空间。盒子的范围到边框为止，不会延伸到 margin。

默认浏览器会使用标准模型。如果需要使用替代模型，可以通过为其设置 `box-sizing: border-box` 来实现。 这样就可以告诉浏览器使用 border-box 来定义区域，从而设定您想要的大小。Internet Explorer 默认使用替代盒模型，IE8+ 支持使用 box-sizing 进行切换。

## 行内元素和块级元素

1. 行内元素：一个行内元素只占据它对应标签的边框所包含的空间。
  - a/button/big/em/i/input/mark/span/select/option/strog/b/sup/sub/textarea/u
2. 块级元素：块级元素占据其父元素（容器）的整个空间，因此创建了一个“块”。通常浏览器会在块级元素前后另起一个新行。
  - table/dl-dt-dd/figure/figcaption/div/h1-h6/hr/ul-li/ol-li/nav/p/form
3. 行内块状元素 
  - img/input

块级元素的特点

1. 独占一行，每一个块级元素都会从新的一行重新开始
2. 排列方式是从上到下依次排布
3. 可以直接控制宽度、高度以及盒子模型的相关 CSS 属性
4. 在不设置宽度的情况下，块级元素的宽度是它父级元素内容的宽度，高度是它本身内容的高度
5. 块级元素可以嵌套行内元素
6. ul/ol下面只能是li；dl下面只能是dt/dd
7. p不能包裹其他块级元素包括它本身，可以嵌套行内元素

## box-sizing

box-sizing 属性？

CSS 中的 box-sizing 属性定义了 user agent（用户代理）应该如何计算一个元素的总宽度和总高度。

1. content-box 是默认值。任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。
2. border-box 告诉浏览器：你想要设置的边框和内边距的值是包含在 width 内的。

## 回流和重绘

回流，当 Render Tree 中部分或全部元素的尺寸、结构、或某些属性发生改变时，浏览器重新渲染部分或全部文档。

会导致回流的操作：

- 页面首次渲染
- 浏览器窗口大小发生改变
- 元素尺寸或位置发生改变
- 元素内容变化（文字数量或图片大小等等）
- 元素字体大小变化
- 添加或者删除可见的DOM元素
- 激活CSS伪类（例如：:hover）
- 查询某些属性或调用某些方法

一些常用且会导致回流的属性和方法：

```
clientWidth、clientHeight、clientTop、clientLeft
offsetWidth、offsetHeight、offsetTop、offsetLeft
scrollWidth、scrollHeight、scrollTop、scrollLeft
scrollIntoView()、scrollIntoViewIfNeeded()
getComputedStyle()
getBoundingClientRect()
scrollTo()
```

重绘：当页面中元素样式的改变并不影响它在文档流中的位置时，浏览器会将新样式赋予给元素并重新绘制它。

```
color、background-color、visibility
```


# 选择器

**CSS 选择器有哪些？**

| Basic Selectors | Combinators       | Pseudo-classes | Pseudo-elements |
| --------------- | ----------------- | -------------- | --------------- |
| 元素选择器      | 相邻兄弟选择器    | :hover         | ::after         |
| 类选择器        | 通用兄弟选择器    | :first         | ::before        |
| ID 选择器       | 子选择器          | :first-child   | ::first-letter  |
| 通配选择器      | 后代选择器        | :first-of-type | ::first-line    |
| 属性选择器      | Column combinator | ...            | ...             |

**CSS 优先级算法如何计算？**

- 元素选择符：1
- class 选择符：10
- id 选择符：100
- 元素标签（内联样式）：1000

`!important`声明的样式优先级最高。如果优先级相同，则选择最后出现的样式。继承得到的样式的优先级最低。

- `!important` > 行内样式 > `#id` > `.class` > tag > `*` > 继承 > 默认
- 选择器 从右往左 解析

**CSS3 新增伪类有那些?**

- p:first-of-type 选择属于其父元素的首个元素
- p:last-of-type 选择属于其父元素的最后元素
- p:only-of-type 选择属于其父元素唯一的元素
- p:only-child 选择属于其父元素的唯一子元素
- p:nth-child(2) 选择属于其父元素的第二个子元素
- :enabled :disabled 表单控件的禁用状态。
- :checked 单选框或复选框被选中。

# CSS 属性

**css 有继承性的属性有哪些？**

继承是一种规则，它允许样式不仅应用于某个特定 html 标签元素，而且应用于其后代。一般用于设置网页上的共性信息，例如网页的文字颜色、字体、文字大小等内容。

1. 文本系列属性，如 text-indent/text-align/line-height/color
2. 字体系列属性，如 font/font-family/font-weight/font-size
3. 表格布局属性，如 caption-side/border-collapse/border-spacing
4. 列表布局属性，如 list-style-type/list-style-image/list-style-position/list-style
5. 元素可见性，如 visibility
6. 生成内容属性，如 quotes
7. 光标属性，如 cursor
8. 页面样式属性，如 page/page-break-inside/windows/orphans
9. 声音样式属性，如 speak/speak-punctuation/speak-numeral

**display 有哪些值？说明他们的作用?**

- inline（默认）--内联
- none--隐藏
- block--块显示
- table--表格显示
- list-item--项目列表
- inline-block

**position 的值？**

position 属性被指定为从下面的值列表中选择的单个关键字。

1. static
   该关键字指定元素使用正常的布局行为，即元素在文档常规流中当前的布局位置。此时 top, right, bottom, left 和 z-index 属性无效。
2. relative
   该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。`position:relative` 对 `table-*-group`, `table-row`, `table-column`, `table-cell`, `table-caption` 元素无效。
3. absolute
   元素会被移出正常文档流，并不为元素预留空间，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并。
4. fixed
   元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于屏幕视口（viewport）的位置来指定元素位置。元素的位置在屏幕滚动时不会改变。打印时，元素会出现在的每页的固定位置。fixed 属性会创建新的层叠上下文。当元素祖先的 transform, perspective 或 filter 属性非 none 时，容器由视口改为该祖先。
5. sticky
   元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block (最近块级祖先 nearest block-level ancestor)，包括 table-related 元素，基于 top, right, bottom, 和 left 的值进行偏移。偏移值不会影响任何其他元素的位置。
   该值总是创建一个新的层叠上下文（stacking context）。注意，一个 sticky 元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上（当该祖先的 overflow 是 hidden, scroll, auto, 或 overlay 时），即便这个祖先不是最近的真实可滚动祖先。这有效地抑制了任何“sticky”行为。

- static（默认）：按照正常文档流进行排列；
- relative（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；
- absolute（绝对定位）：参考距其最近一个不为 static 的父级元素通过 top, bottom, left, right 定位；
- fixed（固定定位）：所固定的参照对像是可视窗口。

# 分析

**CSS3 有哪些新特性？**

**请解释一下 CSS3 的 flexbox（弹性盒布局模型），以及适用场景？**

该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。在传统的布局方式中，block 布局是把块在垂直方向从上到下依次排列的；而 inline 布局则是在水平方向来排列。弹性盒布局并没有这样内在的方向限制，可以由开发人员自由操作。

试用场景：弹性布局适合于移动前端开发，在 Android 和 ios 上也完美支持。

# 实现

**用纯 CSS 创建一个三角形的原理是什么？**

首先，需要把元素的宽度、高度设为 0。然后设置边框样式。

```css
.triangle {
  width: 0;
  height: 0;
  border: 40px solid transparent;
  border-top-width: 0;
  border-bottom-color: blue;
}
```

**实现直角箭头**

可支持旋转和缩放，进行方向管理和角度管理（角度要计算 scaleX()）

```css
.triangle {
  position: relative;
  width: 0;
  height: 0;
  border: 40px solid transparent;
  border-top-width: 0;
  border-bottom-color: blue;
}
.triangle::after {
  content: '';
  position: absolute;
  left: -38px;
  top: 2px;
  width: 0;
  height: 0;
  border: 38px solid transparent;
  border-top-width: 0;
  border-bottom-color: white;
}
```

**一个满屏品字布局如何设计?**

第一种真正的品字：

三块高宽是确定的；
上面那块用 margin: 0 auto;居中；
下面两块用 float 或者 inline-block 不换行；
用 margin 调整位置使他们居中。

第二种全屏的品字布局:
上面的 div 设置成 100%，下面的 div 分别宽 50%，然后使用 float 或者 inline 使其不换行。

**常见的兼容性问题？**

不同浏览器的标签默认的 margin 和 padding 不一样。

```css
* {
  margin: 0;
  padding: 0;
}
```

IE6 双边距 bug：块属性标签 float 后，又有横行的 margin 情况下，在 IE6 显示 margin 比设置的大。hack：display:inline;将其转化为行内属性。

渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将 IE 浏览器从所有情况中分离出来。接着，再次使用“+”将 IE8 和 IE7、IE6 分离开来，这样 IE8 已经独立识别。

```css
 {
  background-color: #f1ee18; /*所有识别*/
  .background-color: #00deff\9; /*IE6、7、8识别*/
  +background-color: #a200ff; /*IE6、7识别*/
  _background-color: #1e0bd1; /*IE6识别*/
}
```

设置较小高度标签（一般小于 10px），在 IE6，IE7 中高度超出自己设置高度。hack：给超出高度的标签设置 overflow:hidden;或者设置行高 line-height 小于你设置的高度。
IE 下，可以使用获取常规属性的方法来获取自定义属性,也可以使用 getAttribute()获取自定义属性；Firefox 下，只能使用 getAttribute()获取自定义属性。解决方法:统一通过 getAttribute()获取自定义属性。

Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
超链接访问过后 hover 样式就不出现了，被点击访问过的超链接样式不再具有 hover 和 active 了。解决方法是改变 CSS 属性的排列顺序:L-V-H-A ( love hate ): a:link {} a:visited {} a:hover {} a:active {}

**为什么要初始化 CSS 样式**

因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对 CSS 初始化往往会出现浏览器之间的页面显示差异。

15 absolute 的 containing block 计算方式跟正常流有什么不同？

无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：

若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形；否则,则由这个祖先元素的 padding box 构成。如果都找不到，则为 initial containing block。

16 CSS 里的 visibility 属性有个 collapse 属性值？在不同浏览器下以后什么区别？

当一个元素的 visibility 属性被设置成 collapse 值后，对于一般的元素，它的表现跟 hidden 是一样的。

- chrome 中，使用 collapse 值和使用 hidden 没有区别。
- firefox，opera 和 IE，使用 collapse 值和使用 display：none 没有什么区别。

**display:none 与 visibility：hidden 的区别？**

- display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）
- visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

18 position 跟 display、overflow、float 这些特性相互叠加后会怎么样？

display 属性规定元素应该生成的框的类型；position 属性规定元素的定位类型；float 属性是一种布局方式，定义元素在哪个方向浮动。

类似于优先级机制：position：absolute/fixed 优先级最高，有他们在时，float 不起作用，display 值需要调整。float 或者 absolute 定位的元素，只能是块元素或表格。

**对 BFC 规范的理解？**

格式化上下文，是一个独立的渲染区域，让处于 BFC 内部的元素与外部的元素相互隔离，使内外元素的定位不会相互影响。BFC 规定了内部的 Block Box 如何布局。

定位方案：

- 内部的 Box 会在垂直方向上一个接一个放置。
- Box 垂直方向的距离由 margin 决定，属于同一个 BFC 的两个相邻 Box 的 margin 会发生重叠。
- 每个元素的 margin box 的左边，与包含块 border box 的左边相接触。
- BFC 的区域不会与 float box 重叠。
- BFC 是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
- 计算 BFC 的高度时，浮动元素也会参与计算。

满足下列条件之一就可触发 BFC

- 根元素，即 html 元素
- float 的值不为 none（默认）
- position 的值为 absolute 或 fixed
- display 的值为 inline-block/table-cell/table-caption/flex/inline-flex
- overflow 的值不为 visible（默认）

解决问题

- 防止外边距折叠
- 包含浮动元素 防止父元素高度坍塌
- 防止文字环绕

**为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？**

浮动元素碰到包含它的边框或者浮动元素的边框停留。由于浮动元素不在文档流中，所以文档流的块框表现得就像浮动框不存在一样。浮动元素会漂浮在文档流的块框上。
浮动带来的问题：

- 父元素的高度无法被撑开，影响与父元素同级的元素
- 与浮动元素同级的非浮动元素（内联元素）会跟随其后
- 若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构。

清除浮动的方式：

- 父级 div 定义 height
- 最后一个浮动元素后加空 div 标签 并添加样式 clear:both。
- 包含浮动元素的父标签添加样式 overflow 为 hidden 或 auto。
- 父级 div 定义 zoom

**上下 margin 重合的问题**

在重合元素外包裹一层容器，并触发该容器生成一个 BFC。

例子：

```
<div class="aside"></div>
<div class="text">
  <div class="main"></div>
</div>
<!--下面是css代码-->
.aside {
  margin-bottom: 100px;
  width: 100px;
  height: 150px;
  background: #f66;
}
.main {
  margin-top: 100px;
  height: 200px;
  background: #fcc;
}
.text{
  /*盒子main的外面包一个div，通过改变此div的属性使两个盒子分属于两个不同的BFC，以此来阻止margin重叠*/
  overflow: hidden;  //此时已经触发了BFC属性。
}
```

**设置元素浮动后，该元素的 display 值是多少？**

自动变成 display:block

**移动端的布局用过媒体查询吗？**

通过媒体查询可以为不同大小和尺寸的媒体定义不同的 css，适应相应的设备的显示。

```html
<head>
  里边
  <link
    rel="stylesheet"
    type="text/css"
    href="xxx.css"
    media="only screen and (max-device-width:480px)"
  />
</head>
```

```css
@media only screen and (max-device-width:480px) {/css样式/}
```

24 使用 CSS 预处理器吗？

Less sass

**CSS 优化、提高性能的方法有哪些？**

- 避免过度约束
- 避免后代选择符
- 避免链式选择符
- 使用紧凑的语法
- 避免不必要的命名空间
- 避免不必要的重复
- 最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么
- 避免！important，可以选择其他选择器
- 尽可能的精简规则，你可以合并不同类里的重复规则

**浏览器是怎样解析 CSS 选择器的？**

CSS 选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。

而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。

27 在网页中的应该使用奇数还是偶数的字体？为什么呢？

使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px 时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。

**margin 和 padding 分别适合什么场景使用？**

何时使用 margin：

- 需要在 border 外侧添加空白
- 空白处不需要背景色
- 上下相连的两个盒子之间的空白，需要相互抵消时。

何时使用 padding：

- 需要在 border 内侧添加空白
- 空白处需要背景颜色
- 上下相连的两个盒子的空白，希望为两者之和。

兼容性的问题：在 IE5 IE6 中，为 float 的盒子指定 margin 时，左侧的 margin 可能会变成两倍的宽度。通过改变 padding 或者指定盒子的 display：inline 解决。

**元素竖向的百分比设定是相对于容器的高度吗？**

当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，但是，对于一些表示竖向距离的属性，例如 padding-top , padding-bottom , margin-top , margin-bottom 等，当按百分比设定它们时，依据的也是父容器的宽度，而不是高度。

30 全屏滚动的原理是什么？用到了 CSS 的哪些属性？

原理：有点类似于轮播，整体的元素一直排列下去，假设有 5 个需要展示的全屏页面，那么高度是 500%，只是展示 100%，剩下的可以通过 transform 进行 y 轴定位，也可以通过 margin-top 实现
overflow：hidden；transition：all 1000ms ease；

31 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的 IE？

响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。
基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。
页面头部必须有 meta 声明的 viewport。

```html
<meta
  name="’viewport’"
  content="”width"
  ="device-width,"
  initial-scale="1."
  maximum-scale="1,user-scalable"
  ="no”"
/>
```

32 视差滚动效果？

视差滚动（Parallax Scrolling）通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的 3D 效果。

CSS3 实现
优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器
jQuery 实现
通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。
优点：能兼容到各个版本的，效果可控性好
缺点：开发起来对制作者要求高
插件实现方式
例如：parallax-scrolling，兼容性十分好

**::before 和 :after 中双冒号和单冒号有什么区别？解释一下这 2 个伪元素的作用**

单冒号(:)用于 CSS3 伪类，双冒号(::)用于 CSS3 伪元素。
::before 就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于 dom 之中，只存在在页面之中。
:before 和 :after 这两个伪元素，是在 CSS2.1 里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着 Web 的进化，在 CSS3 的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

**你对 line-height 是如何理解的？**

行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS 中起高度作用的是 height 和 line-height，没有定义 height 属性，最终其表现作用一定是 line-height。
单行文本垂直居中：把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中，其实也可以把 height 删除。
多行文本垂直居中：需要设置 display 属性为 inline-block。

**怎么让 Chrome 支持小于 12px 的文字？**

```css
p {
  font-size: 10px;
  -webkit-transform: scale(0.8);
} //0.8是缩放比例
```

36 让页面里的字体变清晰，变细用 CSS 怎么做？

-webkit-font-smoothing 在 window 系统下没有起作用，但是在 IOS 设备上起作用-webkit-font-smoothing：antialiased 是最佳的，灰度平滑。

37 position:fixed;在 android 下无效怎么处理？

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>

**如果需要手动写动画，你认为最小时间间隔是多久，为什么？**

多数显示器默认频率是 60Hz，即 1 秒刷新 60 次，所以理论上最小间隔为 1/60＊1000ms ＝ 16.7ms。

39 li 与 li 之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为 0，就没有空格了。
解决方法：

可以将<li>代码全部写在一排
浮动 li 中 float：left
在 ul 中用 font-size：0（谷歌不支持）；可以使用 letter-space：-3px

40 display:inline-block 什么时候会显示间隙？

有空格时候会有间隙 解决：移除空格
margin 正值的时候 解决：margin 使用负值
使用 font-size 时候 解决：font-size:0、letter-spacing、word-spacing

41 有一个高度自适应的 div，里面有两个 div，一个高度 100px，希望另一个填满剩下的高度

外层 div 使用 position：relative；高度要求自适应的 div 使用 position: absolute; top: 100px; bottom: 0; left: 0

42 png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过 webp？

png 是便携式网络图片（Portable Network Graphics）是一种无损数据压缩位图文件格式.优点是：压缩比高，色彩好。 大多数地方都可以用。
jpg 是一种针对相片使用的一种失真压缩方法，是一种破坏性的压缩，在色调及颜色平滑变化做的不错。在 www 上，被用来储存和传输照片的格式。
gif 是一种位图文件格式，以 8 位色重现真色彩的图像。可以实现动画效果.
webp 格式是谷歌在 2010 年推出的图片格式，压缩率只有 jpg 的 2/3，大小比 png 小了 45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和 opera 支持。

43 style 标签写在 body 后与 body 前有什么区别？

页面加载自上而下 当然是先加载样式。
写在 body 标签后由于浏览器以逐行方式对 HTML 文档进行解析，当解析到写在尾部的样式表（外联或写在 style 标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在 windows 的 IE 下可能会出现 FOUC 现象（即样式失效导致的页面闪烁问题）

44 CSS 属性 overflow 属性定义溢出元素内容区的内容会如何处理?

参数是 scroll 时候，必会出现滚动条。
参数是 auto 时候，子元素内容大于父元素时出现滚动条。
参数是 visible 时候，溢出的内容出现在父元素之外。
参数是 hidden 时候，溢出隐藏。

**阐述一下 CSS Sprites**

将一个页面涉及到的所有图片都包含到一张大图中去，然后利用 CSS 的 background-image，background- repeat，background-position 的组合进行背景定位。利用 CSS Sprites 能很好地减少网页的 http 请求，从而大大的提高页面的性能；CSS Sprites 能减少图片的字节。

**css+background 实现 图片宽高自适应**

```html
<div
  style="width:500px; height:600px; border: 1px solid #000000; background: url(http://img17.3lian.com/d/file/201703/07/4ceeb6fc3d7956ac7731290a603e0a84.jpg) no-repeat; background-size:cover; 　　 background-position: center center; "
></div>
```

## 布局

### 水平垂直居中布局

水平居中。

- 使用`text-align + inline-block`。此方案兼容性较好，可兼容至 IE8，对于 IE567 并不支持 inline-block，需要使用 css hack 进行兼容。
- 使用`table + margin`。此方案兼容至 IE8，可以使用`<table/>`标签代替 css 写法，兼容性良好。另外也直接在某些情况下直接使用 `margin: 0 auto` 。
- 使用`absolute + transform`。此方案兼容至 IE9，因为 transform 兼容性限制。如果`.child`为定宽元素，可以使用`margin-left`为元素一般宽度的负数值，兼容性极佳。
  - 子元素绝对定位，使其左侧位置是相对框真实宽度的一半，再往左移动自身宽度的一般。
- 使用`flex + justify-content`。通过 CSS3 的 一维布局 flex 实现，可以轻松的满足各种居中、对其、平分的布局要求。

垂直居中。

- 使用`height + line-height`。
- 使用`table-cell + vertial-align`。将富矿转化为一个表格单元格显示。
- 使用`absolute + transform`。存在 css3 兼容问题，定宽兼容性良好。
- 使用`flex + align-items`。高版本浏览器兼容，低版本不适用。
