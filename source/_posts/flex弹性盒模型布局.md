---
title: flex弹性盒模型布局
copyright: true
date: 2020-09-24 21:53:57
toc: true
tags: [前端,CSS]
categories: [前端,CSS]
---
##  一、设置在容器上6个属性:

<!-- more -->

### 默认属性下主轴沿着x轴从左向右

### 侧轴(交叉轴)默认情况下和y轴方向相同由上至下

### 不用设inline-block了，默认沿主轴进行排列

### 1.flex-direction: 决定主轴的方向

属性决定主轴的方向,即项目的排列方向
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。

```css
.item:nth-of-type(1) {
	order: 0;
	margin-top: 10px;
}
.item:nth-of-type(2) {
	order: -1;
}
.item:nth-of-type(3) {
	order: 1;
}
.wrapper {
	flex-direction: row-reverse;
	// flex-direction: column
	// flex-direction: column-reverse;
}
```

### 2.flex-wrap: 是否换行

注意：当设置flex-grow属性的时候wrap失效，flex-basis尽可能按basis值往大了去从而达到折行的目的， flex-shrink会失效 (根据子元素实际的宽度判断是否折行)

```css
默认情况下(flex-shrink:1)，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
（1）nowrap（默认）：不换行。
（2）wrap：换行，第一行在上方。
（3）wrap-reverse：换行，第一行在下方。
```

### 3.flex-flow: flex-direction和flex-wrap的简写

flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

```css
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
```

### 4.justify-content: 项目在主轴上的对齐方式

justify-content属性定义了项目在主轴上的对齐方式。

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

```css
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

### 5.align-items : 项目在侧轴上如何对齐

align-items属性定义项目在侧轴(交叉轴)上如何对齐。

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

如果同时设置了align-items 和 align-self ,则 align-self 把 align-items覆盖

```css
.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
```

### 6.align-content: 多根轴线的对齐方式

align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
(类似于在侧轴上，每个主轴为一个项目);

该属性可能取6个值。
flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。

```css
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```



## 二、设置在项目（子元素）上6个属性:

### flex为复合属性，且必须配合父元素display:flex使用。

### 默认属性下主轴沿着x轴从左向右

### 侧轴(交叉轴)默认情况下和y轴方向相同由上至下

### 不用设inline-block了，默认沿主轴进行排列

### 1.flex-grow:  放大比例

根据所设置的比例分配盒子所剩余空间

```css
.wrapper {
	display: flex;
	width: 500px;
	height: 500px;
	border: 1px solid #000;
	font-size: 0px;
 }
 .item {
	width: 50px; //剩余空间500 - 50 * 3 = 350px,350px 进行 1 : 1 : 1分配
	text-align: center;
	height: 30px;
	line-height: 30px;
	border: 1px solid #000;
	box-sizing: border-box;
	font-size: 20px;
	flex-grow: 1;
 }

 .item:nth-of-type(1) {
	flex-grow: 1; //350*1/5 + 50 = 120px
 }
 .item:nth-of-type(2) {
	flex-grow: 2; //350*2/5 + 50 = 190px
 }
 .item:nth-of-type(3) {
	flex-grow: 2; // 350*2/5 + 50 = 190px
 }
 // 意思剩余空间分成 1+2+3份;
```

### 2.flex-shrink: 缩小比例

子元素的收缩比例— 多出盒子的部分，按照比例的大小砍掉相应的大小，即比例越大，被砍的越大，默认值1

```css
.wrapper {
	display: flex;
	width: 500px;
	height: 500px;
	border: 1px solid #000;
	font-size: 0px;
 }
 .item {
	width: 200px;//超出600-500 = 100px, 每个砍100/3 = 33.33px;
	text-align: center;
	height: 30px;
	line-height: 30px;
	border: 1px solid #000;
	box-sizing: border-box;
	font-size: 20px;
	//默认flex-shrink:1;
 }
```

### 3.flex-basis: 伸缩基准值

项目占据主轴的空间
该属性设置元素的宽度或高度，当然width也可以用来设置元素宽度，如果元素上同时出现了width 和flex-basis那么flex-basis会覆盖width的值
子元素宽度尽可能按照basis来如果基准值相加大于容器宽度那么 下面由下面公式分配宽度给子元素
flex-basis / (所有项目的flex-basis相加) * 容器的宽度
单位："auto"、"inherit" 或一个后跟 "%"、"px"、"em" 或任何其他长度单位的数字。

```css
 .item {
	flex-basis:50px;//主轴默认x轴方向,把width覆盖掉。如果主轴沿y轴,则覆盖height;
	width: 200px;
	text-align: center;
	height: 30px;
	line-height: 30px;
	border: 1px solid #000;
	box-sizing: border-box;
	font-size: 20px;
	//默认flex-shrink:1;
 }
```

### 4.flex

常用简化写法:

```css
flex:1 —>  flex:1 1 0%; // grow shrink flex-basis
flex:3 —> flex:3 1 0%;  // grow shrink flex-basis
```

注意:flexbox布局和原来的布局是两个概念，部分css属性在flexbox盒子里面不起作用，eg：float， clear， column,vertical-align 等等

```css
son1 = flex-shrink * flex-basis；
son2 = flex-shrink * flex-basis；
…..
sonN = flex-shrink * flex-basis；
加权值 = son1 + son2 + …. + sonN；
子元素压缩的宽度 w = (子元素flex-basis值 * flex-shrink / 加权值) * 溢出值
缩减值1：(flex-basis1 * 1/ 加权值) * 溢出值
缩减值2：(flex-basis2 * 2/ 加权值) * 溢出值
缩减值3：(flex-basis3 * 3/ 加权值) * 溢出值
最后son1、son2、son3，.., son n的实际宽度为：
flex-basis – 缩减值  = son 的真实宽度；
```

### 5.order

number定义项目的排列顺序。数值越小，排列越靠前，默认为0,可以为负值。

```css
.demo {
  order: number;
}
.item:nth-of-type(1) {
	order: 0;
}
.item:nth-of-type(2) {
	order: -1;
}
.item:nth-of-type(3) {
	order: 1;
}
```

### 6.align-self

align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```css
.demo{
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
.item {
		align-self: baseline;//所有第一行文字底线对齐
		// 如果容器里没有文字,则容器底边和第一行文字底线对齐
}
.item:nth-of-type(1) {
	order: 0;
	margin-top: 10px;
}
.item:nth-of-type(2) {
	order: -1;
}
.item:nth-of-type(3) {
	order: 1;
}
.item {
	// 如果没设高
	align-self:stretch默认为父级高度
}
```

---


