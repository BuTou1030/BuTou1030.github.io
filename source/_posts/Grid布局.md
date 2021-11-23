---
title: Grid布局
copyright: true
date: 2020-09-25 14:28:38
toc: true
tags: [前端,CSS]
categories: [前端,CSS]
---
## 一、设置在容器上的属性:

<!-- more -->

### 两条水平线之间的区域叫做行轨道

### 两条垂直线之间的区域叫做列轨道

### 有水平方向上的横轴和垂直方向上的块轴

### 开启grid布局,只需给容器加上以下代码

### 注意，设为网格布局以后，容器子元素（项目）的`float`、`display: inline-block`、`display: table-cell`、`vertical-align`和`column-*`等设置都将失效。

```css
.grid {
    display: grid;
}
/* 默认情况下，容器元素都是块级元素，但也可以设成行内元素。*/
.grid {
    display: inline-grid;
}
```

### 1.grid-template-columns: 指定每列宽度

```html
<div class="grid">
	<div class="column1">column1</div>
	<div class="column2">column2</div>
	<div class="column3">column3</div>
	<div class="column4">column4</div>
	<div class="column5">column5</div>
	<div class="column6">column6</div>
</div>
```

```css
.grid {
	display: grid;
    grid-template-columns: 100px 100px 100px; 固定宽度
    /*                      1fr   1fr   1fr  浮动宽度 1:1:1分配剩余空间
                            1fr   2fr   1fr  浮动宽度 1:2:1分配剩余空间
                            33.33% 33.33% 33.33% 百分比分配剩余空间
                             repeat(3, 33,33%) 第一个参数是重复次数，第二个参数是重复的值
        若有6列，可以grid-template-columns: repeat(2, 100px 20px 80px); 重复模式
        1,4列为100px, 2,5列为20px,3,6列为80px  */
}
/* 有时，单元格的大小是固定的，但是容器的大小不确定。如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用auto-fill关键字表示自动填充。*/
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
/* minmax()函数产生一个长度范围，表示长度就在这个范围之中。它接受两个参数，分别为最小值和最大值。*/
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr minmax(100px, 1fr);
  /* 上面代码中，minmax(100px, 1fr)表示列宽不小于100px，不大于1fr。*/
}
/* auto关键字表示由浏览器自己决定长度。*/
.grid {
	display: grid;
    grid-template-columns: 100px auto 100px;
    /* 上面代码中，第二列的宽度，基本上等于该列单元格的最大宽度，除非单元格内容设置了min-width，且这个值大于最大宽度。*/
}
/* 网格线的名称 */
.grid {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
  /* 上面代码指定网格布局为3行 x 3列，因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字。 */
}
```

### 2.column-gap: 列间距

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    column-gap: 24px;
}
```

### 3.row-gap: 行间距

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    row-gap: 24px;
}
```

### 4.gap: column-gap 和 row-gap 的简写

```css
.grid {
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    gap: 24px;
}
```

### 5.grid-template-areas: 排列元素

搭配在项目上的属性 grid-area使用

```html
<div class="layout">
	<header>头部</header>
	<aside>侧边栏</aside>
	<main>内容</main>
	<footer>底部</footer>
</div>
```

```css
.grid {
    display: grid;
    grid-template-areas:
        "header header header"
        "sidebar content content"
        "footer footer footer";
    // 如果某些区域不需要利用，则使用"点"（.）表示。
}
header {
    grid-area: header;
}
main {
    grid-area: content;
}
aside {
    grid-area: sidebar;
}
footer {
    grid-area: footer;
}
```

### 6.align-items: 垂直方向上对齐子元素

```css
.grid {
    align-items: start|end|center|stretch;
}
```

### 7.justify-items: 水平方向上对齐子元素

```css
.grid {
    justify-items: start|end|center|stretch|space-between;
}
```

### 8.place-items: `align-items`属性和`justify-items`属性的合并简写形式

```css
.grid {
    place-items: start end;
}
```

