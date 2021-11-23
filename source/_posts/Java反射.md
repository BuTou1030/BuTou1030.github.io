---
title: Java反射
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# Java反射

<!-- more -->

## 一.为什么要有反射？

反射(reflection)通常用于使程序有能力检查或修改在Java虚拟机上运行的应用程序，由于它功能强，需要熟练掌握Java技术，有可能带来一些副作用，所以初学者能够不用反射就不用.

## 二.获取Class对象（字节码文件对象）的三种方式

### 1.Object类的getClass()方法

```java
Class clazz = 对象名.getClass();
```

### 2.类的静态属性

```java
Class clazz = 类名.class;
```

### 3.Class类的静态方法

```java
Class clazz = Class.forName("类的正名");
/*
	正名：包名 + 类名
	注意：
		一个源文件（.java文件）对应一个字节码文件对象
*/
```

### 4.举例

```java
public class ReflectDemo1 {
    public static void main(String[] args) throws ClassNotFoundException {
        //需求：获取Class对象
        //方式一：Object类的getClass()方法
        Student stu = new Student();
        Class clazz1 = stu.getClass();
        
        //方式二：类的静态属性
        Class clazz2 = Student.class;
        
        //方式三：Class类的静态方法
        Class clazz3 = Class.forName("cn.butou.demo1.Student");
        
        //验证这三个Class对象是同一个对象
        System.out.println(clazz1 == clazz2); //true
        System.out.println(clazz2 == clazz3); //true
    }
}

//学生类
public class Student {}
```

## 三.获取构造器对象

### 1.Class类中的成员方法

public Constructor getConstructor(Class... params);			根据参数列表，获取对应的构造器对象(仅限公共构造函数)

public Constructor getDeclaredConstructor(Class... params);			根据参数列表，获取对应的构造器对象（包含私有构造函数）

public Constructor[] getConstructors();			获取此类所有的构造函数（不含私有）

### 2.Constructor类：构造器类

概述：属于java.base模块下的java.lang.reflect包下的类.

成员方法：

public String getName();			获取构造函数名

public T newInstances(Object... params);			根据此构造函数和指定参数创建对象

### 3.举例

```java
public class ReflectDemo1 {
    public static void main(String[] args) throws Exception {
        //需求，通过反射的方式创建：Student类型的对象
        //1.获取Student类的字节码文件对象.
        Class clazz = Class.forName("cn.butou.demo1.Student");
        
        //2.根据第一步获取到的字节码文件对象，获取指定的构造器对象.
        //2.1获取公共的无参构造
        Constructor con1 = clazz.getConstructor();
        System.out.println(con1);
        
        //2.2获取公共的有参构造
        Constructor con2 = clazz.getConstructor(String.class);
        System.out.println(con2);
        
        //2.3获取私有的有参构造
        Constructor con3 = clazz.getDeclaredConstructor(int.class);
        System.out.println(con3);
        
        //2.4获取Student类的所有公共的构造函数
        System.out.println("-----------");
        Constructor[] cons = clazz.getConstructors();
        //遍历数组
        for (Constructor con : cons) {
            System.out.println(con);
        }
        
        //获取构造器的名字，看看它是哪个类的构造
        String name = con2.getName();
        System.out.println(name);
        
        //3.根据构造器对象和函数，创建对应的Student对象
        Student stu = (Student)con2.newInstance("张三");
        
        //4.打印结果
        System.out.println(stu);
    }
}

//学生类
public class Student {
    //公共的无参构造
    public Student() {}
    
    //公共的带参构造
    public Student(String name) {
        System.out.println("您录入的姓名是：" + name);
    }
    
    //私有的带参构造
    private Student(int age) {
        System.out.println("您录入的年龄是：" + age);
    }
}
```

## 三.获取成员方法对象

### 1.Class类中的成员方法

public Method getMethod(String name, Class... params)			返回一个Method对象，仅公共成员方法

public Method getDeclaredMethod(String name, Class... params)			返回一个Method对象，可获取私有成员方法

public Method getMethods()			返回此类所有（不含私有）方法的数组

### 2.Method类

概述：方法类，用来表示所有的成员方法（对象）的，属于java.base模块下的java.lang.reflect包下的类.

成员方法：

public String getName();			获取成员方法名

public Object invoke(Object obj, Object...params)			调用指定方法，obj表示该类的对象，params表示调用该方法所需的参数

public void setAccessible(boolean flag);			是否开启暴力反射（true：开启）

### 3.举例

```java
public class ReflectDemo1 {
    public static void main(String[] args) throws Exception {
		//需求：通过反射获取Student类中的成员方法并调用.
        //1.获取Student类的字节码文件对象.
        Class clazz = Class.forName("cn.butou.demo1.Student");
        
        //2.获取该类的构造器对象，然后创建Student类的对象
        Constructor con = clazz.getConstructor();
        Student stu = (Student)con.newInstance();
        
        //3.获取该类的成员方法对象，然后调用此方法
        //3.1调用公共的空参方法
        Method method1 = clazz.getMethod("show1");
        //打印方法对象
        System.out.println(method1);
        //打印方法名
        System.out.println(method1.getName());
        //调用此方法
        method1.invoke(stu);
        System.out.println("-------------");
        
        //3.2调用公共的带参方法
        Method method2 = clazz.getMethod("show2", int.class);
        //调用方法
        method2.invoke(stu, 100);
        System.out.println("-------------");
        
        //3.3调用私有的带参方法
        Method method3 = clazz.getDeclaredMethod("show3", int.class, int.class);
        //开启暴力反射
        method3.setAccessible(true);
    }
}

//学生类
public class Student {
    //公共的无参方法
    public void show1() {
        System.out.println("我是公共的带参方法");
    }
    
    //公共的带参方法
    public void show2(int a) {
        System.out.print("a：" + a);
    }
    
    //私有的带参方法
    private int show3(int a, int b) {
        System.out.println("我是私有的带参方法");
        return a + b;
    }
}
```

## 四.获取域（属性，成员变量）对象

### 1.Class类的成员方法：

public Field getField(String name)			返回一个Field对象，仅公共成员变量

public Field getDeclaredField(String name)			返回一个Field对象，可获取私有成员变量

public Field getDeclaredFields()			返回此类所有(含私有)成员变量的数组

### 2.Field类

概述：属性类，用来表示所有的域（属性，成员变量）对象的.

成员方法：

​	public void setAccessible(boolean flag);			是否开启暴力反射（true： 是)

​	public void set(Object obj, object value);			设置obj对象的指定属性

### 3.举例

```java
public class ReflectDemo1 {
    public static void main(String[] args) throws Exception {
        //需求：通过反射获取成员变量并使用
        //1.获取Student类的字节码文件对象.
        Class clazz = Class.forName("cn.butou.demo1.Student");
        
        //2.通过字节码文件对象获取构造器对象，然后创建学生类对象.
        Constructor con = clazz.getConstructor();
        Student stu = (Student)con.newInstance();
        //Student stu2 = (Student)clazz.getConstructor().newInstance();
        //链式编程
		
        //3.设置学生对象的各个属性值
        //3.1设置姓名
        Field field1 = clazz.getField("name");
        field1.set(stu, "张无忌");
        
        //3.2设置年龄
        Field field2 = clazz.getDeclaredField("age");
        //开启暴力反射
        field2.setAccessible(true);
        field2.set(stu, 30);
        
        //4.打印学生对象
        System.out.println(stu);
    }
}

//学生类
public class Student {
    //公共的属性
    public String name;
    //私有的属性
	private int age;
    
    //用来打印对象的各个属性值的.
    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```







