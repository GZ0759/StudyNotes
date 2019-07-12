> Bootstrap实战  
> 2015年 5 月第 1 版  
> 著 [美] David Cochran [美] Ian Whitley  
> 译 李松峰

# 第一章 初识Bootstrap

## 1.1 数量和质量

Bootstrap v2.0 发布之后，响应式设计随之成为主流，其界面元素也做到了跨设备响应（包括桌面、平板和手机）。
现在， Bootstrap v3.0 也发布了，其功能愈加完善，包括：
- 移动优先的响应式网格；
- 基于 Web 字体的图标，适用于移动及高密度屏幕；
- 不再支持 IE7，标记和样式更加简洁高效

从单纯给标记添加类深入到自定义 Bootstrap 的 LESS 文件，大幅提高了我们的工作效率和控制力。在 Bootstrap 默认的样式表基础之上，开发人员可以发挥自己的创造力，定制出自己的核心内容。

## 1.2 下载Bootstrap

下载到的文件中的实际内容可能会随着时间推移而有所变化，但主要内容通常不会变。比如，在 less 文件夹中，可以找到所有重要的 LESS 文件，它们是本书所有项目的基础。另外， js 文件夹中包含的是 Bootstrap 的插件，可供我们选择使用。
假如你只需要 Bootstrap 默认提供的预编译的 CSS 或 JavaScript 文件（bootstrap.css 或 bootstrap.min.js），也可以在 dist 文件夹中找到它们。

## 1.3 准备项目模板文件夹

在浏览器中打开 h5bp.com。这是一个短链接，服务器解析后会重定向到 H5BP 的主文档
页面。可以在这个页面直接下载 H5BP，也可以单击 SOURCE CODE 链接，在 GitHub 上
下载。

## 1.4 加入Bootstrap文件

从 Bootstrap 的主文件夹中，把 fonts 文件夹复制粘贴到 Project Template 1 文件夹中。这个文件夹里包含着 Bootstrap 附带的重要的 Glyphicon 字体。

保险起见，建议大家再在这个文件夹里放一个跨域友好的.htaccess 文件。为什么？因为随
着越来越多的 CDN（ Content Delivery Network，内容分发网络）为你的网站缓存静态资源，你会发现如果没有这个文件，某些浏览器会拒绝识别你的 Web 字体。

Bootstrap 的插件都基于 jQuery，而 H5BP 已经为我们准备好了。除了 jQuery，我们还看到了 Modernizr 脚本。简单介绍一下， Modernizr 包含的是 HTML5“垫片”（ shiv）脚本，可以让 IE8 支持 HTML5 的分区（ section）元素。因为我们这个项目打算支持 IE8，所以也用得着它。除此之外， Modernizr 还可以让我们更方便地检测特定浏览器的能力，比如 CSS 3D 变换。

## 1.5 大盘点

由于采用了模块化的开发方式， Bootstrap 的 less 文件夹中包含很多文件。

## 1.6 构造HTML模板

 HTML5 文档类型声明：
 ```html
<!DOCTYPE html>
```

针对 IE 的条件注释，开发者通过嵌套的选择符可以加入对旧版本浏览器的修复代码：
```html
<!--[if lt IE 7]><html class="no-js lt-ie9 lt-ie8 lt-ie7"><![endif]-->
<!--[if IE 7]><html class="no-js lt-ie9 lt-ie8"><![endif]-->
<!--[if IE 8]><html class="no-js lt-ie9"><![endif]-->
<!--[if gt IE 8]><!--><html class="no-js"><!--<![endif]-->
```

html 标签也包含一个 no-js 类。如果浏览器的 JavaScript 可用， Modernizr 脚本会把这个类删除，并将其替换成 js 类。如果这个类没有被删除，则表明 JavaScript 不可用，我们就需要使用嵌套的选择符为这种情况写一些 CSS 规则。

接下来是几个 meta 标签。
```html
<!-- 用于指定字符集的： -->
<meta charset="utf-8">

<!-- 告诉 IE 使用最新版的渲染引擎，或者如果安装了的话，使用谷歌的 Chrome Frame： -->
<meta http-equiv="X-UA-Compatible"
content="IE=edge,chrome=1">

<!-- 预留给描述站点用的： -->
<meta name="description" content="">

<!-- 针对移动浏览器的视口标签： -->
<meta name="viewport" content="width=device-width">
```

## 1.7 设定站点标题

可以随便给自己的作品起名字，比如Bootstrappin’ Portfolio。为准确起见，这里使用HTML实体&#39来表示单引号，结果如下所示：
```html
<title>Bootstrappin&#39; Portfolio</title>
```

HTML5 后来又增加了`<main role="main"></main>`元素，目的是专门为页面或分区中的主内容提供一个专用的元素。

