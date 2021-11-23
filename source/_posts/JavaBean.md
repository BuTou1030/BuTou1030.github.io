---
title: JavaBean
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaBean

<!-- more -->

## 一.概述

JavaBean是Java语言编写类的标准规范。符合JavaBean标准的类，必须是具体的公共的，并且具有无参数的构造方法，提供用来操作成员变量的set和get方法

## 二.Java中封装的概念

将一系列相关事物共同的属性和行为提取出来，放到一个类中，隐藏对象的属性和实现细节，仅对外提供公共的访问方式

## 三.封装的关键

绝对不能让类中的方法直接访问其他类的数据（属性），程序仅通过对象的方法与对象的数据进行交互

## 四.定义一个标准的JavaBean类

```java
public class Student {
    //成员变量，全部用private修饰.
    //姓名
    private String name;
    //年龄
	private int age;
    
    //构造方法，无参构造，全参构造
    public Student() {}
    
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    //公共的访问方式：getXxx(), setXxx()
    //设置姓名
    public void setName(String name) {
        this.name = name;
    }
    
    //获取姓名
	public String getName() {
        return name;
    }
    
    //设置年龄
    public void setAge(int age) {
        this.age = age;
    }
    
    //获取年龄
    public int getAge() {
		return age;
    }
}
```

