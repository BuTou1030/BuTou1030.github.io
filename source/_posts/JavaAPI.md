---
title: JavaAPI
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaAPI

<!-- more -->

## 一.API简介

### 1.什么是API?

Application Programming Interface，应用程序编程接口，这里指的是API文档，通常叫“Java文档”，是Java中提供的类的使用说明书。

JDK11API：https://docs.oracle.com/en/java/javase/11/docs/api/index.html

### 2.为什么学习API文档？

发挥面向对象思想，找到Java提供的对象来实现功能，学习API文档就是学习Java中的类的使用方法。

### 3.Java中组件的层次结构

模块（module）--> 包（package）--> 类或接口（class/interface）

![image-20210325131711384](https://z3.ax1x.com/2021/03/25/6Lqbkt.png)

##### 什么是模块？

module，自JAVA9起提供的一种新的Java基础组件，在包（package）的基础上又进行了一层封装，是包的容器。

JavaSE Modules

​	Java语言的核心类库，其下的模块名多以java开头

JDK Modules

​	Java开发工具相关内容，其下的模块名多以jdk开头

## 二.Object类

### 1.简介

类层次结构最顶层的基类，所有类都直接或间接的继承自Object类，所以，所有的类都是一个Object（对象）。

![ba1367fa9948d183c1a160411dca60f](https://z3.ax1x.com/2021/03/25/6LLHu4.png)

### 2.构造方法

Object()：构造一个对象。所有子类对象初始化时都会优先调用该方法

### 3.成员方法

int hashCode()：返回对象的哈希码值，该方法通过对象的地址值进行计算，不同对象的返回值一般不同

Class<?> getClass()：返回调用此方法对象的运行时类对象（调用者的字节码文件对象）

String toString()：返回该对象的字符串表示

boolean equals()：返回其它某个对象是否于此对象“相等”。默认情况下比较两个对象的引用（地址值），建议重写

```java
public class Test {
    public static void main(String args[]) {
        // 非静态方法的调用方式：通过 对象名.的形式调用
        // 1.创建Object类型的对象
        Object obj1 = new Object();
        Object obj2 = new Object();
        
        // 2.测试Object类中的成员方法.
        // int hashCode()：返回对象的哈希码值，不同对象的哈希码值一般不同.
        int code1 = obj1.hashCode();
        int code2 = obj2.hashCode();
        System.out.println(code1); // 1134712904
        System.out.println(code2); // 985922955
        System.out.println("-------------------------");
        
        // Class<?> getClass()：返回该调用者的字节码文件对象，一个类只有一个字节码文件对象
        Class clazz1 = obj1.getClass();
        Class clazz2 = obj2.getClass();
        System.out.println(clazz1); // class java.lang.Object
        System.out.println(clazz2); // class java.lang.Object
        System.out.println("--------------------------");
        
        // String toString()：返回该对象的字符串表示形式. 默认打印的是地址值，但是不同对象的地址值肯定不同.
        // 地址值的组成：全类名 + @ + 该对象的哈希码的无符号十六进制形式
        String s1 = obj1.toString();
        String s2 = obj2.toString();
        System.out.println(s1); // java.lang.Object@43a25848
        System.out.println(s1); // java.lang.Object@3ac3fd8b
        System.out.println("---------------------------");
        
        //boolean equals(); 比较两个对象是否相等，默认比较的是地址值，无意义，子类一般都会重写该方法;
        boolean b1 = obj1.equals(obj2);
        System.out.println(b1);
        
    }
}
```

### 4.JavaBean重写Object类的方法

需求：开发中通常需要将对象转成字符串形式进行传输，也需要对即将使用的对象进行相等判断。定义标准JavaBean类，重写toString和equals方法。

步骤：

定义标准JavaBean类Student，属性：id,name,score

重写toString()：该对象的字符串表现形式，一般都是包含所有属性值且具有一定的格式的字符串

重写equals()：可以通过关键属性（id）来确定该类的两个对象是否相同，可以比较所有的属性值

在测试类中创建Student对象并使用

```java
public class Test {
    public static void main(String[] args) {
        //测试toString()方法
        
        //创建学生类对象
        Student s1 = new Student(1, "欧阳修", 66);
        
        // 输出语句直接打印对象，默认调用了该对象的toString()方法.
        System.out.println(s1);
        System.out.println(s1.toString());
        
        //测试equals()方法
        Student s2 = new Student(10, "欧阳修", 66);
        boolean b1 = s1.equals(s2);
        System.out.println(b1);
    }
}
```

```java
package cn.butou.demo2;

// 学生类
public class Student {
    // 成员变量 
    private int id; // 编号
    private String name; // 姓名
    private int score; // 成绩
    // 构造方法
    public Student() {
        
    }
    public Student(int id, String name, int score) {
       this.id = id;
       this.name = name;
       this.score = score;
    }
    
    //成员方法
    private int getId() {
        return id;
    }
    
    public void setId(int id) {
        this.id = id;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name  = name;
    }
    
    public int getScore() {
        return score;
    }
    
    public void setScore(int score) {
        this.score = score;
    }
    
    //toString(), 用来将对象转成其对应的字符串形式.
    @Override
    public String toString() {
        return "Student{" +
               "id="  + id + 
               ", name='" + name + '\'' + 
               ", score=" + score + 
               '}';
    }
    //equals()方法，用来比较两个对象是否相同的.
    @Override
    public boolean equals(Object o) {
        // this：s1 o：s2
        // 比较俩个对象的地址值是否相同，提高效率
        if(this == o) return true;
        // 判断要比较的两个对象是否是同一个类型的对象.
        if(o == null || getClass() != o.getClass()) return false;
        // 向下转型，正常的逻辑代码.
        Student student = (Student) o;
        return id == student.id && 
            		score == student.score &&
            		name.equals(student.name);
    }
}
```

## 三.Scanner类

### 1.简介

扫描器。能够解析字符串（String）和基本类型的数据

![97b8d3d21c4c9cb50f9fc8ce2713eeb](https://z3.ax1x.com/2021/03/25/6XikWQ.png)

### 2.构造方法

Scanner(InputStream)：构造一个扫描器对象，从指定输入流中获取参数System.in，对应键盘录入

### 3.成员方法

hasNextXxx()：判断是否还有下一个输入项，其中Xxx可能是任意基本数据类型，返回结果为布尔类型

nextXxx()：获取下一个输入项，其中Xxx可能是任意基本数据类型，返回对应类型的数据

String nextLine()：获取下一行数据。以换行符作为分隔符。

String next()：获取下一个输入项，以空白字符作为分隔符，空白字符：空格，tab，回车等

```java
public class Test {
    public static void main(String[] args) {
        // 创建Scanner类型的对象（注意：要导包）
        // System.in；标准的输入流，默认指向键盘.
        Scanner sc = new Scanner(System.in);
        
        // 接收整数.
        System.out.println("请录入一个整数：");
        // 为了解决（避免）InputMismatchException异常，可以加入一个判断
        if(sc.hasNextInt()) { // 判断下一个录入的是否是整数，如果是，结果就是true
            int num = sc.nextInt();
            System.out.println("num：" + num);
        }
        
        // 接收字符串类型的数据
        System.out.println("请录入一个字符串：");
        String str1 = sc.nextLine(); // 结束标记是：换行符
        System.out.println("str1：" + str1);
        
        String str2 = sc.next();	// 结束标记：空白字符（空格，tab，换行符）
        System.out.println("str2：" + str2);
        
    } 
}
```

## 四.String类

### 1.简介

字符串。每一个字符串对象都是常量。

![d9324328a82d2ec9d81cc0acfe4342d](https://z3.ax1x.com/2021/03/25/6XniFI.png)

### 2.构造方法

String(byte[])：构造一个String对象，将指定字节数组中的数据转化成字符串

String(char[])：构造一个String对象，将指定字符数组中的数据转化成字符串

### 3.成员方法

#### 1）判断功能

boolean equals(String)：判断当前字符串与给定字符串是否相同，不区分大小写

boolean equalsIgnoreCase(String)：判断当前字符串与给定字符串是否相同，不区分大小写

boolean startsWith(String)：判断是否以给定字符串开头

boolean isEmpty()：判断字符串是否为空

```java
public class Test {
    public static void main(Stirng[] args) {
        // 测试 构造方法
        // 1.将指定的字节数组转成字符串
        // 'a'：97
        byte[] bys = {97, 98, 99};
        String s1 = new String(bys);
        System.out.pritln("s1：" + s1); // abs
        
        // 2.将指定字符数组转成字符串
        char[] chs = {'h', 'e', 'l', 'l', 'o'};
        String s2 = new String(chs);
        System.out.println("s2：" + s2);
        
        // 在实际开发中，String类非常非常常用，每次都new很麻烦，于是针对String的语法进行优化，省去了new操作
        String s3 = "abc"; //免new
        
        // 测试成员方法
        String str1 = "abc";
        String str2 = "ABC";
        // boolean equals(String)：判断当前字符串与给定字符串是否相同，不区分大小写
        boolean b1 = str1.equals(str2);
        System.out.println("equals()：" + b1);
        // boolean equalsIgnoreCase(String)：判断当前字符串与给定字符串是否相同，不区分大小写
        boolean b2 = str1.equalsIgnoreCase(str2);
        System.out.println("equalsIgnoreCase()：" + b2);
        // boolean startsWith(String)：判断是否以给定字符串开头
        // 需求：判断字符串str1，是否已字符串"ab"开头
        boolean b3 = str1.startsWith("ab");
        System.out.println("startWith()：" + b3);
        // boolean isEmpty()：判断字符串是否为空
        boolean b4 = str1.isEmpty();
        System.out.println("isEmpty()：" + b4);
    } 
}
```

#### 2）获取功能

int length()：获取当前字符串的长度

char charAt(int index)：获取指定索引位置的字符

int indexOf(String)：获取指定字符（串）第一次出现的索引

int lastIndexOf(String)：获取指定字符（串）最后一次出现的索引

String substring(int)：获取指定索引位置（含）之后的字符串

String substring(int, int)：获取从索引start位置（含）起至索引end位置（不含）的字符串

```java
public class Test {
    public static void main(String[] args) {
        // 定义一个字符串
        String str = "java Hello java";
        
        // int length()：获取当前字符串的长度
        int length = str.length();
        System.out.println(str.length());
        
        // char charAt(int index)：获取指定索引位置的字符
        char ch = str.charAt(1);
        System.out.println(ch);
        
        // int indexOf(String)：获取指定字符（串）第一次出现的索引
        // 需求：字符'a'第一次出现的位置
        int index1 = str.indexOf('a');
        System.out.println("index1：" + index1);
        
        // int lastIndexOf(String)：获取指定字符（串）最后一次出现的索引
        // 需求：字符'a'最后一次出现的位置
        int index2 = str.lastIndexOf('a');
        System.out.println("index2：" + index2);
        
        // String substring(int)：获取指定索引位置（含）之后的字符串
        // 需求：获取从索引5开始的所有元素
        String s1 = str.substring(5);
        System.out.println("s1：" + s1); // Hello java
        
        // String substring(int, int)：获取从索引start位置（含）起至索引end位置（不含）的字符串
        //需求：获取索引5，10的所有元素
        String s2 = str.substring(5,10);
        System.out.println("s2：" + s2); // Hello
    } 
}
```

#### 3）转换功能

byte[] getBytes()：将字符串转换成字节数组

char[] toCharArray()：将字符串转换成字符数组

static String valueOf(..)：将指定类型数据转换成字符串

String replace(old, new)：将指定字符（串）替换成新的字符（串）

String[] split(String)：切割字符串，返回切割后的字符串数据，原字符串不变

String trim()：去掉字符串两端的空白字符

```java
public class Test {
    public static void main(String[] args) {
        // 定义一个字符串
        String s1 = "abc";
        
        // byte[] getBytes(): 将字符串转换成字节数组
        byte[] bys = s1.getBytes(); // 97, 98, 99
        for(int i = 0; i < bys.length; i ++) {
            System.out.println(bys[i]);
        }
        System.out.println("----------------");
        
        // char[] toCharArray(): 将字符串转换成字符数组
        char[] chs = s1.toCharArray(); // 'a', 'b', 'c'
        for(int i = 0; i < chs.length; i ++) {
            System.out.println(chs[i]);
        }
        System.out.println("-----------------");
        
        // static String valueOf(...)：将指定类型数据转换成字符串
        // 整数123 --> 字符串"123"
        String s2 = String.valueOf(123);
        System.out.println(s2 + 4);
        // 在实际开发中，上述的方式基本上都会用下边的代码替代
        String s3 = "" + 123;
        System.out.println(s3 + 4);
        
        // String replace(old, new)：将指定字符（串）替换成新的字符（串）
        String s4 = "abc abc abc";
        String s5 = s4.replace('b', 'd');
        System.out.println("s5：" + s5);
        
        // String[] split(String)：切割字符串，返回切割后的字符串数据，原字符串不变
        // 将字符串s4，按照空格进行切割
        String[] arr = s4.split(" ");
        for(int i = 0; i < arr.length; i ++) {
            System.out.println(arr[i]);
        }
        System.out.println("-------------------");
        
        // String trim()：去掉字符串两端的空白字符
        String s6 = "  a   b   c  ";
        String s7 = s6.trim();
        System.out.println("s6：" + s7);
        System.out.println("s7：" + s7);
        
    }
}
```

## 五.StringBuilder和StringBuffer类

### 1.简介

可变字符序列，用于构造字符串对象。内部使用自动扩容的数组操作字符串数据。StringBuilder和StringBuffer使用相同的API。

### 2.构造方法

StringBuilder()：构造一个空的StringBuilder容器

StringBuilder(String)：构造一个StringBuilder容器，并添加指定字符串

### 3.成员方法

StringBuilder append(...)：将任意数据添加到StringBuilder容器中，返回自身

String toString()：将当前StringBuilder容器转成字符串



![d24ab20bd39fe76055915314334114e](https://z3.ax1x.com/2021/03/25/6XNra6.png)

```java
public class Test {
    public static void main(String[] args) {
        //测试构造方法
        //测试空参构造
        StringBuilder sb = new StringBuilder();
        StringBuilder sb2 = sb.append("abc");
        System.out.println("sb：" + sb); // abc
        System.out.println("sb；" + sb2); // abc
        
        //需求：将String类型的"abc"转成StringBuilder类型的对象
        StringBuilder sb3 = new StringBuilder("abc");
        System.out.println("sb3：" + sb3);
        System.out.println("-------------------");
        
        //测试成员方法
        //需求：将三个字符串拼接成一个新的字符串：Hello Java World
        StringBuilder sb4 = new StringBuilder();
        sb4.append("Hello");
        sb4.append("Java");
        sb4.append("World");
        System.out.println("sb4：" + sb4); // HelloJavaWorld
        System.out.println("------------");
        String s = sb4.toString();
        System.out.println("字符串s：" + s); // HelloJavaWorld
    } 
}
```

 ### 4.String、StringBuffer与StringBuilder的区别。

String表示内容不可修改的字符串，StringBuffer表示内容可以修改的字符串，

String覆盖了equals（）方法和hashcode（）方法，而StringBuffer没有覆盖两个方法，，所以StringBuffer对象存储到java集合类中时会出现问题。

StringBulider也表示内容可以修改的字符串，但是其线程是不安全的，运行效率高。


String不可变很简单，如下图，给一个已有字符串"abcd"第二次赋值成"abcedl"，不是在原内存地址上修改数据，而是重新指向一个新对象，新地址。

![img](https://pic2.zhimg.com/80/46c03ae5abf6111879423f38375207cc_720w.jpg?source=1940ef5c)

## 六.Date类和Calendar类

### 1.简介

日期和日历类，用于操作日期相关信息。

![date](https://z3.ax1x.com/2021/03/28/cpnR9H.png)

### 2.构造方法

Date()：构造一个日期对象，当前系统时间，精确到毫秒

Date(long)：构造一个日期对象，时间为自“1970年1月1日00:00:00 GMT“起，至指定参数的毫秒数

### 3.成员方法

Date：

long getTime()：将日期对象转换成对应时间的毫秒值

Calendar：

static Calendar getInstance()：根据当前系统时区和语言环境获取日历对象

int get(int field)：返回给定日历字段的值

void set(int field, int value)：将给定的日历字段设置为指定的值

```java
public class Test {
    // 测试Date类
    // 测试空参构造，采用当前操作系统的默认时间
    Date date1 = new Date();
    System.out.println("date1：" + date1);
    
    // 获取当前操作系统时间的毫秒值
    long time = date1.getTime();
    System.out.println("time："  + time);
    
    // Sun Jun 06 17:04:39 CST 2066 --> 3043040679456
    // 创建一个指定的时间
    Date date2 = new Date(3043040679456);
    System.out.println("date2："  + date2);
}
```

```java
public class Test2 {
    // 创建Calendar类型的对象
    Calendar c = Calendar.getInstance();
    System.out.println(c);
    
    // 获取年月日的信息
    int year = c.get(Calendar.YEAR);
    int month = c.get(Calendar.MONTH); // Java中使用0-11的数字表示月份，对应1-12月
    int day = c.get(Calendar.DATE);
    System.out.println(year + "年" + (month + 1) + "月" + day + "日");
    System.out.println("------------------------");
    
    // 设置指定时间为：2022年2月2日
    //c.set(Calendar.YEAR, 2022);
    //int year2 = c.get(Calendar.YEAR);
    c.set(2022, 1, 2);
    int year2 = c.get(Calendar.YEAR);
    int month2 = c.get(Calendar.MONTH); // Java中使用0-11的数字表示月份，对应1-12月
    int day2 = c.get(Calendar.DATE);
    System.out.println(year + "年" + (month + 1) + "月" + day + "日");
    
}
```



## 七.基本类型的包装类

### 1.简介

基本数据类型不是对象，所以Java针对基本类型提供了对应的包装类，以对象的形式来使用。

![baozhuanglei](https://z3.ax1x.com/2021/03/28/cpQjiT.md.png)

### 2.装箱和拆箱

装箱：基本类型转包装类型（对象类型）

拆箱：包装类型（对象类型）转基本类型

### 3.成员方法

static 基本类型 parseXxx(String)：将字符串类型的数据转成对应的基本类型

注意：除了Charater类以外，其他的7种包装类都有parseXXX()方法，因为如果字符串想转换成char类型的数据，可以通过：String类中的方法toCharArray()，charAt()方法

```java
public class Test {
    public static void main(String[] args) {
        // 因为变量a属于基本类型，不能通过对象名.的形式调用方法
        // 解决方案：将其转换成对应的包装类（引用类型）即可.
        int a = 10;
        
        // 装箱
        Integer i1 = new Integer(20);
        // 拆箱
        int b = i1.intValue();
        System.out.println(i1);
        System.out.println(b);
        System.out.println("--------------");
        
        // JDK5的新特性，自动拆装箱
        Integer i2 = 30; // 装箱
        int c = i2; // 拆箱
        System.out.println("---------------------");
        
        // 需求：将字符串类型的"10"，转换成int类型的10
        String s = "10";
        int num = Integer.parseInt(s);
        System.out.println("num：" + num);
        System.out.println("num + 100 = " + (num + 100));
    }
}
```

