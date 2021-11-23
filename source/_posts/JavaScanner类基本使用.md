---
title: JavaScanner类基本使用
copyright: true
date: 2021-03-28 16:34:41
toc: true
tags: [后端,JAVA]
categories: [后端,JAVA]
---

# JavaScanner类基本使用

<!-- more -->

## 一.Scanner的概念

扫描器，即可以通过Scanner类扫描用户在控制台录入的数据

## 二.键盘录入数据步骤

```java
//第一步：导包
import java.util.Scanner;

public class ScannerDemo {
    public static void main(String[] args) {
        //第二步：创建键盘录入对象
        Scanner sc = new Scanner(System.in);
        
        //给出提示
		System.out.println("请输入一个整数：");
        
        //第三步：接收数据
        int i = sc.nextInt(); //此代码执行时，控制台会等待用户录入数据
        
        //把获取的数据输出
		System.out.println("i：" + i);
    }
}
```