## 1.8 导航条

- 添加了 navbar-static-top 类，因为我们希望导航条能够定位到窗口顶部，但能够
随页面滚动而滚动；
- 把项目名称链接到 index.html；
- 把原来的父 div 标签改成了语义化的 HTML5 nav 标签。
```html
<header role="banner">
  <nav role="navigation" class="navbar navbar-static-top navbar-default">
    <div class="container">
      <div class="navbar-header">
        <a class="navbar-brand" href="index.html">Project name</a>
      </div>
      <ul class="nav navbar-nav">
        <li class="active"><a href="index.html">Home</a></li>
        <li><a href="#">Link</a></li>
        <li><a href="#">Link</a></li>
      </ul>
    </div>
  </nav>
</header>
```

## 1.9 编译和链接默认的Bootstrap CSS

完成响应式导航条。

搜索到`<div class="navbar-header">`，在这个元素中，添加一个 navbar-toggle
按钮，用于展开和收起响应式导航条。

```html
<div class="navbar-header">
  <button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse">
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
    <span class="icon-bar"></span>
  </button>
  <a class="navbar-brand" href="index.html">Project
  name</a>
</div>
```

- 按钮中的 navbar-toggle 类用于应用 CSS 样式；
- 后面的数据属性 data-toggle 和 data-target 是 Bootstrap 的 JavaScript 插件要用的，分别表示预期行为和预期目标（即 collapse 和类名为 navbar-collapse 的
元素，这个元素后面会添加）；
- 类名为 icon-bar 的 span 元素是 CSS 用来创建按钮中的三道杠按钮用的。

接下来把导航项包装在一个收起的 div 中，即用带有适当 Bootstrap 类的 div 把 ul
class="nav navbar-nav">包装起来。

```html
<div class="navbar-collapse collapse">
  <ul class="nav navbar-nav">
    <li class="active"><a href="index.html">Home</a></li>
    <li><a href="#">Link</a></li>
    <li><a href="#">Link</a></li>
  </ul>
</div><!--/.nav-collapse -->
```

要支持 IE8，需要一段 JavaScript 代码让浏览器能够响应媒体查询。这段代码就是 Scott Jehl 的 respond.js“腻子脚本”。

为了针对 IE8 应用这段脚本，需要针对 IE8 的条件注释：
```html
<!--[if lt IE 9]>
...
<![endif]-->
```

# 第二章 作品展示站点

## 2.1 设计目标

这个作品展示站点应该具有下列功能：
- 带 Logo 的可折叠的响应式导航条；
- 重点展示 4 张作品的图片传送带；
- 单栏布局中包含三块内容，每块内容中都包含标题、短段落和吸引人点击阅读的大
按钮；
- 页脚包含社交媒体链接

在这个针对大屏幕的设计效果图中，可以发现下列功能：
- 位于顶部的导航条，而且各导航项都附带图标；
- 宽屏版的图片传送带，其中的图片拉伸至与浏览器窗口同宽；
- 三栏布局分别容纳三块文本内容；
- 页脚在布局中水平居中。

## 2.2 查看练习文件

## 2.3 搭建传送带

可以按照示例中的结构设置其中的元素。以下代码就是传送带的所有标记，包含各个部
分，首先是进度指示器：
```html
<div id="homepage-feature" class="carousel slide">
  <ol class="carousel-indicators">
    <li data-target="#homepage-feature" data-slide-to="0"
    class="active"></li>
    <li data-target="#homepage-feature" data-slide-to="1"></li>
    <li data-target="#homepage-feature" data-slide-to="2"></li>
    <li data-target="#homepage-feature" data-slide-to="3"></li>
  </ol>
```
整个传送带是一个带 ID 属性（ id="homepage-feature"）的 div 标签，其 carousel
类用于把 Bootstrap 的传送带 CSS 应用到这个元素，为指示器、传送带项和前一张及后一张控件添加样式。
进度指示器的 data-target 属性必须使用传送带的 ID homepage-feature。有了这个
属性， JavaScript 插件才能为活动的传送带项添加 active 类。在此我们预先为第一个指示器添加了 active 类。然后，类的切换就由 JavaScript 控制了。它会删除第一个指示器的这个类，再添加到后续指示器，如此循环。

