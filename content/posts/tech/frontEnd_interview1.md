---
title: "前端知识点CSS"
date: 2023-03-17T14:10:33+08:00
author: ["yjlintp"]
tags:
- 前端
# summary->在列表页展现的摘要内容，自动生成，内容默认前70个字符，可通过此参数自定义，一般无需专门设置
summary: "准备百度面试"
# description->需要自己编写的文章描述，是搜索引擎呈现在搜索结果链接下方的网页简介，建议设置
description: "不会"
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true # 顶部显示当前路径
---

<h1>css</h1>
<h2>三种布局</h3>
<h3>盒模型</h3> 

传统的布局解决方式。在 CSS 中广泛地使用两种“盒子” —— 块级盒子 (block box) 和 内联盒子 (inline box)。这两种盒子会在**页面流**（page flow）和元素之间的关系方面表现出不同的行为。完整的 CSS 盒模型应用于块级盒子，内联盒子只使用盒模型中定义的部分内容。模型定义了盒的每个部分 —— `margin, border, padding, and content` —— 合在一起就可以创建我们在页面上看到的内容。盒子的实际宽度=`content + border + padding`

**外边距**是盒子周围一圈看不到的空间。它会把其他元素从盒子旁边推开。外边距属性值可以为正也**可以为负**。设置负值会导致和其他内容重叠。理解外边距的一个关键是外边距折叠的概念。如果你有两个外边距相接的元素，这些外边距将合并为一个外边距，即最大的单个外边距的大小。

对**内联盒子**应用宽度、高度、边距、边框和内边距。宽度和高度不会起作用。外边距(横向)、内边距和边框是生效的，但盒子的内联性质不会改变，因此内边距和边框会与段落中的其他单词重叠。如果对display属性设置值inline-block，则既可以实现inline的不换行，同时width/height又可以发挥作用。

<p>
    I am a paragraph and this is a <span 
    style='  margin: 50px;
    padding: 20px;
    width: 100px;
    height: 0px;
    background-color: lightblue;
    border: 2px solid blue;'>
  span</span> inside that paragraph. A span is an inline element and so does not respect width and height.
</p>



    span{
        margin: 50px;
        padding: 10px;
        width: 100px;
        height: 0px;
        background-color: lightblue;
        border: 2px solid blue;
    }


#### 定位规则
- 普通流：按照次序依次定位每个盒子
- 浮动：将盒子从普通流中单独拎出来，将其放到外层盒子的某一边
- 绝对定位：按照绝对位置来定位盒子，其位置根据盒子的包含元素所建立的绝对坐标系来计算，因此绝对定位元素有可能会覆盖其他元素

**普通流**

依次排列。块盒子在垂直方向依次排列；行内盒子水平依次排列

当css的`position`属性为`static`或`relative`，并且无float属性值时为普通流布局。

**浮动**

在浮动定位中，浮动盒子会浮动到当前行的**开始或尾部**位置。这会导致普通流中的文本及其他内容会“流”到浮动盒子的边缘处，除非元素通过 `clear `清除了周围的浮动。行盒子会伸缩以适应浮动盒子的大小。

>`clear` 属性可设置以下值之一：
>
>- `none` - 允许两侧都有浮动元素。默认值
>- `left` - 左侧不允许浮动元素
>- `right`- 右侧不允许浮动元素
>- `both` - 左侧或右侧均不允许浮动元素
>- `inherit` - 元素继承其父级的 clear 值

**绝对定位**

在绝对定位中，盒子会完全从**当前流中移除**，并且不会再与其有任何联系（此处仅指定位和位置计算，而绝对定位的元素在文档树中仍然与其他元素有父子或兄弟等关系），其位置会使用 top、bottom、left 和 right 相对其包含块进行计算。

如果元素的 `position` 为 `absolute` 或 `fixed`，该元素为绝对定位。

对`position: fixed`的元素来说，该元素相对视口进行绝对定位，因此滚动时元素的位置并不会改变。

综上，盒模型依赖`display` + `position` + `float`这三个属性值来定位。

<h3>flex布局</h3> 
flexbox是一种一维的布局模型，它给 flexbox 的子元素之间提供了强大的空间分布和对齐能力。

#### flexbox的两根轴线

