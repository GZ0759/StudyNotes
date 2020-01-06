> CSS权威指南第四版  
> CSS:The Definitive Guide(4th Edition)
> 2000-05-01: First Release  
> 2004-03-01: Second Release  
> 2006-11-01: Third Release  
> 2017-10-10: Fourth Release  
> [线上资源](https://github.com/gdut-yy/CSS-The-Definitive-Guide-4th-zh)

# 第 1 章 CSS 和 Documents

层叠样式表(Cascading Style Sheets, CSS)是一种强大的工具，它可以转换文档或文档集合的格式，而且它已经扩展到 web 的几乎每个角落，并进入许多表面上没有 web 的环境。例如，基于 gecko 的浏览器使用 CSS 来影响浏览器 chrome 本身的表现，许多 RSS 客户端允许您将 CSS 应用于提要和提要条目，一些即时消息客户端使用 CSS 来格式化聊天窗口。CSS 的各个方面可以在 JavaScript 框架使用的语法中找到，甚至在 JavaScript 本身中也可以找到。到处都是!

## 1.1 A Brief History of (Web) Style

CSS 最初是在 1994 年提出的，当时 web 刚刚开始流行。当时，浏览器为用户提供了各种样式设置功能——例如，Mosaic 中的表示首选项允许用户在每个元素的基础上定义各种字体、大小和颜色。这些对文档作者都是不可用的;他们所能做的就是将一段内容标记为段落、某个级别的标题、预先格式化的文本或少数其他元素类型之一。如果一个用户配置他的浏览器使所有一级的标题都是小的和粉红色的，而所有六级的标题都是大的和红色的，那么，这就是他的问题了。

CSS 就是在这种环境中引入的。它的目标是提供一种简单的、声明式的样式语言，这种语言对作者来说是灵活的，最重要的是，它为作者和用户都提供了样式功能。通过“级联”的方式，这些风格可以被组合在一起并按优先级排列，这样作者和读者都有发言权——尽管读者总是拥有最后的发言权。

工作进展迅速，到 1996 年年底，CSS1 已经完成。当新成立的 CSS 工作组推进 CSS2 时，浏览器却难以以互操作的方式实现 CSS1。尽管每个 CSS 片段本身相当简单，但是这些片段的组合创建了一些令人惊讶的复杂行为。在早期的实现中也有一些不幸的失误，比如 box 模型实现中臭名昭著的差异。这些问题威胁着 CSS 的发展，但幸运的是，一些聪明的建议得以实施，浏览器开始协调起来。在几年之内，由于增强的互操作性和引人注目的发展，例如基于 CSS 的 Wired 杂志的重新设计和 CSS Zen Garden, CSS 开始流行起来。

然而，在这一切发生之前，CSS 工作组已经在 1998 年初确定了 CSS2 规范。CSS2 完成后，立即开始 CSS3 的工作，并将 CSS2 的一个明确版本称为 CSS2.1。为了顺应时代精神，CSS3 被构建为一系列(理论上)独立的模块，而不是单一的单一规范。这种方法反映了当时处于活动状态的 XHTML 规范，出于类似的原因，该规范被划分为多个模块。

模块化 CSS3 的基本原理是，每个模块都可以按照自己的速度工作，而且特别重要的(或流行的)模块可以按照 W3C 的进度前进，而不会受到其他模块的阻碍。事实上，事实就是如此。到 2012 年初，三个 CSS3 模块(以及 CSS1 和 CSS 2.1)已经达到了完全推荐状态——CSS 颜色级别 3、CSS 名称空间和选择器级别 3。与此同时，有 7 个模块处于候选推荐状态，其他几十个模块处于不同的工作草拟阶段。在旧的方法下，颜色、选择器和名称空间必须等到规范的其他部分完成或删除之后才能成为完整规范的一部分。由于模块化，他们不必等待。

这种优势的另一面是，很难谈论一个“CSS3 规范”。“没有这种东西，也不可能有。即使其他所有的 CSS 模块在 2016 年末达到了第 3 级(他们没有)，已经有了第 4 级的选择器。我们会把它称为 CSS4 吗?还有哪些“CSS3”特性仍在发挥作用?或者网格布局，甚至还没有达到一级?

因此，虽然我们不能指着一本大部头说“有 CSS3”，但我们可以通过介绍这些功能的模块名称来谈论它们。这些灵活性模块不仅弥补了它们有时造成的语义上的尴尬。(如果你想要一个近似于单一规范的东西，CSS 工作组每年都会发布“快照”文档。)

有了这些，我们就可以开始理解 CSS 了。不过，我们必须先检查一下标记。

## 1.2 Elements

元素是文档结构的基础。在 HTML 中，最常见的元素很容易识别，如 `p`, `table`, `span`, `a`, 和 `div`。文档中的每个元素都在其表示中起作用。

### 1.2.1 Replaced and Nonreplaced Elements

虽然 CSS 依赖于元素，但并不是所有的元素都是平等创建的。例如，图像和段落不是同一类型的元素，`span` and `div` 也不是。在 CSS 中，元素通常有两种形式:替换和非替换。

#### Replaced elements

被替换的元素是那些元素的内容被文档内容没有直接表示的内容所替换的元素。最熟悉的 HTML 示例可能是 img 元素，它被文档本身外部的图像文件所取代。事实上，img 并没有实际的内容，你可以在这个简单的例子中看到:

```html
<img src="howdy.gif" />
```

这个标记片段只包含一个元素名和一个属性。元素不会显示任何内容，除非您将其指向某些外部内容(在本例中，是由 src 属性指定的图像)。如果您指向一个有效的图像文件，则图像将被放置在文档中。如果没有，它将不显示任何内容，或者浏览器将显示一个“损坏的图像”占位符。

类似地，input 元素也可以替换为单选按钮、复选框或文本输入框，这取决于它的类型。

#### Nonreplaced elements

大多数 HTML 元素是不可替换的元素。这意味着它们的内容由用户代理(通常是浏览器)在元素本身生成的框中显示。例如，`<span>hi there</span>` 是一个不可替换的元素，文本“hi there”将由用户代理显示。这适用于 HTML 中的段落、标题、表格单元格、列表和几乎所有其他内容。

### 1.2.2 Element Display Roles

除了替换和非替换元素外，CSS 还使用了其他两种基本类型的元素:块级和行内级。还有更多的显示类型，但这些是最基本的，也是大多数(如果不是所有)其他显示类型所引用的类型。对于那些花时间研究 HTML 标记及其在 web 浏览器中的显示的作者来说，块类型和内联类型是很熟悉的。这些元素如图 1-1 所示。

```html
<Figures figure="1-1">Block- and inline-level elements in an HTML document</Figures>
```

#### Block-level elements

块级元素生成一个元素框，该元素框(默认情况下)填充其父元素的内容区域，并且不能在其两侧有其他元素。换句话说，它在元素框之前和之后生成“break”。HTML 中最常见的块元素是 p 和 div。被替换的元素可以是块级别的元素，但通常不是。

列表项是块级元素的特殊情况。除了以与其他块元素一致的方式工作外，它们还生成一个标记(通常是无序列表的项目符号和有序列表的数字)，该标记被“附加”到元素框中。除了此标记之外，列表项在其他所有方面都与其他块元素相同。

#### Inline-level elements

内联级元素在一行文本中生成一个元素框，并且不会破坏该行的流。最好的内联元素示例是 HTML 中的 a 元素。这些元素不会在它们自己之前或之后生成“break”，因此它们可以出现在另一个元素的内容中，而不会中断它的显示。

请注意，虽然“块”和“内联”的名称与 HTML 中的块级和内联级元素有很多相同之处，但它们之间有一个重要的区别。在 HTML 中，块级元素不能从内联级元素派生。在 CSS 中，对于显示角色之间如何嵌套没有限制。为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

为了了解它是如何工作的，让我们考虑一个 CSS 属性 display。

//

你可能已经注意到了这里有许多取值，只有其中三个是我提到过的：`block`、`inline`和`list-item`。这些取值的大部分会在本书其他部分介绍；例如`grid`和`inline-grid`涵盖在介绍栅格布局的独立的一章，跟表格相关的值都包含在介绍 CSS 表格布局的章节中。

现在我们把注意力放在`block`和`inline`上，看下面的代码：

```html
<body>
  <p>This is a paragraph with <em>an inline element</em> within it.</p>
</body>
```

这里有两个块级元素（`body`和`p`）和一个行内元素（`em`）。根据 HTML 规范，`em`可以作为`p`的后代，但反过来则不行。通常 HTML 的层级结构允许行内元素作为块级元素的后代，而不是相反。

CSS 则没有这样的限制，你可以保持现有的标签结构，然后修改这两个元素的显示角色：

```css
p {
  display: inline;
}
em {
  display: block;
}
```

这使得元素在一个行内框里面生成了一个块级框，这在 CSS 中是完全合法的，不会破坏任何规范。但是，如果你想在 HTML 中使用相反的嵌套结构，那就有会问题了，像这样：

```html
<em><p>This is a paragraph improperly enclosed by an inline element.</p></em>
```

不管你如何使用 CSS 来修改它们的显示角色，这在 HTML 中都是不合法的。

修改元素的显示角色在 HTML 文档中很有用，它对 XML 文档也至关重要。XML 文档一般没有默认的显示角色，而完全依赖文档开发者去定义它们。例如，如果你想要展示下面的 XML 片段：

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

因为`display`属性的默认值是`inline`，所以这块内容会默认被显示为行内文本，就像图 2 所示的那样。这样的排版不太有用。

<Figures figure="1-2">Default display of an XML document</Figures>

你可以用`display`来定义文档的基本板式：

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

这样把 7 种元素中的 5 个设置成块级元素，2 个设置成行内元素。块级元素会被像 HTML 中的`div`那样处理，两个行内元素会被类似`span`那样处理。

因为这种设置显示角色的基本能力，CSS 在各种场景下都非常有用。你可以从上面的规则开始，添加一些更具视觉效果的样式，然后得到像图 3 这样的显示效果。

<Figures figure="1-3">Styled display of an XML document</Figures>

在详细学习如何编写 CSS 之前，我们先要看一下如何关联 CSS 和文档，毕竟，如果不把它们结合在一起，CSS 是无法对文档起作用的。我们从最熟悉的 HTML 设置开始。

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