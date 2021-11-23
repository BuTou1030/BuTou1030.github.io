---
title: Java多态
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# Java多态

<!-- more -->

## 一.多态概述

### 1. 什么是多态？

多种状态，同一对象在不同情况下表现出不同的状态或行为

### 2.Java中实现多态的步骤

要有继承（或实现）关系

要有方法重写

父类引用指向子类对象（is a关系)

### 3.举例

```java
//测试类
/*
	动物类案例：
		已知父类Animal，成员变量为：姓名，成员方法为：eat()方法.
		其中一子类Dog类，请用该案例模拟多态.
*/
public class Test {
    public static void main(String[] args) {
        //需求：演示多态
        /*
        	Java中实现多态的三个步骤：
        	1.要有继承（或者）实现关系
        	2.要有方法重写
        	3.要有父类引用指向子类对象
        */
        //多态
        Animal an = new Dog();
    }
}

//定义父类
public class Animal {
    //姓名
    private String name;
    
    //空参构造
    public Animal() {}
    
    //全参构造
    public Animal(String name) {
        this.name = name;
    }
    
    //getXxx(), setXxx()
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
    
    //成员方法
    public void eat() {
        System.out.println("吃饭");
    }
}

//Animal类的子类
public class Dog extends Animal {
    //需求：因为狗吃骨头，所以要优化父类的eat()方法
    @Override
    public void eat() {
        System.out.println(getName() + "吃骨头");
    }
}
```

## 二.多态关系中成员变量的使用

需求：子父类中定义了同名的成员变量，如何调用？

分析：

​	A: 子父类中定义同名属性name并分别初始化值：String name;

​	B：在测试类中以多态的方式创建对象并打印name属性值：Animal animal = new Dog();

​	C：在测试类中以普通方式创建对象并打印name属性值：Dog dog = new Dog();

```java
public class Test {
    public static void main(String[] args) {
        Animal animal = new Dog();
        System.out.println(animal.name);
        Dog dog = new Dog();
        System.out.println(dog.name);
    }
}
public class Animal {
    String name = "Animal";
}
public class Dog extends Animal {
    String name = "Dog";
}
```

结论：成员变量不能重写

总结方法：在继承关系中，成员变量或方法都应该默认向上看，但使用多态时，需要查看子类是否重写了父类的成员方法因此需要向下看。

## 三.多态的好处和弊端

### 1.多态的好处

可维护性：基于继承关系，只需要维护父类代码，提高了代码的复用性，大大降低了维护程序的工作量

可扩展性：把不同的子类对象都当作父类看待，屏蔽了不同子类对象间的差异，做出通用的代码，以适应不同的需求，实现了向后兼容

### 2.多态的弊端

不能使用子类特有成员

### 3.类型转换

当需要使用子类特有功能时，需要进行类型转换

##### 1.向上转型（自动类型转换）

子类型转换成父类型

Animal animal = new Dog();

##### 2.向下转型（强制类型转换）

父类型转换成子类型

Dog dog = (Dog)animal;

注意事项：

只能在继承层次内进行转换，否则抛出异常(ClassCastException)

将父类对象转换成子类之前，使用instanceof进行检查

A instanceof B == B is a A

```java
public static void main(String[] args) {
    Dog dog = new Dog();
    dog.setName("布鲁斯");
    showAnimal(dog); 
}
public static void showAnimal(Animal animal) {
    if(animal instanceof Dog) {
        Dog dog = (Dog)animal;
        dog.watch();
    }
    animal.eat();
}
```

## 四.抽象类

### 1.抽象类的例子

```java
//将类定义为抽象的：abstract
public abstract class Animal {
    private String name;
    //将eat方法定义为抽象的：abstract
    public abstract void eat();
    //getter, setter
}

public class Mouse extends Animal {
    public void eat() {
		System.out.println(getName() + "吃奶酪");
    }
}

public class Dog extends Animal {
    public void eat() {
        System.out.println(getName() + "吃骨头");
    }
}
```

### 2.抽象类的概念

包含抽象方法的类。用abstract修饰

### 3.抽象方法的概念

只有方法声明，没有方法体的方法。用abstract修饰

### 4.抽象方法的由来

当需要定义一个方法，却不明确方法的具体实现时，可以将方法定义为abstract，具体实现延迟到子类

### 5.抽象类的特点

修饰符：

必须用abstract关键字修饰

修饰符 abstract class 类名{}

修饰符 abstract 返回类型 方法名();

抽象类不能被实例化，只能创建子类对象

抽象类子类的两个选择：

重写父类所有抽象方法

定义成抽象类

### 6.抽象类成员的特点

成员变量：

可以有普通的成员变量

也可以有成员常量(final)

成员方法：

可以有普通方法，也可以有抽象方法

抽象类不一定有抽象方法，有抽象方法的类一定是抽象类（或接口）

构造方法：

像普通类一样有构造方法，且可以重载

## 五.final的作用

修饰方法：该方法不能被重写，不能与abstract共存

修饰变量：最终变量，即常量，只能赋值一次，不建议修饰引用类型数据，因为依然可以通过引用修改对象的内部数据，意义不大

## 六.static关键字

### 1.static的概念

静态的

### 2.static的作用

用于修饰类的成员：

成员变量：类变量

成员方法：类方法

### 3.调用方式

类名.成员变量名;

类名.成员方法名(参数);

### 4.static修饰成员变量

特点：

被本类所有对象共享

注意事项：

随意修改静态变量的值是有风险的，为了降低风险，可以同时用final关键字修饰，即公有静态常量（注意命名的变化）

```java
public final static String DEPARTMENT_NAME = "研发部";
```

### 5.static修饰成员方法

静态方法：

静态方法中没有对象this，所以不能访问非静态成员

静态方法的使用场景：

只需要访问静态成员

不需要访问对象状态，所需参数都由参数列表显示提供

## 七.接口

### 1.接口的概念

接口技术用于描述类具有什么功能，但并不给出具体实现，类要遵从接口描述的统一规则进行定义，所以，接口是对外提供的一组规则，标准。

### 2.接口的定义

定义接口使用关键字interface：

interface 接口名 {}

类和接口是实现关系，用implements表示：

class 类名 implements 接口名

### 3.接口创建对象的特点

接口不能实例化：

通过多态的方式实例化子类对象

接口的子类(实现类)：

可以是抽象类，也可以是普通类

### 4.接口继承关系的特点

接口与接口之间的关系：

继承关系，可以多继承，格式：

接口 extends 接口1，接口2，接口3...

继承和实现的区别：

继承体现的是"is a"的关系，父类中定义共性内容

实现体现的是"like a"的关系，接口中定义扩展功能

### 5.接口成员的特点

#### 1.成员变量的特点

接口没有成员变量，只有公有的，静态的常量：

public static final 常量名 = 常量值;

### 2.接口成员方法的特点

成员方法：

JDK7及以前，公有的，抽象方法：

public abstract 返回值类型 方法名();

JDK8以后，可以有默认方法和静态方法：

public default 返回值类型 方法名() {}

static 返回值类型 方法名() {}

JDK9以后，可以有私有方法：

private 返回值类型 方法名() {}

### 3.接口没有构造方法

接口不能够实例化，也没有需要初始化的成员，所以接口没有构造方法