flex布局中有两根轴线：主轴和交叉轴。主轴由 `flex-direction` 定义，另一根轴垂直于它。

**主轴**

`flex-direction` 可以取 4 个值：

- row(初始值)
- row-reverse
- column
- column-reverse

主轴，也就是排列的方向。当选值为`row`，主轴将沿横向(inline)延伸，当选值为`column`，主轴将沿纵向(block)延伸。交叉轴则相反。

注意flexbox方向与书写方向(左右顺序)无关。`reverse`改变的是子元素的排列顺序（或者说改变的是起始线和终止线的位置）。

`display`值为`flex`的区域就叫flex容器，容器中的**直系子元素**会变为flex元素。如果容器中一些元素比其他元素高，那么元素会沿交叉轴被拉伸来填满它的大小。

#### 多行flex容器

虽然flexbox是一维模型，但设置`flex-wrap: wrap`flex布局可以应用到多行，这时候把每一行可以看作一个新的flex容器。任何空间分布都将在该行上发生，而**不影响该空间分布的其他行**。

现在，如果子元素无法全部显示在一行中，则会换行显示。若将`display`其设置为`nowrap`(初始值)，子元素将会缩小以适应容器(这取决于其他属性的值，初始值会缩小)，若不然，使用nowrap会导致溢出。

#### flex元素的控制属性

- `flex-basis`
- `flex-shrink`
- `flex-grow`

用以实现flex元素自动填充剩余空间。

**flex-basis:** 默认值为auto，此时按照设置的元素尺寸或自动按照元素内容的尺寸。如果设置值，为主轴的假定尺寸（会覆盖width/height，但会受到min-width/max-width等值的影响）

**flex-grow:** 若被设置为正整数，flex 元素会以 `flex-basis` 为基础，沿主轴方向增长尺寸，并占据此方向轴上的可用空间。若有多个元素进行延展，会按照`flex-grow`的值分配权重。

**flex-shrink:** 若设置为正整数，则是用于控制 flex 元素收缩的程度，伸缩权重是`flex-shrink` × `flex-basis`。

可以用flex属性进行简写。

- `flex: initial` 是把 flex 元素重置为初始值，它相当于 flex: 0 1 auto。`flex-grow` 的值为 0，所以 flex 元素不会超过它们 flex-basis 的尺寸。`flex-shrink` 的值为 1, 所以可以缩小 flex 元素来防止它们溢出。`flex-basis` 的值为 auto. Flex 元素尺寸可以是在主维度上设置的，也可以是根据内容自动得到的。
- `flex: auto`等同于`flex: 1 1 auto`
- `flex: none`等同于`flex: 0 0 auto`
- `flex: 2` 等同于 `flex: 2 1 0` 设置flex-basis为0，完全按flex-grow来占用剩余空间，若另外的元素尺寸就已经超过容器尺寸，会占据最小大小。

#### 对齐和空间分配

flexbox 的一个关键特性是能够设置 flex 元素沿两根轴线对齐方式，以及它们之间的空间分配。

**align-items:** 使元素在交叉轴方向对齐，默认值stretch使flex元素默认被拉到最高来填满容器。

取值：
- `stretch`
- `flex-start`: 按容器顶部对齐
- `flex-end`: 按容器下部对齐
- `center`: 居中对齐


    <div style="border: 1.5px dotted gray;display:flex;align-items: center;padding: 20px">
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px">One</div>
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px">Two</div>
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px">Three
    <br/>has
    <br/>extra
    <br/>text
          </div>
    </div>
      
**justify-content:** 使元素在主轴方向上对齐,初始值是flex-start，元素从容器的起始线排列。

- `stretch`
- `flex-start`: 从起始线开始排列
- `flex-end`: 从终止线开始排列
- `center`: 居中对齐
- `space-around`: 剩余空间在主轴方向环绕所有子元素均分
- `space-between`: 剩余空间在主轴方向所有子元素之间均分

如果设置了flex-grow，`space-around`、`space-between`不会起效


<div style="border: 1.5px dotted gray;display: flex;justify-content:space-around;">
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px;">One</div>
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px">Two</div>
    <div style="border: 2px solid rgb(0.6,0.6,0.6);border-radius: 5px">Three
    <br/>has
    <br/>extra
    <br/>text
          </div>
    </div>  

<h3>Grid布局</h3>
