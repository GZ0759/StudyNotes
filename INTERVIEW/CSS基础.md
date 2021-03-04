> [50道CSS基础面试题（附答案）](https://segmentfault.com/a/1190000013325778)  

# 盒模型

**介绍一下标准的 CSS 的盒子模型？与低版本 IE 的盒子模型有什么不同的？**

完整的 CSS 盒模型应用于块级盒子，内联盒子只使用盒模型中定义的部分内容。模型定义了盒的每个部分 —— margin, border, padding, and content —— 合在一起就可以创建我们在页面上看到的内容。为了增加一些额外的复杂性，有一个标准的和替代（IE）的盒模型。

1. 标准盒模型。在标准盒模型中，如果给盒设置 width 和 height，实际设置的是 content box , 也就是说 padding 和 border 再加上设置的宽高一起决定整个盒子的大小。
2. 替代盒模型。可能有人会认为盒子的大小还要加上边框和内边距，因此，css 还有一个替代盒模型，也叫怪异盒子。使用这个模型，所有宽度都是可见宽度，所以内容宽度是该宽度减去边框和填充部分。

> margin 不计入实际大小。它会影响盒子在页面所占空间，但是影响的是盒子外部空间。盒子的范围到边框为止，不会延伸到 margin。

默认浏览器会使用标准模型。如果需要使用替代模型，可以通过为其设置 `box-sizing: border-box` 来实现。 这样就可以告诉浏览器使用 border-box 来定义区域，从而设定您想要的大小。Internet Explorer 默认使用替代盒模型，IE8+ 支持使用 box-sizing 进行切换。

**box-sizing 属性？**

CSS 中的 box-sizing 属性定义了 user agent（用户代理） 应该如何计算一个元素的总宽度和总高度。

1. content-box 是默认值。任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。
2. border-box 告诉浏览器：你想要设置的边框和内边距的值是包含在 width 内的。

# 选择器

**CSS选择器有哪些？**

| Basic Selectors | Combinators | Pseudo-classes | Pseudo-elements |
|---|---|---|---|
| 元素选择器 | 相邻兄弟选择器 | :hover | ::after |
| 类选择器 | 通用兄弟选择器 | :first | ::before |
| ID选择器 | 子选择器 | :first-child | ::first-letter |
| 通配选择器 | 后代选择器 | :first-of-type | ::first-line |
| 属性选择器 | Column combinator | ... | ... |

**CSS优先级算法如何计算？**

- 元素选择符： 1
- class选择符： 10
- id选择符：100
- 元素标签（内联样式）：1000

`!important`声明的样式优先级最高。如果优先级相同，则选择最后出现的样式。继承得到的样式的优先级最低。

**CSS3新增伪类有那些?**

- p:first-of-type 选择属于其父元素的首个元素
- p:last-of-type 选择属于其父元素的最后元素
- p:only-of-type 选择属于其父元素唯一的元素
- p:only-child 选择属于其父元素的唯一子元素
- p:nth-child(2) 选择属于其父元素的第二个子元素
- :enabled :disabled 表单控件的禁用状态。
- :checked 单选框或复选框被选中。

# CSS 属性

**css有继承性的属性有哪些？**

继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。一般用于设置网页上的共性信息，例如网页的文字颜色、字体、文字大小等内容。

1. 文本系列属性，如 text-indent/text-align/line-height/color
2. 字体系列属性，如 font/font-family/font-weight/font-size
3. 表格布局属性，如 caption-side/border-collapse/border-spacing
4. 列表布局属性，如 list-style-type/list-style-image/list-style-position/list-style
5. 元素可见性，如 visibility
6. 生成内容属性，如 quotes
7. 光标属性，如 cursor
8. 页面样式属性，如 page/page-break-inside/windows/orphans
9. 声音样式属性，如 speak/speak-punctuation/speak-numeral

**display有哪些值？说明他们的作用?**

- inline（默认）--内联
- none--隐藏
- block--块显示
- table--表格显示
- list-item--项目列表
- inline-block

**position的值？**

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
元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block (最近块级祖先 nearest block-level ancestor)，包括table-related元素，基于top, right, bottom, 和 left的值进行偏移。偏移值不会影响任何其他元素的位置。
该值总是创建一个新的层叠上下文（stacking context）。注意，一个sticky元素会“固定”在离它最近的一个拥有“滚动机制”的祖先上（当该祖先的overflow 是 hidden, scroll, auto, 或 overlay时），即便这个祖先不是最近的真实可滚动祖先。这有效地抑制了任何“sticky”行为。

- static（默认）：按照正常文档流进行排列；
- relative（相对定位）：不脱离文档流，参考自身静态位置通过 top, bottom, left, right 定位；
- absolute（绝对定位）：参考距其最近一个不为static的父级元素通过top, bottom, left, right 定位；
- fixed（固定定位）：所固定的参照对像是可视窗口。

# 分析

**CSS3有哪些新特性？**

**请解释一下CSS3的flexbox（弹性盒布局模型），以及适用场景？**

该布局模型的目的是提供一种更加高效的方式来对容器中的条目进行布局、对齐和分配空间。在传统的布局方式中，block 布局是把块在垂直方向从上到下依次排列的；而 inline 布局则是在水平方向来排列。弹性盒布局并没有这样内在的方向限制，可以由开发人员自由操作。

试用场景：弹性布局适合于移动前端开发，在Android和ios上也完美支持。

# 实现

**用纯CSS创建一个三角形的原理是什么？**

首先，需要把元素的宽度、高度设为0。然后设置边框样式。

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
上面那块用margin: 0 auto;居中；
下面两块用float或者inline-block不换行；
用margin调整位置使他们居中。

第二种全屏的品字布局:
上面的div设置成100%，下面的div分别宽50%，然后使用float或者inline使其不换行。

**常见的兼容性问题？**

不同浏览器的标签默认的margin和padding不一样。

```css
*{margin:0;padding:0;}
```

IE6双边距bug：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置的大。hack：display:inline;将其转化为行内属性。

渐进识别的方式，从总体中逐渐排除局部。首先，巧妙的使用“9”这一标记，将IE浏览器从所有情况中分离出来。接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。

```css
{
background-color:#f1ee18;/*所有识别*/
.background-color:#00deff\9; /*IE6、7、8识别*/
+background-color:#a200ff;/*IE6、7识别*/
_background-color:#1e0bd1;/*IE6识别*/
}
```

设置较小高度标签（一般小于10px），在IE6，IE7中高度超出自己设置高度。hack：给超出高度的标签设置overflow:hidden;或者设置行高line-height 小于你设置的高度。
IE下，可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性；Firefox下，只能使用getAttribute()获取自定义属性。解决方法:统一通过getAttribute()获取自定义属性。

Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示,可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决。
超链接访问过后hover样式就不出现了，被点击访问过的超链接样式不再具有hover和active了。解决方法是改变CSS属性的排列顺序:L-V-H-A ( love hate ): a:link {} a:visited {} a:hover {} a:active {}

**为什么要初始化CSS样式**

因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。

15 absolute的containing block计算方式跟正常流有什么不同？

无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断：

若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形；否则,则由这个祖先元素的 padding box 构成。如果都找不到，则为 initial containing block。

16 CSS里的visibility属性有个collapse属性值？在不同浏览器下以后什么区别？

当一个元素的visibility属性被设置成collapse值后，对于一般的元素，它的表现跟hidden是一样的。

- chrome中，使用collapse值和使用hidden没有区别。
- firefox，opera和IE，使用collapse值和使用display：none没有什么区别。

**display:none与visibility：hidden的区别？**

- display：none 不显示对应的元素，在文档布局中不再分配空间（回流+重绘）
- visibility：hidden 隐藏对应元素，在文档布局中仍保留原来的空间（重绘）

18 position跟display、overflow、float这些特性相互叠加后会怎么样？

display属性规定元素应该生成的框的类型；position属性规定元素的定位类型；float属性是一种布局方式，定义元素在哪个方向浮动。

类似于优先级机制：position：absolute/fixed优先级最高，有他们在时，float不起作用，display值需要调整。float 或者absolute定位的元素，只能是块元素或表格。

**对BFC规范的理解？**

BFC规定了内部的Block Box如何布局。

定位方案：
- 内部的Box会在垂直方向上一个接一个放置。
- Box垂直方向的距离由margin决定，属于同一个BFC的两个相邻Box的margin会发生重叠。
- 每个元素的margin box 的左边，与包含块border box的左边相接触。
- BFC的区域不会与float box重叠。
- BFC是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素。
- 计算BFC的高度时，浮动元素也会参与计算。

满足下列条件之一就可触发BFC
- 根元素，即html
- float的值不为none（默认）
- overflow的值不为visible（默认）
- display的值为inline-block、table-cell、table-caption
- position的值为absolute或fixed

**为什么会出现浮动和什么时候需要清除浮动？清除浮动的方式？**

浮动元素碰到包含它的边框或者浮动元素的边框停留。由于浮动元素不在文档流中，所以文档流的块框表现得就像浮动框不存在一样。浮动元素会漂浮在文档流的块框上。
浮动带来的问题：

- 父元素的高度无法被撑开，影响与父元素同级的元素
- 与浮动元素同级的非浮动元素（内联元素）会跟随其后
- 若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构。

清除浮动的方式：

- 父级div定义height
- 最后一个浮动元素后加空div标签 并添加样式clear:both。
- 包含浮动元素的父标签添加样式overflow为hidden或auto。
- 父级div定义zoom

**上下margin重合的问题**

在重合元素外包裹一层容器，并触发该容器生成一个BFC。

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

**设置元素浮动后，该元素的display值是多少？**

自动变成display:block

**移动端的布局用过媒体查询吗？**

通过媒体查询可以为不同大小和尺寸的媒体定义不同的css，适应相应的设备的显示。

```html
<head>里边
<link rel="stylesheet" type="text/css" href="xxx.css" media="only screen and (max-device-width:480px)">
```

```css
@media only screen and (max-device-width:480px) {/css样式/}
```

24 使用 CSS 预处理器吗？

Less sass

**CSS优化、提高性能的方法有哪些？**

- 避免过度约束
- 避免后代选择符
- 避免链式选择符
- 使用紧凑的语法
- 避免不必要的命名空间
- 避免不必要的重复
- 最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么
- 避免！important，可以选择其他选择器
- 尽可能的精简规则，你可以合并不同类里的重复规则

**浏览器是怎样解析CSS选择器的？**

CSS选择器的解析是从右向左解析的。若从左向右的匹配，发现不符合规则，需要进行回溯，会损失很多性能。若从右向左匹配，先找到所有的最右节点，对于每一个节点，向上寻找其父节点直到找到根元素或满足条件的匹配规则，则结束这个分支的遍历。两种匹配规则的性能差别很大，是因为从右向左的匹配在第一步就筛选掉了大量的不符合条件的最右节点（叶子节点），而从左向右的匹配规则的性能都浪费在了失败的查找上面。

而在 CSS 解析完毕后，需要将解析的结果与 DOM Tree 的内容一起进行分析建立一棵 Render Tree，最终用来进行绘图。在建立 Render Tree 时（WebKit 中的「Attachment」过程），浏览器就要为每个 DOM Tree 中的元素根据 CSS 的解析结果（Style Rules）来确定生成怎样的 Render Tree。

27 在网页中的应该使用奇数还是偶数的字体？为什么呢？

使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。

**margin和padding分别适合什么场景使用？**

何时使用margin：
- 需要在border外侧添加空白
- 空白处不需要背景色
- 上下相连的两个盒子之间的空白，需要相互抵消时。

何时使用padding：
- 需要在border内侧添加空白
- 空白处需要背景颜色
- 上下相连的两个盒子的空白，希望为两者之和。

兼容性的问题：在IE5 IE6中，为float的盒子指定margin时，左侧的margin可能会变成两倍的宽度。通过改变padding或者指定盒子的display：inline解决。

**元素竖向的百分比设定是相对于容器的高度吗？**

当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，但是，对于一些表示竖向距离的属性，例如 padding-top , padding-bottom , margin-top , margin-bottom 等，当按百分比设定它们时，依据的也是父容器的宽度，而不是高度。

30 全屏滚动的原理是什么？用到了CSS的哪些属性？

原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500%，只是展示100%，剩下的可以通过transform进行y轴定位，也可以通过margin-top实现
overflow：hidden；transition：all 1000ms ease；

31 什么是响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？

响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。
基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。
页面头部必须有meta声明的viewport。

```html
<meta name=’viewport’ content=”width=device-width, initial-scale=1. maximum-scale=1,user-scalable=no”>
```

32 视差滚动效果？

视差滚动（Parallax Scrolling）通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的3D效果。

CSS3实现
优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器
jQuery实现
通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。
优点：能兼容到各个版本的，效果可控性好
缺点：开发起来对制作者要求高
插件实现方式
例如：parallax-scrolling，兼容性十分好

**::before 和 :after中双冒号和单冒号有什么区别？解释一下这2个伪元素的作用**

单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。
::before就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于dom之中，只存在在页面之中。
:before 和 :after 这两个伪元素，是在CSS2.1里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着Web的进化，在CSS3的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

**你对line-height是如何理解的？**

行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS中起高度作用的是height和line-height，没有定义height属性，最终其表现作用一定是line-height。
单行文本垂直居中：把line-height值设置为height一样大小的值可以实现单行文字的垂直居中，其实也可以把height删除。
多行文本垂直居中：需要设置display属性为inline-block。

**怎么让Chrome支持小于12px 的文字？**

```css
p{font-size:10px;-webkit-transform:scale(0.8);} //0.8是缩放比例
```

36 让页面里的字体变清晰，变细用CSS怎么做？

-webkit-font-smoothing在window系统下没有起作用，但是在IOS设备上起作用-webkit-font-smoothing：antialiased是最佳的，灰度平滑。

37 position:fixed;在android下无效怎么处理？

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>

**如果需要手动写动画，你认为最小时间间隔是多久，为什么？**

多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60＊1000ms ＝ 16.7ms。

39 li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？

行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为0，就没有空格了。
解决方法：

可以将<li>代码全部写在一排
浮动li中float：left
在ul中用font-size：0（谷歌不支持）；可以使用letter-space：-3px

40 display:inline-block 什么时候会显示间隙？

有空格时候会有间隙 解决：移除空格
margin正值的时候 解决：margin使用负值
使用font-size时候 解决：font-size:0、letter-spacing、word-spacing

41 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度

外层div使用position：relative；高度要求自适应的div使用position: absolute; top: 100px; bottom: 0; left: 0

42 png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp？

png是便携式网络图片（Portable Network Graphics）是一种无损数据压缩位图文件格式.优点是：压缩比高，色彩好。 大多数地方都可以用。
jpg是一种针对相片使用的一种失真压缩方法，是一种破坏性的压缩，在色调及颜色平滑变化做的不错。在www上，被用来储存和传输照片的格式。
gif是一种位图文件格式，以8位色重现真色彩的图像。可以实现动画效果.
webp格式是谷歌在2010年推出的图片格式，压缩率只有jpg的2/3，大小比png小了45%。缺点是压缩的时间更久了，兼容性不好，目前谷歌和opera支持。

43 style标签写在body后与body前有什么区别？

页面加载自上而下 当然是先加载样式。
写在body标签后由于浏览器以逐行方式对HTML文档进行解析，当解析到写在尾部的样式表（外联或写在style标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在windows的IE下可能会出现FOUC现象（即样式失效导致的页面闪烁问题）

44 CSS属性overflow属性定义溢出元素内容区的内容会如何处理?

参数是scroll时候，必会出现滚动条。
参数是auto时候，子元素内容大于父元素时出现滚动条。
参数是visible时候，溢出的内容出现在父元素之外。
参数是hidden时候，溢出隐藏。

**阐述一下CSS Sprites**

将一个页面涉及到的所有图片都包含到一张大图中去，然后利用CSS的 background-image，background- repeat，background-position 的组合进行背景定位。利用CSS Sprites能很好地减少网页的http请求，从而大大的提高页面的性能；CSS Sprites能减少图片的字节。