### 9.align-content: 整个内容区域的垂直位置

```css
.grid {
    align-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
```

### 10.justify-content: 整个内容区域在容器里面的水平位置

```css
.grid {
    justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
}
 /* stretch - 项目大小没有指定时，拉伸占据整个网格容器。
 space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
 space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
 space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。*/
```

### 11.grid-auto-flow

划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行。

这个顺序由`grid-auto-flow`属性决定，默认值是`row`，即"先行后列"。也可以将它设成`column`，变成"先列后行"。

```css
.grid{
    grid-auto-flow: column;
}
```

`grid-auto-flow`属性除了设置成`row`和`column`，还可以设成`row dense`和`column dense`。这两个值主要用于，某些项目指定位置以后，剩下的项目怎么自动放置。

`row dense`，表示"先行后列"，并且尽可能紧密填满，尽量不出现空格。

`column dense`，表示"先列后行"，并且尽量填满空格。

### 12. grid-auto-columns, grid-auto-rows

有时候，一些项目的指定位置，在现有网格的外部。比如网格只有3行 x 3列，但是某一个项目指定在第5行。这时，浏览器会自动生成多余的网格，以便放置项目。

`grid-auto-columns`属性和`grid-auto-rows`属性用来设置，浏览器自动创建的多余网格的列宽和行高。它们的写法与`grid-template-columns`和`grid-template-rows`完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px;
}
```

### 13.grid-template, grid

`grid-template`属性是`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

`grid`属性是`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。

## 二、设置在项目上的属性

### 1. grid-column-start ， grid-column-end ， grid-row-start ， grid-row-end

项目的位置是可以指定的，具体方法就是指定项目的四个边框，分别定位在哪根网格线。

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
}
/*grid-column-start属性：左边框所在的垂直网格线
// grid-column-end属性：右边框所在的垂直网格线
// grid-row-start属性：上边框所在的水平网格线
// grid-row-end属性：下边框所在的水平网格线
// 上面代码指定，1号项目的左边框是第二根垂直网格线，右边框是第四根垂直网格线。
// 这四个属性的值，除了指定为第几个网格线，还可以指定为网格线的名字。
// 这四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格。*/
.item-1 {
  grid-column-start: span 2;
}
```

只指定了1号项目的左右边框，没有指定上下边框，所以会采用默认位置，即上边框是第一根水平网格线，下边框是第二根水平网格线。除了1号项目以外，其他项目都没有指定位置，由浏览器自动布局，这时它们的位置由容器的`grid-auto-flow`属性决定，这个属性的默认值是`row`，因此会"先行后列"进行排列。

### 2.grid-column,grid-row

`grid-column`属性是`grid-column-start`和`grid-column-end`的合并简写形式，`grid-row`属性是`grid-row-start`属性和`grid-row-end`的合并简写形式。

```css
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
.item-1 {
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
/* 等同于 */
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 3;
}
/* 等同于 */
.item-1 {
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
}
```

### 3.grid-area

`grid-area`属性指定项目放在哪一个区域。

```css
.item-1 {
  grid-area: content;
}
```

`grid-area`属性还可用作`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end`的合并简写形式，直接指定项目的位置。

```css
.item-1 {
  grid-area: 1 / 1 / 3 / 3;
}
```

### 4. justify-self, align-self ,place-self

`justify-self`属性设置单元格内容的水平位置（左中右），跟`justify-items`属性的用法完全一致，但只作用于单个项目。

`align-self`属性设置单元格内容的垂直位置（上中下），跟`align-items`属性的用法完全一致，也是只作用于单个项目。

```css
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
/* start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。*/
```

#### 5.place-self

place-self属性是align-self属性和justify-self属性的合并简写形式。

```css
.item {
    place-self: center center;
    /* 如果省略第二个值，place-self属性会认为这两个值相等。*/
}
```
---
参考链接[CSS Grid 网格布局教程](http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html) , by 阮一峰

