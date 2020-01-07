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

但是这样做也有缺点，那就是CSS规范不能涵盖一切。所以我们没有办法指着某些文件说：这就是CSS3，而是应该分模块学习不同的特性。模块的灵活性有时可以弥补由此引起的语义不足。如果要看单独的完整规范，可以留意CSS工作组每年发布的[Snapshot 文档](https://www.w3.org/Style/CSS/)。

## 1.2 元素

元素是文档结构的根基。在 HTML 中，最常见的元素有 `p`, `table`, `span`, `a`, 和 `div`等。文档中的每个元素都对文档起一定作用。

### 1.2.1 置换元素和非置换元素

虽然 CSS 依赖于元素，但并不是所有的元素都以同样的方式创建的。例如，图像和段落不是同一类型的元素，`span` 和 `div` 也不是。在 CSS 中，元素通常有两种形式:置换元素和非置换。

#### 置换元素

置换元素（replaced element）指用来置换元素内容的部分不由文档内容直接表示。在 HTML 中，最常见的置换元素要数 img ，它的内容由文档之外的图像文件替换。其实，通过下面这个简单的例子可以看出， img 元素没有内容。

```html
<img src="howdy.gif" />
```

如果指向的图像文件存在，文档会把那个图像显示出来，否则，浏览器什么也不显示，或者限时“图像损坏”占位符。

input 元素类似，根据类型的不同， 会替换成单选按钮、复选框或文本输入框。

#### 非置换元素

HTML 元素大部分是非置换元素（nonreplaced element），即元素的内容由用户代理（通常为浏览器）在元素自身生成的框中显示。例如，`<span>hi there</span>`是非置换元素，用户代理会显示“hi there”文本。段落、标题、单元格、列表，以及 HTML 中其他几乎所有元素都是非置换元素。

### 1.2.2 元素的显示方式

除了置换元素和非置换元素，CSS还把元素分为块级和行内两种基本类型。（这两种最常见，除此之外还有其他的显示类型）。

#### 块级元素

块级元素默认生成一个填满父级元素内容区域的框，旁边不能有其他元素。也就是说，块级元素在元素框前后都有断行。常见的块级元素有p和div。

列表项目是一种特殊的块级元素，它会在元素框旁边生成一个记号（无序列表通常是圆点，有序列表通常是数字），除此之外列表项目和其他块级元素并没有什么不同。

#### 行内元素

行内元素在一行文本内生成元素框，不打断所在的行。最常见的行内元素是a。

在HTML中，块级元素不能出现在行内元素中。但是在CSS中没有这个限制，可以随便嵌套。

```html
<body>
  <p>This is a paragraph with <em>an inline element</em> within it.</p>
</body>
```

```css
p {
  display: inline;
}
em {
  display: block;
}
```

```html
<em><p>This is a paragraph improperly enclosed by an inline element.</p></em>
```

```html
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

# 第 2 章 选择器
第 3 章 特异性和级联
第 4 章 值和单位
第 5 章 字体
第 6 章 文本属性
第 7 章 基本的视觉格式化
第 8 章 Padding, Borders, Outlines 和 Margins
第 9 章 颜色、背景和渐变
第 10 章 浮动和形状
第 11 章 定位
第 12 章 灵活的框布局
第 13 章 网格布局
第 14 章 CSS 中的表格布局
第 15 章 列表和生成的内容
第 16 章 转换
第 17 章 跃迁
第 18 章 动画
第 19 章 过滤器，混合，剪切和掩蔽
第 20 章 Media-Dependent 风格