指示器后面，是类为 carousel-inner 的元素。这个元素是所有传送带项（ item），也就
是所有图片。carousel-inner 元素内部是传送带项，是一组 div 标签， 每个都带着 class="item"。把第一项修改成包含 item 和 active 两个类，使其一开始就可见。
```html
<!-- Wrapper for slides -->
<div class="carousel-inner">
  <div class="item active">
    <img src="img/okwu-athletics.jpg" alt="OKWU Athletics Homepage">
  </div>
  <div class="item">
    <img src="img/okwu.jpg" alt="OKWU.edu Homepage">
  </div>
  <div class="item">
    <img src="img/bso.jpg" alt="Bartlesville Symphony Homepage">
  </div>
  <div class="item">
    <img src="img/alittlecode.jpg" alt="aLittleCode.com Homepage">
  </div>
</div><!-- /.carousel-inner -->
```
传送带项之后，还需要添加传送带控件，用于在传送带左、右两侧显示前一个和后一个
按钮。你会发现其中有类对应着 Glyphicon 字体图标。在控件后面，我们再用一个结束
div 标签关闭整个传送带。
```html
<!-- Controls -->
<a class="left carousel-control" href="#homepage-feature" data-slide="prev">
<span class="glyphicon glyphicon-chevron-left"></span>
</a>
<a class="right carousel-control" href="#homepage-feature" data-slide="next">
<span class="glyphicon glyphicon-chevron-right"></span>
</a>
</div><!-- /#homepage-feature.carousel -->
```

默认情况下，传送带的幻灯片每 5 秒切换一次。为了充分展示我们的作品，可以改成 8 秒。这里先用 jQuery 方法检测相应的页面元素是否存在，如果存在则将传送带的间隔时间初始化为 8000 毫秒。
```html
$( document ).ready(function() {
  $('.carousel').carousel({
    interval: 8000
  });
});
```

## 2.4创建响应式分栏。

页面中有三块文本，每块都有标题、段落和链接。在大于等于平板电脑的屏幕上， 我们希望内容分三栏，而在较窄的屏幕上，我们希望内容变成一栏全宽。

简单地说， Bootstrap 内置 12 栏网格系统，其基本的类结构支持 col-12 表示全宽， col-6 表示半宽， col-4 表示三分之一宽，以此类推。

在 Bootstrap 3 中，由于创造性地使用了媒体查询，网格系统具有极强的适应力。如前所
述，我们希望欢迎消息在比平板小的屏幕中呈现为一栏全宽，而在大约 768px 时变成三
分之一栏宽。巧合的是， Bootstrap 内置的小屏幕断点恰好是 768px ， 也就是
@screen-sm-min 变量的默认值。而大于 768px 的中屏幕断点是 992px，对应变量是
@screen-md-min。然后，大于 1200px 断点的算大屏幕。这几个断点我们后面统称为小、
中、大断点。

小断点有一个特殊的栏类命名法： col-sm-。因为我们想在小断点之上使用三栏，所以
这里使用 class="col-sm-4"。这样在小断点之下，分块元素会保持全宽，而在小断点
之上，则会各占三分之一宽并肩排列。完整的结构如下所示，为简明起见，段落内容作
了省略处理：

```html
<div class="container">
  <div class="row">
    <div class="col-sm-4">
      <h2>Welcome!</h2>
      <p>Suspendisse et arcu felis ...</p>
      <p><a href="#">See our portfolio</a></p>
    </div>
    <div class="col-sm-4">
      <h2>Recent Updates</h2>
      <p>Suspendisse et arcu felis ...</p>
      <p><a href="#">See what's new!</a></p>
    </div>
    <div class="col-sm-4">
      <h2>Our Team</h2>
      <p>Suspendisse et arcu felis ...</p>
      <p><a href="#">Meet the team!</a></p>
    </div>
  </div><!-- /.row -->
</div><!-- /.container -->
```

- container 类用于约束内容的宽度，并使其在页面内居中；
- row 类用于包装三个栏，并为栏间留出左右外边距；
- container 类和 row 类都设定了清除，因而它们可以包含浮动元素，同时又清除之前
的浮动元素。

## 2.5 把链接变成按钮

把重要的内容链接转换成突出显示的按钮很简单。为此要用到如下几个关键的类：
- btn 类用于把链接变成按钮的样式；
- btn-primary 类用于把按钮变成主品牌颜色；
- pull-right 类用于把链接浮动到右侧，使其占据更大的空间，从而更便于发现和点击。

```html
<p>
  <a class="btn btn-primary pull-right" href="#">See our portfolio</a>
</p>
```

## 2.6 理解LESS

嵌套规则。嵌套规则极大提高了组合样式的效率。

相同的选择符用 LESS 写会简洁很多，只要使用一个简单的嵌套即可：
```less
.navbar-nav { ...
  > li { ...
    > a { ...
      &:hover,
      &:focus { ... }
    }
  }
}
```
编译后，这些规则会生成标准的 CSS。但 LESS 的嵌套规则更容易写，也更容易维护。

变量。使用变量可以让我们只设定（或修改）一次，就能自动影响（更新）整个样式表中用到该值的属性。
```less 
@off-white: #e5e5e5;
@brand-primary: #890000;

a {
  color: @brand-primary;
}
.navbar {
  background-color: @brand-primary;
  > li > a {
    color: @off-white;
  }
}
```

