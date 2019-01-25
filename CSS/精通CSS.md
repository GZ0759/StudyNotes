> CSS Mastery: Advanced Web Standards Solutions, Third Edition
> [官方源码](https://github.com/Apress/css-mastery-16)


# 目录

- [第一章 奠定基础](#第一章-奠定基础)
- [第二章 让你的样式达到目标](#第二章-让你的样式达到目标)
- [第三章 可视化格式模型概述](#第三章-可视化格式模型概述)
- [第四章 Web印刷样式](#第四章-Web印刷样式)
- [第五章 完美盒模型](#第五章-完美盒模型)
- [第六章 内容布局](#第六章-内容布局)
  - [6.1 使用定位](#6.1-使用定位)
  - [6.2 水平布局](#6.2-水平布局)
  - [6.3 弹性布局](#6.3-弹性布局)
- [第七章 页面布局和网格](#第七章-页面布局和网格)
- [第八章 响应式Web设计和CSS](#第八章-响应式Web设计和CSS)
- [第九章 样式表和数据表](#第九章-样式表和数据表)
- [第十章 让它动起来：Transforms，Transitions和Animations](#第十章-让它动起来：Transforms，Transitions和Animations)
- [第十一章 前沿视觉效果](#第十一章-前沿视觉效果)
- [第十二章 代码质量和工作流](#第十二章-代码质量和工作流)

# 第一章 奠定基础

# 第二章 让你的样式达到目标

# 第三章 可视化格式模型概述

# 第四章 Web印刷样式

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

额外：用 CSS 创建三角形。

```css
.comment:after {
  position: absolute;
  content: '';
  display: block;
  width: 0;
  height: 0;
  border: .5em solid #dcf0ff;
  border-bottom-color: transparent;
  border-right-color: transparent;
  position: absolute;
  right: -1em;
  top: .5em;
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
  background-color: rgba(255,255,255,0.7);
  padding: 2em;
}
```

## 6.2 水平布局

## 6.3 弹性布局

# 第七章 页面布局和网格

# 第八章 响应式Web设计和CSS

# 第九章 样式表和数据表

# 第十章 让它动起来：Transforms，Transitions和Animations

# 第十一章 前沿视觉效果

# 第十二章 代码质量和工作流


