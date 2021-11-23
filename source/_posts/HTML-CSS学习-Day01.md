---
title: HTML+CSS学习 Day01
copyright: true
date: 2020-09-22 17:06:43
toc: true
tags: [前端,HTML]
categories: [前端,HTML]
---
## 一、浏览器及其内核
<!-- more -->

| Shell         | 内核         |
| ------------- | ------------ |
| IE            | trident      |
| Google chrome | webkit/blink |
| Safari        | webkit       |
| Firefox       | Gecko        |
| Opera         | presto       |

## 二、标签

### 1.基本结构构成标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>

</body>
</html>
```

### 2.独立成行

```html
<p>独立成行的内容</p>
```

### 3.回车

```html
<br>
```

### 4.空格

```html
&nbsp
```

### 5.输入关键词''<>''的方法

```html
&lt;divgt&; <!-- 输出 <div> -->
```

### 6.标题

```html
 <h1>一级标题</h1>
 <h2>二级标题</h2>
 <h3>三级标题</h3>
 <h4>四级标题</h4>
 <h5>五级标题</h5>
 <h6>六级标题</h6>
```

### 7.加粗和斜体

```html
<strong>加粗字体</strong>
<em>斜体字体</em>
```

### 8.划一杠

```html
<del>被划一杠</del>
```

### 9.地址

```html
<adress>北京市朝阳区xxx</adress>
```

### 10.容器

```html
<div></div>
<span></span>
```

### 11.里外结构(order list,unorder list)

```html
<ol type="A" reversed="reversed" start="3">
 <!-- start代表从哪开始,reversed代表倒序. -->
 <!-- type默认为1(阿拉伯数字),还有a,A,I,i(罗马数字) -->
    <li></li>
    <li></li>
    <li></li>
</ol>
<ul type="disc">
<!-- disc:discircle实心圆,除此之外还有circle圈 -->
	<li></li>
	<li></li>
	<li></li>
</ul>
```
### 12.anchor(锚)标签

```html
<a href="http://www.baidu.com">www.baidu.com</a>
<!-- 用途: (1)超链接 (2)锚点 (3)电话/邮件 tel:xxx-xxx-xxx/mailto:xxx@xxx.xxx (4) 协议限定符 javascript:代码 -->
```
### 13.form表单

```html
<form method="get/post"action="">
	username:<input type="text" name="username">
	password: <input type="password" name="password">
	<input type="submit" value="">
	 这是一道题目:
     选项1:<input type="radio/checkbox" name="problem" value="f1" checked="checked">
     选项2:<input type="radio/checkbox" name="problem" value="f2">
     <input type="submit" value="">
     保存密码多久：
     <select name="savetime">
	       <option value="7days">7天</option>
	       <option value="1month">1个月</option>
	  </select>
</form>
<!-- (发送方式)method="get/post"(发送给谁)action="" -->
<!-- value默认值为"提交"可以改为"登入""Login"等 发送数据要有数据名name 数据值 value -->
<!-- <input type=(单选/多选)"radio/checkbox" name="problem" value="f1" (帮用户提前选好)checked="checked"> -->
```
---