混入。混入可以让生成整套规则更方便也更容易管理。比如，可以利用它简化为元素应用
border-box 属性的任务。在 CSS 中，要涵盖所有浏览器，需要用到每种浏览器的供应
商前缀，为此针对每个元素都要写三行相同的声明，而且还要记住每一种前缀的写法。在 LESS 中，可以只写一个供混入的规则，后面则可以通过 @boxmodel 参数来指定期望
的盒模型。
```less
.box-sizing(@boxmodel) {
  -webkit-box-sizing: @boxmodel;
  -moz-box-sizing: @boxmodel;
  box-sizing: @boxmodel;
}
// 然后就可以在需要的地方使用这个混入了：
.box {
  .box-sizing(border-box);
}
.another-element {
  .box-sizing(border-box);
}
// 编译之后，还会为每个元素生成三行 CSS。
```

运算式。通过运算式可以基于变量实现数学计算。比如，可以将一种颜色作为基准，对其进行加亮和减暗处理：
```less
a:hover { darken(@link-color, 15%); }
```
还可以计算内边距的值，以适应导航条的高度。比如，以下 Bootstrap 的 navbar.less 文件中的代码，就将导航项的内边距值设定为导航条高度减去行高之后剩余的高度值。然后，把这个值一分为二，平均应用为顶部和底部内边距：
```less
.navbar > li > a {
  padding-top: ((@navbar-height - @line-height-computed) / 2);
  padding-bottom: ((@navbar-height - @line-height-computed) / 2);
}
```

导入文件。LESS 编译器支持导入并组合多个文件，最终生成一个统一的 CSS 文件。我们可以指定导入的次序，按照需要的层叠关系精确组织结果样式表。

Bootstrap 的导入文件 bootstrap.less 一开始导入了基本的变量和混入。然后，又导入了（代替 CSS 重置样式表的） normalize.css 的 LESS 版，之后是针对打印媒体的基本样式（ print.less）、基本的全局样式（ scaffolding.less）和排版样式（type.less）。结果这个 bootstrap.less 文件的开头几行就是这样的：
```less
// Core variables and mixins
@import "variables.less";
@import "mixins.less";

// Reset
@import "normalize.less";
@import "print.less";

// Core CSS
@import "scaffolding.less";
@import "type.less";
```

模块化。把多个文件导入并输出成一个文件，可以让我们更方便地组织样式，对它们进行分组，并在不同的文件中对它们进行维护。这也是 Bootstrap 会带有那么多 LESS 文件的原因，导航条有一个，按钮有一个，警告框有一个，传送带有一个……，而所有这些都会被导入到 bootstrap.less 文件。

## 根据需要定制 Bootstrap 的 LESS 文件

根据需要定制 Bootstrap 的 LESS 文件。在定制 Bootstrap 的 LESS 文件期间，我们会发挥很大的主观能动性，具体如下：
- 组织 less 文件夹，以便灵活、自由地实现我们需要，同时也让将来的维护者更方便；
- 自定义 Bootstrap 提供的几个 LESS 文件；
- 创建几个新的 LESS 文件；
- 为站点整合一套较大的字体图标，数量翻倍，并将图标运用于社交媒体链接。

什么文件名开头要使用两个下划线？事实上，原因有四。
- 按字母排序时，下划线可以让文件排在前头。
- 它不是我们唯一的自定义文件，如果其他自定义文件只使用一个下划线，那么它就显
得更突出。
- 采用这种命名方式，更便于我们扫描或搜索自定义文件。由于下划线比较显眼，所以
在搜索时，只输入一个下划线，就可以列出所有自定义文件。
- 同时打开多个文件编辑时，带下划线的文件名也容易让我们找到相应的标签页。

## 2.8 添加 Logo 图片

- 我们并没有动原始的 bootstrap/navbar.less 文件，因此如果需要可以随时恢复原状；
- 我们完全用自己的定制版替换了这个文件，只是__main.less 里面的注释为我们留下了
改动的痕迹；
- 我们还在_navbar.less 中注释掉一行代码，这样就可以知道修改了什么规则；
- 不过，由于我们使用的是 JavaScript 风格的单行注释，所有被注释掉的规则都不会被编译进最终的 CSS 文件。

## 2.9 调整导航项内边距

# 第三章 WordPress主题

以 Roots 主题作为 WordPress 主题的起点。本章介绍的流程适用于将任意 Bootstrap 设计转换为 WordPress 主题。

# 第四章 企业网站


# 第五章 电子商务网站


# 第六章 单页销售网站


# 附录A 优化站点资源


# 附录B 实现响应式图片


# 附录C 让传送带支持手势

