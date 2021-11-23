---
title: Java继承
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# Java继承

<!-- more -->

## 一.继承概述

让类与类之间产生父子关系

被继承的类叫做父类（基类，超类）

继承的类叫做子类（派生类)

格式(extends)

```java
class 父类 {    
}
class 子类 extends 父类 {
}
```



子类拥有了父类的非私有成员（成员变量，成员方法）

## 二.继承的优缺点

### 1.优点

功能复用：直接将已有的属性和行为继承过来，实现了功能的复用，节省了大量的工作

便于扩展新功能：在已有功能的基础上，更容易建立，扩充新功能

结构清晰，简化认识：同属于一个继承体系的相关类，他们之间结构层次清晰，简化了人们对代码结构的认识

易维护性：不同类之间的继承关系，让这些事物之间保持了一定程度的一致性，大大降低了维护成本

### 2.缺点

打破了封装性：父类向子类暴露的实现细节，打破了父类对象的封装性

高耦合性：类与类之间紧密的结合在一起，相互依赖性高

程序设计的追求

低耦合，高内聚

耦合：两个（或更多）模块相互依赖于对方

内聚：模块内部结构紧密，独立性强

## 三.继承关系中类成员的使用

需求：字符类中定义了同名的成员变量，如何使用?

```java
//父类，水果类
public class Fruit {
    int price = 20;
}

//子类，苹果类
public class Apple extends Fruit {
    //成员变量
    int price = 10;
    
    public void showPrice() {
        //局部变量
        int price = 5;
        System.out.println(price); //5
        System.out.println(this.price); //10
        System.out.println(super.price); //20
    }
}

//测试类
public class Test {
    public static void main(String[] args) {
        Apple apple = new Apple();
        apple.showPrice();
        
        /*
        	Java中使用变量的规则：
        		遵循"就近原则"，局部位置有就使用，
        		没有就去本类的成员位置找，有就使用,
        		没有就去父类的成员位置找，有就使用,
        		没有就报错.
        */
    }
}
```



## 四.this和super的区别

|      | this         | super              |
| ---- | ------------ | ------------------ |
| 本质 | 对象         | 父类内存空间的标识 |
| 用法 | 从本类开始找 | 从父类开始找       |

## 五.继承关系中类成员的使用

### 1.继承关系中子父类成员方法的使用

需求：子父类中定义了同名的成员方法，如何使用？

分析：

​	天下武功，无非是内功和招式。

​	定义武功类Martial，定义练习内功和招式的成员方法：internalStrength(), stroke()

​	闪电五连鞭，讲究以柔克刚，定义闪电五连鞭类JieHuaFa()，继承Martial类

​	闪电五连鞭的修炼，不仅要练习基本内功，还要能以柔克刚，需要扩展父类方法；简单的招式已经不足为用，

​	必须有闪电五连鞭这样的大招才能打败英国大理石，需要重新实现父类方法

```java
/*
	父类，武功类
*/
public class Martial {
    //练习内功
    public void internalStrength() {
		System.out.println("练习内功");
    }
    
    //练习招式
    public void stroke() {
		System.out.println("练习招式");
    }
}

//子类：闪电五连鞭
public class JieHuaFa extends Martial {
    //练习内功
    public void internalStrength() {
		//这里是在调用父类的成员方法
        super.internalStrength();
        System.out.println("以柔克刚"); 
    }
    
    //练习招式
    public void stroke() {
		System.out.println("接!化!发!")
    }
}

//测试类
public class Test {
    public static void main(String[] args) {
        JieHuaFa jhf = new JieHuaFa();
        jhf.internalStrength();
        jhf.stroke();
    }
}
```

### 2.子父类构造方法的使用

需求：创建对象时，构造方法是如何被调用的？

分析：

​	定义父类Person，在默认无参构造中输出语句

​	定义子类Worker，继承Person，在默认无参构造中输出语句

```java
public class Person {
    public Person() {
        System.out.println("person");
    }
}

public class Worker extends Person {
    public Worker() {
        super(); //调用父类默认无参构造
        System.out.println("worker");
    }
}
```

结论

创建子类对象时，优先调用父类构造方法

子类构造方法的第一行，隐含语句super(),用于调用父类默认无参构造

需求：若父类不存在默认无参构造方法怎么办？

分析：子类创建对象时，必须先初始化该对象的父类内容，若父类中不存在默认无参构造，须手动调用父类其他构造。

```java
//父类
public class Person { 
    public Person(String name) {
        System.out.println("Person：" + name);
    }
}

//子类
public class Worker extends Person {
    public Woker() {
        super("JOJO"); //用于初始化父类成员
        System.out.println("Worker类的空参构造");
    }
}
```



## 六.Java中继承的特点

### 1.单继承

Java只支持类的单继承，但是支持多层（重）继承
Java支持接口的多继承，语法为：

​	接口A extends 接口B, 接口C, ... 

### 2.私有成员不能继承

只能继承父类的非私有成员（成员变量，成员方法）

### 3.构造方法不能继承

构造方法用于初始化本类对象。

创建子类对象时，需要调用父类构造初始化该对象的父类内容若父类构造可以被继承，该操作会造成调用的混乱。

### 4.继承体现了"is a"的关系

子类符合"is a(是一个)"父类的情况下，才使用继承，其他情况不建议